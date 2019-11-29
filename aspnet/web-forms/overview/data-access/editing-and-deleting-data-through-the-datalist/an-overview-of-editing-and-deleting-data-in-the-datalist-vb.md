---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
title: 在 DataList 中編輯和刪除資料的總覽（VB） |Microsoft Docs
author: rick-anderson
description: 雖然 DataList 缺少內建的編輯和刪除功能，但在本教學課程中，我們將瞭解如何建立可支援編輯和刪除的 DataList 。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 9410a23c-9697-4f07-bd71-e62b0ceac655
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 49b09cbf0f12f7c7233c3bb2a8b3b2c073bf117e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74573133"
---
# <a name="an-overview-of-editing-and-deleting-data-in-the-datalist-vb"></a>在 DataList 中編輯和刪除資料的總覽（VB）

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_VB.exe)或[下載 PDF](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/datatutorial36vb1.pdf)

> 雖然 DataList 缺少內建的編輯和刪除功能，但在本教學課程中，我們將瞭解如何建立 DataList，以支援編輯和刪除其基礎資料。

## <a name="introduction"></a>簡介

在[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教學課程的總覽中，我們探討了如何使用應用程式架構、ObjectDataSource 和 GridView、DetailsView 和 FormView 控制項來插入、更新和刪除資料。 有了 ObjectDataSource 和這三個數據 Web 控制項，執行簡單的資料修改介面就是一種貼齊，只涉及智慧標籤的核取方塊。 不需要撰寫任何程式碼。

可惜的是，DataList 缺少 GridView 控制項中固有的內建編輯和刪除功能。 這項遺漏功能的原因是，當您無法使用宣告式資料來源控制項和無程式碼的資料修改頁面時，DataList 是來自舊版 ASP.NET 的 new relic。 雖然 ASP.NET 2.0 中的 DataList 並未提供與 GridView 相同的現成資料修改功能，但我們可以使用 ASP.NET 1.x 技術來加入這類功能。 這種方法需要一些程式碼，但如我們在本教學課程中所見，DataList 有一些事件和屬性可協助進行此程式。

在本教學課程中，我們將瞭解如何建立 DataList，以支援編輯和刪除其基礎資料。 未來的教學課程會檢查更先進的編輯和刪除案例，包括輸入欄位驗證、正常處理從資料存取或商務邏輯層引發的例外狀況等等。

> [!NOTE]
> 就像 DataList 一樣，中繼器控制項缺少插入、更新或刪除的現成功能。 雖然可以加入這類功能，但 DataList 卻包含在中繼器中找不到的屬性和事件，可簡化新增這類功能。 因此，本教學課程和未來查看編輯和刪除的教學課程，將會嚴格著重在 DataList 上。

## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>步驟1：建立編輯和刪除教學課程的網頁

開始探索如何從 DataList 更新和刪除資料之前，讓我們先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程中使用，以及接下來的幾頁。 從新增名為 `EditDeleteDataList`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![新增教學課程的 ASP.NET 網頁](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image1.png)

**圖 1**：新增教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`EditDeleteDataList`] 資料夾中的 `Default.aspx` 會列出其章節中的教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將這個使用者控制項加入至 `Default.aspx`，方法是將它從方案總管拖曳至頁面 s 設計檢視。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image2.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image4.png)）

最後，將頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，請在具有 DataList 和中繼器 `<siteMapNode>`的主要/詳細資料包表之後，加入下列標記：

