---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 監視和遙測（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: 44941c9fd0dcd3223604fc4a4f2836f587578acb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585622"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>監視和遙測（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

有很多人會依賴客戶，讓他們知道他們的應用程式何時關閉。 這不是任何地方的最佳作法，尤其是不在雲端中。 並不保證快速通知，而當您收到通知時，您通常會得到最小或誤導的資料，告訴您發生了什麼事。 有了良好的遙測和記錄系統，您就可以瞭解應用程式的運作狀況，而當發生問題時，您會立即找出並提供有用的疑難排解資訊來處理。

## <a name="buy-or-rent-a-telemetry-solution"></a>購買或出租遙測解決方案

> [!NOTE]
> 這篇文章是在[Application Insights](/azure/application-insights/app-insights-overview)發行之前撰寫的。 Application Insights 是 Azure 上遙測解決方案的慣用方法。 如需詳細資訊，請參閱[設定 ASP.NET 網站的 Application Insights](/azure/application-insights/app-insights-asp-net) 。

雲端環境最棒的其中一件事，就是很容易購買或出租您的勝利。 遙測是一個範例。 如果沒有這麼多工作，您可以將真正好用的遙測系統啟動並執行，以非常符合成本效益的方式運作。 有許多與 Azure 整合的絕佳合作夥伴，其中有些有免費層，因此您可以取得基本遙測資料，而不需要進行任何動作。 以下只是 Azure 上目前可用的幾個：

