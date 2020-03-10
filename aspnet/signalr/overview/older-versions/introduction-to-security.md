---
uid: signalr/overview/older-versions/introduction-to-security
title: SignalR 安全性簡介（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 說明開發 SignalR 應用程式時，您必須考慮的安全性問題。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 715a4059-d307-4631-abbb-c789c95d6eb4
msc.legacyurl: /signalr/overview/older-versions/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 34172c0a2a15a7ab0d782704d5831ce236f5c989
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536726"
---
# <a name="introduction-to-signalr-security-signalr-1x"></a><span data-ttu-id="bfc7f-103">SignalR 安全性簡介 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="bfc7f-103">Introduction to SignalR Security (SignalR 1.x)</span></span>

<span data-ttu-id="bfc7f-104">由一[Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bfc7f-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="bfc7f-105">本文說明開發 SignalR 應用程式時必須考慮的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-105">This article describes the security issues you must consider when developing a SignalR application.</span></span>

## <a name="overview"></a><span data-ttu-id="bfc7f-106">概觀</span><span class="sxs-lookup"><span data-stu-id="bfc7f-106">Overview</span></span>

<span data-ttu-id="bfc7f-107">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="bfc7f-107">This document contains the following sections:</span></span>

- [<span data-ttu-id="bfc7f-108">SignalR 安全性概念</span><span class="sxs-lookup"><span data-stu-id="bfc7f-108">SignalR Security Concepts</span></span>](#concepts)

    - [<span data-ttu-id="bfc7f-109">驗證與授權</span><span class="sxs-lookup"><span data-stu-id="bfc7f-109">Authentication and authorization</span></span>](#authentication)
    - [<span data-ttu-id="bfc7f-110">連接權杖</span><span class="sxs-lookup"><span data-stu-id="bfc7f-110">Connection token</span></span>](#connectiontoken)
    - [<span data-ttu-id="bfc7f-111">重新連接時重新加入群組</span><span class="sxs-lookup"><span data-stu-id="bfc7f-111">Rejoining groups when reconnecting</span></span>](#rejoingroup)
- [<span data-ttu-id="bfc7f-112">SignalR 如何防止跨網站偽造要求</span><span class="sxs-lookup"><span data-stu-id="bfc7f-112">How SignalR prevents Cross-Site Request Forgery</span></span>](#csrf)
- [<span data-ttu-id="bfc7f-113">SignalR 安全性建議</span><span class="sxs-lookup"><span data-stu-id="bfc7f-113">SignalR Security Recommendations</span></span>](#recommendations)

    - [<span data-ttu-id="bfc7f-114">安全通訊端層（SSL）通訊協定</span><span class="sxs-lookup"><span data-stu-id="bfc7f-114">Secure Socket Layers (SSL) protocol</span></span>](#ssl)
    - [<span data-ttu-id="bfc7f-115">請勿使用群組做為安全性機制</span><span class="sxs-lookup"><span data-stu-id="bfc7f-115">Do not use groups as a security mechanism</span></span>](#groupsecurity)
    - [<span data-ttu-id="bfc7f-116">安全地處理來自用戶端的輸入</span><span class="sxs-lookup"><span data-stu-id="bfc7f-116">Safely handling input from clients</span></span>](#input)
    - [<span data-ttu-id="bfc7f-117">使用作用中連線協調使用者狀態的變更</span><span class="sxs-lookup"><span data-stu-id="bfc7f-117">Reconciling a change in user status with an active connection</span></span>](#reconcile)
    - [<span data-ttu-id="bfc7f-118">自動產生的 JavaScript proxy 檔案</span><span class="sxs-lookup"><span data-stu-id="bfc7f-118">Automatically generated JavaScript proxy files</span></span>](#autogen)
    - [<span data-ttu-id="bfc7f-119">例外狀況</span><span class="sxs-lookup"><span data-stu-id="bfc7f-119">Exceptions</span></span>](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a><span data-ttu-id="bfc7f-120">SignalR 安全性概念</span><span class="sxs-lookup"><span data-stu-id="bfc7f-120">SignalR Security Concepts</span></span>

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a><span data-ttu-id="bfc7f-121">驗證與授權</span><span class="sxs-lookup"><span data-stu-id="bfc7f-121">Authentication and authorization</span></span>

<span data-ttu-id="bfc7f-122">SignalR 是設計來整合到應用程式的現有驗證結構中。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-122">SignalR is designed to be integrated into the existing authentication structure for an application.</span></span> <span data-ttu-id="bfc7f-123">它不會提供驗證使用者的任何功能。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-123">It does not provide any features for authenticating users.</span></span> <span data-ttu-id="bfc7f-124">相反地，您會在應用程式中以平常的方式驗證使用者，然後在您的 SignalR 程式碼中使用驗證的結果。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-124">Instead, you authenticate users as you would normally in your application, and then work with the results of the authentication in your SignalR code.</span></span> <span data-ttu-id="bfc7f-125">例如，您可以使用 ASP.NET 表單驗證來驗證您的使用者，然後在您的中樞內，強制執行哪些使用者或角色獲授權可以呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-125">For example, you might authenticate your users with ASP.NET forms authentication, and then in your hub, enforce which users or roles are authorized to call a method.</span></span> <span data-ttu-id="bfc7f-126">在您的中樞中，您也可以將驗證資訊（例如使用者名稱或使用者是否屬於角色）傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-126">In your hub, you can also pass authentication information, such as user name or whether a user belongs to a role, to the client.</span></span>

<span data-ttu-id="bfc7f-127">SignalR 提供[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性，以指定哪些使用者可以存取中樞或方法。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-127">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users have access to a hub or method.</span></span> <span data-ttu-id="bfc7f-128">您會將授權屬性套用至中樞中的中樞或特定方法。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-128">You apply the Authorize attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="bfc7f-129">如果沒有授權屬性，中樞上的所有公用方法都可供連線至中樞的用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-129">Without the Authorize attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span> <span data-ttu-id="bfc7f-130">如需中樞的詳細資訊，請參閱[SignalR 中樞的驗證和授權](../security/hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-130">For more information about hubs, see [Authentication and Authorization for SignalR Hubs](../security/hub-authorization.md).</span></span>

<span data-ttu-id="bfc7f-131">`Authorize` 屬性僅適用于中樞。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-131">The `Authorize` attribute is used only with hubs.</span></span> <span data-ttu-id="bfc7f-132">若要在使用 `PersistentConnection` 時強制執行授權規則，您必須覆寫 `AuthorizeRequest` 方法。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-132">To enforce authorization rules when using a `PersistentConnection` you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="bfc7f-133">如需持續連線的詳細資訊，請參閱[SignalR 持續連線的驗證和授權](../security/persistent-connection-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-133">For more information about persistent connections, see [Authentication and Authorization for SignalR Persistent Connections](../security/persistent-connection-authorization.md).</span></span>

<a id="connectiontoken"></a>

### <a name="connection-token"></a><span data-ttu-id="bfc7f-134">連接權杖</span><span class="sxs-lookup"><span data-stu-id="bfc7f-134">Connection token</span></span>

<span data-ttu-id="bfc7f-135">SignalR 藉由驗證寄件者的身分識別，來降低執行惡意命令的風險。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-135">SignalR mitigates the risk of executing malicious commands by validating the identity of the sender.</span></span> <span data-ttu-id="bfc7f-136">用戶端和伺服器會在每個要求之間傳遞連接權杖，其中包含已驗證使用者的連接識別碼和使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-136">A connection token, containing the connection id and username for authenticated users, is passed between the client and server for each request.</span></span> <span data-ttu-id="bfc7f-137">連接識別碼是唯一的識別碼，會在建立新的連接時由伺服器隨機產生，並在連接期間保存。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-137">The connection id is a unique identifier that is randomly generated by the server when a new connection is created, and is persisted for the duration of the connection.</span></span> <span data-ttu-id="bfc7f-138">使用者名稱是由 web 應用程式的驗證機制所提供。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-138">The username is provided by the authentication mechanism for the web application.</span></span> <span data-ttu-id="bfc7f-139">連接權杖會受到加密和數位簽章的保護。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-139">The connection token is protected with encryption and a digital signature.</span></span>

![](introduction-to-security/_static/image2.png)

<span data-ttu-id="bfc7f-140">針對每個要求，伺服器會驗證權杖的內容，以確保要求來自指定的使用者。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-140">For each request, the server validates the contents of the token to ensure that the request is coming from the specified user.</span></span> <span data-ttu-id="bfc7f-141">使用者名稱必須對應到連接識別碼。藉由驗證連線識別碼和使用者名稱，SignalR 可防止惡意使用者輕鬆地模擬另一位使用者。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-141">The username must correspond to the connection id. By validating both the connection id and the username, SignalR prevents a malicious user from easily impersonating another user.</span></span> <span data-ttu-id="bfc7f-142">如果伺服器無法驗證連線 token，要求就會失敗。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-142">If the server cannot validate the connection token, the request fails.</span></span>

![](introduction-to-security/_static/image4.png)

<span data-ttu-id="bfc7f-143">因為連線識別碼是驗證程式的一部分，所以您不應該向其他使用者顯示某個使用者的連線識別碼，或將此值儲存在用戶端上，例如在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-143">Because the connection id is part of the verification process, you should not reveal one user's connection id to other users or store the value on the client, such as in a cookie.</span></span>

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a><span data-ttu-id="bfc7f-144">重新連接時重新加入群組</span><span class="sxs-lookup"><span data-stu-id="bfc7f-144">Rejoining groups when reconnecting</span></span>

<span data-ttu-id="bfc7f-145">根據預設，SignalR 應用程式會在中斷連線時，自動將使用者重新指派給適當的群組，例如在連接逾時之前中斷連接並重新建立連線。重新連線時，用戶端會傳遞包含連線識別碼和指派群組的群組 token。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-145">By default, the SignalR application will automatically re-assign a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. When reconnecting, the client passes a group token that includes the connection id and the assigned groups.</span></span> <span data-ttu-id="bfc7f-146">群組權杖會經過數位簽署和加密。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-146">The group token is digitally signed and encrypted.</span></span> <span data-ttu-id="bfc7f-147">用戶端會在重新連線後保留相同的連接識別碼;因此，從重新連線的用戶端傳遞的連接識別碼必須符合用戶端使用的先前連線識別碼。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-147">The client retains the same connection id after a reconnection; therefore, the connection id passed from the reconnected client must match the previous connection id used by the client.</span></span> <span data-ttu-id="bfc7f-148">此驗證可防止惡意使用者在重新連線時，將要求傳遞至加入未經授權的群組。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-148">This verification prevents a malicious user from passing requests to join unauthorized groups when reconnecting.</span></span>

<span data-ttu-id="bfc7f-149">不過，請務必注意，群組權杖不會過期。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-149">However, it is important to note, that the group token does not expire.</span></span> <span data-ttu-id="bfc7f-150">如果使用者屬於過去的群組，但已從該群組中禁止，該使用者可能可以模擬包含禁止群組的群組 token。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-150">If a user belonged to a group in the past, but was banned from that group, that user may be able to mimic a group token that includes the prohibited group.</span></span> <span data-ttu-id="bfc7f-151">如果您需要安全地管理哪些使用者屬於哪些群組，您需要將該資料儲存在伺服器上，例如在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-151">If you need to securely manage which users belong to which groups, you need to store that data on the server, such as in a database.</span></span> <span data-ttu-id="bfc7f-152">然後，將邏輯新增至您的應用程式，以在伺服器上驗證使用者是否屬於群組。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-152">Then, add logic to your application that verifies on the server whether a user belongs to a group.</span></span> <span data-ttu-id="bfc7f-153">如需驗證群組成員資格的範例，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-153">For an example of verifying group membership, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<span data-ttu-id="bfc7f-154">只有在暫時中斷之後，連接重新連線時，才會套用自動重新加入群組。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-154">Automatically rejoining groups only applies when a connection is reconnected after a temporary disruption.</span></span> <span data-ttu-id="bfc7f-155">如果使用者離開應用程式或應用程式重新開機來中斷連線，您的應用程式必須處理如何將該使用者新增至正確的群組。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-155">If a user disconnects by navigating away from the application or the application restarts, your application must handle how to add that user to the correct groups.</span></span> <span data-ttu-id="bfc7f-156">如需詳細資訊，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-156">For more information, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a><span data-ttu-id="bfc7f-157">SignalR 如何防止跨網站偽造要求</span><span class="sxs-lookup"><span data-stu-id="bfc7f-157">How SignalR prevents Cross-Site Request Forgery</span></span>

<span data-ttu-id="bfc7f-158">跨網站偽造要求（CSRF）是一種攻擊，惡意網站會將要求傳送至使用者目前登入的弱點網站。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-158">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in.</span></span> <span data-ttu-id="bfc7f-159">SignalR 會讓惡意網站非常不太可能建立 SignalR 應用程式的有效要求，而避免 CSRF。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-159">SignalR prevents CSRF by making it extremely unlikely for a malicious site to create a valid request for your SignalR application.</span></span>

### <a name="description-of-csrf-attack"></a><span data-ttu-id="bfc7f-160">CSRF 攻擊的描述</span><span class="sxs-lookup"><span data-stu-id="bfc7f-160">Description of CSRF attack</span></span>

<span data-ttu-id="bfc7f-161">以下是 CSRF 攻擊的範例：</span><span class="sxs-lookup"><span data-stu-id="bfc7f-161">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="bfc7f-162">使用者使用表單驗證登入 `www.example.com`。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-162">A user logs into `www.example.com`, using forms authentication.</span></span>
2. <span data-ttu-id="bfc7f-163">伺服器會驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-163">The server authenticates the user.</span></span> <span data-ttu-id="bfc7f-164">伺服器的回應包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-164">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="bfc7f-165">若未登出，使用者會造訪惡意網站。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-165">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="bfc7f-166">這個惡意網站包含下列 HTML 表單：</span><span class="sxs-lookup"><span data-stu-id="bfc7f-166">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   <span data-ttu-id="bfc7f-167">請注意，表單動作會張貼到易受攻擊的網站，而不是惡意網站。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-167">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="bfc7f-168">這是 CSRF 的「跨網站」部分。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-168">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="bfc7f-169">使用者按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-169">The user clicks the submit button.</span></span> <span data-ttu-id="bfc7f-170">瀏覽器會在要求中包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-170">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="bfc7f-171">此要求會在 example.com 伺服器上以使用者的驗證內容執行，並可執行已驗證使用者允許執行的任何動作。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-171">The request runs on the example.com server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="bfc7f-172">雖然此範例需要使用者按一下表單按鈕，但惡意的網頁也可以輕鬆地執行腳本，將 AJAX 要求傳送至您的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-172">Although this example requires the user to click the form button, the malicious page could just as easily run a script that sends an AJAX request to your SignalR application.</span></span> <span data-ttu-id="bfc7f-173">此外，使用 SSL 並不會防止 CSRF 攻擊，因為惡意網站可以傳送「HTTPs://」要求。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-173">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="bfc7f-174">一般來說，使用 cookie 進行驗證的網站可能會發生 CSRF 攻擊，因為瀏覽器會將所有相關的 cookie 傳送至目的地網站。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-174">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="bfc7f-175">不過，CSRF 攻擊並不限於利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-175">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="bfc7f-176">例如，基本和摘要式驗證也很容易受到攻擊。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-176">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="bfc7f-177">使用者使用基本或摘要式驗證登入之後，瀏覽器會自動傳送認證，直到會話結束為止。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-177">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

### <a name="csrf-mitigations-taken-by-signalr"></a><span data-ttu-id="bfc7f-178">SignalR 所採用的 CSRF 緩和措施</span><span class="sxs-lookup"><span data-stu-id="bfc7f-178">CSRF mitigations taken by SignalR</span></span>

<span data-ttu-id="bfc7f-179">SignalR 會採取下列步驟，以防止惡意網站對您的 SignalR 應用程式建立有效的要求。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-179">SignalR takes the following steps to prevent a malicious site from creating valid requests to your SignalR application.</span></span> <span data-ttu-id="bfc7f-180">預設會採取這些步驟，而且不需要在您的程式碼中執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-180">These steps are taken by default and do not require any action in your code.</span></span>

- <span data-ttu-id="bfc7f-181">**停用跨網域要求**</span><span class="sxs-lookup"><span data-stu-id="bfc7f-181">**Disable cross domain requests**</span></span>  
 <span data-ttu-id="bfc7f-182">根據預設，SignalR 應用程式中的跨網域要求會停用，以防止使用者從外部網域呼叫 SignalR 端點。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-182">By default, cross domain requests are disabled in a SignalR application to prevent users from calling a SignalR endpoint from an external domain.</span></span> <span data-ttu-id="bfc7f-183">來自外部網域的任何要求都會自動視為無效，而且會被封鎖。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-183">Any request that comes from an external domain is automatically considered invalid and is blocked.</span></span> <span data-ttu-id="bfc7f-184">建議您保留此預設行為;否則，惡意網站可以誘騙使用者傳送命令給您的網站。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-184">It is recommended that you keep this default behavior; otherwise, a malicious site could trick users into sending commands to your site.</span></span> <span data-ttu-id="bfc7f-185">如果您需要使用跨網域要求，請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-185">If you need to use cross domain requests, see     [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .</span></span>
- <span data-ttu-id="bfc7f-186">**在查詢字串中傳遞連接 token，而不是 cookie**</span><span class="sxs-lookup"><span data-stu-id="bfc7f-186">**Pass connection token in query string, not cookie**</span></span>  
 <span data-ttu-id="bfc7f-187">SignalR 會將連接 token 傳遞為查詢字串值，而不是 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-187">SignalR passes the connection token as a query string value, instead of as a cookie.</span></span> <span data-ttu-id="bfc7f-188">藉由不將連線權杖儲存為 cookie，瀏覽器在遇到惡意程式碼時，不會不慎轉送連接標記。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-188">By not storing the connection token as a cookie, the connection token is not inadvertently forwarded by the browser when malicious code is encountered.</span></span> <span data-ttu-id="bfc7f-189">此外，連接權杖不會保存在目前的連接之外。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-189">Also, the connection token is not persisted beyond the current connection.</span></span> <span data-ttu-id="bfc7f-190">因此，惡意使用者無法以另一個使用者的驗證認證來提出要求。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-190">Therefore, a malicious user cannot make a request under another user's authentication credentials.</span></span>
- <span data-ttu-id="bfc7f-191">**驗證連接權杖**</span><span class="sxs-lookup"><span data-stu-id="bfc7f-191">**Verify connection token**</span></span>  
 <span data-ttu-id="bfc7f-192">如連線[權杖](#connectiontoken)一節中所述，伺服器知道哪個連接識別碼與每個已驗證的使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-192">As described in the [Connection token](#connectiontoken) section, the server knows which connection id is associated with each authenticated user.</span></span> <span data-ttu-id="bfc7f-193">伺服器不會處理來自不符合使用者名稱之連線識別碼的任何要求。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-193">The server does not process any request from a connection id that does not match the user name.</span></span> <span data-ttu-id="bfc7f-194">惡意使用者不太可能猜到有效的要求，因為惡意使用者必須知道使用者名稱和目前隨機產生的連接識別碼。當連接結束時，該連接識別碼就會變成無效。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-194">It is unlikely a malicious user could guess a valid request because the malicious user would have to know the user name and the current randomly-generated connection id. That connection id becomes invalid as soon as the connection is ended.</span></span> <span data-ttu-id="bfc7f-195">匿名使用者不應該有任何機密資訊的存取權。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-195">Anonymous users should not have access to any sensitive information.</span></span>

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a><span data-ttu-id="bfc7f-196">SignalR 安全性建議</span><span class="sxs-lookup"><span data-stu-id="bfc7f-196">SignalR Security Recommendations</span></span>

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a><span data-ttu-id="bfc7f-197">安全通訊端層（SSL）通訊協定</span><span class="sxs-lookup"><span data-stu-id="bfc7f-197">Secure Socket Layers (SSL) protocol</span></span>

<span data-ttu-id="bfc7f-198">SSL 通訊協定會使用加密來保護用戶端與伺服器之間的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-198">The SSL protocol uses encryption to secure the transport of data between a client and server.</span></span> <span data-ttu-id="bfc7f-199">如果您的 SignalR 應用程式會在用戶端與伺服器之間傳輸機密資訊，請使用 SSL 進行傳輸。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-199">If your SignalR application transmits sensitive information between the client and server, use SSL for the transport.</span></span> <span data-ttu-id="bfc7f-200">如需設定 SSL 的詳細資訊，請參閱[如何在 IIS 7 上設定 ssl](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-200">For more information about setting up SSL, see [How to set up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a><span data-ttu-id="bfc7f-201">請勿使用群組做為安全性機制</span><span class="sxs-lookup"><span data-stu-id="bfc7f-201">Do not use groups as a security mechanism</span></span>

<span data-ttu-id="bfc7f-202">群組是一種方便收集相關使用者的方式，但不是限制存取機密資訊的安全機制。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-202">Groups are a convenient way of collecting related users, but they are not a secure mechanism for limiting access to sensitive information.</span></span> <span data-ttu-id="bfc7f-203">當使用者可以在重新連線期間自動重新加入群組時，更是如此。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-203">This is especially true when users can automatically rejoin groups during a reconnect.</span></span> <span data-ttu-id="bfc7f-204">相反地，請考慮將特殊許可權使用者新增至角色，並將中樞方法的存取限制為只有該角色的成員。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-204">Instead, consider adding privileged users to a role and limiting access to a hub method to only members of that role.</span></span> <span data-ttu-id="bfc7f-205">如需根據角色限制存取的範例，請參閱[SignalR 中樞的驗證和授權](../security/hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-205">For an example of restricting access based on a role, see [Authentication and Authorization for SignalR Hubs](../security/hub-authorization.md).</span></span> <span data-ttu-id="bfc7f-206">如需在重新連接時檢查使用者對群組存取權的範例，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-206">For an example of checking user access to groups when reconnecting, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a><span data-ttu-id="bfc7f-207">安全地處理來自用戶端的輸入</span><span class="sxs-lookup"><span data-stu-id="bfc7f-207">Safely handling input from clients</span></span>

<span data-ttu-id="bfc7f-208">所有要用於廣播至其他用戶端的用戶端輸入，都必須經過編碼，以確保惡意使用者不會傳送腳本給其他使用者。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-208">All input from clients that is intended for broadcast to other clients must be encoded to ensure that a malicious user does not send script to other users.</span></span> <span data-ttu-id="bfc7f-209">最好是在接收用戶端而非伺服器上編碼訊息，因為您的 SignalR 應用程式可能會有許多不同類型的用戶端。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-209">It is best to encode messages on the receiving clients rather than the server, because your SignalR application may have many different types of clients.</span></span> <span data-ttu-id="bfc7f-210">因此，HTML 編碼適用于 web 用戶端，但不適用於其他類型的用戶端。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-210">Therefore, HTML-encoding works for a web client, but not for other types of clients.</span></span> <span data-ttu-id="bfc7f-211">例如，用來顯示聊天訊息的 web 用戶端方法，會藉由呼叫 `html()` 函式，安全地處理使用者名稱和訊息。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-211">For example, a web client method to display a chat message would safely handle the user name and message by calling the `html()` function.</span></span>

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a><span data-ttu-id="bfc7f-212">使用作用中連線協調使用者狀態的變更</span><span class="sxs-lookup"><span data-stu-id="bfc7f-212">Reconciling a change in user status with an active connection</span></span>

<span data-ttu-id="bfc7f-213">如果使用者的驗證狀態在作用中連接存在時變更，使用者將會收到錯誤訊息，指出「使用者識別在使用中的 SignalR 連線期間無法變更」。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-213">If a user's authentication status changes while an active connection exists, the user will receive an error that states, "The user identity cannot change during an active SignalR connection."</span></span> <span data-ttu-id="bfc7f-214">在這種情況下，您的應用程式應該重新連接到伺服器，以確保連接識別碼和使用者名稱的協調。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-214">In that case, your application should re-connect to the server to make sure the connection id and username are coordinated.</span></span> <span data-ttu-id="bfc7f-215">例如，如果您的應用程式允許使用者在使用中連接存在時登出，則連接的使用者名稱將不再符合下一個要求所傳入的名稱。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-215">For example, if your application allows the user to log out while an active connection exists, the username for the connection will no longer match the name that is passed in for the next request.</span></span> <span data-ttu-id="bfc7f-216">您會想要在使用者登出之前停止連線，然後再重新開機。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-216">You will want to stop the connection before the user logs out, and then restart it.</span></span>

<span data-ttu-id="bfc7f-217">不過，請務必注意，大部分的應用程式都不需要手動停止和啟動連接。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-217">However, it is important to note that most applications will not need to manually stop and start the connection.</span></span> <span data-ttu-id="bfc7f-218">如果您的應用程式在登出之後將使用者重新導向至另一個頁面（例如 Web form 應用程式或 MVC 應用程式中的預設行為），或在登出後重新整理目前的頁面，則使用中的連接會自動中斷連線，而且不會需要任何額外的動作。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-218">If your application redirects users to a separate page after logging out, such as the default behavior in a Web Forms application or MVC application, or refreshes the current page after logging out, the active connection is automatically disconnected and does not require any additional action.</span></span>

<span data-ttu-id="bfc7f-219">下列範例顯示如何在使用者狀態變更時停止和啟動連接。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-219">The following example shows how to stop and start a connection when the user status has changed.</span></span>

[!code-html[Main](introduction-to-security/samples/sample3.html)]

<span data-ttu-id="bfc7f-220">或者，如果您的網站使用具有表單驗證的滑動到期日，則使用者的驗證狀態可能會變更，而且沒有任何活動可以讓驗證 cookie 有效。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-220">Or, the user's authentication status may change if your site uses sliding expiration with Forms Authentication, and there is no activity to keep the authentication cookie valid.</span></span> <span data-ttu-id="bfc7f-221">在此情況下，使用者將會登出，而使用者名稱將不再符合連接權杖中的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-221">In that case, the user will be logged out and the user name will no longer match the user name in the connection token.</span></span> <span data-ttu-id="bfc7f-222">若要修正這個問題，您可以新增一些定期要求 web 伺服器上資源的腳本，讓驗證 cookie 保持有效。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-222">You can fix this problem by adding some script that periodically requests a resource on the web server to keep the authentication cookie valid.</span></span> <span data-ttu-id="bfc7f-223">下列範例顯示如何每隔30分鐘要求資源。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-223">The following example shows how to request a resource every 30 minutes.</span></span>

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a><span data-ttu-id="bfc7f-224">自動產生的 JavaScript proxy 檔案</span><span class="sxs-lookup"><span data-stu-id="bfc7f-224">Automatically generated JavaScript proxy files</span></span>

<span data-ttu-id="bfc7f-225">如果您不想要在每個使用者的 JavaScript proxy 檔案中包含所有的中樞和方法，您可以停用自動產生檔案。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-225">If you do not want to include all of the hubs and methods in the JavaScript proxy file for each user, you can disable the automatic generation of the file.</span></span> <span data-ttu-id="bfc7f-226">如果您有多個中樞和方法，但不想讓每位使用者都知道所有方法，您可以選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-226">You might choose this option if you have multiple hubs and methods, but do not want every user to be aware of all of the methods.</span></span> <span data-ttu-id="bfc7f-227">您可以藉由將**EnableJavaScriptProxies**設定為**false**來停用自動產生。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-227">You disable automatic generation by setting **EnableJavaScriptProxies** to **false**.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

<span data-ttu-id="bfc7f-228">如需 JavaScript proxy 檔案的詳細資訊，請參閱[產生的 proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-228">For more information about the JavaScript proxy files, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span> <a id="exceptions"></a>

### <a name="exceptions"></a><span data-ttu-id="bfc7f-229">例外狀況</span><span class="sxs-lookup"><span data-stu-id="bfc7f-229">Exceptions</span></span>

<span data-ttu-id="bfc7f-230">您應該避免將例外狀況物件傳遞給用戶端，因為物件可能會向用戶端公開機密資訊。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-230">You should avoid passing exception objects to clients because the objects may expose sensitive information to the clients.</span></span> <span data-ttu-id="bfc7f-231">相反地，請在顯示相關錯誤訊息的用戶端上呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="bfc7f-231">Instead, call a method on the client that displays the relevant error message.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
