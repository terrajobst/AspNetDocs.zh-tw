---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 原始檔控制（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 5a1e0d7cd3c396d4be79c8958422602055eb3db1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457098"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="d4ba5-104">原始檔控制（使用 Azure 建立真實世界的雲端應用程式）</span><span class="sxs-lookup"><span data-stu-id="d4ba5-104">Source Control (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="d4ba5-105">由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d4ba5-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="d4ba5-106">[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="d4ba5-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="d4ba5-107">**使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="d4ba5-108">其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="d4ba5-109">如需電子書的相關資訊，請參閱[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="d4ba5-110">原始檔控制對於所有雲端開發專案都是不可或缺的，而不只是小組環境。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-110">Source control is essential for all cloud development projects, not just team environments.</span></span> <span data-ttu-id="d4ba5-111">您不想要在沒有復原功能和自動備份的情況下編輯原始程式碼或甚至是 Word 檔，而原始檔控制會在專案層級提供這些函式，以便在發生錯誤時更多時間儲存。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-111">You wouldn't think of editing source code or even a Word document without an undo function and automatic backups, and source control gives you those functions at a project level where they can save even more time when something goes wrong.</span></span> <span data-ttu-id="d4ba5-112">使用雲端原始檔控制服務時，您不再需要擔心複雜的設定，而且您可以免費使用 Azure Repos 的原始檔控制，最多5位使用者。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-112">With cloud source control services, you no longer have to worry about complicated set-up, and you can use Azure Repos source control free for up to 5 users.</span></span>

<span data-ttu-id="d4ba5-113">本章的第一個部分將說明要牢記在心的三個重要最佳作法：</span><span class="sxs-lookup"><span data-stu-id="d4ba5-113">The first part of this chapter explains three key best practices to keep in mind:</span></span>

- <span data-ttu-id="d4ba5-114">將[自動化腳本視為原始程式碼](#scripts)，並將它們與您的應用程式程式碼搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-114">[Treat automation scripts as source code](#scripts) and version them together with your application code.</span></span>
- <span data-ttu-id="d4ba5-115">[請勿將秘密（機密](#secrets)資料，例如認證）簽入原始程式碼存放庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-115">[Never check in secrets](#secrets) (sensitive data such as credentials) into a source code repository.</span></span>
- <span data-ttu-id="d4ba5-116">[設定來源分支](#devops)以啟用 DevOps 工作流程。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-116">[Set up source branches](#devops) to enable the DevOps workflow.</span></span>

<span data-ttu-id="d4ba5-117">本章的其餘部分會在 Visual Studio、Azure 和 Azure Repos 中提供這些模式的一些範例執行：</span><span class="sxs-lookup"><span data-stu-id="d4ba5-117">The remainder of the chapter gives some sample implementations of these patterns in Visual Studio, Azure, and Azure Repos:</span></span>

- [<span data-ttu-id="d4ba5-118">在 Visual Studio 中將腳本加入至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="d4ba5-118">Add scripts to source control in Visual Studio</span></span>](#vsscripts)
- [<span data-ttu-id="d4ba5-119">將敏感性資料儲存在 Azure 中</span><span class="sxs-lookup"><span data-stu-id="d4ba5-119">Store sensitive data in Azure</span></span>](#appsettings)
- [<span data-ttu-id="d4ba5-120">在 Visual Studio 和 Azure Repos 中使用 Git</span><span class="sxs-lookup"><span data-stu-id="d4ba5-120">Use Git in Visual Studio and Azure Repos</span></span>](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a><span data-ttu-id="d4ba5-121">將自動化腳本視為原始程式碼</span><span class="sxs-lookup"><span data-stu-id="d4ba5-121">Treat automation scripts as source code</span></span>

<span data-ttu-id="d4ba5-122">當您正在處理雲端專案時，您會經常變更，而且您想要能夠快速地回應客戶所回報的問題。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-122">When you're working on a cloud project you're changing things frequently and you want to be able to react quickly to issues reported by your customers.</span></span> <span data-ttu-id="d4ba5-123">快速回應包括使用自動化腳本，如[自動化所有事項](automate-everything.md)一章所述。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-123">Responding quickly involves using automation scripts, as explained in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="d4ba5-124">您用來建立環境、加以部署、調整規模等等的所有腳本，都必須與您的應用程式原始程式碼同步。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-124">All of the scripts that you use to create your environment, deploy to it, scale it, etc., need to be in sync with your application source code.</span></span>

<span data-ttu-id="d4ba5-125">若要讓腳本與程式碼保持同步，請將其儲存在您的原始檔控制系統中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-125">To keep scripts in sync with code, store them in your source control system.</span></span> <span data-ttu-id="d4ba5-126">然後，如果您需要復原變更，或快速修正與開發程式碼不同的實際執行程式碼，則不必浪費時間嘗試追蹤哪些設定已變更，或是哪些小組成員有您需要的版本複本。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-126">Then if you ever need to roll back changes or make a quick fix to production code which is different from development code, you don't have to waste time trying to track down which settings have changed or which team members have copies of the version you need.</span></span> <span data-ttu-id="d4ba5-127">您可以確定所需的腳本與您所需的程式碼基底同步，而且您可以確保所有小組成員都使用相同的腳本。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-127">You're assured that the scripts you need are in sync with the code base that you need them for, and you're assured that all team members are working with the same scripts.</span></span> <span data-ttu-id="d4ba5-128">然後，不論您是否需要將熱修正的測試和部署作業自動化至生產環境或新功能開發，您都可以使用正確的腳本來處理需要更新的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-128">Then whether you need to automate testing and deployment of a hot fix to production or new feature development, you'll have the right script for the code that needs to be updated.</span></span>

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a><span data-ttu-id="d4ba5-129">不簽入秘密</span><span class="sxs-lookup"><span data-stu-id="d4ba5-129">Don't check in secrets</span></span>

<span data-ttu-id="d4ba5-130">原始碼存放庫通常可供太多人存取，以確保機密資料（例如密碼）有適當的安全位置。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-130">A source code repository is typically accessible to too many people for it to be an appropriately secure place for sensitive data such as passwords.</span></span> <span data-ttu-id="d4ba5-131">如果腳本依賴秘密（例如密碼），請將這些設定參數化，讓它們不會儲存在原始程式碼中，並將您的密碼儲存在其他地方。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-131">If scripts rely on secrets such as passwords, parameterize those settings so that they don't get saved in source code, and store your secrets somewhere else.</span></span>

<span data-ttu-id="d4ba5-132">例如，Azure 可讓您下載包含發行設定的檔案，以便自動建立發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-132">For example, Azure lets you download files that contain publish settings in order to automate the creation of publish profiles.</span></span> <span data-ttu-id="d4ba5-133">這些檔案包括已獲授權可管理 Azure 服務的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-133">These files include user names and passwords that are authorized to manage your Azure services.</span></span> <span data-ttu-id="d4ba5-134">如果您使用此方法來建立發行設定檔，而且將這些檔案簽入原始檔控制，任何可存取您存放庫的人都可以看到那些使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-134">If you use this method to create publish profiles, and if you check in these files to source control, anyone with access to your repository can see those user names and passwords.</span></span> <span data-ttu-id="d4ba5-135">您可以安全地將密碼儲存在發行設定檔本身，因為它已加密，而且它是在預設不包含在原始檔控制中的 *.pubxml*檔案中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-135">You can safely store the password in the publish profile itself because it's encrypted and it's in a *.pubxml.user* file that by default is not included in source control.</span></span>

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a><span data-ttu-id="d4ba5-136">結構來源分支以加速 DevOps 工作流程</span><span class="sxs-lookup"><span data-stu-id="d4ba5-136">Structure source branches to facilitate DevOps workflow</span></span>

<span data-ttu-id="d4ba5-137">您在存放庫中執行分支的方式，會影響您在生產環境中開發新功能和修正問題的能力。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-137">How you implement branches in your repository affects your ability to both develop new features and fix issues in production.</span></span> <span data-ttu-id="d4ba5-138">以下是許多中型小組使用的模式：</span><span class="sxs-lookup"><span data-stu-id="d4ba5-138">Here is a pattern that a lot of medium sized teams use:</span></span>

![來源分支結構](source-control/_static/image1.png)

<span data-ttu-id="d4ba5-140">主要分支一律會符合生產環境中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-140">The master branch always matches code that is in production.</span></span> <span data-ttu-id="d4ba5-141">Master 底下的分支對應到開發生命週期中的不同階段。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-141">Branches underneath master correspond to different stages in the development life cycle.</span></span> <span data-ttu-id="d4ba5-142">開發分支是您可在其中執行新功能的位置。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-142">The development branch is where you implement new features.</span></span> <span data-ttu-id="d4ba5-143">對於小型小組，您可能只是主要和開發，但我們通常建議使用者在開發與主伺服器之間擁有預備分支。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-143">For a small team you might just have master and development, but we often recommend that people have a staging branch between development and master.</span></span> <span data-ttu-id="d4ba5-144">您可以使用預備來進行最終的整合測試，再將更新移至生產環境。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-144">You can use staging for final integration testing before an update is moved to production.</span></span>

<span data-ttu-id="d4ba5-145">對於大型團隊而言，每項新功能可能會有個別的分支;對於較小的小組，您可能會有每個人簽入開發分支。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-145">For big teams there may be separate branches for each new feature; for a smaller team you might have everyone checking in to the development branch.</span></span>

<span data-ttu-id="d4ba5-146">如果您有每個功能的分支，當功能 A 準備好時，您可以將其原始程式碼變更合併到開發分支，再將其移至其他功能分支。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-146">If you have a branch for each feature, when Feature A is ready you merge its source code changes up into the development branch and down into the other feature branches.</span></span> <span data-ttu-id="d4ba5-147">此原始程式碼合併程式可能非常耗時，若要避免該工作，同時仍保持功能的不同，某些小組會執行稱為 *[功能切換](http://en.wikipedia.org/wiki/Feature_toggle)* 的替代方法（也稱為*功能旗標*）。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-147">This source code merging process can be time-consuming, and to avoid that work while still keeping features separate, some teams implement an alternative called *[feature toggles](http://en.wikipedia.org/wiki/Feature_toggle)* (also known as *feature flags*).</span></span> <span data-ttu-id="d4ba5-148">這表示所有功能的所有程式碼都位於相同的分支中，但是您可以使用程式碼中的參數來啟用或停用每項功能。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-148">This means all of the code for all of the features is in the same branch, but you enable or disable each feature by using switches in the code.</span></span> <span data-ttu-id="d4ba5-149">例如，假設「功能 A」是用來修正 It 應用程式工作的新欄位，而「功能 B」則新增快取功能。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-149">For example, suppose Feature A is a new field for Fix It app tasks, and Feature B adds caching functionality.</span></span> <span data-ttu-id="d4ba5-150">這兩個功能的程式碼可以在開發分支中，但只有當變數設定為 true 時，應用程式才會顯示新的欄位，而且當不同的變數設定為 true 時，它只會使用快取。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-150">The code for both features can be in the development branch, but the app will only display the new field when a variable is set to true, and it will only use caching when a different variable is set to true.</span></span> <span data-ttu-id="d4ba5-151">如果功能 A 尚未準備好升級，但功能 B 已準備就緒，您可以將所有的程式碼升級至生產環境，並將功能切換為關閉，並開啟功能 B 開關。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-151">If Feature A isn't ready to be promoted but the Feature B is ready, you can promote all of the code to Production with the Feature A switch off and the Feature B switch on.</span></span> <span data-ttu-id="d4ba5-152">接著，您可以完成功能 A 並于稍後升級，而不需要合併原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-152">You can then finish Feature A and promote it later, all with no source code merging.</span></span>

<span data-ttu-id="d4ba5-153">不論您是使用分支還是切換功能，這類分支結構都可讓您以敏捷且可重複的方式，將您的程式碼從開發流到生產環境。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-153">Whether or not you use branches or toggles for features, a branching structure like this enables you to flow your code from development into production in an agile and repeatable way.</span></span>

<span data-ttu-id="d4ba5-154">此結構也可讓您快速回應客戶的意見反應。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-154">This structure also enables you to react quickly to customer feedback.</span></span> <span data-ttu-id="d4ba5-155">如果您需要快速修正生產環境，您也可以透過敏捷的方式有效率地進行。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-155">If you need to make a quick fix to production, you can also do that efficiently in an agile way.</span></span> <span data-ttu-id="d4ba5-156">您可以從主要或預備環境建立分支，並在它準備好將它合併到主伺服器和功能分支中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-156">You can create a branch off of master or staging, and when it's ready merge it up into master and down into development and feature branches.</span></span>

![修補程式分支](source-control/_static/image2.png)

<span data-ttu-id="d4ba5-158">如果沒有像這樣的分支結構，並將其與生產和開發分支分開，則生產環境問題可能會讓您進入必須升級新功能程式碼的位置，以及您的生產環境修正。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-158">Without a branching structure like this with its separation of production and development branches, a production problem could put you in the position of having to promote new feature code along with your production fix.</span></span> <span data-ttu-id="d4ba5-159">新的功能程式碼可能尚未經過完整測試，且可供生產環境使用，您可能需要執行許多工作，以備份尚未準備好的變更。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-159">The new feature code might not be fully tested and ready for production and you might have to do a lot of work backing out changes that aren't ready.</span></span> <span data-ttu-id="d4ba5-160">或者，您可能必須延遲修正程式，才能測試變更並準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-160">Or you might have to delay your fix in order to test changes and get them ready to deploy.</span></span>

<span data-ttu-id="d4ba5-161">接下來，您會看到如何在 Visual Studio、Azure 和 Azure Repos 中執行這三種模式的範例。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-161">Next you'll see examples of how to implement these three patterns in Visual Studio, Azure, and Azure Repos.</span></span> <span data-ttu-id="d4ba5-162">這些是範例，而不是詳細的逐步操作方法指示;如需提供所有必要內容的詳細指示，請參閱本章結尾的[Resources （資源](#resources)）一節。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-162">These are examples rather than detailed step-by-step how-to-do-it instructions; for detailed instructions that provide all of the context necessary, see the [Resources](#resources) section at the end of the chapter.</span></span>

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a><span data-ttu-id="d4ba5-163">在 Visual Studio 中將腳本加入至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="d4ba5-163">Add scripts to source control in Visual Studio</span></span>

<span data-ttu-id="d4ba5-164">在 Visual Studio 中，您可以將腳本加入至原始檔控制中，方法是將它們包含在 Visual Studio 方案資料夾中（假設您的專案是在原始檔控制中）。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-164">You can add scripts to source control in Visual Studio by including them in a Visual Studio solution folder (assuming your project is in source control).</span></span> <span data-ttu-id="d4ba5-165">以下是其中一種方法。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-165">Here's one way to do it.</span></span>

<span data-ttu-id="d4ba5-166">為方案資料夾中的腳本建立資料夾（具有 *.sln*檔案的相同資料夾）。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-166">Create a folder for the scripts in your solution folder (the same folder that has your *.sln* file).</span></span>

![自動化資料夾](source-control/_static/image3.png)

<span data-ttu-id="d4ba5-168">將腳本檔案複製到資料夾中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-168">Copy the script files into the folder.</span></span>

![自動化資料夾內容](source-control/_static/image4.png)

<span data-ttu-id="d4ba5-170">在 Visual Studio 中，將 [方案] 資料夾新增至專案。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-170">In Visual Studio, add a solution folder to the project.</span></span>

![新增方案資料夾功能表選取專案](source-control/_static/image5.png)

<span data-ttu-id="d4ba5-172">並將腳本檔案加入至 [方案] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-172">And add the script files to the solution folder.</span></span>

![[加入現有專案] 功能表選取範圍](source-control/_static/image6.png)

![加入現有項目對話方塊](source-control/_static/image7.png)

<span data-ttu-id="d4ba5-175">腳本檔案現在已包含在您的專案中，而原始檔控制會追蹤其版本變更以及對應的原始程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-175">The script files are now included in your project and source control is tracking their version changes along with corresponding source code changes.</span></span>

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a><span data-ttu-id="d4ba5-176">將敏感性資料儲存在 Azure 中</span><span class="sxs-lookup"><span data-stu-id="d4ba5-176">Store sensitive data in Azure</span></span>

<span data-ttu-id="d4ba5-177">如果您在 Azure 網站中執行應用程式，其中一個避免將認證儲存在原始檔控制中的方法，就是將其儲存在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-177">If you run your application in an Azure Web Site, one way to avoid storing credentials in source control is to store them in Azure instead.</span></span>

<span data-ttu-id="d4ba5-178">例如，Fix It 應用程式會在其 Web.config 檔案中儲存兩個將在生產環境中具有密碼的連接字串，以及一個可存取您 Azure 儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-178">For example, the Fix It application stores in its Web.config file two connection strings that will have passwords in production and a key that gives access to your Azure storage account.</span></span>

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

<span data-ttu-id="d4ba5-179">如果您將這些設定的實際生產值放在*web.config 檔案*中，或將它們放在*web.config*檔案中以設定 web.config 轉換，以便在部署期間將其插入，它們將會儲存在來源存放庫中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-179">If you put actual production values for these settings in your *Web.config* file, or if you put them in the *Web.Release.config* file to configure a Web.config transform to insert them during deployment, they'll be stored in the source repository.</span></span> <span data-ttu-id="d4ba5-180">如果您在生產發行設定檔中輸入資料庫連接字串，密碼將會在您的 *.pubxml*檔案中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-180">If you enter the database connection strings into the production publish profile, the password will be in your *.pubxml* file.</span></span> <span data-ttu-id="d4ba5-181">（您可以將 *.pubxml*檔案從原始檔控制中排除，但這樣會失去共用所有其他部署設定的優點）。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-181">(You could exclude the *.pubxml* file from source control, but then you lose the benefit of sharing all the other deployment settings.)</span></span>

<span data-ttu-id="d4ba5-182">Azure 為您*提供 web.config 檔案*中**appSettings**和連接字串區段的替代方案。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-182">Azure gives you an alternative for the **appSettings** and connection strings sections of the *Web.config* file.</span></span> <span data-ttu-id="d4ba5-183">以下是 Azure 入口網站中網站的 [**設定] 索引標籤的相關**部分：</span><span class="sxs-lookup"><span data-stu-id="d4ba5-183">Here is the relevant part of the **Configuration** tab for a web site in the Azure management portal:</span></span>

![入口網站中的 appSettings 和 connectionStrings](source-control/_static/image8.png)

<span data-ttu-id="d4ba5-185">當您將專案部署到這個網站並執行應用程式時，任何您儲存在 Azure 中的值都會覆寫 Web.config 檔案中的任何值。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-185">When you deploy a project to this web site and the application runs, whatever values you have stored in Azure override whatever values are in the Web.config file.</span></span>

<span data-ttu-id="d4ba5-186">您可以使用管理入口網站或腳本，在 Azure 中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-186">You can set these values in Azure by using either the management portal or scripts.</span></span> <span data-ttu-id="d4ba5-187">您在[自動化所有事項](automate-everything.md)一章中看到的環境建立自動化腳本會建立一個 Azure SQL Database、取得儲存體並 SQL Database 連接字串，並將這些秘密儲存在您的網站設定中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-187">The environment creation automation script you saw in the [Automate Everything](automate-everything.md) chapter creates an Azure SQL Database, gets the storage and SQL Database connection strings, and stores these secrets in the settings for your web site.</span></span>

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

<span data-ttu-id="d4ba5-188">請注意，腳本已參數化，因此實際值不會保存至來源存放庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-188">Notice that the scripts are parameterized so that actual values don't get persisted to the source repository.</span></span>

<span data-ttu-id="d4ba5-189">當您在開發環境中于本機執行時，應用程式會讀取您的本機 Web.config 檔案，而您的連接字串會指向 Web 專案之*應用程式\_Data*資料夾中的 LocalDB SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-189">When you run locally in your development environment, the app reads your local Web.config file and your connection string points to a LocalDB SQL Server database in the *App\_Data* folder of your web project.</span></span> <span data-ttu-id="d4ba5-190">當您在 Azure 中執行應用程式，且應用程式嘗試從 Web.config 檔案讀取這些值時，它所傳回的內容是儲存在網站上的值，而不是在 web.config 檔案中實際的值。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-190">When you run the app in Azure and the app tries to read these values from the Web.config file, what it gets back and uses are the values stored for the Web Site, not what's actually in Web.config file.</span></span>

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a><span data-ttu-id="d4ba5-191">在 Visual Studio 和 Azure DevOps 中使用 Git</span><span class="sxs-lookup"><span data-stu-id="d4ba5-191">Use Git in Visual Studio and Azure DevOps</span></span>

<span data-ttu-id="d4ba5-192">您可以使用任何原始檔控制環境來執行稍早所提供的 DevOps 分支結構。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-192">You can use any source control environment to implement the DevOps branching structure presented earlier.</span></span> <span data-ttu-id="d4ba5-193">對於分散式小組而言，[分散式版本控制系統](http://en.wikipedia.org/wiki/Distributed_revision_control)（DVCS）可能會有最佳效果;對於其他小組而言，[集中式系統](http://en.wikipedia.org/wiki/Revision_control)可能更有效果。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-193">For distributed teams a [distributed version control system](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS) might work best; for other teams a [centralized system](http://en.wikipedia.org/wiki/Revision_control) might work better.</span></span>

<span data-ttu-id="d4ba5-194">[Git](http://git-scm.com/)是受歡迎的分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-194">[Git](http://git-scm.com/) is a popular distributed version control system.</span></span> <span data-ttu-id="d4ba5-195">當您使用 Git 進行原始檔控制時，您可以在本機電腦上擁有完整的存放庫複本及其所有歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-195">When you use Git for source control, you have a complete copy of the repository with all of its history on your local computer.</span></span> <span data-ttu-id="d4ba5-196">許多人偏好這麼做，因為當您未連線到網路時，可以更輕鬆地繼續工作--您可以繼續執行認可和復原、建立和切換分支等等。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-196">Many people prefer that because it's easier to continue working when you're not connected to the network -- you can continue to do commits and rollbacks, create and switch branches, and so forth.</span></span> <span data-ttu-id="d4ba5-197">即使您已連線到網路，當所有專案都在本機時，建立分支和切換分支會變得更容易且更快速。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-197">Even when you're connected to the network, it's easier and quicker to create branches and switch branches when everything is local.</span></span> <span data-ttu-id="d4ba5-198">您也可以執行本機認可和回復，而不會影響其他開發人員。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-198">You can also do local commits and rollbacks without having an impact on other developers.</span></span> <span data-ttu-id="d4ba5-199">而且您可以先批次處理認可，再將它們傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-199">And you can batch commits before sending them to the server.</span></span>

<span data-ttu-id="d4ba5-200">[Azure Repos](/azure/devops/repos/index?view=vsts)提供[Git](/azure/devops/repos/git/?view=vsts)和[Team Foundation 版本控制](/azure/devops/repos/tfvc/index?view=vsts)（TFVC; 集中式原始檔控制）。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-200">[Azure Repos](/azure/devops/repos/index?view=vsts) offers both [Git](/azure/devops/repos/git/?view=vsts) and [Team Foundation Version Control](/azure/devops/repos/tfvc/index?view=vsts) (TFVC; centralized source control).</span></span> <span data-ttu-id="d4ba5-201">從[這裡](https://app.vsaex.visualstudio.com/signup)開始使用 Azure DevOps。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-201">Get started with Azure DevOps [here](https://app.vsaex.visualstudio.com/signup).</span></span>

<span data-ttu-id="d4ba5-202">Visual Studio 2017 包含內建的第一級[Git 支援](https://msdn.microsoft.com/library/hh850437.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-202">Visual Studio 2017 includes built-in, first-class [Git support](https://msdn.microsoft.com/library/hh850437.aspx).</span></span> <span data-ttu-id="d4ba5-203">以下是其運作方式的快速示範。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-203">Here's a quick demo of how that works.</span></span>

<span data-ttu-id="d4ba5-204">在 Visual Studio 中開啟專案時，以滑鼠右鍵按一下**方案總管**中的方案，然後選擇 [**將方案加入至原始檔控制**]。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-204">With a project open in Visual Studio, right-click the solution in **Solution Explorer**, and then choose **Add Solution to Source Control**.</span></span>

![將方案加入至原始檔控制](source-control/_static/image9.png)

<span data-ttu-id="d4ba5-206">Visual Studio 詢問您是否要使用 TFVC （集中式版本控制）或 Git。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-206">Visual Studio asks if you want to use TFVC (centralized version control) or Git.</span></span>

![選擇原始檔控制](source-control/_static/image10.png)

<span data-ttu-id="d4ba5-208">當您選取 [Git]，然後按一下 **[確定]** 時，Visual Studio 會在方案資料夾中建立新的本機 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-208">When you select Git and click **OK**, Visual Studio creates a new local Git repository in your solution folder.</span></span> <span data-ttu-id="d4ba5-209">新的存放庫尚未提供任何檔案;您必須執行 Git 認可，將它們新增至存放庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-209">The new repository has no files yet; you have to add them to the repository by doing a Git commit.</span></span> <span data-ttu-id="d4ba5-210">以滑鼠右鍵按一下**方案總管**中的方案，然後按一下 [**認可**]。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-210">Right-click the solution in **Solution Explorer**, and then click **Commit**.</span></span>

![Commit](source-control/_static/image11.png)

<span data-ttu-id="d4ba5-212">Visual Studio 會自動為認可的所有專案檔案設置階段，並在 [**包含的變更**] 窗格的**Team Explorer**中列出它們。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-212">Visual Studio automatically stages all of the project files for the commit and lists them in **Team Explorer** in the **Included Changes** pane.</span></span> <span data-ttu-id="d4ba5-213">（如果有一些您不想要包含在認可中，您可以選取它們、按一下滑鼠右鍵，然後按一下 [**排除**]）。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-213">(If there were some you didn't want to include in the commit, you could select them, right-click, and click **Exclude**.)</span></span>

![Team Explorer](source-control/_static/image12.png)

<span data-ttu-id="d4ba5-215">輸入認可批註，然後按一下 [**認可**]，Visual Studio 執行認可並顯示認可識別碼。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-215">Enter a commit comment and click **Commit**, and Visual Studio executes the commit and displays the commit ID.</span></span>

![Team Explorer 變更](source-control/_static/image13.png)

<span data-ttu-id="d4ba5-217">現在，如果您變更一些程式碼，使其與存放庫中的不同，您可以輕鬆地查看差異。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-217">Now if you change some code so that it's different from what's in the repository, you can easily view the differences.</span></span> <span data-ttu-id="d4ba5-218">以滑鼠右鍵按一下您已變更的檔案，選取 [**與未修改的比較**]，然後取得顯示未認可變更的比較顯示。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-218">Right-click a file that you've changed, select **Compare with Unmodified**, and you get a comparison display that shows your uncommitted change.</span></span>

![與未修改的比較](source-control/_static/image14.png)

![差異顯示變更](source-control/_static/image15.png)

<span data-ttu-id="d4ba5-221">您可以輕鬆地查看您所做的變更，並將其簽入。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-221">You can easily see what changes you're making and check them in.</span></span>

<span data-ttu-id="d4ba5-222">假設您需要建立分支–您也可以在 Visual Studio 中這麼做。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-222">Suppose you need to make a branch – you can do that in Visual Studio too.</span></span> <span data-ttu-id="d4ba5-223">在**Team Explorer**中，按一下 [**新增分支**]。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-223">In **Team Explorer**, click **New Branch**.</span></span>

![Team Explorer 新增分支](source-control/_static/image16.png)

<span data-ttu-id="d4ba5-225">輸入分支名稱、按一下 [**建立分支**]，如果您選取 [**簽出分支**]，Visual Studio 會自動簽出新的分支。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-225">Enter a branch name, click **Create Branch**, and if you selected **Checkout branch**, Visual Studio automatically checks out the new branch.</span></span>

![Team Explorer 新增分支](source-control/_static/image17.png)

<span data-ttu-id="d4ba5-227">您現在可以對檔案進行變更，並將其簽入此分支。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-227">You can now make changes to files and check them in to this branch.</span></span> <span data-ttu-id="d4ba5-228">而且您可以輕鬆地在分支之間切換，Visual Studio 會自動將檔案同步處理至您已簽出的任何分支。在此範例中， *\_Layout*中的網頁標題已變更為 HotFix1 分支中的「熱修復1」。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-228">And you can easily switch between branches and Visual Studio automatically syncs the files to whichever branch you have checked out. In this example the web page title in *\_Layout.cshtml* has been changed to "Hot Fix 1" in HotFix1 branch.</span></span>

![Hotfix1 分支](source-control/_static/image18.png)

<span data-ttu-id="d4ba5-230">如果您切換回主要分支， *\_Layout*檔案的內容會自動還原成主要分支中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-230">If you switch back to the master branch, the contents of the *\_Layout.cshtml* file automatically revert to what they are in the master branch.</span></span>

![主要分支](source-control/_static/image19.png)

<span data-ttu-id="d4ba5-232">這是一個簡單的範例，說明如何快速建立分支並在分支之間來回切換。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-232">This a simple example of how you can quickly create a branch and flip back and forth between branches.</span></span> <span data-ttu-id="d4ba5-233">這項功能可讓您使用 [[自動化所有專案](automate-everything.md)] 一章中所提供的分支結構和自動化腳本，來進行高度 agile 工作流程。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-233">This feature enables a highly agile workflow using the branch structure and automation scripts presented in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="d4ba5-234">例如，您可以在開發分支中工作、從 master 建立熱修復分支、切換到新分支、在該處進行變更並加以認可，然後切換回開發分支並繼續進行。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-234">For example, you can be working in the Development branch, create a hot fix branch off of master, switch to the new branch, make your changes there and commit them, and then switch back to the Development branch and continue what you were doing.</span></span>

<span data-ttu-id="d4ba5-235">您在這裡看到的是如何在 Visual Studio 中使用本機 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-235">What you've seen here is how you work with a local Git repository in Visual Studio.</span></span> <span data-ttu-id="d4ba5-236">在小組環境中，您通常也會將變更推送到通用存放庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-236">In a team environment you typically also push changes up to a common repository.</span></span> <span data-ttu-id="d4ba5-237">Visual Studio 工具也可讓您指向遠端 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-237">The Visual Studio tools also enable you to point to a remote Git repository.</span></span> <span data-ttu-id="d4ba5-238">您可以針對該目的使用 GitHub.com，也可以使用[Git 和 Azure Repos](/azure/devops/repos/git/overview?view=vsts)與所有其他 Azure DevOps 功能整合，例如工作專案和 bug 追蹤。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-238">You can use GitHub.com for that purpose, or you can use [Git and Azure Repos](/azure/devops/repos/git/overview?view=vsts) integrated with all the other Azure DevOps capabilities such as work item and bug tracking.</span></span>

<span data-ttu-id="d4ba5-239">當然，這並不是您可以實現 agile 分支策略的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-239">This isn't the only way you can implement an agile branching strategy, of course.</span></span> <span data-ttu-id="d4ba5-240">您可以使用集中式原始檔控制存放庫來啟用相同的 agile 工作流程。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-240">You can enable the same agile workflow using a centralized source control repository.</span></span>

## <a name="summary"></a><span data-ttu-id="d4ba5-241">摘要</span><span class="sxs-lookup"><span data-stu-id="d4ba5-241">Summary</span></span>

<span data-ttu-id="d4ba5-242">根據您可進行變更的速度，並以安全且可預測的方式，測量您的原始檔控制系統是否成功。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-242">Measure the success of your source control system based on how quickly you can make a change and get it live in a safe and predictable way.</span></span> <span data-ttu-id="d4ba5-243">如果您發現自己的害怕進行變更，因為您必須對其進行一天或兩次的手動測試，您可能會問自己，您必須採取何種方式進行處理或測試，讓您可以在幾分鐘內進行變更，或在最差時間不到一小時。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-243">If you find yourself scared to make a change because you have to do a day or two of manual testing on it, you might ask yourself what you have to do process-wise or test-wise so that you can make that change in minutes or at worst no longer than an hour.</span></span> <span data-ttu-id="d4ba5-244">執行這項作業的其中一個策略是執行持續整合和持續傳遞，我們將在[下一章](continuous-integration-and-continuous-delivery.md)中討論。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-244">One strategy for doing that is to implement continuous integration and continuous delivery, which we'll cover in the [next chapter](continuous-integration-and-continuous-delivery.md).</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="d4ba5-245">資源</span><span class="sxs-lookup"><span data-stu-id="d4ba5-245">Resources</span></span>

<span data-ttu-id="d4ba5-246">如需分支策略的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="d4ba5-246">For more information about branching strategies, see the following resources:</span></span>

- <span data-ttu-id="d4ba5-247">[使用 Team Foundation Server 2012 建立發行管線](https://msdn.microsoft.com/library/dn449957.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-247">[Building a Release Pipeline with Team Foundation Server 2012](https://msdn.microsoft.com/library/dn449957.aspx).</span></span> <span data-ttu-id="d4ba5-248">Microsoft 模式和實務檔。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-248">Microsoft Patterns and Practices documentation.</span></span> <span data-ttu-id="d4ba5-249">如需分支策略的討論，請參閱第6章。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-249">See chapter 6 for a discussion of branching strategies.</span></span> <span data-ttu-id="d4ba5-250">提倡者功能會切換功能分支，如果使用功能分支，則會讓它們保持短期（最多數小時或數天）。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-250">Advocates feature toggles over feature branches, and if branches for features are used, advocates keeping them short-lived (hours or days at most).</span></span>
- <span data-ttu-id="d4ba5-251">[版本控制指南](https://aka.ms/vsarsolutions)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-251">[Version Control Guide](https://aka.ms/vsarsolutions).</span></span> <span data-ttu-id="d4ba5-252">ALM Ranger 的分支策略指南。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-252">Guide to branching strategies by the ALM Rangers.</span></span> <span data-ttu-id="d4ba5-253">請參閱 [下載] 索引標籤上的分支策略 .pdf。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-253">See Branching Strategies.pdf on the Downloads tab.</span></span>
- <span data-ttu-id="d4ba5-254">[使用功能切換進行軟體發展](https://msdn.microsoft.com/magazine/dn683796.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-254">[Software Development with Feature Toggles](https://msdn.microsoft.com/magazine/dn683796.aspx).</span></span> <span data-ttu-id="d4ba5-255">MSDN 雜誌文章。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-255">MSDN Magazine article.</span></span>
- <span data-ttu-id="d4ba5-256">[功能切換](http://martinfowler.com/bliki/FeatureToggle.html)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-256">[Feature Toggle](http://martinfowler.com/bliki/FeatureToggle.html).</span></span> <span data-ttu-id="d4ba5-257">在聖馬丁 Fowler 的 blog 上的功能切換/功能旗標簡介。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-257">Introduction to feature toggles / feature flags on Martin Fowler's blog.</span></span>
- <span data-ttu-id="d4ba5-258">[功能會切換 Vs 功能分支](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-258">[Feature Toggles vs Feature Branches](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx).</span></span> <span data-ttu-id="d4ba5-259">另一個關於功能切換的 blog 文章 Dylan Smith。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-259">Another blog post about feature toggles, by Dylan Smith.</span></span>

<span data-ttu-id="d4ba5-260">如需如何處理不應保留在原始檔控制存放庫中之機密資訊的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="d4ba5-260">For more information about how to handle sensitive information that should not be kept in source control repositories, see the following resources:</span></span>

- <span data-ttu-id="d4ba5-261">[將密碼和其他機密資料部署至 ASP.NET 和 Azure App Service 的最佳作法](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-261">[Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
- <span data-ttu-id="d4ba5-262">[Azure 網站：應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-262">[Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="d4ba5-263">說明會覆寫*web.config*檔案中 `appSettings` 和 `connectionStrings` 資料的 Azure 功能。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-263">Explains the Azure feature that overrides `appSettings` and `connectionStrings` data in the *Web.config* file.</span></span>
- <span data-ttu-id="d4ba5-264">[Azure 網站中的自訂設定和應用程式設定-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-264">[Custom configuration and application settings in Azure Web Sites - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/).</span></span>

<span data-ttu-id="d4ba5-265">如需其他將機密資訊保留在原始檔控制之外之方法的詳細資訊，請參閱[ASP.NET MVC：將私用設定保留在原始](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)檔控制中。</span><span class="sxs-lookup"><span data-stu-id="d4ba5-265">For information about other methods for keeping sensitive information out of source control, see [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d4ba5-266">[上一頁](automate-everything.md)
> [下一頁](continuous-integration-and-continuous-delivery.md)</span><span class="sxs-lookup"><span data-stu-id="d4ba5-266">[Previous](automate-everything.md)
[Next](continuous-integration-and-continuous-delivery.md)</span></span>
