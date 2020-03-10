---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
title: 使用具有詳細資料 DataList 的主要記錄項目符號清單的主要/詳細資料（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們會將上一個教學課程的兩頁主要/詳細資料包表壓縮成單一頁面，並在 [t ...] 上顯示分類名稱的項目符號清單。
ms.author: riande
ms.date: 10/17/2006
ms.assetid: ee20742f-6fb7-49a0-a009-058fe363aacb
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 81d72c666925e89729464e7ea696bde8d323e277
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78605956"
---
# <a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb"></a>使用具有詳細資料 DataList 的主要記錄項目符號清單的主要/詳細 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_VB.exe)或[下載 PDF](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/datatutorial35vb1.pdf)

> 在本教學課程中，我們會將上一個教學課程的兩頁主要/詳細資料包表壓縮成單一頁面，並在畫面的左側顯示分類名稱的項目符號清單，以及螢幕右側所選類別目錄的產品。

## <a name="introduction"></a>簡介

在[先前的教學](master-detail-filtering-acess-two-pages-datalist-vb.md)課程中，我們探討了如何跨兩個頁面分隔主要/詳細資料包表。 在主版頁面中，我們使用了重複項控制項來轉譯類別的項目符號清單。 每個類別目錄名稱都是超連結，當按下時，會將使用者帶到詳細資料頁面，其中，兩欄的 DataList 會顯示屬於所選類別目錄的產品。

在本教學課程中，我們會將兩頁教學課程壓縮成單一頁面，在畫面左側顯示類別目錄名稱的項目符號清單，並將每個類別目錄名稱轉譯為 LinkButton。 按一下其中一個類別目錄名稱 LinkButtons 會引發回傳，並將選取的類別 s 產品系結至螢幕右邊的兩個數據行 DataList。 除了顯示每個類別目錄的名稱，左邊的中繼器會顯示指定類別的總產品數（請參閱 [圖 1]）。

[![類別目錄的名稱，以及顯示在左側的產品總數](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image1.png)

**圖 1**：類別目錄的名稱和產品總數會顯示在左邊（[按一下以觀看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image3.png)）

## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>步驟1：在畫面的左邊部分顯示中繼器

在本教學課程中，我們必須在所選類別目錄的左邊顯示分類的類別目錄清單。 網頁中的內容可以使用標準的 HTML 專案段落標記、不分行空格、`<table>` s，或透過級聯樣式表單（CSS）技術來定位。 到目前為止，我們的所有教學課程都使用了 CSS 技術來定位。 當我們在主版頁面[和網站導覽](../introduction/master-pages-and-site-navigation-vb.md)教學課程的主版頁面中建立導覽使用者介面時，我們使用了*絕對位置*，指出導覽清單和主要內容的精確圖元位移。 或者，您可以使用 CSS，透過*浮動*將某個元素放在另一個專案的右邊或左邊。 在選取的類別 s 產品的左邊，我們可以將重複項的清單顯示在 [DataList] 左邊，

從 [`DataListRepeaterFiltering`] 資料夾開啟 [`CategoriesAndProducts.aspx`] 頁面，並將 [中繼器] 和 [DataList] 加入至頁面。 將 中繼器 s `ID` 設定為 `Categories`，並將 DataList 設為 `CategoryProducts`。 移至 [來源] 視圖，並將 [中繼器] 和 [DataList] 控制項放在自己的 `<div>` 元素內。 也就是，先將重複項放在 `<div>` 專案中，然後在它自己的 `<div>` 元素中，直接在中繼器後面加上 DataList。 此時您的標記看起來應該如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample1.aspx)]

若要將重複項的浮動加入 DataList 的左邊，我們必須使用 `float` CSS 樣式屬性，如下所示：

[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample2.html)]

