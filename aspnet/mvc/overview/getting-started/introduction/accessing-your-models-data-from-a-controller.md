---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 從控制器存取模型的資料 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: e01953dcfb2abf2db53a8aa869aa75b40485daca
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519085"
---
# <a name="accessing-your-models-data-from-a-controller"></a>從控制器存取模型資料

依[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](index.md)]

在本節中，您將建立新的 `MoviesController` 類別，並撰寫可抓取電影資料的程式碼，並使用 view 範本在瀏覽器中顯示它。

請先**建立應用程式**，再繼續進行下一個步驟。 如果您未建立應用程式，您將會在新增控制器時收到錯誤。

在方案總管中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後依序按一下 [**新增**]、[**控制器**]。

![](accessing-your-models-data-from-a-controller/_static/image1.png)

在 [**新增 Scaffold** ] 對話方塊中，按一下 [**具有視圖的 MVC 5 控制器，使用 Entity Framework**]，然後按一下 [**新增**]。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- 選取模型類別的 [**電影（MvcMovie）** ]。
- 選取資料內容類別的**MovieDBCoNtext （MvcMovie）** 。
- 在 [控制器名稱] 中輸入**moviescontroller.cs**。

  下圖顯示已完成的對話方塊。  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

按一下 [加入]。 （如果您收到錯誤，您可能未在開始新增控制器之前建立應用程式）。Visual Studio 會建立下列檔案和資料夾：

- [*控制器*] 資料夾中的*MoviesController.cs*檔案。
- *Views\Movies*資料夾。
- 在新的*Views\Movies*資料夾中，*建立. cshtml、Delete.* cshtml、Details、cshtml 和*Index.* cshtml。

Visual Studio 為您自動建立[crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) （建立、讀取、更新和刪除）動作方法和視圖（自動建立 crud 動作方法和視圖）稱為「樣板」（樣板））。 您現在有一個功能完整的 web 應用程式，可讓您建立、列出、編輯和刪除電影專案。

執行應用程式，並按一下 [ **MVC 電影**] 連結（或將 */Movies*附加至瀏覽器網址列中的 URL，以流覽至 `Movies` 控制器）。 因為應用程式會依賴預設路由（在應用程式中定義 *\_Start\RouteConfig.cs*檔），所以瀏覽器要求 `http://localhost:xxxxx/Movies` 會路由傳送至 `Movies` 控制器的預設 `Index` 動作方法。 換句話說，瀏覽器要求 `http://localhost:xxxxx/Movies` 與瀏覽器要求 `http://localhost:xxxxx/Movies/Index`有效。 結果是空的電影清單，因為您還沒有加入。

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>建立電影

