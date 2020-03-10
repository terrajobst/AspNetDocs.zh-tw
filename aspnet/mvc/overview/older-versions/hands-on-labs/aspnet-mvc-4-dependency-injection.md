---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 相依性插入 |Microsoft Docs
author: rick-anderson
description: 注意：此實際操作實驗室假設您有 ASP.NET MVC 和 ASP.NET MVC 4 篩選器的基本知識。 如果您之前未使用過 ASP.NET MVC 4 篩選，我們會將 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560610"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="c486f-104">ASP.NET MVC 4 相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="c486f-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="c486f-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="c486f-106">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="c486f-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="c486f-107">這個實際操作實驗室假設您有**ASP.NET mvc**和**ASP.NET mvc 4 篩選器**的基本知識。</span><span class="sxs-lookup"><span data-stu-id="c486f-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="c486f-108">如果您之前未使用過**ASP.NET mvc 4 篩選**，建議您前往**ASP.NET Mvc 自訂動作篩選實際操作**實驗室。</span><span class="sxs-lookup"><span data-stu-id="c486f-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="c486f-109">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可從[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="c486f-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="c486f-110">此實驗室的特定專案可在[ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)相依性插入中取得。</span><span class="sxs-lookup"><span data-stu-id="c486f-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="c486f-111">在面向**物件程式設計**架構中，物件會在有參與者和取用者的共同作業模型中一起工作。</span><span class="sxs-lookup"><span data-stu-id="c486f-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="c486f-112">自然地，此通訊模型會產生物件和元件之間的相依性，因而在複雜度增加時變得很容易管理。</span><span class="sxs-lookup"><span data-stu-id="c486f-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="c486f-113">![類別相依性和模型複雜度](aspnet-mvc-4-dependency-injection/_static/image1.png "類別相依性和模型複雜度")</span><span class="sxs-lookup"><span data-stu-id="c486f-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="c486f-114">*類別相依性和模型複雜度*</span><span class="sxs-lookup"><span data-stu-id="c486f-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="c486f-115">您可能已經聽說過**Factory 模式**，以及介面與使用服務之間的分離，其中用戶端物件通常負責服務位置。</span><span class="sxs-lookup"><span data-stu-id="c486f-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="c486f-116">相依性插入模式是控制反轉的特定執行。</span><span class="sxs-lookup"><span data-stu-id="c486f-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="c486f-117">**控制反轉（IoC）** 表示物件不會建立其他物件來執行其工作。</span><span class="sxs-lookup"><span data-stu-id="c486f-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="c486f-118">相反地，它們會從外部來源取得所需的物件（例如，xml 設定檔案）。</span><span class="sxs-lookup"><span data-stu-id="c486f-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="c486f-119">相依性**插入（DI）** 表示這是在沒有物件介入的情況下完成，通常是由傳遞了函式參數和設定屬性的架構元件所組成。</span><span class="sxs-lookup"><span data-stu-id="c486f-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="c486f-120">相依性插入（DI）設計模式</span><span class="sxs-lookup"><span data-stu-id="c486f-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="c486f-121">概括而言，相依性插入的目標是用戶端類別（例如*高爾夫的*物件）需要滿足介面的專案（例如*IClub*）。</span><span class="sxs-lookup"><span data-stu-id="c486f-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="c486f-122">它並不在意具體的類型（例如*WoodClub、IronClub、WedgeClub*或*PutterClub*），而是要讓其他人處理該型別（例如，不錯的*caddy*）。</span><span class="sxs-lookup"><span data-stu-id="c486f-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="c486f-123">ASP.NET MVC 中的相依性解析程式可讓您在其他地方註冊相依性邏輯（例如容器或*俱樂部袋*）。</span><span class="sxs-lookup"><span data-stu-id="c486f-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="c486f-124">![相依性插入圖表](aspnet-mvc-4-dependency-injection/_static/image2.png "相依性插入圖")</span><span class="sxs-lookup"><span data-stu-id="c486f-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="c486f-125">*相依性插入-高爾夫球比喻*</span><span class="sxs-lookup"><span data-stu-id="c486f-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="c486f-126">使用相依性插入模式和反轉控制的優點如下：</span><span class="sxs-lookup"><span data-stu-id="c486f-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="c486f-127">減少類別結合</span><span class="sxs-lookup"><span data-stu-id="c486f-127">Reduces class coupling</span></span>
- <span data-ttu-id="c486f-128">增加重複使用的程式碼</span><span class="sxs-lookup"><span data-stu-id="c486f-128">Increases code reusing</span></span>
- <span data-ttu-id="c486f-129">改善程式碼維護性</span><span class="sxs-lookup"><span data-stu-id="c486f-129">Improves code maintainability</span></span>
- <span data-ttu-id="c486f-130">改善應用程式測試</span><span class="sxs-lookup"><span data-stu-id="c486f-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="c486f-131">相依性插入有時會與抽象 Factory 設計模式進行比較，但這兩種方法之間有些許差異。</span><span class="sxs-lookup"><span data-stu-id="c486f-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="c486f-132">DI 具有一個可在後方運作的架構，藉由呼叫 factory 和已註冊的服務來解決相依性。</span><span class="sxs-lookup"><span data-stu-id="c486f-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>

<span data-ttu-id="c486f-133">既然您已瞭解相依性插入模式，您將會在整個實驗室中學習如何在 ASP.NET MVC 4 中加以套用。</span><span class="sxs-lookup"><span data-stu-id="c486f-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="c486f-134">您將開始在**控制器**中使用相依性插入，以包含資料庫存取服務。</span><span class="sxs-lookup"><span data-stu-id="c486f-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="c486f-135">接下來，您會將相依性插入套用至**Views** ，以取用服務並顯示資訊。</span><span class="sxs-lookup"><span data-stu-id="c486f-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="c486f-136">最後，您將擴充 DI 以 ASP.NET MVC 4 篩選，並在方案中插入自訂動作篩選器。</span><span class="sxs-lookup"><span data-stu-id="c486f-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="c486f-137">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="c486f-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="c486f-138">使用 NuGet 套件整合 ASP.NET MVC 4 與 Unity 以進行相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="c486f-139">在 ASP.NET MVC 控制器內使用相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="c486f-140">在 ASP.NET MVC 視圖內使用相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="c486f-141">在 ASP.NET MVC 動作篩選器內使用相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="c486f-142">此實驗室會使用 Mvc3 NuGet 套件來進行相依性解析，但是您可以調整任何相依性插入架構，以與 ASP.NET MVC 4 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c486f-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c486f-143">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c486f-143">Prerequisites</span></span>

<span data-ttu-id="c486f-144">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="c486f-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="c486f-145">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。</span><span class="sxs-lookup"><span data-stu-id="c486f-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c486f-146">安裝程式</span><span class="sxs-lookup"><span data-stu-id="c486f-146">Setup</span></span>

<span data-ttu-id="c486f-147">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="c486f-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="c486f-148">為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。</span><span class="sxs-lookup"><span data-stu-id="c486f-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="c486f-149">若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="c486f-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="c486f-150">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 B：使用程式碼片段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="c486f-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c486f-151">練習</span><span class="sxs-lookup"><span data-stu-id="c486f-151">Exercises</span></span>

<span data-ttu-id="c486f-152">這個實際操作實驗室是由下列練習所組成：</span><span class="sxs-lookup"><span data-stu-id="c486f-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="c486f-153">練習1：插入控制器</span><span class="sxs-lookup"><span data-stu-id="c486f-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="c486f-154">練習2：插入視圖</span><span class="sxs-lookup"><span data-stu-id="c486f-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="c486f-155">練習3：插入篩選</span><span class="sxs-lookup"><span data-stu-id="c486f-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="c486f-156">每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="c486f-157">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="c486f-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="c486f-158">完成此實驗室的預估時間： **30 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="c486f-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="c486f-159">練習1：插入控制器</span><span class="sxs-lookup"><span data-stu-id="c486f-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="c486f-160">在此練習中，您將瞭解如何藉由使用 NuGet 套件整合 Unity，在 ASP.NET MVC 控制器中使用相依性插入。</span><span class="sxs-lookup"><span data-stu-id="c486f-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="c486f-161">基於這個理由，您將會在 MvcMusicStore 控制器中包含服務，以將邏輯與資料存取區隔開。</span><span class="sxs-lookup"><span data-stu-id="c486f-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="c486f-162">服務會在控制器的函式中建立新的相依性，這會在**Unity**的協助下使用相依性插入來加以解析。</span><span class="sxs-lookup"><span data-stu-id="c486f-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="c486f-163">這種方法會示範如何產生較少的結合應用程式，更有彈性且更容易維護和測試。</span><span class="sxs-lookup"><span data-stu-id="c486f-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="c486f-164">您也將瞭解如何整合 ASP.NET MVC 與 Unity。</span><span class="sxs-lookup"><span data-stu-id="c486f-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="c486f-165">關於 StoreManager 服務</span><span class="sxs-lookup"><span data-stu-id="c486f-165">About StoreManager Service</span></span>

<span data-ttu-id="c486f-166">「開始」解決方案中提供的「MVC 音樂」存放區現在包含一項服務，可管理名為**StoreService**的存放區控制器資料。</span><span class="sxs-lookup"><span data-stu-id="c486f-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="c486f-167">您會在下方找到 Store 服務的執行。</span><span class="sxs-lookup"><span data-stu-id="c486f-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="c486f-168">請注意，所有方法都會傳回模型實體。</span><span class="sxs-lookup"><span data-stu-id="c486f-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="c486f-169">從開始解決方案**StoreController**現在會使用**StoreService**。</span><span class="sxs-lookup"><span data-stu-id="c486f-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="c486f-170">所有的資料參考已從**StoreController**移除，現在可以修改目前的資料存取提供者，而不需要變更任何使用**StoreService**的方法。</span><span class="sxs-lookup"><span data-stu-id="c486f-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="c486f-171">您會發現， **StoreController**實與類別的函式內的**StoreService**有相依性。</span><span class="sxs-lookup"><span data-stu-id="c486f-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="c486f-172">本練習中引進的相依性與**控制反轉**（IoC）有關。</span><span class="sxs-lookup"><span data-stu-id="c486f-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="c486f-173">**StoreController**類別的函式會接收**IStoreService**型別參數，這對於從類別內執行服務呼叫而言是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="c486f-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="c486f-174">不過， **StoreController**不會執行任何控制器必須擁有才能使用 ASP.NET MVC 的預設函式（不含任何參數）。</span><span class="sxs-lookup"><span data-stu-id="c486f-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="c486f-175">若要解決相依性，控制器必須由抽象 factory 建立（傳回指定類型之任何物件的類別）。</span><span class="sxs-lookup"><span data-stu-id="c486f-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="c486f-176">當類別嘗試建立 StoreController 而不傳送服務物件時，您會收到錯誤，因為沒有宣告無參數的函式。</span><span class="sxs-lookup"><span data-stu-id="c486f-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="c486f-177">工作 1-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c486f-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="c486f-178">在這項工作中，您將執行「開始」應用程式，其中會將服務包含在存放區控制器中，以分隔資料存取與應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="c486f-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="c486f-179">執行應用程式時，您會收到例外狀況，因為控制器服務預設不會當做參數傳遞：</span><span class="sxs-lookup"><span data-stu-id="c486f-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="c486f-180">開啟位於**Source\Ex01-Injecting Controller\Begin**的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="c486f-181">在繼續之前，您必須先下載一些遺漏的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="c486f-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c486f-182">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c486f-183">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c486f-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c486f-184">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c486f-185">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c486f-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c486f-186">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c486f-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c486f-187">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c486f-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c486f-188">按**Ctrl + F5**執行應用程式，而不進行偵測。</span><span class="sxs-lookup"><span data-stu-id="c486f-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="c486f-189">您將會收到錯誤訊息，&quot;**未針對此物件定義任何無參數的**函式&quot;：</span><span class="sxs-lookup"><span data-stu-id="c486f-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="c486f-190">![執行 ASP.NET MVC 開始應用程式時發生錯誤](aspnet-mvc-4-dependency-injection/_static/image3.png "執行 ASP.NET MVC 開始應用程式時發生錯誤")</span><span class="sxs-lookup"><span data-stu-id="c486f-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="c486f-191">*執行 ASP.NET MVC 開始應用程式時發生錯誤*</span><span class="sxs-lookup"><span data-stu-id="c486f-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="c486f-192">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c486f-192">Close the browser.</span></span>

<span data-ttu-id="c486f-193">在下列步驟中，您將使用「音樂存放」解決方案來插入此控制器所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="c486f-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="c486f-194">工作 2-將 Unity 包含在 MvcMusicStore 方案中</span><span class="sxs-lookup"><span data-stu-id="c486f-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="c486f-195">在這項工作中，您將會在解決方案中包含**Mvc3** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="c486f-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="c486f-196">Mvc3 封裝是針對 ASP.NET MVC 3 而設計，但它與 ASP.NET MVC 4 完全相容。</span><span class="sxs-lookup"><span data-stu-id="c486f-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="c486f-197">Unity 是輕量、可擴充的相依性插入容器，具有實例和類型攔截的選擇性支援。</span><span class="sxs-lookup"><span data-stu-id="c486f-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="c486f-198">這是一般用途的容器，可用於任何類型的 .NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c486f-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="c486f-199">它提供了相依性插入機制中的所有常見功能，包括：建立物件、在執行時間指定相依性，以及藉由將元件設定延後至容器，以藉由指定相依性來抽象化需求。</span><span class="sxs-lookup"><span data-stu-id="c486f-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>

1. <span data-ttu-id="c486f-200">在**MvcMusicStore**專案中安裝**Mvc3** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="c486f-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="c486f-201">若要這樣做，**請從** **其他視窗** | 開啟 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="c486f-202">執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="c486f-202">Run the following command.</span></span>

    <span data-ttu-id="c486f-203">PMC</span><span class="sxs-lookup"><span data-stu-id="c486f-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="c486f-204">![安裝 Unity. Mvc3 NuGet 套件](aspnet-mvc-4-dependency-injection/_static/image4.png "安裝 Unity. Mvc3 NuGet 套件")</span><span class="sxs-lookup"><span data-stu-id="c486f-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="c486f-205">*安裝 Unity. Mvc3 NuGet 套件*</span><span class="sxs-lookup"><span data-stu-id="c486f-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="c486f-206">安裝**Mvc3**套件之後，請探索它自動新增的檔案和資料夾，以簡化 Unity 設定。</span><span class="sxs-lookup"><span data-stu-id="c486f-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="c486f-207">![已安裝 Unity. Mvc3 封裝](aspnet-mvc-4-dependency-injection/_static/image5.png "已安裝 Unity. Mvc3 封裝")</span><span class="sxs-lookup"><span data-stu-id="c486f-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="c486f-208">*已安裝 Unity. Mvc3 封裝*</span><span class="sxs-lookup"><span data-stu-id="c486f-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a><span data-ttu-id="c486f-209">工作 3-在 Global.asax.cs 應用程式中註冊 Unity\_啟動</span><span class="sxs-lookup"><span data-stu-id="c486f-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="c486f-210">在這項工作中，您將更新位於**Global.asax.cs**中的**應用程式\_Start**方法來呼叫 Unity 啟動載入器初始化運算式，然後更新啟動載入器檔案，以註冊要用於相依性插入的服務和控制器。</span><span class="sxs-lookup"><span data-stu-id="c486f-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="c486f-211">現在，您將連結啟動載入器，這是初始化 Unity 容器和相依性解析程式的檔案。</span><span class="sxs-lookup"><span data-stu-id="c486f-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="c486f-212">若要這樣做，請開啟**Global.asax.cs** ，並在應用程式中新增下列反白顯示的**程式碼\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="c486f-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="c486f-213">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex01-初始化 Unity*）</span><span class="sxs-lookup"><span data-stu-id="c486f-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="c486f-214">開啟**Bootstrapper.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="c486f-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="c486f-215">包含下列命名空間： **MvcMusicStore. Services**和**MusicStore**。</span><span class="sxs-lookup"><span data-stu-id="c486f-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="c486f-216">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex01-新增命名空間的啟動載入*器）</span><span class="sxs-lookup"><span data-stu-id="c486f-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="c486f-217">將**BuildUnityContainer**方法的內容取代為下列程式碼，以註冊存放區控制器和存放服務。</span><span class="sxs-lookup"><span data-stu-id="c486f-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="c486f-218">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex01-註冊存放區控制器和服務*）</span><span class="sxs-lookup"><span data-stu-id="c486f-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c486f-219">工作 4-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c486f-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="c486f-220">在這項工作中，您將執行應用程式，以確認它現在可以在包含 Unity 之後載入。</span><span class="sxs-lookup"><span data-stu-id="c486f-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="c486f-221">按**F5**執行應用程式，應用程式現在應該會載入，而不會顯示任何錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c486f-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="c486f-222">![使用相依性插入執行應用程式](aspnet-mvc-4-dependency-injection/_static/image6.png "使用相依性插入執行應用程式")</span><span class="sxs-lookup"><span data-stu-id="c486f-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="c486f-223">*使用相依性插入執行應用程式*</span><span class="sxs-lookup"><span data-stu-id="c486f-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="c486f-224">流覽至 **/Store**。</span><span class="sxs-lookup"><span data-stu-id="c486f-224">Browse to **/Store**.</span></span> <span data-ttu-id="c486f-225">這會叫用**StoreController**，現在是使用**Unity**建立的。</span><span class="sxs-lookup"><span data-stu-id="c486f-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="c486f-226">![MVC 音樂存放區](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC 音樂存放區")</span><span class="sxs-lookup"><span data-stu-id="c486f-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="c486f-227">*MVC 音樂存放區*</span><span class="sxs-lookup"><span data-stu-id="c486f-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="c486f-228">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c486f-228">Close the browser.</span></span>

