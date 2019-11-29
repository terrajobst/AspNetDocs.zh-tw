---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-vb
title: 儲存額外的使用者資訊（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將建立一個非常基本的留言簿應用程式來回答這個問題。 在這種情況下，我們將探討 modeli 的不同選項 。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: ee4b924e-8002-4dc3-819f-695fca1ff867
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-vb
msc.type: authoredcontent
ms.openlocfilehash: cb352de6f7c2d117b41532112a87956c8dde62f8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74638847"
---
# <a name="storing-additional-user-information-vb"></a>儲存其他的使用者資訊 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_VB.zip)或[下載 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_vb.pdf)

> 在本教學課程中，我們將建立一個非常基本的留言簿應用程式來回答這個問題。 在這種情況下，我們將探討在資料庫中建立使用者資訊模型的不同選項，然後瞭解如何將此資料與成員資格架構所建立的使用者帳戶產生關聯。

## <a name="introduction"></a>簡介

ASP.NET 的成員資格架構提供彈性的介面來管理使用者。 成員資格 API 包含驗證認證的方法、抓取目前登入之使用者的相關資訊、建立新的使用者帳戶，以及刪除使用者帳戶等等。 成員資格架構中的每個使用者帳戶只包含驗證認證所需的屬性，以及執行重要的使用者帳戶相關工作。 這是由[`MembershipUser` 類別](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)的方法和屬性所總合，這會在成員資格架構中建立使用者帳戶模型。 這個類別的屬性如[`UserName`](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx)、 [`Email`](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx)和[`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)，以及[`GetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx)和[`UnlockUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)之類的方法。

應用程式經常需要儲存成員資格架構中未包含的其他使用者資訊。 例如，線上零售商可能需要讓每位使用者儲存其出貨和帳單位址、付款資訊、傳遞喜好設定和連絡人電話號碼。 此外，系統中的每個訂單都與特定的使用者帳戶相關聯。

`MembershipUser` 類別不包含 `PhoneNumber` 或 `DeliveryPreferences` 或 `PastOrders`等屬性。 那麼，我們要如何追蹤應用程式所需的使用者資訊，並讓它與成員資格架構整合？ 在本教學課程中，我們將建立一個非常基本的留言簿應用程式來回答這個問題。 在這種情況下，我們將探討在資料庫中建立使用者資訊模型的不同選項，然後瞭解如何將此資料與成員資格架構所建立的使用者帳戶產生關聯。 讓我們開始吧！

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>步驟1：建立留言簿應用程式的資料模型

有各種不同的技巧可以用來在資料庫中捕捉使用者資訊，並將其與成員資格架構所建立的使用者帳戶產生關聯。 為了說明這些技巧，我們必須擴充教學課程 web 應用程式，讓它能夠捕捉到某種使用者相關的資料。 （目前，應用程式的資料模型只包含 `SqlMembershipProvider`所需的應用程式服務資料表）。

讓我們建立一個非常簡單的留言簿應用程式，其中已驗證的使用者可以離開留言。 除了儲存留言簿留言，讓我們能夠讓每位使用者儲存他的城市、首頁和簽章。 若有提供，使用者的家庭城鎮、首頁和簽章將會出現在他離開留言簿的每則訊息上。

### <a name="adding-theguestbookcommentstable"></a>加入`GuestbookComments`資料表

為了捕捉留言簿留言，我們需要建立名為 `GuestbookComments` 的資料庫資料表，其中具有 `CommentId`、`Subject`、`Body`和 `CommentDate`等資料行。 我們也需要 `GuestbookComments` 資料表中的每筆記錄都參考離開批註的使用者。

若要將此資料表新增至資料庫，請移至 Visual Studio 中的資料庫總管，向下切入至 `SecurityTutorials` 資料庫。 以滑鼠右鍵按一下 [資料表] 資料夾，然後選擇 [加入新資料表]。 這會出現一個介面，可讓我們定義新資料表的資料行。

[![將新資料表新增至 SecurityTutorials 資料庫](storing-additional-user-information-vb/_static/image2.png)](storing-additional-user-information-vb/_static/image1.png)

**圖 1**：在 `SecurityTutorials` 資料庫中加入新的資料表（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image3.png)）

接下來，定義 `GuestbookComments`的資料行。 首先，新增名為 `CommentId` 類型為 `uniqueidentifier`的資料行。 此欄會唯一識別留言簿中的每個留言，因此不允許 `NULL` s，並將其標示為數據表的主鍵。 我們 `INSERT` `uniqueidentifier` 可以將資料行的預設值設定為 [`NEWID()`]，而不是針對每個 `INSERT`上的 [`CommentId`] 欄位提供一個值。 新增第一個欄位、將它標示為主要金鑰，並設定其預設值之後，您的畫面看起來應該像 [圖 2] 所示的螢幕擷取畫面。

[![新增名為 CommentId 的主要資料行](storing-additional-user-information-vb/_static/image5.png)](storing-additional-user-information-vb/_static/image4.png)

**圖 2**：新增名為 `CommentId` 的主要資料行（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image6.png)）

接下來，新增名為 `Subject` 類型為 `nvarchar(50)` 的資料行，以及類型 `nvarchar(MAX)`的資料 `Body` 行，並在兩個數據行中不允許 `NULL` s。 接著，新增名為 `CommentDate` 類型為 `datetime`的資料行。 不允許 `NULL` s，並將 `CommentDate` 資料行的預設值設定為 [`getdate()`]。

剩下的工作就是加入一個資料行，將使用者帳戶與每個留言簿留言產生關聯。 其中一個選項是新增名為 `UserName` 類型為 `nvarchar(256)`的資料行。 當使用 `SqlMembershipProvider`以外的成員資格提供者時，這是適當的選擇。 但是當使用 `SqlMembershipProvider`時，如我們在本教學課程的系列中，`aspnet_Users` 資料表中的 `UserName` 資料行並不保證是唯一的。 `aspnet_Users` 資料表的主要索引鍵是 `UserId`，而且屬於類型 `uniqueidentifier`。 因此，`GuestbookComments` 資料表需要名為 `UserId` 類型為 `uniqueidentifier` 的資料行（不允許 `NULL` 值）。 請繼續並加入此資料行。

> [!NOTE]
> 如我們在 SQL Server 教學課程中[*建立成員資格架構*](creating-the-membership-schema-in-sql-server-vb.md)中所討論，成員資格架構的設計是為了讓多個具有不同使用者帳戶的 web 應用程式共用相同的使用者存放區。 其運作方式是將使用者帳戶分割成不同的應用程式。 而且，雖然每個使用者名稱在應用程式中都是唯一的，但在使用相同使用者存放區的不同應用程式中，可能會使用相同的使用者名稱。 在 [`UserName`] 和 [`ApplicationId`] 欄位的 [`aspnet_Users`] 資料表中，有一個複合 `UNIQUE` 條件約束，但只能在 [`UserName`] 欄位上有一個。 因此，aspnet\_Users 資料表可以有兩個（或多個）具有相同 `UserName` 值的記錄。 不過，`aspnet_Users` 資料表的 `UserId` 欄位上有 `UNIQUE` 條件約束（因為它是主要索引鍵）。 `UNIQUE` 條件約束很重要，因為如果沒有，就無法在 `GuestbookComments` 和 `aspnet_Users` 資料表之間建立外鍵條件約束。

加入 `UserId` 資料行之後，請按一下工具列中的 [儲存] 圖示來儲存資料表。 將新的資料表命名為 `GuestbookComments`。

我們有最後一個要參與 `GuestbookComments` 資料表的問題：我們需要在 [`GuestbookComments.UserId`] 資料行和 [`aspnet_Users.UserId`] 資料行之間建立[外鍵條件約束](https://msdn.microsoft.com/library/ms175464.aspx)。 若要達成此目的，請按一下工具列中的 [關聯性] 圖示，以啟動 [外鍵關聯性] 對話方塊。 （或者，您可以前往 [資料表設計工具] 功能表並選擇 [關聯性] 來啟動此對話方塊）。

按一下 [外鍵關聯性] 對話方塊左下角的 [加入] 按鈕。 這會加入新的外鍵條件約束，但我們仍需要定義參與關聯性的資料表。

[![使用 [外鍵關聯性] 對話方塊來管理資料表的外鍵條件約束](storing-additional-user-information-vb/_static/image8.png)](storing-additional-user-information-vb/_static/image7.png)

**圖 3**：使用 [外鍵關聯性] 對話方塊來管理資料表的外鍵條件約束（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image9.png)）

接下來，按一下右邊 [資料表和資料行規格] 資料列中的省略號圖示。 這會啟動 [資料表和資料行] 對話方塊，我們可以從中指定主鍵資料表和資料行，以及來自 `GuestbookComments` 資料表的外鍵資料行。 特別是，請選取 `aspnet_Users` 並 `UserId` 做為主鍵資料表和資料行，然後從 `GuestbookComments` 資料表 `UserId` 做為外鍵資料行（請參閱 [圖 4]）。 定義主鍵和外鍵資料表和資料行之後，請按一下 [確定] 以返回 [外鍵關聯性] 對話方塊。

[![在 aspnet_Users 和 GuesbookComments 資料表之間建立外鍵條件約束](storing-additional-user-information-vb/_static/image11.png)](storing-additional-user-information-vb/_static/image10.png)

**圖 4**：在 `aspnet_Users` 和 `GuesbookComments` 資料表之間建立外鍵條件約束（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image12.png)）

此時已建立外鍵條件約束。 這個條件約束的存在可確保這兩個數據表之間的[關聯式完整性](http://en.wikipedia.org/wiki/Referential_integrity)，藉由確保永遠不會有參考不存在之使用者帳戶的留言簿專案。 根據預設，如果有對應的子記錄，外鍵條件約束將不允許刪除父記錄。 也就是說，如果使用者提出一或多個留言簿留言，然後嘗試刪除該使用者帳戶，除非先刪除他的留言簿批註，否則刪除將會失敗。

外鍵條件約束可設定為在刪除父記錄時，自動刪除相關聯的子記錄。 換句話說，我們可以設定這個外鍵條件約束，讓使用者的留言簿專案在刪除使用者帳戶時自動刪除。 若要完成此動作，請展開 [插入和更新規格] 區段，並將 [刪除規則] 屬性設定為 [Cascade]。

[![設定外鍵條件約束以重迭刪除](storing-additional-user-information-vb/_static/image14.png)](storing-additional-user-information-vb/_static/image13.png)

**圖 5**：設定外鍵條件約束以重迭刪除（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image15.png)）

若要儲存外鍵條件約束，請按一下 [關閉] 按鈕結束外鍵關聯性。 然後按一下工具列中的 [儲存] 圖示，以儲存資料表和此關聯性。

### <a name="storing-the-users-home-town-homepage-and-signature"></a>儲存使用者的家庭城鎮、首頁和簽章

`GuestbookComments` 表說明如何儲存與使用者帳戶共用一對多關聯性的資訊。 由於每個使用者帳戶可能會有任意數目的相關批註，因此此關聯性是藉由建立資料表來保存一組批註來進行模型化，其中包含一個將每個批註連結回特定使用者的資料行。 使用 `SqlMembershipProvider`時，最好是建立一個 `uniqueidentifier` 型別為 `UserId` 的資料行，並將此資料行與 `aspnet_Users.UserId`之間的外鍵條件約束建立。

我們現在必須將三個數據行與每個使用者帳戶產生關聯，以儲存使用者的家庭城鎮、首頁和簽章，這會顯示在他的留言簿留言中。 有幾種不同的方式可以完成這項操作：

- <strong>將新的資料行加入至</strong><strong>`aspnet_Users`</strong><strong>或</strong><strong>`aspnet_Membership`</strong><strong>資料表。</strong> 我不建議這種方法，因為它會修改 `SqlMembershipProvider`所使用的架構。 這個決策可能會回到輪你」您的道路。 例如，如果未來版本的 ASP.NET 使用不同的 `SqlMembershipProvider` 架構，該怎麼辦。 Microsoft 可能會包含將 ASP.NET 2.0 `SqlMembershipProvider` 資料移轉至新架構的工具，但如果您已修改 ASP.NET 2.0 `SqlMembershipProvider` 架構，則可能無法進行轉換。

- **使用 ASP。NET 的設定檔架構，定義家庭城鎮、首頁和簽章的配置檔案屬性。** ASP.NET 包含一個設定檔架構，其設計目的是用來儲存額外的使用者特定資料。 如同成員資格架構，設定檔架構是建立在提供者模型的上方。 .NET Framework 隨附 `SqlProfileProvider`，將設定檔資料儲存在 SQL Server 資料庫中。 事實上，我們的資料庫已經有 `SqlProfileProvider` （`aspnet_Profile`）所使用的資料表，因為當我們在 SQL Server 教學課程的[*建立成員資格架構*](creating-the-membership-schema-in-sql-server-vb.md)中新增應用程式服務時，就會將它新增回來。   
  設定檔架構的主要優點是，它可讓開發人員在 `Web.config` 中定義配置檔案屬性，而不需要撰寫任何程式碼，將設定檔資料序列化到基礎資料存放區。 簡單地說，定義一組配置檔案屬性，並在程式碼中使用它們是非常簡單的。 不過，配置檔案系統在進行版本控制時，會留下許多需要的內容，因此如果您的應用程式會在稍後新增使用者特定的屬性，或是要移除或修改現有的內容，則設定檔架構可能不是 最佳選項。 此外，`SqlProfileProvider` 會以高度反正規化的方式儲存配置檔案屬性，讓它不可能直接針對設定檔資料執行查詢（例如，有多少使用者擁有紐約的城市）。   
  如需有關設定檔架構的詳細資訊，請參閱本教學課程結尾處的「進一步閱讀」一節。

- <strong>將這三個數據行加入至資料庫中的新資料表，並在這個資料表與`aspnet_Users`之間建立一對一關聯性</strong> <strong>。</strong> 這種方法牽涉到比設定檔架構更多的工作，但提供在資料庫中建立其他使用者屬性模型的最大彈性。 這是我們將在本教學課程中使用的選項。

我們將建立名為 `UserProfiles` 的新資料表，以儲存每位使用者的家庭城鎮、首頁和簽章。 以滑鼠右鍵按一下 [資料庫總管] 視窗中的 [資料表] 資料夾，然後選擇 [建立新的資料表]。 將第一個資料行命名為 `UserId`，並將其類型設定為 `uniqueidentifier`。 不允許 `NULL` 值，並將資料行標示為主鍵。 接下來，新增名為的資料行： `nvarchar(50)`的 `HomeTown` 類型;`nvarchar(100)`類型的 `HomepageUrl`;和類型 `nvarchar(500)`的簽章。 這三個數據行中的每一個都可以接受 `NULL` 值。

[![建立 UserProfiles 資料表](storing-additional-user-information-vb/_static/image17.png)](storing-additional-user-information-vb/_static/image16.png)

**圖 6**：建立 `UserProfiles` 資料表（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image18.png)）

儲存資料表，並將它命名為 `UserProfiles`。 最後，在 `UserProfiles` 資料表的 [`UserId`] 欄位和 [`aspnet_Users.UserId`] 欄位之間建立外鍵條件約束。 如同我們對 `GuestbookComments` 和 `aspnet_Users` 資料表之間的外鍵條件約束所做的一樣，請將這個條件約束 cascade 刪除。 因為 `UserProfiles` 中的 [`UserId`] 欄位是主要金鑰，所以這可確保每個使用者帳戶的 `UserProfiles` 資料表中不會有一個以上的記錄。 這種類型的關聯性稱為「一對一」。

既然我們已經建立資料模型，我們就可以開始使用了。 在步驟2和3中，我們將探討目前登入的使用者如何能夠查看和編輯其主城市、首頁和簽章資訊。 在步驟4中，我們將為已驗證的使用者建立介面，以將新留言提交給留言簿，並查看現有的意見。

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>步驟2：顯示使用者的家庭城鎮、首頁和簽章

有多種方式可讓目前登入的使用者查看和編輯他的家庭城鎮、首頁和簽章資訊。 我們可以用 TextBox 和 Label 控制項手動建立使用者介面，也可以使用其中一個資料 Web 控制項，例如 DetailsView 控制項。 若要執行資料庫 `SELECT` 和 `UPDATE` 語句，我們可以在頁面的程式碼後置類別中撰寫 ADO.NET 程式碼，或者在 SqlDataSource 中使用宣告式方法。 在理想情況下，我們的應用程式會包含階層式架構，我們可以從頁面的程式碼後置類別以程式設計方式叫用，或透過 ObjectDataSource 控制項以宣告方式叫用。

由於本教學課程系列著重于表單驗證、授權、使用者帳戶和角色，因此將不會徹底討論這些不同的資料存取選項，也不會對階層式架構的偏好直接執行 SQL 語句從 [ASP.NET] 頁面。 我將逐步解說使用 DetailsView 和 SqlDataSource –最快速且最簡單的選項，但所討論的概念當然可以套用至替代的 Web 控制項和資料存取邏輯。 如需在 ASP.NET 中使用資料的詳細資訊，請參閱我 *[在 ASP.NET 2.0](../../data-access/index.md)* 教學課程系列中使用資料。

開啟 [`Membership`] 資料夾中的 [`AdditionalUserInfo.aspx`] 頁面，並將 [DetailsView] 控制項新增至頁面，並將其 [ID] 屬性設為 [`UserProfile`]，並清除其 `Width` 和 [`Height`] 屬性。 展開 DetailsView 的智慧標籤，並選擇將其系結至新的資料來源控制項。 這將啟動資料來源設定向導（請參閱 [圖 7]）。 第一個步驟會要求您指定資料來源類型。 因為我們要直接連接到 `SecurityTutorials` 資料庫，所以請選擇 [資料庫] 圖示，並將 `ID` 指定為 [`UserProfileDataSource`]。

[![新增名為 UserProfileDataSource 的新 SqlDataSource 控制項](storing-additional-user-information-vb/_static/image20.png)](storing-additional-user-information-vb/_static/image19.png)

**圖 7**：新增名為 `UserProfileDataSource` 的新 SqlDataSource 控制項（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image21.png)）

下一個畫面會提示您輸入要使用的資料庫。 我們已經在 `Web.config` 中定義 `SecurityTutorials` 資料庫的連接字串。 此連接字串名稱– `SecurityTutorialsConnectionString` –應該在下拉式清單中。 選取此選項，然後按 [下一步]。

[![從下拉式清單中選擇 [SecurityTutorialsConnectionString]](storing-additional-user-information-vb/_static/image23.png)](storing-additional-user-information-vb/_static/image22.png)

**圖 8**：從下拉式清單中選擇 [`SecurityTutorialsConnectionString`] （[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image24.png)）

接下來的畫面會要求我們指定要查詢的資料表和資料行。 從下拉式清單中選擇 [`UserProfiles`] 資料表，並檢查所有資料行。

[![從 UserProfiles 資料表取回所有資料行](storing-additional-user-information-vb/_static/image26.png)](storing-additional-user-information-vb/_static/image25.png)

**圖 9**：帶回 `UserProfiles` 資料表中的所有資料行（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image27.png)）

[圖 9] 中的目前查詢會傳回 `UserProfiles`中的*所有*記錄，但我們只對目前登入的使用者記錄感興趣。 若要加入 `WHERE` 子句，請按一下 [`WHERE`] 按鈕以顯示 [加入 `WHERE` 子句] 對話方塊（請參閱 [圖 10]）。 您可以在這裡選取要篩選的資料行、運算子和篩選參數的來源。 選取 [`UserId`] 做為 [資料行] 和 [=] 做為運算子。

不幸的是，沒有內建參數來源可傳回目前登入的使用者 `UserId` 值。 我們需要以程式設計的方式抓取此值。 因此，請將 [來源] 下拉式清單設定為 [無]，然後按一下 [新增] 按鈕以新增參數，再按一下 [確定]。

[![在 UserId 資料行上加入篩選參數](storing-additional-user-information-vb/_static/image29.png)](storing-additional-user-information-vb/_static/image28.png)

**圖 10**：在 [`UserId`] 資料行上加入篩選參數（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image30.png)）

按一下 [確定] 之後，就會回到 [圖 9] 所示的畫面。 不過，這次畫面底部的 SQL 查詢應該包含 `WHERE` 子句。 按 [下一步] 以移至 [測試查詢] 畫面。 您可以在這裡執行查詢並查看結果。 按一下 [完成] 以完成精靈。

完成資料來源設定 Wizard 時，Visual Studio 會根據 Wizard 中指定的設定來建立 SqlDataSource 控制項。 此外，它也會針對 SqlDataSource 的 `SelectCommand`所傳回的每個資料行，以手動方式將 BoundFields 新增至 DetailsView。 不需要在 DetailsView 中顯示 [`UserId`] 欄位，因為使用者不需要知道此值。 您可以直接從 DetailsView 控制項的宣告式標記中移除此欄位，或按一下其智慧標籤中的 [編輯欄位] 連結。

此時，您頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample1.aspx)]

我們需要在選取資料之前，以程式設計方式將 SqlDataSource 控制項的 `UserId` 參數設定為目前登入的使用者 `UserId`。 藉由建立 SqlDataSource 的 `Selecting` 事件的事件處理常式，並在該處新增下列程式碼，即可完成這項作業：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample2.vb)]

上述程式碼一開始會藉由呼叫 `Membership` 類別的 `GetUser` 方法，取得目前登入之使用者的參考。 這會傳回 `MembershipUser` 物件，其 `ProviderUserKey` 屬性包含 `UserId`。 `UserId` 值接著會指派給 SqlDataSource 的 `@UserId` 參數。

> [!NOTE]
> `Membership.GetUser()` 方法會傳回目前登入之使用者的相關資訊。 如果匿名使用者正在造訪頁面，則會傳回 `Nothing`的值。 在這種情況下，當嘗試讀取 `ProviderUserKey` 屬性時，這會導致下列程式程式碼 `NullReferenceException`。 當然，我們不需要擔心 `Membership.GetUser()` 在 `AdditionalUserInfo.aspx` 頁面中傳回任何內容，因為我們在上一個教學課程中設定了 URL 授權，因此只有經過驗證的使用者才能存取此資料夾中的 ASP.NET 資源。 如果您需要在允許匿名存取的頁面中存取目前登入之使用者的相關資訊，請務必先檢查從 `GetUser()` 方法傳回的 `MembershipUser` 物件是否不是任何內容，再參考其屬性。

如果您透過瀏覽器造訪 [`AdditionalUserInfo.aspx`] 頁面，將會看到空白頁面，因為我們尚未將任何資料列加入 `UserProfiles` 資料表。 在步驟6中，我們將探討如何自訂 CreateUserWizard 控制項，以便在建立新的使用者帳戶時，自動將新的資料列加入至 `UserProfiles` 資料表。 不過，我們現在需要在資料表中手動建立一筆記錄。

流覽至 Visual Studio 中的資料庫總管，然後展開 [資料表] 資料夾。 以滑鼠右鍵按一下 [`aspnet_Users`] 資料表，然後選擇 [顯示資料表資料] 以查看資料表中的記錄;針對 `UserProfiles` 資料表執行相同的動作。 [圖 11] 以垂直並排顯示這些結果。 在我的資料庫中，目前有 Bruce、Fred 和 Tito 的 `aspnet_Users` 記錄，但 `UserProfiles` 資料表中沒有任何記錄。

[![顯示 aspnet_Users 和 UserProfiles 資料表的內容](storing-additional-user-information-vb/_static/image32.png)](storing-additional-user-information-vb/_static/image31.png)

**圖 11**：顯示 `aspnet_Users` 和 `UserProfiles` 資料表的內容（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image33.png)）

手動輸入 [`HomeTown`]、[`HomepageUrl`] 和 [`Signature`] 欄位的值，以將新記錄新增至 `UserProfiles` 資料表。 若要在新的 `UserProfiles` 記錄中取得有效的 `UserId` 值，最簡單的方式是在 `aspnet_Users` 資料表中選取特定使用者帳戶的 [`UserId`] 欄位，然後將它複製並貼到 `UserId` 的 [`UserProfiles`] 欄位中。 [圖 12] 顯示加入 Bruce 的新記錄之後的 `UserProfiles` 資料表。

[![A 記錄新增至 Bruce 的 UserProfiles](storing-additional-user-information-vb/_static/image35.png)](storing-additional-user-information-vb/_static/image34.png)

**圖 12**：已將記錄新增至 Bruce 的 `UserProfiles` （[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image36.png)）

返回 `AdditionalUserInfo.aspx page`，以 Bruce 的身分登入。 如 [圖 13] 所示，會顯示 Bruce 的設定。

[![目前造訪的使用者顯示他的設定](storing-additional-user-information-vb/_static/image38.png)](storing-additional-user-information-vb/_static/image37.png)

**圖 13**：目前造訪的使用者顯示他的設定（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image39.png)）

> [!NOTE]
> 繼續進行，並在每個成員資格使用者的 `UserProfiles` 資料表中手動新增記錄。 在步驟6中，我們將探討如何自訂 CreateUserWizard 控制項，以便在建立新的使用者帳戶時，自動將新的資料列加入至 `UserProfiles` 資料表。

## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>步驟3：允許使用者編輯他的家庭城鎮、首頁和簽章

此時，目前登入的使用者可以查看其主城市、首頁和簽章設定，但他們尚未修改。 讓我們更新 DetailsView 控制項，讓資料可供編輯。

我們要做的第一件事是新增 SqlDataSource 的 `UpdateCommand`，並指定要執行的 `UPDATE` 語句及其對應的參數。 選取 SqlDataSource，然後在 屬性視窗中，按一下 UpdateQuery 屬性旁邊的省略號，以顯示 命令和參數編輯器 對話方塊。 在文字方塊中輸入下列 `UPDATE` 語句：

[!code-sql[Main](storing-additional-user-information-vb/samples/sample3.sql)]

接下來，按一下 [重新整理參數] 按鈕，這會在 SqlDataSource 控制項的 `UpdateParameters` 集合中，為 `UPDATE` 語句中的每個參數建立參數。 將所有參數的 [來源] 保持設定為 [無]，然後按一下 [確定] 按鈕以完成對話方塊。

[![指定 SqlDataSource 的 UpdateCommand 和 UpdateParameters](storing-additional-user-information-vb/_static/image41.png)](storing-additional-user-information-vb/_static/image40.png)

**圖 14**：指定 SqlDataSource 的 `UpdateCommand` 和 `UpdateParameters` （[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image42.png)）

由於我們對 SqlDataSource 控制項所做的新增，DetailsView 控制項現在可以支援編輯。 從 DetailsView 的智慧標籤中，勾選 [啟用編輯] 核取方塊。 這會將 CommandField 新增至控制項的 `Fields` 集合，並將其 `ShowEditButton` 屬性設定為 True。 當 DetailsView 以唯讀模式顯示，並在 [編輯] 模式中顯示 [更新] 和 [取消] 按鈕時，這會轉譯 [編輯] 按鈕。 雖然我們可以將 DetailsView 控制項的[`DefaultMode` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx)設定為 `Edit`，而不需要使用者按一下 [編輯]，而是讓 detailsview 呈現為「永遠可編輯」狀態。

有了這些變更，您的 DetailsView 控制項的宣告式標記看起來應該如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample4.aspx)]

請注意 CommandField 和 `DefaultMode` 屬性的新增。

繼續進行，並透過瀏覽器測試此頁面。 當您造訪 `UserProfiles`中具有對應記錄的使用者時，使用者的設定會顯示在可編輯的介面中。

[![DetailsView 呈現可編輯的介面](storing-additional-user-information-vb/_static/image44.png)](storing-additional-user-information-vb/_static/image43.png)

**圖 15**： DetailsView 呈現可編輯的介面（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image45.png)）

請嘗試變更值，然後按一下 [更新] 按鈕。 看起來好像沒有發生。 有一個回傳，值會儲存到資料庫中，但不會有任何視覺效果的意見反應會發生儲存。

若要解決此問題，請回到 Visual Studio，並在 DetailsView 上方新增標籤控制項。 將其 `ID` 設為 `SettingsUpdatedMessage`、其 `Text` 屬性設定為「您的設定已更新」，以及要 `EnableViewState` 的 `Visible` 和 `False`屬性。

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample5.aspx)]

每次更新 DetailsView 時，都需要顯示 [`SettingsUpdatedMessage`] 標籤。 若要完成這項操作，請為 DetailsView 的 `ItemUpdated` 事件建立事件處理常式，並新增下列程式碼：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample6.vb)]

透過瀏覽器返回 [`AdditionalUserInfo.aspx`] 頁面並更新資料。 這次會顯示實用的狀態訊息。

[![更新設定時，會顯示短訊息](storing-additional-user-information-vb/_static/image47.png)](storing-additional-user-information-vb/_static/image46.png)

**圖 16**：更新設定時，會顯示簡短訊息（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image48.png)）

> [!NOTE]
> DetailsView 控制項的編輯介面有很多工作需要。 它會使用標準大小的文字方塊，但簽章欄位應該是多行文字方塊。 RegularExpressionValidator 應該用來確保首頁 URL （如果輸入）是以 "HTTP://" 或 "HTTPs://" 為開頭。 此外，由於 DetailsView 控制項的 `DefaultMode` 屬性設定為 `Edit`，因此 [取消] 按鈕不會執行任何動作。 您應該將它移除，或在按一下時，將使用者重新導向至其他頁面（例如 `~/Default.aspx`）。 我將這些增強功能留給讀者的練習。

### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>將連結新增至主版頁面中的 [`AdditionalUserInfo.aspx`] 頁面

網站目前未提供任何 `AdditionalUserInfo.aspx` 頁面的連結。 唯一的方法是直接在瀏覽器的網址列中輸入頁面的 URL。 讓我們在 `Site.master` 主版頁面中新增此頁面的連結。

回想一下，主版頁面在其 `LoginContent` ContentPlaceHolder 中包含一個 LoginView 的 Web 控制項，它會針對已驗證和匿名的訪客顯示不同的標記。 更新 LoginView 控制項的 `LoggedInTemplate`，以包含 `AdditionalUserInfo.aspx` 頁面的連結。 進行這些變更之後，LoginView 控制項的宣告式標記看起來應該如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample7.aspx)]

請注意，將 `lnkUpdateSettings` HyperLink 控制項加入至 `LoggedInTemplate`。 使用此連結時，已驗證的使用者可以快速跳至頁面，以查看及修改其主城市、首頁和簽章設定。

## <a name="step-4-adding-new-guestbook-comments"></a>步驟4：加入新的留言簿留言

[`Guestbook.aspx`] 頁面是已驗證的使用者可以在其中查看留言簿並留下留言的地方。 讓我們從建立介面開始，加入新的留言簿留言。

在 Visual Studio 中開啟 [`Guestbook.aspx`] 頁面，並建立由兩個 TextBox 控制群組成的使用者介面，一個用於新批註的主旨，另一個用於其主體。 將第一個 TextBox 控制項的 `ID` 屬性設為 `Subject`，並將其 `Columns` 屬性設定為 40;將第二個 `ID` 設定為 `Body`、其 `TextMode` `MultiLine`，以及將其 `Width` 和 `Rows` 屬性分別設為 "95%" 和8。 若要完成使用者介面，請新增名為 `PostCommentButton` 的按鈕 Web 控制項，並將其 [`Text`] 屬性設為 [張貼您的留言]。

因為每個留言簿留言都需要主旨和本文，所以請為每個文字方塊新增一個 RequiredFieldValidator。 將這些控制項的 `ValidationGroup` 屬性設定為 "EnterComment";同樣地，將 `PostCommentButton` 控制項的 `ValidationGroup` 屬性設定為 "EnterComment"。 如需 ASP 的詳細資訊。NET 的驗證控制項、簽出[ASP.NET 中的表單驗證](http://www.4guysfromrolla.com/webtech/090200-1.shtml)、[剖析 ASP.NET 2.0 中的驗證控制項](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)，以及[W3Schools](http://www.w3schools.com/)上的[驗證服務器控制項教學](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp)課程。

在製作使用者介面之後，您頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample8.aspx)]

完成使用者介面後，下一個工作是在按一下 `PostCommentButton` 時，將新的記錄插入 `GuestbookComments` 資料表。 這可以透過數種方式來完成：我們可以在按鈕的 `Click` 事件處理常式中撰寫 ADO.NET 程式碼;我們可以將 SqlDataSource 控制項加入至頁面，設定其 `InsertCommand`，然後從 `Click` 事件處理常式中呼叫其 `Insert` 方法;或者，我們可以建立一個負責插入新留言簿留言的仲介層，並從 `Click` 事件處理常式叫用此功能。 因為我們探討了在步驟3中使用 SqlDataSource，所以讓我們在這裡使用 ADO.NET 程式碼。

> [!NOTE]
> 用來以程式設計方式從 Microsoft SQL Server 資料庫存取資料的 ADO.NET 類別位於 `System.Data.SqlClient` 命名空間中。 您可能需要將此命名空間匯入頁面的程式碼後置類別中（亦即 `Imports System.Data.SqlClient`）。

建立 `PostCommentButton`的 `Click` 事件的事件處理常式，並新增下列程式碼：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample9.vb)]

`Click` 事件處理常式會先檢查使用者提供的資料是否有效，以開始。 如果不是，則事件處理常式會在插入記錄之前結束。 假設提供的資料有效，則會抓取目前登入的使用者 `UserId` 值，並將其儲存在 `currentUserId` 區域變數中。 此值是必要的，因為在將記錄插入 `GuestbookComments`時，必須提供 `UserId` 值。

之後，就會從 `Web.config` 抓取 `SecurityTutorials` 資料庫的連接字串，並指定 `INSERT` 的 SQL 語句。 接著會建立並開啟 `SqlConnection` 物件。 接下來，會建立 `SqlCommand` 物件，並指派 `INSERT` 查詢中使用之參數的值。 接著會執行 `INSERT` 語句，並關閉連接。 在事件處理常式的結尾，會清除 [`Subject`] 和 [`Body` textbox] `Text` 屬性，如此一來，使用者的值就不會在回傳期間保存。

請繼續並在瀏覽器中測試此頁面。 因為此頁面位於 `Membership` 資料夾中，所以匿名訪客無法存取它。 因此，您必須先登入（如果您還沒這樣做）。 在 [`Subject`] 和 [`Body`] 文字方塊中輸入值，然後按一下 [`PostCommentButton`] 按鈕。 這會導致新的記錄新增至 `GuestbookComments`。 在回傳時，您提供的主旨和主體會從文字方塊中抹除。

按一下 [`PostCommentButton`] 按鈕之後，就不會有批註新增至 [留言簿] 的視覺效果意見反應。 我們仍然需要更新此頁面，以顯示現有的留言簿留言，我們將在步驟5中執行。 完成之後，就會在批註清單中顯示剛新增的批註，並提供適當的視覺效果意見反應。 目前，請檢查 `GuestbookComments` 資料表的內容，以確認您的留言簿留言已儲存。

[圖 17] 顯示在留下兩個批註之後，`GuestbookComments` 資料表的內容。

[![您可以在 GuestbookComments 資料表中看到留言簿留言](storing-additional-user-information-vb/_static/image50.png)](storing-additional-user-information-vb/_static/image49.png)

**圖 17**：您可以在 [`GuestbookComments`] 資料表中看到 [留言簿] 批註（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image51.png)）

> [!NOTE]
> 如果使用者嘗試插入包含潛在危險標記的留言簿留言（例如 HTML – ASP.NET 將會擲回 `HttpRequestValidationException`。 若要深入瞭解此例外狀況、為什麼會擲回，以及如何允許使用者提交可能危險的值，請參閱[要求驗證技術白皮書](../../../../whitepapers/request-validation.md)。

## <a name="step-5-listing-the-existing-guestbook-comments"></a>步驟5：列出現有的留言簿留言

除了留下留言，造訪 `Guestbook.aspx` 頁面的使用者也應該能夠查看留言簿的現有留言。 若要完成這項操作，請將名為 `CommentList` 的 ListView 控制項新增至頁面底部。

> [!NOTE]
> ListView 控制項是 ASP.NET 3.5 版的新手。 其設計目的是要以可自訂且彈性的版面配置來顯示專案清單，但仍提供內建的編輯、插入、刪除、分頁和排序功能（如 GridView）。 如果您使用 ASP.NET 2.0，您將需要改為使用 DataList 或重複項控制項。 如需有關使用 ListView 的詳細資訊，請參閱[Scott Guthrie](https://weblogs.asp.net/scottgu/)的 blog 專案、 [Asp： ListView 控制項](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)和我的文章，以及[使用 ListView 控制項顯示資料](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)。

開啟 ListView 的智慧標籤，然後從 [選擇資料來源] 下拉式清單中，將控制項系結至新的資料來源。 如我們在步驟2中所見，這會啟動 [資料來源設定向導]。 選取資料庫圖示，將產生的 SqlDataSource 命名為 `CommentsDataSource`，然後按一下 [確定]。 接下來，從下拉式清單中選取 [`SecurityTutorialsConnectionString` 連接字串]，然後按 [下一步]。

在步驟2中，我們已指定要查詢的資料，方法是從下拉式清單中挑選 [`UserProfiles`] 資料表，然後選取要傳回的資料行（請參閱 [圖 9]）。 不過這一次，我們想要製作一個 SQL 語句，它不僅會拉出 `GuestbookComments`的記錄，還會提取注釋器的首頁、首頁、簽章和使用者名稱。 因此，請選取 [指定自訂 SQL 語句或預存程式] 選項按鈕，然後按 [下一步]。

這會顯示 [定義自訂語句或預存程式] 畫面。 按一下 [查詢產生器] 按鈕，以圖形方式建立查詢。 「查詢產生器」會從提示我們指定要查詢的資料表開始。 選取 [`GuestbookComments`]、[`UserProfiles`] 和 [`aspnet_Users`] 資料表，然後按一下 [確定]。 這會將這三個數據表加入至設計介面。 由於 `GuestbookComments`、`UserProfiles`和 `aspnet_Users` 資料表之間有外鍵條件約束，因此，查詢產生器會自動 `JOIN` 這些資料表。

剩下的就是指定要傳回的資料行。 從 [`GuestbookComments`] 資料表中，選取 [`Subject`]、[`Body`] 和 [`CommentDate`] 資料行;傳回 `UserProfiles` 資料表中的 `HomeTown`、`HomepageUrl`和 `Signature` 資料行;和會從 `aspnet_Users`傳回 `UserName`。 此外，將「`ORDER BY CommentDate DESC`」新增至 `SELECT` 查詢的結尾，以便先傳回最新的文章。 進行這些選擇之後，您的 [查詢產生器] 介面看起來應該會類似 [圖 18] 中的螢幕擷取畫面。

[![結構化查詢聯結 GuestbookComments、UserProfiles 和 aspnet_Users 資料表](storing-additional-user-information-vb/_static/image53.png)](storing-additional-user-information-vb/_static/image52.png)

**圖 18**：結構化查詢 `JOIN` s `GuestbookComments`、`UserProfiles`和 `aspnet_Users` 資料表（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image54.png)）

按一下 [確定] 以關閉 [查詢產生器] 視窗，並返回 [定義自訂語句或預存程式] 畫面。 按 [下一步] 前進至 [測試查詢] 畫面，您可以在其中按一下 [測試查詢] 按鈕來查看查詢結果。 當您準備好時，請按一下 [完成] 完成 [設定資料來源嚮導]。

當我們完成步驟2中的 [設定資料來源] 時，會更新相關的 DetailsView 控制項的 `Fields` 集合，以包含 `SelectCommand`所傳回之每個資料行的 BoundField。 不過，ListView 會保持不變;我們仍然需要定義其版面配置。 ListView 的版面配置可以透過其宣告式標記或其智慧標籤中的 "Configure ListView" 選項，以手動方式建立。 我通常偏好以手動方式定義標記，但使用任何最適合您的方法。

最後，我使用了 ListView 控制項的下列 `LayoutTemplate`、`ItemTemplate`和 `ItemSeparatorTemplate`：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample10.aspx)]

`LayoutTemplate` 定義由控制項發出的標記，而 `ItemTemplate` 呈現 SqlDataSource 所傳回的每個專案。 `ItemTemplate`的結果標記會放在 `LayoutTemplate`的 `itemPlaceholder` 控制項中。 除了 `itemPlaceholder`以外，`LayoutTemplate` 還包含 DataPager 控制項，它會限制 ListView 只顯示每頁10個留言簿留言（預設值），並呈現分頁介面。

我的 `ItemTemplate` 會以主旨底下的主體，顯示 `<h4>` 元素中的每個留言簿留言主題。 請注意，用來顯示本文的語法會採用 `Eval("Body")` databinding 語句所傳回的資料，將它轉換為字串，並以 `<br />` 元素取代分行符號。 需要進行這項轉換，才能顯示提交批註時所輸入的分行符號，因為 HTML 會忽略空白字元。 使用者的簽章會顯示在 [斜體] 的本文底下，後面接著使用者的主城市、首頁的連結、留言的日期和時間，以及離開留言之人員的使用者名稱。

請花點時間透過瀏覽器觀看頁面。 您應該會在這裡顯示的步驟5中，看到您新增至留言簿的留言。

[![的留言簿現在會顯示留言簿的留言](storing-additional-user-information-vb/_static/image56.png)](storing-additional-user-information-vb/_static/image55.png)

**圖 19**： `Guestbook.aspx` 現在會顯示留言簿的留言（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image57.png)）

嘗試將新留言新增至 [留言簿]。 當您按一下 [`PostCommentButton`] 按鈕時，頁面會回傳並將批註加入至資料庫，但 ListView 控制項不會更新以顯示新的批註。 這可以藉由下列其中一項來修正：

- 更新 `PostCommentButton` 按鈕的 `Click` 事件處理常式，使其在將新批註插入資料庫之後，叫用 ListView 控制項的 `DataBind()` 方法，或
- 將 ListView 控制項的 `EnableViewState` 屬性設定為 `False`。 這種方法的運作方式是，因為停用控制項的 view 狀態，所以它必須在每次回傳時重新系結至基礎資料。

本教學課程中可下載的教學課程網站說明這兩種技術。 ListView 控制項的 `EnableViewState` 屬性會 `False`，而以程式設計方式將資料重新系結到 ListView 所需的程式碼會出現在 `Click` 事件處理常式中，但已標記為批註。

> [!NOTE]
> 目前 [`AdditionalUserInfo.aspx`] 頁面可讓使用者查看和編輯其主城市、首頁和簽章設定。 更新 `AdditionalUserInfo.aspx` 以顯示已登入使用者的留言簿留言可能是很好的。 也就是說，除了檢查和修改她的資訊之外，使用者也可以造訪 `AdditionalUserInfo.aspx` 頁面，查看她在過去所做的留言簿留言。 我將這個練習留給感興趣的讀者。

## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>步驟6：自訂 CreateUserWizard 控制項以包含主城市、首頁和簽章的介面

`Guestbook.aspx` 頁面使用的 `SELECT` 查詢會使用 `INNER JOIN`，將相關記錄結合在 `GuestbookComments`、`UserProfiles`和 `aspnet_Users` 資料表之間。 如果 `UserProfiles` 中沒有記錄的使用者建立了留言簿批註，則批註不會顯示在 ListView 中，因為 `INNER JOIN` 只有 `UserProfiles` 和 `aspnet_Users`中有相符的記錄時，才會傳回 `GuestbookComments` 記錄。 如我們在步驟3中所見，如果使用者沒有記錄，`UserProfiles` 她無法在 `AdditionalUserInfo.aspx` 頁面中查看或編輯她的設定。

不用說，由於我們的設計決策，成員系統中的每個使用者帳戶都必須在 `UserProfiles` 資料表中具有相符的記錄。 我們想要的是，每當透過 CreateUserWizard 建立新的成員資格使用者帳戶時，就會將對應的記錄新增至 `UserProfiles`。

如[*建立使用者帳戶*](creating-user-accounts-vb.md)教學課程中所述，建立新的成員資格使用者帳戶之後，CreateUserWizard 控制項會引發其[`CreatedUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)。 我們可以建立這個事件的事件處理常式，取得剛建立之使用者的 UserId，然後將記錄插入 `UserProfiles` 資料表中，其中包含 `HomeTown`、`HomepageUrl`和 `Signature` 資料行的預設值。 另外，您也可以自訂 CreateUserWizard 控制項的介面來加入其他文字方塊，以提示使用者輸入這些值。

