---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
title: 建立和管理角色（C#） |Microsoft Docs
author: rick-anderson
description: 本教學課程會檢查設定角色架構所需的步驟。 之後，我們將建立網頁來建立及刪除角色。
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 113f10b3-a19a-471b-8ff6-db3c79ce8a91
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
msc.type: authoredcontent
ms.openlocfilehash: a7883d0b05f2fa5a3fdac887f8c8b39d70418fb3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595856"
---
# <a name="creating-and-managing-roles-c"></a>建立及管理角色 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.09.zip)或[下載 PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_cs.pdf)

> 本教學課程會檢查設定角色架構所需的步驟。 之後，我們將建立網頁來建立及刪除角色。

## <a name="introduction"></a>簡介

在以<a id="_msoanchor_1"> </a>[*使用者為基礎的授權*](../membership/user-based-authorization-cs.md)教學課程中，我們探討了如何使用 URL 授權，從一組頁面限制特定使用者，並探索宣告式和程式設計技巧，以根據造訪的使用者調整 ASP.NET 網頁的功能。 不過，以使用者為基礎授與頁面存取或功能的許可權，但在有許多使用者帳戶或使用者的許可權經常變更的情況下，可能會變得很麻煩。 每當使用者取得或失去執行特定工作的授權時，系統管理員就必須更新適當的 URL 授權規則、宣告式標記和程式碼。

它通常有助於將使用者分類為群組或*角色*，然後依角色逐一套用許可權。 例如，大部分的 web 應用程式都有一組特定的頁面或工作，只保留給系統管理使用者。 使用以使用者為基礎的*授權*教學課程中所學到的技術，我們將新增適當的 URL 授權規則、宣告式標記和程式碼，以允許指定的使用者帳戶執行系統管理工作。 但是，如果已加入新的系統管理員，或現有的系統管理員需要撤銷其管理許可權，我們就必須傳回並更新設定檔和網頁。 不過，有了角色，我們可以建立一個名為 Administrators 的角色，並將這些信任的使用者指派給系統管理員角色。 接下來，我們要新增適當的 URL 授權規則、宣告式標記和程式碼，讓系統管理員角色能夠執行各種系統管理工作。 當此基礎結構就緒時，將新的系統管理員加入至網站或移除現有的系統管理員，就像在 [系統管理員] 角色中包含或移除使用者一樣簡單。 不需要設定、宣告式標記或程式碼變更。

ASP.NET 提供角色架構來定義角色，並將它們與使用者帳戶建立關聯。 有了角色架構，我們就可以建立和刪除角色、在角色中新增使用者或移除使用者、判斷屬於特定角色的使用者集合，以及判斷使用者是否屬於特定角色。 一旦設定了角色架構，我們就可以透過 URL 授權規則來限制每個角色對頁面的存取權，並根據目前登入的使用者角色，顯示或隱藏頁面上的其他資訊或功能。

本教學課程會檢查設定角色架構所需的步驟。 之後，我們將建立網頁來建立及刪除角色。 在將<a id="_msoanchor_2"> </a>[*角色指派給使用者*](assigning-roles-to-users-cs.md)教學課程中，我們將探討如何從角色新增和移除使用者。 在以<a id="_msoanchor_3"> </a>[*角色為基礎的授權*](role-based-authorization-cs.md)教學課程中，我們將瞭解如何依角色來限制頁面的存取權，以及如何根據造訪的使用者角色來調整頁面功能。 讓我們開始吧！

## <a name="step-1-adding-new-aspnet-pages"></a>步驟1：加入新的 ASP.NET 網頁

在本教學課程和接下來的兩個中，我們將探討各種角色相關的功能和功能。 我們將需要一系列的 ASP.NET 網頁，以執行整個教學課程中所探討的主題。 讓我們建立這些頁面並更新網站地圖。

首先，在名為 `Roles`的專案中建立新的資料夾。 接下來，在 [`Roles`] 資料夾中新增四個新的 ASP.NET 網頁，並將每個頁面與 `Site.master` 主版頁面連結。 將頁面命名為：

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

此時，專案的方案總管看起來應該像 [圖 1] 所示的螢幕擷取畫面。

