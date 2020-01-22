---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: 執行自訂 MySQL ASP.NET Identity 存放裝置提供者-ASP.NET 4。x
author: raquelsa
description: ASP.NET Identity 是可延伸的系統，可讓您建立自己的儲存提供者，並將它插入您的應用程式，而不需要重新運作 & 。
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519124"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>實作自訂的 MySQL ASP.NET Identity 儲存體提供者

依[Raquel Soares De Almeida](https://github.com/raquelsa)、 [Suhas Joshi](https://github.com/suhasj)、 [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity 是可延伸的系統，可讓您建立自己的儲存提供者，並將它插入您的應用程式，而不需要重新運作應用程式。 本主題說明如何建立 ASP.NET Identity 的 MySQL 存放裝置提供者。 如需建立自訂存放裝置提供者的總覽，請參閱[ASP.NET Identity 的自訂儲存體提供者總覽](overview-of-custom-storage-providers-for-aspnet-identity.md)。
> 
> 若要完成本教學課程，您必須有 Update 2 的 Visual Studio 2013。
> 
> 本教學課程將：
> 
> - 示範如何在 Azure 上建立 MySQL 資料庫實例。
> - 示範如何使用 MySQL 用戶端工具（MySQL 工作臺）來建立資料表，以及在 Azure 上管理您的遠端資料庫。
> - 示範如何在 MVC 應用程式專案上以我們的自訂執行來取代預設的 ASP.NET Identity 儲存區執行。
> 
> 本教學課程原本是由 Raquel Soares De Almeida 和 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）撰寫。 Suhas Joshi 已針對身分識別2.0 更新範例專案。 本主題已針對 Tom FitzMacken 更新為身分識別2.0。

## <a name="download-completed-project"></a>下載已完成的專案

在本教學課程結束時，您將會有一個 MVC 應用程式專案，其 ASP.NET Identity 使用裝載于 Azure 上的 MySQL 資料庫。

您可以在[AspNet. Identity. mysql （GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)下載已完成的 MySQL 儲存提供者。

## <a name="the-steps-you-will-perform"></a>您將執行的步驟

在此教學課程中，您將：

1. 在 Azure 上建立 MySQL 資料庫
2. 在 MySQL 中建立 ASP.NET Identity 資料表
3. 建立 MVC 應用程式，並將它設定為使用 MySQL 提供者
4. 執行應用程式

本主題不涵蓋 ASP.NET Identity 的架構，以及在執行客戶存放裝置提供者時必須進行的決策。 如需相關資訊，請參閱[ASP.NET Identity 的自訂儲存體提供者總覽](overview-of-custom-storage-providers-for-aspnet-identity.md)。

## <a name="review-mysql-storage-provider-classes"></a>審查 MySQL 儲存提供者類別

在您開始建立 MySQL 存放裝置提供者的步驟之前，讓我們先查看組成存放裝置提供者的類別。 您將需要可管理資料庫作業的類別，以及從應用程式呼叫來管理使用者和角色的類別。

### <a name="storage-classes"></a>儲存類別

- [IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -包含使用者的屬性。
- [UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -包含用來新增、更新或正在抓取使用者的作業。
- [IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -包含角色的屬性。
- [RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -包含新增、刪除、更新和抓取角色的作業。

### <a name="data-access-layer-classes"></a>資料存取層類別

在此範例中，資料存取層類別包含用來處理資料表的 SQL 語句;不過，在您的程式碼中，您可能會想要使用物件關聯式對應（ORM），例如 Entity Framework 或 NHibernate。 特別是，如果沒有包含消極式載入和物件快取的 ORM，您的應用程式可能會遇到效能不佳的情況。 如需詳細資訊，請參閱[ASP.NET Identity 2.0 而不 Entity Framework？](https://aspnetidentity.codeplex.com/discussions/561828)

- [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -包含 MySQL 資料庫連接，以及執行資料庫作業的方法。 UserStore 和 RoleStore 都是使用這個類別的實例具現化。
- [RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -包含儲存角色之資料表的資料庫作業。
- [UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -包含儲存使用者宣告之資料表的資料庫作業。
- [UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -包含儲存使用者登入資訊之資料表的資料庫作業。
- [UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -包含資料表的資料庫作業，其會儲存哪些使用者指派給哪些角色。
- [UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -包含儲存使用者之資料表的資料庫作業。

## <a name="create-a-mysql-database-instance-on-azure"></a>在 Azure 上建立 MySQL 資料庫實例

1. 登入 [Azure 入口網站](https://manage.windowsazure.com/)。
2. 按一下頁面底部的 [ **+ 新增**]，然後選取 [**儲存**]。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. 在 [**選擇和附加**元件] 中，選取 [ **ClearDB MySQL 資料庫**]，然後按一下對話方塊右下方的 [下一步] 箭號。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. 保留預設的 [**免費**] 方案，並將**名稱**變更為**IdentityMySQLDatabase**。 選取最接近您的區域，然後按 [下一步] 箭號。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. 按一下核取記號以完成資料庫建立。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. 建立資料庫之後，您可以從管理入口網站的 [附加元件] 索引標籤加以管理。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. 按一下頁面底部的 [**連接資訊**]，即可取得資料庫連接資訊。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. 按一下 [複製] 按鈕來複製連接字串並加以儲存，以便稍後在 MVC 應用程式中使用。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>在 MySQL 資料庫中建立 ASP.NET Identity 資料表

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>安裝 MySQL 工作臺工具以連接及管理 MySQL 資料庫

1. 從[mysql 下載頁面](http://dev.mysql.com/downloads/windows/installer/)安裝**mysql 工作臺**工具
2. 啟動應用程式並新增按一下 [ **MySQLConnections +** ] 按鈕，以新增連接。 使用您稍早在本教學課程中建立的 Azure MySQL 資料庫所複製的連接字串資料。
3. 建立連線之後，請開啟新的 [**查詢**] 索引標籤;將[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)中的命令貼入查詢中並加以執行，以便建立資料庫資料表。
4. 您現在已擁有在裝載于 Azure 上的 MySQL 資料庫上建立的所有 ASP.NET Identity 必要資料表，如下所示。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>從範本建立 MVC 應用程式專案，並將其設定為使用 MySQL 提供者

如有需要，請[為 Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)安裝 Update 2 的 Visual Studio Express 2013。

### <a name="download-the-aspnetidentitymysql-project-from-github"></a>從 GitHub 下載. NET.TCP 專案

1. 流覽至位於[AspNet. Identity. MySQL （GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)的存放庫 URL。
2. 下載原始程式碼。
3. 將 .zip 檔案解壓縮至本機資料夾。
4. 開啟 AspNet. 身分識別 MySQL 解決方案，並加以建立。

### <a name="create-a-new-mvc-application-project-from-template"></a>從範本建立新的 MVC 應用程式專案

1. 以滑鼠右鍵按一下**AspNet. 身分識別 MySQL**方案 **，** 然後**新增新專案**
2. 在 [**加入新的專案**] 對話方塊中，選取左側的 [**視覺效果C#**  ] **，然後選取**[ **ASP.NET web 應用程式**]。 將專案命名為**IdentityMySQLDemo**;然後按一下 [確定]。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. 在 [**新增 ASP.NET 專案**] 對話方塊中，選取具有預設選項（其中包含**個別使用者帳戶**做為驗證方法）的 MVC 範本，然後按一下 **[確定]** 。![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. 在方案總管中，以滑鼠右鍵按一下 IdentityMySQLDemo 專案，然後選取 [**管理 NuGet 套件**]。 在 [搜尋文字方塊] 對話方塊中，輸入**Identity. EntityFramework**。 在結果清單中選取此套件，然後按一下 [**卸載**]。 系統會提示您卸載相依性套件 EntityFramework。 按一下 [是]，因為此應用程式不會再有此套件。
5. 以滑鼠右鍵按一下 IdentityMySQLDemo 專案，選取 [**加入**]、[**參考]、[方案]、[專案**]，然後選取 [node.js] 專案，再按一下 **[確定]** 。
6. 在 IdentityMySQLDemo 專案中，將所有參考取代為  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   使用  
     `using AspNet.Identity.MySQL;`
7. 在 IdentityModels.cs 中，將 **[applicationdbcoNtext]** 設定為衍生自**MySqlDatabase** ，並包含採用單一參數與連接名稱的函式。  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. 開啟 IdentityConfig.cs 檔案。 在**ApplicationUserManager**方法中，將具現化的 UserManager 取代為下列程式碼：  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. 開啟 web.config 檔案，並將 DefaultConnection 字串取代為此專案，並將反白顯示的值取代為您在先前步驟中建立的 MySQL 資料庫連接字串：  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>執行應用程式並連接到 MySQL DB

1. 以滑鼠右鍵按一下**IdentityMySQLDemo**專案，然後選取 [**設定為啟始專案**]
2. 按**Ctrl + F5**以建立並執行應用程式。
3. 按一下頁面頂端的 [**註冊**] 索引標籤。
4. 輸入新的 [使用者名稱] 和 [密碼]，然後按一下 [**註冊**]。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. 新的使用者現在已註冊並登入。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. 返回 MySQL 工作臺工具，並檢查**IdentityMySQLDatabase**資料表的內容。 當您註冊新的使用者時，請檢查 [使用者] 資料表中的專案。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>後續步驟

如需如何在此應用程式上啟用其他驗證方法的詳細資訊，請參閱[使用 Facebook 和 Google OAuth2 和 OpenID 登入建立 ASP.NET MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。

若要瞭解如何整合 DB 與 OAuth，並設定角色以限制使用者存取您的應用程式，請參閱將[具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署至 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。
