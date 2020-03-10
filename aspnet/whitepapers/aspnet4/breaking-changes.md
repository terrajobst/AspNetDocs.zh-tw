---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 重大變更 |Microsoft Docs
author: rick-anderson
description: 本檔說明 .NET Framework 版本4版本所做的變更，可能會影響使用建立的應用程式 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546246"
---
# <a name="aspnet-4-breaking-changes"></a>ASP.NET 4 重大變更

> 本檔說明 .NET Framework 版本4版本所做的變更，可能會影響使用舊版所建立的應用程式，包括 ASP.NET 4 Beta 1 和 Beta 2 版本。
> 
> [下載此白皮書](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>內容

[Web.config 檔案中的 ControlRenderingCompatibilityVersion 設定](#0.1__Toc256770141 "_Toc256770141")  
[ClientIDMode 變更](#0.1__Toc256770142 "_Toc256770142")  
[HtmlEncode 和 UrlEncode 現在會將單引號編碼](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET Page （.aspx）剖析器較嚴格](#0.1__Toc256770144 "_Toc256770144")  
[已更新瀏覽器定義檔案](#0.1__Toc256770145 "_Toc256770145")  
[從根 Web 設定檔案移除的 system.web. .dll](#0.1__Toc256770146 "_Toc256770146")  
[ASP.NET 要求驗證](#0.1__Toc256770147 "_Toc256770147")  
[預設雜湊演算法現已 HMACSHA256](#0.1__Toc256770148 "_Toc256770148")  
[與新的 ASP.NET 4 根設定相關的設定錯誤](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 4 子應用程式在 ASP.NET 2.0 或 ASP.NET 3.5 應用程式下無法啟動](#0.1__Toc256770150 "_Toc256770150")  
[ASP.NET 4 網站在安裝 SharePoint 的電腦上無法啟動](#0.1__Toc256770151 "_Toc256770151")  
[HttpRequest 的屬性不再包含 PathInfo 值](#0.1__Toc256770152 "_Toc256770152")  
[ASP.NET 2.0 應用程式可能會產生參考 eurl 的 HttpException 錯誤](#0.1__Toc256770153 "_Toc256770153")  
[事件處理常式可能不會在 IIS 7 或 IIS 7.5 整合模式的預設檔中引發](#0.1__Toc256770154 "_Toc256770154")  
[對 ASP.NET 代碼啟用安全性（CAS）實行的變更](#0.1__Toc256770155 "_Toc256770155")  
[MembershipUser 和 System.web. Security 命名空間中的其他類型已移動](#0.1__Toc256770156 "_Toc256770156")  
[輸出快取變更為不同的 \* HTTP 標頭](#0.1__Toc256770157 "_Toc256770157")  
[Passport 的安全性類型已過時](#0.1__Toc256770158 "_Toc256770158")  
[PopOutImageUrl 屬性無法轉譯 ASP.NET 4 中的影像](#0.1__Toc256770159 "_Toc256770159")  
[StaticPopOutImageUrl 和 Menu. DynamicPopOutImageUrl 無法在路徑包含反斜線時呈現影像](#0.1__Toc256770160 "_Toc256770160")  
[免責聲明](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Web.config 檔案中的 ControlRenderingCompatibilityVersion 設定

ASP.NET 控制項在 .NET Framework 第4版中已經過修改，可讓您更精確地指定它們呈現標記的方式。 在舊版的 .NET Framework 中，有些控制項發出的標記是您無法停用的。 根據預設，ASP.NET 4 不會再產生這種類型的標記。

如果您使用 Visual Studio 2010 從 ASP.NET 2.0 或 ASP.NET 3.5 升級您的應用程式，此工具會自動將設定新增至保留舊版轉譯的 `Web.config` 檔案。 不過，如果您將 IIS 中的應用程式集區變更成以.NET Framework 4 為目標來升級應用程式，則 ASP.NET 預設會使用新轉譯模式。 若要停用新的轉譯模式，請在 `Web.config` 檔案中新增下列設定：

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

新行為所帶入的主要呈現變更如下所示：

- **影像**和**ImageButton**控制項不再呈現 `border="0"` 屬性。
- 根據預設，衍生自它的**BaseValidator**類別和驗證控制項不會再轉譯紅色文字。
- **HtmlForm**控制項不會呈現**name**屬性。
- **資料表**控制項不再呈現 `border="0"` 屬性。
- 如果控制項的 [ **Enabled** ] 屬性設定為**false** （或從容器控制項繼承此設定），則不是針對使用者輸入（例如， **Label**控制項）所設計的控制項就不會再轉譯 `disabled="disabled"` 屬性。

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>ClientIDMode 變更

ASP.NET 4 中的**ClientIDMode**設定可讓您指定 ASP.NET 如何產生 HTML 元素的**id**屬性。 在舊版的 ASP.NET 中，預設行為相當於**ClientIDMode**的**autoid predictable**設定。 不過，預設設定現在是**可預測**的。

如果您使用 Visual Studio 2010 從 ASP.NET 2.0 或 ASP.NET 3.5 升級您的應用程式，此工具會自動將設定新增至 `Web.config` 檔案，以保留舊版 .NET Framework 的行為。 不過，如果您將 IIS 中的應用程式集區變更成以.NET Framework 4 為目標來升級應用程式，則 ASP.NET 預設會使用新模式。 若要停用新的用戶端識別碼模式，請在 `Web.config` 檔案中新增下列設定：

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>HtmlEncode 和 UrlEncode 現在會將單引號編碼

在 ASP.NET 4 中， **HTTPutility.htmlencode**和**HttpServerUtility**類別的**HtmlEncode**和**UrlEncode**方法已更新為將單引號字元（'）編碼，如下所示：

- **HtmlEncode**方法會將單引號的實例編碼為 '。
- **UrlEncode**方法會將單引號的實例編碼為 %27。

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET Page （.aspx）剖析器較嚴格

ASP.NET 網頁（`.aspx` 檔案）和使用者控制項（`.ascx` 檔案）的頁面剖析器在 ASP.NET 4 中更嚴格，而且將會拒絕無效標記的更多實例。 例如，下列兩個程式碼片段會在舊版的 ASP.NET 中成功剖析，但現在會在 ASP.NET 4 中引發剖析器錯誤。

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

請注意**HiddenField**標記結尾的無效分號。

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

請注意，在**CssClass**屬性中執行的未封閉**樣式**屬性。

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>已更新瀏覽器定義檔案

瀏覽器定義檔已更新成包含新增和已更新瀏覽器及裝置的資訊。 已移除 Netscape Navigator 這類較舊的瀏覽器和裝置，並已新增 Google Chrome 和 Apple iPhone 這類較新的瀏覽器和裝置。

如果您的應用程式包含繼承自其中一個已移除瀏覽器定義的自訂瀏覽器定義，則您會看到錯誤。 例如，如果 [`App_Browsers`] 資料夾包含繼承自 IE2 瀏覽器定義的瀏覽器定義，您將會收到下列設定錯誤訊息：

- 找不到識別碼為 ' IE2 ' 的瀏覽器或閘道元素。

> [!NOTE]
> **HttpBrowserCapabilities**物件（由頁面的 [**要求流覽**] 屬性公開）是由瀏覽器定義檔案所驅動。 因此，在 ASP.NET 4 中存取此物件的屬性所傳回的資訊，可能會與舊版 ASP.NET 中傳回的資訊不同。

您可以從下列資料夾複製瀏覽器定義檔案，以還原成舊的瀏覽器定義檔案：

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

將檔案複製到 ASP.NET 4 的對應 `\CONFIG\Browsers` 資料夾。 複製檔案之後，請執行 Aspnet\_regbrowsers 命令列工具。

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>從根 Web 設定檔案移除的 system.web. .dll

在舊版的 ASP.NET 中，在底下的**元件**區段中，根 `Web.config` 檔案中會包含 system.web. .dll 元件的參考。 為了改善效能，已移除此元件的參考。

ASP.NET 4 包含 system.servicemodel 元件，但它已被取代。 如果您想要使用 system.servicemodel 元件中的類型，請將此元件的參考新增至根 `Web.config` 檔案或應用程式 `Web.config` 檔案。 例如，如果您想要使用任何（已淘汰）的 ASP.NET mobile 控制項，則必須將 System.web 元件的參考加入至 `Web.config` 檔案。

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>ASP.NET 要求驗證

ASP.NET 中的要求驗證功能會針對跨網站腳本（XSS）攻擊提供特定層級的預設保護。 在舊版的 ASP.NET 中，預設會啟用要求驗證。 不過，它只會套用至 ASP.NET 網頁（`.aspx` 檔案及其類別檔案），而且只會套用至這些頁面執行時。

在 ASP.NET 4 中，預設會針對所有要求啟用要求驗證，因為它是在 HTTP 要求的**BeginRequest**階段之前啟用。 因此，要求驗證會套用至所有 ASP.NET 資源的要求，而不只是 .aspx 頁面要求。 這包括像是 Web 服務呼叫和自訂 HTTP 處理常式之類的要求。 當自訂 HTTP 模組讀取 HTTP 要求的內容時，要求驗證也是作用中。

因此，先前未觸發錯誤的要求，現在可能會發生要求驗證錯誤。 若要還原為 ASP.NET 2.0 要求驗證功能的行為，請在 `Web.config` 檔案中新增下列設定：

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

不過，我們建議您分析任何要求驗證錯誤，以判斷現有處理常式、模組或其他自訂程式碼是否會存取可能為 XSS 攻擊媒介的潛在不安全 HTTP 輸入。

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>預設雜湊演算法現已 HMACSHA256

ASP.NET 使用加密和雜湊演算法來協助保護資料，例如表單驗證 Cookie 和檢視狀態。 根據預設，ASP.NET 4 現在會針對 cookie 和 view 狀態的雜湊作業使用 HMACSHA256 演算法。 較早版本的 ASP.NET 使用較舊的 HMACSHA1 演算法。

如果您執行混合 ASP.NET 2.0/ASP. NET 4 環境，例如表單驗證 cookie 的資料必須使用 across.NET Framework 版本，您的應用程式可能會受到影響。 若要將 ASP.NET 4 Web 應用程式設定為使用較舊的 HMACSHA1 演算法，請在 `Web.config` 檔案中新增下列設定：

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>與新的 ASP.NET 4 根設定相關的設定錯誤

.NET Framework 4 （因此 ASP.NET 4）的根設定檔案（`machine.config` 檔案和根 `Web.config` 檔案）已經更新，以包含在應用程式 `Web.config` 檔案中找到的大部分 ASP.NET 3.5 中的重複使用設定資訊。 由於受管理的 IIS 7 和 IIS 7.5 設定系統的複雜性，在 ASP.NET 4 和 iis 7 和 IIS 7.5 下執行 ASP.NET 3.5 應用程式可能會導致 ASP.NET 或 IIS 設定錯誤。

我們建議您在實際情況下，使用 Visual Studio 2010 中的專案升級工具，將 ASP.NET 3.5 應用程式升級至 ASP.NET 4。 Visual Studio 2010 會自動修改 ASP.NET 3.5 應用程式的 `Web.config` 檔，使其包含 ASP.NET 4 的適當設定。

不過，使用 .NET Framework 4 來執行 ASP.NET 3.5 應用程式不需要重新編譯，這是支援的案例。 在這種情況下，您可能必須先手動修改應用程式的 `Web.config` 檔，然後才能在 .NET Framework 4 和 IIS 7 或 IIS 7.5 下執行應用程式。

接下來的兩節說明您可能需要針對不同的軟體組合進行的變更。

**Windows Vista SP1 或 Windows Server 2008 SP1，其中不會安裝任何修補程式 KB958854 或 SP2。** 在此設定中，IIS 7 設定系統會藉由比較應用層級的 `Web.config` 檔案與 ASP.NET 2.0 `machine.config` 檔，來不正確地合併應用程式的受管理設定。 因此，來自 .NET Framework 3.5 或更新版本的應用層級 `Web.config` 檔案必須有**system.web 副檔名**設定區段定義（元素），才不會導致 IIS 7 驗證失敗。

不過，手動修改的應用層級 `Web.config` 檔案專案若未精確符合 Visual Studio 2008 引進的原始樣板設定區段定義，則會導致 ASP.NET 設定錯誤。 （Visual Studio 2008 產生的預設設定專案會正常運作）。常見的問題是，手動修改 `Web.config` 檔案會省略在各種設定區段定義上找到的**allowDefinition**和**requirePermission**設定屬性。 這會導致應用層級 `Web.config` 檔案中的縮寫設定區段與 ASP.NET 4 `machine.config` 檔案中的完整定義不相符。 因此，在執行時間，ASP.NET 4 設定系統會擲回設定錯誤。

**Windows Vista SP2、Windows Server 2008 SP2、Windows 7、Windows Server 2008 R2 以及 Windows Vista SP1 和 Windows Server 2008 SP1，其中安裝了「修正程式 KB958854。**

在此案例中，IIS 7 和 IIS 7.5 原生設定系統會傳回設定錯誤，因為它會對針對 managed 設定區段處理常式所定義的**類型**屬性執行文字比較。 因為 Visual Studio 2008 和 Visual Studio 2008 SP1 所產生的所有 `Web.config` 檔案在系統的類型字串中都有 "3.5" **。網頁副檔名**（和相關）設定區段處理常式，而且由於 ASP.NET 4 `machine.config` 檔案在相同設定區段處理常式的**type**屬性中具有 "4.0"，所以在 Visual Studio 2008 或 Visual Studio 2008 SP1 中產生的應用程式一律會在 iis 7 和 iis 7.5 中失敗設定驗證。

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>解決這些問題

第一個案例的因應措施是藉由在 Visual Studio 2008 自動產生的 `Web.config` 檔案中包含未定案設定文字，以更新應用層級 `Web.config` 檔案。

第一個案例的替代因應措施是在您的電腦上安裝適用于 Vista 或 Windows Server 2008 的 Service Pack 2，或安裝 fix KB958854 （[https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)），以修正 IIS 設定系統的不正確設定合併行為。 不過，在您執行上述任一動作之後，您的應用程式可能會因為第二個案例所述的問題而遇到設定錯誤。

第二個案例的因應措施是從應用層級的 `Web.config` 檔中，刪除或批註所有的**system.web. extensions**設定區段定義和 configuration 區段群組定義。 這些定義通常位於應用層級 `Web.config` 檔案的頂端，而且可以由**configSections**元素和其子系加以識別。

在這兩種情況下，建議您也手動刪除**system.object**區段，雖然這不是必要的。

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 4 子應用程式在 ASP.NET 2.0 或 ASP.NET 3.5 應用程式下無法啟動

因為發生組態或編譯錯誤，所以可能無法啟動設定為執行舊版 ASP.NET 之應用程式子系的 ASP.NET 4 應用程式。 下列範例顯示受影響應用程式的目錄結構。

`/parentwebapp` （設定為使用 ASP.NET 2.0 或 ASP.NET 3.5）  
`/childwebapp` （設定為使用 ASP.NET 4）

[`childwebapp`] 資料夾中的應用程式將無法在 IIS 7 或 IIS 7.5 上啟動，並且會報告設定錯誤。 錯誤文字將包含類似下面的訊息：

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

在 IIS 6 上，[`childwebapp`] 資料夾中的應用程式也將無法啟動，但它會報告不同的錯誤。 例如，錯誤文字可能會陳述下列內容：

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

發生這些狀況的原因是，來自 [`parentwebapp`] 資料夾中父應用程式的設定資訊是設定資訊階層的一部分，可決定 [`childwebapp`] 資料夾中子 web 應用程式所使用的最終合併設定。 根據 ASP.NET 4 Web 應用程式是在 IIS 7 （或 IIS 7.5）還是在 IIS 6 上執行，IIS 設定系統或 ASP.NET 4 編譯系統會傳回錯誤。

您必須遵循這些步驟來解決此問題，並讓子 ASP.NET 4 應用程式運作，取決於 ASP.NET 4 應用程式是在 IIS 6 或 IIS 7 （或 IIS 7.5）上執行。

### <a name="step-1-iis-7-or-iis-75-only"></a>步驟1（僅限 IIS 7 或 IIS 7.5）

只有執行 IIS 7 或 IIS 7.5 的作業系統（包括 Windows Vista、Windows Server 2008、Windows 7 和 Windows Server 2008 R2），才需要執行此步驟。

將父應用程式的 `Web.config` 檔案中的**configSections**定義（執行 ASP.NET 2.0 或 ASP.NET 3.5 的應用程式）移至 the.NET Framework 2.0 的根 `Web.config` 檔案。 IIS 7 和 IIS 7.5 原生設定系統會在合併設定檔階層時掃描**configSections**元素。 將**configSections**定義從父系 Web 應用程式的 `Web.config` 檔案移至根 `Web.config` 檔案，可有效地隱藏子 ASP.NET 4 應用程式所發生之設定合併處理的元素。

在32位作業系統或32位應用程式集區中，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 檔案通常位於下列資料夾：

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

在64位作業系統或64位應用程式集區中，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 檔案通常位於下列資料夾：

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

如果您在64位電腦上執行32位和64位的 Web 應用程式，您必須將**configSections**元素移到根 `Web.config` 檔案中，以供32位和64位系統使用。

當您將**configSections**元素放在根 `Web.config` 檔案時，請將該區段貼到**configuration**元素之後的後面。 下列範例顯示當您完成移動元素時，根 `Web.config` 檔案的上半部應該看起來的樣子。

> [!NOTE]
> 在下列範例中，已包裝行以方便閱讀。

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>步驟2（所有版本的 IIS）

無論 ASP.NET 4 子 Web 應用程式是在 IIS 6 或 IIS 7 （或 IIS 7.5）上執行，都需要這個步驟。

在執行 ASP.NET 2 或 ASP.NET 3.5 之父 Web 應用程式的 `Web.config` 檔案中，新增一個**位置**標籤，此標記會明確指定（適用于 IIS 和 ASP.NET 設定系統），而設定專案只會套用至父 web 應用程式。 下列範例顯示要加入之**location**元素的語法：

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

下列範例顯示如何使用**location**標記來包裝所有設定區段，從**appSettings**區段開始，並以**system.webserver**區段結束。

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

當您完成步驟1和2時，子 ASP.NET 4 Web 應用程式將會啟動而不會發生錯誤。

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>ASP.NET 4 網站在安裝 SharePoint 的電腦上無法啟動

執行 SharePoint 的 Web 服務器具有部署在 SharePoint 網站根目錄的 `Web.config` 檔案（例如，`c:\inetpub\wwwroot\web.config` 用於預設的網站）。 在此 `Web.config` 檔案中，SharePoint 會將名為 WSS\_的自訂部分信任層級設定為最少。

如果您嘗試執行的 ASP.NET 4 網站是部署為此類型 SharePoint 網站的子系，您將會看到下列錯誤：

`Could not find permission set named 'ASP.NET'.`

之所以發生此錯誤，是因為 ASP.NET 4 代碼啟用安全性（CAS）基礎結構會尋找名為 ASP.NET 的許可權集合。 不過，WSS\_所參考的部分信任設定檔案，並不包含任何具有該名稱的許可權集合。

目前沒有可與 ASP.NET 相容的 SharePoint 版本。 因此，您不應該嘗試在 SharePoint 網站底下，將 ASP.NET 4 網站當做子網站執行。

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>HttpRequest 的屬性不再包含 PathInfo 值

舊版的 ASP.NET 在不同檔案路徑相關屬性（包括**HttpRequest**、 **HttpRequest、AppRelativeCurrentExecutionFilePath**和**HttpRequest**）所傳回的值中，包含了**PathInfo**值。 ASP.NET 4 不再包含這些屬性的傳回值中的**PathInfo**值。 相反地， **PathInfo**資訊可在**HttpRequest. PathInfo**中取得。 例如，假設有下列 URL 片段：

`/testapp/Action.mvc/SomeAction`

在舊版的 ASP.NET 中， **HttpRequest**屬性具有下列值：

**HttpRequest FilePath**： `/testapp/Action.mvc/SomeAction`

**HttpRequest. PathInfo**：（空白）

在 ASP.NET 4 中， **HttpRequest**屬性會改為具有下列值：

**HttpRequest FilePath**： `/testapp/Action.mvc`

**HttpRequest. PathInfo**： `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>ASP.NET 2.0 應用程式可能會產生參考 eurl 的 HttpException 錯誤

在 IIS 6 上啟用 ASP.NET 4 之後，IIS 6 上執行的 ASP.NET 2.0 應用程式 (在 Windows Server 2003 或 Windows Server 2003 R2 中) 可能會產生下列這類錯誤：

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

發生此錯誤的原因是當 ASP.NET 偵測到某個網站已設定為使用 ASP.NET 4 時，ASP.NET 4 的原生元件會將無副檔名 URL 傳遞至 ASP.NET 的 managed 部分，以供進一步處理。 不過，如果 ASP.NET 4 網站底下的虛擬目錄設定為使用 ASP.NET 2.0，以這種方式處理無副檔名 URL 會產生包含字串 "eurl" 的修改 URL。 這個修改後的 URL 會傳送至 ASP.NET 2.0 應用程式。 ASP.NET 2.0 無法辨識 "eurl" 格式。 因此，ASP.NET 2.0 會嘗試尋找名為 `eurl.axd` 的檔案，並加以執行。 因為沒有這類檔案存在，要求會失敗並出現**HttpException**例外狀況。

您可以使用下列其中一個選項來解決此問題。

### <a name="option-1"></a>選項 1

如果執行網站時不需要 ASP.NET 4，請重新對應網站，改為使用 ASP.NET 2.0。

### <a name="option-2"></a>選項 2

如果需要 ASP.NET 4 才能執行網站，請將任何子 ASP.NET 2.0 虛擬目錄移到另一個對應至 ASP.NET 2.0 的網站。

### <a name="option-3"></a>選項3

如果將網站重新對應至 ASP.NET 2.0 或變更虛擬目錄的位置並不實用，請明確停用 ASP.NET 4 中的無副檔名 URL 處理。 請使用下列程序：

1. 在 Windows 登錄中，開啟下列節點：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. 建立名為**EnableExtensionlessUrls**的新**DWORD**值。
2. 將**EnableExtensionlessUrls**設定為0。 這會停用無副檔名 URL 行為。
3. 儲存登錄值，然後關閉 [登錄編輯程式]。
4. 執行**iisreset**命令列工具，這會導致 IIS 讀取新的登錄值。

> [!NOTE]
> 將**EnableExtensionlessUrls**設定為1可啟用無副檔名 URL 行為。 如果未指定任何值，這就是預設設定。

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>事件處理常式可能不會在 IIS 7 或 IIS 7.5 整合模式的預設檔中引發

ASP.NET 4 包含修改，可變更當無副檔名 URL 解析為預設檔時，如何呈現 HTML**表單**元素的**action**屬性。 無副檔名 URL 解析為預設檔的範例會[http://contoso.com/](http://contoso.com/)，因而導致[http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)的要求。

ASP.NET 4 現在會在對具有對應預設檔的無副檔名 URL 提出要求時，將 HTML**表單**元素的**動作**屬性值呈現為空字串。 例如，在舊版的 ASP.NET 中， [http://contoso.com](http://contoso.com)的要求會導致 `Default.aspx`的要求。 在該檔中，開啟**表單**標記會如下列範例所示呈現：

`<form action="Default.aspx" />`

在 ASP.NET 4 中， [http://contoso.com](http://contoso.com)的要求也會導致 `Default.aspx`的要求。 不過，ASP.NET 現在會轉譯 HTML 開啟**表單**標記，如下列範例所示：

`<form action="" />`

如何轉譯**動作**屬性的這項差異，可能會導致 IIS 和 ASP.NET 處理表單張貼時的細微變更。 當**action**屬性是空字串時，IIS **DefaultDocumentModule**物件將會建立 `Default.aspx`的子要求。 在大部分的情況下，此子要求對應用程式代碼而言是透明的，而且 [`Default.aspx`] 頁面會正常執行。

不過，Managed 程式碼與 IIS 7 或 IIS 7.5 整合模式之間的可能互動可能會在子要求期間讓受管理 .aspx 頁面適當地停止運作。 如果發生下列情況，對 `Default.aspx` 檔的子要求將會導致錯誤或非預期的行為：

1. .Aspx 頁面會傳送至瀏覽器，並將**form**元素的**action**屬性設定為 ""。
2. 表單會回傳給 ASP.NET。
3. Managed HTTP 模組會讀取實體主體的某個部分。 例如，模組會讀取**Request. Form**或**request. Params**。 這會將 POST 要求的實體主體讀入受管理記憶體中。 因此，任何以 IIS 7 或 IIS 7.5 整合模式執行的機器碼模組都無法再使用實體主體。
4. IIS **DefaultDocumentModule**物件最後會執行，並建立 `Default.aspx` 檔的子要求。 不過，因為 Managed 程式碼的某個部分已經讀取實體主體，所以沒有實體主體可用來傳送至子要求。
5. 當 HTTP 管線針對子要求執行時，`.aspx` 檔案的處理常式會在處理常式執行階段執行。
6. 因為沒有實體主體，所以沒有任何表單變數和 view 狀態，因此 .aspx 頁面處理常式不會提供任何資訊來判斷應該引發的事件（如果有的話）。 因此，未執行受影響 .aspx 頁面的回傳事件處理常式。

您可以透過下列方式來解決這個行為：

- 識別在預設檔要求期間存取要求之實體主體的 HTTP 模組，並判斷是否可以將它設定為僅針對受控要求執行。 在 IIS 7 和 IIS 7.5 的整合模式中，HTTP 模組可以標記為僅針對受控要求執行，方法是將下列屬性新增至模組的 system.webserver **/模組**專案：

- `precondition="managedHandler"`

- 此設定會針對 IIS 7 和 IIS 7.5 判斷為不受管理要求的要求停用模組。 對於預設檔要求，第一個要求是無副檔名 URL。 因此，在初始要求處理期間，IIS 不會執行任何標記為受管理處理程式前置條件的受管理模組。 因此，受控模組不會不慎讀取實體主體，因此實體主體仍然可以使用，並傳遞至子要求和預設檔。

- 如果有問題的 HTTP 模組必須針對所有要求執行（針對靜態檔案、針對解析為**DefaultDocumentModule**物件的無副檔名 url、針對 managed 要求等），請明確地將網頁的**microsoft.visualstudio.testtools.uitesting.htmlcontrols> HtmlForm**控制項的**Action**屬性設定為非空白字串，以修改受影響的 .aspx 頁面。 例如，如果預設檔是 `Default.aspx`，請修改頁面的程式碼，將**HtmlForm**控制項的**Action**屬性明確設定為 "default.aspx"。

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>對 ASP.NET 代碼啟用安全性（CAS）實行的變更

ASP.NET 2.0，並擴充3.5 中新增的 ASP.NET 功能，請使用 .NET Framework 1.1 和2.0 代碼啟用安全性（CAS）模型。 不過，已大幅全面檢查 ASP.NET 4 中 CAS 的實作。 因此，依賴全域組件快取（GAC）中執行之受信任程式碼的部分信任 ASP.NET 應用程式可能會失敗，並出現各種安全性例外狀況。 依賴大量修改機器 CAS 原則的部分信任應用程式也可能會因為安全性例外狀況而失敗。

您可以使用**信任**設定元素中的新**legacyCasModel**屬性，將部分信任 ASP.NET 4 應用程式還原為 ASP.NET 1.1 和2.0 的行為，如下列範例所示：

`<trust level= "Medium" legacyCasModel="true" />`

當您還原為舊版 CAS 模型時，會啟用下列舊的 CAS 行為：

- 遵守機器 CAS 原則。
- 允許單一應用程式域中有多個不同的許可權集合。
- 當只有 ASP.NET 或其他 .NET Framework 程式碼位於堆疊上時，GAC 中的元件不需要明確許可權判斷提示。

其中一個案例無法在 .NET Framework 4 中還原：非 Web 部分信任應用程式無法再呼叫 System.web 和 System.web 中的特定 Api。 在舊版的 .NET Framework 中，非 Web 部分信任應用程式可能會明確授與**內所 aspnethostingpermission**許可權。 然後，這些應用程式就可以使用**HTTPutility.htmlencode**、ClientServices 中的型別 **\*** 命名空間，以及與成員資格、角色和設定檔相關的類型。 .NET Framework 4 中不再支援從非 Web 部分信任應用程式呼叫這些類型。

> [!NOTE]
> **Httputility.htmlencode**類別的**HtmlEncode**和**system.net.webutility.htmldecode**功能已移至新的 .NET Framework 4**系統 .net. webutility.htmldecode**類別。 如果這是唯一使用的 ASP.NET 功能，請修改應用程式的程式碼，改為使用新的**webutility.htmldecode**類別。

以下是 ASP.NET 4 中預設 CAS 執行變更的高階摘要：

- ASP.NET 應用程式域現在是同質應用程式域。 只有部分信任和完全信任的授與集可在應用程式域中使用。
- ASP.NET 部分信任的授與集與任何企業層級、電腦層級或使用者層級的 CAS 原則無關。
- 已將3.5 和 3.5 SP1 隨附的 ASP.NET 元件轉換成使用 .NET Framework 4 透明度模型。
- ASP.NET**內所 aspnethostingpermission**屬性的使用已大幅降低。 已從公用 ASP.NET Api 中移除此屬性的大多數實例。
- ASP.NET 組建提供者所建立的動態編譯元件已更新，以明確地將元件標記為透明。
- 所有的 ASP.NET 元件現在都會標示為僅在 Web 主控環境中接受 APTCA 屬性。 部分信任的非 Web 裝載環境（例如 ClickOnce）無法呼叫 ASP.NET 元件。

如需新的 ASP.NET 4 代碼啟用安全性模型的詳細資訊，請參閱 MSDN 網站上的在[ASP.NET 應用程式中使用代碼啟用安全性](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx)。

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>MembershipUser 和 System.web. Security 命名空間中的其他類型已移動

某些用於 ASP.NET 成員資格的類型已從 `System.Web.dll` 移至新的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception .dll 元件。 已移動類型，以解析用戶端和擴充 .NET Framework SKU 中類型之間的架構層相依性。

由於 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 已新增至 ASP.NET 編譯系統預設使用的參考元件清單中，因此網站專案不會因為移動這些類型而產生任何問題。 如果您將使用舊版 ASP.NET 建立的網站專案升級為 ASP.NET 4，方法是在 Visual Studio 2010 中開啟它，專案就會編譯而不會發生錯誤。

同樣地，如果您在 Visual Studio 2010 中開啟以舊版 ASP.NET 建立的 Web 應用程式專案到 ASP.NET 4，升級程式就會將 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的參考加入至專案。 因此，升級的 Web 應用程式專案也會編譯而不會發生錯誤。

使用舊版 ASP.NET 所建立的已編譯（二進位）檔案也會在 ASP.NET 4 上執行，而不會發生錯誤，即使成員資格類型已移至不同的元件也一樣。 類型轉送資訊已新增至 ASP.NET 4 版的 `System.Web.dll`，會自動將這些類型的執行時間參考路由至類型的新位置。

不過，使用特定成員資格類型，而且已從舊版 ASP.NET 升級的類別庫，在 ASP.NET 4 專案中使用時，將無法進行編譯。 例如，類別庫專案可能無法編譯和報告錯誤，如下所示：

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

若要解決這個問題，您可以在類別庫專案中加入 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的參考。

下列清單顯示已從 `System.Web.dll` 移至 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的*system.web. Security*型別：

- *System.web. Security. MembershipCreateStatus*
- *CreateUserException 的成員。*
- *System.web. Security. System.web.security.membershippasswordexception*
- *System.web. Security. MembershipPasswordFormat*
- *System.web. MembershipProvider*
- *System.web. Security. MembershipProviderCollection*
- *System.web. Security. MembershipUser*
- *System.web. Security. MembershipUserCollection*
- *System.web. Security. MembershipValidatePasswordEventHandler*
- *System.web. Security. ValidatePasswordEventArgs*
- *System.web. Security. RoleProvider*
- <a id="0.1_a"></a>*System.web. MembershipPasswordCompatibilityMode*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>輸出快取變更為不同的 \* HTTP 標頭

在 ASP.NET 1.0 中，bug 導致指定 `Location="ServerAndClient"` 的快取頁面做為輸出–快取設定，以在回應中發出 `Vary:*` HTTP 標頭。 這會影響如何告知用戶端瀏覽器永遠不要在本機快取頁面。

在 ASP.NET 1.1 中，已新增**HttpCachePolicy. SetOmitVaryStar**方法，您可以呼叫它來隱藏 `Vary:*` 標頭。 已選擇這個方法，因為變更發出的 HTTP 標頭在當時已被視為可能的重大變更。 不過，開發人員已被 ASP.NET 中的行為搞混，而 bug 報告則建議開發人員不知道現有的**SetOmitVaryStar**行為。

在 ASP.NET 4 中，決策是為了修正根本問題而做出的。 不會再從指定下列指示詞的回應發出 `Vary:*` HTTP 標頭：

`<%@OutputCache Location="ServerAndClient" %>`

因此，不需要**SetOmitVaryStar**就能隱藏 `Vary:*` 標頭。

在在頁面上的 **@ OutputCache**指示詞中指定 `Location="ServerAndClient"` 的應用程式中，您現在會看到**Location**屬性的值所隱含的行為，也就是可以在瀏覽器中快取頁面，而不需要呼叫**SetOmitVaryStar**方法。

如果您應用程式中的頁面必須發出 `Vary:*`，請呼叫**AppendHeader**方法，如下列範例所示：

`HttpResponse.AppendHeader("Vary","*");`

或者，您可以將 [輸出快取**位置**] 屬性的值變更為 [伺服器]。

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Passport 的安全性類型已過時

ASP.NET 2.0 內建的 Passport 支援已經過時，而且因為 Passport 的變更（現在是 LiveID）而不支援幾年。 因此，與**system.web**中的 Passport 相關的五種類型現在會以**ObsoleteAttribute**屬性標記。

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>PopOutImageUrl 屬性無法轉譯 ASP.NET 4 中的影像

在 ASP.NET 3.5 中， *PopOutImageUrl*屬性可讓您指定功能表項目中顯示之影像的 URL，以指出功能表項目具有動態子功能表。 下列範例顯示如何在 ASP.NET 3.5 的標記中指定此屬性。

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

由於 ASP.NET 4 中的設計變更，如果為*MenuItem*類別設定了屬性，則不會呈現*PopOutImageUrl*的輸出。 您必須改為使用*StaticPopOutImageUrl*屬性或*DynamicPopOutImageUrl*屬性，直接在*MENU*控制項中指定影像 URL。 當您使用靜態功能表時， *StaticPopOutImageUrl*屬性會指定要顯示之影像的 URL，以指出靜態功能表項目具有子功能表，如下列範例所示：

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

如果您要使用動態功能表，請使用*DynamicPopOutImageUrl*屬性來指定影像的 URL，表示動態功能表項目具有子功能表。 下列範例與上一個範例類似，但會顯示如何設定動態功能表的*DynamicPopOutImageUrl*屬性。

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

如果未設定*DynamicPopOutImageUrl*屬性，而且*DynamicEnableDefaultPopOutImage*屬性設定為*false*，則不會顯示任何影像。 同樣地，如果未設定*StaticPopOutImageUrl*屬性，而且*StaticEnableDefaultPopOutImage*屬性設定為*false*，則不會顯示任何影像。

當您設定這些屬性的路徑時，請使用正斜線（/），而不是反斜線（\)。 如需詳細資訊，請參閱[StaticPopOutImageUrl 和 menu。當路徑包含](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu。 StaticPopOutImageUrl_and_Menu。")本檔中其他位置的反斜線時，DynamicPopOutImageUrl 無法轉譯影像。

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>StaticPopOutImageUrl 和 Menu. DynamicPopOutImageUrl 無法在路徑包含反斜線時呈現影像

在 ASP.NET 4 中，如果路徑包含 backlashes （\)，則使用*StaticPopOutImageUrl*和*menu. DynamicPopOutImageUrl*屬性所指定的影像將不會呈現。 這是舊版 ASP.NET 的變更。

下列*Menu*控制項標記範例顯示使用包含反斜線的路徑所設定的*StaticPopOutImageUrl*屬性。 在 ASP.NET 4 中，屬性中指定的影像將不會呈現。

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

若要更正此問題，請將*StaticPopOutImageUrl*和*DynamicPopOutImageUrl*屬性中指定的路徑值變更為使用正斜線（/）。 下列範例會顯示這項變更：

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

請注意，從舊版 ASP.NET 遷移至 ASP.NET 4 的應用程式可能也會受到影響，因為*PopOutImageUrl*屬性已經變更。 如需詳細資訊，請參閱本檔中其他位置[的 PopOutImageUrl 屬性無法轉譯 ASP.NET 4 中的影像](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem。 PopOutImageUrl_Propert")。

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>免責聲明

這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。

本文件中的資訊表示直到文件發行日前 Microsoft Corporation 針對問題的看法。 Microsoft 必須因應不斷變化的市場狀況，因此本文件不代表 Microsoft 的保證，且 Microsoft 不保證這些資訊在文件發行後的正確性。

本技術白皮書僅供參考。 MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。

承諾遵守所有適用的著作權法是使用者的責任。 著作權法沒有針對某種權利加以限制，但在未獲得 Microsoft Corporation 書面同意的情況下，本文件的任何部分不得複製、以檢索系統存放或擷取、以任何形式或方法傳送 (電子、機械、影像複製、錄音或其他任何方法)、或基於任何其他不良意圖。

本文件所提及的主要事務，Microsoft 得擁有專利、專利應用程式、商標、著作權或其他智慧財產權。 除了 Microsoft 於授權合約書中書面提供的之外，本文件所述內容並未賦予您這些專利、商標、著作權、或其他智慧財產的任何授權或使用權利。

除非另有說明，否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、商標、人員、地點及事件均屬虛構，而且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件相關。位址、標誌、人員、地點或事件的預定或應加以推斷。

© 2010 Microsoft Corporation。 著作權所有，並保留一切權利。

Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。

本文件中所提實際公司和產品，可能為各所有人所有之商標。
