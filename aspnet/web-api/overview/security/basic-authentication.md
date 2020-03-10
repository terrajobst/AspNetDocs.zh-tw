---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 中的基本驗證 |Microsoft Docs
author: MikeWasson
description: 描述在 ASP.NET Web API 中使用基本驗證。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555724"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="ac3d4-103">ASP.NET Web API 中的基本驗證</span><span class="sxs-lookup"><span data-stu-id="ac3d4-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="ac3d4-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ac3d4-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ac3d4-105">基本驗證是在 RFC 2617 中定義，也就是[HTTP 驗證：基本和摘要式存取驗證](http://www.ietf.org/rfc/rfc2617.txt)。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="ac3d4-106">缺點</span><span class="sxs-lookup"><span data-stu-id="ac3d4-106">Disadvantages</span></span>

- <span data-ttu-id="ac3d4-107">使用者認證會在要求中傳送。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="ac3d4-108">認證會以純文字傳送。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="ac3d4-109">認證會與每個要求一起傳送。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="ac3d4-110">無法登出，除非結束瀏覽器會話。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="ac3d4-111">容易遭受跨網站偽造要求（CSRF）;需要反 CSRF 量值。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="ac3d4-112">優點</span><span class="sxs-lookup"><span data-stu-id="ac3d4-112">Advantages</span></span>

- <span data-ttu-id="ac3d4-113">網際網路標準。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-113">Internet standard.</span></span>
- <span data-ttu-id="ac3d4-114">受到所有主要瀏覽器的支援。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="ac3d4-115">相對簡單的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-115">Relatively simple protocol.</span></span>

<span data-ttu-id="ac3d4-116">基本驗證的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="ac3d4-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="ac3d4-117">如果要求需要驗證，伺服器會傳回401（未經授權）。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="ac3d4-118">回應包含 WWW 驗證標頭，指出伺服器支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="ac3d4-119">用戶端會使用 Authorization 標頭中的用戶端認證來傳送另一個要求。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="ac3d4-120">認證會格式化為字串 "name： password"，以 base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="ac3d4-121">認證不會加密。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="ac3d4-122">基本驗證是在「領域」的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="ac3d4-123">伺服器會在 WWW 驗證標頭中包含領域的名稱。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="ac3d4-124">使用者的認證在該領域內是有效的。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="ac3d4-125">領域的確切範圍是由伺服器所定義。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="ac3d4-126">例如，您可以定義數個領域來分割資源。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="ac3d4-127">因為認證會以未加密的形式傳送，基本驗證只會透過 HTTPS 保護。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="ac3d4-128">請參閱[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="ac3d4-129">基本驗證也容易遭受 CSRF 攻擊。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="ac3d4-130">在使用者輸入認證之後，瀏覽器會在會話的持續時間內，自動將這些要求傳送至相同的網域。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="ac3d4-131">這包括 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-131">This includes AJAX requests.</span></span> <span data-ttu-id="ac3d4-132">請參閱[防止跨網站偽造要求（CSRF）攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="ac3d4-133">使用 IIS 進行基本驗證</span><span class="sxs-lookup"><span data-stu-id="ac3d4-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="ac3d4-134">IIS 支援基本驗證，但有一點要注意：使用者會針對其 Windows 認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="ac3d4-135">這表示使用者必須擁有伺服器網域上的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="ac3d4-136">對於公開的網站，您通常會想要針對 ASP.NET 成員資格提供者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="ac3d4-137">若要使用 IIS 啟用基本驗證，請在 ASP.NET 專案的 web.config 中將驗證模式設定為 "Windows"：</span><span class="sxs-lookup"><span data-stu-id="ac3d4-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="ac3d4-138">在此模式中，IIS 會使用 Windows 認證來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="ac3d4-139">此外，您必須在 IIS 中啟用基本驗證。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="ac3d4-140">在 IIS 管理員中，移至 [功能] [視圖]，選取 [驗證]，然後啟用 [基本驗證]</span><span class="sxs-lookup"><span data-stu-id="ac3d4-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="ac3d4-141">在您的 Web API 專案中，為任何需要驗證的控制器動作新增 `[Authorize]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="ac3d4-142">用戶端會藉由在要求中設定 Authorization 標頭來驗證本身。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="ac3d4-143">瀏覽器用戶端會自動執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="ac3d4-144">Nonbrowser 用戶端將需要設定標頭。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="ac3d4-145">使用自訂成員資格進行基本驗證</span><span class="sxs-lookup"><span data-stu-id="ac3d4-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="ac3d4-146">如前所述，內建于 IIS 中的基本驗證會使用 Windows 認證。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="ac3d4-147">這表示您需要在主控伺服器上為您的使用者建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="ac3d4-148">但若是網際網路應用程式，使用者帳戶通常會儲存在外部資料庫中。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="ac3d4-149">下列程式碼說明如何執行基本驗證的 HTTP 模組。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="ac3d4-150">您可以藉由取代 `CheckPassword` 方法（在此範例中為虛擬方法），輕鬆地插入 ASP.NET 成員資格提供者。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="ac3d4-151">在 Web API 2 中，您應該考慮撰寫[驗證篩選器](authentication-filters.md)或[OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/index.md)，而不是 HTTP 模組。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="ac3d4-152">若要啟用 HTTP 模組，請將下列內容新增至**system.webserver**區段中的 web.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="ac3d4-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="ac3d4-153">將 "YourAssemblyName" 取代為元件的名稱（不包括 "dll" 副檔名）。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="ac3d4-154">您應該停用其他驗證配置，例如表單或 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="ac3d4-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
