---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: 搭配使用 OAuth 提供者與 MVC 4 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程會示範如何建立 ASP.NET MVC 4 web 應用程式，讓使用者能夠以來自外部提供者的認證登入，例如 Facebo 。
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539078"
---
# <a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="bf4c7-103">使用 OAuth 提供者與 MVC 4</span><span class="sxs-lookup"><span data-stu-id="bf4c7-103">Using OAuth Providers with MVC 4</span></span>

<span data-ttu-id="bf4c7-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bf4c7-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bf4c7-105">本教學課程會示範如何建立 ASP.NET MVC 4 web 應用程式，讓使用者能夠使用來自外部提供者（例如 Facebook、Twitter、Microsoft 或 Google）的認證進行登入，然後將這些提供者的一些功能整合到您的web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="bf4c7-106">為了簡單起見，本教學課程著重于使用 Facebook 的認證。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="bf4c7-107">若要在 ASP.NET MVC 5 web 應用程式中使用外部認證，請參閱[使用 Facebook 和 Google OAuth2 和 OpenID 登入建立 ASP.NET MVC 5 應用](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)程式。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="bf4c7-108">在您的網站中啟用這些認證可提供顯著的優點，因為數百萬名使用者已經有這些外部提供者的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="bf4c7-109">如果您不需要建立和記住一組新的認證，這些使用者可能更傾向于註冊您的網站。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="bf4c7-110">此外，在使用者透過這些提供者的其中之一登入之後，您可以從提供者併入社交作業。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="bf4c7-111">您將建立的內容</span><span class="sxs-lookup"><span data-stu-id="bf4c7-111">What you'll build</span></span>

<span data-ttu-id="bf4c7-112">本教學課程中有兩個主要目標：</span><span class="sxs-lookup"><span data-stu-id="bf4c7-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="bf4c7-113">讓使用者能夠使用 OAuth 提供者的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="bf4c7-114">從提供者取出帳戶資訊，並將該資訊與您網站的帳戶註冊進行整合。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="bf4c7-115">雖然本教學課程中的範例著重于使用 Facebook 做為驗證提供者，但您可以修改程式碼來使用任何提供者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="bf4c7-116">執行任何提供者的步驟，與您在本教學課程中會看到的步驟非常類似。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="bf4c7-117">當您直接呼叫提供者的 API 集時，您只會注意到顯著的差異。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf4c7-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bf4c7-118">Prerequisites</span></span>

- <span data-ttu-id="bf4c7-119">[適用于 Web 的](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express) [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)或 Microsoft Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="bf4c7-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="bf4c7-120">或</span><span class="sxs-lookup"><span data-stu-id="bf4c7-120">Or</span></span>

