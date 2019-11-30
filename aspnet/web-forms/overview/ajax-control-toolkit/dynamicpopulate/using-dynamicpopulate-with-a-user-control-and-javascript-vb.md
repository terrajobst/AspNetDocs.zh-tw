---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: 使用 DynamicPopulate 搭配使用者控制項和 JavaScript （VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿至 t ... 的目標控制項
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599119"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="0ae35-103">使用具有使用者控制項的 DynamicPopulate 和 JavaScript (VB)</span><span class="sxs-lookup"><span data-stu-id="0ae35-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>

<span data-ttu-id="0ae35-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0ae35-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0ae35-105">[下載程式代碼](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0ae35-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="0ae35-106">ASP.NET AJAX 控制項工具組中的 DynamicPopulate 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="0ae35-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="0ae35-107">您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。</span><span class="sxs-lookup"><span data-stu-id="0ae35-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="0ae35-108">不過，當擴充項位於使用者控制項時，必須特別小心。</span><span class="sxs-lookup"><span data-stu-id="0ae35-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="0ae35-109">概觀</span><span class="sxs-lookup"><span data-stu-id="0ae35-109">Overview</span></span>

<span data-ttu-id="0ae35-110">ASP.NET AJAX 控制項工具組中的 `DynamicPopulate` 控制項會呼叫 web 服務（或頁面方法），並將產生的值填滿頁面上的目標控制項中，而不需要重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="0ae35-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="0ae35-111">您也可以使用自訂用戶端 JavaScript 程式碼來觸發填入。</span><span class="sxs-lookup"><span data-stu-id="0ae35-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="0ae35-112">不過，當擴充項位於使用者控制項時，必須特別小心。</span><span class="sxs-lookup"><span data-stu-id="0ae35-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="0ae35-113">步驟</span><span class="sxs-lookup"><span data-stu-id="0ae35-113">Steps</span></span>

<span data-ttu-id="0ae35-114">首先，您需要一個 ASP.NET Web 服務，它會執行由 `DynamicPopulateExtender` 控制項呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="0ae35-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="0ae35-115">Web 服務會執行方法 `getDate()`，預期會有一個字串類型的引數，稱為 `contextKey`，因為 `DynamicPopulate` 控制項會傳送一個內容資訊給每個 web 服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="0ae35-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="0ae35-116">以下程式碼（files `DynamicPopulate.vb.asmx`）會以下列三種格式的其中一種來抓取目前的日期：</span><span class="sxs-lookup"><span data-stu-id="0ae35-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="0ae35-117">在下一個步驟中，建立新的使用者控制項（`.ascx` 檔案），並在第一行中以下列宣告表示：</span><span class="sxs-lookup"><span data-stu-id="0ae35-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="0ae35-118">&lt;`label`&gt; 元素將用來顯示來自伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="0ae35-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="0ae35-119">此外，在使用者控制項檔案中，我們會使用三個選項按鈕，分別代表 web 服務支援的三種可能日期格式之一。</span><span class="sxs-lookup"><span data-stu-id="0ae35-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="0ae35-120">當使用者按一下其中一個選項按鈕時，瀏覽器將會執行 JavaScript 程式碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0ae35-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="0ae35-121">此程式碼會存取 `DynamicPopulateExtender` （不擔心奇怪的識別碼，這將于稍後說明），並使用資料觸發動態擴展。</span><span class="sxs-lookup"><span data-stu-id="0ae35-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="0ae35-122">在目前選項按鈕的內容中，`this.value` 指的是 `format1`、`format2` 或 `format3` web 方法所預期的值。</span><span class="sxs-lookup"><span data-stu-id="0ae35-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="0ae35-123">使用者控制項中唯一缺少的東西，就是將選項按鈕連結至 web 服務的 `DynamicPopulateExtender` 控制項。</span><span class="sxs-lookup"><span data-stu-id="0ae35-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="0ae35-124">同樣地，您可能會注意到控制項中使用的奇怪識別碼： `mcd1$myDate`，而不是 `myDate`。</span><span class="sxs-lookup"><span data-stu-id="0ae35-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="0ae35-125">先前，用來 `mcd1_dpe1` 的 JavaScript 程式碼可存取 `DynamicPopulateExtender`，而不是 `dpe1`。此命名策略是在使用者控制項中使用 `DynamicPopulateExtender` 時的特殊需求。</span><span class="sxs-lookup"><span data-stu-id="0ae35-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="0ae35-126">此外，您必須以特定方式內嵌使用者控制項，才能讓它進行所有工作。</span><span class="sxs-lookup"><span data-stu-id="0ae35-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="0ae35-127">建立新的 ASP.NET 網頁，並為您剛執行的使用者控制項註冊標記前置詞：</span><span class="sxs-lookup"><span data-stu-id="0ae35-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="0ae35-128">然後，在新的頁面上包含 ASP.NET AJAX `ScriptManager` 控制項：</span><span class="sxs-lookup"><span data-stu-id="0ae35-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="0ae35-129">最後，將使用者控制項加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="0ae35-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="0ae35-130">您只需要設定其 `ID` 屬性（當然也 `runat="server"`），但您也必須將它設定為特定名稱： `mcd1`，因為這是使用者控制項內用來使用 JavaScript 來存取它的前置詞。</span><span class="sxs-lookup"><span data-stu-id="0ae35-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="0ae35-131">就是這麼容易！</span><span class="sxs-lookup"><span data-stu-id="0ae35-131">And that's it!</span></span> <span data-ttu-id="0ae35-132">頁面會如預期般運作：使用者按一下其中一個選項按鈕，工具組中的控制項就會呼叫 web 服務，並以所需的格式顯示目前的日期。</span><span class="sxs-lookup"><span data-stu-id="0ae35-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="0ae35-133">[![選項按鈕位於使用者控制項中](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0ae35-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="0ae35-134">選項按鈕位於使用者控制項（[按一下以查看完整大小的影像](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="0ae35-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0ae35-135">上一篇</span><span class="sxs-lookup"><span data-stu-id="0ae35-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
