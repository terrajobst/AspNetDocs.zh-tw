---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：遷移至 SQL Server-10/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640610"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a><span data-ttu-id="e36b8-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：遷移至 SQL Server-10/12</span><span class="sxs-lookup"><span data-stu-id="e36b8-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Migrating to SQL Server - 10 of 12</span></span>

<span data-ttu-id="e36b8-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e36b8-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e36b8-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="e36b8-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="e36b8-106">這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="e36b8-107">如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="e36b8-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="e36b8-108">如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。</span><span class="sxs-lookup"><span data-stu-id="e36b8-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="e36b8-109">如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e36b8-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="e36b8-110">概觀</span><span class="sxs-lookup"><span data-stu-id="e36b8-110">Overview</span></span>

<span data-ttu-id="e36b8-111">本教學課程說明如何從 SQL Server Compact 遷移至 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="e36b8-111">This tutorial shows you how to migrate from SQL Server Compact to SQL Server.</span></span> <span data-ttu-id="e36b8-112">其中一個原因是，您可能會想要利用 SQL Server Compact 不支援的 SQL Server 功能，例如預存程式、觸發程式、視圖或複寫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-112">One reason you might want to do that is to take advantage of SQL Server features that SQL Server Compact does not support, such as stored procedures, triggers, views, or replication.</span></span> <span data-ttu-id="e36b8-113">如需 SQL Server Compact 和 SQL Server 之間差異的詳細資訊，請參閱[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="e36b8-113">For more information about the differences between SQL Server Compact and SQL Server, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

### <a name="sql-server-express-versus-full-sql-server-for-development"></a><span data-ttu-id="e36b8-114">SQL Server Express 與完整 SQL Server 以進行開發</span><span class="sxs-lookup"><span data-stu-id="e36b8-114">SQL Server Express versus full SQL Server for Development</span></span>

<span data-ttu-id="e36b8-115">一旦決定升級至 SQL Server 之後，您可能會想要在開發和測試環境中使用 SQL Server 或 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="e36b8-115">Once you've decided to upgrade to SQL Server, you might want to use SQL Server or SQL Server Express in your development and test environments.</span></span> <span data-ttu-id="e36b8-116">除了工具支援和資料庫引擎功能的差異之外，SQL Server Compact 和其他版本的 SQL Server 之間提供者的差異。</span><span class="sxs-lookup"><span data-stu-id="e36b8-116">In addition to the differences in tool support and in database engine features, there are differences in provider implementations between SQL Server Compact and other versions of SQL Server.</span></span> <span data-ttu-id="e36b8-117">這些差異可能會導致相同的程式碼產生不同的結果。</span><span class="sxs-lookup"><span data-stu-id="e36b8-117">These differences can cause the same code to generate different results.</span></span> <span data-ttu-id="e36b8-118">因此，如果您決定將 SQL Server Compact 保留為開發資料庫，您應該在每次部署到生產環境之前，在測試環境中的 SQL Server 或 SQL Server Express 中徹底測試您的網站。</span><span class="sxs-lookup"><span data-stu-id="e36b8-118">Therefore, if you decide to keep SQL Server Compact as your development database, you should thoroughly test your site in SQL Server or SQL Server Express in a test environment before each deployment to production.</span></span>

<span data-ttu-id="e36b8-119">不同于 SQL Server Compact，SQL Server Express 基本上是相同的資料庫引擎，並使用與完整 SQL Server 相同的 .NET 提供者。</span><span class="sxs-lookup"><span data-stu-id="e36b8-119">Unlike SQL Server Compact, SQL Server Express is essentially the same database engine and uses the same .NET provider as full SQL Server.</span></span> <span data-ttu-id="e36b8-120">當您使用 SQL Server Express 進行測試時，您可以放心取得與 SQL Server 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="e36b8-120">When you test with SQL Server Express, you can be confident of getting the same results as you will with SQL Server.</span></span> <span data-ttu-id="e36b8-121">您可以使用與 SQL Server Express 搭配使用的大部分相同資料庫工具，SQL Server （ [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)的值得注意的例外狀況），並支援其他 SQL Server 的功能，例如預存程式、視圖、觸發程式和複寫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-121">You can use most of the same database tools with SQL Server Express that you can use with SQL Server (a notable exception being [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), and it supports other features of SQL Server like stored procedures, views, triggers, and replication.</span></span> <span data-ttu-id="e36b8-122">（不過，您通常必須在生產網站中使用完整的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="e36b8-122">(You typically have to use full SQL Server in a production website, however.</span></span> <span data-ttu-id="e36b8-123">SQL Server Express 可以在共用的主控環境中執行，但它不是專為它所設計，而且許多主機提供者都不支援）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-123">SQL Server Express can run in a shared hosting environment, but it was not designed for that, and many hosting providers do not support it.)</span></span>

<span data-ttu-id="e36b8-124">如果您使用 Visual Studio 2012，通常會為您的開發環境選擇 SQL Server Express LocalDB，因為這是預設會隨 Visual Studio 安裝的內容。</span><span class="sxs-lookup"><span data-stu-id="e36b8-124">If you are using Visual Studio 2012, you typically choose SQL Server Express LocalDB for your development environment because that is what is installed by default with Visual Studio.</span></span> <span data-ttu-id="e36b8-125">不過，LocalDB 無法在 IIS 中運作，因此針對您的測試環境，您必須使用 SQL Server 或 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="e36b8-125">However, LocalDB does not work in IIS, so for your test environment you have to use either SQL Server or SQL Server Express.</span></span>

### <a name="combining-databases-versus-keeping-them-separate"></a><span data-ttu-id="e36b8-126">結合資料庫與保持獨立</span><span class="sxs-lookup"><span data-stu-id="e36b8-126">Combining Databases versus Keeping Them Separate</span></span>

<span data-ttu-id="e36b8-127">Contoso 大學應用程式有兩個 SQL Server Compact 資料庫：成員資格資料庫（*aspnet .sdf*）和應用程式資料庫（*School .sdf*）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-127">The Contoso University application has two SQL Server Compact databases: the membership database (*aspnet.sdf*) and the application database (*School.sdf*).</span></span> <span data-ttu-id="e36b8-128">當您遷移時，可以將這些資料庫移轉至兩個不同的資料庫或單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-128">When you migrate, you can migrate these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="e36b8-129">您可能想要結合這些專案，以便在應用程式資料庫與成員資格資料庫之間進行資料庫聯結。</span><span class="sxs-lookup"><span data-stu-id="e36b8-129">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="e36b8-130">您的主控方案也可能提供組合的原因。</span><span class="sxs-lookup"><span data-stu-id="e36b8-130">Your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="e36b8-131">例如，主機服務提供者可能會對多個資料庫收取更多費用，或甚至不允許一個以上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-131">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span> <span data-ttu-id="e36b8-132">這就是在本教學課程中使用的 Cytanium Lite 主控帳戶的情況，只允許單一 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-132">That's the case with the Cytanium Lite hosting account that's used for this tutorial, which allows only a single SQL Server database.</span></span>

<span data-ttu-id="e36b8-133">在本教學課程中，您將以這種方式遷移兩個資料庫：</span><span class="sxs-lookup"><span data-stu-id="e36b8-133">In this tutorial, you'll migrate your two databases this way:</span></span>

- <span data-ttu-id="e36b8-134">遷移至開發環境中的兩個 LocalDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-134">Migrate to two LocalDB databases in the development environment.</span></span>
- <span data-ttu-id="e36b8-135">遷移至測試環境中的兩個 SQL Server Express 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-135">Migrate to two SQL Server Express databases in the test environment.</span></span>
- <span data-ttu-id="e36b8-136">遷移至生產環境中的一個合併完整 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-136">Migrate to one combined full SQL Server database in the production environment.</span></span>

<span data-ttu-id="e36b8-137">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="e36b8-137">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="installing-sql-server-express"></a><span data-ttu-id="e36b8-138">安裝 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="e36b8-138">Installing SQL Server Express</span></span>

<span data-ttu-id="e36b8-139">SQL Server Express 預設會隨 Visual Studio 2010 自動安裝，但根據預設，它不會隨 Visual Studio 2012 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="e36b8-139">SQL Server Express is automatically installed by default with Visual Studio 2010, but by default it is not installed with Visual Studio 2012.</span></span> <span data-ttu-id="e36b8-140">若要安裝 SQL Server 2012 Express，請按一下下列連結</span><span class="sxs-lookup"><span data-stu-id="e36b8-140">To install SQL Server 2012 Express, click the following link</span></span>

- [<span data-ttu-id="e36b8-141">SQL Server Express 2012</span><span class="sxs-lookup"><span data-stu-id="e36b8-141">SQL Server Express 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=29062)