`float: left;` 會將第一個 `<div>` 專案浮動到第二個元素的左邊。 `width` 和 `padding-right` 設定會指出第一個 `<div>` 的 `width`，以及要在 `<div>` 元素的內容及其右邊界之間加入多少填補。 如需 CSS 中浮動元素的詳細資訊，請參閱[Floatutorial](http://css.maxdesign.com.au/floatutorial/)。

不是直接透過第一個 `<p>` 元素 `style` 屬性來指定樣式設定，而是改為在名為 `FloatLeft`的 `Styles.css` 中建立新的 CSS 類別：

[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample3.css)]

然後，我們可以使用 `<div class="FloatLeft">`來取代 `<div>`。

在 [`CategoriesAndProducts.aspx`] 頁面中加入 CSS 類別並設定標記之後，請移至設計工具。 您應該會看到在 DataList 左邊浮動的中繼器（雖然現在這兩個都只會顯示為灰色方塊，因為我們尚未設定其資料來源或範本）。

[![在 DataList 的左邊浮動中繼器](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image4.png)

**圖 2**：中繼器會浮動在 DataList 的左邊（[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image6.png)）

## <a name="step-2-determining-the-number-of-products-for-each-category"></a>步驟2：判斷每個類別目錄的產品數目

有了重複項標記和 DataList 的周圍標記完成後，我們就準備好將類別目錄資料系結至重複項控制項。 不過，如同 [圖 1] 中的類別目錄清單所示，除了每個類別目錄的名稱之外，我們也需要顯示與類別相關聯的產品數目。 若要存取這項資訊，我們可以執行下列其中一項：

- **從 ASP.NET 網頁的程式碼後置類別中判斷此資訊。** 假設有特定 *`categoryID`* 我們可以藉由呼叫 `ProductsBLL` 類別 s `GetProductsByCategoryID(categoryID)` 方法來判斷相關聯的產品數目。 這個方法會傳回 `ProductsDataTable` 物件，其 `Count` 屬性指出存在多少 `ProductsRow` 秒，也就是指定 *`categoryID`* 的產品數目。 我們可以為中繼器建立 `ItemDataBound` 事件處理常式，每個系結至中繼器的類別都會呼叫 `ProductsBLL` 類別 s `GetProductsByCategoryID(categoryID)` 方法，並將其計數包含在輸出中。
- **更新具類型資料集中的 `CategoriesDataTable`，以包含 `NumberOfProducts` 的資料行。** 然後，我們可以更新 `CategoriesDataTable` 中的 `GetCategories()` 方法以包含這項資訊，或者將 `GetCategories()` 保持原狀，並建立稱為 `GetCategoriesAndNumberOfProducts()`的新 `CategoriesDataTable` 方法。

讓我們來探索這兩種技術。 第一種方法較容易實行，因為我們不需要更新資料存取層;不過，它需要更多與資料庫的通訊。 在 `ItemDataBound` 事件處理常式中呼叫 `ProductsBLL` 類別 `GetProductsByCategoryID(categoryID)` 方法，會為重複項中顯示的每個類別新增額外的資料庫呼叫。 使用這項技術時，會有*n* + 1 個資料庫呼叫，其中*N*是在中繼器中顯示的類別目錄數目。 使用第二種方法時，會傳回產品計數，其中包含來自 `CategoriesBLL` 類別 `GetCategories()` （或 `GetCategoriesAndNumberOfProducts()`）方法的每個分類的相關資訊，因此只會產生一次資料庫的往返。

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>判斷 ItemDataBound 事件處理常式中的產品數目

判斷中繼器中每個類別的產品數目 `ItemDataBound` 事件處理常式不需要對現有的資料存取層進行任何修改。 所有的修改都可以直接在 [`CategoriesAndProducts.aspx`] 頁面中進行。 首先，透過 [中繼器] 智慧標籤，新增名為 `CategoriesDataSource` 的新 ObjectDataSource。 接下來，設定 `CategoriesDataSource` ObjectDataSource，使其從 `CategoriesBLL` 類別 s `GetCategories()` 方法中抓取其資料。

[![將 ObjectDataSource 設定為使用 CategoriesBLL 類別的 GetCategories （）方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image7.png)

**圖 3**：設定 ObjectDataSource 使用 `CategoriesBLL` 類別的 `GetCategories()` 方法（[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image9.png)）

`Categories` 中繼器中的每個專案都必須是可按的，並且在按一下時，會導致 `CategoryProducts` DataList 顯示所選類別的這些產品。 這可以藉由將每個類別設為超連結、連結回到這個相同的頁面（`CategoriesAndProducts.aspx`）來完成，但透過 querystring 傳遞 `CategoryID`，與我們在上一個教學課程中看到的類似。 這種方法的優點是顯示特定類別目錄產品的頁面，可以由搜尋引擎以書簽和編制索引。

或者，我們可以將每個類別設為 LinkButton，這是我們將在本教學課程中使用的方法。 LinkButton 會在使用者的瀏覽器中轉譯為超連結，但是按一下時，會引發回傳。在回傳時，DataList s ObjectDataSource 必須重新整理，才能顯示屬於所選類別目錄的產品。 在本教學課程中，使用超連結會比使用 LinkButton 更合理。不過，在某些情況下，使用 LinkButton 會更有利。 雖然超連結方法是此範例的理想選擇，但讓我們改為使用 LinkButton 來探索。 如我們所見，使用 LinkButton 會帶來一些因超連結而不會發生的挑戰。 因此，在本教學課程中使用 LinkButton 將會反白顯示這些挑戰，並協助為我們想要使用 LinkButton 而非超連結的案例提供解決方案。

> [!NOTE]
> 建議您使用超連結控制項或 `<a>` 元素（而不是 LinkButton）來重複本教學課程。

下列標記顯示中繼器和 ObjectDataSource 的宣告式語法。 請注意，[中繼器] 範本會以項目符號清單呈現每個專案的 LinkButton：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample4.aspx)]

