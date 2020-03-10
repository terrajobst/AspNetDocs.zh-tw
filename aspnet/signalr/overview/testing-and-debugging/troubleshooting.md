---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: SignalR 疑難排解 |Microsoft Docs
author: bradygaster
description: 本文說明開發 SignalR 應用程式的常見問題。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: bcd273d839aed64ad2712eb503dd1942a2d4e355
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578824"
---
# <a name="signalr-troubleshooting"></a><span data-ttu-id="42a55-103">SignalR 疑難排解</span><span class="sxs-lookup"><span data-stu-id="42a55-103">SignalR Troubleshooting</span></span>

<span data-ttu-id="42a55-104">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="42a55-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="42a55-105">本檔說明 SignalR 的常見疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="42a55-105">This document describes common troubleshooting issues with SignalR.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="42a55-106">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="42a55-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="42a55-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="42a55-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="42a55-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="42a55-108">.NET 4.5</span></span>
> - <span data-ttu-id="42a55-109">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="42a55-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="42a55-110">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="42a55-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="42a55-111">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="42a55-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="42a55-112">問題與意見</span><span class="sxs-lookup"><span data-stu-id="42a55-112">Questions and comments</span></span>
>
> <span data-ttu-id="42a55-113">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="42a55-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="42a55-114">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="42a55-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="42a55-115">本檔包含下列各節。</span><span class="sxs-lookup"><span data-stu-id="42a55-115">This document contains the following sections.</span></span>

