---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
title: 在 DataList 或重複項控制項中排序資料C#（） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何在 DataList 和重複項中包含排序支援，以及如何建立其資料可以的 DataList 或中繼器 。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: f52c302a-1b7c-46fe-8a13-8412c95cbf6d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 66a09c637d33c812b39e0ce85a552bd71665a2e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78620278"
---
# <a name="sorting-data-in-a-datalist-or-repeater-control-c"></a>DataList 或重複項控制項中的排序資料 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_CS.exe)或[下載 PDF](sorting-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial45cs1.pdf)

> 在本教學課程中，我們將探討如何在 DataList 和中繼器中包含排序支援，以及如何建立可分頁和排序其資料的 DataList 或中繼器。

## <a name="introduction"></a>簡介

在[上一個教學](paging-report-data-in-a-datalist-or-repeater-control-cs.md)課程中，我們探討了如何將分頁支援新增至 DataList。 我們已在傳回 `PagedDataSource` 物件的 `ProductsBLL` 類別（`GetProductsAsPagedDataSource`）中建立新的方法。 當系結至 DataList 或中繼器時，DataList 或中繼器只會顯示所要求的資料頁面。 這項技術與 GridView、DetailsView 和 FormView 控制項內部使用的類似，以提供其內建的預設分頁功能。

除了提供分頁支援外，GridView 也包含現成的排序支援。 DataList 和中繼器都不會提供內建的排序功能;不過，您可以使用一些程式碼來加入排序功能。 在本教學課程中，我們將探討如何在 DataList 和中繼器中包含排序支援，以及如何建立可分頁和排序其資料的 DataList 或中繼器。

## <a name="a-review-of-sorting"></a>排序的審查

如我們在[分頁和排序報表資料](../paging-and-sorting/paging-and-sorting-report-data-cs.md)教學課程中所見，GridView 控制項提供現成的排序支援。 每個 GridView 欄位都可以有相關聯的 `SortExpression`，表示用來排序資料的資料欄位。 當 GridView 的 `AllowSorting` 屬性設定為 `true`時，具有 `SortExpression` 屬性值的每個 GridView 欄位都會將其標頭轉譯為 LinkButton。 當使用者按一下特定的 GridView 欄位標頭時，就會發生回傳，並根據按下的欄位 `SortExpression`來排序資料。

GridView 控制項也有 `SortExpression` 屬性，它會儲存 GridView 欄位的 `SortExpression` 以排序資料。 此外，`SortDirection` 屬性會指出是否要以遞增或遞減順序來排序資料（如果使用者連續按一下特定的 GridView 欄位標題連結兩次，則會切換排序次序）。

當 GridView 系結至其資料來源控制項時，它會將其 `SortExpression` 和 `SortDirection` 屬性交給資料來源控制項。 資料來源控制項會抓取資料，然後根據提供的 `SortExpression` 和 `SortDirection` 屬性加以排序。 排序資料之後，資料來源控制項會將它傳回給 GridView。

若要使用 DataList 或重複項控制項來複寫這項功能，我們必須：

- 建立排序介面
- 請記住要排序的資料欄位，以及是否要以遞增或遞減順序排序
- 指示 ObjectDataSource 依特定資料欄位排序資料

我們將在步驟3和4中解決這三項工作。 接下來，我們將探討如何在 DataList 或中繼器中包含分頁和排序支援。

## <a name="step-2-displaying-the-products-in-a-repeater"></a>步驟2：在中繼器中顯示產品

在我們擔心如何執行任何排序相關的功能之前，請先讓我們先在中繼器控制項中列出產品。 從開啟 [`PagingSortingDataListRepeater`] 資料夾中的 [`Sorting.aspx`] 頁面開始。 將 [中繼器] 控制項新增至網頁，並將其 `ID` 屬性設定為 [`SortableProducts`]。 從 [中繼器] 智慧標籤中，建立名為 `ProductsDataSource` 的新 ObjectDataSource，並將其設定為從 `ProductsBLL` 類別 s `GetProducts()` 方法中取出資料。 從 [插入]、[更新] 和 [刪除] 索引標籤的下拉式清單中，選取 [（無）] 選項。

