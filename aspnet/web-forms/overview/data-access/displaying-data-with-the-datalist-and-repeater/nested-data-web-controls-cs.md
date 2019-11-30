---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
title: 嵌套的資料 Web 控制項C#（） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何使用嵌套在另一個中繼器內的中繼器。 這些範例將說明如何將內部中繼器全部填入 d 。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: ad3cb0ec-26cf-42d7-b81b-184a34ec9f86
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8ef15bebb2c29976274b0cca1d6ace434ccc55ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640343"
---
# <a name="nested-data-web-controls-c"></a>巢狀資料 Web 控制項 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_CS.exe)或[下載 PDF](nested-data-web-controls-cs/_static/datatutorial32cs1.pdf)

> 在本教學課程中，我們將探討如何使用嵌套在另一個中繼器內的中繼器。 這些範例將說明如何以宣告方式和程式設計方式填入內部中繼器。

## <a name="introduction"></a>簡介

除了靜態 HTML 和資料系結語法，範本也可以包含 Web 控制項和使用者控制項。 這些 Web 控制項可以透過宣告式、資料系結語法來指派其屬性，或可在適當的伺服器端事件處理常式中以程式設計方式存取。

藉由在範本中內嵌控制項，可以自訂和改善外觀和使用者體驗。 例如，在 GridView 控制項教學課程的[使用 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)中，我們已瞭解如何在 TemplateField 中加入行事曆控制項來自訂 GridView 的顯示，以顯示員工的雇用日期;在將[驗證控制項新增至編輯和插入介面](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)和[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教學課程中，我們已瞭解如何藉由加入驗證控制項、文字方塊、dropdownlist 進行和其他 Web 控制項來自訂編輯和插入介面。

範本也可以包含其他資料 Web 控制項。 也就是說，在其範本中，我們可以有一個 DataList，其中包含另一個 DataList （或重複項或 GridView 或 DetailsView 等等）。 這類介面的挑戰，就是將適當的資料系結至內部資料 Web 控制項。 有幾種不同的方法可用，範圍從使用 ObjectDataSource 的宣告式選項到程式設計方式。

在本教學課程中，我們將探討如何使用嵌套在另一個中繼器內的中繼器。 外部中繼器會針對資料庫中的每個類別目錄包含一個專案，並顯示類別目錄的名稱和描述。 每個類別目錄專案的內部中繼器都會在項目符號清單中顯示屬於該類別的每個產品的資訊（請參閱 [圖 1]）。 我們的範例將說明如何以宣告方式和程式設計方式填入內部中繼器。

[列出每個類別及其產品的 ![](nested-data-web-controls-cs/_static/image2.png)](nested-data-web-controls-cs/_static/image1.png)

**圖 1**：會列出每個類別及其產品（[按一下以觀看完整大小的影像](nested-data-web-controls-cs/_static/image3.png)）

## <a name="step-1-creating-the-category-listing"></a>步驟1：建立類別目錄清單

在建立使用嵌套資料 Web 控制項的網頁時，我發現，最好先設計、建立和測試最外層的資料 Web 控制項，而不必擔心內部的嵌套控制項。 因此，讓我們先逐步完成在列出每個類別的名稱和描述的情況下，將中繼器新增至頁面的必要步驟。

一開始先開啟 [`DataListRepeaterBasics`] 資料夾中的 [`NestedControls.aspx`] 頁面，並將 [中繼器] 控制項新增至頁面，將其 `ID` 屬性設定為 [`CategoryList`]。 從 [中繼器] 智慧標籤中，選擇建立名為 `CategoriesDataSource`的新 ObjectDataSource。

[![命名新的 ObjectDataSource CategoriesDataSource](nested-data-web-controls-cs/_static/image5.png)](nested-data-web-controls-cs/_static/image4.png)

**圖 2**：為新的 ObjectDataSource `CategoriesDataSource` 命名（[按一下以查看完整大小的影像](nested-data-web-controls-cs/_static/image6.png)）

設定 ObjectDataSource，使其從 `CategoriesBLL` 類別的 `GetCategories` 方法提取其資料。

[![將 ObjectDataSource 設定為使用 CategoriesBLL 類別的 GetCategories 方法](nested-data-web-controls-cs/_static/image8.png)](nested-data-web-controls-cs/_static/image7.png)

**圖 3**：設定 ObjectDataSource 使用 `CategoriesBLL` 類別的 `GetCategories` 方法（[按一下以查看完整大小的影像](nested-data-web-controls-cs/_static/image9.png)）

若要指定中繼器的範本內容，我們需要移至來源視圖，然後手動輸入宣告式語法。 新增 `ItemTemplate`，在 `<h4>` 專案中顯示類別目錄名稱，並在段落元素（`<p>`）中加入 category s 描述。 此外，讓我們使用水準規則（`<hr>`）來分隔每個類別目錄。 進行這些變更之後，您的頁面應該會包含如下所示之中繼器和 ObjectDataSource 的宣告式語法：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample1.aspx)]

