---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: 使用 ASP.NET MVC 搭配不同版本的 IIS （VB） |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何使用不同版本 Internet Information Services 的 ASP.NET MVC 和 URL 路由。 您將瞭解不同的策略 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: b754175c853c20eec6be3521376b62d62f33106d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581834"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a><span data-ttu-id="fe0fa-104">使用 ASP.NET MVC 與不同版本的 IIS (VB)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-104">Using ASP.NET MVC with Different Versions of IIS (VB)</span></span>

<span data-ttu-id="fe0fa-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fe0fa-106">在本教學課程中，您將瞭解如何使用不同版本 Internet Information Services 的 ASP.NET MVC 和 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="fe0fa-107">您會瞭解使用 ASP.NET MVC 搭配 IIS 7.0 （傳統模式）、IIS 6.0 和舊版 IIS 的不同策略。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="fe0fa-108">ASP.NET MVC 架構相依于 ASP.NET 路由，以將瀏覽器要求路由至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="fe0fa-109">為了充分利用 ASP.NET 路由，您可能必須在 web 伺服器上執行其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="fe0fa-110">這全都取決於應用程式的 Internet Information Services （IIS）版本和要求處理模式。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="fe0fa-111">以下是不同版本 IIS 的摘要：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="fe0fa-112">IIS 7.0 （整合模式）-不需要特殊設定即可使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="fe0fa-113">IIS 7.0 （傳統模式）-您需要執行特殊設定以使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="fe0fa-114">IIS 6.0 或以下-您需要執行特殊設定，才能使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="fe0fa-115">最新版本的 IIS 是7.5 版（在 Win7 上）。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="fe0fa-116">Iis 的 iis 7 包含在 Windows Server 2008 和 VISTA/SP1 及更新版本中。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="fe0fa-117">您也可以在任何版本的 Vista 作業系統（Home Basic 除外）上安裝 IIS 7.0 （請參閱[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="fe0fa-118">IIS 7.0 支援兩種模式來處理要求。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="fe0fa-119">您可以使用整合模式或傳統模式。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="fe0fa-120">在整合模式中使用 IIS 7.0 時，您不需要執行任何特殊的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="fe0fa-121">不過，在傳統模式中使用 IIS 7.0 時，您必須執行其他設定。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="fe0fa-122">Microsoft Windows Server 2003 包含 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="fe0fa-123">當您使用 Windows Server 2003 作業系統時，無法將 IIS 6.0 升級至 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="fe0fa-124">使用 IIS 6.0 時，您必須執行額外的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="fe0fa-125">Microsoft Windows XP Professional 包含 IIS 5.1。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="fe0fa-126">使用 IIS 5.1 時，您必須執行額外的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="fe0fa-127">最後，Microsoft Windows 2000 和 Microsoft Windows 2000 Professional 包含 IIS 5.0。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="fe0fa-128">使用 IIS 5.0 時，您必須執行額外的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="fe0fa-129">整合式與傳統模式</span><span class="sxs-lookup"><span data-stu-id="fe0fa-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="fe0fa-130">IIS 7.0 可以使用兩種不同的要求處理模式來處理要求：整合式和傳統。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="fe0fa-131">整合模式可提供更佳的效能和更多功能。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="fe0fa-132">包括傳統模式，以提供與舊版 IIS 的回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="fe0fa-133">要求處理模式取決於應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="fe0fa-134">藉由判斷與應用程式相關聯的應用程式集區，您可以判斷特定 web 應用程式正在使用哪種處理模式。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="fe0fa-135">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-135">Follow these steps:</span></span>

1. <span data-ttu-id="fe0fa-136">啟動 Internet Information Services 管理員</span><span class="sxs-lookup"><span data-stu-id="fe0fa-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="fe0fa-137">在 [連線] 視窗中，選取應用程式</span><span class="sxs-lookup"><span data-stu-id="fe0fa-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="fe0fa-138">在 [動作] 視窗中，按一下 [**基本設定**] 連結以開啟 [編輯應用程式] 對話方塊（請參閱 [圖 1]）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="fe0fa-139">記下所選的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="fe0fa-140">根據預設，IIS 會設定為支援兩個應用程式集區： **DefaultAppPool**和**傳統 .net AppPool**。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="fe0fa-141">如果已選取 [DefaultAppPool]，則您的應用程式會以整合式要求處理模式執行。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="fe0fa-142">如果選取了傳統的 .NET AppPool，您的應用程式就會在傳統要求處理模式下執行。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="fe0fa-143">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span></span>

<span data-ttu-id="fe0fa-144">**圖 1**：偵測要求處理模式（[按一下以查看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span></span>

<span data-ttu-id="fe0fa-145">請注意，您可以在 [編輯應用程式] 對話方塊中修改要求處理模式。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="fe0fa-146">按一下 [選取] 按鈕，並變更與應用程式相關聯的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="fe0fa-147">請注意，將 ASP.NET 應用程式從 [傳統] 變更為 [整合模式] 時，會發生相容性問題。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="fe0fa-148">如需詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="fe0fa-149">在 Windows Vista 和 Windows Server 上將 ASP.NET 1.1 升級至 IIS 7.0 2008-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>

- <span data-ttu-id="fe0fa-150">ASP.NET 與 IIS 7.0 整合- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="fe0fa-151">如果 ASP.NET 應用程式正在使用 DefaultAppPool，則您不需要執行任何額外的步驟，即可讓 ASP.NET 路由（因而 ASP.NET MVC）得以正常操作。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="fe0fa-152">不過，如果 ASP.NET 應用程式設定為使用傳統的 .NET AppPool，然後繼續閱讀，則您會有更多的工作要執行。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="fe0fa-153">搭配舊版 IIS 使用 ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="fe0fa-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="fe0fa-154">如果您需要使用比 IIS 7.0 更舊的 IIS 版本的 ASP.NET MVC，或需要在傳統模式中使用 IIS 7.0，則您有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="fe0fa-155">首先，您可以修改路由表以使用副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="fe0fa-156">例如，您會要求類似/Store.aspx/Details. 的 URL，而不是要求/Store/Details 之類的 URL。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="fe0fa-157">第二個選項是建立一個名為*萬用字元腳本對應*的東西。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="fe0fa-158">萬用字元腳本對應可讓您將每個要求對應到 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="fe0fa-159">如果您沒有 web 伺服器的存取權（例如，您的 ASP.NET MVC 應用程式是由網際網路服務提供者所裝載），則您必須使用第一個選項。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="fe0fa-160">如果您不想修改 Url 的外觀，而且可以存取您的 web 伺服器，則可以使用第二個選項。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="fe0fa-161">我們將在下列各節中詳細探討每個選項。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="fe0fa-162">將擴充功能新增至路由表</span><span class="sxs-lookup"><span data-stu-id="fe0fa-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="fe0fa-163">取得 ASP.NET 路由以使用舊版 IIS 的最簡單方式，就是修改 global.asax 檔案中的路由表。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="fe0fa-164">[清單 1] 中的預設和未修改的 global.asax 檔案會設定一個名為「預設路由」的路由。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="fe0fa-165">**清單 1-global.asax （未修改）**</span><span class="sxs-lookup"><span data-stu-id="fe0fa-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

<span data-ttu-id="fe0fa-166">[清單 1] 中設定的預設路由可讓您路由 Url，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="fe0fa-167">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="fe0fa-167">/Home/Index</span></span>

<span data-ttu-id="fe0fa-168">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="fe0fa-168">/Product/Details/3</span></span>

<span data-ttu-id="fe0fa-169">/Product</span><span class="sxs-lookup"><span data-stu-id="fe0fa-169">/Product</span></span>

<span data-ttu-id="fe0fa-170">可惜的是，較舊版本的 IIS 不會將這些要求傳遞至 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="fe0fa-171">因此，這些要求將不會路由傳送至控制器。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="fe0fa-172">例如，如果您對 URL/Home/Index 提出瀏覽器要求，則會出現 [圖 2] 中的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="fe0fa-173">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span></span>

<span data-ttu-id="fe0fa-174">**圖 2**：收到404找不到錯誤（[按一下以觀看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span></span>

<span data-ttu-id="fe0fa-175">較舊版本的 IIS 只會將特定要求對應至 ASP.NET framework。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="fe0fa-176">要求必須是具有正確副檔名的 URL。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="fe0fa-177">例如，/SomePage.aspx 的要求會對應至 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="fe0fa-178">不過，/SomePage.htm 的要求不會。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="fe0fa-179">因此，若要讓 ASP.NET 路由能夠正常執行，我們必須修改預設路由，使其包含對應至 ASP.NET 架構的副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="fe0fa-180">這是使用名為 `registermvc.wsf`的腳本來完成。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="fe0fa-181">它隨附于 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`中的 ASP.NET MVC 1 版本，但從 ASP.NET 2 開始，此腳本已移至 ASP.NET 的未來，可從[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)取得。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="fe0fa-182">執行此腳本會向 IIS 註冊新的. mvc 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="fe0fa-183">註冊 mvc 副檔名之後，您可以修改 global.asax 檔案中的路由，讓路由使用 mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="fe0fa-184">[清單 2] 中修改的 global.asax 檔案可與舊版的 IIS 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="fe0fa-185">**清單 2-global.asax （使用延伸模組修改）**</span><span class="sxs-lookup"><span data-stu-id="fe0fa-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

<span data-ttu-id="fe0fa-186">重要事項：請記得在變更 global.asax 檔案之後，再次建立您的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-186">Important: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="fe0fa-187">[清單 2] 中的 global.asax 檔案有兩項重要的變更。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="fe0fa-188">現在 global.asax 中定義了兩個路由。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="fe0fa-189">預設路由的 URL 模式（第一個路由）現在看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="fe0fa-190">{controller}. mvc/{action}/{id}</span><span class="sxs-lookup"><span data-stu-id="fe0fa-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="fe0fa-191">新增 mvc 副檔名會變更 ASP.NET 路由模組所攔截的檔案類型。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="fe0fa-192">透過這項變更，ASP.NET MVC 應用程式現在會路由傳送如下的要求：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="fe0fa-193">/Home.mvc/Index/</span><span class="sxs-lookup"><span data-stu-id="fe0fa-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="fe0fa-194">/Product.mvc/Details/3</span><span class="sxs-lookup"><span data-stu-id="fe0fa-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="fe0fa-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="fe0fa-195">/Product.mvc/</span></span>

<span data-ttu-id="fe0fa-196">第二個路由（根路由）是新的。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="fe0fa-197">根路由的此 URL 模式是空字串。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="fe0fa-198">需要此路由，才能比對對您的應用程式根目錄提出的要求。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="fe0fa-199">例如，根路由會符合如下所示的要求：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="fe0fa-200">對您的路由表進行這些修改之後，您必須確定應用程式中的所有連結都與這些新的 URL 模式相容。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="fe0fa-201">換句話說，請確定您所有的連結都包含 mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="fe0fa-202">如果您使用 Html.actionlink （） helper 方法來產生連結，則不需要進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="fe0fa-203">除了使用 registermvc，您也可以將新的延伸模組新增至 IIS，並手動對應至 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="fe0fa-204">自行新增擴充功能時，請確定未核取標示為 [**確認檔案存在**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="fe0fa-205">主控伺服器</span><span class="sxs-lookup"><span data-stu-id="fe0fa-205">Hosted Server</span></span>

<span data-ttu-id="fe0fa-206">您不一定可以存取您的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-206">You don't always have access to your web server.</span></span> <span data-ttu-id="fe0fa-207">例如，如果您使用網際網路主控提供者裝載 ASP.NET MVC 應用程式，則您不一定會有 IIS 的存取權。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="fe0fa-208">在這種情況下，您應該使用對應至 ASP.NET 架構的其中一個現有副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="fe0fa-209">對應至 ASP.NET 的副檔名範例包括 .aspx、axd 和 ashx 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="fe0fa-210">例如，在 [清單 3] 中修改的 global.asax 檔案使用 .aspx 副檔名，而不是 mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="fe0fa-211">**清單 3-global.asax （以 .aspx 副檔名修改）**</span><span class="sxs-lookup"><span data-stu-id="fe0fa-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

<span data-ttu-id="fe0fa-212">[清單 3] 中的 global.asax 檔案與先前的 global.asax 檔案完全相同，不同之處在于它使用 .aspx 副檔名，而不是 mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="fe0fa-213">您不需要在遠端 web 伺服器上執行任何安裝程式，就能使用 .aspx 副檔名。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="fe0fa-214">建立萬用字元腳本對應</span><span class="sxs-lookup"><span data-stu-id="fe0fa-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="fe0fa-215">如果您不想要修改 ASP.NET MVC 應用程式的 Url，而且可以存取您的 web 伺服器，則您會有額外的選項。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="fe0fa-216">您可以建立萬用字元腳本對應，將 web 伺服器的所有要求對應到 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="fe0fa-217">如此一來，您就可以使用預設的 ASP.NET MVC 路由表搭配 IIS 7.0 （在傳統模式中）或 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="fe0fa-218">請注意，此選項會使 IIS 攔截對網頁伺服器提出的每個要求。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="fe0fa-219">這包括對影像、傳統 ASP 網頁和 HTML 網頁的要求。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="fe0fa-220">因此，啟用萬用字元腳本對應至 ASP.NET 會對效能造成影響。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="fe0fa-221">以下是針對 IIS 7.0 啟用萬用字元腳本對應的方式：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="fe0fa-222">在 [連接] 視窗中選取您的應用程式</span><span class="sxs-lookup"><span data-stu-id="fe0fa-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="fe0fa-223">請確定已選取 [**功能**] 視圖</span><span class="sxs-lookup"><span data-stu-id="fe0fa-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="fe0fa-224">按兩下 [**處理常式**對應] 按鈕</span><span class="sxs-lookup"><span data-stu-id="fe0fa-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="fe0fa-225">按一下 [**新增萬用字元腳本對應**] 連結（請參閱 [圖 3]）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="fe0fa-226">輸入 aspnet\_isapi .dll 檔案的路徑（您可以從 PageHandlerFactory 腳本對應複製此路徑）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="fe0fa-227">輸入 MVC 的名稱</span><span class="sxs-lookup"><span data-stu-id="fe0fa-227">Enter the name MVC</span></span>
7. <span data-ttu-id="fe0fa-228">按一下 [**確定]** 按鈕</span><span class="sxs-lookup"><span data-stu-id="fe0fa-228">Click the **OK** button</span></span>

<span data-ttu-id="fe0fa-229">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span></span>

<span data-ttu-id="fe0fa-230">**圖 3**：使用 IIS 7.0 建立萬用字元腳本對應（[按一下以觀看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span></span>

<span data-ttu-id="fe0fa-231">請遵循下列步驟，以使用 IIS 6.0 建立萬用字元腳本對應：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="fe0fa-232">以滑鼠右鍵按一下網站，然後選取 [屬性]</span><span class="sxs-lookup"><span data-stu-id="fe0fa-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="fe0fa-233">選取 [**主目錄**] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="fe0fa-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="fe0fa-234">按一下 [**設定**] 按鈕</span><span class="sxs-lookup"><span data-stu-id="fe0fa-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="fe0fa-235">選取 [**對應**] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="fe0fa-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="fe0fa-236">按一下 [**插入**] 按鈕（請參閱 [圖 4]）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="fe0fa-237">將 aspnet\_的路徑貼到 [可執行檔] 欄位中（您可以從 .aspx 檔案的腳本對應複製此路徑）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="fe0fa-238">取消核取標示為 [**確認檔案存在**] 的核取方塊</span><span class="sxs-lookup"><span data-stu-id="fe0fa-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="fe0fa-239">按一下 [**確定]** 按鈕</span><span class="sxs-lookup"><span data-stu-id="fe0fa-239">Click the **OK** button</span></span>

<span data-ttu-id="fe0fa-240">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span></span>

<span data-ttu-id="fe0fa-241">**圖 4**：使用 IIS 6.0 建立萬用字元腳本對應（[按一下以觀看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span></span>

<span data-ttu-id="fe0fa-242">啟用萬用字元腳本對應之後，您必須修改 global.asax 檔案中的路由表，使其包含根路由。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="fe0fa-243">否則，當您對應用程式的根頁面提出要求時，您會看到 [圖 5] 中的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="fe0fa-244">您可以使用 [清單 4] 中已修改的 global.asax 檔案。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="fe0fa-245">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="fe0fa-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span></span>

<span data-ttu-id="fe0fa-246">**圖 5**：遺漏根路由錯誤（[按一下以查看完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="fe0fa-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span></span>

<span data-ttu-id="fe0fa-247">**清單 4-global.asax （使用根路由修改）**</span><span class="sxs-lookup"><span data-stu-id="fe0fa-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

<span data-ttu-id="fe0fa-248">啟用 IIS 7.0 或 IIS 6.0 的萬用字元腳本對應之後，您可以建立與預設路由表搭配使用的要求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fe0fa-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="fe0fa-249">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="fe0fa-249">/Home/Index</span></span>

<span data-ttu-id="fe0fa-250">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="fe0fa-250">/Product/Details/3</span></span>

<span data-ttu-id="fe0fa-251">/Product</span><span class="sxs-lookup"><span data-stu-id="fe0fa-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="fe0fa-252">總結</span><span class="sxs-lookup"><span data-stu-id="fe0fa-252">Summary</span></span>

<span data-ttu-id="fe0fa-253">本教學課程的目的是要說明在使用舊版 IIS （或傳統模式的 IIS 7.0）時，您可以如何使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="fe0fa-254">我們討論了兩種取得 ASP.NET 路由以使用舊版 IIS 的方法：修改預設路由表或建立萬用字元腳本對應。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="fe0fa-255">第一個選項會要求您修改 ASP.NET MVC 應用程式中使用的 Url。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="fe0fa-256">第一個選項的其中一個非常重要的優點是，您不需要存取 web 伺服器，就可以修改路由表。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="fe0fa-257">這表示您可以使用這個第一個選項，即使是在裝載與網際網路主控公司的 ASP.NET MVC 應用程式時也一樣。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="fe0fa-258">第二個選項是建立萬用字元腳本對應。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="fe0fa-259">第二個選項的優點是您不需要修改 Url。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="fe0fa-260">第二個選項的缺點是，它可能會影響 ASP.NET MVC 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="fe0fa-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fe0fa-261">上一篇</span><span class="sxs-lookup"><span data-stu-id="fe0fa-261">Previous</span></span>](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
