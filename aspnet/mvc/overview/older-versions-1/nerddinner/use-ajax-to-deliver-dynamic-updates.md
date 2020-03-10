---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 傳遞動態更新 |Microsoft Docs
author: microsoft
description: 步驟10會使用以 Ajax 為基礎的方法（在晚餐詳細資料內整合），將登入使用者的支援回復為出席晚餐的相關資訊 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600846"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="19869-103">使用 AJAX 傳送動態更新</span><span class="sxs-lookup"><span data-stu-id="19869-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="19869-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="19869-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="19869-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="19869-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="19869-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟10，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="19869-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="19869-107">步驟10會使用在晚餐詳細資料頁面中整合的以 Ajax 為基礎的方法，來支援已登入的使用者，讓他們有興趣參加晚餐。</span><span class="sxs-lookup"><span data-stu-id="19869-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="19869-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="19869-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="19869-109">NerdDinner 步驟10： AJAX 啟用 RSVPs 接受</span><span class="sxs-lookup"><span data-stu-id="19869-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="19869-110">現在讓我們開始支援已登入的使用者，以在參與晚餐時將其感興趣。</span><span class="sxs-lookup"><span data-stu-id="19869-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="19869-111">我們會使用在晚餐詳細資料頁面中整合的 AJAX 型方法來啟用此程式。</span><span class="sxs-lookup"><span data-stu-id="19869-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="19869-112">指出使用者是否為 RSVP</span><span class="sxs-lookup"><span data-stu-id="19869-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="19869-113">使用者可以造訪 */Dinners/Details/[id*] URL，以查看特定晚餐的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="19869-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="19869-114">Details （）動作方法會實作為，如下所示：</span><span class="sxs-lookup"><span data-stu-id="19869-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="19869-115">執行 RSVP 支援的第一個步驟是將「IsUserRegistered （使用者名稱）」 helper 方法新增至晚餐物件（在我們先前建立的 Dinner.cs 部分類別中）。</span><span class="sxs-lookup"><span data-stu-id="19869-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="19869-116">此 helper 方法會傳回 true 或 false，取決於使用者目前是否為晚餐的 RSVP：</span><span class="sxs-lookup"><span data-stu-id="19869-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="19869-117">然後，我們可以將下列程式碼加入至 Details view 範本，以顯示適當的訊息，指出是否已針對事件註冊使用者：</span><span class="sxs-lookup"><span data-stu-id="19869-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="19869-118">現在當使用者造訪晚餐時，他們會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="19869-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="19869-119">而當他們造訪晚餐時，他們就會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="19869-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="19869-120">執行 Register 動作方法</span><span class="sxs-lookup"><span data-stu-id="19869-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="19869-121">現在讓我們新增必要的功能，讓使用者可以從 [詳細資料] 頁面取得晚餐。</span><span class="sxs-lookup"><span data-stu-id="19869-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="19869-122">若要執行這項操作，我們將建立新的 "RSVPController" 類別，方法是以滑鼠右鍵按一下 \Controllers 目錄，然後選擇 [新增-&gt;控制器] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="19869-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="19869-123">我們會在新的 RSVPController 類別內執行「註冊」動作方法，以取得晚餐的識別碼做為引數、抓取適當的晚餐物件、檢查登入的使用者目前是否在已註冊它的使用者清單中，以及請勿為他們新增 RSVP 物件：</span><span class="sxs-lookup"><span data-stu-id="19869-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="19869-124">請注意，我們如何傳回簡單字串做為動作方法的輸出。</span><span class="sxs-lookup"><span data-stu-id="19869-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="19869-125">我們可以將此訊息內嵌在視圖範本中，但因為它很小，所以我們只會在控制器基類上使用 Content （） helper 方法，並傳回上述的字串訊息。</span><span class="sxs-lookup"><span data-stu-id="19869-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="19869-126">使用 AJAX 呼叫 RSVPForEvent 動作方法</span><span class="sxs-lookup"><span data-stu-id="19869-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="19869-127">我們將使用 AJAX，從我們的詳細資料檢視叫用 Register 動作方法。</span><span class="sxs-lookup"><span data-stu-id="19869-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="19869-128">這麼做非常簡單。</span><span class="sxs-lookup"><span data-stu-id="19869-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="19869-129">首先，我們要新增兩個腳本程式庫參考：</span><span class="sxs-lookup"><span data-stu-id="19869-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="19869-130">第一個程式庫參考核心 ASP.NET AJAX 用戶端腳本程式庫。</span><span class="sxs-lookup"><span data-stu-id="19869-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="19869-131">此檔案大約24k 大小（已壓縮），並包含核心用戶端 AJAX 功能。</span><span class="sxs-lookup"><span data-stu-id="19869-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="19869-132">第二個程式庫包含公用程式函式，這些函式會與 ASP.NET MVC 的內建 AJAX helper 方法整合（我們很快就會用到）。</span><span class="sxs-lookup"><span data-stu-id="19869-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="19869-133">然後，我們可以更新稍早新增的視圖範本程式碼，讓您不會輸出「您未註冊此事件」訊息，我們會改為轉譯連結，以在推播的情況下執行可在我們的 RSVP 控制器上叫用 RSVPForEvent 動作方法的 AJAX 呼叫並 RSVPs 使用者：</span><span class="sxs-lookup"><span data-stu-id="19869-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="19869-134">上述使用的 Ajax （） helper 方法是內建的 ASP.NET MVC，類似于 Html.actionlink （） helper 方法，不同之處在于，它不會執行標準導覽，而是在按一下連結時，對動作方法進行 AJAX 呼叫。</span><span class="sxs-lookup"><span data-stu-id="19869-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="19869-135">在上述情況中，我們會在 "RSVP" 控制器上呼叫 "Register" 動作方法，並將 DinnerID 當做 "id" 參數傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="19869-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="19869-136">我們所傳遞的最後一個 AjaxOptions 參數指出我們想要從動作方法傳回的內容，並更新頁面上的 HTML &lt;div&gt; 元素，其識別碼為 "rsvpmsg"。</span><span class="sxs-lookup"><span data-stu-id="19869-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="19869-137">現在，當使用者流覽至尚未註冊的晚餐時，他們會看到其 RSVP 的連結：</span><span class="sxs-lookup"><span data-stu-id="19869-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="19869-138">如果他們按一下「此事件的 RSVP」連結，他們會對 RSVP 控制器上的 Register 動作方法進行 AJAX 呼叫，當它完成時，就會看到如下所示的更新訊息：</span><span class="sxs-lookup"><span data-stu-id="19869-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="19869-139">進行此 AJAX 呼叫時，所需的網路頻寬和流量非常輕量。</span><span class="sxs-lookup"><span data-stu-id="19869-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="19869-140">當使用者按一下「此事件的 RSVP」連結時，會對 */Dinners/Register/1* URL 提出小型的 HTTP POST 網路要求，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="19869-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="19869-141">而來自我們的 Register 動作方法的回應只是：</span><span class="sxs-lookup"><span data-stu-id="19869-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="19869-142">這個輕量呼叫很快，而且即使在慢速網路也能正常執行。</span><span class="sxs-lookup"><span data-stu-id="19869-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="19869-143">新增 jQuery 動畫</span><span class="sxs-lookup"><span data-stu-id="19869-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="19869-144">我們所實行的 AJAX 功能既順暢又快速。</span><span class="sxs-lookup"><span data-stu-id="19869-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="19869-145">不過，有時可能會發生這種情況，因為使用者可能不會注意到 RSVP 連結已被新文字取代。</span><span class="sxs-lookup"><span data-stu-id="19869-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="19869-146">為了讓結果變得更明顯，我們可以加入簡單的動畫，將注意力吸引更新訊息。</span><span class="sxs-lookup"><span data-stu-id="19869-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="19869-147">預設 ASP.NET MVC 專案範本包含 jQuery – Microsoft 也支援的絕佳（且非常熱門）開放原始碼 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="19869-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="19869-148">jQuery 提供許多功能，包括美觀的 HTML DOM 選擇和效果程式庫。</span><span class="sxs-lookup"><span data-stu-id="19869-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="19869-149">若要使用 jQuery，我們會先新增腳本參考。</span><span class="sxs-lookup"><span data-stu-id="19869-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="19869-150">因為我們會在網站內的各種地方使用 jQuery，所以我們會在網站中新增腳本參考。主版分頁檔案，讓所有頁面都可以使用它。</span><span class="sxs-lookup"><span data-stu-id="19869-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="19869-151">*秘訣：請確定您已安裝適用于 VS 2008 SP1 的 JavaScript intellisense，針對 JavaScript 檔案啟用更豐富的 intellisense 支援（包括 jQuery）。您可以從下列下載： http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="19869-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="19869-152">使用 JQuery 撰寫的程式碼通常會使用全域 "$ （）" JavaScript 方法，以使用 CSS 選取器來抓取一或多個 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="19869-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="19869-153">例如， *$ （"#rsvpmsg"）* 會選取識別碼為 rsvpmsg 的任何 HTML 元素，而 *$ （". elements"）* 會選取所有具有 "elements" CSS 類別名稱的專案。</span><span class="sxs-lookup"><span data-stu-id="19869-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="19869-154">您也可以使用選取器查詢（例如： *$ （"input [@type= 單選] [@checked]"）* ，撰寫更多先進的查詢，例如「傳回所有已核取的選項按鈕」。</span><span class="sxs-lookup"><span data-stu-id="19869-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="19869-155">選取專案之後，您可以在其上呼叫方法來採取動作，例如隱藏它們： *$ （"#rsvpmsg"）。 hide （）;*</span><span class="sxs-lookup"><span data-stu-id="19869-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="19869-156">在我們的 RSVP 案例中，我們將定義名為 "AnimateRSVPMessage" 的簡單 JavaScript 函式，以選取 "rsvpmsg" &lt;div&gt; 並以動畫呈現其文字內容的大小。</span><span class="sxs-lookup"><span data-stu-id="19869-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="19869-157">下列程式碼會啟動小型文字，然後讓它在400毫秒的時間範圍內增加：</span><span class="sxs-lookup"><span data-stu-id="19869-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="19869-158">接著，我們就可以在 AJAX 呼叫成功完成後呼叫這個 JavaScript 函式，方法是將其名稱傳遞至我們的 Ajax （） helper 方法（透過 AjaxOptions "OnSuccess" 事件屬性）：</span><span class="sxs-lookup"><span data-stu-id="19869-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="19869-159">現在，當您按一下「此事件的 RSVP」連結，而我們的 AJAX 呼叫成功完成時，送回的內容訊息會以動畫顯示並成長大：</span><span class="sxs-lookup"><span data-stu-id="19869-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="19869-160">除了提供 "OnSuccess" 事件之外，AjaxOptions 物件也會公開您可以處理的 OnBegin、OnFailure 和 OnComplete 事件（以及各種其他屬性和實用的選項）。</span><span class="sxs-lookup"><span data-stu-id="19869-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="19869-161">清除-重構 RSVP 部分視圖</span><span class="sxs-lookup"><span data-stu-id="19869-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="19869-162">我們的 details （詳細資料檢視）範本開始變得很長，這會讓您更難瞭解。</span><span class="sxs-lookup"><span data-stu-id="19869-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="19869-163">為了協助改善程式碼的可讀性，讓我們藉由建立部分視圖– RSVPStatus，封裝詳細資料頁面的所有 RSVP 視圖程式碼來完成。</span><span class="sxs-lookup"><span data-stu-id="19869-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="19869-164">若要這麼做，請以滑鼠右鍵按一下 [\Views\Dinners] 資料夾，然後選擇 [新增-&gt;View] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="19869-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="19869-165">我們會將晚餐物件做為其強型別 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="19869-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="19869-166">然後，我們可以從詳細資料 .aspx 視圖將 RSVP 內容複寫/貼上到其中。</span><span class="sxs-lookup"><span data-stu-id="19869-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="19869-167">完成之後，讓我們另外建立另一個部分視圖– EditAndDeleteLinks，用來封裝我們的編輯和刪除連結視圖程式碼。</span><span class="sxs-lookup"><span data-stu-id="19869-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="19869-168">我們也會將晚餐物件當做其強型別 ViewModel，並將 Edit 和 Delete 邏輯從我們的詳細資料 .aspx 視圖複製/貼上。</span><span class="sxs-lookup"><span data-stu-id="19869-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="19869-169">然後，我們的詳細資料檢視範本就可以在底部加入兩個 RenderPartial （）方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="19869-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="19869-170">這可讓程式碼更簡潔地進行讀取和維護。</span><span class="sxs-lookup"><span data-stu-id="19869-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="19869-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19869-171">Next Step</span></span>

<span data-ttu-id="19869-172">現在讓我們來看看如何進一步使用 AJAX，並在應用程式中加入互動式對應支援。</span><span class="sxs-lookup"><span data-stu-id="19869-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="19869-173">[上一頁](secure-applications-using-authentication-and-authorization.md)
> [下一頁](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="19869-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
