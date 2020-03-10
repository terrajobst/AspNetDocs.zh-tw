---
uid: web-pages/readme/beta3
title: Web Matrix 和 ASP.NET Web Pages （Razor） Beta 3 版本讀我檔案 |Microsoft Docs
author: rick-anderson
description: Web Matrix 與 ASP.NET Web Pages (Razor) 搶鮮版 (Beta) 3 讀我檔案
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628895"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>Web Matrix 與 ASP.NET Web Pages (Razor) 搶鮮版 (Beta) 3 讀我檔案

> Web Matrix 與 ASP.NET Web Pages (Razor) 搶鮮版 (Beta) 3 讀我檔案

2010年11月9日

## <a name="contents"></a>內容

- [概觀](#Overview)
- [安裝](#Installation_Notes)
- [Beta 3 版本中的新功能、變更和已知問題](#Known_Issues)

    - [WebMatrix 安裝問題](#Known_Issues_Installation)
    - [ASP.NET Web Pages](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [安裝應用程式](#Known_Issues_Installing_Applications)
    - [發行應用程式](#Known_Issues_Publishing_Applications)
    - [其他問題](#Known_Issues_Other_Issues)
- [詳細資訊](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概觀

> Microsoft WebMatrix Beta 是免費的 網頁程式開發堆疊，會在幾分鐘內安裝。 它會將網頁伺服器與資料庫和程式設計架構整合，以便建立單一且整合的使用經驗。 您可以使用 WebMatrix 搶鮮版（Beta）來簡化撰寫程式碼、測試及發佈自己的 ASP.NET 或 PHP 網站的方式，或者您可以使用 WebMatrix Beta 版，使用熱門的開放原始碼應用程式（例如 DotNetNuke、Umbraco、WordPress 或 Joomla）來啟動新的網站。 WebMatrix 搶鮮版（Beta）使用的功能強大的 web 伺服器、資料庫引擎和架構環境，會在網際網路上執行您的網站，這使得從開發到生產環境的轉換順暢且順暢。

<a id="Installation_Notes"></a>

## <a name="installation"></a>安裝

> 若要安裝 WebMatrix Beta 3，請使用[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。 安裝 Web Platform Installer 之後，您就可以使用它來安裝 WebMatrix Beta 3。
> 
> 如果您在安裝期間遇到問題，請參閱[疑難排解 Microsoft Web Platform Installer 的問題](https://go.microsoft.com/fwlink/?LinkId=196212)。

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>發行應用程式的指示

> 請參閱[發行應用程式的逐步指示](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>新功能、變更、andKnown 問題

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix Beta 3 安裝

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>問題： WebMatrix 搶鮮版（Beta）3僅適用于支援 Microsoft .NET Framework 4 的平臺

> WebMatrix 搶鮮版（Beta）需要 .NET Framework 第4版。 在某些情況下，WebMatrix 搶鮮版（Beta）安裝程式可讓您嘗試在不屬於受支援設定集的平臺上安裝。 特別是，沒有 SP1 更新的 Windows Vista 可讓您開始安裝 WebMatrix Beta，但 .NET Framework 4 元件將會失敗，並封鎖您的安裝。
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

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>問題：如果安裝 Microsoft Visual Studio 2008 但未 Microsoft Visual Studio 2008 SP1，就無法安裝 WebMatrix Beta 3

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

本檔的這一節描述具有 Razor 語法之 ASP.NET Web Pages Beta 3 版本的新功能、變更和已知問題。

- [新功能](#NewFeatures)
- [變更](#Changes)
- [問題](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Beta 3 的新功能，適用于使用 Razor 語法的 ASP.NET Web Pages

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>New： ".Html" 方法會轉譯未編碼的標記

> 新的 `Html.Raw` 方法可讓您將 HTML 標籤呈現為標記，而不是轉譯編碼的輸出。 （根據預設，ASP.NET Razor 會先編碼字串，再進行轉譯）。語法為：
> 
> `Html.Raw(value)`
> 
> 下列範例顯示如何使用 `Html.Raw`：
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Beta 3 中使用 Razor 語法進行 ASP.NET Web Pages 的變更

#### <a name="change-hrefattribute-method-removed"></a>變更：已移除 "HrefAttribute" 方法

> 已移除 `WebPage` 類別的 `HrefAttribute` 方法。 此 helper 是用來編碼 Url 中的不安全字元。 已不再需要它，因為 ASP.NET Razor 會自動將字串編碼。 （使用新的 `Html.Raw` 方法來呈現未編碼的字串）。

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>變更：宣告式 "@helper" 協助程式的語法已變更

> 在 Beta 3 版本中，ASP.NET 會變更如何剖析使用 `@helper` 語法所建立的協助程式。 基本上，`@helper` 語法現在會剖析為程式碼區塊，而不是會剖析為可包含程式碼的標記區塊。 因此，helper 內的程式碼不需要括在 `@{ }` 區塊中。 相反地，helper 內的標記必須明確包含在 HTML 元素中，或 ASP.NET Razor `<text></text>` 標籤中。
> 
> 例如，下列 `@helper` 語法適用于 Beta 3 版：
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> 在 Beta 3 版本中，此協助程式必須變更，看起來如下列範例所示：
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> 請注意，已不再使用 helper 中初始程式碼周圍的 `@{ }` 字元。 這是因為根據預設，系統會將 helper 的內容視為程式碼區塊。 協助程式呈現標記，其開頭為開啟的 `<a>` 標記。 如果 helper 必須轉譯純文字或不含結束記號的標記（例如，`<meta>` 標記），則要轉譯的內容必須在 `<text></text>` 標記中。

#### <a name="change-webpagecontexthttpcontext-removed"></a>變更：已移除 "WebPageCoNtext"

> `WebPageContext.HttpContext` 屬性已經移除。 請改用 `HttpContext.Current`。 （`WebPageContext.HttpContext` 屬性只會包裝此內容）。

#### <a name="change-facebook-helper-moved-to-new-package"></a>變更： "Facebook" helper 已移至新套件

> `Facebook` helper 已移至*Facebook. helper*程式庫，其中包含 `Facebook` 協助程式和其他功能。 您必須將此程式庫安裝為個別套件，如 < 使用封裝管理員安裝協助程式[ASP.NET 網頁](https://go.microsoft.com/fwlink/?LinkId=202889)中的教學課程消費者入門中所述。

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>變更：成員資格、角色和安全性類型會移至新的元件

> 下列類型已移至 `WebMatrix.WebData` 元件：
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>變更：已將 "TagBuilder" 類別移至 System.web 元件

> `TagBuilde` r 類別已移至 System.web .dll 元件。 先前，這是在屬於 ASP.NET MVC 的元件中。 這項變更表示您不需要安裝 ASP.NET MVC，即可使用 `TagBuilder` 類別。
> 
> 不過，類別仍在 `System.Web.Mvc` 命名空間中。 若要使用 `TagBuilder` 類別（例如，在自訂的 ASP.NET Razor helper 中），您必須參考命名空間（例如，藉由將 `@using System.Web.Mvc` 新增至您的程式碼）。

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>變更：要求驗證語法已變更;已移除 "驗證" 類別

> 在 Beta 3 版本中，若要停用個別欄位或一組欄位的驗證，您可以呼叫 `Validation.Exclude` 方法，傳入要從驗證排除之欄位的名稱或名稱。 Beta 3 版本提供新的語法，以略過驗證。 搶鮮版（Beta）3中使用的 `Validation` 方法已經移除。
> 
> > [!NOTE]
> > 如果您未停用要求驗證，如果使用者嘗試上傳 HTML 標籤（例如，藉由在頁面上使用 rtf 編輯器），網站將會報告錯誤，例如*潛在危險的要求。從用戶端偵測到表單值*，而且不接受使用者輸入。 如果您停用要求驗證，則必須手動檢查使用者輸入，以確定它不包含可能有害的標記或腳本，其使用的是[Microsoft 反跨網站腳本程式庫 v4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)。
> 
> 
> 若要停用自動要求驗證，請呼叫 `Request.Unvalidated` 方法，將您想要略過要求驗證的欄位或其他 post 物件的名稱傳遞給它。 您可以使用這個方法，略過 `Form`、`QueryString`、`Cookies`和 `ServerVariables` 集合中任何專案的驗證。 下列範例示範如何使用 `Unvalidated` 方法：
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>使用 Razor 語法 ASP.NET Web Pages 的已知問題

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>問題：針對成員資格使用自訂使用者資料表時發生非預期的行為

> 若要初始化 ASP.NET Razor 網站的成員資格提供者，您可以呼叫 `WebSecurity.InitializeDatabaseConnection` 方法。 （在 WebMatrix 中，入門網站範本會在 *\_AppStart*中包含此方法的呼叫）。如果此方法的 `autoCreateTables` 參數設定為 true （預設會在入門網站範本中設定為 true），而且如果將無法辨識的資料表名稱傳遞給方法（第二個參數），則此方法不會擲回錯誤。 不過，它會自動產生資料表。
> 
> 如果您想要使用自訂使用者資料表來取得成員資格，但將錯誤的資料表名稱傳遞給 `WebSecurity.InitializeDatabaseConnection` 方法，這可能會是個問題。 因為如果您所指定的資料表不存在，此方法預設不會引發錯誤，而且因為它會改為建立新的資料表，所以應用程式可能會看似正常運作。 不過，相依於自訂使用者資料表 (以及資料表中的欄位) 的應用程式程式碼最後可能會失敗並發生非預期的錯誤。
> 
> **因應措施**  
> 請確定在 `InitializeDatabaseConnection` 方法中傳遞的名稱符合成員資格資料庫中的使用者設定檔資料表，或確認 `autoCreateTables` 參數設定為 false。

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>問題：「無法產生 SQL Server 的使用者執行個體」錯誤

> 如果 WebMatrix Web 應用程式使用了 SQL Server Express 而且正在 Windows 7 或 Windows Server 2008 R2 上執行 IIS 7.5，您可能會看見一則錯誤，表示 SQL Server 無法在執行階段中擷取使用者的本機應用程式路徑。
> 
> 因應措施確定用來執行應用程式的 Windows 帳戶（通常是 NETWORK SERVICE）擁有應用程式根資料夾和子資料夾（例如*應用程式\_資料*）的讀取/寫入權限。 如需詳細資訊，請參閱知識庫文章[SQL Server Express 使用者實例和 ASP.net Web 應用程式專案的問題](https://support.microsoft.com/kb/2002980)。

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>問題：在 Visual Studio 中，不會自動匯入自訂群組件（Dll）的命名空間

> 如果您在 Visual Studio 的專案中使用自訂群組件，則這些元件中宣告的命名空間不會在設計階段自動匯入。 因此，在設計階段可能無法辨識自訂類型的參考，並在 Visual Studio 中將其標示為無法辨識（使用「波浪線」）。 這個問題只會發生在 Visual Studio 的設計階段;應用程式本身會正常執行。
> 
> **因應措施**  
> 包含 `using` 語句（Visual Basic 中的`imports`），其參考在設計階段無法辨識的實體。

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>問題：Visual Studio IntelliSense 和專案範本只能在 ASP.NET MVC 3 版中使用

> 安裝 ASP.NET Web Pages 不會一併安裝適用於 Visual Studio 的工具，例如適用於 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本。
> 
> 因應措施若要在 Visual Studio 中使用 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本，請透過 Web Platform Installer 或[獨立安裝程式](https://go.microsoft.com/fwlink/?LinkID=191797)來安裝 ASP.NET MVC 3 RC。

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>問題：「找不到&lt;helper&gt; 類別」錯誤

> 升級至 Beta 3 之後，您可能會看到錯誤，指出找不到 helper 類別（例如，`Facebook` 類別）。 從 Beta 2 開始並繼續 Beta 3，協助程式已移至您必須明確安裝的套件。 現有的網站不會升級為包含這些套件;這包括 [ *\My Documents\IISExpress* ] 或 [ *\My documents\ 我 Web sites* ] 資料夾中的網站。 特別的是，如果您在 [*我的網站*] （WebSite1）中使用預設網站（其中包含 `Twitter` helper 的參考），就會看到此錯誤。
> 
> **因應措施**  
> 將呼叫批註至網站中的任何協助程式，執行 [ *\_管理員*] 頁面，並安裝包含您要使用之 helper 的封裝。 安裝封裝之後，您可以取消批註參考 helper 的程式列。

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>問題：將搶鮮版（Beta 3） ASP.NET Razor 元件部署到 Bin 資料夾可能無法在主控網站上運作

> 如果您將 ASP.NET Web Pages 網站部署至主控網站，而且將 ASP.NET Razor Beta 3 元件部署到網站的*Bin*資料夾，您可能會遇到錯誤，包括下列各項：
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> 如果主控提供者已將 ASP.NET Web Pages Beta 1 元件安裝到伺服器的全域應用程式快取（GAC）中，就會發生這種情況。 GAC 中的元件優先于*Bin*資料夾中本機安裝的元件。
> 
> 因應措施請洽詢您的主控提供者，以確認您看到的錯誤是由提供者版本的元件與您的衝突所造成。 若是如此，請要求主控提供者補救伺服器 GAC 中的元件。

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>問題：經由 Proxy 伺服器讀取摘要或其他外部資料

> 如果執行網站的伺服器位於 proxy 伺服器後方，您可能需要*在 web.config 檔案*中設定 proxy 資訊，才能讀取來自網站外部的資訊。 例如，如果您使用 `ReCaptcha` 協助程式，則協助專家會與 reCAPTCHA 服務通訊，但您的 proxy 伺服器可能會封鎖它。 同樣地，用於 ASP.NET Web Pages 中的摘要 (例如封裝管理員所使用的摘要) 可能需要 Proxy 組態。
> 
> 如果您在使用外部服務或使用封裝摘要時遇到問題，請將下列元素放入應用程式*的根 web.config*檔案中：
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> 如需設定 proxy 伺服器的詳細資訊，請參閱 MSDN 網站上的[&lt;proxy&gt; 元素（網路設定）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>問題：「無法載入 Microsoft Web .dll .dll」錯誤

> 如果您先前已使用 Razor 語法安裝 Beta 1 版的 ASP.NET Web Pages，然後再安裝 Beta 3 版，則所有適當的元件都會安裝在 GAC 中，但不包括*Microsoft. Web. 基礎結構 .dll*。 因此，當您執行 ASP.NET Razor pages 時，您會看到錯誤訊息，*指出無法載入*[node.js]。
> 
> 如果您在乾淨的電腦上載入 Beta 3 版本，就不會發生此問題。
> 
> **因應措施**  
> 在 [控制台] 中，卸載 ASP.NET Web Pages。 然後重新安裝 Beta 3 版。

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>問題：解除安裝 .NET Framework 4 版就會停用含有 Razor 語法的 ASP.NET Web Pages

> 如果您解除安裝 .NET Framework 4 版，然後重新安裝它，就會停用含有 Razor 語法的 ASP.NET Web Pages。 具有 *. cshtml*副檔名的頁面無法正確執行。 ASP.NET Web Pages 在*電腦根目錄的 web.config 檔案*中註冊元件，移除 .NET Framework 會移除該檔案。 雖然重新安裝 .NET Framework 會安裝新版的組態檔，不過卻不會加入 ASP.NET Web Pages 組件的參考。
> 
> 因應措施重新安裝 .NET Framework 之後，請使用 Razor 語法重新安裝 ASP.NET Web Pages。 這會將下列專案新增至電腦根目錄*中的 web.config*檔案，此檔案通常位於下列位置：  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>問題：先前使用 Bin 資料夾中的 ASP.NET 元件部署的應用程式發生錯誤

> 在部署期間，ASP.NET Web Pages 元件（例如， *Microsoft. .dll*）的複本會複製到伺服器上網站的*Bin*資料夾中。 （這可能會在部署期間自動發生，或因為開發人員已明確複製元件）。不過，在安裝 Beta 3 版本時，會發生錯誤，例如找不到特定類型的錯誤。 這是因為在 Beta 3 版本中，有一些 ASP.NET Web Pages 類型已移至不同的命名空間。
> 
> 因應**措施 **  
> 清除已部署應用程式的*Bin*資料夾，將新的元件複製到資料夾（或重新部署應用程式），然後重新開機應用程式。

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
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>問題：在相同的應用程式中使用 Web 應用程式專案或 ASP.NET MVC 和 ASP.NET Web pages

> 如果您在 Web 應用程式專案或 ASP.NET MVC 應用程式中使用 ASP.NET Web Pages，您可能會看到*WebPageHttpApplication*找不到的錯誤。
> 
> **因應措施**  
> 如果您收到此錯誤，請變更應用程式衍生的基類。 在*global.asax*檔案中，變更下列程式程式碼：
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> 為此值：
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> 這實際上會反轉 ASP.NET Web Pages 的 Beta 1 版本所引進的變更與 Razor 語法。

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>問題：將應用程式部署到未安裝 SQL Server Compact 的電腦

> 包含 SQL Server Compact 資料庫的應用程式可以在未安裝 SQL Server Compact 的電腦上執行。 Microsoft WebMatrix Beta 3 會自動為您複製這些二進位檔，並執行適當的*web.config*檔案轉換。
> 
> 因應措施如果您需要複製這些檔案，並手動進行*web.config*檔案變更，請執行下列動作：
> 
> 1. 將資料庫引擎元件複製到目的電腦上應用程式的*Bin*資料夾（和子資料夾）： 
> 
>     - 將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*複製**到** *\bin*
>     - 將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* * 複製**到** *\Bin\x86*
>     - 將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * 複製**到** *\Bin\amd64*
> 2. 在網站的根資料夾中，建立或*開啟 web.config 檔案*。 （在 WebMatrix 搶鮮版（Beta 3）中，如果您在 [**選擇檔案類型**] 對話方塊中按一下 [**全部**]，則可以使用此檔案類型）。
> 3. 新增下列專案做為 **&lt;configuration&gt;** 專案的子系（而不是在 **&lt;system.web&gt;** 專案中）：
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>問題：資料庫和 WebGrid 協助程式在 Visual Basic 中的中度信任無法正常操作

> 如果您使用 Visual Basic （建立*vbhtml*檔案），則當應用程式設定為使用中度信任時，`Database` 和 `WebGrid` helper 將無法使用。
> 
> **因應措施**  
> 暫時將應用程式設定為使用完全信任。

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>問題：無法辨識「加密」屬性

> SQL Server Compact 4.0 無法辨識 `SqlCeConnection` 類別的 `Encrypt` 屬性。 您不應該使用這個屬性來加密資料庫檔案。 `Encrypt` 屬性在 SQL Server Compact 3.5 版本中已被取代，而且只為了回溯相容性而保留。 
> 
> **因應措施**  
> 使用 `SqlCeConnection` 類別的 `Encryption Mode` 屬性來加密 SQL Server Compact 4.0 資料庫檔案。 下列範例示範如何使用 `Encryption Mode` 屬性來建立加密的 SQL Server Compact 4.0 資料庫：
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> 若要變更現有 SQL Server Compact 4.0 資料庫的加密模式，請執行下列動作：
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> 若要加密未加密的 SQL Server Compact 4.0 資料庫，請執行下列動作：
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>問題：需要 Microsoft C++ Visual 2008 執行時間程式庫

> SQL Server Compact 4.0 的原生 Dll 需要 Microsoft Visual C++ 2008 執行時間程式庫（X86、IA64 和 X64） Service Pack 1。
> 
> **因應措施**  
> 安裝 .NET Framework 3.5 SP1。 這也會安裝 Visual C++ 2008 執行時間程式庫 SP1。 您可以從下列位置下載程式庫：   
>   
> [Microsoft Visual C++ 2008 Service Pack 1 可轉散發套件 ATL 安全性更新](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> 請注意，安裝 .NET Framework 2.0、3.0 或*4 並不*會安裝 Visual C++ 2008 執行時間程式庫 SP1。

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>問題：如果在電腦上安裝 .NET Framework 之前已安裝 SQL Server Compact，則其提供者不變名稱不會在 .NET Framework machine.config 檔案中註冊

> SQL Server Compact 可以安裝在未安裝 .NET Framework 的電腦上，因為 SQL Server Compact 需要 .NET Framework。 如果在安裝 SQL Server Compact 之前都未安裝 .NET Framework 版本3.5 或4，SQL Server Compact 安裝程式不會在*machine.config*檔案中註冊其提供者不變名稱。 依賴*machine.config*檔案中 SQL Server Compact 專案的任何應用程式都會失敗。 *Machine.config*中的非變異名稱註冊專案如下列範例所示：
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **因應措施**  
> 卸載 SQL Server Compact 4.0 CTP1。 從下列位置下載並安裝完整版的 .NET Framework：
> 
> [Microsoft .NET Framework 3.5 Service pack 1 （完整套件）](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft .NET Framework 4.0 版本（完整套件）](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> 然後重新安裝[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)。

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>安裝應用程式

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>問題：如果使用者的 [我的文件] 資料夾重新導向到網路共用，則安裝應用程式可能需要很長的時間

> **因應措施**  
> 無。 應用程式可能需要一些時間來安裝，但會正確安裝。

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>發行應用程式

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

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>其他問題

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>問題：在 [群組依據] 的報表中，搜尋/篩選無法運作：問題類型

> 當您執行網站的報表時，如果您在 [*依 URL 篩選*] 方塊中輸入文字，然後按一下 [*搜尋*]，就不會發生任何事。 這是因為當報表的 [*群組依據*] 狀態設定為 [*問題類型*] （預設值）時，此控制項無法正常運作。
> 
> 因應措施在功能區的 [*分組方式*] 索引標籤中，按一下 [ *URL* ]，依據專案的來源 URL 來分組專案。 在此狀態下，用來篩選項目的文字方塊和按鈕會有作用。

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>問題： WCF 應用程式無法使用 IIS Express 執行

> 流覽 WCF 應用程式會產生類似下列的錯誤：
> 
> *無法載入檔案或元件 ' 7.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 ' 或其相依性的其中之一。系統找不到指定的檔案。*
> 
> 之所以會發生這種情況，是因為 IIS Express 的 Beta 版預設不支援 WCF。
> 
> 因應措施使用下列任何一個因應措施（因應措施 #2 需要 Microsoft Windows Vista 或更高版本）：
> 
> 
> 1. 從 WebMatrix 安裝位置將*system.web*和*microsoft. web.config*元件複製到 WCF 應用程式的*bin*目錄。 根據預設，WebMatrix 會安裝在系統 [ *Program Files* ] 資料夾下的 [ *Microsoft WebMatrix* ] 子資料夾中。
> 2. 在 Microsoft Windows Vista 或更高版本上，使用下列命令建立*bin*目錄中元件的符號連結。 （這種方法的優點是它不會建立元件的複本）。
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. 在 GAC 中安裝這兩個元件。 從提高許可權的提示字元中，執行下列命令：
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>問題： WebMatrix Beta 3 無法執行某些需要提高許可權的工作

> WebMatrix Beta 3 無法執行需要提高許可權的特定工作，例如在下列情況下安裝其他元件：
> 
> - 在 Windows Vista 或 Windows 7 上，您使用不具有系統管理許可權的帳戶登入，且使用者帳戶控制（UAC）已停用。
> - 您使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。
> 
> **因應措施**  
> WebMatrix Beta 3 中的大部分工作都不需要系統管理許可權。 若是這樣做，您可以系統管理員身分執行作業，或遵循下列步驟進行操作：
> 
> - 在 Windows Vista 或 Windows 7 上，啟用 UAC。
> - 在 Windows XP 上，將使用者新增至 [系統管理員] 安全性群組。

#### <a name="issue-site-from-web-gallery-is-disabled"></a>問題：「Web 元件庫中的網站」已停用

> 如果未安裝 Web Platform Installer 3.0，則會停用 [**從 Web 元件庫中的網站**] 選項。
> 
> **因應措施**  
> 安裝[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>問題：在 Windows Server 2003 上，不會為非系統管理使用者啟動 IIS Express

> 在 Windows Server 2003 上，當您啟動頁面或開始 IIS Express 時，IIS Express 不會啟動。 若為網頁，則會顯示錯誤，指出應用程式已由非系統管理使用者啟動。
> 
> **因應措施**  
> 以系統管理使用者身分啟動 WebMatrix 搶鮮版（Beta 3）。 如需詳細資訊，請參閱下列知識庫文章：  
>   
> [非系統管理使用者所啟動的應用程式無法接聽在 Windows Vista、Windows Server 2003 或 Windows XP 中執行應用程式之電腦的 HTTP 流量。](https://support.microsoft.com/kb/939786)

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

#### <a name="issue-the-relationships-button-is-disabled"></a>問題： [關聯性] 按鈕已停用

> [**資料庫**] 工作區中 [**資料表**] 索引標籤下的 [**關聯**性] 按鈕會停用 SQL Server Compact 資料庫。
> 
> **因應措施**  
> 無。 SQL Server Compact 不支援資料表之間的關聯性。

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>問題：參數化 SQL 查詢會擲回例外狀況

> 在 SQL Server Compact 4.0 中，如果您未在參數化查詢中指定參數的資料類型（例如 `SqlDbType` 或 `DbType`），當查詢執行時，就會擲回例外狀況（exception）。
> 
> **因應措施**  
> 明確設定參數的資料類型，例如 `SqlDbType` 或 `DbType`。 這在 BLOB 資料類型（`image` 和 `ntext`）的情況下是不可或缺的。 使用如下所示的程式碼：
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a>取得更多資訊

如需 WebMatrix Beta 3 的詳細資訊，請參閱下列網站：

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

---

© 2010 Microsoft Corporation。 All Rights Reserved. [使用條款](https://msdn.microsoft.cos/cc300389.aspx)。
