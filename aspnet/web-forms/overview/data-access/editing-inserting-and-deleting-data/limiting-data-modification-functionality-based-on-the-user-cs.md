---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
title: 根據使用者（C#）限制資料修改功能 |Microsoft Docs
author: rick-anderson
description: 在允許使用者編輯資料的 web 應用程式中，不同的使用者帳戶可能會有不同的資料編輯許可權。 在本教學課程中，我們將探討 t 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2b251c82-77cf-4e36-baa9-b648eddaa394
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
msc.type: authoredcontent
ms.openlocfilehash: c3cacaddb7e9b493ba39718f41dcaab360d36fd9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74580402"
---
# <a name="limiting-data-modification-functionality-based-on-the-user-c"></a>根據使用者限制資料修改功能 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_CS.exe)或[下載 PDF](limiting-data-modification-functionality-based-on-the-user-cs/_static/datatutorial23cs1.pdf)

> 在允許使用者編輯資料的 web 應用程式中，不同的使用者帳戶可能會有不同的資料編輯許可權。 在本教學課程中，我們將探討如何根據造訪的使用者動態調整資料修改功能。

## <a name="introduction"></a>簡介

有一些 web 應用程式支援使用者帳戶，並根據登入的使用者提供不同的選項、報表和功能。 例如，在我們的教學課程中，我們可能會想要讓供應商公司的使用者能夠登入網站，並更新其產品的一般資訊-每個單位的名稱和數量，也許還有供應商資訊，例如公司名稱、位址、連絡人的資訊等等。 此外，我們可能會想要為公司的人員加入一些使用者帳戶，讓他們可以登入並更新產品資訊，例如庫存的單位、重新排序層級等等。 我們的 web 應用程式可能也會允許匿名使用者流覽（未登入的人員），但會限制他們只能查看資料。 有了這類使用者帳戶系統之後，我們會希望 ASP.NET 網頁中的資料 Web 控制項提供適用于目前登入使用者的插入、編輯和刪除功能。

在本教學課程中，我們將探討如何根據造訪的使用者動態調整資料修改功能。 特別是，我們將建立一個頁面，以可編輯的 DetailsView 顯示供應商資訊，以及一個 GridView，其中列出供應商所提供的產品。 如果造訪頁面的使用者是來自我們的公司，他們可以：查看任何供應商的資訊;編輯其位址;並編輯供應商所提供之任何產品的資訊。 不過，如果使用者是來自特定公司，他們只能查看和編輯自己的位址資訊，而且只能編輯尚未標示為已停止的產品。

