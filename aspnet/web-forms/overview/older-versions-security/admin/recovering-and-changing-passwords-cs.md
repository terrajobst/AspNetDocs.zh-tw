---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
title: 復原及變更密碼（C#） |Microsoft Docs
author: rick-anderson
description: ASP.NET 包含兩個 Web 控制項，協助您復原和變更密碼。 PasswordRecovery 控制項可讓訪客復原遺失的 pa 。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 19c4d042-4e34-4b44-9f1d-6bf2253ba366
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c07b8a3c36e4863c6d2d356b8483544ac4cafeb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576518"
---
# <a name="recovering-and-changing-passwords-c"></a>復原及變更密碼 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.13.zip)或[下載 PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_cs.pdf)

> ASP.NET 包含兩個 Web 控制項，協助您復原和變更密碼。 PasswordRecovery 控制項可讓訪客復原其遺失的密碼。 ChangePassword 控制項可讓使用者更新其密碼。 就像我們在本教學課程系列中所見到的其他登入相關 Web 控制項一樣，PasswordRecovery 和 ChangePassword 控制項也會在幕後使用成員資格架構來重設或修改使用者的密碼。

## <a name="introduction"></a>簡介

在我的銀行、公用程式公司、電話公司、電子郵件帳戶和個人化 web 入口網站之間，我與大多數人一樣，都有數十種不同的密碼需要記住。 因為有這麼多的認證可以記住這些日子，所以人們不太常忘記自己的密碼。 為因應此情況，提供使用者帳戶的網站必須包含一種方法，讓使用者能夠復原自己的密碼。 此程式通常牽涉到產生新的隨機密碼，並以電子郵件傳送給使用者在檔案上的電子郵件地址。 接收到新密碼之後，大部分的使用者都會回到網站，並將其密碼從隨機產生的密碼變更為更容易記住的密碼。

ASP.NET 包含兩個 Web 控制項，協助您復原和變更密碼。 PasswordRecovery 控制項可讓訪客復原其遺失的密碼。 ChangePassword 控制項可讓使用者更新其密碼。 就像我們在本教學課程系列中所見到的其他登入相關 Web 控制項一樣，PasswordRecovery 和 ChangePassword 控制項也會在幕後使用成員資格架構來重設或修改使用者的密碼。

在本教學課程中，我們將使用這兩個控制項來進行檢查。 我們也會瞭解如何透過 `MembershipUser` 類別的 `ChangePassword` 和 `ResetPassword` 方法，以程式設計方式變更和重設使用者的密碼。

## <a name="step-1-helping-users-recover-lost-passwords"></a>步驟1：協助使用者復原遺失的密碼

所有支援使用者帳戶的網站都必須為使用者提供一些機制來復原其遺忘的密碼。 好消息是，您可以輕鬆地在 ASP.NET 中執行這類功能，這是因為 PasswordRecovery 的 Web 控制項。 PasswordRecovery 控制項會轉譯介面，以提示使用者輸入其使用者名稱，並視需要回應其安全性問題的答案。 然後，它會以電子郵件傳送使用者的密碼。

> [!NOTE]
> 由於電子郵件訊息是透過網路以純文字傳輸，因此在透過電子郵件傳送使用者的密碼時，會有安全性風險。

PasswordRecovery 控制項包含三個視圖：

- **Username** -提示訪客提供他們的使用者名稱。 這是初始的視圖。
- **問題**-將使用者的使用者名稱和安全性問題顯示為文字，並附上一個文字方塊，讓使用者輸入他的安全性問題答案。
- **成功**-顯示訊息，通知使用者他的密碼已通過電子郵件傳送。

顯示的視圖和 PasswordRecovery 控制項執行的動作，取決於下列成員資格設定：

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

