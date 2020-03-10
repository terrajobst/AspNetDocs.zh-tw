---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 設定資料庫伺服器以進行 Web Deploy 發行 |Microsoft Docs
author: jrjlee
description: 本主題說明如何設定 SQL Server 2008 R2 資料庫伺服器，以支援 web 部署和發佈。 本主題中所述的工作為「共同 ...」
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: ade3c1ba1c470092f512436f39b8831458408c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634614"
---
# <a name="configuring-a-database-server-for-web-deploy-publishing"></a><span data-ttu-id="a805e-104">設定 Web Deploy 發行的資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="a805e-104">Configuring a Database Server for Web Deploy Publishing</span></span>

<span data-ttu-id="a805e-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="a805e-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a805e-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="a805e-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a805e-107">本主題說明如何設定 SQL Server 2008 R2 資料庫伺服器，以支援 web 部署和發佈。</span><span class="sxs-lookup"><span data-stu-id="a805e-107">This topic describes how to configure a SQL Server 2008 R2 database server to support web deployment and publishing.</span></span>
> 
> <span data-ttu-id="a805e-108">本主題所述的工作在每個部署案例&#x2014;中都是常見的，無論您的 web 伺服器是否設定為使用 IIS Web 部署工具（Web Deploy）遠端代理程式服務、Web Deploy 處理常式或離線部署，或是您的應用程式是在單一 web 伺服器或伺服器陣列上執行。</span><span class="sxs-lookup"><span data-stu-id="a805e-108">The tasks described in this topic are common to every deployment scenario&#x2014;it doesn't matter whether your web servers are configured to use the IIS Web Deployment Tool (Web Deploy) Remote Agent Service, the Web Deploy Handler, or offline deployment or your application is running on a single web server or a server farm.</span></span> <span data-ttu-id="a805e-109">根據安全性需求和其他考慮，您部署資料庫的方式可能會改變。</span><span class="sxs-lookup"><span data-stu-id="a805e-109">The way you deploy the database may change according to security requirements and other considerations.</span></span> <span data-ttu-id="a805e-110">例如，您可以部署包含或不含範例資料的資料庫，而且您可以部署使用者角色對應，或在部署之後手動設定它們。</span><span class="sxs-lookup"><span data-stu-id="a805e-110">For example, you might deploy the database with or without sample data, and you might deploy user role mappings or configure them manually after deployment.</span></span> <span data-ttu-id="a805e-111">不過，您設定資料庫伺服器的方式維持不變。</span><span class="sxs-lookup"><span data-stu-id="a805e-111">However, the way you configure the database server remains the same.</span></span>

<span data-ttu-id="a805e-112">您不需要安裝任何額外的產品或工具，就能設定資料庫伺服器以支援 web 部署。</span><span class="sxs-lookup"><span data-stu-id="a805e-112">You don't have to install any additional products or tools to configuring a database server to support web deployment.</span></span> <span data-ttu-id="a805e-113">假設您的資料庫伺服器和您的 web 伺服器在不同的電腦上執行，您只需要：</span><span class="sxs-lookup"><span data-stu-id="a805e-113">Assuming that your database server and your web server run on different machines, you simply need to:</span></span>

- <span data-ttu-id="a805e-114">允許 SQL Server 使用 TCP/IP 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a805e-114">Permit SQL Server to communicate using TCP/IP.</span></span>
- <span data-ttu-id="a805e-115">允許 SQL Server 流量通過任何防火牆。</span><span class="sxs-lookup"><span data-stu-id="a805e-115">Allow SQL Server traffic through any firewalls.</span></span>
- <span data-ttu-id="a805e-116">為 web 伺服器電腦帳戶提供 SQL Server 登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-116">Give the web server machine account a SQL Server login.</span></span>
- <span data-ttu-id="a805e-117">將電腦帳戶登入對應到任何必要的資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-117">Map the machine account login to any required database roles.</span></span>
- <span data-ttu-id="a805e-118">將執行部署的帳戶授與 SQL Server 登入和資料庫建立者許可權。</span><span class="sxs-lookup"><span data-stu-id="a805e-118">Give the account that will run the deployment a SQL Server login and database creator permissions.</span></span>
- <span data-ttu-id="a805e-119">若要支援重複部署，請將部署帳戶登入對應至**db\_擁有**者資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-119">To support repeat deployments, map the deployment account login to the **db\_owner** database role.</span></span>

<span data-ttu-id="a805e-120">本主題將說明如何執行上述每個程式。</span><span class="sxs-lookup"><span data-stu-id="a805e-120">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="a805e-121">本主題中的工作和逐步解說假設您是從在 Windows Server 2008 R2 上執行的 SQL Server 2008 R2 的預設實例開始。</span><span class="sxs-lookup"><span data-stu-id="a805e-121">The tasks and walkthroughs in this topic assume that you're starting with a default instance of SQL Server 2008 R2 running on Windows Server 2008 R2.</span></span> <span data-ttu-id="a805e-122">在繼續之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="a805e-122">Before you continue, ensure that:</span></span>

