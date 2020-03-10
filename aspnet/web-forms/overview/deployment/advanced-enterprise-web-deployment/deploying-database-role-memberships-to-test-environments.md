---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 將資料庫角色成員資格部署到測試環境 |Microsoft Docs
author: jrjlee
description: 本主題描述如何將使用者帳戶新增至資料庫角色，做為方案部署到測試環境的一部分。 當您部署包含 ... 的方案時
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587588"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a><span data-ttu-id="620a3-104">將資料庫角色成員資格部署到測試環境</span><span class="sxs-lookup"><span data-stu-id="620a3-104">Deploying Database Role Memberships to Test Environments</span></span>

<span data-ttu-id="620a3-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="620a3-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="620a3-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="620a3-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="620a3-107">本主題描述如何將使用者帳戶新增至資料庫角色，做為方案部署到測試環境的一部分。</span><span class="sxs-lookup"><span data-stu-id="620a3-107">This topic describes how to add user accounts to database roles as part of a solution deployment to a test environment.</span></span>
> 
> <span data-ttu-id="620a3-108">當您將包含資料庫專案的方案部署至預備或生產環境時，您通常不會想要讓開發人員自動將使用者帳戶新增至資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="620a3-108">When you deploy a solution containing a database project to a staging or production environment, you typically don't want the developer to automate the addition of user accounts to database roles.</span></span> <span data-ttu-id="620a3-109">在大部分情況下，開發人員不會知道需要將哪些使用者帳戶新增至哪些資料庫角色，而這些需求可能會隨時變更。</span><span class="sxs-lookup"><span data-stu-id="620a3-109">In most cases, the developer won't know which user accounts need to be added to which database roles, and these requirements could change at any time.</span></span> <span data-ttu-id="620a3-110">不過，當您將包含資料庫專案的方案部署到開發或測試環境時，通常會有不同的情況：</span><span class="sxs-lookup"><span data-stu-id="620a3-110">However, when you deploy a solution containing a database project to a development or test environment, the situation is usually rather different:</span></span>
> 
> - <span data-ttu-id="620a3-111">開發人員通常會定期重新部署解決方案，通常是一天多次。</span><span class="sxs-lookup"><span data-stu-id="620a3-111">The developer typically re-deploys the solution on a regular basis, often several times a day.</span></span>
> - <span data-ttu-id="620a3-112">資料庫通常會在每個部署上重新建立，這表示必須在每次部署之後建立資料庫使用者，並將其新增至角色。</span><span class="sxs-lookup"><span data-stu-id="620a3-112">The database is typically re-created on every deployment, which means that database users must be created and added to roles after every deployment.</span></span>
> - <span data-ttu-id="620a3-113">開發人員通常可以完全掌控目標開發或測試環境。</span><span class="sxs-lookup"><span data-stu-id="620a3-113">The developer typically has full control over the target development or test environment.</span></span>
> 
> <span data-ttu-id="620a3-114">在此案例中，在部署程式中自動建立資料庫使用者並指派資料庫角色成員資格，通常會有説明。</span><span class="sxs-lookup"><span data-stu-id="620a3-114">In this scenario, it's often beneficial to automatically create database users and assign database role memberships as part of the deployment process.</span></span>
> 
> <span data-ttu-id="620a3-115">主要因素是，此作業必須根據目標環境進行條件式設定。</span><span class="sxs-lookup"><span data-stu-id="620a3-115">The key factor is that this operation needs to be conditional based on the target environment.</span></span> <span data-ttu-id="620a3-116">如果您要部署至預備或生產環境，您會想要略過此作業。</span><span class="sxs-lookup"><span data-stu-id="620a3-116">If you're deploying to a staging or a production environment, you want to skip the operation.</span></span> <span data-ttu-id="620a3-117">如果您要部署至開發人員或測試環境，您會想要部署角色成員資格，而不需要進一步介入。</span><span class="sxs-lookup"><span data-stu-id="620a3-117">If you're deploying to a developer or test environment, you want to deploy role memberships without further intervention.</span></span> <span data-ttu-id="620a3-118">本主題說明您可以用來解決這項挑戰的一種方法。</span><span class="sxs-lookup"><span data-stu-id="620a3-118">This topic describes one approach you can use to address this challenge.</span></span>

