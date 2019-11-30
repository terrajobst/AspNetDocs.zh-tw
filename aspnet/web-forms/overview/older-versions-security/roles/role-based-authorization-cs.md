---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-cs
title: 以角色為基礎的C#授權（） |Microsoft Docs
author: rick-anderson
description: 本教學課程一開始會探討角色架構如何讓使用者的角色與他的安全性內容產生關聯。 然後，它會檢查如何套用以角色為基礎的 URL 。
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 4d9b63fa-c3d4-4e85-82b1-26ae3ba3ca1c
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 46153ab310bdee814baaa53c372fb92f8a23ce11
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619673"
---
# <a name="role-based-authorization-c"></a>以角色為基礎的授權 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.11.zip)或[下載 PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_cs.pdf)

> 本教學課程一開始會探討角色架構如何讓使用者的角色與他的安全性內容產生關聯。 然後，它會檢查如何套用以角色為基礎的 URL 授權規則。 之後，我們將探討如何使用宣告式和程式設計方式來改變顯示的資料，以及 ASP.NET 網頁所提供的功能。

## <a name="introduction"></a>簡介

在以<a id="_msoanchor_1"> </a>[*使用者為基礎的授權*](../membership/user-based-authorization-cs.md)教學課程中，我們已瞭解如何使用 URL 授權來指定使用者可以造訪一組特定頁面的內容。 在 `Web.config`中只有一些標記，我們可以指示 ASP.NET 只允許已驗證的使用者流覽頁面。 或者，我們可以決定只允許 Tito 和 Bob 的使用者，或指出所有已驗證的使用者（Sam 除外）都是允許的。

除了 URL 授權之外，我們也探討了用來控制所顯示資料的宣告式和程式設計技術，以及根據使用者造訪的網頁所提供的功能。 特別是，我們建立了一個頁面，其中列出目前目錄的內容。 任何人都可以造訪此頁面，但只有經過驗證的使用者才能看到檔案的內容，而且只有 Tito 可以刪除檔案。

以使用者為基礎來套用授權規則，可能會增加到簿記的麻煩。 更容易維護的方法是使用以角色為基礎的授權。 好消息是，我們用來套用授權規則的工具，與角色一樣適用于使用者帳戶。 URL 授權規則可以指定角色，而不是使用者。 針對已驗證和匿名使用者呈現不同輸出的 LoginView 控制項，可以設定為根據登入使用者的角色來顯示不同的內容。 角色 API 包含用來判斷登入使用者角色的方法。

本教學課程一開始會探討角色架構如何讓使用者的角色與他的安全性內容產生關聯。 然後，它會檢查如何套用以角色為基礎的 URL 授權規則。 之後，我們將探討如何使用宣告式和程式設計方式來改變顯示的資料，以及 ASP.NET 網頁所提供的功能。 讓我們開始吧！

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>瞭解角色如何與使用者的安全性內容產生關聯

每當要求進入 ASP.NET 管線時，它就會與安全性內容相關聯，其中包括識別要求者的資訊。 使用表單驗證時，會使用驗證票證作為身分識別權杖。 如我們在<a id="_msoanchor_2"> </a>「[*表單驗*](../introduction/an-overview-of-forms-authentication-cs.md)證」和<a id="_msoanchor_3"> </a>「表單驗證」設定和「[*高級主題*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)」教學課程中所討論，`FormsAuthenticationModule` 會負責判斷要求者的身分識別，這在[`AuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)期間會執行。

如果找到有效、未過期的驗證票證，`FormsAuthenticationModule` 會將其解碼，以確定要求者的身分識別。 它會建立新的 `GenericPrincipal` 物件，並將它指派給 `HttpContext.User` 物件。 主體的用途（例如 `GenericPrincipal`）是識別已驗證使用者的名稱，以及她所屬的角色。 這是因為所有的主體物件都有一個 `Identity` 屬性和一個 `IsInRole(roleName)` 方法，這是顯而易見的。 不過，`FormsAuthenticationModule`不想要記錄角色資訊，而它所建立的 `GenericPrincipal` 物件不會指定任何角色。

如果已啟用角色架構， [`RoleManagerModule`](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx)的 HTTP 模組會在 `FormsAuthenticationModule` 後的步驟，並在[`PostAuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)期間識別已驗證使用者的角色，這會在 `AuthenticateRequest` 事件之後引發。 如果要求是來自已驗證的使用者，則 `RoleManagerModule` 會覆寫 `FormsAuthenticationModule` 所建立的 `GenericPrincipal` 物件，並將它取代為[`RolePrincipal` 物件](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)。 `RolePrincipal` 類別會使用角色 API 來判斷使用者屬於哪些角色。

[圖 1] 描述使用表單驗證和角色架構時的 ASP.NET 管線工作流程。 `FormsAuthenticationModule` 會先執行，並透過她的驗證票證來識別使用者，並建立新的 `GenericPrincipal` 物件。 接下來，`RoleManagerModule` 中的步驟，並使用 `RolePrincipal` 物件覆寫 `GenericPrincipal` 物件。

如果匿名使用者造訪網站，則 `FormsAuthenticationModule` 或 `RoleManagerModule` 都不會建立主體物件。

[使用表單驗證和角色架構時，![已驗證使用者的 ASP.NET 管線事件](role-based-authorization-cs/_static/image2.png)](role-based-authorization-cs/_static/image1.png)

**圖 1**：使用表單驗證和角色架構時，已驗證使用者的 ASP.NET 管線事件（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image3.png)）

### <a name="caching-role-information-in-a-cookie"></a>在 Cookie 中快取角色資訊

