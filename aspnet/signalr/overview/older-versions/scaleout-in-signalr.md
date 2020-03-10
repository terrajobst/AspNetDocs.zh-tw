---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: SignalR 1.x 中的向外延展簡介 |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 04/29/2013
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9bad72d31a0ebc491910ebb128b3b3a7fb537958
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536565"
---
# <a name="introduction-to-scaleout-in-signalr-1x"></a><span data-ttu-id="71e99-102">SignalR 1.x 的向外延展簡介</span><span class="sxs-lookup"><span data-stu-id="71e99-102">Introduction to Scaleout in SignalR 1.x</span></span>

<span data-ttu-id="71e99-103">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="71e99-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="71e99-104">一般來說，有兩種方式可以調整 web 應用程式：相應*增加*和*相應*放大。</span><span class="sxs-lookup"><span data-stu-id="71e99-104">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="71e99-105">相應增加表示使用較大的伺服器（或較大的 VM），具有更多的 RAM、Cpu 等等。</span><span class="sxs-lookup"><span data-stu-id="71e99-105">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="71e99-106">相應放大表示新增更多伺服器來處理負載。</span><span class="sxs-lookup"><span data-stu-id="71e99-106">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="71e99-107">相應增加的問題是，您快速達到機器大小的限制。</span><span class="sxs-lookup"><span data-stu-id="71e99-107">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="71e99-108">除此之外，您還必須相應放大。不過，當您相應放大時，用戶端可以路由至不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="71e99-108">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="71e99-109">連接到一部伺服器的用戶端不會接收從另一部伺服器傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-109">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="71e99-110">其中一個解決方法是使用稱為*背板*的元件，在伺服器之間轉送訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-110">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="71e99-111">啟用背板後，每個應用程式實例會將訊息傳送至後擋板，而背板會將它們轉送至其他應用程式實例。</span><span class="sxs-lookup"><span data-stu-id="71e99-111">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="71e99-112">（在電子產品中，背板是一組平行連接器。</span><span class="sxs-lookup"><span data-stu-id="71e99-112">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="71e99-113">相較之下，SignalR 背板會連接多部伺服器）。</span><span class="sxs-lookup"><span data-stu-id="71e99-113">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="71e99-114">SignalR 目前提供三個背板：</span><span class="sxs-lookup"><span data-stu-id="71e99-114">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="71e99-115">**Azure 服務匯流排**。</span><span class="sxs-lookup"><span data-stu-id="71e99-115">**Azure Service Bus**.</span></span> <span data-ttu-id="71e99-116">服務匯流排是一種訊息基礎結構，可讓元件以鬆散耦合的方式傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-116">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="71e99-117">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="71e99-117">**Redis**.</span></span> <span data-ttu-id="71e99-118">Redis 是記憶體中的索引鍵/值存放區。</span><span class="sxs-lookup"><span data-stu-id="71e99-118">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="71e99-119">Redis 支援發行/訂閱（"pub/sub"）模式來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-119">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="71e99-120">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="71e99-120">**SQL Server**.</span></span> <span data-ttu-id="71e99-121">SQL Server 背板會將訊息寫入至 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="71e99-121">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="71e99-122">背板會使用 Service Broker 來提供有效率的訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-122">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="71e99-123">不過，如果未啟用 Service Broker，它也可以運作。</span><span class="sxs-lookup"><span data-stu-id="71e99-123">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="71e99-124">如果您在 Azure 上部署應用程式，請考慮使用 Azure 服務匯流排背板。</span><span class="sxs-lookup"><span data-stu-id="71e99-124">If you deploy your application on Azure, consider using the Azure Service Bus backplane.</span></span> <span data-ttu-id="71e99-125">如果您要部署到您自己的伺服器陣列，請考慮 SQL Server 或 Redis 的背板。</span><span class="sxs-lookup"><span data-stu-id="71e99-125">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="71e99-126">下列主題包含每個背板的逐步教學課程：</span><span class="sxs-lookup"><span data-stu-id="71e99-126">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="71e99-127">SignalR 向外延展與 Azure 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="71e99-127">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="71e99-128">SignalR 向外延展與 Redis</span><span class="sxs-lookup"><span data-stu-id="71e99-128">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="71e99-129">SignalR 向外延展與 SQL Server</span><span class="sxs-lookup"><span data-stu-id="71e99-129">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="71e99-130">實作</span><span class="sxs-lookup"><span data-stu-id="71e99-130">Implementation</span></span>

