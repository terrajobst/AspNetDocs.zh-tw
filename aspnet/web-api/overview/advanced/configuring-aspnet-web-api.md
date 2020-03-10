---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: 設定 ASP.NET Web API 2-ASP.NET 4。x
author: MikeWasson
description: 為 ASP.NET 4.x 設定 ASP.NET Web API 2： Configure settings，ASP.NET 4.x 裝載，OWIN 自我裝載，全域服務和前控制站設定。
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557719"
---
# <a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="7997e-103">設定 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="7997e-103">Configuring ASP.NET Web API 2</span></span>

<span data-ttu-id="7997e-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7997e-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7997e-105">本主題描述如何設定 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="7997e-105">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="7997e-106">設定</span><span class="sxs-lookup"><span data-stu-id="7997e-106">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="7997e-107">設定具有 ASP.NET 裝載的 Web API</span><span class="sxs-lookup"><span data-stu-id="7997e-107">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="7997e-108">使用 OWIN 自我裝載設定 Web API</span><span class="sxs-lookup"><span data-stu-id="7997e-108">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="7997e-109">全域 Web API 服務</span><span class="sxs-lookup"><span data-stu-id="7997e-109">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="7997e-110">每一控制器設定</span><span class="sxs-lookup"><span data-stu-id="7997e-110">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="7997e-111">組態設定</span><span class="sxs-lookup"><span data-stu-id="7997e-111">Configuration Settings</span></span>

