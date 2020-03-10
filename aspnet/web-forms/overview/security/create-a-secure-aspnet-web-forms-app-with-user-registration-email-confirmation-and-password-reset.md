---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: 建立具有使用者註冊、電子郵件確認和密碼重設（C#）的安全 ASP.NET Web Forms 應用程式 |Microsoft Docs
author: Erikre
description: 本教學課程示範如何使用 ASP.NET Identity 的成員，建立具有使用者註冊、電子郵件確認和密碼重設的 ASP.NET Web Forms 應用程式 。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: af3653bc164810126bc3bf8f1b1794d75642d807
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78625150"
---
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a><span data-ttu-id="15ae9-103">以使用者註冊、電子郵件確認和密碼重設建立安全的 ASP.NET Web Forms 應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="15ae9-103">Create a secure ASP.NET Web Forms app with user registration, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="15ae9-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="15ae9-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="15ae9-105">本教學課程說明如何使用 ASP.NET Identity 成員資格系統，建立具有使用者註冊、電子郵件確認和密碼重設的 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="15ae9-105">This tutorial shows you how to build an ASP.NET Web Forms app with user registration, email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="15ae9-106">本教學課程是以 Rick Anderson 的[MVC 教學](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)課程為基礎。</span><span class="sxs-lookup"><span data-stu-id="15ae9-106">This tutorial was based on Rick Anderson's [MVC tutorial](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="15ae9-107">簡介</span><span class="sxs-lookup"><span data-stu-id="15ae9-107">Introduction</span></span>

<span data-ttu-id="15ae9-108">本教學課程會引導您完成使用 Visual Studio 和 ASP.NET 4.5 建立 ASP.NET Web Forms 應用程式所需的步驟，以建立具有使用者註冊、電子郵件確認和密碼重設的安全 Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="15ae9-108">This tutorial guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio and ASP.NET 4.5 to create a secure Web Forms app with user registration, email confirmation and password reset.</span></span>

### <a name="tutorial-tasks-and-information"></a><span data-ttu-id="15ae9-109">教學課程工作和資訊：</span><span class="sxs-lookup"><span data-stu-id="15ae9-109">Tutorial Tasks and Information:</span></span>

