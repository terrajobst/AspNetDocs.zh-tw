---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
title: 設定資料存取層的連接和命令層級設定（VB） |Microsoft Docs
author: rick-anderson
description: 具類型資料集內的 Tableadapter 會自動負責連接到資料庫、發出命令，並以結果填入 DataTable 。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: d57dfa2b-d627-45cb-b5b1-abbf3159d770
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
msc.type: authoredcontent
ms.openlocfilehash: fa2868fc0dd8acd76f600b47d92adb984ce8d105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78551804"
---
# <a name="configuring-the-data-access-layers-connection--and-command-level-settings-vb"></a>設定資料存取層的連線和命令層級設定 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_VB.zip)或[下載 PDF](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/datatutorial72vb1.pdf)

> 具類型資料集內的 Tableadapter 會自動負責連接到資料庫、發出命令，以及以結果擴展 DataTable。 有時候，我們想要自行處理這些細節，而在本教學課程中，我們將學習如何存取 TableAdapter 中的資料庫連接和命令層級設定。

## <a name="introduction"></a>簡介

在整個教學課程系列中，我們使用了具類型的資料集來執行分層架構的資料存取層和商務物件。 如[第一個教學](../introduction/creating-a-data-access-layer-vb.md)課程中所討論，具類型資料集的 datatable 當做資料存放庫，而 tableadapter 則是做為與資料庫進行通訊的包裝函式，以取得和修改基礎資料。 Tableadapter 會封裝使用資料庫所牽涉到的複雜性，並讓我們不必撰寫程式碼來連接到資料庫、發出命令，或將結果填入 DataTable。

不過有時候，當我們需要 burrow 到 TableAdapter 的深度，並撰寫直接與 ADO.NET 物件搭配運作的程式碼時。 例如，在交易教學課程[中的包裝資料庫修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md)中，我們已將方法新增至 TableAdapter，以開始、認可和回復 ADO.NET 交易。 這些方法會使用已指派給 TableAdapter `SqlCommand` 物件的內部手動建立 `SqlTransaction` 物件。

在本教學課程中，我們將探討如何存取 TableAdapter 中的資料庫連接和命令層級設定。 特別的是，我們會將功能加入至 `ProductsTableAdapter`，以啟用基礎連接字串和命令逾時設定的存取權。

## <a name="working-with-data-using-adonet"></a>使用 ADO.NET 處理資料

