---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
title: 使用 DropDownList （C#）的主要/詳細資料篩選 |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們會瞭解如何使用 Dropdownlist 進行在單一網頁中顯示主要/詳細資料包表，以顯示「主要」記錄和 DataList 至 displ 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 07fa47ae-e491-4a2f-b265-d342b9ddef46
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 8289f46fd6d0143802269d5c6196a4c40db9378c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78590262"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-c"></a>使用 DropDownList 進行主要/詳細資料篩選 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_CS.exe)或[下載 PDF](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/datatutorial33cs1.pdf)

> 在本教學課程中，我們會瞭解如何在單一網頁中顯示主要/詳細資料包表，方法是使用 Dropdownlist 進行來顯示「主要」記錄和 DataList 來顯示「詳細資料」。

## <a name="introduction"></a>簡介

主要/詳細資料包表，我們在先前的[主要/詳細資料篩選](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)中使用 GridView 以 DropDownList 教學課程來建立，一開始會顯示一組「主要」記錄。 使用者接著可以向下切入到其中一個主要記錄，藉此查看該主記錄的「詳細資料」。 主要/詳細資料包表是視覺化一對多關聯性，以及顯示特別「寬」資料表（具有大量資料行）的詳細資訊的理想選擇。 我們已探討如何在先前的教學課程中使用 GridView 和 DetailsView 控制項來執行主要/詳細資料包表。 在本教學課程和接下來的兩個中，我們將重新檢查這些概念，但專注于改為使用 DataList 和重複項控制項。

在本教學課程中，我們將探討如何使用 DropDownList 來包含「主要」記錄，以及 DataList 中所顯示的「詳細資料」記錄。

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>步驟1：加入主版/詳細教學課程網頁

開始進行本教學課程之前，讓我們先花點時間新增本教學課程所需的資料夾和 ASP.NET 網頁，以及使用 DataList 和重複項控制項來處理主版/詳細報告的下兩頁。 首先，在名為 `DataListRepeaterFiltering`的專案中建立新的資料夾。 接下來，將下列五個 ASP.NET 網頁新增到此資料夾，並將它們全部設定為使用主版頁面 `Site.master`：

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`

![建立 DataListRepeaterFiltering 資料夾並新增教學課程 ASP.NET 網頁](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image1.png)

**圖 1**：建立 `DataListRepeaterFiltering` 資料夾並新增教學課程 ASP.NET 網頁

接下來，開啟 [`Default.aspx`] 頁面，並將 [`SectionLevelTutorialListing.ascx` 使用者] 控制項從 [`UserControls`] 資料夾拖曳到設計介面上。 我們在[主版頁面和網站導覽](../introduction/master-pages-and-site-navigation-cs.md)教學課程中建立的這個使用者控制項，會列舉網站地圖，並從項目符號清單中的目前區段顯示教學課程。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image2.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image4.png)）

為了讓項目符號清單顯示我們將建立的主要/詳細教學課程，我們需要將它們新增至網站地圖。 開啟 `Web.sitemap` 檔案，並在「使用 DataList 和中繼器來顯示資料」網站地圖節點標記後面新增下列標記：

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample1.xml)]

![更新網站地圖以包含新的 ASP.NET 網頁](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image5.png)

**圖 3**：更新網站地圖以包含新的 ASP.NET 網頁

## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>步驟2：在 DropDownList 中顯示類別

我們的主要/詳細資料包表會列出 DropDownList 中的類別，並在 DataList 的頁面中進一步顯示選取的清單專案產品。 然後，前面的第一項工作是讓類別顯示在 DropDownList 中。 一開始先開啟 [`DataListRepeaterFiltering`] 資料夾中的 [`FilterByDropDownList.aspx`] 頁面，然後將 DropDownList 從 [工具箱] 拖曳至頁面的設計工具。 接下來，將 DropDownList 的 `ID` 屬性設定為 `Categories`。 按一下 DropDownList 的智慧標籤中的 [選擇資料來源] 連結，然後建立名為 `CategoriesDataSource`的新 ObjectDataSource。

[![新增名為 CategoriesDataSource 的新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image6.png)

**圖 4**：新增名為 `CategoriesDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image8.png)）

