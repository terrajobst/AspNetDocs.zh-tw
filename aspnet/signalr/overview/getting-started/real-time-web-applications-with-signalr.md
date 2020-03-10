---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 實習實驗室：使用 SignalR 的即時 Web 應用程式 |Microsoft Docs
author: bradygaster
description: 即時 Web 應用程式可讓您即時將伺服器端內容推送至連線的用戶端。 針對 ASP.NET 開發人員，ASP ...。
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537097"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="43c3d-104">實習實驗室：使用 SignalR 的即時 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="43c3d-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>

<span data-ttu-id="43c3d-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="43c3d-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="43c3d-106">下載 Web Camp 訓練套件，2015年10月版本</span><span class="sxs-lookup"><span data-stu-id="43c3d-106">Download Web Camps Training Kit, October 2015 Release</span></span>](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> <span data-ttu-id="43c3d-107">即時 Web 應用程式可讓您即時將伺服器端內容推送至連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="43c3d-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="43c3d-108">針對 ASP.NET 開發人員， **ASP.NET SignalR**是一種程式庫，可將即時 web 功能新增至其應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c3d-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="43c3d-109">它會利用數個傳輸，並根據用戶端和伺服器的最佳可用傳輸，自動選取最佳可用的傳輸。</span><span class="sxs-lookup"><span data-stu-id="43c3d-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="43c3d-110">它會利用**WebSocket**，這是可在瀏覽器和伺服器之間進行雙向通訊的 HTML5 API。</span><span class="sxs-lookup"><span data-stu-id="43c3d-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="43c3d-111">**SignalR**也提供簡單的高階 API，可在您的 ASP.NET 應用程式中執行伺服器到用戶端 RPC （從伺服器端的 .net 程式碼呼叫 JavaScript 函式），以及為連線管理新增有用的勾點，例如連接/中斷線上活動、群組連接和授權。</span><span class="sxs-lookup"><span data-stu-id="43c3d-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="43c3d-112">**SignalR**是在用戶端與伺服器之間進行即時工作所需的一些傳輸的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="43c3d-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="43c3d-113">**SignalR**連線會以 HTTP 啟動，然後升級至**WebSocket**連線（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="43c3d-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="43c3d-114">**WebSocket**是**SignalR**的理想傳輸，因為它最有效率地使用伺服器記憶體、具有最低延遲，而且具有最基本的功能（例如用戶端與伺服器之間的全雙工通訊），但它也具有最嚴格的需求： **WebSocket**要求伺服器必須使用**windows server 2012**或**windows 8**，以及 **.NET Framework 4.5**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="43c3d-115">如果不符合這些需求， **SignalR**會嘗試使用其他傳輸來建立其連接（例如*Ajax 長輪詢*）。</span><span class="sxs-lookup"><span data-stu-id="43c3d-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="43c3d-116">**SignalR** API 包含兩個可在用戶端和伺服器之間通訊的模型：**持續**連線和**中樞**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="43c3d-117">**連接**代表傳送單一收件者、群組或廣播訊息的簡單端點。</span><span class="sxs-lookup"><span data-stu-id="43c3d-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="43c3d-118">**中樞**是以連線 API 為基礎所建立的高階管線，可讓您的用戶端和伺服器直接對彼此呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="43c3d-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR 架構](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="43c3d-120">所有範例程式碼和程式碼片段都包含在2015年10月版的 Web Camp 訓練套件中，可在[https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)取得。</span><span class="sxs-lookup"><span data-stu-id="43c3d-120">All sample code and snippets are included in the Web Camps Training Kit, October 2015 Release, available at [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b).</span></span>  <span data-ttu-id="43c3d-121">請注意，該頁面上的安裝程式連結將無法再運作;請改為使用 [資產] 區段下的其中一個連結。</span><span class="sxs-lookup"><span data-stu-id="43c3d-121">Please note that the Installer link on that page no longer works; use one of the links under the Assets section instead.</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="43c3d-122">概觀</span><span class="sxs-lookup"><span data-stu-id="43c3d-122">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="43c3d-123">目標</span><span class="sxs-lookup"><span data-stu-id="43c3d-123">Objectives</span></span>

<span data-ttu-id="43c3d-124">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="43c3d-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="43c3d-125">使用 SignalR 將通知從伺服器傳送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="43c3d-125">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="43c3d-126">使用**SQL Server**Scale Out SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c3d-126">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="43c3d-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43c3d-127">Prerequisites</span></span>

<span data-ttu-id="43c3d-128">若要完成此實際操作實驗室，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="43c3d-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="43c3d-129">[適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="43c3d-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="43c3d-130">安裝程式</span><span class="sxs-lookup"><span data-stu-id="43c3d-130">Setup</span></span>

<span data-ttu-id="43c3d-131">為了在此實際操作實驗室中執行練習，您必須先設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="43c3d-131">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="43c3d-132">開啟 Windows Explorer 視窗，並流覽至實驗室的 [**源**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="43c3d-132">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="43c3d-133">以滑鼠右鍵按一下 [ **Setup** ]，然後選取 [以**系統管理員身分執行**] 來啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="43c3d-133">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="43c3d-134">如果顯示 [使用者帳戶控制] 對話方塊，請確認動作以繼續。</span><span class="sxs-lookup"><span data-stu-id="43c3d-134">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="43c3d-135">執行安裝程式之前，請確定您已檢查過此實驗室的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="43c3d-135">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="43c3d-136">使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="43c3d-136">Using the Code Snippets</span></span>

<span data-ttu-id="43c3d-137">在整個實驗室檔中，系統會指示您插入程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="43c3d-137">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="43c3d-138">為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 2013 內進行存取，以避免必須以手動方式新增。</span><span class="sxs-lookup"><span data-stu-id="43c3d-138">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="43c3d-139">每個練習都附有一個起始解決方案，此方案位於練習的 [**開始**] 資料夾中，可讓您獨立于其他練習之外進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="43c3d-139">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="43c3d-140">請注意，在練習期間新增的程式碼片段缺少這些起始的解決方案，而且在您完成練習之前可能無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="43c3d-140">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="43c3d-141">在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的**結束**資料夾，其中含有完成對應練習中步驟所產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="43c3d-141">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="43c3d-142">如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。</span><span class="sxs-lookup"><span data-stu-id="43c3d-142">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="43c3d-143">練習</span><span class="sxs-lookup"><span data-stu-id="43c3d-143">Exercises</span></span>

<span data-ttu-id="43c3d-144">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="43c3d-144">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="43c3d-145">使用 SignalR 處理即時資料</span><span class="sxs-lookup"><span data-stu-id="43c3d-145">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="43c3d-146">使用 SQL Server 相應放大</span><span class="sxs-lookup"><span data-stu-id="43c3d-146">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="43c3d-147">完成此實驗室的預估時間： **60 分鐘**</span><span class="sxs-lookup"><span data-stu-id="43c3d-147">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="43c3d-148">當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。</span><span class="sxs-lookup"><span data-stu-id="43c3d-148">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="43c3d-149">每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。</span><span class="sxs-lookup"><span data-stu-id="43c3d-149">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="43c3d-150">本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。</span><span class="sxs-lookup"><span data-stu-id="43c3d-150">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="43c3d-151">如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。</span><span class="sxs-lookup"><span data-stu-id="43c3d-151">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="43c3d-152">練習1：使用 SignalR 處理即時資料</span><span class="sxs-lookup"><span data-stu-id="43c3d-152">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="43c3d-153">雖然對話通常是用來做為範例，但您可以使用即時 Web 功能來完成更多工作。</span><span class="sxs-lookup"><span data-stu-id="43c3d-153">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="43c3d-154">每當使用者重新整理網頁以查看新資料或頁面執行 Ajax 長期輪詢來取得新資料時，您可以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="43c3d-154">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="43c3d-155">SignalR 支援**伺服器推**播或**廣播**功能;它會自動處理連接管理。</span><span class="sxs-lookup"><span data-stu-id="43c3d-155">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="43c3d-156">在用戶端-伺服器通訊的傳統 HTTP 連線中，會針對每個要求重新建立連線，但 SignalR 會提供用戶端與伺服器之間的持續連線。</span><span class="sxs-lookup"><span data-stu-id="43c3d-156">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="43c3d-157">在 SignalR 中，伺服器程式碼會使用遠端程序呼叫（RPC）來呼叫瀏覽器中的用戶端程式代碼，而不是我們今天知道的要求-回應模型。</span><span class="sxs-lookup"><span data-stu-id="43c3d-157">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="43c3d-158">在此練習中，您會將**萬能技客測驗**應用程式設定為使用 SignalR，以更新的計量顯示統計資料儀表板，而不需要重新整理整個頁面。</span><span class="sxs-lookup"><span data-stu-id="43c3d-158">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="43c3d-159">工作1–探索萬能技客測驗統計資料頁面</span><span class="sxs-lookup"><span data-stu-id="43c3d-159">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="43c3d-160">在這項工作中，您將會經歷應用程式，並確認統計資料頁面的顯示方式，以及如何改善資訊的更新方式。</span><span class="sxs-lookup"><span data-stu-id="43c3d-160">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="43c3d-161">開啟 [ **Visual Studio Express 2013 For Web** ]，然後開啟位於**Source\Ex1-WorkingWithRealTimeData\Begin**資料夾中的 [ **GeekQuiz** ] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-161">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="43c3d-162">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-162">Press **F5** to run the solution.</span></span> <span data-ttu-id="43c3d-163">[**登入**] 頁面應該會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="43c3d-163">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="43c3d-164">![正在執行解決方案](real-time-web-applications-with-signalr/_static/image2.png "正在執行解決方案")</span><span class="sxs-lookup"><span data-stu-id="43c3d-164">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    <span data-ttu-id="43c3d-165">*正在執行解決方案*</span><span class="sxs-lookup"><span data-stu-id="43c3d-165">*Running the solution*</span></span>
3. <span data-ttu-id="43c3d-166">按一下頁面右上角的 [**註冊**]，在應用程式中建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="43c3d-166">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="43c3d-167">![註冊連結](real-time-web-applications-with-signalr/_static/image3.png "註冊連結")</span><span class="sxs-lookup"><span data-stu-id="43c3d-167">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    <span data-ttu-id="43c3d-168">*註冊連結*</span><span class="sxs-lookup"><span data-stu-id="43c3d-168">*Register link*</span></span>
4. <span data-ttu-id="43c3d-169">在 [**註冊**] 頁面中，輸入**使用者名稱**和**密碼**，然後按一下 [**註冊**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-169">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="43c3d-170">![註冊使用者](real-time-web-applications-with-signalr/_static/image4.png "註冊使用者")</span><span class="sxs-lookup"><span data-stu-id="43c3d-170">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    <span data-ttu-id="43c3d-171">*註冊使用者*</span><span class="sxs-lookup"><span data-stu-id="43c3d-171">*Registering a user*</span></span>
5. <span data-ttu-id="43c3d-172">應用程式會註冊新帳戶，並驗證使用者並重新導向至顯示第一個測驗問題的首頁。</span><span class="sxs-lookup"><span data-stu-id="43c3d-172">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="43c3d-173">在新視窗中開啟 [**統計資料]** 頁面，然後並排放置 [**首頁**] 和 [**統計資料]** 頁面。</span><span class="sxs-lookup"><span data-stu-id="43c3d-173">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="43c3d-174">![並存視窗](real-time-web-applications-with-signalr/_static/image5.png "並存視窗")</span><span class="sxs-lookup"><span data-stu-id="43c3d-174">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    <span data-ttu-id="43c3d-175">*並存視窗*</span><span class="sxs-lookup"><span data-stu-id="43c3d-175">*Side-by-side windows*</span></span>
7. <span data-ttu-id="43c3d-176">在首頁**中**，按一下其中一個選項來回答問題。</span><span class="sxs-lookup"><span data-stu-id="43c3d-176">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="43c3d-177">![回答問題](real-time-web-applications-with-signalr/_static/image6.png "回答問題")</span><span class="sxs-lookup"><span data-stu-id="43c3d-177">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    <span data-ttu-id="43c3d-178">*回答問題*</span><span class="sxs-lookup"><span data-stu-id="43c3d-178">*Answering a question*</span></span>
8. <span data-ttu-id="43c3d-179">按一下其中一個按鈕之後，應該會出現答案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-179">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="43c3d-180">![問題解答正確](real-time-web-applications-with-signalr/_static/image7.png "問題解答正確")</span><span class="sxs-lookup"><span data-stu-id="43c3d-180">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    <span data-ttu-id="43c3d-181">*已正確回答問題*</span><span class="sxs-lookup"><span data-stu-id="43c3d-181">*Question answered correctly*</span></span>
9. <span data-ttu-id="43c3d-182">請注意，統計資料頁面中提供的資訊已過期。</span><span class="sxs-lookup"><span data-stu-id="43c3d-182">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="43c3d-183">重新整理頁面，以便查看更新的結果。</span><span class="sxs-lookup"><span data-stu-id="43c3d-183">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="43c3d-184">![統計資料頁面](real-time-web-applications-with-signalr/_static/image8.png "統計資料頁面")</span><span class="sxs-lookup"><span data-stu-id="43c3d-184">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    <span data-ttu-id="43c3d-185">*統計資料頁面*</span><span class="sxs-lookup"><span data-stu-id="43c3d-185">*Statistics page*</span></span>
10. <span data-ttu-id="43c3d-186">返回 Visual Studio 並停止調試。</span><span class="sxs-lookup"><span data-stu-id="43c3d-186">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="43c3d-187">工作2–將 SignalR 新增至萬能技客測驗以顯示線上圖表</span><span class="sxs-lookup"><span data-stu-id="43c3d-187">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="43c3d-188">在這項工作中，您會將 SignalR 新增至解決方案，並在新的回應傳送至伺服器時，自動將更新傳送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="43c3d-188">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="43c3d-189">從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-189">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="43c3d-190">在 [**套件管理員主控台**] 視窗中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="43c3d-190">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="43c3d-191">![SignalR 套件安裝](real-time-web-applications-with-signalr/_static/image9.png "SignalR 套件安裝")</span><span class="sxs-lookup"><span data-stu-id="43c3d-191">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    <span data-ttu-id="43c3d-192">*SignalR 套件安裝*</span><span class="sxs-lookup"><span data-stu-id="43c3d-192">*SignalR package installation*</span></span>

   > [!NOTE]
   > <span data-ttu-id="43c3d-193">從全新的 MVC 5 應用程式安裝**SignalR** NuGet 套件版本2.0.2 時，您必須手動將**OWIN**套件更新為2.0.1 版（或更高版本），才能安裝 SignalR。</span><span class="sxs-lookup"><span data-stu-id="43c3d-193">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="43c3d-194">若要這樣做，您可以在 [**套件管理員主控台**] 中執行下列腳本：</span><span class="sxs-lookup"><span data-stu-id="43c3d-194">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="43c3d-195">在未來的 SignalR 版本中，將會自動更新 OWIN 相依性。</span><span class="sxs-lookup"><span data-stu-id="43c3d-195">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="43c3d-196">在**方案總管**中，展開 [**腳本**] 資料夾，並注意 SignalR *js*檔案已新增至方案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-196">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="43c3d-197">![SignalR JavaScript 參考](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 參考")</span><span class="sxs-lookup"><span data-stu-id="43c3d-197">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    <span data-ttu-id="43c3d-198">*SignalR JavaScript 參考*</span><span class="sxs-lookup"><span data-stu-id="43c3d-198">*SignalR JavaScript references*</span></span>
4. <span data-ttu-id="43c3d-199">在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案，選取 [**新增] | 新資料夾**，並**將**其命名為 [**中樞**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-199">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="43c3d-200">以滑鼠右鍵按一下 [**中樞**] 資料夾，然後選取 [**新增] |新專案**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-200">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="43c3d-201">![加入新專案](real-time-web-applications-with-signalr/_static/image11.png "加入新項目")</span><span class="sxs-lookup"><span data-stu-id="43c3d-201">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    <span data-ttu-id="43c3d-202">*加入新專案*</span><span class="sxs-lookup"><span data-stu-id="43c3d-202">*Add new item*</span></span>
6. <span data-ttu-id="43c3d-203">在 [**加入新專案**] 對話方塊中，選取 **[ C#視覺效果] |Web |** 在左窗格中的 [SignalR] 節點中，從中央窗格中選取 [ **SignalR Hub Class （v2）** ]，將檔案命名為**StatisticsHub.cs** ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-203">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="43c3d-204">![[加入新專案] 對話方塊](real-time-web-applications-with-signalr/_static/image12.png "[加入新專案] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="43c3d-204">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    <span data-ttu-id="43c3d-205">*[加入新專案] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="43c3d-205">*Add new item dialog box*</span></span>
7. <span data-ttu-id="43c3d-206">將**StatisticsHub**類別中的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="43c3d-206">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="43c3d-207">（程式碼片段- *RealTimeSignalR-Ex1-StatisticsHubClass*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-207">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="43c3d-208">開啟**Startup.cs** ，**並在設定方法的**結尾新增下列程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="43c3d-208">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="43c3d-209">（程式碼片段- *RealTimeSignalR-Ex1-MapSignalR*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-209">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="43c3d-210">開啟 [**服務**] 資料夾內的 [ **StatisticsService.cs** ] 頁面，並新增下列 using 指示詞。</span><span class="sxs-lookup"><span data-stu-id="43c3d-210">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="43c3d-211">（程式碼片段- *RealTimeSignalR-Ex1-UsingDirectives*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-211">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="43c3d-212">若要通知已連線用戶端的更新，您必須先抓取目前連接的**內容**物件。</span><span class="sxs-lookup"><span data-stu-id="43c3d-212">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="43c3d-213">**Hub**物件包含將訊息傳送至單一用戶端或廣播至所有已連線用戶端的方法。</span><span class="sxs-lookup"><span data-stu-id="43c3d-213">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="43c3d-214">將下列方法新增至**StatisticsService**類別，以廣播統計資料。</span><span class="sxs-lookup"><span data-stu-id="43c3d-214">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="43c3d-215">（程式碼片段- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-215">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="43c3d-216">在上述程式碼中，您會使用任意方法名稱來呼叫用戶端上的函式（亦即： *updateStatistics*）。</span><span class="sxs-lookup"><span data-stu-id="43c3d-216">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="43c3d-217">您指定的方法名稱會被視為動態物件，這表示沒有任何 IntelliSense 或編譯時間驗證。</span><span class="sxs-lookup"><span data-stu-id="43c3d-217">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="43c3d-218">運算式會在執行時間進行評估。</span><span class="sxs-lookup"><span data-stu-id="43c3d-218">The expression is evaluated at run time.</span></span> <span data-ttu-id="43c3d-219">當方法呼叫執行時，SignalR 會將方法名稱和參數值傳送給用戶端。</span><span class="sxs-lookup"><span data-stu-id="43c3d-219">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="43c3d-220">如果用戶端具有符合名稱的方法，則會呼叫該方法，並將參數值傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="43c3d-220">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="43c3d-221">如果在用戶端上找不到相符的方法，則不會引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="43c3d-221">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="43c3d-222">如需詳細資訊，請參閱[ASP.NET SignalR HUB API Guide](../guide-to-the-api/hubs-api-guide-server.md)。</span><span class="sxs-lookup"><span data-stu-id="43c3d-222">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="43c3d-223">開啟 [**控制器**] 資料夾內的 [ **TriviaController.cs** ] 頁面，並新增下列 using 指示詞。</span><span class="sxs-lookup"><span data-stu-id="43c3d-223">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="43c3d-224">將下列反白顯示的程式碼新增至**Post**動作方法。</span><span class="sxs-lookup"><span data-stu-id="43c3d-224">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="43c3d-225">（程式碼片段- *RealTimeSignalR-Ex1-NotifyUpdatesCall*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-225">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="43c3d-226">開啟 Views 內的**Statistics. cshtml**頁面 **|主**資料夾。</span><span class="sxs-lookup"><span data-stu-id="43c3d-226">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="43c3d-227">找出 [**腳本**] 區段，並在區段的開頭新增下列腳本參考。</span><span class="sxs-lookup"><span data-stu-id="43c3d-227">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="43c3d-228">（程式碼片段- *RealTimeSignalR-Ex1-SignalRScriptReferences*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-228">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="43c3d-229">當您將 SignalR 和其他腳本程式庫新增至 Visual Studio 專案時，套件管理員可能會安裝比本主題中所示版本還新的 SignalR 腳本檔案版本。</span><span class="sxs-lookup"><span data-stu-id="43c3d-229">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="43c3d-230">請確定程式碼中的腳本參考符合您的專案中所安裝的腳本程式庫版本。</span><span class="sxs-lookup"><span data-stu-id="43c3d-230">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="43c3d-231">新增下列反白顯示的程式碼，將用戶端連接到 SignalR 中樞，並在從中樞收到新訊息時，更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="43c3d-231">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="43c3d-232">（程式碼片段- *RealTimeSignalR-Ex1-SignalRClientCode*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-232">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="43c3d-233">在此程式碼中，您會建立中樞 Proxy，並註冊事件處理常式來接聽伺服器所傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-233">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="43c3d-234">在此情況下，您會接聽透過*updateStatistics*方法傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-234">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="43c3d-235">工作3–執行解決方案</span><span class="sxs-lookup"><span data-stu-id="43c3d-235">Task 3 – Running the Solution</span></span>

<span data-ttu-id="43c3d-236">在這項工作中，您將執行解決方案，以確認在回答新問題之後，會使用 SignalR 自動更新統計資料檢視。</span><span class="sxs-lookup"><span data-stu-id="43c3d-236">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="43c3d-237">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-237">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43c3d-238">如果尚未登入應用程式，請使用您在工作1中建立的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="43c3d-238">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="43c3d-239">在新視窗中開啟 [**統計資料]** 頁面，並將 [**首頁**] 和 [**統計資料]** 頁面並排放在工作1中。</span><span class="sxs-lookup"><span data-stu-id="43c3d-239">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="43c3d-240">在首頁**中**，按一下其中一個選項來回答問題。</span><span class="sxs-lookup"><span data-stu-id="43c3d-240">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="43c3d-241">![回答另一個問題](real-time-web-applications-with-signalr/_static/image13.png "回答另一個問題")</span><span class="sxs-lookup"><span data-stu-id="43c3d-241">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    <span data-ttu-id="43c3d-242">*回答另一個問題*</span><span class="sxs-lookup"><span data-stu-id="43c3d-242">*Answering another question*</span></span>
4. <span data-ttu-id="43c3d-243">按一下其中一個按鈕之後，應該會出現答案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-243">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="43c3d-244">請注意，在使用更新的資訊回答問題之後，會自動更新頁面上的統計資料資訊，而不需要重新整理整個頁面。</span><span class="sxs-lookup"><span data-stu-id="43c3d-244">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="43c3d-245">![在解答之後重新整理統計資料頁面](real-time-web-applications-with-signalr/_static/image14.png "在解答之後重新整理統計資料頁面")</span><span class="sxs-lookup"><span data-stu-id="43c3d-245">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    <span data-ttu-id="43c3d-246">*在解答之後重新整理統計資料頁面*</span><span class="sxs-lookup"><span data-stu-id="43c3d-246">*Statistics page refreshed after answer*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="43c3d-247">練習2：使用 SQL Server 相應放大</span><span class="sxs-lookup"><span data-stu-id="43c3d-247">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="43c3d-248">調整 web 應用程式時，您通常可以在相應*增加*和*相應*放大選項之間選擇。</span><span class="sxs-lookup"><span data-stu-id="43c3d-248">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="43c3d-249">相應*增加*表示使用較大的伺服器，包含更多資源（CPU、RAM 等等），而*相應*放大則表示新增更多伺服器來處理負載。</span><span class="sxs-lookup"><span data-stu-id="43c3d-249">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="43c3d-250">後者的問題是，用戶端可以路由傳送至不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="43c3d-250">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="43c3d-251">連接到一部伺服器的用戶端不會接收從另一部伺服器傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-251">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="43c3d-252">您可以使用稱為*背板*的元件來解決這些問題，以便在伺服器之間轉送訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-252">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="43c3d-253">啟用背板後，每個應用程式實例會將訊息傳送至後擋板，而背板會將它們轉送至其他應用程式實例。</span><span class="sxs-lookup"><span data-stu-id="43c3d-253">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="43c3d-254">目前有三種類型的背板可用於 SignalR：</span><span class="sxs-lookup"><span data-stu-id="43c3d-254">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="43c3d-255">**Windows Azure 服務匯流排**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-255">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="43c3d-256">服務匯流排是一種訊息基礎結構，可讓元件傳送鬆散耦合的訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-256">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="43c3d-257">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-257">**SQL Server**.</span></span> <span data-ttu-id="43c3d-258">SQL Server 背板會將訊息寫入至 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="43c3d-258">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="43c3d-259">背板會使用 Service Broker 來提供有效率的訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-259">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="43c3d-260">不過，如果未啟用 Service Broker，它也可以運作。</span><span class="sxs-lookup"><span data-stu-id="43c3d-260">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="43c3d-261">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-261">**Redis**.</span></span> <span data-ttu-id="43c3d-262">Redis 是記憶體中的索引鍵/值存放區。</span><span class="sxs-lookup"><span data-stu-id="43c3d-262">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="43c3d-263">Redis 支援發行/訂閱（"pub/sub"）模式來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-263">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="43c3d-264">每則訊息都會透過訊息匯流排傳送。</span><span class="sxs-lookup"><span data-stu-id="43c3d-264">Every message is sent through a message bus.</span></span> <span data-ttu-id="43c3d-265">訊息匯流排會執行[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)介面，以提供發佈/訂閱抽象概念。</span><span class="sxs-lookup"><span data-stu-id="43c3d-265">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="43c3d-266">背板的工作方式是將預設**IMessageBus**取代為針對該後擋板設計的匯流排。</span><span class="sxs-lookup"><span data-stu-id="43c3d-266">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="43c3d-267">每個伺服器實例都會透過匯流排連接至後擋板。</span><span class="sxs-lookup"><span data-stu-id="43c3d-267">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="43c3d-268">當傳送訊息時，它會移至背板，而背板會將它傳送到每一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="43c3d-268">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="43c3d-269">當伺服器從背板接收訊息時，它會將訊息儲存在其本機快取中。</span><span class="sxs-lookup"><span data-stu-id="43c3d-269">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="43c3d-270">接著，伺服器會從其本機快取將訊息傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="43c3d-270">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="43c3d-271">如需 SignalR 背板運作方式的詳細資訊，請閱讀這[篇文章](../performance/scaleout-in-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="43c3d-271">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="43c3d-272">在某些情況下，背板可能會變成瓶頸。</span><span class="sxs-lookup"><span data-stu-id="43c3d-272">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="43c3d-273">以下是一些典型的 SignalR 案例：</span><span class="sxs-lookup"><span data-stu-id="43c3d-273">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="43c3d-274">[伺服器廣播](tutorial-server-broadcast-with-signalr.md)（例如股票行情指示器）：背板適用于此案例，因為伺服器會控制傳送訊息的速率。</span><span class="sxs-lookup"><span data-stu-id="43c3d-274">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="43c3d-275">[用戶端對用戶端](tutorial-getting-started-with-signalr.md)（例如聊天）：在此案例中，如果訊息數目隨著用戶端數目調整，則背板可能是瓶頸;也就是說，如果訊息的速率會隨著更多用戶端聯結而按比例成長。</span><span class="sxs-lookup"><span data-stu-id="43c3d-275">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="43c3d-276">[高頻率即時](tutorial-high-frequency-realtime-with-signalr.md)（例如即時遊戲）：在此案例中不建議使用背板。</span><span class="sxs-lookup"><span data-stu-id="43c3d-276">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

<span data-ttu-id="43c3d-277">在此練習中，您將使用**SQL Server**在**萬能技客測驗**應用程式中散發訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-277">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="43c3d-278">您將會在單一測試電腦上執行這些工作，以瞭解如何設定設定，但為了獲得完整的效果，您必須將 SignalR 應用程式部署到兩部以上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="43c3d-278">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="43c3d-279">您也必須在其中一部伺服器上，或在個別的專用伺服器上安裝 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="43c3d-279">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![使用 SQL Server 圖表 Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="43c3d-281">工作 1-瞭解案例</span><span class="sxs-lookup"><span data-stu-id="43c3d-281">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="43c3d-282">在這項工作中，您將執行2個**萬能技客測驗**實例，在本機電腦上模擬多個 IIS 實例。</span><span class="sxs-lookup"><span data-stu-id="43c3d-282">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="43c3d-283">在此案例中，當您在某一個應用程式上回答邏輯問題時，不會在第二個實例的 [統計資料] 頁面上通知更新。</span><span class="sxs-lookup"><span data-stu-id="43c3d-283">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="43c3d-284">此模擬類似于將您的應用程式部署在多個實例上，並使用負載平衡器與其通訊的環境。</span><span class="sxs-lookup"><span data-stu-id="43c3d-284">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="43c3d-285">開啟位於 [**來源/Ex2-ScalingOutWithSQLServer/開始**] 資料夾中的 [**開始 .sln** ] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-285">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="43c3d-286">載入之後，您會注意到**伺服器總管**解決方案有兩個專案具有相同的結構，但名稱不同。</span><span class="sxs-lookup"><span data-stu-id="43c3d-286">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="43c3d-287">這會在您的本機電腦上模擬相同應用程式的兩個實例。</span><span class="sxs-lookup"><span data-stu-id="43c3d-287">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="43c3d-288">![開始模擬2個萬能技客測驗實例的解決方案](real-time-web-applications-with-signalr/_static/image16.png "開始模擬2個萬能技客測驗實例的解決方案")</span><span class="sxs-lookup"><span data-stu-id="43c3d-288">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    <span data-ttu-id="43c3d-289">*開始模擬2個萬能技客測驗實例的解決方案*</span><span class="sxs-lookup"><span data-stu-id="43c3d-289">*Begin Solution Simulating 2 Instances of Geek Quiz*</span></span>
2. <span data-ttu-id="43c3d-290">以滑鼠右鍵按一下方案節點，然後選取 [**屬性**]，以開啟方案的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="43c3d-290">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="43c3d-291">在 [**啟始專案**] 底下，選取 [**多個啟始專案**]，並將兩個專案的**動作**值變更為 [*啟動*]</span><span class="sxs-lookup"><span data-stu-id="43c3d-291">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="43c3d-292">![啟動多個專案](real-time-web-applications-with-signalr/_static/image17.png "啟動多個專案")</span><span class="sxs-lookup"><span data-stu-id="43c3d-292">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    <span data-ttu-id="43c3d-293">*啟動多個專案*</span><span class="sxs-lookup"><span data-stu-id="43c3d-293">*Starting Multiple Projects*</span></span>
3. <span data-ttu-id="43c3d-294">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="43c3d-294">Press **F5** to run the solution.</span></span> <span data-ttu-id="43c3d-295">應用程式會在不同的埠中啟動兩個**萬能技客測驗**實例，模擬相同應用程式的多個實例。</span><span class="sxs-lookup"><span data-stu-id="43c3d-295">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="43c3d-296">將左側的其中一個瀏覽器釘選到螢幕右側的另一個。</span><span class="sxs-lookup"><span data-stu-id="43c3d-296">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="43c3d-297">使用您的認證登入，或註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="43c3d-297">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="43c3d-298">登入之後，請將 [邏輯] 頁面保持在左側，並移至右側瀏覽器中的 [**統計資料]** 頁面。</span><span class="sxs-lookup"><span data-stu-id="43c3d-298">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![並排萬能技客測驗](real-time-web-applications-with-signalr/_static/image18.png)

    <span data-ttu-id="43c3d-300">*並排萬能技客測驗*</span><span class="sxs-lookup"><span data-stu-id="43c3d-300">*Geek Quiz Side by Side*</span></span>

    ![不同埠中的萬能技客測驗](real-time-web-applications-with-signalr/_static/image19.png)

    <span data-ttu-id="43c3d-302">*不同埠中的萬能技客測驗*</span><span class="sxs-lookup"><span data-stu-id="43c3d-302">*Geek Quiz in Different Ports*</span></span>
4. <span data-ttu-id="43c3d-303">在左側瀏覽器中開始回答問題，您會注意到右側瀏覽器中的 [**統計資料]** 頁面並未更新。</span><span class="sxs-lookup"><span data-stu-id="43c3d-303">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="43c3d-304">這是因為**SignalR**會使用本機快取，將訊息散發到其用戶端，而此案例會模擬多個實例，因此不會在兩者之間共用快取。</span><span class="sxs-lookup"><span data-stu-id="43c3d-304">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="43c3d-305">您可以藉由測試相同的步驟，但使用單一應用程式，來確認**SignalR**是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="43c3d-305">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="43c3d-306">在下列工作中，您將設定背板來複寫各個實例的訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-306">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="43c3d-307">返回 Visual Studio 並停止調試。</span><span class="sxs-lookup"><span data-stu-id="43c3d-307">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="43c3d-308">工作2–建立 SQL Server 背板</span><span class="sxs-lookup"><span data-stu-id="43c3d-308">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="43c3d-309">在這項工作中，您將建立一個將作為**萬能技客測驗**應用程式後擋板的資料庫。</span><span class="sxs-lookup"><span data-stu-id="43c3d-309">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="43c3d-310">您將使用**SQL Server 物件總管**來流覽伺服器並初始化資料庫。</span><span class="sxs-lookup"><span data-stu-id="43c3d-310">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="43c3d-311">此外，您將會啟用**Service Broker**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-311">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="43c3d-312">在**Visual Studio**中，開啟功能表**視圖**並選取 [ **SQL Server 物件總管**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-312">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="43c3d-313">以滑鼠右鍵按一下 [ **SQL Server** ] 節點，然後選取 [**新增 SQL Server** ] 選項，以連接到您的 LocalDB 實例。</span><span class="sxs-lookup"><span data-stu-id="43c3d-313">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="43c3d-314">![加入 SQL Server 實例](real-time-web-applications-with-signalr/_static/image20.png "加入 SQL Server 實例")</span><span class="sxs-lookup"><span data-stu-id="43c3d-314">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="43c3d-315">*將 SQL Server 實例新增至 SQL Server 物件總管*</span><span class="sxs-lookup"><span data-stu-id="43c3d-315">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
3. <span data-ttu-id="43c3d-316">將 [**伺服器名稱**] 設定為 *（localdb） \v11.0* ，並將 [ **Windows 驗證**] 保留為您的驗證模式。</span><span class="sxs-lookup"><span data-stu-id="43c3d-316">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="43c3d-317">按一下 [連接] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="43c3d-317">Click **Connect** to continue.</span></span>

    <span data-ttu-id="43c3d-318">![連接到 LocalDB](real-time-web-applications-with-signalr/_static/image21.png "連接到 LocalDB")</span><span class="sxs-lookup"><span data-stu-id="43c3d-318">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="43c3d-319">*連接到 LocalDB*</span><span class="sxs-lookup"><span data-stu-id="43c3d-319">*Connecting to LocalDB*</span></span>
4. <span data-ttu-id="43c3d-320">既然您已連接到 LocalDB 實例，您將需要建立一個資料庫，以代表 SignalR 的 SQL Server 背板。</span><span class="sxs-lookup"><span data-stu-id="43c3d-320">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="43c3d-321">若要這樣做，請以滑鼠右鍵按一下 [**資料庫**] 節點，然後選取 [**加入新的資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-321">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="43c3d-322">![加入新的資料庫](real-time-web-applications-with-signalr/_static/image22.png "加入新的資料庫")</span><span class="sxs-lookup"><span data-stu-id="43c3d-322">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    <span data-ttu-id="43c3d-323">*加入新的資料庫*</span><span class="sxs-lookup"><span data-stu-id="43c3d-323">*Adding a new database*</span></span>
5. <span data-ttu-id="43c3d-324">將資料庫名稱設定為*SignalR* ，然後按一下 **[確定]** 加以建立。</span><span class="sxs-lookup"><span data-stu-id="43c3d-324">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="43c3d-325">![建立 SignalR 資料庫](real-time-web-applications-with-signalr/_static/image23.png "建立 SignalR 資料庫")</span><span class="sxs-lookup"><span data-stu-id="43c3d-325">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    <span data-ttu-id="43c3d-326">*建立 SignalR 資料庫*</span><span class="sxs-lookup"><span data-stu-id="43c3d-326">*Creating the SignalR database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="43c3d-327">您可以為資料庫選擇任何名稱。</span><span class="sxs-lookup"><span data-stu-id="43c3d-327">You can choose any name for the database.</span></span>
6. <span data-ttu-id="43c3d-328">若要從背板更有效率地接收更新，建議您啟用資料庫的 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="43c3d-328">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="43c3d-329">Service Broker 在 SQL Server 中提供訊息和佇列的原生支援。</span><span class="sxs-lookup"><span data-stu-id="43c3d-329">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="43c3d-330">背板也可以運作，而不 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="43c3d-330">The backplane also works without Service Broker.</span></span> <span data-ttu-id="43c3d-331">以滑鼠右鍵按一下資料庫，然後選取 [追加**查詢**]，以開啟新的查詢。</span><span class="sxs-lookup"><span data-stu-id="43c3d-331">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="43c3d-332">![開啟新的查詢](real-time-web-applications-with-signalr/_static/image24.png "開啟新的查詢")</span><span class="sxs-lookup"><span data-stu-id="43c3d-332">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    <span data-ttu-id="43c3d-333">*開啟新的查詢*</span><span class="sxs-lookup"><span data-stu-id="43c3d-333">*Opening a New Query*</span></span>
7. <span data-ttu-id="43c3d-334">若要檢查是否已啟用 Service Broker，請查詢**sys.databases**目錄檢視中 **\_Broker\_enabled**資料行。</span><span class="sxs-lookup"><span data-stu-id="43c3d-334">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="43c3d-335">在最近開啟的查詢視窗中執行下列腳本。</span><span class="sxs-lookup"><span data-stu-id="43c3d-335">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="43c3d-336">![查詢 Service Broker 狀態](real-time-web-applications-with-signalr/_static/image25.png "查詢 Service Broker 狀態")</span><span class="sxs-lookup"><span data-stu-id="43c3d-336">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    <span data-ttu-id="43c3d-337">*查詢 Service Broker 狀態*</span><span class="sxs-lookup"><span data-stu-id="43c3d-337">*Querying the Service Broker Status*</span></span>
8. <span data-ttu-id="43c3d-338">如果您資料庫中 **\_broker\_已啟用**資料行的值為 &quot;0&quot;，請使用下列命令來啟用它。</span><span class="sxs-lookup"><span data-stu-id="43c3d-338">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="43c3d-339">使用您在建立資料庫時所設定的名稱（例如： SignalR），取代**您的資料庫&gt;&lt;** 。</span><span class="sxs-lookup"><span data-stu-id="43c3d-339">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="43c3d-340">![啟用 Service Broker](real-time-web-applications-with-signalr/_static/image26.png "啟用 Service Broker")</span><span class="sxs-lookup"><span data-stu-id="43c3d-340">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    <span data-ttu-id="43c3d-341">*啟用 Service Broker*</span><span class="sxs-lookup"><span data-stu-id="43c3d-341">*Enabling Service Broker*</span></span>

    > [!NOTE]
    > <span data-ttu-id="43c3d-342">如果此查詢出現鎖死，請確定沒有任何應用程式連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="43c3d-342">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="43c3d-343">工作 3-設定 SignalR 應用程式</span><span class="sxs-lookup"><span data-stu-id="43c3d-343">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="43c3d-344">在這項工作中，您將設定**萬能技客測驗**以連接到 SQL Server 背板。</span><span class="sxs-lookup"><span data-stu-id="43c3d-344">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="43c3d-345">您會先新增**SignalR** NuGet 套件，並將連接字串設定為您的背板資料庫。</span><span class="sxs-lookup"><span data-stu-id="43c3d-345">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="43c3d-346">從 [**工具**] > [ **NuGet 套件管理員**] 開啟 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-346">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="43c3d-347">請確定已在 [**預設專案**] 下拉式清單中選取 [ **GeekQuiz**專案]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-347">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="43c3d-348">輸入下列命令以安裝**SignalR** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="43c3d-348">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="43c3d-349">重複上一個步驟，但這次是針對 [專案**GeekQuiz2**]。</span><span class="sxs-lookup"><span data-stu-id="43c3d-349">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="43c3d-350">若要設定 SQL Server 背板，請開啟**GeekQuiz**專案的**Startup.cs**檔案，並將下列程式碼新增至**configure**方法。</span><span class="sxs-lookup"><span data-stu-id="43c3d-350">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="43c3d-351">以您在建立 SQL Server 後擋板時所使用的資料庫名稱取代**您的資料庫&gt;&lt;** 。</span><span class="sxs-lookup"><span data-stu-id="43c3d-351">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="43c3d-352">針對**GeekQuiz2**專案重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="43c3d-352">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="43c3d-353">（程式碼片段- *RealTimeSignalR-Ex2-StartupConfiguration*）</span><span class="sxs-lookup"><span data-stu-id="43c3d-353">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="43c3d-354">現在這兩個專案都設定為使用 SQL Server 背板，請按**F5**同時執行它們。</span><span class="sxs-lookup"><span data-stu-id="43c3d-354">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="43c3d-355">同樣地， **Visual Studio**會在不同的埠中啟動兩個**萬能技客測驗**實例。</span><span class="sxs-lookup"><span data-stu-id="43c3d-355">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="43c3d-356">將左側的其中一個瀏覽器釘選在畫面右側，然後使用您的認證登入。</span><span class="sxs-lookup"><span data-stu-id="43c3d-356">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="43c3d-357">保持左側的 [邏輯] 頁面，並移至 [**統計資料]** pagein 正確的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="43c3d-357">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="43c3d-358">在左側瀏覽器中開始回答問題。</span><span class="sxs-lookup"><span data-stu-id="43c3d-358">Start answering questions in the left browser.</span></span> <span data-ttu-id="43c3d-359">這次，**統計資料**頁面會因為背板而更新。</span><span class="sxs-lookup"><span data-stu-id="43c3d-359">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="43c3d-360">在應用程式之間切換（**統計資料**現在位於左側，而**邏輯**位於右邊）並重複測試，以驗證這兩個實例都能正常運作。</span><span class="sxs-lookup"><span data-stu-id="43c3d-360">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="43c3d-361">背板會作為每個連線伺服器的*共用*訊息快取，而每部伺服器會將訊息儲存在自己的本機快取中，以散發給已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="43c3d-361">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="43c3d-362">返回 Visual Studio 並停止調試。</span><span class="sxs-lookup"><span data-stu-id="43c3d-362">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="43c3d-363">SQL Server 的背板元件會在指定的資料庫上自動產生必要的資料表。</span><span class="sxs-lookup"><span data-stu-id="43c3d-363">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="43c3d-364">在 [ **SQL Server 物件總管**] 面板中，開啟您為背板建立的資料庫（例如： SignalR），並展開其資料表。</span><span class="sxs-lookup"><span data-stu-id="43c3d-364">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="43c3d-365">您應該會看到下列資料表：</span><span class="sxs-lookup"><span data-stu-id="43c3d-365">You should see the following tables:</span></span>

    ![背板產生的資料表](real-time-web-applications-with-signalr/_static/image27.png)

    <span data-ttu-id="43c3d-367">*背板產生的資料表*</span><span class="sxs-lookup"><span data-stu-id="43c3d-367">*Backplane Generated Tables*</span></span>
9. <span data-ttu-id="43c3d-368">以滑鼠右鍵按一下  **SignalR\_0**  資料表，然後選取 **查看資料**。</span><span class="sxs-lookup"><span data-stu-id="43c3d-368">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![View SignalR 背板訊息資料表](real-time-web-applications-with-signalr/_static/image28.png)

    <span data-ttu-id="43c3d-370">*View SignalR 背板訊息資料表*</span><span class="sxs-lookup"><span data-stu-id="43c3d-370">*View SignalR Backplane Messages Table*</span></span>
10. <span data-ttu-id="43c3d-371">回答邏輯問題時，您可以看到傳送至**中樞**的不同訊息。</span><span class="sxs-lookup"><span data-stu-id="43c3d-371">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="43c3d-372">背板會將這些訊息散發到任何已連接的實例。</span><span class="sxs-lookup"><span data-stu-id="43c3d-372">The backplane distributes these messages to any connected instance.</span></span>

    ![背板訊息資料表](real-time-web-applications-with-signalr/_static/image29.png)

    <span data-ttu-id="43c3d-374">*背板訊息資料表*</span><span class="sxs-lookup"><span data-stu-id="43c3d-374">*Backplane Messages Table*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="43c3d-375">總結</span><span class="sxs-lookup"><span data-stu-id="43c3d-375">Summary</span></span>

<span data-ttu-id="43c3d-376">在此實際操作實驗室中，您已瞭解如何將**SignalR**新增至您的應用程式，並使用**中樞**將通知從伺服器傳送到已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="43c3d-376">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="43c3d-377">此外，當您的應用程式部署在多個 IIS 實例時，您已瞭解如何使用*背板*元件來相應放大應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c3d-377">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>