> [!NOTE]
> 在本教學課程中，中繼器必須啟用其 view 狀態（請注意，從中繼器 s 宣告式語法省略 `EnableViewState="False"`）。 在步驟3中，我們將為 [中繼器] `ItemCommand` 事件建立事件處理常式，我們將在其中更新 DataList s ObjectDataSource `SelectParameters` 集合。 不過，如果停用檢視狀態，則不會引發中繼器 `ItemCommand`。 請參閱[ASP.NET 問題](http://scottonwriting.net/sowblog/posts/1263.aspx)和[其解決方案](http://scottonwriting.net/sowBlog/posts/1268.aspx)的 Stumper，以瞭解為什麼必須針對中繼器 `ItemCommand` 事件啟用 view 狀態的詳細資訊。

`ID` 屬性值為 `ViewCategory` 的 LinkButton 並未設定其 `Text` 屬性。 如果我們只想要顯示類別名稱，我們會透過資料系結語法，以宣告方式設定文字屬性，如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample5.aspx)]

不過，我們想要顯示類別目錄的名稱 *，以及*屬於該類別目錄的產品數目。 這項資訊可以從中繼器 `ItemDataBound` 事件處理常式中取得，方法是呼叫 `ProductBLL` 類別 s `GetCategoriesByProductID(categoryID)` 方法，並判斷產生的 `ProductsDataTable`中傳回多少筆記錄，如下列程式碼所示：

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample6.vb)]

我們一開始先確定我們會使用資料項目（其 `ItemType` `Item` 或 `AlternatingItem`），然後參考剛系結至目前 `RepeaterItem`的 `CategoriesRow` 實例。 接下來，我們會藉由建立 `ProductsBLL` 類別的實例、呼叫其 `GetCategoriesByProductID(categoryID)` 方法，以及使用 `Count` 屬性來判斷傳回的記錄數目，來判斷此類別的產品數目。 最後，ItemTemplate 中的 `ViewCategory` LinkButton 是參考，而且它的 `Text` 屬性會設定為 [*類別名稱*（*NumberOfProductsInCategory*）]，其中*NumberOfProductsInCategory*會格式化為零位數的數位。

