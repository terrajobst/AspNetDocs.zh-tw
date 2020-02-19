---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: 將現有的網站從 SQL 成員資格遷移至 ASP.NET Identity-ASP.NET 4。x
author: Rick-Anderson
description: 本教學課程說明將現有 web 應用程式（使用 SQL 成員資格建立的使用者和角色資料）遷移至新的 ASP.NET Identity s 。
ms.author: riande
ms.date: 12/19/2014
ms.custom: seoapril2019
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 633229cc4311d151121bf6a91b9fa8aeecca1197
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456149"
---
# <a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>將現有的網站從 SQL 成員資格移轉至 ASP.NET Identity

由[Rick Anderson](https://twitter.com/RickAndMSFT)、 [Suhas Joshi](https://github.com/suhasj)

> 本教學課程說明將現有 web 應用程式（使用 SQL 成員資格建立的使用者和角色資料）遷移至新 ASP.NET Identity 系統的步驟。 此方法牽涉到將現有的資料庫架構變更為 ASP.NET Identity 所需的架構，並將舊的/新類別連結到它。 在您採用這種方法之後，一旦您的資料庫移轉之後，未來的身分識別更新將可輕鬆地處理。

在本教學課程中，我們將採用使用 Visual Studio 2010 建立的 web 應用程式範本（Web form）來建立使用者和角色資料。 接著，我們將使用 SQL 腳本，將現有的資料庫移轉至身分識別系統所需的資料表。 接下來，我們將安裝必要的 NuGet 套件，並新增使用身分識別系統來進行成員資格管理的新帳戶管理頁面。 作為遷移的測試，使用 SQL 成員資格建立的使用者應該能夠登入，而新的使用者應該能夠註冊。 您可以在[這裡](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/)找到完整的範例。 另請參閱[從 ASP.NET 成員資格遷移至 ASP.NET Identity](http://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity.html)。

## <a name="getting-started"></a>開始使用

### <a name="creating-an-application-with-sql-membership"></a>建立具有 SQL 成員資格的應用程式

1. 我們必須從使用 SQL 成員資格並具有使用者和角色資料的現有應用程式開始。 基於本文的目的，讓我們在 Visual Studio 2010 中建立 web 應用程式。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. 使用 ASP.NET 設定工具建立2個使用者： **oldAdminUser**和**oldUser。**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. 建立名為 Admin 的角色，並將 ' oldAdminUser ' 新增為該角色中的使用者。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. 使用 default.aspx 建立網站的 Admin 區段。 將 web.config 檔案中的 authorization 標記設定為僅允許系統管理員角色中的使用者存取。 您可以在這裡找到詳細資訊[https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. 在伺服器總管中查看資料庫，以瞭解 SQL 成員資格系統所建立的資料表。 使用者登入資料會儲存在 aspnet\_Users 和 aspnet\_成員資格資料表中，而角色資料則儲存在 aspnet\_Roles 資料表中。 哪些使用者在 aspnet\_UsersInRoles 資料表中儲存哪些角色的相關資訊。 對於基本成員資格管理而言，將上述資料表中的資訊移植到 ASP.NET Identity 系統就已足夠。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>遷移至 Visual Studio 2013

1. 安裝 Web 或 Visual Studio 2013 的 Visual Studio Express 2013，以及[最新的更新](https://www.microsoft.com/download/details.aspx?id=44921)。
2. 在您安裝的 Visual Studio 版本中開啟上述專案。 如果電腦上未安裝 SQL Server Express，當您開啟專案時就會顯示提示，因為連接字串會使用 SQL Express。 您可以選擇安裝 SQL Express，或將連接字串變更為 LocalDb 以進行解決。 在本文中，我們會將它變更為 LocalDb。
3. 開啟 web.config 並從變更連接字串。SQLExpress 至（LocalDb）11.0。 請從連接字串中移除 ' User Instance = true '。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. 開啟伺服器總管，並確認可以觀察資料表架構和資料。
5. ASP.NET Identity 系統適用于 framework 4.5 或更高版本。 將應用程式的目標重定為4.5 或更高版本。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    建立專案，以確認沒有任何錯誤。

### <a name="installing-the-nuget-packages"></a>安裝 Nuget 套件

1. 在方案總管中，以滑鼠右鍵按一下專案 &gt;**管理 NuGet 封裝**。 在搜尋方塊中，輸入「Asp.net Identity」。 在結果清單中選取套件，然後按一下 [安裝]。 按一下 [我接受] 按鈕，以接受授權合約。 請注意，此封裝將會安裝相依性套件： EntityFramework 和 Microsoft ASP.NET 身分識別核心。 同樣地，安裝下列套件（如果您不想啟用 OAuth 登入，請略過最後4個 OWIN 套件）：

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Owin. 安全性 Facebook
   - Owin。 Google
   - Owin. Security. MicrosoftAccount
   - Owin. Security. Twitter

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>將資料庫移轉至新的身分識別系統

下一步是將現有的資料庫移轉至 ASP.NET Identity 系統所需的架構。 為了達到此目的，我們會執行 SQL 腳本，其中包含一組命令來建立新的資料表，並將現有的使用者資訊遷移至新的資料表。 您可以在[這裡](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/Migrations.sql)找到腳本檔案。

此腳本檔案僅適用于此範例。 如果自訂或修改使用 SQL 成員資格所建立之資料表的架構，則必須據此變更腳本。

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>如何產生用於架構遷移的 SQL 腳本

若要讓 ASP.NET Identity 類別與現有使用者的資料一起使用，我們需要將資料庫架構遷移至 ASP.NET Identity 所需的程式。 我們可以藉由加入新的資料表，並將現有的資訊複製到這些資料表來達到這個目的。 根據預設，ASP.NET Identity 會使用 EntityFramework 將身分識別模型類別對應回資料庫，以儲存/抓取資訊。 這些模型類別會執行定義使用者和角色物件的核心身分識別介面。 資料庫中的資料表和資料行是以這些模型類別為基礎。 Identity v 2.1.0 中的 EntityFramework 模型類別及其屬性如下所定義

| **IdentityUser** | **型別** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| Id | 字串 | Id | RoleId | ProviderKey | Id |
| 使用者名稱 | 字串 | 名稱 | UserId | UserId | ClaimType |
| PasswordHash | 字串 |  |  | LoginProvider | ClaimValue |
| SecurityStamp | 字串 |  |  |  | 使用者\_識別碼 |
| 電子郵件 | 字串 |  |  |  |  |
| EmailConfirmed | bool |  |  |  |  |
| PhoneNumber | 字串 |  |  |  |  |
| PhoneNumberConfirmed | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | Datetime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

針對每個模型，我們都必須具有對應至屬性之資料行的資料表。 類別和資料表之間的對應是在 `IdentityDBContext`的 `OnModelCreating` 方法中定義。 這就是所謂的設定 Fluent API 方法，您可以在[這裡](https://msdn.microsoft.com/data/jj591617.aspx)找到詳細資訊。 類別的設定如下所述

| **類別** | **Table** | **主要金鑰** | **外鍵** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | Id |  |
| IdentityRole | AspnetRoles | Id |  |
| IdentityUserRole | AspnetUserRole | UserId + RoleId | 使用者\_識別碼-&gt;AspnetUsers RoleId-&gt;AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | UserId-&gt;AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | Id | 使用者\_識別碼-&gt;AspnetUsers |

有了這種資訊，我們就可以建立 SQL 語句來建立新的資料表。 我們可以個別寫入每個語句，或使用 EntityFramework PowerShell 命令來產生整個腳本，然後我們可以視需要進行編輯。 若要這樣做，請在 VS 中，從 [**視圖**] 或 [**工具**] 功能表開啟 [**套件管理員主控台**]

- 執行命令「啟用-遷移」以啟用 EntityFramework 遷移。
- 執行命令「新增-遷移初始」，以建立在/VB. 中C#建立資料庫的初始安裝程式碼
- 最後一個步驟是執行「更新資料庫-腳本」命令，以根據模型類別產生 SQL 腳本。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

這個資料庫產生腳本可用來做為起點，我們將會在此開始進行其他變更，以加入新的資料行並複製資料。 這樣做的優點是，我們會產生 `_MigrationHistory` 資料表，當模型類別針對未來版本的身分識別版本變更時，EntityFramework 會使用它來修改資料庫架構。

除了身分識別使用者模型類別中的其他屬性（也就是電子郵件、密碼嘗試、上次登入日期、上次的鎖定日期等等）之外，SQL 成員資格使用者資訊還有其他內容。這是有用的資訊，我們想要將它帶入身分識別系統。 將其他屬性加入至使用者模型，並將其對應回資料庫中的資料表資料行，即可完成這項作業。 我們可以藉由加入子類別來分類 `IdentityUser` 模型來執行這項操作。 我們可以在建立資料表時，將屬性新增至這個自訂類別，並編輯 SQL 腳本來加入對應的資料行。 此類別的程式碼會在文章中進一步說明。 新增新屬性之後，用來建立 `AspnetUsers` 資料表的 SQL 腳本會是

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

接下來，我們需要將 SQL 成員資格資料庫中的現有資訊複製到新加入的資料表以供識別。 這可以透過 SQL 來完成，方法是直接將資料從一個資料表複製到另一個。 若要將資料加入至資料表的資料列中，我們會使用 `INSERT INTO [Table]` 結構。 若要從另一個資料表複製，我們可以搭配使用 `INSERT INTO` 語句與 `SELECT` 語句。 若要取得所有使用者資訊，我們需要查詢*aspnet\_使用者*和*Aspnet\_成員資格*資料表，並將資料複製到*AspNetUsers*資料表。 我們會使用 `INSERT INTO` 和 `SELECT` 以及 `JOIN` 和 `LEFT OUTER JOIN` 語句。 如需在資料表之間查詢和複製資料的詳細資訊，請參閱[此](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx)連結。 此外，AspnetUserLogins 和 AspnetUserClaims 資料表的開頭都是空的，因為 SQL 成員資格中預設不會對應到這個資訊。 唯一複製的資訊是針對使用者和角色。 針對在先前步驟中建立的專案，將資訊複製到 [使用者] 資料表的 SQL 查詢會是

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

在上述 SQL 語句中，從*aspnet\_使用者*和*Aspnet\_成員資格*資料表的每個使用者的相關資訊，都會複製到*AspnetUsers*資料表的資料行中。 此處所做的唯一修改是當我們複製密碼時。 因為 SQL 成員資格中的密碼加密演算法使用了 ' PasswordSalt ' 和 ' PasswordFormat '，所以我們也會將它連同雜湊密碼一起複製，以便用來依身分識別解密密碼。 當連結自訂密碼 hasher 時，會在文章中進一步說明。

此腳本檔案僅適用于此範例。 對於具有其他資料表的應用程式，開發人員可以遵循類似的方法，在使用者模型類別上加入其他屬性，並將其對應至 AspnetUsers 資料表中的資料行。 若要執行腳本，

1. 開啟 [伺服器總管]。 展開 [Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception] 連接以顯示資料表。 以滑鼠右鍵按一下 [資料表] 節點，然後選取 [新增查詢] 選項

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. 在查詢視窗中，複製並貼上所有 SQL 腳本，並從 sql 檔案。 藉由按下 [執行] 箭號按鈕來執行腳本檔案。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    重新整理 [伺服器總管] 視窗。 資料庫中會建立五個新資料表。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    以下是 SQL 成員資格資料表中的資訊對應到新身分識別系統的方式。

    aspnet\_角色--&gt; AspNetRoles

    asp\_netUsers 和 asp\_netMembership--&gt; AspNetUsers

    aspnet\_UserInRoles--&gt; [Aspnetuserroles]

    如上一節所述，AspNetUserClaims 和 AspNetUserLogins 資料表是空的。 AspNetUser 資料表中的 ' 鑒別子欄位應符合定義為下一個步驟的模型類別名稱。 此外，PasswordHash 資料行的格式為「加密的密碼 | 密碼 salt | 密碼格式」。 這可讓您使用特殊的 SQL 成員資格加密邏輯，讓您可以重複使用舊密碼。 本文稍後會說明。

### <a name="creating-models-and-membership-pages"></a>建立模型和成員資格頁面

如先前所述，識別功能預設會使用 Entity Framework 來與資料庫通訊，以儲存帳戶資訊。 若要使用資料表中的現有資料，我們必須建立對應回資料表的模型類別，並在身分識別系統中連結它們。 在身分識別合約中，模型類別應執行在 Identity. Core dll 中定義的介面，或可以擴充 EntityFramework 中的現有介面。

在我們的範例中，AspNetRoles、AspNetUserClaims、AspNetLogins 和 AspNetUserRole 資料表的資料行與身分識別系統的現有執行方式類似。 因此，我們可以重複使用現有的類別來對應至這些資料表。 AspNetUser 資料表有一些額外的資料行，這些資料行會用來儲存 SQL 成員資格資料表的其他資訊。 這可以藉由建立模型類別來進行對應，以擴充現有的 ' IdentityUser ' 實作為，並加入其他屬性。

1. 在專案中建立 [模型] 資料夾，並新增類別 [使用者]。 類別的名稱應該與 ' AspnetUsers ' 資料表的 ' 鑒別子資料行中新增的資料相符。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    User 類別應該擴充*EntityFramework* dll 中找到的 IdentityUser 類別。 在類別中宣告對應回 AspNetUser 資料行的屬性。 屬性 ID、Username、PasswordHash 和 SecurityStamp 定義于 IdentityUser 中，因此會省略。 以下是具有所有屬性之 User 類別的程式碼

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. 需要 Entity Framework DbCoNtext 類別，才能將模型中的資料保存回資料表，並從資料表中取出資料來填入模型。 *EntityFramework* dll 會定義 IdentityDbCoNtext 類別，它會與識別資料表互動以取得及儲存資訊。 IdentityDbCoNtext&lt;tuser&gt; 接受 ' TUser ' 類別，它可以是任何擴充 IdentityUser 類別的類別。

    建立新的類別 [ApplicationdbcoNtext]，以在 [模型] 資料夾底下擴充 IdentityDbCoNtext，傳入在步驟1中建立的「使用者」類別

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. 新身分識別系統中的使用者管理是使用*EntityFramework* dll 中定義的 UserManager&lt;tuser&gt; 類別來完成。 我們需要建立擴充 UserManager 的自訂類別，傳入在步驟1中建立的「使用者」類別。

    在 [模型] 資料夾中，建立擴充 UserManager&lt;使用者的新類別 UserManager&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. 應用程式使用者的密碼會經過加密並儲存在資料庫中。 SQL 成員資格中使用的密碼編譯演算法與新身分識別系統中的不同。 若要重複使用舊密碼，我們需要在舊使用者使用 SQL 成員資格演算法登入時，選擇性地解密密碼，同時在新使用者的身分識別中使用加密演算法。

    UserManager 類別具有屬性 ' 並且 '，它會儲存實作為 ' IPasswordHasher ' 介面之類別的實例。 這會在使用者驗證交易期間用來加密/解密密碼。 在步驟3中定義的 UserManager 類別中，建立新的類別 SQLPasswordHasher，並複製下列程式碼。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    藉由匯入 System.web 和 System.web 命名空間來解決編譯錯誤。

    EncodePassword 方法會根據預設 SQL 成員資格加密執行來加密密碼。 這是從 System.web dll 取得。 如果舊的應用程式使用自訂的執行，則應該在此反映。 我們需要定義兩個其他的方法*HashPassword*和*VerifyHashedPassword* ，以使用*EncodePassword*方法來雜湊指定的密碼，或以資料庫中現有的來驗證純文字密碼。

    SQL 成員資格系統使用 PasswordHash、PasswordSalt 和 PasswordFormat 來雜湊使用者註冊或變更其密碼時所輸入的密碼。 在遷移期間，所有三個欄位都會儲存在 AspNetUser 資料表的 PasswordHash 資料行中，並以 ' | ' 字元分隔。 當使用者登入且密碼具有這些欄位時，我們會使用 SQL 成員資格加密來檢查密碼;否則，我們會使用身分識別系統的預設加密來驗證密碼。 如此一來，舊的使用者就不需要在應用程式遷移之後變更其密碼。
5. 宣告 UserManager 類別的函式，並將其當做 SQLPasswordHasher 傳遞至函式中的屬性。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>建立新的帳戶管理頁面

遷移的下一個步驟是新增可讓使用者註冊和登入的帳戶管理頁面。 SQL 成員資格中的舊帳戶頁面會使用無法搭配新身分識別系統的控制項。 若要加入新的使用者管理頁面，請遵循此連結的教學課程[https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)從「新增 Web 表單以將使用者註冊到您的應用程式」步驟開始，因為我們已建立專案並新增 NuGet 套件。

我們需要對範例進行一些變更，才能使用我們在這裡的專案。

- Register.aspx.cs 和 Login.aspx.cs 程式碼後置類別會使用身分識別套件中的 `UserManager` 來建立使用者。 針對此範例，請遵循先前所述的步驟，使用 [模型] 資料夾中加入的 UserManager。
- 在 Register.aspx.cs 和 Login.aspx.cs 程式碼後置類別中，使用建立的使用者類別，而不是 IdentityUser。 這會在我們的自訂使用者類別中攔截到身分識別系統。
- 可以略過建立資料庫的元件。
- 開發人員必須設定新使用者的 ApplicationId，使其符合目前的應用程式識別碼。 這可以藉由查詢此應用程式的 ApplicationId 來完成，方法是在 Register.aspx.cs 類別中建立使用者物件，並在建立使用者之前先設定它。

    範例：

    在 [Register.aspx.cs] 頁面中定義方法，以查詢 aspnet\_應用程式資料表，並根據應用程式名稱取得應用程式識別碼

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    現在請在 user 物件上設定這個

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

使用舊的使用者名稱和密碼來登入現有的使用者。 使用 [註冊] 頁面建立新的使用者。 也請確認使用者是否如預期般在角色中。

移植到身分識別系統可協助使用者將開放式驗證（OAuth）新增至應用程式。 請參閱[這裡](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/)已啟用 OAuth 的範例。

## <a name="next-steps"></a>後續步驟

在本教學課程中，我們示範了如何將 SQL 成員資格的使用者移植到 ASP.NET Identity，但我們並未移植設定檔資料。 在下一個教學課程中，我們將探討如何將來自 SQL 成員資格的設定檔資料移植到新的身分識別系統。

您可以在本文底部留下意見反應。

*感謝 Tom 作者: dykstra 和 Rick Anderson 來審視文章。*
