---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
title: 使用主版頁面建立全網站的版面配置（VB） |Microsoft Docs
author: rick-anderson
description: 本教學課程將顯示主版頁面的基本概念。 也就是說，什麼是主版頁面、如何建立主版頁面、什麼是內容預留位置，還有一個 cr 。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 30945276-8ed9-4b27-8e50-4309244d3559
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: c0ee6ed9d944b9a8ff2b2996e93706b8416de905
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639262"
---
# <a name="creating-a-site-wide-layout-using-master-pages-vb"></a>使用主版頁面建立全網站的版面配置 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_VB.zip)或[下載 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_VB.pdf)

> 本教學課程將顯示主版頁面的基本概念。 也就是說，什麼是主版頁面、如何建立主版頁面、什麼是內容預留位置、如何建立使用主版頁面的 ASP.NET 網頁、修改主版頁面如何自動反映在相關聯的內容頁面等等。

## <a name="introduction"></a>簡介

設計良好的網站的其中一個屬性是一致的全網站頁面配置。 例如，取得 www.asp.net 網站。 在撰寫本文時，每個頁面在頁面的頂端和底部都有相同的內容。 如 [圖 1] 所示，每個頁面的最上方會顯示一個含有 Microsoft 社區清單的灰色列。 其下是網站標誌、網站轉譯的語言清單，以及核心區段：首頁、開始使用、學習、下載等等。 同樣地，頁面底部也會包含有關 www.asp.net 廣告、著作權聲明和隱私權聲明連結的資訊。

