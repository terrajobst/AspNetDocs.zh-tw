---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-vb
title: 嵌套主版頁面（VB） |Microsoft Docs
author: rick-anderson
description: 示範如何在另一個主版頁面上嵌套。
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 14d9aa1b-4dca-43a0-aa9d-a6e891fee019
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9bb39712855c37f5cbcbb447f7691e9451b8dc92
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642090"
---
# <a name="nested-master-pages-vb"></a>巢狀主版頁面 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_VB.zip)或[下載 PDF](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_VB.pdf)

> 示範如何在另一個主版頁面上嵌套。

## <a name="introduction"></a>簡介

在過去九個教學課程中，我們已瞭解如何使用主版頁面來執行全網站的版面配置。 簡言之，主版頁面可讓我們（網頁開發人員）在主版頁面中定義一般標記，以及在內容頁面上依據內容頁面自訂的特定區域。 主版頁面中的 ContentPlaceHolder 控制項指出可自訂的區域;ContentPlaceHolder 控制項的自訂標記會透過內容控制項在內容頁面中定義。

如果您在整個網站上使用單一版面配置，我們目前所探索到的主版頁面技術就很好用。 不過，許多大型網站的網站版面配置會在各種不同的區段中進行自訂。 例如，請考慮醫院員工用來管理患者資訊、活動和帳單的醫療保健應用程式。 在此應用程式中，可能會有三種類型的網頁：

- 員工成員的特定頁面，員工可以在其中更新可用性、查看排程或要求假期時間。
- 員工成員可在其中查看或編輯特定患者資訊的患者特定頁面。
- 會計審查目前理賠狀態和財務報告的計費特定頁面。

每個頁面都可能共用一般的版面配置，例如橫跨頂端的功能表，以及底部的一系列常用的連結。 但員工-、患者和計費特定頁面可能需要自訂此一般版面配置。 例如，可能所有的員工專屬頁面都應該包含行事曆和工作清單，以顯示目前登入的使用者可用性和每日排程。 可能所有的患者特定頁面都需要顯示其資訊正在編輯之患者的名稱、位址和保險資訊。

您可以使用*嵌套主版頁面*來建立這類自訂的版面配置。 若要執行上述案例，我們首先要建立一個主版頁面，定義網站範圍的版面配置、功能表和頁尾內容，以及定義可自訂區域的 ContentPlaceHolders。 接著，我們會建立三個嵌套的主版頁面，每個網頁類型各一個。 每個嵌套的主版頁面都會定義使用主版頁面的內容頁面類型之間的內容。 換句話說，適用于患者特定內容頁面的嵌套主版頁面會包含標記和程式設計邏輯，以顯示所編輯之患者的相關資訊。 在建立新的患者特定頁面時，我們會將它系結到這個嵌套的主版頁面。

本教學課程一開始會強調嵌套主版頁面的優點。 接著，它會示範如何建立和使用嵌套主版頁面。

