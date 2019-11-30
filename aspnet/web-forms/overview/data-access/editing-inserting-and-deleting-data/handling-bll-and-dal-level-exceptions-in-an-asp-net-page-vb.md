---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
title: 在 ASP.NET 網頁中處理 BLL 和 DAL 層級的例外狀況（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將瞭解如何顯示在的插入、更新或刪除作業期間，發生例外狀況的易記、有資訊的錯誤訊息。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 129d4338-1315-4f40-89b5-2b84b807707d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
msc.type: authoredcontent
ms.openlocfilehash: ee277596ade18d2603892d134b47c2c8697836bb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620871"
---
# <a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-vb"></a>處理 ASP.NET 頁面中 BLL 和 DAL 層級的例外狀況 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_VB.exe)或[下載 PDF](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/datatutorial18vb1.pdf)

> 在本教學課程中，我們將瞭解如何在 ASP.NET 資料 Web 控制項的插入、更新或刪除作業期間發生例外狀況時，顯示易記且具資訊性的錯誤訊息。

## <a name="introduction"></a>簡介

使用分層應用程式架構從 ASP.NET web 應用程式處理資料時，需要執行下列三個一般步驟：

1. 判斷需要叫用商務邏輯層的哪一個方法，以及要將哪些參數值傳遞給它。 參數值可以硬式編碼、以程式設計方式指派，或使用者輸入的輸入。
2. 叫用方法。
3. 處理結果。 呼叫會傳回資料的 BLL 方法時，這可能牽涉到將資料系結至資料 Web 控制項。 對於修改資料的 BLL 方法，這可能包括根據傳回值執行一些動作，或妥善處理步驟2中出現的任何例外狀況。

如[先前的教學](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)課程中所見，ObjectDataSource 和資料 Web 控制項都提供步驟1和3的擴充點。 例如，GridView 會在將其域值指派給其 ObjectDataSource 的 `UpdateParameters` 集合之前，引發其 `RowUpdating` 事件。當 ObjectDataSource 完成作業之後，就會引發它的 `RowUpdated` 事件。

我們已檢查步驟1中引發的事件，並瞭解如何使用它們來自訂輸入參數或取消作業。 在本教學課程中，我們會將注意力轉向在作業完成後引發的事件。 有了這些後續層級的事件處理常式之後，就可以判斷作業期間是否發生例外狀況，並正常處理它，在畫面上顯示易記的資訊性錯誤訊息，而不是預設為標準 ASP.NET例外狀況頁面。

為了說明如何使用這些後續層級事件，讓我們建立一個頁面，其中列出可編輯的 GridView 中的產品。 更新產品時，如果引發例外狀況，我們的 ASP.NET 網頁會在 GridView 上方顯示簡短訊息，說明已發生問題。 讓我們開始吧！

## <a name="step-1-creating-an-editable-gridview-of-products"></a>步驟1：建立可編輯產品的 GridView

在上一個教學課程中，我們建立了一個可編輯的 GridView，其中只有兩個欄位，`ProductName` 和 `UnitPrice`。 這需要為 `ProductsBLL` 類別的 `UpdateProduct` 方法建立額外的多載，其中一個只接受三個輸入參數（產品的名稱、單價和識別碼），而不是每個產品欄位的參數。 在本教學課程中，我們將再次練習這項技術，建立可編輯的 GridView，其中顯示產品的名稱、每個單位的數量、單價，以及庫存中的單位，但只允許編輯庫存中的名稱、單價和單位。

為了配合此案例，我們需要 `UpdateProduct` 方法的另一個多載，一個接受四個參數：產品的名稱、單位價格、庫存單位和識別碼。 將下列方法新增至 `ProductsBLL` 類別：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample1.vb)]

