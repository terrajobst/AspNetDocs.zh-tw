---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 瞭解如何在 ASP.NET 中使用 SameSite cookie
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: c81ca38648609aa5347d2a8cc11889fc85d81711
ms.sourcegitcommit: 4d439e01c82c7c95b19216fedaf5b1a11a1deb06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76826610"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="386af-103">在 ASP.NET 中使用 SameSite cookie</span><span class="sxs-lookup"><span data-stu-id="386af-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="386af-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="386af-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="386af-105">SameSite 是一種[IETF](https://ietf.org/about/)草稿標準，旨在針對跨網站偽造要求（CSRF）攻擊提供一些保護。</span><span class="sxs-lookup"><span data-stu-id="386af-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="386af-106">初稿標準已于[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)開始繪製，已于[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)更新。</span><span class="sxs-lookup"><span data-stu-id="386af-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="386af-107">更新的標準不會與前一個標準回溯相容，下列是最顯著的差異：</span><span class="sxs-lookup"><span data-stu-id="386af-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="386af-108">預設會將不含 SameSite 標頭的 cookie 視為 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="386af-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="386af-109">`SameSite=None` 必須用來允許跨網站 cookie 的使用。</span><span class="sxs-lookup"><span data-stu-id="386af-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="386af-110">判斷提示 `SameSite=None` 的 cookie 也必須標示為 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="386af-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="386af-111">[2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允許值 SameSite = None，而是讓一些執行方式將這類 Cookie 視為 SameSite = Strict。</span><span class="sxs-lookup"><span data-stu-id="386af-111">The value SameSite=None is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as SameSite=Strict.</span></span> <span data-ttu-id="386af-112">請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="386af-112">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="386af-113">[`SameSite=Lax`] 設定適用于大部分的應用程式 cookie。</span><span class="sxs-lookup"><span data-stu-id="386af-113">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="386af-114">某些形式的驗證，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[WS-同盟](https://auth0.com/docs/protocols/ws-fed)，預設為以 POST 為基礎的重新導向。</span><span class="sxs-lookup"><span data-stu-id="386af-114">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="386af-115">以 POST 為基礎的重新導向會觸發 SameSite 瀏覽器保護，因此這些元件已停用 SameSite。</span><span class="sxs-lookup"><span data-stu-id="386af-115">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="386af-116">大部分的[OAuth](https://oauth.net/)登入都不會受到影響，因為要求的流動方式不同。</span><span class="sxs-lookup"><span data-stu-id="386af-116">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="386af-117">使用 `iframe` 的應用程式可能會遇到 `SameSite=Lax` 或 `SameSite=Strict` cookie 的問題，因為 iframe 會被視為跨網站案例。</span><span class="sxs-lookup"><span data-stu-id="386af-117">Applications that use `iframe` may experience issues with `SameSite=Lax` or `SameSite=Strict` cookies because iframes are treated as cross-site scenarios.</span></span>

<span data-ttu-id="386af-118">發出 cookie 的每個 ASP.NET 元件都必須決定 SameSite 是否適當。</span><span class="sxs-lookup"><span data-stu-id="386af-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="386af-119">在安裝 2019 .Net SameSite 更新之後，請參閱應用程式問題的[已知問題](#known)。</span><span class="sxs-lookup"><span data-stu-id="386af-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="386af-120">在 ASP.NET 4.7.2 和4.8 中使用 SameSite</span><span class="sxs-lookup"><span data-stu-id="386af-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="386af-121">.Net 4.7.2 和4.8 支援自12月2019的更新發行以來，SameSite 的[2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) 。</span><span class="sxs-lookup"><span data-stu-id="386af-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="386af-122">開發人員可以使用[HttpCookie. SameSite 屬性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)，以程式設計方式控制 SameSite 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="386af-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="386af-123">將 `SameSite` 屬性設定為 `Strict`、`Lax` 或 `None` 會導致在網路上使用 cookie 寫入這些值。</span><span class="sxs-lookup"><span data-stu-id="386af-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="386af-124">將其設定為等於 `(SameSiteMode)(-1)` 表示不應在具有 cookie 的網路上包含任何 SameSite 標頭。</span><span class="sxs-lookup"><span data-stu-id="386af-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="386af-125">Config 檔案中的[HttpCookie 屬性](/dotnet/api/system.web.httpcookie.secure)或 ' requireSSL ' 可以用來將 cookie 標記為 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="386af-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="386af-126">新的 `HttpCookie` 實例會預設為 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false`。</span><span class="sxs-lookup"><span data-stu-id="386af-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="386af-127">這些預設值可以在 `system.web/httpCookies` 設定區段中覆寫，其中字串 `"Unspecified"` 是適用于 `(SameSiteMode)(-1)`的易記僅限設定語法：</span><span class="sxs-lookup"><span data-stu-id="386af-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="386af-128">ASP.Net 也會針對這些功能發行自己的四個特定 cookie：匿名驗證、表單驗證、會話狀態和角色管理。</span><span class="sxs-lookup"><span data-stu-id="386af-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="386af-129">在執行時間取得的這些 cookie 實例，可以使用 `SameSite` 和 `Secure` 屬性來操作，就像任何其他 HttpCookie 實例一樣。</span><span class="sxs-lookup"><span data-stu-id="386af-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="386af-130">不過，由於 SameSite 標準的 patchwork 出現，因此這四個功能 cookie 的設定選項不一致。</span><span class="sxs-lookup"><span data-stu-id="386af-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="386af-131">相關的設定區段和屬性（含預設值）如下所示。</span><span class="sxs-lookup"><span data-stu-id="386af-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="386af-132">如果沒有 `SameSite` 或 `Secure` 功能的相關屬性，則此功能會切換回前面所討論的 [`system.web/httpCookies`] 區段中所設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="386af-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequiresSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

<span data-ttu-id="386af-133">**注意**： ' 未指定 ' 僅適用于目前 `system.web/httpCookies@sameSite`。</span><span class="sxs-lookup"><span data-stu-id="386af-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="386af-134">我們希望在未來的更新中，將類似的語法新增至先前顯示的 cookieSameSite 屬性。</span><span class="sxs-lookup"><span data-stu-id="386af-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="386af-135">在程式碼中設定 `(SameSiteMode)(-1)` 仍可在這些 cookie 的實例上運作。 \*</span><span class="sxs-lookup"><span data-stu-id="386af-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="386af-136">歷程記錄和變更</span><span class="sxs-lookup"><span data-stu-id="386af-136">History and changes</span></span>

<span data-ttu-id="386af-137">SameSite 支援首次使用[2016 draft 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)在 .net 4.7.2 中執行。</span><span class="sxs-lookup"><span data-stu-id="386af-137">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="386af-138">2019年11月19日的 Windows 更新，已將 .NET 4.7.2 + 從2016標準更新為2019標準。</span><span class="sxs-lookup"><span data-stu-id="386af-138">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="386af-139">其他版本的 Windows 即將推出其他更新。</span><span class="sxs-lookup"><span data-stu-id="386af-139">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="386af-140">如需詳細資訊，請參閱<xref:samesite/kbs-samesite>。</span><span class="sxs-lookup"><span data-stu-id="386af-140">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="386af-141">SameSite 規格的2019草稿：</span><span class="sxs-lookup"><span data-stu-id="386af-141">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="386af-142">與2016草稿**不**相容。</span><span class="sxs-lookup"><span data-stu-id="386af-142">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="386af-143">如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="386af-143">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="386af-144">指定預設會將 cookie 視為 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="386af-144">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="386af-145">指定明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie，也應該標示為 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="386af-145">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="386af-146">發行的修補程式支援，如上述 KB 所述。</span><span class="sxs-lookup"><span data-stu-id="386af-146">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="386af-147">排定預設會在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)由 [Chrome](https://chromestatus.com/feature/5088147346030592) 啟用。</span><span class="sxs-lookup"><span data-stu-id="386af-147">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="386af-148">瀏覽器已開始移至2019中的此標準。</span><span class="sxs-lookup"><span data-stu-id="386af-148">Browsers started moving to this standard in 2019.</span></span>

<a name="known"><a/>

## <a name="known-issues"></a><span data-ttu-id="386af-149">已知問題</span><span class="sxs-lookup"><span data-stu-id="386af-149">Known Issues</span></span>

<span data-ttu-id="386af-150">由於2016和2019草稿規格不相容，因此 11 2019 月的 .Net Framework 更新會引進一些可能中斷的變更。</span><span class="sxs-lookup"><span data-stu-id="386af-150">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="386af-151">會話狀態和表單驗證 cookie 現在會以 `Lax` 的方式寫入網路，而不是未指定。</span><span class="sxs-lookup"><span data-stu-id="386af-151">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="386af-152">雖然大部分的應用程式都能使用 `SameSite=Lax` cookie，但在使用 `iframe` 的網站或應用程式之間張貼的應用程式，可能會發現其會話狀態或表單驗證 cookie 未如預期般使用。</span><span class="sxs-lookup"><span data-stu-id="386af-152">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="386af-153">若要解決此問題，請變更先前所討論之適當設定區段中的 `cookieSameSite` 值。</span><span class="sxs-lookup"><span data-stu-id="386af-153">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="386af-154">在程式碼或設定中明確設定 `SameSite=None` 的 HttpCookies 現在具有以 cookie 撰寫的值，而先前已省略。</span><span class="sxs-lookup"><span data-stu-id="386af-154">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="386af-155">這可能會導致舊版瀏覽器的問題僅支援2016草稿標準。</span><span class="sxs-lookup"><span data-stu-id="386af-155">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="386af-156">以 `SameSite=None` cookie 支援2019草稿標準的瀏覽器為目標時，請記得也 `Secure` 將它們標示為，否則可能無法辨識。</span><span class="sxs-lookup"><span data-stu-id="386af-156">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="386af-157">若要還原為不 `SameSite=None`寫入的2016行為，請使用應用程式設定 `aspnet:SupressSameSiteNone=true`。</span><span class="sxs-lookup"><span data-stu-id="386af-157">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="386af-158">請注意，這會套用到應用程式中的所有 HttpCookies。</span><span class="sxs-lookup"><span data-stu-id="386af-158">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="386af-159">Azure App Service-SameSite cookie 處理</span><span class="sxs-lookup"><span data-stu-id="386af-159">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="386af-160">如需有關 Azure App Service 如何在 .Net 4.7.2 應用程式中設定 SameSite 行為的詳細資訊，請參閱[Azure App Service-SameSite cookie 處理和 .NET Framework 4.7.2 修補程式](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)。</span><span class="sxs-lookup"><span data-stu-id="386af-160">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="386af-161">支援舊版瀏覽器</span><span class="sxs-lookup"><span data-stu-id="386af-161">Supporting older browsers</span></span>

<span data-ttu-id="386af-162">2016 SameSite 標準規定必須將未知的值視為 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="386af-162">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="386af-163">從支援 2016 SameSite standard 的舊版瀏覽器存取的應用程式，可能會在取得值為 `None`的 SameSite 屬性時中斷。</span><span class="sxs-lookup"><span data-stu-id="386af-163">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="386af-164">如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。</span><span class="sxs-lookup"><span data-stu-id="386af-164">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="386af-165">ASP.NET 不會實作為瀏覽器偵測，因為使用者代理程式的值會高度變動並經常變更。</span><span class="sxs-lookup"><span data-stu-id="386af-165">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="386af-166">可以在 <xref:HTTP.HttpCookie> 呼叫位置呼叫下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="386af-166">The following code can be called at the <xref:HTTP.HttpCookie> call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="386af-167">在上述範例中，`MyUserAgentDetectionLib.DisallowsSameSiteNone` 是使用者提供的程式庫，可偵測使用者代理程式是否不支援 SameSite `None`。</span><span class="sxs-lookup"><span data-stu-id="386af-167">In the preceding sample, `MyUserAgentDetectionLib.DisallowsSameSiteNone` is a user supplied library that detects if the user agent doesn't support SameSite `None`.</span></span> <span data-ttu-id="386af-168">下列程式碼顯示範例 `DisallowsSameSiteNone` 方法：</span><span class="sxs-lookup"><span data-stu-id="386af-168">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="386af-169">下列程式碼僅供示範之用：</span><span class="sxs-lookup"><span data-stu-id="386af-169">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="386af-170">不應該將它視為已完成。</span><span class="sxs-lookup"><span data-stu-id="386af-170">It should not be considered complete.</span></span>
> * <span data-ttu-id="386af-171">不會維護或支援。</span><span class="sxs-lookup"><span data-stu-id="386af-171">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="386af-172">測試應用程式的 SameSite 問題</span><span class="sxs-lookup"><span data-stu-id="386af-172">Test apps for SameSite problems</span></span>

<span data-ttu-id="386af-173">與遠端網站（例如透過協力廠商登入）互動的應用程式需要：</span><span class="sxs-lookup"><span data-stu-id="386af-173">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="386af-174">測試多個瀏覽器的互動。</span><span class="sxs-lookup"><span data-stu-id="386af-174">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="386af-175">套用本檔中討論的[瀏覽器偵測和緩和措施](#sob)。</span><span class="sxs-lookup"><span data-stu-id="386af-175">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="386af-176">使用可選擇新 SameSite 行為的用戶端版本來測試 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="386af-176">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="386af-177">Chrome、Firefox 和 Chromium Edge 全都具有可用於測試的新加入宣告功能旗標。</span><span class="sxs-lookup"><span data-stu-id="386af-177">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="386af-178">在您的應用程式套用 SameSite 修補程式之後，請使用較舊的用戶端版本（尤其是 Safari）進行測試。</span><span class="sxs-lookup"><span data-stu-id="386af-178">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="386af-179">如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="386af-179">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="386af-180">使用 Chrome 進行測試</span><span class="sxs-lookup"><span data-stu-id="386af-180">Test with Chrome</span></span>

<span data-ttu-id="386af-181">Chrome 78 + 會提供誤導的結果，因為它有暫時的緩和措施。</span><span class="sxs-lookup"><span data-stu-id="386af-181">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="386af-182">Chrome 78 + 暫時緩和可讓 cookie 少於兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="386af-182">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="386af-183">已啟用適當測試旗標的 Chrome 76 或77提供更精確的結果。</span><span class="sxs-lookup"><span data-stu-id="386af-183">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="386af-184">若要測試新的 SameSite 行為，請切換 `chrome://flags/#same-site-by-default-cookies` 為 [**已啟用**]。</span><span class="sxs-lookup"><span data-stu-id="386af-184">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="386af-185">舊版 Chrome （75和更低版本）會回報為失敗，並出現新的 `None` 設定。</span><span class="sxs-lookup"><span data-stu-id="386af-185">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="386af-186">請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="386af-186">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="386af-187">Google 不會提供舊版的 chrome 版本。</span><span class="sxs-lookup"><span data-stu-id="386af-187">Google does not make older chrome versions available.</span></span> <span data-ttu-id="386af-188">請遵循[下載 Chromium](https://www.chromium.org/getting-involved/download-chromium)的指示來測試舊版 Chrome。</span><span class="sxs-lookup"><span data-stu-id="386af-188">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="386af-189">請勿從搜尋舊版 chrome 所提供的**連結下載 Chrome** 。</span><span class="sxs-lookup"><span data-stu-id="386af-189">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="386af-190">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="386af-190">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="386af-191">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="386af-191">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="386af-192">使用 Safari 進行測試</span><span class="sxs-lookup"><span data-stu-id="386af-192">Test with Safari</span></span>

<span data-ttu-id="386af-193">Safari 12 會嚴格實作為先前的草稿，並在新的 `None` 值在 cookie 中失敗。</span><span class="sxs-lookup"><span data-stu-id="386af-193">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="386af-194">透過此檔中[支援較舊流覽](#sob)器的瀏覽器偵測程式碼，可避免 `None`。</span><span class="sxs-lookup"><span data-stu-id="386af-194">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="386af-195">使用 MSAL、ADAL 或您使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。</span><span class="sxs-lookup"><span data-stu-id="386af-195">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="386af-196">問題取決於基礎作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="386af-196">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="386af-197">OSX Mojave （10.14）和 iOS 12 已知具有新 SameSite 行為的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="386af-197">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="386af-198">將 OS 升級至 OSX Catalina （10.15）或 iOS 13 會修正問題。</span><span class="sxs-lookup"><span data-stu-id="386af-198">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="386af-199">Safari 目前沒有加入宣告旗標來測試新的規格行為。</span><span class="sxs-lookup"><span data-stu-id="386af-199">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="386af-200">使用 Firefox 進行測試</span><span class="sxs-lookup"><span data-stu-id="386af-200">Test with Firefox</span></span>

<span data-ttu-id="386af-201">在 [`about:config`] 頁面上選擇 [`network.cookie.sameSite.laxByDefault`] 功能旗標，即可在版本 68 + 上測試新標準的 Firefox 支援。</span><span class="sxs-lookup"><span data-stu-id="386af-201">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="386af-202">尚未報告舊版 Firefox 的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="386af-202">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="386af-203">使用 Edge 瀏覽器進行測試</span><span class="sxs-lookup"><span data-stu-id="386af-203">Test with Edge browser</span></span>

<span data-ttu-id="386af-204">Edge 支援舊的 SameSite 標準。</span><span class="sxs-lookup"><span data-stu-id="386af-204">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="386af-205">Edge 版本44沒有任何已知的新標準相容性問題。</span><span class="sxs-lookup"><span data-stu-id="386af-205">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="386af-206">使用 Edge 進行測試（Chromium）</span><span class="sxs-lookup"><span data-stu-id="386af-206">Test with Edge (Chromium)</span></span>

<span data-ttu-id="386af-207">在 [`edge://flags/#same-site-by-default-cookies`] 頁面上設定 SameSite 旗標。</span><span class="sxs-lookup"><span data-stu-id="386af-207">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="386af-208">Edge Chromium 未發現相容性問題。</span><span class="sxs-lookup"><span data-stu-id="386af-208">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="386af-209">使用 Electron 進行測試</span><span class="sxs-lookup"><span data-stu-id="386af-209">Test with Electron</span></span>

<span data-ttu-id="386af-210">Electron 的版本包含舊版的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="386af-210">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="386af-211">例如，小組所使用的 Electron 版本是 Chromium 66，這會展現較舊的行為。</span><span class="sxs-lookup"><span data-stu-id="386af-211">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="386af-212">您必須使用您的產品所使用的 Electron 版本來執行自己的相容性測試。</span><span class="sxs-lookup"><span data-stu-id="386af-212">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="386af-213">請參閱下一節中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="386af-213">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="386af-214">其他資源</span><span class="sxs-lookup"><span data-stu-id="386af-214">Additional resources</span></span>

* [<span data-ttu-id="386af-215">ASP.NET 和 ASP.NET Core 即將推出的 SameSite Cookie 變更</span><span class="sxs-lookup"><span data-stu-id="386af-215">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="386af-216">Chromium Blog：開發人員：準備開始新的 SameSite = None;安全 Cookie 設定</span><span class="sxs-lookup"><span data-stu-id="386af-216">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="386af-217">SameSite cookie 說明</span><span class="sxs-lookup"><span data-stu-id="386af-217">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