讓我們先看一下如何使用預設值，將新的資料列加入 `CreatedUser` 事件處理常式中的 `UserProfiles` 資料表。 之後，我們將瞭解如何自訂 CreateUserWizard 控制項的使用者介面，以包含其他表單欄位，以收集新使用者的主城市、首頁和簽章。

### <a name="adding-a-default-row-touserprofiles"></a>將預設資料列新增至`UserProfiles`

在[*建立使用者帳戶*](creating-user-accounts-vb.md)教學課程中，我們已將 CreateUserWizard 控制項新增至 [`Membership`] 資料夾中的 [`CreatingUserAccounts.aspx`] 頁面。 為了讓 CreateUserWizard 控制項在建立使用者帳戶時，將記錄新增至 `UserProfiles` 資料表，我們需要更新 CreateUserWizard 控制項的功能。 我們不會對 `CreatingUserAccounts.aspx` 頁面進行這些變更，而是將新的 CreateUserWizard 控制項新增至 `EnhancedCreateUserWizard.aspx` 頁面，並在該處進行本教學課程的修改。

開啟 Visual Studio 中的 [`EnhancedCreateUserWizard.aspx`] 頁面，並將 [CreateUserWizard] 控制項從 [工具箱] 拖曳至頁面上。 將 CreateUserWizard 控制項的 `ID` 屬性設定為 [`NewUserWizard`]。 如我們在[*建立使用者帳戶*](creating-user-accounts-vb.md)教學課程中所討論，CreateUserWizard 的預設使用者介面會提示訪客提供必要的資訊。 一旦提供了這項資訊，控制項就會在內部建立成員資格架構中的新使用者帳戶，而不需要撰寫一行程式碼。

