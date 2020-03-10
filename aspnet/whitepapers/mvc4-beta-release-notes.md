---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 |Microsoft Docs
author: rick-anderson
description: 本檔說明適用于 Visual Studio 2010 的 ASP.NET MVC 4 Beta 發行版本。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523300"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> 本檔說明適用于 Visual Studio 2010 的 ASP.NET MVC 4 Beta 發行版本。
> 
> > [!NOTE]
> > 這不是最新版本。 您可以在[這裡](mvc4-release-notes.md)取得 ASP.NET MVC 4 RC 版本資訊。

- [安裝注意事項](#_Toc303253802)
- [文件](#_Toc303253803)
- [支援](#_Toc303253804)
- [軟體需求](#_Toc303253805)
- [將 ASP.NET MVC 3 專案升級至 ASP.NET MVC 4](#_Toc303253806)
- [ASP.NET MVC 4 Beta 的新功能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [ASP.NET 單一頁面應用程式](#_Toc317096198)
    - [預設專案範本的增強功能](#_Toc303253808)
    - [行動專案範本](#_Toc303253809)
    - [顯示模式](#_Toc303253810)
    - [jQuery Mobile、視圖切換器和瀏覽器覆寫](#_Toc303253811)
    - [Visual Studio 中產生程式碼的配方](#_Toc303253812)
    - [非同步控制器的工作支援](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [已知問題和重大變更](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>安裝注意事項

您可以使用 Web Platform Installer，從 [ [ASP.NET MVC 4](../mvc/mvc4.md) ] 首頁安裝適用于 Visual Studio 2010 的 ASP.NET Mvc 4 Beta。

在安裝 ASP.NET MVC 4 Beta 之前，您必須先卸載任何先前安裝的 ASP.NET MVC 4 預覽。

此版本與 .NET Framework 4.5 開發人員預覽版不相容。 您必須先卸載 .NET 4.5 開發人員預覽版，才能安裝 ASP.NET MVC 4 Beta 版。

ASP.NET MVC 4 可以安裝，而且可以與 ASP.NET MVC 3 並存執行。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>文件

ASP.NET MVC 文件位於 MSDN 網站上，其 URL 如下所示：

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

如需有關 ASP.NET MVC 的教學課程和其他資訊，請在 ASP.NET 網站的 MVC 4 頁面（[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)）中找到。

<a id="_Toc303253804"></a>
## <a name="support"></a>支援

這是預覽版本，並未正式支援。 如果您有關于使用此版本的問題，請將其張貼至 ASP.NET MVC 論壇（[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)），其中 ASP.NET 社區的成員經常能夠提供非正式的支援。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>軟體需求

Visual Studio 的 ASP.NET MVC 4 元件需要 PowerShell 2.0，以及 Visual Studio 2010 Service Pack 1 或 Visual Web Developer Express 2010 （含 Service Pack 1）。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>將 ASP.NET MVC 3 專案升級至 ASP.NET MVC 4

ASP.NET MVC 4 可以與 ASP.NET MVC 3 並存安裝在同一部電腦上，讓您有彈性選擇何時將 ASP.NET MVC 3 應用程式升級為 ASP.NET MVC 4。

最簡單的升級方式是建立新的 ASP.NET MVC 4 專案，並將所有的視圖、控制器、程式碼和內容檔案從現有的 MVC 3 專案複製到新的專案，然後更新新專案中的元件參考，以符合舊的專案。 如果您已變更 MVC 3 專案中的 web.config 檔案，則也必須將這些變更合併到 MVC 4 專案的 web.config 檔案中。

若要將現有的 ASP.NET MVC 3 應用程式手動升級為第4版，請執行下列動作：

1. 在專案的所有 web.config 檔案中（專案的根目錄中有一個，一個在 Views 資料夾，另一個位於專案中每個區域的 Views 資料夾中），取代下列文字的每個實例：

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    具有下列對應的文字：

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. 在根 web.config 檔案中，將*網頁： Version*專案更新為 "2.0.0.0"，並加入值為 "true" 的新*PreserveLoginUrl*機碼：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. 在方案總管中，刪除*system.web*的參考（指向第3版的 DLL）。 然後加入*system.web*的參考（v 4.0.0.0）。 特別是，請進行下列變更，以更新元件參考。 詳細資料如下：

    1. 在方案總管中，刪除下列元件的參考： 

        - *System.web. Mvc*（v 3.0.0.0）
        - *System.web*（1.0.0.0 版）
        - *System.web*（1.0.0.0 版）
        - System.web. *Deployment*（1.0.0.0 版）
        - System.web。 *Razor*（1.0.0.0 版）
    2. 新增下列元件的參考： 

        - *System.web. Mvc*（v 4.0.0.0）
        - *System.web*（v 2.0.0.0）
        - *System.web*（v 2.0.0.0）
        - System.web. *Deployment*（v 2.0.0.0）
        - System.web. *Razor*（v 2.0.0.0）
4. 在方案總管中，以滑鼠右鍵按一下專案名稱，然後選取 [卸載專案]。 然後再次以滑鼠右鍵按一下名稱，然後選取 [編輯*專案*名稱 .csproj]。
5. 找出*ProjectTypeGuids*元素，並將 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 取代為 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。
6. 儲存變更，關閉您編輯的專案（.csproj）檔案，以滑鼠右鍵按一下專案，然後選取 [重載專案]。
7. 如果專案參考使用舊版 ASP.NET MVC 編譯的任何協力廠商程式庫，請開啟根 web.config 檔案，然後*在 [設定*] 區段下新增下列三個*bindingRedirect*元素： 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a>ASP.NET MVC 4 Beta 的新功能

本節說明 ASP.NET MVC 4 Beta 版本中引進的功能。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 現在包含 ASP.NET Web API，這是建立 HTTP 服務的新架構，可以連接到各種用戶端，包括瀏覽器和行動裝置。 ASP.NET Web API 也是建立 RESTful 服務的理想平臺。

ASP.NET Web API 包含下列功能的支援：

- **新式 HTTP 程式設計模型：** 使用新的強型別 HTTP 物件模型，直接存取和操作 Web Api 中的 HTTP 要求和回應。 相同的程式設計模型和 HTTP 管線會透過新的 HttpClient 類型在用戶端上對稱使用。
- **完整的路由支援**： web api 現在支援一組完整的路由功能，一律是 web 堆疊的一部分，包括路由參數和條件約束。 此外，對動作的對應具有對慣例的完整支援，因此您不再需要將屬性（例如 [HttpPost]）套用至您的類別和方法。
- **內容協商**：用戶端和伺服器可以一起使用，以判斷從 API 傳回之資料的正確格式。 我們提供 XML、JSON 和表單 URL 編碼格式的預設支援，您可以新增自己的格式器來擴充這項支援，或甚至取代預設的內容協商策略。
- **模型系結和驗證：** 模型系結器提供簡單的方法，可從 HTTP 要求的各個部分解壓縮資料，並將這些訊息部分轉換成可供 Web API 動作使用的 .NET 物件。
- **篩選器：** Web Api 現在支援篩選準則，包括知名的篩選準則，例如 [授權] 屬性。 您可以撰寫並插入您自己的篩選準則，以進行動作、授權和例外狀況處理。
- **查詢撰寫：** 藉由只傳回 IQueryable&lt;T&gt;，您的 Web API 將支援透過 OData URL 慣例進行查詢。
- 已**改善 HTTP 詳細資料的可測試性：** Web API 動作現在可以與 HttpRequestMessage 和 HttpResponseMessage 的實例搭配使用，而不是在靜態內容物件中設定 HTTP 詳細資料。 這些物件的泛型版本也存在，讓您除了 HTTP 類型之外，還可以使用您的自訂類型。
- **改善的控制反轉（IoC） Via DependencyResolver：** Web API 現在會使用 MVC 的相依性解析程式所執行的服務定位器模式，來取得許多不同設施的實例。
- 以**程式碼為基礎的設定：** Web API 設定只會透過程式碼完成，讓您的設定檔保持乾淨。
- **自我裝載：** Web Api 除了 IIS 之外，也可以裝載于您自己的進程中，同時仍然使用路由的完整功能和 Web API 的其他功能。

如需 ASP.NET Web API 的詳細資訊，請流覽[https://www.asp.net/web-api](../web-api/index.md)。

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a>ASP.NET 單一頁面應用程式

ASP.NET MVC 4 現在提供了使用 JavaScript 和 Web Api 來建立單一頁面應用程式的體驗，並具有大量用戶端互動的早期預覽。 這種支援包括：

- 一組 JavaScript 程式庫，可與快取的資料進行更豐富的本機互動
- 適用于工作單位和 DAL 支援的其他 Web API 元件
- 具有可快速開始使用之樣板的 MVC 專案範本

如需 ASP.NET MVC 4 中單一頁面應用程式支援的詳細資訊，請造訪[https://www.asp.net/single-page-application](../single-page-application/index.md)。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>預設專案範本的增強功能

用來建立新 ASP.NET MVC 4 專案的範本已更新，以建立更現代化的網站：

![](mvc4-beta-release-notes/_static/image1.png)

除了表面改良以外，新的範本中還有改進的功能。 此範本採用一種稱為適應性轉譯的技術，在桌面瀏覽器和行動瀏覽器中都不需要任何自訂。

![](mvc4-beta-release-notes/_static/image2.png)

若要查看作用中的調適型轉譯，您可以使用行動模擬器，或只嘗試調整桌面瀏覽器視窗的大小。 當瀏覽器視窗夠小時，頁面的版面配置就會變更。

預設專案範本的另一個增強功能是使用 JavaScript 來提供更豐富的 UI。 範本中使用的登入和註冊連結，是如何使用 jQuery UI 對話方塊來呈現豐富的登入畫面的範例：

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>行動專案範本

如果您要開始新的專案，並想要特別針對行動和平板電腦瀏覽器建立網站，則可以使用 [新增行動應用程式] 專案範本。 這是以 jQuery Mobile 為基礎，這是一個開放原始碼程式庫，可用於建立觸控優化的 UI：

![](mvc4-beta-release-notes/_static/image4.png)

此範本包含與網際網路應用程式範本相同的應用程式結構（而且控制器程式碼幾乎完全相同），但它是使用 jQuery Mobile 樣式化，在觸控式行動裝置上外觀良好並表現良好。 若要深入瞭解如何結構和樣式行動 UI，請參閱[JQuery mobile 專案網站](http://jquerymobile.com/)。

如果您已經有想要新增行動優化視圖的桌面導向網站，或者您想要建立單一網站來提供不同的樣式視圖給桌上型電腦和行動瀏覽器，您可以使用新的顯示模式功能。 (請參閱下節)。

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>顯示模式

新的顯示模式功能可讓應用程式根據提出要求的瀏覽器選取 views。 例如，如果桌面瀏覽器要求首頁，應用程式可能會使用 Views\Home\Index.cshtml 範本。 如果行動瀏覽器要求首頁，應用程式可能會傳回 Views\Home\Index.mobile.cshtml 範本。

您也可以針對特定瀏覽器類型覆寫版面配置和部分。 例如:

- 如果您的 [Views\Shared] 資料夾同時包含 [\_配置] 和 [\_配置]，則應用程式預設會在行動瀏覽器的要求期間使用 \_的配置，而在其他要求期間則會 \_配置. cshtml。
- 如果資料夾同時包含 \_MyPartial 和 \_MyPartial，則指令 @Html.Partial（"\_MyPartial"）會在行動瀏覽器的要求期間轉譯 \_MyPartial，並在其他要求期間 \_MyPartial. cshtml。

如果您想要為其他裝置建立更特定的視圖、配置或部分視圖，您可以註冊新的*DefaultDisplayMode*實例，以指定當要求符合特定條件時要搜尋的名稱。 例如，您可以將下列程式碼新增至 global.asax 檔案中的*應用程式\_Start*方法，將字串 "iPhone" 註冊為當 Apple iPhone 瀏覽器提出要求時適用的顯示模式：

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

在此程式碼執行之後，當 Apple iPhone 瀏覽器提出要求時，您的應用程式將會使用 Views\Shared\\_Layout iPhone. cshtml 配置（如果有的話）。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a>jQuery Mobile、視圖切換器和瀏覽器覆寫

jQuery Mobile 是一種開放原始碼程式庫，可用於建立觸控式優化的 web UI。 如果您想要搭配使用 jQuery Mobile 與 ASP.NET MVC 4 應用程式，您可以下載並安裝 NuGet 套件，以協助您開始著手。 若要從 Visual Studio 套件管理員主控台安裝它，請輸入下列命令：

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

這會安裝 jQuery Mobile 和一些 helper 檔案，包括下列各項：

- Views/Shared/\_Layout，這是 jQuery Mobile 型版面配置。
- View-切換器元件，其中包含 Views/Shared/\_ViewSwitcher 部分視圖和 ViewSwitcherController.cs 控制器。

安裝套件之後，請使用行動瀏覽器執行應用程式（或對等的，如同 Firefox[使用者代理程式切換](http://chrispederick.com/work/user-agent-switcher/)器附加元件）。 您會看到頁面看起來相當不同，因為 jQuery Mobile 會處理版面配置和樣式設定。 若要利用這一點，您可以執行下列動作：

- 依照稍早的[顯示模式](#_Toc303253810)（例如，建立 Views\Home\Index.mobile.cshtml 來覆寫行動瀏覽器的 Views\Home\Index.cshtml）中所述，建立特定的行動裝置視圖。
- 閱讀[JQuery mobile 檔](http://jquerymobile.com/)，以深入瞭解如何在行動裝置視圖中新增觸控優化的 UI 元素。

行動優化網頁的慣例是加入一個連結，其文字類似于桌面視圖或完整網站模式，可讓使用者切換至桌上出版本的頁面。 JQuery 封裝包含用於此用途的範例視圖-切換器元件。 它會在預設的 Views\Shared\\_Layout 中使用，在轉譯頁面時看起來會像這樣：

![](mvc4-beta-release-notes/_static/image5.png)

如果訪客按一下連結，就會切換到相同頁面的桌上出版本。

因為您的桌上出版面配置預設不會包含視圖切換器，所以訪客不會有辦法進入行動模式。 若要啟用這項操作，請將下列參考新增至您的桌上出版面配置 *\_ViewSwitcher* ，只在 *&lt;body&gt;* 元素內：

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

「視圖切換器」會使用稱為「瀏覽器覆寫」的新功能。 這項功能可讓您的應用程式將要求視為來自不同的瀏覽器（使用者代理程式），而不是實際來源。 下表列出瀏覽器覆寫所提供的方法。

| `HttpContext.SetOverriddenBrowser(userAgentString)` | 使用指定的使用者代理程式，覆寫要求的實際使用者代理程式值。 |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | 傳回要求的使用者代理程式覆寫值，或如果未指定任何覆寫，則為實際的使用者代理字串。 |
| `HttpContext.GetOverriddenBrowser()` | 傳回*HttpBrowserCapabilitiesBase*實例，其對應至目前針對要求所設定的使用者代理程式（實際或已覆寫）。 您可以使用這個值來取得*IsMobileDevice*之類的屬性。 |
| `HttpContext.ClearOverriddenBrowser()` | 移除目前要求之任何已覆寫的使用者代理程式。 |

瀏覽器覆寫是 ASP.NET MVC 4 的核心功能，即使您未安裝 jQuery. node.js 封裝也可以使用。 不過，它只會影響 [視圖]、[版面配置] 和 [局部視圖] 選取專案，而不會影響相依于*要求瀏覽器*物件的任何其他 ASP.NET 功能。

根據預設，會使用 cookie 來儲存使用者代理程式覆寫。 如果您想要將覆寫儲存在其他位置（例如，在資料庫中），您可以取代預設提供者（*BrowserOverrideStores*）。 此提供者的檔將提供給較新版本的 ASP.NET MVC。

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a>Visual Studio 中產生程式碼的配方

新的配方功能可讓 Visual Studio 根據您可以使用 NuGet 安裝的套件，產生解決方案特定的程式碼。 配方架構可讓開發人員輕鬆地撰寫程式碼產生外掛程式，您也可以用它來取代內建的程式碼產生器，以加入區域、新增控制器和加入視圖。 由於配方會部署為 NuGet 套件，因此可以輕鬆地簽入原始檔控制，並自動與專案上的所有開發人員共用。 它們也是以每個解決方案為基礎提供。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>非同步控制器的工作支援

您現在可以將非同步動作方法撰寫為單一方法，以傳回*task*或 task 類型的物件 *&lt;ActionResult&gt;* 。

例如，如果您使用的是 Visual C# 5 （或使用[非同步 CTP](https://msdn.microsoft.com/vstudio/async.aspx)），您可以建立如下所示的非同步動作方法：

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

在上一個動作方法中，會以非同步方式呼叫*NewsService GetHeadlinesAsync*和*sportsService* ，而且不會封鎖執行緒集區中的執行緒。

傳回*工作實例的*非同步動作方法也可以支援超時。 若要讓動作方法可取消，請將*CancellationToken*類型的參數新增至動作方法簽章。 下列範例顯示的非同步動作方法，其超時時間為2500毫秒，且在發生超時時，會向用戶端顯示*TimedOut*的視圖。

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 Beta 版支援2011年9月1.5 版的 Windows Azure SDK。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

- **安裝 ASP.NET MVC 4 Beta 之後，在 cshtml 或 vbhtml 檔案內輸入程式碼片段或 JavaScript 後，Visual Studio 2010 Service Pack 1 CSHTML/VBHTML 編輯器中的 CSHTML/VBHTML 編輯器可能會暫停一段長時間。** 這只會發生在剛建立但尚未編譯的 ASP.NET MVC 4 應用程式中。

    解決方法是編譯專案，以取得 bin 資料夾中的元件。 請注意，如果您清除的專案會從 bin 資料夾中移除元件，則會傳回編輯器問題。

    這將在下一版中更正。
- **C#Visual Studio 11 Beta 的專案範本在 Global.asax.cs 中包含不正確的連接字串。** 在 Visual Studio 11 Beta 版中建立之專案的應用程式\_Start 方法中指定的預設連接包含 LocalDB 連接字串，其中包含非轉義的反斜線（\) 字元。 這會導致嘗試存取 Entity Framework DbCoNtext 時發生連接錯誤，這會產生 SqlException。

    若要更正此問題，請將應用程式中的反斜線字元\_Start Global.asax.cs 方法中，使其如下所示：

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- **在 .NET 4.0 底下執行時，以 .NET 4.5 為目標的 MVC 4 應用程式會在嘗試存取 Http.sys 元件時擲回 FileLoadException。** ASP.NET 在 .NET 4.5 底下建立的 MVC 4 應用程式包含系結重新導向，會導致 FileLoadException 指出「無法載入檔案或元件 ' System .Net. Http ' 或它的其中一個相依性」。 當應用程式在已安裝 .NET 4.0 的系統上執行時。 若要更正此問題，請從 web.config 移除下列系結重新導向：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    已修改之 web.config 中的元件繫結項目應如下所示：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- 在<strong>區域內叫用</strong><strong>時，Visual Basic 專案中的「新增控制器」專案範本會產生不正確的命名空間</strong>。 當您將控制器加入至使用 Visual Basic 之 ASP.NET MVC 專案中的區域時，專案範本會將錯誤的命名空間插入控制器中。 當您流覽至控制器中的任何動作時，結果會是「找不到檔案」錯誤。  
  
  產生的命名空間會省略根命名空間之後的所有內容。 例如，所產生的命名空間是*RootNamespace* ，但應該是*RootNamespace. AreaName. 控制器*。
- **Razor View 引擎中的重大變更。** 在重寫 Razor 剖析器的過程中，下列類型已從*system.web*移除： 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  下列方法也已移除： 

    - *MvcCSharpRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
    - *MvcWebPageRazorHost. DecorateCodeGenerator （System.web. RazorCodeGenerator）*
    - *MvcVBRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
- **當 WebData 包含在 ASP.NET MVC 4 應用程式的/bin 目錄中時，它會接管用於表單驗證的 URL。** 將 WebData 新增至您的應用程式（例如，在使用 [新增可部署的相依性] 對話方塊時，選取 [使用 Razor 語法 ASP.NET Web Pages]）將會覆寫驗證登入重新導向至/account/logon，而非預設 ASP.NET MVC 帳戶控制器所預期的/account/login。 若要避免此行為，並使用已在 web.config 的驗證區段中指定的 URL，您可以新增名為 PreserveLoginUrl 的 appSetting，並將它設定為 true： 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- **嘗試安裝 ASP.NET MVC 4 以進行 Visual Studio 2010 和 Visual Web Developer 2010 的並存安裝時，NuGet 套件管理員無法安裝。** 若要與 ASP.NET MVC 4 並存執行 Visual Studio 2010 和 Visual Web Developer 2010，您必須在兩個版本的 Visual Studio 都已安裝之後，安裝 ASP.NET MVC 4。
- **如果已卸載必要條件，卸載 ASP.NET MVC 4 會失敗。** 若要完全卸載 ASP.NET MVC 4you，必須先卸載 ASP.NET MVC 4，然後再卸載 Visual Studio。
- **執行預設的 Web API 專案會顯示不正確地指示使用者使用 RegisterApis 方法（不存在）來新增路由的指示。** 您應該使用 ASP.NET 路由表，在 RegisterRoutes 方法中新增路由。
- **安裝 ASP.NET MVC 4 Beta 中斷 ASP.NET MVC 3 RTM 應用程式。** ASP.NET 使用 RTM 版本建立的 MVC 3 應用程式（不含 ASP.NET MVC 3 工具更新版本）需要進行下列變更，才能與 ASP.NET MVC 4 Beta 並存使用。 建立專案而不進行這些更新，會導致編譯錯誤。 

    **必要的更新**

  1. 在根 web.config 檔案中，加入新的 *&lt;appSettings&gt;* 專案，其中包含主要*網頁： Version*和值*1.0.0.0*。

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. 在方案總管中，以滑鼠右鍵按一下專案名稱，然後選取 [卸載專案]。 然後再次以滑鼠右鍵按一下名稱，然後選取 [編輯*專案*名稱 .csproj]。
  3. 找出下列元件參考： 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      將其取代為下列內容：

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. 儲存變更，關閉您正在編輯的專案（.csproj）檔案，然後以滑鼠右鍵按一下專案，然後選取 [重載]。
