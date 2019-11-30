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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606989"
---
# <a name="animation-depending-on-a-condition-vb"></a><span data-ttu-id="ef375-104">依據條件的動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="ef375-104">Animation Depending On a Condition (VB)</span></span>

<span data-ttu-id="ef375-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ef375-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ef375-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ef375-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span></span>

> <span data-ttu-id="ef375-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ef375-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ef375-108">是否執行動畫也可能相依于某種 JavaScript 程式碼形式的條件。</span><span class="sxs-lookup"><span data-stu-id="ef375-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="ef375-109">概觀</span><span class="sxs-lookup"><span data-stu-id="ef375-109">Overview</span></span>

<span data-ttu-id="ef375-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ef375-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ef375-111">是否執行動畫也可能相依于某種 JavaScript 程式碼形式的條件。</span><span class="sxs-lookup"><span data-stu-id="ef375-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="ef375-112">步驟</span><span class="sxs-lookup"><span data-stu-id="ef375-112">Steps</span></span>

<span data-ttu-id="ef375-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="ef375-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

<span data-ttu-id="ef375-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ef375-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

<span data-ttu-id="ef375-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="ef375-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

<span data-ttu-id="ef375-116">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="ef375-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

<span data-ttu-id="ef375-117">在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。</span><span class="sxs-lookup"><span data-stu-id="ef375-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="ef375-118">`<Condition>` 元素不是其中一個一般動畫，而是會開始播放。</span><span class="sxs-lookup"><span data-stu-id="ef375-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="ef375-119">提供做為 `ConditionScript` 屬性值的 JavaScript 程式碼會在執行時間執行。</span><span class="sxs-lookup"><span data-stu-id="ef375-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="ef375-120">如果評估為 true，則會執行動畫，否則不會。</span><span class="sxs-lookup"><span data-stu-id="ef375-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="ef375-121">下列標記提供兩個動畫，每一個都是隨機執行的50% 案例。</span><span class="sxs-lookup"><span data-stu-id="ef375-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="ef375-122">由於 `<OnLoad>`中可能只有一個動畫，因此會使用 `<Sequence>` 元素，將兩個 `<Condition>` 動畫聯結在一起：</span><span class="sxs-lookup"><span data-stu-id="ef375-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

<span data-ttu-id="ef375-123">請注意，`ConditionScript` 屬性中的小於符號（`<`）必須經過轉義（）。</span><span class="sxs-lookup"><span data-stu-id="ef375-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="ef375-124">當您執行此腳本時，不會執行任何動畫，或其中一個動作會執行，或兩者都有。</span><span class="sxs-lookup"><span data-stu-id="ef375-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>

<span data-ttu-id="ef375-125">[![面板會淡出而不調整大小，因此第二個動畫會執行，第一個則不會](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ef375-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span></span>

<span data-ttu-id="ef375-126">面板會淡出而不調整大小，因此第二個動畫會執行，第一個則不會（[按一下以查看完整大小的影像](animation-depending-on-a-condition-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="ef375-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ef375-127">[上一頁](executing-several-animations-after-each-other-vb.md)
> [下一頁](picking-one-animation-out-of-a-list-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ef375-127">[Previous](executing-several-animations-after-each-other-vb.md)
[Next](picking-one-animation-out-of-a-list-vb.md)</span></span>
