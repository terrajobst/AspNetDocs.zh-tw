---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 使用 ASP.NET Web Pages （Razor）網站中的外部網站登入 |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何使用 Facebook、Google、Twitter、Yahoo 和其他網站登入您的 ASP.NET Web Pages （Razor）網站，也就是如何支援 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638751"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="3dbdb-103">使用 ASP.NET Web Pages （Razor）網站中的外部網站登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="3dbdb-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3dbdb-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3dbdb-105">本文說明如何使用 Facebook、Google、Twitter、Yahoo 和其他網站登入您的 ASP.NET Web Pages （Razor）網站，也就是如何在您的網站中支援 OAuth 和 OpenID。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="3dbdb-106">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="3dbdb-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3dbdb-107">當您使用 WebMatrix 入門網站範本時，如何啟用其他網站的登入。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="3dbdb-108">這是本文中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="3dbdb-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="3dbdb-109">`OAuthWebSecurity` helper。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3dbdb-110">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="3dbdb-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3dbdb-111">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="3dbdb-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="3dbdb-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="3dbdb-112">WebMatrix 3</span></span>

<span data-ttu-id="3dbdb-113">ASP.NET Web Pages 包含[OAuth](http://oauth.net/)和[OpenID](http://openid.net/)提供者的支援。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="3dbdb-114">使用這些提供者，您可以讓使用者使用他們在 Facebook、Twitter、Microsoft 和 Google 的現有認證來登入您的網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="3dbdb-115">例如，若要使用 Facebook 帳戶登入，使用者可以直接選擇 Facebook 圖示，這會將他們重新導向至他們輸入其使用者資訊的 Facebook 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="3dbdb-116">然後，他們可以在您的網站上建立 Facebook 登入與其帳戶的關聯。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="3dbdb-117">網頁成員資格功能的相關加強之處在于，使用者可以在您的網站上建立多個登入（包括來自社交網路網站的登入）與單一帳戶的關聯。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="3dbdb-118">此圖顯示「**入門網站**」範本的登入頁面，使用者可以在其中選擇 Facebook、Twitter、Google 或 Microsoft 圖示，以使用外部帳戶進行登入：</span><span class="sxs-lookup"><span data-stu-id="3dbdb-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![外部提供者](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="3dbdb-120">您可以藉由在**入門網站**範本中取消批註幾行程式碼，來啟用 OAuth 和 OpenID 成員資格。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="3dbdb-121">您用來處理 OAuth 和 OpenID 提供者的方法和屬性是在 `WebMatrix.Security.OAuthWebSecurity` 類別中。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="3dbdb-122">**入門網站**範本包含完整的成員資格基礎結構、登入頁面、成員資格資料庫，以及您需要的所有程式碼，讓使用者可以使用本機認證或其他網站登入您的網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="3dbdb-123">本節提供一個範例，說明如何讓使用者從外部網站登入以**入門網站**範本為基礎的網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="3dbdb-124">建立入門網站之後，您可以執行此動作（詳細資料請遵循）：</span><span class="sxs-lookup"><span data-stu-id="3dbdb-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="3dbdb-125">針對使用 OAuth 提供者（Facebook、Twitter 和 Microsoft）的網站，您可以在外部網站上建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="3dbdb-126">這會提供您需要的應用程式金鑰，以便叫用這些網站的登入功能。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="3dbdb-127">針對使用 OpenID 提供者（Google）的網站，您不需要建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="3dbdb-128">針對所有這些網站，您必須擁有一個帳戶，才能登入並建立開發人員應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3dbdb-129">Microsoft 應用程式只接受工作網站的即時 URL，因此您無法使用本機網站 URL 來測試登入。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="3dbdb-130">編輯網站中的一些檔案，以指定適當的驗證提供者，並將登入提交至您要使用的網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="3dbdb-131">本文提供下列工作的個別指示：</span><span class="sxs-lookup"><span data-stu-id="3dbdb-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="3dbdb-132">啟用 Google 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="3dbdb-133">啟用 Facebook 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="3dbdb-134">啟用 Twitter 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="3dbdb-135">啟用 Google 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="3dbdb-136">建立或開啟以 WebMatrix 入門網站範本為基礎的 ASP.NET Web Pages 網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="3dbdb-137">開啟 *\_AppStart*  頁面，並取消批註下列程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="3dbdb-138">測試 Google 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-138">Testing Google login</span></span>

1. <span data-ttu-id="3dbdb-139">執行您網站的*預設. cshtml*頁面，然後選擇 [**登入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="3dbdb-140">在 [*登*入] 頁面的 **[使用另一個服務登入**] 區段中，選擇 [ **Google** ] 或 [ **Yahoo** ] [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="3dbdb-141">這個範例會使用 Google 登入。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="3dbdb-142">網頁會將要求重新導向至 Google 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-142">The web page redirects the request to the Google login page.</span></span>

    ![Google 登入](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="3dbdb-144">輸入現有 Google 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="3dbdb-145">如果 Google 詢問您是否要允許*Localhost*使用帳戶中的資訊，請按一下 [**允許**]。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="3dbdb-146">程式碼會使用 Google 權杖來驗證使用者，然後回到網站上的這個頁面。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="3dbdb-147">此頁面可讓使用者將其 Google 登入與您網站上的現有帳戶產生關聯，或者可以在您的網站上註冊新的帳戶，以將外部登入與建立關聯。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="3dbdb-149">選擇 [**關聯**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-149">Choose the **Associate** button.</span></span> <span data-ttu-id="3dbdb-150">瀏覽器會回到您應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="3dbdb-151">啟用 Facebook 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="3dbdb-152">前往[Facebook 開發人員網站](https://developers.facebook.com/apps)（如果您尚未登入，請登入）。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="3dbdb-153">選擇 [**建立新的應用程式**] 按鈕，然後遵循提示來命名和建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="3dbdb-154">在 [**選取您的應用程式將如何與 Facebook 整合**] 區段中，選擇 [**網站**] 區段。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="3dbdb-155">在 [**網站 url** ] 欄位中填入您的網站 url （例如 `http://www.example.com`）。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="3dbdb-156">[**網域**] 欄位是選擇性的;您可以使用這個來提供整個網域（例如*example.com*）的驗證。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3dbdb-157">如果您是在本機電腦上使用類似 `http://localhost:12345` 的 URL 執行網站（其中數位是本機埠號碼），您可以將此值新增至 [**網站 URL** ] 欄位，以測試您的網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="3dbdb-158">不過，每當您本機網站的埠號碼變更時，您都必須更新應用程式的**網站 URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="3dbdb-159">選擇 [**儲存變更**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="3dbdb-160">再次選擇 [**應用**程式] 索引標籤，然後查看應用程式的 [起始頁]。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="3dbdb-161">複製應用程式的「**應用程式識別碼**」和「**應用程式密碼**」值，並將其貼到暫存的文字檔中。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="3dbdb-162">您會將這些值傳遞至您網站程式碼中的 Facebook 提供者。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="3dbdb-163">結束 Facebook 開發人員網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="3dbdb-164">現在您會變更網站中的兩個頁面，讓使用者能夠使用他們的 Facebook 帳戶登入網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="3dbdb-165">建立或開啟以 WebMatrix 入門網站範本為基礎的 ASP.NET Web Pages 網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="3dbdb-166">開啟 *\_AppStart*  頁面，並將 Facebook OAuth 提供者的程式碼取消批註。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="3dbdb-167">取消批註程式碼區塊如下所示：</span><span class="sxs-lookup"><span data-stu-id="3dbdb-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="3dbdb-168">將 Facebook 應用程式的 [**應用程式識別碼**] 值複製為 `appId` 參數的值（在引號內）。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="3dbdb-169">複製 Facebook 應用程式中的**應用程式密碼**值，做為 `appSecret` 參數值。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="3dbdb-170">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="3dbdb-171">測試 Facebook 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-171">Testing Facebook login</span></span>

1. <span data-ttu-id="3dbdb-172">執行網站的 [*預設. cshtml* ] 頁面，然後選擇 [**登**入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="3dbdb-173">在 [*登*入] 頁面的 [**使用另一個服務登入**] 區段中，選擇 [ **Facebook** ] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="3dbdb-174">網頁會將要求重新導向至 Facebook 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-174">The web page redirects the request to the Facebook login page.</span></span>

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="3dbdb-176">登入 Facebook 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="3dbdb-177">程式碼會使用 Facebook 權杖來驗證您的身分，然後返回頁面，您可以在其中將 Facebook 登入與網站登入產生關聯。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="3dbdb-178">您的使用者名稱或電子郵件地址會填入表單上的 [**電子郵件**] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="3dbdb-180">選擇 [**關聯**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="3dbdb-181">瀏覽器會回到首頁，而且您已登入。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="3dbdb-182">啟用 Twitter 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="3dbdb-183">流覽至[Twitter 開發人員網站](https://dev.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="3dbdb-184">選擇 [**建立應用程式**] 連結，然後登入網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="3dbdb-185">在 [**建立應用程式**] 表單上，填寫 [**名稱**] 和 [**描述**] 欄位。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="3dbdb-186">在 [**網站**] 欄位中，輸入您網站的 URL （例如，`http://www.example.com`）。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3dbdb-187">如果您要在本機測試您的網站（使用如 `http://localhost:12345`的 URL），Twitter 可能不會接受 URL。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="3dbdb-188">不過，您可能可以使用本機回送 IP 位址（例如 `http://127.0.0.1:12345`）。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="3dbdb-189">這可簡化在本機測試應用程式的流程。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="3dbdb-190">不過，每次本機網站的埠號碼變更時，您都必須更新應用程式的 [**網站**] 欄位。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="3dbdb-191">在 [**回呼 URL** ] 欄位中，輸入您的網站中要讓使用者在登入 Twitter 之後返回的頁面 URL。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="3dbdb-192">例如，若要將使用者傳送至入門網站的首頁（可辨識其登入狀態），請輸入您在 [**網站**] 欄位中輸入的相同 URL。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="3dbdb-193">接受條款，然後選擇 [**建立您的 Twitter 應用程式**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="3dbdb-194">在 [**我的應用程式**] 登陸頁面上，選擇您所建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="3dbdb-195">在 [**詳細資料**] 索引標籤上，流覽至底部，然後選擇 [**建立我的存取權 Token** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="3dbdb-196">在 [**詳細資料**] 索引標籤上，複製應用程式的取用**者金鑰**和取用**者密碼**值，並將其貼到暫存文字檔中。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="3dbdb-197">您會將這些值傳遞至您網站程式碼中的 Twitter 提供者。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="3dbdb-198">結束 Twitter 網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-198">Exit the Twitter site.</span></span>

<span data-ttu-id="3dbdb-199">現在您會變更網站中的兩個頁面，讓使用者能夠使用其 Twitter 帳戶登入網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="3dbdb-200">建立或開啟以 WebMatrix 入門網站範本為基礎的 ASP.NET Web Pages 網站。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="3dbdb-201">開啟 [ *\_AppStart* ] 頁面，並取消批註 Twitter OAuth 提供者的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="3dbdb-202">取消批註程式碼區塊看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="3dbdb-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="3dbdb-203">將 Twitter 應用程式的取用**者金鑰**值複製為 `consumerKey` 參數的值（在引號內）。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="3dbdb-204">將 Twitter 應用程式的取用**者秘密**值複製為 `consumerSecret` 參數的值。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="3dbdb-205">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="3dbdb-206">測試 Twitter 登入</span><span class="sxs-lookup"><span data-stu-id="3dbdb-206">Testing Twitter login</span></span>

1. <span data-ttu-id="3dbdb-207">執行您網站的*預設. cshtml*頁面，然後選擇 [**登**入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="3dbdb-208">在 [*登*入] 頁面的 [**使用另一個服務登入**] 區段中，選擇**Twitter**圖示。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="3dbdb-209">網頁會將要求重新導向至您所建立之應用程式的 Twitter 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="3dbdb-211">登入 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="3dbdb-212">程式碼會使用 Twitter 權杖來驗證使用者，然後將您返回頁面，您可以在其中將登入與您的網站帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="3dbdb-213">您的姓名或電子郵件地址會填入表單上的 [**電子郵件**] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="3dbdb-215">選擇 [**關聯**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="3dbdb-216">瀏覽器會回到首頁，而且您已登入。</span><span class="sxs-lookup"><span data-stu-id="3dbdb-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3dbdb-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="3dbdb-217">Additional Resources</span></span>

- [<span data-ttu-id="3dbdb-218">自訂全網站行為</span><span class="sxs-lookup"><span data-stu-id="3dbdb-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="3dbdb-219">新增 ASP.NET Web Pages 網站的安全性和成員資格</span><span class="sxs-lookup"><span data-stu-id="3dbdb-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
