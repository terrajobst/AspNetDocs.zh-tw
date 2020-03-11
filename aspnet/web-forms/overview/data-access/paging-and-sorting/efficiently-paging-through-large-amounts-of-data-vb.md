---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
title: 有效率地分頁大量資料（VB） |Microsoft Docs
author: rick-anderson
description: 當使用大量資料時，資料呈現控制項的預設分頁選項不適合，因為其基礎資料來源控制項 retriev 。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 3e20e64a-8808-4b49-88d6-014e2629d56f
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 0c788c4109d0d2839de969c628399290376a1ccd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78589940"
---
# <a name="efficiently-paging-through-large-amounts-of-data-vb"></a>有效率地分頁大量資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_VB.exe)或[下載 PDF](efficiently-paging-through-large-amounts-of-data-vb/_static/datatutorial25vb1.pdf)

> 當使用大量資料時，資料呈現控制項的預設分頁選項不適合，因為其基礎資料來源控制項會抓取所有記錄，即使只顯示資料的子集也一樣。 在這種情況下，我們必須轉換成自訂分頁。

## <a name="introduction"></a>簡介

如先前的教學課程中所討論，分頁可以透過下列兩種方式之一來執行：

- 只要檢查資料 Web 控制項的智慧標籤中的 [啟用分頁] 選項，就可以實作為**預設分頁**;不過，每當您查看資料頁時，ObjectDataSource 都會抓取*所有*記錄，即使頁面中只顯示其中的一部分也是一樣。
- **自訂分頁**藉由只從資料庫中取出需要針對使用者要求的特定資料頁面顯示的記錄，來改善預設分頁的效能;不過，自訂分頁牽涉到比預設分頁更多的執行工作

由於「輕鬆執行」的緣故，只要核取一個核取方塊就大功告成了！ 預設分頁是一個吸引人的選項。 不過，在抓取所有記錄的方法中，它會讓它成為 implausible 的選擇，以分頁處理足夠大量的資料或具有許多並行使用者的網站。 在這種情況下，我們必須轉換成自訂分頁，才能提供回應式系統。

自訂分頁的挑戰是能夠撰寫查詢，以傳回特定資料頁面所需的一組精確記錄。 幸運的是，Microsoft SQL Server 2005 提供了排名結果的新關鍵字，讓我們撰寫可有效率地抓取適當記錄子集的查詢。 在本教學課程中，我們將瞭解如何使用這個新的 SQL Server 2005 關鍵字，在 GridView 控制項中執行自訂分頁。 雖然自訂分頁的使用者介面與預設分頁相同，但使用自訂分頁從一頁逐步執行，可能會比預設分頁更快。

> [!NOTE]
> 自訂分頁所呈現的確切效能增益，取決於要逐頁查看的記錄總數，以及要放在資料庫伺服器上的負載。 在本教學課程結尾，我們將探討一些粗略的計量，展示透過自訂分頁取得的效能優勢。

## <a name="step-1-understanding-the-custom-paging-process"></a>步驟1：瞭解自訂分頁進程

分頁流覽資料時，在頁面中顯示的精確記錄取決於所要求的資料頁和每頁顯示的記錄數目。 例如，假設我們想要逐頁流覽81產品，每頁顯示10個產品。 在觀看第一頁時，我們會想要產品1到 10;在觀看第二頁時，我們 d 對產品11到20的興趣等等。

有三個變數會規定需要抓取哪些記錄，以及應該如何呈現分頁介面：

- **起始資料列索引**頁面中要顯示的第一個資料列的索引;此索引的計算方式是將頁面索引乘以記錄，以顯示每個頁面並加入一個。 例如，一次逐頁查看記錄10時，針對第一個頁面（其頁面索引為0），起始資料列索引為 0 \* 10 + 1 或1。針對第二個頁面（其頁面索引為1），起始資料列索引為 1 \* 10 + 1 或11。
- **最大資料列**每頁顯示的記錄數目上限。 此變數稱為最大資料列，因為在最後一頁中，傳回的記錄可能會比頁面大小少。 例如，當您逐頁查看每頁的81產品10筆記錄時，第九個和最後一頁只會有一筆記錄。 不過，沒有任何頁面會顯示比最大資料列值更多的記錄。
- **總記錄**數：要進行分頁的記錄總數。 雖然這個變數不需要用來決定要針對特定頁面抓取哪些記錄，但它的確會規定分頁介面。 例如，如果有81產品正在進行分頁，則分頁介面知道要在分頁 UI 中顯示九個頁碼。

使用預設分頁時，起始資料列索引會計算為頁面索引的乘積和頁面大小加一，而最大資料列只是頁面大小。 由於預設分頁會在轉譯任何頁面的資料時，從資料庫中抓取所有記錄，因此，每個資料列的索引都是已知的，因此，移至開始資料列索引資料列一項簡單的工作。 此外，記錄計數總計可以立即使用，因為它只是 DataTable 中的記錄數目（或使用任何物件來保存資料庫結果）。

