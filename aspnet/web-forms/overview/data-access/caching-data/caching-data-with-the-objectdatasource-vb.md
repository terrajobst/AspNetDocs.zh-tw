---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
title: 使用 ObjectDataSource 快取資料（VB） |Microsoft Docs
author: rick-anderson
description: 快取可以表示慢速和快速 Web 應用程式之間的差異。 本教學課程是四個中的第一個，深入探討 ASP.NET 中的快取 。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 2e56a733-5512-48a6-9276-70a65bbe4d5d
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 16f20d9a0f4f677073174d680418b278dba40b07
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78550488"
---
# <a name="caching-data-with-the-objectdatasource-vb"></a>使用 ObjectDataSource 快取資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_VB.exe)或[下載 PDF](caching-data-with-the-objectdatasource-vb/_static/datatutorial58vb1.pdf)

> 快取可以表示慢速和快速 Web 應用程式之間的差異。 本教學課程是四個中的第一個，深入探討 ASP.NET 中的快取。 瞭解快取的重要概念，以及如何透過 ObjectDataSource 控制項將快取套用至展示層。

## <a name="introduction"></a>簡介

在「電腦科學」中，快取是取得資料或資訊的*程式，此*程式會耗用大量資源，並將其複本儲存在更快速存取的位置。 對於資料驅動的應用程式，大型和複雜的查詢通常會耗用大部分的應用程式執行時間。 然後，在應用程式記憶體中儲存昂貴資料庫查詢的結果，通常可以改善這類應用程式的效能。

ASP.NET 2.0 提供各種快取選項。 整個網頁或使用者控制項的呈現標記都可以透過*輸出*快取進行快取。 ObjectDataSource 和 SqlDataSource 控制項也提供快取功能，因此可讓資料在控制項層級進行快取。 和 ASP.NET 的*資料*快取提供豐富的快取 API，可讓網頁開發人員以程式設計方式快取物件。 在本教學課程和接下來的三個中，我們將使用 ObjectDataSource s 快取功能以及資料快取來進行檢查。 我們也會探索如何在啟動時快取整個應用程式的資料，以及如何使用 SQL 快取相依性將快取的資料保持在最新。 這些教學課程不會探索輸出快取。 如需輸出快取的詳細資訊，請參閱[ASP.NET 2.0 中的輸出](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)快取。

您可以在架構中的任何位置套用快取，從資料存取層到展示層。 在本教學課程中，我們將探討如何透過 ObjectDataSource 控制項將快取套用至展示層。 在下一個教學課程中，我們將檢查商業邏輯層的快取資料。

## <a name="key-caching-concepts"></a>金鑰快取概念

快取可以藉由將產生並儲存其複本的資料複製到可更有效率存取的位置，大幅提升應用程式的整體效能和擴充性。 由於快取只會保存實際的基礎資料複本，因此如果基礎資料變更，它可能會過時或*過時*。 若要對抗這種情況，頁面開發人員可以使用下列其中一種方式，指出將從快取中*收回*快取專案的準則：

- 以**時間為基礎的準則**：可將專案新增至快取中的絕對或滑動持續時間。 例如，網頁開發人員可能會指出持續時間（例如60秒）。 在絕對持續期間，快取的專案會在新增至快取後的60秒收回，不論存取的頻率為何。 在滑動期間，快取的專案會在上次存取後的60秒收回。
- 以相依性為**基礎的準則**：在新增至快取時，相依性可以與專案產生關聯。 當專案的相依性變更時，它會從快取中收回。 相依性可能是檔案、另一個快取專案或兩者的組合。 ASP.NET 2.0 也允許 SQL 快取相依性，這可讓開發人員將專案新增至快取，並在基礎資料庫資料變更時將它收回。 我們將在未來的[使用 sql](using-sql-cache-dependencies-vb.md)快取相依性教學課程中，檢查 sql 快取相依性。

不論指定的收回準則為何，快取中的專案可能會在符合以時間為基礎或以相依性為基礎的準則之前*清除*。 如果快取已達到其容量，就必須先移除現有的專案，才能新增新的專案。 因此，以程式設計方式處理快取的資料時，您一定會認為快取的資料可能不存在。 我們將探討在下一個教學課程中以程式設計方式從快取存取資料時所要使用的模式，在架構中快取*資料*。

