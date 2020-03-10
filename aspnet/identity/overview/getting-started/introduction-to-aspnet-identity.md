---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: ASP.NET Identity 的簡介-ASP.NET 4。x
author: jongalloway
description: ASP.NET 成員資格系統是以2005中的 ASP.NET 2.0 引進，因為 web 應用程式通常的方式已有許多變更 。
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0268dfc16cd2cfb1e79ee14997a4c5eb247af950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583843"
---
# <a name="introduction-to-aspnet-identity"></a>ASP.NET Identity 簡介

> ASP.NET 成員資格系統是以2005中的 ASP.NET 2.0 引進，既然 web 應用程式通常處理驗證和授權的方式有許多變更。 ASP.NET Identity 是建立 web、手機或平板電腦的現代化應用程式時，成員資格系統的新外觀。

## <a name="background-membership-in-aspnet"></a>背景： ASP.NET 中的成員資格

### <a name="aspnet-membership"></a>ASP.NET 成員資格

[ASP.NET 成員資格](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx)的設計目的是要解決2005中常見的網站成員資格需求，包括表單驗證，以及使用者名稱、密碼和設定檔資料的 SQL Server 資料庫。 現今 web 應用程式有更廣泛的資料儲存選項，而且大部分的開發人員都想要讓其網站使用社交識別提供者來進行驗證和授權功能。 ASP.NET 成員資格設計的限制使得這項轉換變得很棘手：

- 資料庫架構是針對 SQL Server 所設計，而且您無法變更它。 您可以新增設定檔資訊，但額外的資料會封裝到不同的資料表中，讓您難以透過設定檔提供者 API 以外的任何方式存取。
- 提供者系統可讓您變更支援資料存放區，但系統是設計成適用于關係資料庫的假設。 您可以撰寫提供者以在非關聯式儲存機制（例如 Azure 儲存體資料表）中儲存成員資格資訊，但是您必須針對不適用於 NoSQL 資料庫的方法撰寫大量程式碼和許多 `System.NotImplementedException` 例外狀況，以解決關聯式設計。
- 由於登入/登出功能是以表單驗證為基礎，因此成員資格系統無法使用[OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)。 OWIN 包含用於驗證的中介軟體元件，包括使用外部身分識別提供者（例如 Microsoft 帳戶、Facebook、Google、Twitter）的登入支援，以及使用內部部署 Active Directory 或的組織帳戶登入。Azure Active Directory。 OWIN 也包含 OAuth 2.0、JWT 和 CORS 的支援。

### <a name="aspnet-simple-membership"></a>ASP.NET 簡單成員資格

[ASP.NET 簡單成員資格](../../../web-pages/overview/security/16-adding-security-and-membership.md)的開發是做為 ASP.NET Web Pages 的成員資格系統。 其發行于 WebMatrix 和 Visual Studio 2010 SP1。 簡單成員資格的目標是要讓您輕鬆地將成員資格功能加入網頁應用程式中。

簡單成員資格可讓您更輕鬆地自訂使用者設定檔資訊，但它仍會與 ASP.NET 成員資格分享其他問題，而且有一些限制：

- 很難將成員資格系統資料保存在非關聯式存放區中。
- 您無法搭配 OWIN 使用它。
- 它無法與現有的 ASP.NET 成員資格提供者搭配運作，而且無法擴充。

### <a name="aspnet-universal-providers"></a>ASP.NET Universal Providers

[ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)的開發目的是要讓您能夠在 Microsoft Azure SQL Database 中保存成員資格資訊，而且也可以與 SQL Server Compact 搭配使用。 Universal Providers 是以 Entity Framework Code First 為基礎，這表示 Universal Providers 可用來保存 EF 支援的任何存放區中的資料。 在 Universal Providers 中，資料庫架構也會一併清除。

Universal Providers 是建置於 ASP.NET 成員資格基礎結構上，因此它們仍然具有與 SqlMembership 提供者相同的限制。 也就是說，它們是針對關係資料庫所設計，而且很難自訂設定檔和使用者資訊。 這些提供者也仍然會使用表單驗證來登入和登出功能。

## <a name="aspnet-identity"></a>ASP.NET Identity

隨著 ASP.NET 的成員故事演變多年，ASP.NET 團隊也從客戶的意見反應中學到了許多。

