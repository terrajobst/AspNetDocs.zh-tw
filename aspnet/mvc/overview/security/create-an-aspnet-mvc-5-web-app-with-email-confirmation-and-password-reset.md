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
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>使用登入、電子郵件確認和密碼重設建立安全的 ASP.NET MVC 5 Web 應用程式 (C#)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

本教學課程會示範如何使用 ASP.NET Identity 成員資格系統，以電子郵件確認和密碼重設來建立 ASP.NET MVC 5 web 應用程式。

如需本教學課程中使用 .NET Core 的更新版本，請參閱[ASP.NET Core 中的帳戶確認和密碼](/aspnet/core/security/authentication/accconfirm)復原。

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>建立 ASP.NET MVC 應用程式

一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。 安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本。

> [!NOTE]
> 警告：您必須安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本，才能完成本教學課程。

1. 建立新的 ASP.NET Web 專案，並選取 [MVC] 範本。 Web form 也支援 ASP.NET Identity，因此您可以在 web Forms 應用程式中遵循類似的步驟。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. 將預設驗證保留為**個別使用者帳戶**。 如果您想要在 Azure 中裝載應用程式，請將此核取方塊保留為已核取狀態。 稍後在本教學課程中，我們將部署至 Azure。 您可以[免費開啟 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
3. 將[專案設定為使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. 執行應用程式，按一下 [**註冊**] 連結並註冊使用者。 此時，電子郵件上的唯一驗證是使用[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)屬性。
5. 在伺服器總管中，流覽至 [**資料 Connections\DefaultConnection\Tables\AspNetUsers**]，以滑鼠右鍵按一下，然後選取 [**開啟資料表定義**]。

    下圖顯示 `AspNetUsers` 架構：

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. 以滑鼠右鍵按一下 [ **AspNetUsers** ] 資料表，然後選取 [**顯示資料表資料**]。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 此時尚未確認電子郵件。
7. 按一下資料列，然後選取 [刪除]。 您會在下一個步驟中再次新增這封電子郵件，並傳送確認電子郵件。

## <a name="email-confirmation"></a>電子郵件確認

最佳做法是確認新使用者註冊的電子郵件，以確認他們不會模擬其他人（也就是他們尚未向他人的電子郵件註冊）。 假設您有一個討論論壇，您會想要防止 `"bob@example.com"` 註冊為 `"joe@contoso.com"`。 若未確認電子郵件，`"joe@contoso.com"` 可能會從您的應用程式收到不必要的電子郵件。 假設 Bob 不小心註冊為 `"bib@example.com"` 且未注意到，他將無法使用密碼復原，因為應用程式沒有正確的電子郵件。 電子郵件確認僅為 bot 提供有限的保護，並不會提供保護來防止被判定的垃圾郵件，他們有許多可使用的電子郵件別名來進行註冊。

您通常會想要防止新使用者將任何資料張貼到您的網站，然後再由電子郵件、SMS 文字訊息或其他機制確認。 <a id="build"></a>在下列各節中，我們將啟用電子郵件確認並修改程式碼，以防止新註冊的使用者登入，直到他們的電子郵件確認為止。

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>連結 SendGrid

本節中的指示不是最新的。 如需更新的指示，請參閱[設定 SendGrid 電子郵件提供者](/aspnet/core/security/authentication/accconfirm#configure-email-provider)。

雖然本教學課程僅示範如何透過[SendGrid](http://sendgrid.com/)新增電子郵件通知，但您可以使用 SMTP 和其他機制來傳送電子郵件（請參閱[其他資源](#addRes)）。

1. 在 [套件管理器主控台] 中，輸入下列命令： 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. 移至[Azure SendGrid 註冊頁面](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)，並註冊免費的 SendGrid 帳戶。 藉由在*App_Start/identityconfig.cs*中新增類似下列的程式碼來設定 SendGrid：

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

您必須新增下列內容：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

為了讓此範例保持簡單，我們會將應用程式設定儲存*在 web.config 檔案*中：

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> 安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。 帳戶和認證會儲存在 appSetting 中。 在 Azure 上，您可以將這些值安全地儲存在 Azure 入口網站的 [ **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] 索引標籤上。 請參閱[將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。

### <a name="enable-email-confirmation-in-the-account-controller"></a>在帳戶控制器中啟用電子郵件確認

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

確認*Views\Account\ConfirmEmail.cshtml*檔具有正確的 razor 語法。 （可能遺漏第一行中的 @ 字元。 )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

執行應用程式，然後按一下 [註冊] 連結。 提交註冊表單之後，您就會登入。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

檢查您的電子郵件帳戶，然後按一下連結以確認您的電子郵件。

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>在登入之前需要電子郵件確認

目前使用者完成註冊表單之後，就會登入。 在登入之前，您通常會想要先確認其電子郵件。 在下一節中，我們會修改程式碼，要求新的使用者在登入（驗證）之前，必須先有已確認的電子郵件。 使用下列反白顯示的變更來更新 `HttpPost Register` 方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

藉由將 `SignInAsync` 方法加上批註，註冊就不會登入使用者。 `TempData["ViewBagLink"] = callbackUrl;` 行可用於在不傳送電子郵件的情況下，對[應用程式](#dbg)和測試註冊進行錯用。 `ViewBag.Message` 可用來顯示確認指示。 [下載範例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)包含程式碼，可在不設定電子郵件的情況下測試電子郵件確認，而且也可以用來對應用程式進行 debug。

建立 `Views\Shared\Info.cshtml` 檔案，並新增下列 razor 標記：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

將 [[授權] 屬性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)加入至主控制器的 [`Contact` 動作] 方法。 您可以按一下 [**連絡人**] 連結，確認匿名使用者沒有存取權，且已驗證的使用者的確有存取權。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

您也必須更新 `HttpPost Login` 動作方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

更新 [ *Views\Shared\Error.cshtml* ] 視圖以顯示錯誤訊息：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

刪除**AspNetUsers**資料表中的任何帳戶，其中包含您想要測試的電子郵件別名。 執行應用程式並確認您無法登入，直到確認您的電子郵件地址為止。 確認您的電子郵件地址之後，請按一下 [**連絡人**] 連結。

<a id="reset"></a>
## <a name="password-recoveryreset"></a>密碼修復/重設

從帳戶控制器的 [`HttpPost ForgotPassword` 動作] 方法中移除批註字元：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

從*Views\Account\Login.cshtml* razor view 檔案中的 `ForgotPassword` [html.actionlink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx)移除批註字元：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

[登入] 頁面現在會顯示重設密碼的連結。

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>重新傳送電子郵件確認連結

一旦使用者建立新的本機帳戶，他們就會收到電子郵件，要求他們在登入之前必須先使用確認連結。 如果使用者不小心刪除了確認電子郵件，或電子郵件從未送達，他們就需要再次傳送確認連結。 下列程式碼變更顯示如何啟用此動作。

將下列 helper 方法新增至*Controllers\AccountController.cs*檔案的底部：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

更新 Register 方法以使用新的協助程式：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

如果尚未確認使用者帳戶，請更新登入方法以重新傳送密碼：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>合併社交和本機登入帳戶

您可以按一下電子郵件連結，以合併本機和社交帳戶。 在下列順序中 **RickAndMSFT@gmail.com** 會先建立為本機登入，但您可以先將帳戶建立為社交記錄，然後再新增本機登入。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

按一下 [**管理**] 連結。 請注意與此帳戶相關聯的外部登入 **： 0** 。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

按一下另一個登入服務的連結，並接受應用程式要求。 已合併這兩個帳戶，您將能夠使用任一帳戶登入。 您可能想要讓使用者新增本機帳戶，以防其社交記錄在驗證服務已關閉，或更有可能失去其社交帳戶的存取權。

在下圖中，Tom 是社交記錄（您可以從頁面上顯示的 [**外部登入： 1** ] 看到）。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

按一下 [**挑選密碼**] 可讓您新增與相同帳戶相關聯的本機登入。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>深入瞭解電子郵件確認

我的教學課程[帳戶確認和密碼復原與 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)會前往本主題中的詳細資料。

<a id="dbg"></a>
## <a name="debugging-the-app"></a>偵錯工具

如果您沒有收到包含連結的電子郵件：

- 檢查您的垃圾郵件資料夾。
- 登入您的 SendGrid 帳戶，然後按一下 [[電子郵件活動] 連結](https://sendgrid.com/logs/index)。

若要測試不含電子郵件的驗證連結，請下載[完整的範例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。 確認連結和確認碼將會顯示在頁面上。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他資源

- [ASP.NET Identity 建議資源的連結](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [使用 ASP.NET Identity 進行帳戶確認和密碼](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)復原深入瞭解密碼修復和帳戶確認。
- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教學課程說明如何使用 Facebook 和 Google OAuth 2 授權撰寫 ASP.NET MVC 5 應用程式。 它也會示範如何將其他資料新增至身分識別資料庫。
- [將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署至 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教學課程會新增 Azure 部署、如何以角色保護您的應用程式、如何使用成員資格 API 來新增使用者和角色，以及其他安全性功能。
- [建立適用于 OAuth 2 的 Google 應用程式，並將應用程式連接到專案](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [在 Facebook 中建立應用程式，並將應用程式連接到專案](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [在專案中設定 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
