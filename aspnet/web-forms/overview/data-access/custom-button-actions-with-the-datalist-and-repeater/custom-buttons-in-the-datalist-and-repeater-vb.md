---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
title: DataList 和中繼器中的自訂按鈕（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將建立一個介面，以使用重複項來列出系統中的類別，每個類別都提供一個按鈕來顯示其 associ 。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 1afdb14d-6e49-4e1f-aead-2934730d472e
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: bc7e94e59226b739c2948434c1bfecb46b3d7856
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607603"
---
# <a name="custom-buttons-in-the-datalist-and-repeater-vb"></a>在 DataList 與重複項中自訂按鈕 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_VB.exe)或[下載 PDF](custom-buttons-in-the-datalist-and-repeater-vb/_static/datatutorial46vb1.pdf)

> 在本教學課程中，我們將建立一個介面，以使用重複項來列出系統中的類別，每個類別都會提供一個按鈕，以使用 BulletedList 控制項來顯示其相關聯的產品。

## <a name="introduction"></a>簡介

在過去的十七個 DataList 和中繼器教學課程中，我們已建立唯讀範例和編輯和刪除範例。 為了協助在 DataList 中編輯和刪除功能，我們將按鈕新增至 DataList s `ItemTemplate`，按下時，會導致回傳並引發對應于按鈕 s `CommandName` 屬性的 DataList 事件。 例如，將按鈕加入具有 `CommandName` 屬性值為 Edit 的 `ItemTemplate`，會導致 DataList s `EditCommand` 在回傳時引發;其中一個具有 `CommandName` Delete 會引發 `DeleteCommand`。

除了 [編輯] 和 [刪除] 按鈕以外，DataList 和重複項控制項也可以包含按鈕、LinkButtons 或 ImageButtons，當按下時，就會執行一些自訂的伺服器端邏輯。 在本教學課程中，我們將建立使用中繼器來列出系統中類別的介面。 針對每個類別，中繼器會包含一個按鈕，以使用 BulletedList 控制項來顯示與類別相關聯的產品（請參閱 [圖 1]）。

[![按一下 [顯示產品] 連結，會以項目符號清單顯示產品類別目錄](custom-buttons-in-the-datalist-and-repeater-vb/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image1.png)

**圖 1**：按一下 [顯示產品] 連結會以項目符號清單顯示產品類別目錄（[按一下以觀看完整大小的影像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image3.png)）

## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>步驟1：新增自訂按鈕教學課程網頁

在查看如何新增自訂按鈕之前，先讓我們先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程中需要此功能。 從新增名為 `CustomButtonsDataListRepeater`的資料夾開始。 接下來，將下列兩個 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `CustomButtons.aspx`

![新增自訂按鈕相關教學課程的 ASP.NET 網頁](custom-buttons-in-the-datalist-and-repeater-vb/_static/image4.png)

**圖 2**：新增自訂按鈕相關教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`CustomButtonsDataListRepeater`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 將此使用者控制項從方案總管拖曳至頁面 s 設計檢視，以將其新增至 `Default.aspx`。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](custom-buttons-in-the-datalist-and-repeater-vb/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image5.png)

**圖 3**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image7.png)）

最後，將頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，請使用 DataList 和中繼器 `<siteMapNode>`，在分頁和排序之後加入下列標記：

