---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
title: 使用參數化查詢搭配 SqlDataSource （C#） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們會繼續查看 SqlDataSource 控制項，並瞭解如何定義參數化查詢。 參數可以同時指定宣告 。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9128aaac-afe2-449f-84b2-bb1d035083c4
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 241dc8c089d4faa9eb95a63684e8a56756bb302c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78552476"
---
# <a name="using-parameterized-queries-with-the-sqldatasource-c"></a>使用以 SqlDataSource 進行的參數化查詢 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_CS.exe)或[下載 PDF](using-parameterized-queries-with-the-sqldatasource-cs/_static/datatutorial48cs1.pdf)

> 在本教學課程中，我們會繼續查看 SqlDataSource 控制項，並瞭解如何定義參數化查詢。 參數可以用宣告方式和程式設計方式指定，而且可以從數個位置提取，例如 querystring、會話狀態、其他控制項等等。

## <a name="introduction"></a>簡介

在上一個教學課程中，我們已瞭解如何使用 SqlDataSource 控制項直接從資料庫取出資料。 使用 [設定資料來源] 嚮導，我們可以選擇資料庫，然後選取要從資料表或視圖傳回的資料行。輸入自訂 SQL 語句;或使用預存程式。 不論是從資料表或視圖中選取資料行，還是要輸入自訂的 SQL 語句，SqlDataSource 控制項 s `SelectCommand` 屬性都會指派產生的臨機操作 SQL `SELECT` 語句，而這是在叫用 SqlDataSource s `Select()` 方法（以程式設計方式或自動從資料 Web 控制項）時執行的這個 `SELECT` 語句。

先前的教學課程中所使用的 SQL `SELECT` 語句缺少 `WHERE` 的子句。 在 `SELECT` 語句中，可以使用 `WHERE` 子句來限制傳回的結果。 例如，若要顯示產品名稱超過 $50.00 的成本，我們可以使用下列查詢：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample1.sql)]

一般來說，`WHERE` 子句中使用的值會由某些外部來源決定，例如 querystring 值、會話變數，或網頁上 Web 控制項的使用者輸入。 在理想的情況下，這類輸入是透過使用*參數*來指定。 使用 Microsoft SQL Server，參數會使用 `@parameterName`表示，如下所示：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample2.sql)]

SqlDataSource 支援參數化查詢，適用于 `SELECT` 語句和 `INSERT`、`UPDATE`和 `DELETE` 語句。 此外，您可以從各種來源自動提取參數值： querystring、會話狀態、頁面上的控制項等等，或可透過程式設計方式指派。 在本教學課程中，我們將瞭解如何定義參數化查詢，以及如何以宣告方式和程式設計方式來指定參數值。

> [!NOTE]
> 在上一個教學課程中，我們比較了使用 SqlDataSource 前46教學課程所選擇的 ObjectDataSource，並注意其概念相似之處。 這些相似性也會延伸至參數。 對應至商務邏輯層中方法之輸入參數的 ObjectDataSource s 參數。 使用 SqlDataSource 時，參數會直接定義在 SQL 查詢中。 這兩個控制項都有其 `Select()`、`Insert()`、`Update()`和 `Delete()` 方法的參數集合，而且兩者都可以從預先定義的來源（querystring 值、會話變數等等）填入這些參數值，或以程式設計方式指派。

## <a name="creating-a-parameterized-query"></a>建立參數型查詢

SqlDataSource 控制項的 [設定資料來源] 會提供三個途徑來定義要執行以抓取資料庫記錄的命令：

- 藉由從現有的資料表或視圖中挑選資料行，
- 輸入自訂 SQL 語句，或
- 選擇預存程式

從現有的資料表或視圖挑選資料行時，必須透過 [加入 `WHERE` 子句] 對話方塊來指定 `WHERE` 子句的參數。 不過，在建立自訂 SQL 語句時，您可以直接在 `WHERE` 子句中輸入參數（使用 `@parameterName` 來表示每個參數）。 [預存](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)程式是由一或多個 SQL 語句所組成，而且這些語句可以參數化。 不過，在 SQL 語句中使用的參數必須當做預存程式的輸入參數來傳遞。

