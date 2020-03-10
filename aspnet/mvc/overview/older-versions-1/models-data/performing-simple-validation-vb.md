---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: 執行簡單的驗證（VB） |Microsoft Docs
author: StephenWalther
description: 瞭解如何在 ASP.NET MVC 應用程式中執行驗證。 在本教學課程中，Stephen Walther 會為您介紹模型狀態和驗證 HTML helper 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 46925f22b7dfc23f2bb89b8d2fff0cbd8ae49062
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542928"
---
# <a name="performing-simple-validation-vb"></a><span data-ttu-id="81f46-104">執行簡單的驗證 (VB)</span><span class="sxs-lookup"><span data-stu-id="81f46-104">Performing Simple Validation (VB)</span></span>

<span data-ttu-id="81f46-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="81f46-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="81f46-106">瞭解如何在 ASP.NET MVC 應用程式中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="81f46-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="81f46-107">在本教學課程中，Stephen Walther 會為您介紹模型狀態和驗證 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="81f46-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>

<span data-ttu-id="81f46-108">本教學課程的目的是要說明如何在 ASP.NET MVC 應用程式中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="81f46-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="81f46-109">例如，您會瞭解如何防止某人提交不包含必要欄位值的表單。</span><span class="sxs-lookup"><span data-stu-id="81f46-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="81f46-110">您將瞭解如何使用模型狀態和驗證 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="81f46-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="81f46-111">瞭解模型狀態</span><span class="sxs-lookup"><span data-stu-id="81f46-111">Understanding Model State</span></span>

<span data-ttu-id="81f46-112">您可以使用模型狀態或更精確的模型狀態字典，來表示驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="81f46-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="81f46-113">例如，[清單 1] 中的 Create （）動作會先驗證 Product 類別的屬性，再將 Product 類別加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="81f46-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>

<span data-ttu-id="81f46-114">我不建議您將驗證或資料庫邏輯新增至控制器。</span><span class="sxs-lookup"><span data-stu-id="81f46-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="81f46-115">控制器應該只包含與應用程式流程式控制制相關的邏輯。</span><span class="sxs-lookup"><span data-stu-id="81f46-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="81f46-116">我們會帶一個快捷方式，讓事情保持簡單。</span><span class="sxs-lookup"><span data-stu-id="81f46-116">We are taking a shortcut to keep things simple.</span></span>

<span data-ttu-id="81f46-117">**清單 1-Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="81f46-117">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

<span data-ttu-id="81f46-118">在 [清單 1] 中，會驗證 Product 類別的名稱、描述和庫存屬性。</span><span class="sxs-lookup"><span data-stu-id="81f46-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="81f46-119">如果其中任何一個屬性無法通過驗證測試，則會將錯誤加入至模型狀態字典（以 Controller 類別的 ModelState 屬性工作表示）。</span><span class="sxs-lookup"><span data-stu-id="81f46-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="81f46-120">如果模型狀態中有任何錯誤，則 ModelState 屬性會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="81f46-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="81f46-121">在此情況下，會重新顯示用於建立新產品的 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="81f46-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="81f46-122">否則，如果沒有驗證錯誤，就會將新的產品新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="81f46-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="81f46-123">使用驗證協助程式</span><span class="sxs-lookup"><span data-stu-id="81f46-123">Using the Validation Helpers</span></span>

<span data-ttu-id="81f46-124">ASP.NET MVC 架構包含兩個驗證協助程式： ValidationMessage （）協助程式和 ValidationSummary （） helper。</span><span class="sxs-lookup"><span data-stu-id="81f46-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="81f46-125">您會在視圖中使用這兩個協助程式來顯示驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="81f46-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="81f46-126">ValidationMessage （）和 ValidationSummary （） helper 會用於 ASP.NET MVC 樣板自動產生的 Create 和 Edit views。</span><span class="sxs-lookup"><span data-stu-id="81f46-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="81f46-127">請遵循下列步驟來產生 Create view：</span><span class="sxs-lookup"><span data-stu-id="81f46-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="81f46-128">以滑鼠右鍵按一下產品控制器中的 [建立] （）動作，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="81f46-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="81f46-129">在 [**加入視圖**] 對話方塊中，核取標示為 [**建立強型別的視圖**] 的核取方塊（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="81f46-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="81f46-130">從 [ **View data class** ] 下拉式清單中，選取 [Product] 類別。</span><span class="sxs-lookup"><span data-stu-id="81f46-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="81f46-131">從 [**視圖內容**] 下拉式清單中，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="81f46-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="81f46-132">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81f46-132">Click the **Add** button.</span></span>

