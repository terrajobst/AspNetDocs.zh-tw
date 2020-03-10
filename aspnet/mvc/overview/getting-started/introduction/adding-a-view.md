---
title: 將視圖加入至 MVC 應用程式
author: Rick-Anderson
description: 將視圖加入至 MVC 應用程式
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: 0bc6ac06d12aaee4b2a11c1bf246f9f20f0be017
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582716"
---
# <a name="adding-a-view"></a>新增檢視

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

在本節中，您將修改 `HelloWorldController` 類別，以使用視圖範本檔案，將產生 HTML 回應的程式完全封裝至用戶端。 

您將使用[Razor view 引擎](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)建立視圖範本檔案。 以 Razor 為基礎的視圖範本具有 *. cshtml*副檔名，並提供簡潔的方式來使用C#建立 HTML 輸出。 Razor 會將撰寫視圖範本時所需的字元和按鍵數目降至最低，並可提供快速、流暢的編碼工作流程。

目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。 變更 `Index` 方法以呼叫控制器[View](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View)方法，如下列程式碼所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

上述 `Index` 方法會使用視圖範本來產生瀏覽器的 HTML 回應。 控制器方法（也稱為[動作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)）（例如上述的 `Index` 方法）通常會傳回[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) （或衍生自[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)的類別），而不是像字串這樣的基本類型。

以滑鼠右鍵按一下 [ *Views\HelloWorld* ] 資料夾，按一下 [**新增**]，然後按一下 [**具有版面配置的 MVC 5 視圖頁面（Razor）** ]。
  
![](adding-a-view/_static/image1.png)   
  
在 [**指定專案的名稱**] 對話方塊中，輸入 [*索引*]，然後按一下 **[確定]** 。  
  
![](adding-a-view/_static/image2.png)  
  
在 [**選取版面配置頁**] 對話方塊中，接受預設的 [\_] [ **cshtml** ]，然後按一下 **[確定]** 。  
  
![](adding-a-view/_static/image3.png)  
  
在上面的對話方塊中，已在左窗格中選取 [ *Views\Shared* ] 資料夾。 如果您在另一個資料夾中有自訂的版面配置檔案，可以選取它。 我們稍後會在本教學課程中討論版面配置檔案

隨即建立*MvcMovie\Views\HelloWorld\Index.cshtml*檔案。

![](adding-a-view/_static/image4.png)

新增下列反白顯示的標記。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

以滑鼠右鍵按一下*索引. cshtml*檔案，然後選取 [**在瀏覽器中查看**]。

![PI](adding-a-view/_static/image5.png)

您也可以用滑鼠右鍵按一下*索引. cshtml*檔案，然後選取 [**在 Page Inspector 中的 View]。** 如需詳細資訊，請參閱[Page Inspector 教學](../../views/using-page-inspector-in-aspnet-mvc.md)課程。

或者，執行應用程式並流覽至 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。 控制器中的 `Index` 方法不會執行太多工做;它只會執行語句 `return View()`，這會指定方法應該使用視圖範本檔案來呈現瀏覽器的回應。 由於您未明確指定所要使用之視圖範本檔案的名稱，因此 ASP.NET MVC 會預設為使用 *\Views\HelloWorld*資料夾中的*Index. cshtml* view file。 下圖顯示我們的 View 範本中的字串 &quot;Hello！&quot; 在視圖中硬式編碼。

![](adding-a-view/_static/image6.png)

看起來不錯。 不過，請注意，瀏覽器的標題列會顯示「Index-My ASP.NET Application」，而頁面頂端的大連結則會指出「應用程式名稱」。 視您的瀏覽器視窗大小而定，您可能需要按一下右上角的三條線，才能看到 [**首頁**]、[**關於**]、[**連絡人**]、[**註冊**] 和 [**登入**] 連結。

## <a name="changing-views-and-layout-pages"></a>變更視圖和版面配置頁

