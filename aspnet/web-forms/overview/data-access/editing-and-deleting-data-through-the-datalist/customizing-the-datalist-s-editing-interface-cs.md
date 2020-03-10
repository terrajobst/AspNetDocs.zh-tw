---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
title: 自訂 DataList 的編輯介面（C#） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將為 DataList 建立更豐富的編輯介面，其中一個包含 Dropdownlist 進行和一個核取方塊。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: a5d13067-ddfb-4c36-8209-0f69fd40e45c
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 81f5a7f6737f544f577447f263dbd37dbc8279d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78594119"
---
# <a name="customizing-the-datalists-editing-interface-c"></a>自訂 DataList 的編輯介面 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_CS.exe)或[下載 PDF](customizing-the-datalist-s-editing-interface-cs/_static/datatutorial40cs1.pdf)

> 在本教學課程中，我們將為 DataList 建立更豐富的編輯介面，其中一個包含 Dropdownlist 進行和一個核取方塊。

## <a name="introduction"></a>簡介

DataList s 中的標記和 Web 控制項 `EditItemTemplate` 定義其可編輯的介面。 在我們最近檢查過的所有可編輯的 DataList 範例中，可編輯的介面已由 TextBox Web 控制群組成。 在[先前的教學](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)課程中，我們藉由新增驗證控制項來改善編輯時間使用者體驗。

`EditItemTemplate` 可以進一步擴充以包含文字方塊以外的 Web 控制項，例如 Dropdownlist 進行、RadioButtonLists、行事曆等等。 如同文字方塊，當自訂編輯介面以包含其他 Web 控制項時，請採用下列步驟：

1. 將 Web 控制項新增至 `EditItemTemplate`。
2. 使用資料系結語法，將對應的資料欄值指派給適當的屬性。
3. 在 `UpdateCommand` 事件處理常式中，以程式設計方式存取 Web 控制值，並將它傳遞至適當的 BLL 方法。

在本教學課程中，我們將為 DataList 建立更豐富的編輯介面，其中一個包含 Dropdownlist 進行和一個核取方塊。 特別是，我們將建立一個 DataList 來列出產品資訊，並允許更新產品的名稱、供應商、類別和已停止的狀態（請參閱 [圖 1]）。

[![編輯介面包含文字方塊、兩個 Dropdownlist 進行和一個核取方塊](customizing-the-datalist-s-editing-interface-cs/_static/image2.png)](customizing-the-datalist-s-editing-interface-cs/_static/image1.png)

**圖 1**：編輯介面包含文字方塊、兩個 dropdownlist 進行和一個核取方塊（[按一下以查看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image3.png)）

## <a name="step-1-displaying-product-information"></a>步驟1：顯示產品資訊

我們必須先建立唯讀介面，才可以建立 DataList 的可編輯介面。 一開始，從 [`EditDeleteDataList`] 資料夾開啟 [`CustomizedUI.aspx`] 頁面，然後從設計工具的 [將 DataList 加入至] 頁面，將其 `ID` 屬性設定為 [`Products`]。 從 DataList s 智慧標籤中，建立新的 ObjectDataSource。 將這個新的 ObjectDataSource 命名為 `ProductsDataSource`，並將它設定為從 `ProductsBLL` 類別 s `GetProducts` 方法中取出資料。 如同先前可編輯的 DataList 教學課程，我們將直接前往商務邏輯層來更新已編輯的產品的資訊。 因此，請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![將 [更新]、[插入] 和 [刪除] 索引標籤下拉式清單設定為 [（無）]](customizing-the-datalist-s-editing-interface-cs/_static/image5.png)](customizing-the-datalist-s-editing-interface-cs/_static/image4.png)

**圖 2**：將 [更新]、[插入] 和 [刪除] 索引標籤下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image6.png)）

設定 ObjectDataSource 之後，Visual Studio 會為 DataList 建立預設 `ItemTemplate`，其中列出每個傳回之資料欄位的名稱和值。 修改 `ItemTemplate`，讓範本在 `<h4>` 元素中列出產品名稱，以及分類名稱、供應商名稱、價格和已停止狀態。 此外，新增 [編輯] 按鈕，確定其 [`CommandName`] 屬性已設定為 [編輯]。 我的 `ItemTemplate` 的宣告式標記如下所示：

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

上述標記會使用產品 s 名稱的 &lt;h4&gt; 標題，以及其餘欄位的四個數據行 `<table>` 來配置產品資訊。 在先前的教學課程中，已討論 `Styles.css`中定義的 `ProductPropertyLabel` 和 `ProductPropertyValue` CSS 類別。 [圖 3] 顯示透過瀏覽器觀看的進度。

