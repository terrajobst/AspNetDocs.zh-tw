---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
title: 新增 GridView 的選項按鈕欄（VB） |Microsoft Docs
author: rick-anderson
description: 本教學課程探討如何將選項按鈕的資料行新增至 GridView 控制項，以提供使用者更直覺的方式來選取單一資料列 。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 2e31b60b-8723-4f14-b7ee-37859454dc3b
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
msc.type: authoredcontent
ms.openlocfilehash: ee67a4556c65d2c9570bf15b42fc3c8e5f555bda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78590787"
---
# <a name="adding-a-gridview-column-of-radio-buttons-vb"></a>新增 GridView 的選項按鈕欄 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_VB.exe)或[下載 PDF](adding-a-gridview-column-of-radio-buttons-vb/_static/datatutorial51vb1.pdf)

> 本教學課程探討如何將選項按鈕的資料行新增至 GridView 控制項，以提供使用者更直覺的方式來選取 GridView 的單一資料列。

## <a name="introduction"></a>簡介

GridView 控制項提供大量的內建功能。 其中包含一些不同的欄位，可顯示文字、影像、超連結和按鈕。 它支援進一步自訂的範本。 只要按幾下滑鼠，就能建立 GridView，其中每個資料列都可以透過按鈕來選取，或是啟用編輯或刪除功能。 儘管眾多提供的功能，通常還是需要新增額外、不支援的功能。 在本教學課程和接下來的兩個中，我們將探討如何增強 GridView 的功能，以包含額外的功能。

本教學課程和下一個重點著重于增強資料列選取程式。 如[使用可選取的主要 GridView 和詳細資料 detailview 之中所述的主要/詳細資料](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)，我們可以將 CommandField 新增至包含 [選取] 按鈕的 GridView。 當您按一下時，回傳接踵而來和 GridView 的 `SelectedIndex` 屬性會更新為已按下 [選取] 按鈕之資料列的索引。 在[主要/詳細資料中，透過詳細資料 detailview 之教學課程使用可選取的主要 GridView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) ，我們已瞭解如何使用這項功能來顯示所選 GridView 資料列的詳細資訊。

雖然 [選取] 按鈕在許多情況下都可運作，但對其他人而言可能也無法運作。 除了使用按鈕以外，還有其他兩個使用者介面元素常用於選取範圍：選項按鈕和核取方塊。 我們可以擴充 GridView，使其不使用 [選取] 按鈕，而是每個資料列都包含一個選項按鈕或核取方塊。 在使用者只能選取其中一個 GridView 記錄的案例中，選項按鈕可能會優先于 [選取] 按鈕。 在使用者可能會在網頁型電子郵件應用程式中選取多筆記錄（例如）時，使用者可能會想要選取多個訊息來刪除核取方塊提供無法從 [選取] 按鈕或選項按鈕取得的功能使用者介面。

本教學課程探討如何將選項按鈕的資料行新增至 GridView。 繼續進行的教學課程會探索使用核取方塊。

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>步驟1：建立增強 GridView Web Pages

在我們開始增強 GridView 以包含選項按鈕的資料行之前，先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程和接下來的兩頁中使用。 從新增名為 `EnhancedGridView`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`

![新增 SqlDataSource 相關教學課程的 ASP.NET 網頁](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.gif)

**圖 1**：新增 SqlDataSource 相關教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`EnhancedGridView`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將這個使用者控制項加入至 `Default.aspx`，方法是將它從方案總管拖曳至頁面 s 設計檢視。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.png)）

最後，將這四個頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，請使用 SqlDataSource 控制項 `<siteMapNode>`，在之後新增下列標記：

[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含用於編輯、插入及刪除教學課程的專案。

![網站地圖現在包含增強 GridView 教學課程的專案](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.gif)

[**圖 3**]：網站地圖現在包含增強 GridView 教學課程的專案

## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>步驟2：在 GridView 中顯示供應商

在本教學課程中，我們將建立一個 GridView，其中列出美國供應商，每個 GridView 資料列提供一個選項按鈕。 透過選項按鈕選取供應商之後，使用者可以按一下按鈕來查看供應商的產品。 雖然這項工作聽起來很簡單，但還是有一些微妙差異讓它特別棘手。 在深入探討這些微妙差異之前，先讓先取得一個 GridView 來列出供應商。

首先，從 [工具箱] 將 GridView 拖曳至設計工具上，以開啟 [`EnhancedGridView`] 資料夾中的 [`RadioButtonField.aspx`] 頁面。 將 GridView 的 `ID` 設定為 `Suppliers` 並從其智慧標籤，選擇建立新的資料來源。 具體而言，請建立名為 `SuppliersDataSource` 的 ObjectDataSource，從 `SuppliersBLL` 物件提取其資料。

[![建立名為 SuppliersDataSource 的新 ObjectDataSource](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.png)

**圖 4**：建立名為 `SuppliersDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.png)）

