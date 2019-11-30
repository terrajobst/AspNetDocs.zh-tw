---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
title: 在主版頁面中指定標題、中繼標記和其他 HTML 標頭（C#） |Microsoft Docs
author: rick-anderson
description: 查看從 [內容] 頁面，在主版頁面中定義各種 &lt;head&gt; 元素的不同技術。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 0aa1c84f-c9e2-4699-b009-0e28643ecbc6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: a4ec96a5b90f664655d554c064f9d50e76ad2d58
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74624498"
---
# <a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-c"></a>指定主版頁面的標題、中繼標籤與其他 HTML 標頭 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_CS.zip)或[下載 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_CS.pdf)

> 查看從 [內容] 頁面，在主版頁面中定義各種 &lt;head&gt; 元素的不同技術。

## <a name="introduction"></a>簡介

根據預設，在 Visual Studio 2008 中建立的新主版頁面，有兩個 ContentPlaceHolder 控制項：一個名為 head，而位於 `<head>` 元素中。另一個名為 `ContentPlaceHolder1`，放在 Web 表單中。 `ContentPlaceHolder1` 的目的是要在 Web 表單中定義一個可以逐頁自訂的區域。 `head` ContentPlaceHolder 可讓頁面將自訂內容新增至 `<head>` 區段。 （當然，這兩個 ContentPlaceHolders 可以修改或移除，而其他 ContentPlaceHolder 可能會新增至主版頁面。 我們的主版頁面（`Site.master`）目前有四個 ContentPlaceHolder 控制項）。

HTML `<head>` 元素做為存放庫，以取得不屬於檔本身的網頁檔相關資訊。 這包括網頁標題、搜尋引擎或內部編目程式使用的中繼資訊等資訊，以及外部資源的連結，例如 RSS 摘要、JavaScript 和 CSS 檔案。 這其中部分資訊可能與網站中的所有網頁有關。 例如，您可能會想要針對每個 ASP.NET 網頁全域匯入相同的 CSS 規則和 JavaScript 檔案。 不過，有些部分屬於頁面特定的 `<head>` 元素。 頁面標題是一個主要範例。

在本教學課程中，我們將探討如何在主版頁面和其內容頁面中定義全域和頁面特定的 `<head>` 區段標記。

## <a name="examining-the-master-pagesheadsection"></a>檢查主版頁面的`<head>`區段

Visual Studio 2008 所建立的預設主版頁面檔案包含下列 `<head>` 區段中的標記：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample1.aspx)]

