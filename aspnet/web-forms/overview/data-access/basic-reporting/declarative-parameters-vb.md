---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
title: 宣告式參數（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將說明如何使用設定為硬式編碼值的參數，以選取要在 DetailsView 控制項中顯示的資料。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: dc1234a3-114f-4c9a-8d25-50ca03cc8e8e
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
msc.type: authoredcontent
ms.openlocfilehash: cdc42752fc78d18366af037a81fe4ebe5a1646ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597136"
---
# <a name="declarative-parameters-vb"></a>宣告式參數 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_5_VB.exe)或[下載 PDF](declarative-parameters-vb/_static/datatutorial05vb1.pdf)

> 在本教學課程中，我們將說明如何使用設定為硬式編碼值的參數，以選取要在 DetailsView 控制項中顯示的資料。

## <a name="introduction"></a>簡介

在[上一個教學](displaying-data-with-the-objectdatasource-vb.md)課程中，我們探討了如何使用 GridView、DetailsView 和 FormView 控制項（系結至從 `ProductsBLL` 類別叫用 `GetProducts()` 方法的 ObjectDataSource 控制項）來顯示資料。 `GetProducts()` 方法會傳回已填入 Northwind 資料庫之 `Products` 資料表中所有記錄的強型別 DataTable。 `ProductsBLL` 類別包含的其他方法，只會傳回產品的子集-`GetProductByProductID(productID)`、`GetProductsByCategoryID(categoryID)`和 `GetProductsBySupplierID(supplierID)`。 這三種方法預期會有一個輸入參數，指出如何篩選傳回的產品資訊。

ObjectDataSource 可以用來叫用預期輸入參數的方法，但為了這麼做，我們必須指定這些參數的值來自何處。 參數值可以硬式編碼，也可以來自各種動態來源，包括： querystring 值、會話變數、網頁上 Web 控制項的屬性值，或其他專案。

在本教學課程中，讓我們先說明如何使用設定為硬式編碼值的參數。 具體而言，我們將探討如何將 DetailsView 新增至頁面，以顯示特定產品的相關資訊，亦即 Chef Anton 的 Gumbo Mix，其 `ProductID` 為5。 接下來，我們將瞭解如何根據 Web 控制項設定參數值。 特別是，我們將使用 TextBox 讓使用者輸入國家/地區，然後按一下按鈕即可查看位於該國家/地區的供應商清單。

## <a name="using-a-hard-coded-parameter-value"></a>使用硬式編碼的參數值

針對第一個範例，請從將 DetailsView 控制項新增至 [`BasicReporting`] 資料夾中的 [`DeclarativeParams.aspx`] 頁面開始。 從 DetailsView 的智慧標籤中，選取下拉式清單中的 [&lt;新增資料來源&gt;]，然後加入宣告 ObjectDataSource。

[![將 ObjectDataSource 新增至頁面](declarative-parameters-vb/_static/image2.png)](declarative-parameters-vb/_static/image1.png)

**圖 1**：將 ObjectDataSource 新增至頁面（[按一下以查看完整大小的影像](declarative-parameters-vb/_static/image3.png)）

這會自動啟動 ObjectDataSource 控制項的 [選擇資料來源]。 從嚮導的第一個畫面中選取 [`ProductsBLL`] 類別。

[![選取 ProductsBLL 類別](declarative-parameters-vb/_static/image5.png)](declarative-parameters-vb/_static/image4.png)

**圖 2**：選取 [`ProductsBLL`] 類別（[按一下以查看完整大小的影像](declarative-parameters-vb/_static/image6.png)）

因為我們想要顯示特定產品的相關資訊，所以我們想要使用 `GetProductByProductID(productID)` 方法。

[![選擇 GetProductByProductID （productID）方法](declarative-parameters-vb/_static/image8.png)](declarative-parameters-vb/_static/image7.png)

**圖 3**：選擇 [`GetProductByProductID(productID)`] 方法（[按一下以查看完整大小的影像](declarative-parameters-vb/_static/image9.png)）

因為我們選取的方法包含參數，所以會有一個畫面供 wizard 使用，而我們會要求您定義要用於參數的值。 左邊的清單會顯示所選方法的所有參數。 `GetProductByProductID(productID)` 只有一個 `productID`。 在右側，我們可以指定所選取參數的值。 [參數來源] 下拉式清單會列舉參數值的各種可能來源。 因為我們想要為 `productID` 參數指定硬式編碼的值5，請將參數來源保留為 [無]，並在 [DefaultValue] 文字方塊中輸入5。

[![硬式編碼參數值5將用於 productID 參數](declarative-parameters-vb/_static/image11.png)](declarative-parameters-vb/_static/image10.png)