> [!NOTE]
> 從2.0 版的 .NET Framework 開始可能會有嵌套的主版頁面。 不過，Visual Studio 2005 並未包含針對嵌套主版頁面的設計階段支援。 好消息是，Visual Studio 2008 針對嵌套主版頁面提供了豐富的設計階段體驗。 如果您有興趣使用嵌套的主版頁面，但仍在使用 Visual Studio 2005，請查看[Scott Guthrie](https://weblogs.asp.net/scottgu/)的 blog 專案，這是[在 VS 2005 設計階段中嵌套主版頁面的秘訣](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)。

## <a name="the-benefits-of-nested-master-pages"></a>嵌套主版頁面的優點

許多網站的網站設計，以及特定頁面類型特有的自訂設計都有。 比方說，在我們的示範 web 應用程式中，我們建立了一個基本的管理區段（`~/Admin` 資料夾中的頁面）。 [`~/Admin`] 資料夾中的網頁目前使用的主版頁面與不在 [系統管理] 區段中的頁面（也就是 `Site.master` 或 `Alternate.master`，視使用者的選擇而定）。

> [!NOTE]
> 現在，假設我們的網站只有一個主版頁面，`Site.master`。 我們將在本教學課程稍後的使用 [管理] 區段中的 [使用嵌套的主版頁面] 開頭的兩個（或多個）主版頁面中，使用嵌套主版頁面來處理。

假設我們要求您自訂管理頁面的版面配置，以包含其他資訊或網站中其他頁面不會顯示的連結。 有四種方法可實行這項需求：

1. 手動將管理特定的資訊和連結新增至 `~/Admin` 資料夾中的每個內容頁面。
2. 更新 `Site.master` 主版頁面以包含管理區段特定的資訊和連結，然後將程式碼新增至主版頁面，根據是否正在流覽其中一個管理頁面來顯示或隱藏這些區段。
3. 特別針對 [系統管理] 區段建立新的主版頁面、[從 `Site.master`複製標記]、新增 [管理] 區段特定的資訊和連結，然後更新 [`~/Admin`] 資料夾中的 [內容] 頁面，以使用此新的主版頁面。
4. 建立系結至 `Site.master` 的嵌套主版頁面，並讓 `~/Admin` 資料夾中的內容頁使用這個新的嵌套主版頁面。 這個嵌套的主版頁面只會包含系統管理頁面的其他資訊和連結，而且不需要重複已在 `Site.master`中定義的標記。

第一個選項是最少的可行。 使用主版頁面的重點在於，您必須手動將一般標記複製並貼到新的 ASP.NET 網頁。 第二個選項是可接受的，但可讓應用程式的維護變得較少，因為它會以僅偶爾顯示的標記 bulks 主版頁面，而且需要開發人員編輯主版頁面以解決此標記，而且必須記住何時，確切地，會顯示特定標記，而不是隱藏。 這種方法比較不 tenable，因為自訂更多類型的網頁需要此單一主版頁面。

第三個選項會移除使用第二個選項所呈現的雜亂和複雜性問題。 不過，第三個主要缺點是，它需要我們將一般版面配置從 `Site.master` 複製並貼到新的管理區段特定的主版頁面。 如果稍後決定變更全網站的版面配置，我們必須記得在兩個地方進行變更。

第四個選項 [嵌套主版頁面] 提供了第二個和第三個選項的最佳選擇。 全網站的版面配置資訊會保留在一個檔案中，也就是最上層主版頁面，而特定區域特定的內容則會分成不同的檔案。

本教學課程一開始會介紹如何建立和使用簡單的嵌套主版頁面。 我們會建立全新的頂層主版頁面、兩個嵌套主版頁面，以及兩個內容頁面。 從「使用適用于系統管理的內嵌主版頁面」一節，我們將探討如何更新現有的主版頁面架構，以包含使用嵌套主版頁面。 具體而言，我們會建立一個嵌套的主版頁面，並用它在 [`~/Admin`] 資料夾中包含內容頁面的其他自訂內容。

## <a name="step-1-creating-a-simple-top-level-master-page"></a>步驟1：建立簡單的頂層主版頁面

根據其中一個現有的主版頁面建立嵌套的主要頁面，然後將現有的內容頁更新為使用這個新的嵌套主版頁面，而不是最上層的主版頁面，因為現有的內容頁已經預期在最上層主版頁面中定義的 ContentPlaceHolder 控制項。 因此，嵌套主版頁面也必須包含具有相同名稱的相同 ContentPlaceHolder 控制項。 此外，我們的特定示範應用程式會根據使用者的喜好設定，以動態方式指派給內容頁面的兩個主版頁面（`Site.master` 和 `Alternate.master`），這會進一步增加這種複雜性。 我們將在本教學課程稍後的更新現有的應用程式以使用嵌套主版頁面，但讓我們先專注于簡單的嵌套主版頁面範例。

建立名為 `NestedMasterPages` 的新資料夾，然後將新的主版分頁檔新增至名為 `Simple.master`的資料夾。 （請參閱 [圖 1]，以取得在新增這個資料夾和檔案之後，方案總管的螢幕擷取畫面）。將 `AlternateStyles.css` 樣式表單檔案從方案總管拖曳到設計工具上。 這樣會將 `<link>` 專案加入至 `<head>` 元素中的樣式表單檔案，在此之後，主版頁面的 `<head>` 元素的標記看起來應該像這樣：

[!code-aspx[Main](nested-master-pages-vb/samples/sample1.aspx)]

接下來，在 `Simple.master`的 Web 表單中新增下列標記：

[!code-aspx[Main](nested-master-pages-vb/samples/sample2.aspx)]

此標記會顯示標題為「嵌套主版頁面（簡單）」的連結，其位於頁面頂端的海軍藍背景上的大白色字型。 底下是 `MainContent` ContentPlaceHolder。 [圖 1] 顯示在 Visual Studio 設計工具中載入時的 `Simple.master` 主版頁面。

[![嵌套的主版頁面定義 [管理] 區段中頁面的特定內容](nested-master-pages-vb/_static/image2.png)](nested-master-pages-vb/_static/image1.png)

**圖 01**：嵌套的主版頁面定義 [系統管理] 區段中頁面的特定內容（[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image3.png)）

## <a name="step-2-creating-a-simple-nested-master-page"></a>步驟2：建立簡單的嵌套主版頁面

`Simple.master` 包含兩個 ContentPlaceHolder 控制項：我們在 Web 表單中新增的 `MainContent` ContentPlaceHolder，以及 `<head>` 元素中的 `head` ContentPlaceHolder。 如果我們要建立內容頁面，並將它系結至 `Simple.master` [內容] 頁面會有兩個參考這兩個 ContentPlaceHolders 的內容控制項。 同樣地，如果我們建立一個嵌套的主版頁面，並將它系結至 `Simple.master` 則嵌套的主版頁面會有兩個內容控制項。

讓我們將新的嵌套主版頁面新增至名為 `SimpleNested.master`的 `NestedMasterPages` 資料夾。 以滑鼠右鍵按一下 [`NestedMasterPages`] 資料夾，然後選擇 [加入新專案]。 這會顯示 [圖 2] 所示的 [新增專案] 對話方塊。 選取主版頁面範本類型，並輸入新主版頁面的名稱。 若要指出新的主版頁面應該是嵌套的主版頁面，請核取 [選取主版頁面] 核取方塊。

接下來，按一下 [新增] 按鈕。 這會顯示將內容頁系結至主版頁面時，所看到的相同 [選取主版頁面] 對話方塊（請參閱 [圖 3]）。 選擇 [`NestedMasterPages`] 資料夾中的 [`Simple.master` 主版] 頁面，然後按一下 [確定]。

> [!NOTE]
> 如果您使用 Web 應用程式專案模型（而不是網站專案模型）來建立 ASP.NET 網站，則 [圖 2] 所示的 [新增專案] 對話方塊中不會顯示 [選取主版頁面] 核取方塊。 若要在使用 Web 應用程式專案模型時建立嵌套主版頁面，您必須選擇 [嵌套的主版頁面] 範本（而不是 [主版頁面] 範本）。 選取嵌套的主版頁面範本並按一下 [新增] 之後，[圖 3] 所示的 [選取主版頁面] 對話方塊隨即出現。

[![檢查 &quot;選取 [主版頁面]&quot; 核取方塊以新增嵌套的主版頁面](nested-master-pages-vb/_static/image5.png)](nested-master-pages-vb/_static/image4.png)

**圖 02**：核取 [選取主版頁面] 核取方塊以新增嵌套的主版頁面（[按一下以觀看完整大小的影像](nested-master-pages-vb/_static/image6.png)）

[![將嵌套的主版頁面系結至簡單的主要主版頁面](nested-master-pages-vb/_static/image8.png)](nested-master-pages-vb/_static/image7.png)

**圖 03**：將嵌套的主版頁面系結至 `Simple.master` 主版頁面（[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image9.png)）

如下所示，嵌套主版頁面的宣告式標記包含兩個內容控制項，其中參考最上層主版頁面的兩個 ContentPlaceHolder 控制項。

[!code-aspx[Main](nested-master-pages-vb/samples/sample3.aspx)]

除了 `<%@ Master %>` 指示詞之外，嵌套主版頁面的初始宣告式標記與將內容頁系結至相同的最上層主版頁面時一開始產生的標記相同。 如同內容頁的 `<%@ Page %>` 指示詞，這裡的 `<%@ Master %>` 指示詞包含一個 `MasterPageFile` 屬性，可指定嵌套主版頁面的父主版頁面。 嵌套主版頁面和系結至相同頂層主版頁面的內容頁面之間的主要差異在於，嵌套主版頁面可以包含 ContentPlaceHolder 控制項。 嵌套主版頁面的 ContentPlaceHolder 控制項會定義內容頁面可以自訂標記的區域。

更新此嵌套的主版頁面，使其顯示 "Hello，from SimpleNested！" 文字 在對應至 `MainContent` ContentPlaceHolder 控制項的內容控制項中。

[!code-aspx[Main](nested-master-pages-vb/samples/sample4.aspx)]

進行這種新增之後，請儲存嵌套的主版頁面，然後將新的內容頁面新增至名為 `Default.aspx`的 `NestedMasterPages` 資料夾，並將它系結至 `SimpleNested.master` 主版頁面。 新增此頁面時，您可能會很驚訝地發現它沒有包含任何內容控制項（請參閱 [圖 4]）！ 內容頁面只能存取其*父*主版頁面的 ContentPlaceHolders。 `SimpleNested.master` 不包含任何 ContentPlaceHolder 控制項;因此，系結至此主版頁面的任何內容頁面都不能包含任何內容控制項。

[![[新增內容] 頁面未包含內容控制項](nested-master-pages-vb/_static/image11.png)](nested-master-pages-vb/_static/image10.png)

**圖 04**： [新增內容] 頁面未包含內容控制項（[按一下以觀看完整大小的影像](nested-master-pages-vb/_static/image12.png)）

我們需要更新嵌套主版頁面（`SimpleNested.master`），以包含 ContentPlaceHolder 控制項。 一般來說，您會希望您的嵌套主版頁面包含其父主版頁面所定義之每個 ContentPlaceHolder 的 ContentPlaceHolder，藉此允許其子主版頁面或內容頁使用任何頂層主版頁面的 ContentPlaceHoldercontrols.

更新 `SimpleNested.master` 主版頁面，以在其兩個內容控制項中包含 ContentPlaceHolder。 提供 ContentPlaceHolder 控制項與內容控制項所參考之 ContentPlaceHolder 控制項相同的名稱。 也就是在 `SimpleNested.master` 中，將名為 `MainContent` 的 ContentPlaceHolder 控制項新增至參考 `Simple.master`中 `MainContent` ContentPlaceHolder 的內容控制項。 在參考 `head` ContentPlaceHolder 的內容控制項中執行相同的動作。

> [!NOTE]
> 雖然我建議將嵌套主版頁面中的 ContentPlaceHolder 控制項命名為與頂層主版頁面中的 ContentPlaceHolders 相同，但不需要此命名對稱。 您可以用您喜歡的任何名稱，在您的嵌套主版頁面中提供 ContentPlaceHolder 控制項。 不過，如果我的頂層主版頁面和嵌套主版頁面使用相同的名稱，我覺得比較容易記住，ContentPlaceHolders 會與頁面的哪些區域相對應。

新增這些專案之後，您 `SimpleNested.master` 主版頁面的宣告式標記看起來應該像下面這樣：

[!code-aspx[Main](nested-master-pages-vb/samples/sample5.aspx)]

刪除剛建立的 `Default.aspx` 內容頁面，然後將它重新加入，並將它系結至 `SimpleNested.master` 主版頁面。 這次 Visual Studio 會將兩個內容控制項新增至 `Default.aspx`，並參考目前在 `SimpleNested.master` 中定義的 ContentPlaceHolders （請參閱 [圖 6]）。 加入文字 "Hello，from default.aspx！" 在 `MainContent`參考的內容控制項中。

[圖 5] 顯示這裡所牽涉到的三個實體-`Simple.master`、`SimpleNested.master`和 `Default.aspx`，以及它們彼此之間的關聯性。 如圖所示，嵌套的主版頁面會執行其父系 ContentPlaceHolder 的內容控制項。 如果這些區域需要可供 [內容] 頁面存取，則嵌套的主版頁面必須將自己的 ContentPlaceHolders 新增至內容控制項。

[![最上層和嵌套主版頁面，指示內容頁面的版面配置](nested-master-pages-vb/_static/image14.png)](nested-master-pages-vb/_static/image13.png)

**圖 05**：最上層和嵌套主版頁面會指示內容頁面的版面配置（[按一下以觀看完整大小的影像](nested-master-pages-vb/_static/image15.png)）

此行為說明內容頁或主版頁面只 cognizant 其父主版頁面的方式。 Visual Studio 的設計工具也會指出這個行為。 [圖 6] 顯示 `Default.aspx`的設計工具。 雖然設計工具清楚地顯示可從 [內容] 頁面編輯哪些區域，以及哪些部分不存在，但它並不會區分哪些不可編輯的區域是來自于嵌套的主版頁面，以及哪些地區是來自最上層主版頁面。

[![[內容] 頁面現在包含已嵌套主版頁面 ContentPlaceHolders 的內容控制項](nested-master-pages-vb/_static/image17.png)](nested-master-pages-vb/_static/image16.png)

**圖 06**： [內容] 頁面現在包含嵌套主版頁面 ContentPlaceHolders 的內容控制項（[按一下以觀看完整大小的影像](nested-master-pages-vb/_static/image18.png)）

## <a name="step-3-adding-a-second-simple-nested-master-page"></a>步驟3：新增第二個簡單的嵌套主版頁面

當有多個嵌套主版頁面時，嵌套主版頁面的優點較明顯。 為了說明這項優點，請在 [`NestedMasterPages`] 資料夾中建立另一個嵌套的主版頁面;將這個新的嵌套主版頁面命名為 `SimpleNestedAlternate.master`，並將它系結至 `Simple.master` 主版頁面。 在嵌套主版頁面的兩個內容控制項中新增 ContentPlaceHolder 控制項，就像我們在步驟2中所做的一樣。 同時新增 "Hello，from SimpleNestedAlternate！" 文字 在對應至頂層主版頁面的內容控制項中，`MainContent` ContentPlaceHolder。 進行這些變更之後，新的嵌套主版頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](nested-master-pages-vb/samples/sample6.aspx)]

