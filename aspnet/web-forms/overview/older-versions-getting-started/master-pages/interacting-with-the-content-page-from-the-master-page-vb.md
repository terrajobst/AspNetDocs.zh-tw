---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
title: 從主版頁面與內容頁互動（VB） |Microsoft Docs
author: rick-anderson
description: 檢查如何從主版頁面中的程式碼呼叫內容頁面的方法、設定屬性等等。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: a6e2e1a0-c925-43e9-b711-1f178fdd72d7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 5367ad1b7f2fa11c635ad95754c9bcc1edcb6c1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615721"
---
# <a name="interacting-with-the-content-page-from-the-master-page-vb"></a>從主版頁面與內容頁互動 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_VB.zip)或[下載 PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_VB.pdf)

> 檢查如何從主版頁面中的程式碼呼叫內容頁面的方法、設定屬性等等。

## <a name="introduction"></a>簡介

先前的教學課程已檢查如何讓內容頁面以程式設計方式與主版頁面互動。 回想一下，我們更新了主版頁面，使其包含一個 GridView 控制項，其中列出五個最近新增的產品。 接著，我們建立了一個內容頁面，使用者可以從中加入新產品。 加入新產品時，需要指示主版頁面重新整理其 GridView，使其包含剛新增的產品。 這項功能的完成方式是將公用方法新增至主版頁面，以重新整理系結至 GridView 的資料，然後從 [內容] 頁面叫用該方法。

最常見的內容和主版頁面互動形式源自于 [內容] 頁面。 不過，主版頁面可以將目前的內容頁面 rouse 為動作，如果主版頁面包含使用者介面專案，讓使用者修改也會顯示在內容頁面上的資料，則可能需要這類功能。 假設有一個 [內容] 頁面，其中顯示 GridView 控制項中的產品資訊，以及一個包含按鈕控制項的主版頁面，當按下時，會將所有產品的價格加倍。 就像上一個教學課程中的範例一樣，GridView 必須在按下 [雙價] 按鈕之後重新整理，才會顯示新的價格，但在此案例中，則是需要 rouse 內容頁面以進行動作的主版頁面。

本教學課程會探索如何在 [內容] 頁面中定義主版頁面的叫用功能。

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>透過事件和事件處理常式 Instigating 程式設計互動

從主版頁面叫用內容頁面功能比其他方式更具挑戰性。 由於內容頁面具有單一主版頁面，因此在 instigating 內容頁面的程式設計互動時，我們知道有哪些公用方法和屬性是可處置的。 不過，主版頁面可以有許多不同的內容頁面，每個都有自己的一組屬性和方法。 然後，我們可以如何在主版頁面中撰寫程式碼，以便在我們不知道要在執行時間前叫用哪個內容頁面時，在其內容頁面中執行某些動作？

請考慮使用 ASP.NET 的 Web 控制項，例如 Button 控制項。 按鈕控制項可以出現在任意數目的 ASP.NET 網頁上，而且需要一種機制，讓它可以警示頁面已被按一下。 這是使用*事件*來完成的。 特別是，按鈕控制項會在按一下時引發其 `Click` 事件;包含按鈕的 [ASP.NET] 頁面可以選擇性地透過*事件處理常式*來回應該通知。

這個相同的模式可在其內容頁面中使用主版頁面觸發程式功能：

1. 將事件新增至主版頁面。
2. 每當主版頁面需要與其內容頁面通訊時，引發事件。 例如，如果主版頁面需要警示其 [內容] 頁面，而使用者已將價格加倍，則其事件會在價格加倍後立即引發。
3. 在需要採取一些動作的內容頁面中，建立事件處理常式。

本教學課程的其餘部分會執行簡介中所述的範例;也就是 [內容] 頁面，其中列出資料庫中的產品，以及包含按鈕控制項以將價格加倍的主版頁面。

## <a name="step-1-displaying-products-in-a-content-page"></a>步驟1：在內容頁面中顯示產品

