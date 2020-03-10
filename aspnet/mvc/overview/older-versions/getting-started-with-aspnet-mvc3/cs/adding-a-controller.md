---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 新增控制器（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540940"
---
# <a name="adding-a-controller-c"></a>新增控制器 (C#)

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

MVC 代表*模型視圖控制器*。 MVC 是一種模式，可用於開發架構良好且易於維護的應用程式。 以 MVC 為基礎的應用程式包含：

- 控制器：處理應用程式的傳入要求、抓取模型資料，然後指定將回應傳回給用戶端之視圖範本的類別。
- 模型：代表應用程式資料的類別，並使用驗證邏輯來強制執行該資料的商務規則。
- Views：您的應用程式用來動態產生 HTML 回應的範本檔案。

我們將在此教學課程系列中涵蓋所有這些概念，並示範如何使用它們來建立應用程式。

讓我們從建立控制器類別開始。 在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後選取 [**新增控制器**]。

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

將新的控制器命名為 "HelloWorldController"。 將 [預設範本] 保留為**空白控制器**，然後按一下 [**新增**]。

[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

請注意，在**方案總管**中，已建立名為*HelloWorldController.cs*的新檔案。 檔案已在 IDE 中開啟。

![](adding-a-controller/_static/image5.png)

在 `public class HelloWorldController` 區塊內，建立兩個類似下列程式碼的方法。 控制器會傳回 HTML 字串做為範例。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

您的控制器命名為 `HelloWorldController`，而上述第一個方法的名稱為 `Index`。 讓我們從瀏覽器叫用它。 執行應用程式（按 F5 或 Ctrl + F5）。 在瀏覽器中，將 "HelloWorld" 附加至網址列中的路徑。 （例如，在下圖中，它是 `http://localhost:43246/HelloWorld.`）瀏覽器中的頁面看起來會如下列螢幕擷取畫面所示。 在上述方法中，程式碼會直接傳回字串。 您已告訴系統只傳回一些 HTML，而且的確有！

![](adding-a-controller/_static/image6.png)

ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。 ASP.NET MVC 使用的預設對應邏輯會使用類似如下的格式來判斷要叫用的程式碼：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一個部分會決定要執行的控制器類別。 因此， */HelloWorld*會對應至 `HelloWorldController` 類別。 URL 的第二個部分會決定要執行的類別上的動作方法。 因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。 請注意，我們只需要流覽至 */HelloWorld* ，預設會使用 `Index` 方法。 這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。

瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法隨即執行，並傳回字串 "This is the Welcome action method..."。 預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。 在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。 您尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image7.png)

讓我們稍微修改範例，讓您可以將 URL 中的某些參數資訊傳遞至控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。 變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。 請注意，程式碼會C#使用選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

執行您的應用程式，並流覽至範例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。 您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。 系統會自動將來自網址列中的查詢字串的已具名引數對應至方法中的參數。

![](adding-a-controller/_static/image8.png)

在這兩個範例中，控制器已執行 MVC 的 "VC" 部分，也就是視圖和控制器工作。 控制器會直接傳回 HTML。 一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。 相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。 我們來看一下如何執行這個動作。

> [!div class="step-by-step"]
> [上一頁](intro-to-aspnet-mvc-3.md)
> [下一頁](adding-a-view.md)
