---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 成員資格 |Microsoft Docs
author: microsoft
description: ASP.NET 成員資格是以 ASP.NET 1.x 的表單驗證模型成功為基礎。 ASP.NET 表單驗證提供便利的方式來 incorp 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: da6fc205bd852a818d65425586cec38fdb08d310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642153"
---
# <a name="membership"></a>成員資格

由[Microsoft](https://github.com/microsoft)

> ASP.NET 成員資格是以 ASP.NET 1.x 的表單驗證模型成功為基礎。 ASP.NET 表單驗證提供便利的方法，將登入表單併入您的 ASP.NET 應用程式，並針對資料庫或其他資料存放區驗證使用者。

ASP.NET 成員資格是以 ASP.NET 1.x 的表單驗證模型成功為基礎。 ASP.NET 表單驗證提供便利的方法，將登入表單併入您的 ASP.NET 應用程式，並針對資料庫或其他資料存放區驗證使用者。 FormsAuthentication 類別的成員可以處理 cookie 以進行驗證、檢查是否有有效的登入、將使用者登出等等。不過，在 ASP.NET 1.x 應用程式中執行表單驗證，可能需要相當多的程式碼。

ASP.NET 2.0 中的成員資格只是使用表單驗證的主要進步。 （與表單驗證結合時，成員資格最強大，但不需要使用表單驗證）。您很快就會看到，您可以使用 ASP.NET 成員資格和 ASP.NET 2.0 中的登入控制項來執行功能強大的成員資格系統，而不需要撰寫太多程式碼。

## <a name="implementing-membership-in-aspnet-20"></a>在 ASP.NET 2.0 中執行成員資格

成員資格是透過下列四個步驟來執行。 請記住，其中包含許多子步驟，以及可同時執行的選擇性設定。 這些步驟的目的是要說明設定成員資格的重要概念。

1. 建立您的成員資格資料庫（如果 SQL Server 做為成員資格存放區）。
2. 在您的應用程式佈建檔中指定成員資格選項。 （預設會啟用成員資格）。
3. 決定您想要使用的成員資格存放區類型。 選項包括： 

    - Microsoft SQL Server （版本7.0 或更新版本）
    - Active Directory 存放區
    - 自訂成員資格提供者
4. 設定應用程式以進行 ASP.NET 表單驗證。 同樣地，成員資格是設計來利用表單驗證，但不需要使用表單驗證。
5. 定義成員資格的使用者帳戶，並視需要設定角色。

## <a name="creating-the-membership-database"></a>建立成員資格資料庫

如果您使用 SQL Server 7.0 或更新版本作為您的成員資格存放區，則可以使用 aspnet\_regsql 公用程式（可從 Visual Studio .NET 2005 命令提示字元中輕鬆取得）來設定您的資料庫。 Aspnet\_regsql 公用程式可用來做為命令提示字元工具或透過 GUI wizard。 Wizard 方法是設定資料庫最簡單的方式。 若要存取嚮導，只要執行下列命令即可：

`aspnet_regsql W`

執行該命令後，您會看到 ASP.NET SQL Server 安裝程式嚮導，如下所示。

![](membership/_static/image1.jpg)

**圖 1**

[ASP.NET SQL Server 安裝程式] 會在您于 Wizard 中指定的實例中建立網站。 不過，ASP.NET 會使用 machine.config 檔案中的連接字串來連接到您的資料庫。 根據預設，這個連接字串會指向 SQL Server 2005 實例，因此，如果您使用 SQL Server 2000 或 SQL Server 7.0 實例，就必須修改 machine.config 檔案中的連接字串。 該連接字串可以在這裡找到：

[!code-xml[Main](membership/samples/sample1.xml)]

可惜的是，如果您不修改連接字串，ASP.NET 就不會提供描述性錯誤。 它只會繼續抱怨，指出您尚未建立資料庫。 在上述案例中，我已修改連接字串，以指向我的本機 SQL Server 2000 實例。

## <a name="specifying-configuration-and-adding-users-and-roles"></a>指定設定及新增使用者和角色

設定成員資格的下一個步驟是將必要的資訊新增至應用程式的 web.config 檔案。 在 ASP.NET 1.x 中，修改 web.config 檔案有時候很棘手，因為使用的是 lowerCamelCase，而缺乏 Intellisense。 Visual Studio .NET 2005 可讓您更輕鬆地使用 Intellisense 來處理設定檔，但 ASP.NET 2.0 會藉由提供 Web 介面來編輯設定檔，而更進一步。

若要啟動 Web 介面，您可以按一下 [方案總管] 工具列上的 [ASP.NET 設定] 按鈕，如下所示。 您也可以透過在插入登入控制項時顯示的快顯視窗，啟動 Web 介面。

![](membership/_static/image2.jpg)

**圖 2**

這會啟動 ASP.NET 的網站管理工具，如下所示。 ASP.NET 網站管理是一個四個索引標籤的介面，可讓您輕鬆地管理應用程式設定。 下列索引標籤可供使用：

- **Home**
- **安全性**設定使用者、角色和存取權。
- **應用程式**設定應用程式設定。
- **提供者**設定並測試您的應用程式成員資格提供者。

網站管理工具可讓您輕鬆地建立新的使用者、建立新的角色，以及管理使用者和角色。 Windows 介面不提供這項功能。 Windows 介面可讓您輕鬆定義授權設定，以及加入、刪除及管理提供者、不在網站管理工具中的功能。

若要啟動 Windows 介面，請開啟 [Internet Information Services] 嵌入式管理單元，以滑鼠右鍵按一下您的應用程式，然後選擇 [屬性]。 按一下 [ASP.NET] 索引標籤，然後按一下 [編輯設定] 按鈕。 （應用程式必須在 ASP.NET 2.0 下執行，才能啟用 [編輯設定] 按鈕。 您也可以在 [ASP.NET] 對話方塊中設定 ASP.NET 版本）。[ASP.NET 設定設定] 對話方塊隨即顯示，如下所示。

![](membership/_static/image3.jpg)

**圖 3**

[一般] 索引標籤上會列出 [連接字串] 和 [應用程式設定]。 斜體中的任何設定都定義于父設定檔中（machine.config 或較高層級的 web.config），而不是斜體的設定則來自應用程式佈建檔。 如果在應用層級新增、移除或編輯設定，ASP.NET 會在應用層級 web.config 新增、移除或修改設定，而不是從繼承它的設定檔中移除設定。

[驗證] 索引標籤如下所示。 這是您將設定成員資格設定的位置。 您可以在這裡設定表單驗證設定、成員資格提供者和角色提供者。

![](membership/_static/image4.jpg)

**圖 4**

## <a name="implementing-membership-in-your-application"></a>在您的應用程式中執行成員資格

在您的應用程式中執行 ASP.NET 2.0 成員資格的最簡單方式，就是使用提供的登入控制項。 這個方法可讓您在不需撰寫任何程式碼的情況下，執行 ASP.NET 2.0 成員資格的基本概念。

ASP.NET 2.0 提供下列登入控制：

## <a name="login-control"></a>Login 控制項

登入控制項會提供介面，讓使用者登入您的成員資格系統。 它會為您提供 [使用者名稱] 和 [密碼] 文字方塊和 [登入] 按鈕。 還有許多其他常見的功能，例如註冊尚未完成的人員的連結、可讓使用者在後續造訪時自動登入的核取方塊、密碼提醒的連結等等。您可以透過控制項的屬性自訂登入控制項的所有功能。

在 ASP.NET 1.x 中，開發人員在使用表單驗證時，必須撰寫相當大量的程式碼來進行查閱。 有了 ASP.NET 2.0 成員資格，您就可以驗證使用者，而不需要撰寫任何程式碼。 ASP.NET 會自動為您執行使用者查閱。 （如果您使用登入控制項，而不使用 ASP.NET 成員資格，則可以使用**OnAuthenticate**方法來驗證使用者）。

## <a name="loginview-control"></a>LoginView 控制項

LoginView 控制項是樣板化控制項，預設會提供兩個範本;AnonymousTemplate 和 LoggedInTemplate。 所顯示的範本取決於使用者是否登入您的成員資格系統。 此控制項通常用來在使用者尚未登入時顯示登入控制項，以及在使用者已登入時，使用 LoginStatus 控制項和（或）其他登入控制項。 如果您在 ASP.NET 應用程式中使用角色管理，LoginView 控制項可以根據使用者角色來顯示特定的範本。 （稍後會涵蓋 ASP.NET 角色管理的詳細資訊。）

## <a name="passwordrecovery-control"></a>PasswordRecovery 控制項

PasswordRecovery 控制項可讓使用者使用其目前的密碼來接收電子郵件，或重設其密碼。 純文字和加密密碼可以復原，並以電子郵件傳送給使用者。 如果密碼已雜湊，則無法復原。 相反地，使用者將需要執行密碼重設。

## <a name="loginstatus-control"></a>LoginStatus 控制項

LoginStatus 控制項是用來對未登入的使用者，以及目前登入的使用者顯示登出指示器。 IsAuthenticated 屬性是用來決定要顯示的指標。 LoginStatus 控制項所顯示的指標可以是文字（透過**LoginText**和**LogoutText**屬性實作為）或影像（透過**LoginImageUrl**和**LogoutImageUrl**屬性實作為實）。

當使用者透過 LoginStatus 控制項登出時，會將他或她重新導向至**LogoutPageUrl**屬性所指定的 URL。 如果未設定該屬性，則會重新整理目前的頁面。 由於網站可能受到表單驗證的保護，因此目前頁面的重新整理會將使用者重新導向至網站的登入頁面。

## <a name="loginname-control"></a>LoginName 控制項

LoginName 控制項會顯示目前登入網站的使用者名稱。

## <a name="createuserwizard-control"></a>CreateUserWizard 控制項

CreateUserWizard 控制項提供使用者一個便利的方式來註冊您的成員資格系統。 您可以透過如下所示的介面，新增步驟（實作為 WizardSteps 的集合）。

![](membership/_static/image5.jpg)

**圖5**

CreateUserWizard 是衍生自 Wizard 類別的樣板化控制項，並提供下列範本：

- **System.windows.controls.headereditemscontrol.headertemplate**此範本控制 wizard 標頭的外觀。
- **SidebarTemplate**此範本控制 wizard 提要欄位的外觀。
- **StartNavigationTemplate**此範本會在開始步驟中控制流覽的外觀。
- **StepNavigationTemplate**此範本控制流覽區域的外觀，而不是在 [開始] 或 [完成] 步驟中。
- **FinishNavigationTemplate**此範本會在完成步驟時控制流覽區域的外觀。

此外，針對您新增至 Wizard 的每個步驟，ASP.NET 都會建立一個自訂範本，其中同時包含該步驟的 ContentTemplate 和 CustomNavigationTemplate。 如需自訂 CreateUserWizard 的完整詳細資料，請參閱 VS.NET 2005 檔：

## <a name="changepassword-control"></a>ChangePassword 控制項

ChangePassword 控制項可讓使用者變更其密碼。 如果 DisplayUserName 屬性為 true （預設為 false），則使用者可以在未登入時變更其密碼。 如果使用者已經登入，而且 DisplayUserName 屬性為 true，*使用者就能夠*變更另一位未登入使用者的密碼，讓他們知道該使用者的使用者識別碼。

請記住，如果您想要讓使用者能夠在不登入的情況下變更密碼，您必須確定顯示 ChangePassword 控制項的頁面允許匿名存取。 很明顯地，使用者必須提供其舊密碼，才能變更其密碼。

## <a name="role-management"></a>角色管理

角色管理可讓您將使用者指派給特定角色，然後根據該角色來限制對特定檔案或資料夾的存取權。 角色管理也會提供 API，讓您以程式設計方式判斷更輕鬆地角色，或判斷特定角色中的所有使用者，並據以回應。

角色管理不是 ASP.NET 成員資格的需求，也不需要成員資格就能使用角色管理。 不過，這兩個補充程式都很好，而開發人員可能會將它們彼此搭配使用。

若要在您的應用程式中啟用角色管理，請在 web.config 檔案中進行下列變更：

[!code-xml[Main](membership/samples/sample2.xml)]

當**cacheRolesInCookie**屬性設定為 true 時，ASP.NET 會在用戶端上的 cookie 中快取使用者角色成員資格。 這可讓角色查閱進行，而不需要呼叫 RoleProvider。 使用此屬性時，建議開發人員確保**cookieProtection**屬性設定為 All。 （這是預設設定）。這可確保 cookie 資料經過加密，並協助確保 cookie 內容尚未改變。 您可以使用 [網站管理工具] 來新增角色。 它可讓您輕鬆地定義角色、根據這些角色設定網站元件的存取權，以及將使用者指派給角色。

![](membership/_static/image6.jpg)

**圖6**

如上所示，只要輸入角色的名稱，然後按一下 [新增角色]，即可新增角色。 按一下現有角色清單中的適當連結，即可管理或刪除現有的角色。

當您管理角色時，您可以新增或移除使用者，如下所示。

![](membership/_static/image7.jpg)

**圖7**

藉由勾選 [使用者為角色] 核取方塊，您可以輕鬆地將使用者新增至特定角色。 ASP.NET 會自動以適當的專案更新您的成員資格資料庫。 您也會想要設定應用程式的存取規則。 ASP.NET 1.x 開發人員很熟悉如何透過 web.config 檔案中的 &lt;authorization&gt; 元素進行這項作業，而且 ASP.NET 2.0 中仍提供該選項。 不過，使用網站管理工具來管理存取規則的方式較簡單，如下所示。

![](membership/_static/image8.jpg)

**圖8**

在此情況下，系統管理資料夾會反白顯示（很難以看出，因為工具會以淺灰色醒目提示），而且系統管理員角色已被授與存取權。 所有其他使用者都會遭到拒絕。 您可以按一下 head 圖示來選取規則，然後使用 [上移] 和 [下移] 按鈕來排列規則。 如同 ASP.NET &lt;授權&gt; 元素，規則會依照其出現的順序進行處理。 換句話說，如果上述的程式中的規則順序已反轉，則沒有人可以存取 [系統管理] 資料夾，因為 ASP.NET 會遇到的第一個規則是拒絕每個使用者加入該資料夾的規則。

ASP.NET 2.0 會將 web.config 檔案新增至您要為其指定存取規則的資料夾。 您可以透過設定檔或透過網站管理工具來編輯存取規則。 換句話說，網站管理工具只是一個介面，可以在使用者易記的環境中編輯設定檔。

## <a name="using-roles-in-code"></a>在程式碼中使用角色

自1.x 版起，角色管理的 API 尚未變更。 **IsInRole**方法是用來判斷使用者是否為特定角色。

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET 也會建立 RolePrincipal 實例，做為目前內容的成員。 RolePrincipal 物件可以用來取得使用者所屬的所有角色，如下所示：

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>使用 Rolegroup 搭配 LoginView 控制項

既然您已經瞭解角色管理和成員資格，讓我們來簡單地討論 LoginView 控制項如何利用 ASP.NET 2.0 中的這項功能。 如先前所討論，LoginView 控制項是一個樣板化控制項，其中預設包含兩個範本;AnonymousTemplate 和 LoggedInTemplate。 在 [LoginView 工作] 對話方塊中，是一個連結（如下所示），可讓您編輯 Rolegroup。

![](membership/_static/image9.jpg)

**圖9**

每個 RoleGroup 物件都包含一個字串陣列，用以定義 RoleGroup 適用的角色。 若要將新的 RoleGroup 加入至 LoginView 控制項，請按一下 [編輯 Rolegroup] 連結。 在上圖中，您可以看到我已為系統管理員加入新的 RoleGroup。 藉由從 [Views] 下拉式清單中選取該 RoleGroup （RoleGroup [0]），我可以設定只會向系統管理員角色成員顯示的範本。 在下圖中，我加入了新的 RoleGroup，它會套用至 Sales 角色的成員和散發角色。 這會將第二個 RoleGroup 新增至 [LoginView 工作] 對話方塊中的 [Views] 下拉式清單，而任何加入該範本的專案將會由 [銷售] 或 [散發] 角色中的任何使用者顯示。

![](membership/_static/image10.jpg)

**圖10**

## <a name="overriding-the-existing-membership-provider"></a>覆寫現有的成員資格提供者

有幾種方式可讓您擴充 ASP.NET 成員資格的功能。 首先，您可以很明顯地變更 SqlMembershipProvider 類別的現有功能，方法是從它繼承並覆寫其方法。 例如，如果您想要在建立使用者時執行自己的功能，您可以建立繼承自 SqlMembershipProvider 的自訂類別，如下所示：

[!code-csharp[Main](membership/samples/sample5.cs)]

另一方面，如果您想要建立自己的提供者（例如，將您的成員資格資訊儲存在 Access 資料庫中），您可以建立自己的提供者。

## <a name="creating-your-own-membership-provider"></a>建立您自己的成員資格提供者

若要建立您自己的成員資格提供者，首先您必須建立繼承自 MembershipProvider 類別的類別。 如果您使用 VB.NET，Visual Studio 2005 將會為您需要覆寫的所有方法新增存根。 如果您使用C#的是，您可以在其中加入 stub。

您將需要覆寫下列各項：

- ApplicationName 屬性
- ChangePassword 函數
- ChangePasswordQuestionAndAnswer 函式
- CreateUser 函式
- DeleteUser 函式
- EnablePasswordReset 屬性
- EnablePasswordRetrieval 屬性
- FindUsersByEmail 函式
- FindUsersByName 函式
- GetAllUsers 函式
- GetNumberOfUsersOnline 函式
- GetPassword 函式
- GetUser 函式
- GetUserNameByEmail 函式
- MaxInvalidPasswordAttempts 屬性
- MinRequiredNonAlphanumericCharacters 屬性
- MinRequiredPasswordLength 屬性
- PasswordAttemptWindow 屬性
- PasswordFormat 屬性
- PasswordStrengthRegularExpression 屬性
- RequiresQuestionAndAnswer 屬性
- RequiresUniqueEmail 屬性
- ResetPassword 函式
- 解除鎖定使用者函式
- UpdateUser 函式
- ValidateUser 函式

這是一份以C#開發人員的身分來執行的清單。 您可能會發現，在 VB.NET 中建立類別，而不需要任何執行，然後使用 .NET 反映程式或類似的工具，將C#程式碼轉換為。

連接字串和其他屬性應設定為 Initialize 方法中的預設值。 （在執行時間載入提供者時，會引發 Initialize 方法）。Initialize 方法的第二個參數是 NameValueCollection 類型，而且是與 web.config 檔案中自訂提供者相關聯之 &lt;加入&gt; 元素的參考。 該專案看起來如下所示：

[!code-xml[Main](membership/samples/sample6.xml)]

以下是 Initialize 方法的範例。

[!code-csharp[Main](membership/samples/sample7.cs)]

若要在提交登入表單時驗證使用者，您將需要使用 ValidateUser 方法。 這個方法會在使用者按一下登入控制項中的 [登入] 按鈕時引發。 您將會在此方法中放置執行使用者查閱的程式碼。

如您所見，撰寫自己的成員資格提供者並不容易，而且可讓您擴充 ASP.NET 2.0 的這項強大功能。
