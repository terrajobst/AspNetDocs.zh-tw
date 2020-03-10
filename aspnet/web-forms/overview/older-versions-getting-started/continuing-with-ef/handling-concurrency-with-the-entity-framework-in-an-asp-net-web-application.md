---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: 使用 ASP.NET 4 Web 應用程式中的 Entity Framework 4.0 來處理平行存取 |Microsoft Docs
author: tdykstra
description: 本教學課程系列是以 Entity Framework 4.0 教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 3df5f7d9c8fb22e1ea34fe16560bdb9a1309bb56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632584"
---
# <a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>使用 ASP.NET 4 Web 應用程式中的 Entity Framework 4.0 來處理平行存取

由[Tom 作者: dykstra](https://github.com/tdykstra)

> 本教學課程系列是[以 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 如果您未完成先前的教學課程，做為本教學課程的起點，您可以下載您所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 您也可以下載完整的教學課程系列所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果您有關于教學課程的問題，可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)。

在上一個教學課程中，您已瞭解如何使用 `ObjectDataSource` 控制項和 Entity Framework 來排序和篩選資料。 本教學課程會顯示在使用 Entity Framework 的 ASP.NET web 應用程式中處理並行的選項。 您將會建立專門用來更新講師辦公室指派的新網頁。 您將會在該頁面和您稍早建立的 [部門] 頁面中處理並行問題。

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>並行衝突

當使用者編輯記錄，而另一個使用者在第一次使用者的變更寫入資料庫之前，編輯相同的記錄時，就會發生並行衝突。 如果您未設定 Entity Framework 來偵測這類衝突，則更新資料庫的人員會最後覆寫其他使用者的變更。 在許多應用程式中，這是可接受的風險，而且您不需要設定應用程式來處理可能的並行衝突。 （如果有少數幾個使用者或幾個更新，或如果某些變更遭到覆寫，如果不是真的很重要，則並行處理的程式設計成本可能會超過此權益）。如果您不需要擔心並行衝突，可以略過此教學課程;系列中的其餘兩個教學課程不會取決於您在此版本中建立的任何專案。

### <a name="pessimistic-concurrency-locking"></a>封閉式平行存取（鎖定）

若您的應用程式確實需要防止在並行案例下發生的意外資料遺失，其中一個方法便是使用資料庫鎖定。 這稱為「封閉式*並行*存取」。 例如，在您從資料庫讀取一個資料列之前，您會要求唯讀鎖定或更新存取鎖定。 若您鎖定了一個資料列以進行更新存取，其他使用者便無法為了唯讀或更新存取而鎖定該資料列，因為他們會取得一個正在進行變更之資料的複本。 若您鎖定資料列以進行唯讀存取，其他使用者也可以為了唯讀存取將其鎖定，但無法進行更新。

管理鎖定有一些缺點。 其程式可能相當複雜。 它需要大量的資料庫管理資源，而且可能會造成效能問題，因為應用程式的使用者數目增加（亦即，它無法妥善調整）。 基於這些理由，不是所有的資料庫管理系統都支援封閉式並行存取。 Entity Framework 不會提供內建的支援，本教學課程不會示範如何執行此功能。

### <a name="optimistic-concurrency"></a>開放式並行存取

封閉式平行存取的替代方法是*開放式並行*存取。 開放式並行存取表示允許並行衝突發生，然後在衝突發生時適當的做出反應。 例如，John 執行 [*部門 .aspx* ] 頁面，按一下 [歷程記錄] 部門的 [**編輯**] 連結，並將**預算**量從 $1000000.00 縮減為 $125000.00。 （John 負責管理競爭部門，而且想要釋出自己的部門的金錢）。

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John 按一下**更新**之前，Jane 執行相同的頁面，按一下歷程記錄部門的 [**編輯**] 連結，然後將 [**開始日期**] 欄位從1/10/2011 變更為1/1/1999。 （Jane 管理歷程記錄部門，想要讓它更多資歷）。

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

John 按一下 [**更新**]，然後按一下 [**更新**]。 Jane 的瀏覽器現在會將**預算**金額列為 $1000000.00，但這不正確，因為 John 已將金額變更為 $125000.00。

您可以在此案例中採取的一些動作包括下列各項：

- 您可以追蹤使用者修改的屬性，然後僅在資料庫中更新相對應的資料行。 在範例案例中，將不會發生資料遺失，因為兩名使用者更新的屬性不同。 下次有人流覽歷程記錄部門時，將會看到1/1/1999 和 $125000.00。 

    這是 Entity Framework 中的預設行為，它可以大幅減少可能導致資料遺失的衝突數目。 不過，如果對實體的相同屬性進行競爭變更，此行為並不會避免資料遺失。 此外，這種行為不一定是可行的;當您將預存程式對應至實體類型時，會在資料庫中對實體進行任何變更時，更新所有實體的屬性。
- 您可以讓 Jane 的變更覆寫 John 的變更。 Jane 按一下 [**更新**] 之後，**預算**量會回到 $1000000.00。 這稱之為「用戶端獲勝 (Client Wins)」或「最後寫入為準 (Last in Wins)」案例。 （用戶端的值會優先于資料存放區中的內容）。
- 您可以防止 Jane 的變更在資料庫中更新。 一般來說，您會顯示錯誤訊息、顯示資料的目前狀態，並允許她重新輸入變更（如果她仍然想要的話）。 您可以藉由儲存輸入來進一步將程式自動化，讓她有機會重新套用它，而不必重新輸入。 這稱之為「存放區獲勝 (Store Wins)」案例。 (資料存放區的值會優先於用戶端所提交的值。)

### <a name="detecting-concurrency-conflicts"></a>偵測並行衝突

在 Entity Framework 中，您可以藉由處理 Entity Framework 所擲回的 `OptimisticConcurrencyException` 例外狀況來解決衝突。 若要得知何時應擲回這些例外狀況，Entity Framework 必須能夠偵測衝突。 因此，您必須適當的設定資料庫及資料模型。 一部分啟用衝突偵測的選項包括下列選項：

- 在資料庫中，包含可用來判斷資料列何時變更的資料表資料行。 接著，您可以設定 Entity Framework 在 SQL `Update` 的 `Where` 子句或 `Delete` 命令中包含該資料行。

    這就是 `OfficeAssignment` 資料表中 `Timestamp` 資料行的用途。

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    `Timestamp` 資料行的資料類型也稱為 `Timestamp`。 不過，資料行實際上不會包含日期或時間值。 相反地，此值是每次更新資料列時都會遞增的連續數位。 在 `Update` 或 `Delete` 命令中，`Where` 子句會包含原始 `Timestamp` 值。 如果正在更新的資料列已由另一位使用者變更，`Timestamp` 中的值會與原始值不同，因此 `Where` 子句不會傳回任何要更新的資料列。 當 Entity Framework 發現目前的 `Update` 或 `Delete` 命令未更新任何資料列（也就是說，當受影響的資料列數目為零時），它會將它解釋為並行衝突。
- 設定 Entity Framework 在 `Update` 和 `Delete` 命令的 `Where` 子句中，包含資料表中每個資料行的原始值。

    如同第一個選項，如果資料列中的任何專案在第一次讀取之後已變更，則 `Where` 子句不會傳回要更新的資料列，而 Entity Framework 會將它解釋為並行衝突。 這個方法與使用 `Timestamp` 欄位一樣有效率，但可能沒有效率。 對於具有許多資料行的資料庫資料表，可能會產生非常大的 `Where` 子句，而且在 web 應用程式中，它可能會要求您維護大量的狀態。 維護大量的狀態可能會影響應用程式效能，因為它可能需要伺服器資源（例如會話狀態），或必須包含在網頁本身中（例如，檢視狀態）。

在本教學課程中，您將針對沒有追蹤屬性（`Department` 實體）的實體，以及具有追蹤屬性（`OfficeAssignment` 實體）之實體的開放式平行存取衝突，加入錯誤處理。

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>在沒有追蹤屬性的情況下處理開放式平行存取

若要針對沒有追蹤（`Timestamp`）屬性的 `Department` 實體執行開放式平行存取，您將完成下列工作：

- 變更資料模型，以啟用 `Department` 實體的並行追蹤。
- 在 `SchoolRepository` 類別中，處理 `SaveChanges` 方法中的平行存取例外狀況。
- 在 [*部門 .aspx* ] 頁面中，向使用者顯示一則訊息，指出嘗試的變更失敗，以處理並行例外狀況。 使用者接著可以查看目前的值，然後重試變更（如果仍然需要）。

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>在資料模型中啟用並行追蹤

在 Visual Studio 中，開啟您在本系列的上一個教學課程中使用的 Contoso 大學 web 應用程式。

開啟*SchoolModel*，然後在 [資料模型設計工具] 中，以滑鼠右鍵按一下 [`Department`] 實體中的 [`Name`] 屬性，然後按一下 [**屬性**]。 在 [**屬性**] 視窗中，將 [`ConcurrencyMode`] 屬性變更為 [`Fixed`]。

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

對其他非主要索引鍵純量屬性（`Budget`、`StartDate`和 `Administrator`執行相同的動作）。（您無法針對導覽屬性執行此動作）。這指定每當 Entity Framework 產生 `Update` 或 `Delete` SQL 命令以更新資料庫中的 `Department` 實體時，`Where` 子句中就必須包含這些資料行（含原始值）。 當 `Update` 或 `Delete` 命令執行時，如果找不到任何資料列，Entity Framework 將會擲回開放式平行存取例外狀況。

儲存並關閉資料模型。

### <a name="handling-concurrency-exceptions-in-the-dal"></a>處理 DAL 中的平行存取例外狀況

開啟*SchoolRepository.cs* ，並為 `System.Data` 命名空間新增下列 `using` 語句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

新增下列新的 `SaveChanges` 方法，以處理開放式平行存取例外狀況：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

如果呼叫這個方法時，發生並行錯誤，則記憶體中實體的屬性值會取代為目前在資料庫中的值。 平行存取例外狀況會重新擲回，讓網頁可以處理它。

在 `DeleteDepartment` 和 `UpdateDepartment` 方法中，以 `SaveChanges()` 的呼叫取代現有的 `context.SaveChanges()` 呼叫，以叫用新方法。

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>處理展示層中的平行存取例外狀況

開啟 [*部門 .aspx* ]，並將 `OnDeleted="DepartmentsObjectDataSource_Deleted"` 屬性加入至 [`DepartmentsObjectDataSource`] 控制項。 控制項的開頭標記現在會如下列範例所示。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

在 `DepartmentsGridView` 控制項中，指定 `DataKeyNames` 屬性中的所有資料表資料行，如下列範例所示。 請注意，這將會建立非常大的檢視狀態欄位，這是為什麼使用追蹤欄位通常是追蹤並行衝突的慣用方式的原因之一。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

開啟*Departments.aspx.cs* ，並為 `System.Data` 命名空間新增下列 `using` 語句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

加入下列新方法，您將從資料來源控制項的 `Updated` 呼叫，並 `Deleted` 事件處理常式來處理並行例外狀況：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

此程式碼會檢查例外狀況類型，如果是並行例外狀況，程式碼會動態建立 `CustomValidator` 控制項，然後在 `ValidationSummary` 控制項中顯示訊息。

從您稍早新增的 `Updated` 事件處理常式呼叫新的方法。 此外，建立新的 `Deleted` 事件處理常式，以呼叫相同的方法（但不會執行任何其他動作）：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>在 [部門] 頁面中測試開放式平行存取

執行 [*部門 .aspx* ] 頁面。

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

按一下資料列中的 [**編輯**]，然後變更 [**預算**] 資料行中的值。 （請記住，您只能編輯您在本教學課程中建立的記錄，因為現有的 `School` 資料庫記錄包含一些不正確資料。 經濟效益部門的記錄是一種可進行實驗的安全。）

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

開啟新的瀏覽器視窗，然後再次執行頁面（將 URL 從第一個瀏覽器視窗的 [位址] 方塊複製到第二個瀏覽器視窗）。

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

在您稍早編輯的相同資料列中按一下 [**編輯**]，並將**預算**值變更為不同的值。

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

在第二個瀏覽器視窗中，按一下 [**更新**]。 **預算**金額已成功變更為此新值。

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

在第一個瀏覽器視窗中，按一下 [**更新**]。 更新失敗。 **預算**金額會使用您在第二個瀏覽器視窗中設定的值重新顯示，而您會看到一則錯誤訊息。

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>使用追蹤屬性處理開放式平行存取

若要處理具有追蹤屬性之實體的開放式平行存取，您將完成下列工作：

- 將預存程式加入至資料模型，以管理 `OfficeAssignment` 的實體。 （追蹤屬性和預存程式不一定要一起使用; 它們只會在這裡分組以進行說明）。
- 將 CRUD 方法新增至 DAL，並針對 `OfficeAssignment` 實體加入 BLL，包括用來處理 DAL 中開放式平行存取例外狀況的程式碼。
- 建立辦公室指派的網頁。
- 在新網頁中測試開放式平行存取。

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>將 OfficeAssignment 預存程式加入至資料模型

在模型設計師中開啟*SchoolModel* ，以滑鼠右鍵按一下設計介面，然後按一下 [**從資料庫更新模型**]。 在 [**選擇您的資料庫物件**] 對話方塊的 [**加入**] 索引標籤中，展開 [**預存程式**] 並選取三個 `OfficeAssignment` 預存程式（請參閱下列螢幕擷取畫面），然後按一下 **[完成]** 。 （當您使用腳本下載或建立預存程式時，它們已經在資料庫中）。

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

以滑鼠右鍵按一下 [`OfficeAssignment`] 實體，然後選取 [**預存程式對應**]。

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

將**Insert**、 **Update**和**Delete**函數設定為使用其對應的預存程式。 針對 `Update` 函數的 `OrigTimestamp` 參數，將**屬性**設定為 `Timestamp`，然後選取 [**使用原始值**] 選項。

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

當 Entity Framework 呼叫 `UpdateOfficeAssignment` 預存程式時，它會在 `OrigTimestamp` 參數中傳遞 `Timestamp` 資料行的原始值。 預存程式會在其 `Where` 子句中使用此參數：

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

預存程式也會在更新之後選取 `Timestamp` 資料行的新值，讓 Entity Framework 可以讓記憶體中的 `OfficeAssignment` 實體與對應的資料庫資料列同步。

（請注意，刪除 office 指派的預存程式沒有 `OrigTimestamp` 參數。 因此，Entity Framework 無法在刪除實體之前，先確認其是否已變更。）

儲存並關閉資料模型。

### <a name="adding-officeassignment-methods-to-the-dal"></a>將 OfficeAssignment 方法新增至 DAL

開啟*ISchoolRepository.cs* ，並為 `OfficeAssignment` 實體集新增下列 CRUD 方法：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

將下列新方法新增至*SchoolRepository.cs*。 在 `UpdateOfficeAssignment` 方法中，您可以呼叫本機 `SaveChanges` 方法，而不是 `context.SaveChanges`。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

在測試專案中，開啟*MockSchoolRepository.cs* ，並將下列 `OfficeAssignment` 集合和 CRUD 方法加入其中。 （模擬存放庫必須執行存放庫介面，否則解決方案將不會編譯）。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>將 OfficeAssignment 方法新增至 BLL

在主要專案中，開啟*SchoolBL.cs* ，然後將 `OfficeAssignment` 實體集的下列 CRUD 方法加入其中：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>建立 OfficeAssignments 網頁

建立使用 [*網站*主要] 頁面的新網頁，並將其命名為*OfficeAssignments .aspx*。 將下列標記新增至名為 `Content2`的 `Content` 控制項：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

請注意，在 `DataKeyNames` 屬性中，標記會指定 `Timestamp` 屬性以及記錄索引鍵（`InstructorID`）。 在 `DataKeyNames` 屬性中指定屬性，會使控制項將其儲存在控制項狀態中（類似于檢視狀態），以便在回傳處理期間使用原始值。

如果您未儲存 `Timestamp` 值，則 Entity Framework 不會將它用於 SQL `Update` 命令的 `Where` 子句。 因此，將不會有任何更新。 因此，每次更新 `OfficeAssignment` 實體時，Entity Framework 都會擲回開放式平行存取例外狀況。

開啟*OfficeAssignments.aspx.cs* ，並為數據存取層新增下列 `using` 語句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

新增下列 `Page_Init` 方法，這會啟用動態資料功能。 此外，也請為 `ObjectDataSource` 控制項的 `Updated` 事件新增下列處理常式，以檢查並行錯誤：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>在 [OfficeAssignments] 頁面中測試開放式平行存取

執行 [ *OfficeAssignments* ] 頁面。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

按一下資料列中的 [**編輯**]，然後變更 [**位置**] 資料行中的值。

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

開啟新的瀏覽器視窗，然後再次執行頁面（將第一個瀏覽器視窗中的 URL 複製到第二個瀏覽器視窗）。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

在您稍早編輯的相同資料列中按一下 [**編輯**]，然後將 [**位置**] 值變更為不同的。

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

在第二個瀏覽器視窗中，按一下 [**更新**]。

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

切換至第一個瀏覽器視窗，然後按一下 [**更新**]。

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

您會看到一則錯誤訊息，且 [**位置**] 值已更新，以顯示您在第二個瀏覽器視窗中變更的值。

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>使用 EntityDataSource 控制項處理平行存取

`EntityDataSource` 控制項包含內建邏輯，可辨識資料模型中的並行設定，並據此處理更新和刪除作業。 不過，如同所有例外狀況，您必須自行處理 `OptimisticConcurrencyException` 例外狀況，才能提供容易使用的錯誤訊息。

接下來，您將設定 [*課程 .aspx* ] 頁面（使用 `EntityDataSource` 控制項）來允許更新和刪除作業，並在發生並行衝突時顯示錯誤訊息。 `Course` 實體沒有並行追蹤資料行，因此您將使用與 `Department` 實體相同的方法：追蹤所有非索引鍵屬性的值。

開啟*SchoolModel .edmx*檔案。 針對 `Course` 實體（`Title`、`Credits`和 `DepartmentID`）的非索引鍵屬性，請將**並行模式**屬性設定為 [`Fixed`]。 然後儲存並關閉資料模型。

開啟 [*課程 .aspx* ] 頁面，並進行下列變更：

- 在 `CoursesEntityDataSource` 控制項中，加入 `EnableUpdate="true"` 和 `EnableDelete="true"` 屬性。 該控制項的開頭標記現在與下列範例類似：

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- 在 `CoursesGridView` 控制項中，將 `DataKeyNames` 屬性值變更為 [`"CourseID,Title,Credits,DepartmentID"`]。 然後將 `CommandField` 專案新增至顯示 [**編輯**] 和 [**刪除**] 按鈕（`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`）的 `Columns` 元素。 `GridView` 控制項現在與下列範例類似：

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

執行頁面，並在 [部門] 頁面中建立衝突狀況。 在兩個瀏覽器視窗中執行頁面，在每個視窗的同一行中按一下 [**編輯**]，然後在每一個視窗中進行不同的變更。 按一下一個視窗中的 [**更新**]，然後按一下另一個視窗中的 [**更新**]。 當您第二次按下 [**更新**] 時，您會看到錯誤頁面，這是因為未處理的平行存取例外狀況所造成。

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

您處理這個錯誤的方式與處理 `ObjectDataSource` 控制項的方式非常類似。 開啟 [*課程 .aspx* ] 頁面，然後在 [`CoursesEntityDataSource`] 控制項中，指定 `Deleted` 和 `Updated` 事件的處理常式。 控制項的開頭標記現在與下列範例類似：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

在 `CoursesGridView` 控制項之前，新增下列 `ValidationSummary` 控制項：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

在*Courses.aspx.cs*中，加入 `System.Data` 命名空間的 `using` 語句、加入一個檢查並行例外狀況的方法，以及為 `EntityDataSource` 控制項的 `Updated` 和 `Deleted` 處理常式新增處理常式。 程式碼看起來會像下面這樣：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

這段程式碼與您在 `ObjectDataSource` 控制項中所做的唯一差異在於，在此情況下，並行例外狀況是在事件引數物件的 `Exception` 屬性中，而不是在該例外狀況的 `InnerException` 屬性中。

再次執行頁面，並再次建立並行衝突。 這次您會看到錯誤訊息：

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

如此即完成了處理並行衝突的簡介。 下一個教學課程將提供如何在使用 Entity Framework 的 web 應用程式中改善效能的指引。

> [!div class="step-by-step"]
> [上一頁](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [下一頁](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
