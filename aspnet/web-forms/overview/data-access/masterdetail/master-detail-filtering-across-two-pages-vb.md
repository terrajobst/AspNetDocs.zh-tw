---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: 跨兩個頁面的主要/詳細資料篩選（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將使用 GridView 來列出資料庫中的供應商，以執行這種模式。 GridView 中的每個供應商資料列將包含檢視表 w 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 252c6d5e48aff0087e090e3ddc1f58c84a2c030e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74622885"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>跨兩個頁面進行主要/詳細資料篩選 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe)或[下載 PDF](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> 在本教學課程中，我們將使用 GridView 來列出資料庫中的供應商，以執行這種模式。 GridView 中的每個供應商資料列都會包含 View Products 連結，當您按下時，就會將使用者帶到列出所選供應商產品的個別頁面。

## <a name="introduction"></a>簡介

在前兩個教學課程中，我們已瞭解如何在單一網頁中顯示主要/詳細資料包表，方法是使用 Dropdownlist 進行來顯示「主要」記錄和[GridView](master-detail-filtering-with-a-dropdownlist-vb.md)或[DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md)控制項，以顯示 [詳細資料]。 主要/詳細資料包表使用的另一個常見模式是在一個網頁上擁有主要記錄，並在另一個頁面上顯示詳細資料。 論壇網站（如[ASP.NET 論壇](https://forums.asp.net/)）是此模式的絕佳範例。 ASP.NET 論壇包含各種論壇消費者入門、Web form、資料簡報控制項等等。 每個論壇都是由許多執行緒組成，而每個執行緒都是由幾篇文章所組成。 在 ASP.NET 論壇首頁上，會列出論壇。 按一下論壇會 whisks 您前往 `ShowForum.aspx` 頁面，其中會列出該論壇的往來文章。 同樣地，按一下執行緒會帶您前往 `ShowPost.aspx`，這會顯示已按下之執行緒的貼文。

在本教學課程中，我們將使用 GridView 來列出資料庫中的供應商，以執行這種模式。 GridView 中的每個供應商資料列都會包含 View Products 連結，當您按下時，就會將使用者帶到列出所選供應商產品的個別頁面。

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>步驟1：將`SupplierListMaster.aspx`和`ProductsForSupplierDetails.aspx`頁面新增至`Filtering`資料夾

在第三個教學課程中定義頁面配置時，我們在 [`BasicReporting`]、[`Filtering`] 和 [`CustomFormatting`] 資料夾中新增了一些「入門」頁面。 不過，我們目前並未新增本教學課程的起始頁，因此請花點時間將兩個新頁面新增至 `Filtering` 資料夾： `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx`。 `SupplierListMaster.aspx` 將會列出「主要」記錄（供應商），而 `ProductsForSupplierDetails.aspx` 會顯示所選供應商的產品。

建立這兩個新的頁面時，請務必將它們與 `Site.master` 主版頁面建立關聯。

![將 SupplierListMaster 和 ProductsForSupplierDetails 頁面新增至篩選資料夾](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**圖 1**：將 [`SupplierListMaster.aspx`] 和 [`ProductsForSupplierDetails.aspx`] 頁面新增至 [`Filtering`] 資料夾

此外，將新頁面新增至專案時，請務必更新網站地圖檔案，`Web.sitemap`。 在本教學課程中，只需使用下列 XML 內容，將 [`SupplierListMaster.aspx`] 頁面新增至網站地圖，做為篩選報告 `<siteMapNode>` 元素的子系：

[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> 使用[K. Scott Allen](http://odetocode.com/Blogs/scott/)的免費 Visual Studio[網站地圖宏](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)來加入新的 ASP.NET 網頁時，您可以協助將更新網站地圖檔案的程式自動化。

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>步驟2：在`SupplierListMaster.aspx` 中顯示供應商清單

建立 `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx` 頁面後，下一個步驟是在 `SupplierListMaster.aspx`中建立供應商的 GridView。 將 GridView 新增至頁面，並將它系結至新的 ObjectDataSource。 這個 ObjectDataSource 應該使用 `SuppliersBLL` 類別的 `GetSuppliers()` 方法來傳回所有供應商。

[![選取 SuppliersBLL 類別](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**圖 2**：選取 [`SuppliersBLL`] 類別（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image4.png)）

[![將 ObjectDataSource 設定為使用 GetSuppliers （）方法](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**圖 3**：設定 ObjectDataSource 以使用 `GetSuppliers()` 方法（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image7.png)）

我們需要在每個 GridView 資料列中加入一個標題為 View Products 的連結，當按下時，就會透過 querystring 讓使用者 `ProductsForSupplierDetails.aspx` 傳入所選資料列的 `SupplierID` 值。 例如，如果使用者針對東京貿易供應商（其 `SupplierID` 值為4）按一下 [View Products] 連結，則應該將它們傳送至 `ProductsForSupplierDetails.aspx?SupplierID=4`。

若要完成這項操作，請將[HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx)加入 gridview，這會將超連結加入至每個 gridview 資料列。 從 GridView 的智慧標籤按一下 [編輯資料行] 連結開始。 接下來，從左上方的清單中選取 HyperLinkField，然後按一下 [新增] 以在 GridView 的欄位清單中包含 HyperLinkField。

[![將 HyperLinkField 新增至 GridView](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**圖 4**：將 HyperLinkField 新增至 GridView （[按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image10.png)）

HyperLinkField 可以設定為使用相同的文字或 URL 值，每個 GridView 資料列中的連結，或者可以根據系結至每個特定資料列的資料值來做為這些值的依據。 若要在所有資料列上指定靜態值，請使用 HyperLinkField 的 `Text` 或 `NavigateUrl` 屬性。 因為我們希望所有資料列的連結文字都相同，所以請將 HyperLinkField 的 `Text` 屬性設定為 [View Products] （產品）。

[![設定 HyperLinkField 的 Text 屬性以查看產品](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**圖 5**：將 HyperLinkField 的 `Text` 屬性設定為可觀看產品（[按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image13.png)）

若要將文字或 URL 值設定為根據系結至 GridView 資料列的基礎資料，請在 [`DataTextField`] 或 [`DataNavigateUrlFields` 屬性] 中指定要從中提取文字或 URL 值的資料欄位。 `DataTextField` 只能設定為單一資料欄位;不過，`DataNavigateUrlFields`可以設定為以逗號分隔的資料欄位清單。 我們經常需要以目前資料列的資料欄值和一些靜態標記的組合做為文字或 URL 的基礎。 例如，在本教學課程中，我們想要 `ProductsForSupplierDetails.aspx?SupplierID=supplierID`HyperLinkField 連結的 URL，其中 *`supplierID`* 是每個 GridView 的 row's `SupplierID` 值。 請注意，這裡需要靜態和資料驅動的值：連結 URL 的 `ProductsForSupplierDetails.aspx?SupplierID=` 部分是靜態的，而 *`supplierID`* 部分則是資料驅動的，因為它的值是每個資料列本身的 `SupplierID` 值。

若要指示靜態和資料驅動值的組合，請使用 `DataTextFormatString` 並 `DataNavigateUrlFormatString` 屬性。 在這些屬性中，視需要輸入靜態標記，然後使用標記 `{0}` 您想要在 [`DataTextField`] 或 [`DataNavigateUrlFields` 屬性] 中指定的欄位值出現。 如果 `DataNavigateUrlFields` 屬性已指定多個欄位，請使用 `{0}` 您想要插入的第一個域值，`{1}` 作為第二個域值，依此類推。

將此套用到我們的教學課程時，我們必須將 `DataNavigateUrlFields` 屬性設為 `SupplierID`，因為這是我們需要以每個資料列為基礎自訂之值的資料欄位，以及要 `ProductsForSupplierDetails.aspx?SupplierID={0}`的 `DataNavigateUrlFormatString` 屬性。

[![將 HyperLinkField 設定為根據建立的供應商包含適當的連結 URL](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**圖 6**：設定 HyperLinkField 以根據 `SupplierID` 包含適當的連結 URL （[按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image16.png)）

加入 HyperLinkField 之後，您可以隨意自訂並重新排列 GridView 的欄位。 當我進行一些次要欄位層級自訂之後，下列標記會顯示 GridView。

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

請花點時間透過瀏覽器來觀看 `SupplierListMaster.aspx` 頁面。 如 [圖 7] 所示，此頁面目前列出所有供應商，包括 [View Products] 連結。 按一下 [View Products] 連結將會帶您前往 `ProductsForSupplierDetails.aspx`，並在查詢字串中傳遞供應商的 `SupplierID`。

[![每個供應商資料列都包含 View Products 連結](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**圖 7**：每個供應商資料列都包含 [view Products] 連結（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image19.png)）

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>步驟3：在`ProductsForSupplierDetails.aspx` 中列出供應商的產品

此時，`SupplierListMaster.aspx` 頁面會將使用者傳送至 `ProductsForSupplierDetails.aspx`，並在 querystring 中傳遞所選供應商的 `SupplierID`。 本教學課程的最後一個步驟是在 `ProductsForSupplierDetails.aspx` 中顯示 GridView 中的產品，其 `SupplierID` 等於透過 querystring 傳遞的 `SupplierID`。 若要完成這項工作，請先使用名為 `ProductsBySupplierDataSource` 的新 ObjectDataSource 控制項，從 `ProductsBLL` 類別叫用 `GetProductsBySupplierID(supplierID)` 方法，以將 GridView 加入至 `ProductsForSupplierDetails.aspx` 頁面。

[![新增名為 ProductsBySupplierDataSource 的新 ObjectDataSource](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**圖 8**：新增名為 `ProductsBySupplierDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image22.png)）

[![選取 ProductsBLL 類別](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**圖 9**：選取 [`ProductsBLL`] 類別（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image25.png)）

[![讓 ObjectDataSource 叫用 GetProductsBySupplierID （的「已供應商）方法](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**圖 10**：讓 ObjectDataSource 叫用 `GetProductsBySupplierID(supplierID)` 方法（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image28.png)）

[設定資料來源] 嚮導的最後一個步驟會要求我們提供 `GetProductsBySupplierID(supplierID)` 方法 *`supplierID`* 參數的來源。 若要使用 querystring 值，請將參數來源設定為 QueryString，並在 [QueryStringField] 文字方塊中輸入要使用之 querystring 值的名稱（`SupplierID`）。

[![填入來自于 [已的] 參數字串值](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**圖 11**：填入來自 `SupplierID` Querystring 值的 *`supplierID`* 參數值（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image31.png)）

這樣就全部完成了！ [圖 12] 從 `SupplierListMaster.aspx`按一下 [東京貿易] 連結來顯示 [`ProductsForSupplierDetails.aspx`] 頁面。

[![會顯示東京貿易所提供的產品](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**圖 12**：顯示東京商貿所提供的產品（[按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image34.png)）

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>在`ProductsForSupplierDetails.aspx` 中顯示供應商資訊

如 [圖 12] 所示，[`ProductsForSupplierDetails.aspx`] 頁面只會列出查詢字串中所指定之 `SupplierID` 所提供的產品。 不過，直接傳送到此頁面的人不知道 [圖 12] 顯示東京貿易的產品。 若要解決此問題，我們也可以在此頁面中顯示供應商資訊。

首先，在 [products] GridView 上方新增 FormView。 建立名為 `SuppliersDataSource` 的新 ObjectDataSource 控制項，以叫用 `SuppliersBLL` 類別的 `GetSupplierBySupplierID(supplierID)` 方法。

[![選取 SuppliersBLL 類別](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**圖 13**：選取 [`SuppliersBLL`] 類別（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image37.png)）

[![讓 ObjectDataSource 叫用 GetSupplierBySupplierID （的「已供應商）方法](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**圖 14**：讓 ObjectDataSource 叫用 `GetSupplierBySupplierID(supplierID)` 方法（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image40.png)）

如同 `ProductsBySupplierDataSource`，請 *`supplierID`* 參數指派 `SupplierID` querystring 值的值。

[![填入來自于 [已的] 參數字串值](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**圖 15**：填入來自 `SupplierID` Querystring 值的 *`supplierID`* 參數值（[按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image43.png)）

將 FormView 系結至設計檢視中的 ObjectDataSource 時，Visual Studio 會自動為 ObjectDataSource 所傳回的每個資料欄位建立 FormView 的 `ItemTemplate`、`InsertItemTemplate`和 `EditItemTemplate` 以及標籤和 TextBox Web 控制項。 因為我們只想要顯示供應商資訊，所以請隨意移除 `InsertItemTemplate` 和 `EditItemTemplate`。 接著，編輯 ItemTemplate，使其在 [`<h3>`] 專案中顯示供應商的公司名稱，並在 [公司名稱] 下方的 [位址]、[城市]、[國家] 和 [電話號碼]。 或者，您也可以手動設定 FormView 的 `DataSourceID` 並建立 `ItemTemplate` 標記，如同我們在「[使用 ObjectDataSource 顯示資料](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)」教學課程中所做的一樣。

在這些編輯之後，FormView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

[圖 16] 顯示已包含上述的供應商資訊之後，[`ProductsForSupplierDetails.aspx`] 頁面的螢幕擷取畫面。

[![產品清單包含供應商的相關摘要](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**圖 16**：產品清單包含供應商的摘要（[按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image46.png)）

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>為`ProductsForSupplierDetails.aspx`UI 套用最後的潤色

若要改善此報表的使用者體驗，我們應該對 [`ProductsForSupplierDetails.aspx`] 頁面進行幾項新增。 使用者目前唯一可以從 [`ProductsForSupplierDetails.aspx`] 頁面移回供應商清單的方式，是按一下其瀏覽器的 [上一頁] 按鈕。 讓我們將超連結控制項新增至連結回到 `SupplierListMaster.aspx`的 [`ProductsForSupplierDetails.aspx`] 頁面，以提供另一種方法讓使用者回到主要清單。

[![新增超連結控制項，讓使用者回到 SupplierListMaster .aspx](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**圖 17**：新增超連結控制項，讓使用者回到 `SupplierListMaster.aspx` （[按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image49.png)）

如果使用者針對沒有任何產品的供應商按一下 [View Products] 連結，`ProductsForSupplierDetails.aspx` 中的 `ProductsBySupplierDataSource` ObjectDataSource 就不會傳回任何結果。 系結至 ObjectDataSource 的 GridView 不會在使用者的瀏覽器中呈現頁面上產生空白區域的任何標記。 為了更清楚地向使用者傳達沒有與所選供應商相關聯的產品，我們可以將 GridView 的 `EmptyDataText` 屬性設定為要在發生這種情況時顯示的訊息。 我已將此屬性設定為「沒有此供應商提供的產品」

根據預設，Northwinds 資料庫中的所有供應商至少會提供一項產品。 不過，在本教學課程中，我手動修改了 `Products` 的資料表，讓供應商 Escargots Nouveaux 不再與任何產品相關聯。 [圖 18] 顯示在進行此變更之後 Escargots Nouveaux 的詳細資料頁面。

[![使用者會收到通知，表示供應商未提供任何產品](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**圖 18**：通知使用者供應商未提供任何產品（[按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image52.png)）

## <a name="summary"></a>總結

雖然主要/詳細資料包表可以在單一頁面上顯示主要和詳細資料記錄，但在許多網站中，它們會分成兩個網頁。 在本教學課程中，我們探討了如何在「主要」網頁的 GridView 中列出供應商，以及在 [詳細資料] 頁面中列出相關聯的產品，以執行這類主要/詳細報告。 主要網頁中的每個供應商資料列都包含以資料列的 `SupplierID` 值傳遞之詳細資料頁面的連結。 您可以使用 GridView 的 HyperLinkField 輕鬆地加入這類資料列特定連結。

在詳細資料頁面中，藉由叫用 `ProductsBLL` 類別的 `GetProductsBySupplierID(supplierID)` 方法，來為指定的供應商抓取這些產品。 *`supplierID`* 參數值是使用 querystring 當做參數來源以宣告方式指定。 我們也探討了如何使用 FormView 在詳細資料頁面中顯示供應商詳細資料。

我們的[下一個教學](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)課程是主要/詳細資料包告上的最後一個教學課程。 我們將探討如何在 GridView 中顯示產品清單，其中每個資料列都有 [選取] 按鈕。 按一下 [選取] 按鈕，將會在相同頁面上的 DetailsView 控制項中顯示該產品的詳細資料。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](master-detail-filtering-with-two-dropdownlists-vb.md)
> [下一頁](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
