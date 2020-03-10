---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '反復專案 #3 –新增表單驗證（VB） |Microsoft Docs'
author: microsoft
description: 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證 emai 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544447"
---
# <a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="89e6c-105">反復專案 #3 –新增表單驗證（VB）</span><span class="sxs-lookup"><span data-stu-id="89e6c-105">Iteration #3 – Add form validation (VB)</span></span>

<span data-ttu-id="89e6c-106">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="89e6c-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="89e6c-107">下載程式代碼</span><span class="sxs-lookup"><span data-stu-id="89e6c-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="89e6c-108">在第三個反復專案中，我們會新增基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="89e6c-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="89e6c-109">我們會防止人們提交表單，而不需要完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="89e6c-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="89e6c-110">我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="89e6c-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="89e6c-111">建立連絡人管理 ASP.NET MVC 應用程式（VB）</span><span class="sxs-lookup"><span data-stu-id="89e6c-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="89e6c-112">在這一系列的教學課程中，我們從一開始就建立了整個連絡人管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="89e6c-113">連絡人管理員應用程式可讓您儲存連絡人資訊名稱、電話號碼和電子郵件地址，以取得人員清單。</span><span class="sxs-lookup"><span data-stu-id="89e6c-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="89e6c-114">我們會透過多個反復專案來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="89e6c-115">在每次反覆運算時，我們會逐漸改善應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="89e6c-116">這個多個反復專案方法的目標，是要讓您瞭解每項變更的原因。</span><span class="sxs-lookup"><span data-stu-id="89e6c-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="89e6c-117">反復專案 #1-建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="89e6c-118">在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。</span><span class="sxs-lookup"><span data-stu-id="89e6c-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="89e6c-119">我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。</span><span class="sxs-lookup"><span data-stu-id="89e6c-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="89e6c-120">反復專案 #2-讓應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="89e6c-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="89e6c-121">在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。</span><span class="sxs-lookup"><span data-stu-id="89e6c-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="89e6c-122">反復專案 #3-新增表單驗證。</span><span class="sxs-lookup"><span data-stu-id="89e6c-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="89e6c-123">在第三個反復專案中，我們會新增基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="89e6c-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="89e6c-124">我們會防止人們提交表單，而不需要完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="89e6c-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="89e6c-125">我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="89e6c-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="89e6c-126">反復專案 #4-讓應用程式鬆散結合。</span><span class="sxs-lookup"><span data-stu-id="89e6c-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="89e6c-127">在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="89e6c-128">例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="89e6c-129">反復專案 #5-建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="89e6c-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="89e6c-130">在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。</span><span class="sxs-lookup"><span data-stu-id="89e6c-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="89e6c-131">我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="89e6c-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="89e6c-132">反復專案 #6-使用以測試為導向的開發。</span><span class="sxs-lookup"><span data-stu-id="89e6c-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="89e6c-133">在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="89e6c-134">在此反復專案中，我們會新增連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="89e6c-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="89e6c-135">反復專案 #7-新增 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="89e6c-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="89e6c-136">在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。</span><span class="sxs-lookup"><span data-stu-id="89e6c-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="89e6c-137">這個反復專案</span><span class="sxs-lookup"><span data-stu-id="89e6c-137">This Iteration</span></span>