[圖 4] 顯示透過瀏覽器觀看的進度。

[![列出每個分類的名稱和描述，並以水準規則分隔](nested-data-web-controls-cs/_static/image11.png)](nested-data-web-controls-cs/_static/image10.png)

**圖 4**：每個分類的名稱和描述都會列出，並以水準規則分隔（[按一下以查看完整大小的影像](nested-data-web-controls-cs/_static/image12.png)）

## <a name="step-2-adding-the-nested-product-repeater"></a>步驟2：新增嵌套的產品中繼器

類別清單完成後，下一個工作是將「中繼器」新增至 `CategoryList` s `ItemTemplate`，以顯示屬於適當類別的產品相關資訊。 有幾種方法可以抓取此內部中繼器的資料，我們很快就會探索其中兩個。 現在，讓我們只在 `CategoryList` 中繼器 `ItemTemplate`內建立產品中繼器。 具體來說，讓產品中繼器在項目符號清單中顯示每個產品，其中每個清單專案都包含產品的名稱和價格。

若要建立此中繼器，我們必須以手動方式將內部中繼器的宣告式語法和範本輸入 `CategoryList` 的 `ItemTemplate`中。 在 `CategoryList` 中繼器 `ItemTemplate`內新增下列標記：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>步驟3：將類別特定的產品系結至 ProductsByCategoryList 中繼器

如果您在此時透過瀏覽器造訪網頁，您的畫面看起來會像 [圖 4] 所示，因為我們尚未將任何資料系結至中繼器。 有幾種方式可以取得適當的產品記錄，並將它們系結至重複項，比其他專案更有效率。 這裡的主要挑戰是針對指定的類別，取回適當的產品。

要系結至內部重複項控制項的資料，可以透過 `CategoryList` 中繼器 s `ItemTemplate`中的 ObjectDataSource 或以程式設計方式，從 ASP.NET 網頁的程式碼後置頁面進行存取。 同樣地，這項資料可以透過宣告方式，系結至內部中繼器 `DataSourceID` 屬性，或透過宣告式資料系結語法或以程式設計方式系結至內部的 Repeater，方法是在 `CategoryList` 中繼器 s `ItemDataBound` 事件處理常式中參考內部中繼器，以程式設計方式設定其 `DataSource` 屬性，並呼叫其 `DataBind()` 方法。 讓我們來探索每一種方法。

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>使用 ObjectDataSource 控制項和`ItemDataBound`事件處理常式以宣告方式存取資料

由於我們已在整個教學課程系列中廣泛使用 ObjectDataSource，因此在此範例中，存取資料最自然的選擇是要堅持 ObjectDataSource。 `ProductsBLL` 類別具有 `GetProductsByCategoryID(categoryID)` 方法，會傳回屬於指定 *`categoryID`* 之產品的相關資訊。 因此，我們可以將 ObjectDataSource 新增至 `CategoryList` 的中繼器 `ItemTemplate`，並將其設定為從這個類別的方法存取其資料。

可惜的是，中繼器不允許透過設計檢視編輯其範本，因此我們需要手動新增這個 ObjectDataSource 控制項的宣告式語法。 下列語法顯示在新增這個新的 ObjectDataSource （`ProductsByCategoryDataSource`）之後，`CategoryList` 中繼器 `ItemTemplate`：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample3.aspx)]

使用 ObjectDataSource 方法時，我們需要將 `ProductsByCategoryList` 中繼器 s `DataSourceID` 屬性設定為 ObjectDataSource 的 `ID` （`ProductsByCategoryDataSource`）。 此外，請注意，我們的 ObjectDataSource 有一個 `<asp:Parameter>` 元素，指定將傳遞至 `GetProductsByCategoryID(categoryID)` 方法的 *`categoryID`* 值。 但是，我們要如何指定這個值呢？ 在理想的情況下，我們可以使用資料系結語法來設定 `<asp:Parameter>` 元素的 `DefaultValue` 屬性，如下所示：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample4.aspx)]

可惜的是，資料系結語法只有在具有 `DataBinding` 事件的控制項中才有效。 `Parameter` 類別缺少這類事件，因此上述語法不合法，而且會導致執行階段錯誤。

