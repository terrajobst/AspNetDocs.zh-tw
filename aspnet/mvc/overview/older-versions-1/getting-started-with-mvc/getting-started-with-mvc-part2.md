---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 新增控制器 |Microsoft Docs
author: shanselman
description: 如果本教學課程可在此使用 Visual Studio 2013，則為更新版本。 新的教學課程使用 ASP.NET MVC 5，它提供了許多透過 t 的改良功能 。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543978"
---
# <a name="adding-a-controller"></a>新增控制器

由[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。 新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。
>
>
> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

MVC 代表 Model、View、Controller。 MVC 是用來開發應用程式的模式，因此每個部分的責任與另一個元件不同。

- 模型：應用程式的資料
- Views：應用程式將用來動態產生 HTML 回應的範本檔案。
- 控制器：處理應用程式傳入 URL 要求、捕獲模型資料，然後指定將回應轉譯回用戶端的類別

本教學課程將涵蓋所有這些概念，並示範如何使用它們來建立應用程式。

讓我們建立新的控制器，方法是以滑鼠右鍵按一下 [方案瀏覽器] 中的 [控制器] 資料夾，然後選取 [新增控制器]。

[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

將新的控制器命名為 "HelloWorldController"，然後按一下 [新增]。

[![新增控制器 對話方塊](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

請注意，在右邊的方案總管中，已為您建立了名為 HelloWorldController.cs 的新檔案，而該檔案現在已在**IDE**中開啟。

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

建立兩個新的方法，在新的公用類別 HelloWorldController 中看起來像這樣。 我們會直接從我們的控制器傳回 HTML 字串，做為範例。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

您的控制器命名為 HelloWorldController，而您的新方法稱為 Index。 再次執行您的應用程式，就像之前一樣（按一下 [播放] 按鈕，或按 F5 鍵來執行此動作）。 當您的瀏覽器啟動之後，請將網址列中的路徑變更為 `http://localhost:xx/HelloWorld`，其中 xx 是您的電腦所選擇的任何數位。 現在，您的瀏覽器看起來應該像下面的螢幕擷取畫面。 在上述方法中，我們傳回傳遞至稱為「內容」之方法的字串。 我們告訴系統只傳回一些 HTML，而且的確會傳回！

ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。 ASP.NET MVC 使用的預設對應邏輯會使用如下的格式來控制要執行的程式碼：

/[控制器]/[ActionName]/[Parameters]

URL 的第一個部分會決定要執行的控制器類別。 因此，/HelloWorld 會對應至 HelloWorldController 類別。 URL 的第二個部分會決定要執行的類別上的動作方法。 因此，/HelloWorld/Index 會導致 HelloWorldController 類別的 Index （）方法執行。 請注意，我們只需要造訪上面的/HelloWorld，並隱含方法索引。 這是因為名為 "Index" 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。

[![這是我的預設動作](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

現在，讓我們流覽 `http://localhost:xx/HelloWorld/Welcome.` 我們的歡迎方法現在已執行，並傳回其 HTML 字串。

同樣地，/[控制器]/[ActionName]/[Parameters]，讓控制器 HelloWorld，而歡迎是在此情況下的方法。 尚未完成參數。

[![這是歡迎動作方法](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

讓我們稍微修改我們的範例，讓我們可以從 URL 將中的某些資訊傳遞至控制器，例如：/HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4。 變更您的 [歡迎使用] 方法以包含兩個參數，並如下所示更新它。 請注意，我們使用了C#選擇性參數功能，表示如果未傳入參數 numtimes is，它應該預設為1。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

執行您的應用程式，並視需要流覽 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 變更 name 和 numtimes is 的值。 系統會自動將您的查詢字串中的已具名引數對應至方法中的參數。

在這兩個範例中，控制器都已執行所有工作，並已直接傳回 HTML。 一般來說，我們不希望控制器直接傳回 HTML，因為這會使程式碼變得非常繁瑣。 相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。 我們來看一下如何做到這一點。 關閉瀏覽器並返回 IDE。

> [!div class="step-by-step"]
> [上一頁](getting-started-with-mvc-part1.md)
> [下一頁](getting-started-with-mvc-part3.md)