請注意，`<head>` 元素包含 `runat="server"` 屬性，這表示它是伺服器控制項（而不是靜態 HTML）。 所有 ASP.NET 網頁都衍生自位於 `System.Web.UI` 命名空間的[`Page` 類別](https://msdn.microsoft.com/library/system.web.ui.page.aspx)。 這個類別包含一個 `Header` 屬性，可讓您存取頁面的 `<head>` 區域。 使用[`Header` 屬性](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx)，我們可以設定 ASP.NET 網頁的標題，或將其他標記新增至轉譯的 `<head>` 區段。 接著，您可以在頁面的 `Page_Load` 事件處理常式中撰寫一些程式碼，以自訂內容頁的 `<head>` 元素。 我們會檢查如何以程式設計方式，在步驟1中設定頁面的標題。

上述 `<head>` 元素中所顯示的標記也包含名為 head 的 ContentPlaceHolder 控制項。 這個 ContentPlaceHolder 控制項並不是必要的，因為內容頁可以程式設計方式將自訂內容新增至 `<head>` 元素。 不過，在內容頁需要將靜態標記新增至 `<head>` 專案的情況下很有用，因為靜態標記可以宣告方式加入至對應的內容控制項，而非以程式設計方式。

除了 `<title>` 專案和 head ContentPlaceHolder 外，主版頁面的 `<head>` 元素也應包含所有頁面通用的任何 `<head>`層級標記。 在我們的網站中，所有頁面都會使用在 `Styles.css` 檔中定義的 CSS 規則。 因此，我們已更新[*使用主版頁面建立全網站的版面*](creating-a-site-wide-layout-using-master-pages-cs.md)配置教學課程中的 `<head>` 專案，以包含對應的 `<link>` 元素。 我們的 `Site.master` 主版頁面的目前 `<head>` 標記如下所示。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>步驟1：設定內容頁面的標題

網頁的標題是透過 `<title>` 元素所指定。 請務必將每個頁面的標題設定為適當的值。 造訪頁面時，其標題會顯示在瀏覽器的標題列中。 此外，在將頁面加入書簽時，瀏覽器會使用頁面的標題做為書簽的建議名稱。 此外，許多搜尋引擎會在顯示搜尋結果時顯示頁面的標題。

> [!NOTE]
> 根據預設，Visual Studio 會將主版頁面中的 `<title>` 專案設定為 [未命名的頁面]。 同樣地，新的 ASP.NET 網頁也會將其 `<title>` 設為「未命名頁面」。 因為很容易忘記將頁面的標題設定為適當的值，所以在網際網路上有許多頁面上有標題為「未命名頁面」。 使用此標題搜尋 Google for web pages 會傳回大約2460000的結果。 即使是 Microsoft 也很容易發佈標題為「未命名頁面」的網頁。 在撰寫本文時，Google 搜尋在 Microsoft.com 網域中回報了236這類網頁。

ASP.NET 網頁可以使用下列其中一種方式來指定其標題：

- 藉由將值直接放在 `<title>` 元素內
- 使用 `<%@ Page %>` 指示詞中的 `Title` 屬性
- 使用 `Page.Title="title"` 或 `Page.Header.Title="title"`之類的程式碼，以程式設計方式設定頁面的 `Title` 屬性。

內容頁沒有 `<title>` 元素，因為它是在主版頁面中定義。 因此，若要設定內容頁的標題，您可以使用 `<%@ Page %>` 指示詞的 `Title` 屬性，或以程式設計方式進行設定。

### <a name="setting-the-pages-title-declaratively"></a>以宣告方式設定頁面的標題

內容頁的標題可以透過[`<%@ Page %>`](https://msdn.microsoft.com/library/ydy4x04a.aspx)指示詞的 `Title` 屬性，以宣告方式設定。 您可以直接修改 `<%@ Page %>` 指示詞或透過屬性視窗來設定這個屬性。 讓我們來看一下這兩種方法。

從來源視圖中，找出位於頁面宣告式標記頂端的 [`<%@ Page %>`] 指示詞。 `Default.aspx` 的 `<%@ Page %>` 指示詞如下：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample3.aspx)]

`<%@ Page %>` 指示詞會在剖析和編譯頁面時，指定 ASP.NET 引擎所使用的頁面特定屬性。 這包括其主版分頁檔案、其程式碼檔案的位置，以及其標題，以及其他資訊。

根據預設，建立新的內容頁面時 Visual Studio 會將 `Title` 屬性設定為 [未命名] 頁面。 將 `Default.aspx`的 `Title` 屬性從「未命名的頁面」變更為「主版頁面教學課程」，然後透過瀏覽器查看頁面。 [圖 1] 顯示瀏覽器的標題列，它會反映新的頁面標題。

![瀏覽器的標題列現在會顯示 &quot;主版頁面教學課程&quot;，而不是 &quot;未命名的頁面&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image1.png)

**圖 01**：瀏覽器的標題列現在會顯示「主版頁面教學課程」，而不是「未命名的頁面」

頁面的標題也可以從屬性視窗設定。 從 [屬性視窗] 的下拉式清單中選取 [檔]，以載入頁面層級屬性，其中包括 `Title` 屬性。 [圖 2] 顯示 `Title` 設定為「主版頁面教學課程」之後的屬性視窗。

![您也可以從 [屬性] 視窗設定標題](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image2.png)

**圖 02**：您也可以從 [屬性] 視窗設定標題

### <a name="setting-the-pages-title-programmatically"></a>以程式設計方式設定頁面的標題

