---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：使用 ASP.NET MVC 5 應用程式中的 EF 處理平行存取
description: 本教學課程說明當多個使用者同時更新相同的實體時，如何使用開放式平行存取來處理衝突。
author: tdykstra
ms.author: riande
ms.topic: tutorial
ms.date: 01/15/2019
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 43c5fdff5601c9bff32300d3460de0079a498d28
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616106"
---
# <a name="tutorial-handle-concurrency-with-ef-in-an-aspnet-mvc-5-app"></a>教學課程：使用 ASP.NET MVC 5 應用程式中的 EF 處理平行存取

在先前的教學課程中，您已瞭解如何更新資料。 本教學課程說明當多個使用者同時更新相同的實體時，如何使用開放式平行存取來處理衝突。 您可以變更使用 `Department` 實體的網頁，使其能夠處理並行錯誤。 下列圖例顯示了 [編輯] 和 [刪除] 頁面，包括一些發生並行衝突時會顯示的訊息。

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 了解並行衝突
> * 加入開放式平行存取
> * 修改部門控制器
> * 測試並行處理
> * 更新 [刪除] 頁面

## <a name="prerequisites"></a>Prerequisites

* [非同步的預存程序](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="concurrency-conflicts"></a>並行衝突

當一名使用者為了編輯而顯示了實體的資料，然後另一名使用者在第一名使用者所作出的變更寫入到資料庫前便更新了相同實體的資料時，便會發生並行衝突。 若您沒有啟用針對這類衝突的偵測，最後更新資料庫的使用者所作出的變更便會覆寫前一名使用者所作出的變更。 在許多應用程式中，這類風險是可接受的：若僅有幾名使用者或僅有幾項更新，或覆寫變更的風險並不是那麼的重大，則為了處理並行而耗費的程式設計成本可能會大於其所能帶來的利益。 在此情況下，您便不需要設定應用程式來處理並行衝突。

### <a name="pessimistic-concurrency-locking"></a>封閉式平行存取（鎖定）

若您的應用程式確實需要防止在並行案例下發生的意外資料遺失，其中一個方法便是使用資料庫鎖定。 這稱為「封閉式*並行*存取」。 例如，在您從資料庫讀取一個資料列之前，您會要求唯讀鎖定或更新存取鎖定。 若您鎖定了一個資料列以進行更新存取，其他使用者便無法為了唯讀或更新存取而鎖定該資料列，因為他們會取得一個正在進行變更之資料的複本。 若您鎖定資料列以進行唯讀存取，其他使用者也可以為了唯讀存取將其鎖定，但無法進行更新。

管理鎖定有幾個缺點。 其程式可能相當複雜。 這需要大量的資料庫管理資源，並且可能會隨著應用程式使用者的數量提升而導致效能問題。 基於這些理由，不是所有的資料庫管理系統都支援封閉式並行存取。 Entity Framework 不會提供內建的支援，本教學課程不會示範如何執行此功能。

### <a name="optimistic-concurrency"></a>開放式並行存取

封閉式平行存取的替代方法是*開放式並行*存取。 開放式並行存取表示允許並行衝突發生，然後在衝突發生時適當的做出反應。 例如，John 執行 [部門編輯] 頁面，將英文部門的**預算**金額從 $350000.00 變更為 $0.00。

John 按一下 [**儲存**] 之前，Jane 執行相同的頁面，並將 [**開始日期**] 欄位從9/1/2007 變更為8/8/2013。

John 按一下 [**儲存**]，然後在瀏覽器回到 [索引] 頁面時看到變更，然後按一下 [**儲存**]。 接下來發生的情況便是由您處理並行衝突的方式決定。 一部分選項包括下列項目：

- 您可以追蹤使用者修改的屬性，然後僅在資料庫中更新相對應的資料行。 在範例案例中，將不會發生資料遺失，因為兩名使用者更新的屬性不同。 下一次有人流覽英文部門時，他們會看到 John 和 Jane 的變更—開始日期為8/8/2013，預算為零美元。

    這個更新方法可減少可能導致資料遺失之衝突發生的次數，但卻無法在實體中的相同屬性遭到變更時避免資料遺失。 Entity Framework 是否會以這種方式處理並行衝突，取決於您實作更新程式碼的方式。 通常在 Web 應用程式中，這種方法並不實用，因為它需要您維持大量的狀態，以追蹤實體所有原始的屬性值和新的值。 維持大量狀態可能會影響應用程式的效能，因為它不是需要伺服器資源，就是必須包含在網頁中 (例如隱藏欄位)，或是保存在 Cookie 中。
- 您可以讓 Jane 的變更覆寫 John 的變更。 下一次有人流覽英文部門時，他們會看到8/8/2013 和還原的 $350000.00 值。 這稱之為「用戶端獲勝 (Client Wins)」或「最後寫入為準 (Last in Wins)」案例。 （用戶端的所有值會優先于資料存放區中的內容）。如本節簡介中所述，如果您沒有針對並行處理進行任何編碼，則會自動發生。
- 您可以防止 Jane 的變更在資料庫中更新。 一般來說，您會顯示錯誤訊息、顯示資料的目前狀態，並允許她重新套用她的變更（如果她仍然想要這樣做）。 這稱之為「存放區獲勝 (Store Wins)」案例。 （資料存放區的值會優先于用戶端所提交的值。）在本教學課程中，您將會實行「存放區獲勝」案例。 這個方法可確保沒有任何變更會在使用者收到警示，告知其發生的事情前遭到覆寫。

### <a name="detecting-concurrency-conflicts"></a>偵測並行衝突

您可以藉由處理 Entity Framework 擲回的[OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx)例外狀況來解決衝突。 若要得知何時應擲回這些例外狀況，Entity Framework 必須能夠偵測衝突。 因此，您必須適當的設定資料庫及資料模型。 一部分啟用衝突偵測的選項包括下列選項：

- 在資料庫資料表中，包含一個追蹤資料行，該資料行可用於決定資料列發生變更的時機。 接著，您可以設定 Entity Framework 在 SQL `Update` 的 `Where` 子句或 `Delete` 命令中包含該資料行。

    追蹤資料行的資料類型通常是[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)。 [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)值是每次更新資料列時都會遞增的連續數位。 在 `Update` 或 `Delete` 命令中，`Where` 子句會包含追蹤資料行的原始值（原始資料列版本）。 如果正在更新的資料列已由另一位使用者變更，則 [`rowversion`] 資料行中的值會與原始值不同，因此 `Update` 或 `Delete` 語句因為 `Where` 子句而找不到要更新的資料列。 當 Entity Framework 發現 `Update` 或 `Delete` 命令未更新任何資料列時（也就是受影響的資料列數目為零時），它會將它解釋為並行衝突。
- 設定 Entity Framework 在 `Update` 和 `Delete` 命令的 `Where` 子句中，包含資料表中每個資料行的原始值。

    如同第一個選項，如果資料列中的任何專案在第一次讀取之後已變更，則 `Where` 子句不會傳回要更新的資料列，而 Entity Framework 會將它解釋為並行衝突。 對於具有許多資料行的資料庫資料表而言，這種方法可能會產生非常大的 `Where` 子句，而且可能需要您維護大量的狀態。 如前文所述，維持大量的狀態可能會影響應用程式的效能。 因此通常不建議使用這種方法，並且這種方法也不是此教學課程中所使用的方法。

    如果您想要將此方法實作為平行存取，您必須在您想要追蹤並行的實體中，將[ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx)屬性新增至其中，以標示其所有非主要索引鍵屬性。 這項變更可讓 Entity Framework 在 `UPDATE` 語句的 SQL `WHERE` 子句中包含所有資料行。

在本教學課程的其餘部分，您會將[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)追蹤屬性新增至 `Department` 實體、建立控制器和視圖，並進行測試以確認所有專案都能正常運作。

## <a name="add-optimistic-concurrency"></a>加入開放式平行存取

在*Models\Department.cs*中，新增名為 `RowVersion`的追蹤屬性：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)屬性會指定此資料行將包含在 `Update` 的 `Where` 子句中，以及傳送至資料庫 `Delete` 命令。 屬性稱為[時間戳記](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)，因為舊版的 SQL SERVER 在 sql [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)取代它之前使用 sql[時間戳記](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)資料類型。 [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)的 .net 類型是位元組陣列。

