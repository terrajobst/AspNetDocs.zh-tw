---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
title: DataList 或重複項控制項中的分頁報表資料C#（） |Microsoft Docs
author: rick-anderson
description: 雖然 DataList 和中繼器都不會提供自動分頁或排序支援，但本教學課程會示範如何將分頁支援新增至 DataList 或中繼器,。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: e8e0809b-25c4-4c3b-8d12-9a17048148ae
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 16686c7e41926698c0da9c60d3cf26e858f5daca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78620635"
---
# <a name="paging-report-data-in-a-datalist-or-repeater-control-c"></a>DataList 或重複項控制項中的分頁報表資料 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_CS.exe)或[下載 PDF](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial44cs1.pdf)

> 雖然 DataList 和中繼器都不會提供自動分頁或排序支援，但本教學課程會示範如何將分頁支援加入至 DataList 或重複項，以提供更有彈性的分頁和資料顯示介面。

## <a name="introduction"></a>簡介

分頁和排序是在線上應用程式中顯示資料時的兩個很常見的功能。 例如，搜尋線上書店的 ASP.NET 書籍時，可能會有數百份這類書籍，但列出搜尋結果的報表只會列出每頁十個相符專案。 此外，結果也可以依標題、價格、頁面計數、作者姓名等等排序。 如我們在[分頁和排序報表資料](../paging-and-sorting/paging-and-sorting-report-data-cs.md)教學課程中所討論，GridView、DetailsView 和 FormView 控制項全都提供內建的分頁支援，可在核取方塊的滴答處啟用。 GridView 也包含排序支援。

可惜的是，DataList 和中繼器都不會提供自動分頁或排序支援。 在本教學課程中，我們將探討如何將分頁支援新增至 DataList 或中繼器。 我們必須手動建立分頁介面、顯示適當的記錄頁面，並記住跨回傳流覽的頁面。 雖然這會花費比 GridView、DetailsView 或 FormView 更多的時間和程式碼，但 DataList 和中繼器可以提供更有彈性的分頁和資料顯示介面。

> [!NOTE]
> 本教學課程僅著重于分頁。 在下一個教學課程中，我們將重點放在新增排序功能。

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>步驟1：新增分頁和排序教學課程網頁

開始進行本教學課程之前，先花點時間新增本教學課程所需的 ASP.NET 網頁，以及下一頁。 首先，在名為 `PagingSortingDataListRepeater`的專案中建立新的資料夾。 接下來，將下列五個 ASP.NET 網頁新增到此資料夾，並將它們全部設定為使用主版頁面 `Site.master`：

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`

![建立 PagingSortingDataListRepeater 資料夾並新增教學課程 ASP.NET 網頁](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**圖 1**：建立 `PagingSortingDataListRepeater` 資料夾並新增教學課程 ASP.NET 網頁

接下來，開啟 [`Default.aspx`] 頁面，並將 [`SectionLevelTutorialListing.ascx` 使用者] 控制項從 [`UserControls`] 資料夾拖曳到設計介面上。 我們在[主版頁面和網站導覽](../introduction/master-pages-and-site-navigation-cs.md)教學課程中建立的這個使用者控制項，會列舉網站地圖，並在項目符號清單的目前區段中顯示這些教學課程。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image4.png)）

為了讓項目符號清單顯示我們將建立的分頁和排序教學課程，我們需要將它們新增至網站地圖。 開啟 `Web.sitemap` 檔案，並使用 DataList 網站地圖節點標記在編輯和刪除之後新增下列標記：

[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample1.xml)]

![更新網站地圖以包含新的 ASP.NET 網頁](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)

**圖 3**：更新網站地圖以包含新的 ASP.NET 網頁

## <a name="a-review-of-paging"></a>分頁審查

在先前的教學課程中，我們看到了如何逐頁流覽 GridView、DetailsView 和 FormView 控制項中的資料。 這三個控制項提供簡單的分頁形式，稱為「*預設分頁*」，只要核取 [控制項] 智慧標籤中的 [啟用分頁] 選項，就可以實作為實頁。 使用預設分頁時，每次在流覽第一頁時要求一頁數據，或當使用者流覽至不同的資料頁面時，GridView、DetailsView 或 FormView 控制項會重新要求 ObjectDataSource 中的*所有*資料。 接著，它會根據所要求的頁面索引和每頁顯示的記錄數目，來顯示特定記錄集。 我們已在[分頁和排序報表資料](../paging-and-sorting/paging-and-sorting-report-data-cs.md)教學課程中詳細討論預設分頁。

由於預設的分頁會重新要求每個頁面的所有記錄，因此在分頁處理足夠大量的資料時並不實用。 例如，假設頁面大小為10的50000筆記錄分頁。 每次使用者移到新的頁面時，都必須從資料庫中取出所有50000記錄，即使只顯示其中十個。

*自訂分頁*藉由只抓取要在要求的頁面上顯示的精確記錄子集，來解決預設分頁的效能考慮。 在執行自訂分頁時，我們必須撰寫 SQL 查詢，只會有效率地傳回正確的記錄集。 我們已瞭解如何使用 SQL Server 2005 s new [`ROW_NUMBER()` 關鍵字](http://www.4guysfromrolla.com/webtech/010406-1.shtml)，透過大量資料的教學課程[有效率地進行分頁](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)，以建立這類查詢。

若要在 DataList 或重複項控制項中執行預設分頁，我們可以使用[`PagedDataSource` 類別](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx)，做為要分頁其內容之 `ProductsDataTable` 的包裝函式。 `PagedDataSource` 類別具有 `DataSource` 屬性，可以指派給任何可列舉的物件，並[`PageSize`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx)和[`CurrentPageIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx)屬性，指出每頁顯示的記錄數目，以及目前的頁面索引。 一旦設定這些屬性之後，就可以使用 `PagedDataSource` 做為任何資料 Web 控制項的資料來源。 列舉的 `PagedDataSource`只會根據 `PageSize` 和 `CurrentPageIndex` 屬性，傳回其內部 `DataSource` 的適當記錄子集。 [圖 4] 描述了 `PagedDataSource` 類別的功能。