[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含 DataList 編輯和刪除教學課程的專案。

![網站地圖現在包含 DataList 編輯和刪除教學課程的專案](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image5.png)

**圖 3**：網站地圖現在包含 DataList 編輯和刪除教學課程的專案

## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>步驟2：檢查更新和刪除資料的技術

使用 GridView 編輯和刪除資料非常簡單，因為在幕後，GridView 和 ObjectDataSource 會共同工作。 如[檢查與插入、更新和刪除教學課程相關聯的事件](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)中所述，當您按一下 [資料列 s 更新] 按鈕時，GridView 會自動將使用雙向資料系結的欄位指派給其 ObjectDataSource 的 `UpdateParameters` 集合，然後叫用該 objectdatasource 的 `Update()` 方法。

可惜的是，DataList 並不提供任何一種內建功能。 我們負責確保使用者的值會指派給 ObjectDataSource s 參數，而且會呼叫其 `Update()` 方法。 為了協助我們進行這項工作，DataList 提供下列屬性和事件：

- 當更新或刪除時，  **[`DataKeyField` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)** ，我們必須能夠唯一識別 DataList 中的每個專案。 將此屬性設定為所顯示資料的 [主要金鑰] 欄位。 這麼做會將每個 DataList 專案的指定 `DataKeyField` 值填入 DataList s [`DataKeys` 集合](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx)。
- 按一下 `CommandName` 屬性設為 [編輯] 的按鈕、LinkButton 或 ImageButton 時，就會引發 **[`EditCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)** 。
- 按一下 `CommandName` 屬性設為 [取消] 的按鈕、LinkButton 或 ImageButton 時，就會引發 **[`CancelCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)** 。
- 按一下 `CommandName` 屬性設為 Update 的按鈕、LinkButton 或 ImageButton 時，就會引發 **[`UpdateCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)** 。
- 按一下 `CommandName` 屬性設為 [刪除] 的按鈕、LinkButton 或 ImageButton 時，就會引發 **[`DeleteCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)** 。

使用這些屬性和事件，我們可以使用四種方法來更新和刪除 DataList 中的資料：

1. **使用 ASP.NET 1.X 技術**，DataList 在 ASP.NET 2.0 和 ObjectDataSources 之前就已存在，而且能夠透過程式設計的方式來完全更新和刪除資料。 這項技術完全 ditches ObjectDataSource，而且需要將資料直接從商務邏輯層系結至 DataList，這兩者都是在抓取要顯示的資料，以及更新或刪除記錄時。
2. 當 DataList 缺少 GridView 的固有編輯和刪除功能時，在**頁面上使用單一 ObjectDataSource 控制項來進行選取、更新和刪除**，因此無法將它們加入自己。 使用這種方法時，我們會使用 ObjectDataSource，就像在 GridView 範例中一樣，但必須建立 DataList s `UpdateCommand` 事件的事件處理常式，而我們會在其中設定 ObjectDataSource s 參數並呼叫其 `Update()` 方法。
3. 當使用選項2時，**使用 ObjectDataSource 控制項來選取，但是直接針對 BLL 進行更新和刪除**，我們需要在 `UpdateCommand` 事件中撰寫一些程式碼，並指派參數值等等。 相反地，我們可以使用 ObjectDataSource 來選取，但是直接針對 BLL 進行更新和刪除呼叫（如選項1）。 就我的觀點而言，直接與 BLL 互動來更新資料，會導致更容易閱讀的程式碼，而不是指派 ObjectDataSource s `UpdateParameters` 並呼叫其 `Update()` 方法。
4. **透過多個 ObjectDataSources 使用宣告式方法**，先前的三種方法都需要一些程式碼。 如果您不想盡可能繼續使用宣告式語法，最後一個選項就是在頁面上包含多個 ObjectDataSources。 第一個 ObjectDataSource 會從 BLL 抓取資料，並將其系結至 DataList。 針對更新，會加入另一個 ObjectDataSource，但會直接加入至 DataList s `EditItemTemplate`中。 若要包含刪除支援，但 `ItemTemplate`中需要另一個 ObjectDataSource。 使用此方法時，這些內嵌的 ObjectDataSource 會使用 `ControlParameters`，以宣告方式將 ObjectDataSource s 參數系結至使用者輸入控制項（而不需要在 DataList s `UpdateCommand` 事件處理常式中以程式設計方式指定它們）。 這種方法仍然需要一些程式碼，我們必須呼叫 embedded ObjectDataSource s `Update()` 或 `Delete()` 命令，但需要的時間遠低於其他三種方法。 這裡的缺點是，多個 ObjectDataSources 會從整體可讀性中注意力，而使頁面變得雜亂。

如果只強制使用其中一種方法，我可以選擇選項1，因為它提供最大的彈性，而且因為 DataList 原本是設計來配合這個模式。 雖然 DataList 已擴充為可與 ASP.NET 2.0 資料來源控制項搭配使用，但並沒有官方 ASP.NET 2.0 資料 Web 控制項（GridView、DetailsView 和 FormView）的所有擴充點或功能。 不過，選項2到4不會有任何優點。

這和未來的編輯和刪除教學課程將使用 ObjectDataSource 來抓取資料，以顯示並直接呼叫 BLL 以更新和刪除資料（選項3）。

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>步驟3：加入 DataList 並設定其 ObjectDataSource

在本教學課程中，我們將建立一個會列出產品資訊的 DataList，而針對每個產品，會提供使用者編輯名稱和價格，以及完全刪除產品的功能。 特別是，我們將使用 ObjectDataSource 抓取要顯示的記錄，但請直接與 BLL 互動來執行更新和刪除動作。 在我們擔心如何對 DataList 執行編輯和刪除功能之前，先讓先取得頁面來顯示唯讀介面中的產品。 因為我們已在先前的教學課程中檢查過這些步驟，所以我會快速地繼續進行。

一開始先開啟 `EditDeleteDataList` 資料夾中的 `Basics.aspx` 頁面，然後從 設計檢視將 DataList 加入至頁面。 接下來，從 DataList s 智慧標籤建立新的 ObjectDataSource。 由於我們使用的是產品資料，因此請將它設定為使用 `ProductsBLL` 類別。 若要取出*所有*產品，請選擇 [選取] 索引標籤中的 [`GetProducts()`] 方法。

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image6.png)