當 ASP.NET 引擎呈現頁面時，主版頁面的 `<head runat="server">` 標記會轉譯成[`HtmlHead` 類別](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx)實例。 `HtmlHead` 類別具有[`Title` 屬性](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx)，其值會反映在轉譯的 `<title>` 元素中。 這個屬性可以透過 `Page.Header.Title`，從 ASP.NET 網頁的程式碼後置類別存取。這個相同的屬性也可以透過 `Page.Title`來存取。

若要練習以程式設計方式設定頁面的標題，請流覽至 `About.aspx` 頁面的程式碼後置類別，並為頁面的 `Load` 事件建立事件處理常式。 接下來，將頁面的標題設定為「主版頁面教學課程：：關於：：*日期*」，其中*日期*是目前日期。 加入此程式碼之後，您的 `Page_Load` 事件處理常式看起來應該如下所示：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample4.cs)]

[圖 3] 顯示瀏覽器的標題列，造訪 [`About.aspx`] 頁面。

![頁面的標題會以程式設計方式設定並包含目前的日期](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image3.png)

**圖 03**：網頁的標題以程式設計方式設定並包含目前的日期

## <a name="step-2-automatically-assigning-a-page-title"></a>步驟2：自動指派頁面標題

如我們在步驟1中所見，頁面的標題可以用宣告方式或以程式設計方式設定。 不過，如果您忘記明確地將標題變更為更具描述性的名稱，您的網頁將會有預設標題 [未命名頁面]。 在理想的情況下，系統會自動為我們設定頁面的標題，因為我們並未明確指定其值。 例如，如果在執行時間頁面的標題是「未命名的頁面」，我們可能會想要讓標題自動更新，使其與 ASP.NET 網頁的檔案名相同。 好消息是，只要稍加一些前置工作，就可以自動指派標題。

所有的 ASP.NET 網頁都是衍生自 `System.Web.UI` 命名空間中的 `Page` 類別。 `Page` 類別會定義 ASP.NET 網頁所需的最小功能，並公開基本屬性，例如 `IsPostBack`、`IsValid`、`Request`和 `Response`等等。 通常 web 應用程式中的每個頁面都需要額外的特性或功能。 提供這項工作的常見方式是建立自訂的基底頁面類別。 自訂基底頁面類別是您建立的類別，衍生自 `Page` 類別並包含額外的功能。 建立這個基類之後，您就可以讓 ASP.NET 網頁衍生自它（而不是 `Page` 類別），藉此提供 ASP.NET 網頁的擴充功能。

在此步驟中，我們會建立基底頁面，如果尚未明確設定標題，則會自動將頁面的標題設定為 ASP.NET 網頁的檔案名。 步驟3查看根據網站地圖設定頁面標題。

> [!NOTE]
> 建立和使用自訂基底頁面類別的完整檢查已超出本教學課程系列的範圍。 如需詳細資訊，請參閱[使用 ASP.NET 網頁的程式碼後置類別的自訂基類](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)。

### <a name="creating-the-base-page-class"></a>建立基底頁面類別

我們的第一項工作是建立基底頁面類別，這是擴充 `Page` 類別的類別。 首先，將 `App_Code` 資料夾加入至您的專案，方法是以滑鼠右鍵按一下 方案總管中的專案名稱，選擇 新增 ASP.NET 資料夾，然後選取 `App_Code`。 接下來，以滑鼠右鍵按一下 [`App_Code`] 資料夾，然後加入名為 `BasePage.cs`的新類別。 [圖 4] 顯示在加入 `App_Code` 資料夾和 `BasePage.cs` 類別之後的方案總管。

![新增 App_Code 資料夾和名為 BasePage 的類別](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image4.png)

**圖 04**：新增 `App_Code` 資料夾和名為 `BasePage` 的類別

> [!NOTE]
> Visual Studio 支援兩種專案管理模式：網站專案和 Web 應用程式專案。 [`App_Code`] 資料夾是設計用於網站專案模型。 如果您使用 Web 應用程式專案模型，請將 `BasePage.cs` 類別放在名為 `App_Code`以外的資料夾中，例如 `Classes`。 如需本主題的詳細資訊，請參閱將[網站專案遷移至 Web 應用程式專案](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx)。

