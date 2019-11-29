---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
title: 使用 DataList 控制項（C#）顯示每個資料列的多筆記錄 |Microsoft Docs
author: rick-anderson
description: 在這個簡短的教學課程中，我們將探討如何透過其 RepeatColumns 和 RepeatDirection 屬性自訂 DataList 的版面配置。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: cf5acaf5-d4f6-4957-badc-b89956b285f3
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3280a7b5f28207d3e640a6480f47869ce19692bc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74638632"
---
# <a name="showing-multiple-records-per-row-with-the-datalist-control-c"></a>使用 DataList 控制項在每個資料列顯示多筆記錄 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_CS.exe)或[下載 PDF](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/datatutorial31cs1.pdf)

> 在這個簡短的教學課程中，我們將探討如何透過其 RepeatColumns 和 RepeatDirection 屬性自訂 DataList 的版面配置。

## <a name="introduction"></a>簡介

我們在過去兩個教學課程中看到的 DataList 範例，已將其資料來源中的每筆記錄轉譯為單一資料行 HTML `<table>`中的一列。 雖然這是預設的 DataList 行為，但是很容易就能自訂 DataList 顯示，讓資料來源專案散佈到多資料行的多重資料列資料表。 此外，也可以將所有資料來源專案顯示在單一資料列、多資料行的 DataList 中。

我們可以透過其 `RepeatColumns` 和 `RepeatDirection` 屬性來自訂 DataList 的版面配置，分別指出要轉譯的資料行數目，以及這些專案是以垂直或水準方式配置。 例如，[圖 1] 顯示的 DataList 會在具有三個數據行的資料表中顯示產品資訊。

[![DataList 會顯示每個資料列三個產品](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image1.png)

**圖 1**： DataList 會顯示每個資料列三個產品（[按一下以查看完整大小的影像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image3.png)）

藉由顯示每列的多個資料來源專案，DataList 可以更有效地利用水準螢幕空間。 在這個簡短的教學課程中，我們將探討這兩個 DataList 屬性。

## <a name="step-1-displaying-product-information-in-a-datalist"></a>步驟1：在 DataList 中顯示產品資訊

在檢查 `RepeatColumns` 和 `RepeatDirection` 屬性之前，請先在頁面上建立 DataList，其中會使用標準的單一資料行、多列資料表配置來列出產品資訊。 在此範例中，讓我們使用下列標記來顯示產品的名稱、類別和價格：

[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample1.html)]

我們已瞭解如何在先前的範例中將資料系結至 DataList，因此我將快速完成這些步驟。 一開始先開啟 [`DataListRepeaterBasics`] 資料夾中的 [`RepeatColumnAndDirection.aspx`] 頁面，然後從 [工具箱] 將 [DataList] 拖曳至設計工具。 從 DataList 的智慧標籤選擇建立新的 ObjectDataSource，並將其設定為從 `ProductsBLL` 類別的 `GetProducts` 方法提取其資料，從 wizard 的 [插入]、[更新] 和 [刪除] 索引標籤中選擇 [（無）] 選項。

在建立新的 ObjectDataSource 並將其系結至 DataList 之後，Visual Studio 會自動建立 `ItemTemplate`，以顯示每個產品資料欄位的名稱和值。 直接透過宣告式標記或從 DataList s 智慧標籤中的 [編輯範本] 選項來調整 `ItemTemplate`，讓它使用上述標記，將*產品名稱*、*類別名稱*和*價格*文字取代為使用適當的資料系結語法將值指派給其 `Text` 屬性的標籤控制項。 更新 `ItemTemplate`之後，您的頁面宣告式標記看起來應該如下所示：

[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample2.aspx)]

請注意，我在 `UnitPrice`的 `Eval` 資料系結語法中包含格式規範，並將傳回的值格式化為貨幣-`Eval("UnitPrice", "{0:C}").`

請花點時間造訪瀏覽器中的頁面。 如 [圖 2] 所示，DataList 轉譯為單一資料行、多列的產品資料表。

