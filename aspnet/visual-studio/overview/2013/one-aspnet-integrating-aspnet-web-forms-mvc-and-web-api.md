---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 實習實驗室：一個 ASP.NET：整合 ASP.NET Web Forms、MVC 和 Web API |Microsoft Docs
author: rick-anderson
description: ASP.NET 是一種架構，可讓您使用 MVC、Web API 等特殊技術來建立網站、應用程式和服務。 擴充 ASP.NET h 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623197"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="010ec-104">實習實驗室：一 ASP.NET：整合 ASP.NET Web Forms、MVC 和 Web API</span><span class="sxs-lookup"><span data-stu-id="010ec-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>

<span data-ttu-id="010ec-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="010ec-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="010ec-106">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="010ec-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="010ec-107">ASP.NET 是一種架構，可讓您使用 MVC、Web API 等特殊技術來建立網站、應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="010ec-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="010ec-108">隨著擴充 ASP.NET 的建立和表示需要整合這些技術，最近致力於進行**一項 ASP.NET**。</span><span class="sxs-lookup"><span data-stu-id="010ec-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="010ec-109">Visual Studio 2013 引進了新的整合專案系統，可讓您建立應用程式，並在一個專案中使用所有 ASP.NET 技術。</span><span class="sxs-lookup"><span data-stu-id="010ec-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="010ec-110">這項功能可讓您不需要在專案開始時挑選一項技術，而是要鼓勵在一個專案中使用多個 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="010ec-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="010ec-111">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="010ec-111">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="010ec-112">概觀</span><span class="sxs-lookup"><span data-stu-id="010ec-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="010ec-113">目標</span><span class="sxs-lookup"><span data-stu-id="010ec-113">Objectives</span></span>

<span data-ttu-id="010ec-114">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="010ec-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="010ec-115">根據**一個 ASP.NET**專案類型建立網站</span><span class="sxs-lookup"><span data-stu-id="010ec-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="010ec-116">在相同專案中使用不同的**ASP.NET**架構，例如**MVC**和**Web API**</span><span class="sxs-lookup"><span data-stu-id="010ec-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="010ec-117">識別**ASP.NET**應用程式的主要元件</span><span class="sxs-lookup"><span data-stu-id="010ec-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="010ec-118">利用**ASP.NET**的框架架構，自動建立控制器和視圖，以根據您的模型類別來執行 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="010ec-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="010ec-119">使用適用于每個工作的適當工具，公開電腦和人類可讀格式的同一組資訊</span><span class="sxs-lookup"><span data-stu-id="010ec-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="010ec-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="010ec-120">Prerequisites</span></span>

<span data-ttu-id="010ec-121">若要完成此實際操作實驗室，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="010ec-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="010ec-122">[適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="010ec-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="010ec-123">Visual Studio 2013 Update 1</span><span class="sxs-lookup"><span data-stu-id="010ec-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="010ec-124">安裝程式</span><span class="sxs-lookup"><span data-stu-id="010ec-124">Setup</span></span>

<span data-ttu-id="010ec-125">為了在此實際操作實驗室中執行練習，您必須先設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="010ec-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="010ec-126">開啟 Windows Explorer 並流覽至實驗室的 [**源**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="010ec-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="010ec-127">以滑鼠右鍵按一下**setup.exe** ，然後選取 [以**系統管理員身分執行**] 以啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="010ec-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="010ec-128">如果顯示 [使用者帳戶控制] 對話方塊，請確認動作以繼續。</span><span class="sxs-lookup"><span data-stu-id="010ec-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="010ec-129">執行安裝程式之前，請確定您已檢查過此實驗室的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="010ec-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="010ec-130">使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="010ec-130">Using the Code Snippets</span></span>

<span data-ttu-id="010ec-131">在整個實驗室檔中，系統會指示您插入程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="010ec-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="010ec-132">為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 2013 內進行存取，以避免必須以手動方式新增。</span><span class="sxs-lookup"><span data-stu-id="010ec-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="010ec-133">每個練習都附有一個起始解決方案，此方案位於練習的 [**開始**] 資料夾中，可讓您獨立于其他練習之外進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="010ec-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="010ec-134">請注意，在練習期間新增的程式碼片段缺少這些起始的解決方案，而且在您完成練習之前可能無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="010ec-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="010ec-135">在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的**結束**資料夾，其中含有完成對應練習中步驟所產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="010ec-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="010ec-136">如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。</span><span class="sxs-lookup"><span data-stu-id="010ec-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="010ec-137">練習</span><span class="sxs-lookup"><span data-stu-id="010ec-137">Exercises</span></span>

