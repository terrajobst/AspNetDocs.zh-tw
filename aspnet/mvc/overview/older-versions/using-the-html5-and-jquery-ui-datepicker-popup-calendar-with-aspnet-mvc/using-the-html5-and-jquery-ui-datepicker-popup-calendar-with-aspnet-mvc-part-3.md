---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第3部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何在 ASP.NET MV 中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457891"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="048ec-103">搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第3部分</span><span class="sxs-lookup"><span data-stu-id="048ec-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>

<span data-ttu-id="048ec-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="048ec-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="048ec-105">本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。</span><span class="sxs-lookup"><span data-stu-id="048ec-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="working-with-complex-types"></a><span data-ttu-id="048ec-106">使用複雜類型</span><span class="sxs-lookup"><span data-stu-id="048ec-106">Working with Complex Types</span></span>

<span data-ttu-id="048ec-107">在本節中，您將建立一個網址類別別，並瞭解如何建立範本來顯示它。</span><span class="sxs-lookup"><span data-stu-id="048ec-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="048ec-108">在 [*模型*] 資料夾中，建立名為*Person.cs*的新類別檔案，您會在其中放置兩個類型： [`Person` 類別] 和 [`Address` 類別]。</span><span class="sxs-lookup"><span data-stu-id="048ec-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="048ec-109">`Person` 類別將包含以 `Address`類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="048ec-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="048ec-110">`Address` 類型是複雜類型，這表示它不是其中一個內建類型，例如 `int`、`string`或 `double`。</span><span class="sxs-lookup"><span data-stu-id="048ec-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="048ec-111">相反地，它有數個屬性。</span><span class="sxs-lookup"><span data-stu-id="048ec-111">Instead, it has several properties.</span></span> <span data-ttu-id="048ec-112">新類別的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="048ec-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="048ec-113">在 `Movie` 控制器中，新增下列 `PersonDetail` 動作以顯示 person 實例：</span><span class="sxs-lookup"><span data-stu-id="048ec-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="048ec-114">然後將下列程式碼新增至 `Movie` 控制器，以將一些範例資料填入 `Person` 模型：</span><span class="sxs-lookup"><span data-stu-id="048ec-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="048ec-115">開啟*Views\Movies\PersonDetail.cshtml*檔案，並為 `PersonDetail` view 新增下列標記。</span><span class="sxs-lookup"><span data-stu-id="048ec-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="048ec-116">按 Ctrl + F5 執行應用程式，並流覽至 [*電影/PersonDetail*]。</span><span class="sxs-lookup"><span data-stu-id="048ec-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="048ec-117">[`PersonDetail`] 視圖並未包含 `Address` 複雜類型，如您在此螢幕擷取畫面中所見。</span><span class="sxs-lookup"><span data-stu-id="048ec-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="048ec-118">（不會顯示任何位址）。</span><span class="sxs-lookup"><span data-stu-id="048ec-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="048ec-119">不會顯示 `Address` 的模型資料，因為它是複雜型別。</span><span class="sxs-lookup"><span data-stu-id="048ec-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="048ec-120">若要顯示位址資訊，請再次開啟*Views\Movies\PersonDetail.cshtml*檔案，並新增下列標記。</span><span class="sxs-lookup"><span data-stu-id="048ec-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="048ec-121">[`PersonDetail` now] 視圖的完整標記看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="048ec-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="048ec-122">再次執行應用程式，並顯示 [`PersonDetail`] 視圖。</span><span class="sxs-lookup"><span data-stu-id="048ec-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="048ec-123">現在會顯示位址資訊：</span><span class="sxs-lookup"><span data-stu-id="048ec-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="048ec-124">建立複雜類型的範本</span><span class="sxs-lookup"><span data-stu-id="048ec-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="048ec-125">在本節中，您將會建立用來轉譯 `Address` 複雜類型的範本。</span><span class="sxs-lookup"><span data-stu-id="048ec-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="048ec-126">當您建立 `Address` 類型的範本時，ASP.NET MVC 可以自動使用它來格式化應用程式中任何位置的位址模型。</span><span class="sxs-lookup"><span data-stu-id="048ec-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="048ec-127">如此一來，您就可以從應用程式中的單一位置控制 `Address` 類型的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="048ec-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="048ec-128">在*Views\Shared\DisplayTemplates*資料夾中，建立名為**Address**的強型別部分視圖：</span><span class="sxs-lookup"><span data-stu-id="048ec-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="048ec-129">按一下 **[新增]** ，然後開啟新的*Views\Shared\DisplayTemplates\Address.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="048ec-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="048ec-130">新的視圖包含下列產生的標記：</span><span class="sxs-lookup"><span data-stu-id="048ec-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="048ec-131">執行應用程式，並顯示 [`PersonDetail`] 視圖。</span><span class="sxs-lookup"><span data-stu-id="048ec-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="048ec-132">這次，您剛建立的 `Address` 範本會用來顯示 `Address` 複雜類型，因此顯示如下所示：</span><span class="sxs-lookup"><span data-stu-id="048ec-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="048ec-133">摘要：指定模型顯示格式和範本的方式</span><span class="sxs-lookup"><span data-stu-id="048ec-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="048ec-134">您已看到，您可以使用下列方法來指定模型屬性的格式或範本：</span><span class="sxs-lookup"><span data-stu-id="048ec-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="048ec-135">將 `DisplayFormat` 屬性套用至模型中的屬性。</span><span class="sxs-lookup"><span data-stu-id="048ec-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="048ec-136">例如，下列程式碼會在沒有時間的情況下顯示日期：</span><span class="sxs-lookup"><span data-stu-id="048ec-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="048ec-137">將[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性套用至模型中的屬性，並指定資料類型。</span><span class="sxs-lookup"><span data-stu-id="048ec-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="048ec-138">例如，下列程式碼會在沒有時間的情況下顯示日期。</span><span class="sxs-lookup"><span data-stu-id="048ec-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="048ec-139">如果應用程式在*Views\Shared\DisplayTemplates*資料夾或*Views\Movies\DisplayTemplates*資料夾中包含*date. cshtml*範本，則會使用該範本來呈現 `DateTime` 屬性。</span><span class="sxs-lookup"><span data-stu-id="048ec-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="048ec-140">否則，內建的 ASP.NET 範本化系統會將屬性顯示為日期。</span><span class="sxs-lookup"><span data-stu-id="048ec-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="048ec-141">建立*Views\Shared\DisplayTemplates*資料夾或*Views\Movies\DisplayTemplates*資料夾中的顯示範本，其名稱符合您想要格式化的資料類型。</span><span class="sxs-lookup"><span data-stu-id="048ec-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="048ec-142">例如，您看到*Views\Shared\DisplayTemplates\DateTime.cshtml*是用來呈現模型中 `DateTime` 屬性，而不需要將屬性加入至模型，也不需要將任何標記加入至 Views。</span><span class="sxs-lookup"><span data-stu-id="048ec-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="048ec-143">在模型上使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性來指定要顯示模型屬性的範本。</span><span class="sxs-lookup"><span data-stu-id="048ec-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="048ec-144">在視圖中，將顯示範本名稱明確新增至[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)呼叫。</span><span class="sxs-lookup"><span data-stu-id="048ec-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="048ec-145">您所使用的方法取決於您需要在應用程式中執行的動作。</span><span class="sxs-lookup"><span data-stu-id="048ec-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="048ec-146">混用這些方法，以確切取得您所需的格式類型並不常見。</span><span class="sxs-lookup"><span data-stu-id="048ec-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="048ec-147">在下一節中，您將會稍微切換齒輪，並從自訂資料的顯示方式移動，以自訂其輸入方式。</span><span class="sxs-lookup"><span data-stu-id="048ec-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="048ec-148">您會將 jQuery datepicker 連結至應用程式中的編輯檢視，以提供更巧妙的方式來指定日期。</span><span class="sxs-lookup"><span data-stu-id="048ec-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="048ec-149">[上一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [下一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="048ec-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
