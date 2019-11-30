---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: 從伺服器程式碼啟動強制回應快顯視窗C#（） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 不過，有些案例需要 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: fec0ce2cdd24333f65201301718440e1a09d930e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599058"
---
# <a name="launching-a-modal-popup-window-from-server-code-c"></a><span data-ttu-id="7340d-104">從伺服器程式碼啟動強制回應快顯視窗 (C#)</span><span class="sxs-lookup"><span data-stu-id="7340d-104">Launching a Modal Popup Window from Server Code (C#)</span></span>

<span data-ttu-id="7340d-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7340d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7340d-106">[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7340d-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span></span>

> <span data-ttu-id="7340d-107">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="7340d-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7340d-108">不過，有些情況需要在伺服器端觸發強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="7340d-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="7340d-109">概觀</span><span class="sxs-lookup"><span data-stu-id="7340d-109">Overview</span></span>

<span data-ttu-id="7340d-110">AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="7340d-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7340d-111">不過，有些情況需要在伺服器端觸發強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="7340d-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="7340d-112">步驟</span><span class="sxs-lookup"><span data-stu-id="7340d-112">Steps</span></span>

<span data-ttu-id="7340d-113">首先，必須要有 ASP.NET 按鈕 web 控制項，才能示範 ModalPopup 控制項的運作方式。</span><span class="sxs-lookup"><span data-stu-id="7340d-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="7340d-114">在新頁面上的 &lt;表單&gt; 元素中加入這類按鈕：</span><span class="sxs-lookup"><span data-stu-id="7340d-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

<span data-ttu-id="7340d-115">然後，您需要您想要建立之快顯的標記。</span><span class="sxs-lookup"><span data-stu-id="7340d-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="7340d-116">將它定義為 `<asp:Panel>` 控制項，並確定它包含按鈕控制項。</span><span class="sxs-lookup"><span data-stu-id="7340d-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="7340d-117">ModalPopup 控制項提供讓這類按鈕關閉快顯視窗的功能;否則，沒有任何簡單的方法可以讓它消失。</span><span class="sxs-lookup"><span data-stu-id="7340d-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

<span data-ttu-id="7340d-118">接下來，從 ASP.NET AJAX 工具組將 ModalPopup 控制項新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="7340d-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="7340d-119">設定載入控制項的按鈕屬性、使其消失的按鈕，以及實際快顯視窗的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7340d-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

<span data-ttu-id="7340d-120">如同所有以 ASP.NET AJAX 為基礎的網頁，需要腳本管理員，才能為不同的目標瀏覽器載入必要的 JavaScript 程式庫：</span><span class="sxs-lookup"><span data-stu-id="7340d-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

<span data-ttu-id="7340d-121">在瀏覽器中執行範例。</span><span class="sxs-lookup"><span data-stu-id="7340d-121">Run the example in the browser.</span></span> <span data-ttu-id="7340d-122">當您按一下按鈕時，就會出現強制回應快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="7340d-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="7340d-123">若要使用伺服器端程式碼達到相同的效果，則需要新的按鈕：</span><span class="sxs-lookup"><span data-stu-id="7340d-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

<span data-ttu-id="7340d-124">如您所見，按一下按鈕會產生回傳，並在伺服器上執行 `ServerButton_Click()` 方法。</span><span class="sxs-lookup"><span data-stu-id="7340d-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="7340d-125">在這個方法中，稱為 `launchModal()` 的 JavaScript 函式會執行成精確的，一旦載入頁面，就會執行 JavaScript 函式：</span><span class="sxs-lookup"><span data-stu-id="7340d-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

<span data-ttu-id="7340d-126">`launchModal()` 的工作是要顯示 ModalPopup。</span><span class="sxs-lookup"><span data-stu-id="7340d-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="7340d-127">一旦載入完整的 HTML 頁面，就會執行 `launchModal()` 函式。</span><span class="sxs-lookup"><span data-stu-id="7340d-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="7340d-128">不過，目前尚未完全載入 ASP.NET AJAX 架構。</span><span class="sxs-lookup"><span data-stu-id="7340d-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="7340d-129">因此，`launchModal()` 函數只會設定一個變數，ModalPopup 控制項稍後必須顯示：</span><span class="sxs-lookup"><span data-stu-id="7340d-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

<span data-ttu-id="7340d-130">`pageLoad()` JavaScript 函式是一種特殊函式，會在 ASP.NET AJAX 完全載入後執行。</span><span class="sxs-lookup"><span data-stu-id="7340d-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="7340d-131">因此，我們將程式碼加入此函式以顯示 ModalPopup 控制項，但只有在之前呼叫過 `launchModal()`：</span><span class="sxs-lookup"><span data-stu-id="7340d-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

<span data-ttu-id="7340d-132">`$find()` 函式會在頁面上尋找名為的專案，而且需要伺服器端識別碼做為參數。</span><span class="sxs-lookup"><span data-stu-id="7340d-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="7340d-133">因此，`$find("mpe")` 會傳回 ModalPopup 控制項的用戶端標記法;其 `show()` 方法會讓快顯視窗出現。</span><span class="sxs-lookup"><span data-stu-id="7340d-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="7340d-134">[當按一下其中一個按鈕時，就會出現強制回應快顯視窗 ![](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7340d-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="7340d-135">按一下其中一個按鈕時，就會出現強制回應快顯視窗（[按一下以查看完整大小的影像](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="7340d-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7340d-136">下一步</span><span class="sxs-lookup"><span data-stu-id="7340d-136">Next</span></span>](using-modalpopup-with-a-repeater-control-cs.md)
