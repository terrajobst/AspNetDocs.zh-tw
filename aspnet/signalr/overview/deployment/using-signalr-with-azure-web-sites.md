---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: 在 Azure App Service 中使用具有 Web Apps 的 SignalR |Microsoft Docs
author: bradygaster
description: 本檔說明如何設定在 Microsoft Azure 上執行的 SignalR 應用程式。 教學課程中所使用的軟體版本 Visual Studio 2013 或 Vis 。
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558699"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="77320-104">在 Azure App Service 中搭配 Web 應用程式使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="77320-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="77320-105">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="77320-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="77320-106">本檔說明如何設定在 Microsoft Azure 上執行的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77320-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="77320-107">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="77320-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="77320-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)或 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="77320-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="77320-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="77320-109">.NET 4.5</span></span>
> - <span data-ttu-id="77320-110">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="77320-110">SignalR version 2</span></span>
> - <span data-ttu-id="77320-111">適用于 Visual Studio 2013 或2012的 Azure SDK 2。3</span><span class="sxs-lookup"><span data-stu-id="77320-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="77320-112">問題與意見</span><span class="sxs-lookup"><span data-stu-id="77320-112">Questions and comments</span></span>
>
> <span data-ttu-id="77320-113">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="77320-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="77320-114">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)、 [StackOverflow.com](http://stackoverflow.com/)或[Microsoft Azure 論壇](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)。</span><span class="sxs-lookup"><span data-stu-id="77320-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="77320-115">目錄</span><span class="sxs-lookup"><span data-stu-id="77320-115">Table of Contents</span></span>

- [<span data-ttu-id="77320-116">簡介</span><span class="sxs-lookup"><span data-stu-id="77320-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="77320-117">將 SignalR Web 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="77320-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="77320-118">在 Azure App Service 上啟用 Websocket</span><span class="sxs-lookup"><span data-stu-id="77320-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="77320-119">使用 Azure Redis 快取背板</span><span class="sxs-lookup"><span data-stu-id="77320-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="77320-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77320-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="77320-121">簡介</span><span class="sxs-lookup"><span data-stu-id="77320-121">Introduction</span></span>

<span data-ttu-id="77320-122">ASP.NET SignalR 可用來在伺服器與 web 或 .NET 用戶端之間帶入新的互動層級。</span><span class="sxs-lookup"><span data-stu-id="77320-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="77320-123">在 Azure 中託管時，SignalR 應用程式可以利用在雲端中執行的高可用性、可擴充且高效能的環境。</span><span class="sxs-lookup"><span data-stu-id="77320-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="77320-124">將 SignalR Web 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="77320-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="77320-125">SignalR 不會新增任何特定的複雜性，將應用程式部署至 Azure，而不是部署到內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="77320-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="77320-126">使用 SignalR 的應用程式可以裝載于 Azure 中，而不需要變更設定或其他設定（不過，針對 Websocket 支援，請參閱下列[Azure App Service 上的啟用 websocket](#websocket) ）。在本教學課程中，您會將[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中建立的應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="77320-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="77320-127">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="77320-127">**Prerequisites**</span></span>

- <span data-ttu-id="77320-128">Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="77320-128">Visual Studio 2013.</span></span> <span data-ttu-id="77320-129">如果您沒有 Visual Studio，則 Azure SDK 的安裝中會包含適用于 Web 的 Visual Studio 2013 Express。</span><span class="sxs-lookup"><span data-stu-id="77320-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="77320-130">適用于 Visual Studio 2012 的[AZURE sdk 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409)或[azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)。</span><span class="sxs-lookup"><span data-stu-id="77320-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="77320-131">若要完成此教學課程，您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77320-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="77320-132">您可以[啟用 MSDN 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)，或[註冊試用版訂用](https://azure.microsoft.com/pricing/free-trial/)帳戶。</span><span class="sxs-lookup"><span data-stu-id="77320-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="77320-133">將 SignalR web 應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="77320-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="77320-134">完成[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程，或從程式[代碼庫](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)下載已完成的專案。</span><span class="sxs-lookup"><span data-stu-id="77320-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="77320-135">在 Visual Studio 中，選取 [**組建**]、[**發佈 SignalR 交談**]。</span><span class="sxs-lookup"><span data-stu-id="77320-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="77320-136">在 [發行 Web] 對話方塊中，選取 [Windows Azure 網站]。</span><span class="sxs-lookup"><span data-stu-id="77320-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![選取 Azure 網站](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="77320-138">如果您尚未登入您的 Microsoft 帳戶，請按一下 [選取現有的網站] 對話方塊中的 [登**入**]，然後登入。</span><span class="sxs-lookup"><span data-stu-id="77320-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![選取現有的網站](using-signalr-with-azure-web-sites/_static/image2.png)    ![登入 Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="77320-141">在 [選取現有的網站] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="77320-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![新網站](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="77320-143">在 [在 Windows Azure 上建立網站] 對話方塊中，輸入唯一的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="77320-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="77320-144">在 [區域] 下拉式清單中選取最接近您的區域。</span><span class="sxs-lookup"><span data-stu-id="77320-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="77320-145">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="77320-145">Click **Create**.</span></span>

    ![Create site on Azure](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="77320-147">在 [發行 Web] 對話方塊中，按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="77320-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![發行網站](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="77320-149">當應用程式完成發佈時，Azure App Service Web Apps 中裝載的 SignalR Chat 應用程式將會在瀏覽器中開啟。</span><span class="sxs-lookup"><span data-stu-id="77320-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![在瀏覽器中開啟網站](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="77320-151">在 Azure App Service Web Apps 上啟用 Websocket</span><span class="sxs-lookup"><span data-stu-id="77320-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="77320-152">您必須在 web 應用程式中明確啟用 Websocket，才能在 SignalR 應用程式中使用。否則，將會使用其他通訊協定（如需詳細資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)）。</span><span class="sxs-lookup"><span data-stu-id="77320-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="77320-153">若要在 Azure App Service Web Apps 上使用 Websocket，請在 Web 應用程式的 [設定] 區段中加以啟用。</span><span class="sxs-lookup"><span data-stu-id="77320-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="77320-154">若要這麼做，請在[Azure 管理入口網站](https://manage.windowsazure.com/)中開啟您的 web 應用程式，然後選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="77320-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![Configure (設定) 索引標籤](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="77320-156">在 [設定] 頁面頂端，確定您的 web 應用程式已使用 .NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="77320-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET framework 4.5 版設定](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="77320-158">在 [設定] 頁面的 [ **websocket** ] 設定中，選取 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="77320-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![Websocket 設定：開啟](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="77320-160">在 [設定] 頁面的底部，選取 [**儲存**] 以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="77320-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![儲存設定](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="77320-162">使用 Azure Redis 快取背板</span><span class="sxs-lookup"><span data-stu-id="77320-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="77320-163">如果您的 web 應用程式使用多個實例，而且這些實例的使用者需要彼此互動（例如，在某個實例中建立的交談訊息可以連接到連線到其他實例的使用者），就必須在您的應用程式中實作為[Azure Redis 快取背板](../performance/scaleout-with-redis.md)。</span><span class="sxs-lookup"><span data-stu-id="77320-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="77320-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77320-164">Next Steps</span></span>

<span data-ttu-id="77320-165">如需 Azure App Service 中 Web Apps 的詳細資訊，請參閱[Web Apps 總覽](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)。</span><span class="sxs-lookup"><span data-stu-id="77320-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
