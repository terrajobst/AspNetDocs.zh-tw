---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: ASP.NET MVC 和 Web Pages 中的 XSRF/CSRF 防護 |Microsoft Docs
author: Rick-Anderson
description: 跨網站偽造要求（也稱為 XSRF 或 CSRF）是對 web 託管應用程式的攻擊，而惡意網站可能會影響 interacti 。
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 1965063a9b613d0e2857cddcc2165f5fda64ec0c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455525"
---
# <a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>ASP.NET MVC 和 ASP.NET Web Pages 中的 XSRF/CSRF 防護

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 跨網站偽造要求（也稱為 XSRF 或 CSRF）是對 web 裝載應用程式的攻擊，因此惡意網站可能會影響用戶端瀏覽器與該瀏覽器信任的網站之間的互動。 由於網頁瀏覽器會在每次要求網站時自動傳送驗證權杖，因此可以進行這些攻擊。 ASP.NET 的 Forms Authentication 票證即是驗證 Cookie 的標準範例。 不過，使用任何持續性驗證機制（例如 Windows 驗證、基本等等）的網站，都可以受到這些攻擊的目標。
> 
> XSRF 攻擊與網路釣魚攻擊不同。 網路釣魚攻擊需要與受害者互動。 在網路釣魚攻擊中，惡意網站會模擬目標網站，而受害者會愚弄為攻擊者提供機密資訊。 XSRF 攻擊則通常不需要與受害者互動。 相反地，攻擊者會依賴瀏覽器自動將所有相關的 cookie 傳送至目的地網站。
> 
> 如需詳細資訊，請參閱[Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page)（OWASP） [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))。

## <a name="anatomy-of-an-attack"></a>攻擊的剖析

若要逐步完成 XSRF 攻擊，請考慮想要執行一些線上銀行交易的使用者。 此使用者會先造訪 WoodgroveBank.com 和登入，此時回應標頭會包含她的驗證 cookie：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

因為驗證 cookie 是會話 cookie，所以瀏覽器會在瀏覽器進程結束時自動清除。 不過，在該時間之前，瀏覽器會自動包含每個要求到 WoodgroveBank.com 的 cookie。 使用者現在想要將 $1000 轉移到另一個帳戶，因此她會在銀行網站上填滿表單，而瀏覽器會對伺服器提出此要求：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

由於這項作業有副作用（它會起始貨幣交易），因此銀行網站已選擇要求 HTTP POST，以起始這項操作。 伺服器會從要求讀取驗證權杖、查詢目前使用者的帳戶號碼、確認有足夠的資金存在，然後在目的地帳戶中起始交易。

她的線上銀行完成後，使用者離開銀行網站，流覽網站上的其他位置。 其中一個網站– fabrikam.com –在內嵌于 &lt;iframe&gt;的頁面上包含下列標記：

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

這會導致瀏覽器提出此要求：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

攻擊者利用的事實是，使用者對於目標網站可能還是會有有效的驗證權杖，而她使用一小部分的 JAVAscript 讓瀏覽器自動對目標網站進行 HTTP POST。 如果驗證權杖仍然有效，銀行網站將會起始 $250 傳輸到攻擊者選擇的帳戶。

### <a name="ineffective-mitigations"></a>不正確緩和措施

