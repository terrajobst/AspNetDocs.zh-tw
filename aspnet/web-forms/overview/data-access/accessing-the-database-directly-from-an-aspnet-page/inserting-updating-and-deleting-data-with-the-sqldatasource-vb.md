---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
title: 使用 SqlDataSource 插入、更新和刪除資料（VB） |Microsoft Docs
author: rick-anderson
description: 在先前的教學課程中，我們學到了 ObjectDataSource 控制項如何允許插入、更新和刪除資料。 SqlDataSource 控制項支援 t 。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9673bef3-892c-45ba-a7d8-0da3d6f48ec5
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 4f7b282b09769272df8ff3a32aa4c509c8917481
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626557"
---
# <a name="inserting-updating-and-deleting-data-with-the-sqldatasource-vb"></a>使用 SqlDataSource 插入、更新和刪除資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_VB.exe)或[下載 PDF](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/datatutorial49vb1.pdf)

> 在先前的教學課程中，我們學到了 ObjectDataSource 控制項如何允許插入、更新和刪除資料。 SqlDataSource 控制項支援相同的作業，但此方法不同，而本教學課程會示範如何設定 SqlDataSource 來插入、更新和刪除資料。

## <a name="introduction"></a>簡介

如有關[插入、更新和刪除的簡介](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)中所述，GridView 控制項提供內建的更新和刪除功能，而 DetailsView 和 FormView 控制項則包含插入支援以及編輯和刪除功能。 這些資料修改功能可以直接插入資料來源控制項中，而不需要撰寫程式程式碼。 概述使用 ObjectDataSource 進行[的插入、更新和刪除](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)檢查，以加速使用 GridView、DetailsView 和 FormView 控制項進行插入、更新和刪除。 或者，您可以使用 SqlDataSource 來取代 ObjectDataSource。

回想一下，為了支援插入、更新和刪除，我們需要指定要叫用的物件層方法，以執行插入、更新或刪除動作。 在 SqlDataSource 中，我們需要提供要執行的 `INSERT`、`UPDATE`和 `DELETE` SQL 語句（或預存程式）。 如我們在本教學課程中所見，您可以手動建立這些語句，也可以由 SqlDataSource 的 [設定資料來源] [自動產生]。

> [!NOTE]
> 既然我們已經討論過 GridView、DetailsView 和 FormView 控制項的插入、編輯和刪除功能，本教學課程將著重于設定 SqlDataSource 控制項以支援這些作業。 如果您需要在 GridView、DetailsView 和 FormView 內執行這些功能，請回到編輯、插入及刪除資料教學課程，從[插入、更新和刪除的總覽](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)開始。

## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>步驟1：指定`INSERT`、`UPDATE`和`DELETE`語句

如我們在過去兩個教學課程中所見，若要從 SqlDataSource 控制項中取出資料，我們必須設定兩個屬性：

1. `ConnectionString`，指定要將查詢傳送至哪個資料庫，而
2. `SelectCommand`，指定要執行以傳回結果的臨機操作 SQL 語句或預存程式名稱。

針對具有參數的 `SelectCommand` 值，參數值是透過 SqlDataSource s `SelectParameters` 集合指定，而且可以包含硬式編碼值、一般參數來源值（querystring 欄位、會話變數、Web 控制項值等等），或可以透過程式設計方式指派。 以程式設計方式或從資料 Web 控制項自動叫用 SqlDataSource 控制項 `Select()` 方法時，會建立與資料庫的連接，參數值會指派給查詢，而命令則會 shuttled 到資料庫。 然後，結果會以資料集或 DataReader 的形式傳回，視控制項的 `DataSourceMode` 屬性值而定。

除了選取資料，SqlDataSource 控制項也可以藉由以非常相同的方式提供 `INSERT`、`UPDATE`和 `DELETE` SQL 語句，來插入、更新和刪除資料。 只需將 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性指派給要執行的 `INSERT`、`UPDATE`和 `DELETE` SQL 語句。 如果語句具有參數（最常一律為），請將它們包含在 `InsertParameters`、`UpdateParameters`和 `DeleteParameters` 集合中。

一旦指定了 `InsertCommand`、`UpdateCommand`或 `DeleteCommand` 值，對應的資料 Web 控制項 s 智慧標籤中的 [啟用插入]、[啟用編輯] 或 [啟用刪除] 選項就會變成可用。 為了說明這一點，讓我們從[使用 SqlDataSource 控制項來查詢資料](querying-data-with-the-sqldatasource-control-vb.md)教學課程中所建立的 `Querying.aspx` 頁面進行範例，並將其擴大以包含刪除功能。