假設 [起始資料列索引] 和 [最大資料列數] 變數，自訂分頁執行必須只傳回從起始資料列索引開始的精確記錄子集，以及之後的最大資料列數目。 自訂分頁提供兩個挑戰：

- 我們必須能夠有效率地將資料列索引與整頁分頁中的每個資料列產生關聯，讓我們可以在指定的起始列索引處開始傳回記錄。
- 我們需要提供要進行分頁的記錄總數

在接下來的兩個步驟中，我們將檢查回應這兩項挑戰所需的 SQL 腳本。 除了 SQL 腳本之外，我們還需要在 DAL 和 BLL 中執行方法。

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>步驟2：傳回已逐頁查看的記錄總數

在我們檢查如何取得所顯示頁面的精確記錄子集之前，讓我們先看一下如何傳回已進行分頁的記錄總數。 需要這項資訊，才能正確設定分頁使用者介面。 您可以使用[`COUNT` 彙總函式](https://msdn.microsoft.com/library/ms175997.aspx)來取得特定 SQL 查詢所傳回的記錄總數。 例如，若要判斷 `Products` 資料表中的記錄總數，我們可以使用下列查詢：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample1.sql)]

讓 s 將方法新增至會傳回此資訊的 DAL。 特別是，我們將建立名為 `TotalNumberOfProducts()` 的 DAL 方法，以執行上面顯示的 `SELECT` 語句。

首先，在 `App_Code/DAL` 資料夾中開啟 `Northwind.xsd` 類型資料集檔案。 接下來，以滑鼠右鍵按一下設計工具中的 `ProductsTableAdapter`，然後選擇 加入查詢。 如同在先前的教學課程中所見，這可讓我們將新的方法加入 DAL，叫用時，將會執行特定的 SQL 語句或預存程式。 如同先前教學課程中的 TableAdapter 方法，這一個選擇使用臨機操作 SQL 語句。

![使用特定 SQL 語句](efficiently-paging-through-large-amounts-of-data-vb/_static/image1.png)

**圖 1**：使用特定 SQL 語句

在下一個畫面中，我們可以指定要建立的查詢類型。 因為此查詢會傳回單一純量值，所以 `Products` 資料表中的記錄總數會選擇傳回單一值選項的 `SELECT`。

![將查詢設定為使用會傳回單一值的 SELECT 語句](efficiently-paging-through-large-amounts-of-data-vb/_static/image2.png)

**圖 2**：將查詢設定為使用會傳回單一值的 SELECT 語句

指出要使用之查詢的類型之後，我們必須接下來指定查詢。

![使用 SELECT COUNT （*） FROM Products 查詢](efficiently-paging-through-large-amounts-of-data-vb/_static/image3.png)

**圖 3**：使用 [產品] 查詢中的 [選取計數（\*）]

最後，指定方法的名稱。 如前所述，讓我們使用 `TotalNumberOfProducts`。

![將 DAL 方法命名為 TotalNumberOfProducts](efficiently-paging-through-large-amounts-of-data-vb/_static/image4.png)

**圖 4**：命名 DAL 方法 TotalNumberOfProducts

按一下 [完成] 之後，嚮導會將 `TotalNumberOfProducts` 方法新增至 DAL。 DAL 傳回的純量方法會傳回可為 null 的類型，以防 SQL 查詢的結果 `NULL`。 不過，我們的 `COUNT` 查詢一律會傳回非`NULL` 值;無論如何，DAL 方法會傳回可為 null 的整數。

除了 DAL 方法之外，我們也需要 BLL 中的方法。 開啟 `ProductsBLL` 類別檔案，並新增只向下呼叫 DAL s `TotalNumberOfProducts` 方法的 `TotalNumberOfProducts` 方法：

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample2.vb)]

DAL s `TotalNumberOfProducts` 方法會傳回可為 null 的整數;不過，我們已建立 `ProductsBLL` 類別的 `TotalNumberOfProducts` 方法，使其傳回標準整數。 因此，我們必須讓 `ProductsBLL` 類別的 `TotalNumberOfProducts` 方法傳回 DAL s `TotalNumberOfProducts` 方法所傳回之可為 null 整數的值部分。 `GetValueOrDefault()` 的呼叫會傳回可為 null 整數的值（如果有的話）。不過，如果 `null`可為 null 的整數，則會傳回預設的整數值0。

## <a name="step-3-returning-the-precise-subset-of-records"></a>步驟3：傳回記錄的精確子集