[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含用於編輯、插入及刪除教學課程的專案。

![網站地圖現在包含自訂按鈕教學課程的專案](custom-buttons-in-the-datalist-and-repeater-vb/_static/image8.png)

[**圖 4**]：網站地圖現在包含自訂按鈕教學課程的專案

## <a name="step-2-adding-the-list-of-categories"></a>步驟2：加入分類清單

在本教學課程中，我們需要建立一個會列出所有分類的重複項，並顯示產品 LinkButton，當您按一下時，就會在項目符號清單中顯示相關聯的類別目錄產品。 讓我們先建立一個簡單的重複項，以列出系統中的類別。 從開啟 [`CustomButtonsDataListRepeater`] 資料夾中的 [`CustomButtons.aspx`] 頁面開始。 從 [工具箱] 將 [中繼器] 拖曳至設計工具，並將其 [`ID`] 屬性設定為 [`Categories`]。 接下來，從 [中繼器] 智慧標籤建立新的資料來源控制項。 具體而言，請建立名為 `CategoriesDataSource` 的新 ObjectDataSource 控制項，從 `CategoriesBLL` 類別 s `GetCategories()` 方法中選取其資料。

[![將 ObjectDataSource 設定為使用 CategoriesBLL 類別的 GetCategories （）方法](custom-buttons-in-the-datalist-and-repeater-vb/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image9.png)

**圖 5**：設定 ObjectDataSource 使用 `CategoriesBLL` 類別的 `GetCategories()` 方法（[按一下以查看完整大小的影像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image11.png)）

不同于 DataList 控制項，Visual Studio 根據資料來源建立預設 `ItemTemplate`，必須手動定義中繼器的範本。 此外，您必須以宣告方式建立和編輯中繼器的範本（也就是，在中繼器 s 智慧標籤中沒有 [編輯範本] 選項）。

按一下左下角的 [來源] 索引標籤，然後加入一個 `ItemTemplate`，在 `<h3>` 元素中顯示類別目錄的名稱，並將其描述放在段落標記中;包含在每個類別之間顯示水準規則（`<hr />`）的 `SeparatorTemplate`。 同時新增 LinkButton，並將其 `Text` 屬性設定為 [顯示產品]。 完成這些步驟之後，您的頁面宣告式標記看起來應該如下所示：

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample2.aspx)]

[圖 6] 顯示透過瀏覽器觀看的頁面。 列出每個類別目錄名稱和描述。 按一下 [顯示產品] 按鈕會導致回傳，但尚未執行任何動作。

[![會顯示每個類別目錄名稱和描述，以及顯示產品 LinkButton](custom-buttons-in-the-datalist-and-repeater-vb/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image12.png)

**圖 6**：每個類別目錄的名稱和描述，以及顯示產品 LinkButton （[按一下以觀看完整大小的影像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image14.png)）

## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>步驟3：按一下 [顯示產品] LinkButton 時，執行伺服器端邏輯

每當按一下 DataList 或重複項中範本內的按鈕、LinkButton 或 ImageButton 時，就會發生回傳，而 DataList 或 Repeater `ItemCommand` 事件會引發。 除了 `ItemCommand` 事件以外，如果按鈕的 `CommandName` 屬性設定為其中一個保留字元串（Delete、Edit、Cancel、Update 或 Select），DataList 控制項也可能會引發另一個更特定的事件，但 `ItemCommand` 事件*一律*會引發。

當按一下 DataList 或中繼器內的按鈕時，通常需要傳遞按下哪一個按鈕（在控制項中可能有多個按鈕，例如 [編輯] 和 [刪除] 按鈕），還有一些額外的資訊（例如已按下按鈕的專案主要索引鍵值。 按鈕、LinkButton 和 ImageButton 提供兩個屬性，其值會傳遞至 `ItemCommand` 事件處理常式：

- `CommandName` 通常用來識別範本中每個按鈕的字串
- `CommandArgument` 通常用來保存某些資料欄位的值，例如主要金鑰值

在此範例中，請將 LinkButton 的 `CommandName` 屬性設定為 ShowProducts，並使用資料系結語法 `CategoryArgument='<%# Eval("CategoryID") %>'`，將目前的記錄 s 主要金鑰值 `CategoryID` 系結至 `CommandArgument` 的屬性。 指定這兩個屬性之後，LinkButton 的宣告式語法應如下所示：

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample3.aspx)]

按一下按鈕時，就會發生回傳，而 DataList 或中繼器 `ItemCommand` 事件會引發。 事件處理常式會傳遞按鈕 s `CommandName` 並 `CommandArgument` 值。

建立中繼器 `ItemCommand` 事件的事件處理常式，並記下傳遞至事件處理常式的第二個參數（名為 `e`）。 第二個參數的類型是[`RepeaterCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) ，而且具有下列四個屬性：

- `CommandArgument` 已按下按鈕 `CommandArgument` 屬性的值
- `CommandName` 按鈕 `CommandName` 屬性的值
- `CommandSource` 已按下的按鈕控制項的參考
- `Item` [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx)的參考，其中包含已按下的按鈕;系結至中繼器的每一筆記錄都是以 `RepeaterItem`

因為選取的類別目錄 `CategoryID` 是透過 `CommandArgument` 屬性傳入，所以我們可以在 `ItemCommand` 事件處理常式中，取得與所選分類相關聯的產品集合。 這些產品接著可以系結至 `ItemTemplate` 中的 BulletedList 控制項（我們尚未新增）。 剩下的就是新增 BulletedList，在 `ItemCommand` 事件處理常式中參考它，然後系結至所選類別的一組產品，我們將在步驟4中解決。

> [!NOTE]
> DataList s `ItemCommand` 事件處理常式會傳遞[`DataListCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)類型的物件，這會提供與 `RepeaterCommandEventArgs` 類別相同的四個屬性。

## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>步驟4：在項目符號清單中顯示選取的類別 s 產品

選取的類別目錄產品可以使用任意數目的控制項顯示在中繼器 `ItemTemplate` 內。 我們可以加入另一個嵌套的中繼器、DataList、DropDownList、GridView 等等。 不過，因為我們想要將產品顯示為項目符號清單，所以我們將使用 BulletedList 控制項。 回到 `CustomButtons.aspx` 頁面的宣告式標記，將 BulletedList 控制項新增至 顯示產品 LinkButton 之後的 `ItemTemplate`。 將 BulletedLists s `ID` 設定為 `ProductsInCategory`。 BulletedList 會顯示透過 `DataTextField` 屬性指定的資料欄位值。由於此控制項將會系結產品資訊，因此請將 `DataTextField` 屬性設為 `ProductName`。

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample4.aspx)]

在 `ItemCommand` 事件處理常式中，使用 `e.Item.FindControl("ProductsInCategory")` 參考此控制項，並將它系結至與所選分類相關聯的產品集合。

[!code-vb[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample5.vb)]

在 `ItemCommand` 事件處理常式中執行任何動作之前，最好先檢查傳入 `CommandName`的值。 由於在按一下*任何*按鈕時，會引發 `ItemCommand` 事件處理常式，因此，如果範本中有多個按鈕，請使用 `CommandName` 值來辨別要採取的動作。 在這裡檢查 `CommandName` 是想法，因為我們只有一個按鈕，但最好是建立表單的習慣。 接下來，會從 `CommandArgument` 屬性中抓取所選類別的 `CategoryID`。 然後會參考範本中的 BulletedList 控制項，並將其系結至 `ProductsBLL` 類別 s `GetProductsByCategoryID(categoryID)` 方法的結果。

在先前的教學課程中，使用 DataList 中的按鈕，例如在[datalist 中編輯和刪除資料的總覽](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)，我們已透過 `DataKeys` 集合判斷出給定專案的主要索引鍵值。 雖然這種方法適用于 DataList，但中繼器並沒有 `DataKeys` 的屬性。 相反地，我們必須使用替代方法來提供主鍵值，例如透過按鈕的 `CommandArgument` 屬性，或將主要索引鍵值指派給範本內的隱藏標籤 Web 控制項，並使用 `e.Item.FindControl("LabelID")`在 `ItemCommand` 事件處理常式中讀取其值。

完成 `ItemCommand` 事件處理常式之後，請花點時間在瀏覽器中測試此頁面。 如 [圖 7] 所示，按一下 [顯示產品] 連結會導致回傳，並在 BulletedList 中顯示所選取類別目錄的產品。 此外，也請注意，即使按一下其他類別顯示產品連結，此產品資訊仍會保留。

> [!NOTE]
> 如果您想要修改此報告的行為，只會列出一次一個類別目錄的產品，只要將 [BulletedList 控制項] `EnableViewState` 屬性設定為 [`False`] 即可。

[![使用 BulletedList 來顯示所選類別目錄的產品](custom-buttons-in-the-datalist-and-repeater-vb/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image15.png)

**圖 7**： BulletedList 用來顯示所選類別的產品（[按一下以觀看完整大小的影像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image17.png)）

## <a name="summary"></a>總結

DataList 和中繼器控制項可以在其範本中包含任意數目的按鈕、LinkButtons 或 ImageButtons。 按一下這類按鈕時，會導致回傳並引發 `ItemCommand` 事件。 若要將自訂伺服器端動作與按一下的按鈕產生關聯，請建立 `ItemCommand` 事件的事件處理常式。 在此事件處理常式中，會先檢查傳入的 `CommandName` 值，以判斷所按的按鈕。 您可以選擇性地透過按鈕 `CommandArgument` 屬性來提供其他資訊。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dennis Patterson。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](custom-buttons-in-the-datalist-and-repeater-cs.md)
