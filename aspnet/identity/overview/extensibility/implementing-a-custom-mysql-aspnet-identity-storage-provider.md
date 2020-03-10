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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616911"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a><span data-ttu-id="fd09c-103">實作自訂的 MySQL ASP.NET Identity 儲存體提供者</span><span class="sxs-lookup"><span data-stu-id="fd09c-103">Implementing a Custom MySQL ASP.NET Identity Storage Provider</span></span>

<span data-ttu-id="fd09c-104">依[Raquel Soares De Almeida](https://github.com/raquelsa)、 [Suhas Joshi](https://github.com/suhasj)、 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fd09c-104">by [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fd09c-105">ASP.NET Identity 是可延伸的系統，可讓您建立自己的儲存提供者，並將它插入您的應用程式，而不需要重新運作應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd09c-105">ASP.NET Identity is an extensible system which enables you to create your own storage provider and plug it into your application without re-working the application.</span></span> <span data-ttu-id="fd09c-106">本主題說明如何建立 ASP.NET Identity 的 MySQL 存放裝置提供者。</span><span class="sxs-lookup"><span data-stu-id="fd09c-106">This topic describes how to create a MySQL storage provider for ASP.NET Identity.</span></span> <span data-ttu-id="fd09c-107">如需建立自訂存放裝置提供者的總覽，請參閱[ASP.NET Identity 的自訂儲存體提供者總覽](overview-of-custom-storage-providers-for-aspnet-identity.md)。</span><span class="sxs-lookup"><span data-stu-id="fd09c-107">For an overview of creating custom storage providers, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>
> 
> <span data-ttu-id="fd09c-108">若要完成本教學課程，您必須有 Update 2 的 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="fd09c-108">To complete this tutorial, you must have Visual Studio 2013 with Update 2.</span></span>
> 
> <span data-ttu-id="fd09c-109">本教學課程將：</span><span class="sxs-lookup"><span data-stu-id="fd09c-109">This tutorial will:</span></span>
> 
> - <span data-ttu-id="fd09c-110">示範如何在 Azure 上建立 MySQL 資料庫實例。</span><span class="sxs-lookup"><span data-stu-id="fd09c-110">Show how to create a MySQL database instance on Azure.</span></span>
> - <span data-ttu-id="fd09c-111">示範如何使用 MySQL 用戶端工具（MySQL 工作臺）來建立資料表，以及在 Azure 上管理您的遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd09c-111">Show how to use a MySQL client tool (MySQL Workbench) to create tables and manage your remote database on Azure.</span></span>
> - <span data-ttu-id="fd09c-112">示範如何在 MVC 應用程式專案上以我們的自訂執行來取代預設的 ASP.NET Identity 儲存區執行。</span><span class="sxs-lookup"><span data-stu-id="fd09c-112">Show how to replace the default ASP.NET Identity storage implementation with our custom implementation on a MVC application project.</span></span>
> 
> <span data-ttu-id="fd09c-113">本教學課程原本是由 Raquel Soares De Almeida 和 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）撰寫。</span><span class="sxs-lookup"><span data-stu-id="fd09c-113">This tutorial was originally written by Raquel Soares De Almeida and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span> <span data-ttu-id="fd09c-114">Suhas Joshi 已針對身分識別2.0 更新範例專案。</span><span class="sxs-lookup"><span data-stu-id="fd09c-114">The sample project was updated for Identity 2.0 by Suhas Joshi.</span></span> <span data-ttu-id="fd09c-115">本主題已針對 Tom FitzMacken 更新為身分識別2.0。</span><span class="sxs-lookup"><span data-stu-id="fd09c-115">The topic was updated for Identity 2.0 by Tom FitzMacken.</span></span>

## <a name="download-completed-project"></a><span data-ttu-id="fd09c-116">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="fd09c-116">Download completed project</span></span>

<span data-ttu-id="fd09c-117">在本教學課程結束時，您將會有一個 MVC 應用程式專案，其 ASP.NET Identity 使用裝載于 Azure 上的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd09c-117">At the end of this tutorial, you will have an MVC application project with ASP.NET Identity working with a MySQL database hosted on Azure.</span></span>

<span data-ttu-id="fd09c-118">您可以在[AspNet. Identity. mysql （GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)下載已完成的 MySQL 儲存提供者。</span><span class="sxs-lookup"><span data-stu-id="fd09c-118">You can download the completed MySQL storage provider at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL).</span></span>

