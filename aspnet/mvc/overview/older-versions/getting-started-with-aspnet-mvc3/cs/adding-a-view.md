---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 加入 View （C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: b4a1316feb8d9b7f3ef5ca4755bf1cc5b23e6ef9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615469"
---
# <a name="adding-a-view-c"></a>新增檢視 (C#)

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

在本節中，您將修改 `HelloWorldController` 類別，以使用視圖範本檔案，將產生 HTML 回應的程式完全封裝至用戶端。

您將使用 ASP.NET MVC 3 引進的新[Razor view 引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)來建立一個視圖範本檔案。 以 Razor 為基礎的視圖範本具有 *. cshtml*副檔名，並提供簡潔的方式來使用C#建立 HTML 輸出。 Razor 會將撰寫視圖範本時所需的字元和按鍵數目降至最低，並可提供快速、流暢的編碼工作流程。

首先，在 `HelloWorldController` 類別中使用具有 `Index` 方法的視圖範本。 目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。 變更 `Index` 方法，以傳回 `View` 物件，如下所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

這段程式碼會使用視圖範本來產生瀏覽器的 HTML 回應。 在專案中，加入您可以搭配 `Index` 方法使用的 [視圖] 範本。 若要這麼做，請以滑鼠右鍵按一下 `Index` 方法，然後按一下 [**加入視圖**]。

![](adding-a-view/_static/image1.png)

[**加入視圖**] 對話方塊隨即出現。 保留預設值，然後按一下 [**新增**] 按鈕：

![](adding-a-view/_static/image2.png)

系統會建立*MvcMovie\Views\HelloWorld*資料夾和*MvcMovie\Views\HelloWorld\Index.cshtml*檔案。 您可以在**方案總管**中看到這些專案：

![](adding-a-view/_static/image3.png)

以下顯示已建立的*Index. cshtml*檔案：