若要設定這個值，我們需要為 `CategoryList` 中繼器 `ItemDataBound` 事件建立事件處理常式。 回想一下，`ItemDataBound` 事件會針對系結至中繼器的每個專案引發一次。 因此，每次針對外部中繼器引發此事件時，我們可以將目前的 `CategoryID` 值指派給 `ProductsByCategoryDataSource` ObjectDataSource s `CategoryID` 參數。

使用下列程式碼，為 `CategoryList` 中繼器 s `ItemDataBound` 事件建立事件處理常式：

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample5.cs)]

這個事件處理常式一開始會確保我們會處理資料項目，而不是標頭、頁尾或分隔符號專案。 接下來，我們會參考剛系結至目前 `RepeaterItem`的實際 `CategoriesRow` 實例。 最後，我們會參考 `ItemTemplate` 中的 ObjectDataSource，並將其 `CategoryID` 參數值指派給目前 `RepeaterItem`的 `CategoryID`。

使用此事件處理常式，每個 `RepeaterItem` 中的 `ProductsByCategoryList` 中繼器都會系結至 `RepeaterItem` s 類別目錄中的產品。 [圖 5] 顯示結果輸出的螢幕擷取畫面。

[![外部中繼器會列出每個類別;內部程式會列出該類別的產品](nested-data-web-controls-cs/_static/image14.png)](nested-data-web-controls-cs/_static/image13.png)

**圖 5**：外部中繼器會列出每個類別目錄;內部程式會列出該類別的產品（[按一下以查看完整大小的影像](nested-data-web-controls-cs/_static/image15.png)）

## <a name="accessing-the-products-by-category-data-programmatically"></a>以程式設計方式存取依類別目錄資料的產品

我們不使用 ObjectDataSource 來抓取目前類別的產品，而是在 ASP.NET 網頁的程式碼後置類別中（或在 [`App_Code`] 資料夾或個別的類別庫專案中）建立方法，以在 `CategoryID`傳入時傳回適當的一組產品。 假設我們的 ASP.NET page s 程式碼後置類別中有這種方法，而且它的名稱為 `GetProductsInCategory(categoryID)`。 有了這個方法，我們就可以使用下列宣告式語法，將目前類別目錄的產品系結至內部中繼器：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample6.aspx)]

[中繼器] `DataSource` 屬性會使用資料系結語法來表示其資料來自 `GetProductsInCategory(categoryID)` 方法。 由於 `Eval("CategoryID")` 會傳回 `Object`類型的值，因此我們會先將物件轉換成 `Integer`，再將它傳遞至 `GetProductsInCategory(categoryID)` 方法。 請注意，透過資料系結語法存取的 `CategoryID` 是*外部*中繼器（`CategoryList`）中的 `CategoryID`，系結至 `Categories` 資料表中的記錄。 因此，我們知道 `CategoryID` 不可以是資料庫 `NULL` 值，這就是為什麼我們可以盲目地轉換 `Eval` 方法，而不需要檢查是否有 `DBNull`的處理。

使用此方法時，我們必須建立 `GetProductsInCategory(categoryID)` 方法，並讓它根據提供的 *`categoryID`* 來抓取一組適當的產品。 我們可以藉由直接傳回 `ProductsBLL` class s `GetProductsByCategoryID(categoryID)` 方法所傳回的 `ProductsDataTable` 來完成這項操作。 讓 s 在 `NestedControls.aspx` 頁面的程式碼後置類別中建立 `GetProductsInCategory(categoryID)` 方法。 請使用下列程式碼來執行此動作：

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample7.cs)]

這個方法只會建立 `ProductsBLL` 方法的實例，並傳回 `GetProductsByCategoryID(categoryID)` 方法的結果。 請注意，此方法必須標記 `Public` 或 `Protected`;如果方法標記為 `Private`，就無法從 ASP.NET 網頁的宣告式標記存取。

進行這些變更以使用這項新技術之後，請花一點時間透過瀏覽器來觀看頁面。 使用 ObjectDataSource 和 `ItemDataBound` 事件處理常式方法時，輸出應該與輸出相同（請參閱 [圖 5] 以查看螢幕擷取畫面）。

