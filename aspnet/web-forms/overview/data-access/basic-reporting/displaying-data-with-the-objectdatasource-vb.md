---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
title: 使用 ObjectDataSource 顯示資料（VB） |Microsoft Docs
author: rick-anderson
description: 本教學課程會查看使用此控制項的 ObjectDataSource 控制項您可以系結從上一個教學課程中建立的 BLL 抓取的資料，而不需要 havi 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d62c3a63-0940-4019-874e-4a4047df0c1c
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 754188352cbfb08e610027f5b7890a32bd88ae26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597045"
---
# <a name="displaying-data-with-the-objectdatasource-vb"></a>使用 ObjectDataSource 顯示資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_4_VB.exe)或[下載 PDF](displaying-data-with-the-objectdatasource-vb/_static/datatutorial04vb1.pdf)

> 本教學課程探討使用此控制項的 ObjectDataSource 控制項您可以系結從上一個教學課程中建立的 BLL 抓取的資料，而不需要撰寫一行程式碼！

## <a name="introduction"></a>簡介

當我們的應用程式架構和網站頁面配置完成後，我們就準備好開始探索如何完成各種常見的資料和報告相關工作。 在先前的教學課程中，我們已瞭解如何以程式設計方式，將資料從 DAL 和 BLL 系結至 ASP.NET 網頁中的資料 Web 控制項。 這個語法會將資料 Web 控制項的 `DataSource` 屬性指派給要顯示的資料，然後呼叫控制項的 `DataBind()` 方法是 ASP.NET 1.x 應用程式中所使用的模式，而且可以繼續在2.0 應用程式中使用。 不過，ASP.NET 2.0 的新資料來源控制項提供宣告式方式來處理資料。 使用這些控制項，您可以系結從上一個教學課程中建立的 BLL 抓取的資料，而不需要撰寫一行程式碼！

ASP.NET 2.0 隨附五個內建的資料來源控制項[SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)、 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)、 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)、 [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)和[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx) ，不過您可以視需要建立自己的[自訂資料來源控制項](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp)。 由於我們已開發教學課程應用程式的架構，因此我們將針對 BLL 類別使用 ObjectDataSource。

![ASP.NET 2.0 包含五個內建的資料來源控制項](displaying-data-with-the-objectdatasource-vb/_static/image1.png)

**圖 1**： ASP.NET 2.0 包含五個內建的資料來源控制項

ObjectDataSource 做為使用其他物件的 proxy。 若要設定 ObjectDataSource，我們會指定此基礎物件，以及其方法如何對應至 ObjectDataSource 的 `Select`、`Insert`、`Update`和 `Delete` 方法。 一旦指定此基礎物件，並將其方法對應至 ObjectDataSource 的之後，我們就可以將 ObjectDataSource 系結至資料 Web 控制項。 ASP.NET 隨附許多資料 Web 控制項，包括 GridView、DetailsView、RadioButtonList 和 DropDownList，還有其他。 在頁面生命週期期間，資料 Web 控制項可能需要存取其所系結的資料，這會藉由叫用其 ObjectDataSource 的 `Select` 方法來完成。如果資料 Web 控制項支援插入、更新或刪除，則可能會對其 ObjectDataSource 的 `Insert`、`Update`或 `Delete` 方法進行呼叫。 然後，ObjectDataSource 會將這些呼叫路由至適當的基礎物件方法，如下圖所示。

[![ObjectDataSource 作為 Proxy](displaying-data-with-the-objectdatasource-vb/_static/image3.png)](displaying-data-with-the-objectdatasource-vb/_static/image2.png)

**圖 2**： ObjectDataSource 作為 Proxy （[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image4.png)）

雖然 ObjectDataSource 可用來叫用插入、更新或刪除資料的方法，但讓我們只著重于傳回資料。未來的教學課程將使用可修改資料的 ObjectDataSource 和資料 Web 控制項來進行探索。

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>步驟1：新增和設定 ObjectDataSource 控制項

