---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
title: 主版頁面和網站導覽C#（） |Microsoft Docs
author: rick-anderson
description: 方便使用的網站有一項常見的特性，就是他們擁有一致、全網站的頁面配置和流覽配置。 本教學課程探討 y 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 5aee8202-a4e3-4aa9-8a95-cd5d156cea4c
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
msc.type: authoredcontent
ms.openlocfilehash: e1ddd43524a61ff2e012171eba1a8dc8efbf8f1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587712"
---
# <a name="master-pages-and-site-navigation-c"></a>主版頁面與網站導覽 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_3_CS.exe)或[下載 PDF](master-pages-and-site-navigation-cs/_static/datatutorial03cs1.pdf)

> 方便使用的網站有一項常見的特性，就是他們擁有一致、全網站的頁面配置和流覽配置。 本教學課程探討如何在可輕鬆更新的所有頁面上建立一致的外觀與風格。

## <a name="introduction"></a>簡介

方便使用的網站有一項常見的特性，就是他們擁有一致、全網站的頁面配置和流覽配置。 ASP.NET 2.0 引進兩項新功能，可大幅簡化整個網站的頁面配置和流覽配置：主版頁面和網站流覽。 主版頁面可讓開發人員使用指定的可編輯區域來建立全網站範本。 此範本可以套用至網站中的 ASP.NET 網頁。 這類 ASP.NET 網頁只需要提供主版頁面指定之可編輯區域的內容，主版頁面中的所有其他標記在所有使用主版頁面的 ASP.NET 網頁上都相同。 此模型可讓開發人員定義和集中化全網站頁面配置，讓您更輕鬆地在可輕鬆更新的所有頁面上建立一致的外觀與風格。

[網站導覽系統](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)提供一種機制，可讓網頁開發人員定義網站地圖，並為該網站地圖建立 API 以程式設計方式查詢。 新的流覽 Web 控制項功能表、TreeView 和 SiteMapPath 可讓您輕鬆地在一般導覽使用者介面專案中呈現網站地圖的全部或部分。 我們將使用預設的網站流覽提供者，這表示我們的網站地圖將會定義在 XML 格式的檔案中。

為了說明這些概念，並讓我們的教學課程網站更容易使用，讓我們花這堂課來定義全網站的頁面配置、執行網站地圖，以及新增導覽 UI。 在本教學課程結束時，我們將會有一份精美的網站設計，可供您建立教學課程網頁。

[![本教學課程的最終結果](master-pages-and-site-navigation-cs/_static/image2.png)](master-pages-and-site-navigation-cs/_static/image1.png)

**圖 1**：本教學課程的最終結果（[按一下以觀看完整大小的影像](master-pages-and-site-navigation-cs/_static/image3.png)）

## <a name="step-1-creating-the-master-page"></a>步驟1：建立主版頁面

第一個步驟是建立網站的主版頁面。 現在，我們的網站只包含具類型的資料集（`Northwind.xsd`、`App_Code` 資料夾中）、BLL 類別（`ProductsBLL.cs`、`CategoriesBLL.cs`等等、全部在 `App_Code` 資料夾中）、設定檔（`NORTHWND.MDF`），以及 CSS 樣式表單檔案（`App_Data`）。 我從前兩個教學課程中，清除了使用 DAL 和 BLL 示範的頁面和檔案，因為我們將在未來的教學課程中更詳細地 reexamining 這些範例。

![專案中的檔案](master-pages-and-site-navigation-cs/_static/image4.png)

**圖 2**：專案中的檔案

若要建立主版頁面，請在 方案總管中的專案名稱上按一下滑鼠右鍵，然後選擇 加入新專案。 然後從範本清單中選取主版頁面類型，並將其命名為 `Site.master`。

[![將新的主版頁面新增至網站](master-pages-and-site-navigation-cs/_static/image6.png)](master-pages-and-site-navigation-cs/_static/image5.png)

**圖 3**：將新的主版頁面新增至網站（[按一下以觀看完整大小的影像](master-pages-and-site-navigation-cs/_static/image7.png)）