<span data-ttu-id="71e99-131">在 SignalR 中，每個訊息都會透過訊息匯流排傳送。</span><span class="sxs-lookup"><span data-stu-id="71e99-131">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="71e99-132">訊息匯流排會執行[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)介面，以提供發佈/訂閱抽象概念。</span><span class="sxs-lookup"><span data-stu-id="71e99-132">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="71e99-133">背板的工作方式是將預設**IMessageBus**取代為針對該後擋板設計的匯流排。</span><span class="sxs-lookup"><span data-stu-id="71e99-133">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="71e99-134">例如，Redis 的訊息匯流排是[RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)，它會使用 Redis [pub/sub](http://redis.io/topics/pubsub)機制來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-134">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="71e99-135">每個伺服器實例都會透過匯流排連接至後擋板。</span><span class="sxs-lookup"><span data-stu-id="71e99-135">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="71e99-136">當傳送訊息時，它會移至背板，而背板會將它傳送到每一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="71e99-136">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="71e99-137">當伺服器從背板取得訊息時，它會將訊息放在其本機快取中。</span><span class="sxs-lookup"><span data-stu-id="71e99-137">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="71e99-138">接著，伺服器會從其本機快取將訊息傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="71e99-138">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="71e99-139">針對每個用戶端連接，會使用資料指標來追蹤用戶端讀取訊息資料流程的進度。</span><span class="sxs-lookup"><span data-stu-id="71e99-139">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="71e99-140">（資料指標代表訊息資料流程中的位置）。如果用戶端中斷連線再重新連線，它會要求匯流排在用戶端的資料指標值之後抵達的任何訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-140">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="71e99-141">當連接使用[長輪詢](../getting-started/introduction-to-signalr.md#transports)時，就會發生相同的情況。</span><span class="sxs-lookup"><span data-stu-id="71e99-141">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="71e99-142">長時間輪詢要求完成之後，用戶端會開啟新的連接，並要求在游標之後抵達的訊息。</span><span class="sxs-lookup"><span data-stu-id="71e99-142">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="71e99-143">即使在重新連線時，用戶端會路由傳送至不同的伺服器，資料指標機制也會運作。</span><span class="sxs-lookup"><span data-stu-id="71e99-143">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="71e99-144">背板知道所有伺服器，而且用戶端連線到哪一部伺服器並不重要。</span><span class="sxs-lookup"><span data-stu-id="71e99-144">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="71e99-145">限制</span><span class="sxs-lookup"><span data-stu-id="71e99-145">Limitations</span></span>

<span data-ttu-id="71e99-146">使用背板，訊息輸送量的最大值會比用戶端直接與單一伺服器節點交談時的更低。</span><span class="sxs-lookup"><span data-stu-id="71e99-146">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="71e99-147">這是因為背板會將每個訊息轉送到每個節點，因此背板可能會變成瓶頸。</span><span class="sxs-lookup"><span data-stu-id="71e99-147">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="71e99-148">這項限制是否有問題，取決於應用程式。</span><span class="sxs-lookup"><span data-stu-id="71e99-148">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="71e99-149">例如，以下是一些典型的 SignalR 案例：</span><span class="sxs-lookup"><span data-stu-id="71e99-149">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="71e99-150">[伺服器廣播](tutorial-server-broadcast-with-aspnet-signalr.md)（例如股票行情指示器）：背板適用于此案例，因為伺服器會控制傳送訊息的速率。</span><span class="sxs-lookup"><span data-stu-id="71e99-150">[Server broadcast](tutorial-server-broadcast-with-aspnet-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="71e99-151">[用戶端對用戶端](tutorial-getting-started-with-signalr.md)（例如聊天）：在此案例中，如果訊息數目隨著用戶端數目調整，則背板可能是瓶頸;也就是說，如果訊息的速率會隨著更多用戶端聯結而按比例成長。</span><span class="sxs-lookup"><span data-stu-id="71e99-151">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="71e99-152">[高頻率即時](tutorial-high-frequency-realtime-with-signalr.md)（例如即時遊戲）：在此案例中不建議使用背板。</span><span class="sxs-lookup"><span data-stu-id="71e99-152">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="71e99-153">啟用 SignalR 向外延展的追蹤</span><span class="sxs-lookup"><span data-stu-id="71e99-153">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="71e99-154">若要啟用背板的追蹤，請將下列區段新增至 web.config 檔案中的根**configuration**元素底下：</span><span class="sxs-lookup"><span data-stu-id="71e99-154">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