[![建立 ObjectDataSource 並將其設定為使用 GetProductsAsPagedDataSource （）方法](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**圖 1**：建立 ObjectDataSource 並將其設定為使用 `GetProductsAsPagedDataSource()` 方法（[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)）

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image4.png)

**圖 2**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image6.png)）

不同于 DataList，Visual Studio 不會在系結至資料來源之後，自動建立中繼器控制項的 `ItemTemplate`。 此外，我們必須以宣告方式新增此 `ItemTemplate`，因為「中繼器控制項」智慧標籤缺少 DataList s 中的 [編輯範本] 選項。 讓我們使用上一個教學課程中的相同 `ItemTemplate`，這會顯示產品的名稱、供應商和類別目錄。

新增 `ItemTemplate`之後，中繼器和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample1.aspx)]

[圖 3] 顯示透過瀏覽器觀看的此頁面。

[會顯示每個產品的名稱、供應商和類別 ![](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**圖 3**：會顯示每個產品的名稱、供應商和類別（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image9.png)）

## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>步驟3：指示 ObjectDataSource 排序資料

若要排序在中繼器中顯示的資料，我們必須通知資料應該排序之排序運算式的 ObjectDataSource。 在 ObjectDataSource 抓取其資料之前，它會先引發它的[`Selecting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx)，讓我們有機會指定排序運算式。 `Selecting` 事件處理常式會傳遞[`ObjectDataSourceSelectingEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx)類型的物件，其具有名為[`Arguments`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx)類型[`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)的屬性。 `DataSourceSelectArguments` 類別的設計目的是要將資料相關的要求從資料取用者傳遞到資料來源控制項，並包含[`SortExpression` 屬性](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)。

若要將排序資訊從 ASP.NET 網頁傳遞至 ObjectDataSource，請建立 `Selecting` 事件的事件處理常式，並使用下列程式碼：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

應將資料欄位的名稱指派給*sortExpression*值，以排序資料（例如 ProductName）。 沒有排序方向相關的屬性，因此如果您想要以遞減順序排序資料，請將字串 DESC 附加至*sortExpression*值（例如 ProductName DESC）。

請繼續嘗試一些不同的硬式編碼值，以在瀏覽器中*sortExpression*和測試結果。 如 [圖 4] 所示，使用 ProductName DESC 做為*sortExpression*時，產品會依其名稱以反向字母順序排序。

[![產品依其名稱以反向字母順序排序](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**圖 4**：產品依其名稱以相反的字母順序排序（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image12.png)）

## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>步驟4：建立排序介面，並記住排序運算式和方向

開啟 GridView 中的排序支援時，會將每個可排序的欄位 s 標頭文字轉換成 LinkButton，當按下該按鈕時，會據以排序資料。 這類排序介面對 GridView 很有意義，因為它的資料會在資料行中整齊地配置。 不過，對於 DataList 和中繼器控制項，則需要不同的排序介面。 資料清單的一般排序介面（相對於資料格線）是下拉式清單，提供可供排序資料的欄位使用。 在本教學課程中，我們將會執行此類介面。

將 DropDownList Web 控制項新增至 `SortableProducts` 中繼器上方，並將其 `ID` 屬性設定為 [`SortBy`]。 從屬性視窗按一下 [`Items`] 屬性中的省略號，以顯示 [出現內容集合編輯器]。 加入 `ListItem`，以依據 `ProductName`、`CategoryName`和 `SupplierName` 欄位排序資料。 此外，也請新增 `ListItem`，依其名稱以反向字母順序排序產品。

`ListItem` `Text` 屬性可以設定為任何值（例如 [名稱]），但 `Value` 屬性必須設定為資料欄位的名稱（例如 ProductName）。 若要以遞減順序排序結果，請將字串 DESC 附加至資料欄位名稱，例如 ProductName DESC。

![為每個可排序的資料欄位新增資料列](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**圖 5**：為每個可排序的資料欄位加入 `ListItem`

最後，在 DropDownList 的右側新增按鈕 Web 控制項。 將其 `ID` 設為 `RefreshRepeater`，並將其 `Text` 屬性設定為 [重新整理]。

建立 `ListItem` 並新增 [重新整理] 按鈕後，DropDownList 和按鈕的宣告式語法看起來應該如下所示：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

當排序 DropDownList 完成時，我們接下來需要更新 ObjectDataSource s `Selecting` 事件處理常式，使其使用所選取的 `SortBy``ListItem` s `Value` 屬性，而不是硬式編碼的排序運算式。

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample4.cs)]

此時，第一次流覽頁面時，產品一開始會依照 [`ProductName` 資料] 欄位進行排序，因為 `SortBy` 預設 `ListItem` 選取（請參閱 [圖 6]）。 選取不同的排序選項（例如分類和按一下 [重新整理]）將會導致回傳，並依類別目錄名稱重新排序資料，如 [圖 7] 所示。

[![產品一開始依其名稱排序](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)

**圖 6**：產品一開始依其名稱排序（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)）

[![產品現在依類別目錄排序](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)

**圖 7**：產品現在依類別排序（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)）

> [!NOTE]
> 按一下 [重新整理] 按鈕會導致資料自動重新排序，因為已停用中繼器的 view 狀態，因此會導致中繼器在每次回傳時重新系結至其資料來源。 如果您已啟用 [中繼器 s view] 狀態，變更 [排序] 下拉式清單將不會影響排序次序。 若要解決此問題，請為 [重新整理] 按鈕 `Click` 事件建立事件處理常式，並將中繼器重新系結至其資料來源（藉由呼叫 Repeater 的 `DataBind()` 方法）。

## <a name="remembering-the-sort-expression-and-direction"></a>記住排序運算式和方向

在可能發生非排序相關回傳的頁面上建立可排序的 DataList 或中繼器時，必須在回傳之間記住排序運算式和方向。 例如，假設我們已更新本教學課程中的中繼器，以包含每個產品的 [刪除] 按鈕。 當使用者按一下 [刪除] 按鈕時，我們會執行一些程式碼來刪除選取的產品，然後將資料重新系結至重複項。 如果未在回傳期間保存排序詳細資料，螢幕上顯示的資料就會還原成原始排序次序。

在本教學課程中，DropDownList 會隱含地將排序運算式和方向儲存在其檢視狀態中。 如果我們使用不同的排序介面，例如，LinkButtons 提供了各種排序選項，我們就必須小心記住在回傳之間的排序次序。 做法是將排序參數儲存在頁面的 view 狀態中，方法是在 querystring 中包含 sort 參數，或透過一些其他狀態持續性技術來完成這項作業。

本教學課程中的未來範例會探索如何在頁面 s 檢視狀態中保存排序詳細資料。

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>步驟5：將排序支援新增至使用預設分頁的 DataList

在[先前的教學](paging-report-data-in-a-datalist-or-repeater-control-cs.md)課程中，我們探討了如何使用 DataList 來執行預設分頁。 讓 s 擴充這個先前的範例，以包含排序分頁資料的能力。 一開始先開啟 [`SortingWithDefaultPaging.aspx`]，然後 `Paging.aspx` [`PagingSortingDataListRepeater`] 資料夾中的頁面。 從 [`Paging.aspx`] 頁面上，按一下 [來源] 按鈕，以查看頁面的宣告式標記。 複製選取的文字（請參閱 [圖 8]），並將它貼到 `<asp:Content>` 標記之間的 `SortingWithDefaultPaging.aspx` 宣告式標記中。

[![將 &lt;asp： Content&gt; 標記中的宣告式標記，從 default.aspx 分頁複製到 SortingWithDefaultPaging .aspx](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)

**圖 8**：將 `<asp:Content>` 標記中的宣告式標記從 `Paging.aspx` 複寫至 `SortingWithDefaultPaging.aspx` （[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image22.png)）

複製宣告式標記之後，將 `Paging.aspx` 頁 s 程式碼後置類別中的方法和屬性，複製到 `SortingWithDefaultPaging.aspx`的程式碼後置類別。 接下來，請花一點時間查看瀏覽器中的 [`SortingWithDefaultPaging.aspx`] 頁面。 它應該會呈現與 `Paging.aspx`相同的功能和外觀。

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>增強 ProductsBLL 以包含預設分頁和排序方法

在上一個教學課程中，我們在傳回 `PagedDataSource` 物件的 `ProductsBLL` 類別中建立了 `GetProductsAsPagedDataSource(pageIndex, pageSize)` 方法。 這個 `PagedDataSource` 物件已填入*所有*產品（透過 BLL 的 `GetProducts()` 方法），但系結至 DataList 時，只會顯示對應于指定*pageIndex*和*pageSize*輸入參數的記錄。

稍早在本教學課程中，我們新增了排序支援，方法是指定 ObjectDataSource s `Selecting` 事件處理常式的排序運算式。 當 ObjectDataSource 傳回可排序的物件（例如 `GetProducts()` 方法所傳回的 `ProductsDataTable`）時，這項功能就很好用。 不過，`GetProductsAsPagedDataSource` 方法所傳回的 `PagedDataSource` 物件不支援排序其內部資料來源。 相反地，我們需要先排序從 `GetProducts()` 方法傳回的結果，*然後才*將它放入 `PagedDataSource`中。

若要完成這項操作，請在 `ProductsBLL` 類別中建立新方法，`GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`。 若要排序 `GetProducts()` 方法所傳回的 `ProductsDataTable`，請指定其預設 `DataTableView`的 `Sort` 屬性：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

`GetProductsSortedAsPagedDataSource` 方法與在上一個教學課程中建立的 `GetProductsAsPagedDataSource` 方法稍有不同。 特別是，`GetProductsSortedAsPagedDataSource` 會接受額外的輸入參數 `sortExpression`，並將此值指派給 `ProductDataTable` s `DefaultView`的 `Sort` 屬性。 幾行程式碼之後，`PagedDataSource` 物件 s DataSource 會被指派 `ProductDataTable` s `DefaultView`。

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>呼叫 GetProductsSortedAsPagedDataSource 方法，並指定 SortExpression 輸入參數的值

完成 `GetProductsSortedAsPagedDataSource` 方法之後，下一步就是提供此參數的值。 `SortingWithDefaultPaging.aspx` 中的 ObjectDataSource 目前設定為呼叫 `GetProductsAsPagedDataSource` 方法，並透過它在 `SelectParameters` 集合中指定的兩個 `QueryStringParameters`傳遞兩個輸入參數。 這兩個 `QueryStringParameters` 表示 `GetProductsAsPagedDataSource` 方法 s *pageIndex*和*pageSize*參數的來源來自 `pageIndex` 和 `pageSize`的 querystring 欄位。

更新 ObjectDataSource s `SelectMethod` 屬性，使其叫用新的 `GetProductsSortedAsPagedDataSource` 方法。 然後，加入新的 `QueryStringParameter`，以便從 querystring 欄位 `sortExpression`存取*sortExpression*輸入參數。 將 `QueryStringParameter` s `DefaultValue` 設定為 [ProductName]。

這些變更之後，ObjectDataSource 的宣告式標記看起來應該像這樣：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample6.aspx)]

此時，[`SortingWithDefaultPaging.aspx`] 頁面會依產品名稱的字母順序排序其結果（請參閱 [圖 9]）。 這是因為根據預設，ProductName 的值會傳入做為 `GetProductsSortedAsPagedDataSource` 方法 s *sortExpression*參數。

[![根據預設，結果會依 ProductName 排序](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)

**圖 9**：根據預設，結果會依 `ProductName` 排序（[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)）

如果您手動加入 `sortExpression` querystring 欄位（例如 `SortingWithDefaultPaging.aspx?sortExpression=CategoryName`），結果就會依照指定的 `sortExpression`排序。 不過，在移至不同的資料頁面時，querystring 不會包含這個 `sortExpression` 參數。 事實上，按一下 [下一步] 或 [最後一頁] 按鈕會讓我們回到 `Paging.aspx`！ 此外，目前沒有排序介面。 使用者可以變更分頁資料之排序次序的唯一方式，就是直接操作 querystring。

## <a name="creating-the-sorting-interface"></a>建立排序介面

我們必須先更新 `RedirectUser` 方法，以將使用者傳送至 `SortingWithDefaultPaging.aspx` （而不是 `Paging.aspx`），並將 `sortExpression` 值包含在查詢字串中。 我們也應新增名為 `SortExpression` 屬性的唯讀頁面層級。 這個屬性類似于在上一個教學課程中建立的 `PageIndex` 和 `PageSize` 屬性，會傳回 `sortExpression` querystring 欄位的值（如果有的話），否則會傳回預設值（ProductName）。

`RedirectUser` 的方法目前只接受單一輸入參數，即要顯示的頁面索引。 不過，有時候我們會想要使用 querystring 中指定的排序運算式，將使用者重新導向至特定的資料頁面。 我們稍後會建立此頁面的排序介面，其中包含一系列的按鈕 Web 控制項，可依指定的資料行來排序資料。 當按下其中一個按鈕時，我們會想要重新導向傳遞適當排序運算式值的使用者。 若要提供這項功能，請建立兩個版本的 `RedirectUser` 方法。 第一個只應接受要顯示的頁面索引，而第二個則接受頁面索引和排序運算式。

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

在本教學課程的第一個範例中，我們使用 DropDownList 建立排序介面。 在此範例中，讓我們使用位於 DataList 一個上方的三個按鈕 Web 控制項，依 `ProductName`進行排序，一個用於 `CategoryName`，另一個用於 `SupplierName`。 新增三個按鈕 Web 控制項，適當地設定其 `ID` 和 `Text` 屬性：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample8.aspx)]

接下來，為每個建立一個 `Click` 事件處理常式。 事件處理常式應該呼叫 `RedirectUser` 方法，並使用適當的排序運算式將使用者傳回第一頁。

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

第一次造訪網頁時，資料會依產品名稱的字母順序排序（請參閱 [圖 9]）。 按 [下一步] 按鈕，前進到第二頁的資料，然後按一下 [依分類排序] 按鈕。 這會讓我們回到第一頁的資料，依類別目錄名稱排序（請參閱 [圖 10]）。 同樣地，按一下 [依供應商排序] 按鈕會根據供應商從資料的第一頁開始排序資料。 當資料經過分頁處理時，會記住排序選擇。 [圖 11] 顯示依類別排序之後的頁面，然後前進到第十三頁的資料。

[![產品依類別排序](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)

**圖 10**：產品依類別排序（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image28.png)）

[![分頁流覽資料時，會記住排序運算式](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image29.png)

**圖 11**：分頁流覽資料時，會記住排序運算式（[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image31.png)）

## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>步驟6：透過重複項中的記錄自訂分頁

DataList 範例會使用沒有效率的預設分頁技術，在步驟5頁面中檢查其資料。 當逐頁查看大量資料時，請務必使用自訂分頁。 回到有效率的[分頁處理大量資料](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)，並[排序自訂的分頁資料](../paging-and-sorting/sorting-custom-paged-data-cs.md)教學課程，我們已檢查了在使用自訂分頁和排序自訂分頁資料的 BLL 中，預設和自訂分頁與已建立方法之間的差異。 特別是在這兩個先前的教學課程中，我們將下列三種方法新增至 `ProductsBLL` 類別：

- `GetProductsPaged(startRowIndex, maximumRows)` 會傳回從*startRowIndex*開始且不超過*maximumRows*的特定記錄子集。
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` 會傳回依指定的*sortExpression*輸入參數排序之記錄的特定子集。
- `TotalNumberOfProducts()` 提供 `Products` 資料庫資料表中的記錄總數。

這些方法可用來有效率地使用 DataList 或重複項控制項來進行資料的分頁和排序。 為了說明這一點，讓我們從建立具有自訂分頁支援的中繼器控制項開始著手;接著，我們會新增排序功能。

開啟 [`PagingSortingDataListRepeater`] 資料夾中的 [`SortingWithCustomPaging.aspx`] 頁面，並在頁面中新增中繼器，將其 `ID` 屬性設定為 [`Products`]。 從 [中繼器] 智慧標籤中，建立名為 `ProductsDataSource`的新 ObjectDataSource。 將它設定為從 `ProductsBLL` 類別的 `GetProductsPaged` 方法中選取其資料。

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別的 GetProductsPaged 方法](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image32.png)

**圖 12**：設定 ObjectDataSource 使用 `ProductsBLL` 類別的 `GetProductsPaged` 方法（[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image34.png)）

將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]，然後按 [下一步] 按鈕。 [設定資料來源] wizard 現在會提示您輸入 `GetProductsPaged` 方法*startRowIndex*和*maximumRows*輸入參數的來源。 實際上，這些輸入參數會被忽略。 相反地， *startRowIndex*和*maximumRows*值會透過 ObjectDataSource s `Selecting` 事件處理常式中的 `Arguments` 屬性傳入，就像我們在本教學課程中指定*sortExpression*的第一個示範一樣。 因此，請將 wizard 中的 [參數來源] 下拉式清單保留為 [無]。

