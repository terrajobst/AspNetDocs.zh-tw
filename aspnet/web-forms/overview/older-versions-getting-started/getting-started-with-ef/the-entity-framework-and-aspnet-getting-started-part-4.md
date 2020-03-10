---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: 具有 Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第4部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638163"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a><span data-ttu-id="163eb-104">Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第4部分</span><span class="sxs-lookup"><span data-stu-id="163eb-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 4</span></span>

<span data-ttu-id="163eb-105">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="163eb-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="163eb-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="163eb-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="163eb-107">如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程</span><span class="sxs-lookup"><span data-stu-id="163eb-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="working-with-related-data"></a><span data-ttu-id="163eb-108">使用相關資料</span><span class="sxs-lookup"><span data-stu-id="163eb-108">Working with Related Data</span></span>

<span data-ttu-id="163eb-109">在上一個教學課程中，您使用了 `EntityDataSource` 控制項來篩選、排序和分組資料。</span><span class="sxs-lookup"><span data-stu-id="163eb-109">In the previous tutorial you used the `EntityDataSource` control to filter, sort, and group data.</span></span> <span data-ttu-id="163eb-110">在本教學課程中，您將會顯示及更新相關資料。</span><span class="sxs-lookup"><span data-stu-id="163eb-110">In this tutorial you'll display and update related data.</span></span>

<span data-ttu-id="163eb-111">您將建立顯示講師清單的講師頁面。</span><span class="sxs-lookup"><span data-stu-id="163eb-111">You'll create the Instructors page that shows a list of instructors.</span></span> <span data-ttu-id="163eb-112">當您選取講師時，您會看到該講師所教授的課程清單。</span><span class="sxs-lookup"><span data-stu-id="163eb-112">When you select an instructor, you see a list of courses taught by that instructor.</span></span> <span data-ttu-id="163eb-113">當您選取課程時，您會看到課程的詳細資料，以及在課程中註冊的學生清單。</span><span class="sxs-lookup"><span data-stu-id="163eb-113">When you select a course, you see details for the course and a list of students enrolled in the course.</span></span> <span data-ttu-id="163eb-114">您可以編輯講師姓名、雇用日期和辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="163eb-114">You can edit the instructor name, hire date, and office assignment.</span></span> <span data-ttu-id="163eb-115">Office 指派是您透過導覽屬性存取的個別實體集。</span><span class="sxs-lookup"><span data-stu-id="163eb-115">The office assignment is a separate entity set that you access through a navigation property.</span></span>

<span data-ttu-id="163eb-116">您可以將主要資料連結至標記或程式碼中的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="163eb-116">You can link master data to detail data in markup or in code.</span></span> <span data-ttu-id="163eb-117">在本教學課程的這個部分中，您將使用這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="163eb-117">In this part of the tutorial, you'll use both methods.</span></span>

<span data-ttu-id="163eb-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span></span>

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a><span data-ttu-id="163eb-119">顯示和更新 GridView 控制項中的相關實體</span><span class="sxs-lookup"><span data-stu-id="163eb-119">Displaying and Updating Related Entities in a GridView Control</span></span>

<span data-ttu-id="163eb-120">建立名為*default.aspx*的新網頁，此網頁會使用*網站*主要頁面，並將下列標記新增至名為 `Content2`的 `Content` 控制項：</span><span class="sxs-lookup"><span data-stu-id="163eb-120">Create a new web page named *Instructors.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

<span data-ttu-id="163eb-121">此標記會建立一個 `EntityDataSource` 控制項，以選取講師並啟用更新。</span><span class="sxs-lookup"><span data-stu-id="163eb-121">This markup creates an `EntityDataSource` control that selects instructors and enables updates.</span></span> <span data-ttu-id="163eb-122">`div` 元素會將標記設定為在左側轉譯，讓您稍後可以在右側新增資料行。</span><span class="sxs-lookup"><span data-stu-id="163eb-122">The `div` element configures markup to render on the left so that you can add a column on the right later.</span></span>

<span data-ttu-id="163eb-123">在 `EntityDataSource` 標記和結尾 `</div>` 標記之間，新增下列標記，以建立您將用於錯誤訊息的 `GridView` 控制項和 `Label` 控制項：</span><span class="sxs-lookup"><span data-stu-id="163eb-123">Between the `EntityDataSource` markup and the closing `</div>` tag, add the following markup that creates a `GridView` control and a `Label` control that you'll use for error messages:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

