---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: 搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第2部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何在 ASP.NET MV 中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614972"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="1d964-103">搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第2部分</span><span class="sxs-lookup"><span data-stu-id="1d964-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>

<span data-ttu-id="1d964-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1d964-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="1d964-105">本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。</span><span class="sxs-lookup"><span data-stu-id="1d964-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="1d964-106">新增自動日期時間範本</span><span class="sxs-lookup"><span data-stu-id="1d964-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="1d964-107">在本教學課程的第一個部分中，您已瞭解如何將屬性加入至模型以明確指定格式，以及如何明確指定用來呈現模型的範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="1d964-108">例如，下列程式碼中的[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性會明確指定 `ReleaseDate` 屬性的格式。</span><span class="sxs-lookup"><span data-stu-id="1d964-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicitly specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="1d964-109">在下列範例中，使用 `Date` 列舉的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性會指定使用日期範本來呈現模型。</span><span class="sxs-lookup"><span data-stu-id="1d964-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="1d964-110">如果您的專案中沒有任何日期範本，則會使用內建的日期範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="1d964-111">不過，ASP。MVC 可以藉由尋找符合類型名稱的範本，使用慣例過度設定來執行類型比對。</span><span class="sxs-lookup"><span data-stu-id="1d964-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="1d964-112">這可讓您建立自動將資料格式化的範本，而完全不需要使用任何屬性或程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d964-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="1d964-113">在本教學課程的這個部分中，您將建立自動套用至[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)類型之模型屬性的範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="1d964-114">您不需要使用屬性或其他設定來指定範本應該用來呈現[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)類型的所有模型屬性。</span><span class="sxs-lookup"><span data-stu-id="1d964-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="1d964-115">您也將學習自訂個別屬性或甚至是個別欄位的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="1d964-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="1d964-116">首先，讓我們移除現有的格式資訊，並在應用程式中顯示完整的日期。</span><span class="sxs-lookup"><span data-stu-id="1d964-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="1d964-117">開啟*Movie.cs*檔案，並將 `ReleaseDate` 屬性上的 `DataType` 屬性標記為批註：</span><span class="sxs-lookup"><span data-stu-id="1d964-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="1d964-118">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d964-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1d964-119">請注意，[`ReleaseDate`] 屬性現在會顯示日期和時間，因為這是未提供任何格式資訊時的預設值。</span><span class="sxs-lookup"><span data-stu-id="1d964-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="1d964-120">加入用來測試新範本的 CSS 樣式</span><span class="sxs-lookup"><span data-stu-id="1d964-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="1d964-121">在建立格式化日期的範本之前，您將會新增一些 CSS 樣式規則，以套用至新的範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="1d964-122">這些會協助您確認轉譯的頁面使用的是新的範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="1d964-123">開啟*Content\Site.cs*s 檔案，然後將下列 CSS 規則新增至檔案的底部：</span><span class="sxs-lookup"><span data-stu-id="1d964-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="1d964-124">加入日期時間顯示範本</span><span class="sxs-lookup"><span data-stu-id="1d964-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="1d964-125">現在您可以建立新的範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-125">Now you can create the new template.</span></span> <span data-ttu-id="1d964-126">在*Views\Movies*資料夾中，建立*DisplayTemplates*資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d964-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="1d964-127">在*Views\Shared*資料夾中，建立*DisplayTemplates*資料夾和*EditorTemplates*資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d964-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="1d964-128">所有的控制器都會使用*Views\Shared\DisplayTemplates*資料夾中的顯示範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="1d964-129">只有 `Movie` 控制器才會使用*Views\Movie\DisplayTemplates*資料夾中的顯示範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="1d964-130">（如果兩個資料夾中出現相同名稱的範本，則*Views\Movie\DisplayTemplates*資料夾中的範本（也就是較特定的範本）會優先使用 `Movie` 控制器所傳回的視圖）。</span><span class="sxs-lookup"><span data-stu-id="1d964-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="1d964-131">在**方案總管**中，展開 [ *Views* ] 資料夾，展開 [ *Shared* ] 資料夾，然後以滑鼠右鍵按一下 [ *Views\Shared\DisplayTemplates* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d964-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="1d964-132">按一下 [**新增**]，然後按一下 [ **View**]。</span><span class="sxs-lookup"><span data-stu-id="1d964-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="1d964-133">[**加入視圖**] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="1d964-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="1d964-134">在 [**視圖名稱**] 方塊中，輸入 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="1d964-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="1d964-135">（您必須使用此名稱才能符合類型的名稱）。</span><span class="sxs-lookup"><span data-stu-id="1d964-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="1d964-136">選取 [**建立為部分視圖**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1d964-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="1d964-137">請確定未選取 [**使用版面配置或主版] 頁面**，並**建立 [強型別視圖**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1d964-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="1d964-138">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1d964-138">Click **Add**.</span></span> <span data-ttu-id="1d964-139">*Views\Shared\DisplayTemplates*中會建立*日期時間 cshtml*範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="1d964-140">下圖顯示 [`DateTime` 顯示] 和 [編輯器] 範本建立後**方案總管**中的 [ *Views* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d964-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="1d964-141">開啟*Views\Shared\DisplayTemplates\DateTime.cshtml*檔案，並新增下列標記，它會使用[字串. format](https://msdn.microsoft.com/library/system.string.format.aspx)方法將屬性格式化為不含時間的日期。</span><span class="sxs-lookup"><span data-stu-id="1d964-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="1d964-142">（`{0:d}` 格式會指定簡短日期格式）。</span><span class="sxs-lookup"><span data-stu-id="1d964-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="1d964-143">重複此步驟，在*Views\Movie\DisplayTemplates*資料夾中建立 `DateTime` 範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="1d964-144">在*Views\Movie\DisplayTemplates\DateTime.cshtml*檔案中使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d964-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="1d964-145">`loud-1` CSS 類別會使日期以粗體的紅色文字顯示。</span><span class="sxs-lookup"><span data-stu-id="1d964-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="1d964-146">您已將 `loud-1` CSS 類別新增為暫時的量值，因此您可以輕鬆地查看何時使用此特定範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="1d964-147">您所做的就是建立和自訂範本，ASP.NET 將用來顯示日期。</span><span class="sxs-lookup"><span data-stu-id="1d964-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="1d964-148">較一般的範本（在*Views\Shared\DisplayTemplates*資料夾中）會顯示簡單的簡短日期。</span><span class="sxs-lookup"><span data-stu-id="1d964-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="1d964-149">特別針對 `Movie` 控制器（在*Views\Movies\DisplayTemplates*資料夾中）的範本會顯示一段簡短的日期，並將其格式化為粗體的紅色文字。</span><span class="sxs-lookup"><span data-stu-id="1d964-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="1d964-150">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d964-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="1d964-151">瀏覽器會呈現應用程式的索引視圖。</span><span class="sxs-lookup"><span data-stu-id="1d964-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="1d964-152">`ReleaseDate` 屬性現在會以粗體紅色字型顯示不含時間的日期。這可協助您確認已選取 [ *Views\Movies\DisplayTemplates* ] 資料夾中的 `DateTime` 樣板化協助程式，其方式是在共用資料夾中 `DateTime` 樣板化 helper （*Views\Shared\DisplayTemplates*）。</span><span class="sxs-lookup"><span data-stu-id="1d964-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="1d964-153">現在將*Views\Movies\DisplayTemplates\DateTime.cshtml*檔案重新命名為*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1d964-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="1d964-154">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d964-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1d964-155">此時，`ReleaseDate` 屬性會顯示不含時間且不含粗體紅色字型的日期。</span><span class="sxs-lookup"><span data-stu-id="1d964-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="1d964-156">這說明具有資料類型名稱的範本（在此案例中為 `DateTime`）會自動用來顯示該類型的所有模型屬性。</span><span class="sxs-lookup"><span data-stu-id="1d964-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="1d964-157">在您將*DateTime. cshtml*檔案重新命名*為 LoudDateTime*之後，ASP.NET 在*Views\Movies\DisplayTemplates*資料夾中找不到範本，因此它使用了 \* Views\Movies\Shared\* 資料夾中的*DateTime. cshtml*範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the \*Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="1d964-158">（範本比對不區分大小寫，因此您可以使用任何大小寫來建立範本檔案名。</span><span class="sxs-lookup"><span data-stu-id="1d964-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="1d964-159">例如， *datetime. cshtml、datetime. cshtml*和*datetime. cshtml*全都符合 `DateTime` 類型）。</span><span class="sxs-lookup"><span data-stu-id="1d964-159">For example, *DATETIME.cshtml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="1d964-160">若要進行檢查：此時會使用*Views\Movies\DisplayTemplates\DateTime.cshtml*範本來顯示 [`ReleaseDate`] 欄位，這會顯示使用簡短日期格式的資料，但不會新增任何特殊格式。</span><span class="sxs-lookup"><span data-stu-id="1d964-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="1d964-161">使用 UIHint 指定顯示範本</span><span class="sxs-lookup"><span data-stu-id="1d964-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="1d964-162">如果您的 web 應用程式有許多 `DateTime` 欄位，而且根據預設，您想要以僅限日期的格式來顯示全部或大部分，則*DateTime. cshtml*範本是不錯的方法。</span><span class="sxs-lookup"><span data-stu-id="1d964-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="1d964-163">但是，如果您有幾個想要顯示完整日期和時間的日期呢？</span><span class="sxs-lookup"><span data-stu-id="1d964-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="1d964-164">沒問題。</span><span class="sxs-lookup"><span data-stu-id="1d964-164">No problem.</span></span> <span data-ttu-id="1d964-165">您可以建立額外的範本，並使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性來指定完整日期和時間的格式。</span><span class="sxs-lookup"><span data-stu-id="1d964-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="1d964-166">然後，您可以選擇性地套用該範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-166">You can then selectively apply that template.</span></span> <span data-ttu-id="1d964-167">您可以在模型層級使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性，也可以在視圖內指定範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="1d964-168">在本節中，您將瞭解如何使用 `UIHint` 屬性，選擇性地變更一些日期時間欄位實例的格式。</span><span class="sxs-lookup"><span data-stu-id="1d964-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="1d964-169">開啟*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*檔案，並將現有的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="1d964-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="1d964-170">這會顯示完整的日期和時間，並加入讓文字變成綠色和大的 CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="1d964-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="1d964-171">開啟*Movie.cs*檔案，並將[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性新增至 `ReleaseDate` 屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="1d964-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="1d964-172">這會告訴 ASP.NET MVC，當它顯示 `ReleaseDate` 屬性（具體而言，而不只是任何 `DateTime` 物件）時，應該使用*LoudDateTime*範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="1d964-173">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d964-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1d964-174">請注意，[`ReleaseDate`] 屬性現在會以較大的綠色字型顯示日期和時間。</span><span class="sxs-lookup"><span data-stu-id="1d964-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="1d964-175">回到*Movie.cs*檔案中的 `UIHint` 屬性並將它批註，以便不使用*LoudDateTime*範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="1d964-176">再次執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d964-176">Run the application again.</span></span> <span data-ttu-id="1d964-177">發行日期不會顯示為 [大] 和 [綠色]。</span><span class="sxs-lookup"><span data-stu-id="1d964-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="1d964-178">這會驗證 [索引] 和 [詳細資料] 視圖中是否使用*Views\Shared\DisplayTemplates\DateTime.cshtml*範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="1d964-179">如先前所述，您也可以在 view 中套用範本，這可讓您將範本套用至某些資料的個別實例。</span><span class="sxs-lookup"><span data-stu-id="1d964-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="1d964-180">開啟 [ *Views\Movies\Details.cshtml* ] 視圖。</span><span class="sxs-lookup"><span data-stu-id="1d964-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="1d964-181">新增 `"LoudDateTime"` 做為 [`ReleaseDate`] 欄位之[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)呼叫的第二個參數。</span><span class="sxs-lookup"><span data-stu-id="1d964-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="1d964-182">完成的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d964-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="1d964-183">這會指定應該使用 `LoudDateTime` 範本來顯示模型屬性，而不論哪些屬性會套用至模型。</span><span class="sxs-lookup"><span data-stu-id="1d964-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="1d964-184">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d964-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1d964-185">確認電影 [索引] 頁面使用的是*Views\Shared\DisplayTemplates\DateTime.cshtml*範本（紅色粗體），而 [ *Movie\Details* ] 頁面使用的是*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*範本（大和綠色）。</span><span class="sxs-lookup"><span data-stu-id="1d964-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="1d964-186">在下一節中，您將建立複雜類型的範本。</span><span class="sxs-lookup"><span data-stu-id="1d964-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1d964-187">[上一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [下一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="1d964-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