在主版頁面中定義整個網站的頁面配置。 您可以使用設計檢視並新增您需要的任何版面配置或 Web 控制項，也可以手動在來源視圖中新增標記。 在我的主版頁面中，我使用[級聯樣式表](http://www.w3schools.com/css/default.asp)，搭配外部檔案 `Style.css`中定義的 CSS 設定來定位和樣式。 雖然您無法從下面所示的標記中得知，但 CSS 規則的定義是讓導覽 `<div>`的內容絕對位置，使其顯示在左邊，且固定寬度為200圖元。

網站. master

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample1.aspx)]

主版頁面會定義靜態頁面配置，以及可由使用主版頁面的 ASP.NET 網頁編輯的區域。 這些可編輯的區域是由 ContentPlaceHolder 控制項所表示，您可以在內容 `<div>`中看到這些內容。 我們的主版頁面具有單一 ContentPlaceHolder （`MainContent`），但主版頁面可能會有多個 ContentPlaceHolders。

在上方輸入標記之後，切換到設計檢視會顯示主版頁面的版面配置。 任何使用此主版頁面的 ASP.NET 網頁都將具有此統一版面配置，而且能夠指定 `MainContent` 區域的標記。

[![主版頁面（透過設計檢視查看時）](master-pages-and-site-navigation-cs/_static/image9.png)](master-pages-and-site-navigation-cs/_static/image8.png)

**圖 4**：透過設計檢視查看主版頁面時（[按一下以觀看完整大小的影像](master-pages-and-site-navigation-cs/_static/image10.png)）

## <a name="step-2-adding-a-homepage-to-the-website"></a>步驟2：將首頁新增至網站

定義主版頁面之後，我們就可以開始新增網站的 ASP.NET 網頁。 讓我們從新增 `Default.aspx`（我們的網站首頁）開始。 以滑鼠右鍵按一下 方案總管中的專案名稱，然後選擇 加入新專案。 從 [範本] 清單中挑選 [Web 表單] 選項，並將檔案命名為 `Default.aspx`。 此外，請核取 [選取主版頁面] 核取方塊。

[![新增 Web 表單，請勾選 [選取主版頁面] 核取方塊](master-pages-and-site-navigation-cs/_static/image12.png)](master-pages-and-site-navigation-cs/_static/image11.png)

**圖 5**：加入新的 Web 表單，核取 [選取主版頁面] 核取方塊（[按一下以查看完整大小的影像](master-pages-and-site-navigation-cs/_static/image13.png)）

按一下 [確定] 按鈕之後，我們會要求您選擇這個新的 ASP.NET 網頁應使用的主版頁面。 雖然您的專案中可以有多個主版頁面，但我們只有一個。

[![選擇此 ASP.NET 網頁應使用的主版頁面](master-pages-and-site-navigation-cs/_static/image15.png)](master-pages-and-site-navigation-cs/_static/image14.png)

**圖 6**：選擇此 ASP.NET 網頁應使用的主版頁面（[按一下以查看完整大小的影像](master-pages-and-site-navigation-cs/_static/image16.png)）

選取主版頁面之後，新的 ASP.NET 網頁會包含下列標記：

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample2.aspx)]

在 `@Page` 指示詞中，會參考使用的主版頁面檔案（`MasterPageFile="~/Site.master"`），而 ASP.NET 網頁的標記包含主版頁面中定義的每個 ContentPlaceHolder 控制項的內容控制項，而且控制項的 `ContentPlaceHolderID` 會將內容控制項對應至特定 ContentPlaceHolder。 內容控制項是您放置要在對應的 ContentPlaceHolder 中顯示之標記的位置。 將 [`@Page`] 指示詞的 [`Title`] 屬性設定為 [首頁]，並將一些歡迎內容新增至內容控制項：

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample3.aspx)]

