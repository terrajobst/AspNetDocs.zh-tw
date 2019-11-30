---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
title: 更新和刪除現有的二進位資料（VB） |Microsoft Docs
author: rick-anderson
description: 在先前的教學課程中，我們看到 GridView 控制項如何讓您輕鬆編輯和刪除文字資料。 在本教學課程中，我們會瞭解 GridView 控制項也會如何進行 。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 3a052ced-9cf5-47b8-a400-934f0b687c26
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 27ff6941008b4e7bf6d632e4c248fd1d35fb3589
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621592"
---
# <a name="updating-and-deleting-existing-binary-data-vb"></a>更新及刪除現有的二進位資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_VB.exe)或[下載 PDF](updating-and-deleting-existing-binary-data-vb/_static/datatutorial57vb1.pdf)

> 在先前的教學課程中，我們看到 GridView 控制項如何讓您輕鬆編輯和刪除文字資料。 在本教學課程中，我們會瞭解 GridView 控制項是否也可以編輯和刪除二進位資料，不論該二進位資料是儲存在資料庫中，還是儲存在檔案系統中。

## <a name="introduction"></a>簡介

在過去三個教學課程中，我們新增了相當多的功能來處理二進位資料。 我們一開始先將 `BrochurePath` 資料行加入 `Categories` 資料表，並據以更新架構。 我們也新增了資料存取層和商務邏輯層方法，以使用 category 資料表的現有 `Picture` 欄，其中包含影像檔案的二進位內容。 我們已建立網頁，以在 GridView 中顯示二進位資料，這是手冊的下載連結，其中的類別目錄顯示在 `<img>` 元素中，並已新增 DetailsView，讓使用者可以新增新的類別並上傳其手冊和圖片資料。

剩下的工作就是編輯和刪除現有的類別，我們將在本教學課程中使用 GridView 的內建編輯和刪除功能來完成。 編輯分類時，使用者可以選擇上傳新圖片，或讓類別繼續使用現有的圖片。 在手冊中，他們可以選擇使用現有的摺頁冊、上傳新的手冊，或指出該類別已不再有相關聯的手冊。 讓我們開始吧！

## <a name="step-1-updating-the-data-access-layer"></a>步驟1：更新資料存取層

DAL 具有自動產生的 `Insert`、`Update`和 `Delete` 方法，但這些方法是根據 `CategoriesTableAdapter` s 主要查詢所產生，而不包含 `Picture` 資料行。 因此，`Insert` 和 `Update` 方法不包含用來指定類別目錄圖片之二進位資料的參數。 就像我們在[先前的教學](including-a-file-upload-option-when-adding-a-new-record-vb.md)課程中所做的一樣，在指定二進位資料時，我們必須建立新的 TableAdapter 方法來更新 `Categories` 資料表。

開啟具類型的資料集，然後從設計工具中，以滑鼠右鍵按一下 [`CategoriesTableAdapter`] 標頭，然後從內容功能表選擇 [加入查詢]，以啟動 [TableAdapter 查詢設定]。 此 wizard 一開始會詢問 TableAdapter 查詢應該如何存取資料庫。 選擇 [使用 SQL 語句]，然後按 [下一步]。 下一個步驟會提示您輸入要產生的查詢類型。 因為我們會重新建立查詢，將新記錄新增至 `Categories` 資料表，請選擇 [更新]，然後按 [下一步]。

[![選取 [更新] 選項](updating-and-deleting-existing-binary-data-vb/_static/image2.png)](updating-and-deleting-existing-binary-data-vb/_static/image1.png)

**圖 1**：選取更新選項（[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image3.png)）

我們現在需要指定 `UPDATE` SQL 語句。 Wizard 會自動建議一個對應于 TableAdapter s main 查詢的 `UPDATE` 語句（一個更新 `CategoryName`、`Description`和 `BrochurePath` 值）。 變更語句，讓 `Picture` 資料行連同 `@Picture` 參數一起包含，如下所示：

[!code-sql[Main](updating-and-deleting-existing-binary-data-vb/samples/sample1.sql)]

Wizard 的最後一個畫面會要求我們將新的 TableAdapter 方法命名為。 輸入 `UpdateWithPicture`，然後按一下 [完成]。

[![命名新的 TableAdapter 方法 UpdateWithPicture](updating-and-deleting-existing-binary-data-vb/_static/image5.png)](updating-and-deleting-existing-binary-data-vb/_static/image4.png)

**圖 2**：將新的 TableAdapter 方法命名 `UpdateWithPicture` （[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image6.png)）

## <a name="step-2-adding-the-business-logic-layer-methods"></a>步驟2：新增商務邏輯層方法

除了更新 DAL，我們還需要更新 BLL，以包含更新和刪除分類的方法。 這些是將從展示層叫用的方法。

