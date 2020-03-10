---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
title: 多個 ContentPlaceHolders 和預設內容（VB） |Microsoft Docs
author: rick-anderson
description: 檢查如何將多個內容預留位置加入主版頁面，以及如何在內容預留位置中指定預設內容。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 866a7177-6884-451e-88f4-c934b1dd1af5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
msc.type: authoredcontent
ms.openlocfilehash: b71cacb143094dcc5cf483c69c2fcc0f10def51c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78571894"
---
# <a name="multiple-contentplaceholders-and-default-content-vb"></a>多個 ContentPlaceHolder 與預設內容 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_VB.zip)或[下載 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_VB.pdf)

> 檢查如何將多個內容預留位置加入主版頁面，以及如何在內容預留位置中指定預設內容。

## <a name="introduction"></a>簡介

在先前的教學課程中，我們探討了主版頁面如何讓 ASP.NET 開發人員建立一致的全網站配置。 主版頁面會定義所有內容頁面和區域通用的標記，這些都可在每頁上進行自訂。 在上一個教學課程中，我們建立了一個簡單的主版頁面（`Site.master`）和兩個內容頁面（`Default.aspx` 和 `About.aspx`）。 主版頁面是由名為 `head` 和 `MainContent`的兩個 ContentPlaceHolders 所組成，分別位於 `<head>` 元素和 Web Form 中。 雖然內容頁面各有兩個內容控制項，但我們只會針對對應至 `MainContent`的標記指定標記。

如同 `Site.master`中的兩個 ContentPlaceHolder 控制項所總合，主版頁面可能包含多個 ContentPlaceHolders。 最多，主版頁面可能會指定 ContentPlaceHolder 控制項的預設標記。 然後，[內容] 頁面可以選擇性地指定自己的標記或使用預設標記。 在本教學課程中，我們將探討如何在主版頁面中使用多個內容控制項，並瞭解如何在 ContentPlaceHolder 控制項中定義預設標記。

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>步驟1：將其他 ContentPlaceHolder 控制項新增至主版頁面

許多網站設計都包含螢幕上的數個區域，每個頁面都有自訂。 `Site.master`，我們在上一個教學課程中建立的主版頁面包含名為 `MainContent`的 Web 表單內的單一 ContentPlaceHolder。 具體而言，這個 ContentPlaceHolder 位於 `mainContent` `<div>` 元素中。

[圖 1] 顯示透過瀏覽器觀看 `Default.aspx`。 以紅色圈起的區域是對應至 `MainContent`的頁面特定標記。

[![圓圈區域會顯示目前每頁可自訂的區域](multiple-contentplaceholders-and-default-content-vb/_static/image2.png)](multiple-contentplaceholders-and-default-content-vb/_static/image1.png)

**圖 01**：圓形區域會顯示頁面上目前可自訂的區域（[按一下以觀看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image3.png)）

假設除了 [圖 1] 所示的區域之外，我們還需要將頁面特定的專案新增至 [課程和新聞] 區段下方的左欄。 為了達到此目的，我們將另一個 ContentPlaceHolder 控制項新增至主版頁面。 若要跟著做，請在 Visual Web Developer 中開啟 `Site.master` 主版頁面，然後將 [ContentPlaceHolder] 控制項從 [工具箱] 拖曳至 [新聞] 區段後面的設計工具。 將 ContentPlaceHolder 的 `ID` 設定為 `LeftColumnContent`。

[![將 ContentPlaceHolder 控制項新增至主版頁面的左側資料行](multiple-contentplaceholders-and-default-content-vb/_static/image5.png)](multiple-contentplaceholders-and-default-content-vb/_static/image4.png)

**圖 02**：將 ContentPlaceHolder 控制項新增至主版頁面的左側資料行（[按一下以查看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image6.png)）

藉由將 `LeftColumnContent` ContentPlaceHolder 新增至主版頁面，我們可以在頁面上包含內容控制項（其 `ContentPlaceHolderID` 設定為 `LeftColumnContent`），以逐頁定義此區域的內容。 我們會在步驟2中檢查此程式。

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>步驟2：在內容頁面中定義新 ContentPlaceHolder 的內容

將新的內容頁面加入至網站時，Visual Web Developer 會在頁面中自動為所選主版頁面中的每個 ContentPlaceHolder 建立內容控制項。 在步驟1中，將 `LeftColumnContent` ContentPlaceHolder 新增至主版頁面，新的 ASP.NET 網頁現在會有三個內容控制項。

為了說明這一點，請將新的 [內容] 頁面加入至系結至 `Site.master` 主版頁面的根目錄中名為 `MultipleContentPlaceHolders.aspx`。 Visual Web Developer 會使用下列宣告式標記來建立此頁面：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample1.aspx)]