[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

在 `<h2>` 標記底下新增一些 HTML。 修改過的*MvcMovie\Views\HelloWorld\Index.cshtml*檔案如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

執行應用程式，並流覽至 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。 控制器中的 `Index` 方法不會執行太多工做;它只會執行語句 `return View()`，這會指定方法應該使用視圖範本檔案來呈現瀏覽器的回應。 由於您未明確指定所要使用之視圖範本檔案的名稱，因此 ASP.NET MVC 會預設為使用 *\Views\HelloWorld*資料夾中的*Index. cshtml* view file。 下圖顯示在此視圖中硬式編碼的字串。

![](adding-a-view/_static/image6.png)

看起來不錯。 不過，請注意，瀏覽器的標題列會顯示「索引」，而頁面上的大標題會顯示「我的 MVC 應用程式」。 讓我們變更這些。

## <a name="changing-views-and-layout-pages"></a>變更視圖和版面配置頁

首先，您要變更頁面頂端的「我的 MVC 應用程式」標題。 這是每一頁通用的文字。 它實際上只會在專案的一個位置中實作為，即使它出現在應用程式的每個頁面上也一樣。 移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 *\_版面配置. cshtml*檔案。 這個檔案稱為版面配置*頁*，它是所有其他頁面都使用的共用「shell」。

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

版面配置範本可讓您在一處指定網站的 HTML 容器版面配置，然後將它套用到您網站中的多個頁面。 請注意靠近檔案底部的 `@RenderBody()` 行。 `RenderBody` 是一種預留位置，其中您所建立的所有視圖特定頁面都會顯示在版面配置頁中「包裝」。 將版面配置範本中的標題標題從「我的 MVC 應用程式」變更為「MVC 電影應用程式」。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

執行應用程式，並注意它現在會顯示「MVC 電影應用程式」。 按一下 [**關於**] 連結，您也會看到該頁面如何顯示「MVC 電影應用程式」。 我們能夠在版面配置範本中進行變更一次，並讓網站上的所有頁面反映新的標題。

![](adding-a-view/_static/image9.png)

完整的 *\_配置 cshtml*檔案如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

現在，讓我們變更索引頁面的標題（view）。

開啟*MvcMovie\Views\HelloWorld\Index.cshtml*。 有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後是次要標頭（`<h2>` 元素）。 您會使這些變更略有不同，因此可看出哪一段程式碼變更了應用程式的哪個部分。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

若要指示要顯示的 HTML 標題，上述程式碼會設定 `ViewBag` 物件的 `Title` 屬性（位於*Index. cshtml* view template 中）。 如果您回顧版面配置範本的原始程式碼，您會注意到範本會在 `<title>` 元素中使用這個值，做為 HTML `<head>` 區段的一部分。 使用這種方法，您可以輕鬆地在您的視圖範本和配置檔案之間傳遞其他參數。

執行應用程式，並流覽至 `http://localhost:xx/HelloWorld`。 請注意，瀏覽器標題、主要標題和次要標題已變更 (如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。 請在瀏覽器中按 Ctrl + F5 以強制載入來自伺服器的回應)。

同時也請注意，已將 [*建立*] 視圖範本中的內容與 [\_配置] [ *cshtml* ] 視圖範本合併，並將單一 HTML 回應傳送至瀏覽器。 版面配置範本可讓您輕鬆進行會套用到應用程式之所有頁面的變更。

![](adding-a-view/_static/image10.png)

然而，我們的這一點點「資料」(在此案例中為 "Hello from our View Template!" 訊息) 是硬式編碼的資料。 MVC 應用程式具有 "V" (檢視)，並已取得 "C" (控制器)，但還沒有 "M" (模型)。 很快地，我們將逐步解說如何建立資料庫，並從中抓取模型資料。

## <a name="passing-data-from-the-controller-to-the-view"></a>將資料從控制器傳遞至檢視

不過，在我們進入資料庫並討論模型之前，讓我們先討論如何將控制器的資訊傳遞給視圖。 系統會叫用控制器類別，以回應傳入的 URL 要求。 控制器類別是您撰寫程式碼來處理傳入參數、從資料庫抓取資料，最後決定要傳回給瀏覽器的回應類型。 然後，您可以從控制器使用視圖範本來產生並格式化瀏覽器的 HTML 回應。

控制器會負責提供所需的任何資料或物件，以便讓視圖範本呈現對瀏覽器的回應。 「視圖」範本應該永遠不會執行商務邏輯，或直接與資料庫互動。 相反地，它應該只能與由控制器提供給它的資料搭配使用。 維護這項「關注點分離」有助於讓您的程式碼保持整潔且更容易維護。

目前，`HelloWorldController` 類別中的 `Welcome` 動作方法會接受 `name` 和 `numTimes` 參數，然後將這些值直接輸出到瀏覽器。 不是讓控制器將此回應轉譯為字串，讓我們將控制器變更為改用 view 範本。 檢視範本會產生動態回應，這表示您需要將適當數量的資料從控制器傳遞至檢視，以便產生回應。 若要這麼做，您可以讓控制器將 view template 所需的動態資料放在 view 範本可以存取的 `ViewBag` 物件中。

返回*HelloWorldController.cs*檔案並變更 `Welcome` 方法，將 `Message` 和 `NumTimes` 值新增至 `ViewBag` 物件。 `ViewBag` 是動態物件，這表示您可以將任何想要的內容放在其中：`ViewBag` 物件沒有定義的屬性，直到您將內容放在其中為止。 完整的 *HelloWorldController.cs* 檔案如下所示：

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

現在，`ViewBag` 物件包含將會自動傳遞至視圖的資料。

接下來，您需要一個歡迎視圖範本！ 在 [**調試**] 功能表中，選取 [**建立 MvcMovie** ] 以確定專案已編譯。

[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

然後以滑鼠右鍵按一下 `Welcome` 方法，然後按一下 [**加入視圖**]。 [**加入視圖**] 對話方塊如下所示：

![](adding-a-view/_static/image13.png)

按一下 **[新增]** ，然後在新的 [*歡迎使用] cshtml*檔案中的 `<h2>` 專案底下新增下列程式碼。 您將建立一個迴圈，顯示「Hello」，就像使用者所說的一樣多次。 完整的*歡迎使用 cshtml*檔案如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

執行應用程式，並流覽至下列 URL：

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

現在會從 URL 取得資料，並自動傳遞至控制器。 控制器會將資料封裝到 `ViewBag` 物件中，並將該物件傳遞至 view。 然後，此視圖會以 HTML 將資料顯示給使用者。

![](adding-a-view/_static/image14.png)

這是一種代表模型的 "M"，但不是資料庫類型。 讓我們運用所學的內容，建立電影的資料庫。

> [!div class="step-by-step"]
> [上一頁](adding-a-controller.md)
> [下一頁](adding-a-model.md)
