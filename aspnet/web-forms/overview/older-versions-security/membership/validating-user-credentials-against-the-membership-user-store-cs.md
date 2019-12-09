---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: 針對成員資格使用者存放區驗證使用者認證C#（） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何使用程式設計方式和登入控制項，針對成員資格使用者存放區驗證使用者的認證 ...。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: aaf6df6f52253ef0f7369a7e77211b6786b97db1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618167"
---
# <a name="validating-user-credentials-against-the-membership-user-store-c"></a>針對成員資格使用者存放區驗證使用者認證 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip)或[下載 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> 在本教學課程中，我們將探討如何使用程式設計方式和登入控制項，針對成員資格使用者存放區驗證使用者的認證。 我們也將探討如何自訂登入控制項的外觀和行為。

## <a name="introduction"></a>簡介

在<a id="Tutorial05"> </a>[先前的教學](creating-user-accounts-cs.md)課程中，我們探討了如何在成員資格架構中建立新的使用者帳戶。 我們先探討了如何透過 `Membership` 類別的 `CreateUser` 方法以程式設計方式建立使用者帳戶，然後使用 CreateUserWizard Web 控制項進行檢查。 不過，登入頁面目前會針對使用者名稱和密碼配對的硬式編碼清單，驗證提供的認證。 我們需要更新登入頁面的邏輯，讓它能夠根據成員資格架構的使用者存放區驗證認證。

就像建立使用者帳戶一樣，認證可以透過程式設計或宣告方式進行驗證。 成員資格 API 包含一個方法，可讓您以程式設計方式向使用者存放區驗證使用者的認證。 和 ASP.NET 隨附于登入 Web 控制項，它會轉譯使用者介面，其中包含使用者名稱和密碼的文字方塊，以及用來登入的按鈕。

在本教學課程中，我們將探討如何使用程式設計方式和登入控制項，針對成員資格使用者存放區驗證使用者的認證。 我們也將探討如何自訂登入控制項的外觀和行為。 讓我們開始吧！

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>步驟1：根據成員資格使用者存放區驗證認證

若是使用表單驗證的網站，使用者可以透過造訪登入頁面並輸入其認證來登入網站。 然後，這些認證會與使用者存放區進行比較。 如果有效，則使用者會被授與表單驗證票證，這是一種安全性權杖，表示訪客的身分識別和真實性。

