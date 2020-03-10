---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
title: 更新 TableAdapter 以使用 Join （VB） |Microsoft Docs
author: rick-anderson
description: 使用資料庫時，通常會要求分散到多個資料表的資料。 若要從兩個不同的資料表取出資料，我們可以使用 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: e624a3e0-061b-4efc-8b0e-5877f9ff6714
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c94baa99b126cdd24d69afc3d02bfe8b069419b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78532267"
---
# <a name="updating-the-tableadapter-to-use-joins-vb"></a>更新 TableAdapter 以使用 JOIN (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_VB.zip)或[下載 PDF](updating-the-tableadapter-to-use-joins-vb/_static/datatutorial69vb1.pdf)

> 使用資料庫時，通常會要求分散到多個資料表的資料。 若要從兩個不同的資料表中取出資料，我們可以使用相互關聯的子查詢或聯結作業。 在本教學課程中，我們將比較相互關聯的子查詢和聯結語法，然後再查看如何建立在其主要查詢中包含聯結的 TableAdapter。

## <a name="introduction"></a>簡介

使用關係資料庫時，我們想要使用的資料通常會分散到多個資料表。 例如，顯示產品資訊時，我們可能會想要列出每個產品的對應類別和供應商名稱。 `Products` 資料表具有 `CategoryID` 和 `SupplierID` 值，但實際的分類和供應商名稱分別位於 `Categories` 和 `Suppliers` 資料表中。

若要從另一個相關的資料表取出資訊，我們可以使用相互*關聯的子查詢*或 `JOIN`*s*。 相互關聯的子查詢是參考外部查詢中資料行的嵌套 `SELECT` 查詢。 例如，在[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程中，我們在 `ProductsTableAdapter` s 主查詢中使用了兩個相互關聯的子查詢，以傳回每個產品的類別目錄和供應商名稱。 `JOIN` 是一種 SQL 結構，可合併兩個不同資料表的相關資料列。 我們在使用[SqlDataSource 控制項來查詢資料](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb.md)教學課程中使用了 `JOIN`，以便在每個產品旁顯示類別資訊。

我們從使用 `JOIN` s 與 Tableadapter abstained 的原因，是因為 TableAdapter s wizard 中的限制會自動產生對應的 `INSERT`、`UPDATE`和 `DELETE` 語句。 更明確地說，如果 TableAdapter 的主查詢包含任何 `JOIN` s，TableAdapter 就無法針對其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性，自動建立臨機操作 SQL 語句或預存程式。

在本教學課程中，我們將簡短地比較和對比相互關聯的子查詢和 `JOIN`，然後再探索如何建立在其主要查詢中包含 `JOIN` 的 TableAdapter。

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>比較和對比相互關聯的子查詢與`JOIN` s

回想一下，在 `Northwind` 資料集的第一個教學課程中建立的 `ProductsTableAdapter` 會使用相互關聯的子查詢，以傳回每個產品的對應類別和供應商名稱。 `ProductsTableAdapter` s 主要查詢如下所示。

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample1.sql)]

兩個相互關聯的子查詢 `(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` 和 `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)` 是 `SELECT` 查詢，會傳回每個產品的單一值，做為外部 `SELECT` 語句 s 資料行清單中的額外資料行。

或者，`JOIN` 可以用來傳回每個產品的供應商和類別目錄名稱。 下列查詢會傳回與上述相同的輸出，但會使用 `JOIN` s 來取代子查詢：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample2.sql)]

`JOIN` 會根據某些準則，合併一個資料表中的記錄與另一個資料表中的記錄。 例如，在上述查詢中，`LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` 會指示 SQL Server 合併每個產品記錄與分類記錄，其 `CategoryID` 值符合產品的 `CategoryID` 值。 合併的結果可讓我們處理每項產品的對應類別欄位（例如 `CategoryName`）。

