---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
title: 將角色指派給使用者C#（） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將建立兩個 ASP.NET 網頁，協助管理哪些使用者屬於哪些角色。 第一頁將包含可查看目標的設備 。
ms.author: riande
ms.date: 03/24/2008
ms.assetid: d522639a-5aca-421e-9a76-d73f95607f57
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
msc.type: authoredcontent
ms.openlocfilehash: 3346e47cf604ed1d4003ca83203116666e37cb1b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633731"
---
# <a name="assigning-roles-to-users-c"></a>將角色指派給使用者 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.10.zip)或[下載 PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_cs.pdf)

> 在本教學課程中，我們將建立兩個 ASP.NET 網頁，協助管理哪些使用者屬於哪些角色。 第一頁將包含一些設備，可查看哪些使用者屬於指定的角色、特定使用者所屬的角色，以及從特定角色指派或移除特定使用者的能力。 在第二頁中，我們將擴充 CreateUserWizard 控制項，使其包含一個步驟來指定新建立之使用者所屬的角色。 這在系統管理員能夠建立新使用者帳戶的情況下很有用。

## <a name="introduction"></a>簡介

<a id="_msoanchor_1"> </a>[上一個教學](creating-and-managing-roles-cs.md)課程已檢查過角色架構和 `SqlRoleProvider`;我們已瞭解如何使用 `Roles` 類別來建立、取得和刪除角色。 除了建立和刪除角色之外，我們還必須能夠從角色指派或移除使用者。 可惜的是，ASP.NET 不會隨附任何 Web 控制項，以管理哪些使用者屬於哪些角色。 相反地，我們必須建立自己的 ASP.NET 網頁來管理這些關聯。 好消息是，對角色新增和移除使用者相當簡單。 `Roles` 類別包含幾個方法，可將一或多個使用者新增至一或多個角色。

在本教學課程中，我們將建立兩個 ASP.NET 網頁，協助管理哪些使用者屬於哪些角色。 第一頁將包含一些設備，可查看哪些使用者屬於指定的角色、特定使用者所屬的角色，以及從特定角色指派或移除特定使用者的能力。 在第二頁中，我們將擴充 CreateUserWizard 控制項，使其包含一個步驟來指定新建立之使用者所屬的角色。 這在系統管理員能夠建立新使用者帳戶的情況下很有用。

讓我們開始吧！

## <a name="listing-what-users-belong-to-what-roles"></a>列出哪些使用者屬於哪些角色

本教學課程的第一個商務順序是建立可將使用者指派給角色的網頁。 在我們考慮如何將使用者指派給角色之前，讓我們先專注于如何判斷哪些使用者屬於哪些角色。 有兩種方式可以顯示此資訊：「依角色」或「依使用者」。 我們可以讓訪客選取角色，然後顯示屬於該角色的所有使用者（「依角色」顯示），或提示訪客選取使用者，然後顯示指派給該使用者的角色（「使用者」顯示）。

「角色」視圖在訪客想要知道屬於特定角色的使用者集合時很有用;當造訪者需要知道特定使用者的角色時，「使用者」視圖就很理想。 讓我們的頁面包含「依角色」和「依使用者」介面。

我們將從建立「使用者」介面開始。 此介面會由下拉式清單和核取方塊清單所組成。 下拉式清單將會填入系統中的使用者集合;核取方塊會列舉角色。 從下拉式清單中選取使用者，將會檢查使用者所屬的角色。 流覽頁面的人員可以核取或取消核取核取方塊，以從對應的角色新增或移除選取的使用者。

> [!NOTE]
> 使用下拉式清單列出使用者帳戶，對於可能有數百個使用者帳戶的網站來說，並不是理想的選擇。 下拉式清單的設計是讓使用者從相對較短的選項清單中挑選一個專案。 當清單專案的數目增加時，它很快就會變得很困難。 如果您要建立的網站可能會有大量的使用者帳戶，您可能會想要考慮使用替代的使用者介面，例如可分頁的 GridView 或可篩選的介面，其中列出的會提示造訪者選擇字母，然後顯示使用者名稱開頭為所選字母的使用者。

## <a name="step-1-building-the-by-user-user-interface"></a>步驟1：建立「使用者」使用者介面

