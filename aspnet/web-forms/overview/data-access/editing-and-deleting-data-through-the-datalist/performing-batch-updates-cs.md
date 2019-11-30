---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
title: 執行批次更新C#（） |Microsoft Docs
author: rick-anderson
description: 瞭解如何建立可完全編輯的 DataList，其中所有的專案都處於編輯模式，而其值可透過按一下 [...] 上的 [全部更新] 按鈕來儲存
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 57743ca7-5695-4e07-aed1-44b297f245a9
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
msc.type: authoredcontent
ms.openlocfilehash: cde12a4d24555216adc49dd02818901278932eaa
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74631512"
---
# <a name="performing-batch-updates-c"></a>執行批次更新 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_CS.exe)或[下載 PDF](performing-batch-updates-cs/_static/datatutorial37cs1.pdf)

> 瞭解如何建立可完全編輯的 DataList，其中所有的專案都處於編輯模式，而且可以按一下頁面上的 [全部更新] 按鈕來儲存其值。

## <a name="introduction"></a>簡介

在[先前的教學](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)課程中，我們已探討如何建立專案層級 DataList。 如同標準可編輯的 GridView，DataList 中的每個專案都包含 [編輯] 按鈕，當您按一下時，就會讓專案可供編輯。 雖然此專案層級的編輯功能適用于只偶爾更新的資料，但某些使用案例需要使用者編輯許多記錄。 如果使用者需要編輯數十筆記錄，並強制按一下 [編輯]、進行變更，然後按一下每一個的 [更新]，則按一下的量可能會妨礙她的生產力。 在這種情況下，較好的選項是提供可完全編輯的 DataList，*其中一個*專案是在編輯模式中，而且可以按一下頁面上的 [全部更新] 按鈕來編輯其值（請參閱 [圖 1]）。

[可以修改可完全編輯之 DataList 中的每個專案 ![](performing-batch-updates-cs/_static/image2.png)](performing-batch-updates-cs/_static/image1.png)

**圖 1**：可以修改完全可編輯的 DataList 中的每個專案（[按一下以查看完整大小的影像](performing-batch-updates-cs/_static/image3.png)）

在本教學課程中，我們將探討如何讓使用者使用完全可編輯的 DataList 來更新供應商位址資訊。

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>步驟1：在 DataList s ItemTemplate 中建立可編輯的使用者介面

在先前的教學課程中，我們會在這裡建立標準的專案層級可編輯 DataList，我們使用了兩個範本：

- `ItemTemplate` 包含唯讀使用者介面（標籤 Web 控制項，用於顯示每個產品的名稱和價格）。
- `EditItemTemplate` 包含編輯模式使用者介面（這兩個 TextBox Web 控制項）。

DataList s `EditItemIndex` 屬性會指定使用 `EditItemTemplate`轉譯 `DataListItem` （如果有的話）。 特別是，其 `ItemIndex` 值符合 DataList s `EditItemIndex` 屬性的 `DataListItem` 會使用 `EditItemTemplate`來呈現。 當您一次只能編輯一個專案，但在建立可完全編輯的 DataList 時，此模型的運作良好。

針對可完全編輯的 DataList，我們想要使用可編輯的介面來轉譯*所有*的 `DataListItem`。 完成這項操作的最簡單方式是在 `ItemTemplate`中定義可編輯的介面。 若要修改供應商位址資訊，可編輯的介面會將供應商名稱包含為文字，然後將 [位址]、[城市] 和 [國家/地區] 值設為文字方塊。

一開始先開啟 [`BatchUpdate.aspx`] 頁面，加入 DataList 控制項，然後將其 [`ID`] 屬性設定為 [`Suppliers`]。 從 DataList s 智慧標籤中，加入宣告名為 `SuppliersDataSource`的新 ObjectDataSource 控制項。

[![建立名為 SuppliersDataSource 的新 ObjectDataSource](performing-batch-updates-cs/_static/image5.png)](performing-batch-updates-cs/_static/image4.png)

