---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
title: 簡介如何插入、更新和刪除資料（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將瞭解如何將 ObjectDataSource 的 Insert （）、Update （）和 Delete （）方法對應到 BLL 類別的方法，以及如何 devenv.exe.configu 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 35b40b8f-2ca8-4ab3-9c19-f361a91a3647
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 79491118ba1cbbc8c1b67ca9646a817d941f17ba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74630489"
---
# <a name="an-overview-of-inserting-updating-and-deleting-data-vb"></a>簡介插入、更新和刪除資料（VB）

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_VB.exe)或[下載 PDF](an-overview-of-inserting-updating-and-deleting-data-vb/_static/datatutorial16vb1.pdf)

> 在本教學課程中，我們將瞭解如何將 ObjectDataSource 的 Insert （）、Update （）和 Delete （）方法對應到 BLL 類別的方法，以及如何設定 GridView、DetailsView 和 FormView 控制項來提供資料修改功能。

## <a name="introduction"></a>簡介

在過去數個教學課程中，我們已檢查如何使用 GridView、DetailsView 和 FormView 控制項，在 ASP.NET 網頁中顯示資料。 這些控制項只會處理提供給它們的資料。 這些控制項通常會透過使用資料來源控制項（例如 ObjectDataSource）來存取資料。 我們已瞭解 ObjectDataSource 如何作為 ASP.NET 網頁與基礎資料之間的 proxy。 當 GridView 需要顯示資料時，它會叫用其 ObjectDataSource 的 `Select()` 方法，然後從我們的商務邏輯層（BLL）調用方法，這會呼叫適當資料存取層（DAL） TableAdapter 中的方法，然後將 `SELECT` 查詢傳送至 Northwind 資料庫。

回想一下，當我們在[第一個教學](../introduction/creating-a-data-access-layer-cs.md)課程的 DAL 中建立 tableadapter 時，Visual Studio 自動新增了從基礎資料庫資料表插入、更新和刪除資料的方法。 此外，在[建立商務邏輯層](../introduction/creating-a-business-logic-layer-vb.md)時，我們在 BLL 中設計了方法，以向下呼叫這些資料修改 DAL 方法。

除了其 `Select()` 方法之外，ObjectDataSource 也具有 `Insert()`、`Update()`和 `Delete()` 方法。 如同 `Select()` 方法，這三種方法可以對應到基礎物件中的方法。 當設定為插入、更新或刪除資料時，GridView、DetailsView 和 FormView 控制項會提供使用者介面來修改基礎資料。 這個使用者介面會呼叫 ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法，然後叫用基礎物件的相關聯方法（請參閱 [圖 1]）。

[![ObjectDataSource 的 Insert （）、Update （）和 Delete （）方法做為 BLL 中的 Proxy](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image1.png)

**圖 1**： ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法作為 BLL 的 Proxy （[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image3.png)）

在本教學課程中，我們將瞭解如何將 ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法對應到 BLL 中類別的方法，以及如何設定 GridView、DetailsView 和 FormView 控制項來提供資料修改功能。

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>步驟1：建立 Insert、Update 和 Delete 教學課程的網頁

在我們開始探索如何插入、更新和刪除資料之前，讓我們先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程中使用，以及接下來的幾頁。 從新增名為 `EditInsertDelete`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![新增資料修改相關教學課程的 ASP.NET 網頁](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image4.png)

**圖 2**：加入資料修改相關教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`EditInsertDelete`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將此使用者控制項從方案總管拖曳至頁面的設計檢視，以將其新增至 `Default.aspx`。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image5.png)

**圖 3**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image7.png)）

最後，將頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，請在自訂的格式設定 `<siteMapNode>`之後加入下列標記：

[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含用於編輯、插入及刪除教學課程的專案。

![網站地圖現在包含編輯、插入及刪除教學課程的專案](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image8.png)

**圖 4**：網站地圖現在包含用於編輯、插入及刪除教學課程的專案

## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>步驟2：加入和設定 ObjectDataSource 控制項

由於 GridView、DetailsView 和 FormView 各有不同的資料修改功能和配置，因此讓我們個別檢查每個。 不過，不是讓每個控制項使用自己的 ObjectDataSource，而是建立所有三個控制項範例都可以共用的單一 ObjectDataSource。

開啟 [`Basics.aspx`] 頁面，從 [工具箱] 將 [ObjectDataSource] 拖曳至設計工具，然後按一下其智慧標籤中的 [設定資料來源] 連結。 由於 `ProductsBLL` 是唯一提供編輯、插入和刪除方法的 BLL 類別，因此請將 ObjectDataSource 設定為使用這個類別。

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image9.png)

**圖 5**：設定 ObjectDataSource 使用 `ProductsBLL` 類別（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image11.png)）