首先，從 [`SqlDataSource`] 資料夾開啟 [`InsertUpdateDelete.aspx`] 和 [`Querying.aspx`] 頁面。 從 [`Querying.aspx`] 頁面上的 [設計工具] 中，選取第一個範例中的 SqlDataSource 和 GridView （[`ProductsDataSource`] 和 [`GridView1`] 控制項）。 選取這兩個控制項之後，請移至 [編輯] 功能表，然後選擇 [複製] （或直接按 Ctrl + C）。 接下來，移至 `InsertUpdateDelete.aspx` 的設計工具，並貼到控制項中。 將兩個控制項移至 `InsertUpdateDelete.aspx`之後，請在瀏覽器中測試頁面。 您應該會看到 `Products` 資料庫資料表中所有記錄的 `ProductID`、`ProductName`和 `UnitPrice` 資料行的值。

[![列出所有產品，依 ProductID 排序](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.png)

**圖 1**：列出所有產品，並依 `ProductID` 排序（[按一下以觀看完整大小的影像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.png)）

## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>加入 SqlDataSource s`DeleteCommand`和`DeleteParameters`屬性

此時，我們有一個 SqlDataSource，只會傳回 `Products` 資料表中的所有記錄，以及呈現此資料的 GridView。 我們的目標是要擴充此範例，讓使用者可以透過 GridView 刪除產品。 若要完成此動作，我們必須指定 SqlDataSource 控制項的值 `DeleteCommand` 並 `DeleteParameters` 屬性，然後設定 GridView 以支援刪除。

`DeleteCommand` 和 `DeleteParameters` 屬性可以透過數種方式來指定：

- 透過宣告式語法
- 從設計工具中的屬性視窗
- 從 [設定資料來源] 中的 [指定自訂 SQL 語句或預存程式] 畫面
- 透過 [設定資料來源] wizard 中 [從資料表中指定資料行] 畫面的 [Advanced] 按鈕，這會實際自動產生 `DeleteCommand` 和 `DeleteParameters` 屬性中所使用的 `DELETE` SQL 語句和參數集合

我們將檢查如何自動在步驟2中建立 `DELETE` 語句。 現在，讓我們在設計工具中使用屬性視窗，雖然 [設定資料來源] 或 [宣告式語法] 選項也可以運作。

從 `InsertUpdateDelete.aspx`的設計工具中，按一下 [`ProductsDataSource`] SqlDataSource，然後啟動屬性視窗（從 [View] 功能表，選擇 [屬性視窗]，或直接按 F4）。 選取 [DeleteQuery] 屬性，這會顯示一組省略號。

![從 [屬性] 視窗中選取 [DeleteQuery] 屬性](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.gif)

**圖 2**：從 [屬性] 視窗中選取 [DeleteQuery] 屬性

> [!NOTE]
> SqlDataSource 沒有 DeleteQuery 屬性。 相反地，DeleteQuery 是 `DeleteCommand` 和 `DeleteParameters` 屬性的組合，而且只會在透過設計工具查看視窗時的屬性視窗中列出。 如果您要查看 [來源] 視圖中的屬性視窗，您會改為找到 [`DeleteCommand`] 屬性。

按一下 [DeleteQuery] 屬性中的省略號，以顯示 [命令和參數編輯器] 對話方塊（請參閱 [圖 3]）。 在此對話方塊中，您可以指定 `DELETE` SQL 語句，並指定參數。 在 [`DELETE` 命令] 文字方塊中輸入下列查詢（手動或使用 [查詢產生器] （如果您想要的話）：

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample1.sql)]

接下來，按一下 [重新整理參數] 按鈕，將 `@ProductID` 參數新增至下方的參數清單。

[![從 [屬性] 視窗中選取 [DeleteQuery] 屬性](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.png)

**圖 3**：從 [屬性] 視窗中選取 [DeleteQuery] 屬性（[按一下以查看完整大小的影像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.png)）

請勿*提供此*參數的值（將其參數來源保留為 None）。 當我們將刪除支援新增至 GridView 之後，GridView 會自動提供這個參數值，並使用其 `DataKeys` 集合的值，針對按下 [刪除] 按鈕的資料列。

> [!NOTE]
> `DELETE` 查詢中使用的參數名稱*必須*與 GridView、DetailsView 或 FormView 中 `DataKeyNames` 值的名稱相同。 也就是說，`DELETE` 語句中的參數會特意命名為 `@ProductID` （而不是 `@ID`），因為 Products 資料表中的主鍵資料行名稱（因此 GridView 中的 DataKeyNames 值）是 `ProductID`的。

如果參數名稱和 `DataKeyNames` 值不相符，GridView 就無法從 `DataKeys` 集合自動指派值給參數。

在 [命令和參數編輯器] 對話方塊中輸入與刪除相關的資訊後，按一下 [確定] 並移至來源視圖，以檢查產生的宣告式標記：

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample2.aspx)]

