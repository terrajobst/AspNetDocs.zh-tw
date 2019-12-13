---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: 建立自訂資料庫驅動的網站地圖提供者（VB） |Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0 中的預設網站地圖提供者會從靜態 XML 檔案抓取其資料。 雖然以 XML 為基礎的提供者適用于許多小型和中 siz 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: 78051696bd75e1d574f55b1c5d5891fe67c3030d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74630160"
---
# <a name="building-a-custom-database-driven-site-map-provider-vb"></a>建置自訂的資料庫驅動網站導覽提供者 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip)或[下載 PDF](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> ASP.NET 2.0 中的預設網站地圖提供者會從靜態 XML 檔案抓取其資料。 雖然以 XML 為基礎的提供者適用于許多中小型網站，但較大型的 Web 應用程式需要更動態的網站地圖。 在本教學課程中，我們將建立自訂網站地圖提供者，它會從商務邏輯層抓取其資料，然後從資料庫中抓取資料。

## <a name="introduction"></a>簡介

ASP.NET 2.0 s 網站地圖功能可讓網頁開發人員在某些持續性的媒體（例如 XML 檔案）中定義 web 應用程式的網站地圖。 定義好之後，可以透過[`System.Web` 命名空間](https://msdn.microsoft.com/library/system.web.aspx)中的[`SiteMap` 類別](https://msdn.microsoft.com/library/system.web.sitemap.aspx)，或透過各種導覽 Web 控制項（例如 SiteMapPath、Menu 和 TreeView 控制項），以程式設計方式存取網站地圖資料。 網站地圖系統會使用[提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，因此可以建立不同的網站地圖序列化，並將其插入 web 應用程式中。 ASP.NET 2.0 隨附的預設網站地圖提供者會將網站地圖結構保存在 XML 檔案中。 回到[主版頁面和網站導覽](../introduction/master-pages-and-site-navigation-vb.md)教學課程中，我們建立了一個名為 `Web.sitemap` 的檔案，其中包含此結構，並已使用每個新的教學課程區段更新其 XML。

如果網站地圖 s 結構相當靜態，例如這些教學課程，則預設的 XML 網站地圖提供者運作良好。 不過，在許多情況下，都需要更動態的網站地圖。 請考慮 [圖 1] 所示的網站地圖，其中每個類別和產品都會顯示為網站 s 結構中的區段。 使用此網站地圖時，流覽對應到根節點的網頁可能會列出所有類別，而流覽特定的類別目錄則會列出該類別目錄的產品，而查看特定的產品網頁會顯示該產品的詳細資料。

[![分類和產品構成網站地圖 s 結構](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**圖 1**：類別和產品構成網站地圖 s 結構（[按一下以觀看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png)）

雖然這個類別目錄和產品架構的結構可以硬式編碼到 `Web.sitemap` 檔案中，但每次加入、移除或重新命名類別或產品時，都必須更新檔案。 因此，如果從資料庫取出結構，或在理想情況下，從應用程式架構的商務邏輯層來看，網站地圖維護會大幅簡化。 如此一來，當加入、重新命名或刪除產品和類別時，網站地圖會自動更新以反映這些變更。

由於 ASP.NET 2.0 s 網站地圖序列化是以提供者模型為基礎所建立，因此我們可以建立自己的自訂網站地圖提供者，從其他資料存放區（例如資料庫或架構）抓取其資料。 在本教學課程中，我們將建立自訂提供者，以從 BLL 抓取其資料。 讓我們開始吧！

> [!NOTE]
> 本教學課程中建立的自訂網站地圖提供者，與應用程式的架構和資料模型緊密結合。 Jeff Prosise 會將[網站地圖儲存在 SQL Server 中](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)，而[您之前正在等待文章的 SQL 網站地圖提供者，會](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)檢查在 SQL Server 中儲存網站地圖資料的一般化方法。

## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>步驟 1:建立自訂網站地圖提供者網頁

開始建立自訂網站地圖提供者之前，請先新增本教學課程所需的 ASP.NET 網頁。 從新增名為 `SiteMapProvider`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

此外，也請將 `CustomProviders` 子資料夾新增至 `App_Code` 資料夾。

![新增網站地圖提供者相關教學課程的 ASP.NET 網頁](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**圖 2**：新增網站地圖提供者相關教學課程的 ASP.NET 網頁

因為這一節只有一個教學課程，所以我們不需要 `Default.aspx` 來列出章節的教學課程。 相反地，`Default.aspx` 會在 GridView 控制項中顯示類別目錄。 我們會在步驟2中解決此情況。

接下來，更新 `Web.sitemap` 以包含 `Default.aspx` 頁面的參考。 具體而言，請在快取 `<siteMapNode>`之後加入下列標記：

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含唯一網站地圖提供者教學課程的專案。

![網站地圖現在包含網站地圖提供者教學課程的專案](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**圖 3**：網站地圖現在包含網站地圖提供者教學課程的專案

本教學課程的主要重點在於說明如何建立自訂網站地圖提供者，以及如何將 web 應用程式設定為使用該提供者。 特別是，我們將建立一個提供者，它會傳回網站地圖，其中包含根節點以及每個類別目錄和產品的節點，如 [圖 1] 所示。 一般來說，網站地圖中的每個節點都可以指定 URL。 針對我們的網站地圖，根節點的 URL 將會是 `~/SiteMapProvider/Default.aspx`，這會列出資料庫中的所有類別。 網站地圖中的每個類別目錄節點都會有指向 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`的 URL，這會列出指定之*類別*目錄中的所有產品。 最後，每個 [product 網站地圖] 節點都會指向 [`~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`]，這會顯示特定的產品詳細資料。

若要開始，我們必須建立 `Default.aspx`、`ProductsByCategory.aspx`和 `ProductDetails.aspx` 頁面。 這些頁面會分別在步驟2、3和4中完成。 由於本教學課程的天生是在網站地圖提供者上，而且自從過去的教學課程已涵蓋如何建立這類多頁主要/詳細資料包表，因此我們將會在步驟2到4中進行。 如果您需要重新整理程式來建立跨越多個頁面的主要/詳細資料包表，請參閱[跨兩個頁面的主要/詳細資料篩選](../masterdetail/master-detail-filtering-across-two-pages-vb.md)教學課程。

## <a name="step-2-displaying-a-list-of-categories"></a>步驟 2:顯示分類清單

開啟 [`SiteMapProvider`] 資料夾中的 [`Default.aspx`] 頁面，並將 GridView 從 [工具箱] 拖曳至設計工具，將其 `ID` 設定為 [`Categories`]。 從 GridView 的智慧標籤，將它系結至名為 `CategoriesDataSource` 的新 ObjectDataSource 並加以設定，讓它使用 `CategoriesBLL` 類別 s `GetCategories` 方法來抓取其資料。 由於此 GridView 只會顯示類別，而不提供資料修改功能，因此，請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![使用 GetCategories 方法設定 ObjectDataSource 以傳回分類](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**圖 4**：設定 ObjectDataSource 以使用 `GetCategories` 方法傳回分類（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png)）

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**圖 5**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 將會加入 `CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`和 `BrochurePath`的 BoundField。 編輯 GridView，使其只包含 `CategoryName` 和 `Description` BoundFields，並將 `CategoryName` BoundField s `HeaderText` 屬性更新為 [類別]。

接下來，新增 HyperLinkField，並將它放在最左邊的欄位。 將 [`DataNavigateUrlFields`] 屬性設定為 [`CategoryID`]，並將 `DataNavigateUrlFormatString` 屬性設為 [`~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`]。 將 [`Text`] 屬性設定為 [查看產品]。

![將 HyperLinkField 新增至類別 GridView](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**圖 6**：將 HyperLinkField 新增至 `Categories` GridView

建立 ObjectDataSource 並自訂 GridView 欄位之後，這兩個控制項的宣告式標記如下所示：

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

[圖 7] 顯示透過瀏覽器觀看 `Default.aspx`。 按一下 [類別目錄] [產品] 連結會帶您前往 `ProductsByCategory.aspx?CategoryID=categoryID`，我們將在步驟3中建立。

[![每個類別都會與 [View Products] 連結一起列出](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**圖 7**：每個類別都會與 [View Products] 連結一起列出（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png)）

## <a name="step-3-listing-the-selected-category-s-products"></a>步驟 3：列出選取的類別 s 產品

開啟 [`ProductsByCategory.aspx`] 頁面，並加入 GridView，將其命名為 `ProductsByCategory`。 從其智慧標籤，將 GridView 系結至名為 `ProductsByCategoryDataSource`的新 ObjectDataSource。 將 ObjectDataSource 設定為使用 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法，並將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設為（無）。

[![使用 ProductsBLL 類別的 GetProductsByCategoryID （類別 Id）方法](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**圖 8**：使用 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png)）

[設定資料來源] 嚮導中的最後一個步驟會提示您輸入*類別*的參數來源。 由於這項資訊是透過 querystring 欄位 `CategoryID`傳遞，因此請從下拉式清單中選取 [QueryString]，然後在 [QueryStringField] 文字方塊中輸入 [類別]，如 [圖 9] 所示。 按一下 [完成] 完成精靈。

[![使用 [類別 Id] 參數的 [類別 Id Querystring] 欄位](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**圖 9**：針對 [*類別 id* ] 參數使用 [`CategoryID` Querystring] 欄位（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png)）

完成 wizard 之後，Visual Studio 會將對應的 BoundFields 和 CheckBoxField 加入至 GridView 中的產品資料欄位。 移除 `ProductName`、`UnitPrice`和 `SupplierName` BoundFields 以外的所有。 將這三個 BoundFields `HeaderText` 屬性自訂為分別讀取產品、價格和供應商。 將 `UnitPrice` BoundField 格式化為貨幣。

接下來，新增 HyperLinkField，並將它移至最左邊的位置。 將其 [`Text`] 屬性設為 [View Details]，將其 `DataNavigateUrlFields` 屬性設定為 [`ProductID`]，將其 [`DataNavigateUrlFormatString`] `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`屬性設定為

![新增指向 ProductDetails 的 View Details HyperLinkField](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**圖 10**：新增指向 `ProductDetails.aspx` 的 [View Details] HyperLinkField

進行這些自訂之後，GridView 和 ObjectDataSource 的宣告式標記應該如下所示：

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

返回 [透過瀏覽器觀看 `Default.aspx`]，然後按一下飲料的 [查看產品] 連結。 這會讓您 `ProductsByCategory.aspx?CategoryID=1`，在 Northwind 資料庫中顯示屬於飲料類別的產品名稱、價格和供應商（請參閱 [圖 11]）。 歡迎您進一步增強此頁面，以包含可將使用者傳回分類清單頁面（`Default.aspx`）的連結，以及顯示所選類別目錄名稱和描述的 DetailsView 或 FormView 控制項。

[![會顯示飲料名稱、價格和供應商](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**圖 11**：會顯示飲料名稱、價格和供應商（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png)）

## <a name="step-4-showing-a-product-s-details"></a>步驟 4：顯示產品的詳細資料

最後一頁 [`ProductDetails.aspx`] 會顯示所選產品的詳細資料。 開啟 `ProductDetails.aspx`，然後從 [工具箱] 將 [DetailsView] 拖曳至設計工具。 將 [DetailsView s `ID`] 屬性設定為 `ProductInfo` 並清除其 `Height` 和 `Width` 屬性值。 從其智慧標籤，將 DetailsView 系結至名為 `ProductDataSource`的新 ObjectDataSource，並設定 ObjectDataSource 從 `ProductsBLL` 類別 s `GetProductByProductID(productID)` 方法提取其資料。 如同先前在步驟2和3中建立的網頁，將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![將 ObjectDataSource 設定為使用 GetProductByProductID （productID）方法](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**圖 12**：設定 ObjectDataSource 使用 `GetProductByProductID(productID)` 方法（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png)）

[設定資料來源] wizard 的最後一個步驟會提示您輸入*productID*參數的來源。 由於此資料是透過 querystring 欄位 `ProductID`，請將下拉式清單設定為 QueryString，並將 QueryStringField 文字方塊設為 ProductID。 最後，按一下 [完成] 按鈕以完成嚮導。

[![設定 productID 參數，從 ProductID Querystring 欄位提取其值](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**圖 13**：設定*productID*參數，從 [`ProductID` Querystring] 欄位提取其值（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 將會在 [產品資料] 欄位的 DetailsView 中建立對應的 BoundFields 和 CheckBoxField。 移除 [`ProductID`]、[`SupplierID`] 和 [`CategoryID` BoundFields]，並視需要設定其餘欄位。 在少數美觀設定之後，我的 DetailsView 和 ObjectDataSource 宣告式標記看起來如下所示：

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

若要測試此頁面，請返回 `Default.aspx`，然後按一下 [飲料] 類別的 [查看產品]。 從飲料產品的清單中，按一下 [Chai 茶] 的 [View Details] 連結。 這會帶您前往 `ProductDetails.aspx?ProductID=1`，其中顯示 Chai 的茶詳細資料（請參閱 [圖 14]）。

[會顯示 ![Chai 茶 s 供應商、類別、價格及其他資訊](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**圖 14**：隨即顯示 Chai 茶的供應商、類別、價格和其他資訊（[按一下以觀看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png)）

## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>步驟 5：瞭解網站地圖提供者的內部運作

網站地圖會在 web 伺服器的記憶體中表示為構成階層之 `SiteMapNode` 實例的集合。 只能有一個根，所有非根節點都只能有一個父節點，而所有節點可能會有任意數目的子系。 每個 `SiteMapNode` 物件都代表網站 s 結構中的一個區段;這些區段通常會有對應的網頁。 因此， [`SiteMapNode` 類別](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)的屬性如 `Title`、`Url`和 `Description`，可提供 `SiteMapNode` 所代表之區段的資訊。 另外還有一個 `Key` 屬性，可唯一識別階層中的每個 `SiteMapNode`，以及用來建立此階層 `ChildNodes`、`ParentNode`、`NextSibling`、`PreviousSibling`等等的屬性。

[圖 15] 顯示 [圖 1] 中的一般網站地圖結構，但有更詳細的執行詳細資料。

[![每個 SiteMapNode 都有標題、Url、索引鍵等等的屬性](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**圖 15**：每個 `SiteMapNode` 都具有如 `Title`、`Url`、`Key`等屬性（[按一下以觀看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif)）

網站對應可透過[`System.Web` 命名空間](https://msdn.microsoft.com/library/system.web.aspx)中的[`SiteMap` 類別](https://msdn.microsoft.com/library/system.web.sitemap.aspx)來存取。 這個類別的 `RootNode` 屬性會傳回網站地圖 s 根 `SiteMapNode` 實例;`CurrentNode` 會傳回 `SiteMapNode`，其 `Url` 屬性符合目前要求之網頁的 URL。 這個類別是由 ASP.NET 2.0 s 導覽 Web 控制項在內部使用。

存取 `SiteMap` 類別的屬性時，必須將來自某個持續性媒介的網站地圖結構序列化為記憶體。 不過，網站地圖序列化邏輯並不會硬式編碼到 `SiteMap` 類別中。 相反地，在執行時間，`SiteMap` 類別會決定要用於序列化的網站地圖*提供者*。 預設會使用[`XmlSiteMapProvider` 類別](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)，這會從格式正確的 XML 檔案讀取網站地圖 s 結構。 不過，只要稍加一些工作，我們就可以建立自己的自訂網站地圖提供者。

所有網站地圖提供者都必須衍生自[`SiteMapProvider` 類別](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx)，其中包括網站地圖提供者所需的基本方法和屬性，但省略了許多的執行細節。 第二個類別（ [`StaticSiteMapProvider`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx)）會擴充 `SiteMapProvider` 類別，並包含更健全的必要功能執行。 就內部而言，`StaticSiteMapProvider` 會在 `Hashtable` 中儲存網站地圖的 `SiteMapNode` 實例，並提供 `AddNode(child, parent)`、`RemoveNode(siteMapNode),` 和 `Clear()` 之類的方法，將 `SiteMapNode` 新增和移除至內部 `Hashtable`。 `XmlSiteMapProvider` 衍生自 `StaticSiteMapProvider`。

建立擴充 `StaticSiteMapProvider`的自訂網站地圖提供者時，有兩個必須覆寫的抽象方法： [`BuildSiteMap`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx)和[`GetRootNodeCore`](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx)。 `BuildSiteMap`，正如其名，會負責從持續性儲存體載入網站地圖結構，並在記憶體中加以建立。 `GetRootNodeCore` 會傳回網站地圖中的根節點。

在 web 應用程式可以使用網站地圖提供者之前，您必須先在應用程式的設定中註冊。 根據預設，會使用名稱 `AspNetXmlSiteMapProvider`註冊 `XmlSiteMapProvider` 類別。 若要註冊額外的網站地圖提供者，請將下列標記新增至 `Web.config`：

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

*Name*值會將人類可讀的名稱指派給提供者，而*type*會指定網站地圖提供者的完整型別名稱。 我們會在建立自訂網站地圖提供者之後，探索步驟7中的*名稱*和*類型*值的具體值。

網站地圖提供者類別會在第一次從 `SiteMap` 類別存取時具現化，並在 web 應用程式的存留期間保留在記憶體中。 因為只有一個網站地圖提供者的實例可以從多個並行網站訪客叫用，所以提供者的方法必須是*安全線程*。

基於效能和擴充性的原因，我們一定要快取記憶體中的網站地圖結構並傳回此快取的結構，而不是在每次叫用 `BuildSiteMap` 方法時重新建立。 視頁面上使用的導覽控制項和網站地圖結構的深度而定，每位使用者可能會針對每個頁面要求多次呼叫 `BuildSiteMap`。 在任何情況下，如果我們未在 `BuildSiteMap` 中快取網站地圖結構，則每次叫用時，我們都必須從架構重新取出產品和類別資訊（這會導致資料庫的查詢）。 如先前的快取教學課程中所討論，快取的資料可能會過時。 為了對抗此，我們可以使用時間或 SQL 快取相依性的 expiries。

> [!NOTE]
> 網站地圖提供者可以選擇性地覆寫[`Initialize` 方法](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx)。 當第一次具現化網站地圖提供者，並在 `<add>` 專案的 `Web.config` 中傳遞任何指派給提供者的自訂屬性時，會叫用 `Initialize`，例如： `<add name="name" type="type" customAttribute="value" />`。 如果您想要讓網頁開發人員指定各種網站地圖提供者相關的設定，而不需要修改提供者的程式碼，這會很有用。 例如，如果我們直接從資料庫讀取類別目錄和產品資料，而不是透過架構，我們可能會想要讓網頁開發人員透過 `Web.config` 來指定資料庫連接字串，而不是在提供者的程式碼中使用硬式編碼值。 我們將在步驟6中建立的自訂網站地圖提供者，並不會覆寫此 `Initialize` 方法。 如需使用 `Initialize` 方法的範例，請參閱[在 SQL Server 文章中儲存網站對應](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)的[Jeff Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) 。

## <a name="step-6-creating-the-custom-site-map-provider"></a>步驟 6：建立自訂網站地圖提供者

若要建立自訂網站地圖提供者，以根據 Northwind 資料庫中的類別和產品建立網站地圖，我們需要建立可延伸 `StaticSiteMapProvider`的類別。 在步驟1中，我要求您在 [`App_Code`] 資料夾中新增一個 `CustomProviders` 資料夾-將新類別新增至名為 `NorthwindSiteMapProvider`的這個資料夾。 將下列程式碼加入 `NorthwindSiteMapProvider` 類別：

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

讓我們開始探索這個類別的 `BuildSiteMap` 方法，這是以`lock` 的[語句](https://msdn.microsoft.com/library/c5kehkcz.aspx)開頭。 `lock` 語句一次只允許一個執行緒進入，因此會序列化其程式碼的存取，並防止兩個平行線程在另一個腳趾上逐步執行。

類別層級 `SiteMapNode` 變數 `root` 用來快取網站地圖結構。 第一次建立網站對應時，或在基礎資料修改後第一次建立時，`root` 將會 `Nothing`，並會構造網站地圖結構。 網站地圖的根節點會在結構處理期間指派給 `root`，因此下次呼叫這個方法時，將不會 `Nothing``root`。 因此，只要 `root` 不 `Nothing`，網站地圖結構就會傳回給呼叫者，而不需要重新建立。

如果 `Nothing`root，則會從產品和類別資訊建立網站地圖結構。 網站地圖的建立方式，是藉由建立 `SiteMapNode` 實例，然後透過呼叫 `StaticSiteMapProvider` 類別 s `AddNode` 方法來形成階層。 `AddNode` 會執行內部簿記，將各種 `SiteMapNode` 實例儲存在 `Hashtable`中。 開始建立階層之前，我們先呼叫 `Clear` 方法，這會清除內部 `Hashtable`的元素。 接下來，`ProductsBLL` 類別 `GetProducts` 方法和產生的 `ProductsDataTable` 會儲存在本機變數中。

網站地圖的結構一開始先建立根節點，並將它指派給 `root`。 在此 `BuildSiteMap` 中使用的[`SiteMapNode` s](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx)函式的多載會傳遞下列資訊：

- 網站地圖提供者的參考（`Me`）。
- `SiteMapNode` s `Key`。 針對每個 `SiteMapNode`，此必要值必須是唯一的。
- `SiteMapNode` s `Url`。 `Url` 是選擇性的，但如果提供的話，每個 `SiteMapNode` s `Url` 值都必須是唯一的。
- `SiteMapNode` s `Title`，這是必要的。

`AddNode(root)` 方法呼叫會將 `SiteMapNode` `root` 新增至網站地圖做為根。 接下來，會列舉 `ProductsDataTable` 中的每個 `ProductRow`。 如果目前產品的類別已經有 `SiteMapNode`，則會參考它。 否則，會透過 `AddNode(categoryNode, root)` 方法呼叫來建立類別的新 `SiteMapNode`，並將其新增為 `SiteMapNode``root` 的子系。 找到或建立適當的類別 `SiteMapNode` 節點之後，就會為目前的產品建立 `SiteMapNode`，並透過 `AddNode(productNode, categoryNode)`將其新增為類別 `SiteMapNode` 目錄的子系。 請注意，類別 `SiteMapNode` s `Url` 屬性值是 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`，而產品 `SiteMapNode` s `Url` 屬性指派 `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`。

> [!NOTE]
> 具有資料庫 `NULL` 值的產品 `CategoryID` 會分組在其 `Title` 屬性設為 [無] 且其 [`Url`] 屬性設定為空字串的類別 `SiteMapNode`。 我決定將 `Url` 設為空字串，因為 `ProductBLL` 類別的 `GetProductsByCategory(categoryID)` 方法目前缺少以 `NULL` `CategoryID` 值傳回那些產品的功能。 此外，我也想要示範導覽控制項如何呈現缺少其 `Url` 屬性值的 `SiteMapNode`。 我建議您擴充本教學課程，讓 None `SiteMapNode` s `Url` 屬性指向 `ProductsByCategory.aspx`，但只會顯示具有 `NULL` `CategoryID` 值的產品。

在建立網站地圖之後，會使用 `Categories` 上的 SQL 快取相依性，將任意物件新增至資料快取，並透過 `AggregateCacheDependency` 物件 `Products` 資料表。 我們已在先前的教學課程中*使用 sql 快*取相依性來探索使用 sql 快取相依性。 不過，自訂網站地圖提供者會使用我們尚未探索的資料快取 `Insert` 方法的多載。 這個多載會接受在從快取中移除物件時所呼叫的委派作為其最終的輸入參數。 具體而言，我們會傳入新的[`CacheItemRemovedCallback` 委派](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx)，指向 `NorthwindSiteMapProvider` 類別中進一步向下定義的 `OnSiteMapChanged` 方法。

> [!NOTE]
> 網站地圖的記憶體中表示會透過類別層級的變數 `root`進行快取。 因為自訂網站地圖提供者類別只有一個實例，而且該實例會在 web 應用程式中的所有線程之間共用，所以這個類別變數會當做快取。 `BuildSiteMap` 方法也會使用資料快取，但只有在 `Categories` 或 `Products` 資料表中的基礎資料庫資料變更時，才會收到通知。 請注意，放入資料快取中的值只是目前的日期和時間。 實際網站地圖資料並*不*會放在資料快取中。

`BuildSiteMap` 方法會藉由傳回網站地圖的根節點來完成。

其餘的方法相當簡單。 `GetRootNodeCore` 會負責傳回根節點。 因為 `BuildSiteMap` 會傳回根，`GetRootNodeCore` 只會傳回 `BuildSiteMap` s 傳回值。 當移除快取專案時，`OnSiteMapChanged` 方法會將 `root` 設定回 `Nothing`。 當 root 設定為 `Nothing`，下一次叫用 `BuildSiteMap` 時，將會重建網站地圖結構。 最後，如果有這樣的值，`CachedDate` 屬性會傳回儲存在資料快取中的日期和時間值。 頁面開發人員可以使用這個屬性來判斷上次快取網站對應資料的時間。

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>步驟 7：註冊`NorthwindSiteMapProvider`

為了讓 web 應用程式使用在步驟6中建立的 `NorthwindSiteMapProvider` 網站地圖提供者，我們需要在 `Web.config`的 `<siteMap>` 區段中註冊它。 具體而言，請在 `Web.config`中的 `<system.web>` 元素內新增下列標記：

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

此標記會執行兩件事：首先，它會指出內建的 `AspNetXmlSiteMapProvider` 是預設網站地圖提供者;第二，它會註冊在步驟6中建立的自訂網站地圖提供者，並使用易記名稱 Northwind。

> [!NOTE]
> 針對位於應用程式 s `App_Code` 資料夾中的網站地圖提供者，`type` 屬性的值只是類別名稱。 或者，也可以在個別的類別庫專案中建立自訂的網站地圖提供者，並將編譯的元件放在 web 應用程式的 `/Bin` 目錄中。 在此情況下，`type` 屬性值會是*Namespace*。*ClassName*、 *AssemblyName* 。

更新 `Web.config`之後，請花一點時間從瀏覽器的教學課程中查看任何頁面。 請注意，左邊的導覽介面仍然會顯示 `Web.sitemap`中定義的區段和教學課程。 這是因為我們將 `AspNetXmlSiteMapProvider` 保留為預設提供者。 為了建立使用 `NorthwindSiteMapProvider`的導覽使用者介面專案，我們必須明確指定應使用 Northwind 網站地圖提供者。 我們會在步驟8中瞭解如何完成這項工作。

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>步驟 8：使用自訂網站對應提供者顯示網站地圖資訊

在 `Web.config`中建立並註冊自訂網站地圖提供者之後，我們就可以將導覽控制項加入至 [`SiteMapProvider`] 資料夾中的 [`Default.aspx`]、[`ProductsByCategory.aspx`] 和 [`ProductDetails.aspx`] 頁面。 一開始先開啟 [`Default.aspx`] 頁面，並將 `SiteMapPath` 從 [工具箱] 拖曳至設計工具。 SiteMapPath 控制項位於 [工具箱] 的導覽區段中。

[![將 SiteMapPath 新增至 default.aspx](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**圖 16**：將 SiteMapPath 新增至 `Default.aspx` （[按一下以觀看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif)）

SiteMapPath 控制項會顯示階層連結，指出網站地圖內目前的頁面位置。 我們已在主版頁面*和網站導覽*教學課程中，將 SiteMapPath 新增至主版頁面的頂端。

請花點時間透過瀏覽器觀看此頁面。 [圖 16] 中新增的 SiteMapPath 會使用預設網站地圖提供者，從 `Web.sitemap`提取其資料。 因此，階層連結會顯示 [首頁] &gt; 自訂網站地圖，就像右上角的階層連結一樣。

[![階層連結會使用預設的網站地圖提供者](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**圖 17**：階層連結會使用預設網站地圖提供者（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif)）

若要在 [圖 16] 中新增 SiteMapPath，請使用我們在步驟6中建立的自訂網站地圖提供者，將其[`SiteMapProvider` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx)設定為 Northwind，這是我們指派給 `Web.config`中 `NorthwindSiteMapProvider` 的名稱。 可惜的是，設計工具會繼續使用預設的網站地圖提供者，但如果您在進行此屬性變更之後，透過瀏覽器造訪網頁，您會看到階層連結現在會使用自訂網站地圖提供者。

[![階層連結現在會使用自訂網站地圖提供者 NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**圖 18**：階層連結現在使用自訂網站地圖提供者 `NorthwindSiteMapProvider` （[按一下以觀看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif)）

SiteMapPath 控制項會在 [`ProductsByCategory.aspx`] 和 [`ProductDetails.aspx`] 頁面中顯示功能更多功能的使用者介面。 將 SiteMapPath 新增至這些頁面，並將兩者中的 `SiteMapProvider` 屬性設定為 Northwind。 從 `Default.aspx` 按一下飲料的 [查看產品] 連結，然後在 [Chai 茶] 的 [查看詳細資料] 連結上。 如 [圖 19] 所示，階層連結包括目前的網站地圖區段（Chai 茶）及其上階：飲料和所有類別。

[![階層連結現在會使用自訂網站地圖提供者 NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**圖 19**：階層連結現在使用自訂網站地圖提供者 `NorthwindSiteMapProvider` （[按一下以觀看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png)）

除了 SiteMapPath 之外，還可以使用其他導覽使用者介面專案，例如功能表和 TreeView 控制項。 本教學課程的下載中的 `Default.aspx`、`ProductsByCategory.aspx`和 `ProductDetails.aspx` 頁面，例如所有包含功能表控制項（請參閱 [圖 20]）。 如需深入瞭解 ASP.NET 2.0 中的導覽控制項和網站地圖系統，請參閱 <<c0>檢查 ASP.NET 2.0 s 網站流覽功能和使用[ASP.NET 2.0 快速入門](https://quickstarts.asp.net/QuickStartv20/aspnet/)的[網站導覽控制項](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx)一節。

[![功能表控制項列出每個類別和產品](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**圖 20**：Menu 控制項會列出每個類別和產品（[按一下以查看完整大小的影像](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif)）

如本教學課程稍早所述，您可以透過 `SiteMap` 類別，以程式設計方式存取網站地圖結構。 下列程式碼會傳回預設提供者的根 `SiteMapNode`：

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

由於 `AspNetXmlSiteMapProvider` 是應用程式的預設提供者，因此上述程式碼會傳回 `Web.sitemap`中定義的根節點。 若要參考非預設的網站地圖提供者，請使用 `SiteMap` 類別的[`Providers` 屬性](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx)，如下所示：

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

其中*name*是自訂網站地圖提供者的名稱（Northwind，適用于我們的 web 應用程式）。

若要存取網站地圖提供者特定的成員，請使用 `SiteMap.Providers["name"]` 來抓取提供者實例，然後將它轉換成適當的類型。 例如，若要在 ASP.NET 網頁中顯示 `NorthwindSiteMapProvider` s `CachedDate` 屬性，請使用下列程式碼：

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> 請務必測試 SQL 快取相依性功能。 造訪 `Default.aspx`、`ProductsByCategory.aspx`和 `ProductDetails.aspx` 頁面之後，請移至 [編輯、插入及刪除] 區段中的其中一個教學課程，然後編輯類別或產品的名稱。 然後返回 [`SiteMapProvider`] 資料夾中的其中一個頁面。 假設已有足夠的時間來輪詢機制，以注意基礎資料庫的變更，則應該更新網站地圖以顯示新的產品或類別名稱。

## <a name="summary"></a>總結

ASP.NET 2.0 s 網站地圖功能包括 `SiteMap` 類別、數個內建的導覽 Web 控制項，以及預設的網站地圖提供者，其會預期網站對應資訊會保存到 XML 檔案中。 若要從其他來源（例如，從資料庫、應用程式架構或遠端 Web 服務）使用網站地圖資訊，我們需要建立自訂網站地圖提供者。 這牽涉到建立直接或間接從 `SiteMapProvider` 類別衍生的類別。

在本教學課程中，我們已瞭解如何根據從應用程式架構挑選的產品和類別資訊，建立以網站地圖為基礎的自訂網站地圖提供者。 我們的提供者擴充了 `StaticSiteMapProvider` 類別，並詳述如下建立一個 `BuildSiteMap` 方法來抓取資料、結構化網站地圖階層，並在類別層級變數中快取產生的結構。 我們在修改基礎 `Categories` 或 `Products` 資料時，使用了 SQL 快取相依性搭配回呼函數使快取的結構失效。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- 將[網站地圖儲存在 SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)和[您所等待的 SQL 網站地圖提供者](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)中
- [查看 ASP.NET 2.0 s 提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [提供者工具組](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [檢查 ASP.NET 2.0 s 網站導覽功能](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dave Gardner、Zack，Teresa Murphy 和 Bernadette Leigh。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一步](building-a-custom-database-driven-site-map-provider-cs.md)
