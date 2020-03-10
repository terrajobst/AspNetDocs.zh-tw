---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
title: 從內容頁與主版頁面互動（VB） |Microsoft Docs
author: rick-anderson
description: 從 [內容] 頁面中的程式碼，檢查如何呼叫主版頁面的方法、設定屬性等等。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 081fe010-ba0f-4e7d-b4ba-774840b601c2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
msc.type: authoredcontent
ms.openlocfilehash: fe1f7b80b26ff25c1ce744e4f823e3fb35eea074
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548213"
---
# <a name="interacting-with-the-master-page-from-the-content-page-vb"></a>從內容頁面與主版頁互動 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_VB.zip)或[下載 PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_VB.pdf)

> 從 [內容] 頁面中的程式碼，檢查如何呼叫主版頁面的方法、設定屬性等等。

## <a name="introduction"></a>簡介

在過去五個教學課程中，我們探討了如何建立主版頁面、定義內容區域、將 ASP.NET 網頁系結至主版頁面，以及定義頁面特定內容。 當訪客要求特定的內容頁面時，內容和主版頁面的標記會在執行時間進行融合，導致整合控制項階層的呈現。 因此，我們已經看過主版頁面和其中一個內容頁面可以互動的方式： [內容] 頁面會將標記拼寫為 transfuse 至主版頁面的 ContentPlaceHolder 控制項。

我們還必須檢查主版頁面和內容頁面如何以程式設計方式進行互動。 除了定義主版頁面的 ContentPlaceHolder 控制項標記以外，[內容] 頁面也可以將值指派給其主版頁面的公用屬性，並叫用其公用方法。 同樣地，主版頁面也可以與其內容頁面互動。 雖然主要和內容頁面之間的程式設計互動不如其宣告式標記之間的互動，但是在許多情況下都需要這類的程式設計互動。

在本教學課程中，我們會檢查內容頁面如何以程式設計方式與主版頁面互動;在下一個教學課程中，我們將探討主版頁面如何與內容頁面互動。

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>內容頁與主版頁面之間的程式設計互動範例

當頁面的特定區域需要以逐頁進行設定時，我們會使用 ContentPlaceHolder 控制項。 但是，大部分的頁面需要發出特定輸出，但少數頁面需要自訂以顯示其他內容的情況呢？ 我們在[*多 ContentPlaceHolders 和預設內容*](multiple-contentplaceholders-and-default-content-vb.md)教學課程中檢查過的其中一個範例，牽涉到在每個頁面上顯示登入介面。 雖然大部分的頁面都應該包含登入介面，但應該隱藏幾個頁面，例如：主要登入頁面（`Login.aspx`）;[建立帳戶] 頁面;和其他僅供已驗證的使用者存取的頁面。 [*多 ContentPlaceHolders 和預設內容*](multiple-contentplaceholders-and-default-content-vb.md)教學課程示範如何在主版頁面中定義 ContentPlaceHolder 的預設內容，以及如何在不需要預設內容的頁面中覆寫它。

另一個選項是在主版頁面中建立公用屬性或方法，以指出是否要顯示或隱藏登入介面。 例如，主版頁面可能包含名為 `ShowLoginUI` 的公用屬性，其值是用來設定主版頁面中登入控制項的 `Visible` 屬性。 應隱藏登入使用者介面的內容頁面，可以透過程式設計的方式，將 `ShowLoginUI` 屬性設定為 `False`。

當主版頁面中顯示的資料需要在 [內容] 頁面中過了後重新整理時，可能會發生最常見的內容和主版頁面互動範例。 假設有一個包含 GridView 的主版頁面，其中顯示來自特定資料庫資料表的五個最近新增的記錄，而且其中一個內容頁麵包含一個介面，可將新記錄加入至同一個資料表。

當使用者造訪頁面以新增記錄時，她會看到最近新增的五筆記錄顯示在主版頁面中。 填入新記錄之資料行的值之後，她提交表單。 假設主版頁面中的 GridView 將其 `EnableViewState` 屬性設為 True （預設值），則會從 view 狀態重載其內容，因此，即使剛將較新的記錄新增至資料庫，也會顯示五筆相同的記錄。 這可能會造成使用者的混淆。

