---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-cs
title: 在資料 Web 控制項中顯示二進位資料（C#） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討在網頁上顯示二進位資料的選項，包括影像檔的顯示和布建的「下載」連結 。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 5cbeb9f8-5f92-4ba8-87ae-0b4d460ae6d4
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: f38de7adcd77b3dc2622759646168cf533b8308f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642723"
---
# <a name="displaying-binary-data-in-the-data-web-controls-c"></a>以資料 Web 控制項顯示二進位資料 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_CS.exe)或[下載 PDF](displaying-binary-data-in-the-data-web-controls-cs/_static/datatutorial55cs1.pdf)

> 在本教學課程中，我們將探討在網頁上顯示二進位資料的選項，包括影像檔的顯示，以及 PDF 檔案的「下載」連結。

## <a name="introduction"></a>簡介

在先前的教學課程中，我們探討了兩種將二進位資料與應用程式基礎資料模型產生關聯的技巧，並使用 FileUpload 控制項將檔案從瀏覽器上傳至 web 伺服器的檔案系統。 我們還不知道如何將上傳的二進位資料與資料模型產生關聯。 也就是說，在檔案上傳並儲存到檔案系統之後，檔案的路徑必須儲存在適當的資料庫記錄中。 如果資料是直接儲存在資料庫中，則上傳的二進位資料不需要儲存到檔案系統，但必須插入資料庫中。

不過，在我們探討如何將資料與資料模型產生關聯之前，先來看一下如何將二進位資料提供給終端使用者。 呈現文字資料很簡單，但要如何呈現二進位資料呢？ 當然，這也取決於二進位資料的類型。 針對影像，我們可能會想要顯示影像;針對 Pdf、Microsoft Word 檔、ZIP 檔案和其他類型的二進位資料，提供下載連結可能比較合適。

在本教學課程中，我們將探討如何使用資料 Web 控制項（如 GridView 和 DetailsView），將二進位資料連同其相關聯的文字資料一起呈現。 在下一個教學課程中，我們將重點放在將上傳的檔案與資料庫產生關聯。

## <a name="step-1-providingbrochurepathvalues"></a>步驟1：提供`BrochurePath`值

`Categories` 資料表中的 `Picture` 資料行已經包含各種類別目錄影像的二進位資料。 具體而言，每筆記錄的 `Picture` 資料行都包含有顆粒狀、低品質、16色點陣圖影像的二進位內容。 每個類別影像都是172圖元寬和120圖元高，而且會耗用大約 11 KB。 此外，`Picture` 資料行中的二進位內容包含78位元組的[OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding)標頭，必須先將其移除，才能顯示影像。 此標頭資訊存在，因為 Northwind 資料庫在 Microsoft Access 中具有其根目錄。 在 Access 中，會使用 OLE 物件資料類型來儲存二進位資料，而此資料類型會添加到在此標頭上。 現在，我們將瞭解如何從這些低品質影像中去除標頭，以顯示圖片。 在未來的教學課程中，我們將建立一個介面來更新 category `Picture` 資料行，並將使用 OLE 標頭的這些點陣圖影像取代為對等的 JPG 影像，而不需要不必要的 OLE 標頭。

在先前的教學課程中，我們看到了如何使用 FileUpload 控制項。 因此，您可以將手冊檔案加入至 web 伺服器 s 檔案系統。 不過，這樣做並不會更新 `Categories` 資料表中的 `BrochurePath` 資料行。 在下一個教學課程中，我們將瞭解如何完成這項工作，但現在我們需要手動提供此資料行的值。

在本教學課程中，您可以在 [`~/Brochures`] 資料夾中找到七個 PDF 手冊檔案，其中每個類別都有 [海鮮] 除外。 我特意省略了新增海鮮手冊，以說明如何處理並非所有記錄都有相關聯的二進位資料的案例。 若要使用這些值來更新 `Categories` 資料表，請以滑鼠右鍵按一下伺服器總管的 [`Categories`] 節點，然後選擇 [顯示資料表資料]。 然後，針對每個具有手冊的類別輸入手冊檔案的虛擬路徑，如 [圖 1] 所示。 由於 [海鮮] 分類沒有任何手冊，請將其 `BrochurePath` 的 [資料行] 值保留為 [`NULL`]。

