---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
title: 使用 ELMAH 記錄錯誤的詳細資料（VB） |Microsoft Docs
author: rick-anderson
description: 錯誤記錄模組和處理常式（ELMAH）提供另一種方法來記錄生產環境中的執行階段錯誤。 ELMAH 是免費的開放原始碼錯誤 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: a5f0439f-18b2-4c89-96ab-75b02c616f46
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
msc.type: authoredcontent
ms.openlocfilehash: 46b7fc22807c8cb9f47ff035639815d7b6104735
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74622337"
---
# <a name="logging-error-details-with-elmah-vb"></a>使用 ELMAH 記錄錯誤的詳細資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_VB.zip)或[下載 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_vb.pdf)

> 錯誤記錄模組和處理常式（ELMAH）提供另一種方法來記錄生產環境中的執行階段錯誤。 ELMAH 是免費的開放原始碼錯誤記錄程式庫，其中包含錯誤篩選的功能，以及從網頁、RSS 摘要中查看錯誤記錄檔的能力，或是以逗號分隔的檔案形式下載。 本教學課程將逐步引導您下載及設定 ELMAH。

## <a name="introduction"></a>簡介

[先前的教學](logging-error-details-with-asp-net-health-monitoring-vb.md)課程已檢查過 ASP。NET 的健全狀況監視系統，提供現成的程式庫，可供您記錄各式各樣的 Web 事件。 許多開發人員會使用健康情況監控來記錄並傳送未處理之例外狀況的詳細資料。 不過，此系統有幾個痛苦點。 首先，最重要的是缺乏任何使用者介面來查看記錄事件的相關資訊。 如果您想要查看前10個錯誤的摘要，或查看上周發生之錯誤的詳細資料，您必須流覽資料庫、掃描您的電子郵件收件匣，或建立會顯示 `aspnet_WebEvent_Events` 資料表資訊的網頁。

另一個難題是以健全狀況監視的複雜性為中心。 因為健全狀況監視可用來記錄不同事件的眾多，而且因為有各種選項可指示記錄事件的方式和時間，所以正確設定健全狀況監視系統可能是一項繁重的工作。 最後，有相容性問題。 因為健康狀態監視是第一次新增至2.0 版的 .NET Framework，所以無法供使用 ASP.NET 1.x 版所建立的舊版 web 應用程式使用。 此外，我們在先前的教學課程中用來將錯誤詳細資料記錄到資料庫的 `SqlWebEventProvider` 類別，只適用于 Microsoft SQL Server 資料庫。 如果您需要將錯誤記錄到替代的資料存放區，例如 XML 檔案或 Oracle 資料庫，您必須建立自訂記錄提供者類別。

