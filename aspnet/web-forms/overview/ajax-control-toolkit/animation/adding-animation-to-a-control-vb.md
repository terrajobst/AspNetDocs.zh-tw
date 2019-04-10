---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: 將動畫加入至控制項 (VB) |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 本教學課程示範如何...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: c55bbeb383b15f4dc9cb95d25905cade1e8c5c29
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418894"
---
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="ae72b-104">將動畫新增至控制項 (VB)</span><span class="sxs-lookup"><span data-stu-id="ae72b-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="ae72b-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ae72b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ae72b-106">[下載程式碼](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip)或[下載 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ae72b-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="ae72b-107">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ae72b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ae72b-108">本教學課程會示範如何設定這類動畫。</span><span class="sxs-lookup"><span data-stu-id="ae72b-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="ae72b-109">總覽</span><span class="sxs-lookup"><span data-stu-id="ae72b-109">Overview</span></span>

<span data-ttu-id="ae72b-110">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ae72b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ae72b-111">本教學課程會示範如何設定這類動畫。</span><span class="sxs-lookup"><span data-stu-id="ae72b-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="ae72b-112">步驟</span><span class="sxs-lookup"><span data-stu-id="ae72b-112">Steps</span></span>

<span data-ttu-id="ae72b-113">如往常般的第一個步驟是加入`ScriptManager`頁面中，讓 ASP.NET AJAX 程式庫已載入，並控制工具組可以用於：</span><span class="sxs-lookup"><span data-stu-id="ae72b-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="ae72b-114">在此案例中的動畫將會套用至面板的文字看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ae72b-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="ae72b-115">面板相關聯的 CSS 類別定義的背景色彩和寬度：</span><span class="sxs-lookup"><span data-stu-id="ae72b-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="ae72b-116">接下來，我們需要`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="ae72b-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="ae72b-117">提供之後`ID`和一般`runat="server"`，則`TargetControlID`屬性必須設定為控制項，以在我們的案例中，[面板] 中建立動畫：</span><span class="sxs-lookup"><span data-stu-id="ae72b-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="ae72b-118">整個套用該動畫以宣告方式，使用 XML 語法，不幸的是目前不完全受到 Visual Studio's IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ae72b-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="ae72b-119">根節點是`<Animations>;`此節點中，內有多個事件允許用來決定當 animation(s) take(s) 位置：</span><span class="sxs-lookup"><span data-stu-id="ae72b-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- `OnClick` <span data-ttu-id="ae72b-120">（按一下滑鼠）</span><span class="sxs-lookup"><span data-stu-id="ae72b-120">(mouse click)</span></span>
- `OnHoverOut` <span data-ttu-id="ae72b-121">（當滑鼠離開控制項）</span><span class="sxs-lookup"><span data-stu-id="ae72b-121">(when the mouse leaves a control)</span></span>
- `OnHoverOver` <span data-ttu-id="ae72b-122">(當滑鼠停留在控制項時，停止`OnHoverOut`動畫)</span><span class="sxs-lookup"><span data-stu-id="ae72b-122">(when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- `OnLoad` <span data-ttu-id="ae72b-123">（當頁面已載入）</span><span class="sxs-lookup"><span data-stu-id="ae72b-123">(when the page has been loaded)</span></span>
- `OnMouseOut` <span data-ttu-id="ae72b-124">（當滑鼠離開控制項）</span><span class="sxs-lookup"><span data-stu-id="ae72b-124">(when the mouse leaves a control)</span></span>
- `OnMouseOver` <span data-ttu-id="ae72b-125">(當滑鼠停留在控制項時，不會 」 停止`OnMouseOut`動畫)</span><span class="sxs-lookup"><span data-stu-id="ae72b-125">(when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="ae72b-126">此架構隨附一組動畫，由它自己的 XML 項目表示每一個。</span><span class="sxs-lookup"><span data-stu-id="ae72b-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="ae72b-127">以下是選取項目：</span><span class="sxs-lookup"><span data-stu-id="ae72b-127">Here is a selection:</span></span>

- `<Color>` <span data-ttu-id="ae72b-128">（變更色彩）</span><span class="sxs-lookup"><span data-stu-id="ae72b-128">(changing a color)</span></span>
- `<FadeIn>` <span data-ttu-id="ae72b-129">（淡入）</span><span class="sxs-lookup"><span data-stu-id="ae72b-129">(fading in)</span></span>
- `<FadeOut>` <span data-ttu-id="ae72b-130">（淡出）</span><span class="sxs-lookup"><span data-stu-id="ae72b-130">(fading out)</span></span>
- `<Property>` <span data-ttu-id="ae72b-131">（變更控制項的屬性）</span><span class="sxs-lookup"><span data-stu-id="ae72b-131">(changing a control's property)</span></span>
- `<Pulse>` <span data-ttu-id="ae72b-132">(pulsating)</span><span class="sxs-lookup"><span data-stu-id="ae72b-132">(pulsating)</span></span>
- `<Resize>` <span data-ttu-id="ae72b-133">（變更大小）</span><span class="sxs-lookup"><span data-stu-id="ae72b-133">(changing the size)</span></span>
- `<Scale>` <span data-ttu-id="ae72b-134">（按比例變更大小）</span><span class="sxs-lookup"><span data-stu-id="ae72b-134">(proportionally changing the size)</span></span>

<span data-ttu-id="ae72b-135">在此範例中，[面板] 中應該會淡出。動畫應採用 1.5 秒 (`Duration`屬性)，顯示每秒 24 畫面格數 （動畫步驟） (`Fps`屬性)。</span><span class="sxs-lookup"><span data-stu-id="ae72b-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="ae72b-136">以下是完成標記`AnimationExtender`控制項：</span><span class="sxs-lookup"><span data-stu-id="ae72b-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="ae72b-137">當您執行此指令碼時，面板會顯示，而且在一個半秒內淡出。</span><span class="sxs-lookup"><span data-stu-id="ae72b-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


[![T<span data-ttu-id="ae72b-138">他面板漸淡]</span><span class="sxs-lookup"><span data-stu-id="ae72b-138">he panel is fading out]</span></span>(adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

<span data-ttu-id="ae72b-139">面板淡出 ([按一下以檢視完整大小的影像](adding-animation-to-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ae72b-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ae72b-140">[上一頁](dynamically-controlling-updatepanel-animations-cs.md)
> [下一頁](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ae72b-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