開啟 [`UsersAndRoles.aspx`] 頁面。 在頁面頂端，新增名為 `ActionStatus` 的標籤 Web 控制項，並清除其 [`Text`] 屬性。 我們將使用此標籤來提供有關所執行動作的意見反應、顯示如下的訊息：「使用者 Tito 已新增至系統管理員角色」或「使用者 Jisun 已從主管角色移除」。 為了讓這些訊息脫穎而出，請將標籤的 `CssClass` 屬性設定為「重要」。

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample1.aspx)]

接下來，將下列 CSS 類別定義新增至 `Styles.css` 樣式表單：

[!code-css[Main](assigning-roles-to-users-cs/samples/sample2.css)]

此 CSS 定義會指示瀏覽器使用較大的紅色字型來顯示標籤。 [圖 1] 透過 Visual Studio 設計工具來顯示這種效果。

[![標籤的 CssClass 屬性會產生較大的紅色字型](assigning-roles-to-users-cs/_static/image2.png)](assigning-roles-to-users-cs/_static/image1.png)

**圖 1**：標籤的 `CssClass` 屬性會產生較大的紅色字型（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image3.png)）

接下來，將 DropDownList 新增至頁面，將其 `ID` 屬性設為 `UserList`，並將其 `AutoPostBack` 屬性設定為 True。 我們將使用此 DropDownList 來列出系統中的所有使用者。 這個 DropDownList 會系結至 MembershipUser 物件的集合。 因為我們希望 DropDownList 顯示 MembershipUser 物件的 UserName 屬性（並使用它做為清單專案的值），所以請將 DropDownList 的 `DataTextField` 和 `DataValueField` 屬性設定為 "UserName"。

在 DropDownList 底下，新增名為 `UsersRoleList`的中繼器。 此中繼器會將系統中的所有角色列為一系列的核取方塊。 使用下列宣告式標記來定義中繼器的 `ItemTemplate`：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample3.aspx)]

`ItemTemplate` 標記包含名為 `RoleCheckBox`的單一核取方塊 Web 控制項。 核取方塊的 `AutoPostBack` 屬性會設定為 True，且 `Text` 屬性會系結至 `Container.DataItem`。 資料系結語法只是 `Container.DataItem` 是因為角色架構會以字串陣列的形式傳回角色名稱的清單，而這是我們將系結至中繼器的字串陣列。 關於為何使用此語法來顯示系結至資料 Web 控制項之陣列內容的詳細說明，已超出本教學課程的範圍。 如需有關此問題的詳細資訊，請參閱將純量陣列系結[至資料 Web 控制項](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)。

此時，「使用者」介面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample4.aspx)]

我們現在已準備好撰寫程式碼，將一組使用者帳戶系結至 DropDownList，並將一組角色系結至中繼器。 在頁面的程式碼後置類別中，使用下列程式碼新增名為 `BindUsersToUserList` 的方法，以及另一個名為 `BindRolesList`：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample5.cs)]

`BindUsersToUserList` 方法會透過[`Membership.GetAllUsers` 方法](https://msdn.microsoft.com/library/dy8swhya.aspx)，抓取系統中的所有使用者帳戶。 這會傳回[`MembershipUserCollection` 物件](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)，這是[`MembershipUser` 實例](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)的集合。 此集合接著會系結至 `UserList` DropDownList。 組成集合的 `MembershipUser` 實例包含各種不同的屬性，例如 `UserName`、`Email`、`CreationDate`和 `IsOnline`。 為了指示 DropDownList 顯示 `UserName` 屬性的值，請確定 `UserList` DropDownList 的 `DataTextField` 和 `DataValueField` 屬性已設定為 "UserName"。

> [!NOTE]
> `Membership.GetAllUsers` 方法有兩個多載：一個不接受任何輸入參數，而且會傳回所有使用者，另一個則會接受頁面索引和頁面大小的整數值，並只傳回指定的使用者子集。 當可分頁的使用者介面專案中顯示大量的使用者帳戶時，第二個多載可以用來更有效率地流覽使用者，因為它只會傳回使用者帳戶的精確子集，而不是全部。

`BindRolesToList` 方法一開始會呼叫 `Roles` 類別的[`GetAllRoles` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)，它會傳回包含系統中角色的字串陣列。 這個字串陣列接著會系結至中繼器。

最後，我們需要在第一次載入頁面時呼叫這兩種方法。 將下列程式碼加入至 `Page_Load` 事件處理常式：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample6.cs)]

