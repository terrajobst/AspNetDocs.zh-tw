---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
title: 在刪除時新增用戶端確認（C#） |Microsoft Docs
author: rick-anderson
description: 在我們到目前為止所建立的介面中，當使用者想要按一下 [編輯] 按鈕時，按一下 [刪除] 按鈕，就可以不小心刪除資料。 在此 t 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: f6e2a12a-2b5e-48fd-8db3-1e94a500c19a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: e7d53bc65fdbbfa9ce9bfa5fbdbfa0dea598eebe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623539"
---
# <a name="adding-client-side-confirmation-when-deleting-c"></a>於刪除時新增用戶端確認 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe)或[下載 PDF](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)

> 在我們到目前為止所建立的介面中，當使用者想要按一下 [編輯] 按鈕時，按一下 [刪除] 按鈕，就可以不小心刪除資料。 在本教學課程中，我們將新增在按一下 [刪除] 按鈕時顯示的用戶端確認對話方塊。

## <a name="introduction"></a>簡介

在過去數個教學課程中，我們已瞭解如何使用我們的應用程式架構、ObjectDataSource 和資料 Web 控制項，以提供插入、編輯和刪除功能。 到目前為止我們所檢查的刪除介面，都是由 [刪除] 按鈕所組成，當按下時，會導致回傳並叫用 ObjectDataSource s `Delete()` 方法。 然後，`Delete()` 方法會從商務邏輯層叫用已設定的方法，這會將呼叫向下傳播到資料存取層，並將實際的 `DELETE` 語句發行至資料庫。

雖然此使用者介面可讓訪客透過 GridView、DetailsView 或 FormView 控制項刪除記錄，但當使用者按一下 [刪除] 按鈕時，就不會有任何類型的確認。 如果使用者在想要按一下 [編輯] 時不小心按下 [刪除] 按鈕，則會改為刪除他們想要更新的記錄。 為了避免這種情況，在本教學課程中，我們將新增在按一下 [刪除] 按鈕時所顯示的用戶端確認對話方塊。

JavaScript `confirm(string)` 函式會將它的字串輸入參數顯示為強制回應對話方塊中的文字，而這兩個按鈕都隨附于 [確定] 和 [取消] （請參閱 [圖 1]）。 `confirm(string)` 函式會根據所按下的按鈕（`true`，如果使用者按一下 [確定]，則會傳回布林值，如果按下 [取消]，則會 `false`。

![JavaScript confirm （string）方法會顯示強制回應的用戶端 Messagebox](adding-client-side-confirmation-when-deleting-cs/_static/image1.png)

**圖 1**： JavaScript `confirm(string)` 方法會顯示強制回應的用戶端 Messagebox

在表單提交期間，如果 `false` 的值是從用戶端事件處理常式傳回，則會取消表單提交。 使用這項功能，我們可以讓 [刪除] 按鈕 s 用戶端 `onclick` 事件處理常式傳回 `confirm("Are you sure you want to delete this product?")`呼叫的值。 如果使用者按一下 [取消]，`confirm(string)` 會傳回 false，因此會導致表單提交取消。 在沒有回傳的情況下，將不會刪除已按一下 [刪除] 按鈕的產品。 不過，如果使用者在確認對話方塊中按一下 [確定]，回傳將會繼續 unabated，而產品將會被刪除。 如需這項技術的詳細資訊，請參閱[使用 JavaScript `confirm()` 方法來控制表單提交](http://www.webreference.com/programming/javascript/confirm/)。

如果使用範本比使用 CommandField 時，加入必要的用戶端腳本會稍有不同。 因此，在本教學課程中，我們將探討 FormView 和 GridView 範例。

> [!NOTE]
> 使用用戶端確認技術（如本教學課程中討論的），會假設您的使用者正在造訪支援 JavaScript 且已啟用 JavaScript 的瀏覽器。 如果對特定使用者而言，這兩個假設都不成立，按一下 [刪除] 按鈕會立即導致回傳（不會顯示確認 messagebox）。

## <a name="step-1-creating-a-formview-that-supports-deletion"></a>步驟1：建立支援刪除的 FormView

首先，將 FormView 加入至 `EditInsertDelete` 資料夾中的 `ConfirmationOnDelete.aspx` 頁面，並將它系結至新的 ObjectDataSource，以透過 `ProductsBLL` 類別的 `GetProducts()` 方法提取產品資訊。 同時設定 ObjectDataSource，讓 `ProductsBLL` 類別的 `DeleteProduct(productID)` 方法對應到 ObjectDataSource s `Delete()` 方法;確定 [插入和更新索引標籤] 下拉式清單已設定為 [（無）]。 最後，勾選 FormView s 智慧標籤中的 [啟用分頁] 核取方塊。

在這些步驟之後，新的 ObjectDataSource 宣告式標記看起來會像下面這樣：

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample1.aspx)]

