---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: 從.NET 用戶端呼叫 Web API (C#)-ASP.NET 4.x
author: MikeWasson
description: 本教學課程會示範如何從.NET 4.x 應用程式呼叫 web API。
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: ca3b9424f30f48c7b8c71b850ffeca64244b123b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112835"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="91fea-103">呼叫 Web API 的.NET 用戶端 (C#)</span><span class="sxs-lookup"><span data-stu-id="91fea-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="91fea-104">藉由[Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="91fea-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="91fea-105">[下載已完成的專案](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。</span><span class="sxs-lookup"><span data-stu-id="91fea-105">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="91fea-106">[下載指示](/aspnet/core/tutorials/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="91fea-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="91fea-107">本教學課程示範如何從.NET 應用程式呼叫 web API 使用[System.Net.Http.HttpClient。](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="91fea-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="91fea-108">在本教學課程中，用戶端應用程式會寫入，使用下列 web API:</span><span class="sxs-lookup"><span data-stu-id="91fea-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="91fea-109">動作</span><span class="sxs-lookup"><span data-stu-id="91fea-109">Action</span></span> | <span data-ttu-id="91fea-110">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="91fea-110">HTTP method</span></span> | <span data-ttu-id="91fea-111">相對 URI</span><span class="sxs-lookup"><span data-stu-id="91fea-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="91fea-112">取得產品識別碼</span><span class="sxs-lookup"><span data-stu-id="91fea-112">Get a product by ID</span></span> | <span data-ttu-id="91fea-113">GET</span><span class="sxs-lookup"><span data-stu-id="91fea-113">GET</span></span> | <span data-ttu-id="91fea-114">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="91fea-114">/api/products/*id*</span></span> |
| <span data-ttu-id="91fea-115">建立新的產品</span><span class="sxs-lookup"><span data-stu-id="91fea-115">Create a new product</span></span> | <span data-ttu-id="91fea-116">POST</span><span class="sxs-lookup"><span data-stu-id="91fea-116">POST</span></span> | <span data-ttu-id="91fea-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="91fea-117">/api/products</span></span> |
| <span data-ttu-id="91fea-118">將產品更新</span><span class="sxs-lookup"><span data-stu-id="91fea-118">Update a product</span></span> | <span data-ttu-id="91fea-119">PUT</span><span class="sxs-lookup"><span data-stu-id="91fea-119">PUT</span></span> | <span data-ttu-id="91fea-120">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="91fea-120">/api/products/*id*</span></span> |
| <span data-ttu-id="91fea-121">刪除產品</span><span class="sxs-lookup"><span data-stu-id="91fea-121">Delete a product</span></span> | <span data-ttu-id="91fea-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="91fea-122">DELETE</span></span> | <span data-ttu-id="91fea-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="91fea-123">/api/products/*id*</span></span> |

<span data-ttu-id="91fea-124">若要了解如何實作這個使用 ASP.NET Web API 的 API，請參閱[建立 Web API 的支援 CRUD 作業](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。</span><span class="sxs-lookup"><span data-stu-id="91fea-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="91fea-125">為了簡單起見，本教學課程中的用戶端應用程式是一個 Windows 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="91fea-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="91fea-126">**HttpClient**也支援 Windows Phone 和 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="91fea-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="91fea-127">如需詳細資訊，請參閱[撰寫 Web API 用戶端程式碼的多個平台使用可攜式程式庫](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="91fea-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="91fea-128">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="91fea-128">Create the Console Application</span></span>

<span data-ttu-id="91fea-129">在 Visual Studio 中建立名為的新 Windows 主控台應用程式**HttpClientSample**並貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="91fea-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="91fea-130">上述程式碼是完整的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="91fea-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="91fea-131">`RunAsync` 執行並封鎖，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="91fea-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="91fea-132">大部分**HttpClient**方法都是非同步，因為它們執行網路 I/O。</span><span class="sxs-lookup"><span data-stu-id="91fea-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="91fea-133">內的所有非同步工作完成`RunAsync`。</span><span class="sxs-lookup"><span data-stu-id="91fea-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="91fea-134">通常應用程式不會封鎖主執行緒，但此應用程式不允許任何互動。</span><span class="sxs-lookup"><span data-stu-id="91fea-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="91fea-135">安裝 Web API 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="91fea-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="91fea-136">使用 NuGet 套件管理員安裝的 Web API 用戶端程式庫封裝。</span><span class="sxs-lookup"><span data-stu-id="91fea-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="91fea-137">從 [工具] 功能表中，選取 [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="91fea-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="91fea-138">在 套件管理員主控台 (PMC)，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="91fea-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="91fea-139">上述命令會將下列 NuGet 封裝加入專案：</span><span class="sxs-lookup"><span data-stu-id="91fea-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="91fea-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="91fea-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="91fea-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="91fea-141">Newtonsoft.Json</span></span>

<span data-ttu-id="91fea-142">Json.NET 是受歡迎的高效能 JSON 架構適用於.NET。</span><span class="sxs-lookup"><span data-stu-id="91fea-142">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="91fea-143">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="91fea-143">Add a Model Class</span></span>

<span data-ttu-id="91fea-144">檢查 `Product` 類別：</span><span class="sxs-lookup"><span data-stu-id="91fea-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="91fea-145">此類別會比對 web API 所使用的資料模型。</span><span class="sxs-lookup"><span data-stu-id="91fea-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="91fea-146">應用程式可以使用**HttpClient**讀取`Product`之 HTTP 回應中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="91fea-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="91fea-147">應用程式不需要撰寫任何的還原序列化程式碼。</span><span class="sxs-lookup"><span data-stu-id="91fea-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="91fea-148">建立並初始化 HttpClient</span><span class="sxs-lookup"><span data-stu-id="91fea-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="91fea-149">檢查靜態**HttpClient**屬性：</span><span class="sxs-lookup"><span data-stu-id="91fea-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="91fea-150">**HttpClient**是用來具現化一次，並且重複使用的應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="91fea-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="91fea-151">在下列情況可能會導致**SocketException**錯誤：</span><span class="sxs-lookup"><span data-stu-id="91fea-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="91fea-152">建立新**HttpClient**每個要求的執行個體。</span><span class="sxs-lookup"><span data-stu-id="91fea-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="91fea-153">伺服器負載過重。</span><span class="sxs-lookup"><span data-stu-id="91fea-153">Server under heavy load.</span></span>

<span data-ttu-id="91fea-154">建立新**HttpClient**每個要求的執行個體可能會耗盡可用的通訊端。</span><span class="sxs-lookup"><span data-stu-id="91fea-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="91fea-155">下列程式碼會初始化**HttpClient**執行個體：</span><span class="sxs-lookup"><span data-stu-id="91fea-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="91fea-156">上述程式碼：</span><span class="sxs-lookup"><span data-stu-id="91fea-156">The preceding code:</span></span>

* <span data-ttu-id="91fea-157">設定 HTTP 要求的基底 URI。</span><span class="sxs-lookup"><span data-stu-id="91fea-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="91fea-158">將伺服器應用程式中使用的連接埠的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="91fea-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="91fea-159">應用程式將無法運作，除非會使用伺服器應用程式的連接埠。</span><span class="sxs-lookup"><span data-stu-id="91fea-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="91fea-160">設定為"application/json"的 Accept 標頭。</span><span class="sxs-lookup"><span data-stu-id="91fea-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="91fea-161">設定此標頭會要求伺服器傳送資料以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="91fea-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="91fea-162">傳送 GET 要求擷取資源</span><span class="sxs-lookup"><span data-stu-id="91fea-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="91fea-163">下列程式碼會傳送 GET 要求產品：</span><span class="sxs-lookup"><span data-stu-id="91fea-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="91fea-164">**GetAsync**方法會傳送 HTTP GET 要求。</span><span class="sxs-lookup"><span data-stu-id="91fea-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="91fea-165">方法完成時，它會傳回**HttpResponseMessage** ，其中包含 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="91fea-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="91fea-166">如果在回應中的狀態碼是成功的程式碼，回應主體會包含產品的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="91fea-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="91fea-167">呼叫**ReadAsAsync**還原序列化 JSON 承載，以`Product`執行個體。</span><span class="sxs-lookup"><span data-stu-id="91fea-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="91fea-168">**ReadAsAsync**方法是非同步的因為回應主體可以是任意大。</span><span class="sxs-lookup"><span data-stu-id="91fea-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="91fea-169">**HttpClient** HTTP 回應會包含錯誤程式碼時，不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="91fea-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="91fea-170">相反地， **IsSuccessStatusCode**屬性是**false**如果狀態為錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="91fea-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="91fea-171">如果您想要視為例外狀況的 HTTP 錯誤代碼，呼叫[HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx)回應物件上。</span><span class="sxs-lookup"><span data-stu-id="91fea-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="91fea-172">`EnsureSuccessStatusCode` 如果狀態碼超出範圍 200，則擲回例外狀況&ndash;299。</span><span class="sxs-lookup"><span data-stu-id="91fea-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="91fea-173">請注意， **HttpClient**可以擲回例外狀況，因為其他原因而&mdash;比方說，如果要求逾時。</span><span class="sxs-lookup"><span data-stu-id="91fea-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="91fea-174">若要還原序列化的媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="91fea-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="91fea-175">當**ReadAsAsync**呼叫使用任何參數，它會使用一組預設*媒體格式器*讀取回應主體。</span><span class="sxs-lookup"><span data-stu-id="91fea-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="91fea-176">預設格式器支援 JSON、 XML 和表單 url 編碼資料。</span><span class="sxs-lookup"><span data-stu-id="91fea-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="91fea-177">而不是使用預設格式器，您可以提供的格式器清單**ReadAsAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="91fea-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="91fea-178">使用格式器清單很有用，如果您有自訂的媒體類型格式器：</span><span class="sxs-lookup"><span data-stu-id="91fea-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="91fea-179">如需詳細資訊，請參閱[ASP.NET Web API 2 中的媒體格式器](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="91fea-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="91fea-180">傳送 POST 要求來建立資源</span><span class="sxs-lookup"><span data-stu-id="91fea-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="91fea-181">下列程式碼會傳送 POST 要求，其中包含`Product`以 JSON 格式的執行個體：</span><span class="sxs-lookup"><span data-stu-id="91fea-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="91fea-182">**PostAsJsonAsync**方法：</span><span class="sxs-lookup"><span data-stu-id="91fea-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="91fea-183">將物件序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="91fea-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="91fea-184">POST 要求中傳送的 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="91fea-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="91fea-185">如果要求成功：</span><span class="sxs-lookup"><span data-stu-id="91fea-185">If the request succeeds:</span></span>

* <span data-ttu-id="91fea-186">它應該傳回 201 （已建立） 回應。</span><span class="sxs-lookup"><span data-stu-id="91fea-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="91fea-187">回應應包含建立的資源 URL 中的 Location 標頭。</span><span class="sxs-lookup"><span data-stu-id="91fea-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="91fea-188">傳送 PUT 的要求來更新資源</span><span class="sxs-lookup"><span data-stu-id="91fea-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="91fea-189">下列程式碼會傳送 PUT 要求，將產品更新：</span><span class="sxs-lookup"><span data-stu-id="91fea-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="91fea-190">**PutAsJsonAsync**方法的運作方式類似**PostAsJsonAsync**，只不過它會傳送 PUT 要求，而不是 POST。</span><span class="sxs-lookup"><span data-stu-id="91fea-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="91fea-191">傳送 DELETE 要求來刪除資源</span><span class="sxs-lookup"><span data-stu-id="91fea-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="91fea-192">下列程式碼會傳送 DELETE 要求來刪除產品：</span><span class="sxs-lookup"><span data-stu-id="91fea-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="91fea-193">例如 GET、 DELETE 要求沒有要求主體。</span><span class="sxs-lookup"><span data-stu-id="91fea-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="91fea-194">您不需要與 DELETE 一起指定 JSON 或 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="91fea-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="91fea-195">測試範例</span><span class="sxs-lookup"><span data-stu-id="91fea-195">Test the sample</span></span>

<span data-ttu-id="91fea-196">若要測試用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="91fea-196">To test the client app:</span></span>

1. <span data-ttu-id="91fea-197">[下載](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)並執行伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="91fea-197">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="91fea-198">[下載指示](/aspnet/core/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="91fea-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="91fea-199">確認伺服器應用程式正常運作。</span><span class="sxs-lookup"><span data-stu-id="91fea-199">Verify the server app is working.</span></span> <span data-ttu-id="91fea-200">比方說，`http://localhost:64195/api/products`應該會傳回一份產品。</span><span class="sxs-lookup"><span data-stu-id="91fea-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="91fea-201">設定 HTTP 要求的基底 URI。</span><span class="sxs-lookup"><span data-stu-id="91fea-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="91fea-202">將伺服器應用程式中使用的連接埠的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="91fea-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="91fea-203">執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="91fea-203">Run the client app.</span></span> <span data-ttu-id="91fea-204">會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="91fea-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
