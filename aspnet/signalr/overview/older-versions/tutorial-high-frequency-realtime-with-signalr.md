---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: 具有 SignalR 1.x 的高頻率即時 |Microsoft Docs
author: bradygaster
description: 本教學課程說明如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供高頻率的訊息功能。 中的高頻率訊息 。
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623498"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a><span data-ttu-id="2781e-104">使用 SignalR 1.x 進行高頻率即時聊天</span><span class="sxs-lookup"><span data-stu-id="2781e-104">High-Frequency Realtime with SignalR 1.x</span></span>

<span data-ttu-id="2781e-105">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="2781e-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="2781e-106">本教學課程說明如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供高頻率的訊息功能。</span><span class="sxs-lookup"><span data-stu-id="2781e-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="2781e-107">在此情況下，高頻率訊息表示以固定速率傳送的更新;在此應用程式的案例中，每秒最多10個訊息。</span><span class="sxs-lookup"><span data-stu-id="2781e-107">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
> 
> <span data-ttu-id="2781e-108">您在本教學課程中建立的應用程式會顯示使用者可以拖曳的圖形。</span><span class="sxs-lookup"><span data-stu-id="2781e-108">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="2781e-109">接著，所有其他已連接的瀏覽器中的圖形位置都會更新，以符合使用計時更新所拖曳之圖形的位置。</span><span class="sxs-lookup"><span data-stu-id="2781e-109">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
> 
> <span data-ttu-id="2781e-110">本教學課程中引進的概念，具有即時遊戲和其他模擬應用程式中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2781e-110">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
> 
> <span data-ttu-id="2781e-111">歡迎使用教學課程的批註。</span><span class="sxs-lookup"><span data-stu-id="2781e-111">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="2781e-112">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="2781e-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>

## <a name="overview"></a><span data-ttu-id="2781e-113">概觀</span><span class="sxs-lookup"><span data-stu-id="2781e-113">Overview</span></span>

