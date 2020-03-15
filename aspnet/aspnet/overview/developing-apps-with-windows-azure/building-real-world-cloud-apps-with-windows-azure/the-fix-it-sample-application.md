---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附錄：修正 It 範例應用程式（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583444"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="21de5-104">附錄：修正 It 範例應用程式（使用 Azure 建立真實世界的雲端應用程式）</span><span class="sxs-lookup"><span data-stu-id="21de5-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="21de5-105">由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="21de5-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="21de5-106">下載 Fix It 專案</span><span class="sxs-lookup"><span data-stu-id="21de5-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="21de5-107">**使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。</span><span class="sxs-lookup"><span data-stu-id="21de5-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="21de5-108">其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21de5-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="21de5-109">如需電子書的相關資訊，請參閱[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="21de5-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="21de5-110">使用 Azure 電子書建立真實世界雲端應用程式的本附錄包含下列各節，其中提供可供您下載之 Fix It 範例應用程式的其他相關資訊：</span><span class="sxs-lookup"><span data-stu-id="21de5-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="21de5-111">已知問題</span><span class="sxs-lookup"><span data-stu-id="21de5-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="21de5-112">最佳做法</span><span class="sxs-lookup"><span data-stu-id="21de5-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="21de5-113">如何從本機電腦上的 Visual Studio 執行應用程式</span><span class="sxs-lookup"><span data-stu-id="21de5-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="21de5-114">如何使用 Windows PowerShell 腳本將基本應用程式部署至 Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="21de5-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="21de5-115">疑難排解 Windows PowerShell 腳本</span><span class="sxs-lookup"><span data-stu-id="21de5-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="21de5-116">如何將具有佇列處理的應用程式部署至 Azure App Service Web Apps 和 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="21de5-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="21de5-117">已知問題</span><span class="sxs-lookup"><span data-stu-id="21de5-117">Known issues</span></span>

<span data-ttu-id="21de5-118">最初開發的 Fix It 應用程式，是為了說明這種電子書所呈現的一些模式。</span><span class="sxs-lookup"><span data-stu-id="21de5-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="21de5-119">不過，由於電子書是關於建立真實世界的應用程式，因此我們會將 Fix It 程式碼與我們針對發行之軟體所做的檢查和測試流程進行比對。</span><span class="sxs-lookup"><span data-stu-id="21de5-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="21de5-120">我們發現許多問題，如同任何真實世界的應用程式，我們已修正其中一些問題，而其中一些我們已延遲到較新的版本。</span><span class="sxs-lookup"><span data-stu-id="21de5-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="21de5-121">下列清單包含應在實際執行應用程式中解決的問題，但基於其中一個原因或我們決定不在「修正 It」範例應用程式的初始版本中處理。</span><span class="sxs-lookup"><span data-stu-id="21de5-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="21de5-122">安全性</span><span class="sxs-lookup"><span data-stu-id="21de5-122">Security</span></span>

- <span data-ttu-id="21de5-123">請確定您無法將工作指派給不存在的擁有者。</span><span class="sxs-lookup"><span data-stu-id="21de5-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="21de5-124">請確定您只能查看和修改您所建立或指派給您的工作。</span><span class="sxs-lookup"><span data-stu-id="21de5-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="21de5-125">對登入頁面和驗證 cookie 使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="21de5-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="21de5-126">指定驗證 cookie 的時間限制。</span><span class="sxs-lookup"><span data-stu-id="21de5-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="21de5-127">輸入驗證</span><span class="sxs-lookup"><span data-stu-id="21de5-127">Input validation</span></span>

<span data-ttu-id="21de5-128">一般來說，生產應用程式會比修正 It 應用程式執行更多的輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="21de5-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="21de5-129">例如，允許進行上傳的映射大小/影像檔案大小應該會受到限制。</span><span class="sxs-lookup"><span data-stu-id="21de5-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="21de5-130">系統管理員功能</span><span class="sxs-lookup"><span data-stu-id="21de5-130">Administrator functionality</span></span>

<span data-ttu-id="21de5-131">系統管理員應該能夠變更現有工作的擁有權。</span><span class="sxs-lookup"><span data-stu-id="21de5-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="21de5-132">例如，工作的建立者可能會離開公司，除非已啟用系統管理存取權，否則不會有任何人可以維護工作。</span><span class="sxs-lookup"><span data-stu-id="21de5-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="21de5-133">佇列訊息處理</span><span class="sxs-lookup"><span data-stu-id="21de5-133">Queue message processing</span></span>