選取 **Create New** 連結。 輸入電影的一些詳細資料，然後按一下 [**建立**] 按鈕。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> 您可能無法在 [價格] 欄位中輸入小數點或逗號。 若要支援對小數點使用逗號（&quot;、&quot;）之非英文地區設定的 jQuery 驗證，以及非英文日期格式，您必須包含*全球化 .js*和您的特定*文化特性/全球化。文化特性 .js*檔案（從[https://github.com/jquery/globalize](https://github.com/jquery/globalize) ）和 JavaScript，以使用 `Globalize.parseFloat` 。 在下一個教學課程中，我將示範如何執行這項操作。 現在，只要輸入如 10 之類的整數。

按一下 [**建立**] 按鈕會導致表單張貼至伺服器，其中電影資訊會儲存在資料庫中。 接著，您會被重新導向至 [ */Movies* URL]，您可以在清單中看到新建立的電影。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

建立幾個電影項目。 嘗試 **Edit**、**Details** 和 **Delete** 連結，這些連結都可以正常運作。

## <a name="examining-the-generated-code"></a>檢查產生的程式碼

開啟*Controllers\MoviesController.cs*檔案，並檢查產生的 `Index` 方法。 具有 `Index` 方法的電影控制器部分如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

`Movies` 控制器的要求會傳回 `Movies` 資料表中的所有專案，然後將結果傳遞至 `Index` view。 如先前所述，來自 `MoviesController` 類別的下一行會具現化電影資料庫內容。 您可以使用電影資料庫內容來查詢、編輯和刪除電影。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>強型別模型和 @model 關鍵字

稍早在本教學課程中，您已看到控制器如何使用 `ViewBag` 物件，將資料或物件傳遞至視圖範本。 `ViewBag` 是動態物件，可提供方便的晚期繫結方式，將資訊傳遞給視圖。

MVC 也提供將*強*型別物件傳遞至視圖範本的能力。 這個強型別方法可讓您在 Visual Studio 編輯器中，對程式碼和更豐富的[IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx)進行編譯階段檢查。 Visual Studio 中的「架構」機制會使用此方法（也就是，傳遞*強*型別模型）與 `MoviesController` 類別，並在建立方法和 views 時查看範本。

在*Controllers\MoviesController.cs*檔案中，檢查產生的 `Details` 方法。 `Details` 方法如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id` 參數通常會以路由資料的形式傳遞，例如 `http://localhost:1234/movies/details/1` 會將控制器設定為電影控制器、要 `details` 的動作，並將 `id` 設為1。 您也可以使用查詢字串傳入識別碼，如下所示：

`http://localhost:1234/movies/details?id=1`

如果找到 `Movie`，`Movie` 模型的實例會傳遞至 `Details` view：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

檢查*Views\Movies\Details.cshtml*檔案的內容：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

藉由在視圖範本檔案的頂端包含 `@model` 語句，您可以指定此視圖所預期的物件類型。 當您建立電影控制器時，Visual Studio 會在 *Details.cshtml* 檔案的最上方自動包含下列 `@model` 陳述式：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

這個 `@model` 指示詞可讓您使用強型別的 `Model` 物件，存取控制器傳遞至檢視的電影。 例如，在*詳細資料的 cshtml*範本中，程式碼會將每個電影欄位傳遞給 `DisplayNameFor`，並使用強型別 `Model` 物件[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 協助程式。 `Create` 和 `Edit` 方法和視圖範本也會傳遞電影模型物件。

檢查*MoviesController.cs*檔案中的 [ *Index. cshtml* ] （.）視圖範本和 `Index` 方法。 請注意，當程式碼在 `Index` 動作方法中呼叫 `View` helper 方法時，如何建立[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)物件。 然後，此程式碼會將此 `Movies` 清單從 `Index` 動作方法傳遞至視圖：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

當您建立電影控制器時，Visual Studio 會自動將下列 `@model` 語句包含在*索引 cshtml*檔案的頂端：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

此 `@model` 指示詞可讓您使用強型別的 `Model` 物件，來存取控制器傳遞至視圖的電影清單。 例如，在*Index. cshtml*範本中，程式碼會對強型別 `Model` 物件執行 `foreach` 語句，藉以迴圈執行電影：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

因為 `Model` 物件是強型別（做為 `IEnumerable<Movie>` 物件），所以迴圈中的每個 `item` 物件都會輸入為 `Movie`。 除了其他優點外，這也表示您可以在程式碼編輯器中，取得程式碼的編譯時期檢查和完整的 IntelliSense 支援：

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>使用 SQL Server LocalDB

Entity Framework Code First 偵測到所提供的資料庫連接字串指向尚未存在的 `Movies` 資料庫，因此 Code First 自動建立資料庫。 您可以藉由查看*應用程式\_Data*資料夾來確認它是否已建立。 如果您看不到 [*電影 .mdf* ] 檔案，請按一下 [**方案總管**] 工具列中的 [**顯示所有**檔案] 按鈕，按一下 [重新整理 **] 按鈕，** 然後展開*應用程式\_[Data* ] 資料夾。

![](accessing-your-models-data-from-a-controller/_static/image9.png)

按兩下 [ *.Mdf* ] 以開啟 [**伺服器瀏覽器**]，然後展開 [**資料表]** 資料夾，以查看電影資料表。 請注意 [ID] 旁的金鑰圖示。 根據預設，EF 會將名為 ID 的屬性設為主鍵。 如需 EF 和 MVC 的詳細資訊，請參閱 Tom 作者: dykstra 在[MVC 和 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)上的絕佳教學課程。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**顯示資料表資料**] 以查看您所建立的資料。

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**開啟資料表定義**]，查看 Entity Framework Code First 為您建立的資料表結構。

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

請注意 `Movies` 資料表的架構如何對應至您稍早建立的 `Movie` 類別。 Entity Framework Code First 會根據您的 `Movie` 類別，自動為您建立此架構。

當您完成時，請以滑鼠右鍵按一下 [ *MovieDBCoNtext* ]，然後選取 [**關閉連接**] 來關閉連線。 （如果您不關閉連線，下次執行專案時可能會出現錯誤）。

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

您現在擁有一個資料庫和多個頁面，可用來顯示、編輯、更新和刪除資料。 在下一個教學課程中，我們將檢查 scaffold 程式碼的其餘部分，並新增 `SearchIndex` 方法和 `SearchIndex` 視圖，讓您在此資料庫中搜尋電影。 如需搭配 MVC 使用 Entity Framework 的詳細資訊，請參閱[建立 ASP.NET MVC 應用程式的 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

> [!div class="step-by-step"]
> [上一頁](creating-a-connection-string.md)
> [下一頁](examining-the-edit-methods-and-edit-view.md)
