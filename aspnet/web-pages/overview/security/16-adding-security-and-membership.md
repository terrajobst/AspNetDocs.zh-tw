---
uid: web-pages/overview/security/16-adding-security-and-membership
title: 將安全性和成員資格新增至 ASP.NET Web Pages （Razor）網站 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何保護您的網站，讓某些頁面僅供登入的人員使用。 （您也會看到如何建立頁面 。
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: 0be3e767a42939a3c343f6d4a730eb1d9a6b367c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628384"
---
# <a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>新增 ASP.NET Web Pages （Razor）網站的安全性和成員資格

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何保護 ASP.NET Web Pages （Razor）網站，讓某些頁面僅供登入的人員使用。 （您也會看到如何建立任何人都可以存取的頁面）。
> 
> **您將瞭解的內容：** 
> 
> - 如何建立具有註冊頁面和登入頁面的網站，以便在某些頁面上，您可以限制只有成員的存取權。
> - 如何建立公用和僅限成員的頁面。
> - 如何定義角色，也就是在您的網站上具有不同安全性許可權的群組，以及如何將使用者指派給角色。
> - 如何使用 CAPTCHA 防止自動化程式（bot）建立成員帳戶。
>   
> 
> 以下是文章中引進的 ASP.NET 功能：
> 
> - WebMatrix**入門網站**範本。
> - `WebSecurity` helper 和 `Roles` 類別。
> - `ReCaptcha` helper。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - WebMatrix 3
> - ASP.NET Web helper 程式庫

您可以設定您的網站，讓使用者可以登入&#8212; ，也就是，讓網站支援*成員資格*。 基於許多原因，這很有用。 例如，您的網站可能會有只能供成員使用的頁面。 在某些情況下，您可能需要使用者登入，才能傳送意見反應或離開留言。

即使您的網站支援成員資格，在使用者使用網站上的某些頁面之前，不一定需要登入。 未登入的使用者稱為「*匿名使用者*」。

使用者可以在您的網站上註冊，然後就可以登入網站。 網站需要使用者名稱（電子郵件地址）和密碼，以確認使用者是他們所宣稱的身分。 這項登入和確認使用者身分識別的程式稱為「*驗證*」。

您可以用不同的方式設定安全性和成員資格：

- 如果您使用 WebMatrix，簡單的方式是根據**入門網站**範本建立新的網站。 已針對安全性和成員資格設定此範本，且已有註冊頁面、登入頁面等等。

    範本所建立的網站也有選項可讓使用者使用 Facebook、Google 或 Twitter 之類的外部網站登入。
- 如果您想要將安全性新增至現有的網站，或不想使用**入門網站**範本，您可以建立自己的註冊頁面、登入頁面等等。

本文著重于第一個選項 &mdash; 如何使用「**入門網站**」範本來新增安全性。 它也提供一些關於如何執行您自己的安全性的基本資訊，然後提供有關如何執行此動作之詳細資訊的連結。 另外還有關于如何啟用外部登入的資訊，在個別的文章中有更詳細的說明。

## <a name="creating-website-security-using-the-starter-site-template"></a>使用入門網站範本建立網站安全性

在 WebMatrix 中，您可以使用「**入門網站**」範本來建立包含下列內容的網站：

- 用來儲存成員之使用者名稱和密碼的資料庫。
- 匿名（新的）使用者可以註冊的註冊頁面。
- 登入和登出頁面。
- 密碼修復和重設頁面。

下列程式說明如何建立網站並加以設定。

