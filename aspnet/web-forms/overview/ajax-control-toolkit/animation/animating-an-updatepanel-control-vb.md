---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: 製作 UpdatePanel 控制項的動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 適用于 ... 的內容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536334"
---
# <a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="306bf-104">繪製 UpdatePanel 控制項的動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="306bf-104">Animating an UpdatePanel Control (VB)</span></span>

<span data-ttu-id="306bf-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="306bf-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="306bf-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="306bf-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="306bf-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="306bf-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="306bf-108">對於 UpdatePanel 的內容，有一個特殊的擴充項會高度依賴動畫架構： UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="306bf-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="306bf-109">本教學課程說明如何設定 UpdatePanel 的這類動畫。</span><span class="sxs-lookup"><span data-stu-id="306bf-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="306bf-110">概觀</span><span class="sxs-lookup"><span data-stu-id="306bf-110">Overview</span></span>

<span data-ttu-id="306bf-111">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="306bf-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="306bf-112">針對 `UpdatePanel`的內容，有一個特殊的擴充項會高度依賴動畫架構： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="306bf-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="306bf-113">本教學課程說明如何設定 `UpdatePanel`的動畫。</span><span class="sxs-lookup"><span data-stu-id="306bf-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="306bf-114">步驟</span><span class="sxs-lookup"><span data-stu-id="306bf-114">Steps</span></span>

<span data-ttu-id="306bf-115">第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="306bf-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="306bf-116">此案例中的動畫將會套用至位於 `UpdatePanel`的 ASP.NET `Wizard` web 控制項。</span><span class="sxs-lookup"><span data-stu-id="306bf-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="306bf-117">三個（任意）步驟提供足夠的選項來觸發回傳：</span><span class="sxs-lookup"><span data-stu-id="306bf-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="306bf-118">`UpdatePanelAnimationExtender` 控制項所需的標記與用於 `AnimationExtender`的標記非常類似。</span><span class="sxs-lookup"><span data-stu-id="306bf-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="306bf-119">在 [`TargetControlID`] 屬性中，我們提供 `UpdatePanel` 的 `ID` 以建立動畫;在 `UpdatePanelAnimationExtender` 控制項內，`<Animations>` 元素會保存動畫的 XML 標記。</span><span class="sxs-lookup"><span data-stu-id="306bf-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="306bf-120">不過，有一項差異：事件和事件處理常式的數量會與 `AnimationExtender`相較之下受到限制。</span><span class="sxs-lookup"><span data-stu-id="306bf-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="306bf-121">針對 `UpdatePanels`，其中只有兩個存在：</span><span class="sxs-lookup"><span data-stu-id="306bf-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="306bf-122">當 UpdatePanel 已更新時 `<OnUpdated>`</span><span class="sxs-lookup"><span data-stu-id="306bf-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="306bf-123">當 UpdatePanel 開始更新時 `<OnUpdating>`</span><span class="sxs-lookup"><span data-stu-id="306bf-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="306bf-124">在此案例中，`UpdatePanel` 的新內容（在回傳之後）應會淡入。</span><span class="sxs-lookup"><span data-stu-id="306bf-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="306bf-125">這是所需的標記：</span><span class="sxs-lookup"><span data-stu-id="306bf-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="306bf-126">現在，每當 UpdatePanel 中出現回傳時，面板的新內容就會順暢地淡入。</span><span class="sxs-lookup"><span data-stu-id="306bf-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="306bf-127">[![下一個 wizard 步驟會淡入](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="306bf-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="306bf-128">下一個 wizard 步驟已淡入（[按一下以觀看完整大小的影像](animating-an-updatepanel-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="306bf-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="306bf-129">[上一頁](changing-an-animation-using-client-side-code-vb.md)
> [下一頁](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="306bf-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>
