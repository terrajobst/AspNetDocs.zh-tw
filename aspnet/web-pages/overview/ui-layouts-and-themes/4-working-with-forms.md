---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: 在 ASP.NET Web Pages （Razor）網站中使用 HTML 表單 |Microsoft Docs
author: Rick-Anderson
description: 表單是 HTML 檔案的一個區段，您可以在其中放置使用者輸入控制項，例如文字方塊、核取方塊、選項按鈕和下拉式清單。 您可以使用表單 wh 。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639703"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="b1046-104">在 ASP.NET Web Pages （Razor）網站中使用 HTML 表單</span><span class="sxs-lookup"><span data-stu-id="b1046-104">Working with HTML Forms in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="b1046-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b1046-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b1046-106">本文說明當您在 ASP.NET Web Pages （Razor）網站中工作時，如何處理 HTML 表單（使用文字方塊和按鈕）。</span><span class="sxs-lookup"><span data-stu-id="b1046-106">This article describes how to process an HTML form (with text boxes and buttons) when you are working in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="b1046-107">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="b1046-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="b1046-108">如何建立 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="b1046-108">How to create an HTML form.</span></span>
> - <span data-ttu-id="b1046-109">如何從表單讀取使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="b1046-109">How to read user input from the form.</span></span>
> - <span data-ttu-id="b1046-110">如何驗證使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="b1046-110">How to validate user input.</span></span>
> - <span data-ttu-id="b1046-111">如何在提交頁面之後還原表單值。</span><span class="sxs-lookup"><span data-stu-id="b1046-111">How to restore form values after the page is submitted.</span></span>
> 
> <span data-ttu-id="b1046-112">以下是文章中引進的 ASP.NET 程式設計概念：</span><span class="sxs-lookup"><span data-stu-id="b1046-112">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="b1046-113">`Request` 物件。</span><span class="sxs-lookup"><span data-stu-id="b1046-113">The `Request` object.</span></span>
> - <span data-ttu-id="b1046-114">輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="b1046-114">Input validation.</span></span>
> - <span data-ttu-id="b1046-115">HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="b1046-115">HTML encoding.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b1046-116">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="b1046-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b1046-117">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="b1046-117">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="b1046-118">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="b1046-118">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="creating-a-simple-html-form"></a><span data-ttu-id="b1046-119">建立簡單的 HTML 表單</span><span class="sxs-lookup"><span data-stu-id="b1046-119">Creating a Simple HTML Form</span></span>

1. <span data-ttu-id="b1046-120">建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="b1046-120">Create a new website.</span></span>
2. <span data-ttu-id="b1046-121">在根資料夾中，建立名為*Form. cshtml*的網頁，並輸入下列標記：</span><span class="sxs-lookup"><span data-stu-id="b1046-121">In the root folder, create a web page named *Form.cshtml* and enter the following markup:</span></span>

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. <span data-ttu-id="b1046-122">在您的瀏覽器中啟動頁面。</span><span class="sxs-lookup"><span data-stu-id="b1046-122">Launch the page in your browser.</span></span> <span data-ttu-id="b1046-123">（在 WebMatrix 的 [檔案 **] 工作區**中，以滑鼠右鍵按一下檔案，然後選取 [**在瀏覽器中啟動**]。）其中會顯示具有三個輸入欄位和 [**提交**] 按鈕的簡單表單。</span><span class="sxs-lookup"><span data-stu-id="b1046-123">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.) A simple form with three input fields and a **Submit** button is displayed.</span></span>

    ![具有三個文字方塊的表單螢幕擷取畫面。](4-working-with-forms/_static/image1.png)

    <span data-ttu-id="b1046-125">此時，如果您按一下 [**提交**] 按鈕，就不會發生任何事。</span><span class="sxs-lookup"><span data-stu-id="b1046-125">At this point, if you click the **Submit** button, nothing happens.</span></span> <span data-ttu-id="b1046-126">若要讓表單有用，您必須新增一些將在伺服器上執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1046-126">To make the form useful, you have to add some code that will run on the server.</span></span>

## <a name="reading-user-input-from-the-form"></a><span data-ttu-id="b1046-127">讀取表單中的使用者輸入</span><span class="sxs-lookup"><span data-stu-id="b1046-127">Reading User Input from the Form</span></span>