值得注意的是，在上述案例中，WoodgroveBank.com 是透過 SSL 存取，而且具有僅限 SSL 的驗證 cookie 並不足以阻止攻擊。 攻擊者可以在她的 &lt;表單&gt; 元素中指定[URI 配置](http://en.wikipedia.org/wiki/URI_scheme)（HTTPs），而瀏覽器會繼續將未到期的 cookie 傳送至目標網站，只要那些 cookie 與預定目標的 URI 配置一致即可。

其中一個人可能會認為，使用者不應該直接造訪不受信任的網站，因為只造訪信任的網站有助於在線上保持安全。 事實上，這種做法並不一定可行。 可能是使用者「信任」當地新聞網站 ConsolidatedMessenger。 ConsolidatedMessenger.com 並改為造訪該網站，但該網站具有 XSS 弱點，可讓攻擊者插入在 fabrikam.com 上執行的相同程式碼片段。

您可以確認傳入要求的[推薦者標頭](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14)參考您的網域。 這會停止從協力廠商網域中不知情提交的要求。 不過，有些人會因為隱私權的緣故而停用其瀏覽器的推薦者標頭，而攻擊者有時可能會在受害者已安裝特定不安全軟體時偽造該標頭。 驗證[推薦者標頭](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14)不會被視為防止 XSRF 攻擊的安全方法。

## <a name="web-stack-runtime-xsrf-mitigations"></a>Web Stack 執行時間 XSRF 緩和措施

ASP.NET Web Stack 執行時間會使用[同步器權杖模式](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern)的變體，來防禦 XSRF 攻擊。 同步器權杖模式的一般形式是，兩個反 XSRF 權杖會連同每個 HTTP POST （除了驗證 token）提交至伺服器：一個權杖做為 cookie，另一個則當做表單值。 ASP.NET 執行時間所產生的權杖值不具決定性，也不能由攻擊者預測。 提交權杖時，只有在兩個權杖通過比較檢查時，伺服器才會允許要求繼續進行。

XSRF 要求驗證*會話權杖*會儲存為 HTTP cookie，而且目前在其承載中包含下列資訊：

- 由隨機128位識別碼組成的安全性權杖。   
 下圖顯示使用 Internet Explorer F12 開發人員工具顯示的 XSRF 要求驗證會話權杖：（請注意，這是目前的執行，甚至可能會變更）。

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*欄位 token*會儲存為 `<input type="hidden" />`，並在其裝載中包含下列資訊：

- 登入使用者的使用者名稱（如果已驗證的話）。
- [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)提供的任何其他資料。

反 XSRF token 的裝載會經過加密和簽署，因此當您使用工具檢查權杖時，就無法查看使用者名稱。 當 web 應用程式以 ASP.NET 4.0 為目標時，密碼編譯服務會由[MachineKey 提供。編碼](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx)常式。 當 web 應用程式的目標為 ASP.NET 4.5 或更高版本時，MachineKey 會提供密碼編譯服務[。保護](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110))常式，以提供更佳的效能、擴充性和安全性。 如需更多詳細資料，請參閱下列 blog 文章：

