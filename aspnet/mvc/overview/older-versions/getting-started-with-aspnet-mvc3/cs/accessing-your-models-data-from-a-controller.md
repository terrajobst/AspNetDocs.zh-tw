---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
title: 從控制器存取模型的資料（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 002ada5c-f114-47ab-a441-57dbdb728ea0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e9c7f24d426635760b613f570b85455ce71b3dc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623862"
---
# <a name="accessing-your-models-data-from-a-controller-c"></a>從控制器存取模型資料 (C#)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。
> 
> 
> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有C#原始程式碼的 Visual Web Developer 專案。 [下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。

在本節中，您將建立新的 `MoviesController` 類別，並撰寫可抓取電影資料的程式碼，並使用 view 範本在瀏覽器中顯示它。 請務必先建立您的應用程式，再繼續進行。

以滑鼠右鍵按一下 [*控制器*] 資料夾，然後建立新的 `MoviesController` 控制器。 選取下列選項：

- 控制器名稱： **moviescontroller.cs**。 （這是預設值。 )
- 範本：**具有讀取/寫入動作和視圖的控制器，使用 Entity Framework**。
- 模型類別： **Movie （MvcMovie）** 。
- 資料內容類別： **MovieDBCoNtext （MvcMovie）** 。
- Views： **Razor （CSHTML）** 。 （預設值）。

[![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image2.png "AddScaffoldedMovieController")](accessing-your-models-data-from-a-controller/_static/image1.png)

按一下 [新增]。 Visual Web Developer 會建立下列檔案和資料夾：

- 專案的 [*控制器*] 資料夾中的*MoviesController.cs*檔案。
- 專案 [ *Views* ] 資料夾中的 [*電影*] 資料夾。
- 在新的*Views\Movies*資料夾中，*建立. cshtml、Delete.* cshtml、Details、cshtml 和*Index.* cshtml。

[![NewMovieControllerScreenShot](accessing-your-models-data-from-a-controller/_static/image4.png "NewMovieControllerScreenShot")](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 架構機制會自動為您建立 CRUD （建立、讀取、更新和刪除）動作方法和視圖。 您現在有一個功能完整的 web 應用程式，可讓您建立、列出、編輯和刪除電影專案。

執行應用程式，並藉由將 */Movies*附加至瀏覽器網址列中的 URL，流覽至 `Movies` 控制器。 因為應用程式會依賴預設路由（定義于*global.asax*檔案中），所以瀏覽器要求 `http://localhost:xxxxx/Movies` 會路由傳送至 `Movies` 控制器的預設 `Index` 動作方法。 換句話說，瀏覽器要求 `http://localhost:xxxxx/Movies` 與瀏覽器要求 `http://localhost:xxxxx/Movies/Index`有效。 結果是空的電影清單，因為您還沒有加入。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

### <a name="creating-a-movie"></a>建立電影

選取 **Create New** 連結。 輸入電影的一些詳細資料，然後按一下 [**建立**] 按鈕。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

按一下 [**建立**] 按鈕會導致表單張貼至伺服器，其中電影資訊會儲存在資料庫中。 接著，您會被重新導向至 [ */Movies* URL]，您可以在清單中看到新建立的電影。

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png "IndexWhenHarryMet")](accessing-your-models-data-from-a-controller/_static/image7.png)

建立幾個電影項目。 嘗試 **Edit**、**Details** 和 **Delete** 連結，這些連結都可以正常運作。

## <a name="examining-the-generated-code"></a>檢查產生的程式碼

開啟*Controllers\MoviesController.cs*檔案，並檢查產生的 `Index` 方法。 具有 `Index` 方法的電影控制器部分如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

如先前所述，來自 `MoviesController` 類別的下一行會具現化電影資料庫內容。 您可以使用電影資料庫內容來查詢、編輯和刪除電影。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

`Movies` 控制器的要求會傳回 movie 資料庫之 `Movies` 資料表中的所有專案，然後將結果傳遞至 `Index` view。

## <a name="strongly-typed-models-and-the-model-keyword"></a>強型別模型和 @model 關鍵字

