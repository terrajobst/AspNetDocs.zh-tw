---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: 使用 Visual Studio 2012 中的 Page Inspector |Microsoft Docs
author: rick-anderson
description: 在這個實際操作的實驗室中，您將探索新工具，以尋找並修正 Visual Studio 中的網頁問題-Page Inspector。 Page Inspector 是一種新工具，其為 b。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586251"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a><span data-ttu-id="43ea4-104">在 Visual Studio 2012 中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="43ea4-104">Using Page Inspector in Visual Studio 2012</span></span>

<span data-ttu-id="43ea4-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="43ea4-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="43ea4-106">在這個實際操作的實驗室中，您將探索新工具，以尋找並修正 Visual Studio 中的網頁問題-Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="43ea4-106">In this Hands-on Lab, you will discover a new tool to find and fix web page issues in Visual Studio - the Page Inspector.</span></span>
> 
> <span data-ttu-id="43ea4-107">Page Inspector 是新工具，可將瀏覽器診斷工具帶入 Visual Studio，並在瀏覽器、ASP.NET 和原始程式碼之間提供整合的體驗。</span><span class="sxs-lookup"><span data-stu-id="43ea4-107">Page Inspector is a new tool that brings browser diagnostics tools to Visual Studio and provides an integrated experience among the browser, ASP.NET, and source code.</span></span> <span data-ttu-id="43ea4-108">它會直接在 Visual Studio IDE 內呈現網頁（HTML、Web form、ASP.NET MVC 或網頁），並讓您檢查原始程式碼和所產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="43ea4-108">It renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) directly within the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="43ea4-109">Page Inspector 可讓您輕鬆地分解網站、快速從頭開始建立頁面，並快速診斷問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-109">Page Inspector enables you to easily decompose a website, rapidly build pages from the ground up, and quickly diagnose issues.</span></span>
> 
> <span data-ttu-id="43ea4-110">現今我們有一些 Web 架構，可即時建立彈性且可調整的網站，例如 ASP.NET MVC 和 WebForms。</span><span class="sxs-lookup"><span data-stu-id="43ea4-110">Nowadays we have a number of Web frameworks that create flexible and scalable websites in a timely manner, such as ASP.NET MVC and WebForms.</span></span> <span data-ttu-id="43ea4-111">另一方面，因為 IDE 不支援以範本為基礎的頁面和動態內容中的設計工具，所以在頁面上找出問題會比較困難。</span><span class="sxs-lookup"><span data-stu-id="43ea4-111">On the other hand, it gets harder to find issues on the pages because the IDE does not support the designer view in template-based pages and dynamic content.</span></span> <span data-ttu-id="43ea4-112">因此，這些網站必須在瀏覽器中開啟，才能查看他們對使用者的外觀。</span><span class="sxs-lookup"><span data-stu-id="43ea4-112">Therefore, these websites have to be opened in a browser to see how they appear to a user.</span></span>
> 
> <span data-ttu-id="43ea4-113">Web 開發人員使用外部工具來尋找在瀏覽器中定期執行的問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-113">Web developers use external tools to find issues that regularly run in the browser.</span></span> <span data-ttu-id="43ea4-114">然後，它們會回到 IDE 並開始修正。</span><span class="sxs-lookup"><span data-stu-id="43ea4-114">Then, they return to the IDE and start fixing.</span></span> <span data-ttu-id="43ea4-115">在 IDE 之間來回活動的瀏覽器和程式碼剖析工具可能沒有效率，而且有時候每次您想要重現問題時，都需要全新的部署和快取清理。</span><span class="sxs-lookup"><span data-stu-id="43ea4-115">This back and forth activity among the IDE, the browser and the profiling tools can be inefficient, and sometimes requires a fresh deployment and cache cleaning each time you want to reproduce an issue.</span></span>
> 
> <span data-ttu-id="43ea4-116">Page Inspector 在用戶端（瀏覽器工具）與伺服器（ASP.NET 和原始程式碼）之間建立 Web 開發的橋樑，方法是使用結合的一組功能結合兩個世界的優勢。</span><span class="sxs-lookup"><span data-stu-id="43ea4-116">Page Inspector bridges a gap in Web development between the client (browser tools) and the server (ASP.NET and source code) by bringing together the best of both worlds using a combined set of features.</span></span>
> 
> <span data-ttu-id="43ea4-117">使用 Page Inspector，您可以查看原始程式檔（包括伺服器端程式碼）中的哪些元素產生要在瀏覽器中轉譯的 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-117">Using Page Inspector, you can see which elements in the source files (including server-side code) have produced the HTML markup to be rendered in the browser.</span></span> <span data-ttu-id="43ea4-118">Page Inspector 也可讓您修改 CSS 屬性和 DOM 元素屬性，以查看立即反映在瀏覽器中的變更。</span><span class="sxs-lookup"><span data-stu-id="43ea4-118">Page Inspector also lets you modify CSS properties and DOM element attributes to see the changes reflected immediately in the browser.</span></span>
> 
> <span data-ttu-id="43ea4-119">這個實際操作實驗室將逐步引導您完成 Page Inspector 的功能，並示範如何使用它們來修正 Web 應用程式中的問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-119">This hands-on lab will walk you through the Page Inspector features and show you how you can use them to fix issues in Web applications.</span></span> <span data-ttu-id="43ea4-120">**此實驗室包含兩個使用類似流程但以不同技術為目標的練習。如果您是 ASP.NET MVC 開發人員，請遵循練習一，如果您是 WebForms 開發人員，請遵循練習二**。</span><span class="sxs-lookup"><span data-stu-id="43ea4-120">**This lab contains two exercises using similar flows but targeting different technologies. If you are an ASP.NET MVC Developer, follow exercise one; if you are a WebForms developer follow exercise two**.</span></span>
> 
> <span data-ttu-id="43ea4-121">本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="43ea4-121">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="43ea4-122">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)取得。</span><span class="sxs-lookup"><span data-stu-id="43ea4-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="43ea4-123">目標</span><span class="sxs-lookup"><span data-stu-id="43ea4-123">Objectives</span></span>

<span data-ttu-id="43ea4-124">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="43ea4-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="43ea4-125">使用 Page Inspector 分解網站</span><span class="sxs-lookup"><span data-stu-id="43ea4-125">Decompose a Web Site using Page Inspector</span></span>
- <span data-ttu-id="43ea4-126">使用 Page Inspector 檢查和預覽 CSS 樣式變更</span><span class="sxs-lookup"><span data-stu-id="43ea4-126">Inspect and preview CSS styles changes with Page Inspector</span></span>
- <span data-ttu-id="43ea4-127">使用 Page Inspector 偵測並修正網頁中的問題</span><span class="sxs-lookup"><span data-stu-id="43ea4-127">Detect and fix issues in your web pages using Page Inspector</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="43ea4-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43ea4-128">Prerequisites</span></span>

<span data-ttu-id="43ea4-129">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="43ea4-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="43ea4-130">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。</span><span class="sxs-lookup"><span data-stu-id="43ea4-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="43ea4-131">Internet Explorer 9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="43ea4-131">Internet Explorer 9 or higher</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="43ea4-132">練習</span><span class="sxs-lookup"><span data-stu-id="43ea4-132">Exercises</span></span>

