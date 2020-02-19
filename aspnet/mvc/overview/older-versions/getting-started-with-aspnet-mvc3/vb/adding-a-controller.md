---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: 新增控制器（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457390"
---
# <a name="adding-a-controller-vb"></a>新增控制器 (VB)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。 [下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/adding-a-controller.md)。

MVC 代表*模型視圖控制器*。 MVC 是用來開發應用程式的模式，因此每個元件都有個別的責任：

- 模型：應用程式的資料。
- Views：應用程式將用來動態產生 HTML 回應的範本檔案。
- 控制器：處理應用程式傳入 URL 要求、抓取模型資料，然後指定將回應轉譯至用戶端的類別。

本教學課程將涵蓋所有這些概念，並示範如何使用它們來建立應用程式。

以滑鼠右鍵按一下**方案總管**中的 [*控制器*] 資料夾，然後選取 [新增**控制器**]，以建立新的控制器。

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

將新的控制器命名為 &quot;HelloWorldController&quot;，然後按一下 [**新增**]。

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

請注意，在右側**方案總管**中，已為您建立了名為*HelloWorldController.cs*的新檔案，而且該檔案已在 IDE 中開啟。

在新的 `public class HelloWorldController` 區塊內，建立兩個新的方法，看起來像下列程式碼。 我們會直接從控制器傳回 HTML 字串作為範例。

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

您的控制器命名為 `HelloWorldController`，而新方法的名稱為 `Index`。 執行應用程式（按 F5 或 Ctrl + F5）。 當您的瀏覽器啟動之後，將 &quot;HelloWorld&quot; 附加至網址列中的路徑。 （在我的電腦上，它是 `http://localhost:43246/HelloWorld`）您的瀏覽器看起來會像下面的螢幕擷取畫面。 在上述方法中，程式碼會直接傳回字串。 我們已告訴系統只傳回一些 HTML，而且的確有！

![](adding-a-controller/_static/image5.png)

ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。 ASP.NET MVC 使用的預設對應邏輯會使用類似如下的格式來控制要叫用的程式碼：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一個部分會決定要執行的控制器類別。 因此， */HelloWorld*會對應至 `HelloWorldController` 類別。 URL 的第二個部分會決定要執行的類別上的動作方法。 因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。 請注意，我們只需要造訪上述 */HelloWorld* ，預設會使用 `Index` 方法。 這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。

瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法會執行並傳回字串 &quot;這是歡迎動作方法 ...&quot;。 預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。 針對此 URL，控制器會 `HelloWorld`，`Welcome` 是方法。 尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image6.png)

讓我們稍微修改範例，讓我們可以從 URL 將中的一些參數資訊傳遞到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。 變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。 請注意，我們使用了 VB 選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

執行您的應用程式，並流覽至 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **。** 您可以嘗試不同的 `name` 和 `numtimes`值。 系統會自動將網址列中查詢字串的已具名引數對應至方法中的參數。

![](adding-a-controller/_static/image7.png)

在這兩個範例中，控制器已執行 MVC 的 VC 部分，也就是「視圖」和「控制器」工作。 控制器會直接傳回 HTML。 一般來說，我們不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。 相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。 我們來看一下如何做到這一點。

> [!div class="step-by-step"]
> [上一頁](intro-to-aspnet-mvc-3.md)
> [下一頁](adding-a-view.md)
