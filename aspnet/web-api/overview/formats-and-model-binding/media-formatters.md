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
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="bc2b9-103">ASP.NET Web API 2 中的媒體格式器</span><span class="sxs-lookup"><span data-stu-id="bc2b9-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="bc2b9-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bc2b9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bc2b9-105">本教學課程說明如何在 ASP.NET Web API 中支援其他媒體格式。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="bc2b9-106">網際網路媒體類型</span><span class="sxs-lookup"><span data-stu-id="bc2b9-106">Internet Media Types</span></span>

<span data-ttu-id="bc2b9-107">媒體類型也稱為 MIME 類型，可識別資料片段的格式。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="bc2b9-108">在 HTTP 中，媒體類型描述訊息本文的格式。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="bc2b9-109">媒體類型包含兩個字串：類型和子類型。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="bc2b9-110">例如:</span><span class="sxs-lookup"><span data-stu-id="bc2b9-110">For example:</span></span>

- <span data-ttu-id="bc2b9-111">text/html</span><span class="sxs-lookup"><span data-stu-id="bc2b9-111">text/html</span></span>
- <span data-ttu-id="bc2b9-112">image/png</span><span class="sxs-lookup"><span data-stu-id="bc2b9-112">image/png</span></span>
- <span data-ttu-id="bc2b9-113">application/json</span><span class="sxs-lookup"><span data-stu-id="bc2b9-113">application/json</span></span>

<span data-ttu-id="bc2b9-114">當 HTTP 訊息包含實體主體時，Content-type 標頭會指定訊息主體的格式。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="bc2b9-115">這會告訴接收者如何剖析訊息本文的內容。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="bc2b9-116">例如，如果 HTTP 回應包含 PNG 影像，回應可能會有下列標頭。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="bc2b9-117">當用戶端傳送要求訊息時，它可以包含 Accept 標頭。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="bc2b9-118">Accept 標頭會告訴伺服器用戶端想要從伺服器哪種媒體類型。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="bc2b9-119">例如:</span><span class="sxs-lookup"><span data-stu-id="bc2b9-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="bc2b9-120">此標頭會告訴伺服器，用戶端想要 HTML、XHTML 或 XML。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="bc2b9-121">媒體類型決定 Web API 如何序列化和還原序列化 HTTP 訊息內文。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="bc2b9-122">Web API 具有 XML、JSON、BSON 和表單 urlencoded 資料的內建支援，而且您可以藉由撰寫*媒體格式*器來支援其他媒體類型。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="bc2b9-123">若要建立媒體格式器，請從下列其中一個類別衍生：</span><span class="sxs-lookup"><span data-stu-id="bc2b9-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="bc2b9-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="bc2b9-125">這個類別會使用非同步讀取和寫入方法。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="bc2b9-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="bc2b9-127">這個類別衍生自**MediaTypeFormatter** ，但使用同步的讀取/寫入方法。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="bc2b9-128">衍生自**BufferedMediaTypeFormatter**較簡單，因為沒有非同步程式碼，但也表示呼叫執行緒可以在 i/o 期間封鎖。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="bc2b9-129">範例：建立 CSV 媒體格式器</span><span class="sxs-lookup"><span data-stu-id="bc2b9-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="bc2b9-130">下列範例顯示的媒體類型格式器可將產品物件序列化為逗號分隔值（CSV）格式。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="bc2b9-131">這個範例會使用教學課程中定義的產品類型[，建立支援 CRUD 作業的 WEB API](../older-versions/creating-a-web-api-that-supports-crud-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="bc2b9-132">以下是 Product 物件的定義：</span><span class="sxs-lookup"><span data-stu-id="bc2b9-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="bc2b9-133">若要執行 CSV 格式器，請定義衍生自**BufferedMediaTypeFormatter**的類別：</span><span class="sxs-lookup"><span data-stu-id="bc2b9-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="bc2b9-134">在此函式中，新增格式器所支援的媒體類型。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="bc2b9-135">在此範例中，格式器支援單一媒體類型，&quot;text/csv&quot;：</span><span class="sxs-lookup"><span data-stu-id="bc2b9-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="bc2b9-136">覆寫**CanWriteType**方法，以指出格式器可以序列化的類型：</span><span class="sxs-lookup"><span data-stu-id="bc2b9-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="bc2b9-137">在此範例中，格式器可以序列化單一 `Product` 物件，以及 `Product` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="bc2b9-138">同樣地，覆寫**CanReadType**方法，以指出格式器可以還原序列化的類型。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="bc2b9-139">在此範例中，格式器不支援還原序列化，因此此方法只會傳回**false**。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="bc2b9-140">最後，覆寫**WriteToStream**方法。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="bc2b9-141">這個方法會將類型寫入資料流程，以將其序列化。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="bc2b9-142">如果您的格式器支援還原序列化，也會覆寫**ReadFromStream**方法。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="bc2b9-143">將媒體格式器新增至 Web API 管線</span><span class="sxs-lookup"><span data-stu-id="bc2b9-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="bc2b9-144">若要將媒體類型格式器新增至 Web API 管線，請使用**HttpConfiguration**物件上的 [**格式化**程式] 屬性。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="bc2b9-145">字元編碼</span><span class="sxs-lookup"><span data-stu-id="bc2b9-145">Character Encodings</span></span>

<span data-ttu-id="bc2b9-146">或者，媒體格式器可以支援多個字元編碼，例如 UTF-8 或 ISO 8859-1。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="bc2b9-147">在此函數中，將一或[多個](https://msdn.microsoft.com/library/system.text.encoding.aspx)system.string 類型新增至**SupportedEncodings**集合。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="bc2b9-148">先放置預設編碼。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="bc2b9-149">在**WriteToStream**和**ReadFromStream**方法中，呼叫[MediaTypeFormatter](https://msdn.microsoft.com/library/hh969054.aspx)來選取慣用的字元編碼方式。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="bc2b9-150">這個方法會比對要求標頭與支援的編碼清單。</span><span class="sxs-lookup"><span data-stu-id="bc2b9-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="bc2b9-151">當您從資料流程讀取或寫入時，請使用傳回的**編碼方式**：</span><span class="sxs-lookup"><span data-stu-id="bc2b9-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
