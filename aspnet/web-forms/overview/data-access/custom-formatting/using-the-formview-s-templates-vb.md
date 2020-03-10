---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: 使用 FormView 的範本（VB） |Microsoft Docs
author: rick-anderson
description: 與 DetailsView 不同的是，FormView 不是由欄位所組成。 取而代之的是，會使用範本來轉譯 FormView。 在本教學課程中，我們將使用 F 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: cafe47cf5766bb14503852ec6e9f305d1e6d426f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78531161"
---
# <a name="using-the-formviews-templates-vb"></a>使用 FormView 的範本（VB）

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe)或[下載 PDF](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)

> 與 DetailsView 不同的是，FormView 不是由欄位所組成。 取而代之的是，會使用範本來轉譯 FormView。 在本教學課程中，我們將探討如何使用 FormView 控制項來呈現較不嚴格的資料顯示。

## <a name="introduction"></a>簡介

在最後兩個教學課程中，我們已看到如何使用 TemplateFields 自訂 GridView 和 DetailsView 控制項的輸出。 TemplateFields 允許對特定欄位的內容進行高度自訂，但在同時結束 GridView 和 DetailsView 時，會有相當 boxy、類似方格的外觀。 在許多情況下，這類類似方格的配置是理想的，但有時需要更流暢、較不嚴格的顯示。 顯示單一記錄時，可以使用 FormView 控制項來進行這類流暢的版面配置。

與 DetailsView 不同的是，FormView 不是由欄位所組成。 您無法將 BoundField 或 TemplateField 加入至 FormView。 取而代之的是，會使用範本來轉譯 FormView。 將 FormView 視為包含單一 TemplateField 的 DetailsView 控制項。 FormView 支援下列範本：

- `ItemTemplate` 用來轉譯 FormView 中所顯示的特定記錄
- `HeaderTemplate` 用來指定選擇性的標頭資料列
- `FooterTemplate` 用來指定選擇性的頁尾資料列
- `EmptyDataTemplate` 當 FormView 的 `DataSource` 缺少任何記錄時，會使用 `EmptyDataTemplate` 取代 `ItemTemplate` 來呈現控制項的標記
- `PagerTemplate` 可以用來自訂已啟用分頁之 FormViews 的分頁介面
- `EditItemTemplate` / `InsertItemTemplate` 用來自訂編輯介面或為支援這類功能的 FormViews 插入介面

在本教學課程中，我們將探討如何使用 FormView 控制項來呈現較不嚴格的產品顯示。 FormView 的 `ItemTemplate` 會使用標頭元素和 `<table>` 的組合來顯示這些值（請參閱 [圖 1]），而不是擁有名稱、類別目錄、供應商等欄位。