[[角色] 資料夾中已加入 ![四個新頁面](creating-and-managing-roles-cs/_static/image2.png)](creating-and-managing-roles-cs/_static/image1.png)

**圖 1**： [`Roles`] 資料夾中已加入四個新頁面（[按一下以觀看完整大小的影像](creating-and-managing-roles-cs/_static/image3.png)）

此時，每個頁面都應該有兩個內容控制項，每一個主版頁面的 ContentPlaceHolders： `MainContent` 和 `LoginContent`。

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample1.aspx)]

回想一下，`LoginContent` ContentPlaceHolder 的預設標記會根據使用者是否經過驗證，顯示登入或登出網站的連結。 不過，ASP.NET 網頁中存在 `Content2` 內容控制項，會覆寫主版頁面的預設標記。 如我們在<a id="_msoanchor_4"> </a>[*表單驗*](../introduction/an-overview-of-forms-authentication-cs.md)證教學課程的總覽中所討論，覆寫預設標記在頁面中很有用，因為我們不想要在左欄中顯示登入相關的選項。

不過，針對這四個頁面，我們想要顯示主版頁面的 `LoginContent` ContentPlaceHolder 的預設標記。 因此，請移除 `Content2` 內容控制項的宣告式標記。 這麼做之後，四個頁面的每一個標記都應該只包含一個內容控制項。

最後，讓我們更新網站地圖（`Web.sitemap`）以包含這些新的網頁。 在我們為成員資格教學課程新增的 `<siteMapNode>` 之後，新增下列 XML。

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample2.xml)]

更新網站地圖之後，請透過瀏覽器造訪網站。 如 [圖 2] 所示，左邊的導覽現在包含角色教學課程的專案。

[[角色] 資料夾中已加入 ![四個新頁面](creating-and-managing-roles-cs/_static/image5.png)](creating-and-managing-roles-cs/_static/image4.png)

**圖 2**：已將四個新頁面新增至 [`Roles`] 資料夾（[按一下以查看完整大小的影像](creating-and-managing-roles-cs/_static/image6.png)）

## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>步驟2：指定及設定角色架構提供者

如同成員資格架構，角色架構是建立在提供者模型的上方。 如<a id="_msoanchor_5"> </a>[*安全性基本概念和 ASP.NET 支援*](../introduction/security-basics-and-asp-net-support-cs.md)教學課程中所述，.NET Framework 隨附三個內建角色提供者： [`AuthorizationStoreRoleProvider`](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx)、 [`WindowsTokenRoleProvider`](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx)和[`SqlRoleProvider`](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)。 本教學課程系列著重于 `SqlRoleProvider`，其使用 Microsoft SQL Server 資料庫做為角色存放區。

底下的角色架構和 `SqlRoleProvider` 的工作就像成員資格架構和 `SqlMembershipProvider`。 .NET Framework 包含 `Roles` 類別，可作為角色架構的 API。 `Roles` 類別具有像 `CreateRole`、`DeleteRole`、`GetAllRoles`、`AddUserToRole`、`IsUserInRole`等等的靜態方法。 當叫用這些方法的其中之一時，`Roles` 類別會將呼叫委派給已設定的提供者。 `SqlRoleProvider` 適用于特定角色的資料表（`aspnet_Roles` 和 `aspnet_UsersInRoles`）以回應。

為了在我們的應用程式中使用 `SqlRoleProvider` 提供者，我們必須指定要做為存放區使用的資料庫。 `SqlRoleProvider` 預期指定的角色存放區具有特定資料庫資料表、視圖和預存程式。 您可以使用[`aspnet_regsql.exe` 工具](https://msdn.microsoft.com/library/ms229862.aspx)來新增這些必要的資料庫物件。 此時，我們已經有一個資料庫，其中包含了 `SqlRoleProvider`所需的架構。 <a id="_msoanchor_6"></a>回到在[*SQL Server 建立成員資格架構*](../membership/creating-the-membership-schema-in-sql-server-cs.md)教學課程中，我們建立了名為 `SecurityTutorials.mdf` 的資料庫，並使用 `aspnet_regsql.exe` 加入應用程式服務，其中包含 `SqlRoleProvider`所需的資料庫物件。 因此，我們只需要告訴角色架構啟用角色支援，並使用 `SqlRoleProvider` 搭配 `SecurityTutorials.mdf` 資料庫作為角色存放區。

角色架構是透過應用程式 `Web.config` 檔中的 &lt;`roleManager`&gt; 元素來設定。 預設會停用角色支援。 若要啟用它，您必須將[&lt;`roleManager`&gt;](https://msdn.microsoft.com/library/ms164660.aspx)元素的 `enabled` 屬性設定為 `true`，如下所示：

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample3.xml)]

