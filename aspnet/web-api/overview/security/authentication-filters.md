---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 中的驗證篩選器 |Microsoft Docs
author: MikeWasson
description: 驗證篩選器是驗證 HTTP 要求的元件。 Web API 2 和 MVC 5 都支援驗證篩選，但它們稍有不同 。
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555885"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的驗證篩選

由[Mike Wasson](https://github.com/MikeWasson)

> 驗證篩選器是驗證 HTTP 要求的元件。 Web API 2 和 MVC 5 都支援驗證篩選，但它們稍有不同，大部分都是在篩選器介面的命名慣例中。 本主題描述 Web API 驗證篩選準則。

驗證篩選器可讓您設定個別控制器或動作的驗證配置。 如此一來，您的應用程式就可以針對不同的 HTTP 資源支援不同的驗證機制。

在本文中，我將在[https://github.com/aspnet/samples](https://github.com/aspnet/samples)上顯示[基本驗證](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)範例中的程式碼。 此範例顯示的驗證篩選準則會執行 HTTP 基本存取驗證配置（RFC 2617）。 此篩選準則會在名為 `IdentityBasicAuthenticationAttribute`的類別中執行。 我不會顯示範例中的所有程式碼，只是說明如何撰寫驗證篩選器的元件。

## <a name="setting-an-authentication-filter"></a>設定驗證篩選準則

就像其他篩選器一樣，驗證篩選器可以套用至每個控制器、每個動作，或全域套用至所有 Web API 控制器。

若要將驗證篩選套用至控制器，請使用 filter 屬性裝飾控制器類別。 下列程式碼會在控制器類別上設定 `[IdentityBasicAuthentication]` 篩選準則，以啟用所有控制器動作的基本驗證。

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

若要將篩選套用至一個動作，請使用篩選準則裝飾動作。 下列程式碼會在控制器的 `Post` 方法上設定 `[IdentityBasicAuthentication]` 篩選準則。

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

若要將篩選套用至所有 Web API 控制器，請將它新增至**GlobalConfiguration**。

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>執行 Web API 驗證篩選

在 Web API 中，驗證篩選準則會執行[IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)介面。 它們也應該繼承自**system.object**，以便套用為屬性。

**IAuthenticationFilter**介面有兩個方法：

- **AuthenticateAsync**會驗證要求中的認證（如果有的話）來驗證要求。
- **ChallengeAsync**會視需要將驗證挑戰新增至 HTTP 回應。

這些方法對應于[rfc 2612](http://tools.ietf.org/html/rfc2616)和[rfc 2617](http://tools.ietf.org/html/rfc2617)中定義的驗證流程：

1. 用戶端會在授權標頭中傳送認證。 這通常是在用戶端從伺服器收到401（未經授權）回應之後發生。 不過，用戶端可以使用任何要求來傳送認證，而不只是在取得401之後。
2. 如果伺服器不接受認證，則會傳回401（未經授權）的回應。 回應包含 Www 驗證標頭，其中包含一或多個挑戰。 每個挑戰都會指定伺服器所能辨識的驗證配置。

伺服器也可以從匿名要求傳回401。 事實上，這通常是驗證程式的起始方式：

1. 用戶端會傳送匿名要求。
2. 伺服器會傳回401。
3. 用戶端會以認證重新傳送要求。

此流程包含*驗證*和*授權*步驟。

- 驗證會證明用戶端的身分識別。
- 授權會決定用戶端是否可以存取特定資源。

在 Web API 中，驗證篩選器會處理驗證，而不是授權。 授權應由授權篩選或在控制器動作內部完成。

以下是 Web API 2 管線中的流程：

1. 在叫用動作之前，Web API 會建立該動作的驗證篩選器清單。 這包括具有動作範圍、控制器範圍和全域範圍的篩選準則。
2. Web API 會針對清單中的每個篩選呼叫**AuthenticateAsync** 。 每個篩選器都可以驗證要求中的認證。 如果有任何篩選成功驗證認證，篩選準則會建立**IPrincipal** ，並將它附加至要求。 篩選準則也會在此時觸發錯誤。 若是如此，管線的其餘部分就不會執行。
3. 假設沒有發生錯誤，要求會流經管線的其餘部分。
4. 最後，Web API 會呼叫每個驗證篩選器的**ChallengeAsync**方法。 篩選器會使用此方法，視需要將挑戰新增至回應。 通常（但不一定）會發生以回應401錯誤。

下圖顯示兩個可能的案例。 在第一種情況下，驗證篩選器會成功驗證要求，授權篩選準則會授權要求，而控制器動作會傳回200（確定）。

![](authentication-filters/_static/image1.png)

在第二個範例中，驗證篩選器會驗證要求，但授權篩選會傳回401（未經授權）。 在此情況下，不會叫用控制器動作。 驗證篩選準則會將 Www 驗證標頭新增至回應。

![](authentication-filters/_static/image2.png)

其他組合也可能&mdash;例如，如果控制器動作允許匿名要求，您可能會有驗證篩選準則，但沒有授權。

## <a name="implementing-the-authenticateasync-method"></a>執行 AuthenticateAsync 方法

**AuthenticateAsync**方法會嘗試驗證要求。 以下是方法簽章：

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

**AuthenticateAsync**方法必須執行下列其中一項動作：

1. 無（無 op）。
2. 建立**IPrincipal** ，並在要求上設定它。
3. 設定錯誤結果。

選項（1）表示要求沒有篩選器所瞭解的任何認證。 選項（2）表示篩選已成功驗證要求。 選項（3）表示要求具有不正確認證（例如錯誤的密碼），這會觸發錯誤回應。

以下是執行**AuthenticateAsync**的一般大綱。

1. 在要求中尋找認證。
2. 如果沒有任何認證，則不執行任何動作，也不會傳回（無 op）。
3. 如果有認證，但篩選準則無法辨識驗證配置，則不執行任何動作，也不會傳回（無 op）。 管線中的另一個篩選器可能會瞭解配置。
4. 如果有篩選器瞭解的認證，請嘗試進行驗證。
5. 如果認證不正確，請設定 `context.ErrorResult`以傳回401。
6. 如果認證有效，請建立**IPrincipal** ，並設定 `context.Principal`。

下列程式碼顯示[基本驗證](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)範例中的**AuthenticateAsync**方法。 批註會指出每個步驟。 程式碼會顯示數種類型的錯誤：沒有認證的授權標頭、認證格式不正確，以及使用者名稱/密碼不正確。

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>設定錯誤結果

如果認證無效，則篩選準則必須將 `context.ErrorResult` 設定為會建立錯誤回應的**應傳回 iHTTPactionresult** 。 如需**應傳回 iHTTPactionresult**的詳細資訊，請參閱[Web API 2 中的動作結果](../getting-started-with-aspnet-web-api/action-results.md)。

基本驗證範例包含適用于此用途的 `AuthenticationFailureResult` 類別。

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>執行 ChallengeAsync

**ChallengeAsync**方法的目的是要在需要時，將驗證挑戰新增至回應。 以下是方法簽章：

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

方法是在要求管線中的每個驗證篩選準則上呼叫。

請務必瞭解， **ChallengeAsync**是在建立 HTTP 回應*之前*呼叫，甚至可能在控制器動作執行之前進行。 呼叫**ChallengeAsync**時，`context.Result` 包含**應傳回 iHTTPactionresult**，稍後用來建立 HTTP 回應。 因此，在呼叫**ChallengeAsync**時，您還不知道 HTTP 回應的任何內容。 **ChallengeAsync**方法應該以新的**應傳回 iHTTPactionresult**取代 `context.Result` 的原始值。 此**應傳回 iHTTPactionresult**必須包裝原始 `context.Result`。

![](authentication-filters/_static/image3.png)

我會呼叫*內部結果*的原始**應傳回 iHTTPactionresult** ，而新的會**應傳回 iHTTPactionresult** *外部結果*。 外部結果必須執行下列動作：

1. 叫用內部結果以建立 HTTP 回應。
2. 檢查回應。
3. 如有需要，請將驗證挑戰新增至回應。

下列範例取自基本驗證範例。 它會定義外部結果的**應傳回 iHTTPactionresult** 。

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

`InnerResult` 屬性會保存內部**應傳回 iHTTPactionresult**。 `Challenge` 屬性代表 Www 驗證標頭。 請注意， **ExecuteAsync**會先呼叫 `InnerResult.ExecuteAsync` 來建立 HTTP 回應，然後視需要新增挑戰。

請檢查回應碼，然後再新增挑戰。 如果回應為401，大部分的驗證配置只會新增挑戰，如下所示。 不過，某些驗證配置會對成功回應新增挑戰。 例如，請參閱[Negotiate](http://tools.ietf.org/html/rfc4559#section-5) （RFC 4559）。

假設有 `AddChallengeOnUnauthorizedResult` 類別，則**ChallengeAsync**中的實際程式碼很簡單。 您只需建立結果，並將其附加至 `context.Result`。

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

注意：基本驗證範例會將此邏輯一併放在擴充方法中，藉此將它抽象化。

## <a name="combining-authentication-filters-with-host-level-authentication"></a>將驗證篩選器與主機層級驗證結合

「主機層級驗證」是由主機（例如 IIS）執行的驗證，在要求到達 Web API 架構之前。

通常，您可能會想要為應用程式的其餘部分啟用主機層級驗證，但請將它停用於您的 Web API 控制器。 例如，典型的案例是在主機層級啟用表單驗證，但針對 Web API 使用權杖型驗證。

若要在 Web API 管線內停用主機層級驗證，請在您的設定中呼叫 `config.SuppressHostPrincipal()`。 這會導致 Web API 從輸入 Web API 管線的任何要求中移除**IPrincipal** 。 實際上，它 &quot;取消驗證要求&quot;。

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>其他資源

[ASP.NET Web API 安全性篩選](https://msdn.microsoft.com/magazine/dn781361.aspx)（MSDN 雜誌）
