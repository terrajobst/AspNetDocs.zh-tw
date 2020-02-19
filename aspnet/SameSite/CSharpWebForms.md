---
title: 適用于 ASP.NET 4.7.2 C# WebForms 的 SameSite cookie 範例
author: blowdart
description: 適用于 ASP.NET 4.7.2 C# WebForms 的 SameSite cookie 範例
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458480"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a><span data-ttu-id="32a61-103">適用于 ASP.NET 4.7.2 C# WebForms 的 SameSite cookie 範例</span><span class="sxs-lookup"><span data-stu-id="32a61-103">SameSite cookie sample for ASP.NET 4.7.2 C# WebForms</span></span>

<span data-ttu-id="32a61-104">.NET Framework 4.7 具有[SameSite](https://www.owasp.org/index.php/SameSite)屬性的內建支援，但符合原始標準。</span><span class="sxs-lookup"><span data-stu-id="32a61-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="32a61-105">已修補的行為已變更 `SameSite.None` 的意義，以 `None`的值發出屬性，而不是完全發出值。</span><span class="sxs-lookup"><span data-stu-id="32a61-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="32a61-106">如果您不想要發出值，可以將 cookie 上的 `SameSite` 屬性設定為-1。</span><span class="sxs-lookup"><span data-stu-id="32a61-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="32a61-107">撰寫 SameSite 屬性</span><span class="sxs-lookup"><span data-stu-id="32a61-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="32a61-108">以下是如何在 cookie 上撰寫 SameSite 屬性的範例。</span><span class="sxs-lookup"><span data-stu-id="32a61-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookie
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for SameSite none.
// Note this will also require you to be running on HTTPS
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

<span data-ttu-id="32a61-109">表單驗證 cookie 的預設 sameSite 屬性會在的表單驗證設定的 `cookieSameSite` 參數中設定 `web.config`</span><span class="sxs-lookup"><span data-stu-id="32a61-109">The default sameSite attribute for a forms authentication cookie is set in the `cookieSameSite` parameter of the forms authentication settings in `web.config`</span></span> 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

<span data-ttu-id="32a61-110">會話狀態的預設 sameSite 屬性也會在中會話設定的 ' cookieSameSite ' 參數中設定 `web.config`</span><span class="sxs-lookup"><span data-stu-id="32a61-110">The default sameSite attribute for session state is also set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

<span data-ttu-id="32a61-111">.NET 11 月的2019更新會將表單驗證和會話的預設設定變更為 `lax`，因為這是最相容的設定，不過，如果您將頁面內嵌至 iframe，則可能需要將此設定還原為 [無]，然後新增如下所示的[攔截](#interception)程式碼，以根據瀏覽器功能來調整 `none` 行為。</span><span class="sxs-lookup"><span data-stu-id="32a61-111">The November 2019 update to .NET changed the default settings for Forms Authentication and Session to `lax` as is the most compatible setting, however if you embed pages into iframes you may need to revert this setting to None, and then add the [interception](#interception) code shown below to adjust the `none` behavior depending on browser capability.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="32a61-112">執行範例</span><span class="sxs-lookup"><span data-stu-id="32a61-112">Running the sample</span></span>

<span data-ttu-id="32a61-113">如果您執行範例專案，請在初始頁面上載入瀏覽器偵錯工具，並使用它來查看網站的 cookie 集合。</span><span class="sxs-lookup"><span data-stu-id="32a61-113">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="32a61-114">若要在 Edge 和 Chrome 中執行此操作，請按 `F12` 然後選取 [`Application`] 索引標籤，然後按一下 [`Storage`] 區段中 [`Cookies`] 選項底下的網站 URL。</span><span class="sxs-lookup"><span data-stu-id="32a61-114">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![瀏覽器偵錯工具 Cookie 清單](sample/img/BrowserDebugger.png)

<span data-ttu-id="32a61-116">當您按一下 [建立 Cookie] 按鈕的 SameSite 屬性值為 `Lax`，且符合[範例程式碼](#sampleCode)中所設定的值時，您可以從上圖中看到範例所建立的 cookie。</span><span class="sxs-lookup"><span data-stu-id="32a61-116">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="32a61-117">攔截您未控制的 cookie</span><span class="sxs-lookup"><span data-stu-id="32a61-117">Intercepting cookies you do not control</span></span>

<span data-ttu-id="32a61-118">.NET 4.5.2 引進了新的事件來攔截標頭的寫入，`Response.AddOnSendingHeaders`。</span><span class="sxs-lookup"><span data-stu-id="32a61-118">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="32a61-119">這可以用來攔截 cookie，然後再傳回給用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="32a61-119">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="32a61-120">在範例中，我們會將事件連接到靜態方法，以檢查瀏覽器是否支援新的 sameSite 變更，如果沒有，則會將 cookie 變更為如果已設定新的 `None` 值，則不會發出屬性。</span><span class="sxs-lookup"><span data-stu-id="32a61-120">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="32a61-121">請參閱[global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) ，以取得連結事件和[SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs)的範例，以取得處理事件和調整 cookie `sameSite` 屬性的範例。</span><span class="sxs-lookup"><span data-stu-id="32a61-121">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute.</span></span>

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

<span data-ttu-id="32a61-122">您可以用非常相同的方式變更特定的已命名 cookie 行為;下列範例會將預設驗證 cookie 從 `Lax` 調整為支援 `None` 值的瀏覽器 `None`，或移除不支援 `None`之瀏覽器上的 sameSite 屬性。</span><span class="sxs-lookup"><span data-stu-id="32a61-122">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

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

## <a name="more-information"></a><span data-ttu-id="32a61-123">相關資訊</span><span class="sxs-lookup"><span data-stu-id="32a61-123">More Information</span></span>

[<span data-ttu-id="32a61-124">Chrome 更新</span><span class="sxs-lookup"><span data-stu-id="32a61-124">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="32a61-125">ASP.NET 檔</span><span class="sxs-lookup"><span data-stu-id="32a61-125">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="32a61-126">.NET SameSite 修補程式</span><span class="sxs-lookup"><span data-stu-id="32a61-126">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)