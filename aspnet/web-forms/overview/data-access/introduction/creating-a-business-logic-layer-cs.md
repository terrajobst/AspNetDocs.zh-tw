---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
title: 建立商務邏輯層（C#） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將瞭解如何將您的商務規則集中化為商業邏輯層（BLL），以作為在 t 之間交換資料的媒介。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 85554606-47cb-4e4f-9848-eed9da579056
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: df96f3e7422a0537bf1b003a33fe8d71a671ac33
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586147"
---
# <a name="creating-a-business-logic-layer-c"></a>建立商業邏輯層 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_2_CS.exe)或[下載 PDF](creating-a-business-logic-layer-cs/_static/datatutorial02cs1.pdf)

> 在本教學課程中，我們將瞭解如何將您的商務規則集中化為商業邏輯層（BLL），以做為展示層和 DAL 之間資料交換的媒介。

## <a name="introduction"></a>簡介

在[第一個教學](creating-a-data-access-layer-cs.md)課程中建立的資料存取層（DAL）會將資料存取邏輯與展示邏輯明確隔開。 不過，DAL 會將資料存取詳細資料與展示層完全分隔，而不會強制執行任何可能適用的商務規則。 例如，針對我們的應用程式，建議您在 [`Discontinued`] 欄位設定為1時，不允許修改 `Products` 資料表的 `CategoryID` 或 `SupplierID` 欄位，或者我們可能會想要強制執行資歷規則，以禁止員工被雇用之後的某人管理的情況。 另一個常見的情況是授權，可能只有特定角色的使用者可以刪除產品或變更 `UnitPrice` 值。

在本教學課程中，我們將瞭解如何將這些商務規則集中成商業邏輯層（BLL），做為展示層和 DAL 之間資料交換的媒介。 在真實世界的應用程式中，BLL 應該實作為個別的類別庫專案;不過，在這些教學課程中，我們會將 BLL 實作為 `App_Code` 資料夾中一系列的類別，以便簡化專案結構。 [圖 1] 說明展示層、BLL 和 DAL 之間的架構關聯性。

![BLL 會將展示層與資料存取層隔開，並強加商務規則](creating-a-business-logic-layer-cs/_static/image1.png)

**圖 1**： BLL 會將展示層與資料存取層隔開，並強加商務規則

## <a name="step-1-creating-the-bll-classes"></a>步驟1：建立 BLL 類別

我們的 BLL 將由四個類別組成，分別用於 DAL 中的每個 TableAdapter;這些 BLL 類別中的每一個都有方法可從 DAL 中的個別 TableAdapter 進行抓取、插入、更新和刪除，並套用適當的商務規則。

為了更明確地分隔 DAL 和 BLL 相關類別，讓我們在 `App_Code` 資料夾中建立兩個子資料夾，`DAL` 和 `BLL`。 只要以滑鼠右鍵按一下方案總管中的 [`App_Code`] 資料夾，然後選擇 [新增資料夾] 即可。 建立這兩個資料夾之後，請將第一個教學課程中建立的具類型資料集移至 `DAL` 子資料夾。

接下來，在 `BLL` 子資料夾中建立四個 BLL 類別檔案。 若要完成這項操作，請以滑鼠右鍵按一下 [`BLL`] 子資料夾，選擇 [加入新專案]，然後選擇 [類別] 範本。 將四個類別命名為 `ProductsBLL`、`CategoriesBLL`、`SuppliersBLL`和 `EmployeesBLL`。

![將四個新類別新增至 App_Code 資料夾](creating-a-business-logic-layer-cs/_static/image2.png)

**圖 2**：將四個新類別新增至 `App_Code` 資料夾

接下來，讓我們將方法新增至每個類別，以直接包裝第一個教學課程中為 Tableadapter 所定義的方法。 現在，這些方法只會直接呼叫 DAL;我們稍後會傳回以新增任何所需的商務邏輯。

> [!NOTE]
> 如果您使用 Visual Studio Standard Edition 或更新版本（也就是您*不*是使用 Visual Web Developer），您可以選擇使用[類別設計工具](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp)以視覺化方式設計您的類別。 如需 Visual Studio 中這項新功能的詳細資訊，請參閱[類別設計工具的 Blog](https://blogs.msdn.com/classdesigner/default.aspx) 。

針對 `ProductsBLL` 類別，我們需要新增總共七個方法：

- `GetProducts()` 傳回所有產品
- `GetProductByProductID(productID)` 傳回具有指定產品識別碼的產品
- `GetProductsByCategoryID(categoryID)` 傳回指定分類中的所有產品
- `GetProductsBySupplier(supplierID)` 傳回指定供應商的所有產品
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` 會使用傳入的值，將新的產品插入資料庫中。傳回新插入之記錄的 `ProductID` 值
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)` 使用傳入的值來更新資料庫中的現有產品;如果已更新精確的一個資料列，則傳回 `true`，否則為 `false`
- `DeleteProduct(productID)` 從資料庫刪除指定的產品

ProductsBLL.cs

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample1.cs)]

