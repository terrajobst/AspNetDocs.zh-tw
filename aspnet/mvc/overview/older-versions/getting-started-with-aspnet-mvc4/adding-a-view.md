---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: 加入視圖 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599747"
---
# <a name="adding-a-view"></a>新增檢視

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。

在本節中，您將修改 `HelloWorldController` 類別，以使用視圖範本檔案，將產生 HTML 回應的程式完全封裝至用戶端。

您將使用 ASP.NET MVC 3 引進的[Razor view 引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)來建立一個視圖範本檔案。 以 Razor 為基礎的視圖範本具有 *. cshtml*副檔名，並提供簡潔的方式來使用C#建立 HTML 輸出。 Razor 會將撰寫視圖範本時所需的字元和按鍵數目降至最低，並可提供快速、流暢的編碼工作流程。

目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。 變更 `Index` 方法以傳回 `View` 物件，如下列程式碼所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

上述 `Index` 方法會使用視圖範本來產生瀏覽器的 HTML 回應。 控制器方法（也稱為[動作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)）（例如上述的 `Index` 方法）通常會傳回[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) （或衍生自[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)的類別），而不是像字串這樣的基本類型。

在專案中，加入您可以搭配 `Index` 方法使用的 [視圖] 範本。 若要這麼做，請以滑鼠右鍵按一下 `Index` 方法，然後按一下 [**加入視圖**]。

![](adding-a-view/_static/image1.png)

[**加入視圖**] 對話方塊隨即出現。 保留預設值，然後按一下 [**新增**] 按鈕：

![](adding-a-view/_static/image2.png)

系統會建立*MvcMovie\Views\HelloWorld*資料夾和*MvcMovie\Views\HelloWorld\Index.cshtml*檔案。 您可以在**方案總管**中看到這些專案：

![](adding-a-view/_static/image3.png)

以下顯示已建立的*Index. cshtml*檔案：

![HelloWorldIndex](adding-a-view/_static/image4.png)

在 `<h2>` 標記底下新增下列 HTML。

[!code-html[Main](adding-a-view/samples/sample2.html)]

完整的*MvcMovie\Views\HelloWorld\Index.cshtml*檔案如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

如果您使用 Visual Studio 2012，請在 [方案管理器] 中，以滑鼠右鍵按一下 [ *Index. cshtml* ] 檔案，然後選取 [ **Page Inspector 中的 View**]。

![PI](adding-a-view/_static/image5.png)

[Page Inspector 教學](../../views/using-page-inspector-in-aspnet-mvc.md)課程包含此新工具的詳細資訊。

或者，執行應用程式並流覽至 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。 控制器中的 `Index` 方法不會執行太多工做;它只會執行語句 `return View()`，這會指定方法應該使用視圖範本檔案來呈現瀏覽器的回應。 由於您未明確指定所要使用之視圖範本檔案的名稱，因此 ASP.NET MVC 會預設為使用 *\Views\HelloWorld*資料夾中的*Index. cshtml* view file。 下圖顯示我們的 View 範本中的字串 &quot;Hello！&quot; 在視圖中硬式編碼。

![](adding-a-view/_static/image6.png)

看起來不錯。 不過，請注意，瀏覽器的標題列會顯示 &quot;Index My ASP.NET A&quot;，而頁面頂端的大連結則顯示在這裡 &quot;您的標誌。&quot; 在此處 &quot;您的標誌。&quot; 連結是註冊和登入連結，下方連結至 Home、About 和 Contact 頁面。 讓我們變更其中一些部分。

## <a name="changing-views-and-layout-pages"></a>變更視圖和版面配置頁

首先，您想要在這裡變更您的標誌 &quot;。在頁面頂端&quot; [標題]。 這是每一頁通用的文字。 它實際上只會在專案的一個位置中實作為，即使它出現在應用程式的每個頁面上也一樣。 移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 *\_版面配置. cshtml*檔案。 這個檔案稱為版面配置*頁*，它是所有其他頁面都使用的共用 &quot;shell&quot;。

![_LayoutCshtml](adding-a-view/_static/image7.png)

版面配置範本可讓您在一處指定網站的 HTML 容器版面配置，然後將它套用到您網站中的多個頁面。 找到 `@RenderBody()` 這行。 `RenderBody` 是顯示您建立之所有檢視特定頁面的預留位置，「包裝」&quot;&quot;在版面配置頁中。 例如，如果您選取 [關於] 連結，則會在 `RenderBody` 方法中轉譯*Views\Home\About.cshtml*視圖。

變更版面配置範本中的網站標題標題，從此處 &quot;您的標誌&quot; 至 &quot;MVC 電影&quot;。

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

將 title 元素的內容取代為下列標記：

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

執行應用程式，並注意它現在會顯示 &quot;MVC Movie &quot;。 按一下 [**關於**] 連結，您會看到該頁面也會顯示 &quot;MVC 電影&quot;的方式。 我們能夠在版面配置範本中進行變更一次，並讓網站上的所有頁面反映新的標題。

![](adding-a-view/_static/image8.png)

現在，讓我們來變更索引視圖的標題。

開啟*MvcMovie\Views\HelloWorld\Index.cshtml*。 有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後是次要標頭（`<h2>` 元素）。 您會使這些變更略有不同，因此可看出哪一段程式碼變更了應用程式的哪個部分。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

