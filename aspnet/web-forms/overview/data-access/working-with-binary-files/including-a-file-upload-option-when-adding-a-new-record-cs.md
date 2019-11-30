---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
title: 新增記錄時包含檔案上傳選項（C#） |Microsoft Docs
author: rick-anderson
description: 本教學課程說明如何建立 Web 介面，讓使用者可以輸入文字資料並上傳二進位檔案。 說明可用的選項 t 。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 362ade25-3965-4fb2-88d2-835c4786244f
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
msc.type: authoredcontent
ms.openlocfilehash: f1287e180151b3034a7b90ef4b3f1fbe68354a09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74577173"
---
# <a name="including-a-file-upload-option-when-adding-a-new-record-c"></a>新增記錄時包含檔案上傳選項 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_CS.exe)或[下載 PDF](including-a-file-upload-option-when-adding-a-new-record-cs/_static/datatutorial56cs1.pdf)

> 本教學課程說明如何建立 Web 介面，讓使用者可以輸入文字資料並上傳二進位檔案。 為了說明可用來儲存二進位資料的選項，其中一個檔案會儲存在資料庫中，而另一個檔案則儲存在檔案系統中。

## <a name="introduction"></a>簡介

在前兩個教學課程中，我們探討了用來儲存與應用程式資料模型相關聯之二進位資料的技巧，看看如何使用 FileUpload 控制項將檔案從用戶端傳送至 web 伺服器，並瞭解如何在資料中呈現此二進位資料（W）eb 控制項。 不過，我們還在討論如何將上傳的資料與資料模型產生關聯。

在本教學課程中，我們將建立網頁來加入新的類別。 除了分類的 [名稱] 和 [描述] 文字方塊以外，此頁面還需要包含兩個 FileUpload 控制項，其中一個用於新的分類圖片，另一個用於手冊。 上傳的圖片會直接儲存在新的 [記錄] `Picture` 資料行中，而該手冊會儲存至 [`~/Brochures`] 資料夾，其中包含儲存在 [新記錄] `BrochurePath` 資料行中的檔案路徑。

建立這個新的網頁之前，我們必須先更新架構。 `CategoriesTableAdapter` s 的主要查詢不會抓取 `Picture` 資料行。 因此，自動產生的 `Insert` 方法只會有 `CategoryName`、`Description`和 `BrochurePath` 欄位的輸入。 因此，我們需要在 TableAdapter 中建立額外的方法，以提示所有四個 `Categories` 欄位。 商務邏輯層中的 `CategoriesBLL` 類別也需要更新。

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>步驟1：將`InsertWithPicture`方法加入至`CategoriesTableAdapter`

當我們在[建立資料存取層](../introduction/creating-a-data-access-layer-cs.md)教學課程中建立了 `CategoriesTableAdapter` 時，我們已將它設定為根據主要查詢自動產生 `INSERT`、`UPDATE`和 `DELETE` 語句。 此外，我們會指示 TableAdapter 採用 DB 直接方法，這會建立方法 `Insert`、`Update`和 `Delete`。 這些方法會執行自動產生的 `INSERT`、`UPDATE`和 `DELETE` 語句，因此，會根據主要查詢所傳回的資料行來接受輸入參數。 在 [[上傳](uploading-files-cs.md)檔案] 教學課程中，我們增強了 `CategoriesTableAdapter` s 主查詢，以使用 [`BrochurePath`] 資料行。

