---
uid: whitepapers/aspnet-and-iis6
title: 執行具有 IIS 6.0 的 ASP.NET 1.1 |Microsoft Docs
author: rick-anderson
description: 雖然 Windows Server 2003 同時包含 IIS 6.0 和 ASP.NET 1.1，但這些元件預設為停用。 本白皮書說明如何啟用 IIS 6.0 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523307"
---
# <a name="running-aspnet-11-with-iis-60"></a>執行 ASP.NET 1.1 與 IIS 6.0

> 雖然 Windows Server 2003 同時包含 IIS 6.0 和 ASP.NET 1.1，但這些元件預設為停用。 本白皮書說明如何啟用 IIS 6.0 和 ASP.NET 1.1，並建議數個設定，以從 IIS 和 ASP.NET 取得最佳效能。
> 
> 適用于 ASP.NET 1.1 和 IIS 6.0。

ASP.NET 1.1 隨附于 Windows Server 2003，其中也包含最新版的 Internet Information Server （IIS）版本6.0。 IIS 6.0 和 ASP.NET 1.1 是設計用來順暢地整合，而 ASP.NET 現在預設為新的 IIS 6.0 工作者進程模型。

## <a name="aspnet-11-is-not-installed-by-default"></a>預設不會安裝 ASP.NET 1。1

與舊版的 Microsoft 伺服器作業系統不同的是，預設不會啟用 Internet Information Server （IIS）;也不是 ASP.NET 1.1。 有兩個選項可啟用 IIS：

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>啟用 IIS，選項 #1-設定您的伺服器 Wizard

Windows Server 2003 隨附新的「設定您的伺服器嚮導」，協助您在所需的模式下正確設定伺服器。

若要啟動精靈-請注意，若要執行 wizard，您必須以系統管理員的身分登入-前往： Start |程式 |[系統管理工具]，然後選取 [設定您的伺服器]。

選取之後，您應該會看到 [設定您的伺服器 Wizard] 開啟畫面：

![](aspnet-and-iis6/_static/image1.jpg)

按一下 [下一步 &gt;]：

![](aspnet-and-iis6/_static/image2.jpg)

按一下 [下一步 &gt;]

![](aspnet-and-iis6/_static/image3.jpg)

在此畫面上，您將需要選取 [應用程式伺服器（IIS，ASP.NET）] 做為要設定的選項。

按一下 [下一步 &gt;]。

![](aspnet-and-iis6/_static/image4.jpg)

選取將伺服器設定為應用程式伺服器之後，將會顯示此畫面，提示您應安裝的其他功能。 預設不會選取任何選項。 若要自動啟用 ASP.NET，您必須選取 [啟用 ASP]。NET '。

按一下 [下一步 &gt;]。

![](aspnet-and-iis6/_static/image5.jpg)

此畫面會顯示要安裝的選項。

按一下 [下一步 &gt;]。

![](aspnet-and-iis6/_static/image6.jpg)

您在安裝選取的選項時，將會看到此畫面。 在安裝服務時，通常會看到其他對話方塊出現。 系統可能會另外提示您輸入 Windows 2003 Server 安裝光碟的位置。

完成時，請按一下 [下一步 &gt;]。

![](aspnet-and-iis6/_static/image7.jpg)

按一下 [完成]-Windows Server 2003 現在已設定為支援 IIS 6.0 和 ASP.NET 1.1。

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>啟用 IIS，選項 #2-手動設定 IIS 和 ASP.NET

如果您不想使用「設定您的伺服器嚮導」，您可以選擇性地使用 [控制台] 中的 [新增或移除程式] 來安裝 IIS 6.0 和 ASP.NET 1.1。

首先開啟 [控制台]：

![](aspnet-and-iis6/_static/image8.jpg)

接下來，按一下 [新增/移除 Windows 元件]，這會開啟 [Windows 元件嚮導]：

![](aspnet-and-iis6/_static/image9.jpg)

反白顯示並勾選 [應用程式伺服器]，然後按一下 [詳細資料？] button

![](aspnet-and-iis6/_static/image10.jpg)

若要安裝 ASP.NET，請核取 [ASP]。NET '。