稍早在本教學課程中，您已看到控制器如何使用 `ViewBag` 物件，將資料或物件傳遞至視圖範本。 `ViewBag` 是動態物件，可提供方便的晚期繫結方式，將資訊傳遞給視圖。

ASP.NET MVC 也提供將強型別資料或物件傳遞至視圖範本的能力。 這個強型別方法可讓您更妥善地編譯器代碼，以及在 Visual Web Developer editor 中更豐富的 IntelliSense。 我們使用這種方法搭配 `MoviesController` 類別和*索引. cshtml*視圖範本。

請注意，當程式碼在 `Index` 動作方法中呼叫 `View` helper 方法時，如何建立[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)物件。 然後，此程式碼會將此 `Movies` 清單從控制器傳遞至視圖：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

藉由在視圖範本檔案的頂端包含 `@model` 語句，您可以指定此視圖所預期的物件類型。 當您建立電影控制器時，Visual Web Developer 會自動將下列 `@model` 語句包含在*Index. cshtml*檔案的頂端：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

此 `@model` 指示詞可讓您使用強型別的 `Model` 物件，來存取控制器傳遞至視圖的電影清單。 例如，在*Index. cshtml*範本中，程式碼會對強型別 `Model` 物件執行 `foreach` 語句，藉以迴圈執行電影：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml)]

因為 `Model` 物件是強型別（做為 `IEnumerable<Movie>` 物件），所以迴圈中的每個 `item` 物件都會輸入為 `Movie`。 除了其他優點外，這也表示您可以在程式碼編輯器中，取得程式碼的編譯時期檢查和完整的 IntelliSense 支援：

[![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image10.png "ModelIntelliSense")](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>使用 SQL Server Compact

Entity Framework Code First 偵測到所提供的資料庫連接字串指向尚未存在的 `Movies` 資料庫，因此 Code First 自動建立資料庫。 您可以藉由查看*應用程式\_Data*資料夾來確認它是否已建立。 如果您看不到 [*電影 .sdf* ] 檔案，請按一下 [**方案總管**] 工具列中的 [**顯示所有**檔案] 按鈕，按一下 [重新整理 **] 按鈕，** 然後展開 [*應用程式\_* 資料夾]。

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)

按兩下 [ *.sdf* ] 以開啟**伺服器總管**。 然後展開 [**資料表]** 資料夾，以查看已在資料庫中建立的資料表。

> [!NOTE]
> 如果您按兩下 [ *.sdf*] 時出現錯誤，請確定您已安裝[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）。 （如需軟體的連結，請參閱本教學課程系列的第1部分中的必要條件清單）。如果您現在安裝發行，就必須關閉並重新開啟 Visual Web Developer。

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)

有兩個數據表，一個用於 `Movie` 實體集，然後是 `EdmMetadata` 資料表。 Entity Framework 會使用 `EdmMetadata` 資料表來判斷模型和資料庫何時未同步。

以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**顯示資料表資料**] 以查看您所建立的資料。

[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png "MoviesTable")](accessing-your-models-data-from-a-controller/_static/image15.png)

以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**編輯資料表架構**]。

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png "EditTableSchema")](accessing-your-models-data-from-a-controller/_static/image17.png)

[![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image20.png "TableSchemaSM")](accessing-your-models-data-from-a-controller/_static/image19.png)

請注意 `Movies` 資料表的架構如何對應至您稍早建立的 `Movie` 類別。 Entity Framework Code First 會根據您的 `Movie` 類別，自動為您建立此架構。

當您完成時，請關閉連線。 （如果您不關閉連線，下次執行專案時可能會出現錯誤）。

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image22.png "CloseConnection")](accessing-your-models-data-from-a-controller/_static/image21.png)

您現在已擁有資料庫和簡單的清單頁面，可顯示其內容。 在下一個教學課程中，我們將檢查 scaffold 程式碼的其餘部分，並新增 `SearchIndex` 方法和 `SearchIndex` 視圖，讓您在此資料庫中搜尋電影。

> [!div class="step-by-step"]
> [上一頁](adding-a-model.md)
> [下一頁](examining-the-edit-methods-and-edit-view.md)