`RolePrincipal` 物件的 `IsInRole(roleName)` 方法會呼叫 `Roles.GetRolesForUser` 來取得使用者的角色，以便判斷使用者是否為擁有*者的成員。* 使用 `SqlRoleProvider`時，這會導致對角色存放區資料庫進行查詢。 使用以角色為基礎的 URL 授權規則時，將會針對每個對受角色型 URL 授權規則保護之頁面的要求，呼叫 `RolePrincipal`的 `IsInRole` 方法。 角色架構包含一個選項，可在 cookie 中快取使用者的角色，而不需要在每個要求中查閱資料庫中的角色資訊。

如果角色架構設定為在 cookie 中快取使用者的角色，則 `RoleManagerModule` 會在 ASP.NET 管線的[`EndRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)期間建立 cookie。 這個 cookie 會用於 `PostAuthenticateRequest`中的後續要求，也就是建立 `RolePrincipal` 物件時。 如果 cookie 有效且尚未過期，cookie 中的資料會經過剖析並用來填入使用者的角色，藉此儲存 `RolePrincipal`，使其不需要呼叫 `Roles` 類別來判斷使用者的角色。 [圖 2] 說明此工作流程。

[![使用者的角色資訊可以儲存在 Cookie 中以改善效能](role-based-authorization-cs/_static/image5.png)](role-based-authorization-cs/_static/image4.png)

**圖 2**：使用者的角色資訊可以儲存在 Cookie 中以改善效能（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image6.png)）

角色快取 cookie 機制預設為停用。 您可以透過 `Web.config`中的 `<roleManager>` 設定標記來啟用它。 我們已在<a id="_msoanchor_4"> </a>[*建立和管理角色*](creating-and-managing-roles-cs.md)教學課程中，使用[`<roleManager>`](https://msdn.microsoft.com/library/ms164660.aspx)專案來指定角色提供者，因此您在應用程式的 `Web.config` 檔中應該已經有這個元素。 角色快取 cookie 設定會指定為 `<roleManager>` 元素的屬性，並在 [表 1] 中摘要說明。

> [!NOTE]
> [表 1] 中所列的設定會指定所產生之角色快取 cookie 的屬性。 如需 cookie、其使用方式和其各種屬性的詳細資訊，請閱讀[此 cookie 教學](http://www.quirksmode.org/js/cookies.html)課程。

| <strong>Property</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>說明</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              布林值，指出是否使用 cookie 快取。 預設值為 `false`。                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     角色快取 cookie 的名稱。 預設值為 "。ASPXROLES".                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                角色名稱 cookie 的路徑。 Path 屬性可讓開發人員將 cookie 的範圍限制為特定的目錄階層。 預設值為 "/"，這會通知瀏覽器將驗證票證 cookie 傳送至對網域提出的任何要求。                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               指出用來保護角色快取 cookie 的技術。 允許的值為： `All` （預設值）;`Encryption`;`None`;和 `Validation`。 如需這些保護層級的<a id="_anchor_5"></a>詳細資訊，請參閱[*表單驗證設定和 Advanced 主題*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教學課程的步驟3。                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   布林值，指出是否需要 SSL 連線才能傳輸驗證 cookie。 預設值是 `false`。                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  布林值，指出每次使用者在單一會話中造訪網站時，是否重設 cookie 的超時時間。 預設值是 `false`。 只有當 `createPersistentCookie` 設定為 `true`時，這個值才會相關。                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         指定驗證票證 cookie 到期的時間（以分鐘為單位）。 預設值是 `30`。 只有當 `createPersistentCookie` 設定為 `true`時，這個值才會相關。                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   布林值，指定角色快取 cookie 是否為會話 cookie 或持續性 cookie。 如果 `false` （預設值），則會使用會話 cookie，這會在瀏覽器關閉時被刪除。 如果 `true`，則會使用持續性的 cookie;根據 `cookieSlidingExpiration`的值，它會在建立後或在上一次造訪之後 `cookieTimeout` 分鐘數到期。                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 指定 cookie 的網域值。 預設值為空字串，這會導致瀏覽器使用其發行所在的網域（例如 www.yourdomain.com）。 在此情況下，對子域進行要求時，<strong>不</strong>會傳送 cookie，例如 admin.yourdomain.com。 如果您想要將 cookie 傳遞給所有子域，您需要自訂 `domain` 屬性，並將其設定為 "yourdomain.com"。                                                                                                                                                 |
|    `maxCachedResults`     | 指定在 cookie 中快取的角色名稱數目上限。 預設值為 25。 `RoleManagerModule` 不會為屬於超過 `maxCachedResults` 角色的使用者建立 cookie。 因此，`RolePrincipal` 物件的 `IsInRole` 方法會使用 `Roles` 類別來判斷使用者的角色。 `maxCachedResults` 存在的原因是因為許多使用者代理程式不允許大於4096個位元組的 cookie。 因此，此上限的目的是要降低超過此大小限制的可能性。 如果您有非常長的角色名稱，您可能會想要考慮指定較小的 `maxCachedResults` 值。contrariwise，如果您有極短的角色名稱，您可能會增加此值。 |

**表1：** 角色快取 Cookie 設定選項

讓我們將應用程式設定為使用非持續性角色快取 cookie。 若要完成這項操作，請更新 `Web.config` 中的 `<roleManager>` 元素，以包含下列與 cookie 相關的屬性：

[!code-xml[Main](role-based-authorization-cs/samples/sample1.xml)]

我藉由新增三個屬性來更新 `<roleManager>` 元素： `cacheRolesInCookie`、`createPersistentCookie`和 `cookieProtection`。 藉由將 `cacheRolesInCookie` 設定為 `true`，`RoleManagerModule` 現在會自動在 cookie 中快取使用者的角色，而不需要在每個要求上查閱使用者的角色資訊。 我明確地將 `createPersistentCookie` 和 `cookieProtection` 屬性分別設定為 `false` 和 `All`。 就技術上而言，我不需要指定這些屬性的值，因為我只是將它們指派給它們的預設值，但是我將它們放在這裡，明確地清楚我不使用持續性 cookie，而且 cookie 已加密並經過驗證。

這樣就全部完成了！ 因而需要，Roles 架構會在 cookie 中快取使用者的角色。 如果使用者的瀏覽器不支援 cookie，或其 cookie 遭到刪除或遺失，則不會有任何大的差別– `RolePrincipal` 物件只會在沒有 cookie （或無效或過期）可用時，才使用 `Roles` 類別。

> [!NOTE]
> Microsoft 的模式 &amp; 實務小組不鼓勵使用持續性角色快取 cookie。 由於擁有角色快取 cookie 足以證明角色成員資格，因此，如果駭客能夠以某種方式存取有效的使用者 cookie，他就可以模擬該使用者。 如果 cookie 保存在使用者的瀏覽器上，這種情況的可能性就會增加。 如需有關此安全性建議的詳細資訊，以及其他安全性考慮，請參閱[ASP.NET 2.0 的安全性問題清單](https://msdn.microsoft.com/library/ms998375.aspx)。

## <a name="step-1-defining-role-based-url-authorization-rules"></a>步驟1：定義以角色為基礎的 URL 授權規則

如以使用者為<a id="_msoanchor_6"> </a>[*基礎的授權*](../membership/user-based-authorization-cs.md)教學課程中所述，URL 授權提供了一種方法，可依使用者或角色逐一限制存取一組頁面。 URL 授權規則會在 `Web.config` 中使用[`<authorization>` 元素](https://msdn.microsoft.com/library/8d82143t.aspx)搭配 `<allow>` 和 `<deny>` 子項目。 除了先前教學課程中所討論的使用者相關授權規則以外，每個 `<allow>` 和 `<deny>` 子項目也可以包含：

- 特定角色
- 以逗號分隔的角色清單

例如，URL 授權規則會授與系統管理員和主管角色中這些使用者的存取權，但拒絕所有其他人的存取：

[!code-xml[Main](role-based-authorization-cs/samples/sample2.xml)]

上述標記中的 `<allow>` 元素會指出允許系統管理員和主管角色;`<deny>` 元素會指示*所有*使用者都會遭到拒絕。

讓我們設定應用程式，以便只有系統管理員角色的使用者可以存取 [`ManageRoles.aspx`]、[`UsersAndRoles.aspx`] 和 [`CreateUserWizardWithRoles.aspx`] 頁面，而 [`RoleBasedAuthorization.aspx`] 頁面仍然可供所有訪客存取。

若要完成這項操作，請從將 `Web.config` 檔案新增至 `Roles` 資料夾開始。

[![將 Web.config 檔案新增至 Roles 目錄](role-based-authorization-cs/_static/image8.png)](role-based-authorization-cs/_static/image7.png)

**圖 3**：將 `Web.config` 檔案新增至 `Roles` 目錄（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image9.png)）

接下來，將下列設定標記新增至 `Web.config`：

[!code-xml[Main](role-based-authorization-cs/samples/sample3.xml)]

[`<system.web>`] 區段中的 [`<authorization>`] 元素指出只有系統管理員角色中的使用者可以存取 `Roles` 目錄中的 ASP.NET 資源。 `<location>` 元素會為 `RoleBasedAuthorization.aspx` 頁面定義一組替代的 URL 授權規則，讓所有使用者都能造訪該頁面。

將變更儲存至 `Web.config`之後，以不在系統管理員角色中的使用者身分登入，然後嘗試造訪其中一個受保護的頁面。 `UrlAuthorizationModule` 會偵測到您沒有流覽所要求資源的許可權;因此，`FormsAuthenticationModule` 會將您重新導向至登入頁面。 接著，登入頁面會將您重新導向至 [`UnauthorizedAccess.aspx`] 頁面（請參閱 [圖 4]）。 這最後從登入頁面重新導向至 `UnauthorizedAccess.aspx` 的原因是，我們已將程式碼新增至以使用者為<a id="_msoanchor_7"> </a>[*基礎的授權*](../membership/user-based-authorization-cs.md)教學課程步驟2中的登入頁面。 特別的是，如果 querystring 包含 `ReturnUrl` 參數，則登入頁面會自動將任何已驗證的使用者重新導向至 `UnauthorizedAccess.aspx`，因為此參數表示使用者在嘗試查看未獲授權觀看的頁面之後，抵達登入頁面。

[僅 ![系統管理員角色中的使用者可以查看受保護的頁面](role-based-authorization-cs/_static/image11.png)](role-based-authorization-cs/_static/image10.png)

**圖 4**：只有系統管理員（Administrators）角色的使用者可以查看受保護的頁面（[按一下以觀看完整大小的影像](role-based-authorization-cs/_static/image12.png)）

登出，然後以系統管理員角色的使用者身分登入。 現在您應該可以看到這三個受保護的頁面。

[![Tito 可以造訪 UsersAndRoles 頁面，因為他是在系統管理員角色中](role-based-authorization-cs/_static/image14.png)](role-based-authorization-cs/_static/image13.png)

**圖 5**： Tito 可以造訪 `UsersAndRoles.aspx` 頁面，因為他是系統管理員角色（[按一下以觀看完整大小的影像](role-based-authorization-cs/_static/image15.png)）

> [!NOTE]
> 指定 URL 授權規則時-針對角色或使用者-請務必記住，規則會從上到下逐一分析一次。 一旦找到相符專案，就會根據是否在 `<allow>` 或 `<deny>` 元素中找到相符專案，授與或拒絕使用者存取。 **如果找不到相符的，則會授與使用者存取權。** 因此，如果您想要限制對一個或多個使用者帳戶的存取，請務必使用 `<deny>` 元素做為 URL 授權設定中的最後一個元素。 **如果您的 URL 授權規則未包含**`<deny>`**元素，則所有使用者都會被授與存取權。** 如需有關如何分析 URL 授權規則的詳細討論，請參閱以<a id="_msoanchor_8"> </a>[*使用者為基礎的授權*](../membership/user-based-authorization-cs.md)教學課程中的「查看 `UrlAuthorizationModule` 如何使用授權規則來授與或拒絕存取」一節。

## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>步驟2：根據目前登入的使用者角色限制功能

[URL 授權] 可讓您輕鬆地指定粗略的授權規則，以指出允許的身分識別，以及哪些識別會被拒絕以查看特定頁面（或資料夾及其子資料夾中的所有頁面）。 不過，在某些情況下，我們可能會想要允許所有使用者流覽頁面，但根據造訪的使用者角色來限制網頁的功能。 這可能需要根據使用者的角色來顯示或隱藏資料，或為屬於特定角色的使用者提供額外的功能。

以宣告方式或以程式設計方式（或透過這兩個組合）來執行這類精細的角色型授權規則。 在下一節中，我們將瞭解如何透過 LoginView 控制項來執行宣告式精細的授權。 之後，我們將探索程式設計技巧。 不過，在查看如何套用精細的授權規則之前，我們必須先建立一個頁面，其功能取決於使用者造訪它的角色。

讓我們建立一個頁面，其中列出 GridView 中系統的所有使用者帳戶。 GridView 會包含每個使用者的使用者名稱、電子郵件地址、上次登入日期，以及使用者的相關批註。 除了顯示每個使用者的資訊之外，GridView 也會包含編輯和刪除功能。 我們一開始會建立此頁面，其中包含所有使用者都可使用的編輯和刪除功能。 在「使用 LoginView 控制項」和「以程式設計方式限制功能」章節中，我們將瞭解如何根據造訪的使用者角色來啟用或停用這些功能。

> [!NOTE]
> 我們即將建立的 ASP.NET 網頁會使用 GridView 控制項來顯示使用者帳戶。 由於本教學課程系列的重點在於表單驗證、授權、使用者帳戶和角色，因此我不想花太多時間來討論 GridView 控制項的內部運作。 雖然本教學課程提供設定此頁面的特定逐步指示，但並不會深入探討某些選擇的原因，或特定屬性對轉譯輸出的影響。 如需 GridView 控制項的完整檢查，請參閱我的 *[使用 ASP.NET 2.0 中的資料](../../data-access/index.md)* 教學課程系列。

從開啟 [`Roles`] 資料夾中的 [`RoleBasedAuthorization.aspx`] 頁面開始。 將 GridView 從頁面拖曳至設計工具，並將其 `ID` 設定為 [`UserGrid`]。 我們稍後會撰寫程式碼來呼叫 `Membership.GetAllUsers` 方法，並將產生的 `MembershipUserCollection` 物件系結至 GridView。 `MembershipUserCollection` 包含系統中每個使用者帳戶的 `MembershipUser` 物件;`MembershipUser` 物件的屬性如 `UserName`、`Email`、`LastLoginDate`等等。

在撰寫將使用者帳戶系結至方格的程式碼之前，讓我們先定義 GridView 的欄位。 從 GridView 的智慧標籤中，按一下 [編輯資料行] 連結以啟動 [欄位] 對話方塊（請參閱 [圖 6]）。 從這裡，取消核取左下角的 [自動產生欄位] 核取方塊。 由於我們想要這個 GridView 包含編輯和刪除功能，因此請新增 CommandField，並將其 `ShowEditButton` 和 `ShowDeleteButton` 屬性設定為 True。 接下來，加入四個欄位，以顯示 `UserName`、`Email`、`LastLoginDate`和 `Comment` 屬性。 針對這兩個可編輯的欄位（`Email` 和 `Comment`），使用 BoundField 做為兩個唯讀屬性（`UserName` 和 `LastLoginDate`）和 TemplateFields。

讓第一個 BoundField 顯示 `UserName` 屬性;將其 [`HeaderText`] 和 [`DataField` 屬性] 設定為 [使用者名稱]。 此欄位將無法編輯，因此請將其 `ReadOnly` 屬性設定為 True。 將 [`LastLoginDate` BoundField] `HeaderText` 設定為 [上次登入]，並將其 `DataField` 設為 "LastLoginDate"。 讓我們將此 BoundField 的輸出格式化，以便只顯示日期（而不是日期和時間）。 若要完成此動作，請將此 BoundField 的 `HtmlEncode` 屬性設為 False，並將其 `DataFormatString` 屬性設定為 "{0:d}"。 同時將 `ReadOnly` 屬性設定為 True。

將兩個 TemplateFields 的 [`HeaderText` 屬性] 設定為 [電子郵件] 和 [批註]。

[![GridView 的欄位可以透過 [欄位] 對話方塊來設定](role-based-authorization-cs/_static/image17.png)](role-based-authorization-cs/_static/image16.png)

**圖 6**： GridView 的欄位可以透過 [欄位] 對話方塊來設定（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image18.png)）

我們現在必須定義 [電子郵件] 和 [批註] TemplateFields 的 `ItemTemplate` 和 `EditItemTemplate`。 將標籤 Web 控制項新增至每個 `ItemTemplate`，並將其 `Text` 屬性分別系結至 [`Email`] 和 [`Comment`] 屬性。

針對 [電子郵件] TemplateField，將名為 `Email` 的 TextBox 加入其 `EditItemTemplate`，並使用雙向資料系結將其 `Text` 屬性系結至 `Email` 屬性。 將 RequiredFieldValidator 和 RegularExpressionValidator 新增至 `EditItemTemplate`，以確保編輯電子郵件屬性的訪客已輸入有效的電子郵件地址。 在 [批註] TemplateField 中，將名為 `Comment` 的多行文字方塊新增至其 `EditItemTemplate`。 將 TextBox 的 `Columns` 和 `Rows` 屬性分別設定為40和4，然後使用雙向資料系結將其 `Text` 屬性系結至 `Comment` 屬性。

設定這些 TemplateFields 之後，其宣告式標記看起來應該如下所示：

[!code-aspx[Main](role-based-authorization-cs/samples/sample4.aspx)]

編輯或刪除使用者帳戶時，我們必須知道使用者的 `UserName` 屬性值。 將 GridView 的 `DataKeyNames` 屬性設定為 "UserName"，以便透過 GridView 的 `DataKeys` 集合使用此資訊。

最後，將 ValidationSummary 控制項新增至頁面，並將其 `ShowMessageBox` 屬性設為 True，並將其 `ShowSummary` 屬性設定為 False。 使用這些設定時，如果使用者嘗試編輯的使用者帳戶遺失或不正確電子郵件地址，ValidationSummary 將會顯示用戶端警示。

[!code-aspx[Main](role-based-authorization-cs/samples/sample5.aspx)]

我們現在已完成此頁面的宣告式標記。 下一個工作是將一組使用者帳戶系結至 GridView。 將名為 `BindUserGrid` 的方法加入至 `RoleBasedAuthorization.aspx` 頁面的程式碼後置類別，將 `Membership.GetAllUsers` 傳回的 `MembershipUserCollection` 系結至 `UserGrid` GridView。 從第一頁上的 `Page_Load` 事件處理常式呼叫這個方法，造訪。

[!code-csharp[Main](role-based-authorization-cs/samples/sample6.cs)]

將此程式碼備妥之後，請透過瀏覽器造訪頁面。 如 [圖 7] 所示，您應該會看到 GridView 列出系統中每個使用者帳戶的相關資訊。

[![UserGrid GridView 列出系統中每個使用者的相關資訊](role-based-authorization-cs/_static/image20.png)](role-based-authorization-cs/_static/image19.png)

**圖 7**： `UserGrid` GridView 會列出系統中每個使用者的相關資訊（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image21.png)）

> [!NOTE]
> `UserGrid` GridView 會列出非分頁介面中的所有使用者。 這個簡單的方格介面不適合有多個使用者的案例。 其中一個選項是設定 GridView 以啟用分頁。 `Membership.GetAllUsers` 方法有兩個多載：一個不接受任何輸入參數，而會傳回所有使用者，另一個則會針對頁面索引和頁面大小使用整數值，並只傳回指定的使用者子集。 第二個多載可以用來更有效率地流覽使用者，因為它只會傳回使用者帳戶的精確子集，而不是*全部*。 如果您有數千個使用者帳戶，您可能會想要考慮以篩選器為基礎的介面，其中一個只會顯示使用者名稱以選取的字元開頭的使用者。 [`Membership.FindUsersByName method`](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)非常適合用來建立以篩選為基礎的使用者介面。 在未來的教學課程中，我們將探討如何建立這類介面。

當控制項系結至正確設定的資料來源控制項（例如 SqlDataSource 或 ObjectDataSource）時，GridView 控制項會提供內建的編輯和刪除支援。 不過，`UserGrid` GridView 會以程式設計方式系結其資料;因此，我們必須撰寫程式碼來執行這兩項工作。 特別的是，我們必須建立 GridView 的 `RowEditing`、`RowCancelingEdit`、`RowUpdating`和 `RowDeleting` 事件的事件處理常式，當訪客按一下 GridView 的 [編輯]、[取消]、[更新] 或 [刪除] 按鈕時，就會引發這些事件。

首先，建立 GridView 的 `RowEditing`、`RowCancelingEdit`和 `RowUpdating` 事件的事件處理常式，然後新增下列程式碼：

[!code-csharp[Main](role-based-authorization-cs/samples/sample7.cs)]

`RowEditing` 和 `RowCancelingEdit` 事件處理常式只會設定 GridView 的 `EditIndex` 屬性，然後將使用者帳戶清單重新系結至方格。 有趣的東西會發生在 `RowUpdating` 事件處理常式中。 這個事件處理常式一開始會先確保資料有效，然後從 `DataKeys` 集合中抓取已編輯使用者帳戶的 `UserName` 值。 然後以程式設計方式參考兩個 TemplateFields ' `EditItemTemplate` s 中的 [`Email`] 和 [`Comment`] 文字方塊。 其 `Text` 屬性包含已編輯的電子郵件地址和批註。

若要透過成員資格 API 來更新使用者帳戶，我們必須先取得使用者的資訊，我們透過呼叫 `Membership.GetUser(userName)`來完成此動作。 然後，傳回的 `MembershipUser` 物件的 `Email` 和 `Comment` 屬性會使用輸入至編輯介面的兩個文字方塊中的值進行更新。 最後，這些修改會與[`Membership.UpdateUser`](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)的呼叫一起儲存。 `RowUpdating` 事件處理常式會藉由將 GridView 還原至其預先編輯介面來完成。

接下來，建立 `RowDeleting` 事件處理常式，然後新增下列程式碼：

[!code-csharp[Main](role-based-authorization-cs/samples/sample8.cs)]

上述事件處理常式一開始會從 GridView 的 `DataKeys` 集合中抓取 `UserName` 值;這個 `UserName` 值接著會傳遞到成員資格類別的[`DeleteUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)中。 `DeleteUser` 方法會將使用者帳戶從系統中刪除，包括相關的成員資格資料（例如，此使用者所屬的角色）。 刪除使用者之後，方格的 `EditIndex` 會設定為-1 （如果使用者在另一個資料列處於編輯模式時按一下 [刪除]），就會呼叫 `BindUserGrid` 方法。