若要指示要顯示的 HTML 標題，上述程式碼會設定 `ViewBag` 物件的 `Title` 屬性（位於*Index. cshtml* view template 中）。 如果您回頭看一下版面配置範本的原始程式碼，就會發現範本會在 `<title>` 元素中使用這個值，做為我們先前修改之 HTML 的 `<head>` 區段的一部分。 使用這種 `ViewBag` 方法，您可以輕鬆地在您的視圖範本和配置檔案之間傳遞其他參數。

執行應用程式，並流覽至 `http://localhost:xx/HelloWorld`。 請注意，瀏覽器標題、主要標題和次要標題已變更 (如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。 在瀏覽器中按 Ctrl + F5，以強制載入伺服器的回應。）瀏覽器標題會使用*我們在 [&quot;] 視圖範本*中設定的 `ViewBag.Title` 來建立，並在配置檔案中新增額外的 Movie 應用程式&quot;。

同時也請注意，已將 [*建立*] 視圖範本中的內容與 [\_配置] [ *cshtml* ] 視圖範本合併，並將單一 HTML 回應傳送至瀏覽器。 版面配置範本可讓您輕鬆進行會套用到應用程式之所有頁面的變更。

![](adding-a-view/_static/image9.png)

不過，我們有點 &quot;的資料&quot; （在此情況下，我們的 View Template 中的 &quot;Hello！&quot; message）是硬式編碼的。 MVC 應用程式具有 &quot;V&quot; （view），而且您有 &quot;的 C&quot; （控制器），但尚未 &quot;M&quot; （model）。 很快地，我們將逐步解說如何建立資料庫，並從中抓取模型資料。

## <a name="passing-data-from-the-controller-to-the-view"></a>將資料從控制器傳遞至檢視

不過，在我們進入資料庫並討論模型之前，讓我們先討論如何將控制器的資訊傳遞給視圖。 系統會叫用控制器類別，以回應傳入的 URL 要求。 控制器類別是您撰寫程式碼來處理傳入瀏覽器要求、從資料庫抓取資料，最後決定要傳回給瀏覽器的回應類型。 然後，您可以從控制器使用視圖範本來產生並格式化瀏覽器的 HTML 回應。

控制器會負責提供所需的任何資料或物件，以便讓視圖範本呈現對瀏覽器的回應。 最佳做法：**視圖範本絕對不應執行商務邏輯，或直接與資料庫互動**。 相反地，「視圖」範本只能與由控制器提供給它的資料搭配使用。 維護這項 &quot;的顧慮&quot; 有助於讓程式碼保持整潔、可測試且更容易維護。

目前，`HelloWorldController` 類別中的 `Welcome` 動作方法會接受 `name` 和 `numTimes` 參數，然後將這些值直接輸出到瀏覽器。 不是讓控制器將此回應轉譯為字串，讓我們將控制器變更為改用 view 範本。 檢視範本會產生動態回應，這表示您需要將適當數量的資料從控制器傳遞至檢視，以便產生回應。 若要這麼做，您可以讓控制器將視圖範本所需的動態資料（參數）放置在 view 範本可以存取的 `ViewBag` 物件中。

返回*HelloWorldController.cs*檔案並變更 `Welcome` 方法，將 `Message` 和 `NumTimes` 值新增至 `ViewBag` 物件。 `ViewBag` 是動態物件，這表示您可以將任何想要的內容放在其中：`ViewBag` 物件沒有定義的屬性，直到您將內容放在其中為止。 [ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將指定的參數（`name` 和 `numTimes`）從網址列中的查詢字串對應至方法中的參數。 完整的 *HelloWorldController.cs* 檔案如下所示：

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

現在，`ViewBag` 物件包含將會自動傳遞至視圖的資料。

接下來，您需要一個歡迎視圖範本！ 在 [**建立**] 功能表中，選取 [**建立 MvcMovie** ] 以確定專案已編譯。

然後以滑鼠右鍵按一下 `Welcome` 方法，然後按一下 [**加入視圖**]。

![](adding-a-view/_static/image10.png)

[**加入視圖**] 對話方塊如下所示：

![](adding-a-view/_static/image11.png)

按一下 **[新增]** ，然後在新的 [*歡迎使用] cshtml*檔案中的 `<h2>` 專案底下新增下列程式碼。 您將建立一個迴圈，指出 &quot;Hello&quot; 的次數與使用者所說的數目一樣多。 完整的*歡迎使用 cshtml*檔案如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

執行應用程式，並流覽至下列 URL：

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

現在會從 URL 取得資料，並使用[模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結器傳遞至控制器。 控制器會將資料封裝到 `ViewBag` 物件中，並將該物件傳遞至 view。 然後，此視圖會以 HTML 將資料顯示給使用者。

![](adding-a-view/_static/image12.png)

在上述範例中，我們使用了 `ViewBag` 物件，將資料從控制器傳遞至 view。 在本教學課程中，我們將使用 view 模型，將資料從控制器傳遞至 view。 傳遞資料的「視圖模型」方法通常是透過「視圖包」方法來處理的最佳作法。 如需詳細資訊，請參閱 blog 專案[Dynamic V 強](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)型別視圖。

這是一種適用于模型的 &quot;M&quot;，但不是資料庫種類。 讓我們運用所學的內容，建立電影的資料庫。

> [!div class="step-by-step"]
> [上一頁](adding-a-controller.md)
> [下一頁](adding-a-model.md)
