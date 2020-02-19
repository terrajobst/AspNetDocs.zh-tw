---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第4部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何在 ASP.NET MV 中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457488"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a><span data-ttu-id="84cad-103">搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第4部分</span><span class="sxs-lookup"><span data-stu-id="84cad-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 4</span></span>

<span data-ttu-id="84cad-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="84cad-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="84cad-105">本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。</span><span class="sxs-lookup"><span data-stu-id="84cad-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

### <a name="adding-a-template-for-editing-dates"></a><span data-ttu-id="84cad-106">新增用於編輯日期的範本</span><span class="sxs-lookup"><span data-stu-id="84cad-106">Adding a Template for Editing Dates</span></span>

<span data-ttu-id="84cad-107">在本節中，您將會建立編輯日期的範本，當 ASP.NET MVC 顯示 UI 來編輯以 DataType 屬性的**日期**列舉標記的模型屬性時，將會套用這些[資料](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)。</span><span class="sxs-lookup"><span data-stu-id="84cad-107">In this section you'll create a template for editing dates that will be applied when ASP.NET MVC displays UI for editing model properties that are marked with the **Date** enumeration of the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute.</span></span> <span data-ttu-id="84cad-108">此範本只會轉譯日期;將不會顯示時間。</span><span class="sxs-lookup"><span data-stu-id="84cad-108">The template will render only the date; time will not be displayed.</span></span> <span data-ttu-id="84cad-109">在範本中，您將使用[JQUERY UI Datepicker](http://jqueryui.com/demos/datepicker/)快顯行事歷來提供編輯日期的方法。</span><span class="sxs-lookup"><span data-stu-id="84cad-109">In the template you'll use the [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to provide a way to edit dates.</span></span>

<span data-ttu-id="84cad-110">若要開始，請開啟*Movie.cs*檔案，並將具有**Date**列舉的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性加入至 `ReleaseDate` 屬性，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="84cad-110">To begin, open the *Movie.cs* file and add the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute with the **Date** enumeration to the `ReleaseDate` property, as shown in the following code:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

<span data-ttu-id="84cad-111">此程式碼會顯示顯示範本和編輯範本中的 [`ReleaseDate`] 欄位，而不會有時間。</span><span class="sxs-lookup"><span data-stu-id="84cad-111">This code causes the `ReleaseDate` field to be displayed without the time in both display templates and edit templates.</span></span> <span data-ttu-id="84cad-112">如果您的應用程式在*Views\Shared\EditorTemplates*資料夾或*Views\Movies\EditorTemplates*資料夾中包含*date. cshtml*範本，則在編輯時，將會使用該範本來呈現任何 `DateTime` 屬性。</span><span class="sxs-lookup"><span data-stu-id="84cad-112">If your application contains a *date.cshtml* template in the *Views\Shared\EditorTemplates* folder or in the *Views\Movies\EditorTemplates* folder, that template will be used to render any `DateTime` property while editing.</span></span> <span data-ttu-id="84cad-113">否則，內建的 ASP.NET 範本化系統會將屬性顯示為日期。</span><span class="sxs-lookup"><span data-stu-id="84cad-113">Otherwise the built-in ASP.NET templating system will display the property as a date.</span></span>

<span data-ttu-id="84cad-114">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="84cad-114">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="84cad-115">選取 [編輯] 連結，以確認 [發行日期] 的輸入欄位只顯示日期。</span><span class="sxs-lookup"><span data-stu-id="84cad-115">Select an edit link to verify that the input field for the release date is showing only the date.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

<span data-ttu-id="84cad-116">在**方案總管**中，展開 [ *Views* ] 資料夾，展開 [ *Shared* ] 資料夾，然後以滑鼠右鍵按一下 [ *Views\Shared\EditorTemplates* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="84cad-116">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\EditorTemplates* folder.</span></span>

<span data-ttu-id="84cad-117">按一下 [**新增**]，然後按一下 [ **View**]。</span><span class="sxs-lookup"><span data-stu-id="84cad-117">Click **Add**, and then click **View**.</span></span> <span data-ttu-id="84cad-118">[**加入視圖**] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="84cad-118">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="84cad-119">在 [**視圖名稱**] 方塊中，輸入 &quot;日期&quot;。</span><span class="sxs-lookup"><span data-stu-id="84cad-119">In the **View name** box, type &quot;Date&quot;.</span></span>

<span data-ttu-id="84cad-120">選取 [**建立為部分視圖**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="84cad-120">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="84cad-121">請確定未選取 [**使用版面配置或主版] 頁面**，並**建立 [強型別視圖**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="84cad-121">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

<span data-ttu-id="84cad-122">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="84cad-122">Click **Add**.</span></span> <span data-ttu-id="84cad-123">隨即建立*Views\Shared\EditorTemplates\Date.cshtml*範本。</span><span class="sxs-lookup"><span data-stu-id="84cad-123">The *Views\Shared\EditorTemplates\Date.cshtml* template is created.</span></span>

<span data-ttu-id="84cad-124">將下列程式碼新增至*Views\Shared\EditorTemplates\Date.cshtml*範本。</span><span class="sxs-lookup"><span data-stu-id="84cad-124">Add the following code to the *Views\Shared\EditorTemplates\Date.cshtml* template.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

<span data-ttu-id="84cad-125">第一行會將模型宣告為 `DateTime` 型別。</span><span class="sxs-lookup"><span data-stu-id="84cad-125">The first line declares the model to be a `DateTime` type.</span></span> <span data-ttu-id="84cad-126">雖然您不需要在 [編輯] 和 [顯示] 範本中宣告模型類型，但最佳作法是讓您取得要傳遞至視圖之模型的編譯時間檢查。</span><span class="sxs-lookup"><span data-stu-id="84cad-126">Although you don't need to declare the model type in edit and display templates, it's a best practice so that you get compile-time checking of the model being passed to the view.</span></span> <span data-ttu-id="84cad-127">（另一個好處是，您可以在 Visual Studio 的視圖中取得模型的 IntelliSense）。如果模型類型未宣告，ASP.NET MVC 會將它視為[動態](https://msdn.microsoft.com/library/dd264741.aspx)類型，而且不會有編譯時間類型檢查。</span><span class="sxs-lookup"><span data-stu-id="84cad-127">(Another benefit is that you then get IntelliSense for the model in the view in Visual Studio.) If the model type is not declared, ASP.NET MVC considers it a [dynamic](https://msdn.microsoft.com/library/dd264741.aspx) type and there's no compile-time type checking.</span></span> <span data-ttu-id="84cad-128">如果您將模型宣告為 `DateTime` 類型，它就會變成強型別。</span><span class="sxs-lookup"><span data-stu-id="84cad-128">If you declare the model to be a `DateTime` type, it becomes strongly typed.</span></span>

<span data-ttu-id="84cad-129">第二行只是常值 HTML 標籤，會使用日期欄位&quot; 之前的日期範本來顯示 &quot;。</span><span class="sxs-lookup"><span data-stu-id="84cad-129">The second line is just literal HTML markup that displays &quot;Using Date Template&quot; before a date field.</span></span> <span data-ttu-id="84cad-130">您會暫時使用這一行來驗證此日期範本是否正在使用中。</span><span class="sxs-lookup"><span data-stu-id="84cad-130">You'll use this line temporarily to verify that this date template is being used.</span></span>

<span data-ttu-id="84cad-131">下一行是[Html. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper，會呈現文字方塊的 `input` 欄位。</span><span class="sxs-lookup"><span data-stu-id="84cad-131">The next line is an [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper that renders an `input` field that's a text box.</span></span> <span data-ttu-id="84cad-132">Helper 的第三個參數會使用匿名型別，將文字方塊的類別設定為 `datefield`，以及要 `date`的型別。</span><span class="sxs-lookup"><span data-stu-id="84cad-132">The third parameter for the helper uses an anonymous type to set the class for the text box to `datefield` and the type to `date`.</span></span> <span data-ttu-id="84cad-133">（因為 `class` 是中C#保留的，所以您必須使用 `@` 字元來將剖析器中C#的 `class` 屬性。）</span><span class="sxs-lookup"><span data-stu-id="84cad-133">(Because `class` is a reserved in C#, you need to use the `@` character to escape the `class` attribute in the C# parser.)</span></span>

<span data-ttu-id="84cad-134">`date` 類型是 HTML5 輸入類型，可讓 HTML5 感知瀏覽器呈現 HTML5 行事曆控制項。</span><span class="sxs-lookup"><span data-stu-id="84cad-134">The `date` type is an HTML5 input type that enables HTML5-aware browsers to render a HTML5 calendar control.</span></span> <span data-ttu-id="84cad-135">稍後您會加入一些 JavaScript，以使用 `datefield` 類別，將 jQuery datepicker 連結到 `Html.TextBox` 元素。</span><span class="sxs-lookup"><span data-stu-id="84cad-135">Later on you'll add some JavaScript to hook up the jQuery datepicker to the `Html.TextBox` element using the `datefield` class.</span></span>

<span data-ttu-id="84cad-136">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="84cad-136">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="84cad-137">您可以確認 [編輯] 視圖中的 [`ReleaseDate`] 屬性是使用 [編輯範本]，因為範本會使用 [`ReleaseDate` 文字] 輸入方塊前面的 [日期]&quot; 範本來顯示 &quot;，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="84cad-137">You can verify that the `ReleaseDate` property in the edit view is using the edit template because the template displays &quot;Using Date Template&quot; just before the `ReleaseDate` text input box, as shown in this image:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

<span data-ttu-id="84cad-138">在您的瀏覽器中，查看頁面的來源。</span><span class="sxs-lookup"><span data-stu-id="84cad-138">In your browser, view the source of the page.</span></span> <span data-ttu-id="84cad-139">（例如，以滑鼠右鍵按一下頁面，然後選取 [ **View source**]）。下列範例會顯示頁面的部分標記，其中說明轉譯的 HTML 中的 `class` 和 `type` 屬性。</span><span class="sxs-lookup"><span data-stu-id="84cad-139">(For example, right-click the page and select **View source**.) The following example shows some of the markup for the page, illustrating the `class` and `type` attributes in the rendered HTML.</span></span>

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

<span data-ttu-id="84cad-140">返回*Views\Shared\EditorTemplates\Date.cshtml*範本，並使用日期範本&quot; 標記移除 &quot;。</span><span class="sxs-lookup"><span data-stu-id="84cad-140">Return to the *Views\Shared\EditorTemplates\Date.cshtml* template and remove the &quot;Using Date Template&quot; markup.</span></span> <span data-ttu-id="84cad-141">現在完成的範本看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="84cad-141">Now the completed template looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a><span data-ttu-id="84cad-142">使用 NuGet 新增 jQuery UI Datepicker 快顯行事曆</span><span class="sxs-lookup"><span data-stu-id="84cad-142">Adding a jQuery UI Datepicker Popup Calendar using NuGet</span></span>

<span data-ttu-id="84cad-143">在本節中，您會將[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快顯行事曆新增至日期編輯範本。</span><span class="sxs-lookup"><span data-stu-id="84cad-143">In this section you'll add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to the date-edit template.</span></span> <span data-ttu-id="84cad-144">[JQUERY UI](http://jqueryui.com/)程式庫可支援動畫、先進的效果和可自訂的小工具。</span><span class="sxs-lookup"><span data-stu-id="84cad-144">The [jQuery UI](http://jqueryui.com/) library provides support for animation, advanced effects, and customizable widgets.</span></span> <span data-ttu-id="84cad-145">它建置於 jQuery JavaScript 程式庫之上。</span><span class="sxs-lookup"><span data-stu-id="84cad-145">It's built on top of the jQuery JavaScript library.</span></span> <span data-ttu-id="84cad-146">Datepicker 快顯行事曆可讓您輕鬆且自然地使用行事曆輸入日期，而不是輸入字串。</span><span class="sxs-lookup"><span data-stu-id="84cad-146">The datepicker popup calendar makes it easy and natural to enter dates using a calendar instead of entering a string.</span></span> <span data-ttu-id="84cad-147">快顯行事曆也會將使用者限制為合法日期，日期的一般文字輸入可讓您輸入類似 `2/33/1999` （二月33rd，1999），但[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快顯行事曆不會允許此作業。</span><span class="sxs-lookup"><span data-stu-id="84cad-147">The popup calendar also limits users to legal dates — ordinary text entry for a date would let you enter something like `2/33/1999` ( February 33rd, 1999), but the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar won't allow that.</span></span>

<span data-ttu-id="84cad-148">首先，您必須安裝 jQuery UI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="84cad-148">First, you have to install the jQuery UI libraries.</span></span> <span data-ttu-id="84cad-149">若要這麼做，您將使用 NuGet，這是包含在 SP1 版本的 Visual Studio 2010 和 Visual Web Developer 中的套件管理員。</span><span class="sxs-lookup"><span data-stu-id="84cad-149">To do that, you'll use NuGet, which is a package manager that's included in SP1 versions of Visual Studio 2010 and Visual Web Developer.</span></span>

<span data-ttu-id="84cad-150">在 Visual Web Developer 中，從 [**工具**] 功能表選取 [ **nuget 套件管理員**]，然後選取 [**管理 nuget 套件**]。</span><span class="sxs-lookup"><span data-stu-id="84cad-150">In Visual Web Developer, from the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

<span data-ttu-id="84cad-151">注意：如果 [**工具**] 功能表未顯示 [ **nuget 套件管理員**] 命令，您必須遵循 Nuget 網站的 [[安裝 nuget](http://docs.nuget.org/docs/start-here/installing-nuget) ] 頁面上的指示來安裝 nuget。</span><span class="sxs-lookup"><span data-stu-id="84cad-151">Note: If the **Tools** menu doesn't display the **NuGet Package Manager** command, you need to install NuGet by following the instructions on the [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) page of the NuGet website.</span></span>   
  
<span data-ttu-id="84cad-152">如果您使用 Visual Studio 而非 Visual Web Developer，請從 [**工具**] 功能表中選取 [ **NuGet 套件管理員**]，然後選取 [**新增程式庫套件參考**]。</span><span class="sxs-lookup"><span data-stu-id="84cad-152">If you're using Visual Studio instead of Visual Web Developer, from the **Tools** menu, select **NuGet Package Manager** and then select **Add Library Package Reference**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

<span data-ttu-id="84cad-153">在 [ **MVCMovie-管理 NuGet 封裝**] 對話方塊中，按一下左側的 [**線上**] 索引標籤，然後在 [搜尋] 方塊中輸入 &quot;jQuery. UI&quot;。</span><span class="sxs-lookup"><span data-stu-id="84cad-153">In the **MVCMovie - Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter &quot;jQuery.UI&quot; in the search box.</span></span> <span data-ttu-id="84cad-154">選取 [j**查詢 UI widget： Datepicker**]，然後選取 [**安裝**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84cad-154">Select j **Query UI Widgets:Datepicker**, then select the **Install** button.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

<span data-ttu-id="84cad-155">NuGet 會將 jQuery UI Core 和 jQuery UI 日期選擇器的這些偵錯工具版本和縮減版本新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="84cad-155">NuGet adds these debug versions and minified versions of jQuery UI Core and the jQuery UI date picker to your project:</span></span>

- <span data-ttu-id="84cad-156">*jquery. core .js*</span><span class="sxs-lookup"><span data-stu-id="84cad-156">*jquery.ui.core.js*</span></span>
- <span data-ttu-id="84cad-157">*jquery. core. min .js*</span><span class="sxs-lookup"><span data-stu-id="84cad-157">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="84cad-158">*jquery. ui. datepicker .js*</span><span class="sxs-lookup"><span data-stu-id="84cad-158">*jquery.ui.datepicker.js*</span></span>
- <span data-ttu-id="84cad-159">*jquery. datepicker. min .js*</span><span class="sxs-lookup"><span data-stu-id="84cad-159">*jquery.ui.datepicker.min.js*</span></span>

<span data-ttu-id="84cad-160">注意： debug 版本（沒有 *. min .js*副檔名的檔案）在進行調試時很有用，但在生產網站中，您只會包含縮減版本。</span><span class="sxs-lookup"><span data-stu-id="84cad-160">Note: The debug versions (the files without the *.min.js* extension) are useful for debugging, but in a production site, you'd include only the minified versions.</span></span>

<span data-ttu-id="84cad-161">若要實際使用 jQuery 日期選擇器，您需要建立可將行事曆 widget 連結至編輯範本的 jQuery 腳本。</span><span class="sxs-lookup"><span data-stu-id="84cad-161">To actually use the jQuery date picker, you need to create a jQuery script that will hook up the calendar widget to the edit template.</span></span> <span data-ttu-id="84cad-162">在**方案總管**中，以滑鼠右鍵按一下 [*腳本*] 資料夾，然後依序選取 [**加入**]、[**新增專案**] 和 [ **JScript**檔案]。</span><span class="sxs-lookup"><span data-stu-id="84cad-162">In **Solution Explorer**, right-click the *Scripts* folder and select **Add**, then **New Item**, and then **JScript File**.</span></span> <span data-ttu-id="84cad-163">將檔案命名為*DatePickerReady*。</span><span class="sxs-lookup"><span data-stu-id="84cad-163">Name the file *DatePickerReady.js*.</span></span>

<span data-ttu-id="84cad-164">將下列程式碼新增至*DatePickerReady*檔案：</span><span class="sxs-lookup"><span data-stu-id="84cad-164">Add the following code to the *DatePickerReady.js* file:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

<span data-ttu-id="84cad-165">如果您不熟悉 jQuery，以下是此功能的簡短說明：第一行是 &quot;jQuery ready&quot; 函式，當頁面中的所有 DOM 元素都已載入時，就會呼叫此函式。</span><span class="sxs-lookup"><span data-stu-id="84cad-165">If you're not familiar with jQuery, here's a brief explanation of what this does: the first line is the &quot;jQuery ready&quot; function, which is called when all the DOM elements in a page have loaded.</span></span> <span data-ttu-id="84cad-166">第二行會選取所有具有類別名稱 `datefield`的 DOM 元素，然後針對每個專案叫用 `datepicker` 函式。</span><span class="sxs-lookup"><span data-stu-id="84cad-166">The second line selects all DOM elements that have the class name `datefield`, then invokes the `datepicker` function for each of them.</span></span> <span data-ttu-id="84cad-167">（請記住，您稍早在本教學課程中已將 `datefield` 類別新增至*Views\Shared\EditorTemplates\Date.cshtml*範本）。</span><span class="sxs-lookup"><span data-stu-id="84cad-167">(Remember that you added the `datefield` class to the *Views\Shared\EditorTemplates\Date.cshtml* template earlier in the tutorial.)</span></span>

<span data-ttu-id="84cad-168">接下來，開啟*Views\Shared\\_Layout. cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="84cad-168">Next, open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="84cad-169">您需要新增下列檔案的參考，這些檔案都是必要的，以便您可以使用日期選擇器：</span><span class="sxs-lookup"><span data-stu-id="84cad-169">You need to add references to the following files, which are all required so that you can use the date picker:</span></span>

- <span data-ttu-id="84cad-170">*Content/主題/base/jquery. .css*</span><span class="sxs-lookup"><span data-stu-id="84cad-170">*Content/themes/base/jquery.ui.core.css*</span></span>
- <span data-ttu-id="84cad-171">*Content/主題/base/jquery. datepicker .css*</span><span class="sxs-lookup"><span data-stu-id="84cad-171">*Content/themes/base/jquery.ui.datepicker.css*</span></span>
- <span data-ttu-id="84cad-172">*Content/主題/base/jquery. ui. css*</span><span class="sxs-lookup"><span data-stu-id="84cad-172">*Content/themes/base/jquery.ui.theme.css*</span></span>
- <span data-ttu-id="84cad-173">*jquery. core. min .js*</span><span class="sxs-lookup"><span data-stu-id="84cad-173">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="84cad-174">*jquery. datepicker. min .js*</span><span class="sxs-lookup"><span data-stu-id="84cad-174">*jquery.ui.datepicker.min.js*</span></span>
- <span data-ttu-id="84cad-175">*DatePickerReady .js*</span><span class="sxs-lookup"><span data-stu-id="84cad-175">*DatePickerReady.js*</span></span>

<span data-ttu-id="84cad-176">下列範例會顯示您應該在*Views\Shared\\_Layout. cshtml*檔案的 `head` 專案底部加入的實際程式碼。</span><span class="sxs-lookup"><span data-stu-id="84cad-176">The following example shows the actual code that you should add at the bottom of the `head` element in the *Views\Shared\\_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

<span data-ttu-id="84cad-177">完整的 `head` 區段如下所示：</span><span class="sxs-lookup"><span data-stu-id="84cad-177">The complete `head` section is shown here:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

<span data-ttu-id="84cad-178">[URL 內容 helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法會將資源路徑轉換為絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="84cad-178">The [URL content helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) method converts the resource path to an absolute path.</span></span> <span data-ttu-id="84cad-179">當應用程式在 IIS 上執行時，您必須使用 `@URL.Content` 來正確參考這些資源。</span><span class="sxs-lookup"><span data-stu-id="84cad-179">You must use `@URL.Content` to correctly reference these resources when the application is running on IIS.</span></span>

<span data-ttu-id="84cad-180">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="84cad-180">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="84cad-181">選取 [編輯] 連結，然後將插入點放入 [ **ReleaseDate** ] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="84cad-181">Select an edit link, then put the insertion point into the **ReleaseDate** field.</span></span> <span data-ttu-id="84cad-182">隨即顯示 jQuery UI 快顯行事曆。</span><span class="sxs-lookup"><span data-stu-id="84cad-182">The jQuery UI popup calendar is displayed.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

<span data-ttu-id="84cad-183">就像大部分的 jQuery 控制項一樣，datepicker 可讓您廣泛地進行自訂。</span><span class="sxs-lookup"><span data-stu-id="84cad-183">Like most jQuery controls, the datepicker lets you customize it extensively.</span></span> <span data-ttu-id="84cad-184">如需相關資訊，請參閱[JQUERY ui](http://learn.jquery.com/jquery-ui/getting-started/)網站上的[視覺化自訂：設計 jquery ui 主題](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)。</span><span class="sxs-lookup"><span data-stu-id="84cad-184">For information, see [Visual Customization: Designing a jQuery UI theme](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) on the [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) site.</span></span>

### <a name="supporting-the-html5-date-input-control"></a><span data-ttu-id="84cad-185">支援 HTML5 日期輸入控制項</span><span class="sxs-lookup"><span data-stu-id="84cad-185">Supporting the HTML5 Date Input Control</span></span>

<span data-ttu-id="84cad-186">當瀏覽器支援 HTML5 時，您會想要使用原生 HTML5 輸入（例如 `date` input 元素），而不使用 jQuery UI 行事曆。</span><span class="sxs-lookup"><span data-stu-id="84cad-186">As more browsers support HTML5, you'll want to use the native HTML5 input, such as the `date` input element, and not use the jQuery UI calendar.</span></span> <span data-ttu-id="84cad-187">如果瀏覽器支援，您可以在應用程式中新增邏輯，以自動使用 HTML5 控制項。</span><span class="sxs-lookup"><span data-stu-id="84cad-187">You can add logic to your application to automatically use HTML5 controls if the browser supports them.</span></span> <span data-ttu-id="84cad-188">若要這麼做，請將*DatePickerReady*的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="84cad-188">To do this, replace the contents of the *DatePickerReady.js* file with the following:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

<span data-ttu-id="84cad-189">此腳本的第一行會使用 Modernizr 來驗證是否支援 HTML5 日期輸入。</span><span class="sxs-lookup"><span data-stu-id="84cad-189">The first line of this script uses Modernizr to verify that HTML5 date input is supported.</span></span> <span data-ttu-id="84cad-190">如果不支援，jQuery UI 日期選擇器會改為連結。</span><span class="sxs-lookup"><span data-stu-id="84cad-190">If it's not supported, the jQuery UI date picker is hooked up instead.</span></span> <span data-ttu-id="84cad-191">（[Modernizr](http://www.modernizr.com/docs/)是一種開放原始碼 JavaScript 程式庫，可偵測 HTML5 和 CSS3 原生執行的可用性。</span><span class="sxs-lookup"><span data-stu-id="84cad-191">([Modernizr](http://www.modernizr.com/docs/) is an open-source JavaScript library that detects the availability of native implementations of HTML5 and CSS3.</span></span> <span data-ttu-id="84cad-192">Modernizr 會包含在您所建立的任何新 ASP.NET MVC 專案中）。</span><span class="sxs-lookup"><span data-stu-id="84cad-192">Modernizr is included in any new ASP.NET MVC projects that you create.)</span></span>

<span data-ttu-id="84cad-193">進行這項變更之後，您可以使用支援 HTML5 的瀏覽器來測試它，例如 Opera 11。</span><span class="sxs-lookup"><span data-stu-id="84cad-193">After you've made this change, you can test it by using a browser that supports HTML5, such as Opera 11.</span></span> <span data-ttu-id="84cad-194">使用與 HTML5 相容的瀏覽器來執行應用程式，並編輯電影專案。</span><span class="sxs-lookup"><span data-stu-id="84cad-194">Run the application using an HTML5-compatible browser and edit a movie entry.</span></span> <span data-ttu-id="84cad-195">使用 HTML5 日期控制項，而不是 jQuery UI 快顯行事曆：</span><span class="sxs-lookup"><span data-stu-id="84cad-195">The HTML5 date control is used instead of the jQuery UI popup calendar:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

<span data-ttu-id="84cad-196">因為新版本的瀏覽器會以累加方式來執行 HTML5，所以現在最好的方法是將程式碼新增至您的網站，以容納各種 HTML5 支援。</span><span class="sxs-lookup"><span data-stu-id="84cad-196">Because new versions of browsers are implementing HTML5 incrementally, a good approach for now is to add code to your website that accommodates a wide variety of HTML5 support.</span></span> <span data-ttu-id="84cad-197">例如，以下顯示更健全的*DatePickerReady*腳本，可讓您的網站支援僅部分支援 HTML5 日期控制項的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="84cad-197">For example, a more robust *DatePickerReady.js* script is shown below that lets your site support browsers that only partially support the HTML5 date control.</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

<span data-ttu-id="84cad-198">此腳本會選取不完全支援 HTML5 日期控制項 `date` 類型的 HTML5 `input` 元素。</span><span class="sxs-lookup"><span data-stu-id="84cad-198">This script selects HTML5 `input` elements of type `date` that don't fully support the HTML5 date control.</span></span> <span data-ttu-id="84cad-199">針對這些元素，它會連結 jQuery UI 快顯行事曆，然後將 `type` 屬性從 `date` 變更為 `text`。</span><span class="sxs-lookup"><span data-stu-id="84cad-199">For those elements, it hooks up the jQuery UI popup calendar and then changes the `type` attribute from `date` to `text`.</span></span> <span data-ttu-id="84cad-200">藉由將 `type` 屬性從 `date` 變更為 `text`，就會消除部分 HTML5 日期支援。</span><span class="sxs-lookup"><span data-stu-id="84cad-200">By changing the `type` attribute from `date` to `text`, partial HTML5 date support is eliminated.</span></span> <span data-ttu-id="84cad-201">您可以在[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)中找到更健全的*DatePickerReady*腳本。</span><span class="sxs-lookup"><span data-stu-id="84cad-201">An even more robust *DatePickerReady.js* script can be found at [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).</span></span>

### <a name="adding-nullable-dates-to-the-templates"></a><span data-ttu-id="84cad-202">將可為 Null 的日期加入至範本</span><span class="sxs-lookup"><span data-stu-id="84cad-202">Adding Nullable Dates to the Templates</span></span>

<span data-ttu-id="84cad-203">如果您使用其中一個現有的日期範本並傳遞 null 日期，您會收到執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="84cad-203">If you use one of the existing date templates and pass a null date, you'll get a run-time error.</span></span> <span data-ttu-id="84cad-204">為了讓日期範本更穩固，您會將其變更為處理 null 值。</span><span class="sxs-lookup"><span data-stu-id="84cad-204">To make the date templates more robust, you'll change them to handle null values.</span></span> <span data-ttu-id="84cad-205">若要支援可為 null 的日期，請將*Views\Shared\DisplayTemplates\DateTime.cshtml*中的程式碼變更為下列內容：</span><span class="sxs-lookup"><span data-stu-id="84cad-205">To support nullable dates, change the code in the *Views\Shared\DisplayTemplates\DateTime.cshtml* to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

<span data-ttu-id="84cad-206">當模型為**null**時，此程式碼會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="84cad-206">The code returns an empty string when the model is **null**.</span></span>

<span data-ttu-id="84cad-207">將*Views\Shared\EditorTemplates\Date.cshtml*檔案中的程式碼變更為下列內容：</span><span class="sxs-lookup"><span data-stu-id="84cad-207">Change the code in the *Views\Shared\EditorTemplates\Date.cshtml* file to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

<span data-ttu-id="84cad-208">當此程式碼執行時，如果模型不是 null，則會使用模型的 `DateTime` 值。</span><span class="sxs-lookup"><span data-stu-id="84cad-208">When this code runs, if the model is not null, the model's `DateTime` value is used.</span></span> <span data-ttu-id="84cad-209">如果模型是 null，則會改用目前的日期。</span><span class="sxs-lookup"><span data-stu-id="84cad-209">If the model is null, the current date is used instead.</span></span>

### <a name="wrapup"></a><span data-ttu-id="84cad-210">Wrapup</span><span class="sxs-lookup"><span data-stu-id="84cad-210">Wrapup</span></span>

<span data-ttu-id="84cad-211">本教學課程涵蓋 ASP.NET 樣板化 helper 的基本概念，並示範如何在 ASP.NET MVC 應用程式中使用 jQuery UI datepicker 快顯行事曆。</span><span class="sxs-lookup"><span data-stu-id="84cad-211">This tutorial has covered the basics of ASP.NET templated helpers and shows you how to use the jQuery UI datepicker popup calendar in an ASP.NET MVC application.</span></span> <span data-ttu-id="84cad-212">如需詳細資訊，請嘗試下列資源：</span><span class="sxs-lookup"><span data-stu-id="84cad-212">For more information, try these resources:</span></span>

- <span data-ttu-id="84cad-213">如需當地語系化的詳細資訊，請參閱 Rajeesh 的 blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。</span><span class="sxs-lookup"><span data-stu-id="84cad-213">For information on localization, see Rajeesh's blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).</span></span>
- <span data-ttu-id="84cad-214">如需 jQuery UI 的詳細資訊，請參閱[JQUERY ui](http://docs.jquery.com/UI)。</span><span class="sxs-lookup"><span data-stu-id="84cad-214">For information about jQuery UI, see [jQuery UI](http://docs.jquery.com/UI).</span></span>
- <span data-ttu-id="84cad-215">如需如何將 datepicker 控制項當地語系化的詳細資訊，請參閱[UI/datepicker/當地語系化](http://docs.jquery.com/UI/Datepicker/Localization)。</span><span class="sxs-lookup"><span data-stu-id="84cad-215">For information about how to localize the datepicker control, see [UI/Datepicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).</span></span>
- <span data-ttu-id="84cad-216">如需有關 ASP.NET MVC 範本的詳細資訊，請參閱[ASP.NET mvc 2 範本](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)上的 Brad Wilson 的 blog 系列。</span><span class="sxs-lookup"><span data-stu-id="84cad-216">For more information about the ASP.NET MVC templates, see Brad Wilson's blog series on [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="84cad-217">雖然此系列是針對 ASP.NET MVC 2 而撰寫的，但該材料仍然適用于目前版本的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="84cad-217">Although the series was written for ASP.NET MVC 2, the material still applies for the current version of ASP.NET MVC.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="84cad-218">[[上一步]](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="84cad-218">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
