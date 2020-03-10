---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 實習實驗室：使用 ASP.NET Web API 和 .js 建立單一頁面應用程式（SPA） ASP.NET 4。x
author: rick-anderson
description: 逐步執行程式碼：使用適用于 ASP.NET 4.x 的 ASP.NET Web API 和 .js 建立單一頁面應用程式（SPA）。
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557040"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a><span data-ttu-id="b85c9-103">實習實驗室：使用 ASP.NET Web API 和角度 .js 建立單一頁面應用程式（SPA）</span><span class="sxs-lookup"><span data-stu-id="b85c9-103">Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js</span></span>

<span data-ttu-id="b85c9-104">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b85c9-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b85c9-105">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="b85c9-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="b85c9-106">這堂實習實驗室會示範如何使用 ASP.NET Web API 和 ASP.NET 4.x 的 .js 來建立單一頁面應用程式（SPA）。</span><span class="sxs-lookup"><span data-stu-id="b85c9-106">This hands on lab shows you how to build a Single Page Application (SPA) with ASP.NET Web API and Angular.js for ASP.NET 4.x.</span></span>

<span data-ttu-id="b85c9-107">在這個實際操作的實驗室中，您將利用這些技術來執行萬能技客測驗，這是以 SPA 概念為基礎的邏輯網站。</span><span class="sxs-lookup"><span data-stu-id="b85c9-107">In this hand-on lab, you will take advantage of those technologies to implement Geek Quiz, a trivia website based on the SPA concept.</span></span> <span data-ttu-id="b85c9-108">您會先使用 ASP.NET Web API 來執行服務層級，以公開所需的端點來取得測驗問題並儲存答案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-108">You will first implement the service layer with ASP.NET Web API to expose the required endpoints to retrieve the quiz questions and store the answers.</span></span> <span data-ttu-id="b85c9-109">然後，您將使用 AngularJS 和 CSS3 轉換效果，建立豐富且回應迅速的 UI。</span><span class="sxs-lookup"><span data-stu-id="b85c9-109">Then, you will build a rich and responsive UI using AngularJS and CSS3 transformation effects.</span></span>

<span data-ttu-id="b85c9-110">在傳統的 web 應用程式中，用戶端（瀏覽器）會藉由要求頁面來起始與伺服器的通訊。</span><span class="sxs-lookup"><span data-stu-id="b85c9-110">In traditional web applications, the client (browser) initiates the communication with the server by requesting a page.</span></span> <span data-ttu-id="b85c9-111">接著，伺服器會處理要求，並將網頁的 HTML 傳送給用戶端。</span><span class="sxs-lookup"><span data-stu-id="b85c9-111">The server then processes the request and sends the HTML of the page to the client.</span></span> <span data-ttu-id="b85c9-112">在後續與頁面的互動中–例如，使用者導覽至連結或提交含有資料的表單–會將新的要求傳送至伺服器，然後流程會重新開機：伺服器會處理要求，並將新頁面傳送至瀏覽器以回應新的動作要求ed （由用戶端）。</span><span class="sxs-lookup"><span data-stu-id="b85c9-112">In subsequent interactions with the page –e.g. the user navigates to a link or submits a form with data– a new request is sent to the server, and the flow starts again: the server processes the request and sends a new page to the browser in response to the new action requested by the client.</span></span>
> 
> <span data-ttu-id="b85c9-113">在單頁應用程式（Spa）中，在初始要求之後，會在瀏覽器中載入整個頁面，但後續的互動會透過 Ajax 要求進行。</span><span class="sxs-lookup"><span data-stu-id="b85c9-113">In Single-Page Applications (SPAs) the entire page is loaded in the browser after the initial request, but subsequent interactions take place through Ajax requests.</span></span> <span data-ttu-id="b85c9-114">這表示瀏覽器只需要更新已變更之頁面的部分;不需要重載整頁。</span><span class="sxs-lookup"><span data-stu-id="b85c9-114">This means that the browser has to update only the portion of the page that has changed; there is no need to reload the entire page.</span></span> <span data-ttu-id="b85c9-115">SPA 方法可減少應用程式回應使用者動作所花費的時間，進而產生更流暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="b85c9-115">The SPA approach reduces the time taken by the application to respond to user actions, resulting in a more fluid experience.</span></span>
> 
> <span data-ttu-id="b85c9-116">SPA 的架構牽涉到在傳統 web 應用程式中不存在的特定挑戰。</span><span class="sxs-lookup"><span data-stu-id="b85c9-116">The architecture of a SPA involves certain challenges that are not present in traditional web applications.</span></span> <span data-ttu-id="b85c9-117">不過，像是 ASP.NET Web API 之類的新興技術，像是 AngularJS 的 JavaScript 架構和 CSS3 提供的新樣式功能，讓設計和建立 Spa 變得非常容易。</span><span class="sxs-lookup"><span data-stu-id="b85c9-117">However, emerging technologies like ASP.NET Web API, JavaScript frameworks like AngularJS and new styling features provided by CSS3 make it really easy to design and build SPAs.</span></span>
> 
> 
> <span data-ttu-id="b85c9-118">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="b85c9-118">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

## <a name="overview"></a><span data-ttu-id="b85c9-119">概觀</span><span class="sxs-lookup"><span data-stu-id="b85c9-119">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b85c9-120">目標</span><span class="sxs-lookup"><span data-stu-id="b85c9-120">Objectives</span></span>

<span data-ttu-id="b85c9-121">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="b85c9-121">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="b85c9-122">建立用來傳送和接收 JSON 資料的 ASP.NET Web API 服務</span><span class="sxs-lookup"><span data-stu-id="b85c9-122">Create an ASP.NET Web API service to send and receive JSON data</span></span>
- <span data-ttu-id="b85c9-123">使用 AngularJS 建立回應式 UI</span><span class="sxs-lookup"><span data-stu-id="b85c9-123">Create a responsive UI using AngularJS</span></span>
- <span data-ttu-id="b85c9-124">使用 CSS3 轉換來增強 UI 體驗</span><span class="sxs-lookup"><span data-stu-id="b85c9-124">Enhance the UI experience with CSS3 transformations</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b85c9-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b85c9-125">Prerequisites</span></span>

<span data-ttu-id="b85c9-126">若要完成此實際操作實驗室，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="b85c9-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="b85c9-127">[適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="b85c9-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b85c9-128">安裝程式</span><span class="sxs-lookup"><span data-stu-id="b85c9-128">Setup</span></span>

<span data-ttu-id="b85c9-129">為了在此實際操作實驗室中執行練習，您必須先設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="b85c9-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="b85c9-130">開啟 Windows Explorer 並流覽至實驗室的 [**源**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b85c9-130">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="b85c9-131">以滑鼠右鍵按一下**setup.exe** ，然後選取 [以**系統管理員身分執行**] 以啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="b85c9-131">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="b85c9-132">如果顯示 [使用者帳戶控制] 對話方塊，請確認動作以繼續。</span><span class="sxs-lookup"><span data-stu-id="b85c9-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="b85c9-133">執行安裝程式之前，請確定您已檢查過此實驗室的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="b85c9-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="b85c9-134">使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="b85c9-134">Using the Code Snippets</span></span>

<span data-ttu-id="b85c9-135">在整個實驗室檔中，系統會指示您插入程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="b85c9-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="b85c9-136">為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 2013 內進行存取，以避免必須以手動方式新增。</span><span class="sxs-lookup"><span data-stu-id="b85c9-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="b85c9-137">每個練習都附有一個起始解決方案，此方案位於練習的 [**開始**] 資料夾中，可讓您獨立于其他練習之外進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="b85c9-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="b85c9-138">請注意，在練習期間新增的程式碼片段缺少這些起始的解決方案，而且在您完成練習之前可能無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="b85c9-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="b85c9-139">在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的**結束**資料夾，其中含有完成對應練習中步驟所產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b85c9-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="b85c9-140">如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。</span><span class="sxs-lookup"><span data-stu-id="b85c9-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b85c9-141">練習</span><span class="sxs-lookup"><span data-stu-id="b85c9-141">Exercises</span></span>

<span data-ttu-id="b85c9-142">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="b85c9-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="b85c9-143">建立 Web API</span><span class="sxs-lookup"><span data-stu-id="b85c9-143">Creating a Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="b85c9-144">建立 SPA 介面</span><span class="sxs-lookup"><span data-stu-id="b85c9-144">Creating a SPA Interface</span></span>](#Exercise2)

