---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 自動化所有作業（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: e741a753a36ebdaefbff8eee0b38911785c716ac
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457163"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="283a5-104">自動化所有作業（使用 Azure 建立真實世界的雲端應用程式）</span><span class="sxs-lookup"><span data-stu-id="283a5-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="283a5-105">由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="283a5-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="283a5-106">[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="283a5-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="283a5-107">**使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。</span><span class="sxs-lookup"><span data-stu-id="283a5-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="283a5-108">其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="283a5-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="283a5-109">如需電子書的簡介，請參閱[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="283a5-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="283a5-110">我們會查看的前三個模式實際上適用于任何軟體發展專案，但特別是雲端專案。</span><span class="sxs-lookup"><span data-stu-id="283a5-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="283a5-111">此模式是關於自動化開發工作。</span><span class="sxs-lookup"><span data-stu-id="283a5-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="283a5-112">這是很重要的主題，因為手動進程的速度很慢且容易出錯;盡可能自動化這些功能，有助於設定快速、可靠且敏捷的工作流程。</span><span class="sxs-lookup"><span data-stu-id="283a5-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="283a5-113">這對雲端開發而言是唯一重要的，因為您可以輕鬆地自動化許多難以或無法在內部部署環境中自動執行的工作。</span><span class="sxs-lookup"><span data-stu-id="283a5-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="283a5-114">例如，您可以設定整個測試環境，包括新的 web 伺服器和後端 Vm、資料庫、blob 儲存體（檔案儲存體）、佇列等。</span><span class="sxs-lookup"><span data-stu-id="283a5-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="283a5-115">DevOps 工作流程</span><span class="sxs-lookup"><span data-stu-id="283a5-115">DevOps Workflow</span></span>

<span data-ttu-id="283a5-116">越來越多您聽過「DevOps」一詞。</span><span class="sxs-lookup"><span data-stu-id="283a5-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="283a5-117">本詞彙的開發目的是要整合開發和操作工作，以便有效率地開發軟體。</span><span class="sxs-lookup"><span data-stu-id="283a5-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="283a5-118">您想要啟用的工作流程類型是您可以開發應用程式、加以部署、從生產環境使用方式學習、變更它以回應您所學的內容，以及快速且可靠地重複此週期。</span><span class="sxs-lookup"><span data-stu-id="283a5-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="283a5-119">某些成功的雲端開發小組會一天多次部署到即時環境。</span><span class="sxs-lookup"><span data-stu-id="283a5-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="283a5-120">每隔2-3 個月就會用來部署主要更新的 Azure 團隊，但現在它會每隔2-3 天發行次要更新，並每隔2-3 周釋放一次主要版本。</span><span class="sxs-lookup"><span data-stu-id="283a5-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="283a5-121">進入該步調可説明您回應客戶的意見反應。</span><span class="sxs-lookup"><span data-stu-id="283a5-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="283a5-122">若要這麼做，您必須啟用可重複、可靠且可預測的開發和部署週期，並提供低週期時間。</span><span class="sxs-lookup"><span data-stu-id="283a5-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps 工作流程](automate-everything/_static/image1.png)

<span data-ttu-id="283a5-124">換句話說，您對於某項功能的想法，以及客戶使用它和提供意見反應的時間，都必須盡可能縮短。</span><span class="sxs-lookup"><span data-stu-id="283a5-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="283a5-125">前三個模式-自動化所有專案、原始檔控制、持續整合和傳遞--都是我們建議的最佳作法，以便啟用這種程式。</span><span class="sxs-lookup"><span data-stu-id="283a5-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="283a5-126">Azure 管理腳本</span><span class="sxs-lookup"><span data-stu-id="283a5-126">Azure management scripts</span></span>

<span data-ttu-id="283a5-127">在[這篇電子書的簡介](introduction.md)中，您看到了 Azure 管理入口網站的網頁型主控台。</span><span class="sxs-lookup"><span data-stu-id="283a5-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="283a5-128">管理入口網站可讓您監視及管理您已在 Azure 上部署的所有資源。</span><span class="sxs-lookup"><span data-stu-id="283a5-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="283a5-129">這是建立和刪除服務的簡單方式，例如 web 應用程式和 Vm、設定這些服務、監視服務作業等等。</span><span class="sxs-lookup"><span data-stu-id="283a5-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="283a5-130">這是很棒的工具，但使用它是手動程式。</span><span class="sxs-lookup"><span data-stu-id="283a5-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="283a5-131">如果您要開發任何規模的實際執行應用程式，尤其是在小組環境中，建議您流覽入口網站 UI，以瞭解並探索 Azure，然後將重複執行的進程自動化。</span><span class="sxs-lookup"><span data-stu-id="283a5-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="283a5-132">您幾乎可以在管理入口網站或 Visual Studio 中手動執行的所有作業，也可以藉由呼叫 REST 管理 API 來完成。</span><span class="sxs-lookup"><span data-stu-id="283a5-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="283a5-133">您可以使用[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)撰寫腳本，也可以使用開放原始碼架構，例如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)。</span><span class="sxs-lookup"><span data-stu-id="283a5-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="283a5-134">您也可以在 Mac 或 Linux 環境中使用 Bash 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="283a5-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="283a5-135">Azure 有適用于所有這些不同環境的腳本 Api，如果您想要撰寫程式碼而不是腳本，它會有[.net 管理 api](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="283a5-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="283a5-136">針對 Fix It 應用程式，我們建立了一些 Windows PowerShell 腳本，將建立測試環境的程式自動化，並將專案部署到該環境，我們將會回顧這些腳本的一些內容。</span><span class="sxs-lookup"><span data-stu-id="283a5-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="283a5-137">環境建立腳本</span><span class="sxs-lookup"><span data-stu-id="283a5-137">Environment creation script</span></span>

<span data-ttu-id="283a5-138">我們要探討的第一個腳本是名為*New-AzureWebsiteEnv*。</span><span class="sxs-lookup"><span data-stu-id="283a5-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="283a5-139">它會建立 Azure 環境，讓您可以將 Fix It 應用程式部署至進行測試。</span><span class="sxs-lookup"><span data-stu-id="283a5-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="283a5-140">此腳本執行的主要工作如下：</span><span class="sxs-lookup"><span data-stu-id="283a5-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="283a5-141">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="283a5-141">Create a web app.</span></span>
- <span data-ttu-id="283a5-142">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="283a5-142">Create a storage account.</span></span> <span data-ttu-id="283a5-143">（Blob 和佇列的必要項，如您在稍後的章節中所見）。</span><span class="sxs-lookup"><span data-stu-id="283a5-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="283a5-144">建立 SQL Database 伺服器和兩個資料庫：應用程式資料庫和成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="283a5-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="283a5-145">在 Azure 中儲存應用程式將用來存取儲存體帳戶和資料庫的設定。</span><span class="sxs-lookup"><span data-stu-id="283a5-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="283a5-146">建立將用於自動化部署的設定檔。</span><span class="sxs-lookup"><span data-stu-id="283a5-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="283a5-147">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="283a5-147">Run the script</span></span>

> [!NOTE]
> <span data-ttu-id="283a5-148">本章的這個部分會顯示腳本的範例，以及您輸入以執行它們的命令。</span><span class="sxs-lookup"><span data-stu-id="283a5-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="283a5-149">這是示範，並不提供執行腳本所需知道的一切。</span><span class="sxs-lookup"><span data-stu-id="283a5-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="283a5-150">如需逐步執行的作法指示，請參閱[附錄：修正 It 範例應用程式](the-fix-it-sample-application.md#deploybase)。</span><span class="sxs-lookup"><span data-stu-id="283a5-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>

<span data-ttu-id="283a5-151">若要執行 PowerShell 腳本來管理 Azure 服務，您必須安裝 Azure PowerShell 主控台，並將其設定為與您的 Azure 訂用帳戶搭配運作。</span><span class="sxs-lookup"><span data-stu-id="283a5-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="283a5-152">設定好之後，您可以使用如下的命令來執行修正 It 環境建立腳本：</span><span class="sxs-lookup"><span data-stu-id="283a5-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="283a5-153">`Name` 參數會指定建立資料庫和儲存體帳戶時所要使用的名稱，而 `SqlDatabasePassword` 參數會指定將針對 SQL Database 所建立之系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="283a5-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="283a5-154">您可以使用其他參數，我們將在稍後討論。</span><span class="sxs-lookup"><span data-stu-id="283a5-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell 視窗](automate-everything/_static/image2.png)

<span data-ttu-id="283a5-156">腳本完成之後，您可以在管理入口網站中看到所建立的內容。</span><span class="sxs-lookup"><span data-stu-id="283a5-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="283a5-157">您會發現兩個資料庫：</span><span class="sxs-lookup"><span data-stu-id="283a5-157">You'll find two databases:</span></span>

![資料庫](automate-everything/_static/image3.png)

<span data-ttu-id="283a5-159">儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="283a5-159">A storage account:</span></span>

![儲存體帳戶](automate-everything/_static/image4.png)

<span data-ttu-id="283a5-161">和 web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="283a5-161">And a web app:</span></span>

![網站](automate-everything/_static/image5.png)

<span data-ttu-id="283a5-163">在 web 應用程式的 [**設定**] 索引標籤上，您可以看到它已為 [修正 it] 應用程式設定 [儲存體帳戶設定] 和 [SQL database 連接字串]。</span><span class="sxs-lookup"><span data-stu-id="283a5-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![appSettings 和 connectionStrings](automate-everything/_static/image6.png)

<span data-ttu-id="283a5-165">[*自動化*] 資料夾現在也包含一個 *&lt;websitename&gt;. .pubxml*檔案。</span><span class="sxs-lookup"><span data-stu-id="283a5-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="283a5-166">這個檔案會儲存 MSBuild 將用來將應用程式部署至剛建立之 Azure 環境的設定。</span><span class="sxs-lookup"><span data-stu-id="283a5-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="283a5-167">例如：</span><span class="sxs-lookup"><span data-stu-id="283a5-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="283a5-168">如您所見，腳本已建立一個完整的測試環境，而整個程式在大約90秒內完成。</span><span class="sxs-lookup"><span data-stu-id="283a5-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="283a5-169">如果您小組中的其他人想要建立測試環境，他們只要執行腳本就可以了。</span><span class="sxs-lookup"><span data-stu-id="283a5-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="283a5-170">不僅快速，而且也可以確信他們使用的環境與您所使用的環境完全相同。</span><span class="sxs-lookup"><span data-stu-id="283a5-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="283a5-171">如果每個人都是使用入口網站 UI 來手動設定專案，您就無法放心。</span><span class="sxs-lookup"><span data-stu-id="283a5-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="283a5-172">查看腳本</span><span class="sxs-lookup"><span data-stu-id="283a5-172">A look at the scripts</span></span>

<span data-ttu-id="283a5-173">實際上，有三個腳本可執行此工作。</span><span class="sxs-lookup"><span data-stu-id="283a5-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="283a5-174">您可以從命令列呼叫一個，它會自動使用其他兩個來執行一些工作：</span><span class="sxs-lookup"><span data-stu-id="283a5-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="283a5-175">*New-AzureWebSiteEnv*是主要的腳本。</span><span class="sxs-lookup"><span data-stu-id="283a5-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="283a5-176">*New-AzureStorage*會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="283a5-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="283a5-177">*New-AzureSql*會建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="283a5-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="283a5-178">主要腳本中的參數</span><span class="sxs-lookup"><span data-stu-id="283a5-178">Parameters in the main script</span></span>

<span data-ttu-id="283a5-179">主要腳本*New-AzureWebSiteEnv*會定義數個參數：</span><span class="sxs-lookup"><span data-stu-id="283a5-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="283a5-180">需要兩個參數：</span><span class="sxs-lookup"><span data-stu-id="283a5-180">Two parameters are required:</span></span>

- <span data-ttu-id="283a5-181">腳本建立的 web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="283a5-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="283a5-182">（這也用於 URL： `<name>.azurewebsites.net`）。</span><span class="sxs-lookup"><span data-stu-id="283a5-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="283a5-183">腳本所建立之資料庫伺服器的新系統管理使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="283a5-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="283a5-184">選擇性參數可讓您指定資料中心位置（預設為「美國西部」）、資料庫伺服器管理員名稱（預設為 "dbuser"），以及資料庫伺服器的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="283a5-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="283a5-185">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="283a5-185">Create the web app</span></span>

<span data-ttu-id="283a5-186">腳本的第一件事是藉由呼叫 `New-AzureWebsite` Cmdlet 來建立 web 應用程式，並將 web 應用程式名稱和位置參數值傳入其中：</span><span class="sxs-lookup"><span data-stu-id="283a5-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="283a5-187">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="283a5-187">Create the storage account</span></span>

<span data-ttu-id="283a5-188">然後，主要腳本會執行*New-AzureStorage*腳本，並針對儲存體帳戶名稱指定 " *&lt;websitename&gt;* storage"，並為 web 應用程式指定相同的資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="283a5-188">Then the main script runs the *New-AzureStorage.ps1* script, specifying "*&lt;websitename&gt;* storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="283a5-189">*New-AzureStorage*會呼叫 `New-AzureStorageAccount` Cmdlet 來建立儲存體帳戶，並傳回帳戶名稱和存取金鑰值。</span><span class="sxs-lookup"><span data-stu-id="283a5-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="283a5-190">應用程式將需要這些值，才能存取儲存體帳戶中的 blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="283a5-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="283a5-191">您可能不一定會想要建立新的儲存體帳戶;您可以藉由新增可選擇性地指示其使用現有儲存體帳戶的參數，來增強腳本。</span><span class="sxs-lookup"><span data-stu-id="283a5-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="283a5-192">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="283a5-192">Create the databases</span></span>

<span data-ttu-id="283a5-193">然後，主要腳本會在設定預設資料庫和防火牆規則名稱之後，執行資料庫建立腳本*New-AzureSql*：</span><span class="sxs-lookup"><span data-stu-id="283a5-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="283a5-194">資料庫建立腳本會抓取開發電腦的 IP 位址，並設定防火牆規則，讓開發電腦能夠連接及管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="283a5-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="283a5-195">接著，資料庫建立腳本會經歷數個步驟來設定資料庫：</span><span class="sxs-lookup"><span data-stu-id="283a5-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="283a5-196">使用 `New-AzureSqlDatabaseServer` Cmdlet 建立伺服器。</span><span class="sxs-lookup"><span data-stu-id="283a5-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="283a5-197">建立防火牆規則，讓開發電腦能夠管理伺服器，以及讓 web 應用程式連線到它。</span><span class="sxs-lookup"><span data-stu-id="283a5-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="283a5-198">使用 `New-AzureSqlDatabaseServerContext` Cmdlet，建立包含伺服器名稱和認證的資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="283a5-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    <span data-ttu-id="283a5-199">`New-PSCredentialFromPlainText` 是腳本中的函式，會呼叫 `ConvertTo-SecureString` Cmdlet 來加密密碼，並傳回 `PSCredential` 物件，這與 `Get-Credential` Cmdlet 所傳回的類型相同。</span><span class="sxs-lookup"><span data-stu-id="283a5-199">`New-PSCredentialFromPlainText` is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="283a5-200">使用 `New-AzureSqlDatabase` Cmdlet，建立應用程式資料庫和成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="283a5-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="283a5-201">呼叫本機定義的函數，以建立每個資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="283a5-201">Calls a locally defined function to create a connection string for each database.</span></span> <span data-ttu-id="283a5-202">應用程式會使用這些連接字串來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="283a5-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="283a5-203">SQLAzureDatabaseConnectionString 是腳本中定義的函式，它會從提供給它的參數值建立連接字串。</span><span class="sxs-lookup"><span data-stu-id="283a5-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="283a5-204">傳回具有資料庫伺服器名稱和連接字串的雜湊表。</span><span class="sxs-lookup"><span data-stu-id="283a5-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="283a5-205">修正 It 應用程式會使用不同的成員資格和應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="283a5-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="283a5-206">您也可以將成員資格和應用程式資料都放在單一資料庫中。</span><span class="sxs-lookup"><span data-stu-id="283a5-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="283a5-207">儲存應用程式設定和連接字串</span><span class="sxs-lookup"><span data-stu-id="283a5-207">Store app settings and connection strings</span></span>

<span data-ttu-id="283a5-208">Azure 有一項功能，可讓您儲存設定和連接字串，以在嘗試讀取 Web.config 檔案中的 `appSettings` 或 `connectionStrings` 集合時，自動覆寫傳回給應用程式的內容。</span><span class="sxs-lookup"><span data-stu-id="283a5-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="283a5-209">當您部署時，這是套用[web.config 轉換](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)的替代方法。</span><span class="sxs-lookup"><span data-stu-id="283a5-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="283a5-210">如需詳細資訊，請參閱本電子書後面的[將敏感性資料儲存在 Azure](source-control.md#appsettings)中。</span><span class="sxs-lookup"><span data-stu-id="283a5-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="283a5-211">環境建立腳本會將應用程式在 Azure 中執行時所需的所有 `appSettings` 和 `connectionStrings` 值儲存在 Azure 中，以存取儲存體帳戶和資料庫。</span><span class="sxs-lookup"><span data-stu-id="283a5-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="283a5-212">[新的 new relic](http://newrelic.com/)是我們在[監視和遙測](monitoring-and-telemetry.md)一章中示範的遙測架構。</span><span class="sxs-lookup"><span data-stu-id="283a5-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="283a5-213">環境建立腳本也會重新開機 web 應用程式，以確保它會挑選新的 New relic 設定。</span><span class="sxs-lookup"><span data-stu-id="283a5-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="283a5-214">準備部署</span><span class="sxs-lookup"><span data-stu-id="283a5-214">Preparing for deployment</span></span>

<span data-ttu-id="283a5-215">在程式結束時，環境建立腳本會呼叫兩個函數來建立部署腳本將使用的檔案。</span><span class="sxs-lookup"><span data-stu-id="283a5-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="283a5-216">其中一個函式會建立發行設定檔 *（&lt;websitename&gt;. .pubxml*檔案）。</span><span class="sxs-lookup"><span data-stu-id="283a5-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="283a5-217">程式碼會呼叫 Azure REST API 來取得發行設定，並將資訊儲存在 *.publishsettings*檔案中。</span><span class="sxs-lookup"><span data-stu-id="283a5-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="283a5-218">然後，它會使用該檔案中的資訊以及範本檔案（ *.pubxml*）來建立包含發行設定檔的 *.pubxml*檔案。</span><span class="sxs-lookup"><span data-stu-id="283a5-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="283a5-219">這個兩步驟的程式會模擬您在 Visual Studio 中執行的作業：下載 *.publishsettings*檔案，並匯入以建立發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="283a5-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="283a5-220">另一個函式會使用另一個範本檔案（網站-環境範本）來建立*website-environment*檔案，其中包含部署腳本將與 *.pubxml*檔案搭配使用的設定。</span><span class="sxs-lookup"><span data-stu-id="283a5-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="283a5-221">疑難排解和錯誤處理</span><span class="sxs-lookup"><span data-stu-id="283a5-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="283a5-222">腳本就像程式一樣：它們可能會失敗，而且當您想要知道失敗的最大程度和造成問題的原因時。</span><span class="sxs-lookup"><span data-stu-id="283a5-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="283a5-223">基於這個理由，環境建立腳本會將 `VerbosePreference` 變數的值從 `SilentlyContinue` 變更為 `Continue`，以便顯示所有詳細資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="283a5-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="283a5-224">它也會將 `ErrorActionPreference` 變數的值從 `Continue` 變更為 `Stop`，讓腳本即使在遇到非終止錯誤時也會停止：</span><span class="sxs-lookup"><span data-stu-id="283a5-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="283a5-225">在執行任何工作之前，腳本會儲存開始時間，讓它能夠計算完成的已耗用時間：</span><span class="sxs-lookup"><span data-stu-id="283a5-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="283a5-226">完成工作之後，腳本會顯示經過時間：</span><span class="sxs-lookup"><span data-stu-id="283a5-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="283a5-227">針對每個金鑰作業，腳本會寫入詳細資訊訊息，例如：</span><span class="sxs-lookup"><span data-stu-id="283a5-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="283a5-228">部署指令碼</span><span class="sxs-lookup"><span data-stu-id="283a5-228">Deployment script</span></span>

<span data-ttu-id="283a5-229">*New-AzureWebsiteEnv*腳本在建立環境時所執行的工作， *Publish-AzureWebsite*腳本會進行應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="283a5-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="283a5-230">部署腳本會從環境建立腳本所建立的*website-environment*中，取得 web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="283a5-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="283a5-231">它會從 *.publishsettings*檔案取得部署使用者密碼：</span><span class="sxs-lookup"><span data-stu-id="283a5-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="283a5-232">它會執行[MSBuild](http://msbuildbook.com/)命令來建立及部署專案：</span><span class="sxs-lookup"><span data-stu-id="283a5-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="283a5-233">如果您已在命令列上指定 `Launch` 參數，它會呼叫 `Show-AzureWebsite` Cmdlet，將您的預設瀏覽器開啟至網站 URL。</span><span class="sxs-lookup"><span data-stu-id="283a5-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="283a5-234">您可以使用如下的命令來執行部署腳本：</span><span class="sxs-lookup"><span data-stu-id="283a5-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="283a5-235">完成後，瀏覽器會開啟，並在 `<websitename>.azurewebsites.net` URL 的雲端中執行網站。</span><span class="sxs-lookup"><span data-stu-id="283a5-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![修正部署至 Windows Azure 的 It 應用程式](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="283a5-237">摘要</span><span class="sxs-lookup"><span data-stu-id="283a5-237">Summary</span></span>

<span data-ttu-id="283a5-238">使用這些腳本，您可以確信相同的步驟一律會使用相同的循序執行相同的訂單。</span><span class="sxs-lookup"><span data-stu-id="283a5-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="283a5-239">這有助於確保小組中的每位開發人員都不會錯過任何東西，或在自己的電腦上部署自訂專案，而在另一個小組成員的環境或實際執行時，實際上無法以相同的方式運作。</span><span class="sxs-lookup"><span data-stu-id="283a5-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="283a5-240">同樣地，您可以使用 REST API、Windows PowerShell 腳本、.NET 語言 API 或可在 Linux 或 Mac 上執行的 Bash 公用程式，將您可以在管理入口網站中執行的大部分 Azure 管理功能自動化。</span><span class="sxs-lookup"><span data-stu-id="283a5-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="283a5-241">在[下一章](source-control.md)中，我們將探討原始程式碼，並說明在原始程式碼存放庫中包含腳本是很重要的。</span><span class="sxs-lookup"><span data-stu-id="283a5-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="283a5-242">資源</span><span class="sxs-lookup"><span data-stu-id="283a5-242">Resources</span></span>

- <span data-ttu-id="283a5-243">[安裝和設定適用于 Azure 的 Windows PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="283a5-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="283a5-244">說明如何安裝 Azure PowerShell Cmdlet，以及如何在您的電腦上安裝所需的憑證，以便管理您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="283a5-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="283a5-245">這是開始使用的絕佳位置，因為它也有可供學習 PowerShell 本身的資源連結。</span><span class="sxs-lookup"><span data-stu-id="283a5-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="283a5-246">[Azure 腳本中心](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。</span><span class="sxs-lookup"><span data-stu-id="283a5-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="283a5-247">WindowsAzure.com 入口網站來開發可管理 Azure 服務的腳本，並提供入門教學課程的連結、Cmdlet 參考檔和原始程式碼，以及範例腳本</span><span class="sxs-lookup"><span data-stu-id="283a5-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="283a5-248">[週末腳本：使用 Azure 和 PowerShell 消費者入門](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)。</span><span class="sxs-lookup"><span data-stu-id="283a5-248">[Weekend Scripter: Getting Started with Azure and PowerShell](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="283a5-249">在 Windows PowerShell 專用的 blog 中，這篇文章提供了使用 PowerShell 來進行 Azure 管理功能的絕佳簡介。</span><span class="sxs-lookup"><span data-stu-id="283a5-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="283a5-250">[安裝和設定 Azure 跨平臺命令列介面](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。</span><span class="sxs-lookup"><span data-stu-id="283a5-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="283a5-251">適用于 Mac 和 Linux 以及 Windows 系統的 Azure 腳本架構快速入門教學課程。</span><span class="sxs-lookup"><span data-stu-id="283a5-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="283a5-252">[命令列工具區段：下載 Azure sdk 和工具主題](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="283a5-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="283a5-253">適用于 Azure 命令列工具相關檔和下載的入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="283a5-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="283a5-254">[使用 Azure 管理庫和 .NET 將一切自動化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。</span><span class="sxs-lookup"><span data-stu-id="283a5-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="283a5-255">Scott Hanselman 引進了適用于 Azure 的 .NET 管理 API。</span><span class="sxs-lookup"><span data-stu-id="283a5-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="283a5-256">[使用 Windows PowerShell 指令碼來發行至開發和測試環境](https://msdn.microsoft.com/library/azure/dn642480.aspx)。</span><span class="sxs-lookup"><span data-stu-id="283a5-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="283a5-257">說明如何使用 Visual Studio 自動為 Web 專案產生之發佈腳本的 MSDN 檔。</span><span class="sxs-lookup"><span data-stu-id="283a5-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="283a5-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。</span><span class="sxs-lookup"><span data-stu-id="283a5-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="283a5-259">Visual Studio 延伸模組，可在 Visual Studio 中新增 Windows PowerShell 的語言支援。</span><span class="sxs-lookup"><span data-stu-id="283a5-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="283a5-260">[上一頁](introduction.md)
> [下一頁](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="283a5-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>
