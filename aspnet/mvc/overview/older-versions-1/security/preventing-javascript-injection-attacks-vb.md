---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: 防止 JavaScript 插入式攻擊（VB） |Microsoft Docs
author: StephenWalther
description: 避免發生 JavaScript 插入式攻擊和跨網站腳本攻擊。 在本教學課程中，Stephen Walther 將說明您可以如何輕鬆地取消 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: dfe09085f26c62c566649bc6f570aa25367a0f07
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624093"
---
# <a name="preventing-javascript-injection-attacks-vb"></a><span data-ttu-id="5a629-104">防止 JavaScript 插入式攻擊 (VB)</span><span class="sxs-lookup"><span data-stu-id="5a629-104">Preventing JavaScript Injection Attacks (VB)</span></span>

<span data-ttu-id="5a629-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="5a629-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="5a629-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="5a629-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> <span data-ttu-id="5a629-107">避免發生 JavaScript 插入式攻擊和跨網站腳本攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-107">Prevent JavaScript Injection Attacks and Cross-Site Scripting Attacks from happening to you.</span></span> <span data-ttu-id="5a629-108">在本教學課程中，Stephen Walther 將說明如何透過 HTML 編碼您的內容，輕鬆地對抗這些類型的攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-108">In this tutorial, Stephen Walther explains how you can easily defeat these types of attacks by HTML encoding your content.</span></span>

<span data-ttu-id="5a629-109">本教學課程的目的是要說明如何防止 ASP.NET MVC 應用程式中的 JavaScript 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-109">The goal of this tutorial is to explain how you can prevent JavaScript injection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="5a629-110">本教學課程將討論兩種保護您的網站免于遭受 JavaScript 插入式攻擊的方法。</span><span class="sxs-lookup"><span data-stu-id="5a629-110">This tutorial discusses two approaches to defending your website against a JavaScript injection attack.</span></span> <span data-ttu-id="5a629-111">您將瞭解如何藉由編碼所顯示的資料，來防止 JavaScript 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-111">You learn how to prevent JavaScript injection attacks by encoding the data that you display.</span></span> <span data-ttu-id="5a629-112">您也將瞭解如何藉由編碼您接受的資料，來防止 JavaScript 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-112">You also learn how to prevent JavaScript injection attacks by encoding the data that you accept.</span></span>

## <a name="what-is-a-javascript-injection-attack"></a><span data-ttu-id="5a629-113">什麼是 JavaScript 插入式攻擊？</span><span class="sxs-lookup"><span data-stu-id="5a629-113">What is a JavaScript Injection Attack?</span></span>

<span data-ttu-id="5a629-114">每當您接受使用者輸入並重新顯示使用者輸入時，您就會開啟您的網站以進行 JavaScript 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-114">Whenever you accept user input and redisplay the user input, you open your website to JavaScript injection attacks.</span></span> <span data-ttu-id="5a629-115">讓我們來檢查對 JavaScript 插入式攻擊開放的實體應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a629-115">Let's examine a concrete application that is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="5a629-116">假設您已建立客戶意見反應網站（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="5a629-116">Imagine that you have created a customer feedback website (see Figure 1).</span></span> <span data-ttu-id="5a629-117">客戶可以造訪網站，並輸入您的產品使用經驗的意見反應。</span><span class="sxs-lookup"><span data-stu-id="5a629-117">Customers can visit the website and enter feedback on their experience using your products.</span></span> <span data-ttu-id="5a629-118">當客戶提交意見反應時，意見反應會顯示在 [意見反應] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="5a629-118">When a customer submits their feedback, the feedback is redisplayed on the feedback page.</span></span>

