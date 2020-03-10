---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: 使用 OWIN 和 Katana 的消費者入門 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584669"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="5ffe5-102">開始使用 OWIN 與 Katana</span><span class="sxs-lookup"><span data-stu-id="5ffe5-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="5ffe5-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5ffe5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5ffe5-104">[Open Web Interface for .net （OWIN）](http://owin.org/)會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="5ffe5-105">藉由將網頁伺服器與應用程式分離，OWIN 可讓您更輕鬆地建立中介軟體以進行 .NET web 程式開發。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="5ffe5-106">此外，OWIN 可讓您更輕鬆地將 web 應用程式&#8212;移植到其他主機，例如，在 Windows 服務或其他進程中自我裝載。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="5ffe5-107">OWIN 是一種由社區所擁有的規格，而不是實作為。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="5ffe5-108">Katana project 是一組由 Microsoft 開發的開放原始碼 OWIN 元件。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="5ffe5-109">如需 OWIN 和 Katana 的一般總覽，請參閱[專案 Katana 的總覽](an-overview-of-project-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="5ffe5-110">在本文中，我將直接前往程式碼以開始著手。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="5ffe5-111">本教學課程使用[Visual Studio 2013 候選版](https://go.microsoft.com/fwlink/?LinkId=306566)，但您也可以使用 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="5ffe5-112">Visual Studio 2012 中有幾個步驟不同，我在下面說明。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="5ffe5-113">IIS 中的主機 OWIN</span><span class="sxs-lookup"><span data-stu-id="5ffe5-113">Host OWIN in IIS</span></span>

<span data-ttu-id="5ffe5-114">在本節中，我們會在 IIS 中裝載 OWIN。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="5ffe5-115">此選項可讓您彈性地複合性 OWIN 管線和 IIS 的成熟功能集。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="5ffe5-116">使用此選項時，OWIN 應用程式會在 ASP.NET 要求管線中執行。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="5ffe5-117">首先，建立新的 ASP.NET Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="5ffe5-118">（在 Visual Studio 2012 中，使用 ASP.NET 空白 Web 應用程式專案類型）。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="5ffe5-119">在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [**空白**] 範本。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="5ffe5-120">新增 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="5ffe5-120">Add NuGet Packages</span></span>

<span data-ttu-id="5ffe5-121">接下來，新增所需的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="5ffe5-122">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="5ffe5-123">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="5ffe5-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="5ffe5-124">新增啟動類別</span><span class="sxs-lookup"><span data-stu-id="5ffe5-124">Add a Startup Class</span></span>

<span data-ttu-id="5ffe5-125">接下來，新增 OWIN startup 類別。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="5ffe5-126">在方案總管中，以滑鼠右鍵按一下專案並選取 [**加入**]，然後選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="5ffe5-127">在 [**加入新專案**] 對話方塊中，選取 [ **Owin 啟始類別**]。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="5ffe5-128">如需設定 startup 類別的詳細資訊，請參閱[OWIN 啟動類別偵測](owin-startup-class-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="5ffe5-129">將下列程式碼加入 `Startup1.Configuration` 方法：</span><span class="sxs-lookup"><span data-stu-id="5ffe5-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="5ffe5-130">這段程式碼會將簡單的中介軟體新增至 OWIN 管線，並實作為接收**IOwinCoNtext**實例的函式。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="5ffe5-131">當伺服器收到 HTTP 要求時，OWIN 管線會叫用中介軟體。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="5ffe5-132">中介軟體會設定回應的內容類型，並寫入回應主體。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="5ffe5-133">Visual Studio 2013 中提供 OWIN Startup 類別範本。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="5ffe5-134">如果您使用 Visual Studio 2012，只要加入名為 `Startup1`的新空白類別，然後貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5ffe5-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="5ffe5-135">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="5ffe5-135">Run the Application</span></span>

<span data-ttu-id="5ffe5-136">按 F5 開始偵錯。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="5ffe5-137">Visual Studio 將會開啟瀏覽器視窗來 `http://localhost:*port*/`。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="5ffe5-138">此頁面看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="5ffe5-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="5ffe5-139">主控台應用程式中的自我裝載 OWIN</span><span class="sxs-lookup"><span data-stu-id="5ffe5-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="5ffe5-140">在自訂進程中，將此應用程式從 IIS 裝載轉換為自我裝載是很容易的。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="5ffe5-141">使用 IIS 裝載時，IIS 會同時做為 HTTP 伺服器和裝載服務的進程。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="5ffe5-142">使用自我裝載時，您的應用程式會建立進程，並使用**HttpListener**類別做為 HTTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="5ffe5-143">在 Visual Studio 中，建立新的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="5ffe5-144">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="5ffe5-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="5ffe5-145">將本教學課程的第1部分中的 `Startup1` 類別加入至專案。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="5ffe5-146">您不需要修改這個類別。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-146">You don't need to modify this class.</span></span>

<span data-ttu-id="5ffe5-147">依照下列方式，執行應用程式的 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="5ffe5-148">當您執行主控台應用程式時，伺服器會開始接聽 `http://localhost:9000`。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="5ffe5-149">如果您在網頁瀏覽器中流覽至此位址，您會看到 [Hello world] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="5ffe5-150">新增 OWIN 診斷</span><span class="sxs-lookup"><span data-stu-id="5ffe5-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="5ffe5-151">Owin 診斷套件包含的中介軟體會攔截未處理的例外狀況，並顯示包含錯誤詳細資料的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="5ffe5-152">此頁面的運作方式非常類似 ASP.NET 錯誤頁面，有時稱為「[黃色的死亡螢幕](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)」（YSOD）。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="5ffe5-153">就像 YSOD，Katana 錯誤頁面在開發期間很有用，但在生產模式中將它停用是很好的作法。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="5ffe5-154">若要在您的專案中安裝診斷套件，請在 [套件管理員主控台] 視窗中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="5ffe5-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="5ffe5-155">變更 `Startup1.Configuration` 方法中的程式碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5ffe5-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="5ffe5-156">現在使用 CTRL + F5 來執行應用程式，而不進行任何偵測，因此 Visual Studio 不會在例外狀況時中斷。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="5ffe5-157">應用程式的行為與之前相同，除非您流覽至 `http://localhost/fail`，此時應用程式會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="5ffe5-158">錯誤頁面中介軟體會攔截例外狀況，並顯示 HTML 頁面，其中包含錯誤的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="5ffe5-159">您可以按一下索引標籤，以查看堆疊、查詢字串、cookie、要求標頭和 OWIN 環境變數。</span><span class="sxs-lookup"><span data-stu-id="5ffe5-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="5ffe5-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ffe5-160">Next Steps</span></span>

- [<span data-ttu-id="5ffe5-161">OWIN 啟動類別偵測</span><span class="sxs-lookup"><span data-stu-id="5ffe5-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="5ffe5-162">使用 OWIN 自我裝載 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="5ffe5-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="5ffe5-163">使用 OWIN 自我裝載 SignalR</span><span class="sxs-lookup"><span data-stu-id="5ffe5-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
