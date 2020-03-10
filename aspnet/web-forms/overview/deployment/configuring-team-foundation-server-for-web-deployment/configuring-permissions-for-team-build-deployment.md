---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 正在設定 Team Build 部署的許可權 |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定許可權，讓您的組建伺服器將內容部署到 web 伺服器和資料庫伺服器，做為自動化 b 的一部分 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638422"
---
# <a name="configuring-permissions-for-team-build-deployment"></a><span data-ttu-id="93519-103">設定小組組建部署的權限</span><span class="sxs-lookup"><span data-stu-id="93519-103">Configuring Permissions for Team Build Deployment</span></span>

<span data-ttu-id="93519-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="93519-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="93519-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="93519-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="93519-106">本主題描述如何設定許可權，讓您的組建伺服器將內容部署到 web 伺服器和資料庫伺服器，做為自動化組建程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="93519-106">This topic describes how to configure permissions to enable your build server to deploy content to web servers and database servers as part of an automated build process.</span></span>

<span data-ttu-id="93519-107">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="93519-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="93519-108">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="93519-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="93519-109">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="93519-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="93519-110">工作總覽</span><span class="sxs-lookup"><span data-stu-id="93519-110">Task Overview</span></span>

<span data-ttu-id="93519-111">當您安裝 Team Foundation Server （TFS）2010組建服務時，請指定您要用來執行服務的身分識別。</span><span class="sxs-lookup"><span data-stu-id="93519-111">When you install the Team Foundation Server (TFS) 2010 build service, you specify the identity with which you want the service to run.</span></span> <span data-ttu-id="93519-112">根據預設，這是網路服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="93519-112">By default, this is the Network Service account.</span></span> <span data-ttu-id="93519-113">或者，您可以將組建服務設定為使用網域帳戶來執行。</span><span class="sxs-lookup"><span data-stu-id="93519-113">Alternatively, you can configure the build service to run using a domain account.</span></span>

<span data-ttu-id="93519-114">任何需要 Windows 驗證，而且您打算使用 Team Build 自動化的部署工作，都將使用組建服務身分識別來執行。</span><span class="sxs-lookup"><span data-stu-id="93519-114">Any deployment tasks that require Windows authentication, and that you plan to automate using Team Build, will run using the build service identity.</span></span> <span data-ttu-id="93519-115">因此，您必須將 web 伺服器和資料庫伺服器上的任何必要許可權授與組建服務識別。</span><span class="sxs-lookup"><span data-stu-id="93519-115">As such, you'll need to grant the build service identity any required permissions on your web servers and your database servers.</span></span>

> [!NOTE]
> <span data-ttu-id="93519-116">Network Service 帳戶會使用電腦帳戶向其他電腦進行驗證。</span><span class="sxs-lookup"><span data-stu-id="93519-116">The Network Service account uses the machine account to authenticate to other computers.</span></span> <span data-ttu-id="93519-117">電腦帳戶的格式為 \* [功能變數名稱]\[電腦名稱稱] \* **$** &#x2014;例如**FABRIKAM\TFSBUILD $** 。</span><span class="sxs-lookup"><span data-stu-id="93519-117">Machine accounts take the form \*[domain name]\[machine name]\***$**&#x2014;for example, **FABRIKAM\TFSBUILD$**.</span></span> <span data-ttu-id="93519-118">因此，如果您的組建服務使用網路服務識別執行，您應該將任何必要的許可權授與給組建伺服器的電腦帳戶識別。</span><span class="sxs-lookup"><span data-stu-id="93519-118">As such, if your build service runs using the Network Service identity, you should grant any required permissions to the machine account identity for your build server.</span></span>

## <a name="configuring-web-server-permissions"></a><span data-ttu-id="93519-119">設定 Web 服務器許可權</span><span class="sxs-lookup"><span data-stu-id="93519-119">Configuring Web Server Permissions</span></span>

<span data-ttu-id="93519-120">如[選擇正確的 Web 部署方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)中所述，如果您想要將 Web 套件部署到遠端 web 伺服器，您可以使用兩種主要方法：</span><span class="sxs-lookup"><span data-stu-id="93519-120">As described in [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), there are two main approaches you can use if you want to deploy web packages to a remote web server:</span></span>

- <span data-ttu-id="93519-121">將目標設為目的地伺服器上的*Web Deployment Agent 服務*（也稱為遠端代理程式），以從遠端位置部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="93519-121">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the remote agent) on the destination server.</span></span>
- <span data-ttu-id="93519-122">以目的地伺服器上的*Internet Information Services* （*IIS） Web Deploy 處理*程式為目標，從遠端位置部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="93519-122">Deploy the application from a remote location by targeting the *Internet Information Services* (*IIS) Web Deploy Handler* on the destination server.</span></span>