- [<span data-ttu-id="15ae9-110">建立 ASP.NET Web Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="15ae9-110">Create an ASP.NET Web Forms app</span></span>](#createWebForms)
- [<span data-ttu-id="15ae9-111">連結 SendGrid</span><span class="sxs-lookup"><span data-stu-id="15ae9-111">Hook Up SendGrid</span></span>](#SG)
- [<span data-ttu-id="15ae9-112">在登入之前需要電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="15ae9-112">Require Email Confirmation Before Log In</span></span>](#require)
- [<span data-ttu-id="15ae9-113">密碼修復和重設</span><span class="sxs-lookup"><span data-stu-id="15ae9-113">Password Recovery and Reset</span></span>](#reset)
- [<span data-ttu-id="15ae9-114">重新傳送電子郵件確認連結</span><span class="sxs-lookup"><span data-stu-id="15ae9-114">Resend Email Confirmation Link</span></span>](#rsend)
- [<span data-ttu-id="15ae9-115">針對應用程式進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="15ae9-115">Troubleshooting the App</span></span>](#dbg)
- [<span data-ttu-id="15ae9-116">其他資源</span><span class="sxs-lookup"><span data-stu-id="15ae9-116">Additional Resources</span></span>](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a><span data-ttu-id="15ae9-117">建立 ASP.NET Web Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="15ae9-117">Create an ASP.NET Web Forms App</span></span>

<span data-ttu-id="15ae9-118">一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。</span><span class="sxs-lookup"><span data-stu-id="15ae9-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="15ae9-119">請一併安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本。</span><span class="sxs-lookup"><span data-stu-id="15ae9-119">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher as well.</span></span>

> [!NOTE]
> <span data-ttu-id="15ae9-120">警告：您必須安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="15ae9-120">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="15ae9-121">建立新**專案（檔案** -&gt;**新專案**），然後從 [**新增專案**] 對話方塊中選取 [ **ASP.NET Web 應用程式**] 範本和 [最新的 .NET Framework 版本]。</span><span class="sxs-lookup"><span data-stu-id="15ae9-121">Create a new project (**File** -&gt; **New Project**) and select the **ASP.NET Web Application** template and the latest .NET Framework version from the **New Project** dialog box.</span></span>
2. <span data-ttu-id="15ae9-122">從 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **Web** form] 範本。</span><span class="sxs-lookup"><span data-stu-id="15ae9-122">From the **New ASP.NET Project** dialog box, select the **Web Forms** template.</span></span> <span data-ttu-id="15ae9-123">將預設驗證保留為**個別使用者帳戶**。</span><span class="sxs-lookup"><span data-stu-id="15ae9-123">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="15ae9-124">如果您想要在 Azure 中裝載應用程式，請將 [**主機保留在雲端中**] 核取方塊保持核取狀態。</span><span class="sxs-lookup"><span data-stu-id="15ae9-124">If you'd like to host the app in Azure, leave the **Host in the cloud** check box checked.</span></span>   
 <span data-ttu-id="15ae9-125">然後，按一下 **[確定]** 以建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="15ae9-125">Then, click **OK** to create the new project.</span></span>  
    <span data-ttu-id="15ae9-126">![[New ASP.NET Project] 對話方塊](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="15ae9-126">![New ASP.NET Project dialog box](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span></span>
3. <span data-ttu-id="15ae9-127">啟用專案的安全通訊端層（SSL）。</span><span class="sxs-lookup"><span data-stu-id="15ae9-127">Enable Secure Sockets Layer (SSL) for the project.</span></span> <span data-ttu-id="15ae9-128">請遵循[使用 Web Forms 的消費者入門教學課程系列](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)中，為**專案啟用 SSL**一節中提供的步驟。</span><span class="sxs-lookup"><span data-stu-id="15ae9-128">Follow the steps available in the **Enable SSL for the Project** section of the [Getting Started with Web Forms tutorial series](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).</span></span>
4. <span data-ttu-id="15ae9-129">執行應用程式，按一下 [**註冊**] 連結並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="15ae9-129">Run the app, click the **Register** link and register a new user.</span></span> <span data-ttu-id="15ae9-130">此時，電子郵件上的唯一驗證是以[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)屬性為基礎，以確保電子郵件地址的格式正確。</span><span class="sxs-lookup"><span data-stu-id="15ae9-130">At this point, the only validation on the email is based on the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute to ensure the email address is well-formed.</span></span> <span data-ttu-id="15ae9-131">您將修改程式碼以新增電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="15ae9-131">You will modify the code to add email confirmation.</span></span> <span data-ttu-id="15ae9-132">關閉瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="15ae9-132">Close the browser window.</span></span>
5. <span data-ttu-id="15ae9-133">在 Visual Studio 的**伺服器總管**（**View** -&gt;**伺服器總管**）中，流覽至 [**資料 Connections\DefaultConnection\Tables\AspNetUsers**]，以滑鼠右鍵按一下，然後選取 [**開啟資料表定義**]。</span><span class="sxs-lookup"><span data-stu-id="15ae9-133">In **Server Explorer** of Visual Studio (**View** -&gt; **Server Explorer**), navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span> 

    <span data-ttu-id="15ae9-134">下圖顯示 `AspNetUsers` 資料表架構：</span><span class="sxs-lookup"><span data-stu-id="15ae9-134">The following image shows the `AspNetUsers` table schema:</span></span>

    ![AspNetUsers 資料表架構](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="15ae9-136">在**伺服器總管**中，以滑鼠右鍵按一下**AspNetUsers**資料表，然後選取 [**顯示資料表資料**]。</span><span class="sxs-lookup"><span data-stu-id="15ae9-136">In **Server Explorer**, right-click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
  
    ![AspNetUsers 資料表資料](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="15ae9-138">此時，尚未確認已註冊使用者的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15ae9-138">At this point the email for the registered user has not been confirmed.</span></span>
7. <span data-ttu-id="15ae9-139">按一下資料列，然後選取 [刪除] 以刪除使用者。</span><span class="sxs-lookup"><span data-stu-id="15ae9-139">Click on the row and select delete to delete the user.</span></span> <span data-ttu-id="15ae9-140">您會在下一個步驟中再次新增這封電子郵件，並將確認訊息傳送至電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="15ae9-140">You'll add this email again in the next step and send a confirmation message to the email address.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="15ae9-141">電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="15ae9-141">Email Confirmation</span></span>

<span data-ttu-id="15ae9-142">最佳做法是在註冊新使用者時確認電子郵件，以確認他們不會模擬其他人（也就是他們尚未向其他人的電子郵件註冊）。</span><span class="sxs-lookup"><span data-stu-id="15ae9-142">It's a best practice to confirm the email during the registration of a new user to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="15ae9-143">假設您有一個討論論壇，您會想要防止 `"bob@cpandl.com"` 註冊為 `"joe@contoso.com"`。</span><span class="sxs-lookup"><span data-stu-id="15ae9-143">Suppose you had a discussion forum, you would want to prevent `"bob@cpandl.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="15ae9-144">若未確認電子郵件，`"joe@contoso.com"` 可能會從您的應用程式收到不必要的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15ae9-144">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="15ae9-145">假設 Bob 不小心註冊為 `"bib@cpandl.com"` 且未注意到，他將無法使用密碼復原，因為應用程式沒有正確的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15ae9-145">Suppose Bob accidentally registered as `"bib@cpandl.com"` and hadn't noticed it, he wouldn't be able to use password recovery because the app doesn't have his correct email.</span></span> <span data-ttu-id="15ae9-146">電子郵件確認只提供 bot 的有限保護，並不會提供保護來防止被判定的垃圾郵件。</span><span class="sxs-lookup"><span data-stu-id="15ae9-146">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers.</span></span>

<span data-ttu-id="15ae9-147">您通常會想要防止新使用者將任何資料張貼到您的網站，然後再由電子郵件、SMS 文字訊息或其他機制確認。</span><span class="sxs-lookup"><span data-stu-id="15ae9-147">You generally want to prevent new users from posting any data to your website before they have been confirmed by either email, an SMS text message or another mechanism.</span></span> <span data-ttu-id="15ae9-148">在下列各節中，我們將啟用電子郵件確認並修改程式碼，以防止新註冊的使用者登入，直到他們的電子郵件確認為止。</span><span class="sxs-lookup"><span data-stu-id="15ae9-148">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span> <span data-ttu-id="15ae9-149">您將在本教學課程中使用電子郵件服務 SendGrid。</span><span class="sxs-lookup"><span data-stu-id="15ae9-149">You'll use the email service SendGrid in this tutorial.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="15ae9-150">連結 SendGrid</span><span class="sxs-lookup"><span data-stu-id="15ae9-150">Hook up SendGrid</span></span>

<span data-ttu-id="15ae9-151">SendGrid 已變更其 API，因為已撰寫此教學課程。</span><span class="sxs-lookup"><span data-stu-id="15ae9-151">SendGrid has changed it's API since this tutorial was written.</span></span> <span data-ttu-id="15ae9-152">如需目前的 SendGrid 指示，請參閱[SendGrid](http://sendgrid.com/)或[啟用帳戶確認和密碼](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery)復原。</span><span class="sxs-lookup"><span data-stu-id="15ae9-152">For current SendGrid instructions, see [SendGrid](http://sendgrid.com/) or [Enable account confirmation and password recovery](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery).</span></span>

<span data-ttu-id="15ae9-153">雖然本教學課程僅示範如何透過[SendGrid](http://sendgrid.com/)新增電子郵件通知，但您可以使用 SMTP 和其他機制來傳送電子郵件（請參閱[其他資源](#addRes)）。</span><span class="sxs-lookup"><span data-stu-id="15ae9-153">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="15ae9-154">在 Visual Studio 中，開啟 **套件管理員主控台** （**工具**  - &gt;  **NuGet 套件**管理員 -&gt; **Package Manager Console**），然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="15ae9-154">In Visual Studio, open the **Package Manager Console** (**Tools** -&gt; **NuGet Package Manger** -&gt; **Package Manager Console**), and enter the following command:</span></span>  
    `Install-Package SendGrid`
2. <span data-ttu-id="15ae9-155">移至[Azure SendGrid 註冊頁面](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)，並註冊免費的 SendGrid 帳戶。</span><span class="sxs-lookup"><span data-stu-id="15ae9-155">Go to the [Azure SendGrid sign-up page](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) and register for free SendGrid account.</span></span> <span data-ttu-id="15ae9-156">您也可以直接在[SendGrid 的網站](http://www.sendgrid.com)上註冊免費的 SendGrid 帳戶。</span><span class="sxs-lookup"><span data-stu-id="15ae9-156">You can also sign-up for a free SendGrid account directly on [SendGrid's site](http://www.sendgrid.com).</span></span>
3. <span data-ttu-id="15ae9-157">從**方案總管**開啟*應用程式\_[啟動*] 資料夾中的*IdentityConfig.cs*檔案，並將下列以黃色反白顯示的程式碼新增至 `EmailService` 類別以設定**SendGrid**：</span><span class="sxs-lookup"><span data-stu-id="15ae9-157">From **Solution Explorer** open the *IdentityConfig.cs* file in the *App\_Start* folder and add the following code highlighted in yellow to the `EmailService` class to configure **SendGrid**:</span></span>

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. <span data-ttu-id="15ae9-158">此外，將下列 `using` 語句加入至*IdentityConfig.cs*檔案的開頭：</span><span class="sxs-lookup"><span data-stu-id="15ae9-158">Also, add the following `using` statements to the beginning of the *IdentityConfig.cs* file:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. <span data-ttu-id="15ae9-159">為了讓此範例保持簡單，您會將電子郵件服務帳戶值儲存*在 web.config 檔案*的 `appSettings` 區段中。</span><span class="sxs-lookup"><span data-stu-id="15ae9-159">To keep this sample simple, you'll store the email service account values in the `appSettings` section of the *web.config* file.</span></span> <span data-ttu-id="15ae9-160">將下列以黃色反白顯示的 XML 加入至專案*根目錄的 web.config*檔案中：</span><span class="sxs-lookup"><span data-stu-id="15ae9-160">Add the following XML highlighted in yellow to the *web.config* file at the root of your project:</span></span>

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > <span data-ttu-id="15ae9-161">安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="15ae9-161">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="15ae9-162">在此範例中，帳戶和認證會儲存在*web.config*檔案的**appSetting**區段中。</span><span class="sxs-lookup"><span data-stu-id="15ae9-162">In this example, the account and credentials are stored in the **appSetting** section of the *Web.config* file.</span></span> <span data-ttu-id="15ae9-163">在 Azure 上，您可以將這些值安全地儲存在 Azure 入口網站的 [ **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="15ae9-163">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="15ae9-164">如需相關資訊，請參閱 Rick Anderson 的主題[：將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳作法](https://go.microsoft.com/fwlink/?LinkId=513141)。</span><span class="sxs-lookup"><span data-stu-id="15ae9-164">For related information see Rick Anderson's topic titled [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](https://go.microsoft.com/fwlink/?LinkId=513141).</span></span>
6. <span data-ttu-id="15ae9-165">新增電子郵件服務值以反映您的 SendGrid authentication 值（使用者名稱和密碼），以便您可以從您的應用程式成功傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15ae9-165">Add the email service values to reflect your SendGrid authentication values (User Name and Password) so that you can successful send email from your app.</span></span> <span data-ttu-id="15ae9-166">請務必使用您的 SendGrid 帳戶名稱，而不是您所提供的電子郵件地址 SendGrid。</span><span class="sxs-lookup"><span data-stu-id="15ae9-166">Be sure to use your SendGrid account name rather than the email address you provided SendGrid.</span></span>

### <a name="enable-email-confirmation"></a><span data-ttu-id="15ae9-167">啟用電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="15ae9-167">Enable Email Confirmation</span></span>

 <span data-ttu-id="15ae9-168">若要啟用電子郵件確認，您將使用下列步驟來修改註冊程式碼。</span><span class="sxs-lookup"><span data-stu-id="15ae9-168">To enable email confirmation, you'll modify the registration code using the following steps.</span></span>  

1. <span data-ttu-id="15ae9-169">在 [*帳戶*] 資料夾中，開啟*Register.aspx.cs*程式碼後置，並更新 `CreateUser_Click` 方法以啟用下列反白顯示的變更：</span><span class="sxs-lookup"><span data-stu-id="15ae9-169">In the *Account* folder, open the *Register.aspx.cs* code-behind and update the `CreateUser_Click` method to enable the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. <span data-ttu-id="15ae9-170">在**方案總管**中，以滑鼠右鍵按一下*default.aspx* ，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="15ae9-170">In **Solution Explorer**, right-click *Default.aspx* and select **Set As Start Page**.</span></span>
3. <span data-ttu-id="15ae9-171">按 F5 執行應用程式 **。**</span><span class="sxs-lookup"><span data-stu-id="15ae9-171">Run the app by pressing **F5.**</span></span> <span data-ttu-id="15ae9-172">顯示頁面之後，按一下 [**註冊**] 連結以顯示 [註冊] 頁面。</span><span class="sxs-lookup"><span data-stu-id="15ae9-172">After the page is displayed, click the **Register** link to display the Register page.</span></span>
4. <span data-ttu-id="15ae9-173">輸入您的電子郵件和密碼，然後按一下 [**註冊**] 按鈕，透過 SendGrid 傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="15ae9-173">Enter your email and password, then click the **Register** button to send an email message via SendGrid.</span></span>  
   <span data-ttu-id="15ae9-174">專案和程式碼的目前狀態可讓使用者在完成註冊表單之後登入，即使他們尚未確認其帳戶也一樣。</span><span class="sxs-lookup"><span data-stu-id="15ae9-174">The current state of your project and code will allow the user to log in once they complete the registration form, even though they haven't confirmed their account.</span></span>
5. <span data-ttu-id="15ae9-175">檢查您的電子郵件帳戶，然後按一下連結以確認您的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15ae9-175">Check your email account and click on the link to confirm your email.</span></span>  
   <span data-ttu-id="15ae9-176">提交註冊表單之後，您將會登入。</span><span class="sxs-lookup"><span data-stu-id="15ae9-176">Once you submit the registration form, you will be logged in.</span></span>  
    ![範例網站-已登入](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="15ae9-178">在登入之前需要電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="15ae9-178">Require Email Confirmation Before Log In</span></span>

<span data-ttu-id="15ae9-179">雖然您已確認電子郵件帳戶，但此時您不需要按一下驗證電子郵件中包含的連結，即可完整登入。</span><span class="sxs-lookup"><span data-stu-id="15ae9-179">Although you have confirmed the email account, at this point you would not need to click on the link contained in the verification email to be fully signed-in.</span></span> <span data-ttu-id="15ae9-180">在下一節中，您將修改程式碼，要求新的使用者在登入（驗證）之前，必須先有已確認的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="15ae9-180">In the following section, you will modify the code requiring new users to have a confirmed email before they are logged in (authenticated).</span></span>

1. <span data-ttu-id="15ae9-181">在 Visual Studio 的**方案總管**中，以下列醒目提示的變更，更新包含在 [*帳戶*] 資料夾中的*Register.aspx.cs*程式碼後置中的 `CreateUser_Click` 事件：</span><span class="sxs-lookup"><span data-stu-id="15ae9-181">In **Solution Explorer** of Visual Studio, update the `CreateUser_Click` event in the *Register.aspx.cs* code-behind contained in the *Accounts* folder with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. <span data-ttu-id="15ae9-182">在*Login.aspx.cs*程式碼後置中，使用下列反白顯示的變更來更新 `LogIn` 方法：</span><span class="sxs-lookup"><span data-stu-id="15ae9-182">Update the `LogIn` method in the *Login.aspx.cs* code-behind with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a><span data-ttu-id="15ae9-183">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="15ae9-183">Run the Application</span></span>

 <span data-ttu-id="15ae9-184">現在您已完成程式碼來檢查是否已確認使用者的電子郵件地址，您可以同時檢查**註冊**和**登**入頁面上的功能。</span><span class="sxs-lookup"><span data-stu-id="15ae9-184">Now that you have implemented the code to check whether a user's email address has been confirmed, you can check the functionality on both the **Register** and **Login** pages.</span></span> 

1. <span data-ttu-id="15ae9-185">刪除**AspNetUsers**資料表中的任何帳戶，其中包含您想要測試的電子郵件別名。</span><span class="sxs-lookup"><span data-stu-id="15ae9-185">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
2. <span data-ttu-id="15ae9-186">執行應用程式（**F5**），並確認您在確認您的電子郵件地址之前，無法註冊為使用者。</span><span class="sxs-lookup"><span data-stu-id="15ae9-186">Run the app (**F5**) and verify you cannot register as a user until you have confirmed your email address.</span></span>
3. <span data-ttu-id="15ae9-187">在透過剛傳送的電子郵件確認新帳戶之前，請嘗試以新帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="15ae9-187">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
 <span data-ttu-id="15ae9-188">您會看到您無法登入，而且必須有已確認的電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="15ae9-188">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span>
4. <span data-ttu-id="15ae9-189">確認您的電子郵件地址之後，請登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="15ae9-189">Once you confirm your email address, log in to the app.</span></span>

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a><span data-ttu-id="15ae9-190">密碼修復和重設</span><span class="sxs-lookup"><span data-stu-id="15ae9-190">Password Recovery and Reset</span></span>

1. <span data-ttu-id="15ae9-191">在 Visual Studio 中，從包含在*帳戶*資料夾的*Forgot.aspx.cs*程式碼後置中，移除 `Forgot` 方法中的批註字元，讓方法顯示如下：</span><span class="sxs-lookup"><span data-stu-id="15ae9-191">In Visual Studio, remove the comment characters from the `Forgot` method in the *Forgot.aspx.cs* code-behind contained in the *Account* folder, so that the method appears as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. <span data-ttu-id="15ae9-192">開啟 [*登入 .aspx* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="15ae9-192">Open the *Login.aspx* page.</span></span> <span data-ttu-id="15ae9-193">取代**loginForm**區段結尾附近的標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="15ae9-193">Replace the markup near the end of the **loginForm** section as highlighted below:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. <span data-ttu-id="15ae9-194">開啟*Login.aspx.cs*程式碼後置，並取消批註 `Page_Load` 事件處理常式中以黃色醒目提示的下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="15ae9-194">Open the *Login.aspx.cs* code-behind and uncomment the following line of code highlighted in yellow from the `Page_Load` event handler:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. <span data-ttu-id="15ae9-195">按 F5 執行應用程式 **。**</span><span class="sxs-lookup"><span data-stu-id="15ae9-195">Run the app by pressing **F5.**</span></span> <span data-ttu-id="15ae9-196">顯示頁面之後，按一下 [**登入**] 連結。</span><span class="sxs-lookup"><span data-stu-id="15ae9-196">After the page is displayed, click the **Log in** link.</span></span>
5. <span data-ttu-id="15ae9-197">按一下 [**忘記密碼？** ] 連結，以顯示 [**忘記密碼**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="15ae9-197">Click the **Forgot your password?** link to display the **Forgot Password** page.</span></span>
6. <span data-ttu-id="15ae9-198">輸入您的電子郵件地址，然後按一下 [**提交**] 按鈕，將電子郵件傳送至您的位址，以讓您重設密碼。</span><span class="sxs-lookup"><span data-stu-id="15ae9-198">Enter your email address and click the **Submit** button to send an email to your address which will allow you to reset your password.</span></span>   
   <span data-ttu-id="15ae9-199">檢查您的電子郵件帳戶，然後按一下連結以顯示 [**重設密碼**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="15ae9-199">Check your email account and click on the link to display the **Reset Password** page.</span></span>
7. <span data-ttu-id="15ae9-200">在 [**重設密碼**] 頁面上，輸入您的電子郵件、密碼和確認的密碼。</span><span class="sxs-lookup"><span data-stu-id="15ae9-200">On the **Reset Password** page, enter your email, password, and confirmed password.</span></span> <span data-ttu-id="15ae9-201">然後，按下 [**重設**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ae9-201">Then, press the **Reset** button.</span></span>  
   <span data-ttu-id="15ae9-202">當您成功重設密碼時，將會顯示 [**變更密碼**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="15ae9-202">When you successfully reset your password, the **Password Changed** page will be displayed.</span></span> <span data-ttu-id="15ae9-203">現在您可以使用新密碼登入。</span><span class="sxs-lookup"><span data-stu-id="15ae9-203">Now you can log in with your new password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="15ae9-204">重新傳送電子郵件確認連結</span><span class="sxs-lookup"><span data-stu-id="15ae9-204">Resend Email Confirmation Link</span></span>

<span data-ttu-id="15ae9-205">一旦使用者建立新的本機帳戶，他們就會收到電子郵件，要求他們在登入之前必須先使用確認連結。</span><span class="sxs-lookup"><span data-stu-id="15ae9-205">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="15ae9-206">如果使用者不小心刪除了確認電子郵件，或電子郵件從未送達，他們就需要再次傳送確認連結。</span><span class="sxs-lookup"><span data-stu-id="15ae9-206">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="15ae9-207">下列程式碼變更顯示如何啟用此動作。</span><span class="sxs-lookup"><span data-stu-id="15ae9-207">The following code changes show how to enable this.</span></span>

1. <span data-ttu-id="15ae9-208">在 Visual Studio 中，開啟**Login.aspx.cs**程式碼後置，並在 `LogIn` 事件處理常式之後加入下列事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="15ae9-208">In Visual Studio, open the **Login.aspx.cs** code-behind and add the following event handler after the `LogIn` event handler:</span></span>   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. <span data-ttu-id="15ae9-209">藉由變更黃色反白顯示的程式碼，在*Login.aspx.cs*程式碼後置中修改 `LogIn` 事件處理常式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="15ae9-209">Modify the `LogIn` event handler in the *Login.aspx.cs* code-behind by changing the code highlighted in yellow as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. <span data-ttu-id="15ae9-210">新增以黃色反白顯示的程式碼，以更新*登入 .aspx*頁面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="15ae9-210">Update the *Login.aspx* page by adding the code highlighted in yellow as follows:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. <span data-ttu-id="15ae9-211">刪除**AspNetUsers**資料表中的任何帳戶，其中包含您想要測試的電子郵件別名。</span><span class="sxs-lookup"><span data-stu-id="15ae9-211">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
5. <span data-ttu-id="15ae9-212">執行應用程式（**F5**）並註冊您的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="15ae9-212">Run the app (**F5**) and register your email address.</span></span>
6. <span data-ttu-id="15ae9-213">在透過剛傳送的電子郵件確認新帳戶之前，請嘗試以新帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="15ae9-213">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
   <span data-ttu-id="15ae9-214">您會看到您無法登入，而且必須有已確認的電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="15ae9-214">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span> <span data-ttu-id="15ae9-215">此外，您現在可以重新傳送確認訊息到您的電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="15ae9-215">In addition, you can now resend a confirmation message to your email account.</span></span>
7. <span data-ttu-id="15ae9-216">輸入您的電子郵件地址和密碼，然後按下 [**重新傳送確認**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ae9-216">Enter your email address and password, then press the **Resend confirmation** button.</span></span>
8. <span data-ttu-id="15ae9-217">一旦您根據新傳送的電子郵件訊息確認您的電子郵件地址，請登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="15ae9-217">Once you confirm your email address based on the newly sent email message, log in to the app.</span></span>

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a><span data-ttu-id="15ae9-218">針對應用程式進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="15ae9-218">Troubleshooting the App</span></span>

<span data-ttu-id="15ae9-219">如果您未收到電子郵件，其中包含驗證認證的連結：</span><span class="sxs-lookup"><span data-stu-id="15ae9-219">If you don't receive an email containing the link to verify your credentials:</span></span>

- <span data-ttu-id="15ae9-220">檢查您的垃圾郵件資料夾。</span><span class="sxs-lookup"><span data-stu-id="15ae9-220">Check your junk or spam folder.</span></span>
- <span data-ttu-id="15ae9-221">登入您的 SendGrid 帳戶，然後按一下 [[電子郵件活動] 連結](https://sendgrid.com/logs/index)。</span><span class="sxs-lookup"><span data-stu-id="15ae9-221">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>
- <span data-ttu-id="15ae9-222">請確定您使用的是 SendGrid 使用者帳戶名稱作為*web.config*值，而不是您的 SendGrid 帳戶電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="15ae9-222">Be certain you used your SendGrid user account name as a *Web.config* value rather than your SendGrid account email address.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="15ae9-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="15ae9-223">Additional Resources</span></span>

- [<span data-ttu-id="15ae9-224">ASP.NET Identity 建議資源的連結</span><span class="sxs-lookup"><span data-stu-id="15ae9-224">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [<span data-ttu-id="15ae9-225">使用 ASP.NET Identity 進行帳戶確認和密碼復原</span><span class="sxs-lookup"><span data-stu-id="15ae9-225">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="15ae9-226">ASP.NET Web Forms 教學課程系列-新增 OAuth 2.0 提供者</span><span class="sxs-lookup"><span data-stu-id="15ae9-226">ASP.NET Web Forms tutorial series - Add an OAuth 2.0 Provider</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [<span data-ttu-id="15ae9-227">將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="15ae9-227">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [<span data-ttu-id="15ae9-228">ASP.NET Web Forms 教學課程系列-為專案啟用 SSL</span><span class="sxs-lookup"><span data-stu-id="15ae9-228">ASP.NET Web Forms tutorial series - Enable SSL for the Project</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
