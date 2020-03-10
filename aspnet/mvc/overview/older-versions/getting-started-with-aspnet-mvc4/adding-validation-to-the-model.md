---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 將驗證加入至模型 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: c9f6699c5d3500d4c1fcade9252aeb9dd92983da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615028"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="35a3d-104">將驗證新增至模型</span><span class="sxs-lookup"><span data-stu-id="35a3d-104">Adding Validation to the Model</span></span>

<span data-ttu-id="35a3d-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="35a3d-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="35a3d-106">本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="35a3d-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="35a3d-107">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="35a3d-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="35a3d-108">在本節中，您會將驗證邏輯新增至 `Movie` 模型，而且您將確保在使用者嘗試使用應用程式建立或編輯電影時，會強制執行驗證規則。</span><span class="sxs-lookup"><span data-stu-id="35a3d-108">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user attempts to create or edit a movie using the application.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="35a3d-109">讓事情晾乾</span><span class="sxs-lookup"><span data-stu-id="35a3d-109">Keeping Things DRY</span></span>

<span data-ttu-id="35a3d-110">ASP.NET MVC 的其中一個核心設計原則是幹（&quot;不重複原則&quot;）。</span><span class="sxs-lookup"><span data-stu-id="35a3d-110">One of the core design tenets of ASP.NET MVC is DRY (&quot;Don't Repeat Yourself&quot;).</span></span> <span data-ttu-id="35a3d-111">ASP.NET MVC 鼓勵您只指定一次功能或行為，然後讓它反映在應用程式中的所有位置。</span><span class="sxs-lookup"><span data-stu-id="35a3d-111">ASP.NET MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an application.</span></span> <span data-ttu-id="35a3d-112">這可減少您需要撰寫的程式碼數量，讓您撰寫的程式碼更容易出錯且更容易維護。</span><span class="sxs-lookup"><span data-stu-id="35a3d-112">This reduces the amount of code you need to write and makes the code you do write less error prone and easier to maintain.</span></span>

<span data-ttu-id="35a3d-113">ASP.NET MVC 和 Entity Framework Code First 所提供的驗證支援，是實際運作原則的絕佳範例。</span><span class="sxs-lookup"><span data-stu-id="35a3d-113">The validation support provided by ASP.NET MVC and Entity Framework Code First is a great example of the DRY principle in action.</span></span> <span data-ttu-id="35a3d-114">您可以在一個位置以宣告方式指定驗證規則（在模型類別中），而規則會在應用程式的任何位置強制執行。</span><span class="sxs-lookup"><span data-stu-id="35a3d-114">You can declaratively specify validation rules in one place (in the model class) and the rules are enforced everywhere in the application.</span></span>

<span data-ttu-id="35a3d-115">讓我們看看如何在電影應用程式中利用這項驗證支援。</span><span class="sxs-lookup"><span data-stu-id="35a3d-115">Let's look at how you can take advantage of this validation support in the movie application.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="35a3d-116">將驗證規則新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="35a3d-116">Adding Validation Rules to the Movie Model</span></span>

<span data-ttu-id="35a3d-117">首先，將一些驗證邏輯新增至 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="35a3d-117">You'll begin by adding some validation logic to the `Movie` class.</span></span>

<span data-ttu-id="35a3d-118">開啟 *Movie.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="35a3d-118">Open the *Movie.cs* file.</span></span> <span data-ttu-id="35a3d-119">在檔案的頂端新增參考[`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間的 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="35a3d-119">Add a `using` statement at the top of the file that references the [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

<span data-ttu-id="35a3d-120">請注意，命名空間不包含 `System.Web`。</span><span class="sxs-lookup"><span data-stu-id="35a3d-120">Notice the namespace does not contain `System.Web`.</span></span> <span data-ttu-id="35a3d-121">DataAnnotations 提供一組內建的驗證屬性，您可以將其以宣告方式套用至任何類別或屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-121">DataAnnotations provides a built-in set of validation attributes that you can apply declaratively to any class or property.</span></span>

<span data-ttu-id="35a3d-122">現在更新 `Movie` 類別，以利用內建的[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-122">Now update the `Movie` class to take advantage of the built-in [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), and [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) validation attributes.</span></span> <span data-ttu-id="35a3d-123">使用下列程式碼作為套用屬性的範例。</span><span class="sxs-lookup"><span data-stu-id="35a3d-123">Use the following code as an example of where to apply the attributes.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

<span data-ttu-id="35a3d-124">執行應用程式，您會再次收到下列執行階段錯誤：</span><span class="sxs-lookup"><span data-stu-id="35a3d-124">Run the application and you will again get the following run time error:</span></span>

<span data-ttu-id="35a3d-125">***在建立資料庫之後，支援 ' MovieDBCoNtext ' 內容的模型已經變更。請考慮使用 Code First 移轉來更新資料庫（[https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)）。***</span><span class="sxs-lookup"><span data-stu-id="35a3d-125">***The model backing the 'MovieDBContext' context has changed since the database was created. Consider using Code First Migrations to update the database ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).***</span></span>

<span data-ttu-id="35a3d-126">我們將使用「遷移」來更新架構。</span><span class="sxs-lookup"><span data-stu-id="35a3d-126">We will use migrations to update the schema.</span></span> <span data-ttu-id="35a3d-127">建立解決方案，然後開啟 [**套件管理員主控台**] 視窗並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="35a3d-127">Build the solution, and then open the **Package Manager Console** window and enter the following commands:</span></span>

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

<span data-ttu-id="35a3d-128">當此命令完成時，Visual Studio 會開啟類別檔案，該檔案會使用指定的名稱（*AddDataAnnotationsMig*）來定義新的 `DbMigration` 衍生類別，而在 `Up` 方法中，您可以看到更新架構條件約束的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35a3d-128">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class with the name specified (*AddDataAnnotationsMig*), and in the `Up` method you can see the code that updates the schema constraints.</span></span> <span data-ttu-id="35a3d-129">[`Title`] 和 [`Genre`] 欄位不再是可為 null （也就是說，您必須輸入一個值），而 [`Rating`] 欄位的最大長度為5。</span><span class="sxs-lookup"><span data-stu-id="35a3d-129">The `Title` and `Genre` fields are no longer nullable (that is, you must enter a value) and the `Rating` field has a maximum length of 5.</span></span>

<span data-ttu-id="35a3d-130">驗證屬性會指定您想要強制執行模型屬性套用的行為。</span><span class="sxs-lookup"><span data-stu-id="35a3d-130">The validation attributes specify behavior that you want to enforce on the model properties they are applied to.</span></span> <span data-ttu-id="35a3d-131">`Required` 屬性指出屬性必須具有值;在此範例中，電影必須有 `Title`、`ReleaseDate`、`Genre`和 `Price` 屬性的值，才能有效。</span><span class="sxs-lookup"><span data-stu-id="35a3d-131">The `Required` attribute indicates that a property must have a value; in this sample, a movie has to have values for the `Title`, `ReleaseDate`, `Genre`, and `Price` properties in order to be valid.</span></span> <span data-ttu-id="35a3d-132">`Range` 屬性會將值限制在指定的範圍內。</span><span class="sxs-lookup"><span data-stu-id="35a3d-132">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="35a3d-133">`StringLength` 屬性可讓您設定字串屬性的最大長度，並選擇性設定其最小長度。</span><span class="sxs-lookup"><span data-stu-id="35a3d-133">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span> <span data-ttu-id="35a3d-134">預設需要內部類型（例如 `decimal, int, float, DateTime`），而且不需要 `Required` 屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-134">Intrinsic types (such as `decimal, int, float, DateTime`) are required by default and don't need the `Required` attribute.</span></span>

<span data-ttu-id="35a3d-135">Code First 可確保在應用程式將變更儲存到資料庫之前，會強制執行您在模型類別上指定的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="35a3d-135">Code First ensures that the validation rules you specify on a model class are enforced before the application saves changes in the database.</span></span> <span data-ttu-id="35a3d-136">例如，下列程式碼會在呼叫 `SaveChanges` 方法時擲回例外狀況，因為遺漏了數個必要的 `Movie` 屬性值，而且價格為零（超出有效範圍）。</span><span class="sxs-lookup"><span data-stu-id="35a3d-136">For example, the code below will throw an exception when the `SaveChanges` method is called, because several required `Movie` property values are missing and the price is zero (which is out of the valid range).</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

<span data-ttu-id="35a3d-137">由 .NET Framework 自動強制執行驗證規則有助於讓應用程式更穩固。</span><span class="sxs-lookup"><span data-stu-id="35a3d-137">Having validation rules automatically enforced by the .NET Framework helps make your application more robust.</span></span> <span data-ttu-id="35a3d-138">它也確保您不會忘記要驗證某些項目，不小心讓不正確的資料進入資料庫。</span><span class="sxs-lookup"><span data-stu-id="35a3d-138">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

<span data-ttu-id="35a3d-139">以下是已更新之*Movie.cs*檔案的完整程式代碼清單：</span><span class="sxs-lookup"><span data-stu-id="35a3d-139">Here's a complete code listing for the updated *Movie.cs* file:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a><span data-ttu-id="35a3d-140">ASP.NET MVC 中的驗證錯誤 UI</span><span class="sxs-lookup"><span data-stu-id="35a3d-140">Validation Error UI in ASP.NET MVC</span></span>

<span data-ttu-id="35a3d-141">重新執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="35a3d-141">Re-run the application and navigate to the */Movies* URL.</span></span>

<span data-ttu-id="35a3d-142">按一下 [**建立新**的] 連結以新增電影。</span><span class="sxs-lookup"><span data-stu-id="35a3d-142">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="35a3d-143">在表單中填寫一些不正確值，然後按一下 [**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="35a3d-143">Fill out the form with some invalid values and then click the **Create** button.</span></span>

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="35a3d-145">若要支援對小數點使用逗號（&quot;，&quot;）之非英文地區設定的 jQuery 驗證，您必須包含全球化 *.js*和您的特定*文化特性/全球化. 文化特性 .js*檔案（從[https://github.com/jquery/globalize](https://github.com/jquery/globalize) ）和 JavaScript，以使用 `Globalize.parseFloat`。</span><span class="sxs-lookup"><span data-stu-id="35a3d-145">to support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="35a3d-146">下列程式碼顯示對 Views\Movies\Edit.cshtml 檔案所做的修改，以使用 &quot;fr-fr&quot; 文化特性：</span><span class="sxs-lookup"><span data-stu-id="35a3d-146">The following code shows the modifications to the Views\Movies\Edit.cshtml file to work with the &quot;fr-FR&quot; culture:</span></span>

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

<span data-ttu-id="35a3d-147">請注意表單如何自動使用紅色框線色彩來反白顯示包含無效資料的文字方塊，並且在每個文字旁發出適當的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="35a3d-147">Notice how the form has automatically used a red border color to highlight the text boxes that contain invalid data and has emitted an appropriate validation error message next to each one.</span></span> <span data-ttu-id="35a3d-148">用戶端 (使用 JavaScript 和 jQuery) 與伺服器端 (若使用者已停用 JavaScript 時) 都會強制執行這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="35a3d-148">The errors are enforced both client-side (using JavaScript and jQuery) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="35a3d-149">真正的好處是，您不需要在 `MoviesController` 類別或*建立. cshtml*視圖中變更一行程式碼，就能啟用此驗證 UI。</span><span class="sxs-lookup"><span data-stu-id="35a3d-149">A real benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="35a3d-150">您稍早在本教學課程中建立的控制器和檢視會自動拾取您指定的驗證規則 (在 `Movie` 模型類別的屬性 (property) 上使用驗證屬性 (attribute))。</span><span class="sxs-lookup"><span data-stu-id="35a3d-150">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified by using validation attributes on the properties of the `Movie` model class.</span></span>

<span data-ttu-id="35a3d-151">您可能已注意到屬性 `Title` 和 `Genre`，在您提交表單（按下 [**建立**] 按鈕），或在輸入欄位中輸入文字並將它移除之前，不會強制執行必要的屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-151">You might have noticed for the properties `Title` and `Genre`, the required attribute is not enforced until you submit the form (hit the **Create** button), or enter text into the input field and removed it.</span></span> <span data-ttu-id="35a3d-152">對於一開始是空的欄位（例如 [建立] 視圖上的欄位），而且只有 [必要] 屬性和其他驗證屬性，您可以執行下列動作來觸發驗證：</span><span class="sxs-lookup"><span data-stu-id="35a3d-152">For a field which is initially empty (such as the fields on the Create view) and which has only the required attribute and no other validation attributes, you can do the following to trigger validation:</span></span>

1. <span data-ttu-id="35a3d-153">Tab 鍵放入欄位中。</span><span class="sxs-lookup"><span data-stu-id="35a3d-153">Tab into the field.</span></span>
2. <span data-ttu-id="35a3d-154">輸入一些文字。</span><span class="sxs-lookup"><span data-stu-id="35a3d-154">Enter some text.</span></span>
3. <span data-ttu-id="35a3d-155">按下 Tab 鍵切換至下一個欄位。</span><span class="sxs-lookup"><span data-stu-id="35a3d-155">Tab out.</span></span>
4. <span data-ttu-id="35a3d-156">Tab 回到欄位。</span><span class="sxs-lookup"><span data-stu-id="35a3d-156">Tab back into the field.</span></span>
5. <span data-ttu-id="35a3d-157">移除文字。</span><span class="sxs-lookup"><span data-stu-id="35a3d-157">Remove the text.</span></span>
6. <span data-ttu-id="35a3d-158">按下 Tab 鍵切換至下一個欄位。</span><span class="sxs-lookup"><span data-stu-id="35a3d-158">Tab out.</span></span>

<span data-ttu-id="35a3d-159">上述順序會觸發必要的驗證，而不會按下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="35a3d-159">The above sequence will trigger the required validation without hitting the submit button.</span></span> <span data-ttu-id="35a3d-160">只要按下 [提交] 按鈕，而不輸入任何欄位，就會觸發用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="35a3d-160">Simply hitting the submit button without entering any of the fields will trigger client side validation.</span></span> <span data-ttu-id="35a3d-161">直到沒有任何用戶端驗證錯誤後，表單資料才會傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="35a3d-161">The form data is not sent to the server until there are no client side validation errors.</span></span> <span data-ttu-id="35a3d-162">您可以藉由將中斷點放在 HTTP Post 方法中，或使用[fiddler 工具](http://fiddler2.com/fiddler2/)或 IE 9 [F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478)來進行測試。</span><span class="sxs-lookup"><span data-stu-id="35a3d-162">You can test this by putting a break point in the HTTP Post method or using the [fiddler tool](http://fiddler2.com/fiddler2/) or the IE 9 [F12 developer tools](https://msdn.microsoft.com/ie/aa740478).</span></span>

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a><span data-ttu-id="35a3d-163">如何在 Create View 和 Create Action 方法中進行驗證</span><span class="sxs-lookup"><span data-stu-id="35a3d-163">How Validation Occurs in the Create View and Create Action Method</span></span>

<span data-ttu-id="35a3d-164">您可能奇怪如何在不更新控制器或檢視程式碼的狀況下產生驗證 UI。</span><span class="sxs-lookup"><span data-stu-id="35a3d-164">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="35a3d-165">下一個清單會顯示 `MovieController` 類別中的 `Create` 方法看起來如何。</span><span class="sxs-lookup"><span data-stu-id="35a3d-165">The next listing shows what the `Create` methods in the `MovieController` class look like.</span></span> <span data-ttu-id="35a3d-166">它們與您稍早在本教學課程中建立它們的方式不一樣。</span><span class="sxs-lookup"><span data-stu-id="35a3d-166">They're unchanged from how you created them earlier in this tutorial.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

<span data-ttu-id="35a3d-167">第一個 (HTTP GET)`Create` 動作方法會顯示初始建立表單。</span><span class="sxs-lookup"><span data-stu-id="35a3d-167">The first (HTTP GET) `Create` action method displays the initial Create form.</span></span> <span data-ttu-id="35a3d-168">第二個 (`[HttpPost]`) 版本處理表單張貼。</span><span class="sxs-lookup"><span data-stu-id="35a3d-168">The second (`[HttpPost]`) version handles the form post.</span></span> <span data-ttu-id="35a3d-169">第二個 `Create` 方法 (`HttpPost` 版本) 會呼叫`ModelState.IsValid` 檢查電影是否有任何驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="35a3d-169">The second `Create` method (The `HttpPost` version) calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="35a3d-170">呼叫此方法會評估已套用至物件的所有驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-170">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="35a3d-171">如果物件有驗證錯誤，則 `Create` 方法會重新顯示表單。</span><span class="sxs-lookup"><span data-stu-id="35a3d-171">If the object has validation errors, the `Create` method re-displays the form.</span></span> <span data-ttu-id="35a3d-172">如果沒有任何錯誤，方法即會將新的電影儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="35a3d-172">If there are no errors, the method saves the new movie in the database.</span></span> <span data-ttu-id="35a3d-173">在我們使用的電影範例中，**當用戶端偵測到驗證錯誤時，表單不會張貼到伺服器; 第二個**`Create`**方法則**不會被呼叫。</span><span class="sxs-lookup"><span data-stu-id="35a3d-173">In our movie example we are using, **the form is not posted to the server when their are validation errors detected on the client side; the second** `Create`**method is never called**.</span></span> <span data-ttu-id="35a3d-174">如果您在瀏覽器中停用 JavaScript，則會停用用戶端驗證，而且 HTTP POST `Create` 方法會呼叫 `ModelState.IsValid` 以檢查電影是否有任何驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="35a3d-174">If you disable JavaScript in your browser, client validation is disabled and the HTTP POST `Create` method calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span>

<span data-ttu-id="35a3d-175">您可以在 `HttpPost Create` 方法中設定中斷點，並確認永遠不會呼叫該方法，用戶端驗證就不會在偵測到驗證錯誤時，提交表單資料。</span><span class="sxs-lookup"><span data-stu-id="35a3d-175">You can set a break point in the `HttpPost Create` method and verify the method is never called, client side validation will not submit the form data when validation errors are detected.</span></span> <span data-ttu-id="35a3d-176">如果您停用瀏覽器的 JavaScript，然後提交有錯誤的表單，就會叫用中斷點。</span><span class="sxs-lookup"><span data-stu-id="35a3d-176">If you disable JavaScript in your browser, then submit the form with errors, the break point will be hit.</span></span> <span data-ttu-id="35a3d-177">您仍可使用沒有 JavaScript 的完整驗證。</span><span class="sxs-lookup"><span data-stu-id="35a3d-177">You still get full validation without JavaScript.</span></span> <span data-ttu-id="35a3d-178">下圖顯示如何在 Internet Explorer 中停用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="35a3d-178">The following image shows how to disable JavaScript in Internet Explorer.</span></span>

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

<span data-ttu-id="35a3d-179">下圖顯示如何停用 FireFox 瀏覽器的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="35a3d-179">The following image shows how to disable JavaScript in the FireFox browser.</span></span>

![](adding-validation-to-the-model/_static/image5.png)

<span data-ttu-id="35a3d-180">下圖顯示如何使用 Chrome 瀏覽器停用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="35a3d-180">The following image shows how to disable JavaScript with the Chrome browser.</span></span>

![](adding-validation-to-the-model/_static/image6.png)

<span data-ttu-id="35a3d-181">以下是您稍早在本教學課程中 scaffold 的*建立. cshtml*視圖範本。</span><span class="sxs-lookup"><span data-stu-id="35a3d-181">Below is the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="35a3d-182">上述動作方法會使用它來顯示初始表單，以及在發生錯誤時重新顯示它。</span><span class="sxs-lookup"><span data-stu-id="35a3d-182">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

<span data-ttu-id="35a3d-183">請注意程式碼如何使用 `Html.EditorFor` helper 來輸出每個 `Movie` 屬性的 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="35a3d-183">Notice how the code uses an `Html.EditorFor` helper to output the `<input>` element for each `Movie` property.</span></span> <span data-ttu-id="35a3d-184">在此協助程式旁呼叫 `Html.ValidationMessageFor` helper 方法。</span><span class="sxs-lookup"><span data-stu-id="35a3d-184">Next to this helper is a call to the `Html.ValidationMessageFor` helper method.</span></span> <span data-ttu-id="35a3d-185">這兩個 helper 方法會使用由控制器傳遞至視圖的模型物件（在此案例中為 `Movie` 物件）。</span><span class="sxs-lookup"><span data-stu-id="35a3d-185">These two helper methods work with the model object that's passed by the controller to the view (in this case, a `Movie` object).</span></span> <span data-ttu-id="35a3d-186">它們會自動尋找在模型上指定的驗證屬性，並適當地顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="35a3d-186">They automatically look for validation attributes specified on the model and display error messages as appropriate.</span></span>

<span data-ttu-id="35a3d-187">這種方法的好處是，控制器或建立視圖範本都無法得知所強制執行的實際驗證規則，或顯示的特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="35a3d-187">What's really nice about this approach is that neither the controller nor the Create view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="35a3d-188">驗證規則和錯誤字串只在 `Movie` 類別中指定。</span><span class="sxs-lookup"><span data-stu-id="35a3d-188">The validation rules and the error strings are specified only in the `Movie` class.</span></span> <span data-ttu-id="35a3d-189">這些相同的驗證規則會自動套用至編輯檢視，以及您可能會建立以編輯模型的任何其他 views 範本。</span><span class="sxs-lookup"><span data-stu-id="35a3d-189">These same validation rules are automatically applied to the Edit view and any other views templates you might create that edit your model.</span></span>

<span data-ttu-id="35a3d-190">如果您稍後想要變更驗證邏輯，您可以在模型中加入驗證屬性（在此範例中為 `movie` 類別），以在一個位置中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="35a3d-190">If you want to change the validation logic later, you can do so in exactly one place by adding validation attributes to the model (in this example, the `movie` class).</span></span> <span data-ttu-id="35a3d-191">您不必擔心應用程式的不同部分會與規則強制執行的方式不一致，所有的驗證邏輯都是在同一個地方定義，用於所有位置。</span><span class="sxs-lookup"><span data-stu-id="35a3d-191">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="35a3d-192">這會讓程式碼非常整齊乾淨，容易維護及發展。</span><span class="sxs-lookup"><span data-stu-id="35a3d-192">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="35a3d-193">這表示您會完全接受 DRY 原則。</span><span class="sxs-lookup"><span data-stu-id="35a3d-193">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="adding-formatting-to-the-movie-model"></a><span data-ttu-id="35a3d-194">將格式新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="35a3d-194">Adding Formatting to the Movie Model</span></span>

<span data-ttu-id="35a3d-195">開啟 *Movie.cs* 檔案並檢查 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="35a3d-195">Open the *Movie.cs* file and examine the `Movie` class.</span></span> <span data-ttu-id="35a3d-196">除了內建的驗證屬性集之外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間還會提供格式屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-196">The [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="35a3d-197">我們已將[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)列舉值套用至發行日期和價格欄位。</span><span class="sxs-lookup"><span data-stu-id="35a3d-197">We've already applied a [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="35a3d-198">下列程式碼顯示具有適當[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性的 `ReleaseDate` 和 `Price` 屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-198">The following code shows the `ReleaseDate` and `Price` properties with the appropriate [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

<span data-ttu-id="35a3d-199">[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性不是驗證屬性，而是用來告訴視圖引擎如何呈現 HTML。</span><span class="sxs-lookup"><span data-stu-id="35a3d-199">The [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attributes are not validation attributes, they are used to tell the view engine how to render the HTML.</span></span> <span data-ttu-id="35a3d-200">在上述範例中，`DataType.Date` 屬性會將電影日期顯示為僅限日期，沒有時間。</span><span class="sxs-lookup"><span data-stu-id="35a3d-200">In the example above, the `DataType.Date` attribute displays the movie dates as dates only, without time.</span></span> <span data-ttu-id="35a3d-201">例如，下列[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性不會驗證資料的格式：</span><span class="sxs-lookup"><span data-stu-id="35a3d-201">For example, the following [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attributes don't validate the format of the data:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

<span data-ttu-id="35a3d-202">以上所列的屬性只會提供 view engine 用來格式化資料的提示（如 &lt;URL 的&gt; 和 &lt;href =&quot;mailto:EmailAddress&quot;電子郵件的屬性。&gt;</span><span class="sxs-lookup"><span data-stu-id="35a3d-202">The attributes listed above only provide hints for the view engine to format the data (and supply attributes such as &lt;a&gt; for URL's and &lt;a href=&quot;mailto:EmailAddress.com&quot;&gt; for email.</span></span> <span data-ttu-id="35a3d-203">您可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)屬性來驗證資料的格式。</span><span class="sxs-lookup"><span data-stu-id="35a3d-203">You can use the [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) attribute to validate the format of the data.</span></span>

<span data-ttu-id="35a3d-204">另一種使用 `DataType` 屬性的方法，您可以明確地設定[`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)值。</span><span class="sxs-lookup"><span data-stu-id="35a3d-204">An alternative approach to using the `DataType` attributes, you could explicitly set a [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) value.</span></span> <span data-ttu-id="35a3d-205">下列程式碼顯示具有日期格式字串（也就是 &quot;d&quot;）的 [發行日期] 屬性。</span><span class="sxs-lookup"><span data-stu-id="35a3d-205">The following code shows the release date property with a date format string (namely, &quot;d&quot;).</span></span> <span data-ttu-id="35a3d-206">您會使用此來指定在發行日期中不需要時間。</span><span class="sxs-lookup"><span data-stu-id="35a3d-206">You'd use this to specify that you don't want to time as part of the release date.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

<span data-ttu-id="35a3d-207">完整的 `Movie` 類別如下所示。</span><span class="sxs-lookup"><span data-stu-id="35a3d-207">The complete `Movie` class is shown below.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

<span data-ttu-id="35a3d-208">執行應用程式，並流覽至 `Movies` 控制器。</span><span class="sxs-lookup"><span data-stu-id="35a3d-208">Run the application and browse to the `Movies` controller.</span></span> <span data-ttu-id="35a3d-209">發行日期和價格的格式正確。</span><span class="sxs-lookup"><span data-stu-id="35a3d-209">The release date and price are nicely formatted.</span></span> <span data-ttu-id="35a3d-210">下圖顯示使用 &quot;fr-fr&quot; 作為文化特性的發行日期和價格。</span><span class="sxs-lookup"><span data-stu-id="35a3d-210">The image below shows the release date and price using &quot;fr-FR&quot; as the culture.</span></span>

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

<span data-ttu-id="35a3d-212">下圖顯示使用預設文化特性（英文 US）所顯示的相同資料。</span><span class="sxs-lookup"><span data-stu-id="35a3d-212">The image below shows the same data displayed with the default culture (English US).</span></span>

![](adding-validation-to-the-model/_static/image8.png)

<span data-ttu-id="35a3d-213">在數列的下一個部分中，我們會檢閱應用程式，並對自動產生的 `Details` 和 `Delete` 方法進行一些改良。</span><span class="sxs-lookup"><span data-stu-id="35a3d-213">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35a3d-214">[上一頁](adding-a-new-field-to-the-movie-model-and-table.md)
> [下一頁](examining-the-details-and-delete-methods.md)</span><span class="sxs-lookup"><span data-stu-id="35a3d-214">[Previous](adding-a-new-field-to-the-movie-model-and-table.md)
[Next](examining-the-details-and-delete-methods.md)</span></span>
