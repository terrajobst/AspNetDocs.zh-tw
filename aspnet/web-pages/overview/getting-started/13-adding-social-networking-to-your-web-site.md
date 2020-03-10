---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 將社交網路新增至 ASP.NET Web Pages （Razor）網站 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何整合您的網站與社交網路服務。 在本章中，您將瞭解如何讓人員將您的網站加上書簽/連結 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526933"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a><span data-ttu-id="73b4f-104">將社交網路新增至 ASP.NET Web Pages （Razor）網站</span><span class="sxs-lookup"><span data-stu-id="73b4f-104">Adding Social Networking to ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="73b4f-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="73b4f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="73b4f-106">本文說明如何將 Facebook、Twitter、Reddit 和 Digg 的社交網路連結新增至 ASP.NET Web Pages （Razor）網站中的頁面，以及如何包含 Twitter 摘要、Xbox 玩家卡片和 Gravatar 影像。</span><span class="sxs-lookup"><span data-stu-id="73b4f-106">This article explains how to add social networking links for Facebook, Twitter, Reddit, and Digg to pages in an ASP.NET Web Pages (Razor) website, and how to include Twitter feeds, Xbox gamer cards, and Gravatar images.</span></span>
> 
> <span data-ttu-id="73b4f-107">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="73b4f-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="73b4f-108">如何讓人員加入書簽/連結您的網站。</span><span class="sxs-lookup"><span data-stu-id="73b4f-108">How to let people bookmark/link your site.</span></span>
> - <span data-ttu-id="73b4f-109">如何新增 Twitter 摘要。</span><span class="sxs-lookup"><span data-stu-id="73b4f-109">How to add a Twitter feed.</span></span>
> - <span data-ttu-id="73b4f-110">如何將 Facebook **Like**按鈕新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="73b4f-110">How to add a Facebook **Like** button to pages.</span></span>
> - <span data-ttu-id="73b4f-111">如何呈現 Gravatar.com 影像。</span><span class="sxs-lookup"><span data-stu-id="73b4f-111">How to render Gravatar.com images.</span></span>
> - <span data-ttu-id="73b4f-112">如何在您的網站上顯示 Xbox 遊戲者卡片。</span><span class="sxs-lookup"><span data-stu-id="73b4f-112">How to display an Xbox gamer card on your site.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="73b4f-113">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="73b4f-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="73b4f-114">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="73b4f-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="73b4f-115">ASP.NET Web Helper 程式庫（NuGet 套件）</span><span class="sxs-lookup"><span data-stu-id="73b4f-115">ASP.NET Web Helper Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="73b4f-116">本教學課程也適用于 ASP.NET Web Pages 3，但使用 ASP.NET Web Helper 程式庫的元件除外。</span><span class="sxs-lookup"><span data-stu-id="73b4f-116">This tutorial also works with ASP.NET Web Pages 3, except for parts that use the ASP.NET Web Helper Library.</span></span>

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a><span data-ttu-id="73b4f-117">在社交網路網站上連結您的網站</span><span class="sxs-lookup"><span data-stu-id="73b4f-117">Linking Your Website on Social Networking Sites</span></span>

<span data-ttu-id="73b4f-118">如果您的網站上有其他人，他們通常會想要與朋友分享。</span><span class="sxs-lookup"><span data-stu-id="73b4f-118">If people like something on your site, they often want to share it with friends.</span></span> <span data-ttu-id="73b4f-119">您可以藉由顯示使用者可以按一下以在 Digg、Reddit、Facebook、Twitter 或類似網站上共用頁面的圖像（圖示）來簡化這項工作。</span><span class="sxs-lookup"><span data-stu-id="73b4f-119">You can make this easy by displaying glyphs (icons) that people can click to share a page on Digg, Reddit, Facebook, Twitter, or similar sites.</span></span>

<span data-ttu-id="73b4f-120">若要顯示這些字元，請將 `LinkSharecode` helper 新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="73b4f-120">To display these glyphs, add the `LinkSharecode` helper to a page.</span></span> <span data-ttu-id="73b4f-121">造訪您頁面的人員可以按一下個別的圖像。</span><span class="sxs-lookup"><span data-stu-id="73b4f-121">People who visit your page can click an individual glyph.</span></span> <span data-ttu-id="73b4f-122">如果他們擁有具有該社交網路網站的帳戶，他們就可以在該網站上張貼您頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="73b4f-122">If they have an account with that social networking site, they can then post a link to your page on that site.</span></span>

