---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: 視條件而定的動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫是否為 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 583ebdbf109beb74b9a425020477183067bbb79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614342"
---
# <a name="animation-depending-on-a-condition-vb"></a>依據條件的動畫 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 是否執行動畫也可能相依于某種 JavaScript 程式碼形式的條件。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 是否執行動畫也可能相依于某種 JavaScript 程式碼形式的條件。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。 `<Condition>` 元素不是其中一個一般動畫，而是會開始播放。 提供做為 `ConditionScript` 屬性值的 JavaScript 程式碼會在執行時間執行。 如果評估為 true，則會執行動畫，否則不會。 下列標記提供兩個動畫，每一個都是隨機執行的50% 案例。 由於 `<OnLoad>`中可能只有一個動畫，因此會使用 `<Sequence>` 元素，將兩個 `<Condition>` 動畫聯結在一起：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

請注意，`ConditionScript` 屬性中的小於符號（`<`）必須經過轉義（）。 當您執行此腳本時，不會執行任何動畫，或其中一個動作會執行，或兩者都有。

[![面板會淡出而不調整大小，因此第二個動畫會執行，第一個則不會](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

面板會淡出而不調整大小，因此第二個動畫會執行，第一個則不會（[按一下以查看完整大小的影像](animation-depending-on-a-condition-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](executing-several-animations-after-each-other-vb.md)
> [下一頁](picking-one-animation-out-of-a-list-vb.md)