只傳回資料 `GetProducts`、`GetProductByProductID`、`GetProductsByCategoryID`和 `GetProductBySuppliersID` 的方法相當簡單，因為它們只是向下呼叫 DAL。 雖然在某些情況下，可能會有需要在此層級上執行的商務規則（例如以目前登入的使用者或使用者所屬的角色為基礎的授權規則），但我們只會將這些方法保持原狀。 針對這些方法，BLL 僅做為 proxy，展示層會從資料存取層存取基礎資料。

`AddProduct` 和 `UpdateProduct` 方法都會將各種產品欄位的值當做參數，並分別新增產品或更新現有的產品。 由於許多 `Product` 資料表的資料行都可以接受 `NULL` 值（`CategoryID`、`SupplierID`和 `UnitPrice`等等，因此，對應到這類資料行之 `AddProduct` 和 `UpdateProduct` 的輸入參數會使用[可為 null 的類型](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx)。 可為 null 的型別是 .NET 2.0 的新方法，並提供一種技術來指出是否應 `null`實數值型別。 在C#中，您可以藉由在型別之後加入 `?`，將實值型別標示為可為 null 的型別（例如 `int? x;`）。 如需詳細資訊，請參閱程式[ C#設計指南](https://msdn.microsoft.com/library/67ef8sbd%28VS.80%29.aspx)中的[可為 null 的類型](https://msdn.microsoft.com/library/1t3y8s4s.aspx)一節。

這三種方法都會傳回布林值，指出資料列是否已插入、更新或刪除，因為作業可能不會產生受影響的資料列。 例如，如果網頁開發人員呼叫 `DeleteProduct` 傳入不存在產品的 `ProductID`，發出到資料庫的 `DELETE` 語句就不會有任何影響，因此 `DeleteProduct` 方法會傳回 `false`。

請注意，當加入新產品或更新現有產品時，我們會將新的或修改過的產品域值視為純量的清單，而不是接受 `ProductsRow` 實例。 因為 `ProductsRow` 類別衍生自 ADO.NET `DataRow` 類別，但沒有預設的無參數函式，所以已選擇此方法。 若要建立新的 `ProductsRow` 實例，我們必須先建立 `ProductsDataTable` 實例，然後再叫用其 `NewProductRow()` 方法（我們會在 `AddProduct`中這麼做）。 當我們使用 ObjectDataSource 來插入和更新產品時，這種缺點會 rears 標頭。 簡單地說，ObjectDataSource 會嘗試建立輸入參數的實例。 如果 BLL 方法預期 `ProductsRow` 實例，ObjectDataSource 會嘗試建立一個，但因為沒有預設的無參數的函式，而導致失敗。 如需此問題的詳細資訊，請參閱下列兩個 ASP.NET 論壇文章：[使用強型別資料集更新 ObjectDataSources](https://forums.asp.net/1098630/ShowPost.aspx)，以及[ObjectDataSource 和強型別資料集的問題](https://forums.asp.net/1048212/ShowPost.aspx)。

接下來，在 `AddProduct` 和 `UpdateProduct`中，程式碼會建立 `ProductsRow` 實例，並在其中填入剛傳入的值。 將值指派給 DataColumns 的 DataRow 時，可能會發生各種欄位層級的驗證檢查。 因此，以手動方式將傳入的值放回 DataRow，有助於確保傳遞給 BLL 方法的資料有效性。 不幸的是，Visual Studio 所產生的強型別 DataRow 類別不會使用可為 null 的型別。 相反地，若要表示 DataRow 中的特定 DataColumn 應該對應至 `NULL` 資料庫值，我們必須使用 `SetColumnNameNull()` 方法。

在 `UpdateProduct` 我們會先載入產品，使用 `GetProductByProductID(productID)`進行更新。 雖然這似乎不是資料庫的不必要行程，但這項額外的旅程會在未來探索開放式平行存取的教學課程中證明值得。 開放式平行存取是一項技術，可確保同時處理相同資料的兩位使用者不會意外地覆寫另一項變更。 抓取整個記錄也能讓您更輕鬆地在 BLL 中建立更新方法，只會修改 DataRow 資料行的子集。 當我們探索 `SuppliersBLL` 類別時，我們會看到這類範例。

最後請注意，`ProductsBLL` 類別已套用[DataObject 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx)（在檔案頂端附近的 class 語句之前的 `[System.ComponentModel.DataObject]` 語法），而方法則具有[DataObjectMethodAttribute 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx)。 `DataObject` 屬性會將類別標記為適用于系結至[ObjectDataSource 控制項](https://msdn.microsoft.com/library/9a4kyhcx.aspx)的物件，而 `DataObjectMethodAttribute` 則表示方法的用途。 如我們在未來的教學課程中所見，ASP.NET 2.0 的 ObjectDataSource 可讓您輕鬆地以宣告方式從類別存取資料。 為了協助篩選在 ObjectDataSource 的 wizard 中系結的可能類別清單，根據預設，只有標示為 `DataObjects` 的類別會顯示在 wizard 的下拉式清單中。 `ProductsBLL` 類別也會在沒有這些屬性的情況下運作，但新增它們可讓您更輕鬆地在 ObjectDataSource 的 wizard 中使用。

## <a name="adding-the-other-classes"></a>新增其他類別

在 `ProductsBLL` 類別完成後，我們仍需要新增類別，以使用分類、供應商和員工。 請花點時間使用上述範例中的概念來建立下列類別和方法：

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

其中一個值得注意的方法是 `SuppliersBLL` 類別的 `UpdateSupplierAddress` 方法。 這個方法會提供介面來僅更新供應商的位址資訊。 就內部而言，這個方法會針對指定的 `supplierID` （使用 `GetSupplierBySupplierID`）讀取 `SupplierDataRow` 物件，並設定其位址相關的屬性，然後向下呼叫 `SupplierDataTable`的 `Update` 方法。 `UpdateSupplierAddress` 方法如下：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample2.cs)]