<span data-ttu-id="b1046-128">若要處理表單，您可以加入程式碼來讀取已提交的域值，並對它們執行一些作業。</span><span class="sxs-lookup"><span data-stu-id="b1046-128">To process the form, you add code that reads the submitted field values and does something with them.</span></span> <span data-ttu-id="b1046-129">此程式說明如何讀取欄位，並在頁面上顯示使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="b1046-129">This procedure shows you how to read the fields and display the user input on the page.</span></span> <span data-ttu-id="b1046-130">（在生產應用程式中，您通常會使用使用者輸入來執行更有趣的事情。</span><span class="sxs-lookup"><span data-stu-id="b1046-130">(In a production application, you generally do more interesting things with user input.</span></span> <span data-ttu-id="b1046-131">您會在有關使用資料庫的文章中執行此動作）。</span><span class="sxs-lookup"><span data-stu-id="b1046-131">You'll do that in the article about working with databases.)</span></span>

1. <span data-ttu-id="b1046-132">在*表單 cshtml*檔案的頂端，輸入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b1046-132">At the top of the *Form.cshtml* file, enter the following code:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    <span data-ttu-id="b1046-133">當使用者第一次要求頁面時，只會顯示空白表單。</span><span class="sxs-lookup"><span data-stu-id="b1046-133">When the user first requests the page, only the empty form is displayed.</span></span> <span data-ttu-id="b1046-134">使用者（也就是您）填滿表單，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="b1046-134">The user (which will be you) fills in the form and then clicks **Submit**.</span></span> <span data-ttu-id="b1046-135">這會將使用者輸入提交（張貼）到伺服器。</span><span class="sxs-lookup"><span data-stu-id="b1046-135">This submits (posts) the user input to the server.</span></span> <span data-ttu-id="b1046-136">根據預設，要求會移至相同的頁面（也就是*表單. cshtml*）。</span><span class="sxs-lookup"><span data-stu-id="b1046-136">By default, the request goes to the same page (namely, *Form.cshtml*).</span></span>

    <span data-ttu-id="b1046-137">當您這次提交頁面時，您輸入的值會顯示在表單的正上方：</span><span class="sxs-lookup"><span data-stu-id="b1046-137">When you submit the page this time, the values you entered are displayed just above the form:</span></span>

    ![顯示您已輸入的值顯示在頁面上的螢幕擷取畫面。](4-working-with-forms/_static/image2.png)

    <span data-ttu-id="b1046-139">查看頁面的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1046-139">Look at the code for the page.</span></span> <span data-ttu-id="b1046-140">您會先使用 `IsPost` 方法來判斷頁面是否正在張貼&#8212; ，也就是使用者是否按下 [**提交**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1046-140">You first use the `IsPost` method to determine whether the page is being posted &#8212; that is, whether a user clicked the **Submit** button.</span></span> <span data-ttu-id="b1046-141">如果這是 post，`IsPost` 會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="b1046-141">If this is a post, `IsPost` returns true.</span></span> <span data-ttu-id="b1046-142">這是 ASP.NET Web Pages 中的標準方式，可決定您是使用初始要求（GET 要求）還是回傳（POST 要求）。</span><span class="sxs-lookup"><span data-stu-id="b1046-142">This is the standard way in ASP.NET Web Pages to determine whether you're working with an initial request (a GET request) or a postback (a POST request).</span></span> <span data-ttu-id="b1046-143">（如需 GET 和 POST 的詳細資訊，請參閱[使用 Razor 語法的 ASP.NET Web Pages 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)中的「HTTP GET 和 Post 和 IsPost 屬性」提要欄位）。</span><span class="sxs-lookup"><span data-stu-id="b1046-143">(For more information about GET and POST, see the sidebar "HTTP GET and POST and the IsPost Property" in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)</span></span>

    <span data-ttu-id="b1046-144">接下來，您會取得使用者從 `Request.Form` 物件填入的值，並將它們放在變數中以供日後查看。</span><span class="sxs-lookup"><span data-stu-id="b1046-144">Next, you get the values that the user filled in from the `Request.Form` object, and you put them in variables for later.</span></span> <span data-ttu-id="b1046-145">`Request.Form` 物件包含所有以頁面提交的值，每個都是由索引鍵所識別。</span><span class="sxs-lookup"><span data-stu-id="b1046-145">The `Request.Form` object contains all the values that were submitted with the page, each identified by a key.</span></span> <span data-ttu-id="b1046-146">索引鍵等同于您想要讀取之表單欄位的 `name` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b1046-146">The key is the equivalent to the `name` attribute of the form field that you want to read.</span></span> <span data-ttu-id="b1046-147">例如，若要讀取 `companyname` 欄位（文字方塊），您可以使用 `Request.Form["companyname"]`。</span><span class="sxs-lookup"><span data-stu-id="b1046-147">For example, to read the `companyname` field (text box), you use `Request.Form["companyname"]`.</span></span>

    <span data-ttu-id="b1046-148">表單值會以字串形式儲存在 `Request.Form` 物件中。</span><span class="sxs-lookup"><span data-stu-id="b1046-148">Form values are stored in the `Request.Form` object as strings.</span></span> <span data-ttu-id="b1046-149">因此，當您必須使用值做為數位或日期或其他類型時，您必須將它從字串轉換為該類型。</span><span class="sxs-lookup"><span data-stu-id="b1046-149">Therefore, when you have to work with a value as a number or a date or some other type, you have to convert it from a string to that type.</span></span> <span data-ttu-id="b1046-150">在此範例中，`Request.Form` 的 `AsInt` 方法是用來將 employees 欄位的值（包含員工計數）轉換成整數。</span><span class="sxs-lookup"><span data-stu-id="b1046-150">In the example, the `AsInt` method of the `Request.Form` is used to convert the value of the employees field (which contains an employee count) to an integer.</span></span>
2. <span data-ttu-id="b1046-151">在您的瀏覽器中啟動頁面，填寫表單欄位，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="b1046-151">Launch the page in your browser, fill in the form fields, and click **Submit**.</span></span> <span data-ttu-id="b1046-152">此頁面會顯示您所輸入的值。</span><span class="sxs-lookup"><span data-stu-id="b1046-152">The page displays the values you entered.</span></span>

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a><span data-ttu-id="b1046-153">外觀和安全性的 HTML 編碼方式</span><span class="sxs-lookup"><span data-stu-id="b1046-153">HTML Encoding for Appearance and Security</span></span>
> 
> <span data-ttu-id="b1046-154">HTML 對 `<`、`>`和 `&`等字元具有特殊用途。</span><span class="sxs-lookup"><span data-stu-id="b1046-154">HTML has special uses for characters like `<`, `>`, and `&`.</span></span> <span data-ttu-id="b1046-155">如果這些特殊字元出現在非預期的位置，則可能會破壞網頁的外觀和功能。</span><span class="sxs-lookup"><span data-stu-id="b1046-155">If these special characters appear where they're not expected, they can ruin the appearance and functionality of your web page.</span></span> <span data-ttu-id="b1046-156">例如，瀏覽器會將 `<` 字元（除非後面接著空格）解讀為 HTML 元素的開頭，例如 `<b>` 或 `<input ...>`。</span><span class="sxs-lookup"><span data-stu-id="b1046-156">For example, the browser interprets the `<` character (unless it's followed by a space) as the beginning of an HTML element, like `<b>` or `<input ...>`.</span></span> <span data-ttu-id="b1046-157">如果瀏覽器無法辨識元素，它就會捨棄開頭為 `<` 的字串，直到到達它可再次辨識的內容。</span><span class="sxs-lookup"><span data-stu-id="b1046-157">If the browser doesn't recognize the element, it simply discards the string that begins with `<` until it reaches something that it again recognizes.</span></span> <span data-ttu-id="b1046-158">很明顯地，這可能會導致頁面中出現一些奇怪的呈現。</span><span class="sxs-lookup"><span data-stu-id="b1046-158">Obviously, this can result in some weird rendering in the page.</span></span>
> 
> <span data-ttu-id="b1046-159">HTML 編碼會以瀏覽器解讀為正確符號的程式碼來取代這些保留字元。</span><span class="sxs-lookup"><span data-stu-id="b1046-159">HTML encoding replaces these reserved characters with a code that browsers interpret as the correct symbol.</span></span> <span data-ttu-id="b1046-160">例如，`<` 字元會取代為 `&lt;`，而 `>` 字元則會取代為 `&gt;`。</span><span class="sxs-lookup"><span data-stu-id="b1046-160">For example, the `<` character is replaced with `&lt;` and the `>` character is replaced with `&gt;`.</span></span> <span data-ttu-id="b1046-161">瀏覽器會以您想要查看的字元呈現這些取代字串。</span><span class="sxs-lookup"><span data-stu-id="b1046-161">The browser renders these replacement strings as the characters that you want to see.</span></span>
> 
> <span data-ttu-id="b1046-162">當您顯示從使用者所提供的字串（輸入）時，使用 HTML 編碼是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="b1046-162">It's a good idea to use HTML encoding any time you display strings (input) that you got from a user.</span></span> <span data-ttu-id="b1046-163">如果您沒有這麼做，使用者可以嘗試讓網頁執行惡意腳本，或執行其他動作來危害您的網站安全性，或者這不是您想要的東西。</span><span class="sxs-lookup"><span data-stu-id="b1046-163">If you don't, a user can try to get your web page to run a malicious script or do something else that compromises your site security or that's just not what you intend.</span></span> <span data-ttu-id="b1046-164">（這對於您採取使用者輸入、將它儲存在其他地方，然後在稍後&#8212;顯示，例如，作為 blog 批註、使用者評論或像這樣）的情況下特別重要。</span><span class="sxs-lookup"><span data-stu-id="b1046-164">(This is particularly important if you take user input, store it someplace, and then display it later &#8212; for example, as a blog comment, user review, or something like that.)</span></span>
> 
> <span data-ttu-id="b1046-165">為協助避免這些問題，ASP.NET Web Pages 會自動對您從程式碼輸出的任何文字內容進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="b1046-165">To help prevent these problems, ASP.NET Web Pages automatically HTML-encodes any text content that you output from your code.</span></span> <span data-ttu-id="b1046-166">例如，當您使用 `@MyVar`之類的程式碼顯示變數或運算式的內容時，ASP.NET Web Pages 會自動將輸出編碼。</span><span class="sxs-lookup"><span data-stu-id="b1046-166">For example, when you display the content of a variable or an expression using code such as `@MyVar`, ASP.NET Web Pages automatically encodes the output.</span></span>