當此程式碼準備好之後，請花一點時間透過瀏覽器造訪頁面;您的畫面看起來應該像 [圖 2]。 系統會在下拉式清單中填入所有使用者帳戶，而在該情況下，每個角色會顯示為一個核取方塊。 由於我們將 DropDownList 的 `AutoPostBack` 屬性和核取方塊設定為 True，因此變更所選使用者或檢查或取消選取角色會導致回傳。 不過，因為我們尚未撰寫程式碼來處理這些動作，所以不會執行任何動作。 我們將在接下來的兩節中解決這些工作。

[![頁面會顯示使用者和角色](assigning-roles-to-users-cs/_static/image5.png)](assigning-roles-to-users-cs/_static/image4.png)

**圖 2**：頁面會顯示使用者和角色（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image6.png)）

### <a name="checking-the-roles-the-selected-user-belongs-to"></a>檢查選取的使用者所屬的角色

第一次載入頁面時，或每當訪客從下拉式清單中選取新的使用者時，我們需要更新 `UsersRoleList`的核取方塊，如此一來，只有在選取的使用者屬於該角色時，才會檢查指定的角色核取方塊。 若要完成此動作，請使用下列程式碼建立名為 `CheckRolesForSelectedUser` 的方法：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample7.cs)]

上述程式碼一開始會先決定所選取的使用者是誰。 然後，它會使用 Roles 類別的[`GetRolesForUser(userName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)，將指定的使用者角色集當做字串陣列傳回。 接下來，系統會列舉中繼器的專案，並以程式設計方式參考每個專案的 `RoleCheckBox` 核取方塊。 只有當對應的角色包含在 `selectedUsersRoles` 字串陣列內時，才會檢查此核取方塊。

> [!NOTE]
> 如果您使用 ASP.NET 2.0 版，則不會編譯 `selectedUserRoles.Contains<string>(...)` 語法。 `Contains<string>` 方法是[LINQ 程式庫](http://en.wikipedia.org/wiki/Language_Integrated_Query)的一部分，這是 ASP.NET 3.5 的新手。 如果您仍在使用 ASP.NET 版本2.0，請改用[`Array.IndexOf<string>` 方法](https://msdn.microsoft.com/library/eha9t187.aspx)。

在兩種情況下，必須呼叫 `CheckRolesForSelectedUser` 方法：第一次載入頁面時，以及每次變更 `UserList` DropDownList 的選取索引時。 因此，請從 `Page_Load` 事件處理常式呼叫這個方法（在呼叫 `BindUsersToUserList` 和 `BindRolesToList`之後）。 此外，建立 DropDownList `SelectedIndexChanged` 事件的事件處理常式，並從該處呼叫此方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample8.cs)]

將此程式碼備妥之後，您就可以透過瀏覽器來測試頁面。 不過，由於 [`UsersAndRoles.aspx`] 頁面目前缺乏將使用者指派給角色的能力，因此沒有任何使用者擁有角色。 我們會建立介面，以便將使用者指派給角色一段時間，讓您可以將此程式碼設為正常運作，並確認它會在稍後執行，或者您可以藉由將記錄插入 `aspnet_UsersInRoles` 資料表來手動將使用者新增至角色，以便立即測試此功能。

### <a name="assigning-and-removing-users-from-roles"></a>從角色指派和移除使用者

當訪客在 `UsersRoleList` 中繼器中檢查或取消核取核取方塊時，我們需要從對應的角色新增或移除選取的使用者。 核取方塊的 `AutoPostBack` 屬性目前設定為 True，這會在每次有重複項的核取方塊被勾選或取消選取時，導致回傳。 簡言之，我們必須為 CheckBox 的 `CheckChanged` 事件建立事件處理常式。 因為此核取方塊是在重複項控制項中，所以我們需要手動新增事件處理常式的管道。 首先，將事件處理常式加入至程式碼後置類別做為 `protected` 方法，如下所示：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample9.cs)]

我們稍後會回到撰寫這個事件處理常式的程式碼。 但先讓我們完成事件處理的管道。 從中繼器 `ItemTemplate`的核取方塊中，新增 `OnCheckedChanged="RoleCheckBox_CheckChanged"`。 此語法會將 `RoleCheckBox_CheckChanged` 事件處理常式線路到 `RoleCheckBox`的 `CheckedChanged` 事件。

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample10.aspx)]

我們的最後一項工作是完成 `RoleCheckBox_CheckChanged` 事件處理常式。 我們必須先參考引發事件的 CheckBox 控制項，因為這個 CheckBox 實例會告訴我們哪些角色是透過其 `Text` 和 `Checked` 屬性來檢查或取消核取。 使用此資訊以及所選使用者的使用者名稱，我們會透過 `Roles` 類別的[`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)或[`RemoveUserFromRole` 方法](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)，從角色新增或移除使用者。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample11.cs)]

