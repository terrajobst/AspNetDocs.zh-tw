---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
title: 主版頁面和 ASP.NET AJAX （VB） |Microsoft Docs
author: rick-anderson
description: 討論使用 ASP.NET AJAX 和主版頁面的選項。 查看如何使用 ScriptManagerProxy 類別;討論如何將各種 JS 檔案載入 dependi 。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 0ee9318c-29bb-4d58-b1dc-94e575b8ae10
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
msc.type: authoredcontent
ms.openlocfilehash: 7be4ff422b91321ff83ed1f1c731c9a0bfe768f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525603"
---
# <a name="master-pages-and-aspnet-ajax-vb"></a>主版頁面與 ASP.NET AJAX (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_VB.zip)或[下載 PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_VB.pdf)

> 討論使用 ASP.NET AJAX 和主版頁面的選項。 查看如何使用 ScriptManagerProxy 類別;討論如何載入各種 JS 檔案，取決於是否在主版頁面或內容頁面中使用 ScriptManager。

## <a name="introduction"></a>簡介

過去幾年來，越來越多的開發人員建立了啟用 AJAX 的 web 應用程式。 啟用 AJAX 的網站會使用許多相關的 web 技術，以提供更快速的使用者體驗。 由於 Microsoft 的 ASP.NET AJAX 架構，建立啟用 AJAX 的 ASP.NET 應用程式出乎意料簡單。 ASP.NET AJAX 內建于 ASP.NET 3.5 和 Visual Studio 2008;它也可作為 ASP.NET 2.0 應用程式的個別下載。

使用 ASP.NET AJAX 架構建立具備 AJAX 功能的網頁時，您必須在每個使用該架構的頁面中，精確地新增一個 ScriptManager 控制項。 正如其名，ScriptManager 會管理在啟用 AJAX 的網頁中使用的用戶端腳本。 ScriptManager 至少會發出 HTML，指示瀏覽器下載構成 ASP.NET AJAX 用戶端程式庫的 JavaScript 檔案。 它也可以用來註冊自訂 JavaScript 檔案、啟用腳本的 web 服務，以及自訂的應用程式服務功能。

如果您的網站使用主版頁面（如其所示），則不一定需要將 ScriptManager 控制項新增至每個單一內容頁面;相反地，您可以將 ScriptManager 控制項加入至主版頁面。 本教學課程說明如何將 ScriptManager 控制項新增至主版頁面。 它也會探討如何使用 ScriptManagerProxy 控制項，在特定的內容頁面中註冊自訂腳本和腳本服務。

> [!NOTE]
> 本教學課程不會探索使用 ASP.NET AJAX 架構來設計或建立具備 AJAX 功能的 web 應用程式。 如需使用 AJAX 的詳細資訊，請參閱 ASP.NET AJAX 影片和教學課程，以及本教學課程結尾的進一步閱讀一節中所列的資源。

## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>檢查 ScriptManager 控制項發出的標記

ScriptManager 控制項會發出標記，指示瀏覽器下載構成 ASP.NET AJAX 用戶端程式庫的 JavaScript 檔案。 它也會在初始化此程式庫的頁面上新增一些內嵌 JavaScript。 下列標記顯示加入至包含 ScriptManager 控制項的頁面呈現輸出中的內容：

[!code-html[Main](master-pages-and-asp-net-ajax-vb/samples/sample1.html)]

`<script src="url"></script>` 標記會指示瀏覽器在*url*下載並執行 JavaScript 檔案。 ScriptManager 發出三種這類標記;其中一個參考檔案 `WebResource.axd`，另兩個則參考檔案 `ScriptResource.axd`。 這些檔案實際上不會以檔案的形式存在於您的網站中。 相反地，當下列其中一個檔案的要求抵達 web 伺服器時，ASP.NET 引擎會檢查 querystring 並傳回適當的 JavaScript 內容。 這三個外部 JavaScript 檔案提供的腳本構成 ASP.NET AJAX 架構的用戶端程式庫。 ScriptManager 所發出的其他 `<script>` 標記會包含初始化此程式庫的內嵌腳本。