> [!NOTE]
> 或者，我們也可以將*格式化函數*新增至 ASP.NET 網頁的程式碼後置類別，此類別會接受 category `CategoryName` 並 `CategoryID` 值，並傳回與類別目錄中的產品數目（藉由呼叫 `GetCategoriesByProductID(categoryID)` 方法所決定）串連的 `CategoryName`。 這類格式化函式的結果可以用宣告方式指派給 LinkButton s Text 屬性，以取代 `ItemDataBound` 事件處理常式的需求。 如需有關使用格式化函數的詳細資訊，請參閱[GridView 控制項中的 Using TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)或根據資料教學課程來[格式化 DataList 和中繼器](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md)。

加入這個事件處理常式之後，請花一點時間透過瀏覽器來測試頁面。 請注意每個類別目錄在項目符號清單中的列出方式，其中會顯示類別目錄的名稱，以及與類別目錄相關聯的產品數目（請參閱 [圖 4]）。

[![顯示每個分類的名稱和產品數目](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image10.png)

**圖 4**：顯示每個類別目錄的名稱和產品數目（[按一下以觀看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image12.png)）

## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>更新`CategoriesDataTable`和`CategoriesTableAdapter`，以包含每個類別目錄的產品數目

我們可以藉由調整資料存取層中的 `CategoriesDataTable` 和 `CategoriesTableAdapter`，以原生方式包含這項資訊，而不是判斷每個類別的產品數與中繼器系結。 若要達到此目的，我們必須將新的資料行新增至 `CategoriesDataTable`，以保存相關聯的產品數目。 若要將新的資料行加入至 DataTable，請開啟具類型資料集（`App_Code\DAL\Northwind.xsd`），以滑鼠右鍵按一下要修改的 DataTable，然後選擇 [加入/資料行]。 將新的資料行加入至 `CategoriesDataTable` （請參閱 [圖 5]）。

[![在 CategoriesDataSource 中加入新的資料行](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image13.png)

**圖 5**：將新的資料行加入至 `CategoriesDataSource` （[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image15.png)）

這會新增名為 `Column1`的新資料行，您只要輸入不同的名稱就可以變更。 將這個新的資料行重新命名為 `NumberOfProducts`。 接下來，我們需要設定這個資料行的屬性。 按一下 [新增] 資料行，然後移至 [屬性視窗]。 將 [資料行 `DataType`] 屬性從 `System.String` 變更為 [`System.Int32`]，並將 `ReadOnly` 屬性設定為 [`True`]，如 [圖 6] 所示。

![設定新資料行的 DataType 和 ReadOnly 屬性](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image16.png)

**圖 6**：設定新資料行的 `DataType` 和 `ReadOnly` 屬性

雖然 `CategoriesDataTable` 現在具有 `NumberOfProducts` 的資料行，但它的值不是由任何對應的 TableAdapter 查詢所設定。 如果我們想要在每次取得類別資訊時傳回這類資訊，我們可以更新 `GetCategories()` 方法以傳回這份資訊。 不過，如果我們只需要抓取罕見實例（例如本教學課程）中類別的相關產品數目，我們可以保持 `GetCategories()`，並建立新的方法來傳回這項資訊。 讓我們使用這個第二種方法，建立名為 `GetCategoriesAndNumberOfProducts()`的新方法。

若要加入這個新的 `GetCategoriesAndNumberOfProducts()` 方法，請在 `CategoriesTableAdapter` 上按一下滑鼠右鍵，然後選擇 [新增查詢]。 這會顯示 [TableAdapter 查詢設定] Wizard，我們在先前的教學課程中使用了許多次。 針對這個方法，您可以藉由指示查詢使用會傳回資料列的臨機操作 SQL 語句來啟動精靈。

[![使用特定 SQL 語句來建立方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image17.png)

**圖 7**：使用臨機操作 SQL 語句建立方法（[按一下以觀看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image19.png)）

[![SQL 語句傳回資料列](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image20.png)

**圖 8**： SQL 語句會傳回資料列（[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image22.png)）

下一個 wizard 畫面會提示我們提供查詢來使用。 若要傳回每個分類 `CategoryID`、`CategoryName`和 `Description` 欄位，以及與類別目錄相關聯的產品數目，請使用下列 `SELECT` 語句：

[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample7.sql)]

[![指定要使用的查詢](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image23.png)

**圖 9**：指定要使用的查詢（[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image25.png)）

請注意，計算與類別目錄相關聯之產品數目的子查詢，其別名為 `NumberOfProducts`。 這個命名相符會使這個子查詢所傳回的值與 `CategoriesDataTable` s `NumberOfProducts` 資料行相關聯。

輸入此查詢之後，最後一個步驟是選擇新方法的名稱。 使用 `FillWithNumberOfProducts` 和 `GetCategoriesAndNumberOfProducts` 來填入 DataTable，並分別傳回 DataTable 模式。

[![命名新的 TableAdapter s 方法 FillWithNumberOfProducts 和 GetCategoriesAndNumberOfProducts](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image26.png)

**圖 10**：命名新的 TableAdapter s 方法 `FillWithNumberOfProducts` 和 `GetCategoriesAndNumberOfProducts` （[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image28.png)）

此時，資料存取層已擴充為包含每個類別的產品數目。 因為我們的所有展示層都會透過不同的商務邏輯層來將所有的呼叫路由傳送給 DAL，所以我們需要將對應的 `GetCategoriesAndNumberOfProducts` 方法新增至 `CategoriesBLL` 類別：

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample8.vb)]

當 DAL 和 BLL 完成後，我們就可以開始將此資料系結至 `CategoriesAndProducts.aspx`中的 `Categories` 中繼器！ 如果您已經從判斷 `ItemDataBound` 事件處理常式中的產品數目一節建立了重複項的 ObjectDataSource，請刪除此 ObjectDataSource 並移除重複項 `DataSourceID` 屬性設定;也藉由移除 ASP.NET 程式碼後置類別中的 `Handles Categories.OnItemDataBound` 語法，從事件處理常式中 unwire 重複項的 `ItemDataBound` 事件。

當重複項回到其原始狀態時，透過中繼器 s 智慧標籤新增名為 `CategoriesDataSource` 的新 ObjectDataSource。 將 ObjectDataSource 設定為使用 `CategoriesBLL` 類別，但不要讓它使用 `GetCategories()` 方法，請改為使用 `GetCategoriesAndNumberOfProducts()` （請參閱 [圖 11]）。

[![將 ObjectDataSource 設定為使用 GetCategoriesAndNumberOfProducts 方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image29.png)

**圖 11**：設定 ObjectDataSource 以使用 `GetCategoriesAndNumberOfProducts` 方法（[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image31.png)）

接下來，更新 `ItemTemplate`，以便以宣告方式使用資料系結語法來指派 LinkButton s `Text` 屬性，同時包含 `CategoryName` 和 `NumberOfProducts` 資料欄位。 中繼器和 `CategoriesDataSource` ObjectDataSource 的完整宣告式標記如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample9.aspx)]

更新 DAL 以包含 `NumberOfProducts` 資料行時所呈現的輸出，與使用 `ItemDataBound` 事件處理常式方法相同（請參閱 [圖 4]，以查看可顯示類別名稱和產品數目的中繼器螢幕擷取畫面）。

## <a name="step-3-displaying-the-selected-category-s-products"></a>步驟3：顯示選取的類別目錄 s 產品

此時，我們有 `Categories` 的重複項會顯示類別目錄清單，以及每個類別目錄中的產品數目。 中繼器會針對每個分類使用 LinkButton，當按下時，會導致回傳，此時我們需要在 `CategoryProducts` DataList 中針對選取的類別顯示這些產品。

我們有一個挑戰，就是如何讓 DataList 只顯示所選類別目錄的產品。 在[主要/詳細資料中使用可選取的主要 GridView 與詳細資料 DetailsView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)教學課程中，我們瞭解到如何建立可以選取資料列的 GridView，並在相同頁面上的 DetailsView 中顯示選取的資料列詳細資料。 GridView 的 ObjectDataSource 會使用 `ProductsBLL` s `GetProducts()` 方法傳回所有產品的相關資訊，而 DetailsView s 則會使用 `GetProductsByProductID(productID)` 方法來抓取所選產品的相關資訊。 *`productID`* 參數值是以宣告方式提供，方法是將它與 GridView 的 `SelectedValue` 屬性的值產生關聯。 可惜的是，中繼器沒有 `SelectedValue` 的屬性，而且不能做為參數來源。

> [!NOTE]
> 這是在中繼器中使用 LinkButton 時所出現的挑戰之一。 我們已使用超連結透過 querystring 傳遞 `CategoryID`，我們可以使用該 QueryString 欄位做為參數 s 值的來源。

不過，在我們擔心會缺少中繼器的 `SelectedValue` 屬性之前，先讓我們先將 DataList 系結至 ObjectDataSource，並指定其 `ItemTemplate`。

從 DataList 的智慧標籤中，加入宣告名為 `CategoryProductsDataSource` 的新 ObjectDataSource，並將其設定為使用 `ProductsBLL` 類別 s `GetProductsByCategoryID(categoryID)` 方法。 由於本教學課程中的 DataList 提供唯讀介面，因此您可以隨意將 [插入]、[更新] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別 s GetProductsByCategoryID （類別 Id）方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image32.png)

**圖 12**：設定 ObjectDataSource 使用 `ProductsBLL` 類別 `GetProductsByCategoryID(categoryID)` 方法（[按一下以觀看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image34.png)）

因為 `GetProductsByCategoryID(categoryID)` 方法需要輸入參數（ *`categoryID`* ），所以 [設定資料來源] wizard 可讓我們指定參數 s 來源。 在 GridView 或 DataList 中列出分類之後，我們會將 [參數來源] 下拉式清單設定為 [控制]，並將 ControlID 至資料 Web 控制項的 [`ID`]。 不過，因為中繼器缺少 `SelectedValue` 的屬性，所以不能用來做為參數來源。 如果您檢查，您會發現 [ControlID] 下拉式清單只包含一個控制項 `ID``CategoryProducts`，也就是 DataList 的 `ID`。

現在，請將 [參數來源] 下拉式清單設定為 [無]。 當您在中繼器中按一下類別 LinkButton 時，最後會以程式設計方式指派此參數值。

[![未指定類別 Id 參數的參數來源](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image35.png)

**圖 13**：請勿指定 *`categoryID`* 參數的參數來源（[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image37.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 自動產生 DataList s `ItemTemplate`。 以我們在上一個教學課程中使用的範本取代此預設 `ItemTemplate`;此外，將 DataList s `RepeatColumns` 屬性設為2。 進行這些變更之後，您的 DataList 及其相關聯的 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample10.aspx)]

目前永遠不會設定 `CategoryProductsDataSource` ObjectDataSource s *`categoryID`* 參數，因此在流覽頁面時不會顯示任何產品。 我們需要做的是根據中繼器中所按下的類別的 `CategoryID`，設定此參數值。 這會帶來兩項挑戰：首先，我們要如何判斷 LinkButton 在中繼器 s `ItemTemplate` 中的何時已按下;第二，如何判斷已按下 LinkButton 的對應分類的 `CategoryID`？

LinkButton （例如按鈕和 ImageButton 控制項）具有 `Click` 事件和[`Command` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)。 `Click` 事件的設計只是要注意，已按一下 LinkButton。 不過，有時候，除了注意到 LinkButton 已按下，我們也需要將一些額外的資訊傳遞給事件處理常式。 如果是這種情況，就可以將此額外資訊指派給 LinkButton s [`CommandName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx)和[`CommandArgument`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx)屬性。 然後，當按一下 LinkButton 時，就會引發它的 `Command` 事件（而不是它的 `Click` 事件），而事件處理常式會傳遞 `CommandName` 和 `CommandArgument` 屬性的值。

當從中繼器中的範本內引發 `Command` 事件時，會引發 Repeater 的[`ItemCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx)，並將所按下 LinkButton （或按鈕或 ImageButton）的 `CommandName` 和 `CommandArgument` 值傳遞給它。 因此，若要判斷是否已按下中繼器中的類別 LinkButton，我們需要執行下列動作：

1. 將中繼器 `ItemTemplate` 中 LinkButton 的 `CommandName` 屬性設定為某個值（我使用 ListProducts）。 藉由設定這個 `CommandName` 值，當按一下 LinkButton 時，就會引發 LinkButton s `Command` 事件。
2. 將 LinkButton 的 `CommandArgument` 屬性設定為目前專案的 `CategoryID`的值。
3. 建立中繼器 `ItemCommand` 事件的事件處理常式。 在事件處理常式中，將 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 參數設定為傳入 `CommandArgument`的值。

類別中繼器的下列 `ItemTemplate` 標記會執行步驟1和2。 請注意，使用資料系結語法，`CommandArgument` 值如何指派 `CategoryID` 資料項目：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample11.aspx)]