Microsoft .NET Framework 包含專門設計來處理資料的類別眾多。 這些類別（位於[`System.Data` 命名空間](https://msdn.microsoft.com/library/system.data.aspx)內）稱為*ADO.NET*類別。 ADO.NET 傘底下的某些類別會系結至特定的*資料提供者*。 您可以將資料提供者視為通道，讓資訊可以在 ADO.NET 類別與基礎資料存放區之間流動。 有一般化的提供者，例如 OleDb 和 ODBC，以及專為特定資料庫系統設計的提供者。 例如，雖然您可以使用 OleDb 提供者連接到 Microsoft SQL Server 資料庫，但 SqlClient 提供者會更有效率，因為它是專為 SQL Server 而設計和優化的。

以程式設計方式存取資料時，通常會使用下列模式：

1. 建立資料庫的連接。
2. 發出命令。
3. 針對 `SELECT` 查詢，請使用所產生的記錄。

有個別的 ADO.NET 類別可用於執行上述每個步驟。 例如，若要使用 SqlClient 提供者連接到資料庫，請使用[`SqlConnection` 類別](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)。 若要對資料庫發出 `INSERT`、`UPDATE`、`DELETE`或 `SELECT` 命令，請使用[`SqlCommand` 類別](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)。

除了交易教學課程[中的包裝資料庫修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md)外，我們也不需要自行撰寫任何低層級的 ADO.NET 程式碼，因為 tableadapter 自動產生的程式碼包含連接到資料庫所需的功能、發出命令、抓取資料，並將該資料填入 datatable。 不過，有時候我們可能需要自訂這些低層級的設定。 在接下來的幾個步驟中，我們將探討如何利用 Tableadapter 在內部使用的 ADO.NET 物件。

## <a name="step-1-examining-with-the-connection-property"></a>步驟1：使用連接屬性進行檢查

每個 TableAdapter 類別都有指定資料庫連接資訊的 `Connection` 屬性。 這個屬性的資料類型和 `ConnectionString` 值是由 [TableAdapter 設定] [wizard] 中所做的選擇所決定。 回想一下，當我們第一次將 TableAdapter 加入至具類型的資料集時，此 wizard 會向我們詢問資料庫來源（請參閱 [圖 1]）。 第一個步驟中的下拉式清單包括設定檔中所指定的資料庫，以及伺服器總管 s 資料連線中的任何其他資料庫。 如果下拉式清單中沒有想要使用的資料庫，您可以按一下 [新增連接] 按鈕，並提供所需的連接資訊來指定新的資料庫連接。

[![TableAdapter Configuration Wizard 的第一個步驟](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image1.png)

**圖 1**： TableAdapter 設定 Wizard 的第一個步驟（[按一下以查看完整大小的影像](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image3.png)）

讓我們花點時間檢查 TableAdapter `Connection` 屬性的程式碼。 如[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程中所述，我們可以前往 [類別檢視] 視窗來查看自動產生的 TableAdapter 程式碼，向下切入至適當的類別，然後按兩下該成員名稱。

前往 [View] 功能表，然後選擇 [類別檢視] （或輸入 Ctrl + Shift + C），以流覽至 [類別檢視] 視窗。 從 [類別檢視] 視窗的上半部，向下切入至 [`NorthwindTableAdapters`] 命名空間，然後選取 [`ProductsTableAdapter`] 類別。 這會在類別檢視的下半部顯示 `ProductsTableAdapter` s 成員，如 [圖 2] 所示。 按兩下 [`Connection`] 屬性以查看其程式碼。

![按兩下 類別檢視中的 連接 屬性，以查看其自動產生的程式碼](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image4.png)

**圖 2**：按兩下 類別檢視中的連接屬性，以查看其自動產生的程式碼

TableAdapter `Connection` 屬性和其他連接相關的程式碼如下所示：

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample1.vb)]

當 TableAdapter 類別具現化時，`_connection` 的成員變數等於 `Nothing`。 存取 `Connection` 屬性時，會先檢查 `_connection` 的成員變數是否已具現化。 如果沒有，則會叫用 `InitConnection` 方法，它會將 `_connection` 具現化，並將其 `ConnectionString` 屬性設定為從 TableAdapter Configuration wizard 第一個步驟指定的連接字串值。

`Connection` 屬性也可以指派給 `SqlConnection` 物件。 這麼做會使新的 `SqlConnection` 物件與每個 TableAdapter `SqlCommand` 物件產生關聯。

## <a name="step-2-exposing-connection-level-settings"></a>步驟2：公開連接層級設定

連接資訊應該保持封裝在 TableAdapter 內，而應用程式架構中的其他層則無法存取。 不過，在某些情況下，可能需要為查詢、使用者或 ASP.NET 網頁存取或自訂 TableAdapter 的連接層級資訊。

讓 s 擴充 `Northwind` 資料集中的 `ProductsTableAdapter`，使其包含可供商務邏輯層用來讀取或變更 TableAdapter 所使用之連接字串的 `ConnectionString` 屬性。

> [!NOTE]
> *連接字串*是一個字串，用來指定資料庫連接資訊，例如要使用的提供者、資料庫的位置、驗證認證，以及其他與資料庫相關的設定。 如需各種資料存放區和提供者所使用的連接字串模式清單，請參閱[ConnectionStrings.com](http://www.connectionstrings.com/)。

如[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程所述，具類型資料集 s 自動產生的類別可以透過使用部分類別來擴充。 首先，在名為 `ConnectionAndCommandSettings` 的專案中，于 [`~/App_Code/DAL`] 資料夾之下建立新的子資料夾。

![新增名為 ConnectionAndCommandSettings 的子資料夾](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image5.png)

**圖 3**：新增名為 `ConnectionAndCommandSettings` 的子資料夾

新增名為 `ProductsTableAdapter.ConnectionAndCommandSettings.vb` 的類別檔案，並輸入下列程式碼：

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample2.vb)]

這個部分類別會將名為 `ConnectionString` 的 `Public` 屬性加入至 `ProductsTableAdapter` 類別，讓任何圖層都可以讀取或更新 TableAdapter s 基礎連接的連接字串。

在建立（並儲存）這個部分類別的情況下，開啟 [`ProductsBLL`] 類別。 移至其中一個現有的方法，並在 `Adapter` 中輸入，然後按 [period] 鍵以顯示 IntelliSense。 您應該會在 IntelliSense 中看到新的 `ConnectionString` 屬性，這表示您可以透過程式設計方式從 BLL 讀取或調整此值。

## <a name="exposing-the-entire-connection-object"></a>公開整個連線物件

這個部分類別只會公開基礎連線物件的一個屬性： `ConnectionString`。 如果您想要讓整個連線物件可供 TableAdapter 的範圍外使用，您也可以變更 `Connection` 屬性 s 保護等級。 我們在步驟1中檢查的自動產生程式碼顯示 TableAdapter s `Connection` 屬性標示為 `Friend`，這表示它只能由相同元件中的類別存取。 不過，這可以透過 TableAdapter `ConnectionModifier` 屬性來變更。

開啟 `Northwind` 資料集，按一下設計工具中的 `ProductsTableAdapter`，然後流覽至 屬性視窗。 在這裡，您會看到 `ConnectionModifier` 設為其預設值 `Assembly`。 若要讓 `Connection` 屬性可在具類型資料集元件的外部使用，請將 `ConnectionModifier` 屬性變更為 [`Public`]。

[![可以透過 ConnectionModifier 屬性設定連線屬性的存取範圍層級](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image6.png)

**圖 4**： `Connection` 屬性 s 存取範圍層級可以透過 [`ConnectionModifier`] 屬性來設定（[按一下以查看完整大小的影像](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image8.png)）

儲存資料集，然後返回 `ProductsBLL` 類別。 如先前所示，移至其中一個現有的方法，然後在 `Adapter` 中輸入，然後按 [period] 鍵以顯示 IntelliSense。 此清單應包含 `Connection` 屬性，這表示您現在可以程式設計方式從 BLL 讀取或指派任何連線層級的設定。

## <a name="step-3-examining-the-command-related-properties"></a>步驟3：檢查與命令相關的屬性

TableAdapter 是由主查詢所組成，根據預設，它具有自動產生的 `INSERT`、`UPDATE`和 `DELETE` 語句。 此主要查詢 `INSERT`、`UPDATE`和 `DELETE` 語句會透過 `Adapter` 屬性，實作為 ADO.NET 資料介面卡物件，在 TableAdapter s 程式碼中執行。 就像它的 `Connection` 屬性一樣，`Adapter` 屬性 s 資料類型是由所使用的資料提供者所決定。 由於這些教學課程會使用 SqlClient 提供者，因此 `Adapter` 屬性的類型[`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)。

TableAdapter 的 `Adapter` 屬性有三種類型 `SqlCommand` 的屬性，用來發出 `INSERT`、`UPDATE`和 `DELETE` 語句：

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

`SqlCommand` 物件負責將特定查詢傳送至資料庫，而且具有如下的屬性： [`CommandText`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx)，其中包含要執行的臨機操作 SQL 語句或預存程式;和[`Parameters`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx)，這是 `SqlParameter` 物件的集合。 如我們在[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程中所見，您可以透過屬性視窗自訂這些命令物件。

除了其主要查詢以外，TableAdapter 也可以包含可變數目的方法，當叫用時，會將指定的命令分派給資料庫。 所有其他方法的主要查詢 s 命令物件和命令物件都儲存在 TableAdapter s `CommandCollection` 屬性中。

讓我們花一點時間查看 `Northwind` DataSet 中的 `ProductsTableAdapter` 所產生的程式碼，這兩個屬性及其支援的成員變數和 helper 方法如下：

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample3.vb)]

`Adapter` 和 `CommandCollection` 屬性的程式碼會密切模擬 `Connection` 屬性的。 有些成員變數會保存屬性所使用的物件。 `Get` 存取子的屬性一開始會先檢查是否 `Nothing`對應的成員變數。 若是如此，則會呼叫初始化方法，以建立成員變數的實例，並指派與核心命令相關的屬性。

## <a name="step-4-exposing-command-level-settings"></a>步驟4：公開命令層級設定

在理想的情況下，命令層級資訊應保持封裝在資料存取層內。 如果架構的其他層需要這項資訊，則可以透過部分類別公開，就像使用連接層級設定一樣。

由於 TableAdapter 只有一個 `Connection` 屬性，因此公開連接層級設定的程式碼相當簡單。 修改命令層級設定時，會比較複雜一點，因為 TableAdapter 可以有多個命令物件（`InsertCommand`、`UpdateCommand`和 `DeleteCommand`，以及 `CommandCollection` 屬性中的命令物件數目不定。 更新命令層級設定時，必須將這些設定傳播至所有命令物件。

例如，假設 TableAdapter 中有一些查詢需要花很長的時間來執行。 當使用 TableAdapter 來執行其中一個查詢時，我們可能會想要增加 command 物件的[`CommandTimeout` 屬性](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)。 這個屬性會指定等待命令執行的秒數，並將預設值設為30。

若要允許 BLL 調整 `CommandTimeout` 屬性，請使用在步驟2（`ProductsTableAdapter.ConnectionAndCommandSettings.vb`）中建立的部分類別檔案，將下列 `Public` 方法新增至 `ProductsDataTable`：

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample4.vb)]

您可以從 BLL 或展示層叫用這個方法，為該 TableAdapter 實例的所有命令設定命令逾時。

> [!NOTE]
> `Adapter` 和 `CommandCollection` 屬性會標示為 `Private`，這表示它們只能從 TableAdapter 內的程式碼存取。 不同于 `Connection` 屬性，無法設定這些存取修飾詞。 因此，如果您需要將命令層級屬性公開給架構中的其他層，您必須使用上述的部分類別方法，提供可讀取或寫入 `Private` 命令物件的 `Public` 方法或屬性。

## <a name="summary"></a>總結

具類型資料集內的 Tableadapter 可封裝資料存取的詳細資訊和複雜度。 使用 Tableadapter，我們不需要擔心撰寫 ADO.NET 程式碼來連接到資料庫、發出命令，或將結果填入 DataTable。 系統會自動為我們處理。

不過，有時我們需要自訂低層級的 ADO.NET 細節，例如變更連接字串或預設連接或命令逾時值。 TableAdapter 具有自動產生的 `Connection`、`Adapter`和 `CommandCollection` 屬性，但預設為 `Friend` 或 `Private`。 藉由使用部分類別擴充 TableAdapter 以包含 `Public` 方法或屬性，即可公開此內部資訊。 或者，您可以透過 TableAdapter 的 `ConnectionModifier` 屬性來設定 TableAdapter 的 `Connection` 屬性存取修飾詞。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Burnadette Leigh、S ren Jacob Lauritsen、Teresa Murphy 和 Hilton Geisenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](working-with-computed-columns-vb.md)
> [下一頁](protecting-connection-strings-and-other-configuration-information-vb.md)