`@Page` 指示詞中的 `Title` 屬性可讓我們從 ASP.NET 網頁設定頁面的標題，即使在主版頁面中定義了 `<title>` 元素也一樣。 我們也可以使用 `Page.Title`，以程式設計方式設定標題。 另請注意，主版頁面的樣式表單參考（例如 `Style.css`）會自動更新，使其可在任何 ASP.NET 網頁中使用，不論 ASP.NET 網頁相對於主版頁面的目錄為何。

切換到設計檢視我們可以看到頁面在瀏覽器中的外觀。 請注意，在 [ASP.NET] 頁面的設計檢視中，只有內容可編輯區域可供編輯，主版頁面中定義的非 ContentPlaceHolder 標記會變成灰色。

[![[ASP.NET] 頁面的設計檢視會顯示可編輯和不可編輯的區域](master-pages-and-site-navigation-cs/_static/image18.png)](master-pages-and-site-navigation-cs/_static/image17.png)

**圖 7**： [ASP.NET] 頁面的設計檢視會同時顯示可編輯和不可編輯的區域（[按一下以查看完整大小的影像](master-pages-and-site-navigation-cs/_static/image19.png)）

當瀏覽器造訪 [`Default.aspx`] 頁面時，ASP.NET 引擎會自動合併頁面的主版頁面內容和 ASP。NET 的內容，並將合併的內容轉譯成最後的 HTML，然後傳送到要求的瀏覽器。 當主版頁面的內容更新時，所有使用此主版頁面的 ASP.NET 網頁都會在下一次要求時，以新的主版頁面內容 remerged 其內容。 簡單來說，主版頁面模型允許定義單一頁面配置範本（主版頁面），其變更會立即反映在整個網站上。

## <a name="adding-additional-aspnet-pages-to-the-website"></a>將其他 ASP.NET 網頁新增至網站

讓我們花點時間將額外的 ASP.NET 網頁存根新增至網站，最終將會保存各種報告示範。 總共會有35個以上的示範，而不是建立所有的 stub 頁面，而只是建立前幾頁。 由於也有許多示範的類別，因此若要更有效地管理示範，請新增類別目錄的資料夾。 現在新增下列三個資料夾：

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

最後，新增檔案，如 [圖 8] 中的方案總管所示。 新增每個檔案時，請記得勾選 [選取主版頁面] 核取方塊。

![新增下列檔案](master-pages-and-site-navigation-cs/_static/image20.png)

**圖 8**：新增下列檔案

## <a name="step-2-creating-a-site-map"></a>步驟2：建立網站地圖

管理由多個頁面組成的網站，其中一項挑戰是提供直接的方式讓訪客流覽網站。 首先，必須定義網站的導覽結構。 接下來，此結構必須轉譯成可流覽的使用者介面元素，例如功能表或階層連結。 最後，這整個程式必須在新頁面新增至網站，且現有的網頁已移除時進行維護和更新。 在 ASP.NET 2.0 之前，開發人員會自行建立網站的導覽結構、維護它，並將它轉譯成可流覽的使用者介面專案。 不過，使用 ASP.NET 2.0 時，開發人員可以利用非常彈性的內建網站流覽系統。

ASP.NET 2.0 site 導覽系統提供一種方法，讓開發人員定義網站地圖，然後透過程式設計的 API 來存取此資訊。 ASP.NET 隨附的網站地圖提供者，需要將網站地圖資料儲存在以特定方式格式化的 XML 檔案中。 但是，由於網站導覽系統是以[提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)為基礎，因此可以擴充，以支援序列化網站地圖資訊的替代方式。 Jeff Prosise 的文章，[您所等待的 SQL 網站地圖提供者](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)示範如何建立網站地圖提供者，將網站地圖儲存在 SQL Server 資料庫中;另一個選項是建立以[檔案系統結構為基礎的網站地圖提供者](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)。

不過，在本教學課程中，我們將使用隨附于 ASP.NET 2.0 的預設網站地圖提供者。 若要建立網站地圖，只要以滑鼠右鍵按一下 方案總管中的專案名稱，選擇 加入新專案，然後選擇 網站地圖 選項即可。 將名稱保留 `Web.sitemap`，然後按一下 [新增] 按鈕。