- [<span data-ttu-id="42a55-116">在用戶端與伺服器之間呼叫方法無訊息失敗</span><span class="sxs-lookup"><span data-stu-id="42a55-116">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="42a55-117">將 IIS websocket 設定為 ping/乒乓球以偵測出無作用的用戶端</span><span class="sxs-lookup"><span data-stu-id="42a55-117">Configuring IIS websockets to ping/pong to detect a dead client</span></span>](#pong)
- [<span data-ttu-id="42a55-118">其他連接問題</span><span class="sxs-lookup"><span data-stu-id="42a55-118">Other connection issues</span></span>](#other)
- [<span data-ttu-id="42a55-119">編譯和伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-119">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="42a55-120">Visual Studio 問題</span><span class="sxs-lookup"><span data-stu-id="42a55-120">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="42a55-121">Internet Information Services 問題</span><span class="sxs-lookup"><span data-stu-id="42a55-121">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="42a55-122">Microsoft Azure 問題</span><span class="sxs-lookup"><span data-stu-id="42a55-122">Microsoft Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="42a55-123">在用戶端與伺服器之間呼叫方法無訊息失敗</span><span class="sxs-lookup"><span data-stu-id="42a55-123">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="42a55-124">本節描述用戶端和伺服器之間方法呼叫失敗的可能原因，而不會有有意義的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42a55-124">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="42a55-125">在 SignalR 應用程式中，伺服器不會有用戶端所執行之方法的相關資訊;當伺服器叫用用戶端方法時，方法名稱和參數資料會傳送至用戶端，而且只有在該方法是以伺服器指定的格式存在時，才會執行它。</span><span class="sxs-lookup"><span data-stu-id="42a55-125">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="42a55-126">如果在用戶端上找不到相符的方法，就不會發生任何事，也不會在伺服器上引發錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42a55-126">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="42a55-127">若要進一步調查不會呼叫的用戶端方法，您可以在呼叫中樞上的啟動方法之前開啟記錄功能，以查看來自伺服器的呼叫。</span><span class="sxs-lookup"><span data-stu-id="42a55-127">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="42a55-128">若要在 JavaScript 應用程式中啟用記錄，請參閱[如何啟用用戶端記錄（JavaScript 用戶端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="42a55-128">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="42a55-129">若要在 .NET 用戶端應用程式中啟用記錄，請參閱[如何啟用用戶端記錄（.Net 用戶端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="42a55-129">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="42a55-130">拼錯的方法、不正確的方法簽章或不正確的中樞名稱</span><span class="sxs-lookup"><span data-stu-id="42a55-130">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="42a55-131">如果所呼叫方法的名稱或簽章不完全符合用戶端上的適當方法，則呼叫將會失敗。</span><span class="sxs-lookup"><span data-stu-id="42a55-131">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="42a55-132">確認伺服器所呼叫的方法名稱符合用戶端上的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="42a55-132">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="42a55-133">此外，SignalR 會使用 camel 大小寫方法建立中樞 proxy，如同在 JavaScript 中適用，因此會在用戶端 proxy 中呼叫在伺服器上 `SendMessage` 的方法 `sendMessage`。</span><span class="sxs-lookup"><span data-stu-id="42a55-133">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="42a55-134">如果您在伺服器端程式碼中使用 `HubName` 屬性，請確認所使用的名稱符合用來在用戶端上建立中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="42a55-134">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="42a55-135">如果您未使用 `HubName` 屬性，請確認 JavaScript 用戶端中的中樞名稱為 camel 大小寫，例如 chatHub，而不是 ChatHub。</span><span class="sxs-lookup"><span data-stu-id="42a55-135">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="42a55-136">用戶端上重複的方法名稱</span><span class="sxs-lookup"><span data-stu-id="42a55-136">Duplicate method name on client</span></span>

<span data-ttu-id="42a55-137">請確認您的用戶端上沒有重複的方法，只有大小寫不同。</span><span class="sxs-lookup"><span data-stu-id="42a55-137">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="42a55-138">如果您的用戶端應用程式有一個稱為 `sendMessage`的方法，請確認也沒有稱為 `SendMessage` 的方法。</span><span class="sxs-lookup"><span data-stu-id="42a55-138">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="42a55-139">用戶端上缺少 JSON 剖析器</span><span class="sxs-lookup"><span data-stu-id="42a55-139">Missing JSON parser on the client</span></span>

<span data-ttu-id="42a55-140">SignalR 需要有 JSON 剖析器，才能序列化伺服器和用戶端之間的呼叫。</span><span class="sxs-lookup"><span data-stu-id="42a55-140">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="42a55-141">如果您的用戶端沒有內建的 JSON 剖析器（例如 Internet Explorer 7），您必須在應用程式中包含一個。</span><span class="sxs-lookup"><span data-stu-id="42a55-141">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="42a55-142">您可以在[這裡](http://nuget.org/packages/json2)下載 JSON 剖析器。</span><span class="sxs-lookup"><span data-stu-id="42a55-142">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="42a55-143">混合中樞和 PersistentConnection 語法</span><span class="sxs-lookup"><span data-stu-id="42a55-143">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="42a55-144">SignalR 使用兩種通訊模型：中樞和 PersistentConnections。</span><span class="sxs-lookup"><span data-stu-id="42a55-144">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="42a55-145">在用戶端程式代碼中呼叫這兩種通訊模型的語法不同。</span><span class="sxs-lookup"><span data-stu-id="42a55-145">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="42a55-146">如果您已在伺服器程式碼中新增中樞，請確認您的所有用戶端程式代碼都使用適當的中樞語法。</span><span class="sxs-lookup"><span data-stu-id="42a55-146">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="42a55-147">**在 JavaScript 用戶端中建立 PersistentConnection 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-147">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="42a55-148">**在 JAVAscript 用戶端中建立中樞 Proxy 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-148">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="42a55-149">**C#將路由對應至 PersistentConnection 的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-149">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="42a55-150">**C#將路由對應至中樞的伺服器程式碼，如果您有多個應用程式，則為多個中樞**</span><span class="sxs-lookup"><span data-stu-id="42a55-150">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="42a55-151">在新增訂閱之前啟動連線</span><span class="sxs-lookup"><span data-stu-id="42a55-151">Connection started before subscriptions are added</span></span>

<span data-ttu-id="42a55-152">如果在可以從伺服器呼叫的方法加入至 proxy 之前，中樞的連線已啟動，則不會收到訊息。</span><span class="sxs-lookup"><span data-stu-id="42a55-152">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="42a55-153">下列 JavaScript 程式碼不會正確啟動中樞：</span><span class="sxs-lookup"><span data-stu-id="42a55-153">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="42a55-154">**不正確的 JavaScript 用戶端程式代碼將不允許接收中樞訊息**</span><span class="sxs-lookup"><span data-stu-id="42a55-154">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="42a55-155">請改為在呼叫 Start 之前新增方法訂閱：</span><span class="sxs-lookup"><span data-stu-id="42a55-155">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="42a55-156">**將訂用帳戶正確新增至中樞的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-156">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="42a55-157">中樞 proxy 上缺少方法名稱</span><span class="sxs-lookup"><span data-stu-id="42a55-157">Missing method name on the hub proxy</span></span>

<span data-ttu-id="42a55-158">確認伺服器上定義的方法已在用戶端上訂閱。</span><span class="sxs-lookup"><span data-stu-id="42a55-158">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="42a55-159">即使伺服器定義方法，仍然必須將它加入至用戶端 proxy。</span><span class="sxs-lookup"><span data-stu-id="42a55-159">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="42a55-160">方法可以透過下列方式新增至用戶端 proxy （請注意，方法會新增至中樞的 `client` 成員，而不是直接加入中樞）：</span><span class="sxs-lookup"><span data-stu-id="42a55-160">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="42a55-161">**將方法新增至中樞 proxy 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-161">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="42a55-162">中樞或中樞方法未宣告為公用</span><span class="sxs-lookup"><span data-stu-id="42a55-162">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="42a55-163">若要在用戶端上顯示，中樞的執行和方法必須宣告為 `public`。</span><span class="sxs-lookup"><span data-stu-id="42a55-163">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="42a55-164">從不同的應用程式存取中樞</span><span class="sxs-lookup"><span data-stu-id="42a55-164">Accessing hub from a different application</span></span>

<span data-ttu-id="42a55-165">SignalR Hub 只能透過執行 SignalR 用戶端的應用程式來存取。</span><span class="sxs-lookup"><span data-stu-id="42a55-165">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="42a55-166">SignalR 無法與其他通訊庫（例如 SOAP 或 WCF web 服務）相交互操作。如果您的目標平臺沒有可用的 SignalR 用戶端，您就無法直接存取伺服器的端點。</span><span class="sxs-lookup"><span data-stu-id="42a55-166">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="42a55-167">手動序列化資料</span><span class="sxs-lookup"><span data-stu-id="42a55-167">Manually serializing data</span></span>

<span data-ttu-id="42a55-168">SignalR 會自動使用 JSON 來序列化您的方法參數，而不需要自行執行此動作。</span><span class="sxs-lookup"><span data-stu-id="42a55-168">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="42a55-169">遠端中樞方法未在 OnDisconnected 函式的用戶端上執行</span><span class="sxs-lookup"><span data-stu-id="42a55-169">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="42a55-170">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-170">This behavior is by design.</span></span> <span data-ttu-id="42a55-171">呼叫 `OnDisconnected` 時，中樞已經進入 `Disconnected` 狀態，這不允許呼叫進一步的中樞方法。</span><span class="sxs-lookup"><span data-stu-id="42a55-171">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="42a55-172">**C#在 OnDisconnected 事件中正確執行程式碼的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-172">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a><span data-ttu-id="42a55-173">OnDisconnect 不會在一致的時間引發</span><span class="sxs-lookup"><span data-stu-id="42a55-173">OnDisconnect not firing at consistent times</span></span>

<span data-ttu-id="42a55-174">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-174">This behavior is by design.</span></span> <span data-ttu-id="42a55-175">當使用者嘗試從具有作用中 SignalR 連線的頁面離開時，SignalR 用戶端會進行最佳的嘗試，以通知伺服器用戶端連接將會停止。</span><span class="sxs-lookup"><span data-stu-id="42a55-175">When a user attempts to navigate away from a page with an active SignalR connection, the SignalR client will then make a best-effort attempt to notify the server that the client connection will be stopped.</span></span> <span data-ttu-id="42a55-176">如果 SignalR 用戶端的最佳嘗試無法連線到伺服器，伺服器將會在稍後可設定的 `DisconnectTimeout` 之後處置連接，此時將會引發 `OnDisconnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="42a55-176">If the SignalR client's best-effort attempt fails to reach the server, the server will dispose of the connection after a configurable `DisconnectTimeout` later, at which time the `OnDisconnected` event will fire.</span></span> <span data-ttu-id="42a55-177">如果 SignalR 用戶端的盡力嘗試成功，則會立即引發 `OnDisconnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="42a55-177">If the SignalR client's best-effort attempt is successful, the `OnDisconnected` event will fire immediately.</span></span>

<span data-ttu-id="42a55-178">如需設定 `DisconnectTimeout` 設定的詳細資訊，請參閱[處理連接存留期事件： DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout)。</span><span class="sxs-lookup"><span data-stu-id="42a55-178">For information on setting the `DisconnectTimeout` setting, see [Handling connection lifetime events: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).</span></span>

### <a name="connection-limit-reached"></a><span data-ttu-id="42a55-179">已達到連接限制</span><span class="sxs-lookup"><span data-stu-id="42a55-179">Connection limit reached</span></span>

<span data-ttu-id="42a55-180">在 Windows 7 之類的用戶端作業系統上使用完整版的 IIS 時，會強加10個連線限制。</span><span class="sxs-lookup"><span data-stu-id="42a55-180">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="42a55-181">使用用戶端 OS 時，請改用 IIS Express 以避免此限制。</span><span class="sxs-lookup"><span data-stu-id="42a55-181">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="42a55-182">未正確設定跨網域連線</span><span class="sxs-lookup"><span data-stu-id="42a55-182">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="42a55-183">如果跨網域連線（SignalR URL 與主控頁面不在相同網域中的連線）未正確設定，則連接可能會失敗，且不會出現錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42a55-183">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="42a55-184">如需如何啟用跨網域通訊的相關資訊，請參閱[如何建立跨網域](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)連線。</span><span class="sxs-lookup"><span data-stu-id="42a55-184">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="42a55-185">使用 NTLM （Active Directory）的連接在 .NET 用戶端中無法運作</span><span class="sxs-lookup"><span data-stu-id="42a55-185">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="42a55-186">如果連接未正確設定，在 .NET 用戶端應用程式中使用網域安全性的連接可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="42a55-186">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="42a55-187">若要在網域環境中使用 SignalR，請設定必要的連接屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="42a55-187">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="42a55-188">**C#執行連接認證的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-188">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a><span data-ttu-id="42a55-189">將 IIS websocket 設定為 ping/乒乓球以偵測出無作用的用戶端</span><span class="sxs-lookup"><span data-stu-id="42a55-189">Configuring IIS websockets to ping/pong to detect a dead client</span></span>

<span data-ttu-id="42a55-190">SignalR 伺服器不知道用戶端是否已失效，它們是否依賴連線失敗的基礎 websocket 通知，也就是 `OnClose` 回呼。</span><span class="sxs-lookup"><span data-stu-id="42a55-190">SignalR servers don't know if the client is dead or not and they rely on notification from the underlying websocket for connection failures, that is, the `OnClose` callback.</span></span> <span data-ttu-id="42a55-191">這個問題的解決方法之一，就是設定 IIS websocket 來為您進行 ping/乒乓球。</span><span class="sxs-lookup"><span data-stu-id="42a55-191">One solution to this problem is to configure IIS websockets to do the ping/pong for you.</span></span> <span data-ttu-id="42a55-192">這可確保當您的連線意外中斷時，您的連接將會關閉。</span><span class="sxs-lookup"><span data-stu-id="42a55-192">This ensures that your connection will close if it breaks unexpectedly.</span></span> <span data-ttu-id="42a55-193">如需詳細資訊，請參閱[這 stackoverflow 文章](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)。</span><span class="sxs-lookup"><span data-stu-id="42a55-193">For more information see [this stackoverflow post](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss).</span></span>

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="42a55-194">其他連接問題</span><span class="sxs-lookup"><span data-stu-id="42a55-194">Other connection issues</span></span>

<span data-ttu-id="42a55-195">本節說明連線期間所發生之特定徵兆或錯誤訊息的原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="42a55-195">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="42a55-196">「必須在可以傳送資料之前呼叫啟動」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-196">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="42a55-197">如果在啟動連接之前，程式碼參考 SignalR 物件，通常會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-197">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="42a55-198">在連接完成之後，必須新增處理常式的裝設，以及將呼叫在伺服器上定義之方法的 like。</span><span class="sxs-lookup"><span data-stu-id="42a55-198">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="42a55-199">請注意，`Start` 的呼叫是非同步，因此呼叫之後的程式碼可能會在完成之前執行。</span><span class="sxs-lookup"><span data-stu-id="42a55-199">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="42a55-200">在連接完全啟動之後加入處理常式的最佳方式，是將它們放入回呼函式，並以參數的形式傳遞給 start 方法：</span><span class="sxs-lookup"><span data-stu-id="42a55-200">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="42a55-201">**可正確加入參考 SignalR 物件之事件處理常式的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-201">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="42a55-202">如果在仍在參考 SignalR 物件的情況下，連接停止，也會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-202">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="42a55-203">「已永久移動301」或「已暫時移動302」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-203">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="42a55-204">如果專案包含名為 SignalR 的資料夾，這會干擾自動建立的 proxy，可能會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-204">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="42a55-205">若要避免這個錯誤，請不要在應用程式中使用名為 `SignalR` 的資料夾，或關閉自動產生 proxy。</span><span class="sxs-lookup"><span data-stu-id="42a55-205">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="42a55-206">如需更多詳細資料，請參閱[產生的 Proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="42a55-206">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="42a55-207">.NET 或 Silverlight 用戶端發生「403禁止」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-207">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="42a55-208">跨網域的環境中，如果未正確啟用跨網域通訊，則可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-208">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="42a55-209">如需如何啟用跨網域通訊的相關資訊，請參閱[如何建立跨網域](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)連線。</span><span class="sxs-lookup"><span data-stu-id="42a55-209">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="42a55-210">若要在 Silverlight 用戶端中建立跨網域連接，請參閱[silverlight 用戶端的跨網域](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)連線。</span><span class="sxs-lookup"><span data-stu-id="42a55-210">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="42a55-211">「找不到404」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-211">"404 Not Found" error</span></span>

<span data-ttu-id="42a55-212">發生此問題的原因有好幾個。</span><span class="sxs-lookup"><span data-stu-id="42a55-212">There are several causes for this issue.</span></span> <span data-ttu-id="42a55-213">確認下列所有事項：</span><span class="sxs-lookup"><span data-stu-id="42a55-213">Verify all of the following:</span></span>

- <span data-ttu-id="42a55-214">**中樞 proxy 位址參考的格式不正確：** 如果所產生之中樞 proxy 位址的參考格式不正確，通常會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-214">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="42a55-215">確認已正確地對中樞位址進行參考。</span><span class="sxs-lookup"><span data-stu-id="42a55-215">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="42a55-216">如需詳細資訊，請參閱[如何參考動態產生的 proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 。</span><span class="sxs-lookup"><span data-stu-id="42a55-216">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="42a55-217">新增**路由至應用程式，再新增中樞路由：** 如果您的應用程式使用其他路由，請確認新增的第一個路由是 `MapSignalR`的呼叫。</span><span class="sxs-lookup"><span data-stu-id="42a55-217">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapSignalR`.</span></span>
- <span data-ttu-id="42a55-218">**使用 IIS 7 或7.5，而不更新無副檔名 url：** 使用 IIS 7 或7.5 需要更新無副檔名 Url，讓伺服器可以在 `/signalr/hubs`提供中樞定義的存取權。</span><span class="sxs-lookup"><span data-stu-id="42a55-218">**Using IIS 7 or 7.5 without the update for extensionless URLs:** Using IIS 7 or 7.5 requires an update for extensionless URLs so that the server can provide access to the hub definitions at `/signalr/hubs`.</span></span> <span data-ttu-id="42a55-219">您可以在[這裡](https://support.microsoft.com/kb/980368)找到更新。</span><span class="sxs-lookup"><span data-stu-id="42a55-219">The update can be found [here](https://support.microsoft.com/kb/980368).</span></span>
- <span data-ttu-id="42a55-220">**IIS 快取已過期或已**損毀：若要確認快取內容不是過時的，請在 PowerShell 視窗中輸入下列命令來清除快取：</span><span class="sxs-lookup"><span data-stu-id="42a55-220">**IIS cache out of date or corrupt:** To verify that the cache contents are not out of date, enter the following command in a PowerShell window to clear the cache:</span></span>

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a><span data-ttu-id="42a55-221">「500內部伺服器錯誤」</span><span class="sxs-lookup"><span data-stu-id="42a55-221">"500 Internal Server Error"</span></span>

<span data-ttu-id="42a55-222">這是一個非常一般的錯誤，可能會有各種不同的原因。</span><span class="sxs-lookup"><span data-stu-id="42a55-222">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="42a55-223">錯誤的詳細資料應該會出現在伺服器的事件記錄檔中，或透過偵測伺服器來找到。</span><span class="sxs-lookup"><span data-stu-id="42a55-223">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="42a55-224">藉由開啟伺服器上的詳細錯誤，可取得更詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="42a55-224">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="42a55-225">如需詳細資訊，請參閱[如何處理中樞類別中的錯誤](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="42a55-225">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

<span data-ttu-id="42a55-226">如果防火牆或 proxy 設定不正確，導致重寫要求標頭時，通常也會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-226">This error is also commonly seen if a firewall or proxy is not configured properly, causing the request headers to be rewritten.</span></span> <span data-ttu-id="42a55-227">解決方法是確保防火牆或 proxy 上已啟用埠80。</span><span class="sxs-lookup"><span data-stu-id="42a55-227">The solution is to make sure that port 80 is enabled on the firewall or proxy.</span></span>

### <a name="unexpected-response-code-500"></a><span data-ttu-id="42a55-228">「未預期的回應碼：500」</span><span class="sxs-lookup"><span data-stu-id="42a55-228">"Unexpected response code: 500"</span></span>

<span data-ttu-id="42a55-229">如果應用程式中使用的 .NET framework 版本與 web.config 中指定的版本不相符，可能會發生此錯誤。解決方法是確認應用程式設定和 web.config 檔案中都使用 .NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="42a55-229">This error may occur if the version of .NET framework used in the application does not match the version specified in Web.Config. The solution is to verify that .NET 4.5 is used in both the application settings and the Web.Config file.</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="42a55-230">「TypeError： &lt;hubType&gt; 未定義」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-230">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="42a55-231">如果未正確呼叫 `MapSignalR`，將會產生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-231">This error will result if the call to `MapSignalR` is not made properly.</span></span> <span data-ttu-id="42a55-232">如需詳細資訊，請參閱[如何註冊 SignalR 中介軟體和設定 SignalR 選項](../guide-to-the-api/hubs-api-guide-server.md#route)。</span><span class="sxs-lookup"><span data-stu-id="42a55-232">See [How to register SignalR Middleware and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="42a55-233">JsonSerializationException 已由使用者程式碼未處理</span><span class="sxs-lookup"><span data-stu-id="42a55-233">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="42a55-234">確認您傳送至方法的參數不包含非可序列化的類型（例如檔案控制代碼或資料庫連接）。</span><span class="sxs-lookup"><span data-stu-id="42a55-234">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="42a55-235">如果您需要在不想要傳送至用戶端的伺服器端物件上使用成員（基於安全性或序列化的原因），請使用 `JSONIgnore` 屬性。</span><span class="sxs-lookup"><span data-stu-id="42a55-235">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="42a55-236">「通訊協定錯誤：未知的傳輸」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-236">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="42a55-237">如果用戶端不支援 SignalR 所使用的傳輸，則可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-237">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="42a55-238">如需可與 SignalR 搭配使用之瀏覽器的相關資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="42a55-238">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="42a55-239">「JavaScript 中樞 proxy 產生已停用。」</span><span class="sxs-lookup"><span data-stu-id="42a55-239">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="42a55-240">如果設定了 `DisableJavaScriptProxies`，同時包含 `signalr/hubs`上動態產生之 proxy 的參考，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-240">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="42a55-241">如需手動建立 proxy 的詳細資訊，請參閱[產生的 proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="42a55-241">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="42a55-242">「連線識別碼的格式不正確」或「使用者識別在使用中的 SignalR 連接期間無法變更」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-242">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="42a55-243">如果正在使用驗證，而且在連線停止之前，用戶端已登出，可能會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-243">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="42a55-244">解決方法是在登出用戶端之前，先停止 SignalR 連接。</span><span class="sxs-lookup"><span data-stu-id="42a55-244">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="42a55-245">「未攔截的錯誤： SignalR：找不到 jQuery。</span><span class="sxs-lookup"><span data-stu-id="42a55-245">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="42a55-246">請確定已在 SignalR .js 檔案之前參考 jQuery」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-246">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="42a55-247">SignalR JavaScript 用戶端需要 jQuery 才能執行。</span><span class="sxs-lookup"><span data-stu-id="42a55-247">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="42a55-248">請確認您對 jQuery 的參考是否正確、使用的路徑是否有效，以及 jQuery 的參考是否在 SignalR 的參考之前。</span><span class="sxs-lookup"><span data-stu-id="42a55-248">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="42a55-249">「未攔截的 TypeError：無法讀取屬性 '&lt;屬性&gt;' 未定義」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-249">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="42a55-250">此錯誤的結果是未正確參考 jQuery 或中樞 proxy。</span><span class="sxs-lookup"><span data-stu-id="42a55-250">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="42a55-251">請確認您對 jQuery 和中樞 proxy 的參考是否正確、使用的路徑是否有效，以及 jQuery 的參考是否在中樞 proxy 的參考之前。</span><span class="sxs-lookup"><span data-stu-id="42a55-251">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="42a55-252">中樞 proxy 的預設參考看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="42a55-252">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="42a55-253">**正確參考中樞 proxy 的 HTML 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="42a55-253">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="42a55-254">「RuntimeBinderException 由使用者程式碼未處理」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-254">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="42a55-255">使用不正確的 `Hub.On` 多載時，可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-255">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="42a55-256">如果方法有傳回值，則傳回型別必須指定為泛型型別參數：</span><span class="sxs-lookup"><span data-stu-id="42a55-256">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="42a55-257">**在用戶端上定義的方法（不含產生的 proxy）**</span><span class="sxs-lookup"><span data-stu-id="42a55-257">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="42a55-258">連接識別碼不一致，或頁面載入之間的連接中斷</span><span class="sxs-lookup"><span data-stu-id="42a55-258">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="42a55-259">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-259">This behavior is by design.</span></span> <span data-ttu-id="42a55-260">由於中樞物件裝載于 page 物件中，因此當頁面重新整理時，中樞會遭到終結。</span><span class="sxs-lookup"><span data-stu-id="42a55-260">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="42a55-261">多頁應用程式必須維護使用者與連接識別碼之間的關聯，以便在頁面載入之間保持一致。</span><span class="sxs-lookup"><span data-stu-id="42a55-261">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="42a55-262">連接識別碼可以儲存在伺服器上的 `ConcurrentDictionary` 物件或資料庫中。</span><span class="sxs-lookup"><span data-stu-id="42a55-262">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="42a55-263">「值不能為 null」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-263">"Value cannot be null" error</span></span>

<span data-ttu-id="42a55-264">目前不支援具有選擇性參數的伺服器端方法;如果省略了選擇性參數，方法將會失敗。</span><span class="sxs-lookup"><span data-stu-id="42a55-264">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="42a55-265">如需詳細資訊，請參閱[選擇性參數](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="42a55-265">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="42a55-266">「Firefox 無法在 Firebug 時建立與伺服器的連接，&lt;位址&gt;」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-266">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="42a55-267">如果 WebSocket 傳輸的協商失敗，而改用另一個傳輸，則會在 Firebug 中看到此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42a55-267">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="42a55-268">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-268">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="42a55-269">.NET 用戶端應用程式中的「根據驗證程式，遠端憑證無效」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-269">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="42a55-270">如果您的伺服器需要自訂用戶端憑證，您可以在提出要求之前，將 x509certificate 新增至連接。</span><span class="sxs-lookup"><span data-stu-id="42a55-270">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="42a55-271">使用 `Connection.AddClientCertificate`將憑證新增至連接。</span><span class="sxs-lookup"><span data-stu-id="42a55-271">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="42a55-272">驗證超時之後中斷連接</span><span class="sxs-lookup"><span data-stu-id="42a55-272">Connection drops after authentication times out</span></span>

<span data-ttu-id="42a55-273">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-273">This behavior is by design.</span></span> <span data-ttu-id="42a55-274">當連接啟用時，無法修改驗證認證;若要重新整理認證，必須停止並重新啟動連接。</span><span class="sxs-lookup"><span data-stu-id="42a55-274">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="42a55-275">使用 jQuery Mobile 時，會呼叫 OnConnected 兩次</span><span class="sxs-lookup"><span data-stu-id="42a55-275">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="42a55-276">jQuery Mobile 的 `initializePage` 函式會強制重新執行每個頁面中的腳本，因此會建立第二個連接。</span><span class="sxs-lookup"><span data-stu-id="42a55-276">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="42a55-277">此問題的解決方案包括：</span><span class="sxs-lookup"><span data-stu-id="42a55-277">Solutions for this issue include:</span></span>

- <span data-ttu-id="42a55-278">在您的 JavaScript 檔案之前包含 jQuery Mobile 的參考。</span><span class="sxs-lookup"><span data-stu-id="42a55-278">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="42a55-279">藉由設定 `$.mobile.autoInitializePage = false`來停用 `initializePage` 函數。</span><span class="sxs-lookup"><span data-stu-id="42a55-279">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="42a55-280">等候頁面完成初始化，再開始連接。</span><span class="sxs-lookup"><span data-stu-id="42a55-280">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="42a55-281">使用伺服器傳送事件的 Silverlight 應用程式中的訊息延遲</span><span class="sxs-lookup"><span data-stu-id="42a55-281">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="42a55-282">在 Silverlight 上使用伺服器傳送事件時，會延遲訊息。</span><span class="sxs-lookup"><span data-stu-id="42a55-282">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="42a55-283">若要改為強制使用長輪詢，請在啟動連線時使用下列內容：</span><span class="sxs-lookup"><span data-stu-id="42a55-283">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="42a55-284">「拒絕許可權」使用永久框架通訊協定</span><span class="sxs-lookup"><span data-stu-id="42a55-284">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="42a55-285">這是已知的問題，如[這裡](https://github.com/SignalR/SignalR/issues/1963)所述。</span><span class="sxs-lookup"><span data-stu-id="42a55-285">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="42a55-286">您可以使用最新的 JQuery 程式庫看到此徵兆;因應措施是將您的應用程式降級至 JQuery 1.8.2。</span><span class="sxs-lookup"><span data-stu-id="42a55-286">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a><span data-ttu-id="42a55-287">「InvalidOperationException：不是有效的 web 通訊端要求。</span><span class="sxs-lookup"><span data-stu-id="42a55-287">"InvalidOperationException: Not a valid web socket request.</span></span>

<span data-ttu-id="42a55-288">如果使用 WebSocket 通訊協定，但網路 proxy 正在修改要求標頭，則可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-288">This error may occur if the WebSocket protocol is used, but the network proxy is modifying the request headers.</span></span> <span data-ttu-id="42a55-289">解決方法是將 proxy 設定為允許埠80上的 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="42a55-289">The solution is to configure the proxy to allow WebSocket on port 80.</span></span>

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a><span data-ttu-id="42a55-290">「例外狀況：當用戶端呼叫伺服器上的方法時，無法解析 &lt;方法名稱&gt; 方法」</span><span class="sxs-lookup"><span data-stu-id="42a55-290">"Exception: &lt;method name&gt; method could not be resolved" when client calls method on server</span></span>

<span data-ttu-id="42a55-291">此錯誤可能是因為使用的資料類型無法在 JSON 承載中探索到，例如陣列。</span><span class="sxs-lookup"><span data-stu-id="42a55-291">This error can result from using data types that cannot be discovered in a JSON payload, such as Array.</span></span> <span data-ttu-id="42a55-292">因應措施是使用可由 JSON 探索的資料類型，例如 IList。</span><span class="sxs-lookup"><span data-stu-id="42a55-292">The workaround is to use a data type that is discoverable by JSON, such as IList.</span></span> <span data-ttu-id="42a55-293">如需詳細資訊，請參閱[.Net 用戶端無法呼叫具有陣列參數的中樞方法](https://github.com/SignalR/SignalR/issues/2672)。</span><span class="sxs-lookup"><span data-stu-id="42a55-293">For more information, see [.NET Client unable to call hub methods with array parameters](https://github.com/SignalR/SignalR/issues/2672).</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="42a55-294">編譯和伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-294">Compilation and server-side errors</span></span>

 <span data-ttu-id="42a55-295">下一節包含編譯器和伺服器端執行時間錯誤的可能解決方案。</span><span class="sxs-lookup"><span data-stu-id="42a55-295">The following section contains possible solutions to compiler and server-side runtime errors.</span></span>

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="42a55-296">中樞實例的參考為 null</span><span class="sxs-lookup"><span data-stu-id="42a55-296">Reference to Hub instance is null</span></span>

<span data-ttu-id="42a55-297">由於會針對每個連接建立中樞實例，因此您無法自行在程式碼中建立中樞的實例。</span><span class="sxs-lookup"><span data-stu-id="42a55-297">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="42a55-298">若要從中樞本身外部呼叫中樞上的方法，請參閱[如何從中樞類別外部呼叫用戶端方法和管理群組](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，以瞭解如何取得中樞內容的參考。</span><span class="sxs-lookup"><span data-stu-id="42a55-298">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="42a55-299">HTTPCoNtext。會話為 null</span><span class="sxs-lookup"><span data-stu-id="42a55-299">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="42a55-300">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-300">This behavior is by design.</span></span> <span data-ttu-id="42a55-301">SignalR 不支援 ASP.NET 會話狀態，因為啟用會話狀態會中斷雙工訊息。</span><span class="sxs-lookup"><span data-stu-id="42a55-301">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="42a55-302">沒有適合的覆寫方法</span><span class="sxs-lookup"><span data-stu-id="42a55-302">No suitable method to override</span></span>

<span data-ttu-id="42a55-303">如果您使用舊版檔或 blog 中的程式碼，可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-303">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="42a55-304">請確認您未參考已變更或已淘汰之方法的名稱（例如 `OnConnectedAsync`）。</span><span class="sxs-lookup"><span data-stu-id="42a55-304">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="42a55-305">HostCoNtextExtensions. WebSocketServerUrl 為 null</span><span class="sxs-lookup"><span data-stu-id="42a55-305">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="42a55-306">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-306">This behavior is by design.</span></span> <span data-ttu-id="42a55-307">這個成員已被取代，不應使用。</span><span class="sxs-lookup"><span data-stu-id="42a55-307">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="42a55-308">「路由集合中已有名為 ' signalr ' 的路由」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-308">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="42a55-309">如果您的應用程式呼叫了兩次 `MapSignalR`，就會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42a55-309">This error will be seen if `MapSignalR` is called twice by your application.</span></span> <span data-ttu-id="42a55-310">某些範例應用程式會直接在 Startup 類別中呼叫 `MapSignalR`;其他則會在包裝函式類別中進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="42a55-310">Some example applications call `MapSignalR` directly in the Startup class; others make the call in a wrapper class.</span></span> <span data-ttu-id="42a55-311">請確定您的應用程式不會同時執行這兩項操作。</span><span class="sxs-lookup"><span data-stu-id="42a55-311">Ensure that your application does not do both.</span></span>

### <a name="websocket-is-not-used"></a><span data-ttu-id="42a55-312">未使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="42a55-312">WebSocket is not used</span></span>

<span data-ttu-id="42a55-313">如果您已確認您的伺服器和用戶端符合 WebSocket 的需求（列在[支援的平臺](../getting-started/supported-platforms.md)檔中），您將需要在伺服器上啟用 websocket。</span><span class="sxs-lookup"><span data-stu-id="42a55-313">If you have verified that your server and clients meet the requirements for WebSocket (listed in the [Supported Platforms](../getting-started/supported-platforms.md) document), you will need to enable WebSocket on your server.</span></span> <span data-ttu-id="42a55-314">您可以在[這裡](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)找到執行此動作的指示。</span><span class="sxs-lookup"><span data-stu-id="42a55-314">Instructions for doing this can be found [here](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

### <a name="connection-is-undefined"></a><span data-ttu-id="42a55-315">$. connection 未定義</span><span class="sxs-lookup"><span data-stu-id="42a55-315">$.connection is undefined</span></span>

<span data-ttu-id="42a55-316">此錯誤表示網頁上的腳本未正確載入，或中樞 proxy 無法連線或存取不正確。</span><span class="sxs-lookup"><span data-stu-id="42a55-316">This error indicates that either the scripts on a page are not being loaded properly, or the hub proxy is not reachable or is being accessed incorrectly.</span></span> <span data-ttu-id="42a55-317">確認頁面上的腳本參考對應至專案中載入的腳本，而且當伺服器正在執行時，可以在瀏覽器中存取該/signalr/hubs。</span><span class="sxs-lookup"><span data-stu-id="42a55-317">Verify that the script references on your page correspond to the scripts loaded in your project, and that /signalr/hubs can be accessed in a browser when the server is running.</span></span>

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a><span data-ttu-id="42a55-318">找不到編譯動態運算式所需的一或多個類型</span><span class="sxs-lookup"><span data-stu-id="42a55-318">One or more types required to compile a dynamic expression cannot be found</span></span>

<span data-ttu-id="42a55-319">此錯誤表示遺失 `Microsoft.CSharp` 程式庫。</span><span class="sxs-lookup"><span data-stu-id="42a55-319">This error indicates that the `Microsoft.CSharp` library is missing.</span></span> <span data-ttu-id="42a55-320">將它加入 [**元件-&gt;Framework** ] 索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="42a55-320">Add it in the **Assemblies-&gt;Framework** tab.</span></span>

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a><span data-ttu-id="42a55-321">無法從用戶端存取呼叫者狀態。 Visual Basic 或在強型別中樞的呼叫者;「從類型 ' 工作轉換成類型 ' 字串 ' 無效」錯誤</span><span class="sxs-lookup"><span data-stu-id="42a55-321">Caller state cannot be accessed from Clients.Caller in Visual Basic or in a strongly typed hub; "Conversion from type 'Task(Of Object)' to type 'String' is not valid" error</span></span>

<span data-ttu-id="42a55-322">若要存取 Visual Basic 或強型別中樞內的呼叫端狀態，請使用 `Clients.CallerState` 屬性（在 SignalR 2.1 中引進），而不是 `Clients.Caller`。</span><span class="sxs-lookup"><span data-stu-id="42a55-322">To access caller state in Visual Basic or in a strongly typed hub, use the `Clients.CallerState` property (introduced in SignalR 2.1) instead of `Clients.Caller`.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="42a55-323">Visual Studio 問題</span><span class="sxs-lookup"><span data-stu-id="42a55-323">Visual Studio issues</span></span>

<span data-ttu-id="42a55-324">本節說明 Visual Studio 中遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="42a55-324">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="42a55-325">[指令檔] 節點不會出現在方案總管</span><span class="sxs-lookup"><span data-stu-id="42a55-325">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="42a55-326">我們的一些教學課程會在進行調試時，將您導向方案總管中的 [指令檔] 節點。</span><span class="sxs-lookup"><span data-stu-id="42a55-326">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="42a55-327">這個節點是由 JavaScript 偵錯工具所產生，而且只會在在 Internet Explorer 中進行瀏覽器用戶端的偵測時出現;如果使用 Chrome 或 Firefox，節點將不會出現。</span><span class="sxs-lookup"><span data-stu-id="42a55-327">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="42a55-328">如果另一個用戶端偵錯工具正在執行（例如 Silverlight 偵錯工具），JavaScript 偵錯工具也不會執行。</span><span class="sxs-lookup"><span data-stu-id="42a55-328">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="42a55-329">SignalR 無法在 Visual Studio 2008 或更早版本上運作</span><span class="sxs-lookup"><span data-stu-id="42a55-329">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="42a55-330">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="42a55-330">This behavior is by design.</span></span> <span data-ttu-id="42a55-331">SignalR 需要 .NET Framework 4 或更新版本;這需要在 Visual Studio 2010 或更新版本中開發 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42a55-331">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span> <span data-ttu-id="42a55-332">SignalR 的伺服器元件需要 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="42a55-332">The server component of SignalR requires .NET Framework 4.5.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="42a55-333">IIS 問題</span><span class="sxs-lookup"><span data-stu-id="42a55-333">IIS issues</span></span>

<span data-ttu-id="42a55-334">本節包含 Internet Information Services 的問題。</span><span class="sxs-lookup"><span data-stu-id="42a55-334">This section contains issues with Internet Information Services.</span></span>

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a><span data-ttu-id="42a55-335">SignalR 適用于 Visual Studio 的開發伺服器，但不能在 IIS 中運作</span><span class="sxs-lookup"><span data-stu-id="42a55-335">SignalR works on Visual Studio development server, but not in IIS</span></span>

<span data-ttu-id="42a55-336">IIS 7.0 和7.5 支援 SignalR，但必須新增無副檔名 Url 的支援。</span><span class="sxs-lookup"><span data-stu-id="42a55-336">SignalR is supported on IIS 7.0 and 7.5, but support for extensionless URLs must be added.</span></span> <span data-ttu-id="42a55-337">若要新增無副檔名 Url 的支援，請參閱[https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span><span class="sxs-lookup"><span data-stu-id="42a55-337">To add support for extensionless URLs, see [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span></span>

<span data-ttu-id="42a55-338">SignalR 需要在伺服器上安裝 ASP.NET （預設不會在 IIS 上安裝 ASP.NET）。</span><span class="sxs-lookup"><span data-stu-id="42a55-338">SignalR requires ASP.NET to be installed on the server (ASP.NET is not installed on IIS by default).</span></span> <span data-ttu-id="42a55-339">若要安裝 ASP.NET，請參閱[ASP.NET 下載](https://www.asp.net/downloads)。</span><span class="sxs-lookup"><span data-stu-id="42a55-339">To install ASP.NET, see [ASP.NET Downloads](https://www.asp.net/downloads).</span></span>

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a><span data-ttu-id="42a55-340">Microsoft Azure 問題</span><span class="sxs-lookup"><span data-stu-id="42a55-340">Microsoft Azure issues</span></span>

<span data-ttu-id="42a55-341">本節包含 Microsoft Azure 的問題。</span><span class="sxs-lookup"><span data-stu-id="42a55-341">This section contains issues with Microsoft Azure.</span></span>

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a><span data-ttu-id="42a55-342">在 Azure 背景工作角色中裝載 SignalR 時的 FileLoadException</span><span class="sxs-lookup"><span data-stu-id="42a55-342">FileLoadException when hosting SignalR in an Azure Worker Role</span></span>

<span data-ttu-id="42a55-343">在 Azure 背景工作角色中裝載 SignalR 可能會導致例外狀況：「無法載入檔案或元件 ' Owin，Version = 2.0.0.0」。</span><span class="sxs-lookup"><span data-stu-id="42a55-343">Hosting SignalR in an Azure Worker Role might result in the exception "Could not load file or assembly 'Microsoft.Owin, Version=2.0.0.0".</span></span> <span data-ttu-id="42a55-344">這是 NuGet 的已知問題;不會在 Azure 背景工作角色專案中自動新增系結重新導向。</span><span class="sxs-lookup"><span data-stu-id="42a55-344">This is a known issue with NuGet; Binding redirects are not added automatically in Azure Worker Role projects.</span></span> <span data-ttu-id="42a55-345">若要修正這個問題，您可以手動新增系結重新導向。</span><span class="sxs-lookup"><span data-stu-id="42a55-345">To fix this, you can add the binding redirects manually.</span></span> <span data-ttu-id="42a55-346">將下列幾行新增至背景工作角色專案的 `app.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="42a55-346">Add the following lines to the `app.config` file for your Worker Role project.</span></span>

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="42a55-347">修改主題名稱之後，不會透過 Azure 後擋板接收訊息</span><span class="sxs-lookup"><span data-stu-id="42a55-347">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="42a55-348">Azure 背板所使用的主題會在內部維護;它們不適合用戶設定。</span><span class="sxs-lookup"><span data-stu-id="42a55-348">The topics used by the Azure backplane are maintained internally; they are not intended to be user-configurable.</span></span>