成員資格架構的 `RequiresQuestionAndAnswer` 設定會指出在註冊帳戶時，使用者是否必須指定安全性問題和答案。 如我們在<a id="_msoanchor_1"> </a>[*建立使用者帳戶*](../membership/creating-user-accounts-cs.md)教學課程中所討論，如果 `RequiresQuestionAndAnswer` 為 True （預設值），則 CreateUserWizard 的介面會包含新使用者安全性問題和答案的 TextBox 控制項。如果 `RequiresQuestionAndAnswer` 為 False，則不會收集這類資訊。 同樣地，如果 `RequiresQuestionAndAnswer` 為 True，則 PasswordRecovery 控制項會在使用者輸入其使用者名稱之後，顯示問題視圖;只有當使用者輸入正確的安全性答案時，才會復原密碼。 不過，如果 `RequiresQuestionAndAnswer` 為 False，則 PasswordRecovery 控制項會直接從 [使用者名稱] 視圖移至 [成功] 視圖。

在使用者提供他的使用者名稱（或其使用者名稱和安全性答案）之後，如果 `RequiresQuestionAndAnswer` 為 True，PasswordRecovery 會以電子郵件傳送使用者的密碼。 如果 [`EnablePasswordRetrieval`] 選項設定為 [True]，則會以電子郵件將其目前的密碼傳送給使用者。 如果設定為 False，且 `EnablePasswordReset` 設定為 True，則 PasswordRecovery 控制項會為使用者產生新的隨機密碼，並以電子郵件將新密碼傳送給他們。 如果 `EnablePasswordRetrieval` 和 `EnablePasswordReset` 都是 False，則 PasswordRecovery 控制項會擲回例外狀況。

> [!NOTE]
> 回想一下，`SqlMembershipProvider` 會以下列三種格式的其中一種來儲存使用者的密碼：清除、雜湊（預設值）或加密。 所使用的儲存機制視成員資格設定而定;示範應用程式會使用雜湊的密碼格式。 使用雜湊的密碼格式時，`EnablePasswordRetrieval` 選項必須設定為 False，因為系統無法從資料庫中儲存的雜湊版本判斷使用者的實際密碼。

[圖 1] 說明 PasswordRecovery 的介面和行為如何受到成員資格設定的影響。

[![RequiresQuestionAndAnswer、EnablePasswordRetrieval 和 EnablePasswordReset 會影響 PasswordRecovery 控制項的外觀和行為](recovering-and-changing-passwords-cs/_static/image2.png)](recovering-and-changing-passwords-cs/_static/image1.png)

**圖 1**： `RequiresQuestionAndAnswer`、`EnablePasswordRetrieval`和 `EnablePasswordReset` 會影響 PasswordRecovery 控制項的外觀和行為（[按一下以觀看完整大小的影像](recovering-and-changing-passwords-cs/_static/image3.png)）

> [!NOTE]
> <a id="_msoanchor_2"></a>在[*SQL Server 中建立成員資格架構*](../membership/creating-the-membership-schema-in-sql-server-cs.md)教學課程中，我們會將 `RequiresQuestionAndAnswer` 設定為 true、`EnablePasswordRetrieval` 設為 False，並 `EnablePasswordReset` 為 true 來設定成員資格提供者。

### <a name="using-the-passwordrecovery-control"></a>使用 PasswordRecovery 控制項

讓我們看一下如何在 ASP.NET 網頁中使用 PasswordRecovery 控制項。 開啟 `RecoverPassword.aspx`，並將 PasswordRecovery 控制項從 [工具箱] 拖放到設計工具上;將其 `ID` 設定為 `RecoverPwd`。 如同 Login 和 CreateUserWizard Web 控制項，PasswordRecovery 控制項的 views 會轉譯豐富的複合介面，其中包含標籤、文字方塊、按鈕和驗證控制項。 您可以透過控制項的樣式屬性自訂視圖的外觀，或將 views 轉換成範本。 我將這個練習留給感興趣的讀者。