由於建立參數化查詢的方式取決於如何指定 SqlDataSource s `SelectCommand`，讓我們來看一下這三種方法。 若要開始使用，請開啟 [`SqlDataSource`] 資料夾中的 [`ParameterizedQueries.aspx`] 頁面，將 [SqlDataSource] 控制項從 [工具箱] 拖曳至設計工具，並將其 `ID` 設定為 [`Products25BucksAndUnderDataSource`]。 接下來，按一下控制項 s 智慧標籤中的 [設定資料來源] 連結。 選取要使用的資料庫（`NORTHWINDConnectionString`），然後按 [下一步]。

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>步驟1：從資料表或視圖挑選資料行時，加入`WHERE`子句

當您使用 SqlDataSource 控制項選取要從資料庫傳回的資料時，[設定資料來源] 會讓我們直接挑選要從現有的資料表或視圖傳回的資料行（請參閱 [圖 1]）。 這麼做會自動建立 SQL `SELECT` 語句，這就是叫用 SqlDataSource s `Select()` 方法時，會傳送至資料庫的內容。 如同我們在上一個教學課程中所做的一樣，請從下拉式清單中選取 [Products] 資料表，然後檢查 [`ProductID`]、[`ProductName`] 和 [`UnitPrice`] 資料行。

[![挑選要從資料表或視圖傳回的資料行](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.png)

**圖 1**：挑選要從資料表或視圖傳回的資料行（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.png)）

若要在 `SELECT` 的語句中包含 `WHERE` 子句，請按一下 [`WHERE`] 按鈕，這會顯示 [新增 `WHERE` 子句] 對話方塊（請參閱 [圖 2]）。 若要加入參數來限制 `SELECT` 查詢所傳回的結果，請先選擇要用來篩選資料的資料行。 接下來，選擇要用於篩選的運算子（=、&lt;、&lt;=、&gt;等等）。 最後，選擇參數 s 值的來源，例如從 querystring 或會話狀態。 設定參數之後，請按一下 [新增] 按鈕，將它包含在 `SELECT` 查詢中。

在此範例中，讓只傳回 `UnitPrice` 值小於或等於 $25.00 的結果。 因此，請從 資料行 下拉式清單中挑選 `UnitPrice`，然後從 運算子 下拉式清單中 &lt;=。 使用硬式編碼的參數值（例如 $25.00），或如果參數值是以程式設計方式指定，請從 [來源] 下拉式清單中選取 [無]。 接下來，在 [值] 25.00 文字方塊中輸入硬式編碼的參數值，然後按一下 [新增] 按鈕來完成程式。

[![限制從 [加入 WHERE 子句] 對話方塊傳回的結果](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.png)

**圖 2**：限制從 [加入 `WHERE` 子句] 對話方塊傳回的結果（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.png)）

加入參數之後，按一下 [確定] 以返回 [設定資料來源]。 位於 wizard 底部的 `SELECT` 語句現在應該包含具有名為 `@UnitPrice`之參數的 `WHERE` 子句：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample3.sql)]

> [!NOTE]
> 如果您從 [加入 `WHERE` 子句] 對話方塊的 [`WHERE`] 子句中指定多個條件，則 wizard 會使用 `AND` 運算子來加入它們。 如果您需要在 `WHERE` 子句（例如 `WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`）中包含 `OR`，則必須透過 [自訂 SQL 語句] 畫面建立 `SELECT` 語句。

完成 SqlDataSource 的設定（按 [下一步]，然後按一下 [完成]），然後檢查 SqlDataSource 的宣告式標記。 標記現在包含一個 `<SelectParameters>` 集合，它會將 `SelectCommand`中的參數的來源拼寫出來。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample4.aspx)]

