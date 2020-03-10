---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: 同時執行數個動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許執行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598116"
---
# <a name="executing-several-animations-at-the-same-time-c"></a>同時執行數個動畫（C#）

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許以平行方式執行數個動畫。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許以平行方式執行數個動畫。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。 一般來說，`<OnLoad>` 只接受一個動畫。 動畫架構可讓您使用 `<Parallel>` 元素，將數個動畫聯結至其中一個。 `<Parallel>` 內的所有動畫都是在同一時間執行。

以下是 `AnimationExtender` 控制項的可能標記、淡出並同時調整面板大小：

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

事實上：當您執行此腳本時，會顯示面板，然後調整大小（大於增加三倍其寬度並減半其高度）並同時淡出。

[![面板會淡出並根據瀏覽器的轉譯引擎調整大小（包括其內容）](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)

由於瀏覽器的轉譯引擎，面板會淡出並調整大小（包括其內容）（請[按一下以觀看完整大小的影像](executing-several-animations-at-the-same-time-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](adding-animation-to-a-control-cs.md)
> [下一頁](executing-several-animations-after-each-other-cs.md)
