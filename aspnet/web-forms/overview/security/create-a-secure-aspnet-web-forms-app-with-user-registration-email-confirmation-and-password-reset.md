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
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a>以使用者註冊、電子郵件確認和密碼重設建立安全的 ASP.NET Web Forms 應用程式 (C#)

依[Erik Reitan](https://github.com/Erikre)

> 本教學課程說明如何使用 ASP.NET Identity 成員資格系統，建立具有使用者註冊、電子郵件確認和密碼重設的 ASP.NET Web Forms 應用程式。 本教學課程是以 Rick Anderson 的[MVC 教學](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)課程為基礎。

## <a name="introduction"></a>簡介

本教學課程會引導您完成使用 Visual Studio 和 ASP.NET 4.5 建立 ASP.NET Web Forms 應用程式所需的步驟，以建立具有使用者註冊、電子郵件確認和密碼重設的安全 Web Forms 應用程式。

### <a name="tutorial-tasks-and-information"></a>教學課程工作和資訊：

- [建立 ASP.NET Web Forms 應用程式](#createWebForms)
- [連結 SendGrid](#SG)
- [在登入之前需要電子郵件確認](#require)
- [密碼修復和重設](#reset)
- [重新傳送電子郵件確認連結](#rsend)
- [針對應用程式進行疑難排解](#dbg)
- [其他資源](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>建立 ASP.NET Web Forms 應用程式

一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。 請一併安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本。

> [!NOTE]
> 警告：您必須安裝[Visual Studio 2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390465)版本，才能完成本教學課程。

1. 建立新**專案（檔案** -&gt;**新專案**），然後從 [**新增專案**] 對話方塊中選取 [ **ASP.NET Web 應用程式**] 範本和 [最新的 .NET Framework 版本]。
2. 從 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **Web** form] 範本。 將預設驗證保留為**個別使用者帳戶**。 如果您想要在 Azure 中裝載應用程式，請將 [**主機保留在雲端中**] 核取方塊保持核取狀態。   
 然後，按一下 **[確定]** 以建立新的專案。  
    ![[New ASP.NET Project] 對話方塊](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)
3. 啟用專案的安全通訊端層（SSL）。 請遵循[使用 Web Forms 的消費者入門教學課程系列](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)中，為**專案啟用 SSL**一節中提供的步驟。
4. 執行應用程式，按一下 [**註冊**] 連結並註冊新的使用者。 此時，電子郵件上的唯一驗證是以[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)屬性為基礎，以確保電子郵件地址的格式正確。 您將修改程式碼以新增電子郵件確認。 關閉瀏覽器視窗。
5. 在 Visual Studio 的**伺服器總管**（**View** -&gt;**伺服器總管**）中，流覽至 [**資料 Connections\DefaultConnection\Tables\AspNetUsers**]，以滑鼠右鍵按一下，然後選取 [**開啟資料表定義**]。 

    下圖顯示 `AspNetUsers` 資料表架構：

    ![AspNetUsers 資料表架構](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. 在**伺服器總管**中，以滑鼠右鍵按一下**AspNetUsers**資料表，然後選取 [**顯示資料表資料**]。  
  
    ![AspNetUsers 資料表資料](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 此時，尚未確認已註冊使用者的電子郵件。
7. 按一下資料列，然後選取 [刪除] 以刪除使用者。 您會在下一個步驟中再次新增這封電子郵件，並將確認訊息傳送至電子郵件地址。

## <a name="email-confirmation"></a>電子郵件確認

最佳做法是在註冊新使用者時確認電子郵件，以確認他們不會模擬其他人（也就是他們尚未向其他人的電子郵件註冊）。 假設您有一個討論論壇，您會想要防止 `"bob@cpandl.com"` 註冊為 `"joe@contoso.com"`。 若未確認電子郵件，`"joe@contoso.com"` 可能會從您的應用程式收到不必要的電子郵件。 假設 Bob 不小心註冊為 `"bib@cpandl.com"` 且未注意到，他將無法使用密碼復原，因為應用程式沒有正確的電子郵件。 電子郵件確認只提供 bot 的有限保護，並不會提供保護來防止被判定的垃圾郵件。

您通常會想要防止新使用者將任何資料張貼到您的網站，然後再由電子郵件、SMS 文字訊息或其他機制確認。 在下列各節中，我們將啟用電子郵件確認並修改程式碼，以防止新註冊的使用者登入，直到他們的電子郵件確認為止。 您將在本教學課程中使用電子郵件服務 SendGrid。

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>連結 SendGrid

SendGrid 已變更其 API，因為已撰寫此教學課程。 如需目前的 SendGrid 指示，請參閱[SendGrid](http://sendgrid.com/)或[啟用帳戶確認和密碼](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery)復原。

雖然本教學課程僅示範如何透過[SendGrid](http://sendgrid.com/)新增電子郵件通知，但您可以使用 SMTP 和其他機制來傳送電子郵件（請參閱[其他資源](#addRes)）。

1. 在 Visual Studio 中，開啟 **套件管理員主控台** （**工具**  - &gt;  **NuGet 套件**管理員 -&gt; **Package Manager Console**），然後輸入下列命令：  
    `Install-Package SendGrid`
2. 移至[Azure SendGrid 註冊頁面](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)，並註冊免費的 SendGrid 帳戶。 您也可以直接在[SendGrid 的網站](http://www.sendgrid.com)上註冊免費的 SendGrid 帳戶。
3. 從**方案總管**開啟*應用程式\_[啟動*] 資料夾中的*IdentityConfig.cs*檔案，並將下列以黃色反白顯示的程式碼新增至 `EmailService` 類別以設定**SendGrid**：

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. 此外，將下列 `using` 語句加入至*IdentityConfig.cs*檔案的開頭： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. 為了讓此範例保持簡單，您會將電子郵件服務帳戶值儲存*在 web.config 檔案*的 `appSettings` 區段中。 將下列以黃色反白顯示的 XML 加入至專案*根目錄的 web.config*檔案中：

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > 安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。 在此範例中，帳戶和認證會儲存在*web.config*檔案的**appSetting**區段中。 在 Azure 上，您可以將這些值安全地儲存在 Azure 入口網站的 [ **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] 索引標籤上。 如需相關資訊，請參閱 Rick Anderson 的主題[：將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳作法](https://go.microsoft.com/fwlink/?LinkId=513141)。
6. 新增電子郵件服務值以反映您的 SendGrid authentication 值（使用者名稱和密碼），以便您可以從您的應用程式成功傳送電子郵件。 請務必使用您的 SendGrid 帳戶名稱，而不是您所提供的電子郵件地址 SendGrid。

### <a name="enable-email-confirmation"></a>啟用電子郵件確認

 若要啟用電子郵件確認，您將使用下列步驟來修改註冊程式碼。  

1. 在 [*帳戶*] 資料夾中，開啟*Register.aspx.cs*程式碼後置，並更新 `CreateUser_Click` 方法以啟用下列反白顯示的變更： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. 在**方案總管**中，以滑鼠右鍵按一下*default.aspx* ，然後選取 [**設定為起始頁**]。
3. 按 F5 執行應用程式 **。** 顯示頁面之後，按一下 [**註冊**] 連結以顯示 [註冊] 頁面。
4. 輸入您的電子郵件和密碼，然後按一下 [**註冊**] 按鈕，透過 SendGrid 傳送電子郵件訊息。  
   專案和程式碼的目前狀態可讓使用者在完成註冊表單之後登入，即使他們尚未確認其帳戶也一樣。
5. 檢查您的電子郵件帳戶，然後按一下連結以確認您的電子郵件。  
   提交註冊表單之後，您將會登入。  
    ![範例網站-已登入](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>在登入之前需要電子郵件確認

雖然您已確認電子郵件帳戶，但此時您不需要按一下驗證電子郵件中包含的連結，即可完整登入。 在下一節中，您將修改程式碼，要求新的使用者在登入（驗證）之前，必須先有已確認的電子郵件。

1. 在 Visual Studio 的**方案總管**中，以下列醒目提示的變更，更新包含在 [*帳戶*] 資料夾中的*Register.aspx.cs*程式碼後置中的 `CreateUser_Click` 事件： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. 在*Login.aspx.cs*程式碼後置中，使用下列反白顯示的變更來更新 `LogIn` 方法： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a>執行應用程式

 現在您已完成程式碼來檢查是否已確認使用者的電子郵件地址，您可以同時檢查**註冊**和**登**入頁面上的功能。 

1. 刪除**AspNetUsers**資料表中的任何帳戶，其中包含您想要測試的電子郵件別名。
2. 執行應用程式（**F5**），並確認您在確認您的電子郵件地址之前，無法註冊為使用者。
3. 在透過剛傳送的電子郵件確認新帳戶之前，請嘗試以新帳戶登入。  
 您會看到您無法登入，而且必須有已確認的電子郵件帳戶。
4. 確認您的電子郵件地址之後，請登入應用程式。

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a>密碼修復和重設

1. 在 Visual Studio 中，從包含在*帳戶*資料夾的*Forgot.aspx.cs*程式碼後置中，移除 `Forgot` 方法中的批註字元，讓方法顯示如下： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. 開啟 [*登入 .aspx* ] 頁面。 取代**loginForm**區段結尾附近的標記，如下所示： 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. 開啟*Login.aspx.cs*程式碼後置，並取消批註 `Page_Load` 事件處理常式中以黃色醒目提示的下列程式程式碼： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. 按 F5 執行應用程式 **。** 顯示頁面之後，按一下 [**登入**] 連結。
5. 按一下 [**忘記密碼？** ] 連結，以顯示 [**忘記密碼**] 頁面。
6. 輸入您的電子郵件地址，然後按一下 [**提交**] 按鈕，將電子郵件傳送至您的位址，以讓您重設密碼。   
   檢查您的電子郵件帳戶，然後按一下連結以顯示 [**重設密碼**] 頁面。
7. 在 [**重設密碼**] 頁面上，輸入您的電子郵件、密碼和確認的密碼。 然後，按下 [**重設**] 按鈕。  
   當您成功重設密碼時，將會顯示 [**變更密碼**] 頁面。 現在您可以使用新密碼登入。

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>重新傳送電子郵件確認連結

一旦使用者建立新的本機帳戶，他們就會收到電子郵件，要求他們在登入之前必須先使用確認連結。 如果使用者不小心刪除了確認電子郵件，或電子郵件從未送達，他們就需要再次傳送確認連結。 下列程式碼變更顯示如何啟用此動作。

1. 在 Visual Studio 中，開啟**Login.aspx.cs**程式碼後置，並在 `LogIn` 事件處理常式之後加入下列事件處理常式：   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. 藉由變更黃色反白顯示的程式碼，在*Login.aspx.cs*程式碼後置中修改 `LogIn` 事件處理常式，如下所示： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. 新增以黃色反白顯示的程式碼，以更新*登入 .aspx*頁面，如下所示： 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. 刪除**AspNetUsers**資料表中的任何帳戶，其中包含您想要測試的電子郵件別名。
5. 執行應用程式（**F5**）並註冊您的電子郵件地址。
6. 在透過剛傳送的電子郵件確認新帳戶之前，請嘗試以新帳戶登入。  
   您會看到您無法登入，而且必須有已確認的電子郵件帳戶。 此外，您現在可以重新傳送確認訊息到您的電子郵件帳戶。
7. 輸入您的電子郵件地址和密碼，然後按下 [**重新傳送確認**] 按鈕。
8. 一旦您根據新傳送的電子郵件訊息確認您的電子郵件地址，請登入應用程式。

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a>針對應用程式進行疑難排解

如果您未收到電子郵件，其中包含驗證認證的連結：

- 檢查您的垃圾郵件資料夾。
- 登入您的 SendGrid 帳戶，然後按一下 [[電子郵件活動] 連結](https://sendgrid.com/logs/index)。
- 請確定您使用的是 SendGrid 使用者帳戶名稱作為*web.config*值，而不是您的 SendGrid 帳戶電子郵件地址。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他資源

- [ASP.NET Identity 建議資源的連結](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [使用 ASP.NET Identity 進行帳戶確認和密碼復原](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Web Forms 教學課程系列-新增 OAuth 2.0 提供者](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms 教學課程系列-為專案啟用 SSL](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
