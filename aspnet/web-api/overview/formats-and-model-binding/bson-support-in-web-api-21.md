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
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="b97e9-103">ASP.NET Web API 2.1 中的 BSON 支援</span><span class="sxs-lookup"><span data-stu-id="b97e9-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="b97e9-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b97e9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b97e9-105">本主題說明如何在您的 Web API 控制器（伺服器端）和 .NET 用戶端應用程式中使用 BSON。</span><span class="sxs-lookup"><span data-stu-id="b97e9-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="b97e9-106">Web API 2.1 引進對 BSON 的支援。</span><span class="sxs-lookup"><span data-stu-id="b97e9-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="b97e9-107">什麼是 BSON？</span><span class="sxs-lookup"><span data-stu-id="b97e9-107">What is BSON?</span></span>

<span data-ttu-id="b97e9-108">[BSON](http://bsonspec.org/)是二進位序列化格式。</span><span class="sxs-lookup"><span data-stu-id="b97e9-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="b97e9-109">"BSON" 代表 "Binary JSON"，但是 BSON 和 JSON 的序列化方式非常不同。</span><span class="sxs-lookup"><span data-stu-id="b97e9-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="b97e9-110">BSON 是「類似 JSON」，因為物件是以名稱/值組表示，類似于 JSON。</span><span class="sxs-lookup"><span data-stu-id="b97e9-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="b97e9-111">不同于 JSON，數值資料類型會儲存為位元組，而不是字串</span><span class="sxs-lookup"><span data-stu-id="b97e9-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="b97e9-112">BSON 的設計是輕量、容易掃描，而且可以快速編碼/解碼。</span><span class="sxs-lookup"><span data-stu-id="b97e9-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="b97e9-113">BSON 的大小相當於 JSON。</span><span class="sxs-lookup"><span data-stu-id="b97e9-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="b97e9-114">BSON 承載可能小於或大於 JSON 酬載，取決於資料。</span><span class="sxs-lookup"><span data-stu-id="b97e9-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="b97e9-115">針對序列化二進位資料（例如影像檔案），BSON 會小於 JSON，因為二進位資料不是以 base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="b97e9-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="b97e9-116">BSON 檔很容易掃描，因為元素前面會加上長度欄位，因此剖析器可以略過專案，而不將其解碼。</span><span class="sxs-lookup"><span data-stu-id="b97e9-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="b97e9-117">編碼和解碼很有效率，因為數值資料類型會儲存為數字，而不是字串。</span><span class="sxs-lookup"><span data-stu-id="b97e9-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="b97e9-118">原生用戶端（例如 .NET 用戶端應用程式）可使用 BSON 取代以文字為基礎的格式，例如 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="b97e9-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="b97e9-119">對於瀏覽器用戶端，您可能會想要使用 JSON，因為 JavaScript 可以直接轉換 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="b97e9-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="b97e9-120">幸運的是，Web API 會使用[內容協商](content-negotiation.md)，因此您的 api 可以同時支援這兩種格式，並讓用戶端選擇。</span><span class="sxs-lookup"><span data-stu-id="b97e9-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="b97e9-121">在伺服器上啟用 BSON</span><span class="sxs-lookup"><span data-stu-id="b97e9-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="b97e9-122">在您的 Web API 設定中，將**BsonMediaTypeFormatter**新增至 [格式器] 集合。</span><span class="sxs-lookup"><span data-stu-id="b97e9-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="b97e9-123">現在，如果用戶端要求 "application/bson"，Web API 會使用 BSON 格式器。</span><span class="sxs-lookup"><span data-stu-id="b97e9-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="b97e9-124">若要將 BSON 與其他媒體類型產生關聯，請將它們新增至 SupportedMediaTypes 集合。</span><span class="sxs-lookup"><span data-stu-id="b97e9-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="b97e9-125">下列程式碼會將 "application/application" 新增至支援的媒體類型：</span><span class="sxs-lookup"><span data-stu-id="b97e9-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="b97e9-126">HTTP 會話範例</span><span class="sxs-lookup"><span data-stu-id="b97e9-126">Example HTTP Session</span></span>

<span data-ttu-id="b97e9-127">在此範例中，我們將使用下列模型類別，再加上簡單的 Web API 控制器：</span><span class="sxs-lookup"><span data-stu-id="b97e9-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="b97e9-128">用戶端可能會傳送下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="b97e9-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="b97e9-129">回應如下：</span><span class="sxs-lookup"><span data-stu-id="b97e9-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="b97e9-130">我在此將二進位資料取代為 &quot;。&quot; 個字元。</span><span class="sxs-lookup"><span data-stu-id="b97e9-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="b97e9-131">下列來自 Fiddler 的螢幕擷取畫面會顯示原始的十六進位值。</span><span class="sxs-lookup"><span data-stu-id="b97e9-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="b97e9-132">搭配使用 BSON 與 HttpClient</span><span class="sxs-lookup"><span data-stu-id="b97e9-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="b97e9-133">.NET 用戶端應用程式可以搭配**HttpClient**使用 BSON 格式器。</span><span class="sxs-lookup"><span data-stu-id="b97e9-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="b97e9-134">如需**HttpClient**的詳細資訊，請參閱[從 .Net 用戶端呼叫 Web API](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="b97e9-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="b97e9-135">下列程式碼會傳送接受 BSON 的 GET 要求，然後將回應中的 BSON 裝載還原序列化。</span><span class="sxs-lookup"><span data-stu-id="b97e9-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="b97e9-136">若要從伺服器要求 BSON，請將 Accept 標頭設為 "application/BSON"：</span><span class="sxs-lookup"><span data-stu-id="b97e9-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="b97e9-137">若要還原序列化回應主體，請使用**BsonMediaTypeFormatter**。</span><span class="sxs-lookup"><span data-stu-id="b97e9-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="b97e9-138">此格式器不在預設的格式器集合中，因此當您讀取回應本文時，必須指定它：</span><span class="sxs-lookup"><span data-stu-id="b97e9-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="b97e9-139">下一個範例顯示如何傳送包含 BSON 的 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="b97e9-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="b97e9-140">這段程式碼大部分都與上一個範例相同。</span><span class="sxs-lookup"><span data-stu-id="b97e9-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="b97e9-141">但是在**PostAsync**方法中，將**BsonMediaTypeFormatter**指定為格式器：</span><span class="sxs-lookup"><span data-stu-id="b97e9-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="b97e9-142">序列化最上層基本類型</span><span class="sxs-lookup"><span data-stu-id="b97e9-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="b97e9-143">每個 BSON 檔都是索引鍵/值組的清單。BSON 規格不會定義序列化單一原始值（例如整數或字串）的語法。</span><span class="sxs-lookup"><span data-stu-id="b97e9-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="b97e9-144">為了解決這項限制， **BsonMediaTypeFormatter**會將基本類型視為特殊案例。</span><span class="sxs-lookup"><span data-stu-id="b97e9-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="b97e9-145">在序列化之前，它會將值轉換成索引鍵/值組，並輸入 "Value"。</span><span class="sxs-lookup"><span data-stu-id="b97e9-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="b97e9-146">例如，假設您的 API 控制器傳回一個整數：</span><span class="sxs-lookup"><span data-stu-id="b97e9-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="b97e9-147">在序列化之前，BSON 格式器會將此轉換成下列索引鍵/值組：</span><span class="sxs-lookup"><span data-stu-id="b97e9-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="b97e9-148">當您還原序列化時，格式器會將資料轉換回原始值。</span><span class="sxs-lookup"><span data-stu-id="b97e9-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="b97e9-149">不過，如果您的 Web API 會傳回原始值，則使用不同 BSON 剖析器的用戶端必須處理此情況。</span><span class="sxs-lookup"><span data-stu-id="b97e9-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="b97e9-150">一般來說，您應該考慮傳回結構化資料，而不是原始值。</span><span class="sxs-lookup"><span data-stu-id="b97e9-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b97e9-151">其他資源</span><span class="sxs-lookup"><span data-stu-id="b97e9-151">Additional Resources</span></span>

[<span data-ttu-id="b97e9-152">Web API BSON 範例</span><span class="sxs-lookup"><span data-stu-id="b97e9-152">Web API BSON Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[<span data-ttu-id="b97e9-153">媒體格式器</span><span class="sxs-lookup"><span data-stu-id="b97e9-153">Media Formatters</span></span>](media-formatters.md)