在 `NestedMasterPages` 資料夾中建立名為 `Alternate.aspx` 的內容頁面，並將它系結至 `SimpleNestedAlternate.master` 的嵌套主版頁面。 新增 "Hello，from 替代！" 文字 在對應至 `MainContent`的內容控制項中。 [圖 7] 顯示透過 Visual Studio 設計工具觀看 `Alternate.aspx`。

[![的 default.aspx 會系結至 SimpleNestedAlternate 主版頁面](nested-master-pages-vb/_static/image20.png)](nested-master-pages-vb/_static/image19.png)

**圖 07**： `Alternate.aspx` 系結至 `SimpleNestedAlternate.master` 主版頁面（[按一下以觀看完整大小的影像](nested-master-pages-vb/_static/image21.png)）

將 [圖 7] 中的設計工具與 [圖 6] 中的設計工具做比較。 這兩個內容頁面共用最上層主版頁面（`Simple.master`）中所定義的相同配置，也就是「嵌套主版頁面教學課程（簡單）」標題。 同時在其父主版頁面中定義了不同的內容，也就是 "Hello，from SimpleNested！" 在 [圖 6] 和 "Hello，from SimpleNestedAlternate！" 如 [圖 7] 所示。 不過，這裡的差異很簡單，但您可以擴充此範例，以包含更有意義的差異。 例如，`SimpleNested.master` 頁面可能會包含一個功能表，其中包含其內容頁面特有的選項，而 `SimpleNestedAlternate.master` 可能會有與系結至它的內容頁面相關的資訊。