> [!NOTE]
> 在刪除使用者帳戶之前，[刪除] 按鈕不需要使用者進行任何確認。 我建議您新增某種形式的使用者確認，以減少意外刪除帳戶的機會。 確認動作最簡單的方法之一，是透過用戶端確認對話方塊。 如需這項技術的詳細資訊，請參閱[在刪除時新增用戶端確認](https://asp.net/learn/data-access/tutorial-42-cs.aspx)。

請確認此頁面是否如預期般運作。 您應該能夠編輯任何使用者的電子郵件地址和批註，以及刪除任何使用者帳戶。 由於 [`RoleBasedAuthorization.aspx`] 頁面可供所有使用者存取，因此任何使用者（甚至是匿名的訪客）都可以造訪此頁面，並編輯和刪除使用者帳戶！ 讓我們更新此頁面，讓監督員和系統管理員角色中的使用者只能編輯使用者的電子郵件地址和留言，而且只有系統管理員可以刪除使用者帳戶。

「使用 LoginView 控制項」一節會探討如何使用 LoginView 控制項來顯示使用者角色的特定指示。 如果系統管理員角色中的人員造訪此頁面，我們將會顯示如何編輯和刪除使用者的指示。 如果 [主管] 角色中的使用者到達此頁面，我們將會顯示有關編輯使用者的指示。 而且，如果訪客是匿名的，或不是在主管或 Administrators 角色中，我們會顯示一則訊息，說明他們無法編輯或刪除使用者帳戶資訊。 在「以程式設計方式限制功能」一節中，我們將撰寫程式碼，以程式設計方式顯示或隱藏根據使用者角色的 [編輯] 和 [刪除] 按鈕。

### <a name="using-the-loginview-control"></a>使用 LoginView 控制項

如我們在過去的教學課程中所見，LoginView 控制項適用于針對已驗證和匿名的使用者顯示不同的介面，但是 LoginView 控制項也可以用來根據使用者的角色來顯示不同的標記。 讓我們使用 LoginView 控制項，根據造訪的使用者角色來顯示不同的指示。

一開始請先在 `UserGrid` GridView 之上加入 LoginView。 如先前所討論，LoginView 控制項有兩個內建範本： `AnonymousTemplate` 和 `LoggedInTemplate`。 在這兩個範本中輸入簡短訊息，通知使用者他們無法編輯或刪除任何使用者資訊。

[!code-aspx[Main](role-based-authorization-cs/samples/sample9.aspx)]

除了 `AnonymousTemplate` 和 `LoggedInTemplate`之外，LoginView 控制項也可以包含*rolegroup*，這是角色特定的範本。 每個 RoleGroup 都包含一個 `Roles`的單一屬性，可指定 RoleGroup 適用的角色。 `Roles` 屬性可以設定為單一角色（例如 "Administrators"），或設為以逗號分隔的角色清單（例如「系統管理員」、「主管」）。

若要管理 Rolegroup，請按一下控制項智慧標籤中的 [編輯 Rolegroup] 連結，以顯示 RoleGroup 集合編輯器。 加入兩個新的 Rolegroup。 將第一個 RoleGroup 的 `Roles` 屬性設定為「系統管理員」，第二個設為「主管」。

[![透過 RoleGroup 集合編輯器來管理 LoginView 的角色特定範本](role-based-authorization-cs/_static/image23.png)](role-based-authorization-cs/_static/image22.png)

**圖 8**：透過 RoleGroup 集合編輯器（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image24.png)）來管理 LoginView 的角色特定範本

