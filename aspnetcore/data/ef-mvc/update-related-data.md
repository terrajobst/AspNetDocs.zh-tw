---
title: 教學課程：更新相關資料 - ASP.NET MVC 搭配 EF Core
description: 在本教學課程中，您會藉由更新外部索引鍵欄位和導覽屬性來更新相關資料。
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/05/2019
ms.topic: tutorial
uid: data/ef-mvc/update-related-data
ms.openlocfilehash: ac94f2e2876c2d8d571a451e4641787ffe37b3d2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058325"
---
# <a name="tutorial-update-related-data---aspnet-mvc-with-ef-core"></a><span data-ttu-id="96a8e-103">教學課程：更新相關資料 - ASP.NET MVC 搭配 EF Core</span><span class="sxs-lookup"><span data-stu-id="96a8e-103">Tutorial: Update related data - ASP.NET MVC with EF Core</span></span>

<span data-ttu-id="96a8e-104">在先前的教學課程中，您顯示了相關資料。在本教學課程中，您會藉由更新外部索引鍵欄位和導覽屬性來更新相關資料。</span><span class="sxs-lookup"><span data-stu-id="96a8e-104">In the previous tutorial you displayed related data; in this tutorial you'll update related data by updating foreign key fields and navigation properties.</span></span>

<span data-ttu-id="96a8e-105">下列圖例顯示了您將操作的一些頁面。</span><span class="sxs-lookup"><span data-stu-id="96a8e-105">The following illustrations show some of the pages that you'll work with.</span></span>

![Course [編輯] 頁面](update-related-data/_static/course-edit.png)

![Instructor [編輯] 頁面](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="96a8e-108">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="96a8e-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96a8e-109">自訂 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-109">Customize Courses pages</span></span>
> * <span data-ttu-id="96a8e-110">新增 Instructors [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-110">Add Instructors Edit page</span></span>
> * <span data-ttu-id="96a8e-111">將課程新增至 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-111">Add courses to Edit page</span></span>
> * <span data-ttu-id="96a8e-112">更新 [刪除] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-112">Update Delete page</span></span>
> * <span data-ttu-id="96a8e-113">將辦公室位置和課程新增至 [建立] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-113">Add office location and courses to Create page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96a8e-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="96a8e-114">Prerequisites</span></span>

* [<span data-ttu-id="96a8e-115">使用 EF Core 來讀取 ASP.NET Core MVC Web 應用程式的相關資料</span><span class="sxs-lookup"><span data-stu-id="96a8e-115">Read related data with EF Core for an ASP.NET Core MVC web app</span></span>](read-related-data.md)

## <a name="customize-courses-pages"></a><span data-ttu-id="96a8e-116">自訂 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-116">Customize Courses pages</span></span>

<span data-ttu-id="96a8e-117">當新的課程實體建立時，其必須要與現有的部門具有關聯性。</span><span class="sxs-lookup"><span data-stu-id="96a8e-117">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="96a8e-118">若要達成此目的，Scaffold 程式碼包含了控制器方法和 [建立] 和 [編輯] 檢視，當中包含了一個可選取部門的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="96a8e-118">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="96a8e-119">下拉式清單會設定 `Course.DepartmentID` 外部索引鍵屬性，以讓 Entity Framework 使用適當的 Department 實體載入 `Department` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="96a8e-119">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate Department entity.</span></span> <span data-ttu-id="96a8e-120">您將使用 Scaffold 程式碼，但會稍微對其進行一些變更以新增錯誤處理及排序下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="96a8e-120">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="96a8e-121">在 *CoursesController.cs* 中，刪除四個 Create 及 Edit 方法，並以下列程式碼取代：</span><span class="sxs-lookup"><span data-stu-id="96a8e-121">In *CoursesController.cs*, delete the four Create and Edit methods and replace them with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreateGet)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreatePost)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditGet)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditPost)]

<span data-ttu-id="96a8e-122">在 `Edit` HttpPost 方法後，建立一個新的方法，該方法會將部門資訊載入下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="96a8e-122">After the `Edit` HttpPost method, create a new method that loads department info for the drop-down list.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_Departments)]

<span data-ttu-id="96a8e-123">`PopulateDepartmentsDropDownList` 方法會取得依照名稱排序的所有部門清單，為下拉式清單建立 `SelectList` 集合，然後將集合傳遞給位於 `ViewBag` 中的檢視。</span><span class="sxs-lookup"><span data-stu-id="96a8e-123">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in `ViewBag`.</span></span> <span data-ttu-id="96a8e-124">方法接受選擇性的 `selectedDepartment` 參數，可允許呼叫程式碼在呈現下拉式清單時指定選取的項目。</span><span class="sxs-lookup"><span data-stu-id="96a8e-124">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="96a8e-125">檢視會將名稱 "DepartmentID" 傳遞到 `<select>` 標籤協助程式，協助程式接著便會知道要在 `ViewBag` 物件中尋找一個名為 "DepartmentID" 的 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="96a8e-125">The view will pass the name "DepartmentID" to the `<select>` tag helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named "DepartmentID".</span></span>

