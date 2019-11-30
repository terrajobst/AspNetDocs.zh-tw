---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-cs
title: 建立介面以從許多（C#）選取一個使用者帳戶 |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將建立一個具有分頁、可篩選方格的使用者介面。 特別是，我們的使用者介面將由一系列的 LinkButtons for 。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 9e4e687c-b4ec-434f-a4ef-edb0b8f365e4
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-cs
msc.type: authoredcontent
ms.openlocfilehash: 8057cfbcd33c74376076363bc27940cebd522c08
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575809"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-c"></a>建置介面從許多個使用者帳戶中選取一個 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.12.zip)或[下載 PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_cs.pdf)

> 在本教學課程中，我們將建立一個具有分頁、可篩選方格的使用者介面。 特別是，我們的使用者介面會包含一系列的 LinkButtons，以便根據使用者名稱的起始字母來篩選結果，並使用 GridView 控制項來顯示相符的使用者。 我們一開始會列出 GridView 中的所有使用者帳戶。 然後，在步驟3中，我們將新增篩選 LinkButtons。 步驟4會查看篩選後的結果分頁。 在後續的教學課程中，將會使用在步驟2到4中所建立的介面，來執行特定使用者帳戶的系統管理工作。

## <a name="introduction"></a>簡介

在將<a id="_msoanchor_1"> </a>[*角色指派給使用者*](../roles/assigning-roles-to-users-cs.md)教學課程中，我們建立了基本介面，讓系統管理員選取使用者並管理她的角色。 具體而言，介面會向系統管理員顯示所有使用者的下拉式清單。 這類介面適用于有數十個或更多使用者帳戶的情況，但對具有數百或數千個帳戶的網站來說很困難。 針對具有大型使用者群的網站，分頁、可篩選的方格較適合使用者介面。

在本教學課程中，我們將建立這類使用者介面。 特別是，我們的使用者介面會包含一系列的 LinkButtons，以便根據使用者名稱的起始字母來篩選結果，並使用 GridView 控制項來顯示相符的使用者。 我們一開始會列出 GridView 中的所有使用者帳戶。 然後，在步驟3中，我們將新增篩選 LinkButtons。 步驟4會查看篩選後的結果分頁。 在後續的教學課程中，將會使用在步驟2到4中所建立的介面，來執行特定使用者帳戶的系統管理工作。

讓我們開始吧！

## <a name="step-1-adding-new-aspnet-pages"></a>步驟1：加入新的 ASP.NET 網頁

在本教學課程和接下來的兩個課程中，我們將檢查各種系統管理相關的功能和功能。 我們將需要一系列的 ASP.NET 網頁，以執行整個教學課程中所探討的主題。 讓我們建立這些頁面並更新網站地圖。

首先，在名為 `Administration`的專案中建立新的資料夾。 接下來，在資料夾中新增兩個新的 ASP.NET 網頁，並將每個頁面與 `Site.master` 主版頁面連結。 將頁面命名為：

- `ManageUsers.aspx`
- `UserInformation.aspx`

此外，也請將兩個頁面新增至網站的根目錄： `ChangePassword.aspx` 和 `RecoverPassword.aspx`。

此時，這四個頁面都有兩個內容控制項，每個主版頁面的 ContentPlaceHolders 都有一個： `MainContent` 和 `LoginContent`。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample1.aspx)]

我們想要針對這些頁面的 `LoginContent` ContentPlaceHolder 顯示主版頁面的預設標記。 因此，請移除 `Content2` 內容控制項的宣告式標記。 這麼做之後，頁面的標記應該只包含一個內容控制項。

[`Administration`] 資料夾中的 [ASP.NET] 頁面僅適用于系統管理使用者。 在<a id="_msoanchor_2"> </a>[*建立和管理角色*](../roles/creating-and-managing-roles-cs.md)教學課程中，我們已將系統管理員角色新增至系統;將這兩個頁面的存取許可權制為此角色。 若要完成這項操作，請將 `Web.config` 檔案新增至 `Administration` 資料夾，並設定其 `<authorization>` 元素以授與系統管理員角色的使用者，並拒絕所有其他人。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample2.xml)]

此時，專案的方案總管看起來應該像 [圖 1] 所示的螢幕擷取畫面。