> [!NOTE]
> 在查詢關係資料庫中的資料時，通常會使用 `JOIN` s。 如果您不熟悉 `JOIN` 語法，或需要在其使用方式上進行多筆處理，我建議您在[W3 學校](http://www.w3schools.com/)的[SQL 聯結教學](http://www.w3schools.com/sql/sql_join.asp)課程。 另請閱讀《 [SQL 線上叢書》](https://msdn.microsoft.com/library/ms130214.aspx)中的[`JOIN` 基本](https://msdn.microsoft.com/library/ms191517.aspx)概念和[子查詢基本](https://msdn.microsoft.com/library/ms189575.aspx)概念一節。

因為 `JOIN` s 和相互關聯的子查詢都可以用來從其他資料表中取出相關資料，所以許多開發人員會留下抓著自己的想法，並知道要使用哪種方法。 我之前提到的所有 SQL 專家都說過大致相同的事，因為 SQL Server 會產生大致相同的執行計畫。 我們的建議是使用您和您的小組最熟悉的技術。 值得注意的是，在清楚告知這項建議之後，這些專家會立即透過相互關聯的子查詢來表達其 `JOIN` 的喜好設定。

使用具類型的資料集來建立資料存取層時，使用子查詢時，工具的效果較佳。 特別的是，如果主要查詢包含任何 `JOIN`，則 TableAdapter s wizard 不會自動產生對應的 `INSERT`、`UPDATE`和 `DELETE` 語句，但會在使用相互關聯的子查詢時自動產生這些語句。

若要探索此缺點，請在 `~/App_Code/DAL` 資料夾中建立臨時類型資料集。 在 [TableAdapter 設定向導] 中，選擇使用臨機操作 SQL 語句，並輸入下列 `SELECT` 查詢（請參閱 [圖 1]）：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample3.sql)]

[![輸入包含聯結的主要查詢](updating-the-tableadapter-to-use-joins-vb/_static/image2.png)](updating-the-tableadapter-to-use-joins-vb/_static/image1.png)

**圖 1**：輸入包含 `JOIN` s 的主要查詢（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image3.png)）

根據預設，TableAdapter 會依據主要查詢自動建立 `INSERT`、`UPDATE`和 `DELETE` 語句。 如果您按一下 [Advanced] 按鈕，就會看到此功能已啟用。 雖然此設定，但 TableAdapter 將無法建立 `INSERT`、`UPDATE`和 `DELETE` 語句，因為主要查詢包含 `JOIN`。

![輸入包含聯結的主要查詢](updating-the-tableadapter-to-use-joins-vb/_static/image4.png)

**圖 2**：輸入包含 `JOIN` s 的主要查詢

按一下 [完成] 完成精靈。 此時，您的資料集的設計工具會包含一個具有 DataTable 的單一 TableAdapter，其中每個欄位在 `SELECT` query s 資料行清單中傳回。 這包括 `CategoryName` 和 `SupplierName`，如 [圖 3] 所示。

![DataTable 會針對資料行清單中傳回的每個欄位包含一個資料行。](updating-the-tableadapter-to-use-joins-vb/_static/image5.png)

**圖 3**： DataTable 針對資料行清單中傳回的每個欄位包含一個資料行

雖然 DataTable 具有適當的資料行，但 TableAdapter 缺少其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性的值。 若要確認這一點，請按一下設計工具中的 TableAdapter，然後移至 [屬性視窗]。 在這裡，您會看到 [`InsertCommand`]、[`UpdateCommand`] 和 [`DeleteCommand`] 屬性設定為 [（無）]。

[![[InsertCommand]、[UpdateCommand] 和 [DeleteCommand] 屬性設定為 [（無）]](updating-the-tableadapter-to-use-joins-vb/_static/image7.png)](updating-the-tableadapter-to-use-joins-vb/_static/image6.png)

**圖 4**： [`InsertCommand`]、[`UpdateCommand`] 和 [`DeleteCommand`] 屬性設定為 [（無）] （[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image8.png)）

為了解決這種缺點，我們可以透過屬性視窗，手動提供 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性的 SQL 語句和參數。 或者，我們也可以開始設定 TableAdapter s 查詢，*不要*包含任何 `JOIN` s。 這將允許為我們自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句。 完成 wizard 之後，我們就可以從屬性視窗手動更新 TableAdapter `SelectCommand`，使其包含 `JOIN` 語法。

雖然這種方法可行，但在使用臨機操作 SQL 查詢時非常脆弱，因為每當您透過 wizard 重新設定 TableAdapter 主查詢時，自動產生的 `INSERT`、`UPDATE`和 `DELETE` 語句都會重新建立。 這表示，如果我們在 TableAdapter 上按一下滑鼠右鍵、從操作功能表中選擇 [設定]，然後再次完成嚮導，則我們之後所做的所有自訂都會遺失。

