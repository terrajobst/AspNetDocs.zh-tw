---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 將內容加入至原始檔控制 |Microsoft Docs
author: jrjlee
description: 本主題說明如何將內容加入至 Team Foundation Server （TFS）2010中的原始檔控制。 其中說明如何將方案和專案加入至小組 proje 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634460"
---
# <a name="adding-content-to-source-control"></a><span data-ttu-id="df68e-104">將內容新增至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="df68e-104">Adding Content to Source Control</span></span>

<span data-ttu-id="df68e-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="df68e-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="df68e-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="df68e-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="df68e-107">本主題說明如何將內容加入至 Team Foundation Server （TFS）2010中的原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="df68e-108">其中說明如何將方案和專案加入至 TFS 中的 team 專案，並說明如何將外部相依性（例如架構或元件）加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>

<span data-ttu-id="df68e-109">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="df68e-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="df68e-110">工作總覽</span><span class="sxs-lookup"><span data-stu-id="df68e-110">Task Overview</span></span>

<span data-ttu-id="df68e-111">在大部分情況下，開發人員小組的每個成員都應該能夠將內容新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="df68e-112">若要將方案加入至 TFS 中的原始檔控制，您必須完成下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="df68e-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="df68e-113">連接到 team 專案。</span><span class="sxs-lookup"><span data-stu-id="df68e-113">Connect to a team project.</span></span>
- <span data-ttu-id="df68e-114">將伺服器上的 team 專案資料夾結構對應至本機電腦上的資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="df68e-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="df68e-115">將方案和其內容新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="df68e-116">將任何外部相依性加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="df68e-117">本主題將說明如何執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="df68e-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="df68e-118">本主題中的工作和逐步解說假設您已建立新的 TFS team 專案來管理您的內容。</span><span class="sxs-lookup"><span data-stu-id="df68e-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="df68e-119">如需建立新 team 專案的詳細資訊，請參閱[在 TFS 中建立 Team 專案](creating-a-team-project-in-tfs.md)。</span><span class="sxs-lookup"><span data-stu-id="df68e-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="df68e-120">誰執行這些程式？</span><span class="sxs-lookup"><span data-stu-id="df68e-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="df68e-121">在大部分情況下，開發人員小組的每個成員都應該能夠加入和修改特定 team 專案中的內容。</span><span class="sxs-lookup"><span data-stu-id="df68e-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="df68e-122">連接至 Team 專案並建立資料夾對應</span><span class="sxs-lookup"><span data-stu-id="df68e-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="df68e-123">將任何內容加入至原始檔控制之前，您必須先連接到 team 專案，並在伺服器上的資料夾結構和本機電腦上的檔案系統之間建立對應。</span><span class="sxs-lookup"><span data-stu-id="df68e-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="df68e-124">**若要連接至 team 專案並對應本機路徑**</span><span class="sxs-lookup"><span data-stu-id="df68e-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="df68e-125">在開發人員工作站上，開啟 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="df68e-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="df68e-126">在 Visual Studio 的 [**小組**] 功能表上，按一下 [**連接到 Team Foundation Server]** 。</span><span class="sxs-lookup"><span data-stu-id="df68e-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="df68e-127">如果您已經設定與 TFS 伺服器的連接，您可以省略步驟3-6。</span><span class="sxs-lookup"><span data-stu-id="df68e-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="df68e-128">在 [**連接到 Team 專案**] 對話方塊中，按一下 [**伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="df68e-129">在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="df68e-130">在 [**新增 Team Foundation Server** ] 對話方塊中，提供 TFS 實例的詳細資料，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="df68e-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="df68e-131">在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="df68e-132">在 [**連接到 Team 專案**] 對話方塊中，選取您要連接的 TFS 實例，選取 Team 專案集合，選取您要加入的 team 專案，然後按一下 **[連接]** 。</span><span class="sxs-lookup"><span data-stu-id="df68e-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="df68e-133">在 [ **Team Explorer** ] 視窗中，展開您的 Team 專案，然後按兩下 [**原始檔控制**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="df68e-134">在 [**原始檔控制總管**] 索引標籤上，按一下 [**未對應**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="df68e-135">在 [**對應**] 對話方塊的 [**本機資料夾**] 方塊中，流覽（或建立）本機資料夾作為 team 專案的根資料夾，然後按一下 [**對應**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="df68e-136">當系統提示您下載原始檔時，按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="df68e-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="df68e-137">此時，您已將 team 專案的伺服器端資料夾對應至開發人員工作站上的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="df68e-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="df68e-138">您也已將 team 專案中的任何現有內容下載到本機資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="df68e-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="df68e-139">您現在可以開始將自己的內容新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="df68e-140">將專案和方案加入至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="df68e-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="df68e-141">若要將專案和方案加入至原始檔控制，您必須先將它們移至本機電腦上 team 專案的對應資料夾。</span><span class="sxs-lookup"><span data-stu-id="df68e-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="df68e-142">然後您可以簽入內容，將您的新增專案與伺服器同步。</span><span class="sxs-lookup"><span data-stu-id="df68e-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="df68e-143">**若要將專案加入至原始檔控制**</span><span class="sxs-lookup"><span data-stu-id="df68e-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="df68e-144">在開發人員工作站上，將您的專案和方案移至 team 專案對應資料夾結構內的適當位置。</span><span class="sxs-lookup"><span data-stu-id="df68e-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="df68e-145">許多組織都有慣用的方法，可讓您在原始檔控制中組織專案和方案的方式。</span><span class="sxs-lookup"><span data-stu-id="df68e-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="df68e-146">如需如何結構資料夾的指引，請參閱[如何：在 Team Foundation Server 中結構您的原始檔控制資料夾](https://msdn.microsoft.com/library/bb668992.aspx)。</span><span class="sxs-lookup"><span data-stu-id="df68e-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="df68e-147">在 Visual Studio 2010 中開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="df68e-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="df68e-148">在 [**方案總管**] 視窗中，以滑鼠右鍵按一下方案，然後按一下 [**將方案加入至原始檔控制**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="df68e-149">在某些情況下，您可能需要個別將專案新增至原始檔控制，以提供更精細的方式來控制如何組織您的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="df68e-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="df68e-150">確認 [**原始檔控制總管**] 索引標籤會顯示您已在 team 專案的伺服器資料夾結構中新增的內容。</span><span class="sxs-lookup"><span data-stu-id="df68e-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="df68e-151">[**原始檔控制總管**] 索引標籤會顯示您的內容，而不會進一步提示，因為您已將解決方案新增至本機檔案系統上的對應資料夾。</span><span class="sxs-lookup"><span data-stu-id="df68e-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="df68e-152">如果您的方案位於未對應的位置，系統會提示您在 TFS 和本機檔案系統中指定資料夾位置。</span><span class="sxs-lookup"><span data-stu-id="df68e-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="df68e-153">在 [**原始檔控制總管**] 索引標籤的 [**資料夾**] 窗格中，以滑鼠右鍵按一下 team 專案（例如， **ContactManager**），然後按一下 [**簽入暫**止的變更]。</span><span class="sxs-lookup"><span data-stu-id="df68e-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="df68e-154">在 [**簽入-來源**檔案] 對話方塊中，輸入批註，然後按一下 [**簽入**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="df68e-155">此時，您已將方案加入至 TFS 中的原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="df68e-156">將外部相依性加入至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="df68e-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="df68e-157">當您將專案或方案加入至原始檔控制時，您的專案或方案中的任何檔案和資料夾也會一併加入。</span><span class="sxs-lookup"><span data-stu-id="df68e-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="df68e-158">不過，在許多情況下，專案和方案也依賴外部相依性（例如本機組件），才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="df68e-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="df68e-159">您必須將任何這類資源加入至原始檔控制，讓開發人員小組的小組組建和其他成員都能順利建立您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="df68e-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="df68e-160">例如，Contact Manager 範例解決方案的資料夾結構包含名為 [套件] 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="df68e-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="df68e-161">其中包含 ADO.NET Entity Framework 4.1 的元件和各種支援資源。</span><span class="sxs-lookup"><span data-stu-id="df68e-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="df68e-162">[套件] 資料夾不是 Contact Manager 解決方案的一部分，但如果沒有，解決方案就不會成功地建立。</span><span class="sxs-lookup"><span data-stu-id="df68e-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="df68e-163">若要啟用 Team Build 來建立方案，您必須將 [封裝] 資料夾加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="df68e-164">包含封裝資料夾，通常是當您使用適用于 Visual Studio 2010 的 NuGet 擴充功能將 Entity Framework 或類似的資源新增至您的解決方案時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="df68e-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>

<span data-ttu-id="df68e-165">**若要將非專案內容加入至原始檔控制**</span><span class="sxs-lookup"><span data-stu-id="df68e-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="df68e-166">確定您想要新增的專案（例如封裝資料夾）位於本機檔案系統上對應資料夾內的適當位置。</span><span class="sxs-lookup"><span data-stu-id="df68e-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="df68e-167">在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，展開您的 Team 專案，然後按兩下 [**原始檔控制**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="df68e-168">在 [**原始檔控制總管**] 索引標籤的 [**資料夾**] 窗格中，選取包含您要新增之專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="df68e-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="df68e-169">按一下 [**將專案加入資料夾**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="df68e-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="df68e-170">在 [**加入至原始檔控制**] 對話方塊中，選取您要新增的資料夾，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="df68e-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="df68e-171">在 [**排除的專案**] 索引標籤上，選取已自動排除的任何必要專案（例如 [元件]），然後按一下 [**包含專案**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="df68e-172">在 [**要新增的專案**] 索引標籤上，確認已列出您要包含的所有檔案，然後按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="df68e-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="df68e-173">在 [**原始檔控制總管**] 視窗中，按一下 [**簽入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="df68e-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="df68e-174">在 [**簽入-來源**檔案] 對話方塊中，輸入批註，然後按一下 [**簽入**]。</span><span class="sxs-lookup"><span data-stu-id="df68e-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="df68e-175">此時，您已將方案的外部相依性加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="df68e-176">結論</span><span class="sxs-lookup"><span data-stu-id="df68e-176">Conclusion</span></span>

<span data-ttu-id="df68e-177">本主題說明如何連接至 team 專案、對應資料夾結構，以及將內容新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="df68e-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="df68e-178">如需如何在原始檔控制下使用專案的詳細資訊，請參閱[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。</span><span class="sxs-lookup"><span data-stu-id="df68e-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="df68e-179">下一個主題設定[Web 部署的 TFS 組建伺服器](configuring-a-tfs-build-server-for-web-deployment.md)，說明如何準備 TFS Team build server 以建立和部署您的方案。</span><span class="sxs-lookup"><span data-stu-id="df68e-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="df68e-180">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="df68e-180">Further Reading</span></span>

<span data-ttu-id="df68e-181">如需在 TFS 中使用原始檔控制的詳細資訊，請參閱[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。</span><span class="sxs-lookup"><span data-stu-id="df68e-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="df68e-182">[上一頁](creating-a-team-project-in-tfs.md)
> [下一頁](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="df68e-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