- [新增 New relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#)也包含監視功能。

我們會快速逐步解說如何設定新的 New relic，以顯示使用遙測系統有多容易。

在 Azure 管理入口網站中，註冊服務。 按一下 [**新增**]，然後按一下 [**儲存**]。 [**選擇附加**元件] 對話方塊隨即出現。 向下 New relic，然後按一下 [**新增**]。

![選擇附加元件](monitoring-and-telemetry/_static/image1.png)

按一下向右箭號，然後選擇您想要的服務層級。 在此示範中，我們將使用免費層。

![個人化附加元件](monitoring-and-telemetry/_static/image2.png)

按一下向右箭號，確認 [購買]，新的 New relic 現在會在入口網站中顯示為附加元件。

![審查購買](monitoring-and-telemetry/_static/image3.png)

![在入口網站中新增 New relic 附加元件](monitoring-and-telemetry/_static/image4.png)

按一下 [**連接資訊**]，然後複製授權金鑰。

![連接資訊](monitoring-and-telemetry/_static/image5.png)

在入口網站中，移至 web 應用程式的 [**設定**] 索引標籤，將 [**效能監視**] 設定為 [**附加**元件]，然後將 [**選擇附加**元件] 下拉式清單設定為 [**新 new relic**]。 然後按一下 [**儲存**]。

![[設定] 索引標籤中的新 New relic](monitoring-and-telemetry/_static/image6.png)

在 Visual Studio 中，在您的應用程式中安裝新的 New relic NuGet 套件。

![[設定] 索引標籤中的開發人員分析](monitoring-and-telemetry/_static/image7.png)

將應用程式部署至 Azure，並開始使用它。 建立幾個 Fix It 工作，以提供一些活動讓新的 New relic 監視。

然後返回入口網站的 [**附加**元件] 索引標籤中的 [**新增 new relic** ] 頁面，然後按一下 [**管理**]。 入口網站會將您傳送至新的 New relic 管理入口網站，使用單一登入進行驗證，因此您不需要再次輸入認證。 [總覽] 頁面會顯示各種效能統計資料。 （按一下影像以查看完整大小的 [總覽] 頁面）。

[![新的 New relic 監視 索引標籤](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

以下是您可以看到的幾個統計資料：

- 一天中不同時間的平均回應時間。

    ![回應時間](monitoring-and-telemetry/_static/image10.png)
- 一天中不同時間的輸送量速率（以每分鐘的要求數計算）。

    ![輸送量](monitoring-and-telemetry/_static/image11.png)
- 處理不同 HTTP 要求所花費的伺服器 CPU 時間。

    ![Web 交易時間](monitoring-and-telemetry/_static/image12.png)
- 應用程式代碼的不同部分所花費的 CPU 時間：

    ![追蹤詳細資料](monitoring-and-telemetry/_static/image13.png)
- 歷程記錄效能統計資料。

    ![歷程記錄效能](monitoring-and-telemetry/_static/image14.png)
- 對外部服務的呼叫，例如 Blob 服務，以及有關服務的可靠和回應程度的統計資料。

    ![外部服務](monitoring-and-telemetry/_static/image15.png)

    ![外部服務](monitoring-and-telemetry/_static/image16.png)

    ![外部服務](monitoring-and-telemetry/_static/image17.png)
- 有關全球何處或美國 web 應用程式流量來自何處的資訊。

    ![地理位置](monitoring-and-telemetry/_static/image18.png)

您也可以設定報表和事件。 例如，您可以在每次開始看到錯誤時，傳送電子郵件給警示支援人員以解決問題。

![報表](monitoring-and-telemetry/_static/image19.png)

新的 New relic 只是遙測系統的其中一個範例;您也可以從其他服務取得所有此項。 雲端的優點是，不需要撰寫任何程式碼，而且最少或完全沒有費用，因此您突然可以取得更多有關應用程式的使用方式，以及您的客戶實際遇到的資訊。

<a id="log"></a>
## <a name="log-for-insight"></a>記錄以深入解析

遙測封裝是一個很好的第一個步驟，但您仍然必須檢測自己的程式碼。 遙測服務會在發生問題時通知您，並告訴您客戶所遇到的情況，但可能不會讓您深入瞭解程式碼中的狀況。

您不想要遠端進入生產伺服器，以查看您的應用程式正在執行的作業。 當您有一部伺服器時，這可能很實用，但當您擴充到數百部伺服器，而您不知道需要遠端執行哪些作業時，該怎麼辦？ 您的記錄應該提供足夠的資訊，讓您永遠都不需要從遠端進入實際執行伺服器來分析和偵測問題。 您應該記錄足夠的資訊，讓您可以只透過記錄來隔離問題。

### <a name="log-in-production"></a>登入生產環境

有很多人只有在發生問題而想要進行 debug 時，才會在生產環境中開啟追蹤。 這可能會在您注意到問題的時間與取得有用的疑難排解資訊的時間之間產生明顯的延遲。 而您取得的資訊對於間歇錯誤可能不會有説明。

在雲端環境中，我們建議的儲存體成本較低，因為您一律會在生產環境中保留登入。 如此一來，當錯誤發生時，您就已經記錄了，而且您有歷程記錄資料，可協助您分析隨著時間而開發的問題，或在不同時間定期發生。 您可以將清除程式自動化以刪除舊的記錄檔，但您可能會發現設定這類程式比保留記錄更耗費資源。

相較于疑難排解時間和成本，您可以在發生問題時，讓所需的所有資訊都可供使用，而增加的記錄成本也很簡單。 然後，當有人告訴您，他們在過去晚上8:00 時有隨機的錯誤，但他們並不記得該錯誤，您可以輕易地找出問題所在。

每月不到 $4，您可以保留 50 gb 的記錄檔，而記錄的效能影響很簡單，因為您必須記住一件事--為了避免效能瓶頸，請確定您的記錄程式庫是非同步。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>區分記錄檔，以從需要採取動作的記錄來通知

記錄檔的目的是要通知（我希望您知道某專案）或 ACT （我想要做一些事）。 請小心，只針對真的需要人員或自動化程式採取行動的問題撰寫 ACT 記錄。 有太多 ACT 記錄會造成雜訊，需要太多工來進行全部的檢查，以找出真正的問題。 而且，如果您的 ACT 記錄自動觸發某些動作，例如傳送電子郵件給支援人員，請避免單一問題觸發數以千計的這類動作。

在 .NET 的診斷追蹤中，可以指派錯誤、警告、資訊和 Debug/Verbose 層級的記錄。 您可以保留 ACT 記錄的錯誤層級，並使用較低層級的通知記錄，來區別來自通知記錄的 ACT。

![記錄層級](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>在執行時間設定記錄層級

雖然可以在生產環境中記錄永遠開啟，但另一個最佳作法是執行記錄架構，讓您在執行時間調整您所記錄的詳細資料層級，而不需要重新部署或重新開機您的應用程式。 例如，當您在 `System.Diagnostics` 中使用追蹤設備時，可以建立錯誤、警告、資訊和 Debug/Verbose 記錄。 我們建議您一律在生產環境中記錄錯誤、警告和資訊記錄，而且您會想要能夠動態新增 Debug/Verbose 記錄，以進行逐案例的疑難排解。

Azure App Service 中的 Web Apps 具有將 `System.Diagnostics` 記錄寫入檔案系統、資料表儲存體或 Blob 儲存體的內建支援。 您可以為每個儲存體目的地選取不同的記錄層級，而且可以即時變更記錄層級，而不必重新開機應用程式。 Blob 儲存體支援可讓您更輕鬆地在應用程式記錄上執行[hdinsight](https://docs.microsoft.com/azure/hdinsight/)分析工作，因為 hdinsight 知道如何直接使用 Blob 儲存體。

### <a name="log-exceptions"></a>記錄例外狀況

不要單純放入*例外狀況。* 記錄程式碼中的 ToString （）。 這會留下內容相關資訊。 在發生 SQL 錯誤的情況下，它會留下 SQL 錯誤號碼。 針對所有例外狀況，包括內容資訊、例外狀況本身和內部例外狀況，以確保您提供疑難排解所需的所有專案。 例如，內容資訊可能包括伺服器名稱、交易識別碼，以及使用者名稱（而不是密碼或任何秘密！）。

如果您依賴每一位開發人員來進行例外狀況記錄的正確動作，其中有些是不會的。 為了確保每次都能以正確的方式執行，請將例外狀況處理直接放在記錄器介面中：將例外狀況物件本身傳遞至記錄器類別，並在記錄器類別中正確記錄例外狀況資料。

### <a name="log-calls-to-services"></a>記錄對服務的呼叫

我們強烈建議您在每次應用程式向外呼叫服務時（不論是在資料庫或 REST API 或任何外部服務）時，撰寫記錄檔。 您的記錄中不只會包含成功或失敗的指示，而是每個要求所花費的時間。 在雲端環境中，您通常會看到與緩慢的問題相關的問題，而不是完全中斷。 通常需要10毫秒的時間可能會突然開始花上一秒鐘。 當有人告訴您您的應用程式速度變慢時，您希望能夠查看新的 New relic 或您擁有的任何遙測服務並驗證其經驗，然後您想要能夠查看自己的記錄，以深入瞭解為什麼速度變慢的細節。

### <a name="use-an-ilogger-interface"></a>使用 ILogger 介面

當您建立生產應用程式時，我們建議您建立一個簡單的*ILogger*介面，並將其中的一些方法保持在其中。 這可讓您在稍後輕鬆變更記錄執行，而不需要逐一查看所有程式碼。 我們可以在整個修正 It 應用程式中使用 `System.Diagnostics.Trace` 類別，但我們會在執行*ILogger*的記錄類別中的幕後使用它，而我們會在整個應用程式中進行*ILogger*方法呼叫。

如此一來，如果您想要讓記錄更豐富，可以用您想要的任何記錄機制來取代[`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) 。 例如，當您的應用程式成長時，您可能會決定要使用更完整的記錄套件，例如[NLog](http://nlog-project.org/)或[Enterprise Library 記錄應用程式區塊](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)。 （[Log4Net](http://logging.apache.org/log4net/)是另一個熱門的記錄架構，但它不會執行非同步記錄）。

使用架構（例如 NLog）的其中一個可能原因是有助於將記錄輸出分割成不同的高容量和高價值的資料存放區。 這可協助您有效率地儲存大量通知資料，而您不需要針對執行快速查詢，同時又能快速存取 ACT 資料。

### <a name="semantic-logging"></a>語義記錄

如需以較新的方式執行記錄以產生更有用的診斷資訊，請參閱[企業程式庫語義記錄應用程式區塊（樓板）](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 樓板會使用 .NET 4.5 中[的 Windows 事件追蹤](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)（ETW）和[EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)支援，讓您能夠建立更具結構化和可查詢的記錄。 您可以針對您所記錄的每一種事件種類定義不同的方法，讓您自訂您所撰寫的資訊。 例如，若要記錄 SQL Database 錯誤，您可以呼叫 `LogSQLDatabaseError` 方法。 針對這種例外狀況，您知道資訊的重要部分是錯誤號碼，因此您可以在方法簽章中包含錯誤號碼參數，並將錯誤號碼記錄為所撰寫記錄檔記錄中的個別欄位。 因為此數目位於不同的欄位，所以您可以更輕鬆可靠地取得以 SQL 錯誤號碼為基礎的報表，而不只是將錯誤號碼串連成訊息字串。

## <a name="logging-in-the-fix-it-app"></a>在修正 It 應用程式中登入

### <a name="the-ilogger-interface"></a>ILogger 介面

以下是 Fix It 應用程式中的*ILogger*介面。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

這些方法可讓您以*System. Diagnostics*支援的相同四個層級來寫入記錄。 TraceApi 方法是用來記錄外部服務呼叫，並提供延遲的相關資訊。 您也可以加入一組適用于 Debug/Verbose 層級的方法。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 介面的記錄器執行

介面的執行其實很簡單。 基本上，它只會呼叫標準的*系統診斷*方法。 下列程式碼片段會顯示這三個資訊方法，以及其中一個。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>呼叫 ILogger 方法

每次修正 It 應用程式中的程式碼攔截到例外狀況時，它會呼叫*ILogger*方法來記錄例外狀況的詳細資料。 而且每次呼叫資料庫、Blob 服務或 REST API 時，它會在呼叫之前啟動碼錶、在服務傳回時停止碼錶，並記錄已耗用的時間，以及成功或失敗的相關資訊。

請注意，記錄訊息包含 [類別名稱] 和 [方法名稱]。 最好的作法是確保記錄檔訊息能夠識別應用程式程式碼的哪個部分會寫入它們。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

因此，在每次修正 It 應用程式對 SQL Database 進行呼叫時，您都可以看到呼叫、呼叫它的方法，以及確切花費的時間。

![記錄中的 SQL Database 查詢](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

如果您流覽記錄檔，您可以看到資料庫呼叫所花費的時間是變數。 該資訊可能很有用：因為應用程式會記錄所有這項功能，所以您可以分析資料庫服務在一段時間內執行的歷程記錄趨勢。 例如，服務可能會在大部分的時間內快速，但要求可能會失敗，而回應可能會在一天的特定時間變慢。

您可以對 Blob 服務執行相同的動作–每次應用程式上傳新檔案時，都會有一個記錄檔，而您可以看到上傳每個檔案所需的確切時間。

![Blob 上傳記錄檔](monitoring-and-telemetry/_static/image23.png)

每當您呼叫服務時，就只需要撰寫幾行程式碼，現在當有人說他們遇到問題時，您就知道問題到底是什麼，無論是錯誤，還是就算是執行緩慢。 您可以找出問題的來源，而不需要遠端登入伺服器，或在錯誤發生後開啟記錄，希望重新建立。

## <a name="dependency-injection-in-the-fix-it-app"></a>修正 It 應用程式中的相依性插入

您可能會想知道上述範例中的存放庫構造函式如何取得記錄器介面執行：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

若要將介面連線到執行，應用程式會使用相依性[插入](http://en.wikipedia.org/wiki/Dependency_injection)（DI）搭配[AutoFac](http://autofac.org/)。 DI 可讓您在整個程式碼中使用以介面為基礎的物件，而且只需要在一個位置指定介面具現化時所使用的實作為。 這可讓您更輕鬆地變更執行：例如，您可能會想要將 NLog 記錄器取代為診斷記錄器。 或者，若要進行自動化測試，您可能會想要取代記錄器的 mock 版本。

修正 It 應用程式會在所有的存放庫和所有的控制器中使用 DI。 控制器類別的函式會取得*ITaskRepository*介面，與存放庫取得記錄器介面的方式相同：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

應用程式會使用 AutoFac DI 程式庫來自動提供這些函式的*TaskRepository*和*記錄器*實例。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

這段程式碼基本上會指出，任何位置的函式都需要*ILogger*介面、傳入*記錄器*類別的實例，而且每當需要*IFixItTaskRepository*介面時，就會傳入*FixItTaskRepository*類別的實例。

[AutoFac](http://autofac.org/)是您可以使用的許多相依性插入架構之一。 另一個熱門的是[Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)，這是 Microsoft 模式與實務的建議和支援。

## <a name="built-in-logging-support-in-azure"></a>Azure 中的內建記錄支援

Azure 支援[Azure App Service 中 Web Apps](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)的下列記錄類型：

- [診斷] 追蹤（您可以在不重新開機網站的情況下開啟和關閉和設定層級）。
- Windows 事件。
- IIS 記錄檔（HTTP/FREB）。

Azure 支援下列雲端服務類型的[記錄](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)：

- 系統診斷追蹤。
- 效能計數器。
- Windows 事件。
- IIS 記錄檔（HTTP/FREB）。
- 自訂目錄監視。

Fix It 應用程式會使用 System. Diagnostics 追蹤。 您只需要啟用 web 應用程式中的診斷記錄，就會在入口網站中翻轉交換器，或呼叫 REST API。 在入口網站中，按一下您網站**的 [設定**] 索引標籤，然後向下滾動以查看 [**應用程式診斷**] 區段。 您可以開啟或關閉記錄，並選取您想要的記錄層級。 您可以讓 Azure 將記錄寫入檔案系統或儲存體帳戶。

![[設定] 索引標籤中的應用程式診斷和網站診斷](monitoring-and-telemetry/_static/image24.png)

在 Azure 中啟用記錄功能之後，您可以在 [Visual Studio 輸出] 視窗中查看記錄檔的建立時間。

![串流記錄功能表](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![串流記錄功能表](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

您也可以將記錄寫入儲存體帳戶，並使用可存取 Azure 儲存體表格服務的任何工具來加以查看，例如 Visual Studio 或[Azure 儲存體總管](https://azure.microsoft.com/features/storage-explorer/)中的**伺服器總管**。

![伺服器總管中的記錄](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>總結

執行現成的遙測系統、在您自己的程式碼中檢測記錄，以及在 Azure 中設定記錄非常簡單。 當您有生產環境問題時，遙測系統和自訂記錄的組合將可協助您快速解決問題，然後才會成為客戶的主要問題。

在[下一章](transient-fault-handling.md)中，我們將探討如何處理暫時性錯誤，使其不會成為您必須調查的生產環境問題。

## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源。

檔主要是關於遙測：

- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱檢測和遙測指引、服務計量指引、健康情況端點監視模式，以及執行時間重新設定模式。
- [雲端中的捏合：在 Azure 網站上啟用新的 New relic 效能監視](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)。
- [Azure 上大規模服務設計的最佳作法雲端服務](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 以標記 Simm 和 Michael Thomassy 的技術白皮書。 請參閱遙測和診斷一節。
- [Application Insights 的新一代開發](https://msdn.microsoft.com/magazine/dn683794.aspx)。 MSDN 雜誌文章。

檔主要是關於記錄：

- [語義記錄應用程式區塊（樓板）](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 Neil Mackenzie 呈現使用樓板進行語義記錄的案例。
- [建立具有語義記錄的結構化且有意義的記錄](https://channel9.msdn.com/Events/Build/2013/3-336)。 影片「Julian Dominguez」呈現使用樓板進行語義記錄的情況。
- [EF6 SQL 記錄–第1部分：簡單記錄](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)。 Arthur Vickers 說明如何記錄 EF 6 中 Entity Framework 所執行的查詢。
- [在 ASP.NET MVC 應用程式中使用 Entity Framework 的連接恢復功能和命令攔截](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 第四個在9部分的教學課程系列中，示範如何使用 EF 6 命令攔截功能，透過 Entity Framework 來記錄傳送至資料庫的 SQL 命令。
- [使用5.0 呼叫C#端資訊屬性來改善記錄](http://www.dotnetcurry.com/showarticle.aspx?ID=972)。 如何輕鬆地記錄呼叫方法的名稱，而不需要將其硬式編碼成常值，或使用反映手動取得。

檔主要是關於疑難排解：

- [Azure 疑難排解 &amp; 的調試 blog](https://blogs.msdn.com/b/kwill/)。
- [AzureTools – Azure 開發人員支援小組所使用的診斷公用程式](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)。 引進並提供工具的下載連結，可在 Azure VM 上用來下載及執行各種不同的診斷和監視工具。 當您需要診斷特定 VM 上的問題時，很有用。
- [使用 Visual Studio，針對 Azure App Service 中的 web 應用程式進行疑難排解](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 開始使用 System. Diagnostics 追蹤和遠端偵錯程式的逐步教學課程。

影片：

- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九部分系列。 以非常容易存取且有趣的方式呈現高階概念和架構原則，並提供 Microsoft 客戶諮詢小組（CAT）體驗與實際客戶的故事。 劇集4和9是關於監視和遙測。 第9集包含監視服務 MetricsHub、AppDynamics、New New relic 和 PagerDuty 的總覽。
- [打造 Big：從 Azure 客戶學到的經驗-第二部](https://channel9.msdn.com/Events/Build/2012/3-030)。 Mark Simm 討論如何設計失敗和檢測所有專案。 類似于防故障的系列，並深入探討如何詳細說明。

程式碼範例：

- [Azure 中的雲端服務基本](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)概念。 Microsoft Azure 客戶諮詢小組所建立的範例應用程式。 示範遙測和記錄實務，如下列文章中所述。 此範例會使用[NLog](http://nlog-project.org/)來執行應用程式記錄。 如需相關檔，請參閱[四個關於遙測和記錄的 TechNet wiki 文章系列](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)。

> [!div class="step-by-step"]
> [上一頁](design-to-survive-failures.md)
> [下一頁](transient-fault-handling.md)
