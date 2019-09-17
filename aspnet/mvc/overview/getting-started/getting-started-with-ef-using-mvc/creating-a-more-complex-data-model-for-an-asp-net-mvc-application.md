---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 教學課程：為 ASP.NET MVC 應用程式建立更複雜的資料模型
author: tdykstra
description: 在本教學課程中，您將新增更多實體和關聯性，並藉由指定格式、驗證和資料庫對應規則來自訂資料模型。
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 46f7f3c9-274f-4649-811d-92222a9b27e2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 933354b09eb4674e6f523f8a65816410521f026f
ms.sourcegitcommit: aa3c2efd56466fc6bdc387ee01ad6f50a261665b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2019
ms.locfileid: "70021000"
---
# <a name="tutorial-create-a-more-complex-data-model-for-an-aspnet-mvc-app"></a><span data-ttu-id="763f8-103">教學課程：為 ASP.NET MVC 應用程式建立更複雜的資料模型</span><span class="sxs-lookup"><span data-stu-id="763f8-103">Tutorial: Create a more complex data model for an ASP.NET MVC app</span></span>

<span data-ttu-id="763f8-104">在先前的教學課程中，您使用了由三個實體組成的簡單資料模型。</span><span class="sxs-lookup"><span data-stu-id="763f8-104">In the previous tutorials you worked with a simple data model that was composed of three entities.</span></span> <span data-ttu-id="763f8-105">在本教學課程中，您會新增更多實體和關聯性，並藉由指定格式、驗證和資料庫對應規則來自訂資料模型。</span><span class="sxs-lookup"><span data-stu-id="763f8-105">In this tutorial you add more entities and relationships and you customize the data model by specifying formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="763f8-106">本文說明兩種自訂資料模型的方式：將屬性加入至實體類別，以及藉由將程式碼加入至資料庫內容類別。</span><span class="sxs-lookup"><span data-stu-id="763f8-106">This article shows two ways to customize the data model: by adding attributes to entity classes and by adding code to the database context class.</span></span>

<span data-ttu-id="763f8-107">當您完成時，實體類別會構成如下列圖例中所顯示的完整資料模型：</span><span class="sxs-lookup"><span data-stu-id="763f8-107">When you're finished, the entity classes will make up the completed data model that's shown in the following illustration:</span></span>

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="763f8-109">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="763f8-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="763f8-110">自訂資料模型</span><span class="sxs-lookup"><span data-stu-id="763f8-110">Customize the data model</span></span>
> * <span data-ttu-id="763f8-111">更新 Student 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-111">Update Student entity</span></span>
> * <span data-ttu-id="763f8-112">建立 Instructor 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-112">Create Instructor entity</span></span>
> * <span data-ttu-id="763f8-113">建立 OfficeAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-113">Create OfficeAssignment entity</span></span>
> * <span data-ttu-id="763f8-114">修改課程實體</span><span class="sxs-lookup"><span data-stu-id="763f8-114">Modify the Course entity</span></span>
> * <span data-ttu-id="763f8-115">建立 Department 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-115">Create the Department entity</span></span>
> * <span data-ttu-id="763f8-116">修改 Enrollment 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-116">Modify the Enrollment entity</span></span>
> * <span data-ttu-id="763f8-117">將程式碼加入至資料庫內容</span><span class="sxs-lookup"><span data-stu-id="763f8-117">Add code to database context</span></span>
> * <span data-ttu-id="763f8-118">將測試資料植入資料庫</span><span class="sxs-lookup"><span data-stu-id="763f8-118">Seed database with test data</span></span>
> * <span data-ttu-id="763f8-119">新增移轉</span><span class="sxs-lookup"><span data-stu-id="763f8-119">Add a migration</span></span>
> * <span data-ttu-id="763f8-120">更新資料庫</span><span class="sxs-lookup"><span data-stu-id="763f8-120">Update the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="763f8-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="763f8-121">Prerequisites</span></span>