<span data-ttu-id="81f46-133">請確定您已建立應用程式，然後再加入視圖。</span><span class="sxs-lookup"><span data-stu-id="81f46-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="81f46-134">否則，類別清單將不會出現在 [ **View data class** ] 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="81f46-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>

<span data-ttu-id="81f46-135">[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="81f46-135">[![The New Project dialog box](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="81f46-136">**圖 01**：加入視圖（[按一下以觀看完整大小的影像](performing-simple-validation-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="81f46-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-vb/_static/image2.png))</span></span>

<span data-ttu-id="81f46-137">[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="81f46-137">[![The New Project dialog box](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)</span></span>

<span data-ttu-id="81f46-138">**圖 02**：建立強型別視圖（[按一下以觀看完整大小的影像](performing-simple-validation-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="81f46-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-vb/_static/image4.png))</span></span>

<span data-ttu-id="81f46-139">完成這些步驟之後，您會在 [清單 2] 中看到 [建立] 視圖。</span><span class="sxs-lookup"><span data-stu-id="81f46-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

<span data-ttu-id="81f46-140">**清單 2-Views\Product\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="81f46-140">**Listing 2 - Views\Product\Create.aspx**</span></span>

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

<span data-ttu-id="81f46-141">在 [清單 2] 中，Html. ValidationSummary （） helper 會緊接在 HTML 表單的正上方呼叫。</span><span class="sxs-lookup"><span data-stu-id="81f46-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="81f46-142">此 helper 用來顯示驗證錯誤訊息的清單。</span><span class="sxs-lookup"><span data-stu-id="81f46-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="81f46-143">ValidationSummary （） helper 會以項目符號清單呈現錯誤。</span><span class="sxs-lookup"><span data-stu-id="81f46-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="81f46-144">每個 HTML 表單欄位旁都會呼叫 ValidationMessage （） helper。</span><span class="sxs-lookup"><span data-stu-id="81f46-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="81f46-145">此 helper 可用來在表單欄位旁顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="81f46-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="81f46-146">在 [清單 2] 的案例中，ValidationMessage （） helper 會在發生錯誤時顯示星號。</span><span class="sxs-lookup"><span data-stu-id="81f46-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="81f46-147">[圖 3] 中的頁面說明當提交表單時，驗證協助程式所呈現的錯誤訊息，其中包含遺漏的欄位和不正確值。</span><span class="sxs-lookup"><span data-stu-id="81f46-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>

<span data-ttu-id="81f46-148">[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="81f46-148">[![The New Project dialog box](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)</span></span>

<span data-ttu-id="81f46-149">**圖 03**：以問題提交的建立視圖（[按一下以查看完整大小的影像](performing-simple-validation-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="81f46-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-vb/_static/image6.png))</span></span>

<span data-ttu-id="81f46-150">請注意，當發生驗證錯誤時，HTML 輸入欄位的外觀也會一併修改。</span><span class="sxs-lookup"><span data-stu-id="81f46-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="81f46-151">當有與 Html. TextBox （） helper 所呈現之屬性相關聯的驗證錯誤時，Html. TextBox （） helper 會轉譯*class = "input--error"* 屬性。</span><span class="sxs-lookup"><span data-stu-id="81f46-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="81f46-152">有三個級聯樣式表類別可用來控制驗證錯誤的外觀：</span><span class="sxs-lookup"><span data-stu-id="81f46-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="81f46-153">輸入-驗證-錯誤-適用于 Html. TextBox （） helper 所轉譯的 &lt;輸入&gt; 標記。</span><span class="sxs-lookup"><span data-stu-id="81f46-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="81f46-154">欄位驗證-錯誤-套用至 ValidationMessage （） helper 所呈現的 &lt;範圍&gt; 標記。</span><span class="sxs-lookup"><span data-stu-id="81f46-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="81f46-155">驗證-摘要-錯誤-適用于 ValidationSummary （） helper 所轉譯的 &lt;ul&gt; 標記。</span><span class="sxs-lookup"><span data-stu-id="81f46-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSummary() helper.</span></span>

<span data-ttu-id="81f46-156">您可以修改這些級聯樣式表類別，藉由修改位於 Content 資料夾中的 .css 檔案，修改驗證錯誤的外觀。</span><span class="sxs-lookup"><span data-stu-id="81f46-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="81f46-157">HtmlHelper 類別包含唯讀的靜態屬性，可用於抓取驗證相關的 CSS 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="81f46-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="81f46-158">這些靜態屬性的名稱為 ValidationInputCssClassName、ValidationFieldCssClassName 和 ValidationSummaryCssClassName。</span><span class="sxs-lookup"><span data-stu-id="81f46-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>

## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="81f46-159">Prebinding 驗證和 Postbinding 驗證</span><span class="sxs-lookup"><span data-stu-id="81f46-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="81f46-160">如果您提交用來建立產品的 HTML 表單，而且您在 [價格] 欄位中輸入不正確值，而且沒有 [庫存] 欄位的值，則您會取得如 [圖 4] 所示的驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="81f46-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="81f46-161">這些驗證錯誤訊息來自何處？</span><span class="sxs-lookup"><span data-stu-id="81f46-161">Where do these validation error messages come from?</span></span>

<span data-ttu-id="81f46-162">[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="81f46-162">[![The New Project dialog box](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)</span></span>

<span data-ttu-id="81f46-163">**圖 04**： Prebinding 驗證錯誤（[按一下以查看完整大小的影像](performing-simple-validation-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="81f46-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-vb/_static/image8.png))</span></span>

<span data-ttu-id="81f46-164">實際上有兩種類型的驗證錯誤訊息：在 HTML 表單欄位之前所產生的會系結至類別，以及在表單欄位系結至類別之後所產生的訊息。</span><span class="sxs-lookup"><span data-stu-id="81f46-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="81f46-165">換句話說，有 prebinding 的驗證錯誤和 postbinding 驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="81f46-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="81f46-166">[清單 1] 中的產品控制器所公開的 Create （）動作會接受 Product 類別的實例。</span><span class="sxs-lookup"><span data-stu-id="81f46-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="81f46-167">Create 方法的簽章看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="81f46-167">The signature of the Create method looks like this:</span></span>

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

<span data-ttu-id="81f46-168">[建立] 表單中的 HTML 表單欄位值會透過稱為「模型系結器」的專案系結至 productToCreate 類別。</span><span class="sxs-lookup"><span data-stu-id="81f46-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="81f46-169">預設模型系結器會在無法將表單欄位系結至表單內容時，自動將錯誤訊息新增至模型狀態。</span><span class="sxs-lookup"><span data-stu-id="81f46-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="81f46-170">預設的模型系結器無法將字串 "apple" 系結至 Product 類別的 Price 屬性。</span><span class="sxs-lookup"><span data-stu-id="81f46-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="81f46-171">您無法將字串指派給 decimal 屬性。</span><span class="sxs-lookup"><span data-stu-id="81f46-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="81f46-172">因此，模型系結器會將錯誤新增至模型狀態。</span><span class="sxs-lookup"><span data-stu-id="81f46-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="81f46-173">預設的模型系結器也不能將值指定為不接受值任何的屬性。</span><span class="sxs-lookup"><span data-stu-id="81f46-173">The default model binder also cannot assign the value Nothing to a property that does not accept the value Nothing.</span></span> <span data-ttu-id="81f46-174">特別的是，模型系結器無法將值指派給「庫存」屬性。</span><span class="sxs-lookup"><span data-stu-id="81f46-174">In particular, the model binder cannot assign the value Nothing to the UnitsInStock property.</span></span> <span data-ttu-id="81f46-175">同樣地，模型系結器會啟動並將錯誤訊息加入至模型狀態。</span><span class="sxs-lookup"><span data-stu-id="81f46-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="81f46-176">如果您想要自訂這些 prebinding 錯誤訊息的外觀，則需要建立這些訊息的資源字串。</span><span class="sxs-lookup"><span data-stu-id="81f46-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="81f46-177">總結</span><span class="sxs-lookup"><span data-stu-id="81f46-177">Summary</span></span>

<span data-ttu-id="81f46-178">本教學課程的目的是要說明 ASP.NET MVC 架構中驗證的基本機制。</span><span class="sxs-lookup"><span data-stu-id="81f46-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="81f46-179">您已瞭解如何使用模型狀態和驗證 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="81f46-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="81f46-180">我們也討論了 prebinding 和 postbinding 驗證之間的區別。</span><span class="sxs-lookup"><span data-stu-id="81f46-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="81f46-181">在其他教學課程中，我們將討論將您的驗證程式代碼移出控制器和模型類別的各種策略。</span><span class="sxs-lookup"><span data-stu-id="81f46-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="81f46-182">[上一頁](displaying-a-table-of-database-data-vb.md)
> [下一頁](validating-with-the-idataerrorinfo-interface-vb.md)</span><span class="sxs-lookup"><span data-stu-id="81f46-182">[Previous](displaying-a-table-of-database-data-vb.md)
[Next](validating-with-the-idataerrorinfo-interface-vb.md)</span></span>
