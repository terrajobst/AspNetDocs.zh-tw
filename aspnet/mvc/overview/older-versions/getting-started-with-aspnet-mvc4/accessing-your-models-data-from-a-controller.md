---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 從控制器存取模型的資料 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456162"
---
# <a name="accessing-your-models-data-from-a-controller"></a>從控制器存取模型資料

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。

在本節中，您將建立新的 `MoviesController` 類別，並撰寫可抓取電影資料的程式碼，並使用 view 範本在瀏覽器中顯示它。

請先**建立應用程式**，再繼續進行下一個步驟。

以滑鼠右鍵按一下 [*控制器*] 資料夾，然後建立新的 `MoviesController` 控制器。 在您建立應用程式之前，將不會顯示下列選項。 選取下列選項：

- 控制器名稱： **moviescontroller.cs**。 （這是預設值。 )
- 範本：**具有讀取/寫入動作和視圖的 MVC 控制器，使用 Entity Framework**。
- 模型類別： **Movie （MvcMovie）** 。
- 資料內容類別： **MovieDBCoNtext （MvcMovie）** 。
- Views： **Razor （CSHTML）** 。 （預設值）。

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

按一下 [新增]。 Visual Studio Express 會建立下列檔案和資料夾：

- 專案的 [*控制器*] 資料夾中的*MoviesController.cs*檔案。
- 專案 [ *Views* ] 資料夾中的 [*電影*] 資料夾。
- 在新的*Views\Movies*資料夾中，*建立. cshtml、Delete.* cshtml、Details、cshtml 和*Index.* cshtml。

ASP.NET MVC 4 會為您自動建立 CRUD （建立、讀取、更新和刪除）動作方法和視圖（自動建立 CRUD 動作方法和 views）稱為「樣板」（樣板））。 您現在有一個功能完整的 web 應用程式，可讓您建立、列出、編輯和刪除電影專案。

執行應用程式，並藉由將 */Movies*附加至瀏覽器網址列中的 URL，流覽至 `Movies` 控制器。 因為應用程式會依賴預設路由（定義于*global.asax*檔案中），所以瀏覽器要求 `http://localhost:xxxxx/Movies` 會路由傳送至 `Movies` 控制器的預設 `Index` 動作方法。 換句話說，瀏覽器要求 `http://localhost:xxxxx/Movies` 與瀏覽器要求 `http://localhost:xxxxx/Movies/Index`有效。 結果是空的電影清單，因為您還沒有加入。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>建立電影

選取 **Create New** 連結。 輸入電影的一些詳細資料，然後按一下 [**建立**] 按鈕。

![](accessing-your-models-data-from-a-controller/_static/image3.png)

按一下 [**建立**] 按鈕會導致表單張貼至伺服器，其中電影資訊會儲存在資料庫中。 接著，您會被重新導向至 [ */Movies* URL]，您可以在清單中看到新建立的電影。

