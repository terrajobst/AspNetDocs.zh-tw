---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: 具有 Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第5部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78527997"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a><span data-ttu-id="85d56-104">Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第5部分</span><span class="sxs-lookup"><span data-stu-id="85d56-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 5</span></span>

<span data-ttu-id="85d56-105">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="85d56-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="85d56-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="85d56-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="85d56-107">如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程</span><span class="sxs-lookup"><span data-stu-id="85d56-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="working-with-related-data-continued"></a><span data-ttu-id="85d56-108">繼續使用相關資料</span><span class="sxs-lookup"><span data-stu-id="85d56-108">Working with Related Data, Continued</span></span>

<span data-ttu-id="85d56-109">在上一個教學課程中，您開始使用 `EntityDataSource` 控制項來處理相關資料。</span><span class="sxs-lookup"><span data-stu-id="85d56-109">In the previous tutorial you began to use the `EntityDataSource` control to work with related data.</span></span> <span data-ttu-id="85d56-110">您在導覽屬性中顯示了多層級的階層和編輯的資料。</span><span class="sxs-lookup"><span data-stu-id="85d56-110">You displayed multiple levels of hierarchy and edited data in navigation properties.</span></span> <span data-ttu-id="85d56-111">在本教學課程中，您將繼續使用相關的資料，方法是新增和刪除關聯性，以及加入與現有實體具有關聯性的新實體。</span><span class="sxs-lookup"><span data-stu-id="85d56-111">In this tutorial you'll continue to work with related data by adding and deleting relationships and by adding a new entity that has a relationship to an existing entity.</span></span>

<span data-ttu-id="85d56-112">您將建立一個頁面，以加入指派給部門的課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-112">You'll create a page that adds courses that are assigned to departments.</span></span> <span data-ttu-id="85d56-113">部門已經存在，而當您建立新的課程時，您將會在這兩者與現有的部門之間建立關聯性。</span><span class="sxs-lookup"><span data-stu-id="85d56-113">The departments already exist, and when you create a new course, at the same time you'll establish a relationship between it and an existing department.</span></span>

<span data-ttu-id="85d56-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="85d56-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span></span>

<span data-ttu-id="85d56-115">您也會建立一個與多對多關聯性搭配運作的頁面，方法是將講師指派給課程（在您選取的兩個實體之間新增關聯性），或從課程中移除講師（移除您的兩個實體之間的關聯性。選取）。</span><span class="sxs-lookup"><span data-stu-id="85d56-115">You'll also create a page that works with a many-to-many relationship by assigning an instructor to a course (adding a relationship between two entities that you select) or removing an instructor from a course (removing a relationship between two entities that you select).</span></span> <span data-ttu-id="85d56-116">在資料庫中，在講師和課程之間加入關聯性，會導致新的資料列加入至 `CourseInstructor` 關聯資料表;移除關聯性牽涉到刪除 `CourseInstructor` 關聯資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="85d56-116">In the database, adding a relationship between an instructor and a course results in a new row being added to the `CourseInstructor` association table; removing a relationship involves deleting a row from the `CourseInstructor` association table.</span></span> <span data-ttu-id="85d56-117">不過，您可以藉由設定導覽屬性在 Entity Framework 中執行此動作，而不需要明確地參考 `CourseInstructor` 資料表。</span><span class="sxs-lookup"><span data-stu-id="85d56-117">However, you do this in the Entity Framework by setting navigation properties, without referring to the `CourseInstructor` table explicitly.</span></span>

<span data-ttu-id="85d56-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="85d56-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span></span>

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a><span data-ttu-id="85d56-119">將具有關聯性的實體加入至現有實體</span><span class="sxs-lookup"><span data-stu-id="85d56-119">Adding an Entity with a Relationship to an Existing Entity</span></span>

<span data-ttu-id="85d56-120">建立名為*CoursesAdd*的新網頁，此網頁會使用*網站*的主版頁面，並將下列標記新增至名為 `Content2`的 `Content` 控制項：</span><span class="sxs-lookup"><span data-stu-id="85d56-120">Create a new web page named *CoursesAdd.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