當使用者造訪此頁面時，她會輸入她的使用者名稱，然後按一下 [提交] 按鈕。 因為我們已在成員資格設定設定中，將 `RequiresQuestionAndAnswer` 屬性設為 True，所以 PasswordRecovery 控制項會顯示問題視圖。 在使用者輸入正確的安全性答案，並按一下 [提交] 之後，PasswordRecovery 控制項會將使用者的密碼更新為隨機產生的密碼，並以電子郵件將此密碼傳送至檔案上的電子郵件地址。 這一切都可以讓我們不必撰寫一行程式碼！

在測試此頁面之前，有一個設定的最後一個部分通常是：我們需要在 `Web.config`中指定郵件傳遞設定。 PasswordRecovery 控制項會依賴這些設定來傳送電子郵件。

郵件傳遞設定是透過[`<system.net>` 元素](https://msdn.microsoft.com/library/6484zdc1.aspx)的[`<mailSettings>` 元素](https://msdn.microsoft.com/library/w355a94k.aspx)所指定。 使用[`<smtp>` 元素](https://msdn.microsoft.com/library/ms164240.aspx)來指出傳遞方法和預設的 [寄件者] 位址。 下列標記會將郵件設置設定為使用通訊埠25上名為 `smtp.example.com` 的網路 SMTP 伺服器，並以使用者名稱和密碼的使用者名稱/密碼認證。

> [!NOTE]
> `<system.net>` 是根 `<configuration>` 元素的子專案，以及 `<system.web>`的同級元素。 因此，請勿將 `<system.net>` 元素放在 `<system.web>` 元素內;相反地，請將它放在相同的層級。

[!code-xml[Main](recovering-and-changing-passwords-cs/samples/sample1.xml)]

除了使用網路上的 SMTP 伺服器以外，您也可以指定要傳送電子郵件訊息的收取目錄。

設定 SMTP 設定之後，請透過瀏覽器造訪 [`RecoverPassword.aspx`] 頁面。 請先嘗試輸入不存在於使用者存放區中的使用者名稱。 如 [圖 2] 所示，PasswordRecovery 控制項會顯示一則訊息，指出無法存取使用者資訊。 訊息的文字可以透過控制項的[`UserNameFailureText` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)自訂。

[如果輸入的使用者名稱無效，就會顯示 ![錯誤訊息](recovering-and-changing-passwords-cs/_static/image5.png)](recovering-and-changing-passwords-cs/_static/image4.png)

**圖 2**：如果輸入的使用者名稱無效，就會顯示錯誤訊息（[按一下以查看完整大小的影像](recovering-and-changing-passwords-cs/_static/image6.png)）

現在輸入使用者名稱。 使用系統中帳戶的使用者名稱，以及您可以存取的電子郵件地址，以及您知道的安全性答案。 輸入使用者名稱並按一下 [提交] 之後，PasswordRecovery 控制項會顯示其問題視圖。 如同 [使用者名稱] 視圖，如果您輸入不正確的答案，PasswordRecovery 控制項會顯示錯誤訊息（請參閱 [圖 3]）。 使用 [ [`QuestionFailureText`] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx)來自訂此錯誤訊息。

[![如果使用者輸入不正確安全性答案，就會顯示錯誤訊息](recovering-and-changing-passwords-cs/_static/image8.png)](recovering-and-changing-passwords-cs/_static/image7.png)

**圖 3**：如果使用者輸入不正確安全性答案（[按一下以觀看完整大小的影像](recovering-and-changing-passwords-cs/_static/image9.png)），就會顯示錯誤訊息

最後，輸入正確的安全性答案，然後按一下 [提交]。 PasswordRecovery 控制項會在幕後產生隨機密碼、將它指派給使用者帳戶、傳送電子郵件通知使用者新密碼（請參閱 [圖 4]），然後顯示成功的視圖。

[![使用者會收到電子郵件，附有他的新密碼](recovering-and-changing-passwords-cs/_static/image11.png)](recovering-and-changing-passwords-cs/_static/image10.png)

**圖 4**：使用新密碼傳送電子郵件給使用者（[按一下以觀看完整大小的影像](recovering-and-changing-passwords-cs/_static/image12.png)）

### <a name="customizing-the-email"></a>自訂電子郵件

PasswordRecovery 控制項所傳送的預設電子郵件相當乏味（請參閱 [圖 4]）。 訊息是從 `<smtp>` 專案的 `from` 屬性中所指定的帳號，使用主體密碼和純文字主體來傳送：

請回到網站，並使用下列資訊登入。

使用者名稱： *username*

密碼：*密碼*

您可以透過 PasswordRecovery 控制項之[`SendingMail` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)的事件處理常式，或以宣告方式透過[`MailDefinition` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)自訂此訊息。 讓我們來探索這兩個選項。

`SendingMail` 事件會在電子郵件訊息傳送之前引發，而這是以程式設計方式調整電子郵件訊息的最後機會。 當引發這個事件時，事件處理常式會傳遞[`MailMessageEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx)類型的物件，其 `Message` 屬性包含要傳送之電子郵件的參考。

建立 `SendingMail` 事件的事件處理常式，並加入下列程式碼，以程式設計方式將 `webmaster@example.com` 新增至 [CC] 清單。

[!code-csharp[Main](recovering-and-changing-passwords-cs/samples/sample2.cs)]

也可以透過宣告式方式來設定電子郵件訊息。 PasswordRecovery 的 `MailDefinition` 屬性是[`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)類型的物件。 `MailDefinition` 類別提供與電子郵件相關的屬性主控制項，包括 `From`、`CC`、`Priority`、`Subject`、`IsBodyHtml`、`BodyFileName`和其他專案。 針對初學者，將[`Subject` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx)設定為比預設值（密碼）更具描述性的內容，例如您的密碼已重設 。

若要自訂電子郵件訊息的本文，我們需要建立另一個包含本文內容的電子郵件範本檔案。 首先，在名為 `EmailTemplates`的網站中建立新的資料夾。 接下來，將新的文字檔新增至此名為 `PasswordRecovery.txt` 的資料夾，並新增下列內容：

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample3.aspx)]