健全狀況監視系統的另一個替代方案是錯誤記錄模組和處理常式（ELMAH），這是[Atif Aziz](http://www.raboof.com/)所建立的免費開放原始碼錯誤記錄系統。 這兩個系統之間最明顯的差異在於 ELAMH 能夠從網頁和 RSS 摘要中顯示錯誤清單，以及特定錯誤的詳細資料。 ELMAH 比健全狀況監視更容易設定，因為它只會記錄錯誤。 此外，ELMAH 還支援 ASP.NET 1.x、ASP.NET 2.0 和 ASP.NET 3.5 應用程式，並隨附各種記錄來源提供者。

本教學課程會逐步解說將 ELMAH 新增至 ASP.NET 應用程式所牽涉到的步驟。 讓我們開始吧！

> [!NOTE]
> 健全狀況監視系統和 ELMAH 都有自己的一組優缺點。 我建議您同時嘗試這兩個系統，並決定哪一個最適合您的需求。

## <a name="adding-elmah-to-an-aspnet-web-application"></a>將 ELMAH 新增至 ASP.NET Web 應用程式

將 ELMAH 整合到新的或現有的 ASP.NET 應用程式中，是一個簡單且直接的程式，需要五分鐘的時間。 簡言之，它牽涉到四個簡單的步驟：

1. 下載 ELMAH 並將 `Elmah.dll` 元件新增至您的 web 應用程式。
2. 在 `Web.config`中註冊 ELMAH 的 HTTP 模組和處理常式。
3. 指定 ELMAH 的設定選項，以及
4. 如有需要，請建立錯誤記錄檔來源基礎結構。

讓我們逐一解說這四個步驟，一次一個。

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>步驟1：下載 ELMAH 專案檔案，並將`Elmah.dll`新增至您的 Web 應用程式

此教學課程提供的下載包含 ELMAH 1.0 BETA 3 （組建10617），這是撰寫本文時的最新版本。 或者，您可以流覽[ELMAH 網站](https://code.google.com/p/elmah/)以取得最新版本，或下載原始程式碼。 將 ELMAH 下載解壓縮到您桌面上的資料夾，並找出 ELMAH 元件檔（`Elmah.dll`）。

> [!NOTE]
> `Elmah.dll` 檔案位於下載的 `Bin` 資料夾中，其具有不同 .NET Framework 版本的子資料夾，以及發行和偵錯工具組建。 針對適當的架構版本使用發行組建。 例如，如果您要建立 ASP.NET 3.5 web 應用程式，請從 `Bin\net-3.5\Release` 資料夾複製 `Elmah.dll` 檔案。

接下來，開啟 Visual Studio 並將元件新增至您的專案，方法是以滑鼠右鍵按一下方案總管中的網站名稱，然後從內容功能表選擇 [加入參考]。 這會顯示 [加入參考] 對話方塊。 流覽至 [流覽] 索引標籤，然後選擇 [`Elmah.dll`] 檔案。 此動作會將 `Elmah.dll` 檔案加入至 web 應用程式的 `Bin` 資料夾。

> [!NOTE]
> Web 應用程式專案（WAP）類型不會顯示方案總管中的 [`Bin`] 資料夾。 相反地，它會在 [參考] 資料夾底下列出這些專案。

`Elmah.dll` 元件包含 ELMAH 系統所使用的類別。 這些類別可分為三個分類的其中一種：

- **Http 模組**-HTTP 模組是一個類別，它會定義 `HttpApplication` 事件的事件處理常式，例如 `Error` 事件。 ELMAH 包含多個 HTTP 模組，這三個最無關的都是： 

    - `ErrorLogModule`-將未處理的例外狀況記錄到記錄來源。
    - `ErrorMailModule`-在電子郵件訊息中傳送未處理之例外狀況的詳細資料。
    - `ErrorFilterModule`-套用開發人員指定的篩選準則，以判斷要記錄的例外狀況，以及要忽略的例外狀況。
- **Http 處理**程式-Http 處理常式是一個類別，負責產生特定類型要求的標記。 ELMAH 包含以網頁、RSS 摘要或逗號分隔檔案（CSV）的形式呈現錯誤詳細資料的 HTTP 處理常式。
- **錯誤記錄檔來源**-最新版的 ELMAH 可以將錯誤記錄到記憶體、Microsoft SQL Server 資料庫、Microsoft Access 資料庫、Oracle 資料庫、XML 檔案、SQLite 資料庫或 Vista DB 資料庫。 如同健全狀況監視系統，ELMAH 的架構是使用提供者模型所建立，這表示您可以建立並順暢地整合您自己的自訂記錄來源提供者（如有需要）。

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>步驟2：註冊 ELMAH 的 HTTP 模組和處理常式

雖然 `Elmah.dll` 檔案包含自動記錄未處理的例外狀況，以及從網頁顯示錯誤詳細資料所需的 HTTP 模組和處理常式，但這些都必須在 web 應用程式的設定中明確註冊。 `ErrorLogModule` 的 HTTP 模組一旦註冊，就會訂閱 `HttpApplication`的 `Error` 事件。 每當引發此事件時，`ErrorLogModule` 會將例外狀況的詳細資料記錄至指定的記錄來源。 我們將在下一節「設定 ELMAH」中瞭解如何定義記錄來源提供者。 當您從網頁查看錯誤記錄檔時，`ErrorLogPageFactory` HTTP 處理常式 factory 會負責產生標記。

註冊 HTTP 模組和處理常式的特定語法，取決於正在為網站供電的 web 伺服器。 針對 ASP.NET 程式開發伺服器和 Microsoft 的 IIS 6.0 版和更早版本，HTTP 模組和處理常式會在 `<system.web>` 專案中顯示的 `<httpModules>` 和 `<httpHandlers>` 區段中註冊。 如果您使用 IIS 7.0，則必須在 `<system.webServer>` 元素的 `<modules>` 和 `<handlers>` 區段中註冊這些專案。 幸運的是，無論使用哪一種 web 伺服器，您都可以在*這兩個*地方定義 HTTP 模組和處理常式。 此選項最具便攜功能，因為它允許在開發和生產環境中使用相同的設定，而不論使用的 web 伺服器為何。

一開始請先在 `<system.web>`的 `<httpModules>` 和 `<httpHandlers>` 區段中註冊 `ErrorLogModule` HTTP 模組和 `ErrorLogPageFactory` HTTP 處理常式。 如果您的設定已經定義這兩個元素，那麼只要包含 ELMAH 的 HTTP 模組和處理常式的 `<add>` 元素即可。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample1.xml)]