[![保持參數來源設定為 [無]](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image35.png)

**圖 13**：讓 [參數來源] 設定為 [無] （[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image37.png)）

> [!NOTE]
> 請勿將 ObjectDataSource s `EnablePaging`*屬性設為*`true`。 這會導致 ObjectDataSource 自動將自己的*startRowIndex*和*maximumRows*參數包含在 `SelectMethod` 的現有參數清單中。 將自訂分頁資料系結至 GridView、DetailsView 或 FormView 控制項時，`EnablePaging` 屬性會很有用，因為這些控制項會預期只有在 `true``EnablePaging` 屬性時，才可以使用該類型的特定行為。 因為我們必須手動新增 DataList 和中繼器的分頁支援，所以將此屬性設定為 `false` （預設值），因為我們會直接在 ASP.NET 網頁中製作所需的功能。

最後，定義中繼器 `ItemTemplate`，以便顯示產品的名稱、類別和供應商。 這些變更之後，中繼器和 ObjectDataSource 的宣告式語法看起來應該如下所示：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample10.aspx)]

請花點時間透過瀏覽器造訪頁面，並注意不會傳回任何記錄。 這是因為我們尚未指定*startRowIndex*和*maximumRows*參數值;因此，會針對兩者傳入0的值。 若要指定這些值，請建立 ObjectDataSource s `Selecting` 事件的事件處理常式，並以程式設計方式將這些參數值設定為0和5的硬式編碼值：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample11.cs)]

