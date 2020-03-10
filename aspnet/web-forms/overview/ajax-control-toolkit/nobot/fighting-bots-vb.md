---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: 對抗 Bot （VB） |Microsoft Docs
author: wenz
description: 自動化機器人會 plaster weblog 和其他具有垃圾郵件的網站，並在沒有任何使用者互動的情況下提交留言表單。 ASP.NET AJAX Con 中的 NoBot 控制項 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: a8ca71b96cb84c97b1a60ae6a3d1a129cd1b0b10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627390"
---
# <a name="fighting-bots-vb"></a><span data-ttu-id="7a2d0-104">對抗 Bot (VB)</span><span class="sxs-lookup"><span data-stu-id="7a2d0-104">Fighting Bots (VB)</span></span>

<span data-ttu-id="7a2d0-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7a2d0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7a2d0-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7a2d0-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span></span>

> <span data-ttu-id="7a2d0-107">自動化機器人會 plaster weblog 和其他具有垃圾郵件的網站，並在沒有任何使用者互動的情況下提交留言表單。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="7a2d0-108">ASP.NET AJAX 控制項工具組中的 NoBot 控制項可協助對抗這些 bot。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="overview"></a><span data-ttu-id="7a2d0-109">概觀</span><span class="sxs-lookup"><span data-stu-id="7a2d0-109">Overview</span></span>

<span data-ttu-id="7a2d0-110">自動化機器人會 plaster weblog 和其他具有垃圾郵件的網站，並在沒有任何使用者互動的情況下提交留言表單。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="7a2d0-111">ASP.NET AJAX 控制項工具組中的 NoBot 控制項可協助對抗這些 bot。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="7a2d0-112">步驟</span><span class="sxs-lookup"><span data-stu-id="7a2d0-112">Steps</span></span>

<span data-ttu-id="7a2d0-113">擊敗 bot 的一個常見方法是使用 CAPTCHAs 完全自動化的公用 Turing 測試，以告訴電腦和人類的與眾不同之處。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="7a2d0-114">Turing 測試原本就是一種測試，其中有人需要決定通訊夥伴是人或電腦。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="7a2d0-115">在 web 中，CAPTCHA 通常是由影像所組成，其中包含一些失真字母。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="7a2d0-116">其概念是，只有人可以讀取影像上的字母，而 OCR 演算法將會失敗。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="7a2d0-117">這種方法有幾個優點和缺點，但這項討論已超出本教學課程的範圍。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="7a2d0-118">不過，ASP.NET AJAX 控制項工具組中的控制項提供類似的方法： `NoBot`。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="7a2d0-119">比起 CAPTCHA 更容易克服，但是很容易就能使用和車資在類似 blog 的網站上，如果大部分的垃圾郵件嘗試都失效，`NoBot` 控制項就會被視為成功。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="7a2d0-120">如果至少符合下列其中一個條件，`NoBot` 會攔截目前 ASP.NET web 表單的回傳：</span><span class="sxs-lookup"><span data-stu-id="7a2d0-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="7a2d0-121">瀏覽器無法解決 JavaScript 謎題（例如，當 JavaScript 停用時）</span><span class="sxs-lookup"><span data-stu-id="7a2d0-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="7a2d0-122">使用者已將表單提交到快速</span><span class="sxs-lookup"><span data-stu-id="7a2d0-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="7a2d0-123">用戶端 IP 位址在一段時間內提交表單的頻率太高。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="7a2d0-124">若要檢查這些條件，`NoBot` 控制項需要這些屬性（全部都是選擇性的）：</span><span class="sxs-lookup"><span data-stu-id="7a2d0-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="7a2d0-125">`ResponseMinimumDelaySeconds` 回傳之間的最小秒數</span><span class="sxs-lookup"><span data-stu-id="7a2d0-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="7a2d0-126">`CutoffWindowSeconds` 某個 IP 的回傳為量值的時間間隔長度</span><span class="sxs-lookup"><span data-stu-id="7a2d0-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="7a2d0-127">`CutoffMaximumInstances` 每個時間間隔的最大秒數</span><span class="sxs-lookup"><span data-stu-id="7a2d0-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="7a2d0-128">下列標記要求在回傳之間至少有兩秒鐘的時間，而且30秒間隔內只有五個回傳或小於：</span><span class="sxs-lookup"><span data-stu-id="7a2d0-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

<span data-ttu-id="7a2d0-129">然後，如同往常一般，請務必將 `ScriptManager` 包含在頁面中，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="7a2d0-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

<span data-ttu-id="7a2d0-130">由於大部分的檢查 `NoBot` 是在伺服器端進行，因此您必須檢查這些驗證的結果。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="7a2d0-131">這可以藉由呼叫 `NoBot`的 `IsValid()` 方法來完成。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="7a2d0-132">它有一個 `NoBotState`類型的引數（做為 `out` 參數/`ByRef` 參數）。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="7a2d0-133">其字串標記法包含檢查失敗的原因，否則 `Valid`。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="7a2d0-134">下列程式碼會根據 `NoBot`的結果來輸出訊息：</span><span class="sxs-lookup"><span data-stu-id="7a2d0-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

<span data-ttu-id="7a2d0-135">最後，您需要提交表單，並使用 label 元素來輸出訊息，而且您已完成！</span><span class="sxs-lookup"><span data-stu-id="7a2d0-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

<span data-ttu-id="7a2d0-136">當您執行此腳本並停用 JavaScript，或在前兩秒內提交表單，或在三十秒內提交表單七次時，您會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="7a2d0-137">不過，請謹慎使用此控制項，因為只有大約有90-95% 的使用者已啟用 JavaScript，因此5-10% 的使用者將會失敗 `NoBot`的測試。</span><span class="sxs-lookup"><span data-stu-id="7a2d0-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>

<span data-ttu-id="7a2d0-138">[![此錯誤訊息可能是 bot 所造成](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7a2d0-138">[![This error message could have been caused by a bot](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span></span>

<span data-ttu-id="7a2d0-139">此錯誤訊息可能是 bot 造成的（[按一下以觀看完整大小的影像](fighting-bots-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="7a2d0-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7a2d0-140">上一篇</span><span class="sxs-lookup"><span data-stu-id="7a2d0-140">Previous</span></span>](fighting-bots-cs.md)
