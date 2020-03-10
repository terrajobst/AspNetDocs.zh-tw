---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 設定和檢測 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 中的設定和檢測有重大變更。 新的 ASP.NET 設定 API 允許將設定變更為 pr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: cd5bedce5459e8cf8e72df8de69ebd82f2d97789
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626025"
---
# <a name="configuration-and-instrumentation"></a>設定與檢測

由[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 中的設定和檢測有重大變更。 新的 ASP.NET 設定 API 可讓您以程式設計方式變更設定。 此外，有許多新的設定會允許新的設定和檢測。

ASP.NET 2.0 中的設定和檢測有重大變更。 新的 ASP.NET 設定 API 可讓您以程式設計方式變更設定。 此外，有許多新的設定會允許新的設定和檢測。

在此課程模組中，我們將討論 ASP.NET 與讀取和寫入 ASP.NET 設定檔相關的設定 API，而且我們也會介紹 ASP.NET 檢測。 我們也會討論 ASP.NET 追蹤中提供的新功能。

## <a name="aspnet-configuration-api"></a>ASP.NET 設定 API

ASP.NET 設定 API 可讓您使用單一程式設計介面來開發、部署和管理應用程式設定資料。 您可以使用設定 API，以程式設計方式開發和修改完整的 ASP.NET 設定，而不需要直接在設定檔中編輯 XML。 此外，您還可以在主控台應用程式和腳本中使用設定 API，在 Web 管理工具和 Microsoft Management Console （MMC）嵌入式管理單元中進行開發。

下列兩個設定管理工具會使用設定 API，並隨附于 .NET Framework 版本2.0：

- ASP.NET MMC 嵌入式管理單元，它會使用設定 API 來簡化管理工作，從設定階層的所有層級提供本機設定資料的整合式觀點。
- 網站管理工具，可讓您管理本機和遠端應用程式（包括裝載的網站）的配置設定。

ASP.NET 設定 API 包含一組 ASP.NET 管理物件，可讓您用來以程式設計的方式來設定網站和應用程式。 管理物件會實作為 .NET Framework Class Library。 設定 API 程式設計模型可在編譯時期強制執行資料類型，以確保程式碼的一致性和可靠性。 為了讓您更輕鬆地管理應用程式設定，設定 API 可讓您將從設定階層中所有點合併的資料視為單一集合，而不是以不同的個別集合形式來查看資料。設定檔。 此外，設定 API 可讓您操作整個應用程式設定，而不需要直接編輯設定檔中的 XML。 最後，API 會藉由支援系統管理工具（例如網站管理工具）來簡化設定工作。 設定 API 可支援在電腦上建立設定檔，並在多部電腦上執行設定腳本，以簡化部署。

> [!NOTE]
> 設定 API 不支援建立 IIS 應用程式。

## <a name="working-with-local-and-remote-configuration-settings"></a>使用本機和遠端設定

Configuration 物件代表套用至特定實體實體（如電腦）或邏輯實體（例如應用程式或網站）之設定的合併視圖。 指定的邏輯實體可以存在於本機電腦或遠端伺服器上。 當指定的實體沒有任何設定檔存在時，設定物件會代表 Machine.config 檔案所定義的預設設定。

您可以使用下列類別中的其中一個 open Configuration 方法來取得設定物件：

1. 如果您的實體是用戶端應用程式，則為 ConfigurationManager 類別。
2. 如果您的實體是 Web 應用程式，則為 WebConfigurationManager 類別。

這些方法會傳回設定物件，而後者會提供必要的方法和屬性來處理基礎的設定檔。 您可以存取這些檔案以進行讀取或寫入。

### <a name="reading"></a>讀取

您可以使用 GetSection 或 GetSectionGroup 方法來讀取設定資訊。 讀取的使用者或處理常式必須具有階層中所有設定檔的讀取權限。

> [!NOTE]
> 如果您使用採用 path 參數的靜態 GetSection 方法，path 參數必須參考程式碼執行所在的應用程式。 否則，會忽略參數，並傳回目前正在執行之應用程式的設定資訊。

### <a name="writing"></a>撰寫

您可以使用其中一個 Save 方法來寫入設定資訊。 寫入的使用者或處理常式必須具有目前設定階層層級之設定檔案和目錄的寫入權限，以及階層中所有設定檔的讀取權限。

若要產生代表所指定實體之繼承設定的設定檔，請使用下列其中一個儲存配置方法：

1. 用來建立新設定檔案的 Save 方法。
2. 在另一個位置產生新設定檔案的 SaveAs 方法。

## <a name="configuration-classes-and-namespaces"></a>設定類別和命名空間

許多設定類別和方法彼此類似。 下表描述最常使用的設定類別和命名空間。

| **設定類別或命名空間** | **說明** |
| --- | --- |
| [System. Configuration](https://msdn.microsoft.com/library/system.configuration.aspx)命名空間 | 包含所有 .NET Framework 應用程式的主要設定類別。 區段處理常式類別是用來從方法（例如 GetSection 和 GetSectionGroup）取得區段的設定資料。 這兩種方法不是靜態的。 |
| Configuration 類別 | 代表電腦、應用程式、Web 目錄或其他資源的一組設定資料。 此類別包含有用的方法（例如 GetSection 和 GetSectionGroup），可用來更新設定，以及取得區段和區段群組的參考。 這個類別是用來做為取得設計階段設定資料之方法的傳回型別，例如 WebConfigurationManager 和 ConfigurationManager 類別的方法。 |
| System.web. Configuration 命名空間 | 包含 ASP.NET 設定區段的區段處理常式類別，定義于[ASP.NET Configuration Settings](https://msdn.microsoft.com/library/b5ysx397.aspx)。 區段處理常式類別是用來從方法（例如 GetSection 和 GetSectionGroup）取得區段的設定資料。 |
| System.web. WebConfigurationManager 類別 | 提供實用的方法來取得執行時間和設計階段設定的參考。 這些方法會使用 System.object 做為傳回型別。 您可以交替使用這個類別的靜態 GetSection 方法，或 ConfigurationManager 類別的非靜態 GetSection 方法。 針對 Web 應用程式設定，建議使用 WebConfigurationManager 類別，而不是 ConfigurationManager 類別。 |
| [提供者](https://msdn.microsoft.com/library/system.configuration.provider.aspx)命名空間 | 提供自訂和擴充設定提供者的方法。 這是設定系統中所有提供者類別的基本類別。 |
| [System.web. Management](https://msdn.microsoft.com/library/system.web.management.aspx)命名空間 | 包含用來管理及監視 Web 應用程式健全狀況的類別和介面。 嚴格來說，此命名空間不會被視為設定 API 的一部分。 例如，追蹤和事件引發是由這個命名空間中的類別來完成。 |
| [System.web](https://msdn.microsoft.com/library/system.management.instrumentation.aspx)命名空間 | 提供應用程式檢測所需的類別，透過 Windows Management Instrumentation （WMI）向潛在取用者公開其管理資訊和事件。 ASP.NET 健全狀況監視會使用 WMI 來傳遞事件。 嚴格來說，此命名空間不會被視為設定 API 的一部分。 |

## <a name="reading-from-aspnet-configuration-files"></a>從 ASP.NET 設定檔讀取

WebConfigurationManager 類別是用來從 ASP.NET 設定檔讀取的核心類別。 基本上，有三個步驟可讀取 ASP.NET 設定檔：

1. 使用 OpenWebConfiguration 方法取得設定物件。
2. 取得設定檔中所需區段的參考。
3. 從設定檔讀取所需的資訊。

Configuration 物件代表不代表特定的設定檔。 相反地，它代表電腦、應用程式或網站設定的合併視圖。 下列程式碼範例會具現化設定物件，代表名為*ProductInfo*的 Web 應用程式的設定。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> 請注意，如果/ProductInfo 路徑不存在，則上述程式碼會傳回 machine.config 檔案中指定的預設設定。

擁有設定物件之後，您就可以使用 GetSection 或 GetSectionGroup 方法來深入探索設定。 下列範例會取得上述 ProductInfo 應用程式之模擬設定的參考：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>寫入 ASP.NET 設定檔案

如同從設定檔讀取，WebConfigurationManager 類別是寫入 Asp.NET 設定檔的核心。 寫入 ASP.NET 設定檔的步驟也有三個。

1. 使用 OpenWebConfiguration 方法取得設定物件。
2. 取得設定檔中所需區段的參考。
3. 使用 Save 或 SaveAs 方法，從設定檔案寫入所需的資訊。

下列程式碼會將 &lt;編譯&gt; 元素的**debug**屬性變更為 false：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

執行此程式碼時，會針對*webApp*應用程式的 web.config 檔案，將 &lt;編譯&gt; 元素的**debug**屬性設為 false。

## <a name="systemwebmanagement-namespace"></a>System.web. Management 命名空間

System.web 命名空間提供類別和介面，可用來管理和監視 ASP.NET 應用程式的健全狀況。

藉由定義將事件與提供者產生關聯的規則，即可完成記錄。 此規則會定義傳送給提供者的事件種類。 下列基底事件可供您記錄：

| **WebBaseEvent** | 所有事件的基底事件類別。 包含所有事件（例如事件程式碼、事件詳細資料、引發事件的日期和時間、序號、事件訊息和事件詳細資料）所需的屬性。 |
| --- | --- |
| **WebManagementEvent** | 管理事件的基底事件類別，例如應用程式存留期、要求、錯誤和 audit 事件。 |
| **WebHeartbeatEvent** | 應用程式定期產生的事件，用來捕捉有用的執行時間狀態資訊。 |
| **WebAuditEvent** | 安全性 audit 事件的基類，用來標示條件，例如授權失敗、解密失敗*等等。* |
| **WebRequestEvent** | 所有資訊要求事件的基類。 |
| **WebBaseErrorEvent** | 所有表示錯誤狀況之事件的基類。 |

可用的提供者類型可讓您將事件輸出傳送至事件檢視器、SQL Server、Windows Management Instrumentation （WMI）和電子郵件。 預先設定的提供者和事件對應會減少取得記錄事件輸出所需的工作量。

ASP.NET 2.0 會使用現成的事件記錄提供者，根據啟動和停止的應用程式域記錄事件，以及記錄任何未處理的例外狀況。 這有助於涵蓋一些基本案例。 例如，假設您的應用程式擲回例外狀況，但使用者不會儲存錯誤，而且您無法重現此問題。 使用預設的事件記錄檔規則，您可以收集例外狀況和堆疊資訊，以深入瞭解發生的錯誤類型。 如果您的應用程式遺失會話狀態，則會套用另一個範例。 在這種情況下，您可以查看事件記錄檔，以判斷應用程式域是否正在回收，以及為什麼應用程式域是在第一個位置停止的。

此外，健全狀況監視系統也是可擴充的。 例如，您可以定義自訂的 Web 事件、在應用程式內引發它們，然後定義規則以將事件資訊傳送給提供者（例如您的電子郵件）。 這可讓您輕鬆地將檢測與健全狀況監視提供者結合。 另舉一個例子，您可以在每次處理訂單時引發事件，並設定一個規則，將每個事件傳送至 SQL Server 資料庫。 當使用者無法在資料列中登入多次時，您也可以引發事件，並設定事件以使用以電子郵件為基礎的提供者。

預設提供者和事件的設定會儲存在全域 Web.config 檔案中。 全域 web.config 檔案會將儲存在 machine.config 檔案中的所有網頁型設定儲存在 ASP.NET 1x 中。 全域 web.config 檔案位於下列目錄：

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

全域 Web.config 檔案的 &lt;healthMonitoring&gt; 區段會提供預設的設定。 您可以藉由在應用程式的 web.config 檔案中，執行 &lt;healthMonitoring&gt; 區段來覆寫這些設定或設定您自己的設定。

全域 Web.config 檔案的 &lt;healthMonitoring&gt; 區段包含下列專案：

| **提供者** | 包含為事件檢視器、WMI 和 SQL Server 設定的提供者。 |
| --- | --- |
| **Healthmonitoring 之 eventmappings** | 包含各種 WebBase 類別的對應。 如果您產生自己的事件類別，可以擴充此清單。 產生您自己的事件類別，可讓您更精確地處理您傳送資訊的提供者。 例如，您可以設定要傳送至 SQL Server 的未處理例外狀況，同時將您自己的自訂事件傳送至電子郵件。 |
| **條** | 將 Healthmonitoring 之 eventmappings 連結至提供者。 |
| **緩衝** | 與 SQL Server 和電子郵件提供者搭配使用，以決定將事件排清至提供者的頻率。 |

以下是來自全域 Web.config 檔案的程式碼範例。

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>如何將事件儲存至事件檢視器

如先前所述，在全域 Web.config 檔案中，會為您設定在事件檢視器中記錄事件的提供者。 根據預設，系統會記錄以**WebBaseErrorEvent**和**WebFailureAuditEvent**為基礎的所有事件。 您可以新增其他規則，以將其他資訊記錄到事件記錄檔。 例如，如果您想要記錄所有事件（也就是以**WebBaseEvent**為*基礎的每*個事件），您可以將下列規則新增至 web.config 檔案：

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

此規則會將 [**所有事件**] 事件對應連結至事件記錄檔提供者。 EventMapping 和提供者都包含在全域 Web.config 檔案中。

## <a name="how-to-store-events-to-sql-server"></a>如何將事件儲存至 SQL Server

這個方法會使用**aspnetdb.mdf**資料庫，這是由 Aspnet\_regsql 所產生。 預設的提供者會使用 LocalSqlServer 連接字串，其使用應用程式中以檔案為基礎的資料庫\_data 資料夾或 SQL Server 的本機 SQLExpress 實例。 LocalSqlServer 連接字串和 SqlProvider 都是在全域 web.config 檔案中設定。

全域 Web.config 檔案中的 LocalSqlServer 連接字串看起來像這樣：

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

如果您想要使用另一個 SQL Server 實例，您必須使用 Aspnet\_regsql，此工具可在%windir%\Microsoft.Net\Framework\v2.0. 中找到。\* 資料夾。 使用 Aspnet\_regsql 工具，在 SQL Server 實例上產生自訂**aspnetdb.mdf**資料庫，然後將連接字串新增至您的應用程式佈建檔，然後使用新的連接字串新增提供者。 建立**aspnetdb.mdf**資料庫之後，您必須設定規則，將 eventMapping 連結到 sqlProvider。

無論您是使用預設 SqlProvider 或設定自己的提供者，都必須新增連結提供者與事件對應的規則。 下列規則會將您先前建立的新提供者連結至 [**所有事件**] 事件對應。 此規則會記錄以**WebBaseEvent**為基礎的所有事件，並將它們傳送至將使用 MYASPNETDB 連接字串的 MySqlWebEventProvider。 下列程式碼會新增規則，以將提供者與事件對應連結：

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

如果您只想要將錯誤傳送至 SQL Server，您可以新增下列規則：

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>如何將事件轉送至 WMI

您也可以將事件轉送至 WMI。 預設會在全域 Web.config 檔案中為您設定 WMI 提供者。

下列程式碼範例會新增規則，以將事件轉送至 WMI：

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

您必須新增規則，以將 eventMapping 與提供者產生關聯，以及使用 WMI 接聽程式應用程式來接聽事件。 下列程式碼範例會新增規則，以將 WMI 提供者連結至 [**所有事件**] 事件對應：

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>如何將事件轉寄至電子郵件

您也可以將事件轉寄至電子郵件。 請留意您對應到電子郵件提供者的事件規則，因為您可能會不小心傳送許多可能較適合 SQL Server 或事件記錄檔的資訊。 有兩個電子郵件提供者;SimpleMailWebEventProvider 和 TemplatedMailWebEventProvider。 每個都具有相同的設定屬性，但「範本」和「detailedTemplateErrors」屬性除外，這兩者都只能在 TemplatedMailWebEventProvider 上使用。

> [!NOTE]
> 這兩個電子郵件提供者都不會為您設定。 您必須將它們新增至您的 web.config 檔案。

這兩個電子郵件提供者的主要差異在於，SimpleMailWebEventProvider 會在無法修改的一般範本中傳送電子郵件。 範例 Web.config 檔案會使用下列規則，將此電子郵件提供者新增至已設定的提供者清單：

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

也會新增下列規則，以將電子郵件提供者系結至 [**所有事件**] 事件對應：

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 追蹤

ASP.NET 2.0 中的追蹤有三個主要增強功能。

1. 整合式追蹤功能
2. 以程式設計方式存取追蹤訊息
3. 改良的應用層級追蹤

## <a name="integrated-tracing-functionality"></a>整合式追蹤功能

您現在可以將由 ASP.NET 追蹤發出的訊息路由傳送至 ASP.NET 追蹤輸出，並將這些訊息路由傳送至診斷。 您也可以將 ASP.NET 檢測事件轉送到 System.webserver。 這項功能是由 &lt;trace&gt; 元素的新**writetodiagnosticstrace 還**屬性所提供。 當此布林值為 true 時，ASP.NET 追蹤訊息會轉送到系統診斷追蹤基礎結構，供任何已註冊顯示追蹤訊息的接聽程式使用。

## <a name="programmatic-access-to-trace-messages"></a>以程式設計方式存取追蹤訊息

ASP.NET 2.0 允許透過**TraceCoNtextRecord**類別和**TraceRecords**集合以程式設計方式存取所有追蹤訊息。 存取追蹤訊息最有效率的方式是註冊**TraceCoNtextEventHandler**委派（也是 ASP.NET 2.0 中的新功能），以處理新的**tracecoNtext.tracefinished**事件。 然後您可以視需要對追蹤訊息進行迴圈。

下列程式碼範例將說明這種情況：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

在上述範例中，我會在 TraceRecords 集合中執行迴圈，然後將每個訊息寫入回應資料流程。

## <a name="improved-application-level-tracing"></a>改良的應用層級追蹤

透過引進 &lt;trace&gt; 元素的新**mostRecent**屬性，即可改善應用層級的追蹤。 這個屬性會指定是否要顯示最新的應用層級追蹤輸出，以及是否捨棄 requestLimit 所指示之限制以外的較舊追蹤資料。 若為 false，則會顯示要求的追蹤資料，直到達到 requestLimit 屬性為止。

## <a name="aspnet-command-line-tools"></a>ASP.NET 命令列工具

有數個命令列工具可協助設定 ASP.NET。 ASP.NET 開發人員應該熟悉 aspnet\_的 regiis 工具。 ASP.NET 2.0 提供其他三個命令列工具來協助設定。

下列是可用的命令列工具：

| **工具** | **使用** |
| --- | --- |
| **aspnet\_regiis .exe** | 允許以 IIS 註冊 ASP.NET。 此工具有兩個版本，隨附于 ASP.NET 2.0，一個用於32位系統（在架構資料夾中），另一個用於64位系統（在 Framework64 資料夾中）。64位版本將不會安裝在32位作業系統上。 |
| **aspnet\_regsql .exe** | ASP.NET SQL Server 註冊工具是用來建立 Microsoft SQL Server 資料庫，供 ASP.NET 中的 SQL Server 提供者使用，或是從現有的資料庫新增或移除選項。 Aspnet\_regsql 檔案位於 Web 服務器的 [drive：] \WINDOWS\Microsoft.NET\Framework\versionNumber 資料夾中。 |
| **aspnet\_regbrowsers .exe** | ASP.NET 瀏覽器註冊工具會剖析所有全系統瀏覽器定義，並將其編譯成元件，並將元件安裝到全域組件快取中。 此工具會使用瀏覽器定義檔案（。瀏覽器檔案 .NET Framework）。 此工具可在%SystemRoot%\Microsoft.NET\Framework\version\ 目錄中找到。 |
| **aspnet\_編譯器 .exe** | ASP.NET 編譯工具可讓您就地編譯 ASP.NET Web 應用程式，或將其部署至目標位置（例如實際伺服器）。 就地編譯有助於應用程式效能，因為終端使用者在編譯應用程式時，對應用程式的第一個要求不會有延遲。 |

因為 aspnet\_regiis 工具不是 ASP.NET 2.0 的新手，所以我們不會在這裡討論。

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL Server 註冊工具-aspnet\_regsql .exe

您可以使用 ASP.NET SQL Server 註冊工具來設定數種類型的選項。 您可以指定 SQL 連接，指定哪些 ASP.NET 應用程式服務會使用 SQL Server 來管理資訊、指出用於 SQL 快取相依性的資料庫或資料表，以及新增或移除使用 SQL Server 來儲存程式和會話狀態的支援。

有數個 ASP.NET 應用程式服務依賴提供者來管理從資料來源儲存和抓取資料。 每個提供者都是資料來源特有的。 ASP.NET 包含下列 ASP.NET 功能的 SQL Server 提供者：

- 成員資格（ [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)類別）。
- 角色管理（ [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)類別）。
- Profile （ [SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)類別）。
- Web 組件個人化（ [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)類別）。
- Web 事件（ [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)類別）。

當您安裝 ASP.NET 時，伺服器的 machine.config 檔案會包含設定元素，這些專案會針對依賴提供者的每個 ASP.NET 功能指定 SQL Server 提供者。 根據預設，這些提供者會設定為連接到 SQL Server Express 2005 的本機使用者實例。 如果您變更了提供者所使用的預設連接字串，則在您可以使用電腦設定中設定的任何 ASP.NET 功能之前，您必須使用 Aspnet\_regsql，為您選擇的功能安裝 SQL Server 資料庫和資料庫元素。 如果您使用 SQL 註冊工具指定的資料庫不存在（如果命令列上未指定，則 aspnetdb.mdf 會是預設的資料庫），則目前的使用者必須擁有在 SQL Server 中建立資料庫的許可權，以及建立架構 e資料庫內的 lements。

### <a name="sql-cache-dependency"></a>SQL 快取相依性

ASP.NET 輸出快取的一項先進功能是 SQL 快取相依性。 SQL 快取相依性支援兩種不同的作業模式：一個使用資料表輪詢的 ASP.NET 執行，另一個使用 SQL Server 2005 的查詢通知功能的第二種模式。 SQL 註冊工具可以用來設定作業的資料表輪詢模式。

### <a name="session-state"></a>工作階段狀態

根據預設，會話狀態值和資訊會儲存在 ASP.NET 程式的記憶體中。 或者，您也可以將會話資料儲存在 SQL Server 資料庫中，以供多部 Web 服務器共用。 如果您針對具有 SQL 註冊工具的會話狀態所指定的資料庫不存在，則目前的使用者必須擁有在 SQL Server 中建立資料庫的許可權，以及在資料庫內建立架構元素的許可權。 如果資料庫存在，則目前的使用者必須擁有在現有資料庫中建立架構元素的許可權。

若要在 SQL Server 上安裝會話狀態資料庫，請執行 Aspnet\_regsql 工具，並使用命令提供下列資訊：

- 使用 **-S**選項的 SQL Server 實例的名稱。
- 具有在執行 SQL Server 的電腦上建立資料庫之許可權的帳戶登入認證。 使用 **-E**選項來使用目前登入的使用者，或使用 **-U**選項來指定使用者識別碼以及 **-P**選項來指定密碼。
- **-Ssadd**命令列選項，用以新增會話狀態資料庫。

根據預設，您無法使用 Aspnet\_regsql，在執行 SQL Server 2005 Express Edition 的電腦上安裝會話狀態資料庫。

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET 瀏覽器註冊工具-aspnet\_regbrowsers

在 ASP.NET 版本1.1 中，Machine.config 檔案包含一個稱為 &lt;browserCaps&gt;的區段。 本章節包含一系列的 XML 專案，這些專案會根據正則運算式定義各種瀏覽器的設定。 針對 ASP.NET 版本2.0，這是新的。瀏覽器檔案使用 XML 專案定義特定瀏覽器的參數。 您可以藉由加入新的，在新的瀏覽器上加入資訊。瀏覽器檔案至位於系統上%SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers 的資料夾。

因為應用程式在每次需要瀏覽器資訊時都不會讀取 .config 檔案，所以您可以建立新的。瀏覽器檔案並執行 Aspnet\_regbrowsers，將必要的變更新增至元件。 如此一來，伺服器就可以立即存取新的瀏覽器資訊，因此您不需要關閉任何應用程式來收取資訊。 應用程式可以透過目前 HttpRequest 的 Browser 屬性來存取瀏覽器功能。

執行 aspnet\_regbrowser 時，可以使用下列選項：

| **選項** | **說明** |
| --- | --- |
| **-?** | 在命令視窗中顯示 Aspnet\_regbbrowsers 的解說文字。 |
| **-i** | 建立執行時間瀏覽器功能元件，並將它安裝在全域組件快取中。 |
| **-u** | 從全域組件快取卸載執行時間瀏覽器功能元件。 |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET 編譯工具-aspnet\_編譯器 .exe

ASP.NET 編譯工具可以用兩種一般方式來使用：適用于部署的就地編譯和編譯，其中指定了目標輸出目錄。

### <a name="compiling-an-application-in-place"></a>[就地編譯應用程式](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET 編譯工具可以就地編譯應用程式，也就是說，它會模擬對應用程式提出多個要求的行為，因而導致一般編譯。 預先編譯網站的使用者不會因為第一次要求而編譯頁面而遇到延遲。

當您就地預先編譯網站時，適用下列專案：

- 網站會保留其檔案和目錄結構。
- 您必須擁有伺服器上網站所使用之所有程式設計語言的編譯器。
- 如果任何檔案編譯失敗，整個網站就無法編譯。

您也可以在將應用程式新增至新的來源檔案後，就地重新編譯。 此工具只會編譯新的或已變更的檔案，除非您包含 **-c**選項。

> [!NOTE]
> 編譯包含嵌套應用程式的應用程式時，不會編譯該嵌套應用程式。 必須個別編譯此嵌套應用程式。

### <a name="compiling-an-application-for-deployment"></a>[編譯應用程式以進行部署](https://msdn.microsoft.com/library/ms229863.aspx)

您可以藉由指定 targetDir 參數，編譯用於部署的應用程式（編譯至目標位置）。 TargetDir 可以是 Web 應用程式的最終位置，也可以進一步部署已編譯的應用程式。 使用 **-u**選項會編譯應用程式，讓您可以對編譯過的應用程式中的某些檔案進行變更，而不需要重新編譯。 Aspnet\_cmd.exe 會區分靜態和動態檔案類型，而且在建立產生的應用程式時，會以不同的方式處理它們。

- 靜態檔案類型是沒有相關聯編譯器或組建提供者的檔案，例如名為的檔案具有副檔名，例如 .css、.gif、.htm、.html、.jpg、.js 等等。 這些檔案只會複製到目標位置，並保留它們在目錄結構中的相對位置。
- 動態檔案類型是具有相關聯編譯器或組建提供者的檔案，包括具有 ASP.NET 特定副檔名的檔案，例如 global.asax、.ascx、ashx、.aspx、browser、.master 等等。 ASP.NET 編譯工具會從這些檔案產生元件。 如果省略 **-u**選項，此工具也會建立副檔名為的檔案。已進行編譯，將原始來源檔案對應至其元件。 為了確保保留應用程式來源的目錄結構，此工具會在目標應用程式的對應位置中產生預留位置檔案。

您必須使用 **-u**選項來表示已編譯之應用程式的內容可以修改。 否則，會忽略後續的修改或造成執行階段錯誤。

下表描述當包含 **-u**選項時，ASP.NET 編譯工具如何處理不同的檔案類型。

| **檔案類型** | **編譯器動作** |
| --- | --- |
| .ascx、.aspx、.master | 這些檔案會分割成標記和原始程式碼，其中包含程式碼後置檔案，以及 &lt;script runat = "server"&gt; 元素中的任何程式碼。 原始程式碼會編譯成元件，其名稱是衍生自雜湊演算法，而元件則放在 Bin 目錄中。 任何內嵌程式碼（也就是包含在 **&lt;%** 和 **%&gt;** 方括弧之間的程式碼）都會包含在標記中，而且不會進行編譯。 系統會建立與來源檔案相同名稱的新檔案，以包含標記並放在對應的輸出目錄中。 |
| . ashx，.asmx | 這些檔案不會進行編譯，而且會依其方式移至輸出目錄，而不會進行編譯。 如果您想要編譯器代碼，請將程式碼放入原始程式碼檔案的應用程式\_Code 目錄中。 |
| .cs、.vb、. form1.jsl、.cpp （不包含先前所列檔案類型的程式碼後置檔案） | 這些檔案會進行編譯，並以資源的形式包含在參考它們的元件中。 來源檔案不會複製到輸出目錄。 如果未參考程式碼檔案，則不會進行編譯。 |
| 自訂檔案類型 | 這些檔案不會經過編譯。 這些檔案會複製到對應的輸出目錄。 |
| 應用程式\_代碼子目錄中的原始程式碼檔 | 這些檔案會編譯成元件並放在 Bin 目錄中。 |
| 應用程式\_GlobalResources 子目錄中的 .resx 和資源檔 | 這些檔案會編譯成元件並放在 Bin 目錄中。 在主要輸出目錄底下不會建立任何應用程式\_GlobalResources 子目錄，且來原始目錄中的 .resx 或 .resources 檔案不會複製到輸出目錄。 |
| 應用程式\_LocalResources 子目錄中的 .resx 和資源檔 | 這些檔案不會進行編譯，並且會複製到對應的輸出目錄。 |
| 應用程式中的 .skin 檔案\_主題子目錄 | 不會編譯該檔案和靜態主題檔案，並將其複製到對應的輸出目錄。 |
| 。 browser 的 web.config 靜態檔案類型元件已存在於 Bin 目錄中 | 這些檔案會依原樣複製到輸出目錄。 |

下表描述當省略 **-u**選項時，ASP.NET 編譯工具如何處理不同的檔案類型。

| **檔案類型** | **編譯器動作** |
| --- | --- |
| .aspx、.asmx、ashx、.master | 這些檔案會分割成標記和原始程式碼，其中包含程式碼後置檔案，以及 &lt;script runat = "server"&gt; 元素中的任何程式碼。 原始程式碼會編譯成元件，其名稱是從雜湊演算法衍生而來。 產生的元件會放在 Bin 目錄中。 任何內嵌程式碼（也就是包含在 **&lt;%** 和 **%&gt;** 方括弧之間的程式碼）都會包含在標記中，而且不會進行編譯。 編譯器會建立新的檔案，以包含名稱與來源檔案相同的標記。 這些產生的檔案會放在 Bin 目錄中。 編譯器也會建立與原始檔同名但副檔名為的檔案。已編譯，其中包含對應資訊。 該.編譯的檔案會放在輸出目錄中，並對應至來源檔案的原始位置。 |
| .ascx | 這些檔案會分割成標記和原始碼。 原始程式碼會編譯成元件並放在 Bin 目錄中，其名稱衍生自雜湊演算法。 不會產生任何標記檔案。 |
| .cs、.vb、. form1.jsl、.cpp （不包含先前所列檔案類型的程式碼後置檔案） | 從 .ascx、. ashx 或 .aspx 檔案所產生的元件所參考的原始程式碼會編譯成元件並放在 Bin 目錄中。 不會複製任何來源檔案。 |
| 自訂檔案類型 | 這些檔案會進行編譯，就像動態檔案一樣。 根據它們所根據的檔案類型，編譯器可以將對應檔放在輸出目錄中。 |
| 應用程式中的檔案\_代碼子目錄 | 這個子目錄中的原始程式碼檔會編譯成元件並放在 Bin 目錄中。 |
| 應用程式中的檔案\_GlobalResources 子目錄 | 這些檔案會編譯成元件並放在 Bin 目錄中。 主要輸出目錄底下不會建立任何應用程式\_GlobalResources 子目錄。 如果設定檔指定 appliesTo = "All"，.resx 和 .resources 檔案就會複製到輸出目錄。 如果[BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)參考它們，則不會複製它們。 |
| 應用程式\_LocalResources 子目錄中的 .resx 和資源檔 | 這些檔案會編譯成具有唯一名稱並放在 Bin 目錄中的元件。 不會將 .resx 或. 資源檔案複製到輸出目錄。 |
| 應用程式中的 .skin 檔案\_主題子目錄 | 主題會編譯成元件並放在 Bin 目錄中。 系統會為 .skin 檔案建立 Stub 檔案，並將其放在對應的輸出目錄中。 靜態檔案（例如 .css）會複製到輸出目錄。 |
| 。 browser 的 web.config 靜態檔案類型元件已存在於 Bin 目錄中 | 這些檔案會依原樣複製到輸出目錄。 |

### <a name="fixed-assembly-names"></a>[固定的元件名稱](https://msdn.microsoft.com/library/ms229863.aspx##)

在某些情況下，例如使用 MSI Windows Installer 部署 Web 應用程式，需要使用一致的檔案名和內容，以及一致的目錄結構，以識別更新的元件或配置設定。 在這些情況下，您可以使用 **-fixednames**選項，指定 ASP.NET 編譯工具應針對每個原始程式檔編譯元件，而不是使用將多個頁面編譯成元件的。 這可能會導致大量的元件，因此如果您擔心擴充性，您應該謹慎使用此選項。

### <a name="strong-name-compilation"></a>[強式名稱編譯](https://msdn.microsoft.com/library/ms229863.aspx##)

提供 **-aptca**、 **-delaysign**、 **-keycontainer**和 **-Keyfile**選項，讓您可以使用 Aspnet\_cmd.exe 來建立強式名稱的元件，而不需分別使用[強式名稱工具（sn.exe）](https://msdn.microsoft.com/library/k5b5tt23.aspx) 。 這些選項分別對應至**AllowPartiallyTrustedCallersAttribute**、 **AssemblyDelaySignAttribute**、 **AssemblyKeyNameAttribute**和**AssemblyKeyFileAttribute**。

這些屬性的討論不在此課程的範圍內。

## <a name="labs"></a>實驗室

下列實驗室都是以先前的實驗室為基礎。 您將需要依序執行。

## <a name="lab-1-using-the-configuration-api"></a>實驗室1：使用設定 API

1. 建立名為*mod9lab*的新網站。
2. 將新的 Web 設定檔新增至網站。
3. 將下列內容新增至 web.config 檔案：

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

這可確保您擁有儲存 web.config 檔案變更的許可權。

1. 將新的標籤控制項加入至 default.aspx，並將識別碼變更為**lblDebugStatus**。
2. 將新的按鈕控制項加入 default.aspx。
3. 將按鈕控制項的 ID 變更為**btnToggleDebug** ，並將文字變更為**切換偵錯工具狀態**。
4. 開啟 default.aspx 的程式碼後置檔案的程式碼片段，並為**system.web. Configuration**新增**using**語句，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 將兩個私用變數新增至類別，並將頁面\_Init 方法，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 將下列程式碼新增至頁面\_載入：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 儲存並流覽 default.aspx。 請注意，標籤控制項會顯示目前的「偵錯工具」狀態。
2. 按兩下設計工具中的 [Button] 控制項，然後將下列程式碼加入按鈕控制項的 Click 事件中：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 儲存並流覽 default.aspx，然後按一下按鈕。
2. 在每個按鈕按一下後開啟 web.config 檔案，並觀察 &lt;編譯&gt; 區段中的**debug**屬性。

## <a name="lab-2-logging-application-restarts"></a>實驗室2：記錄應用程式重新開機

在此實驗室中，您將建立可讓您在事件檢視器中切換應用程式關閉、重新開機和重新編譯記錄的程式碼。

1. 將 DropDownList 新增至 default.aspx，並將識別碼變更為 ddlLogAppEvents。
2. 將 DropDownList 的**AutoPostBack**屬性設定為**true**。
3. 將三個專案新增至 DropDownList 的 Items 集合。 將第一個專案的**文字***選取值*，並將值設為-1。 將第二個專案的**文字**和**值**設**為 True** ，並將第三個專案的**文字**和**值**設**為 False**。
4. 將新的標籤加入 default.aspx。 將識別碼變更為**lblLogAppEvents**。
5. 開啟 default.aspx 的程式碼後置視圖，並為 HealthMonitoringSection 類型的變數加入新的宣告，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 將下列程式碼新增至頁面\_Init 中的現有程式碼：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. 按兩下 DropDownList，並將下列程式碼新增至 SelectedIndexChanged 事件：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. 流覽 default.aspx。
2. 將下拉式清單設定為**False**。
3. 清除事件檢視器中的應用程式記錄檔。
4. 按一下此按鈕，即可變更應用程式的 Debug 屬性。
5. 重新整理事件檢視器中的應用程式記錄檔。 

    1. 是否已記錄任何事件？
    2. 為何或為什麼不這麼做？
6. 將下拉式清單設定為 [ **True]。**
7. 按一下按鈕以切換應用程式的 Debug 屬性。
8. 重新整理應用程式登入事件檢視器。 

    1. 是否已記錄任何事件？
    2. 應用程式關閉的原因為何？
9. 試驗開啟和關閉記錄，並查看對 web.config 檔案所做的變更。

## <a name="more-information"></a>其他相關資訊：

ASP.NET 2.0 的提供者模型可讓您建立自己的提供者，不僅適用于應用程式檢測，還有其他許多用途，例如成員資格、設定檔等。如需撰寫自訂提供者以將應用程式事件記錄到文字檔的詳細資訊，請造訪[此連結](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)。