完成這個方法之後，我們就可以建立 ASP.NET 網頁，讓您編輯這四個特定的產品欄位。 開啟 [`EditInsertDelete`] 資料夾中的 [`ErrorHandling.aspx`] 頁面，然後透過設計工具將 GridView 新增至頁面。 將 GridView 系結至新的 ObjectDataSource，將 `Select()` 方法對應至 `ProductsBLL` 類別的 `GetProducts()` 方法，並將 `Update()` 方法對應到剛建立的 `UpdateProduct` 多載。

[![使用接受四個輸入參數的 UpdateProduct 方法多載](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image1.png)

**圖 1**：使用接受四個輸入參數的 `UpdateProduct` 方法多載（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image3.png)）

這會建立一個具有一個 `UpdateParameters` 集合的 ObjectDataSource，其中包含四個參數，而一個 GridView 具有每個產品欄位的欄位。 ObjectDataSource 的宣告式標記會將值 `original_{0}`指派給 `OldValuesParameterFormatString` 屬性，這會造成例外狀況，因為我們的 BLL 類別不會預期傳入名為 `original_productID` 的輸入參數。 別忘了從宣告式語法中移除此設定（或將它設定為預設值 `{0}`）。

接下來，向下削減 GridView，只包含 `ProductName`、`QuantityPerUnit`、`UnitPrice`和 `UnitsInStock` BoundFields。 也可以隨意套用您認為必要的任何欄位層級格式（例如變更 `HeaderText` 屬性）。

在上一個教學課程中，我們探討了如何在唯讀模式和編輯模式中，將 `UnitPrice` BoundField 格式化為貨幣。 讓我們在這裡執行相同的動作。 回想一下，這需要將 BoundField 的 `DataFormatString` 屬性設定為 `{0:c}`、其 `HtmlEncode` 屬性設為 `false`，以及將其 `ApplyFormatInEditMode` 為 `true`，如 [圖 2] 所示。

[![將 [單價] BoundField 設定為顯示為貨幣](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image4.png)

**圖 2**：將 `UnitPrice` BoundField 設定為顯示為貨幣（[按一下以觀看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image6.png)）

在編輯介面中將 `UnitPrice` 格式化為貨幣時，需要為 GridView 的 `RowUpdating` 事件建立事件處理常式，以將貨幣格式的字串剖析成 `decimal` 值。 回想一下，最後一個教學課程中的 `RowUpdating` 事件處理常式也會進行檢查，以確保使用者提供了 `UnitPrice` 的值。 不過，在本教學課程中，我們會讓使用者省略價格。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample2.vb)]

我們的 GridView 包含 `QuantityPerUnit` BoundField，但此 BoundField 應僅供顯示之用，不應由使用者編輯。 若要進行這種排列，只要將 BoundFields ' `ReadOnly` 屬性設為 `true`即可。

[![將 QuantityPerUnit BoundField 設為唯讀](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image7.png)

**圖 3**：使 `QuantityPerUnit` BoundField 為唯讀（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image9.png)）

最後，檢查 GridView 的智慧標籤中的 [啟用編輯] 核取方塊。 完成這些步驟之後，`ErrorHandling.aspx` 頁面的設計工具看起來應該如 [圖 4] 所示。

[![移除所有必要的 BoundFields，然後勾選 [啟用編輯] 核取方塊](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image10.png)

**圖 4**：移除所有必要的 BoundFields，然後勾選 [啟用編輯] 核取方塊（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image12.png)）

此時，我們會有一份清單，列出所有產品的 `ProductName`、`QuantityPerUnit`、`UnitPrice`和 `UnitsInStock` 欄位;不過，只能編輯 [`ProductName`]、[`UnitPrice`] 和 [`UnitsInStock`] 欄位。

