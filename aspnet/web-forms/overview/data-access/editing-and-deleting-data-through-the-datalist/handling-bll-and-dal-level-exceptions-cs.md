---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
title: 處理 BLL 和 DAL 層級的例外狀況C#（） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將瞭解如何 tactfully 處理在可編輯的 DataList 更新工作流程期間引發的例外狀況。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: f8fd58e2-f932-4f08-ab3d-fbf8ff3295d2
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 35ff60be6ed67ea8d1bf226ae70f590100597757
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634176"
---
# <a name="handling-bll--and-dal-level-exceptions-c"></a>處理 BLL 和 DAL 層級的例外狀況 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_CS.exe)或[下載 PDF](handling-bll-and-dal-level-exceptions-cs/_static/datatutorial38cs1.pdf)

> 在本教學課程中，我們將瞭解如何 tactfully 處理在可編輯的 DataList 更新工作流程期間引發的例外狀況。

## <a name="introduction"></a>簡介

在 DataList 教學課程中[編輯和刪除資料的總覽](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)中，我們建立了一個 DataList，提供簡單的編輯和刪除功能。 雖然功能完整，但使用者並不容易使用，因為在編輯或刪除程式期間發生的任何錯誤都會導致未處理的例外狀況。 例如，省略產品的名稱，或在編輯產品時，輸入非常實惠的價格值！會擲回例外狀況。 由於此例外狀況不會在程式碼中攔截，因此會反升至 ASP.NET 執行時間，然後在網頁中顯示例外狀況的詳細資料。

如同在[ASP.NET 網頁中處理 BLL 和 DAL 層級的例外](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)狀況教學課程中所見，如果從商務邏輯或資料存取層的深度引發例外狀況，例外狀況詳細資料會傳回給 ObjectDataSource，然後再傳給 GridView。 我們已瞭解如何藉由建立 ObjectDataSource 或 GridView 的 `Updated` 或 `RowUpdated` 事件處理常式、檢查是否有例外狀況，然後指出是否已處理例外狀況，來適當地處理這些例外狀況。

不過，我們的 DataList 教學課程不會使用 ObjectDataSource 來更新和刪除資料。 相反地，我們會直接針對 BLL 進行操作。 為了偵測源自 BLL 或 DAL 的例外狀況，我們需要在 ASP.NET 網頁的程式碼後置中，執行例外狀況處理常式代碼。 在本教學課程中，我們將瞭解如何在可編輯的 DataList s 更新工作流程期間，更 tactfully 處理引發的例外狀況。

> [!NOTE]
> 在 DataList 教學課程中*編輯和刪除資料的總覽*中，我們討論過從 datalist 中編輯和刪除資料的不同技巧，其中包括使用 ObjectDataSource 進行更新和刪除的一些技巧。 如果您採用這些技術，您可以透過 ObjectDataSource `Updated` 或 `Deleted` 事件處理常式，處理來自 BLL 或 DAL 的例外狀況。

## <a name="step-1-creating-an-editable-datalist"></a>步驟1：建立可編輯的 DataList