根據預設，所有 web 應用程式都有一個名為 `AspNetSqlRoleProvider` 類型為 `SqlRoleProvider`的角色提供者。 這個預設提供者會在 `machine.config` 中註冊（位於 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`）：

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample4.xml)]

提供者的 `connectionStringName` 屬性會指定所使用的角色存放區。 `AspNetSqlRoleProvider` 提供者會將這個屬性設定為 `LocalSqlServer`，這也會在 `machine.config` 和點中定義為 `App_Data` 資料夾中名為 `aspnet.mdf`的 SQL Server 2005 Express Edition 資料庫。

因此，如果我們只在應用程式的 `Web.config` 檔中啟用角色架構，而不指定任何提供者資訊，應用程式就會使用預設的已註冊角色提供者，`AspNetSqlRoleProvider`。 如果 `~/App_Data/aspnet.mdf` 資料庫不存在，ASP.NET 執行時間會自動建立它並加入應用程式服務架構。 不過，我們不想要使用 `aspnet.mdf` 資料庫;相反地，我們想要使用我們已建立的 `SecurityTutorials.mdf` 資料庫，並將應用程式服務架構新增至。 這項修改可以透過下列兩種方式的其中一種來完成：

- 在<strong>`Web.config`</strong>中<strong>指定</strong><strong>`LocalSqlServer`</strong><strong>連接字串名稱</strong>的值<strong>。</strong> 藉由覆寫 `Web.config`中的 `LocalSqlServer` 連接字串名稱值，我們可以使用預設的已註冊角色提供者（`AspNetSqlRoleProvider`），並讓它正確地使用 `SecurityTutorials.mdf` 資料庫。 如需這項技術的詳細資訊，請參閱[Scott Guthrie](https://weblogs.asp.net/scottgu/)的 blog 文章，[將 ASP.NET 2.0 應用程式服務設定為使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)。
- <strong>新增`SqlRoleProvider`類型的已註冊提供者</strong> <strong>，並將其</strong><strong>`connectionStringName`</strong><strong>設定設為指向</strong><strong>`SecurityTutorials.mdf`</strong><strong>資料庫。</strong> 這是我在 SQL Server 教學課程中<a id="_msoanchor_7"> </a>[*建立成員資格架構*](../membership/creating-the-membership-schema-in-sql-server-cs.md)時所建議和使用的方法，而且也是我將在本教學課程中使用的方法。

將下列角色設定標記新增至 `Web.config` 檔案。 此標記會註冊名為 `SecurityTutorialsSqlRoleProvider`的新提供者。

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample5.xml)]

上述標記會將 `SecurityTutorialsSqlRoleProvider` 定義為預設提供者（透過 `<roleManager>` 元素中的 `defaultProvider` 屬性）。 它也會將 `SecurityTutorialsSqlRoleProvider`的 `applicationName` 設定設定為 `SecurityTutorials`，這是成員資格提供者（`SecurityTutorialsSqlMembershipProvider`）所使用的相同 `applicationName` 設定。 雖然此處未顯示，但 `SqlRoleProvider` 的[`<add>` 元素](https://msdn.microsoft.com/library/ms164662.aspx)也可能包含 `commandTimeout` 屬性，以指定資料庫超時時間（以秒為單位）。 預設值是 30。

當此設定標記備妥之後，我們就可以開始在應用程式中使用角色功能。

> [!NOTE]
> 上述設定標記說明如何使用 &lt;`roleManager`&gt; 元素的 `enabled` 和 `defaultProvider` 屬性。 還有一些其他屬性會影響角色架構如何以使用者為基礎來關聯角色資訊。 我們將在以<a id="_msoanchor_8"> </a>[*角色為基礎的授權*](role-based-authorization-cs.md)教學課程中檢查這些設定。

## <a name="step-3-examining-the-roles-api"></a>步驟3：檢查角色 API

角色架構的功能是透過[`Roles` 類別](https://msdn.microsoft.com/library/system.web.security.roles.aspx)公開，其中包含13個用於執行角色型作業的靜態方法。 當我們查看在步驟4和6中建立和刪除角色時，將會使用[`CreateRole`](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx)和[`DeleteRole`](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx)方法，這會在系統中新增或移除角色。

若要取得系統中所有角色的清單，請使用[`GetAllRoles` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)（請參閱步驟5）。 [`RoleExists` 方法](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx)會傳回布林值，指出指定的角色是否存在。

在下一個教學課程中，我們將探討如何將使用者與角色產生關聯。 `Roles` 類別的[`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)、 [`AddUserToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx)、 [`AddUsersToRole`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx)和[`AddUsersToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx)方法會將一或多個使用者新增至一或多個角色。 若要從角色中移除使用者，請使用[`RemoveUserFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)、 [`RemoveUserFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx)、 [`RemoveUsersFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx)或[`RemoveUsersFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx)方法。