<span data-ttu-id="96a8e-126">HttpGet `Create` 方法會呼叫 `PopulateDepartmentsDropDownList` 方法，而不設定選取項目，因為新課程所屬的部門還未建立：</span><span class="sxs-lookup"><span data-stu-id="96a8e-126">The HttpGet `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department isn't established yet:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=3&name=snippet_CreateGet)]

<span data-ttu-id="96a8e-127">HttpGet `Edit` 方法會根據已指派給正在編輯之課程的部門識別碼來設定選取項目：</span><span class="sxs-lookup"><span data-stu-id="96a8e-127">The HttpGet `Edit` method sets the selected item, based on the ID of the department that's already assigned to the course being edited:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=15&name=snippet_EditGet)]

<span data-ttu-id="96a8e-128">`Create` 和 `Edit` 的 HttpPost 方法都同時包含了在錯誤之後重新顯示頁面時設定選取項目的程式碼。</span><span class="sxs-lookup"><span data-stu-id="96a8e-128">The HttpPost methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error.</span></span> <span data-ttu-id="96a8e-129">這可確保當頁面重新顯示以顯示錯誤訊息時，任何已選取的部門都會維持該選取狀態。</span><span class="sxs-lookup"><span data-stu-id="96a8e-129">This ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

### <a name="add-asnotracking-to-details-and-delete-methods"></a><span data-ttu-id="96a8e-130">將 .AsNoTracking 新增至 Details 及 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="96a8e-130">Add .AsNoTracking to Details and Delete methods</span></span>

<span data-ttu-id="96a8e-131">若要最佳化 Course [詳細資料] 和 [刪除] 頁面的效能，請在 `Details` 和 HttpGet `Delete` 方法中新增 `AsNoTracking` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="96a8e-131">To optimize performance of the Course Details and Delete pages, add `AsNoTracking` calls in the `Details` and HttpGet `Delete` methods.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_Details)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_DeleteGet)]

### <a name="modify-the-course-views"></a><span data-ttu-id="96a8e-132">修改 Course 檢視</span><span class="sxs-lookup"><span data-stu-id="96a8e-132">Modify the Course views</span></span>

<span data-ttu-id="96a8e-133">在 *Views/Courses/Create.cshtml* 中，將一個「選取部門」選項新增至 [部門] 下拉式清單，將標題從 **DepartmentID** 變更為 **Department**，然後新增一個驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="96a8e-133">In *Views/Courses/Create.cshtml*, add a "Select Department" option to the **Department** drop-down list, change the caption from **DepartmentID** to **Department**, and add a validation message.</span></span>

[!code-html[](intro/samples/cu/Views/Courses/Create.cshtml?highlight=2-6&range=29-34)]

<span data-ttu-id="96a8e-134">在 *Views/Courses/Edit.cshtml* 中，為 [部門] 欄位進行您剛剛為 *Create.cshtml* 進行的相同變更。</span><span class="sxs-lookup"><span data-stu-id="96a8e-134">In *Views/Courses/Edit.cshtml*, make the same change for the Department field that you just did in *Create.cshtml*.</span></span>

<span data-ttu-id="96a8e-135">同樣的，在 *Views/Courses/Edit.cshtml* 中，在 [標題] 欄位之前新增一個課程號碼欄位。</span><span class="sxs-lookup"><span data-stu-id="96a8e-135">Also in *Views/Courses/Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="96a8e-136">由於課程號碼是主索引鍵，雖然會顯示，但您無法變更它。</span><span class="sxs-lookup"><span data-stu-id="96a8e-136">Because the course number is the primary key, it's displayed, but it can't be changed.</span></span>

[!code-html[](intro/samples/cu/Views/Courses/Edit.cshtml?range=15-18)]

<span data-ttu-id="96a8e-137">在 [編輯] 檢視中已有一個針對課程號碼的隱藏欄位 (`<input type="hidden">`)。</span><span class="sxs-lookup"><span data-stu-id="96a8e-137">There's already a hidden field (`<input type="hidden">`) for the course number in the Edit view.</span></span> <span data-ttu-id="96a8e-138">新增 `<label>` 標籤協助程式無法消除隱藏欄位的必要，因為它無法讓課程號碼包含在使用者按一下位於 [編輯] 頁面上的 [儲存] 時以 Post 方式提交的資料中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-138">Adding a `<label>` tag helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the **Edit** page.</span></span>

<span data-ttu-id="96a8e-139">在 *Views/Courses/Delete.cshtml* 中，在頂端新增一個課程號碼欄位，並將部門識別碼變更為部門名稱。</span><span class="sxs-lookup"><span data-stu-id="96a8e-139">In *Views/Courses/Delete.cshtml*, add a course number field at the top and change department ID to department name.</span></span>

[!code-html[](intro/samples/cu/Views/Courses/Delete.cshtml?highlight=14-19,36)]

<span data-ttu-id="96a8e-140">在 *Views/Courses/Details.cshtml* 中，進行您方才對 *Delete.cshtml* 進行的相同變更。</span><span class="sxs-lookup"><span data-stu-id="96a8e-140">In *Views/Courses/Details.cshtml*, make the same change that you just did for *Delete.cshtml*.</span></span>

### <a name="test-the-course-pages"></a><span data-ttu-id="96a8e-141">測試 Course 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-141">Test the Course pages</span></span>

<span data-ttu-id="96a8e-142">執行應用程式，選取 [Course] 索引標籤，按一下 [新建]，並輸入新的課程資料：</span><span class="sxs-lookup"><span data-stu-id="96a8e-142">Run the app, select the **Courses** tab, click **Create New**, and enter data for a new course:</span></span>

![Course [建立] 頁面](update-related-data/_static/course-create.png)

<span data-ttu-id="96a8e-144">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="96a8e-144">Click **Create**.</span></span> <span data-ttu-id="96a8e-145">Courses [索引] 頁面便會顯示，並且清單中已有新建立的課程。</span><span class="sxs-lookup"><span data-stu-id="96a8e-145">The Courses Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="96a8e-146">[索引] 頁面中的部門名稱來自於導覽屬性，顯示關聯性已正確建立。</span><span class="sxs-lookup"><span data-stu-id="96a8e-146">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

<span data-ttu-id="96a8e-147">按一下 Courses [索引] 頁面中課程的 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="96a8e-147">Click **Edit** on a course in the Courses Index page.</span></span>

![Course [編輯] 頁面](update-related-data/_static/course-edit.png)

<span data-ttu-id="96a8e-149">變更頁面上的資料，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="96a8e-149">Change data on the page and click **Save**.</span></span> <span data-ttu-id="96a8e-150">Courses [索引] 頁面便會顯示，並且清單中已有更新的課程資料。</span><span class="sxs-lookup"><span data-stu-id="96a8e-150">The Courses Index page is displayed with the updated course data.</span></span>

## <a name="add-instructors-edit-page"></a><span data-ttu-id="96a8e-151">新增 Instructors [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-151">Add Instructors Edit page</span></span>

<span data-ttu-id="96a8e-152">當您編輯講師記錄時，您可能會想要更新講師的辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="96a8e-152">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="96a8e-153">Instructor 實體與 OfficeAssignment 實體具有一對零或一關聯性，表示您的程式碼必須處理下列狀況：</span><span class="sxs-lookup"><span data-stu-id="96a8e-153">The Instructor entity has a one-to-zero-or-one relationship with the OfficeAssignment entity, which means your code has to handle the following situations:</span></span>

* <span data-ttu-id="96a8e-154">若使用者清除了原先擁有值的辦公室指派，刪除 OfficeAssignment 實體。</span><span class="sxs-lookup"><span data-stu-id="96a8e-154">If the user clears the office assignment and it originally had a value, delete the OfficeAssignment entity.</span></span>

* <span data-ttu-id="96a8e-155">若使用者輸入了辦公室指派的值，而該指派原先是空白的，請建立新的 OfficeAssignment 實體。</span><span class="sxs-lookup"><span data-stu-id="96a8e-155">If the user enters an office assignment value and it originally was empty, create a new OfficeAssignment entity.</span></span>

* <span data-ttu-id="96a8e-156">若使用者變更辦公室指派的值，請變更現有 OfficeAssignment 實體中的值。</span><span class="sxs-lookup"><span data-stu-id="96a8e-156">If the user changes the value of an office assignment, change the value in an existing OfficeAssignment entity.</span></span>

### <a name="update-the-instructors-controller"></a><span data-ttu-id="96a8e-157">更新 Instructor 控制器</span><span class="sxs-lookup"><span data-stu-id="96a8e-157">Update the Instructors controller</span></span>

<span data-ttu-id="96a8e-158">在 *InstructorsController.cs* 中，變更 HttpGet `Edit` 方法中的程式碼，使其載入 Instructor 實體的 `OfficeAssignment` 導覽屬性，並呼叫 `AsNoTracking`：</span><span class="sxs-lookup"><span data-stu-id="96a8e-158">In *InstructorsController.cs*, change the code in the HttpGet `Edit` method so that it loads the Instructor entity's `OfficeAssignment` navigation property and calls `AsNoTracking`:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=9,10&name=snippet_EditGetOA)]

<span data-ttu-id="96a8e-159">使用下列程式碼取代 HttpPost `Edit` 方法來處理辦公室指派更新：</span><span class="sxs-lookup"><span data-stu-id="96a8e-159">Replace the HttpPost `Edit` method with the following code to handle office assignment updates:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EditPostOA)]

<span data-ttu-id="96a8e-160">程式碼會執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="96a8e-160">The code does the following:</span></span>

-  <span data-ttu-id="96a8e-161">將方法名稱變更為 `EditPost`，因為簽章目前與 HttpGet `Edit` 方法相同 (`ActionName` 屬性指出 `/Edit/` URL 仍在使用中)。</span><span class="sxs-lookup"><span data-stu-id="96a8e-161">Changes the method name to `EditPost` because the signature is now the same as the HttpGet `Edit` method (the `ActionName` attribute specifies that the `/Edit/` URL is still used).</span></span>

-  <span data-ttu-id="96a8e-162">針對 `OfficeAssignment` 導覽屬性使用積極式載入從資料庫中取得目前的 Instructor 實體。</span><span class="sxs-lookup"><span data-stu-id="96a8e-162">Gets the current Instructor entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="96a8e-163">這與您在 HttpGet `Edit` 方法中所做的事情一樣。</span><span class="sxs-lookup"><span data-stu-id="96a8e-163">This is the same as what you did in the HttpGet `Edit` method.</span></span>

-  <span data-ttu-id="96a8e-164">使用從模型繫結器取得的值更新擷取的 Instructor 實體。</span><span class="sxs-lookup"><span data-stu-id="96a8e-164">Updates the retrieved Instructor entity with values from the model binder.</span></span> <span data-ttu-id="96a8e-165">`TryUpdateModel` 多載可讓您將要包含的屬性加入允許清單中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-165">The `TryUpdateModel` overload enables you to whitelist the properties you want to include.</span></span> <span data-ttu-id="96a8e-166">這可防止大量指派，如同在[第二個教學課程](crud.md)中所解釋的。</span><span class="sxs-lookup"><span data-stu-id="96a8e-166">This prevents over-posting, as explained in the [second tutorial](crud.md).</span></span>

    <!-- Snippets don't play well with <ul> [!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?range=241-244)] -->

    ```csharp
    if (await TryUpdateModelAsync<Instructor>(
        instructorToUpdate,
        "",
        i => i.FirstMidName, i => i.LastName, i => i.HireDate, i => i.OfficeAssignment))
    ```

-   <span data-ttu-id="96a8e-167">若辦公室位置為空白，將 Instructor.OfficeAssignment 屬性設為 Null，以刪除在 OfficeAssignment 資料表中的相關資料列。</span><span class="sxs-lookup"><span data-stu-id="96a8e-167">If the office location is blank, sets the Instructor.OfficeAssignment property to null so that the related row in the OfficeAssignment table will be deleted.</span></span>

    <!-- Snippets don't play well with <ul>  "intro/samples/cu/Controllers/InstructorsController.cs"} -->

    ```csharp
    if (String.IsNullOrWhiteSpace(instructorToUpdate.OfficeAssignment?.Location))
    {
        instructorToUpdate.OfficeAssignment = null;
    }
    ```

- <span data-ttu-id="96a8e-168">將變更儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="96a8e-168">Saves the changes to the database.</span></span>

### <a name="update-the-instructor-edit-view"></a><span data-ttu-id="96a8e-169">更新 Instructor [編輯] 檢視</span><span class="sxs-lookup"><span data-stu-id="96a8e-169">Update the Instructor Edit view</span></span>

<span data-ttu-id="96a8e-170">在 *Views/Instructors/Edit.cshtml* 中，在 [儲存] 按鈕前的結尾處新增一個用於編輯辦公室位置的欄位：</span><span class="sxs-lookup"><span data-stu-id="96a8e-170">In *Views/Instructors/Edit.cshtml*, add a new field for editing the office location, at the end before the **Save** button:</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Edit.cshtml?range=30-34)]

<span data-ttu-id="96a8e-171">執行應用程式，選取 [Instructor] 索引標籤，然後在講師上按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="96a8e-171">Run the app, select the **Instructors** tab, and then click **Edit** on an instructor.</span></span> <span data-ttu-id="96a8e-172">變更 [辦公室位置]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="96a8e-172">Change the **Office Location** and click **Save**.</span></span>

![Instructor [編輯] 頁面](update-related-data/_static/instructor-edit-office.png)

## <a name="add-courses-to-edit-page"></a><span data-ttu-id="96a8e-174">將課程新增至 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-174">Add courses to Edit page</span></span>

<span data-ttu-id="96a8e-175">講師可教授任何數量的課程。</span><span class="sxs-lookup"><span data-stu-id="96a8e-175">Instructors may teach any number of courses.</span></span> <span data-ttu-id="96a8e-176">現在您將藉由使用核取方塊群組，新增變更課程指派的能力來強化 Instructor [編輯] 頁面，如以下螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="96a8e-176">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor [編輯] 頁面與課程](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="96a8e-178">Course 與 Instructor 實體的關係為多對多。</span><span class="sxs-lookup"><span data-stu-id="96a8e-178">The relationship between the Course and Instructor entities is many-to-many.</span></span> <span data-ttu-id="96a8e-179">若要新增和移除關聯性，您必須在 CourseAssignments 聯結實體集中新增和移除實體。</span><span class="sxs-lookup"><span data-stu-id="96a8e-179">To add and remove relationships, you add and remove entities to and from the CourseAssignments join entity set.</span></span>

<span data-ttu-id="96a8e-180">可讓您變更講師指派之課程的 UI 為一組核取方塊。</span><span class="sxs-lookup"><span data-stu-id="96a8e-180">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="96a8e-181">資料庫中每個課程的核取方塊都會顯示，而該名講師目前受指派的課程會已選取狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="96a8e-181">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="96a8e-182">使用者可選取或清除核取方塊來變更課程指派。</span><span class="sxs-lookup"><span data-stu-id="96a8e-182">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="96a8e-183">若課程數量要大上許多，您可能會想要使用不同的方法來在檢視中呈現資料，但您操縱聯結實體以建立或刪除關聯性的方法是相同的。</span><span class="sxs-lookup"><span data-stu-id="96a8e-183">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating a join entity to create or delete relationships.</span></span>

### <a name="update-the-instructors-controller"></a><span data-ttu-id="96a8e-184">更新 Instructor 控制器</span><span class="sxs-lookup"><span data-stu-id="96a8e-184">Update the Instructors controller</span></span>

<span data-ttu-id="96a8e-185">若要針對核取方塊清單提供資料給檢視，您必須使用一個檢視模型類別。</span><span class="sxs-lookup"><span data-stu-id="96a8e-185">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span>

<span data-ttu-id="96a8e-186">在 *SchoolViewModels* 資料夾中建立 *AssignedCourseData.cs*，然後以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="96a8e-186">Create *AssignedCourseData.cs* in the *SchoolViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

<span data-ttu-id="96a8e-187">在 *InstructorsController.cs* 中，使用下列程式碼取代 HttpGet `Edit` 方法。</span><span class="sxs-lookup"><span data-stu-id="96a8e-187">In *InstructorsController.cs*, replace the HttpGet `Edit` method with the following code.</span></span> <span data-ttu-id="96a8e-188">所做的變更已醒目提示。</span><span class="sxs-lookup"><span data-stu-id="96a8e-188">The changes are highlighted.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=10,17,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36&name=snippet_EditGetCourses)]

<span data-ttu-id="96a8e-189">程式碼會為 `Courses` 導覽屬性新增積極式載入，然後使用 `AssignedCourseData` 檢視模型類別來呼叫新的 `PopulateAssignedCourseData` 方法以提供資訊給核取方塊陣列。</span><span class="sxs-lookup"><span data-stu-id="96a8e-189">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="96a8e-190">`PopulateAssignedCourseData` 方法中的程式碼會讀取所有的 Course 實體以使用檢視模型類別載入課程清單。</span><span class="sxs-lookup"><span data-stu-id="96a8e-190">The code in the `PopulateAssignedCourseData` method reads through all Course entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="96a8e-191">針對每個課程，程式碼會檢查課程是否存在於講師的 `Courses` 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-191">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="96a8e-192">為了在檢查課程是否已指派給講師的過程中更有效率，指派給講師的課程會放入一個 `HashSet` 集合中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-192">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a `HashSet` collection.</span></span> <span data-ttu-id="96a8e-193">`Assigned` 屬性會針對已指派給講師的課程設定為 true。</span><span class="sxs-lookup"><span data-stu-id="96a8e-193">The `Assigned` property  is set to true for courses the instructor is assigned to.</span></span> <span data-ttu-id="96a8e-194">檢視會使用這個屬性，來判斷哪一個核取方塊必須顯示為已選取。</span><span class="sxs-lookup"><span data-stu-id="96a8e-194">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="96a8e-195">最後，清單會傳遞至位於 `ViewData` 的檢視中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-195">Finally, the list is passed to the view in `ViewData`.</span></span>

<span data-ttu-id="96a8e-196">接下來，新增當使用者按一下 [儲存] 時要執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="96a8e-196">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="96a8e-197">使用下列程式碼取代 `EditPost` 方法，然後新增一個方法，該方法會更新 Instructor 實體的 `Courses` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="96a8e-197">Replace the `EditPost` method with the following code, and add a new method that updates the `Courses` navigation property of the Instructor entity.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=1,3,12,13,25,39-40&name=snippet_EditPostCourses)]

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=1-31)]

<span data-ttu-id="96a8e-198">方法簽章現在已和 HttpGet `Edit` 方法不同，因此方法名稱會從 `EditPost` 變回 `Edit`。</span><span class="sxs-lookup"><span data-stu-id="96a8e-198">The method signature is now different from the HttpGet `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="96a8e-199">由於檢視沒有 Course 實體的集合，模型繫結器無法自動更新 `CourseAssignments` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="96a8e-199">Since the view doesn't have a collection of Course entities, the model binder can't automatically update the `CourseAssignments` navigation property.</span></span> <span data-ttu-id="96a8e-200">相較於使用模型繫結器更新 `CourseAssignments` 導覽屬性，您會在新的 `UpdateInstructorCourses` 方法中進行相同的操作。</span><span class="sxs-lookup"><span data-stu-id="96a8e-200">Instead of using the model binder to update the `CourseAssignments` navigation property, you do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="96a8e-201">因此您必須從模型繫結器中排除 `CourseAssignments` 屬性。</span><span class="sxs-lookup"><span data-stu-id="96a8e-201">Therefore you need to exclude the `CourseAssignments` property from model binding.</span></span> <span data-ttu-id="96a8e-202">這並不需要對呼叫 `TryUpdateModel` 的程式碼進行任何變更，因為您使用的是允許清單多載，且 `CourseAssignments` 並未位於包含清單中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-202">This doesn't require any change to the code that calls `TryUpdateModel` because you're using the whitelisting overload and `CourseAssignments` isn't in the include list.</span></span>

