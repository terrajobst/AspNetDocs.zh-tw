---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR 1.x 中的相依性插入 |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536950"
---
# <a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="f4a89-102">SignalR 1.x 中的相依性插入</span><span class="sxs-lookup"><span data-stu-id="f4a89-102">Dependency Injection in SignalR 1.x</span></span>

<span data-ttu-id="f4a89-103">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="f4a89-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="f4a89-104">相依性插入是一種方法，可移除物件之間的硬式編碼相依性，讓您更輕鬆地取代物件的相依性，以進行測試（使用模擬物件）或變更執行時間行為。</span><span class="sxs-lookup"><span data-stu-id="f4a89-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="f4a89-105">本教學課程說明如何在 SignalR hub 上執行相依性插入。</span><span class="sxs-lookup"><span data-stu-id="f4a89-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="f4a89-106">它也會示範如何搭配 SignalR 使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="f4a89-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="f4a89-107">IoC 容器是用於相依性插入的一般架構。</span><span class="sxs-lookup"><span data-stu-id="f4a89-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="f4a89-108">什麼是相依性插入？</span><span class="sxs-lookup"><span data-stu-id="f4a89-108">What is Dependency Injection?</span></span>

<span data-ttu-id="f4a89-109">如果您已經熟悉相依性插入，請略過本節。</span><span class="sxs-lookup"><span data-stu-id="f4a89-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="f4a89-110">相依性*插入*（DI）是一種模式，物件不負責建立自己的相依性。</span><span class="sxs-lookup"><span data-stu-id="f4a89-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="f4a89-111">以下是激勵 DI 的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="f4a89-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="f4a89-112">假設您有一個需要記錄訊息的物件。</span><span class="sxs-lookup"><span data-stu-id="f4a89-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="f4a89-113">您可能會定義記錄介面：</span><span class="sxs-lookup"><span data-stu-id="f4a89-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="f4a89-114">在您的物件中，您可以建立 `ILogger` 來記錄訊息：</span><span class="sxs-lookup"><span data-stu-id="f4a89-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="f4a89-115">這是可行的，但不是最佳的設計。</span><span class="sxs-lookup"><span data-stu-id="f4a89-115">This works, but it's not the best design.</span></span> <span data-ttu-id="f4a89-116">如果您想要將 `FileLogger` 取代為另一個 `ILogger` 執行，則必須修改 `SomeComponent`。</span><span class="sxs-lookup"><span data-stu-id="f4a89-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="f4a89-117">假設有很多其他物件使用 `FileLogger`，您必須加以變更。</span><span class="sxs-lookup"><span data-stu-id="f4a89-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="f4a89-118">或者，如果您決定讓 `FileLogger` 單一，您也必須在整個應用程式中進行變更。</span><span class="sxs-lookup"><span data-stu-id="f4a89-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="f4a89-119">較好的方法是將 `ILogger` 「插入」物件，例如，藉由使用「方法」引數：</span><span class="sxs-lookup"><span data-stu-id="f4a89-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="f4a89-120">現在，物件不負責選取要使用的 `ILogger`。</span><span class="sxs-lookup"><span data-stu-id="f4a89-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="f4a89-121">您可以切換 `ILogger` 的執行，而不需要變更相依于它的物件。</span><span class="sxs-lookup"><span data-stu-id="f4a89-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="f4a89-122">此模式稱為「[函數化插入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)」。</span><span class="sxs-lookup"><span data-stu-id="f4a89-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="f4a89-123">另一個模式是 setter 插入，您可以在其中透過 setter 方法或屬性來設定相依性。</span><span class="sxs-lookup"><span data-stu-id="f4a89-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="f4a89-124">SignalR 中的簡單相依性插入</span><span class="sxs-lookup"><span data-stu-id="f4a89-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="f4a89-125">請考慮[使用 SignalR](../getting-started/tutorial-getting-started-with-signalr.md)的教學課程消費者入門的聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="f4a89-126">以下是來自該應用程式的中樞類別：</span><span class="sxs-lookup"><span data-stu-id="f4a89-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="f4a89-127">假設您想要將聊天訊息儲存在伺服器上，然後再傳送它們。</span><span class="sxs-lookup"><span data-stu-id="f4a89-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="f4a89-128">您可以定義可抽象化此功能的介面，並使用 DI 將介面插入 `ChatHub` 類別。</span><span class="sxs-lookup"><span data-stu-id="f4a89-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="f4a89-129">唯一的問題是，SignalR 應用程式不會直接建立中樞;SignalR 會為您建立這些專案。</span><span class="sxs-lookup"><span data-stu-id="f4a89-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="f4a89-130">根據預設，SignalR 會預期中樞類別具有無參數的函式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="f4a89-131">不過，您可以輕鬆地註冊函式來建立中樞實例，並使用此函數來執行 DI。</span><span class="sxs-lookup"><span data-stu-id="f4a89-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="f4a89-132">藉由呼叫**GlobalHost. DependencyResolver**註冊函式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="f4a89-133">現在，每當 SignalR 需要建立 `ChatHub` 實例時，就會叫用這個匿名函數。</span><span class="sxs-lookup"><span data-stu-id="f4a89-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="f4a89-134">IoC 容器</span><span class="sxs-lookup"><span data-stu-id="f4a89-134">IoC Containers</span></span>