在下一個畫面中，我們可以選取適當的索引標籤，然後從下拉式清單中選擇方法，以指定 `ProductsBLL` 類別對應至 ObjectDataSource `Select()`、`Insert()`、`Update()`和 `Delete()` 的方法。 [圖 6] 現在看起來應該很熟悉，將 ObjectDataSource 的 `Select()` 方法對應到 `ProductsBLL` 類別的 `GetProducts()` 方法。 您可以從頂端的清單中選取適當的索引標籤，來設定 `Insert()`、`Update()`和 `Delete()` 方法。

[![讓 ObjectDataSource 傳回所有產品](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image12.png)

**圖 6**：讓 ObjectDataSource 傳回所有產品（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image14.png)）

圖7、8和9顯示 ObjectDataSource 的 [更新]、[插入] 和 [刪除] 索引標籤。 設定這些索引標籤，讓 `Insert()`、`Update()`和 `Delete()` 方法分別叫用 `ProductsBLL` 類別的 `UpdateProduct`、`AddProduct`和 `DeleteProduct` 方法。

[![將 ObjectDataSource 的 Update （）方法對應至 ProductBLL 類別的 UpdateProduct 方法](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image15.png)

**圖 7**：將 ObjectDataSource 的 `Update()` 方法對應到 `ProductBLL` 類別的 `UpdateProduct` 方法（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image17.png)）

[![將 ObjectDataSource 的 Insert （）方法對應至 ProductBLL 類別的 AddProduct 方法](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image18.png)

**圖 8**：將 ObjectDataSource 的 `Insert()` 方法對應到 `ProductBLL` 類別的新增 `Product` 方法（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image20.png)）

[![將 ObjectDataSource 的 Delete （）方法對應至 ProductBLL 類別的 DeleteProduct 方法](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image21.png)

**圖 9**：將 ObjectDataSource 的 `Delete()` 方法對應到 `ProductBLL` 類別的 `DeleteProduct` 方法（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image23.png)）

您可能已經注意到，[更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單已選取這些方法。 這是因為我們使用 `DataObjectMethodAttribute` 來裝飾 `ProductsBLL`的方法。 例如，DeleteProduct 方法具有下列簽章：

[!code-vb[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample2.vb)]

`DataObjectMethodAttribute` 屬性指出每個方法的用途，不論它是用於選取、插入、更新或刪除，以及它是否為預設值。 如果您在建立 BLL 類別時省略這些屬性，則必須從 [更新]、[插入] 和 [刪除] 索引標籤手動選取方法。

確定適當的 `ProductsBLL` 方法對應到 ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法之後，請按一下 [完成] 以完成嚮導。

## <a name="examining-the-objectdatasources-markup"></a>檢查 ObjectDataSource 的標記

透過其 wizard 設定 ObjectDataSource 之後，請前往來源視圖來檢查產生的宣告式標記。 `<asp:ObjectDataSource>` 標記會指定基礎物件和要叫用的方法。 此外，還有 `DeleteParameters`、`UpdateParameters`和 `InsertParameters` 對應至 `ProductsBLL` 類別的 `AddProduct`、`UpdateProduct`和 `DeleteProduct` 方法的輸入參數：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample3.aspx)]

ObjectDataSource 會針對其相關聯的方法包含每個輸入參數的參數，就像當 ObjectDataSource 設定為呼叫預期輸入參數（例如 `GetProductsByCategoryID(categoryID)`）的 select 方法時，會出現 `SelectParameter` s 的清單。 如我們稍後所見，GridView、DetailsView 和 FormView 會在叫用 ObjectDataSource 的 `Insert()`、`Update()`或 `Delete()` 方法之前，自動設定這些 `DeleteParameters`、`UpdateParameters`和 `InsertParameters` 的值。 您也可以視需要以程式設計方式設定這些值，我們將在未來的教學課程中討論。

使用 wizard 設定 ObjectDataSource 的一個副作用是，Visual Studio 將[OldValuesParameterFormatString 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx)設定為 `original_{0}`。 這個屬性值是用來包含正在編輯之資料的原始值，在兩種情況下很有用：

- 如果在編輯記錄時，使用者可以變更主要金鑰值。 在此情況下，必須提供新的主鍵值和原始的主要金鑰值，才能找到具有原始主要金鑰值的記錄，並據此更新其值。
- 使用開放式平行存取時。 開放式平行存取是一項技術，可確保兩個同時進行的使用者不會覆寫另一個變更，而是後續教學課程的主題。

`OldValuesParameterFormatString` 屬性會指出原始值的基礎物件之 update 和 delete 方法中的輸入參數名稱。 當我們探索開放式平行存取時，我們會更詳細地討論此屬性及其用途。 不過，我現在會將它帶入，因為我們的 BLL 方法不會預期原始值，因此請務必移除此屬性。 將 `OldValuesParameterFormatString` 屬性設定為預設值以外的任何專案（`{0}`），會在資料 Web 控制項嘗試叫用 ObjectDataSource 的 `Update()` 或 `Delete()` 方法時造成錯誤，因為 ObjectDataSource 會嘗試同時傳入 `UpdateParameters` 或指定的 `DeleteParameters`，以及原始值參數。