由於自訂基底頁面會作為 ASP.NET 網頁程式碼後置類別的基類，因此需要擴充 `Page` 類別。

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample5.cs)]

每當要求 ASP.NET 網頁時，它會繼續進行一系列的階段，而要求的頁面中的累積會轉譯為 HTML。 我們可以藉由覆寫 `Page` 類別的 `OnEvent` 方法來利用階段。 針對我們的基礎頁面，讓我們自動設定標題（如果它尚未由 `LoadComplete` 階段明確指定）（您可能已經猜到，這會在 `Load` 階段之後發生）。

若要完成這項操作，請覆寫 `OnLoadComplete` 方法，並輸入下列程式碼：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample6.cs)]

`OnLoadComplete` 方法一開始先判斷是否尚未明確設定 `Title` 屬性。 如果 `Title` 屬性是 `null`、空字串，或具有值「未命名頁面」，則會將它指派給要求的 ASP.NET 網頁的檔案名。 例如，您可以透過 `Request.PhysicalPath` 屬性存取要求之 ASP.NET 網頁 `C:\MySites\Tutorial03\Login.aspx`的實體路徑。 `Path.GetFileNameWithoutExtension` 方法只會用來提取 filename 部分，然後將這個檔案名指派給 `Page.Title` 屬性。

> [!NOTE]
> 我邀請您增強此邏輯，以改善標題的格式。 例如，如果頁面的檔案名是 `Company-Products.aspx`，上述程式碼將會產生標題「公司產品」，但在理想的情況下，會以空格取代虛線，如同「公司產品」。 此外，每當發生大小寫變更時，請考慮加入空格。 也就是，請考慮加入程式碼，將檔案名 `OurBusinessHours.aspx` 轉換成「我們的上班時間」的標題。

### <a name="having-the-content-pages-inherit-the-base-page-class"></a>讓內容頁繼承基底頁面類別

我們現在需要更新網站中的 ASP.NET 網頁，以從自訂基底頁面（`BasePage`）衍生，而不是 `Page` 類別。 若要完成這項操作，請移至每個程式碼後置類別，並從變更類別宣告：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample7.cs)]

收件者：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample8.cs)]

這麼做之後，請透過瀏覽器造訪網站。 如果您造訪標題已明確設定的頁面，例如 `Default.aspx` 或 `About.aspx`，則會使用明確指定的標題。 不過，如果您造訪標題尚未從預設值變更的頁面（「未命名的頁面」），則基底頁面類別會將標題設定為頁面的檔案名。

[圖 5] 顯示透過瀏覽器觀看時的 `MultipleContentPlaceHolders.aspx` 頁面。 請注意，標題會精確地說是頁面的檔案名（副檔名較少）、"MultipleContentPlaceHolders"。