在以<a id="_msoanchor_9"> </a>[*角色為基礎的授權*](role-based-authorization-cs.md)教學課程中，我們將探討以程式設計方式，根據目前登入的使用者角色來顯示或隱藏功能的方式。 為了達成此目的，我們可以使用 `Role` 類別的[`FindUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx)、 [`GetRolesForUser`](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)、 [`GetUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)或[`IsUserInRole`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)方法。

> [!NOTE]
> 請記住，每當叫用其中一種方法時，`Roles` 類別就會將呼叫委派給已設定的提供者。 在我們的案例中，這表示會將呼叫傳送至 `SqlRoleProvider`。 然後，`SqlRoleProvider` 會根據叫用的方法執行適當的資料庫作業。 例如，程式碼 `Roles.CreateRole("Administrators")` 會導致 `SqlRoleProvider` 執行 `aspnet_Roles_CreateRole` 預存程式，這會將新記錄插入名為 Administrators 的 `aspnet_Roles` 資料表。

本教學課程的其餘部分將探討如何使用 `Roles` 類別的 `CreateRole`、`GetAllRoles`和 `DeleteRole` 方法來管理系統中的角色。

## <a name="step-4-creating-new-roles"></a>步驟4：建立新的角色

角色提供任意群組使用者的方式，而且最常見的群組是用來更方便的方式來套用授權規則。 但是，若要使用角色做為授權機制，我們必須先定義應用程式中存在哪些角色。 可惜的是，ASP.NET 不包含 CreateRoleWizard 控制項。 為了加入新的角色，我們需要建立適當的使用者介面，並自行叫用角色 API。 好消息是，這很容易完成。

> [!NOTE]
> 雖然沒有 CreateRoleWizard Web 控制項，但有[ASP.NET 的網站管理工具](https://msdn.microsoft.com/library/ms228053.aspx)，它是一種本機 ASP.NET 應用程式，專門設計來協助您查看和管理 Web 應用程式的設定。 不過，我不是 ASP.NET 網站管理工具的大風扇，原因有兩個。 首先，這有點錯誤，而使用者經驗卻不太需要。 第二，ASP.NET 網站管理工具的設計是只在本機上工作，這表示如果您需要從遠端系統管理即時網站上的角色，就必須建立自己的角色管理網頁。 基於這兩個原因，本教學課程和下一步將著重于在網頁中建立必要的角色管理工具，而不是依賴 ASP.NET 的網站管理工具。

開啟 [`Roles`] 資料夾中的 [`ManageRoles.aspx`] 頁面，然後在頁面中加入 TextBox 和 Button Web 控制項。 將 TextBox 控制項的 `ID` 屬性設定為 [`RoleName`]，然後將按鈕的 `ID` 和 `Text` 屬性分別設為 [`CreateRoleButton`] 和 [建立角色]。 此時，您頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample6.aspx)]