> [!NOTE]
> 即使您停用 GridView 的 view 狀態，使其在每次回傳時重新系結至其基礎資料來源，它仍然不會顯示剛剛加入的記錄，因為資料會系結至比新記錄新增至 datab 時更早在頁面生命週期中的 GridViewase.

若要解決此問題，使剛加入的記錄在回傳時顯示在主版頁面的 GridView 中，我們需要在新記錄新增至資料庫*之後*，指示 GridView 重新系結至其資料來源。 這需要在內容和主版頁面之間進行互動，因為用於新增新記錄（及其事件處理常式）的介面位於 [內容] 頁面中，但需要重新整理的 GridView 是在主版頁面中。

因為從內容頁面中的事件處理常式重新整理主版頁面的顯示是內容和主版頁面互動的最常見需求之一，所以讓我們更詳細地探索這個主題。 本教學課程的下載包含網站 `App_Data` 資料夾中名為 `NORTHWIND.MDF` 的 Microsoft SQL Server 2005 Express Edition 資料庫。 Northwind 資料庫會儲存一家虛構公司 Northwind 商貿的產品、員工和銷售資訊。

步驟1會逐步解說如何在主版頁面中顯示 GridView 的五個最近新增的產品。 步驟2會建立用於加入新產品的內容頁面。 步驟3探討如何在主版頁面中建立公用屬性和方法，而步驟4則說明如何以程式設計方式，從 [內容] 頁面使用這些屬性和方法進行介面化。

> [!NOTE]
> 本教學課程不會深入探討在 ASP.NET 中使用資料的細節。 設定主版頁面以顯示資料和 [內容] 頁面以進行插入資料的步驟已完成，但已 breezy。 若要深入瞭解如何顯示及插入資料，以及如何使用 SqlDataSource 和 GridView 控制項，請參閱本教學課程結尾的進一步閱讀一節中的資源。

## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>步驟1：在主版頁面中顯示五個最近新增的產品

開啟 [網站] 主版頁面，並將標籤和 GridView 控制項新增至 `leftContent` `<div>`。 清除標籤的 [`Text`] 屬性，將其 [`EnableViewState`] 屬性設為 [`False`]，並將其 `ID` 屬性設定為 [`GridMessage`]。將 GridView 的 `ID` 屬性設定為 [`RecentProducts`]。 接下來，從設計工具展開 GridView 的智慧標籤，並選擇將其系結至新的資料來源。 這會啟動 [資料來源設定向導]。 由於 [`App_Data`] 資料夾中的 Northwind 資料庫是 Microsoft SQL Server 資料庫，因此請選擇建立 SqlDataSource，方法是選取（請參閱 [圖 1]）。將 SqlDataSource 命名為 `RecentProductsDataSource`。

[![將 GridView 系結至名為 RecentProductsDataSource 的 SqlDataSource 控制項](interacting-with-the-master-page-from-the-content-page-vb/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image1.png)

**圖 01**：將 GridView 系結至名為 `RecentProductsDataSource` 的 SqlDataSource 控制項（[按一下以查看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image3.png)）

下一個步驟會要求我們指定要連接的資料庫。 從下拉式清單中選擇 [`NORTHWIND.MDF` 資料庫檔案]，然後按 [下一步]。 因為這是我們第一次使用此資料庫，所以嚮導會提供將連接字串儲存在 `Web.config`中。 讓它使用名稱 `NorthwindConnectionString`來儲存連接字串。

[![連接到 Northwind 資料庫](interacting-with-the-master-page-from-the-content-page-vb/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image4.png)

**圖 02**：連接到 Northwind 資料庫（[按一下以觀看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image6.png)）

[設定資料來源] 嚮導會提供兩種方法，讓我們指定用來抓取資料的查詢：

- 藉由指定自訂 SQL 語句或預存程式，或
- 藉由挑選資料表或視圖，然後指定要傳回的資料行

因為我們只想要傳回五個最近新增的產品，所以我們需要指定自訂的 SQL 語句。 使用下列 `SELECT` 查詢：

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample1.sql)]

