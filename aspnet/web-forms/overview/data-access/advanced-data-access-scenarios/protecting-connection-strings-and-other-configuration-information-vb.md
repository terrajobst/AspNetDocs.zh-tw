---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
title: 保護連接字串和其他設定資訊（VB） |Microsoft Docs
author: rick-anderson
description: ASP.NET 應用程式通常會將設定資訊儲存在 web.config 檔案中。 這其中的部分資訊是機密的，而且保證受到保護。 依 def 。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: cd17dbe1-c5e1-4be8-ad3d-57233d52cef1
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
msc.type: authoredcontent
ms.openlocfilehash: 070e1dccb80ef9af21ea621357c5b23e2ada6f9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524651"
---
# <a name="protecting-connection-strings-and-other-configuration-information-vb"></a>保護連接字串與其他設定資訊 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_VB.zip)或[下載 PDF](protecting-connection-strings-and-other-configuration-information-vb/_static/datatutorial73vb1.pdf)

> ASP.NET 應用程式通常會將設定資訊儲存在 web.config 檔案中。 這其中的部分資訊是機密的，而且保證受到保護。 根據預設，這個檔案不會提供給網站訪客，但是系統管理員或駭客可能會取得網頁伺服器檔案系統的存取權，並查看檔案的內容。 在本教學課程中，我們將瞭解 ASP.NET 2.0 可讓我們藉由加密 Web.config 檔案的區段來保護機密資訊。

## <a name="introduction"></a>簡介

ASP.NET 應用程式的設定資訊通常會儲存在名為 `Web.config`的 XML 檔案中。 在這些教學課程中，我們已更新 `Web.config` 幾次。 例如，在[第一個教學](../introduction/creating-a-data-access-layer-vb.md)課程中建立 `Northwind` 型別資料集時，連接字串資訊會自動新增至 [`<connectionStrings>`] 區段中的 `Web.config`。 之後，在[主版頁面和網站導覽](../introduction/master-pages-and-site-navigation-vb.md)教學課程中，我們會手動更新 `Web.config`，並加入 `<pages>` 元素，指出專案中的所有 ASP.NET 網頁都應該使用 `DataWebControls` 主題。

由於 `Web.config` 可能包含機密資料（例如連接字串），因此 `Web.config` 的內容必須保持安全，而且不受未經授權的檢視器影響。 根據預設，具有 `.config` 副檔名之檔案的任何 HTTP 要求都會由 ASP.NET 引擎處理，這會傳回 [圖 1] 所示的 [*不提供這種類型的頁面*] 訊息。 這表示訪客無法藉由直接在瀏覽器的網址列中輸入 http://www.YourServer.com/Web.config，來查看您 `Web.config` 的檔案內容。