如同過去未使用開放式平行存取的範例，請花一點時間清除 ObjectDataSource s `OldValuesParameterFormatString` 屬性。

因為它已系結至僅支援刪除的 ObjectDataSource 控制項，所以 FormView 的 `ItemTemplate` 只會提供 [刪除] 按鈕，但缺少 [新增] 和 [更新] 按鈕。 不過，FormView 的宣告式標記包含了多餘的 `EditItemTemplate` 和 `InsertItemTemplate`，可以移除。 請花一些時間自訂 `ItemTemplate`，如此就只會顯示產品資料欄位的子集。 我設定了 [我的用]，在 [供應商] 和 [類別目錄名稱] （連同 [刪除] 按鈕）上方的 `<h3>` 標題中顯示產品名稱。

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample2.aspx)]

有了這些變更，我們有一個功能完整的網頁，可讓使用者一次切換一個產品，而且只要按一下 [刪除] 按鈕，就能刪除產品。 [圖 2] 顯示透過瀏覽器觀看時，到目前為止的進度螢幕擷取畫面。

[![FormView 顯示單一產品的相關資訊](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)

**圖 2**： FormView 顯示單一產品的相關資訊（[按一下以觀看完整大小的影像](adding-client-side-confirmation-when-deleting-cs/_static/image4.png)）

## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>步驟2：從 [刪除] 按鈕用戶端的 onclick 事件呼叫 confirm （string）函數

建立 FormView 之後，最後一個步驟是設定 [刪除] 按鈕，如此一來，當訪客按下時，就會叫用 JavaScript `confirm(string)` 函數。 將用戶端腳本新增至按鈕、LinkButton 或 ImageButton s 用戶端 `onclick` 事件可以透過使用 `OnClientClick property`（這是 ASP.NET 2.0 的新手）來完成。 因為我們想要傳回 `confirm(string)` 函式的值，所以只需將此屬性設定為： `return confirm('Are you certain that you want to delete this product?');`

在這項變更之後，刪除 LinkButton 的宣告式語法看起來應該像這樣：

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample3.aspx)]

這樣就大功告成了！ [圖 3] 顯示此確認動作的螢幕擷取畫面。 按一下 [刪除] 按鈕會顯示 [確認] 對話方塊。 如果使用者按一下 [取消]，就會取消回傳並不會刪除產品。 但是，如果使用者按一下 [確定]，回傳會繼續，而且會叫用 ObjectDataSource s `Delete()` 方法，累積在要刪除的資料庫記錄中。

> [!NOTE]
> 傳遞至 `confirm(string)` JavaScript 函式的字串會以單引號（而不是引號）來分隔。 在 JavaScript 中，可以使用任一字元來分隔字串。 我們在這裡使用 [撇號]，讓傳遞至 `confirm(string)` 的字串分隔符號不會與用於 `OnClientClick` 屬性值的分隔符號造成混淆。

