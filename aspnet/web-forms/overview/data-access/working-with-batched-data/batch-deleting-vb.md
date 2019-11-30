---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
title: 批次刪除（VB） |Microsoft Docs
author: rick-anderson
description: 瞭解如何在單一作業中刪除多個資料庫記錄。 在使用者介面層中，我們是以先前 tut 中建立的增強 GridView 為基礎 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4fb72f75-32ab-4bf7-a764-be20367be726
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: 0974a16764eee2ef03cf36b4b15f9ef41f99982b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621676"
---
# <a name="batch-deleting-vb"></a>批次刪除 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_VB.zip)或[下載 PDF](batch-deleting-vb/_static/datatutorial65vb1.pdf)

> 瞭解如何在單一作業中刪除多個資料庫記錄。 在使用者介面層中，我們是以稍早教學課程中建立的增強 GridView 為基礎。 在資料存取層中，我們會將多個刪除作業包裝在交易中，以確保所有刪除動作都會成功，或所有刪除動作都會復原。

## <a name="introduction"></a>簡介

[先前的教學](batch-updating-vb.md)課程探索到如何使用可完全編輯的 GridView 來建立批次編輯介面。 在使用者經常同時編輯許多記錄的情況下，批次編輯介面需要的回傳和鍵盤到滑鼠內容切換較少，因此可提高使用者的效率。 這項技術同樣適用于使用者經常在一處刪除許多記錄的頁面。

曾經使用線上電子郵件客戶程式的任何人，都已經熟悉其中一個最常見的批次刪除介面：格線中的每個資料列都有對應的 [刪除所有已檢查的專案] 按鈕（請參閱 [圖 1]）。 本教學課程很簡單，因為我們已在先前的教學課程中，完成建立 web 型介面和方法將一系列記錄刪除為單一不可部分完成的作業。 在 [[新增 GridView 的核取方塊](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)] 資料行教學課程中，我們建立了一個 GridView，其中包含一個核取方塊的[資料行](wrapping-database-modifications-within-a-transaction-vb.md)，而在交易教學課程中，我們已在 BLL 中建立一個方法，這會使用交易來刪除 `ProductID` 值的 `List<T>`。 在本教學課程中，我們將建立併合並先前的體驗，以建立運作中的批次刪除範例。

[![每個資料列都包含一個核取方塊](batch-deleting-vb/_static/image1.gif)](batch-deleting-vb/_static/image1.png)

**圖 1**：每個資料列都包含一個核取方塊（[按一下以查看完整大小的影像](batch-deleting-vb/_static/image2.png)）

## <a name="step-1-creating-the-batch-deleting-interface"></a>步驟1：建立批次刪除介面

由於我們已在[新增 GridView 的核取方塊資料行](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)教學課程中建立批次刪除介面，因此我們可以直接將它複製到 `BatchDelete.aspx`，而不是從頭建立。 一開始請開啟 [`BatchData`] 資料夾中的 [`BatchDelete.aspx`] 頁面，並在 [`EnhancedGridView`] 資料夾的 [`CheckBoxField.aspx`] 頁面。 從 [`CheckBoxField.aspx`] 頁面，移至 [來源] 視圖，並複製 `<asp:Content>` 標記之間的標記，如 [圖 2] 所示。

[![將 CheckBoxField 的宣告式標記複製到剪貼簿](batch-deleting-vb/_static/image2.gif)](batch-deleting-vb/_static/image3.png)

**圖 2**：將 `CheckBoxField.aspx` 的宣告式標記複製到剪貼簿（[按一下以觀看完整大小的影像](batch-deleting-vb/_static/image4.png)）

接下來，移至 `BatchDelete.aspx` 中的來源視圖，並在 `<asp:Content>` 標記中貼上剪貼簿的內容。 此外，也會從 `CheckBoxField.aspx.vb` 的程式碼後置類別中，將程式碼複製並貼到 `BatchDelete.aspx.vb` 中的程式碼後置類別中（`DeleteSelectedProducts` 按鈕 s `Click` 事件處理常式、`ToggleCheckState` 方法，以及 `Click` 和 `CheckAll` 按鈕的 `UncheckAll` 事件處理常式）。 複製此內容之後，`BatchDelete.aspx` page s 程式碼後置類別應該包含下列程式碼：

[!code-vb[Main](batch-deleting-vb/samples/sample1.vb)]

複製宣告式標記和原始程式碼之後，請花點時間透過瀏覽器查看 `BatchDelete.aspx`。 您應該會看到 GridView 列出 GridView 中的前10個產品，其中每個資料列都會列出產品的名稱、類別和價格，以及一個核取方塊。 應該會有三個按鈕： [全選]、[取消選取全部] 和 [刪除選取的產品]。 按一下 [全選] 按鈕會選取所有核取方塊，而 [取消選取全部] 則會清除所有核取方塊。 按一下 [刪除選取的產品] 會顯示一則訊息，其中列出所選產品的 `ProductID` 值，但不會實際刪除產品。

[從 CheckBoxField ![介面已移至 BatchDeleting](batch-deleting-vb/_static/image3.gif)](batch-deleting-vb/_static/image5.png)

**圖 3**： `CheckBoxField.aspx` 的介面已移至 `BatchDeleting.aspx` （[按一下以觀看完整大小的影像](batch-deleting-vb/_static/image6.png)）