若要針對成員資格架構驗證使用者，請使用 `Membership` 類別的[`ValidateUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)。 `ValidateUser` 方法會接受兩個輸入參數- *`username`* 和 *`password`* ，並傳回布林值，指出認證是否有效。 就像我們在上一個教學課程中所檢查的 `CreateUser` 方法一樣，`ValidateUser` 方法會將實際的驗證委派給設定的成員資格提供者。

`SqlMembershipProvider` 藉由透過 `aspnet_Membership_GetPasswordWithFormat` 預存程式取得指定使用者的密碼，來驗證提供的認證。 回想一下，`SqlMembershipProvider` 使用下列三種格式的其中一種來儲存使用者的密碼：清除、加密或雜湊。 `aspnet_Membership_GetPasswordWithFormat` 預存程式會以其原始格式傳回密碼。 對於加密或雜湊的密碼，`SqlMembershipProvider` 會將傳入 `ValidateUser` 方法的 *`password`* 值轉換為其對等的加密或雜湊狀態，然後將它與從資料庫傳回的內容進行比較。 如果儲存在資料庫中的密碼符合使用者輸入的格式化密碼，則認證會是有效的。

讓我們更新登入頁面（~/`Login.aspx`），使其根據成員資格架構使用者存放區驗證提供的認證。 我們<a id="Tutorial02"> </a>[*已在表單驗*](../introduction/an-overview-of-forms-authentication-cs.md)證教學課程的總覽中建立此登入頁面，建立具有兩個文字方塊的使用者名稱和密碼、[記住我] 核取方塊和 [登入] 按鈕的介面（請參閱 [圖 1]）。 此程式碼會針對使用者名稱和密碼配對的硬式編碼清單（Scott/password、Jisun/password 和 Sam/password）來驗證輸入的認證。 <a id="Tutorial03"></a>在[*表單驗證設定和 Advanced 主題*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教學課程中，我們更新了登入頁面的程式碼，以在表單驗證票證的 `UserData` 屬性中儲存其他資訊。

[![登入頁面的介面包含兩個文字方塊、一個 CheckBoxList 和一個按鈕](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**圖 1**：登入頁面的介面包含兩個文字方塊、一個 CheckBoxList 和一個按鈕（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png)）

登入頁面的使用者介面可以維持不變，但我們需要將登入按鈕的 `Click` 事件處理常式，取代為驗證使用者對成員資格架構使用者存放區的程式碼。 更新事件處理常式，使其程式碼看起來如下：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

這段程式碼很簡單。 我們一開始會先呼叫 `Membership.ValidateUser` 方法，傳入提供的使用者名稱和密碼。 如果該方法傳回 true，則會透過 `FormsAuthentication` 類別的 RedirectFromLoginPage 方法，將使用者登入網站。 （如我們在<a id="Tutorial2"> </a>[*表單驗*](../introduction/an-overview-of-forms-authentication-cs.md)證教學課程中所討論，`FormsAuthentication.RedirectFromLoginPage` 會建立表單驗證票證，然後將使用者重新導向至適當的頁面）。不過，如果認證無效，則會顯示 [`InvalidCredentialsMessage`] 標籤，通知使用者他們的使用者名稱或密碼不正確。

這樣就全部完成了！

若要測試登入頁面是否如預期般運作，請嘗試使用您在上一個教學課程中建立的其中一個使用者帳戶來登入。 或者，如果您尚未建立帳戶，請繼續並從 [`~/Membership/CreatingUserAccounts.aspx`] 頁面建立一個。

> [!NOTE]
> 當使用者輸入自己的認證並提交登入頁面表單時，會透過網際網路將認證（包括她的密碼）以*純文字*格式傳送至 web 伺服器。 這表示任何駭客探查網路流量都可以看到使用者名稱和密碼。 若要避免這種情況，請務必使用[安全通訊端層（SSL）](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)來加密網路流量。 這可確保在網頁伺服器收到認證（以及整個網頁的 HTML 標籤）後，就會將它們從離開瀏覽器的時間加密。

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>成員資格架構如何處理不正確登入嘗試

當造訪者到達登入頁面並提交其認證時，其瀏覽器會對登入頁面提出 HTTP 要求。 如果認證有效，HTTP 回應會在 cookie 中包含驗證票證。 因此，嘗試侵入您的網站的駭客可能會建立一個程式，將 HTTP 要求以有效的使用者名稱和猜測的密碼，徹底地傳送到登入頁面。 如果密碼猜測正確，登入頁面將會傳回驗證票證 cookie，此時程式會知道它是否已偶然發現有效的使用者名稱/密碼組。 透過暴力密碼破解，這類程式或許能夠遇到使用者的密碼，特別是如果密碼很弱。

為避免這類暴力密碼破解攻擊，如果在一段時間內有一定數目的失敗登入嘗試，成員資格架構就會鎖定使用者。 確切的參數可透過下列兩個成員資格提供者設定設定來設定：

- `maxInvalidPasswordAttempts`-指定在帳戶被鎖定之前，使用者允許的無效密碼嘗試次數。預設值為5。
- `passwordAttemptWindow`-指出指定的無效登入嘗試次數將導致帳戶遭到鎖定的時間間隔（以分鐘為單位）。預設值為10。

如果使用者遭到鎖定，則在系統管理員解除鎖定其帳戶之前，她無法登入。 當使用者遭到鎖定時，即使提供有效的認證，`ValidateUser` 方法*一律*會傳回 `false`。 雖然此行為可降低駭客透過暴力密碼破解方式侵入網站的可能性，但最終會鎖定只是忘記密碼的有效使用者，或不小心有 CAPS LOCK 或有不正確的輸入日期。

可惜的是，沒有任何內建工具可解除鎖定使用者帳戶。 若要解除鎖定帳戶，您可以直接修改資料庫-針對適當的使用者帳戶變更 `aspnet_Membership` 資料表中的 [`IsLockedOut`] 欄位，或建立 web 型介面，其中列出已鎖定的帳戶，並具有可解除鎖定的選項。 我們將在未來的教學課程中，檢查建立系統管理介面來完成一般使用者帳戶和角色相關的工作。

> [!NOTE]
> `ValidateUser` 方法的其中一個缺點是，當提供的認證無效時，不會提供任何說明。 認證可能無效，因為使用者存放區中沒有相符的使用者名稱/密碼組，或是使用者尚未核准，或使用者已被鎖定。在步驟4中，我們將瞭解如何在登入嘗試失敗時，向使用者顯示更詳細的訊息。

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>步驟2：透過登入 Web 控制項收集認證

[登入 Web 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)呈現的預設使用者介面，與我們在<a id="SKM5"> </a>[*表單驗*](../introduction/an-overview-of-forms-authentication-cs.md)證教學課程的總覽中所建立的介面非常類似。 使用登入控制項可讓我們完成建立介面以收集訪客認證的工作。 此外，登入控制項會自動登入使用者（假設提交的認證是有效的），因此讓我們不必撰寫任何程式碼。

讓我們更新 `Login.aspx`，將手動建立的介面和程式碼取代為登入控制項。 從移除 `Login.aspx`中現有的標記和程式碼開始。 您可以直接將其刪除，或只將其批註。若要將宣告式標記批註，請使用 `<%--` 和 `--%>` 分隔符號將它括住。 您可以手動輸入這些分隔符號，或如 [圖 2] 所示，您可以選取要加上批註的文字，然後按一下工具列中的 [批註掉選取的行] 圖示。 同樣地，您可以使用 [批註] [選取的行] 圖示，將程式碼後置類別中選取的程式碼標記為批註。

[![將登入 .aspx 中現有的宣告式標記和原始程式碼批註](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**圖 2**：批註 `Login.aspx` 中現有的宣告式標記和原始程式碼（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png)）

> [!NOTE]
> 在 Visual Studio 2005 中觀看宣告式標記時，無法使用 [批註外的選取行] 圖示。 如果您不是使用 Visual Studio 2008，就必須手動新增 `<%--` 和 `--%>` 分隔符號。

接下來，將登入控制項從 [工具箱] 拖曳至頁面，並將其 [`ID`] 屬性設定為 [`myLogin`]。 此時，您的畫面看起來應該像 [圖 3]。 請注意，登入控制項的預設介面包含 [使用者名稱] 和 [密碼] 的 TextBox 控制項、[下次提醒我] 核取方塊和 [登入] 按鈕。 也有兩個文字方塊的 `RequiredFieldValidator` 控制項。

[![將登入控制項新增至頁面](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**圖 3**：將登入控制項新增至頁面（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png)）

我們已經完成了！ 按一下 [登入] 控制項的 [登入] 按鈕時，將會發生回傳，而登入控制項將會呼叫 `Membership.ValidateUser` 方法，傳入輸入的使用者名稱和密碼。 如果認證無效，登入控制項會顯示一則訊息，說明這種情況。 不過，如果認證有效，則登入控制項會建立表單驗證票證，並將使用者重新導向至適當的頁面。

登入控制項會使用四個因素來決定適當的頁面，以便在成功登入時將使用者重新導向至：

- 登入控制項是否位於 [表單驗證設定] 中的 `loginUrl` 設定所定義的登入頁面上;此設定的預設值為 `Login.aspx`
- `ReturnUrl` querystring 參數是否存在
- 登入控制項的[`DestinationUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)值
- [表單驗證設定] 中指定的 `defaultUrl` 值;此設定的預設值為 `Default.aspx`