我們的下一個工作是在 DAL 和 BLL 中建立方法，以接受先前討論的開始資料列索引和最大資料列變數，並傳回適當的記錄。 在這麼做之前，先讓我們先看一下所需的 SQL 腳本。 我們的挑戰是，我們必須能夠有效率地將索引指派給整頁結果中的每個資料列，如此一來，我們就可以只傳回從開始資料列索引開始的記錄（以及最多記錄筆記錄數目）。

如果資料庫資料表中已經有資料行做為資料列索引，這不是一項挑戰。 乍看之下，我們可能會認為 `Products` 資料表的 `ProductID` 欄位就夠了，因為第一個產品的 `ProductID` 是1，第二個是2，依此類推。 不過，若要刪除產品，請取消之前這種方法。

有兩種一般技巧可用來有效率地將資料列索引與要逐頁處理的資料產生關聯，藉此讓您能夠取得精確的記錄子集：

- **使用 SQL Server 2005 s `ROW_NUMBER()` 關鍵字**new SQL Server 2005，`ROW_NUMBER()` 關鍵字會根據某種排序，將排名與每個傳回的記錄產生關聯。 這個次序可用來做為每個資料列的資料列索引。
- **使用資料表變數和 `SET ROWCOUNT`** SQL Server s [`SET ROWCOUNT` 語句](https://msdn.microsoft.com/library/ms188774.aspx)可用來指定查詢在終止前應處理的總記錄數;[資料表變數](http://www.sqlteam.com/item.asp?ItemID=9454)是可以保存表格式資料的本機 t-sql 變數，類似于[臨時表](http://www.sqlteam.com/item.asp?ItemID=2029)。 這種方法同樣適用于 Microsoft SQL Server 2005 和 SQL Server 2000 （而 `ROW_NUMBER()` 方法僅適用于 SQL Server 2005）。  
  
  這裡的概念是建立一個資料表變數，其中包含資料要進行分頁的資料表之主鍵的 `IDENTITY` 資料行和資料行。 接下來，要透過其資料分頁的資料表內容會傾印到資料表變數中，藉此將資料表中每一筆記錄的連續資料列索引（透過 `IDENTITY` 資料行）產生關聯。 一旦填入資料表變數之後，就可以執行資料表變數上與基礎資料表聯結的 `SELECT` 語句，以提取特定記錄。 `SET ROWCOUNT` 語句用來以智慧方式限制需要傾印到資料表變數中的記錄數目。  
  
  這種方式的效率是以所要求的頁碼為依據，因為 `SET ROWCOUNT` 值會指派開始資料列索引的值加上最大資料列數目。 透過低編號頁面（例如前幾頁的資料）進行分頁時，此方法非常有效率。 不過，它會在抓取接近結尾的頁面時，展現預設的類似分頁效能。

本教學課程會使用 `ROW_NUMBER()` 關鍵字來執行自訂分頁。 如需有關使用資料表變數和 `SET ROWCOUNT` 技術的詳細資訊，請參閱[更有效率的方法來分頁處理大型結果集](http://www.4guysfromrolla.com/webtech/042606-1.shtml)。

`ROW_NUMBER()` 關鍵字會使用下列語法，將排名與特定排序所傳回的每筆記錄相關聯：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample3.sql)]

`ROW_NUMBER()` 會傳回數值，指定每筆記錄對指定之順序的排名。 例如，若要查看每項產品的排名（從最昂貴到最低的順序），我們可以使用下列查詢：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample4.sql)]

[圖 5] 顯示在 Visual Studio 的查詢視窗中執行時的查詢結果。 請注意，產品依價格排序，以及每個資料列的價格等級。

![每個傳回的記錄都會包含價格等級](efficiently-paging-through-large-amounts-of-data-vb/_static/image5.png)

**圖 5**：為每個傳回的記錄包含價格等級

> [!NOTE]
> `ROW_NUMBER()` 只是 SQL Server 2005 中可用的許多新次序函數之一。 如需 `ROW_NUMBER()`的詳細討論以及其他次序函數，請參閱[使用 Microsoft SQL Server 2005 傳回排名結果](http://www.4guysfromrolla.com/webtech/010406-1.shtml)。

當根據 `OVER` 子句中指定的 `ORDER BY` 資料行來排序結果時（在上述範例中為`UnitPrice`），SQL Server 必須排序結果。 如果資料行上有叢集索引，而其結果是以排序，或如果有涵蓋索引，則這是快速作業，否則會更耗費成本。 若要協助改善足夠大型查詢的效能，請考慮為結果排序依據的資料行加入非叢集索引。 如需效能考慮的詳細資訊，請參閱[SQL Server 2005 中的次序函數和效能](http://www.sql-server-performance.com/ak_ranking_functions.asp)。

`ROW_NUMBER()` 傳回的排名資訊不能直接用在 `WHERE` 子句中。 不過，您可以使用衍生資料表來傳回 `ROW_NUMBER()` 的結果，然後它會出現在 `WHERE` 子句中。 例如，下列查詢會使用衍生資料表來傳回 ProductName 和單價資料行，以及 `ROW_NUMBER()` 結果，然後使用 `WHERE` 子句，只傳回價格等級介於11到20之間的產品：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample5.sql)]