<span data-ttu-id="85d56-121">此標記會建立一個 `EntityDataSource` 控制項，以選取可進行插入的課程，並指定 `Inserting` 事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="85d56-121">This markup creates an `EntityDataSource` control that selects courses, that enables inserting, and that specifies a handler for the `Inserting` event.</span></span> <span data-ttu-id="85d56-122">建立新的 `Course` 實體時，您將使用處理程式來更新 `Department` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="85d56-122">You'll use the handler to update the `Department` navigation property when a new `Course` entity is created.</span></span>

<span data-ttu-id="85d56-123">標記也會建立用來加入新 `Course` 實體的 `DetailsView` 控制項。</span><span class="sxs-lookup"><span data-stu-id="85d56-123">The markup also creates a `DetailsView` control to use for adding new `Course` entities.</span></span> <span data-ttu-id="85d56-124">標記會使用系結欄位來 `Course` 實體屬性。</span><span class="sxs-lookup"><span data-stu-id="85d56-124">The markup uses bound fields for `Course` entity properties.</span></span> <span data-ttu-id="85d56-125">您必須輸入 `CourseID` 值，因為這不是系統產生的識別碼欄位。</span><span class="sxs-lookup"><span data-stu-id="85d56-125">You have to enter the `CourseID` value because this is not a system-generated ID field.</span></span> <span data-ttu-id="85d56-126">而是課程號碼，必須在課程建立時以手動方式指定。</span><span class="sxs-lookup"><span data-stu-id="85d56-126">Instead, it's a course number that must be specified manually when the course is created.</span></span>

<span data-ttu-id="85d56-127">您可以使用範本欄位做為 `Department` 導覽屬性，因為導覽屬性無法搭配 `BoundField` 控制項使用。</span><span class="sxs-lookup"><span data-stu-id="85d56-127">You use a template field for the `Department` navigation property because navigation properties cannot be used with `BoundField` controls.</span></span> <span data-ttu-id="85d56-128">[範本] 欄位提供下拉式清單來選取部門。</span><span class="sxs-lookup"><span data-stu-id="85d56-128">The template field provides a drop-down list to select the department.</span></span> <span data-ttu-id="85d56-129">因為您無法直接系結導覽屬性來更新它們，所以下拉式清單會使用 `Eval` 而不是 `Bind`，系結至 `Departments` 實體集。</span><span class="sxs-lookup"><span data-stu-id="85d56-129">The drop-down list is bound to the `Departments` entity set by using `Eval` rather than `Bind`, again because you cannot directly bind navigation properties in order to update them.</span></span> <span data-ttu-id="85d56-130">您可以為 `DropDownList` 控制項的 `Init` 事件指定處理常式，以便儲存控制項的參考，供更新 `DepartmentID` 外鍵的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="85d56-130">You specify a handler for the `DropDownList` control's `Init` event so that you can store a reference to the control for use by the code that updates the `DepartmentID` foreign key.</span></span>

<span data-ttu-id="85d56-131">在*CoursesAdd.aspx.cs*的部分類別宣告之後，新增類別欄位以保存 `DepartmentsDropDownList` 控制項的參考：</span><span class="sxs-lookup"><span data-stu-id="85d56-131">In *CoursesAdd.aspx.cs* just after the partial-class declaration, add a class field to hold a reference to the `DepartmentsDropDownList` control:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

<span data-ttu-id="85d56-132">為 `DepartmentsDropDownList` 控制項的 `Init` 事件新增處理常式，以便儲存控制項的參考。</span><span class="sxs-lookup"><span data-stu-id="85d56-132">Add a handler for the `DepartmentsDropDownList` control's `Init` event so that you can store a reference to the control.</span></span> <span data-ttu-id="85d56-133">這可讓您取得使用者已輸入的值，並使用它來更新 `Course` 實體的 `DepartmentID` 值。</span><span class="sxs-lookup"><span data-stu-id="85d56-133">This lets you get the value the user has entered and use it to update the `DepartmentID` value of the `Course` entity.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