`TOP 5` 關鍵字只會傳回查詢中的前五筆記錄。 `Products` 資料表的主鍵（`ProductID`）是 `IDENTITY` 的資料行，可確保新增至資料表的每個新產品都有比前一個專案更大的值。 因此，依 `ProductID` 以遞減順序排序結果，會傳回從最近建立的產品開始。

[![傳回最近新增的五個產品](interacting-with-the-master-page-from-the-content-page-vb/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image7.png)

**圖 03**：傳回最近新增的五個產品（[按一下以觀看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image9.png)）

完成 wizard 之後，Visual Studio 會為 GridView 產生兩個 BoundFields，以顯示從資料庫傳回的 `ProductName` 和 `UnitPrice` 欄位。 此時，主版頁面的宣告式標記應該包含類似下列的標記：

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample2.aspx)]

如您所見，標記包含：標籤 Web 控制項（`GridMessage`）;GridView `RecentProducts`，有兩個 BoundFields;和 SqlDataSource 控制項，它會傳回最近新增的五個產品。

建立此 GridView 並設定其 SqlDataSource 控制項之後，請透過瀏覽器造訪網站。 如 [圖 4] 所示，您會在左下角看到一個方格，其中列出五個最近新增的產品。

[![GridView 會顯示最近新增的五個產品](interacting-with-the-master-page-from-the-content-page-vb/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image10.png)

**圖 04**： GridView 會顯示最近新增的五個產品（[按一下以觀看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image12.png)）

> [!NOTE]
> 請隨意清除 GridView 的外觀。 某些建議包括將顯示的 `UnitPrice` 值格式化為貨幣，以及使用背景色彩和字型來改善方格的外觀。

## <a name="step-2-creating-a-content-page-to-add-new-products"></a>步驟2：建立內容頁面以新增產品

我們的下一個工作是建立一個內容頁面，讓使用者可以從中將新產品加入 `Products` 資料表。 將新的 [內容] 頁面新增至名為 `AddProduct.aspx`的 `Admin` 資料夾，並務必將它系結至 `Site.master` 主版頁面。 [圖 5] 顯示此頁面新增至網站後的方案總管。

[![將新的 ASP.NET 網頁新增至管理資料夾](interacting-with-the-master-page-from-the-content-page-vb/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image13.png)

**圖 05**：將新的 [ASP.NET] 頁面新增至 [`Admin`] 資料夾（[按一下以查看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image15.png)）

回想一下，在[*主版頁面教學課程中指定標題、中繼標記和其他 HTML 標頭*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)時，我們建立了名為 `BasePage` 的自訂基底頁面類別，如果未明確設定，則會產生頁面標題。 移至 `AddProduct.aspx` 頁面的程式碼後置類別，並讓它衍生自 `BasePage` （而不是從 `System.Web.UI.Page`）。

最後，更新 `Web.sitemap` 檔案以包含此課程的專案。 在 [控制項 ID 命名問題] 課程的 `<siteMapNode>` 下方新增下列標記：

[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample3.xml)]

如 [圖 6] 所示，加入此 `<siteMapNode>` 元素會反映在課程清單中。

返回 `AddProduct.aspx`。 在 [`MainContent` ContentPlaceHolder] 的內容控制項中，新增 DetailsView 控制項並將其命名為 `NewProduct`。 將 DetailsView 系結至名為 `NewProductDataSource`的新 SqlDataSource 控制項。 如同步驟1中的 SqlDataSource，請設定 wizard，讓它使用 Northwind 資料庫，然後選擇指定自訂的 SQL 語句。 因為 DetailsView 將用來將專案加入至資料庫，所以我們需要同時指定 `SELECT` 語句和 `INSERT` 語句。 使用下列 `SELECT` 查詢：

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample4.sql)]

然後，在 [插入] 索引標籤中，新增下列 `INSERT` 語句：

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample5.sql)]

完成嚮導之後，請移至 DetailsView 的智慧標籤，然後勾選 [啟用插入] 核取方塊。 這會將 CommandField 新增至 DetailsView，並將其 `ShowInsertButton` 屬性設定為 True。 由於此 DetailsView 只會用於插入資料，因此請將 DetailsView 的 `DefaultMode` 屬性設定為 `Insert`。