如果這不太清楚，別擔心，我們將在未來的教學課程中檢查這個屬性及其公用程式。 目前，您只需從宣告式語法中移除此屬性宣告，或將值設為預設值（{0}）。

> [!NOTE]
> 如果您只是從設計檢視中的屬性視窗清除 `OldValuesParameterFormatString` 屬性值，屬性仍然會存在於宣告式語法中，但會設為空字串。 不幸的是，仍然會產生上述的相同問題。 因此，請從宣告式語法中移除該屬性，或從屬性視窗將值設定為預設的 `{0}`。

## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>步驟3：加入資料 Web 控制項並設定它以進行資料修改

一旦將 ObjectDataSource 新增至頁面並設定之後，我們就可以將資料 Web 控制項新增至頁面，以顯示資料並提供方法讓使用者進行修改。 我們會分別探討 GridView、DetailsView 和 FormView，因為這些資料 Web 控制項的資料修改功能和設定各有不同。

我們將在本文的其餘部分看到，透過 GridView、DetailsView 和 FormView 控制項來新增非常基本的編輯、插入及刪除支援，其實就像檢查幾個核取方塊一樣簡單。 在現實世界中，有許多微妙差異和 edge 案例可提供比單純點和按一下更多的功能。 不過，本教學課程只著重于證明簡單的資料修改功能。 未來的教學課程會檢查在實際設定中一定會發生的顧慮。

## <a name="deleting-data-from-the-gridview"></a>刪除 GridView 中的資料

首先，從 [工具箱] 將 GridView 拖曳至設計工具。 接下來，從 GridView 智慧標籤的下拉式清單中選取 ObjectDataSource，將其系結至 GridView。 此時，GridView 的宣告式標記會是：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample4.aspx)]

透過其智慧標籤將 GridView 系結至 ObjectDataSource 有兩個優點：

- 系統會針對 ObjectDataSource 所傳回的每個欄位，自動建立 BoundFields 和 CheckBoxFields。 此外，BoundField 和 CheckBoxField 的屬性會根據基礎欄位的中繼資料來設定。 例如，[`ProductID`]、[`CategoryName`] 和 [`SupplierName`] 欄位在 `ProductsDataTable` 中會標示為唯讀，因此在編輯時，不應該是可更新的。 為了配合此，這些 BoundFields 的[ReadOnly 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx)會設定為 `True`。
- [DataKeyNames 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx)會指派給基礎物件的主要索引鍵欄位。 使用 GridView 編輯或刪除資料時，這是必要的，因為此屬性會指出唯一識別每筆記錄的欄位（或欄位集合）。 如需 `DataKeyNames` 屬性的詳細資訊，請參閱使用可[選取的主要 GridView 和詳細資訊 detailview 之教學課程中的主要/詳細資料](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)。

雖然 GridView 可以透過屬性視窗或宣告式語法系結至 ObjectDataSource，但這麼做會要求您手動新增適當的 BoundField 和 `DataKeyNames` 標記。

GridView 控制項提供資料列層級編輯和刪除的內建支援。 設定 GridView 以支援刪除會新增 [刪除] 按鈕的資料行。 當終端使用者按一下特定資料列的 [刪除] 按鈕時，回傳接踵而來和 GridView 會執行下列步驟：

1. 已指派 ObjectDataSource 的 `DeleteParameters` 值
2. 已叫用 ObjectDataSource 的 `Delete()` 方法，正在刪除指定的記錄
3. GridView 藉由叫用其 `Select()` 方法，將其本身重新系結至 ObjectDataSource

指派給 `DeleteParameters` 的值是已按一下 [刪除] 按鈕之資料列的 `DataKeyNames` 欄位值。 因此，要正確設定 GridView 的 `DataKeyNames` 屬性是很重要的。 如果遺失，`DeleteParameters` 將在步驟1中指派 `Nothing` 的值，而這不會導致步驟2中任何已刪除的記錄。

> [!NOTE]
> `DataKeys` 集合會儲存在 GridView 的控制項狀態中，這表示即使已停用 GridView s view 狀態，仍會在回傳期間記住 `DataKeys` 值。 不過，對於支援編輯或刪除的 Gridview （預設行為），檢視狀態會保持為 [已啟用] 非常重要。 如果您將 GridView 的 `EnableViewState` 屬性設定為 `false`，則單一使用者的編輯和刪除行為將會正常運作，但如果有並行使用者刪除資料，則這些並行使用者可能會不小心刪除或編輯他們不想要的記錄。 如需詳細資訊，請參閱我的 blog 專案，[警告： ASP.NET 2.0 gridview/DetailsView/FormViews 的並行處理問題，支援編輯及/或刪除，以及停用檢視狀態](http://scottonwriting.net/sowblog/posts/10054.aspx)的。

這個相同的警告也適用于 DetailsViews 和 FormViews。

若要新增 GridView 的刪除功能，只要移至其智慧標籤，然後勾選 [啟用刪除] 核取方塊即可。

![勾選 [啟用刪除] 核取方塊](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image24.png)

**圖 10**：勾選 [啟用刪除] 核取方塊

核取 [從智慧標籤啟用刪除] 核取方塊，會將 CommandField 新增至 GridView。 CommandField 會使用可執行下列一或多項工作的按鈕，呈現 GridView 中的資料行：選取記錄、編輯記錄，以及刪除記錄。 我們先前已看到 CommandField 的運作方式，是使用可[選取的主要 GridView 和詳細資料 detailview 之教學課程來選取主要/詳細資料](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)中的記錄。

CommandField 包含數個 `ShowXButton` 屬性，指出要在 CommandField 中顯示哪一系列的按鈕。 藉由勾選 [啟用刪除] 核取方塊，其 `ShowDeleteButton` 屬性為 `True` 的 CommandField 已加入 GridView 的資料行集合中。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample5.aspx)]