現在，假設我們需要變更整體的網站版面配置。 例如，假設我們想要將通用連結清單新增至所有內容頁面。 為了達到此目的，我們會更新頂層主版頁面，`Simple.master`。 任何變更都會立即反映在其嵌套主版頁面中，並依擴充功能的內容頁面。

為了示範我們可以變更主要網站版面配置的便利性，請開啟 `Simple.master` 主版頁面，並在 `topContent` 和 `mainContent` `<div>` 專案之間新增下列標記：

[!code-aspx[Main](nested-master-pages-vb/samples/sample7.aspx)]

這會在系結至 `Simple.master`、`SimpleNested.master`或 `SimpleNestedAlternate.master`的每個頁面頂端加上兩個連結。這些變更會立即套用至所有的嵌套主版頁面及其內容頁面。 [圖 8] 顯示透過瀏覽器觀看 `Alternate.aspx`。 請注意，在頁面頂端新增連結（相較于 [圖 7]）。

[![變更為頂層主版頁面，會立即反映在其嵌套主版頁面及其內容頁面中](nested-master-pages-vb/_static/image23.png)](nested-master-pages-vb/_static/image22.png)

**圖 08**：變更為最上層主版頁面會立即反映在其嵌套主版頁面及其內容頁面中（[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image24.png)）