每當建立 `ItemCommand` 事件處理常式時，一定要先檢查傳入的 `CommandName` 值，因為中繼器中*任何*按鈕、LinkButton 或 ImageButton 所引發的*任何*`Command` 事件都會導致 `ItemCommand` 事件引發。 雖然我們目前只有一個這類 LinkButton，但在未來，我們（或小組中的其他開發人員）可能會將額外的按鈕 Web 控制項新增至重複項，當按下時，會引發相同的 `ItemCommand` 事件處理常式。 因此，最好一律確保您檢查 `CommandName` 屬性，並只在符合預期值時才繼續程式設計邏輯。

在確認傳入的 `CommandName` 值等於 ListProducts 之後，事件處理常式會將 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 參數指派給傳入的 `CommandArgument`值。 這種對 ObjectDataSource 的修改 `SelectParameters` 會自動導致 DataList 將自己重新系結至資料來源，並顯示新選取之類別目錄的產品。

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample12.vb)]

有了這些新增功能，我們的教學課程就完成了！ 花點時間在瀏覽器中進行測試。 [圖 14] 顯示第一次造訪網頁時的畫面。 因為尚未選取類別，所以不會顯示任何產品。 按一下類別，例如 [產生]，會在兩個數據行的視圖中顯示產品類別目錄中的產品（請參閱 [圖 15]）。

