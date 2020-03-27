---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 使用模型系結和 web forms 來更新、刪除和建立資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586643"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="c111a-104">使用模型系結和 web forms 來更新、刪除及建立資料</span><span class="sxs-lookup"><span data-stu-id="c111a-104">Updating, deleting, and creating data with model binding and web forms</span></span>

<span data-ttu-id="c111a-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c111a-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c111a-106">本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。</span><span class="sxs-lookup"><span data-stu-id="c111a-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="c111a-107">模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。</span><span class="sxs-lookup"><span data-stu-id="c111a-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="c111a-108">此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。</span><span class="sxs-lookup"><span data-stu-id="c111a-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="c111a-109">本教學課程說明如何使用模型系結來建立、更新和刪除資料。</span><span class="sxs-lookup"><span data-stu-id="c111a-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="c111a-110">您將設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c111a-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="c111a-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="c111a-111">DeleteMethod</span></span>
> - <span data-ttu-id="c111a-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="c111a-112">InsertMethod</span></span>
> - <span data-ttu-id="c111a-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="c111a-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="c111a-114">這些屬性會接收處理對應作業的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="c111a-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="c111a-115">在該方法中，您會提供與資料互動的邏輯。</span><span class="sxs-lookup"><span data-stu-id="c111a-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="c111a-116">本教學課程是以系列第一個[部分](retrieving-data.md)中所建立的專案為基礎。</span><span class="sxs-lookup"><span data-stu-id="c111a-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="c111a-117">您可以在或 VB 中 C# [下載](https://go.microsoft.com/fwlink/?LinkId=286116)完整專案。</span><span class="sxs-lookup"><span data-stu-id="c111a-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="c111a-118">可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="c111a-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="c111a-119">它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。</span><span class="sxs-lookup"><span data-stu-id="c111a-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="c111a-120">您將建立的內容</span><span class="sxs-lookup"><span data-stu-id="c111a-120">What you'll build</span></span>

<span data-ttu-id="c111a-121">在本教學課程中，您將會：</span><span class="sxs-lookup"><span data-stu-id="c111a-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="c111a-122">新增動態資料範本</span><span class="sxs-lookup"><span data-stu-id="c111a-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="c111a-123">啟用透過模型系結方法來更新和刪除資料</span><span class="sxs-lookup"><span data-stu-id="c111a-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="c111a-124">套用資料驗證規則-啟用在資料庫中建立新記錄</span><span class="sxs-lookup"><span data-stu-id="c111a-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="c111a-125">新增動態資料範本</span><span class="sxs-lookup"><span data-stu-id="c111a-125">Add dynamic data templates</span></span>