在我們擔心如何處理更新工作流程期間所發生的例外狀況之前，先建立一個可編輯的 DataList。 開啟 [`EditDeleteDataList`] 資料夾中的 [`ErrorHandling.aspx`] 頁面，將 DataList 新增至設計工具，將其 `ID` 屬性設定為 [`Products`]，然後新增名為 `ProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以使用 `ProductsBLL` 類別 s `GetProducts()` 方法來選取記錄;將 [插入]、[更新] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![使用 GetProducts （）方法傳回產品資訊](handling-bll-and-dal-level-exceptions-cs/_static/image2.png)](handling-bll-and-dal-level-exceptions-cs/_static/image1.png)

**圖 1**：使用 `GetProducts()` 方法傳回產品資訊（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-cs/_static/image3.png)）

完成 ObjectDataSource wizard 之後，Visual Studio 會自動建立 DataList 的 `ItemTemplate`。 將此取代為顯示每個產品名稱和價格的 `ItemTemplate`，並包含 [編輯] 按鈕。 接下來，建立具有 [名稱] 和 [價格] 和 [更新] 和 [取消] 按鈕之 TextBox Web 控制項的 `EditItemTemplate`。 最後，將 DataList s `RepeatColumns` 屬性設為2。

這些變更之後，您的頁面宣告式標記看起來應該如下所示。 請仔細檢查 [編輯]、[取消] 和 [更新] 按鈕，將其 `CommandName` 屬性分別設定為 [編輯]、[取消] 和 [更新]。

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample1.aspx)]

> [!NOTE]
> 在本教學課程中，必須啟用 DataList s 檢視狀態。

請花點時間透過瀏覽器查看進度（請參閱 [圖 2]）。

[![每個產品都包含 [編輯] 按鈕](handling-bll-and-dal-level-exceptions-cs/_static/image5.png)](handling-bll-and-dal-level-exceptions-cs/_static/image4.png)

**圖 2**：每個產品都包含 [編輯] 按鈕（[按一下以觀看完整大小的影像](handling-bll-and-dal-level-exceptions-cs/_static/image6.png)）

目前，[編輯] 按鈕只會導致回傳，而不會讓產品變成可編輯狀態。 若要啟用編輯，我們必須建立 DataList s `EditCommand`、`CancelCommand`和 `UpdateCommand` 事件的事件處理常式。 `EditCommand` 和 `CancelCommand` 事件只會更新 DataList s `EditItemIndex` 屬性，並將資料重新系結至 DataList：

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample2.cs)]

`UpdateCommand` 事件處理常式比較複雜。 它必須從 `DataKeys` 集合中讀取已編輯的產品 `ProductID`，連同 `EditItemTemplate`中文字方塊的產品名稱和價格，然後在將 DataList 傳回其預先編輯狀態之前，先呼叫 `ProductsBLL` 類別的 `UpdateProduct` 方法。

現在，讓我們在 DataList 教學課程中*編輯和刪除資料的總覽*中，使用 `UpdateCommand` 事件處理常式中完全相同的程式碼。 我們會新增程式碼，以正常處理步驟2中的例外狀況。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample3.cs)]

在臉部不正確輸入中，其格式可能不正確、不合法的單位價格值（例如-$5.00），或省略產品的名稱時，將會引發例外狀況。 由於 `UpdateCommand` 事件處理常式在此時不會包含任何例外狀況處理常式代碼，因此例外狀況會反升至 ASP.NET 執行時間，並在其中向終端使用者顯示（請參閱 [圖 3]）。

![當未處理的例外狀況發生時，終端使用者會看到錯誤頁面](handling-bll-and-dal-level-exceptions-cs/_static/image7.png)

**圖 3**：當發生未處理的例外狀況時，終端使用者會看到錯誤頁面

## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>步驟2：正常處理 UpdateCommand 事件處理常式中的例外狀況

在更新工作流程期間，例外狀況可能會發生在 `UpdateCommand` 事件處理常式、BLL 或 DAL 中。 例如，如果使用者輸入的價格過高，`UpdateCommand` 事件處理常式中的 `Decimal.Parse` 語句將會擲回 `FormatException` 例外狀況。 如果使用者省略產品的名稱，或如果價格具有負值，則 DAL 會引發例外狀況。

發生例外狀況時，我們想要在頁面本身內顯示資訊訊息。 將 [標籤] Web 控制項新增至頁面，其 `ID` 設定為 [`ExceptionDetails`]。 藉由將標籤的 [`CssClass`] 屬性指派給在 `Styles.css` 檔中定義的 `Warning` CSS 類別，設定要以紅色、超大、粗體和斜體字型顯示的文字。

發生錯誤時，我們只希望標籤顯示一次。 也就是說，在後續回傳時，標籤 s 警告訊息應該會消失。 這可以藉由清除標籤 `Text` 屬性來完成，或將其 `Visible` 屬性設定為 `Page_Load` 事件處理常式中 `False` （如同我們在 ASP.NET 網頁教學課程中[處理 BLL 和 DAL 層級的例外](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)狀況），或停用標籤 s 檢視狀態支援。 讓 s 使用第二個選項。

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample4.aspx)]

當引發例外狀況時，我們會將例外狀況的詳細資料指派給 `ExceptionDetails` Label 控制項 s `Text` 屬性。 因為已停用其 view 狀態，所以在後續回傳時，`Text` 屬性 s 程式設計變更將會遺失，並還原為預設文字（空字串），因此會隱藏警告訊息。

若要判斷何時引發錯誤以便在頁面上顯示有用的訊息，我們必須將 `Try ... Catch` 區塊加入 `UpdateCommand` 事件處理常式。 `Try` 部分包含可能會導致例外狀況的程式碼，而 `Catch` 區塊包含在發生例外狀況時執行的程式碼。 如需有關 `Try ... Catch` 組塊的詳細資訊，請參閱 .NET Framework 檔中的[例外狀況處理基本](https://msdn.microsoft.com/library/2w8f0bss.aspx)概念一節。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample5.cs)]

當 `Try` 區塊內的程式碼擲回任何類型的例外狀況時，`Catch` 區塊程式碼就會開始執行。 `DbException`、`NoNullAllowedException`、`ArgumentException`等等所擲回的例外狀況類型，取決於第一次促使錯誤的確切狀況。 如果資料庫層級發生問題，則會擲回 `DbException`。 如果為 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`或 `ReorderLevel` 欄位輸入了不合法的值，將會擲回 `ArgumentException`，因為我們已新增程式碼來驗證 `ProductsDataTable` 類別中的域值（請參閱[建立商務邏輯層](../introduction/creating-a-business-logic-layer-cs.md)教學課程）。

