---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中使用 EF 讀取相關資料
description: 在本教學課程中，您將讀取並顯示相關資料，也就是 Entity Framework 載入導覽屬性的資料。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445656"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="b83f6-103">教學課程：在 ASP.NET MVC 應用程式中使用 EF 讀取相關資料</span><span class="sxs-lookup"><span data-stu-id="b83f6-103">Tutorial: Read related data with EF in an ASP.NET MVC app</span></span>

<span data-ttu-id="b83f6-104">在上一個教學課程中，您已完成 School 資料模型。</span><span class="sxs-lookup"><span data-stu-id="b83f6-104">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="b83f6-105">在本教學課程中，您將讀取並顯示相關資料，也就是 Entity Framework 載入導覽屬性的資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-105">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="b83f6-106">下列圖例顯示了您將操作的頁面。</span><span class="sxs-lookup"><span data-stu-id="b83f6-106">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[<span data-ttu-id="b83f6-108">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="b83f6-108">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> <span data-ttu-id="b83f6-109">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 6 Code First 和 Visual Studio 來建立 ASP.NET MVC 5 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b83f6-109">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio.</span></span> <span data-ttu-id="b83f6-110">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="b83f6-110">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="b83f6-111">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="b83f6-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b83f6-112">了解如何載入相關資料</span><span class="sxs-lookup"><span data-stu-id="b83f6-112">Learn how to load related data</span></span>
> * <span data-ttu-id="b83f6-113">建立 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="b83f6-113">Create a Courses page</span></span>
> * <span data-ttu-id="b83f6-114">建立 Instructors 頁面</span><span class="sxs-lookup"><span data-stu-id="b83f6-114">Create an Instructors page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b83f6-115">先決條件</span><span class="sxs-lookup"><span data-stu-id="b83f6-115">Prerequisites</span></span>

* [<span data-ttu-id="b83f6-116">建立更複雜的資料模型</span><span class="sxs-lookup"><span data-stu-id="b83f6-116">Create a more complex data model</span></span>](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a><span data-ttu-id="b83f6-117">了解如何載入相關資料</span><span class="sxs-lookup"><span data-stu-id="b83f6-117">Learn how to load related data</span></span>

<span data-ttu-id="b83f6-118">Entity Framework 可以透過數種方式將相關資料載入至實體的導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="b83f6-118">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="b83f6-119">*消極式載入*。</span><span class="sxs-lookup"><span data-stu-id="b83f6-119">*Lazy loading*.</span></span> <span data-ttu-id="b83f6-120">第一次讀取實體時，不會擷取相關資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-120">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="b83f6-121">不過，第一次嘗試存取導覽屬性時，將會自動擷取該導覽屬性所需的資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-121">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="b83f6-122">這會導致多個查詢傳送至資料庫，一個用於實體本身，而每次必須取得實體的相關資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-122">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> <span data-ttu-id="b83f6-123">`DbContext` 類別預設會啟用消極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-123">The `DbContext` class enables lazy loading by default.</span></span>

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="b83f6-125">*積極式載入*。</span><span class="sxs-lookup"><span data-stu-id="b83f6-125">*Eager loading*.</span></span> <span data-ttu-id="b83f6-126">讀取實體時，將會同時擷取其相關資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-126">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="b83f6-127">這通常會導致單一聯結查詢，其可擷取所有需要的資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-127">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="b83f6-128">您可以使用 `Include` 方法來指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-128">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="b83f6-130">*明確式載入*。</span><span class="sxs-lookup"><span data-stu-id="b83f6-130">*Explicit loading*.</span></span> <span data-ttu-id="b83f6-131">這類似于消極式載入，不同之處在于您在程式碼中明確地取得相關資料。當您存取導覽屬性時，不會自動進行此動作。</span><span class="sxs-lookup"><span data-stu-id="b83f6-131">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="b83f6-132">您可以手動載入相關資料，方法是取得實體的物件狀態管理員專案，並針對保留單一實體的屬性呼叫[集合](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)、[載入](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="b83f6-132">You load related data manually by getting the object state manager entry for an entity and calling the [Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) method for collections or the [Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) method for properties that hold a single entity.</span></span> <span data-ttu-id="b83f6-133">（在下列範例中，如果您想要載入 [系統管理員] 導覽屬性，請將 `Collection(x => x.Courses)` 取代為 `Reference(x => x.Administrator)`）。通常只有在您關閉延遲載入時，才會使用明確載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-133">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.) Typically you'd use explicit loading only when you've turned lazy loading off.</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="b83f6-135">因為它們不會立即取得屬性值，所以消極式載入和明確載入也稱為*延後載入*。</span><span class="sxs-lookup"><span data-stu-id="b83f6-135">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

