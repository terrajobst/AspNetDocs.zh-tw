---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 使用滑杆控制項搭配自動回傳（C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 可以讓滑杆 autopost 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553617"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="3e560-104">使用滑杆控制項搭配自動回傳（C#）</span><span class="sxs-lookup"><span data-stu-id="3e560-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="3e560-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3e560-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3e560-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3e560-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="3e560-107">AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="3e560-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="3e560-108">它的值變更後，可以讓滑杆 autopostback。</span><span class="sxs-lookup"><span data-stu-id="3e560-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="3e560-109">概觀</span><span class="sxs-lookup"><span data-stu-id="3e560-109">Overview</span></span>

<span data-ttu-id="3e560-110">AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="3e560-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="3e560-111">它的值變更後，可以讓滑杆 autopostback。</span><span class="sxs-lookup"><span data-stu-id="3e560-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="3e560-112">步驟</span><span class="sxs-lookup"><span data-stu-id="3e560-112">Steps</span></span>

<span data-ttu-id="3e560-113">為了讓滑杆在變更時自動回傳，這兩個文字方塊都需要屬性 `AutoPostBack="true"`：將成為滑杆本身的文字方塊，以及保留滑杆位置的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3e560-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="3e560-114">以下是所需的標記：</span><span class="sxs-lookup"><span data-stu-id="3e560-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="3e560-115">ASP.NET AJAX 控制項工具組中的 `SliderExtender` 控制項，會將滑杆功能指派給這兩個文字方塊：</span><span class="sxs-lookup"><span data-stu-id="3e560-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="3e560-116">稍後會使用其他的 label 元素來通知使用者回傳：</span><span class="sxs-lookup"><span data-stu-id="3e560-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="3e560-117">最後，ASP.NET AJAX 的 `ScriptManager` 控制項會載入必要的 JavaScript，讓控制項工具組能夠正常執行：</span><span class="sxs-lookup"><span data-stu-id="3e560-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="3e560-118">現在滑杆回傳了;在伺服器端，此事件可能會被攔截並採取下列動作：</span><span class="sxs-lookup"><span data-stu-id="3e560-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

<span data-ttu-id="3e560-119">[移動滑杆的 ![會觸發回傳](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3e560-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="3e560-120">移動滑杆會觸發回傳（[按一下以觀看完整大小的影像](using-the-slider-control-with-auto-postback-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="3e560-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>

<span data-ttu-id="3e560-121">[![之後，這項變更的日期會寫入至標籤](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3e560-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="3e560-122">之後，這項變更的日期會寫入標籤（[按一下以查看完整大小的影像](using-the-slider-control-with-auto-postback-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="3e560-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3e560-123">下一個</span><span class="sxs-lookup"><span data-stu-id="3e560-123">Next</span></span>](databinding-the-slider-control-cs.md)
