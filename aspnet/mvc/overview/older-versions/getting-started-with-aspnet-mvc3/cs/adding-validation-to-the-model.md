---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: 將驗證新增至模型（C#） |Microsoft Docs
author: Rick-Anderson
description: 建立控制器
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 19d86dc0df931a9d135e46209559892b77626cf6
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457712"
---
# <a name="adding-validation-to-the-model-c"></a><span data-ttu-id="cc909-103">將驗證新增至模型 (C#)</span><span class="sxs-lookup"><span data-stu-id="cc909-103">Adding Validation to the Model (C#)</span></span>

<span data-ttu-id="cc909-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cc909-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="cc909-105">本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="cc909-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="cc909-106">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="cc909-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="cc909-107">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="cc909-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="cc909-108">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="cc909-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="cc909-109">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="cc909-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="cc909-110">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="cc909-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="cc909-111">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="cc909-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="cc909-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="cc909-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="cc909-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="cc909-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="cc909-114">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="cc909-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="cc909-115">本主題提供具有C#原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="cc909-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="cc909-116">[下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="cc909-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="cc909-117">如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="cc909-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="cc909-118">在本節中，您會將驗證邏輯新增至 `Movie` 模型，而且您將確保在使用者嘗試使用應用程式建立或編輯電影時，會強制執行驗證規則。</span><span class="sxs-lookup"><span data-stu-id="cc909-118">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user attempts to create or edit a movie using the application.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="cc909-119">讓事情晾乾</span><span class="sxs-lookup"><span data-stu-id="cc909-119">Keeping Things DRY</span></span>

<span data-ttu-id="cc909-120">ASP.NET MVC 的其中一個核心設計原則是試（「不重複原則」）。</span><span class="sxs-lookup"><span data-stu-id="cc909-120">One of the core design tenets of ASP.NET MVC is DRY ("Don't Repeat Yourself").</span></span> <span data-ttu-id="cc909-121">ASP.NET MVC 鼓勵您只指定一次功能或行為，然後讓它反映在應用程式中的所有位置。</span><span class="sxs-lookup"><span data-stu-id="cc909-121">ASP.NET MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an application.</span></span> <span data-ttu-id="cc909-122">這可減少您需要撰寫的程式碼數量，讓您撰寫的程式碼更容易維護。</span><span class="sxs-lookup"><span data-stu-id="cc909-122">This reduces the amount of code you need to write and makes the code you do write much easier to maintain.</span></span>

<span data-ttu-id="cc909-123">ASP.NET MVC 和 Entity Framework Code First 所提供的驗證支援，是實際運作原則的絕佳範例。</span><span class="sxs-lookup"><span data-stu-id="cc909-123">The validation support provided by ASP.NET MVC and Entity Framework Code First is a great example of the DRY principle in action.</span></span> <span data-ttu-id="cc909-124">您可以在一個位置以宣告方式指定驗證規則（在模型類別中），然後在應用程式中的任何位置強制執行這些規則。</span><span class="sxs-lookup"><span data-stu-id="cc909-124">You can declaratively specify validation rules in one place (in the model class) and then those rules are enforced everywhere in the application.</span></span>

<span data-ttu-id="cc909-125">讓我們看看如何在電影應用程式中利用這項驗證支援。</span><span class="sxs-lookup"><span data-stu-id="cc909-125">Let's look at how you can take advantage of this validation support in the movie application.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="cc909-126">將驗證規則新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="cc909-126">Adding Validation Rules to the Movie Model</span></span>

<span data-ttu-id="cc909-127">首先，將一些驗證邏輯新增至 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="cc909-127">You'll begin by adding some validation logic to the `Movie` class.</span></span>

<span data-ttu-id="cc909-128">開啟 *Movie.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc909-128">Open the *Movie.cs* file.</span></span> <span data-ttu-id="cc909-129">在檔案的頂端新增參考[`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間的 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="cc909-129">Add a `using` statement at the top of the file that references the [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

<span data-ttu-id="cc909-130">命名空間是 .NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="cc909-130">The namespace is part of the .NET Framework.</span></span> <span data-ttu-id="cc909-131">它提供了一組內建的驗證屬性，可讓您以宣告方式套用至任何類別或屬性。</span><span class="sxs-lookup"><span data-stu-id="cc909-131">It provides a built-in set of validation attributes that you can apply declaratively to any class or property.</span></span>

<span data-ttu-id="cc909-132">現在更新 `Movie` 類別，以利用內建的[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="cc909-132">Now update the `Movie` class to take advantage of the built-in [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), and [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) validation attributes.</span></span> <span data-ttu-id="cc909-133">使用下列程式碼作為套用屬性的範例。</span><span class="sxs-lookup"><span data-stu-id="cc909-133">Use the following code as an example of where to apply the attributes.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

<span data-ttu-id="cc909-134">驗證屬性會指定您想要強制執行模型屬性套用的行為。</span><span class="sxs-lookup"><span data-stu-id="cc909-134">The validation attributes specify behavior that you want to enforce on the model properties they are applied to.</span></span> <span data-ttu-id="cc909-135">`Required` 屬性指出屬性必須具有值;在此範例中，電影必須有 `Title`、`ReleaseDate`、`Genre`和 `Price` 屬性的值，才能有效。</span><span class="sxs-lookup"><span data-stu-id="cc909-135">The `Required` attribute indicates that a property must have a value; in this sample, a movie has to have values for the `Title`, `ReleaseDate`, `Genre`, and `Price` properties in order to be valid.</span></span> <span data-ttu-id="cc909-136">`Range` 屬性會將值限制在指定的範圍內。</span><span class="sxs-lookup"><span data-stu-id="cc909-136">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="cc909-137">`StringLength` 屬性可讓您設定字串屬性的最大長度，並選擇性設定其最小長度。</span><span class="sxs-lookup"><span data-stu-id="cc909-137">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span>

<span data-ttu-id="cc909-138">Code First 可確保在應用程式將變更儲存到資料庫之前，會強制執行您在模型類別上指定的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="cc909-138">Code First ensures that the validation rules you specify on a model class are enforced before the application saves changes in the database.</span></span> <span data-ttu-id="cc909-139">例如，下列程式碼會在呼叫 `SaveChanges` 方法時擲回例外狀況，因為遺漏了數個必要的 `Movie` 屬性值，而且價格為零（超出有效範圍）。</span><span class="sxs-lookup"><span data-stu-id="cc909-139">For example, the code below will throw an exception when the `SaveChanges` method is called, because several required `Movie` property values are missing and the price is zero (which is out of the valid range).</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

<span data-ttu-id="cc909-140">由 .NET Framework 自動強制執行驗證規則有助於讓應用程式更穩固。</span><span class="sxs-lookup"><span data-stu-id="cc909-140">Having validation rules automatically enforced by the .NET Framework helps make your application more robust.</span></span> <span data-ttu-id="cc909-141">它也確保您不會忘記要驗證某些項目，不小心讓不正確的資料進入資料庫。</span><span class="sxs-lookup"><span data-stu-id="cc909-141">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

<span data-ttu-id="cc909-142">以下是已更新之*Movie.cs*檔案的完整程式代碼清單：</span><span class="sxs-lookup"><span data-stu-id="cc909-142">Here's a complete code listing for the updated *Movie.cs* file:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a><span data-ttu-id="cc909-143">ASP.NET MVC 中的驗證錯誤 UI</span><span class="sxs-lookup"><span data-stu-id="cc909-143">Validation Error UI in ASP.NET MVC</span></span>

<span data-ttu-id="cc909-144">重新執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="cc909-144">Re-run the application and navigate to the */Movies* URL.</span></span>

<span data-ttu-id="cc909-145">按一下 [**建立電影**] 連結以新增電影。</span><span class="sxs-lookup"><span data-stu-id="cc909-145">Click the **Create Movie** link to add a new movie.</span></span> <span data-ttu-id="cc909-146">在表單中填寫一些不正確值，然後按一下 [**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc909-146">Fill out the form with some invalid values and then click the **Create** button.</span></span>

<span data-ttu-id="cc909-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cc909-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span></span>

<span data-ttu-id="cc909-148">請注意表單如何自動使用背景色彩來反白顯示包含無效資料的文字方塊，並且在每個文字旁發出適當的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="cc909-148">Notice how the form has automatically used a background color to highlight the text boxes that contain invalid data and has emitted an appropriate validation error message next to each one.</span></span> <span data-ttu-id="cc909-149">錯誤訊息符合您在批註 `Movie` 類別時所指定的錯誤字串。</span><span class="sxs-lookup"><span data-stu-id="cc909-149">The error messages match the error strings you specified when you annotated the `Movie` class.</span></span> <span data-ttu-id="cc909-150">用戶端（使用 JavaScript）和伺服器端（如果使用者已停用 JavaScript）都會強制執行錯誤。</span><span class="sxs-lookup"><span data-stu-id="cc909-150">The errors are enforced both client-side (using JavaScript) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="cc909-151">真正的好處是，您不需要在 `MoviesController` 類別或*建立. cshtml*視圖中變更一行程式碼，就能啟用此驗證 UI。</span><span class="sxs-lookup"><span data-stu-id="cc909-151">A real benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="cc909-152">您稍早在本教學課程中建立的控制器和視圖，會自動挑選您使用 `Movie` 模型類別上的屬性所指定的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="cc909-152">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified using attributes on the `Movie` model class.</span></span>

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a><span data-ttu-id="cc909-153">如何在 Create View 和 Create Action 方法中進行驗證</span><span class="sxs-lookup"><span data-stu-id="cc909-153">How Validation Occurs in the Create View and Create Action Method</span></span>

<span data-ttu-id="cc909-154">您可能奇怪如何在不更新控制器或檢視程式碼的狀況下產生驗證 UI。</span><span class="sxs-lookup"><span data-stu-id="cc909-154">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="cc909-155">下一個清單會顯示 `MovieController` 類別中的 `Create` 方法看起來如何。</span><span class="sxs-lookup"><span data-stu-id="cc909-155">The next listing shows what the `Create` methods in the `MovieController` class look like.</span></span> <span data-ttu-id="cc909-156">它們與您稍早在本教學課程中建立它們的方式不一樣。</span><span class="sxs-lookup"><span data-stu-id="cc909-156">They're unchanged from how you created them earlier in this tutorial.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

<span data-ttu-id="cc909-157">第一個動作方法會顯示初始的建立表單。</span><span class="sxs-lookup"><span data-stu-id="cc909-157">The first action method displays the initial Create form.</span></span> <span data-ttu-id="cc909-158">第二個處理表單張貼。</span><span class="sxs-lookup"><span data-stu-id="cc909-158">The second handles the form post.</span></span> <span data-ttu-id="cc909-159">第二個 `Create` 方法會呼叫 `ModelState.IsValid`，以檢查電影是否有任何驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="cc909-159">The second `Create` method calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="cc909-160">呼叫此方法會評估已套用至物件的所有驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="cc909-160">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="cc909-161">如果物件有驗證錯誤，`Create` 方法就會重新出現表單。</span><span class="sxs-lookup"><span data-stu-id="cc909-161">If the object has validation errors, the `Create` method redisplays the form.</span></span> <span data-ttu-id="cc909-162">如果沒有任何錯誤，方法即會將新的電影儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="cc909-162">If there are no errors, the method saves the new movie in the database.</span></span>

<span data-ttu-id="cc909-163">以下是您稍早在本教學課程中 scaffold 的*建立. cshtml*視圖範本。</span><span class="sxs-lookup"><span data-stu-id="cc909-163">Below is the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="cc909-164">上述動作方法會使用它來顯示初始表單，以及在發生錯誤時重新顯示它。</span><span class="sxs-lookup"><span data-stu-id="cc909-164">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

<span data-ttu-id="cc909-165">請注意程式碼如何使用 `Html.EditorFor` helper 來輸出每個 `Movie` 屬性的 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="cc909-165">Notice how the code uses an `Html.EditorFor` helper to output the `<input>` element for each `Movie` property.</span></span> <span data-ttu-id="cc909-166">在此協助程式旁呼叫 `Html.ValidationMessageFor` helper 方法。</span><span class="sxs-lookup"><span data-stu-id="cc909-166">Next to this helper is a call to the `Html.ValidationMessageFor` helper method.</span></span> <span data-ttu-id="cc909-167">這兩個 helper 方法會使用由控制器傳遞至視圖的模型物件（在此案例中為 `Movie` 物件）。</span><span class="sxs-lookup"><span data-stu-id="cc909-167">These two helper methods work with the model object that's passed by the controller to the view (in this case, a `Movie` object).</span></span> <span data-ttu-id="cc909-168">它們會自動尋找在模型上指定的驗證屬性，並適當地顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="cc909-168">They automatically look for validation attributes specified on the model and display error messages as appropriate.</span></span>

<span data-ttu-id="cc909-169">這種方法的好處是，控制器或建立視圖範本都無法得知所強制執行的實際驗證規則，或顯示的特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="cc909-169">What's really nice about this approach is that neither the controller nor the Create view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="cc909-170">驗證規則和錯誤字串只在 `Movie` 類別中指定。</span><span class="sxs-lookup"><span data-stu-id="cc909-170">The validation rules and the error strings are specified only in the `Movie` class.</span></span>

<span data-ttu-id="cc909-171">如果您稍後想要變更驗證邏輯，您可以在一個地方執行此動作。</span><span class="sxs-lookup"><span data-stu-id="cc909-171">If you want to change the validation logic later, you can do so in exactly one place.</span></span> <span data-ttu-id="cc909-172">您不必擔心應用程式的不同部分會與規則強制執行的方式不一致，所有的驗證邏輯都是在同一個地方定義，用於所有位置。</span><span class="sxs-lookup"><span data-stu-id="cc909-172">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="cc909-173">這會讓程式碼非常整齊乾淨，容易維護及發展。</span><span class="sxs-lookup"><span data-stu-id="cc909-173">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="cc909-174">這表示您會完全接受 DRY 原則。</span><span class="sxs-lookup"><span data-stu-id="cc909-174">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="adding-formatting-to-the-movie-model"></a><span data-ttu-id="cc909-175">將格式新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="cc909-175">Adding Formatting to the Movie Model</span></span>

<span data-ttu-id="cc909-176">開啟 *Movie.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc909-176">Open the *Movie.cs* file.</span></span> <span data-ttu-id="cc909-177">除了內建的驗證屬性集之外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間還會提供格式屬性。</span><span class="sxs-lookup"><span data-stu-id="cc909-177">The [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="cc909-178">您會將[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性和[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)列舉值套用至發行日期和價格欄位。</span><span class="sxs-lookup"><span data-stu-id="cc909-178">You'll apply the [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute and a [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="cc909-179">下列程式碼顯示具有適當[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性的 `ReleaseDate` 和 `Price` 屬性。</span><span class="sxs-lookup"><span data-stu-id="cc909-179">The following code shows the `ReleaseDate` and `Price` properties with the appropriate [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

<span data-ttu-id="cc909-180">或者，您可以明確地設定[`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)值。</span><span class="sxs-lookup"><span data-stu-id="cc909-180">Alternatively, you could explicitly set a [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) value.</span></span> <span data-ttu-id="cc909-181">下列程式碼顯示具有日期格式字串（也就是 "d"）的 [發行日期] 屬性。</span><span class="sxs-lookup"><span data-stu-id="cc909-181">The following code shows the release date property with a date format string (namely, "d").</span></span> <span data-ttu-id="cc909-182">您會使用此來指定在發行日期中不需要時間。</span><span class="sxs-lookup"><span data-stu-id="cc909-182">You'd use this to specify that you don't want to time as part of the release date.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

<span data-ttu-id="cc909-183">下列程式碼會將 `Price` 屬性格式化為貨幣。</span><span class="sxs-lookup"><span data-stu-id="cc909-183">The following code formats the `Price` property as currency.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

<span data-ttu-id="cc909-184">完整的 `Movie` 類別如下所示。</span><span class="sxs-lookup"><span data-stu-id="cc909-184">The complete `Movie` class is shown below.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

<span data-ttu-id="cc909-185">執行應用程式，並流覽至 `Movies` 控制器。</span><span class="sxs-lookup"><span data-stu-id="cc909-185">Run the application and browse to the `Movies` controller.</span></span>

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

<span data-ttu-id="cc909-187">在數列的下一個部分中，我們會檢閱應用程式，並對自動產生的 `Details` 和 `Delete` 方法進行一些改良。</span><span class="sxs-lookup"><span data-stu-id="cc909-187">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cc909-188">[上一頁](adding-a-new-field.md)
> [下一頁](improving-the-details-and-delete-methods.md)</span><span class="sxs-lookup"><span data-stu-id="cc909-188">[Previous](adding-a-new-field.md)
[Next](improving-the-details-and-delete-methods.md)</span></span>