<span data-ttu-id="010ec-138">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="010ec-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="010ec-139">建立新的 Web Forms 專案</span><span class="sxs-lookup"><span data-stu-id="010ec-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="010ec-140">使用樣板建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="010ec-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="010ec-141">使用樣板建立 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="010ec-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="010ec-142">完成此實驗室的預估時間： **60 分鐘**</span><span class="sxs-lookup"><span data-stu-id="010ec-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="010ec-143">當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。</span><span class="sxs-lookup"><span data-stu-id="010ec-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="010ec-144">每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。</span><span class="sxs-lookup"><span data-stu-id="010ec-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="010ec-145">本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。</span><span class="sxs-lookup"><span data-stu-id="010ec-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="010ec-146">如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。</span><span class="sxs-lookup"><span data-stu-id="010ec-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="010ec-147">練習1：建立新的 Web form 專案</span><span class="sxs-lookup"><span data-stu-id="010ec-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="010ec-148">在此練習中，您將使用**ASP.NET**整合專案體驗，在 Visual Studio 2013 中建立新的 Web form 網站，這可讓您輕鬆地在相同的應用程式中整合 web FORMS、MVC 和 web API 元件。</span><span class="sxs-lookup"><span data-stu-id="010ec-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="010ec-149">接著，您將探索所產生的解決方案並識別其元件，最後您會看到網站的運作方式。</span><span class="sxs-lookup"><span data-stu-id="010ec-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="010ec-150">工作1–使用一 ASP.NET 體驗建立新網站</span><span class="sxs-lookup"><span data-stu-id="010ec-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="010ec-151">在這項工作中，您將根據**ASP.NET**專案類型，開始在 Visual Studio 中建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="010ec-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="010ec-152">**其中一個 ASP.NET**會將所有 ASP.NET 技術合併，並提供您視需要混合使用和比對的選項。</span><span class="sxs-lookup"><span data-stu-id="010ec-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="010ec-153">接著，您將會辨識應用程式中即時的 Web form、MVC 和 Web API 的不同元件。</span><span class="sxs-lookup"><span data-stu-id="010ec-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="010ec-154">開啟**Web Visual Studio Express 2013** ，然後選取 [檔案] **|新增專案 ...** 以啟動新的解決方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![建立新專案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="010ec-156">*建立新專案*</span><span class="sxs-lookup"><span data-stu-id="010ec-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="010ec-157">在 [**新增專案**] 對話方塊中，選取視覺效果  **C#底下的 [ASP.NET Web 應用程式] |[Web** ] 索引標籤，並確認已選取 [ **.NET Framework 4.5** ]。</span><span class="sxs-lookup"><span data-stu-id="010ec-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="010ec-158">將專案命名為*MyHybridSite*，選擇 [**位置**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="010ec-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![新增 ASP.NET Web 應用程式專案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="010ec-160">*建立新的 ASP.NET Web 應用程式專案*</span><span class="sxs-lookup"><span data-stu-id="010ec-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="010ec-161">在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **Web** form] 範本，然後選取 [ **MVC**和**Web API** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="010ec-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="010ec-162">此外，請確定 [**驗證**] 選項已設為 [**個別使用者帳戶**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="010ec-163">按一下 [確定] 繼續操作。</span><span class="sxs-lookup"><span data-stu-id="010ec-163">Click **OK** to continue.</span></span>

    ![使用 Web Forms 範本建立新的專案，包括 Web API 和 MVC 元件](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="010ec-165">*使用 Web Forms 範本建立新的專案，包括 Web API 和 MVC 元件*</span><span class="sxs-lookup"><span data-stu-id="010ec-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="010ec-166">您現在可以探索所產生解決方案的結構。</span><span class="sxs-lookup"><span data-stu-id="010ec-166">You can now explore the structure of the generated solution.</span></span>

    ![探索產生的解決方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="010ec-168">*探索產生的解決方案*</span><span class="sxs-lookup"><span data-stu-id="010ec-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="010ec-169">**帳戶：** 此資料夾包含要註冊的 Web 表單頁面、登入及管理應用程式的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="010ec-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="010ec-170">在設定 Web form 專案範本期間選取 [**個別使用者帳戶**] 驗證選項時，會加入此資料夾。</span><span class="sxs-lookup"><span data-stu-id="010ec-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="010ec-171">**模型：** 此資料夾將包含代表您的應用程式資料的類別。</span><span class="sxs-lookup"><span data-stu-id="010ec-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="010ec-172">**控制器**和**VIEWS**： **ASP.NET MVC**和**ASP.NET Web API**元件都需要這些資料夾。</span><span class="sxs-lookup"><span data-stu-id="010ec-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="010ec-173">在下一個練習中，您將會探索 MVC 和 Web API 技術。</span><span class="sxs-lookup"><span data-stu-id="010ec-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="010ec-174">Default.aspx **、** **Contact .aspx**和**關於 .aspx**檔案是預先定義的 Web Form 頁面，可供您用來做為建立應用程式特定頁面的起點。</span><span class="sxs-lookup"><span data-stu-id="010ec-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="010ec-175">這些檔案的程式設計邏輯位於稱為 &quot;程式碼後置&quot; 檔案的個別檔案中，該檔案具有 &quot;.aspx .vb&quot; 或 &quot;aspx.cs&quot; 延伸模組（視使用的語言而定）。</span><span class="sxs-lookup"><span data-stu-id="010ec-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="010ec-176">程式碼後置邏輯會在伺服器上執行，並以動態方式產生頁面的 HTML 輸出。</span><span class="sxs-lookup"><span data-stu-id="010ec-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="010ec-177">[**網站**] 和 [**網站**] 頁面會定義應用程式中所有頁面的外觀與風格，以及標準行為。</span><span class="sxs-lookup"><span data-stu-id="010ec-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="010ec-178">按兩下**default.aspx**檔案以流覽頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="010ec-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![探索 default.aspx 頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="010ec-180">*探索 default.aspx 頁面*</span><span class="sxs-lookup"><span data-stu-id="010ec-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="010ec-181">檔案頂端的**Page**指示詞會定義 Web Forms 頁面的屬性。</span><span class="sxs-lookup"><span data-stu-id="010ec-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="010ec-182">例如， **MasterPageFile**屬性會指定主版頁面的路徑，在此案例中為 [*網站. 主版*] 頁面，而 [**繼承**] 屬性則會定義要繼承之頁面的程式碼後置類別。</span><span class="sxs-lookup"><span data-stu-id="010ec-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="010ec-183">這個類別位於程式碼後**置屬性所決定的檔案**中。</span><span class="sxs-lookup"><span data-stu-id="010ec-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="010ec-184">**Asp： Content**控制項會保存網頁的實際內容（文字、標記和控制項），並對應至主版頁面上的**asp： ContentPlaceHolder**控制項。</span><span class="sxs-lookup"><span data-stu-id="010ec-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="010ec-185">在此情況下，頁面內容會呈現在 [*網站*] 頁面中定義的*MainContent*控制項內。</span><span class="sxs-lookup"><span data-stu-id="010ec-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="010ec-186">展開**應用程式\_[開始**] 資料夾，並注意**WebApiConfig.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="010ec-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="010ec-187">Visual Studio 將該檔案包含在產生的解決方案中，因為您在使用一個 ASP.NET 範本設定專案時包含 Web API。</span><span class="sxs-lookup"><span data-stu-id="010ec-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="010ec-188">開啟**WebApiConfig.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="010ec-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="010ec-189">在*WebApiConfig*類別中，您會找到與 web api 相關聯的設定，其會將 HTTP 路由對應至**web api 控制器**。</span><span class="sxs-lookup"><span data-stu-id="010ec-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="010ec-190">開啟**RouteConfig.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="010ec-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="010ec-191">在*RegisterRoutes*方法中，您會發現與 mvc 相關聯的設定，其會將 HTTP 路由對應至**mvc 控制器**。</span><span class="sxs-lookup"><span data-stu-id="010ec-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="010ec-192">工作2–執行解決方案</span><span class="sxs-lookup"><span data-stu-id="010ec-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="010ec-193">在這項工作中，您將執行所產生的解決方案、探索應用程式及其部分功能，例如 URL 重寫和內建驗證。</span><span class="sxs-lookup"><span data-stu-id="010ec-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="010ec-194">若要執行方案，請按**F5**或按一下位於工具列上的 [**開始**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="010ec-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="010ec-195">應用程式首頁應該會在瀏覽器中開啟。</span><span class="sxs-lookup"><span data-stu-id="010ec-195">The application home page should open in the browser.</span></span>

    ![正在執行解決方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="010ec-197">確認正在叫用 Web form 頁面。</span><span class="sxs-lookup"><span data-stu-id="010ec-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="010ec-198">若要這麼做，請將 **/contact.aspx**附加至網址列中的 URL，然後按**enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="010ec-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![易記的 URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="010ec-200">*易記 Url*</span><span class="sxs-lookup"><span data-stu-id="010ec-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="010ec-201">如您所見，URL 會變更為 **/contact**。</span><span class="sxs-lookup"><span data-stu-id="010ec-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="010ec-202">從**ASP.NET 4**開始，URL 路由功能已新增至 Web 表單，因此您可以撰寫類似 *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* 的 url，而不是 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* 。</span><span class="sxs-lookup"><span data-stu-id="010ec-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="010ec-203">如需詳細資訊，請參閱[URL 路由](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="010ec-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="010ec-204">您現在會探索整合到應用程式中的驗證流程。</span><span class="sxs-lookup"><span data-stu-id="010ec-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="010ec-205">若要這樣做，請按一下頁面右上角的 [**註冊**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![註冊新的使用者](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="010ec-207">*註冊新的使用者*</span><span class="sxs-lookup"><span data-stu-id="010ec-207">*Registering a new user*</span></span>
4. <span data-ttu-id="010ec-208">在 [**註冊**] 頁面中，輸入**使用者名稱**和**密碼**，然後按一下 [**註冊**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![註冊頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="010ec-210">*註冊頁面*</span><span class="sxs-lookup"><span data-stu-id="010ec-210">*Register page*</span></span>
5. <span data-ttu-id="010ec-211">應用程式會註冊新帳戶，並驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="010ec-211">The application registers the new account, and the user is authenticated.</span></span>

    ![使用者已驗證](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="010ec-213">*使用者已驗證*</span><span class="sxs-lookup"><span data-stu-id="010ec-213">*User authenticated*</span></span>
6. <span data-ttu-id="010ec-214">返回 Visual Studio，然後按**SHIFT + F5**停止調試。</span><span class="sxs-lookup"><span data-stu-id="010ec-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="010ec-215">練習2：使用樣板建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="010ec-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="010ec-216">在此練習中，您將利用 Visual Studio 所提供的 ASP.NET 樣板架構，建立具有動作和 Razor views 的 ASP.NET MVC 5 控制器來執行 CRUD 作業，而不需要撰寫任何一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="010ec-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="010ec-217">此樣板進程會使用 Entity Framework Code First，在 SQL 資料庫中產生資料內容和資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="010ec-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="010ec-218">**關於 Entity Framework Code First**</span><span class="sxs-lookup"><span data-stu-id="010ec-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="010ec-219">Entity Framework （EF）是物件關聯式對應程式（ORM），可讓您以概念應用程式模型進行程式設計來建立資料存取應用程式，而不需要直接使用關聯式儲存架構進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="010ec-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="010ec-220">Entity Framework Code First 模型化工作流程可讓您使用自己的網域類別來代表 EF 在執行查詢、變更追蹤和更新函數時所依賴的模型。</span><span class="sxs-lookup"><span data-stu-id="010ec-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="010ec-221">使用 Code First 開發工作流程，您不需要藉由建立資料庫或指定架構來開始您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="010ec-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="010ec-222">相反地，您可以撰寫標準的 .NET 類別，為您的應用程式定義最適當的領域模型物件，Entity Framework 將會為您建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="010ec-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="010ec-223">您可以在[這裡](../../../entity-framework.md)深入瞭解 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="010ec-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="010ec-224">工作1–建立新的模型</span><span class="sxs-lookup"><span data-stu-id="010ec-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="010ec-225">您現在將定義**Person**類別，這會是由「基類庫」進程用來建立 MVC 控制器和 views 的模型。</span><span class="sxs-lookup"><span data-stu-id="010ec-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="010ec-226">您將從建立**Person**模型類別開始，並使用「基類庫」功能自動建立控制器中的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="010ec-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="010ec-227">開啟**Web 的 Visual Studio Express 2013**和位於**來源/Ex2-MvcScaffolding/Begin**資料夾中的**MyHybridSite。**</span><span class="sxs-lookup"><span data-stu-id="010ec-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="010ec-228">或者，您可以繼續使用您在上一個練習中取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="010ec-229">在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案的 [**模型**] 資料夾，然後選取 [**新增] |類別 ...** 。</span><span class="sxs-lookup"><span data-stu-id="010ec-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![新增 Person 模型類別](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="010ec-231">*新增 Person 模型類別*</span><span class="sxs-lookup"><span data-stu-id="010ec-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="010ec-232">在 [**加入新專案**] 對話方塊中，將檔案命名為*Person.cs* ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![建立 Person 模型類別](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="010ec-234">*建立 Person 模型類別*</span><span class="sxs-lookup"><span data-stu-id="010ec-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="010ec-235">將**Person.cs**檔案的內容取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="010ec-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="010ec-236">按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="010ec-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="010ec-237">（程式碼片段- *BringingTogetherOneAspNet-Ex2-PersonClass*）</span><span class="sxs-lookup"><span data-stu-id="010ec-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="010ec-238">在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案，然後選取 [**建立**]，或按**CTRL + SHIFT + B**來建立專案。</span><span class="sxs-lookup"><span data-stu-id="010ec-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="010ec-239">工作2–建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="010ec-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="010ec-240">建立**人員**模型之後，您將使用 ASP.NET MVC 樣板搭配 Entity Framework 來建立 CRUD 控制器動作和**人員**的視圖。</span><span class="sxs-lookup"><span data-stu-id="010ec-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="010ec-241">在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案的 [**控制器**] 資料夾，然後選取 [**新增] |新增 Scaffold 專案 ...** 。</span><span class="sxs-lookup"><span data-stu-id="010ec-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![建立新的 scaffold 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="010ec-243">*建立新的 Scaffold 控制器*</span><span class="sxs-lookup"><span data-stu-id="010ec-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="010ec-244">在 [**新增 Scaffold** ] 對話方塊中，**使用 Entity Framework 選取 [具有 views 的 MVC 5 控制器**]，然後按一下 [**新增]。**</span><span class="sxs-lookup"><span data-stu-id="010ec-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![選取具有 views 和 Entity Framework 的 MVC 5 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="010ec-246">*選取具有 views 和 Entity Framework 的 MVC 5 控制器*</span><span class="sxs-lookup"><span data-stu-id="010ec-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="010ec-247">將 [ *MvcPersonController* ] 設定為 [**控制器名稱**]，選取 [**使用非同步控制器動作**] 選項，然後選取 [ **Person （MyHybridSite）** ] 做為**模型類別**。</span><span class="sxs-lookup"><span data-stu-id="010ec-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![新增具有樣板的 MVC 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="010ec-249">*新增具有樣板的 MVC 控制器*</span><span class="sxs-lookup"><span data-stu-id="010ec-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="010ec-250">在 [**資料內容類別**] 底下，按一下 [**新增資料內容 ...** ]。</span><span class="sxs-lookup"><span data-stu-id="010ec-250">Under **Data context class**, click **New data context...**.</span></span>

    ![建立新的資料內容](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="010ec-252">*建立新的資料內容*</span><span class="sxs-lookup"><span data-stu-id="010ec-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="010ec-253">在 [**新增資料內容**] 對話方塊中，將新的資料內容命名為*PersonCoNtext* ，然後按一下 [**加入**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![建立新的 PersonCoNtext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="010ec-255">*建立新的 PersonCoNtext 類型*</span><span class="sxs-lookup"><span data-stu-id="010ec-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="010ec-256">按一下 [**新增**]，為具有樣板的**人員**建立新的控制器。</span><span class="sxs-lookup"><span data-stu-id="010ec-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="010ec-257">Visual Studio 接著會產生控制器動作、人員資料內容和 Razor views。</span><span class="sxs-lookup"><span data-stu-id="010ec-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![建立具有樣板的 MVC 控制器之後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="010ec-259">*建立具有樣板的 MVC 控制器之後*</span><span class="sxs-lookup"><span data-stu-id="010ec-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="010ec-260">開啟 [**控制器**] 資料夾中的**MvcPersonController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="010ec-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="010ec-261">請注意，CRUD 動作方法已自動產生。</span><span class="sxs-lookup"><span data-stu-id="010ec-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="010ec-262">藉由在先前步驟的 [樣板] 選項中選取 [**使用非同步控制器動作**] 核取方塊，Visual Studio 會為牽涉到人員資料內容存取權的所有動作產生非同步動作方法。</span><span class="sxs-lookup"><span data-stu-id="010ec-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="010ec-263">建議您針對長時間執行的非 CPU 系結要求使用非同步動作方法，以避免在處理要求時封鎖 Web 服務器執行工作。</span><span class="sxs-lookup"><span data-stu-id="010ec-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="010ec-264">工作3–執行解決方案</span><span class="sxs-lookup"><span data-stu-id="010ec-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="010ec-265">在這項工作中，您將再次執行方案，以確認**人員**的觀點如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="010ec-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="010ec-266">您將加入新的人員，以確認它已成功儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="010ec-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="010ec-267">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="010ec-268">流覽至 **/MvcPerson**。</span><span class="sxs-lookup"><span data-stu-id="010ec-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="010ec-269">[Scaffold] 視圖會顯示應顯示的人員清單。</span><span class="sxs-lookup"><span data-stu-id="010ec-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="010ec-270">按一下 [**建立新**的] 以加入新人員。</span><span class="sxs-lookup"><span data-stu-id="010ec-270">Click **Create New** to add a new person.</span></span>

    ![流覽至 scaffold MVC views](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="010ec-272">*流覽至 scaffold MVC views*</span><span class="sxs-lookup"><span data-stu-id="010ec-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="010ec-273">在 [**建立**] 視圖中，提供人員的**名稱**和**年齡**，然後按一下 [**建立**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![加入新人員](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="010ec-275">*加入新人員*</span><span class="sxs-lookup"><span data-stu-id="010ec-275">*Adding a new person*</span></span>
5. <span data-ttu-id="010ec-276">新人員會加入清單中。</span><span class="sxs-lookup"><span data-stu-id="010ec-276">The new person is added to the list.</span></span> <span data-ttu-id="010ec-277">在 [專案] 清單中，按一下 [**詳細資料**] 以顯示個人的詳細資料檢視。</span><span class="sxs-lookup"><span data-stu-id="010ec-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="010ec-278">然後，在**詳細資料**視圖中，按一下 [**返回清單**] 以返回清單視圖。</span><span class="sxs-lookup"><span data-stu-id="010ec-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![個人的詳細資料檢視](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="010ec-280">*個人的詳細資料檢視*</span><span class="sxs-lookup"><span data-stu-id="010ec-280">*Person's details view*</span></span>
6. <span data-ttu-id="010ec-281">按一下 [**刪除**] 連結以刪除人員。</span><span class="sxs-lookup"><span data-stu-id="010ec-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="010ec-282">在 [**刪除**] 視圖中，按一下 [**刪除**] 以確認操作。</span><span class="sxs-lookup"><span data-stu-id="010ec-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![刪除人員](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="010ec-284">*刪除人員*</span><span class="sxs-lookup"><span data-stu-id="010ec-284">*Deleting a person*</span></span>
7. <span data-ttu-id="010ec-285">返回 Visual Studio，然後按**SHIFT + F5**停止調試。</span><span class="sxs-lookup"><span data-stu-id="010ec-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="010ec-286">練習3：使用樣板建立 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="010ec-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="010ec-287">Web API 架構是 ASP.NET 堆疊的一部分，其設計目的是為了讓您更輕鬆地執行 HTTP 服務，通常會透過 RESTful API 傳送和接收 JSON 或 XML 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="010ec-288">在此練習中，您將再次使用 ASP.NET 的樣板來產生 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="010ec-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="010ec-289">您將使用上一個練習中的相同**person**和**PersonCoNtext**類別，以 JSON 格式提供相同的人員資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="010ec-290">您將瞭解如何在相同的 ASP.NET 應用程式中以不同的方式公開相同的資源。</span><span class="sxs-lookup"><span data-stu-id="010ec-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="010ec-291">工作1–建立 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="010ec-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="010ec-292">在這項工作中，您將建立新的**WEB API 控制器**，它會以電腦可耗用的格式（例如 JSON）公開人員資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="010ec-293">如果尚未開啟，請開啟**Visual Studio Express 2013 For Web** ，然後開啟位於**Source/Ex3-WebAPI/Begin**資料夾中的**MyHybridSite。**</span><span class="sxs-lookup"><span data-stu-id="010ec-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="010ec-294">或者，您可以繼續使用您在上一個練習中取得的解決方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="010ec-295">如果您從練習3開始使用開始解決方案，請按**CTRL + SHIFT + B**來建立方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="010ec-296">在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案的 [**控制器**] 資料夾，然後選取 [**新增] |新增 Scaffold 專案 ...** 。</span><span class="sxs-lookup"><span data-stu-id="010ec-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![建立新的 scaffold 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="010ec-298">*建立新的 scaffold 控制器*</span><span class="sxs-lookup"><span data-stu-id="010ec-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="010ec-299">在 [**新增 Scaffold** ] 對話方塊中，選取左窗格中的 [ **web api** ]，然後在中間窗格中，**使用 Entity Framework** ，然後按一下 [新增] **。**</span><span class="sxs-lookup"><span data-stu-id="010ec-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="010ec-300">![選取具有動作和 Entity Framework 的 Web API 2 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "選取具有動作和 Entity Framework 的 Web API 2 控制器")</span><span class="sxs-lookup"><span data-stu-id="010ec-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="010ec-301">*選取具有動作和 Entity Framework 的 Web API 2 控制器*</span><span class="sxs-lookup"><span data-stu-id="010ec-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="010ec-302">將 [ *ApiPersonController* ] 設定為 [**控制器名稱**]，選取 [**使用非同步控制器動作**] 選項，然後選取 [ **Person] （MyHybridSite）** 和 [ **PersonCoNtext （MyHybridSite）** ] 做為 [**模型**] 和 [**資料內容**類別]。</span><span class="sxs-lookup"><span data-stu-id="010ec-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="010ec-303">然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="010ec-303">Then click **Add**.</span></span>

    <span data-ttu-id="010ec-304">![使用樣板新增 Web API 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "使用樣板新增 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="010ec-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="010ec-305">*使用樣板新增 Web API 控制器*</span><span class="sxs-lookup"><span data-stu-id="010ec-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="010ec-306">Visual Studio 接著會產生具有四個 CRUD 動作的**ApiPersonController**類別，以處理您的資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="010ec-307">![使用樣板建立 Web API 控制器之後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "使用樣板建立 Web API 控制器之後")</span><span class="sxs-lookup"><span data-stu-id="010ec-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="010ec-308">*使用樣板建立 Web API 控制器之後*</span><span class="sxs-lookup"><span data-stu-id="010ec-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="010ec-309">開啟**ApiPersonController.cs**檔案，並檢查*GetPeople*動作方法。</span><span class="sxs-lookup"><span data-stu-id="010ec-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="010ec-310">這個方法會查詢**PersonCoNtext**類型的 db 欄位，以便取得人員資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="010ec-311">現在請注意方法定義上方的批註。</span><span class="sxs-lookup"><span data-stu-id="010ec-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="010ec-312">它提供的 URI 會公開此動作，而您將在下一個工作中使用。</span><span class="sxs-lookup"><span data-stu-id="010ec-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="010ec-313">根據預設，Web API 會設定為攔截 */api*路徑的查詢，以避免與 MVC 控制器發生衝突。</span><span class="sxs-lookup"><span data-stu-id="010ec-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="010ec-314">如果您需要變更此設定，請參閱[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="010ec-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="010ec-315">工作2–執行解決方案</span><span class="sxs-lookup"><span data-stu-id="010ec-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="010ec-316">在這項工作中，您將使用 Internet Explorer **F12 開發人員工具**來檢查來自 Web API 控制器的完整回應。</span><span class="sxs-lookup"><span data-stu-id="010ec-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="010ec-317">您將瞭解如何捕捉網路流量，以深入瞭解您的應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="010ec-318">請確定已在 [Visual Studio] 工具列上的 [**開始**] 按鈕中選取**Internet Explorer** 。</span><span class="sxs-lookup"><span data-stu-id="010ec-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 選項](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="010ec-320">**F12 開發人員工具**有一組廣泛的功能，不涵蓋在此實際操作實驗室中。</span><span class="sxs-lookup"><span data-stu-id="010ec-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="010ec-321">如果您想要深入瞭解，請參閱[使用 F12 開發人員工具](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="010ec-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>

1. <span data-ttu-id="010ec-322">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="010ec-323">為了正確地執行此工作，您的應用程式需要有資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="010ec-324">如果您的資料庫是空的，您可以回到練習2中的工作3，並遵循如何使用 MVC views 建立新人員的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="010ec-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="010ec-325">在瀏覽器中，按**F12**開啟 [**開發人員工具**] 面板。</span><span class="sxs-lookup"><span data-stu-id="010ec-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="010ec-326">按**CTRL** + **4**或按一下**網路**圖示，然後按一下綠色箭號按鈕來開始捕獲網路流量。</span><span class="sxs-lookup"><span data-stu-id="010ec-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="010ec-327">![正在起始 Web API 網路捕獲](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "正在起始 Web API 網路捕獲")</span><span class="sxs-lookup"><span data-stu-id="010ec-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="010ec-328">*正在起始 Web API 網路捕獲*</span><span class="sxs-lookup"><span data-stu-id="010ec-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="010ec-329">將**api/ApiPerson**附加至瀏覽器網址列中的 URL。</span><span class="sxs-lookup"><span data-stu-id="010ec-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="010ec-330">您現在將會從**ApiPersonController**檢查回應的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="010ec-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="010ec-331">![透過 Web API 來抓取人員資料](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "透過 Web API 來抓取人員資料")</span><span class="sxs-lookup"><span data-stu-id="010ec-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="010ec-332">*透過 Web API 來抓取人員資料*</span><span class="sxs-lookup"><span data-stu-id="010ec-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="010ec-333">下載完成後，系統會提示您對下載的檔案進行動作。</span><span class="sxs-lookup"><span data-stu-id="010ec-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="010ec-334">讓對話方塊保持開啟狀態，以便能夠透過 [開發人員] 工具視窗觀看回應內容。</span><span class="sxs-lookup"><span data-stu-id="010ec-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="010ec-335">現在，您將會檢查回應的主體。</span><span class="sxs-lookup"><span data-stu-id="010ec-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="010ec-336">若要這樣做，請按一下 [**詳細資料**] 索引標籤，然後按一下 [**回應主體**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="010ec-337">您可以檢查下載的資料是否為具有與**Person**類別對應之屬性**識別碼**、**名稱**和**年齡**的物件清單。</span><span class="sxs-lookup"><span data-stu-id="010ec-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="010ec-338">![查看 Web API 回應主體](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "查看 Web API 回應主體")</span><span class="sxs-lookup"><span data-stu-id="010ec-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="010ec-339">*查看 Web API 回應主體*</span><span class="sxs-lookup"><span data-stu-id="010ec-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="010ec-340">工作 3-新增 Web API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="010ec-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="010ec-341">當您建立 Web API 時，建立說明頁會很有説明，讓其他開發人員知道如何呼叫您的 API。</span><span class="sxs-lookup"><span data-stu-id="010ec-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="010ec-342">您可以手動建立和更新檔頁面，但最好是自動產生它們，以避免必須執行維護工作。</span><span class="sxs-lookup"><span data-stu-id="010ec-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="010ec-343">在這項工作中，您將使用 Nuget 套件，自動產生 Web API 說明頁面至解決方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="010ec-344">從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="010ec-344">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="010ec-345">在 [**套件管理員主控台**] 視窗中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="010ec-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="010ec-346">**WebApi. HelpPage**套件會安裝必要的元件，並將 [說明] 頁面的 MVC 視圖加入 [**區域/HelpPage** ] 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="010ec-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="010ec-347">![HelpPage 區域](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 區域")</span><span class="sxs-lookup"><span data-stu-id="010ec-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="010ec-348">*HelpPage 區域*</span><span class="sxs-lookup"><span data-stu-id="010ec-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="010ec-349">根據預設，說明頁面會有檔的預留位置字串。</span><span class="sxs-lookup"><span data-stu-id="010ec-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="010ec-350">您可以使用 XML 檔批註來建立檔。</span><span class="sxs-lookup"><span data-stu-id="010ec-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="010ec-351">若要啟用此功能，請開啟位於 [**區域/HelpPage/應用程式]\_[開始**] 資料夾中的**HelpPageConfig.cs**檔案，並取消批註下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="010ec-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="010ec-352">在**方案總管**中，以滑鼠右鍵按一下專案**MyHybridSite**，選取 [**屬性**]，然後按一下 [**組建**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="010ec-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="010ec-353">![[組建] 索引標籤](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "組建區段")</span><span class="sxs-lookup"><span data-stu-id="010ec-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="010ec-354">*[組建] 索引標籤*</span><span class="sxs-lookup"><span data-stu-id="010ec-354">*Build tab*</span></span>
5. <span data-ttu-id="010ec-355">在 [**輸出**] 底下，選取 [ **XML**檔檔]。</span><span class="sxs-lookup"><span data-stu-id="010ec-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="010ec-356">在 [編輯] 方塊中，輸入**應用程式\_Data/xml**。</span><span class="sxs-lookup"><span data-stu-id="010ec-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="010ec-357">![[組建] 索引標籤中的輸出區段](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "[組建] 索引標籤中的輸出區段")</span><span class="sxs-lookup"><span data-stu-id="010ec-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="010ec-358">*[組建] 索引標籤中的輸出區段*</span><span class="sxs-lookup"><span data-stu-id="010ec-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="010ec-359">按**CTRL** + **S**以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="010ec-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="010ec-360">從 [**控制器**] 資料夾中開啟**ApiPersonController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="010ec-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="010ec-361">在*GetPeople*方法簽章和 *//GET api/ApiPerson*批註之間輸入新的一行，然後輸入三個正斜線。</span><span class="sxs-lookup"><span data-stu-id="010ec-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="010ec-362">Visual Studio 會自動插入定義方法檔的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="010ec-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="010ec-363">加入摘要文字和*GetPeople*方法的傳回值。</span><span class="sxs-lookup"><span data-stu-id="010ec-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="010ec-364">看起來應該如下所示。</span><span class="sxs-lookup"><span data-stu-id="010ec-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="010ec-365">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="010ec-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="010ec-366">將 **/help**附加至網址列中的 URL，以流覽至 [說明] 頁面。</span><span class="sxs-lookup"><span data-stu-id="010ec-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="010ec-367">![ASP.NET Web API 說明頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 說明頁面")</span><span class="sxs-lookup"><span data-stu-id="010ec-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="010ec-368">*ASP.NET Web API 說明頁面*</span><span class="sxs-lookup"><span data-stu-id="010ec-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="010ec-369">頁面的主要內容是以控制器分組的 Api 資料表。</span><span class="sxs-lookup"><span data-stu-id="010ec-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="010ec-370">系統會使用**IApiExplorer**介面，以動態方式產生資料表專案。</span><span class="sxs-lookup"><span data-stu-id="010ec-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="010ec-371">如果您新增或更新 API 控制器，下一次建立應用程式時，資料表會自動更新。</span><span class="sxs-lookup"><span data-stu-id="010ec-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="010ec-372">[ **API** ] 欄會列出 HTTP 方法和相對 URI。</span><span class="sxs-lookup"><span data-stu-id="010ec-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="010ec-373">[**描述**] 資料行包含已從方法的檔中解壓縮的資訊。</span><span class="sxs-lookup"><span data-stu-id="010ec-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="010ec-374">請注意，您在方法定義上方新增的描述會顯示在 [描述] 欄中。</span><span class="sxs-lookup"><span data-stu-id="010ec-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="010ec-375">![API 方法描述](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 方法描述")</span><span class="sxs-lookup"><span data-stu-id="010ec-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="010ec-376">*API 方法描述*</span><span class="sxs-lookup"><span data-stu-id="010ec-376">*API method description*</span></span>
13. <span data-ttu-id="010ec-377">按一下其中一個 API 方法，流覽至包含詳細資訊的頁面，包括範例回應主體。</span><span class="sxs-lookup"><span data-stu-id="010ec-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="010ec-378">![詳細資訊頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "詳細資訊頁面")</span><span class="sxs-lookup"><span data-stu-id="010ec-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="010ec-379">*詳細資訊頁面*</span><span class="sxs-lookup"><span data-stu-id="010ec-379">*Detailed information page*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="010ec-380">總結</span><span class="sxs-lookup"><span data-stu-id="010ec-380">Summary</span></span>

<span data-ttu-id="010ec-381">藉由完成此實際操作實驗室，您已瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="010ec-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="010ec-382">使用 Visual Studio 2013 中的一個 ASP.NET 體驗建立新的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="010ec-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="010ec-383">將多個 ASP.NET 技術整合成一個單一專案</span><span class="sxs-lookup"><span data-stu-id="010ec-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="010ec-384">使用 ASP.NET 的架構，從您的模型類別產生 MVC 控制器和 views</span><span class="sxs-lookup"><span data-stu-id="010ec-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="010ec-385">產生 Web API 控制器，其使用非同步程式設計和透過 Entity Framework 的資料存取等功能</span><span class="sxs-lookup"><span data-stu-id="010ec-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="010ec-386">自動為您的控制器產生 Web API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="010ec-386">Automatically generate Web API Help Pages for your controllers</span></span>