接下來，按兩下設計工具中的 [`CreateRoleButton`] 按鈕控制項，以建立 `Click` 事件處理常式，然後新增下列程式碼：

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample7.cs)]

上述程式碼一開始會將 [`RoleName`] 文字方塊中輸入的修剪角色名稱，指派給 `newRoleName` 變數。 接下來，會呼叫 `Roles` 類別的 `RoleExists` 方法，以判斷角色 `newRoleName` 是否已存在於系統中。 如果角色不存在，則會透過呼叫 `CreateRole` 方法來建立。 如果將已存在系統中的角色名稱傳遞給 `CreateRole` 方法，則會擲回 `ProviderException` 例外狀況。 這就是為什麼程式碼會先檢查以確保該角色不存在於系統中，然後才呼叫 `CreateRole`。 `Click` 事件處理常式會藉由清除 `RoleName` TextBox 的 `Text` 屬性來結束。

> [!NOTE]
> 您可能想知道，如果使用者未在 [`RoleName`] 文字方塊中輸入任何值，將會發生什麼事。 如果傳入 `CreateRole` 方法的值為 `null` 或空字串，則會引發例外狀況。 同樣地，如果角色名稱包含逗號，則會引發例外狀況。 因此，此頁面應該包含驗證控制項，以確保使用者輸入角色，且不包含任何逗號。 我為讀者保持練習。

讓我們建立一個名為 Administrators 的角色。 透過瀏覽器造訪 `ManageRoles.aspx` 頁面，在文字方塊中輸入 Administrators （請參閱 [圖 3]），然後按一下 [建立角色] 按鈕。

[![建立系統管理員角色](creating-and-managing-roles-cs/_static/image8.png)](creating-and-managing-roles-cs/_static/image7.png)

**圖 3**：建立系統管理員角色（[按一下以觀看完整大小的影像](creating-and-managing-roles-cs/_static/image9.png)）

會發生什麼事？ 發生回傳，但是沒有視覺提示，因為該角色實際上已加入系統中。 我們會在步驟5中更新此頁面，以包含視覺效果的意見反應。 不過，現在您可以前往 [`SecurityTutorials.mdf`] 資料庫，並顯示 [`aspnet_Roles`] 資料表中的資料，來確認角色是否已建立。 如 [圖 4] 所示，[`aspnet_Roles`] 資料表包含剛新增之系統管理員角色的記錄。

[![aspnet_Roles 資料表包含系統管理員的資料列](creating-and-managing-roles-cs/_static/image11.png)](creating-and-managing-roles-cs/_static/image10.png)

**圖 4**： `aspnet_Roles` 資料表有系統管理員的資料列（[按一下以查看完整大小的影像](creating-and-managing-roles-cs/_static/image12.png)）

## <a name="step-5-displaying-the-roles-in-the-system"></a>步驟5：顯示系統中的角色

讓我們擴大 [`ManageRoles.aspx`] 頁面，以包含系統中目前角色的清單。 若要完成此動作，請將 GridView 控制項新增至頁面，並將其 `ID` 屬性設為 `RoleList`。 接下來，使用下列程式碼，將方法加入至頁面的程式碼後置類別（名為 `DisplayRolesInGrid`）：

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample8.cs)]

`Roles` 類別的 `GetAllRoles` 方法會以字串陣列的形式傳回系統中的所有角色。 這個字串陣列接著會系結至 GridView。 若要在第一次載入頁面時將角色清單系結至 GridView，我們需要從頁面的 `Page_Load` 事件處理常式中呼叫 `DisplayRolesInGrid` 方法。 下列程式碼會在第一次流覽頁面時呼叫這個方法，而不是在後續的回傳上。

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample9.cs)]

將此程式碼備妥之後，請透過瀏覽器造訪頁面。 如 [圖 5] 所示，您應該會看到一個方格，其中包含標示為 Item 的單一資料行。 方格會針對我們在步驟4中新增的系統管理員角色包含一個資料列。

