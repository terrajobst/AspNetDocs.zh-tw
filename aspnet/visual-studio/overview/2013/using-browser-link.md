---
uid: visual-studio/overview/2013/using-browser-link
title: 在 Visual Studio 2013 中使用瀏覽器連結 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622903"
---
# <a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="8c4ed-102">在 Visual Studio 2013 中使用瀏覽器連結</span><span class="sxs-lookup"><span data-stu-id="8c4ed-102">Using Browser Link in Visual Studio 2013</span></span>

<span data-ttu-id="8c4ed-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8c4ed-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8c4ed-104">瀏覽器連結是 Visual Studio 2013 中的一項新功能，可在開發環境與一或多個網頁瀏覽器之間建立通道。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="8c4ed-105">您可以使用瀏覽器連結，一次在數個瀏覽器中重新整理 web 應用程式，這對於跨瀏覽器測試很有用。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="8c4ed-106">瀏覽器重新整理</span><span class="sxs-lookup"><span data-stu-id="8c4ed-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="8c4ed-107">查看瀏覽器連結儀表板</span><span class="sxs-lookup"><span data-stu-id="8c4ed-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="8c4ed-108">啟用靜態 HTML 檔案的瀏覽器連結</span><span class="sxs-lookup"><span data-stu-id="8c4ed-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="8c4ed-109">停用瀏覽器連結</span><span class="sxs-lookup"><span data-stu-id="8c4ed-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="8c4ed-110">它如何運作？</span><span class="sxs-lookup"><span data-stu-id="8c4ed-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="8c4ed-111">瀏覽器重新整理</span><span class="sxs-lookup"><span data-stu-id="8c4ed-111">Browser Refresh</span></span>

<span data-ttu-id="8c4ed-112">使用瀏覽器重新整理時，您可以透過瀏覽器連結來重新整理連線到 Visual Studio 的多個瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="8c4ed-113">若要使用瀏覽器重新整理，請先使用任何專案範本來建立 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="8c4ed-114">按 F5 或按一下工具列中的箭號圖示，以對應用程式進行 Debug：</span><span class="sxs-lookup"><span data-stu-id="8c4ed-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="8c4ed-115">您也可以使用下拉式清單來選取要進行偵錯工具的特定瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="8c4ed-116">若要使用多個瀏覽器進行調試，請選取 **[流覽方式]** 。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="8c4ed-117">在 [**流覽方式**] 對話方塊中，按住 CTRL 鍵以選取一個以上的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="8c4ed-118">按一下 **[流覽]** ，以選取的瀏覽器進行 debug。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="8c4ed-119">瀏覽器連結也適用于從外部 Visual Studio 啟動瀏覽器，並流覽至應用程式 URL 的情況。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="8c4ed-120">瀏覽器連結控制項位於具有圓形箭號圖示的下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="8c4ed-121">箭號圖示是 [重新整理 **] 按鈕。**</span><span class="sxs-lookup"><span data-stu-id="8c4ed-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="8c4ed-122">若要查看哪些瀏覽器已連接，請在進行調試時將滑鼠停留在 [重新整理 **] 按鈕上方**。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="8c4ed-123">[已連接的瀏覽器] 會顯示在工具提示視窗中。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="8c4ed-124">若要重新整理已連線的瀏覽器，請按一下 [重新整理 **] 按鈕，** 或按 CTRL + ALT + ENTER。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="8c4ed-125">例如，下列螢幕擷取畫面顯示我使用 MVC 5 專案範本所建立的 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="8c4ed-126">您可以在頂端的兩個瀏覽器中看到應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="8c4ed-127">在底部，專案會在 Visual Studio 中開啟。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="8c4ed-128">在 Visual Studio 中，我變更了首頁的 &lt;h1&gt; 標題：</span><span class="sxs-lookup"><span data-stu-id="8c4ed-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="8c4ed-129">當我按一下 [重新整理 **] 按鈕時**，變更會同時出現在這兩個瀏覽器視窗中：</span><span class="sxs-lookup"><span data-stu-id="8c4ed-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="8c4ed-130">**備註**</span><span class="sxs-lookup"><span data-stu-id="8c4ed-130">**Notes**</span></span>