<span data-ttu-id="b85c9-145">完成此實驗室的預估時間： **60 分鐘**</span><span class="sxs-lookup"><span data-stu-id="b85c9-145">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="b85c9-146">當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。</span><span class="sxs-lookup"><span data-stu-id="b85c9-146">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="b85c9-147">每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。</span><span class="sxs-lookup"><span data-stu-id="b85c9-147">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="b85c9-148">本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。</span><span class="sxs-lookup"><span data-stu-id="b85c9-148">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="b85c9-149">如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。</span><span class="sxs-lookup"><span data-stu-id="b85c9-149">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a><span data-ttu-id="b85c9-150">練習1：建立 Web API</span><span class="sxs-lookup"><span data-stu-id="b85c9-150">Exercise 1: Creating a Web API</span></span>

<span data-ttu-id="b85c9-151">SPA 的其中一個重要部分就是服務層。</span><span class="sxs-lookup"><span data-stu-id="b85c9-151">One of the key parts of a SPA is the service layer.</span></span> <span data-ttu-id="b85c9-152">它負責處理 UI 所傳送的 Ajax 呼叫，並傳回資料以回應該呼叫。</span><span class="sxs-lookup"><span data-stu-id="b85c9-152">It is responsible for processing the Ajax calls sent by the UI and returning data in response to that call.</span></span> <span data-ttu-id="b85c9-153">抓取的資料應該以電腦可讀取的格式呈現，才能供用戶端剖析及取用。</span><span class="sxs-lookup"><span data-stu-id="b85c9-153">The data retrieved should be presented in a machine-readable format in order to be parsed and consumed by the client.</span></span>

<span data-ttu-id="b85c9-154">Web API 架構是 ASP.NET 堆疊的一部分，其設計旨在讓您輕鬆地執行 HTTP 服務，通常會透過 RESTful API 來傳送和接收 JSON 或 XML 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="b85c9-154">The Web API framework is part of the ASP.NET Stack and is designed to make it easy to implement HTTP services, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span> <span data-ttu-id="b85c9-155">在此練習中，您將建立網站來裝載萬能技客測驗應用程式，然後使用 ASP.NET Web API 來執行後端服務，以公開並保存測驗資料。</span><span class="sxs-lookup"><span data-stu-id="b85c9-155">In this exercise you will create the Web site to host the Geek Quiz application and then implement the back-end service to expose and persist the quiz data using ASP.NET Web API.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a><span data-ttu-id="b85c9-156">工作1–建立萬能技客測驗的初始專案</span><span class="sxs-lookup"><span data-stu-id="b85c9-156">Task 1 – Creating the Initial Project for Geek Quiz</span></span>

<span data-ttu-id="b85c9-157">在這項工作中，您將根據 Visual Studio 隨附的**一個 ASP.NET**專案類型，開始建立具有 ASP.NET Web API 支援的新 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-157">In this task you will start creating a new ASP.NET MVC project with support for ASP.NET Web API based on the **One ASP.NET** project type that comes with Visual Studio.</span></span> <span data-ttu-id="b85c9-158">**其中一個 ASP.NET**會將所有 ASP.NET 技術合併，並提供您視需要混合使用和比對的選項。</span><span class="sxs-lookup"><span data-stu-id="b85c9-158">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="b85c9-159">接著，您將加入 Entity Framework 的模型類別和資料庫初始化運算式，以插入測驗問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-159">You will then add the Entity Framework's model classes and the database initializer to insert the quiz questions.</span></span>

1. <span data-ttu-id="b85c9-160">開啟**Web Visual Studio Express 2013** ，然後選取 [檔案] **|新增專案 ...** 以啟動新的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-160">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    <span data-ttu-id="b85c9-161">![建立新專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "建立新專案")</span><span class="sxs-lookup"><span data-stu-id="b85c9-161">![Creating a New Project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Creating a New Project")</span></span>

    <span data-ttu-id="b85c9-162">*建立新專案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-162">*Creating a New Project*</span></span>