[![www.asp.net 網站在所有頁面上都採用一致的外觀與風格](creating-a-site-wide-layout-using-master-pages-vb/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image1.png)

<strong>圖 01</strong>： www.asp.net 網站在所有頁面上都採用一致的外觀與風格（[按一下以觀看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image3.png)）

設計良好的網站的另一個屬性，就是網站外觀可以變更的便利性。 [圖 1] 顯示從2008年3月起的 www.asp.net 首頁，但現在和本教學課程的發行版本之間，外觀與風格可能已變更。 或許頂端的功能表項目會展開以包含 MVC 架構的新區段。 或者，可能會揭曉具有不同色彩、字型和版面配置的全新設計。 將這類變更套用到整個網站應該是快速且簡單的程式，而不需要修改組成網站的數千個網頁。

透過使用*主版頁面*，即可在 ASP.NET 中建立全網站的頁面範本。 簡單來說，主版頁面是一種特殊的 ASP.NET 網頁，它會定義所有*內容頁面*中通用的標記，以及每個內容頁面上可自訂的區域。 （內容頁面是系結至主版頁面的 ASP.NET 網頁。）每當主版頁面的版面配置或格式變更時，其所有內容頁的輸出同樣都會立即更新，因此套用全網站外觀變更的方式，就像更新和部署單一檔案（也就是主版頁面）一樣簡單。

這是一系列教學課程中的第一個教學課程，可使用主版頁面進行探索。 在本教學課程系列中，我們將：

- 檢查建立主版頁面及其相關聯的內容頁面，
- 討論各種秘訣、訣竅和陷阱，
- 找出常見的主版頁面陷阱並探索因應措施，
- 請參閱如何從內容頁面存取主版頁面，反之亦然。
- 瞭解如何在執行時間指定內容頁面的主版頁面，以及
- 其他先進的主版頁面主題。

這些教學課程的目的是要精簡，並提供逐步指示，讓您能以視覺化方式逐步完成整個流程。 每個教學課程都C#可在和 Visual Basic 版本中取得，並包含下載所使用的完整程式碼。

本執筆教學課程一開始會介紹主版頁面的基本概念。 我們會討論主版頁面的使用方式、查看使用 Visual Web Developer 建立主版頁面和相關聯的內容頁面，以及查看主版頁面的變更會如何立即反映在其內容頁面中。 現在就開始吧！

## <a name="understanding-how-master-pages-work"></a>瞭解主版頁面的工作方式

建立具有一致全網站頁面配置的網站，會要求每個網頁除了其自訂內容之外，也會發出一般格式標記。 例如，雖然 www.asp.net 上的每個教學課程或論壇文章都有自己的獨特內容，但每個頁面也會轉譯一系列常見的 `<div>` 專案，這些專案會顯示最上層的區段連結：首頁、入門、學習等等。

有各種技術可讓您以一致的外觀和風格來建立網頁。 簡單的方法是直接將一般版面配置標記複製並貼到所有網頁中，但這種方法有許多缺點。 針對初學者，每次建立新的頁面時，您都必須記得將共用內容複寫並貼到頁面中。 這類複製和貼上作業會 ripe 錯誤，因為您可能會不小心將共用標記的子集複製到新的頁面。 因此，這種方法會將現有全網站的外觀取代為新的樣子，因為網站中的每一頁都必須經過編輯，才能使用新的外觀與風格。

在 ASP.NET 2.0 版之前，頁面開發人員通常會在[使用者控制項](https://msdn.microsoft.com/library/y6wb1a0e.aspx)中放置常見的標記，然後將這些使用者控制項新增至每個頁面。 這種方法需要網頁程式開發人員務必要手動將使用者控制項加入至每個新的頁面，但可讓您更輕鬆地修改整個網站，因為在更新一般標記時，只需要修改使用者控制項。 可惜的是，Visual Studio .NET 2002 和 2003-用來在設計檢視中建立 ASP.NET 1.x 應用程式轉譯的使用者控制項做為灰色方塊的 Visual Studio 版本。 因此，使用這種方法的網頁開發人員不會享用 WYSIWYG 設計階段環境。

使用使用者控制項的缺點是在 ASP.NET 版本2.0 和 Visual Studio 2005 中，透過*主版頁面*的引進來解決。 主版頁面是一種特殊的 ASP.NET 網頁，可定義網站範圍的標記和*區域*，其中相關聯的*內容頁面*會定義其自訂標記。 如我們在步驟1中所見，這些區域是由 ContentPlaceHolder 控制項所定義。 ContentPlaceHolder 控制項只是代表主版頁面控制項階層中的一個位置，其中的自訂內容可以由內容頁面插入。

> [!NOTE]
> ASP.NET 版本2.0 之後，主版頁面的核心概念和功能並未變更。 不過，Visual Studio 2008 針對嵌套主版頁面提供設計階段支援，這是在 Visual Studio 2005 中缺少的功能。 在未來的教學課程中，我們將探討如何使用嵌套的主版頁面。

[圖 2] 顯示 www.asp.net 的主版頁面看起來可能像這樣。 請注意，主版頁面會定義一般全網站的版面配置-每個頁面頂端、底部和右邊的標記，以及位於中間左側的 ContentPlaceHolder，其中每個個別網頁的唯一內容。

![主版頁面會以內容頁面為基礎，定義網站範圍的版面配置和區域可編輯的地區](creating-a-site-wide-layout-using-master-pages-vb/_static/image4.png)

**圖 02**：主版頁面會定義網站範圍的版面配置，以及每個內容頁面上可編輯的區域

定義主版頁面之後，即可透過核取方塊的滴答來系結至新的 ASP.NET 網頁。 這些 ASP.NET 網頁（稱為內容頁）-包含每個主版頁面 ContentPlaceHolder 控制項的內容控制項。 透過瀏覽器造訪內容頁面時，ASP.NET 引擎會建立主版頁面的控制項階層，並將內容頁面的控制階層插入適當的位置。 這個合併的控制項階層會轉譯，而產生的 HTML 會傳回給使用者的瀏覽器。 因此，[內容] 頁面會在 ContentPlaceHolder 控制項以外的主版頁面中，以及在其本身內容控制項內定義的頁面特定標記，發出一般的標記。 [圖 3] 說明此概念。

[![要求的頁面標記已融合至主版頁面](creating-a-site-wide-layout-using-master-pages-vb/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image5.png)

**圖 03**：要求的頁面標記已融合至主版頁面（[按一下以觀看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image7.png)）

既然我們已經討論過主版頁面的工作方式，讓我們來看一下如何使用 Visual Web Developer 建立主版頁面和相關聯的內容頁面。

> [!NOTE]
> 為了達到最廣泛的可能物件，我們在本教學課程系列中建立的 ASP.NET 網站將使用 ASP.NET 3.5 搭配 Microsoft 的免費版 Visual Studio 2008、 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)來建立。 如果您尚未升級至 ASP.NET 3.5，別擔心，這些教學課程中所討論的概念同樣適用于 ASP.NET 2.0 和 Visual Studio 2005。 不過，某些示範應用程式可能會使用 .NET Framework 版本3.5 的新功能;當使用3.5 特有的功能時，我會包含一個附注，討論如何在2.0 版中執行類似的功能。 請記住，您可以從每個教學課程中下載的示範應用程式會以 .NET Framework 版本3.5 為目標，這會產生包含3.5 特定設定元素的 `Web.config` 檔案。 簡短故事說，如果您還沒有在電腦上安裝 .NET 3.5，下載的 web 應用程式將無法使用，而不需要先從 `Web.config`移除3.5 特定的標記。 如需本主題的詳細資訊，請參閱[剖析 ASP.NET 3.5 版的 `Web.config`](http://www.4guysfromrolla.com/articles/121207-1.aspx)檔案。

## <a name="step-1-creating-a-master-page"></a>步驟1：建立主版頁面

在探索如何建立和使用主要和內容頁面之前，我們先需要 ASP.NET 網站。 一開始請先建立新的以檔案系統為基礎的 ASP.NET 網站。 若要完成此動作，請啟動 Visual Web Developer，然後移至 [檔案] 功能表，並選擇 [新網站]，並顯示 [新網站] 對話方塊（請參閱 [圖 4]）。 選擇 [ASP.NET 網站] 範本，將 [位置] 下拉式清單設定為 [檔案系統]，選擇要放置網站的資料夾，然後將語言設定為 [Visual Basic]。 這會建立新的網站，其中包含 `Default.aspx` ASP.NET 頁面、`App_Data` 資料夾和 `Web.config` 檔案。

> [!NOTE]
> Visual Studio 支援兩種專案管理模式：網站專案和 Web 應用程式專案。 網站專案缺少專案檔，而 Web 應用程式專案在 Visual Studio .NET 2002/2003 中模擬專案架構-它們包括專案檔，並將專案的原始程式碼編譯成單一元件，並放在 [`/bin`] 資料夾中。 Visual Studio 2005 一開始只有支援的網站專案，雖然 Web 應用程式專案模型已與 Service Pack 1 一併重新引入，Visual Studio 2008 提供這兩個專案模型。 不過，Visual Web Developer 2005 和2008版本只支援網站專案。 在本教學課程系列中，我使用網站專案模型來進行示範。 如果您使用非 Express edition，而且想要改為使用[Web 應用程式專案模型](https://msdn.microsoft.com/library/aa730880(vs.80).aspx)，請隨意執行此動作，但請注意，您在畫面上看到的內容和您必須採取的步驟，以及這些教學課程中提供的指示，都可能不一致。

[![建立以檔案系統為基礎的新網站](creating-a-site-wide-layout-using-master-pages-vb/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image8.png)

**圖 04**：建立以檔案系統為基礎的新網站（[按一下以觀看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image10.png)）

接下來，以滑鼠右鍵按一下 [專案名稱]，選擇 [加入新專案]，然後選取 [主版頁面] 範本，將主版頁面新增到根目錄中的網站。 請注意，主版頁面的結尾是 `.master`的延伸模組。 將此新主版頁面命名為 `Site.master`，然後按一下 [新增]。

[![將名為網站的主版頁面新增至網站](creating-a-site-wide-layout-using-master-pages-vb/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image11.png)

**圖 05**：將名為 `Site.master` 的主版頁面新增至網站（[按一下以觀看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image13.png)）

透過 Visual Web Developer 加入新的主版頁面檔案時，會建立含有下列宣告式標記的主版頁面：

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample1.aspx)]

宣告式標記中的第一行是[`@Master`](https://msdn.microsoft.com/library/ms228176.aspx)指示詞。 `@Master` 指示詞類似于出現在 ASP.NET 網頁中的[`@Page`](https://msdn.microsoft.com/library/ydy4x04a.aspx)指示詞。 它會定義伺服器端語言（VB）和主版頁面程式碼後置類別的位置和繼承相關資訊。

`DOCTYPE` 和頁面的宣告式標記會出現在 `@Master` 指示詞之下。 此頁面包含靜態 HTML 和四個伺服器端控制項：

- **Web form （`<form runat="server">`）** -因為所有 ASP.NET 網頁通常都有 Web 表單，而且主版頁面可能包含必須出現在 Web 表單中的 web 控制項-請務必將 web form 新增至主版頁面（而不是將 web form 新增至每個內容頁面）。
- **名為 `ContentPlaceHolder1`的 ContentPlaceHolder 控制項**-此 ContentPlaceHolder 控制項會出現在 Web 表單中，並作為內容頁面使用者介面的區域。
- **伺服器端 `<head>` 元素**-`<head>` 元素具有 `runat="server"` 屬性，讓它可透過伺服器端程式碼存取。 `<head>` 專案會以這種方式執行，以便以程式設計方式新增或調整頁面的標題和其他 `<head>`相關的標記。 例如，設定 ASP.NET 網頁的 `Title` 屬性會變更 `<head>` 伺服器控制項所呈現的 `<title>` 元素。
- **名為 `head`的 ContentPlaceHolder 控制項**-此 ContentPlaceHolder 控制項會出現在 `<head>` 伺服器控制項內，而且可用來以宣告方式將內容新增至 `<head>` 元素。

這個預設的主版頁面宣告式標記可做為設計您自己主版頁面的起點。 您可以隨意編輯 HTML，或將其他 Web 控制項或 ContentPlaceHolders 加入主版頁面。

> [!NOTE]
> 設計主版頁面時，請確定主版頁面包含 Web 表單，且此 Web 表單中至少出現一個 ContentPlaceHolder 控制項。

### <a name="creating-a-simple-site-layout"></a>建立簡單的網站版面配置

讓我們展開 `Site.master`的預設宣告式標記，以建立所有頁面共用的網站版面配置：通用標頭;含有導覽、新聞和其他網站範圍內容的左欄;顯示「由 Microsoft ASP.NET 提供技術支援」圖示的頁尾。 [圖 6] 顯示透過瀏覽器觀看其其中一個內容頁面時，主版頁面的最終結果。 [圖 6] 中的紅色圓圈區域專屬於所造訪的頁面（`Default.aspx`）;其他內容則定義于主版頁面中，因此在所有內容頁面上都是一致的。

[![主版頁面定義頂端、左側和底部部分的標記](creating-a-site-wide-layout-using-master-pages-vb/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image14.png)

**圖 06**：主版頁面定義頂端、左邊和下半部的標記（[按一下以查看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image16.png)）

若要達到 [圖 6] 所示的網站版面配置，請從更新 `Site.master` 主版頁面開始，使其包含下列宣告式標記：

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample2.aspx)]

主版頁面的版面配置是使用一系列的 `<div>` HTML 元素來定義。 `topContent` `<div>` 包含出現在每個頁面頂端的標記，而 `mainContent`、`leftContent`和 `footerContent` `<div>` 會分別用來顯示頁面的內容、左邊的資料行和「由 Microsoft ASP.NET 提供技術支援」圖示。 除了加入這些 `<div>` 元素之外，我也將主要 ContentPlaceHolder 控制項的 `ID` 屬性從 `ContentPlaceHolder1` 重新命名為 `MainContent`。

這些分類 `<div>` 專案的格式設定和配置規則會在[級聯樣式表單（CSS）](http://en.wikipedia.org/wiki/Cascading_Style_Sheets)檔案 `Styles.css`中拼出，這是透過主版頁面的 `<head>` 專案中的 `<link>` 元素所指定。 這些不同的規則會定義上述每個 `<div>` 元素的外觀與風格。 例如，顯示「主版頁面教學課程」文字和連結的 `topContent` `<div>` 元素，在 `Styles.css` 中指定其格式規則，如下所示：

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample3.css)]

如果您在電腦上進行下列動作，您將需要下載本教學課程隨附的程式碼，並將 `Styles.css` 檔案新增至您的專案。 同樣地，您也需要建立名為 `Images` 的資料夾，並將從下載的示範網站複製到您專案的「由 Microsoft ASP.NET 提供」圖示。

> [!NOTE]
> CSS 和網頁格式的討論已超出本文的範圍。 如需 CSS 的詳細資訊，請參閱[Css 教學](http://www.w3schools.com/css/default.asp)課程，網址為[W3Schools.com](http://www.w3schools.com/)。 我也建議您下載本教學課程隨附的程式碼，並在 `Styles.css` 中使用 CSS 設定來查看不同格式規則的效果。

### <a name="creating-a-master-page-using-an-existing-design-template"></a>使用現有的設計範本建立主版頁面

多年來，我為中小型公司打造了一些 ASP.NET 的 web 應用程式。 我的一些用戶端有他們想要使用的現有網站版面配置;其他人雇用了有能力的圖形設計工具。 我有幾個信賴我設計網站版面配置。 如 [圖 6] 所示，負責設計網站版面配置的程式設計師，通常是讓您的會計師執行開放式的外科，同時醫生會進行您的稅金。

幸運的是，有 innumerous 網站提供免費的 HTML 設計範本-Google 針對搜尋詞彙「免費網站範本」傳回6000000以上的結果。 我最愛的一個就是[OpenDesigns.org](http://opendesigns.org/)。一旦找到您喜歡的網站範本之後，請將 CSS 檔案和影像新增至您的網站專案，並將範本的 HTML 整合到主版頁面。

> [!NOTE]
> Microsoft 也提供了一些[免費的 ASP.NET Design 啟動套件範本](https://msdn.microsoft.com/asp.net/aa336613.aspx)，可整合到 Visual Studio 的 [新網站] 對話方塊中。

## <a name="step-2-creating-associated-content-pages"></a>步驟2：建立相關聯的內容頁面

建立主版頁面之後，我們就可以開始建立系結至主版頁面的 ASP.NET 網頁。 這類頁面稱為*內容頁面*。

讓我們將新的 ASP.NET 網頁新增至專案，並將它系結至 `Site.master` 主版頁面。 以滑鼠右鍵按一下方案總管中的專案名稱，然後選擇 [加入新專案] 選項。 選取 [Web 表單] 範本，輸入 `About.aspx`的名稱，然後選取 [選取主版頁面] 核取方塊，如 [圖 7] 所示。 這麼做會顯示 [選取主版頁面] 對話方塊（請參閱 [圖 8]），您可以從這裡選擇要使用的主版頁面。

> [!NOTE]
> 如果您使用 Web 應用程式專案模型（而不是網站專案模型）來建立 ASP.NET 網站，您將不會在 [圖 7] 所示的 [加入新專案] 對話方塊中看到 [選取主版頁面] 核取方塊。 若要在使用 Web 應用程式專案模型時建立內容頁面，您必須選擇 [Web 內容表單] 範本，而不是 [Web 表單] 範本。 選取 [Web 內容表單] 範本並按一下 [新增] 之後，就會出現 [圖 8] 中所示的相同 [選取主版頁面] 對話方塊。

[![新增內容頁面](creating-a-site-wide-layout-using-master-pages-vb/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image17.png)

**圖 07**：新增內容頁面（[按一下以觀看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image19.png)）

[![選取 [網站] 主版頁面](creating-a-site-wide-layout-using-master-pages-vb/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image20.png)

**圖 08**：選取 `Site.master` 主版頁面（[按一下以查看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image22.png)）

如下列宣告式標記所示，新的內容頁面會包含一個 `@Page` 指示詞，它會指向其主版頁面，以及每個主版頁面 ContentPlaceHolder 控制項的內容控制項。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample4.aspx)]

> [!NOTE]
> 在步驟1中的「建立簡單的網站配置」一節中，我將 `ContentPlaceHolder1` 重新命名為 `MainContent`。 如果您未以相同方式重新命名此 ContentPlaceHolder 控制項的 `ID`，則內容頁面的宣告式標記會與上面所示的標記稍有不同。 亦即，第二個內容控制項的 `ContentPlaceHolderID` 將會反映主版頁面中對應 ContentPlaceHolder 控制項的 `ID`。

轉譯內容頁時，ASP.NET 引擎必須在頁面的內容控制項中加上其主版頁面的 ContentPlaceHolder 控制項。 ASP.NET 引擎會從 `@Page` 指示詞的 `MasterPageFile` 屬性判斷內容頁面的主版頁面。 如上述標記所示，此內容頁面會系結至 `~/Site.master`。

因為主版頁面有兩個 ContentPlaceHolder 控制項，`head` 和 `MainContent`-Visual Web Developer 產生了兩個內容控制項。 每個內容控制項都會透過其 `ContentPlaceHolderID` 屬性來參考特定的 ContentPlaceHolder。

主版頁面會在其設計階段支援的情況下，與先前全網站的範本技術相比。 [圖 9] 顯示透過 Visual Web Developer 的設計檢視觀看時的 `About.aspx` 內容頁面。 請注意，主版頁面內容會顯示為灰色，而且無法修改。 不過，與主版頁面的 ContentPlaceHolders 對應的內容控制項是可編輯的。 就像任何其他 ASP.NET 網頁，您可以透過來源或設計檢視加入 Web 控制項，來建立內容頁面的介面。

[![[內容] 頁面的設計檢視會同時顯示頁面特定和主版頁面的內容](creating-a-site-wide-layout-using-master-pages-vb/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image23.png)

**圖 09**： [內容] 頁面的設計檢視會同時顯示頁面特定和主版頁面的內容（[按一下以查看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image25.png)）

### <a name="adding-markup-and-web-controls-to-the-content-page"></a>將標記和 Web 控制項新增至內容頁面

請花一些時間建立 `About.aspx` 頁面的一些內容。 如 [圖 10] 所示，我輸入了「關於作者」標題和幾段文字，但您也可以隨意加入 Web 控制項。 建立此介面之後，請透過瀏覽器造訪 [`About.aspx`] 頁面。

[![透過瀏覽器造訪 About .aspx 頁面](creating-a-site-wide-layout-using-master-pages-vb/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image26.png)

**圖 10**：透過瀏覽器造訪 `About.aspx` 頁面（[按一下以觀看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image28.png)）

請務必瞭解，要求的內容頁面和其相關聯的主版頁面都已融合在 web 伺服器上，並全部呈現為整體。 然後，終端使用者的瀏覽器會傳送產生的已融合 HTML。 若要確認這一點，請前往 [View] 功能表並選擇 [Source]，以查看瀏覽器收到的 HTML。 請注意，在單一視窗中，沒有任何框架或任何其他特定的技術可顯示兩個不同的網頁。

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>將主版頁面系結至現有的 ASP.NET 網頁

如我們在這個步驟中所見，將新的內容頁新增至 ASP.NET web 應用程式，就像勾選 [選取主版頁面] 核取方塊並挑選主版頁面一樣簡單。 可惜的是，將現有的 ASP.NET 頁轉換成主版頁面並不容易。

若要將主版頁面系結至現有的 ASP.NET 網頁，您需要執行下列步驟：

1. 將 `MasterPageFile` 屬性加入至 ASP.NET 網頁的 `@Page` 指示詞，並將其指向適當的主版頁面。
2. 在主版頁面中新增每個 ContentPlaceHolders 的內容控制項。
3. 選擇性地將 ASP.NET 網頁的現有內容剪下並貼到適當的內容控制項中。 我在此說「選擇性」，因為 ASP.NET 網頁可能包含主版頁面已經表示的標記，例如 `DOCTYPE`、`<html>` 元素和 Web 表單。

如需此程式的逐步指示以及螢幕擷取畫面，請參閱[Scott Guthrie](https://weblogs.asp.net/scottgu/)的[使用主版頁面和網站導覽](http://webproject.scottgu.com/VisualBasic/MasterPages/MasterPages.aspx)教學課程。 「更新 `Default.aspx` 和 `DataSample.aspx` 使用主版頁面」一節會詳細說明這些步驟。

由於建立新的內容頁面比將現有的 ASP.NET 網頁轉換成內容頁更容易，因此建議您在建立新的 ASP.NET 網站時，將主版頁面新增至網站。 將所有新的 ASP.NET 網頁系結至此主版頁面。 如果初始主版頁面非常簡單或純文字，別擔心，您稍後可以更新主版頁面。

> [!NOTE]
> 當您建立新的 ASP.NET 應用程式時，Visual Web Developer 會加入未系結至主版頁面的 `Default.aspx` 頁面。 如果您想要練習將現有的 ASP.NET 網頁轉換成內容頁面，請繼續進行，並使用 `Default.aspx`。 或者，您可以刪除 `Default.aspx` 然後重新加入它，但這次請勾選 [選取主版頁面] 核取方塊。

## <a name="step-3-updating-the-master-pages-markup"></a>步驟3：更新主版頁面的標記

主版頁面的主要優點之一，是可以使用單一主版頁面來定義網站上多頁的整體版面配置。 因此，更新網站的外觀和風格需要更新單一檔案，也就是主版頁面。

為了說明這種行為，讓我們更新主版頁面，將目前的日期包含在左側資料行的頂端。 將名為 `DateDisplay` 的標籤新增至 `leftContent` `<div>`。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample5.aspx)]

接下來，建立主版頁面的 `Page_Load` 事件處理常式，並加入下列程式碼：

[!code-vb[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample6.vb)]

上述程式碼會將標籤的 `Text` 屬性設定為目前的日期和時間，格式為一周中的日期、月份的名稱和兩位數的日期（請參閱 [圖 11]）。 進行這項變更後，請重新流覽您的其中一個內容頁面。 如 [圖 11] 所示，產生的標記會立即更新以包含主版頁面的變更。

[在觀看內容頁面時，會反映主版頁面的變更 ![](creating-a-site-wide-layout-using-master-pages-vb/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image29.png)

**圖 11**：主版頁面的變更會在觀看內容頁面時反映（[按一下以觀看完整大小的影像](creating-a-site-wide-layout-using-master-pages-vb/_static/image31.png)）

> [!NOTE]
> 如下列範例所示，主版頁面可能包含伺服器端 Web 控制項、程式碼和事件處理常式。

## <a name="summary"></a>總結

主版頁面可讓 ASP.NET 開發人員設計一致的全網站版面配置，輕鬆地進行更新。 建立主版頁面和其相關聯的內容頁面與建立標準 ASP.NET 網頁一樣簡單，因為 Visual Web Developer 提供豐富的設計階段支援。

我們在本教學課程中建立的主版頁面範例有兩個 ContentPlaceHolder 控制項： head 和 MainContent。 不過，我們只在內容頁面中指定了 MainContent ContentPlaceHolder 控制項的標記。 在下一個教學課程中，我們將探討如何在 [內容] 頁面中使用多個內容控制項。 我們也會瞭解如何在主版頁面中定義內容控制項的預設標記，以及如何在使用主版頁面中定義的預設標記，以及從 [內容] 頁面提供自訂標記之間切換。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [適用于設計人員的 ASP.NET：免費的設計範本，以及使用 Web 標準建立 ASP.NET 網站的指引](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET 主版頁面總覽](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [級聯樣式表單（CSS）教學課程](http://www.w3schools.com/css/default.asp)
- [動態設定頁面的標題](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP.NET 中的主版頁面](http://www.odetocode.com/articles/419.aspx)
- [主版頁面快速入門教學課程](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](nested-master-pages-cs.md)
> [下一頁](multiple-contentplaceholders-and-default-content-vb.md)