- <span data-ttu-id="8c4ed-131">若要啟用瀏覽器連結，請在專案的 Web.config 檔案中，于[&lt;編譯&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)元素中設定 `debug=true`。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="8c4ed-132">應用程式必須在 localhost 上執行。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="8c4ed-133">應用程式必須以 .NET 4.0 或更新版本為目標。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="8c4ed-134">查看瀏覽器連結儀表板</span><span class="sxs-lookup"><span data-stu-id="8c4ed-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="8c4ed-135">瀏覽器連結儀表板會顯示瀏覽器連結連接的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="8c4ed-136">若要查看儀表板，請選取瀏覽器連結下拉式功能表（[重新整理 **] 按鈕旁邊的小**箭號）。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="8c4ed-137">然後按一下 [**瀏覽器連結儀表板**]。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="8c4ed-138">儀表板會列出已連線的瀏覽器，以及每個瀏覽器導覽的 URL。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="8c4ed-139">[**必要條件**] 區段會顯示啟用該專案的瀏覽器連結所需的任何步驟。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="8c4ed-140">例如，下列螢幕擷取畫面顯示一個專案，其中 Web.config 檔案中的 "debug" 設定為 false。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="8c4ed-141">啟用靜態 HTML 檔案的瀏覽器連結</span><span class="sxs-lookup"><span data-stu-id="8c4ed-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="8c4ed-142">若要啟用靜態 HTML 檔案的瀏覽器連結，請將下列程式新增至您的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="8c4ed-143">基於效能考慮，請在發行專案時移除此設定。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="8c4ed-144">停用瀏覽器連結</span><span class="sxs-lookup"><span data-stu-id="8c4ed-144">Disabling Browser Link</span></span>

<span data-ttu-id="8c4ed-145">預設會啟用瀏覽器連結。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="8c4ed-146">有幾種方式可以停用它：</span><span class="sxs-lookup"><span data-stu-id="8c4ed-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="8c4ed-147">在 [瀏覽器連結] 下拉式功能表中，取消核取 [**啟用瀏覽器連結**]。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="8c4ed-148">在 web.config 檔案中，于 appSettings 區段中新增名為 "vs： EnableBrowserLink" 的索引鍵，其值為 "false"。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="8c4ed-149">在 web.config 檔案中，將 debug 設為 false。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="8c4ed-150">它如何運作？</span><span class="sxs-lookup"><span data-stu-id="8c4ed-150">How Does It Work?</span></span>

<span data-ttu-id="8c4ed-151">瀏覽器連結會使用[SignalR](../../../signalr/index.md)來建立 Visual Studio 與瀏覽器之間的通道。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="8c4ed-152">啟用瀏覽器連結時，Visual Studio 會作為多個用戶端（瀏覽器）可以連接的 SignalR 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="8c4ed-153">瀏覽器連結也會向 ASP.NET 註冊 HTTP 模組。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="8c4ed-154">此模組會將特殊的 &lt;腳本&gt; 參考插入伺服器中的每個頁面要求。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="8c4ed-155">您可以在瀏覽器中選取 [View source]，以查看腳本參考。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="8c4ed-156">您的原始程式檔不會遭到修改。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-156">Your source files are not modified.</span></span> <span data-ttu-id="8c4ed-157">HTTP 模組會動態插入腳本參考。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="8c4ed-158">因為瀏覽器端程式碼是所有的 JavaScript，所以它適用于所有[SignalR 支援](../../../signalr/overview/getting-started/supported-platforms.md)的瀏覽器，而不需要任何瀏覽器外掛程式。</span><span class="sxs-lookup"><span data-stu-id="8c4ed-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