我們可以藉由在攔截到的例外狀況類型上建立郵件內文，為使用者提供更實用的說明。 在 ASP.NET 網頁教學課程中，用來[處理 BLL 和 DAL 層級例外](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)狀況的下列程式碼，會提供此層級的詳細資料：

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample6.cs)]

若要完成本教學課程，只需要從 `Catch` 區塊呼叫 `DisplayExceptionDetails` 方法，傳入攔截到的 `Exception` 實例（`ex`）。

當 `Try ... Catch` 組塊就緒時，使用者會看到更具資訊性的錯誤訊息，如 [圖 4] 和 [5] 所示。 請注意，在發生例外狀況的情況下，DataList 會維持在編輯模式。 這是因為一旦發生例外狀況，就會立即將控制流程重新導向至 `Catch` 區塊，略過將 DataList 傳回其預先編輯狀態的程式碼。

[![如果使用者省略必要欄位，就會顯示錯誤訊息](handling-bll-and-dal-level-exceptions-cs/_static/image9.png)](handling-bll-and-dal-level-exceptions-cs/_static/image8.png)

**圖 4**：如果使用者省略必要欄位（[按一下以觀看完整大小的影像](handling-bll-and-dal-level-exceptions-cs/_static/image10.png)），就會顯示錯誤訊息

[輸入負值時，會顯示 ![錯誤訊息](handling-bll-and-dal-level-exceptions-cs/_static/image12.png)](handling-bll-and-dal-level-exceptions-cs/_static/image11.png)

**圖 5**：輸入負值時，會顯示錯誤訊息（[按一下以查看完整大小的影像](handling-bll-and-dal-level-exceptions-cs/_static/image13.png)）

## <a name="summary"></a>總結

GridView 和 ObjectDataSource 提供了後續層級的事件處理常式，其中包含在更新和刪除工作流程期間引發之任何例外狀況的相關資訊，以及可設定來指出是否已有例外狀況的屬性。dps. 不過，這些功能在處理 DataList 並直接使用 BLL 時無法使用。 相反地，我們會負責執行例外狀況處理。

在本教學課程中，我們已瞭解如何藉由將 `Try ... Catch` 區塊加入 `UpdateCommand` 事件處理常式中，將例外狀況處理新增至可編輯的 DataList s 更新工作流程。 如果在更新工作流程期間引發例外狀況，則會執行 `Catch` 區塊 s 程式碼，並在 `ExceptionDetails` 標籤中顯示有用的資訊。

此時，DataList 不會避免發生例外狀況的一開始。 雖然我們知道負的價格會導致例外狀況，但我們尚未新增任何功能，以主動防止使用者輸入這類不正確輸入。 在下一個教學課程中，我們將瞭解如何在 `EditItemTemplate`中新增驗證控制項，以協助減少無效使用者輸入所造成的例外狀況。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [例外狀況的設計方針](https://msdn.microsoft.com/library/ms298399.aspx)
- [錯誤記錄模組和處理常式（ELMAH）](http://workspaces.gotdotnet.com/elmah) （用來記錄錯誤的開放原始碼程式庫）
- [適用于 .NET Framework 2.0 的企業程式庫](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en)（包括例外狀況管理應用程式區塊）

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Ken Pespisa。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](performing-batch-updates-cs.md)
> [下一頁](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
