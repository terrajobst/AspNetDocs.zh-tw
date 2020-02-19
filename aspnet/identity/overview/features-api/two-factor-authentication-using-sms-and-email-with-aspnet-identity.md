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
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456734"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a>使用 SMS 的雙因素驗證與 ASP.NET Identity 的電子郵件

by [Hao Kung](https://github.com/HaoK)、 [Pranav 請參閱 rastogi](https://github.com/rustd)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Suhas Joshi](https://github.com/suhasj)

> 本教學課程將說明如何使用 SMS 和電子郵件來設定雙因素驗證（2FA）。
> 
> 這篇文章是由 Rick Anderson （[@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)）、Pranav 請參閱 rastogi （[@rustd](https://twitter.com/rustd)）、Hao Kung 和 Suhas Joshi 所撰寫。 NuGet 範例主要是由 Hao Kung 所撰寫。

本主題包含下列項目：

- [建立身分識別範例](#build)
- [設定 SMS 以進行雙因素驗證](#SMS)
- [啟用雙因素驗證](#enable2)
- [如何註冊雙因素驗證提供者](#reg)
- [合併社交和本機登入帳戶](#combine)
- [從暴力密碼破解攻擊的帳戶鎖定](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>建立身分識別範例

在本節中，您將使用 NuGet 來下載我們將使用的範例。 一開始請先安裝並執行 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。 安裝 Visual Studio [2013 Update 2 或更新](https://go.microsoft.com/fwlink/?LinkId=390521)版本。

> [!NOTE]
> 警告：您必須安裝 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) ，才能完成本教學課程。

1. 建立新的***空白***ASP.NET Web 專案。
2. 在 [套件管理員主控台] 中，輸入下列命令：  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   在本教學課程中，我們將使用[SendGrid](http://sendgrid.com/)來傳送電子郵件和[Twilio](https://www.twilio.com/) ，或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) sms 傳送。 `Identity.Samples` 套件會安裝我們要使用的程式碼。
3. 將[專案設定為使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. *選擇性*：遵循我的[電子郵件確認教學](account-confirmation-and-password-recovery-with-aspnet-identity.md)課程中的指示來連結 SendGrid，然後執行應用程式並註冊電子郵件帳戶。
5. *選擇性：* 移除範例中的電子郵件連結確認代碼（帳戶控制器中的 `ViewBag.Link` 程式碼。 請參閱 `DisplayEmail` 和 `ForgotPasswordConfirmation` 動作方法和 razor views）。
6. *選擇性：* 從 [管理] 和 [帳戶控制器]，以及從*Views\Account\VerifyCode.cshtml*和*Views\Manage\VerifyPhoneNumber.cshtml* razor Views 移除 `ViewBag.Status` 程式碼。 或者，您可以保留 `ViewBag.Status` 顯示，以測試此應用程式在本機運作的方式，而不需要連結和傳送電子郵件和 SMS 訊息。

> [!NOTE]
> 警告：如果您變更此範例中的任何安全性設定，生產應用程式將需要進行安全性審核，以明確地呼叫所做的變更。

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
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   位址：  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   命名空間：  
    `ASPSMSX2`
3. **找出 SMS 提供者使用者認證**  
  
   Twilio  
   從 Twilio 帳戶的 [**儀表板**] 索引標籤中，複製 [**帳戶 SID** ] 和 [**驗證權杖**]。  
  
   ASPSMS:  
   從您的帳戶設定中，流覽至**Userkey** ，並將它與您的自我定義**密碼**一起複製。  
  
   稍後我們會將這些值儲存在變數 `SMSAccountIdentification` 和 `SMSAccountPassword` 中。
4. **指定 SenderID/發信者**  
  
   Twilio  
   在 [**數位**] 索引標籤中，複製您的 Twilio 電話號碼。  
  
   ASPSMS:  
   在 [**解除鎖定**擁有者] 功能表中，解除鎖定一或多個始發者，或選擇英數位元（並非所有網路都支援）。  
  
   稍後我們會將此值儲存在 `SMSAccountFrom` 變數中。
5. **將 SMS 提供者認證傳送至應用程式**  
  
   將認證和寄件者電話號碼提供給應用程式：

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > 安全性-絕對不會將敏感性資料儲存在您的原始程式碼中。 帳戶和認證會加入上述程式碼中，讓範例保持簡單。 請參閱 Jon Atten 的[ASP.NET MVC：將私用設定保留在原始檔控制之外](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。
6. **將資料傳輸到 SMS 提供者的執行**  
  
   在*應用程式\_Start\IdentityConfig.cs*檔案中設定 `SmsService` 類別。  
  
   視使用的 SMS 提供者而定，啟動**Twilio**或**ASPSMS**區段： 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. 執行應用程式，並使用您先前註冊的帳戶登入。
8. 按一下您的使用者識別碼，這會在 `Manage` 控制器中啟用 `Index` 動作方法。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. 按一下 [加入]。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. 幾秒內，您就會收到包含驗證碼的文字訊息。 輸入該檔案並按下 [**提交**]。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. [管理] 視圖會顯示您的電話號碼已加入。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>檢查程式碼

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

`Manage` 控制器中的 `Index` 動作方法會根據您先前的動作來設定狀態訊息，並提供連結來變更您的本機密碼或新增本機帳戶。 `Index` 方法也會顯示此瀏覽器的狀態或您的2FA 電話號碼、外部登入、2FA 啟用和記住2FA 方法（稍後會說明）。 在標題列中按一下您的使用者識別碼（電子郵件）並不會傳遞訊息。 按一下**電話號碼：移除**連結傳遞 `Message=RemovePhoneSuccess` 作為查詢字串。  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

`AddPhoneNumber` 動作方法會顯示一個對話方塊，以輸入可接收 SMS 訊息的電話號碼。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

按一下 [**傳送驗證碼**] 按鈕，就會將電話號碼張貼到 HTTP POST `AddPhoneNumber` 動作方法。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

`GenerateChangePhoneNumberTokenAsync` 方法會產生將在 SMS 訊息中設定的安全性權杖。 如果已設定 SMS 服務，權杖會以字串的形式傳送 &quot;您的安全性驗證碼會 &lt;權杖&gt;&quot;。 `SmsService.SendAsync` 的方法會以非同步方式呼叫，然後應用程式會重新導向至 `VerifyPhoneNumber` 動作方法（顯示下列對話方塊），您可以在其中輸入驗證碼。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

當您輸入程式碼並按一下 [提交] 之後，程式碼就會張貼到 HTTP POST `VerifyPhoneNumber` 動作方法。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

`ChangePhoneNumberAsync` 方法會檢查已張貼的安全性驗證碼。 如果程式碼正確，則會將電話號碼加入 `AspNetUsers` 資料表的 [`PhoneNumber`] 欄位中。 如果該呼叫成功，就會呼叫 `SignInAsync` 方法：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

`isPersistent` 參數會設定驗證會話是否跨多個要求保存。

當您變更安全性設定檔時，系統會產生新的安全性戳記，並將其儲存在*AspNetUsers*資料表的 [`SecurityStamp`] 欄位中。 請注意，[`SecurityStamp`] 欄位與安全性 cookie 不同。 安全性 cookie 不會儲存在 `AspNetUsers` 資料表中（或身分識別 DB 中的任何其他位置）。 安全性 cookie 權杖是使用[DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)自我簽署的，並且是使用 `UserId, SecurityStamp` 和到期時間資訊所建立。

Cookie 中介軟體會檢查每個要求上的 cookie。 `Startup` 類別中的 `SecurityStampValidator` 方法會叫用資料庫，並定期檢查安全性戳記（如 `validateInterval`所指定）。 這只會每隔30分鐘發生一次（在我們的範例中），除非您變更您的安全性設定檔。 選擇30分鐘的間隔，以最小化資料庫的行程。

對安全性設定檔進行任何變更時，必須呼叫 `SignInAsync` 方法。 當安全性設定檔變更時，資料庫會更新 `SecurityStamp` 欄位，而不會呼叫 `SignInAsync` 方法，您*只*會保持登入狀態，直到下一次 OWIN 管線叫用資料庫（`validateInterval`）為止。 您可以藉由將 `SignInAsync` 方法變更為立即傳回，然後將 cookie `validateInterval` 屬性從30分鐘設為5秒來進行測試：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

當上述程式碼變更時，您可以變更安全性設定檔（例如，藉由變更**兩個因素**的狀態），而當 `SecurityStampValidator.OnValidateIdentity` 方法失敗時，您將會在5秒內登出。 移除 `SignInAsync` 方法中的傳回行，讓另一個安全性設定檔變更，而您將不會登出。`SignInAsync` 方法會產生新的安全性 cookie。

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>啟用雙因素驗證

在範例應用程式中，您必須使用 UI 來啟用雙因素驗證（2FA）。 若要啟用2FA，請按一下巡覽列中的 [使用者識別碼] （電子郵件別名）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
按一下 [啟用 2FA]。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) 登出後再重新登入。 如果您已啟用電子郵件（請參閱[前一個教學](account-confirmation-and-password-recovery-with-aspnet-identity.md)課程），您可以選取要2FA 的 SMS 或電子郵件。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) 此時會顯示 [驗證代碼] 頁面，您可以在其中輸入程式碼（來自 SMS 或電子郵件）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) 按一下 [**記住此瀏覽器**] 核取方塊，就不需要使用2FA 來登入該電腦和瀏覽器。 啟用2FA 並按一下 [**記住此瀏覽器**]，可讓您從惡意使用者嘗試存取您的帳戶時，提供強式2FA 保護，前提是他們無法存取您的電腦。 您可以在您經常使用的任何私人電腦上執行此動作。 藉由設定 [**記住此瀏覽器**]，您就能從不常使用的電腦獲得2FA 的安全性，並讓您不必在自己的電腦上進行2FA。 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>如何註冊雙因素驗證提供者

當您建立新的 MVC 專案時， *IdentityConfig.cs*檔案會包含下列程式碼來註冊雙因素驗證提供者：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>新增2FA 的電話號碼

`Manage` 控制器中的 `AddPhoneNumber` 動作方法會產生安全性權杖，並將它傳送至您所提供的電話號碼。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

傳送權杖之後，它會重新導向至 `VerifyPhoneNumber` 動作方法，您可以在其中輸入程式碼以註冊2FA 的 SMS。 在您驗證電話號碼之前，不會使用 SMS 2FA。

## <a name="enabling-2fa"></a>啟用2FA

`EnableTFA` 動作方法會啟用2FA：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

請注意，必須呼叫 `SignInAsync`，因為 [啟用 2FA] 是安全性設定檔的變更。 啟用2FA 時，使用者必須使用2FA 來登入，並使用他們已註冊的2FA 方法（範例中的 SMS 和電子郵件）。

您可以新增更多2FA 提供者（例如 QR 代碼產生器），或您可以自行撰寫（請參閱搭配[ASP.NET Identity 使用 Google 驗證](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)器）。

> [!NOTE]
> 2FA 碼是使用以時間為基礎的單次[密碼演算法](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)所產生，而代碼則有效6分鐘。 如果您需要6分鐘以上的時間來輸入程式碼，將會收到不正確代碼錯誤訊息。

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>合併社交和本機登入帳戶

您可以按一下電子郵件連結，以合併本機和社交帳戶。 在下列順序中 &quot;RickAndMSFT@gmail.com&quot; 會先建立為本機登入，但您可以先將帳戶建立為社交記錄，然後再新增本機登入。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

按一下 [**管理**] 連結。 請注意與此帳戶相關聯的0外部（社交登入）。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

按一下另一個登入服務的連結，並接受應用程式要求。 已合併這兩個帳戶，您將能夠使用任一帳戶登入。 您可能想要讓使用者新增本機帳戶，以防其社交記錄在驗證服務已關閉，或更有可能失去其社交帳戶的存取權。

在下圖中，Tom 是社交記錄（您可以從頁面上顯示的 [**外部登入： 1** ] 看到）。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

按一下 [**挑選密碼**] 可讓您新增與相同帳戶相關聯的本機登入。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>從暴力密碼破解攻擊的帳戶鎖定

您可以藉由啟用使用者鎖定，來保護應用程式上的帳戶免于字典攻擊。 `ApplicationUserManager Create` 方法中的下列程式碼會設定 lock out：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

上述程式碼只會啟用雙因素驗證的鎖定。 雖然您可以藉由在帳戶控制器的 `Login` 方法中將 `shouldLockout` 變更為 true 來啟用登入鎖定，但建議您不要針對登入啟用鎖定，因為它會讓帳戶容易遭受[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)登入攻擊。 在範例程式碼中，已停用在 `ApplicationDbInitializer Seed` 方法中建立之系統管理員帳戶的鎖定：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>要求使用者必須有已驗證的電子郵件帳戶

下列程式碼會要求使用者必須先有已驗證的電子郵件帳戶，才能登入：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>使用檢查2FA 需求的方式

本機登入和社交記錄都會檢查是否已啟用2FA。 如果已啟用2FA，`SignInManager` 登入方法會傳回 `SignInStatus.RequiresVerification`，而使用者將會被重新導向至 `SendCode` 動作方法，讓他們必須輸入程式碼才能依序完成記錄。 如果使用者的本機 cookie 設定了 RememberMe，則 `SignInManager` 會傳回 `SignInStatus.Success`，而不需要經過2FA。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

下列程式碼顯示 `SendCode` 動作方法。 建立[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)時，會為使用者啟用所有的2FA 方法。 [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)會傳遞至[html.dropdownlistfor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper，讓使用者選取2FA 方法（通常是電子郵件和 SMS）。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

一旦使用者張貼2FA 方法，就會呼叫 `HTTP POST SendCode` 動作方法，`SignInManager` 傳送2FA 程式碼，然後將使用者重新導向至 `VerifyCode` 動作方法，他們可以在其中輸入程式碼以完成登入。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA 鎖定

雖然您可以在登入密碼嘗試失敗時設定帳戶鎖定，但該方法會讓您的登入容易受到[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)鎖定的影響。 我們建議您只使用2FA 的帳戶鎖定。 建立 `ApplicationUserManager` 時，範例程式碼會將2FA 鎖定和 `MaxFailedAccessAttemptsBeforeLockout` 設定為五個。 一旦使用者登入（透過本機帳戶或社交帳戶），就會儲存2FA 上的每個失敗嘗試，並在達到最大嘗試次數時，將使用者鎖定五分鐘（您可以使用 `DefaultAccountLockoutTimeSpan`設定鎖定時間）。

<a id="addRes"></a>

## <a name="additional-resources"></a>其他資源

- [ASP.NET Identity 建議的資源](../getting-started/aspnet-identity-recommended-resources.md)完整的身分識別 blog、影片、教學課程，以及絕佳的連結清單。
- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)也會顯示如何將設定檔資訊新增至使用者資料表。
- [ASP.NET MVC 和 Identity 2.0：瞭解 John Atten 的基本概念](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)。
- [使用 ASP.NET Identity 進行帳戶確認和密碼復原](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Identity 簡介](../getting-started/introduction-to-aspnet-identity.md)
- [宣佈 2.0.0 By Pranav 請參閱 rastogi ASP.NET Identity 的 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) 。
- [ASP.NET Identity 2.0：設定帳戶驗證和](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)由 John Atten 的雙因素授權。