<span data-ttu-id="5a629-119">[![客戶意見反應網站](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5a629-119">[![Customer Feedback Website](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span></span>

<span data-ttu-id="5a629-120">**圖 01**：客戶意見反應網站（[按一下以觀看完整大小的影像](preventing-javascript-injection-attacks-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="5a629-120">**Figure 01**: Customer Feedback Website ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image3.png))</span></span>

<span data-ttu-id="5a629-121">客戶意見反應網站使用 [清單 1] 中的 `controller`。</span><span class="sxs-lookup"><span data-stu-id="5a629-121">The customer feedback website uses the `controller` in Listing 1.</span></span> <span data-ttu-id="5a629-122">此 `controller` 包含兩個名為 `Index()` 和 `Create()`的動作。</span><span class="sxs-lookup"><span data-stu-id="5a629-122">This `controller` contains two actions named `Index()` and `Create()`.</span></span>

<span data-ttu-id="5a629-123">**清單1– `HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="5a629-123">**Listing 1 – `HomeController.vb`**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

<span data-ttu-id="5a629-124">`Index()` 方法會顯示 `Index` view。</span><span class="sxs-lookup"><span data-stu-id="5a629-124">The `Index()` method displays the `Index` view.</span></span> <span data-ttu-id="5a629-125">這個方法會藉由從資料庫中抓取意見反應（使用 LINQ to SQL 查詢），將所有先前的客戶意見反應傳遞至 `Index` view。</span><span class="sxs-lookup"><span data-stu-id="5a629-125">This method passes all of the previous customer feedback to the `Index` view by retrieving the feedback from the database (using a LINQ to SQL query).</span></span>

<span data-ttu-id="5a629-126">`Create()` 方法會建立新的意見反應專案，並將其新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="5a629-126">The `Create()` method creates a new Feedback item and adds it to the database.</span></span> <span data-ttu-id="5a629-127">客戶在表單中輸入的訊息會傳遞至 message 參數中的 `Create()` 方法。</span><span class="sxs-lookup"><span data-stu-id="5a629-127">The message that the customer enters in the form is passed to the `Create()` method in the message parameter.</span></span> <span data-ttu-id="5a629-128">隨即建立意見專案，並將訊息指派給意見專案的 [`Message`] 屬性。</span><span class="sxs-lookup"><span data-stu-id="5a629-128">A Feedback item is created and the message is assigned to the Feedback item's `Message` property.</span></span> <span data-ttu-id="5a629-129">意見專案會以 `DataContext.SubmitChanges()` 方法呼叫提交至資料庫。</span><span class="sxs-lookup"><span data-stu-id="5a629-129">The Feedback item is submitted to the database with the `DataContext.SubmitChanges()` method call.</span></span> <span data-ttu-id="5a629-130">最後，訪客會重新導向回到 [`Index`] 視圖，其中顯示所有的意見反應。</span><span class="sxs-lookup"><span data-stu-id="5a629-130">Finally, the visitor is redirected back to the `Index` view where all of the feedback is displayed.</span></span>

<span data-ttu-id="5a629-131">[`Index`] 視圖包含在 [清單 2] 中。</span><span class="sxs-lookup"><span data-stu-id="5a629-131">The `Index` view is contained in Listing 2.</span></span>

<span data-ttu-id="5a629-132">**清單2– `Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="5a629-132">**Listing 2 – `Index.aspx`**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

<span data-ttu-id="5a629-133">[`Index`] 視圖有兩個區段。</span><span class="sxs-lookup"><span data-stu-id="5a629-133">The `Index` view has two sections.</span></span> <span data-ttu-id="5a629-134">頂端區段包含實際的客戶意見反應表單。</span><span class="sxs-lookup"><span data-stu-id="5a629-134">The top section contains the actual customer feedback form.</span></span> <span data-ttu-id="5a629-135">底部區段包含適用于. 的。每個迴圈會逐一查看所有先前的客戶意見反應專案，並顯示每個意見專案的 EntryDate 和訊息屬性。</span><span class="sxs-lookup"><span data-stu-id="5a629-135">The bottom section contains a For..Each loop that loops through all of the previous customer feedback items and displays the EntryDate and Message properties for each feedback item.</span></span>

<span data-ttu-id="5a629-136">客戶意見反應網站是一個簡單的網站。</span><span class="sxs-lookup"><span data-stu-id="5a629-136">The customer feedback website is a simple website.</span></span> <span data-ttu-id="5a629-137">可惜的是，此網站已開放給 JavaScript 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-137">Unfortunately, the website is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="5a629-138">假設您在 [客戶意見反應] 表單中輸入下列文字：</span><span class="sxs-lookup"><span data-stu-id="5a629-138">Imagine that you enter the following text into the customer feedback form:</span></span>

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

<span data-ttu-id="5a629-139">此文字代表會顯示警示訊息方塊的 JavaScript 腳本。</span><span class="sxs-lookup"><span data-stu-id="5a629-139">This text represents a JavaScript script that displays an alert message box.</span></span> <span data-ttu-id="5a629-140">有人將此腳本提交到意見反應表單之後，訊息<em>Boo！</em>每當有人造訪客戶意見反應網站時，就會出現（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="5a629-140">After someone submits this script into the feedback form, the message <em>Boo!</em>will appear whenever anyone visits the customer feedback website in the future (see Figure 2).</span></span>

<span data-ttu-id="5a629-141">[![JavaScript 插入](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5a629-141">[![JavaScript Injection](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span></span>

<span data-ttu-id="5a629-142">**圖 02**： JavaScript 插入（[按一下以查看完整大小的影像](preventing-javascript-injection-attacks-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="5a629-142">**Figure 02**: JavaScript Injection ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image6.png))</span></span>

<span data-ttu-id="5a629-143">現在，您對 JavaScript 插入式攻擊的初始回應可能會動力。</span><span class="sxs-lookup"><span data-stu-id="5a629-143">Now, your initial response to JavaScript injection attacks might be apathy.</span></span> <span data-ttu-id="5a629-144">您可能認為 JavaScript 插入式攻擊只是一*種攻擊的*類型。</span><span class="sxs-lookup"><span data-stu-id="5a629-144">You might think that JavaScript injection attacks are simply a type of *defacement* attack.</span></span> <span data-ttu-id="5a629-145">您可能會認為沒有人可以藉由認可 JavaScript 插入式攻擊來執行任何真正的麻煩。</span><span class="sxs-lookup"><span data-stu-id="5a629-145">You might believe that no one can do anything truly evil by committing a JavaScript injection attack.</span></span>

<span data-ttu-id="5a629-146">可惜的是，駭客可以藉由將 JavaScript 插入網站中，來執行一些真正的惡意專案。</span><span class="sxs-lookup"><span data-stu-id="5a629-146">Unfortunately, a hacker can do some really, really evil things by injecting JavaScript into a website.</span></span> <span data-ttu-id="5a629-147">您可以使用 JavaScript 插入式攻擊來執行跨網站腳本（XSS）攻擊。</span><span class="sxs-lookup"><span data-stu-id="5a629-147">You can use a JavaScript injection attack to perform a Cross-Site Scripting (XSS) attack.</span></span> <span data-ttu-id="5a629-148">在跨網站腳本攻擊中，您會竊取機密的使用者資訊，並將資訊傳送至另一個網站。</span><span class="sxs-lookup"><span data-stu-id="5a629-148">In a Cross-Site Scripting attack, you steal confidential user information and send the information to another website.</span></span>

<span data-ttu-id="5a629-149">例如，駭客可以使用 JavaScript 插入式攻擊，竊取其他使用者的瀏覽器 cookie 值。</span><span class="sxs-lookup"><span data-stu-id="5a629-149">For example, a hacker can use a JavaScript injection attack to steal the values of browser cookies from other users.</span></span> <span data-ttu-id="5a629-150">如果機密資訊（例如密碼、信用卡號碼或社會保險號碼）儲存在瀏覽器 cookie 中，則駭客可以使用 JavaScript 插入式攻擊來竊取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="5a629-150">If sensitive information -- such as passwords, credit card numbers, or social security numbers – is stored in the browser cookies, then a hacker can use a JavaScript injection attack to steal this information.</span></span> <span data-ttu-id="5a629-151">或者，如果使用者在含有 JavaScript 攻擊的頁面中所包含的表單欄位中輸入敏感性資訊，則駭客可以使用插入的 JavaScript 來抓取表單資料，並將它傳送至另一個網站。</span><span class="sxs-lookup"><span data-stu-id="5a629-151">Or, if a user enters sensitive information in a form field contained in a page that has been compromised with a JavaScript attack, then the hacker can use the injected JavaScript to grab the form data and send it to another website.</span></span>

<span data-ttu-id="5a629-152">*請害怕*。</span><span class="sxs-lookup"><span data-stu-id="5a629-152">*Please be scared*.</span></span> <span data-ttu-id="5a629-153">認真採取 JavaScript 插入式攻擊，並保護您的使用者機密資訊。</span><span class="sxs-lookup"><span data-stu-id="5a629-153">Take JavaScript injection attacks seriously and protect your user's confidential information.</span></span> <span data-ttu-id="5a629-154">在接下來的兩節中，我們將討論您可以用來保護 ASP.NET MVC 應用程式免于 JavaScript 插入式攻擊的兩項技術。</span><span class="sxs-lookup"><span data-stu-id="5a629-154">In the next two sections, we discuss two techniques that you can use to defend your ASP.NET MVC applications from JavaScript injection attacks.</span></span>

## <a name="approach-1-html-encode-in-the-view"></a><span data-ttu-id="5a629-155">方法 #1：在視圖中進行 HTML 編碼</span><span class="sxs-lookup"><span data-stu-id="5a629-155">Approach #1: HTML Encode in the View</span></span>

<span data-ttu-id="5a629-156">防止 JavaScript 插入式攻擊的一種簡單方法，就是在您重新顯示視圖中的資料時，以 HTML 編碼網站使用者所輸入的任何資料。</span><span class="sxs-lookup"><span data-stu-id="5a629-156">One easy method of preventing JavaScript injection attacks is to HTML encode any data entered by website users when you redisplay the data in a view.</span></span> <span data-ttu-id="5a629-157">[清單 3] 中已更新的 `Index` 視圖會遵循此方法。</span><span class="sxs-lookup"><span data-stu-id="5a629-157">The updated `Index` view in Listing 3 follows this approach.</span></span>

<span data-ttu-id="5a629-158">**清單3– `Index.aspx` （HTML 編碼）**</span><span class="sxs-lookup"><span data-stu-id="5a629-158">**Listing 3 – `Index.aspx` (HTML Encoded)**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

<span data-ttu-id="5a629-159">請注意，在以下列程式碼顯示值之前，`feedback.Message` 的值是 HTML 編碼的：</span><span class="sxs-lookup"><span data-stu-id="5a629-159">Notice that the value of `feedback.Message` is HTML encoded before the value is displayed with the following code:</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

<span data-ttu-id="5a629-160">HTML 編碼字串的意義為何？</span><span class="sxs-lookup"><span data-stu-id="5a629-160">What does it mean to HTML encode a string?</span></span> <span data-ttu-id="5a629-161">當您以 HTML 編碼字串時，`<` 和 `>` 等危險字元會由 HTML 實體參考（例如 `&lt;` 和 `&gt;`）取代。</span><span class="sxs-lookup"><span data-stu-id="5a629-161">When you HTML encode a string, dangerous characters such as `<` and `>` are replaced by HTML entity references such as `&lt;` and `&gt;`.</span></span> <span data-ttu-id="5a629-162">因此，當字串 `<script>alert("Boo!")</script>` 以 HTML 編碼時，它會轉換成 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`。</span><span class="sxs-lookup"><span data-stu-id="5a629-162">So when the string `<script>alert("Boo!")</script>` is HTML encoded, it gets converted to `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span></span> <span data-ttu-id="5a629-163">已編碼的字串在瀏覽器轉譯時，不再以 JavaScript 腳本的形式執行。</span><span class="sxs-lookup"><span data-stu-id="5a629-163">The encoded string no longer executes as a JavaScript script when interpreted by a browser.</span></span> <span data-ttu-id="5a629-164">相反地，您會在 [圖 3] 中看到無害的頁面。</span><span class="sxs-lookup"><span data-stu-id="5a629-164">Instead, you get the harmless page in Figure 3.</span></span>

<span data-ttu-id="5a629-165">[![失效的 JavaScript 攻擊](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5a629-165">[![Defeated JavaScript Attack](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span></span>

<span data-ttu-id="5a629-166">**圖 03**：通過 JavaScript 攻擊（[按一下以觀看完整大小的影像](preventing-javascript-injection-attacks-vb/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="5a629-166">**Figure 03**: Defeated JavaScript Attack ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image9.png))</span></span>

<span data-ttu-id="5a629-167">請注意，在 [清單 3] 的 [`Index`] 視圖中，只會編碼 `feedback.Message` 的值。</span><span class="sxs-lookup"><span data-stu-id="5a629-167">Notice that in the `Index` view in Listing 3 only the value of `feedback.Message` is encoded.</span></span> <span data-ttu-id="5a629-168">`feedback.EntryDate` 的值未編碼。</span><span class="sxs-lookup"><span data-stu-id="5a629-168">The value of `feedback.EntryDate` is not encoded.</span></span> <span data-ttu-id="5a629-169">您只需要對使用者輸入的資料進行編碼。</span><span class="sxs-lookup"><span data-stu-id="5a629-169">You only need to encode data entered by a user.</span></span> <span data-ttu-id="5a629-170">因為 EntryDate 的值是在控制器中產生的，所以您不需要對此值進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="5a629-170">Because the value of EntryDate was generated in the controller, you don't need to HTML encode this value.</span></span>

## <a name="approach-2-html-encode-in-the-controller"></a><span data-ttu-id="5a629-171">方法 #2：在控制器中進行 HTML 編碼</span><span class="sxs-lookup"><span data-stu-id="5a629-171">Approach #2: HTML Encode in the Controller</span></span>

<span data-ttu-id="5a629-172">您可以在將資料提交至資料庫之前，將資料進行 HTML 編碼，而不是 HTML 編碼資料。</span><span class="sxs-lookup"><span data-stu-id="5a629-172">Instead of HTML encoding data when you display the data in a view, you can HTML encode the data just before you submit the data to the database.</span></span> <span data-ttu-id="5a629-173">第二種方法是在 [清單 4] 的 `controller` 的情況下採取。</span><span class="sxs-lookup"><span data-stu-id="5a629-173">This second approach is taken in the case of the `controller` in Listing 4.</span></span>

<span data-ttu-id="5a629-174">**清單4– `HomeController.cs` （HTML 編碼）**</span><span class="sxs-lookup"><span data-stu-id="5a629-174">**Listing 4 – `HomeController.cs` (HTML Encoded)**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

<span data-ttu-id="5a629-175">請注意，在 `Create()` 動作內將值提交至資料庫之前，Message 的值是 HTML 編碼的。</span><span class="sxs-lookup"><span data-stu-id="5a629-175">Notice that the value of Message is HTML encoded before the value is submitted to the database within the `Create()` action.</span></span> <span data-ttu-id="5a629-176">當訊息在視圖中重新顯示時，訊息會以 HTML 編碼，而且不會執行任何插入訊息中的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="5a629-176">When the Message is redisplayed in the view, the Message is HTML encoded and any JavaScript injected in the Message is not executed.</span></span>

<span data-ttu-id="5a629-177">一般而言，您應該優先于本教學課程中討論的第一種方法，而不是第二種方法。</span><span class="sxs-lookup"><span data-stu-id="5a629-177">Typically, you should favor the first approach discussed in this tutorial over this second approach.</span></span> <span data-ttu-id="5a629-178">第二種方法的問題是，您的資料庫中會有 HTML 編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="5a629-178">The problem with this second approach is that you end up with HTML encoded data in your database.</span></span> <span data-ttu-id="5a629-179">換句話說，您的資料庫資料會以有趣的字元變動。</span><span class="sxs-lookup"><span data-stu-id="5a629-179">In other words, your database data is dirtied with funny looking characters.</span></span>

<span data-ttu-id="5a629-180">為什麼這不好？</span><span class="sxs-lookup"><span data-stu-id="5a629-180">Why is this bad?</span></span> <span data-ttu-id="5a629-181">如果您需要在網頁以外的地方顯示資料庫資料，就會發生問題。</span><span class="sxs-lookup"><span data-stu-id="5a629-181">If you ever need to display the database data in something other than a web page, then you will have problems.</span></span> <span data-ttu-id="5a629-182">例如，您無法再輕鬆地在 Windows Forms 應用程式中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="5a629-182">For example, you can no longer easily display the data in a Windows Forms application.</span></span>

## <a name="summary"></a><span data-ttu-id="5a629-183">總結</span><span class="sxs-lookup"><span data-stu-id="5a629-183">Summary</span></span>

<span data-ttu-id="5a629-184">本教學課程的目的是要怪嚇人您有關 JavaScript 插入式攻擊的潛在客戶。</span><span class="sxs-lookup"><span data-stu-id="5a629-184">The purpose of this tutorial was to scare you about the prospect of a JavaScript injection attack.</span></span> <span data-ttu-id="5a629-185">本教學課程討論了兩種保護 ASP.NET MVC 應用程式免于 JavaScript 插入式攻擊的方法：您可以在視圖中對使用者提交的資料進行 HTML 編碼，或您可以在控制器中對使用者提交的資料進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="5a629-185">This tutorial discussed two approaches for defending your ASP.NET MVC applications against JavaScript injection attacks: you can either HTML encode user submitted data in the view or you can HTML encode user submitted data in the controller.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5a629-186">上一篇</span><span class="sxs-lookup"><span data-stu-id="5a629-186">Previous</span></span>](authenticating-users-with-windows-authentication-vb.md)