上述程式碼一開始會以程式設計方式參考引發事件的核取方塊，這可透過 `sender` 輸入參數來取得。 如果勾選此核取方塊，則會將選取的使用者新增至指定的角色，否則會從角色中移除。 不論是哪一種情況，`ActionStatus` 標籤都會顯示一則訊息，摘要說明剛剛執行的動作。

請花點時間透過瀏覽器測試此頁面。 選取 [使用者 Tito]，然後將 Tito 新增至 [系統管理員] 和 [主管] 角色。

[![Tito 已新增至系統管理員和主管角色](assigning-roles-to-users-cs/_static/image8.png)](assigning-roles-to-users-cs/_static/image7.png)

**圖 3**： Tito 已新增至 [系統管理員] 和 [主管] 角色（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image9.png)）

接下來，從下拉式清單中選取 [使用者 Bruce]。 有一個回傳，而中繼器的核取方塊則會透過 `CheckRolesForSelectedUser`更新。 由於 Bruce 尚未屬於任何角色，因此會取消選取這兩個核取方塊。 接下來，將 Bruce 新增至 [主管] 角色。

[已將 ![Bruce 新增至主管角色](assigning-roles-to-users-cs/_static/image11.png)](assigning-roles-to-users-cs/_static/image10.png)

**圖 4**： Bruce 已新增至 [主管] 角色（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image12.png)）

若要進一步確認 `CheckRolesForSelectedUser` 方法的功能，請選取 Tito 或 Bruce 以外的使用者。 請注意核取方塊如何自動取消選取，表示它們不屬於任何角色。 返回 Tito。 應該檢查 [系統管理員] 和 [監督員] 核取方塊。

## <a name="step-2-building-the-by-roles-user-interface"></a>步驟2：建立「角色」使用者介面

此時，我們已完成「使用者」介面，並準備好開始處理「角色」介面。 「依據角色」介面會提示使用者從下拉式清單中選取角色，然後在 GridView 中顯示屬於該角色的使用者集合。

將另一個 DropDownList 控制項新增至 [`UsersAndRoles.aspx`] 頁面。 將此值放在重複項控制項的下方，將其命名為 `RoleList`，並將其 `AutoPostBack` 屬性設定為 True。 在該底下，新增 GridView 並將其命名為 `RolesUserList`。 這個 GridView 會列出屬於所選角色的使用者。 將 GridView 的 `AutoGenerateColumns` 屬性設定為 False，將 TemplateField 新增至方格的 `Columns` 集合，並將其 `HeaderText` 屬性設定為 "Users"。 定義 TemplateField 的 `ItemTemplate`，讓它在名為 `UserNameLabel`之標籤的 `Text` 屬性中顯示資料系結運算式 `Container.DataItem` 的值。

加入和設定 GridView 之後，您的「依角色」介面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample12.aspx)]

我們需要使用系統中的一組角色來填入 `RoleList` DropDownList。 若要完成這項操作，請更新 `BindRolesToList` 方法，以便將 `Roles.GetAllRoles` 方法所傳回的字串陣列系結至 `RolesList` DropDownList （以及 `UsersRoleList` 中繼器）。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample13.cs)]

已加入 `BindRolesToList` 方法中的最後兩行，將角色集系結至 `RoleList` 的 DropDownList 控制項。 [圖 5] 顯示透過瀏覽器查看的最終結果–以系統角色填入的下拉式清單。

[![角色會顯示在 Rolelist& roles DropDownList](assigning-roles-to-users-cs/_static/image14.png)](assigning-roles-to-users-cs/_static/image13.png)

**圖 5**：角色會顯示在 [`RoleList`] DropDownList 中（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image15.png)）

### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>顯示屬於所選角色的使用者

第一次載入頁面時，或從 [`RoleList` DropDownList] 選取了新角色時，我們必須在 GridView 中顯示屬於該角色的使用者清單。 使用下列程式碼，建立名為 `DisplayUsersBelongingToRole` 的方法：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample14.cs)]

