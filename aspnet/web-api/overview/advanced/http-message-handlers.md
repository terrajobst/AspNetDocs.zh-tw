---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API 中的 HTTP 訊息處理常式-ASP.NET 4。x
author: MikeWasson
description: ASP.NET 4.x 的 ASP.NET Web API 中的 HTTP 訊息處理常式總覽
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622581"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 中的 HTTP 訊息處理常式

由[Mike Wasson](https://github.com/MikeWasson)

*訊息處理常式*是接收 HTTP 要求並傳回 HTTP 回應的類別。 訊息處理常式衍生自抽象**HttpMessageHandler**類別。

通常會將一系列的訊息處理常式連結在一起。 第一個處理常式會接收 HTTP 要求、進行某些處理，並將要求提供給下一個處理常式。 在某個時間點，會建立回應，並備份鏈。 這個模式稱為*委派*處理常式。

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a>伺服器端訊息處理常式

在伺服器端，Web API 管線會使用一些內建的訊息處理常式：

- **HttpServer**會從主機取得要求。
- **HttpRoutingDispatcher**會根據路由分派要求。
- **System.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**會將要求傳送至 Web API 控制器。

您可以將自訂處理常式新增至管線。 訊息處理常式適用于在 HTTP 訊息層級（而不是控制器動作）上運作的跨領域考慮。 例如，訊息處理常式可能會：

- 讀取或修改要求標頭。
- 將回應標頭新增至回應。
- 先驗證要求，然後再到達控制器。

下圖顯示兩個插入管線的自訂處理常式：

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> 在用戶端上，HttpClient 也會使用訊息處理常式。 如需詳細資訊，請參閱[HttpClient 訊息處理常式](httpclient-message-handlers.md)。

## <a name="custom-message-handlers"></a>自訂訊息處理常式

若要撰寫自訂訊息處理常式，請從**DelegatingHandler**衍生，並覆寫**SendAsync**方法。 此方法具有下列簽章：

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

方法會採用**HttpRequestMessage**做為輸入，並以非同步方式傳回**HttpResponseMessage**。 一般的執行會執行下列動作：

1. 處理要求訊息。
2. 呼叫 `base.SendAsync` 以將要求傳送至內部處理常式。
3. 內部處理常式會傳迴響應消息。 （此步驟是非同步）。
4. 處理回應，並將它傳回給呼叫者。

以下是一個簡單的範例：

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> 對 `base.SendAsync` 的呼叫是非同步的。 如果處理常式在此呼叫之後執行任何工作，請使用**await**關鍵字，如下所示。

委派處理常式也可以略過內部處理常式，並直接建立回應：

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

如果委派處理常式在沒有呼叫 `base.SendAsync`的情況下建立回應，則要求會略過管線的其餘部分。 這適用于驗證要求的處理常式（建立錯誤回應）。

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a>將處理常式新增至管線

若要在伺服器端加入訊息處理常式，請將處理常式加入至**HttpConfiguration. MessageHandlers**集合。 如果您使用「ASP.NET MVC 4 Web 應用程式」範本來建立專案，您可以在**WebApiConfig**類別內執行此動作：

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

訊息處理常式的呼叫順序，會與它們出現在**MessageHandlers**收集中的順序相同。 因為它們是嵌套的，回應訊息會以另一個方向移動。 也就是，最後一個處理常式是取得回應訊息的第一個。

請注意，您不需要設定內部處理常式;Web API 架構會自動連接訊息處理常式。

如果您是[自我裝載](../older-versions/self-host-a-web-api.md)，請建立**HttpSelfHostConfiguration**類別的實例，並將處理常式新增至**MessageHandlers**集合。

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

現在讓我們來看一些自訂訊息處理常式的範例。

## <a name="example-x-http-method-override"></a>範例： X-HTTP-方法-覆寫

X-HTTP-方法-覆寫是非標準的 HTTP 標頭。 它是針對無法傳送特定 HTTP 要求類型的用戶端所設計，例如 PUT 或 DELETE。 相反地，用戶端會傳送 POST 要求，並將 X-HTTP 方法覆寫標頭設定為所需的方法。 例如:

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

以下是新增 X-HTTP 方法覆寫支援的訊息處理常式：

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

在**SendAsync**方法中，處理常式會檢查要求訊息是否為 POST 要求，以及它是否包含 X-HTTP 方法覆寫標頭。 若是如此，它會驗證標頭值，然後修改要求方法。 最後，處理常式會呼叫 `base.SendAsync`，將訊息傳遞至下一個處理常式。

當要求到達**system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**類別時， **system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**會根據更新的要求方法來路由傳送要求。

## <a name="example-adding-a-custom-response-header"></a>範例：新增自訂回應標頭

以下是將自訂標頭新增至每個回應訊息的訊息處理常式：

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

首先，處理常式會呼叫 `base.SendAsync`，將要求傳遞至內部訊息處理常式。 內部處理常式會傳迴響應消息，但它會使用工作 **&lt;t&gt;** 物件以非同步方式執行。 除非 `base.SendAsync` 非同步完成，否則無法使用回應訊息。

這個範例會使用**await**關鍵字，在 `SendAsync` 完成後以非同步方式執行工作。 如果您的目標是 .NET Framework 4.0，請**使用&lt;t**&gt;的工作 **。System.threading.tasks.task.continuewith**方法：

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a>範例：檢查 API 金鑰

某些 web 服務要求用戶端在其要求中包含 API 金鑰。 下列範例會顯示訊息處理常式如何檢查有效 API 金鑰的要求：

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

此處理程式會在 URI 查詢字串中尋找 API 金鑰。 （在此範例中，我們假設金鑰是靜態字串。 實際的執行可能會使用更複雜的驗證。）如果查詢字串包含索引鍵，則處理常式會將要求傳遞給內部處理常式。

如果要求沒有有效的索引鍵，則處理常式會建立狀態為403、禁止的回應訊息。 在此情況下，處理常式不會呼叫 `base.SendAsync`，因此內部處理常式永遠不會接收要求，也不會執行控制器。 因此，控制器可以假設所有連入要求都具有有效的 API 金鑰。

> [!NOTE]
> 如果 API 金鑰僅適用于特定的控制器動作，請考慮使用動作篩選，而不是訊息處理常式。 動作篩選準則會在 URI 路由執行之後執行。

## <a name="per-route-message-handlers"></a>每個路由訊息處理常式

**HttpConfiguration. MessageHandlers**集合中的處理常式會全域套用。

或者，您可以在定義路由時，將訊息處理常式新增至特定的路由：

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

在此範例中，如果要求 URI 符合 "Route2"，則會將要求分派給 `MessageHandler2`。 下圖顯示這兩個路由的管線：

![](http-message-handlers/_static/image4.png)

請注意，`MessageHandler2` 取代預設的**system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**。 在此範例中，`MessageHandler2` 會建立回應，且符合 "Route2" 的要求永遠不會移至控制器。 這可讓您將整個 Web API 控制器機制取代為您自己的自訂端點。

或者，每個路由的訊息處理常式可以委派給**system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**，然後再分派給控制器。

![](http-message-handlers/_static/image5.png)

下列程式碼顯示如何設定此路由：

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