此時，相信它不信了，我們已完成將刪除支援新增至 GridView 的作業！ 如 [圖 11] 所示，當您透過瀏覽器造訪此頁面時，會出現 [刪除] 按鈕的資料行。

[![CommandField 新增 [刪除] 按鈕的資料行](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image25.png)

**圖 11**： CommandField 新增 [刪除] 按鈕的資料行（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image27.png)）

如果您是從頭開始建立本教學課程，則在測試此頁面時，按一下 [刪除] 按鈕將會引發例外狀況。 繼續閱讀以瞭解為什麼會引發這些例外狀況，以及如何加以修正。

> [!NOTE]
> 如果您遵循本教學課程隨附的下載內容，這些問題已列入考慮。 不過，我建議您仔細閱讀下面所列的詳細資料，以協助找出可能發生的問題，以及適當的因應措施。

如果嘗試刪除產品時，您會收到例外狀況，其訊息類似于 "*ObjectDataSource ' ObjectDataSource1 ' 找不到具有下列參數的非泛型方法 ' DeleteProduct '： productid，原始\_productID*"，您可能忘了從 ObjectDataSource 移除 `OldValuesParameterFormatString` 屬性。 在指定了 `OldValuesParameterFormatString` 屬性的情況下，ObjectDataSource 會嘗試將 `productID` 和 `original_ProductID` 輸入參數傳入 `DeleteProduct` 方法。 不過，`DeleteProduct`只接受單一輸入參數，因此會發生例外狀況。 移除 `OldValuesParameterFormatString` 屬性（或將它設定為 `{0}`），會指示 ObjectDataSource 不要嘗試傳入原始輸入參數。

[![確定已清除 OldValuesParameterFormatString 屬性](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image28.png)

**圖 12**：確定已清除 `OldValuesParameterFormatString` 屬性（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image30.png)）

即使您已移除 `OldValuesParameterFormatString` 屬性，當您嘗試刪除包含下列訊息的產品時，仍會收到例外狀況：「*delete 語句與參考條件約束衝突」 FK\_順序\_詳細資料\_產品 '* 」。Northwind 資料庫包含 `Order Details` 和 `Products` 資料表之間的外鍵條件約束，這表示如果 `Order Details` 資料表中有一或多筆記錄，就無法從系統中刪除該產品。 由於 Northwind 資料庫中的每個產品在 `Order Details`中至少有一筆記錄，因此在我們第一次刪除產品的相關訂單詳細資料記錄之前，無法刪除任何產品。

[![外鍵條件約束禁止刪除產品](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image31.png)

**圖 13**：外鍵條件約束禁止刪除產品（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image33.png)）

在本教學課程中，我們將直接刪除 `Order Details` 資料表中的所有記錄。 在真實世界的應用程式中，我們需要執行下列其中一項：

- 擁有另一個畫面來管理訂單詳細資訊
- 擴大 `DeleteProduct` 方法，以包含刪除指定產品訂單詳細資料的邏輯
- 修改 TableAdapter 所使用的 SQL 查詢，以包含刪除指定產品的訂單詳細資料

讓我們直接刪除 `Order Details` 資料表中的所有記錄，以規避外鍵條件約束。 移至 Visual Studio 中的伺服器總管，以滑鼠右鍵按一下 [`NORTHWND.MDF`] 節點，然後選擇 [新增查詢]。 然後，在查詢視窗中，執行下列 SQL 語句： `DELETE FROM [Order Details]`

[![刪除 Order Details 資料表中的所有記錄](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image34.png)

**圖 14**：刪除 `Order Details` 資料表中的所有記錄（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image36.png)）

清除 `Order Details` 資料表後，按一下 [刪除] 按鈕將會刪除產品，而不會發生錯誤。 如果按一下 [刪除] 按鈕不會刪除產品，請檢查並確定 GridView 的 `DataKeyNames` 屬性已設為 [主要金鑰] 欄位（`ProductID`）。

> [!NOTE]
> 當按一下 [刪除] 按鈕時，回傳接踵而來和記錄會被刪除。 這可能是危險的，因為很容易不小心按一下錯誤的資料列的 [刪除] 按鈕。 在未來的教學課程中，我們將瞭解如何在刪除記錄時新增用戶端確認。

