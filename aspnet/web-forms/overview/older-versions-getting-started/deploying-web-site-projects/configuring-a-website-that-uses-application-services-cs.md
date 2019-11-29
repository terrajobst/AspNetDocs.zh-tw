---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
title: 設定使用應用程式服務的網站（C#） |Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0 版引進了一系列的應用程式服務，這是 .NET Framework 的一部分，並做為一組即將進行的建立區塊服務
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 1e33d1c6-3f9f-4c26-81e2-2a8f8907bb05
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
msc.type: authoredcontent
ms.openlocfilehash: 72aaca84b8c8d6e558d4c946faa57fa999d48bf8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570123"
---
# <a name="configuring-a-website-that-uses-application-services-c"></a>設定使用應用程式服務的網站 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_CS.zip)或[下載 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_cs.pdf)

> ASP.NET 2.0 版引進了一系列的應用程式服務，這是 .NET Framework 的一部分，並作為一套建立區塊服務，讓您可以用來在 web 應用程式中加入豐富的功能。 本教學課程會探索如何在生產環境中設定網站，以使用應用程式服務，並解決在生產環境中管理使用者帳戶和角色的常見問題。

## <a name="introduction"></a>簡介

ASP.NET 2.0 版引進了一系列的*應用程式服務*，這是 .NET Framework 的一部分，並作為一套建立區塊服務，讓您可以用來在 web 應用程式中加入豐富的功能。 應用程式服務包括：

- **成員資格**-用來建立和管理使用者帳戶的 API。
- **角色**-用來將使用者分類為群組的 API。
- **設定檔**-用來儲存自訂的使用者特定內容的 API。
- **網站地圖**-用來以階層形式定義網站 s 邏輯結構的 API，然後可以透過導覽控制項（例如功能表和階層連結）來顯示。
- **個人**化-用來維護自訂喜好設定的 API，最常用於[*webpart*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)。
- **健全狀況監視**-用來監視執行中 web 應用程式的效能、安全性、錯誤和其他系統健全狀況計量的 API。

應用程式服務 Api 不會系結至特定的執行。 相反地，您會指示應用程式服務使用特定的*提供者*，而該提供者會使用特定技術來執行服務。 裝載于虛擬主機公司之以網際網路為基礎的 web 應用程式最常使用的提供者，就是使用 SQL Server 資料庫執行的提供者。 例如，`SqlMembershipProvider` 是成員資格 API 的提供者，會將使用者帳戶資訊儲存在 Microsoft SQL Server 資料庫中。

使用應用程式服務和 SQL Server 提供者，會在部署應用程式時增加一些挑戰。 對於初學者而言，應用程式服務資料庫物件必須在開發和生產資料庫上正確建立，並適當地加以初始化。 此外，也需要進行重要的設定。

> [!NOTE]
> 應用程式服務 Api 是使用[*提供者模型*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)所設計，這是一種設計模式，可讓您在執行時間提供 API 的執行詳細資料。 .NET Framework 隨附多個可以使用的應用程式服務提供者，例如 `SqlMembershipProvider` 和 `SqlRoleProvider`，這是使用 SQL Server 資料庫執行之成員資格和角色 Api 的提供者。 您也可以建立並外掛程式自訂提供者。 事實上，書籍審查 web 應用程式已經包含網站地圖 API （`ReviewSiteMapProvider`）的自訂提供者，它會從資料庫的 `Genres` 和 `Books` 資料表中的資料來建立網站地圖。

本教學課程一開始會介紹我如何擴充書籍評論 web 應用程式，以使用成員資格和角色 Api。 然後逐步解說如何部署使用應用程式服務與 SQL Server 資料庫執行的 web 應用程式，並藉由解決在生產環境中管理使用者帳戶和角色的常見問題來結束。

## <a name="updates-to-the-book-reviews-application"></a>書籍審查應用程式的更新

