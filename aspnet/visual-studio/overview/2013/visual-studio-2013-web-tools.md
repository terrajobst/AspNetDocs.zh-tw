---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 實習實驗室： Visual Studio 2013 Web 工具 |Microsoft Docs
author: rick-anderson
description: Visual Studio 是適用于的絕佳開發環境。以網路為基礎的 Windows 和 Web 專案。 其中包含強大的文字編輯器，可輕鬆地用於 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622672"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="f9dd1-104">實習實驗室： Visual Studio 2013 Web 工具</span><span class="sxs-lookup"><span data-stu-id="f9dd1-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>

<span data-ttu-id="f9dd1-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f9dd1-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="f9dd1-106">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="f9dd1-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="f9dd1-107">Visual Studio 是適用于的絕佳開發環境。以網路為基礎的 Windows 和 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="f9dd1-108">其中包含強大的文字編輯器，可輕鬆地在不使用專案的情況下編輯獨立檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="f9dd1-109">當您編輯每個檔案時，Visual Studio 會維護功能完整的剖析樹狀目錄。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="f9dd1-110">這可讓 Visual Studio 提供無與倫比的自動完成和以檔為基礎的動作，同時讓開發體驗變得更快且更愉快。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="f9dd1-111">這些功能在 HTML 和 CSS 檔中特別有用。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="f9dd1-112">這項功能也適用于延伸模組，可讓您輕鬆擴充具有強大新功能的編輯器，以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="f9dd1-113">Web Essentials 是（大部分）與 web 相關的 Visual Studio 增強功能的集合。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="f9dd1-114">其中包含許多新的 IntelliSense 完成（特別是針對 CSS）、新的瀏覽器連結功能、JavaScript 檔案的自動 JSHint、HTML 和 CSS 的新警告，以及許多對新式 網頁程式開發不可或缺的其他功能。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="f9dd1-115">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="f9dd1-116">概觀</span><span class="sxs-lookup"><span data-stu-id="f9dd1-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f9dd1-117">目標</span><span class="sxs-lookup"><span data-stu-id="f9dd1-117">Objectives</span></span>

<span data-ttu-id="f9dd1-118">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="f9dd1-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="f9dd1-119">使用 Web Essentials 中包含的新 HTML 編輯器功能，例如豐富的 HTML5 程式碼片段和 Zen 編碼</span><span class="sxs-lookup"><span data-stu-id="f9dd1-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="f9dd1-120">使用 Web Essentials 中包含的新 CSS 編輯器功能，例如色彩選擇器和瀏覽器矩陣工具提示</span><span class="sxs-lookup"><span data-stu-id="f9dd1-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="f9dd1-121">使用 Web Essentials 中包含的新 JavaScript 編輯器功能，例如 [解壓縮至檔案] 和 [IntelliSense]，適用于所有 HTML 元素</span><span class="sxs-lookup"><span data-stu-id="f9dd1-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="f9dd1-122">使用瀏覽器連結在瀏覽器與 Visual Studio 之間交換資料</span><span class="sxs-lookup"><span data-stu-id="f9dd1-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f9dd1-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f9dd1-123">Prerequisites</span></span>

<span data-ttu-id="f9dd1-124">若要完成此實際操作實驗室，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="f9dd1-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="f9dd1-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)或更高版本</span><span class="sxs-lookup"><span data-stu-id="f9dd1-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="f9dd1-126">Web Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="f9dd1-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="f9dd1-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="f9dd1-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f9dd1-128">安裝程式</span><span class="sxs-lookup"><span data-stu-id="f9dd1-128">Setup</span></span>

