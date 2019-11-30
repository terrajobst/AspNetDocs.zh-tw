---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: 動畫期間停用動作（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 它也支援動作 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606823"
---
# <a name="disabling-actions-during-animation-vb"></a><span data-ttu-id="c0655-104">動畫播放期間停用動作 (VB)</span><span class="sxs-lookup"><span data-stu-id="c0655-104">Disabling Actions during Animation (VB)</span></span>

<span data-ttu-id="c0655-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c0655-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c0655-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c0655-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span></span>

> <span data-ttu-id="c0655-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="c0655-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c0655-108">它也支援動作，例如滑鼠點擊。</span><span class="sxs-lookup"><span data-stu-id="c0655-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="c0655-109">不過，當滑鼠按一下啟動動畫時，最好在動畫期間停用滑鼠點按動作。</span><span class="sxs-lookup"><span data-stu-id="c0655-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="c0655-110">概觀</span><span class="sxs-lookup"><span data-stu-id="c0655-110">Overview</span></span>

<span data-ttu-id="c0655-111">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="c0655-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c0655-112">它也支援動作，例如滑鼠點擊。</span><span class="sxs-lookup"><span data-stu-id="c0655-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="c0655-113">不過，當滑鼠按一下啟動動畫時，最好在動畫期間停用滑鼠點按動作。</span><span class="sxs-lookup"><span data-stu-id="c0655-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="c0655-114">步驟</span><span class="sxs-lookup"><span data-stu-id="c0655-114">Steps</span></span>

<span data-ttu-id="c0655-115">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="c0655-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

<span data-ttu-id="c0655-116">動畫將會套用至 HTML 按鈕，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0655-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

<span data-ttu-id="c0655-117">請注意，HTML 控制項是用來取代 Web 控制項，因為我們不想要讓按鈕建立回傳。它應該只為我們啟動用戶端動畫。</span><span class="sxs-lookup"><span data-stu-id="c0655-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="c0655-118">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="c0655-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

<span data-ttu-id="c0655-119">在 [`<Animations>`] 節點內，`<OnClick>` 是用來處理滑鼠點按的右元素。</span><span class="sxs-lookup"><span data-stu-id="c0655-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="c0655-120">不過，在動畫期間也可以按一下按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0655-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="c0655-121">`<EnableAction>` 元素可以處理這一點。</span><span class="sxs-lookup"><span data-stu-id="c0655-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="c0655-122">設定 `Enabled="false"` 會停用按鈕作為動畫的一部分。</span><span class="sxs-lookup"><span data-stu-id="c0655-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="c0655-123">由於我們使用數個個別的動畫（停用按鈕和實際的動畫），因此需要 `<Parallel>` 元素，將單一動畫一併放到一個。</span><span class="sxs-lookup"><span data-stu-id="c0655-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="c0655-124">以下是 `AnimationExtender`的完整標記：</span><span class="sxs-lookup"><span data-stu-id="c0655-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

<span data-ttu-id="c0655-125">您也可以使用清單結尾的下列 XML 元素，在動畫之後重新啟用 [到] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="c0655-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

<span data-ttu-id="c0655-126">不過在給定的案例中，這會很無用，因為按鈕會淡出，而且在動畫結束時看不到。</span><span class="sxs-lookup"><span data-stu-id="c0655-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="c0655-127">[![在動畫執行時立即停用按鈕](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c0655-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span></span>

<span data-ttu-id="c0655-128">動畫執行時，按鈕會立即停用（[按一下以觀看完整大小的影像](disabling-actions-during-animation-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c0655-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c0655-129">[上一頁](animating-in-response-to-user-interaction-vb.md)
> [下一頁](triggering-an-animation-in-another-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c0655-129">[Previous](animating-in-response-to-user-interaction-vb.md)
[Next](triggering-an-animation-in-another-control-vb.md)</span></span>