[![將 ObjectDataSource 設定為使用 SuppliersBLL 類別](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.png)

**圖 5**：設定 ObjectDataSource 使用 `SuppliersBLL` 類別（[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.png)）

因為我們只想要列出美國供應商，請從 [選取] 索引標籤的下拉式清單中選擇 [`GetSuppliersByCountry(country)`] 方法。

[![將 ObjectDataSource 設定為使用 SuppliersBLL 類別](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.png)

**圖 6**：設定 ObjectDataSource 使用 `SuppliersBLL` 類別（[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.png)）

從 [更新] 索引標籤選取 [（無）] 選項，然後按 [下一步]。

[![將 ObjectDataSource 設定為使用 SuppliersBLL 類別](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.png)

**圖 7**：設定 ObjectDataSource 使用 `SuppliersBLL` 類別（[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.png)）

由於 `GetSuppliersByCountry(country)` 方法會接受參數，因此 [設定資料來源] wizard 會提示我們輸入該參數的來源。 若要指定硬式編碼值（在此範例中為美國），請將 [參數來源] 下拉式清單設定為 [無]，並在文字方塊中輸入預設值。 按一下 [完成] 完成精靈。

[![使用 USA 作為 country 參數的預設值](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.png)

**圖 8**：使用 USA 做為 `country` 參數的預設值（[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.png)）

完成 wizard 之後，GridView 會針對每個供應商資料欄位包含一個 BoundField。 移除除了 `CompanyName`、`City`和 `Country` BoundFields 的所有內容，並將 `CompanyName` BoundFields `HeaderText` 屬性重新命名為供應商。 這麼做之後，GridView 和 ObjectDataSource 宣告式語法看起來應該如下所示。

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample2.aspx)]

在本教學課程中，讓使用者可以在與供應商清單相同的頁面上，或在不同的頁面上，查看選取的供應商產品。 為了配合此，請將兩個按鈕 Web 控制項新增至頁面。 我將這兩個按鈕的 `ID` 設定為 `ListProducts` 和 `SendToProducts`，並瞭解當按下 [`ListProducts`] 時，將會發生回傳，而選取的供應商產品將會列在相同的頁面上，但是按一下 [`SendToProducts`] 時，使用者將會即可檢視至另一個列出產品的頁面。

[圖 9] 顯示透過瀏覽器觀看時的 `Suppliers` GridView 和兩個按鈕 Web 控制項。

[![美國供應商列出其姓名、城市和國家/地區資訊](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.png)

**圖 9**：美國的供應商列出其姓名、城市和國家/地區資訊（[按一下以觀看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.png)）

## <a name="step-3-adding-a-column-of-radio-buttons"></a>步驟3：加入選項按鈕的資料行

此時，`Suppliers` GridView 有三個 BoundFields，顯示美國每位供應商的公司名稱、城市和國家/地區。 不過，它仍然缺少選項按鈕的資料行。 可惜的是，GridView 不會包含內建的 RadioButtonField，否則我們可以直接將其加入至方格，然後完成。 相反地，我們可以新增 TemplateField 並設定其 `ItemTemplate` 來轉譯選項按鈕，產生每個 GridView 資料列的選項按鈕。

一開始，我們可能會假設所需的使用者介面可以藉由將選項按鈕 Web 控制項新增至 TemplateField 的 `ItemTemplate` 來執行。 雖然這確實會在 GridView 的每個資料列中加入一個選項按鈕，但無法將選項按鈕分組，因此不會互斥。 也就是說，使用者可以同時從 GridView 中選取多個選項按鈕。

雖然使用選項按鈕 Web 控制項的 TemplateField 不提供我們所需的功能，但讓我們來實行這種方法，因為它很值得檢查產生的選項按鈕為何不會分組。 首先，將 TemplateField 新增至供應商 GridView，使其成為最左邊的欄位。 接下來，從 GridView 的智慧標籤中，按一下 [編輯範本] 連結，並將選項按鈕 Web 控制項從 [工具箱] 拖曳至 TemplateField s `ItemTemplate` （請參閱 [圖 10]）。 將 [選項按鈕] `ID` 屬性設定為 [`RowSelector`]，並將 `GroupName` 屬性設為 [`SuppliersGroup`]。

[![將選項按鈕 Web 控制項加入至 ItemTemplate](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.png)

**圖 10**：將選項按鈕 Web 控制項新增至 `ItemTemplate` （[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.png)）

透過設計工具進行這些新增之後，GridView 的標記看起來應該如下所示：

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample3.aspx)]

選項按鈕的[`GroupName` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx)是用來分組一系列選項按鈕的內容。 所有具有相同 `GroupName` 值的選項按鈕控制項都會被視為群組;一個群組一次只能選取一個選項按鈕。 `GroupName` 屬性會指定呈現的選項按鈕 `name` 屬性的值。 瀏覽器會檢查 `name` 屬性的選項按鈕，以決定選項按鈕分組。

將選項按鈕 Web 控制項加入至 `ItemTemplate`之後，請透過瀏覽器造訪此頁面，然後按一下方格的資料列中的選項按鈕。 請注意，選項按鈕如何分組，讓您可以選取所有資料列，如 [圖 11] 所示。

[![GridView 的選項按鈕未分組](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.png)

**圖 11**： GridView 的選項按鈕不分組（[按一下以觀看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.png)）

選項按鈕不會分組的原因是因為其呈現的 `name` 屬性不同，儘管有相同的 `GroupName` 屬性設定。 若要查看這些差異，請從瀏覽器執行 View/Source，並檢查選項按鈕標記：

[!code-html[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample4.html)]

請注意，`name` 和 `id` 屬性不是屬性視窗中所指定的確切值，而是在前面加上一些其他 `ID` 值。 在轉譯的 `id` 前加入的額外 `ID` 值和 `name` 屬性是選項按鈕的 `ID`，父元素會控制 `GridViewRow` s `ID`、GridView s `ID`、內容控制項 s `ID`和 Web 表單 s `ID`。 加入這些 `ID`，讓 GridView 中每個轉譯的 Web 控制項都有唯一的 `id` 和 `name` 值。

每個呈現的控制項都需要不同的 `name` 和 `id`，因為這是瀏覽器如何唯一識別用戶端上的每個控制項，以及它如何識別 web 伺服器在回傳時所發生的動作或變更。 例如，假設我們想要在選項按鈕的核取狀態變更時執行一些伺服器端程式碼。 我們可以將選項按鈕的 `AutoPostBack` 屬性設定為 `True` 並建立 `CheckChanged` 事件的事件處理常式，來達到這個目的。 不過，如果呈現的 `name` 和所有選項按鈕的 `id` 值都相同，則在回傳時，我們無法判斷按一下哪個特定的選項按鈕。

其中的簡短之處在于，我們無法使用選項按鈕 Web 控制項，在 GridView 中建立一個選項按鈕的資料行。 相反地，我們必須使用，而不是以陳舊的技術來確保將適當的標記插入每個 GridView 資料列。

> [!NOTE]
> 就像選項按鈕 Web 控制項一樣，在新增至範本時，選項按鈕 HTML 控制項將包含唯一的 `name` 屬性，使方格中的選項按鈕取消群組。 如果您不熟悉 HTML 控制項，可以放心忽略這種情況，因為 HTML 控制項很少使用，特別是在 ASP.NET 2.0 中。 但如果您有興趣深入瞭解，請參閱[Allen](http://odetocode.com/blogs/scott/default.aspx)的 Blog 專案[WEB 控制項和 HTML 控制項](http://www.odetocode.com/Articles/348.aspx)。

## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>使用常值控制項插入選項按鈕標記

為了正確地分組 GridView 內的所有選項按鈕，我們需要手動將選項按鈕標記插入 `ItemTemplate`。 每個選項按鈕都需要相同的 `name` 屬性，但應具有唯一的 `id` 屬性（如果我們想要透過用戶端腳本存取選項按鈕）。 在使用者選取選項按鈕並回傳頁面之後，瀏覽器會傳回所選選項按鈕 `value` 屬性的值。 因此，每個選項按鈕都需要唯一的 `value` 屬性。 最後，在回傳時，我們必須確定將 `checked` 屬性加入至選取的選項按鈕，否則，當使用者選取並回傳後，選項按鈕就會回到其預設狀態（全部皆未選取）。

有兩種方法可以採用，以將低層級的標記插入範本中。 其中一種是混合使用程式碼後置類別中所定義的格式化方法，並進行標記和呼叫。 這項技術是第一次在 GridView 控制項教學課程中[使用 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)的討論。 在我們的案例中，它看起來可能像這樣：

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample5.aspx)]

在這裡，`GetUniqueRadioButton` 和 `GetRadioButtonValue` 是在程式碼後置類別中定義的方法，其會針對每個選項按鈕傳回適當的 `id` 和 `value` 屬性值。 這種方法很適合用來指派 `id` 和 `value` 屬性，但在需要指定 `checked` 屬性值時，這是較短的，因為只有在資料第一次系結至 GridView 時，才會執行 databinding 語法。 因此，如果 GridView 已啟用 view 狀態，則只有第一次載入頁面時（或當 GridView 明確地重新系結至資料來源時），才會引發格式化方法，因此不會在回傳時呼叫設定 `checked` 屬性的函數。 這就是有點微妙的問題，而不是本文的討論範圍，所以我要把它放在這裡。 不過，我也建議您嘗試使用上述方法，並將它工作到您要停滯的地方。 雖然這類練習不會讓您更接近工作版本，但它有助於促進 GridView 和資料系結生命週期的深入瞭解。

另一種將自訂、低層級標記插入範本中的方法，以及我們將在本教學課程中使用的方法，就是將[常值控制項](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx)新增至範本。 然後，在 GridView 的 `RowCreated` 或 `RowDataBound` 事件處理常式中，常值控制項可透過程式設計方式存取，並將其 `Text` 屬性設定為要發出的標記。

一開始先從 TemplateField s `ItemTemplate`中移除選項按鈕，並將它取代為常值控制項。 將 [常值控制] `ID` 設定為 [`RadioButtonMarkup`]。

[![將常值控制項加入至 ItemTemplate](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.png)

**圖 12**：將常值控制項加入至 `ItemTemplate` （[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.png)）

接下來，建立 GridView s `RowCreated` 事件的事件處理常式。 無論資料是否正在重新系結至 GridView，`RowCreated` 事件都會針對加入的每個資料列引發一次。 這表示即使在從 view 狀態重載資料時，也會在回傳時引發 `RowCreated` 事件，而這就是我們使用它的原因，而不是 `RowDataBound` （這只會在資料明確系結至資料 Web 控制項時引發）。

在此事件處理常式中，我們只想要在我們重新處理資料列時繼續進行。 針對每個資料列，我們想要以程式設計方式參考 `RadioButtonMarkup` 的常值控制項，並將其 `Text` 屬性設定為要發出的標記。 如下列程式碼所示，發出的標記會建立一個選項按鈕，其 `name` 屬性設為 `SuppliersGroup`，其 `id` 屬性設定為 `RowSelectorX`，其中*X*是 gridview 資料列的索引，而其 `value` 屬性設定為 gridview 資料列的索引。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample6.vb)]

選取 GridView 資料列並進行回傳時，我們會對所選供應商的 `SupplierID` 感興趣。 因此，您可能會認為每個選項按鈕的值都應該是實際的 `SupplierID` （而不是 GridView 資料列的索引）。 雖然這在某些情況下可能會有作用，但還是會有一項安全性風險，可以盲目接受和處理 `SupplierID`。 例如，我們的 GridView 只會列出美國的供應商。 不過，如果直接從選項按鈕傳遞 `SupplierID`，會阻止 mischievous 使用者操作回傳時傳回的 `SupplierID` 值？ 藉由使用資料列索引做為 `value`，然後在從 `DataKeys` 集合回傳時取得 `SupplierID`，我們可以確保使用者只使用其中一個 GridView 資料列相關聯的 `SupplierID` 值。

加入這個事件處理常式程式碼之後，請花幾分鐘的時間在瀏覽器中測試頁面。 首先，請注意，一次只能選取方格中的一個選項按鈕。 不過，當選取選項按鈕並按一下其中一個按鈕時，就會發生回傳，而且選項按鈕會全部還原成其初始狀態（也就是在回傳時，不會再選取選取的選項按鈕）。 若要修正此問題，我們必須擴充 `RowCreated` 事件處理常式，使其檢查從回傳傳送的選取選項按鈕索引，並將 `checked="checked"` 屬性加入至資料列索引相符專案的發出標記。

當回傳時，瀏覽器會傳回選取之選項按鈕的 `name` 和 `value`。 此值可以使用 `Request.Form("name")`以程式設計方式抓取。 [`Request.Form` 屬性](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx)提供代表表單變數的[`NameValueCollection`](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx) 。 表單變數是網頁中表單域的名稱和值，每當回傳接踵而來時，網頁瀏覽器就會送回。 由於 GridView 中選項按鈕的轉譯 `name` 屬性是 `SuppliersGroup`，因此當網頁回傳時，瀏覽器會將 `SuppliersGroup=valueOfSelectedRadioButton` 傳送回 web 伺服器（連同其他表單欄位）。 然後您可以使用： `Request.Form("SuppliersGroup")`，從 `Request.Form` 屬性存取此資訊。

由於我們只需要判斷在 `RowCreated` 事件處理常式中所選取的選項按鈕索引，而是在按鈕 Web 控制項的 `Click` 事件處理常式中，因此，請將 `SuppliersSelectedIndex` 屬性加入至會傳回 `-1` 的程式碼後置類別，如果未選取任何選項按鈕，則為選取的索引，如果選取了其中一個選項按鈕，則會傳回該專案。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample7.vb)]

