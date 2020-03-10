---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第8部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585908"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="64d6d-104">Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第8部分</span><span class="sxs-lookup"><span data-stu-id="64d6d-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>

<span data-ttu-id="64d6d-105">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="64d6d-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="64d6d-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="64d6d-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="64d6d-107">如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程</span><span class="sxs-lookup"><span data-stu-id="64d6d-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="64d6d-108">使用動態資料功能來格式化和驗證資料</span><span class="sxs-lookup"><span data-stu-id="64d6d-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="64d6d-109">在上一個教學課程中，您已執行預存程式。</span><span class="sxs-lookup"><span data-stu-id="64d6d-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="64d6d-110">本教學課程將說明動態資料功能如何提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="64d6d-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="64d6d-111">欄位會根據其資料類型自動格式化以顯示。</span><span class="sxs-lookup"><span data-stu-id="64d6d-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="64d6d-112">欄位會根據其資料類型自動進行驗證。</span><span class="sxs-lookup"><span data-stu-id="64d6d-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="64d6d-113">您可以將中繼資料加入至資料模型，以自訂格式設定和驗證行為。</span><span class="sxs-lookup"><span data-stu-id="64d6d-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="64d6d-114">當您這麼做時，您可以只在一個位置新增格式和驗證規則，而且它們會自動套用到您使用動態資料控制項存取欄位的任何位置。</span><span class="sxs-lookup"><span data-stu-id="64d6d-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="64d6d-115">若要查看其運作方式，您要變更用來顯示和編輯現有 student *.aspx*頁面中之欄位的控制項，然後將格式和驗證中繼資料加入 `Student` 實體類型的 [名稱] 和 [日期] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="64d6d-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="64d6d-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="64d6d-117">使用 DynamicField 和 DynamicControl 控制項</span><span class="sxs-lookup"><span data-stu-id="64d6d-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="64d6d-118">開啟 [student *] 頁面，* 然後在 [`StudentsGridView`] 控制項中，以下列標記取代 [**名稱**] 和 [**註冊日期**] `TemplateField` 元素：</span><span class="sxs-lookup"><span data-stu-id="64d6d-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="64d6d-119">此標記會使用 `DynamicControl` 控制項來取代 [學生名稱] 範本欄位中的 `TextBox` 和 `Label` 控制項，並使用註冊日期的 `DynamicField` 控制項。</span><span class="sxs-lookup"><span data-stu-id="64d6d-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="64d6d-120">未指定格式字串。</span><span class="sxs-lookup"><span data-stu-id="64d6d-120">No format strings are specified.</span></span>

<span data-ttu-id="64d6d-121">將 `ValidationSummary` 控制項加入 `StudentsGridView` 控制項之後。</span><span class="sxs-lookup"><span data-stu-id="64d6d-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="64d6d-122">在 [`SearchGridView`] 控制項中，取代 [**名稱**] 和 [**註冊日期] 資料**行的標記，如同您在 `StudentsGridView` 控制項中所做的一樣，但省略 `EditItemTemplate` 元素除外。</span><span class="sxs-lookup"><span data-stu-id="64d6d-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="64d6d-123">`SearchGridView` 控制項的 `Columns` 元素現在包含下列標記：</span><span class="sxs-lookup"><span data-stu-id="64d6d-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="64d6d-124">開啟*Students.aspx.cs* ，並新增下列 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="64d6d-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="64d6d-125">為頁面的 `Init` 事件新增處理常式：</span><span class="sxs-lookup"><span data-stu-id="64d6d-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="64d6d-126">此程式碼會指定動態資料將在 `Student` 實體欄位的這些資料繫結控制項中提供格式設定和驗證。</span><span class="sxs-lookup"><span data-stu-id="64d6d-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="64d6d-127">如果您在執行頁面時收到類似下列範例的錯誤訊息，通常表示您忘了在 `Page_Init`中呼叫 `EnableDynamicData` 方法：</span><span class="sxs-lookup"><span data-stu-id="64d6d-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="64d6d-128">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="64d6d-128">Run the page.</span></span>

<span data-ttu-id="64d6d-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="64d6d-130">在 [**註冊日期] 資料**行中，時間會隨著日期顯示，因為屬性類型是 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="64d6d-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="64d6d-131">您稍後將會修正此問題。</span><span class="sxs-lookup"><span data-stu-id="64d6d-131">You'll fix that later.</span></span>