<span data-ttu-id="93519-123">在此情況下，遠端代理程式有兩個主要限制：</span><span class="sxs-lookup"><span data-stu-id="93519-123">The remote agent has two key limitations in this case:</span></span>

- <span data-ttu-id="93519-124">遠端代理程式僅支援 NTLM 驗證。</span><span class="sxs-lookup"><span data-stu-id="93519-124">The remote agent supports only NTLM authentication.</span></span> <span data-ttu-id="93519-125">換句話說，部署必須使用組建服務身分識別&#x2014;您無法模擬另一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="93519-125">In other words, the deployment must use the build service identity&#x2014;you can't impersonate another account.</span></span>
- <span data-ttu-id="93519-126">若要使用遠端代理程式，執行部署的帳戶必須是目標伺服器上的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="93519-126">To use the remote agent, the account that performs the deployment must be an administrator on the target server.</span></span>

<span data-ttu-id="93519-127">總之，這兩項限制讓遠端代理程式不需要自動化 Team Build 部署的方法。</span><span class="sxs-lookup"><span data-stu-id="93519-127">Together, these two limitations make the remote agent approach undesirable for an automated Team Build deployment.</span></span> <span data-ttu-id="93519-128">若要使用此方法，您必須將組建服務帳戶設為任何目標 web 伺服器上的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="93519-128">To use this approach, you'd need to make the build service account an administrator on any target web servers.</span></span>

<span data-ttu-id="93519-129">相反地，Web Deploy 處理常式方法會提供各種優點：</span><span class="sxs-lookup"><span data-stu-id="93519-129">In contrast, the Web Deploy Handler approach offers various advantages:</span></span>

- <span data-ttu-id="93519-130">Web Deploy 處理常式支援透過 HTTPS 進行基本驗證，可讓您將替代帳戶的認證傳遞給 IIS Web 部署工具（Web Deploy）。</span><span class="sxs-lookup"><span data-stu-id="93519-130">The Web Deploy Handler supports basic authentication over HTTPS, which allows you to pass the credentials of an alternative account to the IIS Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="93519-131">您可以設定目標 web 伺服器，讓非系統管理員使用者使用 Web Deploy 處理常式將內容部署到特定的 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="93519-131">You can configure target web servers to allow non-administrator users to deploy content to specific IIS websites using the Web Deploy Handler.</span></span>

<span data-ttu-id="93519-132">如此一來，當您從 Team Build 將 Web 套件部署自動化時，最好將目標設為 Web Deploy 處理常式。</span><span class="sxs-lookup"><span data-stu-id="93519-132">As a result, it's clearly preferable to target the Web Deploy Handler when you automate web package deployment from Team Build.</span></span> <span data-ttu-id="93519-133">這是建議的程式：</span><span class="sxs-lookup"><span data-stu-id="93519-133">This is the recommended process:</span></span>