## <a name="the-steps-you-will-perform"></a><span data-ttu-id="fd09c-119">您將執行的步驟</span><span class="sxs-lookup"><span data-stu-id="fd09c-119">The steps you will perform</span></span>

<span data-ttu-id="fd09c-120">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="fd09c-120">In this tutorial you will:</span></span>

1. <span data-ttu-id="fd09c-121">在 Azure 上建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="fd09c-121">Create a MySQL database on Azure</span></span>
2. <span data-ttu-id="fd09c-122">在 MySQL 中建立 ASP.NET Identity 資料表</span><span class="sxs-lookup"><span data-stu-id="fd09c-122">Create the ASP.NET Identity tables in MySQL</span></span>
3. <span data-ttu-id="fd09c-123">建立 MVC 應用程式，並將它設定為使用 MySQL 提供者</span><span class="sxs-lookup"><span data-stu-id="fd09c-123">Create an MVC application and configure it to use the MySQL provider</span></span>
4. <span data-ttu-id="fd09c-124">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="fd09c-124">Run the app</span></span>

<span data-ttu-id="fd09c-125">本主題不涵蓋 ASP.NET Identity 的架構，以及在執行客戶存放裝置提供者時必須進行的決策。</span><span class="sxs-lookup"><span data-stu-id="fd09c-125">This topic does not cover the architecture of ASP.NET Identity and the decisions you must make when implementing a customer storage provider.</span></span> <span data-ttu-id="fd09c-126">如需相關資訊，請參閱[ASP.NET Identity 的自訂儲存體提供者總覽](overview-of-custom-storage-providers-for-aspnet-identity.md)。</span><span class="sxs-lookup"><span data-stu-id="fd09c-126">For that information, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>

## <a name="review-mysql-storage-provider-classes"></a><span data-ttu-id="fd09c-127">審查 MySQL 儲存提供者類別</span><span class="sxs-lookup"><span data-stu-id="fd09c-127">Review MySQL storage provider classes</span></span>

<span data-ttu-id="fd09c-128">在您開始建立 MySQL 存放裝置提供者的步驟之前，讓我們先查看組成存放裝置提供者的類別。</span><span class="sxs-lookup"><span data-stu-id="fd09c-128">Before jumping into the steps to create the MySQL storage provider, let's look at the classes that make up the storage provider.</span></span> <span data-ttu-id="fd09c-129">您將需要可管理資料庫作業的類別，以及從應用程式呼叫來管理使用者和角色的類別。</span><span class="sxs-lookup"><span data-stu-id="fd09c-129">You will need classes that manage the database operations and classes that are called from the application to manage users and roles.</span></span>

### <a name="storage-classes"></a><span data-ttu-id="fd09c-130">儲存類別</span><span class="sxs-lookup"><span data-stu-id="fd09c-130">Storage classes</span></span>