加入這個屬性之後，我們知道當 `SuppliersSelectedIndex` 等於 `e.Row.RowIndex`時，會在 `RowCreated` 事件處理常式中加入 `checked="checked"` 標記。 更新事件處理常式以包含下列邏輯：

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample8.vb)]

透過這種變更，在回傳之後，選取的選項按鈕會保持選取狀態。 既然我們已經能夠指定要選取的選項按鈕，我們可以變更行為，以便在第一次流覽頁面時選取第一個 GridView 資料列 s 選項按鈕（而不是預設選取的選項按鈕，這是目前的行為）。 若要預設選取第一個選項按鈕，只需將 `If SuppliersSelectedIndex = e.Row.RowIndex Then` 語句變更為下列： `If SuppliersSelectedIndex = e.Row.RowIndex OrElse (Not Page.IsPostBack AndAlso e.Row.RowIndex = 0) Then`。

此時，我們已將群組選項按鈕的資料行新增至 GridView，以允許在回傳之間選取並記住單一 GridView 資料列。 接下來的步驟是顯示所選供應商所提供的產品。 在步驟4中，我們將瞭解如何將使用者重新導向至另一個頁面，並沿著選取的 `SupplierID`傳送。 在步驟5中，我們將瞭解如何在同一個頁面上，將選取的供應商產品顯示在 GridView 中。

