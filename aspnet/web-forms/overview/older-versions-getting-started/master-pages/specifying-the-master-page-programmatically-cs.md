---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
title: 以程式設計方式指定主C#版頁面（） |Microsoft Docs
author: rick-anderson
description: 查看如何透過 PreInit 事件處理常式，以程式設計方式設定內容頁面的主版頁面。
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 7c4a3445-2440-4aee-b9fd-779c05e6abb2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
msc.type: authoredcontent
ms.openlocfilehash: 0db23ea05ba001c2bf9fc5330a60a767caa568a0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590382"
---
# <a name="specifying-the-master-page-programmatically-c"></a>以程式設計方式指定主版頁面 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.zip)或[下載 PDF](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.pdf)

> 查看如何透過 PreInit 事件處理常式，以程式設計方式設定內容頁面的主版頁面。

## <a name="introduction"></a>簡介

由於[*使用主版頁面建立全網站版面*](creating-a-site-wide-layout-using-master-pages-cs.md)配置的執筆範例，所有內容頁面都已透過 `@Page` 指示詞中的 `MasterPageFile` 屬性，以宣告方式參考其主版頁面。 例如，下列 `@Page` 指示詞會將內容頁面連結至主版頁面 `Site.master`：

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample1.aspx)]

`System.Web.UI` 命名空間中的[`Page` 類別](https://msdn.microsoft.com/library/system.web.ui.page.aspx)包含[`MasterPageFile` 屬性](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx)，可傳回內容頁面主版頁面的路徑;這是由 `@Page` 指示詞設定的這個屬性。 這個屬性也可以用來以程式設計方式指定內容頁面的主版頁面。 如果您想要根據外部因素（例如造訪頁面的使用者）動態指派主版頁面，這個方法就很有用。

在本教學課程中，我們會在網站中新增第二個主版頁面，並以動態方式決定要在執行時間使用的主版頁面

## <a name="step-1-a-look-at-the-page-lifecycle"></a>步驟1：查看頁面生命週期

每當要求抵達網頁伺服器做為內容頁面的 ASP.NET 網頁時，ASP.NET 引擎就必須將頁面的內容控制項保險絲到主版頁面的對應 ContentPlaceHolder 控制項。 這種融合會建立單一控制階層，然後可以繼續進行一般的網頁生命週期。

[圖 1] 說明這種融合。 [圖 1] 中的步驟1顯示初始內容和主版頁面控制項階層。 在 PreInit 階段的結尾處，頁面中的內容控制項會加入至主版頁面中對應的 ContentPlaceHolders （步驟2）。 在此融合之後，主版頁面會作為融合控制項階層的根。 這個已融合的控制項階層會接著加入至頁面，以產生完成的控制項階層（步驟3）。 最後結果是頁面的控制項階層會包含已融合的控制項階層。

[![主版頁面和內容頁面的控制階層會在 PreInit 階段一起合併在一起](specifying-the-master-page-programmatically-cs/_static/image2.png)](specifying-the-master-page-programmatically-cs/_static/image1.png)

**圖 01**：主版頁面和內容頁面的控制階層會在 PreInit 階段合在一起（[按一下以觀看完整大小的影像](specifying-the-master-page-programmatically-cs/_static/image3.png)）

## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>步驟2：從程式碼設定`MasterPageFile`屬性

這個融合中的主版頁面 partakes 取決於 `Page` 物件的 `MasterPageFile` 屬性值。 在 `@Page` 指示詞中設定 `MasterPageFile` 屬性，會在初始化階段（也就是頁面生命週期的第一個階段）中指派 `Page`的 `MasterPageFile` 屬性的最終效果。 或者，我們也可以透過程式設計方式設定此屬性。 不過，在 [圖 1] 中進行融合之前，必須先設定此屬性。

在 PreInit 階段開始時，`Page` 物件會引發其[`PreInit` 事件](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx)，並呼叫其[`OnPreInit` 方法](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)。 若要以程式設計方式設定主版頁面，可以建立 `PreInit` 事件的事件處理常式，或覆寫 `OnPreInit` 方法。 讓我們來看一下這兩種方法。

一開始請先開啟 `Default.aspx.cs`，即網站首頁的程式碼後置類別檔案。 輸入下列程式碼，為頁面的 `PreInit` 事件新增事件處理常式：

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample2.cs)]