- <span data-ttu-id="a805e-123">Windows Server 2008 R2 Service Pack 1 和所有可用的更新都已安裝。</span><span class="sxs-lookup"><span data-stu-id="a805e-123">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="a805e-124">伺服器已加入網域。</span><span class="sxs-lookup"><span data-stu-id="a805e-124">The server is domain-joined.</span></span>
- <span data-ttu-id="a805e-125">伺服器具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a805e-125">The server has a static IP address.</span></span>
- <span data-ttu-id="a805e-126">SQL Server 2008 R2 Service Pack 1，並已安裝所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="a805e-126">SQL Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>

<span data-ttu-id="a805e-127">SQL Server 實例只需要包含**資料庫引擎服務**角色，這會自動包含在任何 SQL Server 安裝中。</span><span class="sxs-lookup"><span data-stu-id="a805e-127">The SQL Server instance only needs to include the **Database Engine Services** role, which is included automatically in any SQL Server installation.</span></span> <span data-ttu-id="a805e-128">不過，為了簡化設定和維護，建議您包含**管理工具-基本**和**管理工具–完整**的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-128">However, for ease of configuration and maintenance, we recommend that you include the **Management Tools – Basic** and **Management Tools – Complete** server roles.</span></span>

> [!NOTE]
> <span data-ttu-id="a805e-129">如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。</span><span class="sxs-lookup"><span data-stu-id="a805e-129">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="a805e-130">如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a805e-130">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span> <span data-ttu-id="a805e-131">如需有關安裝 SQL Server 的詳細資訊，請參閱[安裝 SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a805e-131">For more information on installing SQL Server, see [Installing SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx).</span></span>

## <a name="enable-remote-access-to-sql-server"></a><span data-ttu-id="a805e-132">啟用 SQL Server 的遠端存取</span><span class="sxs-lookup"><span data-stu-id="a805e-132">Enable Remote Access to SQL Server</span></span>

<span data-ttu-id="a805e-133">SQL Server 使用 TCP/IP 與遠端電腦通訊。</span><span class="sxs-lookup"><span data-stu-id="a805e-133">SQL Server uses TCP/IP to communicate with remote computers.</span></span> <span data-ttu-id="a805e-134">如果您的資料庫伺服器和網頁伺服器位於不同的電腦上，您需要：</span><span class="sxs-lookup"><span data-stu-id="a805e-134">If your database server and your web server are on different machines, you need to:</span></span>

- <span data-ttu-id="a805e-135">設定 SQL Server 網路設定，以允許透過 TCP/IP 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a805e-135">Configure SQL Server networking settings to allow communication over TCP/IP.</span></span>
- <span data-ttu-id="a805e-136">設定任何硬體或軟體防火牆，以允許 TCP 流量（在某些情況下，使用者資料包協定（UDP）流量）在 SQL Server 實例所使用的埠上。</span><span class="sxs-lookup"><span data-stu-id="a805e-136">Configure any hardware or software firewalls to allow TCP traffic (and in some cases User Datagram Protocol (UDP) traffic) on the ports that the SQL Server instance uses.</span></span>

<span data-ttu-id="a805e-137">若要讓 SQL Server 能夠透過 TCP/IP 進行通訊，請使用 SQL Server 組態管理員來變更 SQL Server 實例的網路設定。</span><span class="sxs-lookup"><span data-stu-id="a805e-137">To enable SQL Server to communicate over TCP/IP, use SQL Server Configuration Manager to change the network configuration for your SQL Server instance.</span></span>

<span data-ttu-id="a805e-138">**啟用 SQL Server 使用 TCP/IP 進行通訊**</span><span class="sxs-lookup"><span data-stu-id="a805e-138">**To enable SQL Server to communicate using TCP/IP**</span></span>

