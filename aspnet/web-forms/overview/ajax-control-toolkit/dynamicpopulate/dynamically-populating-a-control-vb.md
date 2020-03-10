---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: 以動態方式填入控制項（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿至 t ... 的目標控制項
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535683"
---
# <a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="3c52d-103">以動態方式填入控制項 (VB)</span><span class="sxs-lookup"><span data-stu-id="3c52d-103">Dynamically Populating a Control (VB)</span></span>

<span data-ttu-id="3c52d-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3c52d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3c52d-105">[下載程式代碼](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="3c52d-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="3c52d-106">ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="3c52d-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="3c52d-107">概觀</span><span class="sxs-lookup"><span data-stu-id="3c52d-107">Overview</span></span>

<span data-ttu-id="3c52d-108">ASP.NET AJAX 控制項工具組中的 `DynamicPopulate` 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="3c52d-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="3c52d-109">本教學課程會示範如何進行這種設定。</span><span class="sxs-lookup"><span data-stu-id="3c52d-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="3c52d-110">步驟</span><span class="sxs-lookup"><span data-stu-id="3c52d-110">Steps</span></span>

<span data-ttu-id="3c52d-111">首先，您需要 ASP.NET Web 服務，以執行 `DynamicPopulate`所呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="3c52d-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="3c52d-112">Web 服務類別需要在 `Microsoft.Web.Script.Services`內定義的 `ScriptService` 屬性;否則，ASP.NET AJAX 就無法為 web 服務建立用戶端 JavaScript proxy，而這是 `DynamicPopulate`所需的。</span><span class="sxs-lookup"><span data-stu-id="3c52d-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="3c52d-113">Web 方法必須預期會有一個字串類型的引數，稱為 `contextKey`，因為 `DynamicPopulate` 控制項會使用每個 web 服務呼叫來傳送一段內容資訊。</span><span class="sxs-lookup"><span data-stu-id="3c52d-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="3c52d-114">下列 web 服務會以 `contextKey` 引數所代表的格式傳回目前的日期：</span><span class="sxs-lookup"><span data-stu-id="3c52d-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="3c52d-115">Web 服務接著會儲存為 `DynamicPopulate.vb.asmx`。</span><span class="sxs-lookup"><span data-stu-id="3c52d-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="3c52d-116">或者，您也可以使用 `DynamicPopulate` 控制項，將 `getDate()` 方法實作為實際 ASP.NET 網頁中的頁面方法。</span><span class="sxs-lookup"><span data-stu-id="3c52d-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="3c52d-117">在下一個步驟中，建立新的 ASP.NET 檔案。</span><span class="sxs-lookup"><span data-stu-id="3c52d-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="3c52d-118">一如往常，第一個步驟是將 `ScriptManager` 包含在目前的頁面中，以載入 ASP.NET AJAX 程式庫並讓控制項工具組正常執行：</span><span class="sxs-lookup"><span data-stu-id="3c52d-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="3c52d-119">然後，新增標籤控制項（例如，使用相同名稱的 HTML 控制項或 &lt;`asp:Label` /&gt; web 控制項），稍後會顯示 web 服務呼叫的結果。</span><span class="sxs-lookup"><span data-stu-id="3c52d-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="3c52d-120">HTML 按鈕（html 控制項，因為我們不需要回傳至伺服器）會接著用來觸發動態擴展：</span><span class="sxs-lookup"><span data-stu-id="3c52d-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="3c52d-121">最後，我們需要 `DynamicPopulateExtender` 控制項來連接東西。</span><span class="sxs-lookup"><span data-stu-id="3c52d-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="3c52d-122">下列屬性將會設定（除了明顯的屬性外，`ID` 和 `runat`=`"server"`）：</span><span class="sxs-lookup"><span data-stu-id="3c52d-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="3c52d-123">`TargetControlID` 從 web 服務呼叫中放置結果的位置</span><span class="sxs-lookup"><span data-stu-id="3c52d-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="3c52d-124">web 服務 `ServicePath` 路徑（如果您想要使用頁面方法，則省略）</span><span class="sxs-lookup"><span data-stu-id="3c52d-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="3c52d-125">web 方法或頁面方法的 `ServiceMethod` 名稱</span><span class="sxs-lookup"><span data-stu-id="3c52d-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="3c52d-126">要傳送至 web 服務的 `ContextKey` 內容資訊</span><span class="sxs-lookup"><span data-stu-id="3c52d-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="3c52d-127">觸發 web 服務呼叫的 `PopulateTriggerControlID` 元素</span><span class="sxs-lookup"><span data-stu-id="3c52d-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="3c52d-128">`ClearContentsDuringUpdate` 是否要在 web 服務呼叫期間清空目標元素</span><span class="sxs-lookup"><span data-stu-id="3c52d-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="3c52d-129">如您所見，控制項需要一些資訊，但將所有內容都放入原處非常簡單。</span><span class="sxs-lookup"><span data-stu-id="3c52d-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="3c52d-130">以下是目前案例中，`DynamicPopulateExtender` 控制項的標記：</span><span class="sxs-lookup"><span data-stu-id="3c52d-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="3c52d-131">執行瀏覽器中的 [ASP.NET] 頁面，然後按一下 [] 按鈕。您將會收到目前的日期，格式為 [月-日]。</span><span class="sxs-lookup"><span data-stu-id="3c52d-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="3c52d-132">[![按一下按鈕，就會從伺服器抓取日期](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3c52d-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="3c52d-133">按一下按鈕，就會從伺服器抓取日期（[按一下以查看完整大小的影像](dynamically-populating-a-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="3c52d-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3c52d-134">[上一頁](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [下一頁](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3c52d-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