- <span data-ttu-id="bf4c7-121">Microsoft Visual Studio 2010 SP1 或[Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="bf4c7-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="bf4c7-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="bf4c7-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="bf4c7-123">此外，本主題假設您有 ASP.NET MVC 和 Visual Studio 的基本知識。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="bf4c7-124">如果您需要 ASP.NET MVC 4 的簡介，請參閱[ASP.NET mvc 4 簡介](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="bf4c7-125">建立專案</span><span class="sxs-lookup"><span data-stu-id="bf4c7-125">Create the project</span></span>

<span data-ttu-id="bf4c7-126">在 Visual Studio 中，建立新的 ASP.NET MVC 4 Web 應用程式，並將它命名 &quot;OAuthMVC&quot;。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="bf4c7-127">您可以將目標設為 .NET Framework 4.5 或4。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-127">You can target either .NET Framework 4.5 or 4.</span></span>

![建立專案](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="bf4c7-129">在 [新增 ASP.NET MVC 4 專案] 視窗中，選取 [**網際網路應用程式**]，並將**Razor**保留為 view engine。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![選取網際網路應用程式](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="bf4c7-131">啟用提供者</span><span class="sxs-lookup"><span data-stu-id="bf4c7-131">Enable a provider</span></span>

<span data-ttu-id="bf4c7-132">當您使用 網際網路應用程式 範本建立 MVC 4 web 應用程式時，系統會在應用程式\_開始 資料夾中，使用名為 AuthConfig.cs 的檔案來建立專案。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig 檔案](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="bf4c7-134">AuthConfig 檔案包含用來註冊外部驗證提供者之用戶端的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="bf4c7-135">根據預設，此程式碼會加上批註，因此不會啟用任何外部提供者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="bf4c7-136">您必須將此程式碼取消批註，才能使用外部驗證用戶端。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="bf4c7-137">您只會取消批註您想要包含在網站中的提供者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="bf4c7-138">在本教學課程中，您只會啟用 Facebook 認證。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="bf4c7-139">請注意，在上述範例中，方法會針對註冊參數包含空字串。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="bf4c7-140">如果您嘗試立即執行應用程式，應用程式會擲回引數例外狀況，因為參數不允許空字串。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="bf4c7-141">若要提供有效的值，您必須向外部提供者註冊您的網站，如下一節所示。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="bf4c7-142">向外部提供者註冊</span><span class="sxs-lookup"><span data-stu-id="bf4c7-142">Registering with an external provider</span></span>

<span data-ttu-id="bf4c7-143">若要使用外部提供者的認證來驗證使用者，您必須向提供者註冊您的網站。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="bf4c7-144">當您註冊網站時，您會收到註冊用戶端時所要包含的參數（例如金鑰或識別碼，以及密碼）。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="bf4c7-145">您必須擁有您想要使用之提供者的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="bf4c7-146">本教學課程不會顯示向這些提供者註冊所需執行的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="bf4c7-147">這些步驟通常並不容易。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-147">The steps are typically not difficult.</span></span> <span data-ttu-id="bf4c7-148">若要成功註冊您的網站，請遵循這些網站上提供的指示。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="bf4c7-149">若要開始註冊您的網站，請參閱開發人員網站，以取得：</span><span class="sxs-lookup"><span data-stu-id="bf4c7-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="bf4c7-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="bf4c7-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="bf4c7-151">Google</span><span class="sxs-lookup"><span data-stu-id="bf4c7-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="bf4c7-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="bf4c7-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="bf4c7-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="bf4c7-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="bf4c7-154">向 Facebook 註冊您的網站時，您可以提供網站網域的 &quot;localhost&quot; 和 URL 的 `&quot; http://localhost/&quot;`，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="bf4c7-155">使用 localhost 可與大部分的提供者搭配運作，但目前不適用於 Microsoft 提供者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="bf4c7-156">針對 Microsoft 提供者，您必須包含有效的網站 URL。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![註冊網站](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="bf4c7-158">在上圖中，已移除應用程式識別碼、應用程式密碼及連絡人電子郵件的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="bf4c7-159">當您實際註冊網站時，這些值將會存在。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="bf4c7-160">您會想要記下 [應用程式識別碼] 和 [應用程式密碼] 的值，因為您會將其新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="bf4c7-161">建立測試使用者</span><span class="sxs-lookup"><span data-stu-id="bf4c7-161">Creating test users</span></span>

<span data-ttu-id="bf4c7-162">如果您不介意使用現有的 Facebook 帳戶來測試您的網站，可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="bf4c7-163">您可以在 Facebook 應用程式管理頁面中，輕鬆地為您的應用程式建立測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="bf4c7-164">您可以使用這些測試帳戶來登入您的網站。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="bf4c7-165">若要建立測試使用者，請按一下左側流覽窗格中的 [**角色**] 連結，然後按一下 [**建立**] 連結。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![建立測試使用者](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="bf4c7-167">Facebook 網站會自動建立您要求的測試帳戶數目。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="bf4c7-168">從提供者新增應用程式識別碼和密碼</span><span class="sxs-lookup"><span data-stu-id="bf4c7-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="bf4c7-169">既然您已從 Facebook 接收識別碼和秘密，請回到 AuthConfig 檔案，並將它們新增為參數值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="bf4c7-170">以下顯示的值不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="bf4c7-171">使用外部認證登入</span><span class="sxs-lookup"><span data-stu-id="bf4c7-171">Log in with external credentials</span></span>

<span data-ttu-id="bf4c7-172">這就是在您的網站中啟用外部認證所需執行的動作。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="bf4c7-173">執行您的應用程式，然後按一下右上角的 [登入] 連結。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="bf4c7-174">此範本會自動辨識您已註冊 Facebook 做為提供者，並包含提供者的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="bf4c7-175">如果您註冊多個提供者，則會自動包含每一個提供者的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![外部登入](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="bf4c7-177">本教學課程未涵蓋如何自訂外部提供者的 [登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="bf4c7-178">如需相關資訊，請參閱[使用 OAuth/OpenID 自訂登入 UI](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="bf4c7-179">按一下 [Facebook] 按鈕以使用 Facebook 認證登入。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="bf4c7-180">當您選取其中一個外部提供者時，系統會將您重新導向至該網站，並提示該服務登入。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="bf4c7-181">下圖顯示 Facebook 的登入畫面。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="bf4c7-182">它會注意到您使用 Facebook 帳戶來登入名為 oauthmvcexample 的網站。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 驗證](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="bf4c7-184">以 Facebook 認證登入之後，頁面會通知使用者該網站將可存取基本資訊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![要求許可權](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="bf4c7-186">選取 [**移至應用程式**] 之後，使用者必須註冊網站。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="bf4c7-187">下圖顯示使用者以 Facebook 認證登入後的註冊頁面。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="bf4c7-188">使用者名稱通常會預先填入提供者的名稱。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-188">The user name is typically pre-filled with a name from the provider.</span></span>

![註冊](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="bf4c7-190">按一下 [**註冊**] 以完成註冊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="bf4c7-191">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-191">Close the browser.</span></span>

<span data-ttu-id="bf4c7-192">您可以看到新的帳戶已新增至您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="bf4c7-193">在伺服器總管中，開啟**DefaultConnection**資料庫，並開啟 [**資料表]** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![資料庫資料表](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="bf4c7-195">以滑鼠右鍵按一下 [ **UserProfile** ] 資料表，然後選取 [**顯示資料表資料**]。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![顯示資料](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="bf4c7-197">您會看到您新增的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-197">You will see the new account you added.</span></span> <span data-ttu-id="bf4c7-198">查看**網頁\_OAuthMembership**資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="bf4c7-199">您會看到更多與您剛新增之帳戶的外部提供者相關的資料。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="bf4c7-200">如果您只想要啟用外部驗證，就大功告成了。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="bf4c7-201">不過，您可以進一步將提供者的資訊整合到新的使用者註冊程式中，如下列各節所示。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="bf4c7-202">建立其他使用者資訊的模型</span><span class="sxs-lookup"><span data-stu-id="bf4c7-202">Create models for additional user information</span></span>

<span data-ttu-id="bf4c7-203">如您在先前各節中所注意，您不需要取得任何額外的資訊，讓內建帳戶註冊能夠正常執行。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="bf4c7-204">不過，大部分的外部提供者會傳回使用者的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="bf4c7-205">下列各節顯示如何保留該資訊，並將它儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="bf4c7-206">具體而言，您會保留使用者完整名稱的值、使用者個人網頁的 URI，以及指出 Facebook 是否已驗證帳戶的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="bf4c7-207">您將使用[Code First 移轉](https://msdn.microsoft.com/data/jj591621)來新增資料表，以儲存額外的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="bf4c7-208">您要將資料表加入現有的資料庫中，因此您必須先建立目前資料庫的快照集。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="bf4c7-209">藉由建立目前資料庫的快照集，您可以在稍後建立只包含新資料表的遷移。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="bf4c7-210">若要建立目前資料庫的快照集：</span><span class="sxs-lookup"><span data-stu-id="bf4c7-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="bf4c7-211">開啟 [**套件管理員主控台**]</span><span class="sxs-lookup"><span data-stu-id="bf4c7-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="bf4c7-212">執行命令**啟用-遷移**</span><span class="sxs-lookup"><span data-stu-id="bf4c7-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="bf4c7-213">執行命令**新增-遷移初始– IgnoreChanges**</span><span class="sxs-lookup"><span data-stu-id="bf4c7-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="bf4c7-214">執行命令**update-database**</span><span class="sxs-lookup"><span data-stu-id="bf4c7-214">Run the command **update-database**</span></span>

<span data-ttu-id="bf4c7-215">現在，您將加入新的屬性。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-215">Now, you will add the new properties.</span></span> <span data-ttu-id="bf4c7-216">在 [模型] 資料夾中，開啟 AccountModels.cs 檔案，並尋找 RegisterExternalLoginModel 類別。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="bf4c7-217">RegisterExternalLoginModel 類別包含從驗證提供者傳回的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="bf4c7-218">新增名為 FullName 和 Link 的屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="bf4c7-219">此外，在 AccountModels.cs 中，新增名為 ExtraUserInformation 的新類別。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="bf4c7-220">此類別代表將在資料庫中建立的新資料表。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="bf4c7-221">在 UsersCoNtext 類別中，新增下列反白顯示的程式碼，以建立新類別的 DbSet 屬性。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="bf4c7-222">您現在已準備好建立新的資料表。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-222">You are now ready to create the new table.</span></span> <span data-ttu-id="bf4c7-223">再次開啟 [套件管理員主控台]，這次：</span><span class="sxs-lookup"><span data-stu-id="bf4c7-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="bf4c7-224">執行命令**新增-遷移 AddExtraUserInformation**</span><span class="sxs-lookup"><span data-stu-id="bf4c7-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="bf4c7-225">執行命令**update-database**</span><span class="sxs-lookup"><span data-stu-id="bf4c7-225">Run the command **update-database**</span></span>

<span data-ttu-id="bf4c7-226">新的資料表現在存在於資料庫中。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="bf4c7-227">取得其他資料</span><span class="sxs-lookup"><span data-stu-id="bf4c7-227">Retrieve the additional data</span></span>

<span data-ttu-id="bf4c7-228">有兩種方式可取得其他使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="bf4c7-229">第一種方式是在驗證要求期間保留傳回的使用者資料（根據預設值）。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="bf4c7-230">第二種方式是特別呼叫提供者 API，並要求詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="bf4c7-231">「FullName」和「連結」的值會由 Facebook 自動回傳。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="bf4c7-232">值，指出 Facebook 是否已通過對 Facebook API 的呼叫來驗證帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="bf4c7-233">首先，您將填入 [FullName] 和 [連結] 的值，之後您將會取得已驗證的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="bf4c7-234">若要取出其他使用者資料，請開啟 [**控制器**] 資料夾中的**AccountController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="bf4c7-235">此檔案包含用來記錄、註冊和管理帳戶的邏輯。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="bf4c7-236">特別要注意的是名為**ExternalLoginCallback**和**ExternalLoginConfirmation**的方法。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="bf4c7-237">在這些方法中，您可以加入程式碼，以自訂應用程式的外部登入作業。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="bf4c7-238">**ExternalLoginCallback**方法的第一行包含：</span><span class="sxs-lookup"><span data-stu-id="bf4c7-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="bf4c7-239">在**VerifyAuthentication**方法傳回的**AuthenticationResult**物件的**ExtraData**屬性中，會傳回額外的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="bf4c7-240">Facebook 用戶端會在**ExtraData**屬性中包含下列值：</span><span class="sxs-lookup"><span data-stu-id="bf4c7-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="bf4c7-241">id</span><span class="sxs-lookup"><span data-stu-id="bf4c7-241">id</span></span>
- <span data-ttu-id="bf4c7-242">名稱</span><span class="sxs-lookup"><span data-stu-id="bf4c7-242">name</span></span>
- <span data-ttu-id="bf4c7-243">連結</span><span class="sxs-lookup"><span data-stu-id="bf4c7-243">link</span></span>
- <span data-ttu-id="bf4c7-244">gender</span><span class="sxs-lookup"><span data-stu-id="bf4c7-244">gender</span></span>
- <span data-ttu-id="bf4c7-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="bf4c7-245">accesstoken</span></span>

<span data-ttu-id="bf4c7-246">其他提供者在 ExtraData 屬性中將會有類似但稍微不同的資料。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="bf4c7-247">如果使用者不熟悉您的網站，您將會抓取一些額外的資料，並將該資料傳遞給確認視圖。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="bf4c7-248">只有在使用者不熟悉您的網站時，才會執行方法中的最後一個程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="bf4c7-249">取代下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="bf4c7-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="bf4c7-250">改用這行︰</span><span class="sxs-lookup"><span data-stu-id="bf4c7-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="bf4c7-251">這種變更只會包含 FullName 和 Link 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="bf4c7-252">在**ExternalLoginConfirmation**方法中，修改下面反白顯示的程式碼，以儲存額外的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="bf4c7-253">調整視圖</span><span class="sxs-lookup"><span data-stu-id="bf4c7-253">Adjusting the view</span></span>

<span data-ttu-id="bf4c7-254">您從提供者取得的其他使用者資料將會顯示在 [註冊] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="bf4c7-255">在  **Views** /**帳戶** 資料夾中，開啟**ExternalLoginConfirmation**。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="bf4c7-256">在 [使用者名稱] 的現有欄位底下，新增 [FullName]、[連結] 和 [PictureLink] 的欄位。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="bf4c7-257">您現在已準備好執行應用程式，並使用儲存的其他資訊來註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="bf4c7-258">您的帳戶必須尚未向網站註冊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="bf4c7-259">您可以使用不同的測試帳戶，或刪除**UserProfile**和網頁中的資料列， **\_OAuthMembership**資料表來尋找您想要重複使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="bf4c7-260">藉由刪除這些資料列，您將可確保帳戶已再次註冊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="bf4c7-261">執行應用程式，並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-261">Run the application and register the new user.</span></span> <span data-ttu-id="bf4c7-262">請注意，這次 [確認] 頁面包含更多的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-262">Notice that this time the confirmation page contains more values.</span></span>

![註冊](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="bf4c7-264">完成註冊之後，請關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-264">After completing registration, close the browser.</span></span> <span data-ttu-id="bf4c7-265">查看資料庫，以注意**ExtraUserInformation**資料表中的新值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="bf4c7-266">安裝 Facebook API 的 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="bf4c7-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="bf4c7-267">Facebook 提供您可以呼叫以執行作業的[API](https://developers.facebook.com/docs/reference/apis/) 。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="bf4c7-268">您可以藉由傳送 HTTP 要求，或使用安裝可協助傳送這些要求的 NuGet 套件來呼叫 Facebook API。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="bf4c7-269">本教學課程中會顯示使用 NuGet 套件，但不一定要安裝 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="bf4c7-270">本教學課程說明如何使用 Facebook C# SDK 套件。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="bf4c7-271">還有其他可協助呼叫 Facebook API 的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="bf4c7-272">從 [**管理 NuGet 封裝**] 視窗中，選取C# [Facebook SDK] 套件。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![安裝套件](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="bf4c7-274">您將使用 Facebook C# SDK 來呼叫需要使用者存取權杖的作業。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="bf4c7-275">下一節將說明如何取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="bf4c7-276">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="bf4c7-276">Retrieve access token</span></span>

<span data-ttu-id="bf4c7-277">在驗證使用者的認證之後，大部分的外部提供者都會傳回存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="bf4c7-278">此存取權杖非常重要，因為它可讓您呼叫僅適用于已驗證使用者的作業。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="bf4c7-279">因此，當您想要提供更多功能時，抓取和儲存存取權杖是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="bf4c7-280">視外部提供者而定，存取權杖在有限的時間內可能有效。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="bf4c7-281">為確保您擁有有效的存取權杖，您會在每次使用者登入時將它取出，並將其儲存為會話值，而不是將它儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="bf4c7-282">在**ExternalLoginCallback**方法中，存取權杖也會在**AuthenticationResult**物件的**ExtraData**屬性中傳回。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="bf4c7-283">將反白顯示的程式碼新增至**ExternalLoginCallback** ，以將存取權杖儲存在**Session**物件中。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="bf4c7-284">每次使用者以 Facebook 帳戶登入時，就會執行此程式碼。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="bf4c7-285">雖然此範例會從 Facebook 取得存取權杖，您可以透過名為 &quot;accesstoken&quot;的相同金鑰，從任何外部提供者抓取存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="bf4c7-286">登出</span><span class="sxs-lookup"><span data-stu-id="bf4c7-286">Logging off</span></span>

<span data-ttu-id="bf4c7-287">預設的**登出**方法會將使用者登出您的應用程式，但不會將使用者登出外部提供者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="bf4c7-288">若要將使用者登出 Facebook，並在使用者登出之後防止權杖保存，您可以將下列反白顯示的程式碼新增至 AccountController 中的**登出**方法。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="bf4c7-289">您在 `next` 參數中提供的值是使用者登出 Facebook 後要使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="bf4c7-290">在您的本機電腦上進行測試時，您會為本機網站提供正確的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="bf4c7-291">在生產環境中，您會提供預設頁面，例如 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="bf4c7-292">取得需要存取權杖的使用者資訊</span><span class="sxs-lookup"><span data-stu-id="bf4c7-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="bf4c7-293">既然您已儲存存取權杖並已安裝 Facebook C# SDK 套件，您可以一起使用它們來要求 facebook 中的其他使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="bf4c7-294">在**ExternalLoginConfirmation**方法中，藉由傳遞存取權杖的值來建立**FacebookClient**類別的實例。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="bf4c7-295">針對目前的已驗證使用者，要求**已驗證**屬性的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="bf4c7-296">[**已驗證**] 屬性會指出 Facebook 是否已透過其他方式驗證帳戶，例如傳送訊息至行動電話。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="bf4c7-297">將此值儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="bf4c7-298">您必須為使用者刪除資料庫中的記錄，或使用不同的 Facebook 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="bf4c7-299">執行應用程式，並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-299">Run the application, and register the new user.</span></span> <span data-ttu-id="bf4c7-300">查看 [ **ExtraUserInformation** ] 資料表以查看 [已驗證] 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bf4c7-301">結論</span><span class="sxs-lookup"><span data-stu-id="bf4c7-301">Conclusion</span></span>

<span data-ttu-id="bf4c7-302">在本教學課程中，您已建立與 Facebook 整合的網站，以進行使用者驗證和註冊資料。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="bf4c7-303">您已瞭解 MVC 4 web 應用程式所設定的預設行為，以及如何自訂該預設行為。</span><span class="sxs-lookup"><span data-stu-id="bf4c7-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="bf4c7-304">相關主題</span><span class="sxs-lookup"><span data-stu-id="bf4c7-304">Related topics</span></span>

- [<span data-ttu-id="bf4c7-305">使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bf4c7-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