按一下 [確定] 以關閉 [RoleGroup 集合編輯器];這會更新 LoginView 的宣告式標記，以包含 `<RoleGroups>` 區段，其中含有 RoleGroup 集合編輯器中所定義之每個 RoleGroup 的 `<asp:RoleGroup>` 子項目。 此外，LoginView 的智慧標籤中的 [Views] 下拉式清單（一開始只會列出 `AnonymousTemplate` 和 `LoggedInTemplate`），現在也包含新增的 Rolegroup。

編輯 Rolegroup，讓 [主管] 角色中的使用者顯示如何編輯使用者帳戶的指示，而 [系統管理員] 角色中的使用者則會顯示編輯和刪除的指示。 進行這些變更之後，您 LoginView 的宣告式標記看起來應該如下所示。

[!code-aspx[Main](role-based-authorization-cs/samples/sample10.aspx)]

進行這些變更之後，請儲存頁面，然後透過瀏覽器造訪。 首先，以匿名使用者的身分造訪頁面。 您應該會看到訊息：「您未登入系統。 因此，您無法編輯或刪除任何使用者資訊。」 然後以已驗證的使用者身分登入，但不在 [監督員] 或 [系統管理員] 角色中。 此時您應該會看到訊息：「您不是主管或系統管理員角色的成員。 因此，您無法編輯或刪除任何使用者資訊。」