![圖片1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. <span data-ttu-id="73b4f-124">如在[ASP.NET Web Pages 網站中安裝](https://go.microsoft.com/fwlink/?LinkId=252372)協助程式中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果您尚未新增）。-建立名為*ListLinkShare*的頁面，並新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="73b4f-124">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.- Create a page named *ListLinkShare.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    <span data-ttu-id="73b4f-125">在此範例中，當 `LinkShare` helper 執行時，會以參數的形式傳遞頁面標題，然後將頁面標題傳遞到社交網路網站。</span><span class="sxs-lookup"><span data-stu-id="73b4f-125">In this example, when the `LinkShare` helper runs, the page title is passed as a parameter, which in turn passes the page title to the social networking site.</span></span> <span data-ttu-id="73b4f-126">不過，您可以傳入任何想要的字串。</span><span class="sxs-lookup"><span data-stu-id="73b4f-126">However, you could pass in any string you want.</span></span> <span data-ttu-id="73b4f-127">這個範例也會指定要包含在清單中的社交網路網站。</span><span class="sxs-lookup"><span data-stu-id="73b4f-127">This example also specifies which social networking sites to include in the list.</span></span> <span data-ttu-id="73b4f-128">您可以指定與網站相關的社交網路網站。</span><span class="sxs-lookup"><span data-stu-id="73b4f-128">You can specify the social networking sites that are relevant to your site.</span></span>
2. <span data-ttu-id="73b4f-129">在瀏覽器中執行*ListLinkShare。*</span><span class="sxs-lookup"><span data-stu-id="73b4f-129">Run the *ListLinkShare.cshtml* page in a browser.</span></span> <span data-ttu-id="73b4f-130">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）</span><span class="sxs-lookup"><span data-stu-id="73b4f-130">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
3. <span data-ttu-id="73b4f-131">按一下您要註冊的其中一個網站的圖像。</span><span class="sxs-lookup"><span data-stu-id="73b4f-131">Click a glyph for one of the sites that you're signed up for.</span></span> <span data-ttu-id="73b4f-132">此連結會帶您前往所選社交網路網站上的頁面，您可以在其中共用連結。</span><span class="sxs-lookup"><span data-stu-id="73b4f-132">The link takes you to the page on the selected social network site where you can share a link.</span></span> <span data-ttu-id="73b4f-133">例如，如果您按一下 [Reddit] 連結，就會進入 Reddit 網站上的 [`submit to reddit`] 頁面。</span><span class="sxs-lookup"><span data-stu-id="73b4f-133">For example, if you click the Reddit link, you're taken to the `submit to reddit` page on the Reddit website.</span></span>

     ![圖片2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a><span data-ttu-id="73b4f-135">新增 Twitter 摘要</span><span class="sxs-lookup"><span data-stu-id="73b4f-135">Adding a Twitter Feed</span></span>

<span data-ttu-id="73b4f-136">如需使用 Twitter 協助程式與目前版本的 Twitter API 相容的詳細資訊，請參閱[twitter helper](../ui-layouts-and-themes/twitter-helper.md)。</span><span class="sxs-lookup"><span data-stu-id="73b4f-136">For information about using a Twitter helper that is compatible with the current version of the Twitter API, see [Twitter helper](../ui-layouts-and-themes/twitter-helper.md).</span></span> <span data-ttu-id="73b4f-137">這個範例示範如何撰寫您自己的 helper，讓您可以輕鬆地重複使用多頁的程式碼。</span><span class="sxs-lookup"><span data-stu-id="73b4f-137">This example shows how to write your own helper so you can easily reuse the code from many pages.</span></span>

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a><span data-ttu-id="73b4f-138">顯示 Facebook &quot;，例如&quot; 按鈕</span><span class="sxs-lookup"><span data-stu-id="73b4f-138">Displaying a Facebook &quot;Like&quot; Button</span></span>

<span data-ttu-id="73b4f-139">在某些情況下，最好的選擇是直接從社交網路提供者取得程式碼，而不是依賴 helper。</span><span class="sxs-lookup"><span data-stu-id="73b4f-139">In some cases, your best option is to get the code directly from the social networking provider rather than relying on a helper.</span></span> <span data-ttu-id="73b4f-140">如果社交網路提供者更新其選項的速度比協助程式更新更快，更是如此。</span><span class="sxs-lookup"><span data-stu-id="73b4f-140">This is especially true if the social network provider updates its options more quickly than the helper is updated.</span></span>

<span data-ttu-id="73b4f-141">若要將 Facebook 功能（例如 [贊] 按鈕）新增至您的網站，您可以從[developers.facebook.com](https://developers.facebook.com/)網站取出程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="73b4f-141">To add Facebook features (such as the Like button) to your site, you can retrieve code snippets from the [developers.facebook.com](https://developers.facebook.com/) site.</span></span> <span data-ttu-id="73b4f-142">在 Facebook 網站上，您可以使用其工具來產生與您的網站相關的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="73b4f-142">On the Facebook site, you use their tools to generate a code snippet that is relevant to your site.</span></span>

<span data-ttu-id="73b4f-143">下列反白顯示的程式碼是從 developers.facebook.com 網站上的 [Like] 按鈕工具中抓取的程式碼。</span><span class="sxs-lookup"><span data-stu-id="73b4f-143">The following highlighted code is the code that was retrieved from the Like Button tool on the developers.facebook.com site.</span></span> <span data-ttu-id="73b4f-144">您必須提供您自己的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="73b4f-144">You must provide your own app ID.</span></span>

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a><span data-ttu-id="73b4f-145">呈現 Gravatar 影像</span><span class="sxs-lookup"><span data-stu-id="73b4f-145">Rendering a Gravatar Image</span></span>

<span data-ttu-id="73b4f-146">*Gravatar* （&quot;全域辨識的頭像&quot;）是可在多個網站上用來作為您的頭像&#8212;的映射，也就是代表您的圖片。</span><span class="sxs-lookup"><span data-stu-id="73b4f-146">A *Gravatar* (a &quot;globally recognized avatar&quot;) is an image that can be used on multiple websites as your avatar &#8212; that is, an image that represents you.</span></span> <span data-ttu-id="73b4f-147">例如，Gravatar 可以識別論壇文章中的人員、blog 留言等等。</span><span class="sxs-lookup"><span data-stu-id="73b4f-147">For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on.</span></span> <span data-ttu-id="73b4f-148">（您可以在 Gravatar 網站註冊自己的 Gravatar，網址為[http://www.gravatar.com/](http://www.gravatar.com/)）。如果您想要在網站上的人名或電子郵件地址旁顯示影像，您可以使用 Gravatar helper。</span><span class="sxs-lookup"><span data-stu-id="73b4f-148">(You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses on your website, you can use the Gravatar helper.</span></span>

<span data-ttu-id="73b4f-149">在此範例中，您是使用代表自己的單一 Gravatar。</span><span class="sxs-lookup"><span data-stu-id="73b4f-149">In this example, you're using a single Gravatar that represents yourself.</span></span> <span data-ttu-id="73b4f-150">另一種使用 Gravatar 的方式，是讓使用者在您的網站上註冊時，指定他們的 Gravatar 位址。</span><span class="sxs-lookup"><span data-stu-id="73b4f-150">Another way to use a Gravatar is to let people specify their Gravatar address when they register on your site.</span></span> <span data-ttu-id="73b4f-151">（您可以瞭解如何讓人們註冊[ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。）然後每當您顯示該使用者的資訊時，就可以將 Gravatar 新增至顯示使用者名稱的位置。</span><span class="sxs-lookup"><span data-stu-id="73b4f-151">(You can learn how to let people register in [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).) Then whenever you display information for that user, you can just add the Gravatar to where you display the user's name.</span></span>

1. <span data-ttu-id="73b4f-152">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。</span><span class="sxs-lookup"><span data-stu-id="73b4f-152">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="73b4f-153">建立名為*Gravatar*的新網頁。</span><span class="sxs-lookup"><span data-stu-id="73b4f-153">Create a new web page named *Gravatar.cshtml*.</span></span>
3. <span data-ttu-id="73b4f-154">將下列標記新增至檔案：</span><span class="sxs-lookup"><span data-stu-id="73b4f-154">Add the following markup to the file:</span></span> 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    <span data-ttu-id="73b4f-155">`Gravatar.GetHtml` 方法會在頁面上顯示 Gravatar 影像。</span><span class="sxs-lookup"><span data-stu-id="73b4f-155">The `Gravatar.GetHtml` method displays the Gravatar image on the page.</span></span> <span data-ttu-id="73b4f-156">若要變更影像的大小，您可以包含數位做為第二個參數。</span><span class="sxs-lookup"><span data-stu-id="73b4f-156">To change the size of the image, you can include a number as a second parameter.</span></span> <span data-ttu-id="73b4f-157">預設大小為80。</span><span class="sxs-lookup"><span data-stu-id="73b4f-157">The default size is 80.</span></span> <span data-ttu-id="73b4f-158">小於80的數位會使映射變小。</span><span class="sxs-lookup"><span data-stu-id="73b4f-158">Numbers less than 80 make the image smaller.</span></span> <span data-ttu-id="73b4f-159">大於80的數位會使影像變大。</span><span class="sxs-lookup"><span data-stu-id="73b4f-159">Numbers greater than 80 make the image larger.</span></span>
4. <span data-ttu-id="73b4f-160">在 `Gravatar.GetHtml` 方法中，將 `<Your Gravatar account here>` 取代為您用於 Gravatar 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="73b4f-160">In the `Gravatar.GetHtml` methods, replace `<Your Gravatar account here>` with the email address that you use for your Gravatar account.</span></span> <span data-ttu-id="73b4f-161">（如果您沒有 Gravatar 帳戶，您可以使用該使用者的電子郵件地址）。</span><span class="sxs-lookup"><span data-stu-id="73b4f-161">(If you don't have a Gravatar account, you can use the email address of someone who does.)</span></span>
5. <span data-ttu-id="73b4f-162">在您的瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="73b4f-162">Run the page in your browser.</span></span> <span data-ttu-id="73b4f-163">此頁面會顯示您所指定電子郵件地址的兩個 Gravatar 影像。</span><span class="sxs-lookup"><span data-stu-id="73b4f-163">The page displays two Gravatar images for the email address you specified.</span></span> <span data-ttu-id="73b4f-164">第二個影像小於第一個映射。</span><span class="sxs-lookup"><span data-stu-id="73b4f-164">The second image is smaller than the first.</span></span> 

    ![圖片4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a><span data-ttu-id="73b4f-166">顯示 Xbox 玩家的卡片</span><span class="sxs-lookup"><span data-stu-id="73b4f-166">Displaying an Xbox Gamer Card</span></span>

<span data-ttu-id="73b4f-167">當人們在線上播放 Microsoft Xbox 遊戲時，每個使用者都有唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="73b4f-167">When people play Microsoft Xbox games online, each user has a unique ID.</span></span> <span data-ttu-id="73b4f-168">每個播放程式的統計資料會以玩家介面卡的形式保留，以顯示其評價、玩家分數和最近玩的遊戲。</span><span class="sxs-lookup"><span data-stu-id="73b4f-168">Statistics are kept for each player in the form of a gamer card, which shows their reputation, gamer score, and recently played games.</span></span> <span data-ttu-id="73b4f-169">如果您是 Xbox 玩家，可以使用 `GamerCard` 協助程式，在網站的頁面上顯示您的玩家卡片。</span><span class="sxs-lookup"><span data-stu-id="73b4f-169">If you're an Xbox gamer, you can show your gamer card on pages in your site by using the `GamerCard` helper.</span></span>

1. <span data-ttu-id="73b4f-170">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。</span><span class="sxs-lookup"><span data-stu-id="73b4f-170">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="73b4f-171">建立名為*XboxGamer*的新頁面，並新增下列標記。</span><span class="sxs-lookup"><span data-stu-id="73b4f-171">Create a new page named *XboxGamer.cshtml* and add the following markup.</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    <span data-ttu-id="73b4f-172">您可以使用 [`GamerCard.GetHtml`] 屬性來指定要顯示之玩家卡片的別名。</span><span class="sxs-lookup"><span data-stu-id="73b4f-172">You use the `GamerCard.GetHtml` property to specify the alias for the gamer card to be displayed.</span></span>
3. <span data-ttu-id="73b4f-173">在您的瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="73b4f-173">Run the page in your browser.</span></span> <span data-ttu-id="73b4f-174">此頁面會顯示您指定的 Xbox 玩家卡片。</span><span class="sxs-lookup"><span data-stu-id="73b4f-174">The page displays the Xbox gamer card that you specified.</span></span>

    ![圖 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
