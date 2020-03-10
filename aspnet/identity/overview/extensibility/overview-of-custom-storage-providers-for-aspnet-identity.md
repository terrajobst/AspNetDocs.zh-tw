---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: ASP.NET Identity 的自訂存放裝置提供者-ASP.NET 4.x 的總覽
author: Rick-Anderson
description: ASP.NET Identity 是可延伸的系統，可讓您建立自己的儲存提供者，並將它插入您的應用程式，而不需要重新運作 & 。
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 21baedf6285b411f89627df9ca25d47a2a42e387
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584410"
---
# <a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity 的自訂儲存體提供者概觀

由[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity 是可延伸的系統，可讓您建立自己的儲存提供者，並將它插入您的應用程式，而不需要重新運作應用程式。 本主題說明如何建立 ASP.NET Identity 的自訂存放裝置提供者。 其中涵蓋建立您自己的儲存區提供者的重要概念，但不是執行自訂儲存提供者的逐步解說。
> 
> 如需執行自訂存放裝置提供者的範例，請參閱[執行自訂 MySQL ASP.NET Identity 存放裝置提供者](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)。
> 
> 本主題已針對 ASP.NET Identity 2.0 進行更新。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Update 2 的 Visual Studio 2013
> - ASP.NET Identity 2

## <a name="introduction"></a>簡介

根據預設，ASP.NET Identity 系統會將使用者資訊儲存在 SQL Server 資料庫中，並使用 Entity Framework Code First 來建立資料庫。 對於許多應用程式而言，這種方法很適合。 不過，您可能會想要使用不同類型的持續性機制（例如 Azure 表格儲存體），或者您可能已經有資料庫資料表，其結構與預設的執行方式不同。 不論是哪一種情況，您都可以為儲存機制撰寫自訂的提供者，並將該提供者插入您的應用程式中。

根據預設，許多 Visual Studio 2013 範本都會包含 ASP.NET Identity。 您可以透過[Microsoft AspNet Identity EntityFramework NuGet 套件](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)取得 ASP.NET Identity 的更新。

本主題包含下列章節：

- [瞭解架構](#architecture)
- [瞭解儲存的資料](#data)
- [建立資料存取層](#dal)
- [自訂使用者類別](#user)
- [自訂使用者存放區](#userstore)
- [自訂角色類別](#role)
- [自訂角色存放區](#rolestore)
- [重新設定應用程式以使用新的存放裝置提供者](#reconfigure)
- [自訂存放裝置提供者的其他執行方式](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>瞭解架構

ASP.NET Identity 是由稱為「經理」和「商店」的類別所組成。 管理員是高階類別，應用程式開發人員在 ASP.NET Identity 系統中用來執行作業，例如建立使用者。 存放區是較低層級的類別，可指定實體（例如使用者和角色）的保存方式。 存放區會與持續性機制緊密結合，但管理員會與存放區分離，這表示您可以取代持續性機制，而不會中斷整個應用程式。

下圖顯示您的 web 應用程式如何與管理員互動，以及儲存與資料存取層的互動。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

若要為 ASP.NET Identity 建立自訂的儲存提供者，您必須建立資料來源、資料存取層，以及與此資料存取層互動的存放區類別。 您可以繼續使用相同的管理員 Api 來執行使用者的資料作業，但現在會將資料儲存到不同的儲存系統。

您不需要自訂管理員類別，因為當建立 UserManager 或 RoleManager 的新實例時，您會提供使用者類別的類型，並傳遞 store 類別的實例做為引數。 這種方法可讓您將自訂類別插入現有的結構中。 您會在[重新設定應用程式以使用新的存放裝置提供者](#reconfigure)一節中，瞭解如何使用自訂的存放區類別來具現化 UserManager 和 RoleManager

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>瞭解儲存的資料

若要執行自訂的儲存提供者，您必須瞭解與 ASP.NET Identity 搭配使用的資料類型，並決定與您的應用程式相關的功能。

| 資料 | 說明 |
| --- | --- |
| 使用者 | 網站的已註冊使用者。 包含使用者識別碼和使用者名稱。 如果使用者使用您網站特有的認證登入（而不是使用來自外部網站的認證，例如 Facebook），則可能會包含雜湊的密碼，以及用來指出使用者認證是否有任何變更的安全性戳記。 也可能包括電子郵件地址、電話號碼、是否已啟用雙因素驗證、目前的失敗登入次數，以及帳戶是否已鎖定。 |
| 使用者宣告 | 使用者的一組語句（或宣告），代表使用者的身分識別。 可以啟用使用者身分識別的更大運算式，而不是透過角色來達成。 |
| 使用者登入 | 要在使用者登入時使用的外部驗證提供者（例如 Facebook）的相關資訊。 |
| 角色 | 網站的授權群組。 包含角色識別碼和角色名稱（例如 "Admin" 或 "Employee"）。 |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>建立資料存取層

本主題假設您熟悉要使用的持續性機制，以及如何建立該機制的實體。 本主題不提供如何建立存放庫或資料存取類別的詳細資料;相反地，它會針對您在使用 ASP.NET Identity 時所需進行的設計決策提供一些建議。

在設計自訂存放區提供者的存放庫時，您有很多自由。 您只需要為您想要在應用程式中使用的功能建立存放庫。 例如，如果您未在應用程式中使用角色，則不需要建立角色或使用者角色的儲存體。 您的技術和現有的基礎結構可能需要的結構與 ASP.NET Identity 的預設執行方式非常不同。 在您的資料存取層中，您會提供邏輯來處理您的存放庫結構。

如需 ASP.NET Identity 2.0 的資料存放庫的 MySQL 執行，請參閱[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)。

在資料存取層中，您會提供將資料從 ASP.NET Identity 儲存至資料來源的邏輯。 您自訂的儲存提供者的資料存取層可能包含下列用來儲存使用者和角色資訊的類別。

| 類別 | 說明 | 範例 |
| --- | --- | --- |
| 內容 | 封裝資訊，以連接到您的持續性機制並執行查詢。 此類別是資料存取層的核心。 其他資料類別則需要這個類別的實例，才能執行其作業。 您也會使用此類別的實例來初始化您的存放區類別。 | [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| 使用者儲存體 | 儲存並抓取使用者資訊（例如使用者名稱和密碼雜湊）。 | [UserTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| 角色儲存體 | 儲存並抓取角色資訊（例如角色名稱）。 | [RoleTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| UserClaims 儲存體 | 儲存並抓取使用者宣告資訊（例如宣告類型和值）。 | [UserClaimsTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins 儲存體 | 儲存並抓取使用者登入資訊（例如外部驗證提供者）。 | [UserLoginsTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| 使用者角色存放裝置 | 儲存並抓取使用者所指派的角色。 | [UserRoleTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

同樣地，您只需要實作為您想要在應用程式中使用的類別。

在資料存取類別中，您會提供程式碼來執行特定持續性機制的資料作業。 例如，在 MySQL 的執行中，UserTable 類別包含將新記錄插入使用者資料庫資料表的方法。 名為 `_database` 的變數是 MySQLDatabase 類別的實例。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

建立資料存取類別之後，您必須建立在資料存取層中呼叫特定方法的存放區類別。

<a id="user"></a>
## <a name="customize-the-user-class"></a>自訂使用者類別

在執行您自己的儲存區提供者時，您必須建立一個與[EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空間中的[IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx)類別相等的使用者類別：

下圖顯示您必須建立的 IdentityUser 類別，以及要在此類別中執行的介面。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

[IUser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)介面會定義 UserManager 在執行要求的作業時嘗試呼叫的屬性。 介面包含兩個屬性：識別碼和使用者名稱。 [IUser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)介面可讓您透過泛型**TKey**參數指定使用者的金鑰型別。 Id 屬性的類型符合 TKey 參數的值。

當您想要使用字串值做為索引鍵時，身分識別架構也會提供[IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx)介面（不含泛型參數）。

IdentityUser 類別會實 IUser，並包含網站上使用者的任何其他屬性或函式。 下列範例顯示使用整數做為索引鍵的 IdentityUser 類別。 [識別碼] 欄位會設定為**int** ，以符合泛型參數的值。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 如需完整的執行方式，請參閱[IdentityUser （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs)。 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>自訂使用者存放區

您也會建立 UserStore 類別，以提供使用者上所有資料作業的方法。 這個類別相當於[EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空間中的[UserStore&lt;TUser&gt;](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx)類別。 在您的 UserStore 類別中，您會執行[TUser、TKey&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx)和任何選擇性介面的 IUserStore&lt;。 您可以根據想要在應用程式中提供的功能，選取要執行的選擇性介面。

下圖顯示您必須建立的 UserStore 類別，以及相關的介面。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

Visual Studio 中的預設專案範本包含的程式碼，會假設已在使用者存放區中實作為許多選用介面。 如果您使用預設範本搭配自訂使用者存放區，您必須在使用者存放區中執行選擇性介面，或修改範本程式碼，使其不會再呼叫尚未執行之介面中的方法。

 下列範例顯示簡單的使用者存放區類別。 **TUser**泛型參數會採用您的使用者類別類型，這通常是您所定義的 IdentityUser 類別。 **TKey**泛型參數會採用您的使用者金鑰類型。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 在此範例中，採用 ExampleDatabase*類型之參數的函*式，只是如何傳入資料存取類別的說明。 例如，在 MySQL 的執行中，此函式會採用 MySQLDatabase 類型的參數。 

在您的 UserStore 類別中，您可以使用您所建立的資料存取類別來執行作業。 例如，在 MySQL 的執行中，UserStore 類別具有 CreateAsync 方法，它會使用 UserTable 的實例來插入新的記錄。 **UserTable**物件上的**Insert**方法與上一節所顯示的方法相同。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>自訂使用者存放區時所要執行的介面

下一個影像會顯示有關每個介面中所定義功能的更多詳細資料。 所有選用的介面都繼承自 IUserStore。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
  [IUserStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx)介面是您必須在使用者存放區中執行的唯一介面。 它會定義用來建立、更新、刪除和抓取使用者的方法。
- **IUserClaimStore**  
  [IUserClaimStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx)介面會定義您必須在使用者存放區中執行的方法，以啟用使用者宣告。 它包含方法，或加入、移除和抓取使用者宣告。
- **IUserLoginStore**  
  [IUserLoginStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx)會定義您必須在使用者存放區中執行的方法，以啟用外部驗證提供者。 其中包含加入、移除和抓取使用者登入的方法，以及根據登入資訊來抓取使用者的方法。
- **IUserRoleStore**  
  [IUserRoleStore&lt;TKey，TUser&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx)介面會定義您必須在使用者存放區中執行的方法，以將使用者對應至角色。 其中包含新增、移除和抓取使用者角色的方法，以及檢查使用者是否已指派給角色的方法。
- **IUserPasswordStore**  
  [IUserPasswordStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx)介面會定義您必須在使用者存放區中執行的方法，以保存雜湊的密碼。 其中包含取得和設定雜湊密碼的方法，以及指出使用者是否已設定密碼的方法。
- **IUserSecurityStampStore**  
  [IUserSecurityStampStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx)介面會定義您必須在使用者存放區中執行的方法，以使用安全性戳記來指出使用者的帳戶資訊是否已變更。 當使用者變更密碼或新增或移除登入時，就會更新此戳記。 其中包含取得和設定安全性戳記的方法。
- **IUserTwoFactorStore**  
  [IUserTwoFactorStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx)介面會定義您必須執行以執行雙因素驗證的方法。 其中包含取得和設定是否為使用者啟用雙因素驗證的方法。
- **IUserPhoneNumberStore**  
  [IUserPhoneNumberStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx)介面會定義您必須執行才能儲存使用者電話號碼的方法。 其中包含取得和設定電話號碼的方法，以及電話號碼是否已確認。
- **IUserEmailStore**  
  [IUserEmailStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx)介面會定義您必須執行才能儲存使用者電子郵件地址的方法。 其中包含取得和設定電子郵件地址的方法，以及是否確認電子郵件。
- **IUserLockoutStore**  
  [IUserLockoutStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx)介面會定義您必須執行的方法，以儲存鎖定帳戶的相關資訊。 其中包含的方法可讓您取得目前失敗的存取嘗試次數、取得及設定是否可以鎖定帳戶、取得和設定鎖定的結束日期、增加失敗嘗試次數，以及重設失敗的嘗試次數。
- **IQueryableUserStore**  
  [IQueryableUserStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx)介面會定義您必須執行才能提供可查詢使用者存放區的成員。 其中包含的屬性會保存可查詢的使用者。

  您會執行應用程式所需的介面;例如，IUserClaimStore、IUserLoginStore、IUserRoleStore、IUserPasswordStore 和 IUserSecurityStampStore 介面，如下所示。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

如需完整的執行（包括所有介面），請參閱[UserStore （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs)。

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>IdentityUserClaim、IdentityUserLogin 和 IdentityUserRole

EntityFramework 命名空間包含[IdentityUserClaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx)、 [IdentityUserLogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx)和[IdentityUserRole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx)類別的執行。 如果您使用這些功能，您可能會想要建立您自己的類別版本，並定義應用程式的屬性。 不過，有時候在執行基本作業（例如新增或移除使用者的宣告）時，不會將這些實體載入記憶體的效率較高。 相反地，後端存放區類別可以直接在資料來源上執行這些作業。 例如，UserStore. GetClaimsAsync （）方法可以呼叫 userClaimTable. FindByUserId （user。Id）方法來直接對該資料表執行查詢，並傳回宣告的清單。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>自訂角色類別

在執行您自己的儲存區提供者時，您必須建立相當於[EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空間中[IdentityRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx)類別的 role 類別：

下圖顯示您必須建立的 IdentityRole 類別，以及要在此類別中執行的介面。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

[IRole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)介面會定義 RoleManager 在執行要求的作業時嘗試呼叫的屬性。 介面包含兩個屬性：識別碼和名稱。 [IRole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)介面可讓您透過泛型**TKey**參數指定角色的金鑰型別。 Id 屬性的類型符合 TKey 參數的值。

當您想要使用字串值做為索引鍵時，身分識別架構也會提供[IRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx)介面（不含泛型參數）。

下列範例顯示使用整數做為索引鍵的 IdentityRole 類別。 [識別碼] 欄位會設定為 int，以符合泛型參數的值。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 如需完整的執行方式，請參閱[IdentityRole （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs)。 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>自訂角色存放區

您也會建立 RoleStore 類別，以提供角色上所有資料作業的方法。 這個類別相當於 EntityFramework 命名空間中的[RoleStore&lt;TRole&gt;](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx)類別。 在您的 RoleStore 類別中，您會執行[IRoleStore&lt;TRole、TKey&gt;](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx)和選擇性的[IQueryableRoleStore&lt;TRole、TKey&gt;](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx)介面。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

下列範例顯示角色存放區類別。 TRole 泛型參數會採用您的角色類別類型，這通常是您所定義的 IdentityRole 類別。 TKey 泛型參數會採用您的角色金鑰類型。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
  [IRoleStore](https://msdn.microsoft.com/library/dn468195.aspx)介面會定義要在您的角色存放區類別中執行的方法。 其中包含用來建立、更新、刪除和抓取角色的方法。
- **RoleStore&lt;TRole&gt;**  
  若要自訂 RoleStore，請建立一個可執行 IRoleStore 介面的類別。 只有在您想要在系統上使用角色時，才需要執行此類別。 採用型別為*ExampleDatabase 之參數的函*式，只是如何傳入資料存取類別的說明。 例如，在 MySQL 的執行中，此函式會採用 MySQLDatabase 類型的參數。  
  
  如需完整的執行方式，請參閱[RoleStore （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) 。

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>重新設定應用程式以使用新的存放裝置提供者

您已執行新的存放裝置提供者。 現在，您必須將應用程式設定為使用此存放裝置提供者。 如果您的專案中包含預設的儲存提供者，您必須移除預設的提供者，並將它取代為您的提供者。

### <a name="replace-default-storage-provider-in-mvc-project"></a>取代 MVC 專案中的預設儲存提供者

1. 在 [**管理 NuGet 套件**] 視窗中，卸載**Microsoft ASP.NET Identity EntityFramework**套件。 您可以在已安裝的套件中搜尋 EntityFramework 來找到此套件。  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png) 系統會詢問您是否也要卸載 Entity Framework。 如果您在應用程式的其他部分中不需要它，您可以將它卸載。
2. 在 [模型] 資料夾的 IdentityModels.cs 檔案中，刪除或批註掉**ApplicationUser**和 **[applicationdbcoNtext]** 類別。 在 MVC 應用程式中，您可以刪除整個 IdentityModels.cs 檔案。 在 Web form 應用程式中，刪除這兩個類別，但請務必保留也位於 IdentityModels.cs 檔案中的 helper 類別。
3. 如果您的存放裝置提供者位於不同的專案中，請在您的 web 應用程式中加入它的參考。
4. 使用儲存提供者命名空間的 using 語句，取代所有 `using Microsoft.AspNet.Identity.EntityFramework;` 的參考。
5. 在**Startup.Auth.cs**類別中，將**configureauth ...** 方法變更為使用適當內容的單一實例。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. 在應用程式\_開始 資料夾中，開啟**IdentityConfig.cs**。 在 ApplicationUserManager 類別中，變更**Create**方法以傳回使用您自訂使用者存放區的使用者管理員。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. 使用**IdentityUser**取代**ApplicationUser**的所有參考。
8. 預設專案包含 user 類別中未在 IUser 介面中定義的某些成員;例如 Email、PasswordHash 和 GenerateUserIdentityAsync。 如果您的使用者類別沒有這些成員，您必須加以執行，或變更使用這些成員的程式碼。
9. 如果您已建立 RoleManager 的任何實例，請變更該程式碼以使用新的 RoleStore 類別。  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. 預設專案是針對具有索引鍵之字串值的使用者類別所設計。 如果您的使用者類別有不同的索引鍵類型（例如整數），您就必須變更專案以與您的類型搭配使用。 請參閱[變更使用者在 ASP.NET Identity 中的主要金鑰](change-primary-key-for-users-in-aspnet-identity.md)。
11. 如有需要，請將連接字串加入至 web.config 檔案。

<a id="other"></a>
## <a name="other-resources"></a>其他資源

- Blog：[執行 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 教學課程和 GIT 程式碼：[簡單的。資料 Asp.Net 識別提供者](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- 教學課程：[設定基本身分識別帳戶，並將它們指向外部 DB](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)。 依[@xivSolutions](https://twitter.com/xivSolutions)。
- 教學課程[：執行自訂 MySQL ASP.NET Identity 存放裝置提供者](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- 依[SoftFluent](http://www.softfluent.com/) [CodeFluent 實體](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/)
- [Azure 表格儲存體](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/)的 James Randall。
- Azure 表格儲存體： [@stuartleeks](https://twitter.com/stuartleeks)的[TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) 。
- [CouchDB/Cloudant by Daniel Wertheim。](https://github.com/danielwertheim/mycouch.aspnet.identity)
- 彈性 h[h：](https://github.com/bmbsqd/elastic-identity) Bombsquad AB 的彈性身分識別。
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) By Jonathan Sheely Jonathan Sheely。
- [NHibernate](https://github.com/milesibastos/NHibernate.AspNet.Identity) By Antônio Milesi Bastos。
- [@tourismgeek](https://twitter.com/tourismgeek) [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) 。
- 依[ILMServices](http://www.ilmservice.com/)的[RavenDB 身分識別](https://github.com/ILMServices/RavenDB.AspNet.Identity)。
- Redis： [Redis。身分識別](https://github.com/aminjam/Redis.AspNet.Identity)
- T4 範本，用來產生「資料庫第一個」使用者存放區的 EF 程式碼： [AspNet. Identity. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)
