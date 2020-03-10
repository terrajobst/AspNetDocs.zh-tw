---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 新增控制器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 194a8a7398e163f0c37164a8724f98b16444984b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615805"
---
# <a name="adding-a-controller"></a>新增控制器

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

MVC 代表*模型視圖控制器*。 MVC 是一種模式，可供開發良好架構、可測試且易於維護的應用程式。 以 MVC 為基礎的應用程式包含：

- **M**模型 ()：代表應用程式資料的類別，並使用驗證邏輯來強制執行該資料的商務規則。
- **V**檢視 ()：您的應用程式用來動態產生 HTML 回應的範本檔案。
- **C**控制器 ()：處理傳入瀏覽器要求、抓取模型資料，然後指定會傳回瀏覽器回應的視圖範本的類別。

我們將在此教學課程系列中涵蓋所有這些概念，並示範如何使用它們來建立應用程式。

讓我們從建立控制器類別開始。 在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後依序按一下 [**新增**]、[**控制器**]。

![](adding-a-controller/_static/image1.png)

在 [**新增 Scaffold** ] 對話方塊中，按一下 [ **MVC 5 控制器-空白**]，然後按一下 [**新增**]。

![](adding-a-controller/_static/image2.png)  

將新的控制器命名為 "HelloWorldController"，然後按一下 [**新增**]。

![新增控制器](adding-a-controller/_static/image3.png)

請注意，在**方案總管**中，已建立名為*HelloWorldController.cs*的新檔案和新的資料夾*Views\HelloWorld*。 控制器已在 IDE 中開啟。

![](adding-a-controller/_static/image4.png)

以下列程式碼取代檔案的內容。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

控制器方法會傳回 HTML 字串做為範例。 控制器的名稱為 `HelloWorldController`，而第一個方法的名稱為 `Index`。 讓我們從瀏覽器叫用它。 執行應用程式（按 F5 或 Ctrl + F5）。 在瀏覽器中，將 &quot;HelloWorld&quot; 附加至網址列中的路徑。 （例如，在下圖中，它是 `http://localhost:1234/HelloWorld.`）瀏覽器中的頁面看起來會如下列螢幕擷取畫面所示。 在上述方法中，程式碼會直接傳回字串。 您已告訴系統只傳回一些 HTML，而且的確有！

![](adding-a-controller/_static/image5.png)

ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。 ASP.NET MVC 使用的預設 URL 路由邏輯會使用類似如下的格式來判斷要叫用的程式碼：

`/[Controller]/[ActionName]/[Parameters]`

您可以在應用程式中設定路由的格式， *\_啟動/RouteConfig .cs*檔案。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

當您執行應用程式但未提供任何 URL 區段時，它會預設為上述程式碼的 [預設值] 區段中所指定的 "Home" 控制器和 "Index" 動作方法。

URL 的第一個部分會決定要執行的控制器類別。 因此， */HelloWorld*會對應至 `HelloWorldController` 類別。 URL 的第二個部分會決定要執行的類別上的動作方法。 因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。 請注意，我們只需要流覽至 */HelloWorld* ，預設會使用 `Index` 方法。 這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。 URL 區段的第三個部分 (`Parameters`) 是路由資料。 我們稍後會在本教學課程中看到路由資料。

瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法會執行並傳回字串 &quot;這是歡迎動作方法 ...&quot;。 預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。 在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。 您尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image6.png)

讓我們稍微修改範例，讓您可以將 URL 中的某些參數資訊傳遞至控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。 變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。 請注意，程式碼會C#使用選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> 安全性注意事項：上述程式碼會使用[HTTPutility.htmlencode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)來保護應用程式免于惡意的輸入（亦即 JavaScript）。 如需詳細資訊，請參閱[如何：在 Web 應用程式中防止腳本惡意探索，方法是將 HTML 編碼套用至字串](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)。

 執行您的應用程式，並流覽至範例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`）。 您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。 [ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將來自網址列中的查詢字串的已具名引數對應至方法中的參數。

![](adding-a-controller/_static/image7.png)

在上述範例中，不會使用 URL 區段（`Parameters`），`name` 和 `numTimes` 參數會當做[查詢字串](http://en.wikipedia.org/wiki/Query_string)傳遞。 ? 上述 URL 中的（問號）是分隔符號，而且查詢字串會跟著。 &amp; 字元可分隔查詢字串。

使用下列程式碼取代歡迎方法：

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

執行應用程式，並輸入下列 URL： `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

這次第三個 URL 區段符合路由參數 `ID.` `Welcome` 動作方法包含符合 `RegisterRoutes` 方法中 URL 規格的參數（`ID`）。

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

在 ASP.NET MVC 應用程式中，較常見的方式是將參數當做路由資料傳遞（像是上述的識別碼），而不是將它們當做查詢字串傳遞。 您也可以新增路由，以將參數中的 `name` 和 `numtimes` 傳遞至 URL 中的路由資料。 在*應用程式\_Start\RouteConfig.cs*檔案中，新增 "Hello" 路由：

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

執行應用程式，並流覽至 `/localhost:XXX/HelloWorld/Welcome/Scott/3`。

![](adding-a-controller/_static/image9.png)

對於許多 MVC 應用程式而言，預設路由運作正常。 您稍後會在本教學課程中瞭解如何使用模型系結器來傳遞資料，而且您不需要修改該的預設路由。

在這些範例中，控制器已執行 MVC 的 &quot;VC&quot; 部分，也就是視圖和控制器工作。 控制器會直接傳回 HTML。 一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。 相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。 我們來看一下如何執行這個動作。

> [!div class="step-by-step"]
> [上一頁](getting-started.md)
> [下一頁](adding-a-view.md)