## <a name="using-a-nested-master-page-for-the-administration-section"></a>使用系統管理區段的嵌套主版頁面

此時，我們已經探討了嵌套主版頁面的優點，並瞭解如何在 ASP.NET 應用程式中建立和使用它們。 不過，步驟1、2和3中的範例牽涉到建立新的最上層主版頁面、新的嵌套主版頁面，以及新的內容頁面。 如何使用現有的最上層主版頁面和內容頁面，將新的嵌套主版頁面新增至網站？

將嵌套的主版頁面整合到現有的網站，並將它與現有的內容頁面建立關聯，需要比從頭開始的工作還多。 步驟4、5、6和7會探索這些挑戰，因為我們會擴充我們的示範應用程式，以包含名為 `AdminNested.master` 的新的嵌套主版頁面，其中包含系統管理員的指示，並由 `~/Admin` 資料夾中的 ASP.NET 網頁使用。

將嵌套的主版頁面整合到示範應用程式中，會帶來下列障礙：

- [`~/Admin`] 資料夾中的現有內容頁面，會有其主版頁面的特定期望。 對於初學者來說，他們預期會出現某些 ContentPlaceHolder 控制項。 此外，`~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx` 頁面會呼叫主版頁面的公用 `RefreshRecentProductsGrid` 方法、設定其 `GridMessageText` 屬性，或具有其 `PricesDoubled` 事件的事件處理常式。 因此，我們的嵌套主版頁面必須提供相同的 ContentPlaceHolders 和 public 成員。
- 在先前的教學課程中，我們增強了 `BasePage` 類別，以根據會話變數動態設定 `Page` 物件的 `MasterPageFile` 屬性。 如何在使用嵌套主版頁面時支援動態主版頁面？

這兩個挑戰會在我們建立嵌套的主版頁面時呈現，並從現有的內容頁面加以使用。 我們會在這些問題發生時加以調查並加以克服。

