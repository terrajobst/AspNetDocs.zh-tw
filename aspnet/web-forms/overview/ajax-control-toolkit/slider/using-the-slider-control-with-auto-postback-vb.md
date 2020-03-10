---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 使用滑杆控制項搭配自動回傳（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 可以讓滑杆 autopost 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553561"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="424ae-104">使用滑杆控制項搭配自動回傳（VB）</span><span class="sxs-lookup"><span data-stu-id="424ae-104">Using the Slider Control With Auto-Postback (VB)</span></span>

<span data-ttu-id="424ae-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="424ae-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="424ae-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="424ae-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="424ae-107">AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="424ae-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="424ae-108">它的值變更後，可以讓滑杆 autopostback。</span><span class="sxs-lookup"><span data-stu-id="424ae-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="424ae-109">概觀</span><span class="sxs-lookup"><span data-stu-id="424ae-109">Overview</span></span>

<span data-ttu-id="424ae-110">AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="424ae-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="424ae-111">它的值變更後，可以讓滑杆 autopostback。</span><span class="sxs-lookup"><span data-stu-id="424ae-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="424ae-112">步驟</span><span class="sxs-lookup"><span data-stu-id="424ae-112">Steps</span></span>

<span data-ttu-id="424ae-113">為了讓滑杆在變更時自動回傳，這兩個文字方塊都需要屬性 `AutoPostBack="true"`：將成為滑杆本身的文字方塊，以及保留滑杆位置的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="424ae-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="424ae-114">以下是所需的標記：</span><span class="sxs-lookup"><span data-stu-id="424ae-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="424ae-115">ASP.NET AJAX 控制項工具組中的 `SliderExtender` 控制項，會將滑杆功能指派給這兩個文字方塊：</span><span class="sxs-lookup"><span data-stu-id="424ae-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="424ae-116">稍後會使用其他的 label 元素來通知使用者回傳：</span><span class="sxs-lookup"><span data-stu-id="424ae-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="424ae-117">最後，ASP.NET AJAX 的 `ScriptManager` 控制項會載入必要的 JavaScript，讓控制項工具組能夠正常執行：</span><span class="sxs-lookup"><span data-stu-id="424ae-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="424ae-118">現在滑杆回傳了;在伺服器端，此事件可能會被攔截並採取下列動作：</span><span class="sxs-lookup"><span data-stu-id="424ae-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

<span data-ttu-id="424ae-119">[移動滑杆的 ![會觸發回傳](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="424ae-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="424ae-120">移動滑杆會觸發回傳（[按一下以觀看完整大小的影像](using-the-slider-control-with-auto-postback-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="424ae-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>

<span data-ttu-id="424ae-121">[![之後，這項變更的日期會寫入至標籤](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="424ae-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="424ae-122">之後，這項變更的日期會寫入標籤（[按一下以查看完整大小的影像](using-the-slider-control-with-auto-postback-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="424ae-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="424ae-123">[上一頁](databinding-the-slider-control-cs.md)
> [下一頁](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="424ae-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