<span data-ttu-id="43ea4-133">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="43ea4-133">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="43ea4-134">練習1：在 ASP.NET MVC 專案中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="43ea4-134">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>](#Exercise1)
2. [<span data-ttu-id="43ea4-135">練習2：在 WebForms 專案中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="43ea4-135">Exercise 2: Using Page Inspector in WebForms Projects</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="43ea4-136">每個練習都附有一個起始解決方案，此方案位於練習的 [開始] 資料夾中，可讓您個別追蹤每個練習。</span><span class="sxs-lookup"><span data-stu-id="43ea4-136">Each exercise is accompanied by a starting solution, located in the Begin folder of the exercise, that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="43ea4-137">在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的結束資料夾，其中含有完成對應練習中步驟所產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-137">Inside the source code for an exercise, you will also find an End folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="43ea4-138">如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。</span><span class="sxs-lookup"><span data-stu-id="43ea4-138">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

<span data-ttu-id="43ea4-139">完成此實驗室的預估時間： **30 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="43ea4-139">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a><span data-ttu-id="43ea4-140">練習1：在 ASP.NET MVC 專案中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="43ea4-140">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>

<span data-ttu-id="43ea4-141">在此練習中，您將瞭解如何使用**Page Inspector**來預覽和 DEBUG **ASP.NET MVC 4**解決方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-141">In this exercise, you will learn how to preview and debug an **ASP.NET MVC 4** solution using **Page Inspector**.</span></span> <span data-ttu-id="43ea4-142">首先，您將會在工具周圍執行簡短的膝上，以瞭解有助於 Web 偵錯工具的功能。</span><span class="sxs-lookup"><span data-stu-id="43ea4-142">First, you will perform a brief lap around the tool to learn the features that facilitate the Web debugging process.</span></span> <span data-ttu-id="43ea4-143">然後，您將會在包含樣式問題的網頁中工作。</span><span class="sxs-lookup"><span data-stu-id="43ea4-143">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="43ea4-144">您將瞭解如何使用 Page Inspector 來尋找產生問題的原始程式碼並加以修正。</span><span class="sxs-lookup"><span data-stu-id="43ea4-144">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="43ea4-145">工作 1-探索 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="43ea4-145">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="43ea4-146">在這項工作中，您將瞭解如何在顯示相片圖庫的 ASP.NET MVC 4 專案內容中使用 Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="43ea4-146">In this task, you will learn how to use the Page Inspector in the context of an ASP.NET MVC 4 project that shows a photo gallery.</span></span>

1. <span data-ttu-id="43ea4-147">開啟位於**來源/Ex1-MVC4/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-147">Open the **Begin** solution located at **Source/Ex1-MVC4/Begin/** folder.</span></span>

   1. <span data-ttu-id="43ea4-148">在繼續之前，您必須先下載一些遺漏的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="43ea4-148">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="43ea4-149">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="43ea4-149">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="43ea4-150">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="43ea4-150">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="43ea4-151">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-151">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="43ea4-152">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="43ea4-152">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="43ea4-153">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="43ea4-153">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="43ea4-154">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="43ea4-154">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="43ea4-155">在 方案總管中，尋找 **/Views/Home**專案資料夾底下的  **Index. cshtml** ，以滑鼠右鍵按一下它，然後**在 Page Inspector 中**選取 view。</span><span class="sxs-lookup"><span data-stu-id="43ea4-155">In the Solution Explorer, locate **Index.cshtml** view under the **/Views/Home** project folder, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="43ea4-156">![在 Page Inspector 中選取要預覽的檔案](using-page-inspector-in-visual-studio-2012/_static/image1.png "在 Page Inspector 中選取要預覽的檔案")</span><span class="sxs-lookup"><span data-stu-id="43ea4-156">![Selecting a file to preview in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "Selecting a file to preview in Page Inspector")</span></span>

    <span data-ttu-id="43ea4-157">*在 Page Inspector 中選取要預覽的檔案*</span><span class="sxs-lookup"><span data-stu-id="43ea4-157">*Selecting a file to preview in Page Inspector*</span></span>
3. <span data-ttu-id="43ea4-158">[Page Inspector] 視窗會顯示對應至您所選取之來源視圖的 */Home/Index* URL。</span><span class="sxs-lookup"><span data-stu-id="43ea4-158">The Page Inspector window will show the */Home/Index* URL mapped to the source View you selected.</span></span>

    ![第一個使用 PageInspector 的連絡人](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    <span data-ttu-id="43ea4-160">*第一個與 Page Inspector 的連絡人*</span><span class="sxs-lookup"><span data-stu-id="43ea4-160">*The first contact with Page Inspector*</span></span>

    <span data-ttu-id="43ea4-161">Page Inspector 工具已整合到您的 Visual Studio 環境中。</span><span class="sxs-lookup"><span data-stu-id="43ea4-161">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="43ea4-162">偵測器包含一個內嵌的瀏覽器，以及強大的 HTML profiler。</span><span class="sxs-lookup"><span data-stu-id="43ea4-162">The inspector contains an embedded browser, together with a powerful HTML profiler.</span></span> <span data-ttu-id="43ea4-163">請注意，您不需要執行解決方案來查看頁面的外觀。</span><span class="sxs-lookup"><span data-stu-id="43ea4-163">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-164">當 Page Inspector 瀏覽器的寬度小於已開啟頁面的寬度時，您將不會正確地看到此頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-164">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="43ea4-165">如果發生這種情況，請調整 Page Inspector 的寬度。</span><span class="sxs-lookup"><span data-stu-id="43ea4-165">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="43ea4-166">按一下 Page Inspector**中的 [** 檔案] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-166">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="43ea4-167">您會看到組成索引頁的所有原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="43ea4-167">You will see all the source files that are composing the Index page.</span></span> <span data-ttu-id="43ea4-168">這項功能有助於一眼地識別所有元素，特別是當您使用部分視圖和範本時。</span><span class="sxs-lookup"><span data-stu-id="43ea4-168">This feature helps to identify all the elements at a glance, especially when you are working with partial views and templates.</span></span> <span data-ttu-id="43ea4-169">請注意，如果您按一下連結，也可以開啟每個檔案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-169">Notice that you can also open each of the files if you click the links.</span></span>

    ![-Files-索引標籤](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    <span data-ttu-id="43ea4-171">*[檔案] 索引標籤*</span><span class="sxs-lookup"><span data-stu-id="43ea4-171">*The Files tab*</span></span>
5. <span data-ttu-id="43ea4-172">按一下位於索引標籤左側的**切換檢查模式** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="43ea4-172">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="43ea4-173">這項工具可讓您選取頁面的任何元素，並查看其 HTML 和 Razor 程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-173">This tool will let you select any element of the page and see its HTML and Razor code.</span></span>

    ![切換-檢查模式-按鈕](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    <span data-ttu-id="43ea4-175">*切換檢查模式按鈕*</span><span class="sxs-lookup"><span data-stu-id="43ea4-175">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="43ea4-176">在 Page Inspector 瀏覽器中，將滑鼠指標移到頁面元素上方。</span><span class="sxs-lookup"><span data-stu-id="43ea4-176">In the Page Inspector browser, move the mouse pointer over the page elements.</span></span> <span data-ttu-id="43ea4-177">當您將滑鼠指標移到所呈現頁面的任何部分上方時，會顯示專案類型，並在 [Visual Studio 編輯器] 中反白顯示對應的來源標記或程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-177">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    ![作用中的檢查模式](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    <span data-ttu-id="43ea4-179">*作用中的檢查模式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-179">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-180">請勿將 [Page Inspector] 視窗最大化，否則您將無法看到顯示原始程式碼的 [預覽] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-180">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="43ea4-181">如果您在 Page Inspector 中按一下最大化的專案，將會出現選取範圍的原始程式碼，但會隱藏 [Page Inspector] 視窗。</span><span class="sxs-lookup"><span data-stu-id="43ea4-181">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="43ea4-182">如果您注意到**Index. cshtml**檔案，就會注意到產生所選項目的原始程式碼部分會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="43ea4-182">If you pay attention to the **Index.cshtml** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="43ea4-183">這項功能可協助編輯較長的原始程式檔，以提供直接且快速的方式來存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-183">This feature facilitates the editing of long source files, providing a direct and fast way to access the code.</span></span>

    ![檢查元素](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    <span data-ttu-id="43ea4-185">*檢查元素*</span><span class="sxs-lookup"><span data-stu-id="43ea4-185">*Inspecting elements*</span></span>
7. <span data-ttu-id="43ea4-186">按一下 [**切換檢查模式**] 按鈕（![選取 [html] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 html 程式碼。](using-page-inspector-in-visual-studio-2012/_static/image7.png "選取 [HTML] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 HTML 程式碼。")</span><span class="sxs-lookup"><span data-stu-id="43ea4-186">Click the **Toggle Inspection Mode** button (![Select the HTML tab to display the HTML code rendered in the Page Inspector browser.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Select the HTML tab to display the HTML code rendered in the Page Inspector browser.")</span></span> <span data-ttu-id="43ea4-187">）以停用游標。</span><span class="sxs-lookup"><span data-stu-id="43ea4-187">) to disable the cursor.</span></span>
8. <span data-ttu-id="43ea4-188">選取 [ **html** ] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 html 程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-188">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="43ea4-189">在 HTML 標籤中，找出具有 Koala 連結的清單專案，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="43ea4-189">In the HTML markup, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="43ea4-190">請注意，當您選取程式碼時，會在瀏覽器中自動反白顯示對應的輸出。</span><span class="sxs-lookup"><span data-stu-id="43ea4-190">Notice that when you select the code, the corresponding output is automatically highlighted in the browser.</span></span> <span data-ttu-id="43ea4-191">這項功能非常適合用來查看 HTML 區塊在頁面上的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-191">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="43ea4-192">![選取頁面中的 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image8.png "選取頁面中的 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="43ea4-192">![Selecting HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image8.png "Selecting HTML element in the page")</span></span>

    <span data-ttu-id="43ea4-193">*選取頁面中的 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="43ea4-193">*Selecting HTML element in the page*</span></span>
10. <span data-ttu-id="43ea4-194">按一下 [**切換檢查模式**] 按鈕以啟用*檢查模式*，然後按一下巡覽列。</span><span class="sxs-lookup"><span data-stu-id="43ea4-194">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="43ea4-195">在 HTML 程式碼右邊的 [樣式] 窗格中，您會看到一份清單，其中包含套用至所選元素的 CSS 樣式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-195">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-196">由於標頭是網站配置的一部分，因此 Page Inspector 也會開啟 \_配置的 cshtml 檔案，並反白顯示受影響的程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="43ea4-196">Since the header is a part of the site layout, Page Inspector will also open \_Layout.cshtml file and highlight the segment of code affected.</span></span>

    ![探索樣式](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    <span data-ttu-id="43ea4-198">*探索所選元素的樣式和原始檔*</span><span class="sxs-lookup"><span data-stu-id="43ea4-198">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="43ea4-199">啟用切換檢查指標後，將滑鼠指標移到藍色的功能列下方，然後按一下半圓。</span><span class="sxs-lookup"><span data-stu-id="43ea4-199">With the toggle inspection pointer enabled, move the mouse pointer below the blue featured bar and click the half circle.</span></span>

    <span data-ttu-id="43ea4-200">![選取元素](using-page-inspector-in-visual-studio-2012/_static/image10.png "選取元素")</span><span class="sxs-lookup"><span data-stu-id="43ea4-200">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image10.png "Selecting an element")</span></span>

    <span data-ttu-id="43ea4-201">*選取元素*</span><span class="sxs-lookup"><span data-stu-id="43ea4-201">*Selecting an element*</span></span>
12. <span data-ttu-id="43ea4-202">在 [樣式] 窗格中，找出 [**主要-內容**] 群組底下的 [**背景影像**] 專案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-202">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="43ea4-203">**取消** **核取背景影像**，並查看發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="43ea4-203">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="43ea4-204">您會注意到，瀏覽器會立即反映變更，並隱藏圓形。</span><span class="sxs-lookup"><span data-stu-id="43ea4-204">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-205">您在 [Page Inspector 樣式] 索引標籤上套用的變更不會影響原始樣式表單。</span><span class="sxs-lookup"><span data-stu-id="43ea4-205">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="43ea4-206">您可以視需要取消核取樣式或變更其值，但它們會在重新整理頁面之後還原。</span><span class="sxs-lookup"><span data-stu-id="43ea4-206">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="43ea4-207">![啟用和停用 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image11.png "啟用和停用 CSS 樣式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-207">![Enabling and disabling CSS styles](using-page-inspector-in-visual-studio-2012/_static/image11.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="43ea4-208">*啟用和停用 CSS 樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-208">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="43ea4-209">現在，使用 [檢查] 模式按一下標頭上的 [**這裡的標誌**] 文字。</span><span class="sxs-lookup"><span data-stu-id="43ea4-209">Now, click the '**your logo here**' text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="43ea4-210">在 [**樣式**] 索引標籤中，找出 [**網站-標題**] 群組底下的 [**字型大小**] CSS 屬性。</span><span class="sxs-lookup"><span data-stu-id="43ea4-210">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="43ea4-211">按兩下屬性值，並以**3 個 em**取代 2.3 em 值，然後按**enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="43ea4-211">Double-click the attribute value and replace the 2.3 em value with **3 em**, and then press **ENTER**.</span></span> <span data-ttu-id="43ea4-212">請注意，標題看起來更大。</span><span class="sxs-lookup"><span data-stu-id="43ea4-212">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="43ea4-213">![變更 Page Inspector 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image12.png "變更 Page Inspector 中的 CSS 值")</span><span class="sxs-lookup"><span data-stu-id="43ea4-213">![Changing CSS values in the Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image12.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="43ea4-214">*變更 Page Inspector 中的 CSS 值*</span><span class="sxs-lookup"><span data-stu-id="43ea4-214">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="43ea4-215">按一下位於 Page Inspector 右窗格中的 [**追蹤樣式**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-215">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="43ea4-216">這是一種替代方式，可查看套用至選取專案的所有樣式（依屬性名稱排序）。</span><span class="sxs-lookup"><span data-stu-id="43ea4-216">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    ![CSS 樣式追蹤](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    <span data-ttu-id="43ea4-218">*追蹤所選元素的 CSS 樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-218">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="43ea4-219">Page Inspector 的另一項功能是 [版面配置] 窗格。</span><span class="sxs-lookup"><span data-stu-id="43ea4-219">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="43ea4-220">使用 [檢查] 模式，選取巡覽列，然後按一下右窗格中**的 [配置**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-220">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="43ea4-221">您會看到所選元素的確切大小，以及其位移、邊界、填補和框線大小。</span><span class="sxs-lookup"><span data-stu-id="43ea4-221">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="43ea4-222">請注意，您也可以從這個視圖中修改值。</span><span class="sxs-lookup"><span data-stu-id="43ea4-222">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="43ea4-223">![Page Inspector 中的元素版面配置](using-page-inspector-in-visual-studio-2012/_static/image14.png "Page Inspector 中的元素版面配置")</span><span class="sxs-lookup"><span data-stu-id="43ea4-223">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image14.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="43ea4-224">*Page Inspector 中的元素版面配置*</span><span class="sxs-lookup"><span data-stu-id="43ea4-224">*Element layout in Page Inspector*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="43ea4-225">工作 2-在相片圖庫中尋找和修正樣式問題</span><span class="sxs-lookup"><span data-stu-id="43ea4-225">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="43ea4-226">您要如何診斷舊版 Visual Studio 的網頁問題？</span><span class="sxs-lookup"><span data-stu-id="43ea4-226">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="43ea4-227">您很可能熟悉在 Visual Studio IDE 外部執行的 web 偵錯工具，例如 Internet Explorer 開發人員工具或 Firebug。</span><span class="sxs-lookup"><span data-stu-id="43ea4-227">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="43ea4-228">瀏覽器只會瞭解 HTML、腳本和樣式，而基礎架構則會產生要轉譯的 HTML。</span><span class="sxs-lookup"><span data-stu-id="43ea4-228">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="43ea4-229">基於這個理由，您通常需要部署整個網站，以查看網頁的外觀。</span><span class="sxs-lookup"><span data-stu-id="43ea4-229">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="43ea4-230">當您想要在網站中偵測並修正問題時，您可能會遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="43ea4-230">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="43ea4-231">從 Visual Studio 執行解決方案，或在 web 伺服器上部署頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-231">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="43ea4-232">在瀏覽器中，開啟您使用的開發人員工具，或直接開啟原始程式碼和樣式，並嘗試符合問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-232">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="43ea4-233">若要尋找相關的檔案，您可以使用 [&quot;搜尋]&quot; 或 &quot;在 [檔案]&quot; [功能] 中，以樣式類別的名稱進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="43ea4-233">To find the files involved, you would have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="43ea4-234">一旦偵測到錯誤，請停止網頁瀏覽器和伺服器。</span><span class="sxs-lookup"><span data-stu-id="43ea4-234">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="43ea4-235">清除瀏覽器快取。</span><span class="sxs-lookup"><span data-stu-id="43ea4-235">Clear the browser cache.</span></span>
5. <span data-ttu-id="43ea4-236">回到 Visual Studio 以套用修正程式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-236">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="43ea4-237">重複所有要測試的步驟。</span><span class="sxs-lookup"><span data-stu-id="43ea4-237">Repeat all the steps to test.</span></span>

<span data-ttu-id="43ea4-238">由於 ASP.NET MVC 4 中沒有實際的 WYSIWYG，因此在執行或部署 web 應用程式之後，大部分的樣式問題都會在稍後的階段中偵測到。</span><span class="sxs-lookup"><span data-stu-id="43ea4-238">As there is no real WYSIWYG in ASP.NET MVC 4, most of the style issues are detected on a later stage, after running or deploying the web application.</span></span> <span data-ttu-id="43ea4-239">現在，有了 Page Inspector，就可以預覽任何頁面，而不需要執行解決方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-239">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="43ea4-240">在這項工作中，您將使用 Page inspector 並修正相片圖庫應用程式的某些問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-240">In this task, you will use the Page inspector and fix some issues the Photo Gallery application.</span></span>

1. <span data-ttu-id="43ea4-241">使用 Page Inspector，找出標頭左邊的**註冊**和**登入**連結。</span><span class="sxs-lookup"><span data-stu-id="43ea4-241">Using Page Inspector, locate the **Register** and the **Log in** links at the left side of the header.</span></span>

    <span data-ttu-id="43ea4-242">請注意，連結不會顯示在右邊的預期位置，而且會顯示為項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="43ea4-242">Notice that the links are not displayed at the expected place on the right, and they are shown like a bulleted list.</span></span> <span data-ttu-id="43ea4-243">您現在會將連結向右對齊，並據以調整其樣式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-243">You will now align the links to the right and restyle them accordingly.</span></span>

    <span data-ttu-id="43ea4-244">![尋找註冊和登入連結](using-page-inspector-in-visual-studio-2012/_static/image15.png "尋找註冊和登入連結")</span><span class="sxs-lookup"><span data-stu-id="43ea4-244">![Locating the Register and Log in links](using-page-inspector-in-visual-studio-2012/_static/image15.png "Locating the Register and Log in links")</span></span>

    <span data-ttu-id="43ea4-245">*尋找註冊和登入連結*</span><span class="sxs-lookup"><span data-stu-id="43ea4-245">*Locating the Register and Log in links*</span></span>
2. <span data-ttu-id="43ea4-246">選取 [切換檢查模式] 時，按一下 [註冊] 連結以開啟其程式碼，然後按一下 [關閉]，但不是 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="43ea4-246">With Toggle Inspection Mode selected, click close to, but not on, the Register link to open its code.</span></span>

    <span data-ttu-id="43ea4-247">請注意，連結的原始程式碼位於 **\_loginpartial.html. cshtml**檔案中，而不是 \_的 Layout，也就是您可能會在第一次尋找的位置。</span><span class="sxs-lookup"><span data-stu-id="43ea4-247">Notice that the source code of the links is located in the **\_LoginPartial.cshtml** file, not the Index.cshtml nor the \_Layout.cshtml, which are the places you might look in first place.</span></span> <span data-ttu-id="43ea4-248">您已直接放在正確的來源檔案中。</span><span class="sxs-lookup"><span data-stu-id="43ea4-248">You have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="43ea4-249">在 **樣式** 索引標籤中，找出並按一下  **\< 區段 > #login**專案，這是這些連結的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="43ea4-249">In the **Styles** tab, locate and click the **\<section> #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="43ea4-250">請注意，在您按一下之後， **#login**樣式會自動置於 [**網站地圖**] 中。</span><span class="sxs-lookup"><span data-stu-id="43ea4-250">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="43ea4-251">此外，現在會反白顯示程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-251">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="43ea4-252">![選取 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image16.png "選取 CSS 樣式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-252">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image16.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="43ea4-253">*選取 CSS 樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-253">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="43ea4-254">藉由移除開頭和結尾字元並儲存**網站 .css**檔案，取消反白顯示的程式碼中的**文字對齊**屬性。</span><span class="sxs-lookup"><span data-stu-id="43ea4-254">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="43ea4-255">Page Inspector 知道組成目前頁面的所有不同檔案，而且它可以偵測到這些檔案中的任何變更。</span><span class="sxs-lookup"><span data-stu-id="43ea4-255">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="43ea4-256">當瀏覽器中目前的頁面未與來源檔案同步時，它就會對您發出警示。</span><span class="sxs-lookup"><span data-stu-id="43ea4-256">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="43ea4-257">在 Page Inspector 瀏覽器中，按一下位於網址列下方的列以重載頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-257">In the Page Inspector browser, click the bar located below the address bar to reload the page.</span></span>

    ![重載頁面](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    <span data-ttu-id="43ea4-259">*重載頁面*</span><span class="sxs-lookup"><span data-stu-id="43ea4-259">*Reloading the page*</span></span>

    <span data-ttu-id="43ea4-260">連結現在位於右方，但它們仍看起來像是項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="43ea4-260">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="43ea4-261">現在，您將移除專案符號，並水準對齊連結。</span><span class="sxs-lookup"><span data-stu-id="43ea4-261">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![已更新頁面](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    <span data-ttu-id="43ea4-263">*已更新頁面*</span><span class="sxs-lookup"><span data-stu-id="43ea4-263">*Updated page*</span></span>
6. <span data-ttu-id="43ea4-264">使用 檢查 模式，選取包含 &quot;暫存器&quot; 的任何 **&lt;li&gt;** 專案，然後 &quot;連結。&quot;</span><span class="sxs-lookup"><span data-stu-id="43ea4-264">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="43ea4-265">然後，按一下  **&lt; 區段&gt; #login**專案 來存取**樣式 .css**程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-265">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="43ea4-266">![尋找樣式](using-page-inspector-in-visual-studio-2012/_static/image19.png "尋找樣式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-266">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image19.png "Finding the style")</span></span>

    <span data-ttu-id="43ea4-267">*尋找樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-267">*Finding the style*</span></span>
7. <span data-ttu-id="43ea4-268">在**Style .css**中，將 **#login li**專案的程式碼取消批註。</span><span class="sxs-lookup"><span data-stu-id="43ea4-268">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="43ea4-269">您要新增的樣式將會隱藏專案符號，並以水準方式顯示專案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-269">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="43ea4-270">![Restyling 登入連結](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling 登入連結")</span><span class="sxs-lookup"><span data-stu-id="43ea4-270">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling the login links")</span></span>

    <span data-ttu-id="43ea4-271">*Restyling 登入連結*</span><span class="sxs-lookup"><span data-stu-id="43ea4-271">*Restyling the login links*</span></span>
8. <span data-ttu-id="43ea4-272">儲存**樣式 .css**檔案，然後在位址下方的列上按一下 [一次]，以重載頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-272">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="43ea4-273">請注意，連結會正確顯示。</span><span class="sxs-lookup"><span data-stu-id="43ea4-273">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="43ea4-274">![對應至右側的連結](using-page-inspector-in-visual-studio-2012/_static/image21.png "對應至右側的連結")</span><span class="sxs-lookup"><span data-stu-id="43ea4-274">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image21.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="43ea4-275">*對應至右側的連結*</span><span class="sxs-lookup"><span data-stu-id="43ea4-275">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="43ea4-276">最後，您將變更標題標題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-276">Finally, you will change the header title.</span></span> <span data-ttu-id="43ea4-277">使用 [檢查] 模式，在**這裡按一下您的標誌**，並取得產生此文字的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-277">Use the inspection mode to click **your logo here** text and get to the source code that generates it.</span></span>
10. <span data-ttu-id="43ea4-278">現在您已 **\_Layout**，請使用「**相片圖庫**」取代「**此處的標誌**」文字。</span><span class="sxs-lookup"><span data-stu-id="43ea4-278">Now you are in **\_Layout.cshtml**, replace '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="43ea4-279">儲存並更新 Page Inspector 的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="43ea4-279">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="43ea4-280">![指派新的標題](using-page-inspector-in-visual-studio-2012/_static/image22.png "指派新的標題")</span><span class="sxs-lookup"><span data-stu-id="43ea4-280">![Assigning a new title](using-page-inspector-in-visual-studio-2012/_static/image22.png "Assigning a new title")</span></span>

    <span data-ttu-id="43ea4-281">*指派新的標題*</span><span class="sxs-lookup"><span data-stu-id="43ea4-281">*Assigning a new title*</span></span>

    ![[相片圖庫] 頁面](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    <span data-ttu-id="43ea4-283">*已更新相片圖庫頁面*</span><span class="sxs-lookup"><span data-stu-id="43ea4-283">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="43ea4-284">最後，選取 [ **PhotoGallery** ] 專案，然後按**F5**以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-284">Finally, select the **PhotoGallery** project and press **F5** to run the app.</span></span> <span data-ttu-id="43ea4-285">查看所有變更如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="43ea4-285">Check out all the changes work as expected.</span></span>

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a><span data-ttu-id="43ea4-286">練習2：在 WebForms 專案中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="43ea4-286">Exercise 2: Using Page Inspector in WebForms Projects</span></span>

<span data-ttu-id="43ea4-287">在此練習中，您將瞭解如何使用 Page Inspector 來預覽和偵測 WebForms 解決方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-287">In this exercise, you will learn how to preview and debug a WebForms solution using Page Inspector.</span></span> <span data-ttu-id="43ea4-288">您會先執行工具的簡短膝上，以瞭解有助於 Web 偵錯工具的 Page Inspector 功能。</span><span class="sxs-lookup"><span data-stu-id="43ea4-288">You will first perform a brief lap around the tool to learn the Page Inspector features that facilitate the Web debugging process.</span></span> <span data-ttu-id="43ea4-289">然後，您將會在包含樣式問題的網頁中工作。</span><span class="sxs-lookup"><span data-stu-id="43ea4-289">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="43ea4-290">您將瞭解如何使用 Page Inspector 來尋找產生問題的原始程式碼並加以修正。</span><span class="sxs-lookup"><span data-stu-id="43ea4-290">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="43ea4-291">工作 1-探索 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="43ea4-291">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="43ea4-292">在這項工作中，您將學習如何在顯示相片圖庫的 WebForms 專案內容中，使用 Page Inspector 功能。</span><span class="sxs-lookup"><span data-stu-id="43ea4-292">In this task, you will learn how to use the Page Inspector features in the context of a WebForms project that shows a photo gallery.</span></span>

1. <span data-ttu-id="43ea4-293">開啟位於**來源/Ex2-WebForms/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-293">Open the **Begin** solution located at **Source/Ex2-WebForms/Begin/** folder.</span></span>

   1. <span data-ttu-id="43ea4-294">在繼續之前，您必須先下載一些遺漏的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="43ea4-294">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="43ea4-295">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="43ea4-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="43ea4-296">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="43ea4-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="43ea4-297">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="43ea4-298">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="43ea4-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="43ea4-299">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="43ea4-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="43ea4-300">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="43ea4-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="43ea4-301">在 方案總管中，找出**default.aspx**頁面，以滑鼠右鍵按一下它，然後選取 **在 Page Inspector 中查看**。</span><span class="sxs-lookup"><span data-stu-id="43ea4-301">In the Solution Explorer, locate **Default.aspx** page, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="43ea4-302">![使用 Page Inspector 開啟 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image24.png "使用 Page Inspector 開啟 default.aspx")</span><span class="sxs-lookup"><span data-stu-id="43ea4-302">![Opening Default.aspx with Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Opening Default.aspx with Page Inspector")</span></span>

    <span data-ttu-id="43ea4-303">*使用 Page Inspector 開啟 default.aspx*</span><span class="sxs-lookup"><span data-stu-id="43ea4-303">*Opening Default.aspx with Page Inspector*</span></span>
3. <span data-ttu-id="43ea4-304">[Page Inspector] 視窗會顯示 default.aspx。</span><span class="sxs-lookup"><span data-stu-id="43ea4-304">The Page Inspector window will show Default.aspx.</span></span>

    <span data-ttu-id="43ea4-305">![在 Page Inspector 中查看 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image25.png "在 Page Inspector 中查看 default.aspx")</span><span class="sxs-lookup"><span data-stu-id="43ea4-305">![Viewing Default.aspx in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image25.png "Viewing Default.aspx in Page Inspector")</span></span>

    <span data-ttu-id="43ea4-306">*在 Page Inspector 中查看 default.aspx*</span><span class="sxs-lookup"><span data-stu-id="43ea4-306">*Viewing Default.aspx in Page Inspector*</span></span>

    <span data-ttu-id="43ea4-307">Page Inspector 工具已整合到您的 Visual Studio 環境中。</span><span class="sxs-lookup"><span data-stu-id="43ea4-307">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="43ea4-308">偵測器包含內嵌的瀏覽器，以及會顯示所選程式碼的強大 HTML profiler。</span><span class="sxs-lookup"><span data-stu-id="43ea4-308">The inspector contains an embedded browser, together with a powerful HTML profiler that will show the selected code.</span></span> <span data-ttu-id="43ea4-309">請注意，您不需要執行解決方案來查看頁面的外觀。</span><span class="sxs-lookup"><span data-stu-id="43ea4-309">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-310">當 Page Inspector 瀏覽器的寬度小於已開啟頁面的寬度時，您將不會正確地看到此頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-310">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="43ea4-311">如果發生這種情況，請調整 Page Inspector 的寬度。</span><span class="sxs-lookup"><span data-stu-id="43ea4-311">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="43ea4-312">按一下 Page Inspector**中的 [** 檔案] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-312">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="43ea4-313">您會看到所有撰寫呈現之預設頁面的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="43ea4-313">You will see all the source files that are composing the rendered Default page.</span></span> <span data-ttu-id="43ea4-314">這是一種很有用的功能，可以一目了然地識別所有的元素，特別是當您使用使用者控制項和主版頁面時。</span><span class="sxs-lookup"><span data-stu-id="43ea4-314">This is a useful feature to identify all the elements at a glance, especially when you are working with User Controls and Master Pages.</span></span> <span data-ttu-id="43ea4-315">請注意，您也可以流覽至每個檔案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-315">Notice that you can also navigate to each of the files.</span></span>

    <span data-ttu-id="43ea4-316">![[檔案] 索引標籤](using-page-inspector-in-visual-studio-2012/_static/image26.png "[檔案] 索引標籤")</span><span class="sxs-lookup"><span data-stu-id="43ea4-316">![The Files tab](using-page-inspector-in-visual-studio-2012/_static/image26.png "The Files tab")</span></span>

    <span data-ttu-id="43ea4-317">*[檔案] 索引標籤*</span><span class="sxs-lookup"><span data-stu-id="43ea4-317">*The Files tab*</span></span>
5. <span data-ttu-id="43ea4-318">按一下位於索引標籤左側的**切換檢查模式** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="43ea4-318">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="43ea4-319">這項工具可讓您選取頁面的任何元素，並查看其 HTML 程式碼和 .aspx 來源。</span><span class="sxs-lookup"><span data-stu-id="43ea4-319">This tool will let you select any element of the page and see its HTML code and .aspx source.</span></span>

    <span data-ttu-id="43ea4-320">![切換檢查模式按鈕](using-page-inspector-in-visual-studio-2012/_static/image27.png "切換檢查模式按鈕")</span><span class="sxs-lookup"><span data-stu-id="43ea4-320">![Toggle Inspection Mode button](using-page-inspector-in-visual-studio-2012/_static/image27.png "Toggle Inspection Mode button")</span></span>

    <span data-ttu-id="43ea4-321">*切換檢查模式按鈕*</span><span class="sxs-lookup"><span data-stu-id="43ea4-321">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="43ea4-322">在 Page Inspector 瀏覽器中，將滑鼠指標移到頁面元素上方。</span><span class="sxs-lookup"><span data-stu-id="43ea4-322">In the Page Inspector browser, move the mouse over the page elements.</span></span> <span data-ttu-id="43ea4-323">當您將滑鼠指標移到所呈現頁面的任何部分上方時，會顯示專案類型，並在 [Visual Studio 編輯器] 中反白顯示對應的來源標記或程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-323">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    <span data-ttu-id="43ea4-324">![作用中的檢查模式](using-page-inspector-in-visual-studio-2012/_static/image28.png "作用中的檢查模式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-324">![Inspection mode in action](using-page-inspector-in-visual-studio-2012/_static/image28.png "Inspection mode in action")</span></span>

    <span data-ttu-id="43ea4-325">*作用中的檢查模式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-325">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-326">請勿將 [Page Inspector] 視窗最大化，否則您將無法看到顯示原始程式碼的 [預覽] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-326">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="43ea4-327">如果您在 Page Inspector 中按一下最大化的專案，將會出現選取範圍的原始程式碼，但會隱藏 [Page Inspector] 視窗。</span><span class="sxs-lookup"><span data-stu-id="43ea4-327">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="43ea4-328">如果您注意到**default.aspx**檔案，就會注意到產生所選項目的原始程式碼部分會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="43ea4-328">If you pay attention to **Default.aspx** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="43ea4-329">這項功能可協助較長的來源檔案版本，並提供直接且快速的方式來存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-329">This feature facilitates the edition of long source files, providing a direct and fast way to access the code.</span></span>

    <span data-ttu-id="43ea4-330">![檢查元素](using-page-inspector-in-visual-studio-2012/_static/image29.png "檢查元素")</span><span class="sxs-lookup"><span data-stu-id="43ea4-330">![Inspecting elements](using-page-inspector-in-visual-studio-2012/_static/image29.png "Inspecting elements")</span></span>

    <span data-ttu-id="43ea4-331">*檢查元素*</span><span class="sxs-lookup"><span data-stu-id="43ea4-331">*Inspecting elements*</span></span>
7. <span data-ttu-id="43ea4-332">按一下 [**切換檢查模式**] 按鈕（![選取-html](using-page-inspector-in-visual-studio-2012/_static/image30.png "選取-HTML---------------------------------------") ---------------------------------------</span><span class="sxs-lookup"><span data-stu-id="43ea4-332">Click the **Toggle Inspection Mode** button (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.")</span></span> <span data-ttu-id="43ea4-333">），位於 Page Inspector 索引標籤中，以停用游標。</span><span class="sxs-lookup"><span data-stu-id="43ea4-333">), located in Page Inspector tabs, to disable the cursor.</span></span>
8. <span data-ttu-id="43ea4-334">選取 [ **html** ] 索引標籤，以顯示在 Page Inspector 瀏覽器中轉譯的 html 程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-334">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="43ea4-335">在 HTML 程式碼中，找出具有 Koala 連結的清單專案，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="43ea4-335">In the HTML code, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="43ea4-336">請注意，當您選取程式碼時，對應的輸出會自動反白顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="43ea4-336">Notice that when you select the code, the corresponding output is automatically highlighted browser.</span></span> <span data-ttu-id="43ea4-337">這項功能非常適合用來查看 HTML 區塊在頁面上的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-337">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="43ea4-338">![選取頁面中的 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image31.png "選取頁面中的 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="43ea4-338">![Selecting an HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image31.png "Selecting an HTML element in the page")</span></span>

    <span data-ttu-id="43ea4-339">*選取頁面中的 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="43ea4-339">*Selecting an HTML element in the page*</span></span>
10. <span data-ttu-id="43ea4-340">按一下 [**切換檢查模式**] 按鈕以啟用*檢查模式*，然後按一下巡覽列。</span><span class="sxs-lookup"><span data-stu-id="43ea4-340">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="43ea4-341">在 HTML 程式碼右邊的 [樣式] 窗格中，您會看到一份清單，其中包含套用至所選元素的 CSS 樣式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-341">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-342">由於標頭是網站配置的一部分，因此 Page Inspector 也會開啟網站檔案，並反白顯示受影響的程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="43ea4-342">since the header is a part of the site layout, Page Inspector will also open Site.Master file and highlight the segment of code affected.</span></span>

    <span data-ttu-id="43ea4-343">![探索樣式 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "探索所選元素的樣式和原始檔")</span><span class="sxs-lookup"><span data-stu-id="43ea4-343">![Discovering styles WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Discovering styles and source files of a selected element")</span></span>

    <span data-ttu-id="43ea4-344">*探索所選元素的樣式和原始檔*</span><span class="sxs-lookup"><span data-stu-id="43ea4-344">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="43ea4-345">啟用切換檢查指標後，將滑鼠指標移至功能表列下方，然後按一下空白的半圓。</span><span class="sxs-lookup"><span data-stu-id="43ea4-345">With the toggle inspection pointer enabled, move the mouse pointer below the menu bar and click the blank half circle.</span></span>

    <span data-ttu-id="43ea4-346">![選取元素](using-page-inspector-in-visual-studio-2012/_static/image33.png "選取元素")</span><span class="sxs-lookup"><span data-stu-id="43ea4-346">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image33.png "Selecting an element")</span></span>

    <span data-ttu-id="43ea4-347">*選取元素*</span><span class="sxs-lookup"><span data-stu-id="43ea4-347">*Selecting an element*</span></span>
12. <span data-ttu-id="43ea4-348">在 [樣式] 窗格中，找出 [**主要-內容**] 群組底下的 [**背景影像**] 專案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-348">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="43ea4-349">**取消** **核取背景影像**，並查看發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="43ea4-349">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="43ea4-350">您會注意到，瀏覽器會立即反映變更，並隱藏圓形。</span><span class="sxs-lookup"><span data-stu-id="43ea4-350">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43ea4-351">您在 [Page Inspector 樣式] 索引標籤上套用的變更不會影響原始樣式表單。</span><span class="sxs-lookup"><span data-stu-id="43ea4-351">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="43ea4-352">您可以視需要取消核取樣式或變更其值，但它們會在重新整理頁面之後還原。</span><span class="sxs-lookup"><span data-stu-id="43ea4-352">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="43ea4-353">![啟用和停用 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "啟用和停用 CSS 樣式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-353">![Enabling and disabling CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="43ea4-354">*啟用和停用 CSS 樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-354">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="43ea4-355">現在，使用 [檢查] 模式按一下標頭上的 [這裡**的** **標誌**] 文字。</span><span class="sxs-lookup"><span data-stu-id="43ea4-355">Now, click the '**your** **logo here'** text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="43ea4-356">在 [**樣式**] 索引標籤中，找出 [**網站-標題**] 群組底下的 [**字型大小**] CSS 屬性。</span><span class="sxs-lookup"><span data-stu-id="43ea4-356">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="43ea4-357">按兩下屬性一次以編輯其值。</span><span class="sxs-lookup"><span data-stu-id="43ea4-357">Double-click the attribute once to edit its value.</span></span> <span data-ttu-id="43ea4-358">以**3em**取代 2.3 em 值，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="43ea4-358">Replace the 2.3em value with **3em**, and then press ENTER.</span></span> <span data-ttu-id="43ea4-359">請注意，標題看起來更大。</span><span class="sxs-lookup"><span data-stu-id="43ea4-359">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="43ea4-360">![變更頁面 Inspector2 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image35.png "變更 Page Inspector 中的 CSS 值")</span><span class="sxs-lookup"><span data-stu-id="43ea4-360">![Changing CSS values in the Page Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="43ea4-361">*變更 Page Inspector 中的 CSS 值*</span><span class="sxs-lookup"><span data-stu-id="43ea4-361">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="43ea4-362">按一下位於 Page Inspector 右窗格中的 [**追蹤樣式**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-362">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="43ea4-363">這是一種替代方式，可查看套用至選取專案的所有樣式（依屬性名稱排序）。</span><span class="sxs-lookup"><span data-stu-id="43ea4-363">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    <span data-ttu-id="43ea4-364">![追蹤所選元素的 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image36.png "追蹤所選元素的 CSS 樣式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-364">![CSS styles tracing of the selected element](using-page-inspector-in-visual-studio-2012/_static/image36.png "CSS styles tracing of the selected element")</span></span>

    <span data-ttu-id="43ea4-365">*追蹤所選元素的 CSS 樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-365">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="43ea4-366">Page Inspector 的另一項功能是 [版面配置] 窗格。</span><span class="sxs-lookup"><span data-stu-id="43ea4-366">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="43ea4-367">使用 [檢查] 模式，選取巡覽列，然後按一下右窗格中**的 [配置**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43ea4-367">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="43ea4-368">您會看到所選元素的確切大小，以及其位移、邊界、填補和框線大小。</span><span class="sxs-lookup"><span data-stu-id="43ea4-368">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="43ea4-369">請注意，您也可以從這個視圖中修改值。</span><span class="sxs-lookup"><span data-stu-id="43ea4-369">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="43ea4-370">![Page Inspector 中的元素版面配置](using-page-inspector-in-visual-studio-2012/_static/image37.png "Page Inspector 中的元素版面配置")</span><span class="sxs-lookup"><span data-stu-id="43ea4-370">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image37.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="43ea4-371">*Page Inspector 中的元素版面配置*</span><span class="sxs-lookup"><span data-stu-id="43ea4-371">*Element layout in Page Inspector*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="43ea4-372">工作 2-在相片圖庫中尋找和修正樣式問題</span><span class="sxs-lookup"><span data-stu-id="43ea4-372">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="43ea4-373">您要如何診斷舊版 Visual Studio 的網頁問題？</span><span class="sxs-lookup"><span data-stu-id="43ea4-373">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="43ea4-374">您很可能熟悉在 Visual Studio IDE 外部執行的 web 偵錯工具，例如 Internet Explorer 開發人員工具或 Firebug。</span><span class="sxs-lookup"><span data-stu-id="43ea4-374">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="43ea4-375">瀏覽器只會瞭解 HTML、腳本和樣式，而基礎架構則會產生要轉譯的 HTML。</span><span class="sxs-lookup"><span data-stu-id="43ea4-375">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="43ea4-376">基於這個理由，您通常需要部署整個網站，以查看網頁的外觀。</span><span class="sxs-lookup"><span data-stu-id="43ea4-376">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="43ea4-377">當您想要在網站中偵測並修正問題時，您可能會遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="43ea4-377">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="43ea4-378">從 Visual Studio 執行解決方案，或在 web 伺服器上部署頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-378">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="43ea4-379">在瀏覽器中，開啟您使用的開發人員工具，或直接開啟原始程式碼和樣式，並嘗試符合問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-379">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="43ea4-380">若要尋找相關的檔案，您可以使用 [&quot;搜尋]&quot; 或 &quot;在 [檔案]&quot; [功能] 中搜尋樣式類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="43ea4-380">To find the files involved, you'd have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="43ea4-381">一旦偵測到錯誤，請停止網頁瀏覽器和伺服器。</span><span class="sxs-lookup"><span data-stu-id="43ea4-381">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="43ea4-382">清除瀏覽器快取。</span><span class="sxs-lookup"><span data-stu-id="43ea4-382">Clear the browser cache.</span></span>
5. <span data-ttu-id="43ea4-383">回到 Visual Studio 以套用修正程式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-383">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="43ea4-384">重複所有要測試的步驟。</span><span class="sxs-lookup"><span data-stu-id="43ea4-384">Repeat all the steps to test.</span></span>

<span data-ttu-id="43ea4-385">由於 ASP.NET WebForms 中沒有實際的 WYSIWYG，因此在執行或部署之後，會在後續階段偵測到某些樣式問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-385">As there is no real WYSIWYG in ASP.NET WebForms, some style issues are detected on a later stage, after running or deploying.</span></span> <span data-ttu-id="43ea4-386">現在，有了 Page Inspector，就可以預覽任何頁面，而不需要執行解決方案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-386">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="43ea4-387">在這項工作中，您將使用 Page inspector 來修正相片圖庫應用程式的某些問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-387">In this task, you will use the Page inspector for fixing some issues of the Photo Gallery application.</span></span> <span data-ttu-id="43ea4-388">在下列步驟中，您將在標頭中偵測並快速修正一些簡單的樣式問題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-388">In the following steps, you will detect and quickly fix some simple styling issue in the header.</span></span>

1. <span data-ttu-id="43ea4-389">使用頁面檢查，找出標頭左邊的**註冊**和**登入**連結。</span><span class="sxs-lookup"><span data-stu-id="43ea4-389">Using Page Inspection, locate the **Register** and the **Log In** links at the left side of the header.</span></span>

    <span data-ttu-id="43ea4-390">請注意，此連結不會顯示在右邊的預期位置。</span><span class="sxs-lookup"><span data-stu-id="43ea4-390">Notice that the link is not displayed at the expected place on the right.</span></span> <span data-ttu-id="43ea4-391">您現在會將連結對齊右邊，並據以調整其樣式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-391">You will now align the link to the right and restyle it accordingly.</span></span>

    <span data-ttu-id="43ea4-392">![位於左側的 [登入] 連結](using-page-inspector-in-visual-studio-2012/_static/image38.png "位於左側的 [登入] 連結")</span><span class="sxs-lookup"><span data-stu-id="43ea4-392">![Log in link positioned on the left](using-page-inspector-in-visual-studio-2012/_static/image38.png "Log in link positioned on the left")</span></span>

    <span data-ttu-id="43ea4-393">*位於左側的 [登入] 連結*</span><span class="sxs-lookup"><span data-stu-id="43ea4-393">*Log In link positioned on the left*</span></span>
2. <span data-ttu-id="43ea4-394">選取 [切換檢查模式] 後，選取 [登入] 連結以開啟其程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-394">With Toggle Inspection Mode selected, select the Log In link to open its code.</span></span>

    <span data-ttu-id="43ea4-395">請注意，連結原始程式碼位於**網站**檔案中，而不是預設的 .aspx 頁面中，這是您可能會看到的位置;您已直接放在正確的來源檔案中。</span><span class="sxs-lookup"><span data-stu-id="43ea4-395">Notice that the link source code is located in the **Site.Master** file, not in the Default.aspx page which is the place you might look in first place; you have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="43ea4-396">在 **樣式** 索引標籤中，找出並按一下  **&lt; 區段&gt; #login**專案，這是這些連結的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="43ea4-396">In the **Styles** tab, locate and click the **&lt;section&gt; #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="43ea4-397">請注意，在您按一下之後， **#login**樣式會自動置於 [**網站地圖**] 中。</span><span class="sxs-lookup"><span data-stu-id="43ea4-397">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="43ea4-398">此外，現在會反白顯示程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-398">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="43ea4-399">![選取 CSS 樣式](using-page-inspector-in-visual-studio-2012/_static/image39.png "選取 CSS 樣式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-399">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image39.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="43ea4-400">*選取 CSS 樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-400">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="43ea4-401">藉由移除開頭和結尾字元並儲存**網站 .css**檔案，取消反白顯示的程式碼中的**文字對齊**屬性。</span><span class="sxs-lookup"><span data-stu-id="43ea4-401">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="43ea4-402">Page Inspector 知道組成目前頁面的所有不同檔案，而且它可以偵測到這些檔案中的任何變更。</span><span class="sxs-lookup"><span data-stu-id="43ea4-402">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="43ea4-403">當瀏覽器中目前的頁面未與來源檔案同步時，它就會對您發出警示。</span><span class="sxs-lookup"><span data-stu-id="43ea4-403">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="43ea4-404">在 Page Inspector 瀏覽器中，按一下位於網址列下方的列，以儲存變更並重載頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-404">In the Page Inspector browser, click the bar located below the address bar to save the changes and reload the page.</span></span>

    ![重載頁面](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    <span data-ttu-id="43ea4-406">*重載頁面*</span><span class="sxs-lookup"><span data-stu-id="43ea4-406">*Reloading the page*</span></span>

    <span data-ttu-id="43ea4-407">連結現在位於右方，但它們仍看起來像是項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="43ea4-407">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="43ea4-408">現在，您將移除專案符號，並水準對齊連結。</span><span class="sxs-lookup"><span data-stu-id="43ea4-408">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![已更新頁面](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    <span data-ttu-id="43ea4-410">*已更新頁面*</span><span class="sxs-lookup"><span data-stu-id="43ea4-410">*Updated page*</span></span>
6. <span data-ttu-id="43ea4-411">使用 檢查 模式，選取包含 &quot;暫存器&quot; 的任何 **&lt;li&gt;** 專案，然後 &quot;連結。&quot;</span><span class="sxs-lookup"><span data-stu-id="43ea4-411">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="43ea4-412">然後，按一下  **&lt; 區段&gt; #login**專案 來存取**樣式 .css**程式碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-412">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="43ea4-413">![尋找樣式](using-page-inspector-in-visual-studio-2012/_static/image42.png "尋找樣式")</span><span class="sxs-lookup"><span data-stu-id="43ea4-413">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image42.png "Finding the style")</span></span>

    <span data-ttu-id="43ea4-414">*尋找樣式*</span><span class="sxs-lookup"><span data-stu-id="43ea4-414">*Finding the style*</span></span>
7. <span data-ttu-id="43ea4-415">在**Style .css**中，將 **#login li**專案的程式碼取消批註。</span><span class="sxs-lookup"><span data-stu-id="43ea4-415">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="43ea4-416">您要新增的樣式將會隱藏專案符號，並以水準方式顯示專案。</span><span class="sxs-lookup"><span data-stu-id="43ea4-416">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="43ea4-417">![Restyling 登入連結](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling 登入連結")</span><span class="sxs-lookup"><span data-stu-id="43ea4-417">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling the login links")</span></span>

    <span data-ttu-id="43ea4-418">*Restyling 登入連結*</span><span class="sxs-lookup"><span data-stu-id="43ea4-418">*Restyling the login links*</span></span>
8. <span data-ttu-id="43ea4-419">儲存**樣式 .css**檔案，然後在位址下方的列上按一下 [一次]，以重載頁面。</span><span class="sxs-lookup"><span data-stu-id="43ea4-419">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="43ea4-420">請注意，連結會正確顯示。</span><span class="sxs-lookup"><span data-stu-id="43ea4-420">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="43ea4-421">![對應至右側的連結](using-page-inspector-in-visual-studio-2012/_static/image44.png "對應至右側的連結")</span><span class="sxs-lookup"><span data-stu-id="43ea4-421">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image44.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="43ea4-422">*對應至右側的連結*</span><span class="sxs-lookup"><span data-stu-id="43ea4-422">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="43ea4-423">最後，您將變更標題標題。</span><span class="sxs-lookup"><span data-stu-id="43ea4-423">Finally, you will change the header title.</span></span> <span data-ttu-id="43ea4-424">不是在所有檔案中搜尋「**此處的標誌**」文字，而是使用 [檢查] 模式來按一下文字，然後取得產生它的原始碼。</span><span class="sxs-lookup"><span data-stu-id="43ea4-424">Instead of searching for the '**your logo here'** text in all the files, use the inspection mode to click the text and get to source code that generates it.</span></span>

    <span data-ttu-id="43ea4-425">![尋找網站標題](using-page-inspector-in-visual-studio-2012/_static/image45.png "尋找網站標題")</span><span class="sxs-lookup"><span data-stu-id="43ea4-425">![Finding the site title](using-page-inspector-in-visual-studio-2012/_static/image45.png "Finding the site title")</span></span>

    <span data-ttu-id="43ea4-426">*尋找網站標題*</span><span class="sxs-lookup"><span data-stu-id="43ea4-426">*Finding the site title*</span></span>
10. <span data-ttu-id="43ea4-427">現在您已在**網站**中，使用 [**相片圖庫**] 取代 [**您的標誌這裡**] 文字。</span><span class="sxs-lookup"><span data-stu-id="43ea4-427">Now you are in **Site.Master**, replace the '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="43ea4-428">儲存並更新 Page Inspector 的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="43ea4-428">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="43ea4-429">![已更新相片圖庫頁面](using-page-inspector-in-visual-studio-2012/_static/image46.png "已更新相片圖庫頁面")</span><span class="sxs-lookup"><span data-stu-id="43ea4-429">![Photo Gallery page updated](using-page-inspector-in-visual-studio-2012/_static/image46.png "Photo Gallery page updated")</span></span>

    <span data-ttu-id="43ea4-430">*已更新相片圖庫頁面*</span><span class="sxs-lookup"><span data-stu-id="43ea4-430">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="43ea4-431">最後按**F5**鍵執行應用程式，查看所有變更如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="43ea4-431">Finally press **F5** to run the app the check out all the changes work as expected.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="43ea4-432">總結</span><span class="sxs-lookup"><span data-stu-id="43ea4-432">Summary</span></span>

<span data-ttu-id="43ea4-433">藉由完成這個實際操作實驗室，您就可以學會如何使用 Page Inspector 來預覽您的 Web 應用程式，而不需要在瀏覽器中重建和執行網站。</span><span class="sxs-lookup"><span data-stu-id="43ea4-433">By completing this Hands-On Lab, you have learnt how to use Page Inspector to preview your Web application without having to rebuild and run the Web site in a browser.</span></span> <span data-ttu-id="43ea4-434">此外，您還學會如何藉由從轉譯的輸出直接存取原始程式碼，快速尋找並修正 bug。</span><span class="sxs-lookup"><span data-stu-id="43ea4-434">In addition, you have learnt how to quickly find and fix bugs by accessing directly from the rendered output to the source code.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="43ea4-435">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="43ea4-435">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="43ea4-436">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="43ea4-436">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="43ea4-437">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="43ea4-437">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="43ea4-438">移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="43ea4-438">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="43ea4-439">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="43ea4-439">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="43ea4-440">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="43ea4-440">Click on **Install Now**.</span></span> <span data-ttu-id="43ea4-441">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="43ea4-441">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="43ea4-442">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="43ea4-442">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="43ea4-443">![安裝 Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="43ea4-443">![Install Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="43ea4-444">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="43ea4-444">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="43ea4-445">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="43ea4-445">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    <span data-ttu-id="43ea4-447">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="43ea4-447">*Accepting the license terms*</span></span>
5. <span data-ttu-id="43ea4-448">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="43ea4-448">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    <span data-ttu-id="43ea4-450">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="43ea4-450">*Installation progress*</span></span>
6. <span data-ttu-id="43ea4-451">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="43ea4-451">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    <span data-ttu-id="43ea4-453">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="43ea4-453">*Installation completed*</span></span>
7. <span data-ttu-id="43ea4-454">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="43ea4-454">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="43ea4-455">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="43ea4-455">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    <span data-ttu-id="43ea4-457">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="43ea4-457">*VS Express for Web tile*</span></span>