TableAdapter s 自動產生的 `INSERT`、`UPDATE`和 `DELETE` 語句的肯定脆弱度，只是特定的 SQL 語句。 如果您的 TableAdapter 使用預存程式，您可以自訂 `SelectCommand`、`InsertCommand`、`UpdateCommand`或 `DeleteCommand` 預存程式，並重新執行 TableAdapter 設定 wizard，而不必擔心預存程式將會被修改。

在接下來的幾個步驟中，我們將建立一個 TableAdapter，一開始會使用會省略任何 `JOIN` s 的主要查詢，以便自動產生對應的插入、更新和刪除預存程式。 然後，我們會更新 `SelectCommand`，以便使用會從相關資料表傳回額外資料行的 `JOIN`。 最後，我們將建立對應的商務邏輯層級類別，並示範如何在 ASP.NET 網頁中使用 TableAdapter。

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>步驟1：使用簡化的主要查詢來建立 TableAdapter

在本教學課程中，我們將為 `NorthwindWithSprocs` 資料集中的 `Employees` 資料表加入 TableAdapter 和強型別 DataTable。 `Employees` 資料表包含一個 `ReportsTo` 欄位，其中指定了員工 s 經理的 `EmployeeID`。 例如，employee Anne 劉天具有5的 `ReportTo` 值，也就是 Steven 林丹的 `EmployeeID`。 因此，Anne 報告給 Steven，她的經理。 除了報告每個員工的 `ReportsTo` 值，我們也可能會想要取得其經理的名稱。 您可以使用 `JOIN`來完成這項作業。 但是在最初建立 TableAdapter 時使用 `JOIN`，會阻止嚮導自動產生對應的插入、更新和刪除功能。 因此，我們一開始會建立一個 TableAdapter，其主要查詢不包含任何 `JOIN` s。 然後，在步驟2中，我們將更新主要查詢預存程式，以透過 `JOIN`來抓取管理員的名稱。

從開啟 `~/App_Code/DAL` 資料夾中的 `NorthwindWithSprocs` 資料集開始。 以滑鼠右鍵按一下設計工具，從內容功能表中選取 [新增] 選項，然後挑選 [TableAdapter] 功能表項目。 這會啟動 [TableAdapter 設定向導]。 如 [圖 5] 所示，讓 wizard 建立新的預存程式，然後按 [下一步]。 如需從 TableAdapter s wizard 建立新預存程式的重新整理程式，請參閱 < 為具[類型的資料集 Tableadapter 建立新的預存程式](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教學課程。

[![選取 [建立新的預存程式] 選項](updating-the-tableadapter-to-use-joins-vb/_static/image10.png)](updating-the-tableadapter-to-use-joins-vb/_static/image9.png)

**圖 5**：選取 [建立新的預存程式] 選項（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image11.png)）

針對 TableAdapter s 主要查詢使用下列 `SELECT` 語句：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample4.sql)]

因為此查詢不包含任何 `JOIN`，所以 TableAdapter wizard 會自動使用對應的 `INSERT`、`UPDATE`和 `DELETE` 語句來建立預存程式，以及執行主要查詢的預存程式。

下列步驟可讓我們命名 TableAdapter s 預存程式。 使用 `Employees_Select`、`Employees_Insert`、`Employees_Update`和 `Employees_Delete`的名稱，如 [圖 6] 所示。

[![命名 TableAdapter s 預存程式](updating-the-tableadapter-to-use-joins-vb/_static/image13.png)](updating-the-tableadapter-to-use-joins-vb/_static/image12.png)

**圖 6**：命名 TableAdapter s 預存程式（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image14.png)）

最後一個步驟會提示我們命名 TableAdapter s 方法。 使用 `Fill`，並 `GetEmployees` 做為方法名稱。 另請務必勾選 [建立方法，直接將更新傳送至資料庫（GenerateDBDirectMethods）] 核取方塊。

[![命名 TableAdapter s 方法填滿和 GetEmployees](updating-the-tableadapter-to-use-joins-vb/_static/image16.png)](updating-the-tableadapter-to-use-joins-vb/_static/image15.png)

**圖 7**：將 TableAdapter 的方法命名為 `Fill` 和 `GetEmployees` （[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image17.png)）

