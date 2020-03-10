---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: 將 SignalR 使用者對應至 SignalR 1.x 中的連接 |Microsoft Docs
author: bradygaster
description: 本主題說明如何保留使用者和其連線的相關資訊。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558482"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="247c3-103">將 SignalR 使用者對應至 SignalR 1.x 的連線</span><span class="sxs-lookup"><span data-stu-id="247c3-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="247c3-104">由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="247c3-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="247c3-105">本主題說明如何保留使用者和其連線的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="247c3-105">This topic shows how to retain information about users and their connections.</span></span>

## <a name="introduction"></a><span data-ttu-id="247c3-106">簡介</span><span class="sxs-lookup"><span data-stu-id="247c3-106">Introduction</span></span>

<span data-ttu-id="247c3-107">連線至中樞的每個用戶端都會傳遞唯一的連線識別碼。您可以在中樞內容的 `Context.ConnectionId` 屬性中取得此值。</span><span class="sxs-lookup"><span data-stu-id="247c3-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="247c3-108">如果您的應用程式需要將使用者對應到連接識別碼並保存該對應，您可以使用下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="247c3-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="247c3-109">[記憶體內部儲存體](#inmemory)（例如字典）</span><span class="sxs-lookup"><span data-stu-id="247c3-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="247c3-110">每位使用者的 SignalR 群組</span><span class="sxs-lookup"><span data-stu-id="247c3-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="247c3-111">[永久的外部儲存體](#database)，例如資料庫資料表或 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="247c3-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="247c3-112">本主題會顯示每個這些實作為。</span><span class="sxs-lookup"><span data-stu-id="247c3-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="247c3-113">您可以使用 `Hub` 類別的 `OnConnected`、`OnDisconnected`和 `OnReconnected` 方法來追蹤使用者連接狀態。</span><span class="sxs-lookup"><span data-stu-id="247c3-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="247c3-114">應用程式的最佳做法取決於：</span><span class="sxs-lookup"><span data-stu-id="247c3-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="247c3-115">裝載應用程式的網頁伺服器數目。</span><span class="sxs-lookup"><span data-stu-id="247c3-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="247c3-116">您是否需要取得目前已連線使用者的清單。</span><span class="sxs-lookup"><span data-stu-id="247c3-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="247c3-117">當應用程式或伺服器重新開機時，是否需要保存群組和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="247c3-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="247c3-118">呼叫外部伺服器的延遲是否有問題。</span><span class="sxs-lookup"><span data-stu-id="247c3-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="247c3-119">下表顯示這些考慮適用的方法。</span><span class="sxs-lookup"><span data-stu-id="247c3-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="247c3-120">一部以上的伺服器</span><span class="sxs-lookup"><span data-stu-id="247c3-120">More than one server</span></span> | <span data-ttu-id="247c3-121">取得目前已連線使用者的清單</span><span class="sxs-lookup"><span data-stu-id="247c3-121">Get list of currently connected users</span></span> | <span data-ttu-id="247c3-122">重新開機之後保存資訊</span><span class="sxs-lookup"><span data-stu-id="247c3-122">Persist information after restarts</span></span> | <span data-ttu-id="247c3-123">最佳效能</span><span class="sxs-lookup"><span data-stu-id="247c3-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="247c3-124">記憶體中</span><span class="sxs-lookup"><span data-stu-id="247c3-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="247c3-125">單一使用者群組</span><span class="sxs-lookup"><span data-stu-id="247c3-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="247c3-126">永久、外部</span><span class="sxs-lookup"><span data-stu-id="247c3-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="247c3-127">記憶體內部儲存體</span><span class="sxs-lookup"><span data-stu-id="247c3-127">In-memory storage</span></span>

<span data-ttu-id="247c3-128">下列範例示範如何在儲存于記憶體中的字典中保留連接和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="247c3-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="247c3-129">字典會使用 `HashSet` 來儲存連接識別碼。任何時候，使用者都可以有一個以上的 SignalR 應用程式連接。</span><span class="sxs-lookup"><span data-stu-id="247c3-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="247c3-130">例如，透過多個裝置或多個瀏覽器索引標籤連線的使用者，會有一個以上的連接識別碼。</span><span class="sxs-lookup"><span data-stu-id="247c3-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="247c3-131">如果應用程式關閉，則會遺失所有資訊，但會在使用者重新建立其連接時重新填入。</span><span class="sxs-lookup"><span data-stu-id="247c3-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="247c3-132">如果您的環境包含一部以上的 web 伺服器，記憶體內部儲存體就無法運作，因為每部伺服器都有不同的連線集合。</span><span class="sxs-lookup"><span data-stu-id="247c3-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="247c3-133">第一個範例顯示的類別會管理使用者與連接的對應。</span><span class="sxs-lookup"><span data-stu-id="247c3-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="247c3-134">HashSet 的索引鍵將會是使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="247c3-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="247c3-135">下一個範例顯示如何使用中樞的連線對應類別。</span><span class="sxs-lookup"><span data-stu-id="247c3-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="247c3-136">類別的實例會儲存在 `_connections`的變數名稱中。</span><span class="sxs-lookup"><span data-stu-id="247c3-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="247c3-137">單一使用者群組</span><span class="sxs-lookup"><span data-stu-id="247c3-137">Single-user groups</span></span>

<span data-ttu-id="247c3-138">您可以為每個使用者建立群組，然後在您只想要觸達該使用者時，傳送一則訊息給該群組。</span><span class="sxs-lookup"><span data-stu-id="247c3-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="247c3-139">每個群組的名稱都是使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="247c3-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="247c3-140">如果使用者有一個以上的連線，每個連線識別碼都會新增至使用者的群組。</span><span class="sxs-lookup"><span data-stu-id="247c3-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="247c3-141">當使用者中斷連線時，您不應該手動從群組中移除使用者。</span><span class="sxs-lookup"><span data-stu-id="247c3-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="247c3-142">SignalR 架構會自動執行此動作。</span><span class="sxs-lookup"><span data-stu-id="247c3-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="247c3-143">下列範例顯示如何執行單一使用者群組。</span><span class="sxs-lookup"><span data-stu-id="247c3-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="247c3-144">永久的外部儲存體</span><span class="sxs-lookup"><span data-stu-id="247c3-144">Permanent, external storage</span></span>

<span data-ttu-id="247c3-145">本主題說明如何使用資料庫或 Azure 資料表儲存體來儲存連接資訊。</span><span class="sxs-lookup"><span data-stu-id="247c3-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="247c3-146">當您有多部網頁伺服器時，這個方法就可以運作，因為每個 web 伺服器都能與相同的資料存放庫互動。</span><span class="sxs-lookup"><span data-stu-id="247c3-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="247c3-147">如果您的 web 伺服器停止運作，或應用程式重新開機，則不會呼叫 `OnDisconnected` 方法。</span><span class="sxs-lookup"><span data-stu-id="247c3-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="247c3-148">因此，您的資料存放庫可能會有不再有效之連接識別碼的記錄。</span><span class="sxs-lookup"><span data-stu-id="247c3-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="247c3-149">若要清除這些孤立的記錄，您可能會想要讓在與您的應用程式相關的時間範圍以外建立的任何連接失效。</span><span class="sxs-lookup"><span data-stu-id="247c3-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="247c3-150">本節中的範例包含一個值，可在建立連接時進行追蹤，但不會顯示如何清除舊記錄，因為您可能會想要做為背景進程。</span><span class="sxs-lookup"><span data-stu-id="247c3-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="247c3-151">資料庫</span><span class="sxs-lookup"><span data-stu-id="247c3-151">Database</span></span>

<span data-ttu-id="247c3-152">下列範例示範如何在資料庫中保留連接和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="247c3-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="247c3-153">您可以使用任何資料存取技術;不過，下列範例顯示如何使用 Entity Framework 定義模型。</span><span class="sxs-lookup"><span data-stu-id="247c3-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="247c3-154">這些實體模型會對應到資料庫資料表和欄位。</span><span class="sxs-lookup"><span data-stu-id="247c3-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="247c3-155">視應用程式的需求而定，您的資料結構可能會有很大的差異。</span><span class="sxs-lookup"><span data-stu-id="247c3-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="247c3-156">第一個範例示範如何定義可以與許多連接實體相關聯的使用者實體。</span><span class="sxs-lookup"><span data-stu-id="247c3-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="247c3-157">然後，您可以從中樞使用如下所示的程式碼，追蹤每個連線的狀態。</span><span class="sxs-lookup"><span data-stu-id="247c3-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="247c3-158">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="247c3-158">Azure table storage</span></span>

<span data-ttu-id="247c3-159">下列 Azure 資料表儲存體範例類似于資料庫範例。</span><span class="sxs-lookup"><span data-stu-id="247c3-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="247c3-160">它不包含開始使用 Azure 表格儲存體服務所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="247c3-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="247c3-161">如需相關資訊，請參閱[如何使用 .net 的資料表儲存體](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。</span><span class="sxs-lookup"><span data-stu-id="247c3-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="247c3-162">下列範例顯示用來儲存連接資訊的資料表實體。</span><span class="sxs-lookup"><span data-stu-id="247c3-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="247c3-163">它會依使用者名稱分割資料，並依連接識別碼來識別每個實體，讓使用者可以隨時擁有多個連接。</span><span class="sxs-lookup"><span data-stu-id="247c3-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="247c3-164">在中樞中，您可以追蹤每個使用者連接的狀態。</span><span class="sxs-lookup"><span data-stu-id="247c3-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