- <span data-ttu-id="fd09c-131">[IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -包含使用者的屬性。</span><span class="sxs-lookup"><span data-stu-id="fd09c-131">[IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) - contains properties for the user.</span></span>
- <span data-ttu-id="fd09c-132">[UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -包含用來新增、更新或正在抓取使用者的作業。</span><span class="sxs-lookup"><span data-stu-id="fd09c-132">[UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) - contains operations for adding, updating or retrieving users.</span></span>
- <span data-ttu-id="fd09c-133">[IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -包含角色的屬性。</span><span class="sxs-lookup"><span data-stu-id="fd09c-133">[IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) - contains properties for roles.</span></span>
- <span data-ttu-id="fd09c-134">[RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -包含新增、刪除、更新和抓取角色的作業。</span><span class="sxs-lookup"><span data-stu-id="fd09c-134">[RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) - contains operations for adding, deleting, updating and retrieving roles.</span></span>

### <a name="data-access-layer-classes"></a><span data-ttu-id="fd09c-135">資料存取層類別</span><span class="sxs-lookup"><span data-stu-id="fd09c-135">Data access layer classes</span></span>

<span data-ttu-id="fd09c-136">在此範例中，資料存取層類別包含用來處理資料表的 SQL 語句;不過，在您的程式碼中，您可能會想要使用物件關聯式對應（ORM），例如 Entity Framework 或 NHibernate。</span><span class="sxs-lookup"><span data-stu-id="fd09c-136">For this example, the data access layer classes contain SQL statements for working with the tables; however, in your code you might want to use object-relational mapping (ORM) such as Entity Framework or NHibernate.</span></span> <span data-ttu-id="fd09c-137">特別是，如果沒有包含消極式載入和物件快取的 ORM，您的應用程式可能會遇到效能不佳的情況。</span><span class="sxs-lookup"><span data-stu-id="fd09c-137">In particular, your application may experience poor performance without an ORM that includes lazy loading and object caching.</span></span> <span data-ttu-id="fd09c-138">如需詳細資訊，請參閱[ASP.NET Identity 2.0 而不 Entity Framework？](https://aspnetidentity.codeplex.com/discussions/561828)</span><span class="sxs-lookup"><span data-stu-id="fd09c-138">For more information, see [ASP.NET Identity 2.0 without Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)</span></span>

- <span data-ttu-id="fd09c-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -包含 MySQL 資料庫連接，以及執行資料庫作業的方法。</span><span class="sxs-lookup"><span data-stu-id="fd09c-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) - contains the MySQL database connection and methods for performing database operations.</span></span> <span data-ttu-id="fd09c-140">UserStore 和 RoleStore 都是使用這個類別的實例具現化。</span><span class="sxs-lookup"><span data-stu-id="fd09c-140">UserStore and RoleStore are both instantiated with an instance of this class.</span></span>
- <span data-ttu-id="fd09c-141">[RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -包含儲存角色之資料表的資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="fd09c-141">[RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) - contains database operations for the table that stores roles.</span></span>
- <span data-ttu-id="fd09c-142">[UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -包含儲存使用者宣告之資料表的資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="fd09c-142">[UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) - contains database operations for the table that stores user claims.</span></span>
- <span data-ttu-id="fd09c-143">[UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -包含儲存使用者登入資訊之資料表的資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="fd09c-143">[UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) - contains database operations for the table that stores user login information.</span></span>
- <span data-ttu-id="fd09c-144">[UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -包含資料表的資料庫作業，其會儲存哪些使用者指派給哪些角色。</span><span class="sxs-lookup"><span data-stu-id="fd09c-144">[UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) - contains database operations for the table that stores which users are assigned to which roles.</span></span>
- <span data-ttu-id="fd09c-145">[UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -包含儲存使用者之資料表的資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="fd09c-145">[UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) - contains database operations for the table that stores users.</span></span>

## <a name="create-a-mysql-database-instance-on-azure"></a><span data-ttu-id="fd09c-146">在 Azure 上建立 MySQL 資料庫實例</span><span class="sxs-lookup"><span data-stu-id="fd09c-146">Create a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="fd09c-147">登入 [Azure 入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="fd09c-147">Log in to the [Azure Portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="fd09c-148">按一下頁面底部的 [ **+ 新增**]，然後選取 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="fd09c-148">Click **+NEW** at the bottom of the page, and then select **STORE**.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. <span data-ttu-id="fd09c-149">在 [**選擇和附加**元件] 中，選取 [ **ClearDB MySQL 資料庫**]，然後按一下對話方塊右下方的 [下一步] 箭號。</span><span class="sxs-lookup"><span data-stu-id="fd09c-149">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database** and click on the next arrow at the bottom right of the dialog.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. <span data-ttu-id="fd09c-150">保留預設的 [**免費**] 方案，並將**名稱**變更為**IdentityMySQLDatabase**。</span><span class="sxs-lookup"><span data-stu-id="fd09c-150">Keep the default **Free** plan and change the **Name** to **IdentityMySQLDatabase**.</span></span> <span data-ttu-id="fd09c-151">選取最接近您的區域，然後按 [下一步] 箭號。</span><span class="sxs-lookup"><span data-stu-id="fd09c-151">Select the region nearest you and then click the next arrow.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. <span data-ttu-id="fd09c-152">按一下核取記號以完成資料庫建立。</span><span class="sxs-lookup"><span data-stu-id="fd09c-152">Click the checkmark to complete the database creation.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. <span data-ttu-id="fd09c-153">建立資料庫之後，您可以從管理入口網站的 [附加元件] 索引標籤加以管理。</span><span class="sxs-lookup"><span data-stu-id="fd09c-153">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. <span data-ttu-id="fd09c-154">按一下頁面底部的 [**連接資訊**]，即可取得資料庫連接資訊。</span><span class="sxs-lookup"><span data-stu-id="fd09c-154">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. <span data-ttu-id="fd09c-155">按一下 [複製] 按鈕來複製連接字串並加以儲存，以便稍後在 MVC 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="fd09c-155">Copy the connection string by clicking on the copy button and save it so you can use later in your MVC application.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a><span data-ttu-id="fd09c-156">在 MySQL 資料庫中建立 ASP.NET Identity 資料表</span><span class="sxs-lookup"><span data-stu-id="fd09c-156">Create the ASP.NET Identity tables in a MySQL database</span></span>

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a><span data-ttu-id="fd09c-157">安裝 MySQL 工作臺工具以連接及管理 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="fd09c-157">Install MySQL Workbench tool to connect and manage MySQL database</span></span>

1. <span data-ttu-id="fd09c-158">從[mysql 下載頁面](http://dev.mysql.com/downloads/windows/installer/)安裝**mysql 工作臺**工具</span><span class="sxs-lookup"><span data-stu-id="fd09c-158">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="fd09c-159">啟動應用程式並新增按一下 [ **MySQLConnections +** ] 按鈕，以新增連接。</span><span class="sxs-lookup"><span data-stu-id="fd09c-159">Launch the app and add click on the **MySQLConnections +** button to add a new connection.</span></span> <span data-ttu-id="fd09c-160">使用您稍早在本教學課程中建立的 Azure MySQL 資料庫所複製的連接字串資料。</span><span class="sxs-lookup"><span data-stu-id="fd09c-160">Use the connection string data you copied from the Azure MySQL database you created earlier in this tutorial.</span></span>
3. <span data-ttu-id="fd09c-161">建立連線之後，請開啟新的 [**查詢**] 索引標籤;將[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)中的命令貼入查詢中並加以執行，以便建立資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="fd09c-161">After establishing the connection, open a new **Query** tab; paste the commands from [MySQLIdentity.sql](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) into the query and execute it in order to create the database tables.</span></span>
4. <span data-ttu-id="fd09c-162">您現在已擁有在裝載于 Azure 上的 MySQL 資料庫上建立的所有 ASP.NET Identity 必要資料表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fd09c-162">You now have all the ASP.NET Identity necessary tables created on a MySQL database hosted on Azure as shown below.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a><span data-ttu-id="fd09c-163">從範本建立 MVC 應用程式專案，並將其設定為使用 MySQL 提供者</span><span class="sxs-lookup"><span data-stu-id="fd09c-163">Create an MVC application project from template and configure it to use MySQL provider</span></span>

<span data-ttu-id="fd09c-164">如有需要，請[為 Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)安裝 Update 2 的 Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="fd09c-164">If needed, install either [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with Update 2.</span></span>

### <a name="download-the-aspnetidentitymysql-project-from-github"></a><span data-ttu-id="fd09c-165">從 GitHub 下載. NET.TCP 專案</span><span class="sxs-lookup"><span data-stu-id="fd09c-165">Download the ASP.NET.Identity.MySQL project from GitHub</span></span>

1. <span data-ttu-id="fd09c-166">流覽至位於[AspNet. Identity. MySQL （GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)的存放庫 URL。</span><span class="sxs-lookup"><span data-stu-id="fd09c-166">Browse to the repository URL at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/).</span></span>
2. <span data-ttu-id="fd09c-167">下載原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd09c-167">Download the source code.</span></span>
3. <span data-ttu-id="fd09c-168">將 .zip 檔案解壓縮至本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="fd09c-168">Extract the .zip file into a local folder.</span></span>
4. <span data-ttu-id="fd09c-169">開啟 AspNet. 身分識別 MySQL 解決方案，並加以建立。</span><span class="sxs-lookup"><span data-stu-id="fd09c-169">Open the AspNet.Identity.MySQL solution and build it.</span></span>

### <a name="create-a-new-mvc-application-project-from-template"></a><span data-ttu-id="fd09c-170">從範本建立新的 MVC 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="fd09c-170">Create a new MVC application project from template</span></span>

1. <span data-ttu-id="fd09c-171">以滑鼠右鍵按一下**AspNet. 身分識別 MySQL**方案 **，** 然後**新增新專案**</span><span class="sxs-lookup"><span data-stu-id="fd09c-171">Right click the **AspNet.Identity.MySQL** solution and **Add**, **New Project**</span></span>
2. <span data-ttu-id="fd09c-172">在 [**加入新的專案**] 對話方塊中，選取左側的 [**視覺效果C#**  ] **，然後選取**[ **ASP.NET web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="fd09c-172">In the **Add New Project** Dialog select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="fd09c-173">將專案命名為**IdentityMySQLDemo**;然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fd09c-173">Name your project **IdentityMySQLDemo**; and then click OK.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. <span data-ttu-id="fd09c-174">在 [**新增 ASP.NET 專案**] 對話方塊中，選取具有預設選項（其中包含**個別使用者帳戶**做為驗證方法）的 MVC 範本，然後按一下 **[確定]** 。![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span><span class="sxs-lookup"><span data-stu-id="fd09c-174">In the **New ASP.NET Project** dialog, select the MVC template with the default options (that includes **Individual User Accounts** as authentication method) and click **OK**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span></span>
4. <span data-ttu-id="fd09c-175">在方案總管中，以滑鼠右鍵按一下 IdentityMySQLDemo 專案，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="fd09c-175">In Solution Explorer, right-click your IdentityMySQLDemo project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="fd09c-176">在 [搜尋文字方塊] 對話方塊中，輸入**Identity. EntityFramework**。</span><span class="sxs-lookup"><span data-stu-id="fd09c-176">In the search text box dialog, type **Identity.EntityFramework**.</span></span> <span data-ttu-id="fd09c-177">在結果清單中選取此套件，然後按一下 [**卸載**]。</span><span class="sxs-lookup"><span data-stu-id="fd09c-177">Select this package in the list of results and click **Uninstall**.</span></span> <span data-ttu-id="fd09c-178">系統會提示您卸載相依性套件 EntityFramework。</span><span class="sxs-lookup"><span data-stu-id="fd09c-178">You will be prompted to uninstall the dependency package EntityFramework.</span></span> <span data-ttu-id="fd09c-179">按一下 [是]，因為此應用程式不會再有此套件。</span><span class="sxs-lookup"><span data-stu-id="fd09c-179">Click on Yes as we will no longer this package on this application.</span></span>
5. <span data-ttu-id="fd09c-180">以滑鼠右鍵按一下 IdentityMySQLDemo 專案，選取 [**加入**]、[**參考]、[方案]、[專案**]，然後選取 [node.js] 專案，再按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="fd09c-180">Right click the IdentityMySQLDemo project, select **Add**, **Reference, Solution, Projects;** select the AspNet.Identity.MySQL project and click **OK**.</span></span>
6. <span data-ttu-id="fd09c-181">在 IdentityMySQLDemo 專案中，將所有參考取代為</span><span class="sxs-lookup"><span data-stu-id="fd09c-181">In the IdentityMySQLDemo project, replace all references to</span></span>  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   <span data-ttu-id="fd09c-182">取代為</span><span class="sxs-lookup"><span data-stu-id="fd09c-182">with</span></span>  
     `using AspNet.Identity.MySQL;`
7. <span data-ttu-id="fd09c-183">在 IdentityModels.cs 中，將 **[applicationdbcoNtext]** 設定為衍生自**MySqlDatabase** ，並包含採用單一參數與連接名稱的函式。</span><span class="sxs-lookup"><span data-stu-id="fd09c-183">In IdentityModels.cs, set **ApplicationDbContext** to derive from **MySqlDatabase** and include a constructor that take a single parameter with the connection name.</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. <span data-ttu-id="fd09c-184">開啟 IdentityConfig.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd09c-184">Open the IdentityConfig.cs file.</span></span> <span data-ttu-id="fd09c-185">在**ApplicationUserManager**方法中，將具現化的 UserManager 取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="fd09c-185">In the **ApplicationUserManager.Create** method, replace instantiating UserManager with the following code:</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. <span data-ttu-id="fd09c-186">開啟 web.config 檔案，並將 DefaultConnection 字串取代為此專案，並將反白顯示的值取代為您在先前步驟中建立的 MySQL 資料庫連接字串：</span><span class="sxs-lookup"><span data-stu-id="fd09c-186">Open the web.config file and replace the DefaultConnection string with this entry replacing the highlighted values with the connection string of the MySQL database you created on previous steps:</span></span>  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a><span data-ttu-id="fd09c-187">執行應用程式並連接到 MySQL DB</span><span class="sxs-lookup"><span data-stu-id="fd09c-187">Run the app and connect to the MySQL DB</span></span>

1. <span data-ttu-id="fd09c-188">以滑鼠右鍵按一下**IdentityMySQLDemo**專案，然後選取 [**設定為啟始專案**]</span><span class="sxs-lookup"><span data-stu-id="fd09c-188">Right click the **IdentityMySQLDemo** project and select **Set as Startup Project**</span></span>
2. <span data-ttu-id="fd09c-189">按**Ctrl + F5**以建立並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd09c-189">Press **Ctrl + F5** to build and run the app.</span></span>
3. <span data-ttu-id="fd09c-190">按一下頁面頂端的 [**註冊**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fd09c-190">Click on **Register** tab on the top of the page.</span></span>
4. <span data-ttu-id="fd09c-191">輸入新的 [使用者名稱] 和 [密碼]，然後按一下 [**註冊**]。</span><span class="sxs-lookup"><span data-stu-id="fd09c-191">Enter a new user name and password and then click on **Register**.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. <span data-ttu-id="fd09c-192">新的使用者現在已註冊並登入。</span><span class="sxs-lookup"><span data-stu-id="fd09c-192">The new user is now registered and logged in.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. <span data-ttu-id="fd09c-193">返回 MySQL 工作臺工具，並檢查**IdentityMySQLDatabase**資料表的內容。</span><span class="sxs-lookup"><span data-stu-id="fd09c-193">Go back to the MySQL Workbench tool and inspect the **IdentityMySQLDatabase** table's contents.</span></span> <span data-ttu-id="fd09c-194">當您註冊新的使用者時，請檢查 [使用者] 資料表中的專案。</span><span class="sxs-lookup"><span data-stu-id="fd09c-194">Inspect the users table for the entries as you register new users.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a><span data-ttu-id="fd09c-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd09c-195">Next Steps</span></span>

<span data-ttu-id="fd09c-196">如需如何在此應用程式上啟用其他驗證方法的詳細資訊，請參閱[使用 Facebook 和 Google OAuth2 和 OpenID 登入建立 ASP.NET MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="fd09c-196">For more information on how to enable other authentication methods on this app, refer to [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<span data-ttu-id="fd09c-197">若要瞭解如何整合 DB 與 OAuth，並設定角色以限制使用者存取您的應用程式，請參閱將[具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署至 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="fd09c-197">To learn how to integrate your DB with OAuth and to set up roles to limit users access to your app, see [Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>