接下來，在 `<system.webServer>` 元素中註冊 ELMAH 的 HTTP 模組和處理常式。 如先前所述，如果您的設定中還沒有此專案，請將它加入。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample2.xml)]

根據預設，如果 HTTP 模組和處理常式是在 `<system.web>` 區段中註冊，IIS 7 會抱怨。 `<validation>` 元素中的 `validateIntegratedModeConfiguration` 屬性會指示 IIS 7 隱藏這類錯誤訊息。

請注意，註冊 `ErrorLogPageFactory` HTTP 處理常式的語法包括 `path` 屬性，其設定為 [`elmah.axd`]。 這個屬性會通知 web 應用程式，如果要求抵達名為 `elmah.axd` 的頁面，則要求應由 `ErrorLogPageFactory` HTTP 處理常式處理。 我們稍後會在本教學課程中看到 `ErrorLogPageFactory` HTTP 處理常式。

### <a name="step-3-configuring-elmah"></a>步驟3：設定 ELMAH

ELMAH 會在名為 `<elmah>`的自訂設定區段中，于網站的 `Web.config` 檔案中尋找其設定選項。 若要在 `Web.config` 中使用自訂區段，則必須先在 `<configSections>` 元素中定義它。 開啟 `Web.config` 檔案，然後將下列標記新增至 `<configSections>`：

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample3.xml)]

> [!NOTE]
> 如果您要為 ASP.NET 1.x 應用程式設定 ELMAH，請從上述的 `<section>` 元素中移除 `requirePermission="false"` 屬性。

上述語法會註冊自訂 `<elmah>` 區段及其子區段： `<security>`、`<errorLog>`、`<errorMail>`和 `<errorFilter>`。

接下來，將 `<elmah>` 區段新增至 `Web.config`。 這個區段應該會出現在與 `<system.web>` 元素相同的層級。 在 `<elmah>` 區段中，新增 `<security>` 和 `<errorLog>` 區段，如下所示：

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample4.xml)]

`<security>` 區段的 `allowRemoteAccess` 屬性會指出是否允許遠端存取。 如果此值設定為0，則只能在本機查看錯誤記錄檔網頁。 如果此屬性設為1，則遠端和本機訪客皆會啟用錯誤記錄網頁。 現在，讓我們停用遠端存取訪客的錯誤記錄網頁。 我們稍後會提供遠端存取，讓我們有機會討論這項作業的安全性考慮。

`<errorLog>` 區段會定義錯誤記錄檔來源，這會指示記錄錯誤詳細資料的位置;它類似于健康情況監視系統中的 `<providers>` 區段。 上述語法會將 `SqlErrorLog` 類別指定為錯誤記錄檔來源，這會將錯誤記錄到 `connectionStringName` 屬性值所指定的 Microsoft SQL Server 資料庫中。