設定新的 ObjectDataSource，使其叫用 `CategoriesBLL` 類別的 `GetCategories()` 方法。 設定 ObjectDataSource 之後，我們仍然需要指定應該在 DropDownList 中顯示哪一個資料來源欄位，以及哪一個應該與每個清單專案的值相關聯。 將 [`CategoryName`] 欄位做為顯示，並 `CategoryID` 為每個清單專案的值。

[![讓 DropDownList 顯示 [類別名稱] 欄位，並使用 [類別名稱] 做為值](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image9.png)

**圖 5**：讓 DropDownList 顯示 `CategoryName` 欄位，並使用 `CategoryID` 作為值（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image11.png)）

此時，我們有一個 DropDownList 控制項，其中填入了 `Categories` 資料表中的記錄（全部在大約六秒內完成）。 [圖 6] 顯示透過瀏覽器觀看的進度。

[![下拉式清單會列出目前的類別](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image12.png)

**圖 6**：下拉式清單會列出目前的類別（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image14.png)）

## <a name="step-2-adding-the-products-datalist"></a>步驟2：加入產品 DataList

主要/詳細資料包告中的最後一個步驟，是列出與所選類別相關聯的產品。 若要完成此動作，請在頁面中新增 DataList，並建立名為 `ProductsByCategoryDataSource`的新 ObjectDataSource。 讓 `ProductsByCategoryDataSource` 控制項從 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法抓取其資料。 由於此主要/詳細報告是唯讀的，因此請在 [插入]、[更新] 和 [刪除] 索引標籤中選擇 [（無）] 選項。

[![選取 GetProductsByCategoryID （[類別]）方法](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image15.png)

**圖 7**：選取 [`GetProductsByCategoryID(categoryID)`] 方法（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image17.png)）

按 [下一步] 之後，ObjectDataSource wizard 會提示我們輸入 `GetProductsByCategoryID(categoryID)` 方法的 *`categoryID`* 參數值的來源。 若要使用所選取 `categories` DropDownList 專案的值，請將參數來源設定為 Control，並將 ControlID 設為 `Categories`。

[![將 [類別目錄] 參數設定為 [分類] DropDownList 的值](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image18.png)

**圖 8**：將 *`categoryID`* 參數設定為 `Categories` DropDownList 的值（[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image20.png)）

完成 [設定資料來源] 時，Visual Studio 會自動產生 DataList 的 `ItemTemplate`，其中顯示每個資料欄位的名稱和值。 讓我們增強 DataList，改為使用只顯示產品名稱、類別、供應商、每單位數量和價格的 `ItemTemplate`，以及在每個專案之間插入 `<hr>` 元素的 `SeparatorTemplate`。 我將使用 [[使用 DataList 和重複項控制項顯示資料](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs.md)] 教學課程中的範例 `ItemTemplate`，但您可以隨意使用您找到最具視覺效果的任何範本標記。

進行這些變更之後，您的 DataList 和其 ObjectDataSource 的標記看起來應該如下所示：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample2.aspx)]

請花點時間在瀏覽器中查看進度。 第一次流覽頁面時，會顯示屬於所選類別（飲料）的產品（如 [圖 9] 所示），但是變更 DropDownList 並不會更新資料。 這是因為必須進行回傳，DataList 才會更新。 若要完成這項操作，我們可以將 DropDownList 的 `AutoPostBack` 屬性設定為 `true`，或將按鈕 Web 控制項加入至頁面。 在本教學課程中，我選擇將 DropDownList 的 `AutoPostBack` 屬性設定為 [`true`]。

[圖 9] 和 [10] 說明主要/詳細報告的實際運作方式。

