---
uid: web-pages/readme/overview
title: WebMatrix 讀我檔案 |Microsoft Docs
author: rick-anderson
description: WebMatrix 和 ASP.NET Web Pages (Razor) 1.0 版讀我檔案
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563466"
---
# <a name="webmatrix-readme"></a>WebMatrix 讀我檔案

2011年1月13日

## <a name="contents"></a>內容

> [!NOTE]
> 此讀我檔案適用于1.0 版的 WebMatrix。

- [概觀](#Overview)
- [安裝](#Installation_Notes)
- [如何發行應用程式](#InstructionsForPublishingApplications)
- [變更和問題](#ChangesAndIssues)

    - [WebMatrix 1.0 安裝](#Known_Issues_Installation)
    - [ASP.NET Web Pages](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [安裝應用程式](#Known_Issues_Installing_Applications)
    - [發行應用程式](#Known_Issues_Publishing_Applications)
- [詳細資訊](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概觀

> Microsoft WebMatrix 1.0 是一套免費的網頁開發堆疊，只要幾分鐘即可安裝完成。 它會將網頁伺服器與資料庫和程式設計架構整合，以便建立單一且整合的使用經驗。 您可以使用 WebMatrix 來簡化編寫程式碼的方式，並且發行您自己的 ASP.NET 或 PHP 網站，也可以使用 WebMatrix 搭配常見的開放原始碼應用程式 (例如 DotNetNuke、Umbraco、WordPress 或 Joomla) 來啟動新的網站。 WebMatrix 所使用的網頁伺服器、資料庫引擎和架構環境都與您在網際網路上執行網站所使用的項目一樣功能強大，因此可讓您順利且流暢地從開發轉換至實際執行環境。

<a id="Installation_Notes"></a>

## <a name="installation"></a>安裝

> 若要安裝 WebMatrix 1.0，您必須先安裝[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。 安裝 Web Platform Installer 之後，您就可以使用它來安裝 WebMatrix。
> 
> 如果您在安裝期間遇到問題，請參閱[疑難排解 Microsoft Web Platform Installer 的問題](https://go.microsoft.com/fwlink/?LinkId=196212)。

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>如何發行應用程式

> 請參閱[發行應用程式的逐步指示](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>變更與問題

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1.0 安裝問題

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>問題：WebMatrix 1.0 只能在支援 Microsoft .NET Framework 4 的平台上使用

> .NET Framework 4 版是 WebMatrix 的必要元件。 在某些情況下，WebMatrix 1.0 安裝程式會讓您嘗試安裝在不屬於受支援組態集的平台上。 尤其，不包含 SP1 更新的 Windows Vista 會讓您開始安裝 WebMatrix，但是 .NET Framework 4 元件會失敗並封鎖安裝。
> 
> **因應措施**  
> 安裝在支援的平台上，包括：
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 (含) 以後版本
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>問題：如果已安裝 Microsoft Visual Studio 2008 但並未安裝 Microsoft Visual Studio 2008 SP1，就無法安裝 WebMatrix 1.0

> **因應措施**  
> 從 Microsoft 下載中心安裝[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 。

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>問題：SQL Server Compact 4.0 的某些組件不會安裝在 GAC 中

> 當您在 64 位元電腦上安裝 SQL Server Compact 4.0，而且該電腦只安裝了 .NET Framework 3.5 SP1 Client Profile 時，SQL Server Compact 4.0 的 Managed 組件就不會放置於全域組件快取 (GAC) 中。 不會安裝在 GAC 中的 Managed 組件包括：
> 
> - *System.data.sqlserverce .dll* （ADO.NET 提供者）
> - *System.data.sqlserverce. Entity* .dll （ADO.NET Entity Framework）
> 
> **因應措施**  
> 解除安裝 SQL Server Compact 4.0。 從下列位置下載並安裝 .NET Framework 3.5 SP1 完整版本：  
>   
> [Microsoft .NET Framework 3.5 Service pack 1 （完整套件）](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> 然後重新安裝 SQL Server Compact 4.0。

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>問題：無法使用命令列解除安裝 SQL Server Compact

> 在這個版本中，使用命令列選項解除安裝 SQL Server Compact 沒有作用。
> 
> **因應措施**  
> 使用 Windows [控制台] 中的 [*程式和功能*] 卸載 Microsoft SQL Server Compact 4.0。

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET Web Pages

本文件的這一節將描述含有 Razor 語法的 ASP.NET Web Pages 1.0 版的新功能、變更和已知問題。

- [新功能](#NewFeatures)
- [變更](#Changes)
- [問題](#Issues)

#### <a id="NewFeatures"></a>新功能

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>新增：加入了停用封裝管理員的組態設定

> *Web.config*檔案中的 `<appSettings>` 元素可以使用新的 `asp:AdminManagerEnabled` 金鑰，這可讓您完全停用封裝管理員。 這個專案的預設值為 true，這表示如果不包含*在 web.config 檔案*中，則會啟用封裝管理員。 若要停用封裝管理員，請將下列元素新增*至網站根目錄中的 web.config*檔案：
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>變更

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>變更："webPages:AdminFolderVirtualPath" 索引鍵已重新命名為 "asp:AdminFolderVirtualPath"

> 可以新增至*web.config*檔案以指定封裝管理員位置的 `webPages:AdminFolderVirtualPath` 金鑰已經重新命名為使用 `asp:` 命名空間，而不是 `webPages` 命名空間。 如果您已經使用此項目，就必須在組態檔中重新命名此項目。

#### <a id="Issues"></a> 已知問題

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>問題：無法再辨識成員資格使用者的密碼

> 用於建立和儲存成員資格 (登入) 密碼的演算法已經變更為更安全的演算法。 因此，系統無法辨識針對 ASP.NET Razor Beta 版中建立之成員 (使用者) 所儲存的密碼。 
> 
> 因應措施如果網站尚未進入生產環境，請從成員資格資料庫中移除使用者記錄。 如果資料庫已上線，請在成員資格資料庫中以程式設計方式重新產生現有的密碼。

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>問題：針對成員資格使用自訂使用者資料表時發生非預期的行為

> 若要初始化 ASP.NET Razor 網站的成員資格提供者，您可以呼叫 `WebSecurity.InitializeDatabaseConnection` 方法。 （在 WebMatrix 中，入門網站範本會在 *\_AppStart*中包含此方法的呼叫）。如果此方法的 `autoCreateTables` 參數設定為 true （預設會在入門網站範本中設定為 true），而且如果將無法辨識的資料表名稱傳遞給方法（第二個參數），則此方法不會擲回錯誤。 不過，它會自動產生資料表。
> 
> 如果您想要使用自訂使用者資料表來取得成員資格，但將錯誤的資料表名稱傳遞給 `WebSecurity.InitializeDatabaseConnection` 方法，這可能會是個問題。 因為如果您所指定的資料表不存在，此方法預設不會引發錯誤，而且因為它會改為建立新的資料表，所以應用程式可能會看似正常運作。 不過，相依於自訂使用者資料表 (以及資料表中的欄位) 的應用程式程式碼最後可能會失敗並發生非預期的錯誤。
> 
> **因應措施**  
> 請確定在 `InitializeDatabaseConnection` 方法中傳遞的名稱符合成員資格資料庫中的使用者設定檔資料表，或確認 `autoCreateTables` 參數設定為 false。

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a>問題：「系統管理模組需要存取 ~/App\_資料」錯誤訊息

> 在某些情況下，嘗試建立使用者或使用 ASP.NET 成員資格系統，可能會導致頁面顯示系統*管理模組需要存取 ~/App\_資料*的錯誤。 如果執行 IIS 或 IIS Express 的帳戶沒有建立和寫入網站根目錄下之*應用程式\_Data*資料夾的許可權，就會發生這種情況。 
> 
> 因應措施為網站手動建立 *\_Data 資料夾的應用程式*。 然後確定應用程式執行的 Windows 帳戶（通常是 NETWORK SERVICE）擁有應用程式根資料夾和子資料夾（例如應用程式\_資料）的讀取/寫入權限。 如需詳細資訊，請參閱知識庫文章[SQL Server Express 使用者實例和 ASP.net Web 應用程式專案的問題](https://support.microsoft.com/kb/2002980)。

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>問題：「無法產生 SQL Server 的使用者執行個體」錯誤

> 如果 WebMatrix Web 應用程式使用了 SQL Server Express 而且正在 Windows 7 或 Windows Server 2008 R2 上執行 IIS 7.5，您可能會看見一則錯誤，表示 SQL Server 無法在執行階段中擷取使用者的本機應用程式路徑。
> 
> 因應措施確定用來執行應用程式的 Windows 帳戶（通常是 NETWORK SERVICE）擁有應用程式根資料夾和子資料夾（例如*應用程式\_資料*）的讀取/寫入權限。 如需詳細資訊，請參閱知識庫文章[SQL Server Express 使用者實例和 ASP.net Web 應用程式專案的問題](https://support.microsoft.com/kb/2002980)。

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>問題：包含封裝管理員資源或封裝管理員密碼的檔案可在 IIS 6.0 和先前版本底下提供

> 如果您部署的是使用 RC2 版本建立的 ASP.NET Web Pages （Razor）應用程式，且應用程式在 */App\_Data/admin*底下包含*password .txt*或*packagesources* ，則 IIS 6.0 將會提供檔案（如有要求），可能會公開您的套件管理員實例的密碼。 
> 
> 因應措施將*密碼 .txt*或*packagesources*重新命名為*config.xml*或*packagesources*。根據預設，IIS 6.0 不會提供副檔名為 *.config*的檔案。 （在 IIS 7 中，應用程式中不會提供任何檔案 *\_Data*資料夾，因此您不需要重新命名檔案）。

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>問題：解除安裝使用 Beta 3 版本所安裝的封裝並未完全移除封裝元件

> 如果您使用 Beta 3 版本中的封裝管理員來安裝某個封裝，然後嘗試使用目前版本來解除安裝該封裝，就無法完全解除安裝該封裝。 使用套件管理員的 [**卸載**] 按鈕會移除部分元件，但會保留套件的程式庫程式碼，而且不會更新*package*檔案。
> 
> 因應**措施 **  
> 執行下列步驟：  
> 1. \_Data\packages 資料夾中刪除*應用程式*。 這會移除所有套件。   
> 2. 刪除網站根目錄中的*封裝 .config*檔案。

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>問題：在 Visual Studio 中，叫用 Web 架構封裝管理員會讓應用程式離線

> 如果您在 Visual Studio （非 WebMatrix）中工作，並使用 *\_系統管理員*功能啟動套件管理員，Visual Studio 會讓應用程式離線，並將應用程式 *\_離線*發佈到網站根目錄，這會破壞您使用封裝管理員的能力。
> 
> [!NOTE]
> 雖然您通常會在使用以 web 為基礎的套件管理員介面時看到這種行為，但如果您新增、移除或修改應用程式中的任何檔案 *\_Data*資料夾，就會發生相同的行為。
> 
> 因應**措施 **  
> 若要在 Visual Studio 中使用封裝，請使用 NuGet 延伸模組而非 Web 架構封裝管理員。 如需詳細資訊，請參閱[NuGet 檔](https://docs.microsoft.com/nuget/)。 如果您使用應用程式中的其他檔案 *\_Data*資料夾，請考慮將檔案保留在其他位置，以避免發生此問題。 如果不可行，請以手動方式刪除*應用程式\_離線的 .htm*檔案，或等到網站自動復原上線（預設為30秒之後）。

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>問題：Visual Studio IntelliSense 和專案範本只能在 ASP.NET MVC 3 版中使用

> 安裝 ASP.NET Web Pages 不會一併安裝適用於 Visual Studio 的工具，例如適用於 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本。
> 
> 因應措施若要在 Visual Studio 中使用 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本，請透過 Web Platform Installer 或[獨立安裝程式](https://go.microsoft.com/fwlink/?LinkID=191797)來安裝 ASP.NET MVC 3 RC。

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>問題：經由 Proxy 伺服器讀取摘要或其他外部資料

> 如果執行網站的伺服器位於 proxy 伺服器後方，您可能需要*在 web.config 檔案*中設定 proxy 資訊，才能讀取來自網站外部的資訊。 例如，如果您使用 `ReCaptcha` 協助程式，則協助專家會與 reCAPTCHA 服務通訊，但您的 proxy 伺服器可能會封鎖它。 同樣地，用於 ASP.NET Web Pages 中的摘要 (例如封裝管理員所使用的摘要) 可能需要 Proxy 組態。
> 
> 如果您在使用外部服務或使用封裝摘要時遇到問題，請將下列元素放入應用程式*的根 web.config*檔案中：
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> 如需設定 proxy 伺服器的詳細資訊，請參閱 MSDN 網站上的[&lt;proxy&gt; 元素（網路設定）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>問題：解除安裝 .NET Framework 4 版就會停用含有 Razor 語法的 ASP.NET Web Pages

> 如果您解除安裝 .NET Framework 4 版，然後重新安裝它，就會停用含有 Razor 語法的 ASP.NET Web Pages。 具有 *. cshtml*副檔名的頁面無法正確執行。 ASP.NET Web Pages 在*電腦根目錄的 web.config 檔案*中註冊元件，移除 .NET Framework 會移除該檔案。 雖然重新安裝 .NET Framework 會安裝新版的組態檔，不過卻不會加入 ASP.NET Web Pages 組件的參考。
> 
> 因應措施重新安裝 .NET Framework 之後，請使用 Razor 語法重新安裝 ASP.NET Web Pages。 這會將下列專案新增至電腦根目錄*中的 web.config*檔案，此檔案通常位於下列位置：  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5

> 在 IIS 7 或 IIS 7.5 上，URL 如下的要求找不到具有 *. cshtml*或*vbhtml*副檔名的頁面：  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> 因為 IIS 7 或 IIS 7.5 預設不會啟用 URL 重寫，所以會發生此問題。 原因案例是，當您使用 IIS Express 在本機進行測試時，不會看到問題，但是當您將網站部署至主控網站時，就會遇到此問題。
> 
> **因應措施**
> 
> - 如果您可以控制伺服器電腦，請在伺服器電腦上安裝更新中所述的更新，[讓特定 IIS 7.0 或 IIS 7.5 處理常式能夠處理其 url 不是以句號結尾的要求](https://support.microsoft.com/kb/980368)。
> - 如果您無法控制伺服器電腦（例如，您要部署至主控網站），請將下列*內容新增至網站的 web.config*檔案： 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>問題：將應用程式部署到未安裝 SQL Server Compact 的電腦

> 包含 SQL Server Compact 資料庫的應用程式可以在未安裝 SQL Server Compact 的電腦上執行。 Microsoft WebMatrix 1.0 會自動為您複製這些二進位檔，並執行適當的*web.config*檔案轉換。
> 
> 因應措施如果您需要複製這些檔案，並手動進行*web.config*檔案變更，請執行下列動作：
> 
> 1. 將資料庫引擎元件複製到目的電腦上應用程式的*Bin*資料夾（和子資料夾）：  
> 
>    - Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>      **至** *\bin*
>    - 將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* 複製**到** *\Bin\x86*
>    - 將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * 複製**到** *\Bin\amd64*
> 
> 2. 在網站的根資料夾中，建立或*開啟 web.config 檔案*。 （在 WebMatrix 1.0 中，如果您在 [**選擇檔案類型**] 對話方塊中按一下 [**全部**]，則可以使用此檔案類型）。
> 3. 新增下列專案做為 `<configuration>` 專案的子系（不在 `<system.web>` 元素內）：
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>問題：「資料庫」和「WebGrid」協助程式無法在 Visual Basic 的中度信任中使用

> 如果您使用 Visual Basic （建立*vbhtml*檔案），則當應用程式設定為使用中度信任時，`Database` 和 `WebGrid` helper 將無法使用。
> 
> **因應措施**  
> 如果您使用 Visual Studio 2010，您可以藉由安裝 Service Pack 1 版本來解決此問題。 在 SP1 版本的最終版本可供使用之前，您可以從 Microsoft 下載中心的[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en)版頁面下載 sp1 的搶鮮版（Beta）。   
>   
> 如果這不可行，或如果您未使用 Visual Studio 2010，您可以暫時將應用程式設定為使用完全信任。

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>問題：「ApplicationPart」資源可從外部存取

> 如果元件包含衍生自 `ApplicationPart` 類別的物件，則 `ResourceRouteHandler` 類別會公開該元件的資源。 例如，請考慮下列 URL：  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> 此要求會下載*system.web. system.web*元件中的所有資源字串。 會下載所有的內嵌資源（即使是不打算做為靜態內容的資源）。 如果內嵌資源包含敏感性資訊，這可能代表安全性風險。 
> 
> 因應**措施 **  
> 如果您建立**ApplicationPart**物件，請確定與該**ApplicationPart**物件的元件相關聯的內嵌資源不包含敏感性資訊。

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> 如需 WebMatrix 安裝問題的相關資訊，請參閱本檔稍早的[WebMatrix 安裝問題](#Known_Issues_Installation)。

檔的這一節說明 WebMatrix 開發環境的已知問題。

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>問題： web.config 檔案中資料庫連接字串的使用者名稱或密碼變更，不會反映在 [資料庫] 工作區中

> **因應措施**  
> 
> 1. 在 web.config*檔案*中，變更連接字串中的資料庫名稱（例如，在其中加上 "1"）。
> 2. 儲存 web.config*檔案*。
> 3. 按一下 [**資料庫**] 和 [重新整理]。
> 4. 將*web.config*檔案之連接字串中的資料庫名稱，變更回原始的資料庫名稱。
> 5. 儲存 web.config*檔案*。
> 6. 按一下 [**資料庫**] 和 [重新整理]。

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>問題：無法刪除 WebMatrix 所建立的資料夾

> 如果使用較高的許可權來執行 WebMatrix （也就是您使用 Windows 中的 [**以系統管理員身分執行**] 選項啟動 webmatrix），則無法使用 windows Explorer 刪除 webmatrix 所建立的資料夾。
> 
> **因應措施**  
> 使用較高的許可權執行 Windows Explorer。 請依照下列步驟：  
> 
> 1. 在 Windows 中，按一下 [**啟動**]。
> 2. 輸入 "Windows Explorer"，然後以滑鼠右鍵按一下 [ **Windows explorer**] 的專案。
> 3. 按一下 [**以系統管理員身分執行**]。 然後您就可以刪除資料夾。

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>問題： WebMatrix 1.0 無法執行需要提高許可權的特定工作

> WebMatrix 1.0 無法執行需要提高許可權的特定工作，例如在下列情況下安裝其他元件：
> 
> - 在 Windows Vista 或 Windows 7 上，您使用不具有系統管理許可權的帳戶登入，且使用者帳戶控制（UAC）已停用。
> - 您使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。
> 
> **因應措施**  
> WebMatrix 1.0 中大部分的工作都不需要系統管理許可權。 若是這樣做，您可以系統管理員身分執行作業，或遵循下列步驟進行操作：
> 
> - 在 Windows Vista 或 Windows 7 上，啟用 UAC。
> - 在 Windows XP 上，將使用者新增至 [系統管理員] 安全性群組。

#### <a name="issue-site-from-web-gallery-is-disabled"></a>問題：「Web 元件庫中的網站」已停用

> 如果未安裝 Web Platform Installer 3.0，則會停用 [**從 Web 元件庫中的網站**] 選項。
> 
> **因應措施**  
> 安裝[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>問題： Google Chrome 無法當做執行選項使用

> Google Chrome 不會顯示在 [**首頁**] 索引標籤上 [**執行**] 底下的瀏覽器清單中。
> 
> **因應措施**  
> 某些版本的 Google Chrome 不會正確地向 Windows 中的 [預設程式] 功能註冊自己。 因應措施是啟動 Google Chrome，按一下 [*自訂和控制 Google chrome* ] 功能表，按一下 [*選項*]，然後按一下 [*將 google Chrome 設為預設瀏覽器*]。

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>問題： [外鍵] 對話方塊不允許輸入主要金鑰

> [**外鍵**] 對話方塊不允許您從主鍵資料表輸入主要金鑰名稱。
> 
> **因應措施**  
> 這是故意的。 您不需要輸入主要索引鍵資料表的主鍵名稱。

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>問題： Razor 語法、 C#或的 WebMatrix 無法使用 IntelliSense Visual Basic

> HTML 和 CSS 的 WebMatrix 支援 IntelliSense。 不過，它不適用於其他語言。 
> 
> 因應**措施 **  
> 無。

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>問題： HTML 和 CSS 的 IntelliSense 建議不適合內容的元素

> WebMatrix 中標記的 IntelliSense 支援使用[XHTML 1.0 轉換架構](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)的 HTML，以及使用[css 2.1 架構](http://www.w3.org/TR/CSS2/)的 css。 由於 IntelliSense 是以這些特定的架構為基礎，因此可能會建議某些標記、屬性或屬性，而不適合目前的頁面或樣式定義。 若是 HTML，它也可能會導致內容中的未預期建議，可能會被視為格式不正確的 XHTML （例如，當標記未關閉時）。 如果插入點位於不完整的標記內，這個問題可能會更明顯;在此情況下，IntelliSense 可能會建議新的開頭標記，或提供其他不正確的建議。 
> 
> 因應**措施 **  
> 若是 HTML，請確定您是在格式正確的完整 XHTML 頁面中工作。 針對 CSS，沒有因應措施。

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>問題：當您輸入時，不會叫用 IntelliSense

> 有時，IntelliSense 可能不會在編輯器中輸入 HTML 或 CSS 時叫用。 特別是，當插入點是直接在另一個專案旁邊或在檔案結尾處時，就可能發生這種情況。 
> 
> 因應**措施 **  
> 請確定插入點周圍有空白字元，而且插入點不在檔案結尾。 您也可以按下 Ctrl + 空格鍵，手動叫用 IntelliSense。

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>問題：沒有可用來停用 IntelliSense 的 UI

> WebMatrix 1.0 不提供任何 UI 或手勢來停用 IntelliSense。 
> 
> 因應**措施 **  
> 使用下列命令啟動 WebMatrix，其中包括停用 IntelliSense 的交換器：  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express 有自己的讀我檔案，可在下列 URL 取得：

[https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact 有自己的讀我檔案，可在下列 URL 取得：

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

如需有關在 WebMatrix 中安裝 SQL Server Compact 之問題的詳細資訊，請參閱本檔稍早的[WebMatrix 安裝問題](#Known_Issues_Installation)。

### <a id="Known_Issues_Installing_Applications"></a>安裝應用程式

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>問題：如果使用者的 [我的文件] 資料夾重新導向到網路共用，則安裝應用程式可能需要很長的時間

> **因應措施**  
> 無。 應用程式可能需要一些時間來安裝，但會正確安裝。

### <a id="Known_Issues_Publishing_Applications"></a>發行應用程式

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>問題：發行 SQL Compact 資料庫時發生「無法取得必要許可權」錯誤

> WebMatrix 並不完全支援使用中度信任設定，將 SQL Server Compact 的支援二進位檔部署至執行 .NET Framework 3.5 版的伺服器。
> 
> **因應措施**  
> 慣用的解決方法是在伺服器上安裝 .NET Framework 4。 或者，執行下列動作：
> 
> 1. 將下列元素新增至*Web\_MediumTrust*中的 `SecurityClasses` 區段：
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. 在*Web\_MediumTrust*中，使用下列必要許可權建立新的許可權集合：
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. 將下列元素放在*Web\_MediumTrust*中，將許可權集合套用至 SQL Server Compact：
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>問題：資源庫和 PhpBB web 應用程式在發佈後顯示「服務無法使用」錯誤

> 在某些情況下，發行應用程式會導致「服務無法使用」錯誤。
> 
> **因應措施**  
> 在 WebMatrix 中，于 [**發佈設定**] 視窗中的伺服器名稱結尾新增反斜線（\)，然後再次發佈應用程式。

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>問題： Moodle 網站版面配置和連結在發佈之後中斷

> 在您發佈 Moodle 應用程式之後，應用程式無法正常運作。
> 
> **因應措施**  
> 在 WebMatrix 中，于 [**發佈設定**] 視窗中的 [**網站名稱**] 欄位結尾加上斜線（/），然後再次發佈應用程式。

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>問題：發行 nopCommerce 失敗，發生資料庫錯誤

> 發行 nopCommerce 失敗並報告資料庫錯誤，例如「插入 nop\_記錄資料表失敗。」
> 
> **因應措施**  
> 
> 1. 在 WebMatrix 中，按一下 [**執行**] 以在本機啟動 nopCommerce。
> 2. 登入 [系統管理] 頁面。
> 3. 按一下 [**系統**] 功能表。
> 4. 按一下 [**記錄**檔] 選項。
> 5. 按一下 [**清除記錄**] 按鈕。
> 6. 再次發佈 nopCommerce。

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>問題：當您下載已發佈的網站時，Silverstripe CMS 會顯示「HTTP 500 PHP HANDLER.FCGI 錯誤」

> **因應措施**  
> 按一下 [**下載發佈的網站**] 之後，請略過 [**發行預覽**] 中的 `silverstripe-cache/manifest_main`。 這個檔案是用於快取用途，而且是每部電腦特有的檔案。

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>問題：當您下載發佈的網站時，會顯示「在 '/' 應用程式中發生伺服器錯誤」的子集

> **因應措施**  
> 開啟網站的*web.config*檔案，並以 SQL Server 系統管理員認證（"sa" 認證）取代資料庫連接字串中的使用者識別碼和密碼。
> 
> 或者，請遵循下列步驟，將您使用 `db_owner` 許可權登入的使用者帳戶提供給您：
> 
> 1. 使用 Web Platform Installer 安裝 SQL Server Management Studio。
> 2. 連接到本機 SQL Server Express 實例（根據預設，`.\SQLEXPRESS`）。
> 3. 按一下 [資料庫 *] &gt; [LocalSubtextDatabase]* &gt;**安全性**&gt;**使用者**&gt; *[localSubtextUser*] （預設值為 `subtextuser`，按一下滑鼠右鍵，然後按一下 [**屬性**]。
> 4. 在 [角色成員資格] 區段中選取 [ **db\_擁有**者]。

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>問題：如果 [目的地 URL] 欄位未在前面加上 HTTP://或 HTTPs://，網站在發佈後可能無法正常執行

> 在 [**發行設定**] 對話方塊中，如果目的地 URL 不是以 `http://` 或 `https://`開頭，則在部署之後，網站可能無法運作。
> 
> **因應措施**  
> 在發佈網站之前，請確定 [**發行設定**] 對話方塊中的 [目的地 URL] 開頭為 [`http://`] 或 [`https://`]。

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>問題：發行 MySQL 資料庫失敗，錯誤為「無法發行資料庫。 如果遠端資料庫無法執行腳本，就會發生這種情況。」

> 發生此錯誤的原因有很多。 您可以看到此錯誤的其中一個原因是，資料庫腳本包含單引號字元（'），而目的地 MySQL 資料庫的預設字元集不是 UTF-8。
> 
> **因應措施**  
> 將遠端 MySQL 資料庫的預設字元集設定為 UTF-8。

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>問題：發佈或下載網站後，在 DotNetNuke 中看不到某些連結

> 如果您發佈或下載 DotNetNuke 網站，您可能需要清除快取，才能讓新連結出現在網站上。
> 
> **因應措施**
> 
> 1. 以「主機」的身分登入。
> 2. 移至 [主機] 功能表並選取 [**主機設定**]。
> 3. 在 [**高級設定**] 底下，展開 [**效能設定**]。
> 4. 按一下 [**清除**快取] 連結以取得頁面。
> 5. 移至頁面底部，然後重新開機應用程式。

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>問題： AtomSite 中的某些連結在您下載發佈的網站之後中斷

> **因應措施**  
> 在*app.config*檔案中，*使用者 .config*檔案和所有 *.XML*檔案中，將 URL 字串（例如，`http://myhost.com/atomsite`）取代為本機檔案（例如，`http://localhost:1239`）。

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>問題：以 MySQL 為基礎的應用程式（例如 WordPress）無法發佈和報告資料庫錯誤

> 根據預設，WebMatrix 會安裝具有 UTF-8 字元集的 MySQL。 如果您自行安裝 MySQL，而字元集不是 UTF-8 （例如，它是採用 latin1-general），則資料庫的發行進程可能會失敗。
> 
> **因應措施**
> 
> 1. 將 MySQL 的字元集設定為 UTF-8。 （如需詳細資訊，請參閱 MySQL 網站上的[伺服器字元集和定序](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)）。
> 2. 重新安裝應用程式。
> 3. 重新發佈應用程式。

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>問題：如果應用程式具有以瀏覽器為基礎的設定，「下載發佈的網站」會失敗

> 某些應用程式（例如 Kentico CMS）會要求您在瀏覽器中啟動它們，以便執行安裝後的設定，例如建立資料庫。 如果您發佈這類應用程式，但未完成以瀏覽器為基礎的安裝程式，則嘗試從遠端伺服器下載相同的網站將會失敗。
> 
> **因應措施**  
> 發行網站之前，請先完成以瀏覽器為基礎的安裝程式。

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>問題：「下載發佈的網站」失敗並出現資料庫錯誤，DotNetNuke 和 Kooboo CMS

> 如果您嘗試從伺服器下載應用程式，而且在 [**發行設定**] 對話方塊的資料庫連接字串中具有系統管理員認證，您可能會在發行記錄檔中看到下列錯誤：
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **因應措施**  
> 如果可行，請使用資料庫的非系統管理員認證重新發佈網站（或已發佈）。

<a id="More_Info"></a>

## <a name="for-more-information"></a>取得更多資訊

如需有關 WebMatrix 1.0 的詳細資訊，請參閱下列網站：

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. All Rights Reserved. [使用條款](https://msdn.microsoft.cos/cc300389.aspx)。
