---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 使用用戶端程式代碼執行動畫（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫執行中 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575497"
---
# <a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="bae2d-104">使用用戶端程式碼執行動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="bae2d-104">Executing Animations Using Client-Side Code (VB)</span></span>

<span data-ttu-id="bae2d-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="bae2d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="bae2d-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="bae2d-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="bae2d-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="bae2d-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="bae2d-108">也可以使用自訂用戶端 JavaScript 程式碼觸發動畫執行。</span><span class="sxs-lookup"><span data-stu-id="bae2d-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="bae2d-109">概觀</span><span class="sxs-lookup"><span data-stu-id="bae2d-109">Overview</span></span>

<span data-ttu-id="bae2d-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="bae2d-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="bae2d-111">也可以使用自訂用戶端 JavaScript 程式碼觸發動畫執行。</span><span class="sxs-lookup"><span data-stu-id="bae2d-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="bae2d-112">步驟</span><span class="sxs-lookup"><span data-stu-id="bae2d-112">Steps</span></span>

<span data-ttu-id="bae2d-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="bae2d-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="bae2d-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bae2d-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="bae2d-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="bae2d-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="bae2d-116">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="bae2d-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="bae2d-117">在 [`<Animations>`] 節點中，當使用者按一下面板後，使用 `<OnClick>` 來執行動畫。</span><span class="sxs-lookup"><span data-stu-id="bae2d-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="bae2d-118">新增要平行執行的兩個動畫：</span><span class="sxs-lookup"><span data-stu-id="bae2d-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="bae2d-119">為了示範，這個動畫（以及使用控制項工具組所建立的任何其他動畫）會在頁面執行之後，使用 JavaScript 程式碼執行。</span><span class="sxs-lookup"><span data-stu-id="bae2d-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="bae2d-120">首先，我們需要 `AnimationExtender` 控制項的存取權。</span><span class="sxs-lookup"><span data-stu-id="bae2d-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="bae2d-121">ASP.NET AJAX 程式庫提供這項工作的 `$find()` 函式：</span><span class="sxs-lookup"><span data-stu-id="bae2d-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="bae2d-122">`AnimationExtender` 控制項會公開豐富的 API，包括名稱與 XML 標記中所用事件處理常式相同的方法： `OnClick()`、`OnLoad()`等等。</span><span class="sxs-lookup"><span data-stu-id="bae2d-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="bae2d-123">例如，`OnClick()` 方法的呼叫會在 `AnimationExtender` 控制項的 `<OnClick>` 元素內執行動畫：</span><span class="sxs-lookup"><span data-stu-id="bae2d-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="bae2d-124">以下是完整載入頁面後，會模擬面板上按一下的完整用戶端 JavaScript 程式碼，請注意 `pageLoad()`，ASP.NET AJAX 會在頁面上載入所有包含的 JavaScript 程式庫之後，使用此名稱來呼叫。</span><span class="sxs-lookup"><span data-stu-id="bae2d-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

<span data-ttu-id="bae2d-125">[![動畫立即執行，而不需按滑鼠按鍵](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bae2d-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="bae2d-126">動畫會立即執行，而不需要按一下滑鼠（[按一下以觀看完整大小的影像](executing-animations-using-client-side-code-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="bae2d-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bae2d-127">[上一頁](modifying-animations-from-the-server-side-vb.md)
> [下一頁](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="bae2d-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