[![使用者現在可以輕鬆地編輯庫存欄位中的產品名稱、價格和單位](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image13.png)

**圖 5**：使用者現在可以輕鬆地編輯庫存欄位中的產品名稱、價格和單位（[按一下以觀看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image15.png)）

## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>步驟2：正常處理 DAL 層級的例外狀況

雖然可編輯的 GridView 會在使用者為已編輯的產品名稱、價格和庫存單位輸入合法的值時 wonderfully，但輸入不合法的值會導致例外狀況。 例如，省略 `ProductName` 值會導致擲回[system.data.nonullallowedexception](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp) ，因為 `ProductsRow` 類別中的 `ProductName` 屬性會將其 `AllowDBNull` 屬性設定為 `false`。如果資料庫已關閉，當嘗試連接到資料庫時，TableAdapter 會擲回 `SqlException`。 若未採取任何動作，這些例外狀況會從資料存取層反升到商務邏輯層、ASP.NET 網頁，最後到 ASP.NET 執行時間。

視 web 應用程式的設定方式，以及您是否從 `localhost`流覽應用程式而定，未處理的例外狀況可能會導致一般伺服器錯誤頁面、詳細的錯誤報表，或方便使用的網頁。 如需 ASP.NET 執行時間如何回應未攔截例外狀況的詳細資訊，請參閱[ASP.NET 中的 Web 應用程式錯誤處理](http://www.15seconds.com/issue/030102.htm)和[customErrors 元素](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx)。

[圖 6] 顯示在不指定 `ProductName` 值的情況下，嘗試更新產品時所遇到的畫面。 這是進入 `localhost`時顯示的預設詳細錯誤報表。

[![省略產品的名稱將會顯示例外狀況詳細資料](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image16.png)

**圖 6**：省略產品的名稱將會顯示例外狀況詳細資料（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image18.png)）

雖然這類例外狀況詳細資料在測試應用程式時很有用，但在遇到例外狀況的情況下，呈現具有這類畫面的終端使用者並不理想。 終端使用者可能不知道 `NoNullAllowedException` 是什麼，或為什麼會造成這種情況。 較好的方法是向使用者呈現更容易使用的訊息，說明嘗試更新產品時發生問題。

如果在執行作業時發生例外狀況，ObjectDataSource 和資料 Web 控制項中的後置層級事件，會提供偵測它的方法，並取消反升至 ASP.NET 執行時間的例外狀況。 在我們的範例中，讓我們建立 GridView 的 `RowUpdated` 事件的事件處理常式，以判斷是否已引發例外狀況，如果是，則會在標籤 Web 控制項中顯示例外狀況詳細資料。

首先，將標籤新增至 [ASP.NET] 頁面，將其 `ID` 屬性設定為 `ExceptionDetails` 並清除其 `Text` 屬性。 若要在此訊息中繪製使用者眼，請將其 [`CssClass`] 屬性設為 [`Warning`]，這是我們在上一個教學課程中新增至 `Styles.css` 檔案的 CSS 類別。 回想一下，這個 CSS 類別會以紅色、斜體、粗體、超大字型來顯示標籤的文字。

[![將標籤 Web 控制項新增至頁面](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image19.png)

**圖 7**：將標籤 Web 控制項新增至頁面（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image21.png)）

因為我們想要在發生例外狀況後立即顯示此標籤 Web 控制項，所以請在 `Page_Load` 事件處理常式中，將其 `Visible` 屬性設為 false：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample3.vb)]

使用此程式碼，在第一頁造訪和後續回傳時，`ExceptionDetails` 控制項的 `Visible` 屬性會設定為 `false`。 在具有 DAL 或 BLL 層級例外狀況的表面上，我們可以在 GridView 的 `RowUpdated` 事件處理常式中偵測到，`ExceptionDetails` 控制項的 `Visible` 屬性設定為 true。 由於 Web 控制項事件處理常式會在頁面生命週期的 `Page_Load` 事件處理常式之後發生，因此會顯示標籤。 不過，在下一次回傳時，`Page_Load` 事件處理常式會將 `Visible` 屬性還原回 `false`，再次將其從 view 中隱藏。

