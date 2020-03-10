---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: 在 TFS 中建立 Team 專案 |Microsoft Docs
author: jrjlee
description: 本主題描述如何在 Team Foundation Server （TFS）2010中建立新的 team 專案。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639654"
---
# <a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="9ebe5-103">在 TFS 中建立 Team 專案</span><span class="sxs-lookup"><span data-stu-id="9ebe5-103">Creating a Team Project in TFS</span></span>

<span data-ttu-id="9ebe5-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="9ebe5-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="9ebe5-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="9ebe5-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="9ebe5-106">本主題描述如何在 Team Foundation Server （TFS）2010中建立新的 team 專案。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>

<span data-ttu-id="9ebe5-107">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="9ebe5-108">工作總覽</span><span class="sxs-lookup"><span data-stu-id="9ebe5-108">Task Overview</span></span>

<span data-ttu-id="9ebe5-109">若要在 TFS 中布建和使用新的 team 專案，您必須完成下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="9ebe5-110">將建立新 team 專案的許可權授與給使用者。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="9ebe5-111">建立 team 專案。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-111">Create the team project.</span></span>
- <span data-ttu-id="9ebe5-112">授與許可權給將在專案上工作的小組成員。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="9ebe5-113">簽入某些內容。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-113">Check in some content.</span></span>