## <a name="validating-user-input"></a><span data-ttu-id="b1046-167">驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="b1046-167">Validating User Input</span></span>

<span data-ttu-id="b1046-168">使用者犯了錯誤。</span><span class="sxs-lookup"><span data-stu-id="b1046-168">Users make mistakes.</span></span> <span data-ttu-id="b1046-169">您要求他們填寫欄位，並忘了，或要求他們輸入員工人數，並改為鍵入名稱。</span><span class="sxs-lookup"><span data-stu-id="b1046-169">You ask them to fill in a field, and they forget to, or you ask them to enter the number of employees and they type a name instead.</span></span> <span data-ttu-id="b1046-170">若要確定表單在處理之前已正確填入，請驗證使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="b1046-170">To make sure that a form has been filled in correctly before you process it, you validate the user's input.</span></span>

<span data-ttu-id="b1046-171">此程式示範如何驗證所有三個表單欄位，以確保使用者不會將其保留空白。</span><span class="sxs-lookup"><span data-stu-id="b1046-171">This procedure shows how to validate all three form fields to make sure the user didn't leave them blank.</span></span> <span data-ttu-id="b1046-172">您也可以檢查員工計數值是否為數字。</span><span class="sxs-lookup"><span data-stu-id="b1046-172">You also check that the employee count value is a number.</span></span> <span data-ttu-id="b1046-173">如果發生錯誤，您將會顯示錯誤訊息，告知使用者哪些值未通過驗證。</span><span class="sxs-lookup"><span data-stu-id="b1046-173">If there are errors, you'll display an error message that tells the user what values didn't pass validation.</span></span>