ScriptManager 發出的外部腳本參考和內嵌腳本，對於使用 ASP.NET AJAX 架構的頁面而言是不可或缺的，但不需要用於不使用架構的頁面。 因此，您可能會因為只將 ScriptManager 新增至使用 ASP.NET AJAX 架構的網頁。 這就已經足夠，但如果您有許多使用此架構的頁面，您最後會將 ScriptManager 控制項新增至所有頁面，也就是重複性的工作，最少。 或者，您也可以將 ScriptManager 新增至主版頁面，然後將此必要腳本插入所有內容頁面。 使用此方法時，您不需要記得將 ScriptManager 新增至使用 ASP.NET AJAX 架構的新頁面，因為它已經由主版頁面包含。 步驟1會逐步解說如何將 ScriptManager 新增至主版頁面。

> [!NOTE]
> 如果您計畫在主版頁面的使用者介面中包含 AJAX 功能，則您沒有任何選擇，因為您必須在主版頁面中包含 ScriptManager。

將 ScriptManager 新增至主版頁面的一個缺點是，上述腳本會在*每個*頁面中發出，不論其是否需要。 這顯然會導致已包含 ScriptManager 的頁面（透過主版頁面）所浪費的頻寬，但不會使用 ASP.NET AJAX 架構的任何功能。 但是，只有多少頻寬浪費？

- ScriptManager 所發出的實際內容（如上所示）總計超過 1 KB。
- 不過，`<script>` 元素所參考的三個外部腳本檔案，都包含未壓縮的資料450KB。在使用 gzip 壓縮的網站中，此總頻寬可以減少接近 100 KB。 不過，瀏覽器會將這些腳本檔案快取一年，表示只需要下載一次，然後就可以在網站上的其他頁面中重複使用。

在最佳情況下，當快取腳本檔案時，總成本是1KB，這是可忽略的。 不過，在最糟的情況下（也就是腳本檔案尚未下載，而 web 伺服器不是使用任何形式的壓縮）時，頻寬就會450KB，這可以透過寬頻連線，從一或兩個位置新增到最多一分鐘的 透過撥號數據機的使用者。 好消息是，因為外部腳本檔案是由瀏覽器快取，所以不常發生這種最壞的情況。

> [!NOTE]
> 如果您仍然不想將 ScriptManager 控制項放在主版頁面中，請考慮 Web Form （主版頁面中的 `<form runat="server">` 標記）。 使用回傳模型的每個 ASP.NET 網頁都必須精確包含一個 Web 表單。 新增 Web 表單會加入其他內容：一些隱藏的表單欄位、`<form>` 標記本身，以及必要時，用來從腳本起始回傳的 JavaScript 函數。 不回傳的頁面不需要這個標記。 從主版頁面移除 Web 表單，並手動將它新增至每個需要一個的內容頁面，即可排除這個無關的標記。 不過，在主版頁面中擁有 Web 表單的優點，比不必要地將它加入特定內容頁面的缺點。

## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>步驟1：將 ScriptManager 控制項加入至主版頁面

使用 ASP.NET AJAX 架構的每個網頁都必須精確包含一個 ScriptManager 控制項。 基於這項需求，通常可以將單一 ScriptManager 控制項放在主版頁面上，如此一來，所有內容頁面就會自動包含 ScriptManager 控制項。 此外，ScriptManager 必須位於任何 ASP.NET AJAX 伺服器控制項之前，例如 UpdatePanel 和 UpdateProgress 控制項。 因此，最好是將 ScriptManager 放在 Web 表單中的任何 ContentPlaceHolder 控制項之前。

開啟 `Site.master` 主版頁面，並將 ScriptManager 控制項新增至 Web 表單中的頁面，但在 `<div id="topContent">` 元素之前（請參閱 [圖 1]）。 如果您使用的是 Visual Web Developer 2008 或 Visual Studio 2008，ScriptManager 控制項位於 [AJAX 延伸模組] 索引標籤的 [工具箱] 中。如果您使用 Visual Studio 2005，就必須先安裝 ASP.NET AJAX 架構，並將控制項加入 [工具箱] 中。 請造訪 ASP.NET AJAX 下載頁面，以取得 ASP.NET 2.0 的架構。

將 ScriptManager 新增至頁面之後，請將其 `ID` 從 `ScriptManager1` 變更為 `MyManager`。