## <a name="step-4-creating-the-nested-master-page"></a>步驟4：建立嵌套的主版頁面

我們的第一項工作是建立可供 [管理] 區段中的頁面使用的嵌套主版頁面。 如我們在步驟2所見，加入新的嵌套主版頁面時，我們必須指定嵌套主版頁面的父主版頁面。 但我們有兩個最上層主版頁面： `Site.master` 和 `Alternate.master`。 回想一下，我們已在先前的教學課程中建立 `Alternate.master`，並在 `BasePage` 類別中撰寫程式碼，在執行時間將 `Page` 物件的 `MasterPageFile` 屬性設定為 `Site.master` 或 `Alternate.master` （視 `MyMasterPage` 會話變數的值而定）。

如何設定我們的嵌套主版頁面，使其使用適當的頂層主版頁面？ 我們有兩個選項：

- 建立兩個嵌套的主版頁面，`AdminNestedSite.master` 和 `AdminNestedAlternate.master`，並分別將它們系結至頂層主版頁面 `Site.master` 和 `Alternate.master`。 在 `BasePage`中，我們會將 `Page` 物件的 `MasterPageFile` 設定為適當的嵌套主版頁面。
- 建立單一的嵌套主版頁面，並讓內容頁面使用這個特定的主版頁面。 然後，在執行時間，我們需要在執行時間將嵌套主版頁面的 `MasterPageFile` 屬性設定為適當的頂層主版頁面。 （您可能已經知道，主版頁面也有 `MasterPageFile` 的屬性）。

讓我們使用第二個選項。 在名為 `AdminNested.master`的 `~/Admin` 資料夾中，建立單一的嵌套主版分頁檔。 由於 `Site.master` 和 `Alternate.master` 都有相同的 ContentPlaceHolder 控制項集合，雖然我建議您將它系結至 `Site.master` 以求一致。

[![將嵌套的主版頁面新增至 ~/Admin 資料夾。](nested-master-pages-vb/_static/image26.png)](nested-master-pages-vb/_static/image25.png)

**圖 09**：將嵌套的主版頁面新增至 `~/Admin` 資料夾。 （[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image27.png)）

因為嵌套的主版頁面會系結至具有四個 ContentPlaceHolder 控制項的主版頁面，Visual Studio 將四個內容控制項加入至新的嵌套主版頁面檔案的初始標記中。 就像我們在步驟2和3中所做的一樣，在每個內容控制項中新增 ContentPlaceHolder 控制項，並提供與最上層主版頁面 ContentPlaceHolder 控制項相同的名稱。 此外，將下列標記新增至對應至 `MainContent` ContentPlaceHolder 的內容控制項：

[!code-html[Main](nested-master-pages-vb/samples/sample8.html)]

接下來，在 `Styles.css` 和 `AlternateStyles.css` CSS 檔案中定義 `instructions` CSS 類別。 下列 CSS 規則會導致以淺黃色背景色彩和黑色實心框線顯示樣式為 `instructions` 類別的 HTML 專案：

[!code-css[Main](nested-master-pages-vb/samples/sample9.css)]

由於此標記已新增至嵌套的主版頁面，因此它只會出現在使用此嵌套主版頁面的頁面中（也就是 [管理] 區段中的頁面）。

將這些專案新增至您的嵌套主版頁面之後，其宣告式標記看起來應該如下所示：

[!code-aspx[Main](nested-master-pages-vb/samples/sample10.aspx)]

請注意，每個內容控制項都有一個 ContentPlaceHolder 控制項，而且 ContentPlaceHolder 控制項的 `ID` 屬性會被指派與頂層主版頁面中對應的 ContentPlaceHolder 控制項相同的值。 此外，[管理] 區段特定標記會出現在 [`MainContent`] ContentPlaceHolder 中。

[圖 10] 顯示透過 Visual Studio 的設計工具觀看時，`AdminNested.master` 的嵌套主版頁面。 您可以在 `MainContent` 內容控制項頂端的黃色方塊中查看指示。

[![嵌套的主版頁面延伸頂層主版頁面，以包含系統管理員的指示。](nested-master-pages-vb/_static/image29.png)](nested-master-pages-vb/_static/image28.png)

**圖 10**：此嵌套主版頁面會擴充最上層主版頁面，以包含系統管理員的指示。 （[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image30.png)）

## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>步驟5：更新現有的內容頁面以使用新的嵌套主版頁面

每當我們將新的內容頁新增至 [管理] 區段時，我們需要將它系結到剛才建立的 `AdminNested.master` 主版頁面。 但是現有的內容頁面呢？ 目前，網站中的所有內容頁都是衍生自 `BasePage` 類別，它會在執行時間以程式設計方式設定內容頁面的主版頁面。 這不是我們想要用於 [管理] 區段中的內容頁面的行為。 相反地，我們希望這些內容頁一律使用 [`AdminNested.master`] 頁面。 這會負責在執行時間選擇正確的最上層內容頁面。