1. <span data-ttu-id="93519-134">建立要用於部署的低許可權網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="93519-134">Create a low-privileged domain account to use for the deployment.</span></span>
2. <span data-ttu-id="93519-135">設定 Web Deploy 處理常式，並授與帳戶將內容部署到特定 IIS 網站的必要許可權，如設定[Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="93519-135">Configure the Web Deploy Handler and grant the account the required permissions to deploy content to a specific IIS website, as described in [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span>
3. <span data-ttu-id="93519-136">使用基本驗證並提供您建立的網域帳號憑證來執行部署，以叫用 Web Deploy 並以 Web Deploy 處理常式為目標。</span><span class="sxs-lookup"><span data-stu-id="93519-136">Invoke Web Deploy and target the Web Deploy Handler, using basic authentication and supplying the credentials of the domain account you created, to perform the deployment.</span></span>

<span data-ttu-id="93519-137">在[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案中，您可以在環境特定的專案檔中指定驗證類型（[基本] 或 [NTLM]）、[Web Deploy 認證] 和 [端點位址] （[遠端代理程式] 或 [Web Deploy 處理常式]）。</span><span class="sxs-lookup"><span data-stu-id="93519-137">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, you specify the authentication type (basic or NTLM), the Web Deploy credentials, and the endpoint address (remote agent or Web Deploy Handler) in the environment-specific project file.</span></span> <span data-ttu-id="93519-138">當執行專案檔時，會使用這些值來制訂和執行 Web Deploy 命令。</span><span class="sxs-lookup"><span data-stu-id="93519-138">These values are used to formulate and run a Web Deploy command when the project file is executed.</span></span> <span data-ttu-id="93519-139">如需詳細資訊，請參閱[部署 Web 封裝](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="93519-139">For more information, see [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="93519-140">如需設定 Web Deploy 處理常式的詳細資訊，包括如何設定許可權，請參閱設定[用於 Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="93519-140">For more information on configuring the Web Deploy Handler, including how to configure permissions, see [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="93519-141">如需有關設定遠端代理程式的詳細資訊，請參閱設定[用於 Web Deploy 發佈的 Web 服務器（遠端代理程式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="93519-141">For more information on configuring the remote agent, see [Configuring a Web Server for Web Deploy Publishing (Remote Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span>

## <a name="configuring-database-server-permissions"></a><span data-ttu-id="93519-142">正在設定資料庫伺服器許可權</span><span class="sxs-lookup"><span data-stu-id="93519-142">Configuring Database Server Permissions</span></span>

<span data-ttu-id="93519-143">若要將資料庫部署到 SQL Server，您必須：</span><span class="sxs-lookup"><span data-stu-id="93519-143">To deploy a database to SQL Server, you must:</span></span>

- <span data-ttu-id="93519-144">在 SQL Server 實例上建立部署帳戶的登入。</span><span class="sxs-lookup"><span data-stu-id="93519-144">Create a login for the deploying account on the SQL Server instance.</span></span>
- <span data-ttu-id="93519-145">授與 SQL Server 實例的登入**DBCreator**許可權。</span><span class="sxs-lookup"><span data-stu-id="93519-145">Grant the login **DBCreator** permissions on the SQL Server instance.</span></span>
- <span data-ttu-id="93519-146">在初始部署之後，將登入新增至目標資料庫上的**db\_擁有**者角色。</span><span class="sxs-lookup"><span data-stu-id="93519-146">After the initial deployment, add the login to the **db\_owner** role on the target database.</span></span> <span data-ttu-id="93519-147">這是必要的，因為在後續的部署中，您要修改現有的資料庫，而不是建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="93519-147">This is required because on subsequent deployments, you're modifying an existing database rather than creating a new database.</span></span>

<span data-ttu-id="93519-148">您可以使用 NTLM 驗證或 SQL Server authentication，向 SQL Server 實例進行驗證：</span><span class="sxs-lookup"><span data-stu-id="93519-148">You can authenticate to a SQL Server instance using either NTLM authentication or SQL Server authentication:</span></span>

- <span data-ttu-id="93519-149">如果您使用 NTLM 驗證，則需要將上述許可權授與組建服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="93519-149">If you use NTLM authentication, you need to grant the permissions described above to the build service account.</span></span>
- <span data-ttu-id="93519-150">如果您使用 SQL Server 驗證，則需要將上述許可權授與 SQL Server 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93519-150">If you use SQL Server authentication, you need to grant the permissions described above to the SQL Server account.</span></span> <span data-ttu-id="93519-151">您也必須在用來部署資料庫的連接字串中包含 SQL Server 的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="93519-151">You also need to include the SQL Server user name and password in the connection string you use to deploy the database.</span></span>

<span data-ttu-id="93519-152">如需如何設定資料庫部署之許可權的逐步詳細資料，請參閱設定用於[Web Deploy 發行的資料庫伺服器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="93519-152">For step-by-step details on how to configure permissions for database deployment, see [Configuring a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="93519-153">結論</span><span class="sxs-lookup"><span data-stu-id="93519-153">Conclusion</span></span>

<span data-ttu-id="93519-154">此時，當您從 Team Build 將 web 應用程式和資料庫部署自動化時，您應該瞭解所需的許可權，以及為您開啟的驗證選項。</span><span class="sxs-lookup"><span data-stu-id="93519-154">At this point, you should understand the permissions required, together with the authentication options open to you, when you automate web application and database deployments from Team Build.</span></span> <span data-ttu-id="93519-155">您也應該能夠在 IIS 網頁伺服器和 SQL Server 資料庫伺服器上執行必要的許可權。</span><span class="sxs-lookup"><span data-stu-id="93519-155">You should also be able to implement the necessary permissions on IIS web servers and SQL Server database servers.</span></span>

## <a name="further-reading"></a><span data-ttu-id="93519-156">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="93519-156">Further Reading</span></span>

<span data-ttu-id="93519-157">如需有關設定 Windows server 環境以支援遠端部署的詳細資訊，請參閱設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="93519-157">For more information on configuring Windows server environments to support remote deployment, see [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="93519-158">上一篇</span><span class="sxs-lookup"><span data-stu-id="93519-158">Previous</span></span>](deploying-a-specific-build.md)