## <a name="editing-data-with-the-gridview"></a>使用 GridView 編輯資料

除了刪除，GridView 控制項也提供內建的資料列層級編輯支援。 設定 GridView 以支援編輯時，會加入 [編輯] 按鈕的資料行。 從使用者的觀點來看，按一下資料列的 [編輯] 按鈕會導致該資料列變成可編輯狀態，然後將儲存格轉換成包含現有值的文字方塊，並以 [更新] 和 [取消] 按鈕取代 [編輯] 按鈕。 進行想要的變更之後，終端使用者可以按一下 [更新] 按鈕來認可變更，或按 [取消] 按鈕來捨棄它們。 不論是哪一種情況，在按一下 [更新] 或 [取消] 之後，GridView 都會回到其預先編輯狀態。

身為頁面開發人員的觀點，當使用者按一下特定資料列的 [編輯] 按鈕時，回傳接踵而來和 GridView 會執行下列步驟：

1. GridView 的 `EditItemIndex` 屬性會指派給按下 [編輯] 按鈕的資料列索引
2. GridView 藉由叫用其 `Select()` 方法，將其本身重新系結至 ObjectDataSource
3. 符合 `EditItemIndex` 的資料列索引會以「編輯模式」呈現。 在此模式中，[編輯] 按鈕會取代為 [更新] 和 [取消] 按鈕和 BoundFields，其 `ReadOnly` 屬性為 False （預設值）會轉譯為 TextBox Web 控制項，其 `Text` 屬性會指派給資料欄位的值。

此時，標記會傳回到瀏覽器，讓使用者可以對資料列的資料進行任何變更。 當使用者按一下 [更新] 按鈕時，就會發生回傳，而 GridView 會執行下列步驟：

1. ObjectDataSource 的 `UpdateParameters` 值會被指派使用者輸入至 GridView 編輯介面的值
2. 會叫用 ObjectDataSource 的 `Update()` 方法，並更新指定的記錄
3. GridView 藉由叫用其 `Select()` 方法，將其本身重新系結至 ObjectDataSource

在步驟1中指派給 `UpdateParameters` 的主要金鑰值來自于 `DataKeyNames` 屬性中指定的值，而非主鍵值則來自于編輯過的資料列之 TextBox Web 控制項中的文字。 如同刪除，很重要的是 GridView 的 `DataKeyNames` 屬性設定正確。 如果遺失，`UpdateParameters` 的主要金鑰值會指派給步驟1中的 `Nothing` 值，而不會在步驟2中產生任何更新的記錄。

只要勾選 GridView 智慧標籤中的 [啟用編輯] 核取方塊，即可啟用編輯功能。

![勾選 [啟用編輯] 核取方塊](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image37.png)

**圖 15**：勾選 [啟用編輯] 核取方塊

勾選 [啟用編輯] 核取方塊將會加入 CommandField （如有需要），並將其 `ShowEditButton` 屬性設為 `True`。 如先前所見，CommandField 包含數個 `ShowXButton` 屬性，指出 CommandField 中顯示的按鈕系列。 勾選 [啟用編輯] 核取方塊會將 `ShowEditButton` 屬性新增至現有的 CommandField：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample6.aspx)]

這就是新增基本編輯支援的所有程式。 如 Figure16 所示，編輯介面相當粗糙每個 BoundField，其 `ReadOnly` 屬性設為 `False` （預設值）會轉譯成 TextBox。 這包括 `CategoryID` 和 `SupplierID`等欄位，也就是其他資料表的索引鍵。

[![按一下 [Chai s 編輯] 按鈕，就會在編輯模式中顯示資料列](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image38.png)

**圖 16**：按一下 [Chai s 編輯] 按鈕會在編輯模式中顯示資料列（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image40.png)）

除了要求使用者直接編輯外鍵值以外，編輯介面的介面也缺少下列方法：

- 如果使用者輸入的 `CategoryID` 或 `SupplierID` 不存在於資料庫中，`UPDATE` 將會違反外鍵條件約束，而導致引發例外狀況。
- 編輯介面不包含任何驗證。 如果您未提供必要的值（例如 `ProductName`），或輸入應為數值的字串值（例如輸入「太多！」 在 [`UnitPrice`] 文字方塊）中，將會擲回例外狀況。 未來的教學課程將會檢查如何將驗證控制項新增至編輯使用者介面。
- 目前，*所有*非唯讀的產品欄位都必須包含在 GridView 中。 如果我們要從 GridView 移除欄位（例如 `UnitPrice`），則在更新資料時，GridView 不會將 `UnitPrice` `UpdateParameters` 值，這會將資料庫記錄的 `UnitPrice` 變更為 `NULL` 值。 同樣地，如果必要的欄位（例如 `ProductName`）已從 GridView 移除，則更新會失敗，並出現相同的「資料*行 ' ProductName ' 不允許 null*」的例外狀況。
- 編輯介面的格式設定並不需要太多。 `UnitPrice` 會以四個小數點顯示。 在理想的情況下，`CategoryID` 和 `SupplierID` 值會包含 Dropdownlist 進行，列出系統中的類別和供應商。

