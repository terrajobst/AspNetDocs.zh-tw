---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2-ASP.NET 4.x 中的動作結果
author: MikeWasson
description: 描述 ASP.NET Web API 如何將控制器動作的傳回值轉換成 ASP.NET 4.x 中的 HTTP 回應訊息。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985842"
---
# <a name="action-results-in-web-api-2"></a>Web API 2 中的動作結果

[!INCLUDE[](~/includes/coreWebAPI.md)]

本主題描述 ASP.NET Web API 如何將控制器動作的傳回值轉換為 HTTP 回應訊息。

Web API 控制器動作可以傳回下列任何一項：

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. 其他類型

根據傳回的是哪一個，Web API 會使用不同的機制來建立 HTTP 回應。

| 傳回類型 | Web API 如何建立回應 |
| --- | --- |
| void | 傳回空的204（沒有內容） |
| **HttpResponseMessage** | 直接轉換為 HTTP 回應訊息。 |
| **IHttpActionResult** | 呼叫**ExecuteAsync**以建立**HttpResponseMessage**，然後轉換為 HTTP 回應訊息。 |
| 其他類型 | 將序列化的傳回值寫入回應主體;傳回200（確定）。 |

本主題的其餘部分將更詳細地說明每個選項。

## <a name="void"></a>void

如果傳回型別為`void`，Web API 只會傳回空的 HTTP 回應，狀態碼為204（沒有內容）。

範例控制器：

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP 回應：

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

如果動作傳回[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)，Web API 會使用**HttpResponseMessage**物件的屬性來填入回應，將傳回值直接轉換為 HTTP 回應訊息。

此選項可讓您對回應訊息有很大的控制權。 例如，下列控制器動作會設定快取控制標頭。

[!code-csharp[Main](action-results/samples/sample3.cs)]

回應：

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

如果您將領域模型傳遞至**CreateResponse**方法，Web API 會使用[媒體格式](../formats-and-model-binding/media-formatters.md)器將序列化的模型寫入回應主體。

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API 會在要求中使用 Accept 標頭來選擇格式器。 如需詳細資訊，請參閱[內容協商](../formats-and-model-binding/content-negotiation.md)。

## <a name="ihttpactionresult"></a>IHttpActionResult

**應傳回 iHTTPactionresult**介面是在 Web API 2 中引進。 基本上，它會定義**HttpResponseMessage** factory。 以下是使用**應傳回 iHTTPactionresult**介面的一些優點：

- 簡化控制器的[單元測試](../testing-and-debugging/unit-testing-controllers-in-web-api.md)。
- 將建立 HTTP 回應的常見邏輯移至不同的類別。
- 藉由隱藏用來建立回應的低層級詳細資料，讓控制器動作的意圖更清楚。

**應傳回 iHTTPactionresult**包含單一方法**ExecuteAsync**，它會以非同步方式建立**HttpResponseMessage**實例。

[!code-csharp[Main](action-results/samples/sample6.cs)]

如果控制器動作傳回**應傳回 iHTTPactionresult**，Web API 會呼叫**ExecuteAsync**方法來建立**HttpResponseMessage**。 然後，它會將**HttpResponseMessage**轉換為 HTTP 回應訊息。

以下是簡單的**應傳回 iHTTPactionresult**執行，可建立純文字回應：

[!code-csharp[Main](action-results/samples/sample7.cs)]

範例控制器動作：

[!code-csharp[Main](action-results/samples/sample8.cs)]

回應：

[!code-console[Main](action-results/samples/sample9.cmd)]

通常，您會使用在 **[system.web. HTTP.sys](https://msdn.microsoft.com/library/system.web.http.results.aspx)** 命名空間中定義的**應傳回 iHTTPactionresult**部署。 **ApiController**類別會定義可傳回這些內建動作結果的 helper 方法。

在下列範例中，如果要求不符合現有的產品識別碼，則控制器會呼叫[ApiController NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)以建立404（找不到）回應。 否則，控制器會呼叫[ApiController](https://msdn.microsoft.com/library/dn314591.aspx)，這會建立包含產品的200（確定）回應。

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>其他傳回類型

針對所有其他傳回類型，Web API 會使用[媒體格式](../formats-and-model-binding/media-formatters.md)器來序列化傳回值。 Web API 會將序列化的值寫入回應主體。 回應狀態碼為200（確定）。

[!code-csharp[Main](action-results/samples/sample11.cs)]

這種方法的缺點是您無法直接傳回錯誤碼，例如404。 不過，您可以擲回錯誤碼的**HttpResponseException** 。 如需詳細資訊，請參閱[ASP.NET Web API 中的例外狀況處理](../error-handling/exception-handling.md)。

Web API 會在要求中使用 Accept 標頭來選擇格式器。 如需詳細資訊，請參閱[內容協商](../formats-and-model-binding/content-negotiation.md)。

範例要求

[!code-console[Main](action-results/samples/sample12.cmd)]

範例回應

[!code-console[Main](action-results/samples/sample13.cmd)]