[![將 ScriptManager 新增至主版頁面](master-pages-and-asp-net-ajax-vb/_static/image2.png)](master-pages-and-asp-net-ajax-vb/_static/image1.png)

**圖 01**：將 ScriptManager 新增至主版頁面（[按一下以觀看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image3.png)）

## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>步驟2：從內容頁面使用 ASP.NET AJAX 架構

將 ScriptManager 控制項加入至主版頁面之後，我們現在可以將 ASP.NET AJAX framework 功能新增至任何內容頁面。 讓我們建立新的 ASP.NET 網頁，以顯示從 Northwind 資料庫隨機選取的產品。 我們將使用 ASP.NET AJAX 架構的 Timer 控制項，每隔15秒更新此顯示，並顯示新的產品。

首先，在名為 `ShowRandomProduct.aspx`的根目錄中建立新的頁面。 別忘了將這個新頁面系結到 `Site.master` 主版頁面。

[![將新的 ASP.NET 網頁新增至網站](master-pages-and-asp-net-ajax-vb/_static/image5.png)](master-pages-and-asp-net-ajax-vb/_static/image4.png)

**圖 02**：將新的 ASP.NET 網頁新增至網站（[按一下以觀看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image6.png)）

回想一下，在主版頁面 [SKM1] 教學課程中指定標題、中繼標記和其他 HTML 標頭時，我們建立了名為 `BasePage` 的自訂基底頁面類別，如果未明確設定，則會產生頁面標題。 移至 `ShowRandomProduct.aspx` 頁面的程式碼後置類別，並讓它衍生自 `BasePage` （而不是從 `System.Web.UI.Page`）。

最後，更新 `Web.sitemap` 檔案以包含此課程的專案。 在 [主要到內容] 頁面互動課程的 `<siteMapNode>` 下方新增下列標記：

[!code-xml[Main](master-pages-and-asp-net-ajax-vb/samples/sample2.xml)]

此 `<siteMapNode>` 專案的加入會反映在課程清單中（請參閱 [圖 5]）。

### <a name="displaying-a-randomly-selected-product"></a>顯示隨機選取的產品

返回 `ShowRandomProduct.aspx`。 從設計工具中，將 [UpdatePanel] 控制項從 [工具箱] 拖曳至 [`MainContent` 內容] 控制項，並將其 [`ID`] 屬性設定為 [`ProductPanel`]。 UpdatePanel 代表螢幕上的一個區域，可以透過部分頁面回傳以非同步方式更新。

我們的第一項工作是顯示 UpdatePanel 中隨機選取之產品的相關資訊。 從將 DetailsView 控制項拖曳至 UpdatePanel 開始。 將 DetailsView 控制項的 `ID` 屬性設定為 `ProductInfo` 並清除其 `Height` 和 `Width` 屬性。 展開 DetailsView 的智慧標籤，然後從 [選擇資料來源] 下拉式清單中，選擇將 DetailsView 系結至名為 `RandomProductDataSource`的新 SqlDataSource 控制項。

[![將 DetailsView 系結至新的 SqlDataSource 控制項](master-pages-and-asp-net-ajax-vb/_static/image8.png)](master-pages-and-asp-net-ajax-vb/_static/image7.png)

**圖 03**：將 DetailsView 系結至新的 SqlDataSource 控制項（[按一下以查看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image9.png)）

設定 SqlDataSource 控制項，以透過 `NorthwindConnectionString` 連接到 Northwind 資料庫（我們在從內容頁面 [SKM2] 教學課程與主版頁面互動中建立）。 設定 select 語句時，請選擇指定自訂的 SQL 語句，然後輸入下列查詢：

[!code-sql[Main](master-pages-and-asp-net-ajax-vb/samples/sample3.sql)]

`SELECT` 子句中的 `TOP 1` 關鍵字只會傳回查詢所傳回的第一筆記錄。 `NEWID()` 函式會產生新的全域唯一識別碼值（GUID），而且可以在 `ORDER BY` 子句中用來以隨機順序傳回資料表的記錄。

[![將 SqlDataSource 設定為傳回單一、隨機選取的記錄](master-pages-and-asp-net-ajax-vb/_static/image11.png)](master-pages-and-asp-net-ajax-vb/_static/image10.png)

