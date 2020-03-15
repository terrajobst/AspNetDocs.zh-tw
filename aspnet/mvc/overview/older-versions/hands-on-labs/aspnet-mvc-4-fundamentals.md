---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 基本概念 |Microsoft Docs
author: rick-anderson
description: 這個實際操作實驗室是以 MVC （模型視圖控制器）音樂商店為基礎，這是一項教學課程應用程式，其仲介紹了如何使用 ASP.NET MV 的逐步解說 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598816"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="c7359-103">ASP.NET MVC 4 基本概念</span><span class="sxs-lookup"><span data-stu-id="c7359-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="c7359-104">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="c7359-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="c7359-105">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="c7359-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="c7359-106">這個實際操作實驗室是以 MVC （模型視圖控制器）音樂商店為基礎，這是一種教學課程應用程式，介紹如何使用 ASP.NET MVC 和 Visual Studio 的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="c7359-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="c7359-107">在整個實驗室中，您將學習簡單的功能，但同時使用這些技術。</span><span class="sxs-lookup"><span data-stu-id="c7359-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="c7359-108">您將從簡單的應用程式開始，並將其建立，直到您擁有功能完整的 ASP.NET MVC 4 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="c7359-109">這個實驗室適用于 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="c7359-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="c7359-110">如果您想要探索教學課程應用程式的 ASP.NET MVC 3 版本，您可以在[MVC-音樂存放區](https://github.com/evilDave/MVC-Music-Store)中找到它。</span><span class="sxs-lookup"><span data-stu-id="c7359-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="c7359-111">這個實際操作實驗室假設開發人員有經驗的 Web 開發技術，例如 HTML 和 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="c7359-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="c7359-112">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="c7359-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="c7359-113">此實驗室的特定專案可在[ASP.NET MVC 4 基本](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)概念中取得。</span><span class="sxs-lookup"><span data-stu-id="c7359-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="c7359-114">音樂存放區應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-114">The Music Store application</span></span>

<span data-ttu-id="c7359-115">將在此實驗室中建立的音樂存放區 web 應用程式包含三個主要部分：購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="c7359-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="c7359-116">訪客可以依內容類型流覽專輯、將專輯加入購物車、檢查其選擇，最後繼續簽出以登入並完成訂單。</span><span class="sxs-lookup"><span data-stu-id="c7359-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="c7359-117">此外，存放區系統管理員將能夠管理可用的專輯以及其主要屬性。</span><span class="sxs-lookup"><span data-stu-id="c7359-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="c7359-118">![音樂存放畫面](aspnet-mvc-4-fundamentals/_static/image1.png "音樂存放畫面")</span><span class="sxs-lookup"><span data-stu-id="c7359-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="c7359-119">*音樂存放畫面*</span><span class="sxs-lookup"><span data-stu-id="c7359-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="c7359-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="c7359-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="c7359-121">音樂存放區應用程式將使用**Model View Controller （MVC）** 建立，這是將應用程式分成三個主要元件的架構模式：</span><span class="sxs-lookup"><span data-stu-id="c7359-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="c7359-122">**模型**：模型物件是應用程式中用來執行領域邏輯的元件。</span><span class="sxs-lookup"><span data-stu-id="c7359-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="c7359-123">通常，模型物件也會在資料庫中捕獲和儲存模型狀態。</span><span class="sxs-lookup"><span data-stu-id="c7359-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="c7359-124">**Views：** Views 是顯示應用程式的使用者介面（UI）的元件。</span><span class="sxs-lookup"><span data-stu-id="c7359-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="c7359-125">通常此 UI 是從模型資料建立。</span><span class="sxs-lookup"><span data-stu-id="c7359-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="c7359-126">例如，專輯的編輯檢視會根據專輯物件的目前狀態顯示文字方塊和下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="c7359-127">**控制器：** 控制器是處理使用者互動、操作模型，最後選取要呈現 UI 之視圖的元件。</span><span class="sxs-lookup"><span data-stu-id="c7359-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="c7359-128">在 MVC 應用程式中，檢視只會顯示資訊，而控制器則會處理及回應使用者輸入和互動。</span><span class="sxs-lookup"><span data-stu-id="c7359-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="c7359-129">MVC 模式可協助您建立應用程式，以區隔應用程式的不同層面（輸入邏輯、商務邏輯和 UI 邏輯），同時提供這些元素之間的鬆散結合。</span><span class="sxs-lookup"><span data-stu-id="c7359-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="c7359-130">這種區隔可協助您在建立應用程式時管理複雜性，因為它可讓您一次專注于一層面的執行。</span><span class="sxs-lookup"><span data-stu-id="c7359-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="c7359-131">此外，MVC 模式可讓您輕鬆地測試應用程式，同時也鼓勵使用以測試為導向的開發（TDD）來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="c7359-132">**ASP.NET MVC**架構提供 ASP.NET Web form 模式的替代方案，可用於建立以 MVC 為基礎的 ASP.NET web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="c7359-133">**ASP.NET MVC**架構是輕量、高度可測試的呈現架構，（如同 Web 表單架構應用程式）已與現有的 ASP.NET 功能整合，例如主版頁面和以成員資格為基礎的驗證，因此您可以取得核心 .net framework 的所有威力。</span><span class="sxs-lookup"><span data-stu-id="c7359-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="c7359-134">如果您已經熟悉 ASP.NET Web form，這會很有用，因為您已經使用的所有程式庫也都可在 ASP.NET MVC 4 中取得。</span><span class="sxs-lookup"><span data-stu-id="c7359-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="c7359-135">此外，MVC 應用程式的三個主要元件之間的鬆散耦合也會提升平行開發。</span><span class="sxs-lookup"><span data-stu-id="c7359-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="c7359-136">比方說，有一位開發人員可以使用此視圖，第二位開發人員可以處理控制器邏輯，而第三位開發人員則可以專注于模型中的商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="c7359-137">目標</span><span class="sxs-lookup"><span data-stu-id="c7359-137">Objectives</span></span>

<span data-ttu-id="c7359-138">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="c7359-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="c7359-139">根據音樂存放區應用程式教學課程從頭開始建立 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="c7359-140">新增控制器以處理網站首頁的 Url，並流覽其主要功能</span><span class="sxs-lookup"><span data-stu-id="c7359-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="c7359-141">新增視圖以自訂顯示的內容及其樣式</span><span class="sxs-lookup"><span data-stu-id="c7359-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="c7359-142">新增模型類別以包含及管理資料和網域邏輯</span><span class="sxs-lookup"><span data-stu-id="c7359-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="c7359-143">使用視圖模型模式將控制器動作的資訊傳遞至視圖範本</span><span class="sxs-lookup"><span data-stu-id="c7359-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="c7359-144">探索適用于網際網路應用程式的 ASP.NET MVC 4 新範本</span><span class="sxs-lookup"><span data-stu-id="c7359-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c7359-145">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7359-145">Prerequisites</span></span>

<span data-ttu-id="c7359-146">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="c7359-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="c7359-147">適用于[Web 的 Visual Studio 2012 Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需如何安裝的指示，請參閱[附錄 A](#AppendixA) ）</span><span class="sxs-lookup"><span data-stu-id="c7359-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c7359-148">安裝程式</span><span class="sxs-lookup"><span data-stu-id="c7359-148">Setup</span></span>

<span data-ttu-id="c7359-149">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="c7359-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="c7359-150">為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。</span><span class="sxs-lookup"><span data-stu-id="c7359-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="c7359-151">若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="c7359-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="c7359-152">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 C：使用程式碼片段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="c7359-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c7359-153">練習</span><span class="sxs-lookup"><span data-stu-id="c7359-153">Exercises</span></span>

