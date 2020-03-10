---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: 使用 SMS 的雙因素驗證與 ASP.NET Identity ASP.NET 4.x 的電子郵件
author: HaoK
description: 本教學課程將說明如何使用 SMS 和電子郵件來設定雙因素驗證（2FA）。 這篇文章是由 Rick Anderson （@RickAndMSFT），Pr 。
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 527b4392846e60dae0b216fdeabf21fd6618e4d7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616680"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="48425-104">使用 SMS 的雙因素驗證與 ASP.NET Identity 的電子郵件</span><span class="sxs-lookup"><span data-stu-id="48425-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>

<span data-ttu-id="48425-105">by [Hao Kung](https://github.com/HaoK)、 [Pranav 請參閱 rastogi](https://github.com/rustd)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Suhas Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="48425-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="48425-106">本教學課程將說明如何使用 SMS 和電子郵件來設定雙因素驗證（2FA）。</span><span class="sxs-lookup"><span data-stu-id="48425-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="48425-107">這篇文章是由 Rick Anderson （[@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)）、Pranav 請參閱 rastogi （[@rustd](https://twitter.com/rustd)）、Hao Kung 和 Suhas Joshi 所撰寫。</span><span class="sxs-lookup"><span data-stu-id="48425-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="48425-108">NuGet 範例主要是由 Hao Kung 所撰寫。</span><span class="sxs-lookup"><span data-stu-id="48425-108">The NuGet sample was written primarily by Hao Kung.</span></span>

<span data-ttu-id="48425-109">本主題包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="48425-109">This topic covers the following:</span></span>

- [<span data-ttu-id="48425-110">建立身分識別範例</span><span class="sxs-lookup"><span data-stu-id="48425-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="48425-111">設定 SMS 以進行雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="48425-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="48425-112">啟用雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="48425-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="48425-113">如何註冊雙因素驗證提供者</span><span class="sxs-lookup"><span data-stu-id="48425-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="48425-114">合併社交和本機登入帳戶</span><span class="sxs-lookup"><span data-stu-id="48425-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="48425-115">從暴力密碼破解攻擊的帳戶鎖定</span><span class="sxs-lookup"><span data-stu-id="48425-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="48425-116">建立身分識別範例</span><span class="sxs-lookup"><span data-stu-id="48425-116">Building the Identity sample</span></span>

<span data-ttu-id="48425-117">在本節中，您將使用 NuGet 來下載我們將使用的範例。</span><span class="sxs-lookup"><span data-stu-id="48425-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="48425-118">一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。</span><span class="sxs-lookup"><span data-stu-id="48425-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="48425-119">安裝 Visual Studio [2013 Update 2 或更新](https://go.microsoft.com/fwlink/?LinkId=390521)版本。</span><span class="sxs-lookup"><span data-stu-id="48425-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="48425-120">警告：您必須安裝 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) ，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="48425-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>

1. <span data-ttu-id="48425-121">建立新的***空白***ASP.NET Web 專案。</span><span class="sxs-lookup"><span data-stu-id="48425-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="48425-122">在 [套件管理員主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="48425-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="48425-123">在本教學課程中，我們將使用[SendGrid](http://sendgrid.com/)來傳送電子郵件和[Twilio](https://www.twilio.com/) ，或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) sms 傳送。</span><span class="sxs-lookup"><span data-stu-id="48425-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="48425-124">`Identity.Samples` 套件會安裝我們要使用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="48425-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="48425-125">將[專案設定為使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="48425-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="48425-126">*選擇性*：遵循我的[電子郵件確認教學](account-confirmation-and-password-recovery-with-aspnet-identity.md)課程中的指示來連結 SendGrid，然後執行應用程式並註冊電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="48425-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="48425-127">*選擇性：* 移除範例中的電子郵件連結確認代碼（帳戶控制器中的 `ViewBag.Link` 程式碼。</span><span class="sxs-lookup"><span data-stu-id="48425-127">*Optional:* Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="48425-128">請參閱 `DisplayEmail` 和 `ForgotPasswordConfirmation` 動作方法和 razor views）。</span><span class="sxs-lookup"><span data-stu-id="48425-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="48425-129">*選擇性：* 從 [管理] 和 [帳戶控制器]，以及從*Views\Account\VerifyCode.cshtml*和*Views\Manage\VerifyPhoneNumber.cshtml* razor Views 移除 `ViewBag.Status` 程式碼。</span><span class="sxs-lookup"><span data-stu-id="48425-129">*Optional:* Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml* and *Views\Manage\VerifyPhoneNumber.cshtml* razor views.</span></span> <span data-ttu-id="48425-130">或者，您可以保留 `ViewBag.Status` 顯示，以測試此應用程式在本機運作的方式，而不需要連結和傳送電子郵件和 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="48425-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="48425-131">警告：如果您變更此範例中的任何安全性設定，生產應用程式將需要進行安全性審核，以明確地呼叫所做的變更。</span><span class="sxs-lookup"><span data-stu-id="48425-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="48425-132">設定 SMS 以進行雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="48425-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="48425-133">本教學課程提供使用 Twilio 或 ASPSMS 的指示，但是您可以使用任何其他 SMS 提供者。</span><span class="sxs-lookup"><span data-stu-id="48425-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="48425-134">**使用 SMS 提供者建立使用者帳戶**</span><span class="sxs-lookup"><span data-stu-id="48425-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="48425-135">建立[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帳戶。</span><span class="sxs-lookup"><span data-stu-id="48425-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="48425-136">**安裝其他套件或加入服務參考**</span><span class="sxs-lookup"><span data-stu-id="48425-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="48425-137">Twilio</span><span class="sxs-lookup"><span data-stu-id="48425-137">Twilio:</span></span>  
   <span data-ttu-id="48425-138">在 [套件管理器主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="48425-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="48425-139">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="48425-139">ASPSMS:</span></span>  
   <span data-ttu-id="48425-140">必須加入下列服務參考：</span><span class="sxs-lookup"><span data-stu-id="48425-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="48425-141">位址:</span><span class="sxs-lookup"><span data-stu-id="48425-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="48425-142">命名空間：</span><span class="sxs-lookup"><span data-stu-id="48425-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="48425-143">**找出 SMS 提供者使用者認證**</span><span class="sxs-lookup"><span data-stu-id="48425-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="48425-144">Twilio</span><span class="sxs-lookup"><span data-stu-id="48425-144">Twilio:</span></span>  
   <span data-ttu-id="48425-145">從 Twilio 帳戶的 [**儀表板**] 索引標籤中，複製 [**帳戶 SID** ] 和 [**驗證權杖**]。</span><span class="sxs-lookup"><span data-stu-id="48425-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="48425-146">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="48425-146">ASPSMS:</span></span>  
   <span data-ttu-id="48425-147">從您的帳戶設定中，流覽至**Userkey** ，並將它與您的自我定義**密碼**一起複製。</span><span class="sxs-lookup"><span data-stu-id="48425-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="48425-148">稍後我們會將這些值儲存在變數 `SMSAccountIdentification` 和 `SMSAccountPassword` 中。</span><span class="sxs-lookup"><span data-stu-id="48425-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="48425-149">**指定 SenderID/發信者**</span><span class="sxs-lookup"><span data-stu-id="48425-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="48425-150">Twilio</span><span class="sxs-lookup"><span data-stu-id="48425-150">Twilio:</span></span>  
   <span data-ttu-id="48425-151">在 [**數位**] 索引標籤中，複製您的 Twilio 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="48425-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="48425-152">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="48425-152">ASPSMS:</span></span>  
   <span data-ttu-id="48425-153">在 [**解除鎖定**擁有者] 功能表中，解除鎖定一或多個始發者，或選擇英數位元（並非所有網路都支援）。</span><span class="sxs-lookup"><span data-stu-id="48425-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="48425-154">稍後我們會將此值儲存在 `SMSAccountFrom` 變數中。</span><span class="sxs-lookup"><span data-stu-id="48425-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="48425-155">**將 SMS 提供者認證傳送至應用程式**</span><span class="sxs-lookup"><span data-stu-id="48425-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="48425-156">將認證和寄件者電話號碼提供給應用程式：</span><span class="sxs-lookup"><span data-stu-id="48425-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="48425-157">安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="48425-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="48425-158">帳戶和認證會加入上述程式碼中，讓範例保持簡單。</span><span class="sxs-lookup"><span data-stu-id="48425-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="48425-159">請參閱 Jon Atten 的[ASP.NET MVC：將私用設定保留在原始檔控制之外](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。</span><span class="sxs-lookup"><span data-stu-id="48425-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="48425-160">**將資料傳輸到 SMS 提供者的執行**</span><span class="sxs-lookup"><span data-stu-id="48425-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="48425-161">在*應用程式\_Start\IdentityConfig.cs*檔案中設定 `SmsService` 類別。</span><span class="sxs-lookup"><span data-stu-id="48425-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="48425-162">視使用的 SMS 提供者而定，啟動**Twilio**或**ASPSMS**區段：</span><span class="sxs-lookup"><span data-stu-id="48425-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="48425-163">執行應用程式，並使用您先前註冊的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="48425-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="48425-164">按一下您的使用者識別碼，這會在 `Manage` 控制器中啟用 `Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="48425-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="48425-165">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="48425-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="48425-166">幾秒內，您就會收到包含驗證碼的文字訊息。</span><span class="sxs-lookup"><span data-stu-id="48425-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="48425-167">輸入該檔案並按下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="48425-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="48425-168">[管理] 視圖會顯示您的電話號碼已加入。</span><span class="sxs-lookup"><span data-stu-id="48425-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="48425-169">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="48425-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="48425-170">`Manage` 控制器中的 `Index` 動作方法會根據您先前的動作來設定狀態訊息，並提供連結來變更您的本機密碼或新增本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="48425-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="48425-171">`Index` 方法也會顯示此瀏覽器的狀態或您的2FA 電話號碼、外部登入、2FA 啟用和記住2FA 方法（稍後會說明）。</span><span class="sxs-lookup"><span data-stu-id="48425-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="48425-172">在標題列中按一下您的使用者識別碼（電子郵件）並不會傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="48425-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="48425-173">按一下**電話號碼：移除**連結傳遞 `Message=RemovePhoneSuccess` 作為查詢字串。</span><span class="sxs-lookup"><span data-stu-id="48425-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="48425-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="48425-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="48425-175">`AddPhoneNumber` 動作方法會顯示一個對話方塊，以輸入可接收 SMS 訊息的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="48425-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="48425-176">按一下 [**傳送驗證碼**] 按鈕，就會將電話號碼張貼到 HTTP POST `AddPhoneNumber` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="48425-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="48425-177">`GenerateChangePhoneNumberTokenAsync` 方法會產生將在 SMS 訊息中設定的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="48425-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="48425-178">如果已設定 SMS 服務，權杖會以字串的形式傳送 &quot;您的安全性驗證碼會 &lt;權杖&gt;&quot;。</span><span class="sxs-lookup"><span data-stu-id="48425-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="48425-179">`SmsService.SendAsync` 的方法會以非同步方式呼叫，然後應用程式會重新導向至 `VerifyPhoneNumber` 動作方法（顯示下列對話方塊），您可以在其中輸入驗證碼。</span><span class="sxs-lookup"><span data-stu-id="48425-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="48425-180">當您輸入程式碼並按一下 [提交] 之後，程式碼就會張貼到 HTTP POST `VerifyPhoneNumber` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="48425-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="48425-181">`ChangePhoneNumberAsync` 方法會檢查已張貼的安全性驗證碼。</span><span class="sxs-lookup"><span data-stu-id="48425-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="48425-182">如果程式碼正確，則會將電話號碼加入 `AspNetUsers` 資料表的 [`PhoneNumber`] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="48425-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="48425-183">如果該呼叫成功，就會呼叫 `SignInAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="48425-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="48425-184">`isPersistent` 參數會設定驗證會話是否跨多個要求保存。</span><span class="sxs-lookup"><span data-stu-id="48425-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="48425-185">當您變更安全性設定檔時，系統會產生新的安全性戳記，並將其儲存在*AspNetUsers*資料表的 [`SecurityStamp`] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="48425-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="48425-186">請注意，[`SecurityStamp`] 欄位與安全性 cookie 不同。</span><span class="sxs-lookup"><span data-stu-id="48425-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="48425-187">安全性 cookie 不會儲存在 `AspNetUsers` 資料表中（或身分識別 DB 中的任何其他位置）。</span><span class="sxs-lookup"><span data-stu-id="48425-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="48425-188">安全性 cookie 權杖是使用[DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)自我簽署的，並且是使用 `UserId, SecurityStamp` 和到期時間資訊所建立。</span><span class="sxs-lookup"><span data-stu-id="48425-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="48425-189">Cookie 中介軟體會檢查每個要求上的 cookie。</span><span class="sxs-lookup"><span data-stu-id="48425-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="48425-190">`Startup` 類別中的 `SecurityStampValidator` 方法會叫用資料庫，並定期檢查安全性戳記（如 `validateInterval`所指定）。</span><span class="sxs-lookup"><span data-stu-id="48425-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="48425-191">這只會每隔30分鐘發生一次（在我們的範例中），除非您變更您的安全性設定檔。</span><span class="sxs-lookup"><span data-stu-id="48425-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="48425-192">選擇30分鐘的間隔，以最小化資料庫的行程。</span><span class="sxs-lookup"><span data-stu-id="48425-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="48425-193">對安全性設定檔進行任何變更時，必須呼叫 `SignInAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="48425-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="48425-194">當安全性設定檔變更時，資料庫會更新 `SecurityStamp` 欄位，而不會呼叫 `SignInAsync` 方法，您*只*會保持登入狀態，直到下一次 OWIN 管線叫用資料庫（`validateInterval`）為止。</span><span class="sxs-lookup"><span data-stu-id="48425-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="48425-195">您可以藉由將 `SignInAsync` 方法變更為立即傳回，然後將 cookie `validateInterval` 屬性從30分鐘設為5秒來進行測試：</span><span class="sxs-lookup"><span data-stu-id="48425-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="48425-196">當上述程式碼變更時，您可以變更安全性設定檔（例如，藉由變更**兩個因素**的狀態），而當 `SecurityStampValidator.OnValidateIdentity` 方法失敗時，您將會在5秒內登出。</span><span class="sxs-lookup"><span data-stu-id="48425-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="48425-197">移除 `SignInAsync` 方法中的傳回行，讓另一個安全性設定檔變更，而您將不會登出。`SignInAsync` 方法會產生新的安全性 cookie。</span><span class="sxs-lookup"><span data-stu-id="48425-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="48425-198">啟用雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="48425-198">Enable two-factor authentication</span></span>

<span data-ttu-id="48425-199">在範例應用程式中，您必須使用 UI 來啟用雙因素驗證（2FA）。</span><span class="sxs-lookup"><span data-stu-id="48425-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="48425-200">若要啟用2FA，請按一下巡覽列中的 [使用者識別碼] （電子郵件別名）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="48425-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="48425-201">按一下 [啟用 2FA]。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="48425-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="48425-202">登出後再重新登入。</span><span class="sxs-lookup"><span data-stu-id="48425-202">Log out, then log back in.</span></span> <span data-ttu-id="48425-203">如果您已啟用電子郵件（請參閱[前一個教學](account-confirmation-and-password-recovery-with-aspnet-identity.md)課程），您可以選取要2FA 的 SMS 或電子郵件。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="48425-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="48425-204">此時會顯示 [驗證代碼] 頁面，您可以在其中輸入程式碼（來自 SMS 或電子郵件）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="48425-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="48425-205">按一下 [**記住此瀏覽器**] 核取方塊，就不需要使用2FA 來登入該電腦和瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="48425-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="48425-206">啟用2FA 並按一下 [**記住此瀏覽器**]，可讓您從惡意使用者嘗試存取您的帳戶時，提供強式2FA 保護，前提是他們無法存取您的電腦。</span><span class="sxs-lookup"><span data-stu-id="48425-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="48425-207">您可以在您經常使用的任何私人電腦上執行此動作。</span><span class="sxs-lookup"><span data-stu-id="48425-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="48425-208">藉由設定 [**記住此瀏覽器**]，您就能從不常使用的電腦獲得2FA 的安全性，並讓您不必在自己的電腦上進行2FA。</span><span class="sxs-lookup"><span data-stu-id="48425-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="48425-209">如何註冊雙因素驗證提供者</span><span class="sxs-lookup"><span data-stu-id="48425-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="48425-210">當您建立新的 MVC 專案時， *IdentityConfig.cs*檔案會包含下列程式碼來註冊雙因素驗證提供者：</span><span class="sxs-lookup"><span data-stu-id="48425-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="48425-211">新增2FA 的電話號碼</span><span class="sxs-lookup"><span data-stu-id="48425-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="48425-212">`Manage` 控制器中的 `AddPhoneNumber` 動作方法會產生安全性權杖，並將它傳送至您所提供的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="48425-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="48425-213">傳送權杖之後，它會重新導向至 `VerifyPhoneNumber` 動作方法，您可以在其中輸入程式碼以註冊2FA 的 SMS。</span><span class="sxs-lookup"><span data-stu-id="48425-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="48425-214">在您驗證電話號碼之前，不會使用 SMS 2FA。</span><span class="sxs-lookup"><span data-stu-id="48425-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="48425-215">啟用2FA</span><span class="sxs-lookup"><span data-stu-id="48425-215">Enabling 2FA</span></span>

<span data-ttu-id="48425-216">`EnableTFA` 動作方法會啟用2FA：</span><span class="sxs-lookup"><span data-stu-id="48425-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="48425-217">請注意，必須呼叫 `SignInAsync`，因為 [啟用 2FA] 是安全性設定檔的變更。</span><span class="sxs-lookup"><span data-stu-id="48425-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="48425-218">啟用2FA 時，使用者必須使用2FA 來登入，並使用他們已註冊的2FA 方法（範例中的 SMS 和電子郵件）。</span><span class="sxs-lookup"><span data-stu-id="48425-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="48425-219">您可以新增更多2FA 提供者（例如 QR 代碼產生器），或您可以自行撰寫（請參閱搭配[ASP.NET Identity 使用 Google 驗證](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)器）。</span><span class="sxs-lookup"><span data-stu-id="48425-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="48425-220">2FA 碼是使用以時間為基礎的單次[密碼演算法](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)所產生，而代碼則有效6分鐘。</span><span class="sxs-lookup"><span data-stu-id="48425-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="48425-221">如果您需要6分鐘以上的時間來輸入程式碼，將會收到不正確代碼錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="48425-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="48425-222">合併社交和本機登入帳戶</span><span class="sxs-lookup"><span data-stu-id="48425-222">Combine social and local login accounts</span></span>

<span data-ttu-id="48425-223">您可以按一下電子郵件連結，以合併本機和社交帳戶。</span><span class="sxs-lookup"><span data-stu-id="48425-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="48425-224">在下列順序中 &quot;RickAndMSFT@gmail.com&quot; 會先建立為本機登入，但您可以先將帳戶建立為社交記錄，然後再新增本機登入。</span><span class="sxs-lookup"><span data-stu-id="48425-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="48425-225">按一下 [**管理**] 連結。</span><span class="sxs-lookup"><span data-stu-id="48425-225">Click on the **Manage** link.</span></span> <span data-ttu-id="48425-226">請注意與此帳戶相關聯的0外部（社交登入）。</span><span class="sxs-lookup"><span data-stu-id="48425-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="48425-227">按一下另一個登入服務的連結，並接受應用程式要求。</span><span class="sxs-lookup"><span data-stu-id="48425-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="48425-228">已合併這兩個帳戶，您將能夠使用任一帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="48425-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="48425-229">您可能想要讓使用者新增本機帳戶，以防其社交記錄在驗證服務已關閉，或更有可能失去其社交帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="48425-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="48425-230">在下圖中，Tom 是社交記錄（您可以從頁面上顯示的 [**外部登入： 1** ] 看到）。</span><span class="sxs-lookup"><span data-stu-id="48425-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="48425-231">按一下 [**挑選密碼**] 可讓您新增與相同帳戶相關聯的本機登入。</span><span class="sxs-lookup"><span data-stu-id="48425-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="48425-232">從暴力密碼破解攻擊的帳戶鎖定</span><span class="sxs-lookup"><span data-stu-id="48425-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="48425-233">您可以藉由啟用使用者鎖定，來保護應用程式上的帳戶免于字典攻擊。</span><span class="sxs-lookup"><span data-stu-id="48425-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="48425-234">`ApplicationUserManager Create` 方法中的下列程式碼會設定 lock out：</span><span class="sxs-lookup"><span data-stu-id="48425-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="48425-235">上述程式碼只會啟用雙因素驗證的鎖定。</span><span class="sxs-lookup"><span data-stu-id="48425-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="48425-236">雖然您可以藉由在帳戶控制器的 `Login` 方法中將 `shouldLockout` 變更為 true 來啟用登入鎖定，但建議您不要針對登入啟用鎖定，因為它會讓帳戶容易遭受[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)登入攻擊。</span><span class="sxs-lookup"><span data-stu-id="48425-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="48425-237">在範例程式碼中，已停用在 `ApplicationDbInitializer Seed` 方法中建立之系統管理員帳戶的鎖定：</span><span class="sxs-lookup"><span data-stu-id="48425-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="48425-238">要求使用者必須有已驗證的電子郵件帳戶</span><span class="sxs-lookup"><span data-stu-id="48425-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="48425-239">下列程式碼會要求使用者必須先有已驗證的電子郵件帳戶，才能登入：</span><span class="sxs-lookup"><span data-stu-id="48425-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="48425-240">使用檢查2FA 需求的方式</span><span class="sxs-lookup"><span data-stu-id="48425-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="48425-241">本機登入和社交記錄都會檢查是否已啟用2FA。</span><span class="sxs-lookup"><span data-stu-id="48425-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="48425-242">如果已啟用2FA，`SignInManager` 登入方法會傳回 `SignInStatus.RequiresVerification`，而使用者將會被重新導向至 `SendCode` 動作方法，讓他們必須輸入程式碼才能依序完成記錄。</span><span class="sxs-lookup"><span data-stu-id="48425-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="48425-243">如果使用者的本機 cookie 設定了 RememberMe，則 `SignInManager` 會傳回 `SignInStatus.Success`，而不需要經過2FA。</span><span class="sxs-lookup"><span data-stu-id="48425-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="48425-244">下列程式碼顯示 `SendCode` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="48425-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="48425-245">建立[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)時，會為使用者啟用所有的2FA 方法。</span><span class="sxs-lookup"><span data-stu-id="48425-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="48425-246">[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)會傳遞至[html.dropdownlistfor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper，讓使用者選取2FA 方法（通常是電子郵件和 SMS）。</span><span class="sxs-lookup"><span data-stu-id="48425-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="48425-247">一旦使用者張貼2FA 方法，就會呼叫 `HTTP POST SendCode` 動作方法，`SignInManager` 傳送2FA 程式碼，然後將使用者重新導向至 `VerifyCode` 動作方法，他們可以在其中輸入程式碼以完成登入。</span><span class="sxs-lookup"><span data-stu-id="48425-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="48425-248">2FA 鎖定</span><span class="sxs-lookup"><span data-stu-id="48425-248">2FA Lockout</span></span>

<span data-ttu-id="48425-249">雖然您可以在登入密碼嘗試失敗時設定帳戶鎖定，但該方法會讓您的登入容易受到[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)鎖定的影響。</span><span class="sxs-lookup"><span data-stu-id="48425-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="48425-250">我們建議您只使用2FA 的帳戶鎖定。</span><span class="sxs-lookup"><span data-stu-id="48425-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="48425-251">建立 `ApplicationUserManager` 時，範例程式碼會將2FA 鎖定和 `MaxFailedAccessAttemptsBeforeLockout` 設定為五個。</span><span class="sxs-lookup"><span data-stu-id="48425-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="48425-252">一旦使用者登入（透過本機帳戶或社交帳戶），就會儲存2FA 上的每個失敗嘗試，並在達到最大嘗試次數時，將使用者鎖定五分鐘（您可以使用 `DefaultAccountLockoutTimeSpan`設定鎖定時間）。</span><span class="sxs-lookup"><span data-stu-id="48425-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="48425-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="48425-253">Additional Resources</span></span>

- <span data-ttu-id="48425-254">[ASP.NET Identity 建議的資源](../getting-started/aspnet-identity-recommended-resources.md)完整的身分識別 blog、影片、教學課程，以及絕佳的連結清單。</span><span class="sxs-lookup"><span data-stu-id="48425-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="48425-255">[使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)也會顯示如何將設定檔資訊新增至使用者資料表。</span><span class="sxs-lookup"><span data-stu-id="48425-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="48425-256">[ASP.NET MVC 和 Identity 2.0：瞭解 John Atten 的基本概念](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)。</span><span class="sxs-lookup"><span data-stu-id="48425-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="48425-257">使用 ASP.NET Identity 進行帳戶確認和密碼復原</span><span class="sxs-lookup"><span data-stu-id="48425-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="48425-258">ASP.NET Identity 簡介</span><span class="sxs-lookup"><span data-stu-id="48425-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="48425-259">[宣佈 2.0.0 By Pranav 請參閱 rastogi ASP.NET Identity 的 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="48425-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="48425-260">[ASP.NET Identity 2.0：設定帳戶驗證和](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)由 John Atten 的雙因素授權。</span><span class="sxs-lookup"><span data-stu-id="48425-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
