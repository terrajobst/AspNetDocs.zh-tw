---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 教學課程：使用 SignalR 2 進行伺服器廣播 |Microsoft Docs
author: tdykstra
description: 本教學課程說明如何建立使用 ASP.NET SignalR 2 來提供伺服器廣播功能的 web 應用程式。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536600"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="6c233-103">教學課程：使用 SignalR 2 進行伺服器廣播</span><span class="sxs-lookup"><span data-stu-id="6c233-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="6c233-104">本教學課程說明如何建立使用 ASP.NET SignalR 2 來提供伺服器廣播功能的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c233-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="6c233-105">伺服器廣播表示伺服器會啟動傳送到用戶端的通訊。</span><span class="sxs-lookup"><span data-stu-id="6c233-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="6c233-106">您在本教學課程中建立的應用程式會模擬股票行情指示器，這是伺服器廣播功能的一般案例。</span><span class="sxs-lookup"><span data-stu-id="6c233-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="6c233-107">伺服器會定期更新股票價格，並將更新廣播到所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c233-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="6c233-108">在瀏覽器中，[**變更**] 和 [ **%** ] 資料行中的數位和符號會動態變更，以回應來自伺服器的通知。</span><span class="sxs-lookup"><span data-stu-id="6c233-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="6c233-109">如果您對相同的 URL 開啟其他瀏覽器，它們會同時顯示相同的資料和相同的資料變更。</span><span class="sxs-lookup"><span data-stu-id="6c233-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![建立 web](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="6c233-111">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="6c233-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c233-112">建立專案</span><span class="sxs-lookup"><span data-stu-id="6c233-112">Create the project</span></span>
> * <span data-ttu-id="6c233-113">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="6c233-113">Set up the server code</span></span>
> * <span data-ttu-id="6c233-114">檢查伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="6c233-114">Examine the server code</span></span>
> * <span data-ttu-id="6c233-115">設定用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="6c233-115">Set up the client code</span></span>
> * <span data-ttu-id="6c233-116">檢查用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="6c233-116">Examine the client code</span></span>
> * <span data-ttu-id="6c233-117">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="6c233-117">Test the application</span></span>
> * <span data-ttu-id="6c233-118">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="6c233-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c233-119">如果您不想要逐步執行建立應用程式的步驟，您可以在新的空白 ASP.NET Web 應用程式專案中安裝 SignalR 封裝。</span><span class="sxs-lookup"><span data-stu-id="6c233-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="6c233-120">如果您在未執行本教學課程中的步驟的情況下安裝 NuGet 套件，則必須遵循*readme.txt*檔案中的指示。</span><span class="sxs-lookup"><span data-stu-id="6c233-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="6c233-121">若要執行封裝，您必須新增 OWIN 啟動類別，以在已安裝的封裝中呼叫 `ConfigureSignalR` 方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="6c233-122">如果您未新增 OWIN startup 類別，則會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="6c233-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="6c233-123">請參閱本文的[安裝 StockTicker 範例](#install-the-stockticker-sample)一節。</span><span class="sxs-lookup"><span data-stu-id="6c233-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c233-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c233-124">Prerequisites</span></span>

* <span data-ttu-id="6c233-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，其中包含 **ASP.NET 和 Web 部署**工作負載。</span><span class="sxs-lookup"><span data-stu-id="6c233-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="6c233-126">建立專案</span><span class="sxs-lookup"><span data-stu-id="6c233-126">Create the project</span></span>

<span data-ttu-id="6c233-127">本節說明如何使用 Visual Studio 2017 來建立空的 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c233-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="6c233-128">在 Visual Studio 中，建立 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c233-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![建立 web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="6c233-130">在 [**新增 ASP.NET Web 應用程式-SignalR StockTicker** ] 視窗中，保持選取 [**空白**]，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="6c233-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="6c233-131">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="6c233-131">Set up the server code</span></span>

<span data-ttu-id="6c233-132">在本節中，您會設定在伺服器上執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6c233-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="6c233-133">建立 Stock 類別</span><span class="sxs-lookup"><span data-stu-id="6c233-133">Create the Stock class</span></span>

<span data-ttu-id="6c233-134">您一開始會先建立用來儲存和傳送股票資訊的*股票*模型類別。</span><span class="sxs-lookup"><span data-stu-id="6c233-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="6c233-135">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **類別**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="6c233-136">將類別命名為*Stock* ，並將其新增至專案。</span><span class="sxs-lookup"><span data-stu-id="6c233-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="6c233-137">將*Stock.cs*檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="6c233-138">您在建立股票時所設定的兩個屬性是 `Symbol` （例如，MSFT for Microsoft）和 `Price`。</span><span class="sxs-lookup"><span data-stu-id="6c233-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="6c233-139">其他屬性則取決於您設定 `Price`的方式和時機。</span><span class="sxs-lookup"><span data-stu-id="6c233-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="6c233-140">第一次設定 `Price`時，值會傳播至 `DayOpen`。</span><span class="sxs-lookup"><span data-stu-id="6c233-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="6c233-141">之後，當您設定 `Price`時，應用程式會根據 `Price` 和 `DayOpen`之間的差異來計算 `Change` 和 `PercentChange` 屬性值。</span><span class="sxs-lookup"><span data-stu-id="6c233-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="6c233-142">建立 StockTickerHub 和 StockTicker 類別</span><span class="sxs-lookup"><span data-stu-id="6c233-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="6c233-143">您將使用 SignalR 中樞 API 來處理伺服器對用戶端的互動。</span><span class="sxs-lookup"><span data-stu-id="6c233-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="6c233-144">衍生自 SignalR `Hub` 類別的 `StockTickerHub` 類別將會處理來自用戶端的接收連接和方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="6c233-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="6c233-145">您也需要維護庫存資料，並執行 `Timer` 物件。</span><span class="sxs-lookup"><span data-stu-id="6c233-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="6c233-146">`Timer` 物件將定期觸發與用戶端連接無關的價格更新。</span><span class="sxs-lookup"><span data-stu-id="6c233-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="6c233-147">您無法將這些函數放在 `Hub` 類別中，因為中樞是暫時性的。</span><span class="sxs-lookup"><span data-stu-id="6c233-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="6c233-148">應用程式會為中樞上的每個工作建立一個 `Hub` 類別實例，例如從用戶端到伺服器的連接和呼叫。</span><span class="sxs-lookup"><span data-stu-id="6c233-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="6c233-149">因此，保留股票資料、更新價格，以及廣播價格更新的機制，必須在不同的類別中執行。</span><span class="sxs-lookup"><span data-stu-id="6c233-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="6c233-150">您會將類別命名為 `StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="6c233-150">You'll name the class `StockTicker`.</span></span>

![從 StockTicker 廣播](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="6c233-152">您只想要在伺服器上執行 `StockTicker` 類別的一個實例，因此您必須設定從每個 `StockTickerHub` 實例到單一 `StockTicker` 實例的參考。</span><span class="sxs-lookup"><span data-stu-id="6c233-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="6c233-153">`StockTicker` 類別必須廣播至用戶端，因為它有存貨資料和觸發程式更新，但 `StockTicker` 不是 `Hub` 類別。</span><span class="sxs-lookup"><span data-stu-id="6c233-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="6c233-154">`StockTicker` 類別必須取得 SignalR Hub 連接內容物件的參考。</span><span class="sxs-lookup"><span data-stu-id="6c233-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="6c233-155">然後，它可以使用 SignalR 連接內容物件廣播至用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c233-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="6c233-156">建立 StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="6c233-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="6c233-157">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="6c233-158">在 **[加入新專案-SignalR**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。</span><span class="sxs-lookup"><span data-stu-id="6c233-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="6c233-159">將類別命名為*StockTickerHub* ，並將它加入至專案。</span><span class="sxs-lookup"><span data-stu-id="6c233-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="6c233-160">此步驟會建立*StockTickerHub.cs*類別檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="6c233-161">同時，它會將支援 SignalR 的一組腳本檔案和元件參考加入至專案。</span><span class="sxs-lookup"><span data-stu-id="6c233-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="6c233-162">將*StockTickerHub.cs*檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="6c233-163">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-163">Save the file.</span></span>

<span data-ttu-id="6c233-164">應用程式會使用[中樞](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)類別來定義用戶端可以在伺服器上呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="6c233-165">您要定義一個方法： `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="6c233-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="6c233-166">當用戶端一開始連線到伺服器時，會呼叫此方法來取得所有股票的清單及其目前的價格。</span><span class="sxs-lookup"><span data-stu-id="6c233-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="6c233-167">方法可以同步執行並傳回 `IEnumerable<Stock>`，因為它會從記憶體傳回資料。</span><span class="sxs-lookup"><span data-stu-id="6c233-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="6c233-168">如果方法必須藉由執行需要等候的專案（例如資料庫查閱或 web 服務呼叫）來取得資料，您會將 `Task<IEnumerable<Stock>>` 指定為傳回值，以啟用非同步處理。</span><span class="sxs-lookup"><span data-stu-id="6c233-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="6c233-169">如需詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-何時以非同步方式執行](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。</span><span class="sxs-lookup"><span data-stu-id="6c233-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="6c233-170">`HubName` 屬性會指定應用程式將如何在用戶端上參考 JavaScript 程式碼中的中樞。</span><span class="sxs-lookup"><span data-stu-id="6c233-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="6c233-171">如果您不使用這個屬性，用戶端上的預設名稱會是類別名稱的 camelCase 版本，在此情況下 `stockTickerHub`。</span><span class="sxs-lookup"><span data-stu-id="6c233-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="6c233-172">您稍後會在建立 `StockTicker` 類別時看到，應用程式會在其靜態 `Instance` 屬性中建立該類別的單一實例。</span><span class="sxs-lookup"><span data-stu-id="6c233-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="6c233-173">無論有多少用戶端連線或中斷連接，`StockTicker` 的單一實例都在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="6c233-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="6c233-174">該實例是 `GetAllStocks()` 方法用來傳回目前股票資訊的內容。</span><span class="sxs-lookup"><span data-stu-id="6c233-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="6c233-175">建立 StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="6c233-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="6c233-176">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **類別**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="6c233-177">將類別命名為*StockTicker* ，並將它加入至專案。</span><span class="sxs-lookup"><span data-stu-id="6c233-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="6c233-178">將*StockTicker.cs*檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="6c233-179">由於所有線程都會執行相同的 StockTicker 程式碼實例，因此 StockTicker 類別必須是安全線程。</span><span class="sxs-lookup"><span data-stu-id="6c233-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="6c233-180">檢查伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="6c233-180">Examine the server code</span></span>

<span data-ttu-id="6c233-181">如果您檢查伺服器程式碼，它會協助您瞭解應用程式的運作方式。</span><span class="sxs-lookup"><span data-stu-id="6c233-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="6c233-182">將單一實例儲存在靜態欄位中</span><span class="sxs-lookup"><span data-stu-id="6c233-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="6c233-183">程式碼會初始化靜態 `_instance` 欄位，以使用類別的實例來支援 `Instance` 屬性。</span><span class="sxs-lookup"><span data-stu-id="6c233-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="6c233-184">因為此函式是私用的，所以它是應用程式可以建立之類別的唯一實例。</span><span class="sxs-lookup"><span data-stu-id="6c233-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="6c233-185">應用程式會針對 `_instance` 欄位使用[延遲初始化](/dotnet/framework/performance/lazy-initialization)。</span><span class="sxs-lookup"><span data-stu-id="6c233-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="6c233-186">基於效能的考慮，這並不適用。</span><span class="sxs-lookup"><span data-stu-id="6c233-186">It's not for performance reasons.</span></span> <span data-ttu-id="6c233-187">這是為了確保實例建立是安全線程。</span><span class="sxs-lookup"><span data-stu-id="6c233-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="6c233-188">每次用戶端連接到伺服器時，在個別執行緒中執行之 StockTickerHub 類別的新實例會從 `StockTicker.Instance` 靜態屬性取得 StockTicker 單一實例，如您稍早在 `StockTickerHub` 類別中所見。</span><span class="sxs-lookup"><span data-stu-id="6c233-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="6c233-189">將存貨資料儲存在 ConcurrentDictionary 中</span><span class="sxs-lookup"><span data-stu-id="6c233-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="6c233-190">此函式會使用一些範例股票資料來初始化 `_stocks` 集合，而 `GetAllStocks` 會傳回股票。</span><span class="sxs-lookup"><span data-stu-id="6c233-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="6c233-191">如您稍早所見，這組股票會由 `StockTickerHub.GetAllStocks`傳回，這是用戶端可以呼叫 `Hub` 類別中的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="6c233-192">股票集合會定義為執行緒安全性的[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)類型。</span><span class="sxs-lookup"><span data-stu-id="6c233-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="6c233-193">或者，您可以使用[dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)物件，並在進行變更時明確地鎖定字典。</span><span class="sxs-lookup"><span data-stu-id="6c233-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="6c233-194">針對此範例應用程式，您可以將應用程式資料儲存在記憶體中，並在應用程式處置 `StockTicker` 實例時遺失資料。</span><span class="sxs-lookup"><span data-stu-id="6c233-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="6c233-195">在實際的應用程式中，您可以使用資料庫之類的後端資料存放區。</span><span class="sxs-lookup"><span data-stu-id="6c233-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="6c233-196">定期更新股票價格</span><span class="sxs-lookup"><span data-stu-id="6c233-196">Periodically updating stock prices</span></span>

<span data-ttu-id="6c233-197">此函式會啟動一個 `Timer` 物件，定期呼叫會隨機更新股票價格的方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="6c233-198">`Timer` 會呼叫 `UpdateStockPrices`，這會在 state 參數中傳遞 null。</span><span class="sxs-lookup"><span data-stu-id="6c233-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="6c233-199">更新價格之前，應用程式會在 `_updateStockPricesLock` 物件上取得鎖定。</span><span class="sxs-lookup"><span data-stu-id="6c233-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="6c233-200">程式碼會檢查另一個執行緒是否已更新價格，然後在清單中的每個股票上呼叫 `TryUpdateStockPrice`。</span><span class="sxs-lookup"><span data-stu-id="6c233-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="6c233-201">`TryUpdateStockPrice` 方法會決定是否要變更股票價格，以及要變更的數量。</span><span class="sxs-lookup"><span data-stu-id="6c233-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="6c233-202">如果股票價格變更，應用程式會呼叫 `BroadcastStockPrice`，以廣播所有已連線用戶端的股票價格變更。</span><span class="sxs-lookup"><span data-stu-id="6c233-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="6c233-203">指定為[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)的 `_updatingStockPrices` 旗標，以確保它是安全線程。</span><span class="sxs-lookup"><span data-stu-id="6c233-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="6c233-204">在實際的應用程式中，`TryUpdateStockPrice` 方法會呼叫 web 服務來查閱價格。</span><span class="sxs-lookup"><span data-stu-id="6c233-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="6c233-205">在此程式碼中，應用程式會使用亂數字產生器來隨機進行變更。</span><span class="sxs-lookup"><span data-stu-id="6c233-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="6c233-206">取得 SignalR 內容，讓 StockTicker 類別可以廣播至用戶端</span><span class="sxs-lookup"><span data-stu-id="6c233-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="6c233-207">因為價格變更會在 `StockTicker` 物件中產生，所以必須在所有已連線的用戶端上呼叫 `updateStockPrice` 方法的物件。</span><span class="sxs-lookup"><span data-stu-id="6c233-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="6c233-208">在 `Hub` 類別中，您有可呼叫用戶端方法的 API，但 `StockTicker` 不是衍生自 `Hub` 類別，而且沒有任何 `Hub` 物件的參考。</span><span class="sxs-lookup"><span data-stu-id="6c233-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="6c233-209">若要廣播至已連線的用戶端，`StockTicker` 類別必須取得 `StockTickerHub` 類別的 SignalR 內容實例，並使用它來呼叫用戶端上的方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="6c233-210">程式碼會在建立單一類別實例時取得 SignalR 內容的參考，將該參考傳遞給此函式，而此函式會將它放在 `Clients` 屬性中。</span><span class="sxs-lookup"><span data-stu-id="6c233-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="6c233-211">當您只想要取得內容一次時，有兩個原因：取得內容是一項昂貴的工作，而且只要取得，就能確保應用程式保留傳送給用戶端的預期訊息順序。</span><span class="sxs-lookup"><span data-stu-id="6c233-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="6c233-212">取得內容的 `Clients` 屬性，並將它放在 `StockTickerClient` 屬性中，可讓您撰寫程式碼來呼叫用戶端方法，其外觀與在 `Hub` 類別中相同。</span><span class="sxs-lookup"><span data-stu-id="6c233-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="6c233-213">比方說，若要廣播至所有用戶端，您可以 `Clients.All.updateStockPrice(stock)`寫入。</span><span class="sxs-lookup"><span data-stu-id="6c233-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="6c233-214">您在 `BroadcastStockPrice` 中呼叫的 `updateStockPrice` 方法尚不存在。</span><span class="sxs-lookup"><span data-stu-id="6c233-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="6c233-215">稍後當您撰寫在用戶端上執行的程式碼時，您將會新增它。</span><span class="sxs-lookup"><span data-stu-id="6c233-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="6c233-216">您可以參考這裡的 `updateStockPrice`，因為 `Clients.All` 是動態的，這表示應用程式會在執行時間評估運算式。</span><span class="sxs-lookup"><span data-stu-id="6c233-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="6c233-217">當這個方法呼叫執行時，SignalR 會將方法名稱和參數值傳送給用戶端，如果用戶端具有名為 `updateStockPrice`的方法，應用程式將會呼叫該方法，並將參數值傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="6c233-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="6c233-218">`Clients.All` 表示傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c233-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="6c233-219">SignalR 提供您其他選項來指定要傳送至哪些用戶端或用戶端群組。</span><span class="sxs-lookup"><span data-stu-id="6c233-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="6c233-220">如需詳細資訊，請參閱[HubConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6c233-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="6c233-221">註冊 SignalR 路由</span><span class="sxs-lookup"><span data-stu-id="6c233-221">Register the SignalR route</span></span>

<span data-ttu-id="6c233-222">伺服器必須知道要攔截並直接 SignalR 的 URL。</span><span class="sxs-lookup"><span data-stu-id="6c233-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="6c233-223">若要這麼做，請新增 OWIN 啟動類別：</span><span class="sxs-lookup"><span data-stu-id="6c233-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="6c233-224">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="6c233-225">在 **加入新專案-SignalR**  中，選取 **已安裝** > **Visual C#**  > **Web** ，然後選取  **OWIN 啟動類別**。</span><span class="sxs-lookup"><span data-stu-id="6c233-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="6c233-226">將類別命名為*Startup* ，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="6c233-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="6c233-227">使用下列程式碼取代*Startup.cs*檔案中的預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="6c233-228">您現在已完成伺服器程式碼的設定。</span><span class="sxs-lookup"><span data-stu-id="6c233-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="6c233-229">在下一節中，您將設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c233-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="6c233-230">設定用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="6c233-230">Set up the client code</span></span>

<span data-ttu-id="6c233-231">在本節中，您會設定在用戶端上執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6c233-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="6c233-232">建立 HTML 網頁和 JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="6c233-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="6c233-233">HTML 網頁會顯示資料，而 JavaScript 檔案會組織資料。</span><span class="sxs-lookup"><span data-stu-id="6c233-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="6c233-234">建立 StockTicker</span><span class="sxs-lookup"><span data-stu-id="6c233-234">Create StockTicker.html</span></span>

<span data-ttu-id="6c233-235">首先，您要加入 HTML 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c233-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="6c233-236">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **HTML 網頁**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="6c233-237">將檔案命名為*StockTicker* ，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="6c233-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="6c233-238">將*StockTicker*中的預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="6c233-239">HTML 會建立具有五個數據行的資料表、一個標題列，以及一個橫跨所有五個數據行的單一儲存格。</span><span class="sxs-lookup"><span data-stu-id="6c233-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="6c233-240">資料列顯示「正在載入 ...」當應用程式啟動時，很快就會發生。</span><span class="sxs-lookup"><span data-stu-id="6c233-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="6c233-241">JavaScript 程式碼將會移除該資料列，並加入其位置列，其中包含從伺服器抓取的股票資料。</span><span class="sxs-lookup"><span data-stu-id="6c233-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="6c233-242">腳本標記會指定：</span><span class="sxs-lookup"><span data-stu-id="6c233-242">The script tags specify:</span></span>

    * <span data-ttu-id="6c233-243">JQuery 腳本檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-243">The jQuery script file.</span></span>

    * <span data-ttu-id="6c233-244">SignalR 核心腳本檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="6c233-245">SignalR proxy 腳本檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="6c233-246">稍後將建立的 StockTicker 腳本檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="6c233-247">應用程式會動態產生 SignalR proxy 腳本檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="6c233-248">它會指定 "/signalr/hubs" URL，並為中樞類別上的方法定義 proxy 方法，在此案例中為 `StockTickerHub.GetAllStocks`。</span><span class="sxs-lookup"><span data-stu-id="6c233-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="6c233-249">如果您想要的話，也可以使用[SignalR 公用程式](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)，以手動方式產生此 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="6c233-250">別忘了在 `MapHubs` 方法呼叫中停用動態檔案建立。</span><span class="sxs-lookup"><span data-stu-id="6c233-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="6c233-251">在**方案總管**中，展開 [**腳本**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="6c233-252">JQuery 和 SignalR 的腳本程式庫會顯示在專案中。</span><span class="sxs-lookup"><span data-stu-id="6c233-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6c233-253">封裝管理員將會安裝較新版本的 SignalR 腳本。</span><span class="sxs-lookup"><span data-stu-id="6c233-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="6c233-254">更新程式碼區塊中的腳本參考，以對應至專案中的腳本檔案版本。</span><span class="sxs-lookup"><span data-stu-id="6c233-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="6c233-255">在**方案總管**中，以滑鼠右鍵按一下 [ *StockTicker*]，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="6c233-256">建立 StockTicker</span><span class="sxs-lookup"><span data-stu-id="6c233-256">Create StockTicker.js</span></span>

<span data-ttu-id="6c233-257">現在建立 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="6c233-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="6c233-258">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **JavaScript**檔案]。</span><span class="sxs-lookup"><span data-stu-id="6c233-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="6c233-259">將檔案命名為*StockTicker* ，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="6c233-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="6c233-260">將下列程式碼新增至*StockTicker*檔案：</span><span class="sxs-lookup"><span data-stu-id="6c233-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="6c233-261">檢查用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="6c233-261">Examine the client code</span></span>

<span data-ttu-id="6c233-262">如果您檢查用戶端程式代碼，它會協助您瞭解用戶端程式代碼如何與伺服器程式碼互動，以讓應用程式正常執行。</span><span class="sxs-lookup"><span data-stu-id="6c233-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="6c233-263">啟動連接</span><span class="sxs-lookup"><span data-stu-id="6c233-263">Starting the connection</span></span>

<span data-ttu-id="6c233-264">`$.connection` 是指 SignalR proxy。</span><span class="sxs-lookup"><span data-stu-id="6c233-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="6c233-265">程式碼會取得 `StockTickerHub` 類別之 proxy 的參考，並將它放在 `ticker` 變數中。</span><span class="sxs-lookup"><span data-stu-id="6c233-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="6c233-266">Proxy 名稱是 `HubName` 屬性所設定的名稱：</span><span class="sxs-lookup"><span data-stu-id="6c233-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="6c233-267">定義所有變數和函數之後，檔案中的最後一行程式碼會藉由呼叫 SignalR `start` 函式來初始化 SignalR 連接。</span><span class="sxs-lookup"><span data-stu-id="6c233-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="6c233-268">`start` 函式會以非同步方式執行，並傳回[JQuery 延遲物件](http://api.jquery.com/category/deferred-object/)。</span><span class="sxs-lookup"><span data-stu-id="6c233-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="6c233-269">您可以呼叫完成函式，以指定當應用程式完成非同步動作時所要呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="6c233-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="6c233-270">取得所有股票</span><span class="sxs-lookup"><span data-stu-id="6c233-270">Getting all the stocks</span></span>

<span data-ttu-id="6c233-271">`init` 函式會在伺服器上呼叫 `getAllStocks` 函數，並使用伺服器傳回的資訊來更新庫存資料表。</span><span class="sxs-lookup"><span data-stu-id="6c233-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="6c233-272">請注意，根據預設，您必須在用戶端上使用 camelCasing，即使伺服器上的方法名稱是 pascal 大小寫也一樣。</span><span class="sxs-lookup"><span data-stu-id="6c233-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="6c233-273">CamelCasing 規則僅適用于方法，而不是物件。</span><span class="sxs-lookup"><span data-stu-id="6c233-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="6c233-274">例如，您指的是 `stock.Symbol` 和 `stock.Price`，而不是 `stock.symbol` 或 `stock.price`。</span><span class="sxs-lookup"><span data-stu-id="6c233-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="6c233-275">在 `init` 方法中，應用程式會藉由呼叫 `formatStock` 來格式化 `stock` 物件的屬性，然後呼叫 `supplant` 將 `rowTemplate` 變數中的預留位置取代為 `stock` 物件屬性值，為每個從伺服器接收的股票物件建立 HTML。</span><span class="sxs-lookup"><span data-stu-id="6c233-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="6c233-276">產生的 HTML 會附加至股票資料表。</span><span class="sxs-lookup"><span data-stu-id="6c233-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="6c233-277">您可以呼叫 `init`，方法是將它傳入做為 `callback` 函式，該函式會在非同步 `start` 函數完成後執行。</span><span class="sxs-lookup"><span data-stu-id="6c233-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="6c233-278">如果您在呼叫 `start`之後，以個別的 JavaScript 語句來呼叫 `init`，此函式會失敗，因為它會立即執行，而不會等候啟動函數完成建立連接。</span><span class="sxs-lookup"><span data-stu-id="6c233-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="6c233-279">在此情況下，`init` 函式會先嘗試呼叫 `getAllStocks` 函式，應用程式才會建立伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="6c233-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="6c233-280">取得更新的股票價格</span><span class="sxs-lookup"><span data-stu-id="6c233-280">Getting updated stock prices</span></span>

<span data-ttu-id="6c233-281">當伺服器變更股票價格時，它會在已連線的用戶端上呼叫 `updateStockPrice`。</span><span class="sxs-lookup"><span data-stu-id="6c233-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="6c233-282">應用程式會將函式新增至 `stockTicker` proxy 的用戶端屬性，使其可供從伺服器呼叫。</span><span class="sxs-lookup"><span data-stu-id="6c233-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="6c233-283">`updateStockPrice` 函數會依照 `init` 函數中的相同方式，將從伺服器接收的股票物件格式化為資料表資料列。</span><span class="sxs-lookup"><span data-stu-id="6c233-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="6c233-284">它不會將資料列附加至資料表，而是在資料表中尋找庫存的目前資料列，並將該資料列取代為新的資料列。</span><span class="sxs-lookup"><span data-stu-id="6c233-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="6c233-285">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="6c233-285">Test the application</span></span>

<span data-ttu-id="6c233-286">您可以測試應用程式以確定其運作正常。</span><span class="sxs-lookup"><span data-stu-id="6c233-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="6c233-287">您會看到所有的瀏覽器視窗都會顯示股票價格變動的即時股票資料表。</span><span class="sxs-lookup"><span data-stu-id="6c233-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="6c233-288">在工具列中，開啟 [**腳本調試**程式]，然後選取 [播放] 按鈕，以在 [偵測模式] 中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c233-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![使用者開啟偵錯模式和選取 [播放] 的螢幕擷取畫面。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="6c233-290">瀏覽器視窗隨即開啟，並顯示 [**即時股票] 資料表**。</span><span class="sxs-lookup"><span data-stu-id="6c233-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="6c233-291">Stock 資料表一開始會顯示「正在載入 ...」一行之後，應用程式就會顯示初始股票資料，然後再開始變更股票價格。</span><span class="sxs-lookup"><span data-stu-id="6c233-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="6c233-292">從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="6c233-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="6c233-293">初始股票顯示與第一個瀏覽器相同，而且會同時進行變更。</span><span class="sxs-lookup"><span data-stu-id="6c233-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="6c233-294">關閉所有瀏覽器，開啟新的瀏覽器，然後移至相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="6c233-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="6c233-295">StockTicker singleton 物件會繼續在伺服器中執行。</span><span class="sxs-lookup"><span data-stu-id="6c233-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="6c233-296">[ **Live Stock] 資料表**顯示股票已繼續變更。</span><span class="sxs-lookup"><span data-stu-id="6c233-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="6c233-297">您看不到具有零變更圖形的初始資料表。</span><span class="sxs-lookup"><span data-stu-id="6c233-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="6c233-298">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6c233-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="6c233-299">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="6c233-299">Enable logging</span></span>

<span data-ttu-id="6c233-300">SignalR 具有內建的記錄功能，可讓您在用戶端上啟用以協助進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="6c233-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="6c233-301">在本節中，您會啟用記錄功能，並查看說明記錄如何告訴您 SignalR 使用下列哪一個傳輸方法的範例：</span><span class="sxs-lookup"><span data-stu-id="6c233-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="6c233-302">[Websocket](http://en.wikipedia.org/wiki/WebSocket)（由 IIS 8 和目前的瀏覽器支援）。</span><span class="sxs-lookup"><span data-stu-id="6c233-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="6c233-303">[伺服器傳送的事件](http://en.wikipedia.org/wiki/Server-sent_events)，由 Internet Explorer 以外的瀏覽器所支援。</span><span class="sxs-lookup"><span data-stu-id="6c233-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="6c233-304">Internet Explorer 所支援的[永久框架](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。</span><span class="sxs-lookup"><span data-stu-id="6c233-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="6c233-305">所有瀏覽器都支援[Ajax 長輪詢](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。</span><span class="sxs-lookup"><span data-stu-id="6c233-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="6c233-306">針對任何指定的連接，SignalR 會選擇伺服器和用戶端支援的最佳傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="6c233-307">開啟*StockTicker*。</span><span class="sxs-lookup"><span data-stu-id="6c233-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="6c233-308">新增這個反白顯示的程式程式碼，以便在檔案結尾初始化連接的程式碼之前立即啟用記錄：</span><span class="sxs-lookup"><span data-stu-id="6c233-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="6c233-309">按 **F5** 執行專案。</span><span class="sxs-lookup"><span data-stu-id="6c233-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="6c233-310">開啟瀏覽器的 [開發人員工具] 視窗，然後選取主控台以查看記錄。</span><span class="sxs-lookup"><span data-stu-id="6c233-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="6c233-311">您可能必須重新整理頁面，才能查看 SignalR 的記錄，以協調新連接的傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="6c233-312">如果您是在 Windows 8 （IIS 8）上執行 Internet Explorer 10，傳輸方法是**websocket**。</span><span class="sxs-lookup"><span data-stu-id="6c233-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="6c233-313">如果您是在 Windows 7 （IIS 7.5）上執行 Internet Explorer 10，則傳輸方法是**iframe**。</span><span class="sxs-lookup"><span data-stu-id="6c233-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="6c233-314">如果您是在 Windows 8 （IIS 8）上執行 Firefox 19，傳輸方法是**websocket**。</span><span class="sxs-lookup"><span data-stu-id="6c233-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="6c233-315">在 Firefox 中，安裝 Firebug 增益集以取得主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="6c233-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="6c233-316">如果您是在 Windows 7 （IIS 7.5）上執行 Firefox 19，傳輸方法就是**伺服器傳送**的事件。</span><span class="sxs-lookup"><span data-stu-id="6c233-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="6c233-317">安裝 StockTicker 範例</span><span class="sxs-lookup"><span data-stu-id="6c233-317">Install the StockTicker sample</span></span>

<span data-ttu-id="6c233-318">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample)會安裝 StockTicker 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c233-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="6c233-319">NuGet 套件包含的功能比您從頭建立的簡化版本還多。</span><span class="sxs-lookup"><span data-stu-id="6c233-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="6c233-320">在本教學課程的這一節中，您會安裝 NuGet 套件，並檢查新功能及其執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6c233-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c233-321">如果您在未執行本教學課程的先前步驟的情況下安裝套件，您必須將 OWIN 啟動類別新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6c233-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="6c233-322">此 NuGet 套件的 readme.txt 檔案會說明此步驟。</span><span class="sxs-lookup"><span data-stu-id="6c233-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="6c233-323">安裝 SignalR NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="6c233-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="6c233-324">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="6c233-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="6c233-325">在**NuGet 套件管理員中： SignalR. StockTicker**，選取 **[流覽]** 。</span><span class="sxs-lookup"><span data-stu-id="6c233-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="6c233-326">在 [**套件來源**] 中，選取 [ **nuget.org**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="6c233-327">在搜尋方塊中輸入*SignalR* ，然後選取 [ **SignalR. 範例** > **安裝**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="6c233-328">在**方案總管**中，展開 [ *SignalR* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="6c233-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="6c233-329">安裝 SignalR 套件時，會建立資料夾及其內容。</span><span class="sxs-lookup"><span data-stu-id="6c233-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="6c233-330">在 [ *SignalR* ] 資料夾中，以滑鼠右鍵按一下 [ *StockTicker*]，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6c233-331">安裝 SignalR 時，NuGet 套件可能會變更您在 [*腳本*] 資料夾中的 jQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="6c233-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="6c233-332">封裝安裝在*SignalR*中的新*StockTicker*檔案會與封裝所安裝的 jQuery 版本同步，但如果您想要再次執行原始的*StockTicker .html*檔案，您可能必須先更新腳本標記中的 jquery 參考。</span><span class="sxs-lookup"><span data-stu-id="6c233-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="6c233-333">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6c233-333">Run the application</span></span>

 <span data-ttu-id="6c233-334">您在第一個應用程式中看到的資料表具有有用的功能。</span><span class="sxs-lookup"><span data-stu-id="6c233-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="6c233-335">「全庫存指示器」應用程式會顯示新功能：顯示股票資料的水準滾動視窗，以及變更色彩隨著上升和落的股票。</span><span class="sxs-lookup"><span data-stu-id="6c233-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="6c233-336">按下 **F5** 即可執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c233-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="6c233-337">當您第一次執行應用程式時，「市場」會是「已關閉」，而您會看到靜態資料表和不會滾動的「捲軸」視窗。</span><span class="sxs-lookup"><span data-stu-id="6c233-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="6c233-338">選取 [**開放市場**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-338">Select **Open Market**.</span></span>

    ![即時報價的螢幕擷取畫面。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="6c233-340">[**即時股票行情**] 方塊會開始水準滾動，而伺服器會開始定期廣播股價變更。</span><span class="sxs-lookup"><span data-stu-id="6c233-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="6c233-341">每次股票價格變更時，應用程式都會更新**即時股票資料表**和**即時股票行情**指示器。</span><span class="sxs-lookup"><span data-stu-id="6c233-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="6c233-342">當股票價格變更為正面時，應用程式會以綠色背景顯示股票。</span><span class="sxs-lookup"><span data-stu-id="6c233-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="6c233-343">當變更為負值時，應用程式會以紅色背景顯示股票。</span><span class="sxs-lookup"><span data-stu-id="6c233-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="6c233-344">選取 [**關閉市場**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="6c233-345">資料表更新會停止。</span><span class="sxs-lookup"><span data-stu-id="6c233-345">The table updates stop.</span></span>

    * <span data-ttu-id="6c233-346">此指示器會停止滾動。</span><span class="sxs-lookup"><span data-stu-id="6c233-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="6c233-347">選取 [**重設**]。</span><span class="sxs-lookup"><span data-stu-id="6c233-347">Select **Reset**.</span></span>

    * <span data-ttu-id="6c233-348">所有的存貨資料都會重設。</span><span class="sxs-lookup"><span data-stu-id="6c233-348">All stock data is reset.</span></span>

    * <span data-ttu-id="6c233-349">應用程式會在價格變更開始前，先還原初始狀態。</span><span class="sxs-lookup"><span data-stu-id="6c233-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="6c233-350">從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="6c233-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="6c233-351">您會看到相同的資料在每個瀏覽器中同時動態更新。</span><span class="sxs-lookup"><span data-stu-id="6c233-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="6c233-352">當您選取任何控制項時，所有瀏覽器會同時以相同的方式回應。</span><span class="sxs-lookup"><span data-stu-id="6c233-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="6c233-353">即時股票行情顯示</span><span class="sxs-lookup"><span data-stu-id="6c233-353">Live Stock Ticker display</span></span>

<span data-ttu-id="6c233-354">**即時股票行情**指示器顯示是在 `<div>` 專案中，以 CSS 樣式格式化成單行的未排序清單。</span><span class="sxs-lookup"><span data-stu-id="6c233-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="6c233-355">應用程式會使用與資料表相同的方式來初始化和更新「滾動框」：藉由取代 `<li>` 範本字串中的預留位置，並動態地將 `<li>` 元素新增至 `<ul>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6c233-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="6c233-356">應用程式包含使用 jQuery `animate` 函式的滾動，來改變 `<div>`內未排序清單的左邊界。</span><span class="sxs-lookup"><span data-stu-id="6c233-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="6c233-357">SignalR. Sample StockTicker .html</span><span class="sxs-lookup"><span data-stu-id="6c233-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="6c233-358">股票行情指示器 HTML 程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="6c233-359">SignalR. Sample StockTicker .css</span><span class="sxs-lookup"><span data-stu-id="6c233-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="6c233-360">股票行情指示器 CSS 程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="6c233-361">SignalR. Sample SignalR. StockTicker .js</span><span class="sxs-lookup"><span data-stu-id="6c233-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="6c233-362">使其滾動的 jQuery 程式碼：</span><span class="sxs-lookup"><span data-stu-id="6c233-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="6c233-363">用戶端可以呼叫之伺服器上的其他方法</span><span class="sxs-lookup"><span data-stu-id="6c233-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="6c233-364">為了增加應用程式的彈性，應用程式可以呼叫其他方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="6c233-365">SignalR. Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="6c233-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="6c233-366">`StockTickerHub` 類別定義了用戶端可以呼叫的四個額外方法：</span><span class="sxs-lookup"><span data-stu-id="6c233-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="6c233-367">應用程式會呼叫 `OpenMarket`、`CloseMarket`和 `Reset`，以回應頁面頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c233-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="6c233-368">它們會示範一個用戶端的模式，觸發狀態變更立即傳播至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c233-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="6c233-369">這些方法中的每一個都會呼叫 `StockTicker` 類別中的方法，這會導致市場狀態變更，然後廣播新的狀態。</span><span class="sxs-lookup"><span data-stu-id="6c233-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="6c233-370">SignalR. Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="6c233-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="6c233-371">在 `StockTicker` 類別中，應用程式會以傳回 `MarketState` 列舉值的 `MarketState` 屬性，來維護市場的狀態：</span><span class="sxs-lookup"><span data-stu-id="6c233-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="6c233-372">每個變更市場狀態的方法都會在鎖定區塊內這麼做，因為 `StockTicker` 類別必須是安全線程：</span><span class="sxs-lookup"><span data-stu-id="6c233-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="6c233-373">為確保此程式碼為安全線程，`_marketState` 欄位會支援指定 `volatile`的 `MarketState` 屬性：</span><span class="sxs-lookup"><span data-stu-id="6c233-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="6c233-374">`BroadcastMarketStateChange` 和 `BroadcastMarketReset` 方法與您已見過的 BroadcastStockPrice 方法類似，不同之處在于它們會呼叫用戶端上定義的不同方法：</span><span class="sxs-lookup"><span data-stu-id="6c233-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="6c233-375">伺服器可以呼叫之用戶端上的其他函數</span><span class="sxs-lookup"><span data-stu-id="6c233-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="6c233-376">`updateStockPrice` 函式現在會同時處理資料表和捲軸顯示，並使用 `jQuery.Color` 來閃爍紅色和綠色色彩。</span><span class="sxs-lookup"><span data-stu-id="6c233-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="6c233-377">*SignalR. StockTicker*中的新函式會根據市場狀態來啟用和停用按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c233-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="6c233-378">他們也會停止或啟動**即時股票**指示器水準滾動。</span><span class="sxs-lookup"><span data-stu-id="6c233-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="6c233-379">由於有許多函式會新增至 `ticker.client`，因此應用程式會使用[jQuery extend](http://api.jquery.com/jQuery.extend/)函式來新增這些函數。</span><span class="sxs-lookup"><span data-stu-id="6c233-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="6c233-380">建立連線後的其他用戶端設定</span><span class="sxs-lookup"><span data-stu-id="6c233-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="6c233-381">用戶端建立連線之後，還有一些額外的工作要執行：</span><span class="sxs-lookup"><span data-stu-id="6c233-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="6c233-382">找出市場是否已開啟或已關閉，以呼叫適當的 `marketOpened` 或 `marketClosed` 函數。</span><span class="sxs-lookup"><span data-stu-id="6c233-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="6c233-383">將伺服器方法呼叫附加至按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c233-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="6c233-384">直到應用程式建立連線之後，伺服器方法才會連接到按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c233-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="6c233-385">這是為了讓程式碼無法在可用之前呼叫伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="6c233-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c233-386">其他資源</span><span class="sxs-lookup"><span data-stu-id="6c233-386">Additional resources</span></span>

<span data-ttu-id="6c233-387">在本教學課程中，您已瞭解如何設計 SignalR 應用程式，以將訊息從伺服器廣播到所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c233-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="6c233-388">現在您可以定期廣播訊息，並回應來自任何用戶端的通知。</span><span class="sxs-lookup"><span data-stu-id="6c233-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="6c233-389">您可以使用多執行緒單一實例的概念，在多玩家的線上遊戲案例中維護伺服器狀態。</span><span class="sxs-lookup"><span data-stu-id="6c233-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="6c233-390">如需範例，請參閱以[SignalR 為基礎的 ShootR 遊戲](https://github.com/NTaylorMullen/ShootR)。</span><span class="sxs-lookup"><span data-stu-id="6c233-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="6c233-391">如需顯示點對點通訊案例的教學課程，請參閱[使用 SignalR](introduction-to-signalr.md)和[使用 SignalR 進行即時更新](tutorial-high-frequency-realtime-with-signalr.md)的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="6c233-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="6c233-392">如需 SignalR 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="6c233-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="6c233-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="6c233-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="6c233-394">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="6c233-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="6c233-395">SignalR GitHub 和範例</span><span class="sxs-lookup"><span data-stu-id="6c233-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="6c233-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="6c233-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="6c233-397">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c233-397">Next steps</span></span>

<span data-ttu-id="6c233-398">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="6c233-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c233-399">建立專案</span><span class="sxs-lookup"><span data-stu-id="6c233-399">Created the project</span></span>
> * <span data-ttu-id="6c233-400">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="6c233-400">Set up the server code</span></span>
> * <span data-ttu-id="6c233-401">檢查伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="6c233-401">Examined the server code</span></span>
> * <span data-ttu-id="6c233-402">設定用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="6c233-402">Set up the client code</span></span>
> * <span data-ttu-id="6c233-403">檢查用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="6c233-403">Examined the client code</span></span>
> * <span data-ttu-id="6c233-404">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="6c233-404">Tested the application</span></span>
> * <span data-ttu-id="6c233-405">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="6c233-405">Enabled logging</span></span>

<span data-ttu-id="6c233-406">前進到下一篇文章，以瞭解如何建立使用 ASP.NET SignalR 2 的即時 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c233-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6c233-407">使用 SignalR 建立即時 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6c233-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