透過這種變更，頁面在瀏覽器中查看時，會顯示前五個產品。

[顯示前五筆記錄 ![](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image38.png)

**圖 14**：顯示前五筆記錄（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image40.png)）

> [!NOTE]
> [圖 14] 中所列的產品是依產品名稱排序，因為執行有效率的自訂分頁查詢的 `GetProductsPaged` 預存程式，會 `ProductName`來依排序結果。

為了讓使用者可以逐步執行頁面，我們必須追蹤開始列索引和最大資料列，並在回傳之間記住這些值。 在預設分頁範例中，我們使用 querystring 欄位來保存這些值;在此示範中，讓我們將這項資訊保存在頁面 s 檢視狀態。 建立下列兩個屬性：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample12.cs)]

接下來，更新選取事件處理常式中的程式碼，使其使用 `StartRowIndex` 並 `MaximumRows` 屬性，而不是硬式編碼值0和5：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample13.cs)]

此時，我們的頁面仍然只會顯示前五筆記錄。 不過，在這些屬性準備就緒之後，我們就可以開始建立分頁介面。

## <a name="adding-the-paging-interface"></a>新增分頁介面

讓我們使用預設分頁範例中使用的相同第一個、上一個、下一個、最後一個分頁介面，包括標籤 Web 控制項，可顯示要查看的資料頁，以及有多少總頁數。 在中繼器底下新增四個按鈕 Web 控制項和標籤。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample14.aspx)]

