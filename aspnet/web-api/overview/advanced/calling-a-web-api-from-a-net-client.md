---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: 從 .NET 用戶端呼叫 Web API （C#）-ASP.NET 4。x
author: MikeWasson
description: 本教學課程說明如何從 .NET 4.x 應用程式呼叫 Web API。
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 960960d26863cc3f725eee8a6c98844c5d3ce721
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519176"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="b7289-103">從 .NET 用戶端呼叫 Web API （C#）</span><span class="sxs-lookup"><span data-stu-id="b7289-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="b7289-104">由[Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b7289-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b7289-105">[下載已完成的專案](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。</span><span class="sxs-lookup"><span data-stu-id="b7289-105">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="b7289-106">[下載指示](/aspnet/core/tutorials/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="b7289-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="b7289-107">本教學課程說明如何使用 HttpClient，從 .NET 應用程式呼叫 Web API [。](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="b7289-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="b7289-108">在本教學課程中，會寫入使用下列 Web API 的用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="b7289-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="b7289-109">動作</span><span class="sxs-lookup"><span data-stu-id="b7289-109">Action</span></span> | <span data-ttu-id="b7289-110">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="b7289-110">HTTP method</span></span> | <span data-ttu-id="b7289-111">相對 URI</span><span class="sxs-lookup"><span data-stu-id="b7289-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b7289-112">依識別碼取得產品</span><span class="sxs-lookup"><span data-stu-id="b7289-112">Get a product by ID</span></span> | <span data-ttu-id="b7289-113">GET</span><span class="sxs-lookup"><span data-stu-id="b7289-113">GET</span></span> | <span data-ttu-id="b7289-114">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="b7289-114">/api/products/*id*</span></span> |
| <span data-ttu-id="b7289-115">建立新的產品</span><span class="sxs-lookup"><span data-stu-id="b7289-115">Create a new product</span></span> | <span data-ttu-id="b7289-116">POST</span><span class="sxs-lookup"><span data-stu-id="b7289-116">POST</span></span> | <span data-ttu-id="b7289-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="b7289-117">/api/products</span></span> |
| <span data-ttu-id="b7289-118">更新產品</span><span class="sxs-lookup"><span data-stu-id="b7289-118">Update a product</span></span> | <span data-ttu-id="b7289-119">PUT</span><span class="sxs-lookup"><span data-stu-id="b7289-119">PUT</span></span> | <span data-ttu-id="b7289-120">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="b7289-120">/api/products/*id*</span></span> |
| <span data-ttu-id="b7289-121">刪除產品</span><span class="sxs-lookup"><span data-stu-id="b7289-121">Delete a product</span></span> | <span data-ttu-id="b7289-122">Delete</span><span class="sxs-lookup"><span data-stu-id="b7289-122">DELETE</span></span> | <span data-ttu-id="b7289-123">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="b7289-123">/api/products/*id*</span></span> |

<span data-ttu-id="b7289-124">若要瞭解如何使用 ASP.NET Web API 來執行此 API，請參閱[建立支援 CRUD 作業的 WEB api](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。</span><span class="sxs-lookup"><span data-stu-id="b7289-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="b7289-125">為了簡單起見，本教學課程中的用戶端應用程式是 Windows 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7289-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="b7289-126">Windows Phone 和 Windows Store 應用程式也支援**HttpClient** 。</span><span class="sxs-lookup"><span data-stu-id="b7289-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="b7289-127">如需詳細資訊，請參閱[使用便攜程式庫撰寫適用于多個平臺的 WEB API 用戶端程式代碼](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="b7289-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="b7289-128">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="b7289-128">Create the Console Application</span></span>

<span data-ttu-id="b7289-129">在 Visual Studio 中，建立名為**HttpClientSample**的新 Windows 主控台應用程式，並貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b7289-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="b7289-130">上述程式碼是完整的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7289-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="b7289-131">`RunAsync` 執行並封鎖，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="b7289-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="b7289-132">大部分的**HttpClient**方法都是非同步，因為它們會執行網路 i/o。</span><span class="sxs-lookup"><span data-stu-id="b7289-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="b7289-133">所有非同步工作都是在 `RunAsync`內完成。</span><span class="sxs-lookup"><span data-stu-id="b7289-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="b7289-134">應用程式通常不會封鎖主執行緒，但此應用程式不允許任何互動。</span><span class="sxs-lookup"><span data-stu-id="b7289-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="b7289-135">安裝 Web API 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="b7289-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="b7289-136">使用 NuGet 套件管理員來安裝 Web API 用戶端程式庫套件。</span><span class="sxs-lookup"><span data-stu-id="b7289-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="b7289-137">從 [工具] 功能表中，選取 [NuGet 套件管理員] >  [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="b7289-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b7289-138">在 [套件管理員主控台] （PMC）中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b7289-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="b7289-139">上述命令會將下列 NuGet 套件新增至專案：</span><span class="sxs-lookup"><span data-stu-id="b7289-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="b7289-140">WebApi。用戶端</span><span class="sxs-lookup"><span data-stu-id="b7289-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="b7289-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="b7289-141">Newtonsoft.Json</span></span>

<span data-ttu-id="b7289-142">Netwonsoft （也稱為 Json.NET）是適用于 .NET 的熱門高效能 JSON 架構。</span><span class="sxs-lookup"><span data-stu-id="b7289-142">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="b7289-143">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="b7289-143">Add a Model Class</span></span>

<span data-ttu-id="b7289-144">檢查 `Product` 類別：</span><span class="sxs-lookup"><span data-stu-id="b7289-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="b7289-145">這個類別符合 Web API 所使用的資料模型。</span><span class="sxs-lookup"><span data-stu-id="b7289-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="b7289-146">應用程式可以使用**HttpClient**從 HTTP 回應讀取 `Product` 實例。</span><span class="sxs-lookup"><span data-stu-id="b7289-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="b7289-147">應用程式不需要撰寫任何還原序列化程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7289-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="b7289-148">建立和初始化 HttpClient</span><span class="sxs-lookup"><span data-stu-id="b7289-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="b7289-149">檢查靜態**HttpClient**屬性：</span><span class="sxs-lookup"><span data-stu-id="b7289-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="b7289-150">**HttpClient**的目的是要具現化一次，並在應用程式的整個生命週期中重複使用。</span><span class="sxs-lookup"><span data-stu-id="b7289-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="b7289-151">下列情況可能會導致**SocketException**錯誤：</span><span class="sxs-lookup"><span data-stu-id="b7289-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="b7289-152">針對每個要求建立新的**HttpClient**實例。</span><span class="sxs-lookup"><span data-stu-id="b7289-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="b7289-153">負載過重的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b7289-153">Server under heavy load.</span></span>

<span data-ttu-id="b7289-154">針對每個要求建立新的**HttpClient**實例可能會耗盡可用的通訊端。</span><span class="sxs-lookup"><span data-stu-id="b7289-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="b7289-155">下列程式碼會初始化**HttpClient**實例：</span><span class="sxs-lookup"><span data-stu-id="b7289-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="b7289-156">上述程式碼：</span><span class="sxs-lookup"><span data-stu-id="b7289-156">The preceding code:</span></span>

* <span data-ttu-id="b7289-157">設定 HTTP 要求的基底 URI。</span><span class="sxs-lookup"><span data-stu-id="b7289-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="b7289-158">將埠號碼變更為伺服器應用程式中所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="b7289-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="b7289-159">除非使用伺服器應用程式的埠，否則應用程式將無法使用。</span><span class="sxs-lookup"><span data-stu-id="b7289-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="b7289-160">將 Accept 標頭設定為 "application/json"。</span><span class="sxs-lookup"><span data-stu-id="b7289-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="b7289-161">設定此標頭會告訴伺服器以 JSON 格式傳送資料。</span><span class="sxs-lookup"><span data-stu-id="b7289-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="b7289-162">傳送 GET 要求以取得資源</span><span class="sxs-lookup"><span data-stu-id="b7289-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="b7289-163">下列程式碼會傳送產品的 GET 要求：</span><span class="sxs-lookup"><span data-stu-id="b7289-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="b7289-164">**GetAsync**方法會傳送 HTTP GET 要求。</span><span class="sxs-lookup"><span data-stu-id="b7289-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="b7289-165">當方法完成時，它會傳回包含 HTTP 回應的**HttpResponseMessage** 。</span><span class="sxs-lookup"><span data-stu-id="b7289-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="b7289-166">如果回應中的狀態碼是成功的程式碼，回應主體會包含產品的 JSON 標記法。</span><span class="sxs-lookup"><span data-stu-id="b7289-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="b7289-167">呼叫**ReadAsAsync**將 JSON 承載還原序列化為 `Product` 實例。</span><span class="sxs-lookup"><span data-stu-id="b7289-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="b7289-168">**ReadAsAsync**方法是非同步，因為回應主體可以任意大。</span><span class="sxs-lookup"><span data-stu-id="b7289-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="b7289-169">當 HTTP 回應包含錯誤代碼時， **HttpClient**不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7289-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="b7289-170">相反地，如果狀態為錯誤碼，則 **.issuccessstatuscode**屬性為**false** 。</span><span class="sxs-lookup"><span data-stu-id="b7289-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="b7289-171">如果您想要將 HTTP 錯誤碼視為例外狀況，請在回應物件上呼叫[HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="b7289-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="b7289-172">如果狀態碼落在 200&ndash;299 的範圍外，`EnsureSuccessStatusCode` 會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7289-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="b7289-173">請注意， **HttpClient**可能會因其他原因而擲回例外狀況 &mdash; 例如，如果要求超時。</span><span class="sxs-lookup"><span data-stu-id="b7289-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="b7289-174">要還原序列化的媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="b7289-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="b7289-175">呼叫不含任何參數的**ReadAsAsync**時，會使用一組預設的*媒體*格式器來讀取回應主體。</span><span class="sxs-lookup"><span data-stu-id="b7289-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="b7289-176">預設的格式器支援 JSON、XML 和表單 url 編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="b7289-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="b7289-177">除了使用預設的格式器之外，您還可以提供格式器清單給**ReadAsAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="b7289-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="b7289-178">如果您有自訂的媒體類型格式器，使用格式器清單會很有用：</span><span class="sxs-lookup"><span data-stu-id="b7289-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="b7289-179">如需詳細資訊，請參閱[ASP.NET Web API 2 中的媒體](../formats-and-model-binding/media-formatters.md)格式器</span><span class="sxs-lookup"><span data-stu-id="b7289-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="b7289-180">傳送 POST 要求以建立資源</span><span class="sxs-lookup"><span data-stu-id="b7289-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="b7289-181">下列程式碼會傳送 POST 要求，其中包含 JSON 格式的 `Product` 實例：</span><span class="sxs-lookup"><span data-stu-id="b7289-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="b7289-182">**PostAsJsonAsync**方法：</span><span class="sxs-lookup"><span data-stu-id="b7289-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="b7289-183">將物件序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="b7289-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="b7289-184">在 POST 要求中傳送 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="b7289-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="b7289-185">如果要求成功：</span><span class="sxs-lookup"><span data-stu-id="b7289-185">If the request succeeds:</span></span>

* <span data-ttu-id="b7289-186">它應該會傳回201（已建立）的回應。</span><span class="sxs-lookup"><span data-stu-id="b7289-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="b7289-187">回應應包含位置標頭中所建立資源的 URL。</span><span class="sxs-lookup"><span data-stu-id="b7289-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="b7289-188">傳送 PUT 要求以更新資源</span><span class="sxs-lookup"><span data-stu-id="b7289-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="b7289-189">下列程式碼會傳送 PUT 要求來更新產品：</span><span class="sxs-lookup"><span data-stu-id="b7289-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="b7289-190">**PutAsJsonAsync**方法的運作方式類似**PostAsJsonAsync**，不同之處在于它會傳送 PUT 要求，而不是 POST。</span><span class="sxs-lookup"><span data-stu-id="b7289-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="b7289-191">傳送刪除要求以刪除資源</span><span class="sxs-lookup"><span data-stu-id="b7289-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="b7289-192">下列程式碼會傳送刪除要求以刪除產品：</span><span class="sxs-lookup"><span data-stu-id="b7289-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="b7289-193">就像 GET 一樣，刪除要求沒有要求主體。</span><span class="sxs-lookup"><span data-stu-id="b7289-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="b7289-194">您不需要使用 DELETE 來指定 JSON 或 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="b7289-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="b7289-195">測試範例</span><span class="sxs-lookup"><span data-stu-id="b7289-195">Test the sample</span></span>

<span data-ttu-id="b7289-196">若要測試用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="b7289-196">To test the client app:</span></span>

1. <span data-ttu-id="b7289-197">[下載](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)並執行伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7289-197">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="b7289-198">[下載指示](/aspnet/core/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="b7289-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="b7289-199">確認伺服器應用程式正在運作。</span><span class="sxs-lookup"><span data-stu-id="b7289-199">Verify the server app is working.</span></span> <span data-ttu-id="b7289-200">例如，`http://localhost:64195/api/products` 應該會傳回一份產品清單。</span><span class="sxs-lookup"><span data-stu-id="b7289-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="b7289-201">設定 HTTP 要求的基底 URI。</span><span class="sxs-lookup"><span data-stu-id="b7289-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="b7289-202">將埠號碼變更為伺服器應用程式中所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="b7289-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="b7289-203">執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7289-203">Run the client app.</span></span> <span data-ttu-id="b7289-204">會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="b7289-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