<span data-ttu-id="7997e-112">Web API 設定是在[HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)類別中定義。</span><span class="sxs-lookup"><span data-stu-id="7997e-112">Web API configuration settings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="7997e-113">成員</span><span class="sxs-lookup"><span data-stu-id="7997e-113">Member</span></span> | <span data-ttu-id="7997e-114">說明</span><span class="sxs-lookup"><span data-stu-id="7997e-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7997e-115">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="7997e-115">**DependencyResolver**</span></span> | <span data-ttu-id="7997e-116">啟用控制器的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="7997e-116">Enables dependency injection for controllers.</span></span> <span data-ttu-id="7997e-117">請參閱[使用 WEB API 相依性解析程式](dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-117">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="7997e-118">**篩選**</span><span class="sxs-lookup"><span data-stu-id="7997e-118">**Filters**</span></span> | <span data-ttu-id="7997e-119">動作篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7997e-119">Action filters.</span></span> |
| <span data-ttu-id="7997e-120">**格式化**</span><span class="sxs-lookup"><span data-stu-id="7997e-120">**Formatters**</span></span> | <span data-ttu-id="7997e-121">[媒體類型](../formats-and-model-binding/media-formatters.md)格式器。</span><span class="sxs-lookup"><span data-stu-id="7997e-121">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="7997e-122">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="7997e-122">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="7997e-123">指定伺服器是否應該在 HTTP 回應訊息中包含錯誤詳細資料，例如例外狀況訊息和堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="7997e-123">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="7997e-124">請參閱[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))。</span><span class="sxs-lookup"><span data-stu-id="7997e-124">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="7997e-125">**初始**</span><span class="sxs-lookup"><span data-stu-id="7997e-125">**Initializer**</span></span> | <span data-ttu-id="7997e-126">執行**HttpConfiguration**最後初始化的函式。</span><span class="sxs-lookup"><span data-stu-id="7997e-126">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="7997e-127">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="7997e-127">**MessageHandlers**</span></span> | <span data-ttu-id="7997e-128">[HTTP 訊息處理常式](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-128">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="7997e-129">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="7997e-129">**ParameterBindingRules**</span></span> | <span data-ttu-id="7997e-130">在控制器動作上系結參數的規則集合。</span><span class="sxs-lookup"><span data-stu-id="7997e-130">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="7997e-131">**內容**</span><span class="sxs-lookup"><span data-stu-id="7997e-131">**Properties**</span></span> | <span data-ttu-id="7997e-132">一般屬性包。</span><span class="sxs-lookup"><span data-stu-id="7997e-132">A generic property bag.</span></span> |
| <span data-ttu-id="7997e-133">**路由**</span><span class="sxs-lookup"><span data-stu-id="7997e-133">**Routes**</span></span> | <span data-ttu-id="7997e-134">路由的集合。</span><span class="sxs-lookup"><span data-stu-id="7997e-134">The collection of routes.</span></span> <span data-ttu-id="7997e-135">請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-135">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="7997e-136">**服務**</span><span class="sxs-lookup"><span data-stu-id="7997e-136">**Services**</span></span> | <span data-ttu-id="7997e-137">服務的集合。</span><span class="sxs-lookup"><span data-stu-id="7997e-137">The collection of services.</span></span> <span data-ttu-id="7997e-138">請參閱[服務](#services)。</span><span class="sxs-lookup"><span data-stu-id="7997e-138">See [Services](#services).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="7997e-139">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7997e-139">Prerequisites</span></span>

<span data-ttu-id="7997e-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional 或 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="7997e-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="7997e-141">設定具有 ASP.NET 裝載的 Web API</span><span class="sxs-lookup"><span data-stu-id="7997e-141">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="7997e-142">在 ASP.NET 應用程式中，呼叫 GlobalConfiguration 來設定 Web API。在**應用程式\_Start**方法中[設定](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7997e-142">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="7997e-143">**Configure**方法會採用具有**HttpConfiguration**類型之單一參數的委派。</span><span class="sxs-lookup"><span data-stu-id="7997e-143">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="7997e-144">執行委派內的所有設定。</span><span class="sxs-lookup"><span data-stu-id="7997e-144">Perform all of your configuration inside the delegate.</span></span>

<span data-ttu-id="7997e-145">以下是使用匿名委派的範例：</span><span class="sxs-lookup"><span data-stu-id="7997e-145">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="7997e-146">在 Visual Studio 2017 中，如果您在 [**新增 ASP.NET 專案**] 對話方塊中選取 [web API]，[ASP.NET Web 應用程式] 專案範本會自動設定設定程式碼。</span><span class="sxs-lookup"><span data-stu-id="7997e-146">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="7997e-147">專案範本會在應用程式\_開始 資料夾內建立名為 WebApiConfig.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="7997e-147">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="7997e-148">這個程式碼檔案會定義委派，您應該在其中放置 Web API 設定程式碼。</span><span class="sxs-lookup"><span data-stu-id="7997e-148">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="7997e-149">專案範本也會將從應用程式呼叫委派的程式碼加入 **\_啟動**。</span><span class="sxs-lookup"><span data-stu-id="7997e-149">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="7997e-150">使用 OWIN 自我裝載設定 Web API</span><span class="sxs-lookup"><span data-stu-id="7997e-150">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="7997e-151">如果您是使用 OWIN 自我裝載，請建立新的**HttpConfiguration**實例。</span><span class="sxs-lookup"><span data-stu-id="7997e-151">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="7997e-152">在此實例上執行任何設定，然後將實例傳遞至**Owin. UseWebApi**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="7997e-152">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="7997e-153">本教學課程[使用 OWIN 至自我裝載 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)顯示完整的步驟。</span><span class="sxs-lookup"><span data-stu-id="7997e-153">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="7997e-154">全域 Web API 服務</span><span class="sxs-lookup"><span data-stu-id="7997e-154">Global Web API Services</span></span>

<span data-ttu-id="7997e-155">**HttpConfiguration**集合包含一組全域服務，可供 Web API 用來執行各種工作，例如控制器選取和內容協調。</span><span class="sxs-lookup"><span data-stu-id="7997e-155">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="7997e-156">**服務**集合不是服務探索或相依性插入的一般用途機制。</span><span class="sxs-lookup"><span data-stu-id="7997e-156">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="7997e-157">它只會儲存 Web API 架構已知的服務類型。</span><span class="sxs-lookup"><span data-stu-id="7997e-157">It only stores service types that are known to the Web API framework.</span></span>

<span data-ttu-id="7997e-158">**服務**集合會使用一組預設的服務進行初始化，您可以提供自己的自訂執行。</span><span class="sxs-lookup"><span data-stu-id="7997e-158">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="7997e-159">有些服務支援多個實例，而其他則只能有一個實例。</span><span class="sxs-lookup"><span data-stu-id="7997e-159">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="7997e-160">（不過，您也可以在控制器層級提供服務; 請參閱[每個控制器](#percontrollerconfig)設定。</span><span class="sxs-lookup"><span data-stu-id="7997e-160">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="7997e-161">單一實例服務</span><span class="sxs-lookup"><span data-stu-id="7997e-161">Single-Instance Services</span></span>

| <span data-ttu-id="7997e-162">服務</span><span class="sxs-lookup"><span data-stu-id="7997e-162">Service</span></span> | <span data-ttu-id="7997e-163">說明</span><span class="sxs-lookup"><span data-stu-id="7997e-163">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7997e-164">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="7997e-164">**IActionValueBinder**</span></span> | <span data-ttu-id="7997e-165">取得參數的系結。</span><span class="sxs-lookup"><span data-stu-id="7997e-165">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="7997e-166">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="7997e-166">**IApiExplorer**</span></span> | <span data-ttu-id="7997e-167">取得應用程式所公開之 Api 的描述。</span><span class="sxs-lookup"><span data-stu-id="7997e-167">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="7997e-168">請參閱[建立 WEB API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)的說明頁面。</span><span class="sxs-lookup"><span data-stu-id="7997e-168">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="7997e-169">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="7997e-169">**IAssembliesResolver**</span></span> | <span data-ttu-id="7997e-170">取得應用程式的元件清單。</span><span class="sxs-lookup"><span data-stu-id="7997e-170">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="7997e-171">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-171">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="7997e-172">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="7997e-172">**IBodyModelValidator**</span></span> | <span data-ttu-id="7997e-173">驗證由媒體類型格式器從要求主體讀取的模型。</span><span class="sxs-lookup"><span data-stu-id="7997e-173">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="7997e-174">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="7997e-174">**IContentNegotiator**</span></span> | <span data-ttu-id="7997e-175">執行內容交涉。</span><span class="sxs-lookup"><span data-stu-id="7997e-175">Performs content negotiation.</span></span> |
| <span data-ttu-id="7997e-176">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="7997e-176">**IDocumentationProvider**</span></span> | <span data-ttu-id="7997e-177">提供 Api 的檔。</span><span class="sxs-lookup"><span data-stu-id="7997e-177">Provides documentation for APIs.</span></span> <span data-ttu-id="7997e-178">預設值是 **null**。</span><span class="sxs-lookup"><span data-stu-id="7997e-178">The default is **null**.</span></span> <span data-ttu-id="7997e-179">請參閱[建立 WEB API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)的說明頁面。</span><span class="sxs-lookup"><span data-stu-id="7997e-179">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="7997e-180">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="7997e-180">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="7997e-181">指出主機是否應緩衝 HTTP 訊息實體內文。</span><span class="sxs-lookup"><span data-stu-id="7997e-181">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="7997e-182">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="7997e-182">**IHttpActionInvoker**</span></span> | <span data-ttu-id="7997e-183">叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="7997e-183">Invokes a controller action.</span></span> <span data-ttu-id="7997e-184">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-184">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="7997e-185">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="7997e-185">**IHttpActionSelector**</span></span> | <span data-ttu-id="7997e-186">選取控制器動作。</span><span class="sxs-lookup"><span data-stu-id="7997e-186">Selects a controller action.</span></span> <span data-ttu-id="7997e-187">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-187">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="7997e-188">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="7997e-188">**IHttpControllerActivator**</span></span> | <span data-ttu-id="7997e-189">啟用控制器。</span><span class="sxs-lookup"><span data-stu-id="7997e-189">Activates a controller.</span></span> <span data-ttu-id="7997e-190">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-190">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="7997e-191">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="7997e-191">**IHttpControllerSelector**</span></span> | <span data-ttu-id="7997e-192">選取控制器。</span><span class="sxs-lookup"><span data-stu-id="7997e-192">Selects a controller.</span></span> <span data-ttu-id="7997e-193">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-193">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="7997e-194">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="7997e-194">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="7997e-195">提供應用程式中的 Web API 控制器類型清單。</span><span class="sxs-lookup"><span data-stu-id="7997e-195">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="7997e-196">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-196">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="7997e-197">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="7997e-197">**ITraceManager**</span></span> | <span data-ttu-id="7997e-198">初始化追蹤架構。</span><span class="sxs-lookup"><span data-stu-id="7997e-198">Initializes the tracing framework.</span></span> <span data-ttu-id="7997e-199">請參閱[ASP.NET Web API 中的追蹤](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-199">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="7997e-200">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="7997e-200">**ITraceWriter**</span></span> | <span data-ttu-id="7997e-201">提供追蹤寫入器。</span><span class="sxs-lookup"><span data-stu-id="7997e-201">Provides a trace writer.</span></span> <span data-ttu-id="7997e-202">預設值為「無 op」追蹤寫入器。</span><span class="sxs-lookup"><span data-stu-id="7997e-202">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="7997e-203">請參閱[ASP.NET Web API 中的追蹤](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7997e-203">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="7997e-204">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="7997e-204">**IModelValidatorCache**</span></span> | <span data-ttu-id="7997e-205">提供模型驗證程式的快取。</span><span class="sxs-lookup"><span data-stu-id="7997e-205">Provides a cache of model validators.</span></span> |

<span data-ttu-id="7997e-206">多重實例服務</span><span class="sxs-lookup"><span data-stu-id="7997e-206">Multiple-Instance Services</span></span>

|                 <span data-ttu-id="7997e-207">服務</span><span class="sxs-lookup"><span data-stu-id="7997e-207">Service</span></span>                 |                                                                                                              <span data-ttu-id="7997e-208">說明</span><span class="sxs-lookup"><span data-stu-id="7997e-208">Description</span></span>                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <span data-ttu-id="7997e-209"><strong>IFilterProvider</strong></span><span class="sxs-lookup"><span data-stu-id="7997e-209"><strong>IFilterProvider</strong></span></span>     |                                                                                           <span data-ttu-id="7997e-210">傳回控制器動作的篩選器清單。</span><span class="sxs-lookup"><span data-stu-id="7997e-210">Returns a list of filters for a controller action.</span></span>                                                                                           |
|  <span data-ttu-id="7997e-211"><strong>ModelBinderProvider</strong></span><span class="sxs-lookup"><span data-stu-id="7997e-211"><strong>ModelBinderProvider</strong></span></span>   |                                                                                                <span data-ttu-id="7997e-212">傳回給定類型的模型系結器。</span><span class="sxs-lookup"><span data-stu-id="7997e-212">Returns a model binder for a given type.</span></span>                                                                                                |
| <span data-ttu-id="7997e-213"><strong>ModelMetadataProvider</strong></span><span class="sxs-lookup"><span data-stu-id="7997e-213"><strong>ModelMetadataProvider</strong></span></span>  |                                                                                                     <span data-ttu-id="7997e-214">提供模型的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7997e-214">Provides metadata for a model.</span></span>                                                                                                     |
| <span data-ttu-id="7997e-215"><strong>ModelValidatorProvider</strong></span><span class="sxs-lookup"><span data-stu-id="7997e-215"><strong>ModelValidatorProvider</strong></span></span> |                                                                                                   <span data-ttu-id="7997e-216">提供模型的驗證程式。</span><span class="sxs-lookup"><span data-stu-id="7997e-216">Provides a validator for a model.</span></span>                                                                                                    |
|  <span data-ttu-id="7997e-217"><strong>ValueProviderFactory</strong></span><span class="sxs-lookup"><span data-stu-id="7997e-217"><strong>ValueProviderFactory</strong></span></span>  | <span data-ttu-id="7997e-218">建立值提供者。</span><span class="sxs-lookup"><span data-stu-id="7997e-218">Creates a value provider.</span></span> <span data-ttu-id="7997e-219">如需詳細資訊，請參閱 Mike 延遲的 blog 文章[如何在 WebAPI 中建立自訂值提供者](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="7997e-219">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |

<span data-ttu-id="7997e-220">若要將自訂的執行加入多重實例服務，請在**服務**集合上呼叫**add**或**Insert** ：</span><span class="sxs-lookup"><span data-stu-id="7997e-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="7997e-221">若要將單一實例服務取代為自訂的執行，請在**服務**集合上呼叫**replace** ：</span><span class="sxs-lookup"><span data-stu-id="7997e-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="7997e-222">每一控制器設定</span><span class="sxs-lookup"><span data-stu-id="7997e-222">Per-Controller Configuration</span></span>

<span data-ttu-id="7997e-223">您可以根據每個控制器來覆寫下列設定：</span><span class="sxs-lookup"><span data-stu-id="7997e-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="7997e-224">媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="7997e-224">Media-type formatters</span></span>
- <span data-ttu-id="7997e-225">參數系結規則</span><span class="sxs-lookup"><span data-stu-id="7997e-225">Parameter binding rules</span></span>
- <span data-ttu-id="7997e-226">服務</span><span class="sxs-lookup"><span data-stu-id="7997e-226">Services</span></span>

<span data-ttu-id="7997e-227">若要這樣做，請定義可執行**IControllerConfiguration**介面的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="7997e-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="7997e-228">然後將屬性套用至控制器。</span><span class="sxs-lookup"><span data-stu-id="7997e-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="7997e-229">下列範例會使用自訂格式器來取代預設的媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="7997e-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="7997e-230">**IControllerConfiguration**方法採用兩個參數：</span><span class="sxs-lookup"><span data-stu-id="7997e-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="7997e-231">**HttpControllerSettings**物件</span><span class="sxs-lookup"><span data-stu-id="7997e-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="7997e-232">**HttpControllerDescriptor**物件</span><span class="sxs-lookup"><span data-stu-id="7997e-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="7997e-233">**HttpControllerDescriptor**包含控制器的描述，您可以在其中檢查資訊的用途（例如，區分兩個控制器）。</span><span class="sxs-lookup"><span data-stu-id="7997e-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="7997e-234">使用**HttpControllerSettings**物件來設定控制器。</span><span class="sxs-lookup"><span data-stu-id="7997e-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="7997e-235">此物件包含您可以根據每個控制器覆寫之設定參數的子集。</span><span class="sxs-lookup"><span data-stu-id="7997e-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="7997e-236">您不會變更的任何設定都會預設為全域**HttpConfiguration**物件。</span><span class="sxs-lookup"><span data-stu-id="7997e-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