[![透過瀏覽器造訪 web.config，會傳回不提供這種類型的頁面訊息](protecting-connection-strings-and-other-configuration-information-vb/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image1.png)

**圖 1**：透過瀏覽器造訪 `Web.config` 會傳回此類型的頁面未提供服務訊息（[按一下以觀看完整大小的影像](protecting-connection-strings-and-other-configuration-information-vb/_static/image3.png)）

但是，如果攻擊者能夠找到一些其他惡意探索，讓她查看您 `Web.config` 的檔案內容呢？ 攻擊者可以利用這種資訊來進行哪些動作，並採取哪些步驟來進一步保護 `Web.config`中的機密資訊？ 幸運的是，`Web.config` 中的大部分區段並不包含敏感性資訊。 如果攻擊者知道您的 ASP.NET 網頁所使用的預設主題名稱，可能會有什麼傷害 perpetrate？

不過，某些 `Web.config` 區段包含敏感性資訊，其中可能包含連接字串、使用者名稱、密碼、伺服器名稱、加密金鑰等等。 這項資訊通常會在下列 `Web.config` 區段中找到：

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

在本教學課程中，我們將探討用來保護這類敏感性設定資訊的技術。 如我們所見，.NET Framework 版本2.0 包含受保護的設定系統，可讓您以程式設計方式加密和解密選取的設定區段。

> [!NOTE]
> 本教學課程最後會介紹從 ASP.NET 應用程式連接到資料庫的 Microsoft 建議。 除了加密您的連接字串之外，您還可以確保您以安全的方式連接到資料庫，藉此協助強化您的系統。

## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>步驟1：探索 ASP.NET 2.0 s 受保護的設定選項

ASP.NET 2.0 包含受保護的設定系統，用於加密和解密設定資訊。 這包括 .NET Framework 中的方法，可用於以程式設計方式加密或解密設定資訊。 受保護的設定系統會使用[提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，讓開發人員選擇要使用的密碼編譯實施。

.NET Framework 隨附兩個受保護的設定提供者：

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) -使用非對稱式[RSA 演算法](http://en.wikipedia.org/wiki/Rsa)進行加密和解密。
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) -使用「Windows[資料保護 API」（DPAPI）](https://msdn.microsoft.com/library/ms995355.aspx)進行加密和解密。

因為受保護的設定系統會實作為提供者設計模式，所以您可以建立自己的受保護設定提供者，並將它插入您的應用程式中。 如需此程式的詳細資訊，請參閱[執行受保護的設定提供者](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx)。

RSA 和 DPAPI 提供者會使用金鑰來加密和解密常式，而這些金鑰可以儲存在電腦或使用者層級。 當 web 應用程式在自己專用的伺服器上執行時，或如果伺服器上有多個應用程式需要共用加密的資訊，電腦層級金鑰就很適合。 使用者層級索引鍵在共用主控環境中是較安全的選項，在相同伺服器上的其他應用程式應該無法解密應用程式的受保護設定區段。

在本教學課程中，我們的範例會使用 DPAPI 提供者和電腦層級的金鑰。 具體而言，我們將探討 `Web.config`中的 `<connectionStrings>` 區段加密，雖然受保護的設定系統可以用來加密大部分的任何 `Web.config` 區段。 如需使用使用者層級索引鍵或使用 RSA 提供者的詳細資訊，請參閱本教學課程結尾的進一步閱讀一節中的資源。

> [!NOTE]
> `RSAProtectedConfigurationProvider` 和 `DPAPIProtectedConfigurationProvider` 提供者會分別以 `RsaProtectedConfigurationProvider` 和 `DataProtectionConfigurationProvider`的提供者名稱，在 `machine.config` 檔案中註冊。 加密或解密設定資訊時，必須提供適當的提供者名稱（`RsaProtectedConfigurationProvider` 或 `DataProtectionConfigurationProvider`），而不是實際的類型名稱（`RSAProtectedConfigurationProvider` 和 `DPAPIProtectedConfigurationProvider`）。 您可以在 [`$WINDOWS$\Microsoft.NET\Framework\version\CONFIG`] 資料夾中找到 `machine.config` 檔案。

## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>步驟2：以程式設計方式加密和解密設定區段

只要幾行程式碼，我們就可以使用指定的提供者來加密或解密特定的設定區段。 我們很快就會看到程式碼，只需要以程式設計方式參考適當的設定區段，呼叫其 `ProtectSection` 或 `UnprotectSection` 方法，然後呼叫 `Save` 方法來保存變更。 此外，.NET Framework 還包含有用的命令列公用程式，可以加密和解密設定資訊。 我們將在步驟3中探索此命令列公用程式。

為了說明以程式設計方式保護設定資訊，讓 s 建立一個 ASP.NET 網頁，其中包含用來加密和解密 `Web.config`中 `<connectionStrings>` 區段的按鈕。

從開啟 [`AdvancedDAL`] 資料夾中的 [`EncryptingConfigSections.aspx`] 頁面開始。 將 TextBox 控制項從 [工具箱] 拖曳至設計工具，將其 [`ID`] 屬性設定為 [`WebConfigContents`]，將其 `TextMode` 屬性設為 [`MultiLine`]，並將其 [`Width`] 和 [`Rows`] 屬性分別設為95% 和15 這個 TextBox 控制項會顯示 `Web.config` 的內容，讓我們快速查看內容是否已加密。 當然，在實際的應用程式中，您不會想要顯示 `Web.config`的內容。

在文字方塊底下，新增兩個名為 `EncryptConnStrings` 和 `DecryptConnStrings`的按鈕控制項。 設定其 Text 屬性以加密連接字串和解密連接字串。

此時，您的畫面看起來應該像 [圖 2]。

[![在頁面中新增文字方塊和兩個按鈕 Web 控制項](protecting-connection-strings-and-other-configuration-information-vb/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image4.png)

**圖 2**：將 TextBox 和兩個按鈕 Web 控制項新增至頁面（[按一下以查看完整大小的影像](protecting-connection-strings-and-other-configuration-information-vb/_static/image6.png)）

接下來，我們需要撰寫程式碼，在第一次載入頁面時，載入並顯示 [`WebConfigContents`] 文字方塊中 `Web.config` 的內容。 將下列程式碼加入至頁面的程式碼後置類別。 這段程式碼會新增名為 `DisplayWebConfig` 的方法，並在 `False``Page.IsPostBack` 時從 `Page_Load` 事件處理常式中呼叫它：

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample1.vb)]

`DisplayWebConfig` 方法會使用[`File` 類別](https://msdn.microsoft.com/library/system.io.file.aspx)來開啟應用程式的 `Web.config` 檔案、 [`StreamReader` 類別](https://msdn.microsoft.com/library/system.io.streamreader.aspx)以將其內容讀入字串，以及[`Path` 類別](https://msdn.microsoft.com/library/system.io.path.aspx)來產生 `Web.config` 檔案的實體路徑。 這三個類別都可以在[`System.IO` 命名空間](https://msdn.microsoft.com/library/system.io.aspx)中找到。 因此，您必須將 `Imports``System.IO` 語句新增至程式碼後置類別的頂端，或者，在這些類別名稱前面加上 `System.IO.`

接下來，我們需要為兩個按鈕控制項加入事件處理常式 `Click` 事件，並新增必要的程式碼，以使用電腦層級金鑰搭配 DPAPI 提供者來加密和解密 `<connectionStrings>` 區段。 在設計工具中，按兩下每個按鈕，以在程式碼後置類別中加入 `Click` 事件處理常式，然後新增下列程式碼：

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample2.vb)]

