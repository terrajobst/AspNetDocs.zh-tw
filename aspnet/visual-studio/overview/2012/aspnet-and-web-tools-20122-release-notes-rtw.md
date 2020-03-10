---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 和 Web 工具2012.2 版本資訊 |Microsoft Docs
author: rick-anderson
description: ASP.NET 和 Web 工具2012.2 的版本資訊。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579517"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 和 Web 工具 2012.2 版本資訊

> 本檔說明 ASP.NET 和 Web 工具2012.2 的版本。 這是 Visual Studio Web 工具和 ASP.NET 的更新。

- [安裝注意事項](#_Installation)
- [文件](#_Documentation)
- [支援](#_Support)
- [軟體需求](#_Software_Requirements)
- [ASP.NET 和 Web 工具2012.2 中的新功能](#_New_Features_in)

    - [工具](#_Tooling)
    - [網頁發佈](#_Web_Publishing)
    - [ASP.NET MVC 範本](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET 易記 Url](#_ASP.NET_Friendly_URLs)
- [已知問題和重大變更](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>安裝注意事項

您可以使用[Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)來安裝 Visual Studio 2012 的 ASP.NET 和 Web 工具2012.2。 這是 Visual Studio 2012 或 Visual Studio Express 2012 for Web 的更新，這是必要的。 如果您未安裝 Visual Studio，將會安裝適用于 Web 的 Visual Studio Express 2012。

您也可以手動安裝 ASP.NET 和 Web 工具2012.2。 您必須已安裝適用于 Web 的 Visual Studio 2012 或 Visual Studio Express 2012。 然後使用下列指示： 

1. 從下載中心下載[ASP.NET 和 Web framework 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)安裝程式。
2. 出現提示時，按一下 [執行]。 您也可以儲存檔案，以便稍後執行。
3. 確認您要更新的 Visual Studio 版本。 您可以藉由啟動您想要更新的 Visual Studio 來完成這項操作。 然後按一下 [說明] 功能表項目。   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. 如果您看到功能表項目 &quot;關於 Web&quot; 的 Microsoft Visual Studio 2012，請下載 web[開發人員工具 2012.2-Visual Studio Express 2012 For web](https://go.microsoft.com/fwlink/?LinkID=282228)。 否則，請下載[Web Developer Tools 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)。
5. 出現提示時，按一下 [執行]。 您也可以儲存檔案，以便稍後執行。

> [!NOTE]
> ASP.NET 和 Web 工具2012.2 版本不包含 SQL Server Data Tools。 SQL Server 和 Windows Azure SQL database 提供一組更豐富的資料庫工具，包括離線專案支援的開發、架構比較和增強的資料庫部署功能。 如需詳細資訊或安裝 SQL Server Data Tools 流覽[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)。

<a id="_Documentation"></a>
## <a name="documentation"></a>文件

您可以從 ASP.NET 網站（ https://www.asp.net)取得 ASP.NET 和 Web 工具2012.2 的教學課程和其他資訊。

<a id="_Support"></a>
## <a name="support"></a>支援

ASP.NET 和 Web 工具2012.2 已正式發行並受到支援。 您可以使用您的一般支援通道。 您也可以將問題張貼至 ASP.NET 論壇（[https://forums.asp.net/](https://forums.asp.net/)），其中 ASP.NET 社區的成員經常能夠提供非正式的支援。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>軟體需求

ASP.NET 和 Web 工具2012.2 需要 Web 的 Visual Studio 2012 或 Visual Studio Express 2012。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET 和 Web 工具2012.2 中的新功能

本節說明 ASP.NET 和 Web 工具2012.2 版本中引進的功能。

<a id="_Tooling"></a>
### <a name="tooling"></a>Tooling

- Page Inspector 

    - 支援 JavaScript 選取對應可讓 Page Inspector 將以動態方式新增至頁面的專案對應回相對應的 JavaScript 程式碼。
    - 即時查看 CSS 更新的功能。
    - 如需詳細資訊，請參閱[Page Inspector 中的 CSS 自動同步處理和 JavaScript 選取對應](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。
- 編輯器 

    - 支援 CoffeeScript、Mustache、Handlebars 和 JsRender 的語法醒目提示。
    - HTML 編輯器會提供 Intellisense 來進行挖結系結。
    - 較少的編輯和編譯器支援，可讓您使用較少的建立動態 CSS。
    - 將 JSON 貼入 .NET 類別。 使用這個特殊的 [貼上] 命令將C# JSON 貼入或 VB.NET 程式碼檔案中，Visual Studio 會自動產生從 JSON 推斷的 .net 類別。
- 行動模擬器支援新增擴充性攔截，讓協力廠商模擬器可以安裝為 VSIX。 已安裝的模擬器會顯示在 F5 下拉式清單中，讓開發人員可以在各種行動裝置上預覽其網站。 如需這項功能的詳細資訊，請參閱 Scott Hanselman 在[與 Visual Studio 的新 BrowserStack 整合](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)的 blog 專案。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web Publishing

- 網站專案現在具有與 Web 應用程式專案相同的發佈體驗，包括發行至 Windows Azure 網站。
- 選擇性發佈&#8211;一或多個檔案您可以執行下列動作（發佈至 Web Deploy 端點之後）： 

    - 發行選取的檔案。
    - 查看本機檔案與遠端檔案之間的差異。
    - 以遠端檔案更新本機檔案，或使用本機檔案更新遠端檔案。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 範本

- 全新的 Facebook 應用程式範本可讓撰寫 Facebook Canvas 應用程式再容易不過了。 只需幾個簡單的步驟，您便可建立 Facebook 應用程式，進而取得已登入使用者的資料並將資料與他的朋友進行整合。 此範本包括一個新程式庫，處理建置 Facebook 應用程式時所涉及的所有連結，包括授權、權限、存取 Facebook 資料等等。 如需使用 Facebook 應用程式範本的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)。
- 全新的單一網頁應用程式 MVC 範本可讓開發人員使用 HTML 5、CSS 3 和熱門的 Knockout 與 jQuery JavaScript 程式庫，在 ASP.NET Web API 的基礎上建置互動式用戶端 Web 應用程式。 此範本包含「待辦事項」清單應用程式，其中示範建立使用 RESTful 伺服器 API 之 JavaScript HTML5 應用程式的常見作法。 您可以在[https://www.asp.net/single-page-application](../../../single-page-application/index.md)閱讀更多。
- 您現在可以建立 VSIX，將新的範本新增至 [ASP.NET MVC 新增專案] 對話方塊。 瞭解做法： [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 套件&#8211; MVC 專案範本已更新為包含新的 ' FixedDisplayModes ' NuGet 套件，其中包含 MVC 4 中 bug 的因應措施。 如需封裝中包含之修正的詳細資訊，請參閱 MVC 小組的這篇 blog 文章（[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)）。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API 已透過數個新功能增強：

- ASP.NET Web API OData
- ASP.NET Web API 追蹤
- ASP.NET Web API 說明頁面

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData 提供您在任何資料來源上使用豐富商務邏輯建立 OData 端點所需的彈性。 有了 ASP.NET Web API OData，您就可以控制要公開的 OData 語義數量。 ASP.NET Web API OData 隨附于 ASP.NET MVC 4 專案範本，而且也可以從 NuGet （[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)）取得。

ASP.NET Web API OData 目前支援下列功能：

- 套用 [可查詢] 屬性來啟用 OData 查詢語義。
- 輕鬆驗證 OData 查詢，並限制支援的查詢選項、運算子和函式的集合。
- 參數系結至直接 ODataQueryOptions，以取得查詢的抽象語法樹狀結構標記法，然後可以驗證並套用至 IQueryable 或 IEnumerable。
- 藉由指定 [可查詢] 屬性的結果限制，啟用服務導向分頁和下一頁連結產生。
- 使用 $inlinecount，要求相符資源總數的內嵌計數。
- 控制 null 傳播。
- $Filter 中的任何/所有運算子。
- 依照慣例推斷實體資料模型，或明確自訂模型，其方式類似于 Entity Framework 程式碼優先。
- 藉由衍生自 EntitySetController 來公開實體集。
- 簡單、可自訂的慣例，用來公開導覽屬性、操作連結和執行 OData 動作。
- 使用 MapODataRoute 擴充方法簡化路由。
- 藉由公開多個 EDM 模型來支援版本控制。
- 公開服務檔和 $metadata，讓您可以為 Web API 產生用戶端（.NET、Windows Phone、Windows Store 等等）。
- 支援 OData Atom、JSON 和 JSON 詳細資訊格式。
- 建立、更新、部分更新（PATCH）和刪除實體。
- 查詢和操作實體之間的關聯性。
- 建立連接到您的路由的關聯性連結。
- 複雜類型。
- 實體類型繼承。
- 集合屬性。
- 列舉.
- OData 動作。
- 建基於與 WCF Data Services 相同的基礎，亦即 ODataLib （[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)）。

如需 ASP.NET Web API OData 的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)。

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 追蹤

ASP.NET Web API 追蹤會使用 .NET 追蹤來整合 Web Api 的追蹤資料。 在 Web API 專案範本中，它現在會預設為啟用。 Web Api 的追蹤資料會傳送至 [輸出] 視窗，並可透過 IntelliTrace 取得。 ASP.NET Web API 追蹤可讓您在 Windows Azure 上透過與[windows Azure 診斷](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)的整合，追蹤 Web API 的相關資訊。 您也可以使用 ASP.NET Web API 追蹤 NuGet 套件（[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)），在任何應用程式中安裝並啟用 ASP.NET Web API 追蹤。

如需設定和使用 ASP.NET Web API 追蹤的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)。

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 說明頁面

[ASP.NET Web API 說明] 頁面現在預設會包含在 [Web API] 專案範本中。 [ASP.NET Web API 說明] 頁面會自動產生 Web Api 的檔，包括 HTTP 端點、支援的 HTTP 方法、參數和範例要求和回應訊息裝載。 檔會自動從您程式碼中的批註提取。 您也可以使用 ASP.NET Web API 說明頁面 NuGet 套件（[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)），將 ASP.NET Web API 說明頁新增至任何應用程式。

如需設定和自訂 ASP.NET Web API [說明] 頁面的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR 可讓您輕鬆地將即時 web 功能新增至您的 ASP.NET 應用程式，使用 Websocket （如果有的話），並在沒有時自動回復至其他技術。

如需使用 ASP.NET SignalR 的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET 易記 URL

ASP.NET FriendlyURLs 讓 web form 開發人員能夠非常輕鬆地產生清楚的 Url （不含 .aspx 副檔名）。 幾乎不需要進行任何設定，而且可以與現有的 ASP.NET v4.0 應用程式搭配使用。 FriendlyURLs 功能也可讓開發人員藉由支援在桌面與行動裝置之間切換，更輕鬆地將行動支援新增至應用程式。

如需安裝和使用 ASP.NET 易記 Url 的詳細資訊，請參閱[http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

本節說明 ASP.NET 和 Web 工具2012.2 版本中的已知問題和重大變更。

### <a name="installation-issues"></a>安裝問題

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>依序安裝 Visual Studio 2012

安裝 ASP.NET 和 Web 工具2012.2 之後，安裝 Visual Studio 2012 的額外 SKU 將需要修復操作。 考量以下發生順序：

1. 安裝 Visual Studio 2012 Express for Web
2. 安裝 ASP.NET 和 Web 工具2012。2
3. 安裝 Visual Studio 2012 Professional、Premium 或旗艦版

步驟2只會導致安裝 Express for Web 的更新。 為確保步驟3中安裝的其他 SKU 包含更新，您必須修復 ASP.NET 和 Web 工具2012.2，才能安裝最後安裝的 SKU 更新。 如果步驟1和3中的 Sku 是相反的，這也適用。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio 開啟時安裝 Microsoft ASP.NET 和 Web 工具2012。2

如果在安裝 Microsoft ASP.NET 和 Web 工具2012.2 期間，VS 是開啟的，Visual Studio 可能會導致不正確的狀態。 建議使用者先關閉 Visual Studio 的所有實例，再繼續進行安裝。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>在安裝過程中取消 ASP.NET 和 Web 工具2012.2 安裝程式

在安裝過程中取消 ASP.NET 和 Web 工具2012.2 安裝程式將會讓 Visual Studio 處於不正常的狀態。 若要解決此問題，請遵循下列步驟： 

- 移至 [新增或移除程式]
- 卸載 Microsoft ASP.NET 和 Web 工具2012.2 （如果有的話）。
- 重新安裝 Microsoft ASP.NET 和 Web 工具2012。2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>卸載 ASP.NET 和 Web 工具2012.2 之後，缺少 ASP.NET MVC 4 範本和 Razor v2 網站範本

卸載 ASP.NET 和 Web 工具2012.2 也會從 Visual Studio 2012 卸載所有的 ASP.NET MVC 4 和 Razor v2 網站範本。

解決方法是修復您的 Visual Studio 2012 安裝，以重新安裝 ASP.NET MVC 4 和 Razor v2 網站範本。

### <a name="tooling-issues"></a>工具問題

#### <a name="nuget-error-reported-during-project-creation"></a>建立專案期間回報的 NuGet 錯誤

安裝 ASP.NET 和 Web 工具2012.2 之後，您可能會在建立 MVC 4 專案時看到下列錯誤

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET 和 Web 工具2012.2 隨附 NuGet 2.1，並會在 Visual Studio 2012 中升級延伸模組。 在某些情況下，VSIX 安裝程式將無法正確更新 VSIX。 下列步驟可讓您解決此問題：

1. 以系統管理員身分啟動 Visual Studio 2012
2. 移至 [工具]-&gt;[擴充功能和更新]，然後卸載 NuGet。
3. 關閉 Visual Studio
4. 流覽至 ASP.NET 和 Web 工具2012.2 安裝資料夾：

    1. 針對 Visual Studio 2012： **Program FILES\MICROSOFT ASP. NET\ASP.NET Web Stack\Visual Studio 2012**
    2. 針對 Visual Studio 2012 Express for Web： **Program FILES\MICROSOFT ASP. NET\ASP.NET web Stack\Visual Studio Express 2012 For web**
5. 按兩下 [Nuget.exe] 以重新安裝 NuGet

### <a name="web-api-issues"></a>Web API 問題

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>剖析 $filter 和日期時間常值中的問題

OData URI 剖析器無法正確剖析部分日期時間常值。 例如，$filter = start eq datetime ' 2012-12-31T12： 00 ' 無法正確剖析。 解決方法是使用完整的常值，$filter = start eq datetime ' 2012-12-31T12：00： 00 '。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData 不支援不區分大小寫的屬性名稱。

Odata 不支援 OData 查詢和 odata 路徑中不區分大小寫的屬性名稱。 請參閱工作專案：

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

如果使用者在 javascript 用戶端和伺服器端上有不同的大小寫，他們可能會遇到此問題。 此問題是在 odata 通訊協定中設計的。 不過，許多使用者會報告此問題。 若要解決此情況，使用者必須在 URL 中更正其案例。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>預設 OData 路由慣例不支援導覽屬性的 POST/PUT。

預設 OData 路由慣例不支援導覽屬性的 POST/PUT。 請參閱工作專案[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)。 在預設慣例中，我們遺漏了這個常用慣例。

若要解決此情況，使用者必須擴充新的路由慣例來支援它。

### <a name="facebook-template-issues"></a>Facebook 範本問題

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook 應用程式範本僅適用于使用 .NET 4。5

您必須在 [新增專案] 對話方塊的 [架構] 下拉式清單中選取 [.NET 4.5]，以查看 ASP.NET MVC 4 中的 Facebook 應用程式範本。

#### <a name="real-time-update-controller"></a>即時更新控制器

Facebook 應用程式範本可讓使用者輕鬆地建立 Web API 控制器，以處理來自 Facebook 的即時更新。 如果您的開發電腦位於 NAT 後方，則您的控制器可能無法在沒有進一步的網路設定的情況下工作。 如需詳細資訊，請參閱這裡： [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>查詢字串值與 Facebook OAuth 參數衝突

下欄欄位與 Facebook OAuth 對話的回呼 URL 衝突。 請勿新增您自己的查詢字串值，其名稱如下：程式碼、錯誤、錯誤\_描述、錯誤\_原因。

#### <a name="using-page-inspector-with-facebook-template"></a>搭配 Facebook 範本使用 Page Inspector

您無法使用 Visual Studio 2012 中的 Page Inspector 功能來偵測您的 Facebook 應用程式。 Page Inspector 目前不支援 iframe。

### <a name="single-page-application-template-issues"></a>單一頁面應用程式範本問題

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>使用 JQuery 1.9/挖 2.2.1 update 時，執行預設 MVC SPA 專案時，不會正確處理新的 todo 專案編輯輸入焦點事件。

使用 JQuery 1.9/挖 2.2.1 update 時，執行預設 MVC SPA 專案時，新的 todo 專案編輯輸入在輸入待辦事項清單的新待辦事項之後，不會再將焦點放回新的 [待辦事項] 編輯方塊。

若要解決此問題，請參考[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)，並對下列範例程式碼進行類似的修正：

檔案 todo. model .js  
 函數 todolist （資料），加入下列內容：  
 **isSelected = ko。可觀察（false）;**

addTodo 的 todoList，新增下列黑色文字：  
 **isSelected （true）;**  
 newTodoTitle （&quot;&quot;）;

檔案索引. cshtml，加入下列黑色文字：  
 &lt;表單資料系結 =&quot;提交： addTodo&quot;&gt;  
 &lt;輸入類別 =&quot;addTodo&quot; 類型 =&quot;文字&quot; 資料系結 =&quot;值： newTodoTitle，預留位置： ' 在這裡加入 ' 類型 '，blurOnEnter： true， **hasfocus： isSelected**，事件： {模糊： addTodo}&quot; /&gt;  
 &lt;/form&gt;
