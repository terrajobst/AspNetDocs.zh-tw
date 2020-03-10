---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 使用登入、電子郵件確認和密碼重設（C#）建立安全的 ASP.NET MVC 5 web 應用程式 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程會示範如何使用 ASP.NET Identity 成員資格系統，以電子郵件確認和密碼重設來建立 ASP.NET MVC 5 web 應用程式。 您的 ca 。
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 6169c972ad0f4ee2079d3638c54a5accc4b8b3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538343"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="fdfac-104">使用登入、電子郵件確認和密碼重設建立安全的 ASP.NET MVC 5 Web 應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="fdfac-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="fdfac-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fdfac-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="fdfac-106">本教學課程會示範如何使用 ASP.NET Identity 成員資格系統，以電子郵件確認和密碼重設來建立 ASP.NET MVC 5 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdfac-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span>

<span data-ttu-id="fdfac-107">如需本教學課程中使用 .NET Core 的更新版本，請參閱[ASP.NET Core 中的帳戶確認和密碼](/aspnet/core/security/authentication/accconfirm)復原。</span><span class="sxs-lookup"><span data-stu-id="fdfac-107">For an updated version of this tutorial that uses .NET Core, see [Account confirmation and password recovery in ASP.NET Core](/aspnet/core/security/authentication/accconfirm).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="fdfac-108">建立 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdfac-108">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="fdfac-109">一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。</span><span class="sxs-lookup"><span data-stu-id="fdfac-109">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="fdfac-110">安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本。</span><span class="sxs-lookup"><span data-stu-id="fdfac-110">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="fdfac-111">警告：您必須安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="fdfac-111">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="fdfac-112">建立新的 ASP.NET Web 專案，並選取 [MVC] 範本。</span><span class="sxs-lookup"><span data-stu-id="fdfac-112">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="fdfac-113">Web form 也支援 ASP.NET Identity，因此您可以在 web Forms 應用程式中遵循類似的步驟。</span><span class="sxs-lookup"><span data-stu-id="fdfac-113">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="fdfac-114">將預設驗證保留為**個別使用者帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fdfac-114">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="fdfac-115">如果您想要在 Azure 中裝載應用程式，請將此核取方塊保留為已核取狀態。</span><span class="sxs-lookup"><span data-stu-id="fdfac-115">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="fdfac-116">稍後在本教學課程中，我們將部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="fdfac-116">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="fdfac-117">您可以[免費開啟 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="fdfac-117">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="fdfac-118">將[專案設定為使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="fdfac-118">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="fdfac-119">執行應用程式，按一下 [**註冊**] 連結並註冊使用者。</span><span class="sxs-lookup"><span data-stu-id="fdfac-119">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="fdfac-120">此時，電子郵件上的唯一驗證是使用[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="fdfac-120">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="fdfac-121">在伺服器總管中，流覽至 [**資料 Connections\DefaultConnection\Tables\AspNetUsers**]，以滑鼠右鍵按一下，然後選取 [**開啟資料表定義**]。</span><span class="sxs-lookup"><span data-stu-id="fdfac-121">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="fdfac-122">下圖顯示 `AspNetUsers` 架構：</span><span class="sxs-lookup"><span data-stu-id="fdfac-122">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="fdfac-123">以滑鼠右鍵按一下 [ **AspNetUsers** ] 資料表，然後選取 [**顯示資料表資料**]。</span><span class="sxs-lookup"><span data-stu-id="fdfac-123">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="fdfac-124">此時尚未確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fdfac-124">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="fdfac-125">按一下資料列，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="fdfac-125">Click on the row and select delete.</span></span> <span data-ttu-id="fdfac-126">您會在下一個步驟中再次新增這封電子郵件，並傳送確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fdfac-126">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="fdfac-127">電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="fdfac-127">Email confirmation</span></span>

<span data-ttu-id="fdfac-128">最佳做法是確認新使用者註冊的電子郵件，以確認他們不會模擬其他人（也就是他們尚未向他人的電子郵件註冊）。</span><span class="sxs-lookup"><span data-stu-id="fdfac-128">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="fdfac-129">假設您有一個討論論壇，您會想要防止 `"bob@example.com"` 註冊為 `"joe@contoso.com"`。</span><span class="sxs-lookup"><span data-stu-id="fdfac-129">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="fdfac-130">若未確認電子郵件，`"joe@contoso.com"` 可能會從您的應用程式收到不必要的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fdfac-130">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="fdfac-131">假設 Bob 不小心註冊為 `"bib@example.com"` 且未注意到，他將無法使用密碼復原，因為應用程式沒有正確的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fdfac-131">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="fdfac-132">電子郵件確認僅為 bot 提供有限的保護，並不會提供保護來防止被判定的垃圾郵件，他們有許多可使用的電子郵件別名來進行註冊。</span><span class="sxs-lookup"><span data-stu-id="fdfac-132">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="fdfac-133">您通常會想要防止新使用者將任何資料張貼到您的網站，然後再由電子郵件、SMS 文字訊息或其他機制確認。</span><span class="sxs-lookup"><span data-stu-id="fdfac-133">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="fdfac-134">在下列各節中，我們將啟用電子郵件確認並修改程式碼，以防止新註冊的使用者登入，直到他們的電子郵件確認為止。</span><span class="sxs-lookup"><span data-stu-id="fdfac-134">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="fdfac-135">連結 SendGrid</span><span class="sxs-lookup"><span data-stu-id="fdfac-135">Hook up SendGrid</span></span>

<span data-ttu-id="fdfac-136">本節中的指示不是最新的。</span><span class="sxs-lookup"><span data-stu-id="fdfac-136">The instructions in this section are not current.</span></span> <span data-ttu-id="fdfac-137">如需更新的指示，請參閱[設定 SendGrid 電子郵件提供者](/aspnet/core/security/authentication/accconfirm#configure-email-provider)。</span><span class="sxs-lookup"><span data-stu-id="fdfac-137">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="fdfac-138">雖然本教學課程僅示範如何透過[SendGrid](http://sendgrid.com/)新增電子郵件通知，但您可以使用 SMTP 和其他機制來傳送電子郵件（請參閱[其他資源](#addRes)）。</span><span class="sxs-lookup"><span data-stu-id="fdfac-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="fdfac-139">在 [套件管理器主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="fdfac-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="fdfac-140">移至[Azure SendGrid 註冊頁面](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)，並註冊免費的 SendGrid 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fdfac-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="fdfac-141">藉由在*App_Start/identityconfig.cs*中新增類似下列的程式碼來設定 SendGrid：</span><span class="sxs-lookup"><span data-stu-id="fdfac-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="fdfac-142">您必須新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="fdfac-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="fdfac-143">為了讓此範例保持簡單，我們會將應用程式設定儲存*在 web.config 檔案*中：</span><span class="sxs-lookup"><span data-stu-id="fdfac-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="fdfac-144">安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="fdfac-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="fdfac-145">帳戶和認證會儲存在 appSetting 中。</span><span class="sxs-lookup"><span data-stu-id="fdfac-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="fdfac-146">在 Azure 上，您可以將這些值安全地儲存在 Azure 入口網站的 [ **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="fdfac-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="fdfac-147">請參閱[將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="fdfac-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="fdfac-148">在帳戶控制器中啟用電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="fdfac-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="fdfac-149">確認*Views\Account\ConfirmEmail.cshtml*檔具有正確的 razor 語法。</span><span class="sxs-lookup"><span data-stu-id="fdfac-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="fdfac-150">（可能遺漏第一行中的 @ 字元。</span><span class="sxs-lookup"><span data-stu-id="fdfac-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="fdfac-151">)</span><span class="sxs-lookup"><span data-stu-id="fdfac-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="fdfac-152">執行應用程式，然後按一下 [註冊] 連結。</span><span class="sxs-lookup"><span data-stu-id="fdfac-152">Run the app and click the Register link.</span></span> <span data-ttu-id="fdfac-153">提交註冊表單之後，您就會登入。</span><span class="sxs-lookup"><span data-stu-id="fdfac-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="fdfac-154">檢查您的電子郵件帳戶，然後按一下連結以確認您的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fdfac-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="fdfac-155">在登入之前需要電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="fdfac-155">Require email confirmation before log in</span></span>

<span data-ttu-id="fdfac-156">目前使用者完成註冊表單之後，就會登入。</span><span class="sxs-lookup"><span data-stu-id="fdfac-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="fdfac-157">在登入之前，您通常會想要先確認其電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fdfac-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="fdfac-158">在下一節中，我們會修改程式碼，要求新的使用者在登入（驗證）之前，必須先有已確認的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fdfac-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="fdfac-159">使用下列反白顯示的變更來更新 `HttpPost Register` 方法：</span><span class="sxs-lookup"><span data-stu-id="fdfac-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="fdfac-160">藉由將 `SignInAsync` 方法加上批註，註冊就不會登入使用者。</span><span class="sxs-lookup"><span data-stu-id="fdfac-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="fdfac-161">`TempData["ViewBagLink"] = callbackUrl;` 行可用於在不傳送電子郵件的情況下，對[應用程式](#dbg)和測試註冊進行錯用。</span><span class="sxs-lookup"><span data-stu-id="fdfac-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="fdfac-162">`ViewBag.Message` 可用來顯示確認指示。</span><span class="sxs-lookup"><span data-stu-id="fdfac-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="fdfac-163">[下載範例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)包含程式碼，可在不設定電子郵件的情況下測試電子郵件確認，而且也可以用來對應用程式進行 debug。</span><span class="sxs-lookup"><span data-stu-id="fdfac-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="fdfac-164">建立 `Views\Shared\Info.cshtml` 檔案，並新增下列 razor 標記：</span><span class="sxs-lookup"><span data-stu-id="fdfac-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="fdfac-165">將 [[授權] 屬性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)加入至主控制器的 [`Contact` 動作] 方法。</span><span class="sxs-lookup"><span data-stu-id="fdfac-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="fdfac-166">您可以按一下 [**連絡人**] 連結，確認匿名使用者沒有存取權，且已驗證的使用者的確有存取權。</span><span class="sxs-lookup"><span data-stu-id="fdfac-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="fdfac-167">您也必須更新 `HttpPost Login` 動作方法：</span><span class="sxs-lookup"><span data-stu-id="fdfac-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="fdfac-168">更新 [ *Views\Shared\Error.cshtml* ] 視圖以顯示錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="fdfac-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="fdfac-169">刪除**AspNetUsers**資料表中的任何帳戶，其中包含您想要測試的電子郵件別名。</span><span class="sxs-lookup"><span data-stu-id="fdfac-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="fdfac-170">執行應用程式並確認您無法登入，直到確認您的電子郵件地址為止。</span><span class="sxs-lookup"><span data-stu-id="fdfac-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="fdfac-171">確認您的電子郵件地址之後，請按一下 [**連絡人**] 連結。</span><span class="sxs-lookup"><span data-stu-id="fdfac-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="fdfac-172">密碼修復/重設</span><span class="sxs-lookup"><span data-stu-id="fdfac-172">Password recovery/reset</span></span>

<span data-ttu-id="fdfac-173">從帳戶控制器的 [`HttpPost ForgotPassword` 動作] 方法中移除批註字元：</span><span class="sxs-lookup"><span data-stu-id="fdfac-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="fdfac-174">從*Views\Account\Login.cshtml* razor view 檔案中的 `ForgotPassword` [html.actionlink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx)移除批註字元：</span><span class="sxs-lookup"><span data-stu-id="fdfac-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="fdfac-175">[登入] 頁面現在會顯示重設密碼的連結。</span><span class="sxs-lookup"><span data-stu-id="fdfac-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="fdfac-176">重新傳送電子郵件確認連結</span><span class="sxs-lookup"><span data-stu-id="fdfac-176">Resend email confirmation link</span></span>

<span data-ttu-id="fdfac-177">一旦使用者建立新的本機帳戶，他們就會收到電子郵件，要求他們在登入之前必須先使用確認連結。</span><span class="sxs-lookup"><span data-stu-id="fdfac-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="fdfac-178">如果使用者不小心刪除了確認電子郵件，或電子郵件從未送達，他們就需要再次傳送確認連結。</span><span class="sxs-lookup"><span data-stu-id="fdfac-178">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="fdfac-179">下列程式碼變更顯示如何啟用此動作。</span><span class="sxs-lookup"><span data-stu-id="fdfac-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="fdfac-180">將下列 helper 方法新增至*Controllers\AccountController.cs*檔案的底部：</span><span class="sxs-lookup"><span data-stu-id="fdfac-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="fdfac-181">更新 Register 方法以使用新的協助程式：</span><span class="sxs-lookup"><span data-stu-id="fdfac-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="fdfac-182">如果尚未確認使用者帳戶，請更新登入方法以重新傳送密碼：</span><span class="sxs-lookup"><span data-stu-id="fdfac-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="fdfac-183">合併社交和本機登入帳戶</span><span class="sxs-lookup"><span data-stu-id="fdfac-183">Combine social and local login accounts</span></span>

<span data-ttu-id="fdfac-184">您可以按一下電子郵件連結，以合併本機和社交帳戶。</span><span class="sxs-lookup"><span data-stu-id="fdfac-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="fdfac-185">在下列順序中 **RickAndMSFT@gmail.com** 會先建立為本機登入，但您可以先將帳戶建立為社交記錄，然後再新增本機登入。</span><span class="sxs-lookup"><span data-stu-id="fdfac-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="fdfac-186">按一下 [**管理**] 連結。</span><span class="sxs-lookup"><span data-stu-id="fdfac-186">Click on the **Manage** link.</span></span> <span data-ttu-id="fdfac-187">請注意與此帳戶相關聯的外部登入 **： 0** 。</span><span class="sxs-lookup"><span data-stu-id="fdfac-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="fdfac-188">按一下另一個登入服務的連結，並接受應用程式要求。</span><span class="sxs-lookup"><span data-stu-id="fdfac-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="fdfac-189">已合併這兩個帳戶，您將能夠使用任一帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="fdfac-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="fdfac-190">您可能想要讓使用者新增本機帳戶，以防其社交記錄在驗證服務已關閉，或更有可能失去其社交帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="fdfac-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="fdfac-191">在下圖中，Tom 是社交記錄（您可以從頁面上顯示的 [**外部登入： 1** ] 看到）。</span><span class="sxs-lookup"><span data-stu-id="fdfac-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="fdfac-192">按一下 [**挑選密碼**] 可讓您新增與相同帳戶相關聯的本機登入。</span><span class="sxs-lookup"><span data-stu-id="fdfac-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="fdfac-193">深入瞭解電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="fdfac-193">Email confirmation in more depth</span></span>

<span data-ttu-id="fdfac-194">我的教學課程[帳戶確認和密碼復原與 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)會前往本主題中的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fdfac-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="fdfac-195">偵錯工具</span><span class="sxs-lookup"><span data-stu-id="fdfac-195">Debugging the app</span></span>

<span data-ttu-id="fdfac-196">如果您沒有收到包含連結的電子郵件：</span><span class="sxs-lookup"><span data-stu-id="fdfac-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="fdfac-197">檢查您的垃圾郵件資料夾。</span><span class="sxs-lookup"><span data-stu-id="fdfac-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="fdfac-198">登入您的 SendGrid 帳戶，然後按一下 [[電子郵件活動] 連結](https://sendgrid.com/logs/index)。</span><span class="sxs-lookup"><span data-stu-id="fdfac-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="fdfac-199">若要測試不含電子郵件的驗證連結，請下載[完整的範例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。</span><span class="sxs-lookup"><span data-stu-id="fdfac-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="fdfac-200">確認連結和確認碼將會顯示在頁面上。</span><span class="sxs-lookup"><span data-stu-id="fdfac-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="fdfac-201">其他資源</span><span class="sxs-lookup"><span data-stu-id="fdfac-201">Additional Resources</span></span>

- [<span data-ttu-id="fdfac-202">ASP.NET Identity 建議資源的連結</span><span class="sxs-lookup"><span data-stu-id="fdfac-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="fdfac-203">[使用 ASP.NET Identity 進行帳戶確認和密碼](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)復原深入瞭解密碼修復和帳戶確認。</span><span class="sxs-lookup"><span data-stu-id="fdfac-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="fdfac-204">[使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教學課程說明如何使用 Facebook 和 Google OAuth 2 授權撰寫 ASP.NET MVC 5 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdfac-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="fdfac-205">它也會示範如何將其他資料新增至身分識別資料庫。</span><span class="sxs-lookup"><span data-stu-id="fdfac-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="fdfac-206">[將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署至 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="fdfac-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="fdfac-207">本教學課程會新增 Azure 部署、如何以角色保護您的應用程式、如何使用成員資格 API 來新增使用者和角色，以及其他安全性功能。</span><span class="sxs-lookup"><span data-stu-id="fdfac-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="fdfac-208">建立適用于 OAuth 2 的 Google 應用程式，並將應用程式連接到專案</span><span class="sxs-lookup"><span data-stu-id="fdfac-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="fdfac-209">在 Facebook 中建立應用程式，並將應用程式連接到專案</span><span class="sxs-lookup"><span data-stu-id="fdfac-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="fdfac-210">在專案中設定 SSL</span><span class="sxs-lookup"><span data-stu-id="fdfac-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
