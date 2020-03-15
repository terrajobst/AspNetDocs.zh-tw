---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 使用 ASP.NET Web API ASP.NET 4.x 建立 RESTful Api
author: rick-anderson
description: 實習實驗室：使用 ASP.NET 4.x 中的 Web API，為連絡人管理員應用程式建立簡單的 REST API。
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621811"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="9cf35-103">使用 ASP.NET Web API 建立 RESTful Api</span><span class="sxs-lookup"><span data-stu-id="9cf35-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="9cf35-104">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="9cf35-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="9cf35-105">實習實驗室：使用 ASP.NET 4.x 中的 Web API，為連絡人管理員應用程式建立簡單的 REST API。</span><span class="sxs-lookup"><span data-stu-id="9cf35-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="9cf35-106">您也會建立取用 API 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9cf35-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="9cf35-107">最近幾年來，它已經很清楚，HTTP 不只是用來提供 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="9cf35-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="9cf35-108">它也是一個強大的平臺，可用於建立 Web Api、使用幾個動詞（GET、POST 等等），再加上一些簡單的概念，例如*uri*和*標頭*。</span><span class="sxs-lookup"><span data-stu-id="9cf35-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="9cf35-109">ASP.NET Web API 是一組可簡化 HTTP 程式設計的元件。</span><span class="sxs-lookup"><span data-stu-id="9cf35-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="9cf35-110">因為它是以 ASP.NET MVC 執行時間為基礎，所以 Web API 會自動處理 HTTP 的低層級傳輸詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9cf35-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="9cf35-111">同時，Web API 會自然地公開 HTTP 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="9cf35-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="9cf35-112">事實上，Web API 的其中一個目標就是*不要*抽象掉 HTTP 的現實。</span><span class="sxs-lookup"><span data-stu-id="9cf35-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="9cf35-113">因此，Web API 既彈性又容易擴充。</span><span class="sxs-lookup"><span data-stu-id="9cf35-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="9cf35-114">REST 架構樣式已證明是利用 HTTP 的有效方法，雖然它肯定不是 HTTP 的唯一有效方法。</span><span class="sxs-lookup"><span data-stu-id="9cf35-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="9cf35-115">連絡人管理員將會公開用來列出、新增和移除連絡人的 RESTful，以及其他人。</span><span class="sxs-lookup"><span data-stu-id="9cf35-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="9cf35-116">此實驗室需要對 HTTP、REST 的基本瞭解，並假設您具備 HTML、JavaScript 和 jQuery 的基本知識。</span><span class="sxs-lookup"><span data-stu-id="9cf35-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="9cf35-117">ASP.NET 網站有一個專門用於 ASP.NET Web API 架構[https://asp.net/web-api](https://asp.net/web-api)的區域。</span><span class="sxs-lookup"><span data-stu-id="9cf35-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="9cf35-118">此網站將繼續提供與 Web API 相關的最新資訊、範例和新聞，因此如果您想要深入瞭解建立可用於幾乎任何裝置或開發架構的自訂 Web Api，請經常檢查。</span><span class="sxs-lookup"><span data-stu-id="9cf35-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="9cf35-119">ASP.NET Web API （類似于 ASP.NET MVC 4）在分隔服務層與控制器之間有很大的彈性，可讓您輕鬆地使用數個可用的相依性插入架構。</span><span class="sxs-lookup"><span data-stu-id="9cf35-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="9cf35-120">MSDN 中有一個很好的範例，示範如何在 ASP.NET Web API 專案中使用相依性插入的 Ninject，您可以從[這裡](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)下載。</span><span class="sxs-lookup"><span data-stu-id="9cf35-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="9cf35-121">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)取得。</span><span class="sxs-lookup"><span data-stu-id="9cf35-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="9cf35-122">目標</span><span class="sxs-lookup"><span data-stu-id="9cf35-122">Objectives</span></span>

<span data-ttu-id="9cf35-123">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="9cf35-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="9cf35-124">執行 RESTful Web API</span><span class="sxs-lookup"><span data-stu-id="9cf35-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="9cf35-125">從 HTML 用戶端呼叫 API</span><span class="sxs-lookup"><span data-stu-id="9cf35-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="9cf35-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9cf35-126">Prerequisites</span></span>

<span data-ttu-id="9cf35-127">若要完成此實際操作實驗室，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="9cf35-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="9cf35-128">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需如何安裝的指示，請參閱[附錄 B](#AppendixB) ）。</span><span class="sxs-lookup"><span data-stu-id="9cf35-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="9cf35-129">安裝程式</span><span class="sxs-lookup"><span data-stu-id="9cf35-129">Setup</span></span>

<span data-ttu-id="9cf35-130">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="9cf35-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="9cf35-131">為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。</span><span class="sxs-lookup"><span data-stu-id="9cf35-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="9cf35-132">若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="9cf35-133">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 A：使用程式碼片段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="9cf35-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="9cf35-134">練習</span><span class="sxs-lookup"><span data-stu-id="9cf35-134">Exercises</span></span>