首先，您想要變更頁面頂端的 [&quot;應用程式名稱]&quot; 連結。 這是每一頁通用的文字。 它實際上只會在專案的一個位置中實作為，即使它出現在應用程式的每個頁面上也一樣。 移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 *\_版面配置. cshtml*檔案。 這個檔案稱為版面配置*頁*，它位於所有其他頁面使用的共用資料夾中。

![_LayoutCshtml](adding-a-view/_static/image7.png)

版面配置範本可讓您在一處指定網站的 HTML 容器版面配置，然後將它套用到您網站中的多個頁面。 找到 `@RenderBody()` 這行。 `RenderBody` 是顯示您建立之所有檢視特定頁面的預留位置，「包裝」&quot;&quot;在版面配置頁中。 例如，如果您選取 [**關於**] 連結，則會在 `RenderBody` 方法中轉譯*Views\Home\About.cshtml*視圖。

變更標題元素的內容。 從 &quot;應用程式名稱&quot; 變更版面配置範本中的的[html.actionlink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) ，以 &quot;MVC 電影&quot; 以及從 `Home` 到 `Movies`的控制器。 完整的版面配置檔案如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

執行應用程式，並注意它現在會顯示 &quot;MVC Movie &quot;。 按一下 [**關於**] 連結，您會看到該頁面也會顯示 &quot;MVC 電影&quot;的方式。 我們能夠在版面配置範本中進行變更一次，並讓網站上的所有頁面反映新的標題。

![](adding-a-view/_static/image8.png)

當我們第一次建立*Views\HelloWorld\Index.cshtml*檔案時，它會包含下列程式碼：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