[![四個新頁面，而且 Web.config 檔案已新增至網站](building-an-interface-to-select-one-user-account-from-many-cs/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image1.png)

**圖 1**：有四個新頁面和一個 `Web.config` 檔案已新增至網站（[按一下以觀看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image3.png)）

最後，將網站地圖（`Web.sitemap`）更新為包含 [`ManageUsers.aspx`] 頁面的專案。 在我們為角色教學課程新增的 `<siteMapNode>` 之後，新增下列 XML。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample3.xml)]

更新網站地圖之後，請透過瀏覽器造訪網站。 如 [圖 2] 所示，左邊的導覽現在包含了管理教學課程的專案。

[![網站地圖包含標題為 [使用者管理] 的節點](building-an-interface-to-select-one-user-account-from-many-cs/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image4.png)

**圖 2**：網站地圖包含標題為 [使用者管理] 的節點（[按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image6.png)）

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>步驟2：列出 GridView 中的所有使用者帳戶

本教學課程的最終目標是要建立一個分頁的可篩選方格，讓系統管理員可以從中選取要管理的使用者帳戶。 讓我們從列出 GridView 中的*所有*使用者開始。 完成後，我們會新增篩選和分頁介面和功能。

開啟 [`Administration`] 資料夾中的 [`ManageUsers.aspx`] 頁面，並加入 GridView，將其 `ID` 設定為 [`UserAccounts`]。 我們稍後會撰寫程式碼，使用 `Membership` 類別的 `GetAllUsers` 方法，將使用者帳戶集合系結至 GridView。 如先前的教學課程中所述，GetAllUsers 方法會傳回 `MembershipUserCollection` 物件，這是 `MembershipUser` 物件的集合。 集合中的每個 `MembershipUser` 都包含如 `UserName`、`Email`、`IsApproved`等屬性。

若要在 GridView 中顯示所需的使用者帳戶資訊，請將 GridView 的 `AutoGenerateColumns` 屬性設定為 False，並針對 `IsApproved`、`IsLockedOut`和 `IsOnline` 屬性的 `UserName`、`Email`和 `Comment` 屬性和 CheckBoxFields 加入 BoundFields。 此設定可透過控制項的宣告式標記或 [欄位] 對話方塊來套用。 [圖 3] 顯示 [自動產生欄位] 核取方塊已取消選取，且已新增並設定 BoundFields 和 CheckBoxFields 之後，[欄位] 對話方塊的螢幕擷取畫面。

[![在 GridView 中新增三個 BoundFields 和三個 CheckBoxFields](building-an-interface-to-select-one-user-account-from-many-cs/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image7.png)

**圖 3**：將三個 BoundFields 和三個 CheckBoxFields 加入 GridView （[按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image9.png)）

設定 GridView 之後，請確定其宣告式標記類似如下：

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample4.aspx)]

接下來，我們需要撰寫程式碼，將使用者帳戶系結至 GridView。 建立名為 `BindUserAccounts` 的方法來執行這項工作，然後從第一頁上的 `Page_Load` 事件處理常式中呼叫它，造訪。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample5.cs)]

請花點時間透過瀏覽器來測試頁面。 如 [圖 4] 所示，`UserAccounts` GridView 會列出系統中所有使用者的使用者名稱、電子郵件地址和其他相關的帳戶資訊。

[![使用者帳戶會列在 GridView 中](building-an-interface-to-select-one-user-account-from-many-cs/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image10.png)

**圖 4**：使用者帳戶會列在 GridView 中（[按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image12.png)）

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>步驟3：依使用者名稱的第一個字母篩選結果

`UserAccounts` GridView 目前會顯示*所有*的使用者帳戶。 針對具有數百或數千個使用者帳戶的網站，使用者必須能夠快速地向下削減所顯示的帳戶。 這可以藉由將篩選 LinkButtons 新增至頁面來完成。 讓我們將 27 LinkButtons 新增至頁面：一個標題為 All，而每個字母都有一個 LinkButton。 如果造訪者按一下 [所有 LinkButton]，GridView 就會顯示所有使用者。 如果他們按一下特定的字母，則只會顯示使用者名稱開頭為所選字母的使用者。

我們的第一項工作是新增27個 LinkButton 控制項。 其中一個選項是以宣告的方式建立 27 LinkButtons，一次一個。 更有彈性的方法是使用具有轉譯 LinkButton 之 `ItemTemplate` 的重複項控制項，然後將篩選選項系結至中繼器，做為 `string` 陣列。

首先，將 [中繼器] 控制項新增至 `UserAccounts` GridView 上方的頁面。 將中繼器的 `ID` 屬性設定為 [`FilteringUI`]。 設定中繼器的範本，使其 `ItemTemplate` 呈現 `Text` 和 `CommandName` 屬性系結至目前陣列元素的 LinkButton。 如我們在將<a id="_msoanchor_3"> </a>[*角色指派給使用者*](../roles/assigning-roles-to-users-cs.md)教學課程中所見，您可以使用 `Container.DataItem` 資料系結語法來完成這項作業。 使用中繼器的 `SeparatorTemplate` 在每個連結之間顯示一條垂直線。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample6.aspx)]

