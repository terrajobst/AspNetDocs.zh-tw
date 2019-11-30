---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: 製作 UpdatePanel 控制項的動畫C#（） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 適用于 ... 的內容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599914"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="ff436-104">繪製 UpdatePanel 控制項的動畫 (C#)</span><span class="sxs-lookup"><span data-stu-id="ff436-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="ff436-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ff436-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ff436-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ff436-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="ff436-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ff436-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ff436-108">對於 UpdatePanel 的內容，有一個特殊的擴充項會高度依賴動畫架構： UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="ff436-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="ff436-109">本教學課程說明如何設定 UpdatePanel 的這類動畫。</span><span class="sxs-lookup"><span data-stu-id="ff436-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="ff436-110">概觀</span><span class="sxs-lookup"><span data-stu-id="ff436-110">Overview</span></span>

<span data-ttu-id="ff436-111">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ff436-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ff436-112">針對 `UpdatePanel`的內容，有一個特殊的擴充項會高度依賴動畫架構： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="ff436-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="ff436-113">本教學課程說明如何設定 `UpdatePanel`的動畫。</span><span class="sxs-lookup"><span data-stu-id="ff436-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="ff436-114">步驟</span><span class="sxs-lookup"><span data-stu-id="ff436-114">Steps</span></span>

<span data-ttu-id="ff436-115">第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="ff436-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="ff436-116">此案例中的動畫將會套用至位於 `UpdatePanel`的 ASP.NET `Wizard` web 控制項。</span><span class="sxs-lookup"><span data-stu-id="ff436-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="ff436-117">三個（任意）步驟提供足夠的選項來觸發回傳：</span><span class="sxs-lookup"><span data-stu-id="ff436-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="ff436-118">`UpdatePanelAnimationExtender` 控制項所需的標記與用於 `AnimationExtender`的標記非常類似。</span><span class="sxs-lookup"><span data-stu-id="ff436-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="ff436-119">在 [`TargetControlID`] 屬性中，我們提供 `UpdatePanel` 的 `ID` 以建立動畫;在 `UpdatePanelAnimationExtender` 控制項內，`<Animations>` 元素會保存動畫的 XML 標記。</span><span class="sxs-lookup"><span data-stu-id="ff436-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="ff436-120">不過，有一項差異：事件和事件處理常式的數量會與 `AnimationExtender`相較之下受到限制。</span><span class="sxs-lookup"><span data-stu-id="ff436-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="ff436-121">針對 `UpdatePanels`，其中只有兩個存在：</span><span class="sxs-lookup"><span data-stu-id="ff436-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="ff436-122">當 UpdatePanel 已更新時 `<OnUpdated>`</span><span class="sxs-lookup"><span data-stu-id="ff436-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="ff436-123">當 UpdatePanel 開始更新時 `<OnUpdating>`</span><span class="sxs-lookup"><span data-stu-id="ff436-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="ff436-124">在此案例中，`UpdatePanel` 的新內容（在回傳之後）應會淡入。</span><span class="sxs-lookup"><span data-stu-id="ff436-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="ff436-125">這是所需的標記：</span><span class="sxs-lookup"><span data-stu-id="ff436-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="ff436-126">現在，每當 UpdatePanel 中出現回傳時，面板的新內容就會順暢地淡入。</span><span class="sxs-lookup"><span data-stu-id="ff436-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="ff436-127">[![下一個 wizard 步驟會淡入](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ff436-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="ff436-128">下一個 wizard 步驟已淡入（[按一下以觀看完整大小的影像](animating-an-updatepanel-control-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="ff436-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ff436-129">[上一頁](changing-an-animation-using-client-side-code-cs.md)
> [下一頁](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ff436-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