<span data-ttu-id="96a8e-203">若沒有選取任何核取方塊，`UpdateInstructorCourses` 中的程式碼會使用空集合初始化 `CourseAssignments` 導覽屬性並傳回：</span><span class="sxs-lookup"><span data-stu-id="96a8e-203">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `CourseAssignments` navigation property with an empty collection and returns:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=3-7)]

<span data-ttu-id="96a8e-204">程式碼會執行迴圈，尋訪資料庫中所有的課程，並檢查每個已指派給講師的課程，以及在檢視中選取的課程。</span><span class="sxs-lookup"><span data-stu-id="96a8e-204">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="96a8e-205">為了協助達成有效率的搜尋，後者的兩個集合會儲存在 `HashSet` 物件中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-205">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="96a8e-206">若課程的核取方塊已被選取，但課程並未位於 `Instructor.CourseAssignments` 導覽屬性中，則課程便會新增至導覽屬性的集合中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-206">If the check box for a course was selected but the course isn't in the `Instructor.CourseAssignments` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=14-20&name=snippet_UpdateCourses)]

<span data-ttu-id="96a8e-207">若課程的核取方塊未被選取，但課程卻位於 `Instructor.CourseAssignments` 導覽屬性中，則課程便會從導覽屬性的集合中移除。</span><span class="sxs-lookup"><span data-stu-id="96a8e-207">If the check box for a course wasn't selected, but the course is in the `Instructor.CourseAssignments` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=21-29&name=snippet_UpdateCourses)]

