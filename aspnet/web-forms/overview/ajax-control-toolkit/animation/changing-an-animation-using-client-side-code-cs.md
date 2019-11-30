---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: 使用用戶端程式代碼變更動畫（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。 動畫也可以 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606960"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="ec949-104">使用用戶端程式碼變更動畫 (C#)</span><span class="sxs-lookup"><span data-stu-id="ec949-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="ec949-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ec949-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ec949-106">[下載程式代碼](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip)或[下載 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ec949-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="ec949-107">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ec949-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ec949-108">您也可以使用自訂用戶端 JavaScript 程式碼來變更動畫。</span><span class="sxs-lookup"><span data-stu-id="ec949-108">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="ec949-109">概觀</span><span class="sxs-lookup"><span data-stu-id="ec949-109">Overview</span></span>

<span data-ttu-id="ec949-110">ASP.NET AJAX 控制項工具組中的動畫控制項不只是控制項，而是可將動畫新增至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="ec949-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ec949-111">您也可以使用自訂用戶端 JavaScript 程式碼來變更動畫。</span><span class="sxs-lookup"><span data-stu-id="ec949-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="ec949-112">步驟</span><span class="sxs-lookup"><span data-stu-id="ec949-112">Steps</span></span>

<span data-ttu-id="ec949-113">首先，在頁面中包含 `ScriptManager`;然後，會載入 ASP.NET AJAX 程式庫，讓您能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="ec949-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="ec949-114">動畫將會套用至文字的面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ec949-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="ec949-115">在面板的相關聯 CSS 類別中，定義良好的背景色彩，同時設定面板的固定寬度：</span><span class="sxs-lookup"><span data-stu-id="ec949-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="ec949-116">實際的動畫是由 HTML 按鈕啟動：</span><span class="sxs-lookup"><span data-stu-id="ec949-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="ec949-117">然後，將 `AnimationExtender` 新增至頁面，並提供 `ID`、`TargetControlID` 屬性和必要 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="ec949-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="ec949-118">請注意，`AnimationExtender` 控制項內沒有 `<Animations>` 節點。</span><span class="sxs-lookup"><span data-stu-id="ec949-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="ec949-119">自訂 JavaScript 程式碼是用來提供要與控制項搭配使用的動畫。</span><span class="sxs-lookup"><span data-stu-id="ec949-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="ec949-120">就像 `AnimationExtender`的伺服器 API 一樣，也沒有簡單的方法可以將動畫指派給擴充項。</span><span class="sxs-lookup"><span data-stu-id="ec949-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="ec949-121">不過，擴充項會公開數個方法來讀取和寫入以各種事件（`OnClick`、`OnLoad`等等）註冊的動畫。</span><span class="sxs-lookup"><span data-stu-id="ec949-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="ec949-122">以下是一些範例：</span><span class="sxs-lookup"><span data-stu-id="ec949-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="ec949-123">`get_*()` 函式的傳回值格式和 `set_*()` 函數的引數格式為 JSON 字串，提供 XML 標記的物件標記法。</span><span class="sxs-lookup"><span data-stu-id="ec949-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="ec949-124">目前，沒有任何方法可以在中傳遞物件，但可以從指定的動畫（`get_OnXXXBehavior()` 方法）讀取物件。</span><span class="sxs-lookup"><span data-stu-id="ec949-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="ec949-125">以下是 JSON 字串（不含分隔的引號和格式），代表按鈕所觸發的動畫，但會以動畫顯示面板的方式來調整其大小，並同時淡出它：</span><span class="sxs-lookup"><span data-stu-id="ec949-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="ec949-126">下列 JavaScript 程式碼會將此 JSON descripting 指派給目前擴充項的 `OnClick` 動畫，並加以執行：</span><span class="sxs-lookup"><span data-stu-id="ec949-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

<span data-ttu-id="ec949-127">[![動畫立即執行，而不需按下滑鼠（且標記非常少）](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ec949-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="ec949-128">動畫會立即執行，而不需要按一下滑鼠（而且標記很少）（[按一下即可觀看完整大小的影像](changing-an-animation-using-client-side-code-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="ec949-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ec949-129">[上一頁](executing-animations-using-client-side-code-cs.md)
> [下一頁](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ec949-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