按一下 [確定] 以返回 Windows 元件嚮導。 按一下 Windows 元件嚮導中的 [下一步 &gt;] 開始安裝：

![](aspnet-and-iis6/_static/image11.jpg)

在安裝服務時，通常會看到其他對話方塊出現。 系統可能會另外提示您輸入 Windows 2003 Server 安裝光碟的位置。

當安裝完成時，您會看到 Windows 元件嚮導的最後一個畫面：

![](aspnet-and-iis6/_static/image12.jpg)

現在已設定並可使用 IIS 6.0 和 ASP.NET 1.1。

## <a name="recommended-settings"></a>建議的設定

執行具有 IIS 6.0 的 ASP.NET 1.1 時，有數個設定建議，以取得 ASP.NET 的最佳效能：

- 設定工作者進程記憶體限制
- 設定工作者進程回收

### <a name="configuring-worker-process-memory-limits"></a>設定工作者進程記憶體限制

根據預設，IIS 6.0 不會設定 IIS 允許使用的記憶體數量限制。 ASP.NET 的快取功能依賴記憶體的限制，因此快取可以主動從記憶體中移除未使用的專案。

建議您設定 IIS 6.0 的記憶體回收功能。 若要設定這個開啟的 Internet Information Services 管理員（開始 |程式 |系統管理工具 |Internet Information Services）。 開啟之後，展開 [應用程式集區] 資料夾：

針對每個應用程式集區：

![](aspnet-and-iis6/_static/image13.jpg)

1. 以滑鼠右鍵按一下應用程式集區（例如 ' DefaultAppPool '），然後選取 [屬性]：

![](aspnet-and-iis6/_static/image14.jpg)

2. 接下來，按一下 [使用的記憶體上限（以 mb 為單位）：] 來啟用記憶體回收。 此值不能超過伺服器上的實體（非虛擬）記憶體量，良好近似值是實體記憶體的60%，亦即，如果是具有512MB 實體記憶體的伺服器，請選取310。 此外，也建議您在使用2GB 位址空間時，最大值不能超過800MB。 如果伺服器的記憶體位址空間是3GB，則工作者進程的最大記憶體限制可以是1，800MB：

![](aspnet-and-iis6/_static/image15.jpg)

按一下 [套用] 和 [確定] 以結束 [屬性] 對話方塊。 針對所有可用的應用程式集區重複此動作。

### <a name="configuring-worker-recycling"></a>設定工作者回收

根據預設，IIS 6.0 已設定為每隔29小時回收其工作者進程。 這對執行 ASP.NET 的應用程式會有點積極，因此建議停用自動背景工作進程回收。

若要停用自動工作者進程回收，請先開啟 Internet Information Services 管理員（[開始] |程式 |系統管理工具 |Internet Information Services）。 開啟之後，展開 [應用程式集區] 資料夾：

![](aspnet-and-iis6/_static/image16.jpg)

針對每個應用程式集區：

1. 以滑鼠右鍵按一下應用程式集區（例如 ' DefaultAppPool '），然後選取 [屬性]：

![](aspnet-and-iis6/_static/image17.jpg)

2. 取消核取 [回收背景工作進程（分鐘）：]：

![](aspnet-and-iis6/_static/image18.jpg)

按一下 [套用] 和 [確定] 以結束 [屬性] 對話方塊。 針對所有可用的應用程式集區重複此動作。

## <a name="granting-write-access-to-the-file-system"></a>授與檔案系統的寫入權限

如果您的應用程式需要檔案系統的寫入權限，而且您使用 NTFS，則必須修改資料夾或檔案上的存取控制清單（ACL），以授與的 ASP.NET 存取權。

例如，若要將 ASP.NET 寫入存取權授與 c:\inetpub\wwwroot，請先開啟瀏覽器並流覽至目錄：

![](aspnet-and-iis6/_static/image19.jpg)

接下來，以滑鼠右鍵按一下目錄，例如 [wwwroot]，然後選取 [屬性]。 在 [屬性] 對話方塊開啟之後，選取 [安全性] 索引標籤：

![](aspnet-and-iis6/_static/image20.jpg)