<span data-ttu-id="c486f-229">在下列練習中，您將瞭解如何擴充相依性插入範圍，以在 ASP.NET MVC Views 和 Action 篩選器內使用。</span><span class="sxs-lookup"><span data-stu-id="c486f-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="c486f-230">練習2：插入視圖</span><span class="sxs-lookup"><span data-stu-id="c486f-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="c486f-231">在此練習中，您將瞭解如何在視圖中使用相依性插入，以及 ASP.NET MVC 4 for Unity 整合的新功能。</span><span class="sxs-lookup"><span data-stu-id="c486f-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="c486f-232">若要這麼做，您將會在 Store 流覽視圖中呼叫自訂服務，這會在下方顯示訊息和影像。</span><span class="sxs-lookup"><span data-stu-id="c486f-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="c486f-233">然後，您會將專案與 Unity 整合，並建立自訂相依性解析程式來插入相依性。</span><span class="sxs-lookup"><span data-stu-id="c486f-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="c486f-234">工作 1-建立使用服務的視圖</span><span class="sxs-lookup"><span data-stu-id="c486f-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="c486f-235">在這項工作中，您將建立一個可執行服務呼叫的視圖，以產生新的相依性。</span><span class="sxs-lookup"><span data-stu-id="c486f-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="c486f-236">此服務包含在此解決方案所包含的簡單訊息服務中。</span><span class="sxs-lookup"><span data-stu-id="c486f-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="c486f-237">開啟位於**Source\Ex02-Injecting View\Begin**資料夾中的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="c486f-238">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c486f-239">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="c486f-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c486f-240">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c486f-241">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c486f-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c486f-242">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c486f-243">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c486f-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c486f-244">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c486f-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c486f-245">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c486f-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="c486f-246">如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="c486f-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="c486f-247">包含**MessageService.cs**和**IMessageService.cs**類別，其位於 **/Services**的**來源 \Assets**資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c486f-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="c486f-248">若要這樣做，請以滑鼠右鍵按一下 [**服務**] 資料夾，然後選取 [**加入現有專案**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="c486f-249">流覽至檔案的位置，並將其包含在內。</span><span class="sxs-lookup"><span data-stu-id="c486f-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="c486f-250">![新增訊息服務和服務介面](aspnet-mvc-4-dependency-injection/_static/image8.png "新增訊息服務和服務介面")</span><span class="sxs-lookup"><span data-stu-id="c486f-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="c486f-251">*新增訊息服務和服務介面*</span><span class="sxs-lookup"><span data-stu-id="c486f-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c486f-252">**IMessageService**介面會定義**MessageService**類別所實作為的兩個屬性。</span><span class="sxs-lookup"><span data-stu-id="c486f-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="c486f-253">這些屬性-**message**和**ImageUrl**-儲存訊息，以及要顯示之影像的 URL。</span><span class="sxs-lookup"><span data-stu-id="c486f-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="c486f-254">在專案的根資料夾中建立 **/Pages**資料夾，然後從**Source\Assets**新增現有的類別**MyBasePage.cs** 。</span><span class="sxs-lookup"><span data-stu-id="c486f-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="c486f-255">您會繼承自的基礎頁面具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="c486f-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="c486f-256">![Pages 資料夾](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages 資料夾")</span><span class="sxs-lookup"><span data-stu-id="c486f-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="c486f-257">從 **/Views/Store**資料夾開啟 **[流覽]** ，並使其繼承自**MyBasePage.cs**。</span><span class="sxs-lookup"><span data-stu-id="c486f-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="c486f-258">在**流覽**視圖中，新增對**MessageService**的呼叫，以顯示由服務所抓取的影像和訊息。</span><span class="sxs-lookup"><span data-stu-id="c486f-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="c486f-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="c486f-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="c486f-260">工作 2-包括自訂相依性解析程式和自訂視圖頁啟動項</span><span class="sxs-lookup"><span data-stu-id="c486f-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="c486f-261">在上一項工作中，您已在視圖內插入新的相依性，以在其中執行服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="c486f-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="c486f-262">現在，您將藉由執行 ASP.NET MVC 相依性插入介面**IViewPageActivator**和**IDependencyResolver**來解決該相依性。</span><span class="sxs-lookup"><span data-stu-id="c486f-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="c486f-263">您將會在解決方案中包含**IDependencyResolver**的執行，以使用 Unity 處理服務的抓取。</span><span class="sxs-lookup"><span data-stu-id="c486f-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="c486f-264">然後，您將會包含**IViewPageActivator**介面的另一個自訂執行，以解決視圖的建立。</span><span class="sxs-lookup"><span data-stu-id="c486f-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="c486f-265">由於 ASP.NET MVC 3 的關係，相依性插入的執行已經簡化了註冊服務的介面。</span><span class="sxs-lookup"><span data-stu-id="c486f-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="c486f-266">**IDependencyResolver**和**IViewPageActivator**是用於相依性插入的 ASP.NET MVC 3 功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="c486f-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="c486f-267">**-IDependencyResolver**介面會取代先前的 IMvcServiceLocator。</span><span class="sxs-lookup"><span data-stu-id="c486f-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="c486f-268">IDependencyResolver 的實施者必須傳回服務或服務集合的實例。</span><span class="sxs-lookup"><span data-stu-id="c486f-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="c486f-269">**-IViewPageActivator**介面可讓您更精細地控制透過相依性插入來具現化視圖頁面的方式。</span><span class="sxs-lookup"><span data-stu-id="c486f-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="c486f-270">執行**IViewPageActivator**介面的類別可以使用內容資訊來建立 view 實例。</span><span class="sxs-lookup"><span data-stu-id="c486f-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. <span data-ttu-id="c486f-271">在專案的**根資料夾中建立/factory**資料夾。</span><span class="sxs-lookup"><span data-stu-id="c486f-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="c486f-272">將**CustomViewPageActivator.cs**加入您的方案，從 **/Sources/Assets/** 到**factory 資料夾。**</span><span class="sxs-lookup"><span data-stu-id="c486f-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="c486f-273">若要這麼做，請以滑鼠右鍵按一下  **/Factories**  資料夾，然後選取 **新增 |現有專案**，然後選取  **CustomViewPageActivator.cs**。</span><span class="sxs-lookup"><span data-stu-id="c486f-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="c486f-274">這個類別會實**IViewPageActivator**介面來保存 Unity 容器。</span><span class="sxs-lookup"><span data-stu-id="c486f-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="c486f-275">**CustomViewPageActivator**會負責管理使用 Unity 容器來建立視圖的方式。</span><span class="sxs-lookup"><span data-stu-id="c486f-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="c486f-276">將**UnityDependencyResolver.cs**檔案從 **/Sources/Assets**納入 **/Factories**資料夾。</span><span class="sxs-lookup"><span data-stu-id="c486f-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="c486f-277">若要這麼做，請以滑鼠右鍵按一下  **/Factories**  資料夾，然後選取 **新增 |現有專案**，然後選取  **UnityDependencyResolver.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="c486f-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="c486f-278">**UnityDependencyResolver**類別是 Unity 的自訂 DependencyResolver。</span><span class="sxs-lookup"><span data-stu-id="c486f-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="c486f-279">在 Unity 容器內找不到服務時，會 invocated 基底解析程式。</span><span class="sxs-lookup"><span data-stu-id="c486f-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="c486f-280">在下列工作中，這兩個執行將會註冊，讓模型知道服務的位置和 views。</span><span class="sxs-lookup"><span data-stu-id="c486f-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="c486f-281">工作 3-註冊 Unity 容器內的相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="c486f-282">在這項工作中，您會將所有先前的專案放在一起，以進行相依性插入作業。</span><span class="sxs-lookup"><span data-stu-id="c486f-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="c486f-283">目前，您的解決方案具有下列元素：</span><span class="sxs-lookup"><span data-stu-id="c486f-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="c486f-284">繼承自**MyBaseClass**並使用**MessageService**的**流覽**視圖。</span><span class="sxs-lookup"><span data-stu-id="c486f-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="c486f-285">中繼類別**MyBaseClass**，其已針對服務介面宣告相依性插入。</span><span class="sxs-lookup"><span data-stu-id="c486f-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="c486f-286">服務**MessageService**及其介面**IMessageService**。</span><span class="sxs-lookup"><span data-stu-id="c486f-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="c486f-287">適用于 Unity- **UnityDependencyResolver**的自訂相依性解析程式，負責處理服務的抓取。</span><span class="sxs-lookup"><span data-stu-id="c486f-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="c486f-288">View Page activator- **CustomViewPageActivator** -建立頁面。</span><span class="sxs-lookup"><span data-stu-id="c486f-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="c486f-289">若要插入**流覽**視圖，您現在會在 Unity 容器中註冊自訂相依性解析程式。</span><span class="sxs-lookup"><span data-stu-id="c486f-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="c486f-290">開啟**Bootstrapper.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="c486f-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="c486f-291">向 Unity 容器註冊**MessageService**的實例，以初始化服務：</span><span class="sxs-lookup"><span data-stu-id="c486f-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="c486f-292">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-註冊訊息服務*）</span><span class="sxs-lookup"><span data-stu-id="c486f-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="c486f-293">加入**MvcMusicStore**的參考。</span><span class="sxs-lookup"><span data-stu-id="c486f-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="c486f-294">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-Factory 命名空間*）</span><span class="sxs-lookup"><span data-stu-id="c486f-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="c486f-295">將**CustomViewPageActivator**註冊為 Unity 容器中的 View Page activator：</span><span class="sxs-lookup"><span data-stu-id="c486f-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="c486f-296">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-註冊 CustomViewPageActivator*）</span><span class="sxs-lookup"><span data-stu-id="c486f-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="c486f-297">以**UnityDependencyResolver**的實例取代 ASP.NET MVC 4 預設相依性解析程式。</span><span class="sxs-lookup"><span data-stu-id="c486f-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="c486f-298">若要這麼做，請將**Initialize**方法內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c486f-298">To do this, replace **Initialize** method content with the following code:</span></span>

    <span data-ttu-id="c486f-299">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex02-更新相依性解析程式*）</span><span class="sxs-lookup"><span data-stu-id="c486f-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="c486f-300">ASP.NET MVC 提供預設的相依性解析程式類別。</span><span class="sxs-lookup"><span data-stu-id="c486f-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="c486f-301">若要使用自訂相依性解析程式做為我們針對 unity 所建立的解決器，必須更換此解決器。</span><span class="sxs-lookup"><span data-stu-id="c486f-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c486f-302">工作 4-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c486f-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="c486f-303">在這項工作中，您將執行應用程式，以確認存放區瀏覽器會取用服務，並顯示影像和抓取的訊息：</span><span class="sxs-lookup"><span data-stu-id="c486f-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="c486f-304">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c486f-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="c486f-305">按一下 [內容] 功能表中的 [**搖滾**]，並查看**MessageService**如何插入至視圖中，以及如何載入歡迎訊息和影像。</span><span class="sxs-lookup"><span data-stu-id="c486f-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="c486f-306">在此範例中，我們輸入 &quot;**搖滾**&quot;：</span><span class="sxs-lookup"><span data-stu-id="c486f-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="c486f-307">![MVC 音樂存放區-視圖插入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC 音樂存放區-視圖插入")</span><span class="sxs-lookup"><span data-stu-id="c486f-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="c486f-308">*MVC 音樂存放區-視圖插入*</span><span class="sxs-lookup"><span data-stu-id="c486f-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="c486f-309">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c486f-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="c486f-310">練習3：插入動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="c486f-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="c486f-311">在先前的實際操作實驗室**自訂動作篩選**條件中，您已使用篩選自訂和插入。</span><span class="sxs-lookup"><span data-stu-id="c486f-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="c486f-312">在此練習中，您將瞭解如何使用 Unity 容器，插入具有相依性插入的篩選器。</span><span class="sxs-lookup"><span data-stu-id="c486f-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="c486f-313">若要這麼做，您要將追蹤網站活動的自訂動作篩選器新增至 [音樂存放區] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="c486f-314">工作 1-在解決方案中包含追蹤篩選</span><span class="sxs-lookup"><span data-stu-id="c486f-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="c486f-315">在這項工作中，您會在 [音樂] 存放區中包含追蹤事件的自訂動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="c486f-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="c486f-316">由於自訂動作篩選器概念已在先前的實驗室中處理 &quot;自訂動作篩選&quot;，您只需要在此實驗室的 [資產] 資料夾中包含篩選準則類別，然後建立 Unity 的篩選器提供者：</span><span class="sxs-lookup"><span data-stu-id="c486f-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="c486f-317">開啟位於 [ **Source\Ex03-插入動作 Filter\Begin** ] 資料夾中的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="c486f-318">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c486f-319">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="c486f-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c486f-320">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c486f-321">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c486f-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c486f-322">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c486f-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c486f-323">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c486f-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c486f-324">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c486f-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c486f-325">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c486f-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="c486f-326">如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="c486f-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="c486f-327">將**TraceActionFilter.cs**檔案從 **/Sources/Assets**納入 **/Filters**資料夾。</span><span class="sxs-lookup"><span data-stu-id="c486f-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="c486f-328">此自訂動作篩選準則會執行 ASP.NET 追蹤。</span><span class="sxs-lookup"><span data-stu-id="c486f-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="c486f-329">您可以查看 &quot;ASP.NET MVC 4 本機和動態動作篩選&quot; 實驗室以取得更多參考。</span><span class="sxs-lookup"><span data-stu-id="c486f-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="c486f-330">將空的類別**FilterProvider.cs**新增至資料夾 **/Filters.** 中的專案</span><span class="sxs-lookup"><span data-stu-id="c486f-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="c486f-331">在**FilterProvider.cs**中新增**system.web**和**Unity**命名空間。</span><span class="sxs-lookup"><span data-stu-id="c486f-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="c486f-332">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-篩選提供者加入命名空間*）</span><span class="sxs-lookup"><span data-stu-id="c486f-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="c486f-333">讓類別繼承自**IFilterProvider**介面。</span><span class="sxs-lookup"><span data-stu-id="c486f-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="c486f-334">在**FilterProvider**類別中新增**IUnityContainer**屬性，然後建立類別的函式來指派容器。</span><span class="sxs-lookup"><span data-stu-id="c486f-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="c486f-335">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-篩選提供者*函式）</span><span class="sxs-lookup"><span data-stu-id="c486f-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="c486f-336">篩選器提供者類別的函式不會在內建立**新**的物件。</span><span class="sxs-lookup"><span data-stu-id="c486f-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="c486f-337">容器會當做參數來傳遞，而相依性則由 Unity 解決。</span><span class="sxs-lookup"><span data-stu-id="c486f-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="c486f-338">在**FilterProvider**類別中，執行從**IFilterProvider**介面**GetFilters**的方法。</span><span class="sxs-lookup"><span data-stu-id="c486f-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="c486f-339">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-篩選提供者 GetFilters*）</span><span class="sxs-lookup"><span data-stu-id="c486f-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="c486f-340">工作 2-註冊並啟用篩選準則</span><span class="sxs-lookup"><span data-stu-id="c486f-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="c486f-341">在這項工作中，您將會啟用網站追蹤。</span><span class="sxs-lookup"><span data-stu-id="c486f-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="c486f-342">若要這麼做，您會在**Bootstrapper.cs BuildUnityContainer**方法中註冊篩選準則，以開始追蹤：</span><span class="sxs-lookup"><span data-stu-id="c486f-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="c486f-343">開啟位於專案根目錄中的**web.config** ，並在 system.web 群組啟用追蹤追蹤。</span><span class="sxs-lookup"><span data-stu-id="c486f-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="c486f-344">在專案根目錄中開啟**Bootstrapper.cs** 。</span><span class="sxs-lookup"><span data-stu-id="c486f-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="c486f-345">加入**MvcMusicStore**命名空間的參考。</span><span class="sxs-lookup"><span data-stu-id="c486f-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="c486f-346">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-新增命名空間的啟動載入*器）</span><span class="sxs-lookup"><span data-stu-id="c486f-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="c486f-347">選取**BuildUnityContainer**方法，並在 Unity 容器中註冊篩選。</span><span class="sxs-lookup"><span data-stu-id="c486f-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="c486f-348">您必須註冊篩選準則提供者以及動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="c486f-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="c486f-349">（程式碼片段- *ASP.NET 相依性插入實驗室-Ex03-註冊 FilterProvider 和 ActionFilter*）</span><span class="sxs-lookup"><span data-stu-id="c486f-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="c486f-350">工作 3-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c486f-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="c486f-351">在這項工作中，您將執行應用程式，並測試自訂動作篩選器是否正在追蹤活動：</span><span class="sxs-lookup"><span data-stu-id="c486f-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="c486f-352">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c486f-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="c486f-353">按一下 [內容] 功能表中的 [**搖滾**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="c486f-354">如果您想要的話，可以流覽至更多內容。</span><span class="sxs-lookup"><span data-stu-id="c486f-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="c486f-355">![Music 市集](aspnet-mvc-4-dependency-injection/_static/image11.png "Music 市集")</span><span class="sxs-lookup"><span data-stu-id="c486f-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="c486f-356">*Music 市集*</span><span class="sxs-lookup"><span data-stu-id="c486f-356">*Music Store*</span></span>