### <a name="performance-considerations"></a><span data-ttu-id="b83f6-136">效能考量</span><span class="sxs-lookup"><span data-stu-id="b83f6-136">Performance considerations</span></span>

<span data-ttu-id="b83f6-137">如果您知道擷取的每個實體需要相關資料，積極式載入通常可以提供最佳效能，因為傳送至資料庫的單一查詢通常比所擷取每個實體的個別查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="b83f6-137">If you know you need related data for every entity retrieved, eager loading often offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="b83f6-138">例如，在上述範例中，假設每個部門都有十個相關課程。</span><span class="sxs-lookup"><span data-stu-id="b83f6-138">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="b83f6-139">積極式載入範例只會產生單一（聯結）查詢，以及對資料庫的單一往返行程。</span><span class="sxs-lookup"><span data-stu-id="b83f6-139">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="b83f6-140">消極式載入和明確載入範例都會導致十個查詢，以及11個對資料庫的往返。</span><span class="sxs-lookup"><span data-stu-id="b83f6-140">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="b83f6-141">當延遲很高時，資料庫的額外來回行程對效能特別不利。</span><span class="sxs-lookup"><span data-stu-id="b83f6-141">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="b83f6-142">另一方面，在某些情況下，延遲載入會更有效率。</span><span class="sxs-lookup"><span data-stu-id="b83f6-142">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="b83f6-143">積極式載入可能會產生非常複雜的聯結，因此 SQL Server 無法有效率地處理。</span><span class="sxs-lookup"><span data-stu-id="b83f6-143">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="b83f6-144">或者，如果您只需要針對所處理的一組實體子集存取實體的導覽屬性，則消極式載入的執行效果可能較佳，因為積極式載入會抓取比您所需更多的資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-144">Or if you need to access an entity's navigation properties only for a subset of a set of the entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="b83f6-145">如果效能嚴重不足，最好先測試這兩種方式的效能，才能做出最好的選擇。</span><span class="sxs-lookup"><span data-stu-id="b83f6-145">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="b83f6-146">消極式載入可以遮罩會造成效能問題的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b83f6-146">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="b83f6-147">例如，未指定積極式或明確載入，但處理大量實體並在每個反復專案中使用多個導覽屬性的程式碼，可能會非常沒有效率（因為有許多對資料庫的來回行程）。</span><span class="sxs-lookup"><span data-stu-id="b83f6-147">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="b83f6-148">在使用內部部署 SQL server 執行良好開發的應用程式，可能會在因為延遲和延遲載入增加而移至 Azure SQL Database 時，發生效能問題。</span><span class="sxs-lookup"><span data-stu-id="b83f6-148">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="b83f6-149">使用實際的測試負載來分析資料庫查詢，可協助您判斷延遲載入是否合適。</span><span class="sxs-lookup"><span data-stu-id="b83f6-149">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="b83f6-150">如需詳細資訊，請參閱[揭密 Entity Framework 策略：載入相關資料](https://msdn.microsoft.com/magazine/hh205756.aspx)和[使用 Entity Framework，以減少 SQL Azure 的網路延遲](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b83f6-150">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

### <a name="disable-lazy-loading-before-serialization"></a><span data-ttu-id="b83f6-151">序列化前停用消極式載入</span><span class="sxs-lookup"><span data-stu-id="b83f6-151">Disable lazy loading before serialization</span></span>

<span data-ttu-id="b83f6-152">如果您在序列化期間讓消極式載入保持啟用狀態，您最後可以查詢的資料會比您預期的還要多。</span><span class="sxs-lookup"><span data-stu-id="b83f6-152">If you leave lazy loading enabled during serialization, you can end up querying significantly more data than you intended.</span></span> <span data-ttu-id="b83f6-153">序列化通常會藉由存取類型實例上的每個屬性來運作。</span><span class="sxs-lookup"><span data-stu-id="b83f6-153">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="b83f6-154">屬性存取會觸發消極式載入，而那些延遲載入的實體也會序列化。</span><span class="sxs-lookup"><span data-stu-id="b83f6-154">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="b83f6-155">然後，序列化程式會存取延遲載入之實體的每個屬性，可能會導致更多的延遲載入和序列化。</span><span class="sxs-lookup"><span data-stu-id="b83f6-155">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="b83f6-156">若要避免這個回合鏈回應，請在序列化實體之前，關閉延遲載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-156">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="b83f6-157">序列化也可能會因為 Entity Framework 所使用的 proxy 類別而複雜，如[Advanced 案例教學](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)課程中所述。</span><span class="sxs-lookup"><span data-stu-id="b83f6-157">Serialization can also be complicated by the proxy classes that the Entity Framework uses, as explained in the [Advanced Scenarios tutorial](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies).</span></span>

<span data-ttu-id="b83f6-158">避免序列化問題的其中一種方法是序列化資料傳輸物件（Dto），而不是實體物件，如[使用 WEB API 與 Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)教學課程中所示。</span><span class="sxs-lookup"><span data-stu-id="b83f6-158">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) tutorial.</span></span>

