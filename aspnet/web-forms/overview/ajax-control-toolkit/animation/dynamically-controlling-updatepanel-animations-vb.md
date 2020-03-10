---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: 動態控制 UpdatePanel 動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 適用于 ... 的內容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 97a52bd75fdf63ad62282afd9df772f0a9e4f931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536152"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="84e1e-104">以動態方式控制 UpdatePanel 動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="84e1e-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>

<span data-ttu-id="84e1e-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="84e1e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="84e1e-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="84e1e-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="84e1e-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="84e1e-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="84e1e-108">對於 UpdatePanel 的內容，有一個特殊的擴充項會高度依賴動畫架構： UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="84e1e-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="84e1e-109">它也可以搭配 UpdatePanel 觸發程式一起使用。</span><span class="sxs-lookup"><span data-stu-id="84e1e-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="84e1e-110">概觀</span><span class="sxs-lookup"><span data-stu-id="84e1e-110">Overview</span></span>

<span data-ttu-id="84e1e-111">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="84e1e-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="84e1e-112">針對 `UpdatePanel`的內容，有一個特殊的擴充項會高度依賴動畫架構： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="84e1e-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="84e1e-113">它也可以搭配 `UpdatePanel` 觸發程式一起使用。</span><span class="sxs-lookup"><span data-stu-id="84e1e-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="84e1e-114">步驟</span><span class="sxs-lookup"><span data-stu-id="84e1e-114">Steps</span></span>

<span data-ttu-id="84e1e-115">第一個步驟通常是在頁面中包含 `ScriptManager`，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="84e1e-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="84e1e-116">此案例中的動畫將會套用至目前時間的顯示。</span><span class="sxs-lookup"><span data-stu-id="84e1e-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="84e1e-117">您可以使用 `Page_Load()` 方法將這項資訊寫入標籤，或（為了簡單起見）使用下列內嵌程式碼：</span><span class="sxs-lookup"><span data-stu-id="84e1e-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="84e1e-118">此外，也會建立觸發更新時間的按鈕：</span><span class="sxs-lookup"><span data-stu-id="84e1e-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="84e1e-119">然後，此程式碼會放入 `UpdatePanel` 元素的 `<ContentTemplate>` 區段中。</span><span class="sxs-lookup"><span data-stu-id="84e1e-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="84e1e-120">面板的 [`UpdateMode`] 屬性必須設定為 [`"Conditional"`]，因為只有觸發程式可以更新面板的內容。</span><span class="sxs-lookup"><span data-stu-id="84e1e-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="84e1e-121">在 `UpdatePanel`的 [`<Triggers>`] 區段中，會建立異步回傳觸發程式，並將其系結至按鈕的 `Click` 事件。</span><span class="sxs-lookup"><span data-stu-id="84e1e-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="84e1e-122">因此，如果使用者按一下按鈕，就會重新整理 `UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="84e1e-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="84e1e-123">以下是 `UpdatePanel` 控制項的標記：</span><span class="sxs-lookup"><span data-stu-id="84e1e-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="84e1e-124">最後，必須設定 `UpdatePanelAnimationExtender`：將 `TargetControlID` 屬性設為面板的識別碼，並在擴充項內定義動畫。</span><span class="sxs-lookup"><span data-stu-id="84e1e-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="84e1e-125">淡入有意義，這會在更新的時間建立美觀的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="84e1e-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="84e1e-126">您的擴充項標記可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="84e1e-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="84e1e-127">在瀏覽器中執行檔案。</span><span class="sxs-lookup"><span data-stu-id="84e1e-127">Run the file in the browser.</span></span> <span data-ttu-id="84e1e-128">當您按一下按鈕時，目前的時間會顯示在面板中，而在一秒的期間內，一律會淡入。</span><span class="sxs-lookup"><span data-stu-id="84e1e-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="84e1e-129">[![目前的時間漸淡](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="84e1e-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="84e1e-130">目前時間已淡入（[按一下以觀看完整大小的影像](dynamically-controlling-updatepanel-animations-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="84e1e-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="84e1e-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="84e1e-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
