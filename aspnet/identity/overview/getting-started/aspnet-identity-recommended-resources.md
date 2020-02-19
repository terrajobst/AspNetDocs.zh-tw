---
uid: identity/overview/getting-started/aspnet-identity-recommended-resources
title: ASP.NET Identity 建議的資源-ASP.NET 4。x
author: Rick-Anderson
description: 本主題提供有關如何使用 ASP.NET Identity 的檔資源連結。 如果您知道絕佳的 blog 文章、stackoverflow 往來文章或任何其他 lin 。
ms.author: riande
ms.date: 04/09/2015
ms.assetid: 0f78aec2-f509-46fa-b20f-d5208425d8ec
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-recommended-resources
msc.type: authoredcontent
ms.openlocfilehash: 4b2a6689839f66121f4a32ee5934f6cda50ae812
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456566"
---
# <a name="aspnet-identity-recommended-resources"></a>ASP.NET Identity 建議資源

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本主題提供有關如何使用 ASP.NET Identity 的檔資源連結。
>
> 如果您知道絕佳的 blog 文章、 [stackoverflow](http://stackoverflow.com)執行緒或任何其他有用的連結，請傳送含有連結的[電子郵件給我們](mailto:aspnetue@microsoft.com?subject=Identity recommended resources)，或只在此頁面底部留下一則訊息。

- [開始使用 ASP.NET Identity](#gettingstarted)
- [新功能必須閱讀文章](#feat)
- [中繼 ASP.NET Identity](#adv)
- [影片](#video)
- [在何處提出問題、要求功能、報告錯誤和夜間組建](#samp)
- [關於身分識別的 Blog 文章](#blog)
- [ASP.NET Identity 的自訂儲存體提供者](#cust)
- [其他身分識別資源](#additional)
- [Q &amp; A （問與答）](#qand)

<a id="gettingstarted"></a>

## <a name="getting-started-with-aspnet-identity"></a>開始使用 ASP.NET Identity

- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教學課程說明如何使用 Facebook 和 Google OAuth 2 授權撰寫 ASP.NET MVC 5 應用程式。 它也會示範如何將其他資料新增至身分識別資料庫。
- 將[具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署至 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教學課程會新增 Azure 部署、如何以角色保護您的應用程式、如何使用成員資格 API 來新增使用者和角色，以及其他安全性功能。
- [ASP.NET Identity 簡介](introduction-to-aspnet-identity.md)
- [建立安全的 ASP.NET MVC 5 Web 應用程式，並重設登入、電子郵件確認與密碼](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)
- [使用 SMS 和電子郵件雙因素驗證的 ASP.NET MVC 5 應用程式](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)

<a id="feat"></a>

## <a name="new-featured-must-read-articles"></a>新功能必須閱讀文章

- 逐步解說：透過[Benjamin 日](http://www.benday.com/about/)[以 Microsoft 帳戶驗證 ASP.NET MVC 身分識別](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [ASP.NET Identity 2.0 擴充身分識別模型並使用整數索引鍵，而不是字串](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
- [使用 ASP.NET Web API 2、Owin 和身分識別來 AngularJS 權杖驗證](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [Thinktecture. IdentityManager 作為 WSAT 的取代](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [ASP.NET Identity 2.0：自訂使用者和角色](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)

<a id="adv"></a>

## <a name="intermediate-aspnet-identity"></a>中繼 ASP.NET Identity

- [使用 ASP.NET Identity 進行帳戶確認和密碼復原](../features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [使用 SMS 的雙因素驗證和使用 ASP.NET Identity 的電子郵件](../features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [將現有的網站從 SQL 成員資格移轉至 ASP.NET Identity](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [將 ASP.NET Identity 新增至空的或現有的 Web Form 專案](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)
- MSDN 雜誌[使用 ASP.NET Identity](https://msdn.microsoft.com/magazine/dn745860.aspx) Dino Esposito 進行外部驗證
- MSDN 雜誌[第一次探討](https://msdn.microsoft.com/magazine/dn605872.aspx)Dino Esposito 的 ASP.NET Identity
- [ASP.NET Identity –使用者鎖定](http://tech.trailmax.info/2014/06/asp-net-identity-user-lockout/)

<a id="samp"></a>

## <a name="where-to-ask-questions-request-features-report-a-bug-and-nightly-builds"></a>在何處提出問題、要求功能、報告錯誤和夜間組建

- 針對 StackOverflow，請使用標記[aspnet-identity](http://stackoverflow.com/questions/tagged/asp.net-identity)
- 針對 ASP.NET 論壇，張貼至[安全性論壇](https://forums.asp.net/25.aspx)，並將**ASP.NET Identity**新增至標題。
- [GitHub 上的 ASP.NET Identity](https://github.com/aspnet/AspNetIdentity)取得夜間組建、要求功能、開啟 bug。

<a id="blog"></a>

## <a name="blog-posts-on-identity"></a>關於身分識別的 Blog 文章

- [ASP.NET Identity 中的 SecurityStamp 為何？](http://stackoverflow.com/questions/19487322/what-is-asp-net-identitys-iusersecuritystampstoretuser-interface/19505060#19505060)
- 依[John Atten](https://twitter.com/xivSolutions)

    - [ASP.NET Identity 2.0 擴充身分識別模型並使用整數索引鍵，而不是字串](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
    - [ASP.NET Identity 2.0：自訂使用者和角色](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)
    - [ASP.NET MVC 和身分識別2.0：瞭解基本概念](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)
    - [設定帳戶驗證和雙因素授權](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)
    - [針對 ASP.NET MVC 5 和 Visual Studio 2013 中的身分識別帳戶設定 Db 連接和程式碼優先遷移](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)
- 依[Taiseer Joudeh](http://bitoftech.net/taiseer-joudeh-blog/)

    - [使用 ASP.NET Web API 2、Owin 中介軟體和 ASP.NET Identity 以權杖為基礎的驗證](http://bitoftech.net/2014/06/01/token-based-authentication-asp-net-web-api-2-owin-asp-net-identity/)
    - [使用 ASP.NET Web API 2、Owin 和身分識別來 AngularJS 權杖驗證](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
    - [使用 ASP .NET Web API 2 和 Owin （第3部分），在 AngularJS 應用程式中啟用 OAuth 重新整理權杖。](http://bitoftech.net/2014/07/16/enable-oauth-refresh-tokens-angularjs-app-using-asp-net-web-api-2-owin/)
- 依[Anders Abel](https://twitter.com/anders_abel)

    - [瞭解 Owin 外部驗證管線](http://coding.abel.nu/2014/06/understanding-the-owin-external-authentication-pipeline/)
    - [ASP.NET Identity 和 Owin 總覽](http://coding.abel.nu/2014/06/asp-net-identity-and-owin-overview/)

  依據程式碼至程式碼的[Scott Allen](https://twitter.com/OdeToCode)

    - [ASP.NET Core 身分識別](http://odetocode.com/blogs/scott/archive/2013/11/25/asp-net-core-identity.aspx)此 blog 探討核心抽象概念，包括 IUser、IUserStore 和 I\*Store 介面。
    - [Entity Framework 的 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/03/asp-net-identity-with-the-entity-framework.aspx)MVC 5、Web API 和 SPA 應用程式中的個別使用者帳戶、連接字串和管理內容
    - [ASP.NET Identity 的自訂選項](http://odetocode.com/blogs/scott/archive/2014/01/09/customization-options-with-asp-net-identity.aspx)
    - [執行 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- [Benjamin Day](http://www.benday.com/about/)[逐步解說：使用 Microsoft 帳戶驗證 ASP.NET MVC 身分識別](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [Brock Allen](https://twitter.com/BrockLAllen)

    - [使用 OWIN/Katana authentication 中介軟體的外部登入提供者（社交登錄）入門](http://brockallen.com/2014/01/09/a-primer-on-external-login-providers-social-logins-with-owinkatana-authentication-middleware/)
    - [IdentityReboot 簡介](http://brockallen.com/2014/02/11/introducing-identityreboot/)：一組 ASP.NET Identity 的延伸模組，可執行我所抱怨的主要遺失功能。
- [Pranav 請參閱 rastogi](https://twitter.com/rustd)

    - [取得社交提供者的詳細資訊](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [@beabigrockstar](https://twitter.com/beabigrockstar) （Jerrie Pelser）

    - [2要素驗證](http://www.beabigrockstar.com/blog/2-factor-authentication-with-asp-net-identity-2-0-beta-1/)
    - [搭配 ASP.NET Identity 使用 Google 驗證器](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/)
    - [ASP.NET MVC 5 驗證指南](http://www.beabigrockstar.com/)
- [從 VS 2013 專案範本中使用的社交提供者取得更多資訊](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [使用 ASP.NET Identity 建立簡單的待辦事項應用程式，並將使用者與 ToDoes 產生關聯](https://blogs.msdn.com/b/webdev/archive/2013/10/20/building-a-simple-todo-application-with-asp-net-identity-and-associating-users-with-todoes.aspx)
- [ASP.NET Identity 的 Google OpenId 整合問題](http://blog.technovert.com/2014/01/google-openid-integration-issues-asp-net-identity/)如果您收到錯誤： HTTP 錯誤404.15 –找不到要求篩選模組已設定為拒絕查詢字串太長的要求
- [Thinktecture. IdentityManager 作為 WSAT 的取代](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [使用 ASP.NET Web API 2、Owin 和身分識別來 AngularJS 權杖驗證](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [不 Entity Framework 的簡單 Asp.net 身分識別核心](https://code.msdn.microsoft.com/Simple-Aspnet-Identiy-Core-7475a961)
- 使用[ASP.NET Identity FOR MVC](http://www.dotnetfunda.com/articles/show/2898/working-with-roles-in-aspnet-identity-for-mvc) By [Sheo Narayan](http://www.dotnetfunda.com/profile/sheonarayan.aspx)中的角色
- [移至 ASP.NET 成員資格](http://webdojo.sharepoint.com/ajmatthews/_layouts/15/start.aspx#/Lists/Posts/Post.aspx?ID=2)By Alistair Matthews 的 ASP.NET Identity

<a id="video"></a>

## <a name="videos"></a>影片

- Channel 9[保護 ASP.NET 應用程式和服務： Ido Flatow 的現代化應用程式安全性 Facelift](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B421#fbid=PhVT9E1WRtr?hashlink=fbid)
- Channel 9 [ASP.NET Identity](https://channel9.msdn.com/Events/dotnetConf/2014/ASP-NET-Identity-Security) Pranav 請參閱 rastogi 的簡介
- Channel 9[使用 ASP.NET Identity](https://channel9.msdn.com/Shows/Web+Camps+TV/Special-Movember-Episode-ASPNET-Authentication-Provider) By Cory Fowler 的 ASP.NET Authentication
- Channel 9[建立現代化的 Web Apps：](https://channel9.msdn.com/Series/Building-Modern-Web-Apps/03) Jeff Koch ASP.NET Identity
- Channel 9[使用 ASP.NET Identity Alex Thissen 保護您的網站](https://channel9.msdn.com/Events/TechDays/Techdays-2014-the-Netherlands/Securing-your-website-with-ASP-NET-Identity)
- 透過 Alexander Schmidt[在現有 DB 模型上使用 ASP.NET Identity](https://www.youtube.com/watch?v=elfqejow5hM)
- 透過 Ivaylo Kenov of Telerik [ASP.NET 一個身分識別](https://www.youtube.com/watch?v=w8GD-QIusKk)
- [捷克文 ASP.NET Identity](https://www.youtube.com/watch?v=tVbZp5brcpY)在此課程中，我們將示範如何部署基本驗證、如何新增對外部身分識別提供者（例如 Twitter 或 Facebook）的支援，以及如何使用單次密碼（OTP）。 [ASP.NET Identity je nástupce 成員資格提供者&#367; v ASP.NET，tedy c pro zajišt&#283;ní autentizace uživatel&#367;。 V 多 p&#345;ednášce si ukážeme，如何 nasad]

<a id="cust"></a>

## <a name="custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity 的自訂儲存體提供者

如果您想要撰寫自己的提供者，請閱讀[ASP.NET Identity 的自訂儲存體提供](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)者和[執行 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)的總覽，然後檢查下列其中一個 OSS 專案的來源。

- 教學課程： FitzMacken 的[自訂儲存體提供者（](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)由 Tom 的 ASP.NET Identity）
- Blog：[執行 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 教學課程：[設定基本身分識別帳戶，並將它們指向外部 DB](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)。 依[@xivSolutions](https://twitter.com/xivSolutions)。
- 教學課程[：執行自訂 MySQL ASP.NET Identity 存放裝置提供者](../extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [Azure 表格儲存體](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/)的 James Randall。
- Azure 表格儲存體： [@stuartleeks](https://twitter.com/stuartleeks)的[TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) 。
- [CouchDB/Cloudant by Daniel Wertheim。](https://github.com/danielwertheim/mycouch.aspnet.identity)
- [彈性搜尋：](https://github.com/bmbsqd/elastic-identity)依 Bombsquad AB 的彈性身分識別。
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) By Jonathan Sheely Jonathan Sheely。
- [NHibernate](https://github.com/milesibastos/NHibernate.AspNet.Identity) By Antônio Milesi Bastos。
- [@tourismgeek](https://twitter.com/tourismgeek) [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) 。
- 依[ILMServices](http://www.ilmservice.com/)的[RavenDB 身分識別](https://github.com/ILMServices/RavenDB.AspNet.Identity)。
- Redis： [Redis。身分識別](https://github.com/aminjam/Redis.AspNet.Identity)
- T4 範本，用來產生「資料庫第一個」使用者存放區的 EF 程式碼： [AspNet. Identity. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)

<a id="additional"></a>

## <a name="additional-aspnet-identity-resources"></a>其他 ASP.NET Identity 資源

- 針對 Yahoo 和 LinkedIn 指示，[介紹 yahoo 和 Linkedin OAuth security provider FOR OWIN](http://blog.beabigrockstar.com/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) By Jerrie Pelser。

<a id="qand"></a>

## <a name="qampa-questionanswer"></a>Q&amp;A （問與答）

- 問：鎖定已啟用「記住我」的使用者（因此他們不需要在該電腦/瀏覽器上進行2FA），也不會遭到鎖定。為何和如何避免這種情況？ 請[在此](http://stackoverflow.com/questions/24312247/locked-out-users-can-login-if-they-have-auth-cookie)回答。
- **問**：如何在 ASP.NET Identity cookie 中儲存自訂宣告（例如使用者的實際名稱），以避免每個要求都有不必要的資料庫查詢。 請[在此](http://stackoverflow.com/questions/23622047/identity-cookie-loses-custom-claim-information-after-a-period-of-time)回答。
- **問：更新 AspNetUser 密碼雜湊**：我有2個專案。 其中一個使用 ASP.NET authentication，另一個使用 Windows 驗證，也就是管理端。 我想要讓管理專案能夠管理其他使用者。 我可以修改密碼以外的所有專案。 請[在此回答](http://stackoverflow.com/questions/23880666/updating-aspnetuser-password-hash)。
- **問**：如何以系統管理員的身分為其他使用者重設密碼？ 請[在此](http://stackoverflow.com/questions/23783249/identity-2-0-reset-password-by-admin/24211766#24211766)回答。
- **問**：我可以在 ASP.NET MVC IdentityUser 中變更 [UserName] 欄位的顯示名稱嗎？ 請[在此](http://stackoverflow.com/questions/23256650/can-i-change-the-displayed-name-of-the-username-field-in-asp-net-mvc-identityuse)回答。
- **問**：如何 gran 使用者將其他使用者新增至特定角色的許可權？ 請[在此](http://stackoverflow.com/questions/23695373/allow-users-to-grant-permissions-to-other-users-for-their-account-in-asp-net-ide)回答。
- **問**：將設定檔資訊儲存在 AspNetUsers 資料表和 AspNetUserClaims 資料表中。 請[在此](http://stackoverflow.com/questions/23215727/is-there-any-benefit-to-storing-user-information-in-aspnetuserclaims-with-asp-ne)回答。
- **問**：在使用外部驗證提供者時，請記住我。 請[在此](http://stackoverflow.com/questions/23180896/how-to-remember-the-login-in-mvc5-when-an-external-provider-is-used)回答。
- **問**：為什麼每個要求都需要 [applicationdbcoNtext]，而不是太多額外負荷？ 答：否，額外負荷很低。
- 問：如何? 取得已登入使用者的清單？ 請[在此](http://stackoverflow.com/questions/22995653/getting-a-list-of-logged-in-users-in-asp-net-identity/)回答。
- 問：如何偵測使用者何時以 Microsoft AspNet 身分登入？ 請[在此](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)回答。
- 問：如何? 取得身分識別的當地語系化錯誤訊息嗎？ 請[在此](http://stackoverflow.com/questions/22835981/asp-net-identity-localization-publickeytoken/22845864#22845864)回答。
- 問：如何? 將 CookieMiddleware 設定為每隔30分鐘取得新的宣告？ 請[在此](http://stackoverflow.com/questions/22682663/how-to-hold-the-cookies-claims-updated-with-mcv5-owin/22796932#22796932)回答。
- 問：如何在使用者登入之後修改其宣告？ 請[在此](http://stackoverflow.com/questions/22768836/can-i-modify-claims-in-asp-net-identity-with-owin-after-calling-signin/22769963#22769963)回答。
- 問：如何? 使安全性權杖失效？ 請[在此](http://stackoverflow.com/questions/22755700/revoke-token-generated-by-usertokenprovider-in-asp-net-identity-2-0/22767286#22767286)回答。
- 問：如何將宣告儲存在 cookie 中介軟體？ 請[在此](http://stackoverflow.com/questions/22320632/storing-retrieving-user-data-without-database-when-using-owin-cookie-authenticat/22541856#22541856)回答。
- 問：我想要對我的 MVC 應用程式中的每個動作方法進行 PIN 或安全性檢查，但我想要儲存使用者成功，讓他們不需要在該動作方法的每個要求上輸入 PIN。 請[在此](http://stackoverflow.com/questions/22479958/security-check-an-user-to-a-access-controller-action/22486075#22486075)回答。
- 問：我想要將從社交提供者傳回的電子郵件地址儲存到資料庫，該怎麼做？ 答案[如下](http://stackoverflow.com/questions/22888397/save-claims-to-db-on-login/22970969#22970969)：
- 問：如何偵測使用者何時以「記住我」 cookie 來登入？ 請[在此](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)回答。
- 問：在呼叫登入之後，我可以使用 OWIN 修改 ASP.NET Identity 中的宣告嗎？ 答：呼叫登入是您想要為使用者修改宣告時所應執行的動作。 基本上，它會將 ClaimsIdentity 序列化為 cookie，這就是您看到新宣告顯示在後續要求上的原因。