首先，開啟 [`BasicReporting`] 資料夾中的 [`SimpleDisplay.aspx`] 頁面，切換至 [設計檢視]，然後將 [ObjectDataSource] 控制項從 [工具箱] 拖曳至頁面的設計介面上。 ObjectDataSource 會在設計介面上顯示為灰色方塊，因為它不會產生任何標記;它只會從指定的物件叫用方法來存取資料。 ObjectDataSource 所傳回的資料可以由資料 Web 控制項（例如 GridView、DetailsView、FormView 等等）顯示。

> [!NOTE]
> 或者，您可以先將資料 Web 控制項加入至頁面，然後從其智慧標籤，選擇下拉式清單中的 [&lt;新資料來源&gt;] 選項。

若要指定 ObjectDataSource 的基礎物件，以及該物件的方法如何對應到 ObjectDataSource，請按一下 ObjectDataSource 的智慧標籤中的 [設定資料來源] 連結。

[![按一下智慧標籤中的 [設定資料來源] 連結](displaying-data-with-the-objectdatasource-vb/_static/image6.png)](displaying-data-with-the-objectdatasource-vb/_static/image5.png)

**圖 3**：按一下智慧標籤中的 [設定資料來源] 連結（[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image7.png)）

這會顯示 [設定資料來源] wizard。 首先，我們必須指定 ObjectDataSource 要使用的物件。 如果已核取 [只顯示資料元件] 核取方塊，則此畫面上的下拉式清單只會列出已使用 `DataObject` 屬性裝飾的物件。 目前，我們的清單包含具類型資料集的 Tableadapter，以及我們在上一個教學課程中建立的 BLL 類別。 如果您忘記將 `DataObject` 屬性新增到商務邏輯層類別，就不會在這份清單中看到它們。 在這種情況下，請取消核取 [只顯示資料元件] 核取方塊，以查看所有物件，其中應包含 BLL 類別（以及 Datatable、Datarow 等等的具類型資料集內的其他類別）。

在第一個畫面上，從下拉式清單中選擇 [`ProductsBLL`] 類別，然後按 [下一步]。

[![指定要搭配 ObjectDataSource 控制項使用的物件](displaying-data-with-the-objectdatasource-vb/_static/image9.png)](displaying-data-with-the-objectdatasource-vb/_static/image8.png)

**圖 4**：指定要搭配 ObjectDataSource 控制項使用的物件（[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image10.png)）

Wizard 中的下一個畫面會提示您選取 ObjectDataSource 應叫用的方法。 下拉式清單會列出從上一個畫面中選取的物件中傳回資料的方法。 在這裡，我們會看到 `GetProductByProductID`、`GetProducts`、`GetProductsByCategoryID`和 `GetProductsBySupplierID`。 從下拉式清單中選取 [`GetProducts`] 方法，然後按一下 [完成] （如果您已將 `DataObjectMethodAttribute` 新增至 `ProductBLL`的方法（如先前的教學課程所示），則預設會選取此選項）。

[![選擇從 [選取] 索引標籤傳回資料的方法](displaying-data-with-the-objectdatasource-vb/_static/image12.png)](displaying-data-with-the-objectdatasource-vb/_static/image11.png)

**圖 5**：選擇從 [選取] 索引標籤傳回資料的方法（[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image13.png)）

## <a name="configure-the-objectdatasource-manually"></a>手動設定 ObjectDataSource

ObjectDataSource 的 [設定資料來源] wizard 提供快速的方法來指定它所使用的物件，以及關聯要叫用的物件方法。 不過，您可以透過屬性視窗或直接在宣告式標記中，透過其屬性來設定 ObjectDataSource。 只需將 `TypeName` 屬性設為要使用之基礎物件的類型，並將 `SelectMethod` 設定為要在抓取資料時叫用的方法。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample1.aspx)]

