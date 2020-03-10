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
# <a name="unit-testing-signalr-applications"></a>對 SignalR 應用程式進行單元測試

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文說明如何使用 SignalR 2 的單元測試功能。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>SignalR 應用程式的單元測試

您可以使用 SignalR 2 中的單元測試功能來建立 SignalR 應用程式的單元測試。 SignalR 2 包含[IHubCallerConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)介面，可用來建立模擬物件，以模擬您的中樞方法以進行測試。

在本節中，您會使用[XUnit.net](https://github.com/xunit/xunit)和[Moq](https://github.com/Moq/moq4)，為在[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中建立的應用程式新增單元測試。

XUnit.net 將用來控制測試;Moq 將用來建立用於測試的[mock](http://en.wikipedia.org/wiki/Mock_object)物件。 如有需要，可以使用其他模擬架構;[NSubstitute](http://nsubstitute.github.io/)也是不錯的選擇。 本教學課程示範如何以兩種方式設定模擬物件：第一種是使用 `dynamic` 物件（在 .NET Framework 4 中引進），而第二種則是使用介面。

### <a name="contents"></a>內容

本教學課程包含下列各節。

- [使用 Dynamic 進行單元測試](#dynamic)
- [依類型的單元測試](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>使用 Dynamic 進行單元測試

在本節中，您會使用動態物件，為[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中建立的應用程式新增單元測試。

1. 安裝適用于 Visual Studio 2013 的 XUnit 執行器[擴充](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099)功能。
2. 請完成[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程，或從[MSDN 程式碼庫](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)下載已完成的應用程式。
3. 如果您使用的是消費者入門應用程式的下載版本，請開啟 [**套件管理員主控台**]，然後按一下 [**還原**]，將 SignalR 套件新增至專案。

    ![還原套件](unit-testing-signalr-applications/_static/image1.png)
4. 將專案加入至單元測試的方案。 在**方案總管**中，以滑鼠右鍵按一下您的方案，然後選取 [**加入**]、[**新增專案**]。在**C#** 節點底下，選取 [ **Windows** ] 節點。 選取 [**類別庫**]。 將新專案命名為**TestLibrary** ，然後按一下 **[確定]** 。

    ![建立測試程式庫](unit-testing-signalr-applications/_static/image2.png)
5. 將測試程式庫專案中的參考加入至 SignalRChat 專案。 以滑鼠右鍵按一下**TestLibrary**專案，然後選取 [**新增**]、[**參考 ...** ]。選取 [**方案**] 節點底下的 [**專案**] 節點，然後檢查**SignalRChat**。 按一下 [確定]。

    ![新增專案參考](unit-testing-signalr-applications/_static/image3.png)
6. 將 SignalR、Moq 和 XUnit 封裝新增至**TestLibrary**專案。 在 [**套件管理員主控台**] 中，將 [**預設專案**] 下拉式清單設定為 [ **TestLibrary**]。 在主控台視窗中執行下列命令：

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![安裝套件](unit-testing-signalr-applications/_static/image4.png)
7. 建立測試檔案。 以滑鼠右鍵按一下**TestLibrary**專案，然後按一下 [**加入**]、[**類別**]。 將新類別命名為**Tests.cs**。
8. 將 Tests.cs 的內容取代為下列程式碼。

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    在上述程式碼中，會使用[Moq](https://github.com/Moq/moq4)程式庫（屬於[IHubCallerConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)型別）中的 `Mock` 物件建立測試用戶端（在 SignalR 2.1 中，為型別參數指派 `dynamic`）。`IHubCallerConnectionContext` 介面是用來在用戶端上叫用方法的 proxy 物件。 然後會為模擬用戶端定義 `broadcastMessage` 函式，讓 `ChatHub` 類別可以呼叫該函數。 然後，測試引擎會呼叫 `ChatHub` 類別的 `Send` 方法，然後再呼叫模擬 `broadcastMessage` 函數。
9. 按**F6**以建立方案。
10. 執行單元測試。 在 Visual Studio 中，選取 [**測試**]、[ **Windows**]、[**測試瀏覽器**]。 在 [測試瀏覽器] 視窗中，以滑鼠右鍵按一下**HubsAreMockableViaDynamic** ，然後選取 [**執行選取的測試**]。

    ![測試總管](unit-testing-signalr-applications/_static/image5.png)
11. 核取 [測試瀏覽器] 視窗中的下方窗格，確認測試通過。 此視窗會顯示測試已通過。

    ![成功的測試](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>依類型的單元測試

在本節中，您會使用包含要測試之方法的介面，為[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中所建立的應用程式加入測試。

1. 完成上述使用動態教學課程的[單元測試](#dynamic)中的步驟1-7。
2. 將 Tests.cs 的內容取代為下列程式碼。

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    在上述程式碼中，會建立介面來定義測試引擎將建立模擬用戶端之 `broadcastMessage` 方法的簽章。 然後會使用[IHubCallerConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)類型的 `Mock` 物件建立模擬用戶端（在 SignalR 2.1 中，為類型參數指派 `dynamic`）。`IHubCallerConnectionContext` 介面是用來在用戶端上叫用方法的 proxy 物件。

    然後，測試會建立 `ChatHub`的實例，然後建立 `broadcastMessage` 方法的模擬版本，然後藉由呼叫中樞上的 `Send` 方法來叫用。
3. 按**F6**以建立方案。
4. 執行單元測試。 在 Visual Studio 中，選取 [**測試**]、[ **Windows**]、[**測試瀏覽器**]。 在 [測試瀏覽器] 視窗中，以滑鼠右鍵按一下**HubsAreMockableViaDynamic** ，然後選取 [**執行選取的測試**]。

    ![測試總管](unit-testing-signalr-applications/_static/image7.png)
5. 核取 [測試瀏覽器] 視窗中的下方窗格，確認測試通過。 此視窗會顯示測試已通過。

    ![成功的測試](unit-testing-signalr-applications/_static/image8.png)
