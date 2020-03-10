---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 從部署中排除檔案和資料夾 |Microsoft Docs
author: jrjlee
description: 本主題說明當您建立和封裝 web 應用程式專案時，如何從 web 部署套件排除檔案和資料夾。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544972"
---
# <a name="excluding-files-and-folders-from-deployment"></a><span data-ttu-id="bbf2e-103">從部署中排除檔案與資料夾</span><span class="sxs-lookup"><span data-stu-id="bbf2e-103">Excluding Files and Folders from Deployment</span></span>

<span data-ttu-id="bbf2e-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="bbf2e-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="bbf2e-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="bbf2e-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="bbf2e-106">本主題說明當您建立和封裝 web 應用程式專案時，如何從 web 部署套件排除檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-106">This topic describes how you can exclude files and folders from a web deployment package when you build and package a web application project.</span></span>

<span data-ttu-id="bbf2e-107">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="bbf2e-108">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="bbf2e-109">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="overview"></a><span data-ttu-id="bbf2e-110">概觀</span><span class="sxs-lookup"><span data-stu-id="bbf2e-110">Overview</span></span>

<span data-ttu-id="bbf2e-111">當您在 Visual Studio 2010 中建立 web 應用程式專案時，Web 發佈管線（WPP）可讓您將已編譯的 web 應用程式封裝成可部署的 web 套件，藉此擴充此組建進程。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-111">When you build a web application project in Visual Studio 2010, the Web Publishing Pipeline (WPP) lets you extend this build process by packaging your compiled web application into a deployable web package.</span></span> <span data-ttu-id="bbf2e-112">接著，您可以使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）將此 web 封裝部署到遠端 IIS Web 服務器，或透過 IIS 管理員以手動方式匯入 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-112">You can then use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy this web package to a remote IIS web server, or import the web package manually through IIS Manager.</span></span> <span data-ttu-id="bbf2e-113">[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中會說明此封裝程式。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-113">This packaging process is explained in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="bbf2e-114">那麼，您要如何控制要包含在 web 套件中的內容呢？</span><span class="sxs-lookup"><span data-stu-id="bbf2e-114">So how do you control what gets included in your web package?</span></span> <span data-ttu-id="bbf2e-115">Visual Studio 中的專案設定，透過基礎專案檔，為許多案例提供足夠的控制。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-115">The project settings in Visual Studio, through the underlying project file, provide sufficient control for a lot of scenarios.</span></span> <span data-ttu-id="bbf2e-116">不過，在某些情況下，您可能會想要將 web 套件的內容量身打造到特定的目的地環境。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-116">However, in some cases you may want to tailor the contents of your web package to specific destination environments.</span></span> <span data-ttu-id="bbf2e-117">例如，當您將應用程式部署至測試環境時，可能會想要包含記錄檔的資料夾，但當您將應用程式部署至預備或生產環境時，會將資料夾排除。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-117">For example, you might want to include a folder for log files when you deploy your application to a test environment but exclude the folder when you deploy the application to a staging or production environment.</span></span> <span data-ttu-id="bbf2e-118">本主題將示範如何執行這種作法。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-118">This topic will show you how to do this.</span></span>

## <a name="what-gets-included-by-default"></a><span data-ttu-id="bbf2e-119">預設會包含哪些專案？</span><span class="sxs-lookup"><span data-stu-id="bbf2e-119">What Gets Included by Default?</span></span>

<span data-ttu-id="bbf2e-120">當您在 Visual Studio 中設定 web 應用程式專案屬性時，[**封裝/發行**] 網頁上的 [**要部署的專案**] 清單可讓您指定要包含在 web 部署套件中的內容。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-120">When you configure your web application project properties in Visual Studio, the **Items to deploy** list on the **Package/Publish Web** page lets you specify what you want to include in your web deployment package.</span></span> <span data-ttu-id="bbf2e-121">根據預設，這會設定為**只有執行此應用程式所需**的檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-121">By default, this is set to **Only files needed to run this application**.</span></span>

![](excluding-files-and-folders-from-deployment/_static/image1.png)

<span data-ttu-id="bbf2e-122">當您**只選擇執行此應用程式所需**的檔案時，WPP 會嘗試判斷哪些檔案應該加入至 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-122">When you choose **Only files needed to run this application**, the WPP will try to determine which files should be added to the web package.</span></span> <span data-ttu-id="bbf2e-123">包括：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-123">This includes:</span></span>

- <span data-ttu-id="bbf2e-124">專案的所有組建輸出。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-124">All the build outputs for the project.</span></span>
- <span data-ttu-id="bbf2e-125">任何以**內容**的組建動作標記的檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-125">Any files marked with a build action of **Content**.</span></span>

> [!NOTE]
> <span data-ttu-id="bbf2e-126">決定要包含哪些檔案的邏輯會包含在這個檔案中：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-126">The logic that determines which files to include is contained in this file:</span></span>   
> <span data-ttu-id="bbf2e-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ OnlyFilesToRunTheApp 的目標*</span><span class="sxs-lookup"><span data-stu-id="bbf2e-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span></span>

## <a name="excluding-specific-files-and-folders"></a><span data-ttu-id="bbf2e-128">排除特定的檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="bbf2e-128">Excluding Specific Files and Folders</span></span>

<span data-ttu-id="bbf2e-129">在某些情況下，您會想要更精細地控制要部署哪些檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-129">In some cases, you'll want more fine-grained control over which files and folders are deployed.</span></span> <span data-ttu-id="bbf2e-130">如果您知道要事先排除哪些檔案，而且排除適用于所有目的地環境，您只要將每個檔案的**組建動作**設定為 [**無**] 即可。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-130">If you know which files you want to exclude ahead of time, and the exclusion applies to all destination environments, you can simply set the **Build Action** of each file to **None**.</span></span>

<span data-ttu-id="bbf2e-131">**若要從部署中排除特定檔案**</span><span class="sxs-lookup"><span data-stu-id="bbf2e-131">**To exclude specific files from deployment**</span></span>

1. <span data-ttu-id="bbf2e-132">在 [**方案總管**] 視窗中，以滑鼠右鍵按一下該檔案，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-132">In the **Solution Explorer** window, right-click the file, and then click **Properties**.</span></span>
2. <span data-ttu-id="bbf2e-133">在 [**屬性**] 視窗的 [**組建動作**] 資料列中，選取 [**無**]。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-133">In the **Properties** window, in the **Build Action** row, select **None**.</span></span>

<span data-ttu-id="bbf2e-134">不過，這種方法並不一定方便。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-134">However, this approach is not always convenient.</span></span> <span data-ttu-id="bbf2e-135">例如，您可能會想要根據您的目的地環境以及外部 Visual Studio，來改變所包含的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-135">For example, you may want to vary which files and folders are included according to your destination environment, and from outside Visual Studio.</span></span> <span data-ttu-id="bbf2e-136">例如，在 Contact Manager 範例解決方案中，查看 ContactManager 專案的內容：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-136">For example, in the Contact Manager sample solution, take a look at the contents of the ContactManager.Mvc project:</span></span>

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- <span data-ttu-id="bbf2e-137">內部資料夾包含一些 SQL 腳本，供開發人員用來建立、卸載和填入本機資料庫以供開發之用。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-137">The Internal folder contains some SQL scripts that the developer uses to create, drop, and populate local databases for development purposes.</span></span> <span data-ttu-id="bbf2e-138">此資料夾中的任何內容都應該部署至預備或生產環境。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-138">Nothing in this folder should be deployed to a staging or production environment.</span></span>
- <span data-ttu-id="bbf2e-139">Scripts 資料夾包含數個 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-139">The Scripts folder contains several JavaScript files.</span></span> <span data-ttu-id="bbf2e-140">其中包含許多檔案，純粹是為了支援在 Visual Studio 中進行調試或提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-140">A lot of these files are included purely to support debugging or provide IntelliSense in Visual Studio.</span></span> <span data-ttu-id="bbf2e-141">這些檔案中的某些檔案不應部署至預備或生產環境。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-141">Some of these files should not be deployed to staging or production environments.</span></span> <span data-ttu-id="bbf2e-142">不過，您可能會想要將它們部署至開發人員測試環境，以協助進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-142">However, you may want to deploy them to a developer test environment to facilitate troubleshooting.</span></span>

<span data-ttu-id="bbf2e-143">雖然您可以操作專案檔來排除特定的檔案和資料夾，但還是有更簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-143">Although you could manipulate your project files to exclude specific files and folders, there is an easier way.</span></span> <span data-ttu-id="bbf2e-144">WPP 包含一個機制，藉由建立名為**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**的專案清單來排除檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-144">The WPP includes a mechanism to exclude files and folders by building item lists named **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles**.</span></span> <span data-ttu-id="bbf2e-145">您可以將自己的專案新增至這些清單，以擴充此機制。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-145">You can extend this mechanism by adding your own items to these lists.</span></span> <span data-ttu-id="bbf2e-146">若要這樣做，您需要完成下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-146">To do this, you need to complete these high-level steps:</span></span>

1. <span data-ttu-id="bbf2e-147">在與專案檔相同的資料夾中，建立名為 *[project name]* 的自訂專案檔。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-147">Create a custom project file named *[project name].wpp.targets* in the same folder as your project file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bbf2e-148">&#x2014;.Csproj &#x2014;.targets 檔案必須與您的 web 應用程式專案檔案位於相同的資料夾中，例如*ContactManager*，而不是與您用來控制組建和部署程式的任何自訂專案檔位於相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-148">The *.wpp.targets* file needs to go in the same folder as your web application project file&#x2014;for example, *ContactManager.Mvc.csproj*&#x2014;rather than in the same folder as any custom project files you use to control the build and deployment process.</span></span>
2. <span data-ttu-id="bbf2e-149">在 *.targets*檔案中，新增**ItemGroup**元素。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-149">In the *.wpp.targets* file, add an **ItemGroup** element.</span></span>
3. <span data-ttu-id="bbf2e-150">在**ItemGroup**元素中，新增**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**專案，以視需要排除特定的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-150">In the **ItemGroup** element, add **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles** items to exclude specific files and folders as required.</span></span>

<span data-ttu-id="bbf2e-151">這是這個*wpp .targets*檔案的基本結構：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-151">This is the basic structure of this *.wpp.targets* file:</span></span>

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

<span data-ttu-id="bbf2e-152">請注意，每個專案都包含名為**FromTarget**的專案中繼資料元素。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-152">Note that each item includes an item metadata element named **FromTarget**.</span></span> <span data-ttu-id="bbf2e-153">這是不會影響組建進程的選擇性值。它只是用來指出當有人審查組建記錄檔時，會省略特定檔案或資料夾的原因。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-153">This is an optional value that doesn't affect the build process; it simply serves to indicate why particular files or folders were omitted if someone reviews the build logs.</span></span>

## <a name="excluding-files-and-folders-from-a-web-package"></a><span data-ttu-id="bbf2e-154">從 Web 套件排除檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="bbf2e-154">Excluding Files and Folders from a Web Package</span></span>

<span data-ttu-id="bbf2e-155">下一個程式會示範如何將 *.targets*檔案加入至 web 應用程式專案，以及如何在建立專案時，使用檔案從 web 封裝中排除特定的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-155">The next procedure shows you how to add a *.wpp.targets* file to a web application project and how to use the file to exclude specific files and folders from the web package when you build your project.</span></span>

<span data-ttu-id="bbf2e-156">**從 web 部署套件排除檔案和資料夾**</span><span class="sxs-lookup"><span data-stu-id="bbf2e-156">**To exclude files and folders from a web deployment package**</span></span>

1. <span data-ttu-id="bbf2e-157">在 Visual Studio 2010 中開啟您的方案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-157">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="bbf2e-158">在 [**方案總管**] 視窗中，以滑鼠右鍵按一下您的 web 應用程式專案節點（例如**ContactManager**），指向 [**加入**]，然後按一下 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-158">In the **Solution Explorer** window, right-click your web application project node (for example, **ContactManager.Mvc**), point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="bbf2e-159">在 [**加入新專案**] 對話方塊中，選取 [ **XML**檔案] 範本。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-159">In the **Add New Item** dialog box, select the **XML File** template.</span></span>
4. <span data-ttu-id="bbf2e-160">在 [**名稱**] 方塊中，輸入 *[project Name] \* \* *. wpp. .targets** （例如， **ContactManager**），然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-160">In the **Name** box, type *[project name]\*\*\*.wpp.targets*\* (for example, **ContactManager.Mvc.wpp.targets**), and then click **Add**.</span></span>

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="bbf2e-161">如果您將新的專案加入至專案的根節點，該檔案會建立在與專案檔相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-161">If you add a new item to the root node of a project, the file is created in the same folder as the project file.</span></span> <span data-ttu-id="bbf2e-162">您可以在 Windows Explorer 中開啟資料夾來確認這一點。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-162">You can verify this by opening the folder in Windows Explorer.</span></span>
5. <span data-ttu-id="bbf2e-163">在檔案中，新增**專案**元素和**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-163">In the file, add a **Project** element and an **ItemGroup** element:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. <span data-ttu-id="bbf2e-164">如果您想要從 web 封裝排除資料夾，請將**ExcludeFromPackageFolders**元素新增至**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-164">If you want to exclude folders from the web package, add an **ExcludeFromPackageFolders** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="bbf2e-165">在 [**包含**] 屬性中，提供您要排除的檔案夾清單（以分號分隔）。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-165">In the **Include** attribute, provide a semicolon-separated list of the folders you want to exclude.</span></span>
   2. <span data-ttu-id="bbf2e-166">在**FromTarget**中繼資料專案中，提供有意義的值來指出排除資料夾的原因，*例如檔案名。*</span><span class="sxs-lookup"><span data-stu-id="bbf2e-166">In the **FromTarget** metadata element, provide a meaningful value to indicate why the folders are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. <span data-ttu-id="bbf2e-167">如果您想要從 web 封裝排除檔案，請將**ExcludeFromPackageFiles**元素新增至**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-167">If you want to exclude files from the web package, add an **ExcludeFromPackageFiles** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="bbf2e-168">在 [**包含**] 屬性中，提供您想要排除的檔案清單（以分號分隔）。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-168">In the **Include** attribute, provide a semicolon-separated list of the files you want to exclude.</span></span>
   2. <span data-ttu-id="bbf2e-169">在**FromTarget**中繼資料元素中，提供有意義的值來指出排除檔案的原因，*例如檔案名。*</span><span class="sxs-lookup"><span data-stu-id="bbf2e-169">In the **FromTarget** metadata element, provide a meaningful value to indicate why the files are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. <span data-ttu-id="bbf2e-170">*[Project name]. wpp .targets*檔案現在看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="bbf2e-170">The *[project name].wpp.targets* file should now resemble this:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. <span data-ttu-id="bbf2e-171">儲存並關閉 *[project name]. wpp .targets*檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-171">Save and close the *[project name].wpp.targets* file.</span></span>

<span data-ttu-id="bbf2e-172">下一次建立和封裝 web 應用程式專案時，WPP 會自動偵測 *.targets*檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-172">The next time you build and package your web application project, the WPP will automatically detect the *.wpp.targets* file.</span></span> <span data-ttu-id="bbf2e-173">您指定的任何檔案和資料夾都不會包含在 web 封裝中。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-173">Any files and folders you specified will not be included in the web package.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bbf2e-174">結論</span><span class="sxs-lookup"><span data-stu-id="bbf2e-174">Conclusion</span></span>

<span data-ttu-id="bbf2e-175">本主題說明如何在建立 web 套件時，排除特定的檔案和資料夾，方法是在與 web 應用程式專案檔相同的資料夾中建立自訂的 *. wpp .targets*檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-175">This topic described how to exclude specific files and folders when you build a web package, by creating a custom *.wpp.targets* file in the same folder as your web application project file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="bbf2e-176">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="bbf2e-176">Further Reading</span></span>

<span data-ttu-id="bbf2e-177">如需使用自訂 Microsoft Build Engine （MSBuild）專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-177">For more information on using custom Microsoft Build Engine (MSBuild) project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="bbf2e-178">如需封裝和部署程式的詳細資訊，請參閱[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)、設定[web 封裝部署的參數](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)和[部署 web 封裝](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf2e-178">For more information on the packaging and deployment process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Configuring Parameters for Web Package Deployment](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), and [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bbf2e-179">[上一頁](deploying-membership-databases-to-enterprise-environments.md)
> [下一頁](taking-web-applications-offline-with-web-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="bbf2e-179">[Previous](deploying-membership-databases-to-enterprise-environments.md)
[Next](taking-web-applications-offline-with-web-deploy.md)</span></span>
