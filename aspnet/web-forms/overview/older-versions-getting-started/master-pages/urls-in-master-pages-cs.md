---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
title: 主版頁面中的C#url （） |Microsoft Docs
author: rick-anderson
description: 解決主版頁面中的 Url 如何中斷，因為主版分頁檔案位於與內容頁面不同的相對目錄中。 查看重定基底 。
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 48b58a18-5ea4-468c-b326-f35331b3e1e9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 2551a5361256234883bb37e46e794037284445a4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640918"
---
# <a name="urls-in-master-pages-c"></a>主版頁面中的 URL (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip)或[下載 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)

> 解決主版頁面中的 Url 如何中斷，因為主版分頁檔案位於與內容頁面不同的相對目錄中。 在宣告式語法中透過 ~ 重定基底 Url，並以程式設計方式使用 ResolveUrl 和 ResolveClientUrl。 （另請參閱

## <a name="introduction"></a>簡介

在目前為止我們看到的所有範例中，主要和內容頁面都位於相同的資料夾（網站的根資料夾）。 但是主要和內容頁面都必須位於相同的資料夾中，因此沒有理由。 您當然可以在子資料夾中建立內容頁。 同樣地，您可以建立一個 `~/MasterPages/` 資料夾來放置網站的主版頁面。

將主要畫面和內容頁面放在不同資料夾的其中一個可能的問題牽涉到的 Url 中斷。 如果主版頁面包含超連結、影像或其他元素中的相對 Url，則該連結將對位於不同資料夾中的內容頁面無效。 在本教學課程中，我們會檢查這個問題的來源和因應措施。

## <a name="the-problem-with-relative-urls"></a>相對 Url 的問題

如果 web 網頁上的 URL 是相對於網頁在網站的資料夾結構中的位置，則會將其視為*相對 url* 。 不是以前置正斜線（`/`）或通訊協定（例如 `http://`）開頭的任何 URL 是相對的，因為瀏覽器會根據包含 URL 之網頁的位置來解析它。

例如，我們的網站有一個具有單一影像檔案的 `~/Images/` 資料夾，`PoweredByASPNET.gif`。 主版分頁檔 `Site.master` 在 `footerContent` 區域中具有具有下列標記的 `<img>` 元素：

[!code-html[Main](urls-in-master-pages-cs/samples/sample1.html)]

`<img>` 元素中的 `src` 屬性值是相對 URL，因為它的開頭不是 `/` 或 `http://`。 簡單地說，`src` 屬性值會告訴瀏覽器在 `Images` 子資料夾中，尋找名為 `PoweredByASPNET.gif`的檔案。

造訪內容頁面時，會將上述標記直接傳送至瀏覽器。 請花點時間造訪 `About.aspx` 並觀看傳送至瀏覽器的 HTML 來源。 您會發現主版頁面中的標記完全相同，已傳送至瀏覽器。

[!code-html[Main](urls-in-master-pages-cs/samples/sample2.html)]

如果 [內容] 頁面位於根資料夾（如 `About.aspx`），所有專案都會如預期般運作，因為有一個與根資料夾相關的 `Images` 子資料夾。 不過，如果內容頁與主版頁面位於不同的資料夾中，就會發生問題。 為了說明這一點，請建立名為 `Admin`的子資料夾。 接下來，將名為 `Default.aspx` 的內容頁新增至 [`Admin`] 資料夾，並務必將新的頁面系結至 `Site.master` 主版頁面。

> [!NOTE]
> 在[*主版頁面教學課程中指定標題、中繼標記和其他 HTML 標頭*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)時，我們建立了名為 `BasePage` 的自訂基底頁面類別，它會自動設定內容頁的標題（如果未明確指派）。 別忘了新建立頁面的程式碼後置類別衍生自 `BasePage`，讓它可以利用這種功能。

建立此內容頁面之後，您的方案總管看起來應該像 [圖 1]。

