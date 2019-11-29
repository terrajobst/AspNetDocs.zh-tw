---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 版本資訊的 ASP.NET 和 Web 工具 |Microsoft Docs
author: microsoft
description: 本檔說明 Visual Studio 2013 的 ASP.NET 和 Web 工具版本。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600443"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>適用於 Visual Studio 2013 的 ASP.NET 和 Web 工具版本資訊

由[Microsoft](https://github.com/microsoft)

> 本檔說明 Visual Studio 2013 的 ASP.NET 和 Web 工具版本。

## <a name="contents"></a>內容

- [安裝注意事項](#TOC1)
- [文件 (英文)](#TOC2)
- [軟體需求](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 ASP.NET 和 Web 工具的新功能

- [一個 ASP.NET](#TOC6)
- [新的 Web 專案體驗](#newproj)
- [ASP.NET 的樣板](#scaffold)
- [瀏覽器連結](#browser-link)
- [Visual Studio Web 編輯器增強功能](#web-editor)
- [Visual Studio 中的 Azure App Service Web Apps 支援](#waws)
- [Web 發行增強功能](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web Forms](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Microsoft OWIN 元件](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET 應用程式暫停](#TOC15)
- [已知問題和重大變更](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>安裝注意事項

Visual Studio 2013 的 ASP.NET 和 Web 工具會配套在主要安裝程式中，而且可以在[這裡](https://www.asp.net/downloads)下載。

<a id="TOC2"></a>
## <a name="documentation"></a>Documentation

有關 Visual Studio 2013 ASP.NET 和 Web 工具的教學課程和其他資訊可從[ASP.NET 網站](https://www.asp.net/)取得。

<a id="TOC4"></a>
## <a name="software-requirements"></a>軟體需求

ASP.NET 和 Web 工具需要 Visual Studio 2013。

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 ASP.NET 和 Web 工具的新功能

下列各節說明版本中引進的功能。

<a id="TOC6"></a>
## <a name="one-aspnet"></a>一個 ASP.NET

隨著 Visual Studio 2013 的發行，我們採取了整合使用 ASP.NET 技術的經驗，讓您可以輕鬆地混搭並比對您想要的。 例如，您可以使用 MVC 啟動專案，並在稍後輕鬆地將 Web form 頁面加入至專案，或在 Web Forms 專案中 scaffold Web Api。 其中一個 ASP.NET 是讓您以開發人員更輕鬆的方式來執行您在 ASP.NET 中所喜愛的專案。 無論您選擇哪一種技術，都可以放心地在一個 ASP.NET 的受信任基礎架構上打造。

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>新的 Web 專案體驗

我們已增強在 Visual Studio 2013 中建立新 Web 專案的體驗。 在 [**新增 ASP.NET Web 專案**] 對話方塊中，您可以選取所需的專案類型、設定任何技術組合（web FORM、MVC、Web API）、設定驗證選項，以及加入單元測試專案。

![新增 ASP.NET 專案](release-notes/_static/image1.png)

新的對話方塊可讓您變更許多範本的預設驗證選項。 例如，當您建立 ASP.NET Web Forms 專案時，您可以選取下列任何選項：

- 無驗證
- 個別使用者帳戶（ASP.NET 成員資格或社交提供者登入）
- 組織帳戶（在網際網路應用程式中 Active Directory）
- Windows 驗證（在內部網路應用程式中 Active Directory）

![驗證選項](release-notes/_static/image2.png)

如需建立 Web 專案之新進程的詳細資訊，請參閱[在 Visual Studio 2013 中建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。 如需新驗證選項的詳細資訊，請參閱本檔稍後的[ASP.NET Identity](#TOC8) 。

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET 的樣板

ASP.NET 樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。 它可讓您輕鬆地將未定案程式碼加入至您的專案，以與資料模型互動。

在舊版的 Visual Studio 中，架構僅限於 ASP.NET MVC 專案。 使用 Visual Studio 2013，您現在可以使用任何 ASP.NET 專案的樣板，包括 Web Forms。 Visual Studio 2013 目前不支援產生 Web form 專案的頁面，但您仍然可以將 MVC 相依性新增至專案，以使用具有 Web form 的樣板。 在未來的更新中，將會新增針對 Web form 產生網頁的支援。

使用 [樣板] 時，我們會確保專案中已安裝所有必要的相依性。 例如，如果您從 ASP.NET Web form 專案開始，然後使用樣板來新增 Web API 控制器，則會自動將所需的 NuGet 套件和參考新增至您的專案。

若要將 MVC 樣板加入至 Web form 專案，請加入**新的 Scaffold 專案**，然後在交談視窗中選取 [ **MVC 5**相依性]。 有兩個適用于樣板 MVC 的選項;最小和完整。 如果您選取 [最低]，則只會將 ASP.NET MVC 的 NuGet 套件和參考新增至您的專案。 如果您選取 [完整] 選項，則會加入最少的相依性，以及 MVC 專案所需的內容檔案。

支援架構的非同步控制器會使用 Entity Framework 6 的新異步功能。

如需詳細資訊和教學課程，請參閱 ASP.NET 架構的[總覽](aspnet-scaffolding-overview.md)。

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>瀏覽器連結-瀏覽器和 Visual Studio 之間的 SignalR 通道

新的[瀏覽器連結](using-browser-link.md)功能可讓您將多個瀏覽器連接到 Visual Studio，然後按一下工具列中的按鈕，將它們全部重新整理。 您可以將多個瀏覽器連接到您的開發網站，包括行動模擬器，然後按一下 [重新整理]，同時重新整理所有的瀏覽器。 瀏覽器連結也會公開 API，讓開發人員能夠撰寫瀏覽器連結延伸模組。

![](release-notes/_static/image3.png)

藉由讓開發人員充分利用瀏覽器連結 API，您就可以建立非常先進的案例，以跨越 Visual Studio 和任何連線的瀏覽器之間的界限。 Web Essentials 利用 API 來建立 Visual Studio 與瀏覽器開發人員工具之間的整合式體驗，以及遠端控制行動模擬器和其他許多功能。

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web 編輯器增強功能

Visual Studio 2013 在 web 應用程式中包含 Razor 檔案和 HTML 檔案的新 HTML 編輯器。 新的 HTML 編輯器提供以 HTML5 為基礎的單一整合架構。 它具有自動大括弧完成、jQuery UI 和 AngularJS 屬性 IntelliSense、屬性 IntelliSense 群組、識別碼和類別名稱 Intellisense，以及其他改良功能，包括更好的效能、格式設定和智慧標籤。

下列螢幕擷取畫面示範如何在 HTML 編輯器中使用啟動程式屬性 IntelliSense。

![HTML 編輯器中的 Intellisense](release-notes/_static/image4.png)

Visual Studio 2013 也隨附內建的 CoffeeScript 和 LESS 編輯器。 較少的編輯器隨附 CSS 編輯器中的所有酷炫功能，而且具有特定的 Intellisense 可用於變數，並在 @import 鏈中的所有較少檔之間 mixin。

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio 中的 Azure App Service Web Apps 支援

在使用 Azure SDK for .NET 2.2 Visual Studio 2013 中，您可以使用**伺服器總管**直接與您的遠端 web 應用程式互動。 您可以登入您的 Azure 帳戶、建立新的 web 應用程式、設定應用程式、查看即時記錄等等。 在 SDK 2.2 發行後即將推出，您將能夠在 Azure 中從遠端執行于 [調試] 模式。 當您安裝目前版本的 Azure SDK for .NET 時，Azure App Service Web Apps 的大部分新功能也可在 Visual Studio 2012 中使用。

如需詳細資訊，請參閱下列資源：

- [在 Azure App Service 中建立 ASP.NET web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web 發行增強功能

Visual Studio 2013 包含新的和增強的 Web 發佈功能。 以下是其中幾個：

- 輕鬆地[自動化 web.config 檔案加密](https://go.microsoft.com/fwlink/?LinkId=325529)。 （這個連結和下列兩個重點，是 MSDN 上的檔，在10/17 年的第一天之後可能無法使用）。
- 輕鬆地[在部署期間自動讓應用程式離線](https://go.microsoft.com/fwlink/?LinkId=325530)。
- 將 Web Deploy 設定為使用檔案總和檢查碼，[而不是上次變更日期](https://go.microsoft.com/fwlink/?LinkId=325531)，以判斷哪些檔案應該複製到伺服器。
- 當您使用 FTP 或檔案系統發行方法以及 Web Deploy 時，可以快速發行個別選取的檔案（包括 web.config）。

如需 ASP.NET web 部署的詳細資訊，請參閱[ASP.NET 網站](https://go.microsoft.com/fwlink/?LinkId=322027)。

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包含一組豐富的新功能，在[NuGet 2.7 版本](http://docs.nuget.org/docs/release-notes/nuget-2.7)資訊中有詳細的說明。

此版本的 NuGet 也不需要為 NuGet 的套件還原功能提供明確同意，即可下載套件。 您現在可以透過安裝 NuGet 來授與同意（以及 NuGet 的 [喜好設定] 對話方塊中關聯的核取方塊）。 套件還原現在只會在預設情況下運作。

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Form

### <a name="one-aspnet"></a>一個 ASP.NET

Web Forms 專案範本會與新的 ASP.NET 體驗緊密整合。 您可以將 MVC 和 Web API 支援新增至您的 Web form 專案，而且可以使用一個 ASP.NET 專案建立嚮導來設定驗證。 如需詳細資訊，請參閱[在 Visual Studio 2013 中建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。

### <a name="aspnet-identity"></a>ASP.NET Identity

Web Forms 專案範本支援新的 ASP.NET Identity 架構。 此外，範本現在支援建立 Web Forms 內部網路專案。 如需詳細資訊，請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案**中的[驗證方法](creating-web-projects-in-visual-studio.md#auth)。

### <a name="bootstrap"></a>從中

Web form 範本會使用[啟動](http://twitter.github.io/bootstrap/)程式，提供您可以輕鬆自訂的精緻且快速的外觀與風格。 如需詳細資訊，請參閱[Visual Studio 2013 Web 專案範本中的啟動](creating-web-projects-in-visual-studio.md#bootstrap)程式。

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>一個 ASP.NET

Web MVC 專案範本會與新的 ASP.NET 體驗緊密整合。 您可以自訂 MVC 專案，並使用一個 ASP.NET 專案建立嚮導來設定驗證。 如需 ASP.NET MVC 5 的簡介教學課程，請參閱[使用 ASP.NET MVC 5 的消費者入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。

如需將 MVC 4 專案升級為 MVC 5 的資訊，請參閱[如何將 ASP.NET mvc 4 和 WEB Api 專案升級至 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。

### <a name="aspnet-identity"></a>ASP.NET Identity

MVC 專案範本已更新為使用 ASP.NET Identity 進行驗證和身分識別管理。 如需 Facebook 和 Google 驗證的教學課程和新的成員資格 API，請參閱[使用 facebook 和 Google OAuth2 和 OpenID 登入建立 ASP.NET mvc 5 應用](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)程式和[使用驗證和 SQL DB 建立 ASP.NET mvc 應用程式並部署至 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。

### <a name="bootstrap"></a>從中

MVC 專案範本已更新為使用[啟動](http://getbootstrap.com/)程式來提供精緻且快速的外觀與風格，讓您可以輕鬆地進行自訂。 如需詳細資訊，請參閱[Visual Studio 2013 Web 專案範本中的啟動](creating-web-projects-in-visual-studio.md#bootstrap)程式。

### <a name="authentication-filters"></a>驗證篩選

驗證篩選是 ASP.NET MVC 中的一種新篩選準則，會在 ASP.NET MVC 管線的授權篩選準則之前執行，並可讓您針對所有控制器指定每個動作的驗證邏輯、每個控制器或全域。 驗證篩選準則會處理要求中的認證，並提供對應的主體。 驗證篩選也可以新增驗證挑戰，以回應未經授權的要求。

### <a name="filter-overrides"></a>篩選覆寫

您現在可以藉由指定覆寫篩選準則，覆寫哪些篩選準則會套用至指定的動作方法或控制器。 覆寫篩選指定一組不應針對指定範圍（動作或控制器）執行的篩選類型。 這可讓您設定全域套用的篩選準則，但會排除特定的全域篩選，使其不會套用至特定動作或控制器。

### <a name="attribute-routing"></a>屬性路由

ASP.NET MVC 現在支援屬性路由，感謝 Tim McCall 的貢獻（ [http://attributerouting.net](http://attributerouting.net)的作者）。 您可以使用屬性路由來指定您的路由，方法是標注動作和控制器。

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>屬性路由

ASP.NET Web API 現在支援屬性路由，感謝 Tim McCall 的貢獻， [http://attributerouting.net](http://attributerouting.net)的作者。 透過屬性路由，您可以藉由對動作和控制器加上批註來指定 Web API 路由，如下所示：

[!code-csharp[Main](release-notes/samples/sample1.cs)]

屬性路由可讓您更充分掌控 Web API 中的 Uri。 例如，您可以使用單一 API 控制器輕鬆地定義資源階層：

[!code-csharp[Main](release-notes/samples/sample2.cs)]

屬性路由也提供便利的語法來指定選擇性參數、預設值和路由條件約束：

[!code-csharp[Main](release-notes/samples/sample3.cs)]

如需屬性路由的詳細資訊，請參閱[WEB API 2 中的屬性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。

### <a name="oauth-20"></a>OAuth 2。0

Web API 和單一頁面應用程式專案範本現在支援使用 OAuth 2.0 的授權。 OAuth 2.0 是一種架構，可授權用戶端存取受保護的資源。 它適用于各種用戶端，包括瀏覽器和行動裝置。

OAuth 2.0 的支援是以 Microsoft OWIN 元件提供的新安全性中介軟體為基礎，用於持有人驗證和執行授權伺服器角色。 或者，您也可以使用組織授權伺服器（例如 Windows Server 2012 R2 中的 Azure Active Directory 或 ADFS）來授權用戶端。

### <a name="odata-improvements"></a>OData 改善

**支援 $select、$expand、$batch 和 $value**

ASP.NET Web API OData 現在具有 $select、$expand 和 $value 的完整支援。 您也可以使用 $batch 進行變更集的要求批次處理和處理。

[$Select] 和 [$expand] 選項可讓您變更從 OData 端點傳回的資料圖形。 如需詳細資訊，請參閱[WEB API OData 中的 $select 和 $expand 支援簡介](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。

**改良的擴充性**

OData 格式器現在可以擴充。 您可以新增 Atom 專案中繼資料、支援命名的資料流程和媒體連結專案、加入實例注釋，以及自訂產生連結的方式。

**不支援類型**

您現在可以建立 OData 服務，而不需要為您的實體類型定義 CLR 類型。 相反地，您的 OData 控制器可以接受或傳回**IEdmObject**的實例，這是 odata 格式器序列化/還原序列化。

**重複使用現有的模型**

如果您已經有現有的 entity data model （EDM），您現在可以直接重複使用它，而不需要建立一個新的。 例如，如果您使用 Entity Framework，您可以使用 EF 為您建立的 EDM。

### <a name="request-batching"></a>要求批次處理

要求批次處理會將多個作業結合成單一 HTTP POST 要求，以減少網路流量，並提供更流暢、較不多對話的使用者介面。 ASP.NET Web API 現在支援數個要求批次處理策略：

- 使用 OData 服務的 $batch 端點。
- 將多個要求封裝成單一 MIME 多部分要求。
- 使用自訂的批次處理格式。

若要啟用要求批次處理，只需將具有批次處理處理常式的路由新增至您的 Web API 設定：

[!code-csharp[Main](release-notes/samples/sample4.cs)]

您也可以控制要求或依序或循序執行。

### <a name="portable-aspnet-web-api-client"></a>可攜 ASP.NET Web API 用戶端

您現在可以使用 ASP.NET Web API 用戶端來建立可在您的 Windows Store 和 Windows Phone 8 應用程式之間工作的便攜類別庫。 您也可以建立可在用戶端和伺服器之間共用的便攜格式器。

### <a name="improved-testability"></a>改良的可測試性

Web API 2 可讓您更輕鬆地對 API 控制器進行單元測試。 只要使用您的要求訊息和設定來具現化您的 API 控制器，然後呼叫您想要測試的動作方法。 針對執行連結產生的動作方法，也很容易模擬**UrlHelper**類別。

### <a name="ihttpactionresult"></a>應傳回 iHTTPactionresult

您現在可以執行應傳回 iHTTPactionresult 來封裝 Web API 動作方法的結果。 ASP.NET Web API 執行時間會執行從 Web API 動作方法傳回的應傳回 iHTTPactionresult，以產生結果回應訊息。 您可以從任何 Web API 動作傳回應傳回 iHTTPactionresult，以簡化 Web API 執行的單元測試。 為了方便起見，會提供一些現成的應傳回 iHTTPactionresult 實作為，包括傳回特定狀態碼、格式化內容或內容協商回應的結果。

### <a name="httprequestcontext"></a>HttpRequestCoNtext

新的**HttpRequestCoNtext**會追蹤系結至要求但不會立即從要求取得的任何狀態。 例如，您可以使用**HttpRequestCoNtext**來取得路由資料、與要求相關聯的主體、用戶端憑證、 **UrlHelper**和虛擬路徑根。 您可以輕鬆地為單元測試目的建立**HttpRequestCoNtext** 。

由於要求的主體會與要求進行流動，而不是依賴**thread.currentprincipal**，因此主體現在會在要求的存留期內提供，同時位於 Web API 管線中。

### <a name="cors"></a>CORS

感謝 Brock Allen 的另一個絕佳貢獻，ASP.NET 現在完全支援跨原始來源要求共用（CORS）。

瀏覽器安全性可防止網頁對另一個網域發出 AJAX 要求。 [CORS](http://www.w3.org/TR/cors/)是一種 W3C 標準，可讓伺服器放寬相同的原始原則。 使用 CORS，伺服器可以明確允許某些跨原始來源要求，同時拒絕其他要求。

Web API 2 現在支援 CORS，包括自動處理預檢要求。 如需詳細資訊，請參閱[在 ASP.NET Web API 中啟用跨原始來源要求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。

### <a name="authentication-filters"></a>驗證篩選

驗證篩選是 ASP.NET Web API 中的一種新篩選準則，會在 ASP.NET Web API 管線中的授權篩選準則之前執行，並可讓您針對所有控制器指定驗證邏輯的每一動作、每個控制器或全域。 驗證篩選準則會處理要求中的認證，並提供對應的主體。 驗證篩選也可以新增驗證挑戰，以回應未經授權的要求。

### <a name="filter-overrides"></a>篩選覆寫

您現在可以藉由指定覆寫篩選準則，覆寫哪些篩選準則會套用至指定的動作方法或控制器。 覆寫篩選指定一組不應針對指定範圍（動作或控制器）執行的篩選類型。 這可讓您新增全域篩選器，但從特定動作或控制器中排除部分。

### <a name="owin-integration"></a>OWIN 整合

ASP.NET Web API 現在完全支援 OWIN，而且可以在任何具有 OWIN 功能的主機上執行。 此外，也包含可與 OWIN authentication 系統整合的**HostAuthenticationFilter** 。

透過 OWIN 整合，您可以在自己的進程中自我裝載 Web API，以及其他 OWIN 中介軟體，例如 SignalR。 如需詳細資訊，請參閱[使用 OWIN 至自我裝載 ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2。0

下列各節說明 SignalR 2.0 的功能。

- [以 OWIN 為基礎](#builtonowin)
- [MapHubs 和 MapConnection 現在已 MapSignalR](#MapSignalR)
- [跨網域支援](#crossdomain)
- [透過 MonoTouch 和 MonoDroid 的 iOS 和 Android 支援](#mobile)
- [可移植的 .NET 用戶端](#portable)
- [新的自我裝載套件](#selfhost)
- [與舊版相容的伺服器支援](#backwardcompat)
- [已移除 .NET 4.0 的伺服器支援](#remove40)
- [將訊息傳送至用戶端和群組的清單](#messagelist)
- [將訊息傳送給特定使用者](#sendtouser)
- [更好的錯誤處理支援](#errorhandling)
- [簡化中樞的單元測試](#unittesting)
- [JavaScript 錯誤處理](#javascripterror)

如需如何將現有1.x 專案升級至 SignalR 2.0 的範例，請參閱[升級 SignalR 1.X 專案](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>以 OWIN 為基礎

SignalR 2.0 完全建置於[OWIN （適用于 .net 的開放式 Web 介面）](http://owin.org/)。 這項變更讓 SignalR 的設定程式在 web 裝載和自我裝載的 SignalR 應用程式之間更加一致，但也需要一些 API 變更。

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs 和 MapConnection 現在已 MapSignalR

為了與 OWIN 標準相容，這些方法已重新命名為 `MapSignalR`。 不含參數的 `MapSignalR` 呼叫將會對應所有中樞（如1.x 版中的 `MapHubs`）;若要對應個別的**PersistentConnection**物件，請將連線類型指定為類型參數，並將連接的 URL 延伸模組指定為第一個引數。

在 Owin 啟動類別中呼叫 `MapSignalR` 方法。 Visual Studio 2013 包含 Owin 啟動類別的新範本;若要使用此範本，請執行下列動作：

1. 以滑鼠右鍵按一下專案
2. 選取 [**加入**]、[**新增專案**]
3. 選取 [ **Owin 啟動類別**]。 將新類別命名為**Startup.cs**。

在**web 應用程式中，** 包含 `MapSignalR` 方法的 Owin 啟動類別，接著會使用 web.config 檔案的 [應用程式設定] 節點中的專案新增至 Owin 的啟動程式，如下所示。

在自我裝載的**應用程式**中，啟動類別會當做 `WebApp.Start` 方法的型別參數傳遞。

**在 SignalR 1.x （從 web 應用程式中的全域應用程式檔）對應中樞和連接：** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**在 SignalR 2.0 （來自 Owin 啟動類別檔案）中對應中樞和連線：** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

在自我裝載的**應用程式**中，啟動類別會當做 `WebApp.Start` 方法的型別參數傳遞，如下所示。

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>跨網域支援

在 SignalR 1.x 中，跨網域要求是由單一 EnableCrossDomain 旗標所控制。 此旗標會同時控制 JSONP 和 CORS 要求。 為了提供更大的彈性，所有 CORS 支援都已從 SignalR 的伺服器元件中移除（如果偵測到瀏覽器支援，JavaScript 用戶端仍會正常使用 CORS），而且已提供新的 OWIN 中介軟體來支援這些案例。

在 SignalR 2.0 中，如果用戶端需要 JSONP （以支援舊版瀏覽器中的跨網域要求），則必須將 `HubConfiguration` 物件上的 `EnableJSONP` 設定為 `true`，以明確地啟用它，如下所示。 預設會停用 JSONP，因為它的安全性不如 CORS。

若要在 SignalR 2.0 中新增新的 CORS 中介軟體，請將 `Microsoft.Owin.Cors` 程式庫新增至您的專案，並在 SignalR 中介軟體之前呼叫 `UseCors`，如下一節所示。

**將 Owin 新增至您的專案**：若要安裝此程式庫，請在 [套件管理員主控台] 中執行下列命令：

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

此命令會將套件的2.0.0 版本新增至您的專案。

**呼叫 UseCors**

下列程式碼片段示範如何在 SignalR 1.x 和2.0 中執行跨網域連接。

**在 SignalR 1.x 中執行跨網域要求（從全域應用程式檔）**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**在 SignalR 2.0 （從程式C#代碼檔案）中執行跨網域要求**

下列程式碼示範如何在 SignalR 2.0 專案中啟用 CORS 或 JSONP。 這個程式碼範例會使用 `Map` 和 `RunSignalR`，而不是 `MapSignalR`，因此 CORS 中介軟體只會針對需要 CORS 支援的 SignalR 要求（而不是針對 `MapSignalR`中指定之路徑上的所有流量）執行。 `Map` 也可以用於需要針對特定 URL 首碼執行的任何其他中介軟體，而不是針對整個應用程式。

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>透過 MonoTouch 和 MonoDroid 的 iOS 和 Android 支援

已使用[Xamarin 程式庫](https://xamarin.com/)中的 MonoTouch 和 MonoDroid 元件，為 IOS 和 Android 用戶端新增了支援。 如需如何使用它們的詳細資訊，請參閱[使用 Xamarin 元件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。 當 SignalR RTW 版本可供使用時， [Xamarin 存放區](https://store.xamarin.com/)中將會提供這些元件。

<a id="portable"></a># # # 可移植 .NET 用戶端

為了更方便跨平臺開發，Silverlight、WinRT 和 Windows Phone 用戶端已由支援下列平臺的單一可移植 .NET 用戶端所取代：

- NET 4。5
- Silverlight 5
- WinRT （適用于 Windows Store 應用程式的 .NET）
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>新的自我裝載套件

現在有 NuGet 套件可讓您更輕鬆地開始使用 SignalR 自我裝載（SignalR 應用程式（裝載于進程或其他應用程式中），而不是裝載在 web 伺服器中。 若要升級以 SignalR 1.x 建立的自我裝載專案，請移除 SignalR. Owin 套件，然後新增 SignalR. SelfHost 套件。 如需有關如何開始使用自我裝載套件的詳細資訊，請參閱[教學課程： SignalR 自我裝載](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>與舊版相容的伺服器支援

在舊版的 SignalR 中，用戶端和伺服器中所使用的 SignalR 套件版本必須相同。 為了支援不容易更新的胖用戶端應用程式，SignalR 2.0 現在支援使用較舊的伺服器版本搭配舊版用戶端。 **注意： SignalR 2.0 不支援以較新版本的舊版用戶端建立的伺服器。**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>已移除 .NET 4.0 的伺服器支援

SignalR 2.0 已中斷與 .NET 4.0 的伺服器互通性支援。 .NET 4.5 必須與 SignalR 2.0 伺服器搭配使用。 SignalR 2.0 仍然有 .NET 4.0 用戶端。

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>將訊息傳送至用戶端和群組的清單

在 SignalR 2.0 中，您可以使用用戶端和群組識別碼的清單來傳送訊息。 下列程式碼片段示範如何執行這項操作。

**使用 PersistentConnection 將訊息傳送至用戶端和群組的清單**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**使用中樞將訊息傳送至用戶端和群組清單**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>將訊息傳送給特定使用者

這項功能可讓使用者透過新的介面 IUserIdProvider，指定 userId 是以 IRequest 為基礎：

**IUserIdProvider 介面**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

根據預設，會有一個使用使用者的 IPrincipal.Identity.Name 做為使用者名稱的執行。

在中樞中，您將能夠透過新的 API 將訊息傳送給這些使用者：

**使用用戶端 API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>更好的錯誤處理支援

使用者現在可以從任何中樞調用中擲回**HubException** 。 **HubException**的函式可以接受字串訊息和物件額外的錯誤資料。 SignalR 會自動將例外狀況序列化，並將它傳送至用戶端，以便用來拒絕/失敗中樞方法叫用。

[**顯示詳細的中樞例外**狀況] 設定與傳送回用戶端的**HubException**無關。一律會傳送。

**示範如何將 HubException 傳送至用戶端的伺服器端程式碼**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**示範回應從伺服器傳送之 HubException 的 JavaScript 用戶端程式代碼**

[!code-html[Main](release-notes/samples/sample16.html)]

**示範回應從伺服器傳送之 HubException 的 .NET 用戶端程式代碼**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>簡化中樞的單元測試

SignalR 2.0 包含一個在中樞上稱為 `IHubCallerConnectionContext` 的介面，可讓您更輕鬆地建立模擬用戶端調用。 下列程式碼片段示範如何將此介面與熱門的測試能力[xUnit.net](https://github.com/xunit/xunit)和[moq](https://code.google.com/p/moq/)搭配使用。

**使用 xUnit.net 的單元測試 SignalR**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**使用 moq 的單元測試 SignalR**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript 錯誤處理

在 SignalR 2.0 中，所有 JavaScript 錯誤處理回呼都會傳回 JavaScript 錯誤物件，而不是原始字串。 這可讓 SignalR 將更豐富的資訊傳遞給您的錯誤處理常式。 您可以從錯誤的 `source` 屬性取得內部例外狀況。

**處理 Start 的 JavaScript 用戶端程式代碼。 Fail 例外狀況**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>新的 ASP.NET 成員資格系統

ASP.NET Identity 是 ASP.NET 應用程式的新成員資格系統。 ASP.NET Identity 可讓您輕鬆地整合使用者特定的設定檔資料與應用程式資料。 ASP.NET Identity 也可讓您選擇應用程式中使用者設定檔的持續性模型。 您可以將資料儲存在 SQL Server 資料庫或另一個資料存放區中，包括 NoSQL 資料存放區（例如 Azure 儲存體資料表）。 如需詳細資訊，請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案**中的[個別使用者帳戶](creating-web-projects-in-visual-studio.md#indauth)。

### <a name="claims-based-authentication"></a>宣告架構驗證

ASP.NET 現在支援以宣告為基礎的驗證，其中使用者的身分識別會表示為來自受信任簽發者的一組宣告。 使用者可以使用在應用程式資料庫中維護的使用者名稱和密碼，或使用社交識別提供者（例如 Microsoft 帳戶、Facebook、Google、Twitter），或透過 Azure Active Directory 或使用組織帳戶來進行驗證。Active Directory 同盟服務（ADFS）。

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>與 Azure Active Directory 和 Windows Server Active Directory 整合

您現在可以建立使用 Azure Active Directory 或 Windows Server Active Directory （AD）進行驗證的 ASP.NET 專案。 如需詳細資訊，請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案**中的[組織帳戶](creating-web-projects-in-visual-studio.md#orgauth)。

### <a name="owin-integration"></a>OWIN 整合

ASP.NET authentication 現在是以 OWIN 中介軟體為基礎，可用於任何以 OWIN 為基礎的主機。 如需 OWIN 的詳細資訊，請參閱下列[MICROSOFT OWIN Components](#TOC7)一節。

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 元件

[Open Web Interface for .net](http://owin.org/) （OWIN）會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。 OWIN 會將 web 應用程式與伺服器分離，使 web 應用程式不受主機限制。 例如，您可以在 IIS 中裝載以 OWIN 為基礎的 web 應用程式，或在自訂進程中自我裝載它。

Microsoft OWIN 元件（也稱為 Katana 專案）中引進的變更包含新的伺服器和主機元件、新的協助程式程式庫和中介軟體，以及新的驗證中介軟體。

如需 OWIN 和 Katana 的詳細資訊，請參閱[OWIN 和 Katana 的新功能](../../../aspnet/overview/owin-and-katana/index.md)。

**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式無法在 IIS 傳統模式中執行;它們必須以整合模式執行。**

**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式必須以完全信任的方式執行。**

### <a name="new-servers-and-hosts"></a>新的伺服器和主機

在此版本中，新增了新的元件以啟用自我裝載案例。 這些元件包括下列 NuGet 套件：

- **Owin. HttpListener**。 提供使用**HttpListener**接聽 HTTP 要求並將其導向 OWIN 管線的 OWIN 伺服器。
- **Owin**為想要在自訂進程（例如主控台應用程式或 Windows 服務）中自我裝載 Owin 管線的開發人員提供程式庫。
- **OwinHost**。 提供獨立的可執行檔，可包裝 `Microsoft.Owin.Hosting`，並可讓您自行裝載 OWIN 管線，而不需要撰寫自訂主應用程式。

此外，`Microsoft.Owin.Host.SystemWeb` 封裝現在可讓中介軟體將提示提供給**SystemWeb**伺服器，表示應該在特定 ASP.NET 管線階段呼叫中介軟體。 這項功能特別適用于驗證中介軟體，這應該在 ASP.NET 管線早期執行。

### <a name="helper-libraries-and-middleware"></a>Helper 程式庫和中介軟體

雖然您只能使用 OWIN 規格中的函式和類型定義來撰寫 OWIN 元件，但新的 `Microsoft.Owin` 封裝會提供一組更好的抽象概念。 此套件將數個先前的套件（例如 `Owin.Extensions`、`Owin.Types`）結合成單一且結構良好的物件模型，讓其他 OWIN 元件可以輕鬆地使用它。 事實上，大部分的 Microsoft OWIN 元件現在都使用這個套件。

> [!NOTE]
> [OWIN](http://www.owin.org)應用程式無法在 IIS 傳統模式中執行;它們必須以整合模式執行。

> [!NOTE]
> [OWIN](http://www.owin.org)應用程式必須以完全信任的方式執行。

此版本也包含 Owin 診斷套件，其中包含用來驗證執行中 OWIN 應用程式的中介軟體，加上錯誤頁面中介軟體可協助調查失敗。

### <a name="authentication-components"></a>驗證元件

下列是可用的驗證元件。

- **Owin. 安全的 ActiveDirectory**。 使用內部部署或雲端式目錄服務來啟用驗證。
- **Owin**使用 cookie 啟用驗證。 此封裝先前已命名為 `Microsoft.Owin.Security.Forms`。
- **Owin**會使用 Facebook 的 OAuth 型服務來啟用驗證。
- **Owin**使用 Google 的 OpenID 型服務來進行驗證。
- **Owin**會使用 jwt 權杖來啟用驗證。
- **Owin. MicrosoftAccount**使用 microsoft 帳戶啟用驗證。
- **Owin. Security. OAuth**。 提供 OAuth 授權伺服器，以及用來驗證持有人權杖的中介軟體。
- **Owin**會使用 Twitter 的 OAuth 型服務來啟用驗證。

此版本也包含 `Microsoft.Owin.Cors` 封裝，其中包含用來處理跨原始來源 HTTP 要求的中介軟體。

> [!NOTE]
> Visual Studio 2013 的最終版本中已移除 JWT 簽署的支援。

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

如需 Entity Framework 6 中的新功能和其他變更清單，請參閱[Entity Framework 版本歷程記錄](https://msdn.com/data/jj574253)。

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3 包含下列新功能：

- 支援索引標籤編輯。 先前，使用 [保留索引標籤 **]** 選項時，Visual Studio 中的**格式檔**命令、自動縮排和自動格式化無法正常運作。 這種變更會更正 Razor 程式碼的 Visual Studio 格式，以進行索引標籤格式。
- 在產生連結時支援 URL 重寫規則。
- 移除安全性透明屬性。
  > [!NOTE]
  > 這是一種重大變更，使 Razor 3 與 MVC4 和更早版本不相容，而 Razor 2 則與 MVC5 或針對 MVC5 編譯的元件不相容。

從發行前版本的 Visual Studio 2013 中修正的 Razor 3 問題，可在[這裡](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到。

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET 應用程式暫停

ASP.NET 應用程式暫停是 .NET Framework 4.5.1 中的遊戲變更功能，它徹底改變了在單一電腦上裝載大量 ASP.NET 網站的使用者體驗和經濟模型。 如需詳細資訊，請參閱[ASP.NET 應用程式暫止–回應式共用 .net web 裝載](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

本節說明 Visual Studio 2013 的 ASP.NET 和 Web 工具中的已知問題和重大變更。

### <a name="nuget"></a>NuGet

- [使用 .sln 檔案時，新的套件還原無法在 Mono 上使用](https://nuget.codeplex.com/workitem/3596)–將在即將推出的 nuget.exe 下載和[Nuget. 命令列套件](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修正。
- [新的封裝還原不適用於 Wix 專案](https://nuget.codeplex.com/workitem/3598)–將在即將推出的 nuget.exe 下載和[Nuget. 命令列套件](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修正。
- [自動套件還原不適用於解決方案資料夾下的專案](https://nuget.codeplex.com/workitem/3625)–將在 NuGet 2.8 中修正。

### <a name="aspnet-web-api"></a>ASP.NET Web 應用程式開發介面

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)` 不會 `IQueryable<T>` 一律傳回，因為我們新增了 `$select` 和 `$expand`的支援。

    先前 `ODataQueryOptions<T>` 的範例一律會將 `ApplyTo` 的傳回值轉換至 `IQueryable<T>`。 這是稍早的作法，因為我們先前支援的查詢選項（`$filter`、`$orderby`、`$skip`、`$top`）並不會變更查詢的形狀。 現在，我們支援 `$select` 並 `$expand` 來自 `ApplyTo` 的傳回值一律不會 `IQueryable<T>`。

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    如果您使用稍早所述的範例程式碼，當用戶端未傳送 `$select` 和 `$expand`時，它會繼續運作。 不過，如果您想要支援 `$select` 和 `$expand` 則必須將該程式碼變更為此。

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **在批次要求期間，request. Url 或 RequestCoNtext 為 null**

    在批次處理案例中，從**Request**或**RequestCoNtext**存取時， **UrlHelper**是 null。

    這裡目前已追蹤此問題：[批次要求的 BatchRequestCoNtext 是 null](http://aspnetwebstack.codeplex.com/workitem/1301)。

    此問題的因應措施是建立**UrlHelper**的新實例，如下列範例所示：

    **建立 UrlHelper 的新實例**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. 使用 MVC5 和 OrgAuth 時，如果您有可執行 AntiForgerToken 驗證的視圖，當您將資料張貼到視圖時，可能會遇到下列錯誤：

    **錯誤**：

    *'/' 應用程式中發生伺服器錯誤。*

    <em>提供的 ClaimsIdentity 上沒有類型為 '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' 或 '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' 的宣告。若要啟用以宣告為基礎之驗證的防偽權杖支援，請確認已設定的宣告提供者在它所產生的 ClaimsIdentity 實例上提供這兩個宣告。如果設定的宣告提供者改為使用不同的宣告類型做為唯一識別碼，則可以藉由設定靜態屬性 AntiForgeryConfig 來進行設定。 UniqueClaimTypeIdentifier。</em>

    **因應措施**：

    在 global.asax 中加入下面這一行來修正它：

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    這會在下一版中修正。
2. 將 MVC4 應用程式升級至 MVC5 之後，請建立解決方案並加以啟動。 您應該會看到下列錯誤：

    為HostSection 無法轉換為 [B] System.web. HostSection....... i m。 類型 A 源自 ' System.webserver，Version = 2.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 '，其位置為 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ System.web. .dll ' 的內容 ' Default '。 類型 B 源自 ' System.webserver，Version = 3.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 '，位於位置 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01 \ System.web. ' 的內容 ' Default ' 中。

    若要修正上述錯誤，請在專案中開啟*所有*的 web.config 檔案（包括 Views 資料夾中的檔案），然後執行下列動作：

   1. 將 "4.0.0.0" 版本 "" 的所有出現專案更新為 "5.0.0.0"。
   2. 更新 "3.0.0.0" 版本中所有出現 "2.0.0.0" 的專案，&quot;System.web&quot; 和 &quot;System.webserver&quot; 至 ""。

      例如，在您進行上述變更之後，元件系結看起來應該像這樣：

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      如需將 MVC 4 專案升級為 MVC 5 的資訊，請參閱[如何將 ASP.NET mvc 4 和 WEB Api 專案升級至 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。
3. 當您使用用戶端驗證搭配 jQuery 不顯眼驗證時，驗證訊息有時不會對類型 = ' number ' 的 HTML 輸入元素進行錯誤。 輸入不正確數位（而不是正確的訊息必須有有效的數位）時，會顯示必要值的驗證錯誤（「需要年齡欄位」）。

    在建立和編輯檢視上具有整數屬性的模型的 scaffold 程式碼，通常會發現此問題。

    若要解決此問題，請將編輯器 helper 變更為：

    `@Html.EditorFor(person => person.Age)`

    收件者：

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 不再支援部分信任。 連結至 MVC 或 WebAPI 二進位檔的專案應該會移除[SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)屬性和[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)屬性。 移除這些屬性將會排除編譯器錯誤，如下所示。

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 請注意，這種情況的副作用是，您無法在同一個應用程式中使用4.0 和5.0 元件。 您必須將它們全部更新為5.0。

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>具有 Facebook 授權的 SPA 範本在網站裝載于內部網路區域時，可能會導致 IE 不穩定

SPA 範本提供使用 Facebook 的外部登入。 當使用範本建立的專案在本機執行時，登入可能會導致 IE 當機。

解決方案：

1. 在網際網路區域中主控網站;或

2. 在 IE 以外的瀏覽器中測試案例。

### <a name="web-forms-scaffolding"></a>Web Forms 樣板

Web form 樣板已從 VS2013 中移除，並將在未來的更新中提供 Visual Studio。 不過，您仍然可以在 Web form 專案中使用樣板，方法是新增 MVC 相依性並產生 MVC 的樣板。 您的專案將包含 Web Forms 和 MVC 的組合。

若要將 MVC 加入至您的 Web form 專案，請加入新的 scaffold 專案，然後選取 [ **MVC 5**相依性]。 根據您是否需要所有內容檔案（例如腳本），選取 [最小] 或 [完整]。 然後，為 MVC 新增 scaffold 專案，這會在專案中建立視圖和控制器。

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 和 Web API 架構-HTTP 404，找不到錯誤

如果將 scaffold 專案新增至專案時遇到錯誤，您的專案可能會處於不一致的狀態。 所做的部分變更會復原，但其他變更（例如已安裝的 NuGet 套件）將不會復原。 如果復原路由設定變更，使用者在流覽至 scaffold 專案時，會收到 HTTP 404 錯誤。

因應措施：

- 若要修正 MVC 的這個錯誤，請加入新的 scaffold 專案，然後選取 [MVC 5 相依性] （最小或完整）。 此程式會將所有必要的變更新增至您的專案。
- 若要修正 Web API 的這個錯誤：

  1. 將 WebApiConfig 類別新增至您的專案。

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 依照下列方式，在 WebApiConfig 中註冊應用程式\_Start 方法：

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
