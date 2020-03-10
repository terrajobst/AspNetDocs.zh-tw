---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 第2部分：控制器 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第2部分涵蓋控制器。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559875"
---
# <a name="part-2-controllers"></a>第2部分：控制器

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第2部分涵蓋控制器。

使用傳統的 web 架構時，連入的 Url 通常會對應到磁片上的檔案。 例如： "/Products.aspx" 或 "/Products.php" 等 URL 的要求可能會由 "Products" 或 "Products. php" 檔案處理。

以 Web 為基礎的 MVC 架構會以稍有不同的方式將 Url 對應至伺服器程式碼。 與其將傳入 Url 對應至檔案，它們會改為將 Url 對應至類別上的方法。 這些類別稱為「控制器」，負責處理傳入 HTTP 要求、處理使用者輸入、抓取和儲存資料，以及判斷要傳回給用戶端的回應（顯示 HTML、下載檔案、重新導向至不同的URL 等）。

## <a name="adding-a-homecontroller"></a>新增 HomeController

我們將會藉由新增控制器類別來處理我們網站首頁的 Url，以開始使用 MVC 音樂存放區應用程式。 我們將遵循 ASP.NET MVC 的預設命名慣例，並將其稱為 HomeController。

以滑鼠右鍵按一下方案總管中的 [控制器] 資料夾，然後依序選取 [新增] 和 [控制器 ...]命令

![](mvc-music-store-part-2/_static/image1.jpg)

這會顯示 [新增控制器] 對話方塊。 將控制器命名為 "HomeController"，然後按 [新增] 按鈕。

![](mvc-music-store-part-2/_static/image1.png)

這會使用下列程式碼建立新的檔案 HomeController.cs：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

為了盡可能地開始，讓我們將 Index 方法取代為只傳回字串的簡單方法。 我們會進行兩個變更：

- 變更方法以傳回字串，而不是 ActionResult
- 變更 return 語句以傳回 "Hello from Home"

方法現在看起來應該像這樣：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>執行應用程式

現在讓我們來執行網站。 我們可以啟動我們的 web 伺服器，並使用下列任何一項來試用網站：

- 選擇 [Debug ⇨] [開始調試] 功能表項目
- 按一下工具列中的綠色箭號按鈕 ![](mvc-music-store-part-2/_static/image2.jpg)
- 使用鍵盤快速鍵 F5。

使用上述任何步驟，將會編譯我們的專案，然後讓 Visual Web Developer 內建的 ASP.NET 程式開發伺服器開始。 畫面的右下角會顯示通知，指出 ASP.NET 程式開發伺服器已啟動，並會顯示其執行所在的埠號碼。

![](mvc-music-store-part-2/_static/image2.png)

Visual Web Developer 接著會自動開啟瀏覽器視窗，其 URL 指向我們的 Web 服務器。 這可讓我們快速試用我們的 web 應用程式：

![](mvc-music-store-part-2/_static/image3.png)

好啦，我們建立了新的網站，新增了三行功能，而且在瀏覽器中有文字。 不是 rocket 科學，而是一開始。

*注意： Visual Web Developer 包含 ASP.NET 程式開發伺服器，會以隨機免費的「埠」號碼執行您的網站。在上方的螢幕擷取畫面中，網站會在 `http://localhost:26641/`執行，因此它會使用埠26641。您的埠號碼會不同。當我們在本教學課程中討論 URL 的類似/Store/Browse 時，將會在埠號碼之後。假設埠號碼為26641，流覽至/Store/Browse 就表示流覽 `http://localhost:26641/Store/Browse`。*

## <a name="adding-a-storecontroller"></a>新增 StoreController

我們新增了一個簡單的 HomeController，可實現網站的首頁。 現在讓我們新增另一個控制器，我們將用它來執行音樂存放區的流覽功能。 我們的存放區控制器將支援三種案例：

- 音樂存放區中音樂內容的清單頁面
- 列出特定內容類型中所有音樂專輯的流覽頁面
- 顯示特定音樂專輯相關資訊的詳細資料頁面

