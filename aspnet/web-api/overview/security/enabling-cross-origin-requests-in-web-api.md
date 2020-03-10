---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: 在 ASP.NET Web API 2 中啟用跨原始來源要求 |Microsoft Docs
author: MikeWasson
description: 說明如何支援 ASP.NET Web API 中的跨原始來源資源分享（CORS）。
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555703"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a>在 ASP.NET Web API 2 中啟用跨原始來源要求

由[Mike Wasson](https://github.com/MikeWasson)

> 瀏覽器安全性可防止網頁對另一個網域提出 AJAX 要求。 這種限制稱為「*相同來源原則*」，可防止惡意網站從另一個網站讀取敏感性資料。 不過，有時候您可能會想要讓其他網站呼叫您的 Web API。
>
> [跨原始來源資源分享](http://www.w3.org/TR/cors/)（CORS）是 W3C 標準，可讓伺服器放寬相同的來源原則。 使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。 CORS 比先前的技術（例如[JSONP](http://en.wikipedia.org/wiki/JSONP)）更安全且更具彈性。 本教學課程說明如何在您的 Web API 應用程式中啟用 CORS。
>
> ## <a name="software-used-in-the-tutorial"></a>教學課程中使用的軟體
>
> - [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2。2

## <a name="introduction"></a>簡介

本教學課程示範 ASP.NET Web API 中的 CORS 支援。 我們一開始會建立兩個 ASP.NET 專案，稱為「WebService」，其中裝載 Web API 控制器，另一個稱為「WebClient」，這會呼叫 WebService。 因為這兩個應用程式裝載于不同的網域，所以從 WebClient 到 WebService 的 AJAX 要求是一個跨原始來源要求。

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>什麼是「相同的來源」？

如果兩個 Url 具有相同的配置、主機和埠，則具有相同的來源。 （[RFC 6454](http://tools.ietf.org/html/rfc6454)）

這兩個 Url 具有相同的來源：

- `http://example.com/foo.html`
- `http://example.com/bar.html`

這些 Url 的來源不同于前兩個：

- `http://example.net`-不同的網域
- `http://example.com:9000/foo.html`-不同的埠
- `https://example.com/foo.html`-不同的配置
- `http://www.example.com/foo.html`-不同的子域

> [!NOTE]
> 在比較原始來源時，Internet Explorer 不會考慮此埠。

## <a name="create-the-webservice-project"></a>建立 WebService 專案

> [!NOTE]
> 本節假設您已經知道如何建立 Web API 專案。 如果沒有，請參閱[使用 ASP.NET Web API 消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。

1. 啟動 Visual Studio，並建立新的**ASP.NET Web 應用程式（.NET Framework）** 專案。
2. 在 [**新增 ASP.NET Web 應用程式**] 對話方塊中，選取 [**空白**專案] 範本。 在 [**新增資料夾和核心參考**] 底下，選取 [ **Web API** ] 核取方塊。

   ![Visual Studio 中的 [新增 ASP.NET 專案] 對話方塊](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. 使用下列程式碼，新增名為 `TestController` 的 Web API 控制器：

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. 您可以在本機執行應用程式，或部署至 Azure。 （針對本教學課程中的螢幕擷取畫面，應用程式會部署至 Azure App Service Web Apps）。若要確認 Web API 是否正常運作，請流覽至 `http://hostname/api/test/`，其中*hostname*是您部署應用程式的網域。 您應該會看到回應文字，&quot;取得：測試訊息&quot;。

   ![顯示測試訊息的網頁瀏覽器](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a>建立 WebClient 專案

1. 建立另一個**ASP.NET Web 應用程式（.NET Framework）** 專案，然後選取 [ **MVC**專案] 範本。 （選擇性）選取 [**變更驗證**] > [**無驗證**]。 您在本教學課程中不需要驗證。

   ![Visual Studio 中 [新增 ASP.NET 專案] 對話方塊中的 MVC 範本](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. 在**方案總管**中，開啟檔案*Views/Home/Index. cshtml*。 將此檔案中的程式碼取代為下列內容：

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   針對*serviceUrl*變數，請使用 WebService 應用程式的 URI。

3. 在本機執行 WebClient 應用程式，或將其發佈至另一個網站。

當您按一下 [試試看] 按鈕時，會使用下拉式方塊中列出的 HTTP 方法（GET、POST 或 PUT）將 AJAX 要求提交至 WebService 應用程式。 這可讓您檢查不同的跨原始來源要求。 目前，WebService 應用程式不支援 CORS，因此，如果您按一下按鈕，就會收到錯誤。

![瀏覽器中的「試試看」錯誤](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> 如果您在[Fiddler](https://www.telerik.com/fiddler)之類的工具中監看 HTTP 流量，您會看到瀏覽器確實傳送 GET 要求，而要求成功，但是 AJAX 呼叫傳回錯誤。 請務必瞭解，相同來源原則並不會防止瀏覽器傳送要求。 相反地，它會防止應用程式看到*回應*。

![顯示 web 要求的 Fiddler web 偵錯工具](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a>啟用 CORS

現在，讓我們在 WebService 應用程式中啟用 CORS。 首先，新增 CORS NuGet 套件。 在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [套件管理員主控台] 視窗中，輸入下列命令：

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

此命令會安裝最新的套件，並更新所有相依性，包括核心 Web API 程式庫。 使用 `-Version` 旗標，以特定版本為目標。 CORS 套件需要 Web API 2.0 或更新版本。

開啟檔案*應用程式\_Start/WebApiConfig. cs*。 將下列程式碼新增至**WebApiConfig**方法：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

接下來，將 **[EnableCors]** 屬性新增至 `TestController` 類別：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

針對 [*來源*] 參數，使用您部署 WebClient 應用程式的 URI。 這可允許來自 WebClient 的跨原始來源要求，同時仍禁止所有其他跨網域要求。 稍後，我將更詳細地說明 **[EnableCors]** 的參數。

請勿在*來源*URL 結尾包含正斜線。

重新部署已更新的 WebService 應用程式。 您不需要更新 WebClient。 現在，WebClient 的 AJAX 要求應該會成功。 GET、PUT 和 POST 方法都是允許的。

![顯示成功測試訊息的網頁瀏覽器](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a>CORS 的運作方式

本節說明在 HTTP 訊息層級的 CORS 要求中會發生什麼事。 請務必瞭解 CORS 的運作方式，讓您可以正確地設定 **[EnableCors]** 屬性，並疑難排解是否如預期般運作。

CORS 規格引進數個新的 HTTP 標頭，可啟用跨原始來源要求。 如果瀏覽器支援 CORS，它會針對跨原始來源要求自動設定這些標頭;您不需要在 JavaScript 程式碼中執行任何特殊動作。

以下是跨原始來源要求的範例。 「來源」標頭會提供提出要求之網站的網域。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

如果伺服器允許此要求，則會設定存取控制-允許來源標頭。 此標頭的值會符合原始標頭，或為萬用字元值 "\*"，表示允許任何來源。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

如果回應不包含存取控制-允許來源標頭，則 AJAX 要求會失敗。 具體而言，瀏覽器不允許此要求。 即使伺服器傳回成功的回應，瀏覽器也不會將回應提供給用戶端應用程式。

**預檢要求**

針對某些 CORS 要求，瀏覽器會在傳送資源的實際要求之前，傳送稱為「預檢要求」的其他要求。

當下列條件成立時，瀏覽器可以略過預檢要求：

- 要求方法為 GET、HEAD 或 POST，*而*
- 應用程式不會設定 [接受]、[接受語言]、[內容語言]、[內容類型] 或 [上一個事件識別碼] 以外的任何要求標頭，*以及*
- Content-type 標頭（如果已設定）為下列其中一項：

    - application/x-www-form-urlencoded
    - 多部分/表單資料
    - text/plain

有關要求標頭的規則會套用至應用程式所設定的標頭，方法是呼叫**XMLHttpRequest**物件上的**setRequestHeader** 。 （CORS 規格會呼叫這些「作者要求標頭」）。此規則並不適用于*瀏覽器*可以設定的標頭，例如使用者代理程式、主機或內容長度。

以下是預檢要求的範例：

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

預先飛行要求會使用 HTTP OPTIONS 方法。 其中包含兩個特殊標頭：

- 存取控制-要求-方法：將用於實際要求的 HTTP 方法。
- 存取控制-要求-標頭：*應用程式*在實際要求上設定的要求標頭清單。 （同樣地，這不包含瀏覽器所設定的標頭）。

以下是範例回應，假設伺服器允許此要求：

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

回應會包含一個存取控制-Allow-方法標頭，其中會列出允許的方法，並可選擇性地列出允許的標頭的「存取控制-允許-標頭」標頭。 如果預檢要求成功，瀏覽器就會傳送實際的要求，如先前所述。

通常用來測試具有預檢選項要求（例如， [Fiddler](https://www.telerik.com/fiddler)和[Postman](https://www.getpostman.com/)）之端點的工具，預設不會傳送必要的選項標頭。 確認 `Access-Control-Request-Method` 和 `Access-Control-Request-Headers` 標頭會與要求一起傳送，且選項標頭會透過 IIS 到達應用程式。

若要設定 IIS 以允許 ASP.NET 應用程式接收和處理選項要求，請將下列設定新增至應用程式在 `<system.webServer><handlers>` 區段*的 web.config 檔案*中：

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

移除 `OPTIONSVerbHandler` 可防止 IIS 處理選項要求。 取代 `ExtensionlessUrlHandler-Integrated-4.0` 可讓選項要求到達應用程式，因為預設的模組註冊只允許 GET、HEAD、POST 和 DEBUG 要求搭配無副檔名 Url。

## <a name="scope-rules-for-enablecors"></a>[EnableCors] 的範圍規則

您可以針對應用程式中的所有 Web API 控制器，啟用每個動作、每個控制器或全域的 CORS。

**每個動作**

若要為單一動作啟用 CORS，請在動作方法上設定 **[EnableCors]** 屬性。 下列範例只會針對 `GetItem` 方法啟用 CORS。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**每個控制器**

如果您在控制器類別上設定 **[EnableCors]** ，它會套用至控制器上的所有動作。 若要停用動作的 CORS，請將 **[DisableCors]** 屬性加入至動作。 下列範例會針對每個方法（`PutItem`除外）啟用 CORS。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**遍佈**

若要針對應用程式中的所有 Web API 控制器啟用 CORS，請將**EnableCorsAttribute**實例傳遞至**EnableCors**方法：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

如果您在一個以上的範圍設定此屬性，則優先順序的順序為：

1. 動作
2. 控制器
3. Global

## <a name="set-the-allowed-origins"></a>設定允許的原始來源

**[EnableCors]** 屬性的*來源*參數會指定允許哪些來源存取資源。 此值是允許的原始來源清單（以逗號分隔）。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

您也可以使用萬用字元值 "\*"，以允許來自任何來源的要求。

在允許來自任何來源的要求之前，請先仔細考慮。 這表示，任何網站實際上都可以對您的 Web API 進行 AJAX 呼叫。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a>設定允許的 HTTP 方法

**[EnableCors]** 屬性的*方法*參數會指定允許哪些 HTTP 方法存取資源。 若要允許所有方法，請使用萬用字元值 "\*"。 下列範例只允許 GET 和 POST 要求。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a>設定允許的要求標頭

本文稍早所述，預檢要求可能會包含存取控制要求標頭標題，列出應用程式所設定的 HTTP 標頭（所謂的「作者要求標頭」）。 **[EnableCors]** 屬性的*標頭*參數會指定允許的作者要求標頭。 若要允許任何標頭，請將*標頭*設定為 "\*"。 若要將特定標頭列入白名單，請將*標頭*設定為允許的標頭清單（以逗號分隔）：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

不過，瀏覽器在設定存取控制-要求標頭方面並不完全一致。 例如，Chrome 目前包含「來源」。 FireFox 不包含標準標頭（例如「接受」），即使應用程式在腳本中設定它們也一樣。

如果您將*標頭*設定為 "\*" 以外的任何專案，您應該包含至少「接受」、「內容類型」和「來源」，加上您想要支援的任何自訂標頭。

## <a name="set-the-allowed-response-headers"></a>設定允許的回應標頭

根據預設，瀏覽器不會將所有的回應標頭公開給應用程式。 預設可用的回應標頭為：

- Cache-Control
- Content-Language
- Content-Type
- 到期 (Expires)
- 上次修改時間
- 雜

CORS 規格會呼叫這些[簡單的回應標頭](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)。 若要讓應用程式可以使用其他標頭，請設定 **[EnableCors]** 的*exposedHeaders*參數。

在下列範例中，控制器的 `Get` 方法會設定名為 ' X-Custom-Header ' 的自訂標頭。 根據預設，瀏覽器不會在跨原始來源要求中公開這個標頭。 若要讓標頭可供使用，請在*exposedHeaders*中加入 ' X-Custom-header '。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a>跨原始來源要求傳遞認證

認證需要在 CORS 要求中進行特殊處理。 根據預設，瀏覽器不會傳送具有跨原始來源要求的任何認證。 認證包括 cookie 以及 HTTP 驗證配置。 若要使用跨原始來源要求傳送認證，用戶端必須將**XMLHttpRequest withCredentials**設定為 true。

直接使用**XMLHttpRequest** ：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

在 jQuery 中：

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

此外，伺服器也必須允許認證。 若要允許 Web API 中的跨原始來源認證，請將 **[EnableCors]** 屬性上的**SupportsCredentials**屬性設定為 true：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

如果此屬性為 true，HTTP 回應會包含一個存取控制-允許-認證標頭。 此標頭會告訴瀏覽器，伺服器允許跨原始來源要求的認證。

如果瀏覽器傳送認證，但回應未包含有效的存取控制-允許-認證標頭，則瀏覽器不會向應用程式公開回應，且 AJAX 要求會失敗。

請小心將**SupportsCredentials**設定為 true，因為這表示另一個網域上的網站可以代表使用者將登入使用者的認證傳送給您的 Web API，而不需要使用者知道。 CORS 規格也會指出，如果**SupportsCredentials**為 true，則設定*來源*為 &quot;\*&quot; 無效。

## <a name="custom-cors-policy-providers"></a>自訂 CORS 原則提供者

**[EnableCors]** 屬性會實行**ICorsPolicyProvider**介面。 您可以藉由建立衍生自**屬性**的類別並執行**ICorsPolicyProvider**，來提供自己的實作為。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

現在您可以將屬性套用至您要放置的任何位置 **[EnableCors]** 。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

例如，自訂 CORS 原則提供者可以從設定檔讀取設定。

除了使用屬性以外，您也可以註冊建立**ICorsPolicyProvider**物件的**ICorsPolicyProviderFactory**物件。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

若要設定**ICorsPolicyProviderFactory**，請在啟動時呼叫**SetCorsPolicyProviderFactory**擴充方法，如下所示：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a>瀏覽器支援

Web API CORS 封裝是一種伺服器端技術。 使用者的瀏覽器也必須支援 CORS。 幸好，所有主要瀏覽器的目前版本都包含[對 CORS 的支援](http://caniuse.com/cors)。