<span data-ttu-id="c111a-126">為了提供最佳的使用者體驗，並將程式碼重複最小化，您將使用動態資料範本。</span><span class="sxs-lookup"><span data-stu-id="c111a-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="c111a-127">您可以藉由安裝 NuGet 套件，輕鬆地將預先建立的動態資料範本整合到您現有的網站。</span><span class="sxs-lookup"><span data-stu-id="c111a-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="c111a-128">在 [**管理 NuGet 套件**] 中，安裝**DynamicDataTemplatesCS**。</span><span class="sxs-lookup"><span data-stu-id="c111a-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![動態資料範本](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="c111a-130">請注意，您的專案現在包含名為**DynamicData**的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c111a-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="c111a-131">在該資料夾中，您會找到自動套用至 web 表單中動態控制項的範本。</span><span class="sxs-lookup"><span data-stu-id="c111a-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![動態資料資料夾](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="c111a-133">啟用更新和刪除</span><span class="sxs-lookup"><span data-stu-id="c111a-133">Enable updating and deleting</span></span>

<span data-ttu-id="c111a-134">讓使用者可以更新和刪除資料庫中的記錄，與抓取資料的程式非常類似。</span><span class="sxs-lookup"><span data-stu-id="c111a-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="c111a-135">在 [ **UpdateMethod** ] 和 [ **DeleteMethod** ] 屬性中，您可以指定執行這些作業的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="c111a-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="c111a-136">有了 GridView 控制項，您也可以指定自動產生 [編輯] 和 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c111a-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="c111a-137">下列反白顯示的程式碼會顯示 GridView 程式碼的新增專案。</span><span class="sxs-lookup"><span data-stu-id="c111a-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="c111a-138">在程式碼後置檔案中，為**system.object**新增 using 語句。</span><span class="sxs-lookup"><span data-stu-id="c111a-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="c111a-139">然後，新增下列 update 和 delete 方法。</span><span class="sxs-lookup"><span data-stu-id="c111a-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="c111a-140">**TryUpdateModel**方法會將相符的資料系結值從 web 表單套用至資料項目。</span><span class="sxs-lookup"><span data-stu-id="c111a-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="c111a-141">資料項目目是根據 id 參數的值來抓取。</span><span class="sxs-lookup"><span data-stu-id="c111a-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="c111a-142">強制執行驗證需求</span><span class="sxs-lookup"><span data-stu-id="c111a-142">Enforce validation requirements</span></span>

<span data-ttu-id="c111a-143">更新資料時，會自動強制執行您套用至 Student 類別中 FirstName、LastName 和 Year 屬性的驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="c111a-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="c111a-144">DynamicField 控制項會根據驗證屬性來新增用戶端和伺服器驗證程式。</span><span class="sxs-lookup"><span data-stu-id="c111a-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="c111a-145">FirstName 和 LastName 屬性都是必要的。</span><span class="sxs-lookup"><span data-stu-id="c111a-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="c111a-146">FirstName 長度不能超過20個字元，而且 LastName 不能超過40個字元。</span><span class="sxs-lookup"><span data-stu-id="c111a-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="c111a-147">Year 必須是有效的 AcademicYear 列舉值。</span><span class="sxs-lookup"><span data-stu-id="c111a-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="c111a-148">如果使用者違反其中一項驗證需求，就不會繼續更新。</span><span class="sxs-lookup"><span data-stu-id="c111a-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="c111a-149">若要查看錯誤訊息，請在 GridView 上方加入 ValidationSummary 控制項。</span><span class="sxs-lookup"><span data-stu-id="c111a-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="c111a-150">若要顯示模型系結的驗證錯誤，請將**ShowModelStateErrors**屬性設定為**true**。</span><span class="sxs-lookup"><span data-stu-id="c111a-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="c111a-151">執行 web 應用程式，並更新和刪除任何記錄。</span><span class="sxs-lookup"><span data-stu-id="c111a-151">Run the web application, and update and delete any of the records.</span></span>

![更新資料](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="c111a-153">請注意，在編輯模式中，Year 屬性的值會自動轉譯為下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="c111a-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="c111a-154">Year 屬性是一個列舉值，而列舉值的動態資料範本會指定一個下拉式清單來進行編輯。</span><span class="sxs-lookup"><span data-stu-id="c111a-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="c111a-155">您可以藉由開啟列舉\_在**DynamicData**/**FieldTemplates**資料夾中**編輯 .ascx**檔案，找到該範本。</span><span class="sxs-lookup"><span data-stu-id="c111a-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="c111a-156">如果您提供有效的值，則更新會順利完成。</span><span class="sxs-lookup"><span data-stu-id="c111a-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="c111a-157">如果您違反其中一項驗證需求，則不會繼續更新，而且格線上方會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c111a-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![錯誤訊息](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="c111a-159">加入新記錄</span><span class="sxs-lookup"><span data-stu-id="c111a-159">Add new records</span></span>

<span data-ttu-id="c111a-160">GridView 控制項不包含**InsertMethod**屬性，因此無法用來加入具有模型系結的新記錄。</span><span class="sxs-lookup"><span data-stu-id="c111a-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="c111a-161">您可以在 [ **FormView**]、[ **DetailsView**] 或 [ **ListView** ] 控制項中找到 InsertMethod 屬性。</span><span class="sxs-lookup"><span data-stu-id="c111a-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="c111a-162">在本教學課程中，您將使用 FormView 控制項來加入新的記錄。</span><span class="sxs-lookup"><span data-stu-id="c111a-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="c111a-163">首先，將連結新增至您將建立以加入新記錄的新頁面。</span><span class="sxs-lookup"><span data-stu-id="c111a-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="c111a-164">在 ValidationSummary 上方，新增：</span><span class="sxs-lookup"><span data-stu-id="c111a-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="c111a-165">新的連結將會出現在 [學生] 頁面內容的頂端。</span><span class="sxs-lookup"><span data-stu-id="c111a-165">The new link will appear at the top of the content for the Students page.</span></span>

![新增連結](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="c111a-167">然後，使用主版頁面新增新的 web 表單，並將其命名為**AddStudent**。</span><span class="sxs-lookup"><span data-stu-id="c111a-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="c111a-168">選取 [網站] 作為主版頁面。</span><span class="sxs-lookup"><span data-stu-id="c111a-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="c111a-169">您將會使用**DynamicEntity**控制項來轉譯加入新學生的欄位。</span><span class="sxs-lookup"><span data-stu-id="c111a-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="c111a-170">DynamicEntity 控制項會在 ItemType 屬性中所指定的類別中轉譯該可編輯的屬性。</span><span class="sxs-lookup"><span data-stu-id="c111a-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="c111a-171">StudentID 屬性是以 **[ScaffoldColumn （false）]** 屬性標記，因此不會呈現。</span><span class="sxs-lookup"><span data-stu-id="c111a-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="c111a-172">在 [AddStudent] 頁面的 [MainContent] 預留位置中，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="c111a-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="c111a-173">在程式碼後置檔案（AddStudent.aspx.cs）中，為**ContosoUniversityModelBinding**命名空間加入**using**語句。</span><span class="sxs-lookup"><span data-stu-id="c111a-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="c111a-174">然後，新增下列方法，以指定如何插入新的記錄和 [取消] 按鈕的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="c111a-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="c111a-175">儲存所有變更。</span><span class="sxs-lookup"><span data-stu-id="c111a-175">Save all of the changes.</span></span>

<span data-ttu-id="c111a-176">執行 web 應用程式，並建立新的學生。</span><span class="sxs-lookup"><span data-stu-id="c111a-176">Run the web application and create a new student.</span></span>

![新增學生](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="c111a-178">按一下 [**插入**]，並注意新的 student 已建立。</span><span class="sxs-lookup"><span data-stu-id="c111a-178">Click **Insert** and notice the new student has been created.</span></span>

![顯示新 student](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="c111a-180">結論</span><span class="sxs-lookup"><span data-stu-id="c111a-180">Conclusion</span></span>

<span data-ttu-id="c111a-181">在本教學課程中，您已啟用更新、刪除及建立資料的功能。</span><span class="sxs-lookup"><span data-stu-id="c111a-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="c111a-182">當您與資料互動時，會套用驗證規則。</span><span class="sxs-lookup"><span data-stu-id="c111a-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="c111a-183">在此系列的下一個[教學](sorting-paging-and-filtering-data.md)課程中，您將啟用排序、分頁及篩選資料。</span><span class="sxs-lookup"><span data-stu-id="c111a-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c111a-184">[上一頁](retrieving-data.md)
> [下一頁](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="c111a-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