1. <span data-ttu-id="a805e-139">在 [**開始**] 功能表上，依序指向 [**所有程式**]、[ **Microsoft SQL Server 2008 R2**]、[**組態工具**]，然後按一下 [ **SQL Server 組態管理員**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-139">On the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, click **Configuration Tools**, and then click **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="a805e-140">在樹狀檢視窗格中，展開 [ **SQL Server 網路**設定]，然後按一下 [ **MSSQLSERVER 的通訊協定**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-140">In the tree view pane, expand **SQL Server Network Configuration**, and then click **Protocols for MSSQLSERVER**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a805e-141">如果您已安裝 SQL Server 的多個實例，您會看到每個實例的<em>[instance name]</em>專案的<strong>通訊協定</strong>。</span><span class="sxs-lookup"><span data-stu-id="a805e-141">If you have installed multiple instances of SQL Server, you'll see a <strong>Protocols for</strong><em>[instance name]</em> item for each instance.</span></span> <span data-ttu-id="a805e-142">您需要依實例逐一設定網路設定。</span><span class="sxs-lookup"><span data-stu-id="a805e-142">You need to configure network settings on an instance-by-instance basis.</span></span>
3. <span data-ttu-id="a805e-143">在詳細資料窗格中，以滑鼠右鍵按一下 [ **tcp/ip** ] 資料列，然後按一下 [**啟用**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-143">In the details pane, right-click the **TCP/IP** row, and then click **Enable**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. <span data-ttu-id="a805e-144">在 [**警告**] 對話方塊中，按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-144">In the **Warning** dialog box, click **OK**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. <span data-ttu-id="a805e-145">您必須重新開機 MSSQLSERVER 服務，新的網路設定才會生效。</span><span class="sxs-lookup"><span data-stu-id="a805e-145">You need to restart the MSSQLSERVER service before your new network configuration will take effect.</span></span> <span data-ttu-id="a805e-146">您可以在命令提示字元中、從 [服務] 主控台，或從 [SQL Server Management Studio] 執行此動作。</span><span class="sxs-lookup"><span data-stu-id="a805e-146">You can do that at a command prompt, from the Services console, or from SQL Server Management Studio.</span></span> <span data-ttu-id="a805e-147">在此程式中，您將使用 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="a805e-147">In this procedure, you'll use SQL Server Management Studio.</span></span>
6. <span data-ttu-id="a805e-148">關閉 SQL Server 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="a805e-148">Close SQL Server Configuration Manager.</span></span>
7. <span data-ttu-id="a805e-149">在 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft SQL Server 2008 R2**]，然後按一下 [ **SQL Server Management Studio**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-149">On the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.</span></span>
8. <span data-ttu-id="a805e-150">在 [**連接到伺服器**] 對話方塊的 [**伺服器名稱**] 方塊中，輸入資料庫伺服器的名稱，然後按一下 **[連接]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-150">In the **Connect to Server** dialog box, in the **Server name** box, type the name of the database server, and then click **Connect**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. <span data-ttu-id="a805e-151">在 [**物件總管**] 窗格中，以滑鼠右鍵按一下父伺服器節點（例如， **TESTDB1**），然後按一下 [**重新開機**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-151">In the **Object Explorer** pane, right-click the parent server node (for example, **TESTDB1**), and then click **Restart**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. <span data-ttu-id="a805e-152">在 [ **Microsoft SQL Server Management Studio** ] 對話方塊中，按一下 **[是**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-152">In the **Microsoft SQL Server Management Studio** dialog box, click **Yes**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. <span data-ttu-id="a805e-153">當服務重新開機時，請關閉 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="a805e-153">When the service has restarted, close SQL Server Management Studio.</span></span>

<span data-ttu-id="a805e-154">若要允許 SQL Server 流量通過防火牆，您必須先知道 SQL Server 實例所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="a805e-154">To allow SQL Server traffic through a firewall, you first need to know which ports your SQL Server instance is using.</span></span> <span data-ttu-id="a805e-155">這將取決於建立和設定 SQL Server 實例的方式：</span><span class="sxs-lookup"><span data-stu-id="a805e-155">This will depend on how the SQL Server instance was created and configured:</span></span>

- <span data-ttu-id="a805e-156">SQL Server 的*預設實例*會接聽 TCP 通訊埠1433上的（並回應）要求。</span><span class="sxs-lookup"><span data-stu-id="a805e-156">A *default instance* of SQL Server listens for (and responds to) requests on TCP port 1433.</span></span>
- <span data-ttu-id="a805e-157">的*已命名實例*SQL Server 會在動態指派的 TCP 通訊埠上接聽（並回應）要求。</span><span class="sxs-lookup"><span data-stu-id="a805e-157">A *named instance* of SQL Server listens for (and responds to) requests on a dynamically assigned TCP port.</span></span>
- <span data-ttu-id="a805e-158">如果 SQL Server Browser 服務已啟用，用戶端就可以在 UDP 埠1434上查詢服務，以找出特定 SQL Server 實例所要使用的 TCP 埠。</span><span class="sxs-lookup"><span data-stu-id="a805e-158">If the SQL Server Browser service is enabled, clients can query the service on UDP port 1434 to find out which TCP port to use for a particular SQL Server instance.</span></span> <span data-ttu-id="a805e-159">不過，基於安全性理由，這種服務通常是停用的。</span><span class="sxs-lookup"><span data-stu-id="a805e-159">However, this service is often disabled for security reasons.</span></span>

<span data-ttu-id="a805e-160">假設您使用 SQL Server 的預設實例，您需要設定防火牆以允許流量。</span><span class="sxs-lookup"><span data-stu-id="a805e-160">Assuming that you're using a default instance of SQL Server, you need to configure your firewall to allow traffic.</span></span>

| <span data-ttu-id="a805e-161">方向</span><span class="sxs-lookup"><span data-stu-id="a805e-161">Direction</span></span> | <span data-ttu-id="a805e-162">來源埠</span><span class="sxs-lookup"><span data-stu-id="a805e-162">From Port</span></span> | <span data-ttu-id="a805e-163">至埠</span><span class="sxs-lookup"><span data-stu-id="a805e-163">To Port</span></span> | <span data-ttu-id="a805e-164">連接埠類型</span><span class="sxs-lookup"><span data-stu-id="a805e-164">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a805e-165">輸入</span><span class="sxs-lookup"><span data-stu-id="a805e-165">Inbound</span></span> | <span data-ttu-id="a805e-166">Any</span><span class="sxs-lookup"><span data-stu-id="a805e-166">Any</span></span> | <span data-ttu-id="a805e-167">1433</span><span class="sxs-lookup"><span data-stu-id="a805e-167">1433</span></span> | <span data-ttu-id="a805e-168">TCP</span><span class="sxs-lookup"><span data-stu-id="a805e-168">TCP</span></span> |
| <span data-ttu-id="a805e-169">輸出</span><span class="sxs-lookup"><span data-stu-id="a805e-169">Outbound</span></span> | <span data-ttu-id="a805e-170">1433</span><span class="sxs-lookup"><span data-stu-id="a805e-170">1433</span></span> | <span data-ttu-id="a805e-171">Any</span><span class="sxs-lookup"><span data-stu-id="a805e-171">Any</span></span> | <span data-ttu-id="a805e-172">TCP</span><span class="sxs-lookup"><span data-stu-id="a805e-172">TCP</span></span> |

> [!NOTE]
> <span data-ttu-id="a805e-173">就技術上來說，用戶端電腦會使用介於1024和5000之間的隨機指派 TCP 埠來與 SQL Server 通訊，而且您可以據以限制您的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a805e-173">Technically, a client computer will use a randomly assigned TCP port between 1024 and 5000 to communicate with SQL Server, and you can restrict your firewall rules accordingly.</span></span> <span data-ttu-id="a805e-174">如需 SQL Server 埠和防火牆的詳細資訊，請參閱透過[防火牆與 SQL 進行通訊所需的 tcp/ip 埠號碼](https://go.microsoft.com/?linkid=9805125)和[如何：設定伺服器接聽特定 TCP 通訊埠（SQL Server 組態管理員）](https://msdn.microsoft.com/library/ms177440.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a805e-174">For more information on SQL Server ports and firewalls, see [TCP/IP port numbers required to communicate to SQL over a firewall](https://go.microsoft.com/?linkid=9805125) and [How to: Configure a Server to Listen on a Specific TCP Port (SQL Server Configuration Manager)](https://msdn.microsoft.com/library/ms177440.aspx).</span></span>

<span data-ttu-id="a805e-175">在大部分的 Windows Server 環境中，您可能必須在資料庫伺服器上設定 Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="a805e-175">In most Windows Server environments, you'll likely have to configure Windows Firewall on the database server.</span></span> <span data-ttu-id="a805e-176">根據預設，除非規則特別禁止，否則 Windows 防火牆會允許所有輸出流量。</span><span class="sxs-lookup"><span data-stu-id="a805e-176">By default, Windows Firewall allows all outbound traffic unless a rule specifically prohibits it.</span></span> <span data-ttu-id="a805e-177">若要讓您的網頁伺服器能夠連線到您的資料庫，您必須設定輸入規則，以允許 SQL Server 實例所使用之埠號碼的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="a805e-177">To enable your web server to reach your database, you need to configure an inbound rule that allows TCP traffic on the port number that the SQL Server instance uses.</span></span> <span data-ttu-id="a805e-178">如果您使用 SQL Server 的預設實例，您可以使用下一個程式來設定此規則。</span><span class="sxs-lookup"><span data-stu-id="a805e-178">If you're using a default instance of SQL Server, you can use the next procedure to configure this rule.</span></span>

<span data-ttu-id="a805e-179">**若要將 Windows 防火牆設定為允許與預設 SQL Server 實例通訊**</span><span class="sxs-lookup"><span data-stu-id="a805e-179">**To configure Windows Firewall to allow communication with a default SQL Server instance**</span></span>

1. <span data-ttu-id="a805e-180">在資料庫伺服器的 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [**具有 Advanced Security 的 Windows 防火牆**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-180">On the database server, on the **Start** menu, point to **Administrative Tools**, and then click **Windows Firewall with Advanced Security**.</span></span>
2. <span data-ttu-id="a805e-181">在樹狀檢視窗格中，按一下 [**輸入規則**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-181">In the tree view pane, click **Inbound Rules**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. <span data-ttu-id="a805e-182">在 [**動作**] 窗格的 [**輸入規則**] 底下，按一下 [**新增規則**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-182">In the **Actions** pane, under **Inbound Rules**, click **New Rule**.</span></span>
4. <span data-ttu-id="a805e-183">在 [新增輸入規則嚮導] 的 [**規則類型**] 頁面上，選取 [**埠**]，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-183">In the New Inbound Rule Wizard, on the **Rule Type** page, select **Port**, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. <span data-ttu-id="a805e-184">在 [**通訊協定和埠**] 頁面上，確定已選取 [ **TCP** ]，然後在 [**特定本機埠**] 方塊中輸入**1433**，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-184">On the **Protocol and Ports** page, ensure that **TCP** is selected, and in the **Specific local ports** box, type **1433**, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. <span data-ttu-id="a805e-185">在 [**動作**] 頁面上，保持選取 **[允許連接**]，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-185">On the **Action** page, leave **Allow the connection** selected and click **Next**.</span></span>
7. <span data-ttu-id="a805e-186">在 **設定檔** 頁面上，保持選取 **網域**，清除 **私**用 和 **公用** 核取方塊，然後按**下一步**</span><span class="sxs-lookup"><span data-stu-id="a805e-186">On the **Profile** page, leave **Domain** selected, clear the **Private** and **Public** check boxes, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. <span data-ttu-id="a805e-187">在 [**名稱**] 頁面上，為規則提供適當的描述性名稱（例如， **SQL Server 預設實例–網路存取**），然後按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-187">On the **Name** page, give the rule a suitably descriptive name (for example, **SQL Server default instance – network access**), and then click **Finish**.</span></span>

<span data-ttu-id="a805e-188">如需設定 Windows 防火牆以進行 SQL Server 的詳細資訊，特別是當您需要透過非標準或動態埠與 SQL Server 通訊時，請參閱 how [to： Configure a Windows firewall for 資料庫引擎 Access](https://technet.microsoft.com/library/ms175043.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a805e-188">For more information on configuring Windows Firewall for SQL Server, particularly if you need to communicate with SQL Server over non-standard or dynamic ports, see [How to: Configure a Windows Firewall for Database Engine Access](https://technet.microsoft.com/library/ms175043.aspx).</span></span>

## <a name="configure-logins-and-database-permissions"></a><span data-ttu-id="a805e-189">設定登入和資料庫許可權</span><span class="sxs-lookup"><span data-stu-id="a805e-189">Configure Logins and Database Permissions</span></span>

<span data-ttu-id="a805e-190">當您將 web 應用程式部署至 Internet Information Services （IIS）時，應用程式會使用應用程式集區的身分識別來執行。</span><span class="sxs-lookup"><span data-stu-id="a805e-190">When you deploy a web application to Internet Information Services (IIS), the application runs using the identity of the application pool.</span></span> <span data-ttu-id="a805e-191">在網域環境中，應用程式集區身分識別會使用其執行所在之伺服器的電腦帳戶來存取網路資源。</span><span class="sxs-lookup"><span data-stu-id="a805e-191">In a domain environment, application pool identities use the machine account of the server on which they run to access network resources.</span></span> <span data-ttu-id="a805e-192">電腦帳戶的格式為<em>[功能變數名稱]</em><strong>\</strong ><em>[電腦名稱稱]</em> <strong>$</strong> &#x2014;例如， <strong>FABRIKAM\TESTWEB1 $</strong>。</span><span class="sxs-lookup"><span data-stu-id="a805e-192">Machine accounts take the form <em>[domain name]</em><strong>\</strong><em>[machine name]</em><strong>$</strong>&#x2014;for example, <strong>FABRIKAM\TESTWEB1$</strong>.</span></span> <span data-ttu-id="a805e-193">若要允許您的 web 應用程式透過網路存取資料庫，您需要：</span><span class="sxs-lookup"><span data-stu-id="a805e-193">To allow your web application to access a database across the network, you need to:</span></span>

- <span data-ttu-id="a805e-194">將 web 伺服器電腦帳戶的登入新增至 SQL Server 實例。</span><span class="sxs-lookup"><span data-stu-id="a805e-194">Add a login for the web server machine account to the SQL Server instance.</span></span>
- <span data-ttu-id="a805e-195">將電腦帳戶登入對應到任何必要的資料庫角色（通常是**db\_datareader**和**db\_資料寫入元**）。</span><span class="sxs-lookup"><span data-stu-id="a805e-195">Map the machine account login to any required database roles (typically **db\_datareader** and **db\_datawriter**).</span></span>

<span data-ttu-id="a805e-196">如果您的 web 應用程式是在伺服器陣列上執行，而不是單一伺服器，您必須針對伺服器陣列中的每一部 web 伺服器重複這些程式。</span><span class="sxs-lookup"><span data-stu-id="a805e-196">If your web application is running on a server farm, rather than a single server, you'll need to repeat these procedures for every web server in the server farm.</span></span>

> [!NOTE]
> <span data-ttu-id="a805e-197">如需應用程式集區身分識別和存取網路資源的詳細資訊，請參閱[應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。</span><span class="sxs-lookup"><span data-stu-id="a805e-197">For more information on application pool identities and accessing network resources, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="a805e-198">您可以透過各種方式來處理這些工作。</span><span class="sxs-lookup"><span data-stu-id="a805e-198">You can approach these tasks in various ways.</span></span> <span data-ttu-id="a805e-199">若要建立登入，您可以執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="a805e-199">To create the login, you can either:</span></span>

- <span data-ttu-id="a805e-200">使用 Transact-sql 或 SQL Server Management Studio，以手動方式在資料庫伺服器上建立登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-200">Create the login manually on the database server, using Transact-SQL or SQL Server Management Studio.</span></span>
- <span data-ttu-id="a805e-201">使用 Visual Studio 中的 SQL Server 2008 伺服器專案來建立和部署登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-201">Use a SQL Server 2008 Server Project in Visual Studio to create and deploy the login.</span></span>

<span data-ttu-id="a805e-202">SQL Server 登入是伺服器層級物件，而不是資料庫層級物件，因此不會相依于您想要部署的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a805e-202">A SQL Server login is a server-level object, rather than a database-level object, so it's not dependent on the database you want to deploy.</span></span> <span data-ttu-id="a805e-203">因此，您可以在任何時間點建立登入，最簡單的方法通常是在開始部署資料庫之前，手動在資料庫伺服器上建立登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-203">As such, you can create the login at any point, and the easiest approach is often to create the login manually on the database server before you start deploying databases.</span></span> <span data-ttu-id="a805e-204">您可以使用下一個程式，在 SQL Server Management Studio 中建立登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-204">You can use the next procedure to create a login in SQL Server Management Studio.</span></span>

<span data-ttu-id="a805e-205">**若要建立 web 伺服器電腦帳戶的 SQL Server 登入**</span><span class="sxs-lookup"><span data-stu-id="a805e-205">**To create a SQL Server login for the web server machine account**</span></span>

1. <span data-ttu-id="a805e-206">在資料庫伺服器的 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft SQL Server 2008 R2**]，然後按一下 [ **SQL Server Management Studio**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-206">On the database server, on the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="a805e-207">在 [**連接到伺服器**] 對話方塊的 [**伺服器名稱**] 方塊中，輸入資料庫伺服器的名稱，然後按一下 **[連接]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-207">In the **Connect to Server** dialog box, in the **Server name** box, type the name of the database server, and then click **Connect**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. <span data-ttu-id="a805e-208">在 [**物件總管**] 窗格中，以滑鼠右鍵按一下 [**安全性**]，指向 [**新增**]，然後按一下 **[登**入]。</span><span class="sxs-lookup"><span data-stu-id="a805e-208">In the **Object Explorer** pane, right-click **Security**, point to **New**, and then click **Login**.</span></span>
4. <span data-ttu-id="a805e-209">在 [**登入-新增**] 對話方塊的 [**登入名稱**] 方塊中，輸入您的 web 伺服器電腦帳戶名稱（例如， **FABRIKAM\TESTWEB1 $** ）。</span><span class="sxs-lookup"><span data-stu-id="a805e-209">In the **Login – New** dialog box, in the **Login name** box, type the name of your web server machine account (for example, **FABRIKAM\TESTWEB1$**).</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. <span data-ttu-id="a805e-210">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a805e-210">Click **OK**.</span></span>

<span data-ttu-id="a805e-211">此時，您的資料庫伺服器已準備好進行 Web Deploy 發佈。</span><span class="sxs-lookup"><span data-stu-id="a805e-211">At this point, your database server is ready for Web Deploy publishing.</span></span> <span data-ttu-id="a805e-212">不過，在您將電腦帳戶登入對應到所需的資料庫角色之前，您部署的任何解決方案都將無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="a805e-212">However, any solutions you deploy won't work until you map the machine account login to the required database roles.</span></span> <span data-ttu-id="a805e-213">將登入對應到資料庫角色需要更多的想法，因為您必須等到部署資料庫之後，才能對應角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-213">Mapping the login to database roles requires a lot more thought, as you can't map roles until after you've deployed the database.</span></span> <span data-ttu-id="a805e-214">若要將電腦帳戶登入對應到所需的資料庫角色，您可以執行下列其中一項動作：</span><span class="sxs-lookup"><span data-stu-id="a805e-214">To map the machine account login to the required database roles, you can either:</span></span>

- <span data-ttu-id="a805e-215">在您第一次部署資料庫之後，手動將資料庫角色指派給登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-215">Assign the database roles to the login manually, after you've deployed the database for the first time.</span></span>
- <span data-ttu-id="a805e-216">使用部署後腳本，將資料庫角色指派給登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-216">Use a post-deployment script to assign the database roles to the login.</span></span>

<span data-ttu-id="a805e-217">如需有關自動建立登入和資料庫角色對應的詳細資訊，請參閱[將資料庫角色成員資格部署到測試環境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="a805e-217">For more information on automating the creation of logins and database role mappings, see [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span> <span data-ttu-id="a805e-218">或者，您可以使用下一個程式，以手動方式將電腦帳戶登入對應到所需的資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-218">Alternatively, you can use the next procedure to map the machine account login to the required database roles manually.</span></span> <span data-ttu-id="a805e-219">請記住 *，在部署資料庫之前，* 您無法執行此程式。</span><span class="sxs-lookup"><span data-stu-id="a805e-219">Remember that you can't perform this procedure until *after* you've deployed the database.</span></span>

<span data-ttu-id="a805e-220">**若要將資料庫角色對應至 web 伺服器電腦帳戶登入**</span><span class="sxs-lookup"><span data-stu-id="a805e-220">**To map database roles to the web server machine account login**</span></span>

1. <span data-ttu-id="a805e-221">如先前一樣開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="a805e-221">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="a805e-222">在 [**物件總管**] 窗格中，依序展開 [**安全性**] 節點和 [登入 **] 節點，** 然後連按兩下電腦帳戶（例如**FABRIKAM\TESTWEB1 $** ）。</span><span class="sxs-lookup"><span data-stu-id="a805e-222">In the **Object Explorer** pane, expand the **Security** node, expand the **Logins** node, and then double-click the machine account login (for example, **FABRIKAM\TESTWEB1$**).</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. <span data-ttu-id="a805e-223">在 [**登入屬性**] 對話方塊中，按一下 [**使用者對應**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-223">In the **Login Properties** dialog box, click **User Mapping**.</span></span>
4. <span data-ttu-id="a805e-224">在 [**對應至此登**入的使用者] 資料表中，選取您的資料庫名稱（例如， **ContactManager**）。</span><span class="sxs-lookup"><span data-stu-id="a805e-224">In the **Users mapped to this login** table, select the name of your database (for example, **ContactManager**).</span></span>
5. <span data-ttu-id="a805e-225">在 [**資料庫角色成員資格：** *[資料庫名稱]]* 清單中，選取所需的許可權。</span><span class="sxs-lookup"><span data-stu-id="a805e-225">In the **Database role membership for:** *[database name]* list, select the permissions required.</span></span> <span data-ttu-id="a805e-226">在 Contact Manager 範例解決方案的情況下，您必須選取**db\_datareader**和**db\_資料寫入元**角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-226">In the case of the Contact Manager sample solution, you must select the **db\_datareader** and **db\_datawriter** roles.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. <span data-ttu-id="a805e-227">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a805e-227">Click **OK**.</span></span>

<span data-ttu-id="a805e-228">雖然手動對應資料庫角色通常會比測試環境所需的還多，但對臨時或生產環境的自動化或單鍵部署較不理想。</span><span class="sxs-lookup"><span data-stu-id="a805e-228">While manually mapping database roles is often more than adequate for test environments, it's less desirable for automated or one-click deployments to staging or production environments.</span></span> <span data-ttu-id="a805e-229">您可以使用[部署資料庫角色成員資格](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)中的部署後腳本，在測試環境中找到自動化這種工作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a805e-229">You can find more information on automating this kind of task using post-deployment scripts in [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a805e-230">如需伺服器專案和資料庫專案的詳細資訊，請參閱[Visual Studio 2010 SQL Server 資料庫專案](https://msdn.microsoft.com/library/ff678491.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a805e-230">For more information on server projects and database projects, see [Visual Studio 2010 SQL Server Database Projects](https://msdn.microsoft.com/library/ff678491.aspx).</span></span>

## <a name="configure-permissions-for-the-deployment-account"></a><span data-ttu-id="a805e-231">設定部署帳戶的許可權</span><span class="sxs-lookup"><span data-stu-id="a805e-231">Configure Permissions for the Deployment Account</span></span>

<span data-ttu-id="a805e-232">如果您用來執行部署的帳戶不是 SQL Server 系統管理員，您也必須為此帳戶建立登入。</span><span class="sxs-lookup"><span data-stu-id="a805e-232">If the account that you'll use to run the deployment is not a SQL Server administrator, you'll also need to create a login for this account.</span></span> <span data-ttu-id="a805e-233">若要建立資料庫，帳戶必須是**dbcreator**伺服器角色的成員，或具有對等的許可權。</span><span class="sxs-lookup"><span data-stu-id="a805e-233">In order to create the database, the account must be a member of the **dbcreator** server role or have equivalent permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="a805e-234">當您使用 Web Deploy 或 VSDBCMD 部署資料庫時，可以使用 Windows 認證或 SQL Server 認證（如果您的 SQL Server 實例設定為支援混合模式驗證）。</span><span class="sxs-lookup"><span data-stu-id="a805e-234">When you use Web Deploy or VSDBCMD to deploy a database, you can use Windows credentials or SQL Server credentials (if your SQL Server instance is configured to support mixed mode authentication).</span></span> <span data-ttu-id="a805e-235">下一個程式假設您想要使用 Windows 認證，但當您設定部署時，並不會阻止您在連接字串中指定 SQL Server 的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="a805e-235">The next procedure assumes that you want to use Windows credentials, but there's nothing stopping you from specifying a SQL Server user name and password in your connection string when you configure the deployment.</span></span>

<span data-ttu-id="a805e-236">**設定部署帳戶的許可權**</span><span class="sxs-lookup"><span data-stu-id="a805e-236">**To set up permissions for the deployment account**</span></span>

1. <span data-ttu-id="a805e-237">如先前一樣開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="a805e-237">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="a805e-238">在 [**物件總管**] 窗格中，以滑鼠右鍵按一下 [**安全性**]，指向 [**新增**]，然後按一下 **[登**入]。</span><span class="sxs-lookup"><span data-stu-id="a805e-238">In the **Object Explorer** pane, right-click **Security**, point to **New**, and then click **Login**.</span></span>
3. <span data-ttu-id="a805e-239">在 [**登入-新增**] 對話方塊的 [**登入名稱**] 方塊中，輸入部署帳戶的名稱（例如， **FABRIKAM\matt**）。</span><span class="sxs-lookup"><span data-stu-id="a805e-239">In the **Login – New** dialog box, in the **Login name** box, type the name of your deployment account (for example, **FABRIKAM\matt**).</span></span>
4. <span data-ttu-id="a805e-240">在 [**選取頁面**] 窗格中，按一下 [**伺服器角色**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-240">In the **Select a page** pane, click **Server Roles**.</span></span>
5. <span data-ttu-id="a805e-241">選取 [ **Dbcreator**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="a805e-241">Select **dbcreator**, and then click **OK**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

<span data-ttu-id="a805e-242">若要支援後續部署，您也必須在第一次部署之後，將部署帳戶新增至資料庫上的**db\_擁有**者角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-242">To support subsequent deployments, you'll also need to add the deploying account to the **db\_owner** role on the database after the first deployment.</span></span> <span data-ttu-id="a805e-243">這是因為在後續的部署中，您要修改現有資料庫的架構，而不是建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a805e-243">This is because on subsequent deployments you're modifying the schema of an existing database, rather than creating a new database.</span></span> <span data-ttu-id="a805e-244">如上一節所述，在您建立資料庫之前，您無法將使用者加入至資料庫角色，原因很明顯。</span><span class="sxs-lookup"><span data-stu-id="a805e-244">As described in the previous section, you can't add a user to a database role until you've created the database, for obvious reasons.</span></span>

<span data-ttu-id="a805e-245">**將部署帳戶登入對應至 db\_擁有者資料庫角色**</span><span class="sxs-lookup"><span data-stu-id="a805e-245">**To map the deployment account login to the db\_owner database role**</span></span>

1. <span data-ttu-id="a805e-246">如先前一樣開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="a805e-246">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="a805e-247">在 [**物件總管**] 視窗中，依序展開 [**安全性**] 節點和 [登入 **] 節點，** 然後連按兩下電腦帳戶（例如， **FABRIKAM\matt**）。</span><span class="sxs-lookup"><span data-stu-id="a805e-247">In the **Object Explorer** window, expand the **Security** node, expand the **Logins** node, and then double-click the machine account login (for example, **FABRIKAM\matt**).</span></span>
3. <span data-ttu-id="a805e-248">在 [**登入屬性**] 對話方塊中，按一下 [**使用者對應**]。</span><span class="sxs-lookup"><span data-stu-id="a805e-248">In the **Login Properties** dialog box, click **User Mapping**.</span></span>
4. <span data-ttu-id="a805e-249">在 [**對應至此登**入的使用者] 資料表中，選取您的資料庫名稱（例如， **ContactManager**）。</span><span class="sxs-lookup"><span data-stu-id="a805e-249">In the **Users mapped to this login** table, select the name of your database (for example, **ContactManager**).</span></span>
5. <span data-ttu-id="a805e-250">在 [**資料庫角色成員資格：** *[資料庫名稱]]* 清單中，選取 [ **db\_擁有**者] 角色。</span><span class="sxs-lookup"><span data-stu-id="a805e-250">In the **Database role membership for:** *[database name]* list, select the **db\_owner** role.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. <span data-ttu-id="a805e-251">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a805e-251">Click **OK**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a805e-252">結論</span><span class="sxs-lookup"><span data-stu-id="a805e-252">Conclusion</span></span>

<span data-ttu-id="a805e-253">您的資料庫伺服器現在應該已準備好接受遠端資料庫部署，並允許遠端 IIS 網頁伺服器存取您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a805e-253">Your database server should now be ready to accept remote database deployments and to allow remote IIS web servers to access your databases.</span></span> <span data-ttu-id="a805e-254">在您嘗試部署和使用資料庫之前，您可能會想要檢查下列重點：</span><span class="sxs-lookup"><span data-stu-id="a805e-254">Before you attempt to deploy and use databases, you may want to check these key points:</span></span>

- <span data-ttu-id="a805e-255">您是否已設定 SQL Server 接受遠端 TCP/IP 連接？</span><span class="sxs-lookup"><span data-stu-id="a805e-255">Have you configured SQL Server to accept remote TCP/IP connections?</span></span>
- <span data-ttu-id="a805e-256">您是否已設定任何防火牆以允許 SQL Server 流量？</span><span class="sxs-lookup"><span data-stu-id="a805e-256">Have you configured any firewalls to permit SQL Server traffic?</span></span>
- <span data-ttu-id="a805e-257">您是否已針對將存取 SQL Server 的每一部 web 伺服器建立電腦帳戶登入？</span><span class="sxs-lookup"><span data-stu-id="a805e-257">Have you created a machine account login for every web server that will access SQL Server?</span></span>
- <span data-ttu-id="a805e-258">您的資料庫部署是否包含用來建立使用者角色對應的腳本，或者您是否需要在第一次部署資料庫之後手動建立這些專案？</span><span class="sxs-lookup"><span data-stu-id="a805e-258">Does your database deployment include a script to create user role mappings, or do you need to create these manually after you deploy the database for the first time?</span></span>
- <span data-ttu-id="a805e-259">您是否已建立部署帳戶的登入，並將它新增至**dbcreator**伺服器角色？</span><span class="sxs-lookup"><span data-stu-id="a805e-259">Have you created a login for the deployment account and added it to the **dbcreator** server role?</span></span>

## <a name="further-reading"></a><span data-ttu-id="a805e-260">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="a805e-260">Further Reading</span></span>

<span data-ttu-id="a805e-261">如需部署資料庫專案的指引，請參閱[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="a805e-261">For guidance on deploying database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="a805e-262">如需執行部署後腳本來建立資料庫角色成員資格的指引，請參閱[將資料庫角色成員資格部署到測試環境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="a805e-262">For guidance on creating database role memberships by running a post-deployment script, see [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span> <span data-ttu-id="a805e-263">如需如何滿足成員資格資料庫所造成之獨特部署挑戰的指引，請參閱將[成員資格資料庫部署到企業環境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="a805e-263">For guidance on how to meet the unique deployment challenges that membership databases pose, see [Deploying Membership Databases to Enterprise Environments](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a805e-264">[上一頁](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [下一頁](creating-a-server-farm-with-the-web-farm-framework.md)</span><span class="sxs-lookup"><span data-stu-id="a805e-264">[Previous](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
[Next](creating-a-server-farm-with-the-web-farm-framework.md)</span></span>
