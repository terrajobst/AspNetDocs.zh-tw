---
uid: webhooks/index
title: ASP.NET Webhook 總覽 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 簡介。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa65a20e1af16d58533e37fafc77ac246e0fe327
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000736"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="4b5fe-103">ASP.NET Webhook 總覽</span><span class="sxs-lookup"><span data-stu-id="4b5fe-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="4b5fe-104">Webhook 是輕量的 HTTP 模式，提供簡單的 pub/sub 模型，可將 Web Api 和 SaaS 服務串聯在一起。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="4b5fe-105">當服務中發生事件時，會以 HTTP POST 要求的形式將通知傳送給已註冊的訂閱者。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="4b5fe-106">POST 要求包含事件的相關資訊，讓接收者可以據以採取動作。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="4b5fe-107">基於其簡單性，Webhook 已由大量服務公開，包括[Dropbox](http://dropbox.com/)、 [GitHub](http://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、[時差](http://www.slack.com) [、等量、](http://www.stripe.com) [Trello](http://www.trello.com/)和許多個.</span><span class="sxs-lookup"><span data-stu-id="4b5fe-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="4b5fe-108">例如，WebHook 可能表示檔案在[Dropbox](http://dropbox.com/)中已變更，或 GitHub 中的程式碼變更已認可，或已在[PayPal](http://www.paypal.com/)中起始付款，或已在[Trello](http://www.trello.com/)中建立了卡片。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="4b5fe-109">可能性非常無限！</span><span class="sxs-lookup"><span data-stu-id="4b5fe-109">The possibilities are endless!</span></span>

<span data-ttu-id="4b5fe-110">Microsoft ASP.NET Webhook 可讓您更輕鬆地在 ASP.NET 應用程式中傳送和接收 Webhook：</span><span class="sxs-lookup"><span data-stu-id="4b5fe-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="4b5fe-111">在接收端，它提供從任何數目的 WebHook 提供者接收和處理 Webhook 的通用模型。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="4b5fe-112">它已提供[Dropbox](http://dropbox.com/)、 [GitHub](http://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、 [Pusher](http://www.pusher.com)、 [Salesforce](http://www.salesforce.com)、[時差](http://www.slack.com) [、等量、](http://www.stripe.com) [Trello](http://www.trello.com/)、[WordPress](http://www.wordpress.com)和的支援[Zendesk](https://www.zendesk.com/) ，但可輕鬆新增更多支援。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="4b5fe-113">在傳送端，它會提供管理和儲存訂閱的支援，以及將事件通知傳送到正確的訂閱者集合。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="4b5fe-114">這可讓您定義自己的一組事件，訂閱者可以訂閱並在發生事情時通知他們。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="4b5fe-115">這兩個部分可以根據您的案例一起或分開使用。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="4b5fe-116">如果您只需要接收來自其他服務的 Webhook，則可以只使用接收者部分;如果您只想要公開 Webhook 供其他人使用，那麼您就可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="4b5fe-117">程式碼會以 ASP.NET Web API 2 和 ASP.NET MVC 5 為目標，並可[在 GitHub 上作為 OSS](https://github.com/aspnet/WebHooks)。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="4b5fe-118">Webhook 總覽</span><span class="sxs-lookup"><span data-stu-id="4b5fe-118">WebHooks Overview</span></span>

<span data-ttu-id="4b5fe-119">Webhook 是一種模式，這表示它會改變從服務到服務的使用方式，但基本概念是一樣的。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="4b5fe-120">您可以將 Webhook 視為簡單的 pub/sub 模型，使用者可以在其中訂閱其他地方發生的事件。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="4b5fe-121">事件通知會傳播為 HTTP POST 要求，其中包含事件本身的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="4b5fe-122">一般來說，HTTP POST 要求會包含由 WebHook 傳送者決定的 JSON 物件或 HTML 表單資料，包括導致 WebHook 觸發的事件相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="4b5fe-123">例如，來自[GitHub](http://www.github.com/)的 WebHook POST 要求主體看起來會像是在特定存放庫中開啟新問題所導致的結果：</span><span class="sxs-lookup"><span data-stu-id="4b5fe-123">For example, a WebHook POST request body from [GitHub](http://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="4b5fe-124">為了確保 WebHook 確實來自預定的寄件者，POST 要求會以某種方式受到保護，然後由接收者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="4b5fe-125">例如， [GitHub webhook](https://developer.github.com/webhooks/)包含一個*X-Hub-Signature* HTTP 標頭，其中包含由接收者執行檢查的要求主體雜湊，因此您不必擔心它。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="4b5fe-126">WebHook 流程通常會如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b5fe-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="4b5fe-127">WebHook 寄件者會公開用戶端可以訂閱的事件。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="4b5fe-128">這些事件描述系統可觀察的變更，例如已插入新資料項目、進程已完成，或其他專案。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="4b5fe-129">WebHook 接收者會藉由註冊包含四個專案的 WebHook 來進行訂閱：</span><span class="sxs-lookup"><span data-stu-id="4b5fe-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="4b5fe-130">應在其中張貼事件通知的 URI，其格式為 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="4b5fe-131">描述應引發 WebHook 之特定事件的一組篩選準則;</span><span class="sxs-lookup"><span data-stu-id="4b5fe-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="4b5fe-132">用來簽署 HTTP POST 要求的秘密金鑰;</span><span class="sxs-lookup"><span data-stu-id="4b5fe-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="4b5fe-133">要包含在 HTTP POST 要求中的其他資料。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="4b5fe-134">例如，這可以是 HTTP POST 要求主體中包含的其他 HTTP 標頭欄位或屬性。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="4b5fe-135">一旦發生事件，就會找到相符的 WebHook 註冊，並提交 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="4b5fe-136">一般來說，如果因為某些原因而導致收件者沒有回應，或 HTTP POST 要求造成錯誤回應，則會重試產生 HTTP POST 要求數次。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="4b5fe-137">Webhook 處理管線</span><span class="sxs-lookup"><span data-stu-id="4b5fe-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="4b5fe-138">傳入 Webhook 的 Microsoft ASP.NET Webhook 處理管線看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4b5fe-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET Webhook 處理管線](_static/WebHookReceivers.png)

<span data-ttu-id="4b5fe-140">這裡的兩個重要概念是*接收者*和*處理常式*：</span><span class="sxs-lookup"><span data-stu-id="4b5fe-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="4b5fe-141">*接收者*會負責處理給定傳送者的特定 WebHook 類別，以及強制執行安全性檢查，以確保 WebHook 要求確實來自預定的寄件者。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="4b5fe-142">*處理常式*通常會在其中執行使用者程式碼來處理特定的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="4b5fe-143">在下列節點中，會詳細說明這些概念。</span><span class="sxs-lookup"><span data-stu-id="4b5fe-143">In the following nodes these concepts are described in more details.</span></span>