<span data-ttu-id="21de5-134">修正 It 應用程式中的佇列訊息處理是設計成簡單的，以便以最少量的程式碼來說明以佇列為中心的工作模式。</span><span class="sxs-lookup"><span data-stu-id="21de5-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="21de5-135">這個簡單的程式碼不適合實際的生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="21de5-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="21de5-136">程式碼不保證每個佇列訊息最多會處理一次。</span><span class="sxs-lookup"><span data-stu-id="21de5-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="21de5-137">當您從佇列取得訊息時，會有一個超時期間，在此期間內，其他佇列接聽程式看不到訊息。</span><span class="sxs-lookup"><span data-stu-id="21de5-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="21de5-138">如果在刪除訊息之前的超時時間已過期，訊息就會再次顯示。</span><span class="sxs-lookup"><span data-stu-id="21de5-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="21de5-139">因此，如果背景工作角色實例花了很長的時間處理訊息，則理論上可能會有相同的訊息處理兩次，導致資料庫發生重複的工作。</span><span class="sxs-lookup"><span data-stu-id="21de5-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="21de5-140">如需有關此問題的詳細資訊，請參閱[使用 Azure 儲存體的佇列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。</span><span class="sxs-lookup"><span data-stu-id="21de5-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="21de5-141">藉由批次處理訊息抓取，佇列輪詢邏輯可能更符合成本效益。</span><span class="sxs-lookup"><span data-stu-id="21de5-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="21de5-142">每次呼叫[CloudQueue](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)時，都有交易成本。</span><span class="sxs-lookup"><span data-stu-id="21de5-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="21de5-143">相反地，您可以呼叫[CloudQueue. GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) （請注意複數的 '），這會在單一交易中取得多個訊息。</span><span class="sxs-lookup"><span data-stu-id="21de5-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="21de5-144">Azure 儲存體佇列的交易成本非常低，因此在大部分的情況下，對成本所造成的影響並不明顯。</span><span class="sxs-lookup"><span data-stu-id="21de5-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="21de5-145">佇列訊息處理常式代碼中的緊密迴圈會導致 CPU 親和性，而不會有效率地使用多核心 Vm。</span><span class="sxs-lookup"><span data-stu-id="21de5-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="21de5-146">較佳的設計會使用工作平行處理原則，平行執行數個非同步工作。</span><span class="sxs-lookup"><span data-stu-id="21de5-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="21de5-147">佇列訊息處理只有基本的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="21de5-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="21de5-148">例如，程式碼不會處理[有害訊息](https://msdn.microsoft.com/library/ms789028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21de5-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="21de5-149">（當訊息處理造成例外狀況時，您必須記錄錯誤並刪除訊息，否則背景工作角色會嘗試再次處理它，迴圈將會無限期地繼續）。</span><span class="sxs-lookup"><span data-stu-id="21de5-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="21de5-150">SQL 查詢沒有界限</span><span class="sxs-lookup"><span data-stu-id="21de5-150">SQL queries are unbounded</span></span>

<span data-ttu-id="21de5-151">最新的修正程式碼不會限制索引頁面的查詢可能會傳回多少資料列。</span><span class="sxs-lookup"><span data-stu-id="21de5-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="21de5-152">如果在資料庫中輸入大量的工作，收到的結果清單大小可能會造成效能問題。</span><span class="sxs-lookup"><span data-stu-id="21de5-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="21de5-153">解決方案是執行分頁。</span><span class="sxs-lookup"><span data-stu-id="21de5-153">The solution is to implement paging.</span></span> <span data-ttu-id="21de5-154">如需範例，請參閱[使用 ASP.NET MVC 應用程式中的 Entity Framework 排序、篩選和分頁](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="21de5-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="21de5-155">建議的視圖模型</span><span class="sxs-lookup"><span data-stu-id="21de5-155">View models recommended</span></span>

<span data-ttu-id="21de5-156">Fix It 應用程式會使用 FixItTask 實體類別，在控制器和視圖之間傳遞資訊。</span><span class="sxs-lookup"><span data-stu-id="21de5-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="21de5-157">最佳做法是使用 view 模型。</span><span class="sxs-lookup"><span data-stu-id="21de5-157">A best practice is to use view models.</span></span> <span data-ttu-id="21de5-158">領域模型（例如，FixItTask 實體類別）是以資料持續性所需的方式來設計，而視圖模型則可以設計來呈現資料。</span><span class="sxs-lookup"><span data-stu-id="21de5-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="21de5-159">如需詳細資訊，請參閱[12 ASP.NET MVC 最佳做法](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21de5-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="21de5-160">建議使用安全映射 blob</span><span class="sxs-lookup"><span data-stu-id="21de5-160">Secure image blob recommended</span></span>

<span data-ttu-id="21de5-161">Fix It 應用程式會將已上傳的影像儲存為公用，這表示任何尋找該 URL 的人都可以存取影像。</span><span class="sxs-lookup"><span data-stu-id="21de5-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="21de5-162">影像可以受到保護，而不是公用。</span><span class="sxs-lookup"><span data-stu-id="21de5-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="21de5-163">沒有適用于佇列的 PowerShell 自動化腳本</span><span class="sxs-lookup"><span data-stu-id="21de5-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="21de5-164">範例 PowerShell 自動化腳本只是針對修正它的基礎版本而撰寫，它完全在 Azure App Service Web Apps 中執行。</span><span class="sxs-lookup"><span data-stu-id="21de5-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="21de5-165">我們尚未提供用來設定和部署至 web 應用程式的腳本，以及佇列處理所需的雲端服務環境。</span><span class="sxs-lookup"><span data-stu-id="21de5-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="21de5-166">使用者輸入中 HTML 程式碼的特殊處理</span><span class="sxs-lookup"><span data-stu-id="21de5-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="21de5-167">ASP.NET 會在使用者輸入文字方塊中輸入腳本，自動防止惡意使用者嘗試跨網站腳本攻擊的許多方式。</span><span class="sxs-lookup"><span data-stu-id="21de5-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="21de5-168">以及用來顯示工作標題和附注的 MVC `DisplayFor` helper，會自動將其傳送至瀏覽器的值進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="21de5-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="21de5-169">但是在生產環境應用程式中，您可能會想要採取其他措施。</span><span class="sxs-lookup"><span data-stu-id="21de5-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="21de5-170">如需詳細資訊，請參閱[在 ASP.NET 中要求驗證](https://msdn.microsoft.com/library/hh882339.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21de5-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="21de5-171">最佳作法</span><span class="sxs-lookup"><span data-stu-id="21de5-171">Best practices</span></span>

<span data-ttu-id="21de5-172">以下是在程式碼審查和測試修正 It 應用程式的原始版本中探索後已修正的一些問題。</span><span class="sxs-lookup"><span data-stu-id="21de5-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="21de5-173">有些是因為原始當中不知道特定的最佳作法，而是因為程式碼是快速撰寫，而不是用於發行的軟體。</span><span class="sxs-lookup"><span data-stu-id="21de5-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="21de5-174">我們會在這裡列出問題，以防我們從這項審查和測試中學習到的內容，對於同時也在開發 web 應用程式的其他人可能會有説明。</span><span class="sxs-lookup"><span data-stu-id="21de5-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="21de5-175">處置資料庫存放庫</span><span class="sxs-lookup"><span data-stu-id="21de5-175">Dispose the database repository</span></span>

<span data-ttu-id="21de5-176">`FixItTaskRepository` 類別必須處置 Entity Framework `DbContext` 實例。</span><span class="sxs-lookup"><span data-stu-id="21de5-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="21de5-177">我們藉由在 `FixItTaskRepository` 類別中執行 `IDisposable` 來完成這項操作：</span><span class="sxs-lookup"><span data-stu-id="21de5-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="21de5-178">請注意，AutoFac 會自動處置 `FixItTaskRepository` 實例，因此我們不需要明確地處置它。</span><span class="sxs-lookup"><span data-stu-id="21de5-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="21de5-179">另一個選項是從 `FixItTaskRepository`移除 `DbContext` 成員變數，並改為在 `using` 語句內部的每個存放庫方法中建立本機 `DbContext` 變數。</span><span class="sxs-lookup"><span data-stu-id="21de5-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="21de5-180">例如:</span><span class="sxs-lookup"><span data-stu-id="21de5-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="21de5-181">使用 DI 註冊單次個體</span><span class="sxs-lookup"><span data-stu-id="21de5-181">Register singletons as such with DI</span></span>

<span data-ttu-id="21de5-182">由於只需要 `PhotoService` 類別和 `Logger` 類別的一個實例，因此應該在*DependenciesConfig.cs*中將這些類別[註冊為單一實例以進行](https://code.google.com/p/autofac/wiki/InstanceScope)相依性插入：</span><span class="sxs-lookup"><span data-stu-id="21de5-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="21de5-183">安全性：不要向使用者顯示錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="21de5-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="21de5-184">原始的修正 It 應用程式沒有一般錯誤頁面，只要讓所有例外狀況反升至 UI，因此某些例外狀況（例如資料庫連接錯誤）可能會導致完整的堆疊追蹤顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="21de5-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="21de5-185">詳細的錯誤資訊有時可能會協助惡意使用者發動攻擊。</span><span class="sxs-lookup"><span data-stu-id="21de5-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="21de5-186">解決方案是記錄例外狀況詳細資料，並向不包含錯誤詳細資料的使用者顯示錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="21de5-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="21de5-187">Fix It 應用程式已在進行記錄，而為了顯示錯誤頁面，我們在 web.config 檔案中加入了 `<customErrors mode=On>`。</span><span class="sxs-lookup"><span data-stu-id="21de5-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="21de5-188">根據預設，這會顯示錯誤的*Views\Shared\Error.cshtml* 。</span><span class="sxs-lookup"><span data-stu-id="21de5-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="21de5-189">您可以自訂*error. cshtml*或建立自己的錯誤網頁檢視，並加入 `defaultRedirect` 屬性。</span><span class="sxs-lookup"><span data-stu-id="21de5-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="21de5-190">您也可以針對特定錯誤指定不同的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="21de5-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="21de5-191">安全性：只允許其建立者編輯工作</span><span class="sxs-lookup"><span data-stu-id="21de5-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="21de5-192">[儀表板索引] 頁面只會顯示登入的使用者所建立的工作，但惡意使用者可以建立一個識別碼為另一個使用者工作的 URL。</span><span class="sxs-lookup"><span data-stu-id="21de5-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="21de5-193">我們已在*DashboardController.cs*中新增程式碼，以在此情況下傳回404：</span><span class="sxs-lookup"><span data-stu-id="21de5-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="21de5-194">不要忍受例外狀況</span><span class="sxs-lookup"><span data-stu-id="21de5-194">Don't swallow exceptions</span></span>

<span data-ttu-id="21de5-195">原始的修正 It 應用程式在記錄 SQL 查詢所產生的例外狀況之後，只會傳回 null：</span><span class="sxs-lookup"><span data-stu-id="21de5-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="21de5-196">這會讓使用者看起來像是查詢成功，但是只是未傳回任何資料列。</span><span class="sxs-lookup"><span data-stu-id="21de5-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="21de5-197">解決方法是在攔截和記錄之後重新擲回例外狀況：</span><span class="sxs-lookup"><span data-stu-id="21de5-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="21de5-198">攔截背景工作角色中的所有例外狀況</span><span class="sxs-lookup"><span data-stu-id="21de5-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="21de5-199">背景工作角色中任何未處理的例外狀況都會導致回收 VM，因此您會想要將您在 try-catch 區塊中執行的所有專案包裝在一起，並處理所有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="21de5-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="21de5-200">在實體類別中指定字串屬性的長度</span><span class="sxs-lookup"><span data-stu-id="21de5-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="21de5-201">為了顯示簡單的程式碼，原始版本的 Fix It 應用程式未指定 FixItTask 實體欄位的長度，因此在資料庫中定義為 Varchar （max）。</span><span class="sxs-lookup"><span data-stu-id="21de5-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="21de5-202">因此，UI 幾乎可以接受任何數量的輸入。</span><span class="sxs-lookup"><span data-stu-id="21de5-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="21de5-203">指定長度會將套用至 web 網頁中的使用者輸入和資料庫中的資料行大小限制：</span><span class="sxs-lookup"><span data-stu-id="21de5-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="21de5-204">當私用成員不應該變更時，將其標記為 readonly</span><span class="sxs-lookup"><span data-stu-id="21de5-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="21de5-205">例如，在 `DashboardController` 類別中，`FixItTaskRepository` 的實例已建立，而且不應該變更，所以我們將它定義為[readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21de5-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="21de5-206">使用清單。Any （）而不是 list。Count （） &gt; 0</span><span class="sxs-lookup"><span data-stu-id="21de5-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="21de5-207">如果您只在意清單中的一個或多個專案是否符合指定的準則，請使用[Any](https://msdn.microsoft.com/library/bb534972.aspx)方法，因為它會在找到條件的專案時立即傳回，而 `Count` 方法一律必須逐一查看每個專案。</span><span class="sxs-lookup"><span data-stu-id="21de5-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="21de5-208">儀表板*索引 cshtml*檔案原先具有下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="21de5-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="21de5-209">我們已將它變更為：</span><span class="sxs-lookup"><span data-stu-id="21de5-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="21de5-210">使用 MVC helper 在 MVC 視圖中產生 Url</span><span class="sxs-lookup"><span data-stu-id="21de5-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="21de5-211">若為首頁上的 [**建立 Fix it** ] 按鈕，請修正 it 應用程式硬式編碼錨定元素：</span><span class="sxs-lookup"><span data-stu-id="21de5-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="21de5-212">針對類似的視圖/動作連結，最好是使用[Url。動作](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx)HTML helper，例如：</span><span class="sxs-lookup"><span data-stu-id="21de5-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="21de5-213">使用工作。延遲而不是執行緒。背景工作角色中的睡眠</span><span class="sxs-lookup"><span data-stu-id="21de5-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="21de5-214">新專案範本會將 `Thread.Sleep` 放入背景工作角色的範例程式碼中，但造成執行緒進入睡眠狀態可能會造成執行緒集區產生額外的不必要執行緒。</span><span class="sxs-lookup"><span data-stu-id="21de5-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="21de5-215">您可以改為使用 [[延遲](https://msdn.microsoft.com/library/hh139096.aspx)] 來避免這種情況。</span><span class="sxs-lookup"><span data-stu-id="21de5-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="21de5-216">避免 async void</span><span class="sxs-lookup"><span data-stu-id="21de5-216">Avoid async void</span></span>

<span data-ttu-id="21de5-217">如果非同步方法不需要傳回值，則會傳回 `Task` 型別，而不是 `void`。</span><span class="sxs-lookup"><span data-stu-id="21de5-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="21de5-218">這個範例來自 `FixItQueueManager` 類別：</span><span class="sxs-lookup"><span data-stu-id="21de5-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="21de5-219">您應該只將 `async void` 用於最上層的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="21de5-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="21de5-220">如果您將方法定義為 `async void`，則呼叫端**無法等候**方法，或攔截方法擲回的任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="21de5-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="21de5-221">如需詳細資訊，請參閱[非同步程式設計中的最佳作法](https://msdn.microsoft.com/magazine/jj991977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21de5-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="21de5-222">使用解除標記來中斷背景工作角色迴圈</span><span class="sxs-lookup"><span data-stu-id="21de5-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="21de5-223">一般而言，背景工作角色上的**Run**方法包含無限迴圈。</span><span class="sxs-lookup"><span data-stu-id="21de5-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="21de5-224">當背景工作角色停止時，會呼叫[RoleEntryPoint](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="21de5-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="21de5-225">您應該使用這個方法來取消在**Run**方法內完成的工作，並正常結束。</span><span class="sxs-lookup"><span data-stu-id="21de5-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="21de5-226">否則，進程可能會在作業中途終止。</span><span class="sxs-lookup"><span data-stu-id="21de5-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="21de5-227">選擇不進行自動 MIME 探查程式</span><span class="sxs-lookup"><span data-stu-id="21de5-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="21de5-228">在某些情況下，Internet Explorer 報告的 MIME 類型與 web 伺服器所指定的類型不同。</span><span class="sxs-lookup"><span data-stu-id="21de5-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="21de5-229">比方說，如果 Internet Explorer 在以 HTTP 回應標頭 Content-type 提供的檔案中找到 HTML 內容： text/純文字，Internet Explorer 會判斷內容應該轉譯為 HTML。</span><span class="sxs-lookup"><span data-stu-id="21de5-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="21de5-230">可惜的是，這種「MIME 探查」也可能導致主控不受信任內容之伺服器的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="21de5-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="21de5-231">為了對抗這個問題，Internet Explorer 8 已對 MIME 類型的判斷程式碼進行了一些變更，並可讓應用程式開發人員選擇不使用[mime 探查](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21de5-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="21de5-232">下列程式碼已加入至*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="21de5-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="21de5-233">啟用捆綁和縮制</span><span class="sxs-lookup"><span data-stu-id="21de5-233">Enable bundling and minification</span></span>

<span data-ttu-id="21de5-234">當 Visual Studio 建立新的 Web 專案時，預設不會啟用 JavaScript 檔案的組合和縮制。</span><span class="sxs-lookup"><span data-stu-id="21de5-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="21de5-235">我們在 BundleConfig.cs 中新增了一行程式碼：</span><span class="sxs-lookup"><span data-stu-id="21de5-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="21de5-236">設定驗證 cookie 的到期時間</span><span class="sxs-lookup"><span data-stu-id="21de5-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="21de5-237">根據預設，驗證 cookie 會在兩周內過期。</span><span class="sxs-lookup"><span data-stu-id="21de5-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="21de5-238">較短的時間比較安全。</span><span class="sxs-lookup"><span data-stu-id="21de5-238">A shorter time is more secure.</span></span> <span data-ttu-id="21de5-239">您可以在*StartupAuth.cs*中變更此設定：</span><span class="sxs-lookup"><span data-stu-id="21de5-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="21de5-240">如何從本機電腦上的 Visual Studio 執行應用程式</span><span class="sxs-lookup"><span data-stu-id="21de5-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="21de5-241">有兩種方式可執行 Fix It 應用程式：</span><span class="sxs-lookup"><span data-stu-id="21de5-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="21de5-242">執行會將新工作直接寫入 SQL 資料庫的基底應用程式。</span><span class="sxs-lookup"><span data-stu-id="21de5-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="21de5-243">使用佇列加上後端服務來執行應用程式，以建立工作。</span><span class="sxs-lookup"><span data-stu-id="21de5-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="21de5-244">佇列模式會在以[佇列為中心的工作模式](queue-centric-work-pattern.md)一章中加以說明。</span><span class="sxs-lookup"><span data-stu-id="21de5-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="21de5-245">執行基底應用程式</span><span class="sxs-lookup"><span data-stu-id="21de5-245">Run the base application</span></span>

1. <span data-ttu-id="21de5-246">安裝 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="21de5-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="21de5-247">安裝[適用于 Visual Studio 的 AZURE SDK for .net](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="21de5-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="21de5-248">從[MSDN 程式碼庫](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下載 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="21de5-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="21de5-249">在 [檔案管理器] 中，以滑鼠右鍵按一下 .zip 檔案，然後按一下 [屬性]，然後在屬性視窗按一下 [解除封鎖]。</span><span class="sxs-lookup"><span data-stu-id="21de5-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="21de5-250">解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="21de5-250">Unzip the file.</span></span>
6. <span data-ttu-id="21de5-251">按兩下 .sln 檔案以啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="21de5-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="21de5-252">從 [**工具**] 功能表中，依序按一下 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="21de5-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="21de5-253">在 [套件管理員主控台] （PMC）中，按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="21de5-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="21de5-254">結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="21de5-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="21de5-255">啟動[Azure 儲存體模擬器](/azure/storage/common/storage-use-emulator)。</span><span class="sxs-lookup"><span data-stu-id="21de5-255">Start the [Azure storage emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="21de5-256">重新開機 Visual Studio，開啟您在上一個步驟中關閉的方案檔。</span><span class="sxs-lookup"><span data-stu-id="21de5-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="21de5-257">請確定 FixIt 專案已設定為啟始專案，然後按 CTRL + F5 執行專案。</span><span class="sxs-lookup"><span data-stu-id="21de5-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="21de5-258">執行具有佇列處理的應用程式</span><span class="sxs-lookup"><span data-stu-id="21de5-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="21de5-259">遵循執行[基底應用程式](#runbase)的指示，然後關閉瀏覽器並關閉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="21de5-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="21de5-260">使用系統管理員許可權啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="21de5-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="21de5-261">（您將會使用 Azure 計算模擬器，而這需要系統管理員許可權）。</span><span class="sxs-lookup"><span data-stu-id="21de5-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="21de5-262">在*MyFixIt*專案（Web 專案）中的應用程式*web.config*檔案中，將 `appSettings/UseQueues` 的值變更為 "true"：</span><span class="sxs-lookup"><span data-stu-id="21de5-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="21de5-263">如果[Azure 儲存體模擬器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)仍未執行，請重新開機它。</span><span class="sxs-lookup"><span data-stu-id="21de5-263">If the [Azure storage emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="21de5-264">同時執行 FixIt Web 專案和 MyFixItCloudService 專案。</span><span class="sxs-lookup"><span data-stu-id="21de5-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="21de5-265">使用 Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="21de5-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="21de5-266">按**F5**執行 FixIt 專案。</span><span class="sxs-lookup"><span data-stu-id="21de5-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="21de5-267">在**方案總管**中，以滑鼠右鍵按一下 MyFixItCloudService 專案，然後按一下  **Debug**  > **開始新實例**。</span><span class="sxs-lookup"><span data-stu-id="21de5-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="21de5-268">使用適用于 Web 的 Visual Studio 2013 Express：</span><span class="sxs-lookup"><span data-stu-id="21de5-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="21de5-269">在方案總管中，以滑鼠右鍵按一下 FixIt 方案，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="21de5-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="21de5-270">選取 [**多個啟始專案**]。</span><span class="sxs-lookup"><span data-stu-id="21de5-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="21de5-271">在 [MyFixIt 和 MyFixItCloudService] 底下的 [**動作**] 下拉式清單中，選取 [**啟動**]。</span><span class="sxs-lookup"><span data-stu-id="21de5-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="21de5-272">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="21de5-272">Click **OK**.</span></span>
   7. <span data-ttu-id="21de5-273">按 **F5** 執行這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="21de5-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="21de5-274">當您執行 MyFixItCloudService 專案時，Visual Studio 會啟動 Azure 計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="21de5-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="21de5-275">視您的防火牆設定而定，您可能需要允許模擬器通過防火牆。</span><span class="sxs-lookup"><span data-stu-id="21de5-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="21de5-276">如何使用 Windows PowerShell 腳本將基本應用程式部署至 Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="21de5-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="21de5-277">為了說明「[自動化所有專案](automate-everything.md)」模式，您可以使用在 Azure 中設定環境並將專案部署到新環境的腳本來提供修正 It 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21de5-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="21de5-278">下列指示說明如何使用腳本。</span><span class="sxs-lookup"><span data-stu-id="21de5-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="21de5-279">如果您想要在 Azure 中執行而不使用佇列，而且您已將變更設定為使用佇列在本機執行，請務必將 UseQueues appSetting 值設回 false，再繼續進行下列指示。</span><span class="sxs-lookup"><span data-stu-id="21de5-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="21de5-280">這些指示假設您已在本機下載並執行 Fix It 解決方案，而且您有 Azure 帳戶，或擁有您有權管理的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="21de5-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="21de5-281">安裝**Azure PowerShell**主控台。</span><span class="sxs-lookup"><span data-stu-id="21de5-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="21de5-282">如需指示，請參閱 [如何安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="21de5-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="21de5-283">此自訂的主控台已設定為可與您的 Azure 訂用帳戶搭配使用。</span><span class="sxs-lookup"><span data-stu-id="21de5-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="21de5-284">Azure 模組會安裝在*Program Files*目錄中，而且會在每次使用 Azure PowerShell 主控台時自動匯入。</span><span class="sxs-lookup"><span data-stu-id="21de5-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="21de5-285">如果您想要在不同的主機程式（例如 Windows PowerShell ISE）中工作，請務必使用[import-module](https://go.microsoft.com/fwlink/?LinkID=141553) Cmdlet 來匯入 azure 模組，或使用 azure 模組中的命令來觸發模組的自動匯入。</span><span class="sxs-lookup"><span data-stu-id="21de5-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="21de5-286">使用 [以**系統管理員身分執行**] 選項啟動 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="21de5-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="21de5-287">執行[ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) Cmdlet，將 Azure PowerShell 執行原則設定為 `RemoteSigned`。</span><span class="sxs-lookup"><span data-stu-id="21de5-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="21de5-288">輸入**Y** （為 [是]）來完成原則變更。</span><span class="sxs-lookup"><span data-stu-id="21de5-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="21de5-289">此設定可讓您執行未數位簽署的本機腳本。</span><span class="sxs-lookup"><span data-stu-id="21de5-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="21de5-290">（您也可以將執行原則設定為 `Unrestricted`，這樣就不需要在稍後解除封鎖步驟的需求，但基於安全性理由，不建議這樣做）。</span><span class="sxs-lookup"><span data-stu-id="21de5-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="21de5-291">執行 `Add-AzureAccount` Cmdlet，使用您帳戶的認證來設定 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="21de5-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="21de5-292">這些認證會在一段時間後到期，您必須重新執行 `Add-AzureAccount` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="21de5-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="21de5-293">在撰寫此電子書時，認證到期前的時間限制為12小時。</span><span class="sxs-lookup"><span data-stu-id="21de5-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="21de5-294">如果您有多個訂用帳戶，請使用 Set-azuresubscription Cmdlet 來指定您想要在其中建立測試環境的訂閱。</span><span class="sxs-lookup"><span data-stu-id="21de5-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="21de5-295">使用 `Get-AzurePublishSettingsFile` 和 `Import-AzurePublishSettingsFile` Cmdlet，匯入相同 Azure 訂用帳戶的管理憑證。</span><span class="sxs-lookup"><span data-stu-id="21de5-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="21de5-296">這些 Cmdlet 的第一個會下載憑證檔案，而在第二個檔案中，您可以指定該檔案的位置，以便匯入該檔案。</span><span class="sxs-lookup"><span data-stu-id="21de5-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="21de5-297">將下載的檔案保留在安全的位置，或在完成時將它刪除，因為它包含可用來管理 Azure 服務的憑證。</span><span class="sxs-lookup"><span data-stu-id="21de5-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="21de5-298">憑證用於偵測開發電腦的 IP 位址的 REST API 呼叫，以便在 SQL Database 伺服器上設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="21de5-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="21de5-299">執行[設定位置](https://go.microsoft.com/fwlink/p/?linkid=293912)Cmdlet （別名是 `cd`、`chdir`和 `sl`），以流覽至包含腳本的目錄。</span><span class="sxs-lookup"><span data-stu-id="21de5-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="21de5-300">（它們位於 [修正 It] 方案資料夾的 [*自動化*] 資料夾中）。如果有任何目錄名稱包含空格，請以引號括住路徑。</span><span class="sxs-lookup"><span data-stu-id="21de5-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="21de5-301">例如，若要流覽至 `c:\Sample Apps\FixIt\Automation` 目錄，您可以輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="21de5-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="21de5-302">若要允許 Windows PowerShell 執行這些腳本，請使用 [[解除封鎖-](https://go.microsoft.com/fwlink/p/?linkid=294021)檔案] Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="21de5-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="21de5-303">（腳本會遭到封鎖，因為它們是從網際網路下載）。</span><span class="sxs-lookup"><span data-stu-id="21de5-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="21de5-304">安全性-在任何腳本或可執行檔上執行 `Unblock-File` 之前，請在 [記事本] 中開啟檔案，檢查命令，並確認它們不包含任何惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="21de5-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="21de5-305">例如，下列命令會在目前目錄中的所有腳本上執行 `Unblock-File` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="21de5-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="21de5-306">若要建立基底的 web 應用程式（沒有佇列處理），請修正 It 應用程式，執行環境建立腳本。</span><span class="sxs-lookup"><span data-stu-id="21de5-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="21de5-307">必要的 `Name` 參數會指定資料庫的名稱，而且也會用於腳本所建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="21de5-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="21de5-308">此名稱在 azurewebsites.net 網域內必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="21de5-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="21de5-309">如果您指定的名稱不是唯一的，例如 Fixit 或 Test （或甚至在範例中為 fixitdemo），則 `New-AzureWebsite` Cmdlet 會失敗，並產生報告衝突的內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="21de5-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="21de5-310">腳本會將名稱轉換為所有小寫，以符合 web 應用程式、儲存體帳戶和資料庫的名稱需求。</span><span class="sxs-lookup"><span data-stu-id="21de5-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="21de5-311">必要的 `SqlDatabasePassword` 參數會指定將針對 SQL Database 建立之系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="21de5-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="21de5-312">請勿在密碼中包含特殊的 XML 字元（&amp; &lt; &gt;;)。</span><span class="sxs-lookup"><span data-stu-id="21de5-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="21de5-313">這是撰寫腳本的方式限制，而不是 Azure 的限制。</span><span class="sxs-lookup"><span data-stu-id="21de5-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="21de5-314">例如，如果您想要建立名為 "fixitdemo" 的 web 應用程式，並使用 "Passw0rd1" 的 SQL Server 系統管理員密碼，您可以輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="21de5-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="21de5-315">此名稱在 azurewebsites.net 網域中必須是唯一的，且密碼必須符合密碼複雜性 SQL Database 需求。</span><span class="sxs-lookup"><span data-stu-id="21de5-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="21de5-316">（範例 Passw0rd1 符合需求）。</span><span class="sxs-lookup"><span data-stu-id="21de5-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="21de5-317">請注意，命令的開頭是 "。\"。</span><span class="sxs-lookup"><span data-stu-id="21de5-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="21de5-318">為了協助防止惡意執行腳本，Windows PowerShell 會要求您在執行腳本時提供腳本檔案的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="21de5-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="21de5-319">您可以使用點來表示目前的目錄（"。\"）或提供完整路徑，例如：</span><span class="sxs-lookup"><span data-stu-id="21de5-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="21de5-320">如需腳本的詳細資訊，請使用 `Get-Help` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="21de5-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="21de5-321">您可以使用 Get-help Cmdlet 的 `Detailed`、`Full`、`Parameters`和 `Examples` 參數來篩選所傳回的說明。</span><span class="sxs-lookup"><span data-stu-id="21de5-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="21de5-322">如果腳本失敗或產生錯誤（例如「AzureWebsite： Call Set-azuresubscription 和 Select-Set-azuresubscription first」），您可能尚未完成 Azure PowerShell 的設定。</span><span class="sxs-lookup"><span data-stu-id="21de5-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="21de5-323">腳本完成之後，您可以使用 Azure 管理入口網站查看已建立的資源，如[自動化所有事項](automate-everything.md)一章所示。</span><span class="sxs-lookup"><span data-stu-id="21de5-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="21de5-324">若要將 FixIt 專案部署到新的 Azure 環境，請使用*AzureWebsite*腳本。</span><span class="sxs-lookup"><span data-stu-id="21de5-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="21de5-325">例如:</span><span class="sxs-lookup"><span data-stu-id="21de5-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="21de5-326">部署完成時，瀏覽器會開啟並修正在 Azure 中執行的問題。</span><span class="sxs-lookup"><span data-stu-id="21de5-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="21de5-327">疑難排解 Windows PowerShell 腳本</span><span class="sxs-lookup"><span data-stu-id="21de5-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="21de5-328">執行這些腳本時最常遇到的錯誤與許可權相關。</span><span class="sxs-lookup"><span data-stu-id="21de5-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="21de5-329">請確定 `Add-AzureAccount` 和 `Import-AzurePublishSettingsFile` 成功，而且您已將它們用於相同的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="21de5-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="21de5-330">即使 `Add-AzureAccount` 成功，您可能必須再次執行。</span><span class="sxs-lookup"><span data-stu-id="21de5-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="21de5-331">`Add-AzureAccount` 新增的許可權會在12小時內過期。</span><span class="sxs-lookup"><span data-stu-id="21de5-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="21de5-332">並未將物件參考設定為物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="21de5-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="21de5-333">如果腳本傳回錯誤，例如「物件參考未設定為物件的實例」，這表示 Windows PowerShell 找不到要處理的物件（這是 null 參考例外狀況），請執行 `Add-AzureAccount` Cmdlet，然後再試一次腳本。</span><span class="sxs-lookup"><span data-stu-id="21de5-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="21de5-334">InternalError：伺服器發生內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="21de5-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="21de5-335">當 azurewebsites.net 網域中的名稱不是唯一時，`New-AzureWebsite` Cmdlet 會傳回內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="21de5-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="21de5-336">若要解決此錯誤，請使用不同的名稱值，也就是*New-AzureWebsiteEnv*的 name 參數。</span><span class="sxs-lookup"><span data-stu-id="21de5-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="21de5-337">重新開機腳本</span><span class="sxs-lookup"><span data-stu-id="21de5-337">Restarting the script</span></span>

<span data-ttu-id="21de5-338">如果您需要重新開機*New-AzureWebsiteEnv*腳本，因為它在列印「腳本已完成」訊息之前失敗，您可能會想要刪除腳本停止之前所建立的資源。</span><span class="sxs-lookup"><span data-stu-id="21de5-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="21de5-339">例如，如果腳本已經建立 ContosoFixItDemo web 應用程式，而且您以相同的名稱再次執行腳本，腳本將會失敗，因為名稱正在使用中。</span><span class="sxs-lookup"><span data-stu-id="21de5-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="21de5-340">若要判斷腳本在停止之前所建立的資源，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="21de5-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="21de5-341">`Get-AzureSqlDatabase`：若要執行此 Cmdlet，請以管線將資料庫伺服器名稱傳送至 `Get-AzureSqlDatabase`： `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="21de5-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="21de5-342">若要刪除這些資源，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="21de5-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="21de5-343">請注意，如果您刪除資料庫伺服器，就會自動刪除與伺服器相關聯的資料庫。</span><span class="sxs-lookup"><span data-stu-id="21de5-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="21de5-344">如何將具有佇列處理的應用程式部署至 Azure App Service Web Apps 和 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="21de5-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="21de5-345">若要啟用佇列，請在 MyFixIt\Web.config 檔案中進行下列變更。</span><span class="sxs-lookup"><span data-stu-id="21de5-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="21de5-346">在 [`appSettings`] 底下，將 `UseQueues` 的值變更為 "true"：</span><span class="sxs-lookup"><span data-stu-id="21de5-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="21de5-347">然後在 Azure App Service 中，將 MVC 應用程式部署至 web 應用程式，如[先前](#deploybase)所述。</span><span class="sxs-lookup"><span data-stu-id="21de5-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="21de5-348">接下來，建立新的 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="21de5-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="21de5-349">Fix It 應用程式隨附的腳本不會建立或部署雲端服務，因此您必須為此使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="21de5-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="21de5-350">在入口網站中，按一下 **新增** -- **計算**–**雲端服務** -- **快速建立**，然後輸入 URL 和資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="21de5-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="21de5-351">使用您部署 web 應用程式所在的相同資料中心。</span><span class="sxs-lookup"><span data-stu-id="21de5-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="21de5-352">在您可以部署雲端服務之前，您必須先更新一些設定檔。</span><span class="sxs-lookup"><span data-stu-id="21de5-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="21de5-353">在 MyFixIt 中的 `connectionStrings`底下，將 `appdb` 連接字串的值取代為 SQL Database 的實際連接字串。</span><span class="sxs-lookup"><span data-stu-id="21de5-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="21de5-354">您可以從入口網站取得連接字串。</span><span class="sxs-lookup"><span data-stu-id="21de5-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="21de5-355">在入口網站中，按一下 [ **SQL 資料庫**] - **appdb** - **VIEW SQL Database ADO .net、ODBC、PHP 和 JDBC 的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="21de5-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="21de5-356">複製 ADO.NET 連接字串，並將值貼到 app.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="21de5-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="21de5-357">將「{您的\_密碼\_這裡}」取代為您的資料庫密碼。</span><span class="sxs-lookup"><span data-stu-id="21de5-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="21de5-358">（假設您使用腳本來部署 MVC 應用程式，您已在 `SqlDatabasePassword` 腳本參數中指定資料庫密碼）。</span><span class="sxs-lookup"><span data-stu-id="21de5-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="21de5-359">結果看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="21de5-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="21de5-360">在相同的 MyFixIt WorkerRole\app.config 檔案中，于 `appSettings`底下，取代 Azure 儲存體帳戶的兩個預留位置值。</span><span class="sxs-lookup"><span data-stu-id="21de5-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="21de5-361">您可以從入口網站取得存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="21de5-361">You can get the access key from the portal.</span></span> <span data-ttu-id="21de5-362">請參閱[如何管理儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="21de5-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="21de5-363">在 MyFixItCloudService\ServiceConfiguration.Cloud.cscfg 中，將 Azure 儲存體帳戶的兩個預留位置值取代為相同。</span><span class="sxs-lookup"><span data-stu-id="21de5-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="21de5-364">現在您已準備好部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="21de5-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="21de5-365">在 [方案探索] 中，以滑鼠右鍵按一下 MyFixItCloudService 專案，然後選取 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="21de5-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="21de5-366">如需詳細資訊，請參閱[本教學](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)課程的第2部分中的「將[應用程式部署到 Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)」。</span><span class="sxs-lookup"><span data-stu-id="21de5-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="21de5-367">上一篇</span><span class="sxs-lookup"><span data-stu-id="21de5-367">Previous</span></span>](more-patterns-and-guidance.md)