我們可以從這裡設定 `MasterPageFile` 屬性。 更新程式碼，讓它將 "~/Site.master" 值指派給 `MasterPageFile` 屬性。

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample3.cs)]

如果您設定中斷點並開始進行偵錯工具，您會看到每次造訪 `Default.aspx` 頁面時，或每當有回傳此頁面時，就會執行 `Page_PreInit` 事件處理常式，並將 `MasterPageFile` 屬性指派給 "~/Site.master"。

或者，您可以覆寫 `Page` 類別的 `OnPreInit` 方法，並在該處設定 `MasterPageFile` 屬性。 在此範例中，我們不會在特定頁面中設定主版頁面，而是從 `BasePage`。 回想一下，我們已在[*主版頁面教學課程中指定標題、中繼標記和其他 HTML 標頭，* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)以在中建立自訂基底頁面類別（`BasePage`）。 目前 `BasePage` 會覆寫 `Page` 類別的 `OnLoadComplete` 方法，其中會根據網站地圖資料設定頁面的 `Title` 屬性。 讓我們更新 `BasePage`，同時覆寫 `OnPreInit` 方法，以程式設計方式指定主版頁面。

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample4.cs)]

因為我們的所有內容頁面都是衍生自 `BasePage`，所以它們現在會以程式設計方式指派其主版頁面。 此時，`Default.aspx.cs` 中的 `PreInit` 事件處理常式是多餘的;請隨意移除它。

### <a name="what-about-thepagedirective"></a>那麼`@Page`指示詞呢？

有點困惑的是，現在會在兩個地方指定內容頁的 `MasterPageFile` 屬性：以程式設計方式在 `BasePage` 類別的 `OnPreInit` 方法，以及透過每個內容頁的 `@Page` 指示詞中的 `MasterPageFile` 屬性。

頁面生命週期中的第一個階段是初始化階段。 在此階段中，`Page` 物件的 `MasterPageFile` 屬性會被指派 `@Page` 指示詞中 `MasterPageFile` 屬性的值（如果有提供的話）。 PreInit 階段會遵循初始化階段，而在此，我們會以程式設計方式設定 `Page` 物件的 `MasterPageFile` 屬性，進而覆寫從 `@Page` 指示詞指派的值。 因為我們要以程式設計方式設定 `Page` 物件的 `MasterPageFile` 屬性，所以我們可以從 `@Page` 指示詞移除 `MasterPageFile` 屬性，而不會影響使用者的經驗。 為了說服這一點，請繼續並從 `Default.aspx` 的 `@Page` 指示詞中移除 `MasterPageFile` 屬性，然後透過瀏覽器造訪頁面。 如您所預期，輸出與移除屬性之前相同。

`MasterPageFile` 屬性是透過 `@Page` 指示詞還是以程式設計方式設定，會不重要至使用者的體驗。 不過，在設計階段期間，Visual Studio 會使用 `@Page` 指示詞中的 `MasterPageFile` 屬性，在設計工具中產生 WYSIWYG 視圖。 如果您在 Visual Studio 中返回 `Default.aspx` 並流覽至設計工具，您會看到訊息：「主版分頁錯誤 . 頁面上有需要主版頁面參考的控制項，但未指定任何內容」（請參閱 [圖 2]）。

簡言之，您必須將 `MasterPageFile` 屬性保留在 `@Page` 指示詞中，以在 Visual Studio 中享有豐富的設計階段體驗。

[![Visual Studio 使用 @Page 指示詞的 MasterPageFile 屬性來轉譯設計檢視](specifying-the-master-page-programmatically-cs/_static/image5.png)](specifying-the-master-page-programmatically-cs/_static/image4.png)

**圖 02**： Visual Studio 使用 `@Page` 指示詞的 `MasterPageFile` 屬性來轉譯設計檢視（[按一下以觀看完整大小的影像](specifying-the-master-page-programmatically-cs/_static/image6.png)）

## <a name="step-3-creating-an-alternative-master-page"></a>步驟3：建立替代的主版頁面

