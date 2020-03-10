---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 504202068f5db4f8614bba02e8066ffecfd15b48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78618045"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

- [概觀](#overview)
- [安裝注意事項](#installation-notes)
- [軟體需求](#software-requirements)
- [文件](#documentation)
- [支援](#support)
- [將 ASP.NET MVC 2 專案升級至 ASP.NET MVC 3 工具更新](#upgrading)
- [ASP.NET MVC 3 工具更新（2011年4月12日）](#tu-changes)

    - [[新增控制器] 對話方塊現在可以使用 views 和資料存取程式碼 scaffold 控制器](#tu-AddControllerDialog)
    - [[ASP.NET MVC 3 新增專案] 對話方塊的改善](#tu-ImprovementsNewDialogBox)
    - [專案範本現在包含 Modernizr 1。7](#tu-Modernizr)
    - [專案範本包含 jQuery、jQuery UI 和 jQuery 驗證的更新版本](#tu-UpdatedJQuery)
    - [專案範本現在包含 ADO.NET Entity Framework 4.1，做為預先安裝的 NuGet 套件](#tu-EF)
    - [專案範本以預先安裝的 NuGet 套件形式包含 JavaScript 程式庫](#tu-JavaScriptLibsNuget)
    - [已知問題](#tu-KI)
- [ASP.NET MVC 3 RTM （2011年1月13日）](#MVC3RTM)

    - [變更：將 jQuery UI 的版本更新為1.8。7](#RTM-1)
    - [變更：將預設 ModelMetadataProvider 變更回 DataAnnotationsModelMetadataProvider](#RTM-2)
    - [已修正：貼上包含空白字元的 Razor 運算式部分，會導致它被反轉](#RTM-3)
    - [已修正：重新命名在編輯器中開啟的 Razor 檔案時，會停用語法顏色標示和 IntelliSense](#RTM-4)
    - [已知問題](#RTM-KI)
    - [重大變更](#RTM-BC)
- [ASP.NET MVC 3 候選版2（2010年12月10日）](#_Toc2)

    - [專案範本已變更為包含 jQuery 1.4.4、jQuery 驗證1.7 和 jQuery UI 1.8.6 y UI 1.8。6](#_Toc2_1)
    - [已新增 "AdditionalMetadataAttribute" 類別](#_Toc2_2)
    - [改良的視圖樣板](#_Toc2_3)
    - [已新增 Html。 Raw 方法](#_Toc2_3)
    - [將 "Controller. ViewModel" 屬性和 "View" 屬性重新命名為 "ViewBag"](#_Toc2_4)
    - [將 "ControllerSessionStateAttribute" 類別重新命名為 "SessionStateAttribute"](#_Toc2_5)
    - [將 RemoteAttribute "Fields" 屬性重新命名為 "AdditionalFields"](#_Toc2_6)
    - [已將 "SkipRequestValidationAttribute" 重新命名為 "AllowHtmlAttribute"](#_Toc2_7)
    - [已將 "ValidationMessage" 方法變更為顯示第一個有用的錯誤訊息](#_Toc2_8)
    - [已修正 @model 宣告，不要在檔中加入空白字元](#_Toc2_9)
    - [已新增 "Microsoft.extensions.configuration fileextensions" 屬性來查看引擎，以支援引擎特定的檔案名](#_Toc2_10)
    - [已修正 "LabelFor" Helper 以發出 "For" 屬性的正確值](#_Toc2_11)
    - [已修正 "RenderAction" 方法，以在模型系結期間提供明確值的優先順序](#_Toc2_12)
    - [重大變更](#_Toc2_BC)
    - [已知問題](#_Toc2_KI)
- [ASP.NET MVC 3 發行候選版本（2010年11月9日）](#TOC_ASP_NET_3_RC)

    - [ASP.NET MVC 3 RC 中的新功能](#_Toc276711785)
    - [NuGet 套件管理員](#_Toc276711786) (英文)
    - [改良的 [新增專案] 對話方塊](#_Toc276711787)
    - [無會話控制器](#_Toc276711788)
    - [新的驗證屬性](#_Toc276711789)
    - ["LabelFor" 和 "LabelForModel" 方法的新多載](#_Toc276711790)
    - [子動作輸出快取](#_Toc276711791)
    - [[加入視圖] 對話方塊的改善](#_Toc276711792)
    - [細微要求驗證](#_Toc276711793)
    - [重大變更](#_Toc276711794)
    - [已知問題](#_Toc276711795)
- [ASP.MVC 3 Beta 附注（2010年10月6日）](#TOC_ASP_NET_3_Beta)

    - [ASP.NET MVC 3 Beta 的新功能](#0.1__Toc274034215)
    - [NuPack 套件管理員](#0.1__Toc274034216)
    - [改良的 [新增專案] 對話方塊](#0.1__Toc274034217)
    - [在 Razor Views 中指定強型別模型的簡化方式](#0.1__Toc274034218)
    - [支援新的 ASP.NET Web Pages Helper 方法](#0.1__Toc274034219)
    - [其他相依性插入支援](#0.1__Toc274034220)
    - [不顯眼的 jQuery 型 Ajax 的新支援](#0.1__Toc274034221)
    - [不顯眼 jQuery 驗證的新支援](#0.1__Toc274034222)
    - [適用于用戶端驗證和不顯眼 JavaScript 的新全應用程式旗標](#0.1__Toc274034223)
    - [新支援在 Views 執行之前執行的程式碼](#0.1__Toc274034224)
    - [VBHTML Razor 語法的新支援](#0.1__Toc274034225)
    - [更精細地控制 Validateinputattribute 套用](#0.1__Toc274034226)
    - [協助程式將底線轉換為使用匿名物件指定之 HTML 屬性名稱的連字號](#0.1__Toc274034227)
    - [錯誤修正](#0.1__Toc274034228)
    - [重大變更](#0.1__Toc274034229)
    - [已知問題](#0.1__Toc274034230)
- [免責聲明](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>概觀

本檔說明適用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 版本。 ASP.NET MVC 是一種架構，可用於開發使用模型視圖控制器（MVC）模式的 Web 應用程式。 ASP.NET MVC 3 安裝套裝程式含下列元件：

- ASP.NET MVC 3 執行時間元件
- ASP.NET MVC 3 Visual Studio 2010 工具
- ASP.NET Web Pages 執行時間元件
- ASP.NET Web Pages Visual Studio 2010 工具
- 適用于 .NET 的 Microsoft 套件管理員（NuGet）
- Visual Studio 2010 的更新，可支援 Razor 語法。 （如需詳細資訊，請參閱知識庫文章2483190。）

您可在 ASP.NET 網站上找到 ASP.NET MVC 3 每個預先發行版本之版本資訊的完整集合，其 URL 如下所示：

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>安裝注意事項

若要使用 Web Platform Installer （Web PI）安裝 ASP.NET MVC 3 RTM，請造訪下列頁面：

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

或者，您可以從下列頁面下載適用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 安裝程式：

https://go.microsoft.com/fwlink/?LinkID=208140

ASP.NET MVC 3 可以安裝，而且可以與 ASP.NET MVC 2 並存執行。

<a id="software-requirements"></a>
## <a name="software-requirements"></a>軟體需求

ASP.NET MVC 3 執行時間元件需要下列軟體：

- .NET Framework 第4版。 

    ASP.NET MVC 3 Visual Studio 2010 工具需要下列軟體：
- Visual Studio 2010 或 Visual Web Developer 2010 Express。

<a id="documentation"></a>
## <a name="documentation"></a>文件

您可以在 MSDN 網站上取得 ASP.NET MVC 的檔，網址如下：

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

如需有關 ASP.NET MVC 的教學課程和其他資訊，請在 ASP.NET 網站的 MVC 頁面上找到，網址如下：

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>支援

這是有完整支援的版本。 您可以在[Microsoft 支援服務網站](https://support.microsoft.com/)中找到取得技術支援的相關資訊。

您也可隨時在 ASP.NET MVC 論壇張貼對此版本的問題，ASP.NET 社群成員可經常在此提供非正式的支援：

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>將 ASP.NET MVC 2 專案升級至 ASP.NET MVC 3 工具更新

ASP.NET MVC 3 可以與 ASP.NET MVC 2 並存安裝在同一部電腦上，讓您有彈性選擇何時將 ASP.NET MVC 2 應用程式升級為 ASP.NET MVC 3。

若要將現有的 ASP.NET MVC 2 應用程式手動升級至第3版，請執行下列動作：

1. 在您的電腦上建立新的空白 ASP.NET MVC 3 專案。 這個專案將會包含升級所需的一些檔案。
2. 將下列檔案從 ASP.NET MVC 3 專案複製到 ASP.NET MVC 2 專案的對應位置。 您必須更新所有 jQuery 程式庫的參考，以說明新檔案名稱 (jQuery-1.5.1.js)： 

    - /Views/Web.config
    - /packages.config
    - /scripts/\*.js
    - /Content/themes/\*。\*
3. 將空白 ASP.NET MVC 3 專案方案根目錄中的 [*套件*] 資料夾複製到方案的根目錄中，這位於方案的 .sln 檔案所在的目錄中。
4. 如果您的 ASP.NET MVC 2 專案包含任何區域，請將/Views/Web.config 檔案複製到每個區域的*Views*資料夾。
5. 在 ASP.NET MVC 2 專案中的兩個 web.config 檔案中，全域搜尋並取代 ASP.NET MVC 版本。 搜尋下列文字： 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    取代為下列內容：

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. 在方案總管中，刪除*system.web*的參考（指向第2版的 DLL），然後加入*system.web*的參考（v 3.0.0.0）。
7. 加入 System.web 的參考，然後再新增 system.web. system.web。 這些組件位於下列資料夾： 

    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies
    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies
8. 在 [方案總管] 中，以滑鼠右鍵按一下專案名稱，並選取 [卸載專案]。 然後再次以滑鼠右鍵按一下專案名稱，並選取 [編輯*專案*名稱 .csproj]。
9. 找出*ProjectTypeGuids*元素，並將 {F85E285D-A4E0-4152-9332-AB1D724D3325} 取代為 {E53F8FEA-EAE0-44A6-8774-FFD645390401}。
10. 儲存變更、以滑鼠右鍵按一下專案，然後選取 [重新載入專案]。
11. 在應用程式的根 web.config 檔案中，將下列設定新增至 [*元件*] 區段。 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. 如果專案參考使用 ASP.NET MVC 2 編譯的任何協力廠商程式庫，請將下列反白顯示的*bindingRedirect*元素新增至應用程式根目錄的 web.config 檔案中設定*區段底下*： 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 3 工具更新中的變更

本節說明自 ASP.NET MVC 3 RTM 版本以來，在 ASP.NET MVC 3 工具更新版本中所做的變更。

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>[加入控制器] 對話方塊現在可以使用檢視和資料存取程式碼 Scaffold 控制器

Scaffolding 可用來快速產生您應用程式的控制器和檢視。 程式碼產生之後，您可以進行編輯，以符合您的專案需求。

若要啟動 ASP.NET MVC 3 中的 [*新增控制器*] 對話方塊，請以滑鼠右鍵按一下*方案總管*中的 [*控制器*] 資料夾，按一下 [*新增*]，然後按一下 [*控制器*]。 此對話方塊功能已增強，可提供額外的 Scaffolding 選項。

![](mvc3-release-notes/_static/image1.png)

根據預設，有三個 Scaffolding 範本可供使用。

#### <a name="empty-controller"></a>空白控制器

此範本會產生空白的控制器檔案。 此範本等同于在舊版 ASP.NET MVC 中，不會*針對 [建立]、[編輯]、[詳細資料]、[刪除] 案例檢查新增動作*。 如果您選擇此範本，就不能另外提供選項。

#### <a name="controller-with-empty-readwrite-actions"></a>具有空白讀取/寫入動作的控制器

此範本會產生包含所有必要動作方法的控制器檔案，但方法中沒有實作程式碼。 此範本相當於針對舊版 ASP.NET MVC 中*的 [建立]、[編輯]、[詳細資料]、[刪除] 案例檢查 [加入動作*]。 如果您選擇此範本，就不能另外提供選項。

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>具有讀取/寫入動作和檢視、使用 Entity Framework 的控制器

此範本可讓您迅速建立有效的資料輸入使用者介面。 它會產生用於處理一組通用需求和案例的程式碼，如下所示：

- *資料存取*。 產生的程式碼會在資料庫中讀取和寫入實體。 如果您選擇現有的資料內容類別，或如果您讓範本產生新的*DbCoNtext*類別，它就會與 Entity Framework Code First 方法搭配使用。 如果您選擇現有的*ObjectCoNtext*類別，它也適用于 Entity Framework Database First 或 Model First 方法。
- *驗證*。 產生的程式碼會使用 ASP.NET MVC 模型繫結和中繼資料功能，如此系統會根據模型類別所宣告的規則來驗證表單提交作業。 這包括內建的驗證規則，例如*Required*和*StringLength*屬性，以及自訂驗證規則。
- *一對多關聯性*。 如果您在模型類別之間定義一對多外部索引鍵關係，則產生的程式碼會產生下拉式清單供您選擇相關的實體。 例如，您可能依循「Entity Framework 程式碼優先」慣例定義下列模型類別： 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    當您接著 scaffold *product*類別的控制器時，其 views 可讓使用者為每個*產品*實例選擇*Category*物件。

    此範本會啟用 [*新增控制器*] 對話方塊中的其他選項。 針對*模型類別*，您可以在方案中選擇任何模型類別，這會決定使用者可以建立或編輯的資料類型：
- 如果您要使用「Entity Framework 程式碼優先」，則可以選擇任何模型類別。
- 如果您使用的是「Entity Framework 資料庫優先」或「Entity Framework 模型優先」，請務必選擇您概念模型中定義的實體類別。

針對*資料內容類別*，您可以進行下列選擇：

- 如果您想要使用 Code First，而且沒有現有的資料內容類別，請選擇 [新增資料內容]。 系統會為您產生資料內容類別。
- 如果您要使用「程式碼優先」且具有資料內容類別，則在此選擇此類別。 此類別會進行更新以保存您選取的模型類別。
- 如果您使用的是「資料庫優先」或「模型優先」，則在此選擇您的物件內容類別。

針對 [檢視]，請選擇您要使用的檢視引擎，或選擇 [無]，如果您不要 Scaffold 任何檢視。

您可以選取 [Advanced Optionsto]，為產生的視圖指定進一步的選項。 例如，您可以選擇要使用的版面配置頁或主版頁面。

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>[ASP.NET MVC 3 新增專案] 對話方塊中的改進功能

您用來建立新 ASP.NET MVC 3 專案的對話方塊包含多項改良功能，如下所示。

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>新的「內部網路專案」範本

[專案範本] 清單包含新的 [內部網路應用程式] 範本。 此範本包含的設定是用於以 Windows 驗證 (而不是表單驗證) 建置 Web 應用程式。 因為內部網路應用程式需要一些無法封裝在專案範本中的 IIS 設定，所以範本會包含讀我檔案，其中包含如何讓專案範本在 IIS 中工作的指示。 您可以在 MSDN 網站上找到新的內部網路應用程式範本的檔，網址如下：

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>專案範本現在已啟用 HTML5

[新增專案] 對話方塊現在包含可將 HTML5 專屬功能加入至專案範本的選項。 選取此選項會產生包含新 HTML5 `<header>`、`<footer>`和 `<navigation>` 元素的 views。

請注意舊版瀏覽器不支援 HTML5 專屬標記。 若要解決這項限制，HTML5 專案範本必須加入 Modernizr 程式庫的參考 (請參閱下節)。

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>專案範本現在包含 Modernizr 1.7

Modernizr 是一種 JavaScript 程式庫，可支援瀏覽器中尚未支援這些功能的 CSS 3 和 HTML5。 此程式庫是以預先安裝的 NuGet 套件形式包含在 ASP.NET MVC 3 專案的範本中。 如需 Modernizr 的詳細資訊，請參閱[http://www.modernizr.com/](http://www.modernizr.com/)。

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>專案範本包含 jQuery、jQuery UI 和 jQuery Validation 的更新版本

專案範本現在包含下列 jQuery 指令碼版本：

- jQuery 1.5.1
- jQuery Validation 1.8
- jQuery UI 1.8.11

這些程式庫皆以預先安裝的 NuGet 套件形式內含在專案範本中。

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>專案範本現在包含 ADO.NET Entity Framework 4.1，其以預先安裝的 NuGet 套件形式內含在範本中

ADO.NET Entity Framework 4.1 包含 Code First 功能。 「程式碼優先」是 ADO.NET Entity Framework 的新開發模式，提供另一種方法來替代現有「資料庫優先」和「模型優先」模式。

「程式碼優先」的重點是使用以 Visual Basic 或 C# 撰寫的 POCO 類別 (「一般簡單的 CLR 物件」) 定義您的模型。 這些類別接著可以對應至現有資料庫，或用來產生資料庫結構描述。 您可以使用*DataAnnotations*屬性或使用流暢的 api 來提供額外的設定。

如需使用程式碼 Firstwith ASP.NET MVC 的檔，請參閱 ASP.NET 網站上的下列 Url：

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>專案範本包含 JavaScript 程式庫，其以預先安裝的 NuGet 套件形式內含在範本中

當您建立新的 ASP.NET MVC 3 專案時，專案會包含先前所述的 JavaScript 檔案（例如，Modernizr 程式庫），方法是使用 NuGet 安裝它們，而不是直接將腳本新增至專案範本中的 Scripts 資料夾。編制. 如此可讓您在指令碼新版本發行時，使用 NuGet 將指令碼更新為最新版本。

例如，鑑於 jQuery 新版發行的頻率，專案範本內含的 jQuery 版本在某個時間點即會過時。 不過，因為 jQuery 是以已安裝的 NuGet 套件內含在專案範本中，當 jQuery 新版發行時，將會透過 NuGet 對話方塊通知您。

因為 jQuery 在檔案名中包含版本號碼，所以將 jQuery 更新為最新版本也需要更新參考 jQuery 檔案的 `<script>` 標記，以使用新的檔案名。 其他內含的指令碼程式庫並沒有在指令碼名稱中加入版本編號，所以較易於更新為最新版本。

<a id="tu-KI"></a>
## <a name="known-issues"></a>已知問題

- 在某些情況下，安裝可能會失敗，並出現錯誤訊息「安裝失敗，錯誤碼為（0x80070643）」。 如需有關如何解決此問題的詳細資訊，請參閱[知識庫文章 2531566](https://support.microsoft.com/kb/2531566)。
- 用於加入控制器的 scaffolding 不會 Scaffold 利用 Entity Framework 實體繼承支援的實體。 例如，假設有一個由*student*類別繼承的基礎*Person*類別，則*student*類別會產生未編譯的程式碼。
- 在方案資料夾中建立新的 ASP.NET MVC 3 專案會造成*NullReferenceException*錯誤。 因應措施是在方案的根目錄中建立 ASP.NET MVC 3 專案，然後將它移至方案資料夾。
- 電腦若有安裝 ReSharper，Razor 語法的 IntelliSense 即無法運作。 如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 中的 Razor IntelliSense 支援，請參閱 Hadi Hariri 的 blog 中的專案[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中會討論今日使用它們的方式。
- 在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。
- 當您編輯 Razor view （. cshtml 或）時。*vbhtml*檔案）、views。 ASP.NET MVC 3 不包含 Razor views 的任何程式碼片段。aspxselecting ASP.NET MVC 的程式碼片段會顯示的程式碼片段
- 如果您在未安裝 Visual Studio 的電腦上安裝 ASP.NET MVC 3 for Visual Web Developer Express，然後在稍後安裝 Visual Studio，則必須重新安裝 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共用 ASP.NET MVC 3 安裝程式所升級的元件。 如果您在沒有 Visual Web Developer Express 的電腦上安裝 ASP.NET MVC Visual Studio 3，然後再安裝 Visual Web Developer Express，則適用相同的問題。

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>ASP.NET MVC 3 RTM 中的變更

本節說明自 RC2 版本開始，在 ASP.NET MVC 3 RTM 版本中所做的變更和 bug 修正。

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>變更：將 jQuery UI 的版本更新為1.8。7

Visual Studio 的 ASP.NET MVC 專案範本已更新為包含最新版的 jQuery UI 程式庫。 這些範本也包含 jQuery UI 所需的最小資源檔集，例如相關聯的 CSS 和影像檔案。

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>變更：將預設 ModelMetadataProvider 變更回 DataAnnotationsModelMetadataProvider

ASP.NET MVC 3 的 RC2 版本引進了*CachedDataAnnotationsMetadataProvider*類別，它會在現有*DataAnnotationsModelMetadataProvider*類別上提供快取，以改善效能。 不過，某些 bug 是使用此實作為回報，因此變更已還原並移至 MVC 先期專案中，可在[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)取得。

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>已修正：貼上包含空白字元的 Razor 運算式部分，會導致它被反轉

在 ASP.NET MVC 3 的發行前版本中，當您將包含空白字元的 Razor 運算式部分貼入 Razor 檔案時，產生的運算式會反轉。 例如，請考慮下列 Razor 程式碼區塊：

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

如果您在第一個方法中選取「第一個參數」文字，並將它當做引數貼入第二個方法中，則結果會如下所示：

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

正確的行為是貼上作業應該會產生下列結果：

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

此問題已在 RTM 版本中修正，以便在貼上作業期間正確地保留運算式。

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>已修正：重新命名在編輯器中開啟的 Razor 檔案時，會停用語法顏色標示和 IntelliSense

在編輯器視窗中開啟檔案時，使用方案總管重新命名 Razor 檔案，會導致語法醒目提示和 IntelliSense 停止處理該檔案。 已修正此問題，以便在重新命名之後維護反白顯示和 IntelliSense。

<a id="RTM-KI"></a>
## <a name="known-issues"></a>已知問題

- 如果您在 NuGet 套件管理員主控台開啟時關閉 Visual Studio 2010 SP1 Beta 版，Visual Studio 損毀並嘗試重新開機。 這會在 Visual Studio 2010 SP1 的 RTM 版本中修正。
- ASP.NET MVC 3 安裝程式只可以安裝 NuGet 套件管理員的初始版本。 安裝初始版本之後，您可以使用 Visual Studio 擴充管理員來安裝和更新 NuGet。 如果您已安裝 NuGet，請移至 Visual Studio 擴充功能庫，以更新為最新版本的 NuGet。
- 在方案資料夾中建立新的 ASP.NET MVC 3 專案會造成*NullReferenceException*錯誤。 因應措施是在方案的根目錄中建立 ASP.NET MVC 3 專案，然後將它移至方案資料夾。
- 安裝程式所需的時間可能比先前版本的 ASP.NET MVC 還長，因此無法完成。 這是因為它會更新 Visual Studio 2010 的元件。
- 電腦若有安裝 ReSharper，Razor 語法的 IntelliSense 即無法運作。 如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 中的 Razor IntelliSense 支援，請參閱 Hadi Hariri 的 blog 中的專案[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中會討論今日使用它們的方式。
- 使用 ASP.NET MVC 3 Beta 版所建立的 CCSHTML 和 VBHTML 視圖並未正確設定其組建動作，結果是在發行專案時，會省略這些檢視類型。 這些檔案的 [組建動作] 值應該設定為 [內容]。 ASP.NET MVC 3 RTM 會針對新檔案修正此問題，但不會針對使用發行前版本所建立之專案的現有檔案更正其設定。
- ![](mvc3-release-notes/_static/image3.png)
- 在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。
- 當您編輯 Razor view （cshtml 檔案）時，Visual Studio 中的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。
- 如果您在未安裝 Visual Studio 的電腦上安裝 ASP.NET MVC 3 for Visual Web Developer Express，然後在稍後安裝 Visual Studio，則必須重新安裝 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共用 ASP.NET MVC 3 安裝程式所升級的元件。 如果您在沒有 Visual Web Developer Express 的電腦上安裝 ASP.NET MVC Visual Studio 3，然後再安裝 Visual Web Developer Express，則適用相同的問題。

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>重大變更

- 在舊版的 ASP.NET MVC 中，動作篩選準則會針對每個要求建立，但在少數情況下除外。 這種行為絕對不是保證的行為，而是只有執行詳細資料，而篩選準則的合約是將其視為無狀態。 在 ASP.NET MVC 3 中，篩選會更積極地快取。 因此，任何不正確儲存實例狀態的自訂動作篩選可能會中斷。
- 例外狀況篩選準則的執行順序已針對具有相同*順序*值的例外狀況篩選準則進行變更。 在 ASP.NET MVC 2 和更早版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其*順序*值會與動作方法上的相同。 這通常是沒有指定*順序*值的例外狀況篩選準則套用時的情況。 在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。 如同在舊版中，如果已明確指定*order*屬性，則會以指定的循序執行篩選。
- 已將名為*microsoft.extensions.configuration fileextensions*的新屬性新增至*VirtualPathProviderViewEngine*基類。 當 ASP.NET 依路徑（而不是名稱）查詢檢視時，只會考慮包含在此新屬性所指定清單中具有副檔名的 views。 這是應用程式的重大變更，其中已註冊自訂群組建提供者以啟用 Web 表單檢視的自訂副檔名，以及提供者使用完整路徑（而非名稱）來參考這些視圖。 解決方法是修改*microsoft.extensions.configuration fileextensions*屬性的值，以包含自訂副檔名。
- 直接執行*IControllerFactory*介面的自訂控制器 factory 預建必須提供新*GetControllerSessionBehavior*方法的實作為，這會在此版本中新增至介面。 一般來說，建議您不要直接執行此介面，而改為從*DefaultControllerFactory*衍生您的類別。

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>ASP.NET MVC 3 RC2 中的變更

本節說明自 RC 版本以來 ASP.NET MVC 3 RC2 版本中所做的變更（新功能和 bug 修正）。

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>專案範本已變更為包含 jQuery 1.4.4、jQuery 驗證1.7 和 jQuery UI 1.8。6

ASP.NET MVC 3 的專案範本現在包含 jQuery、jQuery 驗證和 jQuery UI 的最新版本。 jQuery UI 是專案範本的新功能，並提供實用的使用者介面小工具。 如需 jQuery UI 的詳細資訊，請造訪其首頁： [http://jqueryui.com/](http://jqueryui.com/)。

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>已新增 "AdditionalMetadataAttribute" 類別

您可以使用*AdditionalMetadataAttribute*類別來填入模型屬性的*ModelMetadata. AdditionalValues*字典。

例如，假設視圖模型具有應該只顯示給系統管理員的屬性。 該模型可以使用 AdminOnly 做為索引鍵的新屬性加上批註，並以 true 作為值，如下列範例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

當呈現產品視圖模型時，任何顯示或編輯器範本都會提供此中繼資料。 身為應用程式開發人員，您可以用它來解讀中繼資料資訊。

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>改良的視圖樣板

用於樣板視圖的 T4 範本現在會產生對範本協助程式方法的呼叫，例如*EditorFor* ，而不是像是*TextBoxFor*的協助程式。 這項變更會在 [加入視圖] 對話方塊產生視圖時，以資料批註屬性的形式改善模型上的中繼資料支援。

[加入視圖] 樣板也會根據慣例，在模型上包含改善的主要金鑰資訊偵測和使用方式。 例如，[加入視圖] 對話方塊會使用這項資訊來確保主要索引鍵值不會 scaffold 為可編輯的表單欄位。

預設的 [編輯] 和 [建立] 範本包含用戶端驗證所需之 jQuery 腳本的參考。

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>已新增 Html。 Raw 方法

根據預設，Razor view 引擎會對所有值進行 HTML 編碼。 例如，下列程式碼片段會將問候語變數中的 HTML 編碼，使其在頁面中顯示為 `<strong>Hello World!</strong>`。

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

新的 *.html*方法提供簡單的方式，在已知內容安全時顯示未編碼的 Html。 下列範例會顯示相同的字串，但字串會轉譯為標記：

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>將 "Controller. ViewModel" 屬性和 "View" 屬性重新命名為 "ViewBag"

在過去，*控制器*的*ViewModel*屬性會雖然該值至視圖的*view*屬性。 這兩個屬性都提供使用動態屬性存取子語法來存取*ViewDataDictionary*物件值的方式。 這兩個屬性都已重新命名為相同，以避免混淆並使其更一致。

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>將 "ControllerSessionStateAttribute" 類別重新命名為 "SessionStateAttribute"

*ControllerSessionStateAttribute*類別是在 ASP.NET MVC 3 的 RC 版本中引進。 屬性已重新命名為更簡潔。

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>將 RemoteAttribute "Fields" 屬性重新命名為 "AdditionalFields"

*RemoteAttribute*類別的*Fields*屬性會在使用者之間造成一些混淆。 將此屬性重新命名為*AdditionalFields* ，表示其意圖。

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>已將 "SkipRequestValidationAttribute" 重新命名為 "AllowHtmlAttribute"

*SkipRequestValidationAttribute*屬性已重新命名為*AllowHtmlAttribute* ，以更好的方式表示其預期的使用方式。

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>已將 "ValidationMessage" 方法變更為顯示第一個有用的錯誤訊息

已修正*ValidationMessage*方法來顯示第一個有用的錯誤訊息，而不是只顯示第一個錯誤。

在模型系結期間，可以從多個來源填入*ModelState*字典，其中包含有關屬性的錯誤訊息，包括從模型本身（如果它會執行*IValidatableObject*）、從套用至屬性的驗證屬性，以及存取屬性時擲回的例外狀況。

當*ValidationMessage*方法顯示驗證訊息時，它會略過包含例外狀況的模型狀態專案，因為這通常不是供使用者使用。 相反地，方法會尋找未與例外狀況相關聯的第一個驗證訊息，並顯示該訊息。 如果找不到這類訊息，則會預設為與第一個例外狀況相關聯的一般錯誤訊息。

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>已修正 @model 宣告，不要在檔中加入空白字元

在舊版中，在視圖頂端的 `@model` 宣告，已將空白行新增至轉譯的 HTML 輸出。 已修正此問題，因此宣告不會引進空白字元。

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>已新增 "Microsoft.extensions.configuration fileextensions" 屬性來查看引擎，以支援引擎特定的檔案名

視圖引擎可以使用明確的視圖路徑來傳回視圖，如下列範例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

第一個 view 引擎一律會嘗試呈現視圖。 根據預設，Web form view engine 是第一個 view 引擎;因為 Web 表單引擎無法轉譯 Razor 視圖，所以會發生錯誤。 View engine 現在有一個*microsoft.extensions.configuration fileextensions*屬性，用來指定支援的副檔名。 當 ASP.NET 判斷視圖引擎是否可以轉譯檔案時，會檢查這個屬性。 這是一項重大變更，此檔的[重大變更](#_Toc2_BC)一節包含更多詳細資料。

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>已修正 "LabelFor" Helper 以發出 "For" 屬性的正確值

修正了 bug，其中*LabelFor*方法呈現了符合*輸入*專案之*name*屬性（而非其 ID）的*for*屬性。 根據 W3C， *for*屬性應符合*輸入*元素的識別碼。

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>已修正 "RenderAction" 方法，以在模型系結期間提供明確值的優先順序

在舊版中，傳遞至*RenderAction*方法的明確值，會在子動作內的模型系結期間忽略目前的表單值。 修正可確保明確的值在模型系結期間會優先。

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>重大變更

- 在舊版的 ASP.NET MVC 中，除了少數情況以外，每個要求都會建立動作篩選準則。 這種行為絕對不是保證的行為，而是只有執行詳細資料，而篩選準則的合約是將其視為無狀態。 在 ASP.NET MVC 3 中，篩選會更積極地快取。 因此，任何不正確儲存實例狀態的自訂動作篩選可能會中斷。
- 例外狀況篩選準則的執行順序已針對具有相同*順序*值的例外狀況篩選準則進行變更。 在 ASP.NET MVC 2 和更早版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其*順序*值與動作方法上的相同。 這通常是未使用指定的*順序*值來套用例外狀況篩選時的情況。 在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。 如同在舊版中，如果已明確指定*order*屬性，則會以指定的循序執行篩選。
- 已將名為*microsoft.extensions.configuration fileextensions*的新屬性新增至*VirtualPathProviderViewEngine*基類。 當 ASP.NET 依路徑（而不是名稱）查詢檢視時，只會考慮包含在此新屬性所指定清單中具有副檔名的 views。 這是應用程式的重大變更，其中已註冊自訂群組建提供者以啟用 Web 表單檢視的自訂副檔名，以及提供者使用完整路徑（而非名稱）來參考這些視圖。 解決方法是修改*microsoft.extensions.configuration fileextensions*屬性的值，以包含自訂副檔名。
- 直接執行*IControllerFactory*介面的自訂控制器 factory 預建必須提供新*GetControllerSessionBehavior*方法的實作為，這會在此版本中新增至介面。 一般來說，建議您不要直接執行此介面，而改為從*DefaultControllerFactory*衍生您的類別。

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>已知問題

- ASP.NET MVC 3 安裝程式只可以安裝 NuGet 套件管理員的初始版本。 安裝初始版本之後，您可以使用 Visual Studio 擴充管理員來安裝和更新 NuGet。 如果您已安裝 NuGet，請移至 Visual Studio 擴充功能庫，以更新為最新版本的 NuGet。
- 在方案資料夾中建立新的 ASP.NET MVC 3 專案會造成*NullReferenceException*錯誤。 因應措施是在方案的根目錄中建立 ASP.NET MVC 3 專案，然後將它移至方案資料夾。
- 安裝程式所需的時間可能比先前版本的 ASP.NET MVC 還長，因此無法完成。 這是因為它會更新 Visual Studio 2010 的元件。
- 電腦若有安裝 ReSharper，Razor 語法的 IntelliSense 即無法運作。 如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 RC2 中的 Razor IntelliSense 支援，請參閱 Hadi Hariri 的 blog 中的專案[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中會討論今日使用它們的方式。
- 以 ASP.NET MVC 3 的 Beta 版建立的 CSHTML 和 VBHTML views 並未正確設定其組建動作，結果是在發行專案時，會省略這些檢視類型。 這些檔案的 [*組建動作*] 值應該設定為 [內容]。 ASP.NET MVC 3 RC2 會修正新檔案的這個問題，但不會更正以 Beta 版所建立之專案的現有檔案設定。![](mvc3-release-notes/_static/image4.png)
- 在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。
- 當您編輯 Razor view （cshtml 檔案）時，Visual Studio 中的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。
- 如果您在未安裝 Visual Studio 的電腦上安裝 ASP.NET MVC 3 for Visual Web Developer Express，然後在稍後安裝 Visual Studio，則必須重新安裝 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共用 ASP.NET MVC 3 安裝程式所升級的元件。 如果您在沒有 Visual Web Developer Express 的電腦上安裝 ASP.NET MVC Visual Studio 3，然後再安裝 Visual Web Developer Express，則適用相同的問題。
- 如果您已安裝 ASP.NET MVC 3 RC 2，則不會更新 NuGet。 若要升級 NuGet，請移至 Visual Studio 擴充管理員，它應該會顯示為可用的更新。 您可以從該處將 NuGet 升級至最新版本。

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 發行候選版本

ASP.NET MVC 發行候選版本已于2010年11月9日發行。

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>ASP.NET MVC 3 RC 中的新功能

本節說明自 Beta 版以來，已在 ASP.NET MVC 3 RC 版本中引進的功能。

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>NuGet 套件管理員

ASP.NET MVC 3 包含 NuGet 套件管理員（之前稱為 NuPack），這是整合的封裝管理工具，可用來將程式庫和工具新增至 Visual Studio 專案。 這種工具可讓開發人員立即採取的步驟，將程式庫帶入其來源樹狀結構中。

您可以使用 NuGet 做為命令列工具，作為 Visual Studio 2010 內的整合式主控台視窗，從 [Visual Studio] 內容功能表，以及一組 PowerShell Cmdlet。

如需 NuGet 的詳細資訊，請參閱[Nuget 檔](https://docs.microsoft.com/nuget/)。

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>改良的 [新增專案] 對話方塊

當您建立新的專案時，[新增專案] 對話方塊現在可讓您指定 view engine 以及 ASP.NET MVC 專案類型。

![](mvc3-release-notes/_static/image5.png)

此版本包含修改範本清單和對話方塊中所列之視圖引擎的支援。

預設範本如下所示：

空白。 包含 ASP.NET MVC 專案的最小檔案集，包括 ASP.NET MVC 專案的預設目錄結構、包含預設 ASP.NET MVC 樣式的 .css 檔案，以及包含預設 JavaScript 檔案的腳本目錄。

網際網路應用程式。 包含範例功能，示範如何搭配使用成員資格提供者與 ASP.NET MVC。

對話方塊中顯示的專案範本清單會在 Windows 登錄中指定。

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>無會話控制器

新的*ControllerSessionStateAttribute*會藉由指定[SessionState SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx)列舉值，讓您更充分掌控控制器的會話狀態行為。

下列範例顯示如何關閉對控制器之所有要求的會話狀態。

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

下列範例顯示如何設定對控制器之所有要求的唯讀會話狀態。

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>新的驗證屬性

#### <a name="compareattribute"></a>CompareAttribute

新的*CompareAttribute*驗證屬性可讓您比較模型中兩個不同屬性的值。 在下列範例中， *ComparePassword*屬性必須符合*密碼*欄位，才會生效。

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

新的*RemoteAttribute*驗證屬性會利用 jQuery 驗證外掛程式的遠端驗證程式，這可讓用戶端驗證在執行實際驗證邏輯的伺服器上呼叫方法。

在下列範例中， *UserName*屬性已套用*RemoteAttribute* 。 在編輯檢視中編輯此屬性時，用戶端驗證會在*UsersController*類別上呼叫名為*UserNameAvailable*的動作，以便驗證此欄位。

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

下列範例會顯示對應的控制器。

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

根據預設，套用屬性的屬性名稱會以查詢字串參數的形式傳送至動作方法。

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>"LabelFor" 和 "LabelForModel" 方法的新多載

已新增*LabelFor*和*LabelForModel*方法的新多載，可讓您指定標籤文字。 下列範例顯示如何使用這些多載。

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>子動作輸出快取

*OutputCacheAttribute*支援使用*RenderAction*或*html. 動作*協助程式方法所呼叫之子動作的輸出快取。 下列範例顯示呼叫另一個動作的視圖。

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

*GetDate*動作會以*OutputCacheAttribute*標注：

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

當此程式碼執行時，會快取呼叫 Html. Action （"GetDate"）的結果100秒。

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>[加入視圖] 對話方塊的改善

當您加入強型別視圖時，[加入視圖] 對話方塊現在會篩選出比舊版更不適用的類型，例如許多核心 .NET Framework 類型。 此外，此清單現在會依類別名稱排序，而不是完整的類型名稱，讓您更輕鬆地尋找類型。 例如，現在會顯示類型名稱，如下列範例所示：

ClassName （命名空間）

在先前的版本中，這會顯示如下：

Namespace. ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>細微要求驗證

*Validateinputattribute 套用*的*Exclude*屬性不再存在。 相反地，若要在模型系結期間略過模型特定屬性的要求驗證，請使用新的*SkipRequestValidationAttribute*。

例如，假設有一個動作方法用來編輯 blog 文章：

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

下列範例顯示 blog 文章的視圖模型。

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

當使用者提交 Description 屬性的某些標記時，模型系結會因為要求驗證而失敗。 若要在進行 blog 文章描述的模型系結期間停用要求驗證，請將*SkipRequpestValidationAttribute*套用至屬性，如下列範例所示：。

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

或者，若要關閉模型的每個屬性的要求驗證，請將值為*false*的*validateinputattribute 套用*套用至動作方法：

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>重大變更

- 例外狀況篩選準則的執行順序已針對具有相同*順序*值的例外狀況篩選準則進行變更。 在 ASP.NET MVC 2 和更早版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其*順序*與動作方法上的相同。 這通常是未使用指定的*順序*值來套用例外狀況篩選時的情況。 在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。 如同在舊版中，如果已明確指定*order*屬性，則會以指定的循序執行篩選。
- 將名為*microsoft.extensions.configuration fileextensions*的新屬性新增至*VirtualPathProviderViewEngine*基類。 依路徑（而不是依名稱）查閱 view 時，只會考慮使用此新屬性所指定之清單中包含副檔名的 views。 這是針對註冊自訂群組建提供者以啟用 web 表單檢視之自訂副檔名，並使用完整路徑（而非名稱）來參考這些視圖的使用者的重大變更。 解決方法是修改*microsoft.extensions.configuration fileextensions*屬性的值，以包含自訂副檔名。

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>已知問題

- 安裝程式所需的時間可能比舊版的 ASP.NET MVC 更長，因為它會更新 Visual Studio 2010 的元件。
- 選取 astrongly 具類型的 view scaffold 僅限寫入屬性時的加入視圖。 這些樣板應一律予以忽略。 當產生「編輯」或「建立」視圖時，[加入視圖] 對話方塊也會 scaffold 唯讀屬性。 唯讀屬性只應針對顯示和列出視圖進行 scaffold。
- 當 ASP.NET MVC 3 與非同步 CTP 一起安裝時，不能進行調試。 ASP.NET MVC 3 無法與非同步 CTP 並存安裝。 卸載非同步 CTP 以修復調試。 如需詳細資訊，請閱讀[這篇](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html)關於卸載 ASP.NET MVC 3 RC 所有部分的文章。
- 安裝 Resharper 時，Razor Intellisense 無法運作。 如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 RC 中的 Razor intellisense 支援，請閱讀來自 JetBrains 的[這篇 blog 文章](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)，其中會討論今天使用這些專案的方法。
- 以 ASP.NET MVC 3 搶鮮版建立的 CSHTML 和 VBHTML views，其組建動作不會正確地使其無法發行。 這些檔案的*組建動作*應設定為 [內容]。 ASP.NET MVC 3 RC 會針對新檔案修正此問題，但不會更正以 Beta 版所建立之專案的現有檔案設定。
- 安裝程式所需的時間可能比舊版的 ASP.NET MVC 更長，因為它會更新 Visual Studio 2010 的元件。
- 選取 [編輯] [強型別視圖] scaffold 唯讀屬性時的 [加入視圖] 樣板。 同樣地，[顯示] 視圖也會 scaffold 僅限寫入的屬性。
- 在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。
- 安裝 Visual Studio 非同步 CTP 會與 ASP.NET MVC 3 工具安裝中包含的 Razor 版本發生衝突。 請確定您未嘗試在同一部電腦上安裝 Visual Studio 非同步 CTP 和 Razor 版本。
- 當您編輯 Razor view （cshtml 檔案）時，Visual Studio 中的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 Beta

ASP.NET MVC 3 Beta 已于2010年10月6日發行。 下列是 Beta 版特有的附注，受限於上述 ASP.NET MVC 3 發行候選章節中所參考的任何更新或變更。

## <a id="0.1__Toc274034215"></a>新的 Featuresin ASP.NET MVC 3 Beta

<a id="0.1__Default_validation_system"></a>本節說明 ASP.NET MVC 3 Beta 版本中引進的功能。

### <a id="0.1__Toc274034216"></a>NuGet 套件管理員

ASP.NET MVC 3 包含 NuGet 套件管理員，這是一個整合的封裝管理工具，可用來將程式庫和工具新增至 Visual Studio 專案。 在大部分的情況下，它會將開發人員立即採取的步驟自動化，以將程式庫帶入其來源樹狀結構。

您可以使用 NuGet 做為命令列工具，做為 Visual Studio 2010 內的整合式主控台視窗，從 [Visual Studio] 內容功能表，以及一組 PowerShell Cmdlet。

如需 NuGet 的詳細資訊，請參閱[Nuget 檔](https://docs.microsoft.com/nuget/)。

### <a id="0.1__Toc274034217"></a>改良的 [新增專案] 對話方塊

當您建立新的專案時，[新增專案] 對話方塊現在可讓您指定 view engine 以及 ASP.NET MVC 專案類型。

![](mvc3-release-notes/_static/image6.png)

此版本不包含修改對話方塊中所列的範本清單和視圖引擎的支援。

預設範本如下所示：

空白。 包含 ASP.NET MVC 專案的最小檔案集，包括 ASP.NET MVC 專案的預設目錄結構、包含預設 ASP.NET MVC 樣式的小型網站 .css 檔案，以及包含預設 JavaScript 檔案的腳本目錄。

網際網路應用程式。 包含範例功能，示範如何在 ASP.NET MVC 中使用成員資格提供者。

### <a id="0.1__Toc274034218"></a>在 Razor Views 中指定強型別模型的簡化方式

為強型別 Razor views 指定模型類型的方法，已經使用適用于 CSHTML views 的新 @model 指示詞和 VBHTML 視圖的 @ModelType 指示詞來簡化。 在舊版的 ASP.NET MVC 中，您會以這種方式指定 Razor views 的強型別模型：

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

在此版本中，您可以使用下列語法：

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>支援新的 ASP.NET Web Pages Helper 方法

新的 ASP.NET Web Pages 技術包含一組協助程式方法，適用于將常用的功能新增至視圖和控制器。 ASP.NET MVC 3 支援在控制器和瀏覽器中使用這些協助程式方法（適當時）。 這些方法包含在 System.web. helper 元件中。 下表列出幾個 ASP.NET Web Pages helper 方法。

| **輔助** | **說明** |
| --- | --- |
| 圖表 | 呈現視圖中的圖表。 包含 ToWebImage、Chart、Save 和 Chart 之類的方法。 |
| Ipp | 會使用雜湊演算法來建立適當的 salted 和雜湊密碼。 |
| WebGrid | 將物件的集合（通常是資料庫的資料）當做方格呈現。 支援分頁和排序。 |
| WebImage | 呈現影像。 |
| WebMail | 傳送電子郵件訊息。 |

列出協助程式和基本語法的快速參考主題可在 ASP.NET Razor 語法檔中取得，網址為下列 URL：

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>其他相依性插入支援

目前的版本是以 ASP.NET MVC 3 Preview 1 版本為基礎，其中包括新增了兩項新服務和四個現有服務的支援，並改善了對相依性解析和一般服務定位器的支援。

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>用於微調控制器具現化的新 IControllerActivator 介面

新的 IControllerActivator 介面可讓您更精細地控制透過相依性插入來具現化控制器的方式。 下列範例顯示介面：

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

這與控制器 factory 的角色相反。 控制器 factory 是 IControllerFactory 介面的實作為，負責尋找控制器類型，以及具現化該控制器類型的實例。

控制器啟動程式只負責具現化控制器類型的實例。 它們不會執行控制器類型查閱。 找出適當的控制器類型之後，控制器 factory 應委派給 IControllerActivator 的實例，以處理控制器的實際具現化。

DefaultControllerFactory 類別具有接受 IControllerFactory 實例的新函式。 這可讓您套用相依性插入，以管理控制器建立的這個層面，而不需要覆寫預設的控制器類型查閱行為。

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>IServiceLocator 介面已取代為 IDependencyResolver

根據社區的意見反應，ASP.NET MVC 3 Beta 版已將 IServiceLocator 介面的使用取代為 ASP.NET MVC 需求特有的簡式 IDependencyResolver 介面。 下列範例顯示新的介面：

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

做為這項變更的一部分，ServiceLocator 類別也會取代為 DependencyResolver 類別。 相依性解析程式的註冊類似于舊版的 ASP.NET MVC：

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

此介面的執行應直接委派至基礎相依性插入容器，以提供所要求類型的已註冊服務。

當沒有所要求類型的已註冊服務時，ASP.NET MVC 會預期此介面的執行會從 GetService 傳回 null，並從 GetServices 傳回空集合。

新的 DependencyResolver 類別可讓您註冊用來執行新 IDependencyResolver 介面或泛型服務定位器介面（IServiceLocator）的類別。 如需有關一般服務定位器的詳細資訊，請參閱[GitHub 上的 CommonServiceLocator](https://github.com/unitycontainer/commonservicelocator)。

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>微調視圖頁面具現化的新 IViewActivator 介面

新的 IViewPageActivator 介面可讓您更精細地控制透過相依性插入來具現化視圖頁面的方式。 這同時適用于 WebFormView 實例和 RazorView 實例。 下列範例顯示新的介面：

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

這些類別現在接受 IViewPageActivator 的函式引數，可讓您使用相依性插入來控制 ViewPage、ViewUserControl 和 WebViewPage 類型的具現化方式。

#### <a name="new-dependency-resolver-support-for-existing-services"></a>現有服務的新相依性解析程式支援

新版本包含下列服務的相依性解析支援：

- 模型驗證提供者。 執行 ModelValidatorProvider 的類別可以在相依性解析程式中註冊，而且系統會使用它們來支援用戶端和伺服器端驗證。
- 模型中繼資料提供者。 實 ModelMetadataProvider 的單一類別可以在相依性解析程式中註冊，而且系統會使用它來提供範本化和驗證系統的中繼資料。
- 值提供者。 實 ValueProviderFactory 的類別可以在相依性解析程式中註冊，而且系統會使用它們來建立控制器和模型系結期間所使用的值提供者。
- 模型系結器。 實 IModelBinderProvider 的類別可以在相依性解析程式中註冊，而且系統會使用它們來建立模型系結系統所使用的模型系結器。

### <a id="0.1__Toc274034221"></a>不顯眼的 jQuery 型 Ajax 的新支援

ASP.NET MVC 包含 Ajax helper 方法，如下所示：

- Ajax Html.actionlink
- Ajax. RouteLink
- Ajax. Html.beginform
- Ajax.BeginRouteForm

這些方法會使用 JavaScript 在伺服器上叫用動作方法，而不是使用完整回傳。 這項功能已更新為以不顯眼的方式利用 jQuery。 這些 helper 方法會使用*data ajax*前置詞發出 HTML5 屬性，而不是發出內嵌用戶端腳本干擾。 然後藉由參考適當的 JavaScript 檔案，將行為套用至標記。 請確定已參考下列 JavaScript 檔案：

- jquery-1.7.2.min.js 1.4.1 .js
- jquery. 不顯眼的 .js

在 ASP.NET MVC 3 新專案範本的 web.config 檔案中，預設會啟用這項功能，但現有專案預設會停用。 如需詳細資訊，請參閱本檔稍後的[針對用戶端驗證和不顯眼的 JavaScript 新增應用程式範圍的旗標](#0.1_AddedApplicationWideFlagsForClientValida)。

### <a id="0.1__Toc274034222"></a>不顯眼 jQuery 驗證的新支援

根據預設，ASP.NET MVC 3 Beta 會以不顯眼的方式使用 jQuery 驗證，來執行用戶端驗證。 若要啟用不顯眼的用戶端驗證，請從視圖內部進行呼叫，如下所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

這會要求 ViewCoNtext. UnobtrusiveJavaScriptEnabled 屬性設定為 true，您可以藉由進行下列呼叫來執行此動作：

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

此外，請確定已參考下列 JavaScript 檔案。

- jquery-1.7.2.min.js 1.4.1 .js
- jquery. validate .js
- jquery. validate. 不顯眼的 .js

在 ASP.NET MVC 3 新專案範本的 web.config 檔案中，預設會啟用這項功能，但現有專案預設會停用。 如需詳細資訊，請參閱本檔稍後的[適用于用戶端驗證的新應用程式範圍旗標和不顯眼的 JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) 。

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>適用于用戶端驗證和不顯眼 JavaScript 的新全應用程式旗標

您可以使用 HtmlHelper 類別的靜態成員，全域啟用或停用用戶端驗證和不顯眼的 JavaScript，如下列範例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

預設的專案範本預設會啟用不顯眼的 JavaScript。 您也可以使用下列設定，在應用程式的根 Web.config 檔案中啟用或停用這些功能：

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

因為根據預設，您可以啟用這些功能，所以新的多載會引進 HtmlHelper 類別，讓您覆寫預設設定，如下列範例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

為了回溯相容性，預設會停用這兩項功能。

### <a id="0.1__Toc274034224"></a>新支援在 Views 執行之前執行的程式碼

您現在可以將名為 \_viewstart 的檔案（或 \_viewstart）放在 Views 目錄中，並將程式碼新增至該目錄及其子目錄中的多個視圖之間共用。 例如，您可能會將下列程式碼放入 ~/Views 資料夾中的 \_viewstart. cshtml 頁面：

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

這會以遞迴方式設定 Views 資料夾及其所有子資料夾中每個視圖的版面配置頁。 當正在呈現視圖時，\_viewstart 中的程式碼會在視圖程式碼執行之前執行。 \_viewstart 的程式碼會套用到該資料夾中的每個視圖。

根據預設，\_viewstart 檔案中的程式碼也適用于任何子資料夾中的 views。 不過，個別的子資料夾可以有自己的 \_viewstart 檔版本;在此情況下，會優先使用本機版本。 例如，若要執行 HomeController 的所有視圖通用的程式碼，請在 ~/Views/Home 資料夾中放入 \_viewstart. cshtml 檔案。

### <a id="0.1__Toc274034225"></a>VBHTML Razor 語法的新支援

先前的 ASP.NET MVC preview 包含使用以 Razor 語法為基礎的視圖C#支援。 這些視圖會使用. # 副檔名。 為支援 Razor 的持續性工作，ASP.NET MVC 3 Beta 引進了使用. vbhtml 副檔名之 Visual Basic 中 Razor 語法的支援。

如需在 VBHTML 頁面中使用 Visual Basic 語法的簡介，請參閱下列 URL 的教學課程：

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>更精細地控制 Validateinputattribute 套用

ASP.NET MVC 一律包含 Validateinputattribute 套用類別，它會叫用核心 ASP.NET 要求驗證基礎結構，以確保連入要求不會包含可能的惡意輸入。 根據預設，會啟用輸入驗證。 您可以使用 Validateinputattribute 套用屬性來停用要求驗證，如下列範例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

不過，許多 web 應用程式都有個別的表單欄位，需要允許 HTML，而其餘欄位則不應該。 Validateinputattribute 套用類別現在可讓您指定不應包含在要求驗證中的欄位清單。

例如，如果您正在開發 blog engine，您可能會想要在 [內文] 和 [摘要] 欄位中允許標記。 這些欄位可能會以兩個 input 元素表示，每個專案都有一個對應至屬性名稱（「本文」和「摘要」）的名稱屬性。 若只要停用這些欄位的要求驗證，請在 ValidateInput 類別的 Exclude 屬性中指定名稱（以逗號分隔），如下列範例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>協助程式將底線轉換為使用匿名物件指定之 HTML 屬性名稱的連字號

Helper 方法可讓您使用匿名物件指定屬性名稱/值組，如下列範例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

這種方法不會讓您在屬性名稱中使用連字號，因為 ASP.NET 中的屬性名稱不能使用連字號。 不過，連字號對自訂 HTML5 屬性而言很重要;例如，HTML5 會使用 "data-" 前置詞。

同時，底線無法用於 HTML 中的屬性名稱，但是在屬性名稱中是有效的。 因此，如果您使用匿名物件指定屬性，而且如果屬性名稱包含底線，則 helper 方法會將底線轉換為連字號。 例如，下列 helper 語法會使用底線：

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

上一個範例會在 helper 執行時呈現下列標記：

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>Bug 修正

EditorFor 和 DisplayFor 範本協助程式的預設物件範本現在支援 DisplayAttribute. Order 屬性中所指定的順序。 （在舊版中，不會使用訂單設定）。

用戶端驗證現在支援驗證已套用驗證屬性的已覆寫屬性。

JsonValueProviderFactory 現在預設為已註冊。

## <a id="0.1__Toc274034229"></a>重大變更

例外狀況篩選準則的執行順序已針對具有相同順序值的例外狀況篩選準則進行變更。 在 ASP.NET MVC 2 （含）以前版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其順序與動作方法上的相同。 這通常是未使用指定的順序值來套用例外狀況篩選時的情況。 在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。 如同在舊版中，如果已明確指定 Order 屬性，則會以指定的循序執行篩選。

## <a id="0.1__Toc274034230"></a> 已知問題

在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。

Razor views 沒有 IntelliSense 支援或語法反白顯示。 預期 Visual Studio 中的 Razor 語法支援將會納入為較新版本的一部分。

當您編輯 Razor 視圖（CSHTML 檔案）時，Visual Studio 中<a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a>的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。

使用 @model 語法來指定強型別 CSHTML 視圖時，無法辨識類型的語言特定快捷方式。 例如，@model int 將無法使用，但 @model Int32 會生效。 這個 bug 的因應措施是在您指定模型類型時，使用實際的類型名稱。

使用 @model 語法來指定強型別 CSHTML 視圖（或 @ModelType 指定強型別 VBHTML 視圖）時，不支援可為 null 的類型和陣列宣告。 例如，@model int？不受支援。 請改用 `@model Nullable<Int32>`。 也不支援 @model string [] 語法;請改用 `@model IList<string>`。

當您將 ASP.NET MVC 2 專案升級為 ASP.NET MVC 3 時，請務必將下列內容新增至 web.config 檔案的 appSettings 區段：

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

有一個已知的問題會導致表單驗證一律將未驗證的使用者重新導向至 ~/Account/Login，而忽略 Web.config 中使用的表單驗證設定。解決方法是新增下列應用程式設定。

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>免責聲明

© 2011 Microsoft Corporation. 著作權所有，並保留一切權利。 這份文件係依「現狀」提供。 本文件中提供的資訊與畫面 (包括 URL 及其他網際網路網站參考資料) 如有變更，恕不另行通知。 貴用戶須自行承擔使用風險。

本文件不提供　貴用戶任何 Microsoft 產品之智慧財產權的法定權利。 您可以複製並使用這份文件，供內部參考之用。