**圖 4**：以硬式編碼的參數值5將用於 `productID` 參數（[按一下以查看完整大小的影像](declarative-parameters-vb/_static/image12.png)）

完成 [設定資料來源] wizard 之後，ObjectDataSource 控制項的宣告式標記會在 `SelectParameters` 集合中，針對 `SelectMethod` 屬性中定義的方法所預期的每個輸入參數，包含一個 `Parameter` 物件。 因為我們在此範例中使用的方法只需要單一輸入參數，`parameterID`，所以這裡只有一個專案。 `SelectParameters` 集合可以包含從 `System.Web.UI.WebControls` 命名空間中的 `Parameter` 類別衍生的任何類別。 針對硬式編碼參數值，會使用基底 `Parameter` 類別，但針對其他參數來源選項，則會使用衍生的 `Parameter` 類別;如有需要，您也可以建立自己的[自訂參數類型](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11)。

[!code-aspx[Main](declarative-parameters-vb/samples/sample1.aspx)]

> [!NOTE]
> 如果您在自己的電腦上執行，此時您看到的宣告式標記可能包括 `InsertMethod`、`UpdateMethod`和 `DeleteMethod` 屬性的值，以及 `DeleteParameters`。 ObjectDataSource 的 [選擇資料來源] 嚮導會自動指定 `ProductBLL` 中用來進行插入、更新和刪除的方法，因此除非您明確地清除它們，否則會將它們包含在上述標記中。

流覽此頁面時，資料 Web 控制項將會叫用 ObjectDataSource 的 `Select` 方法，這會針對 `productID` 輸入參數，使用硬式編碼值5來呼叫 `ProductsBLL` 類別的 `GetProductByProductID(productID)` 方法。 方法會傳回強型別 `ProductDataTable` 物件，其中包含單一資料列，其中含有 Chef Anton 的 Gumbo 混合（產品具有 `ProductID` 5）的相關資訊。

[會顯示 Chef Anton 的 Gumbo 混合 ![相關資訊](declarative-parameters-vb/_static/image14.png)](declarative-parameters-vb/_static/image13.png)

**圖 5**：顯示 Chef Anton 的 Gumbo 混合相關資訊（[按一下以觀看完整大小的影像](declarative-parameters-vb/_static/image15.png)）

## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>將參數值設定為 Web 控制項的屬性值

您也可以根據頁面上 Web 控制項的值來設定 ObjectDataSource 的參數值。 為了說明這一點，讓我們有一個 GridView，其中列出的所有供應商都位於使用者所指定的國家/地區。 若要完成這項工作，請先將 TextBox 新增至使用者可以在其中輸入國家/地區名稱的頁面。 將此 TextBox 控制項的 `ID` 屬性設定為 [`CountryName`]。 同時新增按鈕 Web 控制項。

[![將文字方塊新增至識別碼為 CountryName 的頁面](declarative-parameters-vb/_static/image17.png)](declarative-parameters-vb/_static/image16.png)

**圖 6**：使用 `ID` `CountryName` 在頁面中新增文字方塊（[按一下以觀看完整大小的影像](declarative-parameters-vb/_static/image18.png)）

接下來，將 GridView 新增至頁面，並從智慧標籤中加入宣告新的 ObjectDataSource。 因為我們想要顯示供應商資訊，請從嚮導的第一個畫面中選取 [`SuppliersBLL`] 類別。 從第二個畫面中，挑選 `GetSuppliersByCountry(country)` 方法。

[![選擇 GetSuppliersByCountry （國家）方法](declarative-parameters-vb/_static/image20.png)](declarative-parameters-vb/_static/image19.png)

**圖 7**：選擇 [`GetSuppliersByCountry(country)`] 方法（[按一下以查看完整大小的影像](declarative-parameters-vb/_static/image21.png)）

由於 `GetSuppliersByCountry(country)` 方法具有輸入參數，因此 wizard 再次包含選擇參數值的最後一個畫面。 這次，請將參數來源設定為 [控制]。 這會在 [ControlID] 下拉式清單中填入頁面上的控制項名稱;從清單中選取 [`CountryName`] 控制項。 第一次造訪網頁時，`CountryName` TextBox 會是空白的，因此不會傳回任何結果，也不會顯示任何內容。 如果您想要依預設顯示某些結果，請據以設定 [DefaultValue] 文字方塊。

[![將參數值設定為 CountryName 控制項值](declarative-parameters-vb/_static/image23.png)](declarative-parameters-vb/_static/image22.png)

**圖 8**：將參數值設定為 `CountryName` 控制項值（[按一下以查看完整大小的影像](declarative-parameters-vb/_static/image24.png)）