如果您想要使用 Fluent API，您可以使用[IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx)方法來指定追蹤屬性，如下列範例所示：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

由於新增屬性之後，您也變更了資料庫模型，因此您必須再一次進行移轉。 請在套件管理員主控台 (PMC) 中輸入下列命令：

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-department-controller"></a>修改部門控制器

在*Controllers\DepartmentController.cs*中，新增 `using` 語句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

在*DepartmentController.cs*檔案中，將 "LastName" 的全部四個專案都變更為 "FullName"，讓 [部門系統管理員] 下拉式清單包含講師的完整名稱，而不只是 [姓氏]。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

使用下列程式碼，將 `HttpPost` `Edit` 方法的現有程式碼取代：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

若 `FindAsync` 方法傳回 Null，則該部門便已遭其他使用者刪除。 所顯示的程式碼會使用已張貼的表單值來建立部門實體，讓 [編輯] 頁面可以重新顯示，並出現錯誤訊息。 或者，若您選擇只顯示錯誤訊息，而不重新顯示部門欄位，則您也可以不需要重新建立部門實體。

此視圖會將原始 `RowVersion` 值儲存在隱藏欄位中，而方法會在 `rowVersion` 參數中接收它。 在您呼叫 `SaveChanges` 之前，您必須將該原始 `RowVersion` 屬性值放入實體的 `OriginalValues` 集合中。 然後，當 Entity Framework 建立 SQL `UPDATE` 命令時，該命令會包含 `WHERE` 子句，以尋找具有原始 `RowVersion` 值的資料列。

