---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET Web Pages （Razor）常見問題 |Microsoft Docs
author: Rick-Anderson
description: 本文列出一些有關 ASP.NET Web Pages （Razor）和 WebMatrix 的常見問題。 教學課程中使用的軟體版本 ASP.NET Web Pages （R 。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640928"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET Web Pages (Razor) 常見問題集

由[Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > 不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。 使用[Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[Visual Studio Code](https://code.visualstudio.com/)。
>
> 本文列出一些有關 ASP.NET Web Pages （Razor）和 WebMatrix 的常見問題。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2、WebMatrix 2 和 Visual Studio 2012。

- [ASP.NET Web Pages、ASP.NET Web form 和 ASP.NET MVC 之間有何差異？](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [我需要 WebMatrix 才能使用網頁嗎？](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [我可以在網頁頁面上使用 ASP.NET Web Forms 控制項嗎？](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [我可以在不使用 WebMatrix 的情況下部署 ASP.NET Web Pages 網站嗎？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [我是否必須使用 WebSecurity helper 來支援登入？](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET Web Pages 支援 HTML5 嗎？](#Does_ASP.NET_Web_Pages_support_HTML5)
- [我可以搭配網頁使用 JavaScript 和 jQuery 嗎？](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [其他資源](#AdditionalResources)

如有關于錯誤和其他問題的問題，請參閱[ASP.NET Web Pages （Razor）疑難排解指南](https://go.microsoft.com/fwlink/?LinkId=253001)。

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET Web Pages、ASP.NET Web form 和 ASP.NET MVC 之間有何差異？

這三個都是建立動態 web 應用程式的 ASP.NET 技術：

- ASP.NET Web Pages 著重于將動態（伺服器端）程式碼和資料庫存取權新增至 HTML 網頁，並提供簡單和輕量語法的功能。
- ASP.NET Web Forms 是以頁面物件模型和傳統視窗類型控制項（按鈕、清單等）為基礎。 Web form 使用以事件為基礎的模型，熟悉以用戶端為基礎的（Windows form）開發工作。
- ASP.NET MVC 會實現 ASP.NET 的模型視圖控制器模式。 重點在於「關注點分離」（處理、資料和 UI 層）。

這三種架構完全受到支援，並繼續由 ASP.NET 小組開發。 一般而言，選擇要使用的架構取決於您的背景和 ASP.NET 體驗。

具體而言，ASP.NET Web Pages 的設計，是為了讓已經知道 HTML 的人能夠輕鬆地將伺服器處理新增至他們的網頁。 這是適用于學生、業餘人士、一般人對程式設計新手的絕佳選擇。 對於擁有 non-ASP.NET web 技術經驗的開發人員而言，這也是不錯的選擇。

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>我需要 WebMatrix 才能使用網頁嗎？

不會。 不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。 使用[Visual Studio](program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。

如果您不想要使用 Visual Studio 或 Visual Studio Code，您可以使用[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)個別安裝元件產品。 您需要下列產品：

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 （也會安裝 ASP.NET Web Pages framework）
- IIS Express （web 伺服器）
- Microsoft SQL Server Compact 4.0 （資料庫）

您可以使用文字編輯器來編輯*cshtml* （或*vbhtml*）頁面。

不使用工具管理 SQL Server Compact 資料庫（ *.sdf*檔案）會有點困難。 Visual Studio 用來管理 *.sdf*資料庫的 containds 工具。 您也可以在程式碼中執行 SQL 命令，以執行許多 SQL Server 管理工作。

若要在不使用整合式開發環境（IDE）的情況下測試*cshtml*頁面，您可以將它們部署到即時伺服器。 （請參閱[我可以部署 ASP.NET Web Pages 網站而不使用 WebMatrix 嗎？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)）

### <a name="running-iis-express-without-using-an-ide"></a>在不使用 IDE 的情況下執行 IIS Express

如果您在電腦上將 IIS Express 安裝為 web 伺服器，您可以使用它來測試頁面。 您可以從命令列執行 IIS Express，並將它與特定埠號碼產生關聯。 然後，當您在瀏覽器中要求*cshtml*檔案時，您可以指定該埠。

在 Windows 中，以系統管理員許可權開啟命令提示字元，並變更為*C:\Program Files\IIS Express。* （若是64位系統，請使用*C:\Program Files （x86） \IIS Express 資料夾）。* 然後，使用您網站的實際路徑輸入下列命令：

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

您可以使用其他進程尚未保留的任何埠號碼。 （1024以上的埠號碼通常是免費的）。針對 `path` 值，請使用 *. cshtml*檔案所在之網站資料夾的路徑。

執行此命令來設定 IIS Express 以提供您的頁面之後，您可以開啟瀏覽器並流覽至*cshtml*檔案。 使用如下所示的 URL：

`http://localhost:35896/default.cshtml`

如需 IIS Express 命令列選項的說明，請在命令列中輸入 `iisexpress.exe /?`。

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>我可以在網頁頁面上使用 ASP.NET Web Forms 控制項嗎？

不會。 Web form 控制項（如[CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)控制項、[驗證控制項](https://msdn.microsoft.com/library/bwd43d0x)和[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控制項）只適用于 web form 頁面（ *.aspx*檔案）。 這些控制項需要 Web Forms 頁面架構。

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>我可以在不使用 WebMatrix 的情況下部署 ASP.NET Web Pages 網站嗎？

可以。 您可以手動將網站檔案複製到伺服器（通常是使用 FTP）。 如果您執行手動複製，則也必須複製支援 SQL Server Compact 的檔案（資料庫）。 如需詳細資訊，請參閱在[不使用工具的情況下部署網頁應用程式](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)的 blog 專案。

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>我是否必須使用 WebSecurity helper 來支援登入？

不會。 屬於 ASP.NET Web Pages 一部分的 `SimpleMembership` 提供者就是其中一個選項。 也可以使用屬於 ASP.NET 一部分的安全性提供者（您可以在 Web form 中用來處理）。 例如，您可以在 ASP.NET Web Pages 中使用表單驗證，就像在 Web Forms 中一樣。 如需如何使用表單驗證的其中一個範例，Microsoft 支援服務請參閱[如何使用C#.Net 在 ASP.NET 應用程式中執行以表單為基礎的驗證](https://support.microsoft.com/kb/301240)一文。 若要下載簡單的範例，請參閱[ASP.NET 版本的 < 登入 &amp; 密碼](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)。

如需如何使用 Windows 驗證的相關資訊，請參閱[在 ASP.NET Web Pages 中使用 windows 驗證](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)的 blog 文章。

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET Web Pages 支援 HTML5 嗎？

可以。 您使用 ASP.NET Web Pages （ *. cshtml*或*vbhtml*頁面）建立的頁面基本上是 HTML 頁面，其中包含在伺服器上執行的程式碼，然後才呈現頁面。 只要使用者的瀏覽器支援 HTML5，您就可以使用 [ *cshtml* ] 或 [ *vbhtml* ] 頁面中的 html5 元素。

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>我可以搭配網頁使用 JavaScript 和 jQuery 嗎？

當然可以。 您使用 ASP.NET Web Pages （ *. cshtml*或*vbhtml*頁面）建立的頁面只是包含伺服器程式碼的 HTML 網頁。 因此，您可以在一般 HTML 網頁中使用 JavaScript 或 jQuery 來執行的任何動作，也可以在*cshtml*或*vbhtml*頁面中執行。

WebMatrix 中的**入門網站**範本包含許多 jQuery 程式庫。 如果您使用該範本建立網站，[*腳本*] 資料夾中會包含 jquery core 程式庫（*jquery-1.7.2.min.js 1.6.2）* 和 jquery 驗證的程式庫（*jquery. validate. 驗證 .js*等等）。

以下是一些會說明如何搭配 ASP.NET Web Pages 使用 jQuery 的方式的 blog 文章：

- 透過 Rachel Appel[將 jQuery 的使用方式新增至 ASP.NET Web Pages](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)
- [5 分鐘： WebMatrix + JQUERY UI + json + jquery 範本](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)By Jonas Eriksson
- Mike Brind 的[WebMatrix 和 JQuery 表單](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他資源

[ASP.NET Web Pages (Razor) 疑難排解指南](https://go.microsoft.com/fwlink/?LinkId=253001)

ASP.NET 網站上的[WebMatrix 和 ASP.NET Web Pages 論壇](https://forums.asp.net/1224.aspx/1?WebMatrix)
