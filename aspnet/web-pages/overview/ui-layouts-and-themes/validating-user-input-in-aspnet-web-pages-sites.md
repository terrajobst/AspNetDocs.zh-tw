---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 在 ASP.NET Web Pages （Razor）網站中驗證使用者輸入 |Microsoft Docs
author: Rick-Anderson
description: 本文討論如何驗證您從使用者取得的資訊 &mdash; 也就是，確保使用者在中以 HTML 表單輸入有效的資訊 。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563501"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="5bc81-103">在 ASP.NET Web Pages （Razor）網站中驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="5bc81-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="5bc81-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5bc81-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5bc81-105">本文討論如何驗證您從使用者取得的資訊 &mdash; 亦即，確保使用者在 ASP.NET Web Pages （Razor）網站中輸入 HTML 表單中的有效資訊。</span><span class="sxs-lookup"><span data-stu-id="5bc81-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="5bc81-106">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="5bc81-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="5bc81-107">如何檢查使用者的輸入是否符合您定義的驗證準則。</span><span class="sxs-lookup"><span data-stu-id="5bc81-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="5bc81-108">如何判斷是否已通過所有驗證測試。</span><span class="sxs-lookup"><span data-stu-id="5bc81-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="5bc81-109">如何顯示驗證錯誤（以及如何設定其格式）。</span><span class="sxs-lookup"><span data-stu-id="5bc81-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="5bc81-110">如何驗證不是直接來自使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="5bc81-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="5bc81-111">以下是文章中引進的 ASP.NET 程式設計概念：</span><span class="sxs-lookup"><span data-stu-id="5bc81-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="5bc81-112">`Validation` helper。</span><span class="sxs-lookup"><span data-stu-id="5bc81-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="5bc81-113">`Html.ValidationSummary` 和 `Html.ValidationMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="5bc81-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5bc81-114">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="5bc81-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5bc81-115">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="5bc81-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="5bc81-116">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="5bc81-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="5bc81-117">本文包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="5bc81-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="5bc81-118">使用者輸入驗證的總覽</span><span class="sxs-lookup"><span data-stu-id="5bc81-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="5bc81-119">驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="5bc81-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="5bc81-120">加入用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="5bc81-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="5bc81-121">格式化驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="5bc81-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="5bc81-122">驗證不是直接來自使用者的資料</span><span class="sxs-lookup"><span data-stu-id="5bc81-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="5bc81-123">使用者輸入驗證的總覽</span><span class="sxs-lookup"><span data-stu-id="5bc81-123">Overview of User Input Validation</span></span>

<span data-ttu-id="5bc81-124">如果您要求使用者在頁面中輸入資訊（例如，在表單中），請務必確定他們輸入的值有效。</span><span class="sxs-lookup"><span data-stu-id="5bc81-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="5bc81-125">例如，您不想要處理遺失重要資訊的表單。</span><span class="sxs-lookup"><span data-stu-id="5bc81-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="5bc81-126">當使用者在 HTML 表單中輸入值時，他們輸入的值就是字串。</span><span class="sxs-lookup"><span data-stu-id="5bc81-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="5bc81-127">在許多情況下，您需要的值是一些其他的資料類型，例如整數或日期。</span><span class="sxs-lookup"><span data-stu-id="5bc81-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="5bc81-128">因此，您也必須確保使用者輸入的值可以正確地轉換成適當的資料類型。</span><span class="sxs-lookup"><span data-stu-id="5bc81-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="5bc81-129">對於這些值，您可能也會有一些限制。</span><span class="sxs-lookup"><span data-stu-id="5bc81-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="5bc81-130">例如，即使使用者正確輸入整數，您可能還是必須確定該值落在特定範圍內。</span><span class="sxs-lookup"><span data-stu-id="5bc81-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![使用 CSS 樣式類別的驗證錯誤](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="5bc81-132">**重要事項**驗證使用者輸入對於安全性也很重要。</span><span class="sxs-lookup"><span data-stu-id="5bc81-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="5bc81-133">當您限制使用者可以在表單中輸入的值時，您可以減少某人輸入可能會危害網站安全性的值。</span><span class="sxs-lookup"><span data-stu-id="5bc81-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="5bc81-134">驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="5bc81-134">Validating User Input</span></span>

<span data-ttu-id="5bc81-135">在 ASP.NET Web Pages 2 中，您可以使用 `Validator` helper 來測試使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="5bc81-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="5bc81-136">基本方法是執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="5bc81-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="5bc81-137">決定您想要驗證的輸入元素（欄位）。</span><span class="sxs-lookup"><span data-stu-id="5bc81-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="5bc81-138">您通常會驗證表單中 `<input>` 元素的值。</span><span class="sxs-lookup"><span data-stu-id="5bc81-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="5bc81-139">不過，最好是驗證所有輸入，甚至是來自 `<select>` 清單等受限元素的輸入。</span><span class="sxs-lookup"><span data-stu-id="5bc81-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="5bc81-140">這有助於確保使用者不會略過頁面上的控制項並提交表單。</span><span class="sxs-lookup"><span data-stu-id="5bc81-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="5bc81-141">在頁面程式碼中，使用 `Validation` helper 的方法，為每個輸入元素加入個別驗證檢查。</span><span class="sxs-lookup"><span data-stu-id="5bc81-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="5bc81-142">若要檢查必要的欄位，請使用 `Validation.RequireField(field, [error message])` （適用于個別欄位）或 `Validation.RequireFields(field1, field2, ...))` （適用于欄位清單）。</span><span class="sxs-lookup"><span data-stu-id="5bc81-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="5bc81-143">針對其他類型的驗證，請使用 `Validation.Add(field, ValidationType)`。</span><span class="sxs-lookup"><span data-stu-id="5bc81-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="5bc81-144">針對 `ValidationType`，您可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="5bc81-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="5bc81-145">提交頁面時，請檢查 `Validation.IsValid`，以檢查驗證是否已通過：</span><span class="sxs-lookup"><span data-stu-id="5bc81-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="5bc81-146">如果發生任何驗證錯誤，您會略過一般頁面處理。</span><span class="sxs-lookup"><span data-stu-id="5bc81-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="5bc81-147">例如，如果頁面的目的是要更新資料庫，除非已修正所有驗證錯誤，否則您不會這麼做。</span><span class="sxs-lookup"><span data-stu-id="5bc81-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="5bc81-148">如果發生驗證錯誤，請使用 `Html.ValidationSummary` 或 `Html.ValidationMessage`或兩者，在頁面的標記中顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5bc81-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="5bc81-149">下列範例顯示的頁面會說明這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc81-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="5bc81-150">若要查看驗證的運作方式，請執行此頁面並故意進行錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc81-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="5bc81-151">例如，如果您忘記輸入課程名稱、輸入，以及輸入不正確日期，則頁面看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="5bc81-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![呈現的頁面中的驗證錯誤](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="5bc81-153">加入用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="5bc81-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="5bc81-154">根據預設，使用者輸入會在使用者提交頁面後進行驗證，也就是在伺服器程式碼中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc81-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="5bc81-155">這種方法的缺點是，使用者不知道他們在送出頁面之後就會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc81-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="5bc81-156">如果表單很長或很複雜，只有在送出頁面之後才報告錯誤，對使用者而言可能不方便。</span><span class="sxs-lookup"><span data-stu-id="5bc81-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="5bc81-157">您可以在用戶端腳本中加入支援以執行驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc81-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="5bc81-158">在這種情況下，當使用者在瀏覽器中工作時，就會執行驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc81-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="5bc81-159">例如，假設您指定值應為整數。</span><span class="sxs-lookup"><span data-stu-id="5bc81-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="5bc81-160">如果使用者輸入非整數值，當使用者離開輸入欄位時，就會回報錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc81-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="5bc81-161">使用者會收到立即的意見反應，這對他們而言很方便。</span><span class="sxs-lookup"><span data-stu-id="5bc81-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="5bc81-162">以用戶端為基礎的驗證也可以減少使用者提交表單以更正多個錯誤的次數。</span><span class="sxs-lookup"><span data-stu-id="5bc81-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc81-163">即使您使用用戶端驗證，也一律會在伺服器程式碼中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc81-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="5bc81-164">如果使用者略過以用戶端為基礎的驗證，在伺服器程式碼中執行驗證就是一種安全性措施。</span><span class="sxs-lookup"><span data-stu-id="5bc81-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>

1. <span data-ttu-id="5bc81-165">在頁面中註冊下列 JavaScript 程式庫：</span><span class="sxs-lookup"><span data-stu-id="5bc81-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="5bc81-166">其中兩個程式庫可從內容傳遞網路（CDN）載入，因此您不一定要將它們安裝在電腦或伺服器上。</span><span class="sxs-lookup"><span data-stu-id="5bc81-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="5bc81-167">不過，您必須擁有 jquery 的本機複本 *。請驗證.* 不想要的 .js。</span><span class="sxs-lookup"><span data-stu-id="5bc81-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="5bc81-168">如果您還沒有使用包含程式庫的 WebMatrix 範本（例如**入門網站**），請建立以**入門網站**為基礎的 Web 網頁網站。</span><span class="sxs-lookup"><span data-stu-id="5bc81-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="5bc81-169">然後將 *.js*檔案複製到您目前的網站。</span><span class="sxs-lookup"><span data-stu-id="5bc81-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="5bc81-170">在 [標記] 中，針對您要驗證的每個元素，新增對 `Validation.For(field)`的呼叫。</span><span class="sxs-lookup"><span data-stu-id="5bc81-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="5bc81-171">這個方法會發出用戶端驗證所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc81-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="5bc81-172">（而不是發出實際的 JavaScript 程式碼，方法會發出 `data-val-...`之類的屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc81-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="5bc81-173">這些屬性支援不顯眼的用戶端驗證，使用 jQuery 來執行工作。）</span><span class="sxs-lookup"><span data-stu-id="5bc81-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="5bc81-174">下列頁面顯示如何將用戶端驗證功能新增至稍早所示的範例。</span><span class="sxs-lookup"><span data-stu-id="5bc81-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="5bc81-175">並非所有驗證檢查都是在用戶端上執行。</span><span class="sxs-lookup"><span data-stu-id="5bc81-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="5bc81-176">特別的是，資料類型驗證（整數、日期等等）不會在用戶端上執行。</span><span class="sxs-lookup"><span data-stu-id="5bc81-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="5bc81-177">下列檢查同時適用于用戶端和伺服器：</span><span class="sxs-lookup"><span data-stu-id="5bc81-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="5bc81-178">在此範例中，有效日期的測試將無法在用戶端程式代碼中使用。</span><span class="sxs-lookup"><span data-stu-id="5bc81-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="5bc81-179">不過，測試將會在伺服器程式碼中執行。</span><span class="sxs-lookup"><span data-stu-id="5bc81-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="5bc81-180">格式化驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="5bc81-180">Formatting Validation Errors</span></span>

<span data-ttu-id="5bc81-181">您可以藉由定義具有下列保留名稱的 CSS 類別，來控制驗證錯誤的顯示方式：</span><span class="sxs-lookup"><span data-stu-id="5bc81-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="5bc81-182">`field-validation-error`</span><span class="sxs-lookup"><span data-stu-id="5bc81-182">`field-validation-error`.</span></span> <span data-ttu-id="5bc81-183">定義在顯示錯誤時，`Html.ValidationMessage` 方法的輸出。</span><span class="sxs-lookup"><span data-stu-id="5bc81-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="5bc81-184">`field-validation-valid`</span><span class="sxs-lookup"><span data-stu-id="5bc81-184">`field-validation-valid`.</span></span> <span data-ttu-id="5bc81-185">當沒有錯誤時，定義 `Html.ValidationMessage` 方法的輸出。</span><span class="sxs-lookup"><span data-stu-id="5bc81-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="5bc81-186">`input-validation-error`</span><span class="sxs-lookup"><span data-stu-id="5bc81-186">`input-validation-error`.</span></span> <span data-ttu-id="5bc81-187">定義當發生錯誤時，如何轉譯 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="5bc81-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="5bc81-188">（例如，您可以使用這個類別，將 &lt;輸入&gt; 元素的背景色彩設定為不同的色彩（如果其值無效）。只有在用戶端驗證期間（在 ASP.NET Web Pages 2 中），才會使用這個 CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="5bc81-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="5bc81-189">`input-validation-valid`</span><span class="sxs-lookup"><span data-stu-id="5bc81-189">`input-validation-valid`.</span></span> <span data-ttu-id="5bc81-190">當沒有錯誤時，定義 `<input>` 元素的外觀。</span><span class="sxs-lookup"><span data-stu-id="5bc81-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="5bc81-191">`validation-summary-errors`</span><span class="sxs-lookup"><span data-stu-id="5bc81-191">`validation-summary-errors`.</span></span> <span data-ttu-id="5bc81-192">定義其顯示錯誤清單之 `Html.ValidationSummary` 方法的輸出。</span><span class="sxs-lookup"><span data-stu-id="5bc81-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="5bc81-193">`validation-summary-valid`</span><span class="sxs-lookup"><span data-stu-id="5bc81-193">`validation-summary-valid`.</span></span> <span data-ttu-id="5bc81-194">當沒有錯誤時，定義 `Html.ValidationSummary` 方法的輸出。</span><span class="sxs-lookup"><span data-stu-id="5bc81-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="5bc81-195">下列 `<style>` 區塊會顯示錯誤狀況的規則。</span><span class="sxs-lookup"><span data-stu-id="5bc81-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="5bc81-196">如果您在本文稍早的範例頁面中包含此樣式區塊，錯誤顯示將如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="5bc81-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![使用 CSS 樣式類別的驗證錯誤](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="5bc81-198">如果您不是在 ASP.NET Web Pages 2 中使用用戶端驗證，則 `<input>` 元素（`input-validation-error` 和 `input-validation-valid` 的 CSS 類別不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="5bc81-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>

### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="5bc81-199">靜態和動態錯誤顯示</span><span class="sxs-lookup"><span data-stu-id="5bc81-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="5bc81-200">CSS 規則成對出現，例如 `validation-summary-errors` 和 `validation-summary-valid`。</span><span class="sxs-lookup"><span data-stu-id="5bc81-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="5bc81-201">這些配對可讓您定義這兩種條件的規則：錯誤狀況和「正常」（非錯誤）條件。</span><span class="sxs-lookup"><span data-stu-id="5bc81-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="5bc81-202">請務必瞭解，即使沒有任何錯誤，也一定會轉譯錯誤顯示的標記。</span><span class="sxs-lookup"><span data-stu-id="5bc81-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="5bc81-203">例如，如果頁面在標記中有 `Html.ValidationSummary` 方法，則即使第一次要求頁面時，頁面來源也會包含下列標記：</span><span class="sxs-lookup"><span data-stu-id="5bc81-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="5bc81-204">換句話說，即使錯誤清單是空的，`Html.ValidationSummary` 方法一律會呈現 `<div>` 元素和清單。</span><span class="sxs-lookup"><span data-stu-id="5bc81-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="5bc81-205">同樣地，`Html.ValidationMessage` 方法一律會將 `<span>` 元素呈現為個別欄位錯誤的預留位置，即使沒有任何錯誤也一樣。</span><span class="sxs-lookup"><span data-stu-id="5bc81-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="5bc81-206">在某些情況下，顯示錯誤訊息可能會導致頁面重新排列，而且可能會導致頁面上的元素四處移動。</span><span class="sxs-lookup"><span data-stu-id="5bc81-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="5bc81-207">`-valid` 結尾的 CSS 規則可讓您定義有助於防止此問題的版面配置。</span><span class="sxs-lookup"><span data-stu-id="5bc81-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="5bc81-208">例如，您可以定義 `field-validation-error`，`field-validation-valid` 兩者都有相同的固定大小。</span><span class="sxs-lookup"><span data-stu-id="5bc81-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="5bc81-209">如此一來，欄位的顯示區域為靜態，如果顯示錯誤訊息，則不會變更網頁流程。</span><span class="sxs-lookup"><span data-stu-id="5bc81-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="5bc81-210">驗證不是直接來自使用者的資料</span><span class="sxs-lookup"><span data-stu-id="5bc81-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="5bc81-211">有時候，您必須驗證不是直接來自 HTML 表單的資訊。</span><span class="sxs-lookup"><span data-stu-id="5bc81-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="5bc81-212">典型的範例是在查詢字串中傳遞值的頁面，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5bc81-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="5bc81-213">在此情況下，您會想要確定傳遞至頁面的值（在這裡，1022代表 `classid`的值）是有效的。</span><span class="sxs-lookup"><span data-stu-id="5bc81-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="5bc81-214">您無法直接使用 `Validation` helper 來執行這種驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc81-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="5bc81-215">不過，您可以使用驗證系統的其他功能，例如顯示驗證錯誤訊息的能力。</span><span class="sxs-lookup"><span data-stu-id="5bc81-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5bc81-216">**重要事項**一律驗證您從*任何*來源取得的值，包括表單域值、查詢字串值和 cookie 值。</span><span class="sxs-lookup"><span data-stu-id="5bc81-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="5bc81-217">人們很容易就能變更這些值（可能是為了惡意的目的）。</span><span class="sxs-lookup"><span data-stu-id="5bc81-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="5bc81-218">因此，您必須檢查這些值，才能保護您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bc81-218">So you must check these values in order to protect your application.</span></span>

<span data-ttu-id="5bc81-219">下列範例會示範如何驗證在查詢字串中傳遞的值。</span><span class="sxs-lookup"><span data-stu-id="5bc81-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="5bc81-220">此程式碼會測試值不是空的，且為整數。</span><span class="sxs-lookup"><span data-stu-id="5bc81-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="5bc81-221">請注意，當要求不是提交表單（`if(!IsPost)`）時，就會執行測試。</span><span class="sxs-lookup"><span data-stu-id="5bc81-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="5bc81-222">這項測試會在第一次要求頁面時通過，但不會在要求提交表單時傳遞。</span><span class="sxs-lookup"><span data-stu-id="5bc81-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="5bc81-223">若要顯示此錯誤，您可以藉由呼叫 `Validation.AddFormError("message")`，將錯誤加入至驗證錯誤清單。</span><span class="sxs-lookup"><span data-stu-id="5bc81-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="5bc81-224">如果頁面包含對 `Html.ValidationSummary` 方法的呼叫，就會在該處顯示錯誤，就像使用者輸入驗證錯誤一樣。</span><span class="sxs-lookup"><span data-stu-id="5bc81-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="5bc81-225">其他資源</span><span class="sxs-lookup"><span data-stu-id="5bc81-225">Additional Resources</span></span>

[<span data-ttu-id="5bc81-226">在 ASP.NET Web Pages 網站中使用 HTML 表單</span><span class="sxs-lookup"><span data-stu-id="5bc81-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