進一步擴充這個概念，我們可以利用這種方法，根據所需的開始資料列索引和最大資料列值來抓取特定頁面的資料：

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample6.html)]

> [!NOTE]
> 如我們稍後在本教學課程中所見，ObjectDataSource 所提供的 *`StartRowIndex`* 是從零開始編制索引，而 SQL Server 2005 傳回的 `ROW_NUMBER()` 值則是從1開始編制索引。 因此，`WHERE` 子句會傳回 `PriceRank` 嚴格大於 *`StartRowIndex`* 且小於或等於 *`StartRowIndex`*  +  *`MaximumRows`* 的記錄。

現在，我們已討論過如何使用 `ROW_NUMBER()` 來取得給定的起始資料列索引和最大資料列值的特定頁面，我們現在需要將此邏輯實作為 DAL 和 BLL 中的方法。

建立此查詢時，我們必須決定要將結果排序依據的順序;讓 s 依字母順序排序產品名稱。 這表示在本教學課程中，使用自訂分頁執行，我們將無法建立自訂的分頁報表，也無法進行排序。 不過，在下一個教學課程中，我們將瞭解如何提供這類功能。

在上一節中，我們建立了 DAL 方法做為臨機操作 SQL 語句。 可惜的是，TableAdapter wizard 使用 Visual Studio 中的 T-sql 剖析器，並不像 `ROW_NUMBER()` 函數所使用的 `OVER` 語法。 因此，我們必須將此 DAL 方法建立為預存程式。 從 [View] 功能表選取 [伺服器總管] （或按 Ctrl + Alt + S），然後展開 [`NORTHWND.MDF`] 節點。 若要加入新的預存程式，請以滑鼠右鍵按一下 [預存程式] 節點，然後選擇 [加入新的預存程式] （請參閱 [圖 6]）。

![加入新的預存程式，以透過產品進行分頁](efficiently-paging-through-large-amounts-of-data-vb/_static/image6.png)

**圖 6**：加入新的預存程式以進行產品分頁

這個預存程式應該接受兩個整數輸入參數-`@startRowIndex` 和 `@maximumRows`，並使用 `ProductName` 欄位所排序的 `ROW_NUMBER()` 函數，只傳回大於指定 `@startRowIndex` 且小於或等於 `@startRowIndex` + `@maximumRow` s 的資料列。 在新的預存程式中輸入下列腳本，然後按一下 [儲存] 圖示，將預存程式加入至資料庫。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample7.sql)]

建立預存程式之後，請花點時間進行測試。以滑鼠右鍵按一下 伺服器總管中的 `GetProductsPaged` 預存程式名稱，然後選擇 執行 選項。 Visual Studio 接著會提示您輸入參數，`@startRowIndex` 和 `@maximumRow` （請參閱 [圖 7]）。 請嘗試不同的值，並檢查結果。

![輸入 @startRowIndex 和 @maximumRows 參數的值](efficiently-paging-through-large-amounts-of-data-vb/_static/image7.png)

<strong>圖 7</strong>：輸入 @startRowIndex 和 @maximumRows 參數的值

選擇這些輸入參數值之後，[輸出] 視窗會顯示結果。 [圖 8] 顯示同時為 `@startRowIndex` 和 `@maximumRows` 參數傳遞10的結果。

[![會傳回資料第二頁中顯示的記錄](efficiently-paging-through-large-amounts-of-data-vb/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image8.png)

**圖 8**：會傳回資料第二頁中顯示的記錄（[按一下以觀看完整大小的影像](efficiently-paging-through-large-amounts-of-data-vb/_static/image10.png)）

建立這個預存程式之後，我們就可以開始建立 `ProductsTableAdapter` 方法。 開啟 `Northwind.xsd` 類型資料集，以滑鼠右鍵按一下 `ProductsTableAdapter`，然後選擇 [加入查詢] 選項。 請不要使用臨機操作 SQL 語句來建立查詢，而是使用現有的預存程式來建立。

![使用現有的預存程式建立 DAL 方法](efficiently-paging-through-large-amounts-of-data-vb/_static/image11.png)

**圖 9**：使用現有的預存程式建立 DAL 方法

接下來，系統會提示您選取要叫用的預存程式。 從下拉式清單中挑選 `GetProductsPaged` 預存程式。

![從下拉式清單中選擇 [GetProductsPaged] 預存程式](efficiently-paging-through-large-amounts-of-data-vb/_static/image12.png)

**圖 10**：從下拉式清單中選擇 GetProductsPaged 預存程式

接著，下一個畫面會詢問您的預存程式所傳回的資料類型：表格式資料、單一值或無值。 因為 `GetProductsPaged` 預存程式可以傳回多筆記錄，表示它會傳回表格式資料。

![表示預存程式會傳回表格式資料](efficiently-paging-through-large-amounts-of-data-vb/_static/image13.png)

**圖 11**：表示預存程式會傳回表格式資料

最後，指出您想要建立之方法的名稱。 如同先前的教學課程，請繼續進行，並使用 [填入 DataTable] 和 [傳回 DataTable] 來建立方法。 將第一個方法命名為 `FillPaged` 和第二個 `GetProductsPaged`。

![將方法命名為 FillPaged 和 GetProductsPaged](efficiently-paging-through-large-amounts-of-data-vb/_static/image14.png)

**圖 12**：將方法命名為 FillPaged 和 GetProductsPaged

除了建立 DAL 方法來傳回特定的產品頁面之外，我們也需要在 BLL 中提供這類功能。 如同 DAL 方法，BLL s GetProductsPaged 方法必須接受兩個整數輸入來指定開始資料列索引和最大資料列，而且必須只傳回落在指定範圍內的記錄。 在 ProductsBLL 類別中建立這種 BLL 方法，只會向下呼叫 DAL s GetProductsPaged 方法，如下所示：

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample8.vb)]

