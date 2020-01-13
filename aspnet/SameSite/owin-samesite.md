---
title: 使用 SameSite cookie 和 Open Web Interface for .NET （OWIN）
author: rick-anderson
description: 使用 SameSite cookie 和 Open Web Interface for .NET （OWIN）
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: ac5ae24eeb9e8e1cc6296667a4bebef72c3eb62c
ms.sourcegitcommit: 7b1e1784213dd4c301635f9e181764f3e2f94162
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/10/2019
ms.locfileid: "74993072"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a><span data-ttu-id="c3a4d-103">SameSite cookie 和 Open Web Interface for .NET （OWIN）</span><span class="sxs-lookup"><span data-stu-id="c3a4d-103">SameSite cookies and the Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="c3a4d-104">由 [Rick Anderson](https://twitter.com/RickAndMSFT) 提供</span><span class="sxs-lookup"><span data-stu-id="c3a4d-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c3a4d-105">`SameSite` 是針對跨網站偽造要求（CSRF）攻擊提供一些保護的[IETF](https://ietf.org/about/)草稿。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-105">`SameSite` is an [IETF](https://ietf.org/about/) draft designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="c3a4d-106">[SameSite 2019 草稿](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-106">The [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span></span>

* <span data-ttu-id="c3a4d-107">預設會將 cookie 視為 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-107">Treats cookies as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="c3a4d-108">說明明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie 應標示為 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-108">States cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span>

<span data-ttu-id="c3a4d-109">`Lax` 適用于大部分的應用程式 cookie。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-109">`Lax` works for most app cookies.</span></span> <span data-ttu-id="c3a4d-110">某些形式的驗證，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[WS-同盟](https://auth0.com/docs/protocols/ws-fed)，預設為以 POST 為基礎的重新導向。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-110">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="c3a4d-111">以 POST 為基礎的重新導向會觸發 `SameSite` 的瀏覽器保護，因此已停用這些元件的 `SameSite`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-111">The POST based redirects trigger the `SameSite` browser protections, so `SameSite` is disabled for these components.</span></span> <span data-ttu-id="c3a4d-112">大部分的[OAuth](https://oauth.net/)登入不會受到影響，因為要求的流動方式不同。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-112">Most [OAuth](https://oauth.net/) logins aren't affected due to differences in how the request flows.</span></span> <span data-ttu-id="c3a4d-113">根據預設，所有其他元件都**不會**設定 `SameSite`，並使用用戶端預設行為（舊的或新的）。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-113">All other components do **not** set `SameSite` by default and use the clients default behavior (old or new).</span></span>

<span data-ttu-id="c3a4d-114">`None` 參數會導致用戶端的相容性問題，而此標準會實作為先前的[2016 草稿標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)（例如 iOS 12）。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-114">The `None` parameter causes compatibility problems with clients that implemented the prior [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (for example, iOS 12).</span></span> <span data-ttu-id="c3a4d-115">請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-115">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="c3a4d-116">每個發出 cookie 的 OWIN 元件都必須決定 `SameSite` 是否適當。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-116">Each OWIN component that emits cookies needs to decide if `SameSite` is appropriate.</span></span>

<span data-ttu-id="c3a4d-117">如需本文的 ASP.NET 4.x 版本，請參閱 <xref:samesite/system-web-samesite>。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-117">For the ASP.NET 4.x version of this article, see <xref:samesite/system-web-samesite>.</span></span>

## <a name="api-usage-with-samesite"></a><span data-ttu-id="c3a4d-118">使用 SameSite 的 API 使用方式</span><span class="sxs-lookup"><span data-stu-id="c3a4d-118">API usage with SameSite</span></span>

<span data-ttu-id="c3a4d-119">`Microsoft.Owin` 有自己的 `SameSite` 執行：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-119">`Microsoft.Owin` has its own `SameSite` implementation:</span></span>

* <span data-ttu-id="c3a4d-120">這不會直接相依于 `System.Web`中的。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-120">That is not directly dependent on the one in `System.Web`.</span></span>
* <span data-ttu-id="c3a4d-121">`SameSite` 適用于 `Microsoft.Owin` 封裝（.NET 4.5 和更新版本）所目標設為的所有版本。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-121">`SameSite` works on all versions targetable by the `Microsoft.Owin` packages, .NET 4.5 and later.</span></span>
* <span data-ttu-id="c3a4d-122">只有[SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)元件會直接與 `System.Web` `HttpCookie` 類別互動。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-122">Only the [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) component directly interacts with the `System.Web` `HttpCookie` class.</span></span>

<span data-ttu-id="c3a4d-123">`SystemWebCookieManager` 取決於 .NET 4.7.2 `System.Web` Api，以啟用 `SameSite` 支援，以及變更行為的修補程式。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-123">`SystemWebCookieManager` depends on the .NET 4.7.2 `System.Web` APIs to enable `SameSite` support, and the patches to change the behavior.</span></span>

<span data-ttu-id="c3a4d-124">[OWIN 和 system.web 回應 cookie 整合問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)中概述了使用 `SystemWebCookieManager` 的原因。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-124">The reasons to use `SystemWebCookieManager` are outlined in [OWIN and System.Web response cookie integration issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues).</span></span> <span data-ttu-id="c3a4d-125">在 `System.Web`上執行時，建議 `SystemWebCookieManager`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-125">`SystemWebCookieManager` is recommended when running on `System.Web`.</span></span>

<span data-ttu-id="c3a4d-126">下列程式碼會將 `SameSite` 設定為 `Lax`：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-126">The following code sets `SameSite` to `Lax`:</span></span>

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

<span data-ttu-id="c3a4d-127">下列 Api 會使用 `SameSite`：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-127">The following APIs use `SameSite`:</span></span>

* [<span data-ttu-id="c3a4d-128">Owin. SameSiteMode</span><span class="sxs-lookup"><span data-stu-id="c3a4d-128">Microsoft.Owin.SameSiteMode</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [<span data-ttu-id="c3a4d-129">Cookieoptions.secure. SameSite</span><span class="sxs-lookup"><span data-stu-id="c3a4d-129">CookieOptions.SameSite</span></span>](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* <span data-ttu-id="c3a4d-130">[Cookieauthenticationoptions.authenticationtype 類別](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="c3a4d-130">[CookieAuthenticationOptions Class](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span></span> <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [<span data-ttu-id="c3a4d-131">Cookieauthenticationoptions.authenticationtype. CookieSameSite</span><span class="sxs-lookup"><span data-stu-id="c3a4d-131">CookieAuthenticationOptions.CookieSameSite</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* <span data-ttu-id="c3a4d-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="c3a4d-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span></span>
* [<span data-ttu-id="c3a4d-133">SystemWebCookieManager</span><span class="sxs-lookup"><span data-stu-id="c3a4d-133">SystemWebCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [<span data-ttu-id="c3a4d-134">SystemWebChunkingCookieManager</span><span class="sxs-lookup"><span data-stu-id="c3a4d-134">SystemWebChunkingCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [<span data-ttu-id="c3a4d-135">Cookieauthenticationoptions.authenticationtype. CookieManager</span><span class="sxs-lookup"><span data-stu-id="c3a4d-135">CookieAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [<span data-ttu-id="c3a4d-136">OpenIdConnectAuthenticationOptions. CookieManager</span><span class="sxs-lookup"><span data-stu-id="c3a4d-136">OpenIdConnectAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a><span data-ttu-id="c3a4d-137">歷程記錄和變更</span><span class="sxs-lookup"><span data-stu-id="c3a4d-137">History and changes</span></span>

<span data-ttu-id="c3a4d-138">[Owin](https://www.nuget.org/packages/Microsoft.Owin/)不支援[`SameSite` 2016 草案標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-138">[Microsoft.Owin](https://www.nuget.org/packages/Microsoft.Owin/) never supported the [`SameSite` 2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="c3a4d-139">只有 `Microsoft.Owin` 4.1.0 和更新版本才提供對[SameSite 2019 草稿](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)的支援。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-139">Support for the [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) is only available in `Microsoft.Owin` 4.1.0 and later.</span></span> <span data-ttu-id="c3a4d-140">先前版本沒有修補程式。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-140">There are no patches for prior versions.</span></span>

<span data-ttu-id="c3a4d-141">`SameSite` 規格的2019草稿：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-141">The 2019 draft of the `SameSite` specification:</span></span>

* <span data-ttu-id="c3a4d-142">與2016草稿**不**相容。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-142">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="c3a4d-143">如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-143">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="c3a4d-144">指定預設會將 cookie 視為 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-144">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="c3a4d-145">指定明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie，應該標示為 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-145">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span> <span data-ttu-id="c3a4d-146">`None` 是退出宣告的新專案。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-146">`None` is a new entry to opt out.</span></span>
* <span data-ttu-id="c3a4d-147">排定預設會在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)由 [Chrome](https://chromestatus.com/feature/5088147346030592) 啟用。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-147">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="c3a4d-148">瀏覽器已開始移至2019中的此標準。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-148">Browsers started moving to this standard in 2019.</span></span>
* <span data-ttu-id="c3a4d-149">發行的修補程式支援，如知識庫文章所述。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-149">Is supported by patches issued as described in KB articles.</span></span> <span data-ttu-id="c3a4d-150">如需詳細資訊，請參閱<xref:samesite/kbs-samesite>。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-150">For more information, see <xref:samesite/kbs-samesite>.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="c3a4d-151">支援舊版瀏覽器</span><span class="sxs-lookup"><span data-stu-id="c3a4d-151">Supporting older browsers</span></span>

<span data-ttu-id="c3a4d-152">2016 `SameSite` 標準規定必須將未知的值視為 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-152">The 2016 `SameSite` standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="c3a4d-153">從支援 2016 `SameSite` standard 的舊版瀏覽器存取的應用程式，可能會在取得值為 `None`的 `SameSite` 屬性時中斷。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-153">Apps accessed from older browsers which support the 2016 `SameSite` standard may break when they get a `SameSite` property with a value of `None`.</span></span> <span data-ttu-id="c3a4d-154">如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-154">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="c3a4d-155">ASP.NET 不會實作為瀏覽器偵測，因為使用者代理程式的值會高度變動並經常變更。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-155">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="c3a4d-156">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))中的擴充點允許插入使用者代理程式特定的邏輯。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-156">An extension point in [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) allows plugging in User-Agent specific logic.</span></span>
<!-- https://docs.microsoft.com/en-us/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

<span data-ttu-id="c3a4d-157">在 `Startup.Configuration`中，新增類似下列的程式碼：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-157">In `Startup.Configuration`, add code similar to the following:</span></span>

[!code-csharp[](sample/Startup1.cs?name=snippet)]

<span data-ttu-id="c3a4d-158">上述程式碼需要 .NET 4.7.2 或更新版本 `SameSite` patch。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-158">The preceding code requires the .NET 4.7.2 or later `SameSite` patch.</span></span>

<span data-ttu-id="c3a4d-159">下列程式碼顯示 `SameSiteCookieManager`的範例執行：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-159">The following code shows an example implementation of `SameSiteCookieManager`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

<span data-ttu-id="c3a4d-160">在上述範例中，會在 `CheckSameSite` 方法中呼叫 `DisallowsSameSiteNone`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-160">In the preceding sample, `DisallowsSameSiteNone` is called in the `CheckSameSite` method.</span></span> <span data-ttu-id="c3a4d-161">`DisallowsSameSiteNone` 是一個使用者方法，它會偵測使用者代理程式是否不支援 `SameSite` `None`：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-161">`DisallowsSameSiteNone` is a user method that detects if the user agent doesn't support `SameSite` `None`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

<span data-ttu-id="c3a4d-162">下列程式碼顯示範例 `DisallowsSameSiteNone` 方法：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-162">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="c3a4d-163">下列程式碼僅供示範之用：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-163">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="c3a4d-164">不應該將它視為已完成。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-164">It should not be considered complete.</span></span>
> * <span data-ttu-id="c3a4d-165">不會維護或支援。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-165">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="c3a4d-166">測試應用程式的 SameSite 問題</span><span class="sxs-lookup"><span data-stu-id="c3a4d-166">Test apps for SameSite problems</span></span>

<span data-ttu-id="c3a4d-167">與遠端網站（例如透過協力廠商登入）互動的應用程式需要：</span><span class="sxs-lookup"><span data-stu-id="c3a4d-167">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="c3a4d-168">測試多個瀏覽器的互動。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-168">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="c3a4d-169">套用本檔中討論的[瀏覽器偵測和緩和措施](#sob)。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-169">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="c3a4d-170">使用可選擇新的 `SameSite` 行為的用戶端版本來測試 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-170">Test web apps using a client version that can opt-in to the new `SameSite` behavior.</span></span> <span data-ttu-id="c3a4d-171">Chrome、Firefox 和 Chromium Edge 全都具有可用於測試的新加入宣告功能旗標。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-171">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="c3a4d-172">在您的應用程式套用 `SameSite` 修補程式之後，請使用較舊的用戶端版本（尤其是 Safari）進行測試。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-172">After your app applies the `SameSite` patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="c3a4d-173">如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-173">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="c3a4d-174">使用 Chrome 進行測試</span><span class="sxs-lookup"><span data-stu-id="c3a4d-174">Test with Chrome</span></span>

<span data-ttu-id="c3a4d-175">Chrome 78 + 會提供誤導的結果，因為它有暫時的緩和措施。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-175">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="c3a4d-176">Chrome 78 + 暫時緩和可讓 cookie 少於兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-176">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="c3a4d-177">已啟用適當測試旗標的 Chrome 76 或77提供更精確的結果。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-177">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="c3a4d-178">若要測試新的 `SameSite` 行為，請將 `chrome://flags/#same-site-by-default-cookies` 切換為 [**啟用**]。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-178">To test the new `SameSite` behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="c3a4d-179">舊版 Chrome （75和更低版本）會回報為失敗，並出現新的 `None` 設定。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-179">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="c3a4d-180">請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-180">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="c3a4d-181">Google 不會提供舊版的 chrome 版本。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-181">Google does not make older chrome versions available.</span></span> <span data-ttu-id="c3a4d-182">請遵循[下載 Chromium](https://www.chromium.org/getting-involved/download-chromium)的指示來測試舊版 Chrome。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-182">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="c3a4d-183">請勿從搜尋舊版 chrome 所提供的**連結下載 Chrome** 。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-183">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="c3a4d-184">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="c3a4d-184">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="c3a4d-185">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="c3a4d-185">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="c3a4d-186">使用 Safari 進行測試</span><span class="sxs-lookup"><span data-stu-id="c3a4d-186">Test with Safari</span></span>

<span data-ttu-id="c3a4d-187">Safari 12 會嚴格實作為先前的草稿，並在新的 `None` 值在 cookie 中失敗。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-187">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="c3a4d-188">透過此檔中[支援較舊流覽](#sob)器的瀏覽器偵測程式碼，可避免 `None`。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-188">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="c3a4d-189">使用 MSAL、ADAL 或您使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-189">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="c3a4d-190">問題取決於基礎作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-190">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="c3a4d-191">OSX Mojave （10.14）和 iOS 12 已知有新 `SameSite` 行為的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-191">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new `SameSite` behavior.</span></span> <span data-ttu-id="c3a4d-192">將 OS 升級至 OSX Catalina （10.15）或 iOS 13 會修正問題。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-192">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="c3a4d-193">Safari 目前沒有加入宣告旗標來測試新的規格行為。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-193">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="c3a4d-194">使用 Firefox 進行測試</span><span class="sxs-lookup"><span data-stu-id="c3a4d-194">Test with Firefox</span></span>

<span data-ttu-id="c3a4d-195">在 [`about:config`] 頁面上選擇 [`network.cookie.sameSite.laxByDefault`] 功能旗標，即可在版本 68 + 上測試新標準的 Firefox 支援。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-195">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="c3a4d-196">尚未報告舊版 Firefox 的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-196">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="c3a4d-197">使用 Edge 瀏覽器進行測試</span><span class="sxs-lookup"><span data-stu-id="c3a4d-197">Test with Edge browser</span></span>

<span data-ttu-id="c3a4d-198">Edge 支援舊的 `SameSite` 標準。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-198">Edge supports the old `SameSite` standard.</span></span> <span data-ttu-id="c3a4d-199">Edge 版本44沒有任何已知的新標準相容性問題。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-199">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="c3a4d-200">使用 Edge 進行測試（Chromium）</span><span class="sxs-lookup"><span data-stu-id="c3a4d-200">Test with Edge (Chromium)</span></span>

<span data-ttu-id="c3a4d-201">`SameSite` 旗標是設定在 [`edge://flags/#same-site-by-default-cookies`] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-201">`SameSite` flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="c3a4d-202">Edge Chromium 未發現相容性問題。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-202">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="c3a4d-203">使用 Electron 進行測試</span><span class="sxs-lookup"><span data-stu-id="c3a4d-203">Test with Electron</span></span>

<span data-ttu-id="c3a4d-204">Electron 的版本包含舊版的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-204">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="c3a4d-205">例如，小組所使用的 Electron 版本是 Chromium 66，這會展現較舊的行為。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-205">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="c3a4d-206">您必須使用您的產品所使用的 Electron 版本來執行自己的相容性測試。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-206">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="c3a4d-207">請參閱下一節中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="c3a4d-207">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3a4d-208">其他資源</span><span class="sxs-lookup"><span data-stu-id="c3a4d-208">Additional resources</span></span>

* [<span data-ttu-id="c3a4d-209">Chromium Blog：開發人員：準備開始新的 SameSite = None;安全 Cookie 設定</span><span class="sxs-lookup"><span data-stu-id="c3a4d-209">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="c3a4d-210">SameSite cookie 說明</span><span class="sxs-lookup"><span data-stu-id="c3a4d-210">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="c3a4d-211">OWIN 和 System.web 回應 cookie 整合問題</span><span class="sxs-lookup"><span data-stu-id="c3a4d-211">OWIN and System.Web response cookie integration issues</span></span>](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