## <a name="step-2-deleting-the-checked-products-using-transactions"></a>步驟2：使用交易刪除核取的產品

成功將批次刪除介面複製到 `BatchDeleting.aspx`之後，剩下的工作就是更新程式碼，讓 [刪除選取的產品] 按鈕在 `ProductsBLL` 類別中使用 `DeleteProductsWithTransaction` 方法刪除已核取的產品。 這個方法在交易教學課程[中的包裝資料庫修改](wrapping-database-modifications-within-a-transaction-vb.md)中加入，會接受 `ProductID` 值的 `List(Of T)`，並刪除交易範圍內的每個對應 `ProductID`。

`DeleteSelectedProducts` 按鈕 s `Click` 事件處理常式目前使用下列 `For Each` 迴圈逐一查看每個 GridView 資料列：

[!code-vb[Main](batch-deleting-vb/samples/sample2.vb)]

針對每個資料列，會以程式設計方式參考 [`ProductSelector`] 核取方塊 Web 控制項。 如果已核取，則會從 `DataKeys` 集合抓取資料列 `ProductID`，而 `DeleteResults` 標籤 s `Text` 屬性會更新以包含訊息，指出已選取要刪除的資料列。

上述程式碼不會實際刪除任何記錄，因為呼叫 `ProductsBLL` 類別 `Delete` 方法會被標記為批註。這是要套用的刪除邏輯，程式碼會刪除產品，而不是在不可部分完成的作業中。 也就是說，如果序列中的前幾個刪除成功，但後面的一個失敗（可能是因為外鍵條件約束違規），則會擲回例外狀況，但已刪除的產品仍會被刪除。

為了確保不可部分完成性，我們必須改為使用 `ProductsBLL` 類別的 `DeleteProductsWithTransaction` 方法。 因為此方法會接受 `ProductID` 值的清單，所以我們需要先從方格中編譯此清單，然後將它當做參數傳遞。 我們會先建立 `Integer`型別 `List(Of T)` 的實例。 在 `For Each` 迴圈中，我們需要將選取的產品 `ProductID` 值新增至這個 `List(Of T)`。 在迴圈之後，這個 `List(Of T)` 必須傳遞至 `ProductsBLL` 類別 s `DeleteProductsWithTransaction` 方法。 使用下列程式碼更新 `DeleteSelectedProducts` 按鈕 s `Click` 事件處理常式：

[!code-vb[Main](batch-deleting-vb/samples/sample3.vb)]

更新後的程式碼會建立 `Integer` （`productIDsToDelete`）類型的 `List(Of T)`，並在其中填入要刪除的 `ProductID` 值。 在 `For Each` 迴圈之後，如果至少選取一個產品，則會呼叫 `ProductsBLL` 類別 s `DeleteProductsWithTransaction` 方法，並傳遞這份清單。 也會顯示 [`DeleteResults`] 標籤，並將資料重新系結至 GridView （如此一來，新刪除的記錄就不會再顯示為方格中的資料列）。

[圖 4] 顯示已選取數個數據列以供刪除之後的 GridView。 [圖 5] 顯示按一下 [刪除選取的產品] 按鈕之後的畫面。 請注意，在 [圖 5] 中，已刪除之記錄的 `ProductID` 值會顯示在 GridView 底下的標籤中，而那些資料列已不再位於 GridView 中。

[將刪除選取的產品 ![](batch-deleting-vb/_static/image4.gif)](batch-deleting-vb/_static/image7.png)

**圖 4**：將會刪除選取的產品（[按一下以觀看完整大小的影像](batch-deleting-vb/_static/image8.png)）

[![已刪除的產品 ProductID 值會列在 GridView 底下](batch-deleting-vb/_static/image5.gif)](batch-deleting-vb/_static/image9.png)

**圖 5**：已刪除的產品 `ProductID` 值會列在 GridView 底下（[按一下以觀看完整大小的影像](batch-deleting-vb/_static/image10.png)）

> [!NOTE]
> 若要測試 `DeleteProductsWithTransaction` 方法的不可部分完成性，請在 [`Order Details`] 資料表中手動新增產品的專案，然後嘗試刪除該產品（以及其他）。 當您嘗試刪除具有相關聯訂單的產品時，將會收到外鍵條件約束違規，但請注意其他選取的產品刪除如何復原。

## <a name="summary"></a>總結

建立批次刪除介面包括新增 GridView 與核取方塊的資料行，以及按鈕 Web 控制項，按一下時，會將所有選取的資料列刪除為單一不可部分完成的作業。 在本教學課程中，我們建立了這類介面，方法是 piecing 在兩個先前的教學課程中完成的工作，[新增 GridView 資料行的核取方塊](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)，並將[資料庫修改包裝在交易中](wrapping-database-modifications-within-a-transaction-vb.md)。 在第一個教學課程中，我們建立了一個 GridView，其中含有核取方塊的資料行，而在後者中，我們實作為 BLL 中的方法，當傳遞 `ProductID` 值的 `List(Of T)` 時，就會在交易的範圍內全部刪除。

在下一個教學課程中，我們將建立用來執行批次插入的介面。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](batch-updating-vb.md)
> [下一頁](batch-inserting-vb.md)