完成 wizard 之後，請花點時間檢查資料庫中的預存程式。 您應該會看到四個新的： `Employees_Select`、`Employees_Insert`、`Employees_Update`和 `Employees_Delete`。 接下來，檢查 `EmployeesDataTable`，並 `EmployeesTableAdapter` 剛建立的。 DataTable 包含主要查詢所傳回之每個欄位的資料行。 按一下 [TableAdapter]，然後移至 [屬性視窗]。 您會看到 [`InsertCommand`]、[`UpdateCommand`] 和 [`DeleteCommand`] 屬性已正確設定，以呼叫對應的預存程式。

[![TableAdapter 包含插入、更新和刪除功能](updating-the-tableadapter-to-use-joins-vb/_static/image19.png)](updating-the-tableadapter-to-use-joins-vb/_static/image18.png)

**圖 8**： TableAdapter 包含插入、更新和刪除功能（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image20.png)）

當自動建立 insert、update 和 delete 預存程式，且已正確設定 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性後，我們就可以自訂 `SelectCommand` 的預存程式，以傳回每個員工經理的其他相關資訊。 具體而言，我們必須更新 `Employees_Select` 預存程式，才能使用 `JOIN` 並傳回 manager s `FirstName` 和 `LastName` 值。 在更新預存程式之後，我們必須更新 DataTable，使其包含這些額外的資料行。 我們將在步驟2和3中解決這兩項工作。

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>步驟2：自訂預存程式以包含`JOIN`

一開始先前往伺服器總管，向下切入 Northwind 資料庫的 [預存程式] 資料夾，然後開啟 `Employees_Select` 預存程式。 如果您看不到此預存程式，請以滑鼠右鍵按一下 [預存程式] 資料夾，然後選擇 [重新整理]。 更新預存程式，讓它使用 `LEFT JOIN` 來傳回管理員的名字和姓氏：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample5.sql)]

更新 `SELECT` 語句之後，請前往 [檔案] 功能表，然後選擇 [儲存 `Employees_Select`]，以儲存變更。 或者，您也可以按一下工具列中的 [儲存] 圖示，或按 Ctrl + S。 儲存變更之後，以滑鼠右鍵按一下伺服器總管中的 `Employees_Select` 預存程式，然後選擇 [執行]。 這會執行預存程式，並在 [輸出] 視窗中顯示其結果（請參閱 [圖 9]）。

[![預存程式結果會顯示在輸出視窗](updating-the-tableadapter-to-use-joins-vb/_static/image22.png)](updating-the-tableadapter-to-use-joins-vb/_static/image21.png)

**圖 9**：預存程式結果會顯示在輸出視窗中（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image23.png)）

## <a name="step-3-updating-the-datatable-s-columns"></a>步驟3：更新 DataTable 的資料行

此時，`Employees_Select` 預存程式會傳回 `ManagerFirstName` 和 `ManagerLastName` 值，但 `EmployeesDataTable` 遺漏了這些資料行。 這些遺漏的資料行可以透過下列兩種方式的其中一種來加入至 DataTable：

- 以**手動**方式在 DataSet 設計工具中，以滑鼠右鍵按一下 DataTable，然後從 [加入] 功能表選擇 [資料行]。 接著，您可以將資料行命名，並據以設定其屬性。
- **自動**-TableAdapter 設定 wizard 會更新 DataTable s 資料行，以反映 `SelectCommand` 預存程式所傳回的欄位。 使用臨機操作 SQL 語句時，此 wizard 也會移除 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 屬性，因為 `SelectCommand` 現在包含 `JOIN`。 但是在使用預存程式時，這些命令屬性會維持不變。

我們已在先前的教學課程中探索手動新增 DataTable 資料行，包括[主要/詳細資料，使用具有詳細資料 DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)和[上傳](../working-with-binary-files/uploading-files-vb.md)檔案的主要記錄項目符號清單，我們將在下一個教學課程中更詳細地查看此程式。 不過，在本教學課程中，我們會透過 TableAdapter 設定 wizard 來使用自動方法。

首先，以滑鼠右鍵按一下 `EmployeesTableAdapter`，然後從內容功能表中選取 [設定]。 這會顯示 [TableAdapter 設定向導]，其中列出用來選取、插入、更新和刪除的預存程式，以及其傳回值和參數（如果有的話）。 [圖 10] 顯示此嚮導。 在這裡，我們可以看到 `Employees_Select` 預存程式現在會傳回 `ManagerFirstName` 和 `ManagerLastName` 欄位。

