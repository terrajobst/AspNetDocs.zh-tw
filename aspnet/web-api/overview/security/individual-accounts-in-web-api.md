---
uid: web-api/overview/security/individual-accounts-in-web-api
title: 在 ASP.NET Web API 2.2 中使用個別帳戶和本機登入保護 Web API |Microsoft Docs
author: MikeWasson
description: 本主題說明如何使用 OAuth2 來保護 Web API，以根據成員資格資料庫進行驗證。 教學課程中使用的軟體版本 Visual Studio 201 。
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555192"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a>在 ASP.NET Web API 2.2 中使用個別帳戶和本機登入保護 Web API

由[Mike Wasson](https://github.com/MikeWasson)

[下載範例應用程式](https://github.com/MikeWasson/LocalAccountsApp)

> 本主題說明如何使用 OAuth2 來保護 Web API，以根據成員資格資料庫進行驗證。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - [Visual Studio 2013 Update 3](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [Web API 2。2](../releases/whats-new-in-aspnet-web-api-22.md)
> - [ASP.NET Identity 2。1](../../../identity/index.md)

在 Visual Studio 2013 中，Web API 專案範本提供三個驗證選項：

- **個別帳戶。** 應用程式會使用成員資格資料庫。
- **組織帳戶。** 使用者使用其 Azure Active Directory、Office 365 或內部部署 Active Directory 認證登入。
- **Windows 驗證。** 此選項適用于內部網路應用程式，並使用 Windows 驗證 IIS 模組。

如需這些選項的詳細資訊，請參閱[在 Visual Studio 2013 中建立 ASP.NET Web 專案](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)。

個別帳戶提供兩種方式讓使用者登入：

- **本機登**入。 使用者會在網站上註冊，並輸入使用者名稱和密碼。 應用程式會將密碼雜湊儲存在成員資格資料庫中。 當使用者登入時，ASP.NET Identity 系統會驗證密碼。
- **社交登**入。 使用者使用外部服務（例如 Facebook、Microsoft 或 Google）登入。 應用程式仍會在成員資格資料庫中建立使用者的專案，但不會儲存任何認證。 使用者藉由登入外部服務來進行驗證。

本文探討本機登入案例。 針對本機和社交登入，Web API 會使用 OAuth2 來驗證要求。 不過，本機和社交登入的認證流程會不同。

在本文中，我將示範一個簡單的應用程式，讓使用者登入並將已驗證的 AJAX 呼叫傳送至 Web API。 您可以在[這裡](https://github.com/MikeWasson/LocalAccountsApp)下載範例程式碼。 讀我檔案說明如何在 Visual Studio 中從頭開始建立範例。

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

範例應用程式會針對資料系結和 jQuery 使用「挖式 .js」來傳送 AJAX 要求。 我將把焦點放在 AJAX 呼叫，所以您不需要知道這篇文章的挖的 .js。

在過程中，我將說明：

- 應用程式在用戶端上執行的作業。
- 伺服器上的情況。
- 在中間的 HTTP 流量。

首先，我們需要定義一些 OAuth2 的術語。

- *資源*。 可以保護的部分資料。
- *資源伺服器*。 裝載資源的伺服器。
- *資源擁有*者。 可以授與資源存取權的實體。 （通常是使用者）。
- *用戶端*：想要存取資源的應用程式。 在本文中，用戶端是網頁瀏覽器。
- *存取權杖*。 授與資源存取權的權杖。
- *持有人權杖*。 特定類型的存取權杖，其中包含任何人都可以使用權杖的屬性。 換句話說，用戶端不需要密碼編譯金鑰或其他秘密，也能使用持有人權杖。 基於這個理由，持有人權杖只能透過 HTTPS 使用，而且應該要有相對較短的到期時間。
- *授權伺服器*。 提供存取權杖的伺服器。

應用程式可以同時做為授權伺服器和資源伺服器。 Web API 專案範本會遵循此模式。

## <a name="local-login-credential-flow"></a>本機登入認證流程

針對本機登入，Web API 會使用 OAuth2 中所定義的[資源擁有者密碼流程](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html)。

1. 使用者在用戶端輸入名稱和密碼。
2. 用戶端會將這些認證傳送給授權伺服器。
3. 授權伺服器會驗證認證，並傳回存取權杖。
4. 若要存取受保護的資源，用戶端會在 HTTP 要求的 Authorization 標頭中包含存取權杖。

![](individual-accounts-in-web-api/_static/image3.png)

當您選取 [Web API] 專案範本中的**個別帳戶**時，專案會包含驗證使用者認證和發行權杖的授權伺服器。 下圖顯示與 Web API 元件相同的認證流程。

![](individual-accounts-in-web-api/_static/image4.png)

在此案例中，Web API 控制器會作為資源伺服器。 驗證篩選器會驗證存取權杖，而 **[授權]** 屬性則是用來保護資源。 當控制器或動作具有 **[授權]** 屬性時，所有對該控制器或動作的要求都必須經過驗證。 否則，會拒絕授權，而 Web API 會傳回401（未經授權）錯誤。

授權伺服器和驗證篩選準則都會呼叫[OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)元件，以處理 OAuth2 的詳細資料。 我稍後會在本教學課程中詳細說明此設計。

## <a name="sending-an-unauthorized-request"></a>傳送未經授權的要求

若要開始使用，請執行應用程式，然後按一下 [**呼叫 API** ] 按鈕。 當要求完成時，您應該會在 [**結果**] 方塊中看到錯誤訊息。 這是因為要求未包含存取權杖，因此要求未經授權。

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

[**呼叫 API** ] 按鈕會將 AJAX 要求傳送至 ~/api/values，這會叫用 Web API 控制器動作。 以下是傳送 AJAX 要求的 JavaScript 程式碼區段。 在範例應用程式中，所有的 JavaScript 應用程式程式碼都位於 Scripts\app.js 檔案中。

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

在使用者登入之前，不會有任何持有人權杖，因此要求中不會有任何授權標頭。 這會導致要求傳回401錯誤。

以下是 HTTP 要求。 （我使用[Fiddler](http://www.telerik.com/fiddler)來捕捉 HTTP 流量）。

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

HTTP 回應：

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

請注意，回應會包含 Www 驗證標頭，並將挑戰設定為 [持有人]。 這表示伺服器預期持有人權杖。

## <a name="register-a-user"></a>註冊使用者

在應用程式的 [**註冊**] 區段中，輸入電子郵件和密碼，然後按一下 [**註冊**] 按鈕。

您不需要在此範例中使用有效的電子郵件地址，但實際的應用程式會確認此位址。 （請參閱[使用登入、電子郵件確認和密碼重設建立安全的 ASP.NET MVC 5 web 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)）。在 [密碼] 中，使用以大寫字母、小寫字母、數位和非英數位元等字元做為 "Password1！"。 為了讓應用程式保持簡單，我會省略用戶端驗證，因此如果密碼格式發生問題，您會收到400（不正確的要求）錯誤。

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

[**註冊**] 按鈕會將 POST 要求傳送至 ~/api/Account/Register/。 要求主體是包含名稱和密碼的 JSON 物件。 以下是用來傳送要求的 JavaScript 程式碼：

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

HTTP 要求：

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

HTTP 回應：

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

此要求是由 `AccountController` 類別所處理。 就內部而言，`AccountController` 會使用 ASP.NET Identity 來管理成員資格資料庫。

如果您從 Visual Studio 在本機執行應用程式，則使用者帳戶會儲存在 LocalDB 的 AspNetUsers 資料表中。 若要在 Visual Studio 中查看資料表，請按一下 [ **view** ] 功能表，選取 [**伺服器總管**]，然後展開 [**資料連線**]。

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a>取得存取權杖

到目前為止，我們尚未完成任何 OAuth，但我們現在會在要求存取權杖時，看到 OAuth 授權伺服器的運作方式。 在範例應用程式的 [**登入**] 區域中，輸入電子郵件和密碼，然後按一下 [**登入**]。

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

[**登入**] 按鈕會將要求傳送至權杖端點。 要求的主體包含下列表單 url 編碼的資料：

- 授與\_類型：「密碼」
- username： &lt;使用者的電子郵件&gt;
- 密碼： &lt;密碼&gt;

以下是傳送 AJAX 要求的 JavaScript 程式碼：

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

如果要求成功，則授權伺服器會在回應主體中傳回存取權杖。 請注意，我們會將權杖儲存在會話儲存體中，以便稍後將要求傳送至 API 時使用。 不同于某些形式的驗證（例如以 cookie 為基礎的驗證），瀏覽器不會在後續要求中自動包含存取權杖。 應用程式必須明確地執行此動作。 這是件好事，因為它會限制[CSRF 的弱點](preventing-cross-site-request-forgery-csrf-attacks.md)。

HTTP 要求：

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

您可以看到要求包含使用者的認證。 您*必須*使用 HTTPS 來提供傳輸層安全性。

HTTP 回應：

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

為了方便起見，我已縮排 JSON 並截斷存取權杖，這是相當長的時間。

`access_token`、`token_type`和 `expires_in` 屬性是由 OAuth2 規格所定義。其他屬性（`userName`、`.issued`和 `.expires`）僅供資訊參考之用。 在/Providers/ApplicationOAuthProvider.cs 檔案中，您可以在 `TokenEndpoint` 方法中找到新增這些額外屬性的程式碼。

## <a name="send-an-authenticated-request"></a>傳送已驗證的要求

既然我們已擁有持有人權杖，我們就可以向 API 提出已驗證的要求。 這是藉由在要求中設定 Authorization 標頭來完成。 再次按一下 [**呼叫 API** ] 按鈕以查看此情況。

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

HTTP 要求：

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

HTTP 回應：

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a>登出

因為瀏覽器不會快取認證或存取權杖，所以登出只是「忘記」權杖，方法是從會話儲存體中移除它：

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a>瞭解個別帳戶專案範本

當您選取 ASP.NET Web 應用程式專案範本中的**個別帳戶**時，專案會包含：

- OAuth2 授權伺服器。
- 用於管理使用者帳戶的 Web API 端點
- 用來儲存使用者帳戶的 EF 模型。

以下是用來執行這些功能的主要應用程式類別：

- `AccountController` 提供用來管理使用者帳戶的 Web API 端點。 `Register` 動作是我們在本教學課程中唯一使用的動作。 類別上的其他方法則支援密碼重設、社交登入和其他功能。
- `ApplicationUser`，定義于/Models/IdentityModels.cs。 這個類別是成員資格資料庫中使用者帳戶的 EF 模型。
- `ApplicationUserManager`（定義于/App\_Start/IdentityConfig）。此類別衍生自[UserManager](https://msdn.microsoft.com/library/dn613290.aspx)並在使用者帳戶上執行作業，例如建立新的使用者、驗證密碼等等，並自動儲存資料庫的變更。
- `ApplicationOAuthProvider` 此物件會插入至 OWIN 中介軟體，並處理中介軟體所引發的事件。 它衍生自[OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)。

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a>設定授權伺服器

在 StartupAuth.cs 中，下列程式碼會設定 OAuth2 授權伺服器。

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

`TokenEndpointPath` 屬性是授權伺服器端點的 URL 路徑。 這是應用程式用來取得持有人權杖的 URL。

`Provider` 屬性指定的提供者會插入 OWIN 中介軟體，並處理中介軟體所引發的事件。

以下是應用程式想要取得權杖的基本流程：

1. 若要取得存取權杖，應用程式會將要求傳送至 ~/Token。
2. OAuth 中介軟體會呼叫提供者上 `GrantResourceOwnerCredentials`。
3. 提供者會呼叫 `ApplicationUserManager` 來驗證認證，並建立宣告身分識別。
4. 如果成功，提供者會建立驗證票證，用來產生權杖。

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

OAuth 中介軟體不知道使用者帳戶的任何內容。 提供者會在中介軟體和 ASP.NET Identity 之間進行通訊。 如需有關如何執行授權伺服器的詳細資訊，請參閱[OWIN OAuth 2.0 Authorization server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)。

### <a name="configuring-web-api-to-use-bearer-tokens"></a>設定 Web API 以使用持有人權杖

在 `WebApiConfig.Register` 方法中，下列程式碼會設定 Web API 管線的驗證：

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

**HostAuthenticationFilter**類別可讓您使用持有人權杖進行驗證。

**Config.suppressdefaulthostauthentication**方法會指示 Web api 忽略在要求抵達 Web api 管線之前，由 IIS 或 OWIN 中介軟體所發生的任何驗證。 如此一來，我們可以限制 Web API 只驗證使用持有人權杖的要求。

> [!NOTE]
> 特別是，您應用程式的 MVC 部分可能會使用表單驗證，這會將認證儲存在 cookie 中。 以 Cookie 為基礎的驗證需要使用防偽權杖，以防止 CSRF 攻擊。 這是 web Api 的問題，因為 Web API 無法方便地將防偽權杖傳送給用戶端。 （如需此問題的詳細背景，請參閱[防止 WEB API 中的 CSRF 攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)）。呼叫**config.suppressdefaulthostauthentication**可確保 Web API 不容易受到 cookie 中儲存之認證的 CSRF 攻擊。

當用戶端要求受保護的資源時，以下是 Web API 管線中發生的情況：

1. **HostAuthentication**篩選準則會呼叫 OAuth 中介軟體來驗證權杖。
2. 中介軟體會將權杖轉換成宣告身分識別。
3. 此時，要求已*通過驗證*，但未*獲授權*。
4. 授權篩選準則會檢查宣告身分識別。 如果宣告會授權該資源的使用者，則要求已獲得授權。 根據預設， **[授權]** 屬性會授權任何已驗證的要求。 不過，您可以依角色或其他宣告進行授權。 如需詳細資訊，請參閱[WEB API 中的驗證和授權](authentication-and-authorization-in-aspnet-web-api.md)。
5. 如果先前的步驟成功，控制器會傳回受保護的資源。 否則，用戶端會收到401（未經授權）錯誤。

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a>其他資源

- [ASP.NET Identity](../../../identity/index.md)
- [瞭解 VS2013 RC 的 SPA 範本中的安全性功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)。 Hongye Sun 的 MSDN blog 文章。
- [剖析 WEB API 個別帳戶範本-第2部分：本機帳戶](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)。 Dominick Baier 的 Blog 文章。
- [主機驗證和使用 OWIN 的 WEB API](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)。 Brock Allen 的 `SuppressDefaultHostAuthentication` 和 `HostAuthenticationFilter` 的良好說明。
- [在 VS 2013 範本的 ASP.NET Identity 中自訂設定檔資訊](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)。 MSDN blog 文章，請 Pranav 請參閱 rastogi。
- [ASP.NET Identity 中 UserManager 類別的每個要求存留期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。 MSDN blog 文章，請 Suhas Joshi，並提供 `UserManager` 類別的良好說明。