如果 `UPDATE` 命令沒有任何資料列受到影響（沒有任何資料列具有原始的 `RowVersion` 值），則 Entity Framework 會擲回 `DbUpdateConcurrencyException` 例外狀況，而 `catch` 區塊中的程式碼會從例外狀況物件取得受影響的 `Department` 實體。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

此物件具有使用者在其 `Entity` 屬性中輸入的新值，而且您可以藉由呼叫 `GetDatabaseValues` 方法，取得從資料庫讀取的值。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

如果某個人已從資料庫中刪除資料列，則 `GetDatabaseValues` 方法會傳回 null;否則，您必須將傳回的物件轉換為 `Department` 類別，才能存取 `Department` 屬性。 （因為您已經檢查刪除，只有在 `FindAsync` 執行之後和 `SaveChanges` 執行之前刪除部門時，`databaseEntry` 才會是 null）。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

接下來，程式碼會針對每個資料行新增一個自訂錯誤訊息，其資料庫值與使用者在 [編輯] 頁面上輸入的內容不同：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

較長的錯誤訊息會說明發生了什麼事，以及該怎麼做：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

最後，程式碼會將 `Department` 物件的 `RowVersion` 值設定為從資料庫中抓取的新值。 這個新的 `RowVersion` 值會在編輯頁面重新顯示時儲存於隱藏欄位中，並且當下一次使用者按一下 [儲存] 時，只有在重新顯示 [編輯] 頁面之後發生的並行錯誤才會被捕捉到。

在*Views\Department\Edit.cshtml*中，新增隱藏欄位以儲存 `RowVersion` 屬性值，緊接在 `DepartmentID` 屬性的隱藏欄位後面：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="test-concurrency-handling"></a>測試並行處理

執行網站，然後按一下 [**部門**]。

以滑鼠右鍵按一下英文部門的**編輯**超連結，然後選取 [在新索引標籤**中開啟]，** 再按一下英文部門的**編輯**超連結。 這兩個索引標籤會顯示相同的資訊。

變更第一個瀏覽器索引標籤中的欄位，然後按一下 [儲存]。

瀏覽器會顯示索引頁面，當中包含了變更之後的值。

變更第二個瀏覽器索引標籤中的欄位，然後按一下 [**儲存**]。 您會看到一個錯誤訊息：

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

再按一下 [儲存]。 您在第二個 [瀏覽器] 索引標籤中輸入的值，會與您在第一個瀏覽器中變更的資料原始值一起儲存。 您會在索引頁面出現時看到儲存的值。

## <a name="update-the-delete-page"></a>更新 [刪除] 頁面