CreateUserWizard 控制項會在其工作流程期間引發數個事件。 在訪客提供要求資訊並提交表單之後，CreateUserWizard 控制項一開始會引發它的[`CreatingUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)。 如果在建立程式期間發生問題，則會引發[`CreateUserError` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx);不過，如果成功建立使用者，則會引發[`CreatedUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)。 在[*建立使用者帳戶*](creating-user-accounts-vb.md)教學課程中，我們建立了 `CreatingUser` 事件的事件處理常式，以確保提供的使用者名稱不包含任何開頭或結尾的空格，而且使用者名稱不會出現在密碼中的任何位置。

為了在剛建立的使用者的 `UserProfiles` 資料表中加入資料列，我們必須建立 `CreatedUser` 事件的事件處理常式。 當 `CreatedUser` 事件引發時，已在成員資格架構中建立使用者帳戶，讓我們能夠抓取帳戶的使用者識別碼值。

建立 `NewUserWizard`的 `CreatedUser` 事件的事件處理常式，並新增下列程式碼：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample11.vb)]

上述程式碼會藉由抓取剛加入之使用者帳戶的 UserId 來做到。 這是藉由使用 `Membership.GetUser(username)` 方法來傳回特定使用者的相關資訊，然後使用 `ProviderUserKey` 屬性來取得其 UserId 來完成。 使用者在 CreateUserWizard 控制項中輸入的使用者名稱，可以透過其[`UserName` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)取得。