這個方法一開始會從 `RoleList` DropDownList 取得選取的角色。 然後，它會使用[`Roles.GetUsersInRole(roleName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)來抓取屬於該角色的使用者之使用者名稱的字串陣列。 然後，此陣列會系結至 `RolesUserList` GridView。

在兩種情況下，必須呼叫這個方法：一開始載入頁面，以及 `RoleList` DropDownList 中選取的角色何時變更。 因此，請更新 `Page_Load` 事件處理常式，以便在呼叫 `CheckRolesForSelectedUser`之後叫用這個方法。 接下來，建立 `RoleList`的 `SelectedIndexChanged` 事件的事件處理常式，並從該處呼叫此方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample15.cs)]

當此程式碼準備就緒時，`RolesUserList` GridView 應該會顯示屬於所選角色的使用者。 如 [圖 6] 所示，「主管」角色是由兩個成員所組成： Bruce 和 Tito。

[![GridView 會列出屬於所選角色的使用者](assigning-roles-to-users-cs/_static/image17.png)](assigning-roles-to-users-cs/_static/image16.png)

**圖 6**： GridView 會列出屬於所選角色的使用者（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image18.png)）

### <a name="removing-users-from-the-selected-role"></a>從選取的角色移除使用者

讓我們擴大 `RolesUserList` GridView，使其包含 [移除] 按鈕的資料行。 按一下特定使用者的 [移除] 按鈕，將會從該角色中移除。

首先，將 [刪除] 按鈕欄位加入至 GridView。 使此欄位顯示為最左邊的內容，並將其 `DeleteText` 屬性從 [刪除] （預設值）變更為 [移除]。

[![新增](assigning-roles-to-users-cs/_static/image20.png)](assigning-roles-to-users-cs/_static/image19.png)

**圖 7**：將 [移除] 按鈕新增至 GridView （[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image21.png)）

當按一下 [移除] 按鈕時，回傳接踵而來會引發 GridView 的 `RowDeleting` 事件。 我們需要為這個事件建立事件處理常式，並撰寫程式碼，從選取的角色中移除使用者。 建立事件處理常式，然後新增下列程式碼：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample16.cs)]

程式碼一開始會先決定所選的角色名稱。 然後，它會以程式設計方式從已按下 [移除] 按鈕的資料列中參考 `UserNameLabel` 控制項，以決定要移除之使用者的使用者名稱。 然後會透過呼叫 `Roles.RemoveUserFromRole` 方法，將使用者從角色中移除。 接著會重新整理 `RolesUserList` GridView，並透過 [`ActionStatus` Label] 控制項顯示訊息。

> [!NOTE]
> 從角色移除使用者之前，[移除] 按鈕不需要使用者進行任何確認。 我邀請您新增某種層級的使用者確認。 確認動作最簡單的方法之一，是透過用戶端確認對話方塊。 如需這項技術的詳細資訊，請參閱[在刪除時新增用戶端確認](https://asp.net/learn/data-access/tutorial-42-cs.aspx)。

[圖 8] 顯示從 [監督員] 群組中移除使用者 Tito 之後的頁面。

[![很遺憾，Tito 不再是監督員](assigning-roles-to-users-cs/_static/image23.png)](assigning-roles-to-users-cs/_static/image22.png)

**圖 8**：很遺憾，Tito 不再是監督員（[按一下以觀看完整大小的影像](assigning-roles-to-users-cs/_static/image24.png)）

### <a name="adding-new-users-to-the-selected-role"></a>將新使用者新增至選取的角色

除了從選取的角色中移除使用者，此頁面的造訪者也應該能夠將使用者新增至選取的角色。 將使用者新增至所選角色的最佳介面，取決於您預期擁有的使用者帳戶數目。 如果您的網站只會存放數十個使用者帳戶，您可以在這裡使用 DropDownList。 如果可能有數千個使用者帳戶，您可以加入使用者介面，讓訪客可以逐頁流覽帳戶、搜尋特定帳戶，或以其他方式篩選使用者帳戶。

在此頁面中，讓我們使用非常簡單的介面，不論系統中的使用者帳戶數目為何。 也就是，我們將使用 TextBox，提示訪客輸入想要新增至所選角色的使用者名稱。 如果沒有具有該名稱的使用者存在，或使用者已是該角色的成員，則會在 `ActionStatus` 標籤中顯示訊息。 但是，如果使用者存在且不是該角色的成員，我們會將其新增至角色並重新整理方格。

在 GridView 底下新增文字方塊和按鈕。 將 TextBox 的 `ID` 設定為 [`UserNameToAddToRole`]，並將按鈕的 `ID` 和 `Text` 屬性分別設定為 [`AddUserToRoleButton`] 和 [將使用者新增至角色]。

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample17.aspx)]

接下來，建立 `AddUserToRoleButton` 的 `Click` 事件處理常式，並新增下列程式碼：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample18.cs)]

`Click` 事件處理常式中的大部分程式碼都會執行各種驗證檢查。 它可確保造訪者在 [`UserNameToAddToRole`] 文字方塊中提供了使用者名稱，該使用者存在於系統中，而且尚未屬於選取的角色。 如果其中任何一項檢查失敗，則會在 `ActionStatus` 中顯示適當的訊息，並結束事件處理常式。 如果所有檢查都通過，則會透過 `Roles.AddUserToRole` 方法將使用者新增至角色。 之後，TextBox 的 `Text` 屬性會被清除，GridView 會重新整理，而 `ActionStatus` 標籤會顯示一則訊息，指出指定的使用者已成功新增至選取的角色。

> [!NOTE]
> 為了確保指定的使用者還不屬於選取的角色，我們會使用[`Roles.IsUserInRole(userName, roleName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)，它會傳回布林值，指出*userName*是否為角色名稱*的成員。* 當我們查看以角色為基礎的<a id="_msoanchor_2"></a>授權時，我們會在[下一個教學](role-based-authorization-cs.md)課程中再次使用此方法。

透過瀏覽器造訪頁面，然後從 [`RoleList`] DropDownList 中選取 [主管] 角色。 請嘗試輸入不正確使用者名稱-您應該會看到一則訊息，說明系統中不存在該使用者。

[![您無法將不存在的使用者新增至角色](assigning-roles-to-users-cs/_static/image26.png)](assigning-roles-to-users-cs/_static/image25.png)

**圖 9**：您無法將不存在的使用者新增至角色（[按一下以觀看完整大小的影像](assigning-roles-to-users-cs/_static/image27.png)）

現在，請嘗試新增有效的使用者。 繼續進行，並將 Tito 重新加入至 [主管] 角色。

[![Tito 會再次成為監督員！](assigning-roles-to-users-cs/_static/image29.png)](assigning-roles-to-users-cs/_static/image28.png)

**圖 10**： Tito 再次成為監督員！  （[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image30.png)）

## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>步驟3：交叉更新「依使用者」和「依角色」介面

[`UsersAndRoles.aspx`] 頁面提供兩個不同的介面來管理使用者和角色。 目前，這兩個介面彼此獨立，因此在某個介面中所做的變更可能不會立即反映在另一個介面中。 例如，假設頁面的訪客從 [`RoleList`] DropDownList 中選取 [主管] 角色，其中會列出 Bruce 和 Tito 做為其成員。 接下來，訪客會從 `UserList` DropDownList 中選取 Tito，這會檢查 `UsersRoleList` 中繼器中的 [系統管理員] 和 [監督員] 核取方塊。 如果造訪者從中繼器取消核取 [監督員] 角色，Tito 就會從 [主管] 角色中移除，但此修改不會反映在 [依角色] 介面中。 GridView 仍然會將 Tito 顯示為主管角色的成員。

若要修正此問題，我們必須在每次從 `UsersRoleList` 中繼器中核取或取消選取角色時，重新整理 GridView。 同樣地，每當使用者從「角色」介面移除或新增至角色時，我們都需要重新整理中繼器。

「使用者」介面中的中繼器會藉由呼叫 `CheckRolesForSelectedUser` 方法來重新整理。 可以在 `RolesUserList` GridView 的 `RowDeleting` 事件處理常式和 `AddUserToRoleButton` 按鈕的 `Click` 事件處理常式中修改「依據角色」介面。 因此，我們需要從每個方法呼叫 `CheckRolesForSelectedUser` 方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample19.cs)]