接下來，以「主管」角色成員的使用者身分登入。 此時您應該會看到監督員角色特定的訊息（請參閱 [圖 9]）。 而且，如果您以系統管理員角色的使用者身分登入，您應該會看到系統管理員角色特定的訊息（請參閱 [圖 10]）。

[![Bruce 會顯示在主管角色特定的訊息](role-based-authorization-cs/_static/image26.png)](role-based-authorization-cs/_static/image25.png)

**圖 9**： Bruce 會顯示在主管角色特定的訊息（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image27.png)）

[![Tito 會顯示系統管理員角色特定的訊息](role-based-authorization-cs/_static/image29.png)](role-based-authorization-cs/_static/image28.png)

**圖 10**： Tito 顯示為系統管理員角色特定的訊息（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image30.png)）

當螢幕擷取畫面顯示在 [圖 9] 和 [10] 中時，LoginView 只會呈現一個範本，即使有多個範本也適用。 Bruce 和 Tito 都是已登入的使用者，但 LoginView 只會轉譯相符的 RoleGroup，而不會呈現 `LoggedInTemplate`。 此外，Tito 同時屬於系統管理員和主管角色，而 LoginView 控制項會呈現系統管理員角色特定的範本，而不是主管。

[圖 11] 說明 LoginView 控制項用來判斷要轉譯哪些範本的工作流程。 請注意，如果指定了一個以上的 RoleGroup，LoginView 範本會呈現符合的*第一個*RoleGroup。 換句話說，如果我們將監督員 RoleGroup 做為第一個 RoleGroup，而將系統管理員設定為第二個，則當 Tito 造訪此頁面時，他會看到監督員訊息。