我們的第一個企業順序是建立一個內容頁面，其中列出 Northwind 資料庫中的產品。 （我們已在先前的教學課程中，將 Northwind 資料庫新增至專案，[*並從 [內容] 頁面與主版頁面互動*](interacting-with-the-master-page-from-the-content-page-vb.md)）。首先，將新的 ASP.NET 網頁新增至名為 `Products.aspx`的 `~/Admin` 資料夾，並務必將它系結至 `Site.master` 主版頁面。 [圖 1] 顯示此頁面新增至網站後的方案總管。

[![將新的 ASP.NET 網頁新增至管理資料夾](interacting-with-the-content-page-from-the-master-page-vb/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image1.png)

**圖 01**：將新的 ASP.NET 網頁新增至 `Admin` 資料夾（[按一下以觀看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image3.png)）

回想一下，在[*主版頁面教學課程中指定標題、中繼標記和其他 HTML 標頭*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)時，我們建立了名為 `BasePage` 的自訂基底頁面類別，它會產生頁面的標題（如果未明確設定的話）。 移至 `Products.aspx` 頁面的程式碼後置類別，並讓它衍生自 `BasePage` （而不是從 `System.Web.UI.Page`）。

最後，更新 `Web.sitemap` 檔案以包含此課程的專案。 將下列標記新增至 [主要] 頁面互動課程的 [`<siteMapNode>`] 底下：

[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample1.xml)]

此 `<siteMapNode>` 專案的加入會反映在課程清單中（請參閱 [圖 5]）。

返回 `Products.aspx`。 在 `MainContent`的內容控制項中，新增 GridView 控制項並將其命名為 `ProductsGrid`。 將 GridView 系結至名為 `ProductsDataSource`的新 SqlDataSource 控制項。

