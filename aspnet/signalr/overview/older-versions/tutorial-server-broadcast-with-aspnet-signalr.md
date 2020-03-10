---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 教學課程：使用 ASP.NET SignalR 1.x 的伺服器廣播 |Microsoft Docs
author: bradygaster
description: 本教學課程示範如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供伺服器廣播功能。 伺服器廣播表示 communic 。
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579405"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a><span data-ttu-id="012c7-104">教學課程：使用 ASP.NET SignalR 1.x 的伺服器廣播</span><span class="sxs-lookup"><span data-stu-id="012c7-104">Tutorial: Server Broadcast with ASP.NET SignalR 1.x</span></span>

<span data-ttu-id="012c7-105">由一[Fletcher](https://github.com/pfletcher)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="012c7-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="012c7-106">本教學課程示範如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供伺服器廣播功能。</span><span class="sxs-lookup"><span data-stu-id="012c7-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide server broadcast functionality.</span></span> <span data-ttu-id="012c7-107">伺服器廣播表示傳送至用戶端的通訊是由伺服器起始。</span><span class="sxs-lookup"><span data-stu-id="012c7-107">Server broadcast means that communications sent to clients are initiated by the server.</span></span> <span data-ttu-id="012c7-108">此案例所需的程式設計方法與對等案例（例如聊天應用程式）不同，而傳送到用戶端的通訊是由一或多個用戶端起始。</span><span class="sxs-lookup"><span data-stu-id="012c7-108">This scenario requires a different programming approach than peer-to-peer scenarios such as chat applications, in which communications sent to clients are initiated by one or more of the clients.</span></span>
> 
> <span data-ttu-id="012c7-109">您在本教學課程中建立的應用程式會模擬股票行情指示器，這是伺服器廣播功能的一般案例。</span><span class="sxs-lookup"><span data-stu-id="012c7-109">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span>
> 
> <span data-ttu-id="012c7-110">歡迎使用教學課程的批註。</span><span class="sxs-lookup"><span data-stu-id="012c7-110">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="012c7-111">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="012c7-111">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>

## <a name="overview"></a><span data-ttu-id="012c7-112">概觀</span><span class="sxs-lookup"><span data-stu-id="012c7-112">Overview</span></span>

<span data-ttu-id="012c7-113">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 套件會在 Visual Studio 專案中安裝範例模擬股票行情指示器應用程式。</span><span class="sxs-lookup"><span data-stu-id="012c7-113">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package installs a sample simulated stock ticker application in a Visual Studio project.</span></span> <span data-ttu-id="012c7-114">在本教學課程的第一個部分中，您將從頭開始建立該應用程式的簡化版本。</span><span class="sxs-lookup"><span data-stu-id="012c7-114">In the first part of this tutorial, you'll create a simplified version of that application from scratch.</span></span> <span data-ttu-id="012c7-115">在本教學課程的其餘部分中，您將會安裝 NuGet 套件，並檢查它所建立的其他功能和程式碼。</span><span class="sxs-lookup"><span data-stu-id="012c7-115">In the remainder of the tutorial, you'll install the NuGet package and review the additional features and code that it creates.</span></span>

<span data-ttu-id="012c7-116">股票行情指示器應用程式是一種即時應用程式的代表，您想要定期「推送」或「廣播」通知，從伺服器到所有連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="012c7-116">The stock ticker application is a representative of a kind of real-time application in which you want to periodically "push," or broadcast, notifications from the server to all connected clients.</span></span>

<span data-ttu-id="012c7-117">您將在本教學課程的第一個部分中建立的應用程式會顯示包含股票資料的方格。</span><span class="sxs-lookup"><span data-stu-id="012c7-117">The application that you'll build in the first part of this tutorial displays a grid with stock data.</span></span>

![StockTicker 初始版本](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

<span data-ttu-id="012c7-119">伺服器會定期隨機更新股票價格，並將更新推送至所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="012c7-119">Periodically the server randomly updates stock prices and pushes the updates to all connected clients.</span></span> <span data-ttu-id="012c7-120">在瀏覽器中，[**變更**] 和 [ **%** ] 資料行中的數位和符號會動態變更，以回應來自伺服器的通知。</span><span class="sxs-lookup"><span data-stu-id="012c7-120">In the browser the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="012c7-121">如果您對相同的 URL 開啟其他瀏覽器，它們會同時顯示相同的資料和相同的資料變更。</span><span class="sxs-lookup"><span data-stu-id="012c7-121">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

<span data-ttu-id="012c7-122">本教學課程包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="012c7-122">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="012c7-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="012c7-123">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="012c7-124">建立專案</span><span class="sxs-lookup"><span data-stu-id="012c7-124">Create the project</span></span>](#createproject)
- [<span data-ttu-id="012c7-125">新增 SignalR NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="012c7-125">Add the SignalR NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="012c7-126">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="012c7-126">Set up the server code</span></span>](#server)
- [<span data-ttu-id="012c7-127">設定用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="012c7-127">Set up the client code</span></span>](#client)
- [<span data-ttu-id="012c7-128">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="012c7-128">Test the application</span></span>](#test)
- [<span data-ttu-id="012c7-129">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="012c7-129">Enable logging</span></span>](#enablelogging)
- [<span data-ttu-id="012c7-130">安裝和查看完整的 StockTicker 範例</span><span class="sxs-lookup"><span data-stu-id="012c7-130">Install and review the full StockTicker sample</span></span>](#fullsample)
- [<span data-ttu-id="012c7-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="012c7-131">Next steps</span></span>](#nextsteps)

> [!NOTE]
> <span data-ttu-id="012c7-132">如果您不想要逐步執行建立應用程式的步驟，您可以在新的**空白 ASP.NET Web 應用程式**專案中安裝 SignalR 套件，並閱讀這些步驟來取得程式碼的說明。</span><span class="sxs-lookup"><span data-stu-id="012c7-132">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new **Empty ASP.NET Web Application** project, and read through these steps to get explanations of the code.</span></span> <span data-ttu-id="012c7-133">本教學課程的第一個部分涵蓋 SignalR 的子集，第二個部分則說明 SignalR 中其他功能的主要功能。</span><span class="sxs-lookup"><span data-stu-id="012c7-133">The first part of the tutorial covers a subset of the SignalR.Sample code, and the second part explains key features of the additional functionality in the SignalR.Sample package.</span></span>

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="012c7-134">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="012c7-134">Prerequisites</span></span>

<span data-ttu-id="012c7-135">開始之前，請確定您已在電腦上安裝 Visual Studio 2012 或 2010 SP1。</span><span class="sxs-lookup"><span data-stu-id="012c7-135">Before you start, make sure that you have Visual Studio 2012 or 2010 SP1 installed on your computer.</span></span> <span data-ttu-id="012c7-136">如果您沒有 Visual Studio，請參閱[ASP.NET 下載](https://www.asp.net/downloads)以取得免費的 Visual Studio 2012 Express for Web。</span><span class="sxs-lookup"><span data-stu-id="012c7-136">If you don't have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express for Web.</span></span>

<span data-ttu-id="012c7-137">如果您有 Visual Studio 2010，請確定已安裝[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。</span><span class="sxs-lookup"><span data-stu-id="012c7-137">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="012c7-138">建立專案</span><span class="sxs-lookup"><span data-stu-id="012c7-138">Create the project</span></span>

1. <span data-ttu-id="012c7-139">從 [檔案] 功能表，按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="012c7-139">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="012c7-140">在 [**新增專案**] 對話方塊中， **C#** 展開 [**範本**]，然後選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-140">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="012c7-141">選取 [ **ASP.NET 空白 Web 應用程式**] 範本，將專案命名為*SignalR StockTicker*，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="012c7-141">Select the **ASP.NET Empty Web Application** template, name the project *SignalR.StockTicker*, and click **OK**.</span></span>

    ![新增專案對話方塊](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a><span data-ttu-id="012c7-143">新增 SignalR NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="012c7-143">Add the SignalR NuGet Packages</span></span>

### <a name="add-the-signalr-and-jquery-nuget-packages"></a><span data-ttu-id="012c7-144">新增 SignalR 和 JQuery NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="012c7-144">Add the SignalR and JQuery NuGet Packages</span></span>

<span data-ttu-id="012c7-145">您可以藉由安裝 NuGet 套件，將 SignalR 功能新增至專案。</span><span class="sxs-lookup"><span data-stu-id="012c7-145">You can add SignalR functionality to a project by installing a NuGet package.</span></span>

1. <span data-ttu-id="012c7-146">按一下 [**工具] |NuGet 套件管理員 |套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="012c7-146">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="012c7-147">在 [套件管理員] 中輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="012c7-147">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    <span data-ttu-id="012c7-148">SignalR 套件會安裝一些其他 NuGet 套件做為相依性。</span><span class="sxs-lookup"><span data-stu-id="012c7-148">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="012c7-149">當安裝完成時，您會擁有在 ASP.NET 應用程式中使用 SignalR 所需的所有伺服器和用戶端元件。</span><span class="sxs-lookup"><span data-stu-id="012c7-149">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>

<a id="server"></a>

## <a name="set-up-the-server-code"></a><span data-ttu-id="012c7-150">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="012c7-150">Set up the server code</span></span>

<span data-ttu-id="012c7-151">在本節中，您會設定在伺服器上執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="012c7-151">In this section you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="012c7-152">建立 Stock 類別</span><span class="sxs-lookup"><span data-stu-id="012c7-152">Create the Stock class</span></span>

<span data-ttu-id="012c7-153">您一開始會先建立用來儲存和傳送股票資訊的股票模型類別。</span><span class="sxs-lookup"><span data-stu-id="012c7-153">You begin by creating the Stock model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="012c7-154">在專案資料夾中建立新的類別檔案，將其命名為*Stock.cs*，然後將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="012c7-154">Create a new class file in the project folder, name it *Stock.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    <span data-ttu-id="012c7-155">您在建立股票時所設定的兩個屬性是符號（例如，MSFT for Microsoft）和價格。</span><span class="sxs-lookup"><span data-stu-id="012c7-155">The two properties that you'll set when you create stocks are the Symbol (for example, MSFT for Microsoft) and the Price.</span></span> <span data-ttu-id="012c7-156">其他屬性則取決於您設定價格的方式和時間。</span><span class="sxs-lookup"><span data-stu-id="012c7-156">The other properties depend on how and when you set Price.</span></span> <span data-ttu-id="012c7-157">第一次設定價格時，值會傳播至 DayOpen。</span><span class="sxs-lookup"><span data-stu-id="012c7-157">The first time you set Price, the value gets propagated to DayOpen.</span></span> <span data-ttu-id="012c7-158">後續設定價格時，會根據 Price 和 DayOpen 之間的差異來計算變更和 PercentChange 屬性值。</span><span class="sxs-lookup"><span data-stu-id="012c7-158">Subsequent times when you set Price, the Change and PercentChange property values are calculated based on the difference between Price and DayOpen.</span></span>

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a><span data-ttu-id="012c7-159">建立 StockTicker 和 StockTickerHub 類別</span><span class="sxs-lookup"><span data-stu-id="012c7-159">Create the StockTicker and StockTickerHub classes</span></span>

<span data-ttu-id="012c7-160">您將使用 SignalR 中樞 API 來處理伺服器對用戶端的互動。</span><span class="sxs-lookup"><span data-stu-id="012c7-160">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="012c7-161">衍生自 SignalR 中樞類別的 StockTickerHub 類別將會處理來自用戶端的接收連接和方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="012c7-161">A StockTickerHub class that derives from the SignalR Hub class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="012c7-162">您也需要維護庫存資料，並執行計時器物件，以定期觸發價格更新，而不受用戶端連線影響。</span><span class="sxs-lookup"><span data-stu-id="012c7-162">You also need to maintain stock data and run a Timer object to periodically trigger price updates, independently of client connections.</span></span> <span data-ttu-id="012c7-163">因為中樞實例是暫時性的，所以您無法將這些函數放在中樞類別中。</span><span class="sxs-lookup"><span data-stu-id="012c7-163">You can't put these functions in a Hub class, because Hub instances are transient.</span></span> <span data-ttu-id="012c7-164">會針對中樞上的每個作業建立中樞類別實例，例如從用戶端到伺服器的連接和呼叫。</span><span class="sxs-lookup"><span data-stu-id="012c7-164">A Hub class instance is created for each operation on the hub, such as connections and calls from the client to the server.</span></span> <span data-ttu-id="012c7-165">因此，保留股票資料、更新價格，以及廣播價格更新的機制，必須在不同的類別中執行，您將會將其命名為 StockTicker。</span><span class="sxs-lookup"><span data-stu-id="012c7-165">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class, which you'll name StockTicker.</span></span>

![從 StockTicker 廣播](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

<span data-ttu-id="012c7-167">您只想要在伺服器上執行一個 StockTicker 類別實例，因此您必須設定每個 StockTickerHub 實例到單一 StockTicker 實例的參考。</span><span class="sxs-lookup"><span data-stu-id="012c7-167">You only want one instance of the StockTicker class to run on the server, so you'll need to set up a reference from each StockTickerHub instance to the singleton StockTicker instance.</span></span> <span data-ttu-id="012c7-168">StockTicker 類別必須能夠廣播到用戶端，因為它有存貨資料和觸發程式更新，但 StockTicker 不是中樞類別。</span><span class="sxs-lookup"><span data-stu-id="012c7-168">The StockTicker class has to be able to broadcast to clients because it has the stock data and triggers updates, but StockTicker is not a Hub class.</span></span> <span data-ttu-id="012c7-169">因此，StockTicker 類別必須取得 SignalR Hub 連接內容物件的參考。</span><span class="sxs-lookup"><span data-stu-id="012c7-169">Therefore, the StockTicker class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="012c7-170">然後，它可以使用 SignalR 連接內容物件廣播至用戶端。</span><span class="sxs-lookup"><span data-stu-id="012c7-170">It can then use the SignalR connection context object to broadcast to clients.</span></span>

1. <span data-ttu-id="012c7-171">在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**加入新專案**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-171">In **Solution Explorer**, right-click the project and click **Add New Item**.</span></span>
2. <span data-ttu-id="012c7-172">如果您有[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=279941)的 Visual Studio 2012，請按一下 [**視覺效果C#**  ] 底下的 [ **Web** ]，然後選取 [ **SignalR 中樞類別**] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="012c7-172">If you have Visual Studio 2012 with the [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=279941), click **Web** under **Visual C#** and select the **SignalR Hub Class** item template.</span></span> <span data-ttu-id="012c7-173">否則，請選取 [**類別**] 範本。</span><span class="sxs-lookup"><span data-stu-id="012c7-173">Otherwise, select the **Class** template.</span></span>
3. <span data-ttu-id="012c7-174">將新類別命名為*StockTickerHub.cs*，**然後按一下 [新增]** 。</span><span class="sxs-lookup"><span data-stu-id="012c7-174">Name the new class *StockTickerHub.cs*, and then click **Add**.</span></span>

    ![新增 StockTickerHub.cs](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. <span data-ttu-id="012c7-176">使用下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="012c7-176">Replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    <span data-ttu-id="012c7-177">[中樞](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)類別是用來定義用戶端可以在伺服器上呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-177">The [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class is used to define methods the clients can call on the server.</span></span> <span data-ttu-id="012c7-178">您要定義一個方法： `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="012c7-178">You are defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="012c7-179">當用戶端一開始連線到伺服器時，會呼叫此方法來取得所有股票的清單及其目前的價格。</span><span class="sxs-lookup"><span data-stu-id="012c7-179">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="012c7-180">方法可以同步執行並傳回 `IEnumerable<Stock>`，因為它會從記憶體傳回資料。</span><span class="sxs-lookup"><span data-stu-id="012c7-180">The method can execute synchronously and return `IEnumerable<Stock>` because it is returning data from memory.</span></span> <span data-ttu-id="012c7-181">如果方法必須藉由執行需要等候的專案（例如資料庫查閱或 web 服務呼叫）來取得資料，您會將 `Task<IEnumerable<Stock>>` 指定為傳回值，以啟用非同步處理。</span><span class="sxs-lookup"><span data-stu-id="012c7-181">If the method had to get the data by doing something that would involve waiting, such as a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="012c7-182">如需詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-何時以非同步方式執行](index.md)。</span><span class="sxs-lookup"><span data-stu-id="012c7-182">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](index.md).</span></span>

    <span data-ttu-id="012c7-183">HubName 屬性會指定如何在用戶端上的 JavaScript 程式碼中參考中樞。</span><span class="sxs-lookup"><span data-stu-id="012c7-183">The HubName attribute specifies how the Hub will be referenced in JavaScript code on the client.</span></span> <span data-ttu-id="012c7-184">如果您不使用這個屬性，則用戶端上的預設名稱是類別名稱的 camel 大小寫版本，在此案例中會是 stockTickerHub。</span><span class="sxs-lookup"><span data-stu-id="012c7-184">The default name on the client if you don't use this attribute is a camel-cased version of the class name, which in this case would be stockTickerHub.</span></span>

    <span data-ttu-id="012c7-185">您稍後會在建立 StockTicker 類別時看到，會在其靜態實例屬性中建立該類別的單一實例。</span><span class="sxs-lookup"><span data-stu-id="012c7-185">As you'll see later when you create the StockTicker class, a singleton instance of that class is created in its static Instance property.</span></span> <span data-ttu-id="012c7-186">不論有多少用戶端連線或中斷連接，StockTicker 的單一實例都會保留在記憶體中，而該實例就是 GetAllStocks 方法用來傳回目前股票資訊的情況。</span><span class="sxs-lookup"><span data-stu-id="012c7-186">That singleton instance of StockTicker remains in memory no matter how many clients connect or disconnect, and that instance is what the GetAllStocks method uses to return current stock information.</span></span>
5. <span data-ttu-id="012c7-187">在專案資料夾中建立新的類別檔案，將其命名為*StockTicker.cs*，然後將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="012c7-187">Create a new class file in the project folder, name it *StockTicker.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    <span data-ttu-id="012c7-188">因為多個執行緒將會執行相同的 StockTicker 程式碼實例，所以 StockTicker 類別必須是 threadsafe。</span><span class="sxs-lookup"><span data-stu-id="012c7-188">Since multiple threads will be running the same instance of StockTicker code, the StockTicker class has to be threadsafe.</span></span>

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="012c7-189">將單一實例儲存在靜態欄位中</span><span class="sxs-lookup"><span data-stu-id="012c7-189">Storing the singleton instance in a static field</span></span>

    <span data-ttu-id="012c7-190">此程式碼會初始化靜態 \_實例欄位，以使用類別的實例來支援實例屬性，而且這是唯一可以建立之類別的實例，因為此函式會標示為私用。</span><span class="sxs-lookup"><span data-stu-id="012c7-190">The code initializes the static \_instance field that backs the Instance property with an instance of the class, and this is the only instance of the class that can be created, because the constructor is marked as private.</span></span> <span data-ttu-id="012c7-191">[延遲初始化](https://msdn.microsoft.com/library/dd997286.aspx)會用於 \_實例欄位，而不是基於效能考慮，但可確保實例建立是 threadsafe 的。</span><span class="sxs-lookup"><span data-stu-id="012c7-191">[Lazy initialization](https://msdn.microsoft.com/library/dd997286.aspx) is used for the \_instance field, not for performance reasons but to ensure that the instance creation is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    <span data-ttu-id="012c7-192">每次用戶端連接到伺服器時，在個別執行緒中執行之 StockTickerHub 類別的新實例會從 StockTicker 靜態屬性取得 StockTicker 單一實例，如您稍早在 StockTickerHub 類別中所見。</span><span class="sxs-lookup"><span data-stu-id="012c7-192">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the StockTicker.Instance static property, as you saw earlier in the StockTickerHub class.</span></span>

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="012c7-193">將存貨資料儲存在 ConcurrentDictionary 中</span><span class="sxs-lookup"><span data-stu-id="012c7-193">Storing stock data in a ConcurrentDictionary</span></span>

    <span data-ttu-id="012c7-194">此函式會使用一些範例股票資料來初始化 \_的股票集合，而 GetAllStocks 會傳回股票。</span><span class="sxs-lookup"><span data-stu-id="012c7-194">The constructor initializes the \_stocks collection with some sample stock data, and GetAllStocks returns the stocks.</span></span> <span data-ttu-id="012c7-195">如您稍早所見，這組股票會轉而由 StockTickerHub 傳回。 GetAllStocks，這是用戶端可以呼叫的中樞類別中的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-195">As you saw earlier, this collection of stocks is in turn returned by StockTickerHub.GetAllStocks which is a server method in the Hub class that clients can call.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    <span data-ttu-id="012c7-196">股票集合會定義為執行緒安全性的[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)類型。</span><span class="sxs-lookup"><span data-stu-id="012c7-196">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="012c7-197">或者，您可以使用[dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)物件，並在進行變更時明確地鎖定字典。</span><span class="sxs-lookup"><span data-stu-id="012c7-197">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

    <span data-ttu-id="012c7-198">針對此範例應用程式，您可以將應用程式資料儲存在記憶體中，並在處置 StockTicker 實例時遺失資料。</span><span class="sxs-lookup"><span data-stu-id="012c7-198">For this sample application, it's OK to store application data in memory and to lose the data when the StockTicker instance is disposed.</span></span> <span data-ttu-id="012c7-199">在實際的應用程式中，您會使用後端資料存放區，例如資料庫。</span><span class="sxs-lookup"><span data-stu-id="012c7-199">In a real application you would work with a back-end data store such as a database.</span></span>

    ### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="012c7-200">定期更新股票價格</span><span class="sxs-lookup"><span data-stu-id="012c7-200">Periodically updating stock prices</span></span>

    <span data-ttu-id="012c7-201">此函式會啟動計時器物件，定期呼叫會隨機更新股票價格的方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-201">The constructor starts up a Timer object that periodically calls methods that update stock prices on a random basis.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    <span data-ttu-id="012c7-202">UpdateStockPrices 是由計時器呼叫，它會在 state 參數中傳遞 null。</span><span class="sxs-lookup"><span data-stu-id="012c7-202">UpdateStockPrices is called by the Timer, which passes in null in the state parameter.</span></span> <span data-ttu-id="012c7-203">更新價格之前，會對 \_updateStockPricesLock 物件採取鎖定。</span><span class="sxs-lookup"><span data-stu-id="012c7-203">Before updating prices, a lock is taken on the \_updateStockPricesLock object.</span></span> <span data-ttu-id="012c7-204">程式碼會檢查另一個執行緒是否已更新價格，然後在清單中的每個股票上呼叫 TryUpdateStockPrice。</span><span class="sxs-lookup"><span data-stu-id="012c7-204">The code checks if another thread is already updating prices, and then it calls TryUpdateStockPrice on each stock in the list.</span></span> <span data-ttu-id="012c7-205">TryUpdateStockPrice 方法會決定是否要變更股票價格，以及要變更的數量。</span><span class="sxs-lookup"><span data-stu-id="012c7-205">The TryUpdateStockPrice method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="012c7-206">如果股票價格已變更，則會呼叫 BroadcastStockPrice 以將股票價格變更廣播至所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="012c7-206">If the stock price is changed, BroadcastStockPrice is called to broadcast the stock price change to all connected clients.</span></span>

    <span data-ttu-id="012c7-207">\_updatingStockPrices 旗標會標示為[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) ，以確保它的存取權是 threadsafe。</span><span class="sxs-lookup"><span data-stu-id="012c7-207">The \_updatingStockPrices flag is marked as [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to ensure that access to it is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    <span data-ttu-id="012c7-208">在實際的應用程式中，TryUpdateStockPrice 方法會呼叫 web 服務來查閱價格;在此程式碼中，它會使用亂數字產生器來隨機進行變更。</span><span class="sxs-lookup"><span data-stu-id="012c7-208">In a real application, the TryUpdateStockPrice method would call a web service to look up the price; in this code it uses a random number generator to make changes randomly.</span></span>

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="012c7-209">取得 SignalR 內容，讓 StockTicker 類別可以廣播至用戶端</span><span class="sxs-lookup"><span data-stu-id="012c7-209">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

    <span data-ttu-id="012c7-210">因為價格變更的來源是 StockTicker 物件，所以這是需要在所有已連線的用戶端上呼叫 updateStockPrice 方法的物件。</span><span class="sxs-lookup"><span data-stu-id="012c7-210">Because the price changes originate here in the StockTicker object, this is the object that needs to call an updateStockPrice method on all connected clients.</span></span> <span data-ttu-id="012c7-211">在中樞類別中，您有可呼叫用戶端方法的 API，但 StockTicker 不是衍生自中樞類別，而且沒有任何中樞物件的參考。</span><span class="sxs-lookup"><span data-stu-id="012c7-211">In a Hub class you have an API for calling client methods, but StockTicker does not derive from the Hub class and does not have a reference to any Hub object.</span></span> <span data-ttu-id="012c7-212">因此，為了廣播至已連線的用戶端，StockTicker 類別必須取得 StockTickerHub 類別的 SignalR 內容實例，並使用它來呼叫用戶端上的方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-212">Therefore, in order to broadcast to connected clients, the StockTicker class has to get the SignalR context instance for the StockTickerHub class and use that to call methods on clients.</span></span>

    <span data-ttu-id="012c7-213">程式碼會在建立單一類別實例時取得 SignalR 內容的參考，將該參考傳遞給此函式，而此函式會將它放在用戶端屬性中。</span><span class="sxs-lookup"><span data-stu-id="012c7-213">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the Clients property.</span></span>

    <span data-ttu-id="012c7-214">當您只想要取得內容一次時，有兩個原因：取得內容是昂貴的作業，而取得它一次可確保傳送至用戶端之訊息的預期順序會保留下來。</span><span class="sxs-lookup"><span data-stu-id="012c7-214">There are two reasons why you want to get the context just once: getting the context is an expensive operation, and getting it once ensures that the intended order of messages sent to clients is preserved.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    <span data-ttu-id="012c7-215">取得內容的用戶端屬性並將它放在 StockTickerClient 屬性中，可讓您撰寫程式碼來呼叫用戶端方法，其外觀與在中樞類別中相同。</span><span class="sxs-lookup"><span data-stu-id="012c7-215">Getting the Clients property of the context and putting it in the StockTickerClient property lets you write code to call client methods that looks the same as it would in a Hub class.</span></span> <span data-ttu-id="012c7-216">比方說，若要廣播至所有用戶端，您可以撰寫用戶端。 updateStockPrice （股票）。</span><span class="sxs-lookup"><span data-stu-id="012c7-216">For instance, to broadcast to all clients you can write Clients.All.updateStockPrice(stock).</span></span>

    <span data-ttu-id="012c7-217">您在 BroadcastStockPrice 中呼叫的 updateStockPrice 方法尚不存在;稍後當您撰寫在用戶端上執行的程式碼時，您將會新增它。</span><span class="sxs-lookup"><span data-stu-id="012c7-217">The updateStockPrice method that you are calling in BroadcastStockPrice doesn't exist yet; you'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="012c7-218">您可以參考這裡的 updateStockPrice，因為用戶端。全部都是動態的，這表示運算式會在執行時間進行評估。</span><span class="sxs-lookup"><span data-stu-id="012c7-218">You can refer to updateStockPrice here because Clients.All is dynamic, which means the expression will be evaluated at runtime.</span></span> <span data-ttu-id="012c7-219">當這個方法呼叫執行時，SignalR 會將方法名稱和參數值傳送給用戶端，如果用戶端具有名為 updateStockPrice 的方法，就會呼叫該方法，並將參數值傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="012c7-219">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named updateStockPrice, that method will be called and the parameter value will be passed to it.</span></span>

    <span data-ttu-id="012c7-220">用戶端。所有方法皆會傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="012c7-220">Clients.All means send to all clients.</span></span> <span data-ttu-id="012c7-221">SignalR 提供您其他選項來指定要傳送至哪些用戶端或用戶端群組。</span><span class="sxs-lookup"><span data-stu-id="012c7-221">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="012c7-222">如需詳細資訊，請參閱[HubConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="012c7-222">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="012c7-223">註冊 SignalR 路由</span><span class="sxs-lookup"><span data-stu-id="012c7-223">Register the SignalR route</span></span>

<span data-ttu-id="012c7-224">伺服器必須知道要攔截並直接 SignalR 的 URL。</span><span class="sxs-lookup"><span data-stu-id="012c7-224">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="012c7-225">若要這麼做，請將一些程式碼加入至*global.asax*檔案。</span><span class="sxs-lookup"><span data-stu-id="012c7-225">To do that you'll add some code to the *Global.asax* file.</span></span>

1. <span data-ttu-id="012c7-226">在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**加入新專案**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-226">In **Solution Explorer**, right-click the project, and then click **Add New Item**.</span></span>
2. <span data-ttu-id="012c7-227">選取 [**全域應用程式類別**] 專案範本，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-227">Select the **Global Application Class** item template, and then click **Add**.</span></span>

    ![加入 global.asax](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. <span data-ttu-id="012c7-229">將 SignalR 路由註冊碼新增至應用程式\_Start 方法：</span><span class="sxs-lookup"><span data-stu-id="012c7-229">Add the SignalR route registration code to the Application\_Start method:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    <span data-ttu-id="012c7-230">根據預設，所有 SignalR 流量的基底 URL 為 "/signalr"，而 "/signalr/hubs" 是用來抓取動態產生的 JavaScript 檔案，該檔案會針對您應用程式中的所有中樞定義 proxy。</span><span class="sxs-lookup"><span data-stu-id="012c7-230">By default, the base URL for all SignalR traffic is "/signalr", and "/signalr/hubs" is used to retrieve a dynamically generated JavaScript file that defines proxies for all the Hubs you have in your application.</span></span> <span data-ttu-id="012c7-231">MapHubs 方法包含多載，可讓您在[HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx)類別的實例中指定不同的基底 URL 和特定的 SignalR 選項。</span><span class="sxs-lookup"><span data-stu-id="012c7-231">The MapHubs method includes overloads that let you specify a different base URL and certain SignalR options in an instance of the [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) class.</span></span>
4. <span data-ttu-id="012c7-232">在檔案頂端新增 using 語句：</span><span class="sxs-lookup"><span data-stu-id="012c7-232">Add a using statement at the top of the file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. <span data-ttu-id="012c7-233">儲存並關閉*global.asax*檔案，並建立專案。</span><span class="sxs-lookup"><span data-stu-id="012c7-233">Save and close the *Global.asax* file, and build the project.</span></span>

<span data-ttu-id="012c7-234">您現在已完成伺服器程式碼的設定。</span><span class="sxs-lookup"><span data-stu-id="012c7-234">You have now completed setting up the server code.</span></span> <span data-ttu-id="012c7-235">在下一節中，您將設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="012c7-235">In the next section you'll set up the client.</span></span>

<a id="client"></a>

## <a name="set-up-the-client-code"></a><span data-ttu-id="012c7-236">設定用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="012c7-236">Set up the client code</span></span>

1. <span data-ttu-id="012c7-237">在專案資料夾中建立新的 HTML 檔案，並將它命名為*StockTicker*。</span><span class="sxs-lookup"><span data-stu-id="012c7-237">Create a new HTML file in the project folder, and name it *StockTicker.html*.</span></span>
2. <span data-ttu-id="012c7-238">使用下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="012c7-238">Replace the template code with the following code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    <span data-ttu-id="012c7-239">HTML 會建立包含5個數據行的資料表、一個標題列，以及一個橫跨所有5個數據行的單一儲存格。</span><span class="sxs-lookup"><span data-stu-id="012c7-239">The HTML creates a table with 5 columns, a header row, and a data row with a single cell that spans all 5 columns.</span></span> <span data-ttu-id="012c7-240">資料列會顯示「正在載入 ...」只有在應用程式啟動時，才會立即顯示和。</span><span class="sxs-lookup"><span data-stu-id="012c7-240">The data row displays "loading..." and will only be shown momentarily when the application starts.</span></span> <span data-ttu-id="012c7-241">JavaScript 程式碼將會移除該資料列，並加入其位置列，其中包含從伺服器抓取的股票資料。</span><span class="sxs-lookup"><span data-stu-id="012c7-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="012c7-242">腳本標記會指定 jQuery 腳本檔案、SignalR core 腳本檔案、SignalR proxy 腳本檔案，以及稍後將建立的 StockTicker 腳本檔案。</span><span class="sxs-lookup"><span data-stu-id="012c7-242">The script tags specify the jQuery script file, the SignalR core script file, the SignalR proxies script file, and a StockTicker script file that you'll create later.</span></span> <span data-ttu-id="012c7-243">SignalR proxy 腳本檔案（指定 "/signalr/hubs" URL）是以動態方式產生，並定義中樞類別上方法的 proxy 方法，在此案例中為 StockTickerHub. GetAllStocks。</span><span class="sxs-lookup"><span data-stu-id="012c7-243">The SignalR proxies script file, which specifies the "/signalr/hubs" URL, is dynamically generated and defines proxy methods for the methods on the Hub class, in this case for StockTickerHub.GetAllStocks.</span></span> <span data-ttu-id="012c7-244">如果您想要的話，也可以使用[SignalR 公用程式](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手動產生此 JavaScript 檔案，並在 MapHubs 方法呼叫中停用動態檔案建立。</span><span class="sxs-lookup"><span data-stu-id="012c7-244">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) and disable dynamic file creation in the MapHubs method call.</span></span>
3. > [!IMPORTANT]
   > <span data-ttu-id="012c7-245">請確定*StockTicker*中的 JavaScript 檔案參考是正確的。</span><span class="sxs-lookup"><span data-stu-id="012c7-245">Make sure that the JavaScript file references in *StockTicker.html* are correct.</span></span> <span data-ttu-id="012c7-246">也就是說，請確定腳本卷*標*（在範例中為1.8.2）中的 jquery 版本與專案 script 資料夾中的 jquery 版本相同，並確定腳本標記中的 SignalR 版本與專案*腳本*資料夾中的 SignalR 版本相同。</span><span class="sxs-lookup"><span data-stu-id="012c7-246">That is, make sure that the jQuery version in your script tag (1.8.2 in the example) is the same as the jQuery version in your project's *Scripts* folder, and make sure that the SignalR version in your script tag is the same as the SignalR version in your project's *Scripts* folder.</span></span> <span data-ttu-id="012c7-247">必要時，請變更腳本標記中的檔案名。</span><span class="sxs-lookup"><span data-stu-id="012c7-247">Change the file names in the script tags if necessary.</span></span>
4. <span data-ttu-id="012c7-248">在**方案總管**中，以滑鼠右鍵按一下 [ *StockTicker*]，然後按一下 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-248">In **Solution Explorer**, right-click *StockTicker.html*, and then click **Set as Start Page**.</span></span>
5. <span data-ttu-id="012c7-249">在專案資料夾中建立新的 JavaScript 檔案，並將它命名為*StockTicker*。</span><span class="sxs-lookup"><span data-stu-id="012c7-249">Create a new JavaScript file in the project folder and name it *StockTicker.js*..</span></span>
6. <span data-ttu-id="012c7-250">使用下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="012c7-250">Replace the template code with the following code:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    <span data-ttu-id="012c7-251">$. connection 指的是 SignalR proxy。</span><span class="sxs-lookup"><span data-stu-id="012c7-251">$.connection refers to the SignalR proxies.</span></span> <span data-ttu-id="012c7-252">程式碼會取得 StockTickerHub 類別之 proxy 的參考，並將它放在「指示器」變數中。</span><span class="sxs-lookup"><span data-stu-id="012c7-252">The code gets a reference to the proxy for the StockTickerHub class and puts it in the ticker variable.</span></span> <span data-ttu-id="012c7-253">Proxy 名稱是由 [HubName] 屬性所設定的名稱：</span><span class="sxs-lookup"><span data-stu-id="012c7-253">The proxy name is the name that was set by the [HubName] attribute:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    <span data-ttu-id="012c7-254">定義所有變數和函式之後，檔案中的最後一行程式碼會藉由呼叫 SignalR start 函式來初始化 SignalR 連接。</span><span class="sxs-lookup"><span data-stu-id="012c7-254">After all the variables and functions are defined, the last line of code in the file initializes the SignalR connection by calling the SignalR start function.</span></span> <span data-ttu-id="012c7-255">Start 函式會以非同步方式執行並傳回[JQuery 延遲物件](http://api.jquery.com/category/deferred-object/)，這表示您可以呼叫 completed 函式，以指定在非同步作業完成時要呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="012c7-255">The start function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means you can call the done function to specify the function to call when the asynchronous operation is completed..</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    <span data-ttu-id="012c7-256">Init 函數會呼叫伺服器上的 getAllStocks 函數，並使用伺服器傳回的資訊來更新庫存資料表。</span><span class="sxs-lookup"><span data-stu-id="012c7-256">The init function calls the getAllStocks function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="012c7-257">請注意，根據預設，您必須在用戶端上使用 camel 大小寫，但在伺服器上，方法名稱是 pascal 大小寫。</span><span class="sxs-lookup"><span data-stu-id="012c7-257">Notice that by default, you have to use camel casing on the client although the method name is pascal-cased on the server.</span></span> <span data-ttu-id="012c7-258">Camel 大小寫規則僅適用于方法，而不是物件。</span><span class="sxs-lookup"><span data-stu-id="012c7-258">The camel-casing rule only applies to methods, not objects.</span></span> <span data-ttu-id="012c7-259">例如，您指的是股票。符號和股票。價格，而不是股票. 符號或股票。價格。</span><span class="sxs-lookup"><span data-stu-id="012c7-259">For example, you refer to stock.Symbol and stock.Price, not stock.symbol or stock.price.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    <span data-ttu-id="012c7-260">如果您想要在用戶端上使用 pascal 大小寫，或如果您想要使用完全不同的方法名稱，您可以使用 HubMethodName 屬性來裝飾中樞方法，方法與使用 HubName 屬性裝飾中樞類別本身的方式相同。</span><span class="sxs-lookup"><span data-stu-id="012c7-260">If you wanted to use pascal casing on the client, or if you wanted to use a completely different method name, you could decorate the Hub method with the HubMethodName attribute the same way you decorated the Hub class itself with the HubName attribute.</span></span>

    <span data-ttu-id="012c7-261">在 init 方法中，會為從伺服器接收的每個股票物件建立一個資料表資料列的 HTML，方法是呼叫 formatStock 來格式化 stock 物件的屬性，然後呼叫取代（定義于*StockTicker*的頂端），將 rowTemplate 變數中的預留位置取代為 stock 物件屬性值。</span><span class="sxs-lookup"><span data-stu-id="012c7-261">In the init method, HTML for a table row is created for each stock object received from the server by calling formatStock to format properties of the stock object, and then by calling supplant (which is defined at the top of *StockTicker.js*) to replace placeholders in the rowTemplate variable with the stock object property values.</span></span> <span data-ttu-id="012c7-262">產生的 HTML 會附加至股票資料表。</span><span class="sxs-lookup"><span data-stu-id="012c7-262">The resulting HTML is then appended to the stock table.</span></span>

    <span data-ttu-id="012c7-263">您可以呼叫 init，方法是將它傳入做為在非同步啟動函數完成後執行的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="012c7-263">You call init by passing it in as a callback function that executes after the asynchronous start function completes.</span></span> <span data-ttu-id="012c7-264">如果您在呼叫 start 之後將 init 稱為個別的 JavaScript 語句，函式會失敗，因為它會立即執行，而不會等候啟動函式完成建立連接。</span><span class="sxs-lookup"><span data-stu-id="012c7-264">If you called init as a separate JavaScript statement after calling start, the function would fail because it would execute immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="012c7-265">在此情況下，init 函數會嘗試在建立伺服器連接之前呼叫 getAllStocks 函式。</span><span class="sxs-lookup"><span data-stu-id="012c7-265">In that case, the init function would try to call the getAllStocks function before the server connection is established.</span></span>

    <span data-ttu-id="012c7-266">當伺服器變更股票價格時，它會在已連線的用戶端上呼叫 updateStockPrice。</span><span class="sxs-lookup"><span data-stu-id="012c7-266">When the server changes a stock's price, it calls the updateStockPrice on connected clients.</span></span> <span data-ttu-id="012c7-267">函式會新增至 stockTicker proxy 的用戶端屬性，讓它可供從伺服器呼叫。</span><span class="sxs-lookup"><span data-stu-id="012c7-267">The function is added to the client property of the stockTicker proxy in order to make it available to calls from the server.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    <span data-ttu-id="012c7-268">UpdateStockPrice 函數會將接收自伺服器的股票物件格式化為資料表資料列，方法與 init 函數相同。</span><span class="sxs-lookup"><span data-stu-id="012c7-268">The updateStockPrice function formats a stock object received from the server into a table row the same way as in the init function.</span></span> <span data-ttu-id="012c7-269">不過，它不會將資料列附加至資料表，而是在資料表中尋找庫存的目前資料列，並將該資料列取代為新的資料列。</span><span class="sxs-lookup"><span data-stu-id="012c7-269">However, instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

<a id="test"></a>

## <a name="test-the-application"></a><span data-ttu-id="012c7-270">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="012c7-270">Test the application</span></span>

1. <span data-ttu-id="012c7-271">按 F5 以在偵錯模式中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="012c7-271">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="012c7-272">股票資料表一開始會顯示「正在載入 ...」行，然後在短暫延遲之後顯示初始股票資料，然後再開始變更股票價格。</span><span class="sxs-lookup"><span data-stu-id="012c7-272">The stock table initially displays the "loading..." line, then after a short delay the initial stock data is displayed, and then the stock prices start to change.</span></span>

    ![正在載入](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![初始股票表](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![從伺服器接收變更的存貨資料表](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. <span data-ttu-id="012c7-276">複製瀏覽器網址列中的 URL，並將它貼到一個或多個新的瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="012c7-276">Copy the URL from the browser address bar and paste it into one or more new browser window(s).</span></span>

    <span data-ttu-id="012c7-277">初始股票顯示與第一個瀏覽器相同，而且會同時進行變更。</span><span class="sxs-lookup"><span data-stu-id="012c7-277">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>
3. <span data-ttu-id="012c7-278">關閉所有瀏覽器並開啟新的瀏覽器，然後移至相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="012c7-278">Close all browsers and open a new browser, then go to the same URL.</span></span>

    <span data-ttu-id="012c7-279">StockTicker singleton 物件已繼續在伺服器中執行，因此股票資料表顯示會顯示股票已繼續變更。</span><span class="sxs-lookup"><span data-stu-id="012c7-279">The StockTicker singleton object has continued to run in the server, so the stock table display shows that the stocks have continued to change.</span></span> <span data-ttu-id="012c7-280">（您看不到具有零變更圖形的初始資料表）。</span><span class="sxs-lookup"><span data-stu-id="012c7-280">(You don't see the initial table with zero change figures.)</span></span>
4. <span data-ttu-id="012c7-281">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="012c7-281">Close the browser.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="012c7-282">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="012c7-282">Enable logging</span></span>

<span data-ttu-id="012c7-283">SignalR 具有內建的記錄功能，可讓您在用戶端上啟用以協助進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="012c7-283">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="012c7-284">在本節中，您會啟用記錄並查看範例，以顯示記錄如何告訴您 SignalR 使用下列哪一個傳輸方法：</span><span class="sxs-lookup"><span data-stu-id="012c7-284">In this section you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

- <span data-ttu-id="012c7-285">[Websocket](http://en.wikipedia.org/wiki/WebSocket)（由 IIS 8 和目前的瀏覽器支援）。</span><span class="sxs-lookup"><span data-stu-id="012c7-285">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>
- <span data-ttu-id="012c7-286">[伺服器傳送的事件](http://en.wikipedia.org/wiki/Server-sent_events)，由 Internet Explorer 以外的瀏覽器所支援。</span><span class="sxs-lookup"><span data-stu-id="012c7-286">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>
- <span data-ttu-id="012c7-287">Internet Explorer 所支援的[永久框架](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。</span><span class="sxs-lookup"><span data-stu-id="012c7-287">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>
- <span data-ttu-id="012c7-288">所有瀏覽器都支援[Ajax 長輪詢](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。</span><span class="sxs-lookup"><span data-stu-id="012c7-288">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="012c7-289">針對任何指定的連接，SignalR 會選擇伺服器和用戶端支援的最佳傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-289">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="012c7-290">開啟*StockTicker* ，並新增一行程式碼，以便在檔案結尾初始化連接的程式碼之前立即啟用記錄：</span><span class="sxs-lookup"><span data-stu-id="012c7-290">Open *StockTicker.js* and add a line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. <span data-ttu-id="012c7-291">按 F5 執行專案。</span><span class="sxs-lookup"><span data-stu-id="012c7-291">Press F5 to run the project.</span></span>
3. <span data-ttu-id="012c7-292">開啟瀏覽器的 [開發人員工具] 視窗，然後選取主控台以查看記錄。</span><span class="sxs-lookup"><span data-stu-id="012c7-292">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="012c7-293">您可能必須重新整理頁面，才能查看 Signalr 的記錄，以協調新連接的傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-293">You might have to refresh the page to see the logs of Signalr negotiating the transport method for a new connection.</span></span>

    <span data-ttu-id="012c7-294">如果您是在 Windows 8 （IIS 8）上執行 Internet Explorer 10，傳輸方法是 Websocket。</span><span class="sxs-lookup"><span data-stu-id="012c7-294">If you are running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![IE 10 IIS 8 主控台](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    <span data-ttu-id="012c7-296">如果您是在 Windows 7 （IIS 7.5）上執行 Internet Explorer 10，則傳輸方法是 iframe。</span><span class="sxs-lookup"><span data-stu-id="012c7-296">If you are running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is iframe.</span></span>

    ![IE 10 主控台，IIS 7。5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    <span data-ttu-id="012c7-298">在 Firefox 中，安裝 Firebug 增益集以取得主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="012c7-298">In Firefox, install the Firebug add-in to get a Console window.</span></span> <span data-ttu-id="012c7-299">如果您是在 Windows 8 （IIS 8）上執行 Firefox 19，傳輸方法是 Websocket。</span><span class="sxs-lookup"><span data-stu-id="012c7-299">If you are running Firefox 19 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    <span data-ttu-id="012c7-301">如果您在 Windows 7 （IIS 7.5）上執行 Firefox 19，傳輸方法就是伺服器傳送的事件。</span><span class="sxs-lookup"><span data-stu-id="012c7-301">If you are running Firefox 19 on Windows 7 (IIS 7.5), the transport method is server-sent events.</span></span>

    ![Firefox 19 IIS 7.5 主控台](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a><span data-ttu-id="012c7-303">安裝和查看完整的 StockTicker 範例</span><span class="sxs-lookup"><span data-stu-id="012c7-303">Install and review the full StockTicker sample</span></span>

<span data-ttu-id="012c7-304">[SignalR 範例](http://nuget.org/packages/microsoft.aspnet.signalr.sample)所安裝的 StockTicker 應用程式所包含的功能，比您剛從頭建立的簡化版本還多。</span><span class="sxs-lookup"><span data-stu-id="012c7-304">The StockTicker application that is installed by the [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package includes more features than the simplified version that you just created from scratch.</span></span> <span data-ttu-id="012c7-305">在本教學課程的這一節中，您會安裝 NuGet 套件，並檢查新功能及其執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="012c7-305">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="012c7-306">安裝 SignalR NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="012c7-306">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="012c7-307">在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-307">In **Solution Explorer**, right-click the project and click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="012c7-308">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**線上**]，在 [**線上搜尋**] 方塊中輸入*SignalR* ，然後按一下**SignalR 範例**套件中的 [**安裝**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-308">In the **Manage NuGet Packages** dialog box, click **Online**, enter *SignalR.Sample* in the **Search Online** box, and then click **Install** in the **SignalR.Sample** package.</span></span>

    ![安裝 SignalR。範例套件](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. <span data-ttu-id="012c7-310">在*global.asax*檔案中，將 RouteTable 標記為批註 MapHubs （）;您稍早在應用程式中新增的行\_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-310">In the *Global.asax* file, comment out the RouteTable.Routes.MapHubs(); line that you added earlier in the Application\_Start method.</span></span>

    <span data-ttu-id="012c7-311">已不再需要*global.asax*中的程式碼，因為 SignalR 套件會在 App 中註冊 SignalR 路由 *\_啟動/RegisterHubs .cs*檔案：</span><span class="sxs-lookup"><span data-stu-id="012c7-311">The code in *Global.asax* is no longer needed because the SignalR.Sample package registers the SignalR route in the *App\_Start/RegisterHubs.cs* file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    <span data-ttu-id="012c7-312">元件屬性所參考的 WebActivator 類別包含在 WebActivatorEx NuGet 封裝中，該套件會安裝為 SignalR 套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="012c7-312">The WebActivator class that is referenced by the assembly attribute is included in the WebActivatorEx NuGet package, which is installed as a dependency of the SignalR.Sample package.</span></span>
4. <span data-ttu-id="012c7-313">在**方案總管**中，展開安裝 SignalR 範例所建立的*SignalR*資料夾。</span><span class="sxs-lookup"><span data-stu-id="012c7-313">In **Solution Explorer**, expand the *SignalR.Sample* folder which was created by installing the SignalR.Sample package.</span></span>
5. <span data-ttu-id="012c7-314">在 [ *SignalR* ] 資料夾中，以滑鼠右鍵按一下 [ *StockTicker*]，然後按一下 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="012c7-314">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then click **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="012c7-315">安裝 SignalR 時，NuGet 套件可能會變更您在 [*腳本*] 資料夾中的 jQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="012c7-315">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="012c7-316">封裝安裝在*SignalR*中的新*StockTicker*檔案會與封裝所安裝的 jQuery 版本同步，但如果您想要再次執行原始的*StockTicker .html*檔案，您可能必須先更新腳本標記中的 jquery 參考。</span><span class="sxs-lookup"><span data-stu-id="012c7-316">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="012c7-317">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="012c7-317">Run the application</span></span>

1. <span data-ttu-id="012c7-318">按 F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="012c7-318">Press F5 to run the application.</span></span>

    <span data-ttu-id="012c7-319">除了您稍早看到的方格外，「全庫存指示器」應用程式會顯示水準滾動視窗，顯示相同的股票資料。</span><span class="sxs-lookup"><span data-stu-id="012c7-319">In addition to the grid that you saw earlier, the full stock ticker application shows a horizontally scrolling window that displays the same stock data.</span></span> <span data-ttu-id="012c7-320">當您第一次執行應用程式時，「市場」會是「已關閉」，而您會看到不會滾動的靜態方格和「捲軸」視窗。</span><span class="sxs-lookup"><span data-stu-id="012c7-320">When you run the application for the first time, the "market" is "closed" and you see a static grid and a ticker window that isn't scrolling.</span></span>

    ![StockTicker 畫面啟動](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    <span data-ttu-id="012c7-322">當您按一下 [**開啟市場**] 時，[**即時股票行情**] 方塊會開始水準滾動，而伺服器會開始定期廣播股價變更。</span><span class="sxs-lookup"><span data-stu-id="012c7-322">When you click **Open Market**, the **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span> <span data-ttu-id="012c7-323">每次股票價格變更時，就會更新 [**即時股票] 資料表**方格和 [**即時股票行情**] 方塊。</span><span class="sxs-lookup"><span data-stu-id="012c7-323">Each time a stock price changes, both the **Live Stock Table** grid and the **Live Stock Ticker** box are updated.</span></span> <span data-ttu-id="012c7-324">當股票價格變更為正面時，股票會以綠色背景顯示，而當變更為負值時，股票會以紅色背景顯示。</span><span class="sxs-lookup"><span data-stu-id="012c7-324">When a stock's price change is positive, the stock is shown with a green background, and when the change is negative, the stock is shown with a red background.</span></span>

    ![StockTicker 應用程式，市場開放](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    <span data-ttu-id="012c7-326">[**關閉市場**] 按鈕會停止變更並停止捲軸，而且 [**重設**] 按鈕會在價格變更開始之前，將所有存貨資料重設為初始狀態。</span><span class="sxs-lookup"><span data-stu-id="012c7-326">The **Close Market** button stops the changes and stops the ticker scrolling, and the **Reset** button resets all stock data to the initial state before price changes started.</span></span> <span data-ttu-id="012c7-327">如果您開啟其他瀏覽器視窗並移至相同的 URL，您會看到相同的資料在每個瀏覽器中同時動態更新。</span><span class="sxs-lookup"><span data-stu-id="012c7-327">If you open more browser windows and go to the same URL, you see the same data dynamically updated at the same time in each browser.</span></span> <span data-ttu-id="012c7-328">當您按一下其中一個按鈕時，所有瀏覽器會同時以相同的方式回應。</span><span class="sxs-lookup"><span data-stu-id="012c7-328">When you click one of the buttons, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="012c7-329">即時股票行情顯示</span><span class="sxs-lookup"><span data-stu-id="012c7-329">Live Stock Ticker display</span></span>

<span data-ttu-id="012c7-330">**即時股票行情**指示器顯示是 div 元素中的未排序清單，會透過 CSS 樣式格式化成單行。</span><span class="sxs-lookup"><span data-stu-id="012c7-330">The **Live Stock Ticker** display is an unordered list in a div element that is formatted into a single line by CSS styles.</span></span> <span data-ttu-id="012c7-331">此指示器會以與資料表相同的方式進行初始化和更新：藉由取代 &lt;li&gt; 範本字串中的預留位置，並動態地將 &lt;li&gt; 專案新增至 &lt;ul&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="012c7-331">The ticker is initialized and updated the same way as the table: by replacing placeholders in a &lt;li&gt; template string and dynamically adding the &lt;li&gt; elements to the &lt;ul&gt; element.</span></span> <span data-ttu-id="012c7-332">使用 jQuery 動畫函式來執行滾動，會改變 div 內未排序清單的左邊界。</span><span class="sxs-lookup"><span data-stu-id="012c7-332">The scrolling is performed by using the jQuery animate function to vary the margin-left of the unordered list within the div.</span></span>

<span data-ttu-id="012c7-333">股票行情指示器 HTML：</span><span class="sxs-lookup"><span data-stu-id="012c7-333">The stock ticker HTML:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

<span data-ttu-id="012c7-334">股票行情指示器 CSS：</span><span class="sxs-lookup"><span data-stu-id="012c7-334">The stock ticker CSS:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

<span data-ttu-id="012c7-335">使其滾動的 jQuery 程式碼：</span><span class="sxs-lookup"><span data-stu-id="012c7-335">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="012c7-336">用戶端可以呼叫之伺服器上的其他方法</span><span class="sxs-lookup"><span data-stu-id="012c7-336">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="012c7-337">StockTickerHub 類別定義了用戶端可以呼叫的四個額外方法：</span><span class="sxs-lookup"><span data-stu-id="012c7-337">The StockTickerHub class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

<span data-ttu-id="012c7-338">系統會呼叫 OpenMarket、CloseMarket 和 Reset，以回應頁面頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="012c7-338">OpenMarket, CloseMarket, and Reset are called in response to the buttons at the top of the page.</span></span> <span data-ttu-id="012c7-339">它們會示範一個用戶端的模式，其中觸發的狀態變更會立即傳播至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="012c7-339">They demonstrate the pattern of one client triggering a change in state that is immediately propagated to all clients.</span></span> <span data-ttu-id="012c7-340">這些方法中的每一個都會呼叫 StockTicker 類別中的方法，以影響市場狀態變更，然後廣播新的狀態。</span><span class="sxs-lookup"><span data-stu-id="012c7-340">Each of these methods calls a method in the StockTicker class that effects the market state change and then broadcasts the new state.</span></span>

<span data-ttu-id="012c7-341">在 StockTicker 類別中，市場的狀態是由傳回 MarketState 列舉值的 MarketState 屬性所維護：</span><span class="sxs-lookup"><span data-stu-id="012c7-341">In the StockTicker class, the state of the market is maintained by a MarketState property that returns a MarketState enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

<span data-ttu-id="012c7-342">每個變更市場狀態的方法都會在鎖定區塊內這麼做，因為 StockTicker 類別必須是 threadsafe：</span><span class="sxs-lookup"><span data-stu-id="012c7-342">Each of the methods that change the market state do so inside a lock block because the StockTicker class has to be threadsafe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

<span data-ttu-id="012c7-343">為確保此程式碼為 threadsafe，支援 MarketState 屬性的 \_marketState 欄位會標示為 volatile，</span><span class="sxs-lookup"><span data-stu-id="012c7-343">To ensure that this code is threadsafe, the \_marketState field that backs the MarketState property is marked as volatile,</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

<span data-ttu-id="012c7-344">BroadcastMarketStateChange 和 BroadcastMarketReset 方法類似于您已看到的 BroadcastStockPrice 方法，不同的是，它們會呼叫用戶端上定義的不同方法：</span><span class="sxs-lookup"><span data-stu-id="012c7-344">The BroadcastMarketStateChange and BroadcastMarketReset methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="012c7-345">伺服器可以呼叫之用戶端上的其他函數</span><span class="sxs-lookup"><span data-stu-id="012c7-345">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="012c7-346">UpdateStockPrice 函式現在會同時處理方格和捲軸顯示，並使用 jQuery. 色彩來閃爍紅色和綠色色彩。</span><span class="sxs-lookup"><span data-stu-id="012c7-346">The updateStockPrice function now handles both the grid and the ticker display, and it uses jQuery.Color to flash red and green colors.</span></span>

<span data-ttu-id="012c7-347">*SignalR*中的新函式會根據市場狀態來啟用和停用按鈕，並停止或啟動 [捲軸] 視窗水準滾動。</span><span class="sxs-lookup"><span data-stu-id="012c7-347">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state, and they stop or start the ticker window horizontal scrolling.</span></span> <span data-ttu-id="012c7-348">因為有多個函式會新增至「指示器」，所以會使用[jQuery extend 函數](http://api.jquery.com/jQuery.extend/)來新增它們。</span><span class="sxs-lookup"><span data-stu-id="012c7-348">Since multiple functions are being added to ticker.client, the [jQuery extend function](http://api.jquery.com/jQuery.extend/) is used to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="012c7-349">建立連線後的其他用戶端設定</span><span class="sxs-lookup"><span data-stu-id="012c7-349">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="012c7-350">用戶端建立連線之後，會有一些額外的工作需要執行：找出市場是否已開啟或已關閉，以呼叫適當的 marketOpened 或 marketClosed 函式，並將伺服器方法呼叫附加至按鈕。</span><span class="sxs-lookup"><span data-stu-id="012c7-350">After the client establishes the connection, it has some additional work to do: find out if the market is open or closed in order to call the appropriate marketOpened or marketClosed function, and attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

<span data-ttu-id="012c7-351">在建立連接之後，伺服器方法不會連線到按鈕，因此程式碼無法在可用之前嘗試呼叫伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="012c7-351">The server methods are not wired up to the buttons until after the connection is established, so that the code can't try to call the server methods before they are available.</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="012c7-352">後續步驟</span><span class="sxs-lookup"><span data-stu-id="012c7-352">Next steps</span></span>

<span data-ttu-id="012c7-353">在本教學課程中，您已瞭解如何設計 SignalR 應用程式，將訊息從伺服器廣播到所有已連線的用戶端，並定期並回應來自任何用戶端的通知。</span><span class="sxs-lookup"><span data-stu-id="012c7-353">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients, both on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="012c7-354">使用多執行緒單一實例來維護伺服器狀態的模式也可以在多玩家線上遊戲案例中使用。</span><span class="sxs-lookup"><span data-stu-id="012c7-354">The pattern of using a multi-threaded singleton instance to maintain server state can also be also used in multi-player online game scenarios.</span></span> <span data-ttu-id="012c7-355">如需範例，請參閱以[SignalR 為基礎的 ShootR 遊戲](https://github.com/NTaylorMullen/ShootR)。</span><span class="sxs-lookup"><span data-stu-id="012c7-355">For an example, see [the ShootR game that is based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="012c7-356">如需顯示點對點通訊案例的教學課程，請參閱[使用 SignalR](index.md)和[使用 SignalR 進行即時更新](index.md)的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="012c7-356">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](index.md) and [Real-Time Updating with SignalR](index.md).</span></span>

<span data-ttu-id="012c7-357">若要深入瞭解更先進的 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：</span><span class="sxs-lookup"><span data-stu-id="012c7-357">To learn more advanced SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="012c7-358">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="012c7-358">ASP.NET SignalR</span></span>](https://asp.net/signalr/)
- [<span data-ttu-id="012c7-359">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="012c7-359">SignalR Project</span></span>](http://signalr.net/)
- [<span data-ttu-id="012c7-360">SignalR Github 和範例</span><span class="sxs-lookup"><span data-stu-id="012c7-360">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="012c7-361">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="012c7-361">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
