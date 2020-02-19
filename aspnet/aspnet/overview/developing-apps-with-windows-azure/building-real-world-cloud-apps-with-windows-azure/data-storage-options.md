---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: 資料儲存體選項（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 9357ed5aef39bed501cdac9ac26d46c884d4fae0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457176"
---
# <a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>資料儲存體選項（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

大部人員都習慣使用關聯式資料庫，而在設計雲端應用程式時，他們會嘗試尋找其他資料儲存體選項。 結果可能是較佳的效能、高費用或更糟的，因為[NoSQL](http://en.wikipedia.org/wiki/NoSQL) （非關聯式）資料庫可以比關係資料庫更有效率地處理某些工作。 當客戶要求我們協助解決重要的資料儲存問題時，通常是因為他們有一個關係資料庫，其中其中一個 NoSQL 選項會有更好的工作。 在這些情況下，如果客戶在將應用程式部署到生產環境之前已實作為 NoSQL 解決方案，就會更好。

另一方面，假設 NoSQL 資料庫可以執行良好或足夠的效果，也會造成錯誤。 並非所有資料儲存工作都有單一的最佳資料管理選擇;不同的資料管理解決方案會針對不同的工作進行優化。 大部分的真實世界雲端應用程式都有各種資料儲存需求，而且通常是由多個資料儲存解決方案的組合所提供的最佳服務。

本章的目的是要讓您更瞭解雲端應用程式可用的資料儲存體選項，以及一些如何選擇適合您案例的基本指導方針。 在開發應用程式之前，最好先瞭解您可以使用的選項，並考慮其優缺點。 變更生產應用程式中的資料儲存體選項可能非常困難，例如必須在飛機進行時變更 jet 引擎。

## <a name="data-storage-options-on-azure"></a>Azure 上的資料儲存體選項

雲端可讓您更輕鬆地使用各種關聯式和 NoSQL 資料存放區。 以下是一些您可以在 Azure 中使用的資料儲存平臺。

![](data-storage-options/_static/image1.png)

此表格顯示四種類型的 NoSQL 資料庫：

- 索引[鍵/值資料庫](https://msdn.microsoft.com/library/dn313285.aspx#sec7)會針對每個索引鍵值儲存單一序列化物件。 適合用來儲存大量資料，也就是您要在其中取得指定索引鍵值的一個項目，而且不必根據項目的其他屬性進行查詢。

    [Azure Blob 儲存體](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/)是一種索引鍵/值資料庫，其功能類似于雲端中的檔案儲存體，其索引鍵值對應至資料夾和檔案名。 您可以依資料夾和檔案名抓取檔案，而不是搜尋檔案內容中的值。

    「 [Azure 資料表儲存體](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)」也是索引鍵/值資料庫。 每個值都稱為*實體*（類似于資料分割索引鍵和資料列索引鍵所識別的資料列），而且包含多個*屬性*（類似于資料行，但資料表中的所有實體都不需要共用相同的資料行）。 查詢索引鍵以外的資料行非常沒有效率，應予以避免。 例如，您可以儲存使用者設定檔資料，其中有一個分割區儲存單一使用者的相關資訊。 您可以將資料（例如使用者名稱、密碼雜湊、出生日期等等）儲存在單一實體的個別屬性中，或是在相同資料分割的個別實體中。 但是，您不想要查詢具有指定之出生日期範圍的所有使用者，也無法在您的設定檔資料表與另一個資料表之間執行聯結查詢。 資料表儲存體比關係資料庫更具擴充性且成本較低，但不會啟用複雜的查詢或聯結。
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8)是索引鍵/值資料庫，其中的值為*檔*。 此處的「檔」並不是用在 Word 或 Excel 檔的意義上，而是指命名欄位和值的集合，其中任何一項都可以是子檔。 例如，在訂單歷程記錄資料表中，訂單檔可能會有訂單號碼、訂單日期和客戶欄位;而 [customer] 欄位可能會有 [名稱] 和 [位址] 欄位。 資料庫會以 XML、YAML、JSON 或 BSON 之類的格式來編碼欄位資料;或者，它可以使用純文字。 除了索引鍵/值資料庫以外，設定檔資料庫的功能之一，就是能夠查詢非索引鍵欄位並定義次要索引，讓查詢更有效率。 這項功能可讓檔資料庫更適合需要根據比檔索引鍵的值更複雜的準則來抓取資料的應用程式。 例如，在「銷售訂單歷程記錄」檔資料庫中，您可以查詢各種欄位，例如「產品識別碼」、「客戶識別碼」、「客戶名稱」等等。 [MongoDB](http://www.mongodb.org/)是受歡迎的檔資料庫。
- 資料[行系列資料庫](https://msdn.microsoft.com/library/dn313285.aspx#sec9)是索引鍵/值資料存放區，可讓您將資料儲存體結構為相關資料行的集合，稱為資料行系列。 例如，人口普查資料庫可能有一個使用者名稱的資料行群組（第一個、中間、最後一個）、一個群組用於該人員的位址，以及一個群組用於個人的設定檔資訊（DOB、性別等等）。 然後，資料庫可以將每個資料行系列儲存在個別的分割區，同時保留一個人與相同索引鍵相關的所有資料。 您接著可以讀取所有的設定檔資訊，而不需要同時讀取所有的名稱和位址資訊。 [Cassandra](http://cassandra.apache.org/)是熱門的資料行系列資料庫。
- [圖形資料庫](https://msdn.microsoft.com/library/dn313285.aspx#sec10)會將資訊儲存成物件和關聯性的集合。 圖形資料庫的目的是要讓應用程式有效率地執行查詢，以跨越物件的網路和兩者之間的關聯性。 比方說，物件可能是人力資源資料庫中的員工，而您可以進行快速查詢，例如「尋找直接或間接為 Scott 工作的所有員工。」 [Neo4j](http://www.neo4j.org/)是熱門的圖形資料庫。

相較于關係資料庫，NoSQL 選項為儲存和分析非結構化資料提供更高的擴充性和成本效益。 其缺點是它們不會提供關係資料庫的豐富 queryability 和強大的資料完整性功能。 NoSQL 適用于 IIS 記錄檔資料，這牽涉到高容量，而不需要聯結查詢。 NoSQL 不適用於銀行交易，這需要絕對資料完整性，而且牽涉到與其他帳戶相關資料的多個關聯性。

另外還有一種較新的資料庫平臺類別，稱為[NewSQL](http://en.wikipedia.org/wiki/NewSQL) ，其結合了 NoSQL 資料庫的擴充性與關係資料庫的 queryability 和交易完整性。 NewSQL 資料庫是針對分散式儲存和查詢處理而設計的，這通常很難在 "OldSQL" 資料庫中執行。 [NuoDB](http://www.nuodb.com/)是可在 Azure 上使用的 NewSQL 資料庫範例。

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop 和 MapReduce

您可以在 NoSQL 資料庫中儲存的大量資料，很容易就能及時有效率地進行分析。 若要這麼做，您可以使用可實行[MapReduce](http://en.wikipedia.org/wiki/MapReduce)功能的架構，例如[Hadoop](http://hadoop.apache.org/) 。 基本上，MapReduce 程式的作用如下：

- 只選取資料存放區，以限制需要處理的資料大小，僅限您實際需要分析的資料。 例如，您想要以出生年份的方式來知道您的使用者群，因此您只需從使用者設定檔資料存放區中選取出生年份。
- 將資料分成幾個部分，並將它們傳送到不同的電腦進行處理。 電腦 A 會計算具有1950-1959 日期、電腦 B 執行1960-1969 等的人員人數。這一組電腦稱為*Hadoop*叢集。
- 完成元件的處理之後，請將每個部分的結果放在一起。 您現在有一個相對簡短的清單，其中包含每個出生年份的多少人，以及在此整體清單中計算百分比的工作是可管理的。

在 Azure 上， [HDInsight](https://azure.microsoft.com/services/hdinsight/)可讓您使用 Hadoop 的強大功能來處理、分析及取得海量資料的新見解。 例如，您可以使用它來分析 web 伺服器記錄：

- 啟用對您儲存體帳戶的 web 伺服器記錄。 這會設定 Azure 將記錄檔寫入至應用程式的每個 HTTP 要求的 Blob 服務。 Blob 服務基本上是雲端檔案儲存體，而且與 HDInsight 完美整合。

    ![記錄至 Blob 儲存體](data-storage-options/_static/image2.png)
- 當應用程式取得流量時，web 伺服器 IIS 記錄會寫入至 Blob 儲存體。

    ![Web 伺服器記錄](data-storage-options/_static/image3.png)
- 在入口網站中，按一下 **新增** - **資料服務** - **hdinsight** - **快速建立**，並指定 hdinsight 叢集名稱、叢集大小（HDInsight 叢集資料節點數目），以及 hdinsight 叢集的使用者名稱和密碼。

    ![HDInsight](data-storage-options/_static/image4.png)

您現在可以設定 MapReduce 作業來分析記錄，並取得問題的解答，例如：

- 我的應用程式會在一天內取得最多或最少的流量？
- 我的流量來自哪些國家/地區？
- 流量來源區域的平均鄰近收入為何。 （有一個公用資料集可為您提供以 IP 位址為依據的鄰近地區，而您可以將其與 web 伺服器記錄中的 IP 位址比對）。
- 鄰近專案的收入與網站中的特定頁面或產品有何關聯？

接著，您可以根據客戶感興趣或可能購買特定產品的可能性，使用這類問題的答案來鎖定廣告。

如[自動化所有事項一章](automate-everything.md)所述，您可以在入口網站中執行的大部分功能都可以自動化，包括設定和執行 HDInsight 分析作業。 一般的 HDInsight 腳本可能包含下列步驟：

- 布建 HDInsight 叢集，並將它連結至您的儲存體帳戶，以進行 Blob 儲存體輸入。
- 將 MapReduce 工作可執行檔（.jar 或 .exe 檔案）上傳至 HDInsight 叢集。
- 提交將輸出資料儲存至 Blob 儲存體的 MapReduce。
- 等候作業完成。
- 刪除 HDInsight 叢集。
- 存取 Blob 儲存體的輸出。

藉由執行所有這項工作的腳本，您可以將 HDInsight 叢集布建的時間減到最少，以將成本降到最低。

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>平臺即服務（PaaS）與基礎結構即服務（IaaS）的比較

先前所列的資料儲存體選項包含「平臺即服務」（PaaS）和「基礎結構即服務」（IaaS）解決方案。 PaaS 表示我們會管理硬體和軟體基礎結構，而您只是使用服務。 SQL Database 是 Azure 的 PaaS 功能。 您會詢問資料庫，而 Azure 會在幕後設定和設定 Vm，並在其上設定資料庫。 您沒有 Vm 的直接存取權，也不需要管理它們。IaaS 表示您會設定、設定及管理在我們的資料中心基礎結構中執行的 Vm，並將任何您想要的專案放在其上。 我們會提供預先設定的 VM 映射資源庫，以進行常見的 VM 配置。 例如，您可以為 Windows Server 2008、Windows Server 2012、BizTalk Server、Oracle WebLogic Server、Oracle Database 等安裝預先設定的 VM 映射。

Azure 提供的 PaaS 資料解決方案包括：

- Azure SQL Database （先前稱為 SQL Azure）。 以 SQL Server 為基礎的雲端關係資料庫。
- Azure 資料表儲存體。 索引鍵/值 NoSQL 資料庫。
- Azure Blob 儲存體。 雲端中的檔案儲存體。

針對 IaaS，您可以在 VM 上執行任何可載入的專案，例如：

- 關係資料庫，例如 SQL Server、Oracle、MySQL、SQL Compact、SQLite 或 Postgres。
- 索引鍵/值資料存放區，例如 Memcached、Redis、Cassandra 和 Riak。
- 資料行資料存放區，例如 HBase。
- 記錄資料庫，例如 MongoDB、RavenDB 和 CouchDB。
- 圖表資料庫，例如 Neo4j。

![Azure 上的資料儲存體選項](data-storage-options/_static/image5.png)

IaaS 選項提供您幾乎無限制的資料儲存體選項，其中有許多會特別容易使用，因為您可以使用預先設定的映射建立 Vm。 例如，在管理入口網站中，移至**虛擬機器**，按一下 [**映射**] 索引標籤，然後按一下 **[流覽 VM 倉庫**]。

![流覽 VM 維修站](data-storage-options/_static/image6.png)

接著，您會看到[數百個預先設定的 vm 映射](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx)清單，而且您可以從已預先安裝資料庫管理系統的映射建立 VM，例如 MongoDB、Neo4J、Redis、Cassandra 或 CouchDB：

![VM 倉庫中的 MongoDB](data-storage-options/_static/image7.png)

Azure 會盡可能輕鬆地使用 IaaS 資料儲存體選項，但 PaaS 供應專案有許多優點，使其更符合成本效益，而且在許多情況下都很實用：

- 您不需要建立 Vm，只需使用入口網站或腳本來設定資料存放區。 如果您想要 200 tb 的資料存放區，可以只按一下按鈕或執行命令，並在幾秒內準備好供您使用。
- 您不需要管理或修補服務所使用的 Vm;Microsoft 會自動為您執行此程式。-您不需要擔心設定調整規模或高可用性的基礎結構;Microsoft 會為您處理所有的程式。
- 您不需要購買授權;授權費用會包含在服務費用中。
- 您只需依據使用量付費。

Azure 中的 PaaS 資料儲存選項包括協力廠商提供者的供應專案。 例如，您可以從 Azure 市集中選擇[MongoLab 附加](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/)元件，以提供 MongoDB 資料庫即服務。

## <a name="choosing-a-data-storage-option"></a>選擇資料儲存選項

在所有案例中，沒有任何一種方法適合。 如果有人說這項技術是解答，第一件事就是「問題是什麼？」，因為不同的解決方案會針對不同的專案進行優化。 關聯式模型有一些明確的優點;這就是為什麼它已經是這麼久的原因。 但是也有可透過 NoSQL 解決方案解決的 SQL 的右下方。

我們最常看到的工作是一種複合方法，您可以在單一解決方案中使用 SQL 和 NoSQL。 即使有人說他們正在採用 NoSQL，如果您深入探索他們的工作，通常會發現它們使用數個不同的 NoSQL 架構：它們使用[CouchDB](http://wiki.apache.org/couchdb/Introduction)、 [Redis](http://redis.io/)，以及[Riak](http://basho.com/riak/)不同的專案。 即使是 Facebook （廣泛使用 NoSQL），也會針對服務的不同部分使用不同的 NoSQL 架構。 混合和比對資料儲存方法的彈性是雲端的絕佳功能之一，因為它可以輕鬆地使用多個資料解決方案，並將它們整合到單一應用程式中。

以下是您在選擇方法時要考慮的一些問題：

| 資料語義 | -什麼是核心資料儲存體和資料存取語義（您儲存關聯式或非結構化資料）？ 非結構化資料（例如媒體檔案）最適合 blob 儲存體;相關資料的集合，例如產品、清查、供應商、客戶訂單等，最適合在關係資料庫中使用。 |
| --- | --- |
| 查詢支援 | -查詢資料有多簡單？ -可以有效率地詢問哪些類型的問題？ 索引鍵/值資料存放區非常適合用來取得具有索引鍵值的單一資料列，而不適合用于複雜的查詢。 如果是使用者設定檔資料存放區，您一律會取得某個特定使用者的資料，則索引鍵/值資料存放區可能會正常運作;針對您想要根據各種產品屬性來取得不同群組的產品目錄，關係資料庫可能會有更好的效果。 NoSQL 資料庫可以有效率地儲存大量資料，但您必須針對應用程式如何查詢資料來建立資料庫的結構，而這會讓臨機操作查詢更難執行。 透過關系資料庫，您幾乎可以建立任何類型的查詢。 |
| 功能投射 | -是否可以在伺服器端執行問題、匯總等等？ 如果我從 SQL 中的資料表執行 SELECT COUNT （\*），它會非常有效率地在伺服器上執行所有工作，並傳回我要尋找的數位。 如果我想要從不支援匯總的 NoSQL 資料存放區進行相同的計算，這就是沒有效率的「未系結查詢」，而且可能會超時。即使查詢成功，我還是必須將伺服器上的所有資料都取出到用戶端，並計算用戶端上的資料列。 -可以使用哪些語言或類型的運算式？ 在關係資料庫中，我可以使用 SQL。 使用某些 NoSQL 資料庫（例如 Azure 資料表儲存體）時，我會使用[OData](http://www.odata.org/)，而我可以做的就是對主要索引鍵進行篩選並取得投影（選取可用欄位的子集）。 |
| 輕鬆擴充性 | -資料需要多長的時間和規模？ -平臺原本就會執行相應放大嗎？ -新增/移除容量（大小和輸送量）有多簡單？ 關係資料庫和資料表不會自動進行分割以使其可調整，因此很容易擴充到超出特定限制。 NoSQL 資料存放區（例如 Azure 資料表儲存體）本質上會分割所有專案，幾乎不會有新增資料分割的限制。 您可以輕鬆地將表格儲存體調整為 200 tb，但 Azure SQL Database 的資料庫大小上限是 500 gb。 您可以藉由將關聯式資料分割成多個資料庫來進行調整，但設定應用程式以支援該模型，這牽涉到許多程式設計工作。 |
| 檢測與管理能力 | -要檢測、監視和管理的平臺有多簡單？ 您必須持續掌握資料存放區的健全狀況和效能，因此您需要事先知道平臺提供給您的計量，以及您必須自行開發的內容。 |
| 作業 | -在 Azure 上部署和執行的平臺有多簡單？ PaaS? IaaS? 廠商? 您可以輕鬆地在 Azure 上設定表格儲存體和 SQL Database。 不是內建 Azure PaaS 解決方案的平臺需要更多的人力。 |
| API 支援 | -這是可讓您輕鬆使用平臺的 API 嗎？ 針對 Azure 資料表服務，有一個 SDK 具有 .NET API，可支援 .NET 4.5 非同步程式設計模型。 如果您撰寫的是 .NET 應用程式，相較于另一個沒有 API 或較不完整的索引鍵/值資料存放區平臺，撰寫和測試 Azure 資料表服務的程式碼會更容易。 |
| 交易完整性與資料一致性 | -平臺是否支援交易以確保資料的一致性是非常重要的嗎？ 為了追蹤大量傳送的電子郵件，效能和低資料儲存成本可能比自動支援資料平臺中的交易或參考完整性更重要，因此 Azure 資料表服務是不錯的選擇。 針對追蹤銀行帳戶餘額或採購單，提供強式交易保證的關係資料庫平臺是較佳的選擇。 |
| 業務持續性 | -備份、還原和嚴重損壞修復有多簡單？ 較早或之後的生產資料將會損毀，而您將需要復原功能。 關係資料庫通常會有更精細的還原功能，例如能夠還原到某個時間點。 瞭解您所考慮的每個平臺中有哪些可用的還原功能是要考慮的重要因素。 |
| 成本 | -如果有多個平臺可支援您的資料工作負載，它們如何比較成本？ 例如，如果您使用 ASP.NET Identity，您可以將使用者設定檔資料儲存在 Azure 資料表服務或 Azure SQL Database 中。 如果您不需要 SQL Database 的豐富查詢功能，您可以選擇 Azure 資料表，因為它的成本會比指定的儲存體數量低。 |

我們通常建議您在選擇資料儲存體解決方案之前，知道每個類別中問題的答案。

此外，您的工作負載可能會有某些平臺可支援的特定需求，而無法比其他平臺更好。 例如：

- 您的應用程式需要審核功能嗎？
- 您的資料壽命需求為何--您需要自動封存或清除功能嗎？
- 您有特殊的安全性需求嗎？ 例如，資料包含 PII （個人識別資訊），但您必須能夠確保該 PII 不會從查詢結果中排除。
- 如果您有一些資料因為法規或技術因素而無法儲存在雲端中，您可能需要雲端資料儲存平臺，以協助與您的內部部署儲存體整合。

## <a name="demo--using-sql-database-in-azure"></a>示範-在 Azure 中使用 SQL Database

Fix It 應用程式會使用關係資料庫來儲存工作。 [[自動化所有專案] 一章](automate-everything.md)中所顯示的環境建立 Windows PowerShell 腳本會建立兩個 SQL Database 實例。 按一下 [ **SQL** database] 索引標籤，即可在入口網站中查看這些選項。

![入口網站中的 SQL 資料庫](data-storage-options/_static/image8.png)

您也可以使用入口網站輕鬆建立資料庫。

按一下 **新增--資料服務** -- **SQL Database** -- **快速建立**，輸入資料庫名稱，選擇您的帳戶中已有的伺服器，或建立一個新的伺服器，然後按一下 **建立 SQL Database**。

![New SQL Database](data-storage-options/_static/image9.png)

請等候數秒，而且您已在 Azure 中備妥可供您使用的資料庫。

![已建立新 SQL Database](data-storage-options/_static/image10.png)

因此，Azure 會在幾秒內完成，在內部部署環境中可能需要一天或一周或更久的時間。 而且，由於您可以輕鬆地在腳本中自動建立資料庫，或藉由使用管理 API 來進行相應放大，因此只要您的應用程式已經過設計，就可以透過將資料分散到多個資料庫，以動態方式向外延展。

這是我們的平臺即服務模型的範例。 您不需要管理伺服器，而是這麼做。 您不需要擔心備份，而是這麼做。 它會在高可用性中執行–資料庫中的資料會自動複寫到三部伺服器上。 如果電腦停止，我們會自動故障，而且您不會遺失任何資料。 伺服器會定期修補，您不需要擔心。

按一下按鈕，您就會取得所需的確切連接字串，而且可以立即開始使用新的資料庫。

![連接字串](data-storage-options/_static/image11.png)

儀表板會顯示您的連線歷程記錄和使用的儲存體數量。

![SQL Database 儀表板](data-storage-options/_static/image12.png)

您可以在入口網站中或使用您已熟悉的 SQL Server 工具（包括 SQL Server Management Studio （SSMS）和 Visual Studio 工具 SQL Server 物件總管（SSOX）和伺服器總管）來管理資料庫。

![SSOX](data-storage-options/_static/image13.png)

另一個不錯的事是計價模式。 您可以使用免費的 20 MB 資料庫開始開發，而生產資料庫每月大約會啟動 $5。 您只需支付實際儲存在資料庫中的資料量，而不是您的最大容量。 您不需要購買授權。

SQL Database 很容易調整。 針對 Fix It 應用程式，我們在自動化腳本中建立的資料庫的上限為 1 gb。 如果您想要將它相應增加至 150 gb，您可以直接移至入口網站並變更該設定，或執行 REST API 命令，並在幾秒內擁有可以部署資料的 150 gb 資料庫。

![SQL Database 版本和大小](data-storage-options/_static/image14.png)

這就是雲端的威力，可以快速輕鬆地建立基礎結構，並立即開始使用。

Fix It 應用程式會使用兩個 SQL 資料庫，一個用於成員資格（驗證和授權），一個用於資料，而這就是您要進行布建和調整它所需的一切。 您先前已瞭解如何透過 Windows PowerShell 腳本布建資料庫，現在您也已瞭解在入口網站中有多麼簡單。

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>Entity Framework 與使用 ADO.NET 直接存取資料庫

Fix It 應用程式會使用 Entity Framework 來存取這些資料庫，這是 Microsoft 建議的 .NET 應用程式的 ORM （物件關聯式對應工具）。 ORM 是一個絕佳的工具，可提升開發人員的生產力，但在某些情況下，生產力的代價是降低效能。 在真實世界的雲端應用程式中，您不會選擇使用 EF 或直接使用 ADO.NET，您將會同時使用這兩者。 在大部分的情況下，當您撰寫與資料庫搭配使用的程式碼時，取得最大效能並不重要，而且您可以利用 Entity Framework 所取得的簡化編碼和測試。 在 EF 負荷導致無法接受效能的情況下，您可以使用 ADO.NET 來撰寫及執行自己的查詢，最好是藉由呼叫預存程式。

無論您使用何種方法來存取資料庫，您都想要盡可能將「對話」最小化。 換句話說，如果您可以在一個較大的查詢結果集中取得所需的所有資料，而不是數十個或數百個較小的資料集，通常是比較理想的作法。 例如，如果您需要列出學生以及他們所註冊的課程，通常最好是在一個聯結查詢中取得所有資料，而不是讓學生參與一個查詢，並針對每個學生的課程執行個別的查詢。

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>[修正 It] 應用程式中的 SQL 資料庫和 Entity Framework

在修正 It 應用程式中，`FixItContext` 類別（衍生自 Entity Framework `DbContext` 類別）會識別資料庫，並指定資料庫中的資料表。 內容會指定工作的實體集（資料表），而程式碼會將連接字串名稱傳入內容。 該名稱會參考在 web.config 檔案中定義的連接字串。

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

*Web.config 檔案*中的連接字串名為 appdb （這裡指向本機開發資料庫）：

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

Entity Framework 會根據 `FixItTask` 實體類別中包含的屬性來建立*FixItTasks*資料表。 這是簡單的 POCO （單純的 CLR 物件）類別，這表示它不會繼承或具有 Entity Framework 的任何相依性。 但是 Entity Framework 知道如何根據它來建立資料表，並對它執行 CRUD （建立-讀取-更新-刪除）作業。

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks 資料表](data-storage-options/_static/image15.png)

Fix It 應用程式包含一個儲存機制介面，用於與資料存放區一起使用的 CRUD 作業。

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

請注意，存放庫方法全都是非同步，因此所有資料存取都可以用完全非同步方式來完成。

存放庫的執行會呼叫 Entity Framework 非同步方法來處理資料，包括 LINQ 查詢，以及插入、更新和刪除作業。 以下是用來查閱 Fix It 工作的程式碼範例。

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

您會發現這裡還有一些時間和錯誤記錄程式碼，我們將在稍後的[監視和遙測一章](monitoring-and-telemetry.md)中探討。

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>在 Azure 中選擇 VM （IaaS）中的 SQL Database （PaaS）與 SQL Server

SQL Server 和 Azure SQL Database 的一件事，就是兩者的核心程式設計模型都相同。 您在這兩種環境中都可以使用相同的技能。 您甚至可以使用開發中的 SQL Server 資料庫，以及雲端中的 SQL Database 實例，也就是設定 Fix It 應用程式的方式。

或者，您可以在您于內部部署執行的雲端中執行相同的 SQL Server，方法是將它安裝在 IaaS Vm 上。 針對某些繼承應用程式，在 VM 中執行 SQL Server 可能是較佳的解決方案。 因為 SQL Server 的資料庫是在專用的 VM 上執行，所以它所擁有的資源比在共用伺服器上執行的 SQL Database 資料庫還多。 這表示 SQL Server 資料庫可能會變得更大，而且仍然正常執行。 一般來說，資料庫大小和資料表大小越小，使用案例就越適合 SQL Database （PaaS）。

以下是如何在兩個模型之間進行選擇的一些指導方針。

| Azure SQL Database (PaaS) | 虛擬機器（IaaS）中的 SQL Server |
| --- | --- |
| **優點**：您不需要建立或管理 vm、更新或修補作業系統或 SQL;Azure 會為您執行此程式。 -內建高可用性，具有資料庫層級 SLA。 -低擁有權總成本（TCO），因為您只需支付所使用的部分（不需要授權）。 -適用于處理大量較小的資料庫（&lt;= 500 GB）。 -輕鬆地以動態方式建立新的資料庫以啟用相應放大。 | ***優點***-與內部部署 SQL Server 的功能相容。 -可以透過 VM 層級 SLA，透過 2 + Vm 中的 AlwaysOn 來執行 SQL Server[高可用性](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx)。 -您可以完整控制 SQL 的管理方式。 -可以重複使用您已經擁有的 SQL 授權，或按小時支付一次。 -適用于處理較少但較大（1 TB 以上）的資料庫。 |
| **缺點**-相較于內部部署 SQL Server （缺少[CLR 整合](https://technet.microsoft.com/library/ms131102.aspx)、 [TDE](https://technet.microsoft.com/library/bb934049.aspx)、[壓縮支援](https://technet.microsoft.com/library/cc280449.aspx)、 [SQL Server Reporting Services](https://technet.microsoft.com/library/ms159106.aspx)等），其部分功能差距-資料庫大小限制為500gb。 | ***缺點***-更新/修補程式（OS 和 SQL）是您負責建立和管理 db 的責任-磁片 IOPS （每秒輸入/輸出作業）限制為大約8000（經由16個數據磁片磁碟機）。 |

如果您想要在 VM 中使用 SQL Server，您可以使用自己的 SQL Server 授權，或按小時支付一次。 例如，在入口網站中或透過 REST API，您可以使用 SQL Server 映射來建立新的 VM。

![使用 SQL Server 建立 VM](data-storage-options/_static/image16.png)

![SQL Server 的 VM 映射清單](data-storage-options/_static/image17.png)

當您建立具有 SQL Server 映射的 VM 時，我們會根據您的 VM 使用量，以小時為單位來費率 SQL Server 授權成本。 如果您的專案只會執行幾個月，則以小時為單位付費會較便宜。 如果您認為您的專案將會持續幾年，則以平常的方式購買授權較便宜。

## <a name="summary"></a>摘要

雲端運算讓混搭資料儲存的方法更加實用，以符合您應用程式的需求。 如果您要建立新的應用程式，請仔細思考這裡所列的問題，以選擇當您的應用程式成長時，會繼續正常運作的方法。 [下一章](data-partitioning-strategies.md)將說明一些您可以用來結合多個資料儲存方法的分割策略。

## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源。

選擇資料庫平臺：

- [可高度擴充解決方案的資料存取：使用 SQL、NoSQL 和多語言持續](https://aka.ms/dag-doc)性。 透過 Microsoft 模式與實務的電子書，深入探討雲端應用程式可用的各種資料存放區。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/ff898430.aspx)。 請參閱資料一致性入門、資料複寫和同步處理指引、索引資料表模式、具體化視圖模式。
- [基底： Acid 替代方案](http://queue.acm.org/detail.cfm?id=1394128)。 有關資料一致性和擴充性之間取捨的文章。
- 七[周內有七個資料庫：現代化資料庫和 NoSQL 移動的指南](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921)。 Eric Redmond 和 Jim 的著作。 強烈建議您將自己帶入目前可用的資料儲存平臺範圍。

在 SQL Server 和 SQL Database 之間選擇：

- [適用于 SQL Database 指引的 Premium Preview](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)。 簡介 SQL Database Premium，以及如何在 SQL Database Web 和 Business edition 上選擇它的指引。
- [方針和限制（Azure SQL Database）](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)。 入口網站頁面，連結到 SQL Database 限制的相關檔，包括著重于 SQL Database 不支援之 SQL Server 功能的檔。
- [Azure 虛擬機器中的 SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx)。 此入口網站頁面會連結到在 Azure 中執行 SQL Server 的相關檔。
- [Scott Guthrie 說明 Azure 中的 SQL 資料庫](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/)。 Scott Guthrie 的6分鐘影片簡介 SQL Database。
- [Azure 虛擬機器中 SQL Server 的應用程式模式和開發策略](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx)。

在 ASP.NET Web 應用程式中使用 Entity Framework 和 SQL Database

- [使用 MVC 5 與 EF 6 消費者入門](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 九個部分的教學課程系列，會逐步引導您建立使用 EF 的 MVC 應用程式，並將資料庫部署至 Azure 和 SQL Database。
- [使用 Visual Studio 的 ASP.NET Web 部署](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 十二部分教學課程系列，深入瞭解如何使用 EF Code First 來部署資料庫。
- 將[具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署到 Azure 網站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。 逐步教學課程會逐步引導您建立使用驗證的 web 應用程式、將應用程式資料表儲存在成員資格資料庫中、修改資料庫架構，以及將應用程式部署至 Azure。
- [ASP.NET 資料存取內容對應](https://go.microsoft.com/fwlink/p/?LinkId=282414)。 使用 EF 和 SQL Database 的資源連結。

在 Azure 上使用 MongoDB：

- [MongoLab-Azure 上的 MongoDB](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/)。 關於在 Azure 上執行 MongoDB 之檔的入口網站頁面。
- [建立 azure 網站，該網站會連線到在 azure 虛擬機器上執行的 MongoDB](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/)。 說明如何在 ASP.NET web 應用程式中使用 MongoDB 資料庫的逐步教學課程。

HDInsight （Azure 上的 Hadoop）：

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)。 [Azure](https://azure.microsoft.com/)網站上的 HDInsight 的入口網站檔。
- [Hadoop 和 HDInsight： Azure 中的海量資料](https://msdn.microsoft.com/magazine/dn385705.aspx)。 MSDN 雜誌文章 Bruno Terkaly 和 Ricardo Villalobos，介紹 Azure 上的 Hadoop。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱 MapReduce 模式。

> [!div class="step-by-step"]
> [上一頁](single-sign-on.md)
> [下一頁](data-partitioning-strategies.md)
