---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
title: 檢查與插入、更新和刪除（C#）相關聯的事件 |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將使用 ASP.NET 資料 Web 控制項的插入、更新或刪除作業之前、期間和之後所發生的事件進行檢查。 W 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: dab291a0-a8b5-46fa-9dd8-3d35b249201f
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: a8c1388b73524a8bb918b67aa265db894c07636f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78609148"
---
# <a name="examining-the-events-associated-with-inserting-updating-and-deleting-c"></a>檢查與插入、更新和刪除建立關聯的事件 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_CS.exe)或[下載 PDF](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/datatutorial17cs1.pdf)

> 在本教學課程中，我們將使用 ASP.NET 資料 Web 控制項的插入、更新或刪除作業之前、期間和之後所發生的事件進行檢查。 我們也會瞭解如何自訂編輯介面，只更新產品欄位的子集。

## <a name="introduction"></a>簡介

使用 GridView、DetailsView 或 FormView 控制項的內建插入、編輯或刪除功能時，當使用者完成加入新記錄或更新或刪除現有記錄的程式時，會發生各種不同的步驟。 如同我們在上一個[教學](an-overview-of-inserting-updating-and-deleting-data-cs.md)課程中所討論，在 GridView 中編輯資料列時，[編輯] 按鈕會取代為 [更新] 和 [取消] 按鈕，而 [BoundFields] 則會變成 [文字方塊]。 在使用者更新資料並按一下 [更新] 之後，會在回傳時執行下列步驟：

1. GridView 會以編輯記錄的唯一識別欄位（透過 `DataKeyNames` 屬性）填入其 ObjectDataSource 的 `UpdateParameters`，以及使用者輸入的值。
2. GridView 會叫用其 ObjectDataSource 的 `Update()` 方法，而後者會在上一個教學課程中叫用基礎物件（`ProductsDAL.UpdateProduct`中的適當方法）
3. 基礎資料（現在包含已更新的變更）會重新系結至 GridView

在這一系列的步驟期間，會引發一些事件，讓我們建立事件處理常式，以便在需要時新增自訂邏輯。 例如，在步驟1之前，GridView 的 `RowUpdating` 事件會引發。 此時，如果發生驗證錯誤，我們可以取消更新要求。 叫用 `Update()` 方法時，ObjectDataSource 的 `Updating` 事件會引發，讓您有機會新增或自訂任何 `UpdateParameters`的值。 在 ObjectDataSource 的基礎物件的方法完成執行之後，會引發 ObjectDataSource 的 `Updated` 事件。 `Updated` 事件的事件處理常式可以檢查有關更新作業的詳細資訊，例如有多少資料列受到影響，以及是否發生例外狀況。 最後，在步驟2之後，GridView 的 `RowUpdated` 事件會引發;這個事件的事件處理常式可以檢查剛剛執行之更新作業的其他相關資訊。

[圖 1] 說明更新 GridView 時的這一系列事件和步驟。 [圖 1] 中的事件模式不是以 GridView 更新的獨特功能。 從 GridView、DetailsView 或 FormView 中插入、更新或刪除資料時，會 precipitates 資料 Web 控制項和 ObjectDataSource 的相同前置和後置事件順序。

