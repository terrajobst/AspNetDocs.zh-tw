---
uid: signalr/overview/older-versions/working-with-groups
title: 在 SignalR 1.x 中使用群組 |Microsoft Docs
author: bradygaster
description: 本主題說明如何使用中樞 API 來保存群組成員資格資訊。
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579363"
---
# <a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="8094e-103">使用 SignalR 1.x 中的群組</span><span class="sxs-lookup"><span data-stu-id="8094e-103">Working with Groups in SignalR 1.x</span></span>

<span data-ttu-id="8094e-104">由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8094e-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="8094e-105">本主題說明如何將使用者新增至群組，並保存群組成員資格資訊。</span><span class="sxs-lookup"><span data-stu-id="8094e-105">This topic describes how to add users to groups and persist group membership information.</span></span>

## <a name="overview"></a><span data-ttu-id="8094e-106">概觀</span><span class="sxs-lookup"><span data-stu-id="8094e-106">Overview</span></span>

<span data-ttu-id="8094e-107">SignalR 中的群組提供一種方法，可將訊息廣播到已連線用戶端的指定子集。</span><span class="sxs-lookup"><span data-stu-id="8094e-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="8094e-108">群組可以有任意數目的用戶端，而用戶端可以是任意數目群組的成員。</span><span class="sxs-lookup"><span data-stu-id="8094e-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="8094e-109">您不需要明確建立群組。</span><span class="sxs-lookup"><span data-stu-id="8094e-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="8094e-110">實際上，當您第一次在群組的呼叫中指定其名稱時，會自動建立群組。 [加入] 會在您從其中的成員資格移除最後一個連接時刪除。</span><span class="sxs-lookup"><span data-stu-id="8094e-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="8094e-111">如需使用群組的簡介，請參閱《中樞 API-伺服器指南》中的[如何從中樞類別管理群組成員資格](index.md)。</span><span class="sxs-lookup"><span data-stu-id="8094e-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="8094e-112">沒有 API 可取得群組成員資格清單或群組清單。</span><span class="sxs-lookup"><span data-stu-id="8094e-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="8094e-113">SignalR 會根據 pub/sub 模型將訊息傳送至用戶端和群組，而伺服器不會維護群組或群組成員資格的清單。</span><span class="sxs-lookup"><span data-stu-id="8094e-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="8094e-114">這有助於最大化擴充性，因為每當您將節點加入至 web 伺服陣列時，SignalR 維護的任何狀態都必須傳播到新的節點。</span><span class="sxs-lookup"><span data-stu-id="8094e-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="8094e-115">當您使用 `Groups.Add` 方法將使用者新增至群組時，使用者會在目前的連線期間收到導向該群組的訊息，但該群組中的使用者成員資格不會保存在目前的連線範圍之外。</span><span class="sxs-lookup"><span data-stu-id="8094e-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="8094e-116">如果您想要永久保留群組和群組成員資格的相關資訊，您必須將該資料儲存在資料庫或 Azure 資料表儲存體之類的儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="8094e-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="8094e-117">然後，每次使用者連線到您的應用程式時，您會從使用者所屬的儲存機制中抓取，並手動將該使用者新增至這些群組。</span><span class="sxs-lookup"><span data-stu-id="8094e-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="8094e-118">在暫時中斷之後重新連線時，使用者會自動重新加入先前指派的群組。</span><span class="sxs-lookup"><span data-stu-id="8094e-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="8094e-119">自動重新加入群組只有在重新連接時才適用，而不是在建立新的連接時使用。</span><span class="sxs-lookup"><span data-stu-id="8094e-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="8094e-120">數位簽署的權杖會從用戶端傳遞，其中包含先前指派之群組的清單。</span><span class="sxs-lookup"><span data-stu-id="8094e-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="8094e-121">如果您想要確認使用者是否屬於要求的群組，您可以覆寫預設行為。</span><span class="sxs-lookup"><span data-stu-id="8094e-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="8094e-122">本主題包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="8094e-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="8094e-123">新增和移除使用者</span><span class="sxs-lookup"><span data-stu-id="8094e-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="8094e-124">呼叫群組的成員</span><span class="sxs-lookup"><span data-stu-id="8094e-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="8094e-125">在資料庫中儲存群組成員資格</span><span class="sxs-lookup"><span data-stu-id="8094e-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="8094e-126">在 Azure 資料表儲存體中儲存群組成員資格</span><span class="sxs-lookup"><span data-stu-id="8094e-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="8094e-127">重新連接時驗證群組成員資格</span><span class="sxs-lookup"><span data-stu-id="8094e-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="8094e-128">新增和移除使用者</span><span class="sxs-lookup"><span data-stu-id="8094e-128">Adding and removing users</span></span>