1. <span data-ttu-id="b1046-174">在*形式的 cshtml*檔案中，以下列程式碼取代第一個程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="b1046-174">In the *Form.cshtml* file, replace the first block of code with the following code:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    <span data-ttu-id="b1046-175">若要驗證使用者輸入，您可以使用 `Validation` helper。</span><span class="sxs-lookup"><span data-stu-id="b1046-175">To validate user input, you use the `Validation` helper.</span></span> <span data-ttu-id="b1046-176">您可以藉由呼叫 `Validation.RequireField`來註冊所需的欄位。</span><span class="sxs-lookup"><span data-stu-id="b1046-176">You register required fields by calling `Validation.RequireField`.</span></span> <span data-ttu-id="b1046-177">您可以藉由呼叫 `Validation.Add` 並指定要驗證的欄位以及要執行的驗證類型，來註冊其他類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="b1046-177">You register other types of validation by calling `Validation.Add` and specifying the field to validate and the type of validation to perform.</span></span>

    <span data-ttu-id="b1046-178">當頁面執行時，ASP.NET 會為您執行所有驗證。</span><span class="sxs-lookup"><span data-stu-id="b1046-178">When the page runs, ASP.NET does all the validation for you.</span></span> <span data-ttu-id="b1046-179">您可以藉由呼叫 `Validation.IsValid`來檢查結果，如果通過所有專案，則會傳回 true，如果有任何欄位驗證失敗，則傳回 false。</span><span class="sxs-lookup"><span data-stu-id="b1046-179">You can check the results by calling `Validation.IsValid`, which returns true if everything passed and false if any field failed validation.</span></span> <span data-ttu-id="b1046-180">一般來說，您會在對使用者輸入執行任何處理之前，先呼叫 `Validation.IsValid`。</span><span class="sxs-lookup"><span data-stu-id="b1046-180">Typically, you call `Validation.IsValid` before you perform any processing on the user input.</span></span>
