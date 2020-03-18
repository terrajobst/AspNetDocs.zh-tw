---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 使用模型系結和 web forms 排序、分頁及篩選資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548059"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="5b613-104">使用模型系結和 web forms 排序、分頁及篩選資料</span><span class="sxs-lookup"><span data-stu-id="5b613-104">Sorting, paging, and filtering data with model binding and web forms</span></span>

<span data-ttu-id="5b613-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5b613-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5b613-106">本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。</span><span class="sxs-lookup"><span data-stu-id="5b613-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="5b613-107">模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。</span><span class="sxs-lookup"><span data-stu-id="5b613-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="5b613-108">此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。</span><span class="sxs-lookup"><span data-stu-id="5b613-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="5b613-109">本教學課程說明如何透過模型系結來加入排序、分頁和篩選資料。</span><span class="sxs-lookup"><span data-stu-id="5b613-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="5b613-110">本教學課程是以系列第一個[部分](retrieving-data.md)中所建立的專案為基礎。</span><span class="sxs-lookup"><span data-stu-id="5b613-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="5b613-111">您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。</span><span class="sxs-lookup"><span data-stu-id="5b613-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="5b613-112">可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="5b613-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="5b613-113">它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。</span><span class="sxs-lookup"><span data-stu-id="5b613-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="5b613-114">您將建立的內容</span><span class="sxs-lookup"><span data-stu-id="5b613-114">What you'll build</span></span>

<span data-ttu-id="5b613-115">在本教學課程中，您將會：</span><span class="sxs-lookup"><span data-stu-id="5b613-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="5b613-116">啟用資料的排序和分頁</span><span class="sxs-lookup"><span data-stu-id="5b613-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="5b613-117">根據使用者的選取專案來啟用資料篩選</span><span class="sxs-lookup"><span data-stu-id="5b613-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="5b613-118">新增排序</span><span class="sxs-lookup"><span data-stu-id="5b613-118">Add sorting</span></span>

