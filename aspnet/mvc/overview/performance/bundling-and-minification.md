---
uid: mvc/overview/performance/bundling-and-minification
title: 捆綁與縮制 |Microsoft Docs
author: Rick-Anderson
description: 配套和縮制是您可以在 ASP.NET 4.5 中用來改善要求載入時間的兩個技術。 捆綁與縮制可改善載入時間，reducin 。
ms.author: riande
ms.date: 08/23/2012
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 239980d747c6e0d6be1e9b4fe0371e276e37cf21
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519280"
---
# <a name="bundling-and-minification"></a>統合及縮製

依[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 配套和縮制是您可以在 ASP.NET 4.5 中用來改善要求載入時間的兩個技術。 組合和縮制藉由減少對伺服器的要求數並減少要求的資產（例如 CSS 和 JavaScript），來改善載入時間。

目前大部分的主要瀏覽器會將每個主機名稱的[同時](http://www.browserscope.org/?category=network)連線數目限制為六個。 這表示在處理六個要求時，瀏覽器會將其他對主機資產的要求排入佇列。 在下圖中，[IE F12 開發人員工具網路] 索引標籤會顯示範例應用程式的 [關於] 視圖所需的資產時間。

![B/M](bundling-and-minification/_static/image1.png)

灰色列會顯示瀏覽器在等候六個連線限制時，將要求排入佇列的時間。 黃色的長條是要求第一個位元組的時間，也就是傳送要求和接收伺服器的第一個回應所花費的時間。 藍色橫條會顯示從伺服器接收回應資料所花費的時間。 您可以按兩下資產以取得詳細的計時資訊。 例如，下圖顯示載入 */Scripts/MyScripts/JavaScript6.js*檔案的計時詳細資料。

![](bundling-and-minification/_static/image2.png)

上圖顯示 [**啟動**] 事件，這會提供要求排入佇列的時間，因為瀏覽器會限制同時連接的數目。 在此情況下，要求會排入佇列中等候等待另一個要求完成的46毫秒。

## <a name="bundling"></a>統合

配套是 ASP.NET 4.5 中的新功能，可讓您輕鬆地將多個檔案結合或組合成單一檔案。 您可以建立 CSS、JavaScript 和其他套件組合。 較少的檔案表示 HTTP 要求較少，而且可以改善第一頁載入效能。

下圖顯示先前所示之 [關於] 視圖的相同時間觀點，但這次已啟用 [組合] 和 [縮制]。

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>縮製

縮制會對腳本或 css 執行各種不同的程式碼優化，例如移除不必要的空白字元和批註，以及將變數名稱縮短成一個字元。 請考慮下列 JavaScript 函數。

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

縮制之後，函式會縮減為下列內容：

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

除了移除批註和不必要的空白字元以外，下列參數和變數名稱已重新命名（縮短），如下所示：

| **Original** | **經過** |
| --- | --- |
| imageTagAndImageID | n |
| imageCoNtext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>捆綁與縮制的影響

下表顯示個別列出所有資產，以及在範例程式中使用配套和縮制（B/M）的幾個重要差異。

|  | **使用 B/M** | **不含 B/M 的** | **變更** |
| --- | --- | --- | --- |
| **檔案要求** | 9 | 34 | 256% |
| **已傳送 KB** | 3.26 | 11.92 | 266% |
| **已收到 KB** | 388.51 | 530 | 36% |
| **載入時間** | 510毫秒 | 780毫秒 | 53% |

因為瀏覽器在要求上套用的 HTTP 標頭相當冗長，所以傳送的位元組會大幅降低。 已接收的位元組數不大，因為最大的檔案（*腳本\\jquery-ui-1.8.11*和*腳本\\jquery-1.7.2.min.js 1.7.1. min .js*）已經縮減。 注意：範例程式上的時間會使用[Fiddler](http://www.fiddler2.com/fiddler2/)工具來模擬慢速網路。 （從 [Fiddler**規則**] 功能表中，選取 [**效能**]，然後**模擬數據機速度**）。

## <a name="debugging-bundled-and-minified-javascript"></a>已配套和縮減 JavaScript 的調試

在開發環境中，您可以輕鬆地對 JavaScript 進行偵錯工具 *（web.config 檔案*中的[編譯元素](https://msdn.microsoft.com/library/s10awwz0.aspx)會設定為 `debug="true"`），因為 javascript 檔案並未配套或縮減。 您也可以在您的 JavaScript 檔案已配套並縮減的發行組建中進行偵錯工具。 使用 IE F12 開發人員工具，您可以使用下列方法，來偵測縮減配套中包含的 JavaScript 函式：

1. 選取 [**腳本**] 索引標籤，然後選取 [**開始調試**] 按鈕。
2. 使用 [資產] 按鈕，選取包含您想要進行 debug 的 JavaScript 函式的配套。  
    ![](bundling-and-minification/_static/image4.png)
3. ![](bundling-and-minification/_static/image5.png)選取 [設定]**按鈕**，然後選取 [**格式化 javascript**]，以格式化縮減 javascript。
4. 在 [**搜尋腳本**] 輸入方塊中，選取您想要進行 debug 的函式名稱。 在下圖中，已在 [**搜尋腳本**] 輸入方塊中輸入**AddAltToImg** 。  
    ![](bundling-and-minification/_static/image6.png)

如需使用 F12 開發人員工具進行偵錯工具的詳細資訊，請參閱 MSDN 文章[使用 F12 開發人員工具來調試 JavaScript 錯誤](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)。

## <a name="controlling-bundling-and-minification"></a>控制捆綁和縮制

在*web.config*檔案的[編譯元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中設定 debug 屬性的值，即可啟用或停用組合和縮制。 在下列 XML 中，`debug` 設定為 true，因此會停用組合和縮制。

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

若要啟用捆綁和縮制，請將 `debug` 值設定為 "false"。 您可以使用 `BundleTable` 類別上的 `EnableOptimizations` 屬性來覆寫*web.config*設定。 下列程式碼會啟用捆綁和縮制，並覆寫*web.config*檔案中的任何設定。

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> 除非 `true` `EnableOptimizations`，或*web.config*檔案中[編譯](https://msdn.microsoft.com/library/s10awwz0.aspx)專案的 debug 屬性設定為 `false`，否則檔案將不會配套或縮減。 此外，將不會使用檔案的最小版本，將會選取完整的調試版本。 `EnableOptimizations` 覆寫*web.config*檔案中[編譯元素](https://msdn.microsoft.com/library/s10awwz0.aspx)的 debug 屬性

## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>搭配 ASP.NET Web Forms 和網頁使用配套和縮制

- 若為網頁，請參閱[將 Web 優化新增至 Web 網頁網站](https://docs.microsoft.com/archive/blogs/rickandy/adding-web-optimization-to-a-web-pages-site)的 blog 專案。
- 若為 Web form，請參閱[將配套和縮制新增至 web](https://docs.microsoft.com/archive/blogs/rickandy/adding-bundling-and-minification-to-web-forms)form 的 blog 專案。

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>搭配 ASP.NET MVC 使用配套和縮制

在本節中，我們將建立 ASP.NET MVC 專案，以檢查捆綁和縮制。 首先，建立名為**MvcBM**的新 ASP.NET MVC 網際網路專案，而不變更任何預設值。

開啟*應用程式\\\_開始\\BundleConfig.cs*檔案，並檢查用來建立、註冊及設定配套的 `RegisterBundles` 方法。 下列程式碼顯示 `RegisterBundles` 方法的一部分。

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

上述程式碼會建立名為 *~/bundles/jquery*的新 JavaScript 組合，其中包含所有適當的（也就是 debug 或縮減，但不含）。*vsdoc*）*腳本*資料夾中符合萬用字元字串 "~/Scripts/jquery-{version}.js" 的檔案。 針對 ASP.NET MVC 4，這表示使用 debug 設定，檔案*jquery-1.7.2.min.js 1.7.1*會新增至套件組合。 在發行設定中，將會新增*jquery-1.7.2.min.js 1.7.1。* 配套架構會遵循數個常見的慣例，例如：

- 當*FileX* *檔案存在時*，選取 ". min" 檔案以供發行。
- 選取非「最小」版本來進行 debug。
- 忽略只有 IntelliSense 才會使用的 "-vsdoc" 檔案（例如*jquery-1.7.2.min.js 1.7.1-vsdoc. .js*）。

上述的 `{version}` 萬用字元比對是用來在*腳本*資料夾中，自動建立具有適當版本 jQuery 的 jquery 套件組合。 在此範例中，使用萬用字元可提供下列優點：

- 可讓您使用 NuGet 更新為較新的 jQuery 版本，而不需變更您的 view 頁面中的先前組合程式碼或 jQuery 參考。
- 會自動選取完整版的 debug 設定和發行組建的「最小」版本。

## <a name="using-a-cdn"></a>使用 CDN

 下列程式碼會以 CDN jQuery 套件組合取代本機 jQuery 套件組合。

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

在上述程式碼中，會從 CDN 要求 jQuery，而在發行模式中，jQuery 的 debug 版本將會在本機以 debug 模式提取。 使用 CDN 時，您應該擁有回退機制，以防 CDN 要求失敗。 下列來自版面配置檔案結尾的標記片段，會顯示在 CDN 失敗時，新增至要求 jQuery 的腳本。

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>建立配套

配套[類別 `Include`](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)方法會接受字串陣列，其中每個字串都是資源的虛擬路徑。 應用程式\\中 `RegisterBundles` 方法的下列*程式碼 \_啟動\\BundleConfig.cs*檔案會顯示如何將多個檔案新增至組合：

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

提供的配套類別 `IncludeDirectory` 方法，[可在目錄](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)（及所有子目錄）中新增符合搜尋模式的所有檔案。 套件[組合類別 `IncludeDirectory`](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) API 如下所示：

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

使用 Render 方法（適用于 CSS 的`Styles.Render` 和 JavaScript 的 `Scripts.Render`）在 views 中參考配套。 下列來自*Views\\共用\\\_Layout*檔案的標記會顯示預設 ASP.NET internet project VIEW 參考 CSS 和 JavaScript 組合的方式。

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

請注意，Render 方法會接受字串陣列，因此您可以在一行程式碼中加入多個組合。 您通常會想要使用呈現方法，以建立必要的 HTML 來參考資產。 您可以使用 `Url` 方法來產生資產的 URL，而不需要參考資產所需的標記。 假設您想要使用新的 HTML5 [async](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async)屬性。 下列程式碼顯示如何使用 `Url` 方法來參考 modernizr。

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>使用 "\*" 萬用字元來選取檔案

在 `Include` 方法中指定的虛擬路徑和 `IncludeDirectory` 方法中的搜尋模式，可以接受一個 "\*" 萬用字元做為最後一個路徑區段中的前置詞或後置字元。 搜尋字串不區分大小寫。 `IncludeDirectory` 方法可選擇搜尋子目錄。

請考慮具有下列 JavaScript 檔案的專案：

- *\\Common\\AddAltToImg 的腳本*
- *\\Common\\ToggleDiv 的腳本*
- *\\Common\\ToggleImg 的腳本*
- *\\Common\\Sub1\\ToggleLinks 的腳本*

![dir imag](bundling-and-minification/_static/image7.png)

下表顯示使用萬用字元新增至組合的檔案，如下所示：

| **Call** | **已新增檔案或引發例外狀況** |
| --- | --- |
| Include （"~/Scripts/Common/\*.js"） | *AddAltToImg .js*、 *ToggleDiv*、 *ToggleImg .js* |
| Include （"~/Scripts/Common/T\*.js"） | 不正確模式例外狀況。 萬用字元只允許用於前置詞或後置字元。 |
| 包含（"~/Scripts/Common/\*og。\*"） | 不正確模式例外狀況。 只允許一個萬用字元。 |
| Include （"~/Scripts/Common/T\*"） | *ToggleDiv .js*、 *ToggleImg* |
| Include （"~/Scripts/Common/\*"） | 不正確模式例外狀況。 純萬用字元區段無效。 |
| IncludeDirectory （"~/Scripts/Common"，"T\*"） | *ToggleDiv .js*、 *ToggleImg* |
| IncludeDirectory （"~/Scripts/Common"，"T\*"，true） | *ToggleDiv .js*、 *ToggleImg*、 *ToggleLinks .js* |

將每個檔案明確新增至套件組合通常是檔案的萬用字元載入的慣用選項，原因如下：

- 依萬用字元新增腳本預設為依字母順序載入，這通常不是您想要的。 CSS 和 JavaScript 檔案經常需要以特定（非英文字母）順序加入。 您可以藉由新增自訂[IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)執行來降低這項風險，但明確新增每個檔案較不容易出錯。 例如，您可能會在未來將新資產新增至資料夾，這可能會要求您修改[IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)的執行。
- 使用萬用字元載入來查看新增至目錄的特定檔案，可以包含在所有參考該組合的視圖中。 如果將 view 特定的腳本新增至組合，您可能會在參考該組合的其他視圖上收到 JavaScript 錯誤。
- 匯入其他檔案的 CSS 檔案會導致匯入的檔案載入兩次。 例如，下列程式碼會建立套件組合，其中大部分的 jQuery UI 主題 CSS 檔案都會載入兩次。 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  萬用字元選取器 "\*.css 會帶入資料夾中的每個 CSS 檔案，包括*內容\\主題\\基底\\jquery. ui. 所有 .css*檔案。 *Jquery. 所有 .css 檔案都會*匯入其他 css 檔案。

## <a name="bundle-caching"></a>套件組合快取

配套會從建立組合後的一年設定 HTTP Expires 標頭。 如果您流覽至先前查看的頁面，Fiddler 會顯示 IE 不會對配套進行條件式要求，亦即，來自 IE 的 HTTP GET 要求無法用於組合，而且沒有來自伺服器的 HTTP 304 回應。 您可以強制 IE 使用 F5 鍵對每個組合提出條件式要求（針對每個組合產生 HTTP 304 回應）。 您可以使用 ^ F5 強制執行完整重新整理（針對每個組合產生 HTTP 200 回應）。

下圖顯示 [Fiddler 回應]**窗格的 [快取] 索引**標籤：

![fiddler 快取影像](bundling-and-minification/_static/image8.png)

要求   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 適用于配套**AllMyScripts** ，而且包含查詢字串組**v = R0sLDicvP58AIXN\\\_mc3QdyVvVj5euZNzdsa2N1PKvb81**。 查詢字串**v**具有值 token，這是用於快取的唯一識別碼。 只要配套不會變更，ASP.NET 應用程式就會使用此權杖來要求**AllMyScripts**配套。 如果組合中的任何檔案有所變更，ASP.NET 優化架構將會產生新的權杖，以確保配套的瀏覽器要求會取得最新的配套。

如果您執行 IE9 F12 開發人員工具，並流覽至先前載入的頁面，IE 會錯誤地顯示對每個組合和傳回 HTTP 304 的伺服器提出的條件式 GET 要求。 您可以閱讀為什麼 IE9 在使用 Cdn 和 Expires 的 blog 專案中決定條件式要求[，以提升網站效能](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)的原因。

## <a name="less-coffeescript-scss-sass-bundling"></a>LESS、CoffeeScript、SCSS、Sass 配套。

配套和縮制架構提供處理中繼語言（例如[SCSS](http://sass-lang.com/)、 [Sass](http://sass-lang.com/)、 [LESS](http://www.dotlesscss.org/)或[Coffeescript](http://coffeescript.org/)）的機制，並將縮制之類的轉換套用至產生的配套。 例如，若要將[較少的](http://www.dotlesscss.org/)檔案新增至 MVC 4 專案：

1. 建立較少內容的資料夾。 下列範例會使用*Content\\MyLess*資料夾。
2. 將[較少](http://www.dotlesscss.org/)的**NuGet 套件新增至您的專案**。  
    ![NuGet 無點安裝](bundling-and-minification/_static/image9.png)
3. 新增可實[IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx)介面的類別。 對於較少的轉換，請將下列程式碼新增至您的專案。

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. 使用 `LessTransform` 和[CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx)轉換建立較少檔案的組合。 將下列程式碼新增至*應用程式\\_Start\\BundleConfig.cs*檔案中的 `RegisterBundles` 方法。

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. 將下列程式碼新增至任何參考較少組合的視圖。

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>配套考慮

建立配套時應遵循的良好慣例是將「配套」納入套件組合名稱中的前置詞。 這會防止可能的[路由衝突](https://forums.asp.net/post/5012037.aspx)。

一旦您更新配套中的一個檔案，就會為配套查詢字串參數產生新的權杖，而且必須在下次用戶端要求包含配套的頁面時，下載完整的配套。 在個別列出每個資產的傳統標記中，只會下載已變更的檔案。 經常變更的資產可能不適合用來進行捆綁。

組合和縮制主要會改善第一頁的要求載入時間。 一旦要求網頁之後，瀏覽器就會快取資產（JavaScript、CSS 和影像），因此當要求相同的頁面或相同網站上要求相同資產的頁面時，配套和縮制不會提供任何效能提升。 如果您未在資產上正確設定 expires 標頭，且未使用配套和縮制，則瀏覽器的「有效啟發學習法」會在幾天後將資產標示為過時，而且瀏覽器將需要每個資產的驗證要求。 在此情況下，在第一頁要求之後，組合和縮制會提供效能增加。 如需詳細資訊，請參閱[使用 cdn 和 Expires 的 blog，以改善網站效能](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)。

藉由使用[CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)，可以降低每個主機名稱的六個同步連線的瀏覽器限制。 由於 CDN 的主機名稱會與您的主控網站不同，因此來自 CDN 的資產要求不會計算到裝載環境的六個同時連線限制。 CDN 也可以提供常見的套件快取和邊緣快取優勢。

組合應該依需要的頁面進行分割。 例如，網際網路應用程式的預設 ASP.NET MVC 範本會建立與 jQuery 分開的 jQuery 驗證配套。 因為所建立的預設 views 沒有輸入，而且不會張貼值，所以它們不會包含驗證配套。

`System.Web.Optimization` 命名空間會實作為*system.web.* 它會利用 WebGrease 程式庫（*WebGrease*）來取得縮制功能，而這又會使用*Antlr3*。

*我使用 Twitter 來進行快速貼文及分享連結。我的 Twitter 控制碼為*： [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>其他資源

- 影片： [Howard Dierking](https://twitter.com/#!/howard_dierking)的組合[和優化](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing)
- [將 Web 優化新增至 Web Pages 網站](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)。
- [將配套和縮制新增至 Web Forms](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)。
- [Henrik F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk) [的網頁流覽上的組合和縮制效能影響](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx)
- [使用 cdn 和 Expires](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx) ，透過 Rick Anderson [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)改善網站效能
- [最小化 RTT （來回時間）](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>參與者

- Hao Kung
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose
