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
# <a name="aspnet-webhooks-overview"></a>ASP.NET Webhook 總覽

Webhook 是輕量的 HTTP 模式，提供簡單的 pub/sub 模型，可將 Web Api 和 SaaS 服務串聯在一起。 當服務中發生事件時，會以 HTTP POST 要求的形式將通知傳送給已註冊的訂閱者。 POST 要求包含事件的相關資訊，讓接收者可以據以採取動作。

基於其簡單性，Webhook 已由大量服務公開，包括[Dropbox](http://dropbox.com/)、 [GitHub](http://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、[時差](http://www.slack.com) [、等量、](http://www.stripe.com) [Trello](http://www.trello.com/)和許多個. 例如，WebHook 可能表示檔案在[Dropbox](http://dropbox.com/)中已變更，或 GitHub 中的程式碼變更已認可，或已在[PayPal](http://www.paypal.com/)中起始付款，或已在[Trello](http://www.trello.com/)中建立了卡片。 可能性非常無限！

Microsoft ASP.NET Webhook 可讓您更輕鬆地在 ASP.NET 應用程式中傳送和接收 Webhook：

* 在接收端，它提供從任何數目的 WebHook 提供者接收和處理 Webhook 的通用模型。 它已提供[Dropbox](http://dropbox.com/)、 [GitHub](http://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、 [Pusher](http://www.pusher.com)、 [Salesforce](http://www.salesforce.com)、[時差](http://www.slack.com) [、等量、](http://www.stripe.com) [Trello](http://www.trello.com/)、[WordPress](http://www.wordpress.com)和的支援[Zendesk](https://www.zendesk.com/) ，但可輕鬆新增更多支援。

* 在傳送端，它會提供管理和儲存訂閱的支援，以及將事件通知傳送到正確的訂閱者集合。 這可讓您定義自己的一組事件，訂閱者可以訂閱並在發生事情時通知他們。

這兩個部分可以根據您的案例一起或分開使用。 如果您只需要接收來自其他服務的 Webhook，則可以只使用接收者部分;如果您只想要公開 Webhook 供其他人使用，那麼您就可以這麼做。

程式碼會以 ASP.NET Web API 2 和 ASP.NET MVC 5 為目標，並可[在 GitHub 上作為 OSS](https://github.com/aspnet/WebHooks)。

## <a name="webhooks-overview"></a>Webhook 總覽

Webhook 是一種模式，這表示它會改變從服務到服務的使用方式，但基本概念是一樣的。 您可以將 Webhook 視為簡單的 pub/sub 模型，使用者可以在其中訂閱其他地方發生的事件。 事件通知會傳播為 HTTP POST 要求，其中包含事件本身的相關資訊。

一般來說，HTTP POST 要求會包含由 WebHook 傳送者決定的 JSON 物件或 HTML 表單資料，包括導致 WebHook 觸發的事件相關資訊。 例如，來自[GitHub](http://www.github.com/)的 WebHook POST 要求主體看起來會像是在特定存放庫中開啟新問題所導致的結果：

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

為了確保 WebHook 確實來自預定的寄件者，POST 要求會以某種方式受到保護，然後由接收者進行驗證。 例如， [GitHub webhook](https://developer.github.com/webhooks/)包含一個*X-Hub-Signature* HTTP 標頭，其中包含由接收者執行檢查的要求主體雜湊，因此您不必擔心它。

WebHook 流程通常會如下所示：

* WebHook 寄件者會公開用戶端可以訂閱的事件。 這些事件描述系統可觀察的變更，例如已插入新資料項目、進程已完成，或其他專案。

* WebHook 接收者會藉由註冊包含四個專案的 WebHook 來進行訂閱：

     1. 應在其中張貼事件通知的 URI，其格式為 HTTP POST 要求。

     2. 描述應引發 WebHook 之特定事件的一組篩選準則;

     3. 用來簽署 HTTP POST 要求的秘密金鑰;

     4. 要包含在 HTTP POST 要求中的其他資料。 例如，這可以是 HTTP POST 要求主體中包含的其他 HTTP 標頭欄位或屬性。

* 一旦發生事件，就會找到相符的 WebHook 註冊，並提交 HTTP POST 要求。 一般來說，如果因為某些原因而導致收件者沒有回應，或 HTTP POST 要求造成錯誤回應，則會重試產生 HTTP POST 要求數次。

## <a name="webhooks-processing-pipeline"></a>Webhook 處理管線

傳入 Webhook 的 Microsoft ASP.NET Webhook 處理管線看起來像這樣：

![ASP.NET Webhook 處理管線](_static/WebHookReceivers.png)

這裡的兩個重要概念是*接收者*和*處理常式*：

* *接收者*會負責處理給定傳送者的特定 WebHook 類別，以及強制執行安全性檢查，以確保 WebHook 要求確實來自預定的寄件者。

* *處理常式*通常會在其中執行使用者程式碼來處理特定的 WebHook。

在下列節點中，會詳細說明這些概念。
