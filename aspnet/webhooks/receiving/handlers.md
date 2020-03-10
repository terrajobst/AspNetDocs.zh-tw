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
# <a name="aspnet-webhooks-handlers"></a>ASP.NET Webhook 處理常式

一旦 WebHook 接收者驗證 Webhook 要求之後，就可以由使用者程式碼進行處理。 這就是*處理常式*的來源。 處理常式衍生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)介面，但通常會使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)類別，而不是直接衍生自介面。

WebHook 要求可由一或多個處理常式處理。 處理常式會根據其各自的*order*屬性（從最低到最高）順序來呼叫，其中 order 是簡單的整數（建議介於1到100之間）：

![WebHook 處理常式順序屬性圖表](_static/Handlers.png)

處理常式可以選擇性地在 WebHookHandlerCoNtext 上設定*回應*屬性，這會導致處理停止，並將回應傳回為 WEBHOOK 的 HTTP 回應。 在上述情況中，處理常式 C 不會被呼叫，因為它的順序高於 B，而 B 設定回應。

設定回應通常僅與 Webhook 相關，回應會將資訊傳回給原始 API。 這是例如，具有時差的案例 Webhook，其中會將回應回傳至 WebHook 來源的通道。 如果處理常式只想接收來自該特定接收者的 Webhook，則可以設定接收者屬性。 如果未設定接收者，則會對所有使用者呼叫它們。

回應的另一個常見用法是使用*410 消失*的回應，指出 WebHook 不再作用中，而且不會再提交進一步的要求。

根據預設，所有 WebHook 接收者都會呼叫處理常式。 不過，如果*接收者*屬性設定為處理常式的名稱，則該處理常式只會接收來自該接收者的 WebHook 要求。

## <a name="processing-a-webhook"></a>處理 WebHook

呼叫處理常式時，它會取得[WebHookHandlerCoNtext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) ，其中包含 WebHook 要求的相關資訊。 資料（通常是 HTTP 要求主體）可從*資料*屬性取得。

資料的類型通常是 JSON 或 HTML 表單資料，但如果需要，可以轉型為更特定的類型。 例如，ASP.NET Webhook 所產生的自訂 Webhook 可以轉換成類型[CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) ，如下所示：

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

  ## <a name="queued-processing"></a>佇列處理

如果不是在幾秒內產生回應，大部分的 WebHook 傳送者都會重新傳送 WebHook。 這表示您的處理常式必須在該時間範圍內完成處理，才能再次呼叫它。

如果處理需要較長的時間，或分別進行更好的處理，則可以使用[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)將 WebHook 要求提交至佇列，例如[Azure 儲存體的佇列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。

這裡提供[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)執行的大綱：

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
