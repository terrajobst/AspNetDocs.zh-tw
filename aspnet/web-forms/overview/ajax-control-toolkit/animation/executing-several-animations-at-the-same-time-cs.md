---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: 同時執行數個動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它允許執行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575369"
---
# <a name="executing-several-animations-at-the-same-time-c"></a><span data-ttu-id="c6185-104">同時執行數個動畫（C#）</span><span class="sxs-lookup"><span data-stu-id="c6185-104">Executing Several Animations at The Same Time (C#)</span></span>

<span data-ttu-id="c6185-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c6185-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c6185-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c6185-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span></span>

> <span data-ttu-id="c6185-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="c6185-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c6185-108">它允許以平行方式執行數個動畫。</span><span class="sxs-lookup"><span data-stu-id="c6185-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="c6185-109">概觀</span><span class="sxs-lookup"><span data-stu-id="c6185-109">Overview</span></span>

<span data-ttu-id="c6185-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="c6185-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c6185-111">它允許以平行方式執行數個動畫。</span><span class="sxs-lookup"><span data-stu-id="c6185-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="c6185-112">步驟</span><span class="sxs-lookup"><span data-stu-id="c6185-112">Steps</span></span>

<span data-ttu-id="c6185-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="c6185-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

<span data-ttu-id="c6185-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c6185-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

<span data-ttu-id="c6185-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="c6185-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

<span data-ttu-id="c6185-116">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="c6185-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

<span data-ttu-id="c6185-117">在 [`<Animations>`] 節點內，一旦頁面完全載入，請使用 `<OnLoad>` 來執行動畫。</span><span class="sxs-lookup"><span data-stu-id="c6185-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="c6185-118">一般來說，`<OnLoad>` 只接受一個動畫。</span><span class="sxs-lookup"><span data-stu-id="c6185-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="c6185-119">動畫架構可讓您使用 `<Parallel>` 元素，將數個動畫聯結至其中一個。</span><span class="sxs-lookup"><span data-stu-id="c6185-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="c6185-120">`<Parallel>` 內的所有動畫都是在同一時間執行。</span><span class="sxs-lookup"><span data-stu-id="c6185-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="c6185-121">以下是 `AnimationExtender` 控制項的可能標記、淡出並同時調整面板大小：</span><span class="sxs-lookup"><span data-stu-id="c6185-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

<span data-ttu-id="c6185-122">事實上：當您執行此腳本時，會顯示面板，然後調整大小（大於增加三倍其寬度並減半其高度）並同時淡出。</span><span class="sxs-lookup"><span data-stu-id="c6185-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="c6185-123">[![面板會淡出並根據瀏覽器的轉譯引擎調整大小（包括其內容）](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c6185-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span></span>

<span data-ttu-id="c6185-124">由於瀏覽器的轉譯引擎，面板會淡出並調整大小（包括其內容）（請[按一下以觀看完整大小的影像](executing-several-animations-at-the-same-time-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c6185-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c6185-125">[上一頁](adding-animation-to-a-control-cs.md)
> [下一頁](executing-several-animations-after-each-other-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c6185-125">[Previous](adding-animation-to-a-control-cs.md)
[Next](executing-several-animations-after-each-other-cs.md)</span></span>
