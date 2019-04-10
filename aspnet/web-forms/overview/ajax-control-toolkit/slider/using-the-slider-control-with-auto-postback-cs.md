---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 使用滑桿控制項具有自動回傳 (C#) |Microsoft Docs
author: wenz
description: 在 AJAX Control Toolkit 中的滑桿控制項提供的圖形化的滑桿，可以使用滑鼠來控制。 您可將滑桿張貼...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: a5b858a05470caa244902afbb404adbb2e4761b7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59402722"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="30275-104">使用滑桿控制項具有自動回傳 (C#)</span><span class="sxs-lookup"><span data-stu-id="30275-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="30275-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="30275-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="30275-106">[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="30275-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="30275-107">在 AJAX Control Toolkit 中的滑桿控制項提供的圖形化的滑桿，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="30275-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="30275-108">可以變更滑桿 autopostback 一次其值。</span><span class="sxs-lookup"><span data-stu-id="30275-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="30275-109">總覽</span><span class="sxs-lookup"><span data-stu-id="30275-109">Overview</span></span>

<span data-ttu-id="30275-110">在 AJAX Control Toolkit 中的滑桿控制項提供的圖形化的滑桿，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="30275-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="30275-111">可以變更滑桿 autopostback 一次其值。</span><span class="sxs-lookup"><span data-stu-id="30275-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="30275-112">步驟</span><span class="sxs-lookup"><span data-stu-id="30275-112">Steps</span></span>

<span data-ttu-id="30275-113">若要讓發生變更時自動回傳的滑桿，這兩個文字方塊必須屬性`AutoPostBack="true"`:將成為本身，滑桿的文字方塊中，文字方塊中保存滑桿的位置。</span><span class="sxs-lookup"><span data-stu-id="30275-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="30275-114">以下是該所需的標記：</span><span class="sxs-lookup"><span data-stu-id="30275-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="30275-115">`SliderExtender`從 ASP.NET AJAX Control Toolkit 控制項將滑桿功能指派給兩個文字方塊：</span><span class="sxs-lookup"><span data-stu-id="30275-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="30275-116">其他標籤項目，則稍後將用於通知使用者回傳：</span><span class="sxs-lookup"><span data-stu-id="30275-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="30275-117">最後， `ScriptManager` ASP.NET ajax 控制項載入必要的 JavaScript，才能控制工具組：</span><span class="sxs-lookup"><span data-stu-id="30275-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="30275-118">現在滑桿會回傳;伺服器端上可能會攔截及處理此事件：</span><span class="sxs-lookup"><span data-stu-id="30275-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]


[![M<span data-ttu-id="30275-119">釋出滑桿會觸發回傳]</span><span class="sxs-lookup"><span data-stu-id="30275-119">oving the slider triggers a postback]</span></span>(using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)

<span data-ttu-id="30275-120">移動滑桿會觸發回傳 ([按一下以檢視完整大小的影像](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="30275-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>


[![A<span data-ttu-id="30275-121">fterwards，這項變更的日期是以標籤]</span><span class="sxs-lookup"><span data-stu-id="30275-121">fterwards, the date of this change is written in the label]</span></span>(using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)

<span data-ttu-id="30275-122">之後，這項變更的日期以標籤 ([按一下以檢視完整大小的影像](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="30275-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="30275-123">下一步</span><span class="sxs-lookup"><span data-stu-id="30275-123">Next</span></span>](databinding-the-slider-control-cs.md)