### <a name="update-the-instructor-views"></a><span data-ttu-id="96a8e-208">更新 Instructor 檢視</span><span class="sxs-lookup"><span data-stu-id="96a8e-208">Update the Instructor views</span></span>

<span data-ttu-id="96a8e-209">在 *Views/Instructors/Edit.cshtml* 中，藉由將下列程式碼新增到 [辦公室] 欄位的 `div` 項目後及 [儲存] 按鈕的 `div` 項目前，來新增 [課程 ] 欄位與核取方塊陣列。</span><span class="sxs-lookup"><span data-stu-id="96a8e-209">In *Views/Instructors/Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the **Office** field and before the `div` element for the **Save** button.</span></span>

<a id="notepad"></a>
> [!NOTE]
> <span data-ttu-id="96a8e-210">當您將程式碼貼至 Visual Studio 時，分行符號可能會產生變更使程式碼失效。</span><span class="sxs-lookup"><span data-stu-id="96a8e-210">When you paste the code in Visual Studio, line breaks will be changed in a way that breaks the code.</span></span>  <span data-ttu-id="96a8e-211">按 Ctrl+Z 來復原自動格式化。</span><span class="sxs-lookup"><span data-stu-id="96a8e-211">Press Ctrl+Z one time to undo the automatic formatting.</span></span>  <span data-ttu-id="96a8e-212">這會修正分行符號，使他們看起來就跟您在這裡看到的一樣。</span><span class="sxs-lookup"><span data-stu-id="96a8e-212">This will fix the line breaks so that they look like what you see here.</span></span> <span data-ttu-id="96a8e-213">縮排不一定要是完美的，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@:</tr>` 必須要如顯示般各自在獨立的一行上，否則您會接收到執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="96a8e-213">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@:</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span> <span data-ttu-id="96a8e-214">當選取新的程式碼區塊時，按 Tab 鍵三次來讓新的程式碼對準現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="96a8e-214">With the block of new code selected, press Tab three times to line up the new code with the existing code.</span></span> <span data-ttu-id="96a8e-215">您可以在[這裡](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html)檢查此問題的狀態。</span><span class="sxs-lookup"><span data-stu-id="96a8e-215">You can check the status of this problem [here](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html).</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Edit.cshtml?range=35-61)]

<span data-ttu-id="96a8e-216">此程式碼會建立一個 HTML 表格，該表格中有三個資料行。</span><span class="sxs-lookup"><span data-stu-id="96a8e-216">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="96a8e-217">在每個資料行中，核取方塊的後方會是由課程號碼和標題組成的標題。</span><span class="sxs-lookup"><span data-stu-id="96a8e-217">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="96a8e-218">所有核取方塊的名稱都是 ("selectedCourses")，會告知模型繫結器應將其視為一個群組。</span><span class="sxs-lookup"><span data-stu-id="96a8e-218">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they're to be treated as a group.</span></span> <span data-ttu-id="96a8e-219">每個核取方塊的 Value 屬性都會設為 `CourseID` 的值。</span><span class="sxs-lookup"><span data-stu-id="96a8e-219">The value attribute of each check box is set to the value of `CourseID`.</span></span> <span data-ttu-id="96a8e-220">當頁面以 post 方式提交時，模型繫結器便會將只包含我們選取核取方塊之 `CourseID` 值的陣列傳遞到控制器。</span><span class="sxs-lookup"><span data-stu-id="96a8e-220">When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="96a8e-221">核取方塊一開始呈現時，已指派給該名講師的課程便會帶有 Checked 屬性，使其顯示為已選取狀態。</span><span class="sxs-lookup"><span data-stu-id="96a8e-221">When the check boxes are initially rendered, those that are for courses assigned to the instructor have checked attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="96a8e-222">執行應用程式，選取 [Instructor] 索引標籤，然後按一下講師上的 [編輯] 以查看 [編輯] 頁面。</span><span class="sxs-lookup"><span data-stu-id="96a8e-222">Run the app, select the **Instructors** tab, and click **Edit** on an instructor to see the **Edit** page.</span></span>

![Instructor [編輯] 頁面與課程](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="96a8e-224">變更一些課程指派，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="96a8e-224">Change some course assignments and click Save.</span></span> <span data-ttu-id="96a8e-225">您所做的變更會反映在 [索引] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="96a8e-225">The changes you make are reflected on the Index page.</span></span>

> [!NOTE]
> <span data-ttu-id="96a8e-226">這裡所用來編輯講師課程資料的方法在課程的數量有限時運作相當良好。</span><span class="sxs-lookup"><span data-stu-id="96a8e-226">The approach taken here to edit instructor course data works well when there's a limited number of courses.</span></span> <span data-ttu-id="96a8e-227">針對更大的集合，將需要不同的 UI 和不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="96a8e-227">For collections that are much larger, a different UI and a different updating method would be required.</span></span>

## <a name="update-delete-page"></a><span data-ttu-id="96a8e-228">更新 [刪除] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-228">Update Delete page</span></span>

<span data-ttu-id="96a8e-229">在 *InstructorsController.cs* 中，刪除 `DeleteConfirmed` 方法並在相同位置插入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="96a8e-229">In *InstructorsController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=5-7,9-12&name=snippet_DeleteConfirmed)]

<span data-ttu-id="96a8e-230">此程式碼會進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="96a8e-230">This code makes the following changes:</span></span>

* <span data-ttu-id="96a8e-231">為 `CourseAssignments` 導覽屬性進行積極式載入。</span><span class="sxs-lookup"><span data-stu-id="96a8e-231">Does eager loading for the `CourseAssignments` navigation property.</span></span>  <span data-ttu-id="96a8e-232">您必須包含這個，否則 EF 將無法得知相關 `CourseAssignment` 而無法刪除他們。</span><span class="sxs-lookup"><span data-stu-id="96a8e-232">You have to include this or EF won't know about related `CourseAssignment` entities and won't delete them.</span></span>  <span data-ttu-id="96a8e-233">若要避免在此讀取他們，您可以在資料庫中設定串聯刪除。</span><span class="sxs-lookup"><span data-stu-id="96a8e-233">To avoid needing to read them here you could configure cascade delete in the database.</span></span>

* <span data-ttu-id="96a8e-234">若要刪除的講師已指派為任何部門的系統管理員，請先從這些部門中移除講師的指派。</span><span class="sxs-lookup"><span data-stu-id="96a8e-234">If the instructor to be deleted is assigned as administrator of any departments, removes the instructor assignment from those departments.</span></span>

## <a name="add-office-location-and-courses-to-create-page"></a><span data-ttu-id="96a8e-235">將辦公室位置和課程新增至 [建立] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-235">Add office location and courses to Create page</span></span>

<span data-ttu-id="96a8e-236">在 *InstructosController.cs* 中，刪除 HttpGet 和 HttpPost `Create` 方法，然後在相同位置新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="96a8e-236">In *InstructorsController.cs*, delete the HttpGet and HttpPost `Create` methods, and then add the following code in their place:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Create&highlight=3-5,12,14-22,29)]

<span data-ttu-id="96a8e-237">此程式碼與您在 `Edit` 方法中看到的類似，除了一開始沒有選取任何課程之外。</span><span class="sxs-lookup"><span data-stu-id="96a8e-237">This code is similar to what you saw for the `Edit` methods except that initially no courses are selected.</span></span> <span data-ttu-id="96a8e-238">HttpGet `Create` 方法會呼叫 `PopulateAssignedCourseData` 方法，不是因為可能會有已選取的課程，而是為了提供空集合給檢視中的 `foreach` 迴圈 (否則檢視程式碼會擲回 Null 參考例外狀況)。</span><span class="sxs-lookup"><span data-stu-id="96a8e-238">The HttpGet `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="96a8e-239">HttpPost `Create` 方法會在檢查驗證錯誤並將新的講師新增到資料庫前將每個選取的課程新增到 `CourseAssignments` 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="96a8e-239">The HttpPost `Create` method adds each selected course to the `CourseAssignments` navigation property before it checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="96a8e-240">即使發生模型錯誤，課程也會新增，這使得當發生模型錯誤 (例如使用者鍵入了無效的日期)，並且頁面重新顯示並帶有錯誤訊息時，任何課程選取都會自動還原。</span><span class="sxs-lookup"><span data-stu-id="96a8e-240">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date), and the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="96a8e-241">請注意，為了要能夠將課程新增到 `CourseAssignments` 導覽屬性，您必須將屬性以空集合初始化：</span><span class="sxs-lookup"><span data-stu-id="96a8e-241">Notice that in order to be able to add courses to the `CourseAssignments` navigation property you have to initialize the property as an empty collection:</span></span>