<span data-ttu-id="5b613-119">在 GridView 中啟用排序非常簡單。</span><span class="sxs-lookup"><span data-stu-id="5b613-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="5b613-120">在 Student .aspx 檔案中，直接在 GridView 中將**AllowSorting**設定為**true** 。</span><span class="sxs-lookup"><span data-stu-id="5b613-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="5b613-121">當 DataField 自動使用時，您不需要為每個資料行設定**SortExpression**值。</span><span class="sxs-lookup"><span data-stu-id="5b613-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="5b613-122">GridView 會修改查詢，以包含依據選取的值來排序資料。</span><span class="sxs-lookup"><span data-stu-id="5b613-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="5b613-123">下列反白顯示的程式碼顯示啟用排序所需的加法。</span><span class="sxs-lookup"><span data-stu-id="5b613-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="5b613-124">執行 web 應用程式，並依據不同資料行中的值來測試排序 student 記錄。</span><span class="sxs-lookup"><span data-stu-id="5b613-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![排序學生](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="5b613-126">新增分頁</span><span class="sxs-lookup"><span data-stu-id="5b613-126">Add paging</span></span>

<span data-ttu-id="5b613-127">啟用分頁也非常簡單。</span><span class="sxs-lookup"><span data-stu-id="5b613-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="5b613-128">在 GridView 中，將**AllowPaging**屬性設定為**true** ，並將**PageSize**屬性設為您想要在每個頁面上顯示的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="5b613-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="5b613-129">在本教學課程中，您可以將它設定為4。</span><span class="sxs-lookup"><span data-stu-id="5b613-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="5b613-130">執行 web 應用程式，並注意現在記錄會分割成多個頁面，而不會在單一頁面上顯示超過4筆記錄。</span><span class="sxs-lookup"><span data-stu-id="5b613-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![新增分頁](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="5b613-132">延遲的查詢執行可改善應用程式的效率。</span><span class="sxs-lookup"><span data-stu-id="5b613-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="5b613-133">GridView 不會抓取整個資料集，而是修改查詢，只抓取目前頁面的記錄。</span><span class="sxs-lookup"><span data-stu-id="5b613-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="5b613-134">依使用者選擇篩選記錄</span><span class="sxs-lookup"><span data-stu-id="5b613-134">Filter records by user selection</span></span>

<span data-ttu-id="5b613-135">模型系結會加入數個屬性，可讓您指定如何在模型系結方法中設定參數的值。</span><span class="sxs-lookup"><span data-stu-id="5b613-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="5b613-136">這些屬性位於**ModelBinding**命名空間中。</span><span class="sxs-lookup"><span data-stu-id="5b613-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="5b613-137">其中包括：</span><span class="sxs-lookup"><span data-stu-id="5b613-137">They include:</span></span>

- <span data-ttu-id="5b613-138">控制項</span><span class="sxs-lookup"><span data-stu-id="5b613-138">Control</span></span>
- <span data-ttu-id="5b613-139">Cookie</span><span class="sxs-lookup"><span data-stu-id="5b613-139">Cookie</span></span>
- <span data-ttu-id="5b613-140">表單</span><span class="sxs-lookup"><span data-stu-id="5b613-140">Form</span></span>
- <span data-ttu-id="5b613-141">設定檔</span><span class="sxs-lookup"><span data-stu-id="5b613-141">Profile</span></span>
- <span data-ttu-id="5b613-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="5b613-142">QueryString</span></span>
- <span data-ttu-id="5b613-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="5b613-143">RouteData</span></span>
- <span data-ttu-id="5b613-144">工作階段</span><span class="sxs-lookup"><span data-stu-id="5b613-144">Session</span></span>
- <span data-ttu-id="5b613-145">UserProfile</span><span class="sxs-lookup"><span data-stu-id="5b613-145">UserProfile</span></span>
- <span data-ttu-id="5b613-146">ViewState</span><span class="sxs-lookup"><span data-stu-id="5b613-146">ViewState</span></span>

<span data-ttu-id="5b613-147">在本教學課程中，您將使用控制項的值來篩選要在 GridView 中顯示的記錄。</span><span class="sxs-lookup"><span data-stu-id="5b613-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="5b613-148">您會將**控制項**屬性新增至您稍早建立的查詢方法。</span><span class="sxs-lookup"><span data-stu-id="5b613-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="5b613-149">在[稍後](using-query-string-values-to-retrieve-data.md)的教學課程中，您會將**QueryString**屬性套用至參數，以指定參數值來自查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="5b613-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="5b613-150">首先，在 ValidationSummary 上，新增下拉式清單來篩選顯示的學生。</span><span class="sxs-lookup"><span data-stu-id="5b613-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="5b613-151">在程式碼後置檔案中，修改 select 方法以接收控制項的值，並將參數的名稱設定為提供值的控制項名稱。</span><span class="sxs-lookup"><span data-stu-id="5b613-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="5b613-152">您必須為**ModelBinding**命名空間加入**using**語句，才能解析控制項屬性。</span><span class="sxs-lookup"><span data-stu-id="5b613-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="5b613-153">下列程式碼顯示 select 方法重新運作，以根據下拉式清單的值來篩選傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="5b613-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="5b613-154">在參數之前加入控制項屬性指定此參數的值來自具有相同名稱的控制項。</span><span class="sxs-lookup"><span data-stu-id="5b613-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="5b613-155">執行 web 應用程式，並從下拉式清單中選取不同的值，以篩選學生清單。</span><span class="sxs-lookup"><span data-stu-id="5b613-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![篩選學生](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="5b613-157">結論</span><span class="sxs-lookup"><span data-stu-id="5b613-157">Conclusion</span></span>

<span data-ttu-id="5b613-158">在本教學課程中，您已啟用資料的排序和分頁。</span><span class="sxs-lookup"><span data-stu-id="5b613-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="5b613-159">您也啟用了依控制項的值來篩選資料。</span><span class="sxs-lookup"><span data-stu-id="5b613-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="5b613-160">在下一個[教學](integrating-jquery-ui.md)課程中，您將會藉由將 JQuery ui widget 整合至動態資料範本來增強 UI。</span><span class="sxs-lookup"><span data-stu-id="5b613-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5b613-161">[上一頁](updating-deleting-and-creating-data.md)
> [下一頁](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="5b613-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