<span data-ttu-id="c7359-154">這個實際操作實驗室是由下列練習所組成：</span><span class="sxs-lookup"><span data-stu-id="c7359-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="c7359-155">練習1：建立 MusicStore ASP.NET MVC Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="c7359-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="c7359-156">練習2：建立控制器</span><span class="sxs-lookup"><span data-stu-id="c7359-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="c7359-157">練習3：將參數傳遞至控制器</span><span class="sxs-lookup"><span data-stu-id="c7359-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="c7359-158">練習4：建立視圖</span><span class="sxs-lookup"><span data-stu-id="c7359-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="c7359-159">練習5：建立視圖模型</span><span class="sxs-lookup"><span data-stu-id="c7359-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="c7359-160">練習6：使用 View 中的參數</span><span class="sxs-lookup"><span data-stu-id="c7359-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="c7359-161">練習7：膝上圍繞 ASP.NET MVC 4 新範本</span><span class="sxs-lookup"><span data-stu-id="c7359-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="c7359-162">每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="c7359-163">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="c7359-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="c7359-164">完成此實驗室的預估時間： **60 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="c7359-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="c7359-165">練習1：建立 MusicStore ASP.NET MVC Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="c7359-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="c7359-166">在此練習中，您將瞭解如何在 Visual Studio 2012 Express for Web 以及其主要資料夾組織中建立 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="c7359-167">此外，您將學習如何加入新的控制器，並讓它在應用程式的首頁中顯示簡單的字串。</span><span class="sxs-lookup"><span data-stu-id="c7359-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="c7359-168">工作 1-建立 ASP.NET MVC Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="c7359-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="c7359-169">在這項工作中，您將使用 MVC Visual Studio 範本來建立空白的 ASP.NET MVC 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="c7359-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="c7359-170">啟動**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="c7359-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="c7359-171">按一下 [檔案] 功能表上的 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="c7359-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="c7359-172">在 [**新增專案**] 對話方塊中，選取 [ **ASP.NET MVC 4 web 應用程式**] 專案類型，位於 [**視覺效果C#，** **web**範本清單] 底下。</span><span class="sxs-lookup"><span data-stu-id="c7359-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="c7359-173">將**名稱**變更為*MvcMusicStore*。</span><span class="sxs-lookup"><span data-stu-id="c7359-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="c7359-174">將解決方案的位置設定在此練習的源資料夾中新的 **開始**] 資料夾內，例如 **[您的 \Source\Ex01-CreatingMusicStoreProject\Begin**。</span><span class="sxs-lookup"><span data-stu-id="c7359-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="c7359-175">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c7359-175">Click **OK**.</span></span>

    <span data-ttu-id="c7359-176">![[建立新專案] 對話方塊](aspnet-mvc-4-fundamentals/_static/image2.png "[建立新專案] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="c7359-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="c7359-177">*[建立新專案] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c7359-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="c7359-178">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**基本**] 範本，並確定選取的 [**視圖引擎**] 為 [ **Razor**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="c7359-179">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c7359-179">Click **OK**.</span></span>

    <span data-ttu-id="c7359-180">![[新增 ASP.NET MVC 4 專案] 對話方塊](aspnet-mvc-4-fundamentals/_static/image3.png "[新增 ASP.NET MVC 4 專案] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="c7359-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="c7359-181">*[新增 ASP.NET MVC 4 專案] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c7359-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="c7359-182">工作 2-探索方案結構</span><span class="sxs-lookup"><span data-stu-id="c7359-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="c7359-183">ASP.NET MVC 架構包含一個 Visual Studio 專案範本，可協助您建立支援 MVC 模式的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="c7359-184">此範本會建立具有必要資料夾、專案範本和設定檔案專案的新 ASP.NET MVC Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="c7359-185">在這項工作中，您將檢查解決方案結構，以瞭解所牽涉的元素及其關聯性。</span><span class="sxs-lookup"><span data-stu-id="c7359-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="c7359-186">下列資料夾會包含在所有 ASP.NET MVC 應用程式中，因為 ASP.NET MVC 架構預設會使用 &quot;慣例，而不是透過設定&quot; 方法，並根據資料夾命名慣例做出一些預設假設。</span><span class="sxs-lookup"><span data-stu-id="c7359-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="c7359-187">建立專案之後，請檢查在右側的方案總管中建立的資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="c7359-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="c7359-188">![方案總管中的 ASP.NET MVC 資料夾結構](aspnet-mvc-4-fundamentals/_static/image4.png "方案總管中的 ASP.NET MVC 資料夾結構")</span><span class="sxs-lookup"><span data-stu-id="c7359-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="c7359-189">*方案總管中的 ASP.NET MVC 資料夾結構*</span><span class="sxs-lookup"><span data-stu-id="c7359-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="c7359-190">**控制器**。</span><span class="sxs-lookup"><span data-stu-id="c7359-190">**Controllers**.</span></span> <span data-ttu-id="c7359-191">此資料夾將包含控制器類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="c7359-192">在 MVC 架構的應用程式中，控制器會負責處理使用者互動、操作模型，最後選擇要呈現 UI 的視圖。</span><span class="sxs-lookup"><span data-stu-id="c7359-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="c7359-193">MVC framework 需要所有控制器的名稱以 &quot;控制器&quot;結尾，例如 HomeController、LoginController 或 ProductController。</span><span class="sxs-lookup"><span data-stu-id="c7359-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="c7359-194">**模型**。</span><span class="sxs-lookup"><span data-stu-id="c7359-194">**Models**.</span></span> <span data-ttu-id="c7359-195">此資料夾是針對代表 MVC Web 應用程式之應用程式模型的類別所提供。</span><span class="sxs-lookup"><span data-stu-id="c7359-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="c7359-196">這通常包括定義物件的程式碼，以及與資料存放區互動的邏輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="c7359-197">通常實際的模型物件會位於不同的類別庫中。</span><span class="sxs-lookup"><span data-stu-id="c7359-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="c7359-198">不過，當您建立新的應用程式時，您可能會包含類別，然後在開發週期的稍後將它們移至不同的類別庫。</span><span class="sxs-lookup"><span data-stu-id="c7359-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="c7359-199">**Views**。</span><span class="sxs-lookup"><span data-stu-id="c7359-199">**Views**.</span></span> <span data-ttu-id="c7359-200">此資料夾是瀏覽器的建議位置，這是負責顯示應用程式使用者介面的元件。</span><span class="sxs-lookup"><span data-stu-id="c7359-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="c7359-201">Views 會使用 .aspx、.ascx、cshtml 和 .master 檔案，以及任何與轉譯視圖相關的其他檔案。</span><span class="sxs-lookup"><span data-stu-id="c7359-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="c7359-202">Views 資料夾包含每個控制器的資料夾;此資料夾會以控制器名稱前置詞命名。</span><span class="sxs-lookup"><span data-stu-id="c7359-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="c7359-203">例如，如果您有一個名為**HomeController**的控制器，Views 資料夾將會包含一個名為 Home 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7359-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="c7359-204">根據預設，當 ASP.NET MVC 架構載入視圖時，它會在 Views\controllerName 資料夾（**views [controllerName] [action] .aspx**）或 Razor 視圖的（**views [ControllerName] [action]. cshtml**）中尋找要求的視圖名稱的 .aspx 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7359-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c7359-205">除了先前所列的資料夾，MVC Web 應用程式會使用**global.asax**檔案來設定全域 URL 路由預設值，並**使用 web.config 檔案**來設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="c7359-206">工作 3-新增 HomeController</span><span class="sxs-lookup"><span data-stu-id="c7359-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="c7359-207">在不使用 MVC 架構的 ASP.NET 應用程式中，使用者互動會組織在頁面周圍，以及引發和處理來自這些頁面的事件。</span><span class="sxs-lookup"><span data-stu-id="c7359-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="c7359-208">相反地，使用者與 ASP.NET MVC 應用程式的互動會組織在控制器及其動作方法的周圍。</span><span class="sxs-lookup"><span data-stu-id="c7359-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="c7359-209">另一方面，ASP.NET MVC framework 會將 Url 對應至稱為「控制器」的類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="c7359-210">控制器會處理連入要求、處理使用者輸入和互動、執行適當的應用程式邏輯，以及判斷要傳回給用戶端的回應（顯示 HTML、下載檔案、重新導向至不同的 URL 等等）。</span><span class="sxs-lookup"><span data-stu-id="c7359-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="c7359-211">在顯示 HTML 的情況下，控制器類別通常會呼叫個別的 view 元件，以產生要求的 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="c7359-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="c7359-212">在 MVC 應用程式中，檢視只會顯示資訊，而控制器則會處理及回應使用者輸入和互動。</span><span class="sxs-lookup"><span data-stu-id="c7359-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="c7359-213">在這項工作中，您將會新增控制器類別，以處理音樂存放區網站首頁的 Url。</span><span class="sxs-lookup"><span data-stu-id="c7359-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="c7359-214">以滑鼠右鍵按一下方案總管中的 [**控制器**] 資料夾，然後依序選取 [**新增**] 和 [**控制器**命令]：</span><span class="sxs-lookup"><span data-stu-id="c7359-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="c7359-215">![新增控制器命令](aspnet-mvc-4-fundamentals/_static/image5.png "新增控制器命令")</span><span class="sxs-lookup"><span data-stu-id="c7359-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="c7359-216">*新增控制器命令*</span><span class="sxs-lookup"><span data-stu-id="c7359-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="c7359-217">[**新增控制器**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="c7359-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="c7359-218">將控制器命名為*HomeController* ，然後按 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="c7359-219">![[新增控制器] 對話方塊](aspnet-mvc-4-fundamentals/_static/image6.png "[新增控制器] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="c7359-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="c7359-220">*[新增控制器] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c7359-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="c7359-221">檔案**HomeController.cs**會建立在 [**控制器**] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c7359-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="c7359-222">為了讓**HomeController**在其索引動作上傳回字串，請以下列程式碼取代**Index**方法：</span><span class="sxs-lookup"><span data-stu-id="c7359-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="c7359-223">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex1 HomeController 索引*）</span><span class="sxs-lookup"><span data-stu-id="c7359-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c7359-224">工作 4-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="c7359-225">在這項工作中，您將在網頁瀏覽器中試用應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="c7359-226">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="c7359-227">會編譯專案，並啟動本機 IIS Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="c7359-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="c7359-228">本機 IIS Web 服務器會自動開啟網頁瀏覽器，指向網頁伺服器的 URL。</span><span class="sxs-lookup"><span data-stu-id="c7359-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="c7359-229">![在網頁瀏覽器中執行的應用程式](aspnet-mvc-4-fundamentals/_static/image7.png "在網頁瀏覽器中執行的應用程式")</span><span class="sxs-lookup"><span data-stu-id="c7359-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="c7359-230">*在網頁瀏覽器中執行的應用程式*</span><span class="sxs-lookup"><span data-stu-id="c7359-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-231">本機 IIS Web 服務器會以隨機的免費埠號碼來執行網站。</span><span class="sxs-lookup"><span data-stu-id="c7359-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="c7359-232">在上圖中，網站是在 `http://localhost:50103/`執行，因此正在使用埠50103。</span><span class="sxs-lookup"><span data-stu-id="c7359-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="c7359-233">您的埠號碼可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="c7359-233">Your port number may vary.</span></span>
2. <span data-ttu-id="c7359-234">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c7359-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="c7359-235">練習2：建立控制器</span><span class="sxs-lookup"><span data-stu-id="c7359-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="c7359-236">在此練習中，您將瞭解如何更新控制器，以執行音樂存放應用程式的簡單功能。</span><span class="sxs-lookup"><span data-stu-id="c7359-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="c7359-237">該控制器將會定義動作方法，以處理下列每個特定的要求：</span><span class="sxs-lookup"><span data-stu-id="c7359-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="c7359-238">音樂存放區中音樂內容的清單頁面</span><span class="sxs-lookup"><span data-stu-id="c7359-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="c7359-239">一種流覽頁面，其中列出特定內容類型的所有音樂專輯</span><span class="sxs-lookup"><span data-stu-id="c7359-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="c7359-240">顯示特定音樂專輯相關資訊的詳細資料頁面</span><span class="sxs-lookup"><span data-stu-id="c7359-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="c7359-241">針對此練習的範圍，這些動作只會立即傳回字串。</span><span class="sxs-lookup"><span data-stu-id="c7359-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="c7359-242">工作 1-加入新的 StoreController 類別</span><span class="sxs-lookup"><span data-stu-id="c7359-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="c7359-243">在這項工作中，您將加入新的控制器。</span><span class="sxs-lookup"><span data-stu-id="c7359-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="c7359-244">如果尚未開啟，請啟動**VS Express for Web 2012**。</span><span class="sxs-lookup"><span data-stu-id="c7359-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="c7359-245">在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="c7359-246">在 [開啟專案] 對話方塊中，流覽至**Source\Ex02-CreatingAController\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="c7359-247">或者，您可以繼續進行上一個練習完成後取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="c7359-248">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="c7359-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c7359-249">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c7359-250">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c7359-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c7359-251">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c7359-252">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c7359-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c7359-253">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c7359-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c7359-254">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c7359-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="c7359-255">新增控制器。</span><span class="sxs-lookup"><span data-stu-id="c7359-255">Add the new controller.</span></span> <span data-ttu-id="c7359-256">若要這麼做，請在方案總管內的 [**控制器**] 資料夾上按一下滑鼠右鍵，然後依序選取 [**新增**] 和 [**控制器**] 命令。</span><span class="sxs-lookup"><span data-stu-id="c7359-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="c7359-257">將**控制器名稱**變更為*StoreController*，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="c7359-258">![[新增控制器] 對話方塊](aspnet-mvc-4-fundamentals/_static/image8.png "[新增控制器] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="c7359-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="c7359-259">*[新增控制器] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c7359-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="c7359-260">工作 2-修改 StoreController 的動作</span><span class="sxs-lookup"><span data-stu-id="c7359-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="c7359-261">在這項工作中，您將修改稱為「**動作**」的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="c7359-262">動作會負責處理 URL 要求，以及判斷應該傳回給已叫用 URL 之瀏覽器或使用者的內容。</span><span class="sxs-lookup"><span data-stu-id="c7359-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="c7359-263">**StoreController**類別已經有**索引**方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="c7359-264">您稍後會在此實驗室中使用它來執行列出音樂存放區所有內容類型的頁面。</span><span class="sxs-lookup"><span data-stu-id="c7359-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="c7359-265">目前，只要將**Index**方法取代為下列程式碼，即可從 Store. Index （）&quot;傳回字串 &quot;Hello：</span><span class="sxs-lookup"><span data-stu-id="c7359-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="c7359-266">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex2 StoreController 索引*）</span><span class="sxs-lookup"><span data-stu-id="c7359-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="c7359-267">新增**流覽**和**詳細資料**方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="c7359-268">若要這麼做，請將下列程式碼新增至**StoreController**：</span><span class="sxs-lookup"><span data-stu-id="c7359-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="c7359-269">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex2 StoreController BrowseAndDetails*）</span><span class="sxs-lookup"><span data-stu-id="c7359-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="c7359-270">工作 3-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="c7359-271">在這項工作中，您將在網頁瀏覽器中試用應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="c7359-272">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c7359-273">專案會在**首頁**中啟動。</span><span class="sxs-lookup"><span data-stu-id="c7359-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="c7359-274">變更 URL，以確認每個動作的執行。</span><span class="sxs-lookup"><span data-stu-id="c7359-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="c7359-275">**/Store**。</span><span class="sxs-lookup"><span data-stu-id="c7359-275">**/Store**.</span></span> <span data-ttu-id="c7359-276">您會看到 **&quot;Hello 從 Store. Index （）&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="c7359-277">**/Store/Browse**。</span><span class="sxs-lookup"><span data-stu-id="c7359-277">**/Store/Browse**.</span></span> <span data-ttu-id="c7359-278">您會看到**來自 Store. Browse （）&quot;&quot;Hello** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="c7359-279">**/Store/Details**。</span><span class="sxs-lookup"><span data-stu-id="c7359-279">**/Store/Details**.</span></span> <span data-ttu-id="c7359-280">您會看到 **&quot;Hello From Store. Details （）&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="c7359-281">![流覽 StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "流覽 StoreBrowse")</span><span class="sxs-lookup"><span data-stu-id="c7359-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="c7359-282">*流覽/Store/Browse*</span><span class="sxs-lookup"><span data-stu-id="c7359-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="c7359-283">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c7359-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="c7359-284">練習3：將參數傳遞至控制器</span><span class="sxs-lookup"><span data-stu-id="c7359-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="c7359-285">到目前為止，您已從控制器傳回常數位串。</span><span class="sxs-lookup"><span data-stu-id="c7359-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="c7359-286">在此練習中，您將學習如何使用 URL 和 querystring 將參數傳遞至控制器，然後讓方法動作以文字回應瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c7359-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="c7359-287">工作 1-將內容類型參數新增至 StoreController</span><span class="sxs-lookup"><span data-stu-id="c7359-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="c7359-288">在這項工作中，您將使用**querystring**將參數傳送至**StoreController**中的**流覽**動作方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="c7359-289">如果尚未開啟，請啟動**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="c7359-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="c7359-290">在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="c7359-291">在 [開啟專案] 對話方塊中，流覽至**Source\Ex03-PassingParametersToAController\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="c7359-292">或者，您可以繼續進行上一個練習完成後取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="c7359-293">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="c7359-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c7359-294">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c7359-295">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c7359-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c7359-296">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c7359-297">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c7359-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c7359-298">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c7359-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c7359-299">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c7359-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="c7359-300">開啟**StoreController**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-300">Open **StoreController** class.</span></span> <span data-ttu-id="c7359-301">若要這麼做，請在 **方案總管**中展開 **控制器** 資料夾，然後按兩下  **StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="c7359-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="c7359-302">變更**流覽**方法，並新增字串參數來要求特定類型的類型。</span><span class="sxs-lookup"><span data-stu-id="c7359-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="c7359-303">ASP.NET MVC 會在叫用時，自動將名為內容**類型的任何**querystring 或表單 post 參數傳遞至此動作方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="c7359-304">若要這麼做，請使用下列程式碼取代**流覽**方法：</span><span class="sxs-lookup"><span data-stu-id="c7359-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="c7359-305">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex3 StoreController BrowseMethod*）</span><span class="sxs-lookup"><span data-stu-id="c7359-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="c7359-306">您使用的是**HTTPutility.htmlencode. HtmlEncode**公用程式方法，以防止使用者使用/Store/Browse 之類的連結將 JAVAscript 插入此視圖 **？內容類型 =&lt;腳本&gt;視窗。位置 = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="c7359-307">如需進一步說明，請造訪[這篇 msdn 文章](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c7359-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="c7359-308">工作 2-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="c7359-309">在這項工作中，您將在網頁瀏覽器中試用應用程式，並使用內容**類型參數。**</span><span class="sxs-lookup"><span data-stu-id="c7359-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="c7359-310">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c7359-311">專案會在**首頁**中啟動。</span><span class="sxs-lookup"><span data-stu-id="c7359-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="c7359-312">將 URL 變更為 */Store/Browse？內容類型 = Disco* ，用來驗證動作是否會接收內容類型參數。</span><span class="sxs-lookup"><span data-stu-id="c7359-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="c7359-313">![流覽 StoreBrowseGenre = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "流覽 StoreBrowseGenre = Disco")</span><span class="sxs-lookup"><span data-stu-id="c7359-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="c7359-314">*流覽/Store/Browse？內容類型 = Disco*</span><span class="sxs-lookup"><span data-stu-id="c7359-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="c7359-315">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c7359-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="c7359-316">工作 3-新增內嵌在 URL 中的 Id 參數</span><span class="sxs-lookup"><span data-stu-id="c7359-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="c7359-317">在這項工作中，您將使用**URL**將**Id**參數傳遞至**StoreController**的**Details**動作方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="c7359-318">ASP.NET MVC 的預設路由慣例是在動作方法名稱之後，將 URL 的區段視為名為**Id**的參數。如果您的動作方法具有名為 Id 的參數，則 ASP.NET MVC 會自動將 URL 區段當做參數傳遞給您。</span><span class="sxs-lookup"><span data-stu-id="c7359-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="c7359-319">在 URL**存放區/詳細資料/5**中，**識別碼**會解讀為**5**。</span><span class="sxs-lookup"><span data-stu-id="c7359-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="c7359-320">變更**StoreController**的**Details**方法，並新增名為**id**的**int**參數。若要這麼做，請以下列程式碼取代**Details**方法：</span><span class="sxs-lookup"><span data-stu-id="c7359-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="c7359-321">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex3 StoreController DetailsMethod*）</span><span class="sxs-lookup"><span data-stu-id="c7359-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c7359-322">工作 4-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="c7359-323">在這項工作中，您將在網頁瀏覽器中試用應用程式，並使用**Id**參數。</span><span class="sxs-lookup"><span data-stu-id="c7359-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="c7359-324">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c7359-325">專案會在**首頁**中啟動。</span><span class="sxs-lookup"><span data-stu-id="c7359-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="c7359-326">將 URL 變更為 */Store/Details/5* ，以確認動作會收到 id 參數。</span><span class="sxs-lookup"><span data-stu-id="c7359-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="c7359-327">![流覽 StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "流覽 StoreDetails5")</span><span class="sxs-lookup"><span data-stu-id="c7359-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="c7359-328">*流覽/Store/Details/5*</span><span class="sxs-lookup"><span data-stu-id="c7359-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="c7359-329">練習4：建立視圖</span><span class="sxs-lookup"><span data-stu-id="c7359-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="c7359-330">到目前為止，您已從控制器動作傳回字串。</span><span class="sxs-lookup"><span data-stu-id="c7359-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="c7359-331">雖然這是瞭解控制器如何使用的實用方式，但並不是您實際 Web 應用程式的建立方式。</span><span class="sxs-lookup"><span data-stu-id="c7359-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="c7359-332">Views 是元件，可提供更好的方法，讓您使用範本檔案，將 HTML 產生回瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c7359-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="c7359-333">在此練習中，您將學習如何新增版面配置主版頁面，以設定常用 HTML 內容的範本，這是一個可增強網站外觀與風格的樣式表單，最後是一個可讓 HomeController 傳回 HTML 的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c7359-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a><span data-ttu-id="c7359-334">工作 1-修改檔案 \_配置. cshtml</span><span class="sxs-lookup"><span data-stu-id="c7359-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="c7359-335">檔案 **~/Views/Shared/\_layout**可讓您設定通用 HTML 的範本，以在整個網站上使用。</span><span class="sxs-lookup"><span data-stu-id="c7359-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="c7359-336">在這項工作中，您將新增具有通用標題的版面配置主版頁面，其中包含首頁和商店區域的連結。</span><span class="sxs-lookup"><span data-stu-id="c7359-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="c7359-337">如果尚未開啟，請啟動**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="c7359-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="c7359-338">在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="c7359-339">在 [開啟專案] 對話方塊中，流覽至**Source\Ex04-CreatingAView\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="c7359-340">或者，您可以繼續進行上一個練習完成後取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="c7359-341">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="c7359-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c7359-342">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c7359-343">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c7359-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c7359-344">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c7359-345">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c7359-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c7359-346">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c7359-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c7359-347">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c7359-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="c7359-348">檔案<strong>\_layout</strong>包含網站上所有頁面的 HTML 容器版面配置。</span><span class="sxs-lookup"><span data-stu-id="c7359-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="c7359-349">其中包含 HTML 回應的<strong>&lt;html&gt;</strong>元素，以及<strong>&lt;head&gt;</strong>和<strong>&lt;body&gt;</strong>元素。</span><span class="sxs-lookup"><span data-stu-id="c7359-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="c7359-350">HTML 主體中的<strong>@RenderBody（）</strong>會識別視圖範本能夠填入動態內容的區域。</span><span class="sxs-lookup"><span data-stu-id="c7359-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="c7359-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="c7359-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="c7359-352">新增通用標題，其中包含首頁的連結，以及網站中所有頁面上的存放區。</span><span class="sxs-lookup"><span data-stu-id="c7359-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="c7359-353">若要這麼做，請將下列程式碼加入 &lt;body&gt; 語句。</span><span class="sxs-lookup"><span data-stu-id="c7359-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="c7359-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="c7359-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="c7359-355">包含一個 div 來轉譯每個頁面的內文區段。</span><span class="sxs-lookup"><span data-stu-id="c7359-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="c7359-356">將<strong>@RenderBody（）</strong>取代為下列反白顯示的C#程式碼：（）</span><span class="sxs-lookup"><span data-stu-id="c7359-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="c7359-357">您知道嗎？</span><span class="sxs-lookup"><span data-stu-id="c7359-357">Did you know?</span></span> <span data-ttu-id="c7359-358">Visual Studio 2012 具有程式碼片段，可讓您輕鬆地在 HTML、程式碼檔案和更多功能中加入常用的程式碼！</span><span class="sxs-lookup"><span data-stu-id="c7359-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="c7359-359">輸入 **&lt;div&gt;** 並按兩次**tab**鍵，以插入完整的**div**標記來試試看。</span><span class="sxs-lookup"><span data-stu-id="c7359-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="c7359-360">工作 2-新增 CSS 樣式表單</span><span class="sxs-lookup"><span data-stu-id="c7359-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="c7359-361">空白專案範本包含非常簡單的 CSS 檔案，其中只包含用來顯示基本表單和驗證訊息的樣式。</span><span class="sxs-lookup"><span data-stu-id="c7359-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="c7359-362">您將使用其他 CSS 和影像（設計工具可能會提供），以增強網站的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="c7359-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="c7359-363">在這項工作中，您將新增 CSS 樣式表單以定義網站的樣式。</span><span class="sxs-lookup"><span data-stu-id="c7359-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="c7359-364">CSS 檔案和影像會包含在此實驗室的**Source\Assets\Content**資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c7359-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="c7359-365">若要將它們新增至應用程式，請將其內容從**Windows Explorer**視窗拖曳至 Visual Studio Express for Web 中的**方案總管**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7359-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="c7359-366">![拖曳樣式內容](aspnet-mvc-4-fundamentals/_static/image12.png "拖曳樣式內容")</span><span class="sxs-lookup"><span data-stu-id="c7359-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="c7359-367">*拖曳樣式內容*</span><span class="sxs-lookup"><span data-stu-id="c7359-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="c7359-368">隨即會出現警告對話方塊，要求確認取代**網站 .css**檔案和部分現有的影像。</span><span class="sxs-lookup"><span data-stu-id="c7359-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="c7359-369">勾選 [套用**至所有專案**]，然後按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="c7359-370">工作 3-加入視圖範本</span><span class="sxs-lookup"><span data-stu-id="c7359-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="c7359-371">在這項工作中，您將加入一個 View 範本來產生 HTML 回應，以使用此練習中新增的版面配置主版頁面和 CSS。</span><span class="sxs-lookup"><span data-stu-id="c7359-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="c7359-372">若要在流覽網站的首頁時使用視圖範本，您必須先指示，不要傳回字串， **HomeController Index**方法會傳回**View**。</span><span class="sxs-lookup"><span data-stu-id="c7359-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="c7359-373">開啟**HomeController**類別，並將其**Index**方法變更為傳回**ActionResult**，並讓它返回**View （）** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="c7359-374">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex4 HomeController 索引*）</span><span class="sxs-lookup"><span data-stu-id="c7359-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="c7359-375">現在，您需要新增適當的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c7359-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="c7359-376">若要這麼做，請在**索引**動作方法內**按一下滑鼠右鍵**，然後選取 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="c7359-377">這會顯示 [**加入視圖**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c7359-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="c7359-378">![從 Index 方法內加入視圖](aspnet-mvc-4-fundamentals/_static/image13.png "從 Index 方法內加入視圖")</span><span class="sxs-lookup"><span data-stu-id="c7359-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="c7359-379">*從 Index 方法內加入視圖*</span><span class="sxs-lookup"><span data-stu-id="c7359-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="c7359-380">[**加入視圖**] 對話方塊隨即出現，以產生視圖範本檔案。</span><span class="sxs-lookup"><span data-stu-id="c7359-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="c7359-381">根據預設，這個對話方塊會預先填入視圖範本的名稱，使其符合將使用它的動作方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="c7359-382">因為您在 HomeController 內的**索引**動作方法中使用了 [**加入視圖**] 內容功能表，所以 [**加入視圖**] 對話方塊的 [索引] 會是預設的 view name。</span><span class="sxs-lookup"><span data-stu-id="c7359-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="c7359-383">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c7359-383">Click **Add**.</span></span>

    <span data-ttu-id="c7359-384">![[加入視圖] 對話方塊](aspnet-mvc-4-fundamentals/_static/image14.png "[加入視圖] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="c7359-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="c7359-385">*[加入視圖] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c7359-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="c7359-386">Visual Studio 會在**Views\Home**資料夾內產生一個. **cshtml**視圖範本，然後再開啟它。</span><span class="sxs-lookup"><span data-stu-id="c7359-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="c7359-387">![已建立主索引視圖](aspnet-mvc-4-fundamentals/_static/image15.png "已建立主索引視圖")</span><span class="sxs-lookup"><span data-stu-id="c7359-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="c7359-388">*已建立主索引視圖*</span><span class="sxs-lookup"><span data-stu-id="c7359-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-389">**Index. cshtml**檔案的名稱和位置是相關的，並且遵循預設的 ASP.NET MVC 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="c7359-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="c7359-390">資料夾 \Views\**Home*\* 符合控制器名稱（**Home** controller）。</span><span class="sxs-lookup"><span data-stu-id="c7359-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="c7359-391">視圖範本名稱（**索引**）符合將顯示此視圖的控制器動作方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="c7359-392">如此一來，當使用此命名慣例來傳回視圖時，ASP.NET MVC 會避免必須明確指定視圖範本的名稱或位置。</span><span class="sxs-lookup"><span data-stu-id="c7359-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="c7359-393">產生的視圖範本是以稍早定義的 **\_layout. cshtml**範本為基礎。</span><span class="sxs-lookup"><span data-stu-id="c7359-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="c7359-394">將 [ViewBag] 屬性更新為 [**首頁**]，並將主要內容變更為 **[首頁**]，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="c7359-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="c7359-395">在方案總管中選取 [ **MvcMusicStore**專案]，然後按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="c7359-396">工作4：驗證</span><span class="sxs-lookup"><span data-stu-id="c7359-396">Task 4: Verification</span></span>

<span data-ttu-id="c7359-397">若要確認您已正確執行前一個練習中的所有步驟，請依照以下方式進行：</span><span class="sxs-lookup"><span data-stu-id="c7359-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="c7359-398">當應用程式在瀏覽器中開啟時，您應該注意：</span><span class="sxs-lookup"><span data-stu-id="c7359-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="c7359-399">HomeController 的索引動作方法會找到並顯示 **\Views\Home\Index.cshtml** View 範本，即使程式碼稱為**return view （）** ，因為視圖範本會遵循標準命名慣例。</span><span class="sxs-lookup"><span data-stu-id="c7359-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="c7359-400">[首頁] 頁面會顯示在 **\Views\Home\Index.cshtml** view 範本中定義的歡迎訊息。</span><span class="sxs-lookup"><span data-stu-id="c7359-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="c7359-401">首頁使用的是 **\_layout**樣板，因此歡迎訊息包含在標準網站 HTML 版面配置中。</span><span class="sxs-lookup"><span data-stu-id="c7359-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="c7359-402">![使用定義的 LayoutPage 和樣式的主索引視圖](aspnet-mvc-4-fundamentals/_static/image16.png "使用定義的 LayoutPage 和樣式的主索引視圖")</span><span class="sxs-lookup"><span data-stu-id="c7359-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="c7359-403">*使用定義的 LayoutPage 和樣式的主索引視圖*</span><span class="sxs-lookup"><span data-stu-id="c7359-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="c7359-404">練習5：建立視圖模型</span><span class="sxs-lookup"><span data-stu-id="c7359-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="c7359-405">到目前為止，您已將您的視圖顯示成硬式編碼 HTML，但為了建立動態 web 應用程式，視圖範本應該接收來自控制器的資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="c7359-406">要用於該用途的常見技巧之一是**ViewModel**模式，可讓控制器封裝產生適當 HTML 回應所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="c7359-407">在此練習中，您將瞭解如何建立 ViewModel 類別，並新增必要的屬性：存放區中的內容類型，以及這些類型的清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="c7359-408">您也會更新 StoreController 以使用建立的 ViewModel，最後，您將建立新的 View 範本，以在頁面中顯示提到的屬性。</span><span class="sxs-lookup"><span data-stu-id="c7359-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="c7359-409">工作 1-建立 ViewModel 類別</span><span class="sxs-lookup"><span data-stu-id="c7359-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="c7359-410">在這項工作中，您將建立一個 ViewModel 類別，它會實作為「商店內容類型」清單案例。</span><span class="sxs-lookup"><span data-stu-id="c7359-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="c7359-411">如果尚未開啟，請啟動**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="c7359-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="c7359-412">在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="c7359-413">在 [開啟專案] 對話方塊中，流覽至**Source\Ex05-CreatingAViewModel\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="c7359-414">或者，您可以繼續進行上一個練習完成後取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="c7359-415">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="c7359-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c7359-416">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c7359-417">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c7359-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c7359-418">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c7359-419">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c7359-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c7359-420">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c7359-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c7359-421">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c7359-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="c7359-422">建立**viewmodel**資料夾來保存 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="c7359-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="c7359-423">若要這樣做，請以滑鼠右鍵按一下頂層**MvcMusicStore**專案 **，然後依序選取 [** 新增] 和 [**新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="c7359-424">![加入新的資料夾](aspnet-mvc-4-fundamentals/_static/image17.png "加入新的資料夾")</span><span class="sxs-lookup"><span data-stu-id="c7359-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="c7359-425">*加入新的資料夾*</span><span class="sxs-lookup"><span data-stu-id="c7359-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="c7359-426">將資料夾命名為*viewmodel*。</span><span class="sxs-lookup"><span data-stu-id="c7359-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="c7359-427">![方案總管中的 Viewmodel 資料夾](aspnet-mvc-4-fundamentals/_static/image18.png "方案總管中的 Viewmodel 資料夾")</span><span class="sxs-lookup"><span data-stu-id="c7359-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="c7359-428">*方案總管中的 Viewmodel 資料夾*</span><span class="sxs-lookup"><span data-stu-id="c7359-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="c7359-429">建立**ViewModel**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="c7359-430">若要這麼做，請以滑鼠右鍵按一下最近建立的**viewmodel**資料夾 **，然後依序選取 [** 新增] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="c7359-431">在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*StoreIndexViewModel.cs*，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="c7359-432">![加入新的類別](aspnet-mvc-4-fundamentals/_static/image19.png "加入新的類別")</span><span class="sxs-lookup"><span data-stu-id="c7359-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="c7359-433">*加入新的類別*</span><span class="sxs-lookup"><span data-stu-id="c7359-433">*Adding a new Class*</span></span>

    <span data-ttu-id="c7359-434">![建立 StoreIndexViewModel 類別](aspnet-mvc-4-fundamentals/_static/image20.png "建立 StoreIndexViewModel 類別")</span><span class="sxs-lookup"><span data-stu-id="c7359-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="c7359-435">*建立 StoreIndexViewModel 類別*</span><span class="sxs-lookup"><span data-stu-id="c7359-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="c7359-436">工作 2-將屬性新增至 ViewModel 類別</span><span class="sxs-lookup"><span data-stu-id="c7359-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="c7359-437">有兩個參數可從 StoreController 傳遞至 View 範本，以產生預期的 HTML 回應：存放區中的內容組數，以及這些內容的清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="c7359-438">在這項工作中，您會將這**兩個屬性**新增至**StoreIndexViewModel**類別： **NumberOfGenres** （整數）和內容類型（字串清單）。</span><span class="sxs-lookup"><span data-stu-id="c7359-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="c7359-439">將**NumberOfGenres**和**內容**類型屬性新增至**StoreIndexViewModel**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="c7359-440">若要這麼做，請將下列2行新增至類別定義：</span><span class="sxs-lookup"><span data-stu-id="c7359-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="c7359-441">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex5 StoreIndexViewModel 屬性*）</span><span class="sxs-lookup"><span data-stu-id="c7359-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="c7359-442">**{Get; set;}** 標記法會使用C#的自動執行屬性功能。</span><span class="sxs-lookup"><span data-stu-id="c7359-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="c7359-443">它提供屬性的優點，而不需要我們宣告支援欄位。</span><span class="sxs-lookup"><span data-stu-id="c7359-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="c7359-444">工作 3-更新 StoreController 以使用 StoreIndexViewModel</span><span class="sxs-lookup"><span data-stu-id="c7359-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="c7359-445">**StoreIndexViewModel**類別會封裝從**StoreController**的**Index**方法傳遞到 View 範本所需的資訊，以便產生回應。</span><span class="sxs-lookup"><span data-stu-id="c7359-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="c7359-446">在這項工作中，您將更新**StoreController**以使用**StoreIndexViewModel**。</span><span class="sxs-lookup"><span data-stu-id="c7359-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="c7359-447">開啟**StoreController**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="c7359-448">![開啟 StoreController 類別](aspnet-mvc-4-fundamentals/_static/image21.png "開啟 StoreController 類別")</span><span class="sxs-lookup"><span data-stu-id="c7359-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="c7359-449">*開啟 StoreController 類別*</span><span class="sxs-lookup"><span data-stu-id="c7359-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="c7359-450">若要使用**StoreController**中的**StoreIndexViewModel**類別，請在**StoreController**程式碼的頂端新增下列命名空間：</span><span class="sxs-lookup"><span data-stu-id="c7359-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="c7359-451">（程式碼片段- *ASP.NET MVC 4 基本概念-使用 viewmodel 的 Ex5 StoreIndexViewModel*）</span><span class="sxs-lookup"><span data-stu-id="c7359-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="c7359-452">變更**StoreController**的**索引**動作方法，讓它建立並填入**StoreIndexViewModel**物件，然後將它傳遞至 View 範本，以產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="c7359-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-453">在實驗室 &quot;ASP.NET MVC 模型和資料存取&quot; 您會撰寫程式碼，以從資料庫中抓取商店內容清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="c7359-454">在下列程式碼中，您將建立會填入**StoreIndexViewModel**的虛擬資料類型**清單**。</span><span class="sxs-lookup"><span data-stu-id="c7359-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="c7359-455">建立並設定**StoreIndexViewModel**物件之後，它會當做引數傳遞給**View**方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="c7359-456">這表示此視圖範本會使用該物件來產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="c7359-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="c7359-457">以下列程式碼取代**Index**方法：</span><span class="sxs-lookup"><span data-stu-id="c7359-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="c7359-458">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex5 StoreController Index 方法*）</span><span class="sxs-lookup"><span data-stu-id="c7359-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="c7359-459">如果您不熟悉C#，可以假設使用**var**表示**viewModel**變數是晚期繫結。</span><span class="sxs-lookup"><span data-stu-id="c7359-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="c7359-460">這不正確， C#編譯器會根據您指派給變數的內容來使用型別推斷，以判斷**viewModel**的型別是**StoreIndexViewModel**。</span><span class="sxs-lookup"><span data-stu-id="c7359-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="c7359-461">此外，藉由將本機**viewModel**變數編譯為**StoreIndexViewModel**類型，您會取得編譯時期檢查，並 Visual Studio 程式碼編輯器支援。</span><span class="sxs-lookup"><span data-stu-id="c7359-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="c7359-462">工作 4-建立使用 StoreIndexViewModel 的視圖範本</span><span class="sxs-lookup"><span data-stu-id="c7359-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="c7359-463">在這項工作中，您將會建立一個視圖範本，以使用從控制器傳遞的 StoreIndexViewModel 物件來顯示內容清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="c7359-464">在建立新的視圖範本之前，讓我們先建立專案，使 [**加入視圖] 對話方塊**知道**StoreIndexViewModel**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="c7359-465">建立專案，方法是選取 [**建立**] 功能表項目，然後選取 [**建立 MvcMusicStore**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="c7359-466">![建立專案](aspnet-mvc-4-fundamentals/_static/image22.png "建立專案")</span><span class="sxs-lookup"><span data-stu-id="c7359-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="c7359-467">*建立專案*</span><span class="sxs-lookup"><span data-stu-id="c7359-467">*Building the project*</span></span>
2. <span data-ttu-id="c7359-468">建立新的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c7359-468">Create a new View template.</span></span> <span data-ttu-id="c7359-469">若要這麼做，請在**索引**方法內部按一下滑鼠右鍵，然後選取 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="c7359-470">![新增檢視](aspnet-mvc-4-fundamentals/_static/image23.png "新增檢視")</span><span class="sxs-lookup"><span data-stu-id="c7359-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="c7359-471">*新增檢視*</span><span class="sxs-lookup"><span data-stu-id="c7359-471">*Adding a View*</span></span>
3. <span data-ttu-id="c7359-472">因為 [**加入視圖] 對話方塊**是從**StoreController**叫用的，所以預設會在 **\Views\Store\Index.cshtml**檔案中加入視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c7359-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="c7359-473">勾選 [**建立強型別-view** ] 核取方塊，然後選取 [ **StoreIndexViewModel** ] 做為**模型類別**。</span><span class="sxs-lookup"><span data-stu-id="c7359-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="c7359-474">此外，請確定選取的 View engine 是**Razor**。</span><span class="sxs-lookup"><span data-stu-id="c7359-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="c7359-475">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c7359-475">Click **Add**.</span></span>

    <span data-ttu-id="c7359-476">![[加入視圖] 對話方塊](aspnet-mvc-4-fundamentals/_static/image24.png "[加入視圖] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="c7359-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="c7359-477">*[加入視圖] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c7359-477">*Add View Dialog*</span></span>

    <span data-ttu-id="c7359-478">隨即建立並開啟 **\Views\Store\Index.cshtml** View 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="c7359-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="c7359-479">根據在最後一個步驟中提供給 [**加入視圖**] 對話方塊的資訊，View 範本會預期**StoreIndexViewModel**實例會當做用來產生 HTML 回應的資料。</span><span class="sxs-lookup"><span data-stu-id="c7359-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="c7359-480">您會注意到範本會繼承中C#的 `ViewPage<musicstore.viewmodels.storeindexviewmodel>`。</span><span class="sxs-lookup"><span data-stu-id="c7359-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="c7359-481">工作 5-更新視圖範本</span><span class="sxs-lookup"><span data-stu-id="c7359-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="c7359-482">在這項工作中，您將更新在上一個工作中建立的視圖範本，以抓取頁面中的內容和名稱的數目。</span><span class="sxs-lookup"><span data-stu-id="c7359-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="c7359-483">您將使用 @ 語法（通常稱為 &quot;程式碼區塊&quot;）來執行 View 範本中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c7359-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="c7359-484">在 [**存放區**] 資料夾中的**索引. cshtml**檔案中，將其程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="c7359-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="c7359-485">在**StoreIndexViewModel**中的內容類型清單上迴圈，並使用**FOREACH**迴圈建立 HTML **&lt;ul&gt;** 清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="c7359-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="c7359-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="c7359-487">按**F5**執行應用程式並流覽 **/Store**。</span><span class="sxs-lookup"><span data-stu-id="c7359-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="c7359-488">您會在**StoreIndexViewModel**物件中看到從**StoreController**傳遞至 View 範本的內容清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="c7359-489">![顯示內容清單的視圖](aspnet-mvc-4-fundamentals/_static/image26.png "顯示內容清單的視圖")</span><span class="sxs-lookup"><span data-stu-id="c7359-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="c7359-490">*顯示內容清單的視圖*</span><span class="sxs-lookup"><span data-stu-id="c7359-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="c7359-491">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c7359-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="c7359-492">練習6：使用 View 中的參數</span><span class="sxs-lookup"><span data-stu-id="c7359-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="c7359-493">在練習3中，您已瞭解如何將參數傳遞至控制器。</span><span class="sxs-lookup"><span data-stu-id="c7359-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="c7359-494">在此練習中，您將瞭解如何在 View 範本中使用這些參數。</span><span class="sxs-lookup"><span data-stu-id="c7359-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="c7359-495">基於這個目的，您將會先引進模型類別，協助您管理資料和領域邏輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="c7359-496">此外，您將學習如何在 ASP.NET MVC 應用程式內建立頁面的連結，而不需要擔心 URL 路徑編碼之類的事情。</span><span class="sxs-lookup"><span data-stu-id="c7359-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="c7359-497">工作 1-加入模型類別</span><span class="sxs-lookup"><span data-stu-id="c7359-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="c7359-498">不同于 Viewmodel，只是為了將資訊從控制器傳遞至視圖，而建立模型類別是為了包含及管理資料和網域邏輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="c7359-499">在這項工作中，您將新增兩個模型類別來表示這些**概念：內容**類型和**專輯**。</span><span class="sxs-lookup"><span data-stu-id="c7359-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="c7359-500">如果尚未開啟，請啟動**VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="c7359-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="c7359-501">在 [檔案 **] 功能表中，選擇 [** **開啟專案**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="c7359-502">在 [開啟專案] 對話方塊中，流覽至**Source\Ex06-UsingParametersInView\Begin**，選取 [**開始**]，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="c7359-503">或者，您可以繼續進行上一個練習完成後取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="c7359-504">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="c7359-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c7359-505">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c7359-506">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="c7359-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c7359-507">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c7359-508">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="c7359-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c7359-509">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c7359-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c7359-510">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c7359-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="c7359-511">加入內容**類型模型類別**。</span><span class="sxs-lookup"><span data-stu-id="c7359-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="c7359-512">若要這麼做，請以滑鼠右鍵按一下**方案總管**中的 [**模型**] 資料夾，然後依序選取 [**加入**] 和 [**新增專案**] 選項。</span><span class="sxs-lookup"><span data-stu-id="c7359-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="c7359-513">在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*Genre.cs*，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="c7359-514">![新增類別](aspnet-mvc-4-fundamentals/_static/image27.png "新增類別")</span><span class="sxs-lookup"><span data-stu-id="c7359-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="c7359-515">*加入新專案*</span><span class="sxs-lookup"><span data-stu-id="c7359-515">*Adding a new item*</span></span>

    <span data-ttu-id="c7359-516">![加入內容類型模型類別](aspnet-mvc-4-fundamentals/_static/image28.png "加入內容類型模型類別")</span><span class="sxs-lookup"><span data-stu-id="c7359-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="c7359-517">*加入內容類型模型類別*</span><span class="sxs-lookup"><span data-stu-id="c7359-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="c7359-518">將 [**名稱**] 屬性加入至 [內容類型] 類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="c7359-519">若要這麼做，請新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c7359-519">To do this, add the following code:</span></span>

    <span data-ttu-id="c7359-520">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex6*內容類型）</span><span class="sxs-lookup"><span data-stu-id="c7359-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="c7359-521">遵循與先前相同的程式，加入**專輯**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="c7359-522">若要這麼做，請以滑鼠右鍵按一下**方案總管**中的 [**模型**] 資料夾，然後依序選取 [**加入**] 和 [**新增專案**] 選項。</span><span class="sxs-lookup"><span data-stu-id="c7359-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="c7359-523">在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*Album.cs*，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="c7359-524">將兩個屬性新增至專輯類別 **：內容**類型和**標題**。</span><span class="sxs-lookup"><span data-stu-id="c7359-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="c7359-525">若要這麼做，請新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c7359-525">To do this, add the following code:</span></span>

    <span data-ttu-id="c7359-526">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 專輯*）</span><span class="sxs-lookup"><span data-stu-id="c7359-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="c7359-527">工作 2-新增 StoreBrowseViewModel</span><span class="sxs-lookup"><span data-stu-id="c7359-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="c7359-528">此工作中將會使用**StoreBrowseViewModel**來顯示符合所選類型的專輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="c7359-529">在這項工作中，您將建立此類別，然後新增兩個屬性來處理內容**類型和其** **專輯**清單。</span><span class="sxs-lookup"><span data-stu-id="c7359-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="c7359-530">新增**StoreBrowseViewModel**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="c7359-531">若要這麼做，請以滑鼠右鍵按一下**方案總管**中的 [ **viewmodel** ] 資料夾 **，然後依序選取 [** 新增] 和 [**新專案**] 選項。</span><span class="sxs-lookup"><span data-stu-id="c7359-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="c7359-532">在 [程式**代碼**] 底下選擇**類別**專案，並將檔案命名為*StoreBrowseViewModel.cs*，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="c7359-533">在**StoreBrowseViewModel**類別中加入模型的參考。</span><span class="sxs-lookup"><span data-stu-id="c7359-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="c7359-534">若要這麼做，請使用命名空間新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="c7359-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="c7359-535">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 UsingModel*）</span><span class="sxs-lookup"><span data-stu-id="c7359-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="c7359-536">將兩個屬性新增至 StoreBrowseViewModel**類別：內容**類型和**專輯**。</span><span class="sxs-lookup"><span data-stu-id="c7359-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="c7359-537">若要這麼做，請新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c7359-537">To do this, add the following code:</span></span>

    <span data-ttu-id="c7359-538">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 ModelProperties*）</span><span class="sxs-lookup"><span data-stu-id="c7359-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="c7359-539">什麼是 **&lt;專輯&gt;清單**？：此定義使用**清單&lt;t&gt;** 類型，其中**t**會限制此**清單**元素所屬的類型，在此案例中為**專輯**（或其子系）。</span><span class="sxs-lookup"><span data-stu-id="c7359-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="c7359-540">設計類別和方法以延遲一或多個類型的規格，直到用戶端程式代碼宣告並具現化類別或方法，這項功能就是C#稱為**泛型**的語言之一。</span><span class="sxs-lookup"><span data-stu-id="c7359-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="c7359-541">**清單&lt;t&gt;** 是**ArrayList**類型的泛型對應項，而且可以在**system.string 命名空間中使用。**</span><span class="sxs-lookup"><span data-stu-id="c7359-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="c7359-542">使用**泛型**的優點之一，是因為指定了型別，所以您不需要處理型別檢查作業，像是使用**ArrayList**來將元素轉換成**專輯**一樣。</span><span class="sxs-lookup"><span data-stu-id="c7359-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="c7359-543">工作 3-在 StoreController 中使用新的 ViewModel</span><span class="sxs-lookup"><span data-stu-id="c7359-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="c7359-544">在這項工作中，您將修改**StoreController**的 **[流覽] 和 [** **詳細資料**] 動作方法，以使用新的**StoreBrowseViewModel**。</span><span class="sxs-lookup"><span data-stu-id="c7359-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="c7359-545">將參考新增至**StoreController**類別中的 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7359-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="c7359-546">若要這麼做，請展開 **方案總管**中的 **控制器** 資料夾，然後開啟**StoreController**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="c7359-547">然後新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c7359-547">Then add the following code:</span></span>

    <span data-ttu-id="c7359-548">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 UsingModelInController*）</span><span class="sxs-lookup"><span data-stu-id="c7359-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="c7359-549">取代**流覽**動作方法以使用**StoreViewBrowseController**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="c7359-550">您將建立具有虛擬資料的內容類型和兩個新的專輯物件（在下一個實際操作實驗室中，您將會取用資料庫中的實際資料）。</span><span class="sxs-lookup"><span data-stu-id="c7359-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="c7359-551">若要這麼做，請使用下列程式碼取代**流覽**方法：</span><span class="sxs-lookup"><span data-stu-id="c7359-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="c7359-552">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 BrowseMethod*）</span><span class="sxs-lookup"><span data-stu-id="c7359-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="c7359-553">取代**Details**動作方法以使用**StoreViewBrowseController**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="c7359-554">您將建立新的**專輯**物件，以傳回給**視圖**。</span><span class="sxs-lookup"><span data-stu-id="c7359-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="c7359-555">若要這麼做，請以下列程式碼取代**Details**方法：</span><span class="sxs-lookup"><span data-stu-id="c7359-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="c7359-556">（程式碼片段- *ASP.NET MVC 4 基本概念-Ex6 DetailsMethod*）</span><span class="sxs-lookup"><span data-stu-id="c7359-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="c7359-557">工作 4-加入流覽視圖範本</span><span class="sxs-lookup"><span data-stu-id="c7359-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="c7359-558">在這項工作中，您將新增 **[流覽]** 視圖，以顯示找到特定類型的專輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="c7359-559">在建立新的視圖範本之前，您應該先建立專案，讓 [**加入視圖**] 對話方塊知道要使用的**ViewModel**類別。</span><span class="sxs-lookup"><span data-stu-id="c7359-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="c7359-560">建立專案，方法是選取 [**建立**] 功能表項目，然後選取 [**建立 MvcMusicStore**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="c7359-561">新增 **[流覽]** 視圖。</span><span class="sxs-lookup"><span data-stu-id="c7359-561">Add a **Browse** View.</span></span> <span data-ttu-id="c7359-562">若要這麼做，請在**StoreController**的 [**流覽動作]** 方法中按一下滑鼠右鍵，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="c7359-563">在 [**加入視圖**] 對話方塊中，確認視圖名稱為 **[流覽]** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="c7359-564">勾選 [**建立強型別視圖**] 核取方塊，然後從 [**模型類別**] 下拉式清單中選取 [ **StoreBrowseViewModel** ]。</span><span class="sxs-lookup"><span data-stu-id="c7359-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="c7359-565">將其他欄位保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="c7359-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="c7359-566">然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="c7359-566">Then click **Add**.</span></span>

    <span data-ttu-id="c7359-567">![加入流覽視圖](aspnet-mvc-4-fundamentals/_static/image29.png "加入流覽視圖")</span><span class="sxs-lookup"><span data-stu-id="c7359-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="c7359-568">*加入流覽視圖*</span><span class="sxs-lookup"><span data-stu-id="c7359-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="c7359-569">修改**Browse**以顯示內容類型的資訊，並存取傳遞至視圖範本的**StoreBrowseViewModel**物件。</span><span class="sxs-lookup"><span data-stu-id="c7359-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="c7359-570">若要這麼做，請將內容取代為下列各C#項：（）</span><span class="sxs-lookup"><span data-stu-id="c7359-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c7359-571">工作 5-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="c7359-572">在這項工作中，您將測試**流覽**方法從**流覽**方法動作中抓取專輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="c7359-573">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c7359-574">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="c7359-574">The project starts in the Home page.</span></span> <span data-ttu-id="c7359-575">將 URL 變更為 **/Store/Browse？內容類型 = Disco** ，用以確認動作會傳回兩個專輯。</span><span class="sxs-lookup"><span data-stu-id="c7359-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="c7359-576">![流覽存放區 Disco 專輯](aspnet-mvc-4-fundamentals/_static/image30.png "流覽存放區 Disco 專輯")</span><span class="sxs-lookup"><span data-stu-id="c7359-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="c7359-577">*流覽存放區 Disco 專輯*</span><span class="sxs-lookup"><span data-stu-id="c7359-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="c7359-578">工作 6-顯示特定專輯的相關資訊</span><span class="sxs-lookup"><span data-stu-id="c7359-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="c7359-579">在這項工作中，您將會執行 [ **Store/Details** ] 視圖，以顯示特定專輯的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="c7359-580">在這個實際操作的實驗室中，您將會看到有關專輯的所有內容，都已經包含在**View**範本中。</span><span class="sxs-lookup"><span data-stu-id="c7359-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="c7359-581">因此，您不需要建立**StoreDetailsViewModel**類別，而是使用目前的**StoreBrowseViewModel**範本將專輯傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="c7359-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="c7359-582">如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。</span><span class="sxs-lookup"><span data-stu-id="c7359-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="c7359-583">為**StoreController**的**詳細資料**動作方法新增新的**詳細資料**視圖。</span><span class="sxs-lookup"><span data-stu-id="c7359-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="c7359-584">若要這樣做，請以滑鼠右鍵按一下 [ **StoreController** ] 類別中的**詳細資料**方法，然後按一下 [**新增視圖**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="c7359-585">在 [**加入視圖**] 對話方塊中，確認**視圖名稱**為 [**詳細資料**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="c7359-586">勾選 [**建立強型別視圖**] 核取方塊，然後從 [**模型類別**] 下拉式方塊中選取 [**專輯**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="c7359-587">將其他欄位保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="c7359-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="c7359-588">然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="c7359-588">Then click **Add**.</span></span> <span data-ttu-id="c7359-589">這會建立並開啟 **\Views\Store\Details.cshtml**檔案。</span><span class="sxs-lookup"><span data-stu-id="c7359-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="c7359-590">![新增詳細資料檢視](aspnet-mvc-4-fundamentals/_static/image31.png "新增詳細資料檢視")</span><span class="sxs-lookup"><span data-stu-id="c7359-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="c7359-591">*新增詳細資料檢視*</span><span class="sxs-lookup"><span data-stu-id="c7359-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="c7359-592">修改**Details**檔案以顯示專輯資訊，存取傳遞至 view 範本的**專輯**物件。</span><span class="sxs-lookup"><span data-stu-id="c7359-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="c7359-593">若要這麼做，請將內容取代為下列各C#項：（）</span><span class="sxs-lookup"><span data-stu-id="c7359-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="c7359-594">工作 7-執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="c7359-595">在這項工作中，您將測試**詳細資料**視圖是否從**details 動作**方法中抓取專輯資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="c7359-596">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c7359-597">專案會在**首頁**中啟動。</span><span class="sxs-lookup"><span data-stu-id="c7359-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="c7359-598">將 URL 變更為 **/Store/Details/5** ，以驗證專輯的資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="c7359-599">![流覽專輯詳細資料](aspnet-mvc-4-fundamentals/_static/image32.png "流覽專輯詳細資料")</span><span class="sxs-lookup"><span data-stu-id="c7359-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="c7359-600">*流覽專輯的詳細資料*</span><span class="sxs-lookup"><span data-stu-id="c7359-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="c7359-601">工作 8-在頁面之間新增連結</span><span class="sxs-lookup"><span data-stu-id="c7359-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="c7359-602">在這項工作中，您會在 [存放區] 視圖中新增連結，讓每個內容類型名稱中的連結都具有適當的 **/Store/Browse** URL。</span><span class="sxs-lookup"><span data-stu-id="c7359-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="c7359-603">如此一來，當您按一下內容類型（例如**Disco**）時，它會流覽至 **/Store/Browse？內容類型 = Disco** URL。</span><span class="sxs-lookup"><span data-stu-id="c7359-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="c7359-604">如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。</span><span class="sxs-lookup"><span data-stu-id="c7359-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="c7359-605">更新 [**索引**] 頁面，將連結新增至**流覽**頁面。</span><span class="sxs-lookup"><span data-stu-id="c7359-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="c7359-606">若要這麼做，請在**方案總管**展開 [ **Views** ] 資料夾，然後按一下 [ **Store** ] 資料夾，再按兩下 [ **Index. cshtml** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="c7359-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="c7359-607">新增 [流覽] 視圖的連結，指出已選取的內容類型。</span><span class="sxs-lookup"><span data-stu-id="c7359-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="c7359-608">若要這麼做，請將下列反白顯示的程式碼取代為 **&lt;li&gt;** 標記：（C#）</span><span class="sxs-lookup"><span data-stu-id="c7359-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="c7359-609">另一種方法是直接連結到頁面，其程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7359-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="c7359-610">&lt;href =&quot;/Store/Browse？內容類型 =@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="c7359-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="c7359-611">雖然這種方法可行，但它相依于硬式編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="c7359-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="c7359-612">如果您稍後重新命名控制器，就必須手動變更此指令。</span><span class="sxs-lookup"><span data-stu-id="c7359-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="c7359-613">更好的替代方式是使用**HTML Helper**方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="c7359-614">ASP.NET MVC 包含適用于這類工作的 HTML Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="c7359-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="c7359-615">**.Html （）** helper 方法可讓您輕鬆地建立 html **&lt;&gt;** 連結，確保 url 路徑的 url 編碼正確。</span><span class="sxs-lookup"><span data-stu-id="c7359-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="c7359-616">Html.actionlink 有數個多載。</span><span class="sxs-lookup"><span data-stu-id="c7359-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="c7359-617">在此練習中，您將使用接受三個參數的其中一個：</span><span class="sxs-lookup"><span data-stu-id="c7359-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="c7359-618">連結文字，會顯示內容類型名稱</span><span class="sxs-lookup"><span data-stu-id="c7359-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="c7359-619">控制器動作名稱（**流覽**）</span><span class="sxs-lookup"><span data-stu-id="c7359-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="c7359-620">路由參數值，同時指定**名稱（內容**類型）和值（內容類型**名稱**）</span><span class="sxs-lookup"><span data-stu-id="c7359-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="c7359-621">工作 9-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="c7359-622">在這項工作中，您將測試每個內容類型是否顯示，並附有適當 **/Store/Browse** URL 的連結。</span><span class="sxs-lookup"><span data-stu-id="c7359-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="c7359-623">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c7359-624">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="c7359-624">The project starts in the Home page.</span></span> <span data-ttu-id="c7359-625">將 URL 變更為 **/Store** ，以確認每個內容類型都連結到適當的 **/Store/Browse** URL。</span><span class="sxs-lookup"><span data-stu-id="c7359-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="c7359-626">![流覽具有流覽頁面連結的內容內容](aspnet-mvc-4-fundamentals/_static/image33.png "流覽具有流覽頁面連結的內容內容")</span><span class="sxs-lookup"><span data-stu-id="c7359-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="c7359-627">*流覽具有流覽頁面連結的內容內容*</span><span class="sxs-lookup"><span data-stu-id="c7359-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="c7359-628">工作 10-使用動態 ViewModel 集合來傳遞值</span><span class="sxs-lookup"><span data-stu-id="c7359-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="c7359-629">在這項工作中，您將學習簡單且功能強大的方法，以便在控制器和視圖之間傳遞值，而不需要在模型中進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="c7359-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="c7359-630">ASP.NET MVC 4 提供集合 &quot;ViewModel&quot;，可以指派給任何動態值，並在控制器和 views 內進行存取。</span><span class="sxs-lookup"><span data-stu-id="c7359-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="c7359-631">您現在將使用 ViewBag 動態集合，將從控制器&quot; 的 &quot;**加星號**內容清單傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="c7359-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="c7359-632">[存放區索引] 視圖將會存取**ViewModel**並顯示資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="c7359-633">如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。</span><span class="sxs-lookup"><span data-stu-id="c7359-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="c7359-634">開啟**StoreController.cs**並修改**Index**方法，以在 ViewModel 集合中建立加星號的內容清單：</span><span class="sxs-lookup"><span data-stu-id="c7359-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="c7359-635">您也可以使用語法**ViewBag [&quot;加星號&quot;]** 來存取屬性。</span><span class="sxs-lookup"><span data-stu-id="c7359-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="c7359-636">此實驗室的**Source\Assets\Images**資料夾中包含 **&quot;&quot;加星號**的星星圖示。</span><span class="sxs-lookup"><span data-stu-id="c7359-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="c7359-637">若要將其新增至應用程式，請將其內容從**Windows Explorer**視窗拖曳至 Visual Web Developer Express 中的**方案總管**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7359-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="c7359-638">![將星形影像新增至解決方案](aspnet-mvc-4-fundamentals/_static/image34.png "將星形影像新增至解決方案")</span><span class="sxs-lookup"><span data-stu-id="c7359-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="c7359-639">*將星形影像新增至解決方案*</span><span class="sxs-lookup"><span data-stu-id="c7359-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="c7359-640">開啟 view **Store/Index. cshtml**並修改內容。</span><span class="sxs-lookup"><span data-stu-id="c7359-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="c7359-641">您將讀取**ViewBag**集合中的 &quot;加星號&quot; 屬性，並詢問目前的內容類型名稱是否在清單中。</span><span class="sxs-lookup"><span data-stu-id="c7359-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="c7359-642">在此情況下，您會向 [內容類型] 連結顯示星形圖示。</span><span class="sxs-lookup"><span data-stu-id="c7359-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="c7359-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="c7359-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="c7359-644">工作 11-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="c7359-645">在這項工作中，您將測試加星號的內容內容是否顯示星形圖示。</span><span class="sxs-lookup"><span data-stu-id="c7359-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="c7359-646">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c7359-647">專案會在**首頁**中啟動。</span><span class="sxs-lookup"><span data-stu-id="c7359-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="c7359-648">將 URL 變更為 **/Store** ，以確認每個精選的內容類型都具有 [遵循] 標籤：</span><span class="sxs-lookup"><span data-stu-id="c7359-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="c7359-649">![使用加星號專案流覽內容流派](aspnet-mvc-4-fundamentals/_static/image35.png "使用加星號專案流覽內容流派")</span><span class="sxs-lookup"><span data-stu-id="c7359-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="c7359-650">*使用加星號專案流覽內容流派*</span><span class="sxs-lookup"><span data-stu-id="c7359-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="c7359-651">練習7：膝上圍繞 ASP.NET MVC 4 新範本</span><span class="sxs-lookup"><span data-stu-id="c7359-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="c7359-652">在此練習中，您將探索 ASP.NET MVC 4 專案範本中的增強功能，並查看新範本最相關的功能。</span><span class="sxs-lookup"><span data-stu-id="c7359-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="c7359-653">工作1：探索 ASP.NET MVC 4 網際網路應用程式範本</span><span class="sxs-lookup"><span data-stu-id="c7359-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="c7359-654">如果尚未開啟，請啟動**VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="c7359-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="c7359-655">選取檔案 **|新增 |[專案**] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="c7359-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="c7359-656">在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |Web**範本：在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="c7359-657">將專案**命名**為*MusicStore* ，並將**方案名稱**更新為 [*開始*]，然後選取位置（或保留預設值），然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="c7359-658">![建立新的 ASP.NET MVC 4 專案](aspnet-mvc-4-fundamentals/_static/image36.png "建立新的 ASP.NET MVC 4 專案")</span><span class="sxs-lookup"><span data-stu-id="c7359-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="c7359-659">*建立新的 ASP.NET MVC 4 專案*</span><span class="sxs-lookup"><span data-stu-id="c7359-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="c7359-660">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 專案範本，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="c7359-661">請注意，您可以選取 Razor 或 ASPX 做為 view engine。</span><span class="sxs-lookup"><span data-stu-id="c7359-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="c7359-662">![建立新的 ASP.NET MVC 4 網際網路應用程式](aspnet-mvc-4-fundamentals/_static/image37.png "建立新的 ASP.NET MVC 4 網際網路應用程式")</span><span class="sxs-lookup"><span data-stu-id="c7359-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="c7359-663">*建立新的 ASP.NET MVC 4 網際網路應用程式*</span><span class="sxs-lookup"><span data-stu-id="c7359-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-664">Razor 語法已在 ASP.NET MVC 3 中引進。</span><span class="sxs-lookup"><span data-stu-id="c7359-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="c7359-665">其目標是要將檔案中所需的字元和按鍵數目降至最低，以啟用快速且流暢的程式碼撰寫工作流程。</span><span class="sxs-lookup"><span data-stu-id="c7359-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="c7359-666">Razor 利用現有C#的/VB （或其他）語言技能，並提供範本標記語法來啟用絕佳的 HTML 結構工作流程。</span><span class="sxs-lookup"><span data-stu-id="c7359-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="c7359-667">按**F5**執行方案，並查看已更新的範本。</span><span class="sxs-lookup"><span data-stu-id="c7359-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="c7359-668">您可以查看下列功能：</span><span class="sxs-lookup"><span data-stu-id="c7359-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="c7359-669">**現代化樣式範本**</span><span class="sxs-lookup"><span data-stu-id="c7359-669">**Modern-style templates**</span></span>

        <span data-ttu-id="c7359-670">這些範本已更新，提供更現代化的樣式。</span><span class="sxs-lookup"><span data-stu-id="c7359-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="c7359-671">![ASP.NET MVC 4 風貌範本](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 風貌範本")</span><span class="sxs-lookup"><span data-stu-id="c7359-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="c7359-672">*ASP.NET MVC 4 風貌範本*</span><span class="sxs-lookup"><span data-stu-id="c7359-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="c7359-673">**適應性呈現**</span><span class="sxs-lookup"><span data-stu-id="c7359-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="c7359-674">查看調整瀏覽器視窗的大小，並注意頁面配置如何動態適應新的視窗大小。</span><span class="sxs-lookup"><span data-stu-id="c7359-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="c7359-675">這些範本會使用自動調整轉譯技術，在桌上型電腦和行動平臺中正確轉譯，而不需要任何自訂。</span><span class="sxs-lookup"><span data-stu-id="c7359-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="c7359-676">![不同瀏覽器大小的 ASP.NET MVC 4 專案範本](aspnet-mvc-4-fundamentals/_static/image39.png "不同瀏覽器大小的 ASP.NET MVC 4 專案範本")</span><span class="sxs-lookup"><span data-stu-id="c7359-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="c7359-677">*不同瀏覽器大小的 ASP.NET MVC 4 專案範本*</span><span class="sxs-lookup"><span data-stu-id="c7359-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="c7359-678">關閉瀏覽器以停止偵錯工具，並返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c7359-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="c7359-679">現在您可以流覽解決方案，並查看 ASP.NET MVC 4 在專案範本中引進的一些新功能。</span><span class="sxs-lookup"><span data-stu-id="c7359-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="c7359-680">![ASP.NET MVC4-網際網路-應用程式-專案範本](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 網際網路應用程式專案範本")</span><span class="sxs-lookup"><span data-stu-id="c7359-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="c7359-681">*ASP.NET MVC 4 網際網路應用程式專案範本*</span><span class="sxs-lookup"><span data-stu-id="c7359-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="c7359-682">**HTML5 標記**</span><span class="sxs-lookup"><span data-stu-id="c7359-682">**HTML5 markup**</span></span>

       <span data-ttu-id="c7359-683">流覽範本視圖以找出新的主題標記，例如，在**主**資料夾內開啟**About. cshtml** view。</span><span class="sxs-lookup"><span data-stu-id="c7359-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="c7359-684">![使用 Razor 和 HTML5 標記的新範本](aspnet-mvc-4-fundamentals/_static/image41.png "使用 Razor 和 HTML5 標記的新範本")</span><span class="sxs-lookup"><span data-stu-id="c7359-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="c7359-685">*使用 Razor 和 HTML5 標記的新範本*</span><span class="sxs-lookup"><span data-stu-id="c7359-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="c7359-686">**包含的 JavaScript 程式庫**</span><span class="sxs-lookup"><span data-stu-id="c7359-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="c7359-687">**jquery**： jquery 簡化了 HTML 檔案的遍歷、事件處理、動畫，以及 Ajax 互動。</span><span class="sxs-lookup"><span data-stu-id="c7359-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="c7359-688">**JQUERY UI**：此程式庫提供建立于 jQuery JavaScript 程式庫之上的低層級互動和動畫、advanced 效果和 themeable widget 的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="c7359-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="c7359-689">您可以在[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中瞭解 jQuery 和 jquery UI。</span><span class="sxs-lookup"><span data-stu-id="c7359-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="c7359-690">**KnockoutJS**： ASP.NET MVC 4 預設範本現在包含**KnockoutJS**，這是一種 javascript MVVM 架構，可讓您使用 javascript 和 HTML 建立豐富且回應速度高的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="c7359-691">如同在 ASP.NET MVC 3 中，jQuery 和 jQuery UI 程式庫也包含在 ASP.NET MVC 4 中。</span><span class="sxs-lookup"><span data-stu-id="c7359-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="c7359-692">您可以在此連結中取得 KnockOutJS 程式庫的詳細資訊： [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="c7359-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="c7359-693">**Modernizr**：此程式庫會自動執行，讓您的網站在使用 HTML5 和 CSS3 技術時與舊版瀏覽器相容。</span><span class="sxs-lookup"><span data-stu-id="c7359-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="c7359-694">您可以在此連結中取得 Modernizr 程式庫的詳細資訊： [http://www.modernizr.com/](http://www.modernizr.com/)。</span><span class="sxs-lookup"><span data-stu-id="c7359-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="c7359-695">**解決方案中包含的 SimpleMembership**</span><span class="sxs-lookup"><span data-stu-id="c7359-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="c7359-696">SimpleMembership 已設計為取代先前的 ASP.NET 角色和成員資格提供者系統。</span><span class="sxs-lookup"><span data-stu-id="c7359-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="c7359-697">它有許多新功能，可讓開發人員更輕鬆地以更有彈性的方式保護網頁。</span><span class="sxs-lookup"><span data-stu-id="c7359-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="c7359-698">網際網路範本已設定一些專案來整合 SimpleMembership，例如，AccountController 已準備好使用 OAuthWebSecurity （適用于 OAuth 帳戶註冊、登入、管理等）和 Web 安全性。</span><span class="sxs-lookup"><span data-stu-id="c7359-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="c7359-699">![解決方案中包含的 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "解決方案中包含的 SimpleMembership")</span><span class="sxs-lookup"><span data-stu-id="c7359-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="c7359-700">*解決方案中包含的 SimpleMembership*</span><span class="sxs-lookup"><span data-stu-id="c7359-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="c7359-701">在 MSDN 中尋找有關[OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="c7359-702">此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="c7359-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c7359-703">總結</span><span class="sxs-lookup"><span data-stu-id="c7359-703">Summary</span></span>

<span data-ttu-id="c7359-704">藉由完成此實際操作實驗室，您已瞭解 ASP.NET MVC 的基本概念：</span><span class="sxs-lookup"><span data-stu-id="c7359-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="c7359-705">MVC 應用程式的核心元素及其互動方式</span><span class="sxs-lookup"><span data-stu-id="c7359-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="c7359-706">如何建立 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="c7359-707">如何新增和設定控制器來處理透過 URL 和 querystring 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="c7359-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="c7359-708">如何新增版面配置主版頁面來設定常用 HTML 內容的範本、增強外觀與風格的樣式表單，以及顯示 HTML 內容的視圖範本</span><span class="sxs-lookup"><span data-stu-id="c7359-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="c7359-709">如何使用 ViewModel 模式將屬性傳遞至 View 範本以顯示動態資訊</span><span class="sxs-lookup"><span data-stu-id="c7359-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="c7359-710">如何使用傳遞至 View 範本中之控制器的參數</span><span class="sxs-lookup"><span data-stu-id="c7359-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="c7359-711">如何將連結新增至 ASP.NET MVC 應用程式內的頁面</span><span class="sxs-lookup"><span data-stu-id="c7359-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="c7359-712">如何在視圖中新增和使用動態屬性</span><span class="sxs-lookup"><span data-stu-id="c7359-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="c7359-713">ASP.NET MVC 4 專案範本中的增強功能</span><span class="sxs-lookup"><span data-stu-id="c7359-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="c7359-714">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="c7359-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="c7359-715">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="c7359-716">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="c7359-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="c7359-717">移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="c7359-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="c7359-718">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="c7359-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="c7359-719">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-719">Click on **Install Now**.</span></span> <span data-ttu-id="c7359-720">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="c7359-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="c7359-721">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c7359-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="c7359-722">![安裝 Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="c7359-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="c7359-723">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="c7359-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="c7359-724">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="c7359-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="c7359-726">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="c7359-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="c7359-727">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="c7359-727">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="c7359-729">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="c7359-729">*Installation progress*</span></span>
6. <span data-ttu-id="c7359-730">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-730">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="c7359-732">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="c7359-732">*Installation completed*</span></span>
7. <span data-ttu-id="c7359-733">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="c7359-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="c7359-734">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="c7359-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="c7359-736">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="c7359-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="c7359-737">附錄 B：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="c7359-738">本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。</span><span class="sxs-lookup"><span data-stu-id="c7359-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="c7359-739">工作 1-從 Windows Azure 入口網站建立新的網站</span><span class="sxs-lookup"><span data-stu-id="c7359-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="c7359-740">移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="c7359-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-741">有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。</span><span class="sxs-lookup"><span data-stu-id="c7359-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="c7359-742">您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。</span><span class="sxs-lookup"><span data-stu-id="c7359-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="c7359-743">![登入 Windows Azure 入口網站](aspnet-mvc-4-fundamentals/_static/image48.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="c7359-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="c7359-744">*登入 Windows Azure 管理入口網站*</span><span class="sxs-lookup"><span data-stu-id="c7359-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="c7359-745">按一下命令列上的 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="c7359-746">![建立新網站](aspnet-mvc-4-fundamentals/_static/image49.png "建立新網站")</span><span class="sxs-lookup"><span data-stu-id="c7359-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="c7359-747">*建立新網站*</span><span class="sxs-lookup"><span data-stu-id="c7359-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="c7359-748">按一下 [**計算** | 的**網站**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="c7359-749">然後選取 [**快速建立**] 選項。</span><span class="sxs-lookup"><span data-stu-id="c7359-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="c7359-750">提供新網站的可用 URL，然後按一下 [**建立網站**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-751">Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。</span><span class="sxs-lookup"><span data-stu-id="c7359-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="c7359-752">[快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="c7359-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="c7359-753">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="c7359-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="c7359-754">![使用 [快速建立] 建立新的網站](aspnet-mvc-4-fundamentals/_static/image50.png "使用 [快速建立] 建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="c7359-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="c7359-755">*使用 [快速建立] 建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="c7359-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="c7359-756">等到新**網站**建立完畢。</span><span class="sxs-lookup"><span data-stu-id="c7359-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="c7359-757">建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。</span><span class="sxs-lookup"><span data-stu-id="c7359-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="c7359-758">檢查新網站是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="c7359-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="c7359-759">![流覽至新網站](aspnet-mvc-4-fundamentals/_static/image51.png "流覽至新網站")</span><span class="sxs-lookup"><span data-stu-id="c7359-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="c7359-760">*流覽至新網站*</span><span class="sxs-lookup"><span data-stu-id="c7359-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="c7359-761">![網站正在執行](aspnet-mvc-4-fundamentals/_static/image52.png "網站正在執行")</span><span class="sxs-lookup"><span data-stu-id="c7359-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="c7359-762">*網站正在執行*</span><span class="sxs-lookup"><span data-stu-id="c7359-762">*Web site running*</span></span>
6. <span data-ttu-id="c7359-763">返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。</span><span class="sxs-lookup"><span data-stu-id="c7359-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="c7359-764">![開啟網站管理頁面](aspnet-mvc-4-fundamentals/_static/image53.png "開啟網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="c7359-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="c7359-765">*開啟網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="c7359-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="c7359-766">在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。</span><span class="sxs-lookup"><span data-stu-id="c7359-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-767">*發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。</span><span class="sxs-lookup"><span data-stu-id="c7359-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="c7359-768">發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="c7359-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="c7359-769">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="c7359-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="c7359-770">![正在下載網站發行設定檔](aspnet-mvc-4-fundamentals/_static/image54.png "正在下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="c7359-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="c7359-771">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="c7359-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="c7359-772">將發行設定檔下載到已知的位置。</span><span class="sxs-lookup"><span data-stu-id="c7359-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="c7359-773">在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="c7359-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="c7359-774">![儲存發行設定檔](aspnet-mvc-4-fundamentals/_static/image55.png "正在儲存發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="c7359-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="c7359-775">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="c7359-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="c7359-776">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="c7359-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="c7359-777">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7359-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="c7359-778">如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="c7359-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="c7359-779">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="c7359-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="c7359-780">您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7359-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="c7359-781">如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。</span><span class="sxs-lookup"><span data-stu-id="c7359-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="c7359-782">記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="c7359-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="c7359-783">請不要建立資料庫，因為它會在稍後的階段中建立。</span><span class="sxs-lookup"><span data-stu-id="c7359-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="c7359-784">![SQL Database Server 儀表板](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server 儀表板")</span><span class="sxs-lookup"><span data-stu-id="c7359-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="c7359-785">*SQL Database Server 儀表板*</span><span class="sxs-lookup"><span data-stu-id="c7359-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="c7359-786">在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c7359-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="c7359-787">若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](aspnet-mvc-4-fundamentals/_static/image57.png) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c7359-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![正在新增用戶端 IP 位址](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="c7359-789">*正在新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="c7359-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="c7359-790">將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="c7359-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="c7359-792">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="c7359-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="c7359-793">工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7359-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="c7359-794">返回 ASP.NET MVC 4 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7359-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="c7359-795">在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。</span><span class="sxs-lookup"><span data-stu-id="c7359-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="c7359-796">![發行應用程式](aspnet-mvc-4-fundamentals/_static/image60.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="c7359-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="c7359-797">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="c7359-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="c7359-798">匯入您在第一個工作中儲存的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="c7359-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="c7359-799">![匯入發行設定檔](aspnet-mvc-4-fundamentals/_static/image61.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="c7359-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="c7359-800">*正在匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="c7359-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="c7359-801">按一下 [**驗證連接**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-801">Click **Validate Connection**.</span></span> <span data-ttu-id="c7359-802">驗證完成後，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7359-803">當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。</span><span class="sxs-lookup"><span data-stu-id="c7359-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="c7359-804">![正在驗證連接](aspnet-mvc-4-fundamentals/_static/image62.png "正在驗證連接")</span><span class="sxs-lookup"><span data-stu-id="c7359-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="c7359-805">*正在驗證連接*</span><span class="sxs-lookup"><span data-stu-id="c7359-805">*Validating connection*</span></span>
4. <span data-ttu-id="c7359-806">在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="c7359-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="c7359-807">![Web deploy 設定](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy 設定")</span><span class="sxs-lookup"><span data-stu-id="c7359-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="c7359-808">*Web deploy 設定*</span><span class="sxs-lookup"><span data-stu-id="c7359-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="c7359-809">設定資料庫連接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7359-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="c7359-810">在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="c7359-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="c7359-811">在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="c7359-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="c7359-812">在 [**密碼**] 中輸入您的伺服器管理員登入密碼。</span><span class="sxs-lookup"><span data-stu-id="c7359-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="c7359-813">輸入新的資料庫名稱，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="c7359-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="c7359-814">![正在設定目的地連接字串](aspnet-mvc-4-fundamentals/_static/image64.png "正在設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="c7359-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="c7359-815">*正在設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="c7359-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="c7359-816">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c7359-816">Then click **OK**.</span></span> <span data-ttu-id="c7359-817">當系統提示您建立資料庫時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="c7359-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="c7359-818">![建立資料庫](aspnet-mvc-4-fundamentals/_static/image65.png "建立資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="c7359-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="c7359-819">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="c7359-819">*Creating the database*</span></span>
7. <span data-ttu-id="c7359-820">您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="c7359-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="c7359-821">然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c7359-821">Then click **Next**.</span></span>

    <span data-ttu-id="c7359-822">![指向 SQL Database 的連接字串](aspnet-mvc-4-fundamentals/_static/image66.png "指向 SQL Database 的連接字串")</span><span class="sxs-lookup"><span data-stu-id="c7359-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="c7359-823">*指向 SQL Database 的連接字串*</span><span class="sxs-lookup"><span data-stu-id="c7359-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="c7359-824">在 [**預覽**] 頁面中，按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="c7359-825">![發行 web 應用程式](aspnet-mvc-4-fundamentals/_static/image67.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="c7359-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="c7359-826">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="c7359-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="c7359-827">發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="c7359-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="c7359-828">![發行至 Windows Azure 的應用程式](aspnet-mvc-4-fundamentals/_static/image68.png "發行至 Windows Azure 的應用程式")</span><span class="sxs-lookup"><span data-stu-id="c7359-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="c7359-829">*發行至 Windows Azure 的應用程式*</span><span class="sxs-lookup"><span data-stu-id="c7359-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="c7359-830">附錄 C：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="c7359-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="c7359-831">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="c7359-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="c7359-832">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="c7359-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="c7359-833">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-fundamentals/_static/image69.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="c7359-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="c7359-834">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="c7359-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="c7359-835">***若要使用鍵盤新增程式碼片段（C#僅限）***</span><span class="sxs-lookup"><span data-stu-id="c7359-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="c7359-836">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="c7359-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="c7359-837">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="c7359-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="c7359-838">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="c7359-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="c7359-839">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="c7359-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="c7359-840">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="c7359-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="c7359-841">![開始鍵入程式碼片段名稱](aspnet-mvc-4-fundamentals/_static/image70.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="c7359-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="c7359-842">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="c7359-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="c7359-843">![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-fundamentals/_static/image71.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="c7359-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="c7359-844">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="c7359-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="c7359-845">![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-fundamentals/_static/image72.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="c7359-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="c7359-846">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="c7359-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="c7359-847">***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1.</span><span class="sxs-lookup"><span data-stu-id="c7359-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="c7359-848">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="c7359-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="c7359-849">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="c7359-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="c7359-850">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="c7359-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="c7359-851">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-fundamentals/_static/image73.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="c7359-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="c7359-852">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="c7359-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="c7359-853">![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-fundamentals/_static/image74.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="c7359-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="c7359-854">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="c7359-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