請參閱這篇文章的下載，以取得 BLL 類別的完整執行。

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>步驟2：透過 BLL 類別存取具類型的資料集

在第一個教學課程中，我們看到了以程式設計方式直接使用具型別資料集的範例，但是加入了 BLL 類別，展示層應改為針對 BLL 進行處理。 在第一個教學課程的 `AllProducts.aspx` 範例中，`ProductsTableAdapter` 是用來將產品清單系結至 GridView，如下列程式碼所示：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample3.cs)]

若要使用新的 BLL 類別，只需變更第一行程式碼就能將 `ProductsTableAdapter` 物件取代為 `ProductBLL` 物件：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample4.cs)]

您也可以使用 ObjectDataSource，以宣告方式（也可以是具類型的資料集）來存取 BLL 類別。 我們將在下列教學課程中更詳細地討論 ObjectDataSource。

[![顯示在 GridView 中的產品清單](creating-a-business-logic-layer-cs/_static/image4.png)](creating-a-business-logic-layer-cs/_static/image3.png)

**圖 3**：產品清單會顯示在 GridView 中（[按一下以觀看完整大小的影像](creating-a-business-logic-layer-cs/_static/image5.png)）

## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>步驟3：將欄位層級驗證加入至 DataRow 類別

欄位層級驗證是在插入或更新時，與商務物件的屬性值有關的檢查。 產品的部分欄位層級驗證規則包括：

- `ProductName` 欄位的長度必須是40個字元或更少
- `QuantityPerUnit` 欄位的長度必須為20個字元或更少
- [`ProductID`]、[`ProductName`] 和 [`Discontinued`] 欄位是必要的，但所有其他欄位都是選擇性的
- [`UnitPrice`]、[`UnitsInStock`]、[`UnitsOnOrder`] 和 [`ReorderLevel`] 欄位必須大於或等於零

