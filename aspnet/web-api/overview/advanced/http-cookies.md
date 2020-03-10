---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API 中的 HTTP Cookie-ASP.NET 4。x
author: MikeWasson
description: 說明如何在 ASP.NET 4.x 的 Web API 中傳送和接收 HTTP cookie。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557684"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="8f877-103">ASP.NET Web API 中的 HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="8f877-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="8f877-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8f877-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8f877-105">本主題說明如何在 Web API 中傳送和接收 HTTP cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="8f877-106">HTTP Cookie 的背景</span><span class="sxs-lookup"><span data-stu-id="8f877-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="8f877-107">本節提供如何在 HTTP 層級上實作為 cookie 的簡要總覽。</span><span class="sxs-lookup"><span data-stu-id="8f877-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="8f877-108">如需詳細資訊，請參閱[RFC 6265](http://tools.ietf.org/html/rfc6265)。</span><span class="sxs-lookup"><span data-stu-id="8f877-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="8f877-109">Cookie 是伺服器在 HTTP 回應中傳送的一段資料。</span><span class="sxs-lookup"><span data-stu-id="8f877-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="8f877-110">用戶端（選擇性）會儲存 cookie，並在後續要求中傳回它。</span><span class="sxs-lookup"><span data-stu-id="8f877-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="8f877-111">這可讓用戶端和伺服器共用狀態。</span><span class="sxs-lookup"><span data-stu-id="8f877-111">This allows the client and server to share state.</span></span> <span data-ttu-id="8f877-112">若要設定 cookie，伺服器會在回應中包含一個 Set-Cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="8f877-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="8f877-113">Cookie 的格式是具有選擇性屬性的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="8f877-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="8f877-114">例如:</span><span class="sxs-lookup"><span data-stu-id="8f877-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="8f877-115">以下是包含屬性的範例：</span><span class="sxs-lookup"><span data-stu-id="8f877-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="8f877-116">若要將 cookie 傳回給伺服器，用戶端會在後續要求中包含 Cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="8f877-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="8f877-117">HTTP 回應可以包含多個設定 Cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="8f877-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="8f877-118">用戶端會使用單一 Cookie 標頭傳回多個 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="8f877-119">Cookie 的範圍和持續時間是由下列設定-Cookie 標頭中的屬性所控制：</span><span class="sxs-lookup"><span data-stu-id="8f877-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="8f877-120">**網域**：告訴用戶端應接收 cookie 的網域。</span><span class="sxs-lookup"><span data-stu-id="8f877-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="8f877-121">例如，如果網域是 "example.com"，則用戶端會將 cookie 傳回給 example.com 的每個子域。</span><span class="sxs-lookup"><span data-stu-id="8f877-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="8f877-122">如果未指定，則網域為源伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f877-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="8f877-123">**Path**：將 cookie 限制在網域內的指定路徑。</span><span class="sxs-lookup"><span data-stu-id="8f877-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="8f877-124">如果未指定，則會使用要求 URI 的路徑。</span><span class="sxs-lookup"><span data-stu-id="8f877-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="8f877-125">**過期**：設定 cookie 的到期日。</span><span class="sxs-lookup"><span data-stu-id="8f877-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="8f877-126">用戶端會在 cookie 到期時將其刪除。</span><span class="sxs-lookup"><span data-stu-id="8f877-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="8f877-127">**最大壽命**：設定 cookie 的最長存留期。</span><span class="sxs-lookup"><span data-stu-id="8f877-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="8f877-128">用戶端會在達到最長存留期時刪除 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="8f877-129">如果同時設定 `Expires` 和 `Max-Age`，`Max-Age` 會優先使用。</span><span class="sxs-lookup"><span data-stu-id="8f877-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="8f877-130">如果未設定，則用戶端會在目前的會話結束時刪除 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="8f877-131">（「會話」的確切意義是由使用者代理程式所決定）。</span><span class="sxs-lookup"><span data-stu-id="8f877-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="8f877-132">不過，請注意，用戶端可能會忽略 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="8f877-133">例如，使用者可能會因為隱私權原因而停用 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="8f877-134">用戶端可能會在 cookie 過期之前予以刪除，或限制儲存的 cookie 數目。</span><span class="sxs-lookup"><span data-stu-id="8f877-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="8f877-135">基於隱私權原因，用戶端通常會拒絕「協力廠商」 cookie，其中的網域不符合源伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f877-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="8f877-136">簡單地說，伺服器不應該依賴取回它所設定的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="8f877-137">Web API 中的 cookie</span><span class="sxs-lookup"><span data-stu-id="8f877-137">Cookies in Web API</span></span>

<span data-ttu-id="8f877-138">若要將 cookie 新增至 HTTP 回應，請建立代表 cookie 的**CookieHeaderValue**實例。</span><span class="sxs-lookup"><span data-stu-id="8f877-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="8f877-139">然後呼叫**AddCookies**擴充方法，其定義于**System .net. Http 中。HttpResponseHeadersExtensions**類別，以新增 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="8f877-140">例如，下列程式碼會在控制器動作內新增 cookie：</span><span class="sxs-lookup"><span data-stu-id="8f877-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="8f877-141">請注意， **AddCookies**會採用**CookieHeaderValue**實例的陣列。</span><span class="sxs-lookup"><span data-stu-id="8f877-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="8f877-142">若要從用戶端要求中解壓縮 cookie，請呼叫**GetCookies**方法：</span><span class="sxs-lookup"><span data-stu-id="8f877-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="8f877-143">**CookieHeaderValue**包含**CookieState**實例的集合。</span><span class="sxs-lookup"><span data-stu-id="8f877-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="8f877-144">每個**CookieState**都代表一個 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="8f877-145">使用索引子方法，依名稱取得**CookieState** ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8f877-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="8f877-146">結構化 Cookie 資料</span><span class="sxs-lookup"><span data-stu-id="8f877-146">Structured Cookie Data</span></span>

<span data-ttu-id="8f877-147">許多瀏覽器會限制他們會儲存&#8212;總數的 cookie 數，以及每個網域的數目。</span><span class="sxs-lookup"><span data-stu-id="8f877-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="8f877-148">因此，將結構化的資料放入單一 cookie，而不是設定多個 cookie，可能會很有用。</span><span class="sxs-lookup"><span data-stu-id="8f877-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="8f877-149">RFC 6265 不會定義 cookie 資料的結構。</span><span class="sxs-lookup"><span data-stu-id="8f877-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="8f877-150">使用**CookieHeaderValue**類別，您可以傳遞 cookie 資料的名稱/值組清單。</span><span class="sxs-lookup"><span data-stu-id="8f877-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="8f877-151">這些名稱/值配對會編碼為設定 Cookie 標頭中的 URL 編碼格式資料：</span><span class="sxs-lookup"><span data-stu-id="8f877-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="8f877-152">先前的程式碼會產生下列設定 Cookie 標頭：</span><span class="sxs-lookup"><span data-stu-id="8f877-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="8f877-153">**CookieState**類別提供索引子方法，以便從要求訊息中的 cookie 讀取子值：</span><span class="sxs-lookup"><span data-stu-id="8f877-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="8f877-154">範例：在訊息處理常式中設定和取出 Cookie</span><span class="sxs-lookup"><span data-stu-id="8f877-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="8f877-155">先前的範例示範如何從 Web API 控制器內使用 cookie。</span><span class="sxs-lookup"><span data-stu-id="8f877-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="8f877-156">另一個選項是使用[訊息處理常式](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="8f877-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="8f877-157">訊息處理常式會在管線中的前面叫用，而不是控制器。</span><span class="sxs-lookup"><span data-stu-id="8f877-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="8f877-158">訊息處理常式可以在要求到達控制器之前從要求讀取 cookie，或在控制器產生回應後將 cookie 新增至回應。</span><span class="sxs-lookup"><span data-stu-id="8f877-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="8f877-159">下列程式碼顯示用來建立會話識別碼的訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="8f877-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="8f877-160">會話識別碼會儲存在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="8f877-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="8f877-161">處理常式會檢查會話 cookie 的要求。</span><span class="sxs-lookup"><span data-stu-id="8f877-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="8f877-162">如果要求不包含 cookie，處理常式會產生新的會話識別碼。</span><span class="sxs-lookup"><span data-stu-id="8f877-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="8f877-163">不論是哪一種情況，處理常式都會將會話識別碼儲存在**HttpRequestMessage**屬性包中。</span><span class="sxs-lookup"><span data-stu-id="8f877-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="8f877-164">它也會將會話 cookie 新增至 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="8f877-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="8f877-165">此執行不會驗證來自用戶端的會話識別碼是否確實由伺服器發出。</span><span class="sxs-lookup"><span data-stu-id="8f877-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="8f877-166">請勿使用它做為驗證的形式！</span><span class="sxs-lookup"><span data-stu-id="8f877-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="8f877-167">範例的重點在於顯示 HTTP cookie 管理。</span><span class="sxs-lookup"><span data-stu-id="8f877-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="8f877-168">控制器可以從**HttpRequestMessage**屬性包取得會話識別碼。</span><span class="sxs-lookup"><span data-stu-id="8f877-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
