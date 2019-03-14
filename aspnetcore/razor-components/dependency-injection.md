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
# <a name="razor-components-dependency-injection"></a>Razor 元件相依性插入

藉由[Rainer Stropek](https://www.timecockpit.com)

[相依性插入 (DI)](/aspnet/core/fundamentals/dependency-injection)是內建功能。 應用程式可以使用內建的服務，方法是讓它們插入至元件。 應用程式也可以定義自訂的服務，並使其可透過 DI。

## <a name="dependency-injection"></a>相依性插入

DI 是一種技術來存取中央位置中所設定的服務。 這可能是很有用：

* 許多元件之間共用的服務類別的單一執行個體 (稱為*singleton*服務)。
* 分離從特定的具象服務類別的元件，並只能參考抽象概念。 例如，介面`IDataAccess`由具象類別實作`DataAccess`。 當元件會使用 DI 來接收`IDataAccess`元件的實作不具象型別結合。 實作可以交換，或許在單元測試中模擬 （mock） 實作。

DI 系統負責提供服務給元件的執行個體。 DI 會也會解析相依性以遞迴方式，讓服務本身可能會相依於其他服務。 DI 的應用程式啟動期間設定。 範例是本主題稍後所示。

## <a name="add-services-to-di"></a>將服務新增至 DI

建立新的應用程式之後, 檢查`Startup.ConfigureServices`方法：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

`ConfigureServices`傳遞給方法[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)，這是一份服務描述元物件 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor))。 服務會藉由提供服務集合的服務描述元加入。 下列程式碼範例示範概念：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

服務可以使用下列存留期來設定：

| 方法      | 描述 |
| ----------- | ----------- |
| [單一](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | 建立 DI*單一執行個體*的服務。 需要這項服務的所有元件會都接收到這個執行個體的參考。 |
| [暫時性](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | 每當有元件需要這項服務，它會接收*新執行個體*的服務。 |
| [具範圍](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | 用戶端 Blazor 目前沒有 DI 領域的概念。 `Scoped` 行為類似`Singleton`。 不過，ASP.NET Core Razor 元件支援`Scoped`存留期。 在 Razor 元件中，連接範圍已設定領域的服務註冊。 基於這個理由，若要使用已設定領域的服務是慣用的服務，應受限於目前的使用者 (即使目前的目的是要執行用戶端瀏覽器中)。 |

DI 系統是以 ASP.NET Core 中的 DI 系統為基礎。 如需詳細資訊，請參閱 < [ASP.NET Core 中的相依性插入](/aspnet/core/fundamentals/dependency-injection)。

## <a name="default-services"></a>預設服務

預設的服務會自動新增至應用程式的服務集合。 下表顯示一些實用的預設提供的服務。

| 方法       | 描述 |
| ------------ | ----------- |
| [HttpClient](/dotnet/api/system.net.http.httpclient) | 提供方法來傳送 HTTP 要求，以及從 URI (singleton) 所識別的資源接收 HTTP 回應。 請注意，這個執行個體`HttpClient`處理 HTTP 流量，在背景中的使用瀏覽器。 [HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress)會自動設為應用程式的基底 URI 前置詞。 `HttpClient` 僅提供給用戶端 Blazor 應用程式。 |
| `IJSRuntime` | 表示可能會分派呼叫的 JavaScript 執行階段的執行個體。 如需詳細資訊，請參閱<xref:razor-components/javascript-interop>。 |
| `IUriHelper` | 使用 Uri 和瀏覽狀態 (singleton) 的協助程式。 `IUriHelper` 會提供給這兩個用戶端 Blazor 和 ASP.NET Core Razor 元件應用程式。 |

請注意，就可以使用自訂服務提供者，而預設的服務提供者新增的預設範本。 自訂服務提供者不會自動提供資料表中列出的預設服務。 這些服務必須明確地新增至新的服務提供者。

## <a name="request-a-service-in-a-component"></a>要求中元件的服務

一旦服務加入至服務集合，它們可以插入至元件的 Razor 範本使用`@inject`Razor 指示詞。 `@inject` 有兩個參數：

* 類型名稱：要插入的服務型別。
* 屬性名稱：接收插入應用程式服務的屬性名稱。 請注意，屬性不需要手動建立。 編譯器會建立屬性。

多個`@inject`陳述式可用來插入不同的服務。

下列範例示範如何使用 `@inject`。 服務實作`Services.IDataAccess`元件的屬性不會插入`DataRepository`。 請注意程式碼方式只使用`IDataAccess`抽象概念：

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

就內部而言，產生的屬性 (`DataRepository`) 以裝飾`InjectAttribute`屬性。 一般而言，這個屬性不是直接使用。 如果基底類別是必要元件，而且插入的屬性也是必要的基底類別，如`InjectAttribute`可以手動新增：

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

在衍生自基底類別中，元件`@inject`指示詞不需要。 `InjectAttribute`基底類別已足夠：

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a>在服務中的相依性插入

複雜的服務可能需要額外的服務。 在先前範例中，`DataAccess`可能需要`HttpClient`預設服務。 `@inject` 或`InjectAttribute`不能在服務中。 *建構函式插入*必須改為使用。 將參數加入至服務的建構函式時，會新增必要的服務。 當相依性插入建立服務時，它會辨識它需要在建構函式，並據以提供它們的服務。

下列程式碼範例示範概念：

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

請注意下列必要條件，如建構函式插入：

* 必須要有一個建構函式，其引數可以而完成的相依性插入。 請注意，如果會為它們指定預設值允許使用未涵蓋的 DI 的其他參數。
* 適用的建構函式必須是*公開*。
* 只能有一個適用的建構函式。 發生模稜兩可，DI 會擲回例外狀況。

## <a name="additional-resources"></a>其他資源

* [ASP.NET Core 中的相依性插入](/aspnet/core/fundamentals/dependency-injection)
