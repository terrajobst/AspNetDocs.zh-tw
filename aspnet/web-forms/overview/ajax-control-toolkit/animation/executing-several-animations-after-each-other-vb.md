---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 彼此執行數個動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許執行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606883"
---
# <a name="executing-several-animations-after-each-other-vb"></a>接續執行數個動畫 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許逐一執行數個動畫。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許逐一執行數個動畫。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。 一般來說，`<OnLoad>` 只接受一個動畫。 動畫架構可讓您使用 `<Sequence>` 元素，將數個動畫聯結至其中一個。 `<Sequence>` 內的所有動畫都會逐一執行。 以下是 `AnimationExtender` 控制項的可能標記，先使面板變寬，然後減少其高度：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

當您執行此腳本時，面板會先變寬，然後再變小。

[![先增加寬度](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)

首先會增加寬度（[按一下以查看完整大小的影像](executing-several-animations-after-each-other-vb/_static/image3.png)）

[![，則高度會減少](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)

然後會減少高度（[按一下以觀看完整大小的影像](executing-several-animations-after-each-other-vb/_static/image6.png)）

> [!div class="step-by-step"]
> [上一頁](executing-several-animations-at-the-same-time-vb.md)
> [下一頁](animation-depending-on-a-condition-vb.md)