[![在 GridView 中更新資料時引發一系列的前置和後置事件](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image1.png)

**圖 1**：更新 GridView 中的資料時，一系列的前置和後置事件會引發（[按一下以觀看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image3.png)）

在本教學課程中，我們將探討如何使用這些事件來擴充 ASP.NET 資料 Web 控制項的內建插入、更新和刪除功能。 我們也會瞭解如何自訂編輯介面，只更新產品欄位的子集。

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>步驟1：更新產品的`ProductName`和`UnitPrice`欄位

在上一個教學課程的編輯介面中，必須包含*所有*非唯讀的產品欄位。 如果我們要移除 GridView 中的欄位（例如 `QuantityPerUnit`-更新資料時，資料 Web 控制項不會將 ObjectDataSource 的 `QuantityPerUnit` `UpdateParameters` 值。 然後，ObjectDataSource 會將 `null` 值傳入 `UpdateProduct` 商務邏輯層（BLL）方法，這會將編輯過的資料庫記錄的 `QuantityPerUnit` 資料行變更為 `NULL` 值。 同樣地，如果必要欄位（例如 `ProductName`）從編輯介面中移除，則更新會失敗並出現「資料*行 ' ProductName ' 不允許 null*」例外狀況。 此行為的原因是因為 ObjectDataSource 已設定為呼叫 `ProductsBLL` 類別的 `UpdateProduct` 方法，這應該是每個產品欄位的輸入參數。 因此，ObjectDataSource 的 `UpdateParameters` 集合會包含每個方法的輸入參數的參數。

如果我們想要提供可讓使用者只更新欄位子集的資料 Web 控制項，則需要以程式設計方式在 ObjectDataSource 的 `Updating` 事件處理常式中設定遺漏的 `UpdateParameters` 值，或建立並呼叫只預期欄位子集的 BLL 方法。 讓我們來探索這一種方法。

具體而言，我們將建立只顯示 [`ProductName`] 的頁面，並在可編輯的 GridView 中 `UnitPrice` 欄位。 這個 GridView 的編輯介面只會允許使用者更新兩個顯示的欄位，`ProductName` 和 `UnitPrice`。 因為此編輯介面只提供產品欄位的子集，所以我們需要建立一個使用現有 BLL 之 `UpdateProduct` 方法的 ObjectDataSource，並在其 `Updating` 事件處理常式中以程式設計方式設定遺漏的產品欄位值，或者我們必須建立新的 BLL 方法，只預期 GridView 中定義的欄位子集。 在本教學課程中，我們將使用第二個選項，並建立 `UpdateProduct` 方法的多載，只接受三個輸入參數： `productName`、`unitPrice`和 `productID`：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample1.cs)]

就像原始的 `UpdateProduct` 方法一樣，這個多載會從檢查資料庫中是否有具有指定 `ProductID`的產品開始。 如果不是，則會傳回 `false`，表示更新產品資訊的要求失敗。 否則，它會據以更新現有產品記錄的 `ProductName` 並 `UnitPrice` 欄位，並藉由呼叫 TableAdapter 的 `Update()` 方法（傳入 `ProductsRow` 實例）來認可更新。

隨著我們 `ProductsBLL` 類別的加入，我們已準備好建立簡化的 GridView 介面。 開啟 [`EditInsertDelete`] 資料夾中的 `DataModificationEvents.aspx`，並在頁面中新增 GridView。 建立新的 ObjectDataSource，並將其設定為使用 `ProductsBLL` 類別，並將其 `Select()` 方法對應到 `GetProducts`，以及將其 `Update()` 方法對應至只接受 `UpdateProduct`、`productName`和 `unitPrice`輸入參數的 `productID` 多載。 [圖 2] 顯示將 ObjectDataSource 的 `Update()` 方法對應到 `ProductsBLL` 類別的新 `UpdateProduct` 方法多載時，建立資料來源。

[![將 ObjectDataSource 的 Update （）方法對應到新的 UpdateProduct 多載](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image4.png)

**圖 2**：將 ObjectDataSource 的 `Update()` 方法對應至新的 `UpdateProduct` 多載（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image6.png)）

由於我們的範例一開始只需要編輯資料，而不是插入或刪除記錄，因此請花點時間明確地指出 ObjectDataSource 的 `Insert()` 和 `Delete()` 方法不應對應至任何 `ProductsBLL` 類別的方法，方法是前往 [插入] 和 [刪除] 索引標籤，然後從下拉式清單中選擇 [（無）]。

[![從 [插入] 和 [刪除] 索引標籤的下拉式清單中選擇 [（無）]](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image7.png)

**圖 3**：從 [插入] 和 [刪除] 索引標籤的下拉式清單中選擇 [（無）] （[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image9.png)）

完成此嚮導之後，請核取 GridView 的智慧標籤中的 [啟用編輯] 核取方塊。

完成 [建立資料來源] wizard 並系結至 GridView 之後，Visual Studio 已建立這兩個控制項的宣告式語法。 前往來源視圖來檢查 ObjectDataSource 的宣告式標記，如下所示：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample2.aspx)]

