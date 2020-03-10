---
uid: webhooks/receiving/handlers
title: ASP.NET Webhook 處理常式 |Microsoft Docs
author: rick-anderson
description: 如何處理 ASP.NET Webhook 中的要求。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637869"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="f88c0-103">ASP.NET Webhook 處理常式</span><span class="sxs-lookup"><span data-stu-id="f88c0-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="f88c0-104">一旦 WebHook 接收者驗證 Webhook 要求之後，就可以由使用者程式碼進行處理。</span><span class="sxs-lookup"><span data-stu-id="f88c0-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="f88c0-105">這就是*處理常式*的來源。</span><span class="sxs-lookup"><span data-stu-id="f88c0-105">This is where *handlers* come in.</span></span> <span data-ttu-id="f88c0-106">處理常式衍生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)介面，但通常會使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)類別，而不是直接衍生自介面。</span><span class="sxs-lookup"><span data-stu-id="f88c0-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="f88c0-107">WebHook 要求可由一或多個處理常式處理。</span><span class="sxs-lookup"><span data-stu-id="f88c0-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="f88c0-108">處理常式會根據其各自的*order*屬性（從最低到最高）順序來呼叫，其中 order 是簡單的整數（建議介於1到100之間）：</span><span class="sxs-lookup"><span data-stu-id="f88c0-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 處理常式順序屬性圖表](_static/Handlers.png)

<span data-ttu-id="f88c0-110">處理常式可以選擇性地在 WebHookHandlerCoNtext 上設定*回應*屬性，這會導致處理停止，並將回應傳回為 WEBHOOK 的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="f88c0-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="f88c0-111">在上述情況中，處理常式 C 不會被呼叫，因為它的順序高於 B，而 B 設定回應。</span><span class="sxs-lookup"><span data-stu-id="f88c0-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="f88c0-112">設定回應通常僅與 Webhook 相關，回應會將資訊傳回給原始 API。</span><span class="sxs-lookup"><span data-stu-id="f88c0-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="f88c0-113">這是例如，具有時差的案例 Webhook，其中會將回應回傳至 WebHook 來源的通道。</span><span class="sxs-lookup"><span data-stu-id="f88c0-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="f88c0-114">如果處理常式只想接收來自該特定接收者的 Webhook，則可以設定接收者屬性。</span><span class="sxs-lookup"><span data-stu-id="f88c0-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="f88c0-115">如果未設定接收者，則會對所有使用者呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="f88c0-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="f88c0-116">回應的另一個常見用法是使用*410 消失*的回應，指出 WebHook 不再作用中，而且不會再提交進一步的要求。</span><span class="sxs-lookup"><span data-stu-id="f88c0-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="f88c0-117">根據預設，所有 WebHook 接收者都會呼叫處理常式。</span><span class="sxs-lookup"><span data-stu-id="f88c0-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="f88c0-118">不過，如果*接收者*屬性設定為處理常式的名稱，則該處理常式只會接收來自該接收者的 WebHook 要求。</span><span class="sxs-lookup"><span data-stu-id="f88c0-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="f88c0-119">處理 WebHook</span><span class="sxs-lookup"><span data-stu-id="f88c0-119">Processing a WebHook</span></span>

<span data-ttu-id="f88c0-120">呼叫處理常式時，它會取得[WebHookHandlerCoNtext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) ，其中包含 WebHook 要求的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f88c0-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="f88c0-121">資料（通常是 HTTP 要求主體）可從*資料*屬性取得。</span><span class="sxs-lookup"><span data-stu-id="f88c0-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="f88c0-122">資料的類型通常是 JSON 或 HTML 表單資料，但如果需要，可以轉型為更特定的類型。</span><span class="sxs-lookup"><span data-stu-id="f88c0-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="f88c0-123">例如，ASP.NET Webhook 所產生的自訂 Webhook 可以轉換成類型[CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f88c0-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="f88c0-124">佇列處理</span><span class="sxs-lookup"><span data-stu-id="f88c0-124">Queued Processing</span></span>

<span data-ttu-id="f88c0-125">如果不是在幾秒內產生回應，大部分的 WebHook 傳送者都會重新傳送 WebHook。</span><span class="sxs-lookup"><span data-stu-id="f88c0-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="f88c0-126">這表示您的處理常式必須在該時間範圍內完成處理，才能再次呼叫它。</span><span class="sxs-lookup"><span data-stu-id="f88c0-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="f88c0-127">如果處理需要較長的時間，或分別進行更好的處理，則可以使用[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)將 WebHook 要求提交至佇列，例如[Azure 儲存體的佇列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f88c0-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="f88c0-128">這裡提供[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)執行的大綱：</span><span class="sxs-lookup"><span data-stu-id="f88c0-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