若要刪除類別目錄，我們可以使用 `CategoriesTableAdapter` s 自動產生的 `Delete` 方法。 將下列方法新增至 `CategoriesBLL` 類別：

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample2.vb)]

在本教學課程中，我們會建立兩個方法來更新類別目錄-一種會預期二進位圖片資料，並叫用剛才新增至 `CategoriesTableAdapter` 的 `UpdateWithPicture` 方法，另一個只接受 `CategoryName`、`Description`和 `BrochurePath` 值，並使用 `CategoriesTableAdapter` class s 自動產生的 `Update` 語句。 使用兩種方法背後的原理是，在某些情況下，使用者可能會想要更新分類的圖片及其其他欄位，在這種情況下，使用者必須上傳新圖片。 然後，可以在 `UPDATE` 語句中使用上傳的圖片的二進位資料。 在其他情況下，使用者可能只會想要更新名稱和描述。 但是，如果 `UPDATE` 語句也需要 `Picture` 資料行的二進位資料，則我們也必須提供該資訊。 這會需要額外的資料庫行程，以傳回所編輯之記錄的圖片資料。 因此，我們想要兩個 `UPDATE` 方法。 商務邏輯層會根據更新類別目錄時是否提供圖片資料，決定要使用哪一個。

為了方便這項工作，請將兩個方法加入至 `CategoriesBLL` 類別，兩者都命名為 `UpdateCategory`。 第一個應該接受三個 `String` s、`Byte` 陣列和 `Integer` 作為其輸入參數;第二個，只有三個 `String` 和一個 `Integer`。 `String` 輸入參數適用于類別目錄的名稱、描述和手冊檔案路徑，`Byte` 陣列適用于類別目錄圖片的二進位內容，而 `Integer` 則識別要更新之記錄的 `CategoryID`。 請注意，如果傳入的 `Byte` 陣列 `Nothing`，第一個多載會叫用第二個多載：

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample3.vb)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>步驟3：在插入和視圖功能上進行複製

在[先前的教學](including-a-file-upload-option-when-adding-a-new-record-vb.md)課程中，我們建立了一個名為 `UploadInDetailsView.aspx` 的頁面，其中列出 GridView 中的所有類別，並提供 DetailsView 來將新的類別新增至系統。 在本教學課程中，我們將擴充 GridView 以包含編輯和刪除支援。 改為從 `UploadInDetailsView.aspx`繼續工作，而不是從相同的資料夾 `~/BinaryData`，將本教學課程的變更放在 `UpdatingAndDeleting.aspx` 頁面。 將宣告式標記和程式碼從 `UploadInDetailsView.aspx` 複製並貼到 `UpdatingAndDeleting.aspx`。

從開啟 [`UploadInDetailsView.aspx`] 頁面開始。 複製 `<asp:Content>` 元素中的所有宣告式語法，如 [圖 3] 所示。 接下來，開啟 `UpdatingAndDeleting.aspx`，並將此標記貼入其 `<asp:Content>` 元素中。 同樣地，將程式碼從 `UploadInDetailsView.aspx` page s 程式碼後置類別複製到 `UpdatingAndDeleting.aspx`。

[![從 UploadInDetailsView 複製宣告式標記](updating-and-deleting-existing-binary-data-vb/_static/image8.png)](updating-and-deleting-existing-binary-data-vb/_static/image7.png)

**圖 3**：從 `UploadInDetailsView.aspx` 複製宣告式標記（[按一下以觀看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image9.png)）

複製宣告式標記和程式碼之後，請造訪 `UpdatingAndDeleting.aspx`。 您應該會看到相同的輸出，並具有與上一個教學課程中 `UploadInDetailsView.aspx` 頁相同的使用者體驗。

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>步驟4：新增對 ObjectDataSource 和 GridView 的刪除支援