這些規則可以和應該在資料庫層級表示。 [`ProductName`] 和 [`QuantityPerUnit`] 欄位的字元限制是由 `Products` 資料表（分別`nvarchar(40)` 和 `nvarchar(20)`）中這些資料行的資料類型所捕捉。 如果資料庫資料表資料行允許 `NULL`，則是否需要欄位，並將其表示為選擇性。 有四個[check 條件約束](https://msdn.microsoft.com/library/ms188258.aspx)可確保只有大於或等於零的值，才能將它放入 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`或 `ReorderLevel` 資料行中。

除了在資料庫中強制執行這些規則之外，也應該在資料集層級強制執行它們。 事實上，對於每個 DataTable 的 DataColumns 集，其欄位長度以及值是否為必要或選擇性。 若要查看自動提供的現有欄位層級驗證，請移至 [DataSet 設計工具]，從其中一個 Datatable 選取一個欄位，然後移至 [屬性視窗]。 如 [圖 4] 所示，`ProductsDataTable` 中的 `QuantityPerUnit` DataColumn 最大長度為20個字元，並允許 `NULL` 值。 如果我們嘗試將 `ProductsDataRow`的 `QuantityPerUnit` 屬性設定為超過20個字元的字串值，則會擲回 `ArgumentException`。

[![DataColumn 提供基本欄位層級驗證](creating-a-business-logic-layer-cs/_static/image7.png)](creating-a-business-logic-layer-cs/_static/image6.png)

**圖 4**： DataColumn 提供基本欄位層級驗證（[按一下以觀看完整大小的影像](creating-a-business-logic-layer-cs/_static/image8.png)）

可惜的是，我們無法透過屬性視窗指定界限檢查，例如 `UnitPrice` 值必須大於或等於零。 為了提供這種類型的欄位層級驗證，我們必須為 DataTable 的[ColumnChanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx)事件建立事件處理常式。 如[先前教學](creating-a-data-access-layer-cs.md)課程中所述，透過使用部分類別，可以擴充具類型資料集所建立的資料集、Datatable 和 DataRow 物件。 我們可以使用這項技術來建立 `ProductsDataTable` 類別的 `ColumnChanging` 事件處理常式。 首先，在名為 `ProductsDataTable.ColumnChanging.cs`的 `App_Code` 資料夾中建立類別。

[![將新類別新增至 [App_Code] 資料夾](creating-a-business-logic-layer-cs/_static/image10.png)](creating-a-business-logic-layer-cs/_static/image9.png)

**圖 5**：將新類別新增至 [`App_Code`] 資料夾（[按一下以查看完整大小的影像](creating-a-business-logic-layer-cs/_static/image11.png)）

接下來，建立 `ColumnChanging` 事件的事件處理常式，以確保 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` 資料行值（如果不是 `NULL`）大於或等於零。 如果任何這類資料行超出範圍，就會擲回 `ArgumentException`。

ProductsDataTable.ColumnChanging.cs

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample5.cs)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>步驟4：將自訂商務規則新增至 BLL 的類別

除了欄位層級的驗證之外，可能還有高階的自訂商務規則，其中牽涉到在單一資料行層級無法表示的不同實體或概念，例如：

- 如果產品已停止，則無法更新其 `UnitPrice`
- 員工的居住國家/地區必須與其居住的經理國家/地區相同
- 如果產品是供應商所提供的唯一產品，則無法中止

BLL 類別應該包含檢查，以確保遵守應用程式的商務規則。 這些檢查可以直接加入至它們所套用的方法。

假設我們的商務規則規定，如果產品是來自給定供應商的唯一產品，就無法標示為已停止。 也就是說，如果產品*X*是我們從供應商*Y*購買的唯一產品，我們就無法將*X*標示為已中止;不過，如果供應商*Y*提供了三項產品： *A*、 *B*和*C*，則我們可以將任何和全部標示為已中止。 奇數的商務規則，但商務規則和共同意義不一定一致！

若要在 `UpdateProducts` 方法中強制執行此商務規則，我們會先檢查 `Discontinued` 是否設定為 `true`，如果是，我們會呼叫 `GetProductsBySupplierID` 來判斷我們向此產品供應商購買的產品數量。 如果只有一個產品向此供應商購買，我們會擲回 `ApplicationException`。

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample6.cs)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>回應展示層中的驗證錯誤

從展示層呼叫 BLL 時，我們可以決定是否嘗試處理可能引發的任何例外狀況，或讓它們向上反升至 ASP.NET （這會引發 `HttpApplication`的 `Error` 事件）。 若要在以程式設計方式使用 BLL 時處理例外狀況，我們可以使用[try .。。catch](https://msdn.microsoft.com/library/0yd65esw.aspx)區塊，如下列範例所示：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample7.cs)]

如我們在未來的教學課程中所見，當使用資料 Web 控制項來插入、更新或刪除資料時，可以直接在事件處理常式中處理從 BLL 中反升的例外狀況，而不需要將程式碼包裝在 `try...catch` 區塊中。

## <a name="summary"></a>總結

架構完善的應用程式會建立成不同的層級，每個階層都會封裝特定的角色。 在此文章系列的第一個教學課程中，我們使用具類型的資料集建立了資料存取層;在本教學課程中，我們將商務邏輯層建立為應用程式 `App_Code` 資料夾中一系列的類別，以向下呼叫 DAL。 BLL 會為我們的應用程式執列欄位層級和商務層級邏輯。 除了建立個別的 BLL，如同我們在本教學課程中所做的，另一個選項是透過使用部分類別來擴充 Tableadapter 的方法。 不過，使用這項技術並不允許我們覆寫現有的方法，也不會將 DAL 和我們的 BLL 與我們在本文中所採取的方法完全分開。

當 DAL 和 BLL 完成後，我們就可以開始使用我們的展示層。 在[下一個教學](master-pages-and-site-navigation-cs.md)課程中，我們將從資料存取主題中取得簡短的繞道，並定義一致的頁面配置，以便在整個教學課程中使用。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Liz Shulok、Dennis Patterson、Carlos Santos 和 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](creating-a-data-access-layer-cs.md)
> [下一頁](master-pages-and-site-navigation-cs.md)