您可以針對 BLL 方法的輸入參數使用任何名稱，但如我們稍後所見，選擇使用 `startRowIndex` 並 `maximumRows` 在設定 ObjectDataSource 以使用此方法時，將我們從額外的工作中省下。

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>步驟4：設定 ObjectDataSource 使用自訂分頁

藉由使用 BLL 和 DAL 方法來存取特定記錄子集，我們已準備好建立 GridView 控制項，以使用自訂分頁來逐頁查看其基礎記錄。 一開始先開啟 [`PagingAndSorting`] 資料夾中的 [`EfficientPaging.aspx`] 頁面，將 GridView 新增至頁面，並將它設定為使用新的 ObjectDataSource 控制項。 在過去的教學課程中，我們通常會將 ObjectDataSource 設定為使用 `ProductsBLL` 類別的 `GetProducts` 方法。 不過這一次，我們想要改為使用 `GetProductsPaged` 方法，因為 `GetProducts` 方法會傳回資料庫中的*所有*產品，而 `GetProductsPaged` 只會傳回特定的記錄子集。

![將 ObjectDataSource 設定為使用 ProductsBLL 類別 s GetProductsPaged 方法](efficiently-paging-through-large-amounts-of-data-vb/_static/image15.png)

**圖 13**：設定 ObjectDataSource 使用 ProductsBLL Class s GetProductsPaged 方法

由於我們會重新建立唯讀 GridView，請花點時間將 [插入]、[更新] 和 [刪除] 索引標籤中的 [方法] 下拉式清單設定為 [（無）]。

接下來，ObjectDataSource wizard 會提示我們提供 `GetProductsPaged` 方法 `startRowIndex` 的來源，並 `maximumRows` 輸入參數值。 這些輸入參數實際上會由 GridView 自動設定，因此只要將來源設定為 [無]，然後按一下 [完成] 即可。

![將輸入參數來源保留為 [無]](efficiently-paging-through-large-amounts-of-data-vb/_static/image16.png)

**圖 14**：將輸入參數的來源保留為 None

完成 ObjectDataSource wizard 之後，GridView 會針對每個產品資料欄位包含 BoundField 或 CheckBoxField。 您可以隨意調整 GridView 的外觀。 我選擇只顯示 `ProductName`、`CategoryName`、`SupplierName`、`QuantityPerUnit`和 `UnitPrice` BoundFields。 此外，請檢查其智慧標籤中的 [啟用分頁] 核取方塊，將 GridView 設定為支援分頁。 這些變更之後，GridView 和 ObjectDataSource 宣告式標記看起來應該如下所示：

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample9.aspx)]

不過，如果您透過瀏覽器造訪網頁，則 GridView 是找不到的地方。

![GridView 不會顯示](efficiently-paging-through-large-amounts-of-data-vb/_static/image17.png)

**圖 15**： GridView 不會顯示

因為 ObjectDataSource 目前使用0做為兩個 `GetProductsPaged` `startRowIndex` 和 `maximumRows` 輸入參數的值，所以缺少 GridView。 因此，產生的 SQL 查詢不會傳回任何記錄，因此不會顯示 GridView。

若要解決此問題，我們必須將 ObjectDataSource 設定為使用自訂分頁。 這可以在下列步驟中完成：