如同我們在[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教學課程的簡介中所討論，GridView 提供了內建的刪除功能，而且如果格線基礎資料來源支援刪除，則可以在核取方塊的滴答啟用這些功能。 目前 GridView 所系結的 ObjectDataSource （`CategoriesDataSource`）不支援刪除。

若要解決此問題，請按一下 [ObjectDataSource s] 智慧標籤中的 [設定資料來源] 選項，以啟動精靈。 第一個畫面顯示 ObjectDataSource 已設定為與 `CategoriesBLL` 類別搭配使用。 按 [下一步]。 目前，只會指定 ObjectDataSource s `InsertMethod` 和 `SelectMethod` 屬性。 不過，此嚮導會分別自動填入 [更新] 和 [刪除] 索引標籤中的下拉式清單，其中包含 `UpdateCategory` 和 `DeleteCategory` 方法。 這是因為在 `CategoriesBLL` 類別中，我們將這些方法標記為使用 `DataObjectMethodAttribute` 做為更新和刪除的預設方法。

現在，請將 [更新] 索引標籤的下拉式清單設定為 [（無）]，但讓 [刪除] 索引標籤的下拉式清單設定為 [`DeleteCategory`]。 我們會在步驟6中返回此嚮導，以新增更新支援。

[![將 ObjectDataSource 設定為使用 DeleteCategory 方法](updating-and-deleting-existing-binary-data-vb/_static/image11.png)](updating-and-deleting-existing-binary-data-vb/_static/image10.png)

**圖 4**：設定 ObjectDataSource 以使用 `DeleteCategory` 方法（[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image12.png)）

> [!NOTE]
> 完成此嚮導之後，Visual Studio 可能會詢問您是否要重新整理欄位和金鑰，這會重新產生資料 Web 控制項欄位。 選擇 [否]，因為選擇 [是] 將會覆寫您所做的任何欄位自訂。

ObjectDataSource 現在會包含其 `DeleteMethod` 屬性和 `DeleteParameter`的值。 請記得，使用 wizard 來指定方法時，Visual Studio 將 ObjectDataSource s `OldValuesParameterFormatString` 屬性設定為 `original_{0}`，這會造成 update 和 delete 方法調用的問題。 因此，請完全清除此屬性，或將它重設為預設值 `{0}`。 如果您需要重新整理此 ObjectDataSource 屬性的記憶體，請參閱[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教學課程的總覽。

完成 wizard 並修正 `OldValuesParameterFormatString`之後，ObjectDataSource s 宣告式標記看起來應該如下所示：

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample4.aspx)]

設定 ObjectDataSource 之後，請檢查 gridview 的智慧標籤中的 [啟用刪除] 核取方塊，以將刪除功能新增至 GridView。 這會將 CommandField 新增至 GridView，其 `ShowDeleteButton` 屬性設為 `True`。

[![啟用 GridView 中的刪除支援](updating-and-deleting-existing-binary-data-vb/_static/image14.png)](updating-and-deleting-existing-binary-data-vb/_static/image13.png)

**圖 5**：啟用在 GridView 中刪除的支援（[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image15.png)）

請花點時間測試刪除功能。 `Products` 資料表 s `CategoryID` 和 `Categories` 表 s `CategoryID`之間有外鍵，因此如果您嘗試刪除前八個類別中的任何一個，您就會收到外鍵條件約束違規例外狀況。 若要測試這項功能，請加入新的類別，同時提供手冊和圖片。 [圖 6] 所示的 [我的測試] 分類包含名為 `Test.pdf` 的測試手冊檔案和測試圖片。 [圖 7] 顯示加入測試分類之後的 GridView。

[![加入具有手冊和影像的測試分類](updating-and-deleting-existing-binary-data-vb/_static/image17.png)](updating-and-deleting-existing-binary-data-vb/_static/image16.png)

**圖 6**：加入具有手冊和影像的測試分類（[按一下以觀看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image18.png)）

[插入測試分類之後 ![，會顯示在 GridView 中](updating-and-deleting-existing-binary-data-vb/_static/image20.png)](updating-and-deleting-existing-binary-data-vb/_static/image19.png)

**圖 7**：插入測試分類之後，它會顯示在 GridView 中（[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image21.png)）

在 Visual Studio 中，重新整理方案總管。 您現在應該會在 [`~/Brochures`] 資料夾中看到新的檔案，`Test.pdf` （請參閱 [圖 8]）。

接下來，按一下 [測試分類] 資料列中的 [刪除] 連結，使頁面回傳，而 `CategoriesBLL` 類別 `DeleteCategory` 方法引發。 這會叫用 DAL s `Delete` 方法，使適當的 `DELETE` 語句傳送到資料庫。 然後，資料會重新系結至 GridView，而標記會傳回給用戶端，而測試分類則不會再出現。

雖然刪除工作流程已成功從 `Categories` 資料表移除測試分類記錄，但它並不會從 web 伺服器的檔案系統中移除其手冊檔。 重新整理方案總管，您會看到 `Test.pdf` 仍留在 [`~/Brochures`] 資料夾中。

![未從 Web 服務器的檔案系統中刪除 Test .pdf 檔案](updating-and-deleting-existing-binary-data-vb/_static/image1.gif)

**圖 8**：未從 Web 服務器 s 檔案系統刪除 `Test.pdf` 檔案

## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>步驟5：移除已刪除的分類手冊檔案

將二進位資料儲存在資料庫外部的其中一個缺點，就是在刪除相關聯的資料庫記錄時，必須採取額外的步驟來清除這些檔案。 GridView 和 ObjectDataSource 提供了在執行 delete 命令之前和之後引發的事件。 我們實際上需要為前置和後置動作事件建立事件處理常式。 在刪除 `Categories` 記錄之前，我們必須先決定其 PDF 檔案的路徑，但不想要在刪除類別之前刪除該 PDF，以免發生某些例外狀況，而且不會刪除類別。