由於 ObjectDataSource 的 `Insert()` 和 `Delete()` 方法沒有對應，因此沒有 `InsertParameters` 或 `DeleteParameters` 區段。 此外，由於 `Update()` 方法會對應到只接受三個輸入參數的 `UpdateProduct` 方法多載，因此 `UpdateParameters` 區段只有三個 `Parameter` 實例。

請注意，ObjectDataSource 的 `OldValuesParameterFormatString` 屬性會設定為 `original_{0}`。 當您使用 [設定資料來源] 時，Visual Studio 會自動設定此屬性。 不過，由於我們的 BLL 方法不會預期傳入原始 `ProductID` 值，因此請從 ObjectDataSource 的宣告式語法中移除此屬性指派。

> [!NOTE]
> 如果您只是從設計檢視中的屬性視窗清除 `OldValuesParameterFormatString` 屬性值，屬性仍然會存在於宣告式語法中，但會設為空字串。 請移除宣告式語法中的屬性，或從屬性視窗將值設定為預設的 `{0}`。

雖然 ObjectDataSource 只有產品名稱、價格和識別碼的 `UpdateParameters`，但 Visual Studio 已在 GridView 中為每個產品的欄位新增 BoundField 或 CheckBoxField。

[![GridView 包含每個產品欄位的 BoundField 或 CheckBoxField](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image10.png)

**圖 4**： GridView 包含每個產品欄位的 BoundField 或 CheckBoxField （[按一下以觀看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image12.png)）

當使用者編輯產品並按一下其 [更新] 按鈕時，GridView 會列舉不是唯讀的欄位。 然後，它會將 ObjectDataSource 的 `UpdateParameters` 集合中對應的參數值設定為使用者輸入的值。 如果沒有對應的參數，GridView 會在集合中加入一個。 因此，如果我們的 GridView 包含所有產品欄位的 BoundFields 和 CheckBoxFields，則 ObjectDataSource 最後會叫用採用所有這些參數的 `UpdateProduct` 多載，雖然 ObjectDataSource 的宣告式標記只會指定三個輸入參數（請參閱 [圖 5]）。 同樣地，如果 GridView 中的非唯讀產品欄位有某種組合未對應至 `UpdateProduct` 多載的輸入參數，則在嘗試更新時，將會引發例外狀況。

[![GridView 會將參數加入至 ObjectDataSource 的 UpdateParameters 集合](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image13.png)

**圖 5**： GridView 會將參數加入至 ObjectDataSource 的 `UpdateParameters` 集合（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image15.png)）

為了確保 ObjectDataSource 會叫用只採用產品名稱、價格和識別碼的 `UpdateProduct` 多載，我們必須限制 GridView 只讓 `ProductName` 和 `UnitPrice`能夠編輯欄位。 這可以藉由移除其他 BoundFields 和 CheckBoxFields 來完成，方法是將其他欄位的 `ReadOnly` 屬性設定為 `true`，或將這兩者的某種組合。 在本教學課程中，我們只會移除 `ProductName` 和 `UnitPrice` BoundFields 以外的所有 GridView 欄位，在此之後，GridView 的宣告式標記會如下所示：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample3.aspx)]

雖然 `UpdateProduct` 多載預期會有三個輸入參數，但是在 GridView 中只有兩個 BoundFields。 這是因為 `productID` 輸入參數是主要索引鍵值，並透過已編輯資料列的 `DataKeyNames` 屬性值傳入。

我們的 GridView 連同 `UpdateProduct` 多載，可讓使用者只編輯產品的名稱和價格，而不會遺失任何其他產品欄位。

[![介面只允許編輯產品的名稱和價格](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image16.png)

**圖 6**：介面只允許編輯產品的名稱和價格（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image18.png)）

> [!NOTE]
> 如前一個教學課程中所討論，GridView s 檢視狀態必須啟用（預設行為），這是非常重要的。 如果您將 GridView 的 `EnableViewState` 屬性設定為 `false`，就會面臨並行使用者不小心刪除或編輯記錄的風險。 如需詳細資訊，請參閱[警告： ASP.NET 2.0 gridview/DetailsView/FormViews 的並行問題，其支援編輯及/或刪除，且已停用檢視狀態](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx)。

