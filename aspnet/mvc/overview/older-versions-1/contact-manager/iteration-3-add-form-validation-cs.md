---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: '反復專案 #3 –新增表單驗C#證（） |Microsoft Docs'
author: microsoft
description: 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證 emai 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: af2e86e820f60f0a3d8e3db8f78eba67ef63579a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544468"
---
# <a name="iteration-3--add-form-validation-c"></a><span data-ttu-id="fbb29-105">反復專案 #3 –新增表單驗C#證（）</span><span class="sxs-lookup"><span data-stu-id="fbb29-105">Iteration #3 – Add form validation (C#)</span></span>

<span data-ttu-id="fbb29-106">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fbb29-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="fbb29-107">下載程式代碼</span><span class="sxs-lookup"><span data-stu-id="fbb29-107">Download Code</span></span>](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> <span data-ttu-id="fbb29-108">在第三個反復專案中，我們會新增基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="fbb29-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="fbb29-109">我們會防止人們提交表單，而不需要完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="fbb29-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="fbb29-110">我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="fbb29-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="fbb29-111">建立連絡人管理 ASP.NET MVC 應用程式（C#）</span><span class="sxs-lookup"><span data-stu-id="fbb29-111">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="fbb29-112">在這一系列的教學課程中，我們從一開始就建立了整個連絡人管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="fbb29-113">連絡人管理員應用程式可讓您儲存連絡人資訊名稱、電話號碼和電子郵件地址，以取得人員清單。</span><span class="sxs-lookup"><span data-stu-id="fbb29-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="fbb29-114">我們會透過多個反復專案來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="fbb29-115">在每次反覆運算時，我們會逐漸改善應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="fbb29-116">這個多個反復專案方法的目標，是要讓您瞭解每項變更的原因。</span><span class="sxs-lookup"><span data-stu-id="fbb29-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="fbb29-117">反復專案 #1-建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="fbb29-118">在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。</span><span class="sxs-lookup"><span data-stu-id="fbb29-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="fbb29-119">我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。</span><span class="sxs-lookup"><span data-stu-id="fbb29-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="fbb29-120">反復專案 #2-讓應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="fbb29-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="fbb29-121">在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。</span><span class="sxs-lookup"><span data-stu-id="fbb29-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="fbb29-122">反復專案 #3-新增表單驗證。</span><span class="sxs-lookup"><span data-stu-id="fbb29-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="fbb29-123">在第三個反復專案中，我們會新增基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="fbb29-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="fbb29-124">我們會防止人們提交表單，而不需要完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="fbb29-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="fbb29-125">我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="fbb29-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="fbb29-126">反復專案 #4-讓應用程式鬆散結合。</span><span class="sxs-lookup"><span data-stu-id="fbb29-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="fbb29-127">在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="fbb29-128">例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="fbb29-129">反復專案 #5-建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="fbb29-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="fbb29-130">在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。</span><span class="sxs-lookup"><span data-stu-id="fbb29-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="fbb29-131">我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="fbb29-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="fbb29-132">反復專案 #6-使用以測試為導向的開發。</span><span class="sxs-lookup"><span data-stu-id="fbb29-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="fbb29-133">在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="fbb29-134">在此反復專案中，我們會新增連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="fbb29-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="fbb29-135">反復專案 #7-新增 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="fbb29-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="fbb29-136">在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。</span><span class="sxs-lookup"><span data-stu-id="fbb29-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="fbb29-137">這個反復專案</span><span class="sxs-lookup"><span data-stu-id="fbb29-137">This Iteration</span></span>

<span data-ttu-id="fbb29-138">在 Contact Manager 應用程式的第二個反復專案中，我們新增了基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="fbb29-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="fbb29-139">我們會防止人們提交連絡人，而不需要輸入必要表單欄位的值。</span><span class="sxs-lookup"><span data-stu-id="fbb29-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="fbb29-140">我們也會驗證電話號碼和電子郵件地址（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="fbb29-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="fbb29-141">[![[新增專案] 對話方塊](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fbb29-141">[![The New Project dialog box](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="fbb29-142">**圖 01**：具有驗證的表單（[按一下以觀看完整大小的影像](iteration-3-add-form-validation-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="fbb29-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-cs/_static/image2.png))</span></span>

<span data-ttu-id="fbb29-143">在此反復專案中，我們會將驗證邏輯直接新增至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="fbb29-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="fbb29-144">一般來說，這不是將驗證新增至 ASP.NET MVC 應用程式的建議方式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="fbb29-145">較好的方法是將應用程式的驗證邏輯放在不同的[服務層](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。</span><span class="sxs-lookup"><span data-stu-id="fbb29-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="fbb29-146">在下一個反復專案中，我們會重構 Contact Manager 應用程式，讓應用程式更容易維護。</span><span class="sxs-lookup"><span data-stu-id="fbb29-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="fbb29-147">在此反復專案中，為了簡單起見，我們會以手動方式撰寫所有驗證程式代碼。</span><span class="sxs-lookup"><span data-stu-id="fbb29-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="fbb29-148">我們不會自行撰寫驗證程式代碼，而是可以利用驗證架構。</span><span class="sxs-lookup"><span data-stu-id="fbb29-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="fbb29-149">例如，您可以使用 Microsoft 企業程式庫驗證應用程式區塊（VAB）來執行 ASP.NET MVC 應用程式的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="fbb29-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="fbb29-150">若要深入瞭解驗證應用程式區塊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="fbb29-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="fbb29-151">將驗證新增至建立視圖</span><span class="sxs-lookup"><span data-stu-id="fbb29-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="fbb29-152">首先，讓我們先將驗證邏輯加入至 Create view。</span><span class="sxs-lookup"><span data-stu-id="fbb29-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="fbb29-153">幸運的是，因為我們產生了具有 Visual Studio 的 Create view，所以 Create view 已經包含所有必要的使用者介面邏輯來顯示驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="fbb29-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="fbb29-154">[建立] 視圖包含在 [清單 1] 中。</span><span class="sxs-lookup"><span data-stu-id="fbb29-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="fbb29-155">**清單 1-\Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="fbb29-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

<span data-ttu-id="fbb29-156">請注意，ValidationSummary （） helper 方法的呼叫會出現在 HTML 表單的正上方。</span><span class="sxs-lookup"><span data-stu-id="fbb29-156">Notice the call to the Html.ValidationSummary() helper method that appears immediately above the HTML form.</span></span> <span data-ttu-id="fbb29-157">如果有驗證錯誤訊息，則此方法會以項目符號清單顯示驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="fbb29-157">If there are validation error messages, then this method displays validation messages in a bulleted list.</span></span>

<span data-ttu-id="fbb29-158">另外也請注意，ValidationMessage （）的呼叫會出現在每個表單欄位旁。</span><span class="sxs-lookup"><span data-stu-id="fbb29-158">Notice, furthermore, the calls to Html.ValidationMessage() that appear next to each form field.</span></span> <span data-ttu-id="fbb29-159">ValidationMessage （） helper 會顯示個別的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="fbb29-159">The ValidationMessage() helper displays an individual validation error message.</span></span> <span data-ttu-id="fbb29-160">在 [清單 1] 的案例中，如果發生驗證錯誤，就會顯示星號。</span><span class="sxs-lookup"><span data-stu-id="fbb29-160">In the case of Listing 1, an asterisk is displayed when there is a validation error.</span></span>

<span data-ttu-id="fbb29-161">最後，當有與 helper 所顯示的屬性相關聯的驗證錯誤時，Html. TextBox （） helper 會自動轉譯級聯樣式表類別。</span><span class="sxs-lookup"><span data-stu-id="fbb29-161">Finally, the Html.TextBox() helper automatically renders a Cascading Style Sheet class when there is a validation error associated with the property displayed by the helper.</span></span> <span data-ttu-id="fbb29-162">Html. TextBox （） helper 會轉譯名為**input-驗證-error**的類別。</span><span class="sxs-lookup"><span data-stu-id="fbb29-162">The Html.TextBox() helper renders a class named **input-validation-error**.</span></span>

<span data-ttu-id="fbb29-163">當您建立新的 ASP.NET MVC 應用程式時，會自動在 [內容] 資料夾中建立名為 [網站. css] 的樣式表單。</span><span class="sxs-lookup"><span data-stu-id="fbb29-163">When you create a new ASP.NET MVC application, a style sheet named Site.css is created in the Content folder automatically.</span></span> <span data-ttu-id="fbb29-164">此樣式表單包含與驗證錯誤訊息外觀相關之 CSS 類別的下列定義：</span><span class="sxs-lookup"><span data-stu-id="fbb29-164">This style sheet contains the following definitions for CSS classes related to the appearance of validation error messages:</span></span>

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

<span data-ttu-id="fbb29-165">欄位驗證-error 類別是用來將 ValidationMessage （） helper 所呈現的輸出樣式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-165">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="fbb29-166">輸入驗證-error 類別是用來為 Html. TextBox （） helper 所轉譯的 textbox （輸入）樣式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-166">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="fbb29-167">[驗證-摘要-錯誤] 類別是用來將 ValidationSummary （） helper 所呈現的未排序清單樣式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-167">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="fbb29-168">您可以修改本節所述的樣式表單類別，以自訂驗證錯誤訊息的外觀。</span><span class="sxs-lookup"><span data-stu-id="fbb29-168">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="fbb29-169">將驗證邏輯新增至建立動作</span><span class="sxs-lookup"><span data-stu-id="fbb29-169">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="fbb29-170">現在，Create view 永遠不會顯示驗證錯誤訊息，因為我們並未撰寫邏輯來產生任何訊息。</span><span class="sxs-lookup"><span data-stu-id="fbb29-170">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="fbb29-171">若要顯示驗證錯誤訊息，您必須將錯誤訊息新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="fbb29-171">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="fbb29-172">將表單欄位的值指派給屬性時，UpdateModel （）方法會自動將錯誤訊息新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="fbb29-172">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="fbb29-173">例如，如果您嘗試將字串 "apple" 指派給接受 DateTime 值的生日屬性，則 UpdateModel （）方法會將錯誤新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="fbb29-173">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="fbb29-174">[清單 2] 中的 [已修改的 Create （）] 方法包含新的區段，它會先驗證 Contact 類別的屬性，再將新的連絡人插入資料庫。</span><span class="sxs-lookup"><span data-stu-id="fbb29-174">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="fbb29-175">**清單 2-Controllers\ContactController.cs （使用驗證建立）**</span><span class="sxs-lookup"><span data-stu-id="fbb29-175">**Listing 2 - Controllers\ContactController.cs (Create with validation)**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

<span data-ttu-id="fbb29-176">[驗證] 區段會強制執行四個不同的驗證規則：</span><span class="sxs-lookup"><span data-stu-id="fbb29-176">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="fbb29-177">FirstName 屬性的長度必須大於零（而且不能只包含空格）</span><span class="sxs-lookup"><span data-stu-id="fbb29-177">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="fbb29-178">LastName 屬性的長度必須大於零（而且不能只包含空格）</span><span class="sxs-lookup"><span data-stu-id="fbb29-178">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="fbb29-179">如果 Phone 屬性具有值（長度大於0），則電話屬性必須符合正則運算式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-179">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="fbb29-180">如果 [電子郵件] 屬性具有值（長度大於0），則 [電子郵件] 屬性必須符合正則運算式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-180">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="fbb29-181">當發生驗證規則違規時，會使用 AddModelError （）方法的協助，將錯誤訊息新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="fbb29-181">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="fbb29-182">當您將訊息新增至 ModelState 時，您會提供屬性的名稱和驗證錯誤訊息的文字。</span><span class="sxs-lookup"><span data-stu-id="fbb29-182">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="fbb29-183">此錯誤訊息會顯示在 ValidationSummary （）和 ValidationMessage （） helper 方法的視圖中。</span><span class="sxs-lookup"><span data-stu-id="fbb29-183">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="fbb29-184">執行驗證規則之後，會檢查 ModelState 的 IsValid 屬性。</span><span class="sxs-lookup"><span data-stu-id="fbb29-184">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="fbb29-185">當有任何驗證錯誤訊息新增至 ModelState 時，IsValid 屬性會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="fbb29-185">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="fbb29-186">如果驗證失敗，則會重新顯示 [建立] 表單，並顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="fbb29-186">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="fbb29-187">我從正則運算式儲存機制取得用來驗證電話號碼和電子郵件地址的正則運算式， [ *http://regexlib.com* ](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="fbb29-187">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="fbb29-188">將驗證邏輯加入至編輯動作</span><span class="sxs-lookup"><span data-stu-id="fbb29-188">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="fbb29-189">編輯（）動作會更新連絡人。</span><span class="sxs-lookup"><span data-stu-id="fbb29-189">The Edit() action updates a Contact.</span></span> <span data-ttu-id="fbb29-190">編輯（）動作必須執行與 Create （）動作完全相同的驗證。</span><span class="sxs-lookup"><span data-stu-id="fbb29-190">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="fbb29-191">我們應該重構 Contact controller，讓 Create （）和 Edit （）動作都呼叫相同的驗證方法，而不是複製相同的驗證程式代碼。</span><span class="sxs-lookup"><span data-stu-id="fbb29-191">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="fbb29-192">已修改的連絡人控制器類別包含在 [清單 3] 中。</span><span class="sxs-lookup"><span data-stu-id="fbb29-192">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="fbb29-193">這個類別具有新的 ValidateContact （）方法，它會在 Create （）和 Edit （）動作中同時呼叫。</span><span class="sxs-lookup"><span data-stu-id="fbb29-193">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="fbb29-194">**清單 3-Controllers\ContactController.cs**</span><span class="sxs-lookup"><span data-stu-id="fbb29-194">**Listing 3 - Controllers\ContactController.cs**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="fbb29-195">總結</span><span class="sxs-lookup"><span data-stu-id="fbb29-195">Summary</span></span>

<span data-ttu-id="fbb29-196">在此反復專案中，我們已將基本表單驗證新增至我們的 Contact Manager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-196">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="fbb29-197">我們的驗證邏輯會防止使用者提交新的連絡人，或編輯現有的連絡人，而不需要提供 FirstName 和 LastName 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="fbb29-197">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="fbb29-198">此外，使用者必須提供有效的電話號碼和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="fbb29-198">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="fbb29-199">在此反復專案中，我們以最簡單的方式將驗證邏輯新增至連絡人管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-199">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="fbb29-200">不過，將我們的驗證邏輯混用在控制器邏輯中，將會為我們長期建立問題。</span><span class="sxs-lookup"><span data-stu-id="fbb29-200">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="fbb29-201">我們的應用程式會更容易維護及修改一段時間。</span><span class="sxs-lookup"><span data-stu-id="fbb29-201">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="fbb29-202">在下一個反復專案中，我們將會從我們的控制器重構驗證邏輯和資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="fbb29-202">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="fbb29-203">我們將利用數個軟體設計原則，讓我們能夠建立更鬆散結合且更容易維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbb29-203">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fbb29-204">[上一頁](iteration-2-make-the-application-look-nice-cs.md)
> [下一頁](iteration-4-make-the-application-loosely-coupled-cs.md)</span><span class="sxs-lookup"><span data-stu-id="fbb29-204">[Previous](iteration-2-make-the-application-look-nice-cs.md)
[Next](iteration-4-make-the-application-loosely-coupled-cs.md)</span></span>