<span data-ttu-id="f4a89-135">先前的程式碼適用于簡單的案例。</span><span class="sxs-lookup"><span data-stu-id="f4a89-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="f4a89-136">但是您仍然必須撰寫下列內容：</span><span class="sxs-lookup"><span data-stu-id="f4a89-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="f4a89-137">在具有許多相依性的複雜應用程式中，您可能需要撰寫許多此「接線」程式碼。</span><span class="sxs-lookup"><span data-stu-id="f4a89-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="f4a89-138">這個程式碼可能很難維護，特別是當相依性已嵌套時。</span><span class="sxs-lookup"><span data-stu-id="f4a89-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="f4a89-139">這也很難進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="f4a89-139">It is also hard to unit test.</span></span>

<span data-ttu-id="f4a89-140">其中一個解決方案是使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="f4a89-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="f4a89-141">IoC 容器是負責管理相依性的軟體元件。您會向容器註冊類型，然後使用容器來建立物件。</span><span class="sxs-lookup"><span data-stu-id="f4a89-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="f4a89-142">容器會自動將相依性關聯到圖形。</span><span class="sxs-lookup"><span data-stu-id="f4a89-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="f4a89-143">許多 IoC 容器也可讓您控制物件存留期和範圍之類的專案。</span><span class="sxs-lookup"><span data-stu-id="f4a89-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="f4a89-144">「IoC」代表「反轉控制」，這是架構呼叫應用程式程式碼的一般模式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="f4a89-145">IoC 容器會為您構造物件，這會「反轉」一般控制流程。</span><span class="sxs-lookup"><span data-stu-id="f4a89-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="f4a89-146">在 SignalR 中使用 IoC 容器</span><span class="sxs-lookup"><span data-stu-id="f4a89-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="f4a89-147">聊天應用程式可能太容易受益于 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="f4a89-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="f4a89-148">相反地，讓我們來看一下[StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)範例。</span><span class="sxs-lookup"><span data-stu-id="f4a89-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="f4a89-149">StockTicker 範例會定義兩個主要類別：</span><span class="sxs-lookup"><span data-stu-id="f4a89-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="f4a89-150">`StockTickerHub`：中樞類別，它會管理用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="f4a89-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="f4a89-151">`StockTicker`：保存股票價格並定期更新它們的單一專案。</span><span class="sxs-lookup"><span data-stu-id="f4a89-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="f4a89-152">`StockTickerHub` 會保存 `StockTicker` singleton 的參考，而 `StockTicker` 則會保存 `StockTickerHub`的**IHubConnectionCoNtext**參考。</span><span class="sxs-lookup"><span data-stu-id="f4a89-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="f4a89-153">它會使用此介面與 `StockTickerHub` 實例進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f4a89-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="f4a89-154">（如需詳細資訊，請參閱[使用 ASP.NET SignalR 進行伺服器廣播](index.md)。）</span><span class="sxs-lookup"><span data-stu-id="f4a89-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="f4a89-155">我們可以使用 IoC 容器來全集這些相依性。</span><span class="sxs-lookup"><span data-stu-id="f4a89-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="f4a89-156">首先，讓我們來簡化 `StockTickerHub` 和 `StockTicker` 類別。</span><span class="sxs-lookup"><span data-stu-id="f4a89-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="f4a89-157">在下列程式碼中，我已將不需要的元件加上批註。</span><span class="sxs-lookup"><span data-stu-id="f4a89-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="f4a89-158">從 `StockTicker`中移除無參數的函式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="f4a89-159">相反地，我們一律會使用 DI 來建立中樞。</span><span class="sxs-lookup"><span data-stu-id="f4a89-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="f4a89-160">針對 StockTicker，移除單一實例。</span><span class="sxs-lookup"><span data-stu-id="f4a89-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="f4a89-161">稍後，我們將使用 IoC 容器來控制 StockTicker 存留期。</span><span class="sxs-lookup"><span data-stu-id="f4a89-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="f4a89-162">此外，請將此函式設為公用。</span><span class="sxs-lookup"><span data-stu-id="f4a89-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="f4a89-163">接下來，我們可以藉由建立 `StockTicker`的介面來重構程式碼。</span><span class="sxs-lookup"><span data-stu-id="f4a89-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="f4a89-164">我們將使用這個介面，將 `StockTickerHub` 與 `StockTicker` 類別分離。</span><span class="sxs-lookup"><span data-stu-id="f4a89-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="f4a89-165">Visual Studio 使這種重構變得簡單。</span><span class="sxs-lookup"><span data-stu-id="f4a89-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="f4a89-166">開啟檔案 StockTicker.cs，以滑鼠右鍵按一下 `StockTicker` 類別宣告，然後選取 [**重構**...]**解壓縮介面**。</span><span class="sxs-lookup"><span data-stu-id="f4a89-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="f4a89-167">在 [**解壓縮介面**] 對話方塊中，按一下 [**全選**]。</span><span class="sxs-lookup"><span data-stu-id="f4a89-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="f4a89-168">其他部分保留預設值。</span><span class="sxs-lookup"><span data-stu-id="f4a89-168">Leave the other defaults.</span></span> <span data-ttu-id="f4a89-169">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f4a89-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="f4a89-170">Visual Studio 會建立名為 `IStockTicker`的新介面，而且也會變更 `StockTicker` 衍生自 `IStockTicker`。</span><span class="sxs-lookup"><span data-stu-id="f4a89-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="f4a89-171">開啟檔案 IStockTicker.cs，並將介面變更為 [**公用**]。</span><span class="sxs-lookup"><span data-stu-id="f4a89-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="f4a89-172">在 `StockTickerHub` 類別中，將 `StockTicker` 的兩個實例變更為 `IStockTicker`：</span><span class="sxs-lookup"><span data-stu-id="f4a89-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="f4a89-173">建立 `IStockTicker` 介面並不是絕對必要，但我想要示範 DI 如何協助減少應用程式中元件之間的耦合。</span><span class="sxs-lookup"><span data-stu-id="f4a89-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="f4a89-174">新增 Ninject 程式庫</span><span class="sxs-lookup"><span data-stu-id="f4a89-174">Add the Ninject Library</span></span>

