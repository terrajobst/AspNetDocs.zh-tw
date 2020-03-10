---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: 追蹤 ASP.NET Web Pages （Razor）網站的訪客資訊（分析） |Microsoft Docs
author: Rick-Anderson
description: 當您的網站繼續進行之後，您可能會想要分析網站流量。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525183"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="23ffc-103">追蹤 ASP.NET Web Pages （Razor）網站的訪客資訊（分析）</span><span class="sxs-lookup"><span data-stu-id="23ffc-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="23ffc-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="23ffc-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="23ffc-105">本文說明如何使用 helper 將網站分析新增至 ASP.NET Web Pages （Razor）網站中的頁面。</span><span class="sxs-lookup"><span data-stu-id="23ffc-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="23ffc-106">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="23ffc-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="23ffc-107">如何將網站流量的相關資訊傳送至分析提供者。</span><span class="sxs-lookup"><span data-stu-id="23ffc-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="23ffc-108">以下是文章中引進的 ASP.NET 程式設計功能：</span><span class="sxs-lookup"><span data-stu-id="23ffc-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="23ffc-109">`Analytics` helper。</span><span class="sxs-lookup"><span data-stu-id="23ffc-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="23ffc-110">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="23ffc-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="23ffc-111">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="23ffc-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="23ffc-112">ASP.NET Web helper 程式庫（NuGet 套件）</span><span class="sxs-lookup"><span data-stu-id="23ffc-112">ASP.NET Web Helpers Library (NuGet package)</span></span>

<span data-ttu-id="23ffc-113">分析是技術的一般詞彙，可測量您網站上的流量，讓您可以瞭解使用者使用網站的方式。</span><span class="sxs-lookup"><span data-stu-id="23ffc-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="23ffc-114">有許多分析服務可供使用，包括 Google、Yahoo、StatCounter 和其他服務。</span><span class="sxs-lookup"><span data-stu-id="23ffc-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="23ffc-115">分析的運作方式是註冊具有分析提供者的帳戶，您可以在其中登錄您要追蹤的網站。提供者會傳送 JavaScript 程式碼程式碼片段給您，其中包含您帳戶的識別碼或追蹤程式碼。</span><span class="sxs-lookup"><span data-stu-id="23ffc-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="23ffc-116">您會將 JavaScript 程式碼片段新增至您要追蹤之網站上的網頁。（您通常會將分析程式碼片段新增至頁尾或版面配置頁，或在網站中的每個頁面上顯示的其他 HTML 標籤）。當使用者要求包含其中一個 JavaScript 程式碼片段的頁面時，程式碼片段會將目前頁面的相關資訊傳送給分析提供者，以記錄有關頁面的各種詳細資料。</span><span class="sxs-lookup"><span data-stu-id="23ffc-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="23ffc-117">當您想要查看您的網站統計資料時，請登入分析提供者的網站。</span><span class="sxs-lookup"><span data-stu-id="23ffc-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="23ffc-118">接著，您可以查看網站的各種報告，例如：</span><span class="sxs-lookup"><span data-stu-id="23ffc-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="23ffc-119">個別頁面的頁面流覽次數。</span><span class="sxs-lookup"><span data-stu-id="23ffc-119">The number of page views for individual pages.</span></span> <span data-ttu-id="23ffc-120">這會告訴您（大約）有多少人造訪網站，以及您的網站上最受歡迎的網頁。</span><span class="sxs-lookup"><span data-stu-id="23ffc-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="23ffc-121">人們花在特定頁面上的時間。</span><span class="sxs-lookup"><span data-stu-id="23ffc-121">How long people spend on specific pages.</span></span> <span data-ttu-id="23ffc-122">這可能會告訴您，您的首頁是否會讓人感到滿意。</span><span class="sxs-lookup"><span data-stu-id="23ffc-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="23ffc-123">使用者造訪您的網站之前的網站。</span><span class="sxs-lookup"><span data-stu-id="23ffc-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="23ffc-124">這可協助您瞭解流量是否來自連結、搜尋等。</span><span class="sxs-lookup"><span data-stu-id="23ffc-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="23ffc-125">當人們造訪您的網站時，以及它們的持續時間。</span><span class="sxs-lookup"><span data-stu-id="23ffc-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="23ffc-126">您的訪客所來自的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="23ffc-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="23ffc-127">您的訪客所使用的瀏覽器和作業系統。</span><span class="sxs-lookup"><span data-stu-id="23ffc-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="23ffc-129">使用 Helper 將分析新增至頁面</span><span class="sxs-lookup"><span data-stu-id="23ffc-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="23ffc-130">ASP.NET Web Pages 包含數個分析協助程式（`Analytics.GetGoogleHtml`、`Analytics.GetYahooHtml`和 `Analytics.GetStatCounterHtml`），可讓您輕鬆地管理用於分析的 JavaScript 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="23ffc-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="23ffc-131">您只需要將 helper 新增至頁面，而不是找出 JavaScript 程式碼的儲存方式和位置。</span><span class="sxs-lookup"><span data-stu-id="23ffc-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="23ffc-132">您需要提供的唯一資訊是您的帳戶名稱、識別碼或追蹤程式碼。</span><span class="sxs-lookup"><span data-stu-id="23ffc-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="23ffc-133">（對於 StatCounter，您也必須提供一些額外的值）。</span><span class="sxs-lookup"><span data-stu-id="23ffc-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="23ffc-134">在這個程式中，您將建立使用 `GetGoogleHtml` helper 的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="23ffc-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="23ffc-135">如果您已經有一個具有其他其中一個分析提供者的帳戶，您可以改為使用該帳戶，並視需要進行些許調整。</span><span class="sxs-lookup"><span data-stu-id="23ffc-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="23ffc-136">當您建立分析帳戶時，您會註冊您想要追蹤之網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="23ffc-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="23ffc-137">如果您要測試本機電腦上的所有專案，則不會追蹤實際的流量（唯一的流量是您），因此您將無法記錄及查看網站統計資料。</span><span class="sxs-lookup"><span data-stu-id="23ffc-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="23ffc-138">但此程式會顯示如何將分析協助程式新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="23ffc-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="23ffc-139">當您發佈網站時，即時網站會將資訊傳送給您的分析提供者。</span><span class="sxs-lookup"><span data-stu-id="23ffc-139">When you publish your site, the live site will send information to your analytics provider.</span></span>