1. **將 objectdatasource 的 `EnablePaging` 屬性設定為 `true`** 這會向 ObjectDataSource 指出它必須傳遞給 `SelectMethod` 兩個額外的參數：一個用來指定起始資料列索引（[`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx)），另一個則用來指定最大資料列（[`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx)）。
2. **設定 ObjectDataSource s `StartRowIndexParameterName` 並適當地 `MaximumRowsParameterName` 屬性**，`StartRowIndexParameterName` 和 `MaximumRowsParameterName` 屬性則會指出傳入 `SelectMethod` 中的輸入參數名稱，以供自訂分頁用途之用。 根據預設，這些參數名稱會 `startIndexRow` 和 `maximumRows`，這就是為什麼在 BLL 中建立 `GetProductsPaged` 方法時，我使用了這些值做為輸入參數。 如果您選擇針對 BLL `GetProductsPaged` 方法（例如 `startIndex` 和 `maxRows`）使用不同的參數名稱，例如，您將需要適當地設定 ObjectDataSource s `StartRowIndexParameterName` 和 `MaximumRowsParameterName` 屬性（例如，針對 `StartRowIndexParameterName` 使用 [startIndex] 和 [maxRows]）。`MaximumRowsParameterName`
3. **將 [ObjectDataSource s [`SelectCountMethod`] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx)設為方法的名稱，此方法會傳回透過**執行 `SELECT COUNT(*) FROM Products` 查詢之 DAL 方法，透過（`TotalNumberOfProducts`）重新分頁的記錄總數，這是 `ProductsBLL` 類別的 `TotalNumberOfProducts` 方法傳回的記錄總數。 ObjectDataSource 需要這項資訊，才能正確呈現分頁介面。
4. 在透過 wizard 設定 ObjectDataSource 時，**從 objectdatasource s 宣告式標記中移除 `startRowIndex` 和 `maximumRows` `<asp:Parameter>` 元素**，Visual Studio 自動為 `<asp:Parameter>` 方法的輸入參數新增兩個 `GetProductsPaged` 元素。 藉由將 `EnablePaging` 設定為 `true`，將會自動傳遞這些參數;如果它們也出現在宣告式語法中，ObjectDataSource 會嘗試將*四個*參數傳遞給 `GetProductsPaged` 方法，並將兩個參數傳遞給 `TotalNumberOfProducts` 方法。 如果您忘記移除這些 `<asp:Parameter>` 元素，當您透過瀏覽器造訪網頁時，會收到類似下列的錯誤訊息： *ObjectDataSource ' ObjectDataSource1 ' 找不到具有參數的非泛型方法 ' TotalNumberOfProducts '： startRowIndex、maximumRows*。

進行這些變更之後，ObjectDataSource 的宣告式語法應如下所示：

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample10.aspx)]

請注意，`EnablePaging` 和 `SelectCountMethod` 屬性已設定，且已移除 `<asp:Parameter>` 元素。 [圖 16] 顯示了在進行這些變更之後，屬性視窗的螢幕擷取畫面。

![若要使用自訂分頁，請設定 ObjectDataSource 控制項](efficiently-paging-through-large-amounts-of-data-vb/_static/image18.png)

**圖 16**：若要使用自訂分頁，請設定 ObjectDataSource 控制項

進行這些變更之後，請透過瀏覽器造訪此頁面。 您應該會看到列出10個產品，依字母順序排序。 請花點時間一次執行一頁的資料。 雖然預設分頁和自訂分頁之間沒有與使用者的視覺差異，但自訂分頁會更有效率地流覽大量資料，因為它只會抓取需要針對特定頁面顯示的記錄。