![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")

建立幾個電影項目。 嘗試 **Edit**、**Details** 和 **Delete** 連結，這些連結都可以正常運作。

## <a name="examining-the-generated-code"></a>檢查產生的程式碼

開啟*Controllers\MoviesController.cs*檔案，並檢查產生的 `Index` 方法。 具有 `Index` 方法的電影控制器部分如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

如先前所述，來自 `MoviesController` 類別的下一行會具現化電影資料庫內容。 您可以使用電影資料庫內容來查詢、編輯和刪除電影。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

`Movies` 控制器的要求會傳回 movie 資料庫之 `Movies` 資料表中的所有專案，然後將結果傳遞至 `Index` view。

## <a name="strongly-typed-models-and-the-model-keyword"></a>強型別模型和 @model 關鍵字

稍早在本教學課程中，您已看到控制器如何使用 `ViewBag` 物件，將資料或物件傳遞至視圖範本。 `ViewBag` 是動態物件，可提供方便的晚期繫結方式，將資訊傳遞給視圖。

ASP.NET MVC 也提供將強型別資料或物件傳遞至視圖範本的能力。 這個強型別方法可讓您在 Visual Studio 編輯器中，對程式碼和更豐富的 IntelliSense 進行編譯階段檢查。 Visual Studio 中的「架構」機制在建立方法和 views 時，會使用此方法搭配 `MoviesController` 類別和「視圖」範本。

在*Controllers\MoviesController.cs*檔案中，檢查產生的 `Details` 方法。 具有 `Details` 方法的電影控制器部分如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

如果找到 `Movie`，就會將 `Movie` 模型的實例傳遞至詳細資料檢視。 檢查*Views\Movies\Details.cshtml*檔案的內容。

藉由在視圖範本檔案的頂端包含 `@model` 語句，您可以指定此視圖所預期的物件類型。 當您建立電影控制器時，Visual Studio 會在 `@model`Details.cshtml*檔案的最上方自動包含下列* 陳述式：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

這個 `@model` 指示詞可讓您使用強型別的 `Model` 物件，存取控制器傳遞至檢視的電影。 例如，在*詳細資料的 cshtml*範本中，程式碼會將每個電影欄位傳遞給 `DisplayNameFor`，並使用強型別 `Model` 物件[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 協助程式。 建立和編輯方法和視圖範本也會通過電影模型物件。

檢查*MoviesController.cs*檔案中的 [ *Index. cshtml* ] （.）視圖範本和 `Index` 方法。 請注意，當程式碼在 `Index` 動作方法中呼叫 `View` helper 方法時，如何建立[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)物件。 然後，此程式碼會將此 `Movies` 清單從控制器傳遞至視圖：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

當您建立電影控制器時，Visual Studio Express 會自動將下列 `@model` 語句包含在*索引 cshtml*檔案的頂端：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

此 `@model` 指示詞可讓您使用強型別的 `Model` 物件，來存取控制器傳遞至視圖的電影清單。 例如，在*Index. cshtml*範本中，程式碼會對強型別 `Model` 物件執行 `foreach` 語句，藉以迴圈執行電影：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

因為 `Model` 物件是強型別（做為 `IEnumerable<Movie>` 物件），所以迴圈中的每個 `item` 物件都會輸入為 `Movie`。 除了其他優點外，這也表示您可以在程式碼編輯器中，取得程式碼的編譯時期檢查和完整的 IntelliSense 支援：

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>使用 SQL Server LocalDB

Entity Framework Code First 偵測到所提供的資料庫連接字串指向尚未存在的 `Movies` 資料庫，因此 Code First 自動建立資料庫。 您可以藉由查看*應用程式\_Data*資料夾來確認它是否已建立。 如果您看不到 [*電影 .mdf* ] 檔案，請按一下 [**方案總管**] 工具列中的 [**顯示所有**檔案] 按鈕，按一下 [重新整理 **] 按鈕，** 然後展開*應用程式\_[Data* ] 資料夾。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

按兩下 [ *.Mdf* ] 以開啟 [**資料庫瀏覽器**]，然後展開 [**資料表]** 資料夾，以查看電影資料表。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> 如果未出現 [資料庫 explorer]，請從 [**工具**] 功能表中選取 **[連接到資料庫]** ，然後取消 [**選擇資料來源**] 對話方塊。 這會強制開啟 [資料庫 explorer]。

> [!NOTE]
> 如果您使用 VWD 或 Visual Studio 2010，並取得類似下列任一項的錯誤：
> 
> - 資料庫 ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES。無法開啟 .MDF '，因為它是706版。 此伺服器支援655版和更早版本。 不支援降級路徑。
> - &quot;的 InvalidOperation 例外狀況已由使用者程式碼處理，&quot; 提供的 SqlConnection 未指定初始目錄。
> 
> 您必須安裝[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)和[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)。 請確認前一頁指定的 `MovieDBContext` 連接字串。

以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**顯示資料表資料**] 以查看您所建立的資料。

![](accessing-your-models-data-from-a-controller/_static/image8.png)

以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**開啟資料表定義**]，查看 Entity Framework Code First 為您建立的資料表結構。

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

請注意 `Movies` 資料表的架構如何對應至您稍早建立的 `Movie` 類別。 Entity Framework Code First 會根據您的 `Movie` 類別，自動為您建立此架構。

當您完成時，請以滑鼠右鍵按一下 [ *MovieDBCoNtext* ]，然後選取 [**關閉連接**] 來關閉連線。 （如果您不關閉連線，下次執行專案時可能會出現錯誤）。

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

您現在已擁有資料庫和簡單的清單頁面，可顯示其內容。 在下一個教學課程中，我們將檢查 scaffold 程式碼的其餘部分，並新增 `SearchIndex` 方法和 `SearchIndex` 視圖，讓您在此資料庫中搜尋電影。

> [!div class="step-by-step"]
> [上一頁](adding-a-model.md)
> [下一頁](examining-the-edit-methods-and-edit-view.md)