接下來，建立四個按鈕 `Click` 事件處理常式。 當按下其中一個按鈕時，我們需要更新 `StartRowIndex`，並將資料重新系結至中繼器。 [第一個]、[上一個] 和 [下一步] 按鈕的程式碼很簡單，但最後一個按鈕如何判斷最後一頁數據的開始列索引？ 若要計算此索引，以及判斷是否應該啟用 [下一步] 和 [最後一個] 按鈕，我們需要知道總共有多少筆記錄正在進行分頁。 我們可以藉由呼叫 `ProductsBLL` 類別的 `TotalNumberOfProducts()` 方法來判斷這一點。 讓 s 建立一個唯讀的頁面層級屬性，名為 `TotalRowCount`，以傳回 `TotalNumberOfProducts()` 方法的結果：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample15.cs)]

我們現在可以使用這個屬性來判斷最後一頁的開始資料列索引。 具體來說，它是 `TotalRowCount` 的整數結果減去1除以 `MaximumRows`，乘以 `MaximumRows`。 我們現在可以為四個分頁介面按鈕撰寫 `Click` 事件處理常式：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample16.cs)]

最後，當您在流覽最後一頁時，必須停用分頁介面中的第一個和上一個按鈕，而在觀看最後一頁時，則是 [下一個] 和 [最後一個] 按鈕。 若要完成這項操作，請將下列程式碼新增至 ObjectDataSource s `Selecting` 事件處理常式：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample17.cs)]

