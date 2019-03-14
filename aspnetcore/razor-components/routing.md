---
title: 路由的 razor 元件
author: guardrex
description: 了解如何在應用程式及有關 NavLink 元件，將要求路由傳送。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/01/2019
uid: razor-components/routing
ms.openlocfilehash: 5c648ba1bb3846f5baa515e808a98a3b33f81438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031605"
---
# <a name="razor-components-routing"></a><span data-ttu-id="1192b-103">路由的 razor 元件</span><span class="sxs-lookup"><span data-stu-id="1192b-103">Razor Components routing</span></span>

<span data-ttu-id="1192b-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="1192b-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="1192b-105">了解如何在應用程式及有關 NavLink 元件，將要求路由傳送。</span><span class="sxs-lookup"><span data-stu-id="1192b-105">Learn how to route requests in apps and about the NavLink component.</span></span>

<span data-ttu-id="1192b-106">[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([如何下載](xref:index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="1192b-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="1192b-107">請參閱[入門](xref:razor-components/get-started)主題，以取得必要條件。</span><span class="sxs-lookup"><span data-stu-id="1192b-107">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

## <a name="route-templates"></a><span data-ttu-id="1192b-108">路由範本</span><span class="sxs-lookup"><span data-stu-id="1192b-108">Route templates</span></span>

<span data-ttu-id="1192b-109">`<Router>`元件可讓路由和路由範本會提供給每個可存取的元件。</span><span class="sxs-lookup"><span data-stu-id="1192b-109">The `<Router>` component enables routing, and a route template is provided to each accessible component.</span></span> <span data-ttu-id="1192b-110">`<Router>`元件會出現在*App.cshtml*檔案：</span><span class="sxs-lookup"><span data-stu-id="1192b-110">The `<Router>` component appears in the *App.cshtml* file:</span></span>

```cshtml
<Router AppAssembly=typeof(Program).Assembly />
```

<span data-ttu-id="1192b-111">當 *\*.cshtml*檔案`@page`編譯指示詞，指定產生的類別[RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute)指定路由範本。</span><span class="sxs-lookup"><span data-stu-id="1192b-111">When a *\*.cshtml* file with an `@page` directive is compiled, the generated class is given a [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute) specifying the route template.</span></span> <span data-ttu-id="1192b-112">在執行階段，路由器會尋找使用的元件類別`RouteAttribute`並呈現任何元件有符合所要求的 URL 的路由範本。</span><span class="sxs-lookup"><span data-stu-id="1192b-112">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="1192b-113">多個路由範本可以套用至元件。</span><span class="sxs-lookup"><span data-stu-id="1192b-113">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="1192b-114">在 [範例應用程式](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)，下列元件會回應要求`/BlazorRoute`和`/DifferentBlazorRoute`。</span><span class="sxs-lookup"><span data-stu-id="1192b-114">In the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/), the following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`.</span></span>

<span data-ttu-id="1192b-115">*Pages/BlazorRoute.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="1192b-115">*Pages/BlazorRoute.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?start=1&end=4)]

<span data-ttu-id="1192b-116">`<Router>` 支援的設定，轉譯所要求的路由時的後援元件仍未解析的。</span><span class="sxs-lookup"><span data-stu-id="1192b-116">`<Router>` supports setting a fallback component for rendering when a requested route isn't resolved.</span></span> <span data-ttu-id="1192b-117">藉由設定啟用此加入案例`FallbackComponent`後援的元件類別的型別參數。</span><span class="sxs-lookup"><span data-stu-id="1192b-117">Enable this opt-in scenario by setting the `FallbackComponent` parameter to the type of the fallback component class.</span></span>

<span data-ttu-id="1192b-118">下列範例會設定中所定義的元件*Pages/MyFallbackRazorComponent.cshtml*做為後援的元件，如`<Router>`:</span><span class="sxs-lookup"><span data-stu-id="1192b-118">The following example sets a component defined in *Pages/MyFallbackRazorComponent.cshtml* as the fallback component for a `<Router>`:</span></span>

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> <span data-ttu-id="1192b-119">若要正確地產生路由，應用程式必須包含`<base>`標記中的其*wwwroot/index.html*檔案中指定的應用程式基底路徑`href`屬性 (`<base href="/" />`)。</span><span class="sxs-lookup"><span data-stu-id="1192b-119">To generate routes properly, the app must include a `<base>` tag in its *wwwroot/index.html* file with the app base path specified in the `href` attribute (`<base href="/" />`).</span></span> <span data-ttu-id="1192b-120">如需詳細資訊，請參閱[主應用程式和部署：應用程式基底路徑](xref:host-and-deploy/razor-components/index#app-base-path)。</span><span class="sxs-lookup"><span data-stu-id="1192b-120">For more information, see [Host and deploy: App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="route-parameters"></a><span data-ttu-id="1192b-121">路由參數</span><span class="sxs-lookup"><span data-stu-id="1192b-121">Route parameters</span></span>

<span data-ttu-id="1192b-122">路由器會使用路由參數，來填入對應的元件參數具有相同的名稱 （不區分大小寫）。</span><span class="sxs-lookup"><span data-stu-id="1192b-122">The router uses route parameters to populate the corresponding component parameters with the same name (case insensitive).</span></span>

<span data-ttu-id="1192b-123">*Pages/RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="1192b-123">*Pages/RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?start=1&end=8)]

<span data-ttu-id="1192b-124">選擇性參數不支援，因此兩個`@page`指示詞會套用在上述範例中。</span><span class="sxs-lookup"><span data-stu-id="1192b-124">Optional parameters aren't supported yet, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="1192b-125">第一個允許瀏覽至不含參數的元件。</span><span class="sxs-lookup"><span data-stu-id="1192b-125">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="1192b-126">第二個`@page`指示詞會採用`{text}`路由參數，並將值指派給`Text`屬性。</span><span class="sxs-lookup"><span data-stu-id="1192b-126">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="route-constraints"></a><span data-ttu-id="1192b-127">路由條件約束</span><span class="sxs-lookup"><span data-stu-id="1192b-127">Route constraints</span></span>

<span data-ttu-id="1192b-128">路由條件約束會強制執行比對到元件的路由區段的型別。</span><span class="sxs-lookup"><span data-stu-id="1192b-128">A route constraint enforces type matching on a route segment to a component.</span></span>

<span data-ttu-id="1192b-129">在下列範例中，使用者元件的路由才會相符：</span><span class="sxs-lookup"><span data-stu-id="1192b-129">In the following example, the route to the Users component only matches if:</span></span>

* <span data-ttu-id="1192b-130">`Id`路由區段會出現在要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1192b-130">An `Id` route segment is present on the request URL.</span></span>
* <span data-ttu-id="1192b-131">`Id`區段是一個整數 (`int`)。</span><span class="sxs-lookup"><span data-stu-id="1192b-131">The `Id` segment is an integer (`int`).</span></span>

```cshtml
@page "/Users/{Id:int}"

<h1>The user Id is @Id!</h1>

@functions {
    [Parameter]
    private int Id { get; set; }
}
```

<span data-ttu-id="1192b-132">下表所示的路由條件約束可供使用。</span><span class="sxs-lookup"><span data-stu-id="1192b-132">The route constraints shown in the following table are available for use.</span></span> <span data-ttu-id="1192b-133">符合文化特性而異的路由條件約束，請參閱下方的資料表，如需詳細資訊的警告。</span><span class="sxs-lookup"><span data-stu-id="1192b-133">For the route constraints that match with the invariant culture, see the warning below the table for more information.</span></span>

| <span data-ttu-id="1192b-134">條件約束</span><span class="sxs-lookup"><span data-stu-id="1192b-134">Constraint</span></span> | <span data-ttu-id="1192b-135">範例</span><span class="sxs-lookup"><span data-stu-id="1192b-135">Example</span></span>           | <span data-ttu-id="1192b-136">範例相符項目</span><span class="sxs-lookup"><span data-stu-id="1192b-136">Example Matches</span></span>                                                                  | <span data-ttu-id="1192b-137">非變異值</span><span class="sxs-lookup"><span data-stu-id="1192b-137">Invariant</span></span><br><span data-ttu-id="1192b-138">文化特性</span><span class="sxs-lookup"><span data-stu-id="1192b-138">culture</span></span><br><span data-ttu-id="1192b-139">比對</span><span class="sxs-lookup"><span data-stu-id="1192b-139">matching</span></span> |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | <span data-ttu-id="1192b-140">`true`、 `FALSE`</span><span class="sxs-lookup"><span data-stu-id="1192b-140">`true`, `FALSE`</span></span>                                                                  | <span data-ttu-id="1192b-141">否</span><span class="sxs-lookup"><span data-stu-id="1192b-141">No</span></span>                               |
| `datetime` | `{dob:datetime}`  | <span data-ttu-id="1192b-142">`2016-12-31`、 `2016-12-31 7:32pm`</span><span class="sxs-lookup"><span data-stu-id="1192b-142">`2016-12-31`, `2016-12-31 7:32pm`</span></span>                                                | <span data-ttu-id="1192b-143">是</span><span class="sxs-lookup"><span data-stu-id="1192b-143">Yes</span></span>                              |
| `decimal`  | `{price:decimal}` | <span data-ttu-id="1192b-144">`49.99`、 `-1,000.01`</span><span class="sxs-lookup"><span data-stu-id="1192b-144">`49.99`, `-1,000.01`</span></span>                                                             | <span data-ttu-id="1192b-145">是</span><span class="sxs-lookup"><span data-stu-id="1192b-145">Yes</span></span>                              |
| `double`   | `{weight:double}` | <span data-ttu-id="1192b-146">`1.234`、 `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="1192b-146">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="1192b-147">是</span><span class="sxs-lookup"><span data-stu-id="1192b-147">Yes</span></span>                              |
| `float`    | `{weight:float}`  | <span data-ttu-id="1192b-148">`1.234`、 `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="1192b-148">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="1192b-149">是</span><span class="sxs-lookup"><span data-stu-id="1192b-149">Yes</span></span>                              |
| `guid`     | `{id:guid}`       | <span data-ttu-id="1192b-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`、 `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span><span class="sxs-lookup"><span data-stu-id="1192b-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span></span> | <span data-ttu-id="1192b-151">否</span><span class="sxs-lookup"><span data-stu-id="1192b-151">No</span></span>                               |
| `int`      | `{id:int}`        | <span data-ttu-id="1192b-152">`123456789`、 `-123456789`</span><span class="sxs-lookup"><span data-stu-id="1192b-152">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="1192b-153">是</span><span class="sxs-lookup"><span data-stu-id="1192b-153">Yes</span></span>                              |
| `long`     | `{ticks:long}`    | <span data-ttu-id="1192b-154">`123456789`、 `-123456789`</span><span class="sxs-lookup"><span data-stu-id="1192b-154">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="1192b-155">是</span><span class="sxs-lookup"><span data-stu-id="1192b-155">Yes</span></span>                              |

> [!WARNING]
> <span data-ttu-id="1192b-156">確認 URL 可以轉換成 CLR 類型的路由條件約束 (例如 `int` 或 `DateTime`) 一律使用不因國別而異的文化特性。</span><span class="sxs-lookup"><span data-stu-id="1192b-156">Route constraints that verify the URL and are converted to a CLR type (such as `int` or `DateTime`) always use the invariant culture.</span></span> <span data-ttu-id="1192b-157">這些條件約束假設 URL 不可當地語系化。</span><span class="sxs-lookup"><span data-stu-id="1192b-157">These constraints assume that the URL is non-localizable.</span></span>

## <a name="navlink-component"></a><span data-ttu-id="1192b-158">NavLink 元件</span><span class="sxs-lookup"><span data-stu-id="1192b-158">NavLink component</span></span>

<span data-ttu-id="1192b-159">使用 NavLink 元件取代 HTML  **\<>** 時建立導覽連結的項目。</span><span class="sxs-lookup"><span data-stu-id="1192b-159">Use a NavLink component in place of HTML **\<a>** elements when creating navigation links.</span></span> <span data-ttu-id="1192b-160">NavLink 元件的行為類似 **\<>** 項目，但它會切換`active`CSS 類別根據其`href`符合目前的 URL。</span><span class="sxs-lookup"><span data-stu-id="1192b-160">A NavLink component behaves like an **\<a>** element, except it toggles an `active` CSS class based on whether its `href` matches the current URL.</span></span> <span data-ttu-id="1192b-161">`active`類別可協助使用者了解哪一頁是使用中的頁面之間導覽連結顯示。</span><span class="sxs-lookup"><span data-stu-id="1192b-161">The `active` class helps a user understand which page is the active page among the navigation links displayed.</span></span>

<span data-ttu-id="1192b-162">中的 NavMenu 元件[範例應用程式](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)會建立[Bootstrap](https://getbootstrap.com/docs/)示範如何使用 NavLink 元件的瀏覽列。</span><span class="sxs-lookup"><span data-stu-id="1192b-162">The NavMenu component in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) creates a [Bootstrap](https://getbootstrap.com/docs/) nav bar that demonstrates how to use NavLink components.</span></span> <span data-ttu-id="1192b-163">下列標記會顯示在前兩個 NavLinks *Shared/NavMenu.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="1192b-163">The following markup shows the first two NavLinks in the *Shared/NavMenu.cshtml* file.</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?start=13&end=24&highlight=4-6,9-11)]

<span data-ttu-id="1192b-164">有兩個`NavLinkMatch`選項：</span><span class="sxs-lookup"><span data-stu-id="1192b-164">There are two `NavLinkMatch` options:</span></span>

* <span data-ttu-id="1192b-165">`NavLinkMatch.All` &ndash; 指定 NavLink 應該是作用中時，它會比對整個目前的 URL。</span><span class="sxs-lookup"><span data-stu-id="1192b-165">`NavLinkMatch.All` &ndash; Specifies that the NavLink should be active when it matches the entire current URL.</span></span>
* <span data-ttu-id="1192b-166">`NavLinkMatch.Prefix` &ndash; 指定 NavLink 應該作用中，當它符合目前 URL 之任何前置詞。</span><span class="sxs-lookup"><span data-stu-id="1192b-166">`NavLinkMatch.Prefix` &ndash; Specifies that the NavLink should be active when it matches any prefix of the current URL.</span></span>

<span data-ttu-id="1192b-167">在上述範例中，首頁 NavLink (`href=""`) 比對所有的 Url，並一律會收到`active`CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="1192b-167">In the preceding example, the Home NavLink (`href=""`) matches all URLs and always receives the `active` CSS class.</span></span> <span data-ttu-id="1192b-168">只會收到第二個 NavLink`active`當使用者造訪 BlazorRoute 元件類別 (`href="BlazorRoute"`)。</span><span class="sxs-lookup"><span data-stu-id="1192b-168">The second NavLink only receives the `active` class when the user visits the BlazorRoute component (`href="BlazorRoute"`).</span></span>