![PagedDataSource 會使用可分頁的介面包裝可列舉物件](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image6.png)

**圖 4**： `PagedDataSource` 以可分頁的介面包裝可列舉物件

`PagedDataSource` 物件可以直接從商務邏輯層建立和設定，並透過 ObjectDataSource 系結至 DataList 或重複項，也可以直接在 ASP.NET page s 程式碼後置類別中建立和設定。 如果使用第二種方法，我們必須使用 ObjectDataSource 放棄，並改為以程式設計方式將分頁資料系結至 DataList 或中繼器。

`PagedDataSource` 物件也有支援自訂分頁的屬性。 不過，我們可以略過使用自訂分頁的 `PagedDataSource`，因為我們在 `ProductsBLL` 類別中已經有適用于自訂分頁的 BLL 方法，會傳回要顯示的精確記錄。

在本教學課程中，我們將探討如何藉由將新的方法加入至 `ProductsBLL` 類別，以傳回適當設定的 `PagedDataSource` 物件，來在 DataList 中執行預設分頁。 在下一個教學課程中，我們將瞭解如何使用自訂分頁。

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>步驟2：在商務邏輯層中新增預設分頁方法

`ProductsBLL` 類別目前有一種方法可以傳回所有產品資訊 `GetProducts()`，另一種則是在起始索引 `GetProductsPaged(startRowIndex, maximumRows)`傳回產品的特定子集。 使用預設分頁時，GridView、DetailsView 和 FormView 控制項全都會使用 `GetProducts()` 方法來抓取所有產品，但接著在內部使用 `PagedDataSource`，只顯示正確的記錄子集。 若要使用 DataList 和中繼器控制項複寫這項功能，我們可以在會模擬此行為的 BLL 中建立新的方法。

將方法新增至名為 `GetProductsAsPagedDataSource` 的 `ProductsBLL` 類別，以接受兩個整數輸入參數：

- `pageIndex` 要顯示的頁面索引，以零為索引，以及
- `pageSize` 每頁顯示的記錄數目。

`GetProductsAsPagedDataSource` 一開始會從 `GetProducts()`中取出*所有*記錄。 接著，它會建立 `PagedDataSource` 物件，並將其 `CurrentPageIndex` 和 `PageSize` 屬性設定為傳入的 `pageIndex` 和 `pageSize` 參數的值。 方法最後會傳回這個已設定的 `PagedDataSource`：

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>步驟3：使用預設分頁在 DataList 中顯示產品資訊

透過將 `GetProductsAsPagedDataSource` 方法加入 `ProductsBLL` 類別中，我們現在可以建立可提供預設分頁的 DataList 或重複項。 一開始先開啟 [`PagingSortingDataListRepeater`] 資料夾中的 [`Paging.aspx`] 頁面，然後從 [工具箱] 將 [DataList] 拖曳至設計工具，將 [DataList s `ID`] 屬性設為 [`ProductsDefaultPaging`]。 從 DataList s 智慧標籤中，建立名為 `ProductsDefaultPagingDataSource` 的新 ObjectDataSource 並加以設定，以便使用 `GetProductsAsPagedDataSource` 方法來抓取資料。

