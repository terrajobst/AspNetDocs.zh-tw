---
uid: whitepapers/overview
title: 白皮書 |Microsoft Docs
author: rick-anderson
description: 在此頁面上，您會找到可協助您安裝及設定 ASP.NET 的白皮書，並協助您撰寫安全、快速且彈性的 ASP.NET 應用程式。
ms.author: riande
ms.date: 11/15/2011
ms.assetid: d5e79470-01f2-4d65-8077-11c3e10a6784
msc.legacyurl: /whitepapers
msc.type: content
ms.openlocfilehash: 1a3a9fe5d685d4b38efe666fc88ff57016482ada
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640851"
---
# <a name="whitepapers"></a>白皮書

> 在此頁面上，您會找到可協助您安裝及設定 ASP.NET 的白皮書，並協助您撰寫安全、快速且彈性的 ASP.NET 應用程式。
> 
> - [ASP.NET 4](#aspnet4)
> - [ASP.NET 安全性白皮書](#security)
> - [安裝和設定白皮書](#setup)
> - [SQL Server 白皮書](#sql)
> - [一般白皮書](#general)

<a id="aspnet4"></a>
## <a name="aspnet-4"></a>ASP.NET 4

ASP.NET 4 和 Visual Studio 2010 的相關資訊。

[ASP.NET MVC 4 版本資訊](mvc4-beta-release-notes.md "mvc4-版本-注意事項")

本檔說明 ASP.NET MVC 4 Developer Preview for Visual Studio 2010 中引進的新功能和改進，以及安裝注意事項和已知問題。

[ASP.NET MVC 3 版本資訊](mvc3-release-notes.md "mvc3-版本-注意事項")

本檔說明 ASP.NET MVC 3 中引進的新功能和改進，以及安裝注意事項和已知問題。

[ASP.NET 4 和 Visual Studio 2010 網頁程式開發概觀](aspnet4/index.md "aspnet4")

ASP.NET 有許多令人興奮的改變，都是在 .NET Framework 第4版中推出。 本檔概述即將推出的版本中包含的許多新功能。

[ASP.NET 4 Beta 2 的重大變更](aspnet4/breaking-changes.md "重大變更")

本檔描述對 .NET Framework 第4版 Beta 2 版本（也就是 ASP.NET 4 Beta 2 版本）所做的變更，可能會影響使用舊版所建立的應用程式，包括 ASP.NET 4 Beta 1 版本。

[ASP.NET MVC 2 的新功能](what-is-new-in-aspnet-mvc.md "aspnet mvc 的新功能")

本檔說明 ASP.NET MVC 2 中引進的新功能和改進。

[將 ASP.NET MVC 1.0 應用程式升級至 ASP.NET MVC 2](aspnet-mvc2-upgrade-notes.md "aspnet-mvc2-升級-附注")

ASP.NET MVC 2 可以與 ASP.NET MVC 1.0 並存安裝在同一部伺服器上。 這讓應用程式開發人員可以彈性選擇何時將 ASP.NET MVC 1.0 應用程式升級為 ASP.NET MVC 2。 本檔說明如何以手動方式和在 Visual 中的 wizard 進行升級 。

<a id="security"></a>
## <a name="aspnet-security-whitepapers"></a>ASP.NET 安全性白皮書

安全性是網際網路應用程式的重要層面，而這些白皮書討論如何設計和實施安全的 ASP.NET 應用程式。

[檢測 ASP.NET 2.0 應用程式的安全性](https://msdn.microsoft.com/library/ms998325.aspx)

本 how To 說明如何使用自訂健全狀況監視事件來檢測您的 ASP.NET 應用程式，以追蹤安全性相關的事件和作業。 ASP.NET 2.0 版提供健全狀況監視，其中包含許多標準的檢測 。

[執行 ASP.NET 2.0 的安全性部署審查](https://msdn.microsoft.com/library/ms998367.aspx)

本 how To 說明如何執行 ASP.NET 2.0 應用程式的安全性部署審查，以識別不適當的設定所引進的潛在安全性弱點。 大部分的審核程式都牽涉到 。

[針對 ASP.NET 2.0 中的角色使用 ADAM](https://msdn.microsoft.com/library/ms998331.aspx)

本 how To 說明如何開發使用 Active Directory 應用程式模式（ADAM）來儲存 ASP.NET 角色的 ASP.NET 網站。 它會示範如何設定 ADAM 和授權管理員（AzMan）原則存放區，如何建立新的角色，以及 。

[搭配使用授權管理員（AzMan）與 ASP.NET 2。0](https://msdn.microsoft.com/library/ms998336.aspx)

本 how To 說明如何搭配使用「授權管理員」（AzMan）與 ASP.NET 角色管理員 API 來管理角色、檢查使用者角色成員資格，以及授權角色以對 AzMan 原則存放區執行特定作業。 如何 。

[使用 ASP.NET 2.0 中的成員資格](https://msdn.microsoft.com/library/ms998347.aspx)

本 how To 說明如何使用 ASP.NET 2.0 版應用程式中的成員資格功能。 它會示範如何使用兩個不同的成員資格提供者： System.web.security.activedirectorymembershipprovider 和 SqlMembershipProvider。 成員資格功能 。

[使用 ASP.NET 2.0 中的角色管理員](https://msdn.microsoft.com/library/ms998314.aspx)

本 how To 說明如何使用 ASP.NET 2.0 角色管理員。 角色管理員會減輕管理角色和在應用程式中執行以角色為基礎之授權的工作。 它會示範如何設定各種角色提供者以搭配您的 。

[在 ASP.NET 2.0 中使用 Windows 驗證](https://msdn.microsoft.com/library/ms998358.aspx)

本 how To 說明如何在 ASP.NET Web 應用程式中設定及使用 Windows 驗證。 每當使用者屬於您的 Windows 網域時，windows 驗證就是慣用的方法。 這種方法可讓您使用現有的身分識別存放區 。

[執行受控碼的安全性程式碼審查（基準活動）](https://msdn.microsoft.com/library/ms998364.aspx)

本 how To 說明如何執行安全性程式碼審查。 此課程模組提供活動所涉及的步驟，以及用來分析結果的技術。 使用此如何搭配「安全性問題清單：受控碼（.NET Framework 2.0）」 。

[執行 ASP.NET 2.0 的安全性部署審查](https://msdn.microsoft.com/library/ms998367.aspx)

本 how To 說明如何執行 ASP.NET 2.0 應用程式的安全性部署審查，以識別不適當的設定所引進的潛在安全性弱點。 大部分的審核程式都牽涉到 。

[為 Windows 2000 執行 Kerberos 委派](https://msdn.microsoft.com/library/aa302400.aspx)

Kerberos 委派可讓您在應用程式的多個實體層之間流動已驗證的身分識別，以支援下游驗證和授權。 本 how To 說明完成此工作所需的設定步驟。

[在 ASP.NET 2.0 中使用模擬和委派](https://msdn.microsoft.com/library/ms998351.aspx)

本 how To 說明在 ASP.NET 2.0 應用程式中使用模擬的方式和時機。 根據預設，模擬已關閉，您可以使用 ASP.NET Web 應用程式的進程識別來存取資源。 不過，您可以使用 。

[在設計階段建立 Web 應用程式的威脅模型](https://msdn.microsoft.com/library/ms978527.aspx)

本 how To 說明建立 Web 應用程式威脅模型的方法。 威脅分析模型活動可協助您建立安全性設計模型，讓您在投資之前，可以公開潛在的安全性設計缺陷和弱點 。

### <a name="forms-authentication"></a>表單驗證

[保護 ASP.NET 2.0 中的表單驗證](https://msdn.microsoft.com/library/ms998310.aspx)

本 how To 說明如何安全地設定和使用 ASP.NET 2.0 應用程式的表單驗證。 要考慮的重要因素包括適當保護驗證票證，以及保護使用者身分識別存放區和存取該存放區。 ...

[在 ASP.NET 2.0 中使用表單驗證搭配 Active Directory](https://msdn.microsoft.com/library/ms998360.aspx)

本 how To 說明如何搭配 Microsoft®使用表單驗證，Active Directory 使用 System.web.security.activedirectorymembershipprovider®目錄服務。 如何說明如何設定提供者，以及如何建立和驗證使用者 。

[在 ASP.NET 2.0 的多個網域中使用表單驗證搭配 Active Directory](https://msdn.microsoft.com/library/ms998345.aspx)

本 how To 說明如何搭配 Microsoft®使用表單驗證，Active Directory 使用 System.web.security.activedirectorymembershipprovider®目錄服務。 如何說明如何設定提供者，以及如何建立和驗證使用者 。

[在 ASP.NET 2.0 中使用表單驗證搭配 SQL Server](https://msdn.microsoft.com/library/ms998317.aspx)

本 how To 說明如何搭配 SQL Server 成員資格提供者來使用表單驗證。 SQL Server 的表單驗證最適用于您的應用程式使用者不屬於 Windows 網域的情況，因此,。

[在 ASP.NET 1.1 中使用表單驗證建立 GenericPrincipal 物件](https://msdn.microsoft.com/library/aa302399.aspx)

本 how To 說明在使用表單驗證時，如何建立和處理 GenericPrincipal 和 FormsIdentity 物件。

[在 ASP.NET 1.1 中使用表單驗證搭配 Active Directory](https://msdn.microsoft.com/library/aa302397.aspx)

本 how To 文章說明如何針對 Active Directory 認證存放區執行表單驗證。

[在 ASP.NET 1.1 中使用表單驗證搭配 SQL Server](https://msdn.microsoft.com/library/aa302398.aspx)

本 how To 說明如何針對 SQL Server 認證存放區執行表單驗證。 它也會說明如何將密碼摘要儲存在資料庫中。

### <a name="user-input-data-validation"></a>使用者輸入資料驗證

[要求驗證 - 防止指令碼攻擊](request-validation.md "要求-驗證")

本檔描述 ASP.NET 的要求驗證功能，其中，應用程式預設會防止處理提交至伺服器的未編碼 HTML 內容。 當應用程式已完成時，可以停用此要求驗證功能 。

[防止 ASP.NET 中的跨網站腳本](https://msdn.microsoft.com/library/ms998274.aspx)

本 how To 說明如何使用適當的輸入驗證技術和編碼輸出，協助保護您的 ASP.NET 應用程式免于跨網站腳本攻擊。 它也會說明一些您可以在中使用的其他保護機制 。

[防止 ASP.NET 中的 SQL 插入式攻擊](https://msdn.microsoft.com/library/ms998271.aspx)

本 how To 說明一些方法來協助保護您的 ASP.NET 應用程式免于遭受 SQL 插入式攻擊。 當應用程式使用輸入來建立動態 SQL 語句，或使用預存程式連接到 ... 時，就會發生 SQL 插入式攻擊。

[使用正則運算式來限制 ASP.NET 中的輸入](https://msdn.microsoft.com/library/ms998267.aspx)

本 how To 說明如何在 ASP.NET 應用程式中使用正則運算式來限制不受信任的輸入。 正則運算式是驗證文字欄位（例如姓名、位址、電話號碼和其他使用者資訊）的好方法。 您可以使用 。

### <a name="code-access-security"></a>程式碼存取安全性

[在 ASP.NET 2.0 中使用代碼啟用安全性](https://msdn.microsoft.com/library/ms998326.aspx)

本 how To 說明如何為您的應用程式選取適當的信任層級，並在必要時，如何建立自訂的 ASP.NET 代碼啟用安全性原則檔案以定義自訂信任層級。 您可以使用不同的代碼啟用安全性信任 。

[建立自訂加密許可權](https://msdn.microsoft.com/library/aa302362.aspx)

本 how To 說明如何建立自訂代碼啟用安全性許可權，以控制以程式設計方式存取 Win32® Data Protection API （DPAPI）提供的非受控加密功能。 使用此自訂許可權搭配受控 DPAPI 包裝函式 。

[使用代碼啟用安全性原則來限制元件](https://msdn.microsoft.com/library/aa302361.aspx)

系統管理員可以設定代碼啟用安全性原則，以限制 .NET Framework 程式碼（元件）的作業。 在此操作說明中，您會設定代碼啟用安全性原則，以限制元件執行檔案 i/o 和限制的能力 。

### <a name="communications-security"></a>通訊安全性

[在 Web 服務器上設定 SSL](https://msdn.microsoft.com/library/aa302411.aspx)

必須針對 SSL 設定 Web 服務器，才能支援來自用戶端應用程式的 HTTPs 連線。 本 how To 說明如何在 Web 服務器上設定 SSL。

[設定用戶端憑證](https://msdn.microsoft.com/library/aa302412.aspx)

IIS 支援用戶端憑證驗證。 本 how To 說明如何將 Web 應用程式設定為需要用戶端憑證。 它也會示範如何在用戶端電腦上安裝憑證，並在呼叫 Web 應用程式時使用它。

[使用 IPSec 來篩選埠和驗證](https://msdn.microsoft.com/library/aa302366.aspx)

網際網路通訊協定安全性（IPSec）是一種通訊協定，而不是服務，可為以 IP 為基礎的網路流量提供加密、完整性及驗證服務。 IPSec 提供伺服器對伺服器的保護，因此您可以使用 IPSec 來對抗內部威脅 。

[使用 IPSec 在兩部伺服器之間提供安全通訊](https://msdn.microsoft.com/library/aa302413.aspx)

IPSec 是 Windows 2000 所提供的一項技術，可讓您在兩部伺服器之間建立加密通道。 IPSec 可以用來篩選 IP 流量，並驗證服務器。 本 how To 說明如何設定 IPSec 以提供安全（加密） 。

[使用 SSL 來保護與 SQL Server 的通訊](https://msdn.microsoft.com/library/aa302414.aspx)

應用程式必須能夠保護 SQL Server 資料庫伺服器之間傳遞的資料，這通常是很重要的。 使用 SQL Server，您可以使用 SSL 來建立加密通道。 本 how To 說明如何在資料庫伺服器上安裝憑證 。

[使用來自 ASP.NET 1.1 的用戶端憑證呼叫 Web 服務](https://msdn.microsoft.com/library/aa302408.aspx)

本 how To 說明如何將用戶端憑證傳遞至 Web 服務，以便從 ASP.NET Web 應用程式或 Windows Forms 應用程式進行驗證。 您可以在本機電腦存放區或使用者存放區中安裝用戶端憑證。 假設狀況

[使用 ASP.NET 1.1 的 SSL 呼叫 Web 服務](https://msdn.microsoft.com/library/aa302409.aspx)

安全通訊端層（SSL）加密可用於保證傳遞至 Web 服務的訊息完整性和機密性。 本 how To 說明如何搭配 Web 服務使用 SSL。

### <a name="cryptography"></a>密碼編譯

[在 .NET 1.1 中建立 DPAPI 程式庫](https://msdn.microsoft.com/library/aa302402.aspx)

本 how To 說明如何建立 managed 類別庫，將 DPAPI 功能公開給想要加密資料的應用程式，例如資料庫連接字串和帳號憑證。

[在 .NET 1.1 中建立加密程式庫](https://msdn.microsoft.com/library/aa302405.aspx)

本 how To 說明如何建立受控類別庫，以提供應用程式的加密功能。 它可讓應用程式選擇加密演算法。 支援的演算法包括 DES、三重 DES、RC2 和 Rijndael。

[將加密的連接字串儲存在 ASP.NET 1.1 的登錄中](https://msdn.microsoft.com/library/aa302406.aspx)

應用程式可以選擇將加密的資料（例如連接字串和帳號憑證）儲存在 Windows 登錄中。 本 how To 說明如何儲存和取出登錄中的加密字串。

[從 ASP.NET 1.1 使用 DPAPI （電腦存放區）](https://msdn.microsoft.com/library/aa302403.aspx)

本 how To 說明如何從 ASP.NET Web 應用程式或 Web 服務使用 DPAPI 來加密敏感性資料。

[從 ASP.NET 1.1 使用 DPAPI （使用者存放區）與企業服務](https://msdn.microsoft.com/library/aa302404.aspx)

本 how To 說明如何從 ASP.NET Web 應用程式或服務使用 DPAPI 來加密敏感性資料。 這是如何搭配使用 DPAPI 與使用者存放區，這需要使用超出進程的企業服務元件。

<a id="setup"></a>
## <a name="installation-and-setup-whitepapers"></a>安裝和設定白皮書

這些白皮書提供在伺服器上安裝和設定 ASP.NET 的逐步指示。

[建立 ASP.NET 2.0 應用程式的服務帳戶](https://msdn.microsoft.com/library/ms998297.aspx)

本 how To 說明如何建立及設定自訂的最低許可權服務帳戶，以執行 ASP.NET Web 應用程式。 根據預設，Microsoft Windows Server 2003 和 IIS 6.0 上的 ASP.NET 應用程式會使用內建的網路服務來執行 。

[在 ASP.NET 2.0 中裝載多個應用程式時改善安全性](https://msdn.microsoft.com/library/aa480478.aspx)

本 how To 說明如何將多個應用程式與 Web 主控環境中的共用系統資源互相隔離。 裝載環境可能是裝載多個的網際網路服務提供者（ISP）所提供的網頁伺服器 。

[在 ASP.NET 2.0 中使用中度信任](https://msdn.microsoft.com/library/ms998341.aspx)

本 how To 說明如何設定 ASP.NET Web 應用程式以中等信任的方式執行。 如果您在相同的伺服器上裝載多個應用程式，您可以使用代碼啟用安全性和中度信任層級來提供應用程式隔離。 藉由設定 。

[使用網路服務帳戶存取 ASP.NET 2.0 中的資源](https://msdn.microsoft.com/library/ms998320.aspx)

本 how To 說明您可以如何使用 NT AUTHORITY\Network Service 機器帳戶來存取本機和網路資源。 根據預設，在 Windows Server 2003 上，ASP.NET 應用程式會使用此帳戶的身分識別來執行。 這是最低許可權 。

[在 ASP.NET 2.0 中使用通訊協定轉換和限制委派](https://msdn.microsoft.com/library/ms998355.aspx)

本 how To 說明如何設定和使用通訊協定轉換和限制委派，以允許您的 ASP.NET 應用程式在模擬原始呼叫端時存取網路資源。 Microsoft® Windows®2000作業系統 。

[ASP.NET 並存執行 .NET Framework 1.0 和 1.1](side-by-side-with-10.md "並存與1。0")

本白皮書說明如何在您的電腦上安裝 .NET 1.0 和 .NET 1.1，讓 ASP.NET Web 應用程式可在任一版本的架構上執行。

[ASP.NET 拒絕存取 IIS 目錄](denied-access-to-iis-directories.md "拒絕存取 iis 目錄")

本白皮書說明當 ASP.NET 應用程式的要求傳回錯誤「拒絕存取*DirectoryName*目錄」時，您必須執行的動作。 無法開始監視目錄變更。」

[執行 ASP.NET 1.1 與 IIS 6.0](aspnet-and-iis6.md "aspnet 和 iis6")

雖然 Windows Server 2003 同時包含 IIS 6.0 和 ASP.NET 1.1，但這些元件預設為停用。 本白皮書說明如何啟用 IIS 6.0 和 ASP.NET 1.1，並建議數個設定以取得最佳 。

[套用 IE 的安全性更新之後，修正「無法使用伺服器應用程式」錯誤](ms03-32-issue.md "ms03-32-問題")

本文說明的修補程式可修正 Internet Explorer 的 MS03-32 安全性更新問題，這會影響在 Windows XP Professional 上執行的 ASP.NET 1.0 應用程式。

[建立自訂帳戶以執行 ASP.NET 1。1](https://msdn.microsoft.com/library/aa302396.aspx)

ASP.NET Web 應用程式通常會使用內建的 ASPNET 帳戶來執行。 有時，您可能會想要改為使用自訂帳戶。 本 how To 文章說明如何建立最低許可權的本機帳戶來執行 ASP.NET Web 應用程式。 ...

### <a name="configuration"></a>設定

[在 ASP.NET 2.0 中設定電腦金鑰](https://msdn.microsoft.com/library/ms998288.aspx)

本 how To 說明 Web.config 檔案中的 &lt;machineKey&gt; 元素，並示範如何設定 &lt;machineKey&gt; 專案，以控制 ViewState、表單驗證票證和角色 cookie 的篡改校對和加密。 ViewState 已簽署 。

[使用 DPAPI 加密 ASP.NET 2.0 中的設定區段](https://msdn.microsoft.com/library/ms998280.aspx)

本 how To 說明如何使用 Windows 資料保護應用程式開發介面（DPAPI）保護的設定提供者和 Aspnet\_regiis 來加密設定檔的區段。 您可以使用 Aspnet\_regiis 工具 。

[使用 RSA 加密 ASP.NET 2.0 中的設定區段](https://msdn.microsoft.com/library/ms998283.aspx)

本 how To 說明如何使用 RSA 保護的設定提供者和 Aspnet\_regiis 來加密設定檔的區段。 您可以使用 Aspnet\_regiis 工具來加密敏感性資料，例如連接字串，保留在 。

[在 ASP.NET 2.0 中使用模擬和委派](https://msdn.microsoft.com/library/ms998351.aspx)

本 how To 說明在 ASP.NET 2.0 應用程式中使用模擬的方式和時機。 根據預設，模擬已關閉，您可以使用 ASP.NET Web 應用程式的進程識別來存取資源。 不過，您可以使用 。

<a id="sql"></a>
## <a name="sql-server-whitepapers"></a>SQL Server 白皮書

雖然 ASP.NET 適用于各種不同的資料庫，但這些白皮書特別探討如何將 ASP.NET 應用程式連接到 SQL Server。

[使用 ASP.NET 2.0 中的 SQL 驗證連接到 SQL Server](https://msdn.microsoft.com/library/ms998300.aspx)

本 how To 說明當資料庫存取驗證使用原生 SQL 驗證時，如何安全地將 ASP.NET 應用程式連接到 Microsoft® SQL Server™。 Windows 驗證是連接到 SQL Server 的建議方式，因為您 。

[使用 ASP.NET 2.0 中的 Windows 驗證連接到 SQL Server](https://msdn.microsoft.com/library/ms998292.aspx)

本 how To 說明如何使用 ASP.NET 版本2.0 應用程式的 Windows 服務帳戶連接到 SQL Server 2000。 您應該盡可能使用 Windows 驗證而非 SQL 驗證，因為您會避免將認證儲存在 。

[使用 SSL 來保護與 SQL Server 2000 的通訊](https://msdn.microsoft.com/library/aa302414.aspx)

應用程式必須能夠保護 SQL Server 資料庫伺服器之間傳遞的資料，這通常是很重要的。 使用 SQL Server，您可以使用 SSL 來建立加密通道。 本 how To 說明如何在資料庫伺服器上安裝憑證,。

<a id="general"></a>
## <a name="general-whitepapers"></a>一般白皮書

下列案例研究說明用來將 Microsoft 的 .NET 社區網站從傳統主控環境遷移至 Microsoft Azure 的程式。

[將 Microsoft 的 ASP.NET 和 IIS.NET 社區網站遷移至 Microsoft Azure](https://go.microsoft.com/fwlink/?LinkId=400656)

這些白皮書涵蓋有關 ASP.NET 的各種主題。

[使用 ASP.NET 2.0 中的健康狀態監視](https://msdn.microsoft.com/library/ms998306.aspx)

本 how To 說明如何使用健全狀況監視來檢測您的應用程式是否有自訂事件。 若要建立自訂的健全狀況監視事件，請建立衍生自 WebBaseEvent 的類別，並設定 &lt;healthMonitoring&gt; 。

[執行修補程式管理](https://msdn.microsoft.com/library/aa302364.aspx)

本 how To 說明修補程式管理，包括如何讓單一或多部伺服器保持在最新狀態。 除了可從 Microsoft 下載的工具之外，不需要額外的軟體。 作業和安全性原則應採用修補程式管理 。

[Silverlight 3 SDK 中適用于 Silverlight 的 ASP.NET 伺服器控制項](https://go.microsoft.com/fwlink/?LinkId=153377)

Silverlight （「ASP.NET Silverlight 控制項」）的 ASP.NET 伺服器控制項（也就是 ASP.NET MediaPlayer 和 Silverlight 控制項）已從 Silverlight SDK for Silverlight 第3版中移除。 本檔提供使用這些 ASP.NET 的開發人員指引。

[建立高效能的 Web 應用程式](https://devexpress.com/act)

瞭解如何使用 ASP.NET Ajax Library 中的新功能來建立高效能的 Web 應用程式