<span data-ttu-id="85d56-134">為 `DetailsView` 控制項的 `Inserting` 事件新增處理常式：</span><span class="sxs-lookup"><span data-stu-id="85d56-134">Add a handler for the `DetailsView` control's `Inserting` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

<span data-ttu-id="85d56-135">當使用者按一下 [`Insert`] 時，`Inserting` 事件會在插入新記錄之前引發。</span><span class="sxs-lookup"><span data-stu-id="85d56-135">When the user clicks `Insert`, the `Inserting` event is raised before the new record is inserted.</span></span> <span data-ttu-id="85d56-136">處理常式中的程式碼會從 `DropDownList` 控制項取得 `DepartmentID`，並使用它來設定將用於 `Course` 實體之 `DepartmentID` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="85d56-136">The code in the handler gets the `DepartmentID` from the `DropDownList` control and uses it to set the value that will be used for the `DepartmentID` property of the `Course` entity.</span></span>

<span data-ttu-id="85d56-137">Entity Framework 會負責將這個課程加入至相關聯 `Department` 實體的 `Courses` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="85d56-137">The Entity Framework will take care of adding this course to the `Courses` navigation property of the associated `Department` entity.</span></span> <span data-ttu-id="85d56-138">它也會將部門新增至 `Course` 實體的 `Department` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="85d56-138">It also adds the department to the `Department` navigation property of the `Course` entity.</span></span>

<span data-ttu-id="85d56-139">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="85d56-139">Run the page.</span></span>

<span data-ttu-id="85d56-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="85d56-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span></span>

<span data-ttu-id="85d56-141">輸入識別碼、標題、信用額度數，然後選取部門，然後按一下 [**插入**]。</span><span class="sxs-lookup"><span data-stu-id="85d56-141">Enter an ID, a title, a number of credits, and select a department, then click **Insert**.</span></span>

<span data-ttu-id="85d56-142">執行 [*課程 .aspx* ] 頁面，然後選取相同的部門以查看新的課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-142">Run the *Courses.aspx* page, and select the same department to see the new course.</span></span>

<span data-ttu-id="85d56-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="85d56-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span></span>

## <a name="working-with-many-to-many-relationships"></a><span data-ttu-id="85d56-144">使用多對多關聯性</span><span class="sxs-lookup"><span data-stu-id="85d56-144">Working with Many-to-Many Relationships</span></span>

<span data-ttu-id="85d56-145">`Courses` 實體集和 `People` 實體集之間的關聯性是多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="85d56-145">The relationship between the `Courses` entity set and the `People` entity set is a many-to-many relationship.</span></span> <span data-ttu-id="85d56-146">`Course` 實體具有名為 `People` 的導覽屬性，可包含零個、一個或多個相關的 `Person` 實體（代表指派給教學課程的講師）。</span><span class="sxs-lookup"><span data-stu-id="85d56-146">A `Course` entity has a navigation property named `People` that can contain zero, one, or more related `Person` entities (representing instructors assigned to teach that course).</span></span> <span data-ttu-id="85d56-147">`Person` 實體具有名為 `Courses` 的導覽屬性，其中可包含零個、一個或多個相關的 `Course` 實體（代表講師指派給教授的課程）。</span><span class="sxs-lookup"><span data-stu-id="85d56-147">And a `Person` entity has a navigation property named `Courses` that can contain zero, one, or more related `Course` entities (representing courses that instructor is assigned to teach).</span></span> <span data-ttu-id="85d56-148">一個講師可能會教授多個課程，而一個課程可能會由多個講師教授。</span><span class="sxs-lookup"><span data-stu-id="85d56-148">One instructor might teach multiple courses, and one course might be taught by multiple instructors.</span></span> <span data-ttu-id="85d56-149">在本逐步解說的這一節中，您將會藉由更新相關實體的導覽屬性，來新增和移除 `Person` 和 `Course` 實體之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="85d56-149">In this section of the walkthrough, you'll add and remove relationships between `Person` and `Course` entities by updating the navigation properties of the related entities.</span></span>

