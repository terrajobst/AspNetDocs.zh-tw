---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 |Microsoft Docs
author: rick-anderson
description: 本檔說明 ASP.NET MVC 4 的發行版本。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: b57480bd0274fbb76c600dfb0dd09037bdcbf1e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563424"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> 本檔說明 ASP.NET MVC 4 的發行版本。

- [安裝注意事項](#_Toc303253802)
- [文件](#_Toc303253803)
- [支援](#_Toc303253804)
- [軟體需求](#_Toc303253805)
- [ASP.NET MVC 4 的新功能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [預設專案範本的增強功能](#_Toc303253808)
    - [行動專案範本](#_Toc303253809)
    - [顯示模式](#_Toc303253810)
    - [jQuery Mobile、視圖切換器和瀏覽器覆寫](#_Toc303253811)
    - [非同步控制器的工作支援](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [資料庫移轉](#_Toc303253818)
    - [空白專案範本](#_Toc303253819)
    - [將控制器新增至任何專案資料夾](#_Toc303253820)
    - [統合和縮製](#_Toc303253821)
    - [使用 OAuth 和 OpenID 啟用 Facebook 和其他網站的登入](#_Toc303253822)
- [將 ASP.NET MVC 3 專案升級至 ASP.NET MVC 4](#_Toc303253806)
- [ASP.NET MVC 4 發行候選版本的變更](#_Toc303253817)
- [已知問題和重大變更](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>安裝注意事項

您可以使用 Web Platform Installer，從[ASP.NET MVC 4 首頁](../mvc/mvc4.md)安裝適用于 Visual Studio 2010 的 ASP.NET mvc 4。

我們建議您先卸載任何先前安裝的 ASP.NET MVC 4 預覽，再安裝 ASP.NET MVC 4。 您可以將 ASP.NET MVC 4 Beta 和發行候選版本升級為 ASP.NET MVC 4，而不需要卸載。

此版本與任何 .NET Framework 4.5 的預覽版本不相容。 您必須在安裝 ASP.NET MVC 4 之前，將 .NET Framework 4.5 的任何已安裝預覽版本分別升級為最終版本。

ASP.NET MVC 4 可以與 ASP.NET MVC 3 並存安裝及執行。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>文件

ASP.NET MVC 文件位於 MSDN 網站上，其 URL 如下所示：

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

如需有關 ASP.NET MVC 的教學課程和其他資訊，請在 ASP.NET 網站的 MVC 4 頁面（[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)）中找到。

<a id="_Toc303253804"></a>
## <a name="support"></a>支援

ASP.NET MVC 4 完全受到支援。 如果您有關于使用此版本的問題，您也可以將其張貼至 ASP.NET MVC 論壇（[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)），其中 ASP.NET 社區的成員經常能夠提供非正式的支援。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>軟體需求

Visual Studio 的 ASP.NET MVC 4 元件需要 PowerShell 2.0，以及 Visual Studio 2010 Service Pack 1 或 Visual Web Developer Express 2010 （含 Service Pack 1）。

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>ASP.NET MVC 4 的新功能

本節說明 ASP.NET MVC 4 版本中引進的功能。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 包含 ASP.NET Web API，這是建立 HTTP 服務的新架構，可以連接到各種用戶端，包括瀏覽器和行動裝置。 ASP.NET Web API 也是建立 RESTful 服務的理想平臺。

ASP.NET Web API 包含下列功能的支援：

- **新式 HTTP 程式設計模型：** 使用新的強型別 HTTP 物件模型，直接存取和操作 Web Api 中的 HTTP 要求和回應。 相同的程式設計模型和 HTTP 管線會透過新的*HttpClient*類型在用戶端上對稱使用。
- **路由的完整支援：** ASP.NET Web API 支援一組完整的路由功能 ASP.NET 路由，包括路由參數和條件約束。 此外，使用簡單慣例將動作對應至 HTTP 方法。
- **內容協商：** 用戶端和伺服器可以一起使用，以判斷從 Web API 傳回之資料的正確格式。 ASP.NET Web API 提供 XML、JSON 和表單 URL 編碼格式的預設支援，您可以新增自己的格式器，或甚至取代預設的內容協商策略，以擴充這項支援。
- **模型系結和驗證：** 模型系結器提供簡單的方法，可從 HTTP 要求的各個部分解壓縮資料，並將這些訊息部分轉換成可供 Web API 動作使用的 .NET 物件。 也會根據資料批註，在動作參數上執行驗證。
- **篩選器：** ASP.NET Web API 支援篩選準則，包括知名的篩選準則，例如 *[授權]* 屬性。 您可以撰寫並插入您自己的篩選準則，以進行動作、授權和例外狀況處理。
- **查詢撰寫：** 在傳回*IQueryable*的動作上使用 *[可查詢]* 篩選屬性，以支援透過 OData 查詢慣例來查詢您的 Web API。
- **改良**的可測試性：Web API 動作會與*HttpRequestMessage*和*HttpResponseMessage*的實例搭配使用，而不是在靜態內容物件中設定 HTTP 詳細資料。 建立單元測試專案和您的 Web API 專案，以快速開始為您的 Web API 功能撰寫單元測試。
- 以**程式碼為基礎的設定：** ASP.NET Web API 設定只會透過程式碼完成，讓您的設定檔保持乾淨。 使用提供的服務定位器模式來設定擴充點。
- **改良的控制反轉（IoC）容器支援：** ASP.NET Web API 透過改良的相依性解析程式抽象概念，提供 IoC 容器的絕佳支援
- **自我裝載：** Web Api 除了 IIS 之外，也可以裝載于您自己的進程中，同時仍然使用路由的完整功能和 Web API 的其他功能。
- **建立自訂說明和測試頁面：** 現在您可以使用新的*IApiExplorer*服務來取得 web api 的完整執行時間描述，輕鬆地為您的 web api 建立自訂說明和測試頁面。
- **監視和診斷：** ASP.NET Web API 現在提供輕量追蹤基礎結構，可讓您輕鬆地與現有的記錄解決方案（例如，系統診斷、ETW 和協力廠商記錄架構）整合。 您可以提供*ITraceWriter*的執行，並將它新增至您的 Web API 設定，藉以啟用追蹤。
- **連結產生：** 使用 ASP.NET Web API *UrlHelper* ，在相同的應用程式中產生相關資源的連結。
- **WEB API 專案範本：** 選取新的 [MVC 4 專案] [新的 Web API 專案] 表單，以快速啟動並執行 ASP.NET Web API。
- 樣板 **：** 使用 [**新增控制器**] 對話方塊，根據以 Entity Framework 為基礎的模型類型，快速 scaffold Web API 控制器。

如需 ASP.NET Web API 的詳細資訊，請流覽[https://www.asp.net/web-api](../web-api/index.md)。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>預設專案範本的增強功能

用來建立新 ASP.NET MVC 4 專案的範本已更新，以建立更現代化的網站：

![](mvc4-release-notes/_static/image1.png)

除了表面改良以外，新的範本中還有改進的功能。 此範本採用一種稱為適應性轉譯的技術，在桌面瀏覽器和行動瀏覽器中都不需要任何自訂。

![](mvc4-release-notes/_static/image2.png)

若要查看作用中的調適型轉譯，您可以使用行動模擬器，或只嘗試調整桌面瀏覽器視窗的大小。 當瀏覽器視窗夠小時，頁面的版面配置就會變更。

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>行動專案範本

如果您要開始新的專案，並想要特別針對行動和平板電腦瀏覽器建立網站，則可以使用 [新增行動應用程式] 專案範本。 這是以 jQuery Mobile 為基礎，這是一個開放原始碼程式庫，可用於建立觸控優化的 UI：

![](mvc4-release-notes/_static/image3.png)

此範本包含與網際網路應用程式範本相同的應用程式結構（而且控制器程式碼幾乎完全相同），但它是使用 jQuery Mobile 樣式化，在觸控式行動裝置上外觀良好並表現良好。 若要深入瞭解如何結構和樣式行動 UI，請參閱[JQuery mobile 專案網站](http://jquerymobile.com/)。

如果您已經有想要新增行動優化視圖的桌面導向網站，或者您想要建立單一網站來提供不同的樣式視圖給桌上型電腦和行動瀏覽器，您可以使用新的顯示模式功能。 (請參閱下節)。

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>顯示模式

新的顯示模式功能可讓應用程式根據提出要求的瀏覽器選取 views。 例如，如果桌面瀏覽器要求首頁，應用程式可能會使用 Views\Home\Index.cshtml 範本。 如果行動瀏覽器要求首頁，應用程式可能會傳回 Views\Home\Index.mobile.cshtml 範本。

您也可以針對特定瀏覽器類型覆寫版面配置和部分。 例如:

- 如果您的 [Views\Shared] 資料夾同時包含 [\_配置] 和 [\_配置]，則應用程式預設會在行動瀏覽器的要求期間使用 \_的配置，而在其他要求期間則會 \_配置. cshtml。
- 如果資料夾同時包含 \_MyPartial 和 \_MyPartial，則指令 @Html.Partial（"\_MyPartial"）會在行動瀏覽器的要求期間轉譯 \_MyPartial，並在其他要求期間 \_MyPartial. cshtml。

如果您想要為其他裝置建立更特定的視圖、配置或部分視圖，您可以註冊新的*DefaultDisplayMode*實例，以指定當要求符合特定條件時要搜尋的名稱。 例如，您可以將下列程式碼新增至 global.asax 檔案中的*應用程式\_Start*方法，將字串 "iPhone" 註冊為當 Apple iPhone 瀏覽器提出要求時適用的顯示模式：

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

在此程式碼執行之後，當 Apple iPhone 瀏覽器提出要求時，您的應用程式將會使用 Views\Shared\\_Layout iPhone. cshtml 配置（如果有的話）。 如需「顯示模式」的詳細資訊，請參閱[ASP.NET MVC 4 Mobile Features](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)。 使用 DisplayModeProvider 的應用程式應該安裝已[修正的 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 套件。 [ASP.NET 秋季2012更新](https://go.microsoft.com/fwlink/?LinkID=271322)在新的專案範本中包含了[固定的 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 套件。 如需修正的詳細資訊，請參閱[ASP.NET MVC 4 Mobile 快取 Bug Fixedd](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>jQuery Mobile 和行動功能

如需使用 jQuery Mobile 以 ASP.NET MVC 4 來建立行動應用程式的相關資訊，請參閱[ASP.NET MVC 4 行動功能](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)教學課程。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>非同步控制器的工作支援

您現在可以將非同步動作方法撰寫為單一方法，以傳回*task*或 task 類型的物件 *&lt;ActionResult&gt;* 。

 如需詳細資訊，請參閱[使用 ASP.NET MVC 4 中的非同步方法](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 支援1.6 和更新版本的 Windows Azure SDK。

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>資料庫移轉

ASP.NET MVC 4 專案現在包含 Entity Framework 5。 Entity Framework 5 的其中一個絕佳功能就是支援資料庫移轉。 這項功能可讓您使用以程式碼為主的遷移，輕鬆地發展資料庫架構，同時保留資料庫中的資料。 如需資料庫移轉的詳細資訊，請參閱[ASP.NET MVC 4 簡介教學](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)課程中的[將新欄位新增至電影模型和資料表](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md)。

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>空白專案範本

MVC 空白專案範本現在真的是空的，因此您可以從全新的平板電腦開始。 較舊版本的空白專案範本已重新命名為 [基本]。

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>將控制器新增至任何專案資料夾

您現在可以按一下滑鼠右鍵，然後選取 MVC 專案中任何資料夾的 [**新增控制器**]。 這可讓您以更大的彈性來組織您想要的控制器，包括將 MVC 和 Web API 控制器保留在不同的資料夾中。

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>統合和縮製

捆綁套件和縮制架構可讓您將個別檔案結合成腳本和 CSS 的單一配套檔案，藉此減少網頁需要進行的 HTTP 要求數目。 然後，它可以藉由縮小配套的內容來減少這些要求的整體大小。 縮小可以包含像是刪除空白字元來縮短變數名稱，甚至根據其語義折迭 CSS 選取器的活動。 套件組合會在程式碼中宣告和設定，而且可透過協助程式方法輕鬆地在 views 中參考，這可以產生組合的單一連結，或在進行偵錯工具時，針對組合的個別內容提供多個連結。 如需詳細資訊[，請參閱捆綁和縮制](../mvc/overview/performance/bundling-and-minification.md)。

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>使用 OAuth 和 OpenID 啟用 Facebook 和其他網站的登入

ASP.NET MVC 4 網際網路專案範本中的預設範本現在包含使用 DotNetOpenAuth 程式庫的 OAuth 和 OpenID 登入支援。 如需設定 OAuth 或 OpenID 提供者的詳細資訊，請參閱[WebForms、MVC 和網頁的 oauth/OpenID 支援](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx)和[ASP.NET Web Pages 中的 oauth 和 openid 功能檔](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup)。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>將 ASP.NET MVC 3 專案升級至 ASP.NET MVC 4

ASP.NET MVC 4 可以與 ASP.NET MVC 3 並存安裝在同一部電腦上，讓您有彈性選擇何時將 ASP.NET MVC 3 應用程式升級為 ASP.NET MVC 4。

最簡單的升級方式是建立新的 ASP.NET MVC 4 專案，並將所有的視圖、控制器、程式碼和內容檔案從現有的 MVC 3 專案複製到新的專案，然後更新新專案中的元件參考，以符合中的任何非 MVC 範本您正在使用的 cluded 元件。 如果您已變更 MVC 3 專案中的 web.config 檔案，則也必須將這些變更合併到 MVC 4 專案的 web.config 檔案中。

若要將現有的 ASP.NET MVC 3 應用程式手動升級為第4版，請執行下列動作：

1. 在專案的所有 web.config 檔案中（專案的根目錄中有一個，其中一個位於 Views 資料夾，另一個位於專案中每個區域的 Views 資料夾中），取代下列文字的每個實例（注意：在中找不到 System.web、Version = 1.0.0.0）。以 Visual Studio 2012 建立的專案）： 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    具有下列對應的文字：

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. 在根 web.config 檔案中，將*網頁： Version*專案更新為 "2.0.0.0"，並加入值為 "true" 的新*PreserveLoginUrl*機碼： 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. 在方案總管中，以滑鼠右鍵按一下 [參考]，然後選取 [管理 NuGet 套件]。 在左窗格中，選取 [ **Online\NuGet 官方套件來源**]，然後更新下列各項：

    - ASP.NET MVC 4
    - （選擇性） jQuery、jQuery 驗證和 jQuery UI
    - 選擇性Entity Framework
    - 選擇性Modernizr
4. 在方案總管中，以滑鼠右鍵按一下專案名稱，然後選取 [卸載專案]。 然後再次以滑鼠右鍵按一下名稱，然後選取 [編輯*專案*名稱 .csproj]。
5. 找出*ProjectTypeGuids*元素，並將 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 取代為 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。
6. 儲存變更，關閉您編輯的專案（.csproj）檔案，以滑鼠右鍵按一下專案，然後選取 [重載專案]。
7. 如果專案參考使用舊版 ASP.NET MVC 編譯的任何協力廠商程式庫，請開啟根 web.config 檔案，然後*在 [設定*] 區段下新增下列三個*bindingRedirect*元素： 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>ASP.NET MVC 4 發行候選版本的變更

您可以在這裡找到 ASP.NET MVC 4 候選版的版本資訊：

在此版本中，ASP.NET MVC 4 發行候選版本的重大變更摘要如下：

- **每個控制器設定：** ASP.NET Web API 控制器可以使用自訂屬性進行屬性化，以執行*IControllerConfiguration*來設定自己的格式器、動作選取器和參數系結器。 已移除*HttpControllerConfigurationAttribute* 。
- **每個路由訊息處理常式：** 您現在可以針對指定的路由，在要求鏈中指定最後的訊息處理常式。 這可支援進行中的架構，以使用路由來分派至自己的（非*IHttpController*）端點。
- **進度通知：** *ProgressMessageHandler*會為所上傳的要求實體和正在下載的回應實體產生進度通知。 使用此處理程式，可以追蹤您上傳要求本文的程度，或下載回應本文。
- **推送內容：** *PushStreamContent*類別可讓資料產生者想要使用資料流程直接寫入至要求或回應（以同步或非同步方式）。 當*PushStreamContent*準備好接受資料時，它會呼叫具有輸出資料流程的動作委派。 然後，開發人員可以視需要寫入資料流程，並在寫入完成時關閉資料流程。 *PushStreamContent*會偵測資料流程的關閉，並完成基礎*的非同步工作*來寫出內容。
- **建立錯誤回應：** 使用*HttpError*類型，以一致的方式表示錯誤資訊，例如驗證錯誤和例外狀況，同時仍會接受*IncludeErrorDetailPolicy*。 使用新的*CreateErrorResponse*擴充方法，輕鬆地以*HttpError*做為內容來建立錯誤回應。 *HttpError*內容已完全協商內容。
- **MediaRangeMapping 已移除：** 媒體類型範圍現在是由預設內容 negotiator 處理。
- **簡單型別參數的預設參數系結現在是 [FromUri]：** 在舊版的中 ASP.NET Web API 使用模型系結之簡單型別參數的預設參數系結。 簡單型別參數的預設參數系結現在是 *[FromUri]* 。
- **動作選取會接受必要的參數：** 如果提供來自 URI 的所有必要參數，ASP.NET Web API 中的動作選取專案現在只會選取動作。 參數可以指定為選擇性，方法是在動作方法簽章中提供引數的預設值。
- **自訂 HTTP 參數**系結：使用*ParameterBindingAttribute*來自訂特定動作參數的參數系結，或使用*HttpConfiguration*上的*ParameterBindingRules* ，更廣泛地自訂參數系結。
- **MediaTypeFormatter 改良功能：** 格式化程式現在可以存取完整的*HttpContent*實例。
- **主機緩衝原則選取：** 在 ASP.NET Web API 中執行和設定*IHostBufferPolicySelector*服務，讓主機判斷使用緩衝處理時的原則。
- **以主機不可知的方式存取用戶端憑證：** 使用*GetClientCertificate*擴充方法，從要求訊息取得提供的用戶端憑證。
- **內容協調**擴充性：藉由衍生自*DefaultContentNegotiator*並覆寫任何您想要的內容協商層面，來自訂內容協調。
- **支援傳回406無法接受的回應：** 當您建立*DefaultContentNegotiator*並將*excludeMatchOnTypeOnly*參數設定為*true*時，您現在可以在 ASP.NET Web API 中傳回406無法接受的回應。
- 將**表單資料讀取為 NameValueCollection 或 JToken：** 您可以分別使用*ParseQueryString*和*ReadAsFormDataAsync*擴充方法，在 URI 查詢字串或要求本文中讀取表單資料，做為*NameValueCollection* 。 同樣地，您可以分別使用*TryReadQueryAsJson*和*ReadAsAsync*&lt;t&gt; 擴充方法，在 URI 查詢字串或要求本文中讀取表單資料，以做為*JToken* 。
- **多部分改善：** 現在可以撰寫完全針對 MIME 多部分資料類型量身打造的*MultipartStreamProvider* ，讓它能夠讀取並以最佳方式向使用者呈現結果。 您也可以在*MultipartStreamProvider*上攔截後置處理步驟，讓執行程式在 MIME 多部分主體元件上執行所需的任何後置處理。 例如， *MultipartFormDataStreamProvider*的實體系會讀取 HTML 表單資料部分，並將其加入至*NameValueCollection* ，以便從呼叫者輕鬆取得。
- **連結產生改良功能：** *UrlHelper*不再相依于*system.web.HTTP.controllers.HTTPcontrollercoNtext*。 您現在可以從任何可使用*HttpRequestMessage*的內容存取*UrlHelper* 。
- **訊息處理常式執行順序變更：** 訊息處理常式現在會依其設定循序執行，而不是反向順序。
- 連接**訊息處理常式的 Helper：** 可以連線*DelegatingHandlers*並建立*HttpClient*的新*HttpClientFactory* ，並準備好要執行的管線。 它也提供連接替代內部處理常式的功能（預設值為*HttpClientHandler*），以及在使用*HttpMessageInvoker*或另一個*DelegatingHandler*而非*HttpClient*做為最上層啟動程式時，執行的線路。
- **支援 ASP.NET Web 優化中的 cdn：** ASP.NET Web 優化現在提供 CDN 替代路徑的支援，可讓您為每個配套指定一個額外的 URL，以指向內容傳遞網路上的相同資源。 支援 Cdn 可讓您讓您的腳本和樣式組合在地理上更接近 Web 應用程式的終端消費者。 當 CDN 無法使用時，生產應用程式應該會執行回退。 測試回退。
- **ASP.NET Web API 路由和設定已移至*WebApiConfig。請註冊*可在測試程式碼中 resused 的靜態方法。** 先前已在*RouteConfig*中新增 ASP.NET Web API 路由和標準 MVC 路由。 預設 ASP.NET Web API 路由和設定會在個別的 WebApiConfig 中處理 *。請註冊*方法以加速測試。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

- **當行動裝置應該傳回時，RC 和 RTM 版本的 ASP.NET MVC 4 會錯誤地傳回快取的桌面視圖。**

    - 如需修正的詳細資訊，請參閱 < [ASP.NET MVC 4](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)行動快取錯誤修正。 您可以從[Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 套件安裝修正程式。
- **Razor View 引擎中的重大變更**。 下列類型已從*system.web*移除： 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  下列方法也已移除： 

    - *MvcCSharpRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
    - *MvcWebPageRazorHost. DecorateCodeGenerator （System.web. RazorCodeGenerator）*
    - *MvcVBRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
- **當 WebData 包含在 ASP.NET MVC 4 應用程式的/bin 目錄中時，它會接管用於表單驗證的 URL。** 將 WebData 新增至您的應用程式（例如，在使用 [新增可部署的相依性] 對話方塊時，選取 [使用 Razor 語法 ASP.NET Web Pages]）將會覆寫驗證登入重新導向至/account/logon，而非預設 ASP.NET MVC 帳戶控制器所預期的/account/login。 若要避免此行為，並使用已在 web.config 的驗證區段中指定的 URL，您可以新增名為 PreserveLoginUrl 的 appSetting，並將它設定為 true： 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **嘗試安裝 ASP.NET MVC 4 以進行 Visual Studio 2010 和 Visual Web Developer 2010 的並存安裝時，NuGet 套件管理員無法安裝。** 若要與 ASP.NET MVC 4 並存執行 Visual Studio 2010 和 Visual Web Developer 2010，您必須在兩個版本的 Visual Studio 都已安裝之後，安裝 ASP.NET MVC 4。
- **如果已卸載必要條件，卸載 ASP.NET MVC 4 會失敗。** 若要完全卸載 ASP.NET MVC 4you，必須先卸載 ASP.NET MVC 4，然後再卸載 Visual Studio。
- **安裝 ASP.NET MVC 4 會中斷 ASP.NET MVC 3 RTM 應用程式。** ASP.NET 使用 RTM 版本建立的 MVC 3 應用程式（不含[ASP.NET MVC 3 工具更新](https://www.microsoft.com/download/details.aspx?id=1491)版本）需要進行下列變更，才能與 ASP.NET MVC 4 並存工作。 建立專案而不進行這些更新，會導致編譯錯誤。 

    **必要的更新**

  1. 在根 web.config 檔案中，加入新的 *&lt;appSettings&gt;* 專案，其中包含主要*網頁： Version*和值*1.0.0.0*。 

      [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
  2. 在方案總管中，以滑鼠右鍵按一下專案名稱，然後選取 [卸載專案]。 然後再次以滑鼠右鍵按一下名稱，然後選取 [編輯*專案*名稱 .csproj]。
  3. 找出下列元件參考： 

      [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

      將其取代為下列內容：

      [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
  4. 儲存變更，關閉您正在編輯的專案（.csproj）檔案，然後以滑鼠右鍵按一下專案，然後選取 [重載]。

- 將**ASP.NET MVC 4 專案從4.5 變更為目標4.0，並不會更新 EntityFramework 元件參考：** 如果您在瞄準4.5 之後將 ASP.NET MVC 4 專案變更為目標4.0，則 EntityFramework 元件的參考仍然會指向4.5 版本。 若要修正此問題，請卸載並重新安裝 EntityFramework NuGet 套件。
- **403 在從4.5 變更為目標4.0 之後，于 Azure 上執行 ASP.NET MVC 4 應用程式時禁止：** 如果您在瞄準4.5 之後將 ASP.NET MVC 4 專案變更為目標4.0，然後再部署至 Azure，您可能會在執行時間看到「403禁止」錯誤。 若要解決此問題，請將下列內容新增至您的 web.config： `<modules runAllManagedModulesForAllRequests="true" />`
- **當您在 Razor 檔案中的字串常值中輸入 '\' 時，Visual Studio 2012 當機。** 若要解決此問題，請先輸入字串常值的右引號。
- <strong>流覽至 &quot;帳戶/管理網際網路範本&quot;，會導致 CHS、修訂及 CHT 語言的執行階段錯誤。</strong> 若要修正此問題，請修改頁面，將其設為<em>&lt;強式&gt;</em>標記內唯一的內容，以分隔<em>@User.Identity.Name</em> 。
- **Azure 網站中不支援 Google 和 LinkedIn 提供者。** 部署至 Azure 網站時，請使用替代的驗證提供者。
- **當您使用 UriPathExtensionMapping 搭配 IIS 8 Express/IIS 時，當您嘗試使用此延伸模組時，可能會收到404找不到的錯誤。** 靜態檔案處理常式會干擾使用*UriPathExtensionMappings*之 web api 的要求。 在 web.config 中設定*runAllManagedModulesForAllRequests = true*以解決此問題。
- **不會再呼叫 Controller。執行方法。** 所有 MVC 控制器現在一律會以非同步方式執行。
