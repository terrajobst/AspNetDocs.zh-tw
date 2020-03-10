---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 觸發另一個控制項中的動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 一般來說，啟動 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536068"
---
# <a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="60367-104">觸發另一個控制項中的動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="60367-104">Triggering an Animation in another Control (VB)</span></span>

<span data-ttu-id="60367-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="60367-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="60367-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="60367-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="60367-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="60367-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="60367-108">一般來說，啟動動畫是由與相同控制項的使用者互動所觸發。</span><span class="sxs-lookup"><span data-stu-id="60367-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="60367-109">不過，您也可以與一個控制項互動，然後再動畫另一個控制項。</span><span class="sxs-lookup"><span data-stu-id="60367-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="60367-110">概觀</span><span class="sxs-lookup"><span data-stu-id="60367-110">Overview</span></span>

<span data-ttu-id="60367-111">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="60367-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="60367-112">一般來說，啟動動畫是由與相同控制項的使用者互動所觸發。</span><span class="sxs-lookup"><span data-stu-id="60367-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="60367-113">不過，您也可以與一個控制項互動，然後再動畫另一個控制項。</span><span class="sxs-lookup"><span data-stu-id="60367-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="60367-114">步驟</span><span class="sxs-lookup"><span data-stu-id="60367-114">Steps</span></span>

<span data-ttu-id="60367-115">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="60367-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="60367-116">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="60367-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="60367-117">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="60367-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="60367-118">為了開始繪製面板的動畫，會使用 HTML 按鈕。</span><span class="sxs-lookup"><span data-stu-id="60367-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="60367-119">請注意，`<input type="button" />` 是透過 `<asp:Button />` favoured，因為當使用者按一下該按鈕時，不會進行回傳。</span><span class="sxs-lookup"><span data-stu-id="60367-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="60367-120">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`。</span><span class="sxs-lookup"><span data-stu-id="60367-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="60367-121">請務必將 `TargetControlID` 設定為按鈕（觸發動畫的元素）的識別碼，而不是將面板的識別碼（要進行動畫的專案）設為</span><span class="sxs-lookup"><span data-stu-id="60367-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="60367-122">在 [`<Animations>`] 節點內，如往常般放置動畫。</span><span class="sxs-lookup"><span data-stu-id="60367-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="60367-123">為了讓它們變更面板，而不是按鈕，請在 `AnimationExtender`內設定每個動畫元素的 `AnimationTarget` 屬性。</span><span class="sxs-lookup"><span data-stu-id="60367-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="60367-124">當然，`AnimationTarget` 的值是面板的識別碼。</span><span class="sxs-lookup"><span data-stu-id="60367-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="60367-125">如此一來，就會在面板中出現動畫，而不是使用 [觸發] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="60367-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="60367-126">以下是此案例的 `AnimationExtender` 標記：</span><span class="sxs-lookup"><span data-stu-id="60367-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="60367-127">請注意個別動畫出現的特殊順序。</span><span class="sxs-lookup"><span data-stu-id="60367-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="60367-128">首先，按鈕會在動畫執行後停用。</span><span class="sxs-lookup"><span data-stu-id="60367-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="60367-129">因為 `<EnableAction>` 元素中沒有 `AnimationTarget` 屬性，所以這個動畫會套用至原始控制項：按鈕。</span><span class="sxs-lookup"><span data-stu-id="60367-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="60367-130">接下來的兩個動畫步驟應該以平行方式執行（`<Parallel>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="60367-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="60367-131">兩者的 `AnimationTarget` 屬性都設定為 `"Panel1"`，因此會以動畫顯示面板，而不是按鈕。</span><span class="sxs-lookup"><span data-stu-id="60367-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="60367-132">[![滑鼠按一下按鈕時，就會啟動面板動畫](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="60367-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="60367-133">當滑鼠按一下按鈕時，就會啟動面板動畫（[按一下以查看完整大小的影像](triggering-an-animation-in-another-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="60367-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="60367-134">[上一頁](disabling-actions-during-animation-vb.md)
> [下一頁](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="60367-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