[![建立 ObjectDataSource 並將其設定為使用 GetProductsAsPagedDataSource （）方法](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**圖 5**：建立 ObjectDataSource 並將其設定為使用 `GetProductsAsPagedDataSource` `()` 方法（[按一下以查看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image9.png)）

將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**圖 6**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image12.png)）

由於 `GetProductsAsPagedDataSource` 方法預期會有兩個輸入參數，因此，此 wizard 會提示我們提供這些參數值的來源。

分頁索引和頁面大小的值必須在回傳之間記住。 它們可以儲存為 view 狀態、保存至 querystring、儲存在會話變數中，或使用其他技術來記住。 在本教學課程中，我們將使用 querystring，其優點是允許將特定頁面的資料加入書簽。

特別是，請分別針對 `pageIndex` 和 `pageSize` 參數使用 querystring 欄位 pageIndex 和 pageSize （請參閱 [圖 7]）。 請花點時間設定這些參數的預設值，因為當使用者第一次造訪此頁面時，查詢字串值將不會出現。 針對 `pageIndex`，將預設值設定為0（這會顯示資料的第一頁），`pageSize` s 預設值設為4。

[![使用 QueryString 做為 pageIndex 和 pageSize 參數的來源](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**圖 7**：使用 QueryString 做為 `pageIndex` 和 `pageSize` 參數的來源（[按一下以查看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image15.png)）

設定 ObjectDataSource 之後，Visual Studio 會自動建立 DataList 的 `ItemTemplate`。 自訂 `ItemTemplate`，以便只顯示產品的名稱、類別和供應商。 同時將 DataList s `RepeatColumns` 屬性設為2，其 `Width` 為100%，而其 `ItemStyle` s `Width` 為50%。 這些寬度設定會為這兩個數據行提供相等的間距。

進行這些變更之後，DataList 和 ObjectDataSource 的標記看起來應該如下所示：

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

> [!NOTE]
> 因為我們不會在本教學課程中執行任何更新或刪除功能，所以您可以停用 DataList s view 狀態來減少呈現的頁面大小。

一開始透過瀏覽器造訪此頁面時，不會提供 `pageIndex` 或 `pageSize` querystring 參數。 因此，會使用預設值0和4。 如 [圖 8] 所示，這會產生一個 DataList，其中顯示前四個產品。

[![列出前四個產品](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)

**圖 8**：列出前四個產品（[按一下以觀看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image18.png)）

如果沒有分頁介面，使用者目前無法直接流覽至第二頁的資料。 我們會在步驟4中建立分頁介面。 不過，現在只有在 querystring 中直接指定分頁準則，才可以完成分頁。 例如，若要查看第二個頁面，請將瀏覽器的網址列中的 URL 從 `Paging.aspx` 變更為 `Paging.aspx?pageIndex=2`，然後按 Enter 鍵。 這會顯示第二頁的資料（請參閱 [圖 9]）。

[顯示第二頁的資料 ![](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)

**圖 9**：顯示資料的第二頁（[按一下以查看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)）

## <a name="step-4-creating-the-paging-interface"></a>步驟4：建立分頁介面

有各種不同的分頁介面可以實作為。 GridView、DetailsView 和 FormView 控制項提供四種不同的介面來進行選擇：

- **接下來，先前**的使用者可以一次將一個頁面移到下一個或上一個。
- **接下來，[上一步]** 、[下一步] 和 [上一個] 和 [上一個] 按鈕，此介面包含移至第一個或最後一個頁面的第一個和最後一個按鈕。
- **數值**列出分頁介面中的頁碼，可讓使用者快速跳到特定頁面。
- **數位、第一個、最後一個加上**數值頁碼的數位，包含移至第一個或最後一個頁面的按鈕。

對於 DataList 和中繼器，我們負責決定分頁介面並加以執行。 這牽涉到在頁面中建立所需的 Web 控制項，並在按一下特定的 [分頁介面] 按鈕時顯示要求的頁面。 此外，某些分頁介面控制項可能需要停用。 例如，使用 [下一步]、[上一個]、[上一個]、[最後一個] 介面來流覽資料的第一頁時，會停用第一個和前一個按鈕。

在本教學課程中，讓我們使用下一個、上一個、第一個、最後一個介面。 將四個按鈕 Web 控制項新增至頁面，並將其 `ID` 設定為 `FirstPage`、`PrevPage`、`NextPage`和 `LastPage`。 將 `Text` 屬性設定為先 &lt;&lt;、&lt; 上一個、下一個 &gt;和最後一個 &gt;&gt;。

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample4.aspx)]

接下來，為每個按鈕建立一個 `Click` 事件處理常式。 我們稍後會新增必要的程式碼，以顯示要求的頁面。

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>記住要進行分頁的記錄總數

不論選取的分頁介面為何，我們都需要計算並記憶要進行分頁的記錄總數。 總數據列計數（與頁面大小結合）會決定要進行分頁的總數據頁面總計，這會決定要新增或啟用的分頁介面控制項。 在下一個、上一個、第一個、最後一個所建立的介面中，頁面計數的使用方式有兩種：

- 若要判斷我們是否正在觀看最後一頁，在此情況下，[下一步] 和 [最後一個] 按鈕會停用。
- 如果使用者按一下 [上一步] 按鈕，我們必須將其 whisk 到最後一頁，其索引的長度小於頁面計數。

頁面計數是以總數據列計數的上限除以頁面大小來計算。 例如，如果我們使用每頁四筆記錄的79筆記錄進行分頁，則頁面計數為20（79/4 的上限）。 如果我們使用數值分頁介面，此資訊會告知我們要顯示多少數值頁面按鈕;如果我們的分頁介面包含 [下一步] 或 [最後一個] 按鈕，則會使用頁面計數來決定何時要停用下一個或最後一個按鈕。

如果分頁介面包含 [最後一個] 按鈕，則必須在回傳期間記住分頁的記錄總數，以便在按一下最後一個按鈕時，可以判斷最後一頁的索引。 為了方便這項工作，請在 ASP.NET 網頁的程式碼後置類別中建立 `TotalRowCount` 屬性，以保存其值來查看狀態：

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

除了 `TotalRowCount`以外，請花幾分鐘的時間建立唯讀頁面層級的屬性，以便輕鬆存取頁面索引、頁面大小和頁面計數：

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample6.cs)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>判斷要進行分頁的記錄總數

從 ObjectDataSource s `Select()` 方法傳回的 `PagedDataSource` 物件在其*所有*產品記錄中都具有，即使在 DataList 中只會顯示部分的專案。 `PagedDataSource` s [`Count` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx)只會傳回將顯示在 DataList 中的專案數;[`DataSourceCount` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx)會傳回 `PagedDataSource`內的總專案數。 因此，我們需要將 ASP.NET page s `TotalRowCount` 屬性指派 `PagedDataSource` s `DataSourceCount` 屬性的值。

若要完成此動作，請建立 ObjectDataSource s `Selected` 事件的事件處理常式。 在 `Selected` 事件處理常式中，我們可以存取 ObjectDataSource s `Select()` 方法的傳回值，在此案例中為 `PagedDataSource`。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

## <a name="displaying-the-requested-page-of-data"></a>顯示要求的資料頁面

當使用者按一下頁面介面中的其中一個按鈕時，我們必須顯示所要求的資料頁面。 由於分頁參數是透過 querystring 指定的，若要顯示所要求的資料頁面，請使用 `Response.Redirect(url)` 讓使用者的瀏覽器重新要求具有適當分頁參數的 `Paging.aspx` 頁面。 例如，若要顯示第二頁的資料，我們會將使用者重新導向至 `Paging.aspx?pageIndex=1`。

為了加速此工作，請建立 `RedirectUser(sendUserToPageIndex)` 方法，將使用者重新導向至 `Paging.aspx?pageIndex=sendUserToPageIndex`。 然後，從 `Click` 事件處理常式的四個按鈕中呼叫此方法。 在 `FirstPage` `Click` 事件處理常式中，呼叫 `RedirectUser(0)`，將其傳送至第一頁;在 `PrevPage` `Click` 事件處理常式中，使用 `PageIndex - 1` 作為頁面索引;以此類推。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample8.cs)]