請注意，`<%UserName%>` 和 `<%Password%>`的預留位置用法。 PasswordRecovery 控制項會在傳送電子郵件之前，自動以使用者的使用者名稱和已復原的密碼取代這兩個預留位置。

最後，將 `MailDefinition`的[`BodyFileName` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)指向我們剛才建立的電子郵件範本（`~/EmailTemplates/PasswordRecovery.txt`）。

進行這些變更之後，請重新流覽 `RecoverPassword.aspx` 頁面，並輸入您的使用者名稱和安全性解答。 您應該會收到如 [圖 5] 所示的電子郵件。 請注意，`webmaster@example.com` 已是「抄送」，而且主旨和本文已更新。

[![[主旨]、[主體] 和 [副本] 清單已更新](recovering-and-changing-passwords-cs/_static/image14.png)](recovering-and-changing-passwords-cs/_static/image13.png)

**圖 5**： [主旨]、[主體] 和 [副本] 清單已更新（[按一下以觀看完整大小的影像](recovering-and-changing-passwords-cs/_static/image15.png)）

若要將 HTML 格式的電子郵件集傳送[`IsBodyHtml`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx)為 True （預設值為 False），並更新電子郵件範本以包含 HTML。

`MailDefinition` 屬性對 PasswordRecovery 類別而言並不是唯一的。 如我們在步驟2中所見，ChangePassword 控制項也提供 `MailDefinition` 的屬性。 此外，CreateUserWizard 控制項還包含了這類屬性，您可以將其設定為自動傳送歡迎電子郵件訊息給新使用者。