<span data-ttu-id="f9dd1-129">為了在此實際操作實驗室中執行練習，您必須先設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="f9dd1-130">開啟 Windows Explorer 視窗，並流覽至實驗室的 [**源**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="f9dd1-131">以滑鼠右鍵按一下 [ **Setup** ]，然後選取 [以**系統管理員身分執行**] 來啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="f9dd1-132">如果顯示 [使用者帳戶控制] 對話方塊，請確認動作以繼續。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="f9dd1-133">執行安裝程式之前，請確定您已檢查過此實驗室的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="f9dd1-134">使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="f9dd1-134">Using the Code Snippets</span></span>

<span data-ttu-id="f9dd1-135">在整個實驗室檔中，系統會指示您插入程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="f9dd1-136">為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 2013 內進行存取，以避免必須以手動方式新增。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="f9dd1-137">每個練習都附有一個起始解決方案，此方案位於練習的 [**開始**] 資料夾中，可讓您獨立于其他練習之外進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="f9dd1-138">請注意，在練習期間新增的程式碼片段缺少這些起始的解決方案，而且在您完成練習之前可能無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="f9dd1-139">在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的**結束**資料夾，其中含有完成對應練習中步驟所產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="f9dd1-140">如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f9dd1-141">練習</span><span class="sxs-lookup"><span data-stu-id="f9dd1-141">Exercises</span></span>

<span data-ttu-id="f9dd1-142">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="f9dd1-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="f9dd1-143">使用瀏覽器連結和 Web Essentials</span><span class="sxs-lookup"><span data-stu-id="f9dd1-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="f9dd1-144">利用程式碼片段和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="f9dd1-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="f9dd1-145">當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="f9dd1-146">每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="f9dd1-147">本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="f9dd1-148">如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="f9dd1-149">練習1：使用瀏覽器連結和 Web Essentials</span><span class="sxs-lookup"><span data-stu-id="f9dd1-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="f9dd1-150">**Web Essentials**是一個 Visual Studio 延伸模組，可為新式 Web 開發新增各種有用的功能，其主要著重于讓 網頁程式開發體驗更快、更愉快。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="f9dd1-151">您可以從 Visual Studio 的擴充功能庫安裝 Web Essentials。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="f9dd1-152">**瀏覽器連結**是包含在 Visual Studio 2013 中的新功能，可在 Visual Studio IDE 和任何開啟的瀏覽器之間提供通道，以便在您的 web 應用程式和 Visual Studio 之間交換資料。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="f9dd1-153">Web Essentials 使用工具擴充瀏覽器連結，直接從瀏覽器操作您網頁的 DOM 物件模型和 CSS 樣式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="f9dd1-154">在此練習中，您將探索**Web Essentials**和**瀏覽器**所支援的一些功能，以增強簡單的測驗頁面。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="f9dd1-155">工作 1-在多個瀏覽器中執行專案</span><span class="sxs-lookup"><span data-stu-id="f9dd1-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="f9dd1-156">在這項工作中，您會將 web 應用程式設定為同時在多個瀏覽器中執行，這對於跨瀏覽器測試很有用。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="f9dd1-157">開啟**Microsoft Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="f9dd1-158">**在 [檔案**] 功能表中，選取 [開啟] **|專案/方案 ...** 然後流覽至實驗室的**源**資料夾中的**Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** （C:\WebCampsTK\HOL\VSWebTooling\Source）。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="f9dd1-159">選取 [**開始**]，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="f9dd1-160">在 [Visual Studio] 工具列中，展開 [瀏覽器] 功能表，然後選取 **[流覽方式 ...]** 。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="f9dd1-161">![流覽功能表選項](visual-studio-2013-web-tools/_static/image1.png "流覽方式 。在瀏覽器功能表中")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="f9dd1-162">*流覽功能表選項*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="f9dd1-163">在 [**流覽方式**] 對話方塊中，按住**CTRL**鍵並按一下 [**設定為預設值**]，以選取**Google Chrome**和**Internet Explorer** 。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="f9dd1-164">![[流覽方式] 對話方塊](visual-studio-2013-web-tools/_static/image2.png "[流覽方式] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="f9dd1-165">*選取多個預設瀏覽器*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="f9dd1-166">Google Chrome 和 Internet Explorer 現在應該會顯示為預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="f9dd1-167">按一下 [**取消**] 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="f9dd1-168">![Google Chrome 和 Internet Explorer 做為預設瀏覽器](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 和 Internet Explorer 預設瀏覽器")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="f9dd1-169">*Google Chrome 和 Internet Explorer 做為預設瀏覽器*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-170">設定預設瀏覽器之後，瀏覽器功能表中會選取 [**多個流覽**器] 選項。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="f9dd1-171">![多個瀏覽器](visual-studio-2013-web-tools/_static/image4.png "多個瀏覽器")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="f9dd1-172">按**CTRL** + **F5**以執行應用程式，而不進行偵測。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="f9dd1-173">當這兩個瀏覽器視窗都開啟時，將其中一項放在另一個上方，以便同時查看兩個瀏覽器的更新。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="f9dd1-174">瀏覽器應該會顯示含有淺藍色矩形的網頁。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="f9dd1-175">![將一個瀏覽器放在另一個上方](visual-studio-2013-web-tools/_static/image5.png "將一個瀏覽器放在另一個上方")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="f9dd1-176">*將一個瀏覽器放在另一個上方*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="f9dd1-177">請勿關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-177">Do not close the browsers.</span></span> <span data-ttu-id="f9dd1-178">您將在下一項工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="f9dd1-179">工作 2-使用 Zen 編碼來建立 HTML 元素</span><span class="sxs-lookup"><span data-stu-id="f9dd1-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="f9dd1-180">**Zen 編碼**是一個編輯器外掛程式，適用于高速 HTML、XML、XSL （或任何其他結構化程式碼格式）編碼和編輯。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="f9dd1-181">此外掛程式的核心是功能強大的縮寫引擎，可讓您將運算式（類似于 CSS 選取器）展開為 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="f9dd1-182">Zen 編碼是使用 CSS 樣式選擇器語法來撰寫 HTML 的快速方式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="f9dd1-183">在此練習中，您將使用 Web Essentials 提供的 Zen 編碼功能來產生代表問題選項的 HTML 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="f9dd1-184">切換回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="f9dd1-185">開啟位於**Views** | **Home**資料夾中的**Index. cshtml**檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="f9dd1-186">取代 **&lt;!--TODO：在此加入選項--&gt;** 批註加上下列程式碼，然後按**tab**鍵。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="f9dd1-187">程式碼應該展開為 HTML。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="f9dd1-188">![擴充的 HTML](visual-studio-2013-web-tools/_static/image6.png "擴充的 HTML")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="f9dd1-189">*擴充的 HTML*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-190">若要深入瞭解 Zen 編碼語法，請參閱下列[文章](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="f9dd1-191">按一下 [重新整理**連結的瀏覽器**] 按鈕，以更新這兩個瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="f9dd1-192">![重新整理連結的瀏覽器](visual-studio-2013-web-tools/_static/image7.png "重新整理連結的瀏覽器")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="f9dd1-193">*重新整理連結的瀏覽器*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="f9dd1-194">![Internet Explorer-頁面已更新四個按鈕](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-頁面已更新四個按鈕")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="f9dd1-195">*Internet Explorer-頁面已更新四個按鈕*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="f9dd1-196">![Google Chrome-頁面已更新四個按鈕](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-頁面已更新四個按鈕")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="f9dd1-197">*Google Chrome-頁面已更新四個按鈕*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="f9dd1-198">切換回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="f9dd1-199">您已將按鈕新增至頁面，但您仍然需要新增範本問題。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="f9dd1-200">若要這麼做，您將使用 Web Essentials 中名為**Lorem Ipsum**產生器的新功能。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="f9dd1-201">找出具有**class**屬性**front**的**div**元素。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="f9dd1-202">新增下列程式碼做為**div**的第一個子專案，然後按**tab**鍵。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="f9dd1-203">程式碼應該展開為 HTML。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="f9dd1-204">![自動產生的 Lorem Ipsum](visual-studio-2013-web-tools/_static/image10.png "自動產生的 Lorem Ipsum")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="f9dd1-205">*自動產生的 Lorem Ipsum*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-206">在 Zen 程式碼撰寫過程中，您現在可以直接在 HTML 編輯器中產生 Lorem Ipsum 程式碼。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="f9dd1-207">只要輸入**lorem**並按**TAB 鍵**，就會插入30個單字 lorem Ipsum 文字。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="f9dd1-208">例如，</span><span class="sxs-lookup"><span data-stu-id="f9dd1-208">E.g.</span></span> <span data-ttu-id="f9dd1-209">*lorem10*會插入10個 Lorem Ipsum 文字。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="f9dd1-210">您會使用 Web Essentials 中的另一項新功能（稱為**Lorem 圖元**產生器），在問題頂端新增標誌。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="f9dd1-211">新增下列程式碼做為**div**元素的第一個子專案，並將**container**當做**類別**值，然後按**tab**鍵。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="f9dd1-212">程式碼應展開為 HTML。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="f9dd1-213">![自動產生的 Lorem 圖元](visual-studio-2013-web-tools/_static/image11.png "自動產生的 Lorem 圖元")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="f9dd1-214">*自動產生的 Lorem 圖元*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-215">在 Zen 程式碼撰寫過程中，您也可以直接在 HTML 編輯器中產生 Lorem 圖元的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="f9dd1-216">只要輸入**pix-200x200-動物**並按**TAB 鍵**，就會插入含有動物200x200 影像的**img**標記。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="f9dd1-217">如需詳細資訊，請參閱[Lorem 圖元](http://www.lorempixel.com)。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="f9dd1-218">按一下 [重新整理**連結的瀏覽器**] 按鈕，以更新這兩個瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="f9dd1-219">![Internet Explorer-自動產生的影像和文字](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-自動產生的影像和文字")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="f9dd1-220">*Internet Explorer-自動產生的影像和文字*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="f9dd1-221">![Google Chrome-自動產生的影像和文字](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-自動產生的影像和文字")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="f9dd1-222">*Google Chrome-自動產生的影像和文字*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-223">由於新增程式碼片段時，會隨機選取影像，因此瀏覽器中顯示的影像可能會不同。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="f9dd1-224">請勿關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-224">Do not close the browsers.</span></span> <span data-ttu-id="f9dd1-225">您將在下一項工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="f9dd1-226">工作 3-更新樣式屬性</span><span class="sxs-lookup"><span data-stu-id="f9dd1-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="f9dd1-227">在這項工作中，您將使用瀏覽器連結的 [**檢查模式]** 功能來偵測產生特定 DOM 元素的確切位置，然後使用 Web Essentials 所提供的色彩選擇器來更新該專案的 color 屬性。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="f9dd1-228">在 Internet Explorer 瀏覽器中，按**CTRL** + **ALT** + **I**以啟用 [檢查] 模式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="f9dd1-229">將指標移到淺藍色框線上，然後按一下。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="f9dd1-230">![將指標移到淺藍色框線上](visual-studio-2013-web-tools/_static/image14.png "將指標移到淺藍色框線上")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="f9dd1-231">*將指標移到淺藍色框線上*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="f9dd1-232">切換回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="f9dd1-233">請注意，在 [Visual Studio HTML 編輯器] 中，也會選取您在瀏覽器中選取的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="f9dd1-234">![在 Visual Studio HTML 編輯器中選取 HTML 元素](visual-studio-2013-web-tools/_static/image15.png "在 Visual Studio HTML 編輯器中選取 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="f9dd1-235">*在 Visual Studio HTML 編輯器中選取 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="f9dd1-236">您現在將更新**front** CSS 類別，以便變更所選項目的樣式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="f9dd1-237">若要這麼做，請按**CTRL** +  **，** 開啟 [**流覽至**搜尋] 方塊。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="f9dd1-238">輸入**網站 .css** ，然後按**enter**鍵以開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="f9dd1-239">![正在開啟檔案網站 .css](visual-studio-2013-web-tools/_static/image16.png "正在開啟檔案網站 .css")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="f9dd1-240">*正在開啟檔案網站 .css*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="f9dd1-241">按**CTRL** + **F**並輸入**flip-CONTAINER. front**以尋找 CSS 選取器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-241">Press **CTRL** + **F** and type **.flip-container .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="f9dd1-242">按一下類別之 [框線] 屬性中的淺藍色方塊，以開啟色彩選擇器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="f9dd1-243">![開啟色彩選擇器](visual-studio-2013-web-tools/_static/image17.png "開啟色彩選擇器")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="f9dd1-244">*開啟色彩選擇器*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="f9dd1-245">按一下箭號按鈕以展開色彩選擇器，然後選取新的色彩。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="f9dd1-246">![展開色彩選擇器](visual-studio-2013-web-tools/_static/image18.png "展開色彩選擇器")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="f9dd1-247">*展開色彩選擇器*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="f9dd1-248">按**CTRL** + **ALT** + **enter**以重新整理連結的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="f9dd1-249">切換到 Internet Explorer，並注意框線的色彩如何變更。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="f9dd1-250">![Internet Explorer-框線色彩已更新](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-框線色彩已更新")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="f9dd1-251">*Internet Explorer-框線色彩已更新*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="f9dd1-252">切換至 Google Chrome，並注意框線的色彩如何變更。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="f9dd1-253">![Google Chrome-框線色彩已更新](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-框線色彩已更新")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="f9dd1-254">*Google Chrome-框線色彩已更新*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="f9dd1-255">切換回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="f9dd1-256">移至**網站 .css**檔案的結尾，然後按**CTRL** + **F**以尋找**btn**選取器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="f9dd1-257">請注意， **-webkit-border-radius**屬性會加上綠色的底線。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="f9dd1-258">![-webkit-btn 選取器的邊界半徑屬性](visual-studio-2013-web-tools/_static/image21.png "-webkit-btn 選取器的邊界半徑屬性")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="f9dd1-259">*-webkit-btn 選取器的邊界半徑屬性*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="f9dd1-260">將插入號放在 **-webkit-border-radius**屬性中。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="f9dd1-261">屬性之第一個單字的第一個字母底下應會出現藍線。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="f9dd1-262">這是**智慧標籤**。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="f9dd1-263">按**CTRL** +  **。**</span><span class="sxs-lookup"><span data-stu-id="f9dd1-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="f9dd1-264">開啟 [建議] 功能表，然後按一下 [**新增遺漏的標準屬性（框線-半徑）** ]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="f9dd1-265">![新增遺漏的標準屬性建議](visual-studio-2013-web-tools/_static/image22.png "新增遺漏的標準屬性建議")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="f9dd1-266">*新增遺漏的標準屬性建議*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="f9dd1-267">[**框線-半徑**] 屬性會自動新增至 [CSS 規則]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="f9dd1-268">![遺漏新增的標準屬性](visual-studio-2013-web-tools/_static/image23.png "遺漏新增的標準屬性")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="f9dd1-269">*遺漏新增的標準屬性*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="f9dd1-270">將指標移到 [**框線半徑**] 屬性上方，以顯示**瀏覽器矩陣工具提示**。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="f9dd1-271">**瀏覽器矩陣工具提示**會顯示每個瀏覽器中屬性的可用性。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="f9dd1-272">![瀏覽器矩陣工具提示](visual-studio-2013-web-tools/_static/image24.png "瀏覽器矩陣工具提示")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="f9dd1-273">*瀏覽器矩陣工具提示*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="f9dd1-274">請注意，[**框線-半徑**] 屬性的值仍會加上底線。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="f9dd1-275">將指標移到值上方，以查看警告訊息。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="f9dd1-276">![框線-radius 屬性值警告](visual-studio-2013-web-tools/_static/image25.png "框線-radius 屬性值警告")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="f9dd1-277">*框線-radius 屬性值警告*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="f9dd1-278">移除工具提示所建議的**框線-radius**屬性值單位。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="f9dd1-279">As **border-半徑**是定義圓角框線角落的標準屬性，您可以從 CSS 規則中移除 **-webkit-border-radius**屬性和值。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="f9dd1-280">將插入號放在**自動換行**屬性中，並注意智慧標籤也會出現在下方。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="f9dd1-281">開啟功能表，然後按一下 [**新增遺漏的廠商詳細資訊**]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="f9dd1-282">![新增缺少的廠商詳細資訊建議](visual-studio-2013-web-tools/_static/image26.png "新增缺少的廠商詳細資訊建議")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="f9dd1-283">*新增缺少的廠商詳細資訊建議*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="f9dd1-284">**-Ms-單字 wrap**屬性會自動新增至 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="f9dd1-285">![新增的廠商特定屬性](visual-studio-2013-web-tools/_static/image27.png "新增的廠商特定屬性")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="f9dd1-286">*新增的廠商特定屬性*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="f9dd1-287">工作 4-從瀏覽器更新 HTML 程式碼</span><span class="sxs-lookup"><span data-stu-id="f9dd1-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="f9dd1-288">在這項工作中，您將使用瀏覽器連結的 [**設計模式]** 功能，從瀏覽器編輯 DOM 物件，並將變更傳送至 Visual Studio 中的 HTML 原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="f9dd1-289">在 Google Chrome 中，按**CTRL** + **ALT** + **D**以啟用設計模式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="f9dd1-290">將指標移到**Lorem Ipsum dolor sit amet**標籤上，然後按一下。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="f9dd1-291">![編輯問題](visual-studio-2013-web-tools/_static/image28.png "編輯問題")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="f9dd1-292">*編輯問題*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-292">*Editing the question*</span></span>
3. <span data-ttu-id="f9dd1-293">游標應該會出現。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-293">A cursor should appear.</span></span> <span data-ttu-id="f9dd1-294">*當我撰寫較長的問題時*，將原始文字取代為它看起來的樣子，然後按**ESC**鍵結束設計模式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="f9dd1-295">![已編輯問題](visual-studio-2013-web-tools/_static/image29.png "已編輯問題")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="f9dd1-296">*已編輯問題*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-296">*Question edited*</span></span>
4. <span data-ttu-id="f9dd1-297">切換回 Visual Studio 並開啟 [ **Index**] （如果尚未開啟）。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="f9dd1-298">請注意，已更新 **&lt;p&gt;** 元素的內部文字。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="f9dd1-299">![HTML 網頁中的已更新問題](visual-studio-2013-web-tools/_static/image30.png "HTML 網頁中的已更新問題")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="f9dd1-300">*HTML 網頁中的已更新問題*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="f9dd1-301">工作 5-查看 SEO 相關警告</span><span class="sxs-lookup"><span data-stu-id="f9dd1-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="f9dd1-302">**搜尋引擎優化**（SEO）是在搜尋引擎的結果清單上讓網站排名更高的流程。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="f9dd1-303">網站排名越高，列出的也越一致，網站就會從該搜尋引擎取得更多的訪客。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="f9dd1-304">Web Essentials 包含可檢查 HTML 的分析工具、報告找到的問題，並提供修正的協助。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="f9dd1-305">移至 [ **View** ] 功能表，然後按一下 [**錯誤清單**] 以開啟 [**錯誤清單**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="f9dd1-306">![在 [視圖] 功能表中錯誤清單](visual-studio-2013-web-tools/_static/image31.png "在 [視圖] 功能表中錯誤清單")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="f9dd1-307">*在 [視圖] 功能表中錯誤清單*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="f9dd1-308">請注意，有一個 SEO 警告，會通知頁面描述缺少 **&lt;的中繼&gt;** 標記。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="f9dd1-309">按兩下 [SEO 警告] 專案加以修正。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="f9dd1-310">![錯誤清單視窗](visual-studio-2013-web-tools/_static/image32.png "錯誤清單視窗")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="f9dd1-311">*錯誤清單視窗*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-311">*Error List window*</span></span>
3. <span data-ttu-id="f9dd1-312">在 [ **Web Essentials** ] 對話方塊中，按一下 **[是]** ，將描述插入 &lt;meta&gt; 標記。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="f9dd1-313">![Web 基本知識對話方塊](visual-studio-2013-web-tools/_static/image33.png "Web 基本知識對話方塊")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="f9dd1-314">*Web 基本知識對話方塊*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="f9dd1-315">**\_Layout**的編輯器隨即開啟，而且 **&lt;meta&gt;** 標記會自動加入至 HTML 檔案的**標頭**區段。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="f9dd1-316">![_Layout 頁面中自動新增的中繼標記](visual-studio-2013-web-tools/_static/image34.png "_Layout 頁面中自動新增的中繼標記")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="f9dd1-317">*中繼標記自動新增至 \_版面配置頁*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="f9dd1-318">將**content**屬性的值變更為*GeekQuiz* ，並儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="f9dd1-319">練習2：利用程式碼片段和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="f9dd1-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="f9dd1-320">使用 Web Essentials，HTML 編輯器已透過額外的功能擴充。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="f9dd1-321">在此練習中，您會看到一些有助於開發 web 應用程式的新功能。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="f9dd1-322">工作 1-在 HTML 檔案中使用 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="f9dd1-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="f9dd1-323">您會在這項工作中看到的第一項新功能，稱為**動態 IntelliSense**。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="f9dd1-324">動態 IntelliSense 會讀取其他標記和屬性，以推斷您將使用的可能識別碼。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="f9dd1-325">在這項工作中，您將建立新的 HTML 表單元素，其中包含標籤和輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="f9dd1-326">接著，您會將**for**屬性新增至標籤，以將它系結至輸入，而且您會看到根據範圍內輸入之識別碼的 IntelliSense 建議。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="f9dd1-327">開啟**Web 的 Visual Studio Express 2013** ，以及位於**Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin**資料夾中的**Begin .sln**解決方案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="f9dd1-328">或者，您可以繼續使用您在上一個練習中取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="f9dd1-329">在**方案總管**中，開啟位於**Views** | **Home**資料夾中的**Index. cshtml**檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="f9dd1-330">將下列表單加入&gt;元素的 **&lt;區段**內。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="f9dd1-331">（程式碼片段- *VisualStudio2013WebTooling* - *Ex2* - *格式*）</span><span class="sxs-lookup"><span data-stu-id="f9dd1-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="f9dd1-332">輸入標記前面必須加上具有欄位描述的標籤。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="f9dd1-333">在輸入標記之前新增下列標籤。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="f9dd1-334">**&lt;標籤**的**for**屬性&gt;會指定標籤所系結的表單元素。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="f9dd1-335">屬性的值應該等於相關元素的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="f9dd1-336">將**for**屬性新增至 **&lt;標籤&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="f9dd1-337">如下圖所示，[IntelliSense] 方塊中會顯示 &quot;名稱&quot; 值，這取決於相同範圍內專案的識別碼（封閉的 **&lt;表單&gt;** ）。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="f9dd1-338">![在 IntelliSense 中顯示識別碼](visual-studio-2013-web-tools/_static/image35.png "在 IntelliSense 中顯示識別碼")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="f9dd1-339">*在 IntelliSense 中顯示識別碼*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="f9dd1-340">刪除最近新增的 **&lt;表單&gt;** 元素和其內容。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="f9dd1-341">工作 2-使用 HTML 程式碼片段</span><span class="sxs-lookup"><span data-stu-id="f9dd1-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="f9dd1-342">HTML5 引進了超過25個新的語義標記。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="f9dd1-343">Visual Studio 已經具有這些標記的 IntelliSense 支援，但 Visual Studio 2013 藉由新增程式碼片段，讓您更快速且更輕鬆地撰寫標記。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="f9dd1-344">雖然這些標記並不複雜，但有幾個小微妙差異，例如新增*音訊*標記的正確編解碼器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="f9dd1-345">在這項工作中，您會看到音訊標記的 HTML 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="f9dd1-346">在**Index. cshtml**檔案中，于 **&lt;區段&gt;** 元素內輸入 **&lt;aud** ，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="f9dd1-347">![插入音訊元素](visual-studio-2013-web-tools/_static/image36.png "插入音訊元素")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="f9dd1-348">*插入音訊元素*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="f9dd1-349">按兩次**tab**鍵，並注意如何在頁面上加入下列程式碼，並將游標放在第一個來源的**src**屬性上。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="f9dd1-350">按**tab**鍵兩次，即會插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="f9dd1-351">[音訊] 程式碼片段會顯示*音訊*標記的標準使用方式，並提供兩個原始程式檔來改善支援。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="f9dd1-352">刪除第二行，並使用下列 WebCampsTV Katana show 的連結更新第一行的來源： [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="f9dd1-353">產生的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="f9dd1-354">原始程式檔*KatanaProject*是用來作為範例。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="f9dd1-355">如果您想要的話，可以使用另一個來源。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="f9dd1-356">按**CTRL** + **S**以儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="f9dd1-357">按**CTRL** + **F5**啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="f9dd1-358">請注意，音訊播放機已新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="f9dd1-359">![Internet Explorer 中的音訊播放機](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer 中的音訊播放機")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="f9dd1-360">*Internet Explorer 中的音訊播放機*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="f9dd1-361">![Google Chrome 中的音訊播放機](visual-studio-2013-web-tools/_static/image38.png "Google Chrome 中的音訊播放機")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="f9dd1-362">*Google Chrome 中的音訊播放機*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="f9dd1-363">請勿關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-363">Do not close the browsers.</span></span> <span data-ttu-id="f9dd1-364">您將在下一項工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="f9dd1-365">工作 3-在 JavaScript 檔中使用 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="f9dd1-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="f9dd1-366">使用 Web Essentials 2013，樣式表單和 HTML 網頁會產生識別碼和類別名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="f9dd1-367">在這項工作中，您將瞭解這些清單如何改善 Web Essentials 2013 中的 JavaScript IntelliSense 支援。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="f9dd1-368">在 [ **Index. cshtml** ] 檔案中，加入下列程式碼以定義 JavaScript 程式碼的**腳本**標記。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="f9dd1-369">在**腳本**標記內加入下列程式碼，以定義就緒的回呼函數。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="f9dd1-370">（程式碼片段- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*）</span><span class="sxs-lookup"><span data-stu-id="f9dd1-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="f9dd1-371">將插入號放在**腳本**標記中，然後按**CTRL** +  **。**</span><span class="sxs-lookup"><span data-stu-id="f9dd1-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="f9dd1-372">以開啟 [建議] 功能表。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="f9dd1-373">按一下 [**解壓縮至**檔案]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="f9dd1-374">![JavaScript 解壓縮至檔案建議](visual-studio-2013-web-tools/_static/image39.png "JavaScript 解壓縮至檔案建議")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="f9dd1-375">*JavaScript 解壓縮至檔案建議*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="f9dd1-376">在 [**另存**新檔] 視窗中，選取 [**腳本**] 資料夾，將檔案命名為**Init** ，然後按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="f9dd1-377">![另存新檔視窗](visual-studio-2013-web-tools/_static/image40.png "另存新檔視窗")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="f9dd1-378">*另存新檔視窗*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-379">隨即建立**init .js**檔案，並將腳本的內容移至檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="f9dd1-380">![以包含的內容建立的 Init .js 檔案](visual-studio-2013-web-tools/_static/image41.png "以包含的內容建立的 Init .js 檔案")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="f9dd1-381">*以包含的內容建立的 Init .js 檔案*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="f9dd1-382">開啟**Index. cshtml**檔案，並檢查腳本標記是否已取代為**init .js**檔案的參考。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="f9dd1-383">![Init .js html 參考](visual-studio-2013-web-tools/_static/image42.png "Init .js html 參考")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="f9dd1-384">*Init .js html 參考*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="f9dd1-385">請移至**方案總管**，並注意**init .js**檔案已自動包含在方案中。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="f9dd1-386">![方案中包含的 Init .js 檔案](visual-studio-2013-web-tools/_static/image43.png "方案中包含的 Init .js 檔案")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="f9dd1-387">*方案中包含的 Init .js 檔案*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="f9dd1-388">切換回**init .js**檔案，以更新**就緒**函式回呼。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="f9dd1-389">在傳遞至*ready*的函式回呼定義內，新增下列程式碼以取得特定類別屬性的所有專案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="f9dd1-390">在**getElementsByClassName**函式呼叫內的引號之間，按**CTRL** + **空格鍵**。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="f9dd1-391">![顯示 getElementsByClassName 函式的 IntelliSense](visual-studio-2013-web-tools/_static/image44.png "顯示 getElementsByClassName 函式的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="f9dd1-392">*顯示 getElementsByClassName 函式的 IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-393">請注意，IntelliSense 會顯示專案樣式表單中定義的類別。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="f9dd1-394">以下列程式碼取代您所建立的行。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="f9dd1-395">將游標放在**getElementsByTagName**函式中引號內的**au**後面，然後按**CTRL** + **空格鍵**。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="f9dd1-396">![顯示 getElementByTagName 方法的 IntelliSense](visual-studio-2013-web-tools/_static/image45.png "顯示 getElementByTagName 方法的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="f9dd1-397">*顯示 getElementsByTagName 方法的 IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="f9dd1-398">從清單中選取 **&quot;音訊&quot;** ，然後按**enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="f9dd1-399">其結果如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="f9dd1-400">![正在抓取音訊元素](visual-studio-2013-web-tools/_static/image46.png "正在抓取音訊元素")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="f9dd1-401">*正在抓取音訊元素*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="f9dd1-402">在**方案總管**中，以滑鼠右鍵按一下 [**腳本**] 資料夾中的 [ **init** ] 檔案，然後從 [ **Web Essentials** ] 功能表中選取 [**縮小 JavaScript**檔案]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="f9dd1-403">![縮小 JavaScript 檔案](visual-studio-2013-web-tools/_static/image47.png "縮小 JavaScript 檔案")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="f9dd1-404">*縮小 JavaScript 檔案*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="f9dd1-405">當來源檔案變更時，系統提示您啟用自動縮制時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="f9dd1-406">![啟用自動縮制警告](visual-studio-2013-web-tools/_static/image48.png "啟用自動縮制警告")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="f9dd1-407">*啟用自動縮制警告*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9dd1-408">隨即建立**init. min .js** ，並加入作為**init**檔案的相依性。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="f9dd1-409">![已建立 Init. min .js 檔案](visual-studio-2013-web-tools/_static/image49.png "已建立 Init. min .js 檔案")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="f9dd1-410">*已建立 Init. min .js 檔案*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="f9dd1-411">開啟**init. min .js**檔案，並注意檔案是縮減。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="f9dd1-412">![Init. min .js 檔案內容](visual-studio-2013-web-tools/_static/image50.png "Init. min .js 檔案內容")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="f9dd1-413">*Init. min .js 檔案內容*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="f9dd1-414">在**init .js**檔案中，將下列程式碼新增至**getElementsByTagName**函式呼叫下方，以播放所有的音訊元素。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="f9dd1-415">（程式碼片段- *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*）</span><span class="sxs-lookup"><span data-stu-id="f9dd1-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="f9dd1-416">按一下**CTRL** + **S**以儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="f9dd1-417">由於縮減檔案已開啟，您會看到一個對話方塊，指出檔案已在原始檔編輯器之外修改過。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="f9dd1-418">按一下 [ **是**]。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-418">Click **Yes**.</span></span>

    <span data-ttu-id="f9dd1-419">![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="f9dd1-420">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="f9dd1-421">切換回**init. min .js**檔案，確認已使用新的程式碼更新檔案。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="f9dd1-422">![已更新 Init. 最小 .js 檔案](visual-studio-2013-web-tools/_static/image52.png "已更新 Init. 最小 .js 檔案")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="f9dd1-423">*已更新 Init. 最小 .js 檔案*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="f9dd1-424">按一下 [**瀏覽器連結**重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="f9dd1-425">這兩個瀏覽器都重新整理後，您在上一項工作中看到的音訊播放機將會自動開始播放。</span><span class="sxs-lookup"><span data-stu-id="f9dd1-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="f9dd1-426">![包含在 view 中的音訊播放機](visual-studio-2013-web-tools/_static/image53.png "包含在 view 中的音訊播放機")</span><span class="sxs-lookup"><span data-stu-id="f9dd1-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="f9dd1-427">*包含在 view 中的音訊播放機*</span><span class="sxs-lookup"><span data-stu-id="f9dd1-427">*Audio player included in view*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f9dd1-428">總結</span><span class="sxs-lookup"><span data-stu-id="f9dd1-428">Summary</span></span>

<span data-ttu-id="f9dd1-429">藉由完成此實際操作實驗室，您已瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="f9dd1-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="f9dd1-430">使用 Web Essentials 中包含的新 HTML 編輯器功能，例如豐富的 HTML5 程式碼片段和 Zen 編碼</span><span class="sxs-lookup"><span data-stu-id="f9dd1-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="f9dd1-431">使用 Web Essentials 中包含的新 CSS 編輯器功能，例如色彩選擇器和瀏覽器矩陣工具提示</span><span class="sxs-lookup"><span data-stu-id="f9dd1-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="f9dd1-432">使用 Web Essentials 中包含的新 JavaScript 編輯器功能，例如 [解壓縮至檔案] 和 [IntelliSense]，適用于所有 HTML 元素</span><span class="sxs-lookup"><span data-stu-id="f9dd1-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="f9dd1-433">使用瀏覽器連結在瀏覽器與 Visual Studio 之間交換資料</span><span class="sxs-lookup"><span data-stu-id="f9dd1-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
