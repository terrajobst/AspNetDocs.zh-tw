---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 教學課程：使用 SignalR 2 建立高頻率即時應用程式 |Microsoft Docs
author: bradygaster
description: 本教學課程說明如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供高頻率的訊息功能。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600460"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="f1bed-103">教學課程：使用 SignalR 2 建立高頻率即時應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="f1bed-104">本教學課程示範如何建立使用 ASP.NET SignalR 2 的 web 應用程式，以提供高頻率的訊息功能。</span><span class="sxs-lookup"><span data-stu-id="f1bed-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="f1bed-105">在此情況下，「高頻率訊息」表示伺服器會以固定的速率傳送更新。</span><span class="sxs-lookup"><span data-stu-id="f1bed-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="f1bed-106">您每秒最多傳送10則訊息。</span><span class="sxs-lookup"><span data-stu-id="f1bed-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="f1bed-107">您所建立的應用程式會顯示使用者可以拖曳的圖形。</span><span class="sxs-lookup"><span data-stu-id="f1bed-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="f1bed-108">伺服器會在所有連接的瀏覽器中更新圖形的位置，以符合使用計時更新所拖曳之圖形的位置。</span><span class="sxs-lookup"><span data-stu-id="f1bed-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="f1bed-109">本教學課程中引進的概念，具有即時遊戲和其他模擬應用程式中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="f1bed-110">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="f1bed-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f1bed-111">設定專案</span><span class="sxs-lookup"><span data-stu-id="f1bed-111">Set up the project</span></span>
> * <span data-ttu-id="f1bed-112">建立基底應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-112">Create the base application</span></span>
> * <span data-ttu-id="f1bed-113">在應用程式啟動時對應至中樞</span><span class="sxs-lookup"><span data-stu-id="f1bed-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="f1bed-114">新增用戶端</span><span class="sxs-lookup"><span data-stu-id="f1bed-114">Add the client</span></span>
> * <span data-ttu-id="f1bed-115">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-115">Run the app</span></span>
> * <span data-ttu-id="f1bed-116">新增用戶端迴圈</span><span class="sxs-lookup"><span data-stu-id="f1bed-116">Add the client loop</span></span>
> * <span data-ttu-id="f1bed-117">新增伺服器迴圈</span><span class="sxs-lookup"><span data-stu-id="f1bed-117">Add the server loop</span></span>
> * <span data-ttu-id="f1bed-118">新增平滑動畫</span><span class="sxs-lookup"><span data-stu-id="f1bed-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="f1bed-119">必要條件：</span><span class="sxs-lookup"><span data-stu-id="f1bed-119">Prerequisites</span></span>

* <span data-ttu-id="f1bed-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)搭配**ASP.NET 和 網頁程式開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="f1bed-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="f1bed-121">設定專案</span><span class="sxs-lookup"><span data-stu-id="f1bed-121">Set up the project</span></span>