過去幾個教學課程中，書籍審查 web 應用程式已從靜態網站更新為動態、資料導向的 web 應用程式，並提供一組管理頁面來管理內容和評論。 不過，此管理區段目前並未受到保護-任何知道（或猜測）系統管理頁面 URL 的使用者，都可以在我們的網站上 waltz 及建立、編輯或刪除評論。 保護網站某些部分的常見方式是執行使用者帳戶，然後使用 URL 授權規則來限制特定使用者或角色的存取權。 本教學課程可供您下載的書籍評論 web 應用程式支援使用者帳戶和角色。 它具有名為 Admin 的單一角色，而且只有此角色中的使用者可以存取管理頁面。

> [!NOTE]
> 我曾在本書審查 web 應用程式中建立三個使用者帳戶： Scott、Jisun 和 Alice。 這三個使用者都有相同的密碼： **password！** Scott 和 Jisun 是在系統管理員角色中，而 Alice 則不是。 匿名使用者仍然可以存取網站的非系統管理頁面。 也就是說，除非您想要管理網站，否則您不需要登入，就可以造訪該網站，在此情況下，您必須以系統管理員角色的使用者身分登入。

本書審查應用程式的主版頁面已更新為針對已驗證和匿名使用者包含不同的使用者介面。 如果匿名使用者造訪網站，她會看到右上角的登入連結。 已驗證的使用者會看到訊息：「歡迎回來，使用者*名稱*！」 和登出的連結。另外還有一個登入頁面（`~/Login.aspx`），其中包含一個登入 Web 控制項，可提供驗證訪客的使用者介面和邏輯。 只有系統管理員可以建立新的帳戶。 （您可以在 [`~/Admin`] 資料夾中，建立及管理使用者帳戶的頁面）。

### <a name="configuring-the-membership-and-roles-apis"></a>設定成員資格和角色 Api

本書審查 web 應用程式會使用成員資格和角色 Api 來支援使用者帳戶，並將這些使用者分組為角色（也就是系統管理員角色）。 因為我們想要將帳戶和角色資訊儲存在 SQL Server 資料庫中，所以會使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者類別。

> [!NOTE]
> 本教學課程並非針對設定 web 應用程式以支援成員資格和角色 Api 進行詳細的檢查。 若要徹底瞭解這些 Api，以及設定網站使用它們所需採取的步驟，請閱讀我的[*網站安全性教學*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程。

若要搭配使用應用程式服務與 SQL Server 資料庫，您必須先將這些提供者所使用的資料庫物件，新增至您想要儲存使用者帳戶和角色資訊的資料庫。 這些必要的資料庫物件包括各種資料表、視圖和預存程式。 除非另有指定，否則 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者類別會使用位於應用程式 s `App_Data` 資料夾中名為 `ASPNETDB` 的 SQL Server Express Edition 資料庫;如果這類資料庫不存在，則會在執行時間使用這些提供者自動建立所需的資料庫物件。

在儲存網站的應用程式專屬資料的相同資料庫中建立應用程式服務資料庫物件是可行的，通常是理想的做法。 .NET Framework 隨附名為 `aspnet_regsql.exe` 的工具，它會在指定的資料庫上安裝資料庫物件。 我已經開始使用此工具，將這些物件新增至 `App_Data` 資料夾（開發資料庫）中的 `Reviews.mdf` 資料庫。 我們將在本教學課程稍後將這些物件新增至生產資料庫時，瞭解如何使用此工具。

如果您將應用程式服務資料庫物件加入至以外的 `ASPNETDB` 資料庫，就必須自訂 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者類別設定，使其使用適當的資料庫。 若要自訂成員資格提供者，請在 `Web.config`的 `<system.web>` 區段中新增[ *&lt;成員資格&gt; 元素*](https://msdn.microsoft.com/library/1b9hw62f.aspx)。使用[ *&lt;roleManager&gt; 元素*](https://msdn.microsoft.com/library/ms164660.aspx)來設定角色提供者。 下列程式碼片段取自書籍審查應用程式 `Web.config`，並顯示成員資格和角色 Api 的設定。 請注意，同時註冊新的提供者 `ReviewMembership` 和 `ReviewRole`，分別使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample1.xml)]

`Web.config` 檔案 s `<authentication>` 元素也已設定為支援表單架構驗證。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>限制系統管理頁面的存取權

ASP.NET 可讓使用者或角色透過其*URL 授權*功能，輕鬆地授與或拒絕存取特定檔案或資料夾。 （我們在*iis 與 ASP.NET 程式開發伺服器教學課程之間的核心差異*中簡要討論了 url 授權，並示範 iis 和 ASP.NET 程式開發伺服器如何以不同的方式套用靜態與動態內容的 url 授權規則）。因為我們想要禁止 `~/Admin` 存取 [系統管理員] 角色中的使用者，否則我們必須在此資料夾中新增 URL 授權規則。 具體而言，URL 授權規則必須允許系統管理員角色的使用者，並拒絕所有其他使用者。 這是藉由使用下列內容將 `Web.config` 檔案新增至 `~/Admin` 資料夾來完成：

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample3.xml)]