<span data-ttu-id="8094e-129">若要新增或移除群組中的使用者，您可以呼叫[add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)或[remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法，並傳入使用者的連接識別碼和群組的名稱作為參數。</span><span class="sxs-lookup"><span data-stu-id="8094e-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="8094e-130">當連接結束時，您不需要手動從群組中移除使用者。</span><span class="sxs-lookup"><span data-stu-id="8094e-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="8094e-131">下列範例顯示中樞方法中使用的 `Groups.Add` 和 `Groups.Remove` 方法。</span><span class="sxs-lookup"><span data-stu-id="8094e-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="8094e-132">`Groups.Add` 和 `Groups.Remove` 方法會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="8094e-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="8094e-133">如果您想要將用戶端新增至群組，並使用群組立即將訊息傳送至用戶端，您必須確定群組. Add 方法會先完成。</span><span class="sxs-lookup"><span data-stu-id="8094e-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="8094e-134">下列程式碼範例示範如何執行這項作業，其中一個方法是使用在 .NET 4.5 中運作的程式碼，另一個則是使用在 .NET 4 中運作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8094e-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="8094e-135">非同步 .NET 4.5 範例</span><span class="sxs-lookup"><span data-stu-id="8094e-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="8094e-136">非同步 .NET 4 範例</span><span class="sxs-lookup"><span data-stu-id="8094e-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="8094e-137">一般來說，呼叫 `Groups.Remove` 方法時不應該包含 `await`，因為您嘗試移除的連線識別碼可能無法再使用。</span><span class="sxs-lookup"><span data-stu-id="8094e-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="8094e-138">在此情況下，會在要求超時之後擲回 `TaskCanceledException`。如果您的應用程式必須在將訊息傳送至群組之前，確保已從群組中移除使用者，您可以在群組之前加入 `await`。請移除，然後攔截可能會擲回的 `TaskCanceledException` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8094e-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="8094e-139">呼叫群組的成員</span><span class="sxs-lookup"><span data-stu-id="8094e-139">Calling members of a group</span></span>

<span data-ttu-id="8094e-140">您可以將訊息傳送給群組的所有成員，或只傳送給群組的指定成員，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="8094e-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="8094e-141">指定群組中**所有**已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="8094e-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="8094e-142">指定群組中所有已連線的用戶端，**但指定的用戶端除外，但**由連接識別碼識別。</span><span class="sxs-lookup"><span data-stu-id="8094e-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="8094e-143">指定群組中的所有已連線用戶端 **（呼叫用戶端除外**）。</span><span class="sxs-lookup"><span data-stu-id="8094e-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="8094e-144">在資料庫中儲存群組成員資格</span><span class="sxs-lookup"><span data-stu-id="8094e-144">Storing group membership in a database</span></span>

<span data-ttu-id="8094e-145">下列範例示範如何在資料庫中保留群組和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="8094e-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="8094e-146">您可以使用任何資料存取技術;不過，下列範例顯示如何使用 Entity Framework 定義模型。</span><span class="sxs-lookup"><span data-stu-id="8094e-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="8094e-147">這些實體模型會對應到資料庫資料表和欄位。</span><span class="sxs-lookup"><span data-stu-id="8094e-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="8094e-148">視應用程式的需求而定，您的資料結構可能會有很大的差異。</span><span class="sxs-lookup"><span data-stu-id="8094e-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="8094e-149">這個範例包含名為 `ConversationRoom` 的類別，這對應用程式而言是唯一的，可讓使用者加入有關不同主題（例如運動或園藝）的交談。</span><span class="sxs-lookup"><span data-stu-id="8094e-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="8094e-150">此範例也包含連接的類別。</span><span class="sxs-lookup"><span data-stu-id="8094e-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="8094e-151">不一定需要連接類別來追蹤群組成員資格，但通常是追蹤使用者的健全解決方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="8094e-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="8094e-152">然後，在中樞內，您可以從資料庫中取出群組和使用者資訊，並手動將使用者新增至適當的群組。</span><span class="sxs-lookup"><span data-stu-id="8094e-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="8094e-153">此範例不包含用於追蹤使用者連接的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8094e-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="8094e-154">在此範例中，`await` 關鍵字不會在 `Groups.Add` 之前套用，因為訊息不會立即傳送給群組的成員。</span><span class="sxs-lookup"><span data-stu-id="8094e-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="8094e-155">如果您想要在加入新成員之後立即傳送訊息給群組的所有成員，您會想要套用 `await` 關鍵字，以確保非同步作業已完成。</span><span class="sxs-lookup"><span data-stu-id="8094e-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="8094e-156">在 Azure 資料表儲存體中儲存群組成員資格</span><span class="sxs-lookup"><span data-stu-id="8094e-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="8094e-157">使用 Azure 資料表儲存體來儲存群組和使用者資訊與使用資料庫類似。</span><span class="sxs-lookup"><span data-stu-id="8094e-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="8094e-158">下列範例顯示的資料表實體會儲存使用者名稱和組名。</span><span class="sxs-lookup"><span data-stu-id="8094e-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="8094e-159">在中樞中，您會在使用者連接時，抓取指派的群組。</span><span class="sxs-lookup"><span data-stu-id="8094e-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="8094e-160">重新連接時驗證群組成員資格</span><span class="sxs-lookup"><span data-stu-id="8094e-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="8094e-161">根據預設，SignalR 會在中斷連線時，自動將使用者重新指派給適當的群組，例如在連接逾時之前卸載並重新建立連接。重新連接時，會在權杖中傳遞使用者的群組資訊，而且該權杖會在伺服器上進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8094e-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="8094e-162">如需重新加入使用者對群組之驗證程式的相關資訊，請參閱重新[連接時重新加入群組](index.md)。</span><span class="sxs-lookup"><span data-stu-id="8094e-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="8094e-163">一般而言，您應該在重新連線時使用自動重新加入群組的預設行為。</span><span class="sxs-lookup"><span data-stu-id="8094e-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="8094e-164">SignalR 群組不是用於限制敏感性資料存取的安全性機制。</span><span class="sxs-lookup"><span data-stu-id="8094e-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="8094e-165">不過，如果您的應用程式必須在重新連接時再次檢查使用者的群組成員資格，您可以覆寫預設行為。</span><span class="sxs-lookup"><span data-stu-id="8094e-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="8094e-166">變更預設行為可能會增加資料庫的負擔，因為必須針對每個重新連線抓取使用者的群組成員資格，而不是只有在使用者連線時才進行。</span><span class="sxs-lookup"><span data-stu-id="8094e-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="8094e-167">如果您必須在重新連接時驗證群組成員資格，請建立新的中樞管線模組，以傳回指派群組的清單，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8094e-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="8094e-168">然後，將該模組新增至中樞管線，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8094e-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