[![將網站地圖新增至您的專案](master-pages-and-site-navigation-cs/_static/image22.png)](master-pages-and-site-navigation-cs/_static/image21.png)

**圖 9**：將網站地圖新增至您的專案（[按一下以觀看完整大小的影像](master-pages-and-site-navigation-cs/_static/image23.png)）

網站地圖檔案是一個 XML 檔案。 請注意，Visual Studio 會為網站地圖結構提供 IntelliSense。 網站地圖檔案必須有 `<siteMap>` 節點做為其根節點，且必須精確包含一個 `<siteMapNode>` 子項目。 第一個 `<siteMapNode>` 元素可以包含任意數目的子代 `<siteMapNode>` 元素。

定義要模擬檔案系統結構的網站地圖。 也就是，針對這些資料夾中的每個 ASP.NET 網頁，新增三個資料夾和子 `<siteMapNode>` 元素的 `<siteMapNode>` 元素，如下所示：

Web. 網站地圖

[!code-xml[Main](master-pages-and-site-navigation-cs/samples/sample4.xml)]

網站地圖會定義網站的導覽結構，這是描述網站各區段的階層。 `Web.sitemap` 中的每個 `<siteMapNode>` 元素都代表網站導覽結構中的一個區段。

[![網站地圖代表階層式導覽結構](master-pages-and-site-navigation-cs/_static/image25.png)](master-pages-and-site-navigation-cs/_static/image24.png)

**圖 10**：網站地圖代表階層式導覽結構（[按一下以觀看完整大小的影像](master-pages-and-site-navigation-cs/_static/image26.png)）

ASP.NET 會透過 .NET Framework 的[網站地圖類別](https://msdn.microsoft.com/library/system.web.sitemap.aspx)公開網站地圖的結構。 這個類別具有 `CurrentNode` 屬性，它會傳回使用者目前造訪之區段的相關資訊;`RootNode` 屬性會傳回網站地圖（Home）在我們網站地圖中的根。 `CurrentNode` 和 `RootNode` 屬性都會傳回[SiteMapNode](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)實例，其具有如 `ParentNode`、`ChildNodes`、`NextSibling`、`PreviousSibling`等等的屬性，可讓網站地圖階層進行引導。

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>步驟3：顯示以網站地圖為基礎的功能表

存取 ASP.NET 2.0 中的資料可透過程式設計方式完成，例如在 ASP.NET 1.x 中，或以宣告方式在新的[資料來源控制項](https://msdn.microsoft.com/library/ms227679.aspx)中執行。 有數個內建的資料來源控制項，例如 SqlDataSource 控制項，用於存取關係資料庫資料、ObjectDataSource 控制項、用於存取類別的資料，以及其他專案。 您甚至可以建立自己的[自訂資料來源控制項](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp)。

資料來源控制項會當做 ASP.NET 網頁與基礎資料之間的 proxy。 為了顯示資料來源控制項的抓取資料，我們通常會將另一個 Web 控制項加入至頁面，並將它系結至資料來源控制項。 若要將 Web 控制項系結至資料來源控制項，只要將 Web 控制項的 `DataSourceID` 屬性設定為數據源控制項的 `ID` 屬性值即可。

為了協助處理網站地圖的資料，ASP.NET 包含 SiteMapDataSource 控制項，可讓我們將 Web 控制項系結到我們網站的網站地圖。 兩個 Web 控制項： TreeView 和功能表通常用來提供導覽使用者介面。 若要將網站地圖資料系結到這兩個控制項的其中一個，只要將 SiteMapDataSource 連同 TreeView 或 Menu 控制項（其 `DataSourceID` 屬性會據以設定）加入頁面。 例如，我們可以使用下列標記，將功能表控制項加入至主版頁面：

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample5.aspx)]

若要對發出的 HTML 進行更精細的控制，我們可以將 SiteMapDataSource 控制項系結至中繼器控制項，如下所示：

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample6.aspx)]