> [!NOTE]
> 左側導覽中目前沒有連結可到達 [`RecoverPassword.aspx`] 頁面。 如果使用者無法成功登入網站，則只會有興趣造訪此頁面。 因此，請更新 [`Login.aspx`] 頁面，以包含 [`RecoverPassword.aspx`] 頁面的連結。

### <a name="programmatically-resetting-a-users-password"></a>以程式設計方式重設使用者的密碼

重設使用者的密碼時，PasswordRecovery 控制項會呼叫 `MembershipUser` 物件的[`ResetPassword` 方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)。 這個方法有兩個多載：

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** 重設使用者的密碼。 如果 `RequiresQuestionAndAnswer` 為 False，請使用此多載。
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -只有當提供的*securityAnswer*正確時，才重設使用者的密碼。 如果 `RequiresQuestionAndAnswer` 為 True，則使用此多載。

這兩個多載會傳回隨機產生的新密碼。

如同成員資格架構中的其他方法，`ResetPassword` 方法會委派至已設定的提供者。 `SqlMembershipProvider` 會叫用 `aspnet_Membership_ResetPassword` 預存程式，傳入使用者的使用者名稱、新密碼和提供的密碼解答，還有其他欄位。 預存程式可確保密碼答案符合，然後更新使用者的密碼。

一些低層級的執行附注：

- 已鎖定的使用者無法重設密碼。 不過，未經核准的使用者可能會。 我們將在解除鎖定和核准<a id="_msoanchor_3"> </a>[*使用者*](unlocking-and-approving-user-accounts-cs.md)帳戶教學課程中更詳細地討論已鎖定和已核准的狀態。
- 如果密碼答案不正確，使用者的失敗密碼解答嘗試計數會遞增。 如果在指定的時間範圍內發生指定的無效安全性答案嘗試次數，使用者就會被鎖定。

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>如何產生隨機密碼的單字

以 [圖 4] 和 [5] 中的電子郵件訊息顯示的隨機產生密碼，是由成員資格類別的[`GeneratePassword` 方法](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)所建立。 這個方法會接受兩個整數輸入參數-*長度*和*numberOfNonAlphanumericCharacters* ，並以至少*numberOfNonAlphanumericCharacters*的非英數位元數目，傳回*長度*至少為個字元的字串。 從成員資格類別或登入相關的 Web 控制項呼叫這個方法時，這兩個參數的值是由成員資格設定的 `MinRequiredPasswordLength` 和 `MinRequiredNonalphanumericCharacters` 屬性所決定，分別為7和1。

`GeneratePassword` 方法會使用密碼編譯增強式亂數產生器，以確保選取的隨機字元不會有任何偏差。 此外，`GeneratePassword` 是 `public`的，這表示如果您需要產生隨機字串或密碼，就可以直接從 ASP.NET 應用程式使用它。

> [!NOTE]
> `SqlMembershipProvider` 類別一律會產生長度至少為14個字元的隨機密碼，因此，如果 `MinRequiredPasswordLength` 小於14，則會忽略其值。

## <a name="step-2-changing-passwords"></a>步驟2：變更密碼

隨機產生的密碼很容易記住。 請考慮 [圖4： `WWGUZv(f2yM:Bd`] 中顯示的密碼。 請嘗試將它認可到記憶體！ 不用說，在使用者傳送此類隨機產生的密碼之後，她會想要將密碼變更為較容易記住的密碼。

您可以使用 ChangePassword 控制項來建立介面，讓使用者變更其密碼。 ChangePassword 控制項與 PasswordRecovery 控制項非常類似，它包含兩個觀點：變更密碼和成功。 [變更密碼] 視圖會提示使用者提供舊密碼和新密碼。 當提供正確的舊密碼和符合最小長度和非英數位元需求的新密碼時，ChangePassword 控制項會更新使用者的密碼，並顯示成功的視圖。

> [!NOTE]
> ChangePassword 控制項會藉由叫用 `MembershipUser` 物件的[`ChangePassword` 方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)來修改使用者的密碼。 ChangePassword 方法會接受兩個 `string` 輸入參數- *oldPassword*和*newPassword*，並使用*newPassword*更新使用者的帳戶，假設提供的*oldPassword*是正確的。