[![GridView 在單一資料行中顯示角色](creating-and-managing-roles-cs/_static/image14.png)](creating-and-managing-roles-cs/_static/image13.png)

**圖 5**： GridView 會在單一資料行中顯示角色（[按一下以查看完整大小的影像](creating-and-managing-roles-cs/_static/image15.png)）

GridView 會顯示標示為 [專案] 的獨立資料行，因為 GridView 的 `AutoGenerateColumns` 屬性設定為 True （預設值），這會導致 GridView 自動為其 `DataSource`中的每個屬性建立資料行。 陣列具有單一屬性，代表陣列中的元素，因此是 GridView 中的單一資料行。

使用 GridView 顯示資料時，我偏好明確定義我的資料行，而不是由 GridView 隱含產生。 藉由明確定義資料行，就能更輕鬆地將資料格式化、重新排列資料行，以及執行其他一般工作。 因此，讓我們更新 GridView 的宣告式標記，以便明確地定義其資料行。

首先，將 GridView 的 `AutoGenerateColumns` 屬性設定為 False。 接下來，將 TemplateField 新增至方格，將其 `HeaderText` 屬性設為 角色，並設定其 `ItemTemplate`，讓它顯示陣列的內容。 若要完成此動作，請將名為 `RoleNameLabel` 的標籤 Web 控制項新增至 `ItemTemplate`，並將其 `Text` 屬性系結至 `Container.DataItem`。

這些屬性和 `ItemTemplate`的內容可以用宣告方式或透過 GridView 的 [欄位] 對話方塊和 [編輯範本] 介面來設定。 若要到達 [欄位] 對話方塊，請按一下 GridView 智慧標籤中的 [編輯資料行] 連結。 接下來，取消核取 [自動產生欄位] 核取方塊，將 `AutoGenerateColumns` 屬性設定為 [False]，然後將 TemplateField 新增至 GridView，將其 [`HeaderText`] 屬性設定為 [角色]。 若要定義 `ItemTemplate`的內容，請從 GridView 的智慧標籤中選擇 [編輯範本] 選項。 將 [標籤] Web 控制項拖曳至 [`ItemTemplate`]，將其 [`ID`] 屬性設為 [`RoleNameLabel`]，並設定其資料系結設定，使其 `Text` 屬性系結至 `Container.DataItem`。

無論您使用何種方法，GridView 產生的宣告式標記在完成時看起來應該如下所示。

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample10.aspx)]

> [!NOTE]
> 陣列的內容會使用資料系結語法 `<%# Container.DataItem %>`來顯示。 有關在顯示系結至 GridView 的陣列內容時，為何使用此語法的詳細說明，已超出本教學課程的範圍。 如需有關此問題的詳細資訊，請參閱將純量陣列系結[至資料 Web 控制項](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)。

目前，`RoleList` GridView 只會在第一次造訪網頁時系結至角色清單。 每當新增新角色時，就需要重新整理方格。 若要完成此動作，請更新 `CreateRoleButton` 按鈕的 `Click` 事件處理常式，以便在建立新角色時呼叫 `DisplayRolesInGrid` 方法。

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample11.cs)]

現在當使用者新增新角色時，`RoleList` GridView 會在回傳時顯示剛新增的角色，並提供已成功建立角色的視覺化回饋。 為了說明這一點，請造訪瀏覽器中的 [`ManageRoles.aspx`] 頁面，並新增名為 [主管] 的角色。 當您按一下 [建立角色] 按鈕時，回傳將會控制發生，且方格會更新為包含系統管理員以及新角色 [主管]。

[已新增 ![監督員角色](creating-and-managing-roles-cs/_static/image17.png)](creating-and-managing-roles-cs/_static/image16.png)

**圖 6**：已新增監督員角色（[按一下以觀看完整大小的影像](creating-and-managing-roles-cs/_static/image18.png)）

## <a name="step-6-deleting-roles"></a>步驟6：刪除角色