<span data-ttu-id="b83f6-159">如果您不使用 Dto，您可以停用消極式載入，並藉由[停用 proxy 建立](https://msdn.microsoft.com/data/jj592886.aspx)來避免 proxy 問題。</span><span class="sxs-lookup"><span data-stu-id="b83f6-159">If you don't use DTOs, you can disable lazy loading and avoid proxy issues by [disabling proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>

<span data-ttu-id="b83f6-160">以下是停用消極式載入的一些其他[方法](https://msdn.microsoft.com/data/jj574232)：</span><span class="sxs-lookup"><span data-stu-id="b83f6-160">Here are some other [ways to disable lazy loading](https://msdn.microsoft.com/data/jj574232):</span></span>

- <span data-ttu-id="b83f6-161">針對特定導覽屬性，當您宣告屬性時，請省略 `virtual` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="b83f6-161">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="b83f6-162">針對所有導覽屬性，將 `LazyLoadingEnabled` 設定為 `false`，將下列程式碼放入內容類別的函式中：</span><span class="sxs-lookup"><span data-stu-id="b83f6-162">For all navigation properties, set `LazyLoadingEnabled` to `false`, put the following code in the constructor of your context class:</span></span>

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a><span data-ttu-id="b83f6-163">建立 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="b83f6-163">Create a Courses page</span></span>

<span data-ttu-id="b83f6-164">`Course` 實體包含一個導覽屬性，其中包含課程所指派之部門的 `Department` 實體。</span><span class="sxs-lookup"><span data-stu-id="b83f6-164">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="b83f6-165">若要在課程清單中顯示所指派部門的名稱，您需要從 `Course.Department` 導覽屬性中的 `Department` 實體取得 [`Name`] 屬性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-165">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="b83f6-166">使用您稍早針對 `Student` 控制器執行的 Entity Framework scaffolder，為 `Course` 實體類型建立名為 `CourseController` （非 CoursesController）的控制器，方法是使用**具有 views 的 MVC 5 控制器**的相同選項：</span><span class="sxs-lookup"><span data-stu-id="b83f6-166">Create a controller named `CourseController` (not CoursesController) for the `Course` entity type, using the same options for the **MVC 5 Controller with views, using Entity Framework** scaffolder that you did earlier for the `Student` controller:</span></span>

| <span data-ttu-id="b83f6-167">設定</span><span class="sxs-lookup"><span data-stu-id="b83f6-167">Setting</span></span> | <span data-ttu-id="b83f6-168">值</span><span class="sxs-lookup"><span data-stu-id="b83f6-168">Value</span></span> |
| ------- | ----- |
| <span data-ttu-id="b83f6-169">模型類別</span><span class="sxs-lookup"><span data-stu-id="b83f6-169">Model class</span></span> | <span data-ttu-id="b83f6-170">選取 **[課程] （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="b83f6-170">Select **Course (ContosoUniversity.Models)**.</span></span> |
| <span data-ttu-id="b83f6-171">資料內容類別</span><span class="sxs-lookup"><span data-stu-id="b83f6-171">Data context class</span></span> | <span data-ttu-id="b83f6-172">選取 **[SchoolCoNtext （ContosoUniversity）** ]。</span><span class="sxs-lookup"><span data-stu-id="b83f6-172">Select **SchoolContext (ContosoUniversity.DAL)**.</span></span> |
| <span data-ttu-id="b83f6-173">控制器名稱</span><span class="sxs-lookup"><span data-stu-id="b83f6-173">Controller name</span></span> | <span data-ttu-id="b83f6-174">輸入*CourseController*。</span><span class="sxs-lookup"><span data-stu-id="b83f6-174">Enter *CourseController*.</span></span> <span data-ttu-id="b83f6-175">同樣地，不是以*s* *CoursesController* 。</span><span class="sxs-lookup"><span data-stu-id="b83f6-175">Again, not *CoursesController* with an *s*.</span></span> <span data-ttu-id="b83f6-176">當您選取 [**課程（ContosoUniversity）** ] 時，會自動填入 [**控制器名稱**] 值。</span><span class="sxs-lookup"><span data-stu-id="b83f6-176">When you selected **Course (ContosoUniversity.Models)**, the **Controller name** value was automatically populated.</span></span> <span data-ttu-id="b83f6-177">您必須變更此值。</span><span class="sxs-lookup"><span data-stu-id="b83f6-177">You have to change the value.</span></span> |

<span data-ttu-id="b83f6-178">保留其他預設值，並加入控制器。</span><span class="sxs-lookup"><span data-stu-id="b83f6-178">Leave the other default values and add the controller.</span></span>

<span data-ttu-id="b83f6-179">開啟*Controllers\CourseController.cs* ，並查看 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="b83f6-179">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="b83f6-180">自動 Scaffolding 已使用 `Department` 方法，針對 `Include` 導覽屬性指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-180">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="b83f6-181">開啟*Views\Course\Index.cshtml* ，並將範本程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b83f6-181">Open *Views\Course\Index.cshtml* and replace the template code with the following code.</span></span> <span data-ttu-id="b83f6-182">所做的變更已醒目標示：</span><span class="sxs-lookup"><span data-stu-id="b83f6-182">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

<span data-ttu-id="b83f6-183">您已對包含 Scaffold 的程式碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="b83f6-183">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="b83f6-184">已將標題從 [**索引**] 變更為 [**課程**]。</span><span class="sxs-lookup"><span data-stu-id="b83f6-184">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="b83f6-185">新增顯示  **屬性值的 [編號]** `CourseID` 資料行。</span><span class="sxs-lookup"><span data-stu-id="b83f6-185">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="b83f6-186">根據預設，主要金鑰不會 scaffold，因為它們通常對一般使用者來說毫無意義。</span><span class="sxs-lookup"><span data-stu-id="b83f6-186">By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="b83f6-187">不過，在此情況下主索引鍵有意義，因此您想要顯示它。</span><span class="sxs-lookup"><span data-stu-id="b83f6-187">However, in this case the primary key is meaningful and you want to show it.</span></span>
- <span data-ttu-id="b83f6-188">將 [**部門**] 資料行移至右側，並變更其標題。</span><span class="sxs-lookup"><span data-stu-id="b83f6-188">Moved the **Department** column to the right side and changed its heading.</span></span> <span data-ttu-id="b83f6-189">Scaffolder 正確地選擇要從 `Department` 實體顯示 `Name` 屬性，但在課程頁面中，資料行標題應該是**部門**，而不是**名稱**。</span><span class="sxs-lookup"><span data-stu-id="b83f6-189">The scaffolder correctly chose to display the `Name` property from the `Department` entity, but here in the Course page the column heading should be **Department** rather than **Name**.</span></span>

<span data-ttu-id="b83f6-190">請注意，對於 [部門] 資料行，scaffold 程式碼會顯示載入 `Department` 導覽屬性之 `Department` 實體的 `Name` 屬性：</span><span class="sxs-lookup"><span data-stu-id="b83f6-190">Notice that for the Department column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="b83f6-191">執行頁面（選取 Contoso 大學首頁上的 [**課程**] 索引標籤），以查看具有部門名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="b83f6-191">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

## <a name="create-an-instructors-page"></a><span data-ttu-id="b83f6-192">建立 Instructors 頁面</span><span class="sxs-lookup"><span data-stu-id="b83f6-192">Create an Instructors page</span></span>

<span data-ttu-id="b83f6-193">在本節中，您將建立 `Instructor` 實體的控制器和視圖，以便顯示講師頁面。</span><span class="sxs-lookup"><span data-stu-id="b83f6-193">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors page.</span></span> <span data-ttu-id="b83f6-194">此頁面將以下列方式讀取和顯示相關資料：</span><span class="sxs-lookup"><span data-stu-id="b83f6-194">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="b83f6-195">講師清單會顯示來自 `OfficeAssignment` 實體的相關資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-195">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="b83f6-196">`Instructor` 與 `OfficeAssignment` 實體具有一對零或一關聯性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-196">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="b83f6-197">您將針對 `OfficeAssignment` 的實體使用積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-197">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="b83f6-198">如上所述，當您需要主要資料表中所有擷取資料列的相關資料時，積極式載入通常更有效率。</span><span class="sxs-lookup"><span data-stu-id="b83f6-198">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="b83f6-199">在此情況下，您可能想要顯示所有已呈現講師的辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="b83f6-199">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="b83f6-200">當使用者選取講師時，將會顯示相關的 `Course` 實體。</span><span class="sxs-lookup"><span data-stu-id="b83f6-200">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="b83f6-201">`Instructor` 與 `Course` 實體具有多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-201">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="b83f6-202">您將針對 `Course` 實體和其相關的 `Department` 實體使用積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-202">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="b83f6-203">在此情況下，消極式載入可能會更有效率，因為您只需要所選講師的課程。</span><span class="sxs-lookup"><span data-stu-id="b83f6-203">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="b83f6-204">不過，這個範例會示範如何在本身處於導覽屬性內的實體中，針對導覽屬性使用積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-204">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="b83f6-205">當使用者選取課程時，會顯示來自 `Enrollments` 實體集的相關資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-205">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="b83f6-206">`Course` 與 `Enrollment` 實體具有一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-206">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="b83f6-207">您將為 `Enrollment` 實體和其相關的 `Student` 實體新增明確的載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-207">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="b83f6-208">（不需要明確載入，因為已啟用消極式載入，但這會顯示如何執行明確載入）。</span><span class="sxs-lookup"><span data-stu-id="b83f6-208">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="b83f6-209">建立講師索引視圖的視圖模型</span><span class="sxs-lookup"><span data-stu-id="b83f6-209">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="b83f6-210">講師頁面會顯示三個不同的資料表。</span><span class="sxs-lookup"><span data-stu-id="b83f6-210">The Instructors page shows three different tables.</span></span> <span data-ttu-id="b83f6-211">因此，您將建立包含三個屬性的檢視模型，每個保留其中一個資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="b83f6-211">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="b83f6-212">在*viewmodel*資料夾中，建立*InstructorIndexData.cs* ，並將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b83f6-212">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a><span data-ttu-id="b83f6-213">建立講師控制器和 Views</span><span class="sxs-lookup"><span data-stu-id="b83f6-213">Create the Instructor Controller and Views</span></span>

<span data-ttu-id="b83f6-214">使用 EF 讀取/寫入動作來建立 `InstructorController` （非 InstructorsController）控制器：</span><span class="sxs-lookup"><span data-stu-id="b83f6-214">Create an `InstructorController` (not InstructorsController) controller with EF read/write action:</span></span>

| <span data-ttu-id="b83f6-215">設定</span><span class="sxs-lookup"><span data-stu-id="b83f6-215">Setting</span></span> | <span data-ttu-id="b83f6-216">值</span><span class="sxs-lookup"><span data-stu-id="b83f6-216">Value</span></span> |
| ------- | ----- |
| <span data-ttu-id="b83f6-217">模型類別</span><span class="sxs-lookup"><span data-stu-id="b83f6-217">Model class</span></span> | <span data-ttu-id="b83f6-218">選取 **[講師（ContosoUniversity）** ]。</span><span class="sxs-lookup"><span data-stu-id="b83f6-218">Select **Instructor (ContosoUniversity.Models)**.</span></span> |
| <span data-ttu-id="b83f6-219">資料內容類別</span><span class="sxs-lookup"><span data-stu-id="b83f6-219">Data context class</span></span> | <span data-ttu-id="b83f6-220">選取 **[SchoolCoNtext （ContosoUniversity）** ]。</span><span class="sxs-lookup"><span data-stu-id="b83f6-220">Select **SchoolContext (ContosoUniversity.DAL)**.</span></span> |
| <span data-ttu-id="b83f6-221">控制器名稱</span><span class="sxs-lookup"><span data-stu-id="b83f6-221">Controller name</span></span> | <span data-ttu-id="b83f6-222">輸入*InstructorController*。</span><span class="sxs-lookup"><span data-stu-id="b83f6-222">Enter *InstructorController*.</span></span> <span data-ttu-id="b83f6-223">同樣地，不是以*s* *InstructorsController* 。</span><span class="sxs-lookup"><span data-stu-id="b83f6-223">Again, not *InstructorsController* with an *s*.</span></span> <span data-ttu-id="b83f6-224">當您選取 [**課程（ContosoUniversity）** ] 時，會自動填入 [**控制器名稱**] 值。</span><span class="sxs-lookup"><span data-stu-id="b83f6-224">When you selected **Course (ContosoUniversity.Models)**, the **Controller name** value was automatically populated.</span></span> <span data-ttu-id="b83f6-225">您必須變更此值。</span><span class="sxs-lookup"><span data-stu-id="b83f6-225">You have to change the value.</span></span> |

<span data-ttu-id="b83f6-226">保留其他預設值，並加入控制器。</span><span class="sxs-lookup"><span data-stu-id="b83f6-226">Leave the other default values and add the controller.</span></span>

<span data-ttu-id="b83f6-227">開啟*Controllers\InstructorController.cs* ，並加入 `ViewModels` 命名空間的 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="b83f6-227">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="b83f6-228">`Index` 方法中的 scaffold 程式碼只會針對 `OfficeAssignment` 導覽屬性指定積極式載入：</span><span class="sxs-lookup"><span data-stu-id="b83f6-228">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="b83f6-229">將 `Index` 方法取代為下列程式碼，以載入其他相關資料，並將其放在視圖模型中：</span><span class="sxs-lookup"><span data-stu-id="b83f6-229">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="b83f6-230">方法會接受選擇性的路由資料（`id`）和查詢字串參數（`courseID`），以提供所選講師和所選課程的識別碼值，並將所有必要的資料傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="b83f6-230">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="b83f6-231">這些參數由頁面上的**選取**超連結提供。</span><span class="sxs-lookup"><span data-stu-id="b83f6-231">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

<span data-ttu-id="b83f6-232">此程式碼是從建立檢視模型的執行個體，並將其置於講師清單開始。</span><span class="sxs-lookup"><span data-stu-id="b83f6-232">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="b83f6-233">此程式碼會針對 `Instructor.OfficeAssignment` 和 `Instructor.Courses` 導覽屬性指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-233">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="b83f6-234">第二個 `Include` 方法會載入課程，而針對載入的每個課程，會針對 `Course.Department` 導覽屬性進行積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-234">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="b83f6-235">如先前所述，不需要積極式載入，但會完成以改善效能。</span><span class="sxs-lookup"><span data-stu-id="b83f6-235">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="b83f6-236">由於此視圖一律需要 `OfficeAssignment` 實體，因此在相同的查詢中提取該專案會更有效率。</span><span class="sxs-lookup"><span data-stu-id="b83f6-236">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="b83f6-237">當您在網頁中選取講師時，需要 `Course` 實體，因此，只有在選取的課程比 [沒有] 時，才會顯示 [僅限消極式載入]。</span><span class="sxs-lookup"><span data-stu-id="b83f6-237">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="b83f6-238">如果選取了講師識別碼，則會從視圖模型中的講師清單中抓取選取的講師。</span><span class="sxs-lookup"><span data-stu-id="b83f6-238">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="b83f6-239">然後會從該講師的 `Courses` 導覽屬性中，使用 `Course` 實體載入視圖模型的 `Courses` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-239">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="b83f6-240">`Where` 方法會傳回集合，但在此情況下，傳遞至該方法的準則只會傳回單一 `Instructor` 的實體。</span><span class="sxs-lookup"><span data-stu-id="b83f6-240">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="b83f6-241">`Single` 方法會將集合轉換成單一 `Instructor` 實體，讓您存取該實體的 `Courses` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-241">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="b83f6-242">當您知道集合只會有一個專案時，您可以在集合上使用[單一](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="b83f6-242">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="b83f6-243">如果傳遞給它的集合是空的或有一個以上的專案，`Single` 方法會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b83f6-243">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="b83f6-244">替代方案是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，如果集合是空的，則會傳回預設值（在此案例中為`null`）。</span><span class="sxs-lookup"><span data-stu-id="b83f6-244">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="b83f6-245">不過，在此情況下，仍然會導致例外狀況（嘗試尋找 `null` 參考上的 `Courses` 屬性），而例外狀況訊息則不會清楚指出問題的原因。</span><span class="sxs-lookup"><span data-stu-id="b83f6-245">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="b83f6-246">當您呼叫 `Single` 方法時，您也可以傳入 `Where` 條件，而不是分別呼叫 `Where` 方法：</span><span class="sxs-lookup"><span data-stu-id="b83f6-246">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="b83f6-247">而非：</span><span class="sxs-lookup"><span data-stu-id="b83f6-247">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="b83f6-248">接下來，如果已選取課程，則會從檢視模型的課程清單中擷取選取的課程。</span><span class="sxs-lookup"><span data-stu-id="b83f6-248">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="b83f6-249">然後，視圖模型的 `Enrollments` 屬性會與該課程 `Enrollments` 導覽屬性中的 `Enrollment` 實體一併載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-249">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a><span data-ttu-id="b83f6-250">修改講師索引視圖</span><span class="sxs-lookup"><span data-stu-id="b83f6-250">Modify the Instructor Index View</span></span>

<span data-ttu-id="b83f6-251">在*Views\Instructor\Index.cshtml*中，將範本程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b83f6-251">In *Views\Instructor\Index.cshtml*, replace the template code with the following code.</span></span> <span data-ttu-id="b83f6-252">所做的變更已醒目標示：</span><span class="sxs-lookup"><span data-stu-id="b83f6-252">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

<span data-ttu-id="b83f6-253">您已對現有程式碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="b83f6-253">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="b83f6-254">已將模型類別變更為 `InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="b83f6-254">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="b83f6-255">已將頁面標題從**索引**變更為**講師**。</span><span class="sxs-lookup"><span data-stu-id="b83f6-255">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="b83f6-256">已新增 [ **Office** ] 資料行，只有在 `item.OfficeAssignment` 不是 null 時，才會顯示 `item.OfficeAssignment.Location`。</span><span class="sxs-lookup"><span data-stu-id="b83f6-256">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="b83f6-257">（因為這是一對零或一種關聯性，所以可能不會有相關的 `OfficeAssignment` 實體）。</span><span class="sxs-lookup"><span data-stu-id="b83f6-257">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span>

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- <span data-ttu-id="b83f6-258">新增程式碼，以動態方式將 `class="success"` 新增至所選講師的 `tr` 元素。</span><span class="sxs-lookup"><span data-stu-id="b83f6-258">Added code that will dynamically add `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="b83f6-259">這會使用[啟動](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)程式類別設定所選取資料列的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="b83f6-259">This sets a background color for the selected row using a [Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) class.</span></span>

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- <span data-ttu-id="b83f6-260">在每個資料列的其他連結前面加上標示為 [**選取**] 的新 `ActionLink`，這會導致選取的講師識別碼傳送至 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="b83f6-260">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="b83f6-261">執行應用程式，然後選取 [**講師**] 索引標籤。當沒有相關的 `OfficeAssignment` 實體時，此頁面會顯示相關 `OfficeAssignment` 實體的 `Location` 屬性和空的資料表單元格。</span><span class="sxs-lookup"><span data-stu-id="b83f6-261">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

<span data-ttu-id="b83f6-262">在*Views\Instructor\Index.cshtml*檔案中，于結尾 `table` 專案（在檔案結尾）後面，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b83f6-262">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following code.</span></span> <span data-ttu-id="b83f6-263">當選取講師時，此程式碼會顯示與講師相關的課程。</span><span class="sxs-lookup"><span data-stu-id="b83f6-263">This code displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="b83f6-264">此程式碼會讀取檢視模型的 `Courses` 屬性以顯示課程清單。</span><span class="sxs-lookup"><span data-stu-id="b83f6-264">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="b83f6-265">它也會提供 `Select` 超連結，將所選課程的識別碼傳送至 `Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="b83f6-265">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

<span data-ttu-id="b83f6-266">執行頁面，然後選取講師。</span><span class="sxs-lookup"><span data-stu-id="b83f6-266">Run the page and select an instructor.</span></span> <span data-ttu-id="b83f6-267">現在您會看到一個方格，其中顯示指派給所選取講師的課程，而且在每個課程中，您可以看到指派的部門名稱。</span><span class="sxs-lookup"><span data-stu-id="b83f6-267">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

<span data-ttu-id="b83f6-268">在您剛才新增的程式碼區塊之後，新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b83f6-268">After the code block you just added, add the following code.</span></span> <span data-ttu-id="b83f6-269">這會在選取課程時，顯示已註冊該課程的學生清單。</span><span class="sxs-lookup"><span data-stu-id="b83f6-269">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="b83f6-270">此程式碼會閱讀檢視模型的 `Enrollments` 屬性，以顯示課程中註冊的學生清單。</span><span class="sxs-lookup"><span data-stu-id="b83f6-270">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="b83f6-271">執行頁面，然後選取講師。</span><span class="sxs-lookup"><span data-stu-id="b83f6-271">Run the page and select an instructor.</span></span> <span data-ttu-id="b83f6-272">接著選取課程，以查看已註冊學生和其年級的清單。</span><span class="sxs-lookup"><span data-stu-id="b83f6-272">Then select a course to see the list of enrolled students and their grades.</span></span>

### <a name="adding-explicit-loading"></a><span data-ttu-id="b83f6-273">新增明確載入</span><span class="sxs-lookup"><span data-stu-id="b83f6-273">Adding Explicit Loading</span></span>

<span data-ttu-id="b83f6-274">開啟*InstructorController.cs* ，並查看 `Index` 方法如何取得所選課程的註冊清單：</span><span class="sxs-lookup"><span data-stu-id="b83f6-274">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="b83f6-275">當您抓取講師清單時，您已針對 `Courses` 導覽屬性和每個課程的 `Department` 屬性指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-275">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="b83f6-276">然後將 `Courses` 集合放在視圖模型中，現在您就可以從該集合中的一個實體存取 `Enrollments` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-276">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="b83f6-277">因為您未指定 `Course.Enrollments` 導覽屬性的積極式載入，所以該屬性中的資料會因為消極式載入而出現在頁面中。</span><span class="sxs-lookup"><span data-stu-id="b83f6-277">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="b83f6-278">如果您停用消極式載入，而未以其他方式變更程式碼，則不論該課程實際擁有多少註冊，`Enrollments` 屬性都會是 null。</span><span class="sxs-lookup"><span data-stu-id="b83f6-278">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="b83f6-279">在這種情況下，若要載入 `Enrollments` 屬性，您必須指定積極式載入或明確載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-279">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="b83f6-280">您已經瞭解如何執行積極式載入。</span><span class="sxs-lookup"><span data-stu-id="b83f6-280">You've already seen how to do eager loading.</span></span> <span data-ttu-id="b83f6-281">若要查看明確載入的範例，請以下列程式碼取代 `Index` 方法，這會明確載入 `Enrollments` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b83f6-281">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="b83f6-282">變更的程式碼會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="b83f6-282">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

<span data-ttu-id="b83f6-283">取得選取的 `Course` 實體之後，新的程式碼會明確載入該課程的 `Enrollments` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="b83f6-283">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="b83f6-284">然後，它會明確載入每個 `Enrollment` 實體的相關 `Student` 實體：</span><span class="sxs-lookup"><span data-stu-id="b83f6-284">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="b83f6-285">請注意，您可以使用 `Collection` 方法載入集合屬性，但對於只保存一個實體的屬性，您可以使用 `Reference` 方法。</span><span class="sxs-lookup"><span data-stu-id="b83f6-285">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span>

<span data-ttu-id="b83f6-286">立即執行 [講師索引] 頁面，您會看到頁面上顯示的內容沒有任何差異，雖然您已變更資料的抓取方式。</span><span class="sxs-lookup"><span data-stu-id="b83f6-286">Run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="b83f6-287">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="b83f6-287">Get the code</span></span>

[<span data-ttu-id="b83f6-288">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="b83f6-288">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="b83f6-289">其他資源</span><span class="sxs-lookup"><span data-stu-id="b83f6-289">Additional resources</span></span>

<span data-ttu-id="b83f6-290">您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="b83f6-290">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b83f6-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b83f6-291">Next steps</span></span>

<span data-ttu-id="b83f6-292">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="b83f6-292">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b83f6-293">了解如何載入相關資料</span><span class="sxs-lookup"><span data-stu-id="b83f6-293">Learned how to load related data</span></span>
> * <span data-ttu-id="b83f6-294">建立 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="b83f6-294">Created a Courses page</span></span>
> * <span data-ttu-id="b83f6-295">建立 Instructors 頁面</span><span class="sxs-lookup"><span data-stu-id="b83f6-295">Created an Instructors page</span></span>

<span data-ttu-id="b83f6-296">若要了解如何更新相關資料，請前往下一篇文章。</span><span class="sxs-lookup"><span data-stu-id="b83f6-296">Advance to the next article to learn how to update related data.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b83f6-297">更新相關資料</span><span class="sxs-lookup"><span data-stu-id="b83f6-297">Update related data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
