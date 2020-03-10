---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: 帳戶確認 & 密碼復原-ASP.NET Identity （C#）-ASP.NET 4。x
author: HaoK
description: 進行本教學課程之前，您應該先完成使用登入、電子郵件確認和密碼重設來建立安全的 ASP.NET MVC 5 web 應用程式。 本教學課程 。
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4b2c88280df39aa81d60f9508910e8fe5d6db6b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616813"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>使用 ASP.NET Identity （C#）進行帳戶確認和密碼復原

> 進行本教學課程之前，您應該先完成[使用登入、電子郵件確認和密碼重設來建立安全的 ASP.NET MVC 5 web 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。 本教學課程包含更多詳細資料，並將示範如何設定電子郵件以進行本機帳戶確認，並允許使用者在 ASP.NET Identity 中重設忘記密碼。

本機使用者帳戶需要使用者建立帳戶的密碼，並在 web 應用程式中儲存（安全）該密碼。 ASP.NET Identity 也支援社交帳戶，這不需要使用者建立應用程式的密碼。 [社交帳戶](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)會使用協力廠商（例如 Google、Twitter、Facebook 或 Microsoft）來驗證使用者。 本主題包含下列項目：

- [建立 ASP.NET MVC 應用程式](#createMvc)，並探索 ASP.NET Identity 功能。
- [建立身分識別範例](#build)
- [設定電子郵件確認](#email)

新使用者註冊其電子郵件別名，以建立本機帳戶。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

選取 [註冊] 按鈕會將包含驗證權杖的確認電子郵件傳送至其電子郵件地址。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

使用者會收到電子郵件，其中包含其帳戶的確認權杖。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

選取此連結會確認帳戶。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>密碼修復/重設

忘記其密碼的本機使用者可以將安全性權杖傳送至其電子郵件帳戶，讓他們能夠重設其密碼。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
使用者很快會收到一封電子郵件，其中包含可讓他們重設其密碼的連結。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
選取此連結會將其帶至 [重設] 頁面。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
選取 [**重設**] 按鈕將會確認密碼已重設。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>建立 ASP.NET Web 應用程式

從安裝和執行[Visual Studio 2017](https://visualstudio.microsoft.com/)開始。

1. 建立新的 ASP.NET Web 專案，並選取 [MVC] 範本。 Web form 也支援 ASP.NET Identity，因此您可以在 web Forms 應用程式中遵循類似的步驟。
2. 將驗證變更為**個別使用者帳戶**。
3. 執行應用程式，選取 [**註冊**] 連結並註冊使用者。 此時，電子郵件上的唯一驗證是使用[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)屬性。
4. 在伺服器總管中，流覽至 [**資料 Connections\DefaultConnection\Tables\AspNetUsers**]，以滑鼠右鍵按一下，然後選取 [**開啟資料表定義**]。

    下圖顯示 `AspNetUsers` 架構：

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. 以滑鼠右鍵按一下 [ **AspNetUsers** ] 資料表，然後選取 [**顯示資料表資料**]。  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   此時尚未確認電子郵件。

ASP.NET Identity 的預設資料存放區是 Entity Framework 的，但您可以將它設定為使用其他資料存放區，以及新增其他欄位。 請參閱本教學課程結尾處的[其他資源](#addRes)一節。

當應用程式啟動時，會呼叫[OWIN 啟動類別](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md)（ *Startup.cs* ），並叫用*app\_Start\Startup.Auth.cs*中的 `ConfigureAuth` 方法，這會設定 OWIN 管線並將 ASP.NET Identity 初始化。 檢查 `ConfigureAuth` 方法。 每個 `CreatePerOwinContext` 呼叫都會註冊一個回呼（儲存在 `OwinContext`中），每個要求都會呼叫一次，以建立指定類型的實例。 您可以在函式中設定中斷點和每個類型的 `Create` 方法（`ApplicationDbContext, ApplicationUserManager`），並確認是否在每個要求上呼叫它們。 `ApplicationDbContext` 和 `ApplicationUserManager` 的實例會儲存在 OWIN 內容中，這可在整個應用程式中存取。 ASP.NET Identity 透過 cookie 中介軟體攔截到 OWIN 管線。 如需詳細資訊，請參閱[ASP.NET Identity 中適用于 UserManager 類別的每個要求存留期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。

當您變更安全性設定檔時，系統會產生新的安全性戳記，並將其儲存在*AspNetUsers*資料表的 [`SecurityStamp`] 欄位中。 請注意，[`SecurityStamp`] 欄位與安全性 cookie 不同。 安全性 cookie 不會儲存在 `AspNetUsers` 資料表中（或身分識別 DB 中的任何其他位置）。 安全性 cookie 權杖是使用[DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)自我簽署的，並且是使用 `UserId, SecurityStamp` 和到期時間資訊所建立。

Cookie 中介軟體會檢查每個要求上的 cookie。 `Startup` 類別中的 `SecurityStampValidator` 方法會叫用資料庫，並定期檢查安全性戳記（如 `validateInterval`所指定）。 這只會每隔30分鐘發生一次（在我們的範例中），除非您變更您的安全性設定檔。 選擇30分鐘的間隔，以最小化資料庫的行程。 如需詳細資訊，請參閱我的[雙因素驗證教學](index.md)課程。

根據程式碼中的批註，`UseCookieAuthentication` 方法支援 cookie 驗證。 [`SecurityStamp`] 欄位和相關聯的程式碼會為您的應用程式提供額外的安全性層級，當您變更密碼時，就會登出您用來登入的瀏覽器。 `SecurityStampValidator.OnValidateIdentity` 方法可讓應用程式在使用者登入時驗證安全性權杖，這會在您變更密碼或使用外部登入時使用。 這是為了確保使用舊密碼所產生的任何權杖（cookie）失效。 在範例專案中，如果您變更使用者的密碼，則會為使用者產生新的權杖，任何先前的權杖都會失效，而且 [`SecurityStamp`] 欄位會更新。

身分識別系統可讓您設定應用程式，以便在使用者的安全性設定檔變更時（例如，當使用者變更其密碼或變更相關聯的登入（例如從 Facebook、Google、Microsoft 帳戶等）時，使用者已登出所有瀏覽器實例。 例如，下圖顯示[單一 signout 範例](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample)應用程式，可讓使用者藉由選取一個按鈕來登出所有瀏覽器實例（在此案例中為 IE、Firefox 和 Chrome）。 或者，此範例可讓您只登出特定的瀏覽器實例。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[單一 signout 範例](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample)應用程式會顯示 ASP.NET Identity 如何讓您重新產生安全性權杖。 這是為了確保使用舊密碼所產生的任何權杖（cookie）失效。 這項功能會為您的應用程式提供額外的安全性層級;當您變更密碼時，您將會登出已登入此應用程式的位置。

*應用程式\_Start\IdentityConfig.cs*檔案包含 `ApplicationUserManager`、`EmailService` 和 `SmsService` 類別。 `EmailService` 和 `SmsService` 類別都會執行 `IIdentityMessageService` 介面，因此您在每個類別中都有共同的方法來設定電子郵件和 SMS。 雖然本教學課程僅示範如何透過[SendGrid](http://sendgrid.com/)新增電子郵件通知，但您可以使用 SMTP 和其他機制來傳送電子郵件。

`Startup` 類別也包含定案盤子來新增社交登入（Facebook、Twitter 等），請參閱我的教學課程[使用 Facebook、twitter、LinkedIn 和 Google OAuth2 登入](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)的教學課程，以取得詳細資訊。

檢查 `ApplicationUserManager` 類別，其中包含使用者身分識別資訊，並設定下列功能：

- 密碼強度需求。
- 使用者鎖定（嘗試和時間）。
- 雙因素驗證（2FA）。 我會在另一個教學課程中討論2FA 和 SMS。
- 連結電子郵件和 SMS 服務。 （我將在另一個教學課程中討論 SMS）。

`ApplicationUserManager` 類別衍生自泛型 `UserManager<ApplicationUser>` 類別。 `ApplicationUser` 衍生自[IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)。 `IdentityUser` 衍生自泛型 `IdentityUser` 類別：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

上述屬性會與 `AspNetUsers` 資料表中的屬性一致，如上所示。

`IUser` 上的泛型引數可讓您使用不同類型的主要金鑰來衍生類別。 請參閱[ChangePK](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)範例，其中顯示如何將主鍵從字串變更為 INT 或 GUID。

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` （`public class ApplicationUserManager : UserManager<ApplicationUser>`）在*Models\IdentityModels.cs*中定義為：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

上述反白顯示的程式碼會產生[ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)。 ASP.NET Identity 和 OWIN Cookie 驗證是以宣告為基礎，因此架構會要求應用程式為使用者產生 `ClaimsIdentity`。 `ClaimsIdentity` 包含使用者所有宣告的相關資訊，例如使用者的名稱、年齡和使用者所屬的角色。 您也可以在這個階段為使用者新增更多宣告。

OWIN `AuthenticationManager.SignIn` 方法會傳入 `ClaimsIdentity` 並登入使用者：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)會示範如何將其他屬性新增至 `ApplicationUser` 類別。

## <a name="email-confirmation"></a>電子郵件確認

建議您確認新使用者註冊的電子郵件，以確認他們不會模擬其他人（也就是他們尚未向其他人的電子郵件註冊）。 假設您有一個討論論壇，您會想要防止 `"bob@example.com"` 註冊為 `"joe@contoso.com"`。 若未確認電子郵件，`"joe@contoso.com"` 可能會從您的應用程式收到不必要的電子郵件。 假設 Bob 不小心註冊為 `"bib@example.com"` 且未注意到，他將無法使用密碼復原，因為應用程式沒有正確的電子郵件。 電子郵件確認僅為 bot 提供有限的保護，並不會提供保護來防止被判定的垃圾郵件，他們有許多可使用的電子郵件別名來進行註冊。在下列範例中，使用者將無法變更其密碼，除非他們的帳戶已確認（藉由在他們所註冊的電子郵件帳戶上，選取收到的確認連結）。您可以將此工作流程套用至其他案例，例如傳送連結以確認並重設系統管理員所建立之新帳戶的密碼，並在使用者變更其設定檔時，傳送電子郵件給使用者。 您通常會想要防止新使用者將任何資料張貼到您的網站，然後再由電子郵件、SMS 文字訊息或其他機制確認。 <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>建立更完整的範例

在本節中，您將使用 NuGet 來下載我們將使用的更完整範例。

1. 建立新的***空白***ASP.NET Web 專案。
2. 在 [套件管理員主控台] 中，輸入下列命令： 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   在本教學課程中，我們將使用[SendGrid](http://sendgrid.com/)來傳送電子郵件。 `Identity.Samples` 套件會安裝我們要使用的程式碼。
3. 將[專案設定為使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. 藉由執行應用程式、選取 [**註冊**] 連結，以及張貼註冊表單，來測試本機帳戶的建立。
5. 選取 [示範電子郵件] 連結，以模擬電子郵件確認。
6. 移除範例中的電子郵件連結確認代碼（帳戶控制器中的 `ViewBag.Link` 程式碼。 請參閱 `DisplayEmail` 和 `ForgotPasswordConfirmation` 動作方法和 razor views）。

> [!WARNING]
> 如果您變更此範例中的任何安全性設定，則生產應用程式必須進行安全性審查，以明確地呼叫所做的變更。

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>檢查 App\_Start\IdentityConfig.cs 中的程式碼

此範例會示範如何建立帳戶，並將它新增至系統*管理員*角色。 您應該將範例中的電子郵件取代為系統管理員帳戶所使用的電子郵件。 立即建立系統管理員帳戶最簡單的方式，就是在 `Seed` 方法中以程式設計方式。 我們希望未來有一項工具可讓您建立及管理使用者和角色。 範例程式碼可讓您建立和管理使用者和角色，但您必須先擁有系統管理員帳戶，才能執行角色和使用者管理頁面。 在此範例中，系統會在植入資料庫時建立管理帳戶。

變更密碼，並將名稱變更為您可以接收電子郵件通知的帳戶。

> [!WARNING]
> 安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。

如先前所述，startup 類別中的 `app.CreatePerOwinContext` 呼叫會將回呼新增至應用程式 DB 內容、使用者管理員和角色管理員類別的 `Create` 方法。 OWIN 管線會針對每個要求，在這些類別上呼叫 `Create` 方法，並儲存每個類別的內容。 帳戶控制器會從 HTTP 內容公開使用者管理員（其中包含 OWIN 內容）：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

當使用者註冊本機帳戶時，會呼叫 `HTTP Post Register` 方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

上述程式碼會使用模型資料，透過輸入的電子郵件和密碼來建立新的使用者帳戶。 如果電子郵件別名位於資料存放區中，則帳戶建立會失敗，且會再次顯示表單。 `GenerateEmailConfirmationTokenAsync` 方法會建立安全的確認權杖，並將它儲存在 ASP.NET Identity 資料存放區中。 「 [Url」動作](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx)方法會建立包含 `UserId` 和確認 token 的連結。 此連結接著會以電子郵件傳送給使用者，使用者可以在其電子郵件應用程式中選取該連結，以確認其帳戶。

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>設定電子郵件確認

移至[Azure SendGrid 註冊頁面](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)，並註冊免費帳戶。 新增與下列類似的程式碼，以設定 SendGrid：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> 電子郵件用戶端經常只接受文字訊息（沒有 HTML）。 您應該以文字和 HTML 提供訊息。 在上述的 SendGrid 範例中，這項作業是使用上面顯示的 `myMessage.Text` 和 `myMessage.Html` 程式碼來完成。

下列程式碼顯示如何使用[send-mailmessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx)類別傳送電子郵件，其中 `message.Body` 只會傳回連結。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> 安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。 帳戶和認證會儲存在 appSetting 中。 在 Azure 上，您可以將這些值安全地儲存在 Azure 入口網站的 [ **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] 索引標籤上。 請參閱[將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳做法](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。

輸入您的 SendGrid 認證、執行應用程式、使用電子郵件別名進行註冊，即可在您的電子郵件中選取 [確認] 連結。 若要瞭解如何使用您的[Outlook.com](http://outlook.com)電子郵件帳戶執行此動作，請參閱 John Atten 的[ C# smtp Configuration for Outlook.Com SMTP 主機](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx)和他的[ASP.NET Identity 2.0：設定帳戶驗證和雙因素授權](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)文章。

一旦使用者選取 [**註冊**] 按鈕，就會將包含驗證權杖的確認電子郵件傳送到其電子郵件地址。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

使用者會收到電子郵件，其中包含其帳戶的確認權杖。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>檢查程式碼

下列程式碼顯示 `POST ForgotPassword` 方法。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

如果尚未確認使用者電子郵件，方法會以無訊息模式失敗。 如果針對不正確電子郵件地址公佈了錯誤，惡意使用者可以使用該資訊來尋找有效的 userId （電子郵件別名）以進行攻擊。

下列程式碼顯示帳戶控制器中的 `ConfirmEmail` 方法，當使用者在傳送給他們的電子郵件中選取確認連結時，就會呼叫此方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

一旦使用了遺忘的密碼權杖，就會失效。 `Create` 方法（在*應用程式\_Start\IdentityConfig.cs*檔案中）的下列程式碼變更會將權杖設定為在3小時內過期。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

使用上述程式碼時，忘記密碼和電子郵件確認權杖會在3小時內過期。 預設 `TokenLifespan` 為一天。

下列程式碼會顯示電子郵件確認方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 為了讓您的應用程式更安全，ASP.NET Identity 支援雙因素驗證（2FA）。 請參閱[ASP.NET Identity 2.0：設定帳戶驗證和](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)由 John Atten 的雙因素授權。 雖然您可以在登入密碼嘗試失敗時設定帳戶鎖定，但該方法會讓您的登入容易受到[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)鎖定的影響。 我們建議您只使用2FA 的帳戶鎖定。  
<a id="addRes"></a>

## <a name="additional-resources"></a>其他資源

- [ASP.NET Identity 的自訂儲存體提供者概觀](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)也會顯示如何將設定檔資訊新增至使用者資料表。
- [ASP.NET MVC 和 Identity 2.0：瞭解 John Atten 的基本概念](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)。
- [ASP.NET Identity 簡介](../getting-started/introduction-to-aspnet-identity.md)
- [宣佈 2.0.0 By Pranav 請參閱 rastogi ASP.NET Identity 的 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) 。