> [!NOTE]
> ELMAH 隨附額外的錯誤記錄檔提供者，可用來將錯誤記錄到 XML 檔案、Microsoft Access 資料庫、Oracle 資料庫和其他資料存放區。 如需如何使用這些替代錯誤記錄提供者的詳細資訊，請參閱包含在 ELMAH 下載中的範例 `Web.config` 檔案。

### <a name="step-4-creating-the-error-log-source-infrastructure"></a>步驟4：建立錯誤記錄檔來源基礎結構

ELMAH 的 `SqlErrorLog` 提供者會將錯誤詳細資料記錄到指定的 Microsoft SQL Server 資料庫。 `SqlErrorLog` 提供者預期此資料庫具有名為 `ELMAH_Error` 的資料表和三個預存程式： `ELMAH_GetErrorsXml`、`ELMAH_GetErrorXml`和 `ELMAH_LogError`。 ELMAH 下載包含 `db` 資料夾中名為 `SQLServer.sql` 的檔案，其中包含用來建立此資料表和這些預存程式的 T-sql。 您必須在資料庫上執行這些語句，才能使用 `SqlErrorLog` 提供者。

[**圖 1** ] 和 [ **2** ] 會在新增 `SqlErrorLog` 提供者所需的資料庫物件之後，顯示 Visual Studio 中的資料庫總管。

[![](logging-error-details-with-elmah-vb/_static/image2.png)](logging-error-details-with-elmah-vb/_static/image1.png)

**圖 1**： `SqlErrorLog` 提供者將錯誤記錄到 `ELMAH_Error` 資料表

[![](logging-error-details-with-elmah-vb/_static/image4.png)](logging-error-details-with-elmah-vb/_static/image3.png)

**圖 2**： `SqlErrorLog` 提供者使用三個預存程式

## <a name="elmah-in-action"></a>作用中的 ELMAH

此時，我們已將 ELMAH 新增至 web 應用程式，並註冊 `ErrorLogModule` HTTP 模組和 `ErrorLogPageFactory` HTTP 處理常式，並在 `Web.config`中指定 ELMAH 的設定選項，並為 `SqlErrorLog` 錯誤記錄提供者加入所需的資料庫物件。 我們現在已準備好查看 ELMAH 的實際運作！ 流覽書籍評論網站，並造訪會產生執行階段錯誤的頁面，例如 `Genre.aspx?ID=foo`或不存在的頁面，例如 `NoSuchPage.aspx`。 流覽這些頁面時所看到的內容，取決於 `<customErrors>` 的設定，以及您是在本機還是遠端存取。 （如需本主題的重新整理程式，請參閱[*顯示自訂錯誤頁面*教學](displaying-a-custom-error-page-vb.md)課程）。

當發生未處理的例外狀況時，ELMAH 不會影響向使用者顯示的內容。它只會記錄其詳細資料。 此錯誤記錄檔可從網站根目錄（例如 `http://localhost/BookReviews/elmah.axd`）中的網頁 `elmah.axd` 存取。 （此檔案實際上不存在於您的專案中，但當要求 `elmah.axd` 進入時，執行時間會將它分派至 `ErrorLogPageFactory` HTTP 處理常式，這會產生傳回給瀏覽器的標記）。

> [!NOTE]
> 您也可以使用 [`elmah.axd`] 頁面，指示 ELMAH 產生測試錯誤。 造訪 `elmah.axd/test` （如 `http://localhost/BookReviews/elmah.axd/test`）會導致 ELMAH 擲回類型 `Elmah.TestException`的例外狀況，其中包含錯誤訊息：「這是可以放心忽略的測試例外狀況」。

[**圖 3** ] 顯示從開發環境造訪 `elmah.axd` 時的錯誤記錄檔。

[![](logging-error-details-with-elmah-vb/_static/image6.png)](logging-error-details-with-elmah-vb/_static/image5.png)

