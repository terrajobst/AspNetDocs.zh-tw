---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: 使用 DropDownList （C#）的主要/詳細資料篩選 |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將瞭解如何在 GridView 中顯示 DropDownList 控制項中的主要記錄，以及所選取清單專案的詳細資料。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 3ec549f9da7a2b3a021e77827f0039e6ae60b5c5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528816"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-c"></a>使用 DropDownList 進行主要/詳細資料篩選 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe)或[下載 PDF](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)

> 在本教學課程中，我們將瞭解如何在 GridView 中顯示 DropDownList 控制項中的主要記錄，以及所選取清單專案的詳細資料。

## <a name="introduction"></a>簡介

一般報表類型是*主要/詳細資料包表*，報表一開始會顯示一組「主要」記錄。 使用者接著可以向下切入到其中一個主要記錄，藉此查看該主記錄的「詳細資料」。 主要/詳細資料包表是視覺化一對多關聯性的理想選擇，例如顯示所有類別的報表，然後允許使用者選取特定類別，並顯示其相關聯的產品。 此外，主要/詳細資料包表非常適合用來顯示特別「寬」資料表的詳細資訊（具有大量資料行的資料表）。 例如，主要/詳細資料包表的「主要」層級可能只會顯示資料庫中產品的產品名稱和單價，而向下切入特定產品會顯示額外的產品欄位（類別、供應商、每個單位的數量等等）。