[會顯示每個產品的名稱、供應商、類別、已停止狀態和價格 ![](customizing-the-datalist-s-editing-interface-cs/_static/image8.png)](customizing-the-datalist-s-editing-interface-cs/_static/image7.png)

[**圖 3**] 顯示每項產品的名稱、供應商、類別、已停用狀態和價格（[按一下以觀看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image9.png)）

## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>步驟2：將 Web 控制項加入至編輯介面

建立自訂 DataList 編輯介面的第一個步驟，是將所需的 Web 控制項新增至 `EditItemTemplate`。 特別是，我們需要類別的 DropDownList、供應商的另一個，以及已停止狀態的核取方塊。 因為此範例中的產品價格無法編輯，所以我們可以使用標籤 Web 控制項繼續顯示。

若要自訂編輯介面，請按一下 DataList s 智慧標籤中的 [編輯範本] 連結，然後從下拉式清單中選擇 [`EditItemTemplate`] 選項。 將 DropDownList 新增至 `EditItemTemplate`，並將其 `ID` 設定為 [`Categories`]。

[![新增類別的 DropDownList](customizing-the-datalist-s-editing-interface-cs/_static/image11.png)](customizing-the-datalist-s-editing-interface-cs/_static/image10.png)

**圖 4**：新增類別的 DropDownList （[按一下以觀看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image12.png)）

接下來，從 DropDownList s 智慧標籤中，選取 [選擇資料來源] 選項，然後建立名為 `CategoriesDataSource`的新 ObjectDataSource。 設定此 ObjectDataSource 以使用 `CategoriesBLL` 類別的 `GetCategories()` 方法（請參閱 [圖 5]）。 接下來，DropDownList 的資料來源設定 Wizard 會提示您輸入每個 `ListItem` s `Text` 和 `Value` 屬性的資料欄位。 讓 DropDownList 顯示 `CategoryName` 資料欄位，並使用 `CategoryID` 作為值，如 [圖 6] 所示。

[![建立名為 CategoriesDataSource 的新 ObjectDataSource](customizing-the-datalist-s-editing-interface-cs/_static/image14.png)](customizing-the-datalist-s-editing-interface-cs/_static/image13.png)

