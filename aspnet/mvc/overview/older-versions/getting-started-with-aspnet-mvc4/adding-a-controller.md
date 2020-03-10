---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 新增控制器 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599838"
---
# <a name="adding-a-controller"></a>新增控制器

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。

MVC 代表*模型視圖控制器*。 MVC 是一種模式，可供開發良好架構、可測試且易於維護的應用程式。 以 MVC 為基礎的應用程式包含：

- **M**模型 ()：代表應用程式資料的類別，並使用驗證邏輯來強制執行該資料的商務規則。
- **V**檢視 ()：您的應用程式用來動態產生 HTML 回應的範本檔案。
- **C**控制器 ()：處理傳入瀏覽器要求、抓取模型資料，然後指定會傳回瀏覽器回應的視圖範本的類別。

我們將在此教學課程系列中涵蓋所有這些概念，並示範如何使用它們來建立應用程式。

讓我們從建立控制器類別開始。 在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後選取 [**新增控制器**]。

![](adding-a-controller/_static/image1.png)

將新的控制器命名為 &quot;HelloWorldController&quot;。 將預設範本保留為**空白的 MVC 控制器**，然後按一下 [**新增**]。

![新增控制器](adding-a-controller/_static/image2.png)

請注意，在**方案總管**中，已建立名為*HelloWorldController.cs*的新檔案。 檔案已在 IDE 中開啟。

![](adding-a-controller/_static/image3.png)

以下列程式碼取代檔案的內容。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

控制器方法會傳回 HTML 字串做為範例。 控制器的名稱為 `HelloWorldController`，而上述第一個方法的名稱為 `Index`。 讓我們從瀏覽器叫用它。 執行應用程式（按 F5 或 Ctrl + F5）。 在瀏覽器中，將 &quot;HelloWorld&quot; 附加至網址列中的路徑。 （例如，在下圖中，它是 `http://localhost:1234/HelloWorld.`）瀏覽器中的頁面看起來會如下列螢幕擷取畫面所示。 在上述方法中，程式碼會直接傳回字串。 您已告訴系統只傳回一些 HTML，而且的確有！

![](adding-a-controller/_static/image4.png)

ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。 ASP.NET MVC 使用的預設 URL 路由邏輯會使用類似如下的格式來判斷要叫用的程式碼：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一個部分會決定要執行的控制器類別。 因此， */HelloWorld*會對應至 `HelloWorldController` 類別。 URL 的第二個部分會決定要執行的類別上的動作方法。 因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。 請注意，我們只需要流覽至 */HelloWorld* ，預設會使用 `Index` 方法。 這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。

瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法會執行並傳回字串 &quot;這是歡迎動作方法 ...&quot;。 預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。 在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。 您尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image5.png)

讓我們稍微修改範例，讓您可以將 URL 中的某些參數資訊傳遞至控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。 變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。 請注意，程式碼會C#使用選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

執行您的應用程式，並流覽至範例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。 您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。 [ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將來自網址列中的查詢字串的已具名引數對應至方法中的參數。

![](adding-a-controller/_static/image6.png)

在這兩個範例中，控制器已執行 MVC 的 &quot;VC&quot; 部分，也就是視圖和控制器工作。 控制器會直接傳回 HTML。 一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。 相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。 我們來看一下如何執行這個動作。

> [!div class="step-by-step"]
> [上一頁](intro-to-aspnet-mvc-4.md)
> [下一頁](adding-a-view.md)
