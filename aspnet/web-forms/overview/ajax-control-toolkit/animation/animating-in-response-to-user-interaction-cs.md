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
# <a name="animating-in-response-to-user-interaction-c"></a><span data-ttu-id="f5bf0-104">根據使用者互動繪製動畫 (C#)</span><span class="sxs-lookup"><span data-stu-id="f5bf0-104">Animating in Response To User Interaction (C#)</span></span>

<span data-ttu-id="f5bf0-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f5bf0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f5bf0-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f5bf0-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span></span>

> <span data-ttu-id="f5bf0-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="f5bf0-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f5bf0-108">動畫可以自動啟動，或可能由使用者互動觸發，例如按一下滑鼠。</span><span class="sxs-lookup"><span data-stu-id="f5bf0-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="f5bf0-109">概觀</span><span class="sxs-lookup"><span data-stu-id="f5bf0-109">Overview</span></span>

<span data-ttu-id="f5bf0-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="f5bf0-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f5bf0-111">動畫可以自動啟動，或可能由使用者互動觸發，例如按一下滑鼠。</span><span class="sxs-lookup"><span data-stu-id="f5bf0-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="f5bf0-112">步驟</span><span class="sxs-lookup"><span data-stu-id="f5bf0-112">Steps</span></span>

<span data-ttu-id="f5bf0-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="f5bf0-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

<span data-ttu-id="f5bf0-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5bf0-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

<span data-ttu-id="f5bf0-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="f5bf0-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

<span data-ttu-id="f5bf0-116">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="f5bf0-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

<span data-ttu-id="f5bf0-117">在 [`<Animations>`] 節點中，有五種方式可透過使用者互動來啟動動畫（遺失的元素是 `<OnLoad>`，一旦整個頁面完全載入，就會執行此動作）：</span><span class="sxs-lookup"><span data-stu-id="f5bf0-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="f5bf0-118">`<OnClick>` （滑鼠按一下控制項）</span><span class="sxs-lookup"><span data-stu-id="f5bf0-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="f5bf0-119">`<OnHoverOut>` （滑鼠離開控制項）</span><span class="sxs-lookup"><span data-stu-id="f5bf0-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="f5bf0-120">`<OnHoverOver>` （滑鼠停留在控制項上，停止 `<OnHoverOut>` 動畫）</span><span class="sxs-lookup"><span data-stu-id="f5bf0-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="f5bf0-121">`<OnMouseOut>` （滑鼠離開控制項）</span><span class="sxs-lookup"><span data-stu-id="f5bf0-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="f5bf0-122">`<OnMouseOver>` （滑鼠停留在控制項上，而不是停止 `<OnMouseOut>` 動畫）</span><span class="sxs-lookup"><span data-stu-id="f5bf0-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="f5bf0-123">在此案例中，會使用 `<OnClick>`。</span><span class="sxs-lookup"><span data-stu-id="f5bf0-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="f5bf0-124">當使用者按一下面板時，會將其調整大小並淡出一次。</span><span class="sxs-lookup"><span data-stu-id="f5bf0-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

<span data-ttu-id="f5bf0-125">[![按一下滑鼠，就會啟動動畫](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f5bf0-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span></span>

<span data-ttu-id="f5bf0-126">按一下滑鼠即可啟動動畫（[按一下以觀看完整大小的影像](animating-in-response-to-user-interaction-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="f5bf0-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f5bf0-127">[上一頁](picking-one-animation-out-of-a-list-cs.md)
> [下一頁](disabling-actions-during-animation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f5bf0-127">[Previous](picking-one-animation-out-of-a-list-cs.md)
[Next](disabling-actions-during-animation-cs.md)</span></span>