在內容控制項中輸入一些內容，參考 `MainContent` ContentPlaceHolders （`Content2`）。 接下來，將下列標記新增至 `Content3` 內容控制項（它會參考 `LeftColumnContent` ContentPlaceHolder）：

[!code-html[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample2.html)]

新增此標記之後，請造訪瀏覽器中的頁面。 如 [圖 3] 所示，放在 [`Content3` 內容] 控制項中的標記會顯示在 [新聞] 區段下方的左欄中（以紅色圈起）。 放在 `Content2` 中的標記會顯示在頁面的右側部分（以藍色圈起）。

[![左欄現在包含 [新聞] 區段下方的頁面特定內容](multiple-contentplaceholders-and-default-content-vb/_static/image8.png)](multiple-contentplaceholders-and-default-content-vb/_static/image7.png)

**圖 03**：左側資料行現在包含 [新聞] 區段底下的頁面特定內容（[按一下以觀看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image9.png)）

### <a name="defining-content-in-existing-content-pages"></a>定義現有內容頁面中的內容

建立新的 [內容] 頁面會自動納入我們在步驟1中新增的 ContentPlaceHolder 控制項。 但我們的兩個現有的內容頁面-`About.aspx` 和 `Default.aspx`-沒有 `LeftColumnContent` ContentPlaceHolder 的內容控制項。 若要在這兩個現有的頁面中指定此 ContentPlaceHolder 的內容，我們需要自行新增內容控制項。

不同于大部分 ASP.NET 的 Web 控制項，Visual Web Developer 工具箱不包含內容控制項專案。 我們可以在來源視圖中手動輸入內容控制項的宣告式標記，但更簡單且更快速的方法是使用設計檢視。 開啟 [`About.aspx`] 頁面，並切換至 [設計檢視]。 如 [圖 4] 所示，`LeftColumnContent` ContentPlaceHolder 會出現在設計檢視中;如果您將滑鼠停留在其上方，則會顯示標題： "LeftColumnContent （Master）"。 在標題中包含 "Master"，表示此 ContentPlaceHolder 的頁面中未定義內容控制項。 如果有 ContentPlaceHolder 的內容控制項（例如 `MainContent`的案例），標題將會讀取： "*ContentPlaceHolderID* （Custom）"。

若要將 `LeftColumnContent` ContentPlaceHolder 的內容控制項新增至 `About.aspx`，請展開 ContentPlaceHolder 的智慧標籤，然後按一下 [建立自訂內容] 連結。

[![[關於 .aspx] 的設計檢視會顯示 LeftColumnContent ContentPlaceHolder](multiple-contentplaceholders-and-default-content-vb/_static/image11.png)](multiple-contentplaceholders-and-default-content-vb/_static/image10.png)

**圖 04**： `About.aspx` 的設計檢視會顯示 `LeftColumnContent` ContentPlaceHolder （[按一下以觀看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image12.png)）

按一下 [建立自訂內容] 連結會在頁面中產生必要的內容控制項，並將其 [`ContentPlaceHolderID`] 屬性設為 ContentPlaceHolder 的 `ID`。 例如，按一下 `About.aspx` 中 `LeftColumnContent` 區域的 [建立自訂內容] 連結，就會將下列宣告式標記新增至頁面：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>省略內容控制項

ASP.NET 不需要所有內容頁都包含主版頁面中定義之每個 ContentPlaceHolder 的內容控制項。 如果省略內容控制項，ASP.NET 引擎會使用主版頁面中的 ContentPlaceHolder 內所定義的標記。 此標記稱為 ContentPlaceHolder 的*預設內容*，適用于某些區域的內容在大多數頁面中都是通用的案例，但必須針對少量頁面進行自訂。 步驟3探索如何在主版頁面中指定預設內容。

目前，`Default.aspx` 包含 `head` 和 `MainContent` ContentPlaceHolders 的兩個內容控制項;它沒有 `LeftColumnContent`的內容控制項。 因此，轉譯 `Default.aspx` 時，會使用 `LeftColumnContent` ContentPlaceHolder 的預設內容。 由於我們尚未定義此 ContentPlaceHolder 的任何預設內容，因此最終的結果就是不會針對此區域發出任何標記。 若要確認此行為，請透過瀏覽器造訪 `Default.aspx`。 如 [圖 5] 所示，[新聞] 區段下方的左欄中不會發出任何標記。

[![LeftColumnContent ContentPlaceHolder 不會轉譯任何內容](multiple-contentplaceholders-and-default-content-vb/_static/image14.png)](multiple-contentplaceholders-and-default-content-vb/_static/image13.png)