**圖 3**： `Elmah.axd` 從網頁顯示錯誤記錄檔  
（[按一下以查看完整大小的影像](logging-error-details-with-elmah-vb/_static/image7.png)）

[**圖 3** ] 中的錯誤記錄檔包含六個錯誤專案。 每個專案都包含 HTTP 狀態碼（404或500，適用于這些錯誤）、類型、描述、發生錯誤時登入使用者的名稱，以及日期和時間。 按一下 [詳細資料] 連結，會顯示一個頁面，其中包含錯誤詳細資料的黃色畫面中顯示的相同錯誤訊息（請參閱 [**圖 4**]），以及發生錯誤時的伺服器變數值（請參閱 [**圖 5**]）。 您也可以查看儲存錯誤詳細資料的原始 XML，其中包括其他資訊，例如 HTTP POST 標頭中的值。

[![](logging-error-details-with-elmah-vb/_static/image9.png)](logging-error-details-with-elmah-vb/_static/image8.png)

**圖 4**：查看錯誤詳細資料 YSOD  
（[按一下以查看完整大小的影像](logging-error-details-with-elmah-vb/_static/image10.png)）

[![](logging-error-details-with-elmah-vb/_static/image12.png)](logging-error-details-with-elmah-vb/_static/image11.png)

**圖 5**：探索錯誤發生時的伺服器變數集合值  
（[按一下以查看完整大小的影像](logging-error-details-with-elmah-vb/_static/image13.png)）

將 ELMAH 部署到生產網站需要：

- 將 `Elmah.dll` 檔案複製到生產環境中的 `Bin` 資料夾，
- 將 ELMAH 特有的設定值複製到用於生產環境的 `Web.config` 檔案，以及
- 將錯誤記錄檔來源基礎結構新增至生產資料庫。

我們已探討在先前的教學課程中，將檔案從開發複製到生產環境的技術。 若要取得實際執行資料庫上的錯誤記錄檔來源基礎結構，最簡單的方法可能是使用 SQL Server Management Studio 連接到生產資料庫，然後執行 `SqlServer.sql` 腳本檔案，這將會建立所需的資料表和預存程式。

### <a name="viewing-the-error-details-page-on-production"></a>在生產環境上查看錯誤詳細資料頁面

將您的網站部署到生產環境之後，請造訪生產網站並產生未處理的例外狀況。 如同在開發環境中，當發生未處理的例外狀況時，ELMAH 不會影響顯示的錯誤頁面;相反地，它只會記錄錯誤。 如果您嘗試從生產環境流覽錯誤記錄檔頁面（`elmah.axd`），您將會看到 [**圖 6**] 所示的 [禁止] 頁面。

[![](logging-error-details-with-elmah-vb/_static/image15.png)](logging-error-details-with-elmah-vb/_static/image14.png)

**圖 6**：根據預設，遠端訪客無法查看錯誤記錄檔網頁  
（[按一下以查看完整大小的影像](logging-error-details-with-elmah-vb/_static/image16.png)）

回想一下，在 ELMAH 設定的 `<security>` 一節中，我們將 `allowRemoteAccess` 屬性設為0，這會禁止遠端使用者查看錯誤記錄檔。 請務必防止匿名訪客查看錯誤記錄檔，因為錯誤詳細資料可能會顯示安全性弱點或其他機密資訊。 如果您決定將此屬性設定為1，並啟用對錯誤記錄檔的遠端存取，請務必鎖定 `elmah.axd` 路徑，讓只有授權的訪客可以存取它。 這可以藉由將 `<location>` 元素加入至 `Web.config` 檔案來達成。

下列設定只允許系統管理員角色中的使用者存取錯誤記錄網頁：

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample5.xml)]

