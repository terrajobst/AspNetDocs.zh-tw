---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
title: 解除鎖定及核准使用者帳戶C#（） |Microsoft Docs
author: rick-anderson
description: 本教學課程說明如何建立網頁，讓系統管理員管理使用者的鎖定和核准狀態。 我們也會看到如何核准新使用者 。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 5346aab1-9974-489f-a065-ae3883b8a350
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
msc.type: authoredcontent
ms.openlocfilehash: c19f7dfac0ddd12c2b4f3388a71a8ca0f71cbb18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545518"
---
# <a name="unlocking-and-approving-user-accounts-c"></a>解除鎖定及核准使用者帳戶 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.14.zip)或[下載 PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_cs.pdf)

> 本教學課程說明如何建立網頁，讓系統管理員管理使用者的鎖定和核准狀態。 我們也會瞭解如何只有在驗證新使用者的電子郵件地址之後，才予以核准。

## <a name="introduction"></a>簡介

除了使用者名稱、密碼和電子郵件，每個使用者帳戶都有兩個狀態欄位，可決定使用者是否可以登入網站：已鎖定並已核准。 如果使用者在指定的分鐘數內，以指定的次數提供不正確認證，則會自動鎖定使用者（預設設定會在10分鐘內，將使用者鎖定超過5次不正確登入嘗試）。 [已核准] 狀態適用于在新使用者能夠登入網站之前必須執行某些動作的情況。 例如，使用者可能需要先驗證其電子郵件地址，或由系統管理員核准，才能登入。

因為鎖定或未經核准的使用者無法登入，所以只是要知道如何重設這些狀態是很自然的。 ASP.NET 不包含任何內建功能或 Web 控制項，可用來管理使用者的鎖定和核准狀態，因為這些決策必須以網站為基礎來處理。 某些網站可能會自動核准所有新的使用者帳戶（預設行為）。 其他人則是由系統管理員核准新帳戶或不核准使用者，直到他們造訪的連結是在他們註冊時所提供的電子郵件地址。 同樣地，某些網站可能會鎖定使用者，直到系統管理員重設其狀態為止，而其他網站則傳送電子郵件給已鎖定的使用者，其 URL 可供他們造訪以解除鎖定其帳戶。

本教學課程說明如何建立網頁，讓系統管理員管理使用者的鎖定和核准狀態。 我們也會瞭解如何只有在驗證新使用者的電子郵件地址之後，才予以核准。

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>步驟1：管理使用者的已鎖定和核准狀態

<a id="Tutorial12"></a>在[*建立介面來選取許多*](building-an-interface-to-select-one-user-account-from-many-cs.md)教學課程中的一個使用者帳戶時，我們所建立的頁面會在分頁的篩選 GridView 中列出每個使用者帳戶。 方格會列出每個使用者的名稱和電子郵件、其已核准和鎖定的狀態、其目前是否在線上，以及與使用者相關的任何批註。 若要管理使用者的已核准和鎖定狀態，我們可以讓此方格變成可編輯。 若要變更使用者的已核准狀態，系統管理員會先找出使用者帳戶，然後編輯對應的 GridView 資料列，檢查或取消核取 [已核准] 核取方塊。 或者，我們可以透過個別的 ASP.NET 網頁來管理已核准和已鎖定的狀態。

在本教學課程中，我們將使用兩個 ASP.NET 網頁： `ManageUsers.aspx` 和 `UserInformation.aspx`。 這裡的想法是，`ManageUsers.aspx` 列出系統中的使用者帳戶，而 `UserInformation.aspx` 可讓管理員為特定使用者管理已核准和鎖定的狀態。 我們的第一個商務訂單是在 `ManageUsers.aspx` 中擴大 GridView，以包含 HyperLinkField，這會轉譯為連結的資料行。 我們想要讓每個連結指向 `UserInformation.aspx?user=UserName`，其中*UserName*是要編輯的使用者名稱。