<span data-ttu-id="e36b8-142">選擇*繁體中文/x64/SQLEXPR\_x64\_繁體中文*或*繁體中文/x86/SQLEXPR\_x86\_繁體中文 .exe*，然後在安裝精靈中接受預設設定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-142">Choose *ENU/x64/SQLEXPR\_x64\_ENU.exe* or *ENU/x86/SQLEXPR\_x86\_ENU.exe*, and in the installation wizard accept the default settings.</span></span> <span data-ttu-id="e36b8-143">如需安裝選項的詳細資訊，請參閱[從安裝精靈安裝 SQL Server 2012 （安裝程式）](https://msdn.microsoft.com/library/ms143219.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e36b8-143">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="e36b8-144">建立測試環境的 SQL Server Express 資料庫</span><span class="sxs-lookup"><span data-stu-id="e36b8-144">Creating SQL Server Express Databases for the Test Environment</span></span>

<span data-ttu-id="e36b8-145">下一步是建立 ASP.NET 成員資格和學校資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-145">The next step is to create the ASP.NET membership and School databases.</span></span>

<span data-ttu-id="e36b8-146">從  **View**  功能表選取 **伺服器總管**（Visual Web Developer 中的**資料庫總管**），然後以滑鼠右鍵按一下 **資料連線**，然後選取 **建立新的 SQL Server 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="e36b8-146">From the **View** menu select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

<span data-ttu-id="e36b8-148">在 [**建立新的 SQL Server 資料庫**] 對話方塊中，于 [**伺服器名稱**] 方塊中輸入 ".\SQLExpress"，並在 [**新資料庫名稱**] 方塊中輸入 "aspnet-Test"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="e36b8-148">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-Test" in the **New database name** box, then click **OK**.</span></span>

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

<span data-ttu-id="e36b8-150">遵循相同的程式，建立名為「學校測試」的新 SQL Server Express School 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-150">Follow the same procedure to create a new SQL Server Express School database named "School-Test".</span></span>

<span data-ttu-id="e36b8-151">（您會將「測試」附加至這些資料庫名稱，因為稍後您會針對開發環境建立每個資料庫的額外實例，而且您必須能夠區分這兩組資料庫）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-151">(You're appending "Test" to these database names because later you'll create an additional instance of each database for the development environment, and you need to be able to differentiate the two sets of databases.)</span></span>

<span data-ttu-id="e36b8-152">**伺服器總管**現在會顯示兩個新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-152">**Server Explorer** now shows the two new databases.</span></span>

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a><span data-ttu-id="e36b8-154">建立新資料庫的授與腳本</span><span class="sxs-lookup"><span data-stu-id="e36b8-154">Creating a Grant Script for the New Databases</span></span>