若要使用所需的篩選選項填入此中繼器，請建立名為 `BindFilteringUI`的方法。 請務必在第一次載入頁面時，從 `Page_Load` 事件處理常式中呼叫這個方法。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample7.cs)]

這個方法會將篩選選項指定為 `string` 陣列 `filterOptions`中的元素。 針對陣列中的每個元素，中繼器會轉譯 `Text` LinkButton，並將 `CommandName` 屬性指派給陣列元素的值。

[圖 5] 顯示透過瀏覽器觀看時的 `ManageUsers.aspx` 頁面。

[![中繼器清單27篩選 LinkButtons](building-an-interface-to-select-one-user-account-from-many-cs/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image13.png)

**圖 5**：重複項清單27篩選 LinkButtons （[按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image15.png)）

> [!NOTE]
> 使用者名稱的開頭可能是任何字元，包括數位和標點符號。 若要查看這些帳戶，系統管理員必須使用 [All LinkButton] 選項。 或者，您可以新增 LinkButton，以傳回以數位開頭的所有使用者帳戶。 我將此做為讀者的練習。

按一下任何篩選 LinkButtons 會導致回傳並引發重複項的 `ItemCommand` 事件，但方格中不會有任何變更，因為我們尚未撰寫任何程式碼來篩選結果。 `Membership` 類別所包含的[`FindUsersByName` 方法](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)，會傳回使用者名稱符合指定搜尋模式的使用者帳戶。 我們可以使用這個方法，只取出使用者帳戶，其使用者名稱是以所按下篩選 LinkButton 的 `CommandName` 所指定的字母為開頭。

一開始請先更新 `ManageUser.aspx` 頁面的程式碼後置類別，使其包含名為 `UsernameToMatch`的屬性。 這個屬性會在回傳期間保存使用者名稱篩選字串：

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample8.cs)]

`UsernameToMatch` 屬性會使用索引鍵 UsernameToMatch，將它指派給 `ViewState` 集合的值儲存。 當讀取這個屬性的值時，它會檢查 `ViewState` 集合中是否存在值;如果不是，則會傳回預設值，也就是空字串。 `UsernameToMatch` 屬性展現一般模式，也就是保存值來查看狀態，以便對屬性進行任何變更都會保存在回傳之間。 如需此模式的詳細資訊，請參閱[瞭解 ASP.NET View State](https://msdn.microsoft.com/library/ms972976.aspx)。

接下來，請更新 `BindUserAccounts` 方法，如此一來，就不會呼叫 `Membership.GetAllUsers`，而是會呼叫 `Membership.FindUsersByName`，傳入以 SQL 萬用字元字元（%）附加的 `UsernameToMatch` 屬性值。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample9.cs)]

若只要顯示使用者名稱的開頭是字母 A，請將 `UsernameToMatch` 屬性設定為，然後再呼叫 `BindUserAccounts`。 這會導致呼叫 `Membership.FindUsersByName("A%")`，這會傳回其使用者名稱開頭為的所有使用者。同樣地，若要傳回*所有*使用者，請將空字串指派給 `UsernameToMatch` 屬性，如此一來，`BindUserAccounts` 方法就會叫用 `Membership.FindUsersByName("%")`，藉此傳回所有使用者帳戶。

為中繼器的 `ItemCommand` 事件建立事件處理常式。 每當按一下其中一個篩選 LinkButtons 時，就會引發這個事件。系統會透過 `RepeaterCommandEventArgs` 物件，將按一下的 LinkButton `CommandName` 值傳遞給它。 我們需要將適當的值指派給 `UsernameToMatch` 屬性，然後呼叫 `BindUserAccounts` 方法。 如果 `CommandName` 是 All，請將空字串指派給 `UsernameToMatch`，以便顯示所有使用者帳戶。 否則，請將 `CommandName` 值指派給 `UsernameToMatch`。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample10.cs)]

