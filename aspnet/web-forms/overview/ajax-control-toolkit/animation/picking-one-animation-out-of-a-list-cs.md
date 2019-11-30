---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 從清單中挑選一個動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 架構也 w 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2bc203d694792716bbf4f7d7b8d152c589bf99b1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575129"
---
# <a name="picking-one-animation-out-of-a-list-c"></a>從清單中挑選一張動畫 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)

> ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 此架構也可讓程式設計人員從動畫清單中挑選一個動畫，視某些 JavaScript 程式碼的評估而定。

## <a name="overview"></a>概觀

ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 此架構也可讓程式設計人員從動畫清單中挑選一個動畫，視某些 JavaScript 程式碼的評估而定。

## <a name="steps"></a>步驟

首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

動畫將會套用至文字的面板，如下所示：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。 `<Case>` 元素不是其中一個一般動畫，而是會開始播放。 會評估其 SelectScript 屬性的值;傳回值必須是數值。 根據此數目，會執行 &lt;案例&gt; 內的其中一個 subanimations。 例如，如果 SelectScript 評估為2，則控制工具組會在 &lt;案例&gt; （從0開始計算）中執行第三個動畫。

下列標記會定義三個 subanimations：調整寬度大小、調整高度大小，以及淡出。JavaScript 程式碼（`Math.floor(3 * Math.random())`）接著會挑選0和2之間的數位，以便執行三個動畫的其中一個：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

[![其中一種可能的動畫：面板變寬](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

其中一個可能的動畫：面板變寬（[按一下以觀看完整大小的影像](picking-one-animation-out-of-a-list-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](animation-depending-on-a-condition-cs.md)
> [下一頁](animating-in-response-to-user-interaction-cs.md)