2. <span data-ttu-id="b1046-181">藉由新增三個對 `Html.ValidationMessage` 方法的呼叫來更新 `<body>` 元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b1046-181">Update the `<body>` element by adding three calls to the `Html.ValidationMessage` method, like this:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    <span data-ttu-id="b1046-182">若要顯示驗證錯誤訊息，您可以呼叫 Html。`ValidationMessage`</span><span class="sxs-lookup"><span data-stu-id="b1046-182">To display validation error messages, you can call Html.`ValidationMessage`</span></span> <span data-ttu-id="b1046-183">並將您想要訊息的功能變數名稱傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="b1046-183">and pass it the name of the field that you want the message for.</span></span>
3. <span data-ttu-id="b1046-184">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="b1046-184">Run the page.</span></span> <span data-ttu-id="b1046-185">將欄位保留空白，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="b1046-185">Leave the fields blank and click **Submit**.</span></span> <span data-ttu-id="b1046-186">您會看到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b1046-186">You see error messages.</span></span>

    ![螢幕擷取畫面：顯示使用者輸入未通過驗證時所顯示的錯誤訊息。](4-working-with-forms/_static/image3.jpg)
4. <span data-ttu-id="b1046-188">將字串（例如，"ABC"）新增至 [**員工計數**] 欄位，然後再按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="b1046-188">Add a string (for example, "ABC") to the **Employee Count** field and click **Submit** again.</span></span> <span data-ttu-id="b1046-189">此時您會看到錯誤，指出字串不是正確的格式，也就是整數。</span><span class="sxs-lookup"><span data-stu-id="b1046-189">This time you see an error that indicates that the string isn't in the right format, namely, an integer.</span></span>

    ![螢幕擷取畫面：顯示使用者輸入 [員工] 欄位的字串時所顯示的錯誤訊息。](4-working-with-forms/_static/image4.jpg)