有許多方式可以執行主要/詳細資料包告。 在此和接下來的三個教學課程中，我們將探討各種主要/詳細資料包表。 在本教學課程中，我們將瞭解如何在 GridView 中顯示[DropDownList 控制項](https://msdn.microsoft.com/library/dtx91y0z.aspx)中的主要記錄，以及所選取清單專案的詳細資料。 特別是，本教學課程的主要/詳細資料包表會列出類別目錄和產品資訊。

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>步驟1：在 DropDownList 中顯示類別

我們的主要/詳細資料包表會列出 DropDownList 中的類別，並在 GridView 的頁面中進一步顯示選取的清單專案產品。 然後，前面的第一項工作是讓類別顯示在 DropDownList 中。 開啟 [`Filtering`] 資料夾中的 [`FilterByDropDownList.aspx`] 頁面，將 DropDownList 從 [工具箱] 拖曳至頁面的設計工具上，並將其 [`ID`] 屬性設定為 [`Categories`]。 接下來，按一下 DropDownList 的智慧標籤中的 [選擇資料來源] 連結。 這會顯示 [資料來源設定向導]。

[![指定 DropDownList 的資料來源](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)

**圖 1**：指定 DropDownList 的資料來源（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png)）

選擇新增名為 `CategoriesDataSource` 的新 ObjectDataSource，以叫用 `CategoriesBLL` 類別的 `GetCategories()` 方法。

[![新增名為 CategoriesDataSource 的新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)

**圖 2**：新增名為 `CategoriesDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png)）

[![選擇使用 CategoriesBLL 類別](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)

**圖 3**：選擇使用 [`CategoriesBLL`] 類別（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png)）

[![將 ObjectDataSource 設定為使用 GetCategories （）方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)

**圖 4**：設定 ObjectDataSource 以使用 `GetCategories()` 方法（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png)）

設定 ObjectDataSource 之後，我們仍然需要指定應該在 DropDownList 中顯示哪一個資料來源欄位，以及哪一個應該與清單專案的值相關聯。 將 [`CategoryName`] 欄位做為顯示，並 `CategoryID` 為每個清單專案的值。

[![讓 DropDownList 顯示 [類別名稱] 欄位，並使用 [類別名稱] 做為值](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)

**圖 5**：讓 DropDownList 顯示 `CategoryName` 欄位，並使用 `CategoryID` 作為值（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png)）

此時，我們有一個 DropDownList 控制項，其中填入了 `Categories` 資料表中的記錄（全部在大約六秒內完成）。 [圖 6] 顯示透過瀏覽器觀看的進度。

[![下拉式清單會列出目前的類別](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)

**圖 6**：下拉式清單會列出目前的類別（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png)）

## <a name="step-2-adding-the-products-gridview"></a>步驟2：新增產品 GridView

主要/詳細資料包告中的最後一個步驟，是列出與所選類別相關聯的產品。 若要完成此動作，請在頁面中新增 GridView，並建立名為 `productsDataSource`的新 ObjectDataSource。 讓 `productsDataSource` 控制項會從 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法挑選其資料。

[![選取 GetProductsByCategoryID （[類別]）方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)

**圖 7**：選取 [`GetProductsByCategoryID(categoryID)`] 方法（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png)）

選擇這個方法之後，ObjectDataSource wizard 會提示我們輸入方法之 *`categoryID`* 參數的值。 若要使用所選取 `categories` DropDownList 專案的值，請將參數來源設定為 Control，並將 ControlID 設為 `Categories`。

[![將 [類別目錄] 參數設定為 [分類] DropDownList 的值](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)

**圖 8**：將 *`categoryID`* 參數設定為 `Categories` DropDownList 的值（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png)）

請花點時間在瀏覽器中查看進度。 第一次流覽頁面時，會顯示屬於所選類別（飲料）的產品（如 [圖 9] 所示），但是變更 DropDownList 並不會更新資料。 這是因為必須進行回傳，GridView 才會更新。 若要完成這項工作，我們有兩個選項（兩者都不需要撰寫任何程式碼）：

- **將類別 DropDownList 的**[AutoPostBack 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)設定**為 True。** （您可以藉由核取 DropDownList 的智慧標籤中的 [啟用 AutoPostBack] 選項來完成這項操作。）每當使用者變更 DropDownList 的選取專案時，這會觸發回傳。 因此，當使用者從 DropDownList 中選取新的類別時，回傳將會控制發生，而 GridView 會更新為新選取之類別目錄的產品。 （這是我在本教學課程中使用的方法）。
- **在 DropDownList 旁新增按鈕 Web 控制項。** 將其 `Text` 屬性設定為 [重新整理] 或類似的內容。 使用此方法時，使用者必須選取新的類別，然後按一下按鈕。 按一下此按鈕會導致回傳並更新 GridView，以列出所選類別目錄的產品。

[圖 9] 和 [10] 說明主要/詳細報告的實際運作方式。

[![第一次造訪網頁時，會顯示飲料產品](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)

**圖 9**：第一次流覽頁面時，會顯示飲料產品（[按一下以觀看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png)）

[![選取新產品（產生）會自動導致回傳，並更新 GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)

**圖 10**：選取新的產品（產生）會自動導致回傳，並更新 GridView （[按一下以觀看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png)）

## <a name="adding-a----choose-a-category----list-item"></a>新增「--選擇類別--」清單專案

第一次造訪 [`FilterByDropDownList.aspx`] 頁面時，預設會選取 [類別] DropDownList 的 [第一個清單專案（飲料）]，其中顯示 GridView 中的飲料產品。 我們可能會想要改為選取 [--選擇類別--] 這類的 DropDownList 專案，而不是顯示第一個類別的產品。

若要將新的清單專案加入至 DropDownList，請移至 屬性視窗，然後按一下 `Items` 屬性中的省略號。 加入具有 `Text` "--選擇類別目錄--" 和 `Value` `-1`的新清單專案。

[![新增--選擇類別目錄--清單專案](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)

**圖 11**：新增--選擇類別目錄--清單專案（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png)）

或者，您也可以將下列標記新增至 DropDownList，以新增清單專案：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

此外，我們需要將 DropDownList 控制項的 `AppendDataBoundItems` 設定為 True，因為當類別目錄從 ObjectDataSource 系結至 DropDownList 時，如果 `AppendDataBoundItems` 不是 True，就會覆寫任何手動加入的清單專案。

![將 AppendDataBoundItems 屬性設定為 True](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

**圖 12**：將 `AppendDataBoundItems` 屬性設定為 True

這些變更之後，第一次造訪頁面時，會選取 [--選擇類別--] 選項，而且不會顯示任何產品。

[初始頁面上的 ![[載入不顯示任何產品]](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)

**圖 13**：在初始頁面上載入沒有顯示任何產品（[按一下以觀看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png)）

當選取 [--選擇類別--] 清單專案時，沒有顯示任何產品的原因是因為它的值是 `-1`，而且資料庫中沒有任何具有 `CategoryID` `-1`的產品。 如果這是您想要的行為，您就大功告成了！ 不過，如果您想要在選取 [--選擇類別--] 清單專案時顯示*所有*類別，請回到 `ProductsBLL` 類別並自訂 `GetProductsByCategoryID(categoryID)` 方法，以便在傳入的 *`categoryID`* 參數小於零時，叫用 `GetProducts()` 方法：

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

此處所使用的技術與我們用來在[宣告式參數](../basic-reporting/declarative-parameters-cs.md)教學課程中顯示所有供應商的方法類似，雖然在此範例中，我們會使用 `-1` 的值，表示應該抓取所有記錄，而不是 `null`。 這是因為 `GetProductsByCategoryID(categoryID)` 方法的 *`categoryID`* 參數預期傳入的整數值，而在宣告式參數教學課程中，我們傳入的是字串輸入參數。

[圖 14] 顯示已選取 [--選擇類別--] 選項時 `FilterByDropDownList.aspx` 的螢幕擷取畫面。 在這裡，預設會顯示所有產品，而使用者可以選擇特定分類來縮小顯示範圍。

[![現在預設會列出所有產品](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)

**圖 14**：預設會列出所有產品（[按一下以觀看完整大小的影像](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png)）

## <a name="summary"></a>總結

當顯示階層式相關資料時，通常會使用主要/詳細報告來呈現資料，而使用者可以從階層的頂端開始流覽資料，並向下切入詳細資料。 在本教學課程中，我們已檢查建立一個簡單的主版/詳細資料包告，其中顯示所選類別的產品。 這是針對分類清單，以及屬於所選類別之產品的 GridView 而完成。

在[下一個教學](master-detail-filtering-with-two-dropdownlists-cs.md)課程中，我們將使用兩個 dropdownlist 進行，讓 DropDownList 介面更進一步。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [下一個](master-detail-filtering-with-two-dropdownlists-cs.md)
