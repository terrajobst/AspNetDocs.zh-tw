---
uid: signalr/overview/advanced/dependency-injection
title: SignalR 中的相依性插入 |Microsoft Docs
author: bradygaster
description: 本主題中使用的軟體版本 Visual Studio 2013 .NET 4.5 SignalR 第2版本主題的先前版本，以取得舊版的相關資訊 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537328"
---
# <a name="dependency-injection-in-signalr"></a><span data-ttu-id="eb124-103">SignalR 中的相依性插入</span><span class="sxs-lookup"><span data-stu-id="eb124-103">Dependency Injection in SignalR</span></span>

<span data-ttu-id="eb124-104">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="eb124-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="eb124-105">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="eb124-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="eb124-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="eb124-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="eb124-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="eb124-107">.NET 4.5</span></span>
> - <span data-ttu-id="eb124-108">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="eb124-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="eb124-109">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="eb124-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="eb124-110">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="eb124-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="eb124-111">問題與意見</span><span class="sxs-lookup"><span data-stu-id="eb124-111">Questions and comments</span></span>
>
> <span data-ttu-id="eb124-112">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="eb124-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="eb124-113">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="eb124-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="eb124-114">相依性插入是一種方法，可移除物件之間的硬式編碼相依性，讓您更輕鬆地取代物件的相依性，以進行測試（使用模擬物件）或變更執行時間行為。</span><span class="sxs-lookup"><span data-stu-id="eb124-114">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="eb124-115">本教學課程說明如何在 SignalR hub 上執行相依性插入。</span><span class="sxs-lookup"><span data-stu-id="eb124-115">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="eb124-116">它也會示範如何搭配 SignalR 使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="eb124-116">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="eb124-117">IoC 容器是用於相依性插入的一般架構。</span><span class="sxs-lookup"><span data-stu-id="eb124-117">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="eb124-118">什麼是相依性插入？</span><span class="sxs-lookup"><span data-stu-id="eb124-118">What is Dependency Injection?</span></span>