即使您偏好使用 [設定資料來源]，也可能需要手動設定 ObjectDataSource，因為 wizard 只會列出開發人員所建立的類別。 如果您想要將 ObjectDataSource 系結至 .NET Framework 中的類別，例如[成員資格類別](https://msdn.microsoft.com/library/system.web.security.membership.aspx)、存取使用者帳戶資訊，或使用[目錄類別](https://msdn.microsoft.com/library/system.io.directory.aspx)來處理檔案系統資訊，您將需要手動設定 ObjectDataSource 的屬性。

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>步驟2：加入資料 Web 控制項並將它系結至 ObjectDataSource

一旦將 ObjectDataSource 新增至頁面並設定之後，我們就可以將資料 Web 控制項加入至頁面，以顯示 ObjectDataSource 的 `Select` 方法所傳回的資料。 任何資料 Web 控制項都可以系結至 ObjectDataSource;讓我們看看如何在 GridView、DetailsView 和 FormView 中顯示 ObjectDataSource 的資料。

## <a name="binding-a-gridview-to-the-objectdatasource"></a>將 GridView 系結至 ObjectDataSource

從 [工具箱] 將 GridView 控制項新增至 `SimpleDisplay.aspx`的設計介面。 從 GridView 的智慧標籤中，選擇我們在步驟1中新增的 ObjectDataSource 控制項。 這會在 GridView 中針對資料從 ObjectDataSource 的 `Select` 方法（也就是 Products DataTable 所定義的屬性）傳回的每個屬性，自動建立一個 BoundField。

[![GridView 已加入至頁面，並系結至 ObjectDataSource](displaying-data-with-the-objectdatasource-vb/_static/image15.png)](displaying-data-with-the-objectdatasource-vb/_static/image14.png)

**圖 6**： GridView 已加入至頁面，並系結至 ObjectDataSource （[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image16.png)）

接著，您可以從智慧標籤按一下 [編輯資料行] 選項，以自訂、重新排列或移除 GridView 的 BoundFields。

[![透過 [編輯資料行] 對話方塊來管理 GridView 的 BoundFields](displaying-data-with-the-objectdatasource-vb/_static/image18.png)](displaying-data-with-the-objectdatasource-vb/_static/image17.png)

**圖 7**：透過 [編輯資料行] 對話方塊來管理 GridView 的 BoundFields （[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image19.png)）

請花一些時間修改 GridView 的 BoundFields，移除 `ProductID`、`SupplierID`、`CategoryID`、`QuantityPerUnit`、`UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` BoundFields。 只要從左下方的清單中選取 [BoundField]，然後按一下 [刪除] 按鈕（紅色 X）來移除它們。 接下來，重新排列 BoundFields，讓 `CategoryName` 和 `SupplierName` BoundFields 在 `UnitPrice` BoundField 前面選取這些 BoundFields，然後按一下向上箭號。 將其餘 BoundFields 的 `HeaderText` 屬性分別設定為 `Products`、`Category`、`Supplier`和 `Price`。 接下來，將 BoundField 的 [`HtmlEncode`] 屬性設為 False，並將其 `DataFormatString` 屬性設定為 [`{0:c}`]，以將 `Price` BoundField 格式化為貨幣。 最後，透過 [`ItemStyle`/`HorizontalAlign`] 屬性，水準對齊 `Price` 和中心的 [`Discontinued`] 核取方塊。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

[![GridView 的 BoundFields 已自訂](displaying-data-with-the-objectdatasource-vb/_static/image21.png)](displaying-data-with-the-objectdatasource-vb/_static/image20.png)

**圖 8**： GridView 的 BoundFields 已經過自訂（[按一下以觀看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image22.png)）

## <a name="using-themes-for-a-consistent-look"></a>使用主題進行一致的外觀

這些教學課程致力於移除任何控制層級的樣式設定，而不是盡可能使用外部檔案中定義的級聯樣式表。 `Styles.css` 檔案包含 `DataWebControlStyle`、`HeaderStyle`、`RowStyle`和 `AlternatingRowStyle` CSS 類別，這些類別應該用來指定這些教學課程中所使用之資料 Web 控制項的外觀。 為了達成此目的，我們可以將 GridView 的 `CssClass` 屬性設定為 `DataWebControlStyle`，並據此將其 `HeaderStyle`、`RowStyle`和 `AlternatingRowStyle` 屬性的 `CssClass` 屬性。

如果我們在 Web 控制項上設定這些 `CssClass` 屬性，我們必須記得針對新增至教學課程的每一個資料 Web 控制項，明確設定這些屬性值。 更容易管理的方法，是使用主題來定義 GridView、DetailsView 和 FormView 控制項的預設 CSS 相關屬性。 主題是控制項層級屬性設定、影像和 CSS 類別的集合，可套用至網站上的頁面，以強制執行常見的外觀與風格。

我們的主題不會包含任何影像或 CSS 檔案（我們會在 web 應用程式的根資料夾中定義樣式表單 `Styles.css`，但會包含兩個外觀）。 「面板」是一種檔案，可定義 Web 控制項的預設屬性。 具體而言，我們會有 GridView 和 DetailsView 控制項的面板檔案，表示預設 `CssClass`相關的屬性。

首先，在 方案總管中的專案名稱上按一下滑鼠右鍵，然後選擇 加入新專案，以將新的面板檔案新增至名為 `GridView.skin` 的專案。

[![新增名為 GridView 的外觀檔](displaying-data-with-the-objectdatasource-vb/_static/image24.png)](displaying-data-with-the-objectdatasource-vb/_static/image23.png)

**圖 9**：新增名為 `GridView.skin` 的面板檔案（[按一下以觀看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image25.png)）

面板檔案必須放在位於 [`App_Themes`] 資料夾中的主題中。 因為我們還沒有這類資料夾，所以當您新增第一個面板時，Visual Studio 會提供給我們。 按一下 [是] 建立 `App_Theme` 資料夾，並將新的 `GridView.skin` 檔案放到該處。

[![讓 Visual Studio 建立 App_Theme 資料夾](displaying-data-with-the-objectdatasource-vb/_static/image27.png)](displaying-data-with-the-objectdatasource-vb/_static/image26.png)

**圖 10**：讓 Visual Studio 建立 `App_Theme` 資料夾（[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image28.png)）

這會在名為 GridView 的 `App_Themes` 資料夾中，使用面板檔案 `GridView.skin`建立新的主題。

![GridView 主題已新增至 [App_Theme] 資料夾](displaying-data-with-the-objectdatasource-vb/_static/image29.png)

**圖 11**： GridView 主題已新增至 [`App_Theme`] 資料夾

將 GridView 主題重新命名為 DataWebControls （以滑鼠右鍵按一下 [`App_Theme`] 資料夾中的 [GridView] 資料夾，然後選擇 [重新命名]）。 接下來，在 `GridView.skin` 檔案中輸入下列標記：

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample3.aspx)]