這樣就全部完成了！ 讓我們來測試此頁面。 請透過瀏覽器造訪 `AddProduct.aspx`、輸入名稱和價格（請參閱 [圖 6]）。

[![將新產品新增至資料庫](interacting-with-the-master-page-from-the-content-page-vb/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image16.png)

**圖 06**：將新產品新增至資料庫（[按一下以觀看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image18.png)）

輸入新產品的名稱和價格之後，請按一下 [插入] 按鈕。 這會導致表單回傳。 在回傳時，會執行 SqlDataSource 控制項的 `INSERT` 語句;它的兩個參數會填入使用者在 DetailsView 的兩個 TextBox 控制項中輸入的值。 可惜的是，沒有任何視覺效果的意見反應表示已發生插入。 顯示訊息，確認已加入新記錄是很好的做法。 我將此做為讀者的練習。 此外，從 DetailsView 新增記錄之後，主頁面中的 GridView 仍然會顯示與之前相同的五筆記錄;它不包含剛新增的記錄。 我們將在接下來的步驟中探討如何解決此問題。

> [!NOTE]
> 除了新增某種形式的視覺效果意見反應，插入已成功，我也建議您也更新 DetailsView 的插入介面，以包含驗證。 目前沒有驗證。 如果使用者在 [`UnitPrice`] 欄位中輸入不正確值，例如「太昂貴」，當系統嘗試將該字串轉換成十進位時，就會在回傳時擲回例外狀況（exception）。 如需自訂插入介面的詳細資訊，請參閱[使用資料教學課程系列](../../data-access/index.md)中的[*自訂資料修改介面*教學](https://asp.net/learn/data-access/tutorial-20-vb.aspx)課程。

## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>步驟3：在主版頁面中建立公用屬性和方法

在步驟1中，我們已在主版頁面中，將名為 `GridMessage` 的標籤 Web 控制項新增至 GridView。 此標籤的目的是要選擇性地顯示訊息。 例如，將新記錄加入至 `Products` 資料表之後，我們可能會想要顯示訊息：「*ProductName*已新增至資料庫」。 我們不會在主版頁面中將此標籤的文字硬式編碼，而是要讓 [內容] 頁面可以自訂該訊息。

因為 Label 控制項會實作為主版頁面中受保護的成員變數，所以無法直接從內容頁面存取。 若要從 [內容] 頁面使用主版頁面內的標籤（也就是，在主版頁面中的任何 Web 控制項），我們必須在主版頁面中建立公開該 Web 控制項的公用屬性，或作為其其中一個屬性可為的 proxy 存取. 將下列語法新增至主版頁面的程式碼後置類別，以公開卷標的 `Text` 屬性：

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample6.vb)]

從內容頁面將新的記錄新增至 `Products` 資料表時，主版頁面中的 `RecentProducts` GridView 必須重新系結至其基礎資料來源。 若要重新系結 GridView，請呼叫其 `DataBind` 方法。 因為主版頁面中的 GridView 無法以程式設計方式存取內容頁面，所以我們需要在主版頁面中建立公用方法，當呼叫它時，會將資料重新系結至 GridView。 將下列方法新增至主版頁面的程式碼後置類別：

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample7.vb)]

當 `GridMessageText` 屬性和 `RefreshRecentProductsGrid` 方法備妥時，任何內容頁面都可以透過程式設計方式設定或讀取 `GridMessage` 標籤 `Text` 屬性的值，或將資料重新系結至 `RecentProducts` GridView。 步驟4會檢查如何從內容頁面存取主版頁面的公用屬性和方法。

> [!NOTE]
> 別忘了將主版頁面的屬性和方法標示為 `Public`。 如果您未明確將這些屬性和方法表示為 `Public`，就無法從 [內容] 頁面存取它們。

## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>步驟4：從內容頁面呼叫主版頁面的公用成員

