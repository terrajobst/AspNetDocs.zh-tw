---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: 設定 ASP.NET Web API 2-ASP.NET 4.x
author: MikeWasson
description: 設定 ASP.NET Web API 2 適用於 ASP.NET 4.x:設定設定、 ASP.NET 4.x 裝載、 OWIN 自我裝載的全域服務和前的控制站設定。
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 39629ba404e536b29318db00bce8c4443a782497
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59411939"
---
# <a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="d2568-103">設定 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="d2568-103">Configuring ASP.NET Web API 2</span></span>

<span data-ttu-id="d2568-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d2568-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d2568-105">本主題描述如何設定 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="d2568-105">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="d2568-106">組態設定</span><span class="sxs-lookup"><span data-stu-id="d2568-106">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="d2568-107">設定與 ASP.NET 裝載的 Web API</span><span class="sxs-lookup"><span data-stu-id="d2568-107">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="d2568-108">設定 Web API 與 OWIN 自我裝載</span><span class="sxs-lookup"><span data-stu-id="d2568-108">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="d2568-109">全域的 Web API 服務</span><span class="sxs-lookup"><span data-stu-id="d2568-109">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="d2568-110">每個控制站設定</span><span class="sxs-lookup"><span data-stu-id="d2568-110">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="d2568-111">組態設定</span><span class="sxs-lookup"><span data-stu-id="d2568-111">Configuration Settings</span></span>

