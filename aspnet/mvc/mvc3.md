---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: （包含4月2011工具更新）ASP.NET MVC 3 是一種架構，可讓您使用已妥善建立的設計模式來建立可擴充的標準 web 應用程式 。
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 421a06c89d4dbcb05d4080033813cc6558b7c698
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616407"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *（包含4月2011工具更新）*
> 
> ASP.NET MVC 3 是一種架構，可讓您使用妥善建立的設計模式以及 ASP.NET 和 .NET Framework 的強大功能，來建立可擴充且以標準為基礎的 web 應用程式。
> 
> 它會與 ASP.NET MVC 2 並存安裝，因此現在就開始使用它！
> 
> 在[這裡下載安裝程式](https://go.microsoft.com/fwlink/?LinkID=208140)

## <a name="top-features"></a>熱門功能

- 透過 NuGet 擴充的整合式架構系統
- 啟用 HTML 5 的專案範本
- 表達性視圖，包括新的 Razor View Engine
- 具有相依性插入和全域動作篩選器的強大勾點
- 具有不顯眼的 JavaScript、jQuery 驗證和 JSON 系結的豐富 JavaScript 支援
- *閱讀[下列](#overview)完整的功能清單*

## <a name="top-links"></a>熱門連結

ASP.NET MVC 3 的新功能

- Phil Haack： [ASP.NET MVC 3 已發行](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman： [ASP.NET MVC3、WebMatrix、NuGet、IIS Express 和 Orchard 發行-Microsoft 一月 Web 版本的內容](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie：[宣佈發行 ASP.NET MVC 3、IIS Express、SQL CE 4、Web Farm Framework、Orchard、WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3 的版本資訊](../whitepapers/mvc3-release-notes.md)

安裝與協助

- 使用 Web Platform Installer 安裝 ASP.NET MVC 3 [（建議選項）](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- 使用安裝[程式可執行檔](https://go.microsoft.com/fwlink/?LinkID=208140)安裝 ASP.NET MVC 3
- 安裝[適用于 Visual Studio 11 開發人員預覽的 ASP.NET MVC 3](https://go.microsoft.com/fwlink/?LinkID=208140)
- 閱讀[ASP.NET MVC 3 簡介教學](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)課程
- 取得協助並討論[論壇](https://forums.asp.net/1146.aspx)中的 ASP.NET MVC 3

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 概觀 (英文)

ASP.NET MVC 3 建置於 ASP.NET MVC 1 和2，加入了可簡化程式碼並允許更深入擴充性的絕佳功能。 本主題概述此版本中包含的許多新功能，並組織成下列各節：

- [具有 MvcScaffold 整合的可擴充式架構](#BM_MvcScaffolding)
- [啟用 HTML 5 的專案範本](#BM_HTML5)
- [Razor View 引擎](#BM_TheRazorViewEngine)
- [支援多個視圖引擎](#BM_Support_for_Multiple_View_Engines)
- [控制器改善](#BM_Controller_Improvements)
- [JavaScript 和 Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [模型驗證改善](#BM_Model_Validation_Improvements)
- [相依性插入改良功能](#BM_Dependency_Injection_Improvements)
- [其他新功能](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>具有 MvcScaffold 整合的可擴充式架構

新的架構系統可讓您更輕鬆地開始使用，並在您剛體驗到 framework 時，將常見的開發工作自動化，並已瞭解您所執行的作業。

這受到名為**MvcScaffolding**的*新 NuGet 架構*套件支援。 許多軟體技術都使用「架構」一詞來表示「快速產生軟體的基本大綱，讓您可以編輯和自訂」。 我們為 ASP.NET MVC 所建立的樣板套件，在數個案例中有很大的好處：

- **如果您是第一次學習 ASP.NET MVC**，因為它可讓您快速取得一些有用的工作程式碼，因此您可以根據自己的需求進行編輯和調整。 它可以讓您從 trauma 查看空白頁面，而不知道要從何處著手！
- **如果您知道 ASP.NET MVC，而且現在正在探索一些新的附加元件技術**，例如物件關聯式對應程式、視圖引擎、測試程式庫等，這項技術的建立者也可能會為其建立一個元件套件。
- **如果您的工作牽涉到重複建立類似的類別或**檔案，這是因為您可以建立自訂鷹架已經，以輸出測試裝置、部署腳本，或任何您所需的其他類型。 小組中的每個人都可以使用您的自訂鷹架已經。

MvcScaffolding 中的其他功能包括：

- 和 VB C#專案的支援
- Razor 和 ASPX 視圖引擎的支援
- 支援將樣板 ASP.NET MVC 區域，以及使用自訂視圖配置/主版
- 您可以藉由編輯 T4 範本，輕鬆地自訂輸出
- 您可以使用自訂的 PowerShell 邏輯和自訂 T4 範本來新增全新的鷹架已經。 這些（和您指定的任何自訂參數）會自動顯示在主控台索引標籤-完成清單中。
- 您可以針對不同的技術取得包含其他鷹架已經的 NuGet 套件（例如，目前 LINQ to SQL 的概念證明），並將它們混合在一起

ASP.NET MVC 3 工具更新包含此架構系統的絕佳 Visual Studio 支援，例如：

- [新增控制器] 對話方塊現在支援 [建立]、[讀取]、[更新] 和 [刪除控制器動作] 和對應視圖的完整自動架構。 根據預設，這會使用 EF Code First scaffold 資料存取程式碼。
- [新增控制器] 對話方塊透過 NuGet 套件（例如*MvcScaffolding*）支援*可擴充的 scaffold* 。 這可讓您將自訂 scaffold 插入對話方塊中，這可讓您針對其他資料存取技術（例如 NHibernate，甚至是使用 ODBCDirect 的 JET）建立 scaffold （如果您這麼做）。

如需 ASP.NET MVC 3 中之樣板的詳細資訊，請參閱下列資源：

- Steve Sanderson 的文章系列，包括： 

    1. [簡介：使用 MvcScaffolding 套件 Scaffold 您的 ASP.NET MVC 3 專案](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [標準使用方式：一般使用案例和選項](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [一對多關聯性](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [樣板動作和單元測試](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [覆寫 T4 範本](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [這篇文章：建立自訂鷹架已經](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Scott Hanselman 在他的 PDC 2010 研討會發表[了 Microsoft 「未命名的 Web 愛套件](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)」的 Blog
- [MVC 3 版本資訊](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 專案範本

[新增專案] 對話方塊包含 [啟用 HTML 5 版本的專案範本] 核取方塊。 這些範本會利用 Modernizr 1.7，為舊版瀏覽器中的 HTML 5 和 CSS 3 提供相容性支援。

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Razor View 引擎

ASP.NET MVC 3 隨附名為 Razor 的新 view engine，可提供下列優點：

- Razor 語法很簡潔，而且需要最少的擊鍵數。
- Razor 很容易學習，部分是因為它是以現有的語言（如C#和 Visual Basic）為基礎。
- Visual Studio 包含 Razor 語法的 IntelliSense 和程式碼顏色標示。
- Razor views 可以進行單元測試，而不需要您執行應用程式或啟動 web 伺服器。

一些新的 Razor 功能包括下列各項：

- `@model` 語法，用於指定要傳遞至視圖的類型。
- `@* *@` 批註語法。
- 為整個網站指定預設值（例如 `layoutpage`）的能力。
- 在不進行 HTML 編碼的情況下顯示文字的 `Html.Raw` 方法。
- 支援在多個視圖之間共用程式碼（ *\_viewstart*或 *\_viewstart vbhtml*檔案）。

Razor 也包含新的 HTML 協助程式，如下所示：

- `Chart` 呈現圖表，其提供的功能與 ASP.NET 4 中的 chart 控制項相同。
- `WebGrid` 使用分頁和排序功能來呈現資料方格。
- `Crypto` 會使用雜湊演算法來建立適當的 salted 和雜湊密碼。
- `WebImage` 呈現影像。
- `WebMail` 傳送電子郵件訊息。

如需 Razor 的詳細資訊，請參閱下列資源：

- [Scott Guthrie 的文章 Razor 簡介](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Scott Guthrie 的文章，介紹 @model 關鍵字](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Scott Guthrie 的文章 Razor 版面配置簡介](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API 快速參考](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 版本資訊](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>支援多個視圖引擎

ASP.NET MVC 3 中的 [**加入視圖**] 對話方塊可讓您選擇要使用的視圖引擎，而 [**新增專案**] 對話方塊可讓您指定專案的預設視圖引擎。 您可以選擇 [Web form view engine （ASPX）]、[Razor] 或開放原始碼視圖引擎（例如[Spark](http://sparkviewengine.com/)、 [NHaml](https://code.google.com/p/nhaml/)或[NDjango](http://ndjango.org/)）。

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>控制器改善

### <a name="global-action-filters"></a>全域動作篩選

有時候，您可能會想要在動作方法執行之前或動作方法執行之後執行邏輯。 若要支援這種情況，請 ASP.NET MVC 2 提供的動作篩選準則。 動作篩選器是自訂屬性，可提供宣告式方式，將動作前和動作後的行為新增至特定的控制器動作方法。 不過，在某些情況下，您可能會想要指定套用至所有動作方法的前置動作或動作後行為。 MVC 3 可讓您藉由將全域篩選新增至 `GlobalFilters` 集合來指定它們。 如需全域動作篩選器的詳細資訊，請參閱下列資源：

- [在 MVC 3 Preview 上 Scott Guthrie 的 blog](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC 中的篩選](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>新的 "ViewBag" 屬性

MVC 2 控制器支援 `ViewData` 屬性，可讓您使用晚期繫結字典 API 將資料傳遞至視圖範本。 在 MVC 3 中，您也可以搭配 `ViewBag` 屬性使用稍微簡單的語法，以達成相同的目的。 例如，您可以撰寫 `ViewBag.Message="text"`，而不是撰寫 `ViewData["Message"]="text"`。 您不需要定義任何強型別類別，就可以使用 `ViewBag` 屬性。 因為它是動態屬性，所以您可以改為取得或設定屬性，而且它會在執行時間動態加以解析。 就內部而言，`ViewBag` 屬性會以名稱/值組的形式儲存在 `ViewData` 字典中。 （注意：在 MVC 3 的大部分發行前版本中，`ViewBag` 屬性都是命名為 `ViewModel` 屬性）。

### <a name="new-actionresult-types"></a>新的 "ActionResult" 類型

下列 `ActionResult` 類型和對應的 helper 方法是 MVC 3 中的新功能或增強功能：

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。 將 404 HTTP 狀態碼傳回到用戶端。
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。 根據布林值參數傳回暫時重新導向（HTTP 302 狀態碼）或永久重新導向（HTTP 301 狀態碼）。 結合這項變更，[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)類別現在有三種方法可執行永久重新導向： `RedirectPermanent`、`RedirectToRoutePermanent`和 `RedirectToActionPermanent`。 這些方法會傳回 `RedirectResult` 的實例，並將 `Permanent` 屬性設定為 `true`。
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。 傳回使用者指定的 HTTP 狀態碼。

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript 和 Ajax 的改良功能

根據預設，MVC 3 中的 Ajax 和驗證協助程式會使用不顯眼的 JavaScript 方法。 不顯眼的 JavaScript 可避免將內嵌的 JavaScript 插入 HTML。 這可讓您的 HTML 變得更小且更不雜亂，並可讓您更輕鬆地交換或自訂 JavaScript 程式庫。 MVC 3 中的驗證協助程式預設也會使用 `jQueryValidate` 外掛程式。 如果您想要 MVC 2 行為，可以*使用 web.config 檔案*設定來停用不顯眼的 JavaScript。 如需 JavaScript 和 Ajax 改良功能的詳細資訊，請參閱下列資源：

- [維琪百科網站上不顯眼 JavaScript 的基本簡介](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson 的不顯眼 JavaScript 貼文](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson 的不顯眼 JavaScript 驗證貼文](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [使用 Razor 和不顯眼的 JavaScript 建立 MVC 3 應用程式](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET 網站上的教學課程）
- [MVC 3 版本資訊](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>預設會啟用用戶端驗證

在舊版 MVC 中，您必須從視圖明確呼叫 `Html.EnableClientValidation` 方法，才能啟用用戶端驗證。 在 MVC 3 中，因為預設會啟用用戶端驗證，所以不再需要這項功能。 （您可以*使用 web.config 檔案*中的設定來停用此功能）。

為了讓用戶端驗證能夠正常執行，您仍然需要在您的網站中參考適當的 jQuery 和 jQuery 驗證程式庫。 您可以在自己的伺服器上裝載這些程式庫，或從 Microsoft 或 Google 的 Cdn 之類的內容傳遞網路（CDN）加以參考。

### <a name="remote-validator"></a>遠端驗證程式

ASP.NET MVC 3 支援新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)類別，可讓您利用 jQuery 驗證外掛程式的遠端驗證程式支援。 這可讓用戶端驗證程式庫自動呼叫您在伺服器上定義的自訂方法，以便執行只能在伺服器端完成的驗證邏輯。

在下列範例中，`Remote` 屬性會指定用戶端驗證將會在 `UsersController` 類別上呼叫名為 `UserNameAvailable` 的動作，以便驗證 `UserName` 欄位。

[!code-csharp[Main](mvc3/samples/sample1.cs)]

下列範例會顯示對應的控制器。

[!code-csharp[Main](mvc3/samples/sample2.cs)]

如需如何使用 `Remote` 屬性的詳細資訊，請參閱 MSDN library 中的 how [to：在 ASP.NET MVC 中執行遠端驗證](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。

### <a name="json-binding-support"></a>JSON 系結支援

ASP.NET MVC 3 包含內建的 JSON 系結支援，可讓動作方法接收 JSON 編碼的資料，並將它系結至動作方法參數。 這項功能在涉及用戶端範本和資料系結的案例中很有用。 （用戶端範本可讓您使用在用戶端上執行的範本來格式化和顯示單一資料項目或一組資料項目）。MVC 3 可讓您輕鬆地在傳送和接收 JSON 資料的伺服器上，使用動作方法來連接用戶端範本。 如需 JSON 系結支援的詳細資訊，請參閱[Scott Guthrie 的 MVC 3 預覽 blog 文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)的**JavaScript 和 AJAX 改善**一節。

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>模型驗證改善

### <a name="dataannotations-metadata-attributes"></a>"DataAnnotations" 中繼資料屬性

ASP.NET MVC 3 支援 `DataAnnotations` 中繼資料屬性，例如 `DisplayAttribute`。

### <a name="validationattribute-class"></a>"ValidationAttribute" 類別

`ValidationAttribute` 類別已在 .NET Framework 4 中改善，以支援新的 `IsValid` 多載，以提供有關目前驗證內容的詳細資訊，例如要驗證的物件。 這可提供更豐富的案例，讓您可以根據模型的另一個屬性來驗證目前的值。 例如，新的 `CompareAttribute` 屬性可讓您比較模型中兩個屬性的值。 在下列範例中，`ComparePassword` 屬性必須符合 `Password` 欄位，才會生效。

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>驗證介面

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)介面可讓您執行模型層級的驗證，並可讓您提供整體模型狀態特有的驗證錯誤訊息，或模型內的兩個屬性之間。 在模型系結時，MVC 3 現在會從 `IValidatableObject` 介面中抓取錯誤，並使用內建的 HTML 表單協助程式自動旗標或反白顯示視圖中受影響的欄位。

[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)介面可讓 ASP.NET MVC 在執行時間探索驗證程式是否支援用戶端驗證。 這個介面已設計成可與各種不同的驗證架構整合。

如需驗證介面的詳細資訊，請參閱[Scott Guthrie 的 MVC 3 預覽 blog 文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)的**模型驗證改善**一節。 （不過請注意，在 blog 中，"IValidateObject" 的參考應該是 "IValidatableObject"）。

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>相依性插入改良功能

ASP.NET MVC 3 針對套用相依性插入（DI），以及與相依性插入或反轉控制（IOC）容器進行整合，提供更好的支援。 已在下欄區域中新增對 DI 的支援：

- 控制器（註冊和插入控制器工廠，插入控制器）。
- Views （註冊和插入視圖引擎，將相依性插入至視圖頁面）。
- 動作篩選（尋找和插入篩選器）。
- 模型系結器（註冊和插入）。
- 模型驗證提供者（註冊和插入）。
- 模型中繼資料提供者（註冊和插入）。
- 值提供者（註冊和插入）。

MVC 3 支援[泛型服務定位器](https://github.com/unitycontainer/commonservicelocator)程式庫，以及支援該程式庫之 `IServiceLocator` 介面的任何 DI 容器。 它也支援新的 `IDependencyResolver` 介面，可讓您更輕鬆地整合 DI 架構。

如需有關 MVC 3 中 DI 的詳細資訊，請參閱下列資源：

- [Brad Wilson 針對服務位置的一系列 blog 文章](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 版本資訊](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>其他新功能

### <a name="nuget-integration"></a>NuGet 整合

ASP.NET MVC 3 會在安裝過程中自動安裝並啟用 NuGet。 NuGet 是免費的開放原始碼套件管理員，可讓您輕鬆地在專案中尋找、安裝及使用 .NET 程式庫和工具。 它適用于所有 Visual Studio 專案類型（包括 ASP.NET Web Forms 和 ASP.NET MVC）。

NuGet 可讓維護開放原始碼專案（例如 Moq、NHibernate、Ninject、StructureMap、NUnit、Windsor、RhinoMocks 和 Elmah 等專案）的開發人員封裝其程式庫，並在線上元件庫中註冊。 然後，想要使用其中一個程式庫來尋找套件，並將它安裝在正在處理的專案中的 .NET 開發人員很容易。

透過 ASP.NET 3 工具更新，專案範本包含已預先安裝的 JavaScript 程式庫 NuGet 套件，因此可以透過 NuGet 進行更新。 Entity Framework Code First 也會預先安裝為 NuGet 套件。

如需 NuGet 的詳細資訊，請參閱 [NuGet 文件](https://docs.microsoft.com/nuget/) (英文)。

### <a name="partial-page-output-caching"></a>部分頁面輸出快取

ASP.NET MVC 支援從第1版開始的完整頁面回應輸出快取。 MVC 3 也支援部分頁面輸出快取，可讓您輕鬆地快取區域或回應片段。 如需快取的詳細資訊，請參閱 Scott Guthrie 的「**部分頁面輸出**快取」一節，其位於 mvc [3 發行候選版本](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)和[Mvc 3 版本](../whitepapers/mvc3-release-notes.md)資訊的**子動作輸出**快取一節。

### <a name="granular-control-over-request-validation"></a>對要求驗證的細微控制

ASP.NET MVC 具有內建的要求驗證，可自動協助防止 XSS 和 HTML 插入式攻擊。 不過，有時候您會想要明確停用要求驗證，例如，如果您想要讓使用者張貼 HTML 內容（例如，在 blog 專案或 CMS 內容中）。 您現在可以在模型系結期間，將[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)屬性新增至模型或視圖模型，以停用每個屬性的要求驗證。 如需要求驗證的詳細資訊，請參閱下列資源：

- [Scott Guthrie 在 MVC 3 發行候選版本的 blog 文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中，不**顯眼的 JavaScript 和驗證**一節。
- [MVC 3 版本資訊](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>可擴充的 [新增專案] 對話方塊

在 ASP.NET MVC 3 中，您可以將專案範本、視圖引擎和單元測試專案架構加入至 [**新增專案**] 對話方塊。

### <a name="template-scaffolding-improvements"></a>範本樣板的改良功能

ASP.NET MVC 3 樣板範本會更妥善地識別模型上的主鍵屬性，並適當地處理它們，而不是使用舊版 MVC。 （例如，現在，樣板範本會確保主鍵不會 scaffold 為可編輯的表單欄位）。

根據預設，[建立和編輯 scaffold] 現在會使用 `Html.EditorFor` helper，而不是 `Html.TextBoxFor` 協助程式。 這會在 [**加入視圖**] 對話方塊產生視圖時，以資料批註屬性的形式改善模型上的中繼資料支援。

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"LabelFor" 和 "Html. LabelForModel" 的新多載

已為 `LabelFor` 和 `LabelForModel` helper 方法加入新的方法多載。 新的多載可讓您指定或覆寫標籤文字。

### <a name="sessionless-controller-support"></a>無會話控制器支援

在 ASP.NET MVC 3 中，您可以指出您是否要讓控制器類別使用會話狀態，如果是，會話狀態應該是讀取/寫入或唯讀。 如需無會話控制器支援的詳細資訊，請參閱[MVC 3 版本](../whitepapers/mvc3-release-notes.md)資訊。

### <a name="new-additionalmetadataattribute-class"></a>新的 "AdditionalMetadataAttribute" 類別

您可以使用[AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)屬性來填入模型屬性的 `ModelMetadata.AdditionalValues` 字典。 例如，如果視圖模型具有只應顯示給系統管理員的屬性，您可以標注該屬性，如下列範例所示：

[!code-csharp[Main](mvc3/samples/sample4.cs)]

當呈現產品視圖模型時，任何顯示或編輯器範本都會提供此中繼資料。 您可以由您來解讀中繼資料資訊。

### <a name="accountcontroller-improvements"></a>AccountController 改良功能

網際網路專案範本中的 AccountController 已大幅改善。

### <a name="new-intranet-project-template"></a>新的內部網路專案範本

其中包含新的內部網路專案範本，可啟用 Windows 驗證並移除 AccountController。