當 `Click` 事件處理常式完成時，可以按一下按鈕，將 DataList s 記錄分頁。 請花點時間試用！

## <a name="disabling-paging-interface-controls"></a>停用分頁介面控制項

目前，不論流覽的頁面為何，都會啟用全部四個按鈕。 不過，我們想要在顯示第一頁數據時停用第一個和上一個按鈕，而在顯示最後一頁時，則是 [下一步] 和 [最後一個] 按鈕。 ObjectDataSource s `Select()` 方法所傳回的 `PagedDataSource` 物件具有[`IsFirstPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx)和[`IsLastPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx)屬性，可供我們檢查以判斷我們是否正在查看資料的第一個或最後一頁。

將下列內容新增至 ObjectDataSource s `Selected` 事件處理常式：

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

使用這項新增功能時，第一個和前一個按鈕會在流覽第一頁時停用，而 [下一步] 和 [最後一個] 按鈕則會在觀看最後一頁時停用。

讓我們透過通知使用者目前正在查看的頁面以及有多少總頁數，來完成分頁介面。 將 [標籤] Web 控制項新增至頁面，並將其 [`ID`] 屬性設定為 [`CurrentPageNumber`]。 在 ObjectDataSource s 選取的事件處理常式中設定其 `Text` 屬性，使其包含目前正在查看的頁面（`PageIndex + 1`）和總頁數（`PageCount`）。

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample10.cs)]