```csharp
instructor.CourseAssignments = new List<CourseAssignment>();
```

<span data-ttu-id="96a8e-242">作為在控制器程式碼中完成這項操作的替代方案，您可以在 Instructor 模型中藉由將屬性 getter 變更為在不存在時自動建立集合來完成，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="96a8e-242">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

```csharp
private ICollection<CourseAssignment> _courseAssignments;
public ICollection<CourseAssignment> CourseAssignments
{
    get
    {
        return _courseAssignments ?? (_courseAssignments = new List<CourseAssignment>());
    }
    set
    {
        _courseAssignments = value;
    }
}
```

<span data-ttu-id="96a8e-243">若您使用這種方式修改了 `CourseAssignments` 屬性，您便可以移除控制器中的明確屬性初始化程式碼。</span><span class="sxs-lookup"><span data-stu-id="96a8e-243">If you modify the `CourseAssignments` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="96a8e-244">在 *Views/Instructor/Create.cshtml* 中，在 [提交] 按鈕前新增一個辦公室位置文字方塊及課程核取方塊。</span><span class="sxs-lookup"><span data-stu-id="96a8e-244">In *Views/Instructor/Create.cshtml*, add an office location text box and check boxes for courses before the Submit button.</span></span> <span data-ttu-id="96a8e-245">若為 [編輯] 頁面，請[修正 Visual Studio 於您貼上時重新格式化程式碼](#notepad)。</span><span class="sxs-lookup"><span data-stu-id="96a8e-245">As in the case of the Edit page, [fix the formatting if Visual Studio reformats the code when you paste it](#notepad).</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Create.cshtml?range=29-61)]

<span data-ttu-id="96a8e-246">執行應用程式並建立一名講師，以進行測試。</span><span class="sxs-lookup"><span data-stu-id="96a8e-246">Test by running the app and creating an instructor.</span></span>

## <a name="handling-transactions"></a><span data-ttu-id="96a8e-247">處理交易</span><span class="sxs-lookup"><span data-stu-id="96a8e-247">Handling Transactions</span></span>

<span data-ttu-id="96a8e-248">如同在 [CRUD 教學課程](crud.md)中所述，Entity Framework 隱含實作了交易。</span><span class="sxs-lookup"><span data-stu-id="96a8e-248">As explained in the [CRUD tutorial](crud.md), the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="96a8e-249">針對您需要更多控制的案例 -- 例如，若您想要在一個交易中包含在 Entity Framework 之外完成的作業 -- 請參閱[交易](/ef/core/saving/transactions)。</span><span class="sxs-lookup"><span data-stu-id="96a8e-249">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Transactions](/ef/core/saving/transactions).</span></span>

