---
uid: single-page-application/overview/templates/hottowel-template
title: 熱門紙巾範本 |Microsoft Docs
author: madskristensen
description: HotTowel 範本
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075056"
---
# <a name="hot-towel-template"></a>Hot Towel 範本

依[Mads Kristensen](https://github.com/madskristensen)

> 「熱門紙巾」 MVC 範本是由 John Papa 所撰寫
> 
> 選擇要下載的版本：
> 
> [Visual Studio 2012 的熱門紙巾 MVC 範本](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013 的熱門紙巾 MVC 範本](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> 熱紙巾：因為您不想要移至 SPA，而不需要一個！

想要建立 SPA，但無法決定要從何處開始？ 使用最熱門的紙巾，而在幾秒內，您就會有 SPA 和您需要建立的所有工具！

最棒的是使用 ASP.NET 建立單一頁面應用程式（SPA）的絕佳起點。 現成可用來為您的程式碼提供模組化結構、視圖導覽、資料系結、豐富的資料管理，以及簡單但簡潔的樣式。 「熱門的紙巾」提供您建立 SPA 所需的所有專案，因此您可以專注于應用程式，而不是「配管」。

> 深入瞭解如何從[John Papa 的影片、教學課程和 Pluralsight 課程](http://johnpapa.net/spa?vsix)建立 SPA。

## <a name="application-structure"></a>應用程式結構

「熱門的紙巾 SPA」提供應用程式資料夾，其中包含定義應用程式的 JavaScript 和 HTML 檔案。

在應用程式資料夾內：

- durandal 等架構
- 服務
- viewmodel
- 檢視

應用程式資料夾包含模組的集合。 這些模組會封裝功能，並宣告其他模組的相依性。 Views 資料夾包含您應用程式的 HTML，而 viewmodel 資料夾包含 views 的呈現邏輯（通用 MVVM 模式）。 [服務] 資料夾非常適合用來存放應用程式可能需要的任何一般服務，例如 HTTP 資料抓取或本機儲存體互動。 多個 viewmodel 通常會從服務模組重複使用程式碼。

## <a name="aspnet-mvc-server-side-application-structure"></a>ASP.NET MVC 伺服器端應用程式結構

熱門的紙巾建基於熟悉且功能強大的 ASP.NET MVC 結構。

- 應用程式\_啟動
- 內容
- Controllers
- 模型
- 指令碼
- 檢視

## <a name="featured-libraries"></a>精選程式庫

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET Web 優化-捆綁和縮制
- [輕鬆的 .js](http://Breezejs.com) -豐富資料管理
- [Durandal 等架構 .js](http://Durandaljs.com) -導覽和視圖撰寫
- [挖式 .js](http://Knockoutjs.com) -資料系結
- [需要 .js](http://requirejs.org) -具有 AMD 和優化的模組化
- [Toastr](http://jpapa.me/c7toastr) -快顯視窗訊息
- [Twitter 啟動](https://twitter.github.com/bootstrap/)程式-健全的 CSS 樣式

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>透過 Visual Studio 2012 的熱門紙巾 SPA 範本進行安裝

熱門的紙巾可以安裝為 Visual Studio 2012 範本。 只要按一下 `File` | `New Project`，然後選擇 [`ASP.NET MVC 4 Web Application`]。 然後選取 [熱門的紙巾單一頁面應用程式] 範本並執行！

## <a name="installing-via-the-nuget-package"></a>透過 NuGet 套件安裝

熱門的紙巾也是可增強現有空白 ASP.NET MVC 專案的 NuGet 套件。 只要使用 Nuget 進行安裝，然後執行！

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>我該如何建立在熱門的紙巾上？

只要開始加入程式碼！

1. 新增您自己的伺服器端程式碼，最好是 Entity Framework 和 WebAPI （這其實是使用簡單的 .js）
2. 將 views 新增至 `App/views` 資料夾
3. 將 viewmodel 新增至 `App/viewmodels` 資料夾
4. 將 HTML 和挖的資料系結新增至新的視圖
5. 更新 `shell.js` 中的導覽路由

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript 的逐步解說

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index. cshtml

[index] 是 MVC 應用程式的起始路由和視圖。 其中包含您預期的所有標準中繼標記、css 連結和 JavaScript 參考。 本文包含單一 `<div>`，這是要求所有內容（您的視圖）時將放置的位置。 `@Scripts.Render` 使用需要 .js 來執行應用程式程式碼的進入點，其包含在 `main.js` 檔案中。 系統會提供啟動顯示畫面，示範如何在應用程式載入時建立啟動顯示畫面。

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>App/main .js

`main.js` 檔案包含的程式碼，會在您的應用程式載入時立即執行。 這是您要定義流覽路由的位置、設定啟動視圖，以及執行任何安裝/啟動程式，例如預備應用程式的資料。

`main.js` 檔案會定義數個 durandal 等架構的模組，以協助應用程式開始進行。 Define 語句有助於解析模組相依性，使其可供函式使用。 首先會啟用偵錯工具訊息，這會將應用程式正在執行之事件的相關訊息傳送至主控台視窗。 應用程式. 啟動程式碼會指示 durandal 等架構架構啟動應用程式。 系統會設定慣例，讓 durandal 等架構知道所有 views 和 viewmodel 分別包含在相同的命名資料夾中。 最後，`app.setRoot` 啟動會使用預先定義的 `entrance` 動畫來載入 `shell`。

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>檢視

Views 可以在 `App/views` 資料夾中找到。

### <a name="shellhtml"></a>shell .html

`shell.html` 包含您的 HTML 的主要版面配置。 所有其他的視圖都會在 `shell` 視圖的某處組成。 「經常性存取」提供具有三種這類區域的 `shell`：標題、內容區域和頁尾。 當要求時，每個區域都會以其他視圖的內容形式載入。

頁首和頁尾的 `compose` 系結在「熱紙巾」中硬式編碼，分別指向 [`nav`] 和 [`footer`] views。 區段 `#content` 的撰寫系結系結至 `router` 模組的現用專案。 換句話說，當您按一下導覽連結時，它會在此區域中載入對應的 view。

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav .html

`nav.html` 包含 SPA 的流覽連結。 例如，您可以在這裡放置功能表結構。 這通常是資料系結（使用挖式）至 `router` 模組，以顯示您在 `shell.js`中定義的導覽。 挖起來會尋找資料系結屬性，並將其系結至 `shell` viewmodel 以顯示導覽路線，並在 `router` 模組正從一個視圖流覽至另一個時顯示 progressbar （使用 Twitter 啟動程式）（請參閱 `router.isNavigating`）。

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>首頁 .html 和詳細資料 .html

這些 views 包含自訂視圖的 HTML。 按一下 [`nav`] 視圖功能表中的 [`home`] 連結時，`home` 視圖會放在 [`shell`] 視圖的 [內容] 區域中。 您可以使用自己的自訂視圖來增強或取代這些視圖。

### <a name="footerhtml"></a>頁尾 .html

`footer.html` 包含出現在頁尾中的 HTML，位於 [`shell`] 視圖的底部。

## <a name="viewmodels"></a>ViewModels

Viewmodel 可在 `App/viewmodels` 資料夾中找到。

### <a name="shelljs"></a>shell .js

`shell` viewmodel 包含系結至 `shell` 視圖的屬性和函式。 通常這是找到功能表導覽系結的位置（請參閱 `router.mapNav` 邏輯）。

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>首頁和詳細資訊 .js

這些 viewmodel 包含系結至 `home` 視圖的屬性和函數。 它也包含視圖的呈現邏輯，而是資料和視圖之間的粘連。

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>服務

服務可在 [應用程式/服務] 資料夾中找到。 最理想的情況是，您未來的服務（例如 dataservice 模組），負責取得和張貼遠端資料。

### <a name="loggerjs"></a>記錄器 .js

熱紙巾會在 [服務] 資料夾中提供 `logger` 模組。 `logger` 模組適合用來將訊息記錄到主控台和快顯快顯通知中的使用者。