> [!NOTE]
> 我們可以建立自訂的 `DataControlField` 類別來呈現適當的使用者介面和功能，而不是使用 TemplateField （此冗長步驟3的焦點）。 [`DataControlField` 類別](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx)是 BoundField、CheckBoxField、TemplateField 和其他內建 GridView 和 DetailsView 欄位衍生來源的基類。 建立自訂的 `DataControlField` 類別，表示只能使用宣告式語法來新增選項按鈕的資料行，也可以讓您更輕鬆地在其他網頁和其他 web 應用程式上複寫功能。

不過，如果您在 ASP.NET 中建立了自訂的編譯控制項，那麼您知道這麼做需要相當跑腿活兒的，並且攜帶一系列必須謹慎處理的微妙差異和 edge 案例。 因此，我們會放棄將選項按鈕的資料行實作為現在的自訂 `DataControlField` 類別，並使用 TemplateField 選項。 也許我們有機會在未來的教學課程中探索如何建立、使用和部署自訂的 `DataControlField` 類別！

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>步驟4：在不同的頁面中顯示選取的供應商產品

在使用者選取 GridView 資料列之後，我們必須顯示選取的供應商產品。 在某些情況下，我們可能會想要在不同的頁面中顯示這些產品，我們可能會偏好在相同的頁面中執行。 讓我們先檢查如何在不同的頁面中顯示產品;在步驟5中，我們將探討如何將 GridView 新增至 `RadioButtonField.aspx`，以顯示選取的供應商產品。