[![將 GridView 系結至新的 SqlDataSource 控制項](interacting-with-the-content-page-from-the-master-page-vb/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image4.png)

**圖 02**：將 GridView 系結至新的 SqlDataSource 控制項（[按一下以查看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image6.png)）

設定 wizard，使其使用 Northwind 資料庫。 如果您已完成上一個教學課程，則 `Web.config`中應該已經有一個名為 `NorthwindConnectionString` 的連接字串。 從下拉式清單中選擇這個連接字串，如 [圖 3] 所示。

[![將 SqlDataSource 設定為使用 Northwind 資料庫](interacting-with-the-content-page-from-the-master-page-vb/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image7.png)

**圖 03**：將 SqlDataSource 設定為使用 Northwind 資料庫（[按一下以觀看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image9.png)）

接下來，從下拉式清單中選擇 Products 資料表，然後傳回 [`ProductName`] 和 [`UnitPrice`] 資料行，以指定資料來源控制項的 `SELECT` 語句（請參閱 [圖 4]）。 按 [下一步]，然後按一下 [完成] 以完成 [設定資料來源]。

[![從 Products 資料表傳回 ProductName 和單價欄位](interacting-with-the-content-page-from-the-master-page-vb/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image10.png)

**圖 04**：傳回 `Products` 資料表中的 `ProductName` 和 `UnitPrice` 欄位（[按一下以查看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image12.png)）

這樣就全部完成了！ 完成 wizard 後 Visual Studio 將兩個 BoundFields 新增至 GridView，以鏡像 SqlDataSource 控制項所傳回的兩個欄位。 GridView 和 SqlDataSource 控制項的標記如下所示。 [圖 5] 顯示透過瀏覽器查看的結果。

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample2.aspx)]

[![每個產品及其價格都列在 GridView 中](interacting-with-the-content-page-from-the-master-page-vb/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image13.png)

**圖 05**：每個產品及其價格都會列在 GridView 中（[按一下以觀看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image15.png)）

> [!NOTE]
> 請隨意清除 GridView 的外觀。 某些建議包括將顯示的單價值格式化為貨幣，以及使用背景色彩和字型來改善方格的外觀。 如需有關在 ASP.NET 中顯示及格式化資料的詳細資訊，請參閱我[使用資料教學課程系列](../../data-access/index.md)。

## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>步驟2：將雙重價格按鈕新增至主版頁面

我們的下一個工作是將按鈕 Web 控制項新增至主版頁面，當您按一下時，將會加倍資料庫中所有產品的價格。 開啟 `Site.master` 主版頁面，並將按鈕從 [工具箱] 拖曳至設計工具，放在我們在上一個教學課程中新增的 `RecentProductsDataSource` SqlDataSource 控制項底下。 將按鈕的 [`ID`] 屬性設定為 [`DoublePrice`]，並將其 [`Text`] 屬性設為 [雙產品價格]。

接下來，將 SqlDataSource 控制項新增至主版頁面，並將其命名為 `DoublePricesDataSource`。 此 SqlDataSource 將用來執行 `UPDATE` 語句，以將所有價格加倍。 具體而言，我們需要將它的 `ConnectionString` 和 `UpdateCommand` 屬性設定為適當的連接字串和 `UPDATE` 語句。 然後，在按一下 [`DoublePrice`] 按鈕時，我們需要呼叫這個 SqlDataSource 控制項的 `Update` 方法。 若要設定 `ConnectionString` 和 `UpdateCommand` 屬性，請選取 [SqlDataSource] 控制項，然後移至 [屬性視窗]。 [`ConnectionString`] 屬性會列出已儲存在下拉式清單中 `Web.config` 的連接字串。選擇 [`NorthwindConnectionString`] 選項，如 [圖 6] 所示。

[![將 SqlDataSource 設定為使用 NorthwindConnectionString](interacting-with-the-content-page-from-the-master-page-vb/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image16.png)

**圖 06**：設定 SqlDataSource 使用 `NorthwindConnectionString` （[按一下以觀看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image18.png)）

若要設定 `UpdateCommand` 屬性，請在屬性視窗中找出 [UpdateQuery] 選項。 選取此屬性時，會顯示具有省略號的按鈕;按一下此按鈕以顯示 [圖 7] 中所示的 [命令和參數編輯器] 對話方塊。 在對話方塊的文字方塊中輸入下列 `UPDATE` 語句：

[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample3.sql)]

執行此語句時，會將 `Products` 資料表中每筆記錄的 `UnitPrice` 值加倍。

[![設定 SqlDataSource 的 UpdateCommand 屬性](interacting-with-the-content-page-from-the-master-page-vb/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image19.png)

**圖 07**：設定 SqlDataSource 的 `UpdateCommand` 屬性（[按一下以查看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image21.png)）

設定這些屬性之後，您的 Button 和 SqlDataSource 控制項的宣告式標記看起來應該如下所示：

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample4.aspx)]

剩下的就是在按一下 [`DoublePrice`] 按鈕時，呼叫它的 `Update` 方法。 為 [`DoublePrice`] 按鈕建立 `Click` 事件處理常式，並加入下列程式碼：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample5.vb)]

若要測試這項功能，請造訪我們在步驟1中建立的 [`~/Admin/Products.aspx`] 頁面，然後按一下 [兩倍的產品價格] 按鈕。 按一下此按鈕會導致回傳，並執行 `DoublePrice` 按鈕的 `Click` 事件處理常式，使所有產品的價格加倍。 然後會重新轉譯頁面，並在瀏覽器中傳回並重新顯示標記。 不過，[內容] 頁面中的 GridView 會列出與按下 [雙產品價格] 按鈕之前相同的價格。 這是因為一開始在 GridView 中載入的資料狀態會儲存在 view 狀態中，因此除非另有指示，否則不會在回傳時重載。 如果您流覽不同的頁面，然後返回 [`~/Admin/Products.aspx`] 頁面，您會看到更新的價格。

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>步驟3：當價格加倍時引發事件

因為 [`~/Admin/Products.aspx`] 頁面中的 GridView 並不會立即反映價格，所以使用者可能會更認為他們未按下 [兩倍的產品價格] 按鈕，或其無法運作。 他們可以多次嘗試按下按鈕，再重新加倍價格。 若要修正此問題，我們必須讓 [內容] 頁面中的方格在兩倍之後立即顯示新的價格。