* [<span data-ttu-id="763f8-122">Code First 遷移和部署</span><span class="sxs-lookup"><span data-stu-id="763f8-122">Code First migrations and deployment</span></span>](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-the-data-model"></a><span data-ttu-id="763f8-123">自訂資料模型</span><span class="sxs-lookup"><span data-stu-id="763f8-123">Customize the data model</span></span>

<span data-ttu-id="763f8-124">在本節中，您會了解到如何使用指定格式、驗證和資料庫對應規則的屬性來自訂資料模型。</span><span class="sxs-lookup"><span data-stu-id="763f8-124">In this section you'll see how to customize the data model by using attributes that specify formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="763f8-125">然後在下列幾節中，您將會藉由`School`將屬性新增至您已建立的類別，並為模型中的其餘實體類型建立新的類別，來建立完整的資料模型。</span><span class="sxs-lookup"><span data-stu-id="763f8-125">Then in several of the following sections you'll create the complete `School` data model by adding attributes to the classes you already created and creating new classes for the remaining entity types in the model.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="763f8-126">DataType 屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-126">The DataType Attribute</span></span>

<span data-ttu-id="763f8-127">針對學生的註冊日期，所有網頁目前都會同時顯示時間和日期，即使您針對此欄位只需要日期而已。</span><span class="sxs-lookup"><span data-stu-id="763f8-127">For student enrollment dates, all of the web pages currently display the time along with the date, although all you care about for this field is the date.</span></span> <span data-ttu-id="763f8-128">使用資料註解屬性，您可以透過僅對一個程式碼進行變更，來修正每個顯示資料的檢視上的顯示格式。</span><span class="sxs-lookup"><span data-stu-id="763f8-128">By using data annotation attributes, you can make one code change that will fix the display format in every view that shows the data.</span></span> <span data-ttu-id="763f8-129">為了查看如何進行此操作的範例，您將會新增一個屬性至 `Student` 類別中的 `EnrollmentDate` 屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-129">To see an example of how to do that, you'll add an attribute to the `EnrollmentDate` property in the `Student` class.</span></span>

<span data-ttu-id="763f8-130">在*Models\Student.cs*中，加入`using` `System.ComponentModel.DataAnnotations` `DataType` 命名空間`DisplayFormat`的語句，並將和屬性加入至屬性，如下列範例所示：`EnrollmentDate`</span><span class="sxs-lookup"><span data-stu-id="763f8-130">In *Models\Student.cs*, add a `using` statement for the `System.ComponentModel.DataAnnotations` namespace and add `DataType` and `DisplayFormat` attributes to the `EnrollmentDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,12-13)]

<span data-ttu-id="763f8-131">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性是用來指定比資料庫內建類型更特定的資料類型。</span><span class="sxs-lookup"><span data-stu-id="763f8-131">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute is used to specify a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="763f8-132">在此案例中，我們只想要追蹤日期，而非日期和時間。</span><span class="sxs-lookup"><span data-stu-id="763f8-132">In this case we only want to keep track of the date, not the date and time.</span></span> <span data-ttu-id="763f8-133">[DataType 列舉](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供許多資料類型，例如*Date、Time、PhoneNumber、Currency、EmailAddress*等等。</span><span class="sxs-lookup"><span data-stu-id="763f8-133">The [DataType Enumeration](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) provides for many data types, such as *Date, Time, PhoneNumber, Currency, EmailAddress* and more.</span></span> <span data-ttu-id="763f8-134">`DataType` 屬性也可讓應用程式自動提供類型的特定功能。</span><span class="sxs-lookup"><span data-stu-id="763f8-134">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="763f8-135">例如`mailto:` ，您可以建立[EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)的連結，並在支援[HTML5](http://html5.org/)的瀏覽器中提供[資料類型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)的日期選擇器。</span><span class="sxs-lookup"><span data-stu-id="763f8-135">For example, a `mailto:` link can be created for [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), and a date selector can be provided for [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) in browsers that support [HTML5](http://html5.org/).</span></span> <span data-ttu-id="763f8-136">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性會發出 html 5 瀏覽器可以瞭解的[資料](http://ejohn.org/blog/html-5-data-attributes/)（發音*資料虛線*）屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-136">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes emits HTML 5 [data-](http://ejohn.org/blog/html-5-data-attributes/) (pronounced *data dash*) attributes that HTML 5 browsers can understand.</span></span> <span data-ttu-id="763f8-137">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性不會提供任何驗證。</span><span class="sxs-lookup"><span data-stu-id="763f8-137">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes do not provide any validation.</span></span>

<span data-ttu-id="763f8-138">`DataType.Date` 未指定顯示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="763f8-138">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="763f8-139">根據預設，資料欄位會根據伺服器的[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)，以預設格式顯示。</span><span class="sxs-lookup"><span data-stu-id="763f8-139">By default, the data field is displayed according to the default formats based on the server's [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx).</span></span>

<span data-ttu-id="763f8-140">`DisplayFormat` 屬性用來明確指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="763f8-140">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="763f8-141">`ApplyFormatInEditMode`設定會指定在文字方塊中顯示值以供編輯時，也應該套用指定的格式。</span><span class="sxs-lookup"><span data-stu-id="763f8-141">The `ApplyFormatInEditMode` setting specifies that the specified formatting should also be applied when the value is displayed in a text box for editing.</span></span> <span data-ttu-id="763f8-142">（您可能不想針對某些欄位（例如，貨幣值），您可能不希望文字方塊中的貨幣符號進行編輯。）</span><span class="sxs-lookup"><span data-stu-id="763f8-142">(You might not want that for some fields — for example, for currency values, you might not want the currency symbol in the text box for editing.)</span></span>

<span data-ttu-id="763f8-143">您可以單獨使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性，但是使用[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性也是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="763f8-143">You can use the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute by itself, but it's generally a good idea to use the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute also.</span></span> <span data-ttu-id="763f8-144">屬性會傳達資料的*語義*，而不`DisplayFormat`是如何在螢幕上呈現，而且提供下列優點： `DataType`</span><span class="sxs-lookup"><span data-stu-id="763f8-144">The `DataType` attribute conveys the *semantics* of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with `DisplayFormat`:</span></span>

- <span data-ttu-id="763f8-145">瀏覽器可以啟用 HTML5 功能 (例如顯示日曆控制項、適合地區設定的貨幣符號、電子郵件連結、一些用戶端輸入驗證等等)。</span><span class="sxs-lookup"><span data-stu-id="763f8-145">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, some client-side input validation, etc.).</span></span>
- <span data-ttu-id="763f8-146">根據預設，瀏覽器會使用以您的[地區](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)設定為基礎的正確格式來呈現資料。</span><span class="sxs-lookup"><span data-stu-id="763f8-146">By default, the browser will render data using the correct format based on your [locale](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).</span></span>
- <span data-ttu-id="763f8-147">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性可以讓 MVC 選擇正確的欄位範本來呈現資料（ [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)會使用字串範本）。</span><span class="sxs-lookup"><span data-stu-id="763f8-147">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute can enable MVC to choose the right field template to render the data (the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) uses the string template).</span></span> <span data-ttu-id="763f8-148">如需詳細資訊，請參閱 Brad Wilson 的[ASP.NET MVC 2 範本](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="763f8-148">For more information, see Brad Wilson's [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="763f8-149">（雖然是針對 MVC 2 而撰寫的，但本文仍適用于目前版本的 ASP.NET MVC）。</span><span class="sxs-lookup"><span data-stu-id="763f8-149">(Though written for MVC 2, this article still applies to the current version of ASP.NET MVC.)</span></span>

<span data-ttu-id="763f8-150">如果您使用`DataType`屬性搭配日期欄位，您也必須`DisplayFormat`指定屬性，才能確保欄位在 Chrome 瀏覽器中正確呈現。</span><span class="sxs-lookup"><span data-stu-id="763f8-150">If you use the `DataType` attribute with a date field, you have to specify the `DisplayFormat` attribute also in order to ensure that the field renders correctly in Chrome browsers.</span></span> <span data-ttu-id="763f8-151">如需詳細資訊，請參閱[這個 StackOverflow 執行緒](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。</span><span class="sxs-lookup"><span data-stu-id="763f8-151">For more information, see [this StackOverflow thread](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).</span></span>

<span data-ttu-id="763f8-152">如需如何在 mvc 中處理其他日期格式的詳細資訊，請[移至 mvc 5 簡介：檢查 [編輯方法] 和 [](../introduction/examining-the-edit-methods-and-edit-view.md)編輯檢視]，並在&quot;頁面&quot;中搜尋國際化。</span><span class="sxs-lookup"><span data-stu-id="763f8-152">For more information about how to handle other date formats in MVC, go to [MVC 5 Introduction: Examining the Edit Methods and Edit View](../introduction/examining-the-edit-methods-and-edit-view.md) and search in the page for &quot;internationalization&quot;.</span></span>

<span data-ttu-id="763f8-153">再次執行 [學生索引] 頁面，並注意註冊日期不會再顯示時間。</span><span class="sxs-lookup"><span data-stu-id="763f8-153">Run the Student Index page again and notice that times are no longer displayed for the enrollment dates.</span></span> <span data-ttu-id="763f8-154">使用`Student`模型的任何視圖也會有相同的情況。</span><span class="sxs-lookup"><span data-stu-id="763f8-154">The same will be true for any view that uses the `Student` model.</span></span>

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a><span data-ttu-id="763f8-156">StringLengthAttribute</span><span class="sxs-lookup"><span data-stu-id="763f8-156">The StringLengthAttribute</span></span>

<span data-ttu-id="763f8-157">您也可以使用屬性指定資料驗證規則和驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="763f8-157">You can also specify data validation rules and validation error messages using attributes.</span></span> <span data-ttu-id="763f8-158">[StringLength 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)會設定資料庫中的最大長度，並為 ASP.NET MVC 提供用戶端和伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="763f8-158">The [StringLength attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) sets the maximum length in the database and provides client side and server side validation for ASP.NET MVC.</span></span> <span data-ttu-id="763f8-159">您也可以在此屬性中指定最小字串長度，但最小值不會對資料庫結構描述造成任何影響。</span><span class="sxs-lookup"><span data-stu-id="763f8-159">You can also specify the minimum string length in this attribute, but the minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="763f8-160">假設您想要確保使用者不會在名稱中輸入超過 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="763f8-160">Suppose you want to ensure that users don't enter more than 50 characters for a name.</span></span> <span data-ttu-id="763f8-161">若要新增這項限制 ，請將 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) `LastName`屬性`FirstMidName`新增至和屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="763f8-161">To add this limitation, add [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attributes to the `LastName` and `FirstMidName` properties, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

<span data-ttu-id="763f8-162">[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性不會防止使用者在名稱中輸入空白字元。</span><span class="sxs-lookup"><span data-stu-id="763f8-162">The [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute won't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="763f8-163">您可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)屬性，將限制套用至輸入。</span><span class="sxs-lookup"><span data-stu-id="763f8-163">You can use the [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) attribute to apply restrictions to the input.</span></span> <span data-ttu-id="763f8-164">例如，下列程式碼要求第一個字元必須是大寫，其餘字元則以字母順序排列：</span><span class="sxs-lookup"><span data-stu-id="763f8-164">For example the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

<span data-ttu-id="763f8-165">[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)屬性提供與[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性類似的功能，但不提供用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="763f8-165">The [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) attribute provides similar functionality to the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute but doesn't provide client side validation.</span></span>

<span data-ttu-id="763f8-166">執行應用程式，然後按一下 [**學生**] 索引標籤。您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="763f8-166">Run the application and click the **Students** tab. You get the following error:</span></span>

<span data-ttu-id="763f8-167">*在建立資料庫之後，支援 ' SchoolCoNtext ' 內容的模型已經變更。請考慮使用 Code First 移轉來更新資料庫（[https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)）。*</span><span class="sxs-lookup"><span data-stu-id="763f8-167">*The model backing the 'SchoolContext' context has changed since the database was created. Consider using Code First Migrations to update the database ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*</span></span>

<span data-ttu-id="763f8-168">資料庫模型已經變更，而這種方式需要變更資料庫架構，而且 Entity Framework 偵測到這種情況。</span><span class="sxs-lookup"><span data-stu-id="763f8-168">The database model has changed in a way that requires a change in the database schema, and Entity Framework detected that.</span></span> <span data-ttu-id="763f8-169">您將使用「遷移」來更新架構，而不會遺失您使用 UI 新增至資料庫的任何資料。</span><span class="sxs-lookup"><span data-stu-id="763f8-169">You'll use migrations to update the schema without losing any data that you added to the database by using the UI.</span></span> <span data-ttu-id="763f8-170">如果您變更`Seed`方法所建立的資料，因為您在`Seed`方法中使用的[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)方法，所以會變更回其原始狀態。</span><span class="sxs-lookup"><span data-stu-id="763f8-170">If you changed data that was created by the `Seed` method, that will be changed back to its original state because of the [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) method that you're using in the `Seed` method.</span></span> <span data-ttu-id="763f8-171">（[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)相當於來自資料庫術語的「upsert」作業。）</span><span class="sxs-lookup"><span data-stu-id="763f8-171">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) is equivalent to an "upsert" operation from database terminology.)</span></span>

<span data-ttu-id="763f8-172">請在套件管理員主控台 (PMC) 中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="763f8-172">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

<span data-ttu-id="763f8-173">`add-migration`命令會建立名為的檔案 *&lt;時間戳記&gt;\_MaxLengthOnNames.cs* 。</span><span class="sxs-lookup"><span data-stu-id="763f8-173">The `add-migration` command creates a file named *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*.</span></span> <span data-ttu-id="763f8-174">此檔案包含了 `Up` 方法中的程式碼，可更新資料庫，使其符合目前的資料模型。</span><span class="sxs-lookup"><span data-stu-id="763f8-174">This file contains code in the `Up` method that will update the database to match the current data model.</span></span> <span data-ttu-id="763f8-175">`update-database` 命令執行了該程式碼。</span><span class="sxs-lookup"><span data-stu-id="763f8-175">The `update-database` command ran that code.</span></span>

<span data-ttu-id="763f8-176">Entity Framework 會使用遷移檔案名前面加上的時間戳記來排序遷移。</span><span class="sxs-lookup"><span data-stu-id="763f8-176">The timestamp prepended to the migrations file name is used by Entity Framework to order the migrations.</span></span> <span data-ttu-id="763f8-177">執行`update-database`命令之前，您可以建立多個遷移，然後依照建立的順序套用所有的遷移。</span><span class="sxs-lookup"><span data-stu-id="763f8-177">You can create multiple migrations before running the `update-database` command, and then all of the migrations are applied in the order in which they were created.</span></span>

<span data-ttu-id="763f8-178">執行 [**建立**] 頁面，並輸入長度超過50個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="763f8-178">Run the **Create** page, and enter either name longer than 50 characters.</span></span> <span data-ttu-id="763f8-179">當您按一下 [**建立**] 時，用戶端驗證會顯示錯誤訊息：*欄位 LastName 必須是最大長度為50的字串。*</span><span class="sxs-lookup"><span data-stu-id="763f8-179">When you click **Create**, client side validation shows an error message: *The field LastName must be a string with a maximum length of 50.*</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="763f8-180">Column 屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-180">The Column Attribute</span></span>

<span data-ttu-id="763f8-181">您也可以使用屬性控制您的類別和屬性對應到資料庫的方式。</span><span class="sxs-lookup"><span data-stu-id="763f8-181">You can also use attributes to control how your classes and properties are mapped to the database.</span></span> <span data-ttu-id="763f8-182">假設您已針對名字欄位使用 `FirstMidName` 作為名稱，因為欄位中可能也會包含中間名。</span><span class="sxs-lookup"><span data-stu-id="763f8-182">Suppose you had used the name `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span> <span data-ttu-id="763f8-183">但您想要將資料庫資料行命名為 `FirstName`，因為撰寫臨機操作查詢資料庫的使用者比較習慣該名稱。</span><span class="sxs-lookup"><span data-stu-id="763f8-183">But you want the database column to be named `FirstName`, because users who will be writing ad-hoc queries against the database are accustomed to that name.</span></span> <span data-ttu-id="763f8-184">若要進行此對應，您可以使用 `Column` 屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-184">To make this mapping, you can use the `Column` attribute.</span></span>

<span data-ttu-id="763f8-185">`Column` 屬性指定當建立資料庫時，`Student` 資料表中對應到 `FirstMidName` 屬性的資料行會命名為 `FirstName`。</span><span class="sxs-lookup"><span data-stu-id="763f8-185">The `Column` attribute specifies that when the database is created, the column of the `Student` table that maps to the `FirstMidName` property will be named `FirstName`.</span></span> <span data-ttu-id="763f8-186">換句話說，當您的程式碼參照 `Student.FirstMidName` 時，資料便會來自 `Student` 資料表中的 `FirstName` 資料行或在其中更新。</span><span class="sxs-lookup"><span data-stu-id="763f8-186">In other words, when your code refers to `Student.FirstMidName`, the data will come from or be updated in the `FirstName` column of the `Student` table.</span></span> <span data-ttu-id="763f8-187">如果您未指定資料行名稱，則會提供與屬性名稱相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="763f8-187">If you don't specify column names, they are given the same name as the property name.</span></span>

<span data-ttu-id="763f8-188">在*Student.cs*檔案中，新增`using` [system.workflow.componentmodel.activity](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx)的語句，並將`FirstMidName` [資料行名稱] 屬性加入至屬性，如下列反白顯示的程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="763f8-188">In the *Student.cs* file, add a `using` statement for [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) and add the column name attribute to the `FirstMidName` property, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

<span data-ttu-id="763f8-189">加入資料[行屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)會變更支援 SchoolCoNtext 的模型，因此它不會符合資料庫。</span><span class="sxs-lookup"><span data-stu-id="763f8-189">The addition of the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) changes the model backing the SchoolContext, so it won't match the database.</span></span> <span data-ttu-id="763f8-190">在 PMC 中輸入下列命令，以建立另一個遷移：</span><span class="sxs-lookup"><span data-stu-id="763f8-190">Enter the following commands in the PMC to create another migration:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

