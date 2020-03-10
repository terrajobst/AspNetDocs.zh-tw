---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中使用 EF 更新相關資料
description: 在本教學課程中，您將更新相關的資料。 對於大部分的關聯性，您可以藉由更新外鍵欄位或導覽屬性來完成這項作業。
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616001"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="1f0fc-104">教學課程：在 ASP.NET MVC 應用程式中使用 EF 更新相關資料</span><span class="sxs-lookup"><span data-stu-id="1f0fc-104">Tutorial: Update related data with EF in an ASP.NET MVC app</span></span>

<span data-ttu-id="1f0fc-105">在上一個教學課程中，您顯示了相關資料。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-105">In the previous tutorial you displayed related data.</span></span> <span data-ttu-id="1f0fc-106">在本教學課程中，您將更新相關的資料。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-106">In this tutorial you'll update related data.</span></span> <span data-ttu-id="1f0fc-107">對於大部分的關聯性，您可以藉由更新外鍵欄位或導覽屬性來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-107">For most relationships, this can be done by updating either foreign key fields or navigation properties.</span></span> <span data-ttu-id="1f0fc-108">針對多對多關聯性，Entity Framework 不會直接公開聯結資料表，因此您可以在適當的導覽屬性中新增和移除實體。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-108">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="1f0fc-109">下列圖例顯示了您將操作的一些頁面。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-109">The following illustrations show some of the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![講師編輯課程](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="1f0fc-113">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-113">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f0fc-114">自訂課程頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-114">Customize courses pages</span></span>
> * <span data-ttu-id="1f0fc-115">將 office 新增到講師頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-115">Add office to instructors page</span></span>
> * <span data-ttu-id="1f0fc-116">將課程新增至講師頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-116">Add courses to instructors page</span></span>
> * <span data-ttu-id="1f0fc-117">更新 DeleteConfirmed</span><span class="sxs-lookup"><span data-stu-id="1f0fc-117">Update DeleteConfirmed</span></span>
> * <span data-ttu-id="1f0fc-118">將辦公室位置和課程新增至 [新增] 頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-118">Add office location and courses to the Create page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f0fc-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f0fc-119">Prerequisites</span></span>

