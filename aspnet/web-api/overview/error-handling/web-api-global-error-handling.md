---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2-ASP.NET 4.x 中的全域錯誤處理
author: davidmatson
description: 概述 ASP.NET 4.x 的 ASP.NET Web API 2 中的全域錯誤處理。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 94f2d6d31d0b37f9bb0077e6258c70a2dfb1918d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557278"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的全域錯誤處理

依[David Matson](https://github.com/davidmatson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)

本主題概要說明 ASP.NET 4.x 的 ASP.NET Web API 2 中的全域錯誤處理。 現在，Web API 中沒有簡單的方法可全域記錄或處理錯誤。 某些未處理的例外狀況可以透過[例外狀況篩選器](exception-handling.md)來處理，但是例外狀況篩選無法處理的情況有好幾種。 例如:

1. 從控制器建構函式擲回的例外狀況。
2. 從訊息處理常式擲回的例外狀況。
3. 在路由期間擲回的例外狀況。
4. 回應內容序列化期間擲回的例外狀況。

我們想要提供一個簡單、一致的方式來記錄和處理這些例外狀況（可能的話）。 

處理例外狀況有兩個主要案例，這是我們可以傳送錯誤回應的情況，而我們只會記錄例外狀況。 第二種情況的範例是當串流回應內容中途擲回例外狀況時。在此情況下，因為狀態碼、標頭和部分內容已在網路上消失，所以傳送新的回應訊息的時間太晚，因此我們只會中止連接。 雖然無法處理例外狀況來產生新的回應訊息，但仍支援記錄例外狀況。 在我們可以偵測到錯誤的情況下，我們可以傳回適當的錯誤回應，如下所示：

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>現有選項

除了例外狀況[篩選](exception-handling.md)之外，現在還可以使用[訊息處理常式](../advanced/http-message-handlers.md)來觀察所有500層級的回應，但是對這些回應採取行動是很艱難的，因為它們缺少原始錯誤的相關內容。 訊息處理常式也有一些與例外狀況篩選準則相關的限制，它們可以處理這些情況。雖然 Web API 具有追蹤基礎結構來捕捉錯誤狀況，但追蹤基礎結構是為了診斷目的而設計，而且不適合在生產環境中執行。 全域例外狀況處理和記錄應該是可以在生產環境中執行並插入現有監視解決方案（例如， [ELMAH](https://code.google.com/p/elmah/) ）的服務。

### <a name="solution-overview"></a>方案概觀

 我們提供兩個新的使用者可取代服務（ [iexceptionlogger 實作](../releases/whats-new-in-aspnet-web-api-21.md)和 IExceptionHandler）來記錄和處理未處理的例外狀況。 服務非常類似，但有兩個主要差異：

1. 我們支援註冊多個例外狀況記錄器，但只能登錄一個例外狀況處理常式。
2. 例外狀況記錄器一律會被呼叫，即使我們即將中止連接也一樣。 只有當我們仍然可以選擇要傳送的回應訊息時，才會呼叫例外狀況處理常式。

這兩種服務都會提供例外狀況內容的存取權，其中包含偵測到例外狀況之位置的相關資訊，特別是[HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx)、 [HttpRequestCoNtext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)、擲回的例外狀況和例外狀況來源（下面的詳細資料）。

### <a name="design-principles"></a>設計原則

1. **沒有重大變更**因為這項功能是在次要版本中加入，所以影響解決方案的一個重要條件約束就是不會有任何重大變更，可以是類型合約或行為。 此條件約束會根據現有的 catch 區塊（將例外狀況轉換為500回應）來排除一些清除。 在後續的主要版本中，我們可能會考慮這項額外的清除作業。 如果這對您很重要，請在[ASP.NET Web API user voice](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)進行投票。
2. **維護與 WEB API 結構的一致性**Web API 的篩選器管線是處理跨領域考慮的絕佳方式，可彈性地在動作特定的控制器特定或全域範圍內套用邏輯。 篩選準則（包括例外狀況篩選器）一律會有動作和控制器內容，即使是在全域範圍註冊也一樣。 該合約對篩選而言是合理的，但這表示例外狀況篩選（即使是全域範圍）並不適用于某些例外狀況處理案例，例如來自訊息處理常式的例外狀況，而不存在任何動作或控制器內容。 如果我們想要使用篩選準則所提供的彈性範圍來處理例外狀況，我們仍然需要例外狀況篩選準則。 但是，如果我們需要處理控制器內容以外的例外狀況，我們也需要個別的結構來進行完整全域錯誤處理（沒有控制器內容和動作內容條件約束的專案）。

### <a name="when-to-use"></a>使用時機

- 例外狀況記錄器是查看 Web API 所捕捉到的所有未處理例外狀況的解決方案。
- 例外狀況處理常式是自訂 Web API 所攔截到未處理之例外狀況的所有可能回應的解決方案。
- 例外狀況篩選是處理與特定動作或控制器相關之未處理例外狀況的最簡單解決方案。

### <a name="service-details"></a>服務詳細資料

 例外狀況記錄器和處理常式服務介面是接受個別內容的簡單非同步方法： 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 我們也會為這兩個介面提供基類。 必須覆寫核心（同步或非同步）方法，才能在建議的時間進行記錄或處理。 針對記錄，`ExceptionLogger` 基類會確保每個例外狀況只會呼叫一次核心記錄方法（即使稍後再傳播呼叫堆疊並再次攔截）。 `ExceptionHandler` 基類只會針對呼叫堆疊頂端的例外狀況呼叫核心處理方法，並忽略舊版的嵌套 catch 區塊。 （這些基類的簡化版本位於下列附錄中）。`IExceptionLogger` 和 `IExceptionHandler` 都會透過 `ExceptionContext`接收例外狀況的相關資訊。

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

當架構呼叫例外狀況記錄器或例外狀況處理常式時，它一律會提供 `Exception` 和 `Request`。 除了單元測試以外，它也一定會提供 `RequestContext`。 幾乎不會提供 `ControllerContext` 和 `ActionContext` （只有在從例外狀況篩選的 catch 區塊中呼叫時）。 這很少會提供 `Response`（僅適用于在嘗試寫入回應的某些 IIS 案例中）。 請注意，因為其中一些屬性可能 `null`，所以取用者必須先檢查 `null`，才能存取例外狀況類別的成員。`CatchBlock` 這是一個字串，表示哪個 catch 區塊看到例外狀況。 Catch 區塊字串如下所示：

- HttpServer （SendAsync 方法）
- System.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync （SendAsync 方法）
- System.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPbatchhandler.sendasync （SendAsync 方法）
- IExceptionFilter （ApiController 在 ExecuteAsync 中處理例外狀況篩選器管線）
- OWIN 主機：

    - HttpMessageHandlerAdapter. BufferResponseContentAsync （用於緩衝輸出）
    - HttpMessageHandlerAdapter. CopyResponseContentAsync （用於串流輸出）
- Web 主機：

    - HttpControllerHandler. System.web.HTTP.webhost.HTTPcontrollerhandler.writebufferedresponsecontentasync 標（用於緩衝輸出）
    - HttpControllerHandler. System.web.HTTP.webhost.HTTPcontrollerhandler.writestreamedresponsecontentasync 標（用於串流輸出）
    - HttpControllerHandler. System.web.HTTP.webhost.HTTPcontrollerhandler.writeerrorresponsecontentasync 標（適用于在緩衝輸出模式下復原錯誤的失敗）

您也可以透過靜態唯讀屬性取得 catch 區塊字串清單。 （核心 catch 區塊字串位於靜態 ExceptionCatchBlocks 上; 餘數會出現在每個 OWIN 和 web 主機的靜態類別）。`IsTopLevelCatchBlock` 有助於在呼叫堆疊的最上方，遵循建議的處理例外狀況模式。 例外狀況處理常式可以讓例外狀況傳播，直到主機即將看到，而不會將例外狀況轉換成500回應。

除了 `ExceptionContext`以外，記錄器還會透過完整的 `ExceptionLoggerContext`取得一項額外的資訊：

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

第二個屬性（`CanBeHandled`）可讓記錄器識別無法處理的例外狀況。 當連接即將中止，而且無法傳送新的回應訊息時，將會通話記錄器，但***不***會呼叫此處理程式，而且記錄器可以從這個屬性識別此案例。

在 `ExceptionContext`中，處理常式會進一步取得一個屬性，它可以在完整 `ExceptionHandlerContext` 上設定來處理例外狀況：

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

例外狀況處理常式會將 `Result` 屬性設定為動作結果（例如， [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx)、 [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx)、 [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)或自訂的結果），藉此指出它已處理例外狀況。 如果 `Result` 屬性為 null，就會處理例外狀況，並重新擲回原始例外狀況。

對於呼叫堆疊頂端的例外狀況，我們採取額外的步驟，以確保回應適用于 API 呼叫端。 如果例外狀況傳播到主機，則呼叫者會看到死亡的黃色螢幕或一些其他主機提供的回應，這通常是 HTML，通常不是適當的 API 錯誤回應。 在這些情況下，結果會從非 null 開始，而且只有在自訂例外狀況處理常式明確地將它設回 `null` （未處理）時，例外狀況才會傳播到主機。 在這種情況下，將 `Result` 設定為 `null` 會對兩個案例很有用：

1. OWIN 裝載的 Web API，以及在 Web API 之前註冊的自訂例外狀況處理中介軟體。
2. 透過瀏覽器進行本機的偵錯工具，其中的黃色螢幕會實際為未處理的例外狀況提供有用的回應。

針對例外狀況記錄器和例外狀況處理常式，如果記錄器或處理常式本身擲回例外狀況，則不會執行任何動作來進行復原。 （除了讓例外狀況傳播外，如果您有更好的方法，請在此頁面底部留下意見反應）。例外狀況記錄器和處理常式的合約是它們不應讓例外狀況傳播至其呼叫端;否則，例外狀況將只會傳播，而通常所有的主機都會產生 HTML 錯誤（例如 ASP）。NET 的黃色螢幕）傳送回用戶端（通常不是預期 JSON 或 XML 的 API 呼叫者慣用的選項）。

## <a name="examples"></a>範例

### <a name="tracing-exception-logger"></a>追蹤例外狀況記錄器

下列例外狀況記錄器會將例外狀況資料傳送至設定的追蹤來源（包括 Visual Studio 中的 [調試輸出] 視窗）。

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>自訂錯誤訊息例外狀況處理常式

下列程式會產生用戶端的自訂錯誤回應，包括聯絡支援的電子郵件地址。

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>註冊例外狀況篩選準則

如果您使用 [ASP.NET MVC 4 Web 應用程式] 專案範本來建立專案，請將您的 Web API 設定程式碼放在 `WebApiConfig` 類別內的 [ *App/_Start* ] 資料夾中：

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>附錄：基類詳細資料

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