<span data-ttu-id="64d6d-132">現在請注意，動態資料會自動提供基本的資料驗證。</span><span class="sxs-lookup"><span data-stu-id="64d6d-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="64d6d-133">例如，按一下 [**編輯**]，清除 [日期] 欄位，按一下 [**更新**]，您會看到動態資料自動將此設為必要欄位，因為資料模型中的值不可為 null。</span><span class="sxs-lookup"><span data-stu-id="64d6d-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="64d6d-134">此頁面會在欄位之後顯示星號，並在 `ValidationSummary` 控制項中顯示錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="64d6d-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="64d6d-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="64d6d-136">您可能會省略 `ValidationSummary` 控制項，因為您也可以將滑鼠指標放在星號上方，以查看錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="64d6d-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="64d6d-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="64d6d-138">動態資料也會驗證在 [**註冊日期**] 欄位中輸入的資料是有效的日期：</span><span class="sxs-lookup"><span data-stu-id="64d6d-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="64d6d-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="64d6d-140">如您所見，這是一般錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64d6d-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="64d6d-141">在下一節中，您將瞭解如何自訂訊息，以及驗證和格式化規則。</span><span class="sxs-lookup"><span data-stu-id="64d6d-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="64d6d-142">將中繼資料加入至資料模型</span><span class="sxs-lookup"><span data-stu-id="64d6d-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="64d6d-143">一般來說，您會想要自訂動態資料所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="64d6d-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="64d6d-144">例如，您可能會變更資料的顯示方式，以及錯誤訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="64d6d-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="64d6d-145">您通常也會自訂資料驗證規則，以提供比動態資料根據資料類型自動提供更多功能的功能。</span><span class="sxs-lookup"><span data-stu-id="64d6d-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="64d6d-146">若要這樣做，您可以建立對應至實體類型的部分類別。</span><span class="sxs-lookup"><span data-stu-id="64d6d-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="64d6d-147">在**方案總管**中，以滑鼠右鍵按一下**ContosoUniversity**專案，選取 [**新增參考**]，然後加入 `System.ComponentModel.DataAnnotations`的參考。</span><span class="sxs-lookup"><span data-stu-id="64d6d-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="64d6d-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="64d6d-149">在*DAL*資料夾中，建立新的類別檔案，將其命名為*Student.cs*，並將其中的範本程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="64d6d-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="64d6d-150">此程式碼會建立 `Student` 實體的部分類別。</span><span class="sxs-lookup"><span data-stu-id="64d6d-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="64d6d-151">套用至這個部分類別的 `MetadataType` 屬性會識別您用來指定中繼資料的類別。</span><span class="sxs-lookup"><span data-stu-id="64d6d-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="64d6d-152">中繼資料類別可以有任何名稱，但使用機構名稱加上「中繼資料」是常見的作法。</span><span class="sxs-lookup"><span data-stu-id="64d6d-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="64d6d-153">套用至中繼資料類別中屬性的屬性會指定格式、驗證、規則和錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64d6d-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="64d6d-154">此處顯示的屬性會有下列結果：</span><span class="sxs-lookup"><span data-stu-id="64d6d-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="64d6d-155">`EnrollmentDate` 會顯示為日期（不含時間）。</span><span class="sxs-lookup"><span data-stu-id="64d6d-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="64d6d-156">這兩個名稱欄位的長度必須少於25個字元，而且提供了自訂的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64d6d-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="64d6d-157">這兩個名稱欄位都是必要項，並提供自訂錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64d6d-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="64d6d-158">再次執行 [student *.aspx* ] 頁面，您會看到現在顯示的日期沒有時間：</span><span class="sxs-lookup"><span data-stu-id="64d6d-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="64d6d-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="64d6d-160">編輯資料列，並嘗試清除 [名稱] 欄位中的值。</span><span class="sxs-lookup"><span data-stu-id="64d6d-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="64d6d-161">當您離開欄位時，表示欄位錯誤的星號會立即出現，然後再按一下 [**更新**]。</span><span class="sxs-lookup"><span data-stu-id="64d6d-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="64d6d-162">當您按一下 [**更新**] 時，頁面會顯示您指定的錯誤訊息正文。</span><span class="sxs-lookup"><span data-stu-id="64d6d-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="64d6d-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="64d6d-164">請嘗試輸入超過25個字元的名稱，按一下 [**更新**]，頁面就會顯示您指定的錯誤訊息正文。</span><span class="sxs-lookup"><span data-stu-id="64d6d-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="64d6d-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="64d6d-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="64d6d-166">既然您已在資料模型中繼資料中設定這些格式和驗證規則，這些規則會自動套用到顯示或允許變更這些欄位的每個頁面，只要您使用 `DynamicControl` 或 `DynamicField` 控制項即可。</span><span class="sxs-lookup"><span data-stu-id="64d6d-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="64d6d-167">這可減少您必須撰寫的多餘程式碼數量，讓程式設計和測試變得更容易，並確保資料格式和驗證在整個應用程式中都是一致的。</span><span class="sxs-lookup"><span data-stu-id="64d6d-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="64d6d-168">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="64d6d-168">More Information</span></span>

<span data-ttu-id="64d6d-169">這會在與 Entity Framework 消費者入門的這一系列教學課程結束。</span><span class="sxs-lookup"><span data-stu-id="64d6d-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="64d6d-170">如需可協助您瞭解如何使用 Entity Framework 的更多資源，請繼續進行[下一個 Entity Framework 教學課程系列中的第一個教學](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)課程，或造訪下列網站：</span><span class="sxs-lookup"><span data-stu-id="64d6d-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="64d6d-171">Entity Framework 常見問題</span><span class="sxs-lookup"><span data-stu-id="64d6d-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="64d6d-172">Entity Framework 小組的 Blog</span><span class="sxs-lookup"><span data-stu-id="64d6d-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="64d6d-173">MSDN Library 中的 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="64d6d-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="64d6d-174">MSDN 資料開發人員中心內的 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="64d6d-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="64d6d-175">MSDN Library 中的 EntityDataSource Web 服務器控制項總覽</span><span class="sxs-lookup"><span data-stu-id="64d6d-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="64d6d-176">MSDN Library 中的 EntityDataSource 控制項 API 參考</span><span class="sxs-lookup"><span data-stu-id="64d6d-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="64d6d-177">MSDN 上的 Entity Framework 論壇</span><span class="sxs-lookup"><span data-stu-id="64d6d-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="64d6d-178">Julie Lerman 的 blog</span><span class="sxs-lookup"><span data-stu-id="64d6d-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [<span data-ttu-id="64d6d-179">上一篇</span><span class="sxs-lookup"><span data-stu-id="64d6d-179">Previous</span></span>](the-entity-framework-and-aspnet-getting-started-part-7.md)
