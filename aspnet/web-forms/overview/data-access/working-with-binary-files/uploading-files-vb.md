---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
title: 上傳檔案（VB） |Microsoft Docs
author: rick-anderson
description: 瞭解如何允許使用者將二進位檔案（例如 Word 或 PDF 檔）上傳至您的網站，而這些檔案可能會儲存在伺服器的檔案系統中 。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: f7c00fbd-652c-433d-8ed3-0e5168a4d4df
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e0d57ef2f1e8132f19777a7d14e94611c68adcd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615448"
---
# <a name="uploading-files-vb"></a>上傳檔案 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_VB.exe)或[下載 PDF](uploading-files-vb/_static/datatutorial54vb1.pdf)

> 瞭解如何允許使用者將二進位檔案（例如 Word 或 PDF 檔）上傳至您的網站，這些檔案可以儲存在伺服器的檔案系統或資料庫中。

## <a name="introduction"></a>簡介

目前為止我們檢查過的所有教學課程，都是以獨佔方式處理文字資料。 不過，許多應用程式都有可同時捕捉文字和二進位資料的資料模型。 線上可追溯網站可以讓使用者上傳圖片，使其與設定檔產生關聯。 招聘網站可能會讓使用者將其繼續上傳為 Microsoft Word 或 PDF 檔。

使用二進位資料會增加一組新的挑戰。 我們必須決定二進位資料儲存在應用程式中的方式。 用來插入新記錄的介面必須更新，才能讓使用者從其電腦上傳檔案，而且必須採取額外的步驟，才能顯示或提供下載記錄相關二進位資料的方法。 在本教學課程和接下來的三個中，我們將探討如何解決這些挑戰。 在這些教學課程的結尾，我們將建立一個功能完整的應用程式，讓圖片與 PDF 手冊與每個類別產生關聯。 在本教學課程中，我們將探討儲存二進位資料的不同技術，並探索如何讓使用者從電腦上傳檔案，並將它儲存在 web 伺服器 s 檔案系統上。