2. <span data-ttu-id="b85c9-163">在 [**新增專案**] 對話方塊中，選取視覺效果  **C#底下的 [ASP.NET Web 應用程式] |[Web** ] 索引標籤。請確認已選取 **.NET Framework 4.5** ，將其命名為*GeekQuiz*，選擇**位置**，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="b85c9-163">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab. Make sure **.NET Framework 4.5** is selected, name it *GeekQuiz*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="b85c9-164">![建立新的 ASP.NET Web 應用程式專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "建立新的 ASP.NET Web 應用程式專案")</span><span class="sxs-lookup"><span data-stu-id="b85c9-164">![Creating a new ASP.NET Web Application project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Creating a new ASP.NET Web Application project")</span></span>

    <span data-ttu-id="b85c9-165">*建立新的 ASP.NET Web 應用程式專案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-165">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="b85c9-166">在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **MVC** ] 範本，然後選取 [ **Web API** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="b85c9-166">In the **New ASP.NET Project** dialog box, select the **MVC** template and select the **Web API** option.</span></span> <span data-ttu-id="b85c9-167">此外，請確定 [**驗證**] 選項已設為 [**個別使用者帳戶**]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-167">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="b85c9-168">按一下 [確定] 繼續操作。</span><span class="sxs-lookup"><span data-stu-id="b85c9-168">Click **OK** to continue.</span></span>

    ![使用 MVC 範本建立新的專案，包括 Web API 元件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    <span data-ttu-id="b85c9-170">*使用 MVC 範本建立新的專案，包括 Web API 元件*</span><span class="sxs-lookup"><span data-stu-id="b85c9-170">*Creating a new project with the MVC template, including Web API components*</span></span>
4. <span data-ttu-id="b85c9-171">在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [**模型**] 資料夾，然後選取 [**新增] |現有專案 ...** 。</span><span class="sxs-lookup"><span data-stu-id="b85c9-171">In **Solution Explorer**, right-click the **Models** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="b85c9-172">![加入現有的專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "加入現有的專案")</span><span class="sxs-lookup"><span data-stu-id="b85c9-172">![Adding an existing item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Adding an existing item")</span></span>

    <span data-ttu-id="b85c9-173">*加入現有的專案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-173">*Adding an existing item*</span></span>
5. <span data-ttu-id="b85c9-174">在 [**加入現有專案**] 對話方塊中，流覽至 [**來源/資產/模型**] 資料夾，然後選取所有檔案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-174">In the **Add Existing Item** dialog box, navigate to the **Source/Assets/Models** folder and select all the files.</span></span> <span data-ttu-id="b85c9-175">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-175">Click **Add**.</span></span>

    <span data-ttu-id="b85c9-176">![新增模型資產](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "新增模型資產")</span><span class="sxs-lookup"><span data-stu-id="b85c9-176">![Adding the model assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Adding the model assets")</span></span>

    <span data-ttu-id="b85c9-177">*新增模型資產*</span><span class="sxs-lookup"><span data-stu-id="b85c9-177">*Adding the model assets*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b85c9-178">藉由新增這些檔案，您將會新增資料模型、Entity Framework 的資料庫內容，以及萬能技客測驗應用程式的資料庫初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="b85c9-178">By adding these files, you are adding the data model, the Entity Framework's database context and the database initializer for the Geek Quiz application.</span></span>
    > 
    > <span data-ttu-id="b85c9-179">**Entity Framework （EF）** 是物件關聯式對應程式（ORM），可讓您以概念應用程式模型進行程式設計來建立資料存取應用程式，而不需要直接使用關聯式儲存架構進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="b85c9-179">**Entity Framework (EF)** is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span> <span data-ttu-id="b85c9-180">您可以在[這裡](../../../entity-framework.md)深入瞭解 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="b85c9-180">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>
    > 
    > <span data-ttu-id="b85c9-181">以下是您剛才新增之類別的描述：</span><span class="sxs-lookup"><span data-stu-id="b85c9-181">The following is a description of the classes you just added:</span></span>
    > 
    > - <span data-ttu-id="b85c9-182">**TriviaOption：** 代表與測驗問題相關聯的單一選項</span><span class="sxs-lookup"><span data-stu-id="b85c9-182">**TriviaOption:** represents a single option associated with a quiz question</span></span>
    > - <span data-ttu-id="b85c9-183">**TriviaQuestion：** 代表測驗問題，並透過**options**屬性公開相關聯的選項</span><span class="sxs-lookup"><span data-stu-id="b85c9-183">**TriviaQuestion:** represents a quiz question and exposes the associated options through the **Options** property</span></span>
    > - <span data-ttu-id="b85c9-184">**TriviaAnswer：** 代表使用者選取來回應測驗問題的選項</span><span class="sxs-lookup"><span data-stu-id="b85c9-184">**TriviaAnswer:** represents the option selected by the user in response to a quiz question</span></span>
    > - <span data-ttu-id="b85c9-185">**TriviaCoNtext：** 代表萬能技客測驗應用程式的 Entity Framework 資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="b85c9-185">**TriviaContext:** represents the Entity Framework's database context of the Geek Quiz application.</span></span> <span data-ttu-id="b85c9-186">這個類別衍生自**DCoNtext** ，並公開代表上述實體集合的**DbSet**屬性。</span><span class="sxs-lookup"><span data-stu-id="b85c9-186">This class derives from **DContext** and exposes **DbSet** properties that represent collections of the entities described above.</span></span>
    > - <span data-ttu-id="b85c9-187">**TriviaDatabaseInitializer：** 執行繼承自**CreateDatabaseIfNotExists**之**TriviaCoNtext**類別的 Entity Framework 初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="b85c9-187">**TriviaDatabaseInitializer:** the implementation of the Entity Framework initializer for the **TriviaContext** class which inherits from **CreateDatabaseIfNotExists**.</span></span> <span data-ttu-id="b85c9-188">這個類別的預設行為是只在不存在時建立資料庫，插入**Seed**方法中指定的實體。</span><span class="sxs-lookup"><span data-stu-id="b85c9-188">The default behavior of this class is to create the database only if it does not exist, inserting the entities specified in the **Seed** method.</span></span>
6. <span data-ttu-id="b85c9-189">開啟**Global.asax.cs**檔案，並新增下列 using 語句。</span><span class="sxs-lookup"><span data-stu-id="b85c9-189">Open the **Global.asax.cs** file and add the following using statement.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. <span data-ttu-id="b85c9-190">將下列程式碼新增至**應用程式開頭\_Start**方法，將**TriviaDatabaseInitializer**設定為資料庫初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="b85c9-190">Add the following code at the beginning of the **Application\_Start** method to set the **TriviaDatabaseInitializer** as the database initializer.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. <span data-ttu-id="b85c9-191">修改**Home**控制器來限制已驗證使用者的存取權。</span><span class="sxs-lookup"><span data-stu-id="b85c9-191">Modify the **Home** controller to restrict access to authenticated users.</span></span> <span data-ttu-id="b85c9-192">若要這麼做，請開啟 [**控制器**] 資料夾內的**HomeController.cs**檔案，並將 [**授權**] 屬性新增至**HomeController**類別定義。</span><span class="sxs-lookup"><span data-stu-id="b85c9-192">To do this, open the **HomeController.cs** file inside the **Controllers** folder and add the **Authorize** attribute to the **HomeController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > <span data-ttu-id="b85c9-193">**授權**篩選準則會檢查使用者是否已通過驗證。</span><span class="sxs-lookup"><span data-stu-id="b85c9-193">The **Authorize** filter checks to see if the user is authenticated.</span></span> <span data-ttu-id="b85c9-194">如果使用者未經過驗證，則會傳回 HTTP 狀態碼401（未經授權），而不會叫用動作。</span><span class="sxs-lookup"><span data-stu-id="b85c9-194">If the user is not authenticated, it returns HTTP status code 401 (Unauthorized) without invoking the action.</span></span> <span data-ttu-id="b85c9-195">您可以在控制器層級或個別動作層級，全域套用篩選準則。</span><span class="sxs-lookup"><span data-stu-id="b85c9-195">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>
9. <span data-ttu-id="b85c9-196">您現在將自訂網頁的版面配置和商標。</span><span class="sxs-lookup"><span data-stu-id="b85c9-196">You will now customize the layout of the web pages and the branding.</span></span> <span data-ttu-id="b85c9-197">若要這麼做，請開啟 Views 內的 **\_Layout**檔案 **|共用**資料夾，並將*ASP.NET 應用程式*取代為*萬能技客測驗*，以更新 **&lt;標題&gt;** 元素的內容。</span><span class="sxs-lookup"><span data-stu-id="b85c9-197">To do this, open the **\_Layout.cshtml** file inside the **Views | Shared** folder and update the content of the **&lt;title&gt;** element by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. <span data-ttu-id="b85c9-198">在相同的檔案中，移除 [*關於*] 和 [*連絡人*] 連結，並將 [*首頁*] 連結重新命名為 [*播放*]，以更新巡覽列。</span><span class="sxs-lookup"><span data-stu-id="b85c9-198">In the same file, update the navigation bar by removing the *About* and *Contact* links and renaming the *Home* link to *Play*.</span></span> <span data-ttu-id="b85c9-199">此外，將*應用程式名稱*連結重新命名為*萬能技客測驗*。</span><span class="sxs-lookup"><span data-stu-id="b85c9-199">Additionally, rename the *Application name* link to *Geek Quiz*.</span></span> <span data-ttu-id="b85c9-200">導覽列的 HTML 看起來應該像下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b85c9-200">The HTML for the navigation bar should look like the following code.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. <span data-ttu-id="b85c9-201">將*我的 ASP.NET 應用程式*取代為*萬能技客測驗*，以更新版面配置頁的頁尾。</span><span class="sxs-lookup"><span data-stu-id="b85c9-201">Update the footer of the layout page by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span> <span data-ttu-id="b85c9-202">若要這麼做，請將&lt;頁尾 **&gt;** 元素的內容取代為下列反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b85c9-202">To do this, replace the content of the **&lt;footer&gt;** element with the following highlighted code.</span></span>

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a><span data-ttu-id="b85c9-203">工作 2-建立 TriviaController Web API</span><span class="sxs-lookup"><span data-stu-id="b85c9-203">Task 2 – Creating the TriviaController Web API</span></span>

<span data-ttu-id="b85c9-204">在上一個工作中，您已建立萬能技客測驗 web 應用程式的初始結構。</span><span class="sxs-lookup"><span data-stu-id="b85c9-204">In the previous task, you created the initial structure of the Geek Quiz web application.</span></span> <span data-ttu-id="b85c9-205">您現在將建立一個簡單的 Web API 服務，以與測驗資料模型互動並公開下列動作：</span><span class="sxs-lookup"><span data-stu-id="b85c9-205">You will now build a simple Web API service that interacts with the quiz data model and exposes the following actions:</span></span>

- <span data-ttu-id="b85c9-206">**取得/api/trivia**：從測驗清單中抓取要由已驗證使用者回答的下一個問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-206">**GET /api/trivia**: Retrieves the next question from the quiz list to be answered by the authenticated user.</span></span>
- <span data-ttu-id="b85c9-207">**POST/api/trivia**：儲存已驗證使用者所指定的測驗解答。</span><span class="sxs-lookup"><span data-stu-id="b85c9-207">**POST /api/trivia**: Stores the quiz answer specified by the authenticated user.</span></span>

<span data-ttu-id="b85c9-208">您將使用 Visual Studio 所提供的 ASP.NET 架構工具來建立 Web API 控制器類別的基準。</span><span class="sxs-lookup"><span data-stu-id="b85c9-208">You will use the ASP.NET Scaffolding tools provided by Visual Studio to create the baseline for the Web API controller class.</span></span>

1. <span data-ttu-id="b85c9-209">開啟**應用程式\_[開始**] 資料夾內的**WebApiConfig.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-209">Open the **WebApiConfig.cs** file inside the **App\_Start** folder.</span></span> <span data-ttu-id="b85c9-210">此檔案會定義 Web API 服務的設定，例如路由對應至 Web API 控制器動作的方式。</span><span class="sxs-lookup"><span data-stu-id="b85c9-210">This file defines the configuration of the Web API service, like how routes are mapped to Web API controller actions.</span></span>
2. <span data-ttu-id="b85c9-211">在檔案開頭處新增下列 using 語句。</span><span class="sxs-lookup"><span data-stu-id="b85c9-211">Add the following using statement at the beginning of the file.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. <span data-ttu-id="b85c9-212">將下列反白顯示的程式碼新增至**Register**方法，以全域設定 Web API 動作方法所抓取之 JSON 資料的格式器。</span><span class="sxs-lookup"><span data-stu-id="b85c9-212">Add the following highlighted code to the **Register** method to globally configure the formatter for the JSON data retrieved by the Web API action methods.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="b85c9-213">**CamelCasePropertyNamesContractResolver**會自動將屬性名稱轉換成*camel*大小寫，這是 JavaScript 中屬性名稱的一般慣例。</span><span class="sxs-lookup"><span data-stu-id="b85c9-213">The **CamelCasePropertyNamesContractResolver** automatically converts property names to *camel* case, which is the general convention for property names in JavaScript.</span></span>
4. <span data-ttu-id="b85c9-214">在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [**控制器**] 資料夾，然後選取 [**新增] |新增 Scaffold 專案 ...** 。</span><span class="sxs-lookup"><span data-stu-id="b85c9-214">In **Solution Explorer**, right-click the **Controllers** folder of the **GeekQuiz** project and select **Add | New Scaffolded Item...**.</span></span>

    <span data-ttu-id="b85c9-215">![建立新的 scaffold 專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "建立新的 scaffold 專案")</span><span class="sxs-lookup"><span data-stu-id="b85c9-215">![Creating a new scaffolded item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Creating a new scaffolded item")</span></span>

    <span data-ttu-id="b85c9-216">*建立新的 scaffold 專案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-216">*Creating a new scaffolded item*</span></span>
5. <span data-ttu-id="b85c9-217">在 [**新增 Scaffold** ] 對話方塊中，確定已在左窗格中選取 [**一般**] 節點。</span><span class="sxs-lookup"><span data-stu-id="b85c9-217">In the **Add Scaffold** dialog box, make sure that the **Common** node is selected in the left pane.</span></span> <span data-ttu-id="b85c9-218">然後，在中央窗格中選取 [ **WEB API 2 控制器-空白**] 範本，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-218">Then, select the **Web API 2 Controller - Empty** template in the center pane and click **Add**.</span></span>

    <span data-ttu-id="b85c9-219">![選取 [Web API 2 控制器] 空白範本](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "選取 [Web API 2 控制器] 空白範本")</span><span class="sxs-lookup"><span data-stu-id="b85c9-219">![Selecting the Web API 2 Controller Empty template](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Selecting the Web API 2 Controller Empty template")</span></span>

    <span data-ttu-id="b85c9-220">*選取 [Web API 2 控制器] 空白範本*</span><span class="sxs-lookup"><span data-stu-id="b85c9-220">*Selecting the Web API 2 Controller Empty template*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b85c9-221">**ASP.NET**樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。</span><span class="sxs-lookup"><span data-stu-id="b85c9-221">**ASP.NET Scaffolding** is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="b85c9-222">Visual Studio 2013 包括適用于 MVC 和 Web API 專案的預先安裝程式碼產生器。</span><span class="sxs-lookup"><span data-stu-id="b85c9-222">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="b85c9-223">當您想要快速加入與資料模型互動的程式碼，以減少開發標準資料作業所需的時間量時，您應該使用專案中的樣板。</span><span class="sxs-lookup"><span data-stu-id="b85c9-223">You should use scaffolding in your project when you want to quickly add code that interacts with data models in order to reduce the amount of time required to develop standard data operations.</span></span>
    > 
    > <span data-ttu-id="b85c9-224">此樣板程式也可確保專案中已安裝所有必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="b85c9-224">The scaffolding process also ensures that all the required dependencies are installed in the project.</span></span> <span data-ttu-id="b85c9-225">例如，如果您從空的 ASP.NET 專案開始，然後使用樣板來新增 Web API 控制器，則會自動將必要的 Web API NuGet 套件和參考新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-225">For example, if you start with an empty ASP.NET project and then use scaffolding to add a Web API controller, the required Web API NuGet packages and references are added to your project automatically.</span></span>
6. <span data-ttu-id="b85c9-226">在 [**新增控制器**] 對話方塊中，于 [**控制器名稱**] 文字方塊中輸入*TriviaController* ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-226">In the **Add Controller** dialog box, type *TriviaController* in the **Controller name** text box and click **Add**.</span></span>

    <span data-ttu-id="b85c9-227">![新增邏輯控制器](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "新增邏輯控制器")</span><span class="sxs-lookup"><span data-stu-id="b85c9-227">![Adding the Trivia Controller](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Adding the Trivia Controller")</span></span>

    <span data-ttu-id="b85c9-228">*新增邏輯控制器*</span><span class="sxs-lookup"><span data-stu-id="b85c9-228">*Adding the Trivia Controller*</span></span>
7. <span data-ttu-id="b85c9-229">**TriviaController.cs**檔案接著會新增至**GeekQuiz**專案的 [**控制器**] 資料夾，其中包含空的**TriviaController**類別。</span><span class="sxs-lookup"><span data-stu-id="b85c9-229">The **TriviaController.cs** file is then added to the **Controllers** folder of the **GeekQuiz** project, containing an empty **TriviaController** class.</span></span> <span data-ttu-id="b85c9-230">在檔案開頭處新增下列 using 語句。</span><span class="sxs-lookup"><span data-stu-id="b85c9-230">Add the following using statements at the beginning of the file.</span></span>

    <span data-ttu-id="b85c9-231">（程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-231">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. <span data-ttu-id="b85c9-232">在**TriviaController**類別的開頭新增下列程式碼，以定義、初始化及處置控制器中的**TriviaCoNtext**實例。</span><span class="sxs-lookup"><span data-stu-id="b85c9-232">Add the following code at the beginning of the **TriviaController** class to define, initialize and dispose the **TriviaContext** instance in the controller.</span></span>

    <span data-ttu-id="b85c9-233">（程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerCoNtext*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-233">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="b85c9-234">**TriviaController**的**dispose**方法會叫用**TriviaCoNtext**實例的**dispose**方法，以確保在處置或垃圾收集**TriviaCoNtext**實例時，會釋放內容物件所使用的所有資源。</span><span class="sxs-lookup"><span data-stu-id="b85c9-234">The **Dispose** method of **TriviaController** invokes the **Dispose** method of the **TriviaContext** instance, which ensures that all the resources used by the context object are released when the **TriviaContext** instance is disposed or garbage-collected.</span></span> <span data-ttu-id="b85c9-235">這包括關閉 Entity Framework 開啟的所有資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="b85c9-235">This includes closing all database connections opened by Entity Framework.</span></span>
9. <span data-ttu-id="b85c9-236">將下列 helper 方法新增至**TriviaController**類別的結尾。</span><span class="sxs-lookup"><span data-stu-id="b85c9-236">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="b85c9-237">這個方法會從資料庫中抓取下列測驗問題，以供指定的使用者回答。</span><span class="sxs-lookup"><span data-stu-id="b85c9-237">This method retrieves the following quiz question from the database to be answered by the specified user.</span></span>

    <span data-ttu-id="b85c9-238">（程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-238">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. <span data-ttu-id="b85c9-239">將下列**Get**動作方法新增至**TriviaController**類別。</span><span class="sxs-lookup"><span data-stu-id="b85c9-239">Add the following **Get** action method to the **TriviaController** class.</span></span> <span data-ttu-id="b85c9-240">這個動作方法會呼叫在上一個步驟中定義的**NextQuestionAsync** helper 方法，以取得已驗證使用者的下一個問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-240">This action method calls the **NextQuestionAsync** helper method defined in the previous step to retrieve the next question for the authenticated user.</span></span>

    <span data-ttu-id="b85c9-241">（程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-241">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. <span data-ttu-id="b85c9-242">將下列 helper 方法新增至**TriviaController**類別的結尾。</span><span class="sxs-lookup"><span data-stu-id="b85c9-242">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="b85c9-243">這個方法會將指定的答案儲存在資料庫中，並傳回布林值，指出答案是否正確。</span><span class="sxs-lookup"><span data-stu-id="b85c9-243">This method stores the specified answer in the database and returns a Boolean value indicating whether or not the answer is correct.</span></span>

    <span data-ttu-id="b85c9-244">（程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-244">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. <span data-ttu-id="b85c9-245">將下列**Post**動作方法新增至**TriviaController**類別。</span><span class="sxs-lookup"><span data-stu-id="b85c9-245">Add the following **Post** action method to the **TriviaController** class.</span></span> <span data-ttu-id="b85c9-246">此動作方法會將答案與已驗證的使用者建立關聯，並呼叫**StoreAsync** helper 方法。</span><span class="sxs-lookup"><span data-stu-id="b85c9-246">This action method associates the answer to the authenticated user and calls the **StoreAsync** helper method.</span></span> <span data-ttu-id="b85c9-247">然後，它會傳送回應，其中包含 helper 方法所傳回的布林值。</span><span class="sxs-lookup"><span data-stu-id="b85c9-247">Then, it sends a response with the Boolean value returned by the helper method.</span></span>

    <span data-ttu-id="b85c9-248">（程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-248">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. <span data-ttu-id="b85c9-249">修改 Web API 控制器，藉由將**授權**屬性新增至**TriviaController**類別定義，來限制已驗證使用者的存取權。</span><span class="sxs-lookup"><span data-stu-id="b85c9-249">Modify the Web API controller to restrict access to authenticated users by adding the **Authorize** attribute to the **TriviaController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="b85c9-250">工作3–執行解決方案</span><span class="sxs-lookup"><span data-stu-id="b85c9-250">Task 3 – Running the Solution</span></span>

<span data-ttu-id="b85c9-251">在此工作中，您將確認您在上一個工作中建立的 Web API 服務是否如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="b85c9-251">In this task you will verify that the Web API service you built in the previous task is working as expected.</span></span> <span data-ttu-id="b85c9-252">您將使用 Internet Explorer **F12 開發人員工具**來捕獲網路流量，並檢查 Web API 服務的完整回應。</span><span class="sxs-lookup"><span data-stu-id="b85c9-252">You will use the Internet Explorer **F12 Developer Tools** to capture the network traffic and inspect the full response from the Web API service.</span></span>

> [!NOTE]
> <span data-ttu-id="b85c9-253">請確定已在 [Visual Studio] 工具列上的 [**開始**] 按鈕中選取**Internet Explorer** 。</span><span class="sxs-lookup"><span data-stu-id="b85c9-253">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 選項](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. <span data-ttu-id="b85c9-255">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-255">Press **F5** to run the solution.</span></span> <span data-ttu-id="b85c9-256">[**登入**] 頁面應該會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="b85c9-256">The **Log in** page should appear in the browser.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b85c9-257">當應用程式啟動時，預設的 MVC 路由會觸發，其預設會對應至**HomeController**類別的**索引**動作。</span><span class="sxs-lookup"><span data-stu-id="b85c9-257">When the application starts, the default MVC route is triggered, which by default is mapped to the **Index** action of the **HomeController** class.</span></span> <span data-ttu-id="b85c9-258">由於**HomeController**僅限於已驗證的使用者（請記住，您已使用練習1中的**授權**屬性來裝飾該類別），而且尚未驗證使用者，因此應用程式會將原始要求重新導向至 [登入] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b85c9-258">Since **HomeController** is restricted to authenticated users (remember that you decorated that class with the **Authorize** attribute in Exercise 1) and there is no user authenticated yet, the application redirects the original request to the log in page.</span></span>

    <span data-ttu-id="b85c9-259">![正在執行解決方案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "正在執行解決方案")</span><span class="sxs-lookup"><span data-stu-id="b85c9-259">![Running the solution](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Running the solution")</span></span>

    <span data-ttu-id="b85c9-260">*正在執行解決方案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-260">*Running the solution*</span></span>
2. <span data-ttu-id="b85c9-261">按一下 [**註冊**] 以建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="b85c9-261">Click **Register** to create a new user.</span></span>

    <span data-ttu-id="b85c9-262">![註冊新的使用者](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "註冊新的使用者")</span><span class="sxs-lookup"><span data-stu-id="b85c9-262">![Registering a new user](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registering a new user")</span></span>

    <span data-ttu-id="b85c9-263">*註冊新的使用者*</span><span class="sxs-lookup"><span data-stu-id="b85c9-263">*Registering a new user*</span></span>
3. <span data-ttu-id="b85c9-264">在 [**註冊**] 頁面中，輸入**使用者名稱**和**密碼**，然後按一下 [**註冊**]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-264">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="b85c9-265">![註冊頁面](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "註冊頁面")</span><span class="sxs-lookup"><span data-stu-id="b85c9-265">![Register page](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Register page")</span></span>

    <span data-ttu-id="b85c9-266">*註冊頁面*</span><span class="sxs-lookup"><span data-stu-id="b85c9-266">*Register page*</span></span>
4. <span data-ttu-id="b85c9-267">應用程式會註冊新帳戶，並驗證使用者並重新導向至首頁。</span><span class="sxs-lookup"><span data-stu-id="b85c9-267">The application registers the new account and the user is authenticated and redirected back to the home page.</span></span>

    <span data-ttu-id="b85c9-268">![使用者已通過驗證](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "使用者已驗證")</span><span class="sxs-lookup"><span data-stu-id="b85c9-268">![User is authenticated](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "User authenticated")</span></span>

    <span data-ttu-id="b85c9-269">*使用者已通過驗證*</span><span class="sxs-lookup"><span data-stu-id="b85c9-269">*User is authenticated*</span></span>
5. <span data-ttu-id="b85c9-270">在瀏覽器中，按**F12**開啟 [**開發人員工具**] 面板。</span><span class="sxs-lookup"><span data-stu-id="b85c9-270">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="b85c9-271">按**CTRL + 4**或按一下**網路**圖示，然後按一下綠色箭號按鈕以開始捕獲網路流量。</span><span class="sxs-lookup"><span data-stu-id="b85c9-271">Press **CTRL + 4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="b85c9-272">![正在起始 Web API 網路捕獲](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "正在起始 Web API 網路捕獲")</span><span class="sxs-lookup"><span data-stu-id="b85c9-272">![Initiating Web API network capture](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="b85c9-273">*正在起始 Web API 網路捕獲*</span><span class="sxs-lookup"><span data-stu-id="b85c9-273">*Initiating Web API network capture*</span></span>
6. <span data-ttu-id="b85c9-274">將**api/邏輯**附加至瀏覽器網址列中的 URL。</span><span class="sxs-lookup"><span data-stu-id="b85c9-274">Append **api/trivia** to the URL in the browser's address bar.</span></span> <span data-ttu-id="b85c9-275">您現在會從**TriviaController**中的**Get**動作方法，檢查回應的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b85c9-275">You will now inspect the details of the response from the **Get** action method in **TriviaController**.</span></span>

    <span data-ttu-id="b85c9-276">![透過 Web API 抓取下一個問題資料](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "透過 Web API 抓取下一個問題資料")</span><span class="sxs-lookup"><span data-stu-id="b85c9-276">![Retrieving the next question data through Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Retrieving the next question data through Web API")</span></span>

    <span data-ttu-id="b85c9-277">*透過 Web API 抓取下一個問題資料*</span><span class="sxs-lookup"><span data-stu-id="b85c9-277">*Retrieving the next question data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b85c9-278">下載完成後，系統會提示您對下載的檔案進行動作。</span><span class="sxs-lookup"><span data-stu-id="b85c9-278">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="b85c9-279">讓對話方塊保持開啟狀態，以便能夠透過 [開發人員] 工具視窗觀看回應內容。</span><span class="sxs-lookup"><span data-stu-id="b85c9-279">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
7. <span data-ttu-id="b85c9-280">現在，您將會檢查回應的主體。</span><span class="sxs-lookup"><span data-stu-id="b85c9-280">Now you will inspect the body of the response.</span></span> <span data-ttu-id="b85c9-281">若要這樣做，請按一下 [**詳細資料**] 索引標籤，然後按一下 [**回應主體**]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-281">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="b85c9-282">您可以使用屬性**選項**（這是**TriviaOption**物件的清單）、**識別碼**和對應至**TriviaQuestion**類別的**標題**，檢查下載的資料是否為物件。</span><span class="sxs-lookup"><span data-stu-id="b85c9-282">You can check that the downloaded data is an object with the properties **options** (which is a list of **TriviaOption** objects), **id** and **title** that correspond to the **TriviaQuestion** class.</span></span>

    <span data-ttu-id="b85c9-283">![查看 Web API 回應主體](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "查看 Web API 回應主體")</span><span class="sxs-lookup"><span data-stu-id="b85c9-283">![Viewing the Web API Response Body](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Viewing the Web API Response Body")</span></span>

    <span data-ttu-id="b85c9-284">*查看 Web API 回應主體*</span><span class="sxs-lookup"><span data-stu-id="b85c9-284">*Viewing Web API Response Body*</span></span>
8. <span data-ttu-id="b85c9-285">返回 Visual Studio，然後按**SHIFT + F5**停止調試。</span><span class="sxs-lookup"><span data-stu-id="b85c9-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a><span data-ttu-id="b85c9-286">練習2：建立 SPA 介面</span><span class="sxs-lookup"><span data-stu-id="b85c9-286">Exercise 2: Creating the SPA Interface</span></span>

<span data-ttu-id="b85c9-287">在此練習中，您將會先建立萬能技客測驗的 web 前端部分，並將焦點放在使用**AngularJS**的單一頁面應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="b85c9-287">In this exercise you will first build the web front-end portion of Geek Quiz, focusing on the Single-Page Application interaction using **AngularJS**.</span></span> <span data-ttu-id="b85c9-288">接著，您將使用 CSS3 來增強使用者體驗，以執行豐富的動畫，並在從一個問題轉換到下一個時，提供內容切換的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="b85c9-288">You will then enhance the user experience with CSS3 to perform rich animations and provide a visual effect of context switching when transitioning from one question to the next.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a><span data-ttu-id="b85c9-289">工作1–使用 AngularJS 建立 SPA 介面</span><span class="sxs-lookup"><span data-stu-id="b85c9-289">Task 1 – Creating the SPA Interface Using AngularJS</span></span>

<span data-ttu-id="b85c9-290">在這項工作中，您將使用**AngularJS**來執行萬能技客測驗應用程式的用戶端。</span><span class="sxs-lookup"><span data-stu-id="b85c9-290">In this task you will use **AngularJS** to implement the client side of the Geek Quiz application.</span></span> <span data-ttu-id="b85c9-291">**AngularJS**是一種開放原始碼 JavaScript 架構，可使用*模型視圖控制器*（MVC）功能來增強瀏覽器型應用程式，同時加速開發和測試。</span><span class="sxs-lookup"><span data-stu-id="b85c9-291">**AngularJS** is an open-source JavaScript framework that augments browser-based applications with *Model-View-Controller* (MVC) capability, facilitating both development and testing.</span></span>

<span data-ttu-id="b85c9-292">您會從 Visual Studio 的套件管理員主控台開始安裝 AngularJS。</span><span class="sxs-lookup"><span data-stu-id="b85c9-292">You will start by installing AngularJS from Visual Studio's Package Manager Console.</span></span> <span data-ttu-id="b85c9-293">接著，您將建立控制器來提供萬能技客測驗應用程式的行為，以及使用 AngularJS 範本引擎呈現測驗問題和答案的視圖。</span><span class="sxs-lookup"><span data-stu-id="b85c9-293">Then, you will create the controller to provide the behavior of the Geek Quiz app and the view to render the quiz questions and answers using the AngularJS template engine.</span></span>

> [!NOTE]
> <span data-ttu-id="b85c9-294">如需 AngularJS 的詳細資訊，請參閱[[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)。</span><span class="sxs-lookup"><span data-stu-id="b85c9-294">For more information about AngularJS, refer to [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).</span></span>

1. <span data-ttu-id="b85c9-295">開啟 [ **Visual Studio Express 2013 For Web** ]，然後開啟位於 [**來源/Ex2-CreatingASPAInterface/開始**] 資料夾中的 [ **GeekQuiz** ] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-295">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source/Ex2-CreatingASPAInterface/Begin** folder.</span></span> <span data-ttu-id="b85c9-296">或者，您可以繼續使用您在上一個練習中取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-296">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="b85c9-297">從 [**工具**] > [ **NuGet 套件管理員**] 開啟 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-297">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="b85c9-298">輸入下列命令以安裝**AngularJS** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="b85c9-298">Type the following command to install the **AngularJS.Core** NuGet package.</span></span>

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. <span data-ttu-id="b85c9-299">在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [**腳本**] 資料夾，然後選取 [**新增] |新增資料夾**。</span><span class="sxs-lookup"><span data-stu-id="b85c9-299">In **Solution Explorer**, right-click the **Scripts** folder of the **GeekQuiz** project and select **Add | New Folder**.</span></span> <span data-ttu-id="b85c9-300">將資料夾命名為**應用程式**，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="b85c9-300">Name the folder **app** and press **Enter**.</span></span>
4. <span data-ttu-id="b85c9-301">以滑鼠右鍵按一下您剛建立的**應用程式**資料夾，然後選取 [**新增] |JavaScript**檔案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-301">Right-click the **app** folder you just created and select **Add | JavaScript File**.</span></span>

    ![建立新的 JavaScript 檔案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    <span data-ttu-id="b85c9-303">*建立新的 JavaScript 檔案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-303">*Creating a new JavaScript file*</span></span>
5. <span data-ttu-id="b85c9-304">在 [**指定專案的名稱**] 對話方塊中，于 [**專案名稱**] 文字方塊中輸入 [*測驗-控制器*]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="b85c9-304">In the **Specify Name for Item** dialog box, type *quiz-controller* in the **Item name** text box and click **OK**.</span></span>

    ![命名新的 JavaScript 檔案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    <span data-ttu-id="b85c9-306">*命名新的 JavaScript 檔案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-306">*Naming the new JavaScript file*</span></span>
6. <span data-ttu-id="b85c9-307">在**quiz-controller**檔案中，新增下列程式碼以宣告和初始化 AngularJS **QuizCtrl**控制器。</span><span class="sxs-lookup"><span data-stu-id="b85c9-307">In the **quiz-controller.js** file, add the following code to declare and initialize the AngularJS **QuizCtrl** controller.</span></span>

    <span data-ttu-id="b85c9-308">（程式碼片段- *AspNetWebApiSpa-Ex2-AngularQuizController*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-308">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizController*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > <span data-ttu-id="b85c9-309">**QuizCtrl**控制器的函式函數需要名為 **$scope**的得以插入參數。</span><span class="sxs-lookup"><span data-stu-id="b85c9-309">The constructor function of the **QuizCtrl** controller expects an injectable parameter named **$scope**.</span></span> <span data-ttu-id="b85c9-310">範圍的初始狀態應該在函式函式中設定，方法是將屬性附加至 **$scope**物件。</span><span class="sxs-lookup"><span data-stu-id="b85c9-310">The initial state of the scope should be set up in the constructor function by attaching properties to the **$scope** object.</span></span> <span data-ttu-id="b85c9-311">屬性包含**視圖模型**，而且可以在註冊控制器時，供範本存取。</span><span class="sxs-lookup"><span data-stu-id="b85c9-311">The properties contain the **view model**, and will be accessible to the template when the controller is registered.</span></span>
    > 
    > <span data-ttu-id="b85c9-312">**QuizCtrl**控制器是在名為**QuizApp**的模組內定義。</span><span class="sxs-lookup"><span data-stu-id="b85c9-312">The **QuizCtrl** controller is defined inside a module named **QuizApp**.</span></span> <span data-ttu-id="b85c9-313">模組是工作單位，可讓您將應用程式分成不同的元件。</span><span class="sxs-lookup"><span data-stu-id="b85c9-313">Modules are units of work that let you break your application into separate components.</span></span> <span data-ttu-id="b85c9-314">使用模組的主要優點在於程式碼較容易瞭解，並可協助進行單元測試、重複使用和可維護性。</span><span class="sxs-lookup"><span data-stu-id="b85c9-314">The main advantages of using modules is that the code is easier to understand and facilitates unit testing, reusability and maintainability.</span></span>
7. <span data-ttu-id="b85c9-315">您現在會將行為新增至範圍，以回應從視圖觸發的事件。</span><span class="sxs-lookup"><span data-stu-id="b85c9-315">You will now add behavior to the scope in order to react to events triggered from the view.</span></span> <span data-ttu-id="b85c9-316">在**QuizCtrl**控制器的結尾新增下列程式碼，以在 **$scope**物件中定義**nextQuestion**函數。</span><span class="sxs-lookup"><span data-stu-id="b85c9-316">Add the following code at the end of the **QuizCtrl** controller to define the **nextQuestion** function in the **$scope** object.</span></span>

    <span data-ttu-id="b85c9-317">（程式碼片段- *AspNetWebApiSpa-Ex2-AngularQuizControllerNextQuestion*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-317">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > <span data-ttu-id="b85c9-318">此函式會從上一個練習中建立的**邏輯**Web API 抓取下一個問題，並將問題資料附加至 **$scope**物件。</span><span class="sxs-lookup"><span data-stu-id="b85c9-318">This function retrieves the next question from the **Trivia** Web API created in the previous exercise and attaches the question data to the **$scope** object.</span></span>
8. <span data-ttu-id="b85c9-319">在**QuizCtrl**控制器的結尾插入下列程式碼，以在 **$scope**物件中定義**sendAnswer**函數。</span><span class="sxs-lookup"><span data-stu-id="b85c9-319">Insert the following code at the end of the **QuizCtrl** controller to define the **sendAnswer** function in the **$scope** object.</span></span>

    <span data-ttu-id="b85c9-320">（程式碼片段- *AspNetWebApiSpa-Ex2-AngularQuizControllerSendAnswer*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-320">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > <span data-ttu-id="b85c9-321">此函式會將使用者選取的答案傳送至**邏輯**Web API，並將結果（亦即答案是否正確）儲存在 **$scope**物件中。</span><span class="sxs-lookup"><span data-stu-id="b85c9-321">This function sends the answer selected by the user to the **Trivia** Web API and stores the result –i.e. if the answer is correct or not– in the **$scope** object.</span></span>
    > 
    > <span data-ttu-id="b85c9-322">上述的**nextQuestion**和**sendAnswer**函式會使用 AngularJS **$HTTP**物件，透過瀏覽器中的 XMLHttpRequest JAVASCRIPT 物件來抽象化與 Web API 的通訊。</span><span class="sxs-lookup"><span data-stu-id="b85c9-322">The **nextQuestion** and **sendAnswer** functions from above use the AngularJS **$http** object to abstract the communication with the Web API via the XMLHttpRequest JavaScript object from the browser.</span></span> <span data-ttu-id="b85c9-323">AngularJS 支援另一項服務，可透過 RESTful Api，引進更高層級的抽象概念，對資源執行 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="b85c9-323">AngularJS supports another service that brings a higher level of abstraction to perform CRUD operations against a resource through RESTful APIs.</span></span> <span data-ttu-id="b85c9-324">AngularJS **$resource**物件具有動作方法，可提供高階行為，而不需要與 **$HTTP**物件互動。</span><span class="sxs-lookup"><span data-stu-id="b85c9-324">The AngularJS **$resource** object has action methods which provide high-level behaviors without the need to interact with the **$http** object.</span></span> <span data-ttu-id="b85c9-325">請考慮在需要 CRUD 模型的案例中使用 **$resource**物件（前景資訊，請參閱[$resource 檔](https://docs.angularjs.org/api/ngResource/service/$resource)）。</span><span class="sxs-lookup"><span data-stu-id="b85c9-325">Consider using the **$resource** object in scenarios that requires the CRUD model (fore information, see the [$resource documentation](https://docs.angularjs.org/api/ngResource/service/$resource)).</span></span>
9. <span data-ttu-id="b85c9-326">下一步是建立可定義測驗視圖的 AngularJS 範本。</span><span class="sxs-lookup"><span data-stu-id="b85c9-326">The next step is to create the AngularJS template that defines the view for the quiz.</span></span> <span data-ttu-id="b85c9-327">若要這麼做，請開啟 Views 內的**Index. cshtml**檔案 **|主**資料夾，並將內容取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b85c9-327">To do this, open the **Index.cshtml** file inside the **Views | Home** folder and replace the content with the following code.</span></span>

    <span data-ttu-id="b85c9-328">（程式碼片段- *AspNetWebApiSpa-Ex2-GeekQuizView*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-328">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizView*)</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="b85c9-329">AngularJS 範本是一種宣告式規格，它會使用來自模型的資訊和控制器，將靜態標記轉換成使用者在瀏覽器中看到的動態視圖。</span><span class="sxs-lookup"><span data-stu-id="b85c9-329">The AngularJS template is a declarative specification that uses information from the model and the controller to transform static markup into the dynamic view that the user sees in the browser.</span></span> <span data-ttu-id="b85c9-330">以下是可在範本中使用的 AngularJS 元素和元素屬性範例：</span><span class="sxs-lookup"><span data-stu-id="b85c9-330">The following are examples of AngularJS elements and element attributes that can be used in a template:</span></span>
    > 
    > - <span data-ttu-id="b85c9-331">**Ng 應用**程式指示詞會告訴 AngularJS 代表應用程式之根項目的 DOM 元素。</span><span class="sxs-lookup"><span data-stu-id="b85c9-331">The **ng-app** directive tells AngularJS the DOM element that represents the root element of the application.</span></span>
    > - <span data-ttu-id="b85c9-332">**Ng 控制器**指示詞會在宣告指示詞的位置，將控制器附加至 DOM。</span><span class="sxs-lookup"><span data-stu-id="b85c9-332">The **ng-controller** directive attaches a controller to the DOM at the point where the directive is declared.</span></span>
    > - <span data-ttu-id="b85c9-333">大括弧標記法 **{{}}** 代表控制器中定義之範圍屬性的系結。</span><span class="sxs-lookup"><span data-stu-id="b85c9-333">The curly brace notation **{{ }}** denotes bindings to the scope properties defined in the controller.</span></span>
    > - <span data-ttu-id="b85c9-334">**Ng click**指示詞是用來叫用範圍中定義的函式，以回應使用者按下的動作。</span><span class="sxs-lookup"><span data-stu-id="b85c9-334">The **ng-click** directive is used to invoke the functions defined in the scope in response to user clicks.</span></span>
10. <span data-ttu-id="b85c9-335">開啟**Content**資料夾內的 **.css**檔案，並在檔案結尾新增下列反白顯示的樣式，以提供測驗視圖的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="b85c9-335">Open the **Site.css** file inside the **Content** folder and add the following highlighted styles at the end of the file to provide a look and feel for the quiz view.</span></span>

    <span data-ttu-id="b85c9-336">（程式碼片段- *AspNetWebApiSpa-Ex2-GeekQuizStyles*）</span><span class="sxs-lookup"><span data-stu-id="b85c9-336">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="b85c9-337">工作2–執行解決方案</span><span class="sxs-lookup"><span data-stu-id="b85c9-337">Task 2 – Running the Solution</span></span>

<span data-ttu-id="b85c9-338">在這項工作中，您將使用以 AngularJS 建立的新使用者介面來執行解決方案，以回答一些測驗問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-338">In this task you will execute the solution using the new user interface you built with AngularJS to answer some of the quiz questions.</span></span>

1. <span data-ttu-id="b85c9-339">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-339">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="b85c9-340">註冊新的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b85c9-340">Register a new user account.</span></span> <span data-ttu-id="b85c9-341">若要這麼做，請遵循練習1，工作3中所述的註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="b85c9-341">To do this, follow the registration steps described in Exercise 1, Task 3.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b85c9-342">如果您使用上一個練習中的解決方案，您可以使用先前建立的使用者帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="b85c9-342">If you are using the solution from the previous exercise, you can log in with the user account you created before.</span></span>
3. <span data-ttu-id="b85c9-343">首頁**應該**會出現，並顯示測驗的第一個問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-343">The **Home** page should appear, showing the first question of the quiz.</span></span> <span data-ttu-id="b85c9-344">按一下其中一個選項來回答問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-344">Answer the question by clicking one of the options.</span></span> <span data-ttu-id="b85c9-345">這會觸發稍早定義的**sendAnswer**函式，這會將選取的選項傳送至**邏輯**Web API。</span><span class="sxs-lookup"><span data-stu-id="b85c9-345">This will trigger the **sendAnswer** function defined earlier, which sends the selected option to the **Trivia** Web API.</span></span>

    <span data-ttu-id="b85c9-346">![回答問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "回答問題")</span><span class="sxs-lookup"><span data-stu-id="b85c9-346">![Answering a question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Answering a question")</span></span>

    <span data-ttu-id="b85c9-347">*回答問題*</span><span class="sxs-lookup"><span data-stu-id="b85c9-347">*Answering a question*</span></span>
4. <span data-ttu-id="b85c9-348">按一下其中一個按鈕之後，應該會出現答案。</span><span class="sxs-lookup"><span data-stu-id="b85c9-348">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="b85c9-349">按一下 **[下一個問題]** 以顯示下列問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-349">Click **Next Question** to show the following question.</span></span> <span data-ttu-id="b85c9-350">這會觸發控制器中定義的**nextQuestion**函數。</span><span class="sxs-lookup"><span data-stu-id="b85c9-350">This will trigger the **nextQuestion** function defined in the controller.</span></span>

    <span data-ttu-id="b85c9-351">![要求下一個問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "要求下一個問題")</span><span class="sxs-lookup"><span data-stu-id="b85c9-351">![Requesting the next question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Requesting the next question")</span></span>

    <span data-ttu-id="b85c9-352">*要求下一個問題*</span><span class="sxs-lookup"><span data-stu-id="b85c9-352">*Requesting the next question*</span></span>
5. <span data-ttu-id="b85c9-353">下一個問題應該會出現。</span><span class="sxs-lookup"><span data-stu-id="b85c9-353">The next question should appear.</span></span> <span data-ttu-id="b85c9-354">依照您的需要，繼續回答問題數次。</span><span class="sxs-lookup"><span data-stu-id="b85c9-354">Continue answering questions as many times as you want.</span></span> <span data-ttu-id="b85c9-355">完成所有問題之後，您應該會回到第一個問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-355">After completing all the questions you should return to the first question.</span></span>

    <span data-ttu-id="b85c9-356">![另一個問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "另一個問題")</span><span class="sxs-lookup"><span data-stu-id="b85c9-356">![Another question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Another question")</span></span>

    <span data-ttu-id="b85c9-357">*下一個問題*</span><span class="sxs-lookup"><span data-stu-id="b85c9-357">*Next question*</span></span>
6. <span data-ttu-id="b85c9-358">返回 Visual Studio，然後按**SHIFT + F5**停止調試。</span><span class="sxs-lookup"><span data-stu-id="b85c9-358">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a><span data-ttu-id="b85c9-359">工作 3-使用 CSS3 建立翻轉動畫</span><span class="sxs-lookup"><span data-stu-id="b85c9-359">Task 3 – Creating a Flip Animation Using CSS3</span></span>

<span data-ttu-id="b85c9-360">在這項工作中，您將使用 CSS3 屬性來執行豐富的動畫，方法是在問題獲得解答時新增翻轉效果，以及何時抓取下一個問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-360">In this task you will use CSS3 properties to perform rich animations by adding a flip effect when a question is answered and when the next question is retrieved.</span></span>

1. <span data-ttu-id="b85c9-361">在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [ **Content** ] 資料夾，然後選取 [**新增] |現有專案 ...** 。</span><span class="sxs-lookup"><span data-stu-id="b85c9-361">In **Solution Explorer**, right-click the **Content** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="b85c9-362">![將現有的專案加入至 Content 資料夾](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "將現有的專案加入至 Content 資料夾")</span><span class="sxs-lookup"><span data-stu-id="b85c9-362">![Adding an existing item to the Content folder](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Adding an existing item to the Content folder")</span></span>

    <span data-ttu-id="b85c9-363">*將現有的專案加入至 Content 資料夾*</span><span class="sxs-lookup"><span data-stu-id="b85c9-363">*Adding an existing item to the Content folder*</span></span>
2. <span data-ttu-id="b85c9-364">在 [**加入現有專案**] 對話方塊中，流覽至 [**來源/資產**] 資料夾，然後選取 [ **Flip .css**]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-364">In the **Add Existing Item** dialog box, navigate to the **Source/Assets** folder and select **Flip.css**.</span></span> <span data-ttu-id="b85c9-365">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b85c9-365">Click **Add**.</span></span>

    <span data-ttu-id="b85c9-366">![從資產新增 Flip .css 檔案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "從資產新增 Flip .css 檔案")</span><span class="sxs-lookup"><span data-stu-id="b85c9-366">![Adding the Flip.css file from Assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Adding the Flip.css file from Assets")</span></span>

    <span data-ttu-id="b85c9-367">*從資產新增 Flip .css 檔案*</span><span class="sxs-lookup"><span data-stu-id="b85c9-367">*Adding the Flip.css file from Assets*</span></span>
3. <span data-ttu-id="b85c9-368">開啟您剛才新增的**Flip .css**檔案，並檢查其內容。</span><span class="sxs-lookup"><span data-stu-id="b85c9-368">Open the **Flip.css** file you just added and inspect its content.</span></span>
4. <span data-ttu-id="b85c9-369">找出**翻轉轉換**批註。</span><span class="sxs-lookup"><span data-stu-id="b85c9-369">Locate the **flip transformation** comment.</span></span> <span data-ttu-id="b85c9-370">該批註底下的樣式會使用 CSS 的**觀點**和**rotateY**轉換來產生 &quot;卡翻轉&quot; 效果。</span><span class="sxs-lookup"><span data-stu-id="b85c9-370">The styles below that comment use the CSS **perspective** and **rotateY** transformations to generate a &quot;card flip&quot; effect.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. <span data-ttu-id="b85c9-371">在翻轉批註期間，找出窗格的 [**隱藏後一步]** 。</span><span class="sxs-lookup"><span data-stu-id="b85c9-371">Locate the **hide back of pane during flip** comment.</span></span> <span data-ttu-id="b85c9-372">此批註底下的樣式會在臉部離開檢視器時，將**背面可見度**CSS 屬性設定為*hidden*，以隱藏其後端。</span><span class="sxs-lookup"><span data-stu-id="b85c9-372">The style below that comment hides the back-side of the faces when they are facing away from the viewer by setting the **backface-visibility** CSS property to *hidden*.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. <span data-ttu-id="b85c9-373">開啟**應用程式\_[開始**] 資料夾中的**BundleConfig.cs**檔案，並將參考新增至 **&quot;~/Content/css&quot;** 樣式組合中的**Flip .css**檔案</span><span class="sxs-lookup"><span data-stu-id="b85c9-373">Open the **BundleConfig.cs** file inside the **App\_Start** folder and add the reference to the **Flip.css** file in the **&quot;~/Content/css&quot;** style bundle</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. <span data-ttu-id="b85c9-374">按**F5**執行方案，並使用您的認證登入。</span><span class="sxs-lookup"><span data-stu-id="b85c9-374">Press **F5** to run the solution and log in with your credentials.</span></span>
8. <span data-ttu-id="b85c9-375">按一下其中一個選項來回答問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-375">Answer a question by clicking one of the options.</span></span> <span data-ttu-id="b85c9-376">請注意在流覽之間轉換時的翻轉效果。</span><span class="sxs-lookup"><span data-stu-id="b85c9-376">Notice the flip effect when transitioning between views.</span></span>

    <span data-ttu-id="b85c9-377">![使用翻轉效果回答問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "使用翻轉效果回答問題")</span><span class="sxs-lookup"><span data-stu-id="b85c9-377">![Answering a question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Answering a question with the flip effect")</span></span>

    <span data-ttu-id="b85c9-378">*使用翻轉效果回答問題*</span><span class="sxs-lookup"><span data-stu-id="b85c9-378">*Answering a question with the flip effect*</span></span>
9. <span data-ttu-id="b85c9-379">按一下 **[下一個問題]** 以取得下列問題。</span><span class="sxs-lookup"><span data-stu-id="b85c9-379">Click **Next Question** to retrieve the following question.</span></span> <span data-ttu-id="b85c9-380">翻轉效果應該會再次出現。</span><span class="sxs-lookup"><span data-stu-id="b85c9-380">The flip effect should appear again.</span></span>

    <span data-ttu-id="b85c9-381">![使用 flip 效果抓取下列問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "使用 flip 效果抓取下列問題")</span><span class="sxs-lookup"><span data-stu-id="b85c9-381">![Retrieving the following question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Retrieving the following question with the flip effect")</span></span>

    <span data-ttu-id="b85c9-382">*使用 flip 效果抓取下列問題*</span><span class="sxs-lookup"><span data-stu-id="b85c9-382">*Retrieving the following question with the flip effect*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b85c9-383">總結</span><span class="sxs-lookup"><span data-stu-id="b85c9-383">Summary</span></span>

<span data-ttu-id="b85c9-384">藉由完成此實際操作實驗室，您已瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="b85c9-384">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="b85c9-385">使用 ASP.NET 的框架建立 ASP.NET Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="b85c9-385">Create an ASP.NET Web API controller using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="b85c9-386">執行 Web API Get 動作以取得下一個測驗問題</span><span class="sxs-lookup"><span data-stu-id="b85c9-386">Implement a Web API Get action to retrieve the next quiz question</span></span>
- <span data-ttu-id="b85c9-387">執行 Web API Post 動作以儲存測驗解答</span><span class="sxs-lookup"><span data-stu-id="b85c9-387">Implement a Web API Post action to store the quiz answers</span></span>
- <span data-ttu-id="b85c9-388">從 Visual Studio 套件管理員主控台安裝 AngularJS</span><span class="sxs-lookup"><span data-stu-id="b85c9-388">Install AngularJS from the Visual Studio Package Manager Console</span></span>
- <span data-ttu-id="b85c9-389">執行 AngularJS 範本和控制器</span><span class="sxs-lookup"><span data-stu-id="b85c9-389">Implement AngularJS templates and controllers</span></span>
- <span data-ttu-id="b85c9-390">使用 CSS3 轉換來執行動畫效果</span><span class="sxs-lookup"><span data-stu-id="b85c9-390">Use CSS3 transitions to perform animation effects</span></span>
