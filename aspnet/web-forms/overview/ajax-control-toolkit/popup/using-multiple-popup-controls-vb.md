---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 使用多個快顯視窗控制項（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 您也可以使用 m 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: e1f4ff64e9fdf48ea63b75c97acd53a64b5ab5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612529"
---
# <a name="using-multiple-popup-controls-vb"></a>使用多個快顯視窗控制項 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)

> AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 您也可以在單一頁面上使用多個快顯視窗控制項。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 您也可以在單一頁面上使用多個快顯視窗控制項。

## <a name="steps"></a>步驟

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

接下來，新增一個做為快顯視窗的面板。 在目前的案例中，面板包含 `Calendar` 控制項。 為了避免行事曆的回傳所造成的頁面重新整理，面板會放在 `UpdatePanel` 控制項內：

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

此頁面也包含兩個文字方塊。 針對每個文字方塊，一旦啟動文字方塊之後，行事曆快顯視窗就會出現。

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

現在以 `PopupControlExtender`擴充兩個文字方塊。 `TargetControlID` 屬性提供系結至擴充項之控制項的識別碼。 `PopupControlID` 屬性包含快顯面板的識別碼。 在此情況下，這兩個擴充項都會顯示相同的面板，但也可能會有不同的面板。

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

現在，只要您在文字欄位內按一下，行事曆就會出現在欄位下方，讓您可以選取日期。 （在不同的教學課程中將會涵蓋將選取的日期放回文字方塊中）。

[當使用者按一下文字方塊時，就會顯示行事曆 ![](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)

當使用者按一下文字方塊時，就會出現行事曆（[按一下以查看完整大小的影像](using-multiple-popup-controls-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [下一頁](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