如本教學課程稍早所述，當使用者按一下 [`DoublePrice`] 按鈕時，我們必須在主版頁面中引發事件。 事件是一種方式，可讓一個類別（事件發行者）通知另一組有趣的類別（事件訂閱者）。 在此範例中，主版頁面是事件發行者;按一下 [`DoublePrice`] 按鈕時所在意的內容頁面是 [訂閱者]。

類別會藉由建立*事件處理常式*來訂閱事件，這是為了回應引發的事件而執行的方法。 發行者會藉由定義*事件委派*來定義他引發的事件。 事件委派會指定事件處理常式必須接受的輸入參數。 在 .NET Framework 中，事件委派不會傳回任何值並接受兩個輸入參數：

- `Object`，可識別事件來源，而
- 衍生自的類別 `System.EventArgs`

傳遞至事件處理常式的第二個參數可以包含事件的其他相關資訊。 雖然基底 `EventArgs` 類別不會傳遞任何資訊，但 .NET Framework 包含一些擴充 `EventArgs` 並包含額外屬性的類別。 例如，`CommandEventArgs` 實例會傳遞至回應 `Command` 事件的事件處理常式，並包含兩個資訊屬性： `CommandArgument` 和 `CommandName`。

> [!NOTE]
> 如需建立、引發和處理事件的詳細資訊，請參閱[事件和委派](https://msdn.microsoft.com/library/17sde2xt.aspx)和[簡單英文的事件委派](http://www.codeproject.com/KB/cs/eventdelegates.aspx)。

若要定義事件，請使用下列語法：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample6.vb)]

由於我們只需要在使用者按下 [`DoublePrice`] 按鈕而不需要傳遞任何其他資訊時，就會對 [內容] 頁面發出警示，因此我們可以使用事件委派 `EventHandler`，它會定義事件處理常式，以接受 `System.EventArgs`類型物件的第二個參數。 若要在主版頁面中建立事件，請將下列程式程式碼新增至主版頁面的程式碼後置類別：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample7.vb)]

上述程式碼會將公用事件新增至名為 `PricesDoubled`的主版頁面。 我們現在必須在價格加倍後才引發此事件。 若要引發事件，請使用下列語法：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample8.vb)]

其中， *sender*和*eventArgs*是您想要傳遞給訂閱者之事件處理常式的值。

使用下列程式碼，更新 `DoublePrice` `Click` 事件處理常式：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample9.vb)]

就像之前一樣，`Click` 事件處理常式一開始會先呼叫 `DoublePricesDataSource` SqlDataSource 控制項的 `Update` 方法，以將所有產品的價格加倍。 之後，事件處理常式會新增兩個專案。 首先，`RecentProducts` GridView 的資料會重新整理。 這個 GridView 已新增至上一個教學課程中的主版頁面，並顯示五個最近新增的產品。 我們需要重新整理此方格，使其顯示這五項產品的加倍價格。 之後，就會引發 `PricesDoubled` 事件。 主版頁面本身（`Me`）的參考會當做事件來源傳送到事件處理常式，而空的 `EventArgs` 物件則會當做事件引數傳送。

## <a name="step-4-handling-the-event-in-the-content-page"></a>步驟4：處理 [內容] 頁面中的事件

此時，只要按一下 `DoublePrice` 按鈕控制項，主版頁面就會引發它的 `PricesDoubled` 事件。 不過，這只是實際的一半，我們仍需要處理「訂閱者」中的事件。 這包含兩個步驟：建立事件處理常式和新增事件連接程式碼，以便在事件引發時執行事件處理常式。

首先，建立名為 `Master_PricesDoubled`的事件處理常式。 由於我們在主版頁面中定義 `PricesDoubled` 事件的方式，事件處理常式的兩個輸入參數必須分別 `Object` 和 `EventArgs`類型。 在事件處理常式中，呼叫 `ProductsGrid` GridView 的 `DataBind` 方法，將資料重新系結至方格。

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample10.vb)]