開啟 [`ChangePassword.aspx`] 頁面，並將 [ChangePassword] 控制項新增至頁面，並將其命名為 `ChangePwd`。 此時，設計檢視應該會顯示 [變更密碼] 視圖（請參閱 [圖 6]）。 如同 PasswordRecovery 控制項，您可以透過控制項的智慧標籤切換 views。 此外，這些視圖的外觀也可以透過各種樣式屬性來自訂，或將它們轉換成範本。

[![將 ChangePassword 控制項新增至頁面](recovering-and-changing-passwords-cs/_static/image17.png)](recovering-and-changing-passwords-cs/_static/image16.png)

**圖 6**：將 ChangePassword 控制項新增至頁面（[按一下以查看完整大小的影像](recovering-and-changing-passwords-cs/_static/image18.png)）

ChangePassword 控制項可以更新目前登入的使用者密碼，*或*另一個指定使用者的密碼。 如 [圖 6] 所示，預設的 [變更密碼] 視圖只會轉譯三個 TextBox 控制項：一個用於舊密碼，另兩個用於新密碼。 這個預設介面是用來更新目前登入的使用者密碼。

若要使用 ChangePassword 控制項來更新其他使用者的密碼，請將控制項的[`DisplayUserName` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx)設定為 True。 這麼做會在頁面中新增第四個文字方塊，提示您輸入要變更其密碼的使用者名稱。

如果您想讓已登出的使用者變更密碼而不需要登入，將 `DisplayUserName` 設定為 True 會很有用。 我個人認為，要求使用者登入並不會有任何問題，讓她能夠變更密碼。 因此，請將 `DisplayUserName` 設為 False （預設值）。 不過，在進行這項決策時，我們基本上會禁止匿名使用者到達此頁面。 更新網站的 URL 授權規則，以便拒絕匿名使用者造訪 `ChangePassword.aspx`。 如果您需要在 URL 授權規則語法上重新整理記憶體，請回頭參閱以<a id="_msoanchor_4"> </a>[*使用者為基礎的授權*](../membership/user-based-authorization-cs.md)教學課程。

> [!NOTE]
> `DisplayUserName` 屬性似乎可以讓系統管理員變更其他使用者的密碼。 不過，即使 `DisplayUserName` 設定為 True，也必須知道正確的舊密碼並加以輸入。 我們會討論可讓系統管理員在步驟3中變更使用者密碼的技術。

請造訪瀏覽器的 `ChangePassword.aspx` 頁面並變更您的密碼。 請注意，如果您輸入的新密碼無法符合成員資格設定中所指定的密碼長度和非英數位元需求，就會顯示錯誤訊息（請參閱 [圖 7]）。

[![將 ChangePassword 控制項新增至頁面](recovering-and-changing-passwords-cs/_static/image20.png)](recovering-and-changing-passwords-cs/_static/image19.png)

**圖 7**：將 ChangePassword 控制項新增至頁面（[按一下以查看完整大小的影像](recovering-and-changing-passwords-cs/_static/image21.png)）

在輸入正確的舊密碼和有效的新密碼時，會變更登入的使用者密碼，並顯示成功的視圖。

### <a name="sending-a-confirmation-email"></a>傳送確認電子郵件

根據預設，[ChangePassword] 控制項不會傳送電子郵件訊息給剛更新其密碼的使用者。 如果您想要傳送電子郵件，只需設定控制項的 `MailDefinition` 屬性。 讓我們設定 [ChangePassword] 控制項，以便將包含新密碼的 HTML 格式電子郵件傳送給使用者。

首先，在名為 `ChangePassword.htm`的 `EmailTemplates` 資料夾中建立新檔案。 新增下列標記：

[!code-html[Main](recovering-and-changing-passwords-cs/samples/sample4.html)]

