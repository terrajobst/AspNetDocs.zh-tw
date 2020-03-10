---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: 防止 ASP.NET MVC 中的跨網站要求偽造（CSRF）攻擊
author: MikeWasson
description: 描述跨網站偽造要求（CSRF）攻擊，以及如何在 ASP.NET Web MVC 中執行反 CSRF 量值。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555115"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a><span data-ttu-id="1d1ec-103">防止 ASP.NET MVC 應用程式中的跨網站要求偽造（CSRF）攻擊</span><span class="sxs-lookup"><span data-stu-id="1d1ec-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET MVC Application</span></span>

<span data-ttu-id="1d1ec-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1d1ec-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1d1ec-105">跨網站偽造要求（CSRF）是一種攻擊，惡意網站會將要求傳送至使用者目前登入的弱點網站</span><span class="sxs-lookup"><span data-stu-id="1d1ec-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="1d1ec-106">以下是 CSRF 攻擊的範例：</span><span class="sxs-lookup"><span data-stu-id="1d1ec-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="1d1ec-107">使用者使用表單驗證登入 `www.example.com`。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-107">A user logs into `www.example.com` using forms authentication.</span></span>
2. <span data-ttu-id="1d1ec-108">伺服器會驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-108">The server authenticates the user.</span></span> <span data-ttu-id="1d1ec-109">伺服器的回應包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="1d1ec-110">若未登出，使用者會造訪惡意網站。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="1d1ec-111">這個惡意網站包含下列 HTML 表單：</span><span class="sxs-lookup"><span data-stu-id="1d1ec-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="1d1ec-112">請注意，表單動作會張貼到易受攻擊的網站，而不是惡意網站。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="1d1ec-113">這是 CSRF 的「跨網站」部分。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="1d1ec-114">使用者按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-114">The user clicks the submit button.</span></span> <span data-ttu-id="1d1ec-115">瀏覽器會在要求中包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="1d1ec-116">此要求會在伺服器上以使用者的驗證內容執行，並可執行已驗證使用者允許執行的任何動作。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="1d1ec-117">雖然此範例需要使用者按一下表單按鈕，但惡意的網頁也可以輕鬆地執行自動提交表單的腳本。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="1d1ec-118">此外，使用 SSL 並不會防止 CSRF 攻擊，因為惡意網站可以傳送「HTTPs://」要求。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="1d1ec-119">一般來說，使用 cookie 進行驗證的網站可能會發生 CSRF 攻擊，因為瀏覽器會將所有相關的 cookie 傳送至目的地網站。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="1d1ec-120">不過，CSRF 攻擊並不限於利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="1d1ec-121">例如，基本和摘要式驗證也很容易受到攻擊。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="1d1ec-122">使用者使用基本或摘要式驗證登入之後。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="1d1ec-123">瀏覽器會自動傳送認證，直到會話結束為止。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="1d1ec-124">防偽標記</span><span class="sxs-lookup"><span data-stu-id="1d1ec-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="1d1ec-125">為了協助防止 CSRF 攻擊，ASP.NET MVC 會使用防偽權杖，也稱為*要求驗證權杖*。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="1d1ec-126">用戶端會要求包含表單的 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="1d1ec-127">伺服器會在回應中包含兩個權杖。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="1d1ec-128">一個權杖會當做 cookie 傳送。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-128">One token is sent as a cookie.</span></span> <span data-ttu-id="1d1ec-129">另一個則放在隱藏的表單欄位中。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="1d1ec-130">系統會隨機產生權杖，讓敵人無法猜測值。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="1d1ec-131">當用戶端提交表單時，必須將這兩個權杖傳回給伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="1d1ec-132">用戶端會傳送 cookie 權杖做為 cookie，並將表單 token 傳送至表單資料內。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="1d1ec-133">（當使用者提交表單時，瀏覽器用戶端會自動執行此工作）。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="1d1ec-134">如果要求不包含這兩個權杖，伺服器就不會允許該要求。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="1d1ec-135">以下是具有隱藏表單標記的 HTML 表單範例：</span><span class="sxs-lookup"><span data-stu-id="1d1ec-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="1d1ec-136">防偽 token 可以使用，因為由於相同來源的原則，惡意網頁無法讀取使用者的權杖。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="1d1ec-137">（[相同來源原則](http://www.w3.org/Security/wiki/Same_Origin_Policy)會防止裝載于兩個不同網站的檔存取彼此的內容。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="1d1ec-138">因此在先前的範例中，惡意網頁可以將要求傳送至 example.com，但它無法讀取回應。）</span><span class="sxs-lookup"><span data-stu-id="1d1ec-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="1d1ec-139">若要防止 CSRF 攻擊，請使用反偽造權杖搭配任何驗證通訊協定，瀏覽器會在使用者登入之後，以無訊息方式傳送認證。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="1d1ec-140">這包括以 cookie 為基礎的驗證通訊協定，例如表單驗證，以及基本和摘要式驗證等通訊協定。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="1d1ec-141">您應該針對任何 nonsafe 方法（POST、PUT、DELETE）要求防偽 token。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="1d1ec-142">此外，請確定安全方法（GET、HEAD）沒有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="1d1ec-143">此外，如果您啟用跨網域支援（例如 CORS 或 JSONP），那麼即使 GET 之類的安全方法也可能容易遭受 CSRF 攻擊，讓攻擊者能夠讀取潛在的敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="1d1ec-144">ASP.NET MVC 中的防偽標記</span><span class="sxs-lookup"><span data-stu-id="1d1ec-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="1d1ec-145">若要將防偽標記新增至 Razor 頁面，請使用**HtmlHelper. AntiForgeryToken** helper 方法：</span><span class="sxs-lookup"><span data-stu-id="1d1ec-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="1d1ec-146">這個方法會新增隱藏的表單欄位，也會設定 cookie token。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="1d1ec-147">反 CSRF 和 AJAX</span><span class="sxs-lookup"><span data-stu-id="1d1ec-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="1d1ec-148">由於 AJAX 要求可能會傳送 JSON 資料，而不是 HTML 表單資料，因此，表單 token 可能會是 AJAX 要求的問題。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="1d1ec-149">有一個解決方案是在自訂 HTTP 標頭中傳送權杖。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="1d1ec-150">下列程式碼使用 Razor 語法來產生權杖，然後將權杖新增至 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="1d1ec-151">權杖是在伺服器上藉由呼叫 AntiForgery 來產生的 **。 GetTokens**。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="1d1ec-152">當您處理要求時，請從要求標頭擷取權杖。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="1d1ec-153">然後呼叫**AntiForgery**方法來驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="1d1ec-154">如果權杖無效， **Validate**方法會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1d1ec-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