> [!NOTE]
> 如果您下載了<a id="Tutorial13"> </a>[*復原和變更密碼*](recovering-and-changing-passwords-cs.md)的程式碼教學課程，您可能已經注意到 [`ManageUsers.aspx`] 頁面已經包含一組 [管理] 連結，而 [`UserInformation.aspx`] 頁面提供了變更所選使用者密碼的介面。 我決定不要在與本教學課程相關聯的程式碼中複寫該功能，因為它的運作方式是避開成員資格 API 並直接操作 SQL Server 資料庫來變更使用者的密碼。 本教學課程會使用 [`UserInformation.aspx`] 頁面從頭開始。

### <a name="adding-manage-links-to-theuseraccountsgridview"></a>將「管理」連結新增至`UserAccounts`GridView

開啟 [`ManageUsers.aspx`] 頁面，並將 HyperLinkField 新增至 `UserAccounts` GridView。 將 HyperLinkField 的 `Text` 屬性設定為 "Manage"，並將其 `DataNavigateUrlFields` 和 `DataNavigateUrlFormatString` 屬性分別設為 `UserName` 和 "UserInformation. .aspx？ user ={0}"。 這些設定會設定 HyperLinkField，讓所有超連結都會顯示「管理」文字，但每個連結都會將適當的使用者*名稱*值傳遞至 querystring。

將 HyperLinkField 新增至 GridView 之後，請花一點時間透過瀏覽器來觀看 `ManageUsers.aspx` 頁面。 如 [圖 1] 所示，每個 GridView 資料列現在都包含「管理」連結。 Bruce 的 [管理] 連結會指向 `UserInformation.aspx?user=Bruce`，而 Dave 的 [管理] 連結則會指向 `UserInformation.aspx?user=Dave`。

[![HyperLinkField 會新增](unlocking-and-approving-user-accounts-cs/_static/image2.png)](unlocking-and-approving-user-accounts-cs/_static/image1.png)

**圖 1**： HyperLinkField 新增每個使用者帳戶的 [管理] 連結（[按一下以查看完整大小的影像](unlocking-and-approving-user-accounts-cs/_static/image3.png)）

我們稍後會為 [`UserInformation.aspx`] 頁面建立使用者介面和程式碼，但首先我們要討論如何以程式設計方式變更使用者的鎖定和核准狀態。 [`MembershipUser` 類別](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)具有[`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)和[`IsApproved` 屬性](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)。 `IsLockedOut` 屬性是唯讀的。 沒有任何機制可以程式設計方式鎖定使用者;若要解除鎖定使用者，請使用 `MembershipUser` 類別的[`UnlockUser` 方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)。 `IsApproved` 屬性可讀取和寫入。 若要儲存對此屬性所做的任何變更，我們需要呼叫 `Membership` 類別的[`UpdateUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)，並傳入已修改的 `MembershipUser` 物件。

因為 `IsApproved` 屬性是可讀取和寫入的，所以 CheckBox 控制項可能是設定此屬性的最佳使用者介面元素。 不過，[`IsLockedOut`] 屬性的核取方塊無法使用，因為系統管理員無法鎖定使用者，她只能解除鎖定使用者。 [`IsLockedOut`] 屬性的適當使用者介面是一個按鈕，當您按一下時，就會解除鎖定使用者帳戶。 只有在使用者遭到鎖定時，才應該啟用此按鈕。

### <a name="creating-theuserinformationaspxpage"></a>建立`UserInformation.aspx`頁面

我們現在已準備好在 `UserInformation.aspx`中執行使用者介面。 開啟此頁面，並新增下列 Web 控制項：

- 按一下時，會將系統管理員傳回 `ManageUsers.aspx` 頁面的超連結控制項。
- 用來顯示所選使用者名稱的標籤 Web 控制項。 將此標籤的 `ID` 設定為 `UserNameLabel` 並清除其 `Text` 屬性。
- 名為 `IsApproved`的 CheckBox 控制項。 將其 [`AutoPostBack`] 屬性設定為 [`true`]。
- 標籤控制項，用於顯示使用者的上次鎖定日期。 將此標籤命名 `LastLockedOutDateLabel` 並清除其 `Text` 屬性。
- 用來解除鎖定使用者的按鈕。 將此按鈕命名為 `UnlockUserButton`，並將其 `Text` 屬性設定為 [解除鎖定使用者]。
- 顯示狀態訊息的標籤控制項，例如「使用者的已核准狀態已更新」。 將此控制項命名 `StatusMessage`、清除其 [`Text`] 屬性，並將其 [`CssClass`] 屬性設定為 [`Important`]。 （`Important` CSS 類別定義于 `Styles.css` 樣式表單檔案中，它會以較大的紅色字型顯示對應的文字）。

