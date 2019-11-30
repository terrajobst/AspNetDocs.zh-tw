---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 使用 Visual Studio ASP.NET Web 部署：部署額外的檔案 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594899"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="f7dce-103">使用 Visual Studio ASP.NET Web 部署：部署額外的檔案</span><span class="sxs-lookup"><span data-stu-id="f7dce-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>

<span data-ttu-id="f7dce-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f7dce-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f7dce-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="f7dce-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="f7dce-106">本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="f7dce-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="f7dce-107">如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="f7dce-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="f7dce-108">概觀</span><span class="sxs-lookup"><span data-stu-id="f7dce-108">Overview</span></span>

<span data-ttu-id="f7dce-109">本教學課程示範如何擴充 Visual Studio web 發佈管線，以在部署期間執行其他工作。</span><span class="sxs-lookup"><span data-stu-id="f7dce-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="f7dce-110">工作是將不在專案資料夾中的額外檔案複製到目的地網站。</span><span class="sxs-lookup"><span data-stu-id="f7dce-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="f7dce-111">在本教學課程中，您將複製一個額外的檔案： [*機器人 .txt*]。</span><span class="sxs-lookup"><span data-stu-id="f7dce-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="f7dce-112">您想要將此檔案部署至預備環境，而不是實際執行。</span><span class="sxs-lookup"><span data-stu-id="f7dce-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="f7dce-113">在[部署至生產](deploying-to-production.md)教學課程中，您已將此檔案新增至專案，並已設定生產發行設定檔將其排除。</span><span class="sxs-lookup"><span data-stu-id="f7dce-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="f7dce-114">在本教學課程中，您將會看到處理這種情況的替代方法，其中一種方式適用于您想要部署但不想包含在專案中的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="f7dce-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="f7dce-115">移動機器人 .txt 檔案</span><span class="sxs-lookup"><span data-stu-id="f7dce-115">Move the robots.txt file</span></span>

<span data-ttu-id="f7dce-116">若要準備其他處理*機器人*的方法，請在本教學課程的這一節中，將檔案移至未包含在專案中的資料夾，並從預備環境中刪除的 [*機器人]。*</span><span class="sxs-lookup"><span data-stu-id="f7dce-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="f7dce-117">您必須從預備環境中刪除檔案，如此一來，您就可以確認將檔案部署至該環境的新方法是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="f7dce-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="f7dce-118">在**方案總管**中，以滑鼠右鍵按一下 [*機器人 .txt* ] 檔案，然後按一下 [**從專案排除**]。</span><span class="sxs-lookup"><span data-stu-id="f7dce-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="f7dce-119">使用 Windows 檔案瀏覽器，在方案資料夾中建立新資料夾，並將其命名為*ExtraFiles*。</span><span class="sxs-lookup"><span data-stu-id="f7dce-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="f7dce-120">將*ContosoUniversity*專案資料夾中的*機器人 .txt*檔案移至*ExtraFiles*資料夾。</span><span class="sxs-lookup"><span data-stu-id="f7dce-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![ExtraFiles 資料夾](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="f7dce-122">使用您的 FTP 工具，從預備網站刪除*機器人 .txt*檔案。</span><span class="sxs-lookup"><span data-stu-id="f7dce-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="f7dce-123">或者，您可以在預備發行設定檔的 [**設定**] 索引標籤上，選取 [檔案**發佈選項**] 下的 [**移除目的地的其他**檔案]，然後重新發佈至預備環境。</span><span class="sxs-lookup"><span data-stu-id="f7dce-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="f7dce-124">更新發行設定檔</span><span class="sxs-lookup"><span data-stu-id="f7dce-124">Update the publish profile file</span></span>

<span data-ttu-id="f7dce-125">在預備環境中，您只需要有*機器人 .txt* ，因此，您需要更新才能部署的發行設定檔是預備環境。</span><span class="sxs-lookup"><span data-stu-id="f7dce-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="f7dce-126">在 Visual Studio 中，開啟 *.pubxml*。</span><span class="sxs-lookup"><span data-stu-id="f7dce-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="f7dce-127">在檔案結尾的結束 `</Project>` 標記之前，新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="f7dce-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="f7dce-128">此程式碼會建立新的*目標*，以收集要部署的其他檔案。</span><span class="sxs-lookup"><span data-stu-id="f7dce-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="f7dce-129">目標是由一或多個工作所組成，MSBuild 將根據您指定的條件來執行。</span><span class="sxs-lookup"><span data-stu-id="f7dce-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="f7dce-130">`Include` 屬性指定要在其中尋找檔案的資料夾是*ExtraFiles*，位於與專案資料夾相同的層級。</span><span class="sxs-lookup"><span data-stu-id="f7dce-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="f7dce-131">MSBuild 會收集該資料夾中的所有檔案，並從任何子資料夾以遞迴方式進行（雙星號指定遞迴子資料夾）。</span><span class="sxs-lookup"><span data-stu-id="f7dce-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="f7dce-132">使用此程式碼，您可以將多個檔案和檔案放在*ExtraFiles*資料夾內的子資料夾中，而全部都將會部署。</span><span class="sxs-lookup"><span data-stu-id="f7dce-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="f7dce-133">`DestinationRelativePath` 專案指定應將資料夾和檔案複製到目的地網站的根資料夾，其檔案和資料夾結構與在*ExtraFiles*資料夾中找到的相同。</span><span class="sxs-lookup"><span data-stu-id="f7dce-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="f7dce-134">如果您想要複製*ExtraFiles*資料夾本身，`DestinationRelativePath` 值會是*ExtraFiles\%（RecursiveDir）% （Filename）% （Extension）* 。</span><span class="sxs-lookup"><span data-stu-id="f7dce-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="f7dce-135">在檔案結尾的結尾 `</Project>` 標記之前，新增下列標記以指定執行新目標的時機。</span><span class="sxs-lookup"><span data-stu-id="f7dce-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="f7dce-136">此程式碼會在執行將檔案複製到目的地資料夾的目標時，執行新的 `CustomCollectFiles` 目標。</span><span class="sxs-lookup"><span data-stu-id="f7dce-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="f7dce-137">發行與部署套件建立有一個不同的目標，如果您決定使用部署套件（而不是發佈）來部署，新的目標就會插入兩個目標。</span><span class="sxs-lookup"><span data-stu-id="f7dce-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="f7dce-138">*.Pubxml*檔案現在看起來如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f7dce-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="f7dce-139">儲存並關閉 *.pubxml*檔案。</span><span class="sxs-lookup"><span data-stu-id="f7dce-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="f7dce-140">發行至預備環境</span><span class="sxs-lookup"><span data-stu-id="f7dce-140">Publish to staging</span></span>