在此程式碼準備就緒後，請測試篩選功能。 第一次造訪網頁時，會顯示所有使用者帳戶（請參閱 [圖 5]）。 按一下 LinkButton 會導致回傳並篩選結果，只顯示以為開頭的使用者帳戶。

[![使用 [篩選] LinkButtons，顯示使用者名稱以特定字母開頭](building-an-interface-to-select-one-user-account-from-many-cs/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image16.png)

**圖 6**：使用 [篩選] LinkButtons 來顯示使用者名稱以特定字母開頭的使用者（[按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image18.png)）

## <a name="step-4-updating-the-gridview-to-use-paging"></a>步驟4：更新 GridView 以使用分頁

[圖 5] 和 [6] 所示的 GridView 會列出從 `FindUsersByName` 方法傳回的所有記錄。 如果有數百或數千個使用者帳戶，則在查看所有帳戶時，這可能會導致資訊多載（就像是在按一下 [所有 LinkButton] 時，或一開始造訪頁面時的情況）。 為了協助以更容易管理的區塊呈現使用者帳戶，讓我們將 GridView 設定為一次顯示10個使用者帳戶。

GridView 控制項提供兩種類型的分頁：

- **預設分頁**-容易執行，但效率不佳。 簡言之，使用預設分頁時，GridView 會預期其資料來源中的*所有*記錄。 然後，它只會顯示適當的記錄頁面。
- **自訂分頁**-需要執行更多工作，但比預設分頁更有效率，因為使用自訂分頁時，資料來源只會傳回要顯示的精確記錄集。

分頁到數千筆記錄時，預設和自訂分頁的效能差異可能相當大。 因為我們會建立此介面，假設可能有數百個或數千個使用者帳戶，讓我們使用自訂分頁。

> [!NOTE]
> 如需有關預設和自訂分頁之間差異的詳細討論，以及與執行自訂分頁有關的挑戰，請參閱[有效率地分頁處理大量資料](https://asp.net/learn/data-access/tutorial-25-cs.aspx)。 如需預設和自訂分頁之間效能差異的分析，請參閱[ASP.NET 中的自訂分頁與 SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)。

若要執行自訂分頁，我們首先需要一些機制來抓取 GridView 所顯示的確切記錄子集。 好消息是，`Membership` 類別的 `FindUsersByName` 方法有一個多載，可讓我們指定頁面索引和頁面大小，而且只會傳回落在該記錄範圍內的使用者帳戶。

特別是，此多載具有下列簽章： [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx)。

*PageIndex*參數會指定要傳回的使用者帳戶頁面。*pageSize*指出每頁要顯示的記錄數目。 *TotalRecords*參數是一個 `out` 參數，會傳回使用者存放區中使用者帳戶的總數。

> [!NOTE]
> `FindUsersByName` 所傳回的資料會依使用者名稱排序;無法自訂排序準則。

GridView 可以設定為使用自訂分頁，但僅限於系結至 ObjectDataSource 控制項時。 若要讓 ObjectDataSource 控制項執行自訂分頁，它需要兩個方法：一個傳遞開始資料列索引和要顯示的最大記錄數目，然後傳回落在該範圍內的確切記錄子集;和方法，其會傳回已逐頁查看的記錄總數。 `FindUsersByName` 多載會接受頁面索引和頁面大小，並透過 `out` 參數傳回記錄的總數。 這裡有介面不相符的問題。

其中一個選項是建立 proxy 類別，以公開 ObjectDataSource 所預期的介面，然後在內部呼叫 `FindUsersByName` 方法。 另一個選項-我們將在本文中使用的是建立自己的分頁介面，並使用它來取代 GridView 的內建分頁介面。

### <a name="creating-a-first-previous-next-last-paging-interface"></a>建立第一個、上一個、下一個、最後一個分頁介面

讓我們建立一個分頁介面，其中第一個、上一個、下一個和最後一個 LinkButtons。 第一個 LinkButton 按一下時，會將使用者帶到第一頁的資料，而先前的則會將他傳回上一頁。 同樣地，[下一步] 和 [最後] 會分別將使用者移至下一頁和最後一頁。 將四個 LinkButton 控制項新增至 `UserAccounts` GridView 底下。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample11.aspx)]

接下來，為每個 LinkButton 的 `Click` 事件建立事件處理常式。

[圖 7] 顯示透過 Visual Web Developer 設計檢視觀看的四個 LinkButtons。

