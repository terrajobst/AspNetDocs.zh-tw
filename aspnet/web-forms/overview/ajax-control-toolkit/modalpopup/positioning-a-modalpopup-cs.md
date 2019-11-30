---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: 定位 ModalPopup （C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 但控制項不提供 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598998"
---
# <a name="positioning-a-modalpopup-c"></a><span data-ttu-id="5461c-104">定位 ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="5461c-104">Positioning a ModalPopup (C#)</span></span>

<span data-ttu-id="5461c-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5461c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5461c-106">[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5461c-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span></span>

> <span data-ttu-id="5461c-107">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="5461c-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="5461c-108">不過，控制項並未提供可定位快顯的內建功能。</span><span class="sxs-lookup"><span data-stu-id="5461c-108">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="5461c-109">概觀</span><span class="sxs-lookup"><span data-stu-id="5461c-109">Overview</span></span>

<span data-ttu-id="5461c-110">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="5461c-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="5461c-111">不過，控制項並未提供可定位快顯的內建功能。</span><span class="sxs-lookup"><span data-stu-id="5461c-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="5461c-112">步驟</span><span class="sxs-lookup"><span data-stu-id="5461c-112">Steps</span></span>

<span data-ttu-id="5461c-113">為了啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager`。</span><span class="sxs-lookup"><span data-stu-id="5461c-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="5461c-114">控制項必須放在頁面上的任何位置（但在 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="5461c-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="5461c-115">接下來，新增可作為強制回應快顯視窗的面板。</span><span class="sxs-lookup"><span data-stu-id="5461c-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="5461c-116">按鈕可用來關閉快顯視窗：</span><span class="sxs-lookup"><span data-stu-id="5461c-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="5461c-117">每當快顯視窗顯示時，就會放在頁面中的特定位置。</span><span class="sxs-lookup"><span data-stu-id="5461c-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="5461c-118">針對這項工作，會建立用戶端 JavaScript 函式。</span><span class="sxs-lookup"><span data-stu-id="5461c-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="5461c-119">它會先嘗試存取面板。</span><span class="sxs-lookup"><span data-stu-id="5461c-119">It first tries to access the panel.</span></span> <span data-ttu-id="5461c-120">如果成功，則會使用 CSS 和 JavaScript 設定面板的位置（變更快顯的位置）。</span><span class="sxs-lookup"><span data-stu-id="5461c-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="5461c-121">不過，`ModalPopupExtender` 控制項也會嘗試定位快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="5461c-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="5461c-122">因此，JavaScript 程式碼會重複放置快顯，每十秒一次。</span><span class="sxs-lookup"><span data-stu-id="5461c-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

<span data-ttu-id="5461c-123">如您所見，`setTimeout()` JavaScript 方法的傳回值會儲存在全域變數中。</span><span class="sxs-lookup"><span data-stu-id="5461c-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="5461c-124">這可讓您使用 `clearTimeout()` 方法，依需求停止重複的快顯視窗位置：</span><span class="sxs-lookup"><span data-stu-id="5461c-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

<span data-ttu-id="5461c-125">接下來要做的就是讓瀏覽器在適當時呼叫這些函式。</span><span class="sxs-lookup"><span data-stu-id="5461c-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="5461c-126">按一下觸發面板的按鈕時，必須呼叫 `movePanel()` JavaScript 函式：</span><span class="sxs-lookup"><span data-stu-id="5461c-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

<span data-ttu-id="5461c-127">而 `stopMoving()` 函式會在快顯視窗關閉時進入播放狀態，這可以在 `ModalPopupExtender` 控制項中觸發：</span><span class="sxs-lookup"><span data-stu-id="5461c-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

<span data-ttu-id="5461c-128">[![強制回應快顯視窗出現在指定的位置](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5461c-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="5461c-129">強制回應快顯視窗會出現在指定的位置（[按一下以查看完整大小的影像](positioning-a-modalpopup-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="5461c-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5461c-130">[上一頁](handling-postbacks-from-a-modalpopup-cs.md)
> [下一頁](launching-a-modal-popup-window-from-server-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5461c-130">[Previous](handling-postbacks-from-a-modalpopup-cs.md)
[Next](launching-a-modal-popup-window-from-server-code-vb.md)</span></span>