加入這些 `Click` 事件處理常式和程式碼，以根據目前的開始資料列索引來啟用或停用分頁介面元素之後，請在瀏覽器中測試頁面。 如 [圖 15] 所示，第一次造訪網頁時，會停用第一個和上一個按鈕。 按 [下一步] 會顯示第二頁的資料，而按一下 [上次] 則會顯示最後一頁（請參閱圖16和17）。 當觀看最後一頁的資料時，會停用 [下一步] 和 [最後一個] 按鈕。

[![在觀看產品的第一頁時，已停用前一個和最後一個按鈕](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image41.png)

**圖 15**：觀看產品的第一頁時，已停用上一個和最後一個按鈕（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image43.png)）

[顯示產品的第二頁 ![](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image44.png)

**圖 16**：顯示產品的第二頁（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image46.png)）

[![按一下 [上一步] 會顯示最後一頁的資料](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image47.png)

**圖 17**：按一下 [上一步] 會顯示最後一頁的資料（[按一下以查看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image49.png)）

## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>步驟7：包含使用自訂分頁中繼器的排序支援

既然自訂分頁已經完成，我們就準備好加入排序支援。 `ProductsBLL` 類別的 `GetProductsPagedAndSorted` 方法與 `GetProductsPaged`具有相同的*startRowIndex*和*maximumRows*輸入參數，但允許額外的*sortExpression*輸入參數。 若要使用 `SortingWithCustomPaging.aspx`的 `GetProductsPagedAndSorted` 方法，我們需要執行下列步驟：

1. 將 [ObjectDataSource s `SelectMethod`] 屬性從 `GetProductsPaged` 變更為 [`GetProductsPagedAndSorted`]。
2. 將*sortExpression* `Parameter` 物件新增至 ObjectDataSource s `SelectParameters` 集合。
3. 建立私用頁面層級 `SortExpression` 屬性，以透過頁面 s 檢視狀態在回傳期間保存其值。
4. 更新 ObjectDataSource s `Selecting` 事件處理常式，將頁面層級 `SortExpression` 屬性的值指派給 ObjectDataSource s *sortExpression*參數。
5. 建立排序介面。

從更新 ObjectDataSource s `SelectMethod` 屬性，並新增*sortExpression* `Parameter`開始。 請確定 [ *sortExpression* `Parameter` s `Type`] 屬性已設定為 [`String`]。 完成前兩個工作之後，ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample18.aspx)]