首先，我們要加入新的 StoreController 類別。 如果您還沒有這麼做，請關閉瀏覽器或選取 [Debug ⇨停止偵錯工具] 功能表項目，以停止執行應用程式。

現在加入新的 StoreController。 就像我們在 HomeController 中所做的一樣，只要以滑鼠右鍵按一下方案總管中的 [控制器] 資料夾，然後選擇 [加入&gt;控制器] 功能表項目，就可以做到這一點。

![](mvc-music-store-part-2/_static/image4.png)

我們的新 StoreController 已經有 "Index" 方法。 我們將使用此「索引」方法來執行清單頁面，其中列出我們的音樂存放區中的所有內容類型。 我們也會新增兩個其他方法，以執行我們想要讓 StoreController 處理的其他兩個案例：流覽和詳細資料。

在控制器內的這些方法（索引、流覽和詳細資料）稱為「控制器動作」，而且您已經看到 HomeController （）動作方法，其工作是回應 URL 要求，而（通常是說）決定哪些內容應該傳送回叫用 URL 的瀏覽器或使用者。

我們將藉由變更 theIndex （）方法來啟動我們的 StoreController 執行，以傳回字串 "Hello from Store. Index （）"，我們將為 Browse （）和 Details （）新增類似的方法：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

再次執行專案，並流覽下列 Url：

- /Store
- /Store/Browse
- /Store/Details

存取這些 Url 將會叫用控制器中的動作方法，並傳回字串回應：

![](mvc-music-store-part-2/_static/image5.png)

這很棒，但這些只是常數位串。 讓我們將其設為動態，讓他們從 URL 中取出資訊，並將它顯示在頁面輸出中。

首先，我們將變更 [流覽動作] 方法，以從 URL 抓取 querystring 值。 我們可以藉由將「內容類型」參數新增至動作方法來達到此目的。 當我們執行此 ASP.NET 時，MVC 會在叫用時，自動將名為 "內容類型的任何 querystring 或表單 post 參數傳遞至動作方法。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*注意：我們會使用 Httputility.htmlencode. HtmlEncode 公用程式方法來淨化使用者輸入。這可防止使用者使用/Store/Browse 之類的連結將 JAVAscript 插入我們的視圖中？內容類型 =&lt;腳本&gt;視窗。位置 = 'http://hackersite.com'&lt;/script&gt;。*

現在讓我們流覽至/Store/Browse 嗎？內容類型 = Disco

![](mvc-music-store-part-2/_static/image6.png)

接著，讓我們將 [詳細資料] 動作變更為 [讀取]，並顯示名為 ID 的輸入參數。 與先前的方法不同的是，我們不會將識別碼值內嵌為 querystring 參數。 相反地，我們會直接將它內嵌在 URL 本身內。 例如：/Store/Details/5。

ASP.NET MVC 可讓我們輕鬆執行此動作，而不需要進行任何設定。 ASP.NET MVC 的預設路由慣例是在動作方法名稱之後，將 URL 的區段視為名為 "ID" 的參數。 如果您的動作方法具有名為 ID 的參數，則 ASP.NET MVC 會自動將 URL 區段當做參數傳遞給您。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

執行應用程式，並流覽至/Store/Details/5：

![](mvc-music-store-part-2/_static/image7.png)

我們來回顧到目前為止所做的事：

- 我們已在 Visual Web Developer 中建立新的 ASP.NET MVC 專案
- 我們已討論過 ASP.NET MVC 應用程式的基本資料夾結構
- 我們已瞭解如何使用 ASP.NET 程式開發伺服器來執行我們的網站
- 我們建立了兩個控制器類別： HomeController 和 StoreController
- 我們已在控制器上新增動作方法，以回應 URL 要求並將文字傳回瀏覽器

> [!div class="step-by-step"]
> [上一頁](mvc-music-store-part-1.md)
> [下一頁](mvc-music-store-part-3.md)