叫用 SqlDataSource s `Select()` 方法時，`UnitPrice` 參數值（25.00）會在傳送至資料庫之前，套用至 `SelectCommand` 中的 `@UnitPrice` 參數。 最終結果是，只有小於或等於 $25.00 的產品會從 `Products` 資料表傳回。 若要確認這一點，請將 GridView 新增至頁面，並將它系結到此資料來源，然後透過瀏覽器來查看頁面。 您應該只會看到列出的產品小於或等於 $25.00，如 [圖 3] 所示。

[只會顯示小於或等於 $25.00 的產品 ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.png)

**圖 3**：只顯示小於或等於 $25.00 的產品（[按一下以觀看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.png)）

## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>步驟2：將參數加入至自訂 SQL 語句

加入自訂 SQL 語句時，您可以明確地輸入 `WHERE` 子句，或在 [查詢產生器] 的 [篩選] 儲存格中指定值。 為了示範這一點，讓我們只在 GridView 中顯示其價格小於特定閾值的產品。 一開始先將 TextBox 新增至 [`ParameterizedQueries.aspx`] 頁面，以收集使用者的此臨界值。 將 TextBox 的 `ID` 屬性設定為 `MaxPrice`。 新增按鈕 Web 控制項，並設定其 [`Text`] 屬性，以顯示相符的產品。

接下來，將 GridView 拖曳至頁面上，並從其智慧標籤選擇建立名為 `ProductsFilteredByPriceDataSource`的新 SqlDataSource。 從 [設定資料來源] wizard，繼續進行 [指定自訂 SQL 語句或預存程式] 畫面（請參閱 [圖 4]），然後輸入下列查詢：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample5.sql)]

進入查詢（手動或透過查詢產生器）之後，按 [下一步]。

[![只傳回小於或等於參數值的產品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.png)

**圖 4**：只傳回小於或等於參數值的產品（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.png)）

因為查詢包含參數，所以嚮導中的下一個畫面會提示我們輸入參數值的來源。 從 [參數來源] 下拉式清單中選擇 [控制項]，然後從 [ControlID] 下拉式清單中 `MaxPrice` （TextBox 控制項 s `ID` 值）。 如果使用者未在 [`MaxPrice`] 文字方塊中輸入任何文字，您也可以輸入選擇性的預設值來使用。 就時間而言，請勿輸入預設值。

[![MaxPrice TextBox s Text 屬性會當做參數來源使用](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.png)

**圖 5**： `MaxPrice` TextBox s `Text` 屬性是用來做為參數來源（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.png)）

按 [下一步]，然後按一下 [完成]，完成 [設定資料來源]。 [GridView]、[TextBox]、[Button] 和 [SqlDataSource] 的宣告式標記如下所示：

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample6.aspx)]

請注意，SqlDataSource s `<SelectParameters>` 區段中的參數是 `ControlParameter`，其中包括 `ControlID` 和 `PropertyName`等其他屬性。 叫用 SqlDataSource s `Select()` 方法時，`ControlParameter` 會從指定的 Web 控制項屬性抓取值，並將它指派給 `SelectCommand`中的對應參數。 在此範例中，`MaxPrice` s Text 屬性會用來做為 `@MaxPrice` 參數值。

請花幾分鐘的時間透過瀏覽器觀看此頁面。 第一次造訪網頁時，或每當 `MaxPrice` 文字方塊缺少值時，GridView 中不會顯示任何記錄。

[當 [MaxPrice] 文字方塊為空白時，不會顯示任何記錄 ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.png)

**圖 6**：當 [`MaxPrice`] 文字方塊為空白時，不會顯示任何記錄（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.png)）

未顯示任何產品的原因是因為根據預設，參數值的空字串會轉換成資料庫 `NULL` 值。 由於 `[UnitPrice] <= NULL` 的比較一律會評估為 False，因此不會傳回任何結果。

