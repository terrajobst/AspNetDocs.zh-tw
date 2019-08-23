---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 和 Visual Studio 2010 Web 開發總覽 |Microsoft Docs
author: rick-anderson
description: 本檔概述 the.NET Framework 4 和 Visual Studio 2010 中包含的許多 ASP.NET 新功能。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 8c93952adb33d1ce7008ebff9d032a71eb2a5f74
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995333"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 與 Visual Studio 2010 網頁程式開發概觀

> 本檔概述 the.NET Framework 4 和 Visual Studio 2010 中包含的許多 ASP.NET 新功能。
> 
> [下載此白皮書](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

**內容**

**[Core Services](#0.2__Toc253429238 "_Toc253429238")**  
Web.config 檔案[重構](#0.2__Toc253429239 "_Toc253429239")  
[可擴充的輸出]快取(#0.2__Toc253429240 "_Toc253429240")  
[自動啟動 Web 應用程式](#0.2__Toc253429241 "_Toc253429241")  
[永久]重新導向頁面(#0.2__Toc253429242 "_Toc253429242")  
[縮小會話狀態](#0.2__Toc253429243 "_Toc253429243")  
[擴充允許的 Url 範圍](#0.2__Toc253429244 "_Toc253429244")  
可延伸的[要求驗證](#0.2__Toc253429245 "_Toc253429245")  
[物件快取和物件]快取擴充性(#0.2__Toc253429246 "_Toc253429246")  
[可擴充的 HTML、URL 和 HTTP 標頭編碼](#0.2__Toc253429247 "_Toc253429247")  
[單一工作者進程中個別應用程式的效能監視](#0.2__Toc253429248 "_Toc253429248")  
[Multi-Targeting](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[Web Forms 和 MVC 中包含的 jQuery](#0.2__Toc253429251 "_Toc253429251")  
[內容傳遞網路支援](#0.2__Toc253429252 "_Toc253429252")  
[ScriptManager 明確腳本](#0.2__Toc253429253 "_Toc253429253")

**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**  
[使用 MetaKeywords 和 MetaDescription 屬性設定中繼標記](#0.2__Toc253429257 "_Toc253429257")  
[啟用個別控制項的檢視狀態](#0.2__Toc253429258 "_Toc253429258")  
[瀏覽器功能的變更](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4 中的路由](#0.2__Toc253429260 "_Toc253429260")  
[設定用戶端識別碼](#0.2__Toc253429261 "_Toc253429261")  
[保存資料控制項中的資料列選取範圍](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET Chart 控制項](#0.2__Toc253429263 "_Toc253429263")  
[使用 QueryExtender 控制項篩選資料](#0.2__Toc253429264 "_Toc253429264")  
[Html 編碼的程式碼運算式](#0.2__Toc253429265 "_Toc253429265")  
[專案範本變更](#0.2__Toc253429266 "_Toc253429266")  
[CSS 改良功能](#0.2__Toc253429267 "_Toc253429267")  
隱藏[欄位周圍的 Div 元素](#0.2__Toc253429268 "_Toc253429268")  
[呈現樣板化控制項的外部資料表](#0.2__Toc253429269 "_Toc253429269")  
[ListView 控制項增強功能](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList 和 RadioButtonList 控制項的增強功能](#0.2__Toc253429271 "_Toc253429271")  
[Menu 控制項改良功能](#0.2__Toc253429272 "_Toc253429272")  
[Wizard 和 CreateUserWizard 控制項 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[區域支援](#0.2__Toc253429275 "_Toc253429275")  
[資料-批註屬性驗證支援](#0.2__Toc253429276 "_Toc253429276")  
樣板[化]協助程式(#0.2__Toc253429277 "_Toc253429277")

**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**  
[啟用現有專案的動態資料](#0.2__Toc253429279 "_Toc253429279")  
[宣告式 DynamicDataManager 控制語法](#0.2__Toc253429280 "_Toc253429280")  
[實體範本](#0.2__Toc253429281 "_Toc253429281")  
[Url 和電子郵件地址的新欄位範本](#0.2__Toc253429282 "_Toc253429282")  
[使用 DynamicHyperLink 控制項建立連結](#0.2__Toc253429283 "_Toc253429283")  
[資料模型中的繼承支援](#0.2__Toc253429284 "_Toc253429284")  
[支援多對多關聯性 (僅限 Entity Framework)](#0.2__Toc253429285 "_Toc253429285")  
[控制顯示和支援列舉的新屬性](#0.2__Toc253429286 "_Toc253429286")  
[增強的篩選支援](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 Web 開發改良功能](#0.2__Toc253429288 "_Toc253429288")**  
[改良的 CSS 相容性](#0.2__Toc253429289 "_Toc253429289")  
[HTML 和 JavaScript 程式碼片段](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense 增強功能](#0.2__Toc253429291 "_Toc253429291")

**[使用 Visual Studio 2010 的 Web 應用程式部署](#0.2__Toc253429292 "_Toc253429292")**  
[網頁封裝](#0.2__Toc253429293 "_Toc253429293")  
[Web.config Transformation](#0.2__Toc253429294 "_Toc253429294")  
[資料庫部署](#0.2__Toc253429295 "_Toc253429295")  
[針對 Web 應用程式按一下 [發佈]](#0.2__Toc253429296 "_Toc253429296")  
[Resources](#0.2__Toc253429297 "_Toc253429297")

**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>核心服務

ASP.NET 4 引進了一些可改善核心 ASP.NET 服務 (例如輸出快取和會話狀態儲存體) 的功能。

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>Web.config 檔案重構

`Web.config`由於新增功能 (例如 Ajax、路由及與 IIS 7 的整合), 在過去幾個版本的 .NET Framework 中, 包含 Web 應用程式設定的檔案已經大幅增加。 這使得設定或啟動新的 Web 應用程式變得更難, 而不需要像 Visual Studio 的工具。 在中, [NET Framework 4] 是主要設定元素已移至`machine.config`檔案, 而應用程式現在會繼承這些設定。 這可讓`Web.config` ASP.NET 4 應用程式中的檔案是空的, 或只包含下列幾行, 以指定 Visual Studio 應用程式的目標架構版本:

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>可擴充的輸出快取

自從 ASP.NET 1.0 發行以來, 輸出快取已讓開發人員將頁面、控制項和 HTTP 回應的產生輸出儲存在記憶體中。 在後續的 Web 要求中, ASP.NET 可以藉由從記憶體抓取產生的輸出, 而不是從頭開始重新產生輸出, 以更快速的方式提供內容。 不過, 這種方法有一項限制: 產生的內容一律必須儲存在記憶體中, 而在遇到大量流量的伺服器上, 輸出快取所耗用的記憶體可以與 Web 應用程式其他部分的記憶體需求競爭。

ASP.NET 4 會將擴充點新增至輸出快取, 讓您可以設定一或多個自訂輸出快取提供者。 輸出快取提供者可以使用任何儲存機制來保存 HTML 內容。 這可讓您建立各種持續性機制的自訂輸出快取提供者, 其中包括本機或遠端磁片、雲端存放裝置, 以及分散式快取引擎。

您會建立自訂輸出快取提供者, 做為衍生自新*system.web.caching.outputcacheprovider*類型的類別。 接著, 您可以使用*outputCache*元素的`Web.config`新*提供者*子區段, 在檔案中設定提供者, 如下列範例所示:

[!code-xml[Main](overview/samples/sample2.xml)]

根據預設, 在 ASP.NET 4 中, 所有 HTTP 回應、轉譯的頁面和控制項都會使用記憶體中的輸出快取, 如先前範例所示, 其中*defaultProvider*屬性設定為 AspNetInternalProvider。 您可以為*defaultProvider*指定不同的提供者名稱, 以變更用於 Web 應用程式的預設輸出快取提供者。

此外, 您可以針對每個控制項和每個要求選取不同的輸出快取提供者。 若要為不同的 Web 使用者控制項選擇不同的輸出快取提供者, 最簡單的方式就是使用控制項指示詞中的新*providerName*屬性, 以宣告方式執行此動作, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample3.aspx)]

為 HTTP 要求指定不同的輸出快取提供者需要更多工作。 您不是以宣告方式指定提供者, 而是在檔案中`Global.asax`覆寫新的 GetOuputCacheProviderName 方法, 以程式設計方式指定要用於特定要求的提供者。 下列範例顯示如何執行這項工作。

[!code-csharp[Main](overview/samples/sample4.cs)]

透過將輸出快取提供者擴充性新增至 ASP.NET 4, 您現在可以為您的網站實現更積極且更聰明的輸出快取策略。 例如, 您現在可以在記憶體中快取網站的「前10個」頁面, 同時在磁片上快取取得較低流量的頁面。 或者, 您可以針對呈現的頁面快取每個不同的組合, 但使用分散式快取, 以便從前端 Web 服務器卸載記憶體耗用量。

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>自動啟動 Web 應用程式

某些 Web 應用程式需要載入大量資料, 或在服務第一個要求之前執行昂貴的初始化處理。 在舊版的 ASP.NET 中, 在這些情況下, 您必須設計自訂方法來「喚醒」 ASP.NET 應用程式, 然後在檔案中`Global.asax`的*應用\_程式載入*方法期間執行初始化程式碼。

在 Windows Server 2008 R2 上的 IIS 7.5 上執行 ASP.NET 4 時, 可直接解決此案例的新擴充功能稱為*自動啟動*。 自動啟動功能提供控制的方法來啟動應用程式集區、初始化 ASP.NET 應用程式, 然後接受 HTTP 要求。

> [!NOTE] 
> 
> IIS 7.5 的 IIS 應用程式準備模組
> 
> IIS 小組已發行 IIS 7.5 應用程式準備模組的第一個 Beta 測試版本。 這可讓您更輕鬆地啟動應用程式, 而不是先前所述。 您不需要撰寫自訂程式碼, 而是在 Web 應用程式接受來自網路的要求之前, 指定要執行的資源 Url。 這項準備工作會在 IIS 服務啟動時執行 (如果您將 IIS 應用程式集區設定為*AlwaysRunning*), 以及 iis 工作者進程回收的時間。 在回收期間, 舊的 IIS 背景工作進程會繼續執行要求, 直到新產生的背景工作進程完全準備就緒為止, 讓應用程式不會因為 unprimed 快取而遇到中斷或其他問題。 請注意, 此模組適用于任何版本的 ASP.NET, 從2.0 版開始。
> 
> 如需詳細資訊, 請參閱 IIS.net 網站上的[應用程式暖開機](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)。 如需說明如何使用準備功能的逐步解說, 請參閱 IIS.net 網站上[的使用 IIS 7.5 應用程式準備模組的消費者入門](https://www.iis.net/learn/manage)。

若要使用自動啟動功能, iis 系統管理員會將 iis 7.5 中的應用程式集區設定為使用檔案中`applicationHost.config`的下列設定自動啟動:

[!code-xml[Main](overview/samples/sample5.xml)]

因為單一應用程式集區可以包含多個應用程式, 所以您可以使用檔案中`applicationHost.config`的下列設定, 指定要自動啟動的個別應用程式:

[!code-xml[Main](overview/samples/sample6.xml)]

當 iis 7.5 伺服器是冷啟動或回收個別應用程式集區時, iis 7.5 會使用檔案中`applicationHost.config`的資訊來判斷需要自動啟動的 Web 應用程式。 針對每個標示為要自動啟動的應用程式, IIS 7.5 會將要求傳送至 ASP.NET 4, 以在應用程式暫時不接受 HTTP 要求的狀態下啟動應用程式。 當它處於此狀態時, ASP.NET 會具現化*serviceAutoStartProvider*屬性所定義的類型 (如前一個範例所示), 並呼叫其公用進入點。

您可以藉由執行*IProcessHostPreloadClient*介面, 建立具有必要進入點的受控自動啟動類型, 如下列範例所示:

[!code-csharp[Main](overview/samples/sample7.cs)]

當您的初始化程式碼在*預先載入*的方法中執行, 且方法傳回之後, ASP.NET 應用程式就可以開始處理要求。

透過將自動啟動新增至 IIS .5 和 ASP.NET 4, 您現在有一個定義完善的方法, 可在處理第一個 HTTP 要求之前執行昂貴的應用程式初始化。 例如, 您可以使用新的「自動啟動」功能來初始化應用程式, 然後發出應用程式已初始化且準備接受 HTTP 流量的負載平衡器。

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>永久重新導向頁面

Web 應用程式在一段時間前後移動頁面和其他內容是常見的作法, 這可能會導致搜尋引擎中的過時連結累積。 在 ASP.NET 中, 開發人員通常會使用回應來處理舊 Url 的要求 *。重新導向*方法會將要求轉送至新的 url。 不過, 重新*導向*方法會發出 HTTP 302 找到 (暫時重新導向) 回應, 而當使用者嘗試存取舊的 url 時, 就會產生額外的 HTTP 來回行程。

ASP.NET 4 新增了新的*RedirectPermanent* helper 方法, 可讓您輕鬆地發出 HTTP 301 已移動的永久回應, 如下列範例所示:

[!code-csharp[Main](overview/samples/sample8.cs)]

可辨識永久重新導向的搜尋引擎和其他使用者代理程式將會儲存與內容相關聯的新 URL, 以排除瀏覽器暫時重新導向所不必要的來回行程。

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>縮小會話狀態

ASP.NET 提供兩個預設選項, 可讓您在 Web 伺服陣列中儲存會話狀態: 叫用跨進程會話狀態伺服器的會話狀態提供者, 以及將資料儲存在 Microsoft SQL Server 資料庫中的會話狀態提供者。 因為這兩個選項都牽涉到在 Web 應用程式的背景工作進程外部儲存狀態資訊, 所以必須在將會話狀態傳送到遠端存放之前進行序列化。 視開發人員在會話狀態中儲存多少資訊而定, 序列化資料的大小可能會變得相當大。

ASP.NET 4 為這兩種跨進程會話狀態提供者引進了新的壓縮選項。 當下列範例中顯示的*compressionEnabled*設定選項設為*true*時, ASP.NET 會使用 .NET Framework 的 GZipStream 類別來壓縮 (和解壓縮) 序列化的會話狀態 *。* .

[!code-xml[Main](overview/samples/sample9.xml)]

只要將新的屬性新增至`Web.config`檔案, 在 Web 服務器上具有備用 CPU 週期的應用程式就能大幅降低序列化會話狀態資料的大小。

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>擴充允許的 Url 範圍

ASP.NET 4 引進了擴充應用程式 Url 大小的新選項。 舊版的 ASP.NET 會根據 NTFS 檔案路徑限制, 限制 URL 路徑長度為260個字元。 在 ASP.NET 4 中, 您可以選擇使用兩個新的*HTTPRuntime*設定屬性來增加 (或減少) 應用程式適用的此限制。 下列範例會顯示這些新屬性。

[!code-xml[Main](overview/samples/sample10.xml)]

若要允許長或短的路徑 （不包含通訊協定、 伺服器名稱，以及查詢字串之 url 的部分），修改 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 屬性。 若要允許長或短的查詢字串，修改的值 *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 屬性。

ASP.NET 4 也可讓您設定 URL 字元檢查所使用的字元。 當 ASP.NET 在 URL 的路徑部分中找到不正確字元時, 它會拒絕要求併發出 HTTP 400 錯誤。 在舊版的 ASP.NET 中, URL 字元檢查僅限於一組固定的字元。 在 ASP.NET 4 中, 您可以使用*HTTPRuntime* configuration 元素的新*requestPathInvalidCharacters*屬性來自訂一組有效的字元, 如下列範例所示:

[!code-xml[Main](overview/samples/sample11.xml)]

根據預設, *requestPathInvalidCharacters*屬性會將八個字元定義為無效。 (在預設指派給*requestPathInvalidCharacters*的字串&lt;中, 小於 ()、大於 (&gt;) 和連字號 (&amp;) 字元會進行編碼, 因為`Web.config`檔案是 XML 檔案)。您可以視需要自訂一組不正確字元。

> [!NOTE]
> 請注意, ASP.NET 4 一律會拒絕包含 ASCII 範圍0x00 至0x1F 字元的 URL 路徑, 因為這些是 IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)) 的 RFC 2396 中所定義的無效 url 字元。 在執行 IIS 6 或更新版本的 Windows Server 上, HTTP.sys 通訊協定設備磁碟機會自動拒絕含有這些字元的 Url。

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>可延伸的要求驗證

ASP.NET 要求驗證會搜尋傳入 HTTP 要求資料, 尋找經常用於跨網站腳本 (XSS) 攻擊的字串。 如果找到潛在的 XSS 字串, 要求驗證會將可疑的字串加上旗標, 並傳回錯誤。 內建的要求驗證只有在發現 XSS 攻擊中最常見的字串時才會傳回錯誤。 先前嘗試讓 XSS 驗證更加積極, 會導致太多誤報。 不過, 客戶可能會想要以更積極的要求進行驗證, 或相反地可能想要為特定頁面或特定類型的要求, 刻意放寬 XSS 檢查。

在 ASP.NET 4 中, 要求驗證功能已成為可延伸, 因此您可以使用自訂的要求驗證邏輯。 若要擴充要求驗證, 請建立衍生自*Util. RequestValidator*類型的類別, 並設定應用程式 (在檔案的*HTTPRuntime* `Web.config`區段中) 以使用自訂類型。 下列範例顯示如何設定自訂要求驗證類別:

[!code-xml[Main](overview/samples/sample12.xml)]

新的*requestValidationType*屬性需要標準 .NET Framework 類型識別碼字串, 指定提供自訂要求驗證的類別。 針對每個要求, ASP.NET 會叫用自訂類型來處理傳入 HTTP 要求資料的每個部分。 傳入 URL、所有 HTTP 標頭 (cookie 和自訂標頭) 和實體主體全都可供自訂要求驗證類別檢查, 如下列範例所示:

[!code-csharp[Main](overview/samples/sample13.cs)]

如果您不想要檢查傳入 HTTP 資料的某個部分, 要求驗證類別可以切換回, 讓 ASP.NET 預設要求驗證執行, 方法是直接呼叫*base。IsValidRequestString。*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>物件快取和物件快取擴充性

自其第一版起, ASP.NET 已包含強大的記憶體中物件快取 (*system.web. Caching*)。 快取的實行已經很熱門, 已在非 Web 應用程式中使用。 不過, Windows Forms 或 WPF 應用程式`System.Web.dll`只需要包含的參考, 才能夠使用 ASP.NET 物件快取。

為了讓快取可供所有應用程式使用, .NET Framework 4 引進了新的元件、新的命名空間、一些基底類型, 以及具體的快取執行。 新`System.Runtime.Caching.dll`的元件會在 system.servicemodel 命名空間中包含新的快取 API。 命名空間包含兩個核心的類別集合:

- 抽象類別型, 提供建立任何自訂快取實作為類型的基礎。
- 具體的記憶體內建物件快取實作為 ( *MemoryCache*類別)。

新的*MemoryCache*類別會密切地在 ASP.NET 快取上進行模型化, 並與 ASP.NET 共用大部分的內部快取引擎邏輯。 雖然*系統*中的公用快取 api 已更新為支援自訂快取的開發, 但如果您已使用 ASP.NET 快取物件, 您會在新的 api 中找到熟悉的概念。

若要深入討論新的*MemoryCache*類別和支援的基底 api, 則需要整份檔。 不過, 下列範例可讓您瞭解新的快取 API 如何運作。 此範例是針對 Windows Forms 應用程式所撰寫, 而不會`System.Web.dll`有任何相依性。

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>可擴充的 HTML、URL 和 HTTP 標頭編碼

在 ASP.NET 4 中, 您可以建立下列一般文字編碼工作的自訂編碼常式:

- HTML 編碼。
- URL 編碼。
- HTML 屬性編碼。
- 編碼輸出 HTTP 標頭。

您可以從新的*Util HttpEncoder*類型衍生, 然後將 ASP.NET 設定為使用檔案的*HTTPRuntime* `Web.config`區段中的自訂類型, 以建立自訂編碼器, 如下列範例所示:

[!code-xml[Main](overview/samples/sample15.xml)]

設定自訂編碼器之後, 每當呼叫*HTTPutility.htmlencode*或*HttpServerUtility*類別的公用編碼方法時, ASP.NET 就會自動呼叫自訂編碼的執行。 這可讓 Web 開發小組的一個部分建立自訂編碼器來執行嚴格的字元編碼, 而 Web 開發小組的其餘部分則會繼續使用公用 ASP.NET 編碼 Api。 藉由在*HTTPRuntime*元素中集中設定自訂編碼器, 您可以保證來自公用 ASP.NET 編碼 api 的所有文字編碼呼叫都會透過自訂編碼器來路由傳送。

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>單一工作者進程中個別應用程式的效能監視

為了增加可裝載于單一伺服器上的網站數目, 許多主控者會在單一背景工作進程中執行多個 ASP.NET 應用程式。 不過, 如果有多個應用程式使用單一共用背景工作進程, 伺服器系統管理員就很難以識別遇到問題的個別應用程式。

ASP.NET 4 利用 CLR 引進的新資源監視功能。 若要啟用這項功能, 您可以將下列 XML 設定程式碼片段`aspnet.config`新增至設定檔。

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> `aspnet.config`請注意, 檔案位於 .NET Framework 安裝所在的目錄中。 這不`Web.config`是檔案。

當*appDomainResourceMonitoring*功能已啟用時, [ASP.NET 應用程式] 效能類別中會提供兩個新的效能計數器: [ *% 受控的處理器時間*] 和 [*使用的受控記憶體*]。 這兩個效能計數器都使用新的 CLR 應用程式網域資源管理功能來追蹤估計的 CPU 時間, 以及個別 ASP.NET 應用程式的受控記憶體使用率。 因此, 使用 ASP.NET 4, 系統管理員現在可以更精細地查看單一背景工作進程中執行之個別應用程式的資源耗用量。

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>多目標

您可以建立以特定 .NET Framework 版本為目標的應用程式。 在 ASP.NET 4 中, 檔案之`Web.config` *編譯*元素中的新屬性可讓您以 .NET Framework 4 和更新版本為目標。 如果您明確地以 .NET Framework 4 為目標, 而且您在檔案中`Web.config`包含選擇性元素 (例如*system.object*的專案), 則 .NET Framework 4 的這些元素必須是正確的。 (如果您未明確以 .NET Framework 4 為目標, 則會從缺少檔案中`Web.config`的專案來推斷目標架構)。

下列範例示範如何在檔案的*編譯* `Web.config`元素中使用*targetFramework*屬性。

[!code-xml[Main](overview/samples/sample17.xml)]

請注意下列有關以特定 .NET Framework 版本為目標的:

- 在 .NET Framework 4 應用程式集區中, 如果`Web.config`檔案未包含*targetFramework* `Web.config`屬性或檔案遺失, ASP.NET 組建系統會假設 .NET Framework 4 做為目標。 (您可能必須對應用程式進行編碼變更, 使其在 .NET Framework 4 之下執行)。
- 如果您包含*targetFramework*屬性, 而且如果在檔案中 `Web.config`定義了 system.web 元素, 則此檔案必須包含 .NET Framework 4 的正確專案。
- 如果您使用*aspnet\_編譯器*命令來先行編譯您的應用程式 (例如在組建環境中), 您必須使用目標 framework 的正確版本*aspnet\_編譯器*命令。 使用隨附于 .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) 的編譯器, 針對 .NET Framework 3.5 和更早版本進行編譯。 使用 .NET Framework 4 隨附的編譯器來編譯使用該架構建立的應用程式, 或使用較新的版本。
- 在執行時間, 編譯器會使用安裝在電腦上的最新架構元件 (因此在 GAC 中)。 如果稍後會對架構進行更新 (例如, 已安裝假設版本 4.1), 您可以使用較新版本 framework 中的功能, 即使*targetFramework*屬性是以較低的版本 (例如 4.0) 為目標也一樣。 (不過, 在 Visual Studio 2010 的設計階段, 或當您使用*aspnet\_編譯器*命令時, 使用較新的架構功能會導致編譯器錯誤)。

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>Web Forms 和 MVC 中包含的 jQuery

Web Forms 和 MVC 的 Visual Studio 範本都包含開放原始碼的 jQuery 程式庫。 當您建立新的網站或專案時, 會建立包含下列3個檔案的 [腳本] 資料夾:

- Jquery-1.7.2.min.js 1.4.1-jQuery 程式庫的人們可讀取、unminified 版本。
- Jquery-1.7.2.min.js 14.1. min .js – jQuery 程式庫的縮減版本。
- Jquery-1.7.2.min.js 1.4.1-vsdoc-jQuery 程式庫的 Intellisense 檔檔案。

在開發應用程式時包含 jQuery 的 unminified 版本。 包含適用于生產應用程式的 jQuery 縮減版本。

例如, 下列 Web form 頁面說明如何使用 jQuery, 將 ASP.NET TextBox 控制項的背景色彩變更為黃色 (如果有焦點)。

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>內容傳遞網路支援

Microsoft Ajax 內容傳遞網路 (CDN) 可讓您輕鬆地將 ASP.NET Ajax 和 jQuery 腳本新增至您的 Web 應用程式。 例如, 您可以開始使用 jQuery 程式庫, 只要將`<script>`標記新增至您的頁面, 以指向 Ajax.microsoft.com, 如下所示:

[!code-html[Main](overview/samples/sample19.html)]

藉由利用 Microsoft Ajax CDN, 您可以大幅提升 Ajax 應用程式的效能。 Microsoft Ajax CDN 的內容會在位於世界各地的伺服器上進行快取。 此外, Microsoft Ajax CDN 可讓瀏覽器重複使用位於不同網域中之網站的快取 JavaScript 檔案。

如果您需要使用安全通訊端層來服務網頁, Microsoft Ajax 內容傳遞網路支援 SSL (HTTPS)。

當 CDN 無法使用時, 請執行 fallback。 測試回退。

若要深入瞭解 Microsoft Ajax CDN, 請造訪下列網站:

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager 支援 Microsoft Ajax CDN。 只要設定一個屬性 (EnableCdn 屬性), 您就可以從 CDN 抓取所有 ASP.NET framework JavaScript 檔案:

[!code-aspx[Main](overview/samples/sample20.aspx)]

當您將 EnableCdn 屬性設定為 true 值之後, ASP.NET 架構將會從 CDN 抓取所有的 ASP.NET framework JavaScript 檔案, 包括用於驗證和 UpdatePanel 的所有 JavaScript 檔案。 設定這個屬性可能會對 web 應用程式的效能產生顯著的影響。

您可以使用 WebResource 屬性來設定自己的 JavaScript 檔案的 CDN 路徑。 新的 CdnPath 屬性會指定當您將 EnableCdn 屬性設定為 true 值時, 所使用的 CDN 路徑:

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager 明確腳本

在過去, 如果您使用 ASP.NET ScriptManger, 則必須載入整個整合型 ASP.NET Ajax 程式庫。 藉由利用新的 AjaxFrameworkMode 屬性, 您可以精確地控制要載入的 ASP.NET Ajax 程式庫元件, 並只載入所需 ASP.NET Ajax 程式庫的元件。

AjaxFrameworkMode 屬性可以設定為下列值:

- 已啟用--指定 ScriptManager 控制項自動包含 Microsoftajax.debug.js 腳本檔案, 這是每個核心架構腳本的合併腳本檔案 (舊版行為)。
- Disabled--指定停用所有的 Microsoft Ajax 腳本功能, 而且 ScriptManager 控制項不會自動參考任何腳本。
- Explicit--指定您將明確包含網頁所需之個別 framework core 腳本檔案的腳本參考, 而且您將會包含每個腳本檔案所需之相依性的參考。

例如, 如果您將 AjaxFrameworkMode 屬性設定為 Explicit 值, 則可以指定所需的特定 ASP.NET Ajax 元件腳本:

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Web Form

Web form 在發行 ASP.NET 1.0 之後已經是 ASP.NET 的核心功能。 ASP.NET 4 的這方面有許多增強功能, 包括下列各項:

- 設定*中繼*標記的能力。
- 更充分掌控檢視狀態。
- 更簡單的方式來使用瀏覽器功能。
- 支援搭配 Web Forms 使用 ASP.NET 路由。
- 對產生的識別碼有更大的控制權。
- 能夠在資料控制中保存選取的資料列。
- 進一步控制*FormView*和*ListView*控制項中呈現的 HTML。
- 篩選資料來源控制項的支援。

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>使用 MetaKeywords 和 MetaDescription 屬性設定中繼標記

ASP.NET 4 會將兩個屬性新增至*頁面*類別*MetaKeywords*和*MetaDescription*。 這兩個屬性代表頁面中對應的*中繼*標記, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample23.aspx)]

這兩個屬性的運作方式與頁面的 [*標題*] 屬性相同。 它們會遵循下列規則:

1. 如果*標頭*專案中沒有與屬性名稱相符的*中繼*標記 (也就是*MetaKeywords* , name = "關鍵字", 代表 MetaDescription, 表示尚未設定這些屬性 *。* ), 在轉譯時, 會將*中繼*標記加入至頁面。
2. 如果已經有使用這些名稱的*中繼*標記, 這些屬性會作為現有標記內容的 get 和 set 方法。

您可以在執行時間設定這些屬性, 這可讓您從資料庫或其他來源取得內容, 並可讓您以動態方式設定標記, 以描述特定頁面的用途。

您也可以在 Web form 頁面標記的頂端, 設定 *@ Page*指示詞中的*關鍵字*和*Description*屬性, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample24.aspx)]

這會覆寫已在頁面中宣告的*中繼*標記內容 (如果有的話)。

Description *meta*標記的內容是用來改善 Google 中的搜尋清單預覽。 (如需詳細資訊, 請參閱在 Google 網站管理員中心的 blog 中,[使用中繼描述來改善程式碼片段改造](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html))。Google 和 Windows Live Search 不會針對任何專案使用關鍵字的內容, 但其他搜尋引擎可能會。 如需詳細資訊, 請參閱搜尋引擎指南網站上的[中繼關鍵字建議](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)。

這些新屬性是簡單的功能, 但可讓您不需要手動新增這些內容, 或撰寫自己的程式碼來建立*中繼*標記。

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>啟用個別控制項的檢視狀態

根據預設, 頁面會啟用 [檢視狀態], 結果是頁面上的每個控制項都可能儲存檢視狀態, 即使應用程式不需要它也一樣。 檢視狀態資料會包含在頁面產生的標記中, 並會增加將頁面傳送至用戶端並將其回傳所需的時間量。 儲存比所需更多的檢視狀態可能會造成明顯的效能降低。 在舊版的 ASP.NET 中, 開發人員可以停用個別控制項的檢視狀態, 以便減少頁面大小, 但必須針對個別控制項明確地執行此動作。 在 ASP.NET 4 中, Web 服務器控制項包含*ViewStateMode*屬性, 可讓您依預設停用 view 狀態, 然後只針對在頁面中需要它的控制項加以啟用。

*ViewStateMode*屬性會採用具有三個值的列舉:*Enabled*、 *Disabled*和*Inherit*。 [*已啟用*] 會啟用該控制項的檢視狀態, 以及任何設定為*繼承*或未設定任何子控制項的。 [*已停用*] 會停用檢視狀態, 而 [*繼承*] 則會指定控制項使用父控制項的*ViewStateMode*設定。

下列範例顯示*ViewStateMode*屬性的運作方式。 下列頁面中控制項的標記和程式碼包含*ViewStateMode*屬性的值:

[!code-aspx[Main](overview/samples/sample25.aspx)]

如您所見, 程式碼會停用 PlaceHolder1 控制項的檢視狀態。 子 label1 控制項會繼承這個屬性值 (*繼承*是控制項的*ViewStateMode*的預設值), 因此不會儲存任何檢視狀態。 在 PlaceHolder2 控制項中, *ViewStateMode*會設為*Enabled*, 因此 label2 會繼承這個屬性並儲存檢視狀態。 第一次載入頁面時, 這兩個*標籤*控制項的*Text*屬性會設定為字串 "[DynamicValue]"。

這些設定的作用是當頁面第一次載入時, 瀏覽器中會顯示下列輸出:

禁止`: [DynamicValue]`

後`[DynamicValue]`

但是在回傳之後, 會顯示下列輸出:

禁止`: [DeclaredValue]`

後`[DynamicValue]`

Label1 控制項 (其*ViewStateMode*值設定為*停用*) 並未保留在程式碼中設定的值。 不過, label2 控制項 (其*ViewStateMode*值設為 [*已啟用*]) 已保留其狀態。

您也可以在 *@ Page*指示詞中設定*ViewStateMode* , 如下列範例所示:

[!code-aspx[Main](overview/samples/sample26.aspx)]

*Page*類別只是另一個控制項;它會作為頁面中所有其他控制項的父控制項。 *ViewStateMode*的預設值會針對*Page*的實例*啟用*。 因為控制項預設為*繼承*, 除非您在頁面或控制項層級設定*ViewStateMode* , 否則控制項將會繼承*已啟用*的屬性值。

*ViewStateMode*屬性的值會決定只有在*EnableViewState*屬性設定為*true*時, 才會維護檢視狀態。 如果 [ *EnableViewState* ] 屬性設定為 [ *false*], 即使*ViewStateMode*設定為 [*已啟用*], 也不會保留 view 狀態。

這項功能適用于主版頁面中的*ContentPlaceHolder*控制項, 您可以在其中將主版頁面的*ViewStateMode*設定為*停用*, 然後個別針對*ContentPlaceHolder*控制項加以啟用, 然後再進行包含需要 view 狀態的控制項。

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>瀏覽器功能的變更

ASP.NET 會使用稱為「*瀏覽器」功能*的功能, 來決定使用者用來流覽網站的瀏覽器功能。 瀏覽器功能是由*HttpBrowserCapabilities*物件表示 (由*要求*所公開)。 例如, 您可以使用*HttpBrowserCapabilities*物件來判斷目前瀏覽器的類型和版本是否支援特定版本的 JavaScript。 或者, 您可以使用*HttpBrowserCapabilities*物件來判斷要求是否源自行動裝置。

*HttpBrowserCapabilities*物件是由一組瀏覽器定義檔案所驅動。 這些檔案包含特定瀏覽器功能的相關資訊。 在 ASP.NET 4 中, 這些瀏覽器定義檔案已更新為包含最近推出的瀏覽器和裝置的相關資訊, 例如 Google Chrome、Research 在動作中的 BlackBerry smartphone 和 Apple iPhone。

下列清單顯示新的瀏覽器定義檔案:

- *blackberry.browser*
- *chrome.browser*
- *Default.browser*
- *firefox.browser*
- *gateway.browser*
- *generic.browser*
- *ie.browser*
- *iemobile.browser*
- *iphone.browser*
- *opera.browser*
- *safari.browser*

#### <a name="using-browser-capabilities-providers"></a>使用瀏覽器功能提供者

在 ASP.NET 3.5 版 Service Pack 1 中, 您可以使用下列方式定義瀏覽器的功能:

- 在電腦層級, 您可以建立或更新`.browser`下列資料夾中的 XML 檔案:

- [!code-console[Main](overview/samples/sample27.cmd)]

- 定義瀏覽器功能之後, 您可以從 Visual Studio 命令提示字元執行下列命令, 以便重建瀏覽器功能元件, 並將它新增至 GAC:

- [!code-console[Main](overview/samples/sample28.cmd)]

- 針對個別應用程式, 您可以在`.browser`應用程式的`App_Browsers`資料夾中建立檔案。

這些方法需要您變更 XML 檔案, 而針對電腦層級的變更, 您必須在執行 aspnet\_regbrowsers 處理常式之後重新開機應用程式。

ASP.NET 4 包含一個稱為*瀏覽器功能提供者*的功能。 正如其名, 這可讓您建立一個提供者, 讓您能夠使用自己的程式碼來判斷瀏覽器的功能。

在實務上, 開發人員通常不會定義自訂瀏覽器功能。 瀏覽器檔案很難更新, 更新程式的程式相當複雜, 而且檔案的 XML 語法`.browser`可能很複雜, 無法使用和定義。 若有常見的瀏覽器定義語法, 或包含最新瀏覽器定義的資料庫, 或甚至是這類資料庫的 Web 服務, 則會讓此程式變得更容易。 新的瀏覽器功能提供者功能可讓協力廠商開發人員能夠和實際執行這些案例。

使用新的 ASP.NET 4 瀏覽器功能提供者功能的主要方法有兩種: 擴充 ASP.NET 瀏覽器功能定義功能, 或完全取代它。 下列各節將先說明如何取代功能, 以及如何加以擴充。

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>取代 ASP.NET 瀏覽器功能功能

若要完全取代 ASP.NET 的瀏覽器功能定義功能, 請遵循下列步驟:

1. 建立衍生自*HttpCapabilitiesProvider*的提供者類別, 並覆寫*GetBrowserCapabilities*方法, 如下列範例所示: 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    此範例中的程式碼會建立新的*HttpBrowserCapabilities*物件, 只指定名為 browser 的功能, 並將該功能設定為 MyCustomBrowser。
2. 向應用程式註冊提供者。 

    若要將提供者與應用程式搭配使用, 您必須將*provider*屬性加入至 `Web.config`或`Machine.config`檔案中的 browserCaps 區段。 (您也可以針對應用程式中的特定目錄, 定義*location*元素中的提供者屬性, 例如在特定行動裝置的資料夾中)。下列範例顯示如何在設定檔中設定*provider*屬性:

    [!code-xml[Main](overview/samples/sample30.xml)]

    註冊新瀏覽器功能定義的另一種方式是使用程式碼, 如下列範例所示:

    [!code-csharp[Main](overview/samples/sample31.cs)]

    此代碼必須在檔案的*應用\_程式啟動*事件`Global.asax`中執行。 對*BrowserCapabilitiesProvider*類別所做的任何變更, 都必須在應用程式中的任何程式碼執行之前進行, 以確保快取會針對已解析的*HttpCapabilitiesBase*物件維持有效的狀態。

#### <a name="caching-the-httpbrowsercapabilities-object"></a>快取 HttpBrowserCapabilities 物件

上述範例有一個問題, 這是每次叫用自訂提供者以取得*HttpBrowserCapabilities*物件時, 就會執行程式碼。 這可能會在每次要求期間發生多次。 在此範例中, 提供者的程式碼不會執行太多動作。 不過, 如果自訂提供者中的程式碼執行大量工作以取得*HttpBrowserCapabilities*物件, 這可能會影響效能。 若要避免發生這種情況, 您可以快取*HttpBrowserCapabilities*物件。 請遵循下列步驟：

1. 建立衍生自*HttpCapabilitiesProvider*的類別, 如下列範例所示: 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    在此範例中, 程式碼會藉由呼叫自訂 BuildCacheKey 方法來產生快取索引鍵, 並藉由呼叫自訂的 GetCacheTime 方法取得快取的時間長度。 然後, 此程式碼會將已解析的*HttpBrowserCapabilities*物件新增至快取。 您可以從快取中抓取物件, 並重複使用自訂提供者的後續要求。
2. 如先前的程式所述, 向應用程式註冊提供者。

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>擴充 ASP.NET 瀏覽器功能功能

上一節說明如何在 ASP.NET 4 中建立新的*HttpBrowserCapabilities*物件。 您也可以將新的瀏覽器功能定義加入至已 ASP.NET 的使用者, 以擴充 ASP.NET 瀏覽器功能的功能。 您不需要使用 XML 瀏覽器定義即可執行此動作。 下列程式顯示如何。

1. 建立衍生自*HttpCapabilitiesEvaluator*的類別, 並覆寫*GetBrowserCapabilities*方法, 如下列範例所示: 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    此程式碼會先使用 ASP.NET 瀏覽器功能功能來嘗試識別瀏覽器。 不過, 如果找不到根據要求中定義的資訊來識別的瀏覽器 (亦即, 如果*HttpBrowserCapabilities*物件的*browser*屬性是字串 "Unknown"), 則程式碼會呼叫自訂提供者 (MyBrowserCapabilitiesEvaluator) 以識別瀏覽器。
2. 如先前範例所述, 向應用程式註冊提供者。

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>藉由將新功能新增至現有的功能定義來擴充瀏覽器功能功能

除了建立自訂瀏覽器定義提供者, 以及動態建立新的瀏覽器定義以外, 您還可以使用其他功能來擴充現有的瀏覽器定義。 這可讓您使用接近所需的定義, 但只缺少一些功能。 若要這麼做，請使用下列步驟。

1. 建立衍生自*HttpCapabilitiesEvaluator*的類別, 並覆寫*GetBrowserCapabilities*方法, 如下列範例所示: 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    此範例程式碼會使用下列程式碼, 擴充現有的 ASP.NET *HttpCapabilitiesEvaluator*類別, 並取得符合目前要求定義的*HttpBrowserCapabilities*物件:

    [!code-csharp[Main](overview/samples/sample35.cs)]

    然後, 程式碼可以新增或修改此瀏覽器的功能。 有兩種方式可以指定新的瀏覽器功能:

    - 將索引鍵/值組新增至*IDictionary*物件, 而此物件是由*HttpCapabilitiesBase*物件的*功能*屬性所公開。 在上述範例中, 程式碼會新增名為多點觸控且值為*true*的功能。
    - 設定*HttpCapabilitiesBase*物件的現有屬性。 在上述範例中, 程式碼會將 [*框架*] 屬性設定為 [ *true*]。 此屬性只是由 [*功能*] 屬性公開之*IDictionary*物件的存取子。 

        > [!NOTE]
        > 請注意, 此模型適用于*HttpBrowserCapabilities*的任何屬性, 包括控制介面卡。
2. 如先前的程式所述, 向應用程式註冊提供者。

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4 中的路由

ASP.NET 4 加入了使用 Web form 路由的內建支援。 路由可讓您設定應用程式, 以接受未對應至實體檔案的要求 Url。 相反地, 您可以使用路由來定義對使用者有意義的 Url, 並協助您的應用程式使用搜尋引擎優化 (SEO)。 例如, 在現有的應用程式中顯示產品類別目錄之頁面的 URL 可能會如下列範例所示:

[!code-console[Main](overview/samples/sample36.cmd)]

藉由使用路由, 您可以將應用程式設定為接受下列 URL 來呈現相同的資訊:

[!code-console[Main](overview/samples/sample37.cmd)]

從 ASP.NET 3.5 SP1 開始已提供路由。 (如需如何在 ASP.NET 3.5 SP1 中使用路由的範例, 請參閱此專案[使用具有 WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "標題的")路由專案。 在 Phil Haack 的 blog 上)。不過, ASP.NET 4 包含一些功能, 可讓您更輕鬆地使用路由, 包括下列各項:

- *PageRouteHandler*類別, 這是您在定義路由時所使用的簡單 HTTP 處理常式。 類別會將資料傳遞至要求所路由傳送至的頁面。
- 新的屬性*HttpRequest. RequestCoNtext*和*RouteData* (這是*HttpRequest. RequestCoNtext.* RouteData 物件的 proxy)。 這些屬性可讓您更輕鬆地存取從路由傳遞的資訊。
- 下列新的運算式產生器 (定義于 RouteUrlExpressionBuilder 和*RouteValueExpressionBuilder*中): ( *system* 。
- *RouteUrl*, 可提供簡單的方式來建立對應至 ASP.NET 伺服器控制項內之路由 URL 的 URL。
- *RouteValue*, 提供從*routecoNtext.routedata*物件解壓縮資訊的簡單方式。
- *RouteParameter*類別, 可讓您更輕鬆地將*routecoNtext.routedata*物件中包含的資料傳遞至資料來源控制項的查詢 (類似于[*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx))。

#### <a name="routing-for-web-forms-pages"></a>Web Forms 網頁的路由

下列範例示範如何使用*route*類別的新*MapPageRoute*方法來定義 Web Forms 路由:

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4 引進了*MapPageRoute*方法。 下列範例相當於前一個範例所示的 SearchRoute 定義, 但使用*PageRouteHandler*類別。

[!code-csharp[Main](overview/samples/sample39.cs)]

範例中的程式碼會將路由對應至實體頁面 (在第一個路由中, `~/search.aspx`到)。 第一個路由定義也會指定名為 searchterm 的參數應該從 URL 中解壓縮並傳遞至頁面。

*MapPageRoute*方法支援下列方法多載:

- *MapPageRoute (字串 routeName, 字串 routeUrl, 字串 physicalFile, bool checkPhysicalUrlAccess)*
- *MapPageRoute (字串 routeName, 字串 routeUrl, 字串 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 預設值)*
- *MapPageRoute (字串 routeName, 字串 routeUrl, 字串 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 預設值, RouteValueDictionary 條件約束)*

*CheckPhysicalUrlAccess*參數會指定路由是否應檢查要路由至之實體頁面 (在此案例中為 search .aspx) 的安全性許可權, 以及連入 URL (在此案例中為 search/{searchterm}) 的許可權。 如果*checkPhysicalUrlAccess*的值為*false*, 則只會檢查傳入 URL 的許可權。 這些許可權會使用如下的`Web.config`設定定義于檔案中:

[!code-xml[Main](overview/samples/sample40.xml)]

在範例設定中, 所有使用者的實體頁面`search.aspx`存取權除外, 除非是系統管理員角色的人員。 當*checkPhysicalUrlAccess*參數設定為*true* (這是其預設值) 時, 只允許系統管理員使用者存取 URL/search/{searchterm}, 因為實體頁面搜尋 .aspx 僅限於該角色中的使用者。 如果*checkPhysicalUrlAccess*設定為*false* , 且網站已如前一個範例所示設定, 則允許所有已驗證的使用者存取 URL/search/{searchterm}。

#### <a name="reading-routing-information-in-a-web-forms-page"></a>讀取 Web Forms 頁面中的路由資訊

在 Web form 實體頁面的程式碼中, 您可以使用兩個新的屬性, 存取路由已從 URL (或另一個物件已新增至*RouteData*物件的其他資訊) 中解壓縮的資訊:*HttpRequest. RequestCoNtext*和*RouteData*。 (*Page. RouteData*會包裝*HttpRequest. RequestCoNtext. RouteData*)。下列範例顯示如何使用*RouteData*。

[!code-csharp[Main](overview/samples/sample41.cs)]

此程式碼會將傳遞給 searchterm 參數的值 (如稍早的範例路由中所定義) 解壓縮。 請考慮下列要求 URL:

[!code-console[Main](overview/samples/sample42.cmd)]

提出此要求時, 會在`search.aspx`頁面中轉譯「scott」一詞。

#### <a name="accessing-routing-information-in-markup"></a>存取標記中的路由資訊

上一節所述的方法示範如何在 Web form 頁面的程式碼中取得路由資料。 您也可以在標記中使用運算式, 讓您存取相同的資訊。 運算式產生器是使用宣告式程式碼的強大且簡潔的方式。 (如需詳細資訊, 請參閱 Phil Haack 的 blog 的[自訂表格達式](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)產生器中的專案 Express)。

ASP.NET 4 包含兩個用於 Web 表單路由的新運算式產生器。 下列範例顯示如何使用它們。

[!code-aspx[Main](overview/samples/sample43.aspx)]

在此範例中, *RouteUrl*運算式是用來定義以路由參數為基礎的 URL。 如此一來, 您就不必將完整的 URL 硬式編碼到標記中, 並讓您稍後變更 URL 結構, 而不需要變更此連結。

根據稍早定義的路由, 此標記會產生下列 URL:

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET 會根據輸入參數自動處理正確的路由 (也就是, 它會產生正確的 URL)。 您也可以在運算式中包含路由名稱, 讓您指定要使用的路由。

下列範例顯示如何使用*RouteValue*運算式。

[!code-aspx[Main](overview/samples/sample45.aspx)]

當包含此控制項的頁面執行時, [scott] 值會顯示在標籤中。

*RouteValue*運算式可讓您輕鬆地在標記中使用路由資料, 並避免必須使用更複雜的頁面。 RouteData ["x"] 標記中的語法。

#### <a name="using-route-data-for-data-source-control-parameters"></a>使用資料來源控制參數的路由資料

*RouteParameter*類別可讓您指定路由資料, 做為資料來源控制項中查詢的參數值。 其[運作方式非常類似](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)于類別, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample46.aspx)]

在此情況下，路由參數 searchterm 的值將用於@companyname中的參數 *選取* 陳述式。

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>設定用戶端識別碼

新的*ClientIDMode*屬性可解決 ASP.NET 中長期的問題, 也就是控制項如何為其轉譯的元素建立*id*屬性。 如果您的應用程式包含參考這些專案的用戶端腳本, 知道轉譯元素的*id*屬性就很重要。

HTML 中針對 Web 服務器控制項轉譯的*id*屬性是根據控制項的*ClientID*屬性來產生。 在 ASP.NET 4 之前, 從*ClientID*屬性產生*id*屬性的演算法, 已連接到具有識別碼的命名容器 (如果有的話), 並在重複控制項 (如資料控制項) 的情況下, 加入前置詞和順序項數. 雖然這一定會保證頁面中控制項的識別碼是唯一的, 但演算法卻導致無法預測的控制項識別碼, 因此很難在用戶端腳本中參考。

新的*ClientIDMode*屬性可讓您更精確地指定如何為控制項產生用戶端識別碼。 您可以設定任何控制項的*ClientIDMode*屬性, 包括網頁的。 可能的設定如下:

- *Autoid predictable* –這相當於用於產生先前版本 ASP.NET 中所使用之*ClientID*屬性值的演算法。
- *Static* –這會指定*ClientID*值會與識別碼相同, 而不會串連父命名容器的識別碼。 這在 Web 使用者控制項中很有用。 因為 Web 使用者控制項可以位在不同的頁面上, 而且位於不同的容器控制項中, 所以很難以針對使用*autoid predictable*演算法的控制項撰寫用戶端腳本, 因為您無法預測識別碼值會是什麼。
- *可預測*–此選項主要是用於使用重複範本的資料控制項。 它會串連控制項的命名容器的 ID 屬性, 但產生的*ClientID*值不會包含 "ctlxxx" 之類的字串。 此設定會與控制項的*ClientIDRowSuffix*屬性搭配運作。 您可以將*ClientIDRowSuffix*屬性設定為資料欄位的名稱, 並使用該欄位的值做為所產生之*ClientID*值的尾碼。 一般來說, 您會使用資料記錄的主鍵做為*ClientIDRowSuffix*值。
- *Inherit* –此設定是控制項的預設行為;它會指定控制項的識別碼產生與其父系相同。

您可以在頁面層級設定*ClientIDMode*屬性。 這會定義目前頁面中所有控制項的預設*ClientIDMode*值。

頁面層級的預設*ClientIDMode*值為*autoid predictable*, 而控制項層級的預設*ClientIDMode*值為*Inherit*。 因此, 如果您未在程式碼中的任何位置設定此屬性, 則所有控制項都會預設為*autoid predictable*演算法。

您可以在 *@ page*指示詞中設定頁面層級的值, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample47.aspx)]

您也可以在設定檔中, 于電腦 (機器) 層級或應用層級設定*ClientIDMode*值。 這會為應用程式中所有頁面上的所有控制項定義預設的*ClientIDMode*設定。 如果您在電腦層級設定值, 它會定義該電腦上所有網站的預設*ClientIDMode*設定。 下列範例顯示設定檔中的*ClientIDMode*設定:

[!code-xml[Main](overview/samples/sample48.xml)]

如先前所述, *ClientID*屬性的值衍生自控制項父系的命名容器。 在某些情況下, 例如當您使用主版頁面時, 控制項最後可能會有類似下列所呈現 HTML 中的識別碼:

[!code-html[Main](overview/samples/sample49.html)]

雖然標記中所顯示的*輸入*專案 (來自*TextBox*控制項) 只是頁面中的兩個命名容器 (嵌套的*ContentPlaceholder*控制項), 但因為主版頁面的處理方式, 所以最終結果是控制項識別碼, 如下所示:

[!code-console[Main](overview/samples/sample50.cmd)]

此識別碼在頁面中保證是唯一的, 但在大部分的情況下, 它會不必要地長時間。 假設您想要縮短轉譯的識別碼長度, 並能夠更充分掌控識別碼的產生方式。 (例如, 您想要排除 "ctlxxx" 前置詞)。達到此目的的最簡單方式是設定*ClientIDMode*屬性, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample51.aspx)]

在此範例中, 最外層的*NamingPanel*專案的*ClientIDMode*屬性設定為*Static* , 而內部*NamingControl*元素的則設為*可預測*。 這些設定會產生下列標記 (頁面的其餘部分和主版頁面會假設與先前範例中的相同):

[!code-html[Main](overview/samples/sample52.html)]

*靜態*設定具有重設最外層*NamingPanel*元素內任何控制項之命名階層的效果, 以及用來排除產生的識別碼中的*ContentPlaceHolder*和*MasterPage*識別碼。 (轉譯專案的*name*屬性不受影響, 因此會保留事件、檢視狀態等的一般 ASP.NET 功能)。重設命名階層的副作用是, 即使您將*NamingPanel*元素的標記移至不同的*ContentPlaceholder*控制項, 呈現的用戶端識別碼仍會保持不變。

> [!NOTE]
> 請注意, 您必須確定呈現的控制項識別碼是唯一的。 如果不是, 它可能會中斷需要個別 HTML 元素之唯一識別碼的任何功能, 例如用戶端*檔. getElementById*函式。

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>在資料繫結控制項中建立可預測的用戶端識別碼

舊版演算法在資料系結清單控制項中為控制項產生的*ClientID*值可能很長, 而且不是真正可預測的。 *ClientIDMode*功能可協助您更充分掌控這些識別碼的產生方式。

下列範例中的標記包含*ListView*控制項:

[!code-aspx[Main](overview/samples/sample53.aspx)]

在上述範例中, *ClientIDMode*和*RowClientIDRowSuffix*屬性是在標記中設定。 *ClientIDRowSuffix*屬性只能用在資料繫結控制項中, 而且其行為會根據您使用的控制項而有所不同。 其差異如下:

- *GridView*控制項: 您可以在資料來源中指定一個或多個資料行的名稱, 這會在執行時間結合以建立用戶端識別碼。 例如, 如果您將*RowClientIDRowSuffix*設定為 "ProductName, ProductId", 呈現專案的控制項識別碼將會具有如下格式:

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView*控制項: 您可以在資料來源中指定附加至用戶端識別碼的單一資料行。 例如, 如果您將*ClientIDRowSuffix*設定為 "ProductName", 呈現的控制項識別碼將會有如下的格式:

- [!code-console[Main](overview/samples/sample55.cmd)]

- 在此情況下, 尾端1是從目前資料項目的產品識別碼衍生而來。

- *中繼器*控制項-此控制項不支援*ClientIDRowSuffix*屬性。 在*中繼器*控制項中, 會使用目前資料列的索引。 當您使用 ClientIDMode = "可預測的"搭配重複項控制項時, 會產生具有下列格式的用戶端識別碼:

- [!code-console[Main](overview/samples/sample56.cmd)]

- 尾端0是目前資料列的索引。

*FormView*和*DetailsView*控制項不會顯示多個資料列, 因此它們不支援*ClientIDRowSuffix*屬性。

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>保存資料控制項中的資料列選取範圍

*GridView*和*ListView*控制項可讓使用者選取資料列。 在舊版的 ASP.NET 中, 選取範圍是以頁面上的資料列索引為基礎。 例如, 如果您選取第1頁上的第三個專案, 然後移至第2頁, 則會選取該頁面上的第三個專案。

只有 .NET Framework 3.5 SP1 中的動態資料專案一開始才支援保存的選取。 啟用這項功能時, 目前選取的專案會以專案的資料索引鍵為基礎。 這表示如果您在第1頁上選取第三個數據列, 並移至 [第2頁], 第2頁上不會選取任何內容。 當您移回第1頁時, 仍然會選取第三個數據列。 使用*EnablePersistedSelection*屬性, 在所有專案中, *GridView*和*ListView*控制項現在支援保存的選取, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET Chart 控制項

ASP.NET *Chart*控制項會展開 .NET Framework 中的資料視覺效果供應專案。 使用*Chart*控制項, 您可以建立 ASP.NET 網頁, 其具有直覺且引人注目的圖表, 以進行複雜的統計或財務分析。 ASP.NET *Chart*控制項已引進為 .NET Framework 版本 3.5 SP1 版本的附加元件, 而且屬於 .NET Framework 4 版本。

控制項包括下列功能:

- 35 種不同的圖表類型。
- 不限數目的圖表區域、標題、圖例和注釋。
- 適用于所有圖表元素的各種外觀設定。
- 三維支援大部分的圖表類型。
- 可自動納入資料點的智慧型資料標籤。
- 帶狀線、刻度中斷和對數縮放。
- 超過 50 種財務和統計公式可供資料分析與轉換。
- 圖表資料的簡單系結和操作。
- 支援常見的資料格式, 例如日期、時間和貨幣。
- 支援互動式和事件驅動自訂, 包括使用 Ajax 的用戶端 click 事件。
- 狀態管理。
- 二進位資料流。

下圖顯示 ASP.NET Chart 控制項所產生之財務圖表的範例。

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

圖 2：ASP.NET Chart 控制項範例

如需如何使用 ASP.NET Chart 控制項的更多範例, 請在 MSDN 網站上的[Microsoft Chart 控制項的範例環境](https://go.microsoft.com/fwlink/?LinkId=128300)頁面上下載範例程式碼。 您可以在[Chart 控制項論壇](https://go.microsoft.com/fwlink/?LinkId=128713)中找到更多的社區內容範例。

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>將 Chart 控制項加入至 ASP.NET 網頁

下列範例顯示如何使用標記, 將*Chart*控制項加入至 ASP.NET 網頁。 在此範例中, *Chart*控制項會產生靜態資料點的直條圖。

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>使用立體圖表

*Chart*控制項包含*ChartAreas*集合, 其中可包含定義圖表區域特性的*ChartArea*物件。 例如, 若要針對圖表區域使用 3-d, 請使用*顯示 area3dstyle*屬性, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample59.aspx)]

下圖顯示包含四個*條形*圖類型系列的立體圖表。

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

圖 3：立體橫條圖

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>使用刻度中斷和對數刻度

刻度中斷和對數刻度是在圖表中加入複雜的兩種額外方式。 這些功能專屬於圖表區域中的每個軸。 例如, 若要在圖表區域的主要 Y 軸上使用這些功能, 請使用*ChartArea*物件中的*AxisY IsLogarithmic*和*ScaleBreakStyle*屬性。 下列程式碼片段顯示如何在主要 Y 軸上使用刻度分欄。

[!code-aspx[Main](overview/samples/sample60.aspx)]

下圖顯示已啟用尺規分隔的 Y 軸。

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

圖 4：刻度中斷

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>使用 QueryExtender 控制項篩選資料

建立資料導向網頁的開發人員非常常見的工作是篩選資料。 這在傳統上是藉由在資料來源控制項中建立*Where*子句來執行。 這種方法可能很複雜, 而且在某些情況下, *Where*語法並不會讓您利用基礎資料庫的完整功能。

為了讓篩選變得更容易, ASP.NET 4 中已加入新的*QueryExtender*控制項。 這個控制項可以加入至*EntityDataSource*或*LinqDataSource*控制項, 以便篩選這些控制項所傳回的資料。 由於*QueryExtender*控制項會依賴 LINQ, 因此在將資料傳送至頁面之前, 會先在資料庫伺服器上套用篩選, 這樣會產生非常有效率的作業。

*QueryExtender*控制項支援各種不同的篩選選項。 下列各節將說明這些選項, 並提供如何使用它們的範例。

#### <a name="search"></a>搜尋

針對搜尋選項, *QueryExtender*控制項會在指定的欄位中執行搜尋。 在下列範例中, 控制項使用在 TextBoxSearch 控制項中輸入的文字, 並在`ProductName`和`Supplier.CompanyName`資料行中搜尋從*LinqDataSource*控制項傳回的資料中的內容。

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>Range

[範圍] 選項與 [搜尋] 選項相似, 但會指定一對值來定義範圍。 在下列範例中, *QueryExtender*控制項會搜尋*LinqDataSource*控制項`UnitPrice`所傳回之資料中的資料行。 範圍會從頁面上的 TextBoxFrom 和 TextBoxTo 控制項中讀取。

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

[屬性運算式] 選項可讓您定義與屬性值的比較。 如果運算式評估為*true*, 則會傳回正在檢查的資料。 在下列範例中, *QueryExtender*控制項會藉由比較資料`Discontinued`行中的資料與頁面上 CheckBoxDiscontinued 控制項的值, 來篩選資料。

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

最後, 您可以指定要與*QueryExtender*控制項搭配使用的自訂表格達式。 此選項可讓您呼叫頁面中的函式, 該函式會定義自訂篩選邏輯。 下列範例顯示如何在*QueryExtender*控制項中以宣告方式指定自訂表格達式。

[!code-aspx[Main](overview/samples/sample64.aspx)]

下列範例顯示*QueryExtender*控制項所叫用的自訂函式。 在此情況下, 程式碼會使用 LINQ 查詢來篩選資料, 而不是使用包含*Where*子句的資料庫查詢。

[!code-csharp[Main](overview/samples/sample65.cs)]

這些範例一次只會顯示一個在*QueryExtender*控制項中使用的運算式。 不過, 您可以在*QueryExtender*控制項內包含多個運算式。

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Html 編碼的程式碼運算式

某些 ASP.NET 網站 (尤其是 ASP.NET MVC) 高度依賴 using `<%` =  `expression %>`語法 (通常稱為「程式碼區塊」) 來將一些文字寫入回應。 當您使用程式碼運算式時, 很容易忘記對文字進行 HTML 編碼, 如果文字來自使用者輸入, 它可能會讓頁面保持開啟狀態為 XSS (跨網站腳本) 攻擊。

ASP.NET 4 引進了下列適用于程式碼運算式的新語法:

[!code-aspx[Main](overview/samples/sample66.aspx)]

根據預設, 此語法會在寫入回應時使用 HTML 編碼。 這個新運算式會有效地轉譯成下列內容:

[!code-aspx[Main](overview/samples/sample67.aspx)]

例如, &lt;%:Request ["userinput>"]%&gt;針對*Request ["userinput>"]* 的值執行 HTML 編碼。

這項功能的目標是讓您能夠使用新的語法來取代舊語法的所有實例, 如此一來, 您就不會被迫決定要使用的每個步驟。 不過, 在某些情況下, 輸出的文字應該是 HTML 或已經過編碼, 在這種情況下, 這可能會導致雙重編碼。

在這些情況下, ASP.NET 4 引進了一個新介面*IHtmlString*, 以及一個具體的執行*HtmlString*。 這些類型的實例可讓您指出傳回值已經過正確編碼 (或已檢查) 以顯示為 HTML, 因此值不應該再次以 HTML 編碼。 例如, 下列內容不應為 (而不是) HTML 編碼:

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET MVC 2 helper 方法已更新為使用這個新的語法, 因此不會進行雙重編碼, 只有在您執行 ASP.NET 4 時才會這麼做。 當您使用 ASP.NET 3.5 SP1 執行應用程式時, 這個新的語法無法運作。

請記住, 這樣做並不保證受到 XSS 攻擊的保護。 例如, 使用不在引號中的屬性值的 HTML, 可能會包含仍然易受影響的使用者輸入。 請注意, ASP.NET 控制項和 ASP.NET MVC helper 的輸出一律會將屬性值包含在引號中, 這是建議的方法。

同樣地, 此語法不會執行 JavaScript 編碼, 例如當您根據使用者輸入建立 JavaScript 字串時。

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>專案範本變更

在舊版的 ASP.NET 中, 當您使用 Visual Studio 建立新的網站專案或 web 應用程式專案時, 產生的專案只會包含 default.aspx 頁面、預設`Web.config`檔案`App_Data`和資料夾, 如下所示示意圖

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio 也支援空白的網站專案類型, 完全不包含任何檔案, 如下圖所示:

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

結果是, 對於初學者來說, 如何建立生產 Web 應用程式的指引非常少。 因此, ASP.NET 4 引進三個新的範本, 一個用於空白的 Web 應用程式專案, 另一個用於 Web 應用程式和網站專案。

#### <a name="empty-web-application-template"></a>空白 Web 應用程式範本

顧名思義, 空的 Web 應用程式範本是一個減少的 Web 應用程式專案。 您可以從 [Visual Studio 新增專案] 對話方塊中選取此專案範本, 如下圖所示:

[![](overview/_static/image7.png)](overview/_static/image6.png)

([按一下以查看完整大小的影像](overview/_static/image8.png))

當您建立空的 ASP.NET Web 應用程式時, Visual Studio 會建立下列資料夾版面配置:

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

這類似于舊版 ASP.NET 中的空白網站版面配置, 但有一個例外狀況。 在 Visual Studio 2010 中, 空白 web 應用程式和空的網站專案包含下列`Web.config`最小檔案, 其中包含 Visual Studio 用來識別專案目標架構的資訊:

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

若沒有這個*targetFramework*屬性, Visual Studio 預設為以 .NET Framework 2.0 為目標, 以便在開啟繼承應用程式時保留相容性。

#### <a name="web-application-and-web-site-project-templates"></a>Web 應用程式和網站專案範本

隨附于 Visual Studio 2010 的其他兩個新專案範本包含重大變更。 下圖顯示當您建立新的 Web 應用程式專案時, 所建立的專案版面配置。 (網站專案的版面配置幾乎完全相同)。

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

專案包含一些未在舊版中建立的檔案。 此外, 新的 Web 應用程式專案是以基本成員資格功能來設定, 可讓您快速開始保護新應用程式的存取。 由於此包含, 新專案`Web.config`的檔案會包含用來設定成員資格、角色和設定檔的專案。 下列範例會顯示新`Web.config` Web 應用程式專案的檔案。 (在此情況下, *roleManager*會停用)。

[![](overview/_static/image13.png)](overview/_static/image12.png)

([按一下以查看完整大小的影像](overview/_static/image14.png))

專案也包含`Account`目錄中的`Web.config`第二個檔案。 第二個設定檔提供一種方法來保護非登入使用者的 ChangePassword 頁面存取。 下列範例會顯示第二個`Web.config`檔案的內容。

![](overview/_static/image15.png)

新專案範本中預設建立的頁面也包含比舊版更多的內容。 專案包含預設的主版頁面和 CSS 檔案, 預設頁面 (default.aspx) 預設會設定為使用主版頁面。 結果是當您第一次執行 Web 應用程式或網站時, 預設 (首頁) 頁面已經可以正常運作。 事實上, 它類似于您在啟動新的 MVC 應用程式時所看到的預設頁面。

[![](overview/_static/image17.png)](overview/_static/image16.png)

([按一下以查看完整大小的影像](overview/_static/image18.png))

這些專案範本的變更目的是提供如何開始建立新 Web 應用程式的指引。 在語義正確、嚴格的 XHTML 1.0 相容標記和使用 CSS 指定的版面配置中, 範本中的頁面代表建立 ASP.NET 4 Web 應用程式的最佳作法。 預設頁面也有兩個數據行的版面配置, 您可以輕鬆地自訂。

例如, 假設您想要在新的 Web 應用程式中變更一些色彩, 並插入您的公司標誌來取代 [我的 ASP.NET] 應用程式標誌。 若要這麼做, 請在下`Content`建立新的目錄, 以儲存您的標誌影像:

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

若要將影像加入至頁面, 請開啟`Site.Master`檔案, 尋找定義 My ASP.NET 應用程式文字的位置, 並以其*src*屬性設定為新標誌影像的*image*元素取代它, 如下列範例所示:

[![](overview/_static/image21.png)](overview/_static/image20.png)

([按一下以查看完整大小的影像](overview/_static/image22.png))

接著, 您可以移至網站 .css 檔案, 並修改 CSS 類別定義來變更頁面的背景色彩, 以及標頭的色彩。

這些變更的結果是, 您可以輕鬆地顯示自訂的首頁:

[![](overview/_static/image24.png)](overview/_static/image23.png)

([按一下以查看完整大小的影像](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>CSS 改良功能

ASP.NET 4 中的其中一個主要工作領域, 是為了協助呈現符合最新 HTML 標準的 HTML。 這包括 ASP.NET Web 服務器控制項如何使用 CSS 樣式的變更。

#### <a name="compatibility-setting-for-rendering"></a>呈現的相容性設定

根據預設, 當 Web 應用程式或網站的目標為 .NET Framework 4 時, *pages*元素的*controlRenderingCompatibilityVersion*屬性會設定為 "4.0"。 此元素定義于電腦層級`Web.config`檔案中, 而且預設會套用至所有 ASP.NET 4 應用程式:

[!code-xml[Main](overview/samples/sample69.xml)]

*ControlRenderingCompatibility*的值是字串, 它允許未來版本中有可能的新版本定義。 在目前的版本中, 此屬性支援下列值:

- "3.5". 此設定表示舊版的轉譯和標記。 控制項所轉譯的標記是 100% 回溯相容, 而且會接受*xhtmlConformance*屬性的設定。
- "4.0". 如果屬性具有這項設定, ASP.NET Web 服務器控制項就會執行下列動作:
- *XhtmlConformance*屬性一律會被視為「嚴格」。 因此, 控制項會呈現 XHTML 1.0 嚴格標記。
- 停用非輸入控制項不再呈現不正確樣式。
- 隱藏欄位周圍的*div*元素現在已樣式化, 因此不會干擾使用者建立的 CSS 規則。
- Menu 控制項會呈現在語義上正確且符合協助工具方針的標記。
- 驗證控制項不會轉譯內嵌樣式。
- 先前呈現 border = "0" 的控制項 (衍生自 ASP.NET*資料表*控制項的控制項和 ASP.NET*影像*控制項) 不再轉譯此屬性。

#### <a name="disabling-controls"></a>停用控制項

在 ASP.NET 3.5 SP1 和更早版本中, 架構會針對*已啟用*屬性設為*false*的任何控制項, 在 HTML 標籤中呈現*已停用*的屬性。 不過, 根據 HTML 4.01 規格, 只有*輸入*元素應該有這個屬性。

在 ASP.NET 4 中, 您可以將*controlRenderingCompatibilityVersion*屬性設定為 "3.5", 如下列範例所示:

[!code-xml[Main](overview/samples/sample70.xml)]

您可能會建立*標籤*控制項的標記, 如下所示, 這會停用控制項:

[!code-aspx[Main](overview/samples/sample71.aspx)]

*標籤*控制項會轉譯下列 HTML:

[!code-html[Main](overview/samples/sample72.html)]

在 ASP.NET 4 中, 您可以將*controlRenderingCompatibilityVersion*設定為 "4.0"。 在這種情況下, 當控制項的*Enabled*屬性設定為*false*時, 只有轉譯*輸入*專案的控制項會轉譯*已停用*的屬性。 不會轉譯 HTML*輸入*專案的控制項會改為轉譯參考 CSS 類別的*類別*屬性, 您可以用來定義停用的控制面板。 例如, 先前範例中所示的*標籤*控制項會產生下列標記:

[!code-html[Main](overview/samples/sample73.html)]

為此控制項指定之類別的預設值為 "aspNetDisabled"。 不過, 您可以藉由設定*WebControl*類別的靜態*DisabledCssClass*靜態屬性來變更這個預設值。 針對控制項開發人員, 用於特定控制項的行為也可以使用*SupportsDisabledAttribute*屬性來定義。

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>隱藏欄位周圍的 div 元素

ASP.NET 2.0 和更新版本會在*div*元素內轉譯系統特定的隱藏欄位 (例如用來儲存檢視狀態資訊的*hidden*元素), 以符合 XHTML 標準。 不過, 當 CSS 規則影響頁面上的*div*元素時, 這可能會造成問題。 例如, 它可能會導致頁面上出現一條圖元線, 這是隱藏的*div*元素周圍。 在 ASP.NET 4 中, 括住 ASP.NET 所產生之隱藏欄位的*div*元素會新增 CSS 類別參考, 如下列範例所示:

[!code-html[Main](overview/samples/sample74.html)]

接著, 您可以定義僅適用于 ASP.NET 所產生*隱藏*元素的 CSS 類別, 如下列範例所示:

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>呈現樣板化控制項的外部資料表

根據預設, 支援範本的下列 ASP.NET Web 服務器控制項, 會自動包裝在用來套用內嵌樣式的外部資料表中:

- *FormView*
- *登入*
- *PasswordRecovery*
- *ChangePassword*
- *導向*
- *CreateUserWizard*

已將名為*RenderOuterTable*的新屬性新增至這些控制項, 以允許從標記中移除外部資料表。 例如, 請考慮使用*FormView*控制項的下列範例:

[!code-aspx[Main](overview/samples/sample76.aspx)]

此標記會將下列輸出轉譯至頁面, 其中包含 HTML 資料表:

[!code-html[Main](overview/samples/sample77.html)]

若要防止呈現資料表, 您可以設定*FormView*控制項的*RenderOuterTable*屬性, 如下列範例所示:

[!code-aspx[Main](overview/samples/sample78.aspx)]

上一個範例會轉譯下列輸出, 而不含*table*、 *tr*和*td*元素:

> 內容

這項增強功能可讓您更輕鬆地使用 CSS 將控制項的內容樣式, 因為控制項不會轉譯任何未預期的標記。

> [!NOTE]
> 請注意, 這項變更會停用 Visual Studio 2010 設計工具中自動格式化函式的支援, 因為已不再有可以主控自動格式選項所產生之樣式屬性的*table*元素。

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>ListView 控制項增強功能

*ListView*控制項在 ASP.NET 4 中變得更容易使用。 舊版的控制項需要您指定一個版面配置範本, 其中包含具有已知識別碼的伺服器控制項。 下列標記顯示如何在 ASP.NET 3.5 中使用*ListView*控制項的典型範例。

[!code-aspx[Main](overview/samples/sample79.aspx)]

在 ASP.NET 4 中, *ListView*控制項不需要版面配置範本。 先前範例中所顯示的標記可以取代為下列標記:

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList 和 RadioButtonList 控制項的增強功能

在 ASP.NET 3.5 中, 您可以使用下列兩個設定來指定*CheckBoxList*和*RadioButtonList*的版面配置:

- *Flow*。 控制項會呈現*範圍*元素以包含其內容。
- *資料表*。 控制項會呈現包含其內容的*table*元素。

下列範例會顯示每個控制項的標記。

[!code-aspx[Main](overview/samples/sample81.aspx)]

根據預設, 控制項會呈現類似下列的 HTML:

[!code-html[Main](overview/samples/sample82.html)]

因為這些控制項包含專案的清單, 若要轉譯語義正確的 HTML, 則應該使用 HTML 清單 (*li*) 元素來轉譯其內容。 這讓使用輔助技術閱讀網頁的使用者更容易, 並使用 CSS 讓控制項更容易進行樣式。

在 ASP.NET 4 中, *CheckBoxList*和*RadioButtonList*控制項支援*RepeatLayout*屬性的下列新值:

- *OrderedList* –內容會轉譯為*ol*元素內的*li*元素。
- *UnorderedList* –內容會轉譯為*ul*元素內的*li*元素。

下列範例顯示如何使用這些新的值。

[!code-aspx[Main](overview/samples/sample83.aspx)]

上述標記會產生下列 HTML:

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> 注意: 如果您將*RepeatLayout*設定為*OrderedList*或*UnorderedList*, 就無法再使用*RepeatDirection*屬性, 而且如果已在您的標記或程式碼中設定屬性, 就會在執行時間擲回例外狀況。 屬性不會有任何值, 因為這些控制項的視覺化版面配置是使用 CSS 來定義的。

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>Menu 控制項改良功能

在 ASP.NET 4 之前, *Menu*控制項會呈現一系列的 HTML 資料表。 這使得在設定內嵌屬性以外套用 CSS 樣式, 也不符合協助工具標準。

在 ASP.NET 4 中, 控制項現在會使用包含未排序清單和清單元素的語義標記來呈現 HTML。 下列範例會在*Menu*控制項的 ASP.NET 網頁中顯示標記。

[!code-aspx[Main](overview/samples/sample85.aspx)]

當頁面呈現時, 控制項會產生下列 HTML (為了清楚起見, 已省略*onclick*程式碼):

[!code-html[Main](overview/samples/sample86.html)]

除了轉譯改善之外, 也使用焦點管理來改善功能表的鍵盤導覽。 當*功能表*控制項取得焦點時, 您可以使用方向鍵來流覽元素。 *Menu*控制項現在也會附加可存取的豐富網際網路應用程式 (ARIA) 角色和屬性下列次數 w[翼的](http://www.w3.org/TR/wai-aria-practices/#menu "功能表 ARIA 方針"), 以改善協助工具。

Menu 控制項的樣式是在頁面頂端的樣式區塊中轉譯, 而不是以轉譯的 HTML 專案作為程式列來呈現。 如果您想要完全掌控控制項的樣式, 您可以將新的*IncludeStyleBlock*屬性設定為*false*, 在此情況下不會發出樣式區塊。 使用此屬性的其中一種方式是使用 Visual Studio 設計工具中的自動格式化功能來設定功能表的外觀。 接著, 您可以執行頁面, 開啟頁面來源, 然後將轉譯的樣式區塊複製到外部 CSS 檔案。 在 Visual Studio 中, 復原樣式, 並將*IncludeStyleBlock*設定為*false*。 結果是會使用外部樣式表單中的樣式來定義功能表外觀。

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>Wizard 和 CreateUserWizard 控制項

ASP.NET *Wizard*和*CreateUserWizard*控制項支援範本, 可讓您定義所呈現的 HTML。 (*CreateUserWizard*衍生自*Wizard*)。下列範例顯示完整樣板化*CreateUserWizard*控制項的標記:

[!code-aspx[Main](overview/samples/sample87.aspx)]

控制項會呈現如下的 HTML:

[!code-html[Main](overview/samples/sample88.html)]

在 ASP.NET 3.5 SP1 中, 雖然您可以變更範本內容, 但您仍然無法控制*Wizard*控制項的輸出。 在 ASP.NET 4 中, 您可以建立*LayoutTemplate*範本並插入*預留位置*控制項 (使用保留名稱), 以指定您希望*Wizard 控制項*呈現的方式。 下列範例顯示這種情況:

[!code-aspx[Main](overview/samples/sample89.aspx)]

此範例會在*LayoutTemplate*元素中包含下列已命名的預留位置:

- *headerPlaceholder* –在執行時間, 這會由*system.windows.controls.headereditemscontrol.headertemplate*元素的內容所取代。
- *sideBarPlaceholder* –在執行時間, 這會由*SideBarTemplate*元素的內容所取代。
- *wizardStepPlaceHolder* –在執行時間, 這會由*WizardStepTemplate*元素的內容所取代。
- *navigationPlaceholder* –在執行時間, 這會由您已定義的任何導覽範本取代。

範例中使用預留位置的標記會轉譯下列 HTML (不含實際定義于範本中的內容):

[!code-html[Main](overview/samples/sample90.html)]

現在唯一不是使用者定義的 HTML 是*span*元素。 (我們預計在未來的版本中, 即使不會轉譯*span*元素)。這現在可讓您完全掌控*Wizard*控制項所產生的所有內容。

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC 在3月2009推出為 ASP.NET 3.5 SP1 的附加元件架構。 Visual Studio 2010 包含 ASP.NET MVC 2, 其中包含新的特性和功能。

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>區域支援

區域可讓您將控制器和 views 群組成與其他區段相對隔離的大型應用程式區段。 每個區域都可以實作為個別的 ASP.NET MVC 專案, 然後由主應用程式參考。 這可協助您在建立大型應用程式時管理複雜度, 並讓多個小組更輕鬆地在單一應用程式上共同作業。

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>資料-批註屬性驗證支援

*DataAnnotations*屬性可讓您使用中繼資料屬性, 將驗證邏輯附加至模型。 *DataAnnotations*屬性是在 ASP.NET 3.5 SP1 的 ASP.NET 動態資料中引進。 這些屬性已整合到預設的模型系結器中, 並提供中繼資料驅動的方法來驗證使用者輸入。

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>樣板化協助程式

樣板化協助程式可讓您自動將編輯和顯示範本與資料類型產生關聯。 例如, 您可以使用範本協助程式, 指定自動呈現 system.string 值的日期選擇器 UI 元素。 這類似于 ASP.NET 動態資料中的欄位範本。

*EditorFor*和*html. DisplayFor* helper 方法具有內建的支援, 可呈現標準資料類型, 以及具有多個屬性的複雜物件。 它們也會藉由讓您將資料批註屬性 (例如*DisplayName*和*ScaffoldColumn* ) 套用至*ViewModel*物件, 以自訂轉譯。

您通常會想要進一步自訂 UI 協助程式的輸出, 並對產生的內容有完整的控制權。 *EditorFor*和*html. DisplayFor* helper 方法會使用範本化機制來支援此功能, 讓您定義可覆寫並控制所轉譯輸出的外部樣板。 範本可以針對類別個別呈現。

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dynamic Data

動態資料是在2008年 .NET Framework 3.5 SP1 版本中引進。 這項功能提供了許多用於建立資料驅動應用程式的增強功能, 包括下列:

- 用來快速建立資料驅動網站的 RAD 體驗。
- 自動驗證是以資料模型中定義的條件約束為基礎。
- 使用屬於動態資料專案之一部分的欄位範本, 輕鬆變更*GridView*和*DetailsView*控制項中的欄位所產生之標記的能力。

> [!NOTE]
> 注意如需詳細資訊, 請參閱 MSDN Library 中的[動態資料檔](https://msdn.microsoft.com/library/cc488545.aspx)。

對於 ASP.NET 4, 動態資料已經過增強, 可讓開發人員快速建立資料驅動網站的能力。

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>啟用現有專案的動態資料

.NET Framework 3.5 SP1 隨附的動態資料功能引進了下列新功能:

- 欄位範本: 這些會為資料繫結控制項提供以資料類型為基礎的範本。 欄位範本提供更簡單的方式來自訂資料控制項的外觀, 而不是使用每個欄位的範本欄位。
- 驗證–動態資料可讓您在資料類別上使用屬性來指定一般案例的驗證, 例如必要欄位、範圍檢查、類型檢查、使用正則運算式的模式比對, 以及自訂驗證。 驗證是由資料控制項強制執行。

不過, 這些功能具有下列需求:

- 資料存取層必須以 Entity Framework 或 LINQ to SQL 為基礎。
- 這些功能唯一支援的資料來源控制項為*EntityDataSource*或*LinqDataSource*控制項。
- 這些功能需要使用動態資料或動態資料實體範本建立的 Web 專案, 才能擁有支援此功能所需的所有檔案。

在 ASP.NET 4 中動態資料支援的主要目標, 是要為任何 ASP.NET 應用程式啟用動態資料的新功能。 下列範例會顯示可利用現有頁面中動態資料功能之控制項的標記。

[!code-aspx[Main](overview/samples/sample91.aspx)]

在頁面的程式碼中, 必須新增下列程式碼, 才能啟用這些控制項的動態資料支援:

[!code-csharp[Main](overview/samples/sample92.cs)]

當*GridView*控制項處於編輯模式時, 動態資料會自動驗證輸入的資料格式是否正確。 如果不是, 則會顯示錯誤訊息。

這種功能也提供其他優點, 例如能夠指定插入模式的預設值。 如果沒有動態資料, 若要為欄位執行預設值, 您必須附加至事件、尋找控制項 (使用*FindControl*), 並設定其值。 在 ASP.NET 4 中, *EnableDynamicData*呼叫支援第二個參數, 可讓您傳遞物件上任何欄位的預設值, 如下列範例所示:

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>宣告式 DynamicDataManager 控制語法

*DynamicDataManager*控制項已增強, 可讓您以宣告方式設定它, 如同 ASP.NET 中的大部分控制項, 而不只是在程式碼中。 *DynamicDataManager*控制項的標記看起來如下列範例所示:

[!code-aspx[Main](overview/samples/sample94.aspx)]

此標記會針對*DynamicDataManager*控制項的*工具列*區段中所參考的 GridView1 控制項, 啟用動態資料行為。

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>實體範本

實體範本提供新的方式來自訂資料的配置, 而不需要您建立自訂頁面。 頁面範本會使用*FormView*控制項 (而不是在舊版動態資料的頁面範本中使用的*DetailsView*控制項) 和*DynamicEntity*控制項來呈現實體範本。 這可讓您更充分掌控動態資料所呈現的標記。

下列清單顯示包含實體範本的新專案目錄版面配置:

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate`目錄包含如何顯示資料模型物件的範本。 根據預設, 會使用`Default.ascx`範本來呈現物件, 其提供的標記就像是 ASP.NET 3.5 SP1 中動態資料所使用的*DetailsView*控制項所建立的標記。 下列範例會顯示`Default.ascx`控制項的標記:

[!code-aspx[Main](overview/samples/sample96.aspx)]

您可以編輯預設範本, 以變更整個網站的外觀與風格。 有一些範本可用於顯示、編輯和插入作業。 新範本可以根據資料物件的名稱來新增, 以便只變更一種物件類型的外觀和操作。 例如, 您可以新增下列範本:

[!code-console[Main](overview/samples/sample97.cmd)]

此範本可能包含下列標記:

[!code-aspx[Main](overview/samples/sample98.aspx)]

新的實體範本會使用新的*DynamicEntity*控制項顯示在頁面上。 在執行時間, 會將此控制項取代為實體範本的內容。 下列標記會顯示`Detail.aspx`頁面範本中使用實體範本的*FormView*控制項。 請注意標記中的*DynamicEntity*元素。

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>Url 和電子郵件地址的新欄位範本

ASP.NET 4 引進了兩個新的內建欄位`EmailAddress.ascx`範本`Url.ascx`: 和。 這些範本會用於標示為*EmailAddress*的欄位, 或具有*DataType*屬性的*Url* 。 針對*EmailAddress*物件, 此欄位會顯示為使用*mailto:* 通訊協定所建立的超連結。 當使用者按一下連結時, 它會開啟使用者的電子郵件客戶程式, 並建立基本架構訊息。 輸入為*Url*的物件會顯示為一般超連結。

下列範例顯示如何標記欄位。

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>使用 DynamicHyperLink 控制項建立連結

動態資料使用 .NET Framework 3.5 SP1 中新增的路由功能來控制使用者存取網站時所看到的 Url。 新的*DynamicHyperLink*控制項可讓您輕鬆地在動態資料網站中建立頁面的連結。 下列範例顯示如何使用*DynamicHyperLink*控制項:

[!code-aspx[Main](overview/samples/sample101.aspx)]

此標記會根據檔案`Products` `Global.asax`中定義的路由, 建立指向資料表清單頁面的連結。 控制項會自動使用動態資料頁面所依據的預設資料表名稱。

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>資料模型中的繼承支援

Entity Framework 和 LINQ to SQL 都支援其資料模型中的繼承。 其中一個範例可能是具有`InsurancePolicy`資料表的資料庫。 它也可能包含`CarPolicy`與`HousePolicy` `InsurancePolicy`具有相同欄位的和資料表, 然後再新增更多欄位。 動態資料已修改為了解資料模型中的繼承物件, 以及支援繼承資料表的樣板。

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>支援多對多關聯性 (僅限 Entity Framework)

Entity Framework 對資料表之間的多對多關聯性有豐富的支援, 這是藉由將關聯性公開為*實體*物件上的集合來實現。 新增`ManyToMany.ascx`新`ManyToMany_Edit.ascx`的和欄位範本, 以支援顯示和編輯與多對多關聯性相關的資料。

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>控制顯示和支援列舉的新屬性

已新增*DisplayAttribute* , 可讓您進一步控制欄位的顯示方式。 舊版動態資料中的*DisplayName*屬性可讓您變更用來當做欄位標題的名稱。 新的*DisplayAttribute*類別可讓您指定更多選項來顯示欄位, 例如欄位的顯示順序, 以及是否將欄位當做篩選準則使用。 屬性也會針對*GridView*控制項中的標籤提供獨立的控制項、 *DetailsView*控制項中使用的名稱、欄位的解說文字, 以及用於欄位的浮水印 (如果欄位接受文字輸入)。

已加入*EnumDataTypeAttribute*類別, 可讓您將欄位對應至列舉。 當您將此屬性套用至欄位時, 您可以指定列舉類型。 動態資料使用新`Enumeration.ascx`的欄位範本來建立 UI, 以顯示和編輯列舉值。 此範本會將資料庫中的值對應至列舉中的名稱。

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>增強的篩選支援

動態資料1.0 隨附于布林資料行和外鍵資料行的內建篩選。 篩選器不允許您指定是否要顯示它們, 或是以顯示的順序排列。 新的*DisplayAttribute*屬性可解決這兩個問題, 方法是讓您控制是否要將資料行顯示為篩選準則, 以及顯示的順序。

另一個增強功能是已重新撰寫篩選支援,[以使用 Web form 的新](#0.2__QueryExtender "_QueryExtender")功能。 這可讓您建立篩選器, 而不需要知道篩選將會搭配使用的資料來源控制項。 除了這些擴充功能之外, 篩選也已轉換成範本控制項, 讓您可以加入新的控制項。 最後, 先前所述的*DisplayAttribute*類別可讓您覆寫預設篩選, 其方式與*UIHint*允許覆寫資料行的預設欄位範本相同。

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 Web 開發改良功能

Visual Studio 2010 中的 Web 程式開發已經過增強, 可透過 HTML 和 ASP.NET 標記程式碼片段和新的動態 IntelliSense JavaScript, 加強 CSS 相容性、提高生產力。

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>改良的 CSS 相容性

Visual Studio 2010 中的 Visual Web Developer 設計工具已更新, 以改善 CSS 2.1 標準合規性。 設計工具更能保留 HTML 來源的完整性, 而且比舊版的 Visual Studio 更健全。 實際上, 我們也改進了架構, 讓未來的轉譯、版面配置和維護性增強功能更加完備。

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML 和 JavaScript 程式碼片段

在 HTML 編輯器中, IntelliSense 會自動完成標記名稱。 IntelliSense 程式碼片段功能會自動完成整個標記等等。 在 Visual Studio 2010 中, C#與舊版 Visual Studio 支援的 JavaScript 和 Visual Basic 支援 IntelliSense 程式碼片段。

Visual Studio 2010 包含超過200的程式碼片段, 可協助您自動完成常見的 ASP.NET 和 HTML 標籤, 包括必要的屬性 (例如 runat = "server"), 以及標記特有的一般屬性 (例如*ID*、 *DataSourceID*、 *ControlToValidate*和*Text*)。

您可以下載其他程式碼片段, 也可以撰寫自己的程式碼片段, 以封裝您或您的小組用於一般工作的標記區塊。

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense 增強功能

在 Visual 2010 中, JavaScript IntelliSense 已經過重新設計, 可提供更豐富的編輯體驗。 IntelliSense 現在會辨識由方法 (例如*registerNamespace* ) 動態產生的物件, 以及其他 JavaScript 架構所使用的類似技術。 效能已經過改良, 可分析大型的腳本程式庫, 並在幾乎不需要處理延遲的情況之下顯示 IntelliSense。 相容性已大幅增加, 可支援幾乎所有協力廠商程式庫, 並支援各種編碼樣式。 檔批註現在會在您輸入時進行剖析, 而且 IntelliSense 會立即運用。

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>使用 Visual Studio 2010 的 Web 應用程式部署

當 ASP.NET 開發人員部署 Web 應用程式時, 通常會發現它們遇到下列問題:

- 部署至共用的主控網站需要諸如 FTP 等技術, 這可能會很慢。 此外, 您還必須手動執行工作, 例如執行 SQL 腳本來設定資料庫, 而且您必須變更 IIS 設定, 例如將虛擬目錄資料夾設為應用程式。
- 在企業環境中, 除了部署 Web 應用程式檔以外, 系統管理員經常必須修改 ASP.NET 設定檔和 IIS 設定。 資料庫管理員必須執行一系列的 SQL 腳本, 才能讓應用程式資料庫運作。 這類安裝非常耗費人力, 通常需要數小時才能完成, 而且必須仔細記載。

Visual Studio 2010 包含解決這些問題的技術, 並可讓您順暢地部署 Web 應用程式。 其中一項技術是 IIS Web Deployment Tool (Msdeploy.exe)。

Visual Studio 2010 中的 Web 部署功能包含下列主要區域:

- 網頁封裝
- Web.config 轉換
- 資料庫部署
- 針對 Web 應用程式按一下 [發佈]

下列各節提供有關這些功能的詳細資料。

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>網頁封裝

Visual Studio 2010 使用 Msdeploy.exe 工具來為您的應用程式建立壓縮 (.zip) 檔案, 這稱為「 *Web 封裝*」。 封裝檔案包含您應用程式的相關中繼資料, 以及下列內容:

- IIS 設定, 其中包括應用程式集區設定、錯誤頁面設定等等。
- 實際的 Web 內容, 包括網頁、使用者控制項、靜態內容 (影像和 HTML 檔案) 等等。
- SQL Server 資料庫架構和資料。
- 安全性憑證、要安裝在 GAC 中的元件、登錄設定等。

Web 封裝可以複製到任何伺服器, 然後使用 IIS 管理員以手動方式安裝。 或者, 若要進行自動化部署, 可以使用命令列命令或使用部署 Api 來安裝封裝。

Visual Studio 2010 提供內建的 MSBuild 工作和目標, 以建立 Web 封裝。 如需詳細資訊, 請參閱 MSDN 網站上的[ASP.NET Web 應用程式專案部署總覽](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx), 以及[10 + 20 為什麼您應該](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)在 Vishal Joshi 的 Blog 上建立 web 套件的原因。

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web.config 轉換

針對 Web 應用程式部署, Visual Studio 2010 引進了[XML 檔轉換 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), 這是一項功能, 可`Web.config`讓您將檔案從開發設定轉換成生產環境設定。 轉換設定是在名為`web.debug.config`、 `web.release.config`等的轉換檔案中指定。 (這些檔案的名稱符合 MSBuild 設定)。轉換檔案只包含您需要對已部署`Web.config`的檔案進行的變更。 您可以使用簡單的語法來指定變更。

下列範例顯示可能針對部署發行設定`web.release.config`而產生的部分檔案。 範例中的 Replace 關鍵字會指定在部署期間,會將檔案中`Web.config`的 connectionString 節點取代為範例中所列的值。

[!code-xml[Main](overview/samples/sample102.xml)]

如需詳細資訊, 請參閱 MSDN <a id="0.2_a"></a>網站上的 web[應用程式專案部署的 web.config 轉換語法](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)和[web 部署:Vishal Joshi 的 blog](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)上的 web.config 轉換。

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>資料庫部署

Visual Studio 2010 部署套件可以包含 SQL Server 資料庫的相依性。 在封裝定義中, 您會提供源資料庫的連接字串。 當您建立 Web 封裝時, Visual Studio 2010 會為資料庫架構建立 SQL 腳本, 並選擇性地為該資料建立, 然後將它們加入至封裝。 您也可以提供自訂的 SQL 腳本, 並指定它們應該在伺服器上執行的順序。 在部署階段, 您會提供適用于目標伺服器的連接字串。接著, 部署程式會使用此連接字串來執行腳本, 以建立資料庫架構並加入資料。

此外, 只要使用單鍵發行, 您就可以設定部署, 在應用程式發行至遠端共用主控網站時直接發佈資料庫。 如需詳細資訊，請參閱[如何：在 MSDN 網站上使用 Web 應用程式](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)專案部署資料庫, 並在 Vishal Joshi 的 blog 上[使用 VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)來部署資料庫。

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>針對 Web 應用程式按一下 [發佈]

Visual Studio 2010 也可讓您使用 IIS 遠端系統管理服務, 將 Web 應用程式發行至遠端伺服器。 您可以為您的主控帳戶或測試伺服器或預備伺服器建立發行設定檔。 每個設定檔都可以安全地儲存適當的認證。 您接著可以使用 Web 單鍵 [發行] 工具列, 只要按一下就能部署到任何目標伺服器。 使用 Visual Studio 2010, 您也可以使用 MSBuild 命令列來發行。 這可讓您將 team build 環境設定為包含連續整合模型中的發行。

如需詳細資訊，請參閱[如何：在 MSDN 網站上使用單鍵發佈和 Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)部署 web 應用程式專案, 並在 Vishal Joshi 的 blog 上, 按一下 [[使用 VS 2010 發佈](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)]。 若要在 Visual Studio 2010 中觀看有關 Web 應用程式部署的影片簡報, 請參閱 VS 2010, 以取得 Vishal Joshi 的網路上[的 Web 開發人員預覽版](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html)。

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>資源

下列網站提供 ASP.NET 4 和 Visual Studio 2010 的其他相關資訊。

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — MSDN 網站上的 ASP.NET 4 官方檔。
- [https://www.asp.net/](https://www.asp.net/)— ASP.NET 小組自己的網站。
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx)和[ASP.NET 動態資料內容地圖](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)-ASP.NET 小組網站上的線上資源, 以及 ASP.NET 動態資料的官方檔。
- [https://www.asp.net/ajax/](../../ajax/index.md)-用來 ASP.NET Ajax 開發的主要 Web 資源。
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/): Visual Web Developer 小組的 blog, 其中包含 Visual Studio 2010 中功能的相關資訊。
- [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — ASP.NET 的預覽版本主要 Web 資源。

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>免責聲明

這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。

本文件中的資訊表示直到文件發行日前 Microsoft Corporation 針對問題的看法。 Microsoft 必須因應不斷變化的市場狀況，因此本文件不代表 Microsoft 的保證，且 Microsoft 不保證這些資訊在文件發行後的正確性。

本技術白皮書僅供參考。 MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。

承諾遵守所有適用的著作權法是使用者的責任。 著作權法沒有針對某種權利加以限制，但在未獲得 Microsoft Corporation 書面同意的情況下，本文件的任何部分不得複製、以檢索系統存放或擷取、以任何形式或方法傳送 (電子、機械、影像複製、錄音或其他任何方法)、或基於任何其他不良意圖。

本文件所提及的主要事務，Microsoft 得擁有專利、專利應用程式、商標、著作權或其他智慧財產權。 除了 Microsoft 於授權合約書中書面提供的之外，本文件所述內容並未賦予您這些專利、商標、著作權、或其他智慧財產的任何授權或使用權利。

除非另有說明, 否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、商標、人員、地點及事件均屬虛構, 而且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件相關。位址、標誌、人員、地點或事件的預定或應加以推斷。

© 2009 Microsoft Corporation. 著作權所有，並保留一切權利。

Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。

本文件中所提實際公司和產品，可能為各所有人所有之商標。