## <a name="get-the-code"></a><span data-ttu-id="96a8e-250">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="96a8e-250">Get the code</span></span>

[<span data-ttu-id="96a8e-251">下載或檢視已完成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="96a8e-251">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="next-steps"></a><span data-ttu-id="96a8e-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96a8e-252">Next steps</span></span>

<span data-ttu-id="96a8e-253">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="96a8e-253">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96a8e-254">自訂 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-254">Customized Courses pages</span></span>
> * <span data-ttu-id="96a8e-255">新增 Instructors [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-255">Added Instructors Edit page</span></span>
> * <span data-ttu-id="96a8e-256">將課程新增至 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-256">Added courses to Edit page</span></span>
> * <span data-ttu-id="96a8e-257">更新 [刪除] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-257">Updated Delete page</span></span>
> * <span data-ttu-id="96a8e-258">將辦公室位置和課程新增至 [建立] 頁面</span><span class="sxs-lookup"><span data-stu-id="96a8e-258">Added office location and courses to Create page</span></span>

<span data-ttu-id="96a8e-259">若要了解如何處理並行衝突，請前往下一篇文章。</span><span class="sxs-lookup"><span data-stu-id="96a8e-259">Advance to the next article to learn how to handle concurrency conflicts.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="96a8e-260">處理並行衝突</span><span class="sxs-lookup"><span data-stu-id="96a8e-260">Handle concurrency conflicts</span></span>](concurrency.md)