[![如果未明確指定標題，則會自動使用頁面的檔案名](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image5.png)

**圖 05**：如果未明確指定標題，則會自動使用頁面的檔案名（[按一下以查看完整大小的影像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image7.png)）

## <a name="step-3-basing-the-page-title-on-the-site-map"></a>步驟3：在網站地圖上以頁面標題為基礎

ASP.NET 提供穩健的網站地圖架構，可讓網頁開發人員在外部資源（例如 XML 檔案或資料庫資料表）中定義階層式網站地圖，以及用來顯示網站地圖相關資訊的 Web 控制項（例如 SiteMapPath）。功能表和 TreeView 控制項）。

網站地圖結構也可以從 ASP.NET 網頁的程式碼後置類別以程式設計方式存取。 如此一來，我們就可以在網站地圖中，自動將頁面的標題設定為其對應節點的標題。 讓我們增強在步驟2中建立的 `BasePage` 類別，讓它提供這項功能。 但首先我們需要為我們的網站建立網站地圖。

> [!NOTE]
> 本教學課程假設讀者已熟悉 ASP。NET 的網站地圖功能。 如需有關使用網站地圖的詳細資訊，請參閱我的多部分文章系列，[檢查 ASP。NET 的網站流覽](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)。

### <a name="creating-the-site-map"></a>建立網站地圖

網站對應系統是在[提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)之上建立的，它會將網站地圖 API 與在記憶體和持續性存放區之間序列化網站地圖資訊的邏輯分離。 .NET Framework 隨附[`XmlSiteMapProvider` 類別](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)，這是預設的網站地圖提供者。 正如其名，`XmlSiteMapProvider` 使用 XML 檔案做為其網站地圖存放區。 讓我們使用此提供者來定義我們的網站地圖。

首先，在網站的根資料夾中建立名為 `Web.sitemap`的網站地圖檔案。 若要完成此動作，請以滑鼠右鍵按一下方案總管中的網站名稱，選擇 [加入新專案]，然後選取 [網站地圖] 範本。 確定檔案的名稱為 `Web.sitemap`，然後按一下 [新增]。

[![將名為 Web.config 的檔案新增至網站的根資料夾](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image8.png)

**圖 06**：將名為 `Web.sitemap` 的檔案新增至網站的根資料夾（[按一下以查看完整大小的影像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image10.png)）

將下列 XML 新增至 `Web.sitemap` 檔案：

[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample9.xml)]

此 XML 會定義如 [圖 7] 所示的階層式網站對應結構。

![網站地圖目前由三個網站地圖節點組成](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image11.png)

**圖 07**：網站地圖目前由三個網站地圖節點組成

我們會在未來的教學課程中更新網站地圖結構，因為我們新增了新的範例。

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>更新主版頁面以包含流覽 Web 控制項

既然我們已定義網站地圖，讓我們更新主版頁面以包含流覽 Web 控制項。 具體而言，讓我們將 ListView 控制項新增至 [課程] 區段中的左欄，以轉譯具有網站地圖中所定義之每個節點的清單專案的未排序清單。

> [!NOTE]
> ListView 控制項是 ASP.NET 3.5 版的新手。 如果您使用的是舊版的 ASP.NET，請改用中繼器控制項。 如需 ListView 控制項的詳細資訊，請參閱[使用 ASP.NET 3.5 的 ListView 和 DataPager 控制項](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)。

從 [課程] 區段中移除現有的未排序清單標記開始。 接下來，從 [工具箱] 拖曳 [ListView] 控制項，並將它放在 [課程] 標題下方。 ListView 位於 [工具箱] 的 [資料] 區段中，另一個 view 控制項： GridView、DetailsView 和 FormView。 將 ListView 的 ID 屬性設定為 `LessonsList`。

在 [資料來源設定] 中，選擇將 ListView 系結至名為 `LessonsDataSource`的新 SiteMapDataSource 控制項。 SiteMapDataSource 控制項會從網站對應系統傳回階層式結構。

[![將 SiteMapDataSource 控制項系結至 LessonsList ListView 控制項](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image12.png)

**圖 08**：將 SiteMapDataSource 控制項系結至 `LessonsList` ListView 控制項（[按一下以查看完整大小的影像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image14.png)）

建立 SiteMapDataSource 控制項之後，我們必須定義 ListView 的範本，使其呈現未排序清單，其中包含 SiteMapDataSource 控制項所傳回之每個節點的清單專案。 這可以使用下列範本標記來完成：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample10.aspx)]

`LayoutTemplate` 會產生未排序清單的標記（`<ul>...</ul>`），而 `ItemTemplate` 會將 SiteMapDataSource 所傳回的每個專案呈現為包含特定課程連結的清單專案（`<li>`）。

設定 ListView 的範本之後，請造訪網站。 如 [圖 9] 所示，「課程」一節包含單一點符專案 Home。 關於和使用多個 ContentPlaceHolder 控制項課程的位置為何？ SiteMapDataSource 是設計來傳回階層式的資料集，但是 ListView 控制項只能顯示單一層級的階層。 因此，只會顯示 SiteMapDataSource 所傳回的第一個網站地圖節點層級。