- [ASP.NET 4.5 中的密碼編譯改善，pt. 1](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4.5 中的密碼編譯改良功能，pt. 2](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4.5 的密碼編譯增強功能，pt. 3](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>產生權杖

若要產生反 XSRF token，請從 MVC 視圖呼叫[@Html.AntiForgeryToken](https://msdn.microsoft.com/library/dd470175.aspx)方法，或從 Razor 頁面 @AntiForgery.GetHtml（）。 執行時間接著會執行下列步驟：

1. 如果目前的 HTTP 要求已經包含反 XSRF 會話權杖（反 XSRF cookie \_\_RequestVerificationToken），則會從它解壓縮安全性權杖。 如果 HTTP 要求不包含反 XSRF 會話 token，或如果安全性權杖的解壓縮失敗，則會產生新的隨機反 XSRF token。
2. 會使用上述步驟（1）中的安全性權杖，以及目前登入使用者的身分識別，來產生反 XSRF 欄位 token。 （如需有關判斷使用者身分識別的詳細資訊，請參閱下面的「 **[具有特殊支援的案例](#_Scenarios_with_special)** 」一節）。此外，如果已設定[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) ，執行時間會呼叫其[GetAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx)方法，並在欄位 token 中包含傳回的字串。 （如需詳細資訊，請參閱設定 **[和](#_Configuration_and_extensibility)** 擴充性一節）。
3. 如果在步驟（1）中產生新的反 XSRF token，則會建立新的會話權杖以包含它，並將其新增至輸出 HTTP cookie 集合。 步驟（2）中的欄位 token 將會包裝在 `<input type="hidden" />` 元素中，而此 HTML 標籤會是 `Html.AntiForgeryToken()` 或 `AntiForgery.GetHtml()`的傳回值。

## <a name="validating-the-tokens"></a>驗證權杖

若要驗證傳入的防 XSRF token，開發人員在其 MVC 動作或控制器上包含[ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx)屬性，或她從 Razor 頁面呼叫 `@AntiForgery.Validate()`。 執行時間將會執行下列步驟：

1. 系統會讀取傳入會話權杖和欄位權杖，並從每個權杖提取反 XSRF token。 XSRF 權杖在世代常式中的每個步驟（2）都必須相同。
2. 如果目前的使用者已通過驗證，則會與欄位權杖中儲存的使用者名稱進行比較。 使用者名稱必須相符。
3. 如果已設定[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) ，執行時間會呼叫其*ValidateAdditionalData*方法。 此方法必須傳回布林值*true*。

如果驗證成功，則允許要求繼續進行。 如果驗證失敗，架構將會擲回*HttpAntiForgeryException*。

## <a name="failure-conditions"></a>失敗狀況

從 ASP.NET Web Stack 執行時間 v2 開始，驗證期間擲回的任何*HttpAntiForgeryException*都會包含錯誤發生的詳細資訊。 目前定義的失敗狀況如下：

- 會話權杖或表單權杖不存在於要求中。
- 會話權杖或表單 token 無法讀取。 最有可能的原因是執行 ASP.NET Web Stack 執行時間不相符的伺服器陣列，或在 web.config 中的 &lt;machineKey&gt; 元素與電腦之間不同的伺服器陣列。 您可以使用 Fiddler 之類的工具來強制執行此例外狀況，方法是利用反 XSRF token 來進行篡改。
- 已交換會話權杖和欄位 token。
- 會話權杖和欄位權杖包含不相符的安全性權杖。
- 內嵌在欄位 token 內的使用者名稱不符合目前登入的使用者名稱。
- *[IAntiForgeryAdditionalDataProvider. ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* 方法傳回*false*。

防 XSRF 設施也可能在權杖產生或驗證期間執行額外檢查，而這些檢查期間的失敗可能會導致擲回例外狀況。 如需詳細資訊，請參閱[WIF/ACS/以宣告為基礎的驗證](#_WIF_ACS)和設定 **[和](#_Configuration_and_extensibility)** 擴充性章節。

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>具有特殊支援的案例

### <a name="anonymous-authentication"></a>匿名驗證

反 XSRF 系統包含匿名使用者的特殊支援，其中「匿名」定義為使用者，其中*IIdentity. IsAuthenticated*屬性會傳回*false*。 案例包括提供登入頁面的 XSRF 保護（在使用者經過驗證之前）和自訂驗證配置，其中應用程式會使用*IIdentity*以外的機制來識別使用者。

若要支援這些案例，請記得會話和欄位權杖是由安全性權杖聯結，這是128位隨機產生的不透明識別碼。 此安全性權杖會在流覽網站時用來追蹤個別使用者的會話，因此它會有效地提供匿名識別碼的用途。 空字串是用來取代上述產生和驗證常式的使用者名稱。

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF/ACS/以宣告為基礎的驗證

一般來說，.NET Framework 內建的*IIdentity*類別具有*IIdentity.Name*足夠的屬性，可唯一識別特定應用程式內的特定使用者。 例如， *FormsIdentity.Name*會傳回儲存在成員資格資料庫中的使用者名稱（這對於根據該資料庫的所有應用程式而言是唯一的）， *WindowsIdentity.Name*會傳回使用者的網域限定身分識別等等。 這些系統不僅提供驗證，他們也會將使用者*識別*為應用程式。

另一方面，以宣告為基礎的驗證不一定需要識別特定的使用者。 相反地， *ClaimsPrincipal*和*ClaimsIdentity*類型會與一組*宣告實例相關*聯，其中個別宣告可能是「為18個以上的年齡」或「系統管理員」。 由於不一定會識別使用者，因此執行時間無法使用*ClaimsIdentity.Name*屬性做為這個特定使用者的唯一識別碼。 小組已看過真實世界的範例，其中*ClaimsIdentity.Name*會傳回*null*、傳回易記（顯示）名稱，否則會傳回不適合做為使用者唯一識別碼使用的字串。

許多使用以宣告為基礎的驗證的部署，特別是使用[Azure 存取控制服務](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx)（ACS）。 ACS 可讓開發人員設定個別身分*識別提供者*（例如 ADFS、Microsoft 帳戶提供者、OpenID 提供者，例如 yahoo！等），而身分識別提供者會傳回*名稱識別碼*。 這些名稱識別碼可能包含個人識別資訊（PII）（例如電子郵件地址），或者可以像私人個人識別碼（PPID）一樣匿名。 無論是什麼，在流覽網站時，元組（識別提供者、名稱識別碼）可充分做為特定使用者的適當追蹤權杖，因此在產生和時，ASP.NET Web Stack 執行時間可以使用元組來取代使用者名稱正在驗證反 XSRF 欄位標記。 識別提供者的特定 Uri 和名稱識別碼如下：

- `https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

（如需詳細資訊，請參閱此[ACS 檔頁面](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx)）。

產生或驗證權杖時，ASP.NET Web Stack 執行時間會在執行時間嘗試系結至類型：

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` （適用于 WIF SDK）。
- `System.Security.Claims.ClaimsIdentity` （適用于 .NET 4.5）。

如果這些類型存在，而且目前使用者的*IIIIdentity*會執行或子類別其中一種類型，反 XSRF 設施將會在產生和驗證權杖時，使用（識別提供者，名稱識別碼）元組來取代使用者名稱。 如果沒有這類元組，要求將會失敗，並顯示錯誤，說明開發人員如何設定防 XSRF 系統，以瞭解使用中的特定宣告式驗證機制。 如需詳細資訊，請參閱設定 **[和](#_Configuration_and_extensibility)** 擴充性一節。

### <a name="oauth--openid-authentication"></a>OAuth/OpenID 驗證

最後，防 XSRF 設施對於使用 OAuth 或 OpenID 驗證的應用程式具有特殊支援。 這種支援是以啟發學習法為基礎：如果目前*IIdentity.Name*的開頭是 HTTP://或 HTTPs://，則會使用序數比較子（而不是預設的 OrdinalIgnoreCase 比較子）來完成使用者名稱比較。

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>設定和擴充性

有時候，開發人員可能會想要更嚴密地控制反 XSRF 的產生和驗證行為。 例如，可能是 MVC 和網頁協助程式的預設行為，會自動將 HTTP cookie 新增到回應中，而開發人員可能會想要在其他地方保存權杖。 有兩個 Api 可協助您：

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

*GetTokens*方法會以現有的 XSRF 要求驗證會話權杖（可能是 null）做為輸入，並產生新的 XSRF 要求驗證會話權杖和欄位 token 作為輸出。 標記只是不透明的字串，沒有裝飾，實例的*formToken*值不會包裝在 &lt;輸入&gt; 標記中。 *NewCookieToken*值可以是 null;如果發生這種情況，則*oldCookieToken*值仍然有效，而且不需要設定新的回應 cookie。 *GetTokens*的呼叫者會負責保存任何必要的回應 cookie，或產生任何必要的標記;*GetTokens*方法本身不會將回應改變為副作用。 *Validate*方法會接受傳入的會話和欄位權杖，並對它們執行上述驗證邏輯。

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

開發人員可以從應用程式\_開始設定防 XSRF 系統。 以程式設計方式設定。 靜態*AntiForgeryConfig*類型的屬性如下所述。 大部分使用宣告的使用者會想要設定 UniqueClaimTypeIdentifier 屬性。

| **屬性** | **說明** |
| --- | --- |
| **AdditionalDataProvider** | 在權杖產生期間提供額外資料，並在權杖驗證期間耗用額外資料的[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 。 預設值是 *null*。 如需詳細資訊，請參閱[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)一節。 |
| **CookieName** | 提供用來儲存反 XSRF 會話權杖之 HTTP cookie 名稱的字串。 如果未設定此值，系統就會根據應用程式的已部署虛擬路徑自動產生名稱。 預設值是 *null*。 |
| **RequireSsl** | 布林值，指出是否需要透過 SSL 保護的通道提交防 XSRF token。 如果此值為*true*，任何自動產生的 cookie 都會設定 "secure" 旗標，而如果從不是透過 SSL 提交的要求中呼叫，則會擲回反 XSRF api。 預設值為 *false*。 |
| **SuppressIdentityHeuristicChecks** | 布林值，指定反 XSRF 系統是否應停用對宣告式身分識別的支援。 如果此值為*true*，則系統會假設*IIdentity.Name*適合做為每個使用者的唯一識別碼，而且不會嘗試使用[WIF/ACS/宣告式驗證](#_WIF_ACS)一節中所述的特殊案例*IClaimsIdentity*或*ClClaimsIdentity* 。 預設值是 `false`。 |
| **UniqueClaimTypeIdentifier** | 字串，指出哪個宣告類型適合做為唯一的每一使用者識別碼使用。 如果設定了這個值，而目前的*IIdentity*是以宣告為基礎，則系統會嘗試解壓縮*UniqueClaimTypeIdentifier*所指定之類型的宣告，而在產生欄位標記時，將會使用對應的值來取代使用者的使用者名稱。 如果找不到宣告類型，系統就會讓要求失敗。 預設值為*null*，表示系統應該使用先前描述的（識別提供者名稱識別碼）元組來取代使用者的使用者名稱。 |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

*[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* 類型可讓開發人員在每個權杖中來回往返額外的資料，以擴充反 XSRF 系統的行為。 每次產生欄位標記時，會呼叫*GetAdditionalData*方法，而傳回值會內嵌在產生的權杖中。 實施者可能會從這個方法傳回時間戳記、nonce 或任何其他值。

同樣地，每次驗證欄位 token 時都會呼叫*ValidateAdditionalData*方法，而在標記中內嵌的「其他資料」字串則會傳遞至方法。 驗證常式可能會執行超時（藉由檢查目前時間與建立權杖時所儲存的時間）、nonce 檢查常式或任何其他所需的邏輯。

## <a name="design-decisions-and-security-considerations"></a>設計決策和安全性考慮

在技術上，只有在嘗試保護匿名/未驗證的使用者以防止 XSRF 攻擊時，才需要提供連結會話和欄位權杖的安全性權杖。 當使用者通過驗證時，驗證權杖本身（可能是以 cookie 形式提交）可以用來作為同步器權杖組的一半。 不過，有有效的案例可保護未驗證的使用者所叫用的登入頁面，而且即使是已驗證的使用者，一律會產生及驗證安全性權杖，而使反 XSRF 邏輯變得更簡單。 它也會在欄位權杖遭攻擊者洩露時提供一些額外的保護，因為設定或猜測會話權杖會是攻擊者解決的另一個障礙。

當多個應用程式裝載于單一網域時，開發人員應該小心使用。 例如，雖然*example1.cloudapp.net*和*example2.cloudapp.net*是不同的主機，但在 cloudapp.net 網域下 *\** 的所有主機之間，都有隱含的信任關係。 此隱含信任關係[允許可能不受信任的主機影響彼此的 cookie](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) （控管 AJAX 要求的相同來源原則不一定會套用至 HTTP cookie）。 ASP.NET Web Stack 執行時間提供了一些緩和措施，因為使用者名稱會內嵌到欄位 token 中，因此即使惡意子域能夠覆寫會話權杖，也無法為使用者產生有效的欄位 token。 不過，在這種環境中裝載時，內建的反 XSRF 常式仍然無法防禦會話劫持或登入 XSRF。

反 XSRF 常式目前不會抵禦[點擊劫持](https://www.owasp.org/index.php/Clickjacking)。 想要自行防禦點擊劫持的應用程式，可以藉由傳送每個回應的 X 框架選項： SAMEORIGIN 標頭，輕鬆地執行此動作。 所有最近的瀏覽器都支援此標頭。 如需詳細資訊，請參閱[IE blog](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx)、 [SDL blog](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx)和[OWASP](https://www.owasp.org/index.php/Clickjacking)。 在未來的版本中，ASP.NET Web Stack 執行時間可能會讓 MVC 和網頁反 XSRF helper 自動設定此標頭，讓應用程式得以自動保護以防止此攻擊。

Web 開發人員應該繼續確保其網站不容易遭受 XSS 攻擊。 XSS 攻擊的功能非常強大，而成功的惡意探索也會破壞 ASP.NET Web Stack 執行時間防禦 XSRF 攻擊。

## <a name="acknowledgment"></a>通知

[@LeviBroderick](https://twitter.com/LeviBroderick)，他寫了大部分的 ASP.NET 安全性程式碼，這是大部分的資訊。