[第一次造訪網頁時，不會顯示 ![的產品](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image38.png)

**圖 14**：第一次流覽頁面時，不會顯示任何產品（[按一下以觀看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image40.png)）

[![按一下 [產生] 類別會列出右側相符的產品](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image41.png)

**圖 15**：按一下 [產生] 類別會列出右側相符的產品（[按一下以查看完整大小的影像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image43.png)）

## <a name="summary"></a>總結

如我們在本教學課程中所見，以及前一個，主要/詳細資料包表可以散佈在兩個頁面上，或合併在一頁上。 不過，在單一頁面上顯示主版/詳細資料包表時，會對如何在頁面上配置主要和詳細資料記錄的方式帶來一些挑戰。 在*主要/詳細資料中，使用可選取的主要 GridView 搭配詳細資料 DetailsView*教學課程，我們將詳細資料記錄顯示在主要記錄上方;在本教學課程中，我們使用了 CSS 技術，讓主要記錄在詳細資料的左邊浮動。

除了顯示主版/詳細資料包告，我們也有機會探索如何抓取與每個類別相關聯的產品數目，以及在從中繼器內按一下 LinkButton （或按鈕或 ImageButton）時，如何執行伺服器端邏輯。

本教學課程使用 DataList 和中繼器完成主要/詳細資料包告的檢查。 我們的下一組教學課程將說明如何將編輯和刪除功能加入至 DataList 控制項。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- 使用 CSS [Floatutorial](http://css.maxdesign.com.au/floatutorial/)浮動 css 元素的教學課程
- [Css](http://www.brainjar.com/css/positioning/)使用 css 定位元素的詳細資訊
- 使用 `<table>` s 和其他 HTML 專案進行定位，[以 HTML 配置內容](http://www.w3schools.com/html/html_layout.asp)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查員是 Zack 的。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](master-detail-filtering-acess-two-pages-datalist-vb.md)
