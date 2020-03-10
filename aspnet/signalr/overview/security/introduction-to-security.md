---
uid: signalr/overview/security/introduction-to-security
title: SignalR 安全性簡介 |Microsoft Docs
author: bradygaster
description: 說明開發 SignalR 應用程式時，您必須考慮的安全性問題。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558573"
---
# <a name="introduction-to-signalr-security"></a><span data-ttu-id="05860-103">SignalR 安全性簡介</span><span class="sxs-lookup"><span data-stu-id="05860-103">Introduction to SignalR Security</span></span>

<span data-ttu-id="05860-104">由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="05860-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="05860-105">本文說明開發 SignalR 應用程式時必須考慮的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="05860-105">This article describes the security issues you must consider when developing a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="05860-106">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="05860-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="05860-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="05860-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="05860-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="05860-108">.NET 4.5</span></span>
> - <span data-ttu-id="05860-109">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="05860-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="05860-110">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="05860-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="05860-111">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="05860-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="05860-112">問題與意見</span><span class="sxs-lookup"><span data-stu-id="05860-112">Questions and comments</span></span>
>
> <span data-ttu-id="05860-113">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="05860-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="05860-114">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="05860-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="05860-115">概觀</span><span class="sxs-lookup"><span data-stu-id="05860-115">Overview</span></span>

<span data-ttu-id="05860-116">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="05860-116">This document contains the following sections:</span></span>