<span data-ttu-id="89e6c-138">在 Contact Manager 應用程式的第二個反復專案中，我們新增了基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="89e6c-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="89e6c-139">我們會防止人們提交連絡人，而不需要輸入必要表單欄位的值。</span><span class="sxs-lookup"><span data-stu-id="89e6c-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="89e6c-140">我們也會驗證電話號碼和電子郵件地址（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="89e6c-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="89e6c-141">[![[新增專案] 對話方塊](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="89e6c-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="89e6c-142">**圖 01**：具有驗證的表單（[按一下以觀看完整大小的影像](iteration-3-add-form-validation-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="89e6c-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>

<span data-ttu-id="89e6c-143">在此反復專案中，我們會將驗證邏輯直接新增至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="89e6c-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="89e6c-144">一般來說，這不是將驗證新增至 ASP.NET MVC 應用程式的建議方式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="89e6c-145">較好的方法是將應用程式的驗證邏輯放在不同的[服務層](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。</span><span class="sxs-lookup"><span data-stu-id="89e6c-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="89e6c-146">在下一個反復專案中，我們會重構 Contact Manager 應用程式，讓應用程式更容易維護。</span><span class="sxs-lookup"><span data-stu-id="89e6c-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="89e6c-147">在此反復專案中，為了簡單起見，我們會以手動方式撰寫所有驗證程式代碼。</span><span class="sxs-lookup"><span data-stu-id="89e6c-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="89e6c-148">我們不會自行撰寫驗證程式代碼，而是可以利用驗證架構。</span><span class="sxs-lookup"><span data-stu-id="89e6c-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="89e6c-149">例如，您可以使用 Microsoft 企業程式庫驗證應用程式區塊（VAB）來執行 ASP.NET MVC 應用程式的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="89e6c-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="89e6c-150">若要深入瞭解驗證應用程式區塊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="89e6c-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="89e6c-151">將驗證新增至建立視圖</span><span class="sxs-lookup"><span data-stu-id="89e6c-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="89e6c-152">首先，讓我們先將驗證邏輯加入至 Create view。</span><span class="sxs-lookup"><span data-stu-id="89e6c-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="89e6c-153">幸運的是，因為我們產生了具有 Visual Studio 的 Create view，所以 Create view 已經包含所有必要的使用者介面邏輯來顯示驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="89e6c-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="89e6c-154">[建立] 視圖包含在 [清單 1] 中。</span><span class="sxs-lookup"><span data-stu-id="89e6c-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="89e6c-155">**清單 1-\Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="89e6c-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="89e6c-156">欄位驗證-error 類別是用來將 ValidationMessage （） helper 所呈現的輸出樣式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="89e6c-157">輸入驗證-error 類別是用來為 Html. TextBox （） helper 所轉譯的 textbox （輸入）樣式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="89e6c-158">[驗證-摘要-錯誤] 類別是用來將 ValidationSummary （） helper 所呈現的未排序清單樣式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="89e6c-159">您可以修改本節所述的樣式表單類別，以自訂驗證錯誤訊息的外觀。</span><span class="sxs-lookup"><span data-stu-id="89e6c-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="89e6c-160">將驗證邏輯新增至建立動作</span><span class="sxs-lookup"><span data-stu-id="89e6c-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="89e6c-161">現在，Create view 永遠不會顯示驗證錯誤訊息，因為我們並未撰寫邏輯來產生任何訊息。</span><span class="sxs-lookup"><span data-stu-id="89e6c-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="89e6c-162">若要顯示驗證錯誤訊息，您必須將錯誤訊息新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="89e6c-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="89e6c-163">將表單欄位的值指派給屬性時，UpdateModel （）方法會自動將錯誤訊息新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="89e6c-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="89e6c-164">例如，如果您嘗試將字串 "apple" 指派給接受 DateTime 值的生日屬性，則 UpdateModel （）方法會將錯誤新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="89e6c-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="89e6c-165">[清單 2] 中的 [已修改的 Create （）] 方法包含新的區段，它會先驗證 Contact 類別的屬性，再將新的連絡人插入資料庫。</span><span class="sxs-lookup"><span data-stu-id="89e6c-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="89e6c-166">**清單 2-Controllers\ContactController.vb （使用驗證建立）**</span><span class="sxs-lookup"><span data-stu-id="89e6c-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="89e6c-167">[驗證] 區段會強制執行四個不同的驗證規則：</span><span class="sxs-lookup"><span data-stu-id="89e6c-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="89e6c-168">FirstName 屬性的長度必須大於零（而且不能只包含空格）</span><span class="sxs-lookup"><span data-stu-id="89e6c-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="89e6c-169">LastName 屬性的長度必須大於零（而且不能只包含空格）</span><span class="sxs-lookup"><span data-stu-id="89e6c-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="89e6c-170">如果 Phone 屬性具有值（長度大於0），則電話屬性必須符合正則運算式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="89e6c-171">如果 [電子郵件] 屬性具有值（長度大於0），則 [電子郵件] 屬性必須符合正則運算式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="89e6c-172">當發生驗證規則違規時，會使用 AddModelError （）方法的協助，將錯誤訊息新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="89e6c-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="89e6c-173">當您將訊息新增至 ModelState 時，您會提供屬性的名稱和驗證錯誤訊息的文字。</span><span class="sxs-lookup"><span data-stu-id="89e6c-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="89e6c-174">此錯誤訊息會顯示在 ValidationSummary （）和 ValidationMessage （） helper 方法的視圖中。</span><span class="sxs-lookup"><span data-stu-id="89e6c-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="89e6c-175">執行驗證規則之後，會檢查 ModelState 的 IsValid 屬性。</span><span class="sxs-lookup"><span data-stu-id="89e6c-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="89e6c-176">當有任何驗證錯誤訊息新增至 ModelState 時，IsValid 屬性會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="89e6c-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="89e6c-177">如果驗證失敗，則會重新顯示 [建立] 表單，並顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="89e6c-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="89e6c-178">我從正則運算式儲存機制取得用來驗證電話號碼和電子郵件地址的正則運算式， [ *http://regexlib.com* ](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="89e6c-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="89e6c-179">將驗證邏輯加入至編輯動作</span><span class="sxs-lookup"><span data-stu-id="89e6c-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="89e6c-180">編輯（）動作會更新連絡人。</span><span class="sxs-lookup"><span data-stu-id="89e6c-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="89e6c-181">編輯（）動作必須執行與 Create （）動作完全相同的驗證。</span><span class="sxs-lookup"><span data-stu-id="89e6c-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="89e6c-182">我們應該重構 Contact controller，讓 Create （）和 Edit （）動作都呼叫相同的驗證方法，而不是複製相同的驗證程式代碼。</span><span class="sxs-lookup"><span data-stu-id="89e6c-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="89e6c-183">已修改的連絡人控制器類別包含在 [清單 3] 中。</span><span class="sxs-lookup"><span data-stu-id="89e6c-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="89e6c-184">這個類別具有新的 ValidateContact （）方法，它會在 Create （）和 Edit （）動作中同時呼叫。</span><span class="sxs-lookup"><span data-stu-id="89e6c-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="89e6c-185">**清單 3-Controllers\ContactController.vb**</span><span class="sxs-lookup"><span data-stu-id="89e6c-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="89e6c-186">總結</span><span class="sxs-lookup"><span data-stu-id="89e6c-186">Summary</span></span>

<span data-ttu-id="89e6c-187">在此反復專案中，我們已將基本表單驗證新增至我們的 Contact Manager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="89e6c-188">我們的驗證邏輯會防止使用者提交新的連絡人，或編輯現有的連絡人，而不需要提供 FirstName 和 LastName 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="89e6c-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="89e6c-189">此外，使用者必須提供有效的電話號碼和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="89e6c-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="89e6c-190">在此反復專案中，我們以最簡單的方式將驗證邏輯新增至連絡人管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="89e6c-191">不過，將我們的驗證邏輯混用在控制器邏輯中，將會為我們長期建立問題。</span><span class="sxs-lookup"><span data-stu-id="89e6c-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="89e6c-192">我們的應用程式會更容易維護及修改一段時間。</span><span class="sxs-lookup"><span data-stu-id="89e6c-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="89e6c-193">在下一個反復專案中，我們將會從我們的控制器重構驗證邏輯和資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="89e6c-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="89e6c-194">我們將利用數個軟體設計原則，讓我們能夠建立更鬆散結合且更容易維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e6c-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="89e6c-195">[上一頁](iteration-2-make-the-application-look-nice-vb.md)
> [下一頁](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="89e6c-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
