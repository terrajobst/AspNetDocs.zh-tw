---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 針對具類型資料集的 Tableadapter 使用現有的預存程式（VB） |Microsoft Docs
author: rick-anderson
description: 在上一個教學課程中，我們已瞭解如何使用 TableAdapter Wizard 來產生新的預存程式。 在本教學課程中，我們將瞭解相同的 TableAdapter 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 2da25f6a-757e-4e7b-a812-1575288d8f7a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: e35c3d6a98516a07f6119e6cb9dbeb99bc28fe33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78531798"
---
# <a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>使用具類型資料集 Tableadapter 現有的預存程序 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_VB.zip)或[下載 PDF](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial68vb1.pdf)

> 在上一個教學課程中，我們已瞭解如何使用 TableAdapter Wizard 來產生新的預存程式。 在本教學課程中，我們將瞭解相同的 TableAdapter Wizard 如何使用現有的預存程式。 我們也會學習如何以手動方式將新的預存程式加入至我們的資料庫。

## <a name="introduction"></a>簡介

在[先前的教學](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)課程中，我們已瞭解如何將具類型資料集的 tableadapter 設定為使用預存程式來存取資料，而不是特定的 SQL 語句。 特別是，我們已檢查如何讓 TableAdapter wizard 自動建立這些預存程式。 將繼承應用程式移植到 ASP.NET 2.0 時，或在現有的資料模型周圍建立 ASP.NET 2.0 網站時，資料庫可能已經包含我們所需的預存程式。 或者，您可能會想要手動建立預存程式，或透過自動產生預存程式的 TableAdapter wizard 以外的某個工具來建立。

在本教學課程中，我們將探討如何設定 TableAdapter 以使用現有的預存程式。 由於 Northwind 資料庫只有一小部分的內建預存程式，因此我們也會探討透過 Visual Studio 環境，手動將新的預存程式加入至資料庫所需的步驟。 讓我們開始吧！