因為內容頁的主版頁面可在執行時間以程式設計方式設定，所以可以根據某些外部準則動態載入特定的主版頁面。 當網站的版面配置需要根據使用者而有所不同時，這項功能就很有用。 比方說，blog engine web 應用程式可能會允許其使用者選擇其 blog 的版面配置，其中每個版面配置都與不同的主版頁面相關聯。 在執行時間，當訪客正在觀看使用者的 blog 時，web 應用程式就必須判斷 blog 的版面配置，並以動態方式將對應的主版頁面與內容頁面產生關聯。

讓我們檢查如何根據某些外部準則，在執行時間動態載入主版頁面。 我們的網站目前僅包含一個主版頁面（`Site.master`）。 我們需要另一個主版頁面，說明如何在執行時間選擇主版頁面。 此步驟著重于建立和設定新的主版頁面。 步驟4探討如何判斷要在執行時間使用的主版頁面。

在名為 `Alternate.master`的根資料夾中建立新的主版頁面。 此外，將新的樣式表單加入至名為 `AlternateStyles.css`的網站。

[![將另一個主版頁面和 CSS 檔案新增至網站](specifying-the-master-page-programmatically-cs/_static/image8.png)](specifying-the-master-page-programmatically-cs/_static/image7.png)

**圖 03**：將另一個主版頁面和 CSS 檔案新增至網站（[按一下以觀看完整大小的影像](specifying-the-master-page-programmatically-cs/_static/image9.png)）

我設計了 `Alternate.master` 主版頁面，讓標題顯示在頁面頂端，置中和海軍藍背景。 我已分配左欄，並將該內容移至 `MainContent` ContentPlaceHolder 控制項底下，這現在會跨越整個頁面寬度。 此外，我 nixed 了未排序的課程清單，並將其取代為上方的水準清單 `MainContent`。 我也更新了主版頁面所使用的字型和色彩（以及延伸模組的內容頁面）。 [圖 4] 顯示使用 `Alternate.master` 主版頁面時的 `Default.aspx`。

> [!NOTE]
> ASP.NET 包括定義*主題*的能力。 主題是影像、CSS 檔案和樣式相關的 Web 控制項屬性設定的集合，可在執行時間套用至頁面。 如果您的網站版面配置只有顯示的影像和其 CSS 規則不同，主題就是一種方式。 如果版面配置的差異較大（例如使用不同的 Web 控制項或具有完全不同的版面配置），則您必須使用個別的主版頁面。 如需主題的詳細資訊，請參閱本教學課程結尾的進一步閱讀章節。

[![我們的內容頁面現在可以使用全新的外觀與風格](specifying-the-master-page-programmatically-cs/_static/image11.png)](specifying-the-master-page-programmatically-cs/_static/image10.png)

**圖 04**：我們的內容頁面現在可以使用新的外觀和操作（[按一下以觀看完整大小的影像](specifying-the-master-page-programmatically-cs/_static/image12.png)）

當主要和內容頁面的標記已融合時，`MasterPage` 類別會進行檢查，以確保內容頁面中的每個內容控制項都參考主版頁面中的 ContentPlaceHolder。 如果找到參考不存在之 ContentPlaceHolder 的內容控制項，則會擲回例外狀況（exception）。 換句話說，指派給 [內容] 頁面的主版頁面必須具有 [內容] 頁面中每個內容控制項的 ContentPlaceHolder。

`Site.master` 主版頁面包含四個 ContentPlaceHolder 控制項：

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

網站中的部分內容頁面只包含一個或兩個內容控制項;其他則包含每個可用 ContentPlaceHolders 的內容控制項。 如果我們的新主版頁面（`Alternate.master`）可能會指派給具有 `Site.master` 中所有 ContentPlaceHolders 之內容控制項的內容頁面，`Alternate.master` 也必須包含與 `Site.master`相同的 ContentPlaceHolder 控制項。

若要讓您的 `Alternate.master` 主版頁面看起來像我一樣（請參閱 [圖 4]），請從在 `AlternateStyles.css` 樣式表單中定義主版頁面的樣式開始。 將下列規則新增至 `AlternateStyles.css`：

[!code-css[Main](specifying-the-master-page-programmatically-cs/samples/sample5.css)]

接下來，將下列宣告式標記新增至 `Alternate.master`。 如您所見，`Alternate.master` 包含四個 ContentPlaceHolder 控制項，其 `ID` 值與 `Site.master`中的 ContentPlaceHolder 控制項相同。 此外，它還包含 ScriptManager 控制項，這是我們的網站中使用 ASP.NET AJAX 架構的網頁所需的。

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>測試新的主版頁面

