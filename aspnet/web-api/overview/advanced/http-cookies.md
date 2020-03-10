---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API 中的 HTTP Cookie-ASP.NET 4。x
author: MikeWasson
description: 說明如何在 ASP.NET 4.x 的 Web API 中傳送和接收 HTTP cookie。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557684"
---
# <a name="http-cookies-in-aspnet-web-api"></a>ASP.NET Web API 中的 HTTP Cookie

由[Mike Wasson](https://github.com/MikeWasson)

本主題說明如何在 Web API 中傳送和接收 HTTP cookie。

## <a name="background-on-http-cookies"></a>HTTP Cookie 的背景

本節提供如何在 HTTP 層級上實作為 cookie 的簡要總覽。 如需詳細資訊，請參閱[RFC 6265](http://tools.ietf.org/html/rfc6265)。

Cookie 是伺服器在 HTTP 回應中傳送的一段資料。 用戶端（選擇性）會儲存 cookie，並在後續要求中傳回它。 這可讓用戶端和伺服器共用狀態。 若要設定 cookie，伺服器會在回應中包含一個 Set-Cookie 標頭。 Cookie 的格式是具有選擇性屬性的名稱/值組。 例如:

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

以下是包含屬性的範例：

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

若要將 cookie 傳回給伺服器，用戶端會在後續要求中包含 Cookie 標頭。

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

HTTP 回應可以包含多個設定 Cookie 標頭。

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

用戶端會使用單一 Cookie 標頭傳回多個 cookie。

[!code-console[Main](http-cookies/samples/sample5.cmd)]

Cookie 的範圍和持續時間是由下列設定-Cookie 標頭中的屬性所控制：

- **網域**：告訴用戶端應接收 cookie 的網域。 例如，如果網域是 "example.com"，則用戶端會將 cookie 傳回給 example.com 的每個子域。 如果未指定，則網域為源伺服器。
- **Path**：將 cookie 限制在網域內的指定路徑。 如果未指定，則會使用要求 URI 的路徑。
- **過期**：設定 cookie 的到期日。 用戶端會在 cookie 到期時將其刪除。
- **最大壽命**：設定 cookie 的最長存留期。 用戶端會在達到最長存留期時刪除 cookie。

如果同時設定 `Expires` 和 `Max-Age`，`Max-Age` 會優先使用。 如果未設定，則用戶端會在目前的會話結束時刪除 cookie。 （「會話」的確切意義是由使用者代理程式所決定）。

不過，請注意，用戶端可能會忽略 cookie。 例如，使用者可能會因為隱私權原因而停用 cookie。 用戶端可能會在 cookie 過期之前予以刪除，或限制儲存的 cookie 數目。 基於隱私權原因，用戶端通常會拒絕「協力廠商」 cookie，其中的網域不符合源伺服器。 簡單地說，伺服器不應該依賴取回它所設定的 cookie。

## <a name="cookies-in-web-api"></a>Web API 中的 cookie

若要將 cookie 新增至 HTTP 回應，請建立代表 cookie 的**CookieHeaderValue**實例。 然後呼叫**AddCookies**擴充方法，其定義于**System .net. Http 中。HttpResponseHeadersExtensions**類別，以新增 cookie。

例如，下列程式碼會在控制器動作內新增 cookie：

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

請注意， **AddCookies**會採用**CookieHeaderValue**實例的陣列。

若要從用戶端要求中解壓縮 cookie，請呼叫**GetCookies**方法：

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

**CookieHeaderValue**包含**CookieState**實例的集合。 每個**CookieState**都代表一個 cookie。 使用索引子方法，依名稱取得**CookieState** ，如下所示。

## <a name="structured-cookie-data"></a>結構化 Cookie 資料

許多瀏覽器會限制他們會儲存&#8212;總數的 cookie 數，以及每個網域的數目。 因此，將結構化的資料放入單一 cookie，而不是設定多個 cookie，可能會很有用。

> [!NOTE]
> RFC 6265 不會定義 cookie 資料的結構。

使用**CookieHeaderValue**類別，您可以傳遞 cookie 資料的名稱/值組清單。 這些名稱/值配對會編碼為設定 Cookie 標頭中的 URL 編碼格式資料：

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

先前的程式碼會產生下列設定 Cookie 標頭：

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

**CookieState**類別提供索引子方法，以便從要求訊息中的 cookie 讀取子值：

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>範例：在訊息處理常式中設定和取出 Cookie

先前的範例示範如何從 Web API 控制器內使用 cookie。 另一個選項是使用[訊息處理常式](http-message-handlers.md)。 訊息處理常式會在管線中的前面叫用，而不是控制器。 訊息處理常式可以在要求到達控制器之前從要求讀取 cookie，或在控制器產生回應後將 cookie 新增至回應。

![](http-cookies/_static/image2.png)

下列程式碼顯示用來建立會話識別碼的訊息處理常式。 會話識別碼會儲存在 cookie 中。 處理常式會檢查會話 cookie 的要求。 如果要求不包含 cookie，處理常式會產生新的會話識別碼。 不論是哪一種情況，處理常式都會將會話識別碼儲存在**HttpRequestMessage**屬性包中。 它也會將會話 cookie 新增至 HTTP 回應。

此執行不會驗證來自用戶端的會話識別碼是否確實由伺服器發出。 請勿使用它做為驗證的形式！ 範例的重點在於顯示 HTTP cookie 管理。

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

控制器可以從**HttpRequestMessage**屬性包取得會話識別碼。

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