<span data-ttu-id="9cf35-135">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="9cf35-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="9cf35-136">練習1：建立唯讀的 Web API</span><span class="sxs-lookup"><span data-stu-id="9cf35-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="9cf35-137">練習2：建立讀取/寫入 Web API</span><span class="sxs-lookup"><span data-stu-id="9cf35-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="9cf35-138">練習3：使用 HTML 用戶端的 Web API</span><span class="sxs-lookup"><span data-stu-id="9cf35-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="9cf35-139">每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="9cf35-140">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="9cf35-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="9cf35-141">完成此實驗室的預估時間： **60 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="9cf35-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="9cf35-142">練習1：建立唯讀的 Web API</span><span class="sxs-lookup"><span data-stu-id="9cf35-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="9cf35-143">在此練習中，您將為 contact manager 執行唯讀的 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="9cf35-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="9cf35-144">工作 1-建立 API 專案</span><span class="sxs-lookup"><span data-stu-id="9cf35-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="9cf35-145">在這項工作中，您將使用新的 ASP.NET Web 專案範本來建立 Web API web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cf35-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="9cf35-146">執行**Visual Studio 2012 Express For Web**，若要執行此動作，請移至 [**開始**] 並輸入**VS Express for Web**然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9cf35-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="9cf35-147">從 [**檔案**] 功能表中，選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="9cf35-148">選取**視覺效果C# |Web**專案類型從 [專案類型] 樹狀檢視中選取 [ **ASP.NET MVC 4 Web 應用程式**] 專案類型。</span><span class="sxs-lookup"><span data-stu-id="9cf35-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="9cf35-149">將專案的**名稱**設為*ContactManager* ，並將**方案名稱**設定為 [*開始*]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="9cf35-150">![建立新的 ASP.NET MVC 4.0 Web 應用程式專案](build-restful-apis-with-aspnet-web-api/_static/image1.png "建立新的 ASP.NET MVC 4.0 Web 應用程式專案")</span><span class="sxs-lookup"><span data-stu-id="9cf35-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="9cf35-151">*建立新的 ASP.NET MVC 4.0 Web 應用程式專案*</span><span class="sxs-lookup"><span data-stu-id="9cf35-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="9cf35-152">在 [ASP.NET MVC 4 專案類型] 對話方塊中，選取 [ **WEB API** ] 專案類型。</span><span class="sxs-lookup"><span data-stu-id="9cf35-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="9cf35-153">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-153">Click **OK**.</span></span>

    <span data-ttu-id="9cf35-154">![指定 Web API 專案類型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 專案類型")</span><span class="sxs-lookup"><span data-stu-id="9cf35-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="9cf35-155">*指定 Web API 專案類型*</span><span class="sxs-lookup"><span data-stu-id="9cf35-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="9cf35-156">工作 2-建立連絡人管理員 API 控制器</span><span class="sxs-lookup"><span data-stu-id="9cf35-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="9cf35-157">在這項工作中，您將會建立 API 方法所在的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="9cf35-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="9cf35-158">從專案刪除 [**控制器**] 資料夾中名為**ValuesController.cs**的檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="9cf35-159">以滑鼠右鍵按一下專案中的 [**控制器**] 資料夾，然後選取 [**新增] |** 內容功能表中的 [控制器]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="9cf35-160">![將新的控制器新增至專案](build-restful-apis-with-aspnet-web-api/_static/image3.png "將新的控制器新增至專案")</span><span class="sxs-lookup"><span data-stu-id="9cf35-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="9cf35-161">*將新的控制器新增至專案*</span><span class="sxs-lookup"><span data-stu-id="9cf35-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="9cf35-162">在出現的 [**新增控制器**] 對話方塊中，從 [範本] 功能表選取 [**空的 API 控制器**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="9cf35-163">將控制器類別命名為**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="9cf35-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="9cf35-164">然後，按一下 [**新增]。**</span><span class="sxs-lookup"><span data-stu-id="9cf35-164">Then, click **Add.**</span></span>

    <span data-ttu-id="9cf35-165">![使用 [新增控制器] 對話方塊來建立新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用 [新增控制器] 對話方塊來建立新的 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="9cf35-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="9cf35-166">*使用 [新增控制器] 對話方塊來建立新的 Web API 控制器*</span><span class="sxs-lookup"><span data-stu-id="9cf35-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="9cf35-167">將下列程式碼加入至**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="9cf35-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="9cf35-168">（程式碼片段- *WEB API 實驗室-Ex01-取得 API 方法*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="9cf35-169">按 **F5** 鍵來進行應用程式偵錯。</span><span class="sxs-lookup"><span data-stu-id="9cf35-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="9cf35-170">應會出現 Web API 專案的預設首頁。</span><span class="sxs-lookup"><span data-stu-id="9cf35-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="9cf35-171">![ASP.NET Web API 應用程式的預設首頁](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 應用程式的預設首頁")</span><span class="sxs-lookup"><span data-stu-id="9cf35-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="9cf35-172">*ASP.NET Web API 應用程式的預設首頁*</span><span class="sxs-lookup"><span data-stu-id="9cf35-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="9cf35-173">在 Internet Explorer 視窗中，按**F12**鍵以開啟 [**開發人員工具**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9cf35-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="9cf35-174">按一下 [**網路**] 索引標籤，然後按一下 [**開始捕捉**] 按鈕，開始將網路流量捕獲到視窗中。</span><span class="sxs-lookup"><span data-stu-id="9cf35-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="9cf35-175">![開啟 [網路] 索引標籤並起始網路捕獲](build-restful-apis-with-aspnet-web-api/_static/image6.png "開啟 [網路] 索引標籤並起始網路捕獲")</span><span class="sxs-lookup"><span data-stu-id="9cf35-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="9cf35-176">*開啟 [網路] 索引標籤並起始網路捕獲*</span><span class="sxs-lookup"><span data-stu-id="9cf35-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="9cf35-177">使用 **/api/contact**在瀏覽器的網址列中附加 URL，然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="9cf35-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="9cf35-178">傳輸詳細資料會出現在 [網路捕捉] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="9cf35-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="9cf35-179">請注意，回應的 MIME 類型為**application/json**。</span><span class="sxs-lookup"><span data-stu-id="9cf35-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="9cf35-180">這會示範預設輸出格式為 JSON 的方式。</span><span class="sxs-lookup"><span data-stu-id="9cf35-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="9cf35-181">![在網路視圖中查看 Web API 要求的輸出](build-restful-apis-with-aspnet-web-api/_static/image7.png "在網路視圖中查看 Web API 要求的輸出")</span><span class="sxs-lookup"><span data-stu-id="9cf35-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="9cf35-182">*在網路視圖中查看 Web API 要求的輸出*</span><span class="sxs-lookup"><span data-stu-id="9cf35-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cf35-183">此時，Internet Explorer 10 的預設行為會詢問使用者是否想要儲存或開啟 Web API 呼叫所產生的資料流程。</span><span class="sxs-lookup"><span data-stu-id="9cf35-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="9cf35-184">輸出將會是一個文字檔，其中包含 Web API URL 呼叫的 JSON 結果。</span><span class="sxs-lookup"><span data-stu-id="9cf35-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="9cf35-185">請勿取消對話方塊，以便透過 [開發人員] 工具視窗觀看回應的內容。</span><span class="sxs-lookup"><span data-stu-id="9cf35-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="9cf35-186">按一下 [**移至詳細的視圖**] 按鈕，以查看更多關於此 API 呼叫回應的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9cf35-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="9cf35-187">![切換至詳細的視圖](build-restful-apis-with-aspnet-web-api/_static/image8.png "切換至詳細資料檢視")</span><span class="sxs-lookup"><span data-stu-id="9cf35-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="9cf35-188">*切換至詳細的視圖*</span><span class="sxs-lookup"><span data-stu-id="9cf35-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="9cf35-189">按一下 [**回應主體**] 索引標籤，以查看實際的 JSON 回應文字。</span><span class="sxs-lookup"><span data-stu-id="9cf35-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="9cf35-190">![在網路監視器中查看 JSON 輸出文字](build-restful-apis-with-aspnet-web-api/_static/image9.png "在網路監視器中查看 JSON 輸出文字")</span><span class="sxs-lookup"><span data-stu-id="9cf35-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="9cf35-191">*在網路監視器中查看 JSON 輸出文字*</span><span class="sxs-lookup"><span data-stu-id="9cf35-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="9cf35-192">工作 3-建立連絡人模型並擴大連絡人控制器</span><span class="sxs-lookup"><span data-stu-id="9cf35-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="9cf35-193">在這項工作中，您將會建立 API 方法所在的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="9cf35-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="9cf35-194">以滑鼠右鍵按一下 [**模型**] 資料夾，然後選取 [**新增] |類別 ...** 從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="9cf35-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="9cf35-195">![將新模型加入至 web 應用程式](build-restful-apis-with-aspnet-web-api/_static/image10.png "將新模型加入至 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="9cf35-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="9cf35-196">*將新模型加入至 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="9cf35-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="9cf35-197">在 [**加入新專案**] 對話方塊中，將新的檔案命名為**Contact.cs** ，然後按一下 [新增] **。**</span><span class="sxs-lookup"><span data-stu-id="9cf35-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="9cf35-198">![建立新的 Contact 類別檔案](build-restful-apis-with-aspnet-web-api/_static/image11.png "建立新的 Contact 類別檔案")</span><span class="sxs-lookup"><span data-stu-id="9cf35-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="9cf35-199">*建立新的 Contact 類別檔案*</span><span class="sxs-lookup"><span data-stu-id="9cf35-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="9cf35-200">將下列反白顯示的程式碼新增至**Contact**類別。</span><span class="sxs-lookup"><span data-stu-id="9cf35-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="9cf35-201">（程式碼片段- *WEB API 實驗室-Ex01-Contact 類別*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="9cf35-202">在**ContactController**類別中，于**Get**方法的 [方法定義] 中選取 [**字串**]，然後輸入 [ *Contact*] 這個字。</span><span class="sxs-lookup"><span data-stu-id="9cf35-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="9cf35-203">一旦輸入單字，指標就會出現在「**連絡人**」一字的開頭。</span><span class="sxs-lookup"><span data-stu-id="9cf35-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="9cf35-204">按住**Ctrl**鍵，然後按下句點（.）鍵，或按一下圖示來開啟 [程式碼編輯器] 中的 [協助] 對話方塊，以自動填入模型命名空間的**using**指示詞。</span><span class="sxs-lookup"><span data-stu-id="9cf35-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![針對命名空間宣告使用 Intellisense 協助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="9cf35-206">*針對命名空間宣告使用 Intellisense 協助*</span><span class="sxs-lookup"><span data-stu-id="9cf35-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="9cf35-207">修改**Get**方法的程式碼，使其傳回連絡人模型實例的陣列。</span><span class="sxs-lookup"><span data-stu-id="9cf35-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="9cf35-208">（程式碼片段- *WEB API 實驗室-Ex01-傳回連絡人清單*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="9cf35-209">按**F5** ，在瀏覽器中進行 web 應用程式的偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="9cf35-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="9cf35-210">若要查看對 API 回應輸出所做的變更，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="9cf35-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="9cf35-211">當瀏覽器開啟時，如果開發人員工具尚未開啟，請按**F12** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="9cf35-212">按一下 [**網路**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9cf35-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="9cf35-213">按 [**開始捕捉**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cf35-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="9cf35-214">將 URL 尾碼 **/api/contact**新增至網址列中的 url，然後按**enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="9cf35-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="9cf35-215">按 [**移至詳細的視圖**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cf35-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="9cf35-216">選取 [**回應主體**] 索引標籤。您應該會看到 JSON 字串，代表連絡人實例陣列的序列化形式。</span><span class="sxs-lookup"><span data-stu-id="9cf35-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="9cf35-217">![複雜 Web API 方法呼叫的 JSON 序列化輸出](build-restful-apis-with-aspnet-web-api/_static/image13.png "複雜 Web API 方法呼叫的 JSON 序列化輸出")</span><span class="sxs-lookup"><span data-stu-id="9cf35-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="9cf35-218">*複雜 Web API 方法呼叫的 JSON 序列化輸出*</span><span class="sxs-lookup"><span data-stu-id="9cf35-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="9cf35-219">工作 4-將功能解壓縮至服務層</span><span class="sxs-lookup"><span data-stu-id="9cf35-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="9cf35-220">這項工作將示範如何將功能解壓縮至服務層，讓開發人員可以輕鬆地將其服務功能與控制器層隔開，藉此讓實際執行工作的服務得以重複使用。</span><span class="sxs-lookup"><span data-stu-id="9cf35-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="9cf35-221">在方案根目錄中建立新的資料夾，並將其命名為 [it**服務**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="9cf35-222">若要這樣做，請以滑鼠右鍵按一下 [ **ContactManager**專案]，然後選取 [新增] | **新資料夾**，**將**其命名為*服務*</span><span class="sxs-lookup"><span data-stu-id="9cf35-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="9cf35-223">![正在建立服務資料夾](build-restful-apis-with-aspnet-web-api/_static/image14.png "正在建立服務資料夾")</span><span class="sxs-lookup"><span data-stu-id="9cf35-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="9cf35-224">*正在建立服務資料夾*</span><span class="sxs-lookup"><span data-stu-id="9cf35-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="9cf35-225">以滑鼠右鍵按一下 [**服務**] 資料夾，然後選取 [**新增] |類別 ...** 從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="9cf35-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="9cf35-226">![將新類別新增至 [服務] 資料夾](build-restful-apis-with-aspnet-web-api/_static/image15.png "將新類別新增至 [服務] 資料夾")</span><span class="sxs-lookup"><span data-stu-id="9cf35-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="9cf35-227">*將新類別新增至 [服務] 資料夾*</span><span class="sxs-lookup"><span data-stu-id="9cf35-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="9cf35-228">當 [新增**專案**] 對話方塊出現時，將新的類別命名為**contacts.json** ，**然後按一下 [新增]** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="9cf35-229">![建立類別檔案以包含 Contact Repository 服務層的程式碼](build-restful-apis-with-aspnet-web-api/_static/image16.png "建立類別檔案以包含 Contact Repository 服務層的程式碼")</span><span class="sxs-lookup"><span data-stu-id="9cf35-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="9cf35-230">*建立類別檔案以包含 Contact Repository 服務層的程式碼*</span><span class="sxs-lookup"><span data-stu-id="9cf35-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="9cf35-231">將 using 指示詞新增至**ContactRepository.cs**檔案，以包含模型命名空間。</span><span class="sxs-lookup"><span data-stu-id="9cf35-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="9cf35-232">將下列反白顯示的程式碼新增至**ContactRepository.cs**檔案，以執行 GetAllContacts 方法。</span><span class="sxs-lookup"><span data-stu-id="9cf35-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="9cf35-233">（程式碼片段- *WEB API 實驗室-Ex01-連絡人存放庫*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="9cf35-234">如果**ContactController.cs**檔案尚未開啟，請開啟該檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="9cf35-235">將下列 using 語句新增至檔案的命名空間宣告區段。</span><span class="sxs-lookup"><span data-stu-id="9cf35-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="9cf35-236">將下列反白顯示的程式碼新增至**ContactController.cs**類別，以加入私用欄位來代表存放庫的實例，讓其他類別成員可以利用服務執行。</span><span class="sxs-lookup"><span data-stu-id="9cf35-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="9cf35-237">（程式碼片段- *WEB API 實驗室-Ex01-連絡人控制器*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="9cf35-238">變更**Get**方法，使其使用 contact repository 服務。</span><span class="sxs-lookup"><span data-stu-id="9cf35-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="9cf35-239">（程式碼片段- *WEB API 實驗室-Ex01-透過存放庫傳回連絡人清單*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="9cf35-240">將中斷點放在**ContactController**的**Get**方法定義上。</span><span class="sxs-lookup"><span data-stu-id="9cf35-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="9cf35-241">![將中斷點新增至連絡人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "將中斷點新增至連絡人控制器")</span><span class="sxs-lookup"><span data-stu-id="9cf35-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="9cf35-242">*將中斷點新增至連絡人控制器*</span><span class="sxs-lookup"><span data-stu-id="9cf35-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="9cf35-243">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cf35-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="9cf35-244">當瀏覽器開啟時，請按**F12**開啟開發人員工具。</span><span class="sxs-lookup"><span data-stu-id="9cf35-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="9cf35-245">按一下 [**網路**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9cf35-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="9cf35-246">按一下 [**開始捕捉**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cf35-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="9cf35-247">在網址列中使用尾碼 **/api/contact**附加 URL，然後按**enter**載入 api 控制器。</span><span class="sxs-lookup"><span data-stu-id="9cf35-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="9cf35-248">Visual Studio 2012 應該會在**Get**方法開始執行時中斷。</span><span class="sxs-lookup"><span data-stu-id="9cf35-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="9cf35-249">![在 Get 方法內中斷](build-restful-apis-with-aspnet-web-api/_static/image18.png "在 Get 方法內中斷")</span><span class="sxs-lookup"><span data-stu-id="9cf35-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="9cf35-250">*在 Get 方法內中斷*</span><span class="sxs-lookup"><span data-stu-id="9cf35-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="9cf35-251">按 **F5** 繼續。</span><span class="sxs-lookup"><span data-stu-id="9cf35-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="9cf35-252">回到 Internet Explorer （如果尚未處於焦點）。</span><span class="sxs-lookup"><span data-stu-id="9cf35-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="9cf35-253">記下 [網路捕捉] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9cf35-253">Note the network capture window.</span></span>

    <span data-ttu-id="9cf35-254">![Internet Explorer 中顯示 Web API 呼叫結果的網路視圖](build-restful-apis-with-aspnet-web-api/_static/image19.png "Internet Explorer 中顯示 Web API 呼叫結果的網路視圖")</span><span class="sxs-lookup"><span data-stu-id="9cf35-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="9cf35-255">*Internet Explorer 中顯示 Web API 呼叫結果的網路視圖*</span><span class="sxs-lookup"><span data-stu-id="9cf35-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="9cf35-256">按一下 [**移至詳細的視圖**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cf35-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="9cf35-257">按一下 [**回應主體**] 索引標籤。請記下 API 呼叫的 JSON 輸出，以及它如何代表服務層所抓取的兩個連絡人。</span><span class="sxs-lookup"><span data-stu-id="9cf35-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="9cf35-258">![在 [開發人員工具] 視窗中，從 Web API 查看 JSON 輸出](build-restful-apis-with-aspnet-web-api/_static/image20.png "在 [開發人員工具] 視窗中，從 Web API 查看 JSON 輸出")</span><span class="sxs-lookup"><span data-stu-id="9cf35-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="9cf35-259">*在 [開發人員工具] 視窗中，從 Web API 查看 JSON 輸出*</span><span class="sxs-lookup"><span data-stu-id="9cf35-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="9cf35-260">練習2：建立讀取/寫入 Web API</span><span class="sxs-lookup"><span data-stu-id="9cf35-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="9cf35-261">在此練習中，您將會針對連絡人管理員實行 POST 和 PUT 方法，以使用資料編輯功能來加以啟用。</span><span class="sxs-lookup"><span data-stu-id="9cf35-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="9cf35-262">工作 1-開啟 Web API 專案</span><span class="sxs-lookup"><span data-stu-id="9cf35-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="9cf35-263">在這項工作中，您將準備增強在練習1中建立的 Web API 專案，使其可以接受使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="9cf35-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="9cf35-264">執行**Visual Studio 2012 Express For Web**，若要執行此動作，請移至 [**開始**] 並輸入**VS Express for Web**然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9cf35-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="9cf35-265">開啟位於**來源/Ex02-ReadWriteWebAPI/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="9cf35-266">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="9cf35-267">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="9cf35-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="9cf35-268">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="9cf35-269">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="9cf35-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="9cf35-270">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9cf35-271">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="9cf35-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="9cf35-272">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="9cf35-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="9cf35-273">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="9cf35-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="9cf35-274">開啟**Services/contacts.json .cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="9cf35-275">工作 2-將資料持續性功能新增至連絡人存放庫的執行</span><span class="sxs-lookup"><span data-stu-id="9cf35-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="9cf35-276">在這項工作中，您將擴充在練習1中建立之 Web API 專案的 Contacts.json 類別，讓它可以保存並接受使用者輸入和新的連絡人實例。</span><span class="sxs-lookup"><span data-stu-id="9cf35-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="9cf35-277">將下列常數新增至**contacts.json**類別，以代表本練習稍後的 web 伺服器快取專案索引鍵名稱的名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf35-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="9cf35-278">將包含下列程式碼的函式新增至**contacts.json** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="9cf35-279">（程式碼片段- *WEB API 實驗室-Ex02-連絡人存放庫的構造*函式）</span><span class="sxs-lookup"><span data-stu-id="9cf35-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="9cf35-280">修改**GetAllContacts**方法的程式碼，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9cf35-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="9cf35-281">（程式碼片段- *WEB API 實驗室-Ex02-取得所有連絡人*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="9cf35-282">這個範例是為了示範之用，而且會使用 web 伺服器的快取做為儲存媒體，讓多個用戶端都能使用這些值，而不是使用會話儲存機制或要求儲存體存留期。</span><span class="sxs-lookup"><span data-stu-id="9cf35-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="9cf35-283">您可以使用 Entity Framework、XML 儲存體或任何其他各種不同的 web 伺服器快取來取代它。</span><span class="sxs-lookup"><span data-stu-id="9cf35-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="9cf35-284">將名為**SaveContact**的新方法實作為**contacts.json**類別，以執行儲存連絡人的工作。</span><span class="sxs-lookup"><span data-stu-id="9cf35-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="9cf35-285">**SaveContact**方法應該接受單一**連絡人**參數，並傳回表示成功或失敗的布林值。</span><span class="sxs-lookup"><span data-stu-id="9cf35-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="9cf35-286">（程式碼片段- *WEB API 實驗室-Ex02-執行 SaveContact 方法*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="9cf35-287">練習3：使用 HTML 用戶端的 Web API</span><span class="sxs-lookup"><span data-stu-id="9cf35-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="9cf35-288">在此練習中，您將建立 HTML 用戶端來呼叫 Web API。</span><span class="sxs-lookup"><span data-stu-id="9cf35-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="9cf35-289">此用戶端會使用 JavaScript 來加速使用 Web API 交換資料，並使用 HTML 標籤在網頁瀏覽器中顯示結果。</span><span class="sxs-lookup"><span data-stu-id="9cf35-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="9cf35-290">工作 1-修改索引視圖以提供 GUI 來顯示連絡人</span><span class="sxs-lookup"><span data-stu-id="9cf35-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="9cf35-291">在這項工作中，您將修改 web 應用程式的預設 [索引] 視圖，以支援在 HTML 瀏覽器中顯示現有連絡人清單的需求。</span><span class="sxs-lookup"><span data-stu-id="9cf35-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="9cf35-292">開啟 [ **Visual Studio 2012 Express For Web] （** 如果尚未開啟）。</span><span class="sxs-lookup"><span data-stu-id="9cf35-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="9cf35-293">開啟位於**來源/Ex03-ConsumingWebAPI/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="9cf35-294">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="9cf35-295">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="9cf35-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="9cf35-296">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="9cf35-297">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="9cf35-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="9cf35-298">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9cf35-299">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="9cf35-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="9cf35-300">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="9cf35-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="9cf35-301">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="9cf35-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="9cf35-302">開啟位於**Views/Home**資料夾的**Index. cshtml**檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="9cf35-303">將 div 元素內的 HTML 程式碼取代為識別碼**主體**，讓它看起來像下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="9cf35-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="9cf35-304">在檔案底部新增下列 JAVAscript 程式碼，以對 Web API 執行 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="9cf35-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="9cf35-305">如果**ContactController.cs**檔案尚未開啟，請開啟該檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="9cf35-306">將中斷點放在**ContactController**類別的**Get**方法上。</span><span class="sxs-lookup"><span data-stu-id="9cf35-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="9cf35-307">![將中斷點放在 API 控制器的 Get 方法上](build-restful-apis-with-aspnet-web-api/_static/image21.png "將中斷點放在 API 控制器的 Get 方法上")</span><span class="sxs-lookup"><span data-stu-id="9cf35-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="9cf35-308">*將中斷點放在 API 控制器的 Get 方法上*</span><span class="sxs-lookup"><span data-stu-id="9cf35-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="9cf35-309">按 **F5** 執行專案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-309">Press **F5** to run the project.</span></span> <span data-ttu-id="9cf35-310">瀏覽器將會載入 HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cf35-311">請確定您流覽的是應用程式的根 URL。</span><span class="sxs-lookup"><span data-stu-id="9cf35-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="9cf35-312">一旦頁面載入且 JavaScript 執行之後，就會叫用中斷點，而且程式碼執行會在控制器中暫停。</span><span class="sxs-lookup"><span data-stu-id="9cf35-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="9cf35-313">![使用 VS Express for Web 進行 Web API 呼叫的調試](build-restful-apis-with-aspnet-web-api/_static/image22.png "使用 VS Express for Web 進行 Web API 呼叫的調試")</span><span class="sxs-lookup"><span data-stu-id="9cf35-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="9cf35-314">*使用 Visual Studio 2012 Express for Web 進行 Web API 呼叫的偵錯工具*</span><span class="sxs-lookup"><span data-stu-id="9cf35-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="9cf35-315">請移除中斷點，然後按**F5**或偵錯工具工具列的 [**繼續**] 按鈕，繼續在瀏覽器中載入此視圖。</span><span class="sxs-lookup"><span data-stu-id="9cf35-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="9cf35-316">Web API 呼叫完成後，您應該會看到從 Web API 呼叫傳回的連絡人，在瀏覽器中顯示為清單專案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="9cf35-317">![API 呼叫的結果會顯示在瀏覽器中做為清單專案](build-restful-apis-with-aspnet-web-api/_static/image23.png "API 呼叫的結果會顯示在瀏覽器中做為清單專案")</span><span class="sxs-lookup"><span data-stu-id="9cf35-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="9cf35-318">*API 呼叫的結果會顯示在瀏覽器中做為清單專案*</span><span class="sxs-lookup"><span data-stu-id="9cf35-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="9cf35-319">停止偵錯。</span><span class="sxs-lookup"><span data-stu-id="9cf35-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="9cf35-320">工作 2-修改索引視圖以提供 GUI 來建立連絡人</span><span class="sxs-lookup"><span data-stu-id="9cf35-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="9cf35-321">在這項工作中，您將繼續修改 MVC 應用程式的索引視圖。</span><span class="sxs-lookup"><span data-stu-id="9cf35-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="9cf35-322">表單將會新增至 HTML 網頁，此頁面將會捕獲使用者輸入，並將其傳送至 Web API 以建立新的連絡人，並建立新的 Web API 控制器方法以從 GUI 收集日期。</span><span class="sxs-lookup"><span data-stu-id="9cf35-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="9cf35-323">開啟**ContactController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="9cf35-324">將新方法新增至名為**Post**的控制器類別，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="9cf35-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="9cf35-325">（程式碼片段- *WEB API 實驗室-Ex03-Post 方法*）</span><span class="sxs-lookup"><span data-stu-id="9cf35-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="9cf35-326">如果尚未開啟，請在 Visual Studio 中開啟**Index. cshtml**檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="9cf35-327">在您于上一個工作中新增的未排序清單之後，將下面的 HTML 程式碼新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="9cf35-328">在檔底部的腳本專案中，新增下列反白顯示的程式碼以處理按鈕點按事件，這會使用 HTTP POST 呼叫將資料張貼至 Web API。</span><span class="sxs-lookup"><span data-stu-id="9cf35-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="9cf35-329">在**ContactController.cs**中，將中斷點放在**Post**方法上。</span><span class="sxs-lookup"><span data-stu-id="9cf35-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="9cf35-330">按**F5**在瀏覽器中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cf35-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="9cf35-331">在瀏覽器中載入頁面後，輸入新的連絡人名稱和識別碼，然後按一下 [**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cf35-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="9cf35-332">![在瀏覽器中載入的用戶端 HTML 檔案](build-restful-apis-with-aspnet-web-api/_static/image24.png "在瀏覽器中載入的用戶端 HTML 檔案")</span><span class="sxs-lookup"><span data-stu-id="9cf35-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="9cf35-333">*在瀏覽器中載入的用戶端 HTML 檔案*</span><span class="sxs-lookup"><span data-stu-id="9cf35-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="9cf35-334">當偵錯工具視窗在**Post**方法中中斷時，請查看**contact**參數的屬性。</span><span class="sxs-lookup"><span data-stu-id="9cf35-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="9cf35-335">這些值應符合您在表單中輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="9cf35-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="9cf35-336">![要從用戶端傳送至 Web API 的 Contact 物件](build-restful-apis-with-aspnet-web-api/_static/image25.png "要從用戶端傳送至 Web API 的 Contact 物件")</span><span class="sxs-lookup"><span data-stu-id="9cf35-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="9cf35-337">*要從用戶端傳送至 Web API 的 Contact 物件*</span><span class="sxs-lookup"><span data-stu-id="9cf35-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="9cf35-338">在偵錯工具中逐步執行方法，直到已建立**回應**變數為止。</span><span class="sxs-lookup"><span data-stu-id="9cf35-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="9cf35-339">在偵錯工具的 [**區域變數**] 視窗中進行檢查時，您會看到所有屬性都已設定。</span><span class="sxs-lookup"><span data-stu-id="9cf35-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="9cf35-340">![在偵錯工具中建立後的回應](build-restful-apis-with-aspnet-web-api/_static/image26.png "在偵錯工具中建立後的回應")</span><span class="sxs-lookup"><span data-stu-id="9cf35-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="9cf35-341">*在偵錯工具中建立後的回應*</span><span class="sxs-lookup"><span data-stu-id="9cf35-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="9cf35-342">如果您按下**F5**鍵，或在偵錯工具中按一下 [**繼續**]，則要求會完成。</span><span class="sxs-lookup"><span data-stu-id="9cf35-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="9cf35-343">當您切換回瀏覽器之後，新的連絡人就會新增至**contacts.json**執行所儲存的連絡人清單中。</span><span class="sxs-lookup"><span data-stu-id="9cf35-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="9cf35-344">![瀏覽器反映成功建立新的連絡人實例](build-restful-apis-with-aspnet-web-api/_static/image27.png "瀏覽器反映成功建立新的連絡人實例")</span><span class="sxs-lookup"><span data-stu-id="9cf35-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="9cf35-345">*瀏覽器反映成功建立新的連絡人實例*</span><span class="sxs-lookup"><span data-stu-id="9cf35-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="9cf35-346">此外，您可以遵循[附錄 C：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixC)，將此應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="9cf35-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="9cf35-347">總結</span><span class="sxs-lookup"><span data-stu-id="9cf35-347">Summary</span></span>

<span data-ttu-id="9cf35-348">本實驗室為您介紹了新的 ASP.NET Web API 架構，以及如何使用架構來 RESTful Web Api。</span><span class="sxs-lookup"><span data-stu-id="9cf35-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="9cf35-349">從這裡開始，您可以建立新的存放庫，以使用任意數目的機制和連線來加速資料持續性，而不是在此實驗室中提供的範例。</span><span class="sxs-lookup"><span data-stu-id="9cf35-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="9cf35-350">Web API 支援多項額外功能，例如從非 HTML 用戶端，啟用以支援 HTTP 和 JSON 或 XML 的任何語言所撰寫的通訊。</span><span class="sxs-lookup"><span data-stu-id="9cf35-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="9cf35-351">也可以在一般 Web 應用程式之外裝載 Web API 的功能，也能夠建立您自己的序列化格式。</span><span class="sxs-lookup"><span data-stu-id="9cf35-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="9cf35-352">ASP.NET 網站有一個專門用於 ASP.NET Web API 架構[[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)的區域。</span><span class="sxs-lookup"><span data-stu-id="9cf35-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="9cf35-353">此網站將繼續提供與 Web API 相關的最新資訊、範例和新聞，因此如果您想要深入瞭解建立可用於幾乎任何裝置或開發架構的自訂 Web Api，請經常檢查。</span><span class="sxs-lookup"><span data-stu-id="9cf35-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="9cf35-354">附錄 A：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="9cf35-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="9cf35-355">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="9cf35-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="9cf35-356">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="9cf35-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="9cf35-357">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="9cf35-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="9cf35-358">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="9cf35-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="9cf35-359">若要使用鍵盤新增程式碼片段（C#僅限）</span><span class="sxs-lookup"><span data-stu-id="9cf35-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="9cf35-360">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="9cf35-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="9cf35-361">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="9cf35-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="9cf35-362">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf35-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="9cf35-363">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="9cf35-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="9cf35-364">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="9cf35-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="9cf35-365">![開始鍵入程式碼片段名稱](build-restful-apis-with-aspnet-web-api/_static/image29.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="9cf35-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="9cf35-366">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="9cf35-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="9cf35-367">![按 Tab 鍵以選取反白顯示的程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="9cf35-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="9cf35-368">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="9cf35-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="9cf35-369">![再按一次 Tab 鍵，將會展開程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image31.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="9cf35-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="9cf35-370">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="9cf35-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="9cf35-371">若要使用滑鼠（C#、VISUAL BASIC 和 XML）加入程式碼片段</span><span class="sxs-lookup"><span data-stu-id="9cf35-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="9cf35-372">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="9cf35-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="9cf35-373">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="9cf35-374">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="9cf35-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="9cf35-375">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](build-restful-apis-with-aspnet-web-api/_static/image32.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="9cf35-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="9cf35-376">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="9cf35-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="9cf35-377">![按一下清單中的相關程式碼片段，即可加以選取](build-restful-apis-with-aspnet-web-api/_static/image33.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="9cf35-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="9cf35-378">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="9cf35-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="9cf35-379">附錄 B：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="9cf35-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="9cf35-380">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="9cf35-381">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="9cf35-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="9cf35-382">移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="9cf35-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="9cf35-383">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Azure SDK&quot;搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="9cf35-384">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-384">Click on **Install Now**.</span></span> <span data-ttu-id="9cf35-385">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="9cf35-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="9cf35-386">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="9cf35-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="9cf35-387">![安裝 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="9cf35-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="9cf35-388">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="9cf35-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="9cf35-389">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="9cf35-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="9cf35-391">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="9cf35-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="9cf35-392">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="9cf35-392">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="9cf35-394">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="9cf35-394">*Installation progress*</span></span>
6. <span data-ttu-id="9cf35-395">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-395">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="9cf35-397">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="9cf35-397">*Installation completed*</span></span>
7. <span data-ttu-id="9cf35-398">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="9cf35-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="9cf35-399">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="9cf35-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="9cf35-401">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="9cf35-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="9cf35-402">附錄 C：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="9cf35-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="9cf35-403">本附錄將說明如何從 Azure 入口網站建立新的網站，併發布您在實驗室之後取得的應用程式，利用 Azure 所提供的 Web Deploy 發佈功能。</span><span class="sxs-lookup"><span data-stu-id="9cf35-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="9cf35-404">工作 1-從 Azure 入口網站建立新的網站</span><span class="sxs-lookup"><span data-stu-id="9cf35-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="9cf35-405">移至[Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="9cf35-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cf35-406">有了 Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量成長而調整。</span><span class="sxs-lookup"><span data-stu-id="9cf35-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="9cf35-407">您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。</span><span class="sxs-lookup"><span data-stu-id="9cf35-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="9cf35-408">![登入 Windows Azure 入口網站](build-restful-apis-with-aspnet-web-api/_static/image39.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="9cf35-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="9cf35-409">*登入入口網站*</span><span class="sxs-lookup"><span data-stu-id="9cf35-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="9cf35-410">按一下命令列上的 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="9cf35-411">![建立新網站](build-restful-apis-with-aspnet-web-api/_static/image40.png "建立新網站")</span><span class="sxs-lookup"><span data-stu-id="9cf35-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="9cf35-412">*建立新網站*</span><span class="sxs-lookup"><span data-stu-id="9cf35-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="9cf35-413">按一下 [**計算** | 的**網站**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="9cf35-414">然後選取 [**快速建立**] 選項。</span><span class="sxs-lookup"><span data-stu-id="9cf35-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="9cf35-415">提供新網站的可用 URL，然後按一下 [**建立網站**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cf35-416">Azure 是在雲端中執行之 web 應用程式的主機，您可以控制和管理。</span><span class="sxs-lookup"><span data-stu-id="9cf35-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="9cf35-417">[快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="9cf35-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="9cf35-418">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="9cf35-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="9cf35-419">![使用 [快速建立] 建立新的網站](build-restful-apis-with-aspnet-web-api/_static/image41.png "使用 [快速建立] 建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="9cf35-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="9cf35-420">*使用 [快速建立] 建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="9cf35-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="9cf35-421">等到新**網站**建立完畢。</span><span class="sxs-lookup"><span data-stu-id="9cf35-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="9cf35-422">建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。</span><span class="sxs-lookup"><span data-stu-id="9cf35-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="9cf35-423">檢查新網站是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="9cf35-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="9cf35-424">![流覽至新網站](build-restful-apis-with-aspnet-web-api/_static/image42.png "流覽至新網站")</span><span class="sxs-lookup"><span data-stu-id="9cf35-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="9cf35-425">*流覽至新網站*</span><span class="sxs-lookup"><span data-stu-id="9cf35-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="9cf35-426">![網站正在執行](build-restful-apis-with-aspnet-web-api/_static/image43.png "網站正在執行")</span><span class="sxs-lookup"><span data-stu-id="9cf35-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="9cf35-427">*網站正在執行*</span><span class="sxs-lookup"><span data-stu-id="9cf35-427">*Web site running*</span></span>
6. <span data-ttu-id="9cf35-428">返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。</span><span class="sxs-lookup"><span data-stu-id="9cf35-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="9cf35-429">![開啟網站管理頁面](build-restful-apis-with-aspnet-web-api/_static/image44.png "開啟網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="9cf35-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="9cf35-430">*開啟網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="9cf35-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="9cf35-431">在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。</span><span class="sxs-lookup"><span data-stu-id="9cf35-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cf35-432">*發行設定檔*包含針對每個啟用的發行方法，將 web 應用程式發佈到 Azure 所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="9cf35-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="9cf35-433">發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="9cf35-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="9cf35-434">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發行至 Azure。</span><span class="sxs-lookup"><span data-stu-id="9cf35-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="9cf35-435">![正在下載網站發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image45.png "正在下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="9cf35-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="9cf35-436">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="9cf35-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="9cf35-437">將發行設定檔下載到已知的位置。</span><span class="sxs-lookup"><span data-stu-id="9cf35-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="9cf35-438">在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Azure。</span><span class="sxs-lookup"><span data-stu-id="9cf35-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="9cf35-439">![儲存發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image46.png "正在儲存發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="9cf35-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="9cf35-440">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="9cf35-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="9cf35-441">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="9cf35-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="9cf35-442">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9cf35-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="9cf35-443">如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="9cf35-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="9cf35-444">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="9cf35-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="9cf35-445">您可以在 Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9cf35-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="9cf35-446">如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。</span><span class="sxs-lookup"><span data-stu-id="9cf35-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="9cf35-447">記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="9cf35-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="9cf35-448">請不要建立資料庫，因為它會在稍後的階段中建立。</span><span class="sxs-lookup"><span data-stu-id="9cf35-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="9cf35-449">![SQL Database Server 儀表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server 儀表板")</span><span class="sxs-lookup"><span data-stu-id="9cf35-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="9cf35-450">*SQL Database Server 儀表板*</span><span class="sxs-lookup"><span data-stu-id="9cf35-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="9cf35-451">在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf35-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="9cf35-452">若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](build-restful-apis-with-aspnet-web-api/_static/image48.png) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cf35-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![正在新增用戶端 IP 位址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="9cf35-454">*正在新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="9cf35-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="9cf35-455">將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="9cf35-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="9cf35-457">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="9cf35-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="9cf35-458">工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="9cf35-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="9cf35-459">返回 ASP.NET MVC 4 解決方案。</span><span class="sxs-lookup"><span data-stu-id="9cf35-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="9cf35-460">在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。</span><span class="sxs-lookup"><span data-stu-id="9cf35-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="9cf35-461">![發行應用程式](build-restful-apis-with-aspnet-web-api/_static/image51.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="9cf35-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="9cf35-462">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="9cf35-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="9cf35-463">匯入您在第一個工作中儲存的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="9cf35-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="9cf35-464">![匯入發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image52.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="9cf35-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="9cf35-465">*正在匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="9cf35-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="9cf35-466">按一下 [**驗證連接**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-466">Click **Validate Connection**.</span></span> <span data-ttu-id="9cf35-467">驗證完成後，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cf35-468">當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。</span><span class="sxs-lookup"><span data-stu-id="9cf35-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="9cf35-469">![正在驗證連接](build-restful-apis-with-aspnet-web-api/_static/image53.png "正在驗證連接")</span><span class="sxs-lookup"><span data-stu-id="9cf35-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="9cf35-470">*正在驗證連接*</span><span class="sxs-lookup"><span data-stu-id="9cf35-470">*Validating connection*</span></span>
4. <span data-ttu-id="9cf35-471">在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="9cf35-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="9cf35-472">![Web deploy 設定](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy 設定")</span><span class="sxs-lookup"><span data-stu-id="9cf35-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="9cf35-473">*Web deploy 設定*</span><span class="sxs-lookup"><span data-stu-id="9cf35-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="9cf35-474">設定資料庫連接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9cf35-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="9cf35-475">在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="9cf35-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="9cf35-476">在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf35-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="9cf35-477">在 [**密碼**] 中輸入您的伺服器管理員登入密碼。</span><span class="sxs-lookup"><span data-stu-id="9cf35-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="9cf35-478">輸入新的資料庫名稱，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="9cf35-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="9cf35-479">![正在設定目的地連接字串](build-restful-apis-with-aspnet-web-api/_static/image55.png "正在設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="9cf35-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="9cf35-480">*正在設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="9cf35-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="9cf35-481">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-481">Then click **OK**.</span></span> <span data-ttu-id="9cf35-482">當系統提示您建立資料庫時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="9cf35-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="9cf35-483">![建立資料庫](build-restful-apis-with-aspnet-web-api/_static/image56.png "建立資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="9cf35-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="9cf35-484">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="9cf35-484">*Creating the database*</span></span>
7. <span data-ttu-id="9cf35-485">您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="9cf35-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="9cf35-486">然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-486">Then click **Next**.</span></span>

    <span data-ttu-id="9cf35-487">![指向 SQL Database 的連接字串](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL Database 的連接字串")</span><span class="sxs-lookup"><span data-stu-id="9cf35-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="9cf35-488">*指向 SQL Database 的連接字串*</span><span class="sxs-lookup"><span data-stu-id="9cf35-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="9cf35-489">在 [**預覽**] 頁面中，按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="9cf35-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="9cf35-490">![發行 web 應用程式](build-restful-apis-with-aspnet-web-api/_static/image58.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="9cf35-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="9cf35-491">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="9cf35-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="9cf35-492">發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="9cf35-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="9cf35-493">![發行至 Windows Azure 的應用程式](build-restful-apis-with-aspnet-web-api/_static/image59.png "發行至 Windows Azure 的應用程式")</span><span class="sxs-lookup"><span data-stu-id="9cf35-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="9cf35-494">*已發佈至 Azure 的應用程式*</span><span class="sxs-lookup"><span data-stu-id="9cf35-494">*Application published to Azure*</span></span>