[![依產品名稱排序的資料會使用自訂分頁進行分頁](efficiently-paging-through-large-amounts-of-data-vb/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image19.png)

**圖 17**：依產品名稱排序的資料會使用自訂分頁進行分頁（[按一下以查看完整大小的影像](efficiently-paging-through-large-amounts-of-data-vb/_static/image21.png)）

> [!NOTE]
> 使用自訂分頁，ObjectDataSource s `SelectCountMethod` 所傳回的頁面計數值會儲存在 GridView s 檢視狀態。 其他 GridView 變數： `PageIndex`、`EditIndex`、`SelectedIndex`、`DataKeys` 集合等都會儲存在*控制項狀態*中，而不論 GridView 的 `EnableViewState` 屬性值為何。 由於 `PageCount` 值會使用 view 狀態在回傳之間保存，因此，當使用包含連結的分頁介面來將您帶到最後一頁時，就必須啟用 GridView s 檢視狀態。 （如果您的分頁介面不包含最後一頁的直接連結，則您可以停用 view 狀態）。

按一下 [最後一頁] 連結會導致回傳，並指示 GridView 更新其 `PageIndex` 屬性。 如果按一下 [最後一頁] 連結，GridView 會將其 `PageIndex` 屬性指派為一個小於其 `PageCount` 屬性的值。 當停用 view 狀態時，`PageCount` 值會跨回傳遺失，而 `PageIndex` 會改為指派最大整數值。 接下來，GridView 會藉由將 `PageSize` 和 `PageCount` 屬性相乘來嘗試判斷起始資料列索引。 這會導致 `OverflowException`，因為產品超過允許的整數大小上限。

## <a name="implement-custom-paging-and-sorting"></a>執行自訂分頁和排序

目前的自訂分頁執行需要在建立 `GetProductsPaged` 預存程式時，以靜態方式指定資料的分頁順序。 不過，您可能已注意到除了 [啟用分頁] 選項之外，GridView 的智慧標籤包含 [啟用排序] 核取方塊。 可惜的是，使用目前的自訂分頁執行將排序支援加入至 GridView，只會在目前已查看的資料頁面上排序記錄。 例如，如果您將 GridView 設定為同時支援分頁，則在觀看第一頁的資料時，依產品名稱的遞減順序排序，將會反轉頁面1上產品的順序。 如 [圖 18] 所示，這種方式會在以反向字母順序排序時，將 Carnarvon Tigers 顯示為第一項產品，這會忽略 Carnarvon Tigers 之後的71其他產品（依字母順序）;排序中只會考慮第一個頁面上的記錄。

[僅 ![目前頁面上顯示的資料已排序](efficiently-paging-through-large-amounts-of-data-vb/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image22.png)

**圖 18**：只有目前頁面上顯示的資料才會排序（[按一下以查看完整大小的影像](efficiently-paging-through-large-amounts-of-data-vb/_static/image24.png)）

排序僅適用于目前的資料頁面，因為在從 BLL s `GetProductsPaged` 方法抓取資料之後，會進行排序，而此方法只會傳回特定頁面的記錄。 若要正確地執行排序，我們必須將排序運算式傳遞給 `GetProductsPaged` 方法，以便在傳回資料的特定頁面之前，適當地排序資料。 我們會在下一個教學課程中瞭解如何完成這項操作。

## <a name="implementing-custom-paging-and-deleting"></a>執行自訂分頁和刪除

如果您在使用自訂分頁技術來分頁資料的 GridView 中啟用刪除功能，則在刪除最後一頁的最後一筆記錄時，GridView 會消失，而不會適當地遞減 GridView 的 `PageIndex`。 若要重現此 bug，請針對我們剛剛建立的教學課程啟用刪除。 移至最後一頁（第9頁），您應該會看到單一產品，因為我們會逐頁流覽81產品，一次提供10個產品。 刪除此產品。

在刪除最後一個產品時，GridView*應該*會自動移至第八頁，而這類功能會以預設分頁來呈現。 不過，有了自訂分頁，在刪除最後一頁最後一次的產品之後，GridView 就會完全從螢幕上消失。 這種情況的*確切原因是此教學*課程的範圍以外的一點，請參閱[從 GridView 中刪除最後一頁的最後一筆記錄，其中包含自訂分頁](http://scottonwriting.net/sowblog/posts/7326.aspx)，以取得此問題來源的低層級詳細資料。 在 [摘要] 中，由於按下 [刪除] 按鈕時，GridView 所執行的步驟順序如下所示：

1. 刪除記錄
2. 取得適當的記錄，以顯示指定的 `PageIndex` 和 `PageSize`
3. 請檢查並確定 `PageIndex` 不會超過資料來源中的資料頁數目;如果有，會自動遞減 GridView 的 `PageIndex` 屬性
4. 使用步驟2中取得的記錄，將適當的資料頁面系結至 GridView

問題源自于步驟2中，抓取要顯示的記錄時所使用的 `PageIndex`，仍然是剛剛刪除其唯一記錄之最後一個頁面的 `PageIndex`。 因此，在步驟2中，因為資料的最後一頁已不再包含任何記錄，所以*不*會傳回任何記錄。 然後，在步驟3中，GridView 發現其 `PageIndex` 屬性大於資料來源中的總頁數（因為我們已刪除最後一頁中的最後一筆記錄），因此會遞減其 `PageIndex` 屬性。 在步驟4中，GridView 會嘗試將自己系結至在步驟2中抓取的資料;不過，在步驟2中，不會傳回任何記錄，因此會導致空的 GridView。 使用預設分頁時，此問題不會呈現介面，因為在步驟2中，*所有*記錄都是從資料來源中取出。

若要修正此問題，我們有兩個選項。 第一種是建立 GridView `RowDeleted` 事件處理常式的事件處理常式，以判斷剛刪除的頁面中顯示的記錄數目。 如果只有一筆記錄，則剛剛刪除的記錄必須是最後一個，而且我們需要減少 GridView 的 `PageIndex`。 當然，我們只想要在刪除作業確實成功時更新 `PageIndex`，這可以藉由確保 `e.Exception` 屬性 `null`來判斷。

這種方法的運作方式是，它會在步驟1之後但在步驟2之前更新 `PageIndex`。 因此，在步驟2中，會傳回適當的記錄集。 若要完成這項操作，請使用如下所示的程式碼：

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample11.vb)]

替代的解決方法是建立 ObjectDataSource s `RowDeleted` 事件的事件處理常式，並將 `AffectedRows` 屬性設定為1的值。 刪除步驟1中的記錄（但在重新抓取步驟2中的資料之前），GridView 會更新其 `PageIndex` 屬性（如果作業有一或多個資料列受到影響）。 不過，`AffectedRows` 屬性不是由 ObjectDataSource 設定的，因此會省略此步驟。 執行此步驟的其中一個方法是，如果刪除作業順利完成，則手動設定 `AffectedRows` 屬性。 這可以使用如下的程式碼來完成：

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample12.vb)]