> [!NOTE]
> 在交易中的[包裝資料庫修改](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教學課程中，我們已將方法新增至 TableAdapter，以支援交易（`BeginTransaction`、`CommitTransaction`等等）。 或者，您可以完全在預存程式內管理交易，而不需要修改資料存取層程式碼。 在本教學課程中，我們將探索用來在交易範圍內執行預存程式 s 語句的 T-sql 命令。

## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>步驟1：將預存程式加入至 Northwind 資料庫

Visual Studio 可讓您輕鬆地將新的預存程式加入至資料庫。 讓 s 將新的預存程式加入 Northwind 資料庫，以傳回 `Products` 資料表中具有特定 `CategoryID` 值的所有資料行。 從 [伺服器總管] 視窗中，展開 Northwind 資料庫，使其資料夾（資料庫關係圖、資料表、視圖等等）顯示。 如先前的教學課程中所見，[預存程式] 資料夾包含資料庫的現有預存程式。 若要加入新的預存程式，只要以滑鼠右鍵按一下 [預存程式] 資料夾，然後從內容功能表選擇 [加入新的預存程式] 選項即可。

[![以滑鼠右鍵按一下 [預存程式] 資料夾，並加入新的預存程式](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**圖 1**：以滑鼠右鍵按一下 [預存程式] 資料夾，並加入新的預存程式（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)）

如 圖 1 所示，選取 加入新的預存程式 選項會在 Visual Studio 中開啟一個腳本視窗，其中包含建立預存程式所需之 SQL 腳本的外框。 我們的工作是要充實此腳本並加以執行，此時將會在資料庫中加入預存程式。

輸入下列腳本：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

執行此腳本時，會將新的預存程式加入至名為 `Products_SelectByCategoryID`的 Northwind 資料庫。 這個預存程式會接受 `int`類型的單一輸入參數（`@CategoryID`），並傳回具有相符 `CategoryID` 值的所有產品欄位。

若要執行此 `CREATE PROCEDURE` 腳本，並將預存程式加入資料庫，請按一下工具列中的 [儲存] 圖示，或按 Ctrl + S。 這麼做之後，[預存程式] 資料夾會重新整理，並顯示新建立的預存程式。 此外，視窗中的腳本會將奧妙從 `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` 變更為 `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`。 `CREATE PROCEDURE` 會將新的預存程式加入至資料庫，而 `ALTER PROCEDURE` 會更新現有的進程。 由於腳本的開頭已變更為 `ALTER PROCEDURE`，因此，變更預存程式的輸入參數或 SQL 語句，然後按一下 [儲存] 圖示，將會使用這些變更來更新預存程式。

[圖 2] 顯示儲存 `Products_SelectByCategoryID` 預存程式之後 Visual Studio。

[![預存程式 Products_SelectByCategoryID 已加入資料庫中](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)

**圖 2**：預存程式 `Products_SelectByCategoryID` 已新增至資料庫（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)）

## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>步驟2：設定 TableAdapter 使用現有的預存程式

既然 `Products_SelectByCategoryID` 預存程式已新增至資料庫，我們就可以在叫用其其中一個方法時，設定資料存取層來使用這個預存程式。 特別的是，我們會將 `GetProductsByCategoryID(<_i22_>categoryID)<!--_i22_-->` 方法加入至 `NorthwindWithSprocs` 具類型資料集內的 `ProductsTableAdapter`，以呼叫我們剛才建立的 `Products_SelectByCategoryID` 預存程式。

從開啟 `NorthwindWithSprocs` 資料集開始。 以滑鼠右鍵按一下 `ProductsTableAdapter`，然後選擇 [加入查詢] 來啟動 [TableAdapter 查詢設定向導]。 在[先前的教學](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)課程中，我們選擇讓 TableAdapter 為我們建立新的預存程式。 不過，在本教學課程中，我們想要將新的 TableAdapter 方法連接到現有的 `Products_SelectByCategoryID` 預存程式。 因此，請從 wizard 的第一個步驟中選擇 [使用現有的預存程式] 選項，然後按 [下一步]。

[![選擇 [使用現有的預存程式] 選項](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)

**圖 3**：選擇 [使用現有的預存程式] 選項（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)）

下列畫面提供的下拉式清單會填入資料庫的預存程式。 選取預存程式會在左邊列出其輸入參數，並在右邊傳回資料欄位（如果有的話）。 從清單中選擇 [`Products_SelectByCategoryID` 預存程式]，然後按 [下一步]。

[![挑選 Products_SelectByCategoryID 預存程式](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)

**圖 4**：挑選 `Products_SelectByCategoryID` 預存程式（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)）

下一個畫面會詢問預存程式所傳回的資料種類，而這裡的答案會決定 TableAdapter s 方法所傳回的型別。 例如，如果我們指出會傳回表格式資料，此方法將會傳回一個 `ProductsDataTable` 實例，其中填入了預存程式所傳回的記錄。 相反地，如果我們指出此預存程式會傳回單一值，TableAdapter 會傳回 `Object`，而該值會指派給預存程式所傳回之第一個記錄的第一個資料行中的值。

因為 `Products_SelectByCategoryID` 預存程式會傳回屬於特定分類的所有產品，請選擇第一個回應-表格式資料-然後按 [下一步]。

[![表示預存程式會傳回表格式資料](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)

**圖 5**：表示預存程式會傳回表格式資料（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png)）

剩下的就是指出要使用的方法模式，後面接著這些方法的名稱。 將 [填滿 DataTable] 和 [傳回 DataTable 選項] 保持勾選，但將方法重新命名為 `FillByCategoryID` 和 `GetProductsByCategoryID`。 然後按 [下一步]，以查看嚮導將執行之工作的摘要。 如果一切看起來正確，請按一下 [完成]。

[![將方法命名為 FillByCategoryID 和 GetProductsByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**圖 6**：命名方法 `FillByCategoryID` 和 `GetProductsByCategoryID` （[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png)）

> [!NOTE]
> 我們剛才建立、`FillByCategoryID` 和 `GetProductsByCategoryID`的 TableAdapter 方法，預期 `Integer`類型的輸入參數。 這個輸入參數值會透過其 `@CategoryID` 參數傳遞至預存程式。 如果您修改 `Products_SelectByCategory` 預存程式的參數，則也必須更新這些 TableAdapter 方法的參數。 如[前一個教學](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)課程所討論，這可以透過下列兩種方式的其中一種來完成：手動新增或移除參數集合中的參數，或重新執行 TableAdapter wizard。

## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>步驟3：將`GetProductsByCategoryID(categoryID)`方法新增到 BLL

在 `GetProductsByCategoryID` DAL 方法完成後，下一個步驟是在商務邏輯層中提供此方法的存取權。 開啟 `ProductsBLLWithSprocs` 類別檔案，並新增下列方法：

[!code-vb[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.vb)]

這個 BLL 方法只會傳回從 `ProductsTableAdapter` s `GetProductsByCategoryID` 方法傳回的 `ProductsDataTable`。 `DataObjectMethodAttribute` 屬性會提供 ObjectDataSource s [設定資料來源] 嚮導所使用的中繼資料。 特別是，此方法會出現在 [選取索引標籤] 下拉式清單中。

## <a name="step-4-displaying-products-by-category"></a>步驟4：依類別顯示產品

若要測試新增的 `Products_SelectByCategoryID` 預存程式和對應的 DAL 和 BLL 方法，讓 s 建立一個包含 DropDownList 和 GridView 的 ASP.NET 網頁。 DropDownList 將會列出資料庫中的所有類別，而 GridView 會顯示屬於所選類別目錄的產品。

> [!NOTE]
> 我們已在先前的教學課程中使用 Dropdownlist 進行建立主要/詳細資料介面。 如需深入瞭解如何執行這類主要/詳細資料包告，請參閱[使用 DropDownList 的主要/詳細資料篩選](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)教學課程。

開啟 [`AdvancedDAL`] 資料夾中的 [`ExistingSprocs.aspx`] 頁面，並將 DropDownList 從 [工具箱] 拖曳至設計工具。 將 DropDownList s `ID` 屬性設為 `Categories`，並將其 `AutoPostBack` 屬性設定為 `True`。 接下來，從其智慧標籤，將 DropDownList 系結至名為 `CategoriesDataSource`的新 ObjectDataSource。 設定 ObjectDataSource，使其從 `CategoriesBLL` 類別的 `GetCategories` 方法中抓取其資料。 將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![從 CategoriesBLL 類別的 GetCategories 方法取出資料](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**圖 7**：從 `CategoriesBLL` 類別的 `GetCategories` 方法取出資料（[按一下以觀看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png)）

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)

**圖 8**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png)）

完成 ObjectDataSource wizard 之後，將 DropDownList 設定為顯示 `CategoryName` 資料欄位，並使用 [`CategoryID`] 欄位做為每個 `ListItem`的 `Value`。

此時，DropDownList 和 ObjectDataSource 的宣告式標記應該如下所示：

[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.aspx)]

接下來，將 GridView 拖曳至設計工具上，並將它放在 DropDownList 之下。 將 GridView 的 `ID` 設定為 `ProductsByCategory` 並從其智慧標籤，將它系結至名為 `ProductsByCategoryDataSource`的新 ObjectDataSource。 將 `ProductsByCategoryDataSource` ObjectDataSource 設定為使用 `ProductsBLLWithSprocs` 類別，讓它使用 `GetProductsByCategoryID(categoryID)` 方法來抓取其資料。 由於此 GridView 只會用來顯示資料，請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]，然後按 [下一步]。

[![將 ObjectDataSource 設定為使用 ProductsBLLWithSprocs 類別](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)

**圖 9**：設定 ObjectDataSource 使用 `ProductsBLLWithSprocs` 類別（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png)）

[![從 GetProductsByCategoryID （類別 Id）方法取出資料](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)

**圖 10**：從 `GetProductsByCategoryID(categoryID)` 方法取出資料（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png)）

在 [選取] 索引標籤中選擇的方法需要參數，因此 wizard 的最後一個步驟會提示我們輸入參數 s 來源。 將 [參數來源] 下拉式清單設定為 [控制]，然後從 [ControlID] 下拉式清單中選擇 [`Categories`] 控制項。 按一下 [完成] 完成精靈。

[![使用分類 DropDownList 做為類別目錄參數的來源](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**圖 11**：使用 `Categories` DropDownList 做為 `categoryID` 參數的來源（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png)）

完成 ObjectDataSource wizard 之後，Visual Studio 將會為每個產品資料欄位新增 BoundFields 和 CheckBoxField。 您可以視需要隨意自訂這些欄位。

透過瀏覽器造訪頁面。 流覽頁面時，會選取 [飲料] 類別，並在方格中列出對應的產品。 將下拉式清單變更為替代類別目錄，如 [圖 12] 所示，會導致回傳，並以新選取之類別的產品重載格線。

[隨即顯示 [產生] 分類中的產品 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**圖 12**：顯示 [產生] 分類中的產品（[按一下以觀看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)）

## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>步驟5：在交易的範圍內包裝預存程式 s 語句

在交易中的[包裝資料庫修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md)教學課程中，我們討論了在交易範圍內執行一系列資料庫修改語句的技術。 回想一下，在交易的傘之下執行的修改全都成功或全部失敗，以確保不可部分完成性。 使用交易的技巧包括：

- 使用 `System.Transactions` 命名空間中的類別，
- 讓資料存取層使用 ADO.NET 類別，例如 `SqlTransaction`，以及
- 直接在預存程式內加入 T-sql transaction 命令

交易教學課程*中的包裝資料庫修改*使用 DAL 中的 ADO.NET 類別。 本教學課程的其餘部分將探討如何使用預存程式內的 T-sql 命令來管理交易。

用於手動啟動、認可和回復交易的三個關鍵 SQL 命令分別是 `BEGIN TRANSACTION`、`COMMIT TRANSACTION`和 `ROLLBACK TRANSACTION`。 如同使用 ADO.NET 方法，從預存程式內使用交易時，我們必須套用下列模式：

1. 指出交易的開始。
2. 執行組成交易的 SQL 語句。
3. 如果步驟2中的任何一個語句發生錯誤，就會回復交易。
4. 如果步驟2中的所有語句都完成但沒有發生錯誤，請認可交易。

您可以使用下列範本，在 T-sql 語法中實作為此模式：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

此範本一開始會定義 `TRY...CATCH` 區塊，這是 SQL Server 2005 的新結構。 如同 Visual Basic 中的 `Try...Catch` 區塊，SQL `TRY...CATCH` 區塊會執行 `TRY` 區塊中的語句。 如果有任何語句引發錯誤，控制權會立即傳送至 `CATCH` 區塊。

如果執行構成交易的 SQL 語句時沒有任何錯誤，`COMMIT TRANSACTION` 語句會認可變更並完成交易。 但是，如果其中一個語句導致錯誤，則 `CATCH` 區塊中的 `ROLLBACK TRANSACTION` 會將資料庫傳回至交易開始之前的狀態。 預存程式也會使用[RAISERROR 命令](https://msdn.microsoft.com/library/ms178592.aspx)引發錯誤，這會導致在應用程式中引發 `SqlException`。

> [!NOTE]
> 由於 `TRY...CATCH` 區塊是 SQL Server 2005 的新手，因此如果您使用舊版的 Microsoft SQL Server，上述範本將無法使用。 如果您不是使用 SQL Server 2005，請參閱[管理 SQL Server 預存程式中的交易](http://www.4guysfromrolla.com/webtech/080305-1.shtml)，以取得可與其他版本 SQL Server 搭配使用的範本。

讓我們看一下具體的範例。 `Categories` 和 `Products` 資料表之間存在外鍵條件約束，這表示 `Products` 資料表中的每個 `CategoryID` 欄位都必須對應到 `CategoryID` 資料表中的 `Categories` 值。 任何會違反此條件約束的動作（例如，嘗試刪除具有相關聯產品的類別）都會導致外鍵條件約束違規。 若要確認這一點，請造訪使用二進位資料一節（`~/BinaryData/UpdatingAndDeleting.aspx`）中的更新和刪除現有的二進位資料範例。 此頁面會列出系統中的每個類別，以及 [編輯] 和 [刪除] 按鈕（請參閱 [圖 13]），但如果您嘗試刪除具有相關產品（例如飲料）的類別，則刪除作業會因為外鍵條件約束違規而失敗（請參閱 [圖 14]）。

[![每個類別都會顯示在具有 [編輯] 和 [刪除] 按鈕的 GridView 中](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)

**圖 13**：每個類別目錄都會顯示在具有 [編輯] 和 [刪除] 按鈕的 GridView 中（[按一下以查看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)）

[![您無法刪除具有現有產品的類別](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)

**圖 14**：您無法刪除具有現有產品的類別（[按一下以觀看完整大小的影像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)）

不過，假設我們想要允許刪除類別，而不論它們是否有相關聯的產品。 如果您要刪除包含產品的類別，請想像我們也想要刪除其現有的產品（雖然另一個選項是將其產品 `CategoryID` 值設定為 `NULL`）。 這項功能可以透過 foreign key 條件約束的 cascade 規則來執行。 或者，我們可以建立一個可接受 `@CategoryID` 輸入參數的預存程式，並在叫用時明確刪除所有相關聯的產品，然後再將指定的分類。

第一次嘗試這種預存程式時，可能如下所示：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

雖然這絕對會刪除相關聯的產品和類別，但它不會在交易的傘下這麼做。 假設 `Categories` 上有一些其他外鍵條件約束會禁止刪除特定的 `@CategoryID` 值。 問題在於，在這種情況下，我們會先刪除所有產品，再嘗試刪除類別。 最後的結果是，對於這類類別而言，這個預存程式會移除其所有產品，而類別會保留，因為它在其他資料表中仍有相關的記錄。

不過，如果預存程式已包裝在交易的範圍內，則會在 `Categories`的刪除失敗時，回復 `Products` 資料表的刪除。 下列預存程式腳本會使用交易來確保兩個 `DELETE` 語句之間的不可部分完成性：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.sql)]

請花點時間將 `Categories_Delete` 預存程式加入至 Northwind 資料庫。 如需將預存程式加入資料庫的指示，請參閱步驟1。

## <a name="step-6-updating-thecategoriestableadapter"></a>步驟6：更新`CategoriesTableAdapter`

當我們將 `Categories_Delete` 預存程式新增至資料庫時，DAL 目前已設定為使用臨機操作 SQL 語句來執行刪除。 我們需要更新 `CategoriesTableAdapter`，並指示它改用 `Categories_Delete` 預存程式。

> [!NOTE]
> 稍早在本教學課程中，我們使用的是 `NorthwindWithSprocs` 資料集。 但是，該資料集只有單一實體，`ProductsDataTable`，而且我們需要使用類別。 因此，在本教學課程的其餘部分，當我討論資料存取層時，我會參考 `Northwind` 資料集，這是我們在[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程中建立的一項。

開啟 Northwind 資料集，選取 [`CategoriesTableAdapter`]，然後移至 [屬性視窗]。 屬性視窗會列出 TableAdapter 所使用的 `InsertCommand`、`UpdateCommand`、`DeleteCommand`和 `SelectCommand`，以及其名稱和連接資訊。 展開 [`DeleteCommand`] 屬性，以查看其詳細資料。 如 [圖 15] 所示，[`DeleteCommand` s `CommandType`] 屬性設為 [文字]，它會指示它將 `CommandText` 屬性中的文字當做臨機操作 SQL 查詢傳送。

![在設計工具中選取 CategoriesTableAdapter，以在 [屬性] 視窗中查看其屬性](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)

**圖 15**：在設計工具中選取 `CategoriesTableAdapter`，以在 [屬性] 視窗中查看其屬性

若要變更這些設定，請選取屬性視窗中的（DeleteCommand）文字，然後從下拉式清單中選擇 [（新增）]。 這會清除 [`CommandText`]、[`CommandType`] 和 [`Parameters`] 屬性的設定。 接下來，將 [`CommandType`] 屬性設定為 [`StoredProcedure`]，然後輸入 `CommandText` 的預存程式名稱（`dbo.Categories_Delete`）。 如果您確定依照此順序輸入屬性-首先是 `CommandType`，然後 `CommandText` Visual Studio 會自動填入參數集合。 如果您未依照此順序輸入這些屬性，就必須透過 [參數集合編輯器] 手動新增參數。 不論是哪一種情況，請務必按一下 [參數] 屬性中的省略號，以顯示 [參數集合編輯器]，以確認已進行正確的參數設定變更（請參閱 [圖 16]）。 如果您在對話方塊中看不到任何參數，請手動加入 `@CategoryID` 參數（您不需要加入 `@RETURN_VALUE` 參數）。

![確定參數設定正確](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**圖 16**：確定參數設定是否正確

一旦 DAL 已更新，刪除類別目錄就會自動刪除其所有相關聯的產品，並在交易的傘下執行此動作。 若要確認這一點，請回到 [更新和刪除現有的二進位資料] 頁面，然後按一下其中一個類別的 [刪除] 按鈕。 只要按一下滑鼠，就會刪除類別及其所有相關聯的產品。

> [!NOTE]
> 在測試 `Categories_Delete` 預存程式之前，會刪除多個產品以及選取的類別目錄，因此建立資料庫的備份複本可能會很謹慎。 如果您使用 `App_Data`中的 `NORTHWND.MDF` 資料庫，只需關閉 Visual Studio，並將 `App_Data` 中的 MDF 和 LDF 檔案複製到其他資料夾。 測試功能之後，您可以藉由關閉 Visual Studio 來還原資料庫，並以備份複本取代 `App_Data` 中目前的 MDF 和 LDF 檔案。

## <a name="summary"></a>總結

雖然 TableAdapter 的 wizard 會為我們自動產生預存程式，但有時候我們可能已經建立了這類預存程式，或想要以手動方式或使用其他工具來建立它們。 為了配合這類案例，TableAdapter 也可以設定為指向現有的預存程式。 在本教學課程中，我們探討了如何透過 Visual Studio 環境，以手動方式將預存程式新增至資料庫，以及如何將 TableAdapter 的方法與這些預存程式連線。 我們也檢查了用來從預存程式內啟動、認可和回復交易的 T-sql 命令和腳本模式。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Geisenow、S ren Jacob Lauritsen 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [下一頁](updating-the-tableadapter-to-use-joins-vb.md)