上述的 Razor 程式碼會明確設定版面配置頁。 檢查 *\\_ViewStart 的 Views*檔案，其中包含的 Razor 標記完全相同。 *[Views\\_ViewStart](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* ，會定義所有視圖都會使用的一般版面配置，因此您可以從*Views\HelloWorld\Index.cshtml*檔案將該程式碼標記為批註或從中移除。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

您可以使用 `Layout` 屬性來設定不同的版面配置檢視，或將它設定為 `null`，因此不會使用任何版面配置檔案。

現在，讓我們來變更索引視圖的標題。

開啟*MvcMovie\Views\HelloWorld\Index.cshtml*。 有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後是次要標頭（`<h2>` 元素）。 您會使這些變更略有不同，因此可看出哪一段程式碼變更了應用程式的哪個部分。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

若要指示要顯示的 HTML 標題，上述程式碼會設定 `ViewBag` 物件的 `Title` 屬性（位於*Index. cshtml* view template 中）。 請注意，版面配置範本（ *Views\Shared\\_Layout. cshtml* ）會在 `<title>` 專案中使用這個值，做為我們先前修改之 HTML 的 `<head>` 區段的一部分。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

使用這種 `ViewBag` 方法，您可以輕鬆地在您的視圖範本和配置檔案之間傳遞其他參數。

執行應用程式。 請注意，瀏覽器標題、主要標題和次要標題已變更 (如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。 在瀏覽器中按 Ctrl + F5，以強制載入伺服器的回應。）瀏覽器標題會使用*我們在 [&quot;] 視圖範本*中設定的 `ViewBag.Title` 來建立，並在配置檔案中新增額外的 Movie 應用程式&quot;。

同時也請注意，已將 [*建立*] 視圖範本中的內容與 [\_配置] [ *cshtml* ] 視圖範本合併，並將單一 HTML 回應傳送至瀏覽器。 版面配置範本可讓您輕鬆進行會套用到應用程式之所有頁面的變更。

![](adding-a-view/_static/image9.png)

不過，我們有點 &quot;的資料&quot; （在此情況下，我們的 View Template 中的 &quot;Hello！&quot; message）是硬式編碼的。 MVC 應用程式具有 &quot;V&quot; （view），而且您有 &quot;的 C&quot; （控制器），但尚未 &quot;M&quot; （model）。 很快地，我們將逐步解說如何建立資料庫，並從中抓取模型資料。

## <a name="passing-data-from-the-controller-to-the-view"></a>將資料從控制器傳遞至檢視

不過，在我們進入資料庫並討論模型之前，讓我們先討論如何將控制器的資訊傳遞給視圖。 系統會叫用控制器類別，以回應傳入的 URL 要求。 控制器類別是您撰寫程式碼來處理傳入瀏覽器要求、從資料庫抓取資料，最後決定要傳回給瀏覽器的回應類型。 然後，您可以從控制器使用視圖範本來產生並格式化瀏覽器的 HTML 回應。

控制器會負責提供所需的任何資料或物件，以便讓視圖範本呈現對瀏覽器的回應。 最佳做法：**視圖範本絕對不應執行商務邏輯，或直接與資料庫互動**。 相反地，「視圖」範本只能與由控制器提供給它的資料搭配使用。 維護這項 &quot;的顧慮&quot; 有助於讓程式碼保持整潔、可測試且更容易維護。

目前，`HelloWorldController` 類別中的 `Welcome` 動作方法會接受 `name` 和 `numTimes` 參數，然後將這些值直接輸出到瀏覽器。 不是讓控制器將此回應轉譯為字串，讓我們將控制器變更為改用 view 範本。 檢視範本會產生動態回應，這表示您需要將適當數量的資料從控制器傳遞至檢視，以便產生回應。 若要這麼做，您可以讓控制器將視圖範本所需的動態資料（參數）放置在 view 範本可以存取的 `ViewBag` 物件中。

返回*HelloWorldController.cs*檔案並變更 `Welcome` 方法，將 `Message` 和 `NumTimes` 值新增至 `ViewBag` 物件。 `ViewBag` 是動態物件，這表示您可以將任何想要的內容放在其中：`ViewBag` 物件沒有定義的屬性，直到您將內容放在其中為止。 [ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將指定的參數（`name` 和 `numTimes`）從網址列中的查詢字串對應至方法中的參數。 完整的 *HelloWorldController.cs* 檔案如下所示：

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

現在，`ViewBag` 物件包含將會自動傳遞至視圖的資料。 接下來，您需要一個歡迎視圖範本！ 在 [**建立**] 功能表中，選取 [**組建方案**] （或 Ctrl + Shift + B），以確定專案已編譯。 以滑鼠右鍵按一下 [ *Views\HelloWorld* ] 資料夾，按一下 [**新增**]，然後按一下 [**具有版面配置的 MVC 5 視圖頁面（Razor）** ]。
  
![](adding-a-view/_static/image10.png)   
  
在 [**指定專案的名稱**] 對話方塊中，輸入 [*歡迎*]，然後按一下 **[確定]** 。   
  
在 [**選取版面配置頁**] 對話方塊中，接受預設的 [\_] [ **cshtml** ]，然後按一下 **[確定]** 。  
  
![](adding-a-view/_static/image11.png)   

隨即建立*MvcMovie\Views\HelloWorld\Welcome.cshtml*檔案。

取代*歡迎的 cshtml*檔案中的標記。 您將建立一個迴圈，指出 &quot;Hello&quot; 的次數與使用者所說的數目一樣多。 完整的*歡迎使用 cshtml*檔案如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

執行應用程式，並流覽至下列 URL：

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

現在會從 URL 取得資料，並使用[模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結器傳遞至控制器。 控制器會將資料封裝到 `ViewBag` 物件中，並將該物件傳遞至 view。 然後，此視圖會以 HTML 將資料顯示給使用者。

![](adding-a-view/_static/image12.png)

在上述範例中，我們使用了 `ViewBag` 物件，將資料從控制器傳遞至 view。 稍後在教學課程中，我們將使用檢視模型將控制器中的資料傳遞至檢視。 傳遞資料的「視圖模型」方法通常是透過「視圖包」方法來處理的最佳作法。 如需詳細資訊，請參閱 blog 專案[Dynamic V 強](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)型別視圖。 

這是一種適用于模型的 &quot;M&quot;，但不是資料庫種類。 讓我們運用所學的內容，建立電影的資料庫。

> [!div class="step-by-step"]
> [上一頁](adding-a-controller.md)
> [下一頁](adding-a-model.md)
