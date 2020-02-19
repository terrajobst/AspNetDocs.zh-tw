---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: 使用 SMS 雙因素驗證（C#）建立 ASP.NET Web Forms 應用程式 |Microsoft Docs
author: Erikre
description: 本教學課程說明如何使用雙因素驗證來建立 ASP.NET Web Forms 應用程式。 本教學課程的設計目的是要補充標題為 [Cr ...] 的教學課程。
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c9558aca8a655071c0c94ed66433cf721f26c011
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77466422"
---
# <a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>使用 SMS 雙因素驗證建立 ASP.NET Web Forms 應用程式 (C#)

依[Erik Reitan](https://github.com/Erikre)

[下載 ASP.NET Web Forms 應用程式與電子郵件和 SMS 雙因素驗證](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> 本教學課程說明如何使用雙因素驗證來建立 ASP.NET Web Forms 應用程式。 本教學課程的設計目的是要補充標題為[使用使用者註冊、電子郵件確認和密碼重設來建立安全 ASP.NET Web Forms 應用程式](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)的教學課程。 此外，本教學課程是以 Rick Anderson 的[MVC 教學](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)課程為基礎。

## <a name="introduction"></a>簡介

本教學課程會引導您完成建立 ASP.NET Web Forms 應用程式所需的步驟，以使用 Visual Studio 來支援雙因素驗證。 雙因素驗證是額外的使用者驗證步驟。 此額外步驟會在登入期間產生唯一的個人識別碼（PIN）。 PIN 通常會以電子郵件或 SMS 訊息的形式傳送給使用者。 然後，應用程式的使用者會在登入時輸入 PIN 做為額外的驗證量值。

### <a name="tutorial-tasks-and-information"></a>教學課程工作和資訊：

- [建立 ASP.NET Web Forms 應用程式](#createWebForms)
- [設定 SMS 和雙因素驗證](#SMS)
- [為已註冊的使用者啟用雙因素驗證](#use2FA)
- [其他資源](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>建立 ASP.NET Web Forms 應用程式

一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。 請一併安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本。 此外，您還需要建立[Twilio](https://www.twilio.com/try-twilio)帳戶，如下所述。

> [!NOTE]
> 重要：您必須安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本，才能完成本教學課程。

1. 建立新專案（檔案 ** -&gt;** **新專案**），然後從 [**新增專案**] 對話方塊中選取 [ **ASP.NET Web 應用程式**] 範本以及 [.NET Framework 版本 4.5.2]。
2. 從 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **Web** form] 範本。 將預設驗證保留為**個別使用者帳戶**。 然後，按一下 **[確定]** 以建立新的專案。  
    ![[New ASP.NET Project] 對話方塊](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. 啟用專案的安全通訊端層（SSL）。 請遵循[使用 Web Forms 的消費者入門教學課程系列](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)中，為**專案啟用 SSL**一節中提供的步驟。
4. 在 Visual Studio 中，開啟 **套件管理員主控台** （**工具**  - &gt;  **NuGet 套件**管理員 -&gt; **Package Manager Console**），然後輸入下列命令：  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>設定 SMS 和雙因素驗證

本教學課程使用 Twilio，但是您可以使用任何 SMS 提供者。

1. 建立[Twilio](https://www.twilio.com/try-twilio)帳戶。
2. 從 Twilio 帳戶的 [**儀表板**] 索引標籤中，複製 [**帳戶 SID** ] 和 [**驗證權杖]。** 您稍後會將其新增至您的應用程式。
3. 在 [**數位**] 索引標籤上，也請複製您的 Twilio**電話號碼**。
4. 將 Twilio**帳戶 SID**、**驗證權杖**和**電話號碼**提供給應用程式。 為了簡單起見，您會將這些值儲存在*web.config 檔案*中。 當您部署至 Azure 時，可以安全地將這些值儲存在 [網站設定] 索引標籤上的 [ **appSettings** ] 區段中。此外，在新增電話號碼時，只會使用數位。   
   請注意，您也可以新增 SendGrid 認證。 SendGrid 是一種電子郵件通知服務。 如需如何啟用 SendGrid 的詳細資訊，請參閱標題為[使用使用者註冊、電子郵件確認和密碼重設建立安全 ASP.NET Web Forms 應用程式](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)的教學課程中的「掛上 SendGrid」一節。

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > 安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。 在此範例中，帳戶和認證會儲存在*web.config*檔案的**appSettings**區段中。 在 Azure 上，您可以將這些值安全地儲存在 Azure 入口網站的 [ **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] 索引標籤上。 如需相關資訊，請參閱 Rick Anderson 的主題[：將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳作法](/aspnet/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)。
5. 藉由以黃色反白顯示下列變更，在*應用程式\_Start\IdentityConfig.cs*檔案中設定 `SmsService` 類別： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. 將下列 `using` 語句加入至*IdentityConfig.cs*檔案的開頭： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. 藉由移除黃色反白顯示的程式碼，來更新*帳戶/管理 .aspx*檔案：  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. 在*Manage.aspx.cs*程式碼後置的 `Page_Load` 處理常式中，將以黃色反白顯示的程式程式碼取消批註，使其看起來如下所示： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. 在 [*帳戶*的程式碼後置]/*TwoFactorAuthenticationSignIn.aspx.cs*中，新增下列以黃色反白顯示的程式碼，以更新 `Page_Load` 處理常式： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   藉由進行上述程式碼變更，包含驗證選項的「提供者」 DropDownList 將不會重設為第一個值。 這可讓使用者在驗證時（而不只是第一個），成功選取要使用的所有選項。
10. 在**方案總管**中，以滑鼠右鍵按一下*default.aspx* ，然後選取 [**設定為起始頁**]。
11. 藉由測試您的應用程式，請先建立應用程式（**Ctrl**+**Shift**+**B**），然後執行應用程式（**F5**），然後選取 [**註冊**] 來建立新的使用者帳戶，或選取 [**登入**] （如果使用者帳戶已註冊）。
12. 當您（使用者）登入之後，請按一下導覽列中的 [使用者識別碼] （電子郵件地址），以顯示 [**管理帳戶**] 頁面（管理 .aspx）。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. 在 [**管理帳戶**] 頁面上，按一下 [**電話號碼**] 旁的 [**新增**]。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. 新增您（使用者）想要接收 SMS 訊息（文字訊息）的電話號碼，然後按一下 [**提交**] 按鈕。   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    此時，應用程式會*使用 web.config 中的認證來聯繫*Twilio。 SMS 訊息（文字訊息）將會傳送至與使用者帳戶相關聯的電話。 您可以藉由查看 Twilio 儀表板來確認 Twilio 訊息是否已傳送。
15. 在幾秒鐘內，與使用者帳戶相關聯的電話會收到包含驗證碼的文字訊息。 輸入驗證碼，然後按 [**提交**]。  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>為已註冊的使用者啟用雙因素驗證

此時，您已為您的應用程式啟用雙因素驗證。 使用者若要使用雙因素驗證，可以使用 UI 直接變更其設定。 

1. 身為您應用程式的使用者，您可以按一下巡覽列中的 [使用者識別碼] （電子郵件別名）來顯示 [**管理帳戶**] 頁面，為您的特定帳戶啟用雙因素驗證。然後，按一下 [**啟用**] 連結以啟用帳戶的雙因素驗證。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. 登出後再重新登入。 如果您已啟用電子郵件，則可以選取 [SMS] 或 [電子郵件] 進行雙因素驗證。 如果您尚未啟用電子郵件，請參閱標題為[使用使用者註冊、電子郵件確認和密碼重設建立安全 ASP.NET Web Forms 應用程式](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)的教學課程。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. [雙因素驗證] 頁面隨即顯示，您可以在其中輸入程式碼（來自 SMS 或電子郵件）。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 按一下 [**記住此瀏覽器**] 核取方塊，可讓您在使用瀏覽器和已核取該方塊的裝置時，不需要使用雙因素驗證來登入。 只要惡意使用者無法存取您的裝置、啟用雙因素驗證，然後按一下 [**記住此瀏覽器**]，就會提供您便利的單一步驟密碼存取，同時仍會針對來自不受信任裝置的所有存取保留強式雙因素驗證保護。 您可以在您經常使用的任何私人裝置上執行此動作。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他資源

- [使用 SMS 的雙因素驗證和使用 ASP.NET Identity 的電子郵件](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [ASP.NET Identity 建議資源的連結](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure 網站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms 教學課程系列-新增 OAuth 2.0 提供者](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [ASP.NET Web Forms 教學課程系列-為專案啟用 SSL](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [使用 ASP.NET Identity 進行帳戶確認和密碼復原](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [在 Facebook 中建立應用程式，並將應用程式連接到專案](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