既然主版頁面具有必要的公用屬性和方法，我們就準備好從 `AddProduct.aspx` 內容頁面叫用這些屬性和方法。 具體而言，我們需要設定主版頁面的 `GridMessageText` 屬性，並在新產品新增至資料庫之後，呼叫其 `RefreshRecentProductsGrid` 方法。 所有的 ASP.NET 資料 Web 控制項都會在完成各種工作之前和之後引發事件，讓網頁開發人員輕鬆地在工作之前或之後採取一些程式設計動作。 例如，當使用者按一下 DetailsView 的 [插入] 按鈕時，在回傳時，DetailsView 會在開始插入工作流程之前引發其 `ItemInserting` 事件。 然後，它會將記錄插入資料庫中。 之後，DetailsView 會引發它的 `ItemInserted` 事件。 因此，若要在新增產品之後使用主版頁面，請為 DetailsView 的 `ItemInserted` 事件建立事件處理常式。

有兩種方式可讓內容頁面以程式設計方式與主版頁面互動：

- 使用 `Page.Master` 屬性，它會將鬆散類型的參考傳回主版頁面，或
- 透過 `@MasterType` 指示詞指定頁面的主版頁面類型或檔案路徑;這會自動將強型別屬性加入至名為 `Master`的頁面。

讓我們來探討這兩種方法。

### <a name="using-the-loosely-typedpagemasterproperty"></a>使用鬆散類型的`Page.Master`屬性

所有 ASP.NET 的網頁都必須衍生自位於 `System.Web.UI` 命名空間的 `Page` 類別。 `Page` 類別包含[`Master` 屬性](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx)，可傳回頁面主版頁面的參考。 如果頁面沒有主版頁面 `Master` 會傳回 `Nothing`。

`Master` 屬性會傳回類型為[`MasterPage`](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) （也位於 `System.Web.UI` 命名空間）的物件，這是所有主頁面衍生來源的基底類型。 因此，若要使用在網站主版頁面中定義的公用屬性或方法，我們必須將從 `Master` 屬性傳回的 `MasterPage` 物件，轉換為適當的型別。 因為我們將主版分頁檔命名為 `Site.master`，所以程式碼後置類別的名稱 `Site`。 因此，下列程式碼會將 `Page.Master` 屬性轉換為 `Site` 類別的實例。

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample8.vb)]

既然我們已將鬆散類型的 `Page.Master` 屬性轉換至網站類型，我們就可以參考網站特定的屬性和方法。 如 [圖 7] 所示，[公用] 屬性 `GridMessageText` 會出現在 [IntelliSense] 下拉式集中。

[![IntelliSense 顯示主版頁面的公用屬性和方法](interacting-with-the-master-page-from-the-content-page-vb/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image19.png)

**圖 07**： IntelliSense 顯示主版頁面的公用屬性和方法（[按一下以查看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image21.png)）

> [!NOTE]
> 如果您將主版分頁檔命名為 `MasterPage.master` 則會 `MasterPage`主版頁面的程式碼後置類別名稱。 從類型 `System.Web.UI.MasterPage` 轉換成您的 `MasterPage` 類別時，這可能會導致不明確的程式碼。 簡單地說，您必須完整限定要轉換成的類型，這在使用網站專案模型時可能有點困難。 我的建議是確定當您建立主版頁面時，您將它命名為 `MasterPage.master` 或更好的名稱，以建立主版頁面的強型別參考。

### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>使用`@MasterType`指示詞建立強型別參考

如果您仔細查看，您可以看到 ASP.NET 網頁的程式碼後置類別是部分類別（請注意類別定義中的 `Partial` 關鍵字）。 部分類別是在和C# Visual Basic with.NET Framework 2.0 中引進，簡而言之，允許在多個檔案之間定義類別的成員。 程式碼後置類別檔案 `AddProduct.aspx.vb`，例如，包含我們的網頁開發人員所建立的程式碼。 除了我們的程式碼之外，ASP.NET 引擎會在中自動建立具有屬性和事件處理常式的個別類別檔案，將宣告式標記轉譯成頁面的類別階層。

每當流覽 ASP.NET 網頁時，就會產生自動產生程式碼，鋪路一種方法來取得一些有趣且有用的可能性。 在主版頁面的案例中，如果我們告訴 ASP.NET engine 內容頁面正在使用哪一個主版頁面，就會為我們產生強型別 `Master` 屬性。

使用[`@MasterType`](https://msdn.microsoft.com/library/ms228274.aspx)指示詞來通知 ASP.NET 引擎內容頁面的主版頁面類型。 `@MasterType` 指示詞可以接受主版頁面的類型名稱或其檔案路徑。 若要指定 [`AddProduct.aspx`] 頁面使用 `Site.master` 作為其主版頁面，請將下列指示詞新增至 `AddProduct.aspx`的頂端：

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample9.aspx)]