[![公司的使用者可以編輯任何供應商的資訊](limiting-data-modification-functionality-based-on-the-user-cs/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image1.png)

**圖 1**：公司的使用者可以編輯任何供應商的資訊（[按一下以觀看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image3.png)）

[![特定供應商的使用者只能查看和編輯其資訊](limiting-data-modification-functionality-based-on-the-user-cs/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image4.png)

**圖 2**：來自特定供應商的使用者只能查看和編輯其資訊（[按一下以觀看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image6.png)）

讓我們開始吧！

> [!NOTE]
> ASP.NET 2.0 s 成員資格系統提供標準化、可擴充的平臺，可用於建立、管理及驗證使用者帳戶。 由於成員資格系統的檢查已超出這些教學課程的範圍，因此本教學課程會藉由允許匿名訪客選擇其是否來自特定供應商或公司，而改為「fakes」成員資格。 如需成員資格的詳細資訊，請參閱我的[檢查 ASP.NET 2.0 s 成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)一文。

## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>步驟1：允許使用者指定其存取權限

在真實世界的 web 應用程式中，使用者的帳戶資訊會包括其是否適用于公司或特定供應商，而且當使用者登入網站之後，這項資訊就會從我們的 ASP.NET 網頁以程式設計方式存取。 透過 ASP.NET 2.0 s 角色系統，可以透過配置檔案系統中的使用者層級帳戶資訊，或透過一些自訂的方式來捕捉此資訊。

由於本教學課程的目的是要示範如何根據登入的使用者來調整資料修改功能，而不是為了展示 ASP.NET 2.0 s 成員資格、角色和配置檔案系統，因此我們將使用非常簡單的機制來判斷使用者造訪頁面的功能-使用者可以在其中指出是否應該能夠查看和編輯任何供應商資訊，或是他們可以查看和編輯之特定供應商資訊的 DropDownList。 如果使用者指出她可以查看和編輯所有供應商資訊（預設值），她可以逐頁流覽所有供應商，編輯任何供應商的位址資訊，並針對所選供應商所提供的任何產品，編輯每個單位的名稱和數量。 不過，如果使用者指出她只能查看和編輯特定供應商，則她只能查看該供應商的詳細資料和產品，而且只能針對*未*中止的產品更新其名稱和數量。

然後，我們在本教學課程中的第一個步驟是建立此 DropDownList，並在系統中填入供應商。 開啟 [`EditInsertDelete`] 資料夾中的 [`UserLevelAccess.aspx`] 頁面，新增其 `ID` 屬性設定為 [`Suppliers`] 的 DropDownList，然後將此 DropDownList 系結至名為 `AllSuppliersDataSource`的新 ObjectDataSource。

[![建立名為 AllSuppliersDataSource 的新 ObjectDataSource](limiting-data-modification-functionality-based-on-the-user-cs/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image7.png)

**圖 3**：建立名為 `AllSuppliersDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image9.png)）

因為我們想要讓此 DropDownList 包含所有供應商，所以請設定 ObjectDataSource 來叫用 `SuppliersBLL` 類別的 `GetSuppliers()` 方法。 此外，請確定 ObjectDataSource s `Update()` 方法已對應到 `SuppliersBLL` 類別 s `UpdateSupplierAddress` 方法，因為我們將在步驟2中新增的 DetailsView 也會使用這個 ObjectDataSource。

完成 ObjectDataSource wizard 之後，請設定 `Suppliers` DropDownList 來完成步驟，使其顯示 `CompanyName` 資料欄位，並使用 [`SupplierID` 資料] 欄位做為每個 `ListItem`的值。

[![將供應商 DropDownList 設定為使用 [公司名稱] 和 [已供應商] 資料欄位](limiting-data-modification-functionality-based-on-the-user-cs/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image10.png)

**圖 4**：設定 `Suppliers` DropDownList 使用 `CompanyName` 和 `SupplierID` 資料欄位（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image12.png)）

此時，DropDownList 會在資料庫中列出供應商的公司名稱。 不過，我們也需要在 DropDownList 中包含 [顯示/編輯所有供應商] 選項。 若要完成此動作，請將 `Suppliers` DropDownList s `AppendDataBoundItems` 屬性設定為 `true`，然後新增 `ListItem`，其 `Text` 屬性為「顯示/編輯所有供應商」，且其值為 `-1`。 您可以直接透過宣告式標記或透過設計工具新增這項功能，方法是前往屬性視窗，然後按一下 DropDownList s `Items` 屬性中的省略號。

> [!NOTE]
> 如需將 [全選] 專案新增至資料系結 DropDownList 的詳細討論，請參閱使用 DropDownList 教學課程的[*主要/詳細資料篩選*](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)。

設定 `AppendDataBoundItems` 屬性並新增 `ListItem` 之後，DropDownList 的宣告式標記看起來應該像這樣：

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample1.aspx)]

[圖 5] 顯示透過瀏覽器觀看時，目前進度的螢幕擷取畫面。

[![[供應商 DropDownList] 包含 [顯示所有] 的所有人，加上每個供應商一個](limiting-data-modification-functionality-based-on-the-user-cs/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image13.png)

**圖 5**： [`Suppliers`] DropDownList 包含 [顯示所有 `ListItem`]，加上每個供應商的一個（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image15.png)）

因為我們想要在使用者變更其選擇之後立即更新使用者介面，請將 `Suppliers` DropDownList s `AutoPostBack` 屬性設定為 [`true`]。 在步驟2中，我們將建立 DetailsView 控制項，它會根據選取的 DropDownList 顯示供應商的資訊。 然後，在步驟3中，我們將為這個 DropDownList 的 `SelectedIndexChanged` 事件建立事件處理常式，我們會根據選取的供應商，將適當供應商資訊系結至 DetailsView 的程式碼。

## <a name="step-2-adding-a-detailsview-control"></a>步驟2：新增 DetailsView 控制項

讓 s 使用 DetailsView 來顯示供應商資訊。 對於可以查看和編輯所有供應商的使用者，DetailsView 將支援分頁，讓使用者一次一筆記錄就能逐步執行供應商資訊。 不過，如果使用者適用于特定供應商，則 DetailsView 只會顯示該特定供應商的資訊，且不會包含分頁介面。 不論是哪一種情況，DetailsView 都必須允許使用者編輯供應商的位址、城市和國家（地區）欄位。

將 DetailsView 新增至 [`Suppliers`] DropDownList 底下的頁面，將其 [`ID`] 屬性設定為 [`SupplierDetails`]，並將它系結至在上一個步驟中建立的 `AllSuppliersDataSource` ObjectDataSource。 接下來，核取 [啟用分頁] 和 [啟用編輯] 核取方塊（來自 DetailsView s 智慧標籤）。

> [!NOTE]
> 如果您沒有在 DetailsView s 智慧標籤中看到 [啟用編輯] 選項，因為您未將 ObjectDataSource s `Update()` 方法對應到 `SuppliersBLL` 類別 s `UpdateSupplierAddress` 方法。 請花點時間返回並進行這項設定變更，在這之後，[啟用編輯] 選項應該會出現在 DetailsView s 智慧標籤中。

由於 `SuppliersBLL` 類別的 `UpdateSupplierAddress` 方法只接受四個參數，`supplierID`、`address`、`city`和 `country` 修改 DetailsView s BoundFields，讓 `CompanyName` 和 `Phone` BoundFields 都是唯讀的。 此外，請完全移除 `SupplierID` BoundField。 最後，`AllSuppliersDataSource` ObjectDataSource 目前的 `OldValuesParameterFormatString` 屬性設定為 `original_{0}`。 請花點時間從宣告式語法中移除此屬性設定，或將它設定為預設值 `{0}`。

設定 `SupplierDetails` DetailsView 並 `AllSuppliersDataSource` ObjectDataSource 之後，我們將會有下列宣告式標記：

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample2.aspx)]

此時，DetailsView 可以進行分頁，而且選取的供應商位址資訊可以更新，而不論在 `Suppliers` DropDownList 中所做的選擇為何（請參閱 [圖 6]）。

[![可以查看任何供應商資訊，並更新其位址](limiting-data-modification-functionality-based-on-the-user-cs/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image16.png)

**圖 6**：可以查看任何供應商資訊，並更新其位址（[按一下以觀看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image18.png)）

## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>步驟3：只顯示選取的供應商資訊

我們的頁面目前會顯示所有供應商的資訊，而不論是否已從 `Suppliers` DropDownList 中選取特定供應商。 為了只顯示所選供應商的供應商資訊，我們需要在頁面中新增另一個 ObjectDataSource，以抓取特定供應商的相關資訊。

將新的 ObjectDataSource 加入至頁面，並將其命名為 `SingleSupplierDataSource`。 從其智慧標籤，按一下 [設定資料來源] 連結，並讓它使用 `SuppliersBLL` 類別的 `GetSupplierBySupplierID(supplierID)` 方法。 如同 `AllSuppliersDataSource` ObjectDataSource，請將 `SingleSupplierDataSource` ObjectDataSource s `Update()` 方法對應到 `SuppliersBLL` 類別的 `UpdateSupplierAddress` 方法。

[![將 SingleSupplierDataSource ObjectDataSource 設定為使用 GetSupplierBySupplierID （已加入供應商）方法](limiting-data-modification-functionality-based-on-the-user-cs/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image19.png)

**圖 7**：將 `SingleSupplierDataSource` ObjectDataSource 設定為使用 `GetSupplierBySupplierID(supplierID)` 方法（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image21.png)）

接下來，我們會提示您指定 `GetSupplierBySupplierID(supplierID)` 方法 s `supplierID` 輸入參數的參數來源。 因為我們想要顯示從 DropDownList 中選取之供應商的資訊，所以請使用 `Suppliers` DropDownList s `SelectedValue` 屬性作為參數來源。

[![使用供應商 DropDownList 作為廠商參數來源](limiting-data-modification-functionality-based-on-the-user-cs/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image22.png)

**圖 8**：使用 `Suppliers` DropDownList 作為 `supplierID` 參數來源（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image24.png)）

即使加入此第二個 ObjectDataSource，DetailsView 控制項目前已設定為一律使用 `AllSuppliersDataSource` ObjectDataSource。 我們需要新增邏輯，以根據選取的 `Suppliers` DropDownList 專案，調整 DetailsView 所使用的資料來源。 若要完成此動作，請建立供應商 DropDownList 的 `SelectedIndexChanged` 事件處理常式。 按兩下設計工具中的 DropDownList，即可輕鬆地建立此功能。 這個事件處理常式必須判斷要使用的資料來源，而且必須將資料重新系結至 DetailsView。 使用下列程式碼即可完成這項作業：

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample3.cs)]

事件處理常式會從判斷是否已選取 [顯示/編輯所有供應商] 選項開始。 如果是，則會將 `SupplierDetails` DetailsView s `DataSourceID` 設定為 `AllSuppliersDataSource`，並藉由將 `PageIndex` 屬性設定為0，將使用者傳回給供應商集合中的第一筆記錄。 不過，如果使用者已從 DropDownList 中選取特定供應商，則 DetailsView s `DataSourceID` 會指派給 `SingleSuppliersDataSource`。 不論使用何種資料來源，`SuppliersDetails` 模式都會還原成隻讀模式，而資料會藉由呼叫 `SuppliersDetails` 控制項 s `DataBind()` 方法來重新系結至 DetailsView。

使用此事件處理常式時，除非選取了 [顯示/編輯所有供應商] 選項，否則 DetailsView 控制項現在會顯示選取的供應商，在此情況下，所有供應商都可以透過分頁介面來查看。 [圖 9] 顯示已選取 [顯示/編輯所有供應商] 選項的頁面;請注意，分頁介面存在，可讓使用者造訪和更新任何供應商。 [圖 10] 顯示已選取 Ma Maison 供應商的頁面。 在此情況下，只能看到並編輯 Ma Maison 的資訊。

[![可以查看和編輯所有供應商資訊](limiting-data-modification-functionality-based-on-the-user-cs/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image25.png)

**圖 9**：可以查看和編輯所有供應商資訊（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image27.png)）

[只能查看和編輯所選供應商的資訊 ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image28.png)

**圖 10**：只能查看和編輯選取的供應商資訊（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image30.png)）

> [!NOTE]
> 在本教學課程中，DropDownList 和 DetailsView 控制項 `EnableViewState` 都必須設定為 `true` （預設值），因為 DropDownList s `SelectedIndex` 和 DetailsView s `DataSourceID` 屬性 s 變更必須在回傳之間記住。

## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>步驟4：在可編輯的 GridView 中列出供應商產品

完成 DetailsView 之後，我們的下一步是加入可編輯的 GridView，其中會列出所選供應商所提供的產品。 這個 GridView 應該只允許編輯 `ProductName` 和 `QuantityPerUnit` 欄位。 此外，如果造訪頁面的使用者是來自特定供應商，則只允許更新*未*中止的產品。 若要完成這項工作，我們必須先加入 `ProductsBLL` 類別 s `UpdateProducts` 方法的多載，只接受 `ProductID`、`ProductName`和 `QuantityPerUnit` 欄位做為輸入。 我們會在許多教學課程中事先逐步執行此程式，讓我們來看一下此處的程式碼，這應該新增至 `ProductsBLL`：

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample4.cs)]

建立此多載之後，我們就可以準備加入 GridView 控制項及其相關聯的 ObjectDataSource。 將新的 GridView 新增至頁面，將其 `ID` 屬性設為 `ProductsBySupplier`，並將其設定為使用名為 `ProductsBySupplierDataSource`的新 ObjectDataSource。 因為我們想要讓此 GridView 依據選取的供應商列出這些產品，所以請使用 `ProductsBLL` 類別 `GetProductsBySupplierID(supplierID)` 方法。 也會將 `Update()` 方法對應至我們剛才建立的新 `UpdateProduct` 多載。

[![將 ObjectDataSource 設定為使用剛建立的 UpdateProduct 多載](limiting-data-modification-functionality-based-on-the-user-cs/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image31.png)

**圖 11**：設定 ObjectDataSource 使用剛建立的 `UpdateProduct` 多載（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image33.png)）

系統會提示您選取 `GetProductsBySupplierID(supplierID)` 方法 s `supplierID` 輸入參數的參數來源。 因為我們想要顯示在 DetailsView 中所選供應商的產品，所以請使用 [`SuppliersDetails` DetailsView 控制項] `SelectedValue` 屬性作為參數來源。

[![使用 SuppliersDetails DetailsView s SelectedValue 屬性作為參數來源](limiting-data-modification-functionality-based-on-the-user-cs/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image34.png)

**圖 12**：使用 `SuppliersDetails` DetailsView s `SelectedValue` 屬性做為參數來源（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image36.png)）

返回 GridView，移除 `ProductName`、`QuantityPerUnit`和 `Discontinued`以外的所有 GridView 欄位，並將 `Discontinued` CheckBoxField 標記為唯讀。 此外，請檢查 GridView s 智慧標籤的 [啟用編輯] 選項。 進行這些變更之後，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample5.aspx)]

如同先前的 ObjectDataSources，這個 `OldValuesParameterFormatString` 屬性會設定為 `original_{0}`，這會在嘗試更新產品的名稱或每個單位的數量時造成問題。 請將此屬性從宣告式語法全部移除，或將它設定為預設值 `{0}`。

完成此設定後，我們的頁面現在會列出 GridView 中所選供應商所提供的產品（請參閱 [圖 13]）。 目前，每個單位的*任何*產品名稱或數量都可以更新。 不過，我們需要更新頁面邏輯，讓與特定供應商相關聯之使用者的已停止產品可以使用這類功能。 我們會在步驟5中解決這最後這一件。

[顯示所選供應商所提供的產品 ![](limiting-data-modification-functionality-based-on-the-user-cs/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image37.png)

**圖 13**：顯示所選供應商所提供的產品（[按一下以觀看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image39.png)）

> [!NOTE]
> 加入這個可編輯的 GridView 之後，就應該更新 `Suppliers` DropDownList s `SelectedIndexChanged` 事件處理常式，使 GridView 回到唯讀狀態。 否則，如果在編輯產品資訊時選取不同的供應商，則在 GridView 中，新供應商的對應索引也會是可編輯的。 若要避免這種情況，只要將 GridView 的 `EditIndex` 屬性設定為 `SelectedIndexChanged` 事件處理常式中的 `-1` 即可。

此外，請記得要啟用 GridView s 檢視狀態（預設行為）是很重要的。 如果您將 GridView 的 `EnableViewState` 屬性設定為 `false`，就會面臨並行使用者不小心刪除或編輯記錄的風險。 如需詳細資訊，請參閱[警告： ASP.NET 2.0 gridview/DetailsView/FormViews 的並行問題，其支援編輯及/或刪除，且已停用檢視狀態](http://scottonwriting.net/sowblog/posts/10054.aspx)。

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>步驟5：未選取 [顯示/編輯所有供應商] 時，不允許編輯已停止的產品

雖然 `ProductsBySupplier` GridView 完全正常運作，但它目前會授與來自特定供應商的使用者過多的存取權。 根據我們的商務規則，這類使用者應該無法更新已停止的產品。 若要強制執行這項工作，我們可以在使用者從供應商造訪頁面時，隱藏（或停用）那些 GridView 資料列中的 [編輯] 按鈕。

建立 GridView s `RowDataBound` 事件的事件處理常式。 在此事件處理常式中，我們需要判斷使用者是否與特定供應商相關聯，在本教學課程中，您可以藉由檢查供應商 DropDownList s `SelectedValue` 屬性（如果它不是-1）來決定是否要將使用者與特定供應商相關聯。 針對這類使用者，我們必須判斷產品是否已停止。 我們可以透過 `e.Row.DataItem` 屬性抓取與 GridView 資料列系結的實際 `ProductRow` 實例的參考，如在[*gridview 的頁尾中顯示摘要資訊*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md)教學課程中所述。 如果產品已停產，我們可以使用上一個教學課程中所討論的技巧，在 GridView CommandField 中抓取 [編輯] 按鈕的程式設計參考，並在[*刪除時新增用戶端確認*](adding-client-side-confirmation-when-deleting-cs.md)。 我們有了參考之後，就可以隱藏或停用按鈕。

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample6.cs)]

當此事件處理常式已就緒時，以特定供應商的使用者身分造訪此頁面時，將無法編輯已停止的產品，因為這些產品的 [編輯] 按鈕已隱藏。 例如，Chef Anton s Gumbo Mix 是新奧爾良 Cajun 樂趣供應商的已中止產品。 造訪此特定供應商的頁面時，會隱藏此產品的 [編輯] 按鈕（請參閱 [圖 14]）。 不過，當您使用 [顯示/編輯所有供應商] 進行流覽時，可以使用 [編輯] 按鈕（請參閱 [圖 15]）。

[適用于供應商專屬使用者的 ![[Chef Anton s Gumbo Mix] 的 [編輯] 按鈕已隱藏](limiting-data-modification-functionality-based-on-the-user-cs/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image40.png)

**圖 14**：對於供應商專屬的使用者，[Chef Anton s Gumbo Mix] 的 [編輯] 按鈕是隱藏的（[按一下以觀看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image42.png)）

[![顯示/編輯所有供應商使用者，會顯示 [Chef Anton s Gumbo Mix] 的 [編輯] 按鈕](limiting-data-modification-functionality-based-on-the-user-cs/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image43.png)

**圖 15**：針對 [顯示/編輯所有供應商使用者]，會顯示 [Chef Anton s Gumbo Mix] 的 [編輯] 按鈕（[按一下以查看完整大小的影像](limiting-data-modification-functionality-based-on-the-user-cs/_static/image45.png)）

## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>檢查商務邏輯層中的存取權限

在本教學課程中，ASP.NET 網頁會處理有關使用者可以看到哪些資訊以及可以更新哪些產品的所有邏輯。 在理想的情況下，此邏輯也會出現在商務邏輯層。 例如，`SuppliersBLL` 類別 `GetSuppliers()` 方法（傳回所有供應商）可能包括檢查，以確保目前登入的使用者*沒有*與特定供應商相關聯。 同樣地，`UpdateSupplierAddress` 方法可能會包含檢查，以確保目前登入的使用者可以在公司中運作（因此可以更新所有供應商位址資訊），或與資料正在更新的供應商相關聯。

我在本教學課程中並未包含這類 BLL 層檢查，因為在我們的教學課程中，使用者的權利是由頁面上的 DropDownList （BLL 類別無法存取）所決定。 使用成員資格系統或 ASP.NET 提供的其中一種驗證配置（例如 Windows 驗證）時，可以從 BLL 存取目前登入的使用者資訊和角色資訊，進而進行這類存取在簡報和 BLL 層級都可以進行許可權檢查。

## <a name="summary"></a>總結

大部分提供使用者帳戶的網站，都必須根據登入的使用者自訂資料修改介面。 系統管理使用者可能可以刪除和編輯任何記錄，而非系統管理使用者可能會受到限制，只能更新或刪除本身自行建立的記錄。 無論是哪種情況，都可以擴充資料 Web 控制項、ObjectDataSource 和商務邏輯層類別，以根據登入的使用者來新增或拒絕特定功能。 在本教學課程中，我們已瞭解如何根據使用者是否與特定供應商相關聯，或是否適用于我們的公司，來限制可查看和可編輯的資料。

本教學課程將說明如何使用 GridView、DetailsView 和 FormView 控制項來插入、更新和刪除資料。 從下一個教學課程開始，我們會將我們的注意力轉向新增分頁和排序支援。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](adding-client-side-confirmation-when-deleting-cs.md)
> [下一頁](an-overview-of-inserting-updating-and-deleting-data-vb.md)
