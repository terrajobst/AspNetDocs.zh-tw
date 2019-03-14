---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: 執行動畫使用用戶端程式碼 (C#) |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 動畫執行...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 5dc5c0b49a3530988bf42d6d632a061622f0a217
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029475"
---
<a name="executing-animations-using-client-side-code-c"></a><span data-ttu-id="58e79-104">使用用戶端程式碼執行動畫 (C#)</span><span class="sxs-lookup"><span data-stu-id="58e79-104">Executing Animations Using Client-Side Code (C#)</span></span>
====================
<span data-ttu-id="58e79-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="58e79-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="58e79-106">[下載程式碼](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip)或[下載 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="58e79-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span></span>

> <span data-ttu-id="58e79-107">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="58e79-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="58e79-108">動畫執行也可能使用自訂用戶端 JavaScript 程式碼會觸發。</span><span class="sxs-lookup"><span data-stu-id="58e79-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="58e79-109">總覽</span><span class="sxs-lookup"><span data-stu-id="58e79-109">Overview</span></span>

<span data-ttu-id="58e79-110">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="58e79-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="58e79-111">動畫執行也可能使用自訂用戶端 JavaScript 程式碼會觸發。</span><span class="sxs-lookup"><span data-stu-id="58e79-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="58e79-112">步驟</span><span class="sxs-lookup"><span data-stu-id="58e79-112">Steps</span></span>

<span data-ttu-id="58e79-113">首先，包括`ScriptManager`單元頁面; 然後，ASP.NET AJAX 程式庫載入，因此能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="58e79-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="58e79-114">動畫將會套用至面板的文字看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="58e79-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="58e79-115">在 [面板] 中相關聯的 CSS 類別，定義好用的背景色彩和也設定面板的固定的寬度：</span><span class="sxs-lookup"><span data-stu-id="58e79-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="58e79-116">然後，新增`AnimationExtender` 頁面上，以提供`ID`，則`TargetControlID`屬性和必要`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="58e79-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="58e79-117">內`<Animations>`節點，請使用`<OnClick>`執行動畫一次使用者按一下面板上。</span><span class="sxs-lookup"><span data-stu-id="58e79-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="58e79-118">新增兩個動畫 parallelly 執行：</span><span class="sxs-lookup"><span data-stu-id="58e79-118">Add two animations to be executed parallelly:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

<span data-ttu-id="58e79-119">為了示範，這個動畫 （和任何其他使用 Control Toolkit 建立的動畫） 執行之後執行網頁時，使用 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="58e79-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="58e79-120">首先我們必須存取`AnimationExtender`控制項。</span><span class="sxs-lookup"><span data-stu-id="58e79-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="58e79-121">ASP.NET AJAX 程式庫提供`$find()`函式，這項工作：</span><span class="sxs-lookup"><span data-stu-id="58e79-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

<span data-ttu-id="58e79-122">`AnimationExtender`控制項會公開豐富的 API，包括具有名稱相同的 XML 標記中所使用的事件處理常式的方法： `OnClick()`， `OnLoad()`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="58e79-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="58e79-123">比方說，呼叫`OnClick()`方法會執行內的動畫`<OnClick>`項目`AnimationExtender`控制項：</span><span class="sxs-lookup"><span data-stu-id="58e79-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

<span data-ttu-id="58e79-124">以下是 頁面完全載入後，模擬面板上的按一下 完成用戶端 JavaScript 程式碼，請注意，`pageLoad()`函式名稱可由呼叫 ASP.NET AJAX 一次頁面和所有包含的 JavaScript 程式庫已載入。</span><span class="sxs-lookup"><span data-stu-id="58e79-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]


<span data-ttu-id="58e79-125">[![動畫會立即執行，而不需要按下滑鼠](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="58e79-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="58e79-126">動畫會立即執行，沒有滑鼠點選 ([按一下以檢視完整大小的影像](executing-animations-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="58e79-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58e79-127">[上一頁](modifying-animations-from-the-server-side-cs.md)
> [下一頁](changing-an-animation-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="58e79-127">[Previous](modifying-animations-from-the-server-side-cs.md)
[Next](changing-an-animation-using-client-side-code-cs.md)</span></span>