<span data-ttu-id="e36b8-155">當應用程式在開發電腦上的 IIS 中執行時，應用程式會使用預設應用程式集區的認證來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-155">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="e36b8-156">不過，根據預設，應用程式集區識別沒有開啟資料庫的許可權。</span><span class="sxs-lookup"><span data-stu-id="e36b8-156">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="e36b8-157">因此，您必須執行腳本以授與該許可權。</span><span class="sxs-lookup"><span data-stu-id="e36b8-157">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="e36b8-158">在本節中，您會建立稍後將執行的腳本，以確保應用程式在 IIS 中執行時可以開啟資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-158">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="e36b8-159">在您于[部署到生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中建立的解決方案*SolutionFiles*資料夾中，建立名為*Grant .sql*的新 sql 檔案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-159">In the solution's *SolutionFiles* folder that you created in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, create a new SQL file named *Grant.sql*.</span></span> <span data-ttu-id="e36b8-160">將下列 SQL 命令複製到檔案中，然後儲存並關閉檔案：</span><span class="sxs-lookup"><span data-stu-id="e36b8-160">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> <span data-ttu-id="e36b8-161">此腳本是設計來搭配使用 SQL Server 2008 和 Windows 7 中的 IIS 設定，如同在本教學課程中所指定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-161">This script is designed to work with SQL Server 2008 and with the IIS settings in Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="e36b8-162">如果您使用不同版本的 SQL Server 或 Windows，或如果您在電腦上以不同的方式設定 IIS，則可能需要變更此腳本。</span><span class="sxs-lookup"><span data-stu-id="e36b8-162">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="e36b8-163">如需 SQL Server 腳本的詳細資訊，請參閱[SQL Server 線上叢書](https://go.microsoft.com/fwlink/?LinkId=132511)。</span><span class="sxs-lookup"><span data-stu-id="e36b8-163">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e36b8-164">**安全性注意事項**此腳本會將資料庫\_擁有者許可權授與在執行時間存取資料庫的使用者，這就是您在生產環境中擁有的功能。</span><span class="sxs-lookup"><span data-stu-id="e36b8-164">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="e36b8-165">在某些情況下，您可能會想要指定具有完整資料庫架構更新許可權的使用者，只供部署之用，並為執行時間指定僅具有讀取和寫入資料許可權的其他使用者。</span><span class="sxs-lookup"><span data-stu-id="e36b8-165">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="e36b8-166">如需詳細資訊，請參閱在[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)中，**檢查 Code First 移轉的自動 web.config 變更**。</span><span class="sxs-lookup"><span data-stu-id="e36b8-166">For more information, see **Reviewing the Automatic Web.config Changes for Code First Migrations** in [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md).</span></span>

## <a name="configuring-database-deployment-for-the-test-environment"></a><span data-ttu-id="e36b8-167">設定測試環境的資料庫部署</span><span class="sxs-lookup"><span data-stu-id="e36b8-167">Configuring Database Deployment for the Test Environment</span></span>

<span data-ttu-id="e36b8-168">接下來，您將設定 Visual Studio，讓它針對每個資料庫執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="e36b8-168">Next, you'll configure Visual Studio so that it will do the following tasks for each database:</span></span>

- <span data-ttu-id="e36b8-169">產生 SQL 腳本，以在目的地資料庫中建立源資料庫的結構（資料表、資料行、條件約束等）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-169">Generate a SQL script that creates the source database's structure (tables, columns, constraints, etc.) in the destination database.</span></span>
- <span data-ttu-id="e36b8-170">產生 SQL 腳本，將源資料庫的資料插入目的地資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="e36b8-170">Generate a SQL script that inserts the source database's data into the tables in the destination database.</span></span>
- <span data-ttu-id="e36b8-171">在目的地資料庫中執行產生的腳本，以及您所建立的授與腳本。</span><span class="sxs-lookup"><span data-stu-id="e36b8-171">Run the generated scripts, and the Grant script that you created, in the destination database.</span></span>

<span data-ttu-id="e36b8-172">開啟 [**專案屬性**] 視窗，然後選取 [**封裝/發行 SQL** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-172">Open the **Project Properties** window and select the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="e36b8-173">請確定已**在 [設定**] 下拉式清單中選取 [使用中 **（發行）** ] 或 [**發行**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-173">Make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="e36b8-174">按一下 [**啟用此頁面**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-174">Click **Enable this Page**.</span></span>

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

<span data-ttu-id="e36b8-176">[**封裝/發行 SQL** ] 索引標籤通常是停用的，因為它會指定舊版部署方法。</span><span class="sxs-lookup"><span data-stu-id="e36b8-176">The **Package/Publish SQL** tab is normally disabled because it specifies a legacy deployment method.</span></span> <span data-ttu-id="e36b8-177">在大部分的情況下，您應該在 [**發行 Web** wizard] 中設定資料庫部署。</span><span class="sxs-lookup"><span data-stu-id="e36b8-177">For most scenarios, you should configure database deployment in the **Publish Web** wizard.</span></span> <span data-ttu-id="e36b8-178">從 SQL Server Compact 遷移至 SQL Server 或 SQL Server Express 是一個特別的案例，此方法是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="e36b8-178">Migrating from SQL Server Compact to SQL Server or SQL Server Express is a special case for which this method is a good choice.</span></span>

<span data-ttu-id="e36b8-179">按一下 [從 web.config 匯**入**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-179">Click **Import from Web.config**.</span></span>

![Selecting_Import_from_Web .config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

<span data-ttu-id="e36b8-181">Visual Studio 會*在 web.config 檔案*中尋找連接字串，尋找一個用於成員資格資料庫，另一個用於 School 資料庫，並在**資料庫專案**資料表中加入一個對應于每個連接字串的資料列。</span><span class="sxs-lookup"><span data-stu-id="e36b8-181">Visual Studio looks for connection strings in the *Web.config* file, finds one for the membership database and one for the School database, and adds a row corresponding to each connection string in the **Database Entries** table.</span></span> <span data-ttu-id="e36b8-182">它所找到的連接字串適用于現有的 SQL Server Compact 資料庫，而下一個步驟則是設定這些資料庫的部署方式和位置。</span><span class="sxs-lookup"><span data-stu-id="e36b8-182">The connection strings it finds are for the existing SQL Server Compact databases, and your next step will be to configure how and where to deploy these databases.</span></span>

<span data-ttu-id="e36b8-183">您會在 [資料庫專案**詳細資料**] 區段中的 [**資料庫專案**] 資料表底下，輸入資料庫部署設定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-183">You enter database deployment settings in the **Database Entry Details** section below the **Database Entries** table.</span></span> <span data-ttu-id="e36b8-184">[**資料庫專案詳細資料**] 區段中顯示的設定，會與 [**資料庫專案**] 資料表中的任何資料列相關，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="e36b8-184">The settings shown in the **Database Entry Details** section pertain to whichever row in the **Database Entries** table is selected, as shown in the following illustration.</span></span>

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="e36b8-186">設定成員資格資料庫的部署設定</span><span class="sxs-lookup"><span data-stu-id="e36b8-186">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="e36b8-187">選取 [**資料庫專案**] 資料表中的 [ **DefaultConnection-部署**] 資料列，以進行設定以套用至成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-187">Select the **DefaultConnection-Deployment** row in the **Database Entries** table in order to configure settings that apply to the membership database.</span></span>

<span data-ttu-id="e36b8-188">在 [**目的地資料庫的連接字串**] 中，輸入指向新 SQL Server Express 成員資格資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-188">In **Connection string for destination database**, enter a connection string that points to the new SQL Server Express membership database.</span></span> <span data-ttu-id="e36b8-189">您可以從**伺服器總管**取得所需的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-189">You can get the connection string you need from **Server Explorer**.</span></span> <span data-ttu-id="e36b8-190">在**伺服器總管**中，展開 [**資料**連線] 並選取 [ **aspnetTest** ] 資料庫，然後從 [**屬性**] 視窗複製 [**連接字串**] 值。</span><span class="sxs-lookup"><span data-stu-id="e36b8-190">In **Server Explorer**, expand **Data Connections** and select the **aspnetTest** database, then from the **Properties** window copy the **Connection String** value.</span></span>

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

<span data-ttu-id="e36b8-192">相同的連接字串會在此重現：</span><span class="sxs-lookup"><span data-stu-id="e36b8-192">The same connection string is reproduced here:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

<span data-ttu-id="e36b8-193">在 [**封裝/發行 SQL** ] 索引標籤中，將此連接字串複製並貼到**目的地資料庫的連接字串**中。</span><span class="sxs-lookup"><span data-stu-id="e36b8-193">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="e36b8-194">請確定已選取 [**從現有資料庫提取資料及/或架構**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-194">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span> <span data-ttu-id="e36b8-195">這會導致在目的地資料庫中自動產生並執行 SQL 腳本。</span><span class="sxs-lookup"><span data-stu-id="e36b8-195">This is what causes SQL scripts to be automatically generated and run in the destination database.</span></span>

<span data-ttu-id="e36b8-196">**源資料庫值的連接字串**會從*web.config*檔案中解壓縮，並指向開發 SQL Server Compact 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-196">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="e36b8-197">這是將用來產生稍後將在目的地資料庫中執行之腳本的源資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-197">This is the source database that will be used to generate the scripts that will run later in the destination database.</span></span> <span data-ttu-id="e36b8-198">由於您想要部署資料庫的實際執行版本，因此請將 "aspnet-Dev" 變更為 "aspnet-Prod"。</span><span class="sxs-lookup"><span data-stu-id="e36b8-198">Since you want to deploy the production version of the database, change "aspnet-Dev.sdf" to "aspnet-Prod.sdf".</span></span>

<span data-ttu-id="e36b8-199">因為您想要複製資料（使用者帳戶和角色）以及資料庫結構，所以請將**資料庫腳本選項**從**架構**變更為**架構和資料**。</span><span class="sxs-lookup"><span data-stu-id="e36b8-199">Change **Database scripting options** from **Schema Only** to **Schema and data**, since you want to copy your data (user accounts and roles) as well as the database structure.</span></span>

<span data-ttu-id="e36b8-200">若要將部署設定為執行您稍早建立的授與腳本，您必須將它們新增至 [**資料庫腳本**] 區段。</span><span class="sxs-lookup"><span data-stu-id="e36b8-200">To configure deployment to run the grant scripts that you created earlier, you have to add them to the **Database Scripts** section.</span></span> <span data-ttu-id="e36b8-201">按一下 [**新增腳本**]，然後在 [**加入 SQL 腳本**] 對話方塊中，流覽至您儲存授與腳本的資料夾（這是包含您的方案檔的資料夾）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-201">Click **Add Script**, and in the **Add SQL Scripts** dialog box, navigate to the folder where you stored the grant script (this is the folder that contains your solution file).</span></span> <span data-ttu-id="e36b8-202">選取名為*Grant .sql*的檔案，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-202">Select the file named *Grant.sql*, and click **Open**.</span></span>

<span data-ttu-id="e36b8-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="e36b8-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span></span>

<span data-ttu-id="e36b8-204">[**資料庫專案**] 中 [ **DefaultConnection] 部署**資料列的設定現在看起來如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e36b8-204">The settings for the **DefaultConnection-Deployment** row in **Database Entries** now look like the following illustration:</span></span>

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="e36b8-206">配置 School 資料庫的部署設定</span><span class="sxs-lookup"><span data-stu-id="e36b8-206">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="e36b8-207">接下來，選取 [**資料庫專案**] 資料表中的 [ **SchoolCoNtext-部署**] 資料列，以便設定 School 資料庫的部署設定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-207">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure deployment settings for the School database.</span></span>

<span data-ttu-id="e36b8-208">您可以使用先前所用的相同方法來取得新 SQL Server Express 資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-208">You can use the same method you used earlier to get the connection string for the new SQL Server Express database.</span></span> <span data-ttu-id="e36b8-209">在 [**封裝/發行 SQL** ] 索引標籤中，將此連接字串複製到**目的地資料庫的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="e36b8-209">Copy this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

<span data-ttu-id="e36b8-210">請確定已選取 [**從現有資料庫提取資料及/或架構**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-210">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span>

<span data-ttu-id="e36b8-211">**源資料庫值的連接字串**會從*web.config*檔案中解壓縮，並指向開發 SQL Server Compact 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-211">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="e36b8-212">將 "School-Dev" 變更為 "School-Prod"，以部署資料庫的實際執行版本。</span><span class="sxs-lookup"><span data-stu-id="e36b8-212">Change "School-Dev.sdf" to "School-Prod.sdf" to deploy the production version of the database.</span></span> <span data-ttu-id="e36b8-213">（您從未在\_Data 資料夾的應用程式中建立了 School-Prod .sdf 檔案，因此您稍後會從測試環境將該檔案複製到 ContosoUniversity 專案資料夾中的應用程式\_Data 資料夾）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-213">(You never created a School-Prod.sdf file in the App\_Data folder, so you'll copy that file from the test environment to the App\_Data folder in the ContosoUniversity project folder later.)</span></span>

<span data-ttu-id="e36b8-214">將**資料庫腳本選項**變更為**架構和資料**。</span><span class="sxs-lookup"><span data-stu-id="e36b8-214">Change **Database scripting options** to **Schema and data**.</span></span>

<span data-ttu-id="e36b8-215">您也會想要執行腳本，將此資料庫的讀取和寫入權限授與應用程式集區身分識別，因此，請依照您為成員資格資料庫所做的方式新增*grant .sql*腳本檔。</span><span class="sxs-lookup"><span data-stu-id="e36b8-215">You also want to run the script to grant read and write permission for this database to the application pool identity, so add the *Grant.sql* script file as you did for the membership database.</span></span>

<span data-ttu-id="e36b8-216">當您完成時，**資料庫專案**中**SchoolCoNtext 部署**資料列的設定看起來會像下圖：</span><span class="sxs-lookup"><span data-stu-id="e36b8-216">When you're done, the settings for the **SchoolContext-Deployment** row in **Database Entries** look like the following illustration:</span></span>

![Database_Entry_Details_for_SchoolCoNtext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

<span data-ttu-id="e36b8-218">將變更儲存至 [**封裝/發行 SQL** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-218">Save the changes to the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="e36b8-219">從*c:\inetpub\wwwroot\ContosoUniversity\App\_data*資料夾將*School-Prod .sdf*檔案複製到 ContosoUniversity 專案中的*應用程式\_data*資料夾。</span><span class="sxs-lookup"><span data-stu-id="e36b8-219">Copy the *School-Prod.sdf* file from the *c:\inetpub\wwwroot\ContosoUniversity\App\_Data* folder to the *App\_Data* folder in the ContosoUniversity project.</span></span>

### <a name="specifying-transacted-mode-for-the-grant-script"></a><span data-ttu-id="e36b8-220">指定授與腳本的交易模式</span><span class="sxs-lookup"><span data-stu-id="e36b8-220">Specifying Transacted Mode for the Grant Script</span></span>

<span data-ttu-id="e36b8-221">部署程式會產生可部署資料庫架構和資料的腳本。</span><span class="sxs-lookup"><span data-stu-id="e36b8-221">The deployment process generates scripts that deploy the database schema and data.</span></span> <span data-ttu-id="e36b8-222">根據預設，這些腳本會在交易中執行。</span><span class="sxs-lookup"><span data-stu-id="e36b8-222">By default, these scripts run in a transaction.</span></span> <span data-ttu-id="e36b8-223">不過，自訂腳本（例如授與腳本）預設不會在交易中執行。</span><span class="sxs-lookup"><span data-stu-id="e36b8-223">However, custom scripts (like the grant scripts) by default do not run in a transaction.</span></span> <span data-ttu-id="e36b8-224">如果部署程式混合了交易模式，當腳本在部署期間執行時，您可能會收到逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-224">If the deployment process mixes transaction modes, you might get a timeout error when the scripts run during deployment.</span></span> <span data-ttu-id="e36b8-225">在本節中，您會編輯專案檔，以便將自訂腳本設定為在交易中執行。</span><span class="sxs-lookup"><span data-stu-id="e36b8-225">In this section, you edit the project file in order to configure the custom scripts to run in a transaction.</span></span>

<span data-ttu-id="e36b8-226">在**方案總管**中，以滑鼠右鍵按一下**ContosoUniversity**專案，然後選取 **[卸載專案**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-226">In **Solution Explorer**, right-click the **ContosoUniversity** project and select **Unload Project**.</span></span>

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

<span data-ttu-id="e36b8-228">然後再次以滑鼠右鍵按一下專案，然後選取 [**編輯 ContosoUniversity**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-228">Then right-click the project again and select **Edit ContosoUniversity.csproj**.</span></span>

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

<span data-ttu-id="e36b8-230">[Visual Studio 編輯器] 會顯示專案檔的 XML 內容。</span><span class="sxs-lookup"><span data-stu-id="e36b8-230">The Visual Studio editor shows you the XML content of the project file.</span></span> <span data-ttu-id="e36b8-231">請注意，有數個 `PropertyGroup` 元素。</span><span class="sxs-lookup"><span data-stu-id="e36b8-231">Notice that there are several `PropertyGroup` elements.</span></span> <span data-ttu-id="e36b8-232">（在影像中，已省略 `PropertyGroup` 元素的內容）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-232">(In the image, the contents of the `PropertyGroup` elements have been omitted.)</span></span>

![專案檔案編輯器視窗](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

<span data-ttu-id="e36b8-234">第一個沒有 `Condition` 屬性的，就是適用于不論組建設定為何的設定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-234">The first one, which has no `Condition` attribute, is for settings that apply regardless of build configuration.</span></span> <span data-ttu-id="e36b8-235">一個 `PropertyGroup` 元素僅適用于 Debug 組建設定（請注意 `Condition` 屬性），一個僅適用于發行組建設定，另一個僅適用于測試組建設定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-235">One `PropertyGroup` element applies only to the Debug build configuration (note the `Condition` attribute), one applies only to the Release build configuration, and one applies only to the Test build configuration.</span></span> <span data-ttu-id="e36b8-236">在發行組建設定的 `PropertyGroup` 元素中，您會看到 `PublishDatabaseSettings` 元素，其中包含您在 [**封裝/發行 SQL** ] 索引標籤上輸入的設定。有一個 `Object` 元素對應到您指定的每個授與腳本（請注意兩個 "Grant. sql" 實例）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-236">Within the `PropertyGroup` element for the Release build configuration, you'll see a `PublishDatabaseSettings` element that contains the settings you entered on the **Package/Publish SQL** tab. There is an `Object` element that corresponds to each of the grant scripts you specified (notice the two instances of "Grant.sql").</span></span> <span data-ttu-id="e36b8-237">根據預設，每個授與腳本的 `Source` 元素的 `Transacted` 屬性都會 `False`。</span><span class="sxs-lookup"><span data-stu-id="e36b8-237">By default, the `Transacted` attribute of the `Source` element for each grant script is `False`.</span></span>

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

<span data-ttu-id="e36b8-239">將 `Source` 元素的 `Transacted` 屬性值變更為 [`True`]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-239">Change the value of the `Transacted` attribute of the `Source` element to `True`.</span></span>

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

<span data-ttu-id="e36b8-241">儲存並關閉專案檔，然後以滑鼠右鍵按一下**方案總管**中的專案，然後選取 [**重載專案**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-241">Save and close the project file, and then right-click the project in **Solution Explorer** and select **Reload Project**.</span></span>

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a><span data-ttu-id="e36b8-243">設定連接字串的 web.config 轉換</span><span class="sxs-lookup"><span data-stu-id="e36b8-243">Setting up Web.Config Transformations for the Connection Strings</span></span>

<span data-ttu-id="e36b8-244">您在 [**封裝/發行 SQL** ] 索引標籤上輸入之新 SQL Express 資料庫的連接字串，僅供 Web Deploy 在部署期間用來更新目的地資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-244">The connection strings for the new SQL Express databases that you entered on the **Package/Publish SQL** tab are used by Web Deploy only for updating the destination database during deployment.</span></span> <span data-ttu-id="e36b8-245">您仍然必須設定*web.config*轉換，*讓部署的 web.config 檔案*中的連接字串指向新的 SQL Server Express 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-245">You still have to set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file point to the new SQL Server Express databases.</span></span> <span data-ttu-id="e36b8-246">（當您使用 [**封裝/發行 SQL** ] 索引標籤時，您無法在發行設定檔中設定連接字串）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-246">(When you use the **Package/Publish SQL** tab, you can't configure connection strings in the publish profile.)</span></span>

<span data-ttu-id="e36b8-247">開啟*web.config* ，並將 `connectionStrings` 元素取代為下列範例中的 `connectionStrings` 元素。</span><span class="sxs-lookup"><span data-stu-id="e36b8-247">Open *Web.Test.config* and replace the `connectionStrings` element with the `connectionStrings` element in the following example.</span></span> <span data-ttu-id="e36b8-248">（請確定您只複製 connectionStrings 元素，而不是此處顯示的周圍程式碼來提供內容）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-248">(Make sure you only copy the connectionStrings element, not the surrounding code that is shown here to provide context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

<span data-ttu-id="e36b8-249">此程式碼會在部署的*web.config*檔案中，取代每個 `add` 元素的 `connectionString` 和 `providerName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="e36b8-249">This code causes the `connectionString` and `providerName` attributes of each `add` element to be replaced in the deployed *Web.config* file.</span></span> <span data-ttu-id="e36b8-250">這些連接字串與您在 [**封裝/發行 SQL** ] 索引標籤中輸入的不同。已新增 "MultipleActiveResultSets = True" 設定，因為它是 Entity Framework 和 Universal Providers 的必要專案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-250">These connection strings are not identical to the ones you entered in the **Package/Publish SQL** tab. The setting "MultipleActiveResultSets=True" has been added to them because it's required for the Entity Framework and the Universal Providers.</span></span>

## <a name="installing-sql-server-compact"></a><span data-ttu-id="e36b8-251">安裝 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="e36b8-251">Installing SQL Server Compact</span></span>

<span data-ttu-id="e36b8-252">Entityframework.sqlservercompact NuGet 套件提供 Contoso 大學應用程式的 SQL Server Compact database engine 元件。</span><span class="sxs-lookup"><span data-stu-id="e36b8-252">The SqlServerCompact NuGet package provides the SQL Server Compact database engine assemblies for the Contoso University application.</span></span> <span data-ttu-id="e36b8-253">但是現在不是應用程式，但是 Web Deploy 必須能夠讀取 SQL Server Compact 資料庫，才能建立腳本以在 SQL Server 資料庫中執行。</span><span class="sxs-lookup"><span data-stu-id="e36b8-253">But now it is not the application but Web Deploy that must be able to read the SQL Server Compact databases, in order to create scripts to run in the SQL Server databases.</span></span> <span data-ttu-id="e36b8-254">若要讓 Web Deploy 讀取 SQL Server Compact 資料庫，請使用下列連結在開發電腦上安裝 SQL Server Compact： [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)。</span><span class="sxs-lookup"><span data-stu-id="e36b8-254">To enable Web Deploy to read SQL Server Compact databases, install SQL Server Compact on the development computer by using the following link: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6).</span></span>

## <a name="deploying-to-the-test-environment"></a><span data-ttu-id="e36b8-255">部署到測試環境</span><span class="sxs-lookup"><span data-stu-id="e36b8-255">Deploying to the Test Environment</span></span>

<span data-ttu-id="e36b8-256">若要發行至測試環境，您必須建立發行設定檔，並將其設定為使用 [**封裝/發行 SQL** ] 索引標籤來發行資料庫，而不是發行設定檔資料庫設定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-256">In order to publish to the Test environment, you have to create a publish profile that is configured to use the **Package/Publish SQL** tab for database publishing instead of the publish profile database settings.</span></span>

<span data-ttu-id="e36b8-257">首先，刪除現有的測試組態檔。</span><span class="sxs-lookup"><span data-stu-id="e36b8-257">First, delete the existing Test profile.</span></span>

<span data-ttu-id="e36b8-258">在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-258">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="e36b8-259">選取 [**設定檔**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-259">Select the **Profile** tab.</span></span>

<span data-ttu-id="e36b8-260">按一下 [**管理設定檔**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-260">Click **Manage Profiles**.</span></span>

<span data-ttu-id="e36b8-261">選取 [**測試**]，按一下 [**移除**]，然後按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-261">Select **Test**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="e36b8-262">關閉 [**發行 Web** wizard] 以儲存此變更。</span><span class="sxs-lookup"><span data-stu-id="e36b8-262">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="e36b8-263">接下來，建立新的測試組態檔，並使用它來發行專案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-263">Next, create a new Test profile and use it to publish the project.</span></span>

<span data-ttu-id="e36b8-264">在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-264">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="e36b8-265">選取 [**設定檔**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-265">Select the **Profile** tab.</span></span>

<span data-ttu-id="e36b8-266">從下拉式清單中選取 **&lt;新增 ...&gt;** ，然後輸入 "Test" 作為設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="e36b8-266">Select **&lt;New...&gt;** from the drop-down list, and enter "Test" as the profile name.</span></span>

<span data-ttu-id="e36b8-267">在 [**服務 URL** ] 方塊中，輸入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="e36b8-267">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="e36b8-268">在 [**網站/應用程式**] 方塊中，輸入*Default Web Site/ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="e36b8-268">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="e36b8-269">在 [**目的地 URL** ] 方塊中，輸入 `http://localhost/ContosoUniversity/`。</span><span class="sxs-lookup"><span data-stu-id="e36b8-269">In the **Destination URL** box, enter `http://localhost/ContosoUniversity/`.</span></span>

<span data-ttu-id="e36b8-270">按 [ **下一步**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-270">Click **Next**.</span></span>

<span data-ttu-id="e36b8-271">[**設定**] 索引標籤會警告您已設定 [**封裝/發行 SQL** ] 索引標籤，並可讓您按一下 [啟用新的資料庫發行增強功能] 來覆寫這些索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-271">The **Settings** tab warns you that the **Package/Publish SQL** tab has been configured, and it gives you an opportunity to override them by clicking enable the new database publishing improvements.</span></span> <span data-ttu-id="e36b8-272">在此部署中，您不想要覆寫 [**封裝/發行 SQL** ] 索引標籤設定，因此只要按 **[下一步**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-272">For this deployment you don't want to override the **Package/Publish SQL** tab settings, so just click **Next**.</span></span>

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

<span data-ttu-id="e36b8-274">[**預覽**] 索引標籤上的訊息指出**未選取要發行的任何資料庫**，但這只表示發行設定檔中未設定資料庫發行。</span><span class="sxs-lookup"><span data-stu-id="e36b8-274">A message on the **Preview** tab indicates that **No databases are selected to publish**, but this only means that database publishing is not configured in the publish profile.</span></span>

<span data-ttu-id="e36b8-275">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-275">Click **Publish**.</span></span>

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

<span data-ttu-id="e36b8-277">Visual Studio 部署應用程式，並在測試環境中將瀏覽器開啟至網站的首頁。</span><span class="sxs-lookup"><span data-stu-id="e36b8-277">Visual Studio deploys the application and opens the browser to the home page of the site in the test environment.</span></span> <span data-ttu-id="e36b8-278">執行 [講師] 頁面，以查看它是否顯示您稍早看到的相同資料。</span><span class="sxs-lookup"><span data-stu-id="e36b8-278">Run the Instructors page to see that it displays the same data that you saw earlier.</span></span> <span data-ttu-id="e36b8-279">執行 [**新增學生**] 頁面，新增學生，然後在 [**學生**] 頁面中查看新學生。</span><span class="sxs-lookup"><span data-stu-id="e36b8-279">Run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="e36b8-280">這會確認您可以更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-280">This verifies that the you can update the database.</span></span> <span data-ttu-id="e36b8-281">選取 [**更新信用額度**] 頁面（您必須登入）以確認成員資格資料庫已部署，而且您有其存取權。</span><span class="sxs-lookup"><span data-stu-id="e36b8-281">Select the **Update Credits** page (you'll need to log in) to verify that the membership database was deployed and you have access to it.</span></span>

## <a name="creating-a-sql-server-database-for-the-production-environment"></a><span data-ttu-id="e36b8-282">建立生產環境的 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="e36b8-282">Creating a SQL Server Database for the Production Environment</span></span>

<span data-ttu-id="e36b8-283">現在您已部署到測試環境，您已準備好設定部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="e36b8-283">Now that you've deployed to the test environment, you're ready to set up deployment to production.</span></span> <span data-ttu-id="e36b8-284">您可以藉由建立要部署的資料庫來開始進行測試環境。</span><span class="sxs-lookup"><span data-stu-id="e36b8-284">You begin as you did for the test environment, by creating a database to deploy to.</span></span> <span data-ttu-id="e36b8-285">當您從總覽中回想過，Cytanium Lite 主控方案只允許單一 SQL Server 資料庫，因此您只會設定一個資料庫，而不是兩個。</span><span class="sxs-lookup"><span data-stu-id="e36b8-285">As you recall from the Overview, the Cytanium Lite hosting plan only allows a single SQL Server database, so you will set up only one database, not two.</span></span> <span data-ttu-id="e36b8-286">成員資格和學校 SQL Server Compact 資料庫中的所有資料表和資料，都會部署到生產環境中的一個 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-286">All of the tables and data from the membership and School SQL Server Compact databases will be deployed into one SQL Server database in production.</span></span>

<span data-ttu-id="e36b8-287">移至[http://panel.cytanium.com](http://panel.cytanium.com)的 [Cytanium] 控制台。</span><span class="sxs-lookup"><span data-stu-id="e36b8-287">Go to the Cytanium control panel at [http://panel.cytanium.com](http://panel.cytanium.com).</span></span> <span data-ttu-id="e36b8-288">按住滑鼠停留在**資料庫**上，然後按一下 [ **SQL Server 2008**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-288">Hold the mouse over **Databases** and then click **SQL Server 2008**.</span></span>

<span data-ttu-id="e36b8-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="e36b8-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span></span>

<span data-ttu-id="e36b8-290">在 [ **SQL Server 2008** ] 頁面中，按一下 [**建立資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-290">In the **SQL Server 2008** page, click **Create Database**.</span></span>

<span data-ttu-id="e36b8-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="e36b8-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span></span>

<span data-ttu-id="e36b8-292">將資料庫命名為 "School"，然後按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-292">Name the database "School" and click **Save**.</span></span> <span data-ttu-id="e36b8-293">（此頁面會自動新增前置詞 "contosou"，因此有效的名稱會是 "contosouSchool"）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-293">(The page automatically adds the prefix "contosou", so the effective name will be "contosouSchool".)</span></span>

<span data-ttu-id="e36b8-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="e36b8-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span></span>

<span data-ttu-id="e36b8-295">在相同的頁面上，按一下 [**建立使用者**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-295">On the same page, click **Create User**.</span></span> <span data-ttu-id="e36b8-296">在 Cytanium 的伺服器上，而不是使用整合式 Windows 安全性，並讓應用程式集區身分識別開啟您的資料庫，您將建立有權開啟資料庫的使用者。</span><span class="sxs-lookup"><span data-stu-id="e36b8-296">On Cytanium's servers, rather than using integrated Windows security and letting the application pool identity open your database, you'll create a user that has authority to open your database.</span></span> <span data-ttu-id="e36b8-297">您會將使用者的認證加入至生產*web.config*檔案中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-297">You'll add the user's credentials to the connection strings that go in the production *Web.config* file.</span></span> <span data-ttu-id="e36b8-298">在此步驟中，您會建立這些認證。</span><span class="sxs-lookup"><span data-stu-id="e36b8-298">In this step you create those credentials.</span></span>

<span data-ttu-id="e36b8-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="e36b8-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span></span>

<span data-ttu-id="e36b8-300">在 [ **SQL 使用者屬性**] 頁面中填入必要的欄位：</span><span class="sxs-lookup"><span data-stu-id="e36b8-300">Fill in the required fields in the **SQL User Properties** page:</span></span>

- <span data-ttu-id="e36b8-301">輸入 "ContosoUniversityUser" 作為名稱。</span><span class="sxs-lookup"><span data-stu-id="e36b8-301">Enter "ContosoUniversityUser" as the name.</span></span>
- <span data-ttu-id="e36b8-302">輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="e36b8-302">Enter a password.</span></span>
- <span data-ttu-id="e36b8-303">選取 [ **contosouSchool** ] 做為預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-303">Select **contosouSchool** as the default database.</span></span>
- <span data-ttu-id="e36b8-304">選取 [ **contosouSchool** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e36b8-304">Select the **contosouSchool** check box.</span></span>

<span data-ttu-id="e36b8-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="e36b8-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span></span>

## <a name="configuring-database-deployment-for-the-production-environment"></a><span data-ttu-id="e36b8-306">設定生產環境的資料庫部署</span><span class="sxs-lookup"><span data-stu-id="e36b8-306">Configuring Database Deployment for the Production Environment</span></span>

<span data-ttu-id="e36b8-307">現在您已準備好在 [**封裝/發行 SQL** ] 索引標籤中設定資料庫部署設定，如同您先前在測試環境中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="e36b8-307">Now you're ready to set up database deployment settings in the **Package/Publish SQL** tab, as you did earlier for the test environment.</span></span>

<span data-ttu-id="e36b8-308">開啟 [**專案屬性**] 視窗，選取 [**封裝/發行 SQL** ] 索引標籤，並確定已選取 [設定] 下拉式清單中**的 [使用**中 **（發行）** ] 或 [**發行**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-308">Open the **Project Properties** window, select the **Package/Publish SQL** tab, and make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="e36b8-309">當您設定每個資料庫的部署設定時，您在生產和測試環境中所做的主要差異在於如何設定連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-309">When you configure deployment settings for each database, the key difference between what you do for production and test environments is in how you configure connection strings.</span></span> <span data-ttu-id="e36b8-310">針對測試環境，您輸入了不同的目的地資料庫連接字串，但在生產環境中，這兩個資料庫的目的地連接字串都相同。</span><span class="sxs-lookup"><span data-stu-id="e36b8-310">For the test environment you entered different destination database connection strings, but for the production environment the destination connection string will be the same for both databases.</span></span> <span data-ttu-id="e36b8-311">這是因為您要將這兩個資料庫部署到生產環境中的一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-311">This is because you are deploying both databases to one database in production.</span></span>

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="e36b8-312">設定成員資格資料庫的部署設定</span><span class="sxs-lookup"><span data-stu-id="e36b8-312">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="e36b8-313">若要設定套用至成員資格資料庫的設定，請選取 [**資料庫專案**] 資料表中的 [ **DefaultConnection-部署**] 資料列。</span><span class="sxs-lookup"><span data-stu-id="e36b8-313">To configure settings that apply to the membership database, select the **DefaultConnection-Deployment** row in the **Database Entries** table.</span></span>

<span data-ttu-id="e36b8-314">在 [**目的地資料庫的連接字串**] 中，輸入指向您剛才建立之新生產 SQL Server 資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-314">In **Connection string for destination database**, enter a connection string that points to the new production SQL Server database that you just created.</span></span> <span data-ttu-id="e36b8-315">您可以從歡迎電子郵件取得連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-315">You can get the connection string from your welcome email.</span></span> <span data-ttu-id="e36b8-316">電子郵件的相關部分包含下列範例連接字串：</span><span class="sxs-lookup"><span data-stu-id="e36b8-316">The relevant part of the email contains the following sample connection string:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

<span data-ttu-id="e36b8-317">取代三個變數之後，您所需的連接字串看起來就像下面這個範例：</span><span class="sxs-lookup"><span data-stu-id="e36b8-317">After you replace the three variables, the connection string you need looks like this example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

<span data-ttu-id="e36b8-318">在 [**封裝/發行 SQL** ] 索引標籤中，將此連接字串複製並貼到**目的地資料庫的連接字串**中。</span><span class="sxs-lookup"><span data-stu-id="e36b8-318">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="e36b8-319">請確定仍然選取**現有資料庫中的提取資料和/或架構**，而且**資料庫腳本選項**仍然是**架構和資料**。</span><span class="sxs-lookup"><span data-stu-id="e36b8-319">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="e36b8-320">在 [**資料庫腳本**] 方塊中，清除 [Grant. sql 腳本] 旁的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e36b8-320">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="e36b8-322">配置 School 資料庫的部署設定</span><span class="sxs-lookup"><span data-stu-id="e36b8-322">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="e36b8-323">接下來，選取 [**資料庫專案**] 資料表中的 [ **SchoolCoNtext-部署**] 資料列，以便設定 School 資料庫設定。</span><span class="sxs-lookup"><span data-stu-id="e36b8-323">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure the School database settings.</span></span>

<span data-ttu-id="e36b8-324">將相同的連接字串複製到您為成員資格資料庫複製到該欄位之**目的地資料庫的連接字串**中。</span><span class="sxs-lookup"><span data-stu-id="e36b8-324">Copy the same connection string into **Connection string for destination database** that you copied into that field for the membership database.</span></span>

<span data-ttu-id="e36b8-325">請確定仍然選取**現有資料庫中的提取資料和/或架構**，而且**資料庫腳本選項**仍然是**架構和資料**。</span><span class="sxs-lookup"><span data-stu-id="e36b8-325">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="e36b8-326">在 [**資料庫腳本**] 方塊中，清除 [Grant. sql 腳本] 旁的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e36b8-326">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

<span data-ttu-id="e36b8-327">將變更儲存至 [**封裝/發行 SQL** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-327">Save the changes to the **Package/Publish SQL** tab.</span></span>

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a><span data-ttu-id="e36b8-328">將連接字串的 web.config 轉換設定為生產資料庫</span><span class="sxs-lookup"><span data-stu-id="e36b8-328">Setting Up Web.Config Transforms for the Connection Strings to Production Databases</span></span>

<span data-ttu-id="e36b8-329">接下來，您將設定*web.config*轉換，*讓部署的 web.config 檔案*中的連接字串指向新的實際執行資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-329">Next, you'll set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file to point to the new production database.</span></span> <span data-ttu-id="e36b8-330">您在 [**封裝/發行 SQL** ] 索引標籤上輸入以供 Web Deploy 使用的連接字串，與應用程式所需使用的連接字串相同，但新增 [`MultipleResultSets`] 選項除外。</span><span class="sxs-lookup"><span data-stu-id="e36b8-330">The connection string that you entered on the **Package/Publish SQL** tab for Web Deploy to use is the same as the one the application needs to use, except for the addition of the `MultipleResultSets` option.</span></span>

<span data-ttu-id="e36b8-331">開啟*web.config* ，並將 `connectionStrings` 元素取代為如下列範例所示的 `connectionStrings` 元素。</span><span class="sxs-lookup"><span data-stu-id="e36b8-331">Open *Web.Production.config* and replace the `connectionStrings` element with a `connectionStrings` element that looks like the following example.</span></span> <span data-ttu-id="e36b8-332">（只複製 `connectionStrings` 專案，而不是提供用來顯示內容的周圍標記）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-332">(Only copy the `connectionStrings` element, not the surrounding tags that are provided to show the context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

<span data-ttu-id="e36b8-333">您有時會看到通知，告訴您一律加密*web.config*檔案中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-333">You sometimes see advice that tells you to always encrypt connection strings in the *Web.config* file.</span></span> <span data-ttu-id="e36b8-334">如果您要部署到自己公司網路上的伺服器，這可能是適當的。</span><span class="sxs-lookup"><span data-stu-id="e36b8-334">This might be appropriate if you were deploying to servers on your own company's network.</span></span> <span data-ttu-id="e36b8-335">不過，當您要部署至共用的裝載環境時，您會信任主控提供者的安全性作法，而不需要或實際加密連接字串。</span><span class="sxs-lookup"><span data-stu-id="e36b8-335">When you are deploying to a shared hosting environment, though, you're trusting the security practices of the hosting provider, and it's not necessary or practical to encrypt the connection strings.</span></span>

## <a name="deploying-to-the-production-environment"></a><span data-ttu-id="e36b8-336">部署到生產環境</span><span class="sxs-lookup"><span data-stu-id="e36b8-336">Deploying to the Production Environment</span></span>

<span data-ttu-id="e36b8-337">現在您已經準備好部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="e36b8-337">Now you're ready to deploy to production.</span></span> <span data-ttu-id="e36b8-338">Web Deploy 會讀取您專案之*應用程式*中的 SQL Server Compact 資料庫\_[Data] 資料夾，然後在生產 SQL Server 資料庫中重新建立其所有資料表和資料。</span><span class="sxs-lookup"><span data-stu-id="e36b8-338">Web Deploy will read the SQL Server Compact databases in your project's *App\_Data* folder and re-create all of their tables and data in the production SQL Server database.</span></span> <span data-ttu-id="e36b8-339">若要使用 [**封裝/發行 Web** ] 索引標籤設定進行發佈，您必須為生產環境建立新的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="e36b8-339">In order to publish by using the **Package/Publish Web** tab settings, you have to create a new publish profile for production.</span></span>

<span data-ttu-id="e36b8-340">首先，刪除現有的生產設定檔，如同您稍早在測試組態檔中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="e36b8-340">First, delete the existing Production profile as you did the Test profile earlier.</span></span>

<span data-ttu-id="e36b8-341">在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-341">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="e36b8-342">選取 [**設定檔**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-342">Select the **Profile** tab.</span></span>

<span data-ttu-id="e36b8-343">按一下 [**管理設定檔**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-343">Click **Manage Profiles**.</span></span>

<span data-ttu-id="e36b8-344">選取 [**生產**]，按一下 [**移除**]，然後按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-344">Select **Production**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="e36b8-345">關閉 [**發行 Web** wizard] 以儲存此變更。</span><span class="sxs-lookup"><span data-stu-id="e36b8-345">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="e36b8-346">接下來，建立新的生產設定檔，並使用它來發行專案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-346">Next, create a new Production profile and use it to publish the project.</span></span>

<span data-ttu-id="e36b8-347">在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-347">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="e36b8-348">選取 [**設定檔**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-348">Select the **Profile** tab.</span></span>

<span data-ttu-id="e36b8-349">按一下 [匯**入**]，然後選取您稍早下載的 .publishsettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-349">Click **Import**, and select the .publishsettings file that you downloaded earlier.</span></span>

<span data-ttu-id="e36b8-350">在 [**連接**] 索引標籤上，將 [**目的地 URL** ] 變更為正確的暫存 url，在此範例中為 http://contosouniversity.com.vserver01.cytanium.com 。</span><span class="sxs-lookup"><span data-stu-id="e36b8-350">On the **Connection** tab, change the **Destination URL** to the correct temporary URL, which in this example is http://contosouniversity.com.vserver01.cytanium.com.</span></span>

<span data-ttu-id="e36b8-351">將設定檔重新命名為生產環境。</span><span class="sxs-lookup"><span data-stu-id="e36b8-351">Rename the profile to Production.</span></span> <span data-ttu-id="e36b8-352">（選取 [**設定檔**] 索引標籤，然後按一下 [**管理設定檔**] 來這麼做）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-352">(Select the **Profile** tab and click **Manage Profiles** to do that).</span></span>

<span data-ttu-id="e36b8-353">關閉 [**發行 Web** wizard] 以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="e36b8-353">Close the **Publish Web** wizard to save your changes.</span></span>

<span data-ttu-id="e36b8-354">在實際的應用程式中，如果是在生產環境中更新資料庫，您現在可以在發行之前執行兩個額外步驟：</span><span class="sxs-lookup"><span data-stu-id="e36b8-354">In a real application in which the database was being updated in production, you would do two additional steps now before you publish:</span></span>

1. <span data-ttu-id="e36b8-355">如[部署到生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所示，上傳*應用程式\_離線 .htm*。</span><span class="sxs-lookup"><span data-stu-id="e36b8-355">Upload *app\_offline.htm*, as shown in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span>
2. <span data-ttu-id="e36b8-356">使用 [Cytanium] 控制台的 [**檔案管理員**] 功能，將*aspnet-Prod*和*School-Prod .sdf*檔案從生產網站複製到 ContosoUniversity 專案的*應用程式\_Data*資料夾。</span><span class="sxs-lookup"><span data-stu-id="e36b8-356">Use the **File Manager** feature of the Cytanium control panel to copy the *aspnet-Prod.sdf* and *School-Prod.sdf* files from the production site to the *App\_Data* folder of the ContosoUniversity project.</span></span> <span data-ttu-id="e36b8-357">這可確保您要部署到新 SQL Server 資料庫的資料包含生產網站所進行的最新更新。</span><span class="sxs-lookup"><span data-stu-id="e36b8-357">This ensures that the data you're deploying to the new SQL Server database includes the latest updates made by your production website.</span></span>

<span data-ttu-id="e36b8-358">在 Web 單鍵的 [**發佈**] 工具列中，確定已選取 [**生產**設定檔]，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-358">In the **Web One Click Publish** toolbar, make sure that the **Production** profile is selected, and then click **Publish**.</span></span>

<span data-ttu-id="e36b8-359">如果您在發佈之前將<em>應用程式\_離線</em>，您必須使用 [Cytanium 控制台] 中的 [<strong>檔案管理員</strong>] 公用程式來刪除<em>離線應用程式\_。</em>在測試之前的 .htm。</span><span class="sxs-lookup"><span data-stu-id="e36b8-359">If you uploaded <em>app\_offline.htm</em> before publishing, you have to use the <strong>File Manager</strong> utility in the Cytanium control panel to delete <em>app\_offline.</em>htm before you test.</span></span> <span data-ttu-id="e36b8-360">同時，您也可以將應用程式中的<em>.sdf</em>檔案從<em>\_Data</em>資料夾中刪除。</span><span class="sxs-lookup"><span data-stu-id="e36b8-360">You can also at the same time delete the <em>.sdf</em> files from the <em>App\_Data</em> folder.</span></span>

<span data-ttu-id="e36b8-361">您現在可以開啟瀏覽器，並移至公用網站的 URL 來測試應用程式，方法與部署至測試環境的方式相同。</span><span class="sxs-lookup"><span data-stu-id="e36b8-361">You can now open a browser and go to the URL of your public site to test the application the same way you did after deploying to the test environment.</span></span>

## <a name="switching-to-sql-server-express-localdb-in-development"></a><span data-ttu-id="e36b8-362">切換至開發中的 SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="e36b8-362">Switching to SQL Server Express LocalDB in Development</span></span>

<span data-ttu-id="e36b8-363">如總覽中所述，通常最好是在開發中使用您在測試和生產環境中使用的相同資料庫引擎。</span><span class="sxs-lookup"><span data-stu-id="e36b8-363">As was explained in the Overview, it's generally best to use the same database engine in development that you use in test and production.</span></span> <span data-ttu-id="e36b8-364">（請記住，在開發中使用 SQL Server Express 的優點是，資料庫在開發、測試和生產環境中的運作方式都相同）。在本節中，您將設定當您從 Visual Studio 執行應用程式時，要使用 SQL Server Express LocalDB 的 ContosoUniversity 專案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-364">(Remember that the advantage to using SQL Server Express in development is that the database will work the same in your development, test, and production environments.) In this section you'll set up the ContosoUniversity project to use SQL Server Express LocalDB when you run the application from Visual Studio.</span></span>

<span data-ttu-id="e36b8-365">執行此遷移的最簡單方式是讓 Code First 和成員資格系統為您建立新的開發資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-365">The simplest way to perform this migration is to let Code First and the membership system create both new development databases for you.</span></span> <span data-ttu-id="e36b8-366">使用此方法進行遷移需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="e36b8-366">Using this method to migrate requires three steps:</span></span>

1. <span data-ttu-id="e36b8-367">變更連接字串以指定新的 SQL Express LocalDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-367">Change the connection strings to specify new SQL Express LocalDB databases.</span></span>
2. <span data-ttu-id="e36b8-368">執行網站管理工具來建立系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="e36b8-368">Run the Web Site Administration Tool to create an administrator user.</span></span> <span data-ttu-id="e36b8-369">這會建立成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-369">This creates the membership database.</span></span>
3. <span data-ttu-id="e36b8-370">使用 Code First 移轉的 [更新資料庫] 命令來建立和植入應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="e36b8-370">Use the Code First Migrations update-database command to create and seed the application database.</span></span>

### <a name="updating-connection-strings-in-the-webconfig-file"></a><span data-ttu-id="e36b8-371">更新 Web.config 檔案中的連接字串</span><span class="sxs-lookup"><span data-stu-id="e36b8-371">Updating Connection Strings in the Web.config file</span></span>

<span data-ttu-id="e36b8-372">開啟*web.config*檔案，並以下列程式碼取代 `connectionStrings` 元素：</span><span class="sxs-lookup"><span data-stu-id="e36b8-372">Open the *Web.config* file and replace the `connectionStrings` element with the following code:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a><span data-ttu-id="e36b8-373">建立成員資格資料庫</span><span class="sxs-lookup"><span data-stu-id="e36b8-373">Creating the Membership Database</span></span>

<span data-ttu-id="e36b8-374">在**方案總管**中，選取 [ContosoUniversity] 專案，然後按一下 [**專案**] 功能表中的 [ **ASP.NET**設定]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-374">In **Solution Explorer**, select the ContosoUniversity project, and then click **ASP.NET Configuration** in the **Project** menu.</span></span>

<span data-ttu-id="e36b8-375">選取 [安全性] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-375">Select the Security tab.</span></span>

<span data-ttu-id="e36b8-376">按一下 [**建立或管理角色**]，然後建立**系統管理員**角色。</span><span class="sxs-lookup"><span data-stu-id="e36b8-376">Click **Create or Manage Roles**, and then create an **Administrator** role.</span></span>

<span data-ttu-id="e36b8-377">返回 [安全性] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e36b8-377">Return to the Security tab.</span></span>

<span data-ttu-id="e36b8-378">按一下 [**建立使用者**]，然後選取 [**系統管理員**] 核取方塊，並建立名為 admin 的使用者。</span><span class="sxs-lookup"><span data-stu-id="e36b8-378">Click **Create user**, and then select the **Administrator** check box and create a user named admin.</span></span>

<span data-ttu-id="e36b8-379">關閉 [網站**管理工具**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-379">Close the **Web Site Administration Tool**.</span></span>

### <a name="creating-the-school-database"></a><span data-ttu-id="e36b8-380">建立 School 資料庫</span><span class="sxs-lookup"><span data-stu-id="e36b8-380">Creating the School Database</span></span>

<span data-ttu-id="e36b8-381">開啟 [套件管理員主控台] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e36b8-381">Open the Package Manager Console window.</span></span>

<span data-ttu-id="e36b8-382">在 [**預設專案**] 下拉式清單中，選取 [ContosoUniversity] 專案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-382">In the **Default project** drop-down list, select the ContosoUniversity.DAL project.</span></span>

<span data-ttu-id="e36b8-383">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="e36b8-383">Enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

<span data-ttu-id="e36b8-384">Code First 移轉會套用建立資料庫的初始遷移，然後套用 AddBirthDate 遷移，然後執行種子方法。</span><span class="sxs-lookup"><span data-stu-id="e36b8-384">Code First Migrations applies the Initial migration that creates the database and then applies the AddBirthDate migration, then it runs the Seed method.</span></span>

<span data-ttu-id="e36b8-385">按下 Ctrl F5 來執行網站。</span><span class="sxs-lookup"><span data-stu-id="e36b8-385">Run the site by pressing Control-F5.</span></span> <span data-ttu-id="e36b8-386">如同您在測試和生產環境中所做的一樣，執行 [**新增學生**] 頁面，新增學生，然後在 [**學生**] 頁面中查看新的學生。</span><span class="sxs-lookup"><span data-stu-id="e36b8-386">As you did for the test and production environments, run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="e36b8-387">這會驗證 School 資料庫是否已建立並初始化，以及您是否擁有它的讀取和寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="e36b8-387">This verifies that the School database was created and initialized and that you have read and write access to it.</span></span>

<span data-ttu-id="e36b8-388">選取 [**更新信用額度**] 頁面並登入，以確認成員資格資料庫已部署，而且您有其存取權。</span><span class="sxs-lookup"><span data-stu-id="e36b8-388">Select the **Update Credits** page and log in to verify that the membership database was deployed and that you have access to it.</span></span> <span data-ttu-id="e36b8-389">如果您未遷移您的使用者帳戶，請建立系統管理員帳戶，然後選取 [**更新信用額度**] 頁面，以驗證其是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="e36b8-389">If you did not migrate your user accounts, create an administrator account and then select the **Update Credits** page to verify that it works.</span></span>

## <a name="cleaning-up-sql-server-compact-files"></a><span data-ttu-id="e36b8-390">清理 SQL Server Compact 檔案</span><span class="sxs-lookup"><span data-stu-id="e36b8-390">Cleaning Up SQL Server Compact Files</span></span>

<span data-ttu-id="e36b8-391">您不再需要包含的檔案和 NuGet 套件來支援 SQL Server Compact。</span><span class="sxs-lookup"><span data-stu-id="e36b8-391">You no longer need files and NuGet packages that were included to support SQL Server Compact.</span></span> <span data-ttu-id="e36b8-392">如果您想要（不需要此步驟），您可以清除不必要的檔案和參考。</span><span class="sxs-lookup"><span data-stu-id="e36b8-392">If you want (this step is not required), you can clean up unneeded files and references.</span></span>

<span data-ttu-id="e36b8-393">在**方案總管**中，將來自*應用程式*的 *.sdf*檔案從 [ *Bin* ] 資料夾中刪除\_[Data] 資料夾和 [ *amd64* ] 和 [ *x86* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e36b8-393">In **Solution Explorer**, delete the *.sdf* files from the *App\_Data* folder and the *amd64* and *x86* folders from the *bin* folder.</span></span>

<span data-ttu-id="e36b8-394">在**方案總管**中，以滑鼠右鍵按一下方案（不是其中一個專案），然後按一下 [**管理方案的 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-394">In **Solution Explorer**, right-click the solution (not one of the projects), and then click **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="e36b8-395">在 [**管理 NuGet 封裝**] 對話方塊的左窗格中，選取 [**已安裝的封裝**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-395">In the left pane of the **Manage NuGet Packages** dialog box, select **Installed packages**.</span></span>

<span data-ttu-id="e36b8-396">選取 [ **EntityFramework entityframework.sqlservercompact** ] 套件，然後按一下 [**管理**]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-396">Select the **EntityFramework.SqlServerCompact** package and click **Manage**.</span></span>

<span data-ttu-id="e36b8-397">在 [**選取專案**] 對話方塊中，會選取這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="e36b8-397">In the **Select Projects** dialog box, both projects are selected.</span></span> <span data-ttu-id="e36b8-398">若要卸載這兩個專案中的封裝，請清除這兩個核取方塊，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="e36b8-398">To uninstall the package in both projects, clear both check boxes, then click **OK**.</span></span>

<span data-ttu-id="e36b8-399">在詢問您是否也要卸載相依套件的對話方塊中，按一下 [否]。</span><span class="sxs-lookup"><span data-stu-id="e36b8-399">In the dialog box that asks if you want to uninstall the dependent packages also, click No.</span></span> <span data-ttu-id="e36b8-400">其中一個是您必須保留的 Entity Framework 套件。</span><span class="sxs-lookup"><span data-stu-id="e36b8-400">One of these is the Entity Framework package that you have to keep.</span></span>

<span data-ttu-id="e36b8-401">遵循相同的程式來卸載**entityframework.sqlservercompact**套件。</span><span class="sxs-lookup"><span data-stu-id="e36b8-401">Follow the same procedure to uninstall the **SqlServerCompact** package.</span></span> <span data-ttu-id="e36b8-402">（必須依照此順序卸載封裝，因為**EntityFramework. entityframework.sqlservercompact**套件相依于**entityframework.sqlservercompact**套件）。</span><span class="sxs-lookup"><span data-stu-id="e36b8-402">(The packages must be uninstalled in this order because the **EntityFramework.SqlServerCompact** package depends on the **SqlServerCompact** package.)</span></span>

<span data-ttu-id="e36b8-403">您現在已成功遷移至 SQL Server Express 和完整 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="e36b8-403">You have now successfully migrated to SQL Server Express and full SQL Server.</span></span> <span data-ttu-id="e36b8-404">在下一個教學課程中，您將會進行另一個資料庫變更，而您將瞭解如何在測試和實際執行資料庫使用 SQL Server Express 和完整 SQL Server 時，部署資料庫變更。</span><span class="sxs-lookup"><span data-stu-id="e36b8-404">In the next tutorial you'll make another database change, and you'll see how to deploy database changes when your test and production databases use SQL Server Express and full SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e36b8-405">[上一頁](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="e36b8-405">[Previous](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span></span>