SiteMapDataSource 控制項會一次傳回一個層級的網站地圖階層，從根網站地圖節點（Home，在我們的網站地圖中）開始，然後是下一個層級（基礎報表、篩選報表和自訂格式）等等。 將 SiteMapDataSource 系結至中繼器時，它會列舉傳回的第一個層級，並將該第一個層級中每個 `SiteMapNode` 實例的 `ItemTemplate` 具現化。 若要存取 `SiteMapNode`的特定屬性，我們可以使用 `Eval(propertyName)`，這就是我們取得每個 `SiteMapNode`的 `Url` 和超連結控制項 `Title` 屬性的方式。

上述的中繼器範例會轉譯下列標記：

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample7.html)]

這些網站地圖節點（基礎報表、篩選報表和自訂格式）組成所轉譯的*第二*層網站對應，而不是第一個階層。 這是因為 SiteMapDataSource 的 `ShowStartingNode` 屬性設定為 False，導致 SiteMapDataSource 略過根網站對應節點，而改為從網站地圖階層中的第二個層級開始。

若要顯示基本報告、篩選報表和自訂格式設定 `SiteMapNode` 的子系，我們可以將另一個中繼器新增至初始中繼器的 `ItemTemplate`。 第二個中繼器會系結至 `SiteMapNode` 實例的 `ChildNodes` 屬性，如下所示：

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample8.aspx)]

這兩個中繼器會產生下列標記（為了簡潔起見，已移除某些標記）：

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample9.html)]

使用從[Rachel Andrew](http://www.rachelandrew.co.uk/)的書籍中選擇的 Css 樣式[Anthology：101基本秘訣、訣竅、&amp; 的駭客](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance)、`<ul>` 和 `<li>` 元素的樣式，讓標記產生下列視覺效果輸出：

![由兩個中繼器和一些 CSS 組成的功能表](master-pages-and-site-navigation-cs/_static/image27.png)

**圖 11**：由兩個中繼器和一些 CSS 組成的功能表

此功能表位於主版頁面中，並系結至 `Web.sitemap`中定義的網站地圖，這表示網站對應的任何變更都會立即反映在所有使用 `Site.master` 主版頁面的頁面上。

## <a name="disabling-viewstate"></a>停用 ViewState

所有的 ASP.NET 控制項都可以選擇性地將其狀態保存到[view 狀態](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/)，這會在呈現的 HTML 中序列化為隱藏的表單欄位。 控制項會使用 View 狀態來記住其在回傳期間以程式設計方式變更的狀態，例如系結至資料 Web 控制項的資料。 雖然 view 狀態允許在回傳期間記住資訊，但它會增加必須傳送至用戶端的標記大小，而且如果未受到嚴密監視，可能會導致嚴重的頁面膨脹。 資料 Web 控制項特別是 GridView 特別糟，可將數十個額外 kb 的標記新增至頁面。 雖然寬頻或內部網路使用者的這類增加可能是可忽略的，但 view 狀態可能會在撥號使用者的來回行程中加上幾秒鐘。

若要查看 view 狀態的影響，請造訪瀏覽器中的頁面，然後查看網頁所傳送的來源（在 Internet Explorer 中，移至 [View] 功能表，然後選擇 [來源] 選項）。 您也可以開啟[頁面追蹤](https://msdn.microsoft.com/library/sfbfw58f.aspx)，以查看頁面上每個控制項所使用的檢視狀態配置。 檢視狀態資訊會在名為 `__VIEWSTATE`的隱藏表單欄位中序列化，此欄位位於開頭 `<form>` 標記之後的 `<div>` 元素中。 只有在使用 Web 表單時，才會保存 View 狀態;如果您的 ASP.NET 網頁未在其宣告式語法中包含 `<form runat="server">`，呈現的標記中將不會有 `__VIEWSTATE` 隱藏的表單欄位。

主版頁面所產生的 [`__VIEWSTATE` 表單] 欄位會在頁面產生的標記中新增大約1800個位元組。 這項額外的膨脹主要是因重複項控制項的緣故，因為 SiteMapDataSource 控制項的內容會保存到 view 狀態。 雖然額外的1800位元組似乎不太可能會令人興奮，但當您使用具有許多欄位和記錄的 GridView 時，檢視狀態可以輕鬆地源源不絕10個以上的因素。

您可以在頁面或控制項層級停用檢視狀態，方法是將 [`EnableViewState`] 屬性設定為 [`false`]，藉此減少呈現的標記大小。 由於資料 Web 控制項的檢視狀態會將系結至資料 Web 控制項的資料保存在回傳中，因此，在停用資料 Web 控制項的檢視狀態時，必須在每個回傳上系結資料。 在 ASP.NET 1.x 版中，這項責任會落在網頁開發人員的肩膀上;不過，有了 ASP.NET 2.0，資料 Web 控制項就會在每次回傳時，視需要重新系結至其資料來源控制項。

若要減少頁面的檢視狀態，讓我們將重複項控制項的 `EnableViewState` 屬性設定為 [`false`]。 這可以透過設計工具中的屬性視窗來完成，或在原始檔視圖中以宣告方式執行。 進行這項變更之後，中繼器的宣告式標記看起來應該像這樣：

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample10.aspx)]