<span data-ttu-id="f1bed-122">在本節中，您會在 Visual Studio 2017 中建立專案。</span><span class="sxs-lookup"><span data-stu-id="f1bed-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="f1bed-123">本節說明如何使用 Visual Studio 2017 來建立空的 ASP.NET Web 應用程式，並新增 SignalR 和 jQuery UI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f1bed-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="f1bed-124">在 Visual Studio 中，建立 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![建立 web](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="f1bed-126">在 [**新增 ASP.NET Web 應用程式-MoveShapeDemo** ] 視窗中，保持選取 [**空白**]，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="f1bed-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="f1bed-127">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="f1bed-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="f1bed-128">在 **[加入新專案-MoveShapeDemo**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。</span><span class="sxs-lookup"><span data-stu-id="f1bed-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="f1bed-129">將類別命名為*MoveShapeHub* ，並將它加入至專案。</span><span class="sxs-lookup"><span data-stu-id="f1bed-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="f1bed-130">此步驟會建立*MoveShapeHub.cs*類別檔案。</span><span class="sxs-lookup"><span data-stu-id="f1bed-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="f1bed-131">同時，它會加入一組腳本檔案和元件參考，以支援 SignalR 至專案。</span><span class="sxs-lookup"><span data-stu-id="f1bed-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="f1bed-132">選取 **工具** > **NuGet 套件管理員** > **套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="f1bed-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="f1bed-133">在 [**套件管理員主控台**] 中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f1bed-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="f1bed-134">命令會安裝 jQuery UI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f1bed-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="f1bed-135">您可以使用它來建立圖形的動畫。</span><span class="sxs-lookup"><span data-stu-id="f1bed-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="f1bed-136">在**方案總管**中，展開 [腳本] 節點。</span><span class="sxs-lookup"><span data-stu-id="f1bed-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![腳本程式庫參考](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="f1bed-138">JQuery、jQueryUI 和 SignalR 的腳本程式庫會顯示在專案中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="f1bed-139">建立基底應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-139">Create the base application</span></span>

<span data-ttu-id="f1bed-140">在本節中，您會建立瀏覽器應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-140">In this section, you create a browser application.</span></span> <span data-ttu-id="f1bed-141">應用程式會在每個滑鼠移動事件期間，將圖形位置傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1bed-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="f1bed-142">伺服器會即時將這項資訊廣播給所有其他已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1bed-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="f1bed-143">您可以在稍後的章節中深入瞭解此應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="f1bed-144">開啟*MoveShapeHub.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="f1bed-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="f1bed-145">將*MoveShapeHub.cs*檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f1bed-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="f1bed-146">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f1bed-146">Save the file.</span></span>

<span data-ttu-id="f1bed-147">`MoveShapeHub` 類別是 SignalR 中樞的執行。</span><span class="sxs-lookup"><span data-stu-id="f1bed-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="f1bed-148">如同在[消費者入門 With SignalR](tutorial-getting-started-with-signalr.md)教學課程中，中樞具有用戶端直接呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="f1bed-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="f1bed-149">在此情況下，用戶端會將具有圖形的新 X 和 Y 座標的物件傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1bed-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="f1bed-150">這些座標會被廣播到所有其他已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1bed-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="f1bed-151">SignalR 會使用 JSON 自動序列化此物件。</span><span class="sxs-lookup"><span data-stu-id="f1bed-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="f1bed-152">應用程式會將 `ShapeModel` 物件傳送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1bed-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="f1bed-153">它具有可儲存圖形位置的成員。</span><span class="sxs-lookup"><span data-stu-id="f1bed-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="f1bed-154">伺服器上的物件版本也具有成員，可以追蹤正在儲存的用戶端資料。</span><span class="sxs-lookup"><span data-stu-id="f1bed-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="f1bed-155">此物件可防止伺服器將用戶端的資料傳送回其本身。</span><span class="sxs-lookup"><span data-stu-id="f1bed-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="f1bed-156">這個成員會使用 `JsonIgnore` 屬性，以防止應用程式將資料序列化，並將其傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1bed-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="f1bed-157">在應用程式啟動時對應至中樞</span><span class="sxs-lookup"><span data-stu-id="f1bed-157">Map to the hub when app starts</span></span>

<span data-ttu-id="f1bed-158">接下來，您會在應用程式啟動時設定與中樞的對應。</span><span class="sxs-lookup"><span data-stu-id="f1bed-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="f1bed-159">在 SignalR 2 中，新增 OWIN 啟動類別會建立對應。</span><span class="sxs-lookup"><span data-stu-id="f1bed-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="f1bed-160">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="f1bed-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="f1bed-161">在 [**加入新專案-MoveShapeDemo** ] 中，選取 [**已安裝** > **Visual C#**  > **Web** ]，然後選取 [ **OWIN 啟動類別**]。</span><span class="sxs-lookup"><span data-stu-id="f1bed-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="f1bed-162">將類別命名為*Startup* ，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="f1bed-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="f1bed-163">使用下列程式碼取代*Startup.cs*檔案中的預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="f1bed-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="f1bed-164">OWIN 啟動類別會在應用程式執行 `Configuration` 方法時呼叫 `MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="f1bed-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="f1bed-165">應用程式會使用 `OwinStartup` 元件屬性，將類別新增至 OWIN 的啟動進程。</span><span class="sxs-lookup"><span data-stu-id="f1bed-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="f1bed-166">新增用戶端</span><span class="sxs-lookup"><span data-stu-id="f1bed-166">Add the client</span></span>

<span data-ttu-id="f1bed-167">新增用戶端的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="f1bed-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="f1bed-168">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **HTML 網頁**]。</span><span class="sxs-lookup"><span data-stu-id="f1bed-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="f1bed-169">將頁面命名為**預設值**，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="f1bed-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="f1bed-170">在**方案總管**中，以滑鼠右鍵按一下 [*預設的 .html* ]，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="f1bed-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="f1bed-171">使用下列程式碼取代*預設 .html*檔案中的預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="f1bed-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="f1bed-172">在**方案總管**中，展開 [**腳本**]。</span><span class="sxs-lookup"><span data-stu-id="f1bed-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="f1bed-173">JQuery 和 SignalR 的腳本程式庫會顯示在專案中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f1bed-174">封裝管理員會安裝較新版本的 SignalR 腳本。</span><span class="sxs-lookup"><span data-stu-id="f1bed-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="f1bed-175">更新程式碼區塊中的腳本參考，以對應至專案中的腳本檔案版本。</span><span class="sxs-lookup"><span data-stu-id="f1bed-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="f1bed-176">此 HTML 和 JavaScript 程式碼會建立稱為 `shape`的紅色 `div`。</span><span class="sxs-lookup"><span data-stu-id="f1bed-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="f1bed-177">它會使用 jQuery 程式庫來啟用圖形的拖曳行為，並使用 `drag` 事件將圖形的位置傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1bed-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="f1bed-178">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-178">Run the app</span></span>

<span data-ttu-id="f1bed-179">您可以執行應用程式來 se'e 其運作。</span><span class="sxs-lookup"><span data-stu-id="f1bed-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="f1bed-180">當您將圖形拖曳至瀏覽器視窗時，圖形也會移到其他瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="f1bed-181">在工具列中，開啟 [**腳本調試**程式]，然後選取 [播放] 按鈕，以在 [偵測模式] 中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![使用者開啟偵錯模式和選取 [播放] 的螢幕擷取畫面。](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="f1bed-183">瀏覽器視窗隨即開啟，並在右上角出現紅色形狀。</span><span class="sxs-lookup"><span data-stu-id="f1bed-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="f1bed-184">複製頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1bed-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="f1bed-185">開啟另一個瀏覽器，並將 URL 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="f1bed-186">將圖形拖曳到其中一個瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="f1bed-187">另一個瀏覽器視窗中的圖形如下所示。</span><span class="sxs-lookup"><span data-stu-id="f1bed-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="f1bed-188">雖然應用程式會使用這個方法來運作，但它並不是建議的程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="f1bed-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="f1bed-189">傳送的訊息數目沒有上限。</span><span class="sxs-lookup"><span data-stu-id="f1bed-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="f1bed-190">因此，用戶端和伺服器會因為訊息和效能降低而變得非常龐大。</span><span class="sxs-lookup"><span data-stu-id="f1bed-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="f1bed-191">此外，應用程式會在用戶端上顯示脫離的動畫。</span><span class="sxs-lookup"><span data-stu-id="f1bed-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="f1bed-192">因為圖形會立即透過每個方法移動，所以會發生這個無法停用的動畫。</span><span class="sxs-lookup"><span data-stu-id="f1bed-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="f1bed-193">如果圖形順暢地移到每個新位置，這會更好。</span><span class="sxs-lookup"><span data-stu-id="f1bed-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="f1bed-194">接下來，您將瞭解如何修正這些問題。</span><span class="sxs-lookup"><span data-stu-id="f1bed-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="f1bed-195">新增用戶端迴圈</span><span class="sxs-lookup"><span data-stu-id="f1bed-195">Add the client loop</span></span>

<span data-ttu-id="f1bed-196">在每個滑鼠移動事件上傳送圖形的位置，會建立不必要的網路流量量。</span><span class="sxs-lookup"><span data-stu-id="f1bed-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="f1bed-197">應用程式需要對用戶端的訊息進行節流處理。</span><span class="sxs-lookup"><span data-stu-id="f1bed-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="f1bed-198">使用 javascript `setInterval` 函數來設定迴圈，以固定速率將新的位置資訊傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1bed-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="f1bed-199">這個迴圈是「遊戲迴圈」的基本標記法。</span><span class="sxs-lookup"><span data-stu-id="f1bed-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="f1bed-200">它是重複呼叫的函式，它會驅動遊戲的所有功能。</span><span class="sxs-lookup"><span data-stu-id="f1bed-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="f1bed-201">將*預設 .html*檔案中的用戶端程式代碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f1bed-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="f1bed-202">您必須再次取代腳本參考。</span><span class="sxs-lookup"><span data-stu-id="f1bed-202">You have to replace the script references again.</span></span> <span data-ttu-id="f1bed-203">它們必須符合專案中的腳本版本。</span><span class="sxs-lookup"><span data-stu-id="f1bed-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="f1bed-204">這個新的程式碼會加入 `updateServerModel` 函式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="f1bed-205">它會以固定頻率呼叫。</span><span class="sxs-lookup"><span data-stu-id="f1bed-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="f1bed-206">每當 `moved` 旗標指出有要傳送的新位置資料時，函數就會將位置資料傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1bed-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="f1bed-207">選取 [播放] 按鈕以啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="f1bed-208">複製頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1bed-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="f1bed-209">開啟另一個瀏覽器，並將 URL 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="f1bed-210">將圖形拖曳到其中一個瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="f1bed-211">另一個瀏覽器視窗中的圖形如下所示。</span><span class="sxs-lookup"><span data-stu-id="f1bed-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="f1bed-212">由於應用程式會節流傳送至伺服器的訊息數目，因此，動畫一開始不會顯示為平滑。</span><span class="sxs-lookup"><span data-stu-id="f1bed-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="f1bed-213">新增伺服器迴圈</span><span class="sxs-lookup"><span data-stu-id="f1bed-213">Add the server loop</span></span>

<span data-ttu-id="f1bed-214">在目前的應用程式中，從伺服器傳送到用戶端的訊息會在收到時經常消失。</span><span class="sxs-lookup"><span data-stu-id="f1bed-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="f1bed-215">這種網路流量呈現的問題與在用戶端上看到的類似。</span><span class="sxs-lookup"><span data-stu-id="f1bed-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="f1bed-216">應用程式可以傳送的訊息頻率會高於所需。</span><span class="sxs-lookup"><span data-stu-id="f1bed-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="f1bed-217">如此一來，連接可能會變得很溢。</span><span class="sxs-lookup"><span data-stu-id="f1bed-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="f1bed-218">本章節描述如何補救伺服器，以新增計時器來限制外寄訊息的速率。</span><span class="sxs-lookup"><span data-stu-id="f1bed-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="f1bed-219">將 `MoveShapeHub.cs` 的內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f1bed-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="f1bed-220">選取 [播放] 按鈕以啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="f1bed-221">複製頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1bed-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="f1bed-222">開啟另一個瀏覽器，並將 URL 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="f1bed-223">將圖形拖曳到其中一個瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="f1bed-224">此程式碼會擴充用戶端，以加入 `Broadcaster` 類別。</span><span class="sxs-lookup"><span data-stu-id="f1bed-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="f1bed-225">新類別會使用 .NET framework 中的 `Timer` 類別來節流外寄訊息。</span><span class="sxs-lookup"><span data-stu-id="f1bed-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="f1bed-226">瞭解中樞本身是暫時性的，是很好的。</span><span class="sxs-lookup"><span data-stu-id="f1bed-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="f1bed-227">它會在每次需要時建立。</span><span class="sxs-lookup"><span data-stu-id="f1bed-227">It's created every time it's needed.</span></span> <span data-ttu-id="f1bed-228">因此，應用程式會建立 `Broadcaster` 做為單一實例。</span><span class="sxs-lookup"><span data-stu-id="f1bed-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="f1bed-229">它會使用延遲初始化來延遲 `Broadcaster`的建立，直到需要它為止。</span><span class="sxs-lookup"><span data-stu-id="f1bed-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="f1bed-230">這可確保應用程式在啟動計時器之前完全建立第一個中樞實例。</span><span class="sxs-lookup"><span data-stu-id="f1bed-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="f1bed-231">然後，對用戶端的 `UpdateShape` 函式的呼叫會移出中樞的 `UpdateModel` 方法。</span><span class="sxs-lookup"><span data-stu-id="f1bed-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="f1bed-232">每當應用程式收到傳入訊息時，就不會再立即呼叫它。</span><span class="sxs-lookup"><span data-stu-id="f1bed-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="f1bed-233">相反地，應用程式會以每秒25次呼叫的速率，將訊息傳送給用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1bed-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="f1bed-234">進程是由 `Broadcaster` 類別內的 `_broadcastLoop` 計時器所管理。</span><span class="sxs-lookup"><span data-stu-id="f1bed-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="f1bed-235">最後，`Broadcaster` 類別不會直接從中樞呼叫用戶端方法，而是需要取得目前操作 `_hubContext` 中樞的參考。</span><span class="sxs-lookup"><span data-stu-id="f1bed-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="f1bed-236">它會取得 `GlobalHost`的參考。</span><span class="sxs-lookup"><span data-stu-id="f1bed-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="f1bed-237">新增平滑動畫</span><span class="sxs-lookup"><span data-stu-id="f1bed-237">Add smooth animation</span></span>

<span data-ttu-id="f1bed-238">應用程式幾乎已經完成，但我們可以改善一個。</span><span class="sxs-lookup"><span data-stu-id="f1bed-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="f1bed-239">應用程式會在用戶端上移動圖形，以回應伺服器消息。</span><span class="sxs-lookup"><span data-stu-id="f1bed-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="f1bed-240">請使用 JQuery UI 程式庫的 `animate` 函式，而不是將圖形的位置設定為伺服器所指定的新位置。</span><span class="sxs-lookup"><span data-stu-id="f1bed-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="f1bed-241">它可以在其目前和新位置之間順暢地移動圖形。</span><span class="sxs-lookup"><span data-stu-id="f1bed-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="f1bed-242">更新*預設 .html*檔案中用戶端的 `updateShape` 方法，看起來像反白顯示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f1bed-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="f1bed-243">選取 [播放] 按鈕以啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="f1bed-244">複製頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1bed-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="f1bed-245">開啟另一個瀏覽器，並將 URL 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="f1bed-246">將圖形拖曳到其中一個瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="f1bed-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="f1bed-247">在另一個視窗中的圖形移動會顯示較不停的。</span><span class="sxs-lookup"><span data-stu-id="f1bed-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="f1bed-248">應用程式會在一段時間內插補其移動，而不是針對每個傳入訊息設定一次。</span><span class="sxs-lookup"><span data-stu-id="f1bed-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="f1bed-249">此程式碼會將圖形從舊位置移至新位置。</span><span class="sxs-lookup"><span data-stu-id="f1bed-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="f1bed-250">伺服器會在動畫間隔的過程中提供圖形的位置。</span><span class="sxs-lookup"><span data-stu-id="f1bed-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="f1bed-251">在此情況下，這是100毫秒。</span><span class="sxs-lookup"><span data-stu-id="f1bed-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="f1bed-252">應用程式會在新的動畫開始之前，清除在圖形上執行的任何先前動畫。</span><span class="sxs-lookup"><span data-stu-id="f1bed-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="f1bed-253">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="f1bed-253">Get the code</span></span>

[<span data-ttu-id="f1bed-254">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="f1bed-254">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a><span data-ttu-id="f1bed-255">其他資源</span><span class="sxs-lookup"><span data-stu-id="f1bed-255">Additional resources</span></span>

<span data-ttu-id="f1bed-256">您剛學到的溝通架構，對於開發線上遊戲和其他模擬很有用，例如[使用 SignalR 所建立的 ShootR 遊戲](https://shootr.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="f1bed-256">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="f1bed-257">如需 SignalR 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="f1bed-257">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="f1bed-258">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="f1bed-258">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="f1bed-259">SignalR GitHub 和範例</span><span class="sxs-lookup"><span data-stu-id="f1bed-259">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="f1bed-260">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="f1bed-260">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="f1bed-261">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1bed-261">Next steps</span></span>

<span data-ttu-id="f1bed-262">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="f1bed-262">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f1bed-263">設定專案</span><span class="sxs-lookup"><span data-stu-id="f1bed-263">Set up the project</span></span>
> * <span data-ttu-id="f1bed-264">建立基底應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-264">Created the base application</span></span>
> * <span data-ttu-id="f1bed-265">在應用程式啟動時對應至中樞</span><span class="sxs-lookup"><span data-stu-id="f1bed-265">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="f1bed-266">新增用戶端</span><span class="sxs-lookup"><span data-stu-id="f1bed-266">Added the client</span></span>
> * <span data-ttu-id="f1bed-267">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f1bed-267">Ran the app</span></span>
> * <span data-ttu-id="f1bed-268">新增用戶端迴圈</span><span class="sxs-lookup"><span data-stu-id="f1bed-268">Added the client loop</span></span>
> * <span data-ttu-id="f1bed-269">已新增伺服器迴圈</span><span class="sxs-lookup"><span data-stu-id="f1bed-269">Added the server loop</span></span>
> * <span data-ttu-id="f1bed-270">已新增平滑動畫</span><span class="sxs-lookup"><span data-stu-id="f1bed-270">Added smooth animation</span></span>

<span data-ttu-id="f1bed-271">前進到下一篇文章，以瞭解如何建立使用 ASP.NET SignalR 2 來提供伺服器廣播功能的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1bed-271">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f1bed-272">SignalR 2 和伺服器廣播</span><span class="sxs-lookup"><span data-stu-id="f1bed-272">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)