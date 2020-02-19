---
title: ASP.NET 4.7.2 C# MVC 的 SameSite cookie 範例
author: blowdart
description: ASP.NET 4.7.2 C# MVC 的 SameSite cookie 範例
ms.author: riande
ms.date: 2/15/2019
uid: samesite/csMVC
ms.openlocfilehash: dcbd0bee009669fb747d74e6ccef07fbae70a236
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458452"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-mvc"></a><span data-ttu-id="3d5d5-103">ASP.NET 4.7.2 C# MVC 的 SameSite cookie 範例</span><span class="sxs-lookup"><span data-stu-id="3d5d5-103">SameSite cookie sample for ASP.NET 4.7.2 C# MVC</span></span>

<span data-ttu-id="3d5d5-104">.NET Framework 4.7 具有[SameSite](https://www.owasp.org/index.php/SameSite)屬性的內建支援，但符合原始標準。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="3d5d5-105">已修補的行為已變更 `SameSite.None` 的意義，以 `None`的值發出屬性，而不是完全發出值。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="3d5d5-106">如果您不想要發出值，可以將 cookie 上的 `SameSite` 屬性設定為-1。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="3d5d5-107">撰寫 SameSite 屬性</span><span class="sxs-lookup"><span data-stu-id="3d5d5-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="3d5d5-108">以下是如何在 cookie 上撰寫 SameSite 屬性的範例。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookieSite none.
// Note this will also require you to be running on HTTPS
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for Same
sameSiteCookie.Secure = true;

// Set the cookie to HTTP only which is good practice unless you really do need
// to access it client side in scripts.
sameSiteCookie.HttpOnly = true;

// Add the SameSite attribute, this will emit the attribute with a value of none.
// To not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None;

// Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie);
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="3d5d5-109">會話狀態的預設 sameSite 屬性會在的會話設定的 ' cookieSameSite ' 參數中設定 `web.config`</span><span class="sxs-lookup"><span data-stu-id="3d5d5-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="3d5d5-110">MVC 驗證</span><span class="sxs-lookup"><span data-stu-id="3d5d5-110">MVC Authentication</span></span>

<span data-ttu-id="3d5d5-111">OWIN 以 MVC cookie 為基礎的驗證會使用 cookie 管理員來啟用 cookie 屬性的變更。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="3d5d5-112">[SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs)是這類類別的執行，您可以將其複製到您自己的專案中。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-112">The [SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="3d5d5-113">您必須確定您的 Owin 元件全都升級為4.1.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="3d5d5-114">請檢查您的 `packages.config` 檔案，以確保所有版本號碼都相符，例如。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="3d5d5-115">接著，必須將驗證元件設定為使用啟動類別中的 CookieManager;</span><span class="sxs-lookup"><span data-stu-id="3d5d5-115">The authentication components must then be configured to use the CookieManager in your startup class;</span></span>

```c#
public void Configuration(IAppBuilder app)
{
    app.UseCookieAuthentication(new CookieAuthenticationOptions
    {
        CookieSameSite = SameSiteMode.None,
        CookieHttpOnly = true,
        CookieSecure = CookieSecureOption.Always,
        CookieManager = new SameSiteCookieManager(new SystemWebCookieManager())
    });
}
```

<span data-ttu-id="3d5d5-116">您必須在支援的*每個*元件上設定 cookie 管理員，其中包括 CookieAuthentication 和 OpenIdConnectAuthentication。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="3d5d5-117">SystemWebCookieManager 是用來避免回應 cookie 整合的[已知問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="3d5d5-118">執行範例</span><span class="sxs-lookup"><span data-stu-id="3d5d5-118">Running the sample</span></span>

<span data-ttu-id="3d5d5-119">如果您執行範例專案，請在初始頁面上載入瀏覽器偵錯工具，並使用它來查看網站的 cookie 集合。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-119">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="3d5d5-120">若要在 Edge 和 Chrome 中執行此操作，請按 `F12` 然後選取 [`Application`] 索引標籤，然後按一下 [`Storage`] 區段中 [`Cookies`] 選項底下的網站 URL。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![瀏覽器偵錯工具 Cookie 清單](sample/img/BrowserDebugger.png)

<span data-ttu-id="3d5d5-122">當您按一下 [建立 Cookie] 按鈕的 SameSite 屬性值為 `Lax`，且符合[範例程式碼](#sampleCode)中所設定的值時，您可以從上圖中看到範例所建立的 cookie。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-122">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="3d5d5-123">攔截您未控制的 cookie</span><span class="sxs-lookup"><span data-stu-id="3d5d5-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="3d5d5-124">.NET 4.5.2 引進了新的事件來攔截標頭的寫入，`Response.AddOnSendingHeaders`。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="3d5d5-125">這可以用來攔截 cookie，然後再傳回給用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="3d5d5-126">在範例中，我們會將事件連接到靜態方法，以檢查瀏覽器是否支援新的 sameSite 變更，如果沒有，則會將 cookie 變更為如果已設定新的 `None` 值，則不會發出屬性。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="3d5d5-127">請參閱[global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) ，以取得連結事件和[SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs)的範例，以取得處理事件和調整 cookie `sameSite` 屬性的範例，而您可以將它複製到您自己的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```c#
public static void FilterSameSiteNoneForIncompatibleUserAgents(object sender)
{
    HttpApplication application = sender as HttpApplication;
    if (application != null)
    {
        var userAgent = application.Context.Request.UserAgent;
        if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
        {
            HttpContext.Current.Response.AddOnSendingHeaders(context =>
            {
                var cookies = context.Response.Cookies;
                for (var i = 0; i < cookies.Count; i++)
                {
                    var cookie = cookies[i];
                    if (cookie.SameSite == SameSiteMode.None)
                    {
                        cookie.SameSite = (SameSiteMode)(-1); // Unspecified
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="3d5d5-128">您可以用非常相同的方式變更特定的已命名 cookie 行為;下列範例會將預設驗證 cookie 從 `Lax` 調整為支援 `None` 值的瀏覽器 `None`，或移除不支援 `None`之瀏覽器上的 sameSite 屬性。</span><span class="sxs-lookup"><span data-stu-id="3d5d5-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```c#
public static void AdjustSpecificCookieSettings()
{
    HttpContext.Current.Response.AddOnSendingHeaders(context =>
    {
        var cookies = context.Response.Cookies;
        for (var i = 0; i < cookies.Count; i++)
        {
            var cookie = cookies[i]; 
            // Forms auth: ".ASPXAUTH"
            // Session: "ASP.NET_SessionId"
            if (string.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal))
            { 
                if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
                {
                    cookie.SameSite = -1;
                }
                else
                {
                    cookie.SameSite = SameSiteMode.None;
                }
                cookie.Secure = true;
            }
        }
    });
}
```

### <a name="more-information"></a><span data-ttu-id="3d5d5-129">相關資訊</span><span class="sxs-lookup"><span data-stu-id="3d5d5-129">More Information</span></span>
 
[<span data-ttu-id="3d5d5-130">Chrome 更新</span><span class="sxs-lookup"><span data-stu-id="3d5d5-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="3d5d5-131">OWIN SameSite 檔</span><span class="sxs-lookup"><span data-stu-id="3d5d5-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="3d5d5-132">ASP.NET 檔</span><span class="sxs-lookup"><span data-stu-id="3d5d5-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="3d5d5-133">.NET SameSite 修補程式</span><span class="sxs-lookup"><span data-stu-id="3d5d5-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)