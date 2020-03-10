---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
title: 使用兩個 Dropdownlist 進行的主要/詳細資料篩選（VB） |Microsoft Docs
author: rick-anderson
description: 本教學課程會展開主要/詳細資料關聯性來新增第三層，使用兩個 DropDownList 控制項來選取所需的父系和祖系 recor 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11ae4f64-01ba-4823-95f4-a2fe1f84f7d7
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
msc.type: authoredcontent
ms.openlocfilehash: 166d6a7664a326361dc2a3f115eddb988cd39d20
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528494"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-vb"></a>使用兩個 DropDownLis 進行主要/詳細資料篩選 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_8_VB.exe)或[下載 PDF](master-detail-filtering-with-two-dropdownlists-vb/_static/datatutorial08vb1.pdf)

> 本教學課程會展開主要/詳細資料關聯性，以使用兩個 DropDownList 控制項來選取所需的父系和祖系記錄，以新增第三層。

## <a name="introduction"></a>簡介

在[上一個教學](master-detail-filtering-with-a-dropdownlist-vb.md)課程中，我們探討了如何使用以類別填入的單一 DropDownList，以及顯示屬於所選類別之產品的 GridView，顯示簡單的主要/詳細資料包表。 此報表模式適用于顯示具有一對多關聯性的記錄，而且可以輕鬆擴充以用於包含多個一對多關聯性的案例。 例如，訂單輸入系統會有對應至客戶、訂單和訂單明細專案的資料表。 給定的客戶可能會有多個訂單，且每個訂單都包含多個專案。 這類資料可以向使用者呈現兩個 Dropdownlist 進行和 GridView。 第一個 DropDownList 會有資料庫中每個客戶的清單專案，其中第二個內容是所選客戶所放置的訂單。 GridView 會列出所選順序中的行專案。

雖然 Northwind 資料庫在其 `Customers`、`Orders`和 `Order Details` 資料表中包含標準的客戶/訂單/訂單詳細資訊，但這些資料表不會在架構中捕捉。 不過，我們仍然可以說明如何使用兩個相依的 Dropdownlist 進行。 第一個 DropDownList 會列出分類，以及屬於所選類別的第二個產品。 然後 DetailsView 會列出所選產品的詳細資料。

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>步驟1：建立和填入類別 DropDownList

我們的第一個目標是新增列出分類的 DropDownList。 先前的教學課程中已詳細檢查這些步驟，但在此會針對完整性進行摘要說明。

開啟 [`Filtering`] 資料夾中的 [`MasterDetailsDetails.aspx`] 頁面，將 DropDownList 新增至頁面，將其 [`ID`] 屬性設定為 [`Categories`]，然後按一下其智慧標籤中的 [設定資料來源] 連結。 在 [資料來源設定] 中，加入宣告新的資料來源。

[![為 DropDownList 加入新的資料來源](master-detail-filtering-with-two-dropdownlists-vb/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image1.png)

**圖 1**：為 DropDownList 加入新的資料來源（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image3.png)）

新的資料來源應該自然是 ObjectDataSource。 將這個新的 ObjectDataSource 命名為 `CategoriesDataSource` 並讓它叫用 `CategoriesBLL` 物件的 `GetCategories()` 方法。

[![選擇使用 CategoriesBLL 類別](master-detail-filtering-with-two-dropdownlists-vb/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image4.png)

**圖 2**：選擇使用 `CategoriesBLL` 類別（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image6.png)）

[![將 ObjectDataSource 設定為使用 GetCategories （）方法](master-detail-filtering-with-two-dropdownlists-vb/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image7.png)

**圖 3**：設定 ObjectDataSource 以使用 `GetCategories()` 方法（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image9.png)）

設定 ObjectDataSource 之後，我們仍然需要指定應該在 `Categories` DropDownList 中顯示哪個資料來源欄位，以及應該將哪一個設定為清單專案的值。 將 [`CategoryName`] 欄位設定為 [顯示]，並 `CategoryID` 為每個清單專案的值。

[![讓 DropDownList 顯示 [類別名稱] 欄位，並使用 [類別名稱] 做為值](master-detail-filtering-with-two-dropdownlists-vb/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image10.png)

**圖 4**：讓 DropDownList 顯示 `CategoryName` 欄位，並使用 `CategoryID` 作為值（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image12.png)）

