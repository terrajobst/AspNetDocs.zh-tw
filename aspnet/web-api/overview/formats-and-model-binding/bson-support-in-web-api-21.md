---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1-ASP.NET 4.x 中的 BSON 支援
author: MikeWasson
description: 示範如何在 Web API 控制器（伺服器端）和適用于 ASP.NET 4.x 的 .NET 用戶端應用程式中使用 BSON。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622294"
---
# <a name="bson-support-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1 中的 BSON 支援

由[Mike Wasson](https://github.com/MikeWasson)

本主題說明如何在您的 Web API 控制器（伺服器端）和 .NET 用戶端應用程式中使用 BSON。 Web API 2.1 引進對 BSON 的支援。 

## <a name="what-is-bson"></a>什麼是 BSON？

[BSON](http://bsonspec.org/)是二進位序列化格式。 "BSON" 代表 "Binary JSON"，但是 BSON 和 JSON 的序列化方式非常不同。 BSON 是「類似 JSON」，因為物件是以名稱/值組表示，類似于 JSON。 不同于 JSON，數值資料類型會儲存為位元組，而不是字串

BSON 的設計是輕量、容易掃描，而且可以快速編碼/解碼。

- BSON 的大小相當於 JSON。 BSON 承載可能小於或大於 JSON 酬載，取決於資料。 針對序列化二進位資料（例如影像檔案），BSON 會小於 JSON，因為二進位資料不是以 base64 編碼。
- BSON 檔很容易掃描，因為元素前面會加上長度欄位，因此剖析器可以略過專案，而不將其解碼。
- 編碼和解碼很有效率，因為數值資料類型會儲存為數字，而不是字串。

原生用戶端（例如 .NET 用戶端應用程式）可使用 BSON 取代以文字為基礎的格式，例如 JSON 或 XML。 對於瀏覽器用戶端，您可能會想要使用 JSON，因為 JavaScript 可以直接轉換 JSON 承載。

幸運的是，Web API 會使用[內容協商](content-negotiation.md)，因此您的 api 可以同時支援這兩種格式，並讓用戶端選擇。

## <a name="enabling-bson-on-the-server"></a>在伺服器上啟用 BSON

在您的 Web API 設定中，將**BsonMediaTypeFormatter**新增至 [格式器] 集合。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

現在，如果用戶端要求 "application/bson"，Web API 會使用 BSON 格式器。

若要將 BSON 與其他媒體類型產生關聯，請將它們新增至 SupportedMediaTypes 集合。 下列程式碼會將 "application/application" 新增至支援的媒體類型：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>HTTP 會話範例

在此範例中，我們將使用下列模型類別，再加上簡單的 Web API 控制器：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

用戶端可能會傳送下列 HTTP 要求：

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

回應如下：

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

我在此將二進位資料取代為 &quot;。&quot; 個字元。 下列來自 Fiddler 的螢幕擷取畫面會顯示原始的十六進位值。

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>搭配使用 BSON 與 HttpClient

.NET 用戶端應用程式可以搭配**HttpClient**使用 BSON 格式器。 如需**HttpClient**的詳細資訊，請參閱[從 .Net 用戶端呼叫 Web API](../advanced/calling-a-web-api-from-a-net-client.md)。

下列程式碼會傳送接受 BSON 的 GET 要求，然後將回應中的 BSON 裝載還原序列化。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

若要從伺服器要求 BSON，請將 Accept 標頭設為 "application/BSON"：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

若要還原序列化回應主體，請使用**BsonMediaTypeFormatter**。 此格式器不在預設的格式器集合中，因此當您讀取回應本文時，必須指定它：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

下一個範例顯示如何傳送包含 BSON 的 POST 要求。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

這段程式碼大部分都與上一個範例相同。 但是在**PostAsync**方法中，將**BsonMediaTypeFormatter**指定為格式器：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>序列化最上層基本類型

每個 BSON 檔都是索引鍵/值組的清單。BSON 規格不會定義序列化單一原始值（例如整數或字串）的語法。

為了解決這項限制， **BsonMediaTypeFormatter**會將基本類型視為特殊案例。 在序列化之前，它會將值轉換成索引鍵/值組，並輸入 "Value"。 例如，假設您的 API 控制器傳回一個整數：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

在序列化之前，BSON 格式器會將此轉換成下列索引鍵/值組：

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

當您還原序列化時，格式器會將資料轉換回原始值。 不過，如果您的 Web API 會傳回原始值，則使用不同 BSON 剖析器的用戶端必須處理此情況。 一般來說，您應該考慮傳回結構化資料，而不是原始值。

## <a name="additional-resources"></a>其他資源

[Web API BSON 範例](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[媒體格式器](media-formatters.md)