[![第一次造訪網頁時，會顯示飲料產品](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image21.png)

**圖 9**：第一次流覽頁面時，會顯示飲料產品（[按一下以觀看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image23.png)）

[![選取新產品（產生）會自動導致回傳，更新 DataList](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image24.png)

**圖 10**：選取新的產品（產生）會自動導致回傳，更新 DataList （[按一下以查看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image26.png)）

## <a name="adding-a----choose-a-category----list-item"></a>新增「--選擇類別--」清單專案

第一次造訪 [`FilterByDropDownList.aspx`] 頁面時，預設會選取 [類別] DropDownList 的 [第一個清單專案（飲料）]，其中顯示 DataList 中的飲料產品。 在具有 DropDownList 教學課程的*主要/詳細資料篩選*中，我們已將「--選擇類別--」選項新增至預設選取的 DropDownList，並在選取時顯示資料庫中的*所有*產品。 當您在 GridView 中列出產品時，這種方法是可管理的，因為每個產品資料列都佔用少量的畫面空間。 不過，在 DataList 中，每個產品的資訊都會耗用更大的螢幕區塊。 讓我們繼續新增 [--選擇類別] 選項，並依預設選取它，但不要讓它在選取時顯示所有產品，而是設定它，讓它不會顯示任何產品。

若要將新的清單專案加入至 DropDownList，請移至 屬性視窗，然後按一下 `Items` 屬性中的省略號。 加入具有 `Text` "--選擇類別目錄--" 和 `Value` `0`的新清單專案。

![新增](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image27.png)

**圖 11**：新增「--選擇類別--」清單專案

或者，您也可以將下列標記新增至 DropDownList，以新增清單專案：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample3.aspx)]

此外，我們需要將 DropDownList 控制項的 `AppendDataBoundItems` 設定為 [`true`]，因為如果設定為 [`false`] （預設值），則當分類從 ObjectDataSource 系結至 DropDownList 時，它們會覆寫任何手動加入的清單專案。

![將 AppendDataBoundItems 屬性設定為 True](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image28.png)

**圖 12**：將 `AppendDataBoundItems` 屬性設定為 True

我們選擇 [--選擇類別--] 清單專案的值 `0` 的原因是系統中沒有任何分類值為 [`0`]，因此選取 [--選擇類別--] 清單專案時，不會傳回任何產品記錄。 若要確認這一點，請花點時間透過瀏覽器造訪頁面。 如 [圖 13] 所示，一開始在流覽頁面時，會選取 [--選擇類別--] 清單專案，而且不會顯示任何產品。

[![](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image29.png)

**圖 13**：選取 [--選擇類別--] 清單專案時，不會顯示任何產品（[按一下以觀看完整大小的影像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image31.png)）

如果您想要在選取 [--選擇類別--] 選項時顯示*所有*產品，請改用 `-1` 的值。 精明讀取器會回想一下*主要/詳細資料篩選和 DropDownList*教學課程，我們更新了 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法，如此一來，如果傳入 `-1` 的 *`categoryID`* 值，就會傳回所有產品記錄。

## <a name="summary"></a>總結

當顯示階層式相關資料時，通常會使用主要/詳細報告來呈現資料，而使用者可以從階層的頂端開始流覽資料，並向下切入詳細資料。 在本教學課程中，我們已檢查建立一個簡單的主版/詳細資料包告，其中顯示所選類別的產品。 這是使用類別清單的 DropDownList，以及屬於所選類別之產品的 DataList 來完成。

在下一個教學課程中，我們將探討如何在兩個頁面上分隔主要和詳細資料記錄。 在第一頁中，將會顯示「主要」記錄的清單，其中會有連結可供您查看詳細資料。 按一下連結會將使用者 whisk 到第二頁，這會顯示所選主要記錄的詳細資料。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Randy Schmidt。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一個](master-detail-filtering-acess-two-pages-datalist-cs.md)