<span data-ttu-id="b1046-191">ASP.NET Web Pages 提供更多選項來驗證使用者輸入，包括能夠使用用戶端腳本自動執行驗證，讓使用者可以在瀏覽器中取得立即的意見反應。</span><span class="sxs-lookup"><span data-stu-id="b1046-191">ASP.NET Web Pages provides more options for validating user input, including the ability to automatically perform validation using client script, so that users get immediate feedback in the browser.</span></span> <span data-ttu-id="b1046-192">如需詳細資訊，請參閱稍後的[其他資源](#Additional_Resources)一節。</span><span class="sxs-lookup"><span data-stu-id="b1046-192">See the [Additional Resources](#Additional_Resources) section later for more information.</span></span>

## <a name="restoring-form-values-after-postbacks"></a><span data-ttu-id="b1046-193">回傳後還原表單值</span><span class="sxs-lookup"><span data-stu-id="b1046-193">Restoring Form Values After Postbacks</span></span>

<span data-ttu-id="b1046-194">當您測試上一節中的頁面時，您可能已經注意到，如果發生驗證錯誤，您輸入的所有專案（不只是不正確資料）都會消失，而且您必須重新輸入所有欄位的值。</span><span class="sxs-lookup"><span data-stu-id="b1046-194">When you tested the page in the previous section, you might have noticed that if you had a validation error, everything you entered (not just the invalid data) was gone, and you had to re-enter values for all the fields.</span></span> <span data-ttu-id="b1046-195">這說明一個重點：當您提交頁面、處理它，然後再次轉譯頁面時，會從頭重新建立頁面。</span><span class="sxs-lookup"><span data-stu-id="b1046-195">This illustrates an important point: when you submit a page, process it, and then render the page again, the page is re-created from scratch.</span></span> <span data-ttu-id="b1046-196">如您所見，這表示提交的頁面中的任何值都會遺失。</span><span class="sxs-lookup"><span data-stu-id="b1046-196">As you saw, this means that any values that were in the page when it was submitted are lost.</span></span>

<span data-ttu-id="b1046-197">不過，您可以輕鬆地修正此問題。</span><span class="sxs-lookup"><span data-stu-id="b1046-197">You can fix this easily, however.</span></span> <span data-ttu-id="b1046-198">您可以存取已提交的值（在 `Request.Form` 物件中，因此當呈現頁面時，您可以將這些值填回表單欄位中。</span><span class="sxs-lookup"><span data-stu-id="b1046-198">You have access to the values that were submitted (in the `Request.Form` object, so you can fill those values back into the form fields when the page is rendered.</span></span>

1. <span data-ttu-id="b1046-199">在 *. cshtml*檔案中，使用 `value` 屬性取代 `<input>` 元素的 `value` 屬性：</span><span class="sxs-lookup"><span data-stu-id="b1046-199">In the *Form.cshtml* file, replace the `value` attributes of the `<input>` elements using the `value` attribute.:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    <span data-ttu-id="b1046-200">已設定 `<input>` 元素的 `value` 屬性，以動態方式從 `Request.Form` 物件讀取域值。</span><span class="sxs-lookup"><span data-stu-id="b1046-200">The `value` attribute of the `<input>` elements has been set to dynamically read the field value out of the `Request.Form` object.</span></span> <span data-ttu-id="b1046-201">第一次要求頁面時，`Request.Form` 物件中的值都是空的。</span><span class="sxs-lookup"><span data-stu-id="b1046-201">The first time that the page is requested, the values in the `Request.Form` object are all empty.</span></span> <span data-ttu-id="b1046-202">這沒什麼問題，因為表單是空白的。</span><span class="sxs-lookup"><span data-stu-id="b1046-202">This is fine, because that way the form is blank.</span></span>
2. <span data-ttu-id="b1046-203">在您的瀏覽器中啟動頁面，填寫表單欄位或將其保留空白，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="b1046-203">Launch the page in your browser, fill in the form fields or leave them blank, and click **Submit**.</span></span> <span data-ttu-id="b1046-204">隨即會顯示顯示已提交值的頁面。</span><span class="sxs-lookup"><span data-stu-id="b1046-204">A page that shows the submitted values is displayed.</span></span>

    ![表單-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="b1046-206">其他資源</span><span class="sxs-lookup"><span data-stu-id="b1046-206">Additional Resources</span></span>

- [<span data-ttu-id="b1046-207">從 Web 使用者取得輸入的1001方式</span><span class="sxs-lookup"><span data-stu-id="b1046-207">1,001 Ways to Get Input from Web Users</span></span>](https://msdn.microsoft.com/library/ms971057.aspx)
- <span data-ttu-id="b1046-208">[使用表單和處理使用者輸入](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span><span class="sxs-lookup"><span data-stu-id="b1046-208">[Using Forms and Processing User Input](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span></span>
- [<span data-ttu-id="b1046-209">在 ASP.NET Web Pages 網站中驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="b1046-209">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
- <span data-ttu-id="b1046-210">[在 HTML 表單中使用自動完成](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="b1046-210">[Using AutoComplete in HTML Forms](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span></span>
