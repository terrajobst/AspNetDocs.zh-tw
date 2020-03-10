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
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 中的 HttpClient 訊息處理常式

由[Mike Wasson](https://github.com/MikeWasson)

*訊息處理常式*是接收 HTTP 要求並傳回 HTTP 回應的類別。

通常會將一系列的訊息處理常式連結在一起。 第一個處理常式會接收 HTTP 要求、進行某些處理，並將要求提供給下一個處理常式。 在某個時間點，會建立回應，並備份鏈。 這個模式稱為*委派*處理常式。

![](httpclient-message-handlers/_static/image1.png)

在用戶端上， **HttpClient**類別會使用訊息處理常式來處理要求。 預設處理常式是**HttpClientHandler**，它會透過網路傳送要求，並從伺服器取得回應。 您可以將自訂訊息處理常式插入至用戶端管線：

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> ASP.NET Web API 也會使用伺服器端的訊息處理常式。 如需詳細資訊，請參閱[HTTP 訊息處理常式](http-message-handlers.md)。

## <a name="custom-message-handlers"></a>自訂訊息處理常式

若要撰寫自訂訊息處理常式，請從**DelegatingHandler**衍生，並覆寫**SendAsync**方法。 以下是方法簽章：

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

方法會採用**HttpRequestMessage**做為輸入，並以非同步方式傳回**HttpResponseMessage**。 一般的執行會執行下列動作：

1. 處理要求訊息。
2. 呼叫 `base.SendAsync` 以將要求傳送至內部處理常式。
3. 內部處理常式會傳迴響應消息。 （此步驟是非同步）。
4. 處理回應，並將它傳回給呼叫者。

下列範例顯示的訊息處理常式會將自訂標頭新增至傳出要求：

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

對 `base.SendAsync` 的呼叫是非同步的。 如果處理常式在此呼叫之後執行任何工作，請在方法完成後使用**await**關鍵字來繼續執行。 下列範例顯示記錄錯誤碼的處理常式。 記錄本身並不重要，但此範例會示範如何取得處理常式內的回應。

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>將訊息處理常式新增至用戶端管線

若要將自訂處理常式新增至**HttpClient**，請使用**HttpClientFactory. Create**方法：

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

訊息處理常式的呼叫順序如下：您將其傳遞至**Create**方法。 因為處理常式是嵌套的，回應訊息會以另一個方向移動。 也就是，最後一個處理常式是取得回應訊息的第一個。