目前頁面上有兩個按鈕 Web 控制項 `ListProducts` 和 `SendToProducts`。 按一下 [`SendToProducts`] 按鈕時，我們會想要將使用者傳送至 `~/Filtering/ProductsForSupplierDetails.aspx`。 此頁面是在[兩個頁面教學課程的主要/詳細資料篩選](../masterdetail/master-detail-filtering-across-two-pages-vb.md)中建立的，而且會顯示供應商的產品，其 `SupplierID` 是透過名為 `SupplierID`的 querystring 欄位來傳遞。

若要提供這種功能，請建立 `SendToProducts` 按鈕 s `Click` 事件的事件處理常式。 在步驟3中，我們新增了 `SuppliersSelectedIndex` 屬性，它會傳回已選取選項按鈕之資料列的索引。 您可以從 GridView 的 `DataKeys` 集合中抓取對應的 `SupplierID`，然後可以使用 `Response.Redirect("url")`將使用者傳送至 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID`。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample9.vb)]

只要從 GridView 選取其中一個選項按鈕，此程式碼就會運作 wonderfully。 如果一開始，GridView 並未選取任何選項按鈕，而使用者按一下 [`SendToProducts`] 按鈕，`SuppliersSelectedIndex` 將會 `-1`，這會導致擲回例外狀況，因為 `-1` 超出 `DataKeys` 集合的索引範圍。 不過，如果您決定要更新步驟3中所討論的 `RowCreated` 事件處理常式，以便一開始選取 GridView 中的第一個選項按鈕，這就不是問題。

若要配合 `-1`的 `SuppliersSelectedIndex` 值，請將標籤 Web 控制項新增至 GridView 上方的頁面。 將其 [`ID`] 屬性設定為 [`ChooseSupplierMsg`]、其 [`CssClass`] 屬性設為 [`Warning`]、將其 [`EnableViewState`] 和 [`Visible`] 屬性設定為 [`False`]，並將其 [`Text`] 屬性 CSS 類別 `Warning` 以紅色、斜體、粗體、大字型來顯示文字，並在 `Styles.css`中定義。 藉由將 [`EnableViewState`] 和 [`Visible`] 屬性設定為 [`False`]，就不會轉譯標籤，只會轉譯控制項 s `Visible` 屬性以程式設計方式設定為 `True`的那些回傳。

[![在 GridView 上方新增標籤 Web 控制項](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image21.png)

**圖 13**：在 GridView 上方新增標籤 Web 控制項（[按一下以觀看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image22.png)）

接下來，如果 `SuppliersSelectedIndex` 小於零，請擴大 `Click` 事件處理常式以顯示 `ChooseSupplierMsg` 標籤，然後將使用者重新導向至 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID`，否則為。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample10.vb)]