**圖 5**：建立名為 `CategoriesDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image15.png)）

[![設定 DropDownList s 顯示和值欄位](customizing-the-datalist-s-editing-interface-cs/_static/image17.png)](customizing-the-datalist-s-editing-interface-cs/_static/image16.png)

**圖 6**：設定 DropDownList s 顯示和值欄位（[按一下以觀看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image18.png)）

重複這一系列的步驟，為供應商建立 DropDownList。 將此 DropDownList 的 `ID` 設定為 `Suppliers`，並將其 ObjectDataSource `SuppliersDataSource`命名為。

新增兩個 Dropdownlist 進行之後，針對 [已停止] 狀態新增一個核取方塊，並為 [產品名稱] 加入一個文字方塊。 將 CheckBox 和 TextBox 的 [`ID`] 分別設定為 [`Discontinued`] 和 [`ProductName`]。 新增 RequiredFieldValidator，以確保使用者提供產品的名稱值。

最後，新增 [更新] 和 [取消] 按鈕。 請記住，在這兩個按鈕中，其 `CommandName` 屬性必須分別設定為 [更新] 和 [取消]。

您可以視需要隨意配置編輯介面。 我選擇從唯讀介面使用相同的四個數據行 `<table>` 版面配置，如下列宣告式語法和螢幕擷取畫面所示：

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample2.aspx)]

[![編輯介面的配置方式類似唯讀介面](customizing-the-datalist-s-editing-interface-cs/_static/image20.png)](customizing-the-datalist-s-editing-interface-cs/_static/image19.png)

**圖 7**：編輯介面的配置方式就像唯讀介面（[按一下以觀看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image21.png)）

## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>步驟3：建立 EditCommand 和 CancelCommand 事件處理常式

目前，`EditItemTemplate` 中沒有任何資料系結語法（`UnitPriceLabel`除外，這是從 `ItemTemplate`的逐字複製而來）。 我們會一次加入資料系結語法，但會先讓建立 DataList s `EditCommand` 的事件處理常式，並 `CancelCommand` 事件。 回想一下，`EditCommand` 事件處理常式的責任是針對已按下 [編輯] 按鈕的 DataList 專案轉譯編輯介面，而 `CancelCommand` 的工作是將 DataList 傳回其預先編輯狀態。

建立這兩個事件處理常式，並使用下列程式碼：

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample3.cs)]

當這兩個事件處理常式就緒時，按一下 [編輯] 按鈕會顯示編輯介面，然後按一下 [取消] 按鈕，會將編輯過的專案傳回其唯讀模式。 [圖 8] 顯示在按下 [編輯] 按鈕以進行 Chef Anton s Gumbo Mix 之後的 DataList。 由於我們尚未將任何資料系結語法加入至編輯介面，`ProductName` 的 TextBox 是空白的，未核取 [`Discontinued`] 核取方塊，而是從 `Categories` 和 `Suppliers` Dropdownlist 進行中選取的第一個專案。

[![按一下 [編輯] 按鈕會顯示編輯介面](customizing-the-datalist-s-editing-interface-cs/_static/image23.png)](customizing-the-datalist-s-editing-interface-cs/_static/image22.png)

**圖 8**：按一下 [編輯] 按鈕會顯示編輯介面（[按一下以查看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image24.png)）

## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>步驟4：將資料系結語法加入至編輯介面

若要讓編輯介面顯示目前的產品值，我們需要使用資料系結語法，將資料欄值指派給適當的 Web 控制項值。 資料系結語法可以透過設計工具套用，方法是前往 [編輯範本] 畫面，然後從 [Web 控制項] 智慧標籤選取 [編輯資料系結] 連結。 或者，您可以將資料系結語法直接加入至宣告式標記中。

將 `ProductName` 資料欄 值指派給 `ProductName` TextBox s `Text` 屬性、`CategoryID` 和 `SupplierID` 欄位的值加入至 `Categories` 和 `Suppliers` `SelectedValue` 屬性，並將 `Discontinued` 欄位值指定為 `Discontinued` 核取方塊 `Checked` 屬性。 在進行這些變更之後（不論是透過設計工具或直接透過宣告式標記），請透過瀏覽器回顧頁面，然後按一下 [Chef Anton s Gumbo Mix] 的 [編輯] 按鈕。 如 [圖 9] 所示，資料系結語法已將目前的值加入文字方塊、Dropdownlist 進行和核取方塊。

[![按一下 [編輯] 按鈕會顯示編輯介面](customizing-the-datalist-s-editing-interface-cs/_static/image26.png)](customizing-the-datalist-s-editing-interface-cs/_static/image25.png)

**圖 9**：按一下 [編輯] 按鈕會顯示編輯介面（[按一下以查看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image27.png)）

## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>步驟5：在 UpdateCommand 事件處理常式中儲存使用者的變更

當使用者編輯產品並按一下 [更新] 按鈕時，就會發生回傳，而 DataList s `UpdateCommand` 事件會引發。 在事件處理常式中，我們需要從 `EditItemTemplate` 中的 Web 控制項讀取值，並使用 BLL 介面來更新資料庫中的產品。 如先前的教學課程中所見，已更新產品的 `ProductID` 可透過 `DataKeys` 集合來存取。 使用者輸入的欄位是使用 `FindControl("controlID")`以程式設計方式參考 Web 控制項所存取，如下列程式碼所示：

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample4.cs)]

程式碼一開始會先查閱 `Page.IsValid` 屬性，以確保網頁上的所有驗證控制項都是有效的。 如果 `True``Page.IsValid`，就會從 `DataKeys` 集合讀取已編輯的產品 s `ProductID` 值，並以程式設計方式參考 `EditItemTemplate` 中的資料輸入 Web 控制項。 接下來，這些 Web 控制項的值會讀入變數中，然後傳遞至適當的 `UpdateProduct` 多載。 更新資料之後，DataList 會回到其預先編輯狀態。

> [!NOTE]
> 我省略了在[處理 BLL 和 DAL 層級的例外](handling-bll-and-dal-level-exceptions-cs.md)狀況教學課程中新增的例外狀況處理邏輯，以便讓程式碼和此範例獲得焦點。 做為練習，請在完成本教學課程之後加入這種功能。

## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>步驟6：處理 Null 類別 Id 和已供應值

Northwind 資料庫允許 `Products` 資料表 s `CategoryID` 和 `SupplierID` 資料行的 `NULL` 值。 不過，我們的編輯介面目前不會容納 `NULL` 值。 如果我們嘗試編輯的產品具有 `CategoryID` 或 `SupplierID` 資料行的 `NULL` 值，我們將會 `ArgumentOutOfRangeException` 收到類似以下的錯誤訊息：「*分類」有一個不正確 SelectedValue，因為它不存在於專案清單中。* 此外，目前沒有任何方法可將產品的類別或供應商值從非`NULL` 值變更為 `NULL` 一。

若要支援類別和供應商 Dropdownlist 進行的 `NULL` 值，我們需要新增額外的 `ListItem`。 我選擇使用（無）做為此 `ListItem`的 `Text` 值，但如果您想要的話，可以將它變更為其他專案（例如空字串）。 最後，請記得將 Dropdownlist 進行 `AppendDataBoundItems` 設定為 `True`;如果您忘記這麼做，系結至 DropDownList 的類別和供應商將會覆寫靜態新增的 `ListItem`。

進行這些變更之後，DataList s `EditItemTemplate` 中的 Dropdownlist 進行標記看起來應該如下所示：

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample5.aspx)]

> [!NOTE]
> 您可以透過設計工具或直接透過宣告式語法，將靜態 `ListItem` 新增至 DropDownList。 當加入 DropDownList 專案來代表資料庫 `NULL` 值時，請務必透過宣告式語法加入 `ListItem`。 如果您在設計工具中使用 [`ListItem` 集合編輯器]，則產生的宣告式語法會在指派空白字串時完全省略 `Value` 設定，並建立如下的宣告式標記： `<asp:ListItem>(None)</asp:ListItem>`。 雖然這看起來可能無害，但遺漏的 `Value` 會導致 DropDownList 在其位置使用 `Text` 屬性值。 這表示如果選取此 `NULL` `ListItem`，則會嘗試將值（無）指派給產品資料欄位（在本教學課程中為`CategoryID` 或 `SupplierID`），這會導致例外狀況。 藉由明確地設定 `Value=""`，當選取 `NULL` `ListItem` 時，`NULL` 值會指派給 [產品資料] 欄位。

請花點時間透過瀏覽器來查看進度。 編輯產品時，請注意，在 DropDownList 的開頭，`Categories` 和 `Suppliers` Dropdownlist 進行兩者都有（無）選項。

[![[類別和供應商] Dropdownlist 進行包含 [（無）] 選項](customizing-the-datalist-s-editing-interface-cs/_static/image29.png)](customizing-the-datalist-s-editing-interface-cs/_static/image28.png)

**圖 10**： [`Categories`] 和 [`Suppliers`] dropdownlist 進行包括 [（無）] 選項（[按一下以查看完整大小的影像](customizing-the-datalist-s-editing-interface-cs/_static/image30.png)）

若要將（None）選項儲存為資料庫 `NULL` 值，我們必須回到 `UpdateCommand` 事件處理常式。 將 `categoryIDValue` 和 `supplierIDValue` 變數變更為可為 null 的整數，並為它們指派只有在 DropDownList s `SelectedValue` 不是空字串時 `Nothing` 的值：

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample6.cs)]

透過這項變更，如果使用者從任何下拉式清單中選取 [（無）] 選項（對應至 `NULL` 資料庫值），則 `Nothing` 的值將會傳遞至 `UpdateProduct` 的 BLL 方法。

## <a name="summary"></a>總結

在本教學課程中，我們已瞭解如何建立更複雜的 DataList 編輯介面，其中包含三個不同的輸入 Web 控制項： TextBox、兩個 Dropdownlist 進行和一個核取方塊，以及驗證控制項。 建立編輯介面時，不論使用的 Web 控制項為何，步驟都相同：首先將 Web 控制項新增至 DataList s `EditItemTemplate`;使用資料系結語法，以適當的 Web 控制項屬性指派對應的資料欄位值。然後，在 `UpdateCommand` 事件處理常式中，以程式設計方式存取 Web 控制項及其適當的屬性，並將其值傳遞到 BLL 中。

當您建立編輯介面時，不論是由文字方塊還是不同 Web 控制項的集合所組成，請務必正確處理資料庫 `NULL` 值。 當 `NULL` 的會計時，您不一定要在編輯介面中正確顯示現有的 `NULL` 值，但您也可以提供將值標示為 `NULL`的方法。 對於 DataLists 中的 Dropdownlist 進行，這通常表示加入靜態 `ListItem`，其 `Value` 屬性已明確設定為空字串（`Value=""`），並將程式碼新增至 `UpdateCommand` 事件處理常式，以判斷是否已選取 `NULL``ListItem`。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dennis Patterson、David Suru 和 Randy Schmidt。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
> [下一頁](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
