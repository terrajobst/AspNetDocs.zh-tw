---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: 使用 SMS 和電子郵件雙因素驗證 ASP.NET MVC 5 應用程式 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程說明如何使用雙因素驗證來建立 ASP.NET MVC 5 web 應用程式。 您應該完成使用來建立安全的 ASP.NET MVC 5 web 應用程式 。
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457592"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="88b5a-104">使用 SMS 和電子郵件雙因素驗證的 ASP.NET MVC 5 應用程式</span><span class="sxs-lookup"><span data-stu-id="88b5a-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>

<span data-ttu-id="88b5a-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="88b5a-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="88b5a-106">本教學課程說明如何使用雙因素驗證來建立 ASP.NET MVC 5 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88b5a-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="88b5a-107">在繼續之前，您應該先完成[使用登入、電子郵件確認和密碼重設建立安全的 ASP.NET MVC 5 web 應用程式](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。</span><span class="sxs-lookup"><span data-stu-id="88b5a-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="88b5a-108">您可以在[這裡](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)下載已完成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="88b5a-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="88b5a-109">此下載包含可讓您在不設定電子郵件或 SMS 提供者的情況下，測試電子郵件確認和 SMS 的偵錯工具協助程式。</span><span class="sxs-lookup"><span data-stu-id="88b5a-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="88b5a-110">本教學課程是由[Rick Anderson](https://blogs.msdn.com/rickAndy) （Twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ）撰寫。</span><span class="sxs-lookup"><span data-stu-id="88b5a-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

- [<span data-ttu-id="88b5a-111">建立 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="88b5a-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="88b5a-112">設定 SMS 以進行雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="88b5a-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="88b5a-113">啟用雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="88b5a-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="88b5a-114">其他資源</span><span class="sxs-lookup"><span data-stu-id="88b5a-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="88b5a-115">建立 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="88b5a-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="88b5a-116">一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。</span><span class="sxs-lookup"><span data-stu-id="88b5a-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="88b5a-117">安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本。</span><span class="sxs-lookup"><span data-stu-id="88b5a-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="88b5a-118">警告：您應該先完成[使用登入、電子郵件確認和密碼重設來建立安全的 ASP.NET MVC 5 web 應用程式，](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="88b5a-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="88b5a-119">您必須安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="88b5a-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="88b5a-120">建立新的 ASP.NET Web 專案，並選取 [MVC] 範本。</span><span class="sxs-lookup"><span data-stu-id="88b5a-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="88b5a-121">Web form 也支援 ASP.NET Identity，因此您可以在 web Forms 應用程式中遵循類似的步驟。</span><span class="sxs-lookup"><span data-stu-id="88b5a-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="88b5a-122">將預設驗證保留為**個別使用者帳戶**。</span><span class="sxs-lookup"><span data-stu-id="88b5a-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="88b5a-123">如果您想要在 Azure 中裝載應用程式，請將此核取方塊保留為已核取狀態。</span><span class="sxs-lookup"><span data-stu-id="88b5a-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="88b5a-124">稍後在本教學課程中，我們將部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="88b5a-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="88b5a-125">您可以[免費開啟 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="88b5a-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="88b5a-126">將[專案設定為使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="88b5a-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="88b5a-127">設定 SMS 以進行雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="88b5a-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="88b5a-128">本教學課程提供使用 Twilio 或 ASPSMS 的指示，但是您可以使用任何其他 SMS 提供者。</span><span class="sxs-lookup"><span data-stu-id="88b5a-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="88b5a-129">**使用 SMS 提供者建立使用者帳戶**</span><span class="sxs-lookup"><span data-stu-id="88b5a-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="88b5a-130">建立[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帳戶。</span><span class="sxs-lookup"><span data-stu-id="88b5a-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="88b5a-131">**安裝其他套件或加入服務參考**</span><span class="sxs-lookup"><span data-stu-id="88b5a-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="88b5a-132">Twilio</span><span class="sxs-lookup"><span data-stu-id="88b5a-132">Twilio:</span></span>  
   <span data-ttu-id="88b5a-133">在 [套件管理器主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="88b5a-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="88b5a-134">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="88b5a-134">ASPSMS:</span></span>  
   <span data-ttu-id="88b5a-135">必須加入下列服務參考：</span><span class="sxs-lookup"><span data-stu-id="88b5a-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="88b5a-136">位址：</span><span class="sxs-lookup"><span data-stu-id="88b5a-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="88b5a-137">命名空間：</span><span class="sxs-lookup"><span data-stu-id="88b5a-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="88b5a-138">**找出 SMS 提供者使用者認證**</span><span class="sxs-lookup"><span data-stu-id="88b5a-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="88b5a-139">Twilio</span><span class="sxs-lookup"><span data-stu-id="88b5a-139">Twilio:</span></span>  
   <span data-ttu-id="88b5a-140">從 Twilio 帳戶的 [**儀表板**] 索引標籤中，複製 [**帳戶 SID** ] 和 [**驗證權杖**]。</span><span class="sxs-lookup"><span data-stu-id="88b5a-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="88b5a-141">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="88b5a-141">ASPSMS:</span></span>  
   <span data-ttu-id="88b5a-142">從您的帳戶設定中，流覽至**Userkey** ，並將它與您的自我定義**密碼**一起複製。</span><span class="sxs-lookup"><span data-stu-id="88b5a-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="88b5a-143">稍後我們會將這些值儲存在*web.config 檔案*的 `"SMSAccountIdentification"` 和 `"SMSAccountPassword"` 中。</span><span class="sxs-lookup"><span data-stu-id="88b5a-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="88b5a-144">**指定 SenderID/發信者**</span><span class="sxs-lookup"><span data-stu-id="88b5a-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="88b5a-145">Twilio</span><span class="sxs-lookup"><span data-stu-id="88b5a-145">Twilio:</span></span>  
   <span data-ttu-id="88b5a-146">在 [**數位**] 索引標籤中，複製您的 Twilio 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="88b5a-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="88b5a-147">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="88b5a-147">ASPSMS:</span></span>  
   <span data-ttu-id="88b5a-148">在 [**解除鎖定**擁有者] 功能表中，解除鎖定一或多個始發者，或選擇英數位元（並非所有網路都支援）。</span><span class="sxs-lookup"><span data-stu-id="88b5a-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="88b5a-149">稍後我們會將此值儲存在 `"SMSAccountFrom"` 金鑰*的 web.config 檔案*中。</span><span class="sxs-lookup"><span data-stu-id="88b5a-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="88b5a-150">**將 SMS 提供者認證傳送至應用程式**</span><span class="sxs-lookup"><span data-stu-id="88b5a-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="88b5a-151">將認證和寄件者電話號碼提供給應用程式。</span><span class="sxs-lookup"><span data-stu-id="88b5a-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="88b5a-152">為了簡單起見，我們會將這些值儲存在*web.config 檔案*中。</span><span class="sxs-lookup"><span data-stu-id="88b5a-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="88b5a-153">當我們部署到 Azure 時，我們可以將這些值安全地儲存在 [網站設定] 索引標籤上的 [**應用程式設定**] 區段中。</span><span class="sxs-lookup"><span data-stu-id="88b5a-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="88b5a-154">安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="88b5a-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="88b5a-155">帳戶和認證會加入上述程式碼中，讓範例保持簡單。</span><span class="sxs-lookup"><span data-stu-id="88b5a-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="88b5a-156">請參閱[將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="88b5a-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="88b5a-157">**將資料傳輸到 SMS 提供者的執行**</span><span class="sxs-lookup"><span data-stu-id="88b5a-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="88b5a-158">在*應用程式\_Start\IdentityConfig.cs*檔案中設定 `SmsService` 類別。</span><span class="sxs-lookup"><span data-stu-id="88b5a-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="88b5a-159">視使用的 SMS 提供者而定，啟動**Twilio**或**ASPSMS**區段：</span><span class="sxs-lookup"><span data-stu-id="88b5a-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="88b5a-160">更新*Views\Manage\Index.cshtml* Razor view：（注意：不要直接移除程式碼中的批註，請使用下列程式碼）。</span><span class="sxs-lookup"><span data-stu-id="88b5a-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="88b5a-161">確認 `ManageController` 中的 `EnableTwoFactorAuthentication` 和 `DisableTwoFactorAuthentication` 動作方法具有[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)屬性：</span><span class="sxs-lookup"><span data-stu-id="88b5a-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="88b5a-162">執行應用程式，並使用您先前註冊的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="88b5a-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="88b5a-163">按一下您的使用者識別碼，這會在 `Manage` 控制器中啟用 `Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="88b5a-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="88b5a-164">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="88b5a-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="88b5a-165">`AddPhoneNumber` 動作方法會顯示一個對話方塊，以輸入可接收 SMS 訊息的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="88b5a-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="88b5a-166">幾秒內，您就會收到包含驗證碼的文字訊息。</span><span class="sxs-lookup"><span data-stu-id="88b5a-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="88b5a-167">輸入該檔案並按下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="88b5a-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="88b5a-168">[管理] 視圖會顯示您的電話號碼已加入。</span><span class="sxs-lookup"><span data-stu-id="88b5a-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="88b5a-169">啟用雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="88b5a-169">Enable two-factor authentication</span></span>

<span data-ttu-id="88b5a-170">在範本產生的應用程式中，您必須使用 UI 來啟用雙因素驗證（2FA）。</span><span class="sxs-lookup"><span data-stu-id="88b5a-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="88b5a-171">若要啟用2FA，請按一下巡覽列中的 [使用者識別碼] （電子郵件別名）。</span><span class="sxs-lookup"><span data-stu-id="88b5a-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="88b5a-172">按一下 [啟用 2FA]。</span><span class="sxs-lookup"><span data-stu-id="88b5a-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="88b5a-173">登出，然後重新登入。</span><span class="sxs-lookup"><span data-stu-id="88b5a-173">Logout, then log back in.</span></span> <span data-ttu-id="88b5a-174">如果您已啟用電子郵件（請參閱[前一個教學](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)課程），您可以選取要2FA 的 SMS 或電子郵件。</span><span class="sxs-lookup"><span data-stu-id="88b5a-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="88b5a-175">此時會顯示 [驗證代碼] 頁面，您可以在其中輸入程式碼（來自 SMS 或電子郵件）。</span><span class="sxs-lookup"><span data-stu-id="88b5a-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="88b5a-176">按一下 [**記住此瀏覽器**] 核取方塊，可讓您在使用瀏覽器和已核取該方塊的裝置時，不需要使用2FA 來登入。</span><span class="sxs-lookup"><span data-stu-id="88b5a-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="88b5a-177">只要惡意使用者無法存取您的裝置，啟用2FA 並按一下 [**記住此瀏覽器**]，就能提供您便利的單一步驟密碼存取，同時仍保有對不受信任裝置之所有存取的強式2FA 保護。</span><span class="sxs-lookup"><span data-stu-id="88b5a-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="88b5a-178">您可以在您經常使用的任何私人裝置上執行此動作。</span><span class="sxs-lookup"><span data-stu-id="88b5a-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="88b5a-179">本教學課程提供在新 ASP.NET MVC 應用程式上啟用2FA 的快速簡介。</span><span class="sxs-lookup"><span data-stu-id="88b5a-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="88b5a-180">我的教學課程[使用 SMS 的雙因素驗證和含有 ASP.NET Identity 的電子郵件](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)，會詳細說明範例背後的程式碼。</span><span class="sxs-lookup"><span data-stu-id="88b5a-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="88b5a-181">其他資源</span><span class="sxs-lookup"><span data-stu-id="88b5a-181">Additional Resources</span></span>

- <span data-ttu-id="88b5a-182">[使用 SMS 的雙因素驗證與 ASP.NET Identity 的電子郵件](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)詳細說明雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="88b5a-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="88b5a-183">ASP.NET Identity 建議資源的連結</span><span class="sxs-lookup"><span data-stu-id="88b5a-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="88b5a-184">[使用 ASP.NET Identity 進行帳戶確認和密碼](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)復原深入瞭解密碼修復和帳戶確認。</span><span class="sxs-lookup"><span data-stu-id="88b5a-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="88b5a-185">[使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教學課程說明如何使用 Facebook 和 Google OAuth 2 授權撰寫 ASP.NET MVC 5 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88b5a-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="88b5a-186">它也會示範如何將其他資料新增至身分識別資料庫。</span><span class="sxs-lookup"><span data-stu-id="88b5a-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="88b5a-187">[將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署至 Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="88b5a-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="88b5a-188">本教學課程會新增 Azure 部署、如何以角色保護您的應用程式、如何使用成員資格 API 來新增使用者和角色，以及其他安全性功能。</span><span class="sxs-lookup"><span data-stu-id="88b5a-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="88b5a-189">建立適用于 OAuth 2 的 Google 應用程式，並將應用程式連接到專案</span><span class="sxs-lookup"><span data-stu-id="88b5a-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="88b5a-190">在 Facebook 中建立應用程式，並將應用程式連接到專案</span><span class="sxs-lookup"><span data-stu-id="88b5a-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="88b5a-191">在專案中設定 SSL</span><span class="sxs-lookup"><span data-stu-id="88b5a-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [<span data-ttu-id="88b5a-192">如何設定您C#的和 ASP.NET MVC 開發環境</span><span class="sxs-lookup"><span data-stu-id="88b5a-192">How to set up your C# and ASP.NET MVC development environment</span></span>](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