請造訪瀏覽器中的頁面，然後按一下 [`SendToProducts`] 按鈕，然後再從 GridView 選取供應商。 如 [圖 14] 所示，這會顯示 [`ChooseSupplierMsg`] 標籤。 接下來，選取供應商，然後按一下 [`SendToProducts`] 按鈕。 這會 whisk 您到一個頁面，其中列出所選供應商所提供的產品。 [圖 15] 顯示選取 Bigfoot Breweries 供應商時的 `ProductsForSupplierDetails.aspx` 頁面。

[![如果未選取任何供應商，則會顯示 [ChooseSupplierMsg] 標籤](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image23.png)

**圖 14**：如果未選取供應商，就會顯示 [`ChooseSupplierMsg`] 標籤（[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image24.png)）

[![選取的供應商產品會顯示在 ProductsForSupplierDetails 中](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image25.png)

**圖 15**：選取的供應商產品會顯示在 `ProductsForSupplierDetails.aspx` （[按一下以觀看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image26.png)）

## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>步驟5：在相同的頁面上顯示選取的供應商產品

在步驟4中，我們看到如何將使用者傳送至另一個網頁，以顯示選取的供應商產品。 或者，選取的供應商產品可以顯示在相同的頁面上。 為了說明這一點，我們會將另一個 GridView 新增至 `RadioButtonField.aspx`，以顯示選取的供應商產品。

因為我們只想要在選取供應商之後顯示這一 GridView 的產品，請在 `Suppliers` GridView 底下新增面板 Web 控制項，將其 `ID` 設定為 `ProductsBySupplierPanel`，並將其 `Visible` 屬性設為 [`False`]。 在面板中，新增所選供應商的文字產品，後面接著名為 `ProductsBySupplier`的 GridView。 從 GridView 的智慧標籤中，選擇將其系結至名為 `ProductsBySupplierDataSource`的新 ObjectDataSource。

[![將 ProductsBySupplier GridView 系結至新的 ObjectDataSource](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image27.png)

**圖 16**：將 `ProductsBySupplier` GridView 系結至新的 ObjectDataSource （[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image28.png)）

接下來，設定 ObjectDataSource 以使用 `ProductsBLL` 類別。 因為我們只想要取出所選供應商所提供的產品，請指定 ObjectDataSource 應叫用 `GetProductsBySupplierID(supplierID)` 方法來抓取其資料。 從 [更新]、[插入] 和 [刪除] 索引標籤的下拉式清單中，選取 [（無）]。

[![將 ObjectDataSource 設定為使用 GetProductsBySupplierID （已加入供應商）方法](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image29.png)

**圖 17**：設定 ObjectDataSource 以使用 `GetProductsBySupplierID(supplierID)` 方法（[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image30.png)）

[![在 [更新]、[插入] 和 [刪除] 索引標籤中，將下拉式清單設定為 [（無）]](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image31.png)

**圖 18**：在 [更新]、[插入] 和 [刪除] 索引標籤中，將下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image32.png)）

設定 [選取、更新、插入和刪除] 索引標籤之後，按 [下一步]。 由於 `GetProductsBySupplierID(supplierID)` 方法需要輸入參數，因此 [建立資料來源] wizard 會提示我們指定參數 s 值的來源。

在這裡，我們有幾個選項來指定參數 s 值的來源。 我們可以使用預設參數物件，並以程式設計方式將 `SuppliersSelectedIndex` 屬性的值指派給 ObjectDataSource s `Selecting` 事件處理常式中的參數 s `DefaultValue` 屬性。 以程式設計方式[設定 objectdatasource 的參數值](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)教學課程，以程式設計方式將值指派給 objectdatasource s 參數，以進行切換。

或者，我們可以使用 ControlParameter，並參考 `Suppliers` GridView 的[`SelectedValue` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx)（請參閱 [圖 19]）。 GridView 的 `SelectedValue` 屬性會傳回對應至[`SelectedIndex` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx)的 `DataKey` 值。 為了讓這個選項能夠正常執行，我們需要在按一下 [`ListProducts`] 按鈕時，以程式設計方式將 GridView 的 `SelectedIndex` 屬性設定為選取的資料列。 藉由設定 `SelectedIndex`，選取的記錄將會採用 `DataWebControls` 主題中定義的 `SelectedRowStyle` （黃色背景），這是一項額外的好處。

[![使用 ControlParameter 來指定 GridView s SelectedValue 做為參數來源](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image33.png)

**圖 19**：使用 ControlParameter 指定 GridView s SelectedValue 做為參數來源（[按一下以查看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image34.png)）

完成此嚮導後，Visual Studio 會自動為產品的資料欄位加入欄位。 移除除了 `ProductName`、`CategoryName`和 `UnitPrice` BoundFields 的所有內容，並將 `HeaderText` 屬性變更為 [產品]、[類別] 和 [價格]。 設定 `UnitPrice` BoundField，使其值格式化為貨幣。 進行這些變更之後，Panel、GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample11.aspx)]

若要完成此練習，我們必須將 GridView 的 `SelectedIndex` 屬性設為 `SelectedSuppliersIndex`，並將 `ProductsBySupplierPanel` 面板 s `Visible` 屬性設定為按一下 [`True`] 按鈕時的 `ListProducts`。 若要完成這項操作，請為 `ListProducts` 按鈕 Web 控制項 `Click` 事件建立事件處理常式，並新增下列程式碼：

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample12.vb)]

如果尚未從 GridView 選取供應商，則會顯示 [`ChooseSupplierMsg`] 標籤，並隱藏 [`ProductsBySupplierPanel`] 面板。 否則，如果已選取供應商，則會顯示 `ProductsBySupplierPanel`，並更新 GridView 的 `SelectedIndex` 屬性。

[圖 20] 顯示已選取 Bigfoot Breweries 供應商，並按一下 [在頁面上顯示產品] 按鈕之後的結果。

[![Bigfoot Breweries 所提供的產品會列在相同的頁面上](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image35.png)

**圖 20**： Bigfoot Breweries 所提供的產品會列在相同的頁面上（[按一下以觀看完整大小的影像](adding-a-gridview-column-of-radio-buttons-vb/_static/image36.png)）

## <a name="summary"></a>總結

如[使用可選取的主要 GridView 與詳細資料 detailview 之](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)教學課程中所討論的主要/詳細資料，您可以使用 CommandField （其 `ShowSelectButton` 屬性設為 `True`）從 GridView 選取記錄。 但是 CommandField 會將其按鈕顯示為一般的推播按鈕、連結或影像。 另一個資料列選取的使用者介面是在每個 GridView 資料列中提供選項按鈕或核取方塊。 在本教學課程中，我們已檢查如何新增選項按鈕的資料行。

可惜的是，加入選項按鈕的資料行並不像預期般簡單明瞭。 在按一下按鈕時，沒有內建的 RadioButtonField 可以加入，而且在 TemplateField 中使用選項按鈕 Web 控制項會引進自己的問題集。 最後，若要提供這類介面，我們必須建立自訂 `DataControlField` 類別，或在 `RowCreated` 事件期間，將適當的 HTML 插入 TemplateField 中。

探索如何新增選項按鈕的資料行，讓我們將注意力轉變成加入核取方塊的資料行。 使用核取方塊的資料行時，使用者可以選取一或多個 GridView 資料列，然後在所有選取的資料列上執行一些作業（例如，從網頁型電子郵件用戶端選取一組電子郵件，然後選擇刪除所有選取的電子郵件）。 在下一個教學課程中，我們將瞭解如何加入這類資料行。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者是 David Suru。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
> [下一頁](adding-a-gridview-column-of-checkboxes-vb.md)
