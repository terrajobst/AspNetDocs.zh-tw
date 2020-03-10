---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: 以動畫方式回應使用者互動（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫可以是星號 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614370"
---
# <a name="animating-in-response-to-user-interaction-c"></a>根據使用者互動繪製動畫 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫可以自動啟動，或可能由使用者互動觸發，例如按一下滑鼠。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫可以自動啟動，或可能由使用者互動觸發，例如按一下滑鼠。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

在 [`<Animations>`] 節點中，有五種方式可透過使用者互動來啟動動畫（遺失的元素是 `<OnLoad>`，一旦整個頁面完全載入，就會執行此動作）：

- `<OnClick>` （滑鼠按一下控制項）
- `<OnHoverOut>` （滑鼠離開控制項）
- `<OnHoverOver>` （滑鼠停留在控制項上，停止 `<OnHoverOut>` 動畫）
- `<OnMouseOut>` （滑鼠離開控制項）
- `<OnMouseOver>` （滑鼠停留在控制項上，而不是停止 `<OnMouseOut>` 動畫）

在此案例中，會使用 `<OnClick>`。 當使用者按一下面板時，會將其調整大小並淡出一次。

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

[![按一下滑鼠，就會啟動動畫](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

按一下滑鼠即可啟動動畫（[按一下以觀看完整大小的影像](animating-in-response-to-user-interaction-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](picking-one-animation-out-of-a-list-cs.md)
> [下一頁](disabling-actions-during-animation-cs.md)