<span data-ttu-id="9ebe5-114">本主題將說明如何執行這些程式，並會識別可能負責每個程式的使用者和作業角色。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="9ebe5-115">請注意，根據您組織的結構，每個工作都可能是不同人員的責任。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="9ebe5-116">本主題中的工作和逐步解說假設您已安裝並設定 TFS，而且您已在設定程式中建立 team 專案集合。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="9ebe5-117">如需這些假設的詳細資訊，以及有關此案例的一般背景資訊，請參閱[設定 Web 部署的 TFS 組建伺服器](configuring-a-tfs-build-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="9ebe5-118">將許可權授與 Team 專案建立者</span><span class="sxs-lookup"><span data-stu-id="9ebe5-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="9ebe5-119">若要建立新的 team 專案，您需要下列許可權：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="9ebe5-120">您必須擁有 TFS 應用層的 [**建立新專案**] 許可權。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="9ebe5-121">您通常會藉由將使用者加入至 [ **Project Collection Administrators** ] TFS 群組來授與此許可權。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="9ebe5-122">[ **Team Foundation Administrators** ] 全域群組也包含此許可權。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="9ebe5-123">您必須擁有在對應至 TFS team 專案集合的 SharePoint 網站集合中，建立新小組網站的許可權。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="9ebe5-124">您通常會將使用者新增至 SharePoint 群組（具有 SharePoint 網站集合的 [**完全控制**] 許可權），以授與此許可權。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="9ebe5-125">如果您使用 SQL Server Reporting Services 功能，您必須是 Reporting Services 中 [ **Team Foundation 內容管理員**] 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="9ebe5-126">誰執行這些程式？</span><span class="sxs-lookup"><span data-stu-id="9ebe5-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="9ebe5-127">一般而言，負責管理 TFS 部署的人員或群組也會執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="9ebe5-128">由於這是一組高度許可權的許可權，因此新的 team 專案通常是由一小部分的使用者所建立，負責管理 TFS 部署。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="9ebe5-129">開發人員通常不會被授與建立新 team 專案所需的許可權。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="9ebe5-130">在 TFS 中授與許可權</span><span class="sxs-lookup"><span data-stu-id="9ebe5-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="9ebe5-131">如果您想要讓使用者建立新的 team 專案，第一個高階工作就是將使用者加入 team 專案集合的**Project Collection Administrators**群組。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="9ebe5-132">**若要將使用者加入至專案集合系統管理員群組**</span><span class="sxs-lookup"><span data-stu-id="9ebe5-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="9ebe5-133">在 TFS 伺服器的 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft Team Foundation Server 2010**]，然後按一下 [ **Team Foundation 管理主控台**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="9ebe5-134">在導覽樹狀檢視中，展開 [**應用層**]，然後按一下 [ **Team 專案集合**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="9ebe5-135">在 [ **Team 專案集合**] 窗格中，選取您要管理的 Team 專案集合。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="9ebe5-136">在 [**一般**] 索引標籤上，按一下 [**群組成員資格**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="9ebe5-137">在 [**全域群組**] 對話方塊中，選取 [ **Project Collection Administrators** ] 群組，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="9ebe5-138">在 [ **Team Foundation Server 群組屬性**] 對話方塊中，選取 [ **Windows 使用者或群組**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="9ebe5-139">在 [**選取使用者、電腦或群組**] 對話方塊中，輸入您要能夠建立新 team 專案的使用者使用者名稱，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="9ebe5-140">在 [ **Team Foundation Server 群組屬性**] 對話方塊中，按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="9ebe5-141">在 [**全域群組**] 對話方塊中，按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="9ebe5-142">授與 SharePoint Services 中的許可權</span><span class="sxs-lookup"><span data-stu-id="9ebe5-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="9ebe5-143">接下來，您必須授與使用者在對應至 TFS team 專案集合的 SharePoint 網站集合中，建立新小組網站的許可權。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="9ebe5-144">**授與 SharePoint 網站集合的完全控制許可權**</span><span class="sxs-lookup"><span data-stu-id="9ebe5-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="9ebe5-145">在 Team Foundation Server 管理主控台的  **Team 專案集合** 頁面上，選取您要管理的 team 專案集合。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="9ebe5-146">在 [ **SharePoint 網站**] 索引標籤上，記下**目前預設網站位置**URL 的值。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="9ebe5-147">開啟 Internet Explorer，然後移至您在步驟2記下的 URL。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ebe5-148">如果您不是以建立 team 專案集合的使用者身分登入 Windows，則必須以這位使用者的身分登入 SharePoint，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="9ebe5-149">在 **[網站動作]** 功能表上，按一下 **[網站設定]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="9ebe5-150">在 [**網站設定**] 頁面的 [**使用者和許可權**] 底下，按一下 [**人員和群組**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="9ebe5-151">在左側導覽窗格中，按一下 [**群組**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="9ebe5-152">在 [**人員和群組：所有群組**] 頁面上，按一下 [**設定此網站的群組**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="9ebe5-153">由於雙重 HTTP 編碼錯誤，您可能會收到<strong>HTTP 404 找不</strong>到的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="9ebe5-154">如果發生這種情況，請以下列內容取代 URL：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="9ebe5-155">例如 `[site_collection_URL]/_layouts/permsetup.aspx`：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="9ebe5-156">在 [**設定此網站的群組**] 頁面上，將建立 team 專案的使用者新增至 [**擁有**者] 群組，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="9ebe5-157">如需有關如何讓使用者在 team 專案集合中建立新 team 專案的詳細資訊，請參閱[設定 Team 專案集合的系統管理員許可權](https://msdn.microsoft.com/library/dd547204.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="9ebe5-158">建立新的 Team 專案並新增使用者</span><span class="sxs-lookup"><span data-stu-id="9ebe5-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="9ebe5-159">當您擁有必要的許可權之後，就可以使用 Visual Studio 2010 中的 [ **Team Explorer** ] 視窗來建立新的 Team 專案。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="9ebe5-160">這個方法會提供一個 wizard，以收集所有必要的資訊，並在 TFS、SharePoint 和 SQL Server Reporting Services 中執行必要的工作。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="9ebe5-161">您也必須將新 team 專案的許可權授與開發人員小組的成員，讓他們能夠新增和修改內容。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="9ebe5-162">誰執行這些程式？</span><span class="sxs-lookup"><span data-stu-id="9ebe5-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="9ebe5-163">通常 TFS 系統管理員或開發人員小組領導人都會執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="9ebe5-164">建立新的 Team 專案</span><span class="sxs-lookup"><span data-stu-id="9ebe5-164">Create a New Team Project</span></span>

<span data-ttu-id="9ebe5-165">下一個程式描述如何在 TFS 2010 中建立新的 team 專案。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="9ebe5-166">**若要建立新的 team 專案**</span><span class="sxs-lookup"><span data-stu-id="9ebe5-166">**To create a new team project**</span></span>

1. <span data-ttu-id="9ebe5-167">在 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft Visual Studio 2010**]，以滑鼠右鍵按一下 [ **Microsoft Visual Studio 2010**]，然後按一下 [以**系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ebe5-168">如果您未以系統管理員的身分執行 Visual Studio 2010，則在最後一個步驟中，[新增 Team 專案嚮導] 將會失敗。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="9ebe5-169">如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="9ebe5-170">在 Visual Studio 的 [**小組**] 功能表上，按一下 [**連接到 Team Foundation Server]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ebe5-171">如果您已經設定與 TFS 伺服器的連接，您可以省略步驟4-7。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="9ebe5-172">在 [**連接到 Team 專案**] 對話方塊中，按一下 [**伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="9ebe5-173">在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="9ebe5-174">在 [**新增 Team Foundation Server** ] 對話方塊中，提供 TFS 實例的詳細資料，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="9ebe5-175">在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="9ebe5-176">在 [**連接到 Team 專案**] 對話方塊中，選取您要連接的 TFS 實例，選取您要加入的 Team 專案集合，然後按一下 **[連接]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="9ebe5-177">在 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下 Team 專案集合，然後按一下 [**新增 team 專案**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="9ebe5-178">在 [**新增 Team 專案**] 對話方塊中，提供 Team 專案的 [名稱] 和 [描述]，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ebe5-179">如果您的 team 專案包含空格，當您使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）從輸出路徑部署封裝時，可能會遇到一些問題。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="9ebe5-180">路徑中的空格可能會使 Web Deploy 命令的執行變得更容易。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="9ebe5-181">在 [**選取流程範本**] 頁面上，選取您要用來管理開發進程的流程範本，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ebe5-182">如需 TFS 流程範本的詳細資訊，請參閱[流程範本和工具](https://msdn.microsoft.com/vstudio/aa718795)。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="9ebe5-183">在 [**小組網站設定**] 頁面上，保留預設設定不變，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="9ebe5-184">此設定會建立或識別與 TFS team 專案相關聯的 SharePoint 小組網站。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="9ebe5-185">您的開發小組可以使用這個網站來管理檔、參與討論執行緒、建立 wiki 頁面，以及執行與程式碼無關的其他工作。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="9ebe5-186">如需詳細資訊，請參閱[SharePoint 產品與 Team Foundation Server 之間的互動](https://msdn.microsoft.com/library/ms253177.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="9ebe5-187">在 [**指定原始檔控制設定**] 頁面上，保留預設設定不變，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="9ebe5-188">此設定會識別或建立 TFS 資料夾階層中的位置，以作為內容的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="9ebe5-189">在 [**確認 Team 專案設定**] 頁面上，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="9ebe5-190">成功建立新的 team 專案時，請在 [ **Team 專案建立**] 頁面上按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="9ebe5-191">將使用者加入至 Team 專案</span><span class="sxs-lookup"><span data-stu-id="9ebe5-191">Add Users to a Team Project</span></span>

<span data-ttu-id="9ebe5-192">既然您已建立新的 team 專案，您可以授與許可權給使用者，讓他們能夠開始加入和共同作業內容。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="9ebe5-193">**若要將使用者加入至 team 專案**</span><span class="sxs-lookup"><span data-stu-id="9ebe5-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="9ebe5-194">在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下 team 專案，指向 [ **team 專案設定**]，然後按一下 [**群組成員資格**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="9ebe5-195">若要讓使用者加入、修改和移除原始檔控制下的程式碼，您必須將他或她加入至**Contributors**群組。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="9ebe5-196">在 [**專案群組**] 對話方塊中，選取 [ **Contributors** ] 群組，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="9ebe5-197">在 [ **Team Foundation Server 群組屬性**] 對話方塊中，選取 [ **Windows 使用者或群組**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="9ebe5-198">在 [**選取使用者、電腦或群組**] 對話方塊中，輸入您要加入至 team 專案之使用者的使用者名稱，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="9ebe5-199">在 [ **Team Foundation Server 群組屬性**] 對話方塊中，按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="9ebe5-200">在 [**專案群組**] 對話方塊中，按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9ebe5-201">結論</span><span class="sxs-lookup"><span data-stu-id="9ebe5-201">Conclusion</span></span>

<span data-ttu-id="9ebe5-202">此時，您的新 team 專案已準備好可供使用，而您的開發人員小組可以開始在開發程式上新增內容和共同作業。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="9ebe5-203">下一個主題 [[將內容新增至原始檔控制](adding-content-to-source-control.md)] 會說明如何將內容加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="9ebe5-204">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="9ebe5-204">Further Reading</span></span>

<span data-ttu-id="9ebe5-205">如需在 TFS 中建立 team 專案的更廣泛指引，請參閱[建立 Team 專案](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="9ebe5-206">如需有關如何讓使用者在 team 專案集合中建立新 team 專案的詳細資訊，請參閱[設定 Team 專案集合的系統管理員許可權](https://msdn.microsoft.com/library/dd547204.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="9ebe5-207">如需將使用者加入至 team 專案的詳細資訊，請參閱[將使用者加入 Team 專案](https://msdn.microsoft.com/library/bb558971.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9ebe5-208">[上一頁](configuring-team-foundation-server-for-web-deployment.md)
> [下一頁](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="9ebe5-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