[圖 4] 說明登入控制項如何使用這四個參數來達到適當的頁面決策。

[![將登入控制項新增至頁面](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**圖 4**：將登入控制項新增至頁面（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png)）

請花點時間透過瀏覽器造訪網站，並在成員資格架構中以現有的使用者身分登入，以測試登入控制項。

登入控制項的轉譯介面是可高度設定的。 有一些屬性會影響其外觀;還有什麼，登入控制項可以轉換成樣板，以精確控制使用者介面專案的版面配置。 此步驟的其餘部分會檢查如何自訂外觀和版面配置。

### <a name="customizing-the-login-controls-appearance"></a>自訂登入控制項的外觀

登入控制項的預設屬性設定會轉譯使用者介面，其中具有標題（登入）、TextBox 和標籤控制項，用於使用者名稱和密碼輸入、[下次提醒我] 核取方塊和 [登入] 按鈕。 這些元素的外觀都可以透過登入控制項的許多屬性來設定。 此外，您可以藉由設定屬性或兩個來新增其他使用者介面專案（例如，建立新使用者帳戶的頁面連結）。

讓我們花幾分鐘的時間來 gussy 登入控制項的外觀。 因為 [`Login.aspx`] 頁面已在頁面頂端顯示 [登入]，所以登入控制項的標題是多餘的。 因此，請清除[`TitleText` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx)值，以便移除登入控制項的標題。

您可以分別透過 [ [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) ] 和 [ [`PasswordLabelText` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)]，自訂兩個 TextBox 控制項左邊的 [使用者名稱：] 和 [密碼：] 標籤。 讓我們將 [使用者名稱：] 標籤變更為 [讀取 Username：]。 [標籤] 和 [TextBox] 樣式可分別透過 [ [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) ] 和 [ [`TextBoxStyle`] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)來設定。

[下次提醒我] 核取方塊的 [Text] 屬性可以透過登入控制項的[`RememberMeText property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx)來設定，而其預設的核取狀態則可透過[`RememberMeSet property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) （預設為 False）來設定。 請繼續並將 `RememberMeSet` 屬性設為 True，如此一來，預設會核取 [記住我下一個時間] 核取方塊。

登入控制項提供兩個屬性來調整其使用者介面控制項的版面配置。 [`TextLayout property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx)指出使用者名稱：和密碼：標籤出現在其對應的文字方塊左邊（預設值）或上方。 [`Orientation property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx)指出使用者名稱和密碼輸入是以垂直方式放在同一個上方，還是以水準方式放置。 我要將這兩個屬性設為預設值，但我建議您嘗試將這兩個屬性設定為非預設值，以查看產生的效果。

> [!NOTE]
> 在下一節設定登入控制項的版面配置時，我們將探討如何使用範本來定義版面配置控制項的使用者介面元素的精確配置。

將 [ [`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) ] 和 [ [`CreateUserUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx)] 設定為 [尚未註冊]，以將登入控制項的屬性設定加以包裝？ 建立帳戶！ 和會分別 `~/Membership/CreatingUserAccounts.aspx`。 這會將超連結新增至登入控制項的介面，指向我們在<a id="SKM6"> </a>[上一個教學](creating-user-accounts-cs.md)課程中建立的頁面。 登入控制項的[`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx)和[`HelpPageUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx)，以及[`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx)和[`PasswordRecoveryUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx)會以相同的方式工作，也就是將連結轉譯成說明頁和密碼修復頁面。

進行這些屬性變更之後，您的登入控制項的宣告式標記和外觀看起來應該像 [圖 5] 所示。

[![登入控制項的屬性值決定其外觀](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**圖 5**：登入控制項的屬性值會決定其外觀（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png)）

### <a name="configuring-the-login-controls-layout"></a>設定登入控制項的版面配置

登入 Web 控制項的預設使用者介面會在 HTML `<table>`中配置介面。 但如果我們需要更精確地控制轉譯的輸出，該怎麼辦？ 也許我們想要以一系列的 `<div>` 標記來取代 `<table>`。 或者，如果我們的應用程式需要其他認證來進行驗證，該怎麼做？ 比方說，許多財務網站都需要使用者不僅提供使用者名稱和密碼，也可以提供個人識別碼（PIN）或其他識別資訊。 不論原因為何，您都可以將登入控制項轉換成範本，以便明確定義介面的宣告式標記。

我們需要做兩件事，才能更新登入控制項以收集其他認證：

1. 更新登入控制項的介面，以包含用來收集其他認證的 Web 控制項。
2. 覆寫登入控制項的內部驗證邏輯，如此一來，使用者只有在其使用者名稱和密碼有效，而且其其他認證也有效時，才會進行驗證。

若要完成第一個工作，我們必須將登入控制項轉換為範本，並加入必要的 Web 控制項。 就第二個工作而言，登入控制項的驗證邏輯可以藉由建立控制項的[`Authenticate` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)的事件處理常式來取代。

讓我們更新登入控制項，使其提示使用者輸入使用者名稱、密碼和電子郵件地址，並且只在提供的電子郵件地址與檔案上的電子郵件地址相符時，才驗證使用者。 我們必須先將登入控制項的介面轉換為範本。 從登入控制項的智慧標籤中，選擇 [轉換成範本] 選項。

[![將登入控制項轉換為範本](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**圖 6**：將登入控制項轉換為範本（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png)）

> [!NOTE]
> 若要將登入控制項還原為其預先範本版本，請按一下控制項智慧標籤中的 [重設] 連結。

將登入控制項轉換為範本，會使用 HTML 專案和 Web 控制項定義使用者介面，將 `LayoutTemplate` 加入控制項的宣告式標記中。 如 [圖 7] 所示，將控制項轉換為範本會從屬性視窗中移除一些屬性，例如 `TitleText`、`CreateUserUrl`等等，因為在使用範本時，會忽略這些屬性值。

[當登入控制項轉換成範本時，可以使用 ![較少的屬性](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**圖 7**：當登入控制項轉換成範本時，可以使用較少的屬性（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png)）

`LayoutTemplate` 中的 HTML 標籤可能會視需要修改。 同樣地，您也可以隨意將任何新的 Web 控制項加入至範本。 不過，登入控制項的核心 Web 控制項必須保留在範本中，並保留其指派的 `ID` 值，這點很重要。 特別的是，請勿移除或重新命名 [`UserName`] 或 [`Password` 文字方塊]、[`RememberMe`] 核取方塊、[`LoginButton`] 按鈕、[`FailureText`] 標籤或 [`RequiredFieldValidator`] 控制項。

若要收集訪客的電子郵件地址，我們必須將 TextBox 新增至範本。 在包含 [`Password`] 文字方塊的資料表資料列（`<tr>`）與保留 [下次提醒我] 核取方塊的資料表資料列之間，加入下列宣告式標記：

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

新增 [`Email`] 文字方塊之後，請透過瀏覽器造訪頁面。 如 [圖 8] 所示，登入控制項的使用者介面現在包含第三個文字方塊。

[![登入控制項現在包含使用者電子郵件地址的 Textbox](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**圖 8**：登入控制項現在包含使用者電子郵件地址的文字方塊（[按一下以觀看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png)）

此時，登入控制項仍會使用 `Membership.ValidateUser` 方法來驗證提供的認證。 同樣地，在 [`Email`] 文字方塊中輸入的值，與使用者是否可以登入無關。 在步驟3中，我們將探討如何覆寫登入控制項的驗證邏輯，讓認證只有在使用者名稱和密碼有效，而且提供的電子郵件地址與檔案上的電子郵件地址相符時才會被視為有效。

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>步驟3：修改登入控制項的驗證邏輯

當造訪者提供自己的認證，並按一下 [登入] 按鈕時，回傳接踵而來和 Login 控制項會在其驗證工作流程中進行。 工作流程一開始會引發[`LoggingIn` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)。 任何與此事件相關聯的事件處理常式，都可以藉由將 `e.Cancel` 屬性設定為 `true`來取消登入作業。

如果未取消登入作業，工作流程會藉由引發[`Authenticate` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)來進行。 如果 `Authenticate` 事件有事件處理常式，則它會負責判斷提供的認證是否有效。 如果未指定任何事件處理常式，登入控制項會使用 `Membership.ValidateUser` 方法來判斷認證的有效性。

如果提供的認證有效，則會建立表單驗證票證、引發[`LoggedIn` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx)，並將使用者重新導向至適當的頁面。 不過，如果認證被視為無效，則會引發[`LoginError` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx)並顯示訊息，通知使用者其認證無效。 根據預設，在失敗時，登入控制項只會將其 `FailureText` 標籤控制項的 Text 屬性設定為失敗訊息（您的登入嘗試不會成功。 請再試一次。 不過，如果登入控制項的[`FailureAction` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx)設定為 `RedirectToLoginPage`，則登入控制項會發出 `Response.Redirect` 至登入頁面，附加 querystring 參數 `loginfailure=1` （這會導致登入控制項顯示失敗訊息）。

[圖 9] 提供驗證工作流程的流程圖。

[![登入控制項的驗證工作流程](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**圖 9**：登入控制項的驗證工作流程（[按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png)）

> [!NOTE]
> 如果您想要使用 `FailureAction`的 [`RedirectToLogin` 頁面] 選項，請考慮下列案例。 現在，我們的 `Site.master` 主版頁面目前在由匿名使用者流覽時，會在左欄中顯示文字 Hello，stranger，但假設我們想要以登入控制項取代該文字。 這可讓匿名使用者從網站上的任何頁面登入，而不需要直接流覽登入頁面。 不過，如果使用者無法透過主版頁面所轉譯的登入控制項登入，則將它們重新導向至登入頁面（`Login.aspx`）可能會有意義，因為該頁面可能包含其他指示、連結和其他說明（例如，建立新帳戶或抓取遺失密碼的連結）未新增至主版頁面。

### <a name="creating-theauthenticateevent-handler"></a>建立`Authenticate`事件處理常式

為了插入我們的自訂驗證邏輯，我們必須為登入控制項的 `Authenticate` 事件建立事件處理常式。 建立 `Authenticate` 事件的事件處理常式將會產生下列事件處理常式定義：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

如您所見，`Authenticate` 事件處理常式會傳遞[`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx)類型的物件做為第二個輸入參數。 `AuthenticateEventArgs` 類別包含名為 `Authenticated` 的布林值屬性，可用來指定提供的認證是否有效。 然後，我們的工作是在此撰寫程式碼，以判斷提供的認證是否有效，並據以設定 `e.Authenticate` 屬性。

### <a name="determining-and-validating-the-supplied-credentials"></a>判斷和驗證提供的認證

使用登入控制項的[`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) ，並[`Password` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx)來決定使用者輸入的使用者名稱和密碼認證。 為了判斷輸入至任何其他 Web 控制項的值（例如我們在上一個步驟中新增的 [`Email`] 文字方塊），請使用 *`LoginControlID`* `.FindControl`（" *`controlID`* "）來取得範本中 Web 控制項的程式設計參考，其 `ID` 屬性等於 *`controlID`* 。 例如，若要取得 `Email` 文字方塊的參考，請使用下列程式碼：

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

為了驗證使用者的認證，我們必須做兩件事：

1. 確定提供的使用者名稱和密碼有效
2. 請確定輸入的電子郵件地址符合嘗試登入之使用者的電子郵件地址

若要完成第一次檢查，我們可以直接使用 `Membership.ValidateUser` 方法，如我們在步驟1中所見。 針對第二個檢查，我們必須判斷使用者的電子郵件地址，讓我們可以將它與輸入 TextBox 控制項的電子郵件地址進行比較。 若要取得特定使用者的相關資訊，請使用 `Membership` 類別的[`GetUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)。

`GetUser` 方法有許多多載。 如果在不傳入任何參數的情況下使用，它會傳回目前登入之使用者的相關資訊。 若要取得特定使用者的相關資訊，請呼叫 `GetUser` 傳入其使用者名稱。 不論是哪一種方式，`GetUser` 都會傳回[`MembershipUser` 物件](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)，其中包含 `UserName`、`Email`、`IsApproved`、`IsOnline`等等的屬性。

下列程式碼會實行這兩項檢查。 如果兩者都通過，則 `e.Authenticate` 會設定為 `true`，否則會指派 `false`。

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

將此程式碼備妥之後，請嘗試以有效的使用者身分登入，並輸入正確的使用者名稱、密碼和電子郵件地址。 請重試，但這次特意使用不正確的電子郵件地址（請參閱 [圖 10]）。 最後，使用不存在的使用者名稱嘗試第三次。 在第一個案例中，您應該成功登入網站，但在最後兩個案例中，您應該會看到登入控制項的無效認證訊息。

[當提供不正確的電子郵件地址時，![Tito 無法登入](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**圖 10**：當提供不正確的電子郵件地址時，Tito 無法登入（[按一下以觀看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png)）

> [!NOTE]
> 如步驟1中的成員資格架構如何處理不正確登入嘗試一節中所述，當呼叫 `Membership.ValidateUser` 方法並傳遞不正確認證時，它會追蹤不正確登入嘗試，並在使用者超過指定的時間範圍內的無效嘗試臨界值時，將其鎖定。 由於我們的自訂驗證邏輯會呼叫 `ValidateUser` 方法，因此有效使用者名稱的密碼不正確會遞增 [不正確登入嘗試] 計數器，但如果使用者名稱和密碼有效，但電子郵件地址不正確，此計數器就不會遞增。 這種行為很有説明，因為駭客不太可能知道使用者名稱和密碼，而是必須使用暴力密碼破解技術來判斷使用者的電子郵件地址。

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>步驟4：改善登入控制項的無效認證訊息

當使用者嘗試使用不正確認證登入時，登入控制項會顯示一則訊息，說明登入嘗試不成功。 特別是，控制項會顯示其[`FailureText` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)所指定的訊息，其預設值為登入嘗試不成功。 請重試。

回想一下，使用者的認證可能會有許多原因無效：

- 使用者名稱可能不存在
- 使用者名稱已存在，但密碼無效
- 使用者名稱和密碼是有效的，但使用者尚未核准
- 使用者名稱和密碼是有效的，但使用者已被鎖定（最有可能的原因是超過指定時間範圍內的無效登入嘗試次數）

而使用自訂驗證邏輯時，可能還有其他原因。 例如，使用我們在步驟3中撰寫的程式碼，使用者名稱和密碼可能是有效的，但電子郵件地址可能不正確。

無論認證為何無效，登入控制項會顯示相同的錯誤訊息。 對於帳戶尚未核准或已被鎖定的使用者而言，這項意見反應可能會造成混淆。不過有一點工作，我們可以讓登入控制項顯示更適當的訊息。

每當使用者嘗試使用不正確認證登入時，登入控制項會引發其 `LoginError` 事件。 請繼續並建立此事件的事件處理常式，並加入下列程式碼：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

上述程式碼一開始會將登入控制項的 `FailureText` 屬性設定為預設值（您的登入嘗試不會成功。 請再試一次。 然後，它會檢查提供的使用者名稱是否對應到現有的使用者帳戶。 若是如此，它會查閱產生的 `MembershipUser` 物件的 `IsLockedOut` 和 `IsApproved` 屬性，以判斷帳戶是否已鎖定或尚未核准。 不論是哪一種情況，`FailureText` 屬性都會更新為對應的值。

若要測試此程式碼，請特意嘗試以現有的使用者身分登入，但使用的密碼不正確。 在10分鐘時間範圍內的資料列中執行這五次，帳戶將會被鎖定。如 [圖 11] 所示，後續的登入嘗試一律會失敗（即使是使用正確的密碼），但現在會顯示更具描述性的帳戶，因為有太多不正確登入嘗試。 請洽詢系統管理員，以將您的帳戶解除鎖定訊息。

[![Tito 執行太多不正確登入嘗試，而且已被鎖定](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**圖 11**： Tito 執行太多不正確登入嘗試，而且已被鎖定（[按一下以觀看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png)）

## <a name="summary"></a>總結

在本教學課程之前，我們的登入頁面會針對使用者名稱/密碼配對的硬式編碼清單，驗證所提供的認證。 在本教學課程中，我們已更新頁面以根據成員資格架構來驗證認證。 在步驟1中，我們探討了以程式設計方式使用 `Membership.ValidateUser` 方法。 在步驟2中，我們以登入控制項取代了手動建立的使用者介面和程式碼。

登入控制項會呈現標準的登入使用者介面，並根據成員資格架構自動驗證使用者的認證。 此外，在有有效認證的情況下，登入控制項會透過表單驗證，將使用者登入。 簡言之，只要將登入控制項拖曳至頁面上，就可以使用功能完整的登入使用者體驗，而不需要額外的宣告式標記或程式碼。 更多的是，登入控制項可高度自訂，讓您能夠更精確地控制所呈現的使用者介面和驗證邏輯。

此時，我們網站的訪客可以建立新的使用者帳戶並登入網站，但我們尚未探討根據已驗證的使用者來限制頁面的存取權。 目前，任何使用者（已驗證或匿名）都可以在我們的網站上查看任何頁面。 除了以使用者為基礎控制網站頁面的存取權之外，我們可能會有某些網頁的功能取決於使用者。 下一個教學課程將探討如何根據登入的使用者來限制存取和頁面內功能。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [將自訂訊息顯示為鎖定和未核准的使用者](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [檢查 ASP.NET 2.0 的成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何：建立 ASP.NET 登入頁面](https://msdn.microsoft.com/library/ms178331.aspx)
- [登入控制技術檔](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [使用登入控制項](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy 和 Michael Olivero。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](creating-user-accounts-cs.md)
> [下一頁](user-based-authorization-cs.md)