> [!NOTE]
> 或者，我們可以藉由在宣告式語法中指派 `Visible` 屬性 `false` 並停用其 view 狀態（將其 `EnableViewState` 屬性設定為 `false`），移除在 `Page_Load` 中設定 `ExceptionDetails` 控制項之 `Visible` 屬性的必要。 我們將在未來的教學課程中使用這種替代方法。

新增標籤控制項之後，下一步就是建立 GridView 的 `RowUpdated` 事件的事件處理常式。 在設計工具中選取 [GridView]，移至 [屬性視窗]，然後按一下閃電圖示，列出 GridView 的事件。 因為我們稍早在本教學課程中為這個事件建立了事件處理常式，所以 GridView 的 `RowUpdating` 事件應該已經有一個專案。 也請建立 `RowUpdated` 事件的事件處理常式。

![建立 GridView RowUpdated 事件的事件處理常式](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image22.png)

**圖 8**：建立 GridView 的 `RowUpdated` 事件的事件處理常式

> [!NOTE]
> 您也可以透過程式碼後置類別檔案頂端的下拉式清單來建立事件處理常式。 從左邊的下拉式清單中選取 [GridView]，然後從右側的 [`RowUpdated`] 事件。

建立這個事件處理常式會將下列程式碼新增至 ASP.NET 網頁的程式碼後置類別：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample4.vb)]

這個事件處理常式的第二個輸入參數是[GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx)類型的物件，它有三個相關的屬性可處理例外狀況：

- `Exception` 擲回之例外狀況的參考;如果未擲回任何例外狀況，此屬性的值將會是 `null`
- `ExceptionHandled` 布林值，指出是否已在 `RowUpdated` 事件處理常式中處理例外狀況;如果 `false` （預設值），則會重新擲回例外狀況，percolating 到 ASP.NET 執行時間
- `KeepInEditMode` 設定為時 `true` 已編輯的 GridView 資料列仍會保持編輯模式;如果 `false` （預設值），GridView 資料列會還原回其唯讀模式

然後，我們的程式碼應該檢查 `Exception` 是否未 `null`，這表示在執行作業時引發例外狀況。 如果是這種情況，我們想要：

- 在 [`ExceptionDetails`] 標籤中顯示使用者易記的訊息
- 表示已處理例外狀況
- 在編輯模式中保留 GridView 資料列

下列程式碼會完成下列目標：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample5.vb)]

這個事件處理常式一開始會先檢查是否 `null``e.Exception`。 如果不是，`ExceptionDetails` 標籤的 [`Visible`] 屬性會設定為 [`true`]，而其 [`Text`] 屬性會設為 [更新產品時發生問題]。 所擲回之實際例外狀況的詳細資料位於 `e.Exception` 物件的 `InnerException` 屬性中。 系統會檢查這個內部例外狀況，如果它是特定型別，則會將額外的實用訊息附加至 `ExceptionDetails` 標籤的 `Text` 屬性。 最後，`ExceptionHandled` 和 `KeepInEditMode` 屬性都設定為 [`true`]。

[圖 9] 顯示此頁面省略產品名稱時的螢幕擷取畫面;[圖 10] 顯示輸入不合法的 `UnitPrice` 值時的結果（-50）。

[![ProductName BoundField 必須包含值](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image23.png)

**圖 9**： `ProductName` BoundField 必須包含值（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image25.png)）

[不允許 ![負的單價值](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image26.png)

**圖 10**：不允許負值 `UnitPrice` 值（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image28.png)）

藉由將 [`e.ExceptionHandled`] 屬性設定為 [`true`]，`RowUpdated` 事件處理常式表示它已處理例外狀況。 因此，例外狀況不會傳播至 ASP.NET 執行時間。

