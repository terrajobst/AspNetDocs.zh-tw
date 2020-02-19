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
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a>適用于 ASP.NET 4.7.2 C# WebForms 的 SameSite cookie 範例

.NET Framework 4.7 具有[SameSite](https://www.owasp.org/index.php/SameSite)屬性的內建支援，但符合原始標準。
已修補的行為已變更 `SameSite.None` 的意義，以 `None`的值發出屬性，而不是完全發出值。 如果您不想要發出值，可以將 cookie 上的 `SameSite` 屬性設定為-1。

## <a name="sampleCode"></a>撰寫 SameSite 屬性

以下是如何在 cookie 上撰寫 SameSite 屬性的範例。

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

表單驗證 cookie 的預設 sameSite 屬性會在的表單驗證設定的 `cookieSameSite` 參數中設定 `web.config` 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

會話狀態的預設 sameSite 屬性也會在中會話設定的 ' cookieSameSite ' 參數中設定 `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

.NET 11 月的2019更新會將表單驗證和會話的預設設定變更為 `lax`，因為這是最相容的設定，不過，如果您將頁面內嵌至 iframe，則可能需要將此設定還原為 [無]，然後新增如下所示的[攔截](#interception)程式碼，以根據瀏覽器功能來調整 `none` 行為。

### <a name="running-the-sample"></a>執行範例

如果您執行範例專案，請在初始頁面上載入瀏覽器偵錯工具，並使用它來查看網站的 cookie 集合。
若要在 Edge 和 Chrome 中執行此操作，請按 `F12` 然後選取 [`Application`] 索引標籤，然後按一下 [`Storage`] 區段中 [`Cookies`] 選項底下的網站 URL。

![瀏覽器偵錯工具 Cookie 清單](sample/img/BrowserDebugger.png)

當您按一下 [建立 Cookie] 按鈕的 SameSite 屬性值為 `Lax`，且符合[範例程式碼](#sampleCode)中所設定的值時，您可以從上圖中看到範例所建立的 cookie。

## <a name="interception"></a>攔截您未控制的 cookie

.NET 4.5.2 引進了新的事件來攔截標頭的寫入，`Response.AddOnSendingHeaders`。 這可以用來攔截 cookie，然後再傳回給用戶端電腦。 在範例中，我們會將事件連接到靜態方法，以檢查瀏覽器是否支援新的 sameSite 變更，如果沒有，則會將 cookie 變更為如果已設定新的 `None` 值，則不會發出屬性。

請參閱[global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) ，以取得連結事件和[SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs)的範例，以取得處理事件和調整 cookie `sameSite` 屬性的範例。

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

您可以用非常相同的方式變更特定的已命名 cookie 行為;下列範例會將預設驗證 cookie 從 `Lax` 調整為支援 `None` 值的瀏覽器 `None`，或移除不支援 `None`之瀏覽器上的 sameSite 屬性。

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

## <a name="more-information"></a>相關資訊

[Chrome 更新](https://www.chromium.org/updates/same-site)

[ASP.NET 檔](/aspnet/samesite/system-web-samesite)

[.NET SameSite 修補程式](/aspnet/samesite/kbs-samesite)