加入這些控制項之後，Visual Studio 中的設計檢視看起來應該類似 [圖 2] 中的螢幕擷取畫面。

[![建立 UserInformation 的使用者介面](unlocking-and-approving-user-accounts-cs/_static/image5.png)](unlocking-and-approving-user-accounts-cs/_static/image4.png)

**圖 2**：建立 `UserInformation.aspx` 的使用者介面（[按一下以觀看完整大小的影像](unlocking-and-approving-user-accounts-cs/_static/image6.png)）

完成使用者介面後，下一個工作是根據選取的使用者資訊，設定 [`IsApproved`] 核取方塊和其他控制項。 為頁面的 `Load` 事件建立事件處理常式，並新增下列程式碼：

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample1.cs)]

上述程式碼一開始會先確認這是頁面的第一次造訪，而不是後續的回傳。 然後，它會讀取透過 `user` querystring 欄位所傳遞的使用者名稱，並經由 `Membership.GetUser(username)` 方法來抓取有關該使用者帳戶的資訊。 如果未透過 querystring 提供任何使用者名稱，或如果找不到指定的使用者，系統管理員就會傳送回 [`ManageUsers.aspx`] 頁面。

然後，`MembershipUser` 物件的 `UserName` 值會顯示在 `UserNameLabel` 中，並根據 `IsApproved` 屬性值來檢查 `IsApproved` 核取方塊。

`MembershipUser` 物件的[`LastLockoutDate` 屬性](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx)會傳回 `DateTime` 值，指出使用者上次被鎖定的時間。如果使用者從未被鎖定，則傳回的值會視成員資格提供者而定。 建立新帳戶時，`SqlMembershipProvider` 會將 `aspnet_Membership` 資料表的 `LastLockoutDate` 欄位設定為 [`1754-01-01 12:00:00 AM`]。 如果 `LastLockoutDate` 屬性發生在2000年之前，上述程式碼會在 `LastLockoutDateLabel` 中顯示空字串;否則，`LastLockoutDate` 屬性的日期部分會顯示在標籤中。 `UnlockUserButton'` s `Enabled` 屬性會設定為使用者的已鎖定狀態，這表示只有在使用者遭到鎖定時，才會啟用此按鈕。

請花點時間透過瀏覽器測試 `UserInformation.aspx` 頁面。 當然，您將需要從 `ManageUsers.aspx` 開始，並選取要管理的使用者帳戶。 當到達 `UserInformation.aspx`時，請注意，只有在使用者已核准時，才會檢查 [`IsApproved`] 核取方塊。 如果使用者曾經被鎖定，則會顯示其上次鎖定日期。 只有在使用者目前已鎖定時，才會啟用 [解除鎖定使用者] 按鈕。核取或取消核取 [`IsApproved`] 核取方塊，或按一下 [解除鎖定使用者] 按鈕會導致回傳，但不會對使用者帳戶進行任何修改，因為我們尚未建立這些事件的事件處理常式。

返回 Visual Studio，並為 `IsApproved` 核取方塊的 `CheckedChanged` 事件和 `UnlockUser` 按鈕的 `Click` 事件建立事件處理常式。 在 `CheckedChanged` 事件處理常式中，將使用者的 `IsApproved` 屬性設定為核取方塊的 `Checked` 屬性，然後透過對 `Membership.UpdateUser`的呼叫儲存變更。 在 `Click` 事件處理常式中，只要呼叫 `MembershipUser` 物件的 `UnlockUser` 方法即可。 在這兩個事件處理常式中，在 [`StatusMessage`] 標籤中顯示適當的訊息。

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample2.cs)]

### <a name="testing-theuserinformationaspxpage"></a>測試`UserInformation.aspx`頁面

這些事件處理常式備妥之後，請重新流覽頁面，並將使用者重新核准。 如 [圖 3] 所示，您應該會在頁面上看到一則簡短的訊息，指出已成功修改使用者的 `IsApproved` 屬性。