> [!NOTE]
> 屬於應用程式資料模型一部分的二進位資料有時稱為「 [BLOB](http://en.wikipedia.org/wiki/Binary_large_object)」（二進位大型物件的縮寫）。 在這些教學課程中，我選擇使用「二進位」這兩個術語，雖然「BLOB」一詞是同義。

## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>步驟1：建立使用二進位資料網頁

開始探索與新增二進位資料支援相關的挑戰之前，讓我們先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程和接下來的三個網頁中使用。 從新增名為 `BinaryData`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`

![加入二進位資料相關教學課程的 ASP.NET 網頁](uploading-files-vb/_static/image1.gif)

**圖 1**：加入二進位資料相關教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`BinaryData`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將這個使用者控制項加入至 `Default.aspx`，方法是將它從方案總管拖曳至頁面 s 設計檢視。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](uploading-files-vb/_static/image2.gif)](uploading-files-vb/_static/image1.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](uploading-files-vb/_static/image2.png)）

最後，將這些頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，在增強 GridView `<siteMapNode>`之後，加入下列標記：

[!code-xml[Main](uploading-files-vb/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含使用二進位資料教學課程的專案。

![網站地圖現在包含使用二進位資料教學課程的專案](uploading-files-vb/_static/image3.gif)

**圖 3**：網站地圖現在包含使用二進位資料教學課程的專案

## <a name="step-2-deciding-where-to-store-the-binary-data"></a>步驟2：決定二進位資料的儲存位置

與應用程式資料模型相關聯的二進位資料可以儲存在下列兩個位置的其中一個： web 伺服器 s 檔案系統上具有儲存在資料庫中之檔案的參考;或直接在資料庫本身內（請參閱 [圖 4]）。 每種方法都有一組自己的優缺點，並獲得更詳細的討論。

[![二進位資料可以儲存在檔案系統上，或是直接存放在資料庫中。](uploading-files-vb/_static/image4.gif)](uploading-files-vb/_static/image3.png)

**圖 4**：二進位資料可以儲存在檔案系統上，或直接存放在資料庫中（[按一下以查看完整大小的影像](uploading-files-vb/_static/image4.png)）

假設我們想要擴充 Northwind 資料庫，讓圖片與每個產品產生關聯。 其中一個選項是將這些影像檔案儲存在 web 伺服器的檔案系統上，並將路徑記錄在 `Products` 表中。 使用這種方法時，我們會將 `ImagePath` 資料行新增至類型 `varchar(200)`的 `Products` 資料表中，也許是。 當使用者上傳 Chai 的圖片時，該圖片可能會儲存在 web 伺服器 s 檔案系統的 `~/Images/Tea.jpg`，其中 `~` 代表應用程式的實體路徑。 也就是說，如果網站的根目錄是實體路徑 `C:\Websites\Northwind\`，`~/Images/Tea.jpg` 就相當於 `C:\Websites\Northwind\Images\Tea.jpg`。 上傳影像檔案之後，我們會更新 `Products` 資料表中的 Chai 記錄，使其 `ImagePath` 的資料行參考新影像的路徑。 我們可以使用 `~/Images/Tea.jpg` 或只在我們決定將所有產品映射放在應用程式的 `Images` 資料夾中時 `Tea.jpg`。

將二進位資料儲存在檔案系統上的主要優點如下：

- 如我們稍後所見，**輕鬆執行**，儲存和抓取直接儲存在資料庫中的二進位資料，比透過檔案系統處理資料還需要更多的程式碼。 此外，為了讓使用者能夠查看或下載二進位資料，必須以該資料的 URL 呈現。 如果資料位於 web 伺服器的檔案系統上，則 URL 十分簡單。 不過，如果資料儲存在資料庫中，就必須建立網頁，以從資料庫中抓取和傳回資料。
- 若要**更廣泛存取二進位資料**，可能需要其他服務或應用程式才能存取二進位資料，而不能從資料庫提取資料。 例如，與每個產品相關聯的映射可能也必須透過[FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol)提供給使用者，在此情況下，我們會想要將二進位資料儲存在檔案系統上。
- **效能**如果二進位資料儲存在檔案系統上，則資料庫伺服器與 web 伺服器之間的需求和網路擁塞將會小於二進位資料直接儲存在資料庫中的情況。

將二進位資料儲存在檔案系統上的主要缺點是，它會將資料與資料庫分離。 如果從 `Products` 資料表中刪除記錄，則不會自動刪除 web 伺服器 s 檔案系統上的相關聯檔案。 我們必須撰寫額外的程式碼來刪除檔案，否則檔案系統將會與未使用的孤立檔案變得雜亂。 此外，在備份資料庫時，我們也必須務必在檔案系統上建立相關聯二進位資料的備份。 將資料庫移到另一個網站或伺服器會造成類似的挑戰。

或者，您也可以藉由建立 `varbinary`類型的資料行，將二進位資料直接儲存在 Microsoft SQL Server 2005 資料庫中。 如同其他可變長度的資料類型，您可以指定可保留在此資料行中的二進位資料長度上限。 例如，若要保留最多5000個位元組，請使用 `varbinary(5000)`;`varbinary(MAX)` 允許儲存體大小上限，約 2 GB。

直接在資料庫中儲存二進位資料的主要優點是二進位資料與資料庫記錄之間的緊密結合。 這樣可大幅簡化資料庫管理工作，例如備份或將資料庫移至不同的網站或伺服器。 此外，刪除記錄時，會自動刪除對應的二進位資料。 將二進位資料儲存在資料庫中也有更細微的好處。 如需更深入的討論，請參閱[使用 ASP.NET 2.0 直接將二進位檔案儲存在資料庫中](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx)。

> [!NOTE]
> 在 Microsoft SQL Server 2000 和更早版本中，`varbinary` 資料類型的最大限制為8000個位元組。 若要儲存多達 2 GB 的二進位資料，必須改為使用[`image` 資料類型](https://msdn.microsoft.com/library/ms187993.aspx)。 不過，在 SQL Server 2005 中加入 `MAX`，`image` 資料類型已被取代。 它仍然支援回溯相容性，但 Microsoft 宣佈 `image` 資料類型將會在 SQL Server 的未來版本中移除。

如果您使用較舊的資料模型，您可能會看到 `image` 的資料類型。 Northwind 資料庫的 `Categories` 資料表具有 `Picture` 資料行，可用來儲存分類之影像檔案的二進位資料。 由於 Northwind 資料庫在 Microsoft Access 和舊版的 SQL Server 中具有其根目錄，因此這個資料行的類型 `image`。

在本教學課程和接下來的三個中，我們將使用這兩種方法。 `Categories` 資料表已經有 `Picture` 的資料行，可用於儲存分類之影像的二進位內容。 我們會新增額外的資料行 `BrochurePath`，以在 web 伺服器 s 檔案系統上儲存 PDF 的路徑，可用來提供列印品質、精美的類別目錄。

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>步驟3：將`BrochurePath`資料行加入至`Categories`資料表

目前類別目錄資料表只有四個數據行： `CategoryID`、`CategoryName`、`Description`和 `Picture`。 除了這些欄位以外，我們還需要加入一個新的，以指向類別目錄的手冊（如果有的話）。 若要加入此資料行，請移至 [伺服器總管]，向下切入到資料表，以滑鼠右鍵按一下 [`Categories`] 資料表，然後選擇 [開啟資料表定義] （請參閱 [圖 5]）。 如果您看不到伺服器總管，請從 [View] 功能表選取 [伺服器總管] 選項，或按 Ctrl + Alt + S 來啟動它。

將新的 `varchar(200)` 資料行加入至名為 `BrochurePath` 的 `Categories` 資料表，並允許 `NULL`，然後按一下 [儲存] 圖示（或按 Ctrl + S）。

[![將 BrochurePath 資料行加入至分類資料表](uploading-files-vb/_static/image5.gif)](uploading-files-vb/_static/image5.png)

**圖 5**：將 `BrochurePath` 資料行加入 `Categories` 資料表（[按一下以查看完整大小的影像](uploading-files-vb/_static/image6.png)）

## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>步驟4：更新架構以使用`Picture`和`BrochurePath`資料行

資料存取層（DAL）中的 `CategoriesDataTable` 目前已定義四個 `DataColumn`： `CategoryID`、`CategoryName`、`Description`和 `NumberOfProducts`。 當我們最初是在[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程中設計此 DataTable 時，`CategoriesDataTable` 只有前三個數據行;[`NumberOfProducts`] 資料行是[使用具有詳細資料 DataList 教學課程的主要記錄項目符號清單，在主要/細節](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)中加入。

如*建立資料存取層*中所述，具類型資料集中的 datatable 組成商務物件。 Tableadapter 會負責與資料庫通訊，並以查詢結果填入商務物件。 `CategoriesDataTable` 由 `CategoriesTableAdapter`填入，其中包含三個數據抓取方法：

- `GetCategories()` 執行 TableAdapter s main 查詢，並傳回 `Categories` 資料表中所有記錄的 `CategoryID`、`CategoryName`和 `Description` 欄位。 主要查詢是自動產生的 `Insert` 和 `Update` 方法所使用的。
- `GetCategoryByCategoryID(categoryID)` 會傳回分類的 `CategoryID`、`CategoryName`和 `Description` 欄位，其 *`CategoryID` 等於「類別目錄*」。
- `GetCategoriesAndNumberOfProducts()`-傳回 `Categories` 資料表中所有記錄的 `CategoryID`、`CategoryName`和 `Description` 欄位。 也會使用子查詢來傳回與每個類別目錄相關聯的產品數目。

請注意，這些查詢都不會傳回 `Categories` 資料表 s `Picture` 或 `BrochurePath` 資料行;`CategoriesDataTable` 也不會為這些欄位提供 `DataColumn`。 若要使用 [圖片] 和 [`BrochurePath`] 屬性，我們必須先將其加入 `CategoriesDataTable`，然後更新 `CategoriesTableAdapter` 類別以傳回這些資料行。

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>新增`Picture`和`BrochurePath``DataColumn` s

首先，將這兩個數據行加入至 `CategoriesDataTable`。 以滑鼠右鍵按一下 [`CategoriesDataTable` s] 標頭，從內容功能表中選取 [新增]，然後選擇 [資料行] 選項。 這會在名為 `Column1`的 DataTable 中建立新的 `DataColumn`。 將此資料行重新命名為 `Picture`。 從屬性視窗將 `DataColumn` s `DataType` 屬性設定為 [`System.Byte[]`] （這不是下拉式清單中的選項，您必須在中輸入）。

[![建立名為 Picture 的 DataColumn，其資料類型為 System.object []](uploading-files-vb/_static/image6.gif)](uploading-files-vb/_static/image7.png)

**圖 6**：建立名為 `Picture` 的 `DataColumn`，其 `DataType` 為 `System.Byte[]` （[按一下以查看完整大小的影像](uploading-files-vb/_static/image8.png)）

將另一個 `DataColumn` 新增至 DataTable，使用預設 `DataType` 值（`System.String`）將它命名 `BrochurePath`。

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>從 TableAdapter 傳回`Picture`和`BrochurePath`值

在 `CategoriesDataTable`中加入這兩個 `DataColumn` 之後，我們就可以開始更新 `CategoriesTableAdapter`。 我們可以在主要的 TableAdapter 查詢中傳回這兩個數據行值，但這會在每次叫用 `GetCategories()` 方法時帶回二進位資料。 相反地，讓 s 更新主要的 TableAdapter 查詢以帶回 `BrochurePath`，並建立一個會傳回特定分類 `Picture` 資料行的額外資料抓取方法。

若要更新主要的 TableAdapter 查詢，請以滑鼠右鍵按一下 [`CategoriesTableAdapter` s] 標頭，然後從內容功能表中選擇 [設定] 選項。 這會顯示 [表格介面卡設定向導]，我們已在一些過去的教學課程中看到。 更新查詢以取回 `BrochurePath`，然後按一下 [完成]。

[![更新 SELECT 語句中的資料行清單，以同時傳回 BrochurePath](uploading-files-vb/_static/image7.gif)](uploading-files-vb/_static/image9.png)

**圖 7**：更新 `SELECT` 語句中的資料行清單，使其也傳回 `BrochurePath` （[按一下以觀看完整大小的影像](uploading-files-vb/_static/image10.png)）

使用 TableAdapter 的臨機操作 SQL 語句時，更新主查詢中的資料行清單會更新 TableAdapter 中所有 `SELECT` 查詢方法的資料行清單。 這表示 `GetCategoryByCategoryID(categoryID)` 方法已更新，以傳回 `BrochurePath` 的資料行，這可能是我們所預期的。 不過，它也會更新 `GetCategoriesAndNumberOfProducts()` 方法中的資料行清單，移除傳回每個類別目錄之產品數目的子查詢！ 因此，我們需要更新 `SELECT` 查詢的這個方法。 以滑鼠右鍵按一下 [`GetCategoriesAndNumberOfProducts()`] 方法，選擇 [設定]，然後將 `SELECT` 查詢還原回其原始值：

[!code-sql[Main](uploading-files-vb/samples/sample2.sql)]

接下來，建立新的 TableAdapter 方法，以傳回特定分類的 `Picture` 資料行值。 以滑鼠右鍵按一下 [`CategoriesTableAdapter` s] 標頭，然後選擇 [加入查詢] 選項以啟動 [TableAdapter 查詢設定向導]。 此 wizard 的第一個步驟會詢問我們是否要使用臨機操作 SQL 語句、新的預存程式或現有的程式來查詢資料。 選取 [使用 SQL 語句]，然後按 [下一步]。 因為我們將傳回資料列，請選擇第二個步驟中的 [選取傳回資料列] 選項。

[![選取 [使用 SQL 語句] 選項](uploading-files-vb/_static/image8.gif)](uploading-files-vb/_static/image11.png)

**圖 8**：選取 [使用 SQL 語句] 選項（[按一下以查看完整大小的影像](uploading-files-vb/_static/image12.png)）

[![，因為查詢將傳回 category 資料表中的記錄，請選擇 [選取] 以傳回資料列](uploading-files-vb/_static/image9.gif)](uploading-files-vb/_static/image13.png)

**圖 9**：因為查詢將從 category 資料表傳回記錄，請選擇 [選取] 以傳回資料列（[按一下以查看完整大小的影像](uploading-files-vb/_static/image14.png)）

在第三個步驟中，輸入下列 SQL 查詢，然後按 [下一步]：

[!code-sql[Main](uploading-files-vb/samples/sample3.sql)]

最後一個步驟是選擇新方法的名稱。 使用 `FillCategoryWithBinaryDataByCategoryID` 和 `GetCategoryWithBinaryDataByCategoryID` 來填入 DataTable，並分別傳回 DataTable 模式。 按一下 [完成] 以完成精靈。

[![選擇 TableAdapter s 方法的名稱](uploading-files-vb/_static/image10.gif)](uploading-files-vb/_static/image15.png)

**圖 10**：選擇 TableAdapter s 方法的名稱（[按一下以查看完整大小的影像](uploading-files-vb/_static/image16.png)）

> [!NOTE]
> 完成 [資料表介面卡查詢設定] 嚮導之後，您可能會看到一個對話方塊，通知您新的命令文字傳回的資料與主查詢的架構不同。 簡單地說，嚮導會注意到 TableAdapter 的主查詢 `GetCategories()` 傳回的架構與我們剛才建立的不同。 但這就是我們想要的，因此您可以忽略這則訊息。

此外，請記住，如果您使用臨機操作 SQL 語句，並在稍後的時間點使用此嚮導來變更 TableAdapter s 主查詢，它會將 `GetCategoryWithBinaryDataByCategoryID` 方法 s `SELECT` 語句的資料行清單修改成隻包含主要查詢中的資料行（亦即，它會從查詢中移除 `Picture` 的資料行）。 您必須手動更新資料行清單，以傳回 `Picture` 資料行，與我們稍早在此步驟中的 `GetCategoriesAndNumberOfProducts()` 方法所做的類似。

將兩個 `DataColumn` s 新增至 `CategoriesDataTable`，並將 `GetCategoryWithBinaryDataByCategoryID` 方法加入至 `CategoriesTableAdapter`之後，具類型資料集設計工具中的這些類別看起來應該像 [圖 11] 中的螢幕擷取畫面。

![DataSet 設計工具組含新的資料行和方法](uploading-files-vb/_static/image11.gif)

**圖 11**： DataSet 設計工具組含新的資料行和方法

## <a name="updating-the-business-logic-layer-bll"></a>更新商務邏輯層（BLL）

在 DAL 更新之後，剩下的工作就是擴大商務邏輯層（BLL）以包含新 `CategoriesTableAdapter` 方法的方法。 將下列方法新增至 `CategoriesBLL` 類別：

[!code-vb[Main](uploading-files-vb/samples/sample4.vb)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>步驟5：從用戶端將檔案上傳到 Web 服務器

收集二進位資料時，通常會由使用者提供這項資料。 若要捕捉此資訊，使用者必須能夠從他們的電腦上傳檔案到 web 伺服器。 上傳的資料必須與資料模型整合，這可能表示將檔案儲存至 web 伺服器的檔案系統，並將路徑新增至資料庫中的檔案，或將二進位內容直接寫入資料庫中。 在此步驟中，我們將探討如何允許使用者將檔案從他們的電腦上傳到伺服器。 在下一個教學課程中，我們會將您的注意力轉換成將上傳的檔案與資料模型整合。

ASP.NET 2.0 s new [FileUpload web 控制項](https://msdn.microsoft.com/library/ms227677(VS.80).aspx)提供一種機制，讓使用者能夠從他們的電腦傳送檔案到 Web 服務器。 FileUpload 控制項會轉譯為 `<input>` 專案，其 `type` 屬性設定為 [檔案]，而瀏覽器會顯示為具有 [流覽] 按鈕的文字方塊。 按一下 [流覽] 按鈕會顯示對話方塊，使用者可以從中選取檔案。 當表單回傳時，選取的檔案的內容會連同回傳一起傳送。 在伺服器端上，可以透過 FileUpload 控制項的屬性存取上傳檔案的相關資訊。

若要示範上傳檔案，請開啟 [`BinaryData`] 資料夾中的 [`FileUpload.aspx`] 頁面，將 [FileUpload] 控制項從 [工具箱] 拖曳至設計工具上，然後將 [控制項] `ID` 屬性設定為 [`UploadTest`]。 接下來，新增按鈕 Web 控制項設定其 `ID` 並 `Text` 屬性，分別 `UploadButton` 和上傳選取的檔案。 最後，將標籤 Web 控制項放在按鈕下方，清除其 `Text` 屬性，並將其 `ID` 屬性設定為 [`UploadDetails`]。

[![將 FileUpload 控制項新增至 [ASP.NET] 頁面](uploading-files-vb/_static/image12.gif)](uploading-files-vb/_static/image17.png)

**圖 12**：將 FileUpload 控制項新增至 [ASP.NET] 頁面（[按一下以查看完整大小的影像](uploading-files-vb/_static/image18.png)）

[圖 13] 顯示透過瀏覽器觀看的此頁面。 請注意，按一下 [流覽] 按鈕會顯示 [檔案選取] 對話方塊，讓使用者從他們的電腦挑選檔案。 一旦選取檔案之後，按一下 [上傳選取的檔案] 按鈕會導致回傳，將選取的檔案二進位內容傳送至 web 伺服器。

[![使用者可以選取要從電腦上傳到伺服器的檔案](uploading-files-vb/_static/image13.gif)](uploading-files-vb/_static/image19.png)

**圖 13**：使用者可以選取要從電腦上傳到伺服器的檔案（[按一下以查看完整大小的影像](uploading-files-vb/_static/image20.png)）

在回傳時，上傳的檔案可以儲存至檔案系統，或其二進位資料可以透過資料流程直接處理。 在此範例中，讓我們建立一個 `~/Brochures` 資料夾，並將上傳的檔案儲存在該處。 首先，將 `Brochures` 資料夾新增至網站，做為根目錄的子資料夾。 接下來，建立 `UploadButton` s `Click` 事件的事件處理常式，並新增下列程式碼：

[!code-vb[Main](uploading-files-vb/samples/sample5.vb)]

FileUpload 控制項提供各種不同的屬性來處理上傳的資料。 例如， [`HasFile` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx)會指出使用者是否已上傳檔案，而[`FileBytes` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx)則是以位元組陣列的形式提供上傳二進位資料的存取權。 `Click` 事件處理常式會藉由確保檔案已上傳來啟動。 如果檔案已上傳，則標籤會顯示已上傳檔案的名稱、其大小（以位元組為單位）及其內容類型。

> [!NOTE]
> 若要確保使用者上傳檔案，您可以檢查 [`HasFile`] 屬性，並在 `False`時顯示警告，或者您也可以改用[RequiredFieldValidator 控制項](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx)。

FileUpload s `SaveAs(filePath)` 會將上傳的檔案儲存至指定的*filePath*。 *filePath*必須是*實體路徑*（`C:\Websites\Brochures\SomeFile.pdf`），而不是*虛擬* *路徑*（`/Brochures/SomeFile.pdf`）。 [`Server.MapPath(virtPath)` 方法](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx)會採用虛擬路徑，並傳回其對應的實體路徑。 在這裡，虛擬路徑為 `~/Brochures/fileName`，其中*fileName*是上傳檔案的名稱。 如需虛擬和實體路徑及使用 `Server.MapPath`的詳細資訊，請參閱[使用 Server. MapPath](http://www.4guysfromrolla.com/webtech/121799-1.shtml) 。

完成 `Click` 事件處理常式之後，請花點時間在瀏覽器中測試頁面。 按一下 [流覽] 按鈕並從硬碟中選取檔案，然後按一下 [上傳選取的檔案] 按鈕。 回傳會將所選檔案的內容傳送至 web 伺服器，然後在將檔案儲存到 `~/Brochures` 資料夾之前，先顯示該檔案的相關資訊。 上傳檔案之後，請返回 Visual Studio，然後按一下方案總管中的 [重新整理] 按鈕。 您應該會在 ~/Brochures 資料夾中看到您剛才上傳的檔案！

[![檔案 EvolutionValley 已上傳至 Web 服務器](uploading-files-vb/_static/image14.gif)](uploading-files-vb/_static/image21.png)

**圖 14**：檔案 `EvolutionValley.jpg` 已上傳至 Web 服務器（[按一下以觀看完整大小的影像](uploading-files-vb/_static/image22.png)）

![EvolutionValley 已儲存至 ~/Brochures 資料夾](uploading-files-vb/_static/image15.gif)

**圖 15**： `EvolutionValley.jpg` 已儲存到 `~/Brochures` 資料夾

## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>將已上傳的檔案儲存到檔案系統的微妙差異

將上傳檔案儲存至 web 伺服器的檔案系統時，必須處理數個微妙差異。 首先，安全性的問題。 若要將檔案儲存至檔案系統，ASP.NET 網頁執行所在的安全性內容必須具有寫入權限。 ASP.NET 開發 Web 服務器會在您目前使用者帳戶的內容下執行。 如果您使用 Microsoft s Internet Information Services （IIS）做為 web 伺服器，則安全性內容取決於 IIS 的版本及其設定。

將檔案儲存至檔案系統的另一項挑戰，就是將檔案命名為。 目前，我們的頁面會使用與用戶端電腦上的檔案相同的名稱，將所有上傳的檔案儲存到 `~/Brochures` 目錄。 如果使用者上傳名稱為 `Brochure.pdf`的手冊，檔案將會儲存為 `~/Brochure/Brochure.pdf`。 但是，如果稍後使用者 B 上傳不同的摺頁冊檔案，而該檔案剛好有相同的檔案名（`Brochure.pdf`）呢？ 有了現在的程式碼，使用者 B 的上傳會覆寫使用者 A 的檔案。

有數種方法可解決檔案名衝突。 其中一個選項是禁止上傳檔案（如果已經有相同名稱的檔案的話）。 使用此方法時，當使用者 B 嘗試上傳名為 `Brochure.pdf`的檔案時，系統不會儲存其檔案，而是會顯示訊息，通知使用者 B 重新命名檔案，然後再試一次。 另一種方法是使用唯一的檔案名儲存檔案，這可能是[全域唯一識別碼（GUID）](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)或對應資料庫記錄 s 主鍵資料行中的值（假設上傳與資料模型中的特定資料列相關聯）。 在下一個教學課程中，我們將更詳細地探索這些選項。

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>大量二進位資料的相關挑戰

這些教學課程假設所捕獲的二進位資料大小適中。 使用非常大量的二進位資料檔案，這些檔案有數 mb 或更大的容量，引進了這些教學課程範圍以外的新挑戰。 例如，根據預設，ASP.NET 會拒絕超過 4 MB 的上傳，不過這可以透過 `Web.config`中的[`<httpRuntime>` 元素](https://msdn.microsoft.com/library/e1f13641.aspx)來設定。 IIS 也會強加自己的檔案上傳大小限制。 如需詳細資訊，請參閱[IIS 上傳檔案大小](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html)。 此外，上傳大型檔案所花費的時間可能會超過預設的110秒，ASP.NET 會等待要求。 在處理大型檔案時，也會發生記憶體和效能問題。

FileUpload 控制項對於大型檔案上傳而言不切實際。 當檔案的內容張貼到伺服器時，使用者必須耐心等待，而不需要確認其上傳進度。 在處理較小的檔案時，這並不是個問題，但在處理較大的檔案（可能需要幾分鐘的時間才能上傳）時可能會有問題。 有各種協力廠商檔案上傳控制項，較適合用來處理大量上傳，而其中有許多廠商提供進度指標和 ActiveX 上傳管理員，呈現更豐富的使用者體驗。

如果您的應用程式需要處理大型檔案，您必須仔細調查挑戰，並針對您的特定需求尋找適合的解決方案。

## <a name="summary"></a>總結

建立需要用來捕獲二進位資料的應用程式會帶來許多挑戰。 在本教學課程中，我們探討了前兩個：決定要儲存二進位資料的位置，並允許使用者透過網頁上傳二進位內容。 在接下來的三個教學課程中，我們將瞭解如何將上傳的資料與資料庫中的記錄產生關聯，以及如何在其文字資料欄位旁顯示二進位資料。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [使用大數值資料類型](https://msdn.microsoft.com/library/ms178158.aspx)
- [FileUpload 控制項快速入門](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2.0 FileUpload 伺服器控制項](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [檔案上傳的暗邊](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy 和 Bernadette Leigh。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](updating-and-deleting-existing-binary-data-cs.md)
> [下一頁](displaying-binary-data-in-the-data-web-controls-vb.md)