> [!NOTE]
> 在設定[*使用應用程式服務的網站*](configuring-a-website-that-uses-application-services-vb.md)教學課程中，已新增系統管理員角色和系統中的三個使用者-Scott、Jisun 和 Alice。 Scott 和 Jisun 的使用者是系統管理員角色的成員。 如需驗證和授權的詳細資訊，請參閱我的[網站安全性教學](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程。

遠端使用者現在可以查看生產環境的錯誤記錄檔;請回到 [**圖 3**]、[ **4**] 和 [**第 5**頁]，以取得錯誤記錄檔網頁的螢幕擷取畫面。 不過，如果匿名或非系統管理員的使用者嘗試查看錯誤記錄檔頁面，則會自動將其重新導向至登入頁面（`Login.aspx`），如 [**圖 7** ] 所示。

[![](logging-error-details-with-elmah-vb/_static/image18.png)](logging-error-details-with-elmah-vb/_static/image17.png)

**圖 7**：未經授權的使用者會自動重新導向至登入頁面  
（[按一下以查看完整大小的影像](logging-error-details-with-elmah-vb/_static/image19.png)）

### <a name="programmatically-logging-errors"></a>以程式設計方式記錄錯誤

ELMAH 的 `ErrorLogModule` HTTP 模組會自動將未處理的例外狀況記錄到指定的記錄來源。 或者，您可以記錄錯誤，而不需要使用 `ErrorSignal` 類別及其 `Raise` 方法來引發未處理的例外狀況。 `Raise` 方法會傳遞 `Exception` 物件，並將它記錄為已擲回該例外狀況，並在未處理的情況下到達 ASP.NET 執行時間。 不過，其差異在於，在呼叫 `Raise` 方法之後，要求會繼續正常執行，而擲回的未處理例外狀況會中斷要求的一般執行，並使 ASP.NET 執行時間顯示已設定的錯誤頁面。

在有某些動作可能會失敗的情況下，`ErrorSignal` 類別很有用，但其失敗對執行的整體作業而言並不嚴重。 比方說，網站可能包含的表單會接受使用者的輸入、將它儲存在資料庫中，然後傳送電子郵件給使用者，通知他們已處理他們的資訊。 如果成功將資訊儲存到資料庫，但傳送電子郵件訊息時發生錯誤，會發生什麼事？ 其中一個選項是擲回例外狀況，並將使用者傳送至錯誤頁面。 不過，這可能會讓使用者覺得不會儲存所輸入的資訊。 另一種方法是記錄電子郵件相關的錯誤，但無法以任何方式改變使用者的體驗。 這就是 `ErrorSignal` 類別很有用的地方。

[!code-vb[Main](logging-error-details-with-elmah-vb/samples/sample6.vb)]

## <a name="error-notification-via-email"></a>透過電子郵件的錯誤通知

除了將錯誤記錄到資料庫之外，還可以將 ELMAH 設定為將錯誤詳細資料傳送給指定的收件者。 這項功能是由 `ErrorMailModule` HTTP 模組所提供;因此，您必須在 `Web.config` 中註冊此 HTTP 模組，以便透過電子郵件傳送錯誤詳細資料。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample7.xml)]

接下來，在 `<elmah>` 元素的 [`<errorMail>`] 區段中指定有關錯誤電子郵件的資訊，指出電子郵件的寄件者和收件者、主旨，以及是否以非同步方式傳送電子郵件。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample8.xml)]

當上述設定備妥時，每當執行階段錯誤發生時，ELMAH 會將電子郵件傳送至 support@example.com，其中包含錯誤詳細資料。 ELMAH 的錯誤電子郵件包含 [錯誤詳細資料] 網頁中所顯示的相同資訊，也就是錯誤訊息、堆疊追蹤和伺服器變數（請參閱 [**圖 4** ] 和 [ **5**]）。 錯誤電子郵件也會包含例外狀況詳細資料，也就是以附件（`YSOD.html`）顯示死亡內容的黃色畫面。

[**圖 8** ] 顯示藉由造訪 `Genre.aspx?ID=foo`所產生的 ELMAH 錯誤電子郵件。 雖然 [**圖 8** ] 僅顯示錯誤訊息和堆疊追蹤，但伺服器變數會在電子郵件的本文中進一步納入。

[![](logging-error-details-with-elmah-vb/_static/image21.png)](logging-error-details-with-elmah-vb/_static/image20.png)

