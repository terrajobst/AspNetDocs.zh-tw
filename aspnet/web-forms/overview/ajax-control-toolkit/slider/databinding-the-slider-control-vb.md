---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 資料系結滑杆控制項（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。 您可以系結目前的 positio 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598284"
---
# <a name="databinding-the-slider-control-vb"></a><span data-ttu-id="136f3-104">資料繫結滑桿控制項 (VB)</span><span class="sxs-lookup"><span data-stu-id="136f3-104">Databinding the Slider Control (VB)</span></span>

<span data-ttu-id="136f3-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="136f3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="136f3-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="136f3-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span></span>

> <span data-ttu-id="136f3-107">AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="136f3-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="136f3-108">您可以將滑杆的目前位置系結至另一個 ASP.NET 控制項。</span><span class="sxs-lookup"><span data-stu-id="136f3-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="overview"></a><span data-ttu-id="136f3-109">概觀</span><span class="sxs-lookup"><span data-stu-id="136f3-109">Overview</span></span>

<span data-ttu-id="136f3-110">AJAX 控制項工具組中的滑杆控制項提供圖形滑杆，可以使用滑鼠來控制。</span><span class="sxs-lookup"><span data-stu-id="136f3-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="136f3-111">您可以將滑杆的目前位置系結至另一個 ASP.NET 控制項。</span><span class="sxs-lookup"><span data-stu-id="136f3-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="136f3-112">步驟</span><span class="sxs-lookup"><span data-stu-id="136f3-112">Steps</span></span>

<span data-ttu-id="136f3-113">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="136f3-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

<span data-ttu-id="136f3-114">接下來，將兩個 `TextBox` 控制項加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="136f3-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="136f3-115">其中一個會轉換成圖形滑杆，另一個則會保存滑杆的位置。</span><span class="sxs-lookup"><span data-stu-id="136f3-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

<span data-ttu-id="136f3-116">下一個步驟已經是最後一個步驟。</span><span class="sxs-lookup"><span data-stu-id="136f3-116">The next step is already the final step.</span></span> <span data-ttu-id="136f3-117">ASP.NET AJAX 控制項工具組中的 `SliderExtender` 控制項會從第一個文字方塊移出一個滑杆，並在滑杆位置變更時自動更新第二個文字方塊。</span><span class="sxs-lookup"><span data-stu-id="136f3-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="136f3-118">`SliderExtender`的 `TargetControlID` 屬性必須設定為第一個文字方塊的識別碼，才能正常操作。`BoundControlID` 屬性必須設定為第二個文字方塊的識別碼。</span><span class="sxs-lookup"><span data-stu-id="136f3-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

<span data-ttu-id="136f3-119">如您在瀏覽器中所見，資料系結會雙向運作：在文字方塊中輸入新的值會更新滑杆的位置。</span><span class="sxs-lookup"><span data-stu-id="136f3-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="136f3-120">如果您將第二個文字方塊設為唯讀，您可以在文字欄位中加入弱式保護，讓使用者更難以手動更新該處的值。</span><span class="sxs-lookup"><span data-stu-id="136f3-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>

<span data-ttu-id="136f3-121">[![滑杆和文字方塊已同步](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="136f3-121">[![Slider and text box are in sync](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="136f3-122">滑杆和文字方塊已同步（[按一下以觀看完整大小的影像](databinding-the-slider-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="136f3-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="136f3-123">上一篇</span><span class="sxs-lookup"><span data-stu-id="136f3-123">Previous</span></span>](using-the-slider-control-with-auto-postback-vb.md)