請注意，新增 `DeleteCommand` 屬性以及 `<DeleteParameters>` 區段和名為 `productID`的參數物件。

## <a name="configuring-the-gridview-for-deleting"></a>設定 GridView 以進行刪除

加入 `DeleteCommand` 屬性後，GridView 的智慧標籤現在會包含 [啟用刪除] 選項。 請繼續並核取此核取方塊。 如有關[插入、更新和刪除的簡介](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)中所述，這會導致 GridView 新增 CommandField，並將其 `ShowDeleteButton` 屬性設為 `True`。 如 [圖 4] 所示，當頁面透過瀏覽器造訪時，會包含 [刪除] 按鈕。 藉由刪除某些產品來測試此頁面。

[![每個 GridView 資料列現在包含 [刪除] 按鈕](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.png)

**圖 4**：每個 GridView 資料列現在都包含 [刪除] 按鈕（[按一下以查看完整大小的影像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.png)）

當按一下 [刪除] 按鈕時，就會發生回傳，GridView 會針對已按下 [刪除] 按鈕的資料列，將 `DataKeys` 集合值的值指派給 `ProductID` 參數，然後叫用 SqlDataSource s `Delete()` 方法。 然後，SqlDataSource 控制項會連接到資料庫，並執行 `DELETE` 語句。 然後 GridView 會重新系結至 SqlDataSource，並傳回並顯示目前的一組產品（不再包含剛刪除的記錄）。

> [!NOTE]
> 由於 GridView 會使用其 `DataKeys` 集合來填入 SqlDataSource 參數，因此 GridView 的 `DataKeyNames` 屬性必須設定為構成主鍵的資料行，而且 SqlDataSource s `SelectCommand` 會傳回這些資料行。 此外，SqlDataSource s `DeleteCommand` 中的參數名稱必須設定為 `@ProductID`。 如果未設定 `DataKeyNames` 屬性，或參數未命名 `@ProductsID`，按一下 [刪除] 按鈕將會導致回傳，但不會實際刪除任何記錄。

[圖 5] 以圖形方式描繪此互動。 請回到[檢查與插入、更新和刪除教學課程相關聯的事件](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)，以取得與從資料 Web 控制項插入、更新和刪除相關聯之事件鏈的詳細討論。

![按一下 GridView 中的 [刪除] 按鈕會叫用 SqlDataSource s Delete （）方法](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.gif)

**圖 5**：按一下 GridView 中的 [刪除] 按鈕會叫用 SqlDataSource s `Delete()` 方法

## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>步驟2：自動產生`INSERT`、`UPDATE`和`DELETE`語句

在步驟1檢查之後，您可以透過屬性視窗或控制項的宣告式語法來指定 `INSERT`、`UPDATE`和 `DELETE` SQL 語句。 不過，這種方法需要手動寫出 SQL 語句，這可能會單調且容易出錯。 幸好 [設定資料來源] 會提供一個選項，讓您在使用 [從資料表中指定資料行] 畫面時，自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句。

讓我們探索這項自動產生選項。 在 `InsertUpdateDelete.aspx` 中，將 DetailsView 新增至設計工具，並將其 [`ID`] 屬性設定為 [`ManageProducts`]。 接下來，從 DetailsView 的智慧標籤中，選擇建立新的資料來源，並建立名為 `ManageProductsDataSource`的 SqlDataSource。

[![建立名為 ManageProductsDataSource 的新 SqlDataSource](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.png)

**圖 6**：建立名為 `ManageProductsDataSource` 的新 SqlDataSource （[按一下以查看完整大小的影像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.png)）

在 [設定資料來源] 中，選擇使用 `NORTHWINDConnectionString` 連接字串，然後按 [下一步]。 從 [設定 Select 語句] 畫面中，保留選取 [從資料表或視圖指定資料行] 選項按鈕，然後從下拉式清單中挑選 [`Products`] 資料表。 從 [checkbox] 清單中選取 [`ProductID`]、[`ProductName`]、[`UnitPrice`] 和 [`Discontinued`] 資料行。

[![使用 Products 資料表，傳回 ProductID、ProductName、單價和已停止的資料行](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.png)

**圖 7**：使用 `Products` 資料表，傳回 `ProductID`、`ProductName`、`UnitPrice`和 `Discontinued` 資料行（[按一下以查看完整大小的影像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image10.png)）

若要根據選取的資料表和資料行自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句，請按一下 [Advanced] 按鈕，然後勾選 [產生 `INSERT`、`UPDATE`和 `DELETE` 語句] 核取方塊。

![勾選 [產生 INSERT、UPDATE 和 DELETE 子句] 核取方塊](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.gif)

**圖 8**：選取 [產生 `INSERT`、`UPDATE`和 `DELETE` 語句] 核取方塊

只有當選取的資料表具有主鍵，而且主鍵資料行（或資料行）包含在傳回的資料行清單中時，才會 checkable [產生 `INSERT`]、[`UPDATE`] 和 [`DELETE` 語句] 核取方塊。 [使用開放式平行存取] 核取方塊，可在 [產生 `INSERT`]、[`UPDATE`] 和 [`DELETE` 語句] 核取方塊已核取後變成可選取，將會在產生的 `UPDATE` 和 `DELETE` 語句中增加 `WHERE` 子句，以提供開放式並行存取控制。 目前請不要勾選此核取方塊;我們將在下一個教學課程中使用 SqlDataSource 控制項來檢查開放式平行存取。

核取 [產生 `INSERT`]、[`UPDATE`] 和 [`DELETE` 語句] 核取方塊後，按一下 [確定] 返回 [設定 Select 語句] 畫面，然後按 [下一步]，再按一下 [完成]，完成 [設定資料來源嚮導]。 完成此嚮導之後，Visual Studio 會將 BoundFields 加入 `ProductID`、`ProductName`和 `UnitPrice` 資料行的 DetailsView，以及 `Discontinued` 資料行的 CheckBoxField。 從 DetailsView s 智慧標籤，核取 [啟用分頁] 選項，讓流覽此頁面的使用者可以逐步執行產品。 同時清除 DetailsView 的 `Width` 並 `Height` 屬性。

請注意，智慧標籤具有 [啟用插入]、[啟用編輯] 和 [啟用刪除] 選項。 這是因為 SqlDataSource 包含其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand`的值，如下列宣告式語法所示：

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample3.aspx)]

請注意，SqlDataSource 控制項如何自動設定其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性的值。 `InsertCommand` 和 `UpdateCommand` 屬性中所參考的資料行集合是以 `SELECT` 語句中的資料行為基礎。 也就是說，不會讓 `InsertCommand` 和 `UpdateCommand`中的*每個*產品資料行，只會在 `SelectCommand` 中指定那些資料行 `ProductID`（因為它是[`IDENTITY` 資料行](http://www.sqlteam.com/item.asp?ItemID=102)，因此會省略，因為在編輯時，其值不會變更，而在插入時則會自動指派）。 此外，在 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性中的每個參數，`InsertParameters`、`UpdateParameters`和 `DeleteParameters` 集合中都有對應的參數。

若要開啟 DetailsView 的資料修改功能，請核取其智慧標籤中的 [啟用插入]、[啟用編輯] 和 [啟用刪除] 選項。 這會加入 CommandField，並將其 `ShowInsertButton`、`ShowEditButton`和 `ShowDeleteButton` 屬性設定為 `True`。

造訪瀏覽器中的頁面，並記下 DetailsView 中包含的 [編輯]、[刪除] 和 [新增] 按鈕。 按一下 [編輯] 按鈕會將 DetailsView 變成編輯模式，這會顯示 `ReadOnly` 屬性設為 [`False`] （預設值）做為文字方塊的每個 BoundField，以及 [CheckBoxField] 做為核取方塊。

[![DetailsView 的預設編輯介面](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image11.png)

**圖 9**： DetailsView s 預設編輯介面（[按一下以觀看完整大小的影像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image12.png)）

同樣地，您可以刪除目前選取的產品或將新產品加入系統。 由於 `InsertCommand` 語句僅適用于 `ProductName`、`UnitPrice`和 `Discontinued` 資料行，因此在插入時，其他資料行都有 `NULL` 或其預設值。 就像 ObjectDataSource，如果 `InsertCommand` 缺少任何不允許 `NULL` s 的資料庫資料表資料行，而且沒有預設值，則嘗試執行 `INSERT` 語句時，將會發生 SQL 錯誤。

> [!NOTE]
> DetailsView 的插入和編輯介面沒有任何自訂或驗證類型。 若要加入驗證控制項或自訂介面，您必須將 BoundFields 轉換為 TemplateFields。 如需詳細資訊，請參閱將[驗證控制項新增至編輯和插入介面](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)和[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教學課程。

此外，請記住，在更新和刪除的情況下，DetailsView 會使用目前的產品 `DataKey` 值，只有在設定 `DataKeyNames` 屬性時才會出現。 如果 [編輯] 或 [刪除] 似乎沒有作用，請確定已設定 [`DataKeyNames`] 屬性。

## <a name="limitations-of-automatically-generating-sql-statements"></a>自動產生 SQL 語句的限制

由於只有從資料表挑選資料行時，才可以使用 [產生 `INSERT`、`UPDATE`和 `DELETE` 語句] 選項，針對更複雜的查詢，您必須撰寫自己的 `INSERT`、`UPDATE`和 `DELETE` 語句，就像我們在步驟1中所做的一樣。 SQL `SELECT` 語句通常會使用 `JOIN`，從一個或多個查閱資料表中傳回資料以供顯示之用（例如，在顯示產品資訊時，將 [`Categories` 表] `CategoryName` 欄位傳回）。 同時，我們可能會想要允許使用者編輯、更新或插入資料到核心資料表（在此案例中`Products`）。

雖然可以手動輸入 `INSERT`、`UPDATE`和 `DELETE` 語句，但請考慮下列時間儲存提示。 一開始會設定 SqlDataSource，使其只從 `Products` 資料表中提取資料。 使用 [設定資料來源嚮導]，從資料表或視圖畫面指定資料行，讓您可以自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句。 然後，在完成 wizard 之後，選擇從屬性視窗設定 SelectQuery （或者，也可以返回 [設定資料來源]，但使用 [指定自訂 SQL 語句或預存程式] 選項）。 然後更新 `SELECT` 語句，以包含 `JOIN` 語法。 這項技術可為自動產生的 SQL 語句提供省時的優點，並允許更自訂的 `SELECT` 語句。

自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句的另一項限制是，`INSERT` 和 `UPDATE` 語句中的資料行是根據 `SELECT` 語句所傳回的資料行。 不過，我們可能需要更新或插入更多或更少的欄位。 例如，在步驟2的範例中，我們可能想要讓 `UnitPrice` BoundField 為唯讀。 在這種情況下，它應該不會出現在 `UpdateCommand`中。 或者，我們可能想要設定不會出現在 GridView 中的資料表欄位值。 例如，當加入新記錄時，我們可能會想要 `QuantityPerUnit` 值設定為 TODO。

如果需要這類自訂專案，您必須透過 [屬性視窗]、[在嚮導中指定自訂 SQL 語句或預存程式] 或宣告式語法來手動進行。

> [!NOTE]
> 在資料 Web 控制項中加入沒有對應欄位的參數時，請記住，必須以某種方式將值指派給這些參數值。 這些值可以是：直接在 `InsertCommand` 或 `UpdateCommand`中進行硬式編碼;可以來自某些預先定義的來源（querystring、會話狀態、頁面上的 Web 控制項等等）;您也可以透過程式設計方式指派或，如先前的教學課程中所見。

## <a name="summary"></a>總結

為了讓資料 Web 控制項利用內建的插入、編輯和刪除功能，其系結的資料來源控制項必須提供這類功能。 針對 SqlDataSource，這表示 `INSERT`、`UPDATE`和 `DELETE` SQL 語句必須指派給 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性。 這些屬性和對應的參數集合可以手動新增，或透過 [設定資料來源] 嚮導自動產生。 在本教學課程中，我們探討了這兩種技術。

我們已在[執行開放式並行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)存取教學課程中，使用開放式平行存取與 ObjectDataSource 進行檢查。 SqlDataSource 控制項也提供開放式平行存取支援。 如步驟2所述，當自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句時，此 wizard 會提供使用開放式平行存取選項。 如我們在下一個教學課程中所見，使用開放式平行存取與 SqlDataSource 會修改 `UPDATE` 和 `DELETE` 語句中的 `WHERE` 子句，以確保自資料最後一次顯示在頁面上之後，其他資料行的值還沒有變更。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](using-parameterized-queries-with-the-sqldatasource-vb.md)
> [下一頁](implementing-optimistic-concurrency-with-the-sqldatasource-vb.md)
