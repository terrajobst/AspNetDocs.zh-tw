---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN 自我裝載 ASP.NET Web API-ASP.NET 4。x
author: rick-anderson
description: 示範如何在主控台應用程式中裝載 ASP.NET Web API 的程式碼教學課程。
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556536"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="4111d-103">使用 OWIN 自我裝載 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="4111d-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 

> <span data-ttu-id="4111d-104">本教學課程示範如何使用 OWIN，在主控台應用程式中裝載 ASP.NET Web API，以自我裝載 Web API 架構。</span><span class="sxs-lookup"><span data-stu-id="4111d-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="4111d-105">[Open Web Interface for .net](http://owin.org) （OWIN）會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="4111d-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="4111d-106">OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 非常適合在 IIS 以外的進程中自我裝載 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4111d-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4111d-107">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="4111d-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="4111d-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4111d-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="4111d-109">Web API 5.2。7</span><span class="sxs-lookup"><span data-stu-id="4111d-109">Web API 5.2.7</span></span>

> [!NOTE]
> <span data-ttu-id="4111d-110">您可以在[github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)找到本教學課程的完整原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="4111d-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="4111d-111">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="4111d-111">Create a console application</span></span>

<span data-ttu-id="4111d-112">**在 [檔案**] 功能表上，按一下 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="4111d-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="4111d-113">從 [**已安裝**] 的 [**視覺C#效果**] 底下選取 [ **Windows 桌面**]，然後選取 **[主控台應用程式（.net Framework）** ]</span><span class="sxs-lookup"><span data-stu-id="4111d-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="4111d-114">將專案命名為 "OwinSelfhostSample"，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="4111d-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="4111d-115">新增 Web API 和 OWIN 套件</span><span class="sxs-lookup"><span data-stu-id="4111d-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="4111d-116">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="4111d-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4111d-117">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="4111d-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="4111d-118">這會安裝 WebAPI OWIN selfhost 套件和所有必要的 OWIN 套件。</span><span class="sxs-lookup"><span data-stu-id="4111d-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="4111d-119">設定適用于自我裝載的 Web API</span><span class="sxs-lookup"><span data-stu-id="4111d-119">Configure Web API for self-host</span></span>

<span data-ttu-id="4111d-120">在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**新增** / **類別**] 以加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="4111d-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="4111d-121">將類別命名為 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="4111d-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="4111d-122">以下列內容取代此檔案中的所有重複使用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="4111d-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="4111d-123">新增 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="4111d-123">Add a Web API controller</span></span>

<span data-ttu-id="4111d-124">接下來，新增 Web API 控制器類別。</span><span class="sxs-lookup"><span data-stu-id="4111d-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="4111d-125">在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**新增** / **類別**] 以加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="4111d-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="4111d-126">將類別命名為 `ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="4111d-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="4111d-127">以下列內容取代此檔案中的所有重複使用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="4111d-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="4111d-128">啟動 OWIN 主機，並使用 HttpClient 提出要求</span><span class="sxs-lookup"><span data-stu-id="4111d-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="4111d-129">以下列內容取代 Program.cs 檔案中的所有重複使用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="4111d-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="4111d-130">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="4111d-130">Run the application</span></span>

<span data-ttu-id="4111d-131">若要執行應用程式，請在 Visual Studio 中按 F5。</span><span class="sxs-lookup"><span data-stu-id="4111d-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="4111d-132">輸出看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="4111d-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="4111d-133">其他資源</span><span class="sxs-lookup"><span data-stu-id="4111d-133">Additional resources</span></span>

[<span data-ttu-id="4111d-134">Katana 專案概觀</span><span class="sxs-lookup"><span data-stu-id="4111d-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="4111d-135">Azure 背景工作角色中的主機 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="4111d-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