[![嚮導會顯示 Employees_Select 預存程式的已更新資料行清單](updating-the-tableadapter-to-use-joins-vb/_static/image25.png)](updating-the-tableadapter-to-use-joins-vb/_static/image24.png)

**圖 10**：此 Wizard 會顯示 `Employees_Select` 預存程式的已更新資料行清單（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image26.png)）

按一下 [完成] 以完成嚮導。 回到 DataSet 設計工具時，`EmployeesDataTable` 包含兩個額外的資料行： `ManagerFirstName` 和 `ManagerLastName`。

[![EmployeesDataTable 包含兩個新的資料行](updating-the-tableadapter-to-use-joins-vb/_static/image28.png)](updating-the-tableadapter-to-use-joins-vb/_static/image27.png)

**圖 11**： `EmployeesDataTable` 包含兩個新的資料行（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image29.png)）

為了說明已更新的 `Employees_Select` 預存程式已生效，而且 TableAdapter 的插入、更新和刪除功能仍可正常運作，請建立可讓使用者查看及刪除員工的網頁。 不過，在建立這類頁面之前，我們必須先在商務邏輯層中建立新的類別，以便與 `NorthwindWithSprocs` 資料集中的員工合作。 在步驟4中，我們將建立 `EmployeesBLLWithSprocs` 類別。 在步驟5中，我們將從 ASP.NET 網頁使用這個類別。

## <a name="step-4-implementing-the-business-logic-layer"></a>步驟4：執行商務邏輯層

在名為 `EmployeesBLLWithSprocs.vb`的 `~/App_Code/BLL` 資料夾中建立新的類別檔案。 這個類別會模擬現有 `EmployeesBLL` 類別的語義，只有這個新的方法會提供較少的方法，並使用 `NorthwindWithSprocs` 的資料集（而不是 `Northwind` 的資料集）。 將下列程式碼加入 `EmployeesBLLWithSprocs` 類別。

[!code-vb[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample6.vb)]

`EmployeesBLLWithSprocs` class s `Adapter` 屬性會傳回 `NorthwindWithSprocs` 資料集 `EmployeesTableAdapter`的實例。 這是由類別的 `GetEmployees` 和 `DeleteEmployee` 方法所使用。 `GetEmployees` 方法會呼叫對應 `GetEmployees` 方法的 `EmployeesTableAdapter`，它會叫用 `Employees_Select` 預存程式，並在 `EmployeeDataTable`中填入其結果。 `DeleteEmployee` 方法同樣會呼叫 `EmployeesTableAdapter` s `Delete` 方法，這會叫用 `Employees_Delete` 預存程式。

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>步驟5：使用展示層中的資料

完成 `EmployeesBLLWithSprocs` 類別之後，我們就可以透過 ASP.NET 網頁來準備使用員工資料。 開啟 [`AdvancedDAL`] 資料夾中的 [`JOINs.aspx`] 頁面，並將 GridView 從 [工具箱] 拖曳至設計工具，將其 `ID` 屬性設定為 [`Employees`]。 接下來，從 GridView 的智慧標籤，將方格系結至名為 `EmployeesDataSource`的新 ObjectDataSource 控制項。

將 ObjectDataSource 設定為使用 `EmployeesBLLWithSprocs` 類別，並從 [選取] 和 [刪除] 索引標籤，確定已從下拉式清單中選取 [`GetEmployees`] 和 [`DeleteEmployee`] 方法。 按一下 [完成] 以完成 ObjectDataSource s 設定。

[![將 ObjectDataSource 設定為使用 EmployeesBLLWithSprocs 類別](updating-the-tableadapter-to-use-joins-vb/_static/image31.png)](updating-the-tableadapter-to-use-joins-vb/_static/image30.png)

**圖 12**：設定 ObjectDataSource 使用 `EmployeesBLLWithSprocs` 類別（[按一下以觀看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image32.png)）

[![具有 ObjectDataSource，請使用 GetEmployees 和 DeleteEmployee 方法](updating-the-tableadapter-to-use-joins-vb/_static/image34.png)](updating-the-tableadapter-to-use-joins-vb/_static/image33.png)

**圖 13**：讓 ObjectDataSource 使用 `GetEmployees` 和 `DeleteEmployee` 方法（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image35.png)）

