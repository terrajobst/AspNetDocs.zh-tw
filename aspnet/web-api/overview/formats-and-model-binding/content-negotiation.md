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
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="034ce-103">ASP.NET Web API 中的內容協調</span><span class="sxs-lookup"><span data-stu-id="034ce-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="034ce-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="034ce-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="034ce-105">本文說明 ASP.NET Web API 如何執行 ASP.NET 4.x 的內容協調。</span><span class="sxs-lookup"><span data-stu-id="034ce-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="034ce-106">HTTP 規格（RFC 2616）會將內容協商定義為「當有多個標記法可供使用時，為指定回應選取最佳標記法的程式」。</span><span class="sxs-lookup"><span data-stu-id="034ce-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="034ce-107">在 HTTP 中，內容協商的主要機制是下列要求標頭：</span><span class="sxs-lookup"><span data-stu-id="034ce-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="034ce-108">**接受：** 回應可接受哪些媒體類型，例如 "application/json"、"application/xml" 或自訂媒體類型，例如 &quot;application/application。範例 + xml&quot;</span><span class="sxs-lookup"><span data-stu-id="034ce-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="034ce-109">**接受-字元集：** 哪些字元集可接受，例如 UTF-8 或 ISO 8859-1。</span><span class="sxs-lookup"><span data-stu-id="034ce-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="034ce-110">**接受-編碼：** 可接受哪些內容編碼，例如 gzip。</span><span class="sxs-lookup"><span data-stu-id="034ce-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="034ce-111">**Accept-語言：** 慣用的自然語言，例如 "en-us"。</span><span class="sxs-lookup"><span data-stu-id="034ce-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="034ce-112">伺服器也可以查看 HTTP 要求的其他部分。</span><span class="sxs-lookup"><span data-stu-id="034ce-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="034ce-113">例如，如果要求包含以 X 要求的標頭，表示 AJAX 要求，則如果沒有 Accept 標頭，伺服器可能會預設為 JSON。</span><span class="sxs-lookup"><span data-stu-id="034ce-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="034ce-114">在本文中，我們將探討 Web API 如何使用接受和接受字元集的標頭。</span><span class="sxs-lookup"><span data-stu-id="034ce-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="034ce-115">（目前並沒有內建的接受編碼或接受語言支援）。</span><span class="sxs-lookup"><span data-stu-id="034ce-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="034ce-116">序列化</span><span class="sxs-lookup"><span data-stu-id="034ce-116">Serialization</span></span>

<span data-ttu-id="034ce-117">如果 Web API 控制器將資源傳回為 CLR 類型，管線會序列化傳回值，並將它寫入 HTTP 回應主體。</span><span class="sxs-lookup"><span data-stu-id="034ce-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="034ce-118">例如，請考慮下列控制器動作：</span><span class="sxs-lookup"><span data-stu-id="034ce-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="034ce-119">用戶端可能會傳送此 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="034ce-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="034ce-120">伺服器可能會傳送下列內容來回應：</span><span class="sxs-lookup"><span data-stu-id="034ce-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="034ce-121">在此範例中，用戶端要求的是 JSON、JAVAscript 或「任何」（\*/\*）。</span><span class="sxs-lookup"><span data-stu-id="034ce-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="034ce-122">伺服器會回應 `Product` 物件的 JSON 標記法。</span><span class="sxs-lookup"><span data-stu-id="034ce-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="034ce-123">請注意，回應中的 Content-type 標頭會設定為 &quot;application/json&quot;。</span><span class="sxs-lookup"><span data-stu-id="034ce-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="034ce-124">控制器也可以傳回**HttpResponseMessage**物件。</span><span class="sxs-lookup"><span data-stu-id="034ce-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="034ce-125">若要指定回應主體的 CLR 物件，請呼叫**CreateResponse**擴充方法：</span><span class="sxs-lookup"><span data-stu-id="034ce-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="034ce-126">此選項可讓您更充分掌控回應的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="034ce-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="034ce-127">您可以設定狀態碼、新增 HTTP 標頭等等。</span><span class="sxs-lookup"><span data-stu-id="034ce-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="034ce-128">序列化資源的物件稱為「*媒體格式*器」。</span><span class="sxs-lookup"><span data-stu-id="034ce-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="034ce-129">媒體格式器衍生自**MediaTypeFormatter**類別。</span><span class="sxs-lookup"><span data-stu-id="034ce-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="034ce-130">Web API 提供適用于 XML 和 JSON 的媒體格式器，而您可以建立自訂格式器來支援其他媒體類型。</span><span class="sxs-lookup"><span data-stu-id="034ce-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="034ce-131">如需撰寫自訂格式器的詳細資訊，請參閱[媒體格式化](media-formatters.md)程式。</span><span class="sxs-lookup"><span data-stu-id="034ce-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="034ce-132">內容協調的運作方式</span><span class="sxs-lookup"><span data-stu-id="034ce-132">How Content Negotiation Works</span></span>