此時，使用者可以建立新的角色，並從 [`ManageRoles.aspx`] 頁面中查看所有現有的角色。 讓我們允許使用者也刪除角色。 `Roles.DeleteRole` 的方法有兩個多載：

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) -*刪除角色擁有*端。 如果角色包含一或多個成員，則會擲回例外狀況。
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) -*刪除角色擁有*端。 如果 `true`*throwOnPopulateRole* ，則如果角色包含一或多個成員，就會擲回例外狀況。 如果 `false`*throwOnPopulateRole* ，則會刪除角色，不論其是否包含任何成員。 就內部而言，`DeleteRole(roleName)` 方法會呼叫 `DeleteRole(roleName, true)`。

如果使用*的是 `null`* 或空字串，或如果使用*中包含逗號*，則 `DeleteRole` 方法也會擲回例外狀況。 如果*系統中沒有該*等位，`DeleteRole` 會無訊息地失敗，而不會引發例外狀況。

讓我們將 `ManageRoles.aspx` 中的 GridView 擴大為包含 [刪除] 按鈕，當您按一下時，就會刪除選取的角色。 首先，前往 [欄位] 對話方塊並新增 [刪除] 按鈕（位於 [CommandField] 選項底下），將 [刪除] 按鈕新增至 GridView。 將 [刪除] 按鈕設為最左邊的資料行，並將其 `DeleteText` 屬性設定為 [刪除角色]。

[![將 [刪除] 按鈕新增至 Rolelist& roles GridView](creating-and-managing-roles-cs/_static/image20.png)](creating-and-managing-roles-cs/_static/image19.png)

**圖 7**：將 [刪除] 按鈕新增至 `RoleList` GridView （[按一下以查看完整大小的影像](creating-and-managing-roles-cs/_static/image21.png)）

加入 [刪除] 按鈕之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample12.aspx)]

接下來，為 GridView 的 `RowDeleting` 事件建立事件處理常式。 這是按一下 [刪除角色] 按鈕時，在回傳時引發的事件。 將下列程式碼加入事件處理常式。

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample13.cs)]

程式碼一開始會以程式設計方式，參考已按下 [刪除角色] 按鈕的資料列中的 `RoleNameLabel` Web 控制項。 接著會叫用 `Roles.DeleteRole` 方法，傳入 `RoleNameLabel` 和 `false`的 `Text`，藉此刪除角色，而不論是否有任何使用者與角色相關聯。 最後，`RoleList` GridView 會重新整理，使剛刪除的角色不會再出現在方格中。

> [!NOTE]
> 在刪除角色之前，[刪除角色] 按鈕不需要使用者進行任何確認。 確認動作最簡單的方法之一，是透過用戶端確認對話方塊。 如需這項技術的詳細資訊，請參閱[在刪除時新增用戶端確認](https://asp.net/learn/data-access/tutorial-42-cs.aspx)。

## <a name="summary"></a>總結

許多 web 應用程式都有特定的授權規則或頁面層級功能，僅供特定的使用者類別使用。 例如，可能有一組只有系統管理員可以存取的網頁。 與其以使用者為基礎定義這些授權規則，通常會比根據角色定義規則更有説明。 也就是說，不是明確允許 Scott 和 Jisun 存取系統管理網頁，而是允許系統管理員角色的成員存取這些頁面，然後代表 Scott 和 Jisun，因為使用者屬於系統管理員角色。

角色架構可讓您輕鬆地建立及管理角色。 在本教學課程中，我們已檢查如何設定 Roles 架構，以使用 `SqlRoleProvider`，其使用 Microsoft SQL Server 資料庫做為角色存放區。 我們也建立了一個網頁，其中列出系統中的現有角色，並允許建立新的角色並刪除現有的角色。 在後續的教學課程中，我們將瞭解如何將使用者指派給角色，以及如何套用以角色為基礎的授權。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [檢查 ASP.NET 2.0 的成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何：在 ASP.NET 2.0 中使用角色管理員](https://msdn.microsoft.com/library/ms998314.aspx)
- [角色提供者](https://msdn.microsoft.com/library/aa478950.aspx)
- [推出您自己的網站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [`<roleManager>` 元素的技術檔](https://msdn.microsoft.com/library/ms164660.aspx)
- [使用成員資格和角色管理員 Api](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者包括 Alicja Maziarz、Suchi Banerjee 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [下一步](assigning-roles-to-users-cs.md)