Visual Studio 會針對每個 `EmployeesDataTable` s 資料行，將 BoundField 加入至 GridView。 除了 `Title`、`LastName`、`FirstName`、`ManagerFirstName`和 `ManagerLastName` 以外，移除所有這些 BoundFields，並將最後四個 BoundFields 的 `HeaderText` 屬性分別重新命名為 last name、First name、Manager s First Name 和 Manager s 姓。

若要讓使用者能夠從這個頁面刪除員工，我們必須做兩件事。 首先，請檢查 GridView 以提供刪除功能，方法是從其智慧標籤中核取 [啟用刪除] 選項。 第二，將 objectdatasource s `OldValuesParameterFormatString` 屬性從 ObjectDataSource wizard （`original_{0}`）所設定的值變更為其預設值（`{0}`）。 進行這些變更之後，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample7.aspx)]

透過瀏覽器造訪來測試頁面。 如 [圖 14] 所示，此頁面會列出每位員工和他的經理名稱（假設他們有一個）。

[![Employees_Select 預存程式中的聯結會傳回管理員的名稱](updating-the-tableadapter-to-use-joins-vb/_static/image37.png)](updating-the-tableadapter-to-use-joins-vb/_static/image36.png)

**圖 14**： `Employees_Select` 預存程式中的 `JOIN` 會傳回管理員的名稱（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image38.png)）

按一下 [刪除] 按鈕會啟動刪除工作流程，這會在 `Employees_Delete` 預存程式的執行中最後。 不過，在預存程式中嘗試的 `DELETE` 語句會因為外鍵條件約束違規而失敗（請參閱 [圖 15]）。 具體而言，每個員工在 `Orders` 資料表中都有一筆或多筆記錄，導致刪除失敗。

[![刪除具有對應訂單的員工會導致 Foreign Key 條件約束違規](updating-the-tableadapter-to-use-joins-vb/_static/image40.png)](updating-the-tableadapter-to-use-joins-vb/_static/image39.png)

**圖 15**：刪除具有對應訂單的員工會導致外鍵條件約束違規（[按一下以查看完整大小的影像](updating-the-tableadapter-to-use-joins-vb/_static/image41.png)）

若要允許刪除員工，您可以：

- 將 foreign key 條件約束更新為 cascade delete，
- 針對您想要刪除的員工，手動刪除 `Orders` 資料表中的記錄，或
- 更新 `Employees_Delete` 預存程式，先刪除 `Orders` 資料表中的相關記錄，再刪除 `Employees` 記錄。 我們已在[使用具類型資料集的現有預存程式 tableadapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教學課程中討論過這項技術。

我將此做為讀者的練習。

## <a name="summary"></a>總結

使用關係資料庫時，查詢通常會從多個相關的資料表提取其資料。 相互關聯的子查詢和 `JOIN` 會提供兩種不同的技術，以從查詢中的相關資料表存取資料。 在先前的教學課程中，我們最常使用相互關聯的子查詢，因為 TableAdapter 無法針對涉及 `JOIN` 的查詢自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句。 雖然可以手動提供這些值，但使用臨機操作 SQL 語句時，當 TableAdapter 設定 wizard 完成時，將會覆寫任何自訂。

幸運的是，使用預存程式所建立的 Tableadapter 不會與使用臨機操作 SQL 語句所建立的肯定脆弱度相同。 因此，在使用預存程式時，建立主要查詢使用 `JOIN` 的 TableAdapter 是可行的。 在本教學課程中，我們已瞭解如何建立這類 TableAdapter。 我們開始使用適用于 TableAdapter s 主查詢的不 `JOIN``SELECT` 查詢，以便自動建立對應的插入、更新和刪除預存程式。 當 TableAdapter 的初始設定完成時，我們增強了 `SelectCommand` 預存程式來使用 `JOIN` 並重新執行 [TableAdapter 設定]，以更新 `EmployeesDataTable` 的資料行。

重新執行 TableAdapter 設定向導會自動更新 `EmployeesDataTable` 資料行，以反映 `Employees_Select` 預存程式所傳回的資料欄位。 或者，我們也可以將這些資料行手動新增至 DataTable。 在下一個教學課程中，我們將探索手動將資料行加入至 DataTable。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Geisenow、David Suru 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [下一頁](adding-additional-datatable-columns-vb.md)