[![課程區段包含單一清單專案](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image15.png)

**圖 09**：課程區段包含單一清單專案（[按一下以觀看完整大小的影像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image17.png)）

若要顯示多個層級，我們可以在 `ItemTemplate`內嵌套多個 Listview。 這項技術已在[使用資料教學課程系列](../../data-access/index.md)的[*主版頁面和網站導覽*教學](../../data-access/introduction/master-pages-and-site-navigation-cs.md)課程中進行檢查。 不過，在本教學課程的系列中，我們的網站地圖只會包含兩個層級： Home （最上層）;而每一堂課都是家裡的子項。 我們不會製作嵌套的 ListView，而是改為指示 SiteMapDataSource 不要傳回起始節點，方法是將其[`ShowStartingNode` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)設為 `false`。 最後的結果是，SiteMapDataSource 會藉由傳回網站地圖節點的第二層來開始。

有了這項變更，ListView 就會顯示 [關於] 和 [使用多個 ContentPlaceHolder 控制項] 課程的專案符號專案，但省略 [首頁] 的專案符號專案。 若要解決此問題，我們可以在 `LayoutTemplate`中明確新增 Home 的專案符號專案：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample11.aspx)]

藉由設定 SiteMapDataSource 來省略起始節點，並明確新增 Home 專案符號專案，[課程] 區段現在會顯示預期的輸出。

[![課程區段包含 Home 和每個子節點的專案符號專案](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image18.png)

**圖 10**： [課程] 區段包含 Home 和每個子節點的專案符號專案（[按一下以查看完整大小的影像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image20.png)）

### <a name="setting-the-title-based-on-the-site-map"></a>依據網站地圖設定標題

網站地圖備妥之後，我們就可以更新 `BasePage` 類別，使用網站地圖中指定的標題。 如同我們在步驟2中所做的，我們只想要在網頁的標題尚未由頁面開發人員明確設定時，才使用網站地圖節點的標題。 如果所要求的頁面未明確設定頁面標題，而且在網站地圖中找不到，則我們會切換回使用要求的分頁檔名（較少的副檔名），如同我們在步驟2中所做的一樣。 [圖 11] 說明此決策流程。

![如果沒有明確設定頁面標題，則會使用對應的網站地圖節點標題。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image21.png)

**圖 11**：如果沒有明確設定的頁面標題，則會使用對應的網站地圖節點標題

更新 `BasePage` 類別的 `OnLoadComplete` 方法，以包含下列程式碼：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample12.cs)]

就像之前一樣，`OnLoadComplete` 方法一開始會先決定是否已明確設定頁面的標題。 如果 `Page.Title` 是 `null`、空字串，或被指派值「未命名的頁面」，則程式碼會自動將值指派給 `Page.Title`。

為了決定要使用的標題，程式碼一開始會參考[`SiteMap` 類別](https://msdn.microsoft.com/library/system.web.sitemap.aspx)的[`CurrentNode` 屬性](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx)。 `CurrentNode` 會傳回網站地圖中對應至目前所要求頁面的[`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)實例。 假設在網站地圖中找到目前要求的頁面，則會將 `SiteMapNode`的 `Title` 屬性指派給頁面的標題。 如果目前要求的頁面不在網站地圖中，`CurrentNode` 會傳回 `null`，並使用要求的分頁檔名做為標題（如步驟2中所做的）。

[圖 12] 顯示透過瀏覽器觀看時的 `MultipleContentPlaceHolders.aspx` 頁面。 由於未明確設定此頁面的標題，因此會改用其對應的網站地圖節點標題。

![MultipleContentPlaceHolders .aspx 頁面的標題會從網站地圖中提取](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image22.png)

**圖 12**：從網站地圖提取 `MultipleContentPlaceHolders.aspx` 頁面的標題

## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>步驟4：將其他頁面特定標記新增至`<head>`區段

步驟1、2和3探討逐頁自訂 `<title>` 元素。 除了 `<title>`以外，`<head>` 區段也可能包含 `<meta>` 元素和 `<link>` 元素。 如本教學課程稍早所述，`Site.master`的 `<head>` 區段包含 `Styles.css`的 `<link>` 元素。 由於此 `<link>` 專案是在主版頁面中定義，因此它會包含在所有內容頁的 [`<head>`] 區段中。 但是，我們要如何以逐頁逐一加入 `<meta>` 和 `<link>` 元素？

將頁面特定內容新增至 `<head>` 區段的最簡單方式，是在主版頁面中建立 ContentPlaceHolder 控制項。 我們已經有這類 ContentPlaceHolder （名為 `head`）。 因此，若要新增自訂 `<head>` 標記，請在頁面中建立對應的內容控制項，並將標記放在該處。

為了說明如何將自訂 `<head>` 標記新增至頁面，讓我們在目前的內容頁集合中包含 `<meta>` description 元素。 `<meta>` description 元素提供網頁的簡短描述;大部分的搜尋引擎會在顯示搜尋結果時，以某種形式併入這項資訊。

`<meta>` description 元素具有下列格式：

[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample13.html)]