<span data-ttu-id="163eb-124">此 `GridView` 控制項可讓您選取資料列、以淺灰色背景色彩反白顯示選取的資料列，並指定 `SelectedIndexChanged` 和 `Updating` 事件的處理常式（您稍後會建立）。</span><span class="sxs-lookup"><span data-stu-id="163eb-124">This `GridView` control enables row selection, highlights the selected row with a light gray background color, and specifies handlers (which you'll create later) for the `SelectedIndexChanged` and `Updating` events.</span></span> <span data-ttu-id="163eb-125">它也會指定 `DataKeyNames` 屬性的 `PersonID`，讓選取之資料列的索引鍵值可以傳遞至您稍後將新增的另一個控制項。</span><span class="sxs-lookup"><span data-stu-id="163eb-125">It also specifies `PersonID` for the `DataKeyNames` property, so that the key value of the selected row can be passed to another control that you'll add later.</span></span>

<span data-ttu-id="163eb-126">最後一個資料行包含講師的辦公室指派，其儲存在 `Person` 實體的導覽屬性中，因為它來自相關聯的實體。</span><span class="sxs-lookup"><span data-stu-id="163eb-126">The last column contains the instructor's office assignment, which is stored in a navigation property of the `Person` entity because it comes from an associated entity.</span></span> <span data-ttu-id="163eb-127">請注意，`EditItemTemplate` 元素會指定 `Eval` 而不是 `Bind`，因為 `GridView` 控制項無法直接系結至導覽屬性，以便更新它們。</span><span class="sxs-lookup"><span data-stu-id="163eb-127">Notice that the `EditItemTemplate` element specifies `Eval` instead of `Bind`, because the `GridView` control cannot directly bind to navigation properties in order to update them.</span></span> <span data-ttu-id="163eb-128">您將會在程式碼中更新辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="163eb-128">You'll update the office assignment in code.</span></span> <span data-ttu-id="163eb-129">若要這麼做，您需要 `TextBox` 控制項的參考，然後在 `TextBox` 控制項的 `Init` 事件中取得並儲存該專案。</span><span class="sxs-lookup"><span data-stu-id="163eb-129">To do that, you'll need a reference to the `TextBox` control, and you'll get and save that in the `TextBox` control's `Init` event.</span></span>

<span data-ttu-id="163eb-130">遵循 `GridView` 控制項是用於錯誤訊息的 `Label` 控制項。</span><span class="sxs-lookup"><span data-stu-id="163eb-130">Following the `GridView` control is a `Label` control that's used for error messages.</span></span> <span data-ttu-id="163eb-131">控制項的 `Visible` 屬性為 `false`，而 view 狀態為 off，只有在程式碼讓標籤顯示為回應錯誤時才會出現。</span><span class="sxs-lookup"><span data-stu-id="163eb-131">The control's `Visible` property is `false`, and view state is turned off, so that the label will appear only when code makes it visible in response to an error.</span></span>

<span data-ttu-id="163eb-132">開啟*Instructors.aspx.cs*檔案，並新增下列 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="163eb-132">Open the *Instructors.aspx.cs* file and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

<span data-ttu-id="163eb-133">緊接在部分類別名稱宣告之後加入私用類別欄位，以保存 [office 指派] 文字方塊的參考。</span><span class="sxs-lookup"><span data-stu-id="163eb-133">Add a private class field immediately after the partial-class name declaration to hold a reference to the office assignment text box.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

<span data-ttu-id="163eb-134">為您稍後要加入程式碼的 `SelectedIndexChanged` 事件處理常式新增 stub。</span><span class="sxs-lookup"><span data-stu-id="163eb-134">Add a stub for the `SelectedIndexChanged` event handler that you'll add code for later.</span></span> <span data-ttu-id="163eb-135">此外，也請加入 office 指派 `TextBox` 控制項的 `Init` 事件的處理常式，讓您可以儲存 `TextBox` 控制項的參考。</span><span class="sxs-lookup"><span data-stu-id="163eb-135">Also add a handler for the office assignment `TextBox` control's `Init` event so that you can store a reference to the `TextBox` control.</span></span> <span data-ttu-id="163eb-136">您將使用此參考來取得使用者輸入的值，以便更新與導覽屬性相關聯的實體。</span><span class="sxs-lookup"><span data-stu-id="163eb-136">You'll use this reference to get the value the user entered in order to update the entity associated with the navigation property.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

<span data-ttu-id="163eb-137">您將使用 `GridView` 控制項的 `Updating` 事件來更新相關聯 `OfficeAssignment` 實體的 `Location` 屬性。</span><span class="sxs-lookup"><span data-stu-id="163eb-137">You'll use the `GridView` control's `Updating` event to update the `Location` property of the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="163eb-138">為 `Updating` 事件新增下列處理常式：</span><span class="sxs-lookup"><span data-stu-id="163eb-138">Add the following handler for the `Updating` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

<span data-ttu-id="163eb-139">這段程式碼會在使用者按一下 `GridView` 資料列中的 [**更新**] 時執行。</span><span class="sxs-lookup"><span data-stu-id="163eb-139">This code is run when the user clicks **Update** in a `GridView` row.</span></span> <span data-ttu-id="163eb-140">程式碼會使用 LINQ to Entities，以從事件引數中選取的資料列 `PersonID`，抓取與目前 `Person` 實體相關聯的 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="163eb-140">The code uses LINQ to Entities to retrieve the `OfficeAssignment` entity that's associated with the current `Person` entity, using the `PersonID` of the selected row from the event argument.</span></span>

<span data-ttu-id="163eb-141">然後，程式碼會根據 `InstructorOfficeTextBox` 控制項中的值，採取下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="163eb-141">The code then takes one of the following actions depending on the value in the `InstructorOfficeTextBox` control:</span></span>

- <span data-ttu-id="163eb-142">如果文字方塊具有值，而且沒有要更新的 `OfficeAssignment` 實體，則會建立一個。</span><span class="sxs-lookup"><span data-stu-id="163eb-142">If the text box has a value and there's no `OfficeAssignment` entity to update, it creates one.</span></span>
- <span data-ttu-id="163eb-143">如果文字方塊具有值，而且有 `OfficeAssignment` 實體，則會更新 `Location` 屬性值。</span><span class="sxs-lookup"><span data-stu-id="163eb-143">If the text box has a value and there's an `OfficeAssignment` entity, it updates the `Location` property value.</span></span>
- <span data-ttu-id="163eb-144">如果文字方塊是空的，且 `OfficeAssignment` 實體存在，則會刪除實體。</span><span class="sxs-lookup"><span data-stu-id="163eb-144">If the text box is empty and an `OfficeAssignment` entity exists, it deletes the entity.</span></span>

<span data-ttu-id="163eb-145">之後，它會將變更儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="163eb-145">After this, it saves the changes to the database.</span></span> <span data-ttu-id="163eb-146">如果發生例外狀況，則會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="163eb-146">If an exception occurs, it displays an error message.</span></span>

<span data-ttu-id="163eb-147">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="163eb-147">Run the page.</span></span>

<span data-ttu-id="163eb-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span></span>

<span data-ttu-id="163eb-149">按一下 [**編輯**]，所有欄位都會變更為文字方塊。</span><span class="sxs-lookup"><span data-stu-id="163eb-149">Click **Edit** and all fields change to text boxes.</span></span>

<span data-ttu-id="163eb-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span></span>

<span data-ttu-id="163eb-151">變更其中任何值，包括**辦公室指派**。</span><span class="sxs-lookup"><span data-stu-id="163eb-151">Change any of these values, including **Office Assignment**.</span></span> <span data-ttu-id="163eb-152">按一下 [**更新**]，您就會看到這些變更反映在清單中。</span><span class="sxs-lookup"><span data-stu-id="163eb-152">Click **Update** and you'll see the changes reflected in the list.</span></span>

## <a name="displaying-related-entities-in-a-separate-control"></a><span data-ttu-id="163eb-153">在不同的控制項中顯示相關實體</span><span class="sxs-lookup"><span data-stu-id="163eb-153">Displaying Related Entities in a Separate Control</span></span>

<span data-ttu-id="163eb-154">每位講師都可以教授一或多個課程，因此您將新增一個 `EntityDataSource` 控制項和一個 `GridView` 控制項，以列出與講師 `GridView` 控制項中所選講師相關聯的課程。</span><span class="sxs-lookup"><span data-stu-id="163eb-154">Each instructor can teach one or more courses, so you'll add an `EntityDataSource` control and a `GridView` control to list the courses associated with whichever instructor is selected in the instructors `GridView` control.</span></span> <span data-ttu-id="163eb-155">若要建立課程實體的標題和 `EntityDataSource` 控制項，請在錯誤訊息 `Label` 控制項和結尾 `</div>` 標記之間新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="163eb-155">To create a heading and the `EntityDataSource` control for courses entities, add the following markup between the error message `Label` control and the closing `</div>` tag:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

<span data-ttu-id="163eb-156">`Where` 參數包含在 `InstructorsGridView` 控制項中選取資料列之講師的 `PersonID` 值。</span><span class="sxs-lookup"><span data-stu-id="163eb-156">The `Where` parameter contains the value of the `PersonID` of the instructor whose row is selected in the `InstructorsGridView` control.</span></span> <span data-ttu-id="163eb-157">`Where` 屬性包含子選擇命令，可從 `Course` 實體的 `People` 導覽屬性取得所有關聯的 `Person` 實體，只有在其中一個相關聯的 `Course` 實體包含選取的 `Person` 值時，才會選取 `PersonID` 實體。</span><span class="sxs-lookup"><span data-stu-id="163eb-157">The `Where` property contains a subselect command that gets all associated `Person` entities from a `Course` entity's `People` navigation property and selects the `Course` entity only if one of the associated `Person` entities contains the selected `PersonID` value.</span></span>

<span data-ttu-id="163eb-158">若要建立 `GridView` 控制項，請在 `CoursesEntityDataSource` 控制項後面緊接著新增下列標記（在結尾 `</div>` 標記之前）：</span><span class="sxs-lookup"><span data-stu-id="163eb-158">To create the `GridView` control., add the following markup immediately following the `CoursesEntityDataSource` control (before the closing `</div>` tag):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

<span data-ttu-id="163eb-159">因為若未選取任何講師，將不會顯示任何課程，則會包含 `EmptyDataTemplate` 元素。</span><span class="sxs-lookup"><span data-stu-id="163eb-159">Because no courses will be displayed if no instructor is selected, an `EmptyDataTemplate` element is included.</span></span>

<span data-ttu-id="163eb-160">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="163eb-160">Run the page.</span></span>

<span data-ttu-id="163eb-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span></span>

<span data-ttu-id="163eb-162">選取已指派一或多個課程的講師，而課程或課程則會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="163eb-162">Select an instructor who has one or more courses assigned, and the course or courses appear in the list.</span></span> <span data-ttu-id="163eb-163">（注意：雖然資料庫架構允許多個課程，但在資料庫提供的測試資料中，沒有任何講師實際有一個以上的課程。</span><span class="sxs-lookup"><span data-stu-id="163eb-163">(Note: although the database schema allows multiple courses, in the test data supplied with the database no instructor actually has more than one course.</span></span> <span data-ttu-id="163eb-164">您可以使用 [**伺服器總管**] 視窗或 [ *CoursesAdd* ] 頁面（您將在稍後的教學課程中加入），自行將課程新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="163eb-164">You can add courses to the database yourself using the **Server Explorer** window or the *CoursesAdd.aspx* page, which you'll add in a later tutorial.)</span></span>

<span data-ttu-id="163eb-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span></span>

<span data-ttu-id="163eb-166">`CoursesGridView` 控制項只會顯示一些課程欄位。</span><span class="sxs-lookup"><span data-stu-id="163eb-166">The `CoursesGridView` control shows only a few course fields.</span></span> <span data-ttu-id="163eb-167">若要顯示課程的所有詳細資料，您將會在使用者選取的課程中使用 `DetailsView` 控制項。</span><span class="sxs-lookup"><span data-stu-id="163eb-167">To display all the details for a course, you'll use a `DetailsView` control for the course that the user selects.</span></span> <span data-ttu-id="163eb-168">在*default.aspx*中，于結尾 `</div>` 標籤後面新增下列標記（請確定您將此標記放在結尾 div 標記**之後**，而不是在它之前）：</span><span class="sxs-lookup"><span data-stu-id="163eb-168">In *Instructors.aspx*, add the following markup after the closing `</div>` tag (make sure you place this markup **after** the closing div tag, not before it):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

<span data-ttu-id="163eb-169">此標記會建立系結至 `Courses` 實體集的 `EntityDataSource` 控制項。</span><span class="sxs-lookup"><span data-stu-id="163eb-169">This markup creates an `EntityDataSource` control that's bound to the `Courses` entity set.</span></span> <span data-ttu-id="163eb-170">`Where` 屬性會使用課程 `GridView` 控制項中所選取資料列的 `CourseID` 值來選取課程。</span><span class="sxs-lookup"><span data-stu-id="163eb-170">The `Where` property selects a course using the `CourseID` value of the selected row in the courses `GridView` control.</span></span> <span data-ttu-id="163eb-171">標記會指定 `Selected` 事件的處理常式，稍後您會用來顯示學生成績，也就是階層中較低的另一個層級。</span><span class="sxs-lookup"><span data-stu-id="163eb-171">The markup specifies a handler for the `Selected` event, which you'll use later for displaying student grades, which is another level lower in the hierarchy.</span></span>

<span data-ttu-id="163eb-172">在*Instructors.aspx.cs*中，為 `CourseDetailsEntityDataSource_Selected` 方法建立下列 stub。</span><span class="sxs-lookup"><span data-stu-id="163eb-172">In *Instructors.aspx.cs*, create the following stub for the `CourseDetailsEntityDataSource_Selected` method.</span></span> <span data-ttu-id="163eb-173">（您稍後會在本教學課程中填入此存根; 現在，您需要它，才能編譯和執行頁面。）</span><span class="sxs-lookup"><span data-stu-id="163eb-173">(You'll fill this stub out later in the tutorial; for now, you need it so that the page will compile and run.)</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

<span data-ttu-id="163eb-174">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="163eb-174">Run the page.</span></span>

<span data-ttu-id="163eb-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span></span>

<span data-ttu-id="163eb-176">一開始沒有任何課程詳細資料，因為沒有選取任何課程。</span><span class="sxs-lookup"><span data-stu-id="163eb-176">Initially there are no course details because no course is selected.</span></span> <span data-ttu-id="163eb-177">選取已指派課程的講師，然後選取課程以查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="163eb-177">Select an instructor who has a course assigned, and then select a course to see the details.</span></span>

<span data-ttu-id="163eb-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span></span>

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a><span data-ttu-id="163eb-179">使用 EntityDataSource 的「選取」事件來顯示相關資料</span><span class="sxs-lookup"><span data-stu-id="163eb-179">Using the EntityDataSource "Selected" Event to Display Related Data</span></span>

<span data-ttu-id="163eb-180">最後，您想要顯示所選課程的所有已註冊學生和其成績。</span><span class="sxs-lookup"><span data-stu-id="163eb-180">Finally, you want to show all of the enrolled students and their grades for the selected course.</span></span> <span data-ttu-id="163eb-181">若要這麼做，您將使用系結至課程 `DetailsView`之 `EntityDataSource` 控制項的 `Selected` 事件。</span><span class="sxs-lookup"><span data-stu-id="163eb-181">To do this, you'll use the `Selected` event of the `EntityDataSource` control bound to the course `DetailsView`.</span></span>

<span data-ttu-id="163eb-182">在*default.aspx*中，于 `DetailsView` 控制項之後加入下列標記：</span><span class="sxs-lookup"><span data-stu-id="163eb-182">In *Instructors.aspx*, add the following markup after the `DetailsView` control:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

<span data-ttu-id="163eb-183">此標記會建立一個 `ListView` 控制項，其中顯示所選課程的學生清單及其成績。</span><span class="sxs-lookup"><span data-stu-id="163eb-183">This markup creates a `ListView` control that displays a list of students and their grades for the selected course.</span></span> <span data-ttu-id="163eb-184">沒有指定資料來源，因為您會在程式碼中將控制項進行 databind。</span><span class="sxs-lookup"><span data-stu-id="163eb-184">No data source is specified because you'll databind the control in code.</span></span> <span data-ttu-id="163eb-185">[`EmptyDataTemplate`] 元素會提供在未選取任何課程時顯示的訊息，在此情況下，沒有任何學生可顯示。</span><span class="sxs-lookup"><span data-stu-id="163eb-185">The `EmptyDataTemplate` element provides a message to display when no course is selected—in that case, there are no students to display.</span></span> <span data-ttu-id="163eb-186">`LayoutTemplate` 元素會建立一個 HTML 資料表來顯示清單，而 `ItemTemplate` 則指定要顯示的資料行。</span><span class="sxs-lookup"><span data-stu-id="163eb-186">The `LayoutTemplate` element creates an HTML table to display the list, and the `ItemTemplate` specifies the columns to display.</span></span> <span data-ttu-id="163eb-187">學生識別碼和學生的成績來自 `StudentGrade` 實體，而 student 名稱則來自 Entity Framework 在 `StudentGrade` 實體的 `Person` 導覽屬性中提供的 `Person` 實體。</span><span class="sxs-lookup"><span data-stu-id="163eb-187">The student ID and the student grade are from the `StudentGrade` entity, and the student name is from the `Person` entity that the Entity Framework makes available in the `Person` navigation property of the `StudentGrade` entity.</span></span>

<span data-ttu-id="163eb-188">在*Instructors.aspx.cs*中，以下列程式碼取代 stub 時 `CourseDetailsEntityDataSource_Selected` 方法：</span><span class="sxs-lookup"><span data-stu-id="163eb-188">In *Instructors.aspx.cs*, replace the stubbed-out `CourseDetailsEntityDataSource_Selected` method with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

<span data-ttu-id="163eb-189">這個事件的事件引數會以集合的形式提供選取的資料，如果未選取任何專案，則會有零個專案，如果選取了 `Course` 的實體，則會有一個專案。</span><span class="sxs-lookup"><span data-stu-id="163eb-189">The event argument for this event provides the selected data in the form of a collection, which will have zero items if nothing is selected or one item if a `Course` entity is selected.</span></span> <span data-ttu-id="163eb-190">如果選取了 `Course` 的實體，程式碼會使用 `First` 方法，將集合轉換成單一物件。</span><span class="sxs-lookup"><span data-stu-id="163eb-190">If a `Course` entity is selected, the code uses the `First` method to convert the collection to a single object.</span></span> <span data-ttu-id="163eb-191">然後，它會從導覽屬性取得 `StudentGrade` 的實體、將其轉換成集合，並將 `GradesListView` 控制項系結至集合。</span><span class="sxs-lookup"><span data-stu-id="163eb-191">It then gets `StudentGrade` entities from the navigation property, converts them to a collection, and binds the `GradesListView` control to the collection.</span></span>

<span data-ttu-id="163eb-192">這就足以顯示成績，但是您想要確定在第一次顯示頁面時，以及每次未選取課程時，都會顯示空白資料範本中的訊息。</span><span class="sxs-lookup"><span data-stu-id="163eb-192">This is sufficient to display grades, but you want to make sure that the message in the empty data template is displayed the first time the page is displayed and whenever a course is not selected.</span></span> <span data-ttu-id="163eb-193">若要這麼做，請建立下列方法，這會從兩個位置呼叫：</span><span class="sxs-lookup"><span data-stu-id="163eb-193">To do that, create the following method, which you'll call from two places:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

<span data-ttu-id="163eb-194">從 `Page_Load` 方法呼叫這個新方法，以在第一次顯示頁面時顯示空白資料範本。</span><span class="sxs-lookup"><span data-stu-id="163eb-194">Call this new method from the `Page_Load` method to display the empty data template the first time the page is displayed.</span></span> <span data-ttu-id="163eb-195">然後從 `InstructorsGridView_SelectedIndexChanged` 方法呼叫它，因為當選取講師時，就會引發該事件，這表示新課程會載入課程 `GridView` 控制項，而且尚未選取任何專案。</span><span class="sxs-lookup"><span data-stu-id="163eb-195">And call it from the `InstructorsGridView_SelectedIndexChanged` method because that event is raised when an instructor is selected, which means new courses are loaded into the courses `GridView` control and none is selected yet.</span></span> <span data-ttu-id="163eb-196">以下是兩個呼叫：</span><span class="sxs-lookup"><span data-stu-id="163eb-196">Here are the two calls:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

<span data-ttu-id="163eb-197">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="163eb-197">Run the page.</span></span>

<span data-ttu-id="163eb-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span></span>

<span data-ttu-id="163eb-199">選取已指派課程的講師，然後選取課程。</span><span class="sxs-lookup"><span data-stu-id="163eb-199">Select an instructor that has a course assigned, and then select the course.</span></span>

<span data-ttu-id="163eb-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="163eb-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span></span>

<span data-ttu-id="163eb-201">您現在已經看過一些使用相關資料的方式。</span><span class="sxs-lookup"><span data-stu-id="163eb-201">You have now seen a few ways to work with related data.</span></span> <span data-ttu-id="163eb-202">在下列教學課程中，您將瞭解如何加入現有實體之間的關聯性、如何移除關聯性，以及如何加入與現有實體具有關聯性的新實體。</span><span class="sxs-lookup"><span data-stu-id="163eb-202">In the following tutorial, you'll learn how to add relationships between existing entities, how to remove relationships, and how to add a new entity that has a relationship to an existing entity.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="163eb-203">[上一頁](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [下一頁](the-entity-framework-and-aspnet-getting-started-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="163eb-203">[Previous](the-entity-framework-and-aspnet-getting-started-part-3.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-5.md)</span></span>