同樣地，「依據角色」介面中的 GridView 會藉由呼叫 `DisplayUsersBelongingToRole` 方法來重新整理，而「使用者」介面則是透過 `RoleCheckBox_CheckChanged` 事件處理常式來修改。 因此，我們需要從這個事件處理常式呼叫 `DisplayUsersBelongingToRole` 方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample20.cs)]

隨著這些次要程式碼的變更，「依使用者」和「依角色」介面現在可以正確地交叉更新。 若要確認這一點，請造訪瀏覽器中的頁面，然後分別從 `UserList` 和 `RoleList` Dropdownlist 進行中選取 [Tito] 和 [主管]。 請注意，當您取消核取 [由使用者] 介面中的重複項 Tito 的 [監督員] 角色時，Tito 會自動從「依角色」介面中的 GridView 移除。 將 Tito 從「角色」介面新增回「主管」角色時，會自動重新檢查「使用者」介面中的 [監督員] 核取方塊。

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>步驟4：自訂 CreateUserWizard 以包含「指定角色」步驟

<a id="_msoanchor_3"></a>在[*建立使用者帳戶*](../membership/creating-user-accounts-cs.md)教學課程中，我們看到如何使用 CreateUserWizard Web 控制項提供介面來建立新的使用者帳戶。 CreateUserWizard 控制項可透過下列兩種方式之一來使用：

