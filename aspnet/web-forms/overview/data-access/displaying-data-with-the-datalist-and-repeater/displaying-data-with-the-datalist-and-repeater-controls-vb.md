---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: 使用 DataList 和重複項控制項顯示資料（VB） |Microsoft Docs
author: rick-anderson
description: 在先前的教學課程中，我們使用了 GridView 控制項來顯示資料。 從本教學課程開始，我們將探討如何使用 ... 來建立一般報告模式
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 4e7aaa1701da67aec61505b64a835ef41031bb13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626361"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a>使用 DataList 與重複項控制項顯示資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe)或[下載 PDF](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)

> 在先前的教學課程中，我們使用了 GridView 控制項來顯示資料。 從本教學課程開始，我們將探討如何使用 DataList 和重複項控制項來建立常見的報告模式，從使用這些控制項顯示資料的基本概念開始。

## <a name="introduction"></a>簡介

在過去28個教學課程的所有範例中，如果我們需要從資料來源顯示多筆記錄，我們已轉換成 GridView 控制項。 GridView 會針對資料來源中的每一筆記錄轉譯一個資料列，並在資料行中顯示記錄的資料欄位。 當 GridView 讓它變成顯示、逐頁流覽、排序、編輯和刪除資料的貼齊時，其外觀會有點 boxy。 此外，負責 GridView s 結構的標記已修正，其中包括 HTML `<table>`，其中包含每筆記錄的資料表資料列（`<tr>`），以及每個欄位的資料表資料格（`<td>`）。

若要在顯示多筆記錄時，在外觀和轉譯的標記中提供較高的自訂程度，ASP.NET 2.0 提供 DataList 和重複項控制項（這兩者都在 ASP.NET 1.x 版中也有提供）。 DataList 和中繼器控制項會使用範本來呈現其內容，而不是 BoundFields、CheckBoxFields、ButtonFields 等等。 就像 GridView 一樣，DataList 會轉譯為 HTML `<table>`，但允許每個資料表的資料列顯示多個資料來源記錄。 另一方面，中繼器不會轉譯除了您明確指定的其他標記，而且當您需要精確控制所發出的標記時，這是理想的候選項。

在接下來的一或多個教學課程中，我們將探討如何使用 DataList 和重複項控制項來建立常見的報告模式，從使用這些控制項範本顯示資料的基本概念開始。 我們將瞭解如何格式化這些控制項、如何改變 DataList 中的資料來源記錄配置、常見的主要/詳細資料案例、編輯和刪除資料的方式、如何逐頁查看記錄等等。

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>步驟1：新增 DataList 和中繼器教學課程網頁