在這項變更之後，頁面的呈現檢視狀態大小已縮減為僅52個位元組，而在檢視狀態大小中，會節省97%！ 在這一系列的教學課程中，我們預設會停用資料 Web 控制項的檢視狀態，以縮減轉譯標記的大小。 在大部分的範例中，`EnableViewState` 屬性會設定為 `false` 並在不提及的情況下完成。 只有在必須啟用它的情況下，才會討論唯一的時間 view 狀態，才能讓資料 Web 控制項提供其預期的功能。

## <a name="step-4-adding-breadcrumb-navigation"></a>步驟4：新增階層連結導覽

若要完成主版頁面，讓我們將階層式導覽 UI 元素新增至每個頁面。 階層連結會快速顯示使用者在網站階層中的目前位置。 在 ASP.NET 2.0 中新增階層連結很容易，只要將 SiteMapPath 控制項新增至頁面即可。不需要任何程式碼。

針對我們的網站，將此控制項新增至標頭 `<div>`：

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample11.aspx)]

階層連結會顯示使用者在網站地圖階層中造訪的目前頁面，以及該網站地圖節點的「上階」，一直到根目錄（在我們的網站地圖中）為止。

![階層連結會顯示目前頁面及其上階的網站地圖階層架構](master-pages-and-site-navigation-cs/_static/image28.png)

**圖 12**：階層連結會顯示目前頁面及其在網站地圖階層架構中的祖系

## <a name="step-5-adding-the-default-page-for-each-section"></a>步驟5：新增每個區段的預設頁面

我們網站中的教學課程會細分成不同的類別，包括基礎報表、篩選、自訂格式等等，以及每個類別的資料夾和對應的教學課程，做為該資料夾內的 ASP.NET 網頁。 此外，每個資料夾都包含一個 `Default.aspx` 頁面。 在此預設頁面中，讓我們顯示目前區段的所有教學課程。 也就是說，對於 `BasicReporting` 資料夾中的 `Default.aspx`，我們會有 `SimpleDisplay.aspx`、`DeclarativeParams.aspx`和 `ProgrammaticParams.aspx`的連結。 同樣地，我們也可以使用 `SiteMap` 類別和資料 Web 控制項，根據 `Web.sitemap`中定義的網站地圖來顯示這項資訊。