若要達到此所需行為的最佳方式，就是建立新的自訂基底頁面類別，名為 `AdminBasePage` 以擴充 `BasePage` 類別。 `AdminBasePage` 可以接著覆寫 `SetMasterPageFile`，並將 `Page` 物件的 `MasterPageFile` 設定為硬式編碼值 "~/Admin/AdminNested.master"。 如此一來，衍生自 `AdminBasePage` 的任何頁面都會使用 `AdminNested.master`，而衍生自 `BasePage` 的任何頁面，都會根據 `MyMasterPage` 會話變數的值，將其 `MasterPageFile` 屬性動態設定為 "~/Site.master" 或 "~/Alternate.master"。

首先，將新的類別檔案新增至名為 `AdminBasePage.vb`的 `App_Code` 資料夾。 讓 `AdminBasePage` 擴充 `BasePage`，然後覆寫 `SetMasterPageFile` 方法。 在該方法中，請將值指派給 `MasterPageFile` "~/Admin/AdminNested.master"。 進行這些變更之後，您的類別檔案看起來應該如下所示：

[!code-vb[Main](nested-master-pages-vb/samples/sample11.vb)]

我們現在必須讓 [系統管理] 區段中的現有內容頁面衍生自 `AdminBasePage`，而不是 `BasePage`。 移至 [`~/Admin`] 資料夾中每個內容頁面的程式碼後置類別檔案，並進行這項變更。 例如，在 `~/Admin/Default.aspx` 您會變更程式碼後置類別宣告，從：

[!code-vb[Main](nested-master-pages-vb/samples/sample12.vb)]

收件者：

[!code-vb[Main](nested-master-pages-vb/samples/sample13.vb)]

[圖 11] 說明頂層主版頁面（`Site.master` 或 `Alternate.master`）、嵌套主版頁面（`AdminNested.master`），以及管理區段內容頁面彼此之間的關聯性。

[![嵌套的主版頁面定義 [管理] 區段中頁面的特定內容](nested-master-pages-vb/_static/image32.png)](nested-master-pages-vb/_static/image31.png)

**圖 11**：嵌套的主版頁面定義 [系統管理] 區段中頁面的特定內容（[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image33.png)）

## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>步驟6：鏡像主版頁面的公用方法與屬性

回想一下，`~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx` 頁面會以程式設計方式與主版頁面互動： `~/Admin/AddProduct.aspx` 會呼叫主版頁面的公用 `RefreshRecentProductsGrid` 方法，並設定其 `GridMessageText` 屬性。`~/Admin/Products.aspx` 具有 `PricesDoubled` 事件的事件處理常式。 在先前的教學課程中，我們建立了定義這些公用成員的 `MustInherit` `BaseMasterPage` 類別。

[`~/Admin/AddProduct.aspx`] 和 [`~/Admin/Products.aspx`] 頁面會假設其主版頁面衍生自 `BaseMasterPage` 類別。 不過，[`AdminNested.master`] 頁面目前會擴充 `System.Web.UI.MasterPage` 類別。 如此一來，當造訪 `~/Admin/Products.aspx` 會擲回 `InvalidCastException` 一則訊息：「無法將類型為 ' ASP. admin\_adminnested\_master ' 的物件轉型為 ' BaseMasterPage '」。

若要修正此問題，我們必須將 `AdminNested.master` 程式碼後置類別延伸 `BaseMasterPage`。 從下列內容更新嵌套主版頁面的程式碼後置類別宣告：

[!code-vb[Main](nested-master-pages-vb/samples/sample14.vb)]

收件者：

[!code-vb[Main](nested-master-pages-vb/samples/sample15.vb)]

我們尚未完成。 我們需要覆寫標示為 `MustOverride`的成員，亦即 `RefreshRecentProductsGrid` 和 `GridMessageText`。 這些成員是由最上層主版頁面用來更新其使用者介面。 （實際上，只有 `Site.master` 主版頁面會使用這些方法，雖然兩個最上層主版頁面都會執行這些方法，因為兩者都是擴充 `BaseMasterPage`）。

雖然我們需要在 `AdminNested.master`中執行這些成員，但這些所有的實作為只需要在嵌套主版頁面所使用的最上層主版頁面中呼叫相同的成員。 例如，當 [管理] 區段中的 [內容] 頁面呼叫了嵌套主版頁面的 `RefreshRecentProductsGrid` 方法時，所有的嵌套主版頁面都必須執行，然後再呼叫 `Site.master` 或 `Alternate.master`的 `RefreshRecentProductsGrid` 方法。