[![在 DetailsView 中看到的 FormView 分成類似方格的版面配置](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)

**圖 1**： FormView 在 DetailsView 中分成類似方格的版面配置（[按一下以觀看完整大小的影像](using-the-formview-s-templates-vb/_static/image3.png)）

## <a name="step-1-binding-the-data-to-the-formview"></a>步驟1：將資料系結至 FormView

開啟 [`FormView.aspx`] 頁面，並將 [FormView] 從 [工具箱] 拖曳至設計工具。 第一次新增 FormView 時，它會顯示為灰色方塊，指示我們需要 `ItemTemplate`。

[![在提供 ItemTemplate 之前，無法在設計工具中轉譯 FormView](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)

**圖 2**：在提供 `ItemTemplate` 之前，無法在設計工具中轉譯 FormView （[按一下以查看完整大小的影像](using-the-formview-s-templates-vb/_static/image6.png)）

`ItemTemplate` 可以手動建立（透過宣告式語法），也可以透過設計工具將 FormView 系結至資料來源控制項來自動建立。 這個自動建立的 `ItemTemplate` 包含 HTML，其中列出每個欄位的名稱，以及其 `Text` 屬性系結至域值的標籤控制項。 這個方法也會自動建立 `InsertItemTemplate` 和 `EditItemTemplate`，這兩者都是針對資料來源控制項所傳回的每個資料欄位，以輸入控制項填入。

如果您想要自動建立範本，請從 FormView 的智慧標籤加入一個叫用 `ProductsBLL` 類別之 `GetProducts()` 方法的新 ObjectDataSource 控制項。 這會建立具有 `ItemTemplate`、`InsertItemTemplate`和 `EditItemTemplate`的 FormView。 從來源視圖移除 `InsertItemTemplate` 並 `EditItemTemplate`，因為我們不想要建立支援編輯或插入的 FormView。 接下來，清除 `ItemTemplate` 內的標記，讓我們有一個可供使用的乾淨平板電腦。

如果您想要手動建立 `ItemTemplate`，可以將它從 [工具箱] 拖曳至設計工具來加入和設定 ObjectDataSource。 不過，請不要從設計工具設定 FormView 的資料來源。 改為移至來源視圖，並手動將 FormView 的 `DataSourceID` 屬性設定為 ObjectDataSource 的 `ID` 值。 接下來，手動新增 `ItemTemplate`。

無論您決定採取哪一種方法，此時您的 FormView 宣告式標記看起來應該像這樣：

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

請花點時間檢查 FormView 的智慧標籤中的 [啟用分頁] 核取方塊;這會將 `AllowPaging="True"` 屬性加入至 FormView 的宣告式語法。 此外，請將 `EnableViewState` 屬性設定為 False。

## <a name="step-2-defining-theitemtemplates-markup"></a>步驟2：定義`ItemTemplate`的標記

當 FormView 系結至 ObjectDataSource 控制項並設定為支援分頁時，我們就可以指定 `ItemTemplate`的內容。 在本教學課程中，讓我們將產品的名稱顯示在 `<h3>` 標題中。 接下來，讓我們使用 HTML `<table>` 將其餘的產品屬性顯示在四個數據行的資料表中，其中第一個和第三個數據行列出屬性名稱，而第二個和第四個欄位列出其值。

此標記可以透過設計工具中的 FormView 範本編輯介面輸入，或透過宣告式語法手動輸入。 使用範本時，通常會發現直接使用宣告式語法會比較快速，但是您可以隨意使用您最熟悉的任何技術。

下列標記顯示在 `ItemTemplate`的結構完成後的 FormView 宣告式標記：

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

請注意，資料系結語法 `<%# Eval("ProductName") %>`，例如可以直接插入範本的輸出中。 也就是說，它不需要指派給標籤控制項的 `Text` 屬性。 例如，我們的 `ProductName` 值會使用 `<h3><%# Eval("ProductName") %></h3>`顯示在 `<h3>` 元素中，而產品 Chai 會以 `<h3>Chai</h3>`呈現。

`ProductPropertyLabel` 和 `ProductPropertyValue` CSS 類別是用來指定 `<table>`中的產品屬性名稱和值的樣式。 這些 CSS 類別是在 `Styles.css` 中定義，而且會讓屬性名稱為粗體和靠右對齊，並在屬性值中加上右填補。

由於 FormView 沒有可用的 CheckBoxFields，為了將 `Discontinued` 值顯示為 checkbox，我們必須新增自己的 CheckBox 控制項。 `Enabled` 屬性設為 False，使其成為唯讀，核取方塊的 `Checked` 屬性會系結至 `Discontinued` 資料欄位的值。

`ItemTemplate` 完成後，產品資訊會以更流暢的方式顯示。 比較上一個教學課程（圖3）中的 DetailsView 輸出與 FormView 在本教學課程中產生的輸出（圖4）。

[![嚴格的 DetailsView 輸出](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)

**圖 3**：固定 DetailsView 輸出（[按一下以查看完整大小的影像](using-the-formview-s-templates-vb/_static/image9.png)）

[![流體的 FormView 輸出](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)

**圖 4**：流體的 FormView 輸出（[按一下以觀看完整大小的影像](using-the-formview-s-templates-vb/_static/image12.png)）

## <a name="summary"></a>總結

雖然 GridView 和 DetailsView 控制項可以使用 TemplateFields 自訂其輸出，但仍會以類似方格的 boxy 格式呈現其資料。 針對需要使用較不嚴格的配置來顯示單一記錄的時間，FormView 是理想的選擇。 就像 DetailsView 一樣，FormView 會從它的 `DataSource`轉譯一筆記錄，但與 DetailsView 不同的是，它只是由範本組成，不支援欄位。

如我們在本教學課程中所見，FormView 可在顯示單一記錄時提供更有彈性的版面配置。 在未來的教學課程中，我們將檢查 DataList 和重複項控制項，其提供與 FormsView 相同的彈性層級，但是能夠顯示多筆記錄（例如 GridView）。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者已 E.R。 Gilmore. 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](using-templatefields-in-the-detailsview-control-vb.md)
> [下一頁](displaying-summary-information-in-the-gridview-s-footer-vb.md)
