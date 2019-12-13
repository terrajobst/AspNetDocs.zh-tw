---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
title: 新增其他 DataTable 資料行（VB） |Microsoft Docs
author: rick-anderson
description: 使用 TableAdapter Wizard 建立具類型的資料集時，對應的 DataTable 會包含主資料庫查詢所傳回的資料行。 但是 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 1e8e65f9-fe3e-4250-810b-c90227786bed
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: 3a55f8bc4d3508387927ca81674073a001867de7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74608466"
---
# <a name="adding-additional-datatable-columns-vb"></a>新增其他 DataTable 資料行 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_VB.zip)或[下載 PDF](adding-additional-datatable-columns-vb/_static/datatutorial70vb1.pdf)

> 使用 TableAdapter Wizard 建立具類型的資料集時，對應的 DataTable 會包含主資料庫查詢所傳回的資料行。 但是，在某些情況下，DataTable 需要包含額外的資料行。 在本教學課程中，我們將瞭解當我們需要其他 DataTable 資料行時，建議使用預存程式。

## <a name="introduction"></a>簡介

將 TableAdapter 加入至具類型的資料集時，對應的 DataTable s 架構是由 TableAdapter s 主查詢所決定。 例如，如果主要查詢傳回資料欄位*a*、 *b*和*c*，DataTable 將會有三個對應的資料行，名為*a*、 *b*和*c*。除了其主要查詢以外，TableAdapter 還可以包含其他查詢，以根據某些參數傳回資料的子集。 例如，除了會傳回所有產品相關資訊的 `ProductsTableAdapter` s 主查詢之外，它也包含 `GetProductsByCategoryID(categoryID)` 和 `GetProductByProductID(productID)`之類的方法，其會根據提供的參數傳回特定產品資訊。

如果所有 TableAdapter s 方法傳回的資料欄位與主要查詢中所指定的欄位相同或更少，則擁有 DataTable 架構的模型會反映 TableAdapter 的主查詢運作良好。 如果 TableAdapter 方法需要傳回額外的資料欄位，則應該據以展開 DataTable 架構。 在主要[/詳細資料中，使用具有詳細資料 DataList 教學課程的主要記錄項目符號清單](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)，我們已將方法新增至傳回主要查詢中定義之 `CategoryID`、`CategoryName`和 `Description` 資料欄位的 `CategoriesTableAdapter`，再加上 `NumberOfProducts`，這是報告與每個類別目錄相關聯之產品數目的額外資料欄位。 我們會以手動方式將新的資料行新增至 `CategoriesDataTable`，以便從這個新的方法中捕捉 `NumberOfProducts` 的資料欄值。

如[上傳](../working-with-binary-files/uploading-files-vb.md)檔案教學課程中所述，您必須特別注意使用臨機操作 SQL 語句的 tableadapter，以及其資料欄位不會精確符合主要查詢的方法。 如果重新執行 TableAdapter 設定向導，它會更新所有 TableAdapter 的方法，使其資料欄位清單與主要查詢相符。 因此，任何具有自訂資料行清單的方法都會還原成主要查詢的資料行清單，而不會傳回預期的資料。 使用預存程式時，不會發生這個問題。