[![LoginView 控制項的工作流程，以決定要呈現的範本](role-based-authorization-cs/_static/image32.png)](role-based-authorization-cs/_static/image31.png)

**圖 11**：用來判斷要轉譯哪個範本的 LoginView 控制項工作流程（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image33.png)）

### <a name="programmatically-limiting-functionality"></a>以程式設計方式限制功能

雖然 LoginView 控制項會根據造訪頁面的使用者角色來顯示不同的指示，但 [編輯] 和 [取消] 按鈕會保持可見狀態。 我們需要以程式設計方式隱藏匿名訪客的 [編輯] 和 [刪除] 按鈕，以及同時不是主管或系統管理員角色的使用者。 我們必須針對不是系統管理員的每一位使用者隱藏 [刪除] 按鈕。 為了達成此目的，我們將撰寫一些程式碼，以程式設計方式參考 CommandField 的 [編輯] 和 [刪除] LinkButtons，並視需要將其 `Visible` 屬性設定為 [`false`]。

在 CommandField 中以程式設計方式參考控制項的最簡單方式，就是先將它轉換成範本。 若要完成這項操作，請按一下 GridView 智慧標籤中的 [編輯資料行] 連結，從目前欄位的清單中選取 CommandField，然後按一下 [將此欄位轉換成 TemplateField] 連結。 這會將 CommandField 變成具有 `ItemTemplate` 和 `EditItemTemplate`的 TemplateField。 `ItemTemplate` 包含 [編輯] 和 [刪除] LinkButtons，而 `EditItemTemplate` 裝載更新和取消 LinkButtons。