<span data-ttu-id="f7dce-141">使用單鍵發佈或命令列，使用暫存設定檔發行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7dce-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="f7dce-142">如果您使用單鍵發佈，您可以在**預覽**視窗中確認將會複製*機器人 .txt* 。</span><span class="sxs-lookup"><span data-stu-id="f7dce-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="f7dce-143">否則，請使用您的 FTP 工具來確認在部署之後，會在網站的根資料夾中執行*機器人 .txt*檔案。</span><span class="sxs-lookup"><span data-stu-id="f7dce-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="f7dce-144">總結</span><span class="sxs-lookup"><span data-stu-id="f7dce-144">Summary</span></span>

<span data-ttu-id="f7dce-145">這會完成這一系列的教學課程，將 ASP.NET web 應用程式部署到協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="f7dce-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="f7dce-146">如需這些教學課程中所涵蓋之任何主題的詳細資訊，請參閱[ASP.NET 部署內容對應](https://go.microsoft.com/fwlink/p/?LinkId=282413)。</span><span class="sxs-lookup"><span data-stu-id="f7dce-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="f7dce-147">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f7dce-147">More information</span></span>

<span data-ttu-id="f7dce-148">如果您知道如何使用 MSBuild 檔案，您可以在 *.pubxml*檔（適用于設定檔特定的工作）或專案的*wpp*檔案（適用于所有設定檔的工作）中撰寫程式碼，以自動化許多其他部署工作。</span><span class="sxs-lookup"><span data-stu-id="f7dce-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="f7dce-149">如需 *.pubxml*和*wpp .targets*檔案的詳細資訊，請參閱[如何：在發行設定檔（. .Pubxml）檔案中編輯部署設定和 Visual Studio Web 專案中的 wpp .targets](https://msdn.microsoft.com/library/ff398069)檔。</span><span class="sxs-lookup"><span data-stu-id="f7dce-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="f7dce-150">如需 MSBuild 程式碼的基本簡介，請參閱企業部署系列中的**專案檔案剖析** [：瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔。</span><span class="sxs-lookup"><span data-stu-id="f7dce-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="f7dce-151">若要瞭解如何使用 MSBuild 檔案在您自己的案例中執行工作，請參閱這本書：在[Microsoft Build Engine：使用 MSBuild 和 Team Foundation Build](http://msbuildbook.com) By Sayed Ibraham Hashimi 和 William Bartholomew。</span><span class="sxs-lookup"><span data-stu-id="f7dce-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="f7dce-152">致謝</span><span class="sxs-lookup"><span data-stu-id="f7dce-152">Acknowledgements</span></span>

<span data-ttu-id="f7dce-153">我想感謝下列人對本教學課程系列的內容做出重大貢獻：</span><span class="sxs-lookup"><span data-stu-id="f7dce-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="f7dce-154">Alberto Poblacion，MVP &amp; MCT，西班牙</span><span class="sxs-lookup"><span data-stu-id="f7dce-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="f7dce-155">Jarod Ferguson，資料平臺開發 MVP，美國</span><span class="sxs-lookup"><span data-stu-id="f7dce-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="f7dce-156">Microsoft 的 Mittal</span><span class="sxs-lookup"><span data-stu-id="f7dce-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="f7dce-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) （twitter： [@jongalloway](http://twitter.com/jongalloway)）</span><span class="sxs-lookup"><span data-stu-id="f7dce-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="f7dce-158">Kristina Olson，Microsoft</span><span class="sxs-lookup"><span data-stu-id="f7dce-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="f7dce-159">Mike Pope，Microsoft</span><span class="sxs-lookup"><span data-stu-id="f7dce-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="f7dce-160">Mohit Srivastava，Microsoft</span><span class="sxs-lookup"><span data-stu-id="f7dce-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="f7dce-161">Raffaele Rialdi，義大利</span><span class="sxs-lookup"><span data-stu-id="f7dce-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="f7dce-162">Rick Anderson，Microsoft</span><span class="sxs-lookup"><span data-stu-id="f7dce-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="f7dce-163">[Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）</span><span class="sxs-lookup"><span data-stu-id="f7dce-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="f7dce-164">[Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）</span><span class="sxs-lookup"><span data-stu-id="f7dce-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="f7dce-165">[Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）</span><span class="sxs-lookup"><span data-stu-id="f7dce-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="f7dce-166">Srđan Božović，塞爾維亞</span><span class="sxs-lookup"><span data-stu-id="f7dce-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="f7dce-167">[Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）</span><span class="sxs-lookup"><span data-stu-id="f7dce-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f7dce-168">[上一頁](command-line-deployment.md)
> [下一頁](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="f7dce-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>
