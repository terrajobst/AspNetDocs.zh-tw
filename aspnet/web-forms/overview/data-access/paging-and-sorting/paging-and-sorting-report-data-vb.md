---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
title: 分頁和排序報表資料（VB） |Microsoft Docs
author: rick-anderson
description: 分頁和排序是在線上應用程式中顯示資料時的兩個很常見的功能。 在本教學課程中，我們將先介紹如何新增排序和 。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: b895e37e-0e69-45cc-a7e4-17ddd2e1b38d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 6785b5cd2d4d3a2c2e7f2c2fea93f5cd5e2fdf24
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619231"
---
# <a name="paging-and-sorting-report-data-vb"></a>分頁和排序報告資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe)或[下載 PDF](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)

> 分頁和排序是在線上應用程式中顯示資料時的兩個很常見的功能。 在本教學課程中，我們將先探討如何將排序和分頁新增至我們的報表，我們將在未來的教學課程中建立這些記錄。

## <a name="introduction"></a>簡介

分頁和排序是在線上應用程式中顯示資料時的兩個很常見的功能。 例如，搜尋線上書店的 ASP.NET 書籍時，可能會有數百份這類書籍，但列出搜尋結果的報表只會列出每頁十個相符專案。 此外，結果也可以依標題、價格、頁面計數、作者姓名等等排序。 雖然過去23個教學課程已檢查如何建立各種報表，包括允許新增、編輯和刪除資料的介面，但我們並未探討如何排序資料，以及我們在 DetailsView 和 FormView 中所見到的唯一分頁範例controls.

在本教學課程中，我們將瞭解如何將排序和分頁新增至我們的報表，只要檢查幾個核取方塊即可完成。 可惜的是，這種簡化的執行有其缺點，排序介面會留下一個需要的一點，而分頁常式則不是設計來有效率地分頁處理大型結果集。 未來的教學課程將探討如何克服現成分頁和排序解決方案的限制。

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>步驟1：新增分頁和排序教學課程網頁

開始進行本教學課程之前，先花點時間新增本教學課程所需的 ASP.NET 網頁，以及接下來的三項。 首先，在名為 `PagingAndSorting`的專案中建立新的資料夾。 接下來，將下列五個 ASP.NET 網頁新增到此資料夾，並將它們全部設定為使用主版頁面 `Site.master`：

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`

![建立 PagingAndSorting 資料夾並新增教學課程 ASP.NET 網頁](paging-and-sorting-report-data-vb/_static/image1.png)

**圖 1**：建立 PagingAndSorting 資料夾並新增教學課程 ASP.NET 網頁

接下來，開啟 [`Default.aspx`] 頁面，並將 [`SectionLevelTutorialListing.ascx` 使用者] 控制項從 [`UserControls`] 資料夾拖曳到設計介面上。 我們在[主版頁面和網站導覽](../introduction/master-pages-and-site-navigation-vb.md)教學課程中建立的這個使用者控制項，會列舉網站地圖，並在項目符號清單的目前區段中顯示這些教學課程。

![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](paging-and-sorting-report-data-vb/_static/image2.png)

**圖 2**：將 SectionLevelTutorialListing 的 .Ascx 使用者控制項新增至 default.aspx

為了讓項目符號清單顯示我們將建立的分頁和排序教學課程，我們需要將它們新增至網站地圖。 開啟 `Web.sitemap` 檔案，並在編輯、插入及刪除網站地圖節點標記之後，新增下列標記：

[!code-xml[Main](paging-and-sorting-report-data-vb/samples/sample1.xml)]

![更新網站地圖以包含新的 ASP.NET 網頁](paging-and-sorting-report-data-vb/_static/image3.png)

**圖 3**：更新網站地圖以包含新的 ASP.NET 網頁

## <a name="step-2-displaying-product-information-in-a-gridview"></a>步驟2：在 GridView 中顯示產品資訊

在實際實行分頁和排序功能之前，先讓我們先建立一個標準不可排序、不可分頁的 GridView，其中列出產品資訊。 這是我們在整個教學課程系列之前完成過多次的工作，因此應該熟悉這些步驟。 一開始先開啟 [`SimplePagingSorting.aspx`] 頁面，並將 GridView 控制項從 [工具箱] 拖曳至設計工具，將其 [`ID`] 屬性設定為 [`Products`]。 接下來，建立新的 ObjectDataSource，使用 ProductsBLL 類別 s `GetProducts()` 方法來傳回所有產品資訊。

![使用 GetProducts （）方法取出所有產品的相關資訊](paging-and-sorting-report-data-vb/_static/image4.png)

**圖 4**：使用 GetProducts （）方法取出所有產品的相關資訊

因為這份報表是唯讀報表，所以不需要將 ObjectDataSource s `Insert()`、`Update()`或 `Delete()` 方法對應到對應的 `ProductsBLL` 方法。因此，請從 [更新]、[插入] 和 [刪除] 索引標籤的下拉式清單中選擇 [（無）]。

![在 [更新]、[插入] 和 [刪除] 索引標籤的下拉式清單中，選擇 [（無）] 選項](paging-and-sorting-report-data-vb/_static/image5.png)

[**圖 5**]：在 [更新]、[插入] 和 [刪除] 索引標籤的下拉式清單中，選擇 [（無）] 選項

接下來，讓我們自訂 GridView 的欄位，只顯示產品名稱、供應商、類別、價格和已停止的狀態。 此外，您可以隨意進行任何欄位層級的格式變更，例如調整 `HeaderText` 屬性，或將價格格式化為貨幣。 這些變更之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample2.aspx)]

[圖 6] 顯示透過瀏覽器觀看的進度。 請注意，此頁面會在單一畫面中列出所有產品，並顯示每個產品的名稱、類別、供應商、價格和已停止狀態。

[列出每個產品 ![](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)

**圖 6**：列出每項產品（[按一下以觀看完整大小的影像](paging-and-sorting-report-data-vb/_static/image8.png)）

## <a name="step-3-adding-paging-support"></a>步驟3：新增分頁支援

在一個畫面上列出*所有*產品，可能會導致使用者流覽資料的資訊超載。 為了讓結果更容易管理，我們可以將資料分解成較小的資料頁，讓使用者一次一頁就能逐步執行資料。 若要完成此動作，只需核取 GridView 的智慧標籤中的 [啟用分頁] 核取方塊（這會將 GridView 的[`AllowPaging` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx)設定為 `true`）。

[![核取 [啟用分頁] 核取方塊以新增分頁支援](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)

**圖 7**：核取 [啟用分頁] 核取方塊以新增分頁支援（[按一下以查看完整大小的影像](paging-and-sorting-report-data-vb/_static/image11.png)）

啟用分頁會限制每頁顯示的記錄數目，並將*分頁介面*新增至 GridView。 如 [圖 7] 所示，預設的分頁介面是一系列的頁碼，可讓使用者從一頁數據快速流覽至另一個頁面。 此分頁介面看起來應該很熟悉，因為在過去的教學課程中，將分頁支援新增至 DetailsView 和 FormView 控制項時，就會看到這種情況。

DetailsView 和 FormView 控制項都只會針對每個頁面顯示一筆記錄。 不過，GridView 會諮詢其[`PageSize` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx)，以決定每個頁面顯示的記錄數目（此屬性預設為10的值）。

這個 GridView、DetailsView 和 FormView s 分頁介面可以使用下列屬性自訂：

- `PagerStyle` 表示分頁介面的樣式資訊;可以指定如 `BackColor`、`ForeColor`、`CssClass`、`HorizontalAlign`等設定。
- `PagerSettings` 包含可自訂分頁介面功能的屬性系列;`PageButtonCount` 指出分頁介面中顯示的最大數值頁數（預設值為10）;[`Mode` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx)會指出分頁介面的運作方式，而且可以設定為： 

    - `NextPrevious` 顯示 [下一步] 和 [上一個] 按鈕，讓使用者一次向前或向後一頁
    - 除了 [下一步] 和 [上一個] 按鈕以外，還會包含第一個和最後一個按鈕，讓使用者快速移至第一頁或最後一頁的資料。 `NextPreviousFirstLast`
    - `Numeric` 顯示一系列的頁碼，讓使用者立即跳到任何頁面
    - 除了頁碼以外，`NumericFirstLast` 包含第一個和最後一個按鈕，可讓使用者快速地移至第一頁或最後一頁的資料;只有在無法容納所有數值頁碼的情況下，才會顯示第一個/最後一個按鈕

此外，GridView、DetailsView 和 FormView 全都提供 `PageIndex` 和 `PageCount` 屬性，分別指出目前正在查看的頁面和資料的總頁數。 `PageIndex` 屬性是從0開始編制索引，這表示當您在查看資料的第一頁時，`PageIndex` 會等於0。 另一方面，`PageCount`會從1開始計數，這表示 `PageIndex` 限制為0到 `PageCount - 1`之間的值。

讓我們花一點時間來改善 GridView 分頁介面的預設面板。 具體而言，讓分頁介面靠右對齊淺灰色背景。 我們不會直接透過 GridView 的 `PagerStyle` 屬性來設定這些屬性，而是在名為 `PagerRowStyle` 的 `Styles.css` 中建立 CSS 類別，然後透過我們的主題指派 `PagerStyle` s `CssClass` 屬性。 首先，開啟 `Styles.css` 並新增下列 CSS 類別定義：

[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample3.css)]

接下來，在 [`App_Themes`] 資料夾內的 [`DataWebControls`] 資料夾中開啟 `GridView.skin` 檔案。 如我們在*主版頁面和網站導覽*教學課程中所討論的，您可以使用面板檔案來指定 Web 控制項的預設屬性值。 因此，請擴充現有的設定，以包含將 `PagerStyle` s `CssClass` 屬性設定為 `PagerRowStyle`。 同時，讓我們設定分頁介面，使用 `NumericFirstLast` 分頁介面來顯示最多五個數值頁面按鈕。

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>分頁使用者體驗

[圖 8] 顯示當 GridView 的 [啟用分頁] 核取方塊已核取，且已透過 `GridView.skin` 檔案進行 `PagerStyle` 和 `PagerSettings` 設定之後，透過瀏覽器造訪的網頁。 請注意，只會顯示十筆記錄，而分頁介面則表示我們正在查看資料的第一頁。

[已啟用分頁的 ![，一次只會顯示記錄的子集](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)

**圖 8**：啟用分頁時，一次只會顯示記錄的子集（[按一下以觀看完整大小的影像](paging-and-sorting-report-data-vb/_static/image14.png)）

當使用者按一下分頁介面中的其中一個頁碼時，回傳接踵而來和頁面重載會顯示要求的頁面記錄。 [圖 9] 顯示選擇觀看最後一頁的資料之後的結果。 請注意，最後一頁只有一筆記錄。這是因為總共有81筆記錄，因此每頁有八頁的10筆記錄，再加上一頁含有一筆獨立的記錄。

[![按一下頁碼會導致回傳，並顯示適當的記錄子集](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)

**圖 9**：按一下頁碼會導致回傳，並顯示適當的記錄子集（[按一下以查看完整大小的影像](paging-and-sorting-report-data-vb/_static/image17.png)）

## <a name="paging-s-server-side-workflow"></a>分頁 s 伺服器端工作流程

當使用者按一下分頁介面中的按鈕時，回傳接踵而來和下列伺服器端工作流程會開始：

1. GridView s （或 DetailsView 或 FormView） `PageIndexChanging` 事件引發
2. ObjectDataSource 會重新要求 BLL 的*所有*資料;GridView 的 `PageIndex` 和 `PageSize` 屬性值是用來決定要在 GridView 中顯示的 BLL 所傳回的記錄
3. GridView s `PageIndexChanged` 事件引發

在步驟2中，ObjectDataSource 會重新要求其資料來源中的所有資料。 這種分頁方式通常稱為*預設分頁*，這是將 `AllowPaging` 屬性設定為 `true`時，預設會使用的分頁行為。 使用預設分頁時，資料 Web 控制項輕鬆自在管理會抓取每一頁數據的所有記錄，即使只有部分記錄會實際轉譯為傳送至瀏覽器的 HTML。 除非是由 BLL 或 ObjectDataSource 快取資料庫資料，否則預設分頁對於夠大的結果集或具有許多並行使用者的 web 應用程式而言是無法使用的。

在下一個教學課程中，我們將探討如何執行*自訂分頁*。 透過自訂分頁，您可以明確地指示 ObjectDataSource 只取得所要求資料頁面所需的一組精確記錄。 就像您想像的一樣，自訂分頁會大幅提升分頁處理大型結果集的效率。

> [!NOTE]
> 雖然預設分頁不適合用來分頁到夠大的結果集或具有許多同時使用者的網站，但請注意，自訂分頁需要更多的變更和工作來執行，而且不像勾選核取方塊一樣簡單（預設為分頁）。 因此，預設分頁可能是小型、低流量網站的理想選擇，或是透過相對較小的結果集進行分頁時，因為它更容易且更快速地執行。

比方說，如果我們知道我們的資料庫永遠不會有超過100的產品，自訂分頁所能獲得的最小效能增益，可能會因執行它所需的工作而位移。 不過，如果我們可能一天有數千或數十個產品，則*不*會執行自訂分頁會大幅阻礙應用程式的擴充性。

## <a name="step-4-customizing-the-paging-experience"></a>步驟4：自訂分頁體驗

資料 Web 控制項提供一些屬性，可用於增強使用者的分頁體驗。 例如，`PageCount` 屬性會指出有多少總頁數，而 `PageIndex` 屬性則表示目前正在流覽的頁面，而且可以設定為將使用者快速移至特定的頁面。 為了說明如何使用這些屬性來改善使用者的分頁體驗，讓我們將標籤 Web 控制項新增至頁面，通知使用者目前正在造訪的頁面，以及可讓他們快速跳到任何指定頁面的 DropDownList 控制項.

首先，將標籤 Web 控制項新增至您的頁面，將其 `ID` 屬性設定為 `PagingInformation`，並清除其 `Text` 屬性。 接下來，建立 GridView `DataBound` 事件的事件處理常式，並加入下列程式碼：

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample5.vb)]

這個事件處理常式會將 `PagingInformation` 標籤 `Text` 屬性指派給訊息，通知使用者目前正在造訪的頁面 `Products.PageIndex + 1` 超出總頁數 `Products.PageCount` （我們會將1加到 `Products.PageIndex` 屬性，因為 `PageIndex` 是從0開始編制索引）。 我選擇 [在 `DataBound` 事件處理常式中指派此標籤 `Text`] 屬性，而不是 `PageIndexChanged` 事件處理常式，因為 `DataBound` 事件會在每次資料系結至 GridView 時引發，而 `PageIndexChanged` 事件處理常式只會在頁面索引變更時引發。 當 GridView 最初是第一頁上的資料系結時，`PageIndexChanging` 事件不會引發（而 `DataBound` 事件則是）。

透過這項新增功能，使用者現在會看到一則訊息，指出他們正在造訪的網頁，以及有多少總數據頁面。

[![目前的頁碼和總頁面數](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)

**圖 10**：顯示目前的頁碼和總頁數（[按一下以觀看完整大小的影像](paging-and-sorting-report-data-vb/_static/image20.png)）

除了 [標籤] 控制項以外，讓同時也新增 DropDownList 控制項，其中列出 GridView 中的頁碼，並已選取目前所看到的頁面。 這裡的想法是，使用者只要從 DropDownList 中選取新的頁面索引，就可以快速地從目前的頁面跳到另一頁。 首先，將 DropDownList 新增至設計工具，將其 `ID` 屬性設定為 `PageList`，然後從其智慧標籤檢查 Enable AutoPostBack 選項。

接下來，返回 `DataBound` 事件處理常式，並新增下列程式碼：

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample6.vb)]

此程式碼一開始會清除 `PageList` DropDownList 中的專案。 這似乎是多餘的，因為其中一個不會預期要變更的頁數，但其他使用者可能同時使用系統，新增或移除 `Products` 資料表中的記錄。 這類插入或刪除可能會改變數據頁的數目。

接下來，我們需要再次建立頁碼，並將其對應至目前 GridView `PageIndex` 預設為選取。 我們使用0到 `PageCount - 1`的迴圈來完成這項操作，在每個反復專案中加入新的 `ListItem`，並在目前的反復專案索引等於 GridView 的 `PageIndex` 屬性時，將其 `Selected` 屬性設定為 true。

最後，我們需要建立 DropDownList s `SelectedIndexChanged` 事件的事件處理常式，這會在使用者每次從清單中挑選不同的專案時引發。 若要建立這個事件處理常式，只要在設計工具中按兩下 DropDownList，然後加入下列程式碼：

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample7.vb)]

如 [圖 11] 所示，只是變更 GridView 的 `PageIndex` 屬性會導致將資料重新系結至 GridView。 在 GridView 的 `DataBound` 事件處理常式中，會選取適當的 DropDownList `ListItem`。

[![在選取 [第6頁] 下拉式清單專案時，使用者會自動移至第六頁](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)

**圖 11**：選取 [第6頁] 下拉式清單專案時，使用者會自動移至第六頁（[按一下以查看完整大小的影像](paging-and-sorting-report-data-vb/_static/image23.png)）

## <a name="step-5-adding-bi-directional-sorting-support"></a>步驟5：加入雙向排序支援

加入雙向排序支援就像加入分頁支援一樣簡單，只要從 GridView 的智慧標籤檢查 [啟用排序] 選項（這會將 GridView 的[`AllowSorting` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx)設定為 `true`）。 這會將 GridView 欄位的每一個標頭轉譯為 LinkButtons，當按下時，會導致回傳，並以遞增的順序傳回按下的資料行排序的資料。 再次按一下相同的標頭 LinkButton，會以遞減的順序重新排序資料。

> [!NOTE]
> 如果您使用的是自訂資料存取層，而不是具類型資料集，則在 GridView s 智慧標籤中可能不會有 [啟用排序] 選項。 只有系結至原生支援排序之資料來源的 Gridview，才可使用此核取方塊。 具類型的資料集提供現成可用的排序支援，因為 ADO.NET DataTable 提供了 `Sort` 方法，在叫用時，會使用指定的準則來排序 DataTable s Datarow。

如果您的 DAL 不會傳回原生支援排序的物件，您將需要設定 ObjectDataSource 以將排序資訊傳遞給商務邏輯層，這可以排序資料，或讓資料以 DAL 排序。 在未來的教學課程中，我們將探討如何在商務邏輯和資料存取層排序資料。

排序 LinkButtons 會轉譯為 HTML 超連結，其目前的色彩（藍色代表未流覽的連結，紅色代表造訪的連結）與標頭資料列的背景色彩衝突。 而是讓所有標頭資料列連結以白色顯示，不論是否已造訪。 這可以藉由將下列內容新增至 `Styles.css` 類別來完成：

[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample8.css)]

此語法表示在使用 HeaderStyle 類別的專案中顯示這些超連結時，使用白色文字。

在此 CSS 加入之後，透過瀏覽器造訪頁面時，畫面看起來應該像 [圖 12]。 特別是，[圖 12] 顯示在按下 Price 欄位的頁首連結之後的結果。

[![結果已依單價以遞增順序排序](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)

**圖 12**：結果已依單價以遞增順序排序（[按一下以觀看完整大小的影像](paging-and-sorting-report-data-vb/_static/image26.png)）

## <a name="examining-the-sorting-workflow"></a>檢查排序工作流程

BoundField、CheckBoxField、TemplateField 等所有 GridView 欄位都有一個 `SortExpression` 屬性，它會指出當按下該欄位的排序標頭連結時，應該用來排序資料的運算式。 GridView 也具有 `SortExpression` 屬性。 按一下排序標頭 LinkButton 時，GridView 會將該欄位的 `SortExpression` 值指派給它的 `SortExpression` 屬性。 接下來，會從 ObjectDataSource 重新抓取資料，並根據 GridView 的 `SortExpression` 屬性進行排序。 下列清單詳細說明當使用者在 GridView 中排序資料時，所過大幅簡化的步驟順序：

1. GridView s[排序事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx)引發
2. GridView 的[`SortExpression` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)會設定為按一下排序標頭 LinkButton 之欄位的 `SortExpression`
3. ObjectDataSource 會重新抓取 BLL 中的所有資料，然後使用 GridView s 來排序資料 `SortExpression`
4. GridView 的 `PageIndex` 屬性會重設為0，這表示當排序使用者時，會傳回資料的第一頁（假設已執行分頁支援）
5. GridView s [`Sorted` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx)引發

如同預設分頁，預設的排序選項會重新抓取 BLL 中的*所有*記錄。 當不使用分頁或使用預設分頁來排序時，若沒有任何方法可以規避此效能的影響（快取資料庫資料，則不會叫用）。 不過，如我們在未來的教學課程中所見，在使用自訂分頁時，可以有效率地排序資料。

透過 GridView 的智慧標籤中的下拉式清單，將 ObjectDataSource 系結至 GridView 時，每個 GridView 欄位都會自動將其 `SortExpression` 屬性指派給 `ProductsRow` 類別中的資料欄位名稱。 例如，`ProductName` BoundField s `SortExpression` 設定為 `ProductName`，如下列宣告式標記所示：

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample9.aspx)]

可以設定欄位，使其無法藉由清除其 `SortExpression` 屬性（將它指派給空字串）來進行排序。 為了說明這一點，假設我們不想讓客戶依價格排序產品。 您可以從宣告式標記或透過 [欄位] 對話方塊（按一下 [GridView] 智慧標籤中的 [編輯資料行] 連結來存取），將 `UnitPrice` BoundField s `SortExpression` 屬性移除。

![結果已依單價以遞增順序排序](paging-and-sorting-report-data-vb/_static/image27.png)

**圖 13**：結果已依單價以遞增順序排序

移除 `UnitPrice` BoundField 的 `SortExpression` 屬性後，標頭就會轉譯為文字而非連結，藉此防止使用者依價格排序資料。

[藉由移除 SortExpression 屬性 ![，使用者將無法再依價格排序產品](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)

**圖 14**：藉由移除 SortExpression 屬性，使用者就無法再依價格排序產品（[按一下以觀看完整大小的影像](paging-and-sorting-report-data-vb/_static/image30.png)）

## <a name="programmatically-sorting-the-gridview"></a>以程式設計方式排序 GridView

您也可以使用 GridView 的[`Sort` 方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)，以程式設計方式排序 GridView 的內容。 只要傳入 `SortExpression` 值來排序，連同[`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) （`Ascending` 或 `Descending`），GridView 的資料就會重新排序。

