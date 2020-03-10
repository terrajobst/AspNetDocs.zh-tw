---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: 資料系結至可折疊（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會宣告為 w 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bfb31940c0395c7ed1d5d471fb8fb686b66c59ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614517"
---
# <a name="databinding-to-an-accordion-vb"></a>資料繫結至 Accordion (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)

> AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會在頁面本身內宣告，但系結至資料來源可提供更大的彈性。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 [可折疊式] 控制項提供多個窗格，並允許使用者一次顯示其中一項。 面板通常會在頁面本身內宣告，但系結至資料來源可提供更大的彈性。

## <a name="steps"></a>步驟

首先，需要資料來源。 這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。 資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。 AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。 設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。

在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。 如果您的安裝程式不同，則必須調整資料庫的連接資訊。

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

然後，將資料來源加入至頁面。 為了使用有限數量的資料，我們只會在 AdventureWorks 資料庫的 [廠商] 資料表中選取前五個專案。 如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。 下列標記會顯示正確的語法：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

請記住資料來源的名稱（ID）。 接著，必須在 [可折疊] 控制項的 [`DataSourceID`] 屬性中使用此非常識別：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

在 [可折疊] 控制項中，您可以提供控制項各部分的範本，包括標頭（`<HeaderTemplate>`）和內容（`<ContentTemplate>`）。 在這些元素內，只要使用 `DataBinder.Eval()` 方法，就能從資料來源輸出資料：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

載入頁面時，必須使用下列伺服器端程式碼，將資料來源系結至可折疊的：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

若要結束此範例，您需要定義在 [可折疊] 控制項（在其屬性 `HeaderCssClass` 和 `ContentCssClass`）中所參考的兩個 CSS 類別。 將下列標記放在頁面的 [`<head>`] 區段中：

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]

[![中的資料可直接來自資料來源](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)

可折疊中的資料直接來自資料來源（[按一下以查看完整大小的影像](databinding-to-an-accordion-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](dynamically-adding-an-accordion-pane-cs.md)
> [下一頁](dynamically-adding-an-accordion-pane-vb.md)