* [<span data-ttu-id="1f0fc-120">讀取相關資料</span><span class="sxs-lookup"><span data-stu-id="1f0fc-120">Reading Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a><span data-ttu-id="1f0fc-121">自訂課程頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-121">Customize courses pages</span></span>

<span data-ttu-id="1f0fc-122">當新的課程實體建立時，其必須要與現有的部門具有關聯性。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-122">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="1f0fc-123">若要達成此目的，Scaffold 程式碼包含了控制器方法和 [建立] 和 [編輯] 檢視，當中包含了一個可選取部門的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-123">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="1f0fc-124">下拉式清單會設定 `Course.DepartmentID` 外鍵屬性，而這就是載入具有適當 `Department` 實體之 `Department` 導覽屬性的所有 Entity Framework 需求。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-124">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="1f0fc-125">您將使用 Scaffold 程式碼，但會稍微對其進行一些變更以新增錯誤處理及排序下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-125">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="1f0fc-126">在*CourseController.cs*中，刪除四個 `Create` 並 `Edit` 方法，並將其取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-126">In *CourseController.cs*, delete the four `Create` and `Edit` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

<span data-ttu-id="1f0fc-127">在檔案的開頭新增下列 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-127">Add the following `using` statement at the beginning of the file:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="1f0fc-128">`PopulateDepartmentsDropDownList` 方法會取得依名稱排序的所有部門清單、建立下拉式清單的 `SelectList` 集合，並將集合傳遞至 `ViewBag` 屬性中的 view。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-128">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="1f0fc-129">方法接受選擇性的 `selectedDepartment` 參數，可允許呼叫程式碼在呈現下拉式清單時指定選取的項目。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-129">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="1f0fc-130">此視圖會將名稱 `DepartmentID` 傳遞給[DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper，而協助專家會知道要在 `ViewBag` 物件中尋找名為 `DepartmentID`的 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-130">The view will pass the name `DepartmentID` to the [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="1f0fc-131">`HttpGet` `Create` 方法會呼叫 `PopulateDepartmentsDropDownList` 方法，而不會設定選取的專案，因為如果是新的課程，則尚未建立部門：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-131">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="1f0fc-132">`HttpGet` `Edit` 方法會根據已指派給所編輯之課程的部門識別碼，來設定選取的專案：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-132">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

<span data-ttu-id="1f0fc-133">`Create` 和 `Edit` 的 `HttpPost` 方法也包含程式碼，可在錯誤發生後重新顯示頁面時，設定選取的專案：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-133">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

<span data-ttu-id="1f0fc-134">這段程式碼可確保當頁面重新顯示時，如果出現錯誤訊息，則會保留選取的任何部門。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-134">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="1f0fc-135">課程視圖已 scaffold [部門] 欄位的下拉式清單，但您不想要此欄位的 [DepartmentID] 標題，因此請將下列反白顯示的*Views\Course\Create.cshtml*檔案變更變更為 [標題]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-135">The Course views are already scaffolded with drop-down lists for the department field, but you don't want the DepartmentID caption for this field, so make the following highlighted change to the *Views\Course\Create.cshtml* file to change the caption.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

<span data-ttu-id="1f0fc-136">在*Views\Course\Edit.cshtml*中進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-136">Make the same change in *Views\Course\Edit.cshtml*.</span></span>

<span data-ttu-id="1f0fc-137">一般來說，scaffolder 不會 scaffold 主鍵，因為索引鍵值是由資料庫所產生，而且無法變更，而且不是對使用者顯示有意義的值。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-137">Normally the scaffolder doesn't scaffold a primary key because the key value is generated by the database and can't be changed and isn't a meaningful value to be displayed to users.</span></span> <span data-ttu-id="1f0fc-138">針對「課程」實體，scaffolder 的確包含 `CourseID` 欄位的文字方塊，因為它瞭解 `DatabaseGeneratedOption.None` 屬性工作表示使用者應該能夠輸入主要金鑰值。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-138">For Course entities the scaffolder does include an text box for the `CourseID` field because it understands that the `DatabaseGeneratedOption.None` attribute means the user should be able enter the primary key value.</span></span> <span data-ttu-id="1f0fc-139">但它並不瞭解，因為數位有意義，您想要在其他視圖中看到它，因此您需要手動新增。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-139">But it doesn't understand that because the number is meaningful you want to see it in the other views, so you need to add it manually.</span></span>

<span data-ttu-id="1f0fc-140">在*Views\Course\Edit.cshtml*中，于 [**標題**] 欄位前面新增 [課程編號] 欄位。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-140">In *Views\Course\Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="1f0fc-141">因為它是主要金鑰，所以會顯示，但無法變更。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-141">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

<span data-ttu-id="1f0fc-142">[編輯] 視圖中的課程編號已經有一個隱藏欄位（`Html.HiddenFor` helper）。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-142">There's already a hidden field (`Html.HiddenFor` helper) for the course number in the Edit view.</span></span> <span data-ttu-id="1f0fc-143">新增 Html 時， *LabelFor* helper 並不會免除隱藏欄位的需求，因為它不會在使用者按一下 [編輯] 頁面上的 [**儲存**] 時，讓課程號碼包含在張貼的資料中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-143">Adding an *Html.LabelFor* helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the Edit page.</span></span>

<span data-ttu-id="1f0fc-144">在*Views\Course\Delete.cshtml*和*Views\Course\Details.cshtml*中，將部門名稱標題從「名稱」變更為「部門」，然後在 [**標題**] 欄位前面新增 [課程編號] 欄位。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-144">In *Views\Course\Delete.cshtml* and *Views\Course\Details.cshtml*, change the department name caption from "Name" to "Department" and add a course number field before the **Title** field.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

<span data-ttu-id="1f0fc-145">執行 [**建立**] 頁面（顯示 [課程索引] 頁面，然後按一下 [**建立新**的]）並輸入新課程的資料：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-145">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

| <span data-ttu-id="1f0fc-146">值</span><span class="sxs-lookup"><span data-stu-id="1f0fc-146">Value</span></span> | <span data-ttu-id="1f0fc-147">設定</span><span class="sxs-lookup"><span data-stu-id="1f0fc-147">Setting</span></span> |
| ----- | ------- |
| <span data-ttu-id="1f0fc-148">數字</span><span class="sxs-lookup"><span data-stu-id="1f0fc-148">Number</span></span> | <span data-ttu-id="1f0fc-149">輸入*1000*。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-149">Enter *1000*.</span></span> |
| <span data-ttu-id="1f0fc-150">標題</span><span class="sxs-lookup"><span data-stu-id="1f0fc-150">Title</span></span> | <span data-ttu-id="1f0fc-151">輸入*代數*。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-151">Enter *Algebra*.</span></span> |
| <span data-ttu-id="1f0fc-152">學分</span><span class="sxs-lookup"><span data-stu-id="1f0fc-152">Credits</span></span> | <span data-ttu-id="1f0fc-153">輸入*4*。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-153">Enter *4*.</span></span> |
|<span data-ttu-id="1f0fc-154">部門</span><span class="sxs-lookup"><span data-stu-id="1f0fc-154">Department</span></span> | <span data-ttu-id="1f0fc-155">選取 [**數學**]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-155">Select **Mathematics**.</span></span> |

<span data-ttu-id="1f0fc-156">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-156">Click **Create**.</span></span> <span data-ttu-id="1f0fc-157">[課程索引] 頁面隨即顯示，並將新課程加入清單中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-157">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="1f0fc-158">[索引] 頁面中的部門名稱來自於導覽屬性，顯示關聯性已正確建立。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-158">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

<span data-ttu-id="1f0fc-159">執行 [**編輯**] 頁面（顯示課程 [索引] 頁面，然後按一下 [在課程中**編輯**]）。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-159">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

<span data-ttu-id="1f0fc-160">變更頁面上的資料，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-160">Change data on the page and click **Save**.</span></span> <span data-ttu-id="1f0fc-161">[課程索引] 頁面隨即顯示，其中包含更新的課程資料。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-161">The Course Index page is displayed with the updated course data.</span></span>

## <a name="add-office-to-instructors-page"></a><span data-ttu-id="1f0fc-162">將 office 新增到講師頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-162">Add office to instructors page</span></span>

<span data-ttu-id="1f0fc-163">當您編輯講師記錄時，您可能會想要更新講師的辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-163">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="1f0fc-164">`Instructor` 實體與 `OfficeAssignment` 實體具有一對零或一關聯性，這表示您必須處理下列情況：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-164">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="1f0fc-165">如果使用者清除辦公室指派，而且原先具有值，您就必須移除並刪除 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-165">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="1f0fc-166">如果使用者輸入辦公室指派值，而且原先是空的，您就必須建立新的 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-166">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="1f0fc-167">如果使用者變更辦公室指派的值，您必須變更現有 `OfficeAssignment` 實體中的值。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-167">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="1f0fc-168">開啟*InstructorController.cs* ，並查看 `HttpGet` `Edit` 方法：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-168">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="1f0fc-169">此處的 scaffold 程式碼不是您想要的。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-169">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="1f0fc-170">它會設定下拉式清單的資料，但您需要的是文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-170">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="1f0fc-171">以下列程式碼取代此方法：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-171">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

<span data-ttu-id="1f0fc-172">此程式碼會卸載 `ViewBag` 語句，並為相關聯的 `OfficeAssignment` 實體新增積極式載入。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-172">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="1f0fc-173">您無法使用 `Find` 方法執行積極式載入，因此會改為使用 `Where` 和 `Single` 方法來選取講師。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-173">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="1f0fc-174">使用下列程式碼取代 `HttpPost` `Edit` 方法。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-174">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="1f0fc-175">處理 office 指派更新的：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-175">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="1f0fc-176">`RetryLimitExceededException` 的參考需要 `using` 語句;若要新增它，請將滑鼠停留在 `RetryLimitExceededException`。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-176">The reference to `RetryLimitExceededException` requires a `using` statement; to add it - hover your mouse over `RetryLimitExceededException`.</span></span> <span data-ttu-id="1f0fc-177">此時會出現下列訊息： ![ 重試例外狀況訊息](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1f0fc-177">The following message appears: ![ Retry exception message](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span></span>

<span data-ttu-id="1f0fc-178">選取 [**顯示可能的修正**]，然後**使用 [system.object** ]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-178">Select **Show potential fixes**, then **using System.Data.Entity.Infrastructure**</span></span>

![解決重試例外狀況](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="1f0fc-180">程式碼會執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-180">The code does the following:</span></span>

- <span data-ttu-id="1f0fc-181">將方法名稱變更為 `EditPost`，因為簽章現在與 `HttpGet` 方法相同（`ActionName` 屬性指定/Edit/URL 仍在使用中）。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-181">Changes the method name to `EditPost` because the signature is now the same as the `HttpGet` method (the `ActionName` attribute specifies that the /Edit/ URL is still used).</span></span>
- <span data-ttu-id="1f0fc-182">針對 `Instructor` 導覽屬性使用積極式載入從資料庫中取得目前的 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-182">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="1f0fc-183">這與您在 `HttpGet` `Edit` 方法中的做法相同。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-183">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="1f0fc-184">使用從模型繫結器取得的值更新擷取的 `Instructor` 實體。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-184">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="1f0fc-185">使用的[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)多載可讓您將想要包含的屬性*列入*允許清單。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-185">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="1f0fc-186">這可避免過度張貼，如[第二個教學](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)課程中所述。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-186">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- <span data-ttu-id="1f0fc-187">如果辦公室位置為空白，則會將 `Instructor.OfficeAssignment` 屬性設為 null，以便刪除 `OfficeAssignment` 資料表中的相關資料列。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-187">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- <span data-ttu-id="1f0fc-188">將變更儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-188">Saves the changes to the database.</span></span>

<span data-ttu-id="1f0fc-189">在 [ *Views\Instructor\Edit.cshtml*] 中，于 [**雇用日期**] 欄位的 `div` 專案之後，新增欄位以編輯辦公室位置：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-189">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

<span data-ttu-id="1f0fc-190">執行頁面（選取 [**講師**] 索引標籤，然後按一下講師上的 [**編輯**]）。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-190">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="1f0fc-191">變更 [辦公室位置]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-191">Change the **Office Location** and click **Save**.</span></span>

## <a name="add-courses-to-instructors-page"></a><span data-ttu-id="1f0fc-192">將課程新增至講師頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-192">Add courses to instructors page</span></span>

<span data-ttu-id="1f0fc-193">講師可教授任何數量的課程。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-193">Instructors may teach any number of courses.</span></span> <span data-ttu-id="1f0fc-194">現在您將藉由新增使用一組核取方塊來變更課程指派的功能，來增強講師 [編輯] 頁面。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-194">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes.</span></span>

<span data-ttu-id="1f0fc-195">`Course` 和 `Instructor` 實體之間的關聯性是多對多，這表示您無法直接存取聯結資料表中的外鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-195">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the foreign key properties which are in the join table.</span></span> <span data-ttu-id="1f0fc-196">相反地，您可以在 `Instructor.Courses` 導覽屬性中新增和移除實體。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-196">Instead, you add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="1f0fc-197">可讓您變更講師指派之課程的 UI 為一組核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-197">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="1f0fc-198">資料庫中每個課程的核取方塊都會顯示，而該名講師目前受指派的課程會已選取狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-198">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="1f0fc-199">使用者可選取或清除核取方塊來變更課程指派。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-199">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="1f0fc-200">如果課程數很大，您可能會想要使用不同的方法來呈現視圖中的資料，但是您會使用相同的方法來操作導覽屬性，以便建立或刪除關聯性。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-200">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="1f0fc-201">若要針對核取方塊清單提供資料給檢視，您必須使用一個檢視模型類別。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-201">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="1f0fc-202">在*viewmodel*資料夾中建立*AssignedCourseData.cs* ，並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-202">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="1f0fc-203">在*InstructorController.cs*中，將 `HttpGet` `Edit` 方法取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-203">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="1f0fc-204">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-204">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

<span data-ttu-id="1f0fc-205">程式碼會為 `Courses` 導覽屬性新增積極式載入，然後使用 `PopulateAssignedCourseData` 檢視模型類別來呼叫新的 `AssignedCourseData` 方法以提供資訊給核取方塊陣列。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-205">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="1f0fc-206">`PopulateAssignedCourseData` 方法中的程式碼會讀取所有 `Course` 實體，以便使用 view model 類別載入課程清單。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-206">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="1f0fc-207">針對每個課程，程式碼會檢查課程是否存在於講師的 `Courses` 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-207">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="1f0fc-208">若要在檢查課程是否指派給講師時建立有效率的查閱，指派給講師的課程會放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-208">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="1f0fc-209">針對指派講師的課程，`Assigned` 屬性設定為 [`true`]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-209">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="1f0fc-210">檢視會使用這個屬性，來判斷哪一個核取方塊必須顯示為已選取。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-210">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="1f0fc-211">最後，會將清單傳遞至 `ViewBag` 屬性中的 view。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-211">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="1f0fc-212">接下來，新增當使用者按一下 [儲存] 時要執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-212">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="1f0fc-213">以下列程式碼取代 `EditPost` 方法，其會呼叫新的方法來更新 `Instructor` 實體的 `Courses` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-213">Replace the `EditPost` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="1f0fc-214">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-214">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

<span data-ttu-id="1f0fc-215">方法簽章現在與 `HttpGet` `Edit` 方法不同，因此方法名稱會從 `EditPost` 變更為 `Edit`。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-215">The method signature is now different from the `HttpGet` `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="1f0fc-216">由於此視圖沒有 `Course` 實體的集合，因此模型系結器無法自動更新 `Courses` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-216">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="1f0fc-217">您不需要使用模型系結器來更新 `Courses` 導覽屬性，而是在新的 `UpdateInstructorCourses` 方法中這麼做。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-217">Instead of using the model binder to update the `Courses` navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="1f0fc-218">因此您必須從模型繫結器中排除 `Courses` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-218">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="1f0fc-219">這不需要對呼叫[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)的程式碼進行任何變更，因為您使用的是*允許清單*多載，而且 `Courses` 不在包含清單中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-219">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="1f0fc-220">如果未選取任何核取方塊，`UpdateInstructorCourses` 中的程式碼會使用空集合初始化 `Courses` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-220">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="1f0fc-221">程式碼會執行迴圈，尋訪資料庫中所有的課程，並檢查每個已指派給講師的課程，以及在檢視中選取的課程。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-221">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="1f0fc-222">為了協助達成有效率的搜尋，後者的兩個集合會儲存在 `HashSet` 物件中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-222">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="1f0fc-223">若課程的核取方塊已被選取，但課程並未位於 `Instructor.Courses` 導覽屬性中，則課程便會新增至導覽屬性的集合中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-223">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="1f0fc-224">若課程的核取方塊未被選取，但課程卻位於 `Instructor.Courses` 導覽屬性中，則課程便會從導覽屬性的集合中移除。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-224">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="1f0fc-225">在*Views\Instructor\Edit.cshtml*中，新增包含核取方塊陣列的**課程**欄位，方法是在 [`OfficeAssignment`] 欄位的 `div` 元素之後，以及 [**儲存**] 按鈕的 [`div`] 元素之前，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-225">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the `OfficeAssignment` field and before the `div` element for the **Save** button:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

<span data-ttu-id="1f0fc-226">貼上程式碼之後，如果分行符號和縮排看起來不像在這裡執行，請手動修正所有內容，使其看起來像這裡所示。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-226">After you paste the code, if line breaks and indentation don't look like they do here, manually fix everything so that it looks like what you see here.</span></span> <span data-ttu-id="1f0fc-227">縮排不一定要是完美的，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@</tr>` 必須要如顯示般各自在獨立的一行上，否則您會接收到執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-227">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span>

<span data-ttu-id="1f0fc-228">此程式碼會建立一個 HTML 表格，該表格中有三個資料行。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-228">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="1f0fc-229">在每個資料行中，核取方塊的後方會是由課程號碼和標題組成的標題。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-229">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="1f0fc-230">所有核取方塊都具有相同的名稱（"selectedCourses"），這會通知模型系結器將其視為群組。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-230">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="1f0fc-231">當頁面張貼時，每個核取方塊的 `value` 屬性會設定為 `CourseID.` 的值，而模型系結器只會將陣列傳遞至控制器，其中只包含選取之核取方塊的 `CourseID` 值。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-231">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="1f0fc-232">一開始呈現核取方塊時，指派給講師的課程會有 `checked` 的屬性（會將其顯示為已核取）。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-232">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="1f0fc-233">變更課程指派之後，您會想要能夠在網站返回 [`Index`] 頁面時，確認變更。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-233">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="1f0fc-234">因此，您必須將資料行加入該頁面中的資料表。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-234">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="1f0fc-235">在這種情況下，您不需要使用 `ViewBag` 物件，因為您想要顯示的資訊已經在要當做模型傳遞至頁面之 `Instructor` 實體的 `Courses` 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-235">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="1f0fc-236">在*Views\Instructor\Index.cshtml*中，于**Office**標題後面新增**課程**標題，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-236">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

<span data-ttu-id="1f0fc-237">然後緊接在 [office 位置詳細資料] 儲存格後面加入新的 [詳細資料] 資料格：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-237">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

<span data-ttu-id="1f0fc-238">執行 [**講師索引**] 頁面，查看指派給每位講師的課程。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-238">Run the **Instructor Index** page to see the courses assigned to each instructor.</span></span>

<span data-ttu-id="1f0fc-239">按一下講師上的 [**編輯**] 以查看 [編輯] 頁面。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-239">Click **Edit** on an instructor to see the Edit page.</span></span>

<span data-ttu-id="1f0fc-240">變更一些課程指派，然後按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-240">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="1f0fc-241">您所做的變更會反映在 [索引] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-241">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="1f0fc-242">注意：在這裡用來編輯講師課程資料的方法，在有數量有限的課程時也能正常運作。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-242">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="1f0fc-243">針對更大的集合，將需要不同的 UI 和不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-243">For collections that are much larger, a different UI and a different updating method would be required.</span></span>

## <a name="update-deleteconfirmed"></a><span data-ttu-id="1f0fc-244">更新 DeleteConfirmed</span><span class="sxs-lookup"><span data-stu-id="1f0fc-244">Update DeleteConfirmed</span></span>

<span data-ttu-id="1f0fc-245">在*InstructorController.cs*中，刪除 `DeleteConfirmed` 方法，並在其位置插入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-245">In *InstructorController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

<span data-ttu-id="1f0fc-246">此程式碼會進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-246">This code makes the following change:</span></span>

- <span data-ttu-id="1f0fc-247">如果將講師指派為任何部門的系統管理員，則會移除該部門的講師指派。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-247">If the instructor is assigned as administrator of any department, removes the instructor assignment from that department.</span></span> <span data-ttu-id="1f0fc-248">如果沒有這段程式碼，當您嘗試刪除指派為部門系統管理員的講師時，就會出現參考完整性錯誤。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-248">Without this code, you would get a referential integrity error if you tried to delete an instructor who was assigned as administrator for a department.</span></span>

<span data-ttu-id="1f0fc-249">這段程式碼不會處理一個講師指派為多個部門之系統管理員的案例。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-249">This code doesn't handle the scenario of one instructor assigned as administrator for multiple departments.</span></span> <span data-ttu-id="1f0fc-250">在上一個教學課程中，您將新增程式碼，以防止發生該情況。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-250">In the last tutorial you'll add code that prevents that scenario from happening.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="1f0fc-251">將辦公室位置和課程新增至 [新增] 頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-251">Add office location and courses to the Create page</span></span>

<span data-ttu-id="1f0fc-252">在*InstructorController.cs*中，刪除 `HttpGet` 並 `HttpPost` `Create` 方法，然後在其位置新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-252">In *InstructorController.cs*, delete the `HttpGet` and `HttpPost` `Create` methods, and then add the following code in their place:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="1f0fc-253">這段程式碼類似于您在編輯方法中看到的內容，不同之處在于一開始不會選取任何課程。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-253">This code is similar to what you saw for the Edit methods except that initially no courses are selected.</span></span> <span data-ttu-id="1f0fc-254">`HttpGet` `Create` 方法不會呼叫 `PopulateAssignedCourseData` 方法，因為可能會有選取的課程，但為了在視圖中提供 `foreach` 迴圈的空集合（否則，view 程式碼會擲回 null 參考例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-254">The `HttpGet` `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="1f0fc-255">HttpPost Create 方法會在檢查驗證錯誤的範本程式碼之前，將每個選取的課程新增至課程導覽屬性，並將新的講師加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-255">The HttpPost Create method adds each selected course to the Courses navigation property before the template code that checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="1f0fc-256">即使發生模型錯誤，也會新增課程，以便在發生模型錯誤時（例如，使用者輸入不正確日期），因此當頁面重新顯示時，若出現錯誤訊息，則會自動還原已進行的任何課程選擇。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-256">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date) so that when the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="1f0fc-257">請注意，為了要能夠將課程新增到 `Courses` 導覽屬性，您必須將屬性以空集合初始化：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-257">Notice that in order to be able to add courses to the `Courses` navigation property you have to initialize the property as an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="1f0fc-258">作為在控制器程式碼中完成這項操作的替代方案，您可以在 Instructor 模型中藉由將屬性 getter 變更為在不存在時自動建立集合來完成，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-258">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="1f0fc-259">若您使用這種方式修改了 `Courses` 屬性，您便可以移除控制器中的明確屬性初始化程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-259">If you modify the `Courses` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="1f0fc-260">在*Views\Instructor\Create.cshtml*中，于 [雇用日期] 欄位之後和 [**提交**] 按鈕之前，新增 [辦公室位置] 文字方塊和課程核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-260">In *Views\Instructor\Create.cshtml*, add an office location text box and course check boxes after the hire date field and before the **Submit** button.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

<span data-ttu-id="1f0fc-261">在您貼上程式碼之後，請修正分行符號和縮排，如同您先前針對 [編輯] 頁面所執行的步驟。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-261">After you paste the code, fix line breaks and indentation as you did earlier for the Edit page.</span></span>

<span data-ttu-id="1f0fc-262">執行 [建立] 頁面並加入講師。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-262">Run the Create page and add an instructor.</span></span>

<a id="transactions"></a>

## <a name="handling-transactions"></a><span data-ttu-id="1f0fc-263">處理交易</span><span class="sxs-lookup"><span data-stu-id="1f0fc-263">Handling transactions</span></span>

<span data-ttu-id="1f0fc-264">如[基本 CRUD 功能教學](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)課程中所述，根據預設，Entity Framework 會隱含地執行交易。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-264">As explained in the [Basic CRUD Functionality tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), by default the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="1f0fc-265">針對您需要更多控制的案例--例如，如果您想要包含在交易中于 Entity Framework 外部完成的作業，請參閱 MSDN 上的[使用交易](https://msdn.microsoft.com/data/dn456843)。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-265">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Working with Transactions](https://msdn.microsoft.com/data/dn456843) on MSDN.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="1f0fc-266">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="1f0fc-266">Get the code</span></span>

[<span data-ttu-id="1f0fc-267">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="1f0fc-267">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="1f0fc-268">其他資源</span><span class="sxs-lookup"><span data-stu-id="1f0fc-268">Additional resources</span></span>

<span data-ttu-id="1f0fc-269">您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-269">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="1f0fc-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f0fc-270">Next step</span></span>

<span data-ttu-id="1f0fc-271">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="1f0fc-271">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f0fc-272">自訂課程頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-272">Customized courses pages</span></span>
> * <span data-ttu-id="1f0fc-273">已將 office 新增至講師頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-273">Added office to instructors page</span></span>
> * <span data-ttu-id="1f0fc-274">已將課程新增到講師頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-274">Added courses to instructors page</span></span>
> * <span data-ttu-id="1f0fc-275">已更新 DeleteConfirmed</span><span class="sxs-lookup"><span data-stu-id="1f0fc-275">Updated DeleteConfirmed</span></span>
> * <span data-ttu-id="1f0fc-276">將辦公室位置和課程新增至 [建立] 頁面</span><span class="sxs-lookup"><span data-stu-id="1f0fc-276">Added office location and courses to the Create page</span></span>

<span data-ttu-id="1f0fc-277">請前進到下一篇文章，以瞭解如何執行非同步程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="1f0fc-277">Advance to the next article to learn how to implement an asynchronous programming model.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1f0fc-278">非同步程式設計模型</span><span class="sxs-lookup"><span data-stu-id="1f0fc-278">Asynchronous programming model</span></span>](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