[圖 10] 顯示第一次造訪時 `Paging.aspx`。 因為 querystring 是空的，所以 DataList 預設會顯示前四個產品;[第一個] 和 [上一個] 按鈕已停用。 按 [下一步] 會顯示接下來四筆記錄（見 [圖 11]）;[第一個] 和 [上一個] 按鈕現在已啟用。

[顯示第一頁的資料 ![](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image22.png)

**圖 10**：顯示資料的第一頁（[按一下以查看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)）

[顯示第二頁的資料 ![](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)

**圖 11**：顯示資料的第二頁（[按一下以查看完整大小的影像](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)）

> [!NOTE]
> 藉由允許使用者指定每頁要查看的頁面數目，可以進一步增強分頁介面。 例如，您可以新增 DropDownList，列出頁面大小選項，例如5、10、25、50和 All。 選取頁面大小時，使用者必須重新導向回到 `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`。 我將此增強功能作為讀者的練習。

## <a name="using-custom-paging"></a>使用自訂分頁

DataList 頁面會使用沒有效率的預設分頁技術來流覽其資料。 當逐頁查看大量資料時，請務必使用自訂分頁。 雖然執行詳細資料稍有不同，但是在 DataList 中執行自訂分頁的概念與預設分頁相同。 透過自訂分頁，使用 `ProductBLL` 類別的 `GetProductsPaged` 方法（而不是 `GetProductsAsPagedDataSource`）。 如[有效率地逐頁流覽大量資料](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)教學課程中所述，`GetProductsPaged` 必須傳遞開始資料列索引和要傳回的資料列數目上限。 這些參數可以透過 querystring 進行維護，就像 `pageIndex` 和預設分頁中使用的 `pageSize` 參數一樣。

由於自訂分頁沒有 `PagedDataSource`，因此您必須使用替代技術來判斷要進行分頁的記錄總數，以及是否要顯示資料的第一個或最後一頁。 `ProductsBLL` 類別中的 `TotalNumberOfProducts()` 方法會傳回要進行分頁的產品總數。 若要判斷資料的第一頁是否正在查看，請檢查開始列索引是否為零，然後才會查看第一頁。 如果開始資料列索引加上要傳回的最大資料列數目大於或等於要進行分頁的記錄總數，則會查看最後一頁。

在下一個教學課程中，我們將更詳細地探討如何執行自訂分頁。

## <a name="summary"></a>總結

雖然 DataList 和中繼器都不會提供 GridView、DetailsView 和 FormView 控制項中的現成分頁支援，但這類功能可以最輕鬆地新增。 若要執行預設分頁，最簡單的方式是將整個產品集包裝在 `PagedDataSource` 中，然後將 `PagedDataSource` 系結至 DataList 或中繼器。 在本教學課程中，我們已將 `GetProductsAsPagedDataSource` 方法新增至 `ProductsBLL` 類別，以傳回 `PagedDataSource`。 `ProductsBLL` 類別已經包含自訂分頁 `GetProductsPaged` 和 `TotalNumberOfProducts`所需的方法。

除了針對自訂分頁或 `PagedDataSource` 中的所有記錄，抓取要顯示的一組精確記錄，以進行預設分頁，我們也需要手動加入分頁介面。 在本教學課程中，我們建立了下一個、上一個、第一個、最後一個具有四個按鈕 Web 控制項的介面。 此外，也會顯示目前頁碼和總頁數的標籤控制項。

在下一個教學課程中，我們將瞭解如何將排序支援新增至 DataList 和中繼器。 我們也會瞭解如何建立可同時進行分頁和排序的 DataList （使用預設和自訂分頁的範例）。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Liz Shulok、Ken Pespisa 和 Bernadette Leigh。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一個](sorting-data-in-a-datalist-or-repeater-control-cs.md)