C:\inetpub\wwwroot\ 目錄是特殊的目錄，其中已授與特殊的 IIS 6.0 群組 ' IIS\_WPG ' 讀取 &amp; 執行、列出資料夾內容和讀取權限。 不過，若要授與寫入權限，您必須按一下 [允許] 核取方塊以進行寫入：

![](aspnet-and-iis6/_static/image21.jpg)

IIS 6.0 現在具有此資料夾的寫入權限。 若要授與其他資料夾的寫入權限，請遵循下列步驟-請注意，您可能需要新增 IIS\_WPG 群組（如果尚未存在的話）。

> [!CAUTION]
> 將寫入權限授與 IIS\_WPG，可讓任何 ASP.NET 應用程式寫入此目錄。

## <a name="supporting-integrated-authentication-with-sql-server"></a>支援 SQL Server 的整合式驗證

整合式驗證可讓 SQL Server 利用 Windows NT 驗證來驗證 SQL Server 的登入帳戶。 這可讓使用者略過標準的 SQL Server 登入程式。 透過這種方法，網路使用者可以存取 SQL Server 資料庫，而不需提供個別的登入識別或密碼，因為 SQL Server 會從 Windows NT 網路安全性程式取得使用者和密碼資訊。

選擇 ASP.NET 應用程式的整合式驗證是不錯的選擇，因為您的應用程式連接字串中不會儲存任何認證。 相反地，用來連接到 SQL 的連接字串看起來會像這樣：

`"server=localhost; database=Northwind;Trusted_Connection=true"`

此連接字串會告訴 SQL Server 使用嘗試存取 SQL Server 之應用程式的 Windows 認證。 在 ASP.NET/IIS 6 的案例中，這會是 IIS\_WPG 群組中的帳戶。

若要啟用 SQL Server 和 ASP.NET 之間的整合式驗證，您必須先確定已針對整合式驗證或混合模式驗證設定 SQL Server-請洽詢您的 DBA 以判斷此情況。 如果 SQL Server 是這兩種模式的其中一種，您可以使用整合式驗證。

開啟 SQL Server Enterprise Manager （開始 |程式 |Microsoft SQL Server |Enterprise Manager）中，選取適當的伺服器，然後展開 [安全性] 資料夾：

![](aspnet-and-iis6/_static/image22.jpg)

如果未列出 ' BUILTINT\IIS\_WPG ' 群組，請以滑鼠右鍵按一下 登入，然後選取 新增 Login '：

![](aspnet-and-iis6/_static/image23.jpg)

在 [名稱：] 文字方塊中，輸入 ' [Server/Domain Name] \IIS\_WPG '，或按一下省略號按鈕以開啟 [Windows NT 使用者/群組選擇器]：

![](aspnet-and-iis6/_static/image24.jpg)

選取目前電腦的 IIS\_WPG 群組，然後按一下 [新增] 和 [確定] 關閉選擇器。

接著，您也需要設定預設資料庫和存取資料庫的許可權。 若要設定預設資料庫，請從下拉式清單中選擇，例如在 [Northwind] 底下選取：

![](aspnet-and-iis6/_static/image25.jpg)

接下來，按一下 [資料庫存取] 索引標籤：

![](aspnet-and-iis6/_static/image26.jpg)

針對您想要允許存取的每個資料庫，按一下 [允許] 核取方塊。 您也必須選取資料庫角色，檢查 db\_擁有者將確保您的登入具有管理和使用選取之資料庫的所有必要許可權。

按一下 [確定] 以結束 [屬性] 對話方塊。 您的 ASP.NET 應用程式現在已設定為支援整合式 SQL Server 驗證。

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>不要在 IIS 6.0 原生模式中執行 ASP.NET 1。0

Iis 6.0 上的 ASP.NET 1.0 只有在 IIS 5 相容性模式下才支援。

若要設定 ASP.NET 1.0 在 IIS 5.0 相容性模式中執行，請開啟網際網路服務管理員並以滑鼠右鍵按一下 [網站]，然後選取 [屬性]：

![](aspnet-and-iis6/_static/image27.jpg)

切換至 [服務] 索引標籤並檢查嗎？在 IIS 5.0 隔離模式中執行 WWW 服務？：

![](aspnet-and-iis6/_static/image28.jpg)
