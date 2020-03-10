---
uid: web-api/overview/security/individual-accounts-in-web-api
title: 在 ASP.NET Web API 2.2 中使用個別帳戶和本機登入保護 Web API |Microsoft Docs
author: MikeWasson
description: 本主題說明如何使用 OAuth2 來保護 Web API，以根據成員資格資料庫進行驗證。 教學課程中使用的軟體版本 Visual Studio 201 。
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555192"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a><span data-ttu-id="514d4-104">在 ASP.NET Web API 2.2 中使用個別帳戶和本機登入保護 Web API</span><span class="sxs-lookup"><span data-stu-id="514d4-104">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>

<span data-ttu-id="514d4-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="514d4-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="514d4-106">下載範例應用程式</span><span class="sxs-lookup"><span data-stu-id="514d4-106">Download Sample App</span></span>](https://github.com/MikeWasson/LocalAccountsApp)

> <span data-ttu-id="514d4-107">本主題說明如何使用 OAuth2 來保護 Web API，以根據成員資格資料庫進行驗證。</span><span class="sxs-lookup"><span data-stu-id="514d4-107">This topic shows how to secure a web API using OAuth2 to authenticate against a membership database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="514d4-108">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="514d4-108">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="514d4-109">Visual Studio 2013 Update 3</span><span class="sxs-lookup"><span data-stu-id="514d4-109">Visual Studio 2013 Update 3</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [<span data-ttu-id="514d4-110">Web API 2。2</span><span class="sxs-lookup"><span data-stu-id="514d4-110">Web API 2.2</span></span>](../releases/whats-new-in-aspnet-web-api-22.md)
> - [<span data-ttu-id="514d4-111">ASP.NET Identity 2。1</span><span class="sxs-lookup"><span data-stu-id="514d4-111">ASP.NET Identity 2.1</span></span>](../../../identity/index.md)

<span data-ttu-id="514d4-112">在 Visual Studio 2013 中，Web API 專案範本提供三個驗證選項：</span><span class="sxs-lookup"><span data-stu-id="514d4-112">In Visual Studio 2013, the Web API project template gives you three options for authentication:</span></span>

- <span data-ttu-id="514d4-113">**個別帳戶。**</span><span class="sxs-lookup"><span data-stu-id="514d4-113">**Individual accounts.**</span></span> <span data-ttu-id="514d4-114">應用程式會使用成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="514d4-114">The app uses a membership database.</span></span>
- <span data-ttu-id="514d4-115">**組織帳戶。**</span><span class="sxs-lookup"><span data-stu-id="514d4-115">**Organizational accounts.**</span></span> <span data-ttu-id="514d4-116">使用者使用其 Azure Active Directory、Office 365 或內部部署 Active Directory 認證登入。</span><span class="sxs-lookup"><span data-stu-id="514d4-116">Users sign in with their Azure Active Directory, Office 365, or on-premise Active Directory credentials.</span></span>
- <span data-ttu-id="514d4-117">**Windows 驗證。**</span><span class="sxs-lookup"><span data-stu-id="514d4-117">**Windows authentication.**</span></span> <span data-ttu-id="514d4-118">此選項適用于內部網路應用程式，並使用 Windows 驗證 IIS 模組。</span><span class="sxs-lookup"><span data-stu-id="514d4-118">This option is intended for Intranet applications, and uses the Windows Authentication IIS module.</span></span>

<span data-ttu-id="514d4-119">如需這些選項的詳細資訊，請參閱[在 Visual Studio 2013 中建立 ASP.NET Web 專案](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)。</span><span class="sxs-lookup"><span data-stu-id="514d4-119">For more details about these options, see [Creating ASP.NET Web Projects in Visual Studio 2013](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth).</span></span>

<span data-ttu-id="514d4-120">個別帳戶提供兩種方式讓使用者登入：</span><span class="sxs-lookup"><span data-stu-id="514d4-120">Individual accounts provide two ways for a user to log in:</span></span>

- <span data-ttu-id="514d4-121">**本機登**入。</span><span class="sxs-lookup"><span data-stu-id="514d4-121">**Local login**.</span></span> <span data-ttu-id="514d4-122">使用者會在網站上註冊，並輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="514d4-122">The user registers at the site, entering a username and password.</span></span> <span data-ttu-id="514d4-123">應用程式會將密碼雜湊儲存在成員資格資料庫中。</span><span class="sxs-lookup"><span data-stu-id="514d4-123">The app stores the password hash in the membership database.</span></span> <span data-ttu-id="514d4-124">當使用者登入時，ASP.NET Identity 系統會驗證密碼。</span><span class="sxs-lookup"><span data-stu-id="514d4-124">When the user logs in, the ASP.NET Identity system verifies the password.</span></span>
- <span data-ttu-id="514d4-125">**社交登**入。</span><span class="sxs-lookup"><span data-stu-id="514d4-125">**Social login**.</span></span> <span data-ttu-id="514d4-126">使用者使用外部服務（例如 Facebook、Microsoft 或 Google）登入。</span><span class="sxs-lookup"><span data-stu-id="514d4-126">The user signs in with an external service, such as Facebook, Microsoft, or Google.</span></span> <span data-ttu-id="514d4-127">應用程式仍會在成員資格資料庫中建立使用者的專案，但不會儲存任何認證。</span><span class="sxs-lookup"><span data-stu-id="514d4-127">The app still creates an entry for the user in the membership database, but does not store any credentials.</span></span> <span data-ttu-id="514d4-128">使用者藉由登入外部服務來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="514d4-128">The user authenticates by signing into the external service.</span></span>

<span data-ttu-id="514d4-129">本文探討本機登入案例。</span><span class="sxs-lookup"><span data-stu-id="514d4-129">This article looks at the local login scenario.</span></span> <span data-ttu-id="514d4-130">針對本機和社交登入，Web API 會使用 OAuth2 來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="514d4-130">For both local and social login, Web API uses OAuth2 to authenticate requests.</span></span> <span data-ttu-id="514d4-131">不過，本機和社交登入的認證流程會不同。</span><span class="sxs-lookup"><span data-stu-id="514d4-131">However, the credential flows are different for local and social login.</span></span>

<span data-ttu-id="514d4-132">在本文中，我將示範一個簡單的應用程式，讓使用者登入並將已驗證的 AJAX 呼叫傳送至 Web API。</span><span class="sxs-lookup"><span data-stu-id="514d4-132">In this article, I'll demonstrate a simple app that lets the user log in and send authenticated AJAX calls to a web API.</span></span> <span data-ttu-id="514d4-133">您可以在[這裡](https://github.com/MikeWasson/LocalAccountsApp)下載範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="514d4-133">You can download the sample code [here](https://github.com/MikeWasson/LocalAccountsApp).</span></span> <span data-ttu-id="514d4-134">讀我檔案說明如何在 Visual Studio 中從頭開始建立範例。</span><span class="sxs-lookup"><span data-stu-id="514d4-134">The readme describes how to create the sample from scratch in Visual Studio.</span></span>

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

<span data-ttu-id="514d4-135">範例應用程式會針對資料系結和 jQuery 使用「挖式 .js」來傳送 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="514d4-135">The sample app uses Knockout.js for data-binding and jQuery for sending AJAX requests.</span></span> <span data-ttu-id="514d4-136">我將把焦點放在 AJAX 呼叫，所以您不需要知道這篇文章的挖的 .js。</span><span class="sxs-lookup"><span data-stu-id="514d4-136">I'll be focusing on the AJAX calls, so you don't need to know Knockout.js for this article.</span></span>

<span data-ttu-id="514d4-137">在過程中，我將說明：</span><span class="sxs-lookup"><span data-stu-id="514d4-137">Along the way, I'll describe:</span></span>

- <span data-ttu-id="514d4-138">應用程式在用戶端上執行的作業。</span><span class="sxs-lookup"><span data-stu-id="514d4-138">What the app is doing on the client side.</span></span>
- <span data-ttu-id="514d4-139">伺服器上的情況。</span><span class="sxs-lookup"><span data-stu-id="514d4-139">What's happening on the server.</span></span>
- <span data-ttu-id="514d4-140">在中間的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="514d4-140">The HTTP traffic in the middle.</span></span>

<span data-ttu-id="514d4-141">首先，我們需要定義一些 OAuth2 的術語。</span><span class="sxs-lookup"><span data-stu-id="514d4-141">First, we need to define some OAuth2 terminology.</span></span>

- <span data-ttu-id="514d4-142">*資源*。</span><span class="sxs-lookup"><span data-stu-id="514d4-142">*Resource*.</span></span> <span data-ttu-id="514d4-143">可以保護的部分資料。</span><span class="sxs-lookup"><span data-stu-id="514d4-143">Some piece of data that can be protected.</span></span>
- <span data-ttu-id="514d4-144">*資源伺服器*。</span><span class="sxs-lookup"><span data-stu-id="514d4-144">*Resource server*.</span></span> <span data-ttu-id="514d4-145">裝載資源的伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-145">The server that hosts the resource.</span></span>
- <span data-ttu-id="514d4-146">*資源擁有*者。</span><span class="sxs-lookup"><span data-stu-id="514d4-146">*Resource owner*.</span></span> <span data-ttu-id="514d4-147">可以授與資源存取權的實體。</span><span class="sxs-lookup"><span data-stu-id="514d4-147">The entity that can grant permission to access a resource.</span></span> <span data-ttu-id="514d4-148">（通常是使用者）。</span><span class="sxs-lookup"><span data-stu-id="514d4-148">(Typically the user.)</span></span>
- <span data-ttu-id="514d4-149">*用戶端*：想要存取資源的應用程式。</span><span class="sxs-lookup"><span data-stu-id="514d4-149">*Client*: The app that wants access to the resource.</span></span> <span data-ttu-id="514d4-150">在本文中，用戶端是網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="514d4-150">In this article, the client is a web browser.</span></span>
- <span data-ttu-id="514d4-151">*存取權杖*。</span><span class="sxs-lookup"><span data-stu-id="514d4-151">*Access token*.</span></span> <span data-ttu-id="514d4-152">授與資源存取權的權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-152">A token that grants access to a resource.</span></span>
- <span data-ttu-id="514d4-153">*持有人權杖*。</span><span class="sxs-lookup"><span data-stu-id="514d4-153">*Bearer token*.</span></span> <span data-ttu-id="514d4-154">特定類型的存取權杖，其中包含任何人都可以使用權杖的屬性。</span><span class="sxs-lookup"><span data-stu-id="514d4-154">A particular type of access token, with the property that anyone can use the token.</span></span> <span data-ttu-id="514d4-155">換句話說，用戶端不需要密碼編譯金鑰或其他秘密，也能使用持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-155">In other words, a client doesn't need a cryptographic key or other secret to use a bearer token.</span></span> <span data-ttu-id="514d4-156">基於這個理由，持有人權杖只能透過 HTTPS 使用，而且應該要有相對較短的到期時間。</span><span class="sxs-lookup"><span data-stu-id="514d4-156">For that reason, bearer tokens should only be used over a HTTPS, and should have relatively short expiration times.</span></span>
- <span data-ttu-id="514d4-157">*授權伺服器*。</span><span class="sxs-lookup"><span data-stu-id="514d4-157">*Authorization server*.</span></span> <span data-ttu-id="514d4-158">提供存取權杖的伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-158">A server that gives out access tokens.</span></span>

<span data-ttu-id="514d4-159">應用程式可以同時做為授權伺服器和資源伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-159">An application can act as both authorization server and resource server.</span></span> <span data-ttu-id="514d4-160">Web API 專案範本會遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="514d4-160">The Web API project template follows this pattern.</span></span>

## <a name="local-login-credential-flow"></a><span data-ttu-id="514d4-161">本機登入認證流程</span><span class="sxs-lookup"><span data-stu-id="514d4-161">Local Login Credential Flow</span></span>

<span data-ttu-id="514d4-162">針對本機登入，Web API 會使用 OAuth2 中所定義的[資源擁有者密碼流程](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html)。</span><span class="sxs-lookup"><span data-stu-id="514d4-162">For local login, Web API uses the [resource owner password flow](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) defined in OAuth2.</span></span>

1. <span data-ttu-id="514d4-163">使用者在用戶端輸入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="514d4-163">The user enters a name and password into the client.</span></span>
2. <span data-ttu-id="514d4-164">用戶端會將這些認證傳送給授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-164">The client sends these credentials to the authorization server.</span></span>
3. <span data-ttu-id="514d4-165">授權伺服器會驗證認證，並傳回存取權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-165">The authorization server authenticates the credentials and returns an access token.</span></span>
4. <span data-ttu-id="514d4-166">若要存取受保護的資源，用戶端會在 HTTP 要求的 Authorization 標頭中包含存取權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-166">To access a protected resource, the client includes the access token in the Authorization header of the HTTP request.</span></span>

![](individual-accounts-in-web-api/_static/image3.png)

<span data-ttu-id="514d4-167">當您選取 [Web API] 專案範本中的**個別帳戶**時，專案會包含驗證使用者認證和發行權杖的授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-167">When you select **Individual accounts** in the Web API project template, the project includes an authorization server that validates user credentials and issues tokens.</span></span> <span data-ttu-id="514d4-168">下圖顯示與 Web API 元件相同的認證流程。</span><span class="sxs-lookup"><span data-stu-id="514d4-168">The following diagram shows the same credential flow in terms of Web API components.</span></span>

![](individual-accounts-in-web-api/_static/image4.png)

<span data-ttu-id="514d4-169">在此案例中，Web API 控制器會作為資源伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-169">In this scenario, Web API controllers act as resource servers.</span></span> <span data-ttu-id="514d4-170">驗證篩選器會驗證存取權杖，而 **[授權]** 屬性則是用來保護資源。</span><span class="sxs-lookup"><span data-stu-id="514d4-170">An authentication filter validates access tokens, and the **[Authorize]** attribute is used to protect a resource.</span></span> <span data-ttu-id="514d4-171">當控制器或動作具有 **[授權]** 屬性時，所有對該控制器或動作的要求都必須經過驗證。</span><span class="sxs-lookup"><span data-stu-id="514d4-171">When a controller or action has the **[Authorize]** attribute, all requests to that controller or action must be authenticated.</span></span> <span data-ttu-id="514d4-172">否則，會拒絕授權，而 Web API 會傳回401（未經授權）錯誤。</span><span class="sxs-lookup"><span data-stu-id="514d4-172">Otherwise, authorization is denied, and Web API returns a 401 (Unauthorized) error.</span></span>

<span data-ttu-id="514d4-173">授權伺服器和驗證篩選準則都會呼叫[OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)元件，以處理 OAuth2 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="514d4-173">The authorization server and the authentication filter both call into an [OWIN middleware](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) component that handles the details of OAuth2.</span></span> <span data-ttu-id="514d4-174">我稍後會在本教學課程中詳細說明此設計。</span><span class="sxs-lookup"><span data-stu-id="514d4-174">I'll describe the design in more detail later in this tutorial.</span></span>

## <a name="sending-an-unauthorized-request"></a><span data-ttu-id="514d4-175">傳送未經授權的要求</span><span class="sxs-lookup"><span data-stu-id="514d4-175">Sending an Unauthorized Request</span></span>

<span data-ttu-id="514d4-176">若要開始使用，請執行應用程式，然後按一下 [**呼叫 API** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="514d4-176">To get started, run the app and click the **Call API** button.</span></span> <span data-ttu-id="514d4-177">當要求完成時，您應該會在 [**結果**] 方塊中看到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="514d4-177">When the request completes, you should see an error message in the **Result** box.</span></span> <span data-ttu-id="514d4-178">這是因為要求未包含存取權杖，因此要求未經授權。</span><span class="sxs-lookup"><span data-stu-id="514d4-178">That's because the request does not contain an access token, so the request is unauthorized.</span></span>

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

<span data-ttu-id="514d4-179">[**呼叫 API** ] 按鈕會將 AJAX 要求傳送至 ~/api/values，這會叫用 Web API 控制器動作。</span><span class="sxs-lookup"><span data-stu-id="514d4-179">The **Call API** button sends an AJAX request to ~/api/values, which invokes a Web API controller action.</span></span> <span data-ttu-id="514d4-180">以下是傳送 AJAX 要求的 JavaScript 程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="514d4-180">Here is the section of JavaScript code that sends the AJAX request.</span></span> <span data-ttu-id="514d4-181">在範例應用程式中，所有的 JavaScript 應用程式程式碼都位於 Scripts\app.js 檔案中。</span><span class="sxs-lookup"><span data-stu-id="514d4-181">In the sample app, all of the JavaScript app code is located in the Scripts\app.js file.</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

<span data-ttu-id="514d4-182">在使用者登入之前，不會有任何持有人權杖，因此要求中不會有任何授權標頭。</span><span class="sxs-lookup"><span data-stu-id="514d4-182">Until the user logs in, there is no bearer token, and therefore no Authorization header in the request.</span></span> <span data-ttu-id="514d4-183">這會導致要求傳回401錯誤。</span><span class="sxs-lookup"><span data-stu-id="514d4-183">This causes the request to return a 401 error.</span></span>

<span data-ttu-id="514d4-184">以下是 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="514d4-184">Here is the HTTP request.</span></span> <span data-ttu-id="514d4-185">（我使用[Fiddler](http://www.telerik.com/fiddler)來捕捉 HTTP 流量）。</span><span class="sxs-lookup"><span data-stu-id="514d4-185">(I used [Fiddler](http://www.telerik.com/fiddler) to capture the HTTP traffic.)</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

<span data-ttu-id="514d4-186">HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="514d4-186">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

<span data-ttu-id="514d4-187">請注意，回應會包含 Www 驗證標頭，並將挑戰設定為 [持有人]。</span><span class="sxs-lookup"><span data-stu-id="514d4-187">Notice that the response includes a Www-Authenticate header with the challenge set to Bearer.</span></span> <span data-ttu-id="514d4-188">這表示伺服器預期持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-188">That indicates the server expects a bearer token.</span></span>

## <a name="register-a-user"></a><span data-ttu-id="514d4-189">註冊使用者</span><span class="sxs-lookup"><span data-stu-id="514d4-189">Register a User</span></span>

<span data-ttu-id="514d4-190">在應用程式的 [**註冊**] 區段中，輸入電子郵件和密碼，然後按一下 [**註冊**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="514d4-190">In the **Register** section of the app, enter an email and password, and click the **Register** button.</span></span>

<span data-ttu-id="514d4-191">您不需要在此範例中使用有效的電子郵件地址，但實際的應用程式會確認此位址。</span><span class="sxs-lookup"><span data-stu-id="514d4-191">You don't need to use a valid email address for this sample, but a real app would confirm the address.</span></span> <span data-ttu-id="514d4-192">（請參閱[使用登入、電子郵件確認和密碼重設建立安全的 ASP.NET MVC 5 web 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)）。在 [密碼] 中，使用以大寫字母、小寫字母、數位和非英數位元等字元做為 "Password1！"。</span><span class="sxs-lookup"><span data-stu-id="514d4-192">(See [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) For the password, use something like "Password1!", with an upper case letter, lower case letter, number, and non-alpha-numeric character.</span></span> <span data-ttu-id="514d4-193">為了讓應用程式保持簡單，我會省略用戶端驗證，因此如果密碼格式發生問題，您會收到400（不正確的要求）錯誤。</span><span class="sxs-lookup"><span data-stu-id="514d4-193">To keep the app simple, I left out client-side validation, so if there is a problem with the password format, you'll get a 400 (Bad Request) error.</span></span>

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

<span data-ttu-id="514d4-194">[**註冊**] 按鈕會將 POST 要求傳送至 ~/api/Account/Register/。</span><span class="sxs-lookup"><span data-stu-id="514d4-194">The **Register** button sends a POST request to ~/api/Account/Register/.</span></span> <span data-ttu-id="514d4-195">要求主體是包含名稱和密碼的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="514d4-195">The request body is a JSON object that holds the name and password.</span></span> <span data-ttu-id="514d4-196">以下是用來傳送要求的 JavaScript 程式碼：</span><span class="sxs-lookup"><span data-stu-id="514d4-196">Here is the JavaScript code that sends the request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

<span data-ttu-id="514d4-197">HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="514d4-197">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

<span data-ttu-id="514d4-198">HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="514d4-198">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

<span data-ttu-id="514d4-199">此要求是由 `AccountController` 類別所處理。</span><span class="sxs-lookup"><span data-stu-id="514d4-199">This request is handled by the `AccountController` class.</span></span> <span data-ttu-id="514d4-200">就內部而言，`AccountController` 會使用 ASP.NET Identity 來管理成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="514d4-200">Internally, `AccountController` uses ASP.NET Identity to manage the membership database.</span></span>

<span data-ttu-id="514d4-201">如果您從 Visual Studio 在本機執行應用程式，則使用者帳戶會儲存在 LocalDB 的 AspNetUsers 資料表中。</span><span class="sxs-lookup"><span data-stu-id="514d4-201">If you run the app locally from Visual Studio, user accounts are stored in LocalDB, in the AspNetUsers table.</span></span> <span data-ttu-id="514d4-202">若要在 Visual Studio 中查看資料表，請按一下 [ **view** ] 功能表，選取 [**伺服器總管**]，然後展開 [**資料連線**]。</span><span class="sxs-lookup"><span data-stu-id="514d4-202">To view the tables in Visual Studio, click the **View** menu, select **Server Explorer**, then expand **Data Connections**.</span></span>

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a><span data-ttu-id="514d4-203">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="514d4-203">Get an Access Token</span></span>

<span data-ttu-id="514d4-204">到目前為止，我們尚未完成任何 OAuth，但我們現在會在要求存取權杖時，看到 OAuth 授權伺服器的運作方式。</span><span class="sxs-lookup"><span data-stu-id="514d4-204">So far we have not done any OAuth, but now we'll see the OAuth authorization server in action, when we request an access token.</span></span> <span data-ttu-id="514d4-205">在範例應用程式的 [**登入**] 區域中，輸入電子郵件和密碼，然後按一下 [**登入**]。</span><span class="sxs-lookup"><span data-stu-id="514d4-205">In the **Log In** area of the sample app, enter the email and password and click **Log In**.</span></span>

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

<span data-ttu-id="514d4-206">[**登入**] 按鈕會將要求傳送至權杖端點。</span><span class="sxs-lookup"><span data-stu-id="514d4-206">The **Log In** button sends a request to the token endpoint.</span></span> <span data-ttu-id="514d4-207">要求的主體包含下列表單 url 編碼的資料：</span><span class="sxs-lookup"><span data-stu-id="514d4-207">The body of the request contains the following form-url-encoded data:</span></span>

- <span data-ttu-id="514d4-208">授與\_類型：「密碼」</span><span class="sxs-lookup"><span data-stu-id="514d4-208">grant\_type: "password"</span></span>
- <span data-ttu-id="514d4-209">username： &lt;使用者的電子郵件&gt;</span><span class="sxs-lookup"><span data-stu-id="514d4-209">username: &lt;the user's email&gt;</span></span>
- <span data-ttu-id="514d4-210">密碼： &lt;密碼&gt;</span><span class="sxs-lookup"><span data-stu-id="514d4-210">password: &lt;password&gt;</span></span>

<span data-ttu-id="514d4-211">以下是傳送 AJAX 要求的 JavaScript 程式碼：</span><span class="sxs-lookup"><span data-stu-id="514d4-211">Here is the JavaScript code that sends the AJAX request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

<span data-ttu-id="514d4-212">如果要求成功，則授權伺服器會在回應主體中傳回存取權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-212">If the request succeeds, the authorization server returns an access token in the response body.</span></span> <span data-ttu-id="514d4-213">請注意，我們會將權杖儲存在會話儲存體中，以便稍後將要求傳送至 API 時使用。</span><span class="sxs-lookup"><span data-stu-id="514d4-213">Notice that we store the token in session storage, to use later when sending requests to the API.</span></span> <span data-ttu-id="514d4-214">不同于某些形式的驗證（例如以 cookie 為基礎的驗證），瀏覽器不會在後續要求中自動包含存取權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-214">Unlike some forms of authentication (such as cookie-based authentication), the browser will not automatically include the access token in subsequent requests.</span></span> <span data-ttu-id="514d4-215">應用程式必須明確地執行此動作。</span><span class="sxs-lookup"><span data-stu-id="514d4-215">The application must do so explicitly.</span></span> <span data-ttu-id="514d4-216">這是件好事，因為它會限制[CSRF 的弱點](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="514d4-216">That's a good thing, because it limits [CSRF vulnerabilities](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="514d4-217">HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="514d4-217">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

<span data-ttu-id="514d4-218">您可以看到要求包含使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="514d4-218">You can see that the request contains the user's credentials.</span></span> <span data-ttu-id="514d4-219">您*必須*使用 HTTPS 來提供傳輸層安全性。</span><span class="sxs-lookup"><span data-stu-id="514d4-219">You *must* use HTTPS to provide transport layer security.</span></span>

<span data-ttu-id="514d4-220">HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="514d4-220">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

<span data-ttu-id="514d4-221">為了方便起見，我已縮排 JSON 並截斷存取權杖，這是相當長的時間。</span><span class="sxs-lookup"><span data-stu-id="514d4-221">For readability, I indented the JSON and truncated the access token, which is a quite long.</span></span>

<span data-ttu-id="514d4-222">`access_token`、`token_type`和 `expires_in` 屬性是由 OAuth2 規格所定義。其他屬性（`userName`、`.issued`和 `.expires`）僅供資訊參考之用。</span><span class="sxs-lookup"><span data-stu-id="514d4-222">The `access_token`, `token_type`, and `expires_in` properties are defined by the OAuth2 spec. The other properties (`userName`, `.issued`, and `.expires`) are just for informational purposes.</span></span> <span data-ttu-id="514d4-223">在/Providers/ApplicationOAuthProvider.cs 檔案中，您可以在 `TokenEndpoint` 方法中找到新增這些額外屬性的程式碼。</span><span class="sxs-lookup"><span data-stu-id="514d4-223">You can find the code that adds those additional properties in the `TokenEndpoint` method, in the /Providers/ApplicationOAuthProvider.cs file.</span></span>

## <a name="send-an-authenticated-request"></a><span data-ttu-id="514d4-224">傳送已驗證的要求</span><span class="sxs-lookup"><span data-stu-id="514d4-224">Send an Authenticated Request</span></span>

<span data-ttu-id="514d4-225">既然我們已擁有持有人權杖，我們就可以向 API 提出已驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="514d4-225">Now that we have a bearer token, we can make an authenticated request to the API.</span></span> <span data-ttu-id="514d4-226">這是藉由在要求中設定 Authorization 標頭來完成。</span><span class="sxs-lookup"><span data-stu-id="514d4-226">This is done by setting the Authorization header in the request.</span></span> <span data-ttu-id="514d4-227">再次按一下 [**呼叫 API** ] 按鈕以查看此情況。</span><span class="sxs-lookup"><span data-stu-id="514d4-227">Click the **Call API** button again to see this.</span></span>

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

<span data-ttu-id="514d4-228">HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="514d4-228">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

<span data-ttu-id="514d4-229">HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="514d4-229">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a><span data-ttu-id="514d4-230">登出</span><span class="sxs-lookup"><span data-stu-id="514d4-230">Log Out</span></span>

<span data-ttu-id="514d4-231">因為瀏覽器不會快取認證或存取權杖，所以登出只是「忘記」權杖，方法是從會話儲存體中移除它：</span><span class="sxs-lookup"><span data-stu-id="514d4-231">Because the browser does not cache the credentials or the access token, logging out is simply a matter of "forgetting" the token, by removing it from session storage:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a><span data-ttu-id="514d4-232">瞭解個別帳戶專案範本</span><span class="sxs-lookup"><span data-stu-id="514d4-232">Understanding the Individual Accounts Project Template</span></span>

<span data-ttu-id="514d4-233">當您選取 ASP.NET Web 應用程式專案範本中的**個別帳戶**時，專案會包含：</span><span class="sxs-lookup"><span data-stu-id="514d4-233">When you select **Individual Accounts** in the ASP.NET Web Application project template, the project includes:</span></span>

- <span data-ttu-id="514d4-234">OAuth2 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-234">An OAuth2 authorization server.</span></span>
- <span data-ttu-id="514d4-235">用於管理使用者帳戶的 Web API 端點</span><span class="sxs-lookup"><span data-stu-id="514d4-235">A Web API endpoint for managing user accounts</span></span>
- <span data-ttu-id="514d4-236">用來儲存使用者帳戶的 EF 模型。</span><span class="sxs-lookup"><span data-stu-id="514d4-236">An EF model for storing user accounts.</span></span>

<span data-ttu-id="514d4-237">以下是用來執行這些功能的主要應用程式類別：</span><span class="sxs-lookup"><span data-stu-id="514d4-237">Here are the main application classes that implement these features:</span></span>

- <span data-ttu-id="514d4-238">`AccountController`</span><span class="sxs-lookup"><span data-stu-id="514d4-238">`AccountController`.</span></span> <span data-ttu-id="514d4-239">提供用來管理使用者帳戶的 Web API 端點。</span><span class="sxs-lookup"><span data-stu-id="514d4-239">Provides a Web API endpoint for managing user accounts.</span></span> <span data-ttu-id="514d4-240">`Register` 動作是我們在本教學課程中唯一使用的動作。</span><span class="sxs-lookup"><span data-stu-id="514d4-240">The `Register` action is the only one that we used in this tutorial.</span></span> <span data-ttu-id="514d4-241">類別上的其他方法則支援密碼重設、社交登入和其他功能。</span><span class="sxs-lookup"><span data-stu-id="514d4-241">Other methods on the class support password reset, social logins, and other functionality.</span></span>
- <span data-ttu-id="514d4-242">`ApplicationUser`，定義于/Models/IdentityModels.cs。</span><span class="sxs-lookup"><span data-stu-id="514d4-242">`ApplicationUser`, defined in /Models/IdentityModels.cs.</span></span> <span data-ttu-id="514d4-243">這個類別是成員資格資料庫中使用者帳戶的 EF 模型。</span><span class="sxs-lookup"><span data-stu-id="514d4-243">This class is the EF model for user accounts in the membership database.</span></span>
- <span data-ttu-id="514d4-244">`ApplicationUserManager`（定義于/App\_Start/IdentityConfig）。此類別衍生自[UserManager](https://msdn.microsoft.com/library/dn613290.aspx)並在使用者帳戶上執行作業，例如建立新的使用者、驗證密碼等等，並自動儲存資料庫的變更。</span><span class="sxs-lookup"><span data-stu-id="514d4-244">`ApplicationUserManager`, defined in /App\_Start/IdentityConfig.cs This class derives from [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) and performs operations on user accounts, such as creating a new user, verifying passwords, and so forth, and automatically persists changes to the database.</span></span>
- <span data-ttu-id="514d4-245">`ApplicationOAuthProvider`</span><span class="sxs-lookup"><span data-stu-id="514d4-245">`ApplicationOAuthProvider`.</span></span> <span data-ttu-id="514d4-246">此物件會插入至 OWIN 中介軟體，並處理中介軟體所引發的事件。</span><span class="sxs-lookup"><span data-stu-id="514d4-246">This object plugs into the OWIN middleware, and processes events raised by the middleware.</span></span> <span data-ttu-id="514d4-247">它衍生自[OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)。</span><span class="sxs-lookup"><span data-stu-id="514d4-247">It derives from [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx).</span></span>

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a><span data-ttu-id="514d4-248">設定授權伺服器</span><span class="sxs-lookup"><span data-stu-id="514d4-248">Configuring the Authorization Server</span></span>

<span data-ttu-id="514d4-249">在 StartupAuth.cs 中，下列程式碼會設定 OAuth2 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="514d4-249">In StartupAuth.cs, the following code configures the OAuth2 authorization server.</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

<span data-ttu-id="514d4-250">`TokenEndpointPath` 屬性是授權伺服器端點的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="514d4-250">The `TokenEndpointPath` property is the URL path to the authorization server endpoint.</span></span> <span data-ttu-id="514d4-251">這是應用程式用來取得持有人權杖的 URL。</span><span class="sxs-lookup"><span data-stu-id="514d4-251">That's the URL that app uses to get the bearer tokens.</span></span>

<span data-ttu-id="514d4-252">`Provider` 屬性指定的提供者會插入 OWIN 中介軟體，並處理中介軟體所引發的事件。</span><span class="sxs-lookup"><span data-stu-id="514d4-252">The `Provider` property specifies a provider that plugs into the OWIN middleware, and processes events raised by the middleware.</span></span>

<span data-ttu-id="514d4-253">以下是應用程式想要取得權杖的基本流程：</span><span class="sxs-lookup"><span data-stu-id="514d4-253">Here is the basic flow when the app wants to get a token:</span></span>

1. <span data-ttu-id="514d4-254">若要取得存取權杖，應用程式會將要求傳送至 ~/Token。</span><span class="sxs-lookup"><span data-stu-id="514d4-254">To get an access token, the app sends a request to ~/Token.</span></span>
2. <span data-ttu-id="514d4-255">OAuth 中介軟體會呼叫提供者上 `GrantResourceOwnerCredentials`。</span><span class="sxs-lookup"><span data-stu-id="514d4-255">The OAuth middleware calls `GrantResourceOwnerCredentials` on the provider.</span></span>
3. <span data-ttu-id="514d4-256">提供者會呼叫 `ApplicationUserManager` 來驗證認證，並建立宣告身分識別。</span><span class="sxs-lookup"><span data-stu-id="514d4-256">The provider calls the `ApplicationUserManager` to validate the credentials and create a claims identity.</span></span>
4. <span data-ttu-id="514d4-257">如果成功，提供者會建立驗證票證，用來產生權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-257">If that succeeds, the provider creates an authentication ticket, which is used to generate the token.</span></span>

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

<span data-ttu-id="514d4-258">OAuth 中介軟體不知道使用者帳戶的任何內容。</span><span class="sxs-lookup"><span data-stu-id="514d4-258">The OAuth middleware doesn't know anything about the user accounts.</span></span> <span data-ttu-id="514d4-259">提供者會在中介軟體和 ASP.NET Identity 之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="514d4-259">The provider communicates between the middleware and ASP.NET Identity.</span></span> <span data-ttu-id="514d4-260">如需有關如何執行授權伺服器的詳細資訊，請參閱[OWIN OAuth 2.0 Authorization server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)。</span><span class="sxs-lookup"><span data-stu-id="514d4-260">For more information about implementing the authorization server, see [OWIN OAuth 2.0 Authorization Server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md).</span></span>

### <a name="configuring-web-api-to-use-bearer-tokens"></a><span data-ttu-id="514d4-261">設定 Web API 以使用持有人權杖</span><span class="sxs-lookup"><span data-stu-id="514d4-261">Configuring Web API to use Bearer Tokens</span></span>

<span data-ttu-id="514d4-262">在 `WebApiConfig.Register` 方法中，下列程式碼會設定 Web API 管線的驗證：</span><span class="sxs-lookup"><span data-stu-id="514d4-262">In the `WebApiConfig.Register` method, the following code sets up authentication for the Web API pipeline:</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

<span data-ttu-id="514d4-263">**HostAuthenticationFilter**類別可讓您使用持有人權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="514d4-263">The **HostAuthenticationFilter** class enables authentication using bearer tokens.</span></span>

<span data-ttu-id="514d4-264">**Config.suppressdefaulthostauthentication**方法會指示 Web api 忽略在要求抵達 Web api 管線之前，由 IIS 或 OWIN 中介軟體所發生的任何驗證。</span><span class="sxs-lookup"><span data-stu-id="514d4-264">The **SuppressDefaultHostAuthentication** method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware.</span></span> <span data-ttu-id="514d4-265">如此一來，我們可以限制 Web API 只驗證使用持有人權杖的要求。</span><span class="sxs-lookup"><span data-stu-id="514d4-265">That way, we can restrict Web API to authenticate only using bearer tokens.</span></span>

> [!NOTE]
> <span data-ttu-id="514d4-266">特別是，您應用程式的 MVC 部分可能會使用表單驗證，這會將認證儲存在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="514d4-266">In particular, the MVC portion of your app might use forms authentication, which stores credentials in a cookie.</span></span> <span data-ttu-id="514d4-267">以 Cookie 為基礎的驗證需要使用防偽權杖，以防止 CSRF 攻擊。</span><span class="sxs-lookup"><span data-stu-id="514d4-267">Cookie-based authentication requires the use of anti-forgery tokens, to prevent CSRF attacks.</span></span> <span data-ttu-id="514d4-268">這是 web Api 的問題，因為 Web API 無法方便地將防偽權杖傳送給用戶端。</span><span class="sxs-lookup"><span data-stu-id="514d4-268">That's a problem for web APIs, because there is no convenient way for the web API to send the anti-forgery token to the client.</span></span> <span data-ttu-id="514d4-269">（如需此問題的詳細背景，請參閱[防止 WEB API 中的 CSRF 攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)）。呼叫**config.suppressdefaulthostauthentication**可確保 Web API 不容易受到 cookie 中儲存之認證的 CSRF 攻擊。</span><span class="sxs-lookup"><span data-stu-id="514d4-269">(For more background on this issue, see [Preventing CSRF Attacks in Web API](preventing-cross-site-request-forgery-csrf-attacks.md).) Calling **SuppressDefaultHostAuthentication** ensures that Web API is not vulnerable to CSRF attacks from credentials stored in cookies.</span></span>

<span data-ttu-id="514d4-270">當用戶端要求受保護的資源時，以下是 Web API 管線中發生的情況：</span><span class="sxs-lookup"><span data-stu-id="514d4-270">When the client requests a protected resource, here is what happens in the Web API pipeline:</span></span>

1. <span data-ttu-id="514d4-271">**HostAuthentication**篩選準則會呼叫 OAuth 中介軟體來驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="514d4-271">The **HostAuthentication** filter calls the OAuth middleware to validate the token.</span></span>
2. <span data-ttu-id="514d4-272">中介軟體會將權杖轉換成宣告身分識別。</span><span class="sxs-lookup"><span data-stu-id="514d4-272">The middleware converts the token into a claims identity.</span></span>
3. <span data-ttu-id="514d4-273">此時，要求已*通過驗證*，但未*獲授權*。</span><span class="sxs-lookup"><span data-stu-id="514d4-273">At this point, the request is *authenticated* but not *authorized*.</span></span>
4. <span data-ttu-id="514d4-274">授權篩選準則會檢查宣告身分識別。</span><span class="sxs-lookup"><span data-stu-id="514d4-274">The authorization filter examines the claims identity.</span></span> <span data-ttu-id="514d4-275">如果宣告會授權該資源的使用者，則要求已獲得授權。</span><span class="sxs-lookup"><span data-stu-id="514d4-275">If the claims authorize the user for that resource, the request is authorized.</span></span> <span data-ttu-id="514d4-276">根據預設， **[授權]** 屬性會授權任何已驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="514d4-276">By default, the **[Authorize]** attribute will authorize any request that is authenticated.</span></span> <span data-ttu-id="514d4-277">不過，您可以依角色或其他宣告進行授權。</span><span class="sxs-lookup"><span data-stu-id="514d4-277">However, you can authorize by role or by other claims.</span></span> <span data-ttu-id="514d4-278">如需詳細資訊，請參閱[WEB API 中的驗證和授權](authentication-and-authorization-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="514d4-278">For more information, see [Authentication and Authorization in Web API](authentication-and-authorization-in-aspnet-web-api.md).</span></span>
5. <span data-ttu-id="514d4-279">如果先前的步驟成功，控制器會傳回受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="514d4-279">If the previous steps are successful, the controller returns the protected resource.</span></span> <span data-ttu-id="514d4-280">否則，用戶端會收到401（未經授權）錯誤。</span><span class="sxs-lookup"><span data-stu-id="514d4-280">Otherwise, the client receives a 401 (Unauthorized) error.</span></span>

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a><span data-ttu-id="514d4-281">其他資源</span><span class="sxs-lookup"><span data-stu-id="514d4-281">Additional Resources</span></span>

- [<span data-ttu-id="514d4-282">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="514d4-282">ASP.NET Identity</span></span>](../../../identity/index.md)
- <span data-ttu-id="514d4-283">[瞭解 VS2013 RC 的 SPA 範本中的安全性功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)。</span><span class="sxs-lookup"><span data-stu-id="514d4-283">[Understanding Security Features in the SPA Template for VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx).</span></span> <span data-ttu-id="514d4-284">Hongye Sun 的 MSDN blog 文章。</span><span class="sxs-lookup"><span data-stu-id="514d4-284">MSDN blog post by Hongye Sun.</span></span>
- <span data-ttu-id="514d4-285">[剖析 WEB API 個別帳戶範本-第2部分：本機帳戶](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)。</span><span class="sxs-lookup"><span data-stu-id="514d4-285">[Dissecting the Web API Individual Accounts Template–Part 2: Local Accounts](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/).</span></span> <span data-ttu-id="514d4-286">Dominick Baier 的 Blog 文章。</span><span class="sxs-lookup"><span data-stu-id="514d4-286">Blog post by Dominick Baier.</span></span>
- <span data-ttu-id="514d4-287">[主機驗證和使用 OWIN 的 WEB API](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)。</span><span class="sxs-lookup"><span data-stu-id="514d4-287">[Host authentication and Web API with OWIN](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/).</span></span> <span data-ttu-id="514d4-288">Brock Allen 的 `SuppressDefaultHostAuthentication` 和 `HostAuthenticationFilter` 的良好說明。</span><span class="sxs-lookup"><span data-stu-id="514d4-288">A good explanation of `SuppressDefaultHostAuthentication` and `HostAuthenticationFilter` by Brock Allen.</span></span>
- <span data-ttu-id="514d4-289">[在 VS 2013 範本的 ASP.NET Identity 中自訂設定檔資訊](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)。</span><span class="sxs-lookup"><span data-stu-id="514d4-289">[Customizing profile information in ASP.NET Identity in VS 2013 templates](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx).</span></span> <span data-ttu-id="514d4-290">MSDN blog 文章，請 Pranav 請參閱 rastogi。</span><span class="sxs-lookup"><span data-stu-id="514d4-290">MSDN blog post by Pranav Rastogi.</span></span>
- <span data-ttu-id="514d4-291">[ASP.NET Identity 中 UserManager 類別的每個要求存留期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="514d4-291">[Per request lifetime management for UserManager class in ASP.NET Identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).</span></span> <span data-ttu-id="514d4-292">MSDN blog 文章，請 Suhas Joshi，並提供 `UserManager` 類別的良好說明。</span><span class="sxs-lookup"><span data-stu-id="514d4-292">MSDN blog post by Suhas Joshi, with a good explanation of the `UserManager` class.</span></span>