接下來，將 ChangePassword 控制項的 `MailDefinition` 屬性的 `BodyFileName`、`IsBodyHtml`和 `Subject` 屬性設定為 ~/EmailTemplates/ChangePassword.htm、True，且您的密碼已分別變更為！。

進行這些變更之後，再次流覽頁面並變更您的密碼。 這次，ChangePassword 控制項會將自訂的 HTML 格式電子郵件傳送至使用者在檔案上的電子郵件地址（請參閱 [圖 8]）。

[![電子郵件訊息，通知使用者他們的密碼已變更](recovering-and-changing-passwords-cs/_static/image23.png)](recovering-and-changing-passwords-cs/_static/image22.png)

**圖 8**：電子郵件訊息通知使用者他們的密碼已變更（[按一下以觀看完整大小的影像](recovering-and-changing-passwords-cs/_static/image24.png)）

## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>步驟3：允許系統管理員變更使用者的密碼

在支援使用者帳戶的應用程式中，常見的功能是系統管理使用者變更其他使用者密碼的能力。 有時候這是必要的功能，因為系統無法讓使用者變更自己的密碼。 在這種情況下，使用者復原忘記密碼的唯一方式，就是讓系統管理員為他們指派新密碼。 不過，使用 PasswordRecovery 和 ChangePassword 控制項時，系統管理使用者不需要在變更使用者密碼的情況下自行運作，因為使用者可以自行執行此動作。

但如果您的用戶端堅持該系統管理使用者應該能夠變更其他使用者的密碼，該怎麼辦？ 可惜的是，加入這項功能可能會有一些工作。 若要變更使用者的密碼，必須提供新舊密碼給 `MembershipUser` 物件的 `ChangePassword` 方法，但系統管理員不應該知道使用者的密碼，就能修改它。

其中一個因應措施是先重設使用者的密碼，然後使用如下所示的程式碼，將它變更為新密碼：

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample5.aspx)]

此程式碼一開始會抓取使用者*名稱*的相關資訊，也就是系統管理員想要變更其密碼的使用者。 接下來，會叫用 `ResetPassword` 方法，這會為使用者指派新的隨機密碼。 這個隨機產生的密碼是由方法傳回，並儲存在 `resetPwd`變數中。 知道使用者的密碼之後，就可以透過對 `ChangePassword`的呼叫來變更它。

問題在於，此程式碼只有在設定成員資格系統組態時才有效，因此 `RequiresQuestionAndAnswer` 為 False。 如果 `RequiresQuestionAndAnswer` 為 True，與我們的應用程式相同，則必須將 `ResetPassword` 方法傳遞至安全性答案，否則會擲回例外狀況。

如果將成員資格架構設定為需要安全性問題和答案，但您的用戶端堅持系統管理員能夠變更使用者的密碼，您有三個選項：

- 將您的手放在空中，告訴您的用戶端，這只是無法完成的一件事。
- 將 `RequiresQuestionAndAnswer` 設定為 False。 這會導致較不安全的應用程式。 想像一下，惡意使用者已取得另一位使用者電子郵件收件匣的存取權。 可能是遭入侵的使用者離開了午餐，而未鎖定工作站，或是他們從公用終端機存取他們的電子郵件，而未登出。不論是哪一種情況，惡意使用者都可以造訪 [`RecoverPassword.aspx`] 頁面，並輸入使用者的使用者名稱。 系統接著會以電子郵件傳送已復原的密碼，而不會提示您輸入安全性答案。
- 略過成員資格架構所建立的抽象層，並直接使用 SQL Server 資料庫。 成員資格架構包含名為 `aspnet_Membership_SetPassword` 的預存程式，其會設定使用者的密碼，而且不需要安全性答案或舊密碼，即可完成其工作。

這些選項都不是特別吸引人，但這就是開發人員有時候的生命週期。

