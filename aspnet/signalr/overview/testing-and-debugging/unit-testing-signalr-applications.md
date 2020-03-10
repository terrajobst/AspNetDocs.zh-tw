---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: 單元測試 SignalR 應用程式 |Microsoft Docs
author: bradygaster
description: 本文說明如何使用 SignalR 2.0 的單元測試功能。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578670"
---
# <a name="unit-testing-signalr-applications"></a><span data-ttu-id="eee5a-103">對 SignalR 應用程式進行單元測試</span><span class="sxs-lookup"><span data-stu-id="eee5a-103">Unit Testing SignalR Applications</span></span>

<span data-ttu-id="eee5a-104">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="eee5a-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="eee5a-105">本文說明如何使用 SignalR 2 的單元測試功能。</span><span class="sxs-lookup"><span data-stu-id="eee5a-105">This article describes using the Unit Testing features of SignalR 2.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="eee5a-106">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="eee5a-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="eee5a-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="eee5a-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="eee5a-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="eee5a-108">.NET 4.5</span></span>
> - <span data-ttu-id="eee5a-109">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="eee5a-109">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="eee5a-110">問題與意見</span><span class="sxs-lookup"><span data-stu-id="eee5a-110">Questions and comments</span></span>
>
> <span data-ttu-id="eee5a-111">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="eee5a-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="eee5a-112">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="eee5a-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="eee5a-113">SignalR 應用程式的單元測試</span><span class="sxs-lookup"><span data-stu-id="eee5a-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="eee5a-114">您可以使用 SignalR 2 中的單元測試功能來建立 SignalR 應用程式的單元測試。</span><span class="sxs-lookup"><span data-stu-id="eee5a-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="eee5a-115">SignalR 2 包含[IHubCallerConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)介面，可用來建立模擬物件，以模擬您的中樞方法以進行測試。</span><span class="sxs-lookup"><span data-stu-id="eee5a-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="eee5a-116">在本節中，您會使用[XUnit.net](https://github.com/xunit/xunit)和[Moq](https://github.com/Moq/moq4)，為在[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中建立的應用程式新增單元測試。</span><span class="sxs-lookup"><span data-stu-id="eee5a-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="eee5a-117">XUnit.net 將用來控制測試;Moq 將用來建立用於測試的[mock](http://en.wikipedia.org/wiki/Mock_object)物件。</span><span class="sxs-lookup"><span data-stu-id="eee5a-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="eee5a-118">如有需要，可以使用其他模擬架構;[NSubstitute](http://nsubstitute.github.io/)也是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="eee5a-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="eee5a-119">本教學課程示範如何以兩種方式設定模擬物件：第一種是使用 `dynamic` 物件（在 .NET Framework 4 中引進），而第二種則是使用介面。</span><span class="sxs-lookup"><span data-stu-id="eee5a-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="eee5a-120">內容</span><span class="sxs-lookup"><span data-stu-id="eee5a-120">Contents</span></span>

<span data-ttu-id="eee5a-121">本教學課程包含下列各節。</span><span class="sxs-lookup"><span data-stu-id="eee5a-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="eee5a-122">使用 Dynamic 進行單元測試</span><span class="sxs-lookup"><span data-stu-id="eee5a-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="eee5a-123">依類型的單元測試</span><span class="sxs-lookup"><span data-stu-id="eee5a-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="eee5a-124">使用 Dynamic 進行單元測試</span><span class="sxs-lookup"><span data-stu-id="eee5a-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="eee5a-125">在本節中，您會使用動態物件，為[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中建立的應用程式新增單元測試。</span><span class="sxs-lookup"><span data-stu-id="eee5a-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="eee5a-126">安裝適用于 Visual Studio 2013 的 XUnit 執行器[擴充](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099)功能。</span><span class="sxs-lookup"><span data-stu-id="eee5a-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="eee5a-127">請完成[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程，或從[MSDN 程式碼庫](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)下載已完成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eee5a-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="eee5a-128">如果您使用的是消費者入門應用程式的下載版本，請開啟 [**套件管理員主控台**]，然後按一下 [**還原**]，將 SignalR 套件新增至專案。</span><span class="sxs-lookup"><span data-stu-id="eee5a-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![還原套件](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="eee5a-130">將專案加入至單元測試的方案。</span><span class="sxs-lookup"><span data-stu-id="eee5a-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="eee5a-131">在**方案總管**中，以滑鼠右鍵按一下您的方案，然後選取 [**加入**]、[**新增專案**]。在**C#** 節點底下，選取 [ **Windows** ] 節點。</span><span class="sxs-lookup"><span data-stu-id="eee5a-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="eee5a-132">選取 [**類別庫**]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-132">Select **Class Library**.</span></span> <span data-ttu-id="eee5a-133">將新專案命名為**TestLibrary** ，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="eee5a-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![建立測試程式庫](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="eee5a-135">將測試程式庫專案中的參考加入至 SignalRChat 專案。</span><span class="sxs-lookup"><span data-stu-id="eee5a-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="eee5a-136">以滑鼠右鍵按一下**TestLibrary**專案，然後選取 [**新增**]、[**參考 ...** ]。選取 [**方案**] 節點底下的 [**專案**] 節點，然後檢查**SignalRChat**。</span><span class="sxs-lookup"><span data-stu-id="eee5a-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="eee5a-137">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-137">Click **OK**.</span></span>

    ![新增專案參考](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="eee5a-139">將 SignalR、Moq 和 XUnit 封裝新增至**TestLibrary**專案。</span><span class="sxs-lookup"><span data-stu-id="eee5a-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="eee5a-140">在 [**套件管理員主控台**] 中，將 [**預設專案**] 下拉式清單設定為 [ **TestLibrary**]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="eee5a-141">在主控台視窗中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="eee5a-141">Run the following commands in the console window:</span></span>

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![安裝套件](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="eee5a-143">建立測試檔案。</span><span class="sxs-lookup"><span data-stu-id="eee5a-143">Create the test file.</span></span> <span data-ttu-id="eee5a-144">以滑鼠右鍵按一下**TestLibrary**專案，然後按一下 [**加入**]、[**類別**]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="eee5a-145">將新類別命名為**Tests.cs**。</span><span class="sxs-lookup"><span data-stu-id="eee5a-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="eee5a-146">將 Tests.cs 的內容取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="eee5a-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="eee5a-147">在上述程式碼中，會使用[Moq](https://github.com/Moq/moq4)程式庫（屬於[IHubCallerConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)型別）中的 `Mock` 物件建立測試用戶端（在 SignalR 2.1 中，為型別參數指派 `dynamic`）。`IHubCallerConnectionContext` 介面是用來在用戶端上叫用方法的 proxy 物件。</span><span class="sxs-lookup"><span data-stu-id="eee5a-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="eee5a-148">然後會為模擬用戶端定義 `broadcastMessage` 函式，讓 `ChatHub` 類別可以呼叫該函數。</span><span class="sxs-lookup"><span data-stu-id="eee5a-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="eee5a-149">然後，測試引擎會呼叫 `ChatHub` 類別的 `Send` 方法，然後再呼叫模擬 `broadcastMessage` 函數。</span><span class="sxs-lookup"><span data-stu-id="eee5a-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="eee5a-150">按**F6**以建立方案。</span><span class="sxs-lookup"><span data-stu-id="eee5a-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="eee5a-151">執行單元測試。</span><span class="sxs-lookup"><span data-stu-id="eee5a-151">Run the unit test.</span></span> <span data-ttu-id="eee5a-152">在 Visual Studio 中，選取 [**測試**]、[ **Windows**]、[**測試瀏覽器**]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="eee5a-153">在 [測試瀏覽器] 視窗中，以滑鼠右鍵按一下**HubsAreMockableViaDynamic** ，然後選取 [**執行選取的測試**]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![測試總管](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="eee5a-155">核取 [測試瀏覽器] 視窗中的下方窗格，確認測試通過。</span><span class="sxs-lookup"><span data-stu-id="eee5a-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="eee5a-156">此視窗會顯示測試已通過。</span><span class="sxs-lookup"><span data-stu-id="eee5a-156">The window will show that the test passed.</span></span>

    ![成功的測試](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="eee5a-158">依類型的單元測試</span><span class="sxs-lookup"><span data-stu-id="eee5a-158">Unit testing by type</span></span>

<span data-ttu-id="eee5a-159">在本節中，您會使用包含要測試之方法的介面，為[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中所建立的應用程式加入測試。</span><span class="sxs-lookup"><span data-stu-id="eee5a-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="eee5a-160">完成上述使用動態教學課程的[單元測試](#dynamic)中的步驟1-7。</span><span class="sxs-lookup"><span data-stu-id="eee5a-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="eee5a-161">將 Tests.cs 的內容取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="eee5a-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="eee5a-162">在上述程式碼中，會建立介面來定義測試引擎將建立模擬用戶端之 `broadcastMessage` 方法的簽章。</span><span class="sxs-lookup"><span data-stu-id="eee5a-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="eee5a-163">然後會使用[IHubCallerConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)類型的 `Mock` 物件建立模擬用戶端（在 SignalR 2.1 中，為類型參數指派 `dynamic`）。`IHubCallerConnectionContext` 介面是用來在用戶端上叫用方法的 proxy 物件。</span><span class="sxs-lookup"><span data-stu-id="eee5a-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="eee5a-164">然後，測試會建立 `ChatHub`的實例，然後建立 `broadcastMessage` 方法的模擬版本，然後藉由呼叫中樞上的 `Send` 方法來叫用。</span><span class="sxs-lookup"><span data-stu-id="eee5a-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="eee5a-165">按**F6**以建立方案。</span><span class="sxs-lookup"><span data-stu-id="eee5a-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="eee5a-166">執行單元測試。</span><span class="sxs-lookup"><span data-stu-id="eee5a-166">Run the unit test.</span></span> <span data-ttu-id="eee5a-167">在 Visual Studio 中，選取 [**測試**]、[ **Windows**]、[**測試瀏覽器**]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="eee5a-168">在 [測試瀏覽器] 視窗中，以滑鼠右鍵按一下**HubsAreMockableViaDynamic** ，然後選取 [**執行選取的測試**]。</span><span class="sxs-lookup"><span data-stu-id="eee5a-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![測試總管](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="eee5a-170">核取 [測試瀏覽器] 視窗中的下方窗格，確認測試通過。</span><span class="sxs-lookup"><span data-stu-id="eee5a-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="eee5a-171">此視窗會顯示測試已通過。</span><span class="sxs-lookup"><span data-stu-id="eee5a-171">The window will show that the test passed.</span></span>

    ![成功的測試](unit-testing-signalr-applications/_static/image8.png)
