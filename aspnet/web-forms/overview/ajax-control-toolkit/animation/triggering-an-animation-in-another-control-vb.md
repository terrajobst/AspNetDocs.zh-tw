---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 觸發另一個控制項中的動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 一般來說，啟動 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575052"
---
# <a name="triggering-an-animation-in-another-control-vb"></a>觸發另一個控制項中的動畫 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 一般來說，啟動動畫是由與相同控制項的使用者互動所觸發。 不過，您也可以與一個控制項互動，然後再動畫另一個控制項。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 一般來說，啟動動畫是由與相同控制項的使用者互動所觸發。 不過，您也可以與一個控制項互動，然後再動畫另一個控制項。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

為了開始繪製面板的動畫，會使用 HTML 按鈕。 請注意，`<input type="button" />` 是透過 `<asp:Button />` favoured，因為當使用者按一下該按鈕時，不會進行回傳。

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`。 請務必將 `TargetControlID` 設定為按鈕（觸發動畫的元素）的識別碼，而不是將面板的識別碼（要進行動畫的專案）設為

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

在 [`<Animations>`] 節點內，如往常般放置動畫。 為了讓它們變更面板，而不是按鈕，請在 `AnimationExtender`內設定每個動畫元素的 `AnimationTarget` 屬性。 當然，`AnimationTarget` 的值是面板的識別碼。 如此一來，就會在面板中出現動畫，而不是使用 [觸發] 按鈕。 以下是此案例的 `AnimationExtender` 標記：

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

請注意個別動畫出現的特殊順序。 首先，按鈕會在動畫執行後停用。 因為 `<EnableAction>` 元素中沒有 `AnimationTarget` 屬性，所以這個動畫會套用至原始控制項：按鈕。 接下來的兩個動畫步驟應該以平行方式執行（`<Parallel>` 元素）。 兩者的 `AnimationTarget` 屬性都設定為 `"Panel1"`，因此會以動畫顯示面板，而不是按鈕。

[![滑鼠按一下按鈕時，就會啟動面板動畫](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

當滑鼠按一下按鈕時，就會啟動面板動畫（[按一下以查看完整大小的影像](triggering-an-animation-in-another-control-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](disabling-actions-during-animation-vb.md)
> [下一頁](modifying-animations-from-the-server-side-vb.md)
