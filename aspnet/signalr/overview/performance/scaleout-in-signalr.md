---
uid: signalr/overview/performance/scaleout-in-signalr
title: SignalR 中的向外延展簡介 |Microsoft Docs
author: bradygaster
description: 本主題中使用的軟體版本 Visual Studio 2013 .NET 4.5 SignalR 第2版本主題的先前版本，以取得舊版的相關資訊 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14dc22f99a43b566903c59fb23b7d419350f4a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579230"
---
# <a name="introduction-to-scaleout-in-signalr"></a>SignalR 的向外延展簡介

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

一般來說，有兩種方式可以調整 web 應用程式：相應*增加*和*相應*放大。

- 相應增加表示使用較大的伺服器（或較大的 VM），具有更多的 RAM、Cpu 等等。
- 相應放大表示新增更多伺服器來處理負載。

相應增加的問題是，您快速達到機器大小的限制。 除此之外，您還必須相應放大。不過，當您相應放大時，用戶端可以路由至不同的伺服器。 連接到一部伺服器的用戶端不會接收從另一部伺服器傳送的訊息。

![](scaleout-in-signalr/_static/image1.png)

其中一個解決方法是使用稱為*背板*的元件，在伺服器之間轉送訊息。 啟用背板後，每個應用程式實例會將訊息傳送至後擋板，而背板會將它們轉送至其他應用程式實例。 （在電子產品中，背板是一組平行連接器。 相較之下，SignalR 背板會連接多部伺服器）。

![](scaleout-in-signalr/_static/image2.png)

SignalR 目前提供三個背板：

- **Azure 服務匯流排**。 服務匯流排是一種訊息基礎結構，可讓元件以鬆散耦合的方式傳送訊息。
- **Redis**。 Redis 是記憶體中的索引鍵/值存放區。 Redis 支援發行/訂閱（"pub/sub"）模式來傳送訊息。
- **SQL Server**。 SQL Server 背板會將訊息寫入至 SQL 資料表。 背板會使用 Service Broker 來提供有效率的訊息。 不過，如果未啟用 Service Broker，它也可以運作。

如果您在 Azure 上部署應用程式，請考慮使用[Azure Redis Cache](https://azure.microsoft.com/services/cache/)的 Redis 背板。 如果您要部署到您自己的伺服器陣列，請考慮 SQL Server 或 Redis 的背板。

下列主題包含每個背板的逐步教學課程：

- [SignalR 向外延展與 Azure 服務匯流排](scaleout-with-windows-azure-service-bus.md)
- [SignalR 向外延展與 Redis](scaleout-with-redis.md)
- [SignalR 向外延展與 SQL Server](scaleout-with-sql-server.md)

## <a name="implementation"></a>實作

在 SignalR 中，每個訊息都會透過訊息匯流排傳送。 訊息匯流排會執行[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)介面，以提供發佈/訂閱抽象概念。 背板的工作方式是將預設**IMessageBus**取代為針對該後擋板設計的匯流排。 例如，Redis 的訊息匯流排是[RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)，它會使用 Redis [pub/sub](http://redis.io/topics/pubsub)機制來傳送和接收訊息。

每個伺服器實例都會透過匯流排連接至後擋板。 當傳送訊息時，它會移至背板，而背板會將它傳送到每一部伺服器。 當伺服器從背板取得訊息時，它會將訊息放在其本機快取中。 接著，伺服器會從其本機快取將訊息傳遞給用戶端。

針對每個用戶端連接，會使用資料指標來追蹤用戶端讀取訊息資料流程的進度。 （資料指標代表訊息資料流程中的位置）。如果用戶端中斷連線再重新連線，它會要求匯流排在用戶端的資料指標值之後抵達的任何訊息。 當連接使用[長輪詢](../getting-started/introduction-to-signalr.md#transports)時，就會發生相同的情況。 長時間輪詢要求完成之後，用戶端會開啟新的連接，並要求在游標之後抵達的訊息。

即使在重新連線時，用戶端會路由傳送至不同的伺服器，資料指標機制也會運作。 背板知道所有伺服器，而且用戶端連線到哪一部伺服器並不重要。

## <a name="limitations"></a>限制

使用背板，訊息輸送量的最大值會比用戶端直接與單一伺服器節點交談時的更低。 這是因為背板會將每個訊息轉送到每個節點，因此背板可能會變成瓶頸。 這項限制是否有問題，取決於應用程式。 例如，以下是一些典型的 SignalR 案例：

- [伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)（例如股票行情指示器）：背板適用于此案例，因為伺服器會控制傳送訊息的速率。
- [用戶端對用戶端](../getting-started/tutorial-getting-started-with-signalr.md)（例如聊天）：在此案例中，如果訊息數目隨著用戶端數目調整，則背板可能是瓶頸;也就是說，如果訊息的速率會隨著更多用戶端聯結而按比例成長。
- [高頻率即時](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)（例如即時遊戲）：在此案例中不建議使用背板。

## <a name="enabling-tracing-for-signalr-scaleout"></a>啟用 SignalR 向外延展的追蹤

若要啟用背板的追蹤，請將下列區段新增至 web.config 檔案中的根**configuration**元素底下：

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