由於 `CategoriesTableAdapter` s 主查詢不會參考 `Picture` 的資料行，因此我們不可以加入新的記錄，也不會使用 [`Picture`] 資料行的值來更新現有的記錄。 為了捕捉這項資訊，我們可以在 TableAdapter 中建立新的方法，專門用來插入含有二進位資料的記錄，或者我們可以自訂自動產生的 `INSERT` 語句。 自訂自動產生的 `INSERT` 語句的問題是，我們會在嚮導覆寫我們的自訂時有風險。 例如，假設我們已自訂 `INSERT` 語句，以包含 `Picture` 資料行的使用。 這會更新 TableAdapter 的 `Insert` 方法，使其包含分類 s 圖片的二進位資料的額外輸入參數。 然後，我們可以在商務邏輯層中建立方法，以使用此 DAL 方法，並透過展示層叫用這個 BLL 方法，而所有作業都 wonderfully。 也就是，直到下一次透過 [TableAdapter 設定] [嚮導] 設定 TableAdapter 為止。 當 wizard 完成時，就會覆寫 `INSERT` 語句的自訂，`Insert` 方法會還原成舊的表單，而我們的程式碼將不再編譯！

> [!NOTE]
> 當您使用預存程式而非臨機操作 SQL 語句時，這項干擾不會發生問題。 未來的教學課程將探索如何使用預存程式代替資料存取層中的臨機操作 SQL 語句。

若要避免這種可能的麻煩，而不是自訂自動產生的 SQL 語句，請改為建立 TableAdapter 的新方法。 這個名為 `InsertWithPicture`的方法會接受 `CategoryName`、`Description`、`BrochurePath`和 `Picture` 資料行的值，並執行 `INSERT` 語句，將全部四個值儲存在新的記錄中。

開啟具類型的資料集，然後從設計工具中，以滑鼠右鍵按一下 [`CategoriesTableAdapter`] 標頭，然後從內容功能表選擇 [加入查詢]。 這會啟動 [TableAdapter 查詢設定] Wizard，其一開始會詢問 TableAdapter 查詢應該如何存取資料庫。 選擇 [使用 SQL 語句]，然後按 [下一步]。 下一個步驟會提示您輸入要產生的查詢類型。 因為我們會重新建立查詢，以便將新記錄加入 `Categories` 資料表中，請選擇 [插入]，然後按 [下一步]。

[![選取 [插入] 選項](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.png)

**圖 1**：選取 [插入] 選項（[按一下以查看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.png)）

我們現在需要指定 `INSERT` SQL 語句。 Wizard 會自動建議與 TableAdapter s 主查詢對應的 `INSERT` 語句。 在此情況下，它是插入 `CategoryName`、`Description`和 `BrochurePath` 值的 `INSERT` 語句。 更新語句，讓 `Picture` 資料行連同 `@Picture` 參數一起包含，如下所示：

[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample1.sql)]

Wizard 的最後一個畫面會要求我們將新的 TableAdapter 方法命名為。 輸入 `InsertWithPicture`，然後按一下 [完成]。

[![命名新的 TableAdapter 方法 InsertWithPicture](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.png)

**圖 2**：將新的 TableAdapter 方法命名 `InsertWithPicture` （[按一下以查看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.png)）

## <a name="step-2-updating-the-business-logic-layer"></a>步驟2：更新商務邏輯層

因為展示層應該只與商務邏輯層互動，而不是略過它直接進入資料存取層，所以我們需要建立一個會叫用剛才建立之 DAL 方法的 BLL 方法（`InsertWithPicture`）。 在本教學課程中，請在名為 `InsertWithPicture` 的 `CategoriesBLL` 類別中建立方法，以接受做為輸入三 `string` s 和 `byte` 陣列。 `string` 輸入參數適用于類別目錄的名稱、描述和手冊檔案路徑，而 `byte` 陣列則適用于類別目錄圖片的二進位內容。 如下列程式碼所示，這個 BLL 方法會叫用對應的 DAL 方法：

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample2.cs)]

> [!NOTE]
> 將 `InsertWithPicture` 方法加入至 BLL 之前，請確定您已儲存具類型的資料集。 由於會根據具類型的資料集自動產生 `CategoriesTableAdapter` 類別程式碼，因此，如果您不先將變更儲存至具類型的資料集，`Adapter` 屬性就不會知道 `InsertWithPicture` 方法的相關資訊。

## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>步驟3：列出現有的類別及其二進位資料

在本教學課程中，我們將建立可讓使用者將新類別新增至系統的頁面，並為新的類別提供圖片和手冊。 在[先前的教學](displaying-binary-data-in-the-data-web-controls-cs.md)課程中，我們使用了 GridView 搭配 TemplateField 和 ImageField 來顯示每個類別目錄的名稱、描述、圖片，以及下載其手冊的連結。 讓我們在本教學課程中複寫該功能，建立同時列出所有現有分類並允許建立新類別的頁面。

從 [`BinaryData`] 資料夾開啟 [`DisplayOrDownload.aspx`] 頁面開始。 移至來源視圖並複製 GridView 和 ObjectDataSource 的宣告式語法，並將其貼入 `UploadInDetailsView.aspx`的 `<asp:Content>` 元素中。 此外，別忘了將 `GenerateBrochureLink` 方法從 `DisplayOrDownload.aspx` 的程式碼後置類別複製到 `UploadInDetailsView.aspx`。

[![複製 DisplayOrDownload 中的宣告式語法，並將其貼入 UploadInDetailsView](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.png)

**圖 3**：從 `DisplayOrDownload.aspx` 複製並貼上宣告式語法至 `UploadInDetailsView.aspx` （[按一下以查看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.png)）

將宣告式語法和 `GenerateBrochureLink` 方法複製到 `UploadInDetailsView.aspx` 頁面之後，請透過瀏覽器查看頁面，以確保所有專案都已正確複製。 您應該會看到 GridView 列出八個類別，其中包含可下載手冊的連結，以及類別目錄的圖片。

[![您現在應該會看到每個類別及其二進位資料](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.png)

**圖 4**：您現在應該會看到每個類別及其二進位資料（[按一下以查看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.png)）

## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>步驟4：設定`CategoriesDataSource`以支援插入

`Categories` GridView 使用的 `CategoriesDataSource` ObjectDataSource 目前不提供插入資料的能力。 為了支援透過這個資料來源控制項插入，我們必須將其 `Insert` 方法對應到其基礎物件中的方法，`CategoriesBLL`。 特別是，我們想要將它對應至我們在步驟 2 `InsertWithPicture`中新增的 `CategoriesBLL` 方法。

從 [ObjectDataSource s] 智慧標籤按一下 [設定資料來源] 連結開始。 第一個畫面會顯示資料來源已設定為使用的物件，`CategoriesBLL`。 將此設定保持原狀，然後按 [下一步] 進入 [定義資料方法] 畫面。 移至 [插入] 索引標籤，然後從下拉式清單中挑選 `InsertWithPicture` 方法。 按一下 [完成] 以完成精靈。

[![將 ObjectDataSource 設定為使用 InsertWithPicture 方法](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.png)

**圖 5**：設定 ObjectDataSource 以使用 `InsertWithPicture` 方法（[按一下以查看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.png)）

> [!NOTE]
> 完成此嚮導之後，Visual Studio 可能會詢問您是否要重新整理欄位和金鑰，這會重新產生資料 Web 控制項欄位。 選擇 [否]，因為選擇 [是] 將會覆寫您所做的任何欄位自訂。

完成 wizard 之後，ObjectDataSource 現在會包含其 `InsertMethod` 屬性的值，以及四個類別資料行的 `InsertParameters`，如下列宣告式標記所示：

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>步驟5：建立插入介面

第一次[探討插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)時，DetailsView 控制項提供內建的插入介面，可在使用支援插入的資料來源控制項時使用。 讓我們將 DetailsView 控制項新增至 GridView 上方的這個頁面，以永久轉譯其插入介面，讓使用者可以快速地加入新的類別。 在 DetailsView 中加入新的類別時，其底下的 GridView 會自動重新整理並顯示新的類別。

首先，從 [工具箱] 將 [DetailsView] 拖曳至 GridView 上方的設計工具，將其 [`ID`] 屬性設定為 `NewCategory`，並清除 `Height` 和 `Width` 屬性值。 從 DetailsView s 智慧標籤，將它系結至現有的 `CategoriesDataSource`，然後勾選 [啟用插入] 核取方塊。

[![將 DetailsView 系結至 CategoriesDataSource 並啟用插入](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.png)

**圖 6**：將 DetailsView 系結至 `CategoriesDataSource` 並啟用插入（[按一下以觀看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image12.png)）

若要在其插入介面中永久轉譯 DetailsView，請將其 [`DefaultMode`] 屬性設定為 [`Insert`]。

請注意，DetailsView 有五個 BoundFields `CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`和 `BrochurePath`，雖然 `CategoryID` 的 BoundField 不會在插入介面中轉譯，因為它的 `InsertVisible` 屬性會設定為 [`false`]。 這些 BoundFields 已存在，因為它們是 `GetCategories()` 方法所傳回的資料行，而 ObjectDataSource 會叫用它來抓取其資料。 不過，在插入時，我們不想讓使用者指定 `NumberOfProducts`的值。 此外，我們還必須允許它們上傳新類別的圖片，以及上傳手冊的 PDF。

完全移除 DetailsView 中的 `NumberOfProducts` BoundField，然後將 `CategoryName` 的 `HeaderText` 屬性和 `BrochurePath` BoundFields 分別更新為 Category 和手冊。 接下來，將 `BrochurePath` BoundField 轉換成 TemplateField，並為圖片新增新的 TemplateField，讓這個新 TemplateField 成為 `HeaderText` 的圖片值。 移動 `Picture` TemplateField，使其介於 `BrochurePath` TemplateField 和 CommandField 之間。

![將 DetailsView 系結至 CategoriesDataSource 並啟用插入](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.gif)

**圖 7**：將 DetailsView 系結至 `CategoriesDataSource` 並啟用插入

如果您透過 [編輯欄位] 對話方塊，將 `BrochurePath` BoundField 轉換為 TemplateField，則 TemplateField 會包含 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 不過，只需要 `InsertItemTemplate`，因此，您可以隨意移除其他兩個範本。 此時，DetailsView 的宣告式語法應如下所示：

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>新增 [手冊] 和 [圖片] 欄位的 FileUpload 控制項

目前，`BrochurePath` TemplateField s `InsertItemTemplate` 包含 TextBox，而 `Picture` TemplateField 不包含任何範本。 我們需要更新這兩個 TemplateField `InsertItemTemplate` s，才能使用 FileUpload 控制項。

從 DetailsView s 智慧標籤中，選擇 [編輯範本] 選項，然後從下拉式清單中選取 `BrochurePath` TemplateField s `InsertItemTemplate`。 移除文字方塊，然後將 [FileUpload] 控制項從 [工具箱] 拖曳到範本中。 將 FileUpload 控制項 s `ID` 設定為 `BrochureUpload`。 同樣地，將 FileUpload 控制項新增至 `Picture` TemplateField s `InsertItemTemplate`。 將此 FileUpload 控制項 s `ID` 設定為 `PictureUpload`。

[![將 FileUpload 控制項新增至 InsertItemTemplate](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image13.png)

**圖 8**：將 FileUpload 控制項新增至 `InsertItemTemplate` （[按一下以查看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image14.png)）

進行這些新增動作之後，兩個 TemplateField 的宣告式語法會是：

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample5.aspx)]

當使用者加入新的類別時，我們想要確保手冊和圖片的檔案類型正確無誤。 針對手冊，使用者必須提供 PDF。 在此圖片中，我們需要使用者上傳影像檔案，但我們允許*任何*影像檔案，或是只有特定類型的影像檔案，例如 Gif 或 jpg？ 為了允許不同的檔案類型，我們必須擴充 `Categories` 架構，使其包含可捕捉檔案類型的資料行，以便透過 `DisplayCategoryPicture.aspx`中的 `Response.ContentType`，將此類型傳送至用戶端。 因為我們沒有這類資料行，所以要限制使用者只能提供特定的影像檔案類型，是非常謹慎的。 `Categories` 資料表的現有影像是點陣圖，但 Jpg 是更適合透過 web 提供之影像的檔案格式。

如果使用者上傳的檔案類型不正確，我們必須取消插入，並顯示指出問題的訊息。 在 DetailsView 底下新增標籤 Web 控制項。 將其 [`ID`] 屬性設定為 [`UploadWarning`]，清除其 `Text` 屬性，將 [`CssClass`] 屬性設為 [警告]，並將 [`Visible`] 和 [`EnableViewState`] 屬性設定為 `false` `Warning` CSS 類別是在 `Styles.css` 中定義，並以大、紅色、斜體、粗體字型呈現文字。

> [!NOTE]
> 在理想的情況下，`CategoryName` 和 `Description` BoundFields 會轉換成 TemplateFields，並自訂其插入介面。 例如，插入介面的 `Description` 可能較適合透過多行文字方塊。 而且由於 `CategoryName` 資料行不接受 `NULL` 值，因此應新增 RequiredFieldValidator，以確保使用者提供新類別目錄名稱的值。 這些步驟會保留為讀者的練習。 請回頭[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)，以深入瞭解如何擴充資料修改介面。

## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>步驟6：將上傳的手冊儲存至 Web 服務器 s 檔案系統

當使用者輸入新類別的值，並按一下 [插入] 按鈕時，就會發生回傳並插入工作流程色彩。 首先，會引發 DetailsView s [`ItemInserting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx)。 接下來，會叫用 ObjectDataSource s `Insert()` 方法，這會導致新的記錄新增至 `Categories` 資料表。 之後，會引發 DetailsView s [`ItemInserted` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx)。

叫用 ObjectDataSource s `Insert()` 方法之前，我們必須先確定使用者已上傳適當的檔案類型，然後將手冊 PDF 儲存至 web 伺服器的檔案系統。 建立 DetailsView s `ItemInserting` 事件的事件處理常式，並新增下列程式碼：

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample6.cs)]

事件處理常式一開始會從 DetailsView 的範本中參考 `BrochureUpload` FileUpload 控制項。 然後，如果已上傳手冊，則會檢查上傳的檔案 s 延伸模組。 如果擴充功能不是，則為。PDF，則會顯示警告、插入已取消，以及事件處理常式的執行結束。

> [!NOTE]
> 依賴已上傳的檔案的延伸模組並不是確保上傳的檔案是 PDF 檔的一種不確定的方法。 使用者可以擁有副檔名為 `.Brochure`的有效 PDF 檔，或可能已取得非 PDF 檔，並將其指定為 `.pdf` 延伸模組。 必須以程式設計方式檢查檔案的二進位內容，才能更最終驗證檔案類型。 不過，這種徹底的方法通常是大材小用;檢查延伸模組就足以應付大部分的情況。

如[上傳](uploading-files-cs.md)檔案教學課程中所述，將檔案儲存到檔案系統時必須特別小心，讓一個使用者上傳不會覆寫另一個。 在本教學課程中，我們會嘗試使用與上傳檔案相同的名稱。 不過，如果 `~/Brochures` 目錄中已經有同名的檔案，我們會在結尾附加一個數位，直到找到唯一的名稱為止。 例如，如果使用者上傳名為 `Meats.pdf`的手冊檔案，但 `~/Brochures` 資料夾中已經有名為 `Meats.pdf` 的檔案，我們會將儲存的檔案名變更為 `Meats-1.pdf`。 如果存在，我們會嘗試 `Meats-2.pdf`，依此類推，直到找到唯一的檔案名為止。

下列程式碼會使用[`File.Exists(path)` 方法](https://msdn.microsoft.com/library/system.io.file.exists.aspx)來判斷檔案是否已存在，並具有指定的檔案名。 若是如此，它會繼續嘗試手冊的新檔案名，直到找不到任何衝突為止。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample7.cs)]

一旦找到有效的檔案名，就必須將檔案儲存到檔案系統，而且必須更新 ObjectDataSource s `brochurePath``InsertParameter` 值，才能將此檔案名寫入資料庫中。 如我們在*上傳*檔案教學課程中所見，您可以使用 FileUpload 控制項 `SaveAs(path)` 方法來儲存檔案。 若要更新 ObjectDataSource s `brochurePath` 參數，請使用 `e.Values` 集合。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample8.cs)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>步驟7：將上傳的圖片儲存到資料庫

若要將上傳的圖片儲存在新的 `Categories` 記錄中，我們必須將已上傳的二進位內容指派給 DetailsView s `ItemInserting` 事件中的 ObjectDataSource s `picture` 參數。 不過，在進行此指派之前，我們必須先確定上傳的圖片是 JPG，而不是其他影像類型。 如步驟6所示，讓 s 使用上傳的圖片的副檔名來確定其類型。

雖然 `Categories` 資料表允許 `NULL` `Picture` 資料行的值，但所有的分類目前都有一張圖片。 讓使用者在透過此頁面新增類別時，強制提供圖片。 下列程式碼會檢查並確定圖片已上傳，而且它具有適當的延伸模組。

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample9.cs)]

這個程式碼應該放在步驟6的程式碼*之前*，如此一來，如果圖片上傳發生問題，則在將手冊檔案儲存到檔案系統之前，事件處理常式會終止。

假設已上傳適當的檔案，請使用下列程式程式碼，將已上傳的二進位內容指派給圖片參數 s 值：

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample10.cs)]

## <a name="the-completeiteminsertingevent-handler"></a>完整的`ItemInserting`事件處理常式

為求完整性，以下是完整的 `ItemInserting` 事件處理常式：

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample11.cs)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>步驟8：修正`DisplayCategoryPicture.aspx`頁面

讓我們花點時間測試在最後幾個步驟所建立的插入介面和 `ItemInserting` 事件處理常式。 透過瀏覽器造訪 [`UploadInDetailsView.aspx`] 頁面並嘗試新增類別，但省略圖片，或指定非 JPG 圖片或非 PDF 手冊。 在上述任一情況下，將會顯示錯誤訊息，並取消插入工作流程。

[如果上傳的檔案類型無效，就會顯示 ![警告訊息](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image15.png)

**圖 9**：如果上傳了不正確檔案類型，就會顯示警告訊息（[按一下以查看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image16.png)）

一旦您確認頁面需要上傳圖片，而且不接受非 PDF 或非 JPG 檔案，請加入具有有效 JPG 圖片的新類別，並將 [摺頁冊] 欄位保留空白。 按一下 [插入] 按鈕之後，頁面將回傳，而新的記錄將會加入至 [`Categories`] 資料表中，並將已上傳的影像 s 二進位內容直接儲存在資料庫中。 GridView 會更新，並顯示新加入之類別目錄的資料列，但如 [圖 10] 所示，新的分類圖片並未正確轉譯。

[![不會顯示新的分類圖片](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image17.png)

**圖 10**：不會顯示新的分類圖片（[按一下以觀看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image18.png)）

新圖片未顯示的原因是，會將傳回指定分類圖片的 `DisplayCategoryPicture.aspx` 頁面設定為處理具有 OLE 標頭的點陣圖。 這個78位元組標頭會從 `Picture` 資料行的二進位內容中移除，然後再傳送回用戶端。 但我們剛剛為新類別上傳的 JPG 檔案沒有此 OLE 標頭;因此，從影像的二進位資料中移除有效的必要位元組。

因為現在 `Categories` 資料表中有兩個位圖具有 OLE 標頭和 Jpg，所以我們需要更新 `DisplayCategoryPicture.aspx`，讓它針對原始八個類別進行 OLE 標頭的去除，並略過較新類別記錄的去除。 在下一個教學課程中，我們將探討如何更新現有的記錄影像，並更新所有舊的類別圖片，使其 Jpg。 不過，現在，請在 `DisplayCategoryPicture.aspx` 中使用下列程式碼，只針對那些原始八個類別來去除 OLE 標頭：

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample12.cs)]

透過這項變更，JPG 影像現在會在 GridView 中正確轉譯。

[已正確轉譯新類別的 JPG 影像 ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image19.png)

**圖 11**：已正確轉譯新類別的 JPG 影像（[按一下以觀看完整大小的影像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image20.png)）

## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>步驟9：在遇到例外狀況時刪除手冊

將二進位資料儲存在 web 伺服器的檔案系統上的其中一項挑戰，就是它會在資料模型及其二進位資料之間引進中斷連接。 因此，每當刪除記錄時，也必須移除檔案系統上對應的二進位資料。 這也可以在插入時播放。 請考慮下列案例：使用者新增了新的類別，並指定有效的圖片和手冊。 按一下 [插入] 按鈕時，會發生回傳並引發 DetailsView s `ItemInserting` 事件，將手冊儲存至 web 伺服器 s 檔案系統。 接下來，會叫用 ObjectDataSource s `Insert()` 方法，這會呼叫 `CategoriesBLL` 類別 s `InsertWithPicture` 方法，以呼叫 `CategoriesTableAdapter` s `InsertWithPicture` 方法。

現在，如果資料庫離線，或 `INSERT` SQL 語句中有錯誤，會發生什麼事？ 很明顯地，插入將會失敗，因此不會將新的類別資料列新增至資料庫。 但是我們還是把上傳的摺頁冊檔案放在 web 伺服器的檔案系統上！ 在插入工作流程期間，如果發生例外狀況，則需要刪除此檔案。

如先前在[ASP.NET 網頁中處理 BLL 和 DAL 層級的例外](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)狀況教學課程中所述，當從架構的深度中擲回例外狀況時，它會透過各種層級向上展開。 在展示層中，我們可以判斷 DetailsView s `ItemInserted` 事件是否發生例外狀況。 這個事件處理常式也會提供 ObjectDataSource s `InsertParameters`的值。 因此，我們可以建立 `ItemInserted` 事件的事件處理常式，以檢查是否發生例外狀況，如果是的話，則會刪除 ObjectDataSource s `brochurePath` 參數所指定的檔案：

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample13.cs)]

## <a name="summary"></a>總結

為了提供以 web 為基礎的介面來新增包含二進位資料的記錄，必須執行幾個步驟。 如果二進位資料直接儲存到資料庫中，您可能需要更新架構，並加入特定方法來處理插入二進位資料的情況。 一旦架構更新之後，下一步就是建立插入介面，使用已自訂為包含每個二進位資料欄位之 FileUpload 控制項的 DetailsView 即可完成。 然後，可以將上傳的資料儲存至 web 伺服器的檔案系統，或指派給 DetailsView s `ItemInserting` 事件處理常式中的資料來源參數。

將二進位資料儲存到檔案系統需要比直接將資料儲存到資料庫更多的規劃。 必須選擇命名配置，才能避免一個使用者上傳覆寫另一個。 此外，如果資料庫插入失敗，則必須採取額外的步驟來刪除已上傳的檔案。

我們現在可以在系統中加入新的類別，其中包含手冊和圖片，但我們尚未探討如何更新現有的類別二進位資料，或如何正確地移除已刪除之類別的二進位資料。 我們將在下一個教學課程中探索這兩個主題。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dave Gardner、Teresa Murphy 和 Bernadette Leigh。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](displaying-binary-data-in-the-data-web-controls-cs.md)
> [下一頁](updating-and-deleting-existing-binary-data-cs.md)