[當您按一下 [刪除] 按鈕時，現在會顯示確認 ![](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)

**圖 3**：按一下 [刪除] 按鈕時，現在會顯示確認（[按一下以查看完整大小的影像](adding-client-side-confirmation-when-deleting-cs/_static/image7.png)）

## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>步驟3：設定 CommandField 中 [刪除] 按鈕的 OnClientClick 屬性

直接在範本中使用按鈕、LinkButton 或 ImageButton 時，只要設定其 `OnClientClick` 屬性來傳回 JavaScript `confirm(string)` 函式的結果，就可以建立與它相關聯的確認對話方塊。 不過，CommandField-這會將刪除按鈕的欄位新增至 GridView 或 DetailsView，而不會有可透過宣告方式設定的 `OnClientClick` 屬性。 相反地，我們必須以程式設計方式參考 GridView 中的 [刪除] 按鈕，或 DetailsView 適當的 `DataBound` 事件處理常式，然後在該處設定其 `OnClientClick` 屬性。

> [!NOTE]
> 在適當的 `DataBound` 事件處理常式中設定 刪除 按鈕 s `OnClientClick` 屬性時，我們可以存取資料並系結至目前的記錄。 這表示我們可以擴充確認訊息，以包含特定記錄的詳細資料，例如「您確定要刪除 Chai 產品嗎？」 您也可以使用資料系結語法，在範本中進行這類自訂。

若要練習為 CommandField 中的 [刪除] 按鈕設定 [`OnClientClick`] 屬性，讓我們將 GridView 新增至頁面。 將此 GridView 設定為使用 FormView 使用的相同 ObjectDataSource 控制項。 也將 GridView 的 BoundFields 限制為僅包含產品的名稱、類別和供應商。 最後，勾選 GridView 的智慧標籤中的 [啟用刪除] 核取方塊。 這會將 CommandField 新增至 GridView 的 `Columns` 集合，並將其 `ShowDeleteButton` 屬性設定為 [`true`]。

進行這些變更之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample4.aspx)]

CommandField 包含單一 Delete LinkButton 實例，可以從 GridView 的 `RowDataBound` 事件處理常式以程式設計方式存取。 一旦參考之後，我們就可以據以設定其 `OnClientClick` 屬性。 使用下列程式碼，建立 `RowDataBound` 事件的事件處理常式：

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample5.cs)]

這個事件處理常式適用于資料列（將具有 [刪除] 按鈕），並以程式設計方式參考 [刪除] 按鈕。 一般會使用下列模式：

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample6.cs)]

*ButtonType*是 CommandField 按鈕、LinkButton 或 ImageButton 所使用的按鈕類型。 根據預設，CommandField 會使用 LinkButtons，但可透過 CommandField s `ButtonType property`自訂。 *CommandFieldIndex*是 GridView s `Columns` 集合中 CommandField 的序數索引，而*controlIndex*是 CommandField s `Controls` 集合內 [刪除] 按鈕的索引。 *ControlIndex*值取決於相對於 CommandField 中其他按鈕的按鈕 s 位置。 例如，如果 CommandField 中顯示的唯一按鈕是 [刪除] 按鈕，請使用索引0。 不過，如果在 [刪除] 按鈕之前有一個 [編輯] 按鈕，請使用索引2。 使用索引2的原因是因為 CommandField 在 [刪除] 按鈕之前加入了兩個控制項： [編輯] 按鈕和用來在 [編輯] 和 [刪除] 按鈕之間新增一些空格的 LiteralControl。

在我們的特定範例中，CommandField 使用 LinkButtons，而最左邊的欄位是*commandFieldIndex*為0。 由於 CommandField 中沒有其他按鈕，而是 [刪除] 按鈕，因此我們使用的*controlIndex*為0。

