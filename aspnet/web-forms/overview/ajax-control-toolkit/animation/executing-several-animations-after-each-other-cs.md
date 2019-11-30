---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: 多次執行數個動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許執行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: e378ac038796dbd44e89d099532b9e186dcf673f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575409"
---
# <a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="c19f6-104">接續執行數個動畫 (C#)</span><span class="sxs-lookup"><span data-stu-id="c19f6-104">Executing Several Animations after Each Other (C#)</span></span>

<span data-ttu-id="c19f6-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c19f6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c19f6-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c19f6-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="c19f6-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="c19f6-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c19f6-108">它允許逐一執行數個動畫。</span><span class="sxs-lookup"><span data-stu-id="c19f6-108">It allows to run several animations one after the other.</span></span>

<span data-ttu-id="c19f6-109">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="c19f6-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c19f6-110">它允許逐一執行數個動畫。</span><span class="sxs-lookup"><span data-stu-id="c19f6-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="c19f6-111">步驟</span><span class="sxs-lookup"><span data-stu-id="c19f6-111">Steps</span></span>

<span data-ttu-id="c19f6-112">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="c19f6-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="c19f6-113">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c19f6-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="c19f6-114">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="c19f6-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="c19f6-115">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="c19f6-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="c19f6-116">在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。</span><span class="sxs-lookup"><span data-stu-id="c19f6-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="c19f6-117">一般來說，`<OnLoad>` 只接受一個動畫。</span><span class="sxs-lookup"><span data-stu-id="c19f6-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="c19f6-118">動畫架構可讓您使用 `<Sequence>` 元素，將數個動畫聯結至其中一個。</span><span class="sxs-lookup"><span data-stu-id="c19f6-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="c19f6-119">`<Sequence>` 內的所有動畫都會逐一執行。</span><span class="sxs-lookup"><span data-stu-id="c19f6-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="c19f6-120">以下是 `AnimationExtender` 控制項的可能標記，先使面板變寬，然後減少其高度：</span><span class="sxs-lookup"><span data-stu-id="c19f6-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="c19f6-121">當您執行此腳本時，面板會先變寬，然後再變小。</span><span class="sxs-lookup"><span data-stu-id="c19f6-121">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="c19f6-122">[![先增加寬度](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c19f6-122">[![First the width is increased](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span></span>

<span data-ttu-id="c19f6-123">首先會增加寬度（[按一下以查看完整大小的影像](executing-several-animations-after-each-other-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c19f6-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>

<span data-ttu-id="c19f6-124">[![，則高度會減少](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c19f6-124">[![Then the height is decreased](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span></span>

<span data-ttu-id="c19f6-125">然後會減少高度（[按一下以觀看完整大小的影像](executing-several-animations-after-each-other-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="c19f6-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c19f6-126">[上一頁](executing-several-animations-at-the-same-time-cs.md)
> [下一頁](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c19f6-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