我已經開始執行第三個方法，撰寫程式碼來略過 `Membership` 並 `MembershipUser` 類別，並直接針對 `SecurityTutorials` 資料庫操作。

> [!NOTE]
> 藉由直接使用資料庫，成員資格架構所提供的封裝會被破碎。 這種決策會將我們與 `SqlMembershipProvider`結合，使程式碼的可攜性較低。 此外，如果成員資格架構變更，此程式碼可能無法在未來版本的 ASP.NET 中如預期般運作。 這種方法是一個因應措施，如同大部分的因應措施，並不是最佳作法的範例。

程式碼有一些不討喜位，而且相當冗長。 因此，我不想要對此教學課程進行深入的檢查。 如果您有興趣深入瞭解，請下載本教學課程的程式碼，並造訪 `~/Administration/ManageUsers.aspx` 頁面。 我們在<a id="_msoanchor_5"> </a>[前一個教學](building-an-interface-to-select-one-user-account-from-many-cs.md)課程中建立的這個頁面會列出每個使用者。 我已更新 GridView 以包含 `UserInformation.aspx` 頁面的連結，並透過 querystring 傳遞所選使用者的使用者名稱。 [`UserInformation.aspx`] 頁面會顯示所選使用者的相關資訊，以及變更其密碼的文字方塊（請參閱 [圖 9]）。

輸入新密碼之後，在第二個文字方塊中確認，然後按一下 [更新使用者] 按鈕，就會叫用回傳接踵而來和 `aspnet_Membership_SetPassword` 預存程式，並更新使用者的密碼。 我鼓勵那些對這項功能感興趣的讀者更熟悉程式碼，並嘗試擴充功能以包含傳送電子郵件給密碼已變更的使用者。

[![系統管理員可以變更使用者的密碼](recovering-and-changing-passwords-cs/_static/image26.png)](recovering-and-changing-passwords-cs/_static/image25.png)

**圖 9**：系統管理員可以變更使用者的密碼（[按一下以觀看完整大小的影像](recovering-and-changing-passwords-cs/_static/image27.png)）

> [!NOTE]
> 目前只有在成員資格架構設定為以純文字或雜湊格式儲存密碼時，[`UserInformation.aspx`] 頁面才有作用。 雖然您已獲邀加入此功能，但它缺少加密新密碼的程式碼。 我建議新增必要程式碼的方式，是使用解編程式（例如[反映](http://www.aisto.com/roeder/dotnet/)程式）來檢查 .NET Framework 中方法的原始程式碼;從檢查 `SqlMembershipProvider` 類別的 `ChangePassword` 方法開始。 這是我用來撰寫程式碼來建立密碼雜湊的技巧。

## <a name="summary"></a>總結

ASP.NET 提供兩個可協助使用者管理其密碼的控制項。 PasswordRecovery 控制項對忘記其密碼的人來說非常有用。 視成員資格架構的設定而定，使用者可以透過電子郵件傳送其現有的密碼或隨機產生的新密碼。 ChangePassword 控制項可讓使用者更新其密碼。

就像 Login 和 CreateUserWizard 控制項一樣，PasswordRecovery 和 ChangePassword 控制項會呈現豐富的使用者介面，而不需要撰寫宣告式標記或程式程式碼的舔。 如果預設使用者介面不符合您的需求，您可以透過各種樣式屬性來自訂它。 或者，控制項的介面也可以轉換成樣板，以獲得更精細的控制程度。 這些控制項會在幕後使用成員資格 API，叫用 `MembershipUser` 物件的 `ResetPassword` 和 `ChangePassword` 方法。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ChangePassword 控制項快速入門](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery 控制項快速入門](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [在 ASP.NET 中傳送電子郵件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` 常見問題](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者包括 Michael Emmings 和 Suchi Banerjee。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](building-an-interface-to-select-one-user-account-from-many-cs.md)
> [下一頁](unlocking-and-approving-user-accounts-cs.md)