在文字方塊中輸入一個值，例如5.00，然後按一下 [顯示相符的產品] 按鈕。 在回傳時，SqlDataSource 會通知 GridView 其中一個參數來源已變更。 因此，GridView 會重新系結至 SqlDataSource，顯示那些產品小於或等於 $5.00。

[顯示小於或等於 $5.00 的 ![產品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.png)

**圖 7**：顯示小於或等於 $5.00 的產品（[按一下以觀看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.png)）

## <a name="initially-displaying-all-products"></a>一開始顯示所有產品

我們可能會想要顯示*所有*產品，而不是在第一次載入頁面時顯示任何產品。 每當 [`MaxPrice`] 文字方塊為空白時，其中一種列出所有產品的方法是將參數的預設值設定為某個瘋狂高值（例如1000000），因為 Northwind 商貿不太可能會擁有單價超過 $1000000 的庫存。 不過，這種方法是 shortsighted 的，而且在其他情況下可能無法使用。

在先前的教學課程中-[宣告式參數](../basic-reporting/declarative-parameters-cs.md)和[使用 DropDownList 的主要/詳細資料篩選](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)時，會面臨類似的問題。 我們的解決方案是將此邏輯放在商務邏輯層中。 具體而言，BLL 檢查了傳入的值，如果 `NULL` 或某個保留值，則呼叫會路由傳送至傳回所有記錄的 DAL 方法。 如果傳入的值是一般篩選值，則會呼叫 DAL 方法，以執行 SQL 語句，並將參數化 `WHERE` 子句與提供的值搭配使用。

可惜的是，在使用 SqlDataSource 時，我們略過架構。 相反地，我們需要自訂 SQL 語句，以便在 `@MaximumPrice` 參數 `NULL` 或某些保留值時，以智慧方式抓取所有記錄。 在此練習中，讓我們將它設為，如果 `@MaximumPrice` 參數等於 `-1.0`，則會傳回*所有*的記錄（`-1.0` 作為保留值，因為沒有任何產品可以有負值的 `UnitPrice` 值）。 為了達成此目的，我們可以使用下列 SQL 語句：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample7.sql)]

如果 `@MaximumPrice` 參數等於 `-1.0`，這個 `WHERE` 子句會傳回*所有*記錄。 如果未 `-1.0`參數值，則只會傳回其 `UnitPrice` 小於或等於 `@MaximumPrice` 參數值的產品。 藉由將 `@MaximumPrice` 參數的預設值設定為 `-1.0`，在第一頁載入（或每當 [`MaxPrice`] 文字方塊是空的）時，`@MaximumPrice` 會有 `-1.0` 的值，而且會顯示所有產品。

[![現在當 [MaxPrice] 文字方塊為空白時，會顯示所有產品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.png)

**圖 8**：現在所有產品都是在 [`MaxPrice`] 文字方塊空白時顯示（[按一下以觀看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image16.png)）

這種方法有幾個值得注意的事項。 首先，請注意參數 s 資料類型是由 SQL 查詢中的它使用方式所推斷。 如果您將 `WHERE` 子句從 `@MaximumPrice = -1.0` 變更為 `@MaximumPrice = -1`，執行時間會將參數視為整數。 如果您接著嘗試將 [`MaxPrice`] 文字方塊指派為十進位值（例如5.00），就會發生錯誤，因為它無法將5.00 轉換成整數。 若要解決這個問題，請確定您在 `WHERE` 子句中使用 `@MaximumPrice = -1.0`，或者將 `ControlParameter` 物件 s `Type` 屬性設定為 Decimal。

其次，藉由將 `OR @MaximumPrice = -1.0` 新增至 `WHERE` 子句，查詢引擎就無法在 `UnitPrice` 上使用索引（假設有一個），因此會產生資料表掃描。 如果 `Products` 資料表中有足夠大量的記錄，這可能會影響效能。 較好的方法是將這個邏輯移至預存程式，其中 `IF` 語句會在需要傳回所有記錄時，不使用 `WHERE` 子句從 `Products` 資料表執行 `SELECT` 查詢，或其中一個 `WHERE` 子句只包含 `UnitPrice` 準則，如此就可以使用索引。

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>步驟3：建立和使用參數化預存程式

預存程式可以包含一組輸入參數，之後可以在預存程式內定義的 SQL 語句中使用。 設定 SqlDataSource 使用接受輸入參數的預存程式時，可以使用與臨機操作 SQL 語句相同的技術來指定這些參數值。

為了說明如何在 SqlDataSource 中使用預存程式，讓我們在 Northwind 資料庫中建立名為 `GetProductsByCategory`的新預存程式，它會接受名為 `@CategoryID` 的參數，並傳回其 `CategoryID` 資料行符合 `@CategoryID`之產品的所有資料行。 若要建立預存程式，請移至 伺服器總管並向下切入至 `NORTHWND.MDF` 資料庫。 （如果您沒有看到伺服器總管，請移至 [View] 功能表，然後選取 [伺服器總管] 選項）。

在 `NORTHWND.MDF` 資料庫中，以滑鼠右鍵按一下 [預存程式] 資料夾，選擇 [加入新的預存程式]，然後輸入下列語法：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample8.sql)]

