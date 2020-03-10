---
uid: signalr/overview/older-versions/scaleout-with-redis
title: SignalR 向外延展 with Redis （SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536558"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a>使用 Redis 的 SignalR 向外延展 (SignalR 1.x)

由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

在本教學課程中，您將使用[Redis](http://redis.io/) ，將訊息散發至部署在兩個不同 IIS 實例上的 SignalR 應用程式。

Redis 是記憶體中的索引鍵/值存放區。 它也支援具有發行/訂閱模型的訊息系統。 SignalR Redis 背板會使用 pub/sub 功能將訊息轉送至其他伺服器。

![](scaleout-with-redis/_static/image1.png)

在本教學課程中，您將使用三部伺服器：

- 兩部執行 Windows 的伺服器，您將用它來部署 SignalR 應用程式。
- 一部執行 Linux 的伺服器，您將使用它來執行 Redis。 在本教學課程的螢幕擷取畫面中，我使用了 Ubuntu 12.04 TLS。

如果您沒有三個要使用的實體伺服器，您可以在 Hyper-v 上建立 Vm。 另一個選項是在 Azure 上建立 Vm。

雖然本教學課程使用官方 Redis 實，但也有 MSOpenTech 的[Windows 埠 Redis](https://github.com/MSOpenTech/redis) 。 安裝程式和設定不同，但步驟相同。

> [!NOTE] 
> 
> 具有 Redis 的 SignalR 向外延展不支援 Redis 叢集。

## <a name="overview"></a>概觀

在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。

1. 安裝 Redis 並啟動 Redis 伺服器。
2. 將下列 NuGet 套件新增至您的應用程式： 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. Redis](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. 建立 SignalR 應用程式。
4. 將下列程式碼新增至 global.asax 以設定背板： 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Hyper-v 上的 Ubuntu

您可以使用 Windows Hyper-v，輕鬆地在 Windows Server 上建立 Ubuntu VM。

從[http://www.ubuntu.com](http://www.ubuntu.com/)下載 Ubuntu ISO。

在 Hyper-v 中，新增 VM。 在 [**連接虛擬硬碟]** 步驟中，選取 [**建立虛擬硬碟**]。

![](scaleout-with-redis/_static/image2.png)

在 [**安裝選項**] 步驟中，選取 [**影像檔案（.iso）** ]，按一下 **[流覽]** ，然後流覽至 Ubuntu 安裝 iso。

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>安裝 Redis

遵循[http://redis.io/download](http://redis.io/download)的步驟，下載並建立 Redis。

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

這會在 `src` 目錄中建立 Redis 二進位檔。

根據預設，Redis 不需要密碼。 若要設定密碼，請編輯位於原始程式碼根目錄中的 `redis.conf` 檔案。 （您必須先製作檔案的備份副本，然後再進行編輯！）將下列指示詞新增至 `redis.conf`：

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

現在啟動 Redis 伺服器：

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

開啟埠6379，這是 Redis 接聽的預設埠。 （您可以變更設定檔案中的埠號碼）。

## <a name="create-the-signalr-application"></a>建立 SignalR 應用程式

遵循下列其中一個教學課程來建立 SignalR 應用程式：

- [使用 SignalR 消費者入門](../getting-started/tutorial-getting-started-with-signalr.md)
- [使用 SignalR 和 MVC 4 的消費者入門](tutorial-getting-started-with-signalr-and-mvc-4.md)

接下來，我們將修改聊天應用程式，以支援使用 Redis 的向外延展。 首先，將 SignalR Redis NuGet 封裝新增至您的專案。 在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

接下來，開啟 global.asax 檔案。 將下列程式碼新增至**應用程式\_Start**方法：

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- 「伺服器」是正在執行 Redis 的伺服器名稱。
- *port*是埠號碼
- 「密碼」是您在 redis 檔案中定義的密碼。
- "AppName" 為任何字串。 SignalR 會使用此名稱建立 Redis pub/sub 通道。

例如:

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>部署和執行應用程式

準備您的 Windows Server 實例以部署 SignalR 應用程式。

新增 IIS 角色。 包含「應用程式開發」功能，包括 WebSocket 通訊協定。

![](scaleout-with-redis/_static/image5.png)

也請包含管理服務（列在 [管理工具] 底下）。

![](scaleout-with-redis/_static/image6.png)

**安裝 Web Deploy 3.0。** 當您執行 IIS 管理員時，它會提示您安裝 Microsoft Web Platform，或者您可以[下載安裝程式](https://go.microsoft.com/fwlink/?LinkId=255386)。 在平臺安裝程式中，搜尋 Web Deploy 並安裝 Web Deploy 3。0

![](scaleout-with-redis/_static/image7.png)

檢查 Web 管理服務是否正在執行。 如果沒有，請啟動服務。 （如果您在 Windows 服務清單中看不到 [Web 管理服務]，請確定您已在新增 IIS 角色時安裝管理服務）。

根據預設，Web 管理服務會接聽 TCP 通訊埠8172。 在 Windows 防火牆中，建立新的輸入規則，以允許埠8172上的 TCP 流量。 如需詳細資訊，請參閱設定[防火牆規則](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。 （如果您要在 Azure 上裝載 Vm，您可以直接在 Azure 入口網站中執行此動作。 請參閱[如何設定虛擬機器的端點](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)。）

現在您已準備好從開發電腦將 Visual Studio 專案部署到伺服器。 在方案總管中，以滑鼠右鍵按一下方案，然後按一下 [**發佈**]。

如需 web 部署的詳細檔，請參閱[Visual Studio 和 ASP.NET 的 Web 部署內容對應](../../../whitepapers/aspnet-web-deployment-content-map.md)。

如果您將應用程式部署至兩部伺服器，您可以在另一個瀏覽器視窗中開啟每個實例，並查看每個實例都會收到來自另一個的 SignalR 訊息。 （當然，在生產環境中，這兩部伺服器會位於負載平衡器後方）。

![](scaleout-with-redis/_static/image8.png)

如果您想要查看傳送至 Redis 的訊息，可以使用**Redis cli**用戶端，它會與 Redis 一起安裝。

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
