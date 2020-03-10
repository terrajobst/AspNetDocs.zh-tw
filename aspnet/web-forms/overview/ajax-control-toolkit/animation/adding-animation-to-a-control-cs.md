---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: 將動畫新增至控制項（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 本教學課程顯示如何 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614447"
---
# <a name="adding-animation-to-a-control-c"></a><span data-ttu-id="49e7a-104">將動畫新增至控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="49e7a-104">Adding Animation to a Control (C#)</span></span>

<span data-ttu-id="49e7a-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="49e7a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="49e7a-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="49e7a-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="49e7a-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="49e7a-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="49e7a-108">本教學課程說明如何設定這種動畫。</span><span class="sxs-lookup"><span data-stu-id="49e7a-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="49e7a-109">概觀</span><span class="sxs-lookup"><span data-stu-id="49e7a-109">Overview</span></span>

<span data-ttu-id="49e7a-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="49e7a-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="49e7a-111">本教學課程說明如何設定這種動畫。</span><span class="sxs-lookup"><span data-stu-id="49e7a-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="49e7a-112">步驟</span><span class="sxs-lookup"><span data-stu-id="49e7a-112">Steps</span></span>

<span data-ttu-id="49e7a-113">第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="49e7a-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="49e7a-114">此案例中的動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49e7a-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="49e7a-115">面板的相關聯 CSS 類別會定義背景色彩和寬度：</span><span class="sxs-lookup"><span data-stu-id="49e7a-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="49e7a-116">接下來，我們需要 `AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="49e7a-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="49e7a-117">在提供 `ID` 和一般的 `runat="server"`之後，必須將 `TargetControlID` 屬性設定為控制項，以便在我們的案例中以動畫顯示（panel）：</span><span class="sxs-lookup"><span data-stu-id="49e7a-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="49e7a-118">整個動畫會使用 XML 語法以宣告方式套用，但目前並不完全支援 Visual Studio 的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="49e7a-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="49e7a-119">根節點在此節點中 `<Animations>;`，允許數個事件來判斷動畫的執行時間：</span><span class="sxs-lookup"><span data-stu-id="49e7a-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="49e7a-120">`OnClick` （滑鼠按一下）</span><span class="sxs-lookup"><span data-stu-id="49e7a-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="49e7a-121">`OnHoverOut` （當滑鼠離開控制項時）</span><span class="sxs-lookup"><span data-stu-id="49e7a-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="49e7a-122">`OnHoverOver` （當滑鼠停留在控制項上時，停止 `OnHoverOut` 動畫）</span><span class="sxs-lookup"><span data-stu-id="49e7a-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="49e7a-123">`OnLoad` （載入頁面時）</span><span class="sxs-lookup"><span data-stu-id="49e7a-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="49e7a-124">`OnMouseOut` （當滑鼠離開控制項時）</span><span class="sxs-lookup"><span data-stu-id="49e7a-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="49e7a-125">`OnMouseOver` （當滑鼠停留在控制項上時，不會停止 `OnMouseOut` 動畫）</span><span class="sxs-lookup"><span data-stu-id="49e7a-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="49e7a-126">此架構隨附一組動畫，每一個都由自己的 XML 元素表示。</span><span class="sxs-lookup"><span data-stu-id="49e7a-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="49e7a-127">選擇如下：</span><span class="sxs-lookup"><span data-stu-id="49e7a-127">Here is a selection:</span></span>

- <span data-ttu-id="49e7a-128">`<Color>` （變更色彩）</span><span class="sxs-lookup"><span data-stu-id="49e7a-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="49e7a-129">`<FadeIn>` （淡入）</span><span class="sxs-lookup"><span data-stu-id="49e7a-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="49e7a-130">`<FadeOut>` （淡出）</span><span class="sxs-lookup"><span data-stu-id="49e7a-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="49e7a-131">`<Property>` （變更控制項的屬性）</span><span class="sxs-lookup"><span data-stu-id="49e7a-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="49e7a-132">`<Pulse>` （pulsating）</span><span class="sxs-lookup"><span data-stu-id="49e7a-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="49e7a-133">`<Resize>` （變更大小）</span><span class="sxs-lookup"><span data-stu-id="49e7a-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="49e7a-134">`<Scale>` （按比例變更大小）</span><span class="sxs-lookup"><span data-stu-id="49e7a-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="49e7a-135">在此範例中，面板應淡出。動畫應需要1.5 秒（`Duration` 屬性），顯示每秒24個畫面格（動畫步驟）（`Fps` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="49e7a-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="49e7a-136">以下是 `AnimationExtender` 控制項的完整標記：</span><span class="sxs-lookup"><span data-stu-id="49e7a-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="49e7a-137">當您執行此腳本時，會顯示面板並淡出一段半秒。</span><span class="sxs-lookup"><span data-stu-id="49e7a-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="49e7a-138">[![面板會淡出](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="49e7a-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="49e7a-139">此面板會淡出（[按一下以觀看完整大小的影像](adding-animation-to-a-control-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="49e7a-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="49e7a-140">下一個</span><span class="sxs-lookup"><span data-stu-id="49e7a-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