**圖 4**：設定 ObjectDataSource 使用 `ProductsBLL` 類別（[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image8.png)）

[![使用 GetProducts （）方法傳回產品資訊](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image9.png)

**圖 5**：使用 `GetProducts()` 方法傳回產品資訊（[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image11.png)）

DataList （如 GridView）並非設計用來插入新資料;因此，請從 [插入] 索引標籤的下拉式清單中選取 [（無）] 選項。也請為 [更新] 和 [刪除] 索引標籤選擇 [（無）]，因為更新和刪除將會透過 BLL 以程式設計方式執行。

[![確認 [ObjectDataSource] [插入]、[更新] 和 [刪除] 索引標籤中的下拉式清單已設定為 [（無）]](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image12.png)

**圖 6**：確認 [ObjectDataSource] [插入]、[更新] 和 [刪除] 索引標籤中的下拉式清單已設定為 [（無）] （[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image14.png)）

設定 ObjectDataSource 之後，請按一下 [完成]，返回設計工具。 如先前範例中所見，完成 ObjectDataSource 設定時，Visual Studio 會自動建立 DropDownList 的 `ItemTemplate`，並顯示每個資料欄位。 以只顯示產品名稱和價格的 `ItemTemplate` 取代此項。 此外，請將 `RepeatColumns` 屬性設定為2。

> [!NOTE]
> 如*插入、更新和刪除資料*教學課程中所述，使用 objectdatasource 來修改資料時，我們的架構需要從 ObjectDataSource s 宣告式標記中移除 `OldValuesParameterFormatString` 屬性（或將它重設為預設值，`{0}`）。 不過，在本教學課程中，我們只會使用 ObjectDataSource 來抓取資料。 因此，我們不需要修改 ObjectDataSource s `OldValuesParameterFormatString` 屬性值（雖然不會有任何傷害）。

以自訂的 `ItemTemplate` 取代預設的 DataList 之後，您頁面上的宣告式標記看起來應該如下所示：

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample2.aspx)]

請花點時間透過瀏覽器來查看進度。 如 [圖 7] 所示，DataList 會顯示兩個數據行中每個產品的產品名稱和單價。