假設我們關閉了 `UnitPrice` 的排序，因為我們擔心客戶只購買最低價格的產品。 不過，我們想要鼓勵他們購買最昂貴的產品，所以我們可以讓他們能夠依價格排序產品，但只能從最昂貴的價格到最低。

若要完成這項操作，請將按鈕 Web 控制項新增至頁面，將其 `ID` 屬性設為 `SortPriceDescending`，並將其 `Text` 屬性設定為依價格排序。 接下來，在設計工具中按兩下按鈕控制項，以建立按鈕 s `Click` 事件的事件處理常式。 將下列程式碼新增至這個事件處理常式：

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample10.vb)]

按一下此按鈕會將使用者傳回至第一頁，其中包含以價格排序的產品，從最昂貴到最低成本（請參閱 [圖 15]）。

[![按一下按鈕，就會將產品的順序從最昂貴到最低](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)

**圖 15**：按一下按鈕會將產品從最高成本訂購到最少（[按一下以觀看完整大小的影像](paging-and-sorting-report-data-vb/_static/image33.png)）

## <a name="summary"></a>總結

在本教學課程中，我們已瞭解如何執行預設分頁和排序功能，這兩者都與勾選核取方塊一樣簡單！ 當使用者透過資料進行排序或分頁時，類似的工作流程色彩：

1. 回傳接踵而來
2. 資料 Web 控制項 s 的前期層級事件引發（`PageIndexChanging` 或 `Sorting`）
3. ObjectDataSource 會重新取出所有資料
4. 資料 Web 控制項的 post 層級事件引發（`PageIndexChanged` 或 `Sorted`）

雖然實行基本分頁和排序是一種簡單的作業，但必須行使更多工作，才能利用更有效率的自訂分頁或進一步增強分頁或排序介面。 未來的教學課程將探索這些主題。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](creating-a-customized-sorting-user-interface-cs.md)
> [下一頁](efficiently-paging-through-large-amounts-of-data-vb.md)
