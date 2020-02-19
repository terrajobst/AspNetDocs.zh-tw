---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 瞭解如何在 ASP.NET 中使用 SameSite cookie
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: edb368910b24be2d042afe3c19ffa1fb23245443
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455697"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>在 ASP.NET 中使用 SameSite cookie

由 [Rick Anderson](https://twitter.com/RickAndMSFT) 提供

SameSite 是一種[IETF](https://ietf.org/about/)草稿標準，旨在針對跨網站偽造要求（CSRF）攻擊提供一些保護。 初稿標準已于[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)開始繪製，已于[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)更新。 更新的標準不會與前一個標準回溯相容，下列是最顯著的差異：

* 預設會將不含 SameSite 標頭的 cookie 視為 `SameSite=Lax`。
* `SameSite=None` 必須用來允許跨網站 cookie 的使用。
* 判斷提示 `SameSite=None` 的 cookie 也必須標示為 `Secure`。
* 使用[`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe)的應用程式可能會遇到 `sameSite=Lax` 或 `sameSite=Strict` cookie 的問題，因為 `<iframe>` 會被視為跨網站案例。
* [2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允許值 `SameSite=None`，而且會導致某些執行將這類 cookie 視為 `SameSite=Strict`。 請參閱本檔中的[支援舊版瀏覽器](#sob)。

[`SameSite=Lax`] 設定適用于大部分的應用程式 cookie。 某些形式的驗證，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[WS-同盟](https://auth0.com/docs/protocols/ws-fed)，預設為以 POST 為基礎的重新導向。 以 POST 為基礎的重新導向會觸發 SameSite 瀏覽器保護，因此這些元件已停用 SameSite。 大部分的[OAuth](https://oauth.net/)登入都不會受到影響，因為要求的流動方式不同。

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
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**注意**：「未指定」目前僅供 `system.web/httpCookies@sameSite` 使用。 我們希望在未來的更新中，將類似的語法新增至先前顯示的 cookieSameSite 屬性。 在程式碼中設定 `(SameSiteMode)(-1)` 仍可在這些 cookie 的實例上運作。 *

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>將 .NET 應用程式重定目標

若要以 .NET 4.7.2 或更新版本為目標：

* 確定*web.config*包含下列內容：  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  [.Net 遷移指南](/dotnet/framework/migration-guide/)有更多詳細資料。

* 確認專案中的 NuGet 套件是以正確的架構版本為目標。 您可以藉由檢查*封裝 .config*檔案來驗證正確的架構版本，例如：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  在上述的封裝 *.config*檔案中，`Microsoft.ApplicationInsights` 封裝：
    * 以 .NET 4.5.1 為目標。
    * 如果以架構目標為目標的更新套件存在，則應該將其 `targetFramework` 屬性更新為 `net472`。

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>早于4.7.2 的 .NET 版本

Microsoft 不支援較低的 .NET 版本來撰寫相同網站的 cookie 屬性（4.7.2）。 我們找不到可靠的方式來執行下列動作：

* 請確定已根據瀏覽器版本正確寫入屬性。
* 在較舊的 framework 版本上攔截並調整驗證和會話 cookie。

### <a name="december-patch-behavior-changes"></a>12月修補程式列為變更

.NET Framework 的特定行為變更是 `SameSite` 屬性解讀 `None` 值的方式：

* 修補之前的值 `None` 表示：
  * 完全不要發出屬性。
* 在修補程式之後：
  * `None`的值表示「發出屬性，其值為 `None`」。
  * `(SameSiteMode)(-1)` 的 `SameSite` 值會導致不發出屬性。

表單驗證和會話狀態 cookie 的預設 SameSite 值已從 `None` 變更為 `Lax`。

### <a name="summary-of-change-impact-on-browsers"></a>變更瀏覽器影響的摘要

如果您安裝修補程式並使用 `SameSite.None`發出 cookie，將會發生下列兩種情況之一：
* Chrome v80 會根據新的執行來處理此 cookie，而不會對 cookie 強制執行相同的網站限制。
* 任何尚未更新為支援新執行的瀏覽器都將遵循舊的執行。 舊的執行會顯示：
  * 如果您看到不了解的值，請忽略它並切換至嚴格相同的網站限制。

因此，應用程式會在 Chrome 中中斷，或在其他許多地方中斷。

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

2016 SameSite 標準規定必須將未知的值視為 `SameSite=Strict` 值。 從支援 2016 SameSite standard 的舊版瀏覽器存取的應用程式，可能會在取得值為 `None`的 SameSite 屬性時中斷。 如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。 ASP.NET 不會實作為瀏覽器偵測，因為使用者代理程式的值會高度變動並經常變更。

Microsoft 解決問題的方法是協助您執行瀏覽器偵測元件，以從 cookie 中去除 `sameSite=None` 屬性（如果已知瀏覽器不支援）。 Google 的建議是要發出雙重 cookie，一個使用新的屬性，另一個沒有屬性。 不過，我們認為 Google 的建議有限。 有些瀏覽器，特別是行動瀏覽器對於網站或功能變數名稱可以傳送的 cookie 數目有極小的限制。 傳送多個 cookie，特別是大型 cookie （例如驗證 cookie）可以非常快速地觸達行動瀏覽器的限制，導致難以診斷和修正的應用程式失敗。 此外，做為架構，協力廠商程式碼和元件的大型生態系統，可能不會更新為使用雙重 cookie 方法。

[此 GitHub 存放庫]()中的範例專案所使用的瀏覽器偵測程式碼包含在兩個檔案中

* [C#SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB SameSiteSupport .vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

這些偵測是我們所見到的最常見瀏覽器代理程式，可支援2016標準，且必須完全移除屬性。 它不是用來做為完整的執行方式：

* 您的應用程式可能會看到我們的測試網站沒有的瀏覽器。
* 您應該準備好視需要為您的環境新增偵測。

連接偵測的方式會根據您所使用的 .NET 版本和 web 架構而有所不同。 可以在 <xref:HTTP.HttpCookie> 呼叫位置呼叫下列程式碼：

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

請參閱下列 ASP.NET 4.7.2 SameSite cookie 主題：

* [C#MVC](xref:samesite/csMVC)
* [C#WebForms](xref:samesite/CSharpWebForms)
* [VB WebForms](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>確保您的網站重新導向至 HTTPS

針對 ASP.NET 4.x、WebForms 和 MVC， [IIS 的 URL 重寫](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)功能可以用來將所有要求重新導向至 HTTPS。 下列 XML 顯示範例規則：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

在[IIS URL 重寫](https://www.iis.net/downloads/microsoft/url-rewrite)的內部部署安裝中，可能需要安裝的選擇性功能。

## <a name="test-apps-for-samesite-problems"></a>測試應用程式的 SameSite 問題

您必須使用支援的瀏覽器來測試您的應用程式，並流覽牽涉到 cookie 的案例。 Cookie 案例通常牽涉到

* 登入表單
* 外部登入機制，例如 Facebook、Azure AD、OAuth 和 OIDC
* 接受來自其他網站之要求的頁面
* 應用程式中設計成要內嵌在 iframe 中的頁面

您應該檢查您的應用程式中已正確建立、保存和刪除 cookie。

與遠端網站（例如透過協力廠商登入）互動的應用程式需要：

* 測試多個瀏覽器的互動。
* 套用本檔中討論的[瀏覽器偵測和緩和措施](#sob)。

使用可選擇新 SameSite 行為的用戶端版本來測試 web 應用程式。 Chrome、Firefox 和 Chromium Edge 全都具有可用於測試的新加入宣告功能旗標。 在您的應用程式套用 SameSite 修補程式之後，請使用較舊的用戶端版本（尤其是 Safari）進行測試。 如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。

### <a name="test-with-chrome"></a>使用 Chrome 進行測試

Chrome 78 + 會提供誤導的結果，因為它有暫時的緩和措施。 Chrome 78 + 暫時緩和可讓 cookie 少於兩分鐘。 已啟用適當測試旗標的 Chrome 76 或77提供更精確的結果。 若要測試新的 SameSite 行為，請切換 `chrome://flags/#same-site-by-default-cookies` 為 [**已啟用**]。 舊版 Chrome （75和更低版本）會回報為失敗，並出現新的 `None` 設定。 請參閱本檔中的[支援舊版瀏覽器](#sob)。

Google 不會提供舊版的 chrome 版本。 請遵循[下載 Chromium](https://www.chromium.org/getting-involved/download-chromium)的指示來測試舊版 Chrome。 請勿從搜尋舊版 chrome 所提供的**連結下載 Chrome** 。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* 如果您不是使用64位版本的 Windows，您可以使用[OmahaProxy 檢視器](https://omahaproxy.appspot.com/)來尋找哪個 Chromium 分支與 Chrome 74 （v 74.0.3729.108）對應，使用[Chromium 所提供的指示](https://www.chromium.org/getting-involved/download-chromium)。

#### <a name="test-with-chrome-80"></a>使用 Chrome 80 + 進行測試

[下載](https://www.google.com/chrome/)支援其新屬性的 Chrome 版本。 在撰寫本文時，目前的版本是 Chrome 80。 Chrome 80 必須啟用旗標 `chrome://flags/#same-site-by-default-cookies`，才能使用新的行為。 您也應該啟用（`chrome://flags/#cookies-without-same-site-must-be-secure`），以針對未啟用 sameSite 屬性的 cookie 測試即將推出的行為。 Chrome 80 位於目標上，可讓交換器將沒有屬性的 cookie 視為 `SameSite=Lax`，雖然某些要求的時間寬限期較長。 若要停用計時寬限期 Chrome 80，可以使用下列命令列引數來啟動：

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80 在瀏覽器主控台中有關于遺失 sameSite 屬性的警告訊息。 使用 F12 開啟瀏覽器主控台。

### <a name="test-with-safari"></a>使用 Safari 進行測試

Safari 12 會嚴格實作為先前的草稿，並在新的 `None` 值在 cookie 中失敗。 透過此檔中[支援較舊流覽](#sob)器的瀏覽器偵測程式碼，可避免 `None`。 使用 MSAL、ADAL 或您使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。 問題取決於基礎作業系統版本。 OSX Mojave （10.14）和 iOS 12 已知具有新 SameSite 行為的相容性問題。 將 OS 升級至 OSX Catalina （10.15）或 iOS 13 會修正問題。 Safari 目前沒有加入宣告旗標來測試新的規格行為。

### <a name="test-with-firefox"></a>使用 Firefox 進行測試

在 [`about:config`] 頁面上選擇 [`network.cookie.sameSite.laxByDefault`] 功能旗標，即可在版本 68 + 上測試新標準的 Firefox 支援。 尚未報告舊版 Firefox 的相容性問題。

### <a name="test-with-edge-legacy-browser"></a>使用 Edge （舊版）瀏覽器進行測試

Edge 支援舊的 SameSite 標準。 Edge 版本 44 + 沒有任何已知的新標準相容性問題。

### <a name="test-with-edge-chromium"></a>使用 Edge 進行測試（Chromium）

在 [`edge://flags/#same-site-by-default-cookies`] 頁面上設定 SameSite 旗標。 Edge Chromium 未發現相容性問題。

### <a name="test-with-electron"></a>使用 Electron 進行測試

Electron 的版本包含舊版的 Chromium。 例如，小組所使用的 Electron 版本是 Chromium 66，這會展現較舊的行為。 您必須使用您的產品所使用的 Electron 版本來執行自己的相容性測試。 請參閱[支援舊版瀏覽器](#sob)。

## <a name="reverting-samesite-patches"></a>還原 SameSite 修補程式

您可以將 .NET Framework 應用程式中更新的 sameSite 行為還原成先前的行為，其中 `None`的值不會發出 sameSite 屬性，並還原驗證和會話 cookie，使其不會發出此值。 這應該視為*非常暫時性的修正*，因為 Chrome 變更會中斷任何外部 POST 要求，或使用支援標準變更的瀏覽器來驗證使用者。

### <a name="reverting-net-472-behavior"></a>還原 .NET 4.7.2 行為

更新*web.config*以包含下列設定：

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a>其他資源

* [ASP.NET 和 ASP.NET Core 即將推出的 SameSite Cookie 變更](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromium Blog：開發人員：準備開始新的 SameSite = None;安全的 Cookie 設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie 說明](https://web.dev/samesite-cookies-explained/)
* [Chrome 更新](https://www.chromium.org/updates/same-site)
* [.NET SameSite 修補程式](/aspnet/samesite/kbs-samesite)
* [Azure Web 應用程式相同的網站資訊](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Azure ActiveDirectory 相同的網站資訊](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
