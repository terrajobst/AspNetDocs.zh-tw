---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: 具有 Azure 服務匯流排的 SignalR 向外延展（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558412"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a>使用 Azure 服務匯流排的 SignalR 向外延展 (SignalR 1.x)

由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

在本教學課程中，您會將 SignalR 應用程式部署至 Windows Azure Web 角色，使用服務匯流排背板將訊息散發至每個角色實例。

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

必要條件：

- Windows Azure 帳戶。
- [Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。
- Visual Studio 2012。

服務匯流排背板也與[Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)1.1 版的服務匯流排相容。 不過，它與 Windows Server 的1.0 版服務匯流排不相容。

## <a name="pricing"></a>定價

服務匯流排的背板會使用主題來傳送訊息。 如需最新的定價資訊，請參閱[服務匯流排](https://azure.microsoft.com/pricing/details/service-bus/)。 在撰寫本文時，您可以針對小於 $1 的每月傳送1000000訊息。 背板會針對 SignalR 中樞方法的每個調用傳送服務匯流排訊息。 還有一些控制訊息可用於連接、中斷連線、加入或離開群組等等。 在大部分的應用程式中，大部分的訊息流量都會是中樞方法調用。

## <a name="overview"></a>概觀

在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。

1. 使用 Windows Azure 入口網站建立新的服務匯流排命名空間。
2. 將下列 NuGet 套件新增至您的應用程式： 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR。](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. 建立 SignalR 應用程式。
4. 將下列程式碼新增至 global.asax 以設定背板： 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

針對每個應用程式，挑選不同的 "YourAppName" 值。 請勿在多個應用程式中使用相同的值。

## <a name="create-the-azure-services"></a>建立 Azure 服務

如[如何建立和部署雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)中所述，建立雲端服務。 依照「如何：使用快速建立來建立雲端服務」一節中的步驟進行。 在本教學課程中，您不需要上傳憑證。

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

建立新的服務匯流排命名空間，如[如何使用服務匯流排主題/訂用](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)帳戶中所述。 依照「建立服務命名空間」一節中的步驟進行。

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> 請務必為雲端服務和服務匯流排命名空間選取相同的區域。

## <a name="create-the-visual-studio-project"></a>建立 Visual Studio 專案

啟動 Visual Studio。 從 [檔案] 功能表，按一下 [新增專案]。

在 [**新增專案**] 對話方塊中，展開 [**視覺效果C#** ]。 在 [**已安裝的範本**] 底下選取 [**雲端**]，然後選取 [ **Windows Azure 雲端服務**]。 保留預設值 .NET Framework 4.5。 將應用程式命名為 ChatService，然後按一下 **[確定]** 。

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

在 [**新的 Windows Azure 雲端服務**] 對話方塊中，選取 [ASP.NET MVC 4 Web 角色]。 按一下向右箭號按鈕（ **&gt;** ），將角色新增至您的方案。

將滑鼠游標移到新的角色上方，使鉛筆圖示可見。 按一下此圖示以重新命名角色。 將角色命名為 "SignalRChat"，然後按一下 **[確定]** 。

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

在 [**新增 ASP.NET MVC 4 專案**] 中，選取 [**網際網路應用程式**]。 按一下 [確定]。 [專案] wizard 會建立兩個專案：

- ChatService：此專案是 Windows Azure 應用程式。 它會定義 Azure 角色和其他設定選項。
- SignalRChat：此專案是您的 ASP.NET MVC 4 專案。

## <a name="create-the-signalr-chat-application"></a>建立 SignalR Chat 應用程式

若要建立聊天應用程式，請依照教學課程[消費者入門使用 SignalR 和 MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)中的步驟進行。

使用 NuGet 來安裝所需的程式庫。 從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [**套件管理員主控台**] 視窗中，輸入下列命令：

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

使用 [`-ProjectName`] 選項，將套件安裝至 ASP.NET MVC 專案，而不是 Windows Azure 專案。

## <a name="configure-the-backplane"></a>設定背板

在您應用程式的 global.asax 檔案中，新增下列程式碼：

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

現在您需要取得服務匯流排連接字串。 在 Azure 入口網站中，選取您所建立的服務匯流排命名空間，然後按一下 存取金鑰 圖示。

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

將連接字串複製到剪貼簿，然後將它貼到*connectionString*變數中。

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>部署到 Azure

在方案總管中，展開 ChatService 專案內的 [**角色**] 資料夾。

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

以滑鼠右鍵按一下 [SignalRChat] 角色，然後選取 [**屬性**]。 選取 [**設定**] 索引標籤。在 [**實例**] 下選取 [2]。 您也可以將 VM 大小設定為 **[超小型]。**

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

儲存變更。

在方案總管中，以滑鼠右鍵按一下 [ChatService] 專案。 選取 [發行]。

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

如果這是您第一次發行至 Windows Azure，您必須下載您的認證。 在 [**發行**嚮導] 中，按一下 [登入以下載認證]。 這會提示您登入 Windows Azure 入口網站並下載發佈設定檔案。

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

按一下 [匯**入**]，然後選取您已下載的發佈設定檔案。

按 [下一步]。 在 [**發行設定**] 對話方塊的 [**雲端服務**] 底下，選取您稍早建立的雲端服務。

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

按一下 [發行]。 部署應用程式並啟動 Vm 可能需要幾分鐘的時間。

現在當您執行聊天應用程式時，角色實例會使用服務匯流排主題，透過 Azure 服務匯流排進行通訊。 主題是允許多個訂閱者的訊息佇列。

背板會自動建立主題和訂用帳戶。 若要查看 [訂用帳戶] 和 [訊息] 活動，請開啟 Azure 入口網站，選取服務匯流排命名空間，然後按一下 [主題]。

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

這需要幾分鐘的時間，訊息活動才會顯示在儀表板中。

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

SignalR 會管理主題的存留期。 只要您的應用程式已部署，請不要嘗試手動刪除主題或變更設定。
