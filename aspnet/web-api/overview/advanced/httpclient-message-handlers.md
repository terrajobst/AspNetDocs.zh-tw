---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API-ASP.NET 4.x 中的 HttpClient 訊息處理常式
author: MikeWasson
description: 在 ASP.NET 4.x 中建立 ASP.NET Web API 的自訂訊息處理常式
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557642"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="b6bfe-103">ASP.NET Web API 中的 HttpClient 訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="b6bfe-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="b6bfe-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b6bfe-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b6bfe-105">*訊息處理常式*是接收 HTTP 要求並傳回 HTTP 回應的類別。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="b6bfe-106">通常會將一系列的訊息處理常式連結在一起。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="b6bfe-107">第一個處理常式會接收 HTTP 要求、進行某些處理，並將要求提供給下一個處理常式。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="b6bfe-108">在某個時間點，會建立回應，並備份鏈。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="b6bfe-109">這個模式稱為*委派*處理常式。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="b6bfe-110">在用戶端上， **HttpClient**類別會使用訊息處理常式來處理要求。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="b6bfe-111">預設處理常式是**HttpClientHandler**，它會透過網路傳送要求，並從伺服器取得回應。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="b6bfe-112">您可以將自訂訊息處理常式插入至用戶端管線：</span><span class="sxs-lookup"><span data-stu-id="b6bfe-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="b6bfe-113">ASP.NET Web API 也會使用伺服器端的訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="b6bfe-114">如需詳細資訊，請參閱[HTTP 訊息處理常式](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="b6bfe-115">自訂訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="b6bfe-115">Custom Message Handlers</span></span>

<span data-ttu-id="b6bfe-116">若要撰寫自訂訊息處理常式，請從**DelegatingHandler**衍生，並覆寫**SendAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="b6bfe-117">以下是方法簽章：</span><span class="sxs-lookup"><span data-stu-id="b6bfe-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="b6bfe-118">方法會採用**HttpRequestMessage**做為輸入，並以非同步方式傳回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="b6bfe-119">一般的執行會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="b6bfe-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="b6bfe-120">處理要求訊息。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-120">Process the request message.</span></span>
2. <span data-ttu-id="b6bfe-121">呼叫 `base.SendAsync` 以將要求傳送至內部處理常式。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="b6bfe-122">內部處理常式會傳迴響應消息。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-122">The inner handler returns a response message.</span></span> <span data-ttu-id="b6bfe-123">（此步驟是非同步）。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="b6bfe-124">處理回應，並將它傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="b6bfe-125">下列範例顯示的訊息處理常式會將自訂標頭新增至傳出要求：</span><span class="sxs-lookup"><span data-stu-id="b6bfe-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="b6bfe-126">對 `base.SendAsync` 的呼叫是非同步的。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="b6bfe-127">如果處理常式在此呼叫之後執行任何工作，請在方法完成後使用**await**關鍵字來繼續執行。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="b6bfe-128">下列範例顯示記錄錯誤碼的處理常式。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="b6bfe-129">記錄本身並不重要，但此範例會示範如何取得處理常式內的回應。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="b6bfe-130">將訊息處理常式新增至用戶端管線</span><span class="sxs-lookup"><span data-stu-id="b6bfe-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="b6bfe-131">若要將自訂處理常式新增至**HttpClient**，請使用**HttpClientFactory. Create**方法：</span><span class="sxs-lookup"><span data-stu-id="b6bfe-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="b6bfe-132">訊息處理常式的呼叫順序如下：您將其傳遞至**Create**方法。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="b6bfe-133">因為處理常式是嵌套的，回應訊息會以另一個方向移動。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="b6bfe-134">也就是，最後一個處理常式是取得回應訊息的第一個。</span><span class="sxs-lookup"><span data-stu-id="b6bfe-134">That is, the last handler is the first to get the response message.</span></span>
