---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: 從清單中挑選一張動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 架構也 w 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 694416532b558291ff6ab57a442058b53d6167e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536110"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="23da2-104">從清單中挑選一張動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="23da2-104">Picking One Animation Out Of a List (VB)</span></span>

<span data-ttu-id="23da2-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="23da2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="23da2-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="23da2-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="23da2-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="23da2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="23da2-108">此架構也可讓程式設計人員從動畫清單中挑選一個動畫，視某些 JavaScript 程式碼的評估而定。</span><span class="sxs-lookup"><span data-stu-id="23da2-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="23da2-109">概觀</span><span class="sxs-lookup"><span data-stu-id="23da2-109">Overview</span></span>

<span data-ttu-id="23da2-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="23da2-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="23da2-111">此架構也可讓程式設計人員從動畫清單中挑選一個動畫，視某些 JavaScript 程式碼的評估而定。</span><span class="sxs-lookup"><span data-stu-id="23da2-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="23da2-112">步驟</span><span class="sxs-lookup"><span data-stu-id="23da2-112">Steps</span></span>

<span data-ttu-id="23da2-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="23da2-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="23da2-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="23da2-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="23da2-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="23da2-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="23da2-116">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="23da2-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="23da2-117">在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。</span><span class="sxs-lookup"><span data-stu-id="23da2-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="23da2-118">`<Case>` 元素不是其中一個一般動畫，而是會開始播放。</span><span class="sxs-lookup"><span data-stu-id="23da2-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="23da2-119">會評估其 SelectScript 屬性的值;傳回值必須是數值。</span><span class="sxs-lookup"><span data-stu-id="23da2-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="23da2-120">根據此數目，會執行 &lt;案例&gt; 內的其中一個 subanimations。</span><span class="sxs-lookup"><span data-stu-id="23da2-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="23da2-121">例如，如果 SelectScript 評估為2，則控制工具組會在 &lt;案例&gt; （從0開始計算）中執行第三個動畫。</span><span class="sxs-lookup"><span data-stu-id="23da2-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="23da2-122">下列標記會定義三個 subanimations：調整寬度大小、調整高度大小，以及淡出。JavaScript 程式碼（`Math.floor(3 * Math.random())`）接著會挑選0和2之間的數位，以便執行三個動畫的其中一個：</span><span class="sxs-lookup"><span data-stu-id="23da2-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]

<span data-ttu-id="23da2-123">[![其中一種可能的動畫：面板變寬](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="23da2-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span></span>

<span data-ttu-id="23da2-124">其中一個可能的動畫：面板變寬（[按一下以觀看完整大小的影像](picking-one-animation-out-of-a-list-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="23da2-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="23da2-125">[上一頁](animation-depending-on-a-condition-vb.md)
> [下一頁](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="23da2-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