假設使用者會藉由輸入使用者名稱和密碼來登入，其已在您自己的應用程式中註冊，將不再有效。 Web 已經變得越來越社交。 使用者透過社交管道（例如 Facebook、Twitter 和其他社交網站）即時與他人互動。 開發人員想要讓使用者能夠使用他們的社交身分識別登入，讓他們能夠在他們的網站上擁有豐富的體驗。 現代化的成員資格系統必須啟用以重新導向為基礎的登入，以驗證提供者（例如 Facebook、Twitter 等等）。

隨著 網頁程式開發的發展，網頁程式開發的模式也是如此。 應用程式程式碼的單元測試已成為應用程式開發人員的核心考慮。 在2008中，ASP.NET 新增了以模型視圖控制器（MVC）模式為基礎的新架構，部分是為了協助開發人員建立可測試單元的 ASP.NET 應用程式。 想要對其應用程式邏輯進行單元測試的開發人員，也想要能夠使用成員資格系統來執行此動作。

在 web 應用程式開發中考慮這些變更，ASP.NET Identity 是以下列目標進行開發：

- **一個 ASP.NET Identity 系統**

    - ASP.NET Identity 可以與所有 ASP.NET 架構搭配使用，例如 ASP.NET MVC、Web Forms、Web Pages、Web API 和 SignalR。
    - 當您建立 web、手機、商店或混合式應用程式時，可以使用 ASP.NET Identity。
- **輕鬆插入使用者的設定檔資料**

    - 您可以控制使用者和設定檔資訊的架構。 例如，您可以輕鬆地讓系統儲存使用者在您的應用程式中註冊帳戶時所輸入的出生日期。

- **持續性控制**

    - 根據預設，ASP.NET Identity 系統會將所有使用者資訊儲存在資料庫中。 ASP.NET Identity 使用 Entity Framework Code First 來執行其所有持續性機制。
    - 由於您控制了資料庫架構，因此變更資料表名稱或變更主鍵資料類型的一般工作很簡單。
    - 您可以輕鬆地插入不同的儲存機制，例如 SharePoint、Azure 儲存體資料表服務、NoSQL 資料庫等，而不需要擲回 `System.NotImplementedExceptions` 例外狀況。
- **單元可測試性**

    - ASP.NET Identity 讓 web 應用程式更能進行單元測試。 您可以為使用 ASP.NET Identity 之應用程式的元件撰寫單元測試。
- **角色提供者**

    - 有一個角色提供者，可讓您依角色限制存取應用程式的某些部分。 您可以輕鬆地建立角色，例如 "Admin"，並將使用者新增至角色。
- **以宣告為基礎**

    - ASP.NET Identity 支援以宣告為基礎的驗證，其中使用者的身分識別會表示為一組宣告。 宣告可讓開發人員在描述使用者的身分識別時，比角色允許的更具表達性。 角色成員資格只是布林值（成員或非成員），而宣告可以包含有關使用者身分識別和成員資格的豐富資訊。
- **社交登入提供者**

    - 您可以輕鬆地將社交記錄檔（例如 Microsoft 帳戶、Facebook、Twitter、Google 和其他人）新增至您的應用程式，並將使用者專屬的資料儲存在您的應用程式中。

- **OWIN 整合**

    - ASP.NET authentication 現在是以 OWIN 中介軟體為基礎，可用於任何以 OWIN 為基礎的主機。 ASP.NET Identity 在 System.web 上沒有任何相依性。 它是完全相容的 OWIN 架構，可以在任何 OWIN 裝載的應用程式中使用。
    - ASP.NET Identity 會針對網站中的使用者登入/登出，使用 OWIN Authentication。 這表示，應用程式會使用 OWIN CookieAuthentication 來執行此動作，而不是使用 FormsAuthentication 來產生 cookie。
- **NuGet 套件**

    - ASP.NET Identity 會轉散發為 NuGet 套件，並安裝在隨附于 Visual Studio 2017 的 ASP.NET MVC、Web Forms 和 Web API 範本中。 您可以從 NuGet 資源庫下載此 NuGet 套件。
    - 將 ASP.NET Identity 發行為 NuGet 套件，可讓 ASP.NET 小組更輕鬆地反復執行新功能和 bug 修正，並以敏捷的方式將這些專案提供給開發人員。