**圖 04**：設定 SqlDataSource 以傳回單一、隨機選取的記錄（[按一下以查看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image12.png)）

完成 wizard 之後，Visual Studio 會為上述查詢所傳回的兩個數據行建立 BoundField。 此時，您頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample4.aspx)]

[圖 5] 顯示透過瀏覽器觀看時的 `ShowRandomProduct.aspx` 頁面。 按一下瀏覽器的 [重新整理] 按鈕以重載頁面;您應該會看到新的隨機選取記錄的 `ProductName` 和 `UnitPrice` 值。

[![會顯示隨機產品的名稱和價格](master-pages-and-asp-net-ajax-vb/_static/image14.png)](master-pages-and-asp-net-ajax-vb/_static/image13.png)

**圖 05**：顯示隨機產品的名稱和價格（[按一下以觀看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image15.png)）

### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>每隔15秒自動顯示新產品

ASP.NET AJAX 架構包含一個 Timer 控制項，它會在指定的時間執行回傳;在回傳時，會引發計時器的 `Tick` 事件。 如果計時器控制項放在 UpdatePanel 中，它會觸發部分頁面回傳，在此期間，我們可以將資料重新系結到 DetailsView，以顯示新的隨機選取產品。

若要完成此動作，請從 [工具箱] 將 [計時器] 拖曳至 [UpdatePanel]。 將計時器的 `ID` 從 `Timer1` 變更為 `ProductTimer`，並將其 `Interval` 屬性從60000變更為15000。 `Interval` 屬性會指出回傳之間的毫秒數。將它設定為15000會使計時器每隔15秒觸發部分頁面回傳。 此時，計時器的宣告式標記看起來應該如下所示：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample5.aspx)]

為計時器的 `Tick` 事件建立事件處理常式。 在此事件處理常式中，我們需要藉由呼叫 DetailsView 的 `DataBind` 方法，將資料重新系結至 DetailsView。 這麼做會指示 DetailsView 從資料來源控制項重新抓取資料，這會選取並顯示新的隨機選取記錄（就像是在按一下瀏覽器的 [重新整理] 按鈕重載頁面時一樣）。

[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample6.vb)]

這樣就全部完成了！ 透過瀏覽器造訪頁面。 一開始會顯示隨機產品的資訊。 如果您耐心監看畫面，您會注意到，在15秒後，新產品的相關資訊就會取代現有的顯示。

為了進一步瞭解這裡的情況，讓我們將 Label 控制項新增至 UpdatePanel，以顯示上次更新顯示的時間。 在 UpdatePanel 中新增標籤 Web 控制項，將其 `ID` 設定為 `LastUpdateTime`，並清除其 `Text` 屬性。 接下來，建立 UpdatePanel `Load` 事件的事件處理常式，並在標籤中顯示目前的時間。 （UpdatePanel 的 `Load` 事件會在每次完整或部分頁面回傳時引發）。

[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample7.vb)]

完成此變更後，頁面會包含目前所顯示產品的載入時間。 [圖 6] 顯示第一次造訪時的頁面。 [圖 7] 顯示在計時器控制項具有 "核取" 後15秒的頁面，且 UpdatePanel 已重新整理以顯示新產品的相關資訊。

[在頁面載入時顯示隨機選取的產品 ![](master-pages-and-asp-net-ajax-vb/_static/image17.png)](master-pages-and-asp-net-ajax-vb/_static/image16.png)

**圖 06**：隨機選取的產品會在頁面載入時顯示（[按一下以觀看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image18.png)）

[每隔15秒 ![顯示新的隨機選取產品](master-pages-and-asp-net-ajax-vb/_static/image20.png)](master-pages-and-asp-net-ajax-vb/_static/image19.png)

**圖 07**：顯示新隨機選取產品的每15秒一次（[按一下以觀看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image21.png)）

## <a name="step-3-using-the-scriptmanagerproxy-control"></a>步驟3：使用 ScriptManagerProxy 控制項