> [!NOTE]
> [圖 9] 和 [10] 顯示處理因使用者輸入無效而引發之例外狀況的正常方式。 在理想的情況下，這類不正確輸入永遠不會在第一次到達商業邏輯層，因為在叫用 `ProductsBLL` 類別的 `UpdateProduct` 方法之前，ASP.NET 網頁應確保使用者的輸入有效。 在下一個教學課程中，我們將瞭解如何將驗證控制項新增至編輯和插入介面，以確保提交至商務邏輯層的資料符合商務規則。 驗證控制項不只會防止 `UpdateProduct` 方法的叫用，直到使用者提供的資料有效為止，但也會提供更具資訊的使用者體驗來識別資料輸入的問題。

## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>步驟3：正常處理 BLL 層級的例外狀況

在插入、更新或刪除資料時，資料存取層可能會在資料相關錯誤的臉部中擲回例外狀況。 資料庫可能已離線、必要的資料庫資料表資料行可能尚未指定值，或可能已違反資料表層級的條件約束。 除了嚴格的資料相關例外狀況之外，商務邏輯層也可以使用例外狀況來指出違反商務規則的時間。 例如，在[建立商業邏輯層](../introduction/creating-a-business-logic-layer-vb.md)教學課程中，我們已將商務規則檢查新增至原始的 `UpdateProduct` 多載。 具體而言，如果使用者將產品標示為已中止，我們就需要該產品不是其供應商提供的唯一。 如果違反此條件，則會擲回 `ApplicationException`。

針對在本教學課程中建立的 `UpdateProduct` 多載，讓我們新增一個禁止 `UnitPrice` 欄位設定為原始 `UnitPrice` 值兩倍以上的新值的商務規則。 若要完成此動作，請調整 `UpdateProduct` 多載，使其執行這種檢查，並在違反規則時擲回 `ApplicationException`。 更新的方法如下：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample6.vb)]

透過這種變更，任何價格更新若為現有價格的兩倍，將會導致 `ApplicationException` 擲回。 就像從 DAL 引發的例外狀況一樣，這個 BLL 引發的 `ApplicationException` 可以在 GridView 的 `RowUpdated` 事件處理常式中偵測並處理。 事實上，`RowUpdated` 事件處理常式的程式碼，如所撰寫，會正確地偵測此例外狀況，並顯示 `ApplicationException`的 `Message` 屬性值。 [圖 11] 顯示當使用者嘗試將 Chai 的價格更新為 $50.00 時的螢幕擷取畫面，其目前的價格為 $19.95 倍以上。

[![商務規則不允許價格增加，超過產品價格的兩倍](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image29.png)

**圖 11**：商務規則不允許價格增加超過產品價格的兩倍（[按一下以觀看完整大小的影像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image31.png)）

> [!NOTE]
> 在理想的情況下，我們的商務邏輯會從 `UpdateProduct` 方法多載中重構，並放入通用的方法中。 這會留給讀者的練習。

## <a name="summary"></a>總結

在插入、更新和刪除作業期間，資料 Web 控制項和 ObjectDataSource 都涉及引發 bookend 實際作業的前置和後置層級事件。 如我們在本教學課程中所見，和上一個，在使用可編輯的 GridView 時，GridView 的 `RowUpdating` 事件會引發，接著是 ObjectDataSource 的 `Updating` 事件，此時會對 ObjectDataSource 的基礎物件進行 update 命令。 在作業完成之後，ObjectDataSource 的 `Updated` 事件會引發，接著是 GridView 的 `RowUpdated` 事件。

我們可以為預先層級的事件建立事件處理常式，以便自訂輸入參數或 post 層級事件，以便檢查和回應作業的結果。 後置層級事件處理常式最常用來偵測作業期間是否發生例外狀況。 在遇到例外狀況時，這些後置層級事件處理常式可以選擇性地自行處理例外狀況。 在本教學課程中，我們已瞭解如何藉由顯示易記的錯誤訊息來處理這類例外狀況。

在下一個教學課程中，我們將瞭解如何減少因資料格式問題（例如輸入負面 `UnitPrice`）而產生之例外狀況的可能性。 具體而言，我們將探討如何將驗證控制項新增至編輯和插入介面。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Liz Shulok。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
> [下一頁](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
