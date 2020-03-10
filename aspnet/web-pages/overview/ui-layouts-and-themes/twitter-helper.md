---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Twitter Helper 與 ASP.NET Web Pages |Microsoft Docs
author: Rick-Anderson
description: 本主題和應用程式會示範如何將 Twitter Helper 新增至您的 WebMatrix 3 專案。 其中包含 Twitter Helper 程式碼，並示範如何呼叫 Helper 。
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638555"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="716e6-104">Twitter 協助程式與 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="716e6-104">Twitter Helper with ASP.NET Web Pages</span></span>

<span data-ttu-id="716e6-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="716e6-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="716e6-106">Twitter 協助程式已過時。</span><span class="sxs-lookup"><span data-stu-id="716e6-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="716e6-107">如需 Twitter 最新的適用于網站的 engagement 工具，請參閱[twitter 的網站總覽](https://developer.twitter.com/en/docs/twitter-for-websites/overview)。</span><span class="sxs-lookup"><span data-stu-id="716e6-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="716e6-108">本主題和應用程式會示範如何將 Twitter Helper 新增至您的 WebMatrix 3 專案。</span><span class="sxs-lookup"><span data-stu-id="716e6-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="716e6-109">其中包含 Twitter Helper 程式碼，並示範如何呼叫 Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="716e6-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="716e6-110">此 Twitter 檔案的程式碼是由 Microsoft 的**Tian Pan**所開發。</span><span class="sxs-lookup"><span data-stu-id="716e6-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="716e6-111">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="716e6-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="716e6-112">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="716e6-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="716e6-113">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="716e6-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="introduction"></a><span data-ttu-id="716e6-114">簡介</span><span class="sxs-lookup"><span data-stu-id="716e6-114">Introduction</span></span>

<span data-ttu-id="716e6-115">本主題示範如何將 Twitter Helper 新增至您的應用程式，並使用 Razor 語法來呼叫 Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="716e6-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="716e6-116">Twitter Helper 可讓您輕鬆地在應用程式中併入 Twitter 按鈕和小工具。</span><span class="sxs-lookup"><span data-stu-id="716e6-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="716e6-117">若要使用 Twitter widget （例如使用者的時間軸）或主題標籤的搜尋結果，您必須先[在 Twitter 上建立 widget](https://twitter.com/settings/widgets)。</span><span class="sxs-lookup"><span data-stu-id="716e6-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="716e6-118">建立小工具之後，您會收到 widget 識別碼。呼叫顯示 widget 的 helper 方法時，您會傳遞這個 widget id 做為參數。</span><span class="sxs-lookup"><span data-stu-id="716e6-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="716e6-119">本主題是針對 Twitter API 1.1 版所撰寫。</span><span class="sxs-lookup"><span data-stu-id="716e6-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="716e6-120">藉由直接將 Twitter Helper 程式碼新增至您的專案，您可以在 Twitter API 變更時更新 Helper 程式碼。</span><span class="sxs-lookup"><span data-stu-id="716e6-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="716e6-121">如需有關安裝 WebMatrix 的詳細資訊，請參閱[ASP.NET Web Pages 2 消費者入門簡介](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="716e6-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="716e6-122">將 Twitter Helper 新增至您的專案</span><span class="sxs-lookup"><span data-stu-id="716e6-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="716e6-123">若要新增 Twitter 協助程式，請先在您的專案中新增名為**App\_** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="716e6-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="716e6-124">然後，建立名為**Twitter. cshtml**的檔案。</span><span class="sxs-lookup"><span data-stu-id="716e6-124">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code 資料夾](twitter-helper/_static/image1.png)

<span data-ttu-id="716e6-126">將 Twitter 中的預設程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="716e6-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="716e6-127">從您的網頁呼叫 Twitter 方法</span><span class="sxs-lookup"><span data-stu-id="716e6-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="716e6-128">下列範例顯示如何從專案中的頁面使用 Twitter Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="716e6-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="716e6-129">在您的專案中，您會想要將參數值取代為與您的需求相關的值。</span><span class="sxs-lookup"><span data-stu-id="716e6-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="716e6-130">您可以使用提供的 widget id 來探索方法的使用方式，但您會想要為您的專案產生您自己的小工具。</span><span class="sxs-lookup"><span data-stu-id="716e6-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="716e6-131">不需要以下顯示的所有參數。</span><span class="sxs-lookup"><span data-stu-id="716e6-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="716e6-132">選擇性參數是用來自訂按鈕或 widget 的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="716e6-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="716e6-133">例如，[下一項] 按鈕只需要遵循使用者名稱，但此範例會顯示如何包含關注者的數目，以及如何指定按鈕的大小和語言。</span><span class="sxs-lookup"><span data-stu-id="716e6-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="716e6-134">查看結果</span><span class="sxs-lookup"><span data-stu-id="716e6-134">See the results</span></span>

<span data-ttu-id="716e6-135">上述程式碼會產生下列按鈕和小工具。</span><span class="sxs-lookup"><span data-stu-id="716e6-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="716e6-136">這些按鈕和小工具都是功能完整的，而不是螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="716e6-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="716e6-137">[跟隨] 按鈕會以西班牙文顯示，因為 language 參數是設定為**es**。</span><span class="sxs-lookup"><span data-stu-id="716e6-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="716e6-138">追蹤按鈕</span><span class="sxs-lookup"><span data-stu-id="716e6-138">Follow Button</span></span>

<span data-ttu-id="716e6-139">[遵循 @aspnet）](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="716e6-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="716e6-140">推文按鈕</span><span class="sxs-lookup"><span data-stu-id="716e6-140">Tweet Button</span></span>

<span data-ttu-id="716e6-141">[推文](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="716e6-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="716e6-142">使用者時間軸（設定檔）</span><span class="sxs-lookup"><span data-stu-id="716e6-142">User Timeline (Profile)</span></span>

<span data-ttu-id="716e6-143">[@aspnet`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 推文](https://twitter.com/aspnet)</span><span class="sxs-lookup"><span data-stu-id="716e6-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="716e6-144">我的最愛</span><span class="sxs-lookup"><span data-stu-id="716e6-144">Favorites</span></span>

<span data-ttu-id="716e6-145">[@Microsoft`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 的我的最愛推文](https://twitter.com/Microsoft/favorites)</span><span class="sxs-lookup"><span data-stu-id="716e6-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="716e6-146">清單</span><span class="sxs-lookup"><span data-stu-id="716e6-146">List</span></span>

<span data-ttu-id="716e6-147">[從 @Microsoft/MS\_取用者\_的頻帶推文](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="716e6-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="716e6-148">搜尋</span><span class="sxs-lookup"><span data-stu-id="716e6-148">Search</span></span>

<span data-ttu-id="716e6-149">[&quot;#asp .net&quot;的相關推文](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="716e6-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