![已將新的資料夾和 ASP.NET 網頁新增至專案](urls-in-master-pages-cs/_static/image1.png)

**圖 01**：已將新的資料夾和 ASP.NET 網頁新增至專案

接下來，更新 `Web.sitemap` 檔案，以包含這堂課的新 `<siteMapNode>` 專案。 下列 XML 會顯示完整的 `Web.sitemap` 標記，這現在包含了第三個 `<siteMapNode>` 元素的加入。

[!code-xml[Main](urls-in-master-pages-cs/samples/sample3.xml)]

新建立的 `Default.aspx` 頁面應該有四個內容控制項對應到 `Site.master`中的四個 ContentPlaceHolders。 將一些文字新增至參考 `MainContent` ContentPlaceHolder 的內容控制項，然後透過瀏覽器造訪頁面。 如 [圖 2] 所示，瀏覽器找不到 `PoweredByASPNET.gif` 的影像檔案。 這是怎麼回事？

[`~/Admin/Default.aspx` 內容] 頁面會與 [`About.aspx`] 頁面一樣，傳送 `footerContent` 區域的相同 HTML：

[!code-html[Main](urls-in-master-pages-cs/samples/sample4.html)]

因為 `<img>` 元素的 `src` 屬性是相對 URL，所以瀏覽器會嘗試尋找相對於網頁資料夾位置的 `Images` 資料夾。 換句話說，瀏覽器會尋找 `Admin/Images/PoweredByASPNET.gif`的影像檔案。