[![根據預設，DataList 會轉譯為單一資料行、多個資料列的資料表](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image4.png)

**圖 2**：根據預設，DataList 會轉譯為單一資料行、多個資料列的資料表（[按一下以查看完整大小的影像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image6.png)）

## <a name="step-2-changing-the-datalist-s-layout-direction"></a>步驟2：變更 DataList s 版面配置方向

雖然 DataList 的預設行為是在單一資料行、多個資料列的資料表中垂直配置其專案，但您可以透過 DataList s [`RepeatDirection` 屬性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)輕鬆地變更此行為。 `RepeatDirection` 屬性可以接受兩個可能值的其中一個： `Horizontal` 或 `Vertical` （預設）。

藉由將 `RepeatDirection` 屬性從 `Vertical` 變更為 `Horizontal`，DataList 會將其記錄轉譯為單一資料列，為每個資料來源專案建立一個資料行。 若要說明這種效果，請在設計工具中按一下 DataList，然後從 屬性視窗中，將 `RepeatDirection` 屬性從 `Vertical` 變更為 `Horizontal`。 在這麼做之後，設計工具會立即調整 DataList 的版面配置，建立單一資料列的多重資料行介面（請參閱 [圖 3]）。

[![RepeatDirection 屬性規定 DataList s 專案的配置方向](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image7.png)

**圖 3**： `RepeatDirection` 屬性會指示 DataList s 專案的配置方向（[按一下以查看完整大小的影像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image9.png)）

顯示少量資料時，單一資料列的多重資料行資料表可能是最大化螢幕資產的理想方式。 不過，對於較大的資料量，單一資料列將會需要許多資料行，這會將無法在螢幕上容納的專案，推播到右邊。 [圖 4] 顯示以單一資料列 DataList 呈現的產品。 由於有許多產品（超過80），使用者必須向右移動，才能查看每項產品的相關資訊。

[對於夠大的資料來源 ![，單一資料行 DataList 將需要水準滾動](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image10.png)

**圖 4**：如果是夠大的資料來源，單一資料行 DataList 將需要水準滾動（[按一下以查看完整大小的影像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image12.png)）

## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>步驟3：在多重資料行、多列資料表中顯示資料

若要建立多重資料行、多列 DataList，我們必須將[`RepeatColumns` 屬性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx)設定為要顯示的欄數。 根據預設，`RepeatColumns` 屬性會設定為0，這會使 DataList 在單一資料列或資料行中顯示其所有專案（視 `RepeatDirection` 屬性的值而定）。

在我們的範例中，我們會在每個資料表的資料列中顯示三個產品。 因此，請將 `RepeatColumns` 屬性設定為3。 進行這項變更之後，請花一點時間在瀏覽器中查看結果。 如 [圖 5] 所示，產品現在會列在三個數據行的多個資料列資料表中。

[每個資料列顯示 ![三個產品](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image13.png)

**圖 5**：每個資料列顯示三項產品（[按一下以觀看完整大小的影像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image15.png)）

`RepeatDirection` 屬性會影響 DataList 中專案的配置方式。[圖 5] 顯示 `RepeatDirection` 屬性設為 `Horizontal`的結果。 請注意，前三個產品 Chai、變更和 Aniseed Syrup 由左至右配置，由上到下。 接下來的三項產品（從 Chef Anton s Cajun Seasoning 開始）會出現在前三個底下的資料列中。 不過，將 `RepeatDirection` 屬性變更回 `Vertical`，從上到下，由左至右配置這些產品，如 [圖 6] 所示。

[![這裡，產品會以垂直方式配置](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image16.png)

**圖 6**：在此，產品會以垂直方式配置（[按一下以觀看完整大小的影像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image18.png)）

產生的資料表中顯示的資料列數目取決於系結至 DataList 的總記錄數目。 精確地說，這是資料來源專案總數的上限除以 `RepeatColumns` 屬性值。 由於 `Products` 資料表目前有84產品（可由3整除），因此有28個數據列。 如果資料來源中的專案數和 `RepeatColumns` 屬性值無法被整除，則最後一個資料列或資料行將會有空白資料格。 如果 `RepeatDirection` 設定為 `Vertical`，則最後一個資料行將會有空白的資料格;如果 `Horizontal``RepeatDirection`，則最後一個資料列會有空白的資料格。

## <a name="summary"></a>總結

根據預設，DataList 會在單一資料行的多重資料列資料表中列出其專案，這會以單一 TemplateField 模仿 GridView 的配置。 雖然此預設配置是可接受的，但我們可以顯示每個資料列的多個資料來源專案，以最大化螢幕畫面。 完成這項工作只是將 DataList s `RepeatColumns` 屬性設定為每個資料列要顯示的資料行數目。 此外，DataList s `RepeatDirection` 屬性可以用來指出多重資料行、多列資料表的內容是否應該從左至右、由上到下，或是從上到下、從左至右垂直配置。

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 John Suru。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
> [下一頁](nested-data-web-controls-cs.md)
