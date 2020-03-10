---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: 將動畫新增至控制項（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 本教學課程顯示如何 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598298"
---
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="2746b-104">將動畫新增至控制項 (VB)</span><span class="sxs-lookup"><span data-stu-id="2746b-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="2746b-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2746b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2746b-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2746b-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="2746b-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="2746b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2746b-108">本教學課程說明如何設定這種動畫。</span><span class="sxs-lookup"><span data-stu-id="2746b-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="2746b-109">概觀</span><span class="sxs-lookup"><span data-stu-id="2746b-109">Overview</span></span>

<span data-ttu-id="2746b-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="2746b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2746b-111">本教學課程說明如何設定這種動畫。</span><span class="sxs-lookup"><span data-stu-id="2746b-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="2746b-112">步驟</span><span class="sxs-lookup"><span data-stu-id="2746b-112">Steps</span></span>

<span data-ttu-id="2746b-113">第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="2746b-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="2746b-114">此案例中的動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2746b-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="2746b-115">面板的相關聯 CSS 類別會定義背景色彩和寬度：</span><span class="sxs-lookup"><span data-stu-id="2746b-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="2746b-116">接下來，我們需要 `AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="2746b-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="2746b-117">在提供 `ID` 和一般的 `runat="server"`之後，必須將 `TargetControlID` 屬性設定為控制項，以便在我們的案例中以動畫顯示（panel）：</span><span class="sxs-lookup"><span data-stu-id="2746b-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="2746b-118">整個動畫會使用 XML 語法以宣告方式套用，但目前並不完全支援 Visual Studio 的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="2746b-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="2746b-119">根節點在此節點中 `<Animations>;`，允許數個事件來判斷動畫的執行時間：</span><span class="sxs-lookup"><span data-stu-id="2746b-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="2746b-120">`OnClick` （滑鼠按一下）</span><span class="sxs-lookup"><span data-stu-id="2746b-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="2746b-121">`OnHoverOut` （當滑鼠離開控制項時）</span><span class="sxs-lookup"><span data-stu-id="2746b-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="2746b-122">`OnHoverOver` （當滑鼠停留在控制項上時，停止 `OnHoverOut` 動畫）</span><span class="sxs-lookup"><span data-stu-id="2746b-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="2746b-123">`OnLoad` （載入頁面時）</span><span class="sxs-lookup"><span data-stu-id="2746b-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="2746b-124">`OnMouseOut` （當滑鼠離開控制項時）</span><span class="sxs-lookup"><span data-stu-id="2746b-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="2746b-125">`OnMouseOver` （當滑鼠停留在控制項上時，不會停止 `OnMouseOut` 動畫）</span><span class="sxs-lookup"><span data-stu-id="2746b-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="2746b-126">此架構隨附一組動畫，每一個都由自己的 XML 元素表示。</span><span class="sxs-lookup"><span data-stu-id="2746b-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="2746b-127">選擇如下：</span><span class="sxs-lookup"><span data-stu-id="2746b-127">Here is a selection:</span></span>

- <span data-ttu-id="2746b-128">`<Color>` （變更色彩）</span><span class="sxs-lookup"><span data-stu-id="2746b-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="2746b-129">`<FadeIn>` （淡入）</span><span class="sxs-lookup"><span data-stu-id="2746b-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="2746b-130">`<FadeOut>` （淡出）</span><span class="sxs-lookup"><span data-stu-id="2746b-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="2746b-131">`<Property>` （變更控制項的屬性）</span><span class="sxs-lookup"><span data-stu-id="2746b-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="2746b-132">`<Pulse>` （pulsating）</span><span class="sxs-lookup"><span data-stu-id="2746b-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="2746b-133">`<Resize>` （變更大小）</span><span class="sxs-lookup"><span data-stu-id="2746b-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="2746b-134">`<Scale>` （按比例變更大小）</span><span class="sxs-lookup"><span data-stu-id="2746b-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="2746b-135">在此範例中，面板應淡出。動畫應需要1.5 秒（`Duration` 屬性），顯示每秒24個畫面格（動畫步驟）（`Fps` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="2746b-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="2746b-136">以下是 `AnimationExtender` 控制項的完整標記：</span><span class="sxs-lookup"><span data-stu-id="2746b-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="2746b-137">當您執行此腳本時，會顯示面板並淡出一段半秒。</span><span class="sxs-lookup"><span data-stu-id="2746b-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="2746b-138">[![面板會淡出](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2746b-138">[![The panel is fading out](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="2746b-139">此面板會淡出（[按一下以觀看完整大小的影像](adding-animation-to-a-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="2746b-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2746b-140">[上一頁](dynamically-controlling-updatepanel-animations-cs.md)
> [下一頁](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2746b-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