若要測試這個新的主版頁面，請更新 `BasePage` 類別的 `OnPreInit` 方法，讓 `MasterPageFile` 屬性指派 "~/Alternate.master" 值，然後造訪網站。 除了2： `~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx`以外，每個頁面都應該運作而不會發生錯誤。 將產品加入至 DetailsView 的 `~/Admin/AddProduct.aspx` 會導致程式程式碼中的 `NullReferenceException` 嘗試設定主版頁面的 `GridMessageText` 屬性。 流覽 `~/Admin/Products.aspx` 在頁面載入時擲回 `InvalidCastException`，訊息為：「無法將類型 ' ASP. 替代\_master ' 的物件轉換成類型 ' ASP. site\_master '」。

因為 `Site.master` 程式碼後置類別包含未在 `Alternate.master`中定義的公用事件、屬性和方法，所以會發生這些錯誤。 這兩個頁面的標記部分具有參考 `Site.master` 主版頁面的 `@MasterType` 指示詞。

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample7.aspx)]

此外，DetailsView 在 `~/Admin/AddProduct.aspx` 中的 `ItemInserted` 事件處理常式包含將鬆散類型 `Page.Master` 屬性轉換為 `Site`類型物件的程式碼。 `@MasterType` 指示詞（以這種方式使用）和 `ItemInserted` 事件處理常式中的轉換會將 `~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx` 頁面緊密結合到 `Site.master` 主版頁面。

若要打破這種緊密結合，我們可以讓 `Site.master` 和 `Alternate.master` 衍生自包含公用成員定義的通用基類。 之後，我們可以更新 `@MasterType` 指示詞來參考這個通用基底型別。

### <a name="creating-a-custom-base-master-page-class"></a>建立自訂的基底主版頁面類別

將新的類別檔案新增至名為 `BaseMasterPage.cs` 的 `App_Code` 資料夾中，並讓它衍生自 `System.Web.UI.MasterPage`。 我們需要在 `BaseMasterPage`中定義 `RefreshRecentProductsGrid` 方法和 `GridMessageText` 屬性，但我們無法直接從 `Site.master` 移動它們，因為這些成員會使用 `Site.master` 主版頁面（`RecentProducts` GridView 和 `GridMessage` 標籤）特定的 Web 控制項。

我們需要做的是設定 `BaseMasterPage`，讓這些成員定義在該處，但實際上是由 `BaseMasterPage`的衍生類別（`Site.master` 和 `Alternate.master`）所實。 藉由將類別及其成員標示為 `abstract`，就可以進行這種類型的繼承。 簡單地說，將 `abstract` 關鍵字加入這兩個成員，會宣佈 `BaseMasterPage` 尚未實作為 `RefreshRecentProductsGrid` 和 `GridMessageText`，但其衍生類別將會。

我們也需要在 `BaseMasterPage` 中定義 `PricesDoubled` 事件，並提供衍生類別引發事件的方法。 .NET Framework 中用來協助此行為的模式，是在基類中建立公用事件，並新增名為 `OnEventName`的受保護、`virtual` 方法。 然後，衍生的類別可以呼叫這個方法來引發事件，或覆寫它，以便在引發事件之前或之後立即執行程式碼。

更新您的 `BaseMasterPage` 類別，使其包含下列程式碼：

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample8.cs)]

接下來，移至 `Site.master` 程式碼後置類別，並讓它衍生自 `BaseMasterPage`。 因為 `BaseMasterPage` 是 `abstract` 所以我們必須在 `Site.master`中覆寫這些 `abstract` 的成員。 將 `override` 關鍵字新增至方法和屬性定義。 此外，也請使用基類的 `OnPricesDoubled` 方法的呼叫，更新 `DoublePrice` 按鈕的 `Click` 事件處理常式中引發 `PricesDoubled` 事件的程式碼。

這些修改之後，`Site.master` 程式碼後置類別應該包含下列程式碼：

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample9.cs)]

我們也需要更新 `Alternate.master`的程式碼後置類別，以衍生自 `BaseMasterPage` 並覆寫兩個 `abstract` 的成員。 但是因為 `Alternate.master` 不包含會列出最新產品的 GridView，或是在新產品新增至資料庫之後顯示訊息的標籤，所以這些方法不需要執行任何動作。

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample10.cs)]