這些都是我們目前必須提供的缺點，但會在未來的教學課程中解決。

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>使用 DetailsView 插入、編輯和刪除資料

如我們在先前的教學課程中所見，DetailsView 控制項一次會顯示一筆記錄，如 GridView，則允許編輯及刪除目前顯示的記錄。 使用者從 DetailsView 編輯和刪除專案的經驗，以及來自 ASP.NET 端的工作流程，都與 GridView 的功能完全相同。 DetailsView 與 GridView 的不同之處在于，它也提供內建的插入支援。

若要示範 GridView 的資料修改功能，請先將 DetailsView 新增至現有 GridView 上方的 [`Basics.aspx`] 頁面，然後透過 DetailsView 的智慧標籤將其系結至現有的 ObjectDataSource。 接下來，清除 DetailsView 的 `Height` 並 `Width` 屬性，然後從智慧標籤中選取 [啟用分頁] 選項。 若要啟用編輯、插入及刪除支援，只要勾選智慧標籤中的 [啟用編輯]、[啟用插入] 和 [啟用刪除] 核取方塊即可。

![設定 DetailsView 以支援編輯、插入及刪除](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image41.png)

**圖 17**：設定 DetailsView 以支援編輯、插入及刪除

如同 GridView，加入編輯、插入或刪除支援會將 CommandField 新增至 DetailsView，如下列宣告式語法所示：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample7.aspx)]

請注意，針對 DetailsView，CommandField 預設會出現在資料行集合的結尾。 因為 DetailsView 的欄位會轉譯為數據列，所以 CommandField 會顯示為數據列，其中包含 DetailsView 底部的 [插入]、[編輯] 和 [刪除] 按鈕。

[![設定 DetailsView 以支援編輯、插入及刪除](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image42.png)

**圖 18**：設定 DetailsView 以支援編輯、插入和刪除（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image44.png)）

按一下 [刪除] 按鈕會啟動與 GridView 相同的事件順序：回傳;接著，DetailsView 會根據 `DataKeyNames` 值填入其 ObjectDataSource 的 `DeleteParameters`;完成後，請呼叫其 ObjectDataSource 的 `Delete()` 方法，這實際上會從資料庫移除產品。 在 DetailsView 中編輯的功能也與 GridView 的方式相同。

若要插入，使用者會看到一個新按鈕，當您按一下時，就會以「插入模式」轉譯 DetailsView。 使用 [插入模式] 時，[新增] 按鈕會由 [插入] 和 [取消] 按鈕取代，而且只會顯示 `InsertVisible` 屬性設為 `True` （預設值）的 BoundFields。 當您透過智慧標籤將 DetailsView 系結至資料來源時，這些資料欄位（例如 `ProductID`）會將其[InsertVisible 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx)設定為 `False`。

透過智慧標籤將資料來源系結至 DetailsView 時，Visual Studio 會將 `InsertVisible` 屬性設定為僅 `False` 自動遞增欄位。 唯讀欄位（例如 `CategoryName` 和 `SupplierName`）將會顯示在「插入模式」使用者介面中，除非其 `InsertVisible` 屬性已明確設定為 [`False`]。 請花點時間將這兩個欄位的 `InsertVisible` 屬性設定為 `False`，不論是透過 DetailsView 的宣告式語法，或透過智慧標籤中的編輯欄位連結。 [圖 19] 顯示按一下 [編輯欄位] 連結，將 `InsertVisible` 屬性設定為 [`False`]。

[![Northwind 商貿現在提供 Acme 茶](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image45.png)

**圖 19**： Northwind 商貿現在提供 Acme 茶（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image47.png)）

設定 `InsertVisible` 屬性之後，請在瀏覽器中查看 [`Basics.aspx`] 頁面，然後按一下 [新增] 按鈕。 [圖 20] 顯示將新飲料（Acme 茶）新增至產品線時的 DetailsView。

[![Northwind 商貿現在提供 Acme 茶](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image48.png)

**圖 20**： Northwind 商貿現在提供 Acme 茶（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image50.png)）

輸入 Acme 茶的詳細資料並按一下 [插入] 按鈕之後，會將回傳接踵而來和新記錄加入至 `Products` 資料庫資料表。 由於此 DetailsView 會列出產品，而且它們存在於資料庫資料表中，因此我們必須先分頁到最後一個產品，才能看到新的產品。

[適用于 Acme 茶的 ![詳細資料](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image51.png)

**圖 21**： Acme 茶的詳細資料（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image53.png)）

> [!NOTE]
> DetailsView 的[CurrentMode 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx)會指出要顯示的介面，而且可以是下列其中一個值： `Edit`、`Insert`或 `ReadOnly`。 [DefaultMode 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx)指出 detailsview 在完成編輯或插入之後，所傳回的模式，並且適用于顯示永久為 [編輯] 或 [插入] 模式的 DetailsView。