## <a name="improving-theunitpriceformatting"></a>改善`UnitPrice`格式

雖然 [圖 6] 所示的 GridView 範例運作正常，但 [`UnitPrice`] 欄位完全不會格式化，因而導致價格顯示缺少任何貨幣符號，而且有四個小數位數。 若要針對不可編輯的資料列套用貨幣格式，只需將 `UnitPrice` BoundField 的 `DataFormatString` 屬性設為 `{0:c}`，並將其 `HtmlEncode` 屬性設定為 [`false`]。

[![適當地設定單價的 DataFormatString 和 HtmlEncode 屬性](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image19.png)

**圖 7**：適當地設定 `UnitPrice`的 `DataFormatString` 和 `HtmlEncode` 屬性（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image21.png)）

透過這種變更，不可編輯的資料列會將價格格式化為貨幣;不過，已編輯的資料列仍會顯示值，但不含貨幣符號和四位數。

[![無法編輯的資料列現在會格式化為貨幣值](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image22.png)

**圖 8**：無法編輯的資料列現在會格式化為貨幣值（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image24.png)）

藉由將 BoundField 的 `ApplyFormatInEditMode` 屬性設定為 `true` （預設值為 `false`），可以將 `DataFormatString` 屬性中指定的格式化指示套用至編輯介面。 請花點時間將此屬性設定為 `true`。

[![將單價 BoundField 的 ApplyFormatInEditMode 屬性設定為 true](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image25.png)

**圖 9**：將 `UnitPrice` BoundField 的 `ApplyFormatInEditMode` 屬性設定為 `true` （[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image27.png)）

隨著這項變更，在編輯過的資料列中顯示的 `UnitPrice` 值也會格式化為貨幣。

[![編輯過的資料列的 [單價] 值現在已格式化為貨幣](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image28.png)

**圖 10**：編輯過的資料列的 `UnitPrice` 值現在會格式化為貨幣（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image30.png)）

不過，使用文字方塊中的貨幣符號來更新產品（例如 $19.00）會擲回 `FormatException`。 當 GridView 嘗試將使用者提供的值指派給 ObjectDataSource 的 `UpdateParameters` 集合時，無法將 `UnitPrice` 字串 "$19.00" 轉換成參數所需的 `decimal` （請參閱 [圖 11]）。 若要解決這個問題，我們可以為 GridView 的 `RowUpdating` 事件建立事件處理常式，並讓它將使用者提供的 `UnitPrice` 剖析成貨幣格式的 `decimal`。

GridView 的 `RowUpdating` 事件會接受[GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)類型的物件做為其第二個參數，其中包含做為其中一個屬性的 `NewValues` 字典，其中包含準備好要指派給 ObjectDataSource 的 `UpdateParameters` 集合的使用者提供值。 我們可以在 `NewValues` 集合中，使用以貨幣格式剖析的十進位值來覆寫現有的 `UnitPrice` 值，並在 `RowUpdating` 事件處理常式中使用下列程式程式碼：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample4.cs)]

如果使用者已提供 `UnitPrice` 值（例如 "$19.00"），則會使用 Decimal 所計算的十進位值來覆寫這個值[。 Parse](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx)，將值剖析為貨幣。 這會在任何貨幣符號、逗號、小數點等等的事件中正確地剖析十進位，並在[NumberStyles 列舉](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx)[命名空間](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx)中使用。

[圖 11] 顯示使用者提供的 `UnitPrice`中的貨幣符號所造成的問題，以及 GridView 的 `RowUpdating` 事件處理常式如何利用來正確地剖析這類輸入。

[![編輯過的資料列的 [單價] 值現在已格式化為貨幣](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image31.png)

**圖 11**：已編輯的資料列的 `UnitPrice` 值現在會格式化為貨幣（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image33.png)）

## <a name="step-2-prohibitingnull-unitprices"></a>步驟2：禁止`NULL UnitPrices`

當資料庫設定為允許 `Products` 資料表的 `UnitPrice` 資料行中的 `NULL` 值時，我們可能會想要防止使用者造訪此特定頁面，而不指定 `NULL` `UnitPrice` 值。 也就是說，如果使用者在編輯產品資料列時無法輸入 `UnitPrice` 值，而不是將結果儲存到資料庫，而是要顯示一則訊息，告知使用者，透過此頁面，任何已編輯的產品都必須指定價格。