<span data-ttu-id="763f8-191">在**伺服器總管**中，按兩下 [ *student* ] 資料表來開啟*student*資料表設計工具。</span><span class="sxs-lookup"><span data-stu-id="763f8-191">In **Server Explorer**, open the *Student* table designer by double-clicking the *Student* table.</span></span>

<span data-ttu-id="763f8-192">下圖顯示在您套用前兩個遷移之前的原始資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="763f8-192">The following image shows the original column name as it was before you applied the first two migrations.</span></span> <span data-ttu-id="763f8-193">除了從`FirstMidName`變更為`FirstName`的資料行名稱以外，這兩個名稱資料行的`MAX`長度已從 length 變更為50個字元。</span><span class="sxs-lookup"><span data-stu-id="763f8-193">In addition to the column name changing from `FirstMidName` to `FirstName`, the two name columns have changed from `MAX` length to 50 characters.</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="763f8-194">您也可以使用[流暢的 API](https://msdn.microsoft.com/data/jj591617)來進行資料庫對應變更，如您稍後在本教學課程中所見。</span><span class="sxs-lookup"><span data-stu-id="763f8-194">You can also make database mapping changes using the [Fluent API](https://msdn.microsoft.com/data/jj591617), as you'll see later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="763f8-195">若您嘗試在完成建立下列章節中所有的實體類別前進行編譯，您可能會收到編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="763f8-195">If you try to compile before you finish creating all of the entity classes in the following sections, you might get compiler errors.</span></span>

## <a name="update-student-entity"></a><span data-ttu-id="763f8-196">更新 Student 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-196">Update Student entity</span></span>

<span data-ttu-id="763f8-197">在*Models\Student.cs*中，將您先前新增的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="763f8-197">In *Models\Student.cs*, replace the code you added earlier with the following code.</span></span> <span data-ttu-id="763f8-198">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="763f8-198">The changes are highlighted.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=11,13,15,18,22,25-32)]

### <a name="the-required-attribute"></a><span data-ttu-id="763f8-199">必要的屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-199">The Required Attribute</span></span>

<span data-ttu-id="763f8-200">[Required 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)會使 name 屬性成為必要欄位。</span><span class="sxs-lookup"><span data-stu-id="763f8-200">The [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) makes the name properties required fields.</span></span> <span data-ttu-id="763f8-201">`Required attribute`數值型別（例如 DateTime、int、double 和 float）不需要。</span><span class="sxs-lookup"><span data-stu-id="763f8-201">The `Required attribute` is not needed for value types such as DateTime, int, double, and float.</span></span> <span data-ttu-id="763f8-202">實值型別無法指派 null 值，因此它們原本就視為必要欄位。</span><span class="sxs-lookup"><span data-stu-id="763f8-202">Value types cannot be assigned a null value, so they are inherently treated as required fields.</span></span> 

<span data-ttu-id="763f8-203">`Required` 屬性必須搭配 `MinimumLength` 使用，才能強制執行 `MinimumLength`。</span><span class="sxs-lookup"><span data-stu-id="763f8-203">The `Required` attribute must be used with `MinimumLength` for the `MinimumLength` to be enforced.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs?highlight=2)]

<span data-ttu-id="763f8-204">`MinimumLength` 與 `Required` 允許空白字元以滿足驗證。</span><span class="sxs-lookup"><span data-stu-id="763f8-204">`MinimumLength` and `Required` allow whitespace to satisfy the validation.</span></span> <span data-ttu-id="763f8-205">在字串上使用屬性進行完整控制。`RegularExpression`</span><span class="sxs-lookup"><span data-stu-id="763f8-205">Use the `RegularExpression` attribute for full controll over the string.</span></span>

### <a name="the-display-attribute"></a><span data-ttu-id="763f8-206">Display 屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-206">The Display Attribute</span></span>

<span data-ttu-id="763f8-207">`Display` 屬性指定了文字方塊的標題應為「名字」、「姓氏」、「全名」及「註冊日期」，而非每個執行個體中的屬性名稱 (沒有使用空格鍵分隔單字的名稱)。</span><span class="sxs-lookup"><span data-stu-id="763f8-207">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date" instead of the property name in each instance (which has no space dividing the words).</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="763f8-208">FullName 計算屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-208">The FullName Calculated Property</span></span>