開始進行本教學課程之前，先讓我們先花點時間新增本教學課程所需的 ASP.NET 網頁，以及接下來的幾個教學課程，處理如何使用 DataList 和中繼器來顯示資料。 首先，在名為 `DataListRepeaterBasics`的專案中建立新的資料夾。 接下來，將下列五個 ASP.NET 網頁新增到此資料夾，並將它們全部設定為使用主版頁面 `Site.master`：

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`

![建立 DataListRepeaterBasics 資料夾並新增教學課程 ASP.NET 網頁](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

**圖 1**：建立 `DataListRepeaterBasics` 資料夾並新增教學課程 ASP.NET 網頁

開啟 [`Default.aspx`] 頁面，並將 [`SectionLevelTutorialListing.ascx` 使用者] 控制項從 [`UserControls`] 資料夾拖曳到設計介面上。 我們在[主版頁面和網站導覽](../introduction/master-pages-and-site-navigation-vb.md)教學課程中建立的這個使用者控制項，會列舉網站地圖，並從項目符號清單中的目前區段顯示教學課程。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png)）

為了讓項目符號清單顯示我們將建立的 DataList 和中繼器教學課程，我們需要將它們新增至網站地圖。 開啟 `Web.sitemap` 檔案，並在新增自訂按鈕的網站地圖節點標記之後，新增下列標記：

[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]

![更新網站地圖以包含新的 ASP.NET 網頁](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

**圖 3**：更新網站地圖以包含新的 ASP.NET 網頁

## <a name="step-2-displaying-product-information-with-the-datalist"></a>步驟2：使用 DataList 顯示產品資訊

與 FormView 類似，DataList 控制項的呈現輸出取決於範本，而不是 BoundFields、CheckBoxFields 等等。 不同于 FormView，DataList 的設計是用來顯示一組記錄，而不是單獨一筆。 讓我們開始本教學課程，並介紹如何將產品資訊系結至 DataList。 從開啟 [`DataListRepeaterBasics`] 資料夾中的 [`Basics.aspx`] 頁面開始。 接下來，從 [工具箱] 將 [DataList] 拖曳至設計工具。 如 [圖 4] 所示，在指定 DataList 的範本之前，設計工具會將其顯示為灰色方塊。

[![將 DataList 從 [工具箱] 拖曳至設計工具](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

**圖 4**：將 [DataList] 從工具箱拖曳至設計工具（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png)）

從 DataList s 智慧標籤中，加入新的 ObjectDataSource，並將其設定為使用 `ProductsBLL` 類別的 `GetProducts` 方法。 因為我們會在本教學課程中重新建立唯讀的 DataList，請在 wizard s 的 [插入]、[更新] 和 [刪除] 索引標籤中，將下拉式清單設定為 [（無）]。

[![選擇建立新的 ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

**圖 5**：選擇建立新的 ObjectDataSource （[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png)）

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

**圖 6**：設定 ObjectDataSource 使用 `ProductsBLL` 類別（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png)）

[![使用 GetProducts 方法取出所有產品的相關資訊](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

**圖 7**：使用 `GetProducts` 方法來抓取所有產品的相關資訊（[按一下以觀看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png)）

設定 ObjectDataSource 並透過其智慧標籤將它與 DataList 產生關聯之後，Visual Studio 會在 DataList 中自動建立 `ItemTemplate`，以顯示資料來源所傳回之每個資料欄位的名稱和值（請參閱下面的標記）。 這個預設 `ItemTemplate` 的外觀與透過設計工具將資料來源系結至 FormView 時，所自動建立的範本相同。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> 回想一下，透過 FormView s 智慧標籤將資料來源系結至 FormView 控制項時，Visual Studio 建立了 `ItemTemplate`、`InsertItemTemplate`和 `EditItemTemplate`。 不過，使用 DataList，只會建立 `ItemTemplate`。 這是因為 DataList 不具有與 FormView 所提供的相同內建編輯和插入支援。 DataList 包含編輯和刪除相關的事件，而編輯和刪除的支援可以使用一些程式碼來加入，但是沒有像 FormView 一樣的簡單現成支援。 在未來的教學課程中，我們將瞭解如何包含 DataList 的編輯和刪除支援。

讓我們花一點時間來改善此範本的外觀。 我們不會顯示所有的資料欄位，而是只顯示產品的名稱、供應商、類別、每單位數量和單價。 此外，讓 s 在 `<h4>` 標題中顯示名稱，並使用標題底下的 `<table>` 來配置其餘欄位。

若要進行這些變更，您可以從 DataList 的智慧標籤中使用設計工具中的範本編輯功能，按一下 [編輯範本] 連結，或者您可以透過頁面的宣告式語法手動修改範本。 如果您在設計工具中使用 [編輯範本] 選項，則產生的標記可能不會完全符合下列標記，但透過瀏覽器觀看時，看起來應該類似 [圖 8] 所示的螢幕擷取畫面。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> 上述範例會使用標籤 Web 控制項，其 `Text` 屬性指派給資料系結語法的值。 或者，我們可以完全省略標籤，只輸入資料系結語法。 也就是說，我們可以改為使用宣告式語法 `<%# Eval("CategoryName") %>`，而不是使用 `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />`。