[![手動輸入 category Table s BrochurePath 資料行的值](displaying-binary-data-in-the-data-web-controls-cs/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image1.png)

**圖 1**：手動輸入 `Categories` 資料表 s `BrochurePath` 資料行的值（[按一下以查看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image2.png)）

## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>步驟2：在 GridView 中提供摺頁冊的下載連結

針對 `Categories` 資料表提供的 `BrochurePath` 值，我們已準備好建立 GridView，其中列出每個類別，以及下載類別目錄手冊的連結。 在步驟4中，我們將擴充此 GridView，以同時顯示類別目錄的影像。

首先，從 [工具箱] 將 GridView 拖曳至 [`BinaryData`] 資料夾中 [`DisplayOrDownloadData.aspx`] 頁面的設計工具。 將 GridView 的 `ID` 設定為 `Categories`，並透過 GridView 的智慧標籤，選擇將其系結至新的資料來源。 具體而言，請將它系結至名為 `CategoriesDataSource` 的 ObjectDataSource，以使用 `CategoriesBLL` 物件 s `GetCategories()` 方法來抓取資料。

[![建立名為 CategoriesDataSource 的新 ObjectDataSource](displaying-binary-data-in-the-data-web-controls-cs/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image3.png)

**圖 2**：建立名為 `CategoriesDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image4.png)）

[![將 ObjectDataSource 設定為使用 CategoriesBLL 類別](displaying-binary-data-in-the-data-web-controls-cs/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image5.png)

**圖 3**：設定 ObjectDataSource 使用 `CategoriesBLL` 類別（[按一下以查看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image6.png)）

[![使用 GetCategories （）方法來抓取分類清單](displaying-binary-data-in-the-data-web-controls-cs/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image7.png)

**圖 4**：使用 `GetCategories()` 方法抓取分類清單（[按一下以查看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image8.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 會自動將 BoundField 新增至 `CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`和 `BrochurePath` `DataColumn` s 的 `Categories` GridView。 請繼續並移除 `NumberOfProducts` BoundField，因為 `GetCategories()` 方法 s 查詢不會抓取這則資訊。 同時移除 `CategoryID` BoundField，並將 `CategoryName` 和 `BrochurePath` BoundFields `HeaderText` 屬性分別重新命名為 Category 和手冊。 進行這些變更之後，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample1.aspx)]

透過瀏覽器觀看此頁面（請參閱 [圖 5]）。 列出八個類別中的每一個。 具有 `BrochurePath` 值的七個分類會在個別 BoundField 中顯示 `BrochurePath` 值。 具有 `BrochurePath`之 `NULL` 值的海鮮，會顯示空的資料格。

[![列出每個類別目錄的名稱、描述和 BrochurePath 值](displaying-binary-data-in-the-data-web-controls-cs/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image9.png)

**圖 5**：每個分類的名稱、描述和 `BrochurePath` 值都會列出（[按一下以觀看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image10.png)）

我們想要建立手冊的連結，而不是顯示 `BrochurePath` 資料行的文字。 若要完成此動作，請移除 `BrochurePath` BoundField，並將它取代為 HyperLinkField。 將 [新的 HyperLinkField] `HeaderText` 屬性設定為 [手冊]、將 [`Text`] 屬性設為 [摺頁冊]，並將其 `DataNavigateUrlFields` 屬性設定為 `BrochurePath`。

![新增 BrochurePath 的 HyperLinkField](displaying-binary-data-in-the-data-web-controls-cs/_static/image6.gif)

**圖 6**：新增 HyperLinkField 以 `BrochurePath`

這會加入 GridView 連結的資料行，如 [圖 7] 所示。 按一下 [View 宣傳冊] 連結會在瀏覽器中直接顯示 PDF，或提示使用者下載檔案，視是否已安裝 PDF 閱讀程式和瀏覽器的設定而定。

[按一下 [View 摺頁冊] 連結，即可觀看 ![的分類手冊](displaying-binary-data-in-the-data-web-controls-cs/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image11.png)

**圖 7**：您可以按一下 [view 摺頁冊] 連結（[按一下以觀看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image12.png)）來查看類別目錄

[![會顯示類別目錄手冊的 PDF](displaying-binary-data-in-the-data-web-controls-cs/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image13.png)

**圖 8**：顯示的是分類的手冊 PDF （[按一下以觀看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image14.png)）

## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>隱藏沒有手冊之類別的 View 手冊文字

如 [圖 7] 所示，不論是否有 `BrochurePath`的非`NULL` 值，`BrochurePath` HyperLinkField 都會顯示所有記錄的 `Text` 屬性值（View 宣傳冊）。 當然，如果 `NULL``BrochurePath`，則連結只會顯示為文字，如同 [海鮮] 分類的情況（請參閱 [圖 7]）。 不顯示文字視圖手冊，如果沒有 `BrochurePath` 值會顯示一些替代文字（例如沒有可用的手冊），則可能會很不錯。

為了提供這種行為，我們必須使用 TemplateField，其內容是透過呼叫頁面方法所產生的，該方法會根據 `BrochurePath` 值發出適當的輸出。 我們先在 GridView 控制項教學課程中[使用 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)探索此格式化技巧。

藉由選取 [`BrochurePath`] HyperLinkField，然後按一下 [編輯資料行] 對話方塊中的 [將此欄位轉換成 TemplateField] 連結，將 HyperLinkField 轉換為 TemplateField。

![將 HyperLinkField 轉換成 TemplateField](displaying-binary-data-in-the-data-web-controls-cs/_static/image9.gif)

**圖 9**：將 HyperLinkField 轉換成 TemplateField

這會建立具有 `ItemTemplate` 的 TemplateField，其中包含超連結 Web 控制項，其 `NavigateUrl` 屬性系結至 `BrochurePath` 值。 使用方法的呼叫來取代此標記 `GenerateBrochureLink`，傳入 `BrochurePath`的值：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample2.aspx)]

接下來，在 ASP.NET 網頁的程式碼後置類別中，建立名為 `GenerateBrochureLink` 的 `protected` 方法，其會傳回 `string` 並接受 `object` 做為輸入參數。

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample3.cs)]

這個方法會判斷傳入的 `object` 值是否為資料庫 `NULL`，如果是的話，則會傳回訊息，指出類別缺少手冊。 否則，如果有 `BrochurePath` 值，它就會顯示在超連結中。 請注意，如果 `BrochurePath` 值存在，它就會傳遞至[`ResolveUrl(url)` 方法](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)。 這個方法會解析傳入的*url*，以適當的虛擬路徑取代 `~` 字元。 例如，如果應用程式的根目錄為 `/Tutorial55`，`ResolveUrl("~/Brochures/Meats.pdf")` 會傳回 `/Tutorial55/Brochures/Meat.pdf`。

[圖 10] 顯示套用這些變更後的頁面。 請注意，[海鮮] 分類的 [`BrochurePath`] 欄位現在會顯示 [沒有可用的手冊] 文字。

[![不含手冊的那些類別顯示 [沒有可用的手冊] 文字](displaying-binary-data-in-the-data-web-controls-cs/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image15.png)

**圖 10**：不含手冊的類別會顯示不提供任何手冊的文字（[按一下以觀看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image16.png)）

## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>步驟3：新增網頁以顯示分類的圖片

當使用者造訪 ASP.NET 網頁時，他們會收到 ASP.NET 網頁的 HTML。 收到的 HTML 只是文字，不包含任何二進位資料。 任何其他的二進位資料（例如影像、音效檔、Macromedia Flash 應用程式、內嵌的 Windows 媒體播放機影片等等）都會以個別的資源形式存在於 web 伺服器上。 HTML 包含這些檔案的參考，但不包含檔案的實際內容。

例如，在 HTML 中，`<img>` 專案是用來參考圖片，其中 `src` 屬性會指向影像檔，如下所示：

[!code-html[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample4.html)]

當瀏覽器收到此 HTML 時，會向網頁伺服器提出另一項要求，以抓取影像檔案的二進位內容，然後在瀏覽器中顯示該檔案。 相同的概念也適用于任何二進位資料。 在步驟2中，手冊不會傳送至瀏覽器，做為網頁 s HTML 標籤的一部分。 相反地，所呈現的 HTML 提供的超連結，會在按一下時導致瀏覽器直接要求 PDF 檔。

若要顯示或允許使用者下載位於資料庫內的二進位資料，我們必須建立會傳回資料的個別網頁。 在我們的應用程式中，只有一個二進位資料欄位直接儲存在資料庫中，即類別目錄的圖片。 因此，我們需要一個頁面，當呼叫它時，會傳回特定分類的影像資料。

將新的 ASP.NET 網頁新增至名為 `DisplayCategoryPicture.aspx`的 `BinaryData` 資料夾。 執行此動作時，請將 [選取主版頁面] 核取方塊保持未選取狀態。 此頁面需要 querystring 中的 `CategoryID` 值，並傳回該分類的 `Picture` 資料行的二進位資料。 由於此頁面會傳回二進位資料，而不會傳回任何其他內容，因此在 HTML 區段中不需要任何標記。 因此，請按一下左下角的 [來源] 索引標籤，並移除 [`<%@ Page %>`] 指示詞以外的所有 page s 標記。 也就是說，`DisplayCategoryPicture.aspx` s 宣告式標記應該包含一行：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample5.aspx)]

如果您在 `<%@ Page %>` 指示詞中看到 `MasterPageFile` 屬性，請將它移除。

在 [程式碼後置] 類別中，將下列程式碼加入 `Page_Load` 事件處理常式：

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample6.cs)]

此程式碼一開始會將 `CategoryID` querystring 值讀入名為 `categoryID`的變數中。 接下來，會透過呼叫 `CategoriesBLL` 類別的 `GetCategoryWithBinaryDataByCategoryID(categoryID)` 方法來抓取圖片資料。 這項資料會使用 `Response.BinaryWrite(data)` 方法傳回給用戶端，但在呼叫這個資料之前，必須先移除 `Picture` 資料行值 s OLE 標頭。 這是藉由建立名為 `strippedImageData` 的 `byte` 陣列來完成，其會保留比 `Picture` 資料行中精確的78個字元。 [`Array.Copy` 方法](https://msdn.microsoft.com/library/z50k9bft.aspx)是用來將從位置78開始 `category.Picture` 的資料複製到 `strippedImageData`。

`Response.ContentType` 屬性會指定要傳回之內容的[MIME 類型](http://en.wikipedia.org/wiki/MIME)，讓瀏覽器知道如何呈現它。 由於 `Categories` 資料表的 `Picture` 資料行是點陣圖影像，因此會在這裡使用 bitmap MIME 類型（image/bmp）。 如果您省略 MIME 類型，大部分的瀏覽器仍然會正確顯示影像，因為它們可以根據影像檔案的二進位資料內容來推斷類型。 不過，盡可能包含 MIME 類型是非常謹慎的。 如需[MIME 媒體類型](http://www.iana.org/assignments/media-types/)的完整清單，請參閱[網際網路指派的數位授權單位網站](http://www.iana.org/)。

建立此頁面之後，您可以造訪 `DisplayCategoryPicture.aspx?CategoryID=categoryID`來查看特定的類別圖片。 [圖 11] 顯示飲料類別目錄的圖片，可以從 `DisplayCategoryPicture.aspx?CategoryID=1`查看。

[會顯示 [飲料] 類別的圖片 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image17.png)

**圖 11**：顯示飲料類別的圖片（[按一下以觀看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image18.png)）

當造訪 `DisplayCategoryPicture.aspx?CategoryID=categoryID`時，您會收到例外狀況，指出無法將 ' System.object ' 類型的物件轉換成類型 ' system.string [] '，這可能會造成這種情況。 首先，`Categories` table s `Picture` 資料行確實允許 `NULL` 值。 不過，[`DisplayCategoryPicture.aspx`] 頁面會假設有一個非`NULL` 值存在。 如果具有 `NULL` 值，則無法直接存取 `CategoriesDataTable` 的 `Picture` 屬性。 如果您想要允許 `NULL` `Picture` 資料行的值，您應該要包含下列條件：

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample7.cs)]

上述程式碼假設在 `Images` 資料夾中，有一個名為 `NoPictureAvailable.gif` 的影像檔案，而您想要在沒有圖片的情況下顯示這些類別。

如果 `CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` 方法 s `SELECT` 語句還原回主要查詢的資料行清單，可能會發生這個例外狀況，這可能是因為您使用臨機操作 SQL 語句，而且您已針對 TableAdapter s 主要查詢重新執行 wizard。 檢查以確定 `GetCategoryWithBinaryDataByCategoryID` 方法的 `SELECT` 語句仍然包含 `Picture` 的資料行。

> [!NOTE]
> 每次造訪 `DisplayCategoryPicture.aspx` 時，就會存取資料庫並傳回指定的分類圖片資料。 不過，如果類別的圖片自從使用者上次觀看後並未變更，這就是浪費精力。 幸好，HTTP 允許*條件式取得*。 透過條件式取得，提出 HTTP 要求的用戶端會沿著[`If-Modified-Since` HTTP 標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)傳送，以提供用戶端上次從 web 伺服器抓取此資源的日期和時間。 如果在指定的日期後內容尚未變更，web 伺服器可能會以[未修改的狀態碼（304）](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)回應，並放棄傳回要求的資源內容。 簡單地說，這項技術讓網頁伺服器不需要傳送回資源的內容（如果它在用戶端上次存取之後未曾修改過）。

不過，若要執行這種行為，您必須將 `PictureLastModified` 資料行加入至 `Categories` 資料表，以便在上次更新 `Picture` 資料行時進行捕捉，以及檢查 `If-Modified-Since` 標頭的程式碼。 如需有關 `If-Modified-Since` 標頭和條件式取得工作流程的詳細資訊，請參閱[RSS 駭客的 HTTP 條件式取得](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers)，以及[深入瞭解如何在 ASP.NET 網頁中執行 HTTP 要求](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx)。

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>步驟4：在 GridView 中顯示類別圖片

既然我們已經有一個網頁來顯示特定的分類圖片，我們可以使用[影像 web 控制項](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx)或指向 `DisplayCategoryPicture.aspx?CategoryID=categoryID`的 HTML `<img>` 元素來顯示它。 其 URL 是由資料庫資料決定的影像，可以使用 ImageField 在 GridView 或 DetailsView 中顯示。 ImageField 包含 `DataImageUrlField` 和 `DataImageUrlFormatString` 屬性，其作用類似 HyperLinkField s `DataNavigateUrlFields` 和 `DataNavigateUrlFormatString` 屬性。

藉由新增 ImageField 以顯示每個類別目錄的圖片，讓擴充 `DisplayOrDownloadData.aspx` 中的 `Categories` GridView。 只需新增 ImageField，並將其 `DataImageUrlField` 和 `DataImageUrlFormatString` 屬性分別設定為 `CategoryID` 和 `DisplayCategoryPicture.aspx?CategoryID={0}`。 這會建立 GridView 資料行，以轉譯 `src` 屬性參考 `DisplayCategoryPicture.aspx?CategoryID={0}`的 `<img>` 專案，其中 {0} 會以 GridView 資料列 s `CategoryID` 值來取代。

![將 ImageField 新增至 GridView](displaying-binary-data-in-the-data-web-controls-cs/_static/image12.gif)

**圖 12**：將 ImageField 新增至 GridView

加入 ImageField 之後，GridView 的宣告式語法看起來應該如下 soothe：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample8.aspx)]

請花點時間透過瀏覽器觀看此頁面。 請注意，每一筆記錄現在如何包含類別的圖片。

[![顯示每個資料列的類別目錄圖片](displaying-binary-data-in-the-data-web-controls-cs/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image19.png)

**圖 13**：每個資料列都會顯示類別目錄的圖片（[按一下以觀看完整大小的影像](displaying-binary-data-in-the-data-web-controls-cs/_static/image20.png)）

## <a name="summary"></a>總結

在本教學課程中，我們已檢查如何呈現二進位資料。 資料的呈現方式取決於資料類型。 針對 PDF 摺頁冊檔案，我們提供使用者一個 View 宣傳冊連結，當您按下該按鈕時，會將使用者直接帶到 PDF 檔案。 針對類別目錄的圖片，我們先建立一個頁面來抓取和傳回資料庫的二進位資料，然後使用該頁面來顯示 GridView 中的每個類別目錄。

既然我們已經討論過如何顯示二進位資料，我們已經準備好檢查如何對資料庫執行插入、更新和刪除，以及二進位資料。 在下一個教學課程中，我們將探討如何將上傳的檔案與其對應的資料庫記錄產生關聯。 在本教學課程中，我們將瞭解如何更新現有的二進位資料，以及如何在移除其相關聯的記錄時刪除二進位資料。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy 和 Dave Gardner。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](uploading-files-cs.md)
> [下一頁](including-a-file-upload-option-when-adding-a-new-record-cs.md)