參考 CommandField 中的 [刪除] 按鈕之後，我們接下來會抓取系結至目前 GridView 資料列之產品的相關資訊。 最後，我們會將 [刪除] 按鈕的 `OnClientClick` 屬性設定為適當的 JavaScript，其中包含產品的名稱。 因為傳遞至 `confirm(string)` 函式的 JavaScript 字串是使用撇號來分隔，所以我們必須將出現在產品名稱內的任何撇號加以換用。 特別是，產品 s 名稱中的任何撇號都會以 "`\'`" 來進行轉義。

完成這些變更後，按一下 GridView 中的 [刪除] 按鈕會顯示自訂的確認對話方塊（請參閱 [圖 4]）。 如同來自 FormView 的確認 messagebox，如果使用者按一下 [取消]，則會取消回傳，藉此防止刪除發生。

> [!NOTE]
> 這項技術也可以用來以程式設計方式存取 DetailsView 中 CommandField 的 [刪除] 按鈕。 但是在 DetailsView 中，您 d 建立了 `DataBound` 事件的事件處理常式，因為 DetailsView 沒有 `RowDataBound` 的事件。

[![按一下 GridView 的 [刪除] 按鈕會顯示自訂的確認對話方塊](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)

**圖 4**：按一下 GridView 的 [刪除] 按鈕會顯示自訂的確認對話方塊（[按一下以查看完整大小的影像](adding-client-side-confirmation-when-deleting-cs/_static/image10.png)）

## <a name="using-templatefields"></a>使用 TemplateFields

CommandField 的缺點之一是，它的按鈕必須透過索引來存取，而且產生的物件必須轉換成適當的按鈕類型（Button、LinkButton 或 ImageButton）。 使用「魔術數位」和硬式編碼類型來邀請在執行時間之前無法探索的問題。 例如，如果您或其他開發人員在未來的某個時間點將新的按鈕加入至 CommandField （例如 [編輯] 按鈕），或變更 [`ButtonType`] 屬性，則現有程式碼仍會編譯而不會發生錯誤，但流覽頁面可能會造成例外狀況或非預期的行為，這取決於您的程式碼撰寫方式，以及所做的變更。

另一種方法是將 GridView 和 DetailsView s CommandFields 轉換成 TemplateFields。 這會產生 TemplateField，其中包含 CommandField 中每個按鈕具有 LinkButton （或按鈕或 ImageButton）的 `ItemTemplate`。 這些按鈕 `OnClientClick` 屬性可以用宣告方式指派，如同我們在 FormView 中看到的一樣，或者可以使用下列模式以程式設計方式在適當的 `DataBound` 事件處理常式中存取：

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample7.cs)]

其中， *controlID*是按鈕 `ID` 屬性的值。 雖然此模式仍然需要進行轉換的硬式編碼類型，但它不需要編制索引，而讓配置變更，而不會造成執行階段錯誤。

## <a name="summary"></a>總結

JavaScript `confirm(string)` 函數是用來控制表單提交工作流程的常用技術。 執行時，函式會顯示強制回應的用戶端對話方塊，其中包含兩個按鈕： [確定] 和 [取消]。 如果使用者按一下 [確定]，`confirm(string)` 函數會傳回 `true`;按一下 [取消] 會傳回 `false`。 此功能與瀏覽器的行為相結合，如果提交程式期間的事件處理常式傳回 `false`，就可以在刪除記錄時用來顯示確認 messagebox。

`confirm(string)` 函式可以透過控制項 s `OnClientClick` 屬性，與按鈕 Web 控制項的用戶端 `onclick` 事件處理常式相關聯。 使用範本中的 [刪除] 按鈕時（不論是在其中一個 FormView）範本中，或是在 DetailsView 或 GridView 的 TemplateField 中，可以透過宣告方式或以程式設計方式設定這個屬性，如本教學課程中所見。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](implementing-optimistic-concurrency-cs.md)
> [下一頁](limiting-data-modification-functionality-based-on-the-user-cs.md)