1. 啟動 WebMatrix，然後在 [**快速入門**] 頁面中，**從 [範本**] 選取 [網站]。
2. 選取 [**入門網站**] 範本，然後按一下 **[確定]** 。 WebMatrix 會建立新的網站。
3. 在左窗格中，按一下 [檔案 **] 工作區**選取器。
4. 在您網站的根資料夾中，開啟 [ *\_AppStart* ] 檔案，這是用來包含全域設定的特殊檔案。 其中包含一些使用 `//` 字元標記為批註的語句：

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    這些語句會設定 `WebMail` 協助程式，以用來傳送電子郵件。 成員資格系統可以在使用者註冊或想要變更其密碼時，使用電子郵件傳送確認訊息。 （例如，在使用者註冊之後，他們會收到一封電子郵件，其中包含可按一下以完成註冊程式的連結。）

    傳送電子郵件需要 SMTP 伺服器的存取權，如[將電子郵件新增至 ASP.NET Web Pages 網站](https://go.microsoft.com/fwlink/?LinkId=202899)中所述。 您會將電子郵件設定儲存在此中央 *\_AppStart*檔案，讓您不必重複地將它們編碼到每個可傳送電子郵件的頁面。 （您不需要設定 SMTP 設定來設定註冊資料庫; 只有當您想要驗證使用者的電子郵件別名，並讓使用者重設忘記密碼時，才需要 SMTP 設定）。
5. 藉由移除每個語句前面的 `//`，將其取消批註。

    如果您不想要設定電子郵件確認，可以略過此步驟和下一個步驟。 如果未設定 SMTP 值，則會立即提供新帳戶，而不會收到確認電子郵件。
6. 在程式碼中修改下列電子郵件相關設定：

   - 將 `WebMail.SmtpServer` 設定為您可以存取的 SMTP 伺服器名稱。
   - 保留 `WebMail.EnableSsl` 設定為 [`true`]。 此設定會藉由加密來保護傳送到 SMTP 伺服器的認證。
   - 將 `WebMail.UserName` 設定為 SMTP 伺服器帳戶的使用者名稱。
   - 將 `WebMail.Password` 設定為 SMTP 伺服器帳戶的密碼。
   - 將 `WebMail.From` 設定為您自己的電子郵件地址。 這是傳送訊息的來源電子郵件地址。

     > [!NOTE] 
     > 
     > **秘訣**如需這些屬性值的詳細資訊，請參閱[針對 ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkID=202906)中的[電子郵件設定](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings)。
7. 儲存並關閉 *\_AppStart*。
8. 在瀏覽器中執行*預設的. cshtml*頁面。

    ![安全性-成員資格-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > 如果您看到錯誤訊息，指出屬性必須是 `ExtendedMembershipProvider`的實例，則網站可能未設定為使用 ASP.NET Web Pages 成員資格系統（SimpleMembership）。 如果主控提供者的伺服器設定方式不同于本機伺服器，有時可能會發生這種情況。 若要修正此問題，請將下列*元素新增至網站的 web.config*檔案：
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > 將這個專案加入做為 `<configuration>` 專案的子系，並當做 `<system.web>` 元素的對等專案。
9. 在頁面的右上角，按一下 [**註冊**] 連結。 隨即顯示 [ *Register. cshtml* ] 頁面。
10. 輸入 [使用者名稱] 和 [密碼]，然後按一下 [**註冊**]。

    ![安全性-成員資格-3](16-adding-security-and-membership/_static/image2.png)

    當您從**入門網站**範本建立網站時，名為*StarterSite*的資料庫會建立在網站的*應用程式\_Data*資料夾中。 註冊期間，系統會將您的使用者資訊新增至資料庫。 如果您設定 SMTP 值，則會將訊息傳送至您所使用的電子郵件地址，以便完成註冊。

    ![安全性-成員資格-4](16-adding-security-and-membership/_static/image3.png)
11. 移至您的電子郵件程式並尋找訊息，其中會有您的確認碼和網站的超連結。
12. 按一下此超連結以啟用您的帳戶。 確認超連結會開啟註冊確認頁面。

    ![安全性-成員資格-5](16-adding-security-and-membership/_static/image4.png)
13. 按一下 [**登**入] 連結，然後使用您註冊的帳戶登入。

      登入後 **，登入和** **註冊**連結會由**登出**連結取代。 您的登入名稱會顯示為連結。 （此連結可讓您移至可變更密碼的頁面）。

      ![安全性-成員資格-6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > 根據預設，ASP.NET 網頁會以純文字傳送認證給伺服器（以人類看得懂的文字）。 生產網站應該使用安全 HTTP （HTTPs://，也稱為*安全通訊端層*或 SSL）來加密與伺服器交換的機密資訊。 如先前範例所示，您可以設定 `WebMail.EnableSsl=true`，以使用 SSL 來傳送電子郵件訊息。 如需 SSL 的詳細資訊，請參閱[保護 Web 通訊：憑證、SSL 和 HTTPs://](https://go.microsoft.com/fwlink/?LinkId=208660)。

## <a name="additional-membership-functionality-in-the-site"></a>網站中的其他成員資格功能

您的網站包含可讓使用者管理其帳戶的其他功能。 使用者可以執行下列動作：

- 變更其密碼。 登入之後，他們可以按一下使用者名稱（這是一個連結）。 這會將它們帶到可以建立新密碼的頁面（*帳戶/ChangePassword. cshtml*）。
- 復原忘記的密碼。 在 [登入] 頁面上，有一個連結（**您忘記密碼？** ），會將使用者帶到可輸入電子郵件地址的頁面（*Account/ForgotPassword*）。 網站會傳送電子郵件給他們，其中有連結可供按一下，以便設定新密碼（*Account/passwordreset.xml*）。

您也可以讓使用者也可以使用外部網站進行登入，如稍後所述。

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>建立僅限成員的頁面

在這段時間內，任何人都可以流覽至您網站中的任何頁面。 但是，您可能會想要讓只能使用已登入之使用者的頁面（也就是成員）。 ASP.NET 可讓您建立只能由登入成員存取的頁面。 一般而言，如果匿名使用者嘗試存取僅限成員的頁面，您可以將它們重新導向至登入頁面。

在此程式中，您將建立一個資料夾，其中將包含只能供登入使用者使用的頁面。

1. 在網站的根目錄中，建立新的資料夾。 （在功能區中，按一下 [**新增**] 底下的箭號，然後選擇 [**新增資料夾**]）。
2. 將新資料夾命名為*成員*。
3. 在 [*成員*] 資料夾中，建立新的頁面，並將其命名為*MembersInformation*。
4. 使用下列程式碼和標記來取代現有的內容：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    此程式碼會測試 `WebSecurity` 物件的 `IsAuthenticated` 屬性，如果使用者已登入，則會傳回 `true`。 如果使用者未登入，則程式碼會呼叫 `Response.Redirect`，以將使用者傳送至*帳戶*資料夾中的*Login. cshtml*頁面。

    重新導向的 URL 包括一個 `returnUrl` 查詢字串值，這個值會使用 `Request.Url.LocalPath` 來設定目前頁面的路徑。 如果您在查詢字串中設定 `returnUrl` 值，如下所示（如果傳回 URL 是本機路徑），登入頁面會在使用者登入之後，將其傳回此頁面。

    程式碼也會將 *\_SiteLayout*設定為其版面配置頁。 （如需版面配置頁面的詳細資訊，請參閱[在 ASP.NET Web Pages 網站中建立一致的版面](https://go.microsoft.com/fwlink/?LinkId=202891)配置）。
5. 執行網站。 如果您仍然登入，請按一下頁面頂端的 [**登出**] 按鈕。
6. 在瀏覽器中，要求頁面 */Members/MembersInformation*。 例如，URL 看起來可能像這樣：

    `http://localhost:38366/Members/MembersInformation`

    （您的 URL 中的埠號碼（38366）可能會不同）。

    系統會將您重新導向至 [*登入 cshtml* ] 頁面，因為您未登入。
7. 使用您稍早建立的帳戶登入。 系統會將您重新導向回 [ *MembersInformation* ] 頁面。 因為您已經登入，所以這次您會看到頁面內容。

若要保護對多個頁面的存取，您可以執行下列動作：

- 將安全性檢查新增至每個頁面。
- 在您保留受保護頁面的資料夾中建立 *\_PageStart* ，並在該處新增安全性檢查。 [ *\_PageStart* ] 頁面可作為資料夾中所有頁面的一種全域頁面。 這項技術會在[針對 ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)中更詳細地說明。

## <a name="creating-security-for-groups-of-users-roles"></a>建立使用者群組的安全性（角色）

如果您的網站有許多成員，則在您讓他們看到頁面之前，請先個別檢查每個使用者的許可權並不有效率。 相反地，您可以建立個別成員所屬的群組或*角色*。 接著，您可以根據角色來檢查許可權。 在本節中，您將建立一個 &quot;系統管理員&quot; 角色，然後建立可供位在（使用者所屬）該角色之使用者存取的網頁。

ASP.NET 成員資格系統設定為支援角色。 不過，與成員資格註冊和登入不同的是，「**入門網站**」範本不包含可協助您管理角色的頁面。 （管理角色是系統管理工作，而不是使用者工作）。不過，您可以直接在 WebMatrix 的成員資格資料庫中加入群組。

1. 在 WebMatrix 中，按一下 [**資料庫**] 工作區選取器。
2. 在左窗格中，開啟 [ *StarterSite* ] 節點，開啟 [**資料表]** 節點，然後按兩下 [*網頁\_角色*] 資料表。

    ![安全性-成員資格-7](16-adding-security-and-membership/_static/image6.png)
3. 新增名為 &quot;admin&quot;的角色。 *RoleId*欄位會自動填入。 （這是主要索引鍵，而且已設定為識別欄位，如在[ASP.NET Web Pages 網站中使用資料庫簡介](https://go.microsoft.com/fwlink/?LinkId=202893)中所述）。
4. 記下 [ *RoleId* ] 欄位的值。 （如果這是您所定義的第一個角色，則會是1）。

    ![安全性-成員資格-8](16-adding-security-and-membership/_static/image7.png)
5. 關閉 [ *\_角色的網頁*] 資料表。
6. 開啟 [ *UserProfile* ] 資料表。
7. 記下資料表中一或多個使用者的*UserId*值，然後關閉資料表。
8. 開啟 [*網頁\_UserInRoles* ] 資料表，並在資料表中輸入*UserID*和*RoleID*值。 例如，若要將使用者2放入 &quot;admin&quot; 角色中，請輸入下列值：

    ![安全性-成員資格-9](16-adding-security-and-membership/_static/image8.png)
9. 關閉 [ *\_UsersInRoles* ] 資料表的網頁。

    現在您已定義角色，您可以設定可供該角色的使用者存取的頁面。
10. 在網站根資料夾中，建立名為*AdminError*的新頁面，並以下列程式碼取代現有的內容。 如果不允許存取頁面，這會是使用者重新導向的頁面。

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. 在網站根資料夾中，建立名為*AdminOnly*的新頁面，並以下列程式碼取代現有的程式碼：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    如果目前的使用者是指定角色的成員（在此案例中為「系統管理員」角色），則 `Roles.IsUserInRole` 方法會傳回 `true`。
12. 在瀏覽器中執行*預設. cshtml* ，但不要登入。 （如果您已經登入，請登出。）
13. 在瀏覽器的網址列中，在 URL 中新增*AdminOnly* 。 （換句話說，請要求*AdminOnly* ）。系統會將您重新導向至*AdminError* ，因為您目前不是以 &quot;系統管理員&quot; 角色的使用者身分登入。
14. 返回*Default. cshtml* ，並以您新增至 &quot;admin&quot; 角色的使用者身分登入。
15. 流覽至 [ *AdminOnly* ] 頁面。 這次您會看到此頁面。

## <a name="preventing-automated-programs-from-joining-your-website"></a>防止自動化程式加入您的網站

登入頁面將不會停止自動程式（有時也稱為*web 機器人*或*bot*）向您的網站註冊。 此程式說明如何啟用註冊頁面的 ReCaptcha 測試。

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. 在 ReCaptcha.Net （[http://recaptcha.net](http://recaptcha.net)）註冊您的網站。 當您完成註冊時，將會取得公開金鑰和私密金鑰。
2. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。
3. 在 [*帳戶*] 資料夾中，開啟名為 [ *Register. cshtml*] 的檔案。
4. 在頁面頂端的程式碼中，找出下列幾行，並移除 `//` 的批註字元，將其取消批註：

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. 以您自己的 ReCaptcha 私用金鑰取代 `PRIVATE_KEY`。
6. 在頁面的標記中，移除 `@*`，並在頁面標記中的下列幾行周圍 `*@` 批註字元：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. 將 `PUBLIC_KEY` 取代為您的金鑰。
8. 如果您還沒有移除它，請移除包含開頭為 "To enable CAPTCHA 驗證 ..." 之文字的 `<div>` 元素。 （移除整個 `<div>` 元素及其內容）。

9. 在瀏覽器中執行*預設. cshtml* 。 如果您已經登入網站，請按一下 [**登出**] 連結。
10. 按一下 [**註冊**] 連結，並使用 CAPTCHA 測試測試註冊。

     ![安全性-成員資格-10](16-adding-security-and-membership/_static/image9.png)

如需 `ReCaptcha` helper 的詳細資訊，請參閱[使用 CATPCHA 防止自動化程式（bot）使用您的 ASP.NET 網站](https://go.microsoft.com/fwlink/?LinkId=251967)。

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>讓使用者使用外部網站登入

**入門網站**範本包含程式碼和標記，可讓使用者使用 Facebook、Windows Live、Twitter、Google 或 Yahoo 進行登入。 根據預設，不會啟用這項功能。 使用讓使用者使用這些外部提供者登入的一般程式如下：

- 決定您要支援的外部網站。
- 如有需要，請移至該網站並設定登入應用程式。 （例如，您必須這麼做才能允許 Facebook 登入。）
- 在您的網站中，設定提供者。 在大部分的情況下，您只需要取消批註 *\_AppStart*中的某些程式碼。
- 將標記新增至註冊頁面，讓人員可以連結至外部網站進行登入。 您通常可以複製所需的標記，並稍微變更文字。

您可以在[ASP.NET Web Pages 網站中啟用外部網站的登入](https://go.microsoft.com/fwlink/?LinkId=251969)主題中找到逐步指示。

使用者從另一個網站登入之後，使用者會回到您的網站，並將該登入與您的網站建立*關聯*。 實際上，這會在您的網站中為使用者的外部登入建立成員資格專案。 這可讓您使用成員資格的一般功能（例如角色）與外部登入。

## <a name="adding-security-to-an-existing-website"></a>將安全性新增至現有的網站

本文稍早的程式會依賴使用**入門網站**範本作為網站安全性的基礎。 如果您從**入門網站**範本開始，或從以該範本為基礎的網站複製相關的頁面，您可以自行編碼來在自己的網站中執行相同類型的安全性。 您會建立相同類型的頁面（註冊、登入等等），然後使用協助程式和類別來設定成員資格。

基本程式會在 blog 文章中描述，這是[執行 ASP.NET Razor 安全性的最基本方式](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)。 大部分的工作都是使用 `WebSecurity` helper 的下列方法和屬性來完成：

- [WebSecurty. UserExists](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx)、 [WebSecurity. CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx)。 這些方法可讓您判斷某人是否已註冊並加以註冊。
- [WebSecurty. IsAuthenticated](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx)。 這個屬性可讓您判斷目前使用者是否已登入。 這適用于將使用者重新導向至登入頁面（如果尚未登入）。
- [WebSecurity. Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx)， [WebSecurity. 登出](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx)。 這些方法會將使用者登入或登出。
- [WebSecurity. CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx)。 這個屬性適用于顯示目前使用者的登入名稱（如果使用者已登入）。
- [WebSecurity. ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx)。 如果您設定註冊的電子郵件確認，這個方法就很有用。 （如需詳細資料，請參閱[使用 ASP.NET Web Pages 安全性的確認功能](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)的 blog 文章）。

若要管理角色，您可以使用[角色](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx)和[成員資格](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx)類別，如 blog 專案中所述。

## <a name="additional-resources"></a>其他資源

- [自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906)
- [保護 Web 通訊安全：憑證、SSL 和 HTTPs://](https://go.microsoft.com/fwlink/?LinkId=208660)
- [執行 ASP.NET Razor 安全性](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)及[使用 ASP.NET Web Pages 安全性的確認功能](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)的最基本方式。 這些是可說明如何在不使用**入門網站**範本的情況下執行 ASP.NET 成員資格功能的 blog 文章。
- [在 ASP.NET Web Pages 網站中啟用外部網站的登入](https://go.microsoft.com/fwlink/?LinkId=251969)
- [WebSecurity 類別 API 參考](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99))（MSDN）
- [SimpleRoleProvider 類別 API 參考](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99))（MSDN）
- [SimpleMembershipProvider 類別 API 參考](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99))（MSDN）