此時，我們有一個 DropDownList 控制項（`Categories`），其中填入 `Categories` 資料表中的記錄。 當使用者從 DropDownList 選擇新的類別時，我們會想要進行回傳，以便重新整理我們要在步驟2中建立的產品 DropDownList。 因此，請從 `categories` DropDownList 的智慧標籤中，核取 [啟用 AutoPostBack] 選項。

[![針對 [類別] DropDownList 啟用 AutoPostBack](master-detail-filtering-with-two-dropdownlists-vb/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image13.png)

**圖 5**：為 `Categories` DropDownList 啟用 AutoPostBack （[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image15.png)）

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>步驟2：在第二個 DropDownList 中顯示所選類別的產品

當 `Categories` DropDownList 完成時，下一個步驟是顯示屬於所選類別的產品 DropDownList。 若要完成此動作，請將另一個 DropDownList 新增至名為 `ProductsByCategory`的頁面。 如同 `Categories` DropDownList，針對名為 `ProductsByCategoryDataSource`的 `ProductsByCategory` DropDownList 建立新的 ObjectDataSource。

[![為 Productsbycategory DropDownList 加入新的資料來源](master-detail-filtering-with-two-dropdownlists-vb/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image16.png)

**圖 6**：為 `ProductsByCategory` DropDownList 加入新的資料來源（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image18.png)）

[![建立名為 ProductsByCategoryDataSource 的新 ObjectDataSource](master-detail-filtering-with-two-dropdownlists-vb/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image19.png)

**圖 7**：建立名為 `ProductsByCategoryDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image21.png)）

因為 `ProductsByCategory` DropDownList 只需要顯示屬於所選類別目錄的產品，所以 ObjectDataSource 會從 `ProductsBLL` 物件叫用 `GetProductsByCategoryID(categoryID)` 方法。

[![選擇使用 ProductsBLL 類別](master-detail-filtering-with-two-dropdownlists-vb/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image22.png)

**圖 8**：選擇使用 [`ProductsBLL`] 類別（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image24.png)）

[![將 ObjectDataSource 設定為使用 GetProductsByCategoryID （類別 Id）方法](master-detail-filtering-with-two-dropdownlists-vb/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image25.png)

**圖 9**：設定 ObjectDataSource 以使用 `GetProductsByCategoryID(categoryID)` 方法（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image27.png)）

在 wizard 的最後一個步驟中，我們需要指定 *`categoryID`* 參數的值。 從 `Categories` DropDownList 中，將此參數指派給選取的專案。

[![從 [類別] DropDownList 中提取 [類別目錄] 參數值](master-detail-filtering-with-two-dropdownlists-vb/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image28.png)

**圖 10**：從 `Categories` DropDownList 提取 *`categoryID`* 參數值（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image30.png)）

設定 ObjectDataSource 之後，剩下的工作就是指定要將哪些資料來源欄位用於 DropDownList 專案的顯示和值。 顯示 [`ProductName`] 欄位，並使用 [`ProductID`] 欄位做為值。

[![指定用於 DropDownList 之 ListItems 的 Text 和 Value 屬性的資料來源欄位](master-detail-filtering-with-two-dropdownlists-vb/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image31.png)

**圖 11**：指定用於 DropDownList 的 `ListItem` s ' `Text` 和 `Value` 屬性（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image33.png)）的資料來源欄位

在 ObjectDataSource 和 `ProductsByCategory` DropDownList 設定頁面會顯示兩個 Dropdownlist 進行：第一個會列出所有類別，而第二個則會列出屬於所選類別目錄的產品。 當使用者從第一個 DropDownList 選取新的類別時，回傳將會控制發生，而第二個 DropDownList 會重新系結，顯示屬於新選取之類別的產品。 [圖 12] 和 [13] 顯示透過瀏覽器觀看時 `MasterDetailsDetails.aspx` 動作。

[![第一次造訪頁面時，會選取 [飲料] 類別](master-detail-filtering-with-two-dropdownlists-vb/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image34.png)

**圖 12**：第一次流覽頁面時，會選取 [飲料] 類別（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image36.png)）

[選擇不同類別的 ![會顯示新類別的產品](master-detail-filtering-with-two-dropdownlists-vb/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image37.png)

**圖 13**：選擇不同的類別會顯示新類別的產品（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image39.png)）

目前 `productsByCategory` DropDownList 在變更時 *，不會造成回傳*。 不過，我們會希望在我們新增 DetailsView 以顯示所選產品的詳細資料（步驟3）時，回傳才會發生。 因此，請從 `productsByCategory` DropDownList 的智慧標籤中，核取 [啟用 AutoPostBack] 核取方塊。

[![啟用 Productsbycategory DropDownList 的 AutoPostBack 功能](master-detail-filtering-with-two-dropdownlists-vb/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image40.png)

**圖 14**：啟用 `productsByCategory` DropDownList 的 AutoPostBack 功能（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image42.png)）

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>步驟3：使用 DetailsView 來顯示所選產品的詳細資料

最後一個步驟是在 DetailsView 中顯示所選產品的詳細資料。 若要完成此動作，請在頁面中新增 DetailsView，將其 [`ID`] 屬性設為 [`ProductDetails`]，然後為其建立新的 ObjectDataSource。 設定此 ObjectDataSource，使用 *`productID`* 參數值的 `ProductsByCategory` DropDownList 的選取值，從 `ProductsBLL` 類別的 `GetProductByProductID(productID)` 方法中提取其資料。

[![選擇使用 ProductsBLL 類別](master-detail-filtering-with-two-dropdownlists-vb/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image43.png)

**圖 15**：選擇使用 [`ProductsBLL`] 類別（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image45.png)）

[![將 ObjectDataSource 設定為使用 GetProductByProductID （productID）方法](master-detail-filtering-with-two-dropdownlists-vb/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image46.png)

**圖 16**：設定 ObjectDataSource 以使用 `GetProductByProductID(productID)` 方法（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image48.png)）

[![從 Productsbycategory DropDownList 提取 productID 參數值](master-detail-filtering-with-two-dropdownlists-vb/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image49.png)

**圖 17**：從 `ProductsByCategory` DropDownList 提取 *`productID`* 參數值（[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image51.png)）

您可以選擇在 `ProductDetails` DetailsView 中顯示任何可用的欄位。 我選擇移除 [`ProductID`]、[`SupplierID`] 和 [`CategoryID`] 欄位，然後重新排序並格式化其餘的欄位。 此外，我已清除 DetailsView 的 `Height` 和 `Width` 屬性，讓 DetailsView 可以擴充到最佳顯示其資料所需的寬度，而不是將它限制為指定的大小。 完整的標記如下所示：

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample1.aspx)]

請花點時間嘗試瀏覽器中的 `MasterDetailsDetails.aspx` 頁面。 乍看之下，可能會顯示一切都如預期般運作，但有一個小問題。 當您選擇新的類別時，`ProductsByCategory` DropDownList 會更新為包含所選類別的那些產品，但 `ProductDetails` DetailsView 會繼續顯示先前的產品資訊。 為選取的類別選擇不同的產品時，會更新 DetailsView。 此外，如果您徹底測試，就會發現如果您持續選擇 [新類別] （例如從 [`Categories` DropDownList] 選擇 [飲料]，然後 Condiments，然後 Confections）每個其他類別選取專案，就會重新整理 `ProductDetails` DetailsView。

為了協助將實體化這個問題，讓我們來看一個特定的範例。 當您第一次流覽頁面時，會選取 [飲料] 類別，並在 [`ProductsByCategory`] DropDownList 中載入相關的產品。 Chai 是選取的產品，而其詳細資料會顯示在 `ProductDetails` DetailsView 中，如 [圖 18] 所示。

[![所選產品的詳細資料會顯示在 DetailsView 中](master-detail-filtering-with-two-dropdownlists-vb/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image52.png)

**圖 18**：所選產品的詳細資料會顯示在 DetailsView 中（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image54.png)）

如果您將類別選擇從飲料變更為 Condiments，就會發生回傳，並據此更新 `ProductsByCategory` DropDownList，但是 DetailsView 仍然會顯示 Chai 的詳細資料。

[![仍會顯示先前選取的產品詳細資料](master-detail-filtering-with-two-dropdownlists-vb/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image55.png)

**圖 19**：仍會顯示先前選取的產品詳細資料（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image57.png)）

從清單中挑選新產品，會如預期般重新整理 DetailsView。 如果您在變更產品後選擇新的類別，則不會重新整理 DetailsView。 不過，如果您選擇新的產品，而不是選擇新的類別，則 DetailsView 會重新整理。 世界上有哪些功能？

問題是網頁生命週期中的時間問題。 每當要求頁面時，它會繼續執行一些步驟做為其轉譯。 在下列其中一個步驟中，ObjectDataSource 控制項會檢查其 `SelectParameters` 值是否已變更。 若是如此，系結至 ObjectDataSource 的資料 Web 控制項就知道它需要重新整理它的顯示。 例如，當選取新的分類時，`ProductsByCategoryDataSource` ObjectDataSource 會偵測到其參數值已變更，且 `ProductsByCategory` DropDownList 重新系結本身，以取得所選類別目錄的產品。

在這種情況下發生的問題，是頁面生命週期中的 ObjectDataSources 檢查已變更參數的位置會在重新系結相關聯的資料 Web 控制項*之前*進行。 因此，當選取新的類別時，`ProductsByCategoryDataSource` ObjectDataSource 會偵測其參數值的變更。 不過，`ProductDetails` DetailsView 所使用的 ObjectDataSource 並不會注意到任何這類變更，因為 `ProductsByCategory` DropDownList 尚未重新系結。 稍後在生命週期中，`ProductsByCategory` DropDownList 會重新系結至其 ObjectDataSource，並抓取新選取之類別目錄的產品。 當 `ProductsByCategory` DropDownList 的值已變更時，`ProductDetails` DetailsView 的 ObjectDataSource 已經完成其參數值檢查;因此，DetailsView 會顯示其先前的結果。 這項互動如 [圖 20] 所示。

[![ProductDetails DetailsView 的 ObjectDataSource 檢查變更後，Productsbycategory DropDownList 值的變更](master-detail-filtering-with-two-dropdownlists-vb/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image58.png)

**圖 20**： `ProductDetails` DetailsView 的 ObjectDataSource 檢查變更後，`ProductsByCategory` DropDownList 值變更（[按一下以觀看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image60.png)）

若要解決此問題，我們必須在系結 `ProductsByCategory` DropDownList 之後，明確地重新系結 `ProductDetails` DetailsView。 當 `ProductsByCategory` DropDownList 的 `DataBound` 事件引發時，我們可以呼叫 `ProductDetails` DetailsView 的 `DataBind()` 方法來完成這項操作。 將下列事件處理常式程式碼加入至 `MasterDetailsDetails.aspx` 頁面的程式碼後置類別（如需如何新增事件處理常式的相關討論，請參閱「以程式設計[方式設定 ObjectDataSource 的參數值](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)」）：

[!code-vb[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample2.vb)]

新增 `ProductDetails` DetailsView 的 `DataBind()` 方法的明確呼叫之後，本教學課程會如預期般運作。 [圖 21] 強調了這種改變如何補救先前的問題。

[![當 Productsbycategory DropDownList 的資料系結事件引發時，會明確重新整理 ProductDetails DetailsView](master-detail-filtering-with-two-dropdownlists-vb/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image61.png)

**圖 21**：當 `ProductsByCategory` DropDownList 的 `DataBound` 事件引發時，會明確地重新整理 `ProductDetails` DetailsView （[按一下以查看完整大小的影像](master-detail-filtering-with-two-dropdownlists-vb/_static/image63.png)）

## <a name="summary"></a>總結

DropDownList 可做為主要/詳細資料包表的理想使用者介面專案，其中主要和詳細資料記錄之間有一對多關聯性。 在先前的教學課程中，我們已瞭解如何使用單一 DropDownList 來篩選所選類別所顯示的產品。 在本教學課程中，我們將產品的 GridView 取代為 DropDownList，並使用 DetailsView 來顯示所選產品的詳細資料。 本教學課程中所討論的概念可以輕鬆地延伸到涉及多個一對多關聯性的資料模型，例如客戶、訂單和訂單專案。 一般而言，您一律可以針對一對多關聯性中的每個「一」實體加入 DropDownList。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](master-detail-filtering-with-a-dropdownlist-vb.md)
> [下一頁](master-detail-filtering-across-two-pages-vb.md)