<span data-ttu-id="85d56-150">建立名為*InstructorsCourses*的新網頁，此網頁會使用*網站*的主版頁面，並將下列標記新增至名為 `Content2`的 `Content` 控制項：</span><span class="sxs-lookup"><span data-stu-id="85d56-150">Create a new web page named *InstructorsCourses.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

<span data-ttu-id="85d56-151">此標記會建立一個 `EntityDataSource` 控制項，以抓取講師的 `Person` 機構名稱和 `PersonID`。</span><span class="sxs-lookup"><span data-stu-id="85d56-151">This markup creates an `EntityDataSource` control that retrieves the name and `PersonID` of `Person` entities for instructors.</span></span> <span data-ttu-id="85d56-152">`DropDrownList` 控制項系結至 `EntityDataSource` 控制項。</span><span class="sxs-lookup"><span data-stu-id="85d56-152">A `DropDrownList` control is bound to the `EntityDataSource` control.</span></span> <span data-ttu-id="85d56-153">`DropDownList` 控制項會指定 `DataBound` 事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="85d56-153">The `DropDownList` control specifies a handler for the `DataBound` event.</span></span> <span data-ttu-id="85d56-154">您將使用此處理程式來 databind 顯示課程的兩個下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="85d56-154">You'll use this handler to databind the two drop-down lists that display courses.</span></span>

<span data-ttu-id="85d56-155">標記也會建立下列控制項群組，用來將課程指派給選取的講師：</span><span class="sxs-lookup"><span data-stu-id="85d56-155">The markup also creates the following group of controls to use for assigning a course to the selected instructor:</span></span>

- <span data-ttu-id="85d56-156">`DropDownList` 控制項，用於選取要指派的課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-156">A `DropDownList` control for selecting a course to assign.</span></span> <span data-ttu-id="85d56-157">此控制項將會填入目前未指派給所選講師的課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-157">This control will be populated with courses that are currently not assigned to the selected instructor.</span></span>
- <span data-ttu-id="85d56-158">用來起始指派的 `Button` 控制項。</span><span class="sxs-lookup"><span data-stu-id="85d56-158">A `Button` control to initiate the assignment.</span></span>
- <span data-ttu-id="85d56-159">當指派失敗時，用來顯示錯誤訊息的 `Label` 控制項。</span><span class="sxs-lookup"><span data-stu-id="85d56-159">A `Label` control to display an error message if the assignment fails.</span></span>

<span data-ttu-id="85d56-160">最後，標記也會建立一組控制項，用來從選取的講師移除課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-160">Finally, the markup also creates a group of controls to use for removing a course from the selected instructor.</span></span>

<span data-ttu-id="85d56-161">在*InstructorsCourses.aspx.cs*中，新增 using 語句：</span><span class="sxs-lookup"><span data-stu-id="85d56-161">In *InstructorsCourses.aspx.cs*, add a using statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

<span data-ttu-id="85d56-162">新增方法來填入顯示課程的兩個下拉式清單：</span><span class="sxs-lookup"><span data-stu-id="85d56-162">Add a method for populating the two drop-down lists that display courses:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

<span data-ttu-id="85d56-163">此程式碼會從 `Courses` 實體集取得所有課程，並從所選講師的 `Person` 實體 `Courses` 導覽屬性取得課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-163">This code gets all courses from the `Courses` entity set and gets the courses from the `Courses` navigation property of the `Person` entity for the selected instructor.</span></span> <span data-ttu-id="85d56-164">接著，它會決定要指派給該講師的課程，並據此填入下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="85d56-164">It then determines which courses are assigned to that instructor and populates the drop-down lists accordingly.</span></span>

<span data-ttu-id="85d56-165">為 `Assign` 按鈕的 `Click` 事件新增處理常式：</span><span class="sxs-lookup"><span data-stu-id="85d56-165">Add a handler for the `Assign` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