DetailsView 的點和編輯功能與 GridView 的限制相同：使用者必須輸入現有的 `CategoryID`，並透過 textbox `SupplierID` 值;介面缺少任何驗證邏輯;不允許 `NULL` 值或沒有在資料庫層級指定之預設值的所有產品欄位，都必須包含在插入介面中，依此類推。

在未來的文章中，我們將檢查以擴充及增強 GridView 編輯介面的技術，也適用于 DetailsView 控制項的編輯和插入介面。

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>使用 FormView 取得更有彈性的資料修改使用者介面

FormView 提供了插入、編輯和刪除資料的內建支援，但是因為它使用範本而不是欄位，所以沒有任何地方可以加入 GridView 和 DetailsView 控制項用來提供資料的 BoundFields 或 CommandField修改介面。 相反地，在加入新專案時，用來收集使用者輸入的 Web 控制項，或編輯現有的 [新增]、[編輯]、[刪除]、[插入]、[更新] 和 [取消] 按鈕，必須手動新增至適當的範本。 幸好，Visual Studio 會在透過其智慧標籤的下拉式清單將 FormView 系結至資料來源時，自動建立所需的介面。

為了說明這些技術，請先將 FormView 加入至 `Basics.aspx` 頁面，然後從 FormView 的智慧標籤將它系結至已建立的 ObjectDataSource。 這會產生 [FormView with TextBox] Web 控制項的 `EditItemTemplate`、`InsertItemTemplate`和 `ItemTemplate`，用於收集 [新增]、[編輯]、[刪除]、[插入]、[更新] 和 [取消] 按鈕的使用者輸入和按鈕 Web 控制項。 此外，FormView 的 `DataKeyNames` 屬性會設定為 ObjectDataSource 所傳回之物件的主要索引鍵欄位（`ProductID`）。 最後，勾選 FormView 的智慧標籤中的 [啟用分頁] 選項。

以下顯示在 FormView 已系結至 ObjectDataSource 之後，FormView 的 `ItemTemplate` 宣告式標記。 根據預設，每個非布林值產品欄位都會系結至標籤 Web 控制項的 `Text` 屬性，而每個布林值欄位（`Discontinued`）都會系結至已停用之核取方塊 Web 控制項的 `Checked` 屬性。 為了讓 [新增]、[編輯] 和 [刪除] 按鈕在按一下時觸發特定的 FormView 行為，請務必將其 `CommandName` 值分別設定為 `New`、`Edit`和 `Delete`。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample8.aspx)]

[圖 22] 顯示在瀏覽器中觀看 FormView 的 `ItemTemplate`。 每個產品欄位都會以底部的 [新增]、[編輯] 和 [刪除] 按鈕列出。

[![預設使用者名稱為 FormView ItemTemplate 會列出每個產品欄位，以及 [新增]、[編輯] 和 [刪除] 按鈕](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image54.png)

**圖 22**：預設使用者名稱為 FormView `ItemTemplate` 會列出每個產品欄位，以及 [新增]、[編輯] 和 [刪除] 按鈕（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image56.png)）

就像 GridView 和 DetailsView 一樣，按一下 [刪除] 按鈕或 `CommandName` 屬性設為 [刪除] 的任何按鈕、LinkButton 或 ImageButton，都會導致回傳、根據 FormView 的 `DataKeyNames` 值填入 ObjectDataSource 的 `DeleteParameters`，以及叫用 ObjectDataSource 的 `Delete()` 方法。

當按一下 [編輯] 按鈕時，回傳接踵而來和資料會重新系結至 `EditItemTemplate`，這會負責呈現編輯介面。 此介面包含用於編輯資料的 Web 控制項，以及 [更新] 和 [取消] 按鈕。 Visual Studio 產生的預設 `EditItemTemplate` 包含任何自動遞增欄位（`ProductID`）的標籤、每個非布林值欄位的 TextBox，以及每個布林值欄位的核取方塊。 這個行為與 GridView 和 DetailsView 控制項中自動產生的 BoundFields 非常類似。

> [!NOTE]
> FormView 自動產生 `EditItemTemplate` 的一個小問題是，它會針對唯讀的欄位呈現 TextBox Web 控制項，例如 `CategoryName` 和 `SupplierName`。 我們很快就會說明如何將此帳戶。

`EditItemTemplate` 中的 TextBox 控制項使用*雙向資料*系結，將其 `Text` 屬性系結至其對應資料欄位的值。 雙向資料系結（以 `<%# Bind("dataField") %>`表示）會在將資料系結至範本，以及填入 ObjectDataSource 的參數來插入或編輯記錄時，執行資料系結。 也就是說，當使用者從 `ItemTemplate`按一下 [編輯] 按鈕時，`Bind()` 方法會傳回指定的資料欄值。 使用者進行變更並按一下 [更新] 之後，會將回傳的值（對應至使用 `Bind()` 所指定的資料欄位）套用至 ObjectDataSource 的 `UpdateParameters`。 或者，單向資料系結（以 `<%# Eval("dataField") %>`表示）只會在將資料系結至範本時，才會抓取資料欄位值，*而且不會*在回傳時將使用者輸入的值傳回資料來源的參數。

