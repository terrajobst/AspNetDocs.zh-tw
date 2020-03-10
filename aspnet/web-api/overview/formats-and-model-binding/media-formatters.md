---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2-ASP.NET 4.x 中的媒體格式器
author: MikeWasson
description: 示範如何在 ASP.NET 4.x 的 ASP.NET Web API 中支援其他媒體格式。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557250"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的媒體格式器

由[Mike Wasson](https://github.com/MikeWasson)

本教學課程說明如何在 ASP.NET Web API 中支援其他媒體格式。

## <a name="internet-media-types"></a>網際網路媒體類型

媒體類型也稱為 MIME 類型，可識別資料片段的格式。 在 HTTP 中，媒體類型描述訊息本文的格式。 媒體類型包含兩個字串：類型和子類型。 例如:

- text/html
- image/png
- application/json

當 HTTP 訊息包含實體主體時，Content-type 標頭會指定訊息主體的格式。 這會告訴接收者如何剖析訊息本文的內容。

例如，如果 HTTP 回應包含 PNG 影像，回應可能會有下列標頭。

[!code-console[Main](media-formatters/samples/sample1.cmd)]

當用戶端傳送要求訊息時，它可以包含 Accept 標頭。 Accept 標頭會告訴伺服器用戶端想要從伺服器哪種媒體類型。 例如:

[!code-console[Main](media-formatters/samples/sample2.cmd)]

此標頭會告訴伺服器，用戶端想要 HTML、XHTML 或 XML。

媒體類型決定 Web API 如何序列化和還原序列化 HTTP 訊息內文。 Web API 具有 XML、JSON、BSON 和表單 urlencoded 資料的內建支援，而且您可以藉由撰寫*媒體格式*器來支援其他媒體類型。

若要建立媒體格式器，請從下列其中一個類別衍生：

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。 這個類別會使用非同步讀取和寫入方法。
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。 這個類別衍生自**MediaTypeFormatter** ，但使用同步的讀取/寫入方法。

衍生自**BufferedMediaTypeFormatter**較簡單，因為沒有非同步程式碼，但也表示呼叫執行緒可以在 i/o 期間封鎖。

## <a name="example-creating-a-csv-media-formatter"></a>範例：建立 CSV 媒體格式器

下列範例顯示的媒體類型格式器可將產品物件序列化為逗號分隔值（CSV）格式。 這個範例會使用教學課程中定義的產品類型[，建立支援 CRUD 作業的 WEB API](../older-versions/creating-a-web-api-that-supports-crud-operations.md)。 以下是 Product 物件的定義：

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

若要執行 CSV 格式器，請定義衍生自**BufferedMediaTypeFormatter**的類別：

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

在此函式中，新增格式器所支援的媒體類型。 在此範例中，格式器支援單一媒體類型，&quot;text/csv&quot;：

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

覆寫**CanWriteType**方法，以指出格式器可以序列化的類型：

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

在此範例中，格式器可以序列化單一 `Product` 物件，以及 `Product` 物件的集合。

同樣地，覆寫**CanReadType**方法，以指出格式器可以還原序列化的類型。 在此範例中，格式器不支援還原序列化，因此此方法只會傳回**false**。

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

最後，覆寫**WriteToStream**方法。 這個方法會將類型寫入資料流程，以將其序列化。 如果您的格式器支援還原序列化，也會覆寫**ReadFromStream**方法。

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>將媒體格式器新增至 Web API 管線

若要將媒體類型格式器新增至 Web API 管線，請使用**HttpConfiguration**物件上的 [**格式化**程式] 屬性。

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>字元編碼

或者，媒體格式器可以支援多個字元編碼，例如 UTF-8 或 ISO 8859-1。

在此函數中，將一或[多個](https://msdn.microsoft.com/library/system.text.encoding.aspx)system.string 類型新增至**SupportedEncodings**集合。 先放置預設編碼。

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

在**WriteToStream**和**ReadFromStream**方法中，呼叫[MediaTypeFormatter](https://msdn.microsoft.com/library/hh969054.aspx)來選取慣用的字元編碼方式。 這個方法會比對要求標頭與支援的編碼清單。 當您從資料流程讀取或寫入時，請使用傳回的**編碼方式**：

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
