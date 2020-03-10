---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: 專案 Katana 的總覽 |Microsoft Docs
author: howarddierking
description: ASP.NET 架構已有超過十年的時間，而平臺已啟用無數網站和服務的開發。 作為 Web & 。
ms.author: riande
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 1f28db822930cdfd2ebf4cf9bb27d173f4aa4201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617233"
---
# <a name="an-overview-of-project-katana"></a>Katana 專案概觀

依[Howard Dierking](https://github.com/howarddierking)

> ASP.NET 架構已有超過十年的時間，而平臺已啟用無數網站和服務的開發。 隨著 Web 應用程式開發策略的演變，架構也能夠以 ASP.NET MVC 和 ASP.NET Web API 之類的技術來逐步發展。 隨著 Web 應用程式開發進入雲端運算世界的下一個進化性步驟，project [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)提供了基礎元件集來 ASP.NET 應用程式，讓它們具有彈性、可攜、輕量，並提供更好的效能，而另一種方式是讓 project [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) cloud 優化您的 ASP.NET 應用程式。

## <a name="why-katana--why-now"></a>為什麼要 Katana –為什麼要這麼做？

 無論是在討論開發人員架構或使用者產品，都必須瞭解建立產品的基礎動機，其中包括知道產品的建立物件。 ASP.NET 最初是以兩個客戶為考慮而建立的。   
  
**第一組客戶是傳統 ASP 開發人員。** 在此期間，ASP 是透過 interweaving 標記和伺服器端腳本來建立動態、資料驅動的網站和應用程式的其中一種主要技術。 ASP 執行時間提供的伺服器端腳本具有一組物件，可將基礎 HTTP 通訊協定和 Web 服務器的核心層面抽象化，並提供存取其他服務，例如會話和應用程式狀態管理、快取等。雖然功能強大的傳統 ASP 應用程式在規模和複雜度的成長方面變得很困難。 這主要是因為在腳本環境中找不到結構，並結合了程式碼和標記交錯所產生的程式碼重複。 為了充分運用傳統 ASP 的優勢，同時解決一些挑戰，ASP.NET 利用 .NET Framework 的物件導向語言所提供的程式碼組織，同時保留伺服器端程式設計模型傳統 ASP 開發人員已習慣地成長。

**ASP.NET 的第二個目標客戶群組是 Windows 商務應用程式開發人員。** 不同于傳統 ASP 開發人員，他們習慣撰寫 HTML 標籤和程式碼來產生更多 HTML 標籤，WinForms 的開發人員（如他們之前的 VB6 開發人員）習慣于設計階段經驗，其中包含畫布和一組豐富的使用者介面控制項。 第一版的 ASP.NET （也稱為「Web form」）提供了類似的設計階段經驗，以及使用者介面元件的伺服器端事件模型，以及一組基礎結構功能（例如 ViewState）來建立順暢的開發人員體驗在用戶端和伺服器端程式設計之間。 Web form 在 WinForms 開發人員熟悉的具狀態事件模型底下，有效地隱藏 Web 的無狀態性質。

### <a name="challenges-raised-by-the-historical-model"></a>歷程記錄模型所引發的挑戰

**最終結果是一個成熟、功能豐富的執行時間和開發人員程式設計模型。** 不過，有了這項功能，豐富的挑戰就是幾個值得注意的問題。 首先 **，架構是整合**式的，在同一個 system.web .dll 元件（例如，使用 Web form 架構的核心 HTTP 物件）中，具有邏輯上不同的功能單位會緊密結合。 其次，ASP.NET 已包含在較大的 .NET Framework 中，這表示**發行之間的時間是以年**為單位。 這使得 ASP.NET 變得很容易，讓您在快速進化的 Web 程式開發過程中進行所有變更。 最後，system.web 本身是以幾種不同的方式結合特定的 Web 裝載選項： Internet Information Services （IIS）。

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>進化步驟： ASP.NET MVC 和 ASP.NET Web API

網頁程式開發中發生了許多變更！ Web 應用程式逐漸開發成一系列的小型、重點元件，而不是大型架構。 元件的數目以及其發行的頻率會以前所未有的速度增加。 很明顯地，保持 Web 步調會要求架構變得更小、分離且更具焦點，而不是較大且功能更豐富，因此**ASP.NET 團隊採取幾個進化的步驟，讓 ASP.NET 成為一系列的可插入 Web 元件，而不是單一架構**。

其中一項早期的變更是眾所周知的模型視圖控制器（MVC）設計模式的普及度，因為這類 Web 開發架構（例如 Ruby on Rails）。 這種建立 Web 應用程式的風格讓開發人員可以更充分掌控應用程式的標記，同時仍然保有標記和商務邏輯的分隔，這是 ASP.NET 的初始銷售要點之一。 為了滿足這種 Web 應用程式開發風格的需求，Microsoft 藉由**開發超出範圍的 ASP.NET MVC** （而不是在 .NET Framework 中），使其更適合未來的位置。 ASP.NET MVC 已發行為獨立下載。 如此一來，工程團隊就能彈性比以往更常提供更新。

Web 應用程式開發的另一項主要轉變，是將動態、伺服器產生的網頁轉換成靜態初始標記，並從用戶端腳本產生的頁面動態區段，**透過 AJAX 要求與後端 Web api**進行通訊。 此架構轉移有助於前所未見 Web Api 的增加，以及開發 ASP.NET Web API 架構。 就像 ASP.NET MVC 一樣，ASP.NET Web API 的版本提供了另一種將 ASP.NET 發展成更模組化架構的機會。 工程小組利用商機和內**建 ASP.NET Web API，讓它不會相依于在 system.web .dll 中找到的任何核心架構類型**。 這項功能已啟用兩個動作：首先，這表示 ASP.NET Web API 可以完全獨立的方式進行發展（而且它可以繼續快速地反復執行，因為它是透過 NuGet 傳遞）。 第二，由於沒有對 System.web 的外部相依性，因此不會相依于 IIS，ASP.NET Web API 包含在自訂主機（例如主控台應用程式、Windows 服務等）中執行的功能。

### <a name="the-future-a-nimble-framework"></a>未來：敏捷架構

藉由將架構元件彼此分離，然後在 NuGet 上釋放它們，framework 現在可以**更獨立且更快速地反復**執行。 此外，Web API 自我裝載功能的威力和彈性對於想要**小型、輕量主機**來提供服務的開發人員而言，非常吸引人。 它證明了，其他架構也會想要這項功能，而這也是一項新的挑戰，因為每個架構都是在自己的基底位址上，在自己的主機進程中執行，而且需要獨立管理（啟動、停止等）。 新式 Web 應用程式通常支援靜態檔案服務、動態頁面產生、Web API，以及更新的即時/推播通知。 預期每個服務都應該單獨執行和管理，其實並不切合實際。

需要的是單一裝載抽象概念，可讓開發人員從各種不同的元件和架構撰寫應用程式，然後在支援的主機上執行該應用程式。

## <a name="the-open-web-interface-for-net-owin"></a>Open Web Interface for .NET （OWIN）

 由 Ruby 社區中的[機架](http://rack.github.io/)所達成的優點來啟發，這是 .net 社區的幾個成員，可以在網頁伺服器和架構元件之間建立抽象概念。 OWIN 抽象的兩個設計目標是很簡單，而且可能會對其他架構類型採取最少的相依性。 這兩個目標有助於確保：

- 可以更輕鬆地開發和使用新的元件。
- 應用程式可以更輕鬆地在主機和可能整個平臺/作業系統之間移植。

產生的抽象概念包含兩個核心元素。 第一個是環境字典。 此資料結構負責儲存處理 HTTP 要求和回應所需的所有狀態，以及任何相關的伺服器狀態。 環境字典的定義如下：

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

OWIN 相容的 Web 服務器負責將資料填入環境字典，例如 HTTP 要求和回應的主體串流和標頭集合。 接著，應用程式或架構元件會負責填入或更新字典，並將其他值寫入回應主體資料流程。

除了指定環境字典的類型，OWIN 規格也會定義核心字典索引鍵值組的清單。 例如，下表顯示 HTTP 要求所需的字典索引鍵：

| 索引鍵名稱 | 值描述 |
| --- | --- |
| `"owin.RequestBody"` | 包含要求主體的資料流程（如果有的話）。 如果沒有要求主體，可能會使用 Null 做為預留位置。 請參閱[要求主體](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)。 |
| `"owin.RequestHeaders"` | 要求標頭的 `IDictionary<string, string[]>`。 請參閱[標頭](http://owin.org/html/owin.html#3-3-headers)。 |
| `"owin.RequestMethod"` | `string`，其中包含要求的 HTTP 要求方法（例如，`"GET"`、`"POST"`）。 |
| `"owin.RequestPath"` | 包含要求路徑的 `string`。 路徑必須相對於應用程式委派的 "root";請參閱[路徑](http://owin.org/html/owin.html#5-3-paths)。 |
| `"owin.RequestPathBase"` | `string`，其中包含對應至應用程式委派「根」之要求路徑的部分;請參閱[路徑](http://owin.org/html/owin.html#5-3-paths)。 |
| `"owin.RequestProtocol"` | 包含通訊協定名稱和版本的 `string` （例如 `"HTTP/1.0"` 或 `"HTTP/1.1"`）。 |
| `"owin.RequestQueryString"` | `string`，其中包含 HTTP 要求 URI 的查詢字串元件，沒有前置的 "？"（例如，`"foo=bar&baz=quux"`）。 此值可以是空字串。 |
| `"owin.RequestScheme"` | `string`，其中包含用於要求的 URI 配置（例如，`"http"`、`"https"`）;請參閱[URI 配置](http://owin.org/html/owin.html#5-1-uri-scheme)。 |

OWIN 的第二個主要元素是應用程式委派。 這是函式簽章，可作為 OWIN 應用程式中所有元件之間的主要介面。 應用程式委派的定義如下所示：

`Func<IDictionary<string, object>, Task>;`

然後，應用程式委派只是一個 Func 委派型別的實作為函式，其中函式會接受環境字典做為輸入，並傳回工作。 這項設計對開發人員有幾個含意：

- 需要非常少量的類型相依性，才能撰寫 OWIN 元件。 這會大幅增加 OWIN 給開發人員的存取權。
- 非同步設計讓抽象功能能夠有效率地處理運算資源，特別是在需要大量 i/o 的作業中。
- 因為應用程式委派是一個不可部分完成的執行單位，而且因為環境字典會當做委派的參數來執行，所以 OWIN 元件可以輕鬆地連結在一起，以建立複雜的 HTTP 處理管線。

從執行的觀點來看，OWIN 是一種規格（[http://owin.org/html/owin.html](http://owin.org/html/owin.html)）。 它的目標不是下一個 Web 架構，而是 Web 架構和網頁伺服器如何互動的規格。

如果您已調查過[OWIN](http://owin.org/)或[Katana](https://github.com/aspnet/AspNetKatana/wiki)，您可能也已經注意到[OWIN NuGet 封裝](http://nuget.org/packages/Owin)和 OWIN。 此程式庫包含單一介面[IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)，可將 OWIN 規格第[4 節](http://owin.org/html/owin.html#4-application-startup)所述的啟動順序正規化並制訂。 雖然不一定要建立 OWIN 伺服器，但[IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)介面會提供具象的參考點，而且它是由 Katana 專案元件所使用。

## <a name="project-katana"></a>專案 Katana

雖然[OWIN](http://owin.org/html/owin.html)規格和*OWIN*都是由社區所擁有，而社區則是執行開放原始碼的工作，但[KATANA](https://github.com/aspnet/AspNetKatana/wiki)專案代表一組 OWIN 元件，而仍然是開放原始碼，則是由 Microsoft 所建立和發行。 這些元件包括基礎結構元件，例如主機和伺服器，以及功能元件，例如驗證元件和架構的系結，例如[SignalR](../../../signalr/index.md)和[ASP.NET Web API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)。 專案具有下列三個高階目標： 

- **可移植**–元件應該能夠在新元件可供使用時輕鬆地取代。 這包括從架構到伺服器和主機的所有元件類型。 此目標的含意是，協力廠商架構可以順暢地在 Microsoft 伺服器上執行，而 Microsoft framework 可能會在協力廠商伺服器和主機上執行。
- **模組化/彈性**–不同于許多架構，其中包含預設開啟的多種功能，Katana 專案元件應該是小型且專注的，讓應用程式開發人員可以控制要在應用程式中使用哪些元件。
- **輕量/效能/可**調整–藉由將架構的傳統概念細分成一組由應用程式開發人員明確新增的小型、重點元件，產生的 Katana 應用程式可能會耗用較少的運算資源，因此可以處理更多負載，而不是使用其他類型的伺服器和架構。 由於應用程式的需求需要基礎結構的更多功能，因此可以新增至 OWIN 管線，但這應該是應用程式開發人員部分的明確決策。 此外，較低層級元件的可替代性表示當它們變成可用時，可以順暢地引進新的高效能伺服器，以提升 OWIN 應用程式的效能，而不會中斷那些應用程式。

## <a name="getting-started-with-katana-components"></a>Katana 元件的消費者入門

第一次引進時， [node.js 架構的](http://nodejs.org/)其中一個層面會立即吸引人們的注意力，這是一個可以撰寫和執行網頁伺服器的簡單性。 如果 Katana 目標是以[node.js](http://nodejs.org/)為框架，則可能會藉由指出 Katana 帶來 node.js （和架構）的許多優點，而不會強迫開發人員在開發 ASP.NET Web 應用程式時，擲出她[知道的所有](http://nodejs.org/)專案。 若要讓此語句保持為 true，開始使用 Katana 專案對[node.js](http://nodejs.org/)而言應該同樣簡單。

## <a name="creating-hello-world"></a>建立 "Hello World！"

JavaScript 和 .NET 開發之間有一項明顯的差異，就是編譯器的存在（或缺少）。 因此，簡單 Katana 伺服器的起點是 Visual Studio 專案。 不過，我們可以從最小的專案類型開始：空的 ASP.NET Web 應用程式。

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

接下來，我們會將[SystemWeb](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) NuGet 套件安裝到專案中。 此套件提供在 ASP.NET 要求管線中執行的 OWIN 伺服器。 您可以在[NuGet 資源庫](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)中找到，也可以使用 [Visual Studio 套件管理員] 對話方塊或 [套件管理員主控台] （使用下列命令）來安裝它：

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

安裝 `Microsoft.Owin.Host.SystemWeb` 套件將會安裝一些額外的套件做為相依性。 其中一個相依性是 `Microsoft.Owin`，這是一個程式庫，提供數種協助程式類型和方法來開發 OWIN 應用程式。 我們可以使用這些類型快速地撰寫下列 "hello world" 伺服器。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

這個非常簡單的 Web 服務器現在可以使用 Visual Studio 的**F5**命令來執行，並包含完整的偵錯工具支援。

## <a name="switching-hosts"></a>切換主機

根據預設，先前的 "hello world" 範例會在 ASP.NET 要求管線中執行，這會在 IIS 的內容中使用 System.web。 這可以自行增加價值，因為它可讓我們受益于 OWIN 管線的彈性和複合性，並具有 IIS 的管理功能和整體成熟度。 不過，在某些情況下，IIS 所提供的好處並不是必要的，而想要的是較小、更輕量的主機。 需要什麼，才能在 IIS 和 System.web 以外的地方執行簡單的 Web 服務器？

為了說明可攜性目標，從 Web 服務器主機移至命令列主機只需要將新的伺服器和主機相依性新增至專案的輸出檔案夾，然後啟動主機。 在此範例中，我們會將 Web 服務器裝載在名為 `OwinHost.exe` 的 Katana 主機中，並使用 Katana HttpListener 伺服器。 類似于其他 Katana 元件，這些會使用下列命令從 NuGet 取得：

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

接著，我們可以從命令列流覽至專案根資料夾，並直接執行 `OwinHost.exe` （安裝在其各自 NuGet 套件的 [工具] 資料夾中）。 根據預設，`OwinHost.exe` 會設定為尋找 HttpListener 伺服器，因此不需要額外的設定。 在網頁瀏覽器中流覽至 `http://localhost:5000/` 會顯示現在透過主控台執行的應用程式。

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana 架構

 Katana 元件架構會將應用程式分成四個邏輯層，如下所示：*主機、伺服器、中介軟體*和*應用程式*。 元件架構的分解方式是，在許多情況下，可以輕鬆地取代這些層的執行，而不需要重新編譯應用程式。   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>主機

 主機負責：

- 管理基礎進程。
- 協調工作流程，這會導致選取伺服器，以及將處理要求的 OWIN 管線的結構。

  目前，有3個主要裝載選項適用于 Katana 型應用程式：  
  
**Iis/asp.net**：使用標準 HttpModule 和 HttpHandler 類型，OWIN 管線可以在 IIS 上作為 ASP.NET 要求流程的一部分來執行。 將 SystemWeb NuGet 套件安裝到 Web 應用程式專案中，即可啟用 ASP.NET 裝載支援。 此外，由於 IIS 會同時做為主機和伺服器，因此在此 NuGet 套件中會混為一談 OWIN 伺服器/主機區分，這表示如果使用 SystemWeb 主機，開發人員就無法替代替代的伺服器。  
  
**自訂主機**： Katana 元件套件讓開發人員能夠在自己的自訂進程中裝載應用程式，不論是主控台應用程式、Windows 服務等等。這項功能看起來類似于 Web API 所提供的自我裝載功能。 下列範例顯示 Web API 程式碼的自訂主機：  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana 應用程式的自我裝載設定類似：

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Web API 與 Katana 自我裝載範例之間有一項明顯的差異，就是 Katana 自我裝載範例中缺少 Web API 設定程式碼。 為了同時啟用可攜性和複合性，Katana 會將啟動伺服器的程式碼與設定要求處理管線的程式碼分開。 設定 Web API 的程式碼，接著會包含在類別啟動中，此外也會在 WebApplication 中指定為類型參數。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

本文章稍後會更詳細地討論 startup 類別。 不過，啟動 Katana 自我裝載程式所需的程式碼，看起來與您目前在 ASP.NET Web API 自我裝載應用程式中使用的程式碼類似非常。

**OwinHost .exe**：雖然有些人會想要撰寫自訂進程來執行 Katana Web 應用程式，但許多人偏好只啟動預先建立的可執行檔，以便啟動伺服器並執行其應用程式。 在此案例中，Katana 元件套件包含 `OwinHost.exe`。 從專案的根目錄執行時，此可執行檔會啟動伺服器（預設會使用 HttpListener 伺服器），並使用慣例來尋找和執行使用者的 startup 類別。 如需更細微的控制，可執行檔會提供一些額外的命令列參數。

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>伺服器

 當主機負責啟動和維護應用程式執行所在的進程時，伺服器的責任是開啟網路通訊端，接聽要求，然後透過使用者指定的 OWIN 元件管線傳送給它們（可能已經注意到，此管線是在應用程式開發人員的 Startup 類別中指定）。 目前，Katana 專案包含兩個伺服器實現： 

- **SystemWeb**：如同先前所述，與 ASP.NET 管線共同的 IIS 會同時做為主機和伺服器。 因此，在選擇此裝載選項時，IIS 會管理主機層級的考慮，例如進程啟動和接聽 HTTP 要求。 針對 ASP.NET Web 應用程式，它接著會將要求傳送至 ASP.NET 管線。 Katana SystemWeb 主機會註冊 ASP.NET HttpModule 和 HttpHandler，以在要求流經 HTTP 管線並透過使用者指定的 OWIN 管線傳送它們時攔截它們。
- **Owin。 HttpListener**：如其名稱所示，此 Katana 伺服器會使用 .NET Framework 的 HttpListener 類別來開啟通訊端，並將要求傳送至開發人員指定的 Owin 管線。 這是 Katana 自我裝載 API 和 OwinHost 目前的預設伺服器選擇。

## <a name="middlewareframework"></a>中介軟體/架構

 如先前所述，當伺服器接受來自用戶端的要求時，它會負責透過 OWIN 元件（由開發人員的啟動程式碼所指定）的管線來傳遞它。 這些管線元件稱為中介軟體。  
 在非常基本的層級中，OWIN 中介軟體元件只需要執行 OWIN 應用程式委派，就可以呼叫它。

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

不過，為了簡化中介軟體元件的開發和撰寫，Katana 支援一些中介軟體元件的慣例和 helper 類型。 其中最常見的就是 `OwinMiddleware` 類別。 使用此類別建立的自訂中介軟體元件看起來會像下面這樣： 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 這個類別衍生自 `OwinMiddleware`，它會執行可接受管線中下一個中介軟體的實例作為其引數之一的函式，然後將它傳遞至基底函數。 其他用來設定中介軟體的引數也會在下一個中介軟體參數之後宣告為「函式參數」。   
  
在執行時間，中介軟體會透過覆寫的 `Invoke` 方法來執行。 這個方法會接受 `OwinContext`類型的單一引數。 此內容物件是由先前所述的 `Microsoft.Owin` NuGet 套件提供，並提供對要求、回應和環境字典的強型別存取權，以及一些額外的協助程式類型。   
  
中介軟體類別可以輕鬆地新增至應用程式啟動程式碼中的 OWIN 管線，如下所示：   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

由於 Katana 基礎結構只會建立 OWIN 中介軟體元件的管線，而且因為元件只需要支援應用程式委派來參與管線，所以中介軟體元件的複雜性可能會從簡單的記錄器到整個架構（例如 ASP.NET、Web API 或[SignalR](../../../signalr/index.md)）。 例如，將 ASP.NET Web API 新增至先前的 OWIN 管線時，需要新增下列啟動程式碼：

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana 基礎結構將會根據其在設定方法中新增至 IAppBuilder 物件的順序，建立中介軟體元件的管線。 在我們的範例中，LoggerMiddleware 可以處理流經管線的所有要求，而不論這些要求的最終處理方式為何。 這可實現功能強大的案例，其中中介軟體元件（例如驗證元件）可以處理包含多個元件和架構之管線（例如 ASP.NET Web API、SignalR 和靜態檔案伺服器）的要求。
 
## <a name="applications"></a>應用程式

如先前範例所述，OWIN 和 Katana 專案不應視為新的應用程式設計模型，而是用來將應用程式設計模型和架構與伺服器和裝載基礎結構分離的抽象概念。 例如，建立 Web API 應用程式時，不論應用程式是否使用 Katana 專案中的元件在 OWIN 管線中執行，開發人員架構都會繼續使用 ASP.NET Web API 架構。 應用程式開發人員可以看見 OWIN 相關程式碼的其中一個地方，就是開發人員撰寫 OWIN 管線的應用程式啟動代碼。 在啟始程式碼中，開發人員會註冊一系列的 UseXx 語句，通常是每個會處理傳入要求的中介軟體元件。 這項體驗會與在目前的 System.web 環境中註冊 HTTP 模組的效果相同。 一般而言，較大的架構中介軟體（例如 ASP.NET Web API 或[SignalR](../../../signalr/index.md) ）將會在管線的結章節附註冊。 跨領域中介軟體元件（例如用於驗證或快取的程式）通常會註冊到管線的開頭，讓它們能夠處理稍後在管線中註冊之所有架構和元件的要求。 將中介軟體元件與基礎結構元件分開，可讓元件在不同的速度上演進，同時確保整體系統保持穩定。

## <a name="components--nuget-packages"></a>元件– NuGet 套件

如同許多目前的程式庫和架構，Katana 專案元件會以一組 NuGet 套件的形式提供。 針對即將推出的版本2.0，Katana 套件相依性圖形如下所示。 （按一下影像以放大圖片）。

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Katana 專案中幾乎每個套件都會直接或間接相依于 Owin 套件。 您可能還記得這是包含 IAppBuilder 介面的套件，它提供了 OWIN 規格第4節所述之應用程式啟動順序的具體執行。 此外，許多封裝相依于 Owin，其提供一組協助程式類型來處理 HTTP 要求和回應。 套件的其餘部分可以分類為裝載基礎結構套件（伺服器或主機）或中介軟體。 Katana 專案外部的套件和相依性會以橙色顯示。

Katana 2.0 的裝載基礎結構同時包含 SystemWeb 和 HttpListener 型伺服器、使用 OWIN 執行 OWINHOST 應用程式的 OwinHost 套件，以及用於自我裝載 OWIN 應用程式的裝載套件自訂主機（例如主控台應用程式、Windows 服務等）

針對 Katana 2.0，中介軟體元件主要著重于提供不同的驗證方法。 提供診斷的一個額外中介軟體元件，其可支援 [開始] 和 [錯誤] 頁面。 隨著 OWIN 成長到事實上的裝載抽象概念，中介軟體元件的生態系統（由 Microsoft 和協力廠商開發）也會以數位成長。

## <a name="conclusion"></a>結論

 從一開始，Katana 專案的目標並不是建立，因此會強制開發人員學習另一個 Web 架構。 相反地，目標是要建立一個抽象概念，讓 .NET Web 應用程式開發人員比以前更能選擇更多的選項。 藉由將一般 Web 應用程式堆疊的邏輯層分解成一組可取代的元件，Katana 專案可讓整個堆疊中的元件以對那些元件而言合理的速率來改善。 藉由建立簡單 OWIN 抽象的所有元件，Katana 可讓架構和建置於其之上的應用程式在各種不同的伺服器和主機上都可攜。 藉由讓開發人員掌控堆疊，Katana 可確保開發人員對其 Web 堆疊的羽量級或功能豐富程度做出最佳選擇。  

## <a name="for-more-information-about-katana"></a>如需 Katana 的詳細資訊

- GitHub 上的 Katana 專案： [https://github.com/aspnet/AspNetKatana/](https://github.com/aspnet/AspNetKatana/)。
- 影片： [ASP.NET 的 Katana 專案 OWIN](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)，由 Howard Dierking。

## <a name="acknowledgements"></a>通知

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/)：（twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ） Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。
- [Scott Hanselman](http://www.hanselman.com/blog/)：（twitter [@shanselman](https://twitter.com/shanselman) ）
- [Jon Galloway](https://weblogs.asp.net/jgalloway/default.aspx)：（twitter [@jongalloway](https://twitter.com/jongalloway) ）
