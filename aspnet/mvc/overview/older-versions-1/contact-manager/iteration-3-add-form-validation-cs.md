---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: '反覆項目 #3 – 新增表單驗證 (C#) |Microsoft Docs'
author: microsoft
description: 在第三個反覆項目，我們會加入基本表單驗證。 我們可以防止使用者提交表單，而不會完成必要的表單欄位。 我們也會驗證 emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: 4115b3898415d63ffb122f3d0fea93022f2baa02
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030415"
---
<a name="iteration-3--add-form-validation-c"></a><span data-ttu-id="6e930-105">反覆項目 #3 – 新增表單驗證 (C#)</span><span class="sxs-lookup"><span data-stu-id="6e930-105">Iteration #3 – Add form validation (C#)</span></span>
====================
<span data-ttu-id="6e930-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6e930-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="6e930-107">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="6e930-107">Download Code</span></span>](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> <span data-ttu-id="6e930-108">在第三個反覆項目，我們會加入基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="6e930-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="6e930-109">我們可以防止使用者提交表單，而不會完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="6e930-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="6e930-110">此外，我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="6e930-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="6e930-111">建立連絡人管理 ASP.NET MVC 應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="6e930-111">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="6e930-112">在本系列教學課程中，我們會建置整個連絡人管理應用程式從開始到完成。</span><span class="sxs-lookup"><span data-stu-id="6e930-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="6e930-113">請連絡系統管理員應用程式可讓您商店連絡資訊的名稱、 電話號碼和電子郵件地址-的人員清單。</span><span class="sxs-lookup"><span data-stu-id="6e930-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="6e930-114">我們會建置應用程式透過多個反覆項目。</span><span class="sxs-lookup"><span data-stu-id="6e930-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="6e930-115">每次反覆運算時，我們會逐漸改善應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="6e930-116">此多個反覆項目方法的目標是要讓您了解每個變更的原因。</span><span class="sxs-lookup"><span data-stu-id="6e930-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="6e930-117">反覆項目 #1-建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="6e930-118">在第一次反覆運算中，我們建立連絡人管理員中的最簡單的方式可能。</span><span class="sxs-lookup"><span data-stu-id="6e930-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="6e930-119">我們將新增基本資料庫作業的支援：建立、 讀取、 更新和刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="6e930-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="6e930-120">反覆項目 #2-讓應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="6e930-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="6e930-121">這個反覆項目，我們以改善應用程式的外觀的修改預設的 ASP.NET MVC 檢視主版頁面和階層式樣式表。</span><span class="sxs-lookup"><span data-stu-id="6e930-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="6e930-122">反覆項目 #3-新增表單驗證。</span><span class="sxs-lookup"><span data-stu-id="6e930-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="6e930-123">在第三個反覆項目，我們會加入基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="6e930-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="6e930-124">我們可以防止使用者提交表單，而不會完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="6e930-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="6e930-125">此外，我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="6e930-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="6e930-126">反覆項目 #4-進行鬆散偶合的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="6e930-127">在這個第四個反覆項目中，我們利用數種軟體設計模式，以讓它更容易維護及修改連絡人管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="6e930-128">比方說，我們可以重構應用程式使用儲存機制模式和相依性插入模式。</span><span class="sxs-lookup"><span data-stu-id="6e930-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="6e930-129">反覆項目 #5-建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="6e930-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="6e930-130">在第五個反覆項目中，我們讓我們的應用程式容易維護及修改藉由新增單元測試。</span><span class="sxs-lookup"><span data-stu-id="6e930-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="6e930-131">我們模擬我們的資料模型類別，並建置我們的控制器和驗證邏輯單元測試。</span><span class="sxs-lookup"><span data-stu-id="6e930-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="6e930-132">反覆項目 #6-使用測試導向開發。</span><span class="sxs-lookup"><span data-stu-id="6e930-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="6e930-133">在這個第六個反覆項目中，我們新功能加入我們的應用程式方法是先撰寫單元測試，並撰寫單元測試的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6e930-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="6e930-134">在這個反覆項目，我們會新增連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="6e930-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="6e930-135">反覆項目 #7-新增 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="6e930-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="6e930-136">在第七個反覆項目，改善回應性和我們的應用程式的效能透過新增對 Ajax 支援。</span><span class="sxs-lookup"><span data-stu-id="6e930-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="6e930-137">這個反覆項目</span><span class="sxs-lookup"><span data-stu-id="6e930-137">This Iteration</span></span>

<span data-ttu-id="6e930-138">在連絡人管理員應用程式的這個第二個反覆項目，我們會加入基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="6e930-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="6e930-139">我們可以防止人提交連絡人，而不需要的表單欄位中輸入值。</span><span class="sxs-lookup"><span data-stu-id="6e930-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="6e930-140">此外，我們也會驗證電話號碼和電子郵件地址 （請參閱 圖 1）。</span><span class="sxs-lookup"><span data-stu-id="6e930-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="6e930-141">[![[新增專案] 對話方塊](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6e930-141">[![The New Project dialog box](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="6e930-142">**圖 01**:表單驗證 ([按一下以檢視完整大小的影像](iteration-3-add-form-validation-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6e930-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-cs/_static/image2.png))</span></span>


<span data-ttu-id="6e930-143">這個反覆項目，在中，我們會將驗證邏輯直接加入控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6e930-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="6e930-144">一般情況下，這不是建議用來將驗證新增至 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="6e930-145">更好的方法是將應用程式的驗證邏輯放在個別[服務層](http://martinfowler.com/eaaCatalog/serviceLayer.html)。</span><span class="sxs-lookup"><span data-stu-id="6e930-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="6e930-146">在下一個反覆項目中，我們可以重構連絡人管理員應用程式，讓應用程式更容易維護。</span><span class="sxs-lookup"><span data-stu-id="6e930-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="6e930-147">在這個反覆項目，以簡化一切，我們撰寫所有的驗證程式碼以手動方式。</span><span class="sxs-lookup"><span data-stu-id="6e930-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="6e930-148">而不需要自行撰寫驗證程式碼，我們可以利用驗證架構。</span><span class="sxs-lookup"><span data-stu-id="6e930-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="6e930-149">例如，您可以使用 Microsoft 企業程式庫驗證應用程式區塊 (VAB) 來實作驗證邏輯的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="6e930-150">若要深入了解驗證應用程式區塊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="6e930-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="6e930-151">將驗證新增至建立檢視</span><span class="sxs-lookup"><span data-stu-id="6e930-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="6e930-152">可讓 s 著手將驗證邏輯加入至建立檢視。</span><span class="sxs-lookup"><span data-stu-id="6e930-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="6e930-153">幸運的是，由於我們產生使用 Visual Studio 的 [建立] 檢視時，建立檢視已經包含所有必要的使用者介面邏輯，以顯示驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="6e930-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="6e930-154">在 列表 1 中包含建立檢視。</span><span class="sxs-lookup"><span data-stu-id="6e930-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="6e930-155">**Listing 1 - \Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="6e930-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

<span data-ttu-id="6e930-156">請注意 Html.ValidationSummary() helper 方法，它會立即顯示的 HTML 表單上方的呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e930-156">Notice the call to the Html.ValidationSummary() helper method that appears immediately above the HTML form.</span></span> <span data-ttu-id="6e930-157">如果有驗證錯誤訊息，這個方法會顯示驗證訊息中的項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="6e930-157">If there are validation error messages, then this method displays validation messages in a bulleted list.</span></span>

<span data-ttu-id="6e930-158">請注意，此外，每個表單欄位旁邊會顯示 Html.ValidationMessage() 呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e930-158">Notice, furthermore, the calls to Html.ValidationMessage() that appear next to each form field.</span></span> <span data-ttu-id="6e930-159">ValidationMessage() 協助程式會顯示個別的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6e930-159">The ValidationMessage() helper displays an individual validation error message.</span></span> <span data-ttu-id="6e930-160">在 列表 1，發生驗證錯誤時，會顯示一個星號。</span><span class="sxs-lookup"><span data-stu-id="6e930-160">In the case of Listing 1, an asterisk is displayed when there is a validation error.</span></span>

<span data-ttu-id="6e930-161">最後，Html.TextBox() helper 自動呈現的階層式樣式表類別協助程式 」 所顯示的屬性相關聯的驗證錯誤時。</span><span class="sxs-lookup"><span data-stu-id="6e930-161">Finally, the Html.TextBox() helper automatically renders a Cascading Style Sheet class when there is a validation error associated with the property displayed by the helper.</span></span> <span data-ttu-id="6e930-162">Html.TextBox() helper 會呈現一個名為類別**輸入驗證錯誤**。</span><span class="sxs-lookup"><span data-stu-id="6e930-162">The Html.TextBox() helper renders a class named **input-validation-error**.</span></span>

<span data-ttu-id="6e930-163">當您建立新的 ASP.NET MVC 應用程式時，就會自動將名為 Site.css 樣式表中 [Content] 資料夾上建立。</span><span class="sxs-lookup"><span data-stu-id="6e930-163">When you create a new ASP.NET MVC application, a style sheet named Site.css is created in the Content folder automatically.</span></span> <span data-ttu-id="6e930-164">此樣式表包含與相關的驗證錯誤訊息外觀的 CSS 類別的下列定義：</span><span class="sxs-lookup"><span data-stu-id="6e930-164">This style sheet contains the following definitions for CSS classes related to the appearance of validation error messages:</span></span>

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

<span data-ttu-id="6e930-165">欄位驗證錯誤的類別用來設定樣式 Html.ValidationMessage() 協助程式所轉譯的輸出。</span><span class="sxs-lookup"><span data-stu-id="6e930-165">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="6e930-166">輸入驗證錯誤的類別用來設定樣式 Html.TextBox() 協助程式所轉譯的文字方塊 （輸入）。</span><span class="sxs-lookup"><span data-stu-id="6e930-166">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="6e930-167">驗證摘要錯誤類別用來設定樣式 Html.ValidationSummary() 協助程式所呈現的未排序的清單。</span><span class="sxs-lookup"><span data-stu-id="6e930-167">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6e930-168">您可以修改此區段可自訂的驗證錯誤訊息外觀所描述的樣式表類別。</span><span class="sxs-lookup"><span data-stu-id="6e930-168">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="6e930-169">加入驗證邏輯，以建立動作</span><span class="sxs-lookup"><span data-stu-id="6e930-169">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="6e930-170">現在，建立檢視永遠不會顯示驗證錯誤訊息，因為我們已不編寫的邏輯會產生任何訊息。</span><span class="sxs-lookup"><span data-stu-id="6e930-170">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="6e930-171">若要顯示驗證錯誤訊息，您需要加入 ModelState 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6e930-171">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6e930-172">UpdateModel() 方法會將錯誤訊息加入 ModelState 自動錯誤的表單欄位的值指派給屬性時。</span><span class="sxs-lookup"><span data-stu-id="6e930-172">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="6e930-173">例如，如果您嘗試將字串"apple"指派給 BirthDate 屬性可接受的日期時間值，然後 UpdateModel() 方法會將錯誤加入 ModelState。</span><span class="sxs-lookup"><span data-stu-id="6e930-173">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="6e930-174">修改的 create （） 方法，在 列表 2 中包含新的區段，新的連絡人插入資料庫之前會驗證連絡人類別的屬性。</span><span class="sxs-lookup"><span data-stu-id="6e930-174">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="6e930-175">**列表 2-Controllers\ContactController.cs （建立與驗證）**</span><span class="sxs-lookup"><span data-stu-id="6e930-175">**Listing 2 - Controllers\ContactController.cs (Create with validation)**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

<span data-ttu-id="6e930-176">[驗證] 區段中，會強制執行四個不同的驗證規則：</span><span class="sxs-lookup"><span data-stu-id="6e930-176">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="6e930-177">FirstName 屬性必須具有長度小於或等於零 （和它不能僅由空格）</span><span class="sxs-lookup"><span data-stu-id="6e930-177">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="6e930-178">LastName 屬性必須具有長度小於或等於零 （和它不能僅由空格）</span><span class="sxs-lookup"><span data-stu-id="6e930-178">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="6e930-179">如果 [Phone] 屬性的值 （長度大於 0） 則電話屬性必須符合規則運算式。</span><span class="sxs-lookup"><span data-stu-id="6e930-179">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="6e930-180">如果電子郵件屬性的值 （長度大於 0） 則的電子郵件屬性必須符合規則運算式。</span><span class="sxs-lookup"><span data-stu-id="6e930-180">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="6e930-181">驗證規則違規時，出現錯誤訊息會加入 ModelState AddModelError() 方法的協助。</span><span class="sxs-lookup"><span data-stu-id="6e930-181">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="6e930-182">當您將訊息加入 ModelState 時，您可以提供的屬性名稱和驗證錯誤訊息的文字。</span><span class="sxs-lookup"><span data-stu-id="6e930-182">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="6e930-183">Html.ValidationSummary() 和 Html.ValidationMessage() 協助程式方法，此錯誤訊息會顯示在檢視中。</span><span class="sxs-lookup"><span data-stu-id="6e930-183">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="6e930-184">執行驗證規則之後，會檢查 ModelState 的 IsValid 屬性。</span><span class="sxs-lookup"><span data-stu-id="6e930-184">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="6e930-185">當任何驗證錯誤訊息已加入至 ModelState IsValid 屬性會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="6e930-185">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="6e930-186">如果驗證失敗，錯誤訊息重新顯示建立表單。</span><span class="sxs-lookup"><span data-stu-id="6e930-186">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6e930-187">我收到驗證電話號碼和電子郵件地址的規則運算式存放庫中的規則運算式 [*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="6e930-187">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="6e930-188">將驗證邏輯加入至 編輯動作</span><span class="sxs-lookup"><span data-stu-id="6e930-188">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="6e930-189">Edit （） 動作會更新連絡人。</span><span class="sxs-lookup"><span data-stu-id="6e930-189">The Edit() action updates a Contact.</span></span> <span data-ttu-id="6e930-190">Edit （） 動作，就必須執行 create （） 動作完全相同的驗證。</span><span class="sxs-lookup"><span data-stu-id="6e930-190">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="6e930-191">而不必重複相同的驗證程式碼，我們應該重構連絡人控制器，以便將 create （） 與 edit （） 的動作呼叫相同的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="6e930-191">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="6e930-192">在 列表 3 包含修改過的連絡人控制器類別。</span><span class="sxs-lookup"><span data-stu-id="6e930-192">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="6e930-193">這個類別具有新的 ValidateContact() 方法呼叫中將 create （） 與 edit （） 的動作。</span><span class="sxs-lookup"><span data-stu-id="6e930-193">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="6e930-194">**Listing 3 - Controllers\ContactController.cs**</span><span class="sxs-lookup"><span data-stu-id="6e930-194">**Listing 3 - Controllers\ContactController.cs**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="6e930-195">總結</span><span class="sxs-lookup"><span data-stu-id="6e930-195">Summary</span></span>

<span data-ttu-id="6e930-196">在這個反覆項目，我們加入基本表單驗證我們的連絡人管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-196">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="6e930-197">我們將驗證邏輯可防止使用者提交新的連絡人或編輯現有的連絡人，而不需要提供 FirstName 和 LastName 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6e930-197">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="6e930-198">此外，使用者必須提供有效的電話號碼和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="6e930-198">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="6e930-199">在這個反覆項目，我們新增的驗證邏輯至我們的連絡人管理員應用程式中最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="6e930-199">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="6e930-200">不過，混合使用我們的驗證邏輯至我們的控制器邏輯將會產生問題我們長期來看。</span><span class="sxs-lookup"><span data-stu-id="6e930-200">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="6e930-201">我們的應用程式會更難維護及修改一段時間。</span><span class="sxs-lookup"><span data-stu-id="6e930-201">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="6e930-202">中的下一個反覆項目中，我們將我們的控制器重構我們的驗證邏輯和資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="6e930-202">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="6e930-203">我們將利用數種軟體設計原則，讓我們建立更鬆散偶合，且更易於維護，應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e930-203">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6e930-204">[上一頁](iteration-2-make-the-application-look-nice-cs.md)
> [下一頁](iteration-4-make-the-application-loosely-coupled-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6e930-204">[Previous](iteration-2-make-the-application-look-nice-cs.md)
[Next](iteration-4-make-the-application-loosely-coupled-cs.md)</span></span>