[![在 GridView 底下新增 First、Previous、Next 和 Last LinkButtons](building-an-interface-to-select-one-user-account-from-many-cs/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image19.png)

**圖 7**：在 GridView 底下新增第一個、上一個、下一個和最後一個 LinkButtons （[按一下以觀看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image21.png)）

### <a name="keeping-track-of-the-current-page-index"></a>追蹤目前的頁面索引

當使用者第一次造訪 [`ManageUsers.aspx`] 頁面，或按一下其中一個篩選按鈕時，我們想要顯示 GridView 中的第一頁數據。 不過，當使用者按一下其中一個導覽 LinkButtons 時，我們需要更新頁面索引。 若要維護頁面索引和每頁顯示的記錄數目，請將下列兩個屬性新增至頁面的程式碼後置類別：

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample12.cs)]

就像 `UsernameToMatch` 屬性一樣，`PageIndex` 屬性會保存其值以查看狀態。 唯讀 `PageSize` 屬性會傳回硬式編碼的值10。 我邀請感興趣的讀者更新此屬性，以使用與 `PageIndex`相同的模式，然後擴大 `ManageUsers.aspx` 頁面，讓流覽頁面的人可以指定每頁顯示的使用者帳戶數目。

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>只取出目前頁面的記錄、更新頁面索引，以及啟用和停用分頁介面 LinkButtons

使用分頁介面並加入 `PageIndex` 和 `PageSize` 屬性之後，我們就可以更新 `BindUserAccounts` 方法，使其使用適當的 `FindUsersByName` 多載。 此外，我們必須根據顯示的頁面，讓此方法啟用或停用分頁介面。 當您在流覽資料的第一頁時，應該停用第一個和前一個連結;在觀看最後一頁時，應該停用 [下一步] 和 [上次]。

以下列程式碼取代 `BindUserAccounts` 方法：

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample13.cs)]

請注意，逐頁查看的記錄總數取決於 `FindUsersByName` 方法的最後一個參數。 這是 `out` 參數，因此我們必須先宣告變數來保存此值（`totalRecords`），然後在其前面加上 `out` 關鍵字。

傳回使用者帳戶的指定頁面之後，系統會根據資料的第一個或最後一頁是否正在查看，而啟用或停用四個 LinkButtons。

最後一個步驟是為四個 LinkButtons 的「`Click` 事件處理常式撰寫程式碼。 這些事件處理常式必須更新 `PageIndex` 屬性，然後透過呼叫 `BindUserAccounts`將資料重新系結至 GridView。 第一個、上一個和下一個事件處理常式非常簡單。 不過，最後一個 LinkButton 的 `Click` 事件處理常式比較複雜一點，因為我們必須判斷要顯示多少筆記錄，才能判斷最後一頁的索引。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample14.cs)]

圖8和9顯示自訂分頁介面的實際運作方式。 [圖 8] 顯示為所有使用者帳戶流覽資料的第一頁時的 `ManageUsers.aspx` 頁面。 請注意，只會顯示13個帳戶中的10個。 按一下 [下一步] 或 [最後一個] 連結會導致回傳、將 `PageIndex` 更新為1，並將使用者帳戶的第二頁系結至方格（請參閱 [圖 9]）。

[顯示前10個使用者帳戶 ![](building-an-interface-to-select-one-user-account-from-many-cs/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image22.png)

**圖 8**：顯示前10名使用者帳戶（[按一下以觀看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image24.png)）

[![按一下 [下一步] 連結會顯示使用者帳戶的第二頁](building-an-interface-to-select-one-user-account-from-many-cs/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image25.png)

**圖 9**：按一下 [下一步] 連結會顯示使用者帳戶的第二頁（[按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-cs/_static/image27.png)）

## <a name="summary"></a>總結

系統管理員通常需要從帳戶清單中選取使用者。 在先前的教學課程中，我們探討了如何使用已填入使用者的下拉式清單，但此方法無法妥善調整。 在本教學課程中，我們探討了更好的替代方式：其結果會顯示在分頁 GridView 中的可篩選介面。 系統管理員可以使用此使用者介面，快速且有效率地找出並選取其中的一個使用者帳戶。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [在 ASP.NET 中使用 SQL Server 2005 的自訂分頁](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [有效率地分頁處理大量資料](https://asp.net/learn/data-access/tutorial-25-cs.aspx)
- [推出您自己的網站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Alicja Maziarz。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [下一步](recovering-and-changing-passwords-cs.md)