這兩個事件處理常式的程式碼都可以在 `EfficientPaging.aspx` 範例的程式碼後置類別中找到。

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>比較預設值和自訂分頁的效能

由於自訂分頁只會抓取所需的記錄，而預設分頁會傳回每個所要查看頁面的*所有*記錄，這表示自訂分頁比預設分頁更有效率。 但是，自訂分頁的效率是多少？ 從預設分頁移至自訂分頁，可以看到哪些類型的效能提升？

可惜的是，這裡沒有任何一種大小符合所有答案。 效能提升取決於數個因素，最明顯的兩個是要逐頁查看的記錄數目，以及放在資料庫伺服器上的負載，以及 web 伺服器和資料庫伺服器之間的通道。 針對只有數十筆記錄的小型資料表，效能差異可能會是可忽略的。 不過，對於大型資料表，有數千到數十萬個數據列，效能的差異很大。

[在 ASP.NET 2.0 中使用 SQL Server 2005 的自訂分頁](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)一文中，有一些我執行的效能測試，可在分頁處理具有50000記錄的資料庫資料表時，展現這兩個分頁技術之間的效能差異。 在這些測試中，我同時探討了在 SQL Server 層級執行查詢的時間（使用[SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)），以及使用[ASP.NET s 追蹤功能](https://msdn.microsoft.com/library/y13fw6we.aspx)的 ASP.NET 網頁。 請記住，這些測試是在具有單一作用中使用者的開發箱上執行，因此是 unscientific 的，而且不會模擬一般的網站負載模式。 不論如何，在使用足夠大量的資料時，其結果會說明預設和自訂分頁的執行時間相對差異。

|  | **平均持續時間（秒）** | **讀取** |
| --- | --- | --- |
| **預設分頁 SQL Profiler** | 1.411 | 383 |
| **自訂分頁 SQL Profiler** | 0.002 | 29 |
| **預設分頁 ASP.NET 追蹤** | 2.379 | *N/A* |
| **自訂分頁 ASP.NET 追蹤** | 0.029 | *N/A* |

如您所見，抓取資料的特定頁面所需的平均讀取時間為354，而在一小段時間內則會完成。 在 [ASP.NET] 頁面上，[自訂] 頁面在使用預設分頁時，可以在<sup>接近1/100 的</sup>時間呈現。 請參閱[我的文章](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)，以取得有關這些結果的詳細資訊，以及您可以下載的程式碼和資料庫，以便在您自己的環境中重現這些測試。

## <a name="summary"></a>總結

預設分頁是執行的標準化，只需核取 [資料 Web 控制項] 智慧標籤中的 [啟用分頁] 核取方塊，但這種簡化功能就會產生效能成本。 使用預設分頁時，如果使用者要求任何資料頁面，則會傳回*所有*記錄，即使只會顯示其中的一小部分也一樣。 為了對抗這項效能額外負荷，ObjectDataSource 提供了替代的分頁選項自訂分頁。

雖然自訂分頁會藉由只抓取需要顯示的記錄來改善預設的分頁效能問題，但它更牽涉到如何執行自訂分頁。 首先，必須正確地撰寫查詢（且有效率地）存取所要求記錄的特定子集。 這可以透過數種方式來完成;我們在本教學課程中檢查的是使用 SQL Server 2005 s new `ROW_NUMBER()` 函式來排序結果，然後只傳回其排名落在指定範圍內的結果。 此外，我們還需要新增一種方法來判斷要進行分頁的記錄總數。 建立這些 DAL 和 BLL 方法之後，我們也需要設定 ObjectDataSource，讓它可以判斷正在進行分頁的總記錄數，並可將開始資料列索引和最大資料列值正確地傳遞給 BLL。

雖然執行自訂分頁確實需要幾個步驟，而且不像預設分頁一樣簡單，但自訂分頁在分頁處理足夠大量的資料時是必要的。 當所檢查的結果顯示時，自訂分頁可以縮減 ASP.NET 網頁轉譯時間的秒數，而且可以藉由一或多個數量級來使資料庫伺服器上的負載變亮。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](paging-and-sorting-report-data-vb.md)
> [下一頁](sorting-custom-paged-data-vb.md)