<span data-ttu-id="f4a89-175">有許多適用于 .NET 的開放原始碼 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="f4a89-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="f4a89-176">在本教學課程中，我將使用[Ninject](http://www.ninject.org/)。</span><span class="sxs-lookup"><span data-stu-id="f4a89-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="f4a89-177">（其他熱門程式庫包括[Castle Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)和[StructureMap](http://docs.structuremap.net)）。</span><span class="sxs-lookup"><span data-stu-id="f4a89-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="f4a89-178">使用 NuGet 套件管理員來安裝[Ninject 程式庫](https://nuget.org/packages/Ninject/3.0.1.10)。</span><span class="sxs-lookup"><span data-stu-id="f4a89-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="f4a89-179">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**] > [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="f4a89-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="f4a89-180">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="f4a89-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="f4a89-181">取代 SignalR 相依性解析程式</span><span class="sxs-lookup"><span data-stu-id="f4a89-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="f4a89-182">若要在 SignalR 內使用 Ninject，請建立衍生自**DefaultDependencyResolver**的類別。</span><span class="sxs-lookup"><span data-stu-id="f4a89-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="f4a89-183">這個類別會覆寫**DefaultDependencyResolver**的**GetService**和**GetServices**方法。</span><span class="sxs-lookup"><span data-stu-id="f4a89-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="f4a89-184">SignalR 會呼叫這些方法，在執行時間建立各種物件，包括中樞實例，以及 SignalR 在內部使用的各種服務。</span><span class="sxs-lookup"><span data-stu-id="f4a89-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="f4a89-185">**GetService**方法會建立類型的單一實例。</span><span class="sxs-lookup"><span data-stu-id="f4a89-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="f4a89-186">覆寫此方法以呼叫 Ninject 核心的**TryGet**方法。</span><span class="sxs-lookup"><span data-stu-id="f4a89-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="f4a89-187">如果該方法傳回 null，則會切換回預設解析程式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="f4a89-188">**GetServices**方法會建立指定之型別的物件集合。</span><span class="sxs-lookup"><span data-stu-id="f4a89-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="f4a89-189">覆寫此方法，以將來自 Ninject 的結果與預設解析程式的結果串連。</span><span class="sxs-lookup"><span data-stu-id="f4a89-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="f4a89-190">設定 Ninject 系結</span><span class="sxs-lookup"><span data-stu-id="f4a89-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="f4a89-191">現在，我們將使用 Ninject 來宣告型別系結。</span><span class="sxs-lookup"><span data-stu-id="f4a89-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="f4a89-192">開啟檔案 RegisterHubs.cs。</span><span class="sxs-lookup"><span data-stu-id="f4a89-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="f4a89-193">在 `RegisterHubs.Start` 方法中，建立 Ninject 呼叫*核心*的 Ninject 容器。</span><span class="sxs-lookup"><span data-stu-id="f4a89-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="f4a89-194">建立自訂相依性解析程式的實例：</span><span class="sxs-lookup"><span data-stu-id="f4a89-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="f4a89-195">建立 `IStockTicker` 的系結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f4a89-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="f4a89-196">這段程式碼會說兩件事。</span><span class="sxs-lookup"><span data-stu-id="f4a89-196">This code is saying two things.</span></span> <span data-ttu-id="f4a89-197">首先，每當應用程式需要 `IStockTicker`時，核心就應該建立 `StockTicker`的實例。</span><span class="sxs-lookup"><span data-stu-id="f4a89-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="f4a89-198">第二，`StockTicker` 類別應該是建立成單一物件的。</span><span class="sxs-lookup"><span data-stu-id="f4a89-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="f4a89-199">Ninject 會建立一個物件的實例，並針對每個要求傳回相同的實例。</span><span class="sxs-lookup"><span data-stu-id="f4a89-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="f4a89-200">建立**IHubConnectionCoNtext**的系結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f4a89-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="f4a89-201">此程式碼會建立一個會傳回**IHubConnection**的匿名函式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="f4a89-202">只有在建立 `IStockTicker` 實例時， **WhenInjectedInto**方法才會告訴 Ninject 使用此函數。</span><span class="sxs-lookup"><span data-stu-id="f4a89-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="f4a89-203">原因是，SignalR 會在內部建立**IHubConnectionCoNtext**實例，而我們不想要覆寫 SignalR 建立它們的方式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="f4a89-204">此函式僅適用于我們的 `StockTicker` 類別。</span><span class="sxs-lookup"><span data-stu-id="f4a89-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="f4a89-205">將相依性解析程式傳遞至**MapHubs**方法：</span><span class="sxs-lookup"><span data-stu-id="f4a89-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="f4a89-206">現在 SignalR 會使用**MapHubs**中指定的解析程式，而不是預設的解析程式。</span><span class="sxs-lookup"><span data-stu-id="f4a89-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="f4a89-207">以下是 `RegisterHubs.Start`的完整程式代碼清單。</span><span class="sxs-lookup"><span data-stu-id="f4a89-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="f4a89-208">若要在 Visual Studio 中執行 StockTicker 應用程式，請按 F5。</span><span class="sxs-lookup"><span data-stu-id="f4a89-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="f4a89-209">在瀏覽器視窗中，流覽至 [`http://localhost:*port*/SignalR.Sample/StockTicker.html`]。</span><span class="sxs-lookup"><span data-stu-id="f4a89-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="f4a89-210">應用程式與之前的功能完全相同。</span><span class="sxs-lookup"><span data-stu-id="f4a89-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="f4a89-211">（如需說明，請參閱[使用 ASP.NET SignalR 的伺服器廣播](index.md)。）我們尚未變更此行為;只是讓程式碼更容易測試、維護和發展。</span><span class="sxs-lookup"><span data-stu-id="f4a89-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