快取提供經濟實惠的方法，讓應用程式的效能更高。 [Steven Smith](http://aspadvice.com/blogs/ssmith/)闡述在他的文章中[ASP.NET Caching：技術和最佳作法](https://msdn.microsoft.com/library/aa478965.aspx)：

快取可能是取得足夠效能的好方法，而不需要大量時間和分析。 記憶體的成本很低，因此如果您可以快取30秒的輸出，而不是花費一天或一周的時間來優化您的程式碼或資料庫，請執行 caching 解決方案（假設有30秒的舊資料沒問題），然後繼續進行。 最後，不良的設計可能會趕上您，因此您應該嘗試正確地設計應用程式。 但是，如果您現在只需要取得足夠的效能，快取就會是絕佳的 [方法]，讓您在日後有時間執行此動作時，為您購買應用程式的時間。

雖然快取可以提供明顯的效能增強功能，但在所有情況下都不適用，例如使用即時、經常更新資料的應用程式，或甚至是即將過期的資料無法接受。 但對於大部分的應用程式，應該使用快取。 如需 ASP.NET 2.0 中快取的更多背景資訊，請參閱[ASP.NET 2.0 快速入門教學](https://quickstarts.asp.net/QuickStartv20/aspnet/)課程的快取[效能](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx)一節。

## <a name="step-1-creating-the-caching-web-pages"></a>步驟1：建立快取網頁

開始探索 ObjectDataSource s 快取功能之前，讓我們先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程和接下來的三篇中使用。 從新增名為 `Caching`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`

![新增快取相關教學課程的 ASP.NET 網頁](caching-data-with-the-objectdatasource-vb/_static/image1.png)

**圖 1**：新增快取相關教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`Caching`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將這個使用者控制項加入至 `Default.aspx`，方法是將它從方案總管拖曳至頁面 s 設計檢視。

[![圖2：將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](caching-data-with-the-objectdatasource-vb/_static/image3.png)](caching-data-with-the-objectdatasource-vb/_static/image2.png)

**圖 2**：圖2：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image4.png)）

最後，將這些頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，請在使用二進位資料 `<siteMapNode>`之後，加入下列標記：

[!code-xml[Main](caching-data-with-the-objectdatasource-vb/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含快取教學課程的專案。

![網站地圖現在包含快取教學課程的專案](caching-data-with-the-objectdatasource-vb/_static/image5.png)

[**圖 3**]：網站地圖現在包含快取教學課程的專案

## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>步驟2：在網頁中顯示產品清單

本教學課程會探索如何使用 ObjectDataSource control s 內建快取功能。 不過，在我們可以查看這些功能之前，我們先需要一個可供使用的頁面。 讓我們建立一個網頁，使用 GridView 列出由 `ProductsBLL` 類別的 ObjectDataSource 所抓取的產品資訊。

從開啟 [`Caching`] 資料夾中的 [`ObjectDataSource.aspx`] 頁面開始。 將 GridView 從 [工具箱] 拖曳至設計工具，將其 [`ID`] 屬性設定為 [`Products`]，然後從其智慧標籤，選擇將其系結至名為 `ProductsDataSource`的新 ObjectDataSource 控制項。 設定 ObjectDataSource 以與 `ProductsBLL` 類別搭配使用。

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別](caching-data-with-the-objectdatasource-vb/_static/image7.png)](caching-data-with-the-objectdatasource-vb/_static/image6.png)

**圖 4**：設定 ObjectDataSource 使用 `ProductsBLL` 類別（[按一下以查看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image8.png)）

在此頁面中，我們將建立可編輯的 GridView，讓我們可以檢查 ObjectDataSource 中快取的資料是透過 GridView 的介面修改時所發生的情況。 將 [選取] 索引標籤中的下拉式清單保留為預設值 `GetProducts()`，但將 [更新] 索引標籤中選取的專案變更為接受 `productName`、`unitPrice`和 `productID` 做為其輸入參數的 `UpdateProduct` 多載。

[![將 [更新] 索引標籤 s 下拉式清單設定為適當的 UpdateProduct 多載](caching-data-with-the-objectdatasource-vb/_static/image10.png)](caching-data-with-the-objectdatasource-vb/_static/image9.png)

**圖 5**：將 [更新] 索引標籤 s 下拉式清單設定為適當的 `UpdateProduct` 多載（[按一下以查看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image11.png)）

最後，將 [插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]，然後按一下 [完成]。 完成 [設定資料來源] 時，Visual Studio 會將 ObjectDataSource 的 `OldValuesParameterFormatString` 屬性設定為 [`original_{0}`]。 如如何[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教學課程中所述，您必須從宣告式語法中移除此屬性，或將其設回預設值 `{0}`，才能讓更新工作流程繼續進行，而不會發生錯誤。

此外，當 wizard 完成時 Visual Studio 會針對每個產品資料欄位，將欄位加入至 GridView。 移除 `ProductName`、`CategoryName`和 `UnitPrice` BoundFields 以外的所有。 接下來，分別將每個 BoundFields 的 `HeaderText` 屬性更新為 [產品]、[類別] 和 [價格]。 因為 `ProductName` 欄位是必要的，所以請將 BoundField 轉換成 TemplateField，並將 RequiredFieldValidator 新增至 `EditItemTemplate`。 同樣地，將 `UnitPrice` BoundField 轉換成 TemplateField 並加入 CompareValidator，以確保使用者輸入的值是大於或等於零的有效貨幣值。 除了這些修改以外，您可以隨意執行任何美觀變更，例如靠右對齊 `UnitPrice` 值，或指定其唯讀和編輯介面中 `UnitPrice` 文字的格式。

勾選 GridView s 智慧標籤中的 [啟用編輯] 核取方塊，讓 GridView 可供編輯。 另請核取 [啟用分頁] 和 [啟用排序] 核取方塊。

> [!NOTE]
> 需要複習如何自訂 GridView 的編輯介面？ 若是如此，請回頭參閱[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教學課程。

[![啟用 GridView 的編輯、排序和分頁支援](caching-data-with-the-objectdatasource-vb/_static/image13.png)](caching-data-with-the-objectdatasource-vb/_static/image12.png)

**圖 6**：啟用 GridView 支援以進行編輯、排序和分頁（[按一下以查看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image14.png)）

進行這些 GridView 修改之後，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](caching-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

如 [圖 7] 所示，可編輯的 GridView 會列出資料庫中每個產品的名稱、類別和價格。 請花點時間測試頁面的功能排序結果、逐頁流覽，然後編輯記錄。

[![每個產品的名稱、類別和價格都會列在可排序、可分頁、可編輯的 GridView 中](caching-data-with-the-objectdatasource-vb/_static/image16.png)](caching-data-with-the-objectdatasource-vb/_static/image15.png)

**圖 7**：每個產品的名稱、類別和價格都會列在可排序、可分頁、可編輯的 GridView 中（[按一下以查看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image17.png)）

## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>步驟3：檢查 ObjectDataSource 何時要求資料

`Products` GridView 會藉由叫用 `ProductsDataSource` ObjectDataSource 的 `Select` 方法，來抓取其資料以顯示。 這個 ObjectDataSource 會建立 `ProductsBLL` 類別的商務邏輯層實例，並呼叫它的 `GetProducts()` 方法，然後再呼叫資料存取層 `ProductsTableAdapter` s `GetProducts()` 方法。 DAL 方法會連接到 Northwind 資料庫，併發出已設定的 `SELECT` 查詢。 然後，這項資料會傳回到 DAL，並在 `NorthwindDataTable`中將它封裝在一起。 DataTable 物件會傳回給 BLL，其會將它傳回給 GridView，然後將它傳回給 GridView。 然後 GridView 會為 DataTable 中的每個 `DataRow` 建立一個 `GridViewRow` 物件，而每個 `GridViewRow` 最終會轉譯成傳回給用戶端的 HTML，並顯示在造訪者的瀏覽器上。

每次 GridView 需要系結至其基礎資料時，就會發生這個事件順序。 當第一次造訪頁面、在排序 GridView 時，或透過其內建編輯或刪除介面修改 GridView 的資料時，就會發生這種情況。 如果 GridView s 檢視狀態為停用，則 GridView 也會在每次回傳時重新系結。 GridView 也可以藉由呼叫其 `DataBind()` 方法，明確地重新系結至其資料。

為了充分感謝從資料庫抓取資料的頻率，讓 s 顯示訊息，指出重新抓取資料的時間。 在名為 `ODSEvents`的 GridView 上方新增標籤 Web 控制項。 清除其 [`Text`] 屬性，並將其 [`EnableViewState`] 屬性設定為 [`False`]。 在標籤底下，新增按鈕 Web 控制項，並將其 `Text` 屬性設為回傳。

[![將標籤和按鈕新增至 GridView 上方的頁面](caching-data-with-the-objectdatasource-vb/_static/image19.png)](caching-data-with-the-objectdatasource-vb/_static/image18.png)

**圖 8**：將標籤和按鈕新增至 GridView 上方的頁面（[按一下以觀看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image20.png)）

在資料存取工作流程期間，ObjectDataSource s `Selecting` 事件會在建立基礎物件並叫用其設定的方法之前引發。 建立此事件的事件處理常式，並新增下列程式碼：

[!code-vb[Main](caching-data-with-the-objectdatasource-vb/samples/sample3.vb)]

每次 ObjectDataSource 對資料的架構提出要求時，標籤將會顯示 [選取事件引發] 的文字。

在瀏覽器中造訪此頁面。 第一次流覽頁面時，會顯示 [選取引發的事件] 文字。 按一下 [回傳] 按鈕，並注意文字會消失（假設 GridView 的 `EnableViewState` 屬性設定為 `True`（預設值）。 這是因為在回傳時，GridView 會從其 view 狀態重建，因此不會針對其資料轉換成 ObjectDataSource。 不過，排序、分頁或編輯資料會導致 GridView 重新系結至其資料來源，因此會重新出現選取事件引發的文字。

[![當 GridView 重新系結至其資料來源時，會顯示選取 [引發的事件]](caching-data-with-the-objectdatasource-vb/_static/image22.png)](caching-data-with-the-objectdatasource-vb/_static/image21.png)

**圖 9**：每當 GridView 重新系結至其資料來源時，就會顯示選取 [引發的事件] （[按一下以查看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image23.png)）

[![按一下回傳按鈕，會導致 GridView 從其檢視狀態重新構建](caching-data-with-the-objectdatasource-vb/_static/image25.png)](caching-data-with-the-objectdatasource-vb/_static/image24.png)

**圖 10**：按一下回傳按鈕會導致 GridView 從其檢視狀態重新構建（[按一下以觀看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image26.png)）

每次資料經過分頁或進行排序時，抓取資料庫資料似乎會浪費。 畢竟，因為我們重新使用預設分頁，所以 ObjectDataSource 會在顯示第一頁時，抓取所有的記錄。 即使 GridView 並未提供排序和分頁支援，每次使用者第一次造訪頁面時，都必須從資料庫中取出資料（如果停用 view 狀態，則會在每個回傳上）。 但是，如果 GridView 向所有使用者顯示相同的資料，這些額外的資料庫要求就是多餘的。 為什麼不快取從 `GetProducts()` 方法傳回的結果，並將 GridView 系結至這些快取的結果？

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>步驟4：使用 ObjectDataSource 快取資料

藉由只設定幾個屬性，可以將 ObjectDataSource 設定為在 ASP.NET 資料快取中自動快取其抓取的資料。 下列清單摘要說明 ObjectDataSource 的快取相關屬性：

- [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx)必須設定為 `True` 才能啟用快取。 預設為 `False`。
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx)快取資料的時間量（以秒為單位）。 預設值為 0。 只有在 `True` `EnableCaching`，且 `CacheDuration` 設定為大於零的值時，ObjectDataSource 才會快取資料。
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx)可以設定為 `Absolute` 或 `Sliding`。 如果 `Absolute`，ObjectDataSource 會快取其抓取的資料達 `CacheDuration` 秒;如果 `Sliding`，則資料只有在未被存取 `CacheDuration` 秒之後才會到期。 預設為 `Absolute`。
- [CacheKeyDependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx)使用此屬性，將 ObjectDataSource s 快取專案與現有的快取相依性產生關聯。 ObjectDataSource 的資料項目可以藉由將其相關聯的 `CacheKeyDependency`過期，從快取中提前收回。 此屬性最常用於將 SQL 快取相依性與 ObjectDataSource s 快取建立關聯，我們將在未來[使用 SQL](using-sql-cache-dependencies-vb.md)快取相依性教學課程來探索該主題。

讓我們將 `ProductsDataSource` ObjectDataSource 設定為在絕對規模上快取30秒的資料。 將 [ObjectDataSource s `EnableCaching`] 屬性設定為 [`True`]，將其 [`CacheDuration`] 屬性設為30。 將 [`CacheExpirationPolicy`] 屬性保持設定為預設值 [`Absolute`]。

[![將 ObjectDataSource 設定為快取其資料30秒](caching-data-with-the-objectdatasource-vb/_static/image28.png)](caching-data-with-the-objectdatasource-vb/_static/image27.png)

**圖 11**：設定 ObjectDataSource 快取其資料30秒（[按一下以查看完整大小的影像](caching-data-with-the-objectdatasource-vb/_static/image29.png)）

儲存您的變更，並在瀏覽器中造訪此頁面。 當您第一次流覽頁面時，將會出現選取事件引發的文字，因為一開始資料不在快取中。 但是，按一下回傳按鈕、排序、分頁，或按一下 [編輯] 或 [取消] 按鈕所觸發的後續回傳，並*不*會重新顯示選取事件引發的文字。 這是因為只有當 ObjectDataSource 從其基礎物件取得其資料時，才會引發 `Selecting` 事件;如果從資料快取中提取資料，則不會引發 `Selecting` 事件。

30秒之後，資料將會從快取中收回。 如果叫用 ObjectDataSource s `Insert`、`Update`或 `Delete` 方法，資料也會從快取中收回。 因此，經過30秒之後，或按一下 [更新] 按鈕、排序、分頁，或按一下 [編輯] 或 [取消] 按鈕，將會導致 ObjectDataSource 從其基礎物件取得其資料，並顯示在 `Selecting` 事件引發時選取事件引發的文字。 這些傳回的結果會放回資料快取中。

> [!NOTE]
> 如果您看到經常選取事件引發的文字，即使您預期 ObjectDataSource 會使用快取的資料，也可能是因為記憶體限制。 如果沒有足夠的可用記憶體，ObjectDataSource 新增至快取的資料可能已被清除。 如果 ObjectDataSource 似乎沒有正確快取資料，或只是偶爾快取資料，請關閉一些應用程式以釋放記憶體，然後再試一次。

[圖 12] 說明 ObjectDataSource s 快取工作流程。 當選取事件引發的文字出現在螢幕上時，這是因為資料不在快取中，而且必須從基礎物件中抓取。 不過，此文字遺失時，是因為資料可從快取中取得。 從快取傳回資料時，不會呼叫基礎物件，因此不會執行任何資料庫查詢。

![ObjectDataSource 會儲存並從資料快取中抓取其資料](caching-data-with-the-objectdatasource-vb/_static/image30.png)

**圖 12**： ObjectDataSource 儲存和抓取資料快取中的資料

每個 ASP.NET 應用程式都有自己的資料快取實例，其會在所有頁面和訪客之間共用。 這表示由 ObjectDataSource 儲存在資料快取中的資料，同樣會在造訪該頁面的所有使用者之間共用。 若要確認這一點，請在瀏覽器中開啟 [`ObjectDataSource.aspx`] 頁面。 第一次流覽頁面時，將會顯示 [選取引發的事件] 文字（假設先前的測試加入快取的資料現在已經被收回）。 開啟第二個瀏覽器實例，並將 URL 從第一個瀏覽器實例複製並貼到第二個。 在第二個瀏覽器實例中，不會顯示選取事件引發的文字，因為它使用與第一個相同的快取資料。

將其抓取的資料插入快取時，ObjectDataSource 會使用包含下列值的快取索引鍵值： `CacheDuration` 和 `CacheExpirationPolicy` 屬性值;ObjectDataSource 所使用之基礎商務物件的型別，它是透過[`TypeName` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx)（在此範例中為`ProductsBLL`）所指定。`SelectMethod` 屬性的值，以及 `SelectParameters` 集合中參數的名稱和值;以及在執行[自訂分頁](../paging-and-sorting/paging-and-sorting-report-data-vb.md)時，所使用的 `StartRowIndex` 和 `MaximumRows` 屬性的值。

將快取索引鍵值製作為這些屬性的組合，可確保在這些值變更時，有唯一的快取專案。 例如，在過去的教學課程中，我們探討了如何使用 `ProductsBLL` 類別 `GetProductsByCategoryID(categoryID)`，它會傳回指定分類的所有產品。 一位使用者可能會進入頁面和觀看飲料，其 `CategoryID` 為1。 如果 ObjectDataSource 快取其結果，而不考慮 `SelectParameters` 值，則當另一位使用者前往頁面來 condiments 時，當飲料產品在快取中時，他們會看到快取的飲料產品而非 condiments。 根據這些屬性來改變快取索引鍵，其中包括 `SelectParameters`的值，ObjectDataSource 會為飲料和 condiments 維護個別的快取專案。

## <a name="stale-data-concerns"></a>過時的資料考慮

當叫用其 `Insert`、`Update`或 `Delete` 方法的任何一個時，ObjectDataSource 會自動從快取中收回其專案。 這有助於防止過時的資料，方法是在透過頁面修改資料時清除快取專案。 不過，使用快取的 ObjectDataSource 仍然可以顯示過時的資料。 在最簡單的情況下，這可能是因為資料直接在資料庫中變更所造成。 可能是資料庫管理員剛執行的腳本會修改資料庫中的部分記錄。

此案例也可能會以更細微的方式展開。 雖然 ObjectDataSource 會在呼叫其中一個資料修改方法時從快取中收回其專案，但已移除的快取專案是用於 ObjectDataSource 的屬性值（`CacheDuration`、`TypeName`、`SelectMethod`等等）組合。 如果您有兩個使用不同 `SelectMethods` 或 `SelectParameters`的 ObjectDataSources，但仍可更新相同的資料，則一個 ObjectDataSource 可能會更新一個資料列，並使其本身的快取專案失效，但仍會從快取中提供第二個 ObjectDataSource 的對應資料列。 我鼓勵您建立頁面來展現這種功能。 建立頁面，以顯示可編輯的 GridView，從使用快取的 ObjectDataSource 提取其資料，並設定為從 `ProductsBLL` 類別的 `GetProducts()` 方法取得資料。 將另一個可編輯的 GridView 和 ObjectDataSource 加入此頁面（或另一個），但在此第二個 ObjectDataSource 中，它會使用 `GetProductsByCategoryID(categoryID)` 方法。 由於這兩個 ObjectDataSources `SelectMethod` 屬性不同，因此它們各自有快取的值。 如果您在一個方格中編輯某個產品，下次將資料系結回另一個方格（藉由分頁、排序等等）時，它仍然會提供舊的快取資料，而不會反映其他方格所做的變更。

簡單地說，如果您願意擁有過時資料的潛能，請只使用以時間為基礎的 expiries，並在資料的有效期限很重要的案例中使用較短的 expiries。 如果無法接受過時的資料，請放棄快取或使用 SQL 快取相依性（假設它是您要重新快取的資料庫資料）。 我們將在未來的教學課程中探索 SQL 快取相依性。

## <a name="summary"></a>總結

在本教學課程中，我們已檢查 ObjectDataSource s 內建快取功能。 只要設定一些屬性，我們就可以指示 ObjectDataSource 快取從指定的 `SelectMethod` 傳回的結果到 ASP.NET 資料快取。 [`CacheDuration`] 和 [`CacheExpirationPolicy`] 屬性會指出專案的快取持續時間，以及其為絕對或滑動期限。 `CacheKeyDependency` 屬性會將所有 ObjectDataSource s 快取專案與現有的快取相依性產生關聯。 這可以用來從快取中收回 ObjectDataSource 的專案，然後再達到以時間為基礎的到期日，而且通常會搭配 SQL 快取相依性使用。

因為 ObjectDataSource 只會將其值快取至資料快取，所以我們可以透過程式設計方式複寫 ObjectDataSource 的內建功能。 在展示層執行此動作並不合理，因為 ObjectDataSource 提供了現成的這項功能，但我們可以在架構的個別層級中執行快取功能。 若要這麼做，我們必須重複 ObjectDataSource 所使用的相同邏輯。 我們將在下一個教學課程中探索如何以程式設計方式使用架構中的資料快取。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET Caching：技術和最佳作法](https://msdn.microsoft.com/library/aa478965.aspx)
- [.NET Framework 應用程式的快取架構指南](https://msdn.microsoft.com/library/ee817645.aspx)
- [ASP.NET 2.0 中的輸出快取](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](using-sql-cache-dependencies-cs.md)
> [下一頁](caching-data-in-the-architecture-vb.md)
