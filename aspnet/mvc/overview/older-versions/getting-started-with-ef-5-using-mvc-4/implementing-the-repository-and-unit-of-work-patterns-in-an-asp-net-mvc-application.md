---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 應用程式中執行存放庫和工作單位模式（9/10） |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595235"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a><span data-ttu-id="ba7f0-103">在 ASP.NET MVC 應用程式中執行存放庫和工作單位模式（9/10）</span><span class="sxs-lookup"><span data-stu-id="ba7f0-103">Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application (9 of 10)</span></span>

<span data-ttu-id="ba7f0-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ba7f0-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="ba7f0-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="ba7f0-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="ba7f0-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="ba7f0-107">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="ba7f0-108">您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="ba7f0-109">如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="ba7f0-110">您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="ba7f0-111">如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="ba7f0-112">在上一個教學課程中，您使用了繼承來減少 `Student` 和 `Instructor` 實體類別中的重複程式碼。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-112">In the previous tutorial you used inheritance to reduce redundant code in the `Student` and `Instructor` entity classes.</span></span> <span data-ttu-id="ba7f0-113">在本教學課程中，您會看到一些使用存放庫和 CRUD 作業單元模式的方式。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-113">In this tutorial you'll see some ways to use the repository and unit of work patterns for CRUD operations.</span></span> <span data-ttu-id="ba7f0-114">如同在上一個教學課程中，您將會變更程式碼與您已建立的頁面，而不是建立新頁面的方式。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-114">As in the previous tutorial, in this one you'll change the way your code works with pages you already created rather than creating new pages.</span></span>

## <a name="the-repository-and-unit-of-work-patterns"></a><span data-ttu-id="ba7f0-115">儲存機制和工作單位模式</span><span class="sxs-lookup"><span data-stu-id="ba7f0-115">The Repository and Unit of Work Patterns</span></span>

<span data-ttu-id="ba7f0-116">儲存機制和工作單位模式的目的是要在應用程式的資料存取層與商務邏輯層之間建立抽象層。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-116">The repository and unit of work patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="ba7f0-117">實作這些模式可協助隔離您的應用程式與資料存放區中的變更，並可促進自動化單元測試或測試驅動開發 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-117">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span>

<span data-ttu-id="ba7f0-118">在本教學課程中，您將為每個實體類型執行存放庫類別。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-118">In this tutorial you'll implement a repository class for each entity type.</span></span> <span data-ttu-id="ba7f0-119">針對 `Student` 實體類型，您將建立存放庫介面和儲存機制類別。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-119">For the `Student` entity type you'll create a repository interface and a repository class.</span></span> <span data-ttu-id="ba7f0-120">當您具現化控制器中的存放庫時，您將會使用介面，讓控制器接受任何可執行存放庫介面之物件的參考。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-120">When you instantiate the repository in your controller, you'll use the interface so that the controller will accept a reference to any object that implements the repository interface.</span></span> <span data-ttu-id="ba7f0-121">當控制器在 web 伺服器下執行時，它會接收與 Entity Framework 搭配運作的存放庫。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-121">When the controller runs under a web server, it receives a repository that works with the Entity Framework.</span></span> <span data-ttu-id="ba7f0-122">當控制器在單元測試類別下執行時，它會接收使用儲存之資料的儲存機制，您可以輕鬆地操作以進行測試，例如記憶體中的集合。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-122">When the controller runs under a unit test class, it receives a repository that works with data stored in a way that you can easily manipulate for testing, such as an in-memory collection.</span></span>

<span data-ttu-id="ba7f0-123">稍後在本教學課程中，您將使用多個儲存機制和工作單位類別，做為 `Course` 控制器中的 `Course` 和 `Department` 實體類型。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-123">Later in the tutorial you'll use multiple repositories and a unit of work class for the `Course` and `Department` entity types in the `Course` controller.</span></span> <span data-ttu-id="ba7f0-124">工作單位類別會藉由建立所有儲存機制所共用的單一資料庫內容類別，來協調多個存放庫的工作。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-124">The unit of work class coordinates the work of multiple repositories by creating a single database context class shared by all of them.</span></span> <span data-ttu-id="ba7f0-125">如果您想要能夠執行自動化單元測試，您可以使用與 `Student` 存放庫相同的方式，為這些類別建立和使用介面。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-125">If you wanted to be able to perform automated unit testing, you'd create and use interfaces for these classes in the same way you did for the `Student` repository.</span></span> <span data-ttu-id="ba7f0-126">不過，為了讓教學課程保持簡單，您將建立並使用這些沒有介面的類別。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-126">However, to keep the tutorial simple, you'll create and use these classes without interfaces.</span></span>