## <a name="get-started-with-aspnet-identity"></a>開始使用 ASP.NET Identity

ASP.NET Identity 適用于 Visual Studio 2017 專案範本，用於 ASP.NET MVC、Web Forms、Web API 和 SPA。 在本逐步解說中，我們將說明專案範本如何使用 ASP.NET Identity 新增功能來註冊、登入和登出使用者。

使用下列程式來執行 ASP.NET Identity。 本文的目的是要提供您 ASP.NET Identity 的高階總覽;您可以逐步執行，或直接閱讀詳細資料。 如需使用 ASP.NET Identity 建立應用程式的詳細指示，包括使用新的 API 來新增使用者、角色和設定檔資訊，請參閱本文結尾處的後續步驟一節。

1. 建立具有個別帳戶的 ASP.NET MVC 應用程式。 您可以使用 ASP.NET MVC、Web Forms、Web API、SignalR 等中的 ASP.NET Identity。在本文中，我們將從 ASP.NET MVC 應用程式開始。  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. 建立的專案包含下列三個用於 ASP.NET Identity 的封裝。

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   此封裝具有 ASP.NET Identity 的 Entity Framework 執行，將 ASP.NET Identity 資料和架構保存到 SQL Server。
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   此套件具有 ASP.NET Identity 的核心介面。 此套件可用於針對以不同持續性存放區（例如 Azure 表格儲存體、NoSQL 資料庫等）為目標的 ASP.NET Identity 撰寫執行。
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   此套件包含的功能，可用來在 ASP.NET 應用程式中使用 ASP.NET Identity 插入 OWIN authentication。 這是在您將登入功能新增至應用程式並呼叫 OWIN Cookie 驗證中介軟體來產生 Cookie 時使用。
3. 建立使用者。  
   啟動應用程式，然後按一下 [**註冊**] 連結來建立使用者。 下圖顯示收集使用者名稱和密碼的 [註冊] 頁面。  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   當使用者選取 [**註冊**] 按鈕時，帳戶控制器的 [`Register`] 動作會藉由呼叫 ASP.NET Identity API 來建立使用者，如下所示：

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. 登入。  
   如果成功建立使用者，她就會使用 `SignInAsync` 方法來登入。  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]

   `SignInManager.SignInAsync` 方法會產生[ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)。 由於 ASP.NET Identity 和 OWIN Cookie 驗證是以宣告為基礎的系統，因此架構會要求應用程式為使用者產生 ClaimsIdentity。 ClaimsIdentity 包含使用者所有宣告的相關資訊，例如使用者所屬的角色。   
 
5. 登出。  
   選取 [**登出**] 連結以呼叫帳戶控制器中的 [登出] 動作。 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   上述反白顯示的程式碼顯示 OWIN `AuthenticationManager.SignOut` 方法。 這類似于 Web Forms 中[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模組所使用的[FormsAuthentication. SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)方法。

## <a name="components-of-aspnet-identity"></a>ASP.NET Identity 的元件

下圖顯示 ASP.NET Identity 系統的元件（請在[此](introduction-to-aspnet-identity/_static/image3.png)或圖表上選取以放大）。 綠色的套件組成 ASP.NET Identity 系統。 所有其他的封裝都是在 ASP.NET 應用程式中使用 ASP.NET Identity 系統所需的相依性。

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

以下是先前未提及之 NuGet 套件的簡短說明：

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 可讓應用程式使用 cookie 型驗證的中介軟體，類似于 ASP。NET 的表單驗證。
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Entity Framework 是 Microsoft 建議的關係資料庫資料存取技術。

## <a name="migrating-from-membership-to-aspnet-identity"></a>從成員資格遷移至 ASP.NET Identity

我們希望很快就能提供有關將使用 ASP.NET 成員資格或簡單成員資格的現有應用程式遷移至新 ASP.NET Identity 系統的指引。

## <a name="next-steps"></a>後續步驟

- [使用 Facebook 和 Google OAuth2 和 OpenID 登入建立 ASP.NET MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 本教學課程使用 ASP.NET Identity API 將設定檔資訊新增至使用者資料庫，以及如何使用 Google 和 Facebook 進行驗證。
- [使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 本教學課程說明如何使用身分識別 API 來新增使用者和角色。
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 範例應用程式，說明如何新增基本角色和使用者支援，以及如何執行角色和使用者管理。