傳遞至 GridView 的 `RowUpdating` 事件處理常式的 `GridViewUpdateEventArgs` 物件包含 `Cancel` 屬性，如果設定為 `true`，就會終止更新進程。 讓我們擴充 `RowUpdating` 事件處理常式，將 `e.Cancel` 設定為 `true` 並顯示訊息，說明 `NewValues` 集合中的 `UnitPrice` 值為何 `null`。

首先，將標籤 Web 控制項新增至名為 `MustProvideUnitPriceMessage`的頁面。 如果使用者在更新產品時無法指定 `UnitPrice` 值，則會顯示此標籤控制項。 將標籤的 [`Text`] 屬性設為 [您必須提供產品的價格]。 我也在名為 `Warning` 的 `Styles.css` 中，使用下列定義建立了新的 CSS 類別：

[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample5.css)]

最後，將標籤的 [`CssClass`] 屬性設定為 [`Warning`]。 此時，設計工具應該會在 GridView 上方以紅色、粗體、斜體、超大型字型大小顯示警告訊息，如 [圖 12] 所示。

[![已在 GridView 上方新增標籤](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image34.png)

**圖 12**：已在 GridView 上方新增標籤（[按一下以觀看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image36.png)）

根據預設，此標籤應該是隱藏的，因此，請將其 `Visible` 屬性設定為 `Page_Load` 事件處理常式中的 `false`：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample6.cs)]

如果使用者嘗試在未指定 `UnitPrice`的情況下更新產品，我們會想要取消更新並顯示警告標籤。 擴大 GridView 的 `RowUpdating` 事件處理常式，如下所示：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample7.cs)]

如果使用者嘗試在未指定價格的情況下儲存產品，則會取消更新並顯示有用的訊息。 當資料庫（和商務邏輯）允許 `NULL` `UnitPrice` s 時，這個特定的 ASP.NET 網頁不會。

[![使用者不能將 [單價] 保留空白](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image37.png)

**圖 13**：使用者不能將 `UnitPrice` 留白（[按一下以觀看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image39.png)）

到目前為止，我們已瞭解如何使用 GridView 的 `RowUpdating` 事件，以程式設計方式改變指派給 ObjectDataSource `UpdateParameters` 集合的參數值，以及如何完全取消更新程式。 這些概念會延續到 DetailsView 和 FormView 控制項，也適用于插入和刪除。

這些工作也可以透過事件處理常式的 `Inserting`、`Updating`和 `Deleting` 事件，在 ObjectDataSource 層級完成。 這些事件會在叫用基礎物件的相關聯方法之前引發，並提供最後機會來修改輸入參數集合或直接取消作業。 這三個事件的事件處理常式會傳遞[ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx)類型的物件，其中包含兩個相關的屬性：

- [[取消](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx)]，如果設定為 [`true`]，則會取消正在執行的作業
- [輸入參數](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx)，這是 `InsertParameters`、`UpdateParameters`或 `DeleteParameters`的集合，視事件處理常式是針對 `Inserting`、`Updating`還是 `Deleting` 事件而定

為了說明如何使用 ObjectDataSource 層級的參數值，讓我們在頁面中包含 DetailsView，以允許使用者新增新的產品。 此 DetailsView 將用來提供介面，以快速將新產品新增至資料庫。 若要在加入新產品時保持一致的使用者介面，讓使用者只能輸入 `ProductName` 和 `UnitPrice` 欄位的值。 根據預設，在 DetailsView 的插入介面中未提供的值將會設定為 `NULL` 資料庫值。 不過，我們可以使用 ObjectDataSource 的 `Inserting` 事件插入不同的預設值，如我們稍後所見。

## <a name="step-3-providing-an-interface-to-add-new-products"></a>步驟3：提供介面來新增產品

從 [工具箱] 將 [DetailsView] 拖曳至 GridView 上方的設計工具，清除其 `Height` 並 `Width` 屬性，然後將它系結至已存在於頁面上的 ObjectDataSource。 這會為每個產品的欄位新增 BoundField 或 CheckBoxField。 因為我們想要使用此 DetailsView 來加入新的產品，所以我們需要從智慧標籤中選取 [啟用插入] 選項;不過，沒有這種選擇，因為 ObjectDataSource 的 `Insert()` 方法並未對應到 `ProductsBLL` 類別中的方法（回想一下，在設定資料來源時，我們將此對應設為（無），請參閱 [圖 3]）。

若要設定 ObjectDataSource，請從其智慧標籤選取 [設定資料來源] 連結，並啟動精靈。 第一個畫面可讓您變更 ObjectDataSource 所系結的基礎物件。將它設定為 [`ProductsBLL`]。 下一個畫面會列出從 ObjectDataSource 的方法到基礎物件的對應。 雖然我們明確指出 `Insert()` 和 `Delete()` 方法不應對應到任何方法，但如果您移至 [插入] 和 [刪除] 索引標籤，您會看到對應在該處。 這是因為 `ProductsBLL`的 `AddProduct` 和 `DeleteProduct` 方法會使用 `DataObjectMethodAttribute` 屬性來表示它們是分別用於 `Insert()` 和 `Delete()`的預設方法。 因此，除非有明確指定的其他值，否則 ObjectDataSource wizard 會在您每次執行嚮導時加以選取。

將 [`Insert()`] 方法保留指向 [`AddProduct`] 方法，但再次將 [刪除] 索引標籤的下拉式清單設定為 [（無）]。

[![將 [插入] 索引標籤的下拉式清單設定為 AddProduct 方法](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image40.png)

**圖 14**：將 [插入] 索引標籤的下拉式清單設定為 [`AddProduct`] 方法（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image42.png)）

[![將 [刪除] 索引標籤的下拉式清單設定為 [（無）]](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image43.png)

**圖 15**：將 [刪除] 索引標籤的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image45.png)）

進行這些變更之後，會展開 ObjectDataSource 的宣告式語法以包含 `InsertParameters` 集合，如下所示：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample8.aspx)]

