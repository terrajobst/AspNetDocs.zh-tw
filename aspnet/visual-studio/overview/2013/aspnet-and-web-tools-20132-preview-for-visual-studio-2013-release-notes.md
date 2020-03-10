---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: 適用于 Visual Studio 2013 版本資訊的 ASP.NET 和 Web 工具 2013.2 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 22d4d4afd6963f23d6cfef1745a859c20b69d599
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623190"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>適用於 Visual Studio 2013 的 ASP.NET 和 Web 工具 2013.2 版本資訊

由[Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>安裝注意事項

Visual Studio 2013.2 的 ASP.NET 和 Web 工具會配套在主要安裝程式中，而且可以下載為[Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)的一部分。

## <a name="documentation"></a>文件

有關 Visual Studio 2013.2 之 ASP.NET 和 Web 工具的教學課程和其他資訊可從[ASP.NET 網站](https://www.asp.net/)取得。

## <a name="software-requirements"></a>軟體需求

Visual Studio 2013.2 的 ASP.NET 和 Web 工具需要 Visual Studio 2013。

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio 2013.2 ASP.NET 和 Web 工具的新功能

下列各節說明版本中引進的功能。

- [一個 ASP.NET 專案範本](#oneaspnet)
- [在 IIS Express 上啟動 Web 應用程式時支援 SSL](#ssl)
- [Visual Studio Web 編輯器增強功能](#vswebeditor)
- [瀏覽器連結](#browserlink)
- [支援 Visual Studio 中的 Azure App Service Web Apps](#waws)
- [建立新的 Web 專案時建立遠端 Azure 資源](#AzureResources)
- [Web 發行增強功能](#webpublish)
- [ASP.NET 的樣板](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web Forms](#webforms)
- [ASP.NET MVC 5.1。2](#mvc)
- [ASP.NET Web API 2.1。2](#webapi)
- [ASP.NET Web Pages 3.1。2](#webpages)
- [Entity Framework 6。1](#ef)
- [ASP.NET Identity 2.0。0](#identity)
- [Microsoft OWIN 元件](#owin)
- [ASP.NET SignalR 2.0。2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>一個 ASP.NET 專案範本

- ASP.NET 專案範本的更新，以支援帳戶確認和密碼重設。
- 更新 ASP.NET Web API 範本，以支援使用內部部署組織帳戶進行驗證。
- ASP.NET SPA 範本現在包含以 MVC 和伺服器端視圖為基礎的驗證。 此範本具有 WebAPI 控制器，只能由已驗證的使用者存取。

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>在 IIS Express 上啟動 Web 應用程式時支援 SSL

為了消除在 localhost 上流覽和偵測 HTTPS 時的安全性警告，我們新增了一個對話方塊，讓 Internet Explorer 和 Chrome 信任自我簽署的 IIS express SSL 憑證。

例如，Web 專案屬性可以設定為使用 SSL。 按一下 F4 以顯示 [屬性] 對話方塊。 將 [ **SSL 已啟用**] 變更為 [true]。 複製 SSL URL。

![SSL 已啟用屬性](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

將 [Web 專案] 屬性頁 [web] 索引標籤設定為使用 HTTPS 型 URL （除非您先前已建立 SSL 網站，否則會 `https://localhost:44300/` SSL URL）。

![設定專案 URL （HTTPS）](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

按 CTRL+F5 執行應用程式。 遵循指示，以信任 IIS Express 所產生的自我簽署憑證。

![SSL 警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

閱讀 [**安全性警告**] 對話方塊，如果您想要安裝代表 localhost 的憑證，請按一下 **[是]** 。

![安全性警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

網站將會顯示在 IE 或 Chrome 中，而不會在瀏覽器中出現憑證警告。

![沒有警告的 HTTPS 頁面](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox 會使用自己的憑證存放區，因此它會顯示警告。

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web 編輯器增強功能

- **新的 json 專案專案和編輯器**：我們已將 json 專案專案和編輯器新增至 Visual Studio。 目前的 JSON 編輯器功能包括顏色標示、語法驗證、大括弧完成、大綱、工具選項設定等等。

    ![JSON 編輯器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense 現在支援[JSON 架構](http://json-schema.org/)v3 和 v4。 有一個 [架構] 下拉式方塊可選擇現有的架構、編輯本機架構路徑，或直接將專案 JSON 檔案拖放到其中，以取得相對路徑。

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 架構編輯器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **新的 Sass （SCSS）編輯器**：我們在 VS2013 RTM 中新增較少，而我們現在有 Sass 專案專案和編輯器。 Sass 編輯器功能相當於 LESS 編輯器，包括顏色標示、變數和 Mixin IntelliSense、批註/取消批註、快速諮詢、格式、語法驗證、大綱、移至定義、色彩選擇器、工具選項設定等。

    ![加入新專案： SCSS 樣式表單](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![樣式表單編輯器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML、Razor、CSS、LESS 和 Sass 檔中的新 URL 選擇器：** VS 2013 隨附于 Web Forms 頁面以外的任何 URL 選擇器。 適用于 HTML、Razor、CSS、LESS 和 Sass 編輯器的新 URL 選擇器是無對話、流暢類型的選擇器，可瞭解 ' ... ' 和會適當地篩選出 img 標記和連結的檔案清單。

    ![影像標記的 URL 選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![Views 的 URL 選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS 的 URL 選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **藉由新增更多功能來更新為較少的編輯器**
- **挖式 Intellisense 升級**：我們新增了 VS Intellisense 的非標準挖式語法，也就是 "ko vs-editor viewModel：" 語法。 它可以用來系結至頁面上的多個視圖模型，其格式如下：

    ![挖的 Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    我們也新增了對 nested ViewModel IntelliSense 的支援，因此您可以在 ViewModel 上切入到深度的嵌套物件。

    `<div data-bind="text: foo.bar.baz.etc" />`

    顯示的 IntelliSense 是 JavaScript 物件的完整 IntelliSense。

    ![顯示完整 JavaScript 物件的 Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML、Razor、CSS、LESS 和 Sass 檔中的新 URL 選擇器**： VS 2013 隨附于 Web Forms 頁面以外的無 URL 選擇器。 適用于 HTML、Razor、CSS、LESS 和 Sass 編輯器的新 URL 選擇器是無對話、流暢類型的選擇器，可瞭解 ' ... ' 和會適當地篩選出 img 標記和連結的檔案清單。

    ![影像標記的 URL 選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![Views 的 URL 選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS 的 URL 選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>瀏覽器連結

- 瀏覽器連結現在支援 HTTPS 連線，而且只要瀏覽器信任憑證，就會在儀表板中使用其他連線來列出該連接。
- 靜態 HTML 來源對應
- 適用于對應資料的 SPA 支援
- 自動更新對應資料

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>支援 Visual Studio 中的 Azure App Service Web Apps

- **支援 Azure 登入。**
- **Web 應用程式的遠端檢查和遠端查看**：我們現在支援[web 應用程式的遠端](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)檢查，Azure App Service 和在伺服器 explorer 中的 web 應用程式內容檔案的遠端流覽。

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>建立新的 Web 專案時建立遠端 Azure 資源

我們已在 [新增 web 應用程式] 對話方塊中新增 Azure [[建立遠端資源](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)] 核取方塊。 藉由選擇，您可以整合建立新 web 應用程式的體驗、設定 Azure 發行網站進行測試，並以幾個簡單的步驟來建立發行設定檔。

![使用 Azure 資源的新專案](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![發行至 Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web 發行增強功能

- 改善發佈的使用者體驗。

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 的樣板

- **列舉支援：** 如果您的模型使用列舉，則 MVC Scaffolder 會產生 Enum 的下拉式清單。 這會使用 MVC 中的列舉協助程式。
- **啟動程式支援**：更新 MVC 樣板中的 EditorFor 範本，使其使用啟動程式類別。
- **封裝支援**： Mvc 和 Web api 鷹架已經會加入適用于 Mvc 和 web api 的5.1 套件

下列螢幕擷取畫面示範了基架構模型。

- 模型程式碼：

     ![模型程式碼](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 編譯模型程式碼，以滑鼠右鍵按一下，然後選取 [**加入**]、[**新增 scaffold 專案**]。

     ![加入新的 Scaffold 專案](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **使用 Entity Framework，選擇具有 views 的 MVC5 控制器**：

     ![加入具有 views 的新 MVC5 控制器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- 使用模型**新增控制器**：

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 檢查產生的程式碼，例如 Views/WeekdayModels/Edit。 cshtml 包含包含 EnumDropDownListFor 的 `@Html.EnumDropDownListFor`： ![視圖](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 執行頁面以查看所產生的列舉 combobox，請注意，如果值可以是 null，則可以為下拉式方塊選擇空字串。 例如，[**建立**] 頁面會顯示下列內容：

    ![允許空字串的下拉式方塊](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM 將于2014年4月發行。 以下是版本資訊中的顯著重點，但如需這些變更的詳細資訊，請參閱[完整版本](http://docs.nuget.org/docs/release-notes/nuget-2.8)資訊。

- **目標 Windows Phone 8.1 應用程式**： NuGet 2.8.1 現在支援使用目標 framework 名字標記 ' WindowsPhoneApp '、' WPA '、' WindowsPhoneApp81 ' 和 ' WPA81 '，以 Windows Phone 8.1 應用程式為目標。

- 相依性**的修補程式解析**：當解析套件相依性時，NuGet 過去已實行的策略，會選取符合封裝相依性的最低主要和次要套件版本。 但與主要和次要版本不同的是，修補程式版本一律會解析為最高版本。 雖然此行為是因為善意的，但它卻建立了安裝具有相依性之套件的不確定性。
- **DependencyVersion 參數**：雖然 NuGet 2.8 變更瞭解析相依性的*預設*行為，但它也會透過套件管理員主控台中的-DependencyVersion 參數，更精確地控制相依性解析程式。 參數可讓您將相依性解析成最低可能版本（預設行為）、可能的最高版本，或最高的次要或修補程式版本。 此交換器僅適用于 powershell 命令中的安裝套件。
- **DependencyVersion 屬性**：除了上面詳述的-DependencyVersion 參數之外，nuget 也可以在定義預設值的 nuget.exe 檔案中設定新的屬性（如果未在安裝-package 的調用中指定-DependencyVersion 參數）。 [NuGet 套件管理員] 對話方塊也會遵循此值，進行任何安裝封裝作業。 若要設定此值，請將下列屬性新增至您的 nuget .config 檔案：

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **預覽具有-WhatIf 的 Nuget 作業**：某些 NuGet 套件可以有深度相依性圖形，因此在安裝、卸載或更新作業時，先瞭解會發生什麼事，可能會很有説明。 NuGet 2.8 新增標準 PowerShell-如果切換至安裝套件、卸載套件和更新套件命令，以視覺化方式將套用命令的整個套件關閉。
- **降級套件**：安裝套件的搶鮮版，以調查新功能，然後決定復原到最後一個穩定版本，並不是很常見的情況。 在 NuGet 2.8 之前，這是卸載發行前版本套件及其相依性，然後再安裝舊版的多步驟程式。 不過，使用 NuGet 2.8，更新套件現在會將整個套件關閉（例如套件的相依性樹狀結構）復原到先前的版本。
- **開發**相依性：許多不同類型的功能可以做為 NuGet 套件提供，包括用來優化開發程式的工具。 這些元件雖然可能有助於開發新的套件，但在稍後發行時，不應將其視為新封裝的相依性。 NuGet 2.8 可讓封裝將 nuspec 檔案中的本身識別為 developmentDependency。 安裝時，此中繼資料也會加入至已安裝封裝之專案的封裝 .config 檔案中。 當稍後針對 nuget.exe 套件中的 NuGet 相依性分析此封裝時，它會排除標示為開發相依性的相依性。
- **不同平臺的個別封裝 .config**檔案：開發多個目標平臺的應用程式時，每個各自的組建環境都有不同的專案檔案。 在不同的專案檔中使用不同的 NuGet 套件也很常見，因為套件具有不同平臺的各種支援層級。 NuGet 2.8 藉由為不同平臺特定的專案檔建立不同的 config.xml 檔案，為此案例提供了更好的支援。
- **回到本機**快取：雖然 nuget 套件通常會從遠端資源庫（例如使用網路連線的[nuget 資源庫](http://www.nuget.org)）取用，但在許多情況下，用戶端並未連接。 如果沒有網路連線，NuGet 用戶端就無法成功安裝套件，即使這些套件已經在本機 NuGet 快取的用戶端電腦上也一樣。 NuGet 2.8 會將自動快取回溯新增至套件管理員主控台。

    快取回退功能不需要任何特定的命令引數。 此外，快取回退目前僅適用于套件管理員主控台-此行為目前無法在 [套件管理員] 對話方塊中運作。
- **錯誤修正**：所做的其中一個主要錯誤修正是在更新-封裝-重新安裝命令中改善效能。

    除了這些功能和前述的效能修正之外，這一版的 NuGet 也包含其他許多 bug 修正。 發行中解決了181的總問題。 如需 NuGet 2.8 中已修正之工作專案的完整清單，請參閱此版本的[NuGet 問題追蹤](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)程式。

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Form

- Web form 範本現在會示範如何針對 ASP.NET Identity 進行帳戶確認和密碼重設。
- Entity Framework 6 的實體資料來源控制項和動態資料提供者。 如需詳細資訊，請參閱下列 MSDN blog：[動態資料提供者和適用于 Entity Framework 6 的 EntityDataSource 控制項](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)。

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1。2

- [屬性路由改善](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [編輯器範本的啟動程式支援](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Views 中的列舉支援](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [對 MinLength/MaxLength 屬性的不顯眼支援](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [在不顯眼的 Ajax 中支援 ' this ' 內容](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 各種[bug 修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1。2

- [全域錯誤處理](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [屬性路由增強功能](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [說明頁面改良功能](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute 支援](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 媒體類型格式器](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [更好的非同步篩選支援](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [用戶端格式化程式庫的查詢剖析](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 各種[bug 修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Web Pages 3.1。2

- 各種[bug 修正](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6。1

Entity Framework 已針對執行時間和工具更新為6.1 版。 Entity Framework （EF）6.1 是 Entity Framework 6 的次要更新，其中包含許多 bug 修正和新功能。 如需 EF 6.1 的詳細資訊，包括新功能檔的連結，請參閱[Entity Framework 版本歷程記錄](https://msdn.microsoft.com/data/jj574253)。 此版本中的新功能包括：

- **工具匯總**提供一致的方式來建立新的 EF 模型。 這項功能會擴充 ADO.NET 實體資料模型 wizard，以支援建立 Code First 模型，包括從現有的資料庫進行反向工程。 這些功能先前已在 EF Power tool 的 Beta 版品質中提供。
- **處理交易認可失敗**會提供新的[CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) ，利用新引進的功能來攔截交易作業。 **CommitFailureHandler**可讓您在認可交易時，從連線失敗中自動復原。
- **IndexAttribute**可讓您將屬性放在 Code First 模型的屬性（或屬性）上，藉以指定索引。 Code First 接著會在資料庫中建立對應的索引。
- **公用對應 API**可讓您存取 EF 對於屬性和類型如何對應至資料庫中的資料行和資料表的資訊。 在過去的版本中，此 API 是內部的。
- **能夠透過應用程式/web.config 檔案來設定攔截**器（允許新增攔截器，而不需重新編譯應用程式）。
- **DatabaseLogger**是新的攔截器，可讓您輕鬆地將所有資料庫作業記錄到檔案中。 結合先前的功能，可讓您輕鬆地切換已部署應用程式的資料庫作業記錄，而不需要重新編譯。
- 已改善**遷移模型變更偵測**，讓 scaffold 的遷移更為精確;變更偵測程式的效能也已大幅增強。
- **效能改進**，包括在初始化期間減少資料庫作業、在 LINQ 查詢中優化 null 相等比較、在更多案例中產生更快速的視圖（模型建立），以及更有效率地具體化具有多個關聯的追蹤實體。

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identity 2.0。0

- **雙因素驗證**： ASP.NET Identity 現在支援雙因素驗證。 雙因素驗證可在您的密碼遭到入侵的情況下，為您的使用者帳戶提供額外的安全性層級。 針對兩個因素代碼，也有受到暴力密碼破解攻擊的保護。
- **帳戶鎖定：** 提供一種方法，可在使用者不正確地輸入密碼或雙因素代碼時，鎖定使用者。 您可以設定封鎖的無效嘗試次數和使用者的 timespan。 開發人員可以選擇性地關閉特定使用者帳戶所需的帳戶鎖定。
- **帳戶確認：** ASP.NET Identity 系統現在支援帳戶確認。 這是現今大部分網站中相當常見的案例，當您在網站上註冊新的帳戶時，您必須確認您的電子郵件，才能在網站中執行任何動作。 電子郵件確認很有用，因為它可防止建立假的帳戶。 如果您使用電子郵件作為與網站使用者（例如論壇網站、銀行、電子商務或社交網站）通訊的方法，這會非常有用。
- **密碼重設：** 密碼重設功能可讓使用者在忘記密碼時重設其密碼。
- **安全性戳記（登出所有位置）：** 支援在使用者變更其密碼或任何其他安全性相關資訊（例如 Facebook、Google、Microsoft 帳戶等等）時，為使用者重新產生安全性權杖的方法。 這是為了確保使用舊密碼所產生的任何權杖都無效。 在範例專案中，如果您變更使用者的密碼，則會為使用者產生新的權杖，而且任何先前的權杖都會失效。 這項功能會為您的應用程式提供額外的安全性層級，因為當您變更密碼時，您將會登出已登入此應用程式的所有位置（所有其他瀏覽器）。
- **讓主要金鑰的類型可供使用者和角色**擴充：在 ASP.NET Identity 1.0 中，資料表使用者和角色的主鍵類型為字串。 這表示當 ASP.NET Identity 系統使用 Entity Framework 保存在 SQL Server 中時，我們使用的是 Nvarchar。 在 Stack Overflow 上和根據傳入的意見反應，有許多關於此預設實施的討論。 我們提供了擴充性攔截，您可以在其中指定您的 [使用者和角色] 資料表的主要金鑰。 如果您要遷移應用程式，而應用程式儲存使用者 id 是 Guid 或整數，則此擴充性攔截功能特別有用。
- **支援使用者和角色的 iqueryable**：在 UsersStore 和 RolesStore 上新增 iqueryable 的支援，您可以輕鬆地取得使用者和角色的清單。
- **透過 UserManager 支援刪除作業**
- 以使用者**名稱編制索引**：在 ASP.NET Identity Entity Framework 執行中，我們已使用 EF 6.1.0 中的新 IndexAttribute，在使用者名稱上新增唯一的索引。 這可確保使用者名稱一律是唯一的，而且沒有任何競爭條件，因此您最後可能會有重複的使用者名稱。
- **增強式密碼驗證程式：** 在 ASP.NET Identity 1.0 中出貨的密碼驗證程式是相當基本的密碼驗證程式，只會驗證最小長度。 有新的密碼驗證程式可讓您更充分掌控密碼的複雜性。 請注意，即使您開啟此密碼中的所有設定，我們仍建議您為使用者帳戶啟用雙因素驗證。
- **IdentityFactory 中介軟體/CreatePerOwinCoNtext**：

    - **使用者管理員**：您可以使用 Factory 執行，從 OWIN 內容取得 UserManager 的實例。 此模式與我們用來從 OWIN 內容取得 AuthenticationManager 以進行登入和 SignOut 的方式類似。 這是針對每個應用程式要求取得 UserManager 實例的建議方式。
    - **DbCoNtextFactory**： ASP.NET Identity 使用 Entity Framework，在 SQL Server 中保存身分識別系統。 為此，身分識別系統具有 [ApplicationdbcoNtext] 的參考。 DbCoNtextFactory 中介軟體會針對您可在應用程式中使用的每個要求，傳回 [ApplicationdbcoNtext] 的實例。
- **ASP.NET Identity 範例 nuget 套件**：範例 nuget 套件可讓您更輕鬆地安裝和執行 ASP.NET Identity 的範例，並遵循最佳作法。 這是 ASP.NET MVC 應用程式的範例。 在生產環境中部署之前，請先修改程式碼以符合您的應用程式。 此範例應該安裝在空的 ASP.NET 應用程式中。 如需套件的詳細資訊，請移至下列 blog 文章：[宣佈 ASP.NET Identity 2.0.0 的 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 元件

在此版本中已修正許多 bug。 如需詳細資訊，請參閱[2.1.0 版本的版本](https://katanaproject.codeplex.com/releases/view/113281)資訊。

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0。2

在此版本中已修正許多 bug。 如需詳細資訊，請參閱[2.0.2 版本的版本](https://github.com/SignalR/SignalR/releases/tag/2.0.2)資訊。
