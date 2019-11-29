---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: 生產網站上的使用者和角色（C#） |Microsoft Docs
author: rick-anderson
description: ASP.NET 網站管理工具（WSAT）提供網頁型使用者介面，可用來設定成員資格和角色設定，以及建立、編輯、。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: c47bd2c1661f129dd8856916de04b8ba459fbfec
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74616655"
---
# <a name="users-and-roles-on-the-production-website-c"></a>生產網站上的使用者和角色（C#）

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> ASP.NET 網站管理工具（WSAT）提供網頁型使用者介面，可用來設定成員資格和角色，以及建立、編輯和刪除使用者和角色。 可惜的是，WSAT 只能在從 localhost 流覽時運作，這表示您無法透過瀏覽器連線至生產網站的系統管理工具。 好消息是，有一些因應措施，可以讓您在生產環境上管理使用者和角色。 本教學課程會探討這些因應措施及其他方法。

## <a name="introduction"></a>簡介

ASP.NET 2.0 引進了許多*應用程式服務*，這是一組您可以新增至 web 應用程式的建立區塊服務。 我們已在「設定[*使用應用程式服務的網站*」教學](configuring-a-website-that-uses-application-services-cs.md)課程中，將「成員資格」和「角色」服務新增至「書籍評論」網站。 成員資格服務可協助建立和管理使用者帳戶;角色服務提供將使用者分類為群組的 API。 本書評論網站有三個使用者帳戶-Scott、Jisun 和 Alice-以及單一角色 Admin，並具有 Scott 和 Jisun 的系統管理員角色。

ASP.NET 的應用程式服務不會系結至特定的執行。 相反地，您會指示應用程式服務使用特定的*提供者*，而該提供者會使用特定技術來執行服務。 我們已設定書籍審查 web 應用程式，以使用成員資格和角色服務的 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者。 這兩個提供者會將使用者帳戶和角色資訊儲存在 SQL Server 資料庫中，而且是裝載于虛擬主機公司之以網際網路為基礎的 web 應用程式最常使用的提供者。

使用成員資格和角色服務的開發人員經常面臨的挑戰，是管理生產環境中的使用者和角色。 如何從生產網站刪除使用者帳戶、加入新的角色，或將現有的使用者新增至現有的角色？ 本教學課程會探索在生產網站上管理使用者和角色的不同技術。

## <a name="using-the-aspnet-web-site-administration-tool"></a>使用 ASP.NET 網站管理工具