針對 [刪除] 頁面，Entity Framework 會偵測由其他對部門進行類似編輯的人員所造成的並行衝突。 當 `HttpGet` `Delete` 方法顯示 [確認] 視圖時，此視圖會在隱藏欄位中包含原始的 `RowVersion` 值。 該值接著會提供給使用者確認刪除時所呼叫的 `HttpPost` `Delete` 方法。 當 Entity Framework 建立 SQL `DELETE` 命令時，它會包含具有原始 `RowVersion` 值的 `WHERE` 子句。 如果命令導致零個數據列受到影響（也就是說，在 刪除確認 頁面顯示之後，資料列已變更），則會擲回並行例外狀況，而且會呼叫 `HttpGet Delete` 方法，並將錯誤旗標設定為 `true`，以便重新顯示確認頁面，並出現錯誤訊息。 因為資料列已由另一位使用者刪除，所以可能會影響零個數據列，因此在這種情況下，會顯示不同的錯誤訊息。

在*DepartmentController.cs*中，將 `HttpGet` `Delete` 方法取代為下列程式碼：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

方法會接受一個選用的參數，該參數會指示頁面是否已在發生並行錯誤之後重新顯示。 如果 `true`此旗標，則會使用 `ViewBag` 屬性將錯誤訊息傳送至視圖。

以下列程式碼取代 `HttpPost` `Delete` 方法（名為 `DeleteConfirmed`）中的程式碼：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

在您剛剛取代的 Scaffold 程式碼中，此方法僅會接受一個記錄識別碼：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

您已將此參數變更為模型系結器所建立的 `Department` 實體實例。 這可讓您存取 `RowVersion` 屬性值，以及記錄索引鍵。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

您也將動作方法的名稱從 `DeleteConfirmed` 變更為 `Delete`。 名為 `HttpPost` 的 scaffold 程式碼 `Delete` 方法 `DeleteConfirmed`，為 `HttpPost` 方法提供唯一的簽章。 （CLR 需要多載的方法，才能有不同的方法參數）。簽章是唯一的，您可以使用 MVC 慣例，並將相同的名稱用於 `HttpPost` 和 `HttpGet` delete 方法。

若捕捉到並行錯誤，程式碼會重新顯示刪除確認頁面，並提供一個旗標指示其應顯示並行錯誤訊息。

在*Views\Department\Delete.cshtml*中，將 scaffold 程式碼取代為下列程式碼，以新增 DepartmentID 和 RowVersion 屬性的錯誤訊息欄位和隱藏欄位。 所做的變更已醒目標示。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

此程式碼會在 `h2` 和 `h3` 標題之間新增錯誤訊息：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

它會將 `LastName` 取代為 `Administrator` 欄位中的 `FullName`：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

最後，它會在 `Html.BeginForm` 語句後面加入 `DepartmentID` 的隱藏欄位，並 `RowVersion` 屬性：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

執行 [部門索引] 頁面。 以滑鼠右鍵按一下英文部門的 [**刪除**] 超連結，然後選取 [在新索引標籤**中開啟]，** 然後在第一個索引標籤中，按一下英文部門的**編輯**超連結。

在第一個視窗中，變更其中一個值，然後按一下 [**儲存**]。

[索引] 頁面會確認變更。

在第二個索引標籤中，按一下 [刪除]。

您會看到並行錯誤訊息，並且 Department 值已根據資料庫中的內容重新整理。

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

若您再按一下 [刪除]，則您將會重新導向至 [索引] 頁面，並且系統將顯示該部門已遭刪除。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

如需處理各種平行存取案例之其他方式的詳細資訊，請參閱 MSDN 上的[開放式平行存取模式](https://msdn.microsoft.com/data/jj592904)和[使用屬性值](https://msdn.microsoft.com/data/jj592677)。 下一個教學課程會示範如何針對 `Instructor` 和 `Student` 實體，執行每個階層的資料表繼承。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 了解並行衝突
> * 已新增開放式平行存取
> * 已修改的部門控制器
> * 測試的並行處理
> * 更新 [刪除] 頁面

請前進到下一篇文章，以瞭解如何在資料模型中執行繼承。
> [!div class="nextstepaction"]
> [在資料模型中執行繼承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