接下來，會從 `Web.config` 抓取連接字串，並指定 `INSERT` 語句。 系統會具現化必要的 ADO.NET 物件，並執行命令。 此程式碼會將[`DBNull`](https://msdn.microsoft.com/library/system.dbnull.aspx)實例指派給 `@HomeTown`、`@HomepageUrl`和 `@Signature` 參數，其具有插入 `NULL`、`HomeTown`和 `HomepageUrl`欄位之資料庫 `Signature` 值的效果。

透過瀏覽器造訪 [`EnhancedCreateUserWizard.aspx`] 頁面，並建立新的使用者帳戶。 這麼做之後，請返回 Visual Studio，並檢查 `aspnet_Users` 和 `UserProfiles` 資料表的內容（如 [圖 12] 所示）。 您應該會在 `aspnet_Users` 中看到新的使用者帳戶，以及對應的 `UserProfiles` 資料列（具有 `HomeTown`、`HomepageUrl`和 `Signature`的 `NULL` 值）。

[![新的使用者帳戶和 UserProfiles 記錄已新增](storing-additional-user-information-vb/_static/image59.png)](storing-additional-user-information-vb/_static/image58.png)

**圖 20**：已新增使用者帳戶和 `UserProfiles` 記錄（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image60.png)）

在訪客提供新的帳戶資訊並按一下 [建立使用者] 按鈕之後，就會建立使用者帳戶，並將資料列新增至 `UserProfiles` 資料表。 然後，CreateUserWizard 會顯示其 `CompleteWizardStep`，其中會顯示 [成功] 訊息和 [繼續] 按鈕。 按一下 [繼續] 按鈕會導致回傳，但不採取任何動作，讓使用者停留在 [`EnhancedCreateUserWizard.aspx`] 頁面上。