兩個事件處理常式中所使用的程式碼幾乎完全相同。 兩者都是從透過[`WebConfigurationManager` class](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx) s [`OpenWebConfiguration` 方法](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)取得目前應用程式 `Web.config` 檔案的相關資訊開始。 這個方法會傳回所指定虛擬路徑的 web 設定檔案。 接下來，`Web.config` 檔案 s `<connectionStrings>` 區段會透過[`Configuration` 類別](https://msdn.microsoft.com/library/system.configuration.configuration.aspx)的[`GetSection(sectionName)` 方法](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx)來存取，這會傳回[`ConfigurationSection`](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx)物件。

`ConfigurationSection` 物件包含[`SectionInformation` 屬性](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx)，可提供與設定區段相關的其他資訊和功能。 如上述程式碼所示，我們可以藉由檢查 `SectionInformation` 屬性 s `IsProtected` 屬性來判斷設定區段是否已加密。 此外，您可以透過 `SectionInformation` 屬性的 `ProtectSection(provider)` 和 `UnprotectSection` 方法來加密或解密區段。

`ProtectSection(provider)` 方法會接受指定要在加密時使用之受保護設定提供者名稱的字串做為輸入。 在 [`EncryptConnString`] 按鈕的事件處理常式中，我們將 DataProtectionConfigurationProvider 傳遞至 `ProtectSection(provider)` 方法，以便使用 DPAPI 提供者。 `UnprotectSection` 方法可以判斷用來加密設定區段的提供者，因此不需要任何輸入參數。

呼叫 `ProtectSection(provider)` 或 `UnprotectSection` 方法之後，您必須呼叫 `Configuration` 物件 s [`Save` 方法](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx)來保存變更。 一旦設定資訊已加密或解密，並儲存變更之後，我們會呼叫 `DisplayWebConfig` 將更新的 `Web.config` 內容載入 TextBox 控制項。

輸入上述程式碼之後，請透過瀏覽器造訪 `EncryptingConfigSections.aspx` 頁面來進行測試。 一開始，您應該會看到一個頁面，其中列出以純文字顯示的 [`<connectionStrings>`] 區段 `Web.config` 的內容（請參閱 [圖 3]）。

[![在頁面中新增文字方塊和兩個按鈕 Web 控制項](protecting-connection-strings-and-other-configuration-information-vb/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image7.png)

**圖 3**：將 TextBox 和兩個按鈕 Web 控制項新增至頁面（[按一下以查看完整大小的影像](protecting-connection-strings-and-other-configuration-information-vb/_static/image9.png)）

現在，按一下 [加密連接字串] 按鈕。 如果已啟用要求驗證，從 [`WebConfigContents`] 文字方塊回傳的標記將會產生一個 `HttpRequestValidationException`，其中會顯示訊息，表示從用戶端偵測到可能危險的 `Request.Form` 值。 要求驗證（預設會在 ASP.NET 2.0 中啟用）會禁止包含未編碼 HTML 的回傳，而且是設計來協助防止腳本插入式攻擊。 這種檢查可以在頁面或應用層級停用。 若要將此頁面關閉，請將 `@Page` 指示詞中的 `ValidateRequest` 設定設定為 [`False`]。 `@Page` 指示詞位於頁面 s 宣告式標記的頂端。

[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample3.aspx)]

如需有關要求驗證、其用途、如何在頁面和應用層級停用它，以及如何 HTML 編碼標記的詳細資訊，請參閱[要求驗證-防止腳本攻擊](../../../../whitepapers/request-validation.md)。

停用頁面的要求驗證之後，請再次嘗試按一下 [加密連接字串] 按鈕。 在回傳時，將會存取設定檔案，並使用 DPAPI 提供者加密其 `<connectionStrings>` 區段。 文字方塊接著會更新，以顯示新的 `Web.config` 內容。 如 [圖 4] 所示，現在 `<connectionStrings>` 的資訊已加密。

[![按一下 [加密連接字串] 按鈕會加密 &lt;connectionString&gt; 區段](protecting-connection-strings-and-other-configuration-information-vb/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image10.png)

**圖 4**：按一下 [加密連接字串] 按鈕會加密 `<connectionString>` 區段（[按一下以查看完整大小的影像](protecting-connection-strings-and-other-configuration-information-vb/_static/image12.png)）

在電腦上產生的加密 `<connectionStrings>` 區段會遵循，不過為了簡潔起見，已移除 `<CipherData>` 元素中的部分內容：

[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample4.xml)]

> [!NOTE]
> `<connectionStrings>` 元素會指定用來執行加密（`DataProtectionConfigurationProvider`）的提供者。 當按一下 [解密連接字串] 按鈕時，`UnprotectSection` 方法會使用這項資訊。

從 `Web.config` 存取連接字串資訊時（由我們從 SqlDataSource 控制項撰寫的程式碼），或從類型資料集中的 Tableadapter 自動產生的程式碼，它會自動解密。 簡單地說，我們不需要新增任何額外的程式碼或邏輯來解密已加密的 `<connectionString>` 區段。 若要示範這種情況，請造訪其中一個先前的教學課程，例如 [基本報告] 區段中的簡單顯示教學課程（`~/BasicReporting/SimpleDisplay.aspx`）。 如 [圖 5] 所示，本教學課程的運作方式與我們預期的完全相同，表示加密的連接字串資訊會由 ASP.NET 網頁自動解密。

[![資料存取層會自動解密連接字串資訊](protecting-connection-strings-and-other-configuration-information-vb/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image13.png)

**圖 5**：資料存取層會自動解密連接字串資訊（[按一下以查看完整大小的影像](protecting-connection-strings-and-other-configuration-information-vb/_static/image15.png)）

若要將 `<connectionStrings>` 區段還原回其純文字標記法，請按一下 [解密連接字串] 按鈕。 在回傳時，您應該會在 `Web.config` 中看到純文字格式的連接字串。 此時，您的畫面看起來應該像第一次造訪此頁面時一樣（請參閱 [圖 3]）。

## <a name="step-3-encrypting-configuration-sections-usingaspnet_regiisexe"></a>步驟3：使用`aspnet_regiis.exe` 加密設定區段

.NET Framework 在 `$WINDOWS$\Microsoft.NET\Framework\version\` 資料夾中包含各種不同的命令列工具。 例如，在[使用 sql](../caching-data/using-sql-cache-dependencies-vb.md)快取相依性教學課程中，我們探討了如何使用 `aspnet_regsql.exe` 命令列工具來新增 SQL 快取相依性所需的基礎結構。 此資料夾中另一個有用的命令列工具是[ASP.NET IIS 註冊工具（`aspnet_regiis.exe`）](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx)。 正如其名，ASP.NET IIS 註冊工具主要是用來向 Microsoft 專業級的網頁伺服器（IIS）註冊 ASP.NET 2.0 應用程式。 除了與 IIS 相關的功能之外，ASP.NET IIS 註冊工具也可以用來加密或解密 `Web.config`中指定的設定區段。

下列語句顯示使用 `aspnet_regiis.exe` 命令列工具來加密設定區段的一般語法：

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample5.cmd)]

*區段*是要加密的設定區段（例如 connectionStrings），*實體\_目錄*是 web 應用程式根目錄的完整實體路徑，而*提供者*是要使用之受保護設定提供者的名稱（例如 DataProtectionConfigurationProvider）。 或者，如果 web 應用程式是在 IIS 中註冊，您可以使用下列語法來輸入虛擬路徑，而不是實體路徑：

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample6.cmd)]

下列 `aspnet_regiis.exe` 範例會使用 DPAPI 提供者搭配機器層級金鑰來加密 `<connectionStrings>` 區段：

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample7.cmd)]

同樣地，`aspnet_regiis.exe` 命令列工具也可以用來解密設定區段。 不使用 `-pef` 參數，而是使用 `-pdf` （或而不是 `-pe`，使用 `-pd`）。 另請注意，解密時不需要提供者名稱。

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample8.cmd)]

> [!NOTE]
> 由於我們使用的是使用電腦特有金鑰的 DPAPI 提供者，因此您必須從提供網頁的同一部電腦上執行 `aspnet_regiis.exe`。 例如，如果您從本機開發電腦執行這個命令列程式，然後將加密的 Web.config 檔案上傳到實際執行伺服器，實際伺服器將無法解密加密後的連接字串資訊使用您開發電腦特有的金鑰。 RSA 提供者沒有這項限制，因為可以將 RSA 金鑰匯出至另一部電腦。

## <a name="understanding-database-authentication-options"></a>瞭解資料庫驗證選項

在任何應用程式可以對 Microsoft SQL Server 資料庫發出 `SELECT`、`INSERT`、`UPDATE`或 `DELETE` 查詢之前，資料庫首先必須識別要求者。 此程式稱為*驗證*，SQL Server 提供兩種驗證方法：

- **Windows 驗證**-用來執行應用程式的進程會用來與資料庫通訊。 透過 Visual Studio 2005 s ASP.NET 程式開發伺服器執行 ASP.NET 應用程式時，ASP.NET 應用程式會假設目前登入之使用者的身分識別。 針對 Microsoft Internet Information Server （IIS）上的 ASP.NET 應用程式，ASP.NET 應用程式通常會假設 `domainName``\MachineName` 或 `domainName``\NETWORK SERVICE`的身分識別，不過這可以自訂。
- **SQL 驗證**-提供使用者識別碼和密碼值做為驗證的認證。 使用 SQL 驗證時，會在連接字串中提供使用者識別碼和密碼。

Windows 驗證優先于 SQL 驗證，因為這是較安全的方式。 使用 Windows 驗證時，連接字串可從使用者名稱和密碼免費，而且如果 web 伺服器和資料庫伺服器位於兩部不同的電腦上，則不會透過網路以純文字傳送認證。 不過，使用 SQL 驗證時，驗證認證會在連接字串中硬式編碼，並以純文字格式從 web 伺服器傳輸到資料庫伺服器。

這些教學課程已使用 Windows 驗證。 您可以藉由檢查連接字串來分辨正在使用的驗證模式。 本教學課程的 `Web.config` 中的連接字串已：

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

整合式安全性 = True，而且沒有使用者名稱和密碼，表示正在使用 Windows 驗證。 在某些連接字串中，會使用「信任的連接 = 是」或「整合式安全性 = SSPI」這個詞彙，而不是整合式安全性 = True，但這三個都表示使用 Windows 驗證。

下列範例顯示使用 SQL 驗證的連接字串。 請注意內嵌于連接字串中的認證：

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

想像一下，攻擊者可以 `Web.config` 檔案來查看您的應用程式。 如果您使用 SQL 驗證連接到可透過網際網路存取的資料庫，攻擊者就可以使用此連接字串，透過 SQL Management Studio 或其本身網站上的 ASP.NET 網頁，連接到您的資料庫。 若要協助降低此威脅，請使用受保護的設定系統，加密 `Web.config` 中的連接字串資訊。

> [!NOTE]
> 如需 SQL Server 中可用的不同驗證類型的詳細資訊，請參閱[建立安全 ASP.NET 應用程式：驗證、授權和安全通訊](https://msdn.microsoft.com/library/aa302392.aspx)。 如需說明 Windows 和 SQL 驗證語法差異的進一步連接字串範例，請參閱[ConnectionStrings.com](http://www.connectionstrings.com/)。

## <a name="summary"></a>總結

根據預設，ASP.NET 應用程式中具有 `.config` 副檔名的檔案無法透過瀏覽器存取。 不會傳回這些類型的檔案，因為它們可能包含機密資訊，例如資料庫連接字串、使用者名稱和密碼等。 .NET 2.0 中受保護的設定系統可讓指定的設定區段加密，以協助進一步保護敏感性資訊。 有兩個內建的受保護設定提供者：一個使用 RSA 演算法，另一個使用 Windows 資料保護 API （DPAPI）。

在本教學課程中，我們探討了如何使用 DPAPI 提供者來加密和解密設定。 這可以透過程式設計的方式來完成，如我們在步驟2中所見，還有步驟3中所述的 `aspnet_regiis.exe` 命令列工具。 如需有關使用使用者層級索引鍵或改為使用 RSA 提供者的詳細資訊，請參閱進一步閱讀一節中的資源。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [建立安全的 ASP.NET 應用程式：驗證、授權和安全通訊](https://msdn.microsoft.com/library/aa302392.aspx)
- [加密 ASP.NET 2.0 應用程式中的設定資訊](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [在 ASP.NET 2.0 中加密 `Web.config` 值](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [如何：使用 DPAPI 加密 ASP.NET 2.0 中的設定區段](https://msdn.microsoft.com/library/ms998280.aspx)
- [How To：使用 RSA 加密 ASP.NET 2.0 中的設定區段](https://msdn.microsoft.com/library/ms998283.aspx)
- [.NET 2.0 中的設定 API](http://www.odetocode.com/Articles/418.aspx)
- [Windows 資料保護](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy 和 Randy Schmidt。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
> [下一頁](debugging-stored-procedures-vb.md)