GridView s [`RowDeleting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)會在叫用 ObjectDataSource s delete 命令之前引發，而其[`RowDeleted` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx)會在之後引發。 使用下列程式碼，建立這兩個事件的事件處理常式：

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample5.vb)]

在 `RowDeleting` 事件處理常式中，要刪除之資料列的 `CategoryID` 是從 GridView 的 `DataKeys` 集合中抓取的，這可以透過 `e.Keys` 集合在此事件處理常式中存取。 接下來，會叫用 `CategoriesBLL` 類別 `GetCategoryByCategoryID(categoryID)`，以傳回有關要刪除之記錄的資訊。 如果傳回的 `CategoriesDataRow` 物件具有非`NULL``BrochurePath` 值，則會將它儲存在頁面變數 `deletedCategorysPdfPath`，以便在 `RowDeleted` 事件處理常式中刪除檔案。

> [!NOTE]
> 我們可能會將 `BrochurePath` 新增至 GridView 的 `DataKeyNames` 屬性，並透過 `e.Keys` 集合存取記錄 s 值，而不是抓取 `RowDeleting` 事件處理常式中所刪除之 `Categories` 記錄的 `BrochurePath` 詳細資料。 這麼做會稍微增加 GridView 的 view 狀態大小，但會減少所需的程式碼數量，並節省資料庫的旅程。

叫用 ObjectDataSource s 基礎 delete 命令之後，GridView 的 `RowDeleted` 事件處理常式就會引發。 如果刪除資料時沒有任何例外狀況，而且有 `deletedCategorysPdfPath`的值，則會從檔案系統中刪除 PDF。 請注意，您不需要這個額外的程式碼，就能清除與其圖片相關聯的類別 s 二進位資料。 這是因為圖片資料會直接儲存在資料庫中，因此刪除 `Categories` 資料列也會刪除該分類的圖片資料。

加入兩個事件處理常式之後，請再次執行此測試案例。 刪除類別時，也會一併刪除其相關聯的 PDF。

更新現有與記錄相關聯的二進位資料，可提供一些有趣的挑戰。 本教學課程的其餘部分將深入探討至手冊和圖片的新增更新功能。 步驟6探討在步驟7查看更新圖片時，更新手冊資訊的技術。

## <a name="step-6-updating-a-category-s-brochure"></a>步驟6：更新類別目錄手冊

如如何插入、更新和刪除資料教學課程中所述，GridView 提供內建的資料列層級編輯支援，可由核取方塊的滴答來執行（如果已適當設定其基礎資料來源）。 目前，`CategoriesDataSource` ObjectDataSource 尚未設定為包含更新支援，因此請在中將它加入。

按一下 [ObjectDataSource] wizard 中的 [設定資料來源] 連結，然後繼續進行第二個步驟。 因為 `CategoriesBLL`中使用了 `DataObjectMethodAttribute`，所以 [更新] 下拉式清單應該會自動填入接受四個輸入參數的 `UpdateCategory` 多載（適用于所有資料行，但 `Picture`）。 變更此參數，讓它使用具有五個參數的多載。

[![將 ObjectDataSource 設定為使用包含圖片參數的 UpdateCategory 方法](updating-and-deleting-existing-binary-data-vb/_static/image23.png)](updating-and-deleting-existing-binary-data-vb/_static/image22.png)

**圖 9**：設定 ObjectDataSource 使用包含 `Picture` 參數的 `UpdateCategory` 方法（[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image24.png)）

ObjectDataSource 現在會包含其 `UpdateMethod` 屬性的值，以及對應的 `UpdateParameter` s。 如步驟4所述，當使用 [設定資料來源] wizard 時，Visual Studio 將 ObjectDataSource s `OldValuesParameterFormatString` 屬性設定為 `original_{0}`。 這會造成 update 和 delete 方法調用的問題。 因此，請完全清除此屬性，或將它重設為預設值 `{0}`。

完成 wizard 並修正 `OldValuesParameterFormatString`之後，ObjectDataSource s 宣告式標記應該如下所示：

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample6.aspx)]

若要開啟 GridView 的內建編輯功能，請核取 [GridView] 智慧標籤中的 [啟用編輯] 選項。 這會將 [CommandField] `ShowEditButton` 屬性設定為 [`True`]，導致新增 [編輯] 按鈕（以及編輯的資料列的 [更新] 和 [取消] 按鈕）。

[![設定 GridView 以支援編輯](updating-and-deleting-existing-binary-data-vb/_static/image26.png)](updating-and-deleting-existing-binary-data-vb/_static/image25.png)

**圖 10**：設定 GridView 以支援編輯（[按一下以觀看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image27.png)）

透過瀏覽器造訪頁面，然後按一下其中一個資料列的 [編輯] 按鈕。 `CategoryName` 和 `Description` BoundFields 會轉譯成文字方塊。 `BrochurePath` TemplateField 缺少 `EditItemTemplate`，因此它會繼續顯示其 `ItemTemplate` 手冊的連結。 `Picture` ImageField 會轉譯為 TextBox，其 `Text` 屬性會被指派 ImageField s `DataImageUrlField` 值的值，在此情況下 `CategoryID`。

[![GridView 缺少 BrochurePath 的編輯介面](updating-and-deleting-existing-binary-data-vb/_static/image29.png)](updating-and-deleting-existing-binary-data-vb/_static/image28.png)

**圖 11**： GridView 缺少 `BrochurePath` 的編輯介面（[按一下以觀看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image30.png)）

## <a name="customizing-thebrochurepaths-editing-interface"></a>自訂`BrochurePath`s 編輯介面

我們需要為 `BrochurePath` TemplateField 建立一個編輯介面，讓使用者可以：

- 將類別目錄的手冊保持原狀，
- 藉由上傳新的手冊來更新類別目錄手冊，或
- 完全移除分類的手冊（如果類別目錄不再具有相關聯的手冊）。

我們也需要更新 `Picture` ImageField s 編輯介面，但我們會在步驟7中取得這項功能。

從 GridView 的智慧標籤中，按一下 編輯範本 連結，然後從下拉式清單中選取 `BrochurePath` TemplateField s `EditItemTemplate`。 將 RadioButtonList Web 控制項加入此範本，並將其 `ID` 屬性設為 `BrochureOptions`，並將其 `AutoPostBack` 屬性設定為 `True`。 從屬性視窗按一下 [`Items`] 屬性中的省略號，這會顯示 [`ListItem` 集合編輯器]。 分別新增下列三個選項和 `Value` s 1、2和3：

- 使用目前的手冊
- 移除目前的手冊
- 上傳新的手冊

將第一個 `ListItem` s `Selected` 屬性設定為 [`True`]。

![將三個 ListItems 新增至 RadioButtonList](updating-and-deleting-existing-binary-data-vb/_static/image2.gif)

**圖 12**：將三個 `ListItem` 新增至 RadioButtonList

在 RadioButtonList 底下，新增名為 `BrochureUpload`的 FileUpload 控制項。 將其 [`Visible`] 屬性設定為 [`False`]。

[![將 RadioButtonList 和 FileUpload 控制項新增至 EditItemTemplate](updating-and-deleting-existing-binary-data-vb/_static/image32.png)](updating-and-deleting-existing-binary-data-vb/_static/image31.png)

**圖 13**：將 RadioButtonList 和 FileUpload 控制項新增至 `EditItemTemplate` （[按一下以觀看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image33.png)）

此 RadioButtonList 會為使用者提供三個選項。 其概念是，只有在選取 [上傳新的手冊] 的最後一個選項時，才會顯示 FileUpload 控制項。 若要完成此動作，請建立 RadioButtonList s `SelectedIndexChanged` 事件的事件處理常式，並新增下列程式碼：

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample7.vb)]

由於 RadioButtonList 和 FileUpload 控制項是在範本內，因此我們必須撰寫一些程式碼，以程式設計方式存取這些控制項。 `SelectedIndexChanged` 事件處理常式會在 `sender` 輸入參數中傳遞 RadioButtonList 的參考。 若要取得 FileUpload 控制項，我們必須取得 RadioButtonList 的父控制項，並從該處使用 `FindControl("controlID")` 方法。 一旦參考了 RadioButtonList 和 FileUpload 控制項，FileUpload 控制項 s `Visible` 屬性就會設定為 `True` 只有在 RadioButtonList s `SelectedValue` 等於3，這是上傳新手冊 `ListItem`的 `Value`。

將此程式碼備妥之後，請花點時間測試編輯介面。 按一下資料列的 [編輯] 按鈕。 一開始，應選取 [使用目前的摺頁冊] 選項。 變更選取的索引會導致回傳。 如果選取了第三個選項，則會顯示 FileUpload 控制項，否則會隱藏。 [圖 14] 顯示第一次按一下 [編輯] 按鈕時的編輯介面;[圖 15] 顯示選取 [上傳新的摺頁冊] 選項之後的介面。

[![一開始會選取 [使用目前的摺頁冊] 選項](updating-and-deleting-existing-binary-data-vb/_static/image35.png)](updating-and-deleting-existing-binary-data-vb/_static/image34.png)

**圖 14**：一開始會選取 [使用目前的摺頁冊] 選項（[按一下以觀看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image36.png)）

[![選擇 [上傳新的手冊] 選項會顯示 FileUpload 控制項](updating-and-deleting-existing-binary-data-vb/_static/image38.png)](updating-and-deleting-existing-binary-data-vb/_static/image37.png)

**圖 15**：選擇 [上傳新的手冊] 選項會顯示 FileUpload 控制項（[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image39.png)）

## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>儲存手冊檔案並更新`BrochurePath`的資料行

按一下 GridView 的 [更新] 按鈕時，就會引發其 `RowUpdating` 事件。 會叫用 ObjectDataSource s update 命令，然後引發 GridView 的 `RowUpdated` 事件。 如同刪除工作流程，我們需要建立這兩個事件的事件處理常式。 在 `RowUpdating` 事件處理常式中，我們需要根據 `BrochureOptions` RadioButtonList 的 `SelectedValue` 來決定要採取的動作：

- 如果 `SelectedValue` 是1，我們想要繼續使用相同的 `BrochurePath` 設定。 因此，我們需要將 ObjectDataSource s `brochurePath` 參數設定為所要更新之記錄的現有 `BrochurePath` 值。 您可以使用 `e.NewValues["brochurePath"] = value`來設定 ObjectDataSource s `brochurePath` 參數。
- 如果 `SelectedValue` 為2，則我們想要將記錄的 `BrochurePath` 值設定為 [`NULL`]。 這可以藉由將 ObjectDataSource s `brochurePath` 參數設定為 `Nothing`來完成，這會導致 `UPDATE` 語句中使用資料庫 `NULL`。 如果有現有的摺頁冊檔案正在移除，我們必須刪除現有的檔案。 不過，我們只想要在更新完成但未引發例外狀況時執行此動作。
- 如果 `SelectedValue` 是3，則我們想要確保使用者已上傳 PDF 檔案，然後將它儲存至檔案系統，並更新記錄的 `BrochurePath` 資料行值。 此外，如果有現有的摺頁冊檔案正在被取代，我們就必須刪除先前的檔案。 不過，我們只想要在更新完成但未引發例外狀況時執行此動作。

當 RadioButtonList s `SelectedValue` 為3時必須完成的步驟，與 DetailsView s `ItemInserting` 事件處理常式所使用的步驟完全相同。 從我們在[上一個教學](including-a-file-upload-option-when-adding-a-new-record-vb.md)課程中新增的 DetailsView 控制項加入新的分類記錄時，就會執行此事件處理常式。 因此，它對我們將此功能重構成不同的方法。 具體來說，我將通用功能移至兩個方法：

- `ProcessBrochureUpload(FileUpload, out bool)` 接受 FileUpload 控制項實例的輸入，以及指定是否應該繼續執行刪除或編輯作業的輸出布林值，或是因某些驗證錯誤而應取消的輸出布林值。 這個方法會傳回已儲存檔案的路徑，如果未儲存任何檔案，則傳回 `null`。
- `DeleteRememberedBrochurePath` 會刪除頁面變數中的路徑所指定的檔案，`deletedCategorysPdfPath` 如果 `deletedCategorysPdfPath` 不 `null`。

這兩種方法的程式碼如下所示。 請注意上一個教學課程中 `ProcessBrochureUpload` 和 DetailsView s `ItemInserting` 事件處理常式之間的相似性。 在本教學課程中，我已更新 DetailsView 的事件處理常式，以使用這些新的方法。 下載與本教學課程相關的程式碼，以查看 DetailsView s 事件處理常式的修改。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample8.vb)]

GridView 的 `RowUpdating` 和 `RowUpdated` 事件處理常式會使用 `ProcessBrochureUpload` 和 `DeleteRememberedBrochurePath` 方法，如下列程式碼所示：

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample9.vb)]

請注意，`RowUpdating` 事件處理常式如何使用一系列的條件陳述式，根據 `BrochureOptions` RadioButtonList s `SelectedValue` 屬性值來執行適當的動作。

將此程式碼備妥之後，您就可以編輯類別目錄，並使用其目前的手冊、不使用手冊，或上傳新的。 請繼續並試試看。在 `RowUpdating` 中設定中斷點，並 `RowUpdated` 事件處理常式，以瞭解工作流程的意義。

## <a name="step-7-uploading-a-new-picture"></a>步驟7：上傳新圖片

`Picture` ImageField s 編輯介面會轉譯成一個文字方塊，其中填入其 `DataImageUrlField` 屬性的值。 在編輯工作流程期間，GridView 會將參數傳遞給 ObjectDataSource，其參數 s 名稱為 ImageField s `DataImageUrlField` 屬性的值，而參數 s 值則是輸入至編輯介面中文字方塊的值。 當影像儲存為檔案系統上的檔案，且 `DataImageUrlField` 包含影像的完整 URL 時，就適合使用此行為。 在這種情況下，編輯介面會在文字方塊中顯示影像的 URL，使用者可以變更並儲存回資料庫。 授與此預設介面，不允許使用者上傳新的影像，但它可讓他們將影像的 URL 從目前的值變更為另一個。 不過，在本教學課程中，ImageField 的預設編輯介面無法滿足，因為 `Picture` 的二進位資料會直接儲存在資料庫中，而 `DataImageUrlField` 屬性只會保存 `CategoryID`。

若要進一步瞭解當使用者以 ImageField 編輯資料列時，在本教學課程中會發生什麼事，請考慮下列範例：使用者編輯具有 `CategoryID` 10 的資料列，而使 `Picture` ImageField 轉譯為值為10的 textbox。 假設使用者將此文字方塊中的值變更為50，然後按一下 [更新] 按鈕。 發生回傳，GridView 一開始會建立名為 `CategoryID` 的參數，其值為50。 不過，在 GridView 傳送此參數（以及 `CategoryName` 和 `Description` 參數）之前，它會從 `DataKeys` 集合的值中加入。 因此，它會以目前的資料列 s 基礎 `CategoryID` 值10來覆寫 `CategoryID` 參數。 簡言之，ImageField s 編輯介面不會影響本教學課程的編輯工作流程，因為 ImageField s `DataImageUrlField` 屬性和方格 `DataKey` 值的名稱是同一個。

雖然 ImageField 可讓您輕鬆地根據資料庫資料顯示影像，但我們不想在編輯介面中提供文字方塊。 相反地，我們想要提供 FileUpload 控制項，讓使用者可以用來變更分類的圖片。 與 `BrochurePath` 值不同的是，在這些教學課程中，我們決定要求每個類別都必須有一張圖片。 因此，我們不需要讓使用者指出沒有相關聯的圖片。使用者可以上傳新圖片，或將目前的圖片保持原狀。

若要自訂 ImageField s 編輯介面，我們必須將它轉換成 TemplateField。 從 GridView 的智慧標籤中，按一下 [編輯資料行] 連結，選取 ImageField，然後按一下 [將此欄位轉換成 TemplateField] 連結。

![將 ImageField 轉換成 TemplateField](updating-and-deleting-existing-binary-data-vb/_static/image3.gif)

**圖 16**：將 ImageField 轉換成 TemplateField

以這種方式將 ImageField 轉換成 TemplateField 時，會產生包含兩個範本的 TemplateField。 如下列宣告式語法所示，`ItemTemplate` 包含一個影像 Web 控制項，其 `ImageUrl` 屬性是使用以 ImageField s `DataImageUrlField` 和 `DataImageUrlFormatString` 屬性為基礎的資料系結語法所指派。 `EditItemTemplate` 包含一個 TextBox，其 `Text` 屬性系結至 `DataImageUrlField` 屬性所指定的值。

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample10.aspx)]

我們需要更新 `EditItemTemplate`，才能使用 FileUpload 控制項。 從 GridView 的智慧標籤按一下 [編輯範本] 連結，然後從下拉式清單中選取 `Picture` TemplateField s `EditItemTemplate`。 在範本中，您應該會看到一個 TextBox，請移除這個。 接下來，將 [FileUpload] 控制項從 [工具箱] 拖曳至範本，將其 `ID` 設定為 [`PictureUpload`]。 此外，新增文字以變更分類的圖片，指定新圖片。 若要讓分類的圖片維持不變，請一併將欄位保留空白。

[![將 FileUpload 控制項新增至 EditItemTemplate](updating-and-deleting-existing-binary-data-vb/_static/image41.png)](updating-and-deleting-existing-binary-data-vb/_static/image40.png)

**圖 17**：將 FileUpload 控制項新增至 `EditItemTemplate` （[按一下以查看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image42.png)）

自訂編輯介面之後，請在瀏覽器中查看進度。 以唯讀模式來流覽資料列時，類別目錄的影像會顯示為先前的狀態，但是按一下 [編輯] 按鈕會以文字呈現圖片資料行與 FileUpload 控制項。

[![編輯介面包含 FileUpload 控制項](updating-and-deleting-existing-binary-data-vb/_static/image44.png)](updating-and-deleting-existing-binary-data-vb/_static/image43.png)

**圖 18**：編輯介面包含 FileUpload 控制項（[按一下以觀看完整大小的影像](updating-and-deleting-existing-binary-data-vb/_static/image45.png)）

回想一下，ObjectDataSource 已設定為呼叫 `CategoriesBLL` 類別 s `UpdateCategory` 方法，以接受圖片的二進位資料作為 `Byte` 陣列的輸入。 不過，如果 `Nothing`此陣列，則會呼叫替代的 `UpdateCategory` 多載，這會發出不會修改 `Picture` 資料行的 `UPDATE` SQL 語句，因此不會讓類別目錄的目前圖片保持不變。 因此，在 GridView 的 `RowUpdating` 事件處理常式中，我們需要以程式設計方式參考 `PictureUpload` FileUpload 控制項，並判斷是否已上傳檔案。 如果沒有上傳，則*不*想要指定 `picture` 參數的值。 另一方面，如果檔案已上傳到 `PictureUpload` FileUpload 控制項中，我們想要確保它是 JPG 檔案。 如果是，我們可以透過 `picture` 參數，將其二進位內容傳送給 ObjectDataSource。

就像步驟6中所使用的程式碼一樣，這裡所需的大部分程式碼都已經存在於 DetailsView s `ItemInserting` 事件處理常式中。 因此，我已將通用功能重構為新的方法，`ValidPictureUpload`，並更新 `ItemInserting` 事件處理常式以使用此方法。

將下列程式碼加入至 GridView 的 `RowUpdating` 事件處理常式的開頭。 這段程式碼很重要，因為我們不想要將手冊儲存到 web 伺服器的檔案系統（如果上傳了不正確圖片檔案的話）。

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample11.vb)]

`ValidPictureUpload(FileUpload)` 方法會將 FileUpload 控制項當做其唯一的輸入參數，並檢查上傳的檔案 s 延伸模組，以確保上傳的檔案是 JPG;只有在圖片檔案上傳時，才會呼叫它。 如果未上傳任何檔案，則不會設定圖片參數，因此會使用其預設值 `Nothing`。 如果已上傳圖片，且 `ValidPictureUpload` 傳回 `True`，則會將所上傳影像的二進位資料指派給 `picture` 參數;如果方法傳回 `False`，就會取消更新工作流程，並結束事件處理常式。

`ValidPictureUpload(FileUpload)` 的方法程式碼（從 DetailsView s `ItemInserting` 事件處理常式重構）如下所示：

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample12.vb)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>步驟8：使用 Jpg 取代原始類別圖片

回想一下，原始八個類別的圖片是包裝在 OLE 標頭中的點陣圖檔案。 既然我們已新增編輯現有記錄圖片的功能，請花一點時間以 Jpg 取代這些點陣圖。 如果您想要繼續使用目前的類別目錄圖片，您可以執行下列步驟，將它們轉換成 Jpg：

1. 將點陣圖影像儲存至硬碟。 請造訪瀏覽器中的 [`UpdatingAndDeleting.aspx`] 頁面，並針對前八個類別，以滑鼠右鍵按一下影像，然後選擇 [儲存] 圖片。
2. 在您選擇的影像編輯器中開啟影像。 例如，您可以使用 Microsoft Paint。
3. 將點陣圖儲存為 JPG 影像。
4. 使用 JPG 檔案，透過編輯介面來更新類別目錄的圖片。

編輯分類並上傳 JPG 影像之後，影像將不會在瀏覽器中轉譯，因為 [`DisplayCategoryPicture.aspx`] 頁面會從前八個類別的圖片中去除前78個位元組。 藉由移除執行 OLE 標頭去除的程式碼來修正此問題。 這麼做之後，`DisplayCategoryPicture.aspx``Page_Load` 事件處理常式應該只會有下列程式碼：

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample13.vb)]

> [!NOTE]
> [`UpdatingAndDeleting.aspx`] 頁面的插入和編輯介面可以使用更多工具。 DetailsView 和 GridView 中的 `CategoryName` 和 `Description` BoundFields 應該轉換成 TemplateFields。 由於 `CategoryName` 不允許 `NULL` 值，因此應該加入 RequiredFieldValidator。 而且 [`Description`] 文字方塊應該會轉換成多行文字方塊。 我將這些完成的潤色留給您的練習。

## <a name="summary"></a>總結

本教學課程會完成使用二進位資料的檢查。 在本教學課程和前三個中，我們已瞭解如何將二進位資料儲存在檔案系統上，或直接存放在資料庫中。 使用者可以從硬碟機選取檔案並將其上傳至 web 伺服器，以將二進位資料提供給系統，並將其儲存在檔案系統上或插入資料庫中。 ASP.NET 2.0 包含 FileUpload 控制項，可讓您輕鬆地提供此類介面，如同拖放。 不過，如[上傳](uploading-files-vb.md)檔案教學課程中所述，FileUpload 控制項只適用于相對較小的檔案上傳，最好不要超過 mb。 我們也探討了如何將上傳的資料與基礎資料模型產生關聯，以及如何編輯和刪除現有記錄中的二進位資料。

我們的下一組教學課程會探討各種快取技術。 快取提供了一種方法來改善應用程式的整體效能，方法是從昂貴的作業中取得結果，並將其儲存在可更快速存取的位置。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](including-a-file-upload-option-when-adding-a-new-record-vb.md)