按一下 [儲存] 圖示（或 Ctrl + S）以儲存預存程式。 您可以從 [預存程式] 資料夾以滑鼠右鍵按一下預存程式，然後選擇 [執行]，來進行測試。 這會提示您輸入預存程式的參數（在此例中為`@CategoryID`），之後結果就會顯示在 [輸出] 視窗中。

[以 @CategoryID 1 執行時，![GetProductsByCategory 預存程式](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image17.png)

**圖 9**：以 `@CategoryID` 1 執行時的 `GetProductsByCategory` 預存程式（[按一下以觀看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image18.png)）

讓我們使用這個預存程式，在 GridView 中顯示飲料類別目錄中的所有產品。 將新的 GridView 新增至頁面，並將它系結至名為 `BeverageProductsDataSource`的新 SqlDataSource。 繼續進行 [指定自訂 SQL 語句或預存程式] 畫面，選取 [預存程式] 選項按鈕，然後從下拉式清單中挑選 `GetProductsByCategory` 預存程式。

[![從下拉式清單中選取 GetProductsByCategory 預存程式](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image19.png)

**圖 10**：從下拉式清單中選取 [`GetProductsByCategory` 預存程式] （[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image20.png)）

由於預存程式會接受輸入參數（`@CategoryID`），因此按一下 [下一步] 會提示我們指定此參數值的來源。 飲料 `CategoryID` 為1，因此，請將 [參數來源] 下拉式清單保留為 [無]，然後在 [DefaultValue] 文字方塊中輸入1。

[![使用硬式編碼值1來傳回飲料類別目錄中的產品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image21.png)

**圖 11**：使用硬式編碼值1來傳回飲料類別目錄中的產品（[按一下以觀看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image22.png)）

如下列宣告式標記所示，當使用預存程式時，SqlDataSource s `SelectCommand` 屬性會設定為預存程式的名稱，而[`SelectCommandType` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx)會設定為 `StoredProcedure`，表示 `SelectCommand` 是預存程式的名稱，而不是特定 SQL 語句。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample9.aspx)]

在瀏覽器中測試頁面。 只會顯示屬於飲料類別目錄的產品，雖然*所有*的產品欄位都會顯示，但因為 `GetProductsByCategory` 預存程式會傳回 `Products` 資料表中的所有資料行。 當然，我們可以限制或自訂 GridView 的 [編輯資料行] 對話方塊中顯示的欄位。

[會顯示所有飲料 ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image23.png)

**圖 12**：顯示所有飲料（[按一下以觀看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image24.png)）

## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>步驟4：以程式設計方式叫用 SqlDataSource s`Select()`語句

我們在上一個教學課程中看到的範例和本教學課程目前已將 SqlDataSource 控制項直接系結至 GridView。 不過，您可以在程式碼中以程式設計方式存取和列舉 SqlDataSource 控制項的資料。 當您需要查詢資料以進行檢查，但不需要顯示它時，這會特別有用。 您不必撰寫所有的 ADO.NET 程式碼來連接到資料庫、指定命令和抓取結果，而是讓 SqlDataSource 處理這個單調程式碼。

為了說明如何以程式設計方式使用 SqlDataSource 的資料，假設您的老闆已要求您建立網頁，以顯示隨機選取的類別和其相關產品的名稱。 也就是說，當使用者造訪此頁面時，我們想要從 [`Categories`] 資料表隨機播放類別、顯示 [類別目錄名稱]，然後列出屬於該類別目錄的產品。

若要完成這項操作，我們需要兩個 SqlDataSource 控制項來抓取 `Categories` 資料表的隨機分類，另一個則用來取得類別目錄的產品。 我們將在此步驟中建立可抓取隨機分類記錄的 SqlDataSource;步驟5將探討如何製作可抓取類別目錄產品的 SqlDataSource。

首先，將 SqlDataSource 新增至 `ParameterizedQueries.aspx`，並將其 `ID` 設定為 [`RandomCategoryDataSource`]。 加以設定，使其使用下列 SQL 查詢：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample10.sql)]