[![Chris 已未經核准](unlocking-and-approving-user-accounts-cs/_static/image8.png)](unlocking-and-approving-user-accounts-cs/_static/image7.png)

**圖 3**： Chris 已未經核准（[按一下以觀看完整大小的影像](unlocking-and-approving-user-accounts-cs/_static/image9.png)）

接下來，請登出，然後嘗試以帳戶剛沒有核准的使用者身分登入。 因為使用者未經過核准，所以無法登入。 根據預設，如果使用者無法登入，不論原因為何，登入控制項會顯示相同的訊息。 但在<a id="Tutorial6"> </a>[*針對成員資格使用者存放區驗證使用者認證*](../membership/validating-user-credentials-against-the-membership-user-store-cs.md)教學課程中，我們探討了如何增強登入控制項，以顯示更適當的訊息。 如 [圖 4] 所示，Chris 會顯示一則訊息，說明他無法登入，因為他的帳戶尚未核准。

[![Chris 無法登入，因為他的帳戶未核准](unlocking-and-approving-user-accounts-cs/_static/image11.png)](unlocking-and-approving-user-accounts-cs/_static/image10.png)

**圖 4**： Chris 無法登入，因為他的帳戶未核准（[按一下以觀看完整大小的影像](unlocking-and-approving-user-accounts-cs/_static/image12.png)）

若要測試鎖定的功能，請嘗試以核准的使用者身分登入，但使用的密碼不正確。 重複此程式，直到使用者的帳戶被鎖定為止。如果嘗試從已鎖定的帳戶登入，則登入控制項也會更新，以顯示自訂訊息。 當您開始在登入頁面上看到下列訊息時，您知道帳戶已被鎖定：「您的帳戶因為太多不正確登入嘗試而遭到鎖定。 請洽詢系統管理員，讓您的帳戶解除鎖定。」

返回 [`ManageUsers.aspx`] 頁面，然後按一下 [已鎖定的使用者] 的 [管理] 連結。 如 [圖 5] 所示，您應該會在 [`LastLockedOutDateLabel` 解除鎖定使用者] 按鈕中看到一個值。 按一下 [解除鎖定使用者] 按鈕，將使用者帳戶解除鎖定。 一旦您解除鎖定使用者，他們就能夠重新登入。

[系統已鎖定 ![Dave](unlocking-and-approving-user-accounts-cs/_static/image14.png)](unlocking-and-approving-user-accounts-cs/_static/image13.png)

**圖 5**： Dave 已從系統鎖定（[按一下以觀看完整大小的影像](unlocking-and-approving-user-accounts-cs/_static/image15.png)）

## <a name="step-2-specifying-new-users-approved-status"></a>步驟2：指定新使用者的核准狀態

[已核准] 狀態適用于您想要在新的使用者登入及存取網站的使用者特定功能之前執行某個動作的案例。 例如，您可能正在執行私人網站，其中登入和註冊頁面除外，只有已驗證的使用者可以存取所有頁面。 但是，如果 stranger 到達您的網站、尋找註冊頁面，然後建立帳戶，會發生什麼事？ 若要避免發生這種情況，您可以將註冊頁面移至 `Administration` 資料夾，並要求系統管理員手動建立每個帳戶。 或者，您可以允許任何人註冊，但禁止網站存取，直到系統管理員核准使用者帳戶為止。

根據預設，CreateUserWizard 控制項會核准新的帳戶。 您可以使用控制項的[`DisableCreatedUser` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)來設定此行為。 將此屬性設定為 `true`，則不會核准新的使用者帳戶。

> [!NOTE]
> 根據預設，CreateUserWizard 控制項會自動記錄新的使用者帳戶。 這個行為是由控制項的[`LoginCreatedUser` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)所決定。 由於未核准的使用者無法登入網站，因此當 `DisableCreatedUser` 為 `true` 時，新的使用者帳戶就不會登入網站，而不論 `LoginCreatedUser` 屬性的值為何。

如果您透過 `Membership.CreateUser` 方法以程式設計方式建立新的使用者帳戶，若要建立未核准的使用者帳戶，請使用其中一個接受新使用者的 `IsApproved` 屬性值做為輸入參數的多載。

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>步驟3：驗證使用者的電子郵件地址以核准他們

