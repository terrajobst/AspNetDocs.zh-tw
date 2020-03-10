---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: 在 ASP.NET 4 Web 應用程式中使用 Entity Framework 4.0 將效能最大化 |Microsoft Docs
author: tdykstra
description: 本教學課程系列是以 Entity Framework 4.0 教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 5630200a1ad1d30f6d89b38e15179f15b699fa9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545959"
---
# <a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>在 ASP.NET 4 Web 應用程式中使用 Entity Framework 4.0 將效能最大化

由[Tom 作者: dykstra](https://github.com/tdykstra)

> 本教學課程系列是[以 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 如果您未完成先前的教學課程，做為本教學課程的起點，您可以下載您所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 您也可以下載完整的教學課程系列所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果您有關于教學課程的問題，可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)。

在上一個教學課程中，您已瞭解如何處理並行衝突。 本教學課程會示範用來改善使用 Entity Framework 之 ASP.NET web 應用程式效能的選項。 您將瞭解幾種可將效能最大化的方法，或是用來診斷效能問題的方法。

下列各節所提供的資訊，可能會在各種不同的案例中很有用：

- 有效率地載入相關資料。
- 管理檢視狀態。

如果您有顯示效能問題的個別查詢，下列各節所提供的資訊可能會很有用：

- 使用 [`NoTracking` 合併] 選項。
- 預先編譯 LINQ 查詢。
- 檢查傳送至資料庫的查詢命令。

在下一節中提供的資訊，對於具有極大資料模型的應用程式可能很有用：

- 預先產生的視圖。

> [!NOTE]
> Web 應用程式效能會受到許多因素的影響，包括要求和回應資料的大小、資料庫查詢的速度、伺服器可以佇列的要求數，以及服務的效能，甚至是任何專案的效率。您可能使用的用戶端腳本程式庫。 如果您的應用程式中的效能非常重要，或測試或經驗顯示應用程式效能並不令人滿意，您應該遵循正常的通訊協定來進行效能調整。 測量以判斷效能瓶頸發生的位置，然後解決將對整體應用程式效能造成最大影響的區域。
> 
> 本主題主要著重于您可以在 ASP.NET 中特別改善 Entity Framework 效能的方式。 如果您判斷資料存取是應用程式中的其中一個效能瓶頸，這裡的建議很有用。 除非特別說明，否則此處所述的方法不應視為 &quot;最佳作法&quot;，其中有許多僅適用于例外狀況，或因應特定類型的效能瓶頸。

若要開始本教學課程，請啟動 Visual Studio，並開啟您在上一個教學課程中使用的 Contoso 大學 web 應用程式。

## <a name="efficiently-loading-related-data"></a>有效率地載入相關資料

Entity Framework 可以透過數種方式將相關資料載入至實體的導覽屬性：

- *消極式載入*。 第一次讀取實體時，不會擷取相關資料。 不過，第一次嘗試存取導覽屬性時，將會自動擷取該導覽屬性所需的資料。 這會導致多個查詢傳送至資料庫，一個用於實體本身，而每次必須取得實體的相關資料。 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*積極式載入*。 讀取實體時，將會同時擷取其相關資料。 這通常會導致單一聯結查詢，其可擷取所有需要的資料。 您可以使用 `Include` 方法來指定積極式載入，如同您已在這些教學課程中所見。

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *明確式載入*。 這類似于消極式載入，不同之處在于您在程式碼中明確地取得相關資料。當您存取導覽屬性時，不會自動進行此動作。 您可以使用集合之導覽屬性的 `Load` 方法手動載入相關資料，或使用參考屬性的 `Load` 方法來保存單一物件的屬性。 （例如，您可以呼叫 `PersonReference.Load` 方法，載入 `Department` 實體的 `Person` 導覽屬性）。

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

因為它們不會立即取得屬性值，所以消極式載入和明確載入也稱為*延後載入*。

消極式載入是設計工具所產生之物件內容的預設行為。 如果您開啟定義物件內容類別的*SchoolModel.Designer.cs*檔案，您會發現三個方法，其中每一個都包含下列語句：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

一般來說，如果您知道每個抓取的實體都需要相關資料，積極式載入會提供最佳效能，因為傳送至資料庫的單一查詢通常比每個所抓取之實體的個別查詢更有效率。 另一方面，如果您只需要針對一小部分實體存取實體的導覽屬性，則消極式載入或明確載入可能會更有效率，因為積極式載入會抓取比您所需更多的資料。

在 web 應用程式中，消極式載入的值仍然可能相對較小，因為影響相關資料需求的使用者動作會在瀏覽器中進行，而這與轉譯頁面的物件內容沒有任何連接。 相反地，當您將控制項進行資料繫結時，通常會知道您需要什麼資料，因此通常最好是根據每個案例的適當程度來選擇積極式載入或延後載入。

此外，在處置物件內容之後，資料系結控制項可能會使用實體物件。 在這種情況下，嘗試延遲載入導覽屬性會失敗。 您收到的錯誤訊息很明確： &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

`EntityDataSource` 控制項預設會停用延遲載入。 針對目前教學課程所使用的 `ObjectDataSource` 控制項（或者，如果您從頁面程式碼存取物件內容），有幾種方式可以讓延遲載入預設為停用。 當您具現化物件內容時，可以將它停用。 例如，您可以將下列程式程式碼新增至 `SchoolRepository` 類別的「函式」方法：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

針對 Contoso 大學應用程式，您會讓物件內容自動停用消極式載入，如此一來，每當內容具現化時，就不需要設定此屬性。

開啟 [ *SchoolModel* ] 資料模型，按一下設計介面，然後在 [屬性] 窗格中，將 [**已啟用的延遲載入**] 屬性設定為 [`False`]。 儲存並關閉資料模型。

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>管理檢視狀態

為了提供更新功能，ASP.NET 網頁必須在呈現頁面時儲存實體的原始屬性值。 在回傳處理期間，控制項可以重新建立實體的原始狀態，並在套用變更並呼叫 `SaveChanges` 方法之前，先呼叫實體的 `Attach` 方法。 根據預設，ASP.NET Web Forms 資料控制項會使用 view 狀態來儲存原始值。 不過，檢視狀態會影響效能，因為它會儲存在隱藏欄位中，大幅增加與瀏覽器之間傳送的頁面大小。

管理檢視狀態的技術，或會話狀態之類的替代方法，對 Entity Framework 而言並不獨特，因此本教學課程不會詳細說明此主題。 如需詳細資訊，請參閱本教學課程結尾處的連結。

不過，ASP.NET 的第4版提供了一種新的方式來使用 view 狀態，Web Forms 應用程式的每個 ASP.NET 開發人員都應該知道： `ViewStateMode` 屬性。 這個新屬性可以在頁面或控制項層級設定，而且它可以讓您停用頁面的預設檢視狀態，並僅針對需要它的控制項加以啟用。

對於效能非常重要的應用程式，最好一律停用頁面層級的 view state，並只針對需要它的控制項加以啟用。 這種方法不會大幅減少 Contoso 大學頁面中的檢視狀態大小，但若要查看其運作方式，請在 [ *default.aspx* ] 頁面上執行此動作。 該頁面包含許多控制項，包括已停用檢視狀態的 `Label` 控制項。 此頁面上的控制項都不需要啟用檢視狀態。 （`GridView` 控制項的 `DataKeyNames` 屬性會指定必須在回傳之間維護的狀態，但這些值會保留在控制項狀態中，而不會受到 `ViewStateMode` 屬性的影響）。

`Page` 指示詞和 `Label` 控制項標記目前與下列範例類似：

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

進行下列變更：

- 將 `ViewStateMode="Disabled"` 新增至 `Page` 指示詞。
- 從 `Label` 控制項移除 `ViewStateMode="Disabled"`。

標記現在與下列範例類似：

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

所有控制項的檢視狀態現在已停用。 如果您稍後新增的控制項需要使用檢視狀態，您只需要包含該控制項的 `ViewStateMode="Enabled"` 屬性。

## <a name="using-the-notracking-merge-option"></a>使用 NoTracking 合併選項

當物件內容抓取資料庫資料列並建立代表它們的實體物件時，預設也會使用物件狀態管理員來追蹤這些實體物件。 此追蹤資料會作為快取，並在您更新實體時使用。 由於 web 應用程式通常會有存留期較短的物件內容實例，因此查詢通常會傳回不需要追蹤的資料，因為讀取它們的物件內容將會在其讀取的任何實體再次使用或更新之前進行處置。

在 Entity Framework 中，您可以藉由設定*合併選項*來指定物件內容是否追蹤實體物件。 您可以設定個別查詢或實體集的合併選項。 如果您針對實體集設定它，這表示您正在針對針對該實體集所建立的所有查詢設定預設的合併選項。

針對 Contoso 大學應用程式，您從儲存機制存取的任何實體集都不需要追蹤，因此您可以在將存放庫類別中的物件內容具現化時，將合併選項設定為針對這些實體集 `NoTracking`。 （請注意，在本教學課程中，設定 [合併] 選項不會對應用程式的效能造成顯著的影響。 `NoTracking` 選項在某些高資料量的情況下，可能只會使效能改進。）

在 DAL 資料夾中，開啟*SchoolRepository.cs*檔案，並新增可為存放庫所存取之實體集設定合併選項的函式方法：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>預先編譯 LINQ 查詢

第一次 Entity Framework 在給定 `ObjectContext` 實例的生命週期內執行 Entity SQL 查詢時，需要一些時間來編譯查詢。 系統會快取編譯的結果，這表示後續執行查詢的速度會更快。 LINQ 查詢會遵循類似的模式，但編譯查詢所需的部分工作會在每次執行查詢時完成。 換句話說，針對 LINQ 查詢，預設不會快取編譯的所有結果。

如果您有預期會在物件內容的生命週期中重複執行的 LINQ 查詢，您可以撰寫程式碼，在第一次執行 LINQ 查詢時，快取所有編譯結果。

如圖所示，您會在 `SchoolRepository` 類別中的兩個 `Get` 方法中執行此動作，其中一個不接受任何參數（`GetInstructorNames` 方法），而另一個則需要參數（`GetDepartmentsByAdministrator` 方法）。 這些方法現在實際上不需要編譯，因為它們不是 LINQ 查詢：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

不過，您可以試用已編譯的查詢，如同這些查詢已撰寫為下列 LINQ 查詢一樣繼續進行：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

您可以將這些方法中的程式碼變更為上面顯示的內容，並執行應用程式以確認它可正常運作，然後再繼續進行。 但下列指示直接帶您建立預先編譯的版本。

在*DAL*資料夾中建立類別檔案，將其命名為*SchoolEntities.cs*，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

此程式碼會建立部分類別，以擴充自動產生的物件內容類別。 部分類別包含兩個使用 `CompiledQuery` 類別的 `Compile` 方法編譯的 LINQ 查詢。 它也會建立可供您用來呼叫查詢的方法。 儲存並關閉此檔案。

接下來，在*SchoolRepository.cs*中，變更存放庫類別中現有的 `GetInstructorNames` 和 `GetDepartmentsByAdministrator` 方法，使其呼叫已編譯的查詢：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

執行 [*部門 .aspx* ] 頁面，確認它的運作方式與之前相同。 呼叫 `GetInstructorNames` 方法以填入 [系統管理員] 下拉式清單，並在您按一下 [**更新**] 時呼叫 `GetDepartmentsByAdministrator` 方法，以確認講師不是一個以上部門的系統管理員。

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

您已在 Contoso 大學應用程式中預先編譯查詢，只是為了瞭解如何執行，而不是因為它會顯著提升改善效能。 預先編譯 LINQ 查詢會在您的程式碼中增加複雜度層級，因此請確定您只針對實際代表應用程式效能瓶頸的查詢執行此動作。

## <a name="examining-queries-sent-to-the-database"></a>檢查傳送至資料庫的查詢

當您調查效能問題時，有時候知道 Entity Framework 傳送至資料庫的確切 SQL 命令會很有説明。 如果您要使用 `IQueryable` 物件，其中一種方法是使用 `ToTraceString` 方法。

在*SchoolRepository.cs*中，變更 `GetDepartmentsByName` 方法中的程式碼，以符合下列範例：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

`departments` 變數必須轉換成 `ObjectQuery` 型別，因為上一行結尾的 `Where` 方法會建立 `IQueryable` 物件;如果沒有 `Where` 方法，就不需要轉換。

在 `return` 行上設定中斷點，然後在偵錯工具中執行 [*部門 .aspx* ] 頁面。 當您點擊中斷點時，請檢查 [**區域變數**] 視窗中的 `commandText` 變數，並使用文字視覺化效果（[**值**] 資料行中的放大鏡），在 [**文字視覺化檢視**] 視窗中顯示其值。 您可以看到此程式碼所產生的整個 SQL 命令：

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

或者，Visual Studio Ultimate 中的 IntelliTrace 功能提供一種方式來查看 Entity Framework 所產生的 SQL 命令，而不需要變更您的程式碼，甚至是設定中斷點。

> [!NOTE]
> 只有在您有 Visual Studio Ultimate 時，才可以執行下列程式。

還原 `GetDepartmentsByName` 方法中的原始程式碼，然後在偵錯工具中執行 [*部門 .aspx* ] 頁面。

在 Visual Studio 中，依序選取 [**調試**] 功能表、[ **intellitrace**] 和 [ **intellitrace 事件**]。

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

在 [ **IntelliTrace** ] 視窗中，按一下 [**全部中斷**]。

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

[ **IntelliTrace** ] 視窗會顯示最近的事件清單：

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

按一下 [ **ADO.NET** ] 行。 它會展開以顯示命令文字：

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

您可以從 [**區域變數**] 視窗，將整個命令文字字串複製到剪貼簿。

假設您使用的資料庫具有比簡單 `School` 資料庫更多的資料表、關聯性和資料行。 您可能會發現，在包含多個 `Join` 子句的單一 `Select` 語句中收集您所需之所有資訊的查詢，會變得太複雜而無法有效率地運作。 在此情況下，您可以從積極式載入切換到明確的載入，以簡化查詢。

例如，請嘗試在*SchoolRepository.cs*中變更 `GetDepartmentsByName` 方法中的程式碼。 目前在該方法中，您有一個物件查詢，其中具有 `Person` 和 `Courses` 導覽屬性的 `Include` 方法。 以執行明確載入的程式碼取代 `return` 語句，如下列範例所示：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

執行偵錯工具中的 [*部門 .aspx* ] 頁面，然後再次檢查 [ **IntelliTrace** ] 視窗，如同之前一樣。 現在，在之前有單一查詢，您會看到一長串的順序。

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

按一下第一個**ADO.NET**行，以查看您稍早查看的複雜查詢發生了什麼狀況。

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

來自部門的查詢已變成簡單的 `Select` 查詢，沒有 `Join` 子句，但後面接著的個別查詢，會針對原始查詢所傳回的每個部門，使用一組兩個查詢來抓取相關課程和系統管理員。

> [!NOTE]
> 如果您讓消極式載入啟用，則在這裡看到的模式重複多次，可能是因為消極式載入所導致。 您通常會想要避免的模式，是主資料表中每個資料列的延遲載入相關資料。 除非您已確認單一聯結查詢太複雜而無法有效率，否則在這種情況下，您通常可以藉由變更主要查詢來使用積極式載入，來改善效能。

## <a name="pre-generating-views"></a>預先產生的視圖

第一次在新的應用程式域中建立 `ObjectContext` 物件時，Entity Framework 會產生一組用來存取資料庫的類別。 這些類別稱為*views*，如果您有非常大的資料模型，則產生這些視圖可能會在新的應用程式域初始化之後，延遲網站對第一個要求的回應。 您可以在編譯時期（而不是在執行時間）建立視圖，藉此減少第一個要求延遲。

> [!NOTE]
> 如果您的應用程式沒有非常大型的資料模型，或如果它有大型資料模型，但您不在意只有在回收 IIS 後才會影響到第一頁要求的效能問題，您可以略過本節。 當您具現化 `ObjectContext` 物件時，不會發生視圖建立，因為這些視圖會在應用程式域中快取。 因此，除非您經常在 IIS 中回收應用程式，否則只有預先產生的視圖可以受益于極少的頁面要求。

您可以使用*edmgen.exe*命令列工具，或使用「*文字模板轉換*工具組」（T4）範本來預先產生視圖。 在本教學課程中，您將使用 T4 範本。

在*DAL*資料夾中，使用**文字模板**範本來新增檔案（它位於 [**已安裝的範本**] 清單中的 [**一般**] 節點底下），並將它命名為*SchoolModel.Views.tt*。 將檔案中的現有程式碼取代為下列程式碼：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

此程式碼會產生 *.edmx*檔案的視圖，此檔案位於與範本相同的資料夾中，而且名稱與範本檔案相同。 例如，如果您的範本檔案命名為*SchoolModel.Views.tt*，它會尋找名為*SchoolModel*的資料模型檔案。

儲存檔案，然後以滑鼠右鍵按一下**方案總管**中的檔案，然後選取 [**執行自訂工具**]。

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio 會產生程式碼檔案，該檔案會根據範本建立名為*SchoolModel.Views.cs*的視圖。 （您可能已注意到，即使在您選取 [**執行自訂工具**] 之後，您也會在儲存範本檔案之後，才會產生程式碼檔案）。

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

您現在可以執行應用程式，並確認它的運作方式與之前相同。

如需預先產生之視圖的詳細資訊，請參閱下列資源：

- 如何：在 MSDN 網站上[預先產生視圖以改善查詢效能](https://msdn.microsoft.com/library/bb896240.aspx)。 說明如何使用 `EdmGen.exe` 命令列工具來預先產生 views。
- 在 Windows Server AppFabric 客戶諮詢小組的 blog 中，以[Entity Framework 4 的先行編譯/預先產生的觀點來隔離效能](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx)。

這會完成介紹，以在使用 Entity Framework 的 ASP.NET web 應用程式中改善效能。 如需詳細資訊，請參閱下列資源：

- MSDN 網站上的[效能考慮（Entity Framework）](https://msdn.microsoft.com/library/cc853327.aspx) 。
- [Entity Framework 小組 blog 上的效能相關文章](https://blogs.msdn.com/b/adonet/archive/tags/performance/)。
- [EF Merge 選項和已編譯的查詢](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx)。 說明已編譯查詢和合併選項（如 `NoTracking`）之非預期行為的 Blog 文章。 如果您打算在應用程式中使用已編譯的查詢或操作合併選項設定，請先閱讀這項功能。
- [資料和模型化客戶諮詢小組 blog 中的 Entity Framework 相關文章](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/)。 包含已編譯查詢的貼文，並使用 Visual Studio 2010 Profiler 探索效能問題。
- [Entity Framework 論壇往來文章，並提供改善高度複雜查詢效能的建議](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6)。
- [ASP.NET 狀態管理建議](https://msdn.microsoft.com/library/z1hkazw7.aspx)。
- [使用 Entity Framework 和 ObjectDataSource：自訂分頁](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx)。 以在這些教學課程中建立的 ContosoUniversity 應用程式為基礎的 Blog 文章，說明如何在 *[node.js* ] 頁面中執行分頁。

下一個教學課程會針對第4版中的新 Entity Framework，回顧一些重要的增強功能。

> [!div class="step-by-step"]
> [上一頁](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [下一頁](what-s-new-in-the-entity-framework-4.md)