<span data-ttu-id="763f8-209">`FullName` 為一個計算屬性，會傳回藉由串連兩個其他屬性而建立的值。</span><span class="sxs-lookup"><span data-stu-id="763f8-209">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="763f8-210">因此，它只有一個`get`存取子，而且`FullName`資料庫中不會產生任何資料行。</span><span class="sxs-lookup"><span data-stu-id="763f8-210">Therefore it has only a `get` accessor, and no `FullName` column will be generated in the database.</span></span>

## <a name="create-instructor-entity"></a><span data-ttu-id="763f8-211">建立 Instructor 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-211">Create Instructor entity</span></span>

<span data-ttu-id="763f8-212">建立*Models\Instructor.cs*，以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="763f8-212">Create *Models\Instructor.cs*, replacing the template code with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="763f8-213">請注意，當中有幾個屬性跟 `Student` 和 `Instructor` 實體中的一樣。</span><span class="sxs-lookup"><span data-stu-id="763f8-213">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="763f8-214">在本系列稍後的[實作繼承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中，您會對此程式碼進行重構以消除冗餘。</span><span class="sxs-lookup"><span data-stu-id="763f8-214">In the [Implementing Inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series, you'll refactor this code to eliminate the redundancy.</span></span>

<span data-ttu-id="763f8-215">您可以將多個屬性放在同一行，因此您也可以撰寫講師類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="763f8-215">You can put multiple attributes on one line, so you could also write the instructor class as follows:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a><span data-ttu-id="763f8-216">課程和 OfficeAssignment 導覽屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-216">The Courses and OfficeAssignment Navigation Properties</span></span>

<span data-ttu-id="763f8-217">`Courses` 和 `OfficeAssignment` 屬性為導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-217">The `Courses` and `OfficeAssignment` properties are navigation properties.</span></span> <span data-ttu-id="763f8-218">如先前所述，它們通常會定義為[虛擬](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx)，使其能夠利用稱為消極式[載入](https://msdn.microsoft.com/magazine/hh205756.aspx)的 Entity Framework 功能。</span><span class="sxs-lookup"><span data-stu-id="763f8-218">As was explained earlier, they are typically defined as [virtual](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) so that they can take advantage of an Entity Framework feature called [lazy loading](https://msdn.microsoft.com/magazine/hh205756.aspx).</span></span> <span data-ttu-id="763f8-219">此外，如果導覽屬性可以保存多個實體，其型別必須執行[ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx)介面。</span><span class="sxs-lookup"><span data-stu-id="763f8-219">In addition, if a navigation property can hold multiple entities, its type must implement the [ICollection&lt;T&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) Interface.</span></span> <span data-ttu-id="763f8-220">例如， [IList&lt;t&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx)合格但不[符合&lt;IEnumerable&gt; t](https://msdn.microsoft.com/library/9eekhta0.aspx) ，因為`IEnumerable<T>`不會執行[Add](https://msdn.microsoft.com/library/63ywd54z.aspx)。</span><span class="sxs-lookup"><span data-stu-id="763f8-220">For example [IList&lt;T&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) qualifies but not [IEnumerable&lt;T&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) because `IEnumerable<T>` doesn't implement [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).</span></span>

<span data-ttu-id="763f8-221">講師可以教授任何數量的課程，因此`Courses`定義為`Course`實體的集合。</span><span class="sxs-lookup"><span data-stu-id="763f8-221">An instructor can teach any number of courses, so `Courses` is defined as a collection of `Course` entities.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="763f8-222">我們的商務規則狀態講師最多隻能有一個辦公室，因此`OfficeAssignment`定義為單一`OfficeAssignment`實體（如果未指派任何辦公室， `null`則可能為）。</span><span class="sxs-lookup"><span data-stu-id="763f8-222">Our business rules state an instructor can only have at most one office, so `OfficeAssignment` is defined as a single `OfficeAssignment` entity (which may be `null` if no office is assigned).</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-officeassignment-entity"></a><span data-ttu-id="763f8-223">建立 OfficeAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-223">Create OfficeAssignment entity</span></span>

<span data-ttu-id="763f8-224">使用下列程式碼建立*Models\OfficeAssignment.cs* ：</span><span class="sxs-lookup"><span data-stu-id="763f8-224">Create *Models\OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="763f8-225">建立專案，這會儲存您的變更，並確認您尚未進行編譯器可以攔截的任何複製和貼上錯誤。</span><span class="sxs-lookup"><span data-stu-id="763f8-225">Build the project, which saves your changes and verifies you haven't made any copy and paste errors the compiler can catch.</span></span>

### <a name="the-key-attribute"></a><span data-ttu-id="763f8-226">索引鍵屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-226">The Key Attribute</span></span>

<span data-ttu-id="763f8-227">`Instructor`和實體之間有一對零或一關聯性。`OfficeAssignment`</span><span class="sxs-lookup"><span data-stu-id="763f8-227">There's a one-to-zero-or-one relationship between the `Instructor` and the `OfficeAssignment` entities.</span></span> <span data-ttu-id="763f8-228">辦公室指派只存在於指派給的講師，因此其主要索引鍵也是其對`Instructor`實體的外鍵。</span><span class="sxs-lookup"><span data-stu-id="763f8-228">An office assignment only exists in relation to the instructor it's assigned to, and therefore its primary key is also its foreign key to the `Instructor` entity.</span></span> <span data-ttu-id="763f8-229">但是`InstructorID` Entity Framework 無法自動辨識為此實體的主要金鑰，因為它的名稱不`ID`符合或*classname* `ID`命名慣例。</span><span class="sxs-lookup"><span data-stu-id="763f8-229">But the Entity Framework can't automatically recognize `InstructorID` as the primary key of this entity because its name doesn't follow the `ID` or *classname* `ID` naming convention.</span></span> <span data-ttu-id="763f8-230">因此，必須使用 `Key` 屬性將其識別為 PK：</span><span class="sxs-lookup"><span data-stu-id="763f8-230">Therefore, the `Key` attribute is used to identify it as the key:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="763f8-231">如果實體有自己的`Key`主鍵，但是您想要將屬性命名為不同于`classnameID`或`ID`，您也可以使用屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-231">You can also use the `Key` attribute if the entity does have its own primary key but you want to name the property something different than `classnameID` or `ID`.</span></span> <span data-ttu-id="763f8-232">根據預設，EF 會將金鑰視為非資料庫產生的，因為資料行是用於識別關聯性。</span><span class="sxs-lookup"><span data-stu-id="763f8-232">By default EF treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-foreignkey-attribute"></a><span data-ttu-id="763f8-233">ForeignKey 屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-233">The ForeignKey Attribute</span></span>

<span data-ttu-id="763f8-234">當兩個實體之間有一對一或一對一的關聯性或一對一關聯性時（例如介於和`OfficeAssignment` `Instructor`之間），EF 無法解決關聯性的哪一端是主體，以及哪個 end 相依。</span><span class="sxs-lookup"><span data-stu-id="763f8-234">When there is a one-to-zero-or-one relationship or a one-to-one relationship between two entities (such as between `OfficeAssignment` and `Instructor`), EF can't work out which end of the relationship is the principal and which end is dependent.</span></span> <span data-ttu-id="763f8-235">一對一關聯性在每個類別中都有一個參考導覽屬性，指向另一個類別。</span><span class="sxs-lookup"><span data-stu-id="763f8-235">One-to-one relationships have a reference navigation property in each class to the other class.</span></span> <span data-ttu-id="763f8-236">[ForeignKey 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可以套用至相依類別，以建立關聯性。</span><span class="sxs-lookup"><span data-stu-id="763f8-236">The [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) can be applied to the dependent class to establish the relationship.</span></span> <span data-ttu-id="763f8-237">如果您省略[ForeignKey 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)，當您嘗試建立遷移時，會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="763f8-237">If you omit the [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), you get the following error when you try to create the migration:</span></span>

<span data-ttu-id="763f8-238">*無法判斷類型 ' ContosoUniversity. OfficeAssignment ' 與 ' ContosoUniversity ' 之間關聯的主體端點。此關聯的主要端點必須使用關聯性 Fluent API 或資料批註來明確設定。*</span><span class="sxs-lookup"><span data-stu-id="763f8-238">*Unable to determine the principal end of an association between the types 'ContosoUniversity.Models.OfficeAssignment' and 'ContosoUniversity.Models.Instructor'. The principal end of this association must be explicitly configured using either the relationship fluent API or data annotations.*</span></span>

<span data-ttu-id="763f8-239">稍後在本教學課程中，您將瞭解如何使用 Fluent API 來設定此關聯性。</span><span class="sxs-lookup"><span data-stu-id="763f8-239">Later in the tutorial you'll see how to configure this relationship with the fluent API.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="763f8-240">講師導覽屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-240">The Instructor Navigation Property</span></span>

<span data-ttu-id="763f8-241">實體有可為 null `OfficeAssignment`的導覽屬性（因為講師可能沒有 office 指派），而且該`OfficeAssignment`實體具有不可為 null `Instructor`的導覽屬性（因為辦公室指派無法`Instructor`不具有講師的存在- `InstructorID` -不可為 null）。</span><span class="sxs-lookup"><span data-stu-id="763f8-241">The `Instructor` entity has a nullable `OfficeAssignment` navigation property (because an instructor might not have an office assignment), and the `OfficeAssignment` entity has a non-nullable `Instructor` navigation property (because an office assignment can't exist without an instructor -- `InstructorID` is non-nullable).</span></span> <span data-ttu-id="763f8-242">當實體具有相關`OfficeAssignment`實體時，每個實體都會參考其導覽屬性中的另一個實體。 `Instructor`</span><span class="sxs-lookup"><span data-stu-id="763f8-242">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity will have a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="763f8-243">您可以將`[Required]`屬性放在講師導覽屬性上，以指定必須有相關的講師，但您不需要這麼做，因為 InstructorID 外鍵（也是此資料表的索引鍵）不可為 null。</span><span class="sxs-lookup"><span data-stu-id="763f8-243">You could put a `[Required]` attribute on the Instructor navigation property to specify that there must be a related instructor, but you don't have to do that because the InstructorID foreign key (which is also the key to this table) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="763f8-244">修改課程實體</span><span class="sxs-lookup"><span data-stu-id="763f8-244">Modify the Course entity</span></span>

<span data-ttu-id="763f8-245">在*Models\Course.cs*中，將您先前新增的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="763f8-245">In *Models\Course.cs*, replace the code you added earlier with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="763f8-246">課程實體有一個外鍵屬性`DepartmentID` ，它指向相關`Department`實體，而且它有一個`Department`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-246">The course entity has a foreign key property `DepartmentID` which points to the related `Department` entity and it has a `Department` navigation property.</span></span> <span data-ttu-id="763f8-247">當您針對相關實體具有一個導覽屬性時，Entity Framework 便不需要您為資料模型新增一個外部索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-247">The Entity Framework doesn't require you to add a foreign key property to your data model when you have a navigation property for a related entity.</span></span> <span data-ttu-id="763f8-248">EF 會在需要的任何地方，自動在資料庫中建立外鍵。</span><span class="sxs-lookup"><span data-stu-id="763f8-248">EF automatically creates foreign keys in the database wherever they are needed.</span></span> <span data-ttu-id="763f8-249">但在資料模型中擁有外部索引鍵，可讓更新變得更為簡單和有效率。</span><span class="sxs-lookup"><span data-stu-id="763f8-249">But having the foreign key in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="763f8-250">例如，當您提取要編輯`Department`的課程實體時，如果您未載入，實體就會是 null，因此當您更新課程實體時，您必須先`Department`提取實體。</span><span class="sxs-lookup"><span data-stu-id="763f8-250">For example, when you fetch a course entity to edit, the `Department` entity is null if you don't load it, so when you update the course entity, you would have to first fetch the `Department` entity.</span></span> <span data-ttu-id="763f8-251">當外鍵屬性`DepartmentID`包含在資料模型中時，您不需要先`Department`提取實體，就可以更新。</span><span class="sxs-lookup"><span data-stu-id="763f8-251">When the foreign key property `DepartmentID` is included in the data model, you don't need to fetch the `Department` entity before you update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="763f8-252">DatabaseGenerated 屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-252">The DatabaseGenerated Attribute</span></span>

<span data-ttu-id="763f8-253">`CourseID`屬性上具有[None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)參數的[DatabaseGenerated 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx)會指定使用者提供的主鍵值，而不是由資料庫所產生的值。</span><span class="sxs-lookup"><span data-stu-id="763f8-253">The [DatabaseGenerated attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) with the [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parameter on the `CourseID` property specifies that primary key values are provided by the user rather than generated by the database.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="763f8-254">根據預設，Entity Framework 會假設主要金鑰值是由資料庫產生。</span><span class="sxs-lookup"><span data-stu-id="763f8-254">By default, the Entity Framework assumes that primary key values are generated by the database.</span></span> <span data-ttu-id="763f8-255">這是您在大多數案例下所希望的情況。</span><span class="sxs-lookup"><span data-stu-id="763f8-255">That's what you want in most scenarios.</span></span> <span data-ttu-id="763f8-256">不過，針對`Course`實體，您將使用使用者指定的課程編號，例如一個部門的1000系列、另一個部門的2000系列等等。</span><span class="sxs-lookup"><span data-stu-id="763f8-256">However, for `Course` entities, you'll use a user-specified course number such as a 1000 series for one department, a 2000 series for another department, and so on.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="763f8-257">外鍵和導覽屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-257">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="763f8-258">`Course`實體中的外鍵屬性和導覽屬性會反映下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="763f8-258">The foreign key properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

- <span data-ttu-id="763f8-259">課程會指派給一個部門，因此基於上述理由，會有一個 `DepartmentID` 外部索引鍵和一個 `Department` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="763f8-259">A course is assigned to one department, so there's a `DepartmentID` foreign key and a `Department` navigation property for the reasons mentioned above.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- <span data-ttu-id="763f8-260">由於課程可由任何數量的學生進行註冊，因此 `Enrollments` 導覽屬性為一個集合：</span><span class="sxs-lookup"><span data-stu-id="763f8-260">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- <span data-ttu-id="763f8-261">課程可由多個講師進行教授，因此 `Instructors` 導覽屬性為一個集合：</span><span class="sxs-lookup"><span data-stu-id="763f8-261">A course may be taught by multiple instructors, so the `Instructors` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="create-the-department-entity"></a><span data-ttu-id="763f8-262">建立 Department 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-262">Create the Department entity</span></span>

<span data-ttu-id="763f8-263">使用下列程式碼建立*Models\Department.cs* ：</span><span class="sxs-lookup"><span data-stu-id="763f8-263">Create *Models\Department.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a><span data-ttu-id="763f8-264">Column 屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-264">The Column Attribute</span></span>

<span data-ttu-id="763f8-265">先前您已使用[column 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)來變更資料行名稱對應。</span><span class="sxs-lookup"><span data-stu-id="763f8-265">Earlier you used the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) to change column name mapping.</span></span> <span data-ttu-id="763f8-266">在`Department`實體的程式碼中`Column` ，會使用屬性來變更 SQL 資料類型對應，以便在資料庫中使用 SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx)類型來定義資料行：</span><span class="sxs-lookup"><span data-stu-id="763f8-266">In the code for the `Department` entity, the `Column` attribute is being used to change SQL data type mapping so that the column will be defined using the SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) type in the database:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="763f8-267">通常不需要資料行對應，因為 Entity Framework 通常會根據您為屬性定義的 CLR 類型來選擇適當的 SQL Server 資料類型。</span><span class="sxs-lookup"><span data-stu-id="763f8-267">Column mapping is generally not required, because the Entity Framework usually chooses the appropriate SQL Server data type based on the CLR type that you define for the property.</span></span> <span data-ttu-id="763f8-268">CLR `decimal` 類型會對應到 SQL Server 的 `decimal` 類型。</span><span class="sxs-lookup"><span data-stu-id="763f8-268">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="763f8-269">但是在這種情況下，您知道資料行將會保留貨幣金額，而[money](https://msdn.microsoft.com/library/ms179882.aspx)資料類型則更適合這麼做。</span><span class="sxs-lookup"><span data-stu-id="763f8-269">But in this case you know that the column will be holding currency amounts, and the [money](https://msdn.microsoft.com/library/ms179882.aspx) data type is more appropriate for that.</span></span> <span data-ttu-id="763f8-270">如需 CLR 資料類型以及它們如何符合 SQL Server 資料類型的詳細資訊，請參閱[Entity FrameworkTypes 的 SqlClient](https://msdn.microsoft.com/library/bb896344.aspx)。</span><span class="sxs-lookup"><span data-stu-id="763f8-270">For more information about CLR data types and how they match to SQL Server data types, see [SqlClient for Entity FrameworkTypes](https://msdn.microsoft.com/library/bb896344.aspx).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="763f8-271">外鍵和導覽屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-271">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="763f8-272">外部索引鍵及導覽屬性反映了下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="763f8-272">The foreign key and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="763f8-273">部門可以有或沒有一位系統管理員，而系統管理員一律為講師。</span><span class="sxs-lookup"><span data-stu-id="763f8-273">A department may or may not have an administrator, and an administrator is always an instructor.</span></span> <span data-ttu-id="763f8-274">因此，會將`Instructor` `int`屬性當做實體的外鍵包含，並在型別指定之後加入問號，將屬性標示為可為 null。 `InstructorID`導覽屬性會命名`Administrator`為，但會`Instructor`保留實體：</span><span class="sxs-lookup"><span data-stu-id="763f8-274">Therefore the `InstructorID` property is included as the foreign key to the `Instructor` entity, and a question mark is added after the `int` type designation to mark the property as nullable.The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- <span data-ttu-id="763f8-275">一個部門可能有許多課程，因此有一個`Courses`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="763f8-275">A department may have many courses, so there's a `Courses` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > <span data-ttu-id="763f8-276">根據慣例，Entity Framework 會為不可為 Null 的外部索引鍵和多對多關聯性啟用串聯刪除。</span><span class="sxs-lookup"><span data-stu-id="763f8-276">By convention, the Entity Framework enables cascade delete for non-nullable foreign keys and for many-to-many relationships.</span></span> <span data-ttu-id="763f8-277">這可能會導致循環串聯刪除規則，並在您嘗試新增移轉時造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="763f8-277">This can result in circular cascade delete rules, which will cause an exception when you try to add a migration.</span></span> <span data-ttu-id="763f8-278">例如，如果您未將`Department.InstructorID`屬性定義為可為 null，則會收到下列例外狀況訊息：「引用關聯性會產生不允許的迴圈參考。」</span><span class="sxs-lookup"><span data-stu-id="763f8-278">For example, if you didn't define the `Department.InstructorID` property as nullable, you'd get the following exception message: "The referential relationship will result in a cyclical reference that's not allowed."</span></span> <span data-ttu-id="763f8-279">如果您的商務規則`InstructorID`所需的屬性不可為 null，您就必須使用下列 Fluent API 語句來停用關聯性的 cascade 刪除：</span><span class="sxs-lookup"><span data-stu-id="763f8-279">If your business rules required `InstructorID` property to be non-nullable, you would have to use the following fluent API statement to disable cascade delete on the relationship:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modify-the-enrollment-entity"></a><span data-ttu-id="763f8-280">修改 Enrollment 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-280">Modify the Enrollment entity</span></span>

 <span data-ttu-id="763f8-281">在*Models\Enrollment.cs*中，將您先前新增的程式碼取代為下列程式碼</span><span class="sxs-lookup"><span data-stu-id="763f8-281">In *Models\Enrollment.cs*, replace the code you added earlier with the following code</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=1,15)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="763f8-282">外鍵和導覽屬性</span><span class="sxs-lookup"><span data-stu-id="763f8-282">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="763f8-283">外部索引鍵屬性及導覽屬性反映了下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="763f8-283">The foreign key properties and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="763f8-284">註冊記錄乃針對單一課程，因此當中包含了一個 `CourseID` 外部索引鍵屬性及一個 `Course` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="763f8-284">An enrollment record is for a single course, so there's a `CourseID` foreign key property and a `Course` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs)]
- <span data-ttu-id="763f8-285">註冊記錄乃針對單一學生，因此當中包含了一個 `StudentID` 外部索引鍵屬性及一個 `Student` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="763f8-285">An enrollment record is for a single student, so there's a `StudentID` foreign key property and a `Student` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]

### <a name="many-to-many-relationships"></a><span data-ttu-id="763f8-286">多對多關聯性</span><span class="sxs-lookup"><span data-stu-id="763f8-286">Many-to-Many Relationships</span></span>

<span data-ttu-id="763f8-287">`Student` `Enrollment`和實體`Course`之間有多對多關聯性，而實體會當做多對多聯結資料表，並*具有*資料庫中的裝載。</span><span class="sxs-lookup"><span data-stu-id="763f8-287">There's a many-to-many relationship between the `Student` and `Course` entities, and the `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="763f8-288">這表示`Enrollment`資料表除了聯結的資料表外鍵之外，還包含額外的資料（在此案例中是主鍵`Grade`和屬性）。</span><span class="sxs-lookup"><span data-stu-id="763f8-288">This means that the `Enrollment` table contains additional data besides foreign keys for the joined tables (in this case, a primary key and a `Grade` property).</span></span>

<span data-ttu-id="763f8-289">下列圖例展示了在實體圖表中這些關聯性的樣子。</span><span class="sxs-lookup"><span data-stu-id="763f8-289">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="763f8-290">（此圖表是使用 Entity Framework 的[Power](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)tool 產生的; 建立圖表並不是本教學課程的一部分，它只會在這裡用來做為圖例）。</span><span class="sxs-lookup"><span data-stu-id="763f8-290">(This diagram was generated using the [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); creating the diagram isn't part of the tutorial, it's just being used here as an illustration.)</span></span>

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

<span data-ttu-id="763f8-292">每個關聯線的一端都有1個，另一個\*是星號（），表示一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="763f8-292">Each relationship line has a 1 at one end and an asterisk (\*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="763f8-293">如果資料表未包含等級資訊，則只需要包含兩個外鍵`CourseID`和`StudentID`。 `Enrollment`</span><span class="sxs-lookup"><span data-stu-id="763f8-293">If the `Enrollment` table didn't include grade information, it would only need to contain the two foreign keys `CourseID` and `StudentID`.</span></span> <span data-ttu-id="763f8-294">在此情況下，它會對應至資料庫中*沒有*承載（或*純粹聯結資料表*）的多對多聯結資料表，而且您完全不需要為其建立模型類別。</span><span class="sxs-lookup"><span data-stu-id="763f8-294">In that case, it would correspond to a many-to-many join table *without payload* (or a *pure join table*) in the database, and you wouldn't have to create a model class for it at all.</span></span> <span data-ttu-id="763f8-295">`Instructor` 和`Course`實體具有該類型的多對多關聯性，如您所見，它們之間沒有實體類別：</span><span class="sxs-lookup"><span data-stu-id="763f8-295">The `Instructor` and `Course` entities have that kind of many-to-many relationship, and as you can see, there is no entity class between them:</span></span>

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

<span data-ttu-id="763f8-297">不過，資料庫中需要有聯結資料表，如下列資料庫關係圖所示：</span><span class="sxs-lookup"><span data-stu-id="763f8-297">A join table is required in the database, however, as shown in the following database diagram:</span></span>

![Instructor-Course_many-to-many_relationship_tables](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="763f8-299">Entity Framework 會自動建立`CourseInstructor`資料表，而且您可以藉由讀取和`Instructor.Courses`更新和`Course.Instructors`導覽屬性，間接讀取和更新該資料表。</span><span class="sxs-lookup"><span data-stu-id="763f8-299">The Entity Framework automatically creates the `CourseInstructor` table, and you read and update it indirectly by reading and updating the `Instructor.Courses` and `Course.Instructors` navigation properties.</span></span>

## <a name="entity-relationship-diagram"></a><span data-ttu-id="763f8-300">實體關聯性圖表</span><span class="sxs-lookup"><span data-stu-id="763f8-300">Entity relationship diagram</span></span>

<span data-ttu-id="763f8-301">下列圖例顯示了 Entity Framework Power Tools 為完成的 School 模型建立的圖表。</span><span class="sxs-lookup"><span data-stu-id="763f8-301">The following illustration shows the diagram that the Entity Framework Power Tools create for the completed School model.</span></span>

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="763f8-303">除了多對多關聯性線條（\*至\*）和一對多關聯性線條（1到\*），您可以在這裡看到`Instructor`與`OfficeAssignment`之間的一對一關聯性線條（1到 0 ..1）。「講師」和「部門」實體之間的實體和零或一對多關聯性線條（0 ..1 \*到）。</span><span class="sxs-lookup"><span data-stu-id="763f8-303">Besides the many-to-many relationship lines (\* to \*) and the one-to-many relationship lines (1 to \*), you can see here the one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities and the zero-or-one-to-many relationship line (0..1 to \*) between the Instructor and Department entities.</span></span>

## <a name="add-code-to-database-context"></a><span data-ttu-id="763f8-304">將程式碼加入至資料庫內容</span><span class="sxs-lookup"><span data-stu-id="763f8-304">Add code to database context</span></span>

<span data-ttu-id="763f8-305">接下來，您會將新實體新增`SchoolContext`至類別，並使用[Fluent API](https://msdn.microsoft.com/data/jj591617)呼叫來自訂部分對應。</span><span class="sxs-lookup"><span data-stu-id="763f8-305">Next you'll add the new entities to the `SchoolContext` class and customize some of the mapping using [fluent API](https://msdn.microsoft.com/data/jj591617) calls.</span></span> <span data-ttu-id="763f8-306">API 是「流暢」的，因為它通常是用來將一系列的方法呼叫串連成單一語句，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="763f8-306">The API is "fluent" because it's often used by stringing a series of method calls together into a single statement, as in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

<span data-ttu-id="763f8-307">在本教學課程中，您只會將 Fluent API 用於無法使用屬性進行的資料庫對應。</span><span class="sxs-lookup"><span data-stu-id="763f8-307">In this tutorial you'll use the fluent API only for database mapping that you can't do with attributes.</span></span> <span data-ttu-id="763f8-308">然而，您也可以使用 Fluent API 指定大部分透過屬性可完成的格式、驗證及對應規則。</span><span class="sxs-lookup"><span data-stu-id="763f8-308">However, you can also use the fluent API to specify most of the formatting, validation, and mapping rules that you can do by using attributes.</span></span> <span data-ttu-id="763f8-309">某些屬性 (例如 `MinimumLength`) 無法使用 Fluent API 來套用。</span><span class="sxs-lookup"><span data-stu-id="763f8-309">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="763f8-310">如先前所述`MinimumLength` ，不會變更架構，它只會套用用戶端和伺服器端驗證規則。</span><span class="sxs-lookup"><span data-stu-id="763f8-310">As mentioned previously, `MinimumLength` doesn't change the schema, it only applies a client and server side validation rule</span></span>

<span data-ttu-id="763f8-311">某些開發人員偏好單獨使用 Fluent API，使其實體類別保持「整潔」。</span><span class="sxs-lookup"><span data-stu-id="763f8-311">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="763f8-312">若想要的話，您也可以混合使用屬性和 Fluent API，並且有一些自訂項目只能使用 Fluent API 完成。但一般來說，建議的做法是在這兩種方法中選擇其中一項，然後盡可能的一致使用該方法。</span><span class="sxs-lookup"><span data-stu-id="763f8-312">You can mix attributes and fluent API if you want, and there are a few customizations that can only be done by using fluent API, but in general the recommended practice is to choose one of these two approaches and use that consistently as much as possible.</span></span>

<span data-ttu-id="763f8-313">若要將新的實體加入至資料模型，並執行您未使用屬性執行的資料庫對應，請將*DAL\SchoolCoNtext.cs*中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="763f8-313">To add the new entities to the data model and perform database mapping that you didn't do by using attributes, replace the code in *DAL\SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="763f8-314">[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的新語句會設定多對多聯結資料表：</span><span class="sxs-lookup"><span data-stu-id="763f8-314">The new statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method configures the many-to-many join table:</span></span>

- <span data-ttu-id="763f8-315">對於`Instructor` 和`Course`實體之間的多對多關聯性，此程式碼會指定聯結資料表的資料表和資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="763f8-315">For the many-to-many relationship between the `Instructor` and `Course` entities, the code specifies the table and column names for the join table.</span></span> <span data-ttu-id="763f8-316">Code First 可以為您設定多對多關聯性，而不需要此程式碼，但如果您未呼叫它，則會取得預設名稱`InstructorInstructorID` （ `InstructorID`例如資料行的）。</span><span class="sxs-lookup"><span data-stu-id="763f8-316">Code First can configure the many-to-many relationship for you without this code, but if you don't call it, you will get default names such as `InstructorInstructorID` for the `InstructorID` column.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="763f8-317">下列程式碼提供如何使用 Fluent API （而非屬性）來指定`Instructor`和`OfficeAssignment`實體之間關聯性的範例：</span><span class="sxs-lookup"><span data-stu-id="763f8-317">The following code provides an example of how you could have used fluent API instead of attributes to specify the relationship between the `Instructor` and `OfficeAssignment` entities:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

<span data-ttu-id="763f8-318">如需有關「Fluent API」語句如何在幕後執行的資訊，請參閱[流暢的 API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog 文章。</span><span class="sxs-lookup"><span data-stu-id="763f8-318">For information about what "fluent API" statements are doing behind the scenes, see the [Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog post.</span></span>

## <a name="seed-database-with-test-data"></a><span data-ttu-id="763f8-319">將測試資料植入資料庫</span><span class="sxs-lookup"><span data-stu-id="763f8-319">Seed database with test data</span></span>

<span data-ttu-id="763f8-320">將*Migrations\Configuration.cs*檔案中的程式碼取代為下列程式碼，以便為您所建立的新實體提供種子資料。</span><span class="sxs-lookup"><span data-stu-id="763f8-320">Replace the code in the *Migrations\Configuration.cs* file with the following code in order to provide seed data for the new entities you've created.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

<span data-ttu-id="763f8-321">如您在第一個教學課程中所見，大部分的程式碼只會更新或建立新的實體物件，並視需要將範例資料載入至屬性，以供測試之用。</span><span class="sxs-lookup"><span data-stu-id="763f8-321">As you saw in the first tutorial, most of this code simply updates or creates new entity objects and loads sample data into properties as required for testing.</span></span> <span data-ttu-id="763f8-322">不過，請注意`Course`實體（ `Instructor`與實體具有多對多關聯性）的處理方式：</span><span class="sxs-lookup"><span data-stu-id="763f8-322">However, notice how the `Course` entity, which has a many-to-many relationship with the `Instructor` entity, is handled:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

<span data-ttu-id="763f8-323">當您建立`Course`物件時，您可以使用`Instructors`程式碼`Instructors = new List<Instructor>()`，將導覽屬性初始化為空集合。</span><span class="sxs-lookup"><span data-stu-id="763f8-323">When you create a `Course` object, you initialize the `Instructors` navigation property as an empty collection using the code `Instructors = new List<Instructor>()`.</span></span> <span data-ttu-id="763f8-324">這讓您可以使用`Instructor` `Instructors.Add`方法來新增與此`Course`相關的實體。</span><span class="sxs-lookup"><span data-stu-id="763f8-324">This makes it possible to add `Instructor` entities that are related to this `Course` by using the `Instructors.Add` method.</span></span> <span data-ttu-id="763f8-325">如果您沒有建立空白清單，就無法加入這些關聯性，因為`Instructors`屬性會是 null，而且不會`Add`有方法。</span><span class="sxs-lookup"><span data-stu-id="763f8-325">If you didn't create an empty list, you wouldn't be able to add these relationships, because the `Instructors` property would be null and wouldn't have an `Add` method.</span></span> <span data-ttu-id="763f8-326">您也可以將清單初始化加入至此函式。</span><span class="sxs-lookup"><span data-stu-id="763f8-326">You could also add the list initialization to the constructor.</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="763f8-327">新增移轉</span><span class="sxs-lookup"><span data-stu-id="763f8-327">Add a migration</span></span>

<span data-ttu-id="763f8-328">在 PMC 中，輸入`add-migration`命令（不要`update-database`執行命令）：</span><span class="sxs-lookup"><span data-stu-id="763f8-328">From the PMC, enter the `add-migration` command (don't do the `update-database` command yet):</span></span>

`add-Migration ComplexDataModel`

<span data-ttu-id="763f8-329">若您嘗試在這個時間點執行 `update-database` 命令，您會接收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="763f8-329">If you tried to run the `update-database` command at this point (don't do it yet), you would get the following error:</span></span>

<span data-ttu-id="763f8-330">*ALTER TABLE 語句與外鍵條件約束 "FK\_dbo ' 衝突。當然\_是 dbo。部門\_DepartmentID」。衝突發生在資料庫 "ContosoUniversity"，資料表 "dbo。部門 "，資料行 ' DepartmentID '。*</span><span class="sxs-lookup"><span data-stu-id="763f8-330">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Course\_dbo.Department\_DepartmentID". The conflict occurred in database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.*</span></span>

<span data-ttu-id="763f8-331">有時候當您使用現有的資料執行遷移時，您需要將存根資料插入資料庫中以滿足 foreign key 條件約束，這就是您現在必須執行的動作。</span><span class="sxs-lookup"><span data-stu-id="763f8-331">Sometimes when you execute migrations with existing data, you need to insert stub data into the database to satisfy foreign key constraints, and that's what you have to do now.</span></span> <span data-ttu-id="763f8-332">在 ComplexDataModel `Up`方法中產生的程式碼會將不可為`DepartmentID` null 的外鍵`Course`加入至資料表。</span><span class="sxs-lookup"><span data-stu-id="763f8-332">The generated code in the ComplexDataModel `Up` method adds a non-nullable `DepartmentID` foreign key to the `Course` table.</span></span> <span data-ttu-id="763f8-333">當程式碼執行時`Course` `AddColumn` ，資料表中已經有資料列，因此作業將會失敗，因為 SQL Server 不知道要放入資料行中的值不能是 null。</span><span class="sxs-lookup"><span data-stu-id="763f8-333">Because there are already rows in the `Course` table when the code runs, the `AddColumn` operation will fail because SQL Server doesn't know what value to put in the column that can't be null.</span></span> <span data-ttu-id="763f8-334">因此，必須變更程式碼以提供新的資料行預設值，並建立名為 "Temp" 的 stub 部門，以作為預設部門。</span><span class="sxs-lookup"><span data-stu-id="763f8-334">Therefore have to change the code to give the new column a default value, and create a stub department named "Temp" to act as the default department.</span></span> <span data-ttu-id="763f8-335">如此一來，現有`Course`的資料列就會在`Up`方法執行之後與「Temp」部門產生關聯。</span><span class="sxs-lookup"><span data-stu-id="763f8-335">As a result, existing `Course` rows will all be related to the "Temp" department after the `Up` method runs.</span></span> <span data-ttu-id="763f8-336">您可以在`Seed`方法中將它們與正確的部門產生關聯。</span><span class="sxs-lookup"><span data-stu-id="763f8-336">You can relate them to the correct departments in the `Seed` method.</span></span>

<span data-ttu-id="763f8-337">編輯時間*戳\_ComplexDataModel.cs 檔案，將加入 DepartmentID 資料行的程式程式碼批註化至課程資料表，並新增下列反白顯示的程式碼（批註的那一行也是&gt;*  &lt;已反白顯示）：</span><span class="sxs-lookup"><span data-stu-id="763f8-337">Edit the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, comment out the line of code that adds the DepartmentID column to the Course table, and add the following highlighted code (the commented line is also highlighted):</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

<span data-ttu-id="763f8-338">當方法執行時，它會將資料列插入`Department`資料表中，並將現有`Course`的資料列與`Department`這些新的資料列產生關聯。 `Seed`</span><span class="sxs-lookup"><span data-stu-id="763f8-338">When the `Seed` method runs, it will insert rows in the `Department` table and it will relate existing `Course` rows to those new `Department` rows.</span></span> <span data-ttu-id="763f8-339">如果您還沒有在 UI 中新增任何課程，就不再需要資料`Course.DepartmentID`行的「Temp」部門或預設值。</span><span class="sxs-lookup"><span data-stu-id="763f8-339">If you haven't added any courses in the UI, you would then no longer need the "Temp" department or the default value on the `Course.DepartmentID` column.</span></span> <span data-ttu-id="763f8-340">為了讓使用者可以使用應用程式來新增課程，您也會想要更新`Seed`方法程式碼，以確保所有`Course`的資料列（不只是先前執行`Seed`方法所插入的資料列）都具有在`DepartmentID`您移除資料行中的預設值並刪除「暫存」部門之前的有效值。</span><span class="sxs-lookup"><span data-stu-id="763f8-340">To allow for the possibility that someone might have added courses by using the application, you'd also want to update the `Seed` method code to ensure that all `Course` rows (not just the ones inserted by earlier runs of the `Seed` method) have valid `DepartmentID` values before you remove the default value from the column and delete the "Temp" department.</span></span>

## <a name="update-the-database"></a><span data-ttu-id="763f8-341">更新資料庫</span><span class="sxs-lookup"><span data-stu-id="763f8-341">Update the database</span></span>

<span data-ttu-id="763f8-342">完成&lt; `update-database` *時間戳&gt;ComplexDataModel.cs 檔案的編輯之後，請在 PMC 中輸入命令來執行遷移。\_*</span><span class="sxs-lookup"><span data-stu-id="763f8-342">After you have finished editing the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, enter the `update-database` command in the PMC to execute the migration.</span></span>

[!code-powershell[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.ps1)]

> [!NOTE]
> <span data-ttu-id="763f8-343">當您遷移資料並進行架構變更時，可能會收到其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="763f8-343">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="763f8-344">如果收到無法解決的移轉錯誤，您可以變更連接字串中的資料庫名稱，或刪除該資料庫。</span><span class="sxs-lookup"><span data-stu-id="763f8-344">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="763f8-345">最簡單的方法是在*web.config*檔案中重新命名資料庫。</span><span class="sxs-lookup"><span data-stu-id="763f8-345">The simplest approach is to rename the database in *Web.config* file.</span></span> <span data-ttu-id="763f8-346">下列範例顯示已變更為 CU\_測試的名稱：</span><span class="sxs-lookup"><span data-stu-id="763f8-346">The following example shows the name changed to CU\_Test:</span></span>
>
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample36.xml?highlight=1)]
>
> <span data-ttu-id="763f8-347">使用新的資料庫時，沒有可遷移的資料，而命令`update-database`更可能會在沒有錯誤的情況下完成。</span><span class="sxs-lookup"><span data-stu-id="763f8-347">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="763f8-348">如需有關如何刪除資料庫的指示，請參閱[如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="763f8-348">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span>
>
> <span data-ttu-id="763f8-349">如果失敗，您可以嘗試的另一件事就是在 PMC 中輸入下列命令來重新初始化資料庫：</span><span class="sxs-lookup"><span data-stu-id="763f8-349">If that fails, another thing you can try is re-initialize the database by entering the following command in the PMC:</span></span>
>
> `update-database -TargetMigration:0`

<span data-ttu-id="763f8-350">如先前所述在**伺服器總管**中開啟資料庫，然後展開 [**資料表]** 節點，以查看所有資料表都已建立。</span><span class="sxs-lookup"><span data-stu-id="763f8-350">Open the database in **Server Explorer** as you did earlier, and expand the **Tables** node to see that all of the tables have been created.</span></span> <span data-ttu-id="763f8-351">（如果您還**伺服器總管**從較早的時間開啟，請按一下 [重新整理 **] 按鈕）** 。</span><span class="sxs-lookup"><span data-stu-id="763f8-351">(If you still have **Server Explorer** open from the earlier time, click the **Refresh** button.)</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image16.png)

<span data-ttu-id="763f8-352">您未建立`CourseInstructor`資料表的模型類別。</span><span class="sxs-lookup"><span data-stu-id="763f8-352">You didn't create a model class for the `CourseInstructor` table.</span></span> <span data-ttu-id="763f8-353">如先前所`Instructor`述，這是與`Course`實體之間的多對多關聯性的聯結資料表。</span><span class="sxs-lookup"><span data-stu-id="763f8-353">As explained earlier, this is a join table for the many-to-many relationship between the `Instructor` and `Course` entities.</span></span>

<span data-ttu-id="763f8-354">以滑鼠右鍵按一下`CourseInstructor`資料表，然後選取 [**顯示資料表資料**]，確認它在您新增至`Instructor` `Course.Instructors`導覽屬性的實體中有資料。</span><span class="sxs-lookup"><span data-stu-id="763f8-354">Right-click the `CourseInstructor` table and select **Show Table Data** to verify that it has data in it as a result of the `Instructor` entities you added to the `Course.Instructors` navigation property.</span></span>

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image17.png)

## <a name="get-the-code"></a><span data-ttu-id="763f8-356">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="763f8-356">Get the code</span></span>

[<span data-ttu-id="763f8-357">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="763f8-357">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="763f8-358">其他資源</span><span class="sxs-lookup"><span data-stu-id="763f8-358">Additional resources</span></span>

<span data-ttu-id="763f8-359">您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="763f8-359">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="763f8-360">後續步驟</span><span class="sxs-lookup"><span data-stu-id="763f8-360">Next steps</span></span>

<span data-ttu-id="763f8-361">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="763f8-361">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="763f8-362">自訂資料模型</span><span class="sxs-lookup"><span data-stu-id="763f8-362">Customized the data model</span></span>
> * <span data-ttu-id="763f8-363">更新的 Student 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-363">Updated Student entity</span></span>
> * <span data-ttu-id="763f8-364">建立 Instructor 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-364">Created Instructor entity</span></span>
> * <span data-ttu-id="763f8-365">建立 OfficeAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="763f8-365">Created OfficeAssignment entity</span></span>
> * <span data-ttu-id="763f8-366">已修改課程實體</span><span class="sxs-lookup"><span data-stu-id="763f8-366">Modified the Course entity</span></span>
> * <span data-ttu-id="763f8-367">建立部門實體</span><span class="sxs-lookup"><span data-stu-id="763f8-367">Created the Department entity</span></span>
> * <span data-ttu-id="763f8-368">已修改註冊實體</span><span class="sxs-lookup"><span data-stu-id="763f8-368">Modified the Enrollment entity</span></span>
> * <span data-ttu-id="763f8-369">已將程式碼新增至資料庫內容</span><span class="sxs-lookup"><span data-stu-id="763f8-369">Added code to database context</span></span>
> * <span data-ttu-id="763f8-370">將測試資料植入資料庫</span><span class="sxs-lookup"><span data-stu-id="763f8-370">Seeded database with test data</span></span>
> * <span data-ttu-id="763f8-371">新增移轉</span><span class="sxs-lookup"><span data-stu-id="763f8-371">Added a migration</span></span>
> * <span data-ttu-id="763f8-372">更新資料庫</span><span class="sxs-lookup"><span data-stu-id="763f8-372">Updated the database</span></span>

<span data-ttu-id="763f8-373">前進到下一篇文章，以瞭解如何讀取和顯示 Entity Framework 載入導覽屬性的相關資料。</span><span class="sxs-lookup"><span data-stu-id="763f8-373">Advance to the next article to learn how to read and display related data that the Entity Framework loads into navigation properties.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="763f8-374">讀取相關資料</span><span class="sxs-lookup"><span data-stu-id="763f8-374">Read related data</span></span>](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