[![找不到 PoweredByASPNET .gif 影像檔案](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)

**圖 02**：找不到 `PoweredByASPNET.gif` 影像檔案（[按一下以觀看完整大小的影像](urls-in-master-pages-cs/_static/image4.png)）

### <a name="replacing-relative-urls-with-absolute-urls"></a>以絕對 Url 取代相對 Url

相對 URL 的相反之處是*絕對 url*，也就是以正斜線（`/`）或通訊協定（例如 `http://`）開頭的 url。 由於絕對 URL 會從已知的固定點指定資源的位置，因此無論網頁在網站的資料夾結構中的位置為何，相同的絕對 URL 在任何網頁中都是有效的。

為了補救 [圖 2] 所示的中斷影像，我們需要更新 `<img>` 元素的 `src` 屬性，使其使用絕對 URL，而不是相對路徑。 若要判斷正確的絕對 URL，請造訪您網站中的其中一個網頁，並檢查網址列。 如 [圖 2] 中的網址列所示，web 應用程式的完整路徑是 `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`。 因此，我們可以將 `<img>` 元素的 `src` 屬性更新為下列兩個絕對 Url 的其中一個：

- `/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`

請花點時間使用上述其中一個表單，將 `<img>` 專案的 `src` 屬性更新為絕對 URL，然後透過瀏覽器造訪 [`~/Admin/Default.aspx`] 頁面。 此時，瀏覽器會正確地尋找並顯示 `PoweredByASPNET.gif` 影像檔案（請參閱 [圖 3]）。

[![現在會顯示 PoweredByASPNET 的 gif 影像](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)

**圖 03**：現在會顯示 `PoweredByASPNET.gif` 影像（[按一下以觀看完整大小的影像](urls-in-master-pages-cs/_static/image7.png)）

雖然絕對 URL 中的硬編碼運作正常，但它會將您的 HTML 緊密結合到網站的伺服器和資料夾位置，這可能會有所變更。 使用表單 `http://localhost:3908/...` 的絕對 URL 會脆弱，因為每次啟動 Visual Studio 內建 ASP.NET 開發 Web 服務器時，會自動選取前面 `localhost` 的埠號碼。 同樣地，只有在本機測試時，`http://localhost` 部分才有效。 將程式碼部署至實際執行伺服器後，URL 基底會變更為其他專案，例如 `http://www.yourserver.com`。 表單 `/ASPNET_MasterPages_Tutorial_04_CS/...` 的絕對 URL 也會受到相同的肯定脆弱度，因為開發和實際伺服器之間的應用程式路徑有時會有所不同。

好消息是，ASP.NET 提供了一個方法，可在執行時間產生有效的相對 URL。

## <a name="usingandresolveclienturl"></a>使用`~`和`ResolveClientUrl`

ASP.NET 可讓網頁開發人員使用波狀符號（`~`）來指示 web 應用程式的根目錄，而不是硬程式碼為絕對 URL。 例如，稍早在本教學課程中，我使用文字中的標記法 `~/Admin/Default.aspx` 來參考 `Admin` 資料夾中的 `Default.aspx` 頁面。 `~` 表示 `Admin` 資料夾是 web 應用程式根目錄的子資料夾。

`Control` 類別的[`ResolveClientUrl` 方法](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx)會取得 URL，並將它修改為適合控制項所在網頁的相對 url。 例如，從 `About.aspx` 呼叫 `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` 會傳回 `Images/PoweredByASPNET.gif`。 不過，從 `~/Admin/Default.aspx`呼叫它，會傳回 `./Images/PoweredByASPNET.gif`。

> [!NOTE]
> 因為所有的 ASP.NET 伺服器控制項都是衍生自 `Control` 類別，所以所有伺服器控制項都有 `ResolveClientUrl` 方法的存取權。 即使 `Page` 類別衍生自 `Control` 類別，這表示您可以直接從 ASP.NET 網頁的程式碼後置類別使用此方法。

### <a name="usingin-the-declarative-markup"></a>在宣告式標記中使用`~`

數個 ASP.NET 的 Web 控制項包含 URL 相關屬性： HyperLink 控制項具有 `NavigateUrl` 屬性;影像控制項具有 `ImageUrl` 屬性;以此類推。 轉譯時，這些控制項會將其 URL 相關的屬性值傳遞至 `ResolveClientUrl`。 因此，如果這些屬性包含 `~` 來指出 web 應用程式的根目錄，則會將 URL 修改為有效的相對 URL。

請記住，只有 ASP.NET 伺服器控制項會在其 URL 相關屬性中轉換 `~`。 如果 `~` 出現在靜態 HTML 標籤中（例如 `<img src="~/Images/PoweredByASPNET.gif" />`），則 ASP.NET 引擎會將 `~` 連同其餘的 HTML 內容一起傳送到瀏覽器。 瀏覽器會假設 `~` 是 URL 的一部分。 例如，如果瀏覽器收到標記 `<img src="~/Images/PoweredByASPNET.gif" />` 則會假設有一個名為 `~` 的子資料夾，其中包含 `PoweredByASPNET.gif`的影像檔 `Images` 子資料夾。

若要修正 `Site.master`中的影像標記，請將現有的 `<img>` 元素取代為 ASP.NET 影像 Web 控制項。 將影像 Web 控制項的 `ID` 設定為 [`PoweredByImage`]、其 [`ImageUrl`] 屬性設為 [`~/Images/PoweredByASPNET.gif`]，並將其 [`AlternateText`] 屬性設定為 [由 ASP.NET 所提供技術支援]

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample5.aspx)]

對主版頁面進行這種變更之後，再次流覽 `~/Admin/Default.aspx` 頁面。 這次 `PoweredByASPNET.gif` 影像檔案會出現在頁面中（請參閱 [圖 3]）。 呈現影像 Web 控制項時，會使用 `ResolveClientUrl` 方法來解析其 `ImageUrl` 屬性值。 在 `~/Admin/Default.aspx` 會將 `ImageUrl` 轉換為適當的相對 URL，如下列 HTML 來原始程式碼段所示：

[!code-html[Main](urls-in-master-pages-cs/samples/sample6.html)]