[![產品名稱和價格會顯示在兩個數據行的 DataList 中](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image15.png)

**圖 7**：產品名稱和價格會顯示在兩個數據行的 DataList 中（[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image17.png)）

> [!NOTE]
> DataList 具有更新和刪除程式所需的一些屬性，而且這些值會以檢視狀態儲存。 因此，在建立支援編輯或刪除資料的 DataList 時，必須啟用 DataList s view 狀態。  
>   
> 精明的讀者可能會記得，在建立可編輯的 Gridview、DetailsViews 和 FormViews 時，可以停用 view 狀態。 這是因為 ASP.NET 2.0 Web 控制項可以包含*控制項狀態*，也就是在檢視狀態之類的回傳之間保存的狀態，但被視為必要。

停用 GridView 中的 view 狀態只會省略簡單的狀態資訊，但會維持控制項狀態（包括編輯和刪除所需的狀態）。 在 ASP.NET 1.x 時間範圍內建立的 DataList 不會利用控制項狀態，因此必須啟用檢視狀態。 如需控制狀態的用途以及它與檢視狀態有何差異的詳細資訊，請參閱[控制狀態與檢視狀態](https://msdn.microsoft.com/library/1whwt1k7.aspx)。

## <a name="step-4-adding-an-editing-user-interface"></a>步驟4：新增編輯使用者介面

GridView 控制項是由欄位集合（BoundFields、CheckBoxFields、TemplateFields 等等）所組成。 這些欄位可以根據其模式調整其呈現的標記。 例如，在唯讀模式中，BoundField 會將其資料欄值顯示為文字;處於編輯模式時，它會呈現 TextBox Web 控制項，其 `Text` 屬性指派給資料欄位值。

另一方面，DataList 會使用範本來呈現其專案。 唯讀專案會使用 `ItemTemplate` 來轉譯，而編輯模式中的專案則會透過 `EditItemTemplate`呈現。 到目前為止，我們的 DataList 只有一個 `ItemTemplate`。 為了支援專案層級的編輯功能，我們需要加入包含要針對可編輯專案顯示之標記的 `EditItemTemplate`。 在本教學課程中，我們將使用 TextBox Web 控制項來編輯產品的名稱和單價。

`EditItemTemplate` 可以宣告方式或透過設計工具建立（從 DataList s 智慧標籤選取 [編輯範本] 選項）。 若要使用 [編輯範本] 選項，請先按一下智慧標籤中的 [編輯範本] 連結，然後從下拉式清單中選取 [`EditItemTemplate`] 專案。

[![選擇使用 DataList s EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image18.png)

**圖 8**：選擇使用 DataList s `EditItemTemplate` （[按一下以觀看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image20.png)）

接下來，輸入產品名稱：和價格：，然後將兩個 TextBox 控制項從 [工具箱] 拖曳至設計工具上的 `EditItemTemplate` 介面。 將 文字方塊 `ID` 屬性設定為 `ProductName` 和 `UnitPrice`。

[![為產品的名稱和價格新增文字方塊](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image21.png)

**圖 9**：為產品的名稱和價格新增文字方塊（[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image23.png)）

我們需要將對應的產品資料欄值系結到兩個文字方塊的 `Text` 屬性。 從 [文字方塊] 智慧標籤，按一下 [編輯資料系結] 連結，然後將適當的資料欄位與 [`Text`] 屬性建立關聯，如 [圖 10] 所示。

> [!NOTE]
> 將 `UnitPrice` 資料欄位系結至 [價格] 文字方塊 `Text` 欄位時，您可以將其格式化為貨幣值（`{0:C}`）、一般數位（`{0:N}`），或保持未格式化。

![將 [ProductName] 和 [單價] 資料欄位系結至文字方塊的 [文字] 屬性](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image24.png)

**圖 10**：將 [`ProductName`] 和 [`UnitPrice` 資料] 欄位系結至文字方塊的 `Text` 屬性

請注意 [圖 10] 中的 [編輯資料系結] 對話方塊，如何*不*包含在 GridView 或 DetailsView 中編輯 TemplateField 時出現的雙向資料系結核取方塊，或是 FormView 中的範本。 雙向資料系結功能允許在輸入 Web 控制項中輸入的值，在插入或更新資料時，自動指派給對應的 ObjectDataSource s `InsertParameters` 或 `UpdateParameters`。 DataList 不支援雙向資料系結，因為我們稍後會在本教學課程中看到，在使用者進行變更並準備好更新資料之後，我們需要以程式設計方式存取這些文字方塊 `Text` 屬性，並將其值傳入 `ProductsBLL` 類別中的適當 `UpdateProduct` 方法。

最後，我們需要將 [更新] 和 [取消] 按鈕新增至 `EditItemTemplate`。 如我們在[主要/詳細資料中使用具有詳細資料 DataList 教學課程的主要記錄項目符號清單](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)中所見，當按鈕、LinkButton 或 ImageButton 的 `CommandName` 屬性設定是從中繼器或 datalist 內按一下時，就會引發 Repeater 或 datalist 的 `ItemCommand` 事件。 對於 DataList 而言，如果 `CommandName` 屬性設定為某個值，也可能會引發額外的事件。 特殊的 `CommandName` 屬性值包括，還有其他內容：

- [取消] 會引發 `CancelCommand` 事件
- 編輯引發 `EditCommand` 事件
- Update 會引發 `UpdateCommand` 事件

請記住，除了 `ItemCommand` 事件*之外*，也會引發這些事件。

將加入至 [`EditItemTemplate`] 兩個按鈕 Web 控制項，其中 `CommandName` 設定為 [更新]，另一個設定為 [取消]。 新增這兩個按鈕 Web 控制項之後，設計工具看起來應該如下所示：

[![將 [更新] 和 [取消] 按鈕新增至 EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image25.png)

**圖 11**：將 [更新] 和 [取消] 按鈕新增至 `EditItemTemplate` （[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image27.png)）

使用 `EditItemTemplate` 完成 DataList 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>步驟5：新增管線進入編輯模式

此時，我們的 DataList 具有透過其 `EditItemTemplate`定義的編輯介面;不過，目前沒有任何方法可以讓使用者造訪我們的頁面，指出他想要編輯產品的資訊。 我們需要將 [編輯] 按鈕加入至每個產品，按下時，會在編輯模式中轉譯該 DataList 專案。 首先，透過設計工具或以宣告的方式，將 [編輯] 按鈕加入至 `ItemTemplate`。 請務必將 [編輯] 按鈕 `CommandName` 屬性設定為 [編輯]。

新增此 [編輯] 按鈕之後，請花一點時間透過瀏覽器來觀看頁面。 透過這項新增，每個產品清單都應該包含 [編輯] 按鈕。

[![將 [更新] 和 [取消] 按鈕新增至 EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image28.png)

**圖 12**：將 [更新] 和 [取消] 按鈕新增至 `EditItemTemplate` （[按一下以觀看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image30.png)）

按一下按鈕會導致回傳，但不會將產品*清單帶入編輯*模式。 若要讓產品可供編輯，我們必須：

1. 將 DataList s [`EditItemIndex` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)設定為剛才按一下編輯按鈕之 `DataListItem` 的索引。
2. 將資料重新系結至 DataList。 當 DataList 重新轉譯時，其 `ItemIndex` 對應至 DataList s `EditItemIndex` 的 `DataListItem` 會使用其 `EditItemTemplate`來呈現。

由於按一下 [編輯] 按鈕時，會引發 DataList s `EditCommand` 事件，請使用下列程式碼建立 `EditCommand` 事件處理常式：

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample4.vb)]

`EditCommand` 事件處理常式會傳遞 `DataListCommandEventArgs` 類型的物件做為第二個輸入參數，其中包含按一下編輯按鈕之 `DataListItem` 的參考（`e.Item`）。 事件處理常式會先將 DataList s `EditItemIndex` 設定為可編輯 `DataListItem` 的 `ItemIndex`，然後藉由呼叫 DataList s `DataBind()` 方法，將資料重新系結至 DataList。

新增這個事件處理常式之後，請在瀏覽器中重新流覽頁面。 按一下 [編輯] 按鈕現在會讓按一下的產品可供編輯（請參閱 [圖 13]）。

[![按一下 [編輯] 按鈕可讓產品編輯](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image31.png)

**圖 13**：按一下 [編輯] 按鈕可讓產品編輯（[按一下以觀看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image33.png)）

## <a name="step-6-saving-the-user-s-changes"></a>步驟6：儲存使用者的變更

按一下 [已編輯的產品] 更新或 [取消] 按鈕，此時不會執行任何操作;若要加入這種功能，我們必須為 DataList s `UpdateCommand` 和 `CancelCommand` 事件建立事件處理常式。 首先建立 `CancelCommand` 事件處理常式，這會在按一下 [已編輯的產品] [取消] 按鈕時執行，並負責將 DataList 傳回其預先編輯狀態。

若要讓 DataList 以唯讀模式呈現其所有專案，我們必須：

1. 將 DataList s [`EditItemIndex` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)設定為不存在之 `DataListItem` 索引的索引。 `-1` 是一種安全的選擇，因為 `DataListItem` 索引會從 `0`開始。
2. 將資料重新系結至 DataList。 因為沒有任何 `DataListItem` `ItemIndex` es 對應至 DataList s `EditItemIndex`，所以整個 DataList 會以唯讀模式呈現。

您可以使用下列事件處理常式程式碼來完成這些步驟：

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample5.vb)]

在這種新增的情況下，按一下 [取消] 按鈕會將 DataList 傳回其預先編輯狀態。

我們需要完成的最後一個事件處理常式是 `UpdateCommand` 事件處理常式。 這個事件處理常式必須：

1. 以程式設計方式存取使用者輸入的產品名稱和價格，以及已編輯的產品 `ProductID`。
2. 藉由在 `ProductsBLL` 類別中呼叫適當的 `UpdateProduct` 多載，起始更新程式。
3. 將 DataList s [`EditItemIndex` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)設定為不存在之 `DataListItem` 索引的索引。 `-1` 是一種安全的選擇，因為 `DataListItem` 索引會從 `0`開始。
4. 將資料重新系結至 DataList。 因為沒有任何 `DataListItem` `ItemIndex` es 對應至 DataList s `EditItemIndex`，所以整個 DataList 會以唯讀模式呈現。

步驟1和2負責儲存使用者的變更;步驟3和4會在儲存變更之後，將 DataList 回到其預先編輯狀態，而且與 `CancelCommand` 事件處理常式中執行的步驟完全相同。

若要取得更新的產品名稱和價格，我們必須使用 `FindControl` 方法，以程式設計方式參考 `EditItemTemplate`內的 TextBox Web 控制項。 我們也需要取得已編輯的產品 `ProductID` 值。 當我們一開始將 ObjectDataSource 系結至 DataList 時，Visual Studio 將 DataList s `DataKeyField` 屬性指派給資料來源中的主要索引鍵值（`ProductID`）。 然後，您可以從 DataList s `DataKeys` 集合中抓取此值。 請花點時間確定 `DataKeyField` 屬性確實設定為 `ProductID`。

下列程式碼會實行四個步驟：

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample6.vb)]

事件處理常式會從 `DataKeys` 集合中讀取已編輯的產品 s `ProductID` 開始。 接下來，會參考 `EditItemTemplate` 中的兩個文字方塊，而其 `Text` 屬性會儲存在本機變數中，`productNameValue` 和 `unitPriceValue`。 我們使用 `Decimal.Parse()` 方法來讀取 [`UnitPrice`] 文字方塊中的值，如此一來，如果輸入的值有貨幣符號，仍然可以正確地轉換成 `Decimal` 值。

> [!NOTE]
> [`ProductName`] 和 [`UnitPrice`] 文字方塊中的值只會指派給 productNameValue 和 unitPriceValue 變數（如果文字方塊的文字屬性具有指定的值）。 否則，會將 `Nothing` 的值用於變數，這會影響以資料庫 `NULL` 值來更新資料。 也就是說，我們的程式碼會將空字串轉換為資料庫 `NULL` 值，這是 GridView、DetailsView 和 FormView 控制項中編輯介面的預設行為。

讀取值之後，會呼叫 `ProductsBLL` 類別的 `UpdateProduct` 方法，並傳入產品的名稱、價格和 `ProductID`。 事件處理常式會藉由使用與 `CancelCommand` 事件處理常式中完全相同的邏輯，將 DataList 傳回其預先編輯狀態來完成。

在 `EditCommand`、`CancelCommand`和 `UpdateCommand` 事件處理常式完成後，訪客可以編輯產品的名稱和價格。 [圖 14-16] 顯示此編輯工作流程的作用中。

[![第一次造訪網頁時，所有產品都處於唯讀模式](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image34.png)

**圖 14**：第一次造訪網頁時，所有產品都處於唯讀模式（[按一下以觀看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image36.png)）

[![若要更新產品的名稱或價格，請按一下 [編輯] 按鈕](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image37.png)

**圖 15**：若要更新產品的名稱或價格，請按一下 [編輯] 按鈕（[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image39.png)）

[![變更值之後，請按一下 [更新] 回到唯讀模式](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image40.png)

**圖 16**：變更值之後，請按一下 [更新] 回到唯讀模式（[按一下以查看完整大小的影像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image42.png)）

## <a name="step-7-adding-delete-capabilities"></a>步驟7：新增刪除功能

將刪除功能新增至 DataList 的步驟類似于新增編輯功能。 簡單地說，我們必須在按一下時，將 [刪除] 按鈕新增至 `ItemTemplate`：

1. 透過 `DataKeys` 集合，讀取對應產品的 `ProductID`。
2. 藉由呼叫 `ProductsBLL` 類別 s `DeleteProduct` 方法來執行刪除。
3. 將資料重新系結至 DataList。

首先，將 [刪除] 按鈕新增至 [`ItemTemplate`]。

按一下時，`CommandName` 為 [編輯]、[更新] 或 [取消] 的按鈕會引發 DataList s `ItemCommand` 事件以及額外的事件（例如，使用 [編輯] 時，也會引發 `EditCommand` 事件）。 同樣地，DataList 中其 `CommandName` 屬性設為 Delete 的任何按鈕、LinkButton 或 ImageButton，都會引發 `DeleteCommand` 事件（以及 `ItemCommand`）。

在 `ItemTemplate`中的 [編輯] 按鈕旁新增 [刪除] 按鈕，並將其 `CommandName` 屬性設定為 [刪除]。 新增此按鈕控制項之後，您的 DataList `ItemTemplate` 宣告式語法應該如下所示：

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample7.aspx)]

接下來，使用下列程式碼建立 DataList s `DeleteCommand` 事件的事件處理常式：

[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample8.vb)]

按一下 [刪除] 按鈕會導致回傳，並引發 DataList s `DeleteCommand` 事件。 在事件處理常式中，按下的 product s `ProductID` 值會從 `DataKeys` 集合存取。 接下來，藉由呼叫 `ProductsBLL` 類別 s `DeleteProduct` 方法來刪除產品。

刪除產品之後，請務必將資料重新系結至 DataList （`DataList1.DataBind()`），否則 DataList 會繼續顯示剛刪除的產品。

## <a name="summary"></a>總結

雖然 DataList 缺少點，並按一下 [編輯] 和 [刪除 GridView 滿意的支援]，但有一個簡單的程式碼可加以增強，以包含這些功能。 在本教學課程中，我們已瞭解如何建立可刪除的兩欄式產品清單，並可編輯其名稱和價格。 新增編輯和刪除支援的方式，是將適當的 Web 控制項包含在 `ItemTemplate` 和 `EditItemTemplate`中、建立對應的事件處理常式、讀取使用者輸入的和主要金鑰值，以及與商務邏輯層互動。

雖然我們已在 DataList 中新增基本的編輯和刪除功能，但它缺乏更多的先進功能。 例如，沒有輸入欄位驗證-如果使用者輸入太昂貴的價格，當嘗試將太昂貴的資源轉換成 `Decimal`時，`Decimal.Parse` 會擲回例外狀況。 同樣地，如果在商務邏輯或資料存取層更新資料時發生問題，使用者將會看到標準錯誤畫面。 若未在 [刪除] 按鈕上進行任何確認，則不小心刪除產品會很有可能。

在未來的教學課程中，我們將瞭解如何改善編輯使用者體驗。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Zack，Pespisa 和 Randy Schmidt。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](customizing-the-datalist-s-editing-interface-cs.md)
> [下一頁](performing-batch-updates-vb.md)