**圖 8**：您可以設定 ELMAH 以透過電子郵件傳送錯誤詳細資料  
（[按一下以查看完整大小的影像](logging-error-details-with-elmah-vb/_static/image22.png)）

## <a name="only-logging-errors-of-interest"></a>僅記錄感關注的錯誤

根據預設，ELMAH 會記錄每個未處理之例外狀況的詳細資料，包括404和其他 HTTP 錯誤。 您可以指示 ELMAH 使用錯誤篩選來忽略這些或其他類型的錯誤。 篩選邏輯是由 ELMAH 的 `ErrorFilterModule` HTTP 模組執行，您必須在 `Web.config` 中註冊，才能使用篩選邏輯。 在 [`<errorFilter>`] 區段中指定篩選的規則。

下列標記會指示 ELMAH 不記錄404錯誤。

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample9.xml)]

> [!NOTE]
> 別忘了，為了使用錯誤篩選，您必須註冊 `ErrorFilterModule` HTTP 模組。

`<test>` 區段內的 `<equal>` 元素稱為判斷提示。 如果判斷提示評估為 true，則會從 ELMAH 的記錄檔中篩選錯誤。 還有其他可用的判斷提示，包括： `<greater>`、`<greater-or-equal>`、`<not-equal>`、`<lesser>`、`<lesser-or-equal>`等等。 您也可以使用 `<and>` 和 `<or>` 布林運算子來結合判斷提示。 此外，您甚至可以將簡單的 JavaScript 運算式納入判斷提示，或在或 Visual Basic 中C#撰寫自己的判斷提示。

如需有關 ELMAH 錯誤篩選功能的詳細資訊，請參閱[elmah wiki](https://code.google.com/p/elmah/w/list)中的[錯誤篩選一節](https://code.google.com/p/elmah/wiki/ErrorFiltering)。

## <a name="summary"></a>總結

ELMAH 提供一個簡單但功能強大的機制，可在 ASP.NET web 應用程式中記錄錯誤。 就像 Microsoft 的健全狀況監視系統，ELMAH 可以將錯誤記錄到資料庫，並且可以透過電子郵件將錯誤詳細資料傳送給開發人員。 與健全狀況監視系統不同的是，ELMAH 針對更廣泛的錯誤記錄檔資料存放區提供現成的支援，包括： Microsoft SQL Server、Microsoft Access、Oracle、XML 檔案和其他幾個。 此外，ELMAH 提供了內建的機制，可用於查看錯誤記錄檔，以及網頁中特定錯誤的詳細資料，`elmah.axd`。 [`elmah.axd`] 頁面也可以將錯誤資訊轉譯為 RSS 摘要或逗號分隔值檔案（CSV），您可以使用 Microsoft Excel 來加以閱讀。 您也可以指示 ELMAH 使用宣告式或程式設計判斷提示來篩選記錄檔中的錯誤。 和 ELMAH 可以與 ASP.NET 1.x 版應用程式搭配使用。

每個部署的應用程式都應該有一些機制可自動記錄未處理的例外狀況，並傳送通知給開發小組。 是否使用健全狀況監視來完成這項作業，或 ELMAH 為次要。 換句話說，不論您使用的是健全狀況監視還是 ELMAH，都沒什麼意義;評估這兩個系統，然後選擇最符合您需求的系統。 基本上，重要的是將某些機制放在生產環境中，以記錄未處理的例外狀況。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ELMAH-錯誤記錄模組和處理常式](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH 專案頁面](https://code.google.com/p/elmah/)（原始程式碼、範例、wiki）
- [將 ELMAH 插入 Web 應用程式以攔截未處理的例外](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx)狀況（影片）
- [安全性錯誤記錄檔頁面](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [使用 HTTP 模組和處理常式建立可插入的 ASP.NET 元件](https://msdn.microsoft.com/library/aa479332.aspx)
- [網站安全性教學課程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [上一頁](logging-error-details-with-asp-net-health-monitoring-vb.md)
> [下一頁](precompiling-your-website-vb.md)