- 作為訪客在網站上建立自己的使用者帳戶的方法，以及
- 做為系統管理員建立新帳戶的方法

在第一個使用案例中，訪客會前往網站並填滿 CreateUserWizard，並輸入他們的資訊，以便在網站上註冊。 在第二個案例中，系統管理員會為另一個人建立新帳戶。

當系統管理員為某個其他人建立帳戶時，允許系統管理員指定新使用者帳戶所屬的角色可能會很有説明。 在<a id="_msoanchor_4"></a> [*儲存* *額外的使用者資訊*](../membership/storing-additional-user-information-cs.md)教學課程中，我們看到了如何藉由新增其他 `WizardSteps`來自訂 CreateUserWizard。 讓我們看一下如何將額外的步驟新增至 CreateUserWizard，以指定新使用者的角色。

開啟 [`CreateUserWizardWithRoles.aspx`] 頁面，並加入名為 `RegisterUserWithRoles`的 CreateUserWizard 控制項。 將控制項的 `ContinueDestinationPageUrl` 屬性設定為 "~/Default.aspx"。 因為這裡的概念是系統管理員將使用此 CreateUserWizard 控制項來建立新的使用者帳戶，請將控制項的 `LoginCreatedUser` 屬性設定為 False。 這個 `LoginCreatedUser` 屬性會指定訪客是否自動以剛建立的使用者身分登入，而且預設為 True。 我們會將它設定為 False，因為當系統管理員建立新帳戶時，我們想要讓他以自己的身分登入。

接下來，選取 [新增/移除 `WizardSteps`...]選項，從 CreateUserWizard 的智慧標籤，並加入新的 `WizardStep`，將其 `ID` 設定為 [`SpecifyRolesStep`]。 移動 `SpecifyRolesStep WizardStep`，使其位於「註冊新帳戶」步驟之後，但在「完成」步驟之前。 將 `WizardStep`的 `Title` 屬性設定為 [指定角色]、將其 `StepType` 屬性設為 [`Step`]，並將其 [`AllowReturn`] 屬性設定為 [False]。

[![新增](assigning-roles-to-users-cs/_static/image32.png)](assigning-roles-to-users-cs/_static/image31.png)

**圖 11**：將 [指定角色] `WizardStep` 新增至 CreateUserWizard （[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image33.png)）

這項變更之後，您的 CreateUserWizard 宣告式標記看起來應該如下所示：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample21.aspx)]

在 [指定角色] `WizardStep`中，新增名為 `RoleList`的 CheckBoxList。 此 CheckBoxList 會列出可用的角色，讓造訪頁面的人檢查新建立的使用者所屬的角色。

我們會保留兩個編碼工作：首先，我們必須以系統中的角色填入 `RoleList` CheckBoxList;第二，當使用者從 [指定角色] 步驟移至 [完成] 步驟時，我們需要將建立的使用者新增至選取的角色。 我們可以完成 `Page_Load` 事件處理常式中的第一個工作。 下列程式碼會以程式設計方式參考第一次造訪網頁的 `RoleList` 核取方塊，並將系統中的角色系結至該頁面。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample22.cs)]