<span data-ttu-id="eb124-119">如果您已經熟悉相依性插入，請略過本節。</span><span class="sxs-lookup"><span data-stu-id="eb124-119">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="eb124-120">相依性*插入*（DI）是一種模式，物件不負責建立自己的相依性。</span><span class="sxs-lookup"><span data-stu-id="eb124-120">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="eb124-121">以下是激勵 DI 的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="eb124-121">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="eb124-122">假設您有一個需要記錄訊息的物件。</span><span class="sxs-lookup"><span data-stu-id="eb124-122">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="eb124-123">您可能會定義記錄介面：</span><span class="sxs-lookup"><span data-stu-id="eb124-123">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="eb124-124">在您的物件中，您可以建立 `ILogger` 來記錄訊息：</span><span class="sxs-lookup"><span data-stu-id="eb124-124">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="eb124-125">這是可行的，但不是最佳的設計。</span><span class="sxs-lookup"><span data-stu-id="eb124-125">This works, but it's not the best design.</span></span> <span data-ttu-id="eb124-126">如果您想要將 `FileLogger` 取代為另一個 `ILogger` 執行，則必須修改 `SomeComponent`。</span><span class="sxs-lookup"><span data-stu-id="eb124-126">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="eb124-127">假設有很多其他物件使用 `FileLogger`，您必須加以變更。</span><span class="sxs-lookup"><span data-stu-id="eb124-127">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="eb124-128">或者，如果您決定讓 `FileLogger` 單一，您也必須在整個應用程式中進行變更。</span><span class="sxs-lookup"><span data-stu-id="eb124-128">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="eb124-129">較好的方法是將 `ILogger` 「插入」物件，例如，藉由使用「方法」引數：</span><span class="sxs-lookup"><span data-stu-id="eb124-129">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="eb124-130">現在，物件不負責選取要使用的 `ILogger`。</span><span class="sxs-lookup"><span data-stu-id="eb124-130">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="eb124-131">您可以切換 `ILogger` 的執行，而不需要變更相依于它的物件。</span><span class="sxs-lookup"><span data-stu-id="eb124-131">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="eb124-132">此模式稱為「[函數化插入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)」。</span><span class="sxs-lookup"><span data-stu-id="eb124-132">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="eb124-133">另一個模式是 setter 插入，您可以在其中透過 setter 方法或屬性來設定相依性。</span><span class="sxs-lookup"><span data-stu-id="eb124-133">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="eb124-134">SignalR 中的簡單相依性插入</span><span class="sxs-lookup"><span data-stu-id="eb124-134">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="eb124-135">請考慮[使用 SignalR](../getting-started/tutorial-getting-started-with-signalr.md)的教學課程消費者入門的聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="eb124-135">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="eb124-136">以下是來自該應用程式的中樞類別：</span><span class="sxs-lookup"><span data-stu-id="eb124-136">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="eb124-137">假設您想要將聊天訊息儲存在伺服器上，然後再傳送它們。</span><span class="sxs-lookup"><span data-stu-id="eb124-137">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="eb124-138">您可以定義可抽象化此功能的介面，並使用 DI 將介面插入 `ChatHub` 類別。</span><span class="sxs-lookup"><span data-stu-id="eb124-138">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="eb124-139">唯一的問題是，SignalR 應用程式不會直接建立中樞;SignalR 會為您建立這些專案。</span><span class="sxs-lookup"><span data-stu-id="eb124-139">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="eb124-140">根據預設，SignalR 會預期中樞類別具有無參數的函式。</span><span class="sxs-lookup"><span data-stu-id="eb124-140">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="eb124-141">不過，您可以輕鬆地註冊函式來建立中樞實例，並使用此函數來執行 DI。</span><span class="sxs-lookup"><span data-stu-id="eb124-141">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="eb124-142">藉由呼叫**GlobalHost. DependencyResolver**註冊函式。</span><span class="sxs-lookup"><span data-stu-id="eb124-142">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="eb124-143">現在，每當 SignalR 需要建立 `ChatHub` 實例時，就會叫用這個匿名函數。</span><span class="sxs-lookup"><span data-stu-id="eb124-143">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="eb124-144">IoC 容器</span><span class="sxs-lookup"><span data-stu-id="eb124-144">IoC Containers</span></span>

<span data-ttu-id="eb124-145">先前的程式碼適用于簡單的案例。</span><span class="sxs-lookup"><span data-stu-id="eb124-145">The previous code is fine for simple cases.</span></span> <span data-ttu-id="eb124-146">但是您仍然必須撰寫下列內容：</span><span class="sxs-lookup"><span data-stu-id="eb124-146">But you still had to write this:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

<span data-ttu-id="eb124-147">在具有許多相依性的複雜應用程式中，您可能需要撰寫許多此「接線」程式碼。</span><span class="sxs-lookup"><span data-stu-id="eb124-147">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="eb124-148">這個程式碼可能很難維護，特別是當相依性已嵌套時。</span><span class="sxs-lookup"><span data-stu-id="eb124-148">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="eb124-149">這也很難進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="eb124-149">It is also hard to unit test.</span></span>