[![將 CommandField 轉換為 TemplateField](role-based-authorization-cs/_static/image35.png)](role-based-authorization-cs/_static/image34.png)

**圖 12**：將 CommandField 轉換成 TemplateField （[按一下以觀看完整大小的影像](role-based-authorization-cs/_static/image36.png)）

更新 `ItemTemplate`中的 [編輯] 和 [刪除] LinkButtons，分別將其 `ID` 屬性設定為 `EditButton` 和 `DeleteButton`的值。

[!code-aspx[Main](role-based-authorization-cs/samples/sample11.aspx)]

每當資料系結至 GridView 時，GridView 會列舉其 `DataSource` 屬性中的記錄，並產生對應的 `GridViewRow` 物件。 建立每個 `GridViewRow` 物件時，`RowCreated` 事件都會引發。 為了隱藏未授權使用者的 [編輯] 和 [刪除] 按鈕，我們必須建立此事件的事件處理常式，並以程式設計方式參考 [編輯] 和 [刪除] LinkButtons，並據以設定其 `Visible` 屬性。

建立 `RowCreated` 事件的事件處理常式，然後新增下列程式碼：

[!code-csharp[Main](role-based-authorization-cs/samples/sample12.cs)]

請記住，`RowCreated` 事件會針對*所有*GridView 資料列引發，包括標頭、頁尾、分頁程式介面等等。 我們只想要以程式設計方式參考 [編輯] 和 [刪除] LinkButtons （如果我們處理的資料列不是編輯模式）（因為編輯模式中的資料列具有 [更新] 和 [取消] 按鈕，而非 [編輯] 和 [刪除] 這項檢查是由 `if` 語句處理。

如果要處理的資料列不是編輯模式，則會參考 [編輯] 和 [刪除] LinkButtons，而且會根據 `User` 物件的 `IsInRole(roleName)` 方法所傳回的布林值來設定其 `Visible` 屬性。 User 物件會參考 `RoleManagerModule`所建立的主體;因此，`IsInRole(roleName)` 方法會使用「角色 API」來判斷目前的訪客是否*屬於「使用者」。*