**圖 05**： `LeftColumnContent` ContentPlaceHolder 不會轉譯任何內容（[按一下以觀看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image15.png)）

## <a name="step-3-specifying-default-content-in-the-master-page"></a>步驟3：在主版頁面中指定預設內容

部分網站設計包括一個區域，其內容對於網站中的所有頁面都相同，但有一或兩個例外。 假設有一個支援使用者帳戶的網站。 這類網站需要一個登入頁面，訪客可以在其中輸入其認證來登入網站。 若要加速登入程式，網站設計工具可能會在每個頁面的左上角包含 [使用者名稱] 和 [密碼] 文字方塊，讓使用者不需要明確流覽登入頁面，即可進行登入。 雖然這些 [使用者名稱] 和 [密碼] 文字方塊在大部分的頁面上都很有用，但在登入頁面中，它們已經包含使用者認證的文字方塊。

若要執行這項設計，您可以在主版頁面的左上角建立 ContentPlaceHolder 控制項。 在其左上角顯示 [使用者名稱] 和 [密碼] 文字方塊所需的每個頁面，都會建立此 ContentPlaceHolder 的內容控制項，並新增必要的介面。 另一方面，登入頁面會省略新增此 ContentPlaceHolder 的內容控制項，或建立未定義任何標記的內容控制項。 這種方法的缺點是，我們必須記得將 [使用者名稱] 和 [密碼] 文字方塊新增至我們新增至網站的每一頁（登入頁面除外）。 這會詢問問題。 我們很可能忘了將這些文字方塊加入到頁面或兩者中，更糟的是，我們可能不會正確地執行介面（或許只會新增一個 textbox，而不是兩個）。

較好的解決方案是將 [使用者名稱] 和 [密碼] 文字方塊定義為 ContentPlaceHolder 的預設內容。 如此一來，我們只需要覆寫這幾頁中不會顯示 [使用者名稱] 和 [密碼] 文字方塊的預設內容（例如，登入頁面）。 為了說明如何指定 ContentPlaceHolder 控制項的預設內容，讓我們來執行剛才討論過的案例。

> [!NOTE]
> 本教學課程的其餘部分會更新我們的網站，以將登入介面包含在所有頁面的左欄中，但登入頁面。 不過，本教學課程並不會檢查如何設定網站以支援使用者帳戶。 如需本主題的詳細資訊，請參閱我的[表單驗證、授權、使用者帳戶和角色](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)教學課程。

### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>新增 ContentPlaceHolder 並指定其預設內容

開啟 `Site.master` 主版頁面，並將下列標記新增至 [`DateDisplay` 標籤] 和 [課程] 區段之間的左側資料行：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample4.aspx)]

新增此標記之後，主版頁面的設計檢視看起來應該像 [圖 6]。

[![主版頁面包含登入控制項](multiple-contentplaceholders-and-default-content-vb/_static/image17.png)](multiple-contentplaceholders-and-default-content-vb/_static/image16.png)

**圖 06**：主版頁面包含一個登入控制項（[按一下以查看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image18.png)）

這個 ContentPlaceHolder （`QuickLoginUI`）具有登入 Web 控制項做為其預設內容。 登入控制項會顯示使用者介面，它會提示使用者輸入其使用者名稱和密碼，以及 [登入] 按鈕。 當您按一下 [登入] 按鈕時，Login 控制項會在內部根據成員資格 API 來驗證使用者的認證。 若要在實務中使用此登入控制，您必須將網站設定為使用成員資格。 本主題已超出本教學課程的範圍;如需建立支援使用者帳戶之 web 應用程式的詳細資訊，請參閱我的[表單驗證、授權、使用者帳戶和角色](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)教學課程。

您可以隨意自訂登入控制項的行為或外觀。 我已經設定了兩個屬性： `TitleText` 和 `FailureAction`。 預設為 [登入] 的 `TitleText` 屬性值會顯示在控制項使用者介面的頂端。 我已設定此屬性，使其顯示「登入」文字做為 `<h3>` 元素。 `FailureAction` 屬性指出使用者的認證無效時該怎麼辦。 預設為 `Refresh`的值，這會讓使用者離開相同頁面，並在登入控制項中顯示失敗訊息。 我已將它變更為 `RedirectToLoginPage`，這會在認證無效時將使用者傳送至登入頁面。 我想要在使用者嘗試從其他網頁登入時，將使用者傳送至登入頁面，但卻失敗，因為登入頁面可能包含無法輕易放在左欄中的其他指示和選項。 例如，登入頁面可能包含用來捕獲忘記密碼或建立新帳戶的選項。

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>建立登入頁面並覆寫預設內容