<span data-ttu-id="eb124-150">其中一個解決方案是使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="eb124-150">One solution is to use an IoC container.</span></span> <span data-ttu-id="eb124-151">IoC 容器是負責管理相依性的軟體元件。您會向容器註冊類型，然後使用容器來建立物件。</span><span class="sxs-lookup"><span data-stu-id="eb124-151">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="eb124-152">容器會自動將相依性關聯到圖形。</span><span class="sxs-lookup"><span data-stu-id="eb124-152">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="eb124-153">許多 IoC 容器也可讓您控制物件存留期和範圍之類的專案。</span><span class="sxs-lookup"><span data-stu-id="eb124-153">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="eb124-154">「IoC」代表「反轉控制」，這是架構呼叫應用程式程式碼的一般模式。</span><span class="sxs-lookup"><span data-stu-id="eb124-154">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="eb124-155">IoC 容器會為您構造物件，這會「反轉」一般控制流程。</span><span class="sxs-lookup"><span data-stu-id="eb124-155">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="eb124-156">在 SignalR 中使用 IoC 容器</span><span class="sxs-lookup"><span data-stu-id="eb124-156">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="eb124-157">聊天應用程式可能太容易受益于 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="eb124-157">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="eb124-158">相反地，讓我們來看一下[StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)範例。</span><span class="sxs-lookup"><span data-stu-id="eb124-158">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="eb124-159">StockTicker 範例會定義兩個主要類別：</span><span class="sxs-lookup"><span data-stu-id="eb124-159">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="eb124-160">`StockTickerHub`：中樞類別，它會管理用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="eb124-160">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="eb124-161">`StockTicker`：保存股票價格並定期更新它們的單一專案。</span><span class="sxs-lookup"><span data-stu-id="eb124-161">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="eb124-162">`StockTickerHub` 會保存 `StockTicker` singleton 的參考，而 `StockTicker` 則會保存 `StockTickerHub`的**IHubConnectionCoNtext**參考。</span><span class="sxs-lookup"><span data-stu-id="eb124-162">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="eb124-163">它會使用此介面與 `StockTickerHub` 實例進行通訊。</span><span class="sxs-lookup"><span data-stu-id="eb124-163">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="eb124-164">（如需詳細資訊，請參閱[使用 ASP.NET SignalR 進行伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。）</span><span class="sxs-lookup"><span data-stu-id="eb124-164">(For more information, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span></span>

<span data-ttu-id="eb124-165">我們可以使用 IoC 容器來全集這些相依性。</span><span class="sxs-lookup"><span data-stu-id="eb124-165">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="eb124-166">首先，讓我們來簡化 `StockTickerHub` 和 `StockTicker` 類別。</span><span class="sxs-lookup"><span data-stu-id="eb124-166">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="eb124-167">在下列程式碼中，我已將不需要的元件加上批註。</span><span class="sxs-lookup"><span data-stu-id="eb124-167">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="eb124-168">從 `StockTickerHub`中移除無參數的函式。</span><span class="sxs-lookup"><span data-stu-id="eb124-168">Remove the parameterless constructor from `StockTickerHub`.</span></span> <span data-ttu-id="eb124-169">相反地，我們一律會使用 DI 來建立中樞。</span><span class="sxs-lookup"><span data-stu-id="eb124-169">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="eb124-170">針對 StockTicker，移除單一實例。</span><span class="sxs-lookup"><span data-stu-id="eb124-170">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="eb124-171">稍後，我們將使用 IoC 容器來控制 StockTicker 存留期。</span><span class="sxs-lookup"><span data-stu-id="eb124-171">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="eb124-172">此外，請將此函式設為公用。</span><span class="sxs-lookup"><span data-stu-id="eb124-172">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="eb124-173">接下來，我們可以藉由建立 `StockTicker`的介面來重構程式碼。</span><span class="sxs-lookup"><span data-stu-id="eb124-173">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="eb124-174">我們將使用這個介面，將 `StockTickerHub` 與 `StockTicker` 類別分離。</span><span class="sxs-lookup"><span data-stu-id="eb124-174">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="eb124-175">Visual Studio 使這種重構變得簡單。</span><span class="sxs-lookup"><span data-stu-id="eb124-175">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="eb124-176">開啟檔案 StockTicker.cs，以滑鼠右鍵按一下 `StockTicker` 類別宣告，然後選取 [**重構**...]**解壓縮介面**。</span><span class="sxs-lookup"><span data-stu-id="eb124-176">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="eb124-177">在 [**解壓縮介面**] 對話方塊中，按一下 [**全選**]。</span><span class="sxs-lookup"><span data-stu-id="eb124-177">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="eb124-178">其他部分保留預設值。</span><span class="sxs-lookup"><span data-stu-id="eb124-178">Leave the other defaults.</span></span> <span data-ttu-id="eb124-179">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="eb124-179">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="eb124-180">Visual Studio 會建立名為 `IStockTicker`的新介面，而且也會變更 `StockTicker` 衍生自 `IStockTicker`。</span><span class="sxs-lookup"><span data-stu-id="eb124-180">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="eb124-181">開啟檔案 IStockTicker.cs，並將介面變更為 [**公用**]。</span><span class="sxs-lookup"><span data-stu-id="eb124-181">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="eb124-182">在 `StockTickerHub` 類別中，將 `StockTicker` 的兩個實例變更為 `IStockTicker`：</span><span class="sxs-lookup"><span data-stu-id="eb124-182">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="eb124-183">建立 `IStockTicker` 介面並不是絕對必要，但我想要示範 DI 如何協助減少應用程式中元件之間的耦合。</span><span class="sxs-lookup"><span data-stu-id="eb124-183">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="eb124-184">新增 Ninject 程式庫</span><span class="sxs-lookup"><span data-stu-id="eb124-184">Add the Ninject Library</span></span>

<span data-ttu-id="eb124-185">有許多適用于 .NET 的開放原始碼 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="eb124-185">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="eb124-186">在本教學課程中，我將使用[Ninject](http://www.ninject.org/)。</span><span class="sxs-lookup"><span data-stu-id="eb124-186">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="eb124-187">（其他熱門程式庫包括[Castle Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)和[StructureMap](http://docs.structuremap.net)）。</span><span class="sxs-lookup"><span data-stu-id="eb124-187">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="eb124-188">使用 NuGet 套件管理員來安裝[Ninject 程式庫](https://nuget.org/packages/Ninject/3.0.1.10)。</span><span class="sxs-lookup"><span data-stu-id="eb124-188">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="eb124-189">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**] > [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="eb124-189">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="eb124-190">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="eb124-190">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="eb124-191">取代 SignalR 相依性解析程式</span><span class="sxs-lookup"><span data-stu-id="eb124-191">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="eb124-192">若要在 SignalR 內使用 Ninject，請建立衍生自**DefaultDependencyResolver**的類別。</span><span class="sxs-lookup"><span data-stu-id="eb124-192">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="eb124-193">這個類別會覆寫**DefaultDependencyResolver**的**GetService**和**GetServices**方法。</span><span class="sxs-lookup"><span data-stu-id="eb124-193">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="eb124-194">SignalR 會呼叫這些方法，在執行時間建立各種物件，包括中樞實例，以及 SignalR 在內部使用的各種服務。</span><span class="sxs-lookup"><span data-stu-id="eb124-194">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="eb124-195">**GetService**方法會建立類型的單一實例。</span><span class="sxs-lookup"><span data-stu-id="eb124-195">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="eb124-196">覆寫此方法以呼叫 Ninject 核心的**TryGet**方法。</span><span class="sxs-lookup"><span data-stu-id="eb124-196">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="eb124-197">如果該方法傳回 null，則會切換回預設解析程式。</span><span class="sxs-lookup"><span data-stu-id="eb124-197">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="eb124-198">**GetServices**方法會建立指定之型別的物件集合。</span><span class="sxs-lookup"><span data-stu-id="eb124-198">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="eb124-199">覆寫此方法，以將來自 Ninject 的結果與預設解析程式的結果串連。</span><span class="sxs-lookup"><span data-stu-id="eb124-199">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="eb124-200">設定 Ninject 系結</span><span class="sxs-lookup"><span data-stu-id="eb124-200">Configure Ninject Bindings</span></span>

<span data-ttu-id="eb124-201">現在，我們將使用 Ninject 來宣告型別系結。</span><span class="sxs-lookup"><span data-stu-id="eb124-201">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="eb124-202">開啟您應用程式的 Startup.cs 類別（您可以根據 `readme.txt`中的套件指示手動建立，或是將驗證新增至您的專案而建立）。</span><span class="sxs-lookup"><span data-stu-id="eb124-202">Open your application's Startup.cs class (that you either created manually as per the package instructions in `readme.txt`, or that was created by adding authentication to your project).</span></span> <span data-ttu-id="eb124-203">在 `Startup.Configuration` 方法中，建立 Ninject 呼叫*核心*的 Ninject 容器。</span><span class="sxs-lookup"><span data-stu-id="eb124-203">In the `Startup.Configuration` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="eb124-204">建立自訂相依性解析程式的實例：</span><span class="sxs-lookup"><span data-stu-id="eb124-204">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="eb124-205">建立 `IStockTicker` 的系結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eb124-205">Create a binding for `IStockTicker` as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

<span data-ttu-id="eb124-206">這段程式碼會說兩件事。</span><span class="sxs-lookup"><span data-stu-id="eb124-206">This code is saying two things.</span></span> <span data-ttu-id="eb124-207">首先，每當應用程式需要 `IStockTicker`時，核心就應該建立 `StockTicker`的實例。</span><span class="sxs-lookup"><span data-stu-id="eb124-207">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="eb124-208">第二，`StockTicker` 類別應該是建立成單一物件的。</span><span class="sxs-lookup"><span data-stu-id="eb124-208">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="eb124-209">Ninject 會建立一個物件的實例，並針對每個要求傳回相同的實例。</span><span class="sxs-lookup"><span data-stu-id="eb124-209">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="eb124-210">建立**IHubConnectionCoNtext**的系結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eb124-210">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="eb124-211">此程式碼會建立一個會傳回**IHubConnection**的匿名函式。</span><span class="sxs-lookup"><span data-stu-id="eb124-211">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="eb124-212">只有在建立 `IStockTicker` 實例時， **WhenInjectedInto**方法才會告訴 Ninject 使用此函數。</span><span class="sxs-lookup"><span data-stu-id="eb124-212">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="eb124-213">原因是，SignalR 會在內部建立**IHubConnectionCoNtext**實例，而我們不想要覆寫 SignalR 建立它們的方式。</span><span class="sxs-lookup"><span data-stu-id="eb124-213">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="eb124-214">此函式僅適用于我們的 `StockTicker` 類別。</span><span class="sxs-lookup"><span data-stu-id="eb124-214">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="eb124-215">藉由新增中樞設定，將相依性解析程式傳遞至**MapSignalR**方法：</span><span class="sxs-lookup"><span data-stu-id="eb124-215">Pass the dependency resolver into the **MapSignalR** method by adding a hub configuration:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="eb124-216">使用新的參數更新範例啟動類別中的 ConfigureSignalR 方法：</span><span class="sxs-lookup"><span data-stu-id="eb124-216">Update the Startup.ConfigureSignalR method in the sample's Startup class with the new parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="eb124-217">現在 SignalR 會使用**MapSignalR**中指定的解析程式，而不是預設的解析程式。</span><span class="sxs-lookup"><span data-stu-id="eb124-217">Now SignalR will use the resolver specified in **MapSignalR**, instead of the default resolver.</span></span>

<span data-ttu-id="eb124-218">以下是 `Startup.Configuration`的完整程式代碼清單。</span><span class="sxs-lookup"><span data-stu-id="eb124-218">Here is the complete code listing for `Startup.Configuration`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

<span data-ttu-id="eb124-219">若要在 Visual Studio 中執行 StockTicker 應用程式，請按 F5。</span><span class="sxs-lookup"><span data-stu-id="eb124-219">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="eb124-220">在瀏覽器視窗中，流覽至 [`http://localhost:*port*/SignalR.Sample/StockTicker.html`]。</span><span class="sxs-lookup"><span data-stu-id="eb124-220">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="eb124-221">應用程式與之前的功能完全相同。</span><span class="sxs-lookup"><span data-stu-id="eb124-221">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="eb124-222">（如需說明，請參閱[使用 ASP.NET SignalR 的伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。）我們尚未變更此行為;只是讓程式碼更容易測試、維護和發展。</span><span class="sxs-lookup"><span data-stu-id="eb124-222">(For a description, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