ASP.NET 包含[網站管理工具](https://msdn.microsoft.com/library/yy40ytx0.aspx)（WSAT），可讓您輕鬆地建立及管理使用者帳戶和角色，並指定以使用者和角色為基礎的授權規則。 若要使用 WSAT，請按一下 方案總管中的 ASP.NET 設定 圖示，或移至 網站 或 專案 功能表，然後選擇 ASP.NET 設定 選項。 任一種方法都會啟動網頁瀏覽器，並將其指向 WSAT 的位址，例如： `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT 分成三個區段：

- **安全性**-管理使用者、角色和授權規則。
- **Policies.applicationconfiguration** -從這裡管理 &lt;appSettings&gt; 和 SMTP 設定。 您也可以讓應用程式離線，並從這裡管理偵測和追蹤設定，以及指定預設的自訂錯誤網頁。
- **ProviderConfiguration** -設定應用程式服務所使用的提供者。

[安全性] 區段（如 [**圖 1**] 所示）包含用來建立新使用者、管理使用者、建立和管理角色，以及建立和管理存取規則的連結。 您可以從這裡將新角色新增至系統、刪除現有的使用者，或從特定使用者帳戶新增或移除角色。

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**圖 1**： WSAT 安全性區段包含管理使用者和角色的選項  
（[按一下以查看完整大小的影像](users-and-roles-on-the-production-website-cs/_static/image3.png)）

可惜的是，WSAT 只能在本機存取。 您無法造訪遠端生產網站上的 WSAT;如果您造訪 `www.yoursite.com/asp.netwebadminfiles/default.aspx` 會收到「404找不到」回應。 WSAT 的程式碼會使用 .NET Framework 中的 `Membership` 和 `Roles` 類別，來建立、編輯和刪除使用者和角色。 這些類別會參考 web 應用程式的設定資訊，以判斷要使用的提供者;回到設定[*使用應用程式服務的網站*教學](configuring-a-website-that-uses-application-services-cs.md)課程，我們將「書籍評論」網站設為使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者。 這個詳述如下會將 `<membership>` 和 `<roleManager>` 區段新增至 `Web.config`。

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

請注意，`<membership>` 和 `<roleManager>` 區段分別參考其 `type` 屬性中的 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供者。 這些提供者會將使用者和角色資訊儲存在指定的 SQL Server 資料庫中。 這些提供者所使用的資料庫是由 `~/ConfigSections/databaseConnectionStrings.config` 檔中定義的 `connectionStringName` 屬性 `ReviewsConnectionString`所指定。 回想一下，開發環境中的 `databaseConnectionStrings.config` 檔案包含開發資料庫的連接字串，而實際執行的 `databaseConnectionStrings.config` 檔案則包含生產資料庫的連接字串。

簡言之，WSAT 必須透過開發環境在本機存取，而且它會與 `databaseConnectionStrings.config` 檔案所指定之資料庫中的使用者和角色資訊搭配使用。 因此，如果我們在開發環境上變更 `databaseConnectionStrings.config` 檔案中的連接字串資訊，我們可以在本機使用 WSAT 來管理生產環境中的使用者和角色。

若要說明這項功能，請在開發環境的 Visual Studio 中開啟 `databaseConnectionStrings.config` 檔案，然後將開發資料庫連接字串取代為實際執行的資料庫連接字串。 然後啟動 WSAT，並移至 [安全性] 索引標籤，然後新增名為 Sam 且密碼為 "password！" 的新使用者 （較少引號）。 [**圖 2** ] 顯示建立此帳戶時的 WSAT 畫面。

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**圖 2**：在生產環境中建立名為 Sam 的新使用者  
（[按一下以查看完整大小的影像](users-and-roles-on-the-production-website-cs/_static/image6.png)）

因為我們將 `databaseConnectionStrings.config` 中的連接字串變更為指向實際執行的資料庫伺服器，所以 Sam 是以使用者的身分新增到生產環境中。 若要確認這一點，請將 `databaseConnectionStrings.config` 檔案中的連接字串變更回開發資料庫，然後造訪開發環境中的 [`Login.aspx`] 頁面。 嘗試以 Sam 身分登入（請參閱 [**圖 3**]）。

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**圖 3**：您無法在開發環境中以 Sam 的身分登入  
（[按一下以查看完整大小的影像](users-and-roles-on-the-production-website-cs/_static/image9.png)）

您無法在開發環境中以 Sam 的身分登入，因為使用者帳戶資訊不存在於本機資料庫中。 相反地，已加入生產資料庫中。 若要確認這一點，請在開發和生產資料庫中同時查看 `aspnet_Users` 資料表的內容。 在開發環境中，只有 Scott、Jisun 和 Alice 的使用者才會有三筆記錄。 不過，生產資料庫中的 `aspnet_Users` 資料表有四筆記錄： Scott、Jisun、Alice 和 Sam。 因此，Sam 可以在生產環境中透過網站登入，而不是透過開發環境。

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**圖 4**： Sam 可以在生產網站上登入  
（[按一下以查看完整大小的影像](users-and-roles-on-the-production-website-cs/_static/image12.png)）

> [!NOTE]
> 當您完成使用 WSAT 時，別忘了將 `databaseConnectionStrings.config` 檔案中的連接字串變更回開發資料庫的連接字串，否則當您透過開發環境測試網站時，將會使用生產資料。 也請記住，雖然我們剛才討論的技巧可以讓我們使用 WSAT 從遠端系統管理使用者和角色，但變更任何其他 WSAT 設定選項（存取規則、SMTP 設定、偵錯工具和追蹤設定等等）都會修改 `Web.config` 檔案。 因此，對設定所做的任何變更都會套用至開發環境，而不會套用至生產環境。

## <a name="creating-custom-user-and-role-management-web-pages"></a>建立自訂使用者和角色管理網頁

WSAT 提供現成可用的系統來管理使用者和角色，但只能在本機啟動，而且需要變更連接字串資訊，才能管理生產環境中的使用者和角色。 大部分支援使用者帳戶的網站也包含一些使用者和角色管理網頁，可讓系統管理員從網站內的頁面管理使用者和角色。 這類網頁系統管理頁面可讓您更輕鬆地管理使用者和角色，對於可能有許多系統管理員或系統管理員無法存取的網站，或使用 Visual Studio 來啟動 WSAT 的技術背景而言，這是很重要的。

ASP.NET 包含許多內建的登入相關 Web 控制項，可讓您輕鬆地執行這些系統管理網頁，如同拖放。 例如，您可以建立一個頁面，讓系統管理員將 CreateUserWizard 控制項拖曳至頁面上，並設定幾個屬性，以建立新的使用者帳戶。 事實上，如 [**圖 2** ] 所示，在 WSAT 中建立使用者的頁面會使用您可以加入至頁面的相同 CreateUserWizard 控制項。 此外，您可以透過 .NET Framework 中的 `Membership` 和 `Roles` 類別，以程式設計方式取得成員資格和角色服務的功能。 使用這些類別，您可以撰寫程式碼來建立、編輯和刪除使用者和角色，以及新增或移除角色的使用者，以判斷哪些使用者屬於哪些角色，以及執行其他與使用者和角色相關的工作。

在設定[*使用應用程式服務的網站*教學](configuring-a-website-that-uses-application-services-cs.md)課程中，我已將頁面新增至名為 `CreateAccount.aspx`的 `Admin` 資料夾。 此頁面可讓系統管理員將新的使用者帳戶新增至網站，並指定新建立的使用者是否為系統管理員角色（請參閱 [**圖 5**]）。

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**圖 5**：系統管理員可以建立新的使用者帳戶  
（[按一下以查看完整大小的影像](users-and-roles-on-the-production-website-cs/_static/image15.png)）

如需建立使用者和角色管理頁面的詳細資訊，以及使用 `Membership` 和 `Roles` 類別以及與登入相關的 ASP.NET Web 控制項的逐步指示，請務必閱讀我的[網站安全性教學](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程。 您可以在這裡找到如何建立新帳戶、建立和管理角色、將使用者指派給角色和其他一般系統管理工作的網頁指引。

若要在生產網站上執行類似 WSAT 的功能，您一律可以建立自己的一系列網頁來執行 WSAT 的功能。 若要協助您開始使用，請參閱 WSAT 原始程式碼，此程式碼位於資料夾 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`。 另一個選項是使用 Dan Clem 的 WSAT 替代專案，他會在他的文章中分享[自己的網站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)。 Dan 會引導讀者完成建立自訂 WSAT 工具的程式，包括其應用程式的原始程式碼供您下載（在中C#），並提供將自訂 WSAT 加入至託管網站的逐步指示。

## <a name="summary"></a>總結

ASP.NET 網站管理工具（WSAT）可與成員資格和角色應用程式服務一起使用，以管理您網站的使用者和角色資訊。 可惜的是，WSAT 只能在本機存取，無法從您的生產網站造訪。 不過，藉由將開發環境中的連接字串變更為指向實際執行的資料庫，您可以使用 WSAT 來管理生產網站上的使用者和角色。

雖然 WSAT 方法提供快速且輕鬆的方式來管理使用者和角色，但它還是需要從 Visual Studio 啟動 WSAT，以及暫時變更連接字串資訊。 WSAT 提供快速的方式來管理生產環境中的使用者和角色，但非常麻煩，而且對於具有多個系統管理員或沒有或不熟悉 Visual Studio 和 WSAT 的系統管理員而言，並不適用。 基於這些理由，大部分支援使用者帳戶的網站都包含一組系統管理網頁。 這一組網頁不需要 WSAT，而是由各種系統管理使用者從任何電腦使用。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [檢查 ASP。NET 的成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [推出您自己的網站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [網站管理工具總覽](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [網站安全性教學課程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [上一頁](precompiling-your-website-cs.md)
> [下一頁](asp-net-hosting-options-vb.md)