除了包含 ASP.NET AJAX framework 用戶端程式庫所需的腳本之外，ScriptManager 也可以註冊自訂 JavaScript 檔案、已啟用腳本之 Web 服務的參考，以及自訂驗證、授權和設定檔服務。 這類自訂通常是特定頁面特有的。 不過，如果在主版頁面的 ScriptManager 中參考自訂腳本檔案、Web 服務參考或驗證、授權或設定檔服務，則它們會包含在網站的所有頁面中。

若要依頁面逐一新增 ScriptManager 相關的自訂專案，請使用 ScriptManagerProxy 控制項。 您可以將 ScriptManagerProxy 新增至內容頁面，然後從 ScriptManagerProxy 註冊自訂 JavaScript 檔案、Web 服務參考，或驗證、授權或設定檔服務;這會影響針對特定內容頁面註冊這些服務的效果。

> [!NOTE]
> ASP.NET 網頁只能有一個以上的 ScriptManager 控制項存在。 因此，如果 ScriptManager 控制項已在主版頁面中定義，您就無法將 ScriptManager 控制項加入至內容頁面。 ScriptManagerProxy 的唯一目的是要提供一種方法，讓開發人員在主版頁面中定義 ScriptManager，但仍然能夠依網頁逐一新增 ScriptManager 自訂專案。

為了查看作用中的 ScriptManagerProxy 控制項，讓我們擴大 `ShowRandomProduct.aspx` 中的 UpdatePanel，以包含使用用戶端腳本來暫停或繼續計時器控制項的按鈕。 計時器控制項有三種用戶端方法，可讓我們用來達成所需的功能：

- `_startTimer()`-啟動計時器控制項
- `_raiseTick()`-使計時器控制項「滴答」，因而回傳並引發其在伺服器上的滴答事件
- `_stopTimer()`-停止計時器控制項

讓我們建立一個 JavaScript 檔案，其中包含名為 `timerEnabled` 的變數和名為 `ToggleTimer`的函式。 `timerEnabled` 變數指出計時器控制項目前是否已啟用或已停用;預設值為 true。 `ToggleTimer` 函式接受兩個輸入參數： [暫停]/[繼續] 按鈕的參考，以及計時器控制項的用戶端 `id` 值。 此函式會切換 `timerEnabled`的值、取得計時器控制項的參考、啟動或停止計時器（視 `timerEnabled`的值而定），並將按鈕的顯示文字更新為「暫停」或「繼續」。 每當按一下 [暫停]/[繼續] 按鈕時，就會呼叫這個函式。

首先，在名為 `Scripts`的網站中建立新的資料夾。 接下來，將新檔案新增至名為的 [腳本] 資料夾，類型為 [JScript File] `TimerScript.js`。

[![將新的 JavaScript 檔案新增至 [腳本] 資料夾](master-pages-and-asp-net-ajax-vb/_static/image23.png)](master-pages-and-asp-net-ajax-vb/_static/image22.png)

**圖 08**：將新的 JavaScript 檔案新增至 [`Scripts`] 資料夾（[按一下以查看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image24.png)）

[![新的 JavaScript 檔案已新增至網站](master-pages-and-asp-net-ajax-vb/_static/image26.png)](master-pages-and-asp-net-ajax-vb/_static/image25.png)

**圖 09**：新的 JavaScript 檔案已新增至網站（[按一下以觀看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image27.png)）

接下來，將下列腳本新增至 `TimerScript.js` 檔案：

[!code-csharp[Main](master-pages-and-asp-net-ajax-vb/samples/sample8.cs)]

我們現在需要在 `ShowRandomProduct.aspx`中註冊此自訂 JavaScript 檔案。 返回 `ShowRandomProduct.aspx`，並將 ScriptManagerProxy 控制項新增至頁面;將其 `ID` 設定為 `MyManagerProxy`。 若要註冊自訂 JavaScript 檔案，請在設計工具中選取 [ScriptManagerProxy] 控制項，然後移至 [屬性視窗]。 其中一個屬性的標題為 [腳本]。 選取此屬性會顯示如 [圖 10] 所示的 [ScriptReference 集合編輯器]。 按一下 [新增] 按鈕以包含新的腳本參考，然後在 [路徑] 屬性中輸入腳本檔案的路徑： `~/Scripts/TimerScript.js`。

[![將腳本參考新增至 ScriptManagerProxy 控制項](master-pages-and-asp-net-ajax-vb/_static/image29.png)](master-pages-and-asp-net-ajax-vb/_static/image28.png)