> [!NOTE]
> 除了用於以 URL 為基礎的 Web 控制項屬性之外，也可以在呼叫 `Response.Redirect` 和 `Server.MapPath` 方法時使用 `~`。 此外，您可以視需要直接從 ASP.NET 或主版頁面的宣告式標記叫用 `ResolveClientUrl` 方法;請參閱[使用標記中的 `ResolveClientUrl`](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx) [Fritz 繪圖紙](https://www.pluralsight.com/blogs/fritz/)的 blog 專案。

## <a name="fixing-the-master-pages-remaining-relative-urls"></a>修正主版頁面的剩餘相對 Url

除了我們剛剛修正的 `footerContent` 中的 `<img>` 元素之外，主版頁面還包含一個需要我們注意的相對 URL。 `topContent` 區域包含連結「主版頁面教學課程」，其指向 `Default.aspx`。

[!code-html[Main](urls-in-master-pages-cs/samples/sample7.html)]

因為此 URL 是相對的，所以它會將使用者傳送至所造訪內容頁面之資料夾中的 [`Default.aspx`] 頁面。 若要讓這個連結一律指向根資料夾中的 `Default.aspx`，我們必須將 `<a>` 元素取代為 HyperLink Web 控制項，讓我們可以使用 `~` 標記法。

移除 `<a>` 的元素標記，並在其位置新增超連結控制項。 將超連結的 `ID` 設定為 `lnkHome`、其 `NavigateUrl` 屬性設為 `~/Default.aspx`，並將其 `Text` 屬性設定為 主版頁面

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample8.aspx)]

就這麼容易！ 此時，主版頁面中的所有 Url 都會根據內容頁轉譯，而不論主版頁面和內容頁面位於哪個資料夾，都是正確的。

### <a name="automatic-url-resolution-in-theheadsection"></a>`<head>`區段中的自動 URL 解析

在[*使用主版頁面建立全網站的版面*](creating-a-site-wide-layout-using-master-pages-cs.md)配置教學課程中，我們將 `<link>` 新增至 `<head>` 區域中的 `Styles.css` 檔案：

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample9.aspx)]

雖然 `<link>` 元素的 `href` 屬性是相對的，但它會在執行時間自動轉換為適當的路徑。 如同我們在[*主版頁面中指定標題、中繼標記和其他 HTML 標頭*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)中所討論，`<head>` 的區域實際上是伺服器端控制項，可讓它在呈現內部控制項時修改其內容。

若要確認這一點，請重新流覽 [`~/Admin/Default.aspx`] 頁面，並查看傳送至瀏覽器的 HTML 來源。 如下列程式碼片段所示，`<link>` 元素的 `href` 屬性已自動修改為適當的相對 URL，`./Styles.css`。

[!code-html[Main](urls-in-master-pages-cs/samples/sample10.html)]

## <a name="summary"></a>總結

主版頁面通常包含連結、影像和其他必須透過 URL 指定的外部資源。 因為主版頁面和內容頁面可能不存在於相同的資料夾中，所以請務必從使用相對 Url abstain。 雖然可以使用硬式編碼的絕對 Url，但這樣做會緊密結合 web 應用程式的絕對 URL。 如果絕對的 URL 變更-通常是在移動或部署 web 應用程式時，您必須記得返回並更新絕對 Url。

理想的方法是使用波狀符號（`~`）來表示應用程式根目錄。 ASP.NET 包含 URL 相關屬性的 Web 控制項，會在執行時間將 `~` 對應至應用程式根目錄。 就內部而言，Web 控制項會使用 `Control` 類別的 `ResolveClientUrl` 方法來產生有效的相對 URL。 這個方法是公用的，而且可從每個伺服器控制項（包括 `Page` 類別）取得，因此您可以視需要從程式碼後置類別以程式設計方式使用它。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 中的主版頁面](http://www.odetocode.com/Articles/419.aspx)
- [主版頁面中的 URL 重定基底](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [在標記中使用 `ResolveClientUrl`](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
> [下一頁](control-id-naming-in-content-pages-cs.md)
