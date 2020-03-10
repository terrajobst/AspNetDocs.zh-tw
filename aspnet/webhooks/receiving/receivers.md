---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 接收器 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 接收者
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574190"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET Webhook 接收者

接收 Webhook 取決於寄件者是誰。 有時候註冊 WebHook 的額外步驟會確認訂閱者確實正在接聽。 有些 Webhook 會提供推播到提取模型，其中 HTTP POST 要求只包含事件資訊的參考，然後獨立抓取。 安全性模型通常會有相當大的差異。

Microsoft ASP.NET Webhook 的目的是要讓它更簡單且更一致，以連線到您的 API，而不需要花太多時間來瞭解如何處理任何特定的 Webhook 變體。

WebHook 接收者會負責接受和驗證來自特定寄件者的 Webhook。 WebHook 接收者可以支援任意數量的 Webhook，每個都有自己的設定。 例如，GitHub WebHook 接收器可以接受來自任意數目之 GitHub 存放庫的 Webhook。

## <a name="webhook-receiver-uris"></a>WebHook 接收者 Uri

藉由安裝 Microsoft ASP.NET Webhook，您會取得一般 WebHook 控制器，它會接受來自開放式服務數目的 WebHook 要求。 當要求抵達時，它會挑選您已安裝的適當接收者來處理特定的 WebHook 傳送者。

此控制器的 URI 是您向服務註冊的 WebHook URI，其格式如下：

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

基於安全性理由，許多 WebHook 接收者需要 URI 為*HTTPs* uri，而在某些情況下，它也必須包含額外的查詢參數，用來強制只有預定的合作物件可以將 webhook 傳送至上述 URI。

`<receiver>` 元件是接收者的名稱，例如 `github` 或 `slack`。

*{Id}* 是選擇性的識別碼，可以用來識別特定的 WebHook 接收者設定。 這可以用來向特定接收者註冊 N Webhook。 例如，下列三個 Uri 可以用來註冊三個獨立的 Webhook：

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>安裝 WebHook 接收器

若要使用 Microsoft ASP.NET Webhook 接收 Webhook，您必須先安裝 WebHook 提供者的 Nuget 套件，或您想要接收 Webhook 的來源提供者。 Nuget 套件的名稱為[webhook](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) ，其中最後一個部分指出支援的服務。 例如

[Webhook](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)會提供從 GitHub 和 Webhook 接收 webhook 的支援。[自訂](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)會提供接收 ASP.NET webhook 所產生 webhook 的支援。

您可以在這裡找到 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、時差、Stripe、Trello 和 WordPress 的支援，但可支援任何數目的其他提供者。

## <a name="configuring-a-webhook-receiver"></a>設定 WebHook 接收者

WebHook 接收者是透過[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)介面來設定，而且可以使用任何相依性插入模型來註冊該介面的特定實現。 預設的執行會使用可在 web.config 檔案中設定的應用程式設定，或者，如果使用 Azure Web Apps，可以透過[Azure 入口網站](https://portal.azure.com/)來設定。

![API 應用程式設定](_static/AzureAppSettings.png)

應用程式設定金鑰的格式如下：

```
MS_WebHookReceiverSecret_<receiver>
```

值是以逗號分隔的值清單，其中包含已註冊 Webhook 的 *{id}* 值，例如：

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>初始化 WebHook 接收者

藉由登錄 WebHook 接收器，通常是在*WebApiConfig*靜態類別中進行初始化，例如：

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
