---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第3部分：排序和篩選 |Microsoft Docs
author: tdykstra
description: 本教學課程系列是以 Entity Framework 4.0 教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631667"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="2d409-104">使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第3部分：排序和篩選</span><span class="sxs-lookup"><span data-stu-id="2d409-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="2d409-105">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2d409-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="2d409-106">本教學課程系列是[以 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。</span><span class="sxs-lookup"><span data-stu-id="2d409-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="2d409-107">如果您未完成先前的教學課程，做為本教學課程的起點，您可以下載您所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。</span><span class="sxs-lookup"><span data-stu-id="2d409-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="2d409-108">您也可以下載完整的教學課程系列所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。</span><span class="sxs-lookup"><span data-stu-id="2d409-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="2d409-109">如果您有關于教學課程的問題，可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2d409-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="2d409-110">在上一個教學課程中，您已在使用 Entity Framework 和 `ObjectDataSource` 控制項的多層式 web 應用程式中，實作為存放庫模式。</span><span class="sxs-lookup"><span data-stu-id="2d409-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="2d409-111">本教學課程說明如何進行排序和篩選，以及處理主版詳細資料案例。</span><span class="sxs-lookup"><span data-stu-id="2d409-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="2d409-112">您將會在 [*部門 .aspx* ] 頁面中加入下列增強功能：</span><span class="sxs-lookup"><span data-stu-id="2d409-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="2d409-113">允許使用者依名稱選取部門的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2d409-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="2d409-114">方格中所顯示之每個部門的課程清單。</span><span class="sxs-lookup"><span data-stu-id="2d409-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="2d409-115">按一下資料行標題來排序的功能。</span><span class="sxs-lookup"><span data-stu-id="2d409-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="2d409-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2d409-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="2d409-117">新增排序 GridView 資料行的功能</span><span class="sxs-lookup"><span data-stu-id="2d409-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="2d409-118">開啟 [*部門 .aspx* ] 頁面，並將 `SortParameterName="sortExpression"` 屬性加入至名為 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控制項。</span><span class="sxs-lookup"><span data-stu-id="2d409-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="2d409-119">（稍後您將建立使用名為 `sortExpression`之參數的 `GetDepartments` 方法）。控制項開頭標記的標記現在與下列範例類似。</span><span class="sxs-lookup"><span data-stu-id="2d409-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="2d409-120">將 `AllowSorting="true"` 屬性加入 `GridView` 控制項的開頭標記。</span><span class="sxs-lookup"><span data-stu-id="2d409-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="2d409-121">控制項開頭標記的標記現在與下列範例類似。</span><span class="sxs-lookup"><span data-stu-id="2d409-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="2d409-122">在*Departments.aspx.cs*中，從 `Page_Load` 方法呼叫 `GridView` 控制項的 `Sort` 方法，以設定預設排序次序：</span><span class="sxs-lookup"><span data-stu-id="2d409-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="2d409-123">您可以在商務邏輯類別或儲存機制類別中加入排序或篩選的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2d409-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="2d409-124">如果您在商務邏輯類別中執行此動作，則會在從資料庫抓取資料後完成排序或篩選工作，因為商務邏輯類別正在使用儲存機制所傳回的 `IEnumerable` 物件。</span><span class="sxs-lookup"><span data-stu-id="2d409-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="2d409-125">如果您在存放庫類別中加入排序和篩選程式代碼，並在 LINQ 運算式或物件查詢轉換成 `IEnumerable` 物件之前執行它，則您的命令會傳遞到資料庫進行處理，這通常會更有效率。</span><span class="sxs-lookup"><span data-stu-id="2d409-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="2d409-126">在本教學課程中，您將會以導致資料庫完成處理的方式（也就是在存放庫中）來執行排序和篩選。</span><span class="sxs-lookup"><span data-stu-id="2d409-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="2d409-127">若要加入排序功能，您必須將新的方法加入至存放庫介面和存放庫類別，以及商務邏輯類別。</span><span class="sxs-lookup"><span data-stu-id="2d409-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="2d409-128">在*ISchoolRepository.cs*檔案中，加入一個新的 `GetDepartments` 方法，它會使用 `sortExpression` 參數來排序傳回的部門清單：</span><span class="sxs-lookup"><span data-stu-id="2d409-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="2d409-129">`sortExpression` 參數將會指定要排序的資料行以及排序方向。</span><span class="sxs-lookup"><span data-stu-id="2d409-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="2d409-130">將新方法的程式碼新增至*SchoolRepository.cs*檔案：</span><span class="sxs-lookup"><span data-stu-id="2d409-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="2d409-131">變更現有的無參數 `GetDepartments` 方法以呼叫新的方法：</span><span class="sxs-lookup"><span data-stu-id="2d409-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="2d409-132">在測試專案中，將下列新方法新增至*MockSchoolRepository.cs*：</span><span class="sxs-lookup"><span data-stu-id="2d409-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="2d409-133">如果您要建立相依于此方法並傳回已排序清單的任何單元測試，您必須先排序清單，再將它傳回。</span><span class="sxs-lookup"><span data-stu-id="2d409-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="2d409-134">您不會在本教學課程中建立像這樣的測試，因此方法可以只傳回未排序的部門清單。</span><span class="sxs-lookup"><span data-stu-id="2d409-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="2d409-135">在*SchoolBL.cs*檔案中，將下列新方法新增至商務邏輯類別：</span><span class="sxs-lookup"><span data-stu-id="2d409-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="2d409-136">此程式碼會將排序參數傳遞至存放庫方法。</span><span class="sxs-lookup"><span data-stu-id="2d409-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="2d409-137">執行 [*部門 .aspx* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="2d409-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="2d409-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2d409-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="2d409-139">您現在可以按一下任何資料行標題，依該資料行排序。</span><span class="sxs-lookup"><span data-stu-id="2d409-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="2d409-140">如果資料行已經排序，按一下標題會反轉排序方向。</span><span class="sxs-lookup"><span data-stu-id="2d409-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="2d409-141">新增搜尋方塊</span><span class="sxs-lookup"><span data-stu-id="2d409-141">Adding a Search Box</span></span>

<span data-ttu-id="2d409-142">在本節中，您將加入搜尋文字方塊、使用控制項參數將它連結至 `ObjectDataSource` 控制項，以及將方法加入商務邏輯類別以支援篩選。</span><span class="sxs-lookup"><span data-stu-id="2d409-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="2d409-143">開啟 [*部門 .aspx* ] 頁面，並在標題和第一個 `ObjectDataSource` 控制項之間加入下列標記：</span><span class="sxs-lookup"><span data-stu-id="2d409-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="2d409-144">在名為 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控制項中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="2d409-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="2d409-145">為名為 `nameSearchString` 的參數新增 `SelectParameters` 專案，以取得 `SearchTextBox` 控制項中輸入的值。</span><span class="sxs-lookup"><span data-stu-id="2d409-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="2d409-146">將 `SelectMethod` 屬性值變更為 `GetDepartmentsByName`。</span><span class="sxs-lookup"><span data-stu-id="2d409-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="2d409-147">（您稍後會建立此方法）。</span><span class="sxs-lookup"><span data-stu-id="2d409-147">(You'll create this method later.)</span></span>

<span data-ttu-id="2d409-148">`ObjectDataSource` 控制項的標記現在與下列範例類似：</span><span class="sxs-lookup"><span data-stu-id="2d409-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="2d409-149">在*ISchoolRepository.cs*中，新增同時採用 `sortExpression` 和 `nameSearchString` 參數的 `GetDepartmentsByName` 方法：</span><span class="sxs-lookup"><span data-stu-id="2d409-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="2d409-150">在*SchoolRepository.cs*中，新增下列新方法：</span><span class="sxs-lookup"><span data-stu-id="2d409-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="2d409-151">這段程式碼會使用 `Where` 方法來選取包含搜尋字串的專案。</span><span class="sxs-lookup"><span data-stu-id="2d409-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="2d409-152">如果搜尋字串是空的，則會選取所有記錄。</span><span class="sxs-lookup"><span data-stu-id="2d409-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="2d409-153">請注意，當您在像這樣的一個語句中同時指定方法呼叫（`Include`，然後 `OrderBy`，然後 `Where`），`Where` 方法一律必須是最後一個。</span><span class="sxs-lookup"><span data-stu-id="2d409-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="2d409-154">變更使用 `sortExpression` 參數的現有 `GetDepartments` 方法，以呼叫新的方法：</span><span class="sxs-lookup"><span data-stu-id="2d409-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="2d409-155">在測試專案的*MockSchoolRepository.cs*中，新增下列新方法：</span><span class="sxs-lookup"><span data-stu-id="2d409-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="2d409-156">在*SchoolBL.cs*中，新增下列新方法：</span><span class="sxs-lookup"><span data-stu-id="2d409-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="2d409-157">執行 [*部門 .aspx* ] 頁面並輸入搜尋字串，以確定選取邏輯可以運作。</span><span class="sxs-lookup"><span data-stu-id="2d409-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="2d409-158">將文字方塊保留空白，然後嘗試進行搜尋，以確保會傳回所有記錄。</span><span class="sxs-lookup"><span data-stu-id="2d409-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="2d409-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2d409-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="2d409-160">為每個格線列加入詳細資料行</span><span class="sxs-lookup"><span data-stu-id="2d409-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="2d409-161">接下來，您想要查看方格右側儲存格中顯示之每個部門的所有課程。</span><span class="sxs-lookup"><span data-stu-id="2d409-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="2d409-162">若要這麼做，您將使用嵌套的 `GridView` 控制項，並將它從 `Department` 實體的 `Courses` 導覽屬性中的資料進行 databind。</span><span class="sxs-lookup"><span data-stu-id="2d409-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="2d409-163">開啟 *部門 .aspx* ，然後在 `GridView` 控制項的標記中，指定 `RowDataBound` 事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="2d409-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="2d409-164">控制項開頭標記的標記現在與下列範例類似。</span><span class="sxs-lookup"><span data-stu-id="2d409-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="2d409-165">在 [`Administrator` 範本] 欄位之後加入新的 `TemplateField` 元素：</span><span class="sxs-lookup"><span data-stu-id="2d409-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="2d409-166">此標記會建立一個嵌套的 `GridView` 控制項，以顯示課程清單的課程編號和標題。</span><span class="sxs-lookup"><span data-stu-id="2d409-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="2d409-167">它不會指定資料來源，因為您會將它以 `RowDataBound` 處理常式中的程式碼進行 databind。</span><span class="sxs-lookup"><span data-stu-id="2d409-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="2d409-168">開啟*Departments.aspx.cs* ，並新增下列 `RowDataBound` 事件的處理常式：</span><span class="sxs-lookup"><span data-stu-id="2d409-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="2d409-169">此程式碼會從事件引數取得 `Department` 實體、將 `Courses` 導覽屬性轉換為 `List` 集合，並將嵌套的 `GridView` 將至集合。</span><span class="sxs-lookup"><span data-stu-id="2d409-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="2d409-170">開啟*SchoolRepository.cs*檔案，並在您于 `GetDepartmentsByName` 方法中建立的物件查詢中呼叫 `Include` 方法，以指定 `Courses` 導覽屬性的積極式載入。</span><span class="sxs-lookup"><span data-stu-id="2d409-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="2d409-171">`GetDepartmentsByName` 方法中的 `return` 語句現在與下列範例類似。</span><span class="sxs-lookup"><span data-stu-id="2d409-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="2d409-172">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="2d409-172">Run the page.</span></span> <span data-ttu-id="2d409-173">除了您稍早新增的排序和篩選功能之外，GridView 控制項現在會顯示每個部門的嵌套課程詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2d409-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="2d409-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2d409-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="2d409-175">這會完成排序、篩選和主版詳細資料案例的簡介。</span><span class="sxs-lookup"><span data-stu-id="2d409-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="2d409-176">在下一個教學課程中，您將瞭解如何處理平行存取。</span><span class="sxs-lookup"><span data-stu-id="2d409-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2d409-177">[上一頁](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [下一頁](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="2d409-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
