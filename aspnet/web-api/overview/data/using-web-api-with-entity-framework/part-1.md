---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: 搭配 Entity Framework 6 使用 Web API 2 |Microsoft Docs
author: MikeWasson
description: 本教學課程將告訴您使用 ASP.NET Web API 後端建立 web 應用程式的基本概念。 本教學課程使用 Entity Framework 6 來進行資料佈局 。
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622476"
---
# <a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="d8545-104">使用 Web API 2 和 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d8545-104">Using Web API 2 with Entity Framework 6</span></span>

[<span data-ttu-id="d8545-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="d8545-105">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="d8545-106">本教學課程會教您使用 ASP.NET Web API 後端建立 web 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="d8545-106">This tutorial teaches you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="d8545-107">本教學課程使用資料層的 Entity Framework 6，以及用戶端 JavaScript 應用程式的挖式 .js。</span><span class="sxs-lookup"><span data-stu-id="d8545-107">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="d8545-108">本教學課程也會說明如何將應用程式部署至 Azure App Service Web Apps。</span><span class="sxs-lookup"><span data-stu-id="d8545-108">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d8545-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="d8545-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="d8545-110">Web API 2。1</span><span class="sxs-lookup"><span data-stu-id="d8545-110">Web API 2.1</span></span>
> - <span data-ttu-id="d8545-111">Visual Studio 2017 （請[在這裡](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下載 Visual Studio 2017）</span><span class="sxs-lookup"><span data-stu-id="d8545-111">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="d8545-112">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d8545-112">Entity Framework 6</span></span>
> - <span data-ttu-id="d8545-113">.NET 4.7</span><span class="sxs-lookup"><span data-stu-id="d8545-113">.NET 4.7</span></span>
> - <span data-ttu-id="d8545-114">[挖的 .js](http://knockoutjs.com/) 3。1</span><span class="sxs-lookup"><span data-stu-id="d8545-114">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>

<span data-ttu-id="d8545-115">本教學課程使用 ASP.NET Web API 2 與 Entity Framework 6 來建立 Web 應用程式，以操作後端資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8545-115">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="d8545-116">以下是您將建立之應用程式的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="d8545-116">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="d8545-117">應用程式會使用單一頁面應用程式（SPA）設計。</span><span class="sxs-lookup"><span data-stu-id="d8545-117">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="d8545-118">「單頁應用程式」是 web 應用程式的一般詞彙，它會載入單一 HTML 頁面，然後動態更新頁面，而不是載入新的頁面。</span><span class="sxs-lookup"><span data-stu-id="d8545-118">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="d8545-119">載入初始頁面之後，應用程式會透過 AJAX 要求與伺服器交談。</span><span class="sxs-lookup"><span data-stu-id="d8545-119">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="d8545-120">AJAX 要求會傳回 JSON 資料，應用程式會使用它來更新 UI。</span><span class="sxs-lookup"><span data-stu-id="d8545-120">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="d8545-121">AJAX 並不是新的，但目前有 JavaScript 架構可讓您更輕鬆地建立和維護大型的 SPA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8545-121">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="d8545-122">本教學課程使用了[挖的 .js](http://knockoutjs.com/)，但是您可以使用任何 JavaScript 用戶端架構。</span><span class="sxs-lookup"><span data-stu-id="d8545-122">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="d8545-123">以下是此應用程式的主要組建區塊：</span><span class="sxs-lookup"><span data-stu-id="d8545-123">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="d8545-124">ASP.NET MVC 會建立 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="d8545-124">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="d8545-125">ASP.NET Web API 會處理 AJAX 要求並傳回 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="d8545-125">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="d8545-126">挖式 .js 資料-將 HTML 元素系結至 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="d8545-126">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="d8545-127">Entity Framework 與資料庫交談。</span><span class="sxs-lookup"><span data-stu-id="d8545-127">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="d8545-128">請參閱此應用程式在 Azure 上執行</span><span class="sxs-lookup"><span data-stu-id="d8545-128">See this app running on Azure</span></span>

<span data-ttu-id="d8545-129">您是否想要查看已完成的網站以即時 web 應用程式的形式執行？</span><span class="sxs-lookup"><span data-stu-id="d8545-129">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="d8545-130">您可以選取下列按鈕，將完整版的應用程式部署到您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8545-130">You can deploy a complete version of the app to your Azure account by selecting the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="d8545-131">您需要 Azure 帳戶，才能將此解決方案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="d8545-131">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="d8545-132">如果您還沒有帳戶，您可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="d8545-132">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="d8545-133">[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。</span><span class="sxs-lookup"><span data-stu-id="d8545-133">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="d8545-134">[啟用 msdn 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-您的 msdn 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="d8545-134">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="d8545-135">建立專案</span><span class="sxs-lookup"><span data-stu-id="d8545-135">Create the project</span></span>

<span data-ttu-id="d8545-136">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d8545-136">Open Visual Studio.</span></span> <span data-ttu-id="d8545-137">從 [**檔案**] 功能表中，選取 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="d8545-137">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="d8545-138">（或選取 [開始] 頁面上的 [**新增專案**]）。</span><span class="sxs-lookup"><span data-stu-id="d8545-138">(Or select **New Project** on the Start page.)</span></span>

<span data-ttu-id="d8545-139">在 **新增專案** 對話方塊中，選取左窗格中的  **web** ，然後在中間窗格中**ASP.NET web 應用程式（.NET Framework）** 。</span><span class="sxs-lookup"><span data-stu-id="d8545-139">In the **New Project** dialog, select **Web** in the left pane and **ASP.NET Web Application (.NET Framework)** in the middle pane.</span></span> <span data-ttu-id="d8545-140">將專案命名為**BookService** ，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="d8545-140">Name the project **BookService** and select **OK**.</span></span>

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

<span data-ttu-id="d8545-141">在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **Web API** ] 範本。</span><span class="sxs-lookup"><span data-stu-id="d8545-141">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

<span data-ttu-id="d8545-142">選取 [確定] 建立專案。</span><span class="sxs-lookup"><span data-stu-id="d8545-142">Select **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="d8545-143">設定 Azure 設定（選擇性）</span><span class="sxs-lookup"><span data-stu-id="d8545-143">Configure Azure settings (optional)</span></span>

<span data-ttu-id="d8545-144">建立專案之後，您可以隨時選擇部署至 Azure App Service Web Apps。</span><span class="sxs-lookup"><span data-stu-id="d8545-144">After you create the project, you can choose to deploy to Azure App Service Web Apps at any time.</span></span> 

1. <span data-ttu-id="d8545-145">在方案總管中，以滑鼠右鍵按一下您的專案，然後選取 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="d8545-145">In Solution Explorer, right-click on your project and select **Publish**.</span></span>

2. <span data-ttu-id="d8545-146">在出現的視窗中，選取 [**啟動**]。</span><span class="sxs-lookup"><span data-stu-id="d8545-146">In the window that appears, select **Start**.</span></span> <span data-ttu-id="d8545-147">[**挑選發行目標**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="d8545-147">The **Pick a publish target** dialog box appears.</span></span>

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. <span data-ttu-id="d8545-148">選取 [建立設定檔]。</span><span class="sxs-lookup"><span data-stu-id="d8545-148">Select **Create Profile**.</span></span> <span data-ttu-id="d8545-149">[建立 App Service] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="d8545-149">The **Create App Service** dialog box appears.</span></span>

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   <span data-ttu-id="d8545-150">接受預設值，或為應用程式名稱、資源群組、主控方案、Azure 訂用帳戶和地理區域輸入不同的值。</span><span class="sxs-lookup"><span data-stu-id="d8545-150">Accept the defaults, or enter different values for the application name, resource group, hosting plan, Azure subscription, and geographical region.</span></span> 

4. <span data-ttu-id="d8545-151">選取 **[建立 SQL database**]。</span><span class="sxs-lookup"><span data-stu-id="d8545-151">Select **Create a SQL database**.</span></span> <span data-ttu-id="d8545-152">[**設定 SQL Server** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="d8545-152">The **Configure SQL Server** dialog box appears.</span></span> 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   <span data-ttu-id="d8545-153">接受預設值，或輸入不同的值。</span><span class="sxs-lookup"><span data-stu-id="d8545-153">Accept the defaults or enter different values.</span></span> <span data-ttu-id="d8545-154">輸入新資料庫的**系統管理員使用者名稱**和**系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="d8545-154">Enter an **Administrator Username** and **Administrator Password** for your new database.</span></span> <span data-ttu-id="d8545-155">當您完成時，請選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="d8545-155">Select **OK** when you're done.</span></span> <span data-ttu-id="d8545-156">[**建立 App Service** ] 頁面隨即重新出現。</span><span class="sxs-lookup"><span data-stu-id="d8545-156">The **Create App Service** page reappears.</span></span>

5. <span data-ttu-id="d8545-157">選取 [**建立**] 以建立您的設定檔。</span><span class="sxs-lookup"><span data-stu-id="d8545-157">Select **Create** to create your profile.</span></span> <span data-ttu-id="d8545-158">右下角會出現一則訊息，指出部署正在進行中。</span><span class="sxs-lookup"><span data-stu-id="d8545-158">A message appears in the lower-right corner indicating that deployment is in progress.</span></span> <span data-ttu-id="d8545-159">一小段時間之後，[**發行**] 視窗隨即重新出現。</span><span class="sxs-lookup"><span data-stu-id="d8545-159">After a short while, the **Publish** window reappears.</span></span>

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    <span data-ttu-id="d8545-160">您建立用來部署應用程式的設定檔現已推出。</span><span class="sxs-lookup"><span data-stu-id="d8545-160">The profile you created to deploy the app is now available.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="d8545-161">下一個</span><span class="sxs-lookup"><span data-stu-id="d8545-161">Next</span></span>](part-2.md)
