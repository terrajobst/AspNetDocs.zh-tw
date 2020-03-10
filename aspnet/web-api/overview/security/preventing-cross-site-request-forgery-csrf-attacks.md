---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: 防止 ASP.NET MVC 中的跨網站要求偽造（CSRF）攻擊
author: MikeWasson
description: 描述跨網站偽造要求（CSRF）攻擊，以及如何在 ASP.NET Web MVC 中執行反 CSRF 量值。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555115"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a>防止 ASP.NET MVC 應用程式中的跨網站要求偽造（CSRF）攻擊

由[Mike Wasson](https://github.com/MikeWasson)

跨網站偽造要求（CSRF）是一種攻擊，惡意網站會將要求傳送至使用者目前登入的弱點網站

以下是 CSRF 攻擊的範例：

1. 使用者使用表單驗證登入 `www.example.com`。
2. 伺服器會驗證使用者。 伺服器的回應包含驗證 cookie。
3. 若未登出，使用者會造訪惡意網站。 這個惡意網站包含下列 HTML 表單： 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    請注意，表單動作會張貼到易受攻擊的網站，而不是惡意網站。 這是 CSRF 的「跨網站」部分。
4. 使用者按一下 [提交] 按鈕。 瀏覽器會在要求中包含驗證 cookie。
5. 此要求會在伺服器上以使用者的驗證內容執行，並可執行已驗證使用者允許執行的任何動作。

雖然此範例需要使用者按一下表單按鈕，但惡意的網頁也可以輕鬆地執行自動提交表單的腳本。 此外，使用 SSL 並不會防止 CSRF 攻擊，因為惡意網站可以傳送「HTTPs://」要求。

一般來說，使用 cookie 進行驗證的網站可能會發生 CSRF 攻擊，因為瀏覽器會將所有相關的 cookie 傳送至目的地網站。 不過，CSRF 攻擊並不限於利用 cookie。 例如，基本和摘要式驗證也很容易受到攻擊。 使用者使用基本或摘要式驗證登入之後。 瀏覽器會自動傳送認證，直到會話結束為止。

## <a name="anti-forgery-tokens"></a>防偽標記

為了協助防止 CSRF 攻擊，ASP.NET MVC 會使用防偽權杖，也稱為*要求驗證權杖*。

1. 用戶端會要求包含表單的 HTML 網頁。
2. 伺服器會在回應中包含兩個權杖。 一個權杖會當做 cookie 傳送。 另一個則放在隱藏的表單欄位中。 系統會隨機產生權杖，讓敵人無法猜測值。
3. 當用戶端提交表單時，必須將這兩個權杖傳回給伺服器。 用戶端會傳送 cookie 權杖做為 cookie，並將表單 token 傳送至表單資料內。 （當使用者提交表單時，瀏覽器用戶端會自動執行此工作）。
4. 如果要求不包含這兩個權杖，伺服器就不會允許該要求。

以下是具有隱藏表單標記的 HTML 表單範例：

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

防偽 token 可以使用，因為由於相同來源的原則，惡意網頁無法讀取使用者的權杖。 （[相同來源原則](http://www.w3.org/Security/wiki/Same_Origin_Policy)會防止裝載于兩個不同網站的檔存取彼此的內容。 因此在先前的範例中，惡意網頁可以將要求傳送至 example.com，但它無法讀取回應。）

若要防止 CSRF 攻擊，請使用反偽造權杖搭配任何驗證通訊協定，瀏覽器會在使用者登入之後，以無訊息方式傳送認證。 這包括以 cookie 為基礎的驗證通訊協定，例如表單驗證，以及基本和摘要式驗證等通訊協定。

您應該針對任何 nonsafe 方法（POST、PUT、DELETE）要求防偽 token。 此外，請確定安全方法（GET、HEAD）沒有任何副作用。 此外，如果您啟用跨網域支援（例如 CORS 或 JSONP），那麼即使 GET 之類的安全方法也可能容易遭受 CSRF 攻擊，讓攻擊者能夠讀取潛在的敏感性資料。

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>ASP.NET MVC 中的防偽標記

若要將防偽標記新增至 Razor 頁面，請使用**HtmlHelper. AntiForgeryToken** helper 方法：

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

這個方法會新增隱藏的表單欄位，也會設定 cookie token。

## <a name="anti-csrf-and-ajax"></a>反 CSRF 和 AJAX

由於 AJAX 要求可能會傳送 JSON 資料，而不是 HTML 表單資料，因此，表單 token 可能會是 AJAX 要求的問題。 有一個解決方案是在自訂 HTTP 標頭中傳送權杖。 下列程式碼使用 Razor 語法來產生權杖，然後將權杖新增至 AJAX 要求。 權杖是在伺服器上藉由呼叫 AntiForgery 來產生的 **。 GetTokens**。

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

當您處理要求時，請從要求標頭擷取權杖。 然後呼叫**AntiForgery**方法來驗證權杖。 如果權杖無效， **Validate**方法會擲回例外狀況。

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
