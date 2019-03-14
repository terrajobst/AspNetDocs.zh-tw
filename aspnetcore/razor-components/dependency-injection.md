---
title: Razor 元件相依性插入
author: guardrex
description: 請參閱 Blazor 和 Razor 元件的應用程式如何使用內建服務，方法是讓它們插入至元件。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 6ce8fa74f20145f48797d267c20ef2593368b941
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042425"
---
# <a name="razor-components-dependency-injection"></a><span data-ttu-id="d40e7-103">Razor 元件相依性插入</span><span class="sxs-lookup"><span data-stu-id="d40e7-103">Razor Components dependency injection</span></span>

<span data-ttu-id="d40e7-104">藉由[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="d40e7-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="d40e7-105">[相依性插入 (DI)](/aspnet/core/fundamentals/dependency-injection)是內建功能。</span><span class="sxs-lookup"><span data-stu-id="d40e7-105">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection) is built-in.</span></span> <span data-ttu-id="d40e7-106">應用程式可以使用內建的服務，方法是讓它們插入至元件。</span><span class="sxs-lookup"><span data-stu-id="d40e7-106">Apps can use built-in services by having them injected into components.</span></span> <span data-ttu-id="d40e7-107">應用程式也可以定義自訂的服務，並使其可透過 DI。</span><span class="sxs-lookup"><span data-stu-id="d40e7-107">Apps can also define custom services and make them available via DI.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="d40e7-108">相依性插入</span><span class="sxs-lookup"><span data-stu-id="d40e7-108">Dependency injection</span></span>

<span data-ttu-id="d40e7-109">DI 是一種技術來存取中央位置中所設定的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-109">DI is a technique for accessing services configured in a central location.</span></span> <span data-ttu-id="d40e7-110">這可能是很有用：</span><span class="sxs-lookup"><span data-stu-id="d40e7-110">This can be useful to:</span></span>

* <span data-ttu-id="d40e7-111">許多元件之間共用的服務類別的單一執行個體 (稱為*singleton*服務)。</span><span class="sxs-lookup"><span data-stu-id="d40e7-111">Share a single instance of a service class across many components (known as a *singleton* service).</span></span>
* <span data-ttu-id="d40e7-112">分離從特定的具象服務類別的元件，並只能參考抽象概念。</span><span class="sxs-lookup"><span data-stu-id="d40e7-112">Decouple components from particular concrete service classes and only reference abstractions.</span></span> <span data-ttu-id="d40e7-113">例如，介面`IDataAccess`由具象類別實作`DataAccess`。</span><span class="sxs-lookup"><span data-stu-id="d40e7-113">For example, an interface `IDataAccess` is implemented by a concrete class `DataAccess`.</span></span> <span data-ttu-id="d40e7-114">當元件會使用 DI 來接收`IDataAccess`元件的實作不具象型別結合。</span><span class="sxs-lookup"><span data-stu-id="d40e7-114">When a component uses DI to receive an `IDataAccess` implementation, the component isn't coupled to the concrete type.</span></span> <span data-ttu-id="d40e7-115">實作可以交換，或許在單元測試中模擬 （mock） 實作。</span><span class="sxs-lookup"><span data-stu-id="d40e7-115">The implementation can be swapped, perhaps to a mock implementation in unit tests.</span></span>

<span data-ttu-id="d40e7-116">DI 系統負責提供服務給元件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d40e7-116">The DI system is responsible for supplying instances of services to components.</span></span> <span data-ttu-id="d40e7-117">DI 會也會解析相依性以遞迴方式，讓服務本身可能會相依於其他服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-117">DI also resolves dependencies recursively so that services themselves can depend on further services.</span></span> <span data-ttu-id="d40e7-118">DI 的應用程式啟動期間設定。</span><span class="sxs-lookup"><span data-stu-id="d40e7-118">DI is configured during startup of the app.</span></span> <span data-ttu-id="d40e7-119">範例是本主題稍後所示。</span><span class="sxs-lookup"><span data-stu-id="d40e7-119">An example is shown later in this topic.</span></span>

## <a name="add-services-to-di"></a><span data-ttu-id="d40e7-120">將服務新增至 DI</span><span class="sxs-lookup"><span data-stu-id="d40e7-120">Add services to DI</span></span>

<span data-ttu-id="d40e7-121">建立新的應用程式之後, 檢查`Startup.ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="d40e7-121">After creating a new app, examine the `Startup.ConfigureServices` method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

<span data-ttu-id="d40e7-122">`ConfigureServices`傳遞給方法[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)，這是一份服務描述元物件 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor))。</span><span class="sxs-lookup"><span data-stu-id="d40e7-122">The `ConfigureServices` method is passed an [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), which is a list of service descriptor objects ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span></span> <span data-ttu-id="d40e7-123">服務會藉由提供服務集合的服務描述元加入。</span><span class="sxs-lookup"><span data-stu-id="d40e7-123">Services are added by providing service descriptors to the service collection.</span></span> <span data-ttu-id="d40e7-124">下列程式碼範例示範概念：</span><span class="sxs-lookup"><span data-stu-id="d40e7-124">The following code sample demonstrates the concept:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

<span data-ttu-id="d40e7-125">服務可以使用下列存留期來設定：</span><span class="sxs-lookup"><span data-stu-id="d40e7-125">Services can be configured with the following lifetimes:</span></span>

| <span data-ttu-id="d40e7-126">方法</span><span class="sxs-lookup"><span data-stu-id="d40e7-126">Method</span></span>      | <span data-ttu-id="d40e7-127">描述</span><span class="sxs-lookup"><span data-stu-id="d40e7-127">Description</span></span> |
| ----------- | ----------- |
| [<span data-ttu-id="d40e7-128">單一</span><span class="sxs-lookup"><span data-stu-id="d40e7-128">Singleton</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | <span data-ttu-id="d40e7-129">建立 DI*單一執行個體*的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-129">DI creates a *single instance* of the service.</span></span> <span data-ttu-id="d40e7-130">需要這項服務的所有元件會都接收到這個執行個體的參考。</span><span class="sxs-lookup"><span data-stu-id="d40e7-130">All components requiring this service receive a reference to this instance.</span></span> |
| [<span data-ttu-id="d40e7-131">暫時性</span><span class="sxs-lookup"><span data-stu-id="d40e7-131">Transient</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | <span data-ttu-id="d40e7-132">每當有元件需要這項服務，它會接收*新執行個體*的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-132">Whenever a component requires this service, it receives a *new instance* of the service.</span></span> |
| [<span data-ttu-id="d40e7-133">具範圍</span><span class="sxs-lookup"><span data-stu-id="d40e7-133">Scoped</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | <span data-ttu-id="d40e7-134">用戶端 Blazor 目前沒有 DI 領域的概念。</span><span class="sxs-lookup"><span data-stu-id="d40e7-134">Client-side Blazor doesn't currently have the concept of DI scopes.</span></span> <span data-ttu-id="d40e7-135">`Scoped` 行為類似`Singleton`。</span><span class="sxs-lookup"><span data-stu-id="d40e7-135">`Scoped` behaves like `Singleton`.</span></span> <span data-ttu-id="d40e7-136">不過，ASP.NET Core Razor 元件支援`Scoped`存留期。</span><span class="sxs-lookup"><span data-stu-id="d40e7-136">However, ASP.NET Core Razor Components support the `Scoped` lifetime.</span></span> <span data-ttu-id="d40e7-137">在 Razor 元件中，連接範圍已設定領域的服務註冊。</span><span class="sxs-lookup"><span data-stu-id="d40e7-137">In a Razor Component, a scoped service registration is scoped to the connection.</span></span> <span data-ttu-id="d40e7-138">基於這個理由，若要使用已設定領域的服務是慣用的服務，應受限於目前的使用者 (即使目前的目的是要執行用戶端瀏覽器中)。</span><span class="sxs-lookup"><span data-stu-id="d40e7-138">For this reason, using scoped services is preferred for services that should be scoped to the current user (even if the current intent is to run client-side in the browser).</span></span> |

<span data-ttu-id="d40e7-139">DI 系統是以 ASP.NET Core 中的 DI 系統為基礎。</span><span class="sxs-lookup"><span data-stu-id="d40e7-139">The DI system is based on the DI system in ASP.NET Core.</span></span> <span data-ttu-id="d40e7-140">如需詳細資訊，請參閱 < [ASP.NET Core 中的相依性插入](/aspnet/core/fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="d40e7-140">For more information, see [Dependency injection in ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).</span></span>

## <a name="default-services"></a><span data-ttu-id="d40e7-141">預設服務</span><span class="sxs-lookup"><span data-stu-id="d40e7-141">Default services</span></span>

<span data-ttu-id="d40e7-142">預設的服務會自動新增至應用程式的服務集合。</span><span class="sxs-lookup"><span data-stu-id="d40e7-142">Default services are automatically added to the service collection of an app.</span></span> <span data-ttu-id="d40e7-143">下表顯示一些實用的預設提供的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-143">The following table shows some of the useful default services provided.</span></span>

| <span data-ttu-id="d40e7-144">方法</span><span class="sxs-lookup"><span data-stu-id="d40e7-144">Method</span></span>       | <span data-ttu-id="d40e7-145">描述</span><span class="sxs-lookup"><span data-stu-id="d40e7-145">Description</span></span> |
| ------------ | ----------- |
| [<span data-ttu-id="d40e7-146">HttpClient</span><span class="sxs-lookup"><span data-stu-id="d40e7-146">HttpClient</span></span>](/dotnet/api/system.net.http.httpclient) | <span data-ttu-id="d40e7-147">提供方法來傳送 HTTP 要求，以及從 URI (singleton) 所識別的資源接收 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="d40e7-147">Provides methods for sending HTTP requests and receiving HTTP responses from a resource identified by a URI (singleton).</span></span> <span data-ttu-id="d40e7-148">請注意，這個執行個體`HttpClient`處理 HTTP 流量，在背景中的使用瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d40e7-148">Note that this instance of `HttpClient` uses the browser for handling the HTTP traffic in the background.</span></span> <span data-ttu-id="d40e7-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress)會自動設為應用程式的基底 URI 前置詞。</span><span class="sxs-lookup"><span data-stu-id="d40e7-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) is automatically set to the base URI prefix of the app.</span></span> <span data-ttu-id="d40e7-150">`HttpClient` 僅提供給用戶端 Blazor 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d40e7-150">`HttpClient` is only provided to client-side Blazor apps.</span></span> |
| `IJSRuntime` | <span data-ttu-id="d40e7-151">表示可能會分派呼叫的 JavaScript 執行階段的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d40e7-151">Represents an instance of a JavaScript runtime to which calls may be dispatched.</span></span> <span data-ttu-id="d40e7-152">如需詳細資訊，請參閱<xref:razor-components/javascript-interop>。</span><span class="sxs-lookup"><span data-stu-id="d40e7-152">For more information, see <xref:razor-components/javascript-interop>.</span></span> |
| `IUriHelper` | <span data-ttu-id="d40e7-153">使用 Uri 和瀏覽狀態 (singleton) 的協助程式。</span><span class="sxs-lookup"><span data-stu-id="d40e7-153">Helpers for working with URIs and navigation state (singleton).</span></span> <span data-ttu-id="d40e7-154">`IUriHelper` 會提供給這兩個用戶端 Blazor 和 ASP.NET Core Razor 元件應用程式。</span><span class="sxs-lookup"><span data-stu-id="d40e7-154">`IUriHelper` is provided to both client-side Blazor and ASP.NET Core Razor Components apps.</span></span> |

<span data-ttu-id="d40e7-155">請注意，就可以使用自訂服務提供者，而預設的服務提供者新增的預設範本。</span><span class="sxs-lookup"><span data-stu-id="d40e7-155">Note that it is possible to use a custom services provider instead of the default service provider that's added by the default template.</span></span> <span data-ttu-id="d40e7-156">自訂服務提供者不會自動提供資料表中列出的預設服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-156">A custom service provider doesn't automatically provide the default services listed in the table.</span></span> <span data-ttu-id="d40e7-157">這些服務必須明確地新增至新的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="d40e7-157">Those services must be added to the new service provider explicitly.</span></span>

## <a name="request-a-service-in-a-component"></a><span data-ttu-id="d40e7-158">要求中元件的服務</span><span class="sxs-lookup"><span data-stu-id="d40e7-158">Request a service in a component</span></span>

<span data-ttu-id="d40e7-159">一旦服務加入至服務集合，它們可以插入至元件的 Razor 範本使用`@inject`Razor 指示詞。</span><span class="sxs-lookup"><span data-stu-id="d40e7-159">Once services are added to the service collection, they can be injected into the components' Razor templates using the `@inject` Razor directive.</span></span> <span data-ttu-id="d40e7-160">`@inject` 有兩個參數：</span><span class="sxs-lookup"><span data-stu-id="d40e7-160">`@inject` has two parameters:</span></span>

* <span data-ttu-id="d40e7-161">類型名稱：要插入的服務型別。</span><span class="sxs-lookup"><span data-stu-id="d40e7-161">Type name: The type of the service to inject.</span></span>
* <span data-ttu-id="d40e7-162">屬性名稱：接收插入應用程式服務的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="d40e7-162">Property name: The name of the property receiving the injected app service.</span></span> <span data-ttu-id="d40e7-163">請注意，屬性不需要手動建立。</span><span class="sxs-lookup"><span data-stu-id="d40e7-163">Note that the property doesn't require manual creation.</span></span> <span data-ttu-id="d40e7-164">編譯器會建立屬性。</span><span class="sxs-lookup"><span data-stu-id="d40e7-164">The compiler creates the property.</span></span>

<span data-ttu-id="d40e7-165">多個`@inject`陳述式可用來插入不同的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-165">Multiple `@inject` statements can be used to inject different services.</span></span>

<span data-ttu-id="d40e7-166">下列範例示範如何使用 `@inject`。</span><span class="sxs-lookup"><span data-stu-id="d40e7-166">The following example shows how to use `@inject`.</span></span> <span data-ttu-id="d40e7-167">服務實作`Services.IDataAccess`元件的屬性不會插入`DataRepository`。</span><span class="sxs-lookup"><span data-stu-id="d40e7-167">The service implementing `Services.IDataAccess` is injected into the component's property `DataRepository`.</span></span> <span data-ttu-id="d40e7-168">請注意程式碼方式只使用`IDataAccess`抽象概念：</span><span class="sxs-lookup"><span data-stu-id="d40e7-168">Note how the code is only using the `IDataAccess` abstraction:</span></span>

```csharp
@page "/customer-list"
@using Services
@inject IDataAccess DataRepository

<ul>
    @if (Customers != null)
    {
        @foreach (var customer in Customers)
        {
            <li>@customer.FirstName @customer.LastName</li>
        }
    }
</ul>

@functions {
    private IReadOnlyList<Customer> Customers;

    protected override async Task OnInitAsync()
    {
        // The property DataRepository received an implementation
        // of IDataAccess through dependency injection. Use 
        // DataRepository to obtain data from the server.
        Customers = await DataRepository.GetAllCustomersAsync();
    }
}
```

<span data-ttu-id="d40e7-169">就內部而言，產生的屬性 (`DataRepository`) 以裝飾`InjectAttribute`屬性。</span><span class="sxs-lookup"><span data-stu-id="d40e7-169">Internally, the generated property (`DataRepository`) is decorated with the `InjectAttribute` attribute.</span></span> <span data-ttu-id="d40e7-170">一般而言，這個屬性不是直接使用。</span><span class="sxs-lookup"><span data-stu-id="d40e7-170">Typically, this attribute isn't used directly.</span></span> <span data-ttu-id="d40e7-171">如果基底類別是必要元件，而且插入的屬性也是必要的基底類別，如`InjectAttribute`可以手動新增：</span><span class="sxs-lookup"><span data-stu-id="d40e7-171">If a base class is required for components and injected properties are also required for the base class, `InjectAttribute` can be manually added:</span></span>

```csharp
public class ComponentBase : BlazorComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

<span data-ttu-id="d40e7-172">在衍生自基底類別中，元件`@inject`指示詞不需要。</span><span class="sxs-lookup"><span data-stu-id="d40e7-172">In components derived from the base class, the `@inject` directive isn't required.</span></span> <span data-ttu-id="d40e7-173">`InjectAttribute`基底類別已足夠：</span><span class="sxs-lookup"><span data-stu-id="d40e7-173">The `InjectAttribute` of the base class is sufficient:</span></span>

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a><span data-ttu-id="d40e7-174">在服務中的相依性插入</span><span class="sxs-lookup"><span data-stu-id="d40e7-174">Dependency injection in services</span></span>

<span data-ttu-id="d40e7-175">複雜的服務可能需要額外的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-175">Complex services might require additional services.</span></span> <span data-ttu-id="d40e7-176">在先前範例中，`DataAccess`可能需要`HttpClient`預設服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-176">In the prior example, `DataAccess` might require the `HttpClient` default service.</span></span> <span data-ttu-id="d40e7-177">`@inject` 或`InjectAttribute`不能在服務中。</span><span class="sxs-lookup"><span data-stu-id="d40e7-177">`@inject` or the `InjectAttribute` can't be used in services.</span></span> <span data-ttu-id="d40e7-178">*建構函式插入*必須改為使用。</span><span class="sxs-lookup"><span data-stu-id="d40e7-178">*Constructor injection* must be used instead.</span></span> <span data-ttu-id="d40e7-179">將參數加入至服務的建構函式時，會新增必要的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-179">Required services are added by adding parameters to the service's constructor.</span></span> <span data-ttu-id="d40e7-180">當相依性插入建立服務時，它會辨識它需要在建構函式，並據以提供它們的服務。</span><span class="sxs-lookup"><span data-stu-id="d40e7-180">When dependency injection creates the service, it recognizes the services it requires in the constructor and provides them accordingly.</span></span>

<span data-ttu-id="d40e7-181">下列程式碼範例示範概念：</span><span class="sxs-lookup"><span data-stu-id="d40e7-181">The following code sample demonstrates the concept:</span></span>

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
    ...
}
```

<span data-ttu-id="d40e7-182">請注意下列必要條件，如建構函式插入：</span><span class="sxs-lookup"><span data-stu-id="d40e7-182">Note the following prerequisites for constructor injection:</span></span>

* <span data-ttu-id="d40e7-183">必須要有一個建構函式，其引數可以而完成的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="d40e7-183">There must be one constructor whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="d40e7-184">請注意，如果會為它們指定預設值允許使用未涵蓋的 DI 的其他參數。</span><span class="sxs-lookup"><span data-stu-id="d40e7-184">Note that additional parameters not covered by DI are allowed if default values are specified for them.</span></span>
* <span data-ttu-id="d40e7-185">適用的建構函式必須是*公開*。</span><span class="sxs-lookup"><span data-stu-id="d40e7-185">The applicable constructor must be *public*.</span></span>
* <span data-ttu-id="d40e7-186">只能有一個適用的建構函式。</span><span class="sxs-lookup"><span data-stu-id="d40e7-186">There must only be one applicable constructor.</span></span> <span data-ttu-id="d40e7-187">發生模稜兩可，DI 會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d40e7-187">In case of an ambiguity, DI throws an exception.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d40e7-188">其他資源</span><span class="sxs-lookup"><span data-stu-id="d40e7-188">Additional resources</span></span>

* [<span data-ttu-id="d40e7-189">ASP.NET Core 中的相依性插入</span><span class="sxs-lookup"><span data-stu-id="d40e7-189">Dependency injection in ASP.NET Core</span></span>](/aspnet/core/fundamentals/dependency-injection)