<span data-ttu-id="d2568-112">Web API 組態設定會定義在[HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="d2568-112">Web API configuration settings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="d2568-113">成員</span><span class="sxs-lookup"><span data-stu-id="d2568-113">Member</span></span> | <span data-ttu-id="d2568-114">描述</span><span class="sxs-lookup"><span data-stu-id="d2568-114">Description</span></span> |
| --- | --- |
| **<span data-ttu-id="d2568-115">DependencyResolver</span><span class="sxs-lookup"><span data-stu-id="d2568-115">DependencyResolver</span></span>** | <span data-ttu-id="d2568-116">可讓控制站的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="d2568-116">Enables dependency injection for controllers.</span></span> <span data-ttu-id="d2568-117">請參閱[使用 Web API 的相依性解析程式](dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-117">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| **<span data-ttu-id="d2568-118">篩選條件</span><span class="sxs-lookup"><span data-stu-id="d2568-118">Filters</span></span>** | <span data-ttu-id="d2568-119">動作篩選條件。</span><span class="sxs-lookup"><span data-stu-id="d2568-119">Action filters.</span></span> |
| **<span data-ttu-id="d2568-120">格式器</span><span class="sxs-lookup"><span data-stu-id="d2568-120">Formatters</span></span>** | <span data-ttu-id="d2568-121">[媒體類型格式器](../formats-and-model-binding/media-formatters.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-121">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| **<span data-ttu-id="d2568-122">IncludeErrorDetailPolicy</span><span class="sxs-lookup"><span data-stu-id="d2568-122">IncludeErrorDetailPolicy</span></span>** | <span data-ttu-id="d2568-123">指定伺服器是否應該在 HTTP 回應訊息中包含錯誤詳細資料，例如例外狀況訊息和堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="d2568-123">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="d2568-124">請參閱[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))。</span><span class="sxs-lookup"><span data-stu-id="d2568-124">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| **<span data-ttu-id="d2568-125">初始設定式</span><span class="sxs-lookup"><span data-stu-id="d2568-125">Initializer</span></span>** | <span data-ttu-id="d2568-126">執行最後的初始化函式**HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="d2568-126">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| **<span data-ttu-id="d2568-127">MessageHandlers</span><span class="sxs-lookup"><span data-stu-id="d2568-127">MessageHandlers</span></span>** | <span data-ttu-id="d2568-128">[HTTP 訊息處理常式](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-128">[HTTP message handlers](http-message-handlers.md).</span></span> |
| **<span data-ttu-id="d2568-129">ParameterBindingRules</span><span class="sxs-lookup"><span data-stu-id="d2568-129">ParameterBindingRules</span></span>** | <span data-ttu-id="d2568-130">用於控制器動作上的繫結參數的規則集合。</span><span class="sxs-lookup"><span data-stu-id="d2568-130">A collection of rules for binding parameters on controller actions.</span></span> |
| **<span data-ttu-id="d2568-131">屬性</span><span class="sxs-lookup"><span data-stu-id="d2568-131">Properties</span></span>** | <span data-ttu-id="d2568-132">泛型屬性包。</span><span class="sxs-lookup"><span data-stu-id="d2568-132">A generic property bag.</span></span> |
| **<span data-ttu-id="d2568-133">路由</span><span class="sxs-lookup"><span data-stu-id="d2568-133">Routes</span></span>** | <span data-ttu-id="d2568-134">路由的集合。</span><span class="sxs-lookup"><span data-stu-id="d2568-134">The collection of routes.</span></span> <span data-ttu-id="d2568-135">請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-135">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| **<span data-ttu-id="d2568-136">服務</span><span class="sxs-lookup"><span data-stu-id="d2568-136">Services</span></span>** | <span data-ttu-id="d2568-137">服務集合。</span><span class="sxs-lookup"><span data-stu-id="d2568-137">The collection of services.</span></span> <span data-ttu-id="d2568-138">請參閱[Services](#services)。</span><span class="sxs-lookup"><span data-stu-id="d2568-138">See [Services](#services).</span></span> |


## <a name="prerequisites"></a><span data-ttu-id="d2568-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="d2568-139">Prerequisites</span></span>

<span data-ttu-id="d2568-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、 Professional 或 Enterprise edition。</span><span class="sxs-lookup"><span data-stu-id="d2568-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="d2568-141">設定與 ASP.NET 裝載的 Web API</span><span class="sxs-lookup"><span data-stu-id="d2568-141">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="d2568-142">在 ASP.NET 應用程式，請藉由呼叫中設定 Web API [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx)中**應用程式\_啟動**方法。</span><span class="sxs-lookup"><span data-stu-id="d2568-142">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="d2568-143">**設定**方法會接受具有單一參數型別的委派**HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="d2568-143">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="d2568-144">執行所有程式委派中的設定。</span><span class="sxs-lookup"><span data-stu-id="d2568-144">Perform all of your configuration inside the delegate.</span></span>

<span data-ttu-id="d2568-145">以下是使用匿名委派的範例：</span><span class="sxs-lookup"><span data-stu-id="d2568-145">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="d2568-146">在 Visual Studio 2017 中，「 ASP.NET Web 應用程式 」 專案範本會自動設定的組態程式碼中，如果您選取 Web API 」 中**新的 ASP.NET 專案**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d2568-146">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="d2568-147">專案範本會建立名為 「 應用程式的 WebApiConfig.cs 檔案\_開始資料夾。</span><span class="sxs-lookup"><span data-stu-id="d2568-147">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="d2568-148">這個程式碼檔會定義應放置您的 Web API 組態程式碼的委派。</span><span class="sxs-lookup"><span data-stu-id="d2568-148">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="d2568-149">專案範本也會將加入程式碼呼叫的委派**應用程式\_啟動**。</span><span class="sxs-lookup"><span data-stu-id="d2568-149">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="d2568-150">設定 Web API 與 OWIN 自我裝載</span><span class="sxs-lookup"><span data-stu-id="d2568-150">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="d2568-151">如果您是使用 OWIN 自我裝載，建立新**HttpConfiguration**執行個體。</span><span class="sxs-lookup"><span data-stu-id="d2568-151">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="d2568-152">在此情況下，執行任何設定，然後將傳遞至執行個體**Owin.UseWebApi**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="d2568-152">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="d2568-153">本教學課程[使用 OWIN 自我裝載 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)顯示完成的步驟。</span><span class="sxs-lookup"><span data-stu-id="d2568-153">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="d2568-154">全域的 Web API 服務</span><span class="sxs-lookup"><span data-stu-id="d2568-154">Global Web API Services</span></span>

<span data-ttu-id="d2568-155">**HttpConfiguration.Services**集合包含一組 Web API 用來執行各種工作，例如控制器選取項目和內容交涉的全域服務。</span><span class="sxs-lookup"><span data-stu-id="d2568-155">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="d2568-156">**Services**集合不是服務探索或相依性插入的一般用途機制。</span><span class="sxs-lookup"><span data-stu-id="d2568-156">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="d2568-157">它只會儲存 Web API 架構已知的服務類型。</span><span class="sxs-lookup"><span data-stu-id="d2568-157">It only stores service types that are known to the Web API framework.</span></span>


<span data-ttu-id="d2568-158">**Services**集合已初始化與一組預設的服務，而且您可以提供您自己的自訂實作。</span><span class="sxs-lookup"><span data-stu-id="d2568-158">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="d2568-159">某些服務會支援多個執行個體，而有些則可以有只有一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d2568-159">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="d2568-160">(不過，您也可以提供在控制器層級的服務，請參閱[每個控制站設定](#percontrollerconfig)。</span><span class="sxs-lookup"><span data-stu-id="d2568-160">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="d2568-161">單一執行個體的服務</span><span class="sxs-lookup"><span data-stu-id="d2568-161">Single-Instance Services</span></span>


| <span data-ttu-id="d2568-162">服務</span><span class="sxs-lookup"><span data-stu-id="d2568-162">Service</span></span> | <span data-ttu-id="d2568-163">描述</span><span class="sxs-lookup"><span data-stu-id="d2568-163">Description</span></span> |
| --- | --- |
| **<span data-ttu-id="d2568-164">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="d2568-164">IActionValueBinder</span></span>** | <span data-ttu-id="d2568-165">取得參數繫結。</span><span class="sxs-lookup"><span data-stu-id="d2568-165">Gets a binding for a parameter.</span></span> |
| **<span data-ttu-id="d2568-166">IApiExplorer</span><span class="sxs-lookup"><span data-stu-id="d2568-166">IApiExplorer</span></span>** | <span data-ttu-id="d2568-167">取得描述元的應用程式所公開的 Api。</span><span class="sxs-lookup"><span data-stu-id="d2568-167">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="d2568-168">請參閱[建立 Web API 說明頁面](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-168">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| **<span data-ttu-id="d2568-169">IAssembliesResolver</span><span class="sxs-lookup"><span data-stu-id="d2568-169">IAssembliesResolver</span></span>** | <span data-ttu-id="d2568-170">取得應用程式的組件清單。</span><span class="sxs-lookup"><span data-stu-id="d2568-170">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="d2568-171">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-171">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| **<span data-ttu-id="d2568-172">IBodyModelValidator</span><span class="sxs-lookup"><span data-stu-id="d2568-172">IBodyModelValidator</span></span>** | <span data-ttu-id="d2568-173">驗證的模型，會從要求主體讀取媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="d2568-173">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| **<span data-ttu-id="d2568-174">IContentNegotiator</span><span class="sxs-lookup"><span data-stu-id="d2568-174">IContentNegotiator</span></span>** | <span data-ttu-id="d2568-175">執行內容交涉。</span><span class="sxs-lookup"><span data-stu-id="d2568-175">Performs content negotiation.</span></span> |
| **<span data-ttu-id="d2568-176">IDocumentationProvider</span><span class="sxs-lookup"><span data-stu-id="d2568-176">IDocumentationProvider</span></span>** | <span data-ttu-id="d2568-177">提供 Api 的文件。</span><span class="sxs-lookup"><span data-stu-id="d2568-177">Provides documentation for APIs.</span></span> <span data-ttu-id="d2568-178">預設值是**null**。</span><span class="sxs-lookup"><span data-stu-id="d2568-178">The default is **null**.</span></span> <span data-ttu-id="d2568-179">請參閱[建立 Web API 說明頁面](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-179">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| **<span data-ttu-id="d2568-180">IHostBufferPolicySelector</span><span class="sxs-lookup"><span data-stu-id="d2568-180">IHostBufferPolicySelector</span></span>** | <span data-ttu-id="d2568-181">表示主機是否應緩衝 HTTP 訊息實體內文。</span><span class="sxs-lookup"><span data-stu-id="d2568-181">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| **<span data-ttu-id="d2568-182">IHttpActionInvoker</span><span class="sxs-lookup"><span data-stu-id="d2568-182">IHttpActionInvoker</span></span>** | <span data-ttu-id="d2568-183">叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="d2568-183">Invokes a controller action.</span></span> <span data-ttu-id="d2568-184">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-184">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| **<span data-ttu-id="d2568-185">IHttpActionSelector</span><span class="sxs-lookup"><span data-stu-id="d2568-185">IHttpActionSelector</span></span>** | <span data-ttu-id="d2568-186">選取控制器動作。</span><span class="sxs-lookup"><span data-stu-id="d2568-186">Selects a controller action.</span></span> <span data-ttu-id="d2568-187">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-187">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| **<span data-ttu-id="d2568-188">IHttpControllerActivator</span><span class="sxs-lookup"><span data-stu-id="d2568-188">IHttpControllerActivator</span></span>** | <span data-ttu-id="d2568-189">啟動控制站。</span><span class="sxs-lookup"><span data-stu-id="d2568-189">Activates a controller.</span></span> <span data-ttu-id="d2568-190">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-190">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| **<span data-ttu-id="d2568-191">IHttpControllerSelector</span><span class="sxs-lookup"><span data-stu-id="d2568-191">IHttpControllerSelector</span></span>** | <span data-ttu-id="d2568-192">選取控制器。</span><span class="sxs-lookup"><span data-stu-id="d2568-192">Selects a controller.</span></span> <span data-ttu-id="d2568-193">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-193">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| **<span data-ttu-id="d2568-194">IHttpControllerTypeResolver</span><span class="sxs-lookup"><span data-stu-id="d2568-194">IHttpControllerTypeResolver</span></span>** | <span data-ttu-id="d2568-195">提供一份應用程式中的 Web API 控制器類型。</span><span class="sxs-lookup"><span data-stu-id="d2568-195">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="d2568-196">請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-196">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| **<span data-ttu-id="d2568-197">ITraceManager</span><span class="sxs-lookup"><span data-stu-id="d2568-197">ITraceManager</span></span>** | <span data-ttu-id="d2568-198">初始化追蹤架構。</span><span class="sxs-lookup"><span data-stu-id="d2568-198">Initializes the tracing framework.</span></span> <span data-ttu-id="d2568-199">請參閱[ASP.NET Web API 中追蹤](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-199">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| **<span data-ttu-id="d2568-200">ITraceWriter</span><span class="sxs-lookup"><span data-stu-id="d2568-200">ITraceWriter</span></span>** | <span data-ttu-id="d2568-201">提供的追蹤寫入器。</span><span class="sxs-lookup"><span data-stu-id="d2568-201">Provides a trace writer.</span></span> <span data-ttu-id="d2568-202">預設為 「 無操作 」 追蹤寫入器。</span><span class="sxs-lookup"><span data-stu-id="d2568-202">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="d2568-203">請參閱[ASP.NET Web API 中追蹤](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d2568-203">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| **<span data-ttu-id="d2568-204">IModelValidatorCache</span><span class="sxs-lookup"><span data-stu-id="d2568-204">IModelValidatorCache</span></span>** | <span data-ttu-id="d2568-205">提供模型驗證程式的快取。</span><span class="sxs-lookup"><span data-stu-id="d2568-205">Provides a cache of model validators.</span></span> |

<span data-ttu-id="d2568-206">多個執行個體的服務</span><span class="sxs-lookup"><span data-stu-id="d2568-206">Multiple-Instance Services</span></span>


|                 <span data-ttu-id="d2568-207">服務</span><span class="sxs-lookup"><span data-stu-id="d2568-207">Service</span></span>                 |                                                                                                              <span data-ttu-id="d2568-208">描述</span><span class="sxs-lookup"><span data-stu-id="d2568-208">Description</span></span>                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong><span data-ttu-id="d2568-209">IFilterProvider</span><span class="sxs-lookup"><span data-stu-id="d2568-209">IFilterProvider</span></span></strong>     |                                                                                           <span data-ttu-id="d2568-210">傳回控制器動作篩選條件的清單。</span><span class="sxs-lookup"><span data-stu-id="d2568-210">Returns a list of filters for a controller action.</span></span>                                                                                           |
|  <strong><span data-ttu-id="d2568-211">ModelBinderProvider</span><span class="sxs-lookup"><span data-stu-id="d2568-211">ModelBinderProvider</span></span></strong>   |                                                                                                <span data-ttu-id="d2568-212">傳回指定型別的模型繫結。</span><span class="sxs-lookup"><span data-stu-id="d2568-212">Returns a model binder for a given type.</span></span>                                                                                                |
| <strong><span data-ttu-id="d2568-213">ModelMetadataProvider</span><span class="sxs-lookup"><span data-stu-id="d2568-213">ModelMetadataProvider</span></span></strong>  |                                                                                                     <span data-ttu-id="d2568-214">提供模型中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d2568-214">Provides metadata for a model.</span></span>                                                                                                     |
| <strong><span data-ttu-id="d2568-215">ModelValidatorProvider</span><span class="sxs-lookup"><span data-stu-id="d2568-215">ModelValidatorProvider</span></span></strong> |                                                                                                   <span data-ttu-id="d2568-216">提供模型驗證程式。</span><span class="sxs-lookup"><span data-stu-id="d2568-216">Provides a validator for a model.</span></span>                                                                                                    |
|  <strong><span data-ttu-id="d2568-217">ValueProviderFactory</span><span class="sxs-lookup"><span data-stu-id="d2568-217">ValueProviderFactory</span></span></strong>  | <span data-ttu-id="d2568-218">建立值提供者。</span><span class="sxs-lookup"><span data-stu-id="d2568-218">Creates a value provider.</span></span> <span data-ttu-id="d2568-219">如需詳細資訊，請參閱 Mike Stall 的部落格文章[如何在 WebAPI 中建立的自訂值提供者](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="d2568-219">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |

<span data-ttu-id="d2568-220">若要加入多個執行個體服務的自訂實作，請呼叫**新增**或是**插入**上**Services**集合：</span><span class="sxs-lookup"><span data-stu-id="d2568-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="d2568-221">若要使用的自訂實作取代單一執行個體服務，請呼叫**取代**上**服務**集合：</span><span class="sxs-lookup"><span data-stu-id="d2568-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="d2568-222">每個控制站設定</span><span class="sxs-lookup"><span data-stu-id="d2568-222">Per-Controller Configuration</span></span>

<span data-ttu-id="d2568-223">您可以覆寫每個控制器為基礎的下列設定：</span><span class="sxs-lookup"><span data-stu-id="d2568-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="d2568-224">媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="d2568-224">Media-type formatters</span></span>
- <span data-ttu-id="d2568-225">參數繫結規則</span><span class="sxs-lookup"><span data-stu-id="d2568-225">Parameter binding rules</span></span>
- <span data-ttu-id="d2568-226">服務</span><span class="sxs-lookup"><span data-stu-id="d2568-226">Services</span></span>

<span data-ttu-id="d2568-227">若要這樣做，請定義自訂屬性，以實作**IControllerConfiguration**介面。</span><span class="sxs-lookup"><span data-stu-id="d2568-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="d2568-228">然後將屬性套用至控制器中。</span><span class="sxs-lookup"><span data-stu-id="d2568-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="d2568-229">下列範例會以自訂格式器取代預設媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="d2568-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="d2568-230">**IControllerConfiguration.Initialize**方法採用兩個參數：</span><span class="sxs-lookup"><span data-stu-id="d2568-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="d2568-231">**HttpControllerSettings**物件</span><span class="sxs-lookup"><span data-stu-id="d2568-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="d2568-232">**HttpControllerDescriptor**物件</span><span class="sxs-lookup"><span data-stu-id="d2568-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="d2568-233">**HttpControllerDescriptor**包含控制器，您可以檢查僅供參考之用 （例如，若要區別兩個控制站） 的描述。</span><span class="sxs-lookup"><span data-stu-id="d2568-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="d2568-234">使用**HttpControllerSettings**設定控制站的物件。</span><span class="sxs-lookup"><span data-stu-id="d2568-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="d2568-235">此物件包含您可以覆寫每個控制器為基礎的組態參數的子集。</span><span class="sxs-lookup"><span data-stu-id="d2568-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="d2568-236">您不會變更任何設定預設為全域**HttpConfiguration**物件。</span><span class="sxs-lookup"><span data-stu-id="d2568-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