**圖 10**：將腳本參考新增至 ScriptManagerProxy 控制項（[按一下以查看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image30.png)）

加入腳本參考之後，會更新 ScriptManagerProxy 控制項的宣告式標記，以包含具有單一 `ScriptReference` 專案的 `<Scripts>` 集合，如下列標記程式碼片段所示：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample9.aspx)]

`ScriptReference` 專案會指示 ScriptManagerProxy 在其轉譯的標記中包含 JavaScript 檔案的參考。 也就是說，藉由在 ScriptManagerProxy 中註冊自訂腳本，`ShowRandomProduct.aspx` 頁面的轉譯輸出現在會包含另一個 `<script src="url"></script>` 標記： `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`。

我們現在可以從 [`ShowRandomProduct.aspx`] 頁面中的用戶端腳本，呼叫 `TimerScript.js` 中定義的 `ToggleTimer` 函數。 在 UpdatePanel 中新增下列 HTML：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample10.aspx)]

這會顯示具有「暫停」文字的按鈕。 只要按一下，就會呼叫 JavaScript 函式 `ToggleTimer`，並傳入按鈕的參考和計時器控制項的 `id` 值（`ProductTimer`）。 請注意取得計時器控制項之 `id` 值的語法。 `<%=ProductTimer.ClientID%>` 會發出 `ProductTimer` Timer 控制項 `ClientID` 屬性的值。 在內容頁中的控制項識別碼命名 [SKM3] 教學課程中，我們討論了伺服器端 `ID` 值與產生的用戶端 `id` 值之間的差異，以及 `ClientID` 如何傳回用戶端 `id`。

[圖 11] 是第一次造訪瀏覽器時所顯示的頁面。 計時器目前正在執行，並每隔15秒更新顯示的產品資訊。 [圖 12] 顯示按一下 [暫停] 按鈕之後的畫面。 按一下 [暫停] 按鈕會停止計時器，並將按鈕的文字更新為 [繼續]。 使用者按一下 [繼續] 之後，產品資訊將會重新整理（並繼續每15秒重新整理一次）。

[![按一下 [暫停] 按鈕以停止計時器控制項](master-pages-and-asp-net-ajax-vb/_static/image32.png)](master-pages-and-asp-net-ajax-vb/_static/image31.png)

**圖 11**：按一下 [暫停] 按鈕以停止計時器控制項（[按一下以查看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image33.png)）

[![按一下 [繼續] 按鈕以重新開機計時器](master-pages-and-asp-net-ajax-vb/_static/image35.png)](master-pages-and-asp-net-ajax-vb/_static/image34.png)

**圖 12**：按一下 [繼續] 按鈕以重新開機計時器（[按一下以查看完整大小的影像](master-pages-and-asp-net-ajax-vb/_static/image36.png)）

## <a name="summary"></a>總結

使用 ASP.NET AJAX 架構建立啟用 AJAX 的 web 應用程式時，每個具備 AJAX 功能的網頁都必須包含 ScriptManager 控制項。 為了加速此程式，我們可以將 ScriptManager 新增至主版頁面，而不必記得將 ScriptManager 新增至每個內容頁面。 步驟1顯示如何將 ScriptManager 新增至主版頁面，而步驟2探討如何在內容頁面中執行 AJAX 功能。

如果您需要新增自訂腳本、對已啟用腳本之 Web 服務的參考，或是自訂的驗證、授權或對特定內容頁面的設定檔服務，請將 ScriptManagerProxy 控制項新增至 [內容] 頁面，然後設定自訂。 步驟3已檢查如何使用 ScriptManagerProxy 在特定內容頁面中註冊自訂 JavaScript 檔案。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET AJAX 架構](../../../../ajax/index.md)
- [ASP.NET AJAX 教學課程](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX 影片](../../../videos/aspnet-ajax/index.md)
- [使用 Microsoft ASP.NET AJAX 建立互動式使用者介面](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [使用 NEWID 來隨機排序記錄](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [使用計時器控制項](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](interacting-with-the-content-page-from-the-master-page-vb.md)
> [下一頁](specifying-the-master-page-programmatically-vb.md)
