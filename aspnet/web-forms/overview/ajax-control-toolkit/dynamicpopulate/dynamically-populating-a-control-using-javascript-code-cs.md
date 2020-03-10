---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: 使用 JavaScript 程式碼以動態方式填入C#控制項（） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿至 t ... 的目標控制項
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 24dc358427dec3ffcba16d00041c9a2db657e7e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535739"
---
# <a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="0ea76-103">使用 JavaScript 程式碼以動態方式填入控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="0ea76-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>

<span data-ttu-id="0ea76-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0ea76-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0ea76-105">[下載程式代碼](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0ea76-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="0ea76-106">ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="0ea76-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="0ea76-107">您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。</span><span class="sxs-lookup"><span data-stu-id="0ea76-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="0ea76-108">概觀</span><span class="sxs-lookup"><span data-stu-id="0ea76-108">Overview</span></span>

<span data-ttu-id="0ea76-109">ASP.NET AJAX 控制項工具組中的 `DynamicPopulate` 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="0ea76-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="0ea76-110">您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。</span><span class="sxs-lookup"><span data-stu-id="0ea76-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="0ea76-111">步驟</span><span class="sxs-lookup"><span data-stu-id="0ea76-111">Steps</span></span>

<span data-ttu-id="0ea76-112">首先，您需要一個 ASP.NET Web 服務，它會執行由 `DynamicPopulateExtender` 控制項呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="0ea76-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="0ea76-113">Web 服務會執行方法 `getDate()`，預期會有一個字串類型的引數，稱為 `contextKey`，因為 `DynamicPopulate` 控制項會傳送一個內容資訊給每個 web 服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="0ea76-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="0ea76-114">以下程式碼（file `DynamicPopulate.cs.asmx`）會以下列三種格式的其中一種來抓取目前的日期：</span><span class="sxs-lookup"><span data-stu-id="0ea76-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="0ea76-115">在下一個步驟中，建立新的 ASP.NET 網站，並開始使用 ASP.NET AJAX ScriptManager 控制項：</span><span class="sxs-lookup"><span data-stu-id="0ea76-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="0ea76-116">然後，新增標籤控制項（例如，使用相同名稱的 HTML 控制項或 `<asp:Label />` web 控制項），稍後會顯示 web 服務呼叫的結果。</span><span class="sxs-lookup"><span data-stu-id="0ea76-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="0ea76-117">接下來，包含一個 `DynamicPopulateExtender` 控制項，並提供 web 服務資訊、目標控制項，但不是觸發擴展的控制項名稱，這會在稍後使用自訂 JavaScript 來完成：</span><span class="sxs-lookup"><span data-stu-id="0ea76-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="0ea76-118">現在到 JavaScript 部分。</span><span class="sxs-lookup"><span data-stu-id="0ea76-118">Now to the JavaScript part.</span></span> <span data-ttu-id="0ea76-119">ASP.NET AJAX 程式庫所定義的 `$find()` 函式會傳回 ASP.NET AJAX 控制項工具組（例如 `DynamicPopulateExtender`）之伺服器端物件的參考。</span><span class="sxs-lookup"><span data-stu-id="0ea76-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="0ea76-120">在目前的檔案中，`$find("dpe")` 會在頁面中傳回一個 `DynamicPopulateExtender` 控制項的參考。</span><span class="sxs-lookup"><span data-stu-id="0ea76-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="0ea76-121">它會公開稱為 `populate()` 的方法，以觸發動態擴展進程。</span><span class="sxs-lookup"><span data-stu-id="0ea76-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="0ea76-122">`populate()` 方法需要一個引數：將作為 `getDate()` web 方法引數的內容索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0ea76-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="0ea76-123">比方說，`$find("dpe").populate("format1")` 會在標籤中填入以月-日格式表示的目前日期。</span><span class="sxs-lookup"><span data-stu-id="0ea76-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="0ea76-124">為了讓範例更有彈性，使用者現在可以選擇數種日期格式。</span><span class="sxs-lookup"><span data-stu-id="0ea76-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="0ea76-125">其中每一項都會顯示一個選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="0ea76-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="0ea76-126">一旦使用者按一下選項按鈕，JavaScript 程式碼就會以選取的日期格式動態填入標籤。</span><span class="sxs-lookup"><span data-stu-id="0ea76-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="0ea76-127">這些選項按鈕如下：</span><span class="sxs-lookup"><span data-stu-id="0ea76-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="0ea76-128">請注意，在選項按鈕的內容中，JavaScript 運算式 `this.value` 指的是目前按鈕的值，這剛好是 `getDate()` 方法可以使用的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="0ea76-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>

<span data-ttu-id="0ea76-129">[![按一下按鈕，就會以指定的格式從伺服器抓取日期](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0ea76-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="0ea76-130">按一下按鈕，就會以指定的格式（[按一下以查看完整大小的影像](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png)），從伺服器抓取日期</span><span class="sxs-lookup"><span data-stu-id="0ea76-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0ea76-131">[上一頁](dynamically-populating-a-control-cs.md)
> [下一頁](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="0ea76-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>
