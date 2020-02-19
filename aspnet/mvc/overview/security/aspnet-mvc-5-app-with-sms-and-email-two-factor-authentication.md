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
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>使用 SMS 和電子郵件雙因素驗證的 ASP.NET MVC 5 應用程式

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程說明如何使用雙因素驗證來建立 ASP.NET MVC 5 web 應用程式。 在繼續之前，您應該先完成[使用登入、電子郵件確認和密碼重設建立安全的 ASP.NET MVC 5 web 應用程式](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。 您可以在[這裡](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)下載已完成的應用程式。 此下載包含可讓您在不設定電子郵件或 SMS 提供者的情況下，測試電子郵件確認和 SMS 的偵錯工具協助程式。
> 
> 本教學課程是由[Rick Anderson](https://blogs.msdn.com/rickAndy) （Twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ）撰寫。

- [建立 ASP.NET MVC 應用程式](#createMvc)
- [設定 SMS 以進行雙因素驗證](#SMS)
- [啟用雙因素驗證](#enable2)
- [其他資源](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>建立 ASP.NET MVC 應用程式

一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。 安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本。

> [!NOTE]
> 警告：您應該先完成[使用登入、電子郵件確認和密碼重設來建立安全的 ASP.NET MVC 5 web 應用程式，](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)再繼續進行。 您必須安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本，才能完成本教學課程。

1. 建立新的 ASP.NET Web 專案，並選取 [MVC] 範本。 Web form 也支援 ASP.NET Identity，因此您可以在 web Forms 應用程式中遵循類似的步驟。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. 將預設驗證保留為**個別使用者帳戶**。 如果您想要在 Azure 中裝載應用程式，請將此核取方塊保留為已核取狀態。 稍後在本教學課程中，我們將部署至 Azure。 您可以[免費開啟 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
3. 將[專案設定為使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a>設定 SMS 以進行雙因素驗證

本教學課程提供使用 Twilio 或 ASPSMS 的指示，但是您可以使用任何其他 SMS 提供者。

1. **使用 SMS 提供者建立使用者帳戶**  
  
   建立[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帳戶。
2. **安裝其他套件或加入服務參考**  
  
   Twilio  
   在 [套件管理器主控台] 中，輸入下列命令：  
    `Install-Package Twilio`  
  
   ASPSMS:  
   必須加入下列服務參考：  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   位址：  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   命名空間：  
    `ASPSMSX2`
3. **找出 SMS 提供者使用者認證**  
  
   Twilio  
   從 Twilio 帳戶的 [**儀表板**] 索引標籤中，複製 [**帳戶 SID** ] 和 [**驗證權杖**]。  
  
   ASPSMS:  
   從您的帳戶設定中，流覽至**Userkey** ，並將它與您的自我定義**密碼**一起複製。  
  
   稍後我們會將這些值儲存在*web.config 檔案*的 `"SMSAccountIdentification"` 和 `"SMSAccountPassword"` 中。
4. **指定 SenderID/發信者**  
  
   Twilio  
   在 [**數位**] 索引標籤中，複製您的 Twilio 電話號碼。  
  
   ASPSMS:  
   在 [**解除鎖定**擁有者] 功能表中，解除鎖定一或多個始發者，或選擇英數位元（並非所有網路都支援）。  
  
   稍後我們會將此值儲存在 `"SMSAccountFrom"` 金鑰*的 web.config 檔案*中。
5. **將 SMS 提供者認證傳送至應用程式**  
  
   將認證和寄件者電話號碼提供給應用程式。 為了簡單起見，我們會將這些值儲存在*web.config 檔案*中。 當我們部署到 Azure 時，我們可以將這些值安全地儲存在 [網站設定] 索引標籤上的 [**應用程式設定**] 區段中。 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > 安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。 帳戶和認證會加入上述程式碼中，讓範例保持簡單。 請參閱[將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
6. **將資料傳輸到 SMS 提供者的執行**  
  
   在*應用程式\_Start\IdentityConfig.cs*檔案中設定 `SmsService` 類別。  
  
   視使用的 SMS 提供者而定，啟動**Twilio**或**ASPSMS**區段： 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. 更新*Views\Manage\Index.cshtml* Razor view：（注意：不要直接移除程式碼中的批註，請使用下列程式碼）。  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. 確認 `ManageController` 中的 `EnableTwoFactorAuthentication` 和 `DisableTwoFactorAuthentication` 動作方法具有[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)屬性：  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. 執行應用程式，並使用您先前註冊的帳戶登入。
10. 按一下您的使用者識別碼，這會在 `Manage` 控制器中啟用 `Index` 動作方法。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. 按一下 [加入]。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber` 動作方法會顯示一個對話方塊，以輸入可接收 SMS 訊息的電話號碼。

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. 幾秒內，您就會收到包含驗證碼的文字訊息。 輸入該檔案並按下 [**提交**]。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. [管理] 視圖會顯示您的電話號碼已加入。

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>啟用雙因素驗證

在範本產生的應用程式中，您必須使用 UI 來啟用雙因素驗證（2FA）。 若要啟用2FA，請按一下巡覽列中的 [使用者識別碼] （電子郵件別名）。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

按一下 [啟用 2FA]。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

登出，然後重新登入。 如果您已啟用電子郵件（請參閱[前一個教學](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)課程），您可以選取要2FA 的 SMS 或電子郵件。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

此時會顯示 [驗證代碼] 頁面，您可以在其中輸入程式碼（來自 SMS 或電子郵件）。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

按一下 [**記住此瀏覽器**] 核取方塊，可讓您在使用瀏覽器和已核取該方塊的裝置時，不需要使用2FA 來登入。 只要惡意使用者無法存取您的裝置，啟用2FA 並按一下 [**記住此瀏覽器**]，就能提供您便利的單一步驟密碼存取，同時仍保有對不受信任裝置之所有存取的強式2FA 保護。 您可以在您經常使用的任何私人裝置上執行此動作。

本教學課程提供在新 ASP.NET MVC 應用程式上啟用2FA 的快速簡介。 我的教學課程[使用 SMS 的雙因素驗證和含有 ASP.NET Identity 的電子郵件](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)，會詳細說明範例背後的程式碼。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他資源

- [使用 SMS 的雙因素驗證與 ASP.NET Identity 的電子郵件](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)詳細說明雙因素驗證
- [ASP.NET Identity 建議資源的連結](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [使用 ASP.NET Identity 進行帳戶確認和密碼](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)復原深入瞭解密碼修復和帳戶確認。
- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教學課程說明如何使用 Facebook 和 Google OAuth 2 授權撰寫 ASP.NET MVC 5 應用程式。 它也會示範如何將其他資料新增至身分識別資料庫。
- [將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署至 Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教學課程會新增 Azure 部署、如何以角色保護您的應用程式、如何使用成員資格 API 來新增使用者和角色，以及其他安全性功能。
- [建立適用于 OAuth 2 的 Google 應用程式，並將應用程式連接到專案](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [在 Facebook 中建立應用程式，並將應用程式連接到專案](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [在專案中設定 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [如何設定您C#的和 ASP.NET MVC 開發環境](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