<span data-ttu-id="620a3-119">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="620a3-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="620a3-120">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="620a3-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="620a3-121">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="620a3-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="620a3-122">工作總覽</span><span class="sxs-lookup"><span data-stu-id="620a3-122">Task Overview</span></span>

<span data-ttu-id="620a3-123">本主題假設：</span><span class="sxs-lookup"><span data-stu-id="620a3-123">This topic assumes that:</span></span>

- <span data-ttu-id="620a3-124">如[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述，您可以使用分割專案檔案方法來部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="620a3-124">You use the split project file approach to solution deployment, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span>
- <span data-ttu-id="620a3-125">您可以從專案檔呼叫 VSDBCMD 來部署資料庫專案，如[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述。</span><span class="sxs-lookup"><span data-stu-id="620a3-125">You call VSDBCMD from the project file to deploy your database project, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

<span data-ttu-id="620a3-126">當您將資料庫專案部署至測試環境時，若要建立資料庫使用者並指派角色成員資格，您必須：</span><span class="sxs-lookup"><span data-stu-id="620a3-126">To create database users and assign role memberships when you deploy a database project to a test environment, you'll need to:</span></span>

- <span data-ttu-id="620a3-127">建立交易結構化查詢語言 (SQL) （Transact-sql）腳本，以進行必要的資料庫變更。</span><span class="sxs-lookup"><span data-stu-id="620a3-127">Create a Transact Structured Query Language (Transact-SQL) script that makes the necessary database changes.</span></span>
- <span data-ttu-id="620a3-128">建立使用 sqlcmd 公用程式執行 SQL 腳本的 Microsoft Build Engine （MSBuild）目標。</span><span class="sxs-lookup"><span data-stu-id="620a3-128">Create a Microsoft Build Engine (MSBuild) target that uses the sqlcmd.exe utility to run the SQL script.</span></span>
- <span data-ttu-id="620a3-129">將您的方案部署到測試環境時，設定您的專案檔以叫用目標。</span><span class="sxs-lookup"><span data-stu-id="620a3-129">Configure your project files to invoke the target when you're deploying your solution to a test environment.</span></span>

<span data-ttu-id="620a3-130">本主題將說明如何執行上述每個程式。</span><span class="sxs-lookup"><span data-stu-id="620a3-130">This topic will show you how to perform each of these procedures.</span></span>

## <a name="scripting-the-database-role-memberships"></a><span data-ttu-id="620a3-131">編寫資料庫角色成員資格的腳本</span><span class="sxs-lookup"><span data-stu-id="620a3-131">Scripting the Database Role Memberships</span></span>

<span data-ttu-id="620a3-132">您可以用許多不同的方式，以及您選擇的任何位置來建立 Transact-sql 腳本。</span><span class="sxs-lookup"><span data-stu-id="620a3-132">You can create a Transact-SQL script in a lot of different ways, and in any location you choose.</span></span> <span data-ttu-id="620a3-133">最簡單的方法是在您的解決方案中建立 Visual Studio 2010 的腳本。</span><span class="sxs-lookup"><span data-stu-id="620a3-133">The easiest approach is to create the script within your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="620a3-134">**若要建立 SQL 腳本**</span><span class="sxs-lookup"><span data-stu-id="620a3-134">**To create a SQL script**</span></span>

1. <span data-ttu-id="620a3-135">在 [**方案總管**] 視窗中，展開您的資料庫專案節點。</span><span class="sxs-lookup"><span data-stu-id="620a3-135">In the **Solution Explorer** window, expand your database project node.</span></span>
2. <span data-ttu-id="620a3-136">在 [**腳本**] 資料夾上按一下滑鼠右鍵，指向 [**加入**]，然後按一下 [**新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="620a3-136">Right-click the **Scripts** folder, point to **Add**, and then click **New Folder**.</span></span>
3. <span data-ttu-id="620a3-137">輸入**Test**作為資料夾名稱，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="620a3-137">Type **Test** as the folder name, and then press Enter.</span></span>
4. <span data-ttu-id="620a3-138">以滑鼠右鍵按一下 [ **Test** ] 資料夾，指向 [**新增**]，然後按一下 [**腳本**]。</span><span class="sxs-lookup"><span data-stu-id="620a3-138">Right-click the **Test** folder, point to **Add**, and then click **Script**.</span></span>
5. <span data-ttu-id="620a3-139">在 [**加入新專案**] 對話方塊中，為您的腳本提供有意義的名稱（例如**AddRoleMemberships**），然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="620a3-139">In the **Add New Item** dialog box, give your script a meaningful name (for example, **AddRoleMemberships.sql**), and then click **Add**.</span></span>

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. <span data-ttu-id="620a3-140">在*AddRoleMemberships*檔案中，加入下列的 transact-sql 語句：</span><span class="sxs-lookup"><span data-stu-id="620a3-140">In the *AddRoleMemberships.sql* file, add Transact-SQL statements that:</span></span>

    1. <span data-ttu-id="620a3-141">為將存取資料庫的 SQL Server 登入建立資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="620a3-141">Create a database user for the SQL Server login that will access your database.</span></span>
    2. <span data-ttu-id="620a3-142">將資料庫使用者新增至任何必要的資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="620a3-142">Add the database user to any required database roles.</span></span>
7. <span data-ttu-id="620a3-143">檔案看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="620a3-143">The file should resemble this:</span></span>

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. <span data-ttu-id="620a3-144">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="620a3-144">Save the file.</span></span>

## <a name="executing-the-script-on-the-target-database"></a><span data-ttu-id="620a3-145">在目標資料庫上執行腳本</span><span class="sxs-lookup"><span data-stu-id="620a3-145">Executing the Script on the Target Database</span></span>

<span data-ttu-id="620a3-146">在理想的情況下，您會在部署資料庫專案時，執行任何必要的 Transact-sql 腳本作為部署後腳本的一部分。</span><span class="sxs-lookup"><span data-stu-id="620a3-146">Ideally, you'd run any required Transact-SQL scripts as part of a post-deployment script when you deploy your database project.</span></span> <span data-ttu-id="620a3-147">不過，部署後腳本並不允許您根據解決方案設定或組建屬性，有條件地執行邏輯。</span><span class="sxs-lookup"><span data-stu-id="620a3-147">However, post-deployment scripts don't allow you to execute logic conditionally based on solution configurations or build properties.</span></span> <span data-ttu-id="620a3-148">替代方式是建立執行 sqlcmd 命令的**目標**專案，直接從 MSBuild 專案檔執行 SQL 腳本。</span><span class="sxs-lookup"><span data-stu-id="620a3-148">The alternative is to run your SQL scripts directly from the MSBuild project file, by creating a **Target** element that executes a sqlcmd.exe command.</span></span> <span data-ttu-id="620a3-149">您可以使用此命令在目標資料庫上執行腳本：</span><span class="sxs-lookup"><span data-stu-id="620a3-149">You can use this command to run your script on the target database:</span></span>

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> <span data-ttu-id="620a3-150">如需 sqlcmd 命令列選項的詳細資訊，請參閱[Sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="620a3-150">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

<span data-ttu-id="620a3-151">在 MSBuild 目標中內嵌此命令之前，您必須考慮要執行腳本的條件：</span><span class="sxs-lookup"><span data-stu-id="620a3-151">Before you embed this command in an MSBuild target, you need to consider under what conditions you want the script to run:</span></span>

- <span data-ttu-id="620a3-152">目標資料庫必須先存在，您才能變更其角色成員資格。</span><span class="sxs-lookup"><span data-stu-id="620a3-152">The target database must exist before you change its role memberships.</span></span> <span data-ttu-id="620a3-153">因此，您必須在資料庫部署*之後*執行此腳本。</span><span class="sxs-lookup"><span data-stu-id="620a3-153">As such, you need to run this script *after* the database deployment.</span></span>
- <span data-ttu-id="620a3-154">您需要包含條件，才會針對測試環境執行腳本。</span><span class="sxs-lookup"><span data-stu-id="620a3-154">You need to include a condition so that the script is only executed for test environments.</span></span>
- <span data-ttu-id="620a3-155">如果您執行的是「假設」部署&#x2014;，但如果您要產生部署腳本，但未實際執行，&#x2014;則不應該執行 SQL 腳本。</span><span class="sxs-lookup"><span data-stu-id="620a3-155">If you're running a "what if" deployment&#x2014;in other words, if you're generating deployment scripts but not actually running them&#x2014;you shouldn't run the SQL script.</span></span>

<span data-ttu-id="620a3-156">如果您使用[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法（如 Contact Manager 範例解決方案所示），您可以分割 SQL 腳本的組建指示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="620a3-156">If you're using the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), as demonstrated by the Contact Manager sample solution, you can split the build instructions for your SQL script like this:</span></span>

- <span data-ttu-id="620a3-157">任何必要的環境特定屬性，以及決定是否要部署許可權的屬性，都應該在環境特定的專案檔（例如*Env-Dev*）中進行。</span><span class="sxs-lookup"><span data-stu-id="620a3-157">Any required environment-specific properties, together with the property that determines whether to deploy permissions, should go in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>
- <span data-ttu-id="620a3-158">MSBuild 目標本身和任何在目的地環境之間不會變更的屬性，都應該放在通用專案檔（例如， *Publish*）中。</span><span class="sxs-lookup"><span data-stu-id="620a3-158">The MSBuild target itself, together with any properties that will not change between destination environments, should go in the universal project file (for example, *Publish.proj*).</span></span>

<span data-ttu-id="620a3-159">在環境特定的專案檔中，您必須定義資料庫伺服器名稱、目標資料庫名稱，以及可讓使用者指定是否要部署角色成員資格的布林值屬性。</span><span class="sxs-lookup"><span data-stu-id="620a3-159">In the environment-specific project file, you need to define the database server name, the target database name, and a Boolean property that lets the user specify whether to deploy role memberships.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

<span data-ttu-id="620a3-160">在通用專案檔中，您必須提供 sqlcmd 可執行檔的位置，以及您想要執行之 SQL 腳本的位置。</span><span class="sxs-lookup"><span data-stu-id="620a3-160">In the universal project file, you need to provide the location of the sqlcmd executable and the location of the SQL script you want to run.</span></span> <span data-ttu-id="620a3-161">不論目的地環境為何，這些屬性都會維持不變。</span><span class="sxs-lookup"><span data-stu-id="620a3-161">These properties will remain the same regardless of the destination environment.</span></span> <span data-ttu-id="620a3-162">您也需要建立 MSBuild 目標來執行 sqlcmd 命令。</span><span class="sxs-lookup"><span data-stu-id="620a3-162">You also need to create an MSBuild target to execute the sqlcmd command.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

<span data-ttu-id="620a3-163">請注意，您會將 sqlcmd 可執行檔的位置新增為靜態屬性，因為這對其他目標很有用。</span><span class="sxs-lookup"><span data-stu-id="620a3-163">Notice that you add the location of the sqlcmd executable as a static property, as this could be useful to other targets.</span></span> <span data-ttu-id="620a3-164">相反地，您會將 SQL 腳本的位置和 sqlcmd 命令的語法定義為目標內的動態屬性，因為在執行目標之前，不需要它們。</span><span class="sxs-lookup"><span data-stu-id="620a3-164">In contrast, you define the location of your SQL script and the syntax of the sqlcmd command as dynamic properties within the target, as they will not be required before the target is executed.</span></span> <span data-ttu-id="620a3-165">在此情況下，只有在符合下列條件時，才會執行**DeployTestDBPermissions**目標：</span><span class="sxs-lookup"><span data-stu-id="620a3-165">In this case, the **DeployTestDBPermissions** target will only be executed if these conditions are met:</span></span>

- <span data-ttu-id="620a3-166">**DeployTestDBRoleMemberships**屬性設定為**true**。</span><span class="sxs-lookup"><span data-stu-id="620a3-166">The **DeployTestDBRoleMemberships** property is set to **true**.</span></span>
- <span data-ttu-id="620a3-167">使用者未指定**WhatIf = true**旗標。</span><span class="sxs-lookup"><span data-stu-id="620a3-167">The user hasn't specified a **WhatIf=true** flag.</span></span>

<span data-ttu-id="620a3-168">最後，別忘了叫用目標。</span><span class="sxs-lookup"><span data-stu-id="620a3-168">Finally, don't forget to invoke the target.</span></span> <span data-ttu-id="620a3-169">在*Publish*檔案中，您可以藉由將目標新增至預設**FullPublish**目標的相依性清單來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="620a3-169">In the *Publish.proj* file, you can do this by adding the target to the dependency list for the default **FullPublish** target.</span></span> <span data-ttu-id="620a3-170">您必須確保在執行**PublishDbPackages**目標之前，不會執行**DeployTestDBPermissions**目標。</span><span class="sxs-lookup"><span data-stu-id="620a3-170">You need to ensure that the **DeployTestDBPermissions** target is not executed until the **PublishDbPackages** target has been executed.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a><span data-ttu-id="620a3-171">結論</span><span class="sxs-lookup"><span data-stu-id="620a3-171">Conclusion</span></span>

<span data-ttu-id="620a3-172">本主題描述了一種方式，可讓您在部署資料庫專案時，將資料庫使用者和角色成員資格加入為部署後動作。</span><span class="sxs-lookup"><span data-stu-id="620a3-172">This topic described one way in which you can add database users and role memberships as a post-deployment action when you deploy a database project.</span></span> <span data-ttu-id="620a3-173">當您在測試環境中定期重新建立資料庫時，這通常很有用，但當您將資料庫部署至預備或生產環境時，通常應該避免這種情況。</span><span class="sxs-lookup"><span data-stu-id="620a3-173">This is typically useful when you regularly re-create a database in a test environment, but it should usually be avoided when you deploy databases to staging or production environments.</span></span> <span data-ttu-id="620a3-174">因此，您應該確定使用必要的條件式邏輯，以便只在適當的情況下才建立資料庫使用者和角色成員資格。</span><span class="sxs-lookup"><span data-stu-id="620a3-174">As such, you should ensure that you use the necessary conditional logic so that database users and role memberships are only created when it's appropriate to do so.</span></span>

## <a name="further-reading"></a><span data-ttu-id="620a3-175">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="620a3-175">Further Reading</span></span>

<span data-ttu-id="620a3-176">如需使用 VSDBCMD 來部署資料庫專案的詳細資訊，請參閱[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="620a3-176">For more information on using VSDBCMD to deploy database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="620a3-177">如需針對不同目標環境自訂資料庫部署的指引，請參閱[自訂多個環境的資料庫部署](customizing-database-deployments-for-multiple-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="620a3-177">For guidance on customizing database deployments for different target environments, see [Customizing Database Deployments for Multiple Environments](customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="620a3-178">如需使用自訂 MSBuild 專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。</span><span class="sxs-lookup"><span data-stu-id="620a3-178">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="620a3-179">如需 sqlcmd 命令列選項的詳細資訊，請參閱[Sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="620a3-179">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="620a3-180">[上一頁](customizing-database-deployments-for-multiple-environments.md)
> [下一頁](deploying-membership-databases-to-enterprise-environments.md)</span><span class="sxs-lookup"><span data-stu-id="620a3-180">[Previous](customizing-database-deployments-for-multiple-environments.md)
[Next](deploying-membership-databases-to-enterprise-environments.md)</span></span>