- [<span data-ttu-id="05860-117">SignalR 安全性概念</span><span class="sxs-lookup"><span data-stu-id="05860-117">SignalR Security Concepts</span></span>](#concepts)

    - [<span data-ttu-id="05860-118">驗證與授權</span><span class="sxs-lookup"><span data-stu-id="05860-118">Authentication and authorization</span></span>](#authentication)
    - [<span data-ttu-id="05860-119">連接權杖</span><span class="sxs-lookup"><span data-stu-id="05860-119">Connection token</span></span>](#connectiontoken)
    - [<span data-ttu-id="05860-120">重新連接時重新加入群組</span><span class="sxs-lookup"><span data-stu-id="05860-120">Rejoining groups when reconnecting</span></span>](#rejoingroup)
- [<span data-ttu-id="05860-121">SignalR 如何防止跨網站偽造要求</span><span class="sxs-lookup"><span data-stu-id="05860-121">How SignalR prevents Cross-Site Request Forgery</span></span>](#csrf)
- [<span data-ttu-id="05860-122">SignalR 安全性建議</span><span class="sxs-lookup"><span data-stu-id="05860-122">SignalR Security Recommendations</span></span>](#recommendations)

    - [<span data-ttu-id="05860-123">安全通訊端層（SSL）通訊協定</span><span class="sxs-lookup"><span data-stu-id="05860-123">Secure Socket Layers (SSL) protocol</span></span>](#ssl)
    - [<span data-ttu-id="05860-124">請勿使用群組做為安全性機制</span><span class="sxs-lookup"><span data-stu-id="05860-124">Do not use groups as a security mechanism</span></span>](#groupsecurity)
    - [<span data-ttu-id="05860-125">安全地處理來自用戶端的輸入</span><span class="sxs-lookup"><span data-stu-id="05860-125">Safely handling input from clients</span></span>](#input)
    - [<span data-ttu-id="05860-126">使用作用中連線協調使用者狀態的變更</span><span class="sxs-lookup"><span data-stu-id="05860-126">Reconciling a change in user status with an active connection</span></span>](#reconcile)
    - [<span data-ttu-id="05860-127">自動產生的 JavaScript proxy 檔案</span><span class="sxs-lookup"><span data-stu-id="05860-127">Automatically generated JavaScript proxy files</span></span>](#autogen)
    - [<span data-ttu-id="05860-128">例外狀況</span><span class="sxs-lookup"><span data-stu-id="05860-128">Exceptions</span></span>](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a><span data-ttu-id="05860-129">SignalR 安全性概念</span><span class="sxs-lookup"><span data-stu-id="05860-129">SignalR Security Concepts</span></span>

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a><span data-ttu-id="05860-130">驗證與授權</span><span class="sxs-lookup"><span data-stu-id="05860-130">Authentication and authorization</span></span>

<span data-ttu-id="05860-131">SignalR 不會提供驗證使用者的任何功能。</span><span class="sxs-lookup"><span data-stu-id="05860-131">SignalR does not provide any features for authenticating users.</span></span> <span data-ttu-id="05860-132">相反地，您會將 SignalR 功能整合到應用程式現有的驗證結構中。</span><span class="sxs-lookup"><span data-stu-id="05860-132">Instead, you integrate the SignalR features into the existing authentication structure for an application.</span></span> <span data-ttu-id="05860-133">您在應用程式中以平常一般的方式驗證使用者，並在您的 SignalR 程式碼中使用驗證的結果。</span><span class="sxs-lookup"><span data-stu-id="05860-133">You authenticate users as you would normally in your application, and work with the results of the authentication in your SignalR code.</span></span> <span data-ttu-id="05860-134">例如，您可以使用 ASP.NET 表單驗證來驗證您的使用者，然後在您的中樞內，強制執行哪些使用者或角色獲授權可以呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="05860-134">For example, you might authenticate your users with ASP.NET forms authentication, and then in your hub, enforce which users or roles are authorized to call a method.</span></span> <span data-ttu-id="05860-135">在您的中樞中，您也可以將驗證資訊（例如使用者名稱或使用者是否屬於角色）傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="05860-135">In your hub, you can also pass authentication information, such as user name or whether a user belongs to a role, to the client.</span></span>

<span data-ttu-id="05860-136">SignalR 提供[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性，以指定哪些使用者可以存取中樞或方法。</span><span class="sxs-lookup"><span data-stu-id="05860-136">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users have access to a hub or method.</span></span> <span data-ttu-id="05860-137">您會將授權屬性套用至中樞中的中樞或特定方法。</span><span class="sxs-lookup"><span data-stu-id="05860-137">You apply the Authorize attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="05860-138">如果沒有授權屬性，中樞上的所有公用方法都可供連線至中樞的用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="05860-138">Without the Authorize attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span> <span data-ttu-id="05860-139">如需中樞的詳細資訊，請參閱[SignalR 中樞的驗證和授權](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="05860-139">For more information about hubs, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span>

<span data-ttu-id="05860-140">您會將 `Authorize` 屬性套用至中樞，但不會持續連接。</span><span class="sxs-lookup"><span data-stu-id="05860-140">You apply the `Authorize` attribute to hubs, but not persistent connections.</span></span> <span data-ttu-id="05860-141">若要在使用 `PersistentConnection` 時強制執行授權規則，您必須覆寫 `AuthorizeRequest` 方法。</span><span class="sxs-lookup"><span data-stu-id="05860-141">To enforce authorization rules when using a `PersistentConnection` you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="05860-142">如需持續連線的詳細資訊，請參閱[SignalR 持續連線的驗證和授權](persistent-connection-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="05860-142">For more information about persistent connections, see [Authentication and Authorization for SignalR Persistent Connections](persistent-connection-authorization.md).</span></span>

<a id="connectiontoken"></a>

### <a name="connection-token"></a><span data-ttu-id="05860-143">連接權杖</span><span class="sxs-lookup"><span data-stu-id="05860-143">Connection token</span></span>

<span data-ttu-id="05860-144">SignalR 藉由驗證寄件者的身分識別，來降低執行惡意命令的風險。</span><span class="sxs-lookup"><span data-stu-id="05860-144">SignalR mitigates the risk of executing malicious commands by validating the identity of the sender.</span></span> <span data-ttu-id="05860-145">針對每個要求，用戶端和伺服器會傳遞一個連接權杖，其中包含已驗證使用者的連線識別碼和使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="05860-145">For each request, the client and server pass a connection token which contains the connection id and username for authenticated users.</span></span> <span data-ttu-id="05860-146">連接識別碼可唯一識別每個連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="05860-146">The connection id uniquely identifies each connected client.</span></span> <span data-ttu-id="05860-147">當建立新的連接時，伺服器會隨機產生連線識別碼，並在連線期間保存該識別碼。</span><span class="sxs-lookup"><span data-stu-id="05860-147">The server randomly generates the connection id when a new connection is created, and persists that id for the duration of the connection.</span></span> <span data-ttu-id="05860-148">Web 應用程式的驗證機制會提供使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="05860-148">The authentication mechanism for the web application provides the username.</span></span> <span data-ttu-id="05860-149">SignalR 會使用加密和數位簽章來保護連接權杖。</span><span class="sxs-lookup"><span data-stu-id="05860-149">SignalR uses encryption and a digital signature to protect the connection token.</span></span>

![](introduction-to-security/_static/image2.png)

<span data-ttu-id="05860-150">針對每個要求，伺服器會驗證權杖的內容，以確保要求來自指定的使用者。</span><span class="sxs-lookup"><span data-stu-id="05860-150">For each request, the server validates the contents of the token to ensure that the request is coming from the specified user.</span></span> <span data-ttu-id="05860-151">使用者名稱必須對應到連接識別碼。藉由驗證連線識別碼和使用者名稱，SignalR 可防止惡意使用者輕鬆地模擬另一位使用者。</span><span class="sxs-lookup"><span data-stu-id="05860-151">The username must correspond to the connection id. By validating both the connection id and the username, SignalR prevents a malicious user from easily impersonating another user.</span></span> <span data-ttu-id="05860-152">如果伺服器無法驗證連線 token，要求就會失敗。</span><span class="sxs-lookup"><span data-stu-id="05860-152">If the server cannot validate the connection token, the request fails.</span></span>

![](introduction-to-security/_static/image4.png)

<span data-ttu-id="05860-153">因為連線識別碼是驗證程式的一部分，所以您不應該向其他使用者顯示某個使用者的連線識別碼，或將此值儲存在用戶端上，例如在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="05860-153">Because the connection id is part of the verification process, you should not reveal one user's connection id to other users or store the value on the client, such as in a cookie.</span></span>

#### <a name="connection-tokens-vs-other-token-types"></a><span data-ttu-id="05860-154">連接權杖與其他 token 類型的比較</span><span class="sxs-lookup"><span data-stu-id="05860-154">Connection tokens vs. other token types</span></span>

<span data-ttu-id="05860-155">連線權杖偶爾會受到安全性工具的旗標，因為它們看起來像是會話權杖或驗證權杖，這會在公開時帶來風險。</span><span class="sxs-lookup"><span data-stu-id="05860-155">Connection tokens are occasionally flagged by security tools because they appear to be session tokens or authentication tokens, which poses a risk if exposed.</span></span>

<span data-ttu-id="05860-156">SignalR 的連接權杖不是驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="05860-156">SignalR's connection token isn't an authentication token.</span></span> <span data-ttu-id="05860-157">這是用來確認提出此要求的使用者與建立連接的使用者相同。</span><span class="sxs-lookup"><span data-stu-id="05860-157">It is used to confirm that the user making this request is the same one that created the connection.</span></span> <span data-ttu-id="05860-158">連接標記是必要的，因為 ASP.NET SignalR 允許連接在伺服器之間移動。</span><span class="sxs-lookup"><span data-stu-id="05860-158">The connection token is necessary because ASP.NET SignalR allows connections to move between servers.</span></span> <span data-ttu-id="05860-159">權杖會將連線與特定使用者建立關聯，但不會判斷提出要求之使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="05860-159">The token associates the connection with a particular user but doesn't assert the identity of the user making the request.</span></span> <span data-ttu-id="05860-160">若要正確驗證 SignalR 要求，它必須有一些其他的權杖會判斷提示使用者的身分，例如 cookie 或持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="05860-160">For a SignalR request to be properly authenticated, it must have some other token that asserts the identity of the user, such as a cookie or bearer token.</span></span> <span data-ttu-id="05860-161">不過，連線權杖本身不會宣告該使用者所提出的要求，只有包含在權杖中的連接識別碼會與該使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="05860-161">However, the connection token itself makes no claim that the request was made by that user, only that the connection ID contained within the token is associated with that user.</span></span>

<span data-ttu-id="05860-162">由於連接權杖不提供自己的驗證宣告，因此不會被視為「會話」或「驗證」權杖。</span><span class="sxs-lookup"><span data-stu-id="05860-162">Since the connection token provides no authentication claim of its own, it isn't considered a "session" or "authentication" token.</span></span> <span data-ttu-id="05860-163">取得指定使用者的連接權杖，並在以不同使用者身分驗證的要求中重新執行（或未經驗證的要求）將會失敗，因為要求的使用者識別和儲存在權杖中的識別不會相符。</span><span class="sxs-lookup"><span data-stu-id="05860-163">Taking a given user's connection token and replaying it in a request authenticated as a different user (or an unauthenticated request) will fail, because the user identity of the request and the identity stored in the token won't match.</span></span>

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a><span data-ttu-id="05860-164">重新連接時重新加入群組</span><span class="sxs-lookup"><span data-stu-id="05860-164">Rejoining groups when reconnecting</span></span>

<span data-ttu-id="05860-165">根據預設，SignalR 應用程式會在中斷連線時，自動將使用者重新指派給適當的群組，例如在連接逾時之前中斷連接並重新建立連線。重新連線時，用戶端會傳遞包含連線識別碼和指派群組的群組 token。</span><span class="sxs-lookup"><span data-stu-id="05860-165">By default, the SignalR application will automatically re-assign a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. When reconnecting, the client passes a group token that includes the connection id and the assigned groups.</span></span> <span data-ttu-id="05860-166">群組權杖會經過數位簽署和加密。</span><span class="sxs-lookup"><span data-stu-id="05860-166">The group token is digitally signed and encrypted.</span></span> <span data-ttu-id="05860-167">用戶端會在重新連線後保留相同的連接識別碼;因此，從重新連線的用戶端傳遞的連接識別碼必須符合用戶端使用的先前連線識別碼。</span><span class="sxs-lookup"><span data-stu-id="05860-167">The client retains the same connection id after a reconnection; therefore, the connection id passed from the reconnected client must match the previous connection id used by the client.</span></span> <span data-ttu-id="05860-168">此驗證可防止惡意使用者在重新連線時，將要求傳遞至加入未經授權的群組。</span><span class="sxs-lookup"><span data-stu-id="05860-168">This verification prevents a malicious user from passing requests to join unauthorized groups when reconnecting.</span></span>

<span data-ttu-id="05860-169">不過，請務必注意，群組權杖不會過期。</span><span class="sxs-lookup"><span data-stu-id="05860-169">However, it's important to note, that the group token does not expire.</span></span> <span data-ttu-id="05860-170">如果使用者屬於過去的群組，但已從該群組中禁止，該使用者可能可以模擬包含禁止群組的群組 token。</span><span class="sxs-lookup"><span data-stu-id="05860-170">If a user belonged to a group in the past, but was banned from that group, that user may be able to mimic a group token that includes the prohibited group.</span></span> <span data-ttu-id="05860-171">如果您需要安全地管理哪些使用者屬於哪些群組，您需要將該資料儲存在伺服器上，例如在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="05860-171">If you need to securely manage which users belong to which groups, you need to store that data on the server, such as in a database.</span></span> <span data-ttu-id="05860-172">然後，將邏輯新增至您的應用程式，以在伺服器上驗證使用者是否屬於群組。</span><span class="sxs-lookup"><span data-stu-id="05860-172">Then, add logic to your application that verifies on the server whether a user belongs to a group.</span></span> <span data-ttu-id="05860-173">如需驗證群組成員資格的範例，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="05860-173">For an example of verifying group membership, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<span data-ttu-id="05860-174">只有在暫時中斷之後，連接重新連線時，才會套用自動重新加入群組。</span><span class="sxs-lookup"><span data-stu-id="05860-174">Automatically rejoining groups only applies when a connection is reconnected after a temporary disruption.</span></span> <span data-ttu-id="05860-175">如果使用者離開應用程式或應用程式重新開機來中斷連線，您的應用程式必須處理如何將該使用者新增至正確的群組。</span><span class="sxs-lookup"><span data-stu-id="05860-175">If a user disconnects by navigating away from the application or the application restarts, your application must handle how to add that user to the correct groups.</span></span> <span data-ttu-id="05860-176">如需詳細資訊，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="05860-176">For more information, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a><span data-ttu-id="05860-177">SignalR 如何防止跨網站偽造要求</span><span class="sxs-lookup"><span data-stu-id="05860-177">How SignalR prevents Cross-Site Request Forgery</span></span>

<span data-ttu-id="05860-178">跨網站偽造要求（CSRF）是一種攻擊，惡意網站會將要求傳送至使用者目前登入的弱點網站。</span><span class="sxs-lookup"><span data-stu-id="05860-178">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in.</span></span> <span data-ttu-id="05860-179">SignalR 會讓惡意網站非常不太可能建立 SignalR 應用程式的有效要求，而避免 CSRF。</span><span class="sxs-lookup"><span data-stu-id="05860-179">SignalR prevents CSRF by making it extremely unlikely for a malicious site to create a valid request for your SignalR application.</span></span>

### <a name="description-of-csrf-attack"></a><span data-ttu-id="05860-180">CSRF 攻擊的描述</span><span class="sxs-lookup"><span data-stu-id="05860-180">Description of CSRF attack</span></span>

<span data-ttu-id="05860-181">以下是 CSRF 攻擊的範例：</span><span class="sxs-lookup"><span data-stu-id="05860-181">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="05860-182">使用者使用表單驗證登入 www.example.com。</span><span class="sxs-lookup"><span data-stu-id="05860-182">A user logs into www.example.com, using forms authentication.</span></span>
2. <span data-ttu-id="05860-183">伺服器會驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="05860-183">The server authenticates the user.</span></span> <span data-ttu-id="05860-184">伺服器的回應包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="05860-184">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="05860-185">若未登出，使用者會造訪惡意網站。</span><span class="sxs-lookup"><span data-stu-id="05860-185">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="05860-186">這個惡意網站包含下列 HTML 表單：</span><span class="sxs-lookup"><span data-stu-id="05860-186">This malicious site contains the following HTML form:</span></span>

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   <span data-ttu-id="05860-187">請注意，表單動作會張貼到易受攻擊的網站，而不是惡意網站。</span><span class="sxs-lookup"><span data-stu-id="05860-187">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="05860-188">這是 CSRF 的「跨網站」部分。</span><span class="sxs-lookup"><span data-stu-id="05860-188">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="05860-189">使用者按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="05860-189">The user clicks the submit button.</span></span> <span data-ttu-id="05860-190">瀏覽器會在要求中包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="05860-190">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="05860-191">此要求會在 example.com 伺服器上以使用者的驗證內容執行，並可執行已驗證使用者允許執行的任何動作。</span><span class="sxs-lookup"><span data-stu-id="05860-191">The request runs on the example.com server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="05860-192">雖然此範例需要使用者按一下表單按鈕，但惡意的網頁也可以輕鬆地執行腳本，將 AJAX 要求傳送至您的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05860-192">Although this example requires the user to click the form button, the malicious page could just as easily run a script that sends an AJAX request to your SignalR application.</span></span> <span data-ttu-id="05860-193">此外，使用 SSL 並不會防止 CSRF 攻擊，因為惡意網站可以傳送「HTTPs://」要求。</span><span class="sxs-lookup"><span data-stu-id="05860-193">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="05860-194">一般來說，使用 cookie 進行驗證的網站可能會發生 CSRF 攻擊，因為瀏覽器會將所有相關的 cookie 傳送至目的地網站。</span><span class="sxs-lookup"><span data-stu-id="05860-194">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="05860-195">不過，CSRF 攻擊並不限於利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="05860-195">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="05860-196">例如，基本和摘要式驗證也很容易受到攻擊。</span><span class="sxs-lookup"><span data-stu-id="05860-196">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="05860-197">使用者使用基本或摘要式驗證登入之後，瀏覽器會自動傳送認證，直到會話結束為止。</span><span class="sxs-lookup"><span data-stu-id="05860-197">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

### <a name="csrf-mitigations-taken-by-signalr"></a><span data-ttu-id="05860-198">SignalR 所採用的 CSRF 緩和措施</span><span class="sxs-lookup"><span data-stu-id="05860-198">CSRF mitigations taken by SignalR</span></span>

<span data-ttu-id="05860-199">SignalR 會採取下列步驟，以防止惡意網站對您的應用程式建立有效的要求。</span><span class="sxs-lookup"><span data-stu-id="05860-199">SignalR takes the following steps to prevent a malicious site from creating valid requests to your application.</span></span> <span data-ttu-id="05860-200">根據預設，SignalR 會執行這些步驟，您不需要在程式碼中採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="05860-200">SignalR takes these steps by default, you do not need to take any action in your code.</span></span>

- <span data-ttu-id="05860-201">**停用跨網域要求**SignalR 會停用跨網域要求，以防止使用者從外部網域呼叫 SignalR 端點。</span><span class="sxs-lookup"><span data-stu-id="05860-201">**Disable cross domain requests** SignalR disables cross domain requests to prevent users from calling a SignalR endpoint from an external domain.</span></span> <span data-ttu-id="05860-202">SignalR 會將來自外部網域的任何要求視為無效，並封鎖要求。</span><span class="sxs-lookup"><span data-stu-id="05860-202">SignalR considers any request from an external domain to be invalid and blocks the request.</span></span> <span data-ttu-id="05860-203">我們建議您保留此預設行為;否則，惡意網站可以誘騙使用者傳送命令給您的網站。</span><span class="sxs-lookup"><span data-stu-id="05860-203">We recommend that you keep this default behavior; otherwise, a malicious site could trick users into sending commands to your site.</span></span> <span data-ttu-id="05860-204">如果您需要使用跨網域要求，請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="05860-204">If you need to use cross domain requests, see     [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .</span></span>
- <span data-ttu-id="05860-205">**在查詢字串中傳遞連接 token，而不是 cookie**SignalR 會將連接 token 傳遞為查詢字串值，而不是 cookie。</span><span class="sxs-lookup"><span data-stu-id="05860-205">**Pass connection token in query string, not cookie** SignalR passes the connection token as a query string value, instead of as a cookie.</span></span> <span data-ttu-id="05860-206">將連接權杖儲存在 cookie 中並不安全，因為當遇到惡意程式碼時，瀏覽器可能會不慎轉送連接 token。</span><span class="sxs-lookup"><span data-stu-id="05860-206">Storing the connection token in a cookie is unsafe because the browser can inadvertently forward the connection token when malicious code is encountered.</span></span> <span data-ttu-id="05860-207">此外，在查詢字串中傳遞連接 token，可防止連接 token 保存在目前的連接之外。</span><span class="sxs-lookup"><span data-stu-id="05860-207">Also, passing the connection token in the query string prevents the connection token from persisting beyond the current connection.</span></span> <span data-ttu-id="05860-208">因此，惡意使用者無法以另一個使用者的驗證認證來提出要求。</span><span class="sxs-lookup"><span data-stu-id="05860-208">Therefore, a malicious user cannot make a request under another user's authentication credentials.</span></span>
- <span data-ttu-id="05860-209">**驗證連接權杖**如連線[權杖](#connectiontoken)一節中所述，伺服器知道哪個連接識別碼與每個已驗證的使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="05860-209">**Verify connection token** As described in the     [Connection token](#connectiontoken) section, the server knows which connection id is associated with each authenticated user.</span></span> <span data-ttu-id="05860-210">伺服器不會處理來自不符合使用者名稱之連線識別碼的任何要求。</span><span class="sxs-lookup"><span data-stu-id="05860-210">The server does not process any request from a connection id that does not match the user name.</span></span> <span data-ttu-id="05860-211">惡意使用者不太可能猜到有效的要求，因為惡意使用者必須知道使用者名稱和目前隨機產生的連接識別碼。當連接結束時，該連接識別碼就會變成無效。</span><span class="sxs-lookup"><span data-stu-id="05860-211">It is unlikely a malicious user could guess a valid request because the malicious user would have to know the user name and the current randomly-generated connection id. That connection id becomes invalid as soon as the connection is ended.</span></span> <span data-ttu-id="05860-212">匿名使用者不應該有任何機密資訊的存取權。</span><span class="sxs-lookup"><span data-stu-id="05860-212">Anonymous users should not have access to any sensitive information.</span></span>

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a><span data-ttu-id="05860-213">SignalR 安全性建議</span><span class="sxs-lookup"><span data-stu-id="05860-213">SignalR Security Recommendations</span></span>

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a><span data-ttu-id="05860-214">安全通訊端層（SSL）通訊協定</span><span class="sxs-lookup"><span data-stu-id="05860-214">Secure Socket Layers (SSL) protocol</span></span>

<span data-ttu-id="05860-215">SSL 通訊協定會使用加密來保護用戶端與伺服器之間的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="05860-215">The SSL protocol uses encryption to secure the transport of data between a client and server.</span></span> <span data-ttu-id="05860-216">如果您的 SignalR 應用程式會在用戶端與伺服器之間傳輸機密資訊，請使用 SSL 進行傳輸。</span><span class="sxs-lookup"><span data-stu-id="05860-216">If your SignalR application transmits sensitive information between the client and server, use SSL for the transport.</span></span> <span data-ttu-id="05860-217">如需設定 SSL 的詳細資訊，請參閱[如何在 IIS 7 上設定 ssl](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。</span><span class="sxs-lookup"><span data-stu-id="05860-217">For more information about setting up SSL, see [How to set up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a><span data-ttu-id="05860-218">請勿使用群組做為安全性機制</span><span class="sxs-lookup"><span data-stu-id="05860-218">Do not use groups as a security mechanism</span></span>

<span data-ttu-id="05860-219">群組是一種方便收集相關使用者的方式，但不是限制存取機密資訊的安全機制。</span><span class="sxs-lookup"><span data-stu-id="05860-219">Groups are a convenient way of collecting related users, but they are not a secure mechanism for limiting access to sensitive information.</span></span> <span data-ttu-id="05860-220">當使用者可以在重新連線期間自動重新加入群組時，更是如此。</span><span class="sxs-lookup"><span data-stu-id="05860-220">This is especially true when users can automatically rejoin groups during a reconnect.</span></span> <span data-ttu-id="05860-221">相反地，請考慮將特殊許可權使用者新增至角色，並將中樞方法的存取限制為只有該角色的成員。</span><span class="sxs-lookup"><span data-stu-id="05860-221">Instead, consider adding privileged users to a role and limiting access to a hub method to only members of that role.</span></span> <span data-ttu-id="05860-222">如需根據角色限制存取的範例，請參閱[SignalR 中樞的驗證和授權](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="05860-222">For an example of restricting access based on a role, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span> <span data-ttu-id="05860-223">如需在重新連接時檢查使用者對群組存取權的範例，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="05860-223">For an example of checking user access to groups when reconnecting, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a><span data-ttu-id="05860-224">安全地處理來自用戶端的輸入</span><span class="sxs-lookup"><span data-stu-id="05860-224">Safely handling input from clients</span></span>

<span data-ttu-id="05860-225">若要確保惡意使用者不會傳送腳本給其他使用者，您必須針對要廣播至其他用戶端的用戶端，將所有輸入編碼。</span><span class="sxs-lookup"><span data-stu-id="05860-225">To ensure that a malicious user does not send script to other users, you must encode all input from clients that is intended for broadcast to other clients.</span></span> <span data-ttu-id="05860-226">您應該將接收用戶端上的訊息編碼，而不是伺服器，因為您的 SignalR 應用程式可能會有許多不同類型的用戶端。</span><span class="sxs-lookup"><span data-stu-id="05860-226">You should encode messages on the receiving clients rather than the server, because your SignalR application may have many different types of clients.</span></span> <span data-ttu-id="05860-227">因此，HTML 編碼適用于 web 用戶端，但不適用於其他類型的用戶端。</span><span class="sxs-lookup"><span data-stu-id="05860-227">Therefore, HTML-encoding works for a web client, but not for other types of clients.</span></span> <span data-ttu-id="05860-228">例如，用來顯示聊天訊息的 web 用戶端方法，會藉由呼叫 `html()` 函式，安全地處理使用者名稱和訊息。</span><span class="sxs-lookup"><span data-stu-id="05860-228">For example, a web client method to display a chat message would safely handle the user name and message by calling the `html()` function.</span></span>

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a><span data-ttu-id="05860-229">使用作用中連線協調使用者狀態的變更</span><span class="sxs-lookup"><span data-stu-id="05860-229">Reconciling a change in user status with an active connection</span></span>

<span data-ttu-id="05860-230">如果使用者的驗證狀態在作用中連接存在時變更，使用者將會收到錯誤訊息，指出「使用者識別在使用中的 SignalR 連線期間無法變更」。</span><span class="sxs-lookup"><span data-stu-id="05860-230">If a user's authentication status changes while an active connection exists, the user will receive an error that states, "The user identity cannot change during an active SignalR connection."</span></span> <span data-ttu-id="05860-231">在這種情況下，您的應用程式應該重新連接到伺服器，以確保連接識別碼和使用者名稱的協調。</span><span class="sxs-lookup"><span data-stu-id="05860-231">In that case, your application should re-connect to the server to make sure the connection id and username are coordinated.</span></span> <span data-ttu-id="05860-232">例如，如果您的應用程式允許使用者在使用中連接存在時登出，則連接的使用者名稱將不再符合下一個要求所傳入的名稱。</span><span class="sxs-lookup"><span data-stu-id="05860-232">For example, if your application allows the user to log out while an active connection exists, the username for the connection will no longer match the name that is passed in for the next request.</span></span> <span data-ttu-id="05860-233">您會想要在使用者登出之前停止連線，然後再重新開機。</span><span class="sxs-lookup"><span data-stu-id="05860-233">You will want to stop the connection before the user logs out, and then restart it.</span></span>

<span data-ttu-id="05860-234">不過，請務必注意，大部分的應用程式都不需要手動停止和啟動連接。</span><span class="sxs-lookup"><span data-stu-id="05860-234">However, it is important to note that most applications will not need to manually stop and start the connection.</span></span> <span data-ttu-id="05860-235">如果您的應用程式在登出之後將使用者重新導向至另一個頁面（例如 Web form 應用程式或 MVC 應用程式中的預設行為），或在登出後重新整理目前的頁面，則使用中的連接會自動中斷連線，而且不會需要任何額外的動作。</span><span class="sxs-lookup"><span data-stu-id="05860-235">If your application redirects users to a separate page after logging out, such as the default behavior in a Web Forms application or MVC application, or refreshes the current page after logging out, the active connection is automatically disconnected and does not require any additional action.</span></span>

<span data-ttu-id="05860-236">下列範例顯示如何在使用者狀態變更時停止和啟動連接。</span><span class="sxs-lookup"><span data-stu-id="05860-236">The following example shows how to stop and start a connection when the user status has changed.</span></span>

[!code-html[Main](introduction-to-security/samples/sample3.html)]

<span data-ttu-id="05860-237">或者，如果您的網站使用具有表單驗證的滑動到期日，則使用者的驗證狀態可能會變更，而且沒有任何活動可以讓驗證 cookie 有效。</span><span class="sxs-lookup"><span data-stu-id="05860-237">Or, the user's authentication status may change if your site uses sliding expiration with Forms Authentication, and there is no activity to keep the authentication cookie valid.</span></span> <span data-ttu-id="05860-238">在此情況下，使用者將會登出，而使用者名稱將不再符合連接權杖中的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="05860-238">In that case, the user will be logged out and the user name will no longer match the user name in the connection token.</span></span> <span data-ttu-id="05860-239">若要修正這個問題，您可以新增一些定期要求 web 伺服器上資源的腳本，讓驗證 cookie 保持有效。</span><span class="sxs-lookup"><span data-stu-id="05860-239">You can fix this problem by adding some script that periodically requests a resource on the web server to keep the authentication cookie valid.</span></span> <span data-ttu-id="05860-240">下列範例顯示如何每隔30分鐘要求資源。</span><span class="sxs-lookup"><span data-stu-id="05860-240">The following example shows how to request a resource every 30 minutes.</span></span>

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a><span data-ttu-id="05860-241">自動產生的 JavaScript proxy 檔案</span><span class="sxs-lookup"><span data-stu-id="05860-241">Automatically generated JavaScript proxy files</span></span>

<span data-ttu-id="05860-242">如果您不想要在每個使用者的 JavaScript proxy 檔案中包含所有的中樞和方法，您可以停用自動產生檔案。</span><span class="sxs-lookup"><span data-stu-id="05860-242">If you do not want to include all of the hubs and methods in the JavaScript proxy file for each user, you can disable the automatic generation of the file.</span></span> <span data-ttu-id="05860-243">如果您有多個中樞和方法，但不想讓每位使用者都知道所有方法，您可以選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="05860-243">You might choose this option if you have multiple hubs and methods, but do not want every user to be aware of all of the methods.</span></span> <span data-ttu-id="05860-244">您可以藉由將**EnableJavaScriptProxies**設定為**false**來停用自動產生。</span><span class="sxs-lookup"><span data-stu-id="05860-244">You disable automatic generation by setting **EnableJavaScriptProxies** to **false**.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

<span data-ttu-id="05860-245">如需 JavaScript proxy 檔案的詳細資訊，請參閱[產生的 proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="05860-245">For more information about the JavaScript proxy files, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span> <a id="exceptions"></a>

### <a name="exceptions"></a><span data-ttu-id="05860-246">例外狀況</span><span class="sxs-lookup"><span data-stu-id="05860-246">Exceptions</span></span>

<span data-ttu-id="05860-247">您應該避免將例外狀況物件傳遞給用戶端，因為物件可能會向用戶端公開機密資訊。</span><span class="sxs-lookup"><span data-stu-id="05860-247">You should avoid passing exception objects to clients because the objects may expose sensitive information to the clients.</span></span> <span data-ttu-id="05860-248">相反地，請在顯示相關錯誤訊息的用戶端上呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="05860-248">Instead, call a method on the client that displays the relevant error message.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
