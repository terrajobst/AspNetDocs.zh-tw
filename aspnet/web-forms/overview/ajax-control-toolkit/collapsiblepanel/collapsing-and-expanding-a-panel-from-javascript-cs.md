---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: 從 JavaScript 折迭和展開面板（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 CollapsiblePanel 控制項會擴充一個面板，並提供它可折迭其內容並將其展開的功能 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: bed14d82394d28336493bec10e31ddb4d411a192
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599451"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a><span data-ttu-id="a7baa-103">從 JavaScript 摺疊與展開面板 (C#)</span><span class="sxs-lookup"><span data-stu-id="a7baa-103">Collapsing and Expanding a Panel from JavaScript (C#)</span></span>

<span data-ttu-id="a7baa-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a7baa-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a7baa-105">[下載程式代碼](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7baa-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span></span>

> <span data-ttu-id="a7baa-106">ASP.NET AJAX 控制項工具組中的 CollapsiblePanel 控制項會擴充一個面板，並為它提供可折迭其內容並重新展開它的功能。</span><span class="sxs-lookup"><span data-stu-id="a7baa-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="a7baa-107">這兩個動作也可以從自訂 JavaScript 程式碼觸發。</span><span class="sxs-lookup"><span data-stu-id="a7baa-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="a7baa-108">概觀</span><span class="sxs-lookup"><span data-stu-id="a7baa-108">Overview</span></span>

<span data-ttu-id="a7baa-109">ASP.NET AJAX 控制項工具組中的 CollapsiblePanel 控制項會擴充一個面板，並為它提供可折迭其內容並重新展開它的功能。</span><span class="sxs-lookup"><span data-stu-id="a7baa-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="a7baa-110">這兩個動作也可以從自訂 JavaScript 程式碼觸發。</span><span class="sxs-lookup"><span data-stu-id="a7baa-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="a7baa-111">步驟</span><span class="sxs-lookup"><span data-stu-id="a7baa-111">Steps</span></span>

<span data-ttu-id="a7baa-112">首先，建立新的 ASP.NET 網頁，並在一個 `<form>` 元素內包含 `ScriptManager`。</span><span class="sxs-lookup"><span data-stu-id="a7baa-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="a7baa-113">這會載入控制項工具組所需的 ASP.NET AJAX 程式庫：</span><span class="sxs-lookup"><span data-stu-id="a7baa-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="a7baa-114">然後，建立具有一些文字的面板，以便看到折迭/展開效果：</span><span class="sxs-lookup"><span data-stu-id="a7baa-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="a7baa-115">如您所見，面板會參考此處顯示的 CSS 類別（基本上會定義背景色彩和麵板的寬度）：</span><span class="sxs-lookup"><span data-stu-id="a7baa-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

<span data-ttu-id="a7baa-116">`CollapsiblePanelExtender` 控制項需要 `TargetControlID` 屬性，讓工具組知道在要求時要折迭或展開哪個面板：</span><span class="sxs-lookup"><span data-stu-id="a7baa-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

<span data-ttu-id="a7baa-117">可惜的是，擴充專案前不會公開用於折迭或展開面板的特定 API，但是某些未記載的方法將會執行。</span><span class="sxs-lookup"><span data-stu-id="a7baa-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="a7baa-118">首先，將三個 HTML 按鈕新增至頁面，然後觸發用戶端 JavaScript 來折迭或展開面板的內容：</span><span class="sxs-lookup"><span data-stu-id="a7baa-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="a7baa-119">在用戶端 JavaScript 程式碼中（以 `<script type="text/javascript">`開始），必須使用 `$find()` 方法來存取 `CollapsiblePanelExtender`。</span><span class="sxs-lookup"><span data-stu-id="a7baa-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="a7baa-120">`$find("cpe")` 會傳回它的參考。</span><span class="sxs-lookup"><span data-stu-id="a7baa-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="a7baa-121">從這裡開始，特定方法將可解決手邊的工作。</span><span class="sxs-lookup"><span data-stu-id="a7baa-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="a7baa-122">開啟（展開）面板的方法會被呼叫 `_doOpen()`;下列程式碼會在按一下第一個按鈕時，執行呼叫的 `doOpen()` 函式：</span><span class="sxs-lookup"><span data-stu-id="a7baa-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

<span data-ttu-id="a7baa-123">若要關閉或折迭面板，必須執行 `_doClose()` 方法。</span><span class="sxs-lookup"><span data-stu-id="a7baa-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="a7baa-124">因此，當使用者按一下第二個按鈕時，會呼叫下列 JavaScript 程式碼：</span><span class="sxs-lookup"><span data-stu-id="a7baa-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

<span data-ttu-id="a7baa-125">第三個按鈕會切換面板的狀態：從折迭到展開，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="a7baa-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="a7baa-126">`CollapsiblePanelExtender` 會公開 `toggle()` 方法，這完全是：反轉面板的狀態。</span><span class="sxs-lookup"><span data-stu-id="a7baa-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="a7baa-127">不過還有另一種方法（在內部由 `toggle()` 方法使用）： `CollapsiblePanelExtender()` 的 `get_Collapsed()` 方法會告訴我們面板是否已折迭。</span><span class="sxs-lookup"><span data-stu-id="a7baa-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="a7baa-128">根據此函數的傳回值，面板會展開（`_doOpen()` 方法）或折迭（`_doClose()`）方法：</span><span class="sxs-lookup"><span data-stu-id="a7baa-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]

<span data-ttu-id="a7baa-129">[![第三個按鈕會變更面板的狀態：從 [已折迭] 到 [已展開] 和 [上一頁]](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a7baa-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="a7baa-130">第三個按鈕會變更面板的狀態：從 [折迭] 到 [已展開] 和 [上一頁] （[按一下以查看完整大小的影像](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="a7baa-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a7baa-131">下一步</span><span class="sxs-lookup"><span data-stu-id="a7baa-131">Next</span></span>](collapsing-and-expanding-a-panel-from-javascript-vb.md)
