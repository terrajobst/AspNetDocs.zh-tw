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
# <a name="work-with-samesite-cookies-in-aspnet"></a>在 ASP.NET 中使用 SameSite cookie

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite 是一種[IETF](https://ietf.org/about/)草稿標準，旨在針對跨網站偽造要求（CSRF）攻擊提供一些保護。 初稿標準已于[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)開始繪製，已于[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)更新。 更新的標準不會與前一個標準回溯相容，下列是最顯著的差異：

* 預設會將不含 SameSite 標頭的 cookie 視為 `SameSite=Lax`。
* `SameSite=None` 必須用來允許跨網站 cookie 的使用。
* 判斷提示 `SameSite=None` 的 cookie 也必須標示為 `Secure`。
* [2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允許值 SameSite = None，而是讓一些執行方式將這類 Cookie 視為 SameSite = Strict。 請參閱本檔中的[支援舊版瀏覽器](#sob)。

[`SameSite=Lax`] 設定適用于大部分的應用程式 cookie。 某些形式的驗證，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[WS-同盟](https://auth0.com/docs/protocols/ws-fed)，預設為以 POST 為基礎的重新導向。 以 POST 為基礎的重新導向會觸發 SameSite 瀏覽器保護，因此這些元件已停用 SameSite。 大部分的[OAuth](https://oauth.net/)登入都不會受到影響，因為要求的流動方式不同。

使用 `iframe` 的應用程式可能會遇到 `SameSite=Lax` 或 `SameSite=Strict` cookie 的問題，因為 iframe 會被視為跨網站案例。

發出 cookie 的每個 ASP.NET 元件都必須決定 SameSite 是否適當。

在安裝 2019 .Net SameSite 更新之後，請參閱應用程式問題的[已知問題](#known)。

## <a name="using-samesite-in-aspnet-472-and-48"></a>在 ASP.NET 4.7.2 和4.8 中使用 SameSite

.Net 4.7.2 和4.8 支援自12月2019的更新發行以來，SameSite 的[2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) 。 開發人員可以使用[HttpCookie. SameSite 屬性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)，以程式設計方式控制 SameSite 標頭的值。 將 `SameSite` 屬性設定為 `Strict`、`Lax` 或 `None` 會導致在網路上使用 cookie 寫入這些值。 將其設定為等於 `(SameSiteMode)(-1)` 表示不應在具有 cookie 的網路上包含任何 SameSite 標頭。 Config 檔案中的[HttpCookie 屬性](/dotnet/api/system.web.httpcookie.secure)或 ' requireSSL ' 可以用來將 cookie 標記為 `Secure`。

新的 `HttpCookie` 實例會預設為 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false`。 這些預設值可以在 `system.web/httpCookies` 設定區段中覆寫，其中字串 `"Unspecified"` 是適用于 `(SameSiteMode)(-1)`的易記僅限設定語法：

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net 也會針對這些功能發行自己的四個特定 cookie：匿名驗證、表單驗證、會話狀態和角色管理。 在執行時間取得的這些 cookie 實例，可以使用 `SameSite` 和 `Secure` 屬性來操作，就像任何其他 HttpCookie 實例一樣。 不過，由於 SameSite 標準的 patchwork 出現，因此這四個功能 cookie 的設定選項不一致。 相關的設定區段和屬性（含預設值）如下所示。 如果沒有 `SameSite` 或 `Secure` 功能的相關屬性，則此功能會切換回前面所討論的 [`system.web/httpCookies`] 區段中所設定的預設值。

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

**注意**： ' 未指定 ' 僅適用于目前 `system.web/httpCookies@sameSite`。 我們希望在未來的更新中，將類似的語法新增至先前顯示的 cookieSameSite 屬性。 在程式碼中設定 `(SameSiteMode)(-1)` 仍可在這些 cookie 的實例上運作。 *

## <a name="history-and-changes"></a>歷程記錄和變更

SameSite 支援首次使用[2016 draft 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)在 .net 4.7.2 中執行。

2019年11月19日的 Windows 更新，已將 .NET 4.7.2 + 從2016標準更新為2019標準。 其他版本的 Windows 即將推出其他更新。 如需詳細資訊，請參閱<xref:samesite/kbs-samesite>。

 SameSite 規格的2019草稿：

* 與2016草稿**不**相容。 如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。
* 指定預設會將 cookie 視為 `SameSite=Lax`。
* 指定明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie，也應該標示為 `Secure`。
* 發行的修補程式支援，如上述 KB 所述。
* 排定預設會在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)由 [Chrome](https://chromestatus.com/feature/5088147346030592) 啟用。 瀏覽器已開始移至2019中的此標準。

<a name="known"><a/>

## <a name="known-issues"></a>已知問題

由於2016和2019草稿規格不相容，因此 11 2019 月的 .Net Framework 更新會引進一些可能中斷的變更。

* 會話狀態和表單驗證 cookie 現在會以 `Lax` 的方式寫入網路，而不是未指定。
  * 雖然大部分的應用程式都能使用 `SameSite=Lax` cookie，但在使用 `iframe` 的網站或應用程式之間張貼的應用程式，可能會發現其會話狀態或表單驗證 cookie 未如預期般使用。 若要解決此問題，請變更先前所討論之適當設定區段中的 `cookieSameSite` 值。
* 在程式碼或設定中明確設定 `SameSite=None` 的 HttpCookies 現在具有以 cookie 撰寫的值，而先前已省略。 這可能會導致舊版瀏覽器的問題僅支援2016草稿標準。
  * 以 `SameSite=None` cookie 支援2019草稿標準的瀏覽器為目標時，請記得也 `Secure` 將它們標示為，否則可能無法辨識。
  * 若要還原為不 `SameSite=None`寫入的2016行為，請使用應用程式設定 `aspnet:SupressSameSiteNone=true`。 請注意，這會套用到應用程式中的所有 HttpCookies。

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service-SameSite cookie 處理

如需有關 Azure App Service 如何在 .Net 4.7.2 應用程式中設定 SameSite 行為的詳細資訊，請參閱[Azure App Service-SameSite cookie 處理和 .NET Framework 4.7.2 修補程式](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)。

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>支援舊版瀏覽器

2016 SameSite 標準規定必須將未知的值視為 `SameSite=Strict` 值。 從支援 2016 SameSite standard 的舊版瀏覽器存取的應用程式，可能會在取得值為 `None`的 SameSite 屬性時中斷。 如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。 ASP.NET 不會實作為瀏覽器偵測，因為使用者代理程式的值會高度變動並經常變更。 可以在 <xref:HTTP.HttpCookie> 呼叫位置呼叫下列程式碼：

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

在上述範例中，`MyUserAgentDetectionLib.DisallowsSameSiteNone` 是使用者提供的程式庫，可偵測使用者代理程式是否不支援 SameSite `None`。 下列程式碼顯示範例 `DisallowsSameSiteNone` 方法：

> [!WARNING]
> 下列程式碼僅供示範之用：
> * 不應該將它視為已完成。
> * 不會維護或支援。

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>測試應用程式的 SameSite 問題

與遠端網站（例如透過協力廠商登入）互動的應用程式需要：

* 測試多個瀏覽器的互動。
* 套用本檔中討論的[瀏覽器偵測和緩和措施](#sob)。

使用可選擇新 SameSite 行為的用戶端版本來測試 web 應用程式。 Chrome、Firefox 和 Chromium Edge 全都具有可用於測試的新加入宣告功能旗標。 在您的應用程式套用 SameSite 修補程式之後，請使用較舊的用戶端版本（尤其是 Safari）進行測試。 如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。

### <a name="test-with-chrome"></a>使用 Chrome 進行測試

Chrome 78 + 會提供誤導的結果，因為它有暫時的緩和措施。 Chrome 78 + 暫時緩和可讓 cookie 少於兩分鐘。 已啟用適當測試旗標的 Chrome 76 或77提供更精確的結果。 若要測試新的 SameSite 行為，請切換 `chrome://flags/#same-site-by-default-cookies` 為 [**已啟用**]。 舊版 Chrome （75和更低版本）會回報為失敗，並出現新的 `None` 設定。 請參閱本檔中的[支援舊版瀏覽器](#sob)。

Google 不會提供舊版的 chrome 版本。 請遵循[下載 Chromium](https://www.chromium.org/getting-involved/download-chromium)的指示來測試舊版 Chrome。 請勿從搜尋舊版 chrome 所提供的**連結下載 Chrome** 。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>使用 Safari 進行測試

Safari 12 會嚴格實作為先前的草稿，並在新的 `None` 值在 cookie 中失敗。 透過此檔中[支援較舊流覽](#sob)器的瀏覽器偵測程式碼，可避免 `None`。 使用 MSAL、ADAL 或您使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。 問題取決於基礎作業系統版本。 OSX Mojave （10.14）和 iOS 12 已知具有新 SameSite 行為的相容性問題。 將 OS 升級至 OSX Catalina （10.15）或 iOS 13 會修正問題。 Safari 目前沒有加入宣告旗標來測試新的規格行為。

### <a name="test-with-firefox"></a>使用 Firefox 進行測試

在 [`about:config`] 頁面上選擇 [`network.cookie.sameSite.laxByDefault`] 功能旗標，即可在版本 68 + 上測試新標準的 Firefox 支援。 尚未報告舊版 Firefox 的相容性問題。

### <a name="test-with-edge-browser"></a>使用 Edge 瀏覽器進行測試

Edge 支援舊的 SameSite 標準。 Edge 版本44沒有任何已知的新標準相容性問題。

### <a name="test-with-edge-chromium"></a>使用 Edge 進行測試（Chromium）

在 [`edge://flags/#same-site-by-default-cookies`] 頁面上設定 SameSite 旗標。 Edge Chromium 未發現相容性問題。

### <a name="test-with-electron"></a>使用 Electron 進行測試

Electron 的版本包含舊版的 Chromium。 例如，小組所使用的 Electron 版本是 Chromium 66，這會展現較舊的行為。 您必須使用您的產品所使用的 Electron 版本來執行自己的相容性測試。 請參閱下一節中的[支援舊版瀏覽器](#sob)。

## <a name="additional-resources"></a>其他資源

* [ASP.NET 和 ASP.NET Core 即將推出的 SameSite Cookie 變更](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromium Blog：開發人員：準備開始新的 SameSite = None;安全 Cookie 設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie 說明](https://web.dev/samesite-cookies-explained/)