### <a name="referencing-the-base-master-page-class"></a>參考基底主版頁面類別

既然我們已完成 `BaseMasterPage` 類別，並將兩個主版頁面延伸，我們的最後一個步驟是更新 `~/Admin/AddProduct.aspx`，並 `~/Admin/Products.aspx` 頁面來參考此一般類型。 從變更兩個頁面中的 `@MasterType` 指示詞開始：

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample11.aspx)]

收件者：

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample12.aspx)]

`@MasterType` 屬性現在會參考基底類型（`BaseMasterPage`），而不是參考檔案路徑。 因此，在這兩個頁面的程式碼後置類別中使用的強型別 `Master` 屬性現在是 `BaseMasterPage` 型別（而不是型別 `Site`）。 有了這項變更之後，就 `~/Admin/Products.aspx`。 之前，這會導致轉型錯誤，因為頁面已設定為使用 `Alternate.master` 主版頁面，但 `@MasterType` 指示詞參考 `Site.master` 檔。 但現在頁面會轉譯而不會發生錯誤。 這是因為 `Alternate.master` 主版頁面可以轉換成 `BaseMasterPage` 類型的物件（因為它會將它擴充）。

`~/Admin/AddProduct.aspx`需要進行一項小變更。 DetailsView 控制項的 `ItemInserted` 事件處理常式會同時使用強型別的 `Master` 屬性和鬆散類型的 `Page.Master` 屬性。 我們已修正更新 `@MasterType` 指示詞時的強型別參考，但我們仍需要更新鬆散型別參考。 取代下列程式程式碼：

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample13.cs)]

具有下列的，會將 `Page.Master` 轉換成基底類型：

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample14.cs)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>步驟4：決定要系結至內容頁面的主版頁面

我們的 `BasePage` 類別目前會在頁面生命週期的 PreInit 階段中，將所有內容頁的 `MasterPageFile` 屬性設定為硬式編碼的值。 我們可以將此程式碼更新為以某個外部因素作為主版頁面的基礎。 可能要載入的主版頁面，取決於目前登入之使用者的喜好設定。 在這種情況下，我們需要在 `BasePage` 中的 `OnPreInit` 方法中撰寫程式碼，以查閱目前造訪的使用者主版頁面喜好設定。

讓我們建立一個網頁，讓使用者選擇要使用的主版頁面-`Site.master` 或 `Alternate.master`，並將此選項儲存在會話變數中。 首先，在名為 `ChooseMasterPage.aspx`的根目錄中建立新的網頁。 建立此頁面（或任何其他內容頁面因而需要）時，您不需要將它系結至主版頁面，因為主版頁面是以程式設計方式在 `BasePage`中設定。 不過，如果您未將新的頁面系結至主版頁面，則新頁面的預設宣告式標記會包含主版頁面所提供的 Web 表單和其他內容。 您必須以適當的內容控制項手動取代此標記。 基於這個理由，我發現將新的 ASP.NET 網頁系結至主版頁面更容易。

> [!NOTE]
> 由於 `Site.master` 和 `Alternate.master` 擁有一組相同的 ContentPlaceHolder 控制項，因此在您建立新的內容頁面時，您所選擇的主版頁面並不重要。 為求一致，我建議使用 `Site.master`。

[![將新的內容頁面新增至網站](specifying-the-master-page-programmatically-cs/_static/image14.png)](specifying-the-master-page-programmatically-cs/_static/image13.png)

**圖 05**：將新的內容頁面新增至網站（[按一下以觀看完整大小的影像](specifying-the-master-page-programmatically-cs/_static/image15.png)）

更新 `Web.sitemap` 檔案以包含此課程的專案。 在主版頁面的 `<siteMapNode>` 下方新增下列標記，並 ASP.NET AJAX 課程：

[!code-xml[Main](specifying-the-master-page-programmatically-cs/samples/sample15.xml)]

將任何內容加入至 `ChooseMasterPage.aspx` 頁面之前，請花點時間更新頁面的程式碼後置類別，使其衍生自 `BasePage` （而不是 `System.Web.UI.Page`）。 接下來，將 DropDownList 控制項新增至頁面，將其 `ID` 屬性設為 `MasterPageChoice`，然後新增兩個 ListItems，其 `Text` 值為 "~/Site.master" 和 "~/Alternate.master"。

