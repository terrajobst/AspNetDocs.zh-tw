---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2-ASP.NET 4.x 中的相依性插入
author: MikeWasson
description: 本教學課程說明如何將相依性插入 ASP.NET 4.x 的 ASP.NET Web API 控制器。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622602"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="7b303-103">ASP.NET Web API 2 中的相依性插入</span><span class="sxs-lookup"><span data-stu-id="7b303-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="7b303-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7b303-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7b303-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="7b303-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="7b303-106">本教學課程說明如何將相依性插入 ASP.NET Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="7b303-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7b303-107">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="7b303-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7b303-108">Web API 2</span><span class="sxs-lookup"><span data-stu-id="7b303-108">Web API 2</span></span>
> - [<span data-ttu-id="7b303-109">Unity 應用程式區塊</span><span class="sxs-lookup"><span data-stu-id="7b303-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="7b303-110">Entity Framework 6 （第5版也適用）</span><span class="sxs-lookup"><span data-stu-id="7b303-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="7b303-111">什麼是相依性插入？</span><span class="sxs-lookup"><span data-stu-id="7b303-111">What is Dependency Injection?</span></span>

<span data-ttu-id="7b303-112">「相依性」是另一個物件所需的任何物件。</span><span class="sxs-lookup"><span data-stu-id="7b303-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="7b303-113">例如，一般會定義處理資料存取的[儲存](http://martinfowler.com/eaaCatalog/repository.html)機制。</span><span class="sxs-lookup"><span data-stu-id="7b303-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="7b303-114">讓我們使用範例來說明。</span><span class="sxs-lookup"><span data-stu-id="7b303-114">Let's illustrate with an example.</span></span> <span data-ttu-id="7b303-115">首先，我們會定義領域模型：</span><span class="sxs-lookup"><span data-stu-id="7b303-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="7b303-116">以下是簡單的存放庫類別，會使用 Entity Framework 將專案儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7b303-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="7b303-117">現在，讓我們定義 Web API 控制器，以支援 `Product` 實體的 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="7b303-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="7b303-118">（為了簡單起見，我要保留 POST 和其他方法）。第一次嘗試：</span><span class="sxs-lookup"><span data-stu-id="7b303-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="7b303-119">請注意，控制器類別取決於 `ProductRepository`，而我們會讓控制器建立 `ProductRepository` 實例。</span><span class="sxs-lookup"><span data-stu-id="7b303-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="7b303-120">不過，以這種方式硬編碼相依性是不好的主意，原因有好幾個。</span><span class="sxs-lookup"><span data-stu-id="7b303-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="7b303-121">如果您想要以不同的執行取代 `ProductRepository`，您也需要修改控制器類別。</span><span class="sxs-lookup"><span data-stu-id="7b303-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="7b303-122">如果 `ProductRepository` 有相依性，您必須在控制器內設定這些相依性。</span><span class="sxs-lookup"><span data-stu-id="7b303-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="7b303-123">對於具有多個控制器的大型專案，您的設定程式碼會散佈在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="7b303-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="7b303-124">這很難進行單元測試，因為控制器是以硬式編碼方式來查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="7b303-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="7b303-125">針對單元測試，您應該使用模擬或存根存放庫，這在目前的設計中無法使用。</span><span class="sxs-lookup"><span data-stu-id="7b303-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="7b303-126">我們可以藉由將存放*庫插入控制器*來解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="7b303-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="7b303-127">首先，將 `ProductRepository` 類別重構為介面：</span><span class="sxs-lookup"><span data-stu-id="7b303-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="7b303-128">然後提供 `IProductRepository` 做為「函式」參數：</span><span class="sxs-lookup"><span data-stu-id="7b303-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="7b303-129">這個範例使用的是[函數插入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="7b303-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="7b303-130">您也可以使用*setter 插入*，您可以在其中透過 setter 方法或屬性來設定相依性。</span><span class="sxs-lookup"><span data-stu-id="7b303-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="7b303-131">但現在有問題，因為您的應用程式不會直接建立控制器。</span><span class="sxs-lookup"><span data-stu-id="7b303-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="7b303-132">Web API 會在路由要求時建立控制器，而 Web API 並不知道 `IProductRepository`的任何內容。</span><span class="sxs-lookup"><span data-stu-id="7b303-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="7b303-133">這是 Web API 相依性解析程式的來源。</span><span class="sxs-lookup"><span data-stu-id="7b303-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="7b303-134">Web API 相依性解析程式</span><span class="sxs-lookup"><span data-stu-id="7b303-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="7b303-135">Web API 會定義用來解析相依性的**IDependencyResolver**介面。</span><span class="sxs-lookup"><span data-stu-id="7b303-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="7b303-136">以下是介面的定義：</span><span class="sxs-lookup"><span data-stu-id="7b303-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="7b303-137">**IDependencyScope**介面有兩個方法：</span><span class="sxs-lookup"><span data-stu-id="7b303-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="7b303-138">**GetService**會建立一個類型的實例。</span><span class="sxs-lookup"><span data-stu-id="7b303-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="7b303-139">**GetServices**會建立指定之類型的物件集合。</span><span class="sxs-lookup"><span data-stu-id="7b303-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="7b303-140">**IDependencyResolver**方法會繼承**IDependencyScope** ，並新增**BeginScope**方法。</span><span class="sxs-lookup"><span data-stu-id="7b303-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="7b303-141">我稍後會在本教學課程中討論範圍。</span><span class="sxs-lookup"><span data-stu-id="7b303-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="7b303-142">當 Web API 建立控制器實例時，它會先呼叫**IDependencyResolver GetService**，並傳入控制器類型。</span><span class="sxs-lookup"><span data-stu-id="7b303-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="7b303-143">您可以使用此擴充性攔截來建立控制器，並解析任何相依性。</span><span class="sxs-lookup"><span data-stu-id="7b303-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="7b303-144">如果**GetService**傳回 Null，Web API 會在控制器類別上尋找無參數的函式。</span><span class="sxs-lookup"><span data-stu-id="7b303-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="7b303-145">Unity 容器的相依性解析</span><span class="sxs-lookup"><span data-stu-id="7b303-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="7b303-146">雖然您可以從頭開始撰寫完整的**IDependencyResolver**實作為，但介面其實是設計成在 Web API 與現有 IoC 容器之間做為橋樑。</span><span class="sxs-lookup"><span data-stu-id="7b303-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="7b303-147">IoC 容器是負責管理相依性的軟體元件。</span><span class="sxs-lookup"><span data-stu-id="7b303-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="7b303-148">您會向容器註冊類型，然後使用容器來建立物件。</span><span class="sxs-lookup"><span data-stu-id="7b303-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="7b303-149">容器會自動將相依性關聯到圖形。</span><span class="sxs-lookup"><span data-stu-id="7b303-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="7b303-150">許多 IoC 容器也可讓您控制物件存留期和範圍之類的專案。</span><span class="sxs-lookup"><span data-stu-id="7b303-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="7b303-151">「IoC」代表「反轉控制」，這是架構呼叫應用程式程式碼的一般模式。</span><span class="sxs-lookup"><span data-stu-id="7b303-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="7b303-152">IoC 容器會為您構造物件，這會「反轉」一般控制流程。</span><span class="sxs-lookup"><span data-stu-id="7b303-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="7b303-153">在本教學課程中，我們將使用 Microsoft 模式的[Unity](https://msdn.microsoft.com/library/ff647202.aspx) &amp; 實務。</span><span class="sxs-lookup"><span data-stu-id="7b303-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="7b303-154">（其他熱門程式庫包括[Castle Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)和[StructureMap](http://structuremap.github.io/documentation/)）。您可以使用 NuGet 套件管理員來安裝 Unity。</span><span class="sxs-lookup"><span data-stu-id="7b303-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="7b303-155">從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="7b303-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7b303-156">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="7b303-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="7b303-157">以下是包裝 Unity 容器的**IDependencyResolver**的執行。</span><span class="sxs-lookup"><span data-stu-id="7b303-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="7b303-158">如果**GetService**方法無法解析類型，它應該會傳回**null**。</span><span class="sxs-lookup"><span data-stu-id="7b303-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="7b303-159">如果**GetServices**方法無法解析類型，它應該會傳回空的集合物件。</span><span class="sxs-lookup"><span data-stu-id="7b303-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="7b303-160">不擲回未知類型的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7b303-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="7b303-161">設定相依性解析程式</span><span class="sxs-lookup"><span data-stu-id="7b303-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="7b303-162">在全域**HttpConfiguration**物件的**DependencyResolver**屬性上設定相依性解析程式。</span><span class="sxs-lookup"><span data-stu-id="7b303-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="7b303-163">下列程式碼會向 Unity 註冊 `IProductRepository` 介面，然後建立 `UnityResolver`。</span><span class="sxs-lookup"><span data-stu-id="7b303-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="7b303-164">相依性範圍和控制器存留期</span><span class="sxs-lookup"><span data-stu-id="7b303-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="7b303-165">系統會針對每個要求建立控制器。</span><span class="sxs-lookup"><span data-stu-id="7b303-165">Controllers are created per request.</span></span> <span data-ttu-id="7b303-166">為了管理物件存留期， **IDependencyResolver**會使用*範圍*的概念。</span><span class="sxs-lookup"><span data-stu-id="7b303-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="7b303-167">附加至**HttpConfiguration**物件的相依性解析程式具有全域範圍。</span><span class="sxs-lookup"><span data-stu-id="7b303-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="7b303-168">當 Web API 建立控制器時，它會呼叫**BeginScope**。</span><span class="sxs-lookup"><span data-stu-id="7b303-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="7b303-169">這個方法會傳回代表子範圍的**IDependencyScope** 。</span><span class="sxs-lookup"><span data-stu-id="7b303-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="7b303-170">然後，Web API 會在子範圍上呼叫**GetService**來建立控制器。</span><span class="sxs-lookup"><span data-stu-id="7b303-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="7b303-171">當要求完成時，Web API 會呼叫子範圍的**Dispose** 。</span><span class="sxs-lookup"><span data-stu-id="7b303-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="7b303-172">使用**dispose**方法來處置控制器的相依性。</span><span class="sxs-lookup"><span data-stu-id="7b303-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="7b303-173">您執行**BeginScope**的方式取決於 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="7b303-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="7b303-174">針對 Unity，範圍會對應至子容器：</span><span class="sxs-lookup"><span data-stu-id="7b303-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="7b303-175">大部分的 IoC 容器都有類似的對應專案。</span><span class="sxs-lookup"><span data-stu-id="7b303-175">Most IoC containers have similar equivalents.</span></span>