**圖 2**：建立名為 `SuppliersDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](performing-batch-updates-cs/_static/image6.png)）

使用 `SuppliersBLL` 類別的 `GetSuppliers()` 方法，將 ObjectDataSource 設定為取出資料（請參閱 [圖 3]）。 如同先前的教學課程，我們將直接使用商務邏輯層，而不是透過 ObjectDataSource 更新供應商資訊。 因此，請在 [更新] 索引標籤中，將下拉式清單設定為 [（無）] （請參閱 [圖 4]）。

[![使用 GetSuppliers （）方法來取得供應商資訊](performing-batch-updates-cs/_static/image8.png)](performing-batch-updates-cs/_static/image7.png)

**圖 3**：使用 `GetSuppliers()` 方法取出供應商資訊（[按一下以觀看完整大小的影像](performing-batch-updates-cs/_static/image9.png)）

[![在 [更新] 索引標籤中將下拉式清單設定為 [（無）]](performing-batch-updates-cs/_static/image11.png)](performing-batch-updates-cs/_static/image10.png)

**圖 4**：在 [更新] 索引標籤中，將下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](performing-batch-updates-cs/_static/image12.png)）

完成 wizard 之後，Visual Studio 會自動產生 DataList s `ItemTemplate`，以便在標籤 Web 控制項中顯示資料來源所傳回的每個資料欄位。 我們需要修改此範本，使其改為提供編輯介面。 您可以使用 DataList s 智慧標籤中的 [編輯範本] 選項，或直接透過宣告式語法，透過設計工具自訂 `ItemTemplate`。

花點時間建立以文字顯示供應商名稱的編輯介面，但包含供應商位址、城市和國家/地區值的文字方塊。 進行這些變更之後，您的頁面宣告式語法看起來應該如下所示：

[!code-aspx[Main](performing-batch-updates-cs/samples/sample1.aspx)]

> [!NOTE]
> 如同先前的教學課程，本教學課程中的 DataList 必須啟用其檢視狀態。

在 `ItemTemplate` I m 使用兩個新的 CSS 類別，`SupplierPropertyLabel` 和 `SupplierPropertyValue`，其已加入至 `Styles.css` 類別，並已設定為使用與 `ProductPropertyLabel` 和 `ProductPropertyValue` CSS 類別相同的樣式設定。

[!code-css[Main](performing-batch-updates-cs/samples/sample2.css)]

進行這些變更之後，請透過瀏覽器造訪此頁面。 如 [圖 5] 所示，每個 DataList 專案都會將供應商名稱顯示為文字，並使用文字方塊來顯示位址、城市和國家/地區。

[DataList 中的每個供應商 ![可編輯](performing-batch-updates-cs/_static/image14.png)](performing-batch-updates-cs/_static/image13.png)

**圖 5**： DataList 中的每個供應商都是可編輯的（[按一下以查看完整大小的影像](performing-batch-updates-cs/_static/image15.png)）

## <a name="step-2-adding-an-update-all-button"></a>步驟2：新增全部更新按鈕

雖然 [圖 5] 中的每個供應商都在文字方塊中顯示其位址、城市和國家（地區）欄位，但目前沒有可用的 [更新] 按鈕。 並不是每個專案都有 [更新] 按鈕，而且具有完全可編輯的 DataLists，頁面上通常會有一個 [全部更新] 按鈕，當您按一下時，就會更新 DataList 中的*所有*記錄。 在本教學課程中，讓我們新增兩個 [全部更新] 按鈕-一個在頁面頂端，另一個位於底部（雖然按一下任一按鈕會有相同的效果）。

首先，在 DataList 上方加入按鈕 Web 控制項，並將其 `ID` 屬性設為 `UpdateAll1`。 接下來，在 DataList 底下新增第二個按鈕 Web 控制項，將其 `ID` 設定為 `UpdateAll2`。 將兩個按鈕的 `Text` 屬性設定為 [全部更新]。 最後，`Click` 事件的兩個按鈕建立事件處理常式。 我們不會在每個事件處理常式中複製更新邏輯，而是將該邏輯重構到第三個方法，`UpdateAllSupplierAddresses`，讓事件處理常式只叫用第三個方法。

[!code-csharp[Main](performing-batch-updates-cs/samples/sample3.cs)]

[圖 6] 顯示新增 [更新所有] 按鈕之後的頁面。

[已將 [![兩個更新] 按鈕新增至頁面](performing-batch-updates-cs/_static/image17.png)](performing-batch-updates-cs/_static/image16.png)

**圖 6**：已將兩個 Update 按鈕新增至頁面（[按一下以觀看完整大小的影像](performing-batch-updates-cs/_static/image18.png)）

## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>步驟3：更新所有供應商位址資訊

所有 DataList 的專案都顯示編輯介面，並新增 [全部更新] 按鈕之後，剩下的工作就是撰寫程式碼來執行批次更新。 具體而言，我們需要對 DataList 的專案執行迴圈，並為每個專案呼叫 `SuppliersBLL` 類別 s `UpdateSupplierAddress` 方法。

組成 DataList 的 `DataListItem` 實例集合，可以透過 DataList s [`Items` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)來存取。 透過 `DataListItem`的參考，我們可以從 `DataKeys` 集合抓取對應的 `SupplierID`，並以程式設計方式參考 `ItemTemplate` 中的 TextBox Web 控制項，如下列程式碼所示：

[!code-csharp[Main](performing-batch-updates-cs/samples/sample4.cs)]

當使用者按一下其中一個 [全部更新] 按鈕時，`UpdateAllSupplierAddresses` 方法會逐一查看 `Suppliers` DataList 中的每個 `DataListItem`，並呼叫 `SuppliersBLL` 類別的 `UpdateSupplierAddress` 方法，並傳入對應的值。 [位址]、[城市] 或 [國家/地區] 階段的非輸入值是 `UpdateSupplierAddress` 的 `Nothing` 值（而不是空白字串），這會導致資料庫 `NULL` 用於基礎記錄 s 欄位。

> [!NOTE]
> 做為增強功能，您可能會想要在執行批次更新之後，將狀態標籤 Web 控制項新增至提供一些確認訊息的頁面。

## <a name="updating-only-those-addresses-that-have-been-modified"></a>僅更新已修改的位址

本教學課程所使用的批次更新演算法會針對 DataList 中的*每個*供應商呼叫 `UpdateSupplierAddress` 方法，而不論其位址資訊是否已變更。 雖然這類盲人更新通常不會造成效能問題，但如果您重新審核資料庫資料表的變更，它們可能會導致多餘的記錄。 例如，如果您使用觸發程式將 `Suppliers` 資料表的所有 `UPDATE` 記錄到審核表中，則每次使用者按一下 [全部更新] 按鈕時，系統就會為系統中的每個供應商建立新的 audit 記錄，而不論使用者是否進行任何變更。

ADO.NET DataTable 和 DataAdapter 類別是設計用來支援批次更新，其中只有已修改、已刪除和新的記錄會導致任何資料庫通訊。 DataTable 中的每個資料列都有一個[`RowState` 屬性](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)，可指出資料列是否已加入至 DataTable、已從它刪除、修改或保持不變。 一開始填入 DataTable 時，所有資料列都會標示為不變。 變更任何資料列資料行的值，會將資料列標示為已修改。

在 `SuppliersBLL` 類別中，我們會先將單一供應商記錄讀入 `SuppliersDataTable`，然後使用下列程式碼來設定 `Address`、`City`和 `Country` 資料行值，以更新指定的供應商位址資訊：

[!code-csharp[Main](performing-batch-updates-cs/samples/sample5.cs)]

這段程式碼輕鬆自在管理會將傳入的位址、城市和國家值指派給 `SuppliersDataTable` 中的 `SuppliersRow`，而不論值是否已變更。 這些修改會導致 `SuppliersRow` s `RowState` 屬性標示為已修改。 呼叫資料存取層 `Update` 方法時，它會看到 `SupplierRow` 已經過修改，因此會將 `UPDATE` 的命令傳送至資料庫。

不過，假設我們已將程式碼新增至這個方法，只會指派傳入的位址、城市和國家/地區值（如果它們與 `SuppliersRow` 的現有值不同）。 在位址、城市和國家/地區與現有資料相同的情況下，將不會進行任何變更，而且 `SupplierRow` s `RowState` 會保持不變。 最後的結果是，當呼叫 DAL s `Update` 方法時，不會進行任何資料庫呼叫，因為 `SuppliersRow` 尚未修改。

若要制定這項變更，請以下列程式碼取代會盲目指派傳入位址、城市和國家/地區值的語句：

[!code-csharp[Main](performing-batch-updates-cs/samples/sample6.cs)]

使用這段新增的程式碼，DAL 的 `Update` 方法只會針對位址相關值已變更的記錄，將 `UPDATE` 語句傳送到資料庫。

或者，我們可以追蹤傳入的位址欄位和資料庫資料之間是否有任何差異，如果沒有，則只會略過對 DAL s `Update` 方法的呼叫。 如果您重新使用 DB 直接方法，這種方法就很好用，因為 DB 直接方法不會傳遞 `SuppliersRow` 實例，其 `RowState` 可以檢查以判斷是否真的需要資料庫呼叫。

> [!NOTE]
> 每次叫用 `UpdateSupplierAddress` 方法時，就會對資料庫進行呼叫，以取得有關已更新記錄的資訊。 然後，如果資料有任何變更，就會對資料庫進行另一個呼叫，以更新資料表資料列。 藉由建立可接受 `EmployeesDataTable` 實例（其中包含 `BatchUpdate.aspx` 頁面的*所有*變更）的 `UpdateSupplierAddress` 方法多載，即可優化此工作流程。 然後，它可以對資料庫進行一次呼叫，以取得 `Suppliers` 資料表中的所有記錄。 然後可以列舉這兩個結果集，而且只會更新已發生變更的記錄。

## <a name="summary"></a>總結

在本教學課程中，我們已瞭解如何建立可完全編輯的 DataList，讓使用者可以快速地修改多個供應商的位址資訊。 我們從在 DataList s `ItemTemplate`中，為供應商的位址、城市和國家/地區值定義編輯介面的 TextBox Web 控制項開始。 接下來，我們已將 [更新所有] 按鈕新增至 DataList 的上方和下方。 使用者進行變更並按一下其中一個 [全部更新] 按鈕之後，就會列舉 `DataListItem`，並對 `SuppliersBLL` class s `UpdateSupplierAddress` 方法進行呼叫。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Zack，和 Ken Pespisa。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)
> [下一頁](handling-bll-and-dal-level-exceptions-cs.md)