上述程式碼看起來應該很熟悉。 在<a id="_msoanchor_5"></a> [*儲存* *額外的使用者資訊*](../membership/storing-additional-user-information-cs.md)教學課程中，我們使用了兩個 `FindControl` 語句，從自訂 `WizardStep`內參考 Web 控制項。 而將角色系結至 CheckBoxList 的程式碼則是在本教學課程中稍早所建立。

為了執行第二個程式設計工作，我們必須知道「指定角色」步驟何時完成。 回想一下，CreateUserWizard 有一個 `ActiveStepChanged` 事件，每次造訪者流覽至另一個步驟時，就會引發此事件。 我們可以在此判斷使用者是否已到達「完成」步驟;若是如此，我們必須將使用者新增至選取的角色。

建立 `ActiveStepChanged` 事件的事件處理常式，並新增下列程式碼：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample23.cs)]

如果使用者剛到達「已完成」步驟，則事件處理常式會列舉 `RoleList` CheckBoxList 的專案，而剛建立的使用者會被指派至選取的角色。

透過瀏覽器造訪此頁面。 CreateUserWizard 的第一個步驟是「註冊新帳戶」的標準步驟，它會提示您輸入新使用者的使用者名稱、密碼、電子郵件和其他重要資訊。 輸入資訊，以建立名為 Wanda 的新使用者。

[![建立名為 Wanda 的新使用者](assigning-roles-to-users-cs/_static/image35.png)](assigning-roles-to-users-cs/_static/image34.png)

**圖 12**：建立名為 Wanda 的新使用者（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image36.png)）

按一下 [建立使用者] 按鈕。 CreateUserWizard 會在內部呼叫 `Membership.CreateUser` 方法，建立新的使用者帳戶，然後再進行下一個步驟「指定角色」。 這裡列出系統角色。 勾選 [主管] 核取方塊，然後按 [下一步]。

[![使 Wanda 成為主管角色的成員](assigning-roles-to-users-cs/_static/image38.png)](assigning-roles-to-users-cs/_static/image37.png)

**圖 13**：讓 Wanda 成為主管角色的成員（[按一下以查看完整大小的影像](assigning-roles-to-users-cs/_static/image39.png)）

按一下 [下一步] 會導致回傳，並將 `ActiveStep` 更新為「完成」步驟。 在 `ActiveStepChanged` 事件處理常式中，最近建立的使用者帳戶會指派給 [主管] 角色。 若要確認這一點，請回到 [`UsersAndRoles.aspx`] 頁面，然後從 [`RoleList`] DropDownList 選取 [主管]。 如 [圖 14] 所示，現在主管是由三個使用者所組成： Bruce、Tito 和 Wanda。

[![Bruce、Tito 和 Wanda 都是主管](assigning-roles-to-users-cs/_static/image41.png)](assigning-roles-to-users-cs/_static/image40.png)

**圖 14**： Bruce、Tito 和 Wanda 全都是主管（[按一下以觀看完整大小的影像](assigning-roles-to-users-cs/_static/image42.png)）

## <a name="summary"></a>總結

Roles 架構提供方法，可供您用來抓取特定使用者角色的相關資訊，以及用來判斷哪些使用者屬於指定角色的方法。 此外，有許多方法可將一或多個使用者新增至一或多個角色。 在本教學課程中，我們只著重于其中兩種方法： `AddUserToRole` 和 `RemoveUserFromRole`。 還有一些其他的變化，其設計是將多個使用者新增至單一角色，並將多個角色指派給單一使用者。

本教學課程也包含擴充 CreateUserWizard 控制項的說明，以包含指定新建立之使用者角色的 `WizardStep`。 這種步驟可以協助系統管理員簡化為新使用者建立使用者帳戶的程式。

此時，我們已瞭解如何建立和刪除角色，以及如何從角色新增和移除使用者。 但我們尚未探討如何套用以角色為基礎的授權。 <a id="_msoanchor_6"></a>在[下列教學](role-based-authorization-cs.md)課程中，我們將探討如何以角色為基礎來定義 URL 授權規則，以及如何根據目前登入的使用者角色來限制頁面層級功能。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 網站管理工具總覽](https://msdn.microsoft.com/library/ms228053.aspx)
- [檢查 ASP。NET 的成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [推出您自己的網站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](creating-and-managing-roles-cs.md)
> [下一頁](role-based-authorization-cs.md)