> [!NOTE]
> 在 ASP.NET page s 程式碼後置類別中，可能看起來像 busywork 來建立 `GetProductsInCategory(categoryID)` 方法。 畢竟，這個方法只會建立 `ProductsBLL` 類別的實例，並傳回其 `GetProductsByCategoryID(categoryID)` 方法的結果。 為什麼不直接從內部中繼器中的資料系結語法呼叫這個方法，像是： `DataSource='<%# ProductsBLL.GetProductsByCategoryID((int)(Eval("CategoryID"))) %>'`？ 雖然這個語法不適用於目前的 `ProductsBLL` 類別的執行（因為 `GetProductsByCategoryID(categoryID)` 方法是實例方法），您可以修改 `ProductsBLL` 以包含靜態 `GetProductsByCategoryID(categoryID)` 方法，或讓類別包含靜態 `Instance()` 方法，以傳回 `ProductsBLL` 類別的新實例。

雖然這類修改不需要 ASP.NET 網頁的程式碼後置類別中的 `GetProductsInCategory(categoryID)` 方法，但程式碼後置類別方法可讓我們更有彈性地使用所抓取的資料，如我們稍後所見。

## <a name="retrieving-all-of-the-product-information-at-once"></a>一次取出所有產品資訊

我們所檢查的兩個舊技術會藉由呼叫 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法（第一個方法是透過 ObjectDataSource 執行，第二個是透過程式碼後置類別中的 `GetProductsInCategory(categoryID)` 方法），來取得目前類別的產品。 每次叫用此方法時，商務邏輯層會向下呼叫資料存取層，這會使用 SQL 語句來查詢資料庫，而此語句會從 `Products` 資料表中傳回資料列，而該資料表的 `CategoryID` 欄位符合提供的輸入參數。

在系統中指定*n*個類別時，此方法會神經網路*n* + 1 呼叫資料庫一個資料庫查詢來取得所有類別，然後按*n*次呼叫取得每個類別的特定產品。 不過，我們可以只在兩個資料庫呼叫中取出所有需要的資料，以取得所有類別，另一個呼叫來取得所有的產品。 一旦有了所有產品之後，我們就可以篩選這些產品，只有符合目前 `CategoryID` 的產品才會系結到該類別的內部中繼器。

為了提供這項功能，我們只需要稍微修改 ASP.NET page s 程式碼後置類別中的 `GetProductsInCategory(categoryID)` 方法。 我們可以改為先存取*所有*的產品（如果尚未存取），然後根據傳入的 `CategoryID`只傳回產品的篩選視圖，而不是盲目地傳回 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法的結果。

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample8.cs)]

請注意頁面層級變數的加入，`allProducts`。 這會保留所有產品的相關資訊，並在第一次叫用 `GetProductsInCategory(categoryID)` 方法時填入。 確定已建立並填入 `allProducts` 物件之後，方法會篩選 DataTable 的結果，使只有 `CategoryID` 符合指定 `CategoryID` 的資料列可以存取。 這種方法可減少從*N* + 1 到2的資料庫存取次數。

這項增強功能並不會對頁面轉譯的標記引進任何變更，也不會傳回比其他方法更少的記錄。 它只會減少對資料庫的呼叫次數。

> [!NOTE]
> 其中一個可能會直覺地減少資料庫存取的數目，確實改善效能。 不過，這可能不是這種情況。 例如，如果您有大量的產品，而其 `CategoryID` `NULL`，則呼叫 `GetProducts` 方法會傳回永遠不會顯示的產品數目。 此外，如果您只顯示類別的子集，則傳回所有產品可能會很浪費，如果您已經實頁，可能就會發生這種情況。

一如往常，在分析兩項技術的效能時，唯一的笑話量值是執行針對您的應用程式的常見案例所量身打造的受控制測試。

## <a name="summary"></a>總結

在本教學課程中，我們已瞭解如何將一個資料 Web 控制項放在另一個中，特別是檢查如何讓外部的重複項顯示每個類別的專案，並使用內部的重複項來列出項目符號清單中每個類別目錄的產品。 建立嵌套使用者介面的主要挑戰在於存取並將正確的資料系結至內部資料 Web 控制項。 有各種不同的技術，我們在本教學課程中探討了其中兩種。 第一種方法是使用外部資料 Web 控制項中的 ObjectDataSource，`ItemTemplate` 透過其 `DataSourceID` 屬性系結至內部資料 Web 控制項。 第二個技巧是透過 ASP.NET page s 程式碼後置類別中的方法來存取資料。 然後，這個方法就可以透過資料系結語法，系結至內部資料 Web 控制項的 `DataSource` 屬性。

雖然在本教學課程中檢查的嵌套使用者介面使用了在重複項中嵌套的重複項，但這些技術可以擴充至其他資料 Web 控制項。 您可以在 GridView 內或在 DataList 內的 GridView 中嵌套重複項，依此類推。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Zack，Liz Shulok。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
> [下一頁](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
