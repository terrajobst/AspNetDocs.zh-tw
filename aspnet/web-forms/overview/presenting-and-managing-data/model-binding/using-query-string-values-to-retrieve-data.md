---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 使用查詢字串值來篩選模型系結和 web form 的資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639094"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="d9d63-104">使用查詢字串值，以模型系結和 web form 來篩選資料</span><span class="sxs-lookup"><span data-stu-id="d9d63-104">Using query string values to filter data with model binding and web forms</span></span>

<span data-ttu-id="d9d63-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d9d63-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d9d63-106">本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。</span><span class="sxs-lookup"><span data-stu-id="d9d63-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="d9d63-107">模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。</span><span class="sxs-lookup"><span data-stu-id="d9d63-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="d9d63-108">此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。</span><span class="sxs-lookup"><span data-stu-id="d9d63-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="d9d63-109">本教學課程說明如何在查詢字串中傳遞值，並使用該值透過模型系結來抓取資料。</span><span class="sxs-lookup"><span data-stu-id="d9d63-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="d9d63-110">本教學課程是根據在系列的[先前](retrieving-data.md)部分中所建立的專案來建立。</span><span class="sxs-lookup"><span data-stu-id="d9d63-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="d9d63-111">您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。</span><span class="sxs-lookup"><span data-stu-id="d9d63-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="d9d63-112">可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="d9d63-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="d9d63-113">它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。</span><span class="sxs-lookup"><span data-stu-id="d9d63-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="d9d63-114">您將建立的內容</span><span class="sxs-lookup"><span data-stu-id="d9d63-114">What you'll build</span></span>

<span data-ttu-id="d9d63-115">在本教學課程中，您將會：</span><span class="sxs-lookup"><span data-stu-id="d9d63-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="d9d63-116">新增頁面以顯示學生註冊的課程</span><span class="sxs-lookup"><span data-stu-id="d9d63-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="d9d63-117">根據查詢字串中的值，抓取所選學生的已註冊課程</span><span class="sxs-lookup"><span data-stu-id="d9d63-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="d9d63-118">將具有查詢字串值的超連結從方格視圖加入至新頁面</span><span class="sxs-lookup"><span data-stu-id="d9d63-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="d9d63-119">本教學課程中的步驟與您在先前的[教學](sorting-paging-and-filtering-data.md)課程中所做的類似，是根據下拉式清單中的使用者選擇來篩選顯示的學生。</span><span class="sxs-lookup"><span data-stu-id="d9d63-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="d9d63-120">在該教學課程中，您已使用 select 方法中的**control**屬性來指定參數值來自控制項。</span><span class="sxs-lookup"><span data-stu-id="d9d63-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="d9d63-121">在本教學課程中，您將使用 select 方法中的**QueryString**屬性來指定參數值來自查詢字串。</span><span class="sxs-lookup"><span data-stu-id="d9d63-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="d9d63-122">新增用於顯示學生課程的頁面</span><span class="sxs-lookup"><span data-stu-id="d9d63-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="d9d63-123">加入新的 web 表單，以使用 [網站主要] 頁面，並將頁面命名為**課程**。</span><span class="sxs-lookup"><span data-stu-id="d9d63-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="d9d63-124">在**課程 .aspx**檔案中，新增方格視圖，以顯示所選學生的課程。</span><span class="sxs-lookup"><span data-stu-id="d9d63-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="d9d63-125">定義 select 方法</span><span class="sxs-lookup"><span data-stu-id="d9d63-125">Define the select method</span></span>

<span data-ttu-id="d9d63-126">在**Courses.aspx.cs**中，您會使用您在方格視圖的 [ **SelectMethod** ] 屬性中指定的名稱來新增 select 方法。</span><span class="sxs-lookup"><span data-stu-id="d9d63-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="d9d63-127">在該方法中，您將定義用來抓取學生課程的查詢，並指定參數來自與參數名稱相同的查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="d9d63-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="d9d63-128">首先，您必須加入下列**using**語句。</span><span class="sxs-lookup"><span data-stu-id="d9d63-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="d9d63-129">然後，將下列程式碼新增至 Courses.aspx.cs：</span><span class="sxs-lookup"><span data-stu-id="d9d63-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="d9d63-130">QueryString 屬性工作表示名為 StudentID 的查詢字串值會自動指派給這個方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="d9d63-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="d9d63-131">使用查詢字串值新增超連結</span><span class="sxs-lookup"><span data-stu-id="d9d63-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="d9d63-132">在 [student] 的方格視圖中，您將會新增連結至新課程頁面的超連結欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d63-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="d9d63-133">超連結將包含含有學生識別碼的查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="d9d63-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="d9d63-134">在 [student] 中，將下欄欄位加入至 [方格視圖] 欄中的 [總點數] 欄位正下方。</span><span class="sxs-lookup"><span data-stu-id="d9d63-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="d9d63-135">執行應用程式，並注意方格視圖現在包含 [課程] 連結。</span><span class="sxs-lookup"><span data-stu-id="d9d63-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![新增超連結](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="d9d63-137">當您按一下其中一個連結時，您會看到學生註冊的課程。</span><span class="sxs-lookup"><span data-stu-id="d9d63-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![顯示課程](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="d9d63-139">結論</span><span class="sxs-lookup"><span data-stu-id="d9d63-139">Conclusion</span></span>

<span data-ttu-id="d9d63-140">在本教學課程中，您已新增包含查詢字串值的連結。</span><span class="sxs-lookup"><span data-stu-id="d9d63-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="d9d63-141">您已在 select 方法中，使用該查詢字串值做為參數值。</span><span class="sxs-lookup"><span data-stu-id="d9d63-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="d9d63-142">在下一個[教學](adding-business-logic-layer.md)課程中，您會將程式碼後置檔案中的程式碼移至商務邏輯層和資料存取層。</span><span class="sxs-lookup"><span data-stu-id="d9d63-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d9d63-143">[上一頁](integrating-jquery-ui.md)
> [下一頁](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="d9d63-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
