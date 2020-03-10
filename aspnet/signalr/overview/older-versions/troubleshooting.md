---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR 疑難排解（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本文說明開發 SignalR 應用程式的常見問題。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579601"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="4e214-103">SignalR 疑難排解 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="4e214-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="4e214-104">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="4e214-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4e214-105">本檔說明 SignalR 的常見疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="4e214-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="4e214-106">本檔包含下列各節。</span><span class="sxs-lookup"><span data-stu-id="4e214-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="4e214-107">在用戶端與伺服器之間呼叫方法無訊息失敗</span><span class="sxs-lookup"><span data-stu-id="4e214-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="4e214-108">其他連接問題</span><span class="sxs-lookup"><span data-stu-id="4e214-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="4e214-109">編譯和伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="4e214-110">Visual Studio 問題</span><span class="sxs-lookup"><span data-stu-id="4e214-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="4e214-111">Internet Information Services 問題</span><span class="sxs-lookup"><span data-stu-id="4e214-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="4e214-112">Azure 問題</span><span class="sxs-lookup"><span data-stu-id="4e214-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="4e214-113">在用戶端與伺服器之間呼叫方法無訊息失敗</span><span class="sxs-lookup"><span data-stu-id="4e214-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="4e214-114">本節描述用戶端和伺服器之間方法呼叫失敗的可能原因，而不會有有意義的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4e214-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="4e214-115">在 SignalR 應用程式中，伺服器不會有用戶端所執行之方法的相關資訊;當伺服器叫用用戶端方法時，方法名稱和參數資料會傳送至用戶端，而且只有在該方法是以伺服器指定的格式存在時，才會執行它。</span><span class="sxs-lookup"><span data-stu-id="4e214-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="4e214-116">如果在用戶端上找不到相符的方法，就不會發生任何事，也不會在伺服器上引發錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4e214-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="4e214-117">若要進一步調查不會呼叫的用戶端方法，您可以在呼叫中樞上的啟動方法之前開啟記錄功能，以查看來自伺服器的呼叫。</span><span class="sxs-lookup"><span data-stu-id="4e214-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="4e214-118">若要在 JavaScript 應用程式中啟用記錄，請參閱[如何啟用用戶端記錄（JavaScript 用戶端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="4e214-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="4e214-119">若要在 .NET 用戶端應用程式中啟用記錄，請參閱[如何啟用用戶端記錄（.Net 用戶端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="4e214-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="4e214-120">拼錯的方法、不正確的方法簽章或不正確的中樞名稱</span><span class="sxs-lookup"><span data-stu-id="4e214-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="4e214-121">如果所呼叫方法的名稱或簽章不完全符合用戶端上的適當方法，則呼叫將會失敗。</span><span class="sxs-lookup"><span data-stu-id="4e214-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="4e214-122">確認伺服器所呼叫的方法名稱符合用戶端上的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="4e214-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="4e214-123">此外，SignalR 會使用 camel 大小寫方法建立中樞 proxy，如同在 JavaScript 中適用，因此會在用戶端 proxy 中呼叫在伺服器上 `SendMessage` 的方法 `sendMessage`。</span><span class="sxs-lookup"><span data-stu-id="4e214-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="4e214-124">如果您在伺服器端程式碼中使用 `HubName` 屬性，請確認所使用的名稱符合用來在用戶端上建立中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e214-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="4e214-125">如果您未使用 `HubName` 屬性，請確認 JavaScript 用戶端中的中樞名稱為 camel 大小寫，例如 chatHub，而不是 ChatHub。</span><span class="sxs-lookup"><span data-stu-id="4e214-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="4e214-126">用戶端上重複的方法名稱</span><span class="sxs-lookup"><span data-stu-id="4e214-126">Duplicate method name on client</span></span>

<span data-ttu-id="4e214-127">請確認您的用戶端上沒有重複的方法，只有大小寫不同。</span><span class="sxs-lookup"><span data-stu-id="4e214-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="4e214-128">如果您的用戶端應用程式有一個稱為 `sendMessage`的方法，請確認也沒有稱為 `SendMessage` 的方法。</span><span class="sxs-lookup"><span data-stu-id="4e214-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="4e214-129">用戶端上缺少 JSON 剖析器</span><span class="sxs-lookup"><span data-stu-id="4e214-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="4e214-130">SignalR 需要有 JSON 剖析器，才能序列化伺服器和用戶端之間的呼叫。</span><span class="sxs-lookup"><span data-stu-id="4e214-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="4e214-131">如果您的用戶端沒有內建的 JSON 剖析器（例如 Internet Explorer 7），您必須在應用程式中包含一個。</span><span class="sxs-lookup"><span data-stu-id="4e214-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="4e214-132">您可以在[這裡](http://nuget.org/packages/json2)下載 JSON 剖析器。</span><span class="sxs-lookup"><span data-stu-id="4e214-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="4e214-133">混合中樞和 PersistentConnection 語法</span><span class="sxs-lookup"><span data-stu-id="4e214-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="4e214-134">SignalR 使用兩種通訊模型：中樞和 PersistentConnections。</span><span class="sxs-lookup"><span data-stu-id="4e214-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="4e214-135">在用戶端程式代碼中呼叫這兩種通訊模型的語法不同。</span><span class="sxs-lookup"><span data-stu-id="4e214-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="4e214-136">如果您已在伺服器程式碼中新增中樞，請確認您的所有用戶端程式代碼都使用適當的中樞語法。</span><span class="sxs-lookup"><span data-stu-id="4e214-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="4e214-137">**在 JavaScript 用戶端中建立 PersistentConnection 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="4e214-138">**在 JAVAscript 用戶端中建立中樞 Proxy 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="4e214-139">**C#將路由對應至 PersistentConnection 的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="4e214-140">**C#將路由對應至中樞的伺服器程式碼，如果您有多個應用程式，則為多個中樞**</span><span class="sxs-lookup"><span data-stu-id="4e214-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="4e214-141">在新增訂閱之前啟動連線</span><span class="sxs-lookup"><span data-stu-id="4e214-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="4e214-142">如果在可以從伺服器呼叫的方法加入至 proxy 之前，中樞的連線已啟動，則不會收到訊息。</span><span class="sxs-lookup"><span data-stu-id="4e214-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="4e214-143">下列 JavaScript 程式碼不會正確啟動中樞：</span><span class="sxs-lookup"><span data-stu-id="4e214-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="4e214-144">**不正確的 JavaScript 用戶端程式代碼將不允許接收中樞訊息**</span><span class="sxs-lookup"><span data-stu-id="4e214-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="4e214-145">請改為在呼叫 Start 之前新增方法訂閱：</span><span class="sxs-lookup"><span data-stu-id="4e214-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="4e214-146">**將訂用帳戶正確新增至中樞的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="4e214-147">中樞 proxy 上缺少方法名稱</span><span class="sxs-lookup"><span data-stu-id="4e214-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="4e214-148">確認伺服器上定義的方法已在用戶端上訂閱。</span><span class="sxs-lookup"><span data-stu-id="4e214-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="4e214-149">即使伺服器定義方法，仍然必須將它加入至用戶端 proxy。</span><span class="sxs-lookup"><span data-stu-id="4e214-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="4e214-150">方法可以透過下列方式新增至用戶端 proxy （請注意，方法會新增至中樞的 `client` 成員，而不是直接加入中樞）：</span><span class="sxs-lookup"><span data-stu-id="4e214-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="4e214-151">**將方法新增至中樞 proxy 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="4e214-152">中樞或中樞方法未宣告為公用</span><span class="sxs-lookup"><span data-stu-id="4e214-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="4e214-153">若要在用戶端上顯示，中樞的執行和方法必須宣告為 `public`。</span><span class="sxs-lookup"><span data-stu-id="4e214-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="4e214-154">從不同的應用程式存取中樞</span><span class="sxs-lookup"><span data-stu-id="4e214-154">Accessing hub from a different application</span></span>

<span data-ttu-id="4e214-155">SignalR Hub 只能透過執行 SignalR 用戶端的應用程式來存取。</span><span class="sxs-lookup"><span data-stu-id="4e214-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="4e214-156">SignalR 無法與其他通訊庫（例如 SOAP 或 WCF web 服務）相交互操作。如果您的目標平臺沒有可用的 SignalR 用戶端，您就無法直接存取伺服器的端點。</span><span class="sxs-lookup"><span data-stu-id="4e214-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="4e214-157">手動序列化資料</span><span class="sxs-lookup"><span data-stu-id="4e214-157">Manually serializing data</span></span>

<span data-ttu-id="4e214-158">SignalR 會自動使用 JSON 來序列化您的方法參數，而不需要自行執行此動作。</span><span class="sxs-lookup"><span data-stu-id="4e214-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="4e214-159">遠端中樞方法未在 OnDisconnected 函式的用戶端上執行</span><span class="sxs-lookup"><span data-stu-id="4e214-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="4e214-160">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="4e214-160">This behavior is by design.</span></span> <span data-ttu-id="4e214-161">呼叫 `OnDisconnected` 時，中樞已經進入 `Disconnected` 狀態，這不允許呼叫進一步的中樞方法。</span><span class="sxs-lookup"><span data-stu-id="4e214-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="4e214-162">**C#在 OnDisconnected 事件中正確執行程式碼的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="4e214-163">已達到連接限制</span><span class="sxs-lookup"><span data-stu-id="4e214-163">Connection limit reached</span></span>

<span data-ttu-id="4e214-164">在 Windows 7 之類的用戶端作業系統上使用完整版的 IIS 時，會強加10個連線限制。</span><span class="sxs-lookup"><span data-stu-id="4e214-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="4e214-165">使用用戶端 OS 時，請改用 IIS Express 以避免此限制。</span><span class="sxs-lookup"><span data-stu-id="4e214-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="4e214-166">未正確設定跨網域連線</span><span class="sxs-lookup"><span data-stu-id="4e214-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="4e214-167">如果跨網域連線（SignalR URL 與主控頁面不在相同網域中的連線）未正確設定，則連接可能會失敗，且不會出現錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4e214-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="4e214-168">如需如何啟用跨網域通訊的相關資訊，請參閱[如何建立跨網域](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)連線。</span><span class="sxs-lookup"><span data-stu-id="4e214-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="4e214-169">使用 NTLM （Active Directory）的連接在 .NET 用戶端中無法運作</span><span class="sxs-lookup"><span data-stu-id="4e214-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="4e214-170">如果連接未正確設定，在 .NET 用戶端應用程式中使用網域安全性的連接可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="4e214-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="4e214-171">若要在網域環境中使用 SignalR，請設定必要的連接屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4e214-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="4e214-172">**C#執行連接認證的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="4e214-173">其他連接問題</span><span class="sxs-lookup"><span data-stu-id="4e214-173">Other connection issues</span></span>

<span data-ttu-id="4e214-174">本節說明連線期間所發生之特定徵兆或錯誤訊息的原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e214-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="4e214-175">「必須在可以傳送資料之前呼叫啟動」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="4e214-176">如果在啟動連接之前，程式碼參考 SignalR 物件，通常會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="4e214-177">在連接完成之後，必須新增處理常式的裝設，以及將呼叫在伺服器上定義之方法的 like。</span><span class="sxs-lookup"><span data-stu-id="4e214-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="4e214-178">請注意，`Start` 的呼叫是非同步，因此呼叫之後的程式碼可能會在完成之前執行。</span><span class="sxs-lookup"><span data-stu-id="4e214-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="4e214-179">在連接完全啟動之後加入處理常式的最佳方式，是將它們放入回呼函式，並以參數的形式傳遞給 start 方法：</span><span class="sxs-lookup"><span data-stu-id="4e214-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="4e214-180">**可正確加入參考 SignalR 物件之事件處理常式的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="4e214-181">如果在仍在參考 SignalR 物件的情況下，連接停止，也會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="4e214-182">「已永久移動301」或「已暫時移動302」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="4e214-183">如果專案包含名為 SignalR 的資料夾，這會干擾自動建立的 proxy，可能會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="4e214-184">若要避免這個錯誤，請不要在應用程式中使用名為 `SignalR` 的資料夾，或關閉自動產生 proxy。</span><span class="sxs-lookup"><span data-stu-id="4e214-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="4e214-185">如需更多詳細資料，請參閱[產生的 Proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="4e214-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="4e214-186">.NET 或 Silverlight 用戶端發生「403禁止」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="4e214-187">跨網域的環境中，如果未正確啟用跨網域通訊，則可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="4e214-188">如需如何啟用跨網域通訊的相關資訊，請參閱[如何建立跨網域](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)連線。</span><span class="sxs-lookup"><span data-stu-id="4e214-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="4e214-189">若要在 Silverlight 用戶端中建立跨網域連接，請參閱[silverlight 用戶端的跨網域](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)連線。</span><span class="sxs-lookup"><span data-stu-id="4e214-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="4e214-190">「找不到404」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-190">"404 Not Found" error</span></span>

<span data-ttu-id="4e214-191">發生此問題的原因有好幾個。</span><span class="sxs-lookup"><span data-stu-id="4e214-191">There are several causes for this issue.</span></span> <span data-ttu-id="4e214-192">確認下列所有事項：</span><span class="sxs-lookup"><span data-stu-id="4e214-192">Verify all of the following:</span></span>

- <span data-ttu-id="4e214-193">**中樞 proxy 位址參考的格式不正確：** 如果所產生之中樞 proxy 位址的參考格式不正確，通常會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="4e214-194">確認已正確地對中樞位址進行參考。</span><span class="sxs-lookup"><span data-stu-id="4e214-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="4e214-195">如需詳細資訊，請參閱[如何參考動態產生的 proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 。</span><span class="sxs-lookup"><span data-stu-id="4e214-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="4e214-196">新增**路由至應用程式，再新增中樞路由：** 如果您的應用程式使用其他路由，請確認新增的第一個路由是 `MapHubs`的呼叫。</span><span class="sxs-lookup"><span data-stu-id="4e214-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="4e214-197">「500內部伺服器錯誤」</span><span class="sxs-lookup"><span data-stu-id="4e214-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="4e214-198">這是一個非常一般的錯誤，可能會有各種不同的原因。</span><span class="sxs-lookup"><span data-stu-id="4e214-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="4e214-199">錯誤的詳細資料應該會出現在伺服器的事件記錄檔中，或透過偵測伺服器來找到。</span><span class="sxs-lookup"><span data-stu-id="4e214-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="4e214-200">藉由開啟伺服器上的詳細錯誤，可取得更詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="4e214-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="4e214-201">如需詳細資訊，請參閱[如何處理中樞類別中的錯誤](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="4e214-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="4e214-202">「TypeError： &lt;hubType&gt; 未定義」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="4e214-203">如果未正確呼叫 `MapHubs`，將會產生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="4e214-204">如需詳細資訊，請參閱[如何註冊 SignalR 路由和設定 SignalR 選項](../guide-to-the-api/hubs-api-guide-server.md#route)。</span><span class="sxs-lookup"><span data-stu-id="4e214-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="4e214-205">JsonSerializationException 已由使用者程式碼未處理</span><span class="sxs-lookup"><span data-stu-id="4e214-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="4e214-206">確認您傳送至方法的參數不包含非可序列化的類型（例如檔案控制代碼或資料庫連接）。</span><span class="sxs-lookup"><span data-stu-id="4e214-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="4e214-207">如果您需要在不想要傳送至用戶端的伺服器端物件上使用成員（基於安全性或序列化的原因），請使用 `JSONIgnore` 屬性。</span><span class="sxs-lookup"><span data-stu-id="4e214-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="4e214-208">「通訊協定錯誤：未知的傳輸」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="4e214-209">如果用戶端不支援 SignalR 所使用的傳輸，則可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="4e214-210">如需可與 SignalR 搭配使用之瀏覽器的相關資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="4e214-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="4e214-211">「JavaScript 中樞 proxy 產生已停用。」</span><span class="sxs-lookup"><span data-stu-id="4e214-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="4e214-212">如果設定了 `DisableJavaScriptProxies`，同時包含 `signalr/hubs`上動態產生之 proxy 的參考，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="4e214-213">如需手動建立 proxy 的詳細資訊，請參閱[產生的 proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="4e214-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="4e214-214">「連線識別碼的格式不正確」或「使用者識別在使用中的 SignalR 連接期間無法變更」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="4e214-215">如果正在使用驗證，而且在連線停止之前，用戶端已登出，可能會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="4e214-216">解決方法是在登出用戶端之前，先停止 SignalR 連接。</span><span class="sxs-lookup"><span data-stu-id="4e214-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="4e214-217">「未攔截的錯誤： SignalR：找不到 jQuery。</span><span class="sxs-lookup"><span data-stu-id="4e214-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="4e214-218">請確定已在 SignalR .js 檔案之前參考 jQuery」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="4e214-219">SignalR JavaScript 用戶端需要 jQuery 才能執行。</span><span class="sxs-lookup"><span data-stu-id="4e214-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="4e214-220">請確認您對 jQuery 的參考是否正確、使用的路徑是否有效，以及 jQuery 的參考是否在 SignalR 的參考之前。</span><span class="sxs-lookup"><span data-stu-id="4e214-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="4e214-221">「未攔截的 TypeError：無法讀取屬性 '&lt;屬性&gt;' 未定義」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="4e214-222">此錯誤的結果是未正確參考 jQuery 或中樞 proxy。</span><span class="sxs-lookup"><span data-stu-id="4e214-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="4e214-223">請確認您對 jQuery 和中樞 proxy 的參考是否正確、使用的路徑是否有效，以及 jQuery 的參考是否在中樞 proxy 的參考之前。</span><span class="sxs-lookup"><span data-stu-id="4e214-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="4e214-224">中樞 proxy 的預設參考看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="4e214-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="4e214-225">**正確參考中樞 proxy 的 HTML 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="4e214-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="4e214-226">「RuntimeBinderException 由使用者程式碼未處理」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="4e214-227">使用不正確的 `Hub.On` 多載時，可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="4e214-228">如果方法有傳回值，則傳回型別必須指定為泛型型別參數：</span><span class="sxs-lookup"><span data-stu-id="4e214-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="4e214-229">**在用戶端上定義的方法（不含產生的 proxy）**</span><span class="sxs-lookup"><span data-stu-id="4e214-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="4e214-230">連接識別碼不一致，或頁面載入之間的連接中斷</span><span class="sxs-lookup"><span data-stu-id="4e214-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="4e214-231">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="4e214-231">This behavior is by design.</span></span> <span data-ttu-id="4e214-232">由於中樞物件裝載于 page 物件中，因此當頁面重新整理時，中樞會遭到終結。</span><span class="sxs-lookup"><span data-stu-id="4e214-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="4e214-233">多頁應用程式必須維護使用者與連接識別碼之間的關聯，以便在頁面載入之間保持一致。</span><span class="sxs-lookup"><span data-stu-id="4e214-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="4e214-234">連接識別碼可以儲存在伺服器上的 `ConcurrentDictionary` 物件或資料庫中。</span><span class="sxs-lookup"><span data-stu-id="4e214-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="4e214-235">「值不能為 null」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-235">"Value cannot be null" error</span></span>

<span data-ttu-id="4e214-236">目前不支援具有選擇性參數的伺服器端方法;如果省略了選擇性參數，方法將會失敗。</span><span class="sxs-lookup"><span data-stu-id="4e214-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="4e214-237">如需詳細資訊，請參閱[選擇性參數](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="4e214-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="4e214-238">「Firefox 無法在 Firebug 時建立與伺服器的連接，&lt;位址&gt;」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="4e214-239">如果 WebSocket 傳輸的協商失敗，而改用另一個傳輸，則會在 Firebug 中看到此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4e214-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="4e214-240">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="4e214-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="4e214-241">.NET 用戶端應用程式中的「根據驗證程式，遠端憑證無效」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="4e214-242">如果您的伺服器需要自訂用戶端憑證，您可以在提出要求之前，將 x509certificate 新增至連接。</span><span class="sxs-lookup"><span data-stu-id="4e214-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="4e214-243">使用 `Connection.AddClientCertificate`將憑證新增至連接。</span><span class="sxs-lookup"><span data-stu-id="4e214-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="4e214-244">驗證超時之後中斷連接</span><span class="sxs-lookup"><span data-stu-id="4e214-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="4e214-245">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="4e214-245">This behavior is by design.</span></span> <span data-ttu-id="4e214-246">當連接啟用時，無法修改驗證認證;若要重新整理認證，必須停止並重新啟動連接。</span><span class="sxs-lookup"><span data-stu-id="4e214-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="4e214-247">使用 jQuery Mobile 時，會呼叫 OnConnected 兩次</span><span class="sxs-lookup"><span data-stu-id="4e214-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="4e214-248">jQuery Mobile 的 `initializePage` 函式會強制重新執行每個頁面中的腳本，因此會建立第二個連接。</span><span class="sxs-lookup"><span data-stu-id="4e214-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="4e214-249">此問題的解決方案包括：</span><span class="sxs-lookup"><span data-stu-id="4e214-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="4e214-250">在您的 JavaScript 檔案之前包含 jQuery Mobile 的參考。</span><span class="sxs-lookup"><span data-stu-id="4e214-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="4e214-251">藉由設定 `$.mobile.autoInitializePage = false`來停用 `initializePage` 函數。</span><span class="sxs-lookup"><span data-stu-id="4e214-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="4e214-252">等候頁面完成初始化，再開始連接。</span><span class="sxs-lookup"><span data-stu-id="4e214-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="4e214-253">使用伺服器傳送事件的 Silverlight 應用程式中的訊息延遲</span><span class="sxs-lookup"><span data-stu-id="4e214-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="4e214-254">在 Silverlight 上使用伺服器傳送事件時，會延遲訊息。</span><span class="sxs-lookup"><span data-stu-id="4e214-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="4e214-255">若要改為強制使用長輪詢，請在啟動連線時使用下列內容：</span><span class="sxs-lookup"><span data-stu-id="4e214-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="4e214-256">「拒絕許可權」使用永久框架通訊協定</span><span class="sxs-lookup"><span data-stu-id="4e214-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="4e214-257">這是已知的問題，如[這裡](https://github.com/SignalR/SignalR/issues/1963)所述。</span><span class="sxs-lookup"><span data-stu-id="4e214-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="4e214-258">您可以使用最新的 JQuery 程式庫看到此徵兆;因應措施是將您的應用程式降級至 JQuery 1.8.2。</span><span class="sxs-lookup"><span data-stu-id="4e214-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="4e214-259">編譯和伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="4e214-260">下一節包含編譯器和伺服器端執行時間錯誤的可能解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e214-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="4e214-261">中樞實例的參考為 null</span><span class="sxs-lookup"><span data-stu-id="4e214-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="4e214-262">由於會針對每個連接建立中樞實例，因此您無法自行在程式碼中建立中樞的實例。</span><span class="sxs-lookup"><span data-stu-id="4e214-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="4e214-263">若要從中樞本身外部呼叫中樞上的方法，請參閱[如何從中樞類別外部呼叫用戶端方法和管理群組](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，以瞭解如何取得中樞內容的參考。</span><span class="sxs-lookup"><span data-stu-id="4e214-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="4e214-264">HTTPCoNtext。會話為 null</span><span class="sxs-lookup"><span data-stu-id="4e214-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="4e214-265">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="4e214-265">This behavior is by design.</span></span> <span data-ttu-id="4e214-266">SignalR 不支援 ASP.NET 會話狀態，因為啟用會話狀態會中斷雙工訊息。</span><span class="sxs-lookup"><span data-stu-id="4e214-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="4e214-267">沒有適合的覆寫方法</span><span class="sxs-lookup"><span data-stu-id="4e214-267">No suitable method to override</span></span>

<span data-ttu-id="4e214-268">如果您使用舊版檔或 blog 中的程式碼，可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="4e214-269">請確認您未參考已變更或已淘汰之方法的名稱（例如 `OnConnectedAsync`）。</span><span class="sxs-lookup"><span data-stu-id="4e214-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="4e214-270">HostCoNtextExtensions. WebSocketServerUrl 為 null</span><span class="sxs-lookup"><span data-stu-id="4e214-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="4e214-271">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="4e214-271">This behavior is by design.</span></span> <span data-ttu-id="4e214-272">這個成員已被取代，不應使用。</span><span class="sxs-lookup"><span data-stu-id="4e214-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="4e214-273">「路由集合中已有名為 ' signalr ' 的路由」錯誤</span><span class="sxs-lookup"><span data-stu-id="4e214-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="4e214-274">如果您的應用程式呼叫了兩次 `MapHubs`，就會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4e214-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="4e214-275">某些範例應用程式會直接呼叫全域應用程式檔中的 `MapHubs`;其他則會在包裝函式類別中進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="4e214-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="4e214-276">請確定您的應用程式不會同時執行這兩項操作。</span><span class="sxs-lookup"><span data-stu-id="4e214-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="4e214-277">Visual Studio 問題</span><span class="sxs-lookup"><span data-stu-id="4e214-277">Visual Studio issues</span></span>

<span data-ttu-id="4e214-278">本節說明 Visual Studio 中遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="4e214-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="4e214-279">[指令檔] 節點不會出現在方案總管</span><span class="sxs-lookup"><span data-stu-id="4e214-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="4e214-280">我們的一些教學課程會在進行調試時，將您導向方案總管中的 [指令檔] 節點。</span><span class="sxs-lookup"><span data-stu-id="4e214-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="4e214-281">這個節點是由 JavaScript 偵錯工具所產生，而且只會在在 Internet Explorer 中進行瀏覽器用戶端的偵測時出現;如果使用 Chrome 或 Firefox，節點將不會出現。</span><span class="sxs-lookup"><span data-stu-id="4e214-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="4e214-282">如果另一個用戶端偵錯工具正在執行（例如 Silverlight 偵錯工具），JavaScript 偵錯工具也不會執行。</span><span class="sxs-lookup"><span data-stu-id="4e214-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="4e214-283">SignalR 無法在 Visual Studio 2008 或更早版本上運作</span><span class="sxs-lookup"><span data-stu-id="4e214-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="4e214-284">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="4e214-284">This behavior is by design.</span></span> <span data-ttu-id="4e214-285">SignalR 需要 .NET Framework 4 或更新版本;這需要在 Visual Studio 2010 或更新版本中開發 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e214-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="4e214-286">IIS 問題</span><span class="sxs-lookup"><span data-stu-id="4e214-286">IIS issues</span></span>

<span data-ttu-id="4e214-287">本節包含 Internet Information Services 的問題。</span><span class="sxs-lookup"><span data-stu-id="4e214-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="4e214-288">MapHubs 呼叫後網站損毀</span><span class="sxs-lookup"><span data-stu-id="4e214-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="4e214-289">此問題已在最新版本的 SignalR 中修正。</span><span class="sxs-lookup"><span data-stu-id="4e214-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="4e214-290">使用 NuGet 更新安裝，以確認您使用的是最新發行版本的 SignalR。</span><span class="sxs-lookup"><span data-stu-id="4e214-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="4e214-291">Azure 問題</span><span class="sxs-lookup"><span data-stu-id="4e214-291">Azure issues</span></span>

<span data-ttu-id="4e214-292">本節包含 Microsoft Azure 的問題。</span><span class="sxs-lookup"><span data-stu-id="4e214-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="4e214-293">修改主題名稱之後，不會透過 Azure 後擋板接收訊息</span><span class="sxs-lookup"><span data-stu-id="4e214-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="4e214-294">Azure 背板所使用的主題不適合用來進行使用者可設定。</span><span class="sxs-lookup"><span data-stu-id="4e214-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