`ORDER BY NEWID()` 會傳回以隨機順序排序的記錄（請參閱[使用 `NEWID()` 來隨機排序記錄](http://www.sqlteam.com/item.asp?ItemID=8747)）。 `SELECT TOP 1` 會從結果集傳回第一筆記錄。 這個查詢會放在一起，從單一隨機選取的類別傳回 `CategoryID` 和 `CategoryName` 的資料行值。

若要顯示 [類別] `CategoryName` 值，請將標籤 Web 控制項新增至頁面，將其 [`ID`] 屬性設定為 [`CategoryNameLabel`]，並清除其 [`Text`] 屬性。 若要以程式設計方式從 SqlDataSource 控制項取出資料，我們必須叫用其 `Select()` 方法。 [`Select()` 方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx)需要類型為[`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)的單一輸入參數，以指定資料在傳回之前應如何 messaged。 這可以包含排序和篩選資料的指示，而且資料 Web 控制項會在從 SqlDataSource 控制項的資料進行排序或分頁時使用。 但是在我們的範例中，我們不需要在傳回之前修改資料，因此會傳入 `DataSourceSelectArguments.Empty` 物件。

`Select()` 方法會傳回可執行 `IEnumerable`的物件。 傳回的精確類型取決於 SqlDataSource 控制項 s [`DataSourceMode` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)的值。 如先前教學課程中所討論，此屬性可以設定為 `DataSet` 或 `DataReader`的值。 如果設定為 `DataSet`，`Select()` 方法會傳回[DataView](https://msdn.microsoft.com/library/01s96x0z.aspx)物件;如果設定為 `DataReader`，它會傳回可執行[`IDataReader`](https://msdn.microsoft.com/library/system.data.idatareader.aspx)的物件。 因為 `RandomCategoryDataSource` SqlDataSource 的 `DataSourceMode` 屬性設定為 `DataSet` （預設值），所以我們會使用 DataView 物件。

下列程式碼說明如何從 `RandomCategoryDataSource` SqlDataSource 中取出記錄做為 DataView，以及如何從第一個 DataView 資料列讀取 `CategoryName` 資料行值：

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample11.cs)]

`randomCategoryView[0]` 會傳回 DataView 中的第一個 `DataRowView`。 `randomCategoryView[0]["CategoryName"]` 會傳回第一個資料列中 `CategoryName` 資料行的值。 請注意，DataView 是鬆散類型。 若要參考特定的資料行值，我們必須傳入資料行的名稱做為字串（在此案例中為類別名稱）。 [圖 13] 顯示在流覽頁面時，`CategoryNameLabel` 中顯示的訊息。 當然，每次造訪頁面（包括回傳）時，`RandomCategoryDataSource` SqlDataSource 會隨機選取顯示的實體類別名稱。

[![會顯示隨機選取的類別目錄名稱](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image25.png)

**圖 13**：顯示隨機選取的類別目錄名稱（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image26.png)）

> [!NOTE]
> 如果 SqlDataSource 控制項 s `DataSourceMode` 屬性已設為 `DataReader`，則 `Select()` 方法的傳回值必須轉換成 `IDataReader`。 若要讀取第一個資料列中的 `CategoryName` 資料行值，我們使用類似以下的程式碼：

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample12.cs)]

當 SqlDataSource 隨機選取類別時，我們已準備好加入會列出類別目錄產品的 GridView。

> [!NOTE]
> 我們可以將 FormView 或 DetailsView 新增至頁面，並將其系結至 SqlDataSource，而不是使用標籤 Web 控制項來顯示類別目錄名稱。 不過，使用標籤可讓我們探索如何以程式設計方式叫用 SqlDataSource s `Select()` 語句，並在程式碼中處理其產生的資料。

## <a name="step-5-assigning-parameter-values-programmatically"></a>步驟5：以程式設計方式指派參數值

到目前為止，我們在本教學課程中看到的所有範例，都使用硬式編碼參數值，或取自其中一個預先定義的參數來源（querystring 值、頁面上的 Web 控制項等等）。 不過，您也可以透過程式設計方式設定 SqlDataSource 控制 s 參數。 若要完成目前的範例，我們需要一個 SqlDataSource，以傳回屬於指定分類的所有產品。 這個 SqlDataSource 會有一個 `CategoryID` 參數，其值必須根據 `Page_Load` 事件處理常式中 `RandomCategoryDataSource` SqlDataSource 傳回的 `CategoryID` 資料行值來設定。

首先，將 GridView 新增至頁面，並將它系結至名為 `ProductsByCategoryDataSource`的新 SqlDataSource。 就像我們在步驟3中所做的一樣，設定 SqlDataSource，讓它叫用 `GetProductsByCategory` 預存程式。 將 [參數來源] 下拉式清單設定為 [無]，但不要輸入預設值，因為我們將以程式設計方式設定此預設值。

[![未指定參數來源或預設值](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image27.png)

**圖 14**：不要指定參數來源或預設值（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image28.png)）

完成 SqlDataSource wizard 之後，所產生的宣告式標記看起來應該如下所示：

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample13.aspx)]

我們可以在 `Page_Load` 事件處理常式中，以程式設計方式指派 `CategoryID` 參數的 `DefaultValue`：

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample14.cs)]

透過這種新增方式，頁面會包含 GridView，其中顯示與隨機選取的類別相關聯的產品。

[![未指定參數來源或預設值](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image29.png)

**圖 15**：不要指定參數來源或預設值（[按一下以查看完整大小的影像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image30.png)）

## <a name="summary"></a>總結

此 SqlDataSource 可讓網頁開發人員定義參數值可以硬式編碼、從預先定義的參數來源提取，或以程式設計方式指派的參數化查詢。 在本教學課程中，我們已瞭解如何針對臨機操作 SQL 查詢和預存程式，從 [設定資料來源] 建立參數化查詢。 我們也探討了如何使用硬式編碼的參數來源、Web 控制項做為參數來源，以及以程式設計方式指定參數值。

和 ObjectDataSource 一樣，SqlDataSource 也提供修改其基礎資料的功能。 在下一個教學課程中，我們將探討如何使用 SqlDataSource 來定義 `INSERT`、`UPDATE`和 `DELETE` 語句。 一旦新增這些語句之後，我們就可以利用內建的插入、編輯和刪除功能，並提供給 GridView、DetailsView 和 FormView 控制項。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Scott Clyde、Randell Schmidt 和 Ken Pespisa。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](querying-data-with-the-sqldatasource-control-cs.md)
> [下一頁](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
