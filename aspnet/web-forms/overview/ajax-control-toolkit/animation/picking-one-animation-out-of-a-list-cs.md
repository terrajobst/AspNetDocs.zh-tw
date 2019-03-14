---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 挑選一張動畫從清單中 (C#) |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 此架構也允許...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 9cbbfaefca43a2fb25eec30115bcc4b5112754a9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057855"
---
<a name="picking-one-animation-out-of-a-list-c"></a><span data-ttu-id="00cbe-104">從清單中挑選一張動畫 (C#)</span><span class="sxs-lookup"><span data-stu-id="00cbe-104">Picking One Animation Out Of a List (C#)</span></span>
====================
<span data-ttu-id="00cbe-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="00cbe-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="00cbe-106">[下載程式碼](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip)或[下載 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="00cbe-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span></span>

> <span data-ttu-id="00cbe-107">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="00cbe-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="00cbe-108">架構也可讓程式設計人員挑選一張動畫從清單的動畫，根據一些 JavaScript 程式碼的評估結果。</span><span class="sxs-lookup"><span data-stu-id="00cbe-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="00cbe-109">總覽</span><span class="sxs-lookup"><span data-stu-id="00cbe-109">Overview</span></span>

<span data-ttu-id="00cbe-110">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="00cbe-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="00cbe-111">架構也可讓程式設計人員挑選一張動畫從清單的動畫，根據一些 JavaScript 程式碼的評估結果。</span><span class="sxs-lookup"><span data-stu-id="00cbe-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="00cbe-112">步驟</span><span class="sxs-lookup"><span data-stu-id="00cbe-112">Steps</span></span>

<span data-ttu-id="00cbe-113">首先，包括`ScriptManager`單元頁面; 然後，ASP.NET AJAX 程式庫載入，因此能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="00cbe-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

<span data-ttu-id="00cbe-114">動畫將會套用至面板的文字看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="00cbe-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

<span data-ttu-id="00cbe-115">在 [面板] 中相關聯的 CSS 類別，定義好用的背景色彩和也設定面板的固定的寬度：</span><span class="sxs-lookup"><span data-stu-id="00cbe-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

<span data-ttu-id="00cbe-116">然後，新增`AnimationExtender` 頁面上，以提供`ID`，則`TargetControlID`屬性和必要 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="00cbe-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

<span data-ttu-id="00cbe-117">內`<Animations>`節點，請使用`<OnLoad>`頁面完全載入後，執行動畫。</span><span class="sxs-lookup"><span data-stu-id="00cbe-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="00cbe-118">而不是一個一般的動畫，`<Case>`元素派上用場。</span><span class="sxs-lookup"><span data-stu-id="00cbe-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="00cbe-119">會評估其 SelectScript 屬性的值;傳回的值必須是數字。</span><span class="sxs-lookup"><span data-stu-id="00cbe-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="00cbe-120">根據此數字，其中一個內 subanimations&lt;案例&gt;執行。</span><span class="sxs-lookup"><span data-stu-id="00cbe-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="00cbe-121">比方說，如果 SelectScript 判斷值為 2，Control Toolkit 會執行內的第三個動畫&lt;案例&gt;（從 0 開始）。</span><span class="sxs-lookup"><span data-stu-id="00cbe-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="00cbe-122">下列標記會定義三個 subanimations:調整大小的寬度，調整大小的高度和淡出。JavaScript 程式碼 (`Math.floor(3 * Math.random())`)，讓其中的三種動畫會執行，然後選擇 0 和 2 之間的數字：</span><span class="sxs-lookup"><span data-stu-id="00cbe-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]


<span data-ttu-id="00cbe-123">[![其中一種可能的三個動畫：[面板] 中取得更多](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="00cbe-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span></span>

<span data-ttu-id="00cbe-124">其中一種可能的三個動畫：[面板] 中取得更多 ([按一下以檢視完整大小的影像](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="00cbe-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="00cbe-125">[上一頁](animation-depending-on-a-condition-cs.md)
> [下一頁](animating-in-response-to-user-interaction-cs.md)</span><span class="sxs-lookup"><span data-stu-id="00cbe-125">[Previous](animation-depending-on-a-condition-cs.md)
[Next](animating-in-response-to-user-interaction-cs.md)</span></span>