主版頁面完成後，下一個步驟是建立登入頁面。 將 ASP.NET 網頁新增至名為 `Login.aspx`的網站根目錄，並將其系結至 `Site.master` 主版頁面。 這麼做會建立一個具有四個內容控制項的頁面，分別代表 `Site.master`中定義的每個 ContentPlaceHolders。

將登入控制項新增至 `MainContent` 內容控制項。 同樣地，您也可以隨意將任何內容新增至 `LeftColumnContent` 區域。 不過，請務必將 `QuickLoginUI` ContentPlaceHolder 的內容控制項保留空白。 這可確保登入控制項不會出現在登入頁面的左欄中。

定義 `MainContent` 和 `LeftColumnContent` 區域的內容之後，您的登入頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample5.aspx)]

[圖 7] 顯示透過瀏覽器觀看的此頁面。 因為此頁面會指定 `QuickLoginUI` ContentPlaceHolder 的內容控制項，所以會覆寫主版頁面中指定的預設內容。 最後的結果是主頁面的設計檢視中顯示的登入控制項（請參閱 [圖 6]）不會在此頁面中呈現。

[![登入頁面 Represses QuickLoginUI ContentPlaceHolder 的預設內容](multiple-contentplaceholders-and-default-content-vb/_static/image20.png)](multiple-contentplaceholders-and-default-content-vb/_static/image19.png)

**圖 07**：登入頁面會 Represses `QuickLoginUI` ContentPlaceHolder 的預設內容（[按一下以查看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image21.png)）

### <a name="using-the-default-content-in-new-pages"></a>使用新頁面中的預設內容

我們想要針對登入頁面以外的所有頁面，顯示左欄中的 Login 控制項。 為達成此目的，除了登入頁面以外的所有內容頁面，都應省略 `QuickLoginUI` ContentPlaceHolder 的內容控制項。 藉由省略內容控制項，會改為使用 ContentPlaceHolder 的預設內容。

我們現有的內容頁面-`Default.aspx`、`About.aspx`和 `MultipleContentPlaceHolders.aspx`-請勿包含 `QuickLoginUI` 的內容控制項，因為它們是在我們將 ContentPlaceHolder 控制項新增至主版頁面之前建立的。 因此，這些現有的頁面不需要更新。 不過，新增至網站的新頁面預設會包含 `QuickLoginUI` ContentPlaceHolder 的內容控制項。 因此，我們必須記得在每次新增內容頁面時移除這些內容控制項（除非我們想要覆寫 ContentPlaceHolder 的預設內容，如登入頁面的情況）。

若要移除內容控制項，您可以從來源視圖手動刪除其宣告式標記，或從設計檢視中，從其智慧標籤選擇 [預設為主要的內容] 連結。 任一種方法都會從頁面中移除內容控制項，並產生相同的淨效果。

[圖 8] 顯示透過瀏覽器觀看 `Default.aspx`。 回想一下，`Default.aspx` 只有在其宣告式標記中指定了兩個內容控制項-一個用於 `head`，另一個用於 `MainContent`。 因此，會顯示 `LeftColumnContent` 和 `QuickLoginUI` ContentPlaceHolders 的預設內容。

[![顯示 LeftColumnContent 和 QuickLoginUI ContentPlaceHolders 的預設內容](multiple-contentplaceholders-and-default-content-vb/_static/image23.png)](multiple-contentplaceholders-and-default-content-vb/_static/image22.png)

**圖 08**：顯示 `LeftColumnContent` 和 `QuickLoginUI` ContentPlaceHolders 的預設內容（[按一下以觀看完整大小的影像](multiple-contentplaceholders-and-default-content-vb/_static/image24.png)）

## <a name="summary"></a>總結

ASP.NET 主版頁面模型允許在主版頁面中有任意數目的 ContentPlaceHolders。 此外，ContentPlaceHolders 還包含預設內容，這會在內容頁面中沒有對應的內容控制項時發出。 在本教學課程中，我們已瞭解如何將其他 ContentPlaceHolder 控制項包含在主版頁面中，以及如何在新的和現有的 ASP.NET 網頁中定義這些新 ContentPlaceHolders 的內容控制項。 我們也探討了如何在 ContentPlaceHolder 中指定預設內容，這在只有少數幾頁需要在特定區域內自訂標準化內容的案例中很有用。

在下一個教學課程中，我們將更詳細地探討 `head` ContentPlaceHolder，瞭解如何以宣告方式和程式設計方式，逐頁定義標題、中繼標記和其他 HTML 標頭。

快樂的程式設計！

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Suchi Banerjee。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](creating-a-site-wide-layout-using-master-pages-vb.md)
> [下一頁](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)
