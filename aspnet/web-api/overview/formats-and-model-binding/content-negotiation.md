---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API 中的內容協商-ASP.NET 4。x
author: MikeWasson
description: 描述 ASP.NET Web API 如何執行 ASP.NET 4.x 的 HTTP 內容協商。
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622266"
---
# <a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API 中的內容協調

由[Mike Wasson](https://github.com/MikeWasson)

本文說明 ASP.NET Web API 如何執行 ASP.NET 4.x 的內容協調。

HTTP 規格（RFC 2616）會將內容協商定義為「當有多個標記法可供使用時，為指定回應選取最佳標記法的程式」。 在 HTTP 中，內容協商的主要機制是下列要求標頭：

- **接受：** 回應可接受哪些媒體類型，例如 "application/json"、"application/xml" 或自訂媒體類型，例如 &quot;application/application。範例 + xml&quot;
- **接受-字元集：** 哪些字元集可接受，例如 UTF-8 或 ISO 8859-1。
- **接受-編碼：** 可接受哪些內容編碼，例如 gzip。
- **Accept-語言：** 慣用的自然語言，例如 "en-us"。

伺服器也可以查看 HTTP 要求的其他部分。 例如，如果要求包含以 X 要求的標頭，表示 AJAX 要求，則如果沒有 Accept 標頭，伺服器可能會預設為 JSON。

在本文中，我們將探討 Web API 如何使用接受和接受字元集的標頭。 （目前並沒有內建的接受編碼或接受語言支援）。

## <a name="serialization"></a>序列化

如果 Web API 控制器將資源傳回為 CLR 類型，管線會序列化傳回值，並將它寫入 HTTP 回應主體。

例如，請考慮下列控制器動作：

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

用戶端可能會傳送此 HTTP 要求：

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

伺服器可能會傳送下列內容來回應：

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

在此範例中，用戶端要求的是 JSON、JAVAscript 或「任何」（\*/\*）。 伺服器會回應 `Product` 物件的 JSON 標記法。 請注意，回應中的 Content-type 標頭會設定為 &quot;application/json&quot;。

控制器也可以傳回**HttpResponseMessage**物件。 若要指定回應主體的 CLR 物件，請呼叫**CreateResponse**擴充方法：

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

此選項可讓您更充分掌控回應的詳細資料。 您可以設定狀態碼、新增 HTTP 標頭等等。

序列化資源的物件稱為「*媒體格式*器」。 媒體格式器衍生自**MediaTypeFormatter**類別。 Web API 提供適用于 XML 和 JSON 的媒體格式器，而您可以建立自訂格式器來支援其他媒體類型。 如需撰寫自訂格式器的詳細資訊，請參閱[媒體格式化](media-formatters.md)程式。

## <a name="how-content-negotiation-works"></a>內容協調的運作方式

首先，管線會從**HttpConfiguration**物件取得**IContentNegotiator**服務。 它也會從**HttpConfiguration**中取得媒體格式器的清單。

接下來，管線會呼叫**IContentNegotiator**，傳入：

- 要序列化之物件的類型
- 媒體格式器的集合
- HTTP 要求

**Negotiate**方法會傳回兩個資訊片段：

- 要使用的格式器
- 回應的媒體類型

如果找不到格式器，則**Negotiate**方法會傳回**null**，而且用戶端會收到 HTTP 錯誤406（無法接受）。

下列程式碼顯示控制器如何直接叫用內容協商：

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

此程式碼相當於管線自動執行的工作。

## <a name="default-content-negotiator"></a>預設內容 Negotiator

**DefaultContentNegotiator**類別提供**IContentNegotiator**的預設執行。 它會使用數個準則來選取格式器。

首先，格式器必須能夠序列化型別。 這會藉由呼叫 MediaTypeFormatter 來進行驗證 **。 CanWriteType**。

接下來，[內容 negotiator] 會查看每個格式器，並評估它與 HTTP 要求的相符程度。 為了評估相符專案，content negotiator 會在格式器上查看兩件事：

- **SupportedMediaTypes**集合，其中包含支援的媒體類型清單。 Content negotiator 會嘗試將此清單與要求 Accept 標頭比對。 請注意，Accept 標頭可以包含範圍。 例如，"text/純" 是 text/\* 或 \*/\*的相符項。
- **MediaTypeMappings**集合，其中包含**MediaTypeMapping**物件的清單。 **MediaTypeMapping**類別提供了一種一般方式，可將 HTTP 要求與媒體類型進行比對。 例如，它可以將自訂 HTTP 標頭對應至特定的媒體類型。

如果有多個相符專案，則會優先使用最高品質因數的相符專案。 例如:

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

在此範例中，application/json 具有隱含的品質因素1.0，因此偏好高於 application/xml。

如果找不到相符專案，則內容 negotiator 會嘗試比對要求主體的媒體類型（如果有的話）。 例如，如果要求包含 JSON 資料，內容 negotiator 就會尋找 JSON 格式器。

如果仍然沒有相符專案，內容 negotiator 只會挑選可序列化該類型的第一個格式器。

## <a name="selecting-a-character-encoding"></a>選取字元編碼

選取格式器之後，內容 negotiator 會藉由查看格式器上的**SupportedEncodings**屬性來選擇最佳的字元編碼，並比對要求中的接受字元集標頭（如果有的話）。