如需 ASP.NET s URL 授權功能的詳細資訊，以及如何使用它來為使用者和角色簽出授權規則，請務必閱讀我的[*網站安全性教學*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程中的以[*使用者為基礎的授權*](../../older-versions-security/membership/user-based-authorization-cs.md)和以[*角色為基礎的授權*](../../older-versions-security/roles/role-based-authorization-cs.md)教學課程。

## <a name="deploying-a-web-application-that-uses-application-services"></a>部署使用應用程式服務的 Web 應用程式

當部署使用應用程式服務的網站，以及將應用程式服務資訊儲存在資料庫中的提供者時，必須在生產資料庫上建立應用程式服務所需的資料庫物件。 一開始，生產資料庫不會包含這些物件，因此當第一次部署應用程式時（或是在加入應用程式服務之後第一次部署時），您必須採取額外的步驟，才能在上取得這些必要的資料庫物件。生產資料庫。

如果您想要將在開發環境中建立的使用者帳戶複寫到生產環境，部署使用應用程式服務的網站時，可能會發生另一項挑戰。 視成員資格和角色的設定而定，即使您成功地將在開發環境中建立的使用者帳戶複製到實際執行的資料庫，這些使用者還是無法登入生產環境中的 web 應用程式。 我們將探討此問題的原因，並討論如何避免發生這種情況。

ASP.NET 隨附一個絕佳的[*網站管理工具（WSAT）* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) ，可從 Visual Studio 啟動，並允許透過 Web 型介面來管理使用者帳戶、角色和授權規則。 可惜的是，WSAT 只適用于本機網站，這表示它不能用來從遠端系統管理生產環境中 web 應用程式的使用者帳戶、角色和授權規則。 我們將探討不同的方法，從您的生產網站執行類似 WSAT 的行為。

### <a name="adding-the-database-objects-using-aspnet_regsqlexe"></a>使用 aspnet\_regsql 新增資料庫物件

*部署資料庫*教學課程示範如何將資料表和資料從開發資料庫複製到實際執行資料庫，而這些技巧當然可以用來將應用程式服務資料庫物件複製到實際執行資料庫。 另一個選項是 `aspnet_regsql.exe` 工具，它會從資料庫新增或移除應用程式服務資料庫物件。

> [!NOTE]
> `aspnet_regsql.exe` 工具會在指定的資料庫上建立資料庫物件。 它不會將這些資料庫物件中的資料從開發資料庫移轉到生產資料庫。 如果您想要將開發資料庫中的使用者帳戶和角色資訊複製到實際執行資料庫，請使用*部署資料庫*教學課程中所涵蓋的技術。

讓我們看看如何使用 `aspnet_regsql.exe` 工具，將資料庫物件加入至生產資料庫。 一開始請開啟 Windows Explorer，流覽至電腦上的 .NET Framework 2.0 版目錄，% WINDIR% \NET\Framework\v2.0.50727。 您應該會找到 `aspnet_regsql.exe` 工具。 此工具可從命令列使用，但它也包含圖形化使用者介面;按兩下 [`aspnet_regsql.exe`] 檔案以啟動其圖形元件。

此工具一開始會顯示一個說明其用途的啟動顯示畫面。 按 [下一步] 進入 [選取安裝選項] 畫面，如 [圖 1] 所示。 您可以從這裡加入宣告應用程式服務資料庫物件，或從資料庫中移除它們。 因為我們想要將這些物件新增至生產資料庫，請選取 [設定應用程式服務的 SQL Server] 選項，然後按 [下一步]。

[![選擇設定應用程式服務的 SQL Server](configuring-a-website-that-uses-application-services-cs/_static/image2.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image1.jpg)

**圖 1**：選擇設定應用程式服務的 SQL Server （[按一下以查看完整大小的影像](configuring-a-website-that-uses-application-services-cs/_static/image3.jpg)）

在 [選取伺服器和資料庫] 畫面中，會提示您提供連接到資料庫的資訊。 輸入您的 web 主控公司提供的資料庫伺服器、安全性認證和資料庫名稱，然後按 [下一步]。

> [!NOTE]
> 輸入您的資料庫伺服器和認證之後，您可能會在展開 [資料庫] 下拉式清單時收到錯誤。 `aspnet_regsql.exe` 工具會查詢 `sysdatabases` 系統資料表，以取得伺服器上的資料庫清單，但某些虛擬主機公司會鎖定其資料庫伺服器，讓這項資訊無法公開使用。 如果您收到此錯誤，您可以直接在下拉式清單中輸入資料庫名稱。

[![提供您資料庫的連接資訊給工具](configuring-a-website-that-uses-application-services-cs/_static/image5.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image4.jpg)

**圖 2**：提供工具與您的資料庫連接資訊（[按一下以觀看完整大小的影像](configuring-a-website-that-uses-application-services-cs/_static/image6.jpg)）

後續畫面會匯總即將發生的動作，亦即應用程式服務資料庫物件將會加入至指定的資料庫。 按 [下一步] 完成此動作。 幾分鐘後，就會顯示最後一個畫面，請注意，已加入資料庫物件（請參閱 [圖 3]）。

[![成功！應用程式服務資料庫物件已加入至生產資料庫](configuring-a-website-that-uses-application-services-cs/_static/image8.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image7.jpg)

**圖 3**：成功！ 應用程式服務資料庫物件已加入至生產資料庫（[按一下以查看完整大小的影像](configuring-a-website-that-uses-application-services-cs/_static/image9.jpg)）

若要確認應用程式服務資料庫物件已成功加入至生產資料庫，請開啟 SQL Server Management Studio 並聯機到您的生產環境資料庫。 如 [圖 4] 所示，您現在應該會看到資料庫中的應用程式服務資料庫資料表、`aspnet_Applications`、`aspnet_Membership`、`aspnet_Users`等等。

[![確認資料庫物件已加入至生產資料庫](configuring-a-website-that-uses-application-services-cs/_static/image11.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image10.jpg)

**圖 4**：確認資料庫物件已加入至生產資料庫（[按一下以查看完整大小的影像](configuring-a-website-that-uses-application-services-cs/_static/image12.jpg)）

您只需要在第一次部署 web 應用程式時，或在您開始使用應用程式服務之後首次使用 `aspnet_regsql.exe` 工具。 一旦這些資料庫物件位於生產資料庫上，就不需要重新加入或修改。

### <a name="copying-user-accounts-from-development-to-production"></a>將使用者帳戶從開發複製到生產環境

使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者類別將應用程式服務資訊儲存在 SQL Server 資料庫時，使用者帳戶和角色資訊會儲存在各種不同的資料庫資料表中，包括 `aspnet_Users`、`aspnet_Membership`、`aspnet_Roles`和 `aspnet_UsersInRoles`等等。 在開發期間，您會在開發環境中建立使用者帳戶，藉由從適用的資料庫資料表複製對應的記錄，即可在生產環境中複寫這些使用者帳戶。 如果您使用 [資料庫發佈嚮導] 來部署應用程式服務資料庫物件，您可能也已選擇複製記錄，這會導致在開發期間建立的使用者帳戶也會在生產環境中。 但視您的設定而定，您可能會發現那些帳戶在開發中建立並複製到生產環境的使用者無法從生產網站登入。 那該怎麼做呢？

`SqlMembershipProvider` 和 `SqlRoleProvider` 提供者類別的設計，就是單一資料庫可做為多個應用程式的使用者存放區，而每個應用程式在理論上，都有具有相同名稱的使用者和角色重迭。 為了允許此彈性，資料庫會維護 `aspnet_Applications` 資料表中的應用程式清單，而每個使用者都與這些應用程式的其中一個相關聯。 具體而言，`aspnet_Users` 資料表具有 `ApplicationId` 資料行，其會將每個使用者系結至 `aspnet_Applications` 資料表中的記錄。

除了 `ApplicationId` 資料行之外，`aspnet_Applications` 資料表也包含 `ApplicationName` 的資料行，可為應用程式提供更好的易記名稱。 當網站嘗試使用使用者帳戶時（例如從登入頁面驗證使用者的認證），必須告知 `SqlMembershipProvider` 類別要使用哪個應用程式。 它通常會藉由提供應用程式名稱來完成這項工作，而此值是來自 `Web.config` 中的提供者 s 設定-特別是透過 `applicationName` 屬性。

但是，如果 `Web.config`中未指定 `applicationName` 屬性，會發生什麼事？ 在這種情況下，成員資格系統會使用應用程式根目錄路徑作為 `applicationName` 值。 如果未在 `Web.config`中明確設定 `applicationName` 屬性，則開發環境和生產環境可能會使用不同的應用程式根目錄，因此會與應用程式服務中的不同應用程式名稱產生關聯。 如果發生這種不相符的情況，在開發環境中建立的使用者將會有 `ApplicationId` 值與生產環境的 `ApplicationId` 值不相符。 最終結果是那些使用者將無法登入。

> [!NOTE]
> 如果您在這種情況下發現自己-使用 `ApplicationId` 值不相符的使用者帳戶複製到生產環境，您可以撰寫查詢，將這些不正確的 `ApplicationId` 值更新為生產環境中所使用的 `ApplicationId`。 更新之後，在開發環境中建立帳戶的使用者現在將能夠在實際執行時登入 web 應用程式。

好消息是，您可以採取一個簡單的步驟，以確保兩個環境使用相同的 `ApplicationId`-在 `Web.config` 中明確設定所有應用程式服務提供者的 `applicationName` 屬性。 我在 `<membership>` 和 `<roleManager>` 專案中，將 `applicationName` 屬性明確設定為 "BookReviews"，如同 `Web.config` 顯示的這個程式碼片段。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample4.xml)]

如需有關設定 `applicationName` 屬性和其背後原理的詳細討論，請參閱[*Scott Guthrie*](https://weblogs.asp.net/scottgu/)的 blog 文章：[*設定 ASP.NET 成員資格和其他提供者時，一律設定 applicationName 屬性*](https://weblogs.asp.net/scottgu/443634)。

### <a name="managing-user-accounts-in-the-production-environment"></a>管理生產環境中的使用者帳戶

ASP.NET 網站管理工具（WSAT）可讓您輕鬆地建立和管理使用者帳戶、定義和套用角色，以及將使用者和角色型授權規則拼出。 您可以前往 [方案總管]，然後按一下 [ASP.NET 設定] 圖示，或前往 [網站] 或 [專案] 功能表，然後選取 [ASP.NET 設定] 功能表項目，從 Visual Studio 啟動 WSAT。 可惜的是，WSAT 只能搭配本機網站使用。 因此，您無法從您的工作站使用 WSAT 來管理生產環境中的網站。

好消息是，WSAT 所提供的所有功能都可透過成員資格和角色 Api 以程式設計方式取得;此外，許多 WSAT 畫面都使用標準的 ASP.NET 登入相關控制項。 簡言之，您可以將 ASP.NET 網頁新增至您的網站，以提供必要的管理功能。

回想一下，先前的教學課程已更新書籍審查 web 應用程式以包含 `~/Admin` 資料夾，而且此資料夾已設定為只允許系統管理員角色中的使用者。 我在名為 `CreateAccount.aspx` 的資料夾中新增了一個頁面，系統管理員可以從這裡建立新的使用者帳戶。 此頁面使用 CreateUserWizard 控制項來顯示用來建立新使用者帳戶的使用者介面和後端邏輯。 再來，我自訂控制項以包含一個核取方塊，提示新使用者是否也應新增至系統管理員角色（請參閱 [圖 5]）。 有了一些工作，您可以建立一組自訂的頁面，以執行 WSAT 所提供的使用者和角色管理相關工作。

> [!NOTE]
> 如需有關使用成員資格和角色 Api 以及與登入相關的 ASP.NET Web 控制項的詳細資訊，請務必閱讀我的[*網站安全性教學*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程。 如需自訂 CreateUserWizard 控制項的詳細資訊，請參閱[*建立使用者帳戶*](../../older-versions-security/membership/creating-user-accounts-cs.md)和[*儲存其他使用者資訊*](../../older-versions-security/membership/storing-additional-user-information-cs.md)教學課程，或查看[*Erich Peterson*](http://www.erichpeterson.com/) s 文章：[*自訂 CreateUserWizard 控制項*](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)。

[![系統管理員可以建立新的使用者帳戶](configuring-a-website-that-uses-application-services-cs/_static/image14.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image13.jpg)

[**圖 5**]：系統管理員可以建立新的使用者帳戶（[按一下以觀看完整大小的影像](configuring-a-website-that-uses-application-services-cs/_static/image15.jpg)）

如果您需要 WSAT 的完整功能，請參閱[*推出您自己的網站管理工具*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)，其中作者 Dan Clem 會逐步解說建立自訂 WSAT 工具的程式。 Dan 會共用其應用程式的原始程式碼（ C#在中），並提供逐步指示，說明如何將其新增至您的託管網站。

## <a name="summary"></a>總結

當部署使用應用程式服務資料庫執行的 web 應用程式時，您必須先確定生產資料庫具有必要的資料庫物件。 您可以使用*部署資料庫*教學課程中所討論的技術來新增這些物件;或者，您可以使用 `aspnet_regsql.exe` 工具，如我們在本教學課程中所見。 我們在同步處理開發和生產環境中所使用的應用程式名稱時所觸及的其他挑戰（如果您想要在開發環境中建立的使用者和角色在實際執行時有效，這點很重要）和技術管理生產環境中的使用者和角色。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [*ASP.NET SQL Server 註冊工具（aspnet_regsql .exe）* ](https://msdn.microsoft.com/library/ms229862.aspx)
- [*建立 SQL Server 的應用程式服務資料庫*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*在 SQL Server 中建立成員資格架構*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)
- [*檢查 ASP.NET 的成員資格、角色和設定檔*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*推出您自己的網站管理工具*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*網站安全性教學課程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*網站管理工具總覽*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [上一頁](configuring-the-production-web-application-to-use-the-production-database-cs.md)
> [下一頁](strategies-for-database-development-and-deployment-cs.md)