不過，保留 Web 控制項的標籤會提供兩個優點。 首先，它會提供更簡單的方法，讓您根據資料來格式化資料，如我們在下一個教學課程中所見。 第二，設計工具中的 [編輯範本] 選項不會顯示出現在某個 Web 控制項外部的宣告式資料系結語法。 相反地，編輯範本介面是設計用來協助使用靜態標記和 Web 控制項，並假設任何資料系結都是透過 [編輯資料系結] 對話方塊來完成，這可從 Web 控制項智慧標籤存取。

因此，當使用 DataList （可提供透過設計工具編輯範本的選項）時，我偏好使用標籤 Web 控制項，以便透過 [編輯範本] 介面來存取內容。 如我們稍後所見，中繼器需要從來源視圖編輯範本的內容。 因此，在製作中繼器的範本時，我通常會省略標籤 Web 控制項，除非我知道，我必須根據程式設計邏輯來格式化資料系結文字的外觀。

[![每個產品的輸出都會使用 DataList s ItemTemplate 來呈現](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

**圖 8**：每個產品的輸出都會使用 DataList s `ItemTemplate` 來轉譯（[按一下以觀看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png)）

## <a name="step-3-improving-the-appearance-of-the-datalist"></a>步驟3：改善 DataList 的外觀

就像 GridView 一樣，DataList 也提供許多與樣式相關的屬性，例如 `Font`、`ForeColor`、`BackColor`、`CssClass`、`ItemStyle`、`AlternatingItemStyle`、`SelectedItemStyle`等等。 使用 GridView 和 DetailsView 控制項時，我們已在 `DataWebControls` 主題中建立了面板檔案，這些控制項預先定義了這兩個控制項的 `CssClass` 屬性，以及其中幾個子屬性的 `CssClass` 屬性（`RowStyle`、`HeaderStyle`等等）。 讓我們對 DataList 執行相同的動作。

如[使用 ObjectDataSource 顯示資料](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)教學課程中所述，外觀檔案會指定 Web 控制項的預設面板相關屬性。主題是面板、CSS、影像和 JavaScript 檔案的集合，這些檔案會定義網站的特定外觀與風格。 在*使用 ObjectDataSource 顯示資料*教學課程中，我們建立了一個 `DataWebControls` 主題（它會實作為 `App_Themes` 資料夾內的資料夾），其中目前有兩個外觀檔案 `GridView.skin` 和 `DetailsView.skin`。 讓我們加入第三個外觀檔案，以指定 DataList 的預先定義樣式設定。

若要新增面板檔案，請以滑鼠右鍵按一下 [`App_Themes/DataWebControls`] 資料夾，選擇 [加入新專案]，然後從清單中選取 [外觀檔案] 選項。 開啟 `DataList.skin` 檔案。

[![建立名為 DataList. 面板的新外觀檔案](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

**圖 9**：建立名為 `DataList.skin` 的新外觀檔案（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png)）

針對 `DataList.skin` 檔案，請使用下列標記：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

這些設定會將相同的 CSS 類別指派給適當的 DataList 屬性，如同與 GridView 和 DetailsView 控制項一起使用一樣。 此處所使用的 CSS 類別 `DataWebControlStyle`、`AlternatingRowStyle`、`RowStyle`等等都是在 `Styles.css` 檔案中定義，並已在先前的教學課程中新增。

加入此面板檔案後，DataList 的外觀會在設計工具中更新（您可能需要重新整理設計工具視圖，才能看到新的外觀檔的效果，請從 [View] 功能表選擇 [Refresh]）。 如 [圖 10] 所示，每個交替產品都有淺粉色的背景色彩。

[![建立名為 DataList. 面板的新外觀檔案](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

**圖 10**：建立名為 `DataList.skin` 的新外觀檔案（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png)）

## <a name="step-4-exploring-the-datalist-s-other-templates"></a>步驟4：流覽 DataList 的其他範本

除了 `ItemTemplate`以外，DataList 還支援其他六個選擇性範本：

- `HeaderTemplate` 如有提供，則會將標頭資料列新增至輸出，並用來呈現此資料列
- 用來呈現替代專案的 `AlternatingItemTemplate`
- `SelectedItemTemplate` 用來呈現選取的專案;選取的專案是其索引對應至 DataList s [`SelectedIndex` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)的專案
- 用來呈現正在編輯之專案的 `EditItemTemplate`
- `SeparatorTemplate` 如有提供，會在每個專案之間新增分隔符號，並用來呈現此分隔符號
- `FooterTemplate`-如果有提供，會將頁尾資料列新增至輸出，並用來呈現此資料列

當指定 `HeaderTemplate` 或 `FooterTemplate`時，DataList 會將額外的頁首或頁尾資料列加入轉譯的輸出中。 就像 GridView 的頁首和頁尾資料列一樣，DataList 中的頁首和頁尾並不會系結至資料。 因此，嘗試存取系結資料之 `HeaderTemplate` 或 `FooterTemplate` 中的任何資料系結語法都會傳回空白字串。

> [!NOTE]
> 如我們在[gridview 的頁尾中顯示摘要資訊](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)教學課程中所見，當頁首和頁尾資料列不支援 databinding 語法時，可以從 GridView 的 `RowDataBound` 事件處理常式中，將資料特有的資訊直接插入這些資料列。 這項技術可以用來從系結至控制項的資料計算執行總計或其他資訊，以及將該資訊指派給頁尾。 這個相同的概念可以套用至 DataList 和中繼器控制項;唯一的不同之處在于，DataList 和中繼器會建立 `ItemDataBound` 事件的事件處理常式（而不是 `RowDataBound` 事件的）。

在我們的範例中，讓在 DataList 的頂端顯示的標題產品資訊會產生 `<h3>` 標題。 若要完成此動作，請新增具有適當標記的 `HeaderTemplate`。 從設計工具中，按一下 [DataList] 智慧標籤中的 [編輯範本] 連結，從下拉式清單中選擇 [標題] 範本，然後在 [樣式] 下拉式清單中挑選 [標題 3] 選項之後輸入文字，即可完成這項作業（請參閱 [圖 11]）。

[![新增包含文字產品資訊的 System.windows.controls.headereditemscontrol.headertemplate](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

**圖 11**：新增包含文字產品資訊的 `HeaderTemplate` （[按一下以觀看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png)）

或者，您也可以在 `<asp:DataList>` 標籤內輸入下列標記，以宣告方式新增：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

若要在每個產品清單之間加上一個空格，請在每個區段之間加入一個包含一行的 `SeparatorTemplate`。 水準規則標記（`<hr>`）會加入這類分割線。 建立 `SeparatorTemplate`，使其具有下列標記：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> 就像 `HeaderTemplate` 和 `FooterTemplates`，`SeparatorTemplate` 不會系結至資料來源中的任何記錄，因此無法直接存取系結至 DataList 的資料來源記錄。

進行這種新增之後，透過瀏覽器來觀看頁面時，看起來應該類似 [圖 12]。 請注意標頭資料列，以及每個產品清單之間的線條。

[![DataList 包括標頭資料列，以及每個產品清單之間的水準規則](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

**圖 12**： DataList 包含標頭資料列，以及每個產品清單之間的水準規則（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png)）

## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>步驟5：使用重複項控制項呈現特定標記

當您造訪 [圖 12] 中的 DataList 範例時，如果您從瀏覽器執行視圖/來源，您會看到 DataList 發出 HTML `<table>`，其中包含一個資料表資料列（`<tr>`），其中每個系結至 DataList 的專案都有一個資料表資料格（`<td>`）。 事實上，這項輸出與使用單一 TemplateField 從 GridView 發出的結果相同。 如我們在未來的教學課程中所見，DataList 確實允許進一步自訂輸出，讓我們能夠顯示每個資料表資料列的多個資料來源記錄。

不過，如果您不想發出 HTML `<table>`，該怎麼做？ 對於資料 Web 控制項所產生之標記的總計和完整控制，我們必須使用中繼器控制項。 就像 DataList，會根據範本來建造中繼器。 不過，中繼器只提供下列五個範本：

- `HeaderTemplate` 如有提供，則會在專案之前新增指定的標記
- 用來呈現專案的 `ItemTemplate`
- `AlternatingItemTemplate` （若有提供），用來呈現替代專案
- `SeparatorTemplate` 如有提供，會在每個專案之間新增指定的標記
- `FooterTemplate`-如果提供，會在專案之後加入指定的標記

在 ASP.NET 1.x 中，重複項控制項通常用來顯示項目符號清單，其資料來自某個資料來源。 在這種情況下，`HeaderTemplate` 和 `FooterTemplates` 會分別包含開頭和結尾 `<ul>` 標記，而 `ItemTemplate` 會包含具有資料系結語法的 `<li>` 元素。 這種方法仍可在 ASP.NET 2.0 中使用，如我們在[主版頁面和網站導覽](../introduction/master-pages-and-site-navigation-vb.md)教學課程的兩個範例中所見：

- 在 `Site.master` 主版頁面中，會使用中繼器來顯示最上層網站地圖內容的項目符號清單（基礎報表、篩選報表、自訂格式等等）;另一個嵌套的重複項是用來顯示最上層區段的子區段
- 在 `SectionLevelTutorialListing.ascx`中，會使用中繼器來顯示 [目前網站地圖] 區段中子區段的項目符號清單。

> [!NOTE]
> ASP.NET 2.0 引進了新的[BulletedList 控制項](https://msdn.microsoft.com/library/ms228101.aspx)，它可以系結至資料來源控制項，以便顯示簡單的項目符號清單。 使用 BulletedList 控制項時，我們不需要指定任何清單相關的 HTML;相反地，我們只是指示要顯示的資料欄位，做為每個清單專案的文字。

中繼器會作為「全部攔截」資料 Web 控制項。 如果沒有會產生所需標記的現有控制項，則可以使用重複項控制項。 為了說明如何使用中繼器，讓的類別清單顯示在步驟2中建立的產品資訊 DataList 上方。 特別是，讓的類別顯示在單一資料列 HTML `<table>` 中，每個類別都會顯示成資料表中的資料行。

若要完成這項工作，請先從 [工具箱] 將 [中繼器] 控制項拖曳至 [產品資訊] DataList 上方的設計工具。 就像 DataList 一樣，中繼器一開始會顯示為灰色方塊，直到其範本定義完畢為止。

[![在設計工具中新增中繼器](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

**圖 13**：在設計工具中新增中繼器（[按一下以觀看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png)）

在 [中繼器] 智慧標籤中，只有一個選項：選擇 [資料來源]。 選擇建立新的 ObjectDataSource，並將其設定為使用 `CategoriesBLL` 類別的 `GetCategories` 方法。

[![建立新的 ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

**圖 14**：建立新的 ObjectDataSource （[按一下以觀看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png)）

[![將 ObjectDataSource 設定為使用 CategoriesBLL 類別](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

**圖 15**：設定 ObjectDataSource 使用 `CategoriesBLL` 類別（[按一下以觀看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png)）

[![使用 GetCategories 方法取出所有類別的相關資訊](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

**圖 16**：使用 `GetCategories` 方法來抓取所有類別的相關資訊（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png)）

不同于 DataList，Visual Studio 在系結至資料來源之後，不會自動為中繼器建立 ItemTemplate。 此外，無法透過設計工具設定中繼器的範本，而且必須以宣告方式指定。

若要以單一資料列的方式顯示類別目錄 `<table>` 每個類別目錄都有一個資料行，我們需要重複項來發出標記，如下所示：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

因為 `<td>Category X</td>` 文字是重複的部分，所以這會出現在中繼器 s ItemTemplate 中。 出現在 `<table><tr>` 之前的標記會放在 `HeaderTemplate`，而結束標記 `</tr></table>` 則會放在 `FooterTemplate`中。 若要輸入這些範本設定，請移至 [ASP.NET] 頁面的宣告部分，方法是按一下左下角的 [來源] 按鈕，然後輸入下列語法：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

中繼器會以其範本所指定的方式來發出精確的標記，不會再有任何內容。 [圖 17] 顯示透過瀏覽器觀看時的中繼器 s 輸出。

[![單一資料列 HTML &lt;資料表&gt; 會列出個別資料行中的每個類別](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

**圖 17**：單一資料列 HTML `<table>` 列出個別資料行中的每個類別（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png)）

## <a name="step-6-improving-the-appearance-of-the-repeater"></a>步驟6：改善中繼器的外觀

因為重複項會精確地發出其範本所指定的標記，所以不會有任何意外的，因為中繼器沒有與樣式相關的屬性。 若要改變中繼器所產生內容的外觀，我們必須手動將所需的 HTML 或 CSS 內容直接新增至中繼器的範本。

在我們的範例中，讓具有類別目錄資料行的替代背景色彩，例如 DataList 中的交替資料列。 若要完成這項操作，我們必須透過 `ItemTemplate` 和 `AlternatingItemTemplate` 範本，將 `RowStyle` CSS 類別指派給每個中繼器專案，並將 `AlternatingRowStyle` CSS 類別指派給每個交替的中繼器專案，如下所示：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

讓我們也將標頭資料列新增至具有文字產品類別目錄的輸出。 因為我們不知道產生的 `<table>` 將包含多少資料行，所以產生可保證橫跨所有資料行的標頭資料列最簡單的方式，就是使用*兩個*`<table>` s。 第一個 `<table>` 會包含標頭資料列的兩個數據列，以及將包含第二個單一資料列 `<table>` （在系統中每個類別都有一個資料行）的資料列。 也就是說，我們想要發出下列標記：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

下列 `HeaderTemplate` 和 `FooterTemplate` 會產生所需的標記：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

[圖 18] 顯示在進行這些變更之後的中繼器。

[![背景色彩中的類別目錄資料行替代，並包含標題列](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

**圖 18**：背景色彩中替代的類別目錄資料行，並包含標題列（[按一下以查看完整大小的影像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png)）

## <a name="summary"></a>總結

雖然 GridView 控制項可讓您輕鬆地顯示、編輯、刪除、排序和逐頁查看資料，但外觀非常 boxy，而且類似格線。 若要更充分掌控外觀，我們必須轉換成 DataList 或重複項控制項。 這兩個控制項都會使用範本（而不是 BoundFields、CheckBoxFields 等等）來顯示一組記錄。

DataList 會轉譯為 HTML `<table>`，根據預設，會顯示單一資料表列中的每個資料來源記錄，就像具有單一 TemplateField 的 GridView 一樣。 如我們在未來的教學課程中所見，DataList 確實允許每個資料表的資料列顯示多筆記錄。 另一方面，中繼器會嚴格發出其範本中指定的標記;它不會加入任何額外的標記，因此通常用來顯示 `<table>` 以外的 HTML 專案中的資料（例如在項目符號清單中）。

雖然 DataList 和中繼器在其呈現的輸出中提供更大的彈性，但卻缺乏在 GridView 中找到的許多內建功能。 我們將在即將推出的教學課程中進行檢查，其中有些功能不會有太多麻煩，但請記住，使用 DataList 或重複項來代替 GridView 會限制您可以使用的功能，而不需執行這些功能親身.

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Yaakov Ellis、Liz Shulok、Randy Schmidt 和 Stacy 公園。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](nested-data-web-controls-cs.md)
> [下一頁](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