接下來，我們需要頁面層級 `SortExpression` 屬性，其值會序列化為 view 狀態。 如果未設定排序運算式值，請使用 ProductName 做為預設值：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample19.cs)]

在 ObjectDataSource 叫用 `GetProductsPagedAndSorted` 方法之前，我們需要將*sortExpression* `Parameter` 設定為 `SortExpression` 屬性的值。 在 `Selecting` 事件處理常式中，新增下列程式程式碼：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample20.cs)]

剩下的就是執行排序介面。 就像我們在上一個範例中所做的一樣，讓我們使用三個按鈕 Web 控制項來實作為排序介面，讓使用者依產品名稱、類別或供應商來排序結果。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample21.aspx)]

建立這三個按鈕控制項的 `Click` 事件處理常式。 在事件處理常式中，將 `StartRowIndex` 重設為0，將 `SortExpression` 設定為適當的值，並將資料重新系結至中繼器：

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample22.cs)]

這樣就大功告成了！ 雖然有幾個步驟可取得自訂分頁和排序，但這些步驟與預設分頁所需的步驟非常類似。 [圖 18] 顯示依類別目錄排序時，觀看最後一頁數據的產品。

[會顯示 ![最後一頁的資料，依分類排序](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image50.png)

**圖 18**：顯示最後一頁的資料，依分類排序（[按一下以觀看完整大小的影像](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image52.png)）

> [!NOTE]
> 在先前的範例中，由供應商廠商進行排序時，會使用做為排序運算式。 不過，針對自訂分頁執行，我們需要使用 [公司名稱]。 這是因為負責執行自訂分頁 `GetProductsPagedAndSorted` 將排序運算式傳遞至 `ROW_NUMBER()` 關鍵字的預存程式，`ROW_NUMBER()` 關鍵字需要實際的資料行名稱，而不是別名。 因此，我們必須使用 `CompanyName` （`Suppliers` 資料表中的資料行名稱），而不是排序運算式的 `SELECT` 查詢（`SupplierName`）中所使用的別名。

## <a name="summary"></a>總結

DataList 和中繼器都不提供內建的排序支援，但有一些程式碼和自訂排序介面，因此可以加入這類功能。 在執行排序（但不分頁）時，可以透過傳遞至 ObjectDataSource s `Select` 方法的 `DataSourceSelectArguments` 物件來指定排序運算式。 這個 `DataSourceSelectArguments` 物件 `SortExpression` 屬性可以在 ObjectDataSource s `Selecting` 事件處理常式中指派。

若要將排序功能加入至已提供分頁支援的 DataList 或重複項，最簡單的方法是自訂商務邏輯層，以包含接受排序運算式的方法。 這項資訊接著可以透過 ObjectDataSource s `SelectParameters`中的參數傳遞。

本教學課程使用 DataList 和重複項控制項，完成分頁和排序的檢查。 我們的下一個和最後一個教學課程將探討如何將按鈕 Web 控制項新增至 DataList 和 Repeater 的範本，以便為每個專案提供一些自訂、以使用者為基礎的功能。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者是 David Suru。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](paging-report-data-in-a-datalist-or-repeater-control-cs.md)
> [下一頁](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