讓我們再次使用中繼器來顯示未排序的清單，但這次我們會顯示教學課程的標題和描述。 因為要完成這項工作的標記和程式碼必須針對每個 `Default.aspx` 頁面重複，所以我們可以在[使用者控制項](https://msdn.microsoft.com/library/y6wb1a0e.aspx)中封裝此 UI 邏輯。 在名為 `UserControls` 的網站中建立資料夾，並將新增至類型為 [`SectionLevelTutorialListing.ascx`的 Web 使用者控制項] 的新專案，然後新增下列標記：

[![將新的 Web 使用者控制項加入至 Usercontrol 資料夾](master-pages-and-site-navigation-cs/_static/image30.png)](master-pages-and-site-navigation-cs/_static/image29.png)

**圖 13**：在 [`UserControls`] 資料夾中加入新的 Web 使用者控制項（[按一下以觀看完整大小的影像](master-pages-and-site-navigation-cs/_static/image31.png)）

SectionLevelTutorialListing .ascx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.cs

[!code-csharp[Main](master-pages-and-site-navigation-cs/samples/sample13.cs)]

在先前的中繼器範例中，我們以宣告方式將 `SiteMap` 資料系結至中繼器;不過，`SectionLevelTutorialListing` 的使用者控制項會以程式設計方式執行。 在 `Page_Load` 事件處理常式中，會進行檢查以確保此頁面的 URL 會對應至網站地圖中的節點。 如果在沒有對應 `<siteMapNode>` 專案的頁面中使用此使用者控制項，`SiteMap.CurrentNode` 會傳回 `null` 而且不會有任何資料系結至中繼器。 假設我們有 `CurrentNode`，我們會將其 `ChildNodes` 集合系結至中繼器。 由於我們的網站地圖已設定好讓每個區段中的 [`Default.aspx`] 頁面是該區段中所有教學課程的父節點，因此此程式碼會顯示所有區段教學課程的連結和描述，如以下螢幕擷取畫面所示。

建立此中繼器之後，請開啟每個資料夾中的 [`Default.aspx`] 頁面，移至 [設計檢視]，然後直接將使用者控制項從 [方案總管] 拖曳至您想要顯示教學課程清單的設計介面上。

[![使用者控制項已加入至 default.aspx](master-pages-and-site-navigation-cs/_static/image33.png)](master-pages-and-site-navigation-cs/_static/image32.png)

**圖 14**：使用者控制項已加入至 `Default.aspx` （[按一下以查看完整大小的影像](master-pages-and-site-navigation-cs/_static/image34.png)）

[![列出基本的報告教學課程](master-pages-and-site-navigation-cs/_static/image36.png)](master-pages-and-site-navigation-cs/_static/image35.png)

**圖 15**：列出基本的報告教學課程（[按一下以觀看完整大小的影像](master-pages-and-site-navigation-cs/_static/image37.png)）

## <a name="summary"></a>總結

定義網站地圖並完成主版頁面之後，我們的資料相關教學課程現在具有一致的頁面配置和流覽配置。 無論我們新增至網站的頁數有多少，更新全網站頁面配置或網站導覽資訊是快速且簡單的程式，因為這項資訊是集中式的。 具體而言，頁面配置資訊是在主版頁面中定義的，`Site.master` 和 `Web.sitemap`中的網站地圖。 我們不需要撰寫*任何*程式碼來達到這個全網站的頁面配置和流覽機制，而且我們會在 Visual Studio 中保留完整的 WYSIWYG 設計工具支援。

完成資料存取層和商務邏輯層，並定義一致的頁面配置和網站導覽之後，我們就可以開始探索常見的報表模式。 在[接下來](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)的三個教學課程中，我們將探討基本的報告工作，顯示從 GridView、DetailsView 和 FormView 控制項中的 BLL 取得的資料。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 主版頁面總覽](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [ASP.NET 2.0 中的主版頁面](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2.0 設計範本](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET 網站流覽總覽](https://msdn.microsoft.com/library/e468hxky.aspx)
- [檢查 ASP.NET 2.0 的網站導覽](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2.0 網站導覽功能](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [瞭解 ASP.NET 檢視狀態](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [如何：啟用 ASP.NET 網頁的追蹤](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET 使用者控制項](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Liz Shulok、Dennis Patterson 和 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](creating-a-business-logic-layer-cs.md)
> [下一頁](creating-a-data-access-layer-vb.md)