<span data-ttu-id="2781e-114">本教學課程示範如何建立應用程式，以與其他瀏覽器即時共用物件的狀態。</span><span class="sxs-lookup"><span data-stu-id="2781e-114">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="2781e-115">我們將建立的應用程式稱為 MoveShape。</span><span class="sxs-lookup"><span data-stu-id="2781e-115">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="2781e-116">[MoveShape] 頁面會顯示使用者可以拖曳的 HTML Div 元素;當使用者拖曳 Div 時，其新位置將會傳送至伺服器，然後通知所有其他已連線的用戶端更新圖形的位置以符合。</span><span class="sxs-lookup"><span data-stu-id="2781e-116">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="2781e-118">在本教學課程中建立的應用程式是以 Damian Edwards 的示範為基礎。</span><span class="sxs-lookup"><span data-stu-id="2781e-118">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="2781e-119">您可以在[這裡](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)看到包含此示範的影片。</span><span class="sxs-lookup"><span data-stu-id="2781e-119">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="2781e-120">本教學課程一開始會示範如何從每個引發的事件中，將 SignalR 訊息傳送至拖曳的圖形。</span><span class="sxs-lookup"><span data-stu-id="2781e-120">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="2781e-121">每次已連線的用戶端都會在收到訊息時，更新局部版本的圖形位置。</span><span class="sxs-lookup"><span data-stu-id="2781e-121">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="2781e-122">雖然應用程式會使用此方法運作，但這不是建議的程式設計模型，因為傳送的訊息數目沒有上限，因此用戶端和伺服器可能會因為訊息而變得很龐大，而且效能會降低.</span><span class="sxs-lookup"><span data-stu-id="2781e-122">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="2781e-123">在用戶端上顯示的動畫也會脫離，因為圖形會立即由每個方法移動，而不會順暢地移至每個新位置。</span><span class="sxs-lookup"><span data-stu-id="2781e-123">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="2781e-124">本教學課程的後續章節將示範如何建立計時器函式，以限制用戶端或伺服器傳送訊息的最大速率，以及如何在位置之間順暢地移動圖形。</span><span class="sxs-lookup"><span data-stu-id="2781e-124">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="2781e-125">您可以從程式[代碼庫](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下載本教學課程中所建立的最終應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="2781e-125">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="2781e-126">本教學課程包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="2781e-126">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="2781e-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="2781e-127">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="2781e-128">建立專案</span><span class="sxs-lookup"><span data-stu-id="2781e-128">Create the project</span></span>](#createtheproject)
- [<span data-ttu-id="2781e-129">新增 ASP.NET SignalR 和 JQuery. UI NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="2781e-129">Add the ASP.NET SignalR and JQuery.UI NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="2781e-130">建立基底應用程式</span><span class="sxs-lookup"><span data-stu-id="2781e-130">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="2781e-131">新增用戶端迴圈</span><span class="sxs-lookup"><span data-stu-id="2781e-131">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="2781e-132">新增伺服器迴圈</span><span class="sxs-lookup"><span data-stu-id="2781e-132">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="2781e-133">在用戶端上新增平滑動畫</span><span class="sxs-lookup"><span data-stu-id="2781e-133">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="2781e-134">進一步的步驟</span><span class="sxs-lookup"><span data-stu-id="2781e-134">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="2781e-135">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2781e-135">Prerequisites</span></span>

<span data-ttu-id="2781e-136">本教學課程需要 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="2781e-136">This tutorial requires Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="2781e-137">如果使用 Visual Studio 2010，專案將會使用 .NET Framework 4，而不是 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="2781e-137">If Visual Studio 2010 is used, the project will use .NET Framework 4 rather than .NET Framework 4.5.</span></span>

<span data-ttu-id="2781e-138">如果您使用 Visual Studio 2012，建議您安裝[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="2781e-138">If you are using Visual Studio 2012, it's recommended that you install the [ASP.NET and Web Tools 2012.2 update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="2781e-139">此更新包含新功能，例如發佈、新功能和新範本的增強功能。</span><span class="sxs-lookup"><span data-stu-id="2781e-139">This update contains new features such as enhancements to publishing, new functionality, and new templates.</span></span>

<span data-ttu-id="2781e-140">如果您有 Visual Studio 2010，請確定已安裝[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。</span><span class="sxs-lookup"><span data-stu-id="2781e-140">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createtheproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="2781e-141">建立專案</span><span class="sxs-lookup"><span data-stu-id="2781e-141">Create the project</span></span>

<span data-ttu-id="2781e-142">在本節中，我們將在 Visual Studio 中建立專案。</span><span class="sxs-lookup"><span data-stu-id="2781e-142">In this section, we'll create the project in Visual Studio.</span></span>

1. <span data-ttu-id="2781e-143">從 [檔案] 功能表，按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="2781e-143">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="2781e-144">在 [**新增專案**] 對話方塊中， **C#** 展開 [**範本**]，然後選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="2781e-144">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="2781e-145">選取 [ **ASP.NET 空白 Web 應用程式**] 範本，將專案命名為*MoveShapeDemo*，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2781e-145">Select the **ASP.NET Empty Web Application** template, name the project *MoveShapeDemo*, and click **OK**.</span></span>

    ![建立新專案](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a><span data-ttu-id="2781e-147">新增 SignalR 和 JQuery。 UI NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="2781e-147">Add the SignalR and JQuery.UI NuGet Packages</span></span>

<span data-ttu-id="2781e-148">您可以藉由安裝 NuGet 套件，將 SignalR 功能新增至專案。</span><span class="sxs-lookup"><span data-stu-id="2781e-148">You can add SignalR functionality to a project by installing a NuGet package.</span></span> <span data-ttu-id="2781e-149">本教學課程也會使用 JQuery. UI 封裝，讓圖形得以拖曳和動畫。</span><span class="sxs-lookup"><span data-stu-id="2781e-149">This tutorial will also use the JQuery.UI package for allowing the shape to be dragged and animated.</span></span>

1. <span data-ttu-id="2781e-150">按一下 [**工具] |NuGet 套件管理員 |套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="2781e-150">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="2781e-151">在 [套件管理員] 中輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="2781e-151">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="2781e-152">SignalR 套件會安裝一些其他 NuGet 套件做為相依性。</span><span class="sxs-lookup"><span data-stu-id="2781e-152">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="2781e-153">當安裝完成時，您會擁有在 ASP.NET 應用程式中使用 SignalR 所需的所有伺服器和用戶端元件。</span><span class="sxs-lookup"><span data-stu-id="2781e-153">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>
3. <span data-ttu-id="2781e-154">在 [套件管理員主控台] 中輸入下列命令，以安裝 JQuery 和 JQuery. UI 封裝。</span><span class="sxs-lookup"><span data-stu-id="2781e-154">Enter the following command into the package manager console to install the JQuery and JQuery.UI packages.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="2781e-155">建立基底應用程式</span><span class="sxs-lookup"><span data-stu-id="2781e-155">Create the base application</span></span>

<span data-ttu-id="2781e-156">在本節中，我們將建立瀏覽器應用程式，以便在每個滑鼠移動事件期間，將圖形的位置傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="2781e-156">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="2781e-157">接著，伺服器會將此資訊廣播到所有其他已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="2781e-157">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="2781e-158">我們將在稍後的章節中展開此應用程式。</span><span class="sxs-lookup"><span data-stu-id="2781e-158">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="2781e-159">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增**]、[**類別**...]。將類別命名為**MoveShapeHub** ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2781e-159">In **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="2781e-160">將新的**MoveShapeHub**類別中的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2781e-160">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="2781e-161">上述 `MoveShapeHub` 類別是 SignalR 中樞的執行。</span><span class="sxs-lookup"><span data-stu-id="2781e-161">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="2781e-162">如同在[消費者入門 With SignalR](index.md)教學課程中，中樞具有一種方法，可讓用戶端直接呼叫。</span><span class="sxs-lookup"><span data-stu-id="2781e-162">As in the [Getting Started with SignalR](index.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="2781e-163">在此情況下，用戶端會將包含圖形新 X 和 Y 座標的物件傳送至伺服器，然後再將其廣播至所有其他已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="2781e-163">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="2781e-164">SignalR 會使用 JSON 自動序列化此物件。</span><span class="sxs-lookup"><span data-stu-id="2781e-164">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="2781e-165">將傳送至用戶端的物件（`ShapeModel`）包含用來儲存圖形位置的成員。</span><span class="sxs-lookup"><span data-stu-id="2781e-165">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="2781e-166">伺服器上的物件版本也包含成員，以追蹤正在儲存的用戶端資料，讓指定的用戶端不會傳送自己的資料。</span><span class="sxs-lookup"><span data-stu-id="2781e-166">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="2781e-167">這個成員會使用 `JsonIgnore` 屬性，讓它不被序列化並傳送到用戶端。</span><span class="sxs-lookup"><span data-stu-id="2781e-167">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>
3. <span data-ttu-id="2781e-168">接下來，我們會在應用程式啟動時設定中樞。</span><span class="sxs-lookup"><span data-stu-id="2781e-168">Next, we'll set up the hub when the application starts.</span></span> <span data-ttu-id="2781e-169">在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |全域應用程式類別**。</span><span class="sxs-lookup"><span data-stu-id="2781e-169">In **Solution Explorer**, right-click the project, then click **Add | Global Application Class**.</span></span> <span data-ttu-id="2781e-170">接受*全域*的預設名稱，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2781e-170">Accept the default name of *Global* and click **OK**.</span></span>

    ![新增全域應用程式類別](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. <span data-ttu-id="2781e-172">在 Global.asax.cs 類別中提供的**using**語句之後，新增下列 `using` 語句。</span><span class="sxs-lookup"><span data-stu-id="2781e-172">Add the following `using` statement after the provided **using** statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. <span data-ttu-id="2781e-173">在全域類別的 `Application_Start` 方法中新增下列程式程式碼，以註冊 SignalR 的預設路由。</span><span class="sxs-lookup"><span data-stu-id="2781e-173">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="2781e-174">您的 global.asax 檔案看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="2781e-174">Your global.asax file should look like the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. <span data-ttu-id="2781e-175">接下來，我們要新增用戶端。</span><span class="sxs-lookup"><span data-stu-id="2781e-175">Next, we'll add the client.</span></span> <span data-ttu-id="2781e-176">在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |新專案**。</span><span class="sxs-lookup"><span data-stu-id="2781e-176">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="2781e-177">在 [**加入新專案**] 對話方塊中，選取 [ **Html 網頁**]。</span><span class="sxs-lookup"><span data-stu-id="2781e-177">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="2781e-178">為頁面指定適當的名稱（例如 [ **.html**]），然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2781e-178">Give the page an appropriate name (like **Default.html**) and click **Add**.</span></span>
7. <span data-ttu-id="2781e-179">在**方案總管**中，以滑鼠右鍵按一下您剛建立的頁面，然後按一下 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="2781e-179">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
8. <span data-ttu-id="2781e-180">將 HTML 網頁中的預設程式碼取代為下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2781e-180">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2781e-181">確認下列腳本參考符合在 [腳本] 資料夾中新增至專案的套件。</span><span class="sxs-lookup"><span data-stu-id="2781e-181">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span> <span data-ttu-id="2781e-182">在 Visual Studio 2010 中，加入至專案的 JQuery 和 SignalR 版本可能與下列版本號碼不相符。</span><span class="sxs-lookup"><span data-stu-id="2781e-182">In Visual Studio 2010, the version of JQuery and SignalR added to the project may not match the version numbers below.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    <span data-ttu-id="2781e-183">上述 HTML 和 JavaScript 程式碼會建立稱為 Shape 的紅色 Div，使用 jQuery 程式庫啟用圖形的拖曳行為，並使用圖形的 `drag` 事件將圖形的位置傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="2781e-183">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
9. <span data-ttu-id="2781e-184">按 F5 啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2781e-184">Start the application by pressing F5.</span></span> <span data-ttu-id="2781e-185">複製頁面的 URL，並將它貼入第二個瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="2781e-185">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="2781e-186">將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。</span><span class="sxs-lookup"><span data-stu-id="2781e-186">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="2781e-188">新增用戶端迴圈</span><span class="sxs-lookup"><span data-stu-id="2781e-188">Add the client loop</span></span>

<span data-ttu-id="2781e-189">由於在每個滑鼠移動事件上傳送圖形的位置，將會產生不必要的網路流量量，因此來自用戶端的訊息必須進行節流。</span><span class="sxs-lookup"><span data-stu-id="2781e-189">Since sending the location of the shape on every mouse move event will create an unnecessary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="2781e-190">我們將使用 javascript `setInterval` 函數來設定迴圈，以固定速率將新的位置資訊傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="2781e-190">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="2781e-191">這個迴圈是一個非常基本的「遊戲迴圈」標記法，這是一種重複呼叫的函式，可驅動遊戲或其他模擬的所有功能。</span><span class="sxs-lookup"><span data-stu-id="2781e-191">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="2781e-192">更新 HTML 網頁中的用戶端程式代碼，以符合下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2781e-192">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    <span data-ttu-id="2781e-193">上述更新會新增 `updateServerModel` 函式，此函式會以固定頻率呼叫。</span><span class="sxs-lookup"><span data-stu-id="2781e-193">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="2781e-194">每當 `moved` 旗標指出有要傳送的新位置資料時，此函數就會將位置資料傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="2781e-194">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="2781e-195">按 F5 啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2781e-195">Start the application by pressing F5.</span></span> <span data-ttu-id="2781e-196">複製頁面的 URL，並將它貼入第二個瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="2781e-196">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="2781e-197">將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。</span><span class="sxs-lookup"><span data-stu-id="2781e-197">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="2781e-198">因為傳送至伺服器的訊息數目將會受到節流，所以動畫不會像上一節一樣平滑。</span><span class="sxs-lookup"><span data-stu-id="2781e-198">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="2781e-200">新增伺服器迴圈</span><span class="sxs-lookup"><span data-stu-id="2781e-200">Add the server loop</span></span>

<span data-ttu-id="2781e-201">在目前的應用程式中，從伺服器傳送到用戶端的訊息會在收到時經常消失。</span><span class="sxs-lookup"><span data-stu-id="2781e-201">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="2781e-202">這會呈現在用戶端上看到的類似問題;訊息的傳送頻率可能比所需的還多，而且連接可能會變得太大。</span><span class="sxs-lookup"><span data-stu-id="2781e-202">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="2781e-203">本節說明如何補救伺服器，以執行會節流傳出訊息速率的計時器。</span><span class="sxs-lookup"><span data-stu-id="2781e-203">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="2781e-204">將 `MoveShapeHub.cs` 的內容取代為下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2781e-204">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="2781e-205">上述程式碼會擴充用戶端，以加入 `Broadcaster` 類別，這會使用 .NET framework 中的 `Timer` 類別來節流外寄訊息。</span><span class="sxs-lookup"><span data-stu-id="2781e-205">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="2781e-206">由於中樞本身是暫時性的（每次需要時都會建立），因此 `Broadcaster` 將會建立為單一實例。</span><span class="sxs-lookup"><span data-stu-id="2781e-206">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="2781e-207">延遲初始化（在 .NET 4 中引進）是用來延遲其建立，直到需要它為止，確保在啟動計時器之前，會完全建立第一個中樞實例。</span><span class="sxs-lookup"><span data-stu-id="2781e-207">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="2781e-208">接著，對用戶端的 `UpdateShape` 函式的呼叫會移出中樞的 `UpdateModel` 方法，如此一來，只要收到傳入訊息，就不會再立即呼叫該函數。</span><span class="sxs-lookup"><span data-stu-id="2781e-208">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="2781e-209">相反地，用戶端的訊息會以每秒25次呼叫的速率傳送，由 `Broadcaster` 類別內的 `_broadcastLoop` 計時器管理。</span><span class="sxs-lookup"><span data-stu-id="2781e-209">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="2781e-210">最後，`Broadcaster` 類別不會直接從中樞呼叫用戶端方法，而是必須使用 `GlobalHost`取得目前操作中樞（`_hubContext`）的參考。</span><span class="sxs-lookup"><span data-stu-id="2781e-210">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="2781e-211">按 F5 啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2781e-211">Start the application by pressing F5.</span></span> <span data-ttu-id="2781e-212">複製頁面的 URL，並將它貼入第二個瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="2781e-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="2781e-213">將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。</span><span class="sxs-lookup"><span data-stu-id="2781e-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="2781e-214">上一節的瀏覽器中不會有明顯的差異，但傳送至用戶端的訊息數目將會受到節流。</span><span class="sxs-lookup"><span data-stu-id="2781e-214">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="2781e-216">在用戶端上新增平滑動畫</span><span class="sxs-lookup"><span data-stu-id="2781e-216">Add smooth animation on the client</span></span>

<span data-ttu-id="2781e-217">應用程式幾乎已完成，但我們可以在用戶端的圖形移動時，將其移至回應伺服器消息時，改善一個更好的改良。</span><span class="sxs-lookup"><span data-stu-id="2781e-217">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="2781e-218">我們會使用 JQuery UI 程式庫的 `animate` 函式，在其目前和新位置之間順暢地移動圖形，而不是將圖形的位置設定為伺服器所指定的新位置。</span><span class="sxs-lookup"><span data-stu-id="2781e-218">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="2781e-219">更新用戶端的 `updateShape` 方法，讓它看起來像下面的反白顯示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="2781e-219">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    <span data-ttu-id="2781e-220">上述程式碼會在動畫間隔（在此案例中為100毫秒）的過程中，將圖形從舊位置移至伺服器提供的新位置。</span><span class="sxs-lookup"><span data-stu-id="2781e-220">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="2781e-221">在新動畫開始之前，會先清除在圖形上執行的任何先前動畫。</span><span class="sxs-lookup"><span data-stu-id="2781e-221">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="2781e-222">按 F5 啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2781e-222">Start the application by pressing F5.</span></span> <span data-ttu-id="2781e-223">複製頁面的 URL，並將它貼入第二個瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="2781e-223">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="2781e-224">將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。</span><span class="sxs-lookup"><span data-stu-id="2781e-224">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="2781e-225">在另一個視窗中，圖形的移動應該顯示得比較少，因為它會在一段時間內插補，而不是針對每個傳入訊息設定一次。</span><span class="sxs-lookup"><span data-stu-id="2781e-225">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="2781e-227">進一步的步驟</span><span class="sxs-lookup"><span data-stu-id="2781e-227">Further Steps</span></span>

<span data-ttu-id="2781e-228">在本教學課程中，您已瞭解如何針對在用戶端與伺服器之間傳送高頻率訊息的 SignalR 應用程式進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="2781e-228">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="2781e-229">此通訊範例適用于開發線上遊戲和其他模擬，例如[使用 SignalR 建立的 ShootR 遊戲](http://shootr.signalr.net)。</span><span class="sxs-lookup"><span data-stu-id="2781e-229">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](http://shootr.signalr.net).</span></span>

<span data-ttu-id="2781e-230">您可以從程式[代碼庫](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下載本教學課程中建立的完整應用程式。</span><span class="sxs-lookup"><span data-stu-id="2781e-230">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="2781e-231">若要深入瞭解 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：</span><span class="sxs-lookup"><span data-stu-id="2781e-231">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="2781e-232">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="2781e-232">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="2781e-233">SignalR Github 和範例</span><span class="sxs-lookup"><span data-stu-id="2781e-233">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="2781e-234">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="2781e-234">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
