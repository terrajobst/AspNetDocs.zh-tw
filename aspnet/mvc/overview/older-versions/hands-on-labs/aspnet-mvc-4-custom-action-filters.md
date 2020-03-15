---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 自訂動作篩選 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 會提供動作篩選準則，以便在呼叫動作方法之前或之後執行篩選邏輯。 動作篩選器是自訂屬性 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579692"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="0149e-104">ASP.NET MVC 4 自訂動作篩選</span><span class="sxs-lookup"><span data-stu-id="0149e-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="0149e-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="0149e-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="0149e-106">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="0149e-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="0149e-107">ASP.NET MVC 會提供動作篩選準則，以便在呼叫動作方法之前或之後執行篩選邏輯。</span><span class="sxs-lookup"><span data-stu-id="0149e-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="0149e-108">動作篩選器是自訂屬性，可提供宣告式方式，將動作前和動作後的行為新增至控制器的動作方法。</span><span class="sxs-lookup"><span data-stu-id="0149e-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="0149e-109">在這個實際操作的實驗室中，您將會在 MvcMusicStore 解決方案中建立自訂動作篩選屬性來攔截控制器的要求，並將網站的活動記錄到資料庫資料表中。</span><span class="sxs-lookup"><span data-stu-id="0149e-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="0149e-110">您可以藉由插入任何控制器或動作，將您的記錄篩選器新增至其中。</span><span class="sxs-lookup"><span data-stu-id="0149e-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="0149e-111">最後，您會看到記錄檔視圖，顯示訪客清單。</span><span class="sxs-lookup"><span data-stu-id="0149e-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="0149e-112">這個實際操作實驗室假設您有**ASP.NET MVC**的基本知識。</span><span class="sxs-lookup"><span data-stu-id="0149e-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="0149e-113">如果您之前未使用過**ASP.NET mvc** ，建議您移至**ASP.NET mvc 4 基礎**實際操作實驗室。</span><span class="sxs-lookup"><span data-stu-id="0149e-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="0149e-114">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可從[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="0149e-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="0149e-115">此實驗室的特定專案可在[ASP.NET MVC 4 自訂動作篩選](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)中取得。</span><span class="sxs-lookup"><span data-stu-id="0149e-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="0149e-116">目標</span><span class="sxs-lookup"><span data-stu-id="0149e-116">Objectives</span></span>

<span data-ttu-id="0149e-117">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="0149e-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="0149e-118">建立自訂動作篩選準則屬性以擴充篩選功能</span><span class="sxs-lookup"><span data-stu-id="0149e-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="0149e-119">藉由將自訂篩選屬性插入特定層級來套用</span><span class="sxs-lookup"><span data-stu-id="0149e-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="0149e-120">全域註冊自訂動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="0149e-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="0149e-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0149e-121">Prerequisites</span></span>

<span data-ttu-id="0149e-122">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="0149e-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="0149e-123">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。</span><span class="sxs-lookup"><span data-stu-id="0149e-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="0149e-124">安裝程式</span><span class="sxs-lookup"><span data-stu-id="0149e-124">Setup</span></span>

<span data-ttu-id="0149e-125">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="0149e-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="0149e-126">為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。</span><span class="sxs-lookup"><span data-stu-id="0149e-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="0149e-127">若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="0149e-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="0149e-128">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 C：使用程式碼片段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="0149e-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="0149e-129">練習</span><span class="sxs-lookup"><span data-stu-id="0149e-129">Exercises</span></span>

<span data-ttu-id="0149e-130">這個實際操作實驗室是由下列練習所組成：</span><span class="sxs-lookup"><span data-stu-id="0149e-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="0149e-131">練習1：記錄動作</span><span class="sxs-lookup"><span data-stu-id="0149e-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="0149e-132">練習2：管理多個動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="0149e-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="0149e-133">完成此實驗室的預估時間： **30 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="0149e-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="0149e-134">每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="0149e-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="0149e-135">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="0149e-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="0149e-136">練習1：記錄動作</span><span class="sxs-lookup"><span data-stu-id="0149e-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="0149e-137">在此練習中，您將瞭解如何使用 ASP.NET MVC 4 篩選器提供者來建立自訂動作記錄篩選器。</span><span class="sxs-lookup"><span data-stu-id="0149e-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="0149e-138">基於這個目的，您會將記錄篩選套用至 MusicStore 網站，以記錄所選控制器中的所有活動。</span><span class="sxs-lookup"><span data-stu-id="0149e-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="0149e-139">篩選會擴充**ActionFilterAttributeClass**並覆寫**OnActionExecuting**方法，以攔截每個要求，然後執行記錄動作。</span><span class="sxs-lookup"><span data-stu-id="0149e-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="0149e-140">ASP.NET MVC **ActionExecutingCoNtext**類別會提供有關 HTTP 要求、執行方法、結果和參數的內容資訊 **。**</span><span class="sxs-lookup"><span data-stu-id="0149e-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="0149e-141">ASP.NET MVC 4 也有預設的篩選器提供者，您可以使用，而不需要建立自訂篩選器。</span><span class="sxs-lookup"><span data-stu-id="0149e-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="0149e-142">ASP.NET MVC 4 提供下列類型的篩選準則：</span><span class="sxs-lookup"><span data-stu-id="0149e-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="0149e-143">**授權**篩選準則，它會針對是否執行動作方法進行安全性決策，例如執行驗證或驗證要求的屬性。</span><span class="sxs-lookup"><span data-stu-id="0149e-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="0149e-144">**動作**篩選準則，會包裝動作方法的執行。</span><span class="sxs-lookup"><span data-stu-id="0149e-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="0149e-145">此篩選可以執行額外的處理，例如將額外的資料提供給動作方法、檢查傳回值，或取消執行動作方法。</span><span class="sxs-lookup"><span data-stu-id="0149e-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="0149e-146">**結果**篩選準則，會包裝 ActionResult 物件的執行。</span><span class="sxs-lookup"><span data-stu-id="0149e-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="0149e-147">此篩選可以執行其他的結果處理，例如修改 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="0149e-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="0149e-148">**例外**狀況篩選準則，它會在動作方法中的某處擲回未處理的例外狀況時執行，從授權篩選準則開始，並以結果執行結束。</span><span class="sxs-lookup"><span data-stu-id="0149e-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="0149e-149">例外狀況篩選條件可以用於記錄或顯示錯誤頁面這類工作。</span><span class="sxs-lookup"><span data-stu-id="0149e-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="0149e-150">如需篩選器提供者的詳細資訊，請造訪此 MSDN 連結：（[https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="0149e-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="0149e-151">關於 MVC 音樂儲存應用程式記錄功能</span><span class="sxs-lookup"><span data-stu-id="0149e-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="0149e-152">此音樂存放區解決方案有一個新的資料模型資料表可供網站記錄**ActionLog**使用，其欄位如下：接收要求的控制器名稱，稱為「動作」、「用戶端 IP」和「時間戳記」。</span><span class="sxs-lookup"><span data-stu-id="0149e-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="0149e-153">![資料模型。ActionLog 資料表。](aspnet-mvc-4-custom-action-filters/_static/image1.png "資料模型。ActionLog 資料表。")</span><span class="sxs-lookup"><span data-stu-id="0149e-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="0149e-154">*資料模型-ActionLog 資料表*</span><span class="sxs-lookup"><span data-stu-id="0149e-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="0149e-155">解決方案會為動作記錄檔提供 ASP.NET 的 MVC 視圖，可在**MvcMusicStores/Views/ActionLog**找到：</span><span class="sxs-lookup"><span data-stu-id="0149e-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="0149e-156">![動作記錄檔視圖](aspnet-mvc-4-custom-action-filters/_static/image2.png "動作記錄檔視圖")</span><span class="sxs-lookup"><span data-stu-id="0149e-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="0149e-157">*動作記錄檔視圖*</span><span class="sxs-lookup"><span data-stu-id="0149e-157">*Action Log view*</span></span>

<span data-ttu-id="0149e-158">使用此指定的結構，所有工作都將著重于中斷控制器的要求，並使用自訂篩選來執行記錄。</span><span class="sxs-lookup"><span data-stu-id="0149e-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="0149e-159">工作 1-建立自訂篩選來攔截控制器的要求</span><span class="sxs-lookup"><span data-stu-id="0149e-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="0149e-160">在這項工作中，您將建立自訂篩選屬性類別，其中將包含記錄邏輯。</span><span class="sxs-lookup"><span data-stu-id="0149e-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="0149e-161">基於這個目的，您將擴充 ASP.NET MVC **actionfilterattribut**類別，並執行介面**IActionFilter**。</span><span class="sxs-lookup"><span data-stu-id="0149e-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="0149e-162">**Actionfilterattribut**是所有屬性篩選準則的基類。</span><span class="sxs-lookup"><span data-stu-id="0149e-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="0149e-163">它提供下列方法，以在執行控制器動作的前後執行特定邏輯：</span><span class="sxs-lookup"><span data-stu-id="0149e-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="0149e-164">**OnActionExecuting**（ActionExecutingCoNtext filterCoNtext）：在呼叫動作方法之前。</span><span class="sxs-lookup"><span data-stu-id="0149e-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="0149e-165">**OnActionExecuted**（ActionExecutedCoNtext filterCoNtext）：在呼叫動作方法之後，以及執行結果之前（view render 之前）。</span><span class="sxs-lookup"><span data-stu-id="0149e-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="0149e-166">**OnResultExecuting**（ResultExecutingCoNtext filterCoNtext）：緊接在執行結果之前（view render 之前）。</span><span class="sxs-lookup"><span data-stu-id="0149e-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="0149e-167">**OnResultExecuted**（ResultExecutedCoNtext filterCoNtext）：執行結果之後（呈現視圖之後）。</span><span class="sxs-lookup"><span data-stu-id="0149e-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="0149e-168">藉由將這些方法中的任何一項覆寫成衍生類別，您就可以執行自己的篩選程式代碼。</span><span class="sxs-lookup"><span data-stu-id="0149e-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>

1. <span data-ttu-id="0149e-169">開啟位於 **\Source\Ex01-LoggingActions\Begin**資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="0149e-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="0149e-170">在繼續之前，您必須先下載一些遺漏的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="0149e-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="0149e-171">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="0149e-172">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="0149e-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="0149e-173">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="0149e-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0149e-174">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="0149e-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0149e-175">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="0149e-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0149e-176">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="0149e-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="0149e-177">如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="0149e-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="0149e-178">將新類別C#新增至 [**篩選**] 資料夾，並將其命名為*CustomActionFilter.cs*。</span><span class="sxs-lookup"><span data-stu-id="0149e-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="0149e-179">這個資料夾會儲存所有的自訂篩選器。</span><span class="sxs-lookup"><span data-stu-id="0149e-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="0149e-180">開啟**CustomActionFilter.cs** ，並加入**system.web**和**MvcMusicStore**命名空間的參考：</span><span class="sxs-lookup"><span data-stu-id="0149e-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="0149e-181">（程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex1-CustomActionFilterNamespaces*）</span><span class="sxs-lookup"><span data-stu-id="0149e-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="0149e-182">從**actionfilterattribut**繼承**CustomActionFilter**類別，然後將**CustomActionFilter**類別實作為**IActionFilter**介面。</span><span class="sxs-lookup"><span data-stu-id="0149e-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="0149e-183">使**CustomActionFilter**類別覆寫方法**OnActionExecuting** ，並新增必要的邏輯以記錄篩選器的執行。</span><span class="sxs-lookup"><span data-stu-id="0149e-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="0149e-184">若要這樣做，請在**CustomActionFilter**類別內新增下列反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0149e-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="0149e-185">（程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex1-LoggingActions*）</span><span class="sxs-lookup"><span data-stu-id="0149e-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="0149e-186">**OnActionExecuting**方法使用**Entity Framework**新增新的 ActionLog 暫存器。</span><span class="sxs-lookup"><span data-stu-id="0149e-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="0149e-187">它會使用來自**filterCoNtext**的內容資訊，建立並填滿新的實體實例。</span><span class="sxs-lookup"><span data-stu-id="0149e-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="0149e-188">您可以在[msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)閱讀更多關於**ControllerCoNtext**類別的資訊。</span><span class="sxs-lookup"><span data-stu-id="0149e-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="0149e-189">工作 2-將程式碼攔截器插入存放控制器類別</span><span class="sxs-lookup"><span data-stu-id="0149e-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="0149e-190">在這項工作中，您會將自訂篩選器插入所有要記錄的控制器類別和控制器動作。</span><span class="sxs-lookup"><span data-stu-id="0149e-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="0149e-191">基於此練習的目的，存放區控制器類別會有一個記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0149e-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="0149e-192">從**ActionLogFilterAttribute**自訂篩選準則**OnActionExecuting**的方法會在呼叫插入的元素時執行。</span><span class="sxs-lookup"><span data-stu-id="0149e-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="0149e-193">也可以攔截特定的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="0149e-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="0149e-194">在**MvcMusicStore\Controllers**開啟**StoreController** ，並將參考新增至**篩選器**命名空間：</span><span class="sxs-lookup"><span data-stu-id="0149e-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="0149e-195">藉由在類別宣告之前加入 **[CustomActionFilter]** 屬性，將自訂篩選**CustomActionFilter**插入**StoreController**類別中。</span><span class="sxs-lookup"><span data-stu-id="0149e-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="0149e-196">當篩選器插入控制器類別時，其所有動作也會一併插入。</span><span class="sxs-lookup"><span data-stu-id="0149e-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="0149e-197">如果您只想要對一組動作套用篩選，就必須將 **[CustomActionFilter]** 插入其中每個動作：</span><span class="sxs-lookup"><span data-stu-id="0149e-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="0149e-198">工作 3-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="0149e-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="0149e-199">在這項工作中，您將測試記錄篩選是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="0149e-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="0149e-200">您將會啟動應用程式並造訪存放區，然後您會檢查已記錄的活動。</span><span class="sxs-lookup"><span data-stu-id="0149e-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="0149e-201">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0149e-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="0149e-202">流覽至 **/ActionLog**以查看記錄檔視圖的初始狀態：</span><span class="sxs-lookup"><span data-stu-id="0149e-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="0149e-203">![頁面活動前的記錄追蹤程式狀態](aspnet-mvc-4-custom-action-filters/_static/image3.png "頁面活動前的記錄追蹤程式狀態")</span><span class="sxs-lookup"><span data-stu-id="0149e-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="0149e-204">*頁面活動前的記錄追蹤程式狀態*</span><span class="sxs-lookup"><span data-stu-id="0149e-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="0149e-205">根據預設，它一律會顯示在抓取功能表的現有內容類型時所產生的一個專案。</span><span class="sxs-lookup"><span data-stu-id="0149e-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="0149e-206">為了簡單起見，我們會在每次應用程式執行時清除**ActionLog**資料表，因此它只會顯示每個特定工作的驗證記錄。</span><span class="sxs-lookup"><span data-stu-id="0149e-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="0149e-207">您可能需要從會話中移除下列程式碼 **\_Start**方法（在**global.asax**類別中），以便儲存在存放區控制器內執行之所有動作的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0149e-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="0149e-208">按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。</span><span class="sxs-lookup"><span data-stu-id="0149e-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="0149e-209">流覽至 **/ActionLog** ，如果記錄檔是空的，請按**F5**重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="0149e-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="0149e-210">檢查是否已追蹤您的造訪：</span><span class="sxs-lookup"><span data-stu-id="0149e-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="0149e-211">![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image4.png "已記錄活動的動作記錄")</span><span class="sxs-lookup"><span data-stu-id="0149e-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0149e-212">*已記錄活動的動作記錄*</span><span class="sxs-lookup"><span data-stu-id="0149e-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="0149e-213">練習2：管理多個動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="0149e-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="0149e-214">在此練習中，您會將第二個自訂動作篩選準則新增至 StoreController 類別，並定義執行這兩個篩選準則的特定順序。</span><span class="sxs-lookup"><span data-stu-id="0149e-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="0149e-215">接著，您將更新程式碼以全域註冊篩選。</span><span class="sxs-lookup"><span data-stu-id="0149e-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="0149e-216">定義篩選準則的執行順序時，有不同的選項要納入考慮。</span><span class="sxs-lookup"><span data-stu-id="0149e-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="0149e-217">例如，Order 屬性和篩選準則的範圍：</span><span class="sxs-lookup"><span data-stu-id="0149e-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="0149e-218">您可以定義每個篩選準則的**範圍**，例如，您可以將所有動作篩選準則的範圍設為在**控制器範圍**內執行，並將所有授權篩選準則設為在**全域範圍**中執行。</span><span class="sxs-lookup"><span data-stu-id="0149e-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="0149e-219">範圍具有已定義的執行順序。</span><span class="sxs-lookup"><span data-stu-id="0149e-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="0149e-220">此外，每個動作篩選準則都有一個 Order 屬性，用來判斷篩選準則範圍中的執行順序。</span><span class="sxs-lookup"><span data-stu-id="0149e-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="0149e-221">如需自訂動作篩選執行順序的詳細資訊，請造訪這篇 MSDN 文章：（[https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)）。</span><span class="sxs-lookup"><span data-stu-id="0149e-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="0149e-222">工作1：建立新的自訂動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="0149e-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="0149e-223">在這項工作中，您將建立新的自訂動作篩選器以插入 StoreController 類別，學習如何管理篩選的執行順序。</span><span class="sxs-lookup"><span data-stu-id="0149e-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="0149e-224">開啟位於 **\Source\Ex02-ManagingMultipleActionFilters\Begin**資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="0149e-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="0149e-225">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="0149e-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="0149e-226">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="0149e-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0149e-227">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="0149e-228">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="0149e-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="0149e-229">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="0149e-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0149e-230">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="0149e-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0149e-231">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="0149e-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0149e-232">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="0149e-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="0149e-233">如需詳細資訊，請參閱這篇文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="0149e-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="0149e-234">將新類別C#新增至**篩選器**資料夾，並將其命名為*MyNewCustomActionFilter.cs*</span><span class="sxs-lookup"><span data-stu-id="0149e-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="0149e-235">開啟**MyNewCustomActionFilter.cs** ，並加入**system.web**和**MvcMusicStore**命名空間的參考：</span><span class="sxs-lookup"><span data-stu-id="0149e-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="0149e-236">（程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex2-MyNewCustomActionFilterNamespaces*）</span><span class="sxs-lookup"><span data-stu-id="0149e-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="0149e-237">將預設類別宣告取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="0149e-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="0149e-238">（程式碼片段- *ASP.NET MVC 4 自訂動作篩選-Ex2-MyNewCustomActionFilterClass*）</span><span class="sxs-lookup"><span data-stu-id="0149e-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="0149e-239">此自訂動作篩選與您在上一個練習中建立的篩選幾乎相同。</span><span class="sxs-lookup"><span data-stu-id="0149e-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="0149e-240">主要差異在於它具有 *&quot;記錄的&quot;* 屬性已使用這個新類別的名稱更新，以識別哪一個篩選註冊了記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0149e-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="0149e-241">工作2：將新的程式碼攔截器插入 StoreController 類別</span><span class="sxs-lookup"><span data-stu-id="0149e-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="0149e-242">在這項工作中，您會將新的自訂篩選器新增至 StoreController 類別，並執行解決方案來確認兩個篩選準則如何搭配運作。</span><span class="sxs-lookup"><span data-stu-id="0149e-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="0149e-243">開啟位於**MvcMusicStore\Controllers**的**StoreController**類別，並將新的自訂篩選**MyNewCustomActionFilter**插入**StoreController**類別，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="0149e-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="0149e-244">現在，請執行應用程式，以查看這兩個自訂動作篩選準則的運作方式。</span><span class="sxs-lookup"><span data-stu-id="0149e-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="0149e-245">若要這麼做，請按**F5**並等候應用程式啟動。</span><span class="sxs-lookup"><span data-stu-id="0149e-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="0149e-246">流覽至 **/ActionLog**以查看記錄檔視圖的初始狀態。</span><span class="sxs-lookup"><span data-stu-id="0149e-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="0149e-247">![頁面活動前的記錄追蹤程式狀態](aspnet-mvc-4-custom-action-filters/_static/image5.png "頁面活動前的記錄追蹤程式狀態")</span><span class="sxs-lookup"><span data-stu-id="0149e-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="0149e-248">*頁面活動前的記錄追蹤程式狀態*</span><span class="sxs-lookup"><span data-stu-id="0149e-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="0149e-249">按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。</span><span class="sxs-lookup"><span data-stu-id="0149e-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="0149e-250">請檢查這次。您的造訪已追蹤兩次：一次針對您在**StorageController**類別中新增的每個自訂動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="0149e-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="0149e-251">![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image6.png "已記錄活動的動作記錄")</span><span class="sxs-lookup"><span data-stu-id="0149e-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0149e-252">*已記錄活動的動作記錄*</span><span class="sxs-lookup"><span data-stu-id="0149e-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="0149e-253">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="0149e-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="0149e-254">工作3：管理篩選順序</span><span class="sxs-lookup"><span data-stu-id="0149e-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="0149e-255">在這項工作中，您將瞭解如何使用 Order 屬性來管理篩選準則的執行順序。</span><span class="sxs-lookup"><span data-stu-id="0149e-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="0149e-256">開啟位於**MvcMusicStore\Controllers**的**StoreController**類別，並在這兩個篩選準則中指定**Order**屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0149e-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="0149e-257">現在，請根據訂單屬性的值，確認篩選準則的執行方式。</span><span class="sxs-lookup"><span data-stu-id="0149e-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="0149e-258">您會發現具有最小順序值（**CustomActionFilter**）的篩選是第一個執行的。</span><span class="sxs-lookup"><span data-stu-id="0149e-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="0149e-259">按**F5** ，並等候應用程式啟動。</span><span class="sxs-lookup"><span data-stu-id="0149e-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="0149e-260">流覽至 **/ActionLog**以查看記錄檔視圖的初始狀態。</span><span class="sxs-lookup"><span data-stu-id="0149e-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="0149e-261">![頁面活動前的記錄追蹤程式狀態](aspnet-mvc-4-custom-action-filters/_static/image7.png "頁面活動前的記錄追蹤程式狀態")</span><span class="sxs-lookup"><span data-stu-id="0149e-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="0149e-262">*頁面活動前的記錄追蹤程式狀態*</span><span class="sxs-lookup"><span data-stu-id="0149e-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="0149e-263">按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。</span><span class="sxs-lookup"><span data-stu-id="0149e-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="0149e-264">請檢查這次，您的造訪已依照篩選準則「順序值： **CustomActionFilter**記錄」進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="0149e-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="0149e-265">![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image8.png "已記錄活動的動作記錄")</span><span class="sxs-lookup"><span data-stu-id="0149e-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0149e-266">*已記錄活動的動作記錄*</span><span class="sxs-lookup"><span data-stu-id="0149e-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="0149e-267">現在，您將更新篩選準則的順序值，並確認記錄順序的變更方式。</span><span class="sxs-lookup"><span data-stu-id="0149e-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="0149e-268">在**StoreController**類別中，更新篩選準則的順序值，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0149e-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="0149e-269">按**F5**再次執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0149e-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="0149e-270">按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。</span><span class="sxs-lookup"><span data-stu-id="0149e-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="0149e-271">檢查這次， **MyNewCustomActionFilter**篩選器所建立的記錄會先出現。</span><span class="sxs-lookup"><span data-stu-id="0149e-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="0149e-272">![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image9.png "已記錄活動的動作記錄")</span><span class="sxs-lookup"><span data-stu-id="0149e-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0149e-273">*已記錄活動的動作記錄*</span><span class="sxs-lookup"><span data-stu-id="0149e-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="0149e-274">工作4：全域註冊篩選</span><span class="sxs-lookup"><span data-stu-id="0149e-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="0149e-275">在這項工作中，您將更新解決方案，將新的篩選器（**MyNewCustomActionFilter**）註冊為全域篩選器。</span><span class="sxs-lookup"><span data-stu-id="0149e-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="0149e-276">如此一來，就會由應用程式中執行的所有動作觸發，而不只是在上一個工作中的 StoreController。</span><span class="sxs-lookup"><span data-stu-id="0149e-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="0149e-277">在**StoreController**類別中，從 **[CustomActionFilter]** 移除 **[MyNewCustomActionFilter]** 屬性和 order 屬性。</span><span class="sxs-lookup"><span data-stu-id="0149e-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="0149e-278">它應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="0149e-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="0149e-279">開啟**global.asax**檔案，並找出**應用程式\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="0149e-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="0149e-280">請注意，應用程式每次啟動時，都會藉由呼叫**filterconfig.math**類別內的**RegisterGlobalFilters**方法，來註冊全域篩選器。</span><span class="sxs-lookup"><span data-stu-id="0149e-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="0149e-281">![在 global.asax 中註冊全域篩選器](aspnet-mvc-4-custom-action-filters/_static/image10.png "在 global.asax 中註冊全域篩選器")</span><span class="sxs-lookup"><span data-stu-id="0149e-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="0149e-282">*在 global.asax 中註冊全域篩選器*</span><span class="sxs-lookup"><span data-stu-id="0149e-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="0149e-283">在**App\_開始** 資料夾中開啟**FilterConfig.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="0149e-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="0149e-284">使用 System.object 新增的參考。使用 MvcMusicStore;命名空間.</span><span class="sxs-lookup"><span data-stu-id="0149e-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="0149e-285">更新**RegisterGlobalFilters**方法新增您的自訂篩選。</span><span class="sxs-lookup"><span data-stu-id="0149e-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="0149e-286">若要這麼做，請新增反白顯示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="0149e-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="0149e-287">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0149e-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="0149e-288">按一下功能表中的其中一個內容，**然後在其中**執行一些動作，例如流覽可用的專輯。</span><span class="sxs-lookup"><span data-stu-id="0149e-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="0149e-289">請檢查 **[MyNewCustomActionFilter]** 現在是否已插入 HomeController 和 ActionLogController。</span><span class="sxs-lookup"><span data-stu-id="0149e-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="0149e-290">![已記錄活動的動作記錄](aspnet-mvc-4-custom-action-filters/_static/image11.png "已記錄活動的動作記錄")</span><span class="sxs-lookup"><span data-stu-id="0149e-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="0149e-291">*已記錄全域活動的動作記錄*</span><span class="sxs-lookup"><span data-stu-id="0149e-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="0149e-292">此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="0149e-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="0149e-293">總結</span><span class="sxs-lookup"><span data-stu-id="0149e-293">Summary</span></span>

<span data-ttu-id="0149e-294">藉由完成此實際操作實驗室，您已瞭解如何擴充動作篩選準則來執行自訂動作。</span><span class="sxs-lookup"><span data-stu-id="0149e-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="0149e-295">您也已瞭解如何將任何篩選器插入頁面控制器。</span><span class="sxs-lookup"><span data-stu-id="0149e-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="0149e-296">使用的概念如下：</span><span class="sxs-lookup"><span data-stu-id="0149e-296">The following concepts were used:</span></span>

- <span data-ttu-id="0149e-297">如何使用 ASP.NET MVC Actionfilterattribut 類別建立自訂動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="0149e-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="0149e-298">如何將篩選器插入 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="0149e-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="0149e-299">如何使用 Order 屬性管理篩選順序</span><span class="sxs-lookup"><span data-stu-id="0149e-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="0149e-300">如何全域註冊篩選</span><span class="sxs-lookup"><span data-stu-id="0149e-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="0149e-301">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="0149e-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="0149e-302">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="0149e-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="0149e-303">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="0149e-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="0149e-304">移至 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="0149e-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="0149e-305">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="0149e-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="0149e-306">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-306">Click on **Install Now**.</span></span> <span data-ttu-id="0149e-307">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="0149e-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="0149e-308">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="0149e-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="0149e-309">![安裝 Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="0149e-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="0149e-310">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="0149e-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="0149e-311">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="0149e-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="0149e-313">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="0149e-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="0149e-314">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="0149e-314">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="0149e-316">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="0149e-316">*Installation progress*</span></span>
6. <span data-ttu-id="0149e-317">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="0149e-317">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="0149e-319">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="0149e-319">*Installation completed*</span></span>
7. <span data-ttu-id="0149e-320">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="0149e-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="0149e-321">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="0149e-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="0149e-323">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="0149e-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0149e-324">附錄 B：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="0149e-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="0149e-325">本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。</span><span class="sxs-lookup"><span data-stu-id="0149e-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="0149e-326">工作 1-從 Windows Azure 入口網站建立新的網站</span><span class="sxs-lookup"><span data-stu-id="0149e-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="0149e-327">移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="0149e-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0149e-328">有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。</span><span class="sxs-lookup"><span data-stu-id="0149e-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="0149e-329">您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。</span><span class="sxs-lookup"><span data-stu-id="0149e-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="0149e-330">![登入 Windows Azure 入口網站](aspnet-mvc-4-custom-action-filters/_static/image17.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="0149e-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="0149e-331">*登入 Windows Azure 管理入口網站*</span><span class="sxs-lookup"><span data-stu-id="0149e-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="0149e-332">按一下命令列上的 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="0149e-333">![建立新網站](aspnet-mvc-4-custom-action-filters/_static/image18.png "建立新網站")</span><span class="sxs-lookup"><span data-stu-id="0149e-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="0149e-334">*建立新網站*</span><span class="sxs-lookup"><span data-stu-id="0149e-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="0149e-335">按一下 [**計算** | 的**網站**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="0149e-336">然後選取 [**快速建立**] 選項。</span><span class="sxs-lookup"><span data-stu-id="0149e-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="0149e-337">提供新網站的可用 URL，然後按一下 [**建立網站**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0149e-338">Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。</span><span class="sxs-lookup"><span data-stu-id="0149e-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="0149e-339">[快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="0149e-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="0149e-340">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="0149e-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="0149e-341">![使用 [快速建立] 建立新的網站](aspnet-mvc-4-custom-action-filters/_static/image19.png "使用 [快速建立] 建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="0149e-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="0149e-342">*使用 [快速建立] 建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="0149e-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="0149e-343">等到新**網站**建立完畢。</span><span class="sxs-lookup"><span data-stu-id="0149e-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="0149e-344">建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。</span><span class="sxs-lookup"><span data-stu-id="0149e-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="0149e-345">檢查新網站是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="0149e-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="0149e-346">![流覽至新網站](aspnet-mvc-4-custom-action-filters/_static/image20.png "流覽至新網站")</span><span class="sxs-lookup"><span data-stu-id="0149e-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="0149e-347">*流覽至新網站*</span><span class="sxs-lookup"><span data-stu-id="0149e-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="0149e-348">![網站正在執行](aspnet-mvc-4-custom-action-filters/_static/image21.png "網站正在執行")</span><span class="sxs-lookup"><span data-stu-id="0149e-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="0149e-349">*網站正在執行*</span><span class="sxs-lookup"><span data-stu-id="0149e-349">*Web site running*</span></span>
6. <span data-ttu-id="0149e-350">返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。</span><span class="sxs-lookup"><span data-stu-id="0149e-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="0149e-351">![開啟網站管理頁面](aspnet-mvc-4-custom-action-filters/_static/image22.png "開啟網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="0149e-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="0149e-352">*開啟網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="0149e-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="0149e-353">在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。</span><span class="sxs-lookup"><span data-stu-id="0149e-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0149e-354">*發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。</span><span class="sxs-lookup"><span data-stu-id="0149e-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="0149e-355">發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="0149e-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="0149e-356">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="0149e-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="0149e-357">![正在下載網站發行設定檔](aspnet-mvc-4-custom-action-filters/_static/image23.png "正在下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="0149e-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="0149e-358">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="0149e-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="0149e-359">將發行設定檔下載到已知的位置。</span><span class="sxs-lookup"><span data-stu-id="0149e-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="0149e-360">在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="0149e-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="0149e-361">![儲存發行設定檔](aspnet-mvc-4-custom-action-filters/_static/image24.png "正在儲存發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="0149e-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="0149e-362">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="0149e-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="0149e-363">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="0149e-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="0149e-364">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0149e-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="0149e-365">如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="0149e-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="0149e-366">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="0149e-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="0149e-367">您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0149e-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="0149e-368">如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。</span><span class="sxs-lookup"><span data-stu-id="0149e-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="0149e-369">記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="0149e-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="0149e-370">請不要建立資料庫，因為它會在稍後的階段中建立。</span><span class="sxs-lookup"><span data-stu-id="0149e-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="0149e-371">![SQL Database Server 儀表板](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server 儀表板")</span><span class="sxs-lookup"><span data-stu-id="0149e-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="0149e-372">*SQL Database Server 儀表板*</span><span class="sxs-lookup"><span data-stu-id="0149e-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="0149e-373">在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0149e-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="0149e-374">若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](aspnet-mvc-4-custom-action-filters/_static/image26.png) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0149e-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![正在新增用戶端 IP 位址](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="0149e-376">*正在新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="0149e-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="0149e-377">將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="0149e-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="0149e-379">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="0149e-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0149e-380">工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="0149e-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="0149e-381">返回 ASP.NET MVC 4 解決方案。</span><span class="sxs-lookup"><span data-stu-id="0149e-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="0149e-382">在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。</span><span class="sxs-lookup"><span data-stu-id="0149e-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="0149e-383">![發行應用程式](aspnet-mvc-4-custom-action-filters/_static/image29.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="0149e-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="0149e-384">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="0149e-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="0149e-385">匯入您在第一個工作中儲存的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="0149e-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="0149e-386">![匯入發行設定檔](aspnet-mvc-4-custom-action-filters/_static/image30.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="0149e-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="0149e-387">*正在匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="0149e-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="0149e-388">按一下 [**驗證連接**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-388">Click **Validate Connection**.</span></span> <span data-ttu-id="0149e-389">驗證完成後，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="0149e-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0149e-390">當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。</span><span class="sxs-lookup"><span data-stu-id="0149e-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="0149e-391">![正在驗證連接](aspnet-mvc-4-custom-action-filters/_static/image31.png "正在驗證連接")</span><span class="sxs-lookup"><span data-stu-id="0149e-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="0149e-392">*正在驗證連接*</span><span class="sxs-lookup"><span data-stu-id="0149e-392">*Validating connection*</span></span>
4. <span data-ttu-id="0149e-393">在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="0149e-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="0149e-394">![Web deploy 設定](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy 設定")</span><span class="sxs-lookup"><span data-stu-id="0149e-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="0149e-395">*Web deploy 設定*</span><span class="sxs-lookup"><span data-stu-id="0149e-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="0149e-396">設定資料庫連接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0149e-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="0149e-397">在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="0149e-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="0149e-398">在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="0149e-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="0149e-399">在 [**密碼**] 中輸入您的伺服器管理員登入密碼。</span><span class="sxs-lookup"><span data-stu-id="0149e-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="0149e-400">輸入新的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="0149e-400">Type a new database name.</span></span>

     <span data-ttu-id="0149e-401">![正在設定目的地連接字串](aspnet-mvc-4-custom-action-filters/_static/image33.png "正在設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="0149e-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="0149e-402">*正在設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="0149e-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="0149e-403">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0149e-403">Then click **OK**.</span></span> <span data-ttu-id="0149e-404">當系統提示您建立資料庫時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="0149e-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="0149e-405">![建立資料庫](aspnet-mvc-4-custom-action-filters/_static/image34.png "建立資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="0149e-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="0149e-406">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="0149e-406">*Creating the database*</span></span>
7. <span data-ttu-id="0149e-407">您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="0149e-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="0149e-408">然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0149e-408">Then click **Next**.</span></span>

    <span data-ttu-id="0149e-409">![指向 SQL Database 的連接字串](aspnet-mvc-4-custom-action-filters/_static/image35.png "指向 SQL Database 的連接字串")</span><span class="sxs-lookup"><span data-stu-id="0149e-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="0149e-410">*指向 SQL Database 的連接字串*</span><span class="sxs-lookup"><span data-stu-id="0149e-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="0149e-411">在 [**預覽**] 頁面中，按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="0149e-412">![發行 web 應用程式](aspnet-mvc-4-custom-action-filters/_static/image36.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="0149e-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="0149e-413">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="0149e-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="0149e-414">發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="0149e-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="0149e-415">附錄 C：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="0149e-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="0149e-416">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="0149e-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="0149e-417">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="0149e-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="0149e-418">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-custom-action-filters/_static/image37.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="0149e-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="0149e-419">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="0149e-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="0149e-420">***若要使用鍵盤新增程式碼片段（C#僅限）***</span><span class="sxs-lookup"><span data-stu-id="0149e-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="0149e-421">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="0149e-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="0149e-422">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="0149e-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="0149e-423">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="0149e-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="0149e-424">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="0149e-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="0149e-425">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="0149e-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="0149e-426">![開始鍵入程式碼片段名稱](aspnet-mvc-4-custom-action-filters/_static/image38.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="0149e-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="0149e-427">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="0149e-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="0149e-428">![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-custom-action-filters/_static/image39.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="0149e-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="0149e-429">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="0149e-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="0149e-430">![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-custom-action-filters/_static/image40.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="0149e-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="0149e-431">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="0149e-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="0149e-432">***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1.</span><span class="sxs-lookup"><span data-stu-id="0149e-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="0149e-433">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="0149e-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="0149e-434">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="0149e-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="0149e-435">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="0149e-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="0149e-436">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-custom-action-filters/_static/image41.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="0149e-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="0149e-437">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="0149e-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="0149e-438">![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-custom-action-filters/_static/image42.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="0149e-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="0149e-439">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="0149e-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