<span data-ttu-id="85d56-166">此程式碼會取得所選講師的 `Person` 實體，取得所選課程的 `Course` 實體，並將選取的課程加入至講師 `Person` 實體的 [`Courses` 導覽] 屬性。</span><span class="sxs-lookup"><span data-stu-id="85d56-166">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and adds the selected course to the `Courses` navigation property of the instructor's `Person` entity.</span></span> <span data-ttu-id="85d56-167">然後，它會將變更儲存到資料庫，並重新填入下拉式清單，以便立即看到結果。</span><span class="sxs-lookup"><span data-stu-id="85d56-167">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="85d56-168">為 `Remove` 按鈕的 `Click` 事件新增處理常式：</span><span class="sxs-lookup"><span data-stu-id="85d56-168">Add a handler for the `Remove` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

<span data-ttu-id="85d56-169">此程式碼會取得所選講師的 `Person` 實體，取得所選課程的 `Course` 實體，並從 `Person` 實體的 `Courses` 導覽屬性中移除選取的課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-169">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and removes the selected course from the `Person` entity's `Courses` navigation property.</span></span> <span data-ttu-id="85d56-170">然後，它會將變更儲存到資料庫，並重新填入下拉式清單，以便立即看到結果。</span><span class="sxs-lookup"><span data-stu-id="85d56-170">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="85d56-171">將程式碼加入至 `Page_Load` 方法，以確保在沒有報告錯誤時看不到錯誤訊息，並為講師下拉式清單的 `DataBound` 和 `SelectedIndexChanged` 事件新增處理常式，以填入課程下拉式清單：</span><span class="sxs-lookup"><span data-stu-id="85d56-171">Add code to the `Page_Load` method that makes sure the error messages are not visible when there's no error to report, and add handlers for the `DataBound` and `SelectedIndexChanged` events of the instructors drop-down list to populate the courses drop-down lists:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

<span data-ttu-id="85d56-172">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="85d56-172">Run the page.</span></span>

<span data-ttu-id="85d56-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="85d56-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span></span>

<span data-ttu-id="85d56-174">選取講師。</span><span class="sxs-lookup"><span data-stu-id="85d56-174">Select an instructor.</span></span> <span data-ttu-id="85d56-175">[<strong>指派課程</strong>] 下拉式清單會顯示講師未教授的課程，而 [<strong>移除課程</strong>] 下拉式清單會顯示講師已指派給的課程。</span><span class="sxs-lookup"><span data-stu-id="85d56-175">The <strong>Assign a Course</strong> drop-down list displays the courses that the instructor doesn't teach, and the <strong>Remove a Course</strong> drop-down list displays the courses that the instructor is already assigned to.</span></span> <span data-ttu-id="85d56-176">在 [<strong>指派課程</strong>] 區段中，選取課程，然後按一下 [<strong>指派</strong>]。</span><span class="sxs-lookup"><span data-stu-id="85d56-176">In the <strong>Assign a Course</strong> section, select a course and then click <strong>Assign</strong>.</span></span> <span data-ttu-id="85d56-177">課程移至 [<strong>移除課程</strong>] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="85d56-177">The course moves to the <strong>Remove a Course</strong> drop-down list.</span></span> <span data-ttu-id="85d56-178">在 [<strong>移除課程</strong>] 區段中選取課程，然後按一下 [<strong>移除</strong>]<em>。</em></span><span class="sxs-lookup"><span data-stu-id="85d56-178">Select a course in the <strong>Remove a Course</strong> section and click <strong>Remove</strong><em>.</em></span></span> <span data-ttu-id="85d56-179">課程會移至 [<strong>指派課程</strong>] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="85d56-179">The course moves to the <strong>Assign a Course</strong> drop-down list.</span></span>

<span data-ttu-id="85d56-180">您現在已經看過一些更多方式來處理相關資料。</span><span class="sxs-lookup"><span data-stu-id="85d56-180">You have now seen some more ways to work with related data.</span></span> <span data-ttu-id="85d56-181">在下列教學課程中，您將瞭解如何在資料模型中使用繼承，以改善應用程式的可維護性。</span><span class="sxs-lookup"><span data-stu-id="85d56-181">In the following tutorial, you'll learn how to use inheritance in the data model to improve the maintainability of your application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="85d56-182">[上一頁](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="85d56-182">[Previous](the-entity-framework-and-aspnet-getting-started-part-4.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-6.md)</span></span>
