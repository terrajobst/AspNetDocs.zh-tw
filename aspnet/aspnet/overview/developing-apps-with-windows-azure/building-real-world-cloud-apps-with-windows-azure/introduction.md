---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: 使用 Azure 建立真實世界的雲端應用程式 |Microsoft Docs
author: MikeWasson
description: 本電子書將逐步引導您建立以模式為基礎的方法，以建立真實世界的雲端解決方案。 這些模式適用于開發進程以及 。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: b88573b3702b755b155e8da35f5f8a67931bafc6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617590"
---
# <a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="1ce79-104">使用 Azure 建立真實世界的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="1ce79-104">Building Real-World Cloud Apps with Azure</span></span>

<span data-ttu-id="1ce79-105">由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1ce79-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="1ce79-106">[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="1ce79-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="1ce79-107">本電子書將逐步引導您建立以模式為基礎的方法，以建立真實世界的雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="1ce79-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="1ce79-108">這些模式適用于開發程式以及架構和程式碼撰寫實務。</span><span class="sxs-lookup"><span data-stu-id="1ce79-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="1ce79-109">內容是以 Scott Guthrie 開發的簡報為基礎，並由他在2013年6月（第[1](http://vimeo.com/68215538)部分，[第 2](http://vimeo.com/68215602)部分）和 Microsoft Tech Ed 2013 澳大利亞（第[1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)部，第[2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)部分）的「挪威開發人員會議」（NDC）提供。</span><span class="sxs-lookup"><span data-stu-id="1ce79-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="1ce79-110">[許多人](more-patterns-and-guidance.md#acknowledgments)都會更新並增強內容，同時將它從影片轉換成書面形式。</span><span class="sxs-lookup"><span data-stu-id="1ce79-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>

## <a name="intended-audience"></a><span data-ttu-id="1ce79-111">適用對象</span><span class="sxs-lookup"><span data-stu-id="1ce79-111">Intended Audience</span></span>

<span data-ttu-id="1ce79-112">對於想要針對雲端進行開發的開發人員而言，考慮移至雲端或雲端開發的新手，會大致瞭解他們需要知道的最重要概念和做法。</span><span class="sxs-lookup"><span data-stu-id="1ce79-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="1ce79-113">概念會以具體範例來說明，而每個章節都會連結至其他資源，以取得更深入的資訊。</span><span class="sxs-lookup"><span data-stu-id="1ce79-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="1ce79-114">這些範例和其他資源的連結適用于 Microsoft 架構和服務，但說明的原則也適用于其他 網頁程式開發架構和雲端環境。</span><span class="sxs-lookup"><span data-stu-id="1ce79-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="1ce79-115">已針對雲端進行開發的開發人員可能會在這裡找到有助於使其更成功的想法。</span><span class="sxs-lookup"><span data-stu-id="1ce79-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="1ce79-116">系列中的每個章節都可以獨立讀取，因此您可以挑選並選擇您感興趣的主題。</span><span class="sxs-lookup"><span data-stu-id="1ce79-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="1ce79-117">有人監看 Scott Guthrie*使用 Azure 簡報建立真實世界的雲端應用程式*，並想要更多詳細資料和更新的資訊，請參閱這裡。</span><span class="sxs-lookup"><span data-stu-id="1ce79-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="1ce79-118">雲端開發模式</span><span class="sxs-lookup"><span data-stu-id="1ce79-118">Cloud development patterns</span></span>

<span data-ttu-id="1ce79-119">這本電子書會針對雲端開發說明13個建議模式。</span><span class="sxs-lookup"><span data-stu-id="1ce79-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="1ce79-120">在這裡使用「模式」，是指執行事項的建議方式：如何開發、設計和編碼雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ce79-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="1ce79-121">這些是重要的模式，可協助您在後續追蹤「成功」的情況。</span><span class="sxs-lookup"><span data-stu-id="1ce79-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="1ce79-122">將[所有專案自動化](automate-everything.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="1ce79-123">使用腳本來最大化效率，並將重複性進程中的錯誤降至最低。</span><span class="sxs-lookup"><span data-stu-id="1ce79-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="1ce79-124">示範： Azure 管理腳本。</span><span class="sxs-lookup"><span data-stu-id="1ce79-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="1ce79-125">[原始檔控制](source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="1ce79-126">在原始檔控制中設定分支結構，以加速 DevOps 工作流程。</span><span class="sxs-lookup"><span data-stu-id="1ce79-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="1ce79-127">示範：將腳本加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="1ce79-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="1ce79-128">示範：將敏感性資料從原始檔控制中排除。</span><span class="sxs-lookup"><span data-stu-id="1ce79-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="1ce79-129">示範：在 Visual Studio 中使用 Git。</span><span class="sxs-lookup"><span data-stu-id="1ce79-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="1ce79-130">[持續整合與傳遞](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="1ce79-131">使用每個原始檔控制簽入，將組建和部署自動化。</span><span class="sxs-lookup"><span data-stu-id="1ce79-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="1ce79-132">[Web 開發最佳作法](web-development-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="1ce79-133">保持 web 層無狀態。</span><span class="sxs-lookup"><span data-stu-id="1ce79-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="1ce79-134">示範： Azure App Service 中的 Web Apps 縮放和自動調整。</span><span class="sxs-lookup"><span data-stu-id="1ce79-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="1ce79-135">避免會話狀態。</span><span class="sxs-lookup"><span data-stu-id="1ce79-135">Avoid session state.</span></span>
    - <span data-ttu-id="1ce79-136">當 CDN 無法使用時，請將 CDN 與 fallback 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1ce79-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="1ce79-137">使用非同步程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="1ce79-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="1ce79-138">示範：在 ASP.NET MVC 和 Entity Framework 中非同步。</span><span class="sxs-lookup"><span data-stu-id="1ce79-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="1ce79-139">[單一登入](single-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="1ce79-140">Azure Active Directory 簡介。</span><span class="sxs-lookup"><span data-stu-id="1ce79-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="1ce79-141">示範：建立使用 Azure Active Directory 的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ce79-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="1ce79-142">[資料儲存選項](data-storage-options.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="1ce79-143">資料存放區的類型。</span><span class="sxs-lookup"><span data-stu-id="1ce79-143">Types of data stores.</span></span>
    - <span data-ttu-id="1ce79-144">如何選擇正確的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="1ce79-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="1ce79-145">示範： Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="1ce79-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="1ce79-146">[資料分割策略](data-partitioning-strategies.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="1ce79-147">以垂直、水準或兩者的方式分割資料，以加速調整關係資料庫。</span><span class="sxs-lookup"><span data-stu-id="1ce79-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="1ce79-148">[非結構化 blob 儲存體](unstructured-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="1ce79-149">使用 blob 服務將檔案儲存在雲端。</span><span class="sxs-lookup"><span data-stu-id="1ce79-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="1ce79-150">示範：在修正 It 應用程式中使用 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1ce79-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="1ce79-151">[設計到存活的失敗](design-to-survive-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="1ce79-152">失敗的類型。</span><span class="sxs-lookup"><span data-stu-id="1ce79-152">Types of failures.</span></span>
    - <span data-ttu-id="1ce79-153">失敗範圍。</span><span class="sxs-lookup"><span data-stu-id="1ce79-153">Failure Scope.</span></span>
    - <span data-ttu-id="1ce79-154">瞭解 Sla。</span><span class="sxs-lookup"><span data-stu-id="1ce79-154">Understanding SLAs.</span></span>
- <span data-ttu-id="1ce79-155">[監視和遙測](monitoring-and-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="1ce79-156">為什麼您應該同時購買遙測應用程式，並撰寫自己的程式碼來檢測您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ce79-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="1ce79-157">示範： Azure 的新 New relic</span><span class="sxs-lookup"><span data-stu-id="1ce79-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="1ce79-158">示範：在修正 It 應用程式中記錄程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ce79-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="1ce79-159">示範：修正 It 應用程式中的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="1ce79-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="1ce79-160">示範： Azure 中的內建記錄支援。</span><span class="sxs-lookup"><span data-stu-id="1ce79-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="1ce79-161">[暫時性錯誤處理](transient-fault-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="1ce79-162">使用智慧型重試/轉型邏輯來減輕暫時性失敗的影響。</span><span class="sxs-lookup"><span data-stu-id="1ce79-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="1ce79-163">示範： Entity Framework 6 中的 [重試]/[關閉]。</span><span class="sxs-lookup"><span data-stu-id="1ce79-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="1ce79-164">[分散式](distributed-caching.md)快取。</span><span class="sxs-lookup"><span data-stu-id="1ce79-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="1ce79-165">使用分散式快取來改善擴充性並降低資料庫交易成本。</span><span class="sxs-lookup"><span data-stu-id="1ce79-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="1ce79-166">以[佇列為中心的工作模式](queue-centric-work-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="1ce79-167">藉由鬆散結合 web 和背景工作角色層，啟用高可用性並改善擴充性。</span><span class="sxs-lookup"><span data-stu-id="1ce79-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="1ce79-168">示範：修正 It 應用程式中的 Azure 儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="1ce79-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="1ce79-169">[更多雲端應用程式模式和指導](more-patterns-and-guidance.md)方針。</span><span class="sxs-lookup"><span data-stu-id="1ce79-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="1ce79-170">附錄︰修正範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1ce79-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="1ce79-171">已知問題</span><span class="sxs-lookup"><span data-stu-id="1ce79-171">Known Issues</span></span>
    - <span data-ttu-id="1ce79-172">最佳作法</span><span class="sxs-lookup"><span data-stu-id="1ce79-172">Best Practices</span></span>
    - <span data-ttu-id="1ce79-173">如何下載、建立、執行和部署。</span><span class="sxs-lookup"><span data-stu-id="1ce79-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="1ce79-174">這些模式適用于所有雲端環境，但我們將使用以 Microsoft 技術和服務為基礎的範例（例如 Visual Studio、Team Foundation Service、ASP.NET 和 Azure）加以說明。</span><span class="sxs-lookup"><span data-stu-id="1ce79-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="1ce79-175">本章節的其餘部分將介紹 fix it 應用程式執行所在 Azure App Service 雲端環境中的修正 It 範例應用程式和 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="1ce79-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="1ce79-176">修正 it 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1ce79-176">The Fix it sample application</span></span>

<span data-ttu-id="1ce79-177">本電子書中所顯示的大部分螢幕擷取畫面和程式碼範例，都是以[Scott Guthrie](https://weblogs.asp.net/scottgu/)最初開發的修正 It 應用程式為基礎，以示範建議的雲端應用程式開發模式和實務。</span><span class="sxs-lookup"><span data-stu-id="1ce79-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![修正 It 應用程式首頁](introduction/_static/image1.png)

<span data-ttu-id="1ce79-179">範例應用程式是簡單的工作專案票證系統。</span><span class="sxs-lookup"><span data-stu-id="1ce79-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="1ce79-180">當您需要固定的專案時，您會建立票證並將它指派給其他人，而其他人可以登入並查看指派給他們的票證，並在工作完成時將票證標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="1ce79-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="1ce79-181">這是標準的 Visual Studio Web 專案。</span><span class="sxs-lookup"><span data-stu-id="1ce79-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="1ce79-182">它是以 ASP.NET MVC 為基礎，並使用 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1ce79-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="1ce79-183">它可以在 IIS Express 本機執行，並可部署至 Azure 網站以在雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="1ce79-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="1ce79-184">您可以使用表單驗證和本機資料庫，或使用社交提供者（例如 Google）來登入。</span><span class="sxs-lookup"><span data-stu-id="1ce79-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="1ce79-185">（稍後我們也會示範如何使用 Active Directory 組織帳戶登入。）</span><span class="sxs-lookup"><span data-stu-id="1ce79-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![登入頁面](introduction/_static/image2.png)

<span data-ttu-id="1ce79-187">登入之後，您可以建立票證，將它指派給其他人，並上傳您想要修正的圖片。</span><span class="sxs-lookup"><span data-stu-id="1ce79-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![建立 Fix It 工作](introduction/_static/image3.png)

![修正已建立的 It 工作](introduction/_static/image4.png)

<span data-ttu-id="1ce79-190">您可以追蹤所建立之工作專案的進度、查看指派給您的票證、查看票證詳細資料，以及將專案標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="1ce79-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="1ce79-191">這是從功能觀點來看的一個非常簡單的應用程式，但您會瞭解如何建立它，讓它可以擴充至數百萬名使用者，並可復原資料庫失敗和連接終止等專案。</span><span class="sxs-lookup"><span data-stu-id="1ce79-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="1ce79-192">您也將瞭解如何建立自動化和敏捷式開發工作流程，讓您能夠輕鬆地啟動簡單的應用程式，並以有效率且快速的方式反復執行開發週期。</span><span class="sxs-lookup"><span data-stu-id="1ce79-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="1ce79-193">Azure App Service 中的 Web Apps</span><span class="sxs-lookup"><span data-stu-id="1ce79-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="1ce79-194">用於修正 It 應用程式的雲端環境是我們稱之為「網站」的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="1ce79-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="1ce79-195">此服務可讓您在 Azure 中裝載自己的 web 應用程式，而不需要建立 Vm 並保持其更新、安裝和設定 IIS 等。我們會在 Vm 上裝載您的網站，並自動為您提供備份和復原和其他服務。</span><span class="sxs-lookup"><span data-stu-id="1ce79-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="1ce79-196">Web Sites 服務適用于 ASP.NET、node.js、PHP 和 Python。</span><span class="sxs-lookup"><span data-stu-id="1ce79-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="1ce79-197">它可讓您使用 Visual Studio、Web Deploy、FTP、Git 或 TFS，非常快速地進行部署。</span><span class="sxs-lookup"><span data-stu-id="1ce79-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="1ce79-198">在您開始部署的時間和透過網際網路提供更新的時間之間，通常只需要幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="1ce79-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="1ce79-199">免費開始使用，而且您可以隨著流量成長而相應增加。</span><span class="sxs-lookup"><span data-stu-id="1ce79-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="1ce79-200">在幕後，如果您要在自己的 Vm 上使用 IIS 來裝載網站，則 Azure App Service 中的 Web Apps 會提供許多您必須自行建立的架構元件和功能。</span><span class="sxs-lookup"><span data-stu-id="1ce79-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="1ce79-201">其中一個元件是部署端點，會自動設定 IIS，並在您想要執行網站的多個 Vm 上安裝您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ce79-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![部署服務](introduction/_static/image5.png)

<span data-ttu-id="1ce79-203">當使用者叫用網站時，他們不會直接叫用 IIS Vm，而是透過[應用程式要求路由（ARR）](https://www.iis.net/downloads/microsoft/application-request-routing)負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="1ce79-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="1ce79-204">您可以在自己的伺服器上使用這些資訊，但此處的優點是它們是自動設定的。</span><span class="sxs-lookup"><span data-stu-id="1ce79-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="1ce79-205">他們使用智慧型啟發學習法來考慮因素，例如會話親和性、IIS 中的佇列深度，以及每部電腦上的 CPU 使用量，以將流量導向裝載您網站的 Vm。</span><span class="sxs-lookup"><span data-stu-id="1ce79-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR 負載平衡器](introduction/_static/image6.png)

<span data-ttu-id="1ce79-207">如果電腦停止運作，Azure 會自動從輪替中提取該機器、加速新的 VM 實例，並開始將流量導向至新的實例--所有應用程式都不會停機。</span><span class="sxs-lookup"><span data-stu-id="1ce79-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![從電腦失敗中自動復原](introduction/_static/image7.png)

<span data-ttu-id="1ce79-209">這一切都是自動進行。</span><span class="sxs-lookup"><span data-stu-id="1ce79-209">All of this takes place automatically.</span></span> <span data-ttu-id="1ce79-210">您只需要建立網站，然後使用 Windows PowerShell、Visual Studio 或 Azure 管理入口網站，將您的應用程式部署到其中。</span><span class="sxs-lookup"><span data-stu-id="1ce79-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="1ce79-211">如需示範如何在 Visual Studio 中建立 web 應用程式並將其部署至 Azure 網站的快速簡單逐步教學課程，請參閱[開始使用 azure 和 ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="1ce79-212">總結</span><span class="sxs-lookup"><span data-stu-id="1ce79-212">Summary</span></span>

<span data-ttu-id="1ce79-213">本簡介已提供本書將涵蓋的主題清單、範例應用程式的螢幕擷取畫面，以及 Azure App Service 雲端環境中 Web Apps 的簡短總覽。</span><span class="sxs-lookup"><span data-stu-id="1ce79-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="1ce79-214">在和雲端中開發應用程式的其中一個絕佳優點，就是可以輕鬆地自動化重複的開發工作，例如建立測試環境，並將程式碼部署到其中。</span><span class="sxs-lookup"><span data-stu-id="1ce79-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="1ce79-215">這是[下一章](automate-everything.md)的主題。</span><span class="sxs-lookup"><span data-stu-id="1ce79-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="1ce79-216">資源</span><span class="sxs-lookup"><span data-stu-id="1ce79-216">Resources</span></span>

<span data-ttu-id="1ce79-217">如需本章所涵蓋之主題的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="1ce79-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="1ce79-218">文件：</span><span class="sxs-lookup"><span data-stu-id="1ce79-218">Documentation:</span></span>

- <span data-ttu-id="1ce79-219">[Azure App Service 中的 Web Apps](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="1ce79-220">關於 Web Apps 的 Azure 檔入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="1ce79-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="1ce79-221">Web Apps、雲端服務和 Vm：使用時機？</span><span class="sxs-lookup"><span data-stu-id="1ce79-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="1ce79-222">如本章所示，WAWS 只是您可以在 Azure 中執行 web 應用程式的三種方法之一。</span><span class="sxs-lookup"><span data-stu-id="1ce79-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="1ce79-223">本文說明三種方式之間的差異，並提供如何選擇哪一個最適合您案例的指引。</span><span class="sxs-lookup"><span data-stu-id="1ce79-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="1ce79-224">就像 Web Sites，雲端服務是 Azure 的 PaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="1ce79-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="1ce79-225">Vm 是 IaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="1ce79-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="1ce79-226">如需 PaaS 與 IaaS 的說明，請參閱[資料選項](data-storage-options.md#paasiaas)一章。</span><span class="sxs-lookup"><span data-stu-id="1ce79-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="1ce79-227">影片：</span><span class="sxs-lookup"><span data-stu-id="1ce79-227">Videos:</span></span>

- [<span data-ttu-id="1ce79-228">Scott Guthrie 從步驟0開始，什麼是 Azure 雲端 OS？</span><span class="sxs-lookup"><span data-stu-id="1ce79-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="1ce79-229">[Web Sites 架構-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="1ce79-230">[Azure 網站內部的 Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。</span><span class="sxs-lookup"><span data-stu-id="1ce79-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1ce79-231">下一個</span><span class="sxs-lookup"><span data-stu-id="1ce79-231">Next</span></span>](automate-everything.md)