事件處理常式的程式碼已完成，但我們尚未將主版頁面的 `PricesDoubled` 事件連接到這個事件處理常式。 「訂閱者」會透過下列語法，將事件線路至事件處理常式：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample11.vb)]

*發行者*是*提供事件指定*者的物件參考，而*方法*名稱則是在訂閱者中定義的事件處理常式名稱。

此事件的程式碼必須在第一頁造訪和後續回傳上執行，而且應該在頁面生命週期中的某個時間點發生，然後才會引發事件。 新增事件接線程式碼的好時機是在 PreInit 階段，這會在頁面生命週期初期發生。

開啟 `~/Admin/Products.aspx` 並建立 `Page_PreInit` 事件處理常式：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample12.vb)]

為了完成此接線程式碼，我們需要從 [內容] 頁面以程式設計方式參考主版頁面。 如先前的教學課程中所述，有兩種方式可以執行這項操作：

- 將鬆散類型的 `Page.Master` 屬性轉換為適當的主版頁面類型，或
- 藉由在 [`.aspx`] 頁面中加入 `@MasterType` 指示詞，然後使用強型別 `Master` 屬性。

讓我們使用第二種方法。 將下列 `@MasterType` 指示詞新增至頁面的宣告式標記的頂端：

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample13.aspx)]

然後，在 `Page_PreInit` 事件處理常式中新增下列事件接線碼：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample14.vb)]

當此程式碼準備就緒時，每當按一下 [`DoublePrice`] 按鈕時，就會重新整理 [內容] 頁面中的 GridView。

[圖 8] 和 [9] 說明這種行為。 [圖 8] 顯示第一次造訪時的頁面。 請注意，`RecentProducts` GridView （在主版頁面的左欄中）和 `ProductsGrid` GridView （在 [內容] 頁面中）的價格值。 [圖 9] 在按下 [`DoublePrice`] 按鈕之後，立即顯示相同的畫面。 如您所見，新的價格會立即反映在這兩個 Gridview 中。

[![初始價格值](interacting-with-the-content-page-from-the-master-page-vb/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image22.png)

**圖 8**：初始價格值（[按一下以查看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image24.png)）

[![會在 Gridview 中顯示加倍的價格](interacting-with-the-content-page-from-the-master-page-vb/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image25.png)

**圖 09**： Gridview （[按一下以觀看完整大小的影像](interacting-with-the-content-page-from-the-master-page-vb/_static/image27.png)）中顯示加倍的價格

## <a name="summary"></a>總結

在理想情況下，主版頁面和其內容頁面會彼此獨立，而且不需要任何層級的互動。 不過，如果您有 [主版頁面] 或 [內容] 頁面，其中顯示可從主版頁面或 [內容] 頁面修改的資料，則在修改資料以更新顯示畫面時，您可能需要讓主版頁面警示 [內容] 頁面（反之亦然）。 在先前的教學課程中，我們已瞭解如何讓內容頁面以程式設計方式與主版頁面互動;在本教學課程中，我們探討了如何讓主版頁面起始互動。

雖然內容和主版頁面之間的程式設計互動可能來自內容或主版頁面，但所使用的互動模式則視來源而定。 差異在於內容頁面具有單一主版頁面，但主版頁面可以有許多不同的內容頁面。 較好的方法是讓主版頁面引發事件，以通知已發生某個動作，而不是讓主版頁面直接與內容頁面互動。 關心此動作的內容頁面可以建立事件處理常式。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [存取和更新 ASP.NET 中的資料](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [事件和委派](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [在內容和主版頁面之間傳遞資訊](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [使用 ASP.NET 教學課程中的資料](../../data-access/index.md)

### <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 Scott 可以在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Suchi Banerjee。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)下拉一行

> [!div class="step-by-step"]
> [上一頁](interacting-with-the-master-page-from-the-content-page-vb.md)
> [下一頁](master-pages-and-asp-net-ajax-vb.md)
