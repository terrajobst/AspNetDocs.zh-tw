---
title: 使用 SameSite cookie 和 Open Web Interface for .NET （OWIN）
author: rick-anderson
description: 使用 SameSite cookie 和 Open Web Interface for .NET （OWIN）
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: a3353fd0f0332899aaba26b83aea0ff7c3a6d19b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455733"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a>SameSite cookie 和 Open Web Interface for .NET （OWIN）

由 [Rick Anderson](https://twitter.com/RickAndMSFT) 提供

`SameSite` 是針對跨網站偽造要求（CSRF）攻擊提供一些保護的[IETF](https://ietf.org/about/)草稿。 [SameSite 2019 草稿](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)：

* 預設會將 cookie 視為 `SameSite=Lax`。
* 說明明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie 應標示為 `Secure`。

`Lax` 適用于大部分的應用程式 cookie。 某些形式的驗證，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[WS-同盟](https://auth0.com/docs/protocols/ws-fed)，預設為以 POST 為基礎的重新導向。 以 POST 為基礎的重新導向會觸發 `SameSite` 的瀏覽器保護，因此已停用這些元件的 `SameSite`。 大部分的[OAuth](https://oauth.net/)登入不會受到影響，因為要求的流動方式不同。 根據預設，所有其他元件都**不會**設定 `SameSite`，並使用用戶端預設行為（舊的或新的）。

`None` 參數會導致用戶端的相容性問題，而此標準會實作為先前的[2016 草稿標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)（例如 iOS 12）。 請參閱本檔中的[支援舊版瀏覽器](#sob)。

每個發出 cookie 的 OWIN 元件都必須決定 `SameSite` 是否適當。

如需本文的 ASP.NET 4.x 版本，請參閱 <xref:samesite/system-web-samesite>。

## <a name="api-usage-with-samesite"></a>使用 SameSite 的 API 使用方式

`Microsoft.Owin` 有自己的 `SameSite` 執行：

* 這不會直接相依于 `System.Web`中的。
* `SameSite` 適用于 `Microsoft.Owin` 封裝（.NET 4.5 和更新版本）所目標設為的所有版本。
* 只有[SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)元件會直接與 `System.Web` `HttpCookie` 類別互動。

`SystemWebCookieManager` 取決於 .NET 4.7.2 `System.Web` Api，以啟用 `SameSite` 支援，以及變更行為的修補程式。

[OWIN 和 system.web 回應 cookie 整合問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)中概述了使用 `SystemWebCookieManager` 的原因。 在 `System.Web`上執行時，建議 `SystemWebCookieManager`。

下列程式碼會將 `SameSite` 設定為 `Lax`：

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

下列 Api 會使用 `SameSite`：

* [Owin. SameSiteMode](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [Cookieoptions.secure. SameSite](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* [Cookieauthenticationoptions.authenticationtype 類別](/previous-versions/aspnet/dn385599(v%3Dvs.113)) <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [Cookieauthenticationoptions.authenticationtype. CookieSameSite](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))
* [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [SystemWebChunkingCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [Cookieauthenticationoptions.authenticationtype. CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [OpenIdConnectAuthenticationOptions. CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a>歷程記錄和變更

[Owin](https://www.nuget.org/packages/Microsoft.Owin/)不支援[`SameSite` 2016 草案標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)。

只有 `Microsoft.Owin` 4.1.0 和更新版本才提供對[SameSite 2019 草稿](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)的支援。 先前版本沒有修補程式。

`SameSite` 規格的2019草稿：

* 與2016草稿**不**相容。 如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。
* 指定預設會將 cookie 視為 `SameSite=Lax`。
* 指定明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie，應該標示為 `Secure`。 `None` 是退出宣告的新專案。
* 排定預設會在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)由 [Chrome](https://chromestatus.com/feature/5088147346030592) 啟用。 瀏覽器已開始移至2019中的此標準。
* 發行的修補程式支援，如知識庫文章所述。 如需詳細資訊，請參閱<xref:samesite/kbs-samesite>。

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>支援舊版瀏覽器

2016 `SameSite` 標準規定必須將未知的值視為 `SameSite=Strict` 值。 從支援 2016 `SameSite` standard 的舊版瀏覽器存取的應用程式，可能會在取得值為 `None`的 `SameSite` 屬性時中斷。 如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。 ASP.NET 不會實作為瀏覽器偵測，因為使用者代理程式的值會高度變動並經常變更。 [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))中的擴充點允許插入使用者代理程式特定的邏輯。
<!-- https://docs.microsoft.com/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

在 `Startup.Configuration`中，新增類似下列的程式碼：

[!code-csharp[](sample/Startup1.cs?name=snippet)]

上述程式碼需要 .NET 4.7.2 或更新版本 `SameSite` patch。

下列程式碼顯示 `SameSiteCookieManager`的範例執行：

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

在上述範例中，會在 `CheckSameSite` 方法中呼叫 `DisallowsSameSiteNone`。 `DisallowsSameSiteNone` 是一個使用者方法，它會偵測使用者代理程式是否不支援 `SameSite` `None`：

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

下列程式碼顯示範例 `DisallowsSameSiteNone` 方法：

> [!WARNING]
> 下列程式碼僅供示範之用：
> * 不應該將它視為已完成。
> * 不會維護或支援。

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>測試應用程式的 SameSite 問題

與遠端網站（例如透過協力廠商登入）互動的應用程式需要：

* 測試多個瀏覽器的互動。
* 套用本檔中討論的[瀏覽器偵測和緩和措施](#sob)。

使用可選擇新的 `SameSite` 行為的用戶端版本來測試 web 應用程式。 Chrome、Firefox 和 Chromium Edge 全都具有可用於測試的新加入宣告功能旗標。 在您的應用程式套用 `SameSite` 修補程式之後，請使用較舊的用戶端版本（尤其是 Safari）進行測試。 如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。

### <a name="test-with-chrome"></a>使用 Chrome 進行測試

Chrome 78 + 會提供誤導的結果，因為它有暫時的緩和措施。 Chrome 78 + 暫時緩和可讓 cookie 少於兩分鐘。 已啟用適當測試旗標的 Chrome 76 或77提供更精確的結果。 若要測試新的 `SameSite` 行為，請將 `chrome://flags/#same-site-by-default-cookies` 切換為 [**啟用**]。 舊版 Chrome （75和更低版本）會回報為失敗，並出現新的 `None` 設定。 請參閱本檔中的[支援舊版瀏覽器](#sob)。

Google 不會提供舊版的 chrome 版本。 請遵循[下載 Chromium](https://www.chromium.org/getting-involved/download-chromium)的指示來測試舊版 Chrome。 請勿從搜尋舊版 chrome 所提供的**連結下載 Chrome** 。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>使用 Safari 進行測試

Safari 12 會嚴格實作為先前的草稿，並在新的 `None` 值在 cookie 中失敗。 透過此檔中[支援較舊流覽](#sob)器的瀏覽器偵測程式碼，可避免 `None`。 使用 MSAL、ADAL 或您使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。 問題取決於基礎作業系統版本。 OSX Mojave （10.14）和 iOS 12 已知有新 `SameSite` 行為的相容性問題。 將 OS 升級至 OSX Catalina （10.15）或 iOS 13 會修正問題。 Safari 目前沒有加入宣告旗標來測試新的規格行為。

### <a name="test-with-firefox"></a>使用 Firefox 進行測試

在 [`about:config`] 頁面上選擇 [`network.cookie.sameSite.laxByDefault`] 功能旗標，即可在版本 68 + 上測試新標準的 Firefox 支援。 尚未報告舊版 Firefox 的相容性問題。

### <a name="test-with-edge-browser"></a>使用 Edge 瀏覽器進行測試

Edge 支援舊的 `SameSite` 標準。 Edge 版本44沒有任何已知的新標準相容性問題。

### <a name="test-with-edge-chromium"></a>使用 Edge 進行測試（Chromium）

`SameSite` 旗標是設定在 [`edge://flags/#same-site-by-default-cookies`] 頁面上。 Edge Chromium 未發現相容性問題。

### <a name="test-with-electron"></a>使用 Electron 進行測試

Electron 的版本包含舊版的 Chromium。 例如，小組所使用的 Electron 版本是 Chromium 66，這會展現較舊的行為。 您必須使用您的產品所使用的 Electron 版本來執行自己的相容性測試。 請參閱下一節中的[支援舊版瀏覽器](#sob)。

## <a name="additional-resources"></a>其他資源

* [Chromium Blog：開發人員：準備開始新的 SameSite = None;安全的 Cookie 設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie 說明](https://web.dev/samesite-cookies-explained/)
* [OWIN 和 System.web 回應 cookie 整合問題](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