> [!NOTE]
> 我們可以直接使用 Roles 類別，以呼叫[`Roles.IsUserInRole(roleName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)來取代 `User.IsInRole(roleName)` 的呼叫。 我決定使用主體物件在此範例中的 `IsInRole(roleName)` 方法，因為它比直接使用角色 API 更有效率。 稍早在本教學課程中，我們設定了角色管理員，以在 cookie 中快取使用者的角色。 只有在呼叫主體的 `IsInRole(roleName)` 方法時，才會使用這個快取的 cookie 資料。直接呼叫角色 API 一律牽涉到角色存放區的行程。 即使角色不會在 cookie 中快取，呼叫主體物件的 `IsInRole(roleName)` 方法通常會更有效率，因為在要求期間第一次呼叫它時，它會快取結果。 另一方面，角色 API 不會執行任何快取。 因為 `RowCreated` 事件會針對 GridView 中的每個資料列引發一次，所以使用 `User.IsInRole(roleName)` 只牽涉到角色存放區的一個行程，而 `Roles.IsUserInRole(roleName)` 則需要*n*次行程，其中*n*是格線中顯示的使用者帳戶數目。

如果流覽此頁面的使用者是在系統管理員或主管角色中，[編輯] 按鈕的 [`Visible`] 屬性會設定為 [`true`]。否則，它會設定為 `false`。 只有在使用者是系統管理員角色時，[刪除] 按鈕的 `Visible` 屬性才會設定為 [`true`]。

透過瀏覽器測試此頁面。 如果您以匿名訪客或不是監督員或系統管理員的使用者身分造訪網頁，則 CommandField 是空的;它仍然存在，但做為不含 [編輯] 或 [刪除] 按鈕的瘦薄片。

> [!NOTE]
> 當非監督員和非系統管理員造訪此頁面時，可以完全隱藏 CommandField。 我將此做為讀者的練習。

[針對非主管和非系統管理員的 [編輯] 和 [刪除] 按鈕 ![隱藏](role-based-authorization-cs/_static/image38.png)](role-based-authorization-cs/_static/image37.png)

**圖 13**：非主管和非系統管理員的 [編輯] 和 [刪除] 按鈕會隱藏（[按一下以觀看完整大小的影像](role-based-authorization-cs/_static/image39.png)）

如果屬於 [主管] 角色的使用者（而不是系統管理員角色）造訪，他只會看到 [編輯] 按鈕。

[![[編輯] 按鈕可供主管使用時，[刪除] 按鈕會隱藏起來](role-based-authorization-cs/_static/image41.png)](role-based-authorization-cs/_static/image40.png)

**圖 14**：雖然 [編輯] 按鈕適用于 [主管]，但 [刪除] 按鈕是隱藏的（[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image42.png)）

而且，如果系統管理員造訪，她就可以同時存取 [編輯] 和 [刪除] 按鈕。

[![[編輯] 和 [刪除] 按鈕僅供系統管理員使用](role-based-authorization-cs/_static/image44.png)](role-based-authorization-cs/_static/image43.png)

**圖 15**： [編輯] 和 [刪除] 按鈕僅適用于系統管理員（[按一下以觀看完整大小的影像](role-based-authorization-cs/_static/image45.png)）

## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>步驟3：將以角色為基礎的授權規則套用至類別和方法

在步驟2中，我們將編輯功能限制為僅限監督員和系統管理員角色中的使用者，並僅刪除系統管理員的功能。 這是藉由針對未經授權的使用者透過程式設計技術隱藏相關聯的使用者介面元素來完成。 這類量值不保證未經授權的使用者將無法執行特殊許可權動作。 可能是稍後新增的使用者介面元素，或我們忘記對未經授權的使用者隱藏。 或者，駭客可能會發現有其他方法可以讓 ASP.NET 網頁執行所需的方法。

有一個簡單的方法可確保未經授權的使用者無法存取特定功能，就是使用[`PrincipalPermission` 屬性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)來裝飾該類別或方法。 當 .NET 執行時間使用類別或執行它的其中一個方法時，它會檢查以確定目前的安全性內容具有許可權。 `PrincipalPermission` 屬性提供一種機制，可讓我們定義這些規則。

我們探討了<a id="_msoanchor_9"></a>如何使用以[*使用者為基礎的授權*](../membership/user-based-authorization-cs.md)教學課程中的 `PrincipalPermission` 屬性。 具體而言，我們已瞭解如何裝飾 GridView 的 `SelectedIndexChanged` 和 `RowDeleting` 事件處理常式，使其只能由已驗證的使用者和 Tito 來執行。 `PrincipalPermission` 屬性也適用于角色。

讓我們來示範如何在 GridView 的 `RowUpdating` 上使用 `PrincipalPermission` 屬性，並 `RowDeleting` 事件處理常式來禁止未獲授權的使用者執行。 我們只需要在每個函式定義的上方新增適當的屬性即可：

[!code-csharp[Main](role-based-authorization-cs/samples/sample13.cs)]

`RowUpdating` 事件處理常式的屬性（attribute）表示只有系統管理員或主管角色中的使用者可以執行事件處理常式，而 `RowDeleting` 事件處理常式上的屬性（attribute）會將執行限制為系統管理員角色中的使用者。

> [!NOTE]
> `PrincipalPermission` 屬性會表示為 `System.Security.Permissions` 命名空間中的類別。 請務必在程式碼後置類別檔案的頂端加入 `using System.Security.Permissions` 語句，以匯入此命名空間。

如果是，非系統管理員會嘗試執行 `RowDeleting` 事件處理常式，或如果非監督員或非系統管理員嘗試執行 `RowUpdating` 事件處理常式，則 .NET 執行時間會引發 `SecurityException`。

[![如果未授權安全性內容執行方法，則會擲回 SecurityException](role-based-authorization-cs/_static/image47.png)](role-based-authorization-cs/_static/image46.png)

**圖 16**：如果安全性內容沒有執行方法的授權，則會擲回 `SecurityException` （[按一下以查看完整大小的影像](role-based-authorization-cs/_static/image48.png)）

除了 ASP.NET 網頁之外，許多應用程式也具有包含各種層級的架構，例如商務邏輯和資料存取層。 這些層通常會實作為類別庫，並提供類別和方法來執行商務邏輯和資料相關的功能。 `PrincipalPermission` 屬性也適用于將授權規則套用至這些層級。

如需使用 `PrincipalPermission` 屬性來定義類別和方法授權規則的詳細資訊，請參閱[Scott Guthrie](https://weblogs.asp.net/scottgu/)的 Blog 專案[使用 `PrincipalPermissionAttributes`將授權規則新增至商務和資料層](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)。

## <a name="summary"></a>總結

在本教學課程中，我們探討了如何根據使用者的角色指定粗略和精細的授權規則。 ASP.NET 的 URL 授權功能可讓網頁開發人員指定允許或拒絕哪些身分識別存取哪些頁面。 如同我們在以使用者為<a id="_msoanchor_10"> </a>[*基礎的授權*](../membership/user-based-authorization-cs.md)教學課程中所看到的，URL 授權規則可以依使用者逐一套用。 如本教學課程的步驟1所示，您也可以依角色逐一套用這些應用程式。

精細的授權規則可能會以宣告方式或以程式設計方式套用。 在步驟2中，我們探討了如何使用 LoginView 控制項的 Rolegroup 功能，根據造訪的使用者角色來呈現不同的輸出。 我們也探討了如何以程式設計方式判斷使用者是否屬於特定的角色，以及如何據以調整頁面的功能。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [使用 `PrincipalPermissionAttributes` 將授權規則新增至商務和資料層](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [檢查 ASP.NET 2.0 的成員資格、角色和設定檔：使用角色](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [ASP.NET 2.0 的安全性問題清單](https://msdn.microsoft.com/library/ms998375.aspx)
- [`<roleManager>` 元素的技術檔](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者包括 Suchi Banerjee 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](assigning-roles-to-users-cs.md)
> [下一頁](creating-and-managing-roles-vb.md)