3. <span data-ttu-id="c486f-357">流覽至 **/Trace.axd**以查看 [應用程式追蹤] 頁面，然後按一下 [**查看詳細資料**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="c486f-358">![應用程式追蹤記錄檔](aspnet-mvc-4-dependency-injection/_static/image12.png "應用程式追蹤記錄檔")</span><span class="sxs-lookup"><span data-stu-id="c486f-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="c486f-359">*應用程式追蹤記錄檔*</span><span class="sxs-lookup"><span data-stu-id="c486f-359">*Application Trace Log*</span></span>

    <span data-ttu-id="c486f-360">![應用程式追蹤-要求詳細資料](aspnet-mvc-4-dependency-injection/_static/image13.png "應用程式追蹤-要求詳細資料")</span><span class="sxs-lookup"><span data-stu-id="c486f-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="c486f-361">*應用程式追蹤-要求詳細資料*</span><span class="sxs-lookup"><span data-stu-id="c486f-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="c486f-362">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c486f-362">Close the browser.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c486f-363">總結</span><span class="sxs-lookup"><span data-stu-id="c486f-363">Summary</span></span>

<span data-ttu-id="c486f-364">藉由完成此實際操作實驗室，您已瞭解如何使用 NuGet 套件整合 Unity，在 ASP.NET MVC 4 中使用相依性插入。</span><span class="sxs-lookup"><span data-stu-id="c486f-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="c486f-365">為了達到此目的，您已在控制器、視圖和動作篩選內使用相依性插入。</span><span class="sxs-lookup"><span data-stu-id="c486f-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="c486f-366">涵蓋下列概念：</span><span class="sxs-lookup"><span data-stu-id="c486f-366">The following concepts were covered:</span></span>

- <span data-ttu-id="c486f-367">ASP.NET MVC 4 相依性插入功能</span><span class="sxs-lookup"><span data-stu-id="c486f-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="c486f-368">使用 Unity 進行 unity 整合 Mvc3 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c486f-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="c486f-369">控制器中的相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="c486f-370">在 Views 中插入相依性</span><span class="sxs-lookup"><span data-stu-id="c486f-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="c486f-371">動作篩選準則的相依性插入</span><span class="sxs-lookup"><span data-stu-id="c486f-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="c486f-372">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="c486f-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="c486f-373">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="c486f-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="c486f-374">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="c486f-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="c486f-375">移至 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="c486f-375">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="c486f-376">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="c486f-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="c486f-377">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-377">Click on **Install Now**.</span></span> <span data-ttu-id="c486f-378">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="c486f-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="c486f-379">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c486f-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="c486f-380">![安裝 Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="c486f-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="c486f-381">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="c486f-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="c486f-382">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="c486f-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="c486f-384">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="c486f-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="c486f-385">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="c486f-385">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="c486f-387">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="c486f-387">*Installation progress*</span></span>
6. <span data-ttu-id="c486f-388">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="c486f-388">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="c486f-390">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="c486f-390">*Installation completed*</span></span>
7. <span data-ttu-id="c486f-391">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="c486f-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="c486f-392">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="c486f-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="c486f-394">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="c486f-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="c486f-395">附錄 B：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="c486f-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="c486f-396">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="c486f-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="c486f-397">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="c486f-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="c486f-398">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-dependency-injection/_static/image19.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="c486f-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="c486f-399">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="c486f-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="c486f-400">***若要使用鍵盤新增程式碼片段（C#僅限）***</span><span class="sxs-lookup"><span data-stu-id="c486f-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="c486f-401">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="c486f-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="c486f-402">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="c486f-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="c486f-403">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="c486f-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="c486f-404">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="c486f-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="c486f-405">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="c486f-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="c486f-406">![開始鍵入程式碼片段名稱](aspnet-mvc-4-dependency-injection/_static/image20.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="c486f-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="c486f-407">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="c486f-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="c486f-408">![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-dependency-injection/_static/image21.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="c486f-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="c486f-409">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="c486f-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="c486f-410">![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-dependency-injection/_static/image22.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="c486f-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="c486f-411">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="c486f-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="c486f-412">***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1.</span><span class="sxs-lookup"><span data-stu-id="c486f-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="c486f-413">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="c486f-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="c486f-414">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="c486f-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="c486f-415">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="c486f-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="c486f-416">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-dependency-injection/_static/image23.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="c486f-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="c486f-417">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="c486f-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="c486f-418">![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-dependency-injection/_static/image24.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="c486f-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="c486f-419">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="c486f-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