這會在任何使用 DataWebControls 主題的頁面中，為任何 GridView 定義 `CssClass`相關屬性的預設屬性。 讓我們為 DetailsView 新增另一個外觀，這是我們很快就會用到的資料 Web 控制項。 將新的外觀新增至名為 `DetailsView.skin` 的 DataWebControls 主題，並新增下列標記：

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample4.aspx)]

定義主題之後，最後一個步驟是將主題套用至我們的 ASP.NET 網頁。 主題可以逐頁或網站中的所有網頁來套用。 讓我們將此主題用於網站中的所有頁面。 若要完成這項操作，請將下列標記新增至 `Web.config`的 `<system.web>` 區段：

[!code-xml[Main](displaying-data-with-the-objectdatasource-vb/samples/sample5.xml)]

這樣就全部完成了！ `styleSheetTheme` 設定表示主題中指定的屬性*不*應該覆寫在控制項層級指定的屬性。 若要指定主題設定應該王牌控制設定，請使用 `theme` 屬性來取代 `styleSheetTheme`;可惜的是，主題設定不會出現在 Visual Studio 設計檢視中。 如需主題和外觀的詳細資訊，請參閱[ASP.NET 主題和麵板總覽](https://msdn.microsoft.com/library/ykzx33wh.aspx)和[伺服器端樣式](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)。如需設定頁面以使用主題的詳細資訊，請參閱 how [To： Apply ASP.NET 主題](https://msdn.microsoft.com/library/0yy5hxdk%28VS.80%29.aspx)。

[![GridView 會顯示產品的名稱、類別、供應商、價格和已停止的資訊](displaying-data-with-the-objectdatasource-vb/_static/image31.png)](displaying-data-with-the-objectdatasource-vb/_static/image30.png)

**圖 12**： GridView 會顯示產品的名稱、類別、供應商、價格和已停止的資訊（[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image32.png)）

## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>在 DetailsView 中一次顯示一筆記錄

GridView 會針對其所系結的資料來源控制項所傳回的每一筆記錄，各顯示一個資料列。 不過，有時候我們可能會想要一次顯示一筆記錄，或只顯示一筆記錄。 [DetailsView 控制項](https://msdn.microsoft.com/library/s3w1w7t4.aspx)提供這項功能，並以 HTML `<table>` 呈現，其中包含兩個數據行，以及一個資料列代表系結至控制項的每個資料行或屬性。 您可以將 DetailsView 視為具有旋轉90度之單一記錄的 GridView。

一開始請先在 `SimpleDisplay.aspx`的 GridView*上方*新增 DetailsView 控制項。 接下來，將它系結至與 GridView 相同的 ObjectDataSource 控制項。 就像 GridView 一樣，BoundField 會針對 ObjectDataSource 的 `Select` 方法所傳回之物件中的每個屬性加入 DetailsView。 唯一的差別在於 DetailsView 的 BoundFields 是以水準方式配置，而不是垂直版面配置。

[![將 DetailsView 新增至頁面，並將其系結至 ObjectDataSource](displaying-data-with-the-objectdatasource-vb/_static/image34.png)](displaying-data-with-the-objectdatasource-vb/_static/image33.png)

**圖 13**：將 DetailsView 新增至頁面，並將它系結至 ObjectDataSource （[按一下以觀看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image35.png)）

就像 GridView 一樣，DetailsView 的 BoundFields 可以調整，以提供更自訂的 ObjectDataSource 所傳回資料的顯示。 [圖 14] 顯示 BoundFields 之後的 DetailsView，並已設定 `CssClass` 屬性，使其外觀與 GridView 範例類似。

[![DetailsView 顯示單一記錄](displaying-data-with-the-objectdatasource-vb/_static/image37.png)](displaying-data-with-the-objectdatasource-vb/_static/image36.png)

**圖 14**： DetailsView 顯示單一記錄（[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image38.png)）

請注意，DetailsView 只會顯示其資料來源所傳回的第一筆記錄。 若要讓使用者一次逐步執行所有記錄，我們必須啟用 DetailsView 的分頁。 若要這麼做，請返回 Visual Studio，然後勾選 DetailsView 的智慧標籤中的 [啟用分頁] 核取方塊。

[![在 DetailsView 控制項中啟用分頁](displaying-data-with-the-objectdatasource-vb/_static/image40.png)](displaying-data-with-the-objectdatasource-vb/_static/image39.png)

**圖 15**：啟用 DetailsView 控制項中的分頁功能（[按一下以查看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image41.png)）

[已啟用分頁的 ![，DetailsView 可讓使用者查看任何產品](displaying-data-with-the-objectdatasource-vb/_static/image43.png)](displaying-data-with-the-objectdatasource-vb/_static/image42.png)

**圖 16**：啟用分頁時，DetailsView 可讓使用者查看任何產品（[按一下以觀看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image44.png)）

我們將在未來的教學課程中進一步討論分頁。

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>一次顯示一筆記錄的彈性版面配置

DetailsView 會非常嚴格地顯示從 ObjectDataSource 傳回的每一筆記錄。 我們可能會想要更有彈性的資料檢視。 例如，不會在個別的資料列上顯示產品的名稱、類別、供應商、價格和已停止的資訊，我們可能會想要在 `<h4>` 標題中顯示產品名稱和價格，並以較小的字型大小在名稱和價格底下顯示 [類別] 和 [供應商] 資訊。 而且，我們可能不在意在值旁邊顯示內容名稱（Product、Category 等等）。

[FormView 控制項](https://msdn.microsoft.com/library/fyf1dk77.aspx)提供此層級的自訂。 FormView 不會使用欄位（例如 GridView 和 DetailsView），而是使用範本，允許混合 Web 控制項、靜態 HTML 和資料系結[語法](http://www.15seconds.com/issue/040630.htm)。 如果您熟悉 ASP.NET 1.x 的中繼器控制項，您可以將 FormView 視為用於顯示單一記錄的中繼器。

將 FormView 控制項加入至 `SimpleDisplay.aspx` 頁面的設計介面。 一開始，FormView 會顯示為灰色區塊，通知我們至少需要提供控制項的 `ItemTemplate`。

[![FormView 必須包含 ItemTemplate](displaying-data-with-the-objectdatasource-vb/_static/image46.png)](displaying-data-with-the-objectdatasource-vb/_static/image45.png)

**圖 17**： FormView 必須包含 `ItemTemplate` （[按一下以觀看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image47.png)）

您可以透過 FormView 的智慧標籤，將 FormView 直接系結至資料來源控制項，如果已設定 ObjectDataSource 控制項的 `InsertMethod` 和 `UpdateMethod` 屬性，則會自動建立預設 `ItemTemplate` （連同 `EditItemTemplate` 並 `InsertItemTemplate`。 不過，在此範例中，讓我們將資料系結至 FormView，並手動指定其 `ItemTemplate`。 首先，將 FormView 的 `DataSourceID` 屬性設定為 ObjectDataSource 控制項的 `ID`，`ObjectDataSource1`。 接下來，建立 `ItemTemplate`，讓它在 `<h4>` 專案中顯示產品的名稱和價格，並在較小的字型大小中顯示其底下的類別和貨主名稱。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample6.aspx)]

[![第一個產品（Chai）會以自訂格式顯示](displaying-data-with-the-objectdatasource-vb/_static/image49.png)](displaying-data-with-the-objectdatasource-vb/_static/image48.png)

**圖 18**：第一個產品（Chai）會以自訂格式顯示（[按一下以觀看完整大小的影像](displaying-data-with-the-objectdatasource-vb/_static/image50.png)）

`<%# Eval(propertyName) %>` 是資料系結語法。 `Eval` 方法會傳回目前物件系結至 FormView 控制項之指定屬性的值。 如需資料系結的細節和詳細資訊，請參閱 Alex Homer 的文章[中的簡化和擴充的資料系結語法 ASP.NET 2.0](http://www.15seconds.com/issue/040630.htm) 。

就像 DetailsView 一樣，FormView 只會顯示從 ObjectDataSource 傳回的第一筆記錄。 您可以在 FormView 中啟用分頁功能，讓訪客一次逐步執行一項產品。

## <a name="summary"></a>總結

從商務邏輯層存取和顯示資料，不需要撰寫任何程式碼就能完成，而是感謝 ASP.NET 2.0 的 ObjectDataSource 控制項。 ObjectDataSource 會叫用類別的指定方法，並傳回結果。 這些結果可以在系結至 ObjectDataSource 的資料 Web 控制項中顯示。 在本教學課程中，我們探討了如何將 GridView、DetailsView 和 FormView 控制項系結至 ObjectDataSource。

到目前為止，我們只看過如何使用 ObjectDataSource 叫用無參數的方法，但如果我們想要叫用需要輸入參數的方法（例如 `ProductBLL` 類別的 `GetProductsByCategoryID(categoryID)`），該怎麼辦？ 為了呼叫需要一或多個參數的方法，我們必須設定 ObjectDataSource 來指定這些參數的值。 我們會在[下一個教學](declarative-parameters-vb.md)課程中瞭解如何完成這項操作。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [建立您自己的資料來源控制項](https://msdn.microsoft.com/library/ms364049.aspx)
- [ASP.NET 2.0 的 GridView 範例](https://msdn.microsoft.com/library/aa479339.aspx)
- [ASP.NET 2.0 中簡化和擴充的資料系結語法](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2.0 中的主題](http://www.odetocode.com/Articles/423.aspx)
- [使用主題的伺服器端樣式](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [如何：以程式設計方式套用 ASP.NET 主題](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
> [下一頁](declarative-parameters-vb.md)
