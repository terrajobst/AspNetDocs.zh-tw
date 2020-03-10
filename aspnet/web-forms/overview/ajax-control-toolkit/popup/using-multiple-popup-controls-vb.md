---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 使用多個快顯視窗控制項（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。 您也可以使用 m 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: e1f4ff64e9fdf48ea63b75c97acd53a64b5ab5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612529"
---
# <a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="1abb1-104">使用多個快顯視窗控制項 (VB)</span><span class="sxs-lookup"><span data-stu-id="1abb1-104">Using Multiple Popup Controls (VB)</span></span>

<span data-ttu-id="1abb1-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1abb1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1abb1-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1abb1-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="1abb1-107">AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。</span><span class="sxs-lookup"><span data-stu-id="1abb1-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="1abb1-108">您也可以在單一頁面上使用多個快顯視窗控制項。</span><span class="sxs-lookup"><span data-stu-id="1abb1-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="1abb1-109">概觀</span><span class="sxs-lookup"><span data-stu-id="1abb1-109">Overview</span></span>

<span data-ttu-id="1abb1-110">AJAX 控制項工具組中的 PopupControl 擴充項提供了一種簡單的方式，可在啟用任何其他控制項時觸發快顯。</span><span class="sxs-lookup"><span data-stu-id="1abb1-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="1abb1-111">您也可以在單一頁面上使用多個快顯視窗控制項。</span><span class="sxs-lookup"><span data-stu-id="1abb1-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="1abb1-112">步驟</span><span class="sxs-lookup"><span data-stu-id="1abb1-112">Steps</span></span>

<span data-ttu-id="1abb1-113">若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="1abb1-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="1abb1-114">接下來，新增一個做為快顯視窗的面板。</span><span class="sxs-lookup"><span data-stu-id="1abb1-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="1abb1-115">在目前的案例中，面板包含 `Calendar` 控制項。</span><span class="sxs-lookup"><span data-stu-id="1abb1-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="1abb1-116">為了避免行事曆的回傳所造成的頁面重新整理，面板會放在 `UpdatePanel` 控制項內：</span><span class="sxs-lookup"><span data-stu-id="1abb1-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="1abb1-117">此頁面也包含兩個文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1abb1-117">The page also contains two text boxes.</span></span> <span data-ttu-id="1abb1-118">針對每個文字方塊，一旦啟動文字方塊之後，行事曆快顯視窗就會出現。</span><span class="sxs-lookup"><span data-stu-id="1abb1-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="1abb1-119">現在以 `PopupControlExtender`擴充兩個文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1abb1-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="1abb1-120">`TargetControlID` 屬性提供系結至擴充項之控制項的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1abb1-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="1abb1-121">`PopupControlID` 屬性包含快顯面板的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1abb1-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="1abb1-122">在此情況下，這兩個擴充項都會顯示相同的面板，但也可能會有不同的面板。</span><span class="sxs-lookup"><span data-stu-id="1abb1-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="1abb1-123">現在，只要您在文字欄位內按一下，行事曆就會出現在欄位下方，讓您可以選取日期。</span><span class="sxs-lookup"><span data-stu-id="1abb1-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="1abb1-124">（在不同的教學課程中將會涵蓋將選取的日期放回文字方塊中）。</span><span class="sxs-lookup"><span data-stu-id="1abb1-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="1abb1-125">[當使用者按一下文字方塊時，就會顯示行事曆 ![](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1abb1-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="1abb1-126">當使用者按一下文字方塊時，就會出現行事曆（[按一下以查看完整大小的影像](using-multiple-popup-controls-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="1abb1-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1abb1-127">[上一頁](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [下一頁](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1abb1-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
