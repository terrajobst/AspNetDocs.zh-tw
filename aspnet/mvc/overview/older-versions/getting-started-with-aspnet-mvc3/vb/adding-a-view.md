---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 加入視圖（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457301"
---
# <a name="adding-a-view-vb"></a>新增檢視 (VB)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。 [下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/adding-a-view.md)。

在本節中，我們將修改 `HelloWorldController` 類別，以使用視圖範本檔案，將產生 HTML 回應的程式完全封裝至用戶端。

讓我們從在 `HelloWorldController` 類別中使用具有 `Index` 方法的視圖範本開始著手。 目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。 變更 `Index` 方法，以傳回 `View` 物件，如下所示：

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

現在讓我們將一個 view 範本加入至我們可以使用 `Index` 方法叫用的專案。 若要這麼做，請以滑鼠右鍵按一下 `Index` 方法，然後按一下 [**加入視圖**]。

[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)

[**加入視圖**] 對話方塊隨即出現。 保留預設專案，然後按一下 [**新增**] 按鈕。

[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)

系統會建立*MvcMovie\Views\HelloWorld*資料夾和*MvcMovie\Views\HelloWorld\Index.vbhtml*檔案。 您可以在**方案總管**中看到這些專案：

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

在 `<h2>` 標記底下新增一些 HTML。 修改過的*MvcMovie\Views\HelloWorld\Index.vbhtml*檔案如下所示。

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

執行應用程式，並流覽至 &quot;hello world&quot; 控制器（`http://localhost:xxxx/HelloWorld`）。 控制器中的 `Index` 方法不會執行太多工做;它只會執行 `return View()`語句，這表示我們想要使用視圖範本檔案來呈現對用戶端的回應。 因為我們並未明確指定要使用的視圖範本檔案的名稱，所以 ASP.NET MVC 會預設為使用 *\Views\HelloWorld*資料夾中的*vbhtml*視圖檔案。 下圖顯示在此視圖中硬式編碼的字串。

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

看起來不錯。 不過，請注意，瀏覽器的標題列會顯示 &quot;索引&quot; 而頁面上的大標題會顯示為 [&quot;我的 MVC 應用程式]。&quot; 讓我們變更這些。

## <a name="changing-views-and-layout-pages"></a>變更檢視和版面配置頁

首先，讓我們變更 MVC 應用程式 &quot;的文字。&quot; 該文字會共用並顯示在每個頁面上。 它實際上只會出現在專案中的一個位置，即使它是在應用程式的每個頁面上也一樣。 移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 *\_配置 vbhtml*檔案。 這個檔案稱為版面配置頁，它是所有其他頁面都使用的共用 &quot;shell&quot;。

請注意靠近檔案底部的 `@RenderBody()` 行程式碼。 `RenderBody` 是一種預留位置，其中會顯示您建立的所有頁面，&quot;包裝在版面配置頁中的&quot;。 將 [`<h1>`] 標題從 [ **&quot;** 我的 MVC 應用&quot; 程式] 變更為 [&quot;Mvc 電影應用程式&quot;]。

[!code-html[Main](adding-a-view/samples/sample3.html)]

執行應用程式，並注意它現在會顯示 &quot;MVC 電影應用程式&quot;。 按一下 [**關於**] 連結，該頁面也會顯示 &quot;MVC 電影應用程式&quot;。

完整的 *\_配置的 vbhtml*檔案如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

現在，讓我們變更索引頁面的標題（view）。

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

開啟*MvcMovie\Views\HelloWorld\Index.vbhtml*。 有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後是次要標頭（`<h2>` 元素）。 我們會讓它們略有不同，讓您可以看到哪一段程式碼變更了哪個部分的應用程式。

執行應用程式，並流覽至`http://localhost:xx/HelloWorld`。 請注意，瀏覽器標題、主要標題和次要標題已變更 您可以輕鬆地在應用程式中進行大幅變更，而對視圖進行小幅變更。 (如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。 請在瀏覽器中按 Ctrl + F5 以強制載入來自伺服器的回應)。

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

不過，我們有點 &quot;的資料&quot; （在此案例中，&quot;Hello World！&quot; 訊息）是硬式編碼。 我們的 MVC 應用程式有 V （views），而我們已經有 C （控制器），但沒有 M （模型）。 很快地，我們將逐步解說如何建立資料庫，並從中抓取模型資料。

## <a name="passing-data-from-the-controller-to-the-view"></a>將資料從控制器傳遞至檢視

不過，在我們進入資料庫並討論模型之前，讓我們先討論如何將控制器的資訊傳遞給視圖。 我們想要傳遞「視圖」範本所需的內容，以便向用戶端轉譯 HTML 回應。 這些物件通常是由控制器類別所建立並傳遞給視圖範本，而且它們應該只包含此視圖範本所需的資料，而且不再需要。

先前使用 `HelloWorldController` 類別，`Welcome` 動作方法會採用 `name` 和 `numTimes` 參數，然後將參數值輸出至瀏覽器。 而不是讓控制器直接轉譯此回應，讓我們改為將該資料放在此視圖的包中。 控制器和 Views 可以使用 `ViewBag` 物件來保存該資料。 這會自動傳遞至視圖範本，並用來呈現 HTML 回應，使用包的內容做為資料。 如此一來，控制器就會關心一件事，並使用另一個視圖範本，讓我們能夠在應用程式中維護 &quot;的顧慮分離&quot;。

或者，我們可以定義自訂類別，然後自行建立該物件的實例，並在其中填入資料並將其傳遞給視圖。 這通常稱為 ViewModel，因為它是 View 的自訂模型。 不過，對於少量的資料，ViewBag 的效果很好。

返回*HelloWorldController* ，將控制器內的 `Welcome` 方法變更為將訊息和 numtimes is 放入 ViewBag 中。 ViewBag 是動態物件。 這表示您可以將任何想要的內容放在其中。 ViewBag 沒有已定義的屬性，除非您在其中放置內容。

在相同檔案中，具有新類別的完整 `HelloWorldController.vb`。

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

現在，我們的 ViewBag 包含將會自動傳遞到 View 的資料。 同樣地，如果我們喜歡，也可以傳入我們自己的物件，如下所示：

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

現在我們需要一個 `WelcomeView` 範本！ 執行應用程式，以編譯新的程式碼。 關閉瀏覽器，在 `Welcome` 方法內按一下滑鼠右鍵，然後按一下 [**加入視圖**]。

[**加入視圖**] 對話方塊的外觀如下所示。

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

將下列程式碼加入至新的歡迎畫面中的 `<h2>` 元素底下<em>。</em>vbhtml 檔案。 我們會建立迴圈，並說 &quot;Hello&quot; 的次數，如同使用者所說的一樣！

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

執行應用程式，並流覽至 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

現在會從 URL 取得資料，並自動傳遞至控制器。 控制器會將資料封裝成 `Model` 物件，並將該物件傳遞至 view。 視圖會將資料以 HTML 形式顯示給使用者。

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

這是一種適用于模型的 &quot;M&quot;，但不是資料庫種類。 讓我們運用所學的內容，建立電影的資料庫。

> [!div class="step-by-step"]
> [上一頁](adding-a-controller.md)
> [下一頁](adding-a-model.md)
