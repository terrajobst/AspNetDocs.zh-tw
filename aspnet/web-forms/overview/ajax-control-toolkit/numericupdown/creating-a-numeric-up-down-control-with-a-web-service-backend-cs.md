---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: 使用 Web 服務後端建立數值向上/向下控制項（C#） |Microsoft Docs
author: wenz
description: 不是讓使用者在核取方塊中輸入值，而是數值的向上/向下控制項（存在於 Windows 和其他作業系統上）可以證明更多的 c 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598891"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="34332-103">使用 Web 服務後端建立數值向上/向下控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="34332-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>

<span data-ttu-id="34332-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="34332-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="34332-105">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="34332-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="34332-106">不是讓使用者在核取方塊中輸入值，而是由數值向上/向下控制項（存在於 Windows 和其他作業系統上）可能會證明更舒適。</span><span class="sxs-lookup"><span data-stu-id="34332-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="34332-107">根據預設，NumericUpDown 控制項一律會增加或減少1的值，但 web 服務會證明更多的彈性。</span><span class="sxs-lookup"><span data-stu-id="34332-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="34332-108">概觀</span><span class="sxs-lookup"><span data-stu-id="34332-108">Overview</span></span>

<span data-ttu-id="34332-109">不是讓使用者在核取方塊中輸入值，而是由數值向上/向下控制項（存在於 Windows 和其他作業系統上）可能會證明更舒適。</span><span class="sxs-lookup"><span data-stu-id="34332-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="34332-110">根據預設，`NumericUpDown` 控制項一律會增加或減少1的值，但 web 服務會證明更多的彈性。</span><span class="sxs-lookup"><span data-stu-id="34332-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="34332-111">步驟</span><span class="sxs-lookup"><span data-stu-id="34332-111">Steps</span></span>

<span data-ttu-id="34332-112">ASP.NET AJAX 控制項工具組包含 `NumericUpDown` 擴充項，會自動將兩個按鈕加入文字方塊中：一個用於增加其值，一個用於減少。</span><span class="sxs-lookup"><span data-stu-id="34332-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="34332-113">不過，控制項也支援 web 服務呼叫（或頁面方法呼叫）。</span><span class="sxs-lookup"><span data-stu-id="34332-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="34332-114">只要按一下 [向上] 或 [向下] 按鈕，JavaScript 程式碼就會連接到 web 伺服器，並在該處執行方法。</span><span class="sxs-lookup"><span data-stu-id="34332-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="34332-115">方法簽章如下所示：</span><span class="sxs-lookup"><span data-stu-id="34332-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="34332-116">`current` 引數是文字方塊中的目前值;`tag` 屬性是其他內容資料，可設定為 `NumericUpDown` 擴充項的屬性（但非必要）。</span><span class="sxs-lookup"><span data-stu-id="34332-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="34332-117">針對此範例，數值向上/向下控制項只能允許兩個的冪值：1、2、4、8、16、32、64等等。</span><span class="sxs-lookup"><span data-stu-id="34332-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="34332-118">因此，當使用者想要增加值時，所執行的方法必須是舊值的兩倍;另一個方法必須將值除以二。</span><span class="sxs-lookup"><span data-stu-id="34332-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="34332-119">以下是完整的 web 服務：</span><span class="sxs-lookup"><span data-stu-id="34332-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="34332-120">最後，建立新的 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="34332-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="34332-121">如同往常，您需要一個 `ScriptManager` 控制項、一個 `TextBox` 控制項和一個 `NumericUpDownExtender` 控制項。</span><span class="sxs-lookup"><span data-stu-id="34332-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="34332-122">對於後者，您必須提供 web 服務資訊：</span><span class="sxs-lookup"><span data-stu-id="34332-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="34332-123">下層 web 方法或頁面方法的 `ServiceDownMethod` 名稱</span><span class="sxs-lookup"><span data-stu-id="34332-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="34332-124">具有向下服務方法的 web 服務 `ServiceDownPath` 路徑;如果您使用頁面方法，則省略</span><span class="sxs-lookup"><span data-stu-id="34332-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="34332-125">up web 方法或 page 方法的 `ServiceUpMethod` 名稱</span><span class="sxs-lookup"><span data-stu-id="34332-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="34332-126">使用 up 服務方法 `ServiceUpPath` web 服務的路徑;如果您使用頁面方法，則省略</span><span class="sxs-lookup"><span data-stu-id="34332-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="34332-127">以下是頁面的完整標記：</span><span class="sxs-lookup"><span data-stu-id="34332-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="34332-128">如果您執行頁面，請注意文字方塊中的值在您按一下上方按鈕時，一律會加倍，而當您按一下下方按鈕時，則會減半。</span><span class="sxs-lookup"><span data-stu-id="34332-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>

<span data-ttu-id="34332-129">[僅 ![出現2乘冪的數位](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="34332-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="34332-130">只有2乘冪的數位才會出現（[按一下以觀看完整大小的影像](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="34332-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="34332-131">下一步</span><span class="sxs-lookup"><span data-stu-id="34332-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
