---
uid: signalr/overview/performance/scaleout-with-sql-server
title: 具有 SQL Server 的 SignalR 向外延展 |Microsoft Docs
author: bradygaster
description: 本主題中使用的軟體版本 Visual Studio 2013 .NET 4.5 SignalR 第2版本主題的先前版本，以取得舊版的相關資訊 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579181"
---
# <a name="signalr-scaleout-with-sql-server"></a>使用 SQL Server 的向外延展

由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的先前版本
>
> 如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

在本教學課程中，您將使用 SQL Server 將訊息散發至部署在兩個不同 IIS 實例中的 SignalR 應用程式。 您也可以在單一測試電腦上執行本教學課程，但若要取得完整的效果，您必須將 SignalR 應用程式部署到兩部以上的伺服器。 您也必須在其中一部伺服器上，或在個別的專用伺服器上安裝 SQL Server。 另一個選項是使用 Azure 上的 Vm 來執行教學課程。

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>Prerequisites

Microsoft SQL Server 2005 或更新版本。 背板同時支援桌上型電腦和伺服器版本的 SQL Server。 它不支援 SQL Server Compact 版本或 Azure SQL Database。 （如果您的應用程式裝載在 Azure 上，請考慮改為服務匯流排背板）。

## <a name="overview"></a>概觀

在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。

1. 建立新的空白資料庫。 背板會在此資料庫中建立必要的資料表。
2. 將下列 NuGet 套件新增至您的應用程式：

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. 建立 SignalR 應用程式。
4. 將下列程式碼新增至 Startup.cs 以設定背板：

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   這段程式碼會使用[TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)的預設值來設定背板。 如需變更這些值的相關資訊，請參閱[SignalR Performance：向外延展計量](signalr-performance.md#scaleout_metrics)。

## <a name="configure-the-database"></a>設定資料庫

決定應用程式是否會使用 Windows 驗證或 SQL Server 驗證來存取資料庫。 無論如何，請確定資料庫使用者具有登入、建立架構和建立資料表的許可權。

建立新的資料庫，讓背板使用。 您可以為資料庫提供任何名稱。 您不需要在資料庫中建立任何資料表;背板會建立所需的資料表。

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>啟用 Service Broker

建議您啟用背板資料庫的 Service Broker。 Service Broker 在 SQL Server 中提供訊息和佇列的原生支援，讓背板更有效率地接收更新。 （不過，背板也可以運作，而不 Service Broker）。

若要檢查是否已啟用 Service Broker，請查詢**sys.databases**目錄檢視中 **\_Broker\_enabled**資料行。

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

若要啟用 Service Broker，請使用下列 SQL 查詢：

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> 如果此查詢出現鎖死，請確定沒有任何應用程式連接到資料庫。

如果您已啟用追蹤，追蹤也會顯示是否已啟用 Service Broker。

## <a name="create-a-signalr-application"></a>建立 SignalR 應用程式

遵循下列其中一個教學課程來建立 SignalR 應用程式：

- [使用 SignalR 2.0 的消費者入門](../getting-started/tutorial-getting-started-with-signalr.md)
- [使用 SignalR 2.0 和 MVC 5 的消費者入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

接下來，我們將修改聊天應用程式，以支援 SQL Server 的向外延展。 首先，將 SignalR NuGet 套件新增至您的專案。 在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

接下來，開啟 Startup.cs 檔案。 將下列程式碼新增至**Configure**方法：

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>部署和執行應用程式

準備您的 Windows Server 實例以部署 SignalR 應用程式。

新增 IIS 角色。 包含「應用程式開發」功能，包括 WebSocket 通訊協定。

![](scaleout-with-sql-server/_static/image4.png)

也請包含管理服務（列在 [管理工具] 底下）。

![](scaleout-with-sql-server/_static/image5.png)

**安裝 Web Deploy 3.0。** 當您執行 IIS 管理員時，它會提示您安裝 Microsoft Web Platform，或者您可以[下載安裝程式](https://go.microsoft.com/fwlink/?LinkId=255386)。 在平臺安裝程式中，搜尋 Web Deploy 並安裝 Web Deploy 3。0

![](scaleout-with-sql-server/_static/image6.png)

檢查 Web 管理服務是否正在執行。 如果沒有，請啟動服務。 （如果您在 Windows 服務清單中看不到 [Web 管理服務]，請確定您已在新增 IIS 角色時安裝管理服務）。

最後，針對 TCP 開啟埠8172。 這是 Web Deploy 工具所使用的埠。

現在您已準備好從開發電腦將 Visual Studio 專案部署到伺服器。 在方案總管中，以滑鼠右鍵按一下方案，然後按一下 [**發佈**]。

如需 web 部署的詳細檔，請參閱[Visual Studio 和 ASP.NET 的 Web 部署內容對應](../../../whitepapers/aspnet-web-deployment-content-map.md)。

如果您將應用程式部署至兩部伺服器，您可以在另一個瀏覽器視窗中開啟每個實例，並查看每個實例都會收到來自另一個的 SignalR 訊息。 （當然，在生產環境中，這兩部伺服器會位於負載平衡器後方）。

![](scaleout-with-sql-server/_static/image7.png)

執行應用程式之後，您可以看到 SignalR 已自動在資料庫中建立資料表：

![](scaleout-with-sql-server/_static/image8.png)

SignalR 管理資料表。 只要您的應用程式已部署，就不要刪除資料列、修改資料表等等。