<span data-ttu-id="ba7f0-127">下圖顯示相較于不使用存放庫或工作單位模式的情況，與控制器和內容類別別之間的關聯性進行概念化的一種方式。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-127">The following illustration shows one way to conceptualize the relationships between the controller and context classes compared to not using the repository or unit of work pattern at all.</span></span>

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

<span data-ttu-id="ba7f0-129">您不會在本教學課程系列中建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-129">You won't create unit tests in this tutorial series.</span></span> <span data-ttu-id="ba7f0-130">如需使用儲存機制模式之 MVC 應用程式的 TDD 簡介，請參閱[逐步解說：搭配使用 TDD 與 ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-130">For an introduction to TDD with an MVC application that uses the repository pattern, see [Walkthrough: Using TDD with ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx).</span></span> <span data-ttu-id="ba7f0-131">如需存放庫模式的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-131">For more information about the repository pattern, see the following resources:</span></span>

- <span data-ttu-id="ba7f0-132">MSDN 上[的存放庫模式](https://msdn.microsoft.com/library/ff649690.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-132">[The Repository Pattern](https://msdn.microsoft.com/library/ff649690.aspx) on MSDN.</span></span>
- <span data-ttu-id="ba7f0-133">在 Entity Framework 的 team blog 上[使用 Entity Framework 4.0 的存放庫和工作單位模式](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-133">[Using Repository and Unit of Work patterns with Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) on the Entity Framework team blog.</span></span>
- <span data-ttu-id="ba7f0-134">[Agile Entity Framework 4](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) Julie Lerman 的 blog 上的一系列文章。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-134">[Agile Entity Framework 4 Repository](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) series of posts on Julie Lerman's blog.</span></span>
- <span data-ttu-id="ba7f0-135">在 Dan Wahlin 的 blog 上，[建立一眼 HTML5/JQuery 應用程式的帳戶](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-135">[Building the Account at a Glance HTML5/jQuery Application](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) on Dan Wahlin's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="ba7f0-136">有許多方法可以執行存放庫和工作單位模式。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-136">There are many ways to implement the repository and unit of work patterns.</span></span> <span data-ttu-id="ba7f0-137">您可以使用具有或不含工作單位類別的儲存機制類別。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-137">You can use repository classes with or without a unit of work class.</span></span> <span data-ttu-id="ba7f0-138">您可以針對所有實體類型，或針對每個類型來執行單一存放庫。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-138">You can implement a single repository for all entity types, or one for each type.</span></span> <span data-ttu-id="ba7f0-139">如果您針對每個類型執行一個，則可以使用不同的類別、泛型基類和衍生類別，或是抽象基類和衍生類別。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-139">If you implement one for each type, you can use separate classes, a generic base class and derived classes, or an abstract base class and derived classes.</span></span> <span data-ttu-id="ba7f0-140">您可以在存放庫中包含商務邏輯，或將其限制為數據存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-140">You can include business logic in your repository or restrict it to data access logic.</span></span> <span data-ttu-id="ba7f0-141">您也可以使用[idbset 會](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx)介面（而不是您的實體集的[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)類型），將抽象層建立到資料庫內容類別中。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-141">You can also build an abstraction layer into your database context class by using [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) interfaces there instead of [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) types for your entity sets.</span></span> <span data-ttu-id="ba7f0-142">本教學課程中所示的抽象層的執行方法是您可以考慮的一個選項，而不是所有案例和環境的建議。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-142">The approach to implementing an abstraction layer shown in this tutorial is one option for you to consider, not a recommendation for all scenarios and environments.</span></span>

## <a name="creating-the-student-repository-class"></a><span data-ttu-id="ba7f0-143">建立 Student 存放庫類別</span><span class="sxs-lookup"><span data-stu-id="ba7f0-143">Creating the Student Repository Class</span></span>

<span data-ttu-id="ba7f0-144">在*DAL*資料夾中，建立名為*IStudentRepository.cs*的類別檔案，並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-144">In the *DAL* folder, create a class file named *IStudentRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="ba7f0-145">此程式碼會宣告一組典型的 CRUD 方法，包括兩個讀取方法：一個會傳回所有 `Student` 實體，另一個則會依識別碼尋找單一 `Student` 實體。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-145">This code declares a typical set of CRUD methods, including two read methods — one that returns all `Student` entities, and one that finds a single `Student` entity by ID.</span></span>

<span data-ttu-id="ba7f0-146">在*DAL*資料夾中，建立名為*StudentRepository.cs* file 的類別檔案。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-146">In the *DAL* folder, create a class file named *StudentRepository.cs* file.</span></span> <span data-ttu-id="ba7f0-147">將現有的程式碼取代為下列程式碼，以執行 `IStudentRepository` 介面：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-147">Replace the existing code with the following code, which implements the `IStudentRepository` interface:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="ba7f0-148">資料庫內容定義于類別變數中，而此函式需要呼叫物件傳入內容的實例：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-148">The database context is defined in a class variable, and the constructor expects the calling object to pass in an instance of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="ba7f0-149">您可以在存放庫中具現化新的內容，但如果您在一個控制器中使用多個存放庫，每個都有不同的內容。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-149">You could instantiate a new context in the repository, but then if you used multiple repositories in one controller, each would end up with a separate context.</span></span> <span data-ttu-id="ba7f0-150">稍後您將在 `Course` 控制器中使用多個存放庫，您會看到工作單位類別如何確保所有存放庫都使用相同的內容。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-150">Later you'll use multiple repositories in the `Course` controller, and you'll see how a unit of work class can ensure that all repositories use the same context.</span></span>

<span data-ttu-id="ba7f0-151">儲存機制會依照您稍早在控制器中看到的方式來執行[IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx)和處置資料庫內容，而其 CRUD 方法會以您稍早所見的相同方式呼叫資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-151">The repository implements [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) and disposes the database context as you saw earlier in the controller, and its CRUD methods make calls to the database context in the same way that you saw earlier.</span></span>

## <a name="change-the-student-controller-to-use-the-repository"></a><span data-ttu-id="ba7f0-152">變更學生控制器以使用存放庫</span><span class="sxs-lookup"><span data-stu-id="ba7f0-152">Change the Student Controller to Use the Repository</span></span>

<span data-ttu-id="ba7f0-153">在*StudentController.cs*中，將類別中目前的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-153">In *StudentController.cs*, replace the code currently in the class with the following code.</span></span> <span data-ttu-id="ba7f0-154">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-154">The changes are highlighted.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

<span data-ttu-id="ba7f0-155">控制器現在會針對執行 `IStudentRepository` 介面（而非內容類別）的物件宣告類別變數：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-155">The controller now declares a class variable for an object that implements the `IStudentRepository` interface instead of the context class:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="ba7f0-156">預設的（無參數）處理常式會建立新的內容實例，而選擇性的函式可讓呼叫者傳入內容實例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-156">The default (parameterless) constructor creates a new context instance, and an optional constructor allows the caller to pass in a context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="ba7f0-157">（如果您使用的是相依性*插入*或 DI，則不需要預設的函式，因為 DI 軟體會確保一律會提供正確的存放庫物件）。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-157">(If you were using *dependency injection*, or DI, you wouldn't need the default constructor because the DI software would ensure that the correct repository object would always be provided.)</span></span>

<span data-ttu-id="ba7f0-158">在 CRUD 方法中，現在會呼叫儲存機制，而不是內容：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-158">In the CRUD methods, the repository is now called instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="ba7f0-159">而 `Dispose` 方法現在會處置存放庫，而不是內容：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-159">And the `Dispose` method now disposes the repository instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="ba7f0-160">執行網站，然後按一下 [**學生**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-160">Run the site and click the **Students** tab.</span></span>

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="ba7f0-162">此頁面的外觀和運作方式與您變更程式碼以使用存放庫之前一樣，而其他學生頁面也會運作相同。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-162">The page looks and works the same as it did before you changed the code to use the repository, and the other Student pages also work the same.</span></span> <span data-ttu-id="ba7f0-163">不過，控制器的 `Index` 方法進行篩選和排序的方式有一項重要的差異。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-163">However, there's an important difference in the way the `Index` method of the controller does filtering and ordering.</span></span> <span data-ttu-id="ba7f0-164">這個方法的原始版本包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-164">The original version of this method contained the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

<span data-ttu-id="ba7f0-165">更新的 `Index` 方法包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-165">The updated `Index` method contains the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

<span data-ttu-id="ba7f0-166">只有反白顯示的程式碼才會變更。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-166">Only the highlighted code has changed.</span></span>

<span data-ttu-id="ba7f0-167">在程式碼的原始版本中，`students` 會輸入為 `IQueryable` 物件。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-167">In the original version of the code, `students` is typed as an `IQueryable` object.</span></span> <span data-ttu-id="ba7f0-168">查詢不會傳送到資料庫，直到使用 `ToList`之類的方法將它轉換成集合，直到索引視圖存取學生模型為止。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-168">The query isn't sent to the database until it's converted into a collection using a method such as `ToList`, which doesn't occur until the Index view accesses the student model.</span></span> <span data-ttu-id="ba7f0-169">上述原始程式碼中的 `Where` 方法，會成為傳送至資料庫之 SQL 查詢中的 `WHERE` 子句。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-169">The `Where` method in the original code above becomes a `WHERE` clause in the SQL query that is sent to the database.</span></span> <span data-ttu-id="ba7f0-170">這也表示，只有選取的實體會由資料庫傳回。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-170">That in turn means that only the selected entities are returned by the database.</span></span> <span data-ttu-id="ba7f0-171">不過，由於將 `context.Students` 變更為 `studentRepository.GetStudents()`，因此在此語句之後的 `students` 變數是包含資料庫中所有學生的 `IEnumerable` 集合。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-171">However, as a result of changing `context.Students` to `studentRepository.GetStudents()`, the `students` variable after this statement is an `IEnumerable` collection that includes all students in the database.</span></span> <span data-ttu-id="ba7f0-172">套用 `Where` 方法的最終結果是相同的，但現在工作是在 web 伺服器的記憶體中執行，而不是由資料庫完成。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-172">The end result of applying the `Where` method is the same, but now the work is done in memory on the web server and not by the database.</span></span> <span data-ttu-id="ba7f0-173">對於傳回大量資料的查詢，這可能會沒有效率。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-173">For queries that return large volumes of data, this can be inefficient.</span></span>

> [!TIP]
> 
> <span data-ttu-id="ba7f0-174">**IQueryable 與 IEnumerable 的比較**</span><span class="sxs-lookup"><span data-stu-id="ba7f0-174">**IQueryable vs. IEnumerable**</span></span>
> 
> <span data-ttu-id="ba7f0-175">如這裡所示來執行存放庫之後，即使您在**搜尋**方塊中輸入東西，傳送給 SQL Server 的查詢還是會傳回所有學生資料列，因為它不包含您的搜尋條件：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-175">After you implement the repository as shown here, even if you enter something in the **Search** box the query sent to SQL Server returns all Student rows because it doesn't include your search criteria:</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> <span data-ttu-id="ba7f0-176">此查詢會傳回所有學生資料，因為存放庫執行查詢時，不會知道搜尋條件。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-176">This query returns all of the student data because the repository executed the query without knowing about the search criteria.</span></span> <span data-ttu-id="ba7f0-177">在 `IEnumerable` 集合上呼叫 `ToPagedList` 方法時，會在記憶體中排序、套用搜尋準則，以及選取要分頁的資料子集（僅顯示3個數據列）。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-177">The process of sorting, applying search criteria, and selecting a subset of the data for paging (showing only 3 rows in this case) is done in memory later when the `ToPagedList` method is called on the `IEnumerable` collection.</span></span>
> 
> <span data-ttu-id="ba7f0-178">在舊版的程式碼（在您執行存放庫之前）中，如果在 `IQueryable` 物件上呼叫 `ToPagedList`，則查詢不會傳送到資料庫，直到您套用搜尋條件為止。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-178">In the previous version of the code (before you implemented the repository), the query is not sent to the database until after you apply the search criteria, when `ToPagedList` is called on the `IQueryable` object.</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> <span data-ttu-id="ba7f0-179">在 `IQueryable` 物件上呼叫 ToPagedList 時，傳送至 SQL Server 的查詢會指定搜尋字串，因此只會傳回符合搜尋條件的資料列，而且不需要在記憶體中進行任何篩選。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-179">When ToPagedList is called on an `IQueryable` object, the query sent to SQL Server specifies the search string, and as a result only rows that meet the search criteria are returned, and no filtering needs to be done in memory.</span></span>
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> <span data-ttu-id="ba7f0-180">（下列教學課程說明如何檢查傳送至 SQL Server 的查詢）。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-180">(The following tutorial explains how to examine queries sent to SQL Server.)</span></span>

<span data-ttu-id="ba7f0-181">下一節將示範如何執行存放庫方法，讓您指定資料庫應執行此工作。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-181">The following section shows how to implement repository methods that enable you to specify that this work should be done by the database.</span></span>

<span data-ttu-id="ba7f0-182">您現在已在控制器和 Entity Framework 資料庫內容之間建立抽象層。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-182">You've now created an abstraction layer between the controller and the Entity Framework database context.</span></span> <span data-ttu-id="ba7f0-183">如果您要使用此應用程式執行自動化單元測試，您可以在單元測試專案中建立替代的儲存機制類別，以進行 `IStudentRepository` *。*</span><span class="sxs-lookup"><span data-stu-id="ba7f0-183">If you were going to perform automated unit testing with this application, you could create an alternative repository class in a unit test project that implements `IStudentRepository`*.*</span></span> <span data-ttu-id="ba7f0-184">這個模擬儲存機制類別可以操控記憶體內部集合來測試控制器函式，而不是呼叫內容來讀取和寫入資料。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-184">Instead of calling the context to read and write data, this mock repository class could manipulate in-memory collections in order to test controller functions.</span></span>

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a><span data-ttu-id="ba7f0-185">執行一般儲存機制和工作單位類別</span><span class="sxs-lookup"><span data-stu-id="ba7f0-185">Implement a Generic Repository and a Unit of Work Class</span></span>

<span data-ttu-id="ba7f0-186">建立每個實體類型的存放庫類別可能會產生許多多餘的程式碼，而且可能會產生部分更新。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-186">Creating a repository class for each entity type could result in a lot of redundant code, and it could result in partial updates.</span></span> <span data-ttu-id="ba7f0-187">例如，假設您必須更新兩個不同的實體類型，做為相同交易的一部分。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-187">For example, suppose you have to update two different entity types as part of the same transaction.</span></span> <span data-ttu-id="ba7f0-188">如果每個都使用個別的資料庫內容實例，則可能會成功，另一個則可能失敗。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-188">If each uses a separate database context instance, one might succeed and the other might fail.</span></span> <span data-ttu-id="ba7f0-189">將多餘的程式碼減到最少的方法之一，就是使用一般存放庫，另一種方法是確保所有儲存機制都使用相同的資料庫內容（因此協調所有更新）是使用工作單位類別。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-189">One way to minimize redundant code is to use a generic repository, and one way to ensure that all repositories use the same database context (and thus coordinate all updates) is to use a unit of work class.</span></span>

<span data-ttu-id="ba7f0-190">在本教學課程的這一節中，您將建立 `GenericRepository` 類別和 `UnitOfWork` 類別，並在 `Course` 控制器中使用它們來存取 `Department` 和 `Course` 實體集。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-190">In this section of the tutorial, you'll create a `GenericRepository` class and a `UnitOfWork` class, and use them in the `Course` controller to access both the `Department` and the `Course` entity sets.</span></span> <span data-ttu-id="ba7f0-191">如先前所述，為了讓教學課程的這個部分簡單明瞭，您不會為這些類別建立介面。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-191">As explained earlier, to keep this part of the tutorial simple, you aren't creating interfaces for these classes.</span></span> <span data-ttu-id="ba7f0-192">但是，如果您要使用它們來加速 TDD，通常會使用與 `Student` 存放庫相同的方式來執行介面。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-192">But if you were going to use them to facilitate TDD, you'd typically implement them with interfaces the same way you did the `Student` repository.</span></span>

### <a name="create-a-generic-repository"></a><span data-ttu-id="ba7f0-193">建立一般存放庫</span><span class="sxs-lookup"><span data-stu-id="ba7f0-193">Create a Generic Repository</span></span>

<span data-ttu-id="ba7f0-194">在*DAL*資料夾中，建立*GenericRepository.cs* ，並將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-194">In the *DAL* folder, create *GenericRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="ba7f0-195">類別變數是針對資料庫內容，以及存放庫已具現化之實體集的宣告：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-195">Class variables are declared for the database context and for the entity set that the repository is instantiated for:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="ba7f0-196">此函式會接受資料庫內容實例，並初始化實體集變數：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-196">The constructor accepts a database context instance and initializes the entity set variable:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="ba7f0-197">`Get` 方法會使用 lambda 運算式來允許呼叫程式碼指定篩選準則和用來排序結果的資料行，而字串參數可讓呼叫者提供以逗號分隔的導覽屬性清單，以供立即載入：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-197">The `Get` method uses lambda expressions to allow the calling code to specify a filter condition and a column to order the results by, and a string parameter lets the caller provide a comma-delimited list of navigation properties for eager loading:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="ba7f0-198">程式碼 `Expression<Func<TEntity, bool>> filter` 表示呼叫端將根據 `TEntity` 型別提供 lambda 運算式，而此運算式會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-198">The code `Expression<Func<TEntity, bool>> filter` means the caller will provide a lambda expression based on the `TEntity` type, and this expression will return a Boolean value.</span></span> <span data-ttu-id="ba7f0-199">例如，如果為 `Student` 實體類型具現化存放庫，則呼叫方法中的程式碼可能會為 `filter` 參數指定 `student => student.LastName == "Smith`&quot;。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-199">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `student => student.LastName == "Smith`&quot; for the `filter` parameter.</span></span>

<span data-ttu-id="ba7f0-200">程式碼 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 也表示呼叫端會提供 lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-200">The code `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` also means the caller will provide a lambda expression.</span></span> <span data-ttu-id="ba7f0-201">但是在此情況下，運算式的輸入是 `TEntity` 類型的 `IQueryable` 物件。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-201">But in this case, the input to the expression is an `IQueryable` object for the `TEntity` type.</span></span> <span data-ttu-id="ba7f0-202">運算式會傳回該 `IQueryable` 物件的已排序版本。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-202">The expression will return an ordered version of that `IQueryable` object.</span></span> <span data-ttu-id="ba7f0-203">例如，如果為 `Student` 實體類型具現化存放庫，則呼叫方法中的程式碼可能會指定 `orderBy` 參數的 `q => q.OrderBy(s => s.LastName)`。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-203">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `q => q.OrderBy(s => s.LastName)` for the `orderBy` parameter.</span></span>

<span data-ttu-id="ba7f0-204">`Get` 方法中的程式碼會建立 `IQueryable` 物件，然後套用篩選條件運算式（如果有的話）：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-204">The code in the `Get` method creates an `IQueryable` object and then applies the filter expression if there is one:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="ba7f0-205">接下來，它會在剖析逗號分隔清單之後套用立即載入運算式：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-205">Next it applies the eager-loading expressions after parsing the comma-delimited list:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="ba7f0-206">最後，它會套用 `orderBy` 運算式（如果有的話），並傳回結果。否則，它會傳回未排序查詢的結果：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-206">Finally, it applies the `orderBy` expression if there is one and returns the results; otherwise it returns the results from the unordered query:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="ba7f0-207">當您呼叫 `Get` 方法時，您可以對方法所傳回的 `IEnumerable` 集合進行篩選和排序，而不是提供這些函式的參數。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-207">When you call the `Get` method, you could do filtering and sorting on the `IEnumerable` collection returned by the method instead of providing parameters for these functions.</span></span> <span data-ttu-id="ba7f0-208">但是排序和篩選工作會在 web 伺服器的記憶體中完成。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-208">But the sorting and filtering work would then be done in memory on the web server.</span></span> <span data-ttu-id="ba7f0-209">藉由使用這些參數，您可以確保工作是由資料庫執行，而不是 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-209">By using these parameters, you ensure that the work is done by the database rather than the web server.</span></span> <span data-ttu-id="ba7f0-210">另一個替代方式是建立特定實體類型的衍生類別，並加入特殊的 `Get` 方法，例如 `GetStudentsInNameOrder` 或 `GetStudentsByName`。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-210">An alternative is to create derived classes for specific entity types and add specialized `Get` methods, such as `GetStudentsInNameOrder` or `GetStudentsByName`.</span></span> <span data-ttu-id="ba7f0-211">不過，在複雜的應用程式中，這可能會產生大量的這類衍生類別和特殊方法，這可能是更多工具來維護。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-211">However, in a complex application, this can result in a large number of such derived classes and specialized methods, which could be more work to maintain.</span></span>

<span data-ttu-id="ba7f0-212">`GetByID`、`Insert`和 `Update` 方法中的程式碼，與您在非泛型存放庫中看到的類似。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-212">The code in the `GetByID`, `Insert`, and `Update` methods is similar to what you saw in the non-generic repository.</span></span> <span data-ttu-id="ba7f0-213">（您不會在 `GetByID` 簽章中提供積極的載入參數，因為您無法使用 `Find` 方法執行積極式載入）。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-213">(You aren't providing an eager loading parameter in the `GetByID` signature, because you can't do eager loading with the `Find` method.)</span></span>

<span data-ttu-id="ba7f0-214">`Delete` 的方法會提供兩個多載：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-214">Two overloads are provided for the `Delete` method:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

<span data-ttu-id="ba7f0-215">其中一個可讓您只傳入要刪除之實體的識別碼，另一個則採用實體實例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-215">One of these lets you pass in just the ID of the entity to be deleted, and one takes an entity instance.</span></span> <span data-ttu-id="ba7f0-216">如您在[處理並行](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)處理教學課程中所見，針對並行處理，您需要一個 `Delete` 方法，以使用包含追蹤屬性之原始值的實體實例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-216">As you saw in the [Handling Concurrency](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial, for concurrency handling you need a `Delete` method that takes an entity instance that includes the original value of a tracking property.</span></span>

<span data-ttu-id="ba7f0-217">這個一般存放庫會處理一般 CRUD 需求。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-217">This generic repository will handle typical CRUD requirements.</span></span> <span data-ttu-id="ba7f0-218">當特定實體類型具有特殊需求（例如更複雜的篩選或排序）時，您可以建立具有該類型之其他方法的衍生類別。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-218">When a particular entity type has special requirements, such as more complex filtering or ordering, you can create a derived class that has additional methods for that type.</span></span>

## <a name="creating-the-unit-of-work-class"></a><span data-ttu-id="ba7f0-219">建立工作單位類別</span><span class="sxs-lookup"><span data-stu-id="ba7f0-219">Creating the Unit of Work Class</span></span>

<span data-ttu-id="ba7f0-220">工作單位類別有一個用途：為了確保當您使用多個存放庫時，它們會共用單一資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-220">The unit of work class serves one purpose: to make sure that when you use multiple repositories, they share a single database context.</span></span> <span data-ttu-id="ba7f0-221">如此一來，當工作單位完成時，您就可以在該內容實例上呼叫 `SaveChanges` 方法，並確保所有相關的變更都將會協調。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-221">That way, when a unit of work is complete you can call the `SaveChanges` method on that instance of the context and be assured that all related changes will be coordinated.</span></span> <span data-ttu-id="ba7f0-222">類別所需的全部都是 `Save` 方法和每個存放庫的屬性。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-222">All that the class needs is a `Save` method and a property for each repository.</span></span> <span data-ttu-id="ba7f0-223">每個存放庫屬性都會傳回已使用與其他存放庫實例相同的資料庫內容實例具現化的存放庫實例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-223">Each repository property returns a repository instance that has been instantiated using the same database context instance as the other repository instances.</span></span>

<span data-ttu-id="ba7f0-224">在*DAL*資料夾中，建立名為*UnitOfWork.cs*的類別檔案，並以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-224">In the *DAL* folder, create a class file named *UnitOfWork.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="ba7f0-225">此程式碼會建立資料庫內容和每個存放庫的類別變數。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-225">The code creates class variables for the database context and each repository.</span></span> <span data-ttu-id="ba7f0-226">若為 `context` 變數，則會具現化新的內容：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-226">For the `context` variable, a new context is instantiated:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="ba7f0-227">每個存放庫屬性都會檢查存放庫是否已經存在。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-227">Each repository property checks whether the repository already exists.</span></span> <span data-ttu-id="ba7f0-228">如果不是，則會具現化存放庫，並傳入內容實例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-228">If not, it instantiates the repository, passing in the context instance.</span></span> <span data-ttu-id="ba7f0-229">因此，所有存放庫都會共用相同的內容實例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-229">As a result, all repositories share the same context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="ba7f0-230">`Save` 方法會在資料庫內容上呼叫 `SaveChanges`。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-230">The `Save` method calls `SaveChanges` on the database context.</span></span>

<span data-ttu-id="ba7f0-231">就像在類別變數中具現化資料庫內容的任何類別一樣，`UnitOfWork` 類別會執行 `IDisposable` 並處置內容。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-231">Like any class that instantiates a database context in a class variable, the `UnitOfWork` class implements `IDisposable` and disposes the context.</span></span>

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a><span data-ttu-id="ba7f0-232">變更課程式控制制器以使用 UnitOfWork 類別和存放庫</span><span class="sxs-lookup"><span data-stu-id="ba7f0-232">Changing the Course Controller to use the UnitOfWork Class and Repositories</span></span>

<span data-ttu-id="ba7f0-233">以下列程式碼取代您目前在*CourseController.cs*中擁有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="ba7f0-233">Replace the code you currently have in *CourseController.cs* with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

<span data-ttu-id="ba7f0-234">此程式碼會新增 `UnitOfWork` 類別的類別變數。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-234">This code adds a class variable for the `UnitOfWork` class.</span></span> <span data-ttu-id="ba7f0-235">（如果您在這裡使用介面，就不會在這裡初始化變數; 相反地，您會實作為 `Student` 儲存機制的兩個參數模式）。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-235">(If you were using interfaces here, you wouldn't initialize the variable here; instead, you'd implement a pattern of two constructors just as you did for the `Student` repository.)</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="ba7f0-236">在類別的其餘部分中，資料庫內容的所有參考都會以適當存放庫的參考取代，並使用 `UnitOfWork` 屬性來存取存放庫。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-236">In the rest of the class, all references to the database context are replaced by references to the appropriate repository, using `UnitOfWork` properties to access the repository.</span></span> <span data-ttu-id="ba7f0-237">`Dispose` 方法會處置 `UnitOfWork` 實例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-237">The `Dispose` method disposes the `UnitOfWork` instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="ba7f0-238">執行網站，然後按一下 [**課程**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-238">Run the site and click the **Courses** tab.</span></span>

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="ba7f0-240">頁面的外觀和運作方式與變更之前相同，而其他課程也相同。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-240">The page looks and works the same as it did before your changes, and the other Course pages also work the same.</span></span>

## <a name="summary"></a><span data-ttu-id="ba7f0-241">總結</span><span class="sxs-lookup"><span data-stu-id="ba7f0-241">Summary</span></span>

<span data-ttu-id="ba7f0-242">您現在已同時執行存放庫和工作單位模式。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-242">You have now implemented both the repository and unit of work patterns.</span></span> <span data-ttu-id="ba7f0-243">您已使用 lambda 運算式做為一般存放庫中的方法參數。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-243">You have used lambda expressions as method parameters in the generic repository.</span></span> <span data-ttu-id="ba7f0-244">如需如何搭配 `IQueryable` 物件使用這些運算式的詳細資訊，請參閱 MSDN Library 中的[IQueryable （t）介面（system.string）](https://msdn.microsoft.com/library/bb351562.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-244">For more information about how to use these expressions with an `IQueryable` object, see [IQueryable(T) Interface (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) in the MSDN Library.</span></span> <span data-ttu-id="ba7f0-245">在下一個教學課程中，您將瞭解如何處理一些先進的案例。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-245">In the next tutorial you'll learn how to handle some advanced scenarios.</span></span>

<span data-ttu-id="ba7f0-246">您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="ba7f0-246">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ba7f0-247">[上一頁](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一頁](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="ba7f0-247">[Previous](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