當您透過 CreateUserWizard 控制項的[`ContinueDestinationPageUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)來按一下 [繼續] 按鈕時，可以指定要傳送給使用者的 URL。 將 `ContinueDestinationPageUrl` 屬性設定為 "~/Membership/AdditionalUserInfo.aspx"。 這會讓新使用者 `AdditionalUserInfo.aspx`，他們可以在其中查看和更新其設定。

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>自訂 CreateUserWizard 的介面，以提示新使用者的家庭城鎮、首頁和簽章

CreateUserWizard 控制項的預設介面已足夠用於簡單的帳戶建立案例，只需要收集核心使用者帳戶資訊，例如使用者名稱、密碼和電子郵件。 但是，如果我們想要在建立帳戶時提示訪客輸入自己的城市、首頁和簽章，該怎麼辦？ 您可以自訂 CreateUserWizard 控制項的介面，以在註冊時收集其他資訊，而這項資訊可以用在 `CreatedUser` 事件處理常式中，將其他記錄插入基礎資料庫中。

CreateUserWizard 控制項會擴充 ASP.NET Wizard 控制項，這個控制項可讓網頁開發人員定義一系列的已排序 `WizardSteps`。 Wizard 控制項會呈現作用中的步驟，並提供導覽介面，讓訪客可以在這些步驟之間移動。 Wizard 控制項非常適合用來將長的工作分成幾個簡短的步驟。 如需 Wizard 控制項的詳細資訊，請參閱[使用 ASP.NET 2.0 Wizard 控制項建立逐步執行的使用者介面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)。

CreateUserWizard 控制項的預設標記會定義兩個 `WizardSteps`： `CreateUserWizardStep` 和 `CompleteWizardStep`。

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample12.aspx)]

第一個 `WizardStep`（`CreateUserWizardStep`）會轉譯提示輸入使用者名稱、密碼、電子郵件等的介面。 在造訪者提供此資訊並按一下 [建立使用者] 之後，就會顯示 [`CompleteWizardStep`]，其中會顯示 [成功] 訊息和 [繼續] 按鈕。

若要自訂 CreateUserWizard 控制項的介面以包含其他表單欄位，我們可以：

- <strong>建立一或多個新</strong>的<strong>`WizardStep`</strong> <strong>，以包含額外的使用者介面元素</strong>。 若要將新的 `WizardStep` 新增至 CreateUserWizard，請按一下智慧標籤中的 [新增/移除 `WizardStep` s] 連結，以啟動 [`WizardStep` 集合編輯器]。 您可以從該處新增、移除或重新排序嚮導中的步驟。 這是我們將在本教學課程中使用的方法。

- <strong>將</strong><strong>`CreateUserWizardStep`</strong>轉換<strong>成可編輯</strong>的<strong>`WizardStep`</strong> <strong>。</strong> 這會將 `CreateUserWizardStep` 取代為對等的 `WizardStep`，其標記會定義符合 `CreateUserWizardStep`的使用者介面。 藉由將 `CreateUserWizardStep` 轉換成 `WizardStep`，我們可以重新調整控制項的位置，或將其他使用者介面專案加入此步驟。 若要將 `CreateUserWizardStep` 或 `CompleteWizardStep` 轉換為可編輯的 `WizardStep`，請按一下控制項智慧標籤中的 [自訂建立使用者步驟] 或 [自訂完整步驟] 連結。

- **使用上述兩個選項的某種組合。**

要記住的一個重要事項，就是當從其 `CreateUserWizardStep`中按一下 [建立使用者] 按鈕時，CreateUserWizard 控制項會執行其使用者帳戶建立程式。 `CreateUserWizardStep` 之後是否有其他 `WizardStep`，並不重要。

將自訂 `WizardStep` 新增至 CreateUserWizard 控制項以收集額外的使用者輸入時，可以將自訂 `WizardStep` 放在 `CreateUserWizardStep`之前或之後。 如果在 `CreateUserWizardStep` 之前，則會從自訂 `WizardStep` 收集的額外使用者輸入提供給 `CreatedUser` 事件處理常式。 不過，如果自訂的 `WizardStep` 在 `CreateUserWizardStep` 之後，則在自訂 `WizardStep` 顯示時，即已建立新的使用者帳戶，並已引發 `CreatedUser` 事件。

[圖 21] 顯示在 `CreateUserWizardStep`之前新增的 `WizardStep` 工作流程。 由於 `CreatedUser` 事件引發後，已收集額外的使用者資訊，因此我們只需要更新 `CreatedUser` 事件處理常式來抓取這些輸入，並將其用於 `INSERT` 語句的參數值（而非 `DBNull.Value`）。

[當其他 WizardStep 在 CreateUserWizardStep 之前，![CreateUserWizard 工作流程](storing-additional-user-information-vb/_static/image62.png)](storing-additional-user-information-vb/_static/image61.png)

**圖 21**：其他 `WizardStep` 在 `CreateUserWizardStep` 之前的 CreateUserWizard 工作流程（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image63.png)）

不過，如果自訂 `WizardStep` 放在 `CreateUserWizardStep`*之後*，則建立使用者帳戶程式會在使用者有機會輸入自己的「城市」、「首頁」或「簽章」之前進行。 在這種情況下，您必須在建立使用者帳戶之後，將此額外資訊插入資料庫中，如 [圖 22] 所示。

[當 CreateUserWizardStep 之後有其他 WizardStep 時，![CreateUserWizard 工作流程](storing-additional-user-information-vb/_static/image65.png)](storing-additional-user-information-vb/_static/image64.png)

**圖 22**：其他 `WizardStep` 在 `CreateUserWizardStep` 之後的 CreateUserWizard 工作流程（[按一下以觀看完整大小的影像](storing-additional-user-information-vb/_static/image66.png)）

[圖 22] 所示的工作流程會等到步驟2完成後，才將記錄插入 `UserProfiles` 資料表中。 不過，如果造訪者在步驟1之後關閉她的瀏覽器，我們就會到達建立使用者帳戶的狀態，但不會將任何記錄新增至 `UserProfiles`。 其中一個因應措施是將具有 `NULL` 或預設值的記錄插入 `CreatedUser` 事件處理常式中的 `UserProfiles` （在步驟1之後引發），然後在步驟2完成後更新此記錄。 這可確保即使使用者在中途結束註冊程式，也會為使用者帳戶新增 `UserProfiles` 記錄。

在本教學課程中，我們將建立在 `CreateUserWizardStep` 之後，但在 `CompleteWizardStep`之前發生的新 `WizardStep`。 讓我們先取得並設定 WizardStep，然後再查看程式碼。

從 CreateUserWizard 控制項的智慧標籤中，選取 [新增/移除 `WizardStep` s]，這會顯示 [`WizardStep` 集合編輯器] 對話方塊。 新增 `WizardStep`，並將其 `ID` 設定為 [`UserSettings`]、將其 [`Title`] 設為 [您的設定]，並將其 `StepType` 為 [`Step`]。 然後將它放置在 `CreateUserWizardStep` （「註冊您的新帳戶」）和 `CompleteWizardStep` （「完成」）之前，如 [圖 23] 所示。

[![將新的 WizardStep 新增至 CreateUserWizard 控制項](storing-additional-user-information-vb/_static/image68.png)](storing-additional-user-information-vb/_static/image67.png)

**圖 23**：將新的 `WizardStep` 新增至 CreateUserWizard 控制項（[按一下以查看完整大小的影像](storing-additional-user-information-vb/_static/image69.png)）

按一下 [確定] 關閉 [`WizardStep` 集合編輯器] 對話方塊。 新的 `WizardStep` 是由 CreateUserWizard 控制項的已更新宣告式標記所總合：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample13.aspx)]

請注意新的 `<asp:WizardStep>` 元素。 我們需要在此新增使用者介面，以收集新使用者的家庭城鎮、首頁和簽章。 您可以使用宣告式語法或透過設計工具來輸入此內容。 若要使用設計工具，請從智慧標籤的下拉式清單中選取 [您的設定] 步驟，以在設計工具中查看步驟。

> [!NOTE]
> 透過智慧標籤的下拉式清單選取一個步驟，即可更新 CreateUserWizard 控制項的[`ActiveStepIndex` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx)，以指定起始步驟的索引。 因此，如果您使用此下拉式清單來編輯設計工具中的 [設定] 步驟，請務必將其設定回 [註冊新帳戶]，以便在使用者第一次造訪 `EnhancedCreateUserWizard.aspx` 頁面時顯示此步驟。

在「您的設定」步驟內建立使用者介面，其中包含三個名為 `HomeTown`、`HomepageUrl`和 `Signature`的 TextBox 控制項。 在建立此介面之後，CreateUserWizard 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample14.aspx)]

請繼續流覽此頁面，並建立新的使用者帳戶，並指定家庭城鎮、首頁和簽章的值。 完成 `CreateUserWizardStep` 之後，就會在成員資格架構中建立使用者帳戶，並執行 `CreatedUser` 事件處理常式，這會將新的資料列加入 `UserProfiles`中，但會將資料庫 `NULL` 值用於 `HomeTown`、`HomepageUrl`和 `Signature`。 您不會使用針對 [首頁]、[首頁] 和 [簽章] 輸入的值。 最終結果是新的使用者帳戶，其中包含尚未指定 `HomeTown`、`HomepageUrl`和 `Signature` 欄位的 `UserProfiles` 記錄。

我們需要在「您的設定」步驟之後執行程式碼，以取得使用者所輸入的主城市、honepage 和簽章值，並更新適當的 `UserProfiles` 記錄。 每次使用者在 Wizard 控制項的步驟之間移動時，就會引發 Wizard 的[`ActiveStepChanged` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx)。 我們可以建立此事件的事件處理常式，並在「您的設定」步驟完成時更新 `UserProfiles` 資料表。

為 CreateUserWizard 的 `ActiveStepChanged` 事件新增事件處理常式，並加入下列程式碼：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample15.vb)]

上述程式碼一開始會先判斷我們是否剛到達「完成」步驟。 因為「完成」步驟會緊接在「您的設定」步驟之後，所以當訪客到達「完成」步驟時，表示她剛完成「您的設定」步驟。

在這種情況下，我們需要以程式設計方式參考 `UserSettings WizardStep`內的 TextBox 控制項。 首先，使用 `FindControl` 方法，以程式設計方式參考 `UserSettings WizardStep`，然後再從 `WizardStep`內參照文字方塊，來完成這項作業。 一旦參考文字方塊之後，我們就可以開始執行 `UPDATE` 語句。 `UPDATE` 語句的參數數目與 `CreatedUser` 事件處理常式中的 `INSERT` 語句相同，但在此，我們會使用使用者所提供的主城市、首頁和簽章值。

有了這個事件處理常式之後，請透過瀏覽器造訪 [`EnhancedCreateUserWizard.aspx`] 頁面，並建立新的使用者帳戶，指定家庭城鎮、首頁和簽章的值。 建立新帳戶之後，您應該將其重新導向至 [`AdditionalUserInfo.aspx`] 頁面，其中會顯示剛輸入的 [首頁]、[首頁] 和 [簽章] 資訊。

> [!NOTE]
> 我們的網站目前有兩個頁面，可供造訪者建立新的帳戶： `CreatingUserAccounts.aspx` 和 `EnhancedCreateUserWizard.aspx`。 網站的 [網站地圖] 和 [登入] 頁面會指向 [`CreatingUserAccounts.aspx`] 頁面，但 [`CreatingUserAccounts.aspx`] 頁面不會提示使用者輸入其主城市、首頁和簽章資訊，也不會將對應的資料列新增至 `UserProfiles`。 因此，請更新 `CreatingUserAccounts.aspx` 頁面，讓它提供這項功能，或將網站地圖和登入頁面更新為參考 `EnhancedCreateUserWizard.aspx` 而不是 `CreatingUserAccounts.aspx`。 如果您選擇第二個選項，請務必更新 `Membership` 資料夾的 `Web.config` 檔案，以便允許匿名使用者存取 `EnhancedCreateUserWizard.aspx` 頁面。

## <a name="summary"></a>總結

在本教學課程中，我們探討了與成員資格架構中的使用者帳戶相關的資料模型化技術。 特別是，我們探討了與使用者帳戶共用一對多關聯性的模型實體，以及共用一對一關聯性的資料。 此外，我們也看到了這些相關資訊的顯示、插入和更新方式，其中有一些範例使用 SqlDataSource 控制項，其他則使用 ADO.NET 程式碼。

本教學課程會完成使用者帳戶的外觀。 從下一個教學課程開始，我們會將注意力轉向角色。 在接下來的幾個教學課程中，我們將探討角色架構，瞭解如何建立新的角色、如何將角色指派給使用者、如何判斷使用者所屬的角色，以及如何套用以角色為基礎的授權。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [存取和更新 ASP.NET 2.0 中的資料](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2.0 Wizard 控制項](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [使用 ASP.NET 2.0 Wizard 控制項建立逐步執行的使用者介面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [建立自訂資料來源控制項參數](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [自訂 CreateUserWizard 控制項](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [DetailsView 控制項快速入門](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [使用 ListView 控制項顯示資料](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [剖析 ASP.NET 2.0 中的驗證控制項](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [編輯插入和刪除資料](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [ASP.NET 中的表單驗證](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [正在搜集自訂使用者註冊資訊](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2.0 中的設定檔](http://www.odetocode.com/Articles/440.aspx)
- [Asp： ListView 控制項](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [使用者設定檔快速入門](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一篇](user-based-authorization-vb.md)