這個指示詞會指示 ASP.NET 引擎透過名為 `Master`的屬性，將強型別參考新增至主版頁面。 備妥 `@MasterType` 指示詞之後，我們就可以直接透過 `Master` 屬性呼叫 `Site.master` 主版頁面的公用屬性和方法，而不需要任何轉換。

> [!NOTE]
> 如果您省略 `@MasterType` 指示詞，語法 `Page.Master` 和 `Master` 會傳回相同的內容：頁面主版頁面的鬆散類型物件。 如果您包含 `@MasterType` 指示詞，則 `Master` 會傳回指定之主版頁面的強型別參考。 不過，`Page.Master`仍會傳回鬆散類型的參考。 如需深入瞭解為什麼會發生這種情況，以及在包含 `@MasterType` 指示詞時如何建立 `Master` 屬性，請參閱[ASP.NET 2.0 中](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)的[Allen](http://odetocode.com/blogs/scott/default.aspx)的 blog 專案`@MasterType`。

### <a name="updating-the-master-page-after-adding-a-new-product"></a>新增新產品後更新主版頁面

既然我們已經知道如何從內容頁面叫用主版頁面的公用屬性和方法，我們就準備好更新 `AddProduct.aspx` 頁面，讓主版頁面在加入新產品之後重新整理。 在步驟4的開頭，我們為 DetailsView 控制項的 `ItemInserting` 事件建立了事件處理常式，這會在新產品新增至資料庫之後立即執行。 將以下程式碼新增至該事件處理常式：

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample10.vb)]

上述程式碼會同時使用鬆散類型的 `Page.Master` 屬性和強型別的 `Master` 屬性。 請注意，`GridMessageText` 屬性會設定為「*ProductName*已加入至方格 ...」剛新增的產品值可透過 `e.Values` 集合來存取;如您所見，剛新增的 `ProductName` 值是透過 `e.Values("ProductName")`來存取。

[圖 8] 顯示了新產品-Scott 的 Soda 之後的 `AddProduct.aspx` 頁面-已新增至資料庫。 請注意，剛新增的產品名稱會在主版頁面的標籤中注明，而 GridView 已重新整理成包含產品和價格。

[![主版頁面的標籤和 GridView 顯示剛新增的產品](interacting-with-the-master-page-from-the-content-page-vb/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image22.png)

**圖 08**：主版頁面的標籤和 GridView 顯示剛新增的產品（[按一下以觀看完整大小的影像](interacting-with-the-master-page-from-the-content-page-vb/_static/image24.png)）

## <a name="summary"></a>總結

在理想情況下，主版頁面和其內容頁面會彼此獨立，而且不需要任何層級的互動。 雖然主版頁面和內容頁面的設計應該要考慮該目標，但有一些常見的情況是內容頁面必須與主版頁面互動。 其中一個最常見的原因，是根據 [內容] 頁面中過了的某個動作，來更新主版頁面顯示的特定部分。

好消息是，讓內容頁面以程式設計方式與主版頁面互動，是相當直接的。 一開始請先在主版頁面中建立公用屬性或方法，以封裝內容頁面必須叫用的功能。 然後，在 [內容] 頁面中，透過鬆散類型的 `Page.Master` 屬性來存取主版頁面的屬性和方法，或使用 `@MasterType` 指示詞來建立主版頁面的強型別參考。

在下一個教學課程中，我們將探討如何讓主版頁面以程式設計方式與其中一個內容頁面互動。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [存取和更新 ASP.NET 中的資料](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 主版頁面：秘訣、訣竅和陷阱](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 2.0 中的 `@MasterType`](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [在內容和主版頁面之間傳遞資訊](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [使用 ASP.NET 教學課程中的資料](../../data-access/index.md)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查員是 Zack 的。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](control-id-naming-in-content-pages-vb.md)
> [下一頁](interacting-with-the-content-page-from-the-master-page-vb.md)