若要達到此目的，請從將下列 `@MasterType` 指示詞新增至 `AdminNested.master`頂端開始：

[!code-aspx[Main](nested-master-pages-vb/samples/sample16.aspx)]

回想一下，`@MasterType` 指示詞會將強型別屬性加入名為 `Master`的程式碼後置類別。 然後覆寫 `RefreshRecentProductsGrid` 和 `GridMessageText` 成員，直接將呼叫委派給 `Master`的對應方法：

[!code-vb[Main](nested-master-pages-vb/samples/sample17.vb)]

備妥此程式碼之後，您應該能夠造訪並使用 [系統管理] 區段中的內容頁面。 [圖 12] 顯示透過瀏覽器觀看時的 `~/Admin/Products.aspx` 頁面。 如您所見，此頁面包含 [系統管理指示] 方塊，此方塊定義于嵌套的主版頁面中。

[![[管理] 區段中的內容頁麵包含每個頁面頂端的指示](nested-master-pages-vb/_static/image35.png)](nested-master-pages-vb/_static/image34.png)

**圖 12**： [管理] 區段中的 [內容] 頁面包含每個頁面頂端的指示（[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image36.png)）

## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>步驟7：在執行時間使用適當的最上層主版頁面

雖然 [管理] 區段中的所有 [內容] 頁面都有完整的功能，但它們全都使用相同的最上層主版頁面，並忽略使用者在 `ChooseMasterPage.aspx`選取的主版頁面。 此行為的原因是，嵌套主版頁面的 `MasterPageFile` 屬性會在其 `<%@ Master %>` 指示詞中以靜態方式設定為 `Site.master`。

若要使用使用者選取的最上層主版頁面，我們必須將 `AdminNested.master`的 `MasterPageFile` 屬性設定為 `MyMasterPage` 會話變數中的值。 因為我們會在 `BasePage`中設定內容頁的 `MasterPageFile` 屬性，所以您可能會想要在 `BaseMasterPage` 或 `AdminNested.master`的程式碼後置類別中，設定嵌套主版頁面的 `MasterPageFile` 屬性。 不過，這樣做並不可行，因為我們必須在 PreInit 階段結束時設定 `MasterPageFile` 屬性。 我們可以用程式設計的方式，從主版頁面進入頁面生命週期的最早時間是 Init 階段（發生在 PreInit 階段之後）。

因此，我們需要從 [內容] 頁面設定嵌套主版頁面的 [`MasterPageFile`] 屬性。 唯一使用 `AdminNested.master` 主版頁面的內容頁面會衍生自 `AdminBasePage`。 因此，我們可以將這個邏輯放在該處。 在步驟5中，我們會已覆寫 `SetMasterPageFile` 方法，將 Page 物件的 `MasterPageFile` 屬性設定為 "~/Admin/AdminNested.master"。 更新 `SetMasterPageFile`，同時將主版頁面的 `MasterPageFile` 屬性設定為儲存在會話中的結果：

[!code-vb[Main](nested-master-pages-vb/samples/sample18.vb)]

我們在上一個教學課程中新增至 `BasePage` 類別的 `GetMasterPageFileFromSession` 方法，會根據會話變數值傳回適當的主版頁面檔案路徑。

進行這項變更之後，使用者的主版頁面選取範圍會移至 [管理] 區段。 [圖 13] 顯示的頁面與 [圖 12] 相同，但在使用者將主版頁面選取範圍變更為 `Alternate.master`之後。

[![[嵌套管理] 頁面使用使用者選取的最上層主版頁面](nested-master-pages-vb/_static/image38.png)](nested-master-pages-vb/_static/image37.png)

**圖 13**： [嵌套管理] 頁面使用使用者選取的最上層主版頁面（[按一下以查看完整大小的影像](nested-master-pages-vb/_static/image39.png)）

## <a name="summary"></a>總結

與內容頁面系結至主版頁面的方式很類似，您可以將子主版頁面系結至父主版頁面，以建立嵌套的主版頁面。 子主版頁面可能會定義其父系 ContentPlaceHolders 的內容控制項;然後，它可以將自己的 ContentPlaceHolder 控制項（以及其他標記）新增至這些內容控制項。 在所有頁面都共用整體外觀和操作的大型 web 應用程式中，嵌套主版頁面相當有用，但網站的某些區段則需要唯一的自訂專案。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [嵌套的 ASP.NET 主版頁面](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [嵌套主版頁面和 VS 2005 設計階段的秘訣](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 的嵌套主版頁面支援](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一篇](specifying-the-master-page-programmatically-vb.md)