下列宣告式標記會顯示 FormView 的 `EditItemTemplate`。 請注意，這裡的資料系結語法中會使用 `Bind()` 方法，而且 [更新] 和 [取消] 按鈕 Web 控制項會據以設定其 `CommandName` 屬性。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample9.aspx)]

此時，我們的 `EditItemTemplate`會導致擲回例外狀況（如果我們嘗試使用的話）。 問題在於 [`CategoryName`] 和 [`SupplierName`] 欄位會轉譯為 `EditItemTemplate`中的 TextBox Web 控制項。 我們必須將這些文字方塊變更為標籤，或將它們全部移除。 讓我們直接從 `EditItemTemplate`中刪除它們。

[圖 23] 顯示在按一下 [編輯] 按鈕以進行 Chai 之後，瀏覽器中的 FormView。 請注意，`ItemTemplate` 中顯示的 [`SupplierName`] 和 [`CategoryName`] 欄位已不存在，因為我們只是從 `EditItemTemplate`中移除它們。 按一下 [更新] 按鈕時，FormView 會繼續進行與 GridView 和 DetailsView 控制項相同的步驟順序。

[![依預設，EditItemTemplate 會將每個可編輯的產品欄位顯示為文字方塊或核取方塊](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image57.png)

**圖 23**：根據預設，`EditItemTemplate` 會將每個可編輯的產品欄位顯示為文字方塊或核取方塊（[按一下以查看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image59.png)）

當按一下 [插入] 按鈕時，會將 FormView 的 `ItemTemplate` 回傳接踵而來。 不過，因為加入了新的記錄，所以沒有任何資料系結到 FormView。 `InsertItemTemplate` 介面包含的 Web 控制項，可用於加入新記錄以及 [插入] 和 [取消] 按鈕。 Visual Studio 產生的預設 `InsertItemTemplate` 包含每個非布林值欄位的文字方塊，以及每個布林值欄位的核取方塊，類似于自動產生的 `EditItemTemplate`介面。 TextBox 控制項的 `Text` 屬性會使用雙向資料系結，系結至其對應資料欄位的值。

下列宣告式標記會顯示 FormView 的 `InsertItemTemplate`。 請注意，這裡的資料系結語法中會使用 `Bind()` 方法，而且 [插入] 和 [取消] 按鈕 Web 控制項會據以設定其 `CommandName` 屬性。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample10.aspx)]

奧妙會使用 FormView 的自動產生 `InsertItemTemplate`。 具體來說，即使是唯讀的欄位，也會建立 TextBox Web 控制項，例如 `CategoryName` 和 `SupplierName`。 如同 `EditItemTemplate`，我們需要從 `InsertItemTemplate`中移除這些文字方塊。

[圖 24] 在加入新產品時，將 FormView 顯示在瀏覽器中（Acme 咖啡）。 請注意，`ItemTemplate` 中顯示的 [`SupplierName`] 和 [`CategoryName`] 欄位已不存在，因為我們剛剛將其移除。 當按一下 [插入] 按鈕時，FormView 會繼續進行與 DetailsView 控制項相同的步驟順序，並將新的記錄加入 `Products` 資料表。 [圖 25] 顯示在已插入的 FormView 中的 Acme 咖啡產品詳細資料。

[![InsertItemTemplate 規定 FormView 的插入介面](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image60.png)

**圖 24**： `InsertItemTemplate` 規定 FormView 的插入介面（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image62.png)）

[![新產品的詳細資料（Acme 咖啡）會顯示在 FormView 中](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image63.png)

**圖 25**：新產品的詳細資料（Acme 咖啡）會顯示在 FormView 中（[按一下以觀看完整大小的影像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image65.png)）

藉由將唯讀、編輯和插入介面分成三個不同的範本，FormView 可讓您更精細地控制這些介面，而不是 DetailsView 和 GridView。

> [!NOTE]
> 就像 DetailsView 一樣，FormView 的 `CurrentMode` 屬性會指出所顯示的介面，而它的 `DefaultMode` 屬性則表示在完成編輯或插入之後，FormView 傳回的模式。

## <a name="summary"></a>總結

在本教學課程中，我們探討了使用 GridView、DetailsView 和 FormView 來插入、編輯和刪除資料的基本概念。 這三個控制項都提供某種層級的內建資料修改功能，而不必在 ASP.NET 網頁中撰寫任何一行程式碼，因為資料 Web 控制項和 ObjectDataSource。 不過，簡單的點和按一下技巧會轉譯一個相當 frail 且單純的資料修改使用者介面。 為了提供驗證、插入程式設計的值、適當地處理例外狀況、自訂使用者介面等等，我們必須依賴將在接下來的幾個教學課程中討論的技術系列。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](limiting-data-modification-functionality-based-on-the-user-cs.md)
> [下一頁](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