重新執行嚮導，並將其加回 [`OldValuesParameterFormatString`] 屬性。 請花一些時間來清除此屬性，方法是將它設定為預設值（`{0}`），或將它從宣告式語法完全移除。

有了提供插入功能的 ObjectDataSource，DetailsView 的智慧標籤現在會包含 [啟用插入] 核取方塊;回到設計工具並核取此選項。 接下來，向下削減 DetailsView，使其只有兩個 BoundFields `ProductName` 和 `UnitPrice` 和 CommandField。 此時，DetailsView 的宣告式語法看起來應該像這樣：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample9.aspx)]

[圖 16] 顯示此頁面，在此時透過瀏覽器觀看。 如您所見，DetailsView 會列出第一項產品的名稱和價格（Chai）。 不過，我們想要的是插入介面，讓使用者可以快速地將新產品新增至資料庫。

[![DetailsView 目前以唯讀模式呈現](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image46.png)

**圖 16**： DetailsView 目前以唯讀模式轉譯（[按一下以觀看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image48.png)）

為了在其插入模式中顯示 DetailsView，我們需要將 `DefaultMode` 屬性設為 `Inserting`。 這會在第一次造訪時以插入模式轉譯 DetailsView，並在插入新記錄之後將其保留在該處。 如 [圖 17] 所示，這類 DetailsView 提供快速的介面來加入新的記錄。

[![DetailsView 提供快速新增產品的介面](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image49.png)

**圖 17**： DetailsView 提供快速新增產品的介面（[按一下以觀看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image51.png)）

當使用者輸入產品名稱和價格（例如「Acme 水」和1.99，如 [圖 17] 所示）並按一下 [插入] 時，回傳接踵而來和插入工作流程會在新增至資料庫的新產品記錄中累積。 DetailsView 會維護其插入介面，而 GridView 會自動重新系結至其資料來源，以包含新的產品，如 [圖 18] 所示。

![產品](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image52.png)

**圖 18**：產品 "Acme 水" 已新增至資料庫

雖然 [圖 18] 中的 GridView 並未顯示它，但不是來自 DetailsView 介面的產品欄位 `CategoryID`、`SupplierID`、`QuantityPerUnit`等等，都會被指派 `NULL` 資料庫值。 您可以執行下列步驟來查看這一點：

1. 前往 Visual Studio 的伺服器總管
2. 展開 `NORTHWND.MDF` 資料庫節點
3. 以滑鼠右鍵按一下 [`Products` 資料庫資料表] 節點
4. 選取 [顯示資料表資料]

這會列出 `Products` 資料表中的所有記錄。 如 [圖 19] 所示，除了 `ProductID`、`ProductName`和 `UnitPrice` 以外的所有新產品資料行都有 `NULL` 值。

[![DetailsView 中未提供的產品欄位會被指派 Null 值](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image53.png)

**圖 19**： DetailsView 中未提供的產品欄位會被指派 `NULL` 值（[按一下以查看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image55.png)）

我們可能會想要提供一或多個這些資料行值 `NULL` 以外的預設值，因為 `NULL` 不是最佳的預設選項，或資料庫資料行本身不允許 `NULL` s。 若要完成這項操作，我們可以透過程式設計方式設定 DetailsView 之 `InputParameters` 集合的參數值。 這項指派可以在 DetailsView 的 `ItemInserting` 事件或 ObjectDataSource 的 `Inserting` 事件的事件處理常式中完成。 既然我們已經討論過在資料 Web 控制項層級使用前置和後置事件，讓我們來探索這次使用 ObjectDataSource 的事件。

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>步驟4：將值指派給`CategoryID`和`SupplierID`參數

在本教學課程中，我們假設在透過這個介面新增新產品時，我們的應用程式應該指派 `CategoryID`，`SupplierID` 值1。 如先前所述，ObjectDataSource 具有一對在資料修改程式期間引發的前置和後置層級事件。 叫用其 `Insert()` 方法時，ObjectDataSource 會先引發其 `Inserting` 事件，然後再呼叫其 `Insert()` 方法已對應的方法，最後引發 `Inserted` 事件。 `Inserting` 事件處理常式為我們創造了最後一個機會來調整輸入參數，或直接取消作業。

> [!NOTE]
> 在真實世界的應用程式中，您可能會想要讓使用者指定類別和供應商，或根據某些準則或商務邏輯為他們挑選此值（而不是盲目地選取識別碼1）。 不論如何，此範例會示範如何以程式設計方式，從 ObjectDataSource 的預先層級事件設定輸入參數的值。

請花一些時間為 ObjectDataSource 的 `Inserting` 事件建立事件處理常式。 請注意，事件處理常式的第二個輸入參數是 `ObjectDataSourceMethodEventArgs`類型的物件，它具有可存取參數集合（`InputParameters`）的屬性，以及用來取消作業（`Cancel`）的屬性。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample10.cs)]

此時，`InputParameters` 屬性會包含 ObjectDataSource 的 `InsertParameters` 集合，其中具有從 DetailsView 指派的值。 若要變更其中一個參數的值，只要使用： `e.InputParameters["paramName"] = value`即可。 因此，若要將 `CategoryID` 和 `SupplierID` 設定為1的值，請調整 `Inserting` 事件處理常式，如下所示：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample11.cs)]

這次加入新產品（例如 Acme Soda）時，新產品的 [`CategoryID`] 和 [`SupplierID`] 資料行會設定為1（請參閱 [圖 20]）。

[![新產品現在已將其 [類別 Id] 和 [供應商] 值設定為1](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image56.png)

**圖 20**：新產品現在的 `CategoryID` 和 `SupplierID` 值設定為1（[按一下以觀看完整大小的影像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image58.png)）

## <a name="summary"></a>總結

在編輯、插入及刪除進程期間，資料 Web 控制項和 ObjectDataSource 都會繼續進行許多前置和後置事件。 在本教學課程中，我們已檢查預先層級的事件，並瞭解如何使用這些事件來自訂輸入參數，或從資料 Web 控制項和 ObjectDataSource 的事件全部取消資料修改作業。 在下一個教學課程中，我們將探討如何建立和使用後置事件的事件處理常式。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Jackie Goor 和 Liz Shulok。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](an-overview-of-inserting-updating-and-deleting-data-cs.md)
> [下一頁](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