將按鈕 Web 控制項新增至頁面，並將其 `ID` 和 `Text` 屬性分別設定為 `SaveLayout` 和「儲存版面配置選擇」。 此時，您頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample16.aspx)]

第一次流覽頁面時，我們必須顯示使用者目前選取的主版頁面選擇。 建立 `Page_Load` 事件處理常式，並新增下列程式碼：

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample17.cs)]

上述程式碼只會在第一頁流覽（而不是在後續回傳時）執行。 它會先檢查會話變數 `MyMasterPage` 是否存在。 如果有的話，它會嘗試在 `MasterPageChoice` DropDownList 中尋找相符的檔案。 如果找到相符的符合內容，其 `Selected` 屬性會設定為 `true`。

我們也需要將使用者選擇儲存到 `MyMasterPage` 會話變數的程式碼。 為 `SaveLayout` 按鈕的 `Click` 事件建立事件處理常式，並新增下列程式碼：

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample18.cs)]

> [!NOTE]
> 在回傳時，`Click` 事件處理常式執行的時間，已選取主版頁面。 因此，在下一頁流覽之前，使用者的下拉式清單選擇將不會生效。 `Response.Redirect` 會強制瀏覽器重新要求 `ChooseMasterPage.aspx`。

完成 [`ChooseMasterPage.aspx`] 頁面後，我們的最後一項工作是根據 `MyMasterPage` 會話變數的值，`BasePage` 指派 `MasterPageFile` 屬性。 如果未設定會話變數，`BasePage` 預設為 `Site.master`。

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample19.cs)]

> [!NOTE]
> 我將指派 `Page` 物件之 `MasterPageFile` 屬性的程式碼，從 `OnPreInit` 事件處理常式移至兩個不同的方法。 第一個方法 `SetMasterPageFile`，會將 `MasterPageFile` 屬性指派給第二個方法所傳回的值，`GetMasterPageFileFromSession`。 我將 `SetMasterPageFile` 方法 `virtual` 讓擴充 `BasePage` 的未來類別可以視需要覆寫以執行自訂邏輯。 我們會在下一個教學課程中看到覆寫 `BasePage``SetMasterPageFile` 屬性的範例。

將此程式碼備妥之後，請造訪 `ChooseMasterPage.aspx` 頁面。 一開始會選取 [`Site.master` 主版] 頁面（請參閱 [圖 6]），但使用者可以從下拉式清單中挑選不同的主版頁面。

[使用 [網站] 顯示 ![內容頁面。主要主版頁面](specifying-the-master-page-programmatically-cs/_static/image17.png)](specifying-the-master-page-programmatically-cs/_static/image16.png)

**圖 06**：內容頁面會使用 `Site.master` 主版頁面顯示（[按一下以觀看完整大小的影像](specifying-the-master-page-programmatically-cs/_static/image18.png)）

[現在會使用 [其他] 主版頁面來顯示 ![內容頁面](specifying-the-master-page-programmatically-cs/_static/image20.png)](specifying-the-master-page-programmatically-cs/_static/image19.png)

**圖 07**：現在會使用 `Alternate.master` 主版頁面來顯示內容頁面（[按一下以觀看完整大小的影像](specifying-the-master-page-programmatically-cs/_static/image21.png)）

## <a name="summary"></a>總結

流覽內容頁時，其內容控制項會與主版頁面的 ContentPlaceHolder 控制項一起建立。 [內容] 頁面的 [主版] 頁面是由 `Page` 類別的 [`MasterPageFile`] 屬性工作表示，在初始化階段期間會指派給 `@Page` 指示詞的 `MasterPageFile` 屬性。 如本教學課程所示，只要在 PreInit 階段結束之前，我們就可以將值指派給 `MasterPageFile` 屬性。 能夠以程式設計方式指定主版頁面，可為更先進的案例開啟門，例如根據外部因素動態地將內容頁系結至主版頁面。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 網頁生命週期圖表](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET 網頁生命週期總覽](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET 主題和外觀總覽](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [主版頁面：秘訣、訣竅和陷阱](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 中的主題](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Suchi Banerjee。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](master-pages-and-asp-net-ajax-cs.md)
> [下一頁](nested-master-pages-cs.md)
