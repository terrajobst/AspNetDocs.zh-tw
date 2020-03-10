---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: 使用 TagBuilder 類別來建立 HTML 協助程式（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 將為您介紹名為 TagBuilder 類別的 ASP.NET MVC 架構中實用的公用程式類別。 您可以輕鬆地使用 TagBuilder 類別 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599999"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a>使用 TagBuilder 類別來建立 HTML 協助程式（VB）

依[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 將為您介紹名為 TagBuilder 類別的 ASP.NET MVC 架構中實用的公用程式類別。 您可以使用 TagBuilder 類別，輕鬆地建立 HTML 標籤。

ASP.NET MVC 架構包含一個有用的公用程式類別，名為 TagBuilder 類別，可讓您在建立 HTML helper 時使用。 TagBuilder 類別，做為類別名稱的建議，可讓您輕鬆地建立 HTML 標籤。 在這個簡短的教學課程中，您會看到 TagBuilder 類別的總覽，並瞭解如何在建立可轉譯 HTML &lt;img&gt; 標記的簡單 HTML helper 時，使用這個類別。

## <a name="overview-of-the-tagbuilder-class"></a>TagBuilder 類別的總覽

TagBuilder 類別包含在 System.web 命名空間中。 它有五個方法：

- AddCssClass （）–可讓您將新的*class = ""* 屬性新增至標記。
- GenerateId （）–可讓您將 id 屬性新增至標記。 這個方法會自動取代識別碼中的句號（根據預設，句號會以底線取代）
- MergeAttribute （）–可讓您將屬性新增至標記。 這個方法有多個多載。
- SetInnerText （）–可讓您設定標記的內部文字。 內部文字會自動進行 HTML 編碼。
- ToString （）–可讓您呈現標記。 您可以指定是否要建立一般標記、開始標記、結束標記或自我結束記號。

TagBuilder 類別有四個重要的屬性：

- 屬性–代表標記的所有屬性。
- IdAttributeDotReplacement –代表 GenerateId （）方法用來取代句號的字元（預設值為底線）。
- InnerHTML –代表標記的內部內容。 將字串指派給這個屬性*並不會*對字串進行 HTML 編碼。
- TagName –代表標記的名稱。

這些方法和屬性會提供您建立 HTML 標籤所需的所有基本方法和屬性。 您實際上不需要使用 TagBuilder 類別。 您可以改用 StringBuilder 類別。 不過，TagBuilder 類別讓您的生活變得更簡單。

## <a name="creating-an-image-html-helper"></a>建立影像 HTML Helper

當您建立 TagBuilder 類別的實例時，會將您要建立的標記名稱傳遞至 TagBuilder 的函式。 接下來，您可以呼叫方法（例如 AddCssClass 和 MergeAttribute （）方法）來修改標記的屬性。 最後，您可以呼叫 ToString （）方法來呈現標記。

例如，[清單 1] 包含影像 HTML helper。 影像協助程式會在內部實作為 TagBuilder，表示 HTML &lt;img&gt; 標記。

**清單1– Helpers\ImageHelper.vb**

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

[清單 1] 中的模組包含兩個名為 Image （）的多載方法。 當您呼叫 Image （）方法時，可以傳遞代表一組 HTML 屬性的物件。

請注意如何使用 TagBuilder. MergeAttribute （）方法，將個別屬性（例如 src 屬性）新增至 TagBuilder。 此外，請注意如何使用 TagBuilder. MergeAttributes （）方法，將屬性集合加入至 TagBuilder。 MergeAttributes （）方法會接受字典&lt;字串，物件&gt; 參數。 RouteValueDictionary 類別是用來將代表屬性集合的物件，轉換成字典&lt;字串，物件&gt;。

建立映射協助程式之後，您就可以在 ASP.NET MVC views 中使用 helper，就像任何其他標準 HTML helper 一樣。 [清單 2] 中的視圖使用影像協助程式顯示 Xbox 的相同影像兩次（請參閱 [圖 1]）。 不論是否有 HTML 屬性集合，都會呼叫 Image （）協助程式。

**清單2– Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

[![[新增專案] 對話方塊](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)

**圖 01**：使用影像協助程式（[按一下以觀看完整大小的影像](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png)）

請注意，您必須在 [default.aspx] 視圖的頂端匯入與影像協助程式關聯的命名空間。 Helper 會以下列指示詞彙入：

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

在 Visual Basic 應用程式中，預設命名空間與應用程式的名稱相同。

> [!div class="step-by-step"]
> [上一頁](creating-custom-html-helpers-vb.md)
> [下一頁](creating-page-layouts-with-view-master-pages-vb.md)