許多支援使用者帳戶的網站都不會核准新的使用者，直到他們確認註冊時所提供的電子郵件地址為止。 此驗證程式通常用來對抗 bot、垃圾郵件和其他 ne'er 的 wells，因為它需要唯一的已驗證電子郵件地址，並在註冊程式中新增額外的步驟。 使用此模型時，當新使用者註冊時，會傳送電子郵件訊息，其中包含驗證頁面的連結。 藉由造訪連結，使用者證明他們收到了電子郵件，因此提供的電子郵件地址是有效的。 [驗證] 頁面會負責核准使用者。 這可能會自動發生，因此會核准任何到達此頁面的使用者，或僅在使用者提供一些額外資訊（例如[CAPTCHA](http://en.wikipedia.org/wiki/Captcha)）之後。

為了配合此工作流程，我們必須先更新帳戶建立頁面，讓新使用者未經核准。 開啟 [`Membership`] 資料夾中的 [`EnhancedCreateUserWizard.aspx`] 頁面，並將 CreateUserWizard 控制項的 `DisableCreatedUser` 屬性設定為 [`true`]。

接下來，我們需要設定 CreateUserWizard 控制項，將電子郵件傳送給新的使用者，並提供如何驗證其帳戶的指示。 特別的是，我們會在電子郵件中包含連結至 [`Verification.aspx`] 頁面（我們尚未建立），並透過 querystring 傳遞新使用者的 `UserId`。 [`Verification.aspx`] 頁面將會查閱指定的使用者，並將其標示為已核准。

### <a name="sending-a-verification-email-to-new-users"></a>將驗證電子郵件傳送給新使用者

若要從 CreateUserWizard 控制項傳送電子郵件，請適當地設定其 [`MailDefinition`] 屬性。 如<a id="Tutorial13"> </a>[前一個教學](recovering-and-changing-passwords-cs.md)課程中所討論，ChangePassword 和 PasswordRecovery 控制項包含一個[`MailDefinition` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)，其運作方式與 CreateUserWizard 控制項的相同。

> [!NOTE]
> 若要使用 `MailDefinition` 屬性，您必須在 `Web.config`中指定郵件傳遞選項。 如需詳細資訊，請參閱[在 ASP.NET 中傳送電子郵件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)。

首先，在 `EmailTemplates` 資料夾中建立名為 `CreateUserWizard.txt` 的新電子郵件範本。 針對範本使用下列文字：

[!code-aspx[Main](unlocking-and-approving-user-accounts-cs/samples/sample3.aspx)]

將 `MailDefinition'` s `BodyFileName` 屬性設為 "~/EmailTemplates/CreateUserWizard.txt"，並將其 `Subject` 屬性設定為「歡迎使用我的網站！ 請啟用您的帳戶。」

請注意，`CreateUserWizard.txt` 電子郵件範本包含 `<%VerificationUrl%>` 預留位置。 這是將放置 `Verification.aspx` 頁面 URL 的位置。 CreateUserWizard 會自動以新帳戶的使用者名稱和密碼取代 `<%UserName%>` 和 `<%Password%>` 預留位置，但沒有內建 `<%VerificationUrl%>` 預留位置。 我們需要手動將其取代為適當的驗證 URL。

若要完成這項操作，請為 CreateUserWizard 的[`SendingMail` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx)建立事件處理常式，並新增下列程式碼：

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample4.cs)]

`SendingMail` 事件會在 `CreatedUser` 事件之後引發，這表示在上述事件處理常式執行時，已建立新的使用者帳戶。 我們可以藉由呼叫 `Membership.GetUser` 方法，傳入輸入至 CreateUserWizard 控制項的 `UserName`，來存取新使用者的 `UserId` 值。 接下來，驗證 URL 的格式為。 語句 `Request.Url.GetLeftPart(UriPartial.Authority)` 會傳回 URL 的 `http://yourserver.com` 部分;`Request.ApplicationPath` 會傳回應用程式根目錄的路徑。 驗證 URL 接著會定義為 `Verification.aspx?ID=userId`。 接著會串連這兩個字串，以形成完整的 URL。 最後，電子郵件訊息內文（`e.Message.Body`）會以完整的 URL 取代所有出現的 `<%VerificationUrl%>`。