在本教學課程中，我們將探討如何擴充 DataTable 架構以包含額外的資料行。 由於在使用臨機操作 SQL 語句時，會肯定脆弱度 TableAdapter，因此在本教學課程中，我們將使用預存程式。 如需有關設定 TableAdapter 以使用預存程式的詳細資訊，請參閱 <<c0>為具類型的資料集 Tableadapter 建立新的預存程式和[使用 Tableadapter 的資料集的現有預存程式](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教學課程。

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>步驟 1:將`PriceQuartile`資料行加入至`ProductsDataTable`

在*針對具類型資料集的 Tableadapter 建立新的預存程式*教學課程中，我們建立了名為 `NorthwindWithSprocs`的具類型資料集。 此資料集目前包含兩個 Datatable： `ProductsDataTable` 和 `EmployeesDataTable`。 `ProductsTableAdapter` 具有下列三種方法：

- `GetProducts`-主要查詢，會傳回 `Products` 資料表中的所有記錄
- `GetProductsByCategoryID(categoryID)`-傳回具有指定之*類別*的所有產品。
- `GetProductByProductID(productID)`-傳回具有指定*productID*的特定產品。

主要查詢和兩個其他方法全都會傳回相同的資料欄位集，也就是 `Products` 資料表中的所有資料行。 沒有相互關聯的子查詢或 `JOIN` s 從 `Categories` 或 `Suppliers` 資料表提取相關資料。 因此，`ProductsDataTable` 具有 `Products` 資料表中每個欄位的對應資料行。

在本教學課程中，我們會將方法新增至名為 `GetProductsWithPriceQuartile` 的 `ProductsTableAdapter`，以傳回所有產品。 除了標準產品資料欄位以外，`GetProductsWithPriceQuartile` 也會包含 `PriceQuartile` 的資料欄位，以指出產品的價格為四分位。 例如，價格是最昂貴25% 的產品會有 `PriceQuartile` 值1，而其價格落在底部25% 的產品會有4的值。 不過，在我們擔心如何建立預存程式來傳回這份資訊之前，我們必須先更新 `ProductsDataTable`，以便在使用 `GetProductsWithPriceQuartile` 方法時包含資料行來保存 `PriceQuartile` 的結果。

開啟 `NorthwindWithSprocs` 資料集，並以滑鼠右鍵按一下 `ProductsDataTable`。 選擇內容功能表中的 [新增]，然後選取 [資料行]。

[![在 ProductsDataTable 中加入新的資料行](adding-additional-datatable-columns-vb/_static/image2.png)](adding-additional-datatable-columns-vb/_static/image1.png)

**圖 1**：將新的資料行加入至 `ProductsDataTable` （[按一下以查看完整大小的影像](adding-additional-datatable-columns-vb/_static/image3.png)）

這會將新的資料行加入至名為 Column1 的 DataTable，類型為 `System.String`。 我們需要將此資料行的名稱更新為 PriceQuartile，並將其類型更新為 `System.Int32`，因為它將用來保存1到4之間的數位。 在 `ProductsDataTable` 中選取新加入的資料行，然後從屬性視窗，將 `Name` 屬性設為 PriceQuartile，並將 `DataType` 屬性設定為 `System.Int32`。

[![設定新的資料行名稱和資料類型屬性](adding-additional-datatable-columns-vb/_static/image5.png)](adding-additional-datatable-columns-vb/_static/image4.png)

**圖 2**：設定新的資料行 `Name` 並 `DataType` 屬性（[按一下以查看完整大小的影像](adding-additional-datatable-columns-vb/_static/image6.png)）

如 [圖 2] 所示，還有其他可設定的屬性，例如，資料行中的值是否必須是唯一的、如果資料行是自動遞增的資料行、是否允許資料庫 `NULL` 值等等。 將這些值設為其預設值。

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>步驟 2:建立`GetProductsWithPriceQuartile`方法

現在 `ProductsDataTable` 已更新為包含 [`PriceQuartile`] 資料行，我們已準備好建立 `GetProductsWithPriceQuartile` 方法。 首先，以滑鼠右鍵按一下 TableAdapter，然後從內容功能表選擇 [加入查詢]。 這會顯示 [TableAdapter 查詢設定向導]，它會先提示我們是否要使用臨機操作 SQL 語句或新的或現有的預存程式。 因為我們還沒有傳回價格四分資料的預存程式，所以讓 TableAdapter 為我們建立這個預存程式。 選取 [建立新的預存程式] 選項，然後按 [下一步]。

[![指示 TableAdapter Wizard 為我們建立預存程式](adding-additional-datatable-columns-vb/_static/image8.png)](adding-additional-datatable-columns-vb/_static/image7.png)

**圖 3**：指示 [TableAdapter 嚮導] 為我們建立預存程式（[按一下以觀看完整大小的影像](adding-additional-datatable-columns-vb/_static/image9.png)）

在接下來的畫面（如 [圖 4] 所示）中，嚮導會詢問要加入哪一種類型的查詢。 由於 `GetProductsWithPriceQuartile` 方法會傳回 `Products` 資料表中的所有資料行和記錄，請選取 [選取傳回資料列] 選項，然後按 [下一步]。

[![我們的查詢將會是傳回多個資料列的 SELECT 語句](adding-additional-datatable-columns-vb/_static/image11.png)](adding-additional-datatable-columns-vb/_static/image10.png)

**圖 4**：我們的查詢將會是傳回多個資料列的 `SELECT` 語句（[按一下以查看完整大小的影像](adding-additional-datatable-columns-vb/_static/image12.png)）

接下來，系統會提示您輸入 `SELECT` 查詢。 在 wizard 中輸入下列查詢：

[!code-sql[Main](adding-additional-datatable-columns-vb/samples/sample1.sql)]

上述查詢會使用 SQL Server 2005 s new [`NTILE`](https://msdn.microsoft.com/library/ms175126.aspx)函式將結果分成四個群組，其中的群組是由以遞減順序排序的 `UnitPrice` 值所決定。

可惜的是，查詢產生器不知道如何剖析 `OVER` 關鍵字，而且在剖析上述查詢時將會顯示錯誤。 因此，請直接在嚮導的文字方塊中輸入上述查詢，而不使用查詢產生器。

> [!NOTE]
> 如需有關 NTILE 和 SQL Server 2005 s 其他次序函數的詳細資訊，請參閱《 [SQL Server 2005 線上叢書》](https://msdn.microsoft.com/library/ms189798.aspx)中的[使用 Microsoft SQL Server 2005](http://www.4guysfromrolla.com/webtech/010406-1.shtml)和[次序函數一節](https://msdn.microsoft.com/library/ms189798.aspx)傳回等級的結果。

輸入 `SELECT` 查詢並按 [下一步] 之後，嚮導會要求我們提供將建立之預存程式的名稱。 將新的預存程式命名為 `Products_SelectWithPriceQuartile` 然後按 [下一步]。

[![為預存程式命名 Products_SelectWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image14.png)](adding-additional-datatable-columns-vb/_static/image13.png)

**圖 5**：將預存程式命名 `Products_SelectWithPriceQuartile` （[按一下以查看完整大小的影像](adding-additional-datatable-columns-vb/_static/image15.png)）

最後，我們會提示您將 TableAdapter 方法命名為。 將 [填入 DataTable] 和 [傳回 DataTable] 核取方塊保持為已核取，並將方法命名為 `FillWithPriceQuartile` 和 `GetProductsWithPriceQuartile`。

[![命名 TableAdapter s 方法，然後按一下 [完成]](adding-additional-datatable-columns-vb/_static/image17.png)](adding-additional-datatable-columns-vb/_static/image16.png)

**圖 6**：命名 TableAdapter s 方法，然後按一下 [完成] （[按一下以查看完整大小的影像](adding-additional-datatable-columns-vb/_static/image18.png)）

使用指定的 `SELECT` 查詢和名為的預存程式和 TableAdapter 方法，按一下 [完成] 以完成嚮導。 此時，您可能會在嚮導中收到一則警告，指出不支援 `OVER` SQL 結構或語句。 您可以忽略這些警告。

完成 wizard 之後，TableAdapter 應該包含 `FillWithPriceQuartile` 和 `GetProductsWithPriceQuartile` 方法，而資料庫應該包含名為 `Products_SelectWithPriceQuartile`的預存程式。 請花一點時間確認 TableAdapter 確實包含這個新方法，而且預存程式已正確地加入至資料庫。 檢查資料庫時，如果看不到預存程式，請嘗試以滑鼠右鍵按一下 [預存程式] 資料夾，然後選擇 [重新整理]。

![確認新的方法已新增至 TableAdapter](adding-additional-datatable-columns-vb/_static/image19.png)

**圖 7**：確認新的方法已新增至 TableAdapter

[![確保資料庫包含 Products_SelectWithPriceQuartile 預存程式](adding-additional-datatable-columns-vb/_static/image21.png)](adding-additional-datatable-columns-vb/_static/image20.png)

**圖 8**：確定資料庫包含 `Products_SelectWithPriceQuartile` 預存[程式（按一下以查看完整大小的影像](adding-additional-datatable-columns-vb/_static/image22.png)）

> [!NOTE]
> 使用預存程式而非臨機操作 SQL 語句的其中一個優點是，重新執行 TableAdapter 設定 wizard 不會修改預存程式的資料行清單。 以滑鼠右鍵按一下 TableAdapter，從操作功能表中選擇 [設定] 選項以啟動精靈，然後按一下 [完成] 完成作業。 接下來，移至資料庫並查看 `Products_SelectWithPriceQuartile` 預存程式。 請注意，尚未修改其資料行清單。 我們已經使用臨機操作 SQL 語句，重新執行 TableAdapter 設定 wizard 會將此查詢的資料行清單還原成符合主要的查詢資料行清單，藉此從 `GetProductsWithPriceQuartile` 方法所使用的查詢中移除 NTILE 語句。

叫用資料存取層 `GetProductsWithPriceQuartile` 方法時，TableAdapter 會執行 `Products_SelectWithPriceQuartile` 預存程式，並針對每個傳回的記錄，將一個資料列新增至 `ProductsDataTable`。 預存程式所傳回的資料欄位會對應到 `ProductsDataTable` 的資料行。 由於預存程式會傳回 `PriceQuartile` 資料欄位，因此它的值會指派給 `ProductsDataTable` s `PriceQuartile` 資料行。

對於其查詢不會傳回 `PriceQuartile` 資料欄位的 TableAdapter 方法，`PriceQuartile` 資料行 s 值是其 `DefaultValue` 屬性所指定的值。 如 [圖 2] 所示，這個值會設定為預設的 `DBNull`。 如果您偏好使用不同的預設值，只要適當地設定 `DefaultValue` 屬性即可。 只要確定 `DefaultValue` 值在給定資料行 `DataType` （也就是 `PriceQuartile` 資料行的 `System.Int32`）時有效。

此時，我們已執行將額外的資料行新增至 DataTable 的必要步驟。 若要確認此額外資料行是否如預期般運作，請建立 ASP.NET 網頁，以顯示每個產品的名稱、價格和價格四分位。 不過，在這麼做之前，我們必須先更新商務邏輯層，以包含向下呼叫 DAL s `GetProductsWithPriceQuartile` 方法的方法。 我們將在步驟3中更新 BLL，然後在步驟4中建立 [ASP.NET] 頁面。

## <a name="step-3-augmenting-the-business-logic-layer"></a>步驟 3：擴充商務邏輯層

從展示層使用新的 `GetProductsWithPriceQuartile` 方法之前，我們應該先將對應的方法新增到 BLL。 開啟 `ProductsBLLWithSprocs` 類別檔案，並新增下列程式碼：

[!code-vb[Main](adding-additional-datatable-columns-vb/samples/sample2.vb)]

如同 `ProductsBLLWithSprocs`中的其他資料抓取方法，`GetProductsWithPriceQuartile` 方法只會呼叫 DAL 的對應 `GetProductsWithPriceQuartile` 方法，並傳回其結果。

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>步驟 4：在 ASP.NET 的網頁中顯示價格的四分位資訊

完成 BLL 加法之後，我們就準備好建立一個 ASP.NET 網頁，其中顯示每個產品的四位數。 開啟 [`AdvancedDAL`] 資料夾中的 [`AddingColumns.aspx`] 頁面，並將 GridView 從 [工具箱] 拖曳至設計工具，將其 `ID` 屬性設定為 [`Products`]。 從 GridView 的智慧標籤，將它系結至名為 `ProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以使用 `ProductsBLLWithSprocs` 類別的 `GetProductsWithPriceQuartile` 方法。 由於這會是唯讀方格，請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![將 ObjectDataSource 設定為使用 ProductsBLLWithSprocs 類別](adding-additional-datatable-columns-vb/_static/image24.png)](adding-additional-datatable-columns-vb/_static/image23.png)

**圖 9**：設定 ObjectDataSource 使用 `ProductsBLLWithSprocs` 類別（[按一下以查看完整大小的影像](adding-additional-datatable-columns-vb/_static/image25.png)）

[![從 GetProductsWithPriceQuartile 方法取出產品資訊](adding-additional-datatable-columns-vb/_static/image27.png)](adding-additional-datatable-columns-vb/_static/image26.png)

**圖 10**：從 `GetProductsWithPriceQuartile` 方法取出產品資訊（[按一下以觀看完整大小的影像](adding-additional-datatable-columns-vb/_static/image28.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 會自動為方法所傳回的每個資料欄位，將 BoundField 或 CheckBoxField 新增至 GridView。 其中一個資料欄位是 `PriceQuartile`，也就是我們新增至步驟1中 `ProductsDataTable` 的資料行。

編輯 GridView 的欄位，移除 `ProductName`、`UnitPrice`和 `PriceQuartile` BoundFields 以外的所有。 設定 `UnitPrice` BoundField 將其值格式化為貨幣，並分別讓 `UnitPrice` 和 `PriceQuartile` BoundFields 靠右和靠上對齊。 最後，分別將其餘的 BoundFields `HeaderText` 屬性更新為 [產品]、[價格] 和 [價格四分]。 此外，請核取 GridView 的智慧標籤中的 [啟用排序] 核取方塊。

在這些修改之後，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](adding-additional-datatable-columns-vb/samples/sample3.aspx)]

[圖 11] 顯示透過瀏覽器造訪的此頁面。 請注意，一開始，產品會依其價格以遞減順序排序，並將每個產品指派適當的 `PriceQuartile` 值。 當然，這項資料可以依其他條件排序，而價格四分數值資料行值仍會反映產品對於價格的排名（請參閱 [圖 12]）。

[![產品依其價格排序](adding-additional-datatable-columns-vb/_static/image30.png)](adding-additional-datatable-columns-vb/_static/image29.png)

**圖 11**：產品會依其價格排序（[按一下以觀看完整大小的影像](adding-additional-datatable-columns-vb/_static/image31.png)）

[![產品依其名稱排序](adding-additional-datatable-columns-vb/_static/image33.png)](adding-additional-datatable-columns-vb/_static/image32.png)

**圖 12**：產品依其名稱排序（[按一下以觀看完整大小的影像](adding-additional-datatable-columns-vb/_static/image34.png)）

> [!NOTE]
> 只要幾行程式碼，我們就可以擴充 GridView，使其根據其 `PriceQuartile` 值將產品資料列彩色。 我們可能會將這些產品的第一個四個藍色標示為淺綠色，而第二個下的四個為淺黃色，以此類推。 我建議您花一點時間新增這種功能。 如果您需要重新整理 GridView 的格式設定，請參閱以[資料為基礎的自訂格式](../custom-formatting/custom-formatting-based-upon-data-vb.md)教學課程。

## <a name="an-alternative-approach---creating-another-tableadapter"></a>替代方法-建立另一個 TableAdapter

如我們在本教學課程中所見，將方法加入至會傳回主要查詢所述以外之資料欄位的 TableAdapter 時，我們可以將對應的資料行加入至 DataTable。 不過，這種方法只有在 TableAdapter 中有少數方法會傳回不同的資料欄位，而且這些替代資料欄位沒有太多與主查詢的差異時，才會運作良好。

您可以改為將另一個 TableAdapter 加入資料集，而不是將資料行加入至 DataTable，而是包含第一個 TableAdapter 的方法，而後者會傳回不同的資料欄位。 在本教學課程中，我們可以在使用 `Products_SelectWithPriceQuartile` 預存程式做為主要查詢的資料 `ProductsWithPriceQuartileTableAdapter` 集上加入額外的 TableAdapter，而不是將 `PriceQuartile` 資料行加入至 `ProductsDataTable` （僅供 `GetProductsWithPriceQuartile` 方法使用）。 如需取得產品資訊的 ASP.NET 網頁，請以四個分位的方式使用 `ProductsWithPriceQuartileTableAdapter`，但不能繼續使用 `ProductsTableAdapter`。

藉由加入新的 TableAdapter，Datatable 會維持 untarnished，而且其資料行會精確地鏡像其 TableAdapter 方法所傳回的資料欄位。 不過，其他 Tableadapter 可能會引進重複性的工作和功能。 例如，如果顯示 `PriceQuartile` 資料行的那些 ASP.NET 網頁也需要提供 insert、update 和 delete 支援，則 `ProductsWithPriceQuartileTableAdapter` 必須正確設定其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性。 雖然這些屬性會反映 `ProductsTableAdapter` s，但此設定會引進額外的步驟。 此外，現在有兩種方式可更新、刪除或將產品新增至資料庫-透過 `ProductsTableAdapter` 和 `ProductsWithPriceQuartileTableAdapter` 類別。

本教學課程的下載內容包含 `NorthwindWithSprocs` 資料集中的 `ProductsWithPriceQuartileTableAdapter` 類別，其中說明此替代方法。

## <a name="summary"></a>總結

在大部分的情況下，TableAdapter 中的所有方法都會傳回相同的資料欄位集，但有時特定的方法或兩個可能需要傳回額外的欄位。 例如，在[主要/詳細資料中，使用具有詳細資料 DataList 教學課程的主要記錄項目符號清單](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)，我們在 `CategoriesTableAdapter` 中新增了一個方法，除了主要查詢的資料欄位以外，還會傳回一個 `NumberOfProducts` 欄位，其中報告與每個類別相關聯的產品數目。 在本教學課程中，我們探討了在傳回 `PriceQuartile` 欄位的 `ProductsTableAdapter` 中，除了主要查詢的資料欄位以外，還加入了方法。 若要捕捉 TableAdapter s 方法所傳回的其他資料欄位，我們需要將對應的資料行加入至 DataTable。

如果您計畫以手動方式將資料行加入至 DataTable，建議 TableAdapter 使用預存程式。 如果 TableAdapter 使用臨機操作 SQL 語句，則每當執行 TableAdapter 設定向導時，資料欄位清單的所有方法都會還原成主要查詢所傳回的資料欄位。 此問題並不會延伸至預存程式，這就是建議使用並用於本教學課程的原因。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Randy Schmidt、Jacky Goor、Bernadette Leigh 和 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](updating-the-tableadapter-to-use-joins-vb.md)
> [下一頁](working-with-computed-columns-vb.md)
