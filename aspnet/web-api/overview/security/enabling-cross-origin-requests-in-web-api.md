---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: 在 ASP.NET Web API 2 中啟用跨原始來源要求 |Microsoft Docs
author: MikeWasson
description: 說明如何支援 ASP.NET Web API 中的跨原始來源資源分享（CORS）。
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555703"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="6e28a-103">在 ASP.NET Web API 2 中啟用跨原始來源要求</span><span class="sxs-lookup"><span data-stu-id="6e28a-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="6e28a-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6e28a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="6e28a-105">瀏覽器安全性可防止網頁對另一個網域提出 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="6e28a-106">這種限制稱為「*相同來源原則*」，可防止惡意網站從另一個網站讀取敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="6e28a-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="6e28a-107">不過，有時候您可能會想要讓其他網站呼叫您的 Web API。</span><span class="sxs-lookup"><span data-stu-id="6e28a-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="6e28a-108">[跨原始來源資源分享](http://www.w3.org/TR/cors/)（CORS）是 W3C 標準，可讓伺服器放寬相同的來源原則。</span><span class="sxs-lookup"><span data-stu-id="6e28a-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="6e28a-109">使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="6e28a-110">CORS 比先前的技術（例如[JSONP](http://en.wikipedia.org/wiki/JSONP)）更安全且更具彈性。</span><span class="sxs-lookup"><span data-stu-id="6e28a-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="6e28a-111">本教學課程說明如何在您的 Web API 應用程式中啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="6e28a-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="6e28a-112">教學課程中使用的軟體</span><span class="sxs-lookup"><span data-stu-id="6e28a-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="6e28a-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e28a-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="6e28a-114">Web API 2。2</span><span class="sxs-lookup"><span data-stu-id="6e28a-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="6e28a-115">簡介</span><span class="sxs-lookup"><span data-stu-id="6e28a-115">Introduction</span></span>

<span data-ttu-id="6e28a-116">本教學課程示範 ASP.NET Web API 中的 CORS 支援。</span><span class="sxs-lookup"><span data-stu-id="6e28a-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="6e28a-117">我們一開始會建立兩個 ASP.NET 專案，稱為「WebService」，其中裝載 Web API 控制器，另一個稱為「WebClient」，這會呼叫 WebService。</span><span class="sxs-lookup"><span data-stu-id="6e28a-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="6e28a-118">因為這兩個應用程式裝載于不同的網域，所以從 WebClient 到 WebService 的 AJAX 要求是一個跨原始來源要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="6e28a-119">什麼是「相同的來源」？</span><span class="sxs-lookup"><span data-stu-id="6e28a-119">What is "same origin"?</span></span>

<span data-ttu-id="6e28a-120">如果兩個 Url 具有相同的配置、主機和埠，則具有相同的來源。</span><span class="sxs-lookup"><span data-stu-id="6e28a-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="6e28a-121">（[RFC 6454](http://tools.ietf.org/html/rfc6454)）</span><span class="sxs-lookup"><span data-stu-id="6e28a-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="6e28a-122">這兩個 Url 具有相同的來源：</span><span class="sxs-lookup"><span data-stu-id="6e28a-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="6e28a-123">這些 Url 的來源不同于前兩個：</span><span class="sxs-lookup"><span data-stu-id="6e28a-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="6e28a-124">`http://example.net`-不同的網域</span><span class="sxs-lookup"><span data-stu-id="6e28a-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="6e28a-125">`http://example.com:9000/foo.html`-不同的埠</span><span class="sxs-lookup"><span data-stu-id="6e28a-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="6e28a-126">`https://example.com/foo.html`-不同的配置</span><span class="sxs-lookup"><span data-stu-id="6e28a-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="6e28a-127">`http://www.example.com/foo.html`-不同的子域</span><span class="sxs-lookup"><span data-stu-id="6e28a-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="6e28a-128">在比較原始來源時，Internet Explorer 不會考慮此埠。</span><span class="sxs-lookup"><span data-stu-id="6e28a-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="6e28a-129">建立 WebService 專案</span><span class="sxs-lookup"><span data-stu-id="6e28a-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="6e28a-130">本節假設您已經知道如何建立 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="6e28a-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="6e28a-131">如果沒有，請參閱[使用 ASP.NET Web API 消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="6e28a-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="6e28a-132">啟動 Visual Studio，並建立新的**ASP.NET Web 應用程式（.NET Framework）** 專案。</span><span class="sxs-lookup"><span data-stu-id="6e28a-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="6e28a-133">在 [**新增 ASP.NET Web 應用程式**] 對話方塊中，選取 [**空白**專案] 範本。</span><span class="sxs-lookup"><span data-stu-id="6e28a-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="6e28a-134">在 [**新增資料夾和核心參考**] 底下，選取 [ **Web API** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6e28a-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Visual Studio 中的 [新增 ASP.NET 專案] 對話方塊](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="6e28a-136">使用下列程式碼，新增名為 `TestController` 的 Web API 控制器：</span><span class="sxs-lookup"><span data-stu-id="6e28a-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="6e28a-137">您可以在本機執行應用程式，或部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6e28a-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="6e28a-138">（針對本教學課程中的螢幕擷取畫面，應用程式會部署至 Azure App Service Web Apps）。若要確認 Web API 是否正常運作，請流覽至 `http://hostname/api/test/`，其中*hostname*是您部署應用程式的網域。</span><span class="sxs-lookup"><span data-stu-id="6e28a-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="6e28a-139">您應該會看到回應文字，&quot;取得：測試訊息&quot;。</span><span class="sxs-lookup"><span data-stu-id="6e28a-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![顯示測試訊息的網頁瀏覽器](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="6e28a-141">建立 WebClient 專案</span><span class="sxs-lookup"><span data-stu-id="6e28a-141">Create the WebClient project</span></span>

1. <span data-ttu-id="6e28a-142">建立另一個**ASP.NET Web 應用程式（.NET Framework）** 專案，然後選取 [ **MVC**專案] 範本。</span><span class="sxs-lookup"><span data-stu-id="6e28a-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="6e28a-143">（選擇性）選取 [**變更驗證**] > [**無驗證**]。</span><span class="sxs-lookup"><span data-stu-id="6e28a-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="6e28a-144">您在本教學課程中不需要驗證。</span><span class="sxs-lookup"><span data-stu-id="6e28a-144">You don't need authentication for this tutorial.</span></span>

   ![Visual Studio 中 [新增 ASP.NET 專案] 對話方塊中的 MVC 範本](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="6e28a-146">在**方案總管**中，開啟檔案*Views/Home/Index. cshtml*。</span><span class="sxs-lookup"><span data-stu-id="6e28a-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="6e28a-147">將此檔案中的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="6e28a-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="6e28a-148">針對*serviceUrl*變數，請使用 WebService 應用程式的 URI。</span><span class="sxs-lookup"><span data-stu-id="6e28a-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="6e28a-149">在本機執行 WebClient 應用程式，或將其發佈至另一個網站。</span><span class="sxs-lookup"><span data-stu-id="6e28a-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="6e28a-150">當您按一下 [試試看] 按鈕時，會使用下拉式方塊中列出的 HTTP 方法（GET、POST 或 PUT）將 AJAX 要求提交至 WebService 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e28a-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="6e28a-151">這可讓您檢查不同的跨原始來源要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="6e28a-152">目前，WebService 應用程式不支援 CORS，因此，如果您按一下按鈕，就會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="6e28a-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![瀏覽器中的「試試看」錯誤](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="6e28a-154">如果您在[Fiddler](https://www.telerik.com/fiddler)之類的工具中監看 HTTP 流量，您會看到瀏覽器確實傳送 GET 要求，而要求成功，但是 AJAX 呼叫傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="6e28a-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="6e28a-155">請務必瞭解，相同來源原則並不會防止瀏覽器傳送要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="6e28a-156">相反地，它會防止應用程式看到*回應*。</span><span class="sxs-lookup"><span data-stu-id="6e28a-156">Instead, it prevents the application from seeing the *response*.</span></span>

![顯示 web 要求的 Fiddler web 偵錯工具](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="6e28a-158">啟用 CORS</span><span class="sxs-lookup"><span data-stu-id="6e28a-158">Enable CORS</span></span>

<span data-ttu-id="6e28a-159">現在，讓我們在 WebService 應用程式中啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="6e28a-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="6e28a-160">首先，新增 CORS NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="6e28a-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="6e28a-161">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="6e28a-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="6e28a-162">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6e28a-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="6e28a-163">此命令會安裝最新的套件，並更新所有相依性，包括核心 Web API 程式庫。</span><span class="sxs-lookup"><span data-stu-id="6e28a-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="6e28a-164">使用 `-Version` 旗標，以特定版本為目標。</span><span class="sxs-lookup"><span data-stu-id="6e28a-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="6e28a-165">CORS 套件需要 Web API 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6e28a-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="6e28a-166">開啟檔案*應用程式\_Start/WebApiConfig. cs*。</span><span class="sxs-lookup"><span data-stu-id="6e28a-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="6e28a-167">將下列程式碼新增至**WebApiConfig**方法：</span><span class="sxs-lookup"><span data-stu-id="6e28a-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="6e28a-168">接下來，將 **[EnableCors]** 屬性新增至 `TestController` 類別：</span><span class="sxs-lookup"><span data-stu-id="6e28a-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="6e28a-169">針對 [*來源*] 參數，使用您部署 WebClient 應用程式的 URI。</span><span class="sxs-lookup"><span data-stu-id="6e28a-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="6e28a-170">這可允許來自 WebClient 的跨原始來源要求，同時仍禁止所有其他跨網域要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="6e28a-171">稍後，我將更詳細地說明 **[EnableCors]** 的參數。</span><span class="sxs-lookup"><span data-stu-id="6e28a-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="6e28a-172">請勿在*來源*URL 結尾包含正斜線。</span><span class="sxs-lookup"><span data-stu-id="6e28a-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="6e28a-173">重新部署已更新的 WebService 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e28a-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="6e28a-174">您不需要更新 WebClient。</span><span class="sxs-lookup"><span data-stu-id="6e28a-174">You don't need to update WebClient.</span></span> <span data-ttu-id="6e28a-175">現在，WebClient 的 AJAX 要求應該會成功。</span><span class="sxs-lookup"><span data-stu-id="6e28a-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="6e28a-176">GET、PUT 和 POST 方法都是允許的。</span><span class="sxs-lookup"><span data-stu-id="6e28a-176">The GET, PUT, and POST methods are all allowed.</span></span>

![顯示成功測試訊息的網頁瀏覽器](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="6e28a-178">CORS 的運作方式</span><span class="sxs-lookup"><span data-stu-id="6e28a-178">How CORS Works</span></span>

<span data-ttu-id="6e28a-179">本節說明在 HTTP 訊息層級的 CORS 要求中會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="6e28a-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="6e28a-180">請務必瞭解 CORS 的運作方式，讓您可以正確地設定 **[EnableCors]** 屬性，並疑難排解是否如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="6e28a-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="6e28a-181">CORS 規格引進數個新的 HTTP 標頭，可啟用跨原始來源要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="6e28a-182">如果瀏覽器支援 CORS，它會針對跨原始來源要求自動設定這些標頭;您不需要在 JavaScript 程式碼中執行任何特殊動作。</span><span class="sxs-lookup"><span data-stu-id="6e28a-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="6e28a-183">以下是跨原始來源要求的範例。</span><span class="sxs-lookup"><span data-stu-id="6e28a-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="6e28a-184">「來源」標頭會提供提出要求之網站的網域。</span><span class="sxs-lookup"><span data-stu-id="6e28a-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="6e28a-185">如果伺服器允許此要求，則會設定存取控制-允許來源標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="6e28a-186">此標頭的值會符合原始標頭，或為萬用字元值 "\*"，表示允許任何來源。</span><span class="sxs-lookup"><span data-stu-id="6e28a-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="6e28a-187">如果回應不包含存取控制-允許來源標頭，則 AJAX 要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="6e28a-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="6e28a-188">具體而言，瀏覽器不允許此要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="6e28a-189">即使伺服器傳回成功的回應，瀏覽器也不會將回應提供給用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e28a-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="6e28a-190">**預檢要求**</span><span class="sxs-lookup"><span data-stu-id="6e28a-190">**Preflight Requests**</span></span>

<span data-ttu-id="6e28a-191">針對某些 CORS 要求，瀏覽器會在傳送資源的實際要求之前，傳送稱為「預檢要求」的其他要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="6e28a-192">當下列條件成立時，瀏覽器可以略過預檢要求：</span><span class="sxs-lookup"><span data-stu-id="6e28a-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="6e28a-193">要求方法為 GET、HEAD 或 POST，*而*</span><span class="sxs-lookup"><span data-stu-id="6e28a-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="6e28a-194">應用程式不會設定 [接受]、[接受語言]、[內容語言]、[內容類型] 或 [上一個事件識別碼] 以外的任何要求標頭，*以及*</span><span class="sxs-lookup"><span data-stu-id="6e28a-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="6e28a-195">Content-type 標頭（如果已設定）為下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="6e28a-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="6e28a-196">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="6e28a-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="6e28a-197">多部分/表單資料</span><span class="sxs-lookup"><span data-stu-id="6e28a-197">multipart/form-data</span></span>
    - <span data-ttu-id="6e28a-198">text/plain</span><span class="sxs-lookup"><span data-stu-id="6e28a-198">text/plain</span></span>

<span data-ttu-id="6e28a-199">有關要求標頭的規則會套用至應用程式所設定的標頭，方法是呼叫**XMLHttpRequest**物件上的**setRequestHeader** 。</span><span class="sxs-lookup"><span data-stu-id="6e28a-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="6e28a-200">（CORS 規格會呼叫這些「作者要求標頭」）。此規則並不適用于*瀏覽器*可以設定的標頭，例如使用者代理程式、主機或內容長度。</span><span class="sxs-lookup"><span data-stu-id="6e28a-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="6e28a-201">以下是預檢要求的範例：</span><span class="sxs-lookup"><span data-stu-id="6e28a-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="6e28a-202">預先飛行要求會使用 HTTP OPTIONS 方法。</span><span class="sxs-lookup"><span data-stu-id="6e28a-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="6e28a-203">其中包含兩個特殊標頭：</span><span class="sxs-lookup"><span data-stu-id="6e28a-203">It includes two special headers:</span></span>

- <span data-ttu-id="6e28a-204">存取控制-要求-方法：將用於實際要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6e28a-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="6e28a-205">存取控制-要求-標頭：*應用程式*在實際要求上設定的要求標頭清單。</span><span class="sxs-lookup"><span data-stu-id="6e28a-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="6e28a-206">（同樣地，這不包含瀏覽器所設定的標頭）。</span><span class="sxs-lookup"><span data-stu-id="6e28a-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="6e28a-207">以下是範例回應，假設伺服器允許此要求：</span><span class="sxs-lookup"><span data-stu-id="6e28a-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="6e28a-208">回應會包含一個存取控制-Allow-方法標頭，其中會列出允許的方法，並可選擇性地列出允許的標頭的「存取控制-允許-標頭」標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="6e28a-209">如果預檢要求成功，瀏覽器就會傳送實際的要求，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="6e28a-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="6e28a-210">通常用來測試具有預檢選項要求（例如， [Fiddler](https://www.telerik.com/fiddler)和[Postman](https://www.getpostman.com/)）之端點的工具，預設不會傳送必要的選項標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="6e28a-211">確認 `Access-Control-Request-Method` 和 `Access-Control-Request-Headers` 標頭會與要求一起傳送，且選項標頭會透過 IIS 到達應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e28a-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="6e28a-212">若要設定 IIS 以允許 ASP.NET 應用程式接收和處理選項要求，請將下列設定新增至應用程式在 `<system.webServer><handlers>` 區段*的 web.config 檔案*中：</span><span class="sxs-lookup"><span data-stu-id="6e28a-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="6e28a-213">移除 `OPTIONSVerbHandler` 可防止 IIS 處理選項要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="6e28a-214">取代 `ExtensionlessUrlHandler-Integrated-4.0` 可讓選項要求到達應用程式，因為預設的模組註冊只允許 GET、HEAD、POST 和 DEBUG 要求搭配無副檔名 Url。</span><span class="sxs-lookup"><span data-stu-id="6e28a-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="6e28a-215">[EnableCors] 的範圍規則</span><span class="sxs-lookup"><span data-stu-id="6e28a-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="6e28a-216">您可以針對應用程式中的所有 Web API 控制器，啟用每個動作、每個控制器或全域的 CORS。</span><span class="sxs-lookup"><span data-stu-id="6e28a-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="6e28a-217">**每個動作**</span><span class="sxs-lookup"><span data-stu-id="6e28a-217">**Per Action**</span></span>

<span data-ttu-id="6e28a-218">若要為單一動作啟用 CORS，請在動作方法上設定 **[EnableCors]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="6e28a-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="6e28a-219">下列範例只會針對 `GetItem` 方法啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="6e28a-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="6e28a-220">**每個控制器**</span><span class="sxs-lookup"><span data-stu-id="6e28a-220">**Per Controller**</span></span>

<span data-ttu-id="6e28a-221">如果您在控制器類別上設定 **[EnableCors]** ，它會套用至控制器上的所有動作。</span><span class="sxs-lookup"><span data-stu-id="6e28a-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="6e28a-222">若要停用動作的 CORS，請將 **[DisableCors]** 屬性加入至動作。</span><span class="sxs-lookup"><span data-stu-id="6e28a-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="6e28a-223">下列範例會針對每個方法（`PutItem`除外）啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="6e28a-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="6e28a-224">**遍佈**</span><span class="sxs-lookup"><span data-stu-id="6e28a-224">**Globally**</span></span>

<span data-ttu-id="6e28a-225">若要針對應用程式中的所有 Web API 控制器啟用 CORS，請將**EnableCorsAttribute**實例傳遞至**EnableCors**方法：</span><span class="sxs-lookup"><span data-stu-id="6e28a-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="6e28a-226">如果您在一個以上的範圍設定此屬性，則優先順序的順序為：</span><span class="sxs-lookup"><span data-stu-id="6e28a-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="6e28a-227">動作</span><span class="sxs-lookup"><span data-stu-id="6e28a-227">Action</span></span>
2. <span data-ttu-id="6e28a-228">控制器</span><span class="sxs-lookup"><span data-stu-id="6e28a-228">Controller</span></span>
3. <span data-ttu-id="6e28a-229">Global</span><span class="sxs-lookup"><span data-stu-id="6e28a-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="6e28a-230">設定允許的原始來源</span><span class="sxs-lookup"><span data-stu-id="6e28a-230">Set the allowed origins</span></span>

<span data-ttu-id="6e28a-231">**[EnableCors]** 屬性的*來源*參數會指定允許哪些來源存取資源。</span><span class="sxs-lookup"><span data-stu-id="6e28a-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="6e28a-232">此值是允許的原始來源清單（以逗號分隔）。</span><span class="sxs-lookup"><span data-stu-id="6e28a-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="6e28a-233">您也可以使用萬用字元值 "\*"，以允許來自任何來源的要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="6e28a-234">在允許來自任何來源的要求之前，請先仔細考慮。</span><span class="sxs-lookup"><span data-stu-id="6e28a-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="6e28a-235">這表示，任何網站實際上都可以對您的 Web API 進行 AJAX 呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e28a-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="6e28a-236">設定允許的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="6e28a-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="6e28a-237">**[EnableCors]** 屬性的*方法*參數會指定允許哪些 HTTP 方法存取資源。</span><span class="sxs-lookup"><span data-stu-id="6e28a-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="6e28a-238">若要允許所有方法，請使用萬用字元值 "\*"。</span><span class="sxs-lookup"><span data-stu-id="6e28a-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="6e28a-239">下列範例只允許 GET 和 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="6e28a-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="6e28a-240">設定允許的要求標頭</span><span class="sxs-lookup"><span data-stu-id="6e28a-240">Set the allowed request headers</span></span>

<span data-ttu-id="6e28a-241">本文稍早所述，預檢要求可能會包含存取控制要求標頭標題，列出應用程式所設定的 HTTP 標頭（所謂的「作者要求標頭」）。</span><span class="sxs-lookup"><span data-stu-id="6e28a-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="6e28a-242">**[EnableCors]** 屬性的*標頭*參數會指定允許的作者要求標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="6e28a-243">若要允許任何標頭，請將*標頭*設定為 "\*"。</span><span class="sxs-lookup"><span data-stu-id="6e28a-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="6e28a-244">若要將特定標頭列入白名單，請將*標頭*設定為允許的標頭清單（以逗號分隔）：</span><span class="sxs-lookup"><span data-stu-id="6e28a-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="6e28a-245">不過，瀏覽器在設定存取控制-要求標頭方面並不完全一致。</span><span class="sxs-lookup"><span data-stu-id="6e28a-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="6e28a-246">例如，Chrome 目前包含「來源」。</span><span class="sxs-lookup"><span data-stu-id="6e28a-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="6e28a-247">FireFox 不包含標準標頭（例如「接受」），即使應用程式在腳本中設定它們也一樣。</span><span class="sxs-lookup"><span data-stu-id="6e28a-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="6e28a-248">如果您將*標頭*設定為 "\*" 以外的任何專案，您應該包含至少「接受」、「內容類型」和「來源」，加上您想要支援的任何自訂標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="6e28a-249">設定允許的回應標頭</span><span class="sxs-lookup"><span data-stu-id="6e28a-249">Set the allowed response headers</span></span>

<span data-ttu-id="6e28a-250">根據預設，瀏覽器不會將所有的回應標頭公開給應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e28a-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="6e28a-251">預設可用的回應標頭為：</span><span class="sxs-lookup"><span data-stu-id="6e28a-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="6e28a-252">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="6e28a-252">Cache-Control</span></span>
- <span data-ttu-id="6e28a-253">Content-Language</span><span class="sxs-lookup"><span data-stu-id="6e28a-253">Content-Language</span></span>
- <span data-ttu-id="6e28a-254">Content-Type</span><span class="sxs-lookup"><span data-stu-id="6e28a-254">Content-Type</span></span>
- <span data-ttu-id="6e28a-255">到期 (Expires)</span><span class="sxs-lookup"><span data-stu-id="6e28a-255">Expires</span></span>
- <span data-ttu-id="6e28a-256">上次修改時間</span><span class="sxs-lookup"><span data-stu-id="6e28a-256">Last-Modified</span></span>
- <span data-ttu-id="6e28a-257">雜</span><span class="sxs-lookup"><span data-stu-id="6e28a-257">Pragma</span></span>

<span data-ttu-id="6e28a-258">CORS 規格會呼叫這些[簡單的回應標頭](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)。</span><span class="sxs-lookup"><span data-stu-id="6e28a-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="6e28a-259">若要讓應用程式可以使用其他標頭，請設定 **[EnableCors]** 的*exposedHeaders*參數。</span><span class="sxs-lookup"><span data-stu-id="6e28a-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="6e28a-260">在下列範例中，控制器的 `Get` 方法會設定名為 ' X-Custom-Header ' 的自訂標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="6e28a-261">根據預設，瀏覽器不會在跨原始來源要求中公開這個標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="6e28a-262">若要讓標頭可供使用，請在*exposedHeaders*中加入 ' X-Custom-header '。</span><span class="sxs-lookup"><span data-stu-id="6e28a-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="6e28a-263">跨原始來源要求傳遞認證</span><span class="sxs-lookup"><span data-stu-id="6e28a-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="6e28a-264">認證需要在 CORS 要求中進行特殊處理。</span><span class="sxs-lookup"><span data-stu-id="6e28a-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="6e28a-265">根據預設，瀏覽器不會傳送具有跨原始來源要求的任何認證。</span><span class="sxs-lookup"><span data-stu-id="6e28a-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="6e28a-266">認證包括 cookie 以及 HTTP 驗證配置。</span><span class="sxs-lookup"><span data-stu-id="6e28a-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="6e28a-267">若要使用跨原始來源要求傳送認證，用戶端必須將**XMLHttpRequest withCredentials**設定為 true。</span><span class="sxs-lookup"><span data-stu-id="6e28a-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="6e28a-268">直接使用**XMLHttpRequest** ：</span><span class="sxs-lookup"><span data-stu-id="6e28a-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="6e28a-269">在 jQuery 中：</span><span class="sxs-lookup"><span data-stu-id="6e28a-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="6e28a-270">此外，伺服器也必須允許認證。</span><span class="sxs-lookup"><span data-stu-id="6e28a-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="6e28a-271">若要允許 Web API 中的跨原始來源認證，請將 **[EnableCors]** 屬性上的**SupportsCredentials**屬性設定為 true：</span><span class="sxs-lookup"><span data-stu-id="6e28a-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="6e28a-272">如果此屬性為 true，HTTP 回應會包含一個存取控制-允許-認證標頭。</span><span class="sxs-lookup"><span data-stu-id="6e28a-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="6e28a-273">此標頭會告訴瀏覽器，伺服器允許跨原始來源要求的認證。</span><span class="sxs-lookup"><span data-stu-id="6e28a-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="6e28a-274">如果瀏覽器傳送認證，但回應未包含有效的存取控制-允許-認證標頭，則瀏覽器不會向應用程式公開回應，且 AJAX 要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="6e28a-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="6e28a-275">請小心將**SupportsCredentials**設定為 true，因為這表示另一個網域上的網站可以代表使用者將登入使用者的認證傳送給您的 Web API，而不需要使用者知道。</span><span class="sxs-lookup"><span data-stu-id="6e28a-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="6e28a-276">CORS 規格也會指出，如果**SupportsCredentials**為 true，則設定*來源*為 &quot;\*&quot; 無效。</span><span class="sxs-lookup"><span data-stu-id="6e28a-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="6e28a-277">自訂 CORS 原則提供者</span><span class="sxs-lookup"><span data-stu-id="6e28a-277">Custom CORS policy providers</span></span>

<span data-ttu-id="6e28a-278">**[EnableCors]** 屬性會實行**ICorsPolicyProvider**介面。</span><span class="sxs-lookup"><span data-stu-id="6e28a-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="6e28a-279">您可以藉由建立衍生自**屬性**的類別並執行**ICorsPolicyProvider**，來提供自己的實作為。</span><span class="sxs-lookup"><span data-stu-id="6e28a-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="6e28a-280">現在您可以將屬性套用至您要放置的任何位置 **[EnableCors]** 。</span><span class="sxs-lookup"><span data-stu-id="6e28a-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="6e28a-281">例如，自訂 CORS 原則提供者可以從設定檔讀取設定。</span><span class="sxs-lookup"><span data-stu-id="6e28a-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="6e28a-282">除了使用屬性以外，您也可以註冊建立**ICorsPolicyProvider**物件的**ICorsPolicyProviderFactory**物件。</span><span class="sxs-lookup"><span data-stu-id="6e28a-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="6e28a-283">若要設定**ICorsPolicyProviderFactory**，請在啟動時呼叫**SetCorsPolicyProviderFactory**擴充方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6e28a-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="6e28a-284">瀏覽器支援</span><span class="sxs-lookup"><span data-stu-id="6e28a-284">Browser support</span></span>

<span data-ttu-id="6e28a-285">Web API CORS 封裝是一種伺服器端技術。</span><span class="sxs-lookup"><span data-stu-id="6e28a-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="6e28a-286">使用者的瀏覽器也必須支援 CORS。</span><span class="sxs-lookup"><span data-stu-id="6e28a-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="6e28a-287">幸好，所有主要瀏覽器的目前版本都包含[對 CORS 的支援](http://caniuse.com/cors)。</span><span class="sxs-lookup"><span data-stu-id="6e28a-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