最後的結果是新的使用者未經核准，這表示他們無法登入網站。 此外，它們會自動傳送電子郵件，其中包含驗證 URL 的連結（請參閱 [圖 6]）。

[![新使用者會收到一封電子郵件，其中包含驗證 URL 的連結](unlocking-and-approving-user-accounts-cs/_static/image17.png)](unlocking-and-approving-user-accounts-cs/_static/image16.png)

**圖 6**：新的使用者會收到一封電子郵件，其中包含驗證 URL 的連結（[按一下以觀看完整大小的影像](unlocking-and-approving-user-accounts-cs/_static/image18.png)）

> [!NOTE]
> CreateUserWizard 控制項的預設 CreateUserWizard 步驟會顯示一則訊息，通知使用者他們的帳戶已建立，並顯示 [繼續] 按鈕。 按一下此動作會將使用者帶到控制項的 [`ContinueDestinationPageUrl`] 屬性所指定的 URL。 `EnhancedCreateUserWizard.aspx` 中的 CreateUserWizard 設定為將新的使用者傳送至 `~/Membership/AdditionalUserInfo.aspx`，這會提示使用者提供其 [家鄉]、[首頁 URL] 和 [簽章]。 因為這項資訊只能由登入的使用者加入，所以更新此屬性以將使用者傳回網站的首頁（`~/Default.aspx`）是合理的。 此外，`EnhancedCreateUserWizard.aspx` 頁面或 CreateUserWizard 步驟也應增強，以通知使用者他們已傳送驗證電子郵件，而且其帳戶必須遵循這封電子郵件中的指示，才會啟用。 我將這些修改留給讀者的練習。

### <a name="creating-the-verification-page"></a>建立驗證頁面

我們的最後一項工作是建立 `Verification.aspx` 頁面。 將此頁面新增至根資料夾，並將它與 `Site.master` 主版頁面建立關聯。 就像我們在網站中新增的大部分內容頁所做的一樣，移除參考 `LoginContent` ContentPlaceHolder 的內容控制項，讓 [內容] 頁面使用主版頁面的預設內容。

將 標籤 Web 控制項新增至 `Verification.aspx` 頁面，將其 `ID` 設定為 `StatusMessage` 並清除其 text 屬性。 接下來，建立 `Page_Load` 事件處理常式，並新增下列程式碼：

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample5.cs)]

上述大部分的程式碼會驗證透過 querystring 提供的 `UserId` 是否存在、它是有效的 `Guid` 值，而且它會參考現有的使用者帳戶。 如果所有這些檢查都通過，則會核准使用者帳戶;否則，會顯示適當的狀態訊息。

[圖 7] 顯示透過瀏覽器造訪時的 `Verification.aspx` 頁面。

[![新使用者的帳戶現在已核准](unlocking-and-approving-user-accounts-cs/_static/image20.png)](unlocking-and-approving-user-accounts-cs/_static/image19.png)

**圖 7**：現在已核准新使用者的帳戶（[按一下以觀看完整大小的影像](unlocking-and-approving-user-accounts-cs/_static/image21.png)）

## <a name="summary"></a>總結

所有成員資格使用者帳戶都有兩種狀態，可決定使用者是否可以登入網站： `IsLockedOut` 和 `IsApproved`。 這兩個屬性都必須 `true`，使用者才能登入。

使用者的「鎖定」狀態是用來做為安全性措施，以降低駭客透過暴力密碼破解方式進入網站的可能性。 具體而言，如果在特定時間範圍內有特定數目的無效登入嘗試，就會鎖定使用者。 這些界限可透過 `Web.config`中的成員資格提供者設定來設定。

「核准」狀態通常用來防止新使用者登入，直到某個動作有過了為止。 網站可能會要求系統管理員先核准新帳戶，或如我們在步驟3中所見，驗證其電子郵件地址。

快樂的程式設計！

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](recovering-and-changing-passwords-cs.md)
> [下一頁](building-an-interface-to-select-one-user-account-from-many-vb.md)
