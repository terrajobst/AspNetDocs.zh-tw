---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: 不要在 ASP.NET 中做什麼，以及該怎麼做？Microsoft Docs
author: Rick-Anderson
description: 本主題說明在 ASP.NET Web 專案中的幾個常見錯誤。 它會提供您應採取哪些措施來避免這些通用的建議 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616988"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a>在 ASP.NET 中不該做什麼以及該做什麼

> 本主題說明在 ASP.NET Web 專案中的幾個常見錯誤。 它會提供您應採取哪些動作來避免這些常見錯誤的建議。 其以[簡報](http://vimeo.com/68390507)為基礎， **Damian Edwards**在挪威開發人員會議。

## <a name="disclaimer"></a>免責聲明

本主題不是為了確保您的應用程式安全且有效率的完整指南。 您仍然需要遵循本主題未概述之安全性和效能的最佳作法。 它只會建議如何避免與 .NET 類別和進程相關的常見錯誤。

## <a name="overview"></a>概觀

本主題包含下列各節：

- [標準合規性](#standards)

    - [控制介面卡](#adapters)
    - [控制項的樣式屬性](#styleprop)
    - [頁面和控制項回呼](#callback)
    - [瀏覽器功能偵測](#browsercap)
- [Security](#security)

    - [要求驗證](#validation)
    - [無 cookie 的表單驗證和會話](#cookieless)
    - [EnableViewStateMac](#viewstatemac)
    - [中度信任](#medium)
    - [&lt;appSettings&gt;](#appsettings)
    - [UrlPathEncode](#urlpathencode)
- [可靠性和效能](#performance)

    - [PreSendRequestHeaders 和 PreSendRequestContent](#presend)
    - [使用 Web Forms 的非同步頁面事件](#asyncevents)
    - [火災和忘記的工作](#fire)
    - [要求實體主體](#requestentity)
    - [回應。重新導向和回應。結束](#redirect)
    - [EnableViewState 和 ViewStateMode](#viewstatemode)
    - [SqlMembershipProvider](#sqlprovider)
    - [長時間執行的要求（> 110 秒）](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a>標準合規性

<a id="adapters"></a>

### <a name="control-adapters"></a>控制介面卡

建議：停止使用控制項介面卡進行調適型轉譯，而改用 CSS 媒體查詢和符合標準的 HTML。

控制項介面卡是在 .NET 2.0 中引進，以轉譯針對不同裝置和環境自訂的呈現程式碼。 現在，您可以使用 CSS 和 HTML 來完成此彈性轉譯。 您應該停止使用控制項介面卡，並將任何現有的介面卡轉換成 CSS 和 HTML。

如需詳細資訊，請參閱[媒體查詢](http://www.w3.org/TR/css3-mediaqueries/)和[如何：將行動頁面加入至您的 ASP.NET WEB Forms/MVC 應用程式](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)。

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a>控制項的樣式屬性

建議：停止在控制項標記中設定樣式值，並改為在 CSS 樣式表單中設定格式化值。

Web 服務器控制項包含數十個屬性，可用於設定內嵌樣式屬性。 例如，前景屬性會設定控制項的文字色彩。 您可以透過 CSS 樣式表單，更有效率地達成相同的效果。 樣式表單可讓您集中樣式值，並避免在整個應用程式中設定這些值。

下列範例顯示將文字設為紅色的 CSS 類別。

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

下一個範例顯示如何動態套用 CSS 類別。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a>頁面和控制項回呼

建議：停止使用頁面和控制項回呼，並改為使用下列任何一項： AJAX、UpdatePanel、MVC 動作方法、Web API 或 SignalR。

在舊版的 ASP.NET 中，頁面和控制項回呼方法可讓您更新部分網頁，而不需要重新整理整個頁面。 您現在可以透過[AJAX](../../../ajax/index.md)、 [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)、 [MVC](../../../mvc/index.md)、 [Web API](../../../web-api/index.md)或[SignalR](../../../signalr/index.md)完成部分頁面更新。 您應該停止使用回呼方法，因為它們可能會造成易記 Url 和路由的問題。 根據預設，控制項不會啟用回呼方法，但如果您已在控制項中啟用這項功能，您應該將它停用。

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a>瀏覽器功能偵測

建議：停止使用靜態瀏覽器功能偵測，並改為使用動態功能偵測。

在舊版的 ASP.NET 中，每個瀏覽器所支援的功能都是儲存在 XML 檔案中。 透過靜態查閱偵測功能支援並不是最佳的方法。 現在，您可以使用功能偵測架構（例如[Modernizr](http://modernizr.com/)），動態偵測瀏覽器支援的功能。 功能偵測藉由嘗試使用方法或屬性，然後檢查瀏覽器是否產生想要的結果，來判斷支援。 根據預設，Modernizr 會包含在 Web 應用程式範本中。

<a id="security"></a>

## <a name="security"></a>安全性

<a id="validation"></a>

### <a name="request-validation"></a>要求驗證

建議：驗證使用者輸入，並將使用者的輸出編碼。

要求驗證是 ASP.NET 的一項功能，它會檢查每個要求，並在發現認知的威脅時停止要求。 請勿依賴要求驗證來保護您的應用程式，以防止跨網站腳本攻擊。 相反地，請驗證使用者的所有輸入，並將輸出編碼。 在某些有限的情況下，您可以使用正則運算式來驗證輸入，但在較複雜的情況下，您應該使用 .NET 類別來驗證使用者輸入，以判斷值是否符合允許的值。

下列範例示範如何在 Uri 類別中使用靜態方法，以判斷使用者所提供的 Uri 是否有效。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

不過，若要充分驗證 Uri，您也應該檢查以確定它指定 `http` 或 `https`。 下列範例會使用實例方法來確認 Uri 是否有效。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

將使用者輸入轉譯為 HTML 或在 SQL 查詢中包含使用者輸入之前，請將值編碼，以確保不會包含惡意程式碼。

您可以使用 &lt;%：%&gt; 語法，以 HTML 編碼標記中的值，如下所示。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

或者，在 Razor 語法中，您可以使用 @ 進行 HTML 編碼，如下所示。

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

下一個範例顯示如何在程式碼後置中以 HTML 編碼值。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

若要安全地編碼 SQL 命令的值，請使用命令參數，例如[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)。 <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a>無 cookie 的表單驗證和會話

建議：需要 cookie。

在查詢字串中傳遞驗證資訊並不安全。 因此，當您的應用程式包含驗證時，需要 cookie。 如果您的 cookie 會儲存敏感資訊，請考慮為 cookie 要求 SSL。

下列範例顯示如何在 web.config 檔案中指定表單驗證需要透過 SSL 傳輸的 cookie。

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a>EnableViewStateMac

建議：永不設定為 false。

根據預設，EnableViewStateMac 會設定為 true。 即使您的應用程式未使用 view 狀態，也不會將 EnableViewStateMac 設定為 false。 將此值設定為 false 會讓您的應用程式容易遭受跨網站腳本處理。

從 ASP.NET 4.5.2 開始，執行時間會強制執行**EnableViewStateMac = true**。 即使您將它設定為 false，執行時間也會忽略此值，並繼續將值設定為 true。 如需詳細資訊，請參閱[ASP.NET 4.5.2 And EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)。

下列範例顯示如何將 EnableViewStateMac 設定為 true。 您不需要實際將此值設定為 true，因為它預設為 true。 不過，如果您已在應用程式的任何頁面上將它設為 false，則必須立即更正此值。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a>中度信任

建議：不要依賴中等信任（或任何其他信任層級）做為安全性界限。

部分信任不會適當地保護您的應用程式，因此不應使用。 相反地，請使用完全信任，並隔離不同應用程式集區中不受信任的應用程式。 此外，請在唯一的身分識別下執行每個應用程式集區。 如需詳細資訊，請參閱[ASP.NET 部分信任不保證應用程式隔離](https://support.microsoft.com/kb/2698981)。

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a>&lt;appSettings&gt;

建議：請勿停用 &lt;appSettings&gt; 元素中的安全性設定。

AppSettings 元素包含許多安全性更新所需的值。 您不應該變更或停用這些值。 如果您在部署更新時必須停用這些值，請在完成部署之後立即重新啟用。

如需詳細資訊，請參閱[ASP.NET AppSettings 元素](https://msdn.microsoft.com/library/hh975440.aspx)。

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a>UrlPathEncode

建議：請改用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 。

UrlPathEncode 方法已新增至 .NET Framework，以解決非常特定的瀏覽器相容性問題。 它不會對 URL 進行適當的編碼，而且不會保護您的應用程式不會受到跨網站腳本的攻擊。 您不應該在應用程式中使用它。 請改用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)。

下列範例示範如何傳遞編碼的 URL 做為超連結控制項的查詢字串參數。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a>可靠性和效能

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a>PreSendRequestHeaders 和 PreSendRequestContent

建議：請勿將這些事件與受控模組搭配使用。 請改為撰寫原生 IIS 模組來執行必要的工作。 請參閱[建立原生程式碼 HTTP 模組](https://msdn.microsoft.com/library/ms693629.aspx)。

您可以使用[PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx)和[PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx)事件搭配原生 IIS 模組。
> [!WARNING]
> 請不要搭配執行 `IHttpModule`的受控模組使用 `PreSendRequestHeaders` 和 `PreSendRequestContent`。 設定這些屬性可能會造成非同步要求的問題。 應用程式要求路由（ARR）和 websocket 的組合，可能會導致 w3wp.exe 損毀的存取違規例外狀況。 例如，iiscore！Iiscore 中的 W3_CONTEXT_BASE：： GetIsLastNotification + 68 造成存取違規例外狀況（0xC0000005）。

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a>使用 web forms 的非同步頁面事件

建議：在 Web form 中，避免針對頁面生命週期事件撰寫非同步 void 方法，而改為使用[RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx)來執行非同步程式碼。

當您以**async**和**void**標記頁面事件時，您無法判斷非同步程式碼何時完成。 相反地，請使用 RegisterAsyncTask 來執行非同步程式碼，讓您能夠追蹤其完成的方式。

下列範例顯示包含非同步程式碼的按鈕點擊處理常式。 這個範例包括以非同步方式讀取字串值，這僅提供做為非同步工作的簡化範例，而不是建議的作法。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

如果您使用非同步工作，請在 Web.config 檔案中將 Http 執行時間目標架構設定為4.5 （或更新版本）。 將 [目標 framework] 設定為4.5 會開啟 .NET 4.5 中新增的同步處理內容。 預設會在 Visual Studio 的新專案中設定這個值，但如果您使用現有的專案，則不會設定這個值。

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a>火災和忘記的工作

建議：在 ASP.NET 內處理要求時，請避免啟動不正常的工作（例如呼叫 ThreadPool. QueueUserWorkItem 方法，或建立重複呼叫委派的計時器）。

如果您的應用程式有在 ASP.NET 內執行的火災和忘工作，您的應用程式可能會無法同步。應用程式域可以在任何時間終結，這表示您進行中的程式可能不再符合應用程式的目前狀態。

您應該將這種類型的工作移到 ASP.NET 之外。 您可以在 Azure 中使用 Web 作業、Windows 服務或背景工作角色來執行進行中的工作，並從另一個進程執行該程式碼。

如果您必須在 ASP.NET 中執行此工作，您可以新增名為[WebBackgrounder](http://www.nuget.org/packages/webbackgrounder)的 Nuget 套件來執行程式碼。

<a id="requestentity"></a>

### <a name="request-entity-body"></a>要求實體主體

建議：請避免在處理常式的 execute 事件之前，InputStream 讀取要求. Form 或 Request。

您最早應從 Request 讀取。表單或要求。 InputStream 是在處理常式的 execute 事件期間。 在 MVC 中，控制器是處理常式，而執行事件是在動作方法執行時。 在 Web form 中，頁面是處理常式，而執行事件是在 Page. Init 事件引發時。 如果您讀取的要求實體內容早于執行事件，您會干擾要求的處理。

如果您需要在執行事件之前讀取要求實體主體，請使用[GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx)或[request. GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)。 當您使用 GetBufferlessInputStream 時，您會從要求取得未經處理的資料流程，並假設您負責處理整個要求。 在呼叫 GetBufferlessInputStream 之後，要求. Form 和 Request. InputStream 無法使用，因為 ASP.NET 並未填入這些要求。 當您使用 GetBufferedInputStream 時，您會從要求取得資料流程的複本。 InputStream 仍可在要求中使用，因為 ASP.NET 會填入另一個複本。

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a>回應。重新導向和回應。結束

建議：請留意執行緒在呼叫回應後的處理方式差異[。重新導向（字串）](https://msdn.microsoft.com/library/t9dwyts4.aspx)。

[Response （String）](https://msdn.microsoft.com/library/t9dwyts4.aspx)方法會呼叫 Response. End 方法。 在同步處理過程中，呼叫要求。重新導向會導致目前的執行緒立即中止。 不過，在非同步程式中，呼叫回應。重新導向並不會中止目前的執行緒，因此程式碼會繼續執行要求。 在非同步處理過程中，您必須從方法傳回工作，以停止執行程式碼。

在 MVC 專案中，您不應該呼叫 Response。重新導向。 相反地，會傳回 RedirectResult。

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a>EnableViewState 和 ViewStateMode

建議：使用 ViewStateMode，而不是 EnableViewState，以提供更細微的控制哪些控制項使用檢視狀態。

當您在頁面指示詞中將 EnableViewState 設定為 false 時，頁面中的所有控制項都會停用檢視狀態，而且無法啟用。 如果您只想要針對頁面中的特定控制項啟用 [檢視狀態]，請將頁面的 [ViewStateMode] 設定為 [停用]。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

然後，只在實際需要檢視狀態的控制項上，將 [ViewStateMode] 設定為 [已啟用]。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

藉由僅針對需要的控制項啟用 [檢視狀態]，您可以壓縮網頁的檢視狀態大小。

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a>SqlMembershipProvider

建議：使用 Universal Providers。

在目前的專案範本中，SqlMembershipProvider 已由[ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)取代，這是以 NuGet 套件的形式提供。 如果您在以舊版範本建立的專案中使用 SqlMembershipProvider，您應該切換到 Universal Providers。 Universal Providers 會使用 Entity Framework 所支援的所有資料庫。

如需詳細資訊，請參閱[ASP.NET Universal Providers 簡介](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)。

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a>長時間執行的要求（> 110 秒）

建議：針對已連線的用戶端使用[websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx)或[SignalR](../../../signalr/index.md) ，並使用非同步 i/o 作業。

長時間執行的要求可能會導致您的 web 應用程式發生無法預期的結果和效能不佳。 要求的預設超時設定為110秒。 如果您使用會話狀態搭配長時間執行的要求，ASP.NET 會在110秒後釋放會話物件的鎖定。 不過，當釋放鎖定時，您的應用程式可能正在會話物件上進行作業，而此操作可能無法順利完成。 當第一個要求執行時，如果使用者的第二個要求遭到封鎖，第二個要求可能會存取處於不一致狀態的會話物件。

如果您的應用程式包含封鎖（或同步） i/o 作業，應用程式將會沒有回應。

若要改善效能，請使用 .NET Framework 中的非同步 i/o 作業。 此外，請使用 Websocket 或 SignalR 將用戶端連接到伺服器。 這些功能的設計目的是要有效率地處理長時間執行的要求。