若要將此標記新增至 [內容] 頁面，請將上述文字加入至與主版頁面的標題 ContentPlaceHolder 對應的內容控制項。 例如，若要定義 `Default.aspx`的 `<meta>` description 元素，請新增下列標記：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample14.aspx)]

因為 head ContentPlaceHolder 不在 HTML 網頁的主體內，所以新增至內容控制項的標記不會顯示在設計檢視中。 若要查看 `<meta>` description 元素，請造訪瀏覽器 `Default.aspx`。 載入頁面之後，請查看 [來源]，並注意 [`<head>`] 區段包含內容控制項中指定的標記。

請花點時間將 `<meta>` description 元素新增至 `About.aspx`、`MultipleContentPlaceHolders.aspx`和 `Login.aspx`。

### <a name="programmatically-adding-markup-to-theheadregion"></a>以程式設計方式將標記新增至`<head>`區域

Head ContentPlaceHolder 可讓我們以宣告方式將自訂標記新增至主版頁面的 `<head>` 區域。 自訂標記也可以透過程式設計的方式加入。 回想一下，`Page` 類別的 `Header` 屬性會傳回主版頁面中定義的 `HtmlHead` 實例（`<head runat="server">`）。

能夠以程式設計方式將內容新增至 `<head>` 區域，會在要新增的內容為動態時很有用。 也許是根據造訪頁面的使用者而定;也許是從資料庫提取。 不論原因為何，您都可以將內容加入至 `HtmlHead`，方法是將控制項新增至其控制項集合，如下所示：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample15.cs)]

上述程式碼會將 `<meta>` 關鍵字專案新增至 `<head>` 區域，其提供描述頁面的關鍵字（以逗號分隔）清單。 請注意，若要加入 `<meta>` 標記，您可以建立[`HtmlMeta`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx)實例、設定其 `Name` 和 `Content` 屬性，然後將它新增至 `Header`的 `Controls` 集合。 同樣地，若要以程式設計方式加入 `<link>` 專案，請建立[`HtmlLink`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx)物件、設定其屬性，然後將它新增至 `Header`的 `Controls` 集合。

> [!NOTE]
> 若要加入任意標記，請建立[`LiteralControl`](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx)實例、設定其 `Text` 屬性，然後將它新增至 `Header`的 `Controls` 集合。

## <a name="summary"></a>總結

在本教學課程中，我們探討了各種不同的方式，可依頁面逐一新增 `<head>` 區域標記。 主版頁面應包含具有 ContentPlaceHolder 的 `HtmlHead` 實例（`<head runat="server">`）。 `HtmlHead` 實例允許內容頁面以程式設計方式存取 `<head>` 區域，以及以程式設計方式設定頁面的標題;ContentPlaceHolder 控制項可讓您透過內容控制項，以宣告方式將自訂標記新增至 `<head>` 區段。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [在 ASP.NET 中動態設定頁面的標題](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [檢查 ASP。NET 的網站流覽](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [如何使用 HTML 中繼標記](http://searchenginewatch.com/showPage.html?page=2167931)
- [ASP.NET 中的主版頁面](http://www.odetocode.com/articles/419.aspx)
- [使用 ASP.NET 3.5 的 ListView 和 DataPager 控制項](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [針對 ASP.NET 網頁的程式碼後置類別使用自訂基類](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Zack，Suchi Banerjee。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](multiple-contentplaceholders-and-default-content-cs.md)
> [下一頁](urls-in-master-pages-cs.md)
