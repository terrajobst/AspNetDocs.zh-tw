---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API 中的表單驗證 |Microsoft Docs
author: MikeWasson
description: 描述在 ASP.NET Web API 中使用表單驗證。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598592"
---
# <a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="575c0-103">ASP.NET Web API 中的表單驗證</span><span class="sxs-lookup"><span data-stu-id="575c0-103">Forms Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="575c0-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="575c0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="575c0-105">表單驗證會使用 HTML 表單，將使用者的認證傳送給伺服器。</span><span class="sxs-lookup"><span data-stu-id="575c0-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="575c0-106">這不是網際網路標準。</span><span class="sxs-lookup"><span data-stu-id="575c0-106">It is not an Internet standard.</span></span> <span data-ttu-id="575c0-107">表單驗證僅適用于從 web 應用程式呼叫的 web Api，讓使用者可以與 HTML 表單進行互動。</span><span class="sxs-lookup"><span data-stu-id="575c0-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="575c0-108">優點</span><span class="sxs-lookup"><span data-stu-id="575c0-108">Advantages</span></span> | <span data-ttu-id="575c0-109">缺點</span><span class="sxs-lookup"><span data-stu-id="575c0-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="575c0-110">-易於執行：內建于 ASP.NET 中。</span><span class="sxs-lookup"><span data-stu-id="575c0-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="575c0-111">-使用 ASP.NET 成員資格提供者，這可讓您輕鬆地管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="575c0-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="575c0-112">-不是標準 HTTP 驗證機制;會使用 HTTP cookie，而不是標準的授權標頭。</span><span class="sxs-lookup"><span data-stu-id="575c0-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="575c0-113">-需要瀏覽器用戶端。</span><span class="sxs-lookup"><span data-stu-id="575c0-113">- Requires a browser client.</span></span> <span data-ttu-id="575c0-114">-認證會以純文字傳送。</span><span class="sxs-lookup"><span data-stu-id="575c0-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="575c0-115">-容易遭受跨網站偽造要求（CSRF）;需要反 CSRF 量值。</span><span class="sxs-lookup"><span data-stu-id="575c0-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="575c0-116">-不容易從 nonbrowser 用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="575c0-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="575c0-117">登入需要瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="575c0-117">Login requires a browser.</span></span> <span data-ttu-id="575c0-118">-使用者認證會在要求中傳送。</span><span class="sxs-lookup"><span data-stu-id="575c0-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="575c0-119">-某些使用者停用 cookie。</span><span class="sxs-lookup"><span data-stu-id="575c0-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="575c0-120">簡單地說，ASP.NET 中的表單驗證的運作方式如下所示：</span><span class="sxs-lookup"><span data-stu-id="575c0-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="575c0-121">用戶端會要求需要驗證的資源。</span><span class="sxs-lookup"><span data-stu-id="575c0-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="575c0-122">如果使用者未經過驗證，伺服器會傳回 HTTP 302 （找到）並重新導向至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="575c0-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="575c0-123">使用者輸入認證並提交表單。</span><span class="sxs-lookup"><span data-stu-id="575c0-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="575c0-124">伺服器會傳回另一個 HTTP 302，以重新導向回原始 URI。</span><span class="sxs-lookup"><span data-stu-id="575c0-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="575c0-125">此回應包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="575c0-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="575c0-126">用戶端再次要求資源。</span><span class="sxs-lookup"><span data-stu-id="575c0-126">The client requests the resource again.</span></span> <span data-ttu-id="575c0-127">此要求包含驗證 cookie，因此伺服器會授與要求。</span><span class="sxs-lookup"><span data-stu-id="575c0-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="575c0-128">如需詳細資訊，請參閱[表單驗證的總覽。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span><span class="sxs-lookup"><span data-stu-id="575c0-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="575c0-129">使用表單驗證搭配 Web API</span><span class="sxs-lookup"><span data-stu-id="575c0-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="575c0-130">若要建立使用表單驗證的應用程式，請在 MVC 4 專案嚮導中選取 [網際網路應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="575c0-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="575c0-131">此範本會建立用於管理帳戶的 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="575c0-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="575c0-132">您也可以使用 ASP.NET 秋季2012更新中所提供的「單一頁面應用程式」範本。</span><span class="sxs-lookup"><span data-stu-id="575c0-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="575c0-133">在 Web API 控制器中，您可以使用 `[Authorize]` 屬性來限制存取，如[使用 [授權] 屬性](authentication-and-authorization-in-aspnet-web-api.md#auth3)中所述。</span><span class="sxs-lookup"><span data-stu-id="575c0-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="575c0-134">表單驗證會使用會話 cookie 來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="575c0-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="575c0-135">瀏覽器會自動將所有相關的 cookie 傳送至目的地網站。</span><span class="sxs-lookup"><span data-stu-id="575c0-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="575c0-136">這項功能讓表單驗證可能容易遭受跨網站偽造要求（CSRF）攻擊，請參閱[防止跨網站偽造要求（CSRF）攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="575c0-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="575c0-137">表單驗證不會加密使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="575c0-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="575c0-138">因此，除非搭配 SSL 使用，否則表單驗證並不安全。</span><span class="sxs-lookup"><span data-stu-id="575c0-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="575c0-139">請參閱[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="575c0-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
