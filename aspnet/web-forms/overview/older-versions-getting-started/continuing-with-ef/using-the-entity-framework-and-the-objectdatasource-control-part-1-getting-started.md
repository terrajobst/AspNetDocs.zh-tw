---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第1部分：消費者入門 |Microsoft Docs
author: tdykstra
description: 本教學課程系列是以 Entity Framework 教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 如果 yo 。
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2f14707eb058d438495dd2bc4c17b976c471fc97
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547289"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第1部分：消費者入門

由[Tom 作者: dykstra](https://github.com/tdykstra)

> 本教學課程系列是[以 Entity Framework 4.0](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 如果您未完成先前的教學課程，做為本教學課程的起點，您可以下載您所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 您也可以下載完整的教學課程系列所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。
> 
> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 範例應用程式是虛構 Contoso 大學的網站。 其中包括的功能有學生入學許可、課程建立、教師指派。
> 
> 本教學課程會顯示C#中的範例。 [可下載的範例](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)包含C#和 Visual Basic 中的程式碼。
> 
> ## <a name="database-first"></a>Database First
> 
> 有三種方式可以使用 Entity Framework 中的資料： *Database First*、 *Model First*和*Code First*。 本教學課程適用于 Database First。 如需這些工作流程之間的差異，以及如何為您的案例選擇最適合的指引的詳細資訊，請參閱[Entity Framework 開發工作流程](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="web-forms"></a>Web Form
> 
> 就像消費者入門系列一樣，本教學課程系列會使用 ASP.NET Web form 模型，並假設您知道如何在 Visual Studio 中使用 ASP.NET Web Forms。 如果您沒有，請參閱[使用 ASP.NET 4.5 Web Forms 消費者入門](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 如果您想要使用 ASP.NET MVC 架構，請參閱[使用 ASP.NET MVC 的 Entity Framework 消費者入門](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> ## <a name="software-versions"></a>軟體版本
> 
> | **教學課程中所示** | **也適用于** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | 適用于 Web 的 Visual Studio 2010 Express。 本教學課程尚未使用較新版本的 Visual Studio 進行測試。 功能表選項、對話方塊和範本有許多差異。 |
> | .NET 4 | .NET 4.5 與 .NET 4 回溯相容，但本教學課程尚未使用 .NET 4.5 進行測試。 |
> | Entity Framework 4 | 本教學課程尚未使用較新版本的 Entity Framework 進行測試。 從 Entity Framework 5 開始，EF 預設會使用 EF 4.1 引進的 `DbContext API`。 EntityDataSource 控制項的設計目的是要使用 `ObjectContext` API。 如需如何搭配 `DbContext` API 使用 EntityDataSource 控制項的相關資訊，請參閱[這篇 blog 文章](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)。 |
> 
> ## <a name="questions"></a>問題
> 
> 如果您有與本教學課程不直接相關的問題，您可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)、 [Entity Framework 和 LINQ to Entities 論壇](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。

`EntityDataSource` 控制項可讓您快速建立應用程式，但通常會要求您在 *.aspx*頁面中保留大量的商務邏輯和資料存取邏輯。 如果您預期應用程式的複雜性日益增加，而且需要持續維護，您可以事先投入更多開發時間來建立多*層式*或*分層*的應用程式結構，以更容易維護。 若要執行此架構，您可以將展示層與商務邏輯層（BLL）和資料存取層（DAL）分開。 執行此結構的其中一種方式是使用 `ObjectDataSource` 控制項，而不是 `EntityDataSource` 控制項。 當您使用 `ObjectDataSource` 控制項時，您會執行自己的資料存取程式碼，然後在 *.aspx*頁面中使用與其他資料來源控制項有許多相同功能的控制項來叫用它。 這可讓您結合多層式方法的優點與使用 Web form 控制項進行資料存取的優點。

`ObjectDataSource` 控制項也能讓您以其他方式提供更大的彈性。 由於您會撰寫自己的資料存取程式碼，因此比起讀取、插入、更新或刪除特定實體類型更為容易，這就是 `EntityDataSource` 控制項設計來執行的工作。 例如，您可以在每次更新實體時執行記錄、在刪除實體時封存資料，或在插入具有外鍵值的資料列時，視需要自動檢查和更新相關的資料。

## <a name="business-logic-and-repository-classes"></a>商務邏輯和存放庫類別

`ObjectDataSource` 控制項的運作方式是叫用您所建立的類別。 類別包含可抓取和更新資料的方法，而且您可以將這些方法的名稱提供給標記中的 `ObjectDataSource` 控制項。 在呈現或回傳處理期間，`ObjectDataSource` 會呼叫您指定的方法。

除了基本 CRUD 作業以外，您建立來搭配 `ObjectDataSource` 控制項使用的類別，可能需要在 `ObjectDataSource` 讀取或更新資料時執行商務邏輯。 例如，當您更新部門時，您可能需要驗證沒有其他部門具有相同的系統管理員，因為一個人無法成為多個部門的系統管理員。

在某些 `ObjectDataSource` 檔（例如[ObjectDataSource 類別總覽](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx)）中，控制項會呼叫稱為*商務物件*的類別，其中包含商務邏輯和資料存取邏輯。 在本教學課程中，您將為商務邏輯和資料存取邏輯建立不同的類別。 封裝資料存取邏輯的類別稱為「*儲存*機制」。 商務邏輯類別同時包含商業邏輯方法和資料存取方法，但是資料存取方法會呼叫儲存機制來執行資料存取工作。

您也會在 BLL 和 DAL 之間建立抽象層，以促進 BLL 的自動化單元測試。 當您具現化商業邏輯類別中的存放庫時，會建立介面並使用介面來執行此抽象層。 如此一來，您就可以為商業邏輯類別提供任何可執行存放庫介面之物件的參考。 若是正常作業，您會提供可與 Entity Framework 搭配運作的存放庫物件。 若要進行測試，您可以提供一個儲存機制物件，以處理以輕鬆操作的方式儲存的資料，例如定義為集合的類別變數。

下圖顯示商業邏輯類別之間的差異，其中包括不含存放庫的資料存取邏輯，以及使用儲存機制的。

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

首先，您會建立網頁，其中 `ObjectDataSource` 控制項直接系結至存放庫，因為它只會執行基本的資料存取工作。 在下一個教學課程中，您將使用驗證邏輯建立商務邏輯類別，並將 `ObjectDataSource` 控制項系結至該類別，而不是將其系結至儲存機制類別。 您也會建立驗證邏輯的單元測試。 在此系列的第三個教學課程中，您將會在應用程式中加入排序和篩選功能。

您在本教學課程中建立的頁面會使用您在[消費者入門教學課程系列](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)中所建立之資料模型的 `Departments` 實體集。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>更新資料庫和資料模型

您將開始進行此教學課程，方法是對資料庫進行兩個變更，這兩者都需要對您在[消費者入門中使用 Entity Framework 和 Web](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) form 教學課程所建立的資料模型進行相對應的變更。 在其中一個教學課程中，您會以手動方式在設計工具中進行變更，以便在資料庫變更之後同步處理資料模型與資料庫。 在本教學課程中，您將使用來自資料庫工具的設計師**更新模型**，自動更新資料模型。

### <a name="adding-a-relationship-to-the-database"></a>將關聯性加入至資料庫

在 Visual Studio 中，開啟您在[使用 Entity Framework 和 Web Forms](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教學課程系列的消費者入門中建立的 Contoso 大學 web 應用程式，然後開啟 `SchoolDiagram` 資料庫關係圖。

如果您查看資料庫關係圖中的 [`Department`] 資料表，您會看到它有 [`Administrator`] 資料行。 此資料行是 `Person` 資料表的外鍵，但在資料庫中沒有定義任何外鍵關聯性。 您需要建立關聯性並更新資料模型，讓 Entity Framework 可以自動處理此關聯性。

在資料庫關係圖中，以滑鼠右鍵按一下 [`Department`] 資料表，然後選取 [**關聯**性]。

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

在 [**外鍵關聯**性] 方塊中，按一下 [**加入**]，然後按一下 [**資料表和資料行規格]** 的省略號。

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

在 [**資料表和資料行**] 對話方塊中，將主鍵資料表和欄位設定為 `Person` 並 `PersonID`，然後將外鍵資料表和欄位設定為 [`Department`] 和 [`Administrator`]。 （當您這麼做時，關聯性名稱會從 `FK_Department_Department` 變更為 `FK_Department_Person`）。

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

在 [**資料表和資料行**] 方塊中按一下 **[確定]** ，在 [**外鍵關聯**性] 方塊中按一下 [**關閉**]，然後儲存變更。 如果系統詢問您是否要儲存 `Person` 並 `Department` 資料表，請按一下 **[是]** 。

> [!NOTE]
> 如果您已刪除 `Person` 對應到已在 [`Administrator`] 資料行中之資料的資料列，您將無法儲存這項變更。 在這種情況下，請使用**伺服器總管**中的資料表編輯器，確保每個 `Department` 資料列中的 `Administrator` 值都包含實際存在於 `Person` 資料表中的記錄識別碼。
> 
> 儲存變更之後，如果該人員是部門系統管理員，就無法從 `Person` 資料表中刪除資料列。 在生產應用程式中，當資料庫條件約束防止刪除時，您會提供特定的錯誤訊息，或者您會指定串聯刪除。 如需如何指定串聯刪除的範例，請參閱[Entity Framework 和 ASP.NET –消費者入門第2部分](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)。

### <a name="adding-a-view-to-the-database"></a>將視圖加入至資料庫

在您要建立的新 [*部門 .aspx* ] 頁面中，您想要提供一個下拉式清單，其中的名稱為「最後，第一次」格式，讓使用者可以選取部門系統管理員。 為了讓它更容易執行，您會在資料庫中建立一個視圖。 此視圖只會包含下拉式清單所需的資料：完整名稱（格式正確）和記錄索引鍵。

在**伺服器總管**中，展開 [ *School*]，以滑鼠右鍵按一下 [ **Views** ] 資料夾，然後選取 [**加入新的視圖**]。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

出現 [**加入資料表**] 對話方塊時，按一下 [**關閉**]，並將下列 SQL 語句貼入 [sql] 窗格中：

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

將此視圖儲存為 `vInstructorName`。

### <a name="updating-the-data-model"></a>更新資料模型

在*DAL*資料夾中，開啟*SchoolModel*檔案，以滑鼠右鍵按一下設計介面，然後選取 [**從資料庫更新模型**]。

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

在 [**選擇您的資料庫物件**] 對話方塊中，選取 [**新增**] 索引標籤，然後選取您剛才建立的視圖。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

按一下 [完成] **Walkthrough: Calling Code in an VSTO Add-in from VBA**。

在設計工具中，您會看到工具已建立 `vInstructorName` 實體，以及 `Department` 和 `Person` 實體之間的新關聯。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> 在 [**輸出**] 和 [**錯誤清單**] 視窗中，您可能會看到一則警告訊息，通知您工具已自動建立新 `vInstructorName` 視圖的主要金鑰。 這是預期行為。

當您在程式碼中參考新的 `vInstructorName` 實體時，您不會想要在其前面加上小寫 "v" 的資料庫慣例。 因此，您將重新命名模型中的實體和實體集。

開啟 [**模型瀏覽器**]。 您會看到 `vInstructorName` 列為實體類型和一個視圖。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

在 [ **SchoolModel** （不是**SchoolModel**）] 底下，以滑鼠右鍵按一下**VInstructorName** ，然後選取 [**屬性**]。 在 [**屬性**] 視窗中，將 [**名稱**] 屬性變更為 "InstructorName"，並將 [**實體集名稱**] 屬性變更為 "InstructorNames"。

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

儲存並關閉資料模型，然後重建專案。

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>使用儲存機制類別和 ObjectDataSource 控制項

在*DAL*資料夾中建立新的類別檔案，將其命名為*SchoolRepository.cs*，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

這段程式碼會提供單一 `GetDepartments` 方法，以傳回 `Departments` 實體集中的所有實體。 因為您知道將會存取每個傳回之資料列的 `Person` 導覽屬性，所以您可以使用 `Include` 方法指定該屬性的積極式載入。 類別也會執行 `IDisposable` 介面，以確保在處置物件時釋放資料庫連接。

> [!NOTE]
> 常見的做法是為每個實體類型建立一個儲存機制類別。 在本教學課程中，會使用多個實體類型的一個儲存機制類別。 如需有關存放庫模式的詳細資訊，請參閱[Entity Framework 小組的 blog](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)和[Julie Lerman 的 blog](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)中的文章。

`GetDepartments` 方法會傳回 `IEnumerable` 物件，而不是 `IQueryable` 物件，以確保即使在處置存放庫物件本身之後，傳回的集合仍可供使用。 `IQueryable` 物件在存取時可能會導致資料庫存取，但是儲存機制物件可能會在資料系結控制項嘗試轉譯資料時處置。 您可以傳回另一個集合類型，例如 `IList` 物件，而不是 `IEnumerable` 物件。 不過，傳回 `IEnumerable` 物件可確保您可以執行一般唯讀清單處理工作，例如 `foreach` 迴圈和 LINQ 查詢，但是您無法加入或移除集合中的專案，這可能表示這類變更會保存到資料庫中。

建立使用*網站*master 頁面的*部門 .aspx*頁面，並在名為 `Content2`的 `Content` 控制項中新增下列標記：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

此標記會建立一個使用您剛才建立之儲存機制類別的 `ObjectDataSource` 控制項，以及一個 `GridView` 控制項來顯示資料。 `GridView` 控制項會指定**Edit**和**Delete**命令，但是您尚未加入程式碼來支援它們。

有數個數據行使用 `DynamicField` 控制項，讓您可以利用自動格式化和驗證功能。 若要讓這些專案正常執行，您必須在 `Page_Init` 事件處理常式中呼叫 `EnableDynamicData` 方法。 （`DynamicControl` 控制項不會在 [`Administrator`] 欄位中使用，因為它們不適用於導覽屬性）。

稍後當您將具有嵌套 `GridView` 控制項的資料行加入至方格時，`Vertical-Align="Top"` 屬性將會變得很重要。

開啟*Departments.aspx.cs*檔案，並新增下列 `using` 語句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

然後，為頁面的 `Init` 事件新增下列處理常式：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

在*DAL*資料夾中，建立名為*Department.cs*的新類別檔案，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

此程式碼會將中繼資料加入至資料模型。 它會指定 `Department` 實體的 `Budget` 屬性實際上代表貨幣，雖然它的資料類型是 `Decimal`的，而且它會指定此值必須介於0到 $1000000.00 之間。 它也會指定 `StartDate` 屬性應格式化為 mm/dd/yyyy 格式的日期。

執行 [*部門 .aspx* ] 頁面。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

請注意，雖然您並未在 [**預算**] 或 [**開始日期] 資料**行的 [ *.aspx* ] 頁面標記中指定格式字串，`DynamicField` 控制項也會使用您在*Department.cs*檔案中提供的中繼資料來套用預設貨幣和日期格式。

## <a name="adding-insert-and-delete-functionality"></a>新增插入和刪除功能

開啟*SchoolRepository.cs*，加入下列程式碼，以建立 `Insert` 方法和 `Delete` 方法。 程式碼也包含名為 `GenerateDepartmentID` 的方法，其會計算下一個可用的記錄索引鍵值，供 `Insert` 方法使用。 這是必要的，因為資料庫未設定為自動為 `Department` 資料表計算這種情況。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach 方法

`DeleteDepartment` 方法會呼叫 `Attach` 方法，以便重新建立在物件內容的物件狀態管理員中，于記憶體中的實體與它所代表的資料庫資料列之間維護的連結。 這必須在方法呼叫 `SaveChanges` 方法之前發生。

「*物件內容*」一詞指的是衍生自您用來存取實體集和實體之 `ObjectContext` 類別的 Entity Framework 類別。 在此專案的程式碼中，類別會命名為 `SchoolEntities`，而且其實例一律會命名為 `context`。 物件內容的*物件狀態管理員*是衍生自 `ObjectStateManager` 類別的類別。 物件連絡人會使用物件狀態管理員來儲存實體物件，並追蹤每一個物件是否與資料庫中對應的資料表資料列或資料列同步。

當您讀取實體時，物件內容會將它儲存在物件狀態管理員中，並追蹤物件的表示是否與資料庫同步。 例如，如果您變更屬性值，則會設定旗標，表示您所變更的屬性已不再與資料庫同步。 然後，當您呼叫 `SaveChanges` 方法時，物件內容會知道要在資料庫中執行的動作，因為物件狀態管理員知道實體的目前狀態與資料庫狀態之間的差異。

不過，這個進程通常無法在 web 應用程式中運作，因為在轉譯頁面之後，會處置讀取實體的物件內容實例，以及其物件狀態管理員中的所有專案。 必須套用變更的物件內容實例，是針對回傳處理而具現化的一個新的。 在 `DeleteDepartment` 方法的情況下，`ObjectDataSource` 控制項會從 view 狀態中的值重新建立實體的原始版本，但此重新建立的 `Department` 實體並不存在於物件狀態管理員中。 如果您在這個重新建立的實體上呼叫 `DeleteObject` 方法，呼叫將會失敗，因為物件內容並不知道實體是否與資料庫同步。 不過，呼叫 `Attach` 方法會在重新建立的實體與資料庫中的值之間重建相同的追蹤，該實體是在讀取先前的物件內容實例中時自動完成。

有時候，您不希望物件內容追蹤物件狀態管理員中的實體，而且您可以設定旗標來防止它這麼做。 本系列稍後的教學課程中會顯示這種情況的範例。

### <a name="the-savechanges-method"></a>SaveChanges 方法

這個簡單的存放庫類別說明如何執行 CRUD 作業的基本原則。 在此範例中，會在每次更新之後立即呼叫 `SaveChanges` 方法。 在生產應用程式中，您可能會想要從不同的方法呼叫 `SaveChanges` 方法，讓您更充分掌控資料庫的更新時間。 （在下一個教學課程結束時，您會看到一份白皮書的連結，其中討論工作單位模式，這是協調相關更新的一種方法）。另請注意，在此範例中，`DeleteDepartment` 方法不包含處理並行衝突的程式碼;將在本系列稍後的教學課程中新增程式碼來執行此動作。

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>在插入時，抓取要選取的講師名稱

建立新部門時，使用者必須能夠在下拉式清單中選取一份講師清單中的系統管理員。 因此，請將下列程式碼新增至*SchoolRepository.cs* ，以使用您稍早建立的視圖來建立方法來抓取講師清單：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>建立用於插入部門的頁面

建立*DepartmentsAdd* ，並使用 [*網站*] 頁面，並在名為 `Content2`的 `Content` 控制項中新增下列標記：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

此標記會建立兩個 `ObjectDataSource` 控制項，一個用於插入新的 `Department` 實體，另一個用於抓取用於選取部門系統管理員之 `DropDownList` 控制項的講師名稱。 標記會建立一個用於輸入新部門的 `DetailsView` 控制項，並為控制項的 `ItemInserting` 事件指定處理常式，讓您可以設定 `Administrator` 的外鍵值。 結尾是顯示錯誤訊息的 `ValidationSummary` 控制項。

開啟*DepartmentsAdd.aspx.cs* ，並新增下列 `using` 語句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

新增下列類別變數和方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init` 方法會啟用動態資料功能。 `DropDownList` 控制項的 `Init` 事件的處理常式會儲存控制項的參考，而 `DetailsView` 控制項的 `Inserting` 事件的處理常式會使用該參考來取得所選講師的 `PersonID` 值，並更新 `Administrator` 實體的 `Department` 外鍵屬性。

執行頁面，新增新部門的資訊，然後按一下 [**插入**] 連結。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

輸入另一個新部門的值。 在 [**預算**] 欄位中輸入大於1000000.00 的數位，並在下一個欄位上按 tab 鍵。 欄位中會出現一個星號，如果您將滑鼠指標停留在該欄位中，就會看到您在該欄位的中繼資料中輸入的錯誤訊息。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

按一下 [**插入**]，您會看到頁面底部的 [`ValidationSummary`] 控制項所顯示的錯誤訊息。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

接下來，關閉瀏覽器並開啟 [*部門 .aspx* ] 頁面。 藉由將 `DeleteMethod` 屬性加入至 [`ObjectDataSource`] 控制項，並將 `DataKeyNames` 屬性加入至 `GridView` 控制項，將刪除功能新增至 [node.js *] 頁面。* 這些控制項的開頭標記現在會如下列範例所示：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

執行頁面。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

刪除您在執行*DepartmentsAdd*時所新增的部門。

## <a name="adding-update-functionality"></a>新增更新功能

開啟*SchoolRepository.cs* ，並新增下列 `Update` 方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

當您按一下 [*部門 .aspx* ] 頁面中的 [**更新**] 時，`ObjectDataSource` 控制項會建立兩個 `Department` 的實體，以傳遞至 `UpdateDepartment` 方法。 其中一個包含已儲存在 view 狀態中的原始值，另一個則包含在 `GridView` 控制項中輸入的新值。 `UpdateDepartment` 方法中的程式碼會將具有原始值的 `Department` 實體傳遞至 `Attach` 方法，以便在實體和資料庫中的專案之間建立追蹤。 然後，程式碼會將具有新值的 `Department` 實體傳遞至 `ApplyCurrentValues` 方法。 物件內容會比較新舊值。 如果新的值與舊的值不同，則物件內容會變更屬性值。 然後，`SaveChanges` 方法只會更新資料庫中已變更的資料行。 （不過，如果這個實體的 update 函式已對應至預存程式，則不論變更的資料行為何，都會更新整個資料列）。

開啟 [*部門 .aspx*檔案]，並將下列屬性新增至 `DepartmentsObjectDataSource` 控制項：

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 這會導致舊值儲存在 view 狀態中，以便與 `Update` 方法中的新值進行比較。
- `OldValuesParameterFormatString="orig{0}"`   
 這會通知控制項，原始值參數的名稱為 `origDepartment`。

`ObjectDataSource` 控制項之開頭標記的標記現在與下列範例類似：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

將 `OnRowUpdating="DepartmentsGridView_RowUpdating"` 屬性加入至 [`GridView`] 控制項。 您將使用這個值，根據使用者在下拉式清單中選取的資料列，來設定 `Administrator` 屬性值。 `GridView` 開頭標記現在與下列範例類似：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

將 [`Administrator`] 資料行的 `EditItemTemplate` 控制項加入至 [`GridView`] 控制項，緊接在該資料行的 `ItemTemplate` 控制項之後：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

這個 `EditItemTemplate` 控制項類似于*DepartmentsAdd .aspx*頁面中的 `InsertItemTemplate` 控制項。 其差異在於，控制項的初始值是使用 `SelectedValue` 屬性來設定。

在 `GridView` 控制項之前，加入 `ValidationSummary` 控制項，如同您在*DepartmentsAdd .aspx*頁面中所做的一樣。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

開啟*Departments.aspx.cs* ，並緊接在部分類別宣告之後，加入下列程式碼來建立私用欄位來參考 `DropDownList` 控制項：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

然後，為 `DropDownList` 控制項的 `Init` 事件和 `GridView` 控制項的 `RowUpdating` 事件新增處理常式：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

`Init` 事件的處理常式會在 [類別] 欄位中儲存 `DropDownList` 控制項的參考。 `RowUpdating` 事件的處理常式會使用參考來取得使用者輸入的值，並將它套用至 `Department` 實體的 `Administrator` 屬性。

使用 [ *DepartmentsAdd* ] 頁面來新增部門，然後執行 [*部門 .aspx* ] 頁面，然後在您新增的資料列上按一下 [**編輯**]。

> [!NOTE]
> 因為資料庫中的資料無效，所以您將無法編輯未加入的資料列（也就是已經在資料庫中）。使用資料庫所建立之資料列的系統管理員是學生。 如果您嘗試編輯其中一個，您會收到報告錯誤的錯誤頁面，例如 `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`

[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

如果您輸入不正確**預算**金額，然後按一下 [**更新**]，您會看到與您在 [*部門 .aspx* ] 頁面中看到的相同星號和錯誤訊息。

變更域值或選取不同的系統管理員，然後按一下 [**更新**]。 隨即顯示變更。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

這會完成使用 Entity Framework 的基本 CRUD （建立、讀取、更新、刪除）作業的 `ObjectDataSource` 控制項簡介。 您已建立簡單的多層式應用程式，但商業邏輯層仍與資料存取層緊密結合，這會使自動化單元測試變得複雜。 在下列教學課程中，您將瞭解如何執行存放庫模式來加速單元測試。

> [!div class="step-by-step"]
> [下一個](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