ObjectDataSource 的宣告式標記與我們的第一個範例稍有不同，而是使用[ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx) ，而不是標準 `Parameter` 物件。 `ControlParameter` 具有額外的屬性，可指定 Web 控制項的 `ID`，以及用於參數的屬性值（`PropertyName`）。 [設定資料來源] wizard 非常聰明，可判斷文字方塊中，我們可能會想要使用參數值的 [`Text`] 屬性。 不過，如果您想要從 Web 控制項使用不同的屬性值，您可以在此變更 `PropertyName` 值，或按一下 wizard 中的 [顯示 advanced properties] 連結。

[!code-aspx[Main](declarative-parameters-vb/samples/sample2.aspx)]

第一次流覽頁面時，[`CountryName`] 文字方塊是空的。 ObjectDataSource 的 `Select` 方法仍由 GridView 叫用，但 `Nothing` 的值會傳遞至 `GetSuppliersByCountry(country)` 方法。 TableAdapter 會將 `Nothing` 轉換成資料庫 `NULL` 值（`DBNull.Value`），但是 `GetSuppliersByCountry(country)` 方法所使用的查詢會被寫入，讓 `NULL` 參數的 `@CategoryID` 值指定時，不會傳回任何值。 簡言之，不會傳回任何供應商。

但是一旦訪客進入某個國家/地區，然後按一下 [顯示供應商] 按鈕以進行回傳，就會重新查詢 ObjectDataSource 的 `Select` 方法，並傳入 TextBox 控制項的 `Text` 值做為 `country` 參數。

[顯示來自加拿大的供應商 ![](declarative-parameters-vb/_static/image26.png)](declarative-parameters-vb/_static/image25.png)

**圖 9**：顯示來自加拿大的供應商（[按一下以觀看完整大小的影像](declarative-parameters-vb/_static/image27.png)）

## <a name="showing-all-suppliers-by-default"></a>預設顯示所有供應商

我們可能會想要先顯示*所有*供應商，而不是顯示任何供應商，而是在文字方塊中輸入國家/地區名稱，讓使用者向下削減清單。 當文字方塊是空的時，`SuppliersBLL` 類別的 `GetSuppliersByCountry(country)` 方法會在其 *`country`* 輸入參數的 `Nothing` 中傳遞。 這個 `Nothing` 值接著會向下傳遞至 DAL 的 `GetSupplierByCountry(country)` 方法，其中會將它轉譯成下列查詢中 `@Country` 參數的資料庫 `NULL` 值：

[!code-sql[Main](declarative-parameters-vb/samples/sample3.sql)]

運算式 `Country = NULL` 一律會傳回 False，即使是 `Country` 的資料行具有 `NULL` 值的記錄也一樣。因此，不會傳回任何記錄。

若要在 [國家/地區] 文字方塊空白時傳回*所有*供應商，我們可以在 BLL 中增加 `GetSuppliersByCountry(country)` 方法，以在 `Nothing` country 參數時叫用 `GetSuppliers()` 方法，否則呼叫 DAL 的 `GetSuppliersByCountry(country)` 方法。 當您未指定任何國家/地區，且包含 country 參數時，這會有傳回所有供應商的效果。

將 `SuppliersBLL` 類別中的 `GetSuppliersByCountry(country)` 方法變更為下列內容：

[!code-vb[Main](declarative-parameters-vb/samples/sample4.vb)]

使用這項變更時，[`DeclarativeParams.aspx`] 頁面會顯示第一次造訪時的所有供應商（或每次 [`CountryName`] 文字方塊是空的）。

[![現在預設會顯示所有供應商](declarative-parameters-vb/_static/image29.png)](declarative-parameters-vb/_static/image28.png)

**圖 10**：現在預設會顯示所有供應商（[按一下以觀看完整大小的影像](declarative-parameters-vb/_static/image30.png)）

## <a name="summary"></a>總結

若要使用具有輸入參數的方法，我們必須在 ObjectDataSource 的 `SelectParameters` 集合中指定參數的值。 不同類型的參數允許從不同的來源取得參數值。 預設參數類型會使用硬式編碼的值，但如同簡單（而且不含一行程式碼），參數值可以從 querystring、會話變數、cookie，甚至是使用者輸入的值，從頁面上的 Web 控制項取得。

我們在本教學課程中探討的範例說明如何使用宣告式參數值。 不過，有時候我們可能需要使用無法使用的參數來源，例如目前的日期和時間，或者，如果我們的網站使用的是成員資格，則是訪客的使用者識別碼。 在這種情況下，我們可以在 ObjectDataSource 叫用其基礎物件的方法之前，以程式設計方式設定參數值。 我們會在[下一個教學](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)課程中瞭解如何完成這項操作。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](displaying-data-with-the-objectdatasource-vb.md)
> [下一頁](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)