<span data-ttu-id="034ce-133">首先，管線會從**HttpConfiguration**物件取得**IContentNegotiator**服務。</span><span class="sxs-lookup"><span data-stu-id="034ce-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="034ce-134">它也會從**HttpConfiguration**中取得媒體格式器的清單。</span><span class="sxs-lookup"><span data-stu-id="034ce-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="034ce-135">接下來，管線會呼叫**IContentNegotiator**，傳入：</span><span class="sxs-lookup"><span data-stu-id="034ce-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="034ce-136">要序列化之物件的類型</span><span class="sxs-lookup"><span data-stu-id="034ce-136">The type of object to serialize</span></span>
- <span data-ttu-id="034ce-137">媒體格式器的集合</span><span class="sxs-lookup"><span data-stu-id="034ce-137">The collection of media formatters</span></span>
- <span data-ttu-id="034ce-138">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="034ce-138">The HTTP request</span></span>

<span data-ttu-id="034ce-139">**Negotiate**方法會傳回兩個資訊片段：</span><span class="sxs-lookup"><span data-stu-id="034ce-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="034ce-140">要使用的格式器</span><span class="sxs-lookup"><span data-stu-id="034ce-140">Which formatter to use</span></span>
- <span data-ttu-id="034ce-141">回應的媒體類型</span><span class="sxs-lookup"><span data-stu-id="034ce-141">The media type for the response</span></span>

<span data-ttu-id="034ce-142">如果找不到格式器，則**Negotiate**方法會傳回**null**，而且用戶端會收到 HTTP 錯誤406（無法接受）。</span><span class="sxs-lookup"><span data-stu-id="034ce-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="034ce-143">下列程式碼顯示控制器如何直接叫用內容協商：</span><span class="sxs-lookup"><span data-stu-id="034ce-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="034ce-144">此程式碼相當於管線自動執行的工作。</span><span class="sxs-lookup"><span data-stu-id="034ce-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="034ce-145">預設內容 Negotiator</span><span class="sxs-lookup"><span data-stu-id="034ce-145">Default Content Negotiator</span></span>

<span data-ttu-id="034ce-146">**DefaultContentNegotiator**類別提供**IContentNegotiator**的預設執行。</span><span class="sxs-lookup"><span data-stu-id="034ce-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="034ce-147">它會使用數個準則來選取格式器。</span><span class="sxs-lookup"><span data-stu-id="034ce-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="034ce-148">首先，格式器必須能夠序列化型別。</span><span class="sxs-lookup"><span data-stu-id="034ce-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="034ce-149">這會藉由呼叫 MediaTypeFormatter 來進行驗證 **。 CanWriteType**。</span><span class="sxs-lookup"><span data-stu-id="034ce-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="034ce-150">接下來，[內容 negotiator] 會查看每個格式器，並評估它與 HTTP 要求的相符程度。</span><span class="sxs-lookup"><span data-stu-id="034ce-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="034ce-151">為了評估相符專案，content negotiator 會在格式器上查看兩件事：</span><span class="sxs-lookup"><span data-stu-id="034ce-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="034ce-152">**SupportedMediaTypes**集合，其中包含支援的媒體類型清單。</span><span class="sxs-lookup"><span data-stu-id="034ce-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="034ce-153">Content negotiator 會嘗試將此清單與要求 Accept 標頭比對。</span><span class="sxs-lookup"><span data-stu-id="034ce-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="034ce-154">請注意，Accept 標頭可以包含範圍。</span><span class="sxs-lookup"><span data-stu-id="034ce-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="034ce-155">例如，"text/純" 是 text/\* 或 \*/\*的相符項。</span><span class="sxs-lookup"><span data-stu-id="034ce-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="034ce-156">**MediaTypeMappings**集合，其中包含**MediaTypeMapping**物件的清單。</span><span class="sxs-lookup"><span data-stu-id="034ce-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="034ce-157">**MediaTypeMapping**類別提供了一種一般方式，可將 HTTP 要求與媒體類型進行比對。</span><span class="sxs-lookup"><span data-stu-id="034ce-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="034ce-158">例如，它可以將自訂 HTTP 標頭對應至特定的媒體類型。</span><span class="sxs-lookup"><span data-stu-id="034ce-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="034ce-159">如果有多個相符專案，則會優先使用最高品質因數的相符專案。</span><span class="sxs-lookup"><span data-stu-id="034ce-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="034ce-160">例如:</span><span class="sxs-lookup"><span data-stu-id="034ce-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="034ce-161">在此範例中，application/json 具有隱含的品質因素1.0，因此偏好高於 application/xml。</span><span class="sxs-lookup"><span data-stu-id="034ce-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="034ce-162">如果找不到相符專案，則內容 negotiator 會嘗試比對要求主體的媒體類型（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="034ce-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="034ce-163">例如，如果要求包含 JSON 資料，內容 negotiator 就會尋找 JSON 格式器。</span><span class="sxs-lookup"><span data-stu-id="034ce-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="034ce-164">如果仍然沒有相符專案，內容 negotiator 只會挑選可序列化該類型的第一個格式器。</span><span class="sxs-lookup"><span data-stu-id="034ce-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="034ce-165">選取字元編碼</span><span class="sxs-lookup"><span data-stu-id="034ce-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="034ce-166">選取格式器之後，內容 negotiator 會藉由查看格式器上的**SupportedEncodings**屬性來選擇最佳的字元編碼，並比對要求中的接受字元集標頭（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="034ce-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