1. <span data-ttu-id="23ffc-140">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未新增）。</span><span class="sxs-lookup"><span data-stu-id="23ffc-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="23ffc-141">使用 Google Analytics 建立帳戶並記錄帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="23ffc-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="23ffc-142">建立名為 [*分析*] 的版面配置頁，並新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="23ffc-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="23ffc-143">您必須將呼叫放在網頁主體（在 `</body>` 標記之前）中的 `Analytics` helper。</span><span class="sxs-lookup"><span data-stu-id="23ffc-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="23ffc-144">否則，瀏覽器將不會執行腳本。</span><span class="sxs-lookup"><span data-stu-id="23ffc-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="23ffc-145">如果您使用不同的分析提供者，請改為使用下列其中一個協助程式：</span><span class="sxs-lookup"><span data-stu-id="23ffc-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="23ffc-146">（Yahoo） `@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="23ffc-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="23ffc-147">（StatCounter） `@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="23ffc-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="23ffc-148">以您在步驟1中建立的帳戶、識別碼或追蹤程式碼的名稱取代 `myaccount`。</span><span class="sxs-lookup"><span data-stu-id="23ffc-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="23ffc-149">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="23ffc-149">Run the page in the browser.</span></span> <span data-ttu-id="23ffc-150">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）</span><span class="sxs-lookup"><span data-stu-id="23ffc-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="23ffc-151">在瀏覽器中，查看頁面來源。</span><span class="sxs-lookup"><span data-stu-id="23ffc-151">In the browser, view the page source.</span></span> <span data-ttu-id="23ffc-152">您將能夠看到轉譯的分析程式碼：</span><span class="sxs-lookup"><span data-stu-id="23ffc-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="23ffc-153">登入 Google Analytics 網站，並檢查您網站的統計資料。</span><span class="sxs-lookup"><span data-stu-id="23ffc-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="23ffc-154">如果您是在即時網站上執行頁面，您會看到一個專案，將造訪記錄到您的頁面。</span><span class="sxs-lookup"><span data-stu-id="23ffc-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="23ffc-155">其他資源</span><span class="sxs-lookup"><span data-stu-id="23ffc-155">Additional Resources</span></span>

- [<span data-ttu-id="23ffc-156">Google Analytics 網站</span><span class="sxs-lookup"><span data-stu-id="23ffc-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="23ffc-157">Yahoo！ Web Analytics 網站</span><span class="sxs-lookup"><span data-stu-id="23ffc-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="23ffc-158">StatCounter 網站</span><span class="sxs-lookup"><span data-stu-id="23ffc-158">StatCounter site</span></span>](http://statcounter.com/)
