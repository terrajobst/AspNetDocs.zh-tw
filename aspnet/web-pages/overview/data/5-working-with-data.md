---
uid: web-pages/overview/data/5-working-with-data
title: 在 ASP.NET Web Pages （Razor）網站中使用資料庫的簡介 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何從資料庫存取資料，並使用 ASP.NET Web Pages 加以顯示。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586531"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET Web Pages （Razor）網站中使用資料庫的簡介

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何使用 Microsoft WebMatrix 工具在 ASP.NET Web Pages （Razor）網站中建立資料庫，以及如何建立可讓您顯示、新增、編輯和刪除資料的頁面。
> 
> **您將瞭解的內容：** 
> 
> - 如何建立資料庫。
> - 如何連接到資料庫。
> - 如何在網頁中顯示資料。
> - 如何插入、更新和刪除資料庫記錄。
> 
> 以下是文章中引進的功能：
> 
> - 使用 Microsoft SQL Server Compact 版本資料庫。
> - 使用 SQL 查詢。
> - `Database` 類別。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - WebMatrix 2
>   
> 
> 本教學課程也適用于 WebMatrix 3。 您可以使用 ASP.NET Web Pages 3 和 Visual Studio 2013 （或適用于 Web 的 Visual Studio Express 2013）;不過，使用者介面將會不同。

## <a name="introduction-to-databases"></a>資料庫簡介

想像一下一般通訊錄。 針對通訊錄中的每個專案（亦即，針對每個人），您會有數個資訊片段，例如名字、姓氏、位址、電子郵件地址和電話號碼。

以這種方式進行資料圖片的一般方法，就像是具有資料列和資料行的資料表。 在資料庫詞彙中，每個資料列通常稱為「記錄」。 每個資料行（有時稱為「欄位」）都會包含每個資料類型的值：「名字」、「姓氏」等等。

| **ID** | **FirstName** | **姓氏** | **位址** | **電子郵件** | **電話** |
| --- | --- | --- | --- | --- | --- |
| 1 | Jim | Abrus | 210第100個 St SE Orcas WA 98031 | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234主要 St. 西雅圖 WA 99011 | terry@cohowinery.com | 555 0101 |

對於大部分的資料庫資料表而言，資料表必須有一個包含唯一識別碼的資料行，例如客戶編碼、帳戶號碼等等。這就是所謂的資料表*主鍵*，您可以用它來識別資料表中的每個資料列。 在此範例中，[識別碼] 資料行是通訊錄的主要金鑰。

有了對資料庫的基本瞭解之後，您就可以開始學習如何建立簡單的資料庫，並執行新增、修改和刪除資料等作業。

> [!TIP] 
> 
> **關聯式資料庫**
> 
> 您可以用許多方式來儲存資料，包括文字檔和試算表。 不過，對於大部分的企業用途而言，資料會儲存在關係資料庫中。
> 
> 本文不會深入探討資料庫。 不過，您可能會發現很難瞭解。 在關係資料庫中，資訊會以邏輯方式分割成不同的資料表。 例如，學校的資料庫可能包含學生的個別資料表和類別供應專案。 資料庫軟體（例如 SQL Server）支援強大的命令，可讓您以動態方式建立資料表之間的關聯性。 例如，您可以使用關係資料庫來建立學生與類別之間的邏輯關聯性，以便建立排程。 將資料儲存在不同的資料表中可減少資料表結構的複雜性，並減少在資料表中保留多餘資料的需求。

## <a name="creating-a-database"></a>建立資料庫

此程式說明如何使用 WebMatrix 隨附的 SQL Server Compact 資料庫設計工具，建立名為 SmallBakery 的資料庫。 雖然您可以使用程式碼建立資料庫，但更常見的做法是使用 WebMatrix 之類的設計工具來建立資料庫和資料庫資料表。

1. 啟動 WebMatrix，然後在 [快速入門] 頁面上，按一下 [**來自範本的網站**]。
2. 選取 [**空白網站**]，然後在 [**網站名稱**] 方塊中輸入 "SmallBakery"，然後按一下 **[確定]** 。 網站隨即建立，並顯示在 WebMatrix 中。
3. 在左窗格中，按一下 [**資料庫**] 工作區。
4. 在功能區中，按一下 [**新增資料庫**]。 系統會使用與您的網站相同的名稱來建立空的資料庫。
5. 在左窗格中，展開 [ **SmallBakery** ] 節點，然後按一下 [**資料表]** 。
6. 在功能區中，按一下 [**新增資料表**]。 WebMatrix 會開啟 [資料表設計工具]。

    ![[影像]](5-working-with-data/_static/image1.jpg)
7. 按一下 [**名稱**] 資料行，然後輸入 &quot;識別碼&quot;。
8. 在 [**資料類型] 資料**行中，選取 [ **int**]。
9. 設定 [**是主要金鑰嗎？** ] 和 [**識別**] 選項為 **[是]** 。

    如其名稱所示， **Primary key**會告訴資料庫這將是資料表的主鍵。 [身分**識別] 會**告訴資料庫自動建立每個新記錄的識別碼，並將下一個序號指派給它（從1開始）。
10. 按一下下一個資料列。 編輯器會啟動新的資料行定義。
11. 在 [名稱] 值中，輸入 &quot;名稱&quot;。
12. 針對 [**資料類型**]，選擇 [&quot;Nvarchar&quot;]，並將 [長度] 設定為50。 `nvarchar` 的*var*部分會告訴資料庫，此資料行的資料會是字串，其大小可能會因記錄而異。 （ *N*前置詞代表*國家（地區*），表示欄位可以保存代表任何字母或書寫系統&#8212;的字元資料，也就是欄位保留 Unicode 資料）。
13. 將 [**允許 Null]** 選項設為 [**否**]。 這會強制 [*名稱*] 資料行不會保留空白。
14. 使用此相同進程，建立名為*Description*的資料行。 將 [**資料類型**] 設定為 [Nvarchar]，並將 [長度] 設定為50，並將 [**允許 null]** 設為 false
15. 建立名為*Price*的資料行。 將 **[資料類型] 設定為 [money]** ，並將 [**允許 null]** 設定為 false。
16. 在頂端的方塊中，將資料表命名為 &quot;產品&quot;。

    當您完成時，定義看起來會像這樣：

    ![[影像]](5-working-with-data/_static/image2.png)
17. 按 Ctrl + S 以儲存資料表。

## <a name="adding-data-to-the-database"></a>將資料新增至資料庫

現在您可以將一些範例資料新增至您的資料庫，以便稍後在本文中使用。

1. 在左窗格中，展開 [ **SmallBakery** ] 節點，然後按一下 [**資料表]** 。
2. 以滑鼠右鍵按一下 [Product] 資料表，然後按一下 [**資料**]。
3. 在 [編輯] 窗格中，輸入下列記錄：

    | **名稱** | **說明** | **高價** |
    | --- | --- | --- |
    | 麵包 | 每天內建全新的。 | 2.99 |
    | 草莓 Shortcake | 以我們的花園的有機 strawberries 進行。 | 9.99 |
    | Apple 圓形圖 | 第二個僅適用于您的 mom 圓形圖。 | 12.99 |
    | Pecan 圓形圖 | 如果您喜歡 pecans，這是為您提供的。 | 10.99 |
    | 檸檬圓形圖 | 以全世界的最佳 lemons 進行。 | 11.99 |
    | 杯子蛋糕 | 您的孩子和小孩將會很愛。 | 7.99 |

    請記住，您不需要針對 [*識別碼*] 資料行輸入任何內容。 當您建立*Id*資料行時，會將其**Is Identity**屬性設定為 true，這會使其自動填入。

    當您完成輸入資料時，[資料表設計工具] 看起來會像這樣：

    ![[影像]](5-working-with-data/_static/image3.jpg)
4. 關閉包含資料庫資料的索引標籤。

## <a name="displaying-data-from-a-database"></a>顯示資料庫中的資料

一旦資料庫中有資料之後，您就可以在 ASP.NET 網頁中顯示資料。 若要選取要顯示的資料表資料列，您可以使用 SQL 語句，這是您傳遞給資料庫的命令。

1. 在左窗格中，按一下 [檔案]**工作區。**
2. 在網站的根目錄中，建立名為*ListProducts*的新 CSHTML 頁面。
3. 以下列內容取代現有的標記：

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    在第一個程式碼區塊中，開啟您稍早建立的*SmallBakery .sdf*檔案（資料庫）。 `Database.Open` 方法假設 *.sdf*檔案位於您網站的*應用程式\_Data*資料夾中。 （請注意，您不需要指定 *.sdf*副檔名&#8212; ，事實上，如果您這樣做，`Open` 方法將無法使用）。

    > [!NOTE]
    > *應用程式\_Data*資料夾是 ASP.NET 中用來儲存資料檔案的特殊資料夾。 如需詳細資訊，請參閱本文稍後的[連接到資料庫](#SB_ConnectingToADatabase)。

    接著，您可以使用下列 SQL `Select` 語句，提出查詢資料庫的要求：

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    在語句中，`Product` 會識別要查詢的資料表。 `*` 字元指定查詢應傳回資料表中的所有資料行。 （如果您只想查看部分資料行，您也可以個別列出資料行，並以逗號分隔。）`Order By` 子句會指出在此情況下，應該&#8212;如何以*名稱*資料行來排序資料。 這表示資料會依照每個資料列的*名稱*資料行的值依字母順序排序。

    在頁面的主體中，標記會建立用來顯示資料的 HTML 資料表。 在 `<tbody>` 元素內，您可以使用 `foreach` 迴圈，個別取得查詢所傳回的每個資料列。 針對每個資料列，您會建立一個 HTML 資料表列（`<tr>` 元素）。 接著，您會為每個資料行建立 HTML 資料表單元格（`<td>` 元素）。 每次執行迴圈時，資料庫中下一個可用的資料列會位於 `row` 變數中（您會在 `foreach` 語句中設定此項）。 若要從資料列取得個別的資料行，您可以使用 `row.Name` 或 `row.Description` 或任何名稱是您想要的資料行。
4. 在瀏覽器中執行頁面。 （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）此頁面會顯示如下所示的清單：

    ![[影像]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **結構化查詢語言 (SQL)**
> 
> SQL 是一種語言，用於大部分關係資料庫中，用來管理資料庫中的資料。 其中包含的命令可讓您抓取資料並加以更新，並可讓您建立、修改和管理資料庫資料表。 SQL 與程式設計語言（例如您在 WebMatrix 中使用的語言）不同，因為在 SQL 中，其概念是告訴資料庫您所需的內容，以及資料庫的工作，以瞭解如何取得資料或執行工作。 以下是一些 SQL 命令的範例，以及它們的作用：
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 這會從*Product*資料表中的記錄提取*識別碼*、*名稱*和*價格*資料行（如果*Price*的值大於10），並根據*名稱*資料行的值，以字母順序傳回結果。 此命令會傳回包含符合準則之記錄的結果集，如果沒有任何記錄符合，則傳回空的集合。
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> 這會在 [ *Product* ] 資料表中插入新的記錄，將 [*名稱*] 資料行設定為 &quot;可頌麵包&quot;、[*描述*] 資料行 &quot;不穩定取悅&quot;，並將 [價格] 設為1.99。
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> 此命令會刪除*產品*資料表中，其到期日資料行早于2008年1月1日的記錄。 （這是假設*Product*資料表有這類資料行）。以 MM/DD/YYYY 格式輸入日期，但應以用於地區設定的格式輸入。
> 
> `Insert Into` 和 `Delete` 命令不會傳回結果集。 相反地，它們會傳回一個數位，告訴您命令有多少記錄受到影響。
> 
> 對於其中某些作業（例如插入和刪除記錄），要求操作的進程必須在資料庫中擁有適當的許可權。 這就是當您連接到資料庫時，生產資料庫經常需要提供使用者名稱和密碼的原因。
> 
> 有數十個 SQL 命令，但它們都遵循類似的模式。 您可以使用 SQL 命令來建立資料庫資料表、計算資料表中的記錄數目、計算價格，以及執行許多其他作業。

## <a name="inserting-data-in-a-database"></a>在資料庫中插入資料

本節說明如何建立可讓使用者將新產品加入至*產品*資料庫資料表的頁面。 插入新的產品記錄後，頁面會使用您在上一節中建立的*ListProducts*頁面來顯示更新的資料表。

此頁面包含驗證，以確保使用者輸入的資料對於資料庫而言是有效的。 例如，頁面中的程式碼會確定已針對所有必要的資料行輸入值。

1. 在網站中，建立名為*InsertProducts*的新 CSHTML 檔案。
2. 以下列內容取代現有的標記：

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    頁面的本文包含一個 HTML 表單，內含三個文字方塊，可讓使用者輸入名稱、描述和價格。 當使用者按一下 [**插入**] 按鈕時，頁面頂端的程式碼會開啟與*SmallBakery*資料庫的連接。 接著，您可以使用 `Request` 物件來取得使用者已提交的值，並將這些值指派給區域變數。

    若要驗證使用者是否為每個必要的資料行輸入值，請註冊您要驗證的每個 `<input>` 元素：

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    `Validation` helper 會檢查您已註冊的每個欄位中是否有一個值。 您可以藉由檢查 `Validation.IsValid()`來測試所有欄位是否通過驗證，這通常會在處理您從使用者取得的資訊之前執行：

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    （`&&` 運算子表示和-這種測試是指*提交表單，而且所有欄位都已通過驗證*）。

    如果所有資料行都已驗證（不是空的），您可以繼續並建立 SQL 語句來插入資料，然後執行它，如下所示：

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    針對要插入的值，您會包含參數預留位置（`@0`、`@1`、`@2`）。

    > [!NOTE]
    > 為了安全起見，請一律使用參數將值傳遞至 SQL 語句，如先前範例所示。 這讓您有機會驗證使用者的資料，並協助防止嘗試將惡意命令傳送至您的資料庫（有時也稱為 SQL 插入式攻擊）。

    若要執行查詢，您可以使用此語句，並將包含值的變數傳遞給它，以替代預留位置：

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    執行 `Insert Into` 語句之後，您可以使用這一行將使用者傳送至列出產品的頁面：

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    如果驗證失敗，您會略過插入。 相反地，您在頁面中有一個協助程式可以顯示累積的錯誤訊息（如果有的話）：

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    請注意，標記中的樣式區塊包含名為 `.validation-summary-errors`的 CSS 類別定義。 這是預設用於包含任何驗證錯誤之 `<div>` 元素的 CSS 類別名稱。 在此情況下，CSS 類別指定驗證摘要錯誤會以紅色和粗體顯示，但您可以定義 `.validation-summary-errors` 類別，以顯示您喜歡的任何格式。

### <a name="testing-the-insert-page"></a>測試插入頁面

1. 在瀏覽器中查看頁面。 頁面會顯示類似下圖所示的表單。

    ![[影像]](5-working-with-data/_static/image5.jpg)
2. 輸入所有資料行的值，但請確定您將 [*價格*] 欄位保留空白。
3. 按一下 [插入]。 此頁面會顯示錯誤訊息，如下圖所示。 （不會建立新的記錄）。

    ![[影像]](5-working-with-data/_static/image6.jpg)
4. 完整填寫表單，然後按一下 [**插入**]。 此時會顯示 [ *ListProducts* ] 頁面，並顯示新的記錄。

## <a name="updating-data-in-a-database"></a>更新資料庫中的資料

在資料表中輸入資料之後，您可能需要加以更新。 此程式示範如何建立兩個頁面，與您先前為數據插入所建立的分頁類似。 第一頁會顯示產品，並讓使用者選取其中一項來變更。 第二頁可讓使用者實際進行編輯並加以儲存。

> [!NOTE] 
> 
> **重要事項**在生產網站中，您通常會限制可對資料進行變更的人員。 如需如何設定成員資格，以及如何授權使用者在網站上執行工作的相關資訊，請參閱[新增 ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。

1. 在網站中，建立名為*EditProducts*的新 CSHTML 檔案。
2. 將檔案中的現有標記取代為下列內容：

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    此頁面與先前的*ListProducts*頁面之間唯一的差異在於，此頁面中的 HTML 資料表包含一個額外的資料行，可顯示 [**編輯**] 連結。 當您按一下此連結時，它會帶您前往 [ *UpdateProducts* ] 頁面（您將在下一步建立），您可以在其中編輯選取的記錄。

    查看建立 [**編輯**] 連結的程式碼：

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    這會建立一個 HTML `<a>` 專案，其 `href` 屬性是以動態方式設定。 `href` 屬性指定使用者按一下連結時要顯示的頁面。 它也會將目前資料列的 `Id` 值傳遞至連結。 當頁面執行時，頁面來源可能會包含如下的連結：

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    請注意，`href` 屬性會設定為 `UpdateProducts/n`，其中*n*是產品編號。 當使用者按一下其中一個連結時，產生的 URL 看起來會像這樣：

    `http://localhost:18816/UpdateProducts/6`

    換句話說，要編輯的產品編號會在 URL 中傳遞。
3. 在瀏覽器中查看頁面。 頁面會顯示如下格式的資料：

    ![[影像]](5-working-with-data/_static/image7.jpg)

    接下來，您將建立可讓使用者實際更新資料的頁面。 [更新] 頁面包含驗證，以驗證使用者輸入的資料。 例如，頁面中的程式碼會確定已針對所有必要的資料行輸入值。
4. 在網站中，建立名為*UpdateProducts*的新 CSHTML 檔案。
5. 將檔案中的現有標記取代為下列檔案。

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    頁面的本文包含一個 HTML 表單，其中會顯示產品以及使用者可以編輯的位置。 若要讓產品顯示，請使用下列 SQL 語句：

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    這會選取識別碼符合在 `@0` 參數中傳遞之值的產品。 （因為*Id*是主要金鑰，因此必須是唯一的，因此只能以這種方式選取一筆產品記錄）。若要取得要傳遞給這個 `Select` 語句的識別碼值，您可以使用下列語法來讀取傳遞至頁面的值做為 URL 的一部分：

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    若要實際提取產品記錄，您可以使用 `QuerySingle` 方法，這只會傳回一筆記錄：

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    單一資料列會傳回 `row` 變數中。 您可以從每個資料行取得資料，並將它指派給本機變數，如下所示：

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    在表單的標記中，這些值會在個別的文字方塊中使用內嵌程式碼自動顯示，如下所示：

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    該部分的程式碼會顯示要更新的產品記錄。 一旦顯示記錄，使用者就可以編輯個別的資料行。

    當使用者按一下 [**更新**] 按鈕來提交表單時，`if(IsPost)` 區塊中的程式碼就會執行。 這會從 `Request` 物件取得使用者的值、將值儲存在變數中，以及驗證每個資料行都已填入。 如果通過驗證，程式碼會建立下列 SQL Update 語句：

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    在 SQL `Update` 語句中，您可以指定要更新的每個資料行，以及要將其設定為的值。 在此程式碼中，會使用參數預留位置來指定值 `@0`、`@1`、`@2`等等。 （如先前所述，為了安全性，您應該一律使用參數將值傳遞至 SQL 語句）。

    當您呼叫 `db.Execute` 方法時，您會以對應至 SQL 語句中參數的順序，傳遞包含值的變數：

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    執行 `Update` 語句之後，您可以呼叫下列方法，以將使用者重新導向回 [編輯] 頁面：

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    其效果是使用者會看到資料庫中資料的更新清單，而且可以編輯另一個產品。
6. 儲存網頁。
7. 執行 [ *EditProducts* ] 頁面（不是 [更新] 頁面），然後按一下 [**編輯**] 以選取要編輯的產品。 [ *UpdateProducts* ] 頁面隨即顯示，並顯示您所選取的記錄。

    ![[影像]](5-working-with-data/_static/image8.jpg)
8. 進行變更，然後按一下 [**更新**]。 [產品] 清單會與更新的資料再次顯示。

## <a name="deleting-data-in-a-database"></a>刪除資料庫中的資料

本節說明如何讓使用者從*product*資料庫資料表中刪除產品。 此範例包含兩個頁面。 在第一頁中，使用者選取要刪除的記錄。 接著會在第二頁顯示要刪除的記錄，讓他們確認是否要刪除記錄。

> [!NOTE] 
> 
> **重要事項**在生產網站中，您通常會限制可對資料進行變更的人員。 如需如何設定成員資格，以及如何授權使用者在網站上執行工作的相關資訊，請參閱[新增 ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。

1. 在網站中，建立名為*ListProductsForDelete*的新 CSHTML 檔案。
2. 以下列內容取代現有的標記：

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    此頁面與稍早的*EditProducts*頁面類似。 不過，它不會顯示每個產品的 [**編輯**] 連結，而是顯示 [**刪除**] 連結。 [**刪除**] 連結是在標記中使用下列內嵌程式碼所建立：

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    這會在使用者按一下連結時，建立如下所示的 URL：

    `http://<server>/DeleteProduct/4`

    URL 會呼叫名為*DeleteProduct*的頁面（您將在下一步建立），並將它的識別碼傳遞給它，以供刪除（此處為4）。
3. 儲存檔案，但讓它保持開啟。
4. 建立另一個名為*DeleteProduct*的 CHTML 檔案。 以下列內容取代現有的內容：

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    此頁面是由*ListProductsForDelete*所呼叫，可讓使用者確認他們想要刪除產品。 若要列出要刪除的產品，您可以使用下列程式碼，取得要從 URL 刪除的產品識別碼：

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    該頁面接著會要求使用者按一下按鈕，以實際刪除該記錄。 這是一項重要的安全性措施：當您在網站中執行敏感性作業（例如更新或刪除資料）時，應該一律使用 POST 作業來完成這些作業，而不是取得操作。 如果您的網站已設定為可使用「取得」作業來執行「刪除」作業，任何人都可以傳遞類似 `http://<server>/DeleteProduct/4` 的 URL，並從您的資料庫中刪除他們想要的任何專案。 藉由新增確認並撰寫頁面的程式碼，以便只能使用文章來執行刪除作業，您可以將安全性量值新增至您的網站。

    實際的刪除作業會使用下列程式碼來執行，這會先確認這是 post 作業，而且識別碼不是空的：

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    程式碼會執行 SQL 語句，以刪除指定的記錄，然後將使用者重新導向回清單頁面。
5. 在瀏覽器中執行*ListProductsForDelete。*

    ![[影像]](5-working-with-data/_static/image9.jpg)
6. 按一下其中一項產品的 [**刪除**] 連結。 [ *DeleteProduct* ] 頁面隨即顯示，以確認您想要刪除該記錄。
7. 按一下 [刪除] 按鈕。 會刪除產品記錄，並使用更新的產品清單來重新整理此頁面。

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>連接到資料庫
> 
> 您可以透過兩種方式連接到資料庫。 第一種是使用 `Database.Open` 方法，並指定資料庫檔案的名稱（較不是 *.sdf*副檔名）：
> 
> `var db = Database.Open("SmallBakery");`
> 
> `Open` 方法會假設。 *.sdf*檔案位於網站的*應用程式\_Data*資料夾中。 此資料夾是特別為保存資料所設計。 例如，它具有適當的許可權可允許網站讀取及寫入資料，而作為安全性措施，WebMatrix 不允許從這個資料夾存取檔案。
> 
> 第二種方式是使用連接字串。 連線字串包含如何連線到資料庫的相關資訊。 這可以包含檔案路徑，也可以包含本機或遠端伺服器上 SQL Server 資料庫的名稱，以及用來連接到該伺服器的使用者名稱和密碼。 （如果您將資料保留在集中管理的 SQL Server 版本中，例如在主控提供者的網站上，則一律使用連接字串來指定資料庫連接資訊）。
> 
> 在 WebMatrix 中，連接字串通常會儲存在名為*web.config*的 XML 檔案中。正如其名，您可以在網站的根目錄中*使用 web.config 檔案*來儲存網站的設定資訊，包括您的網站可能需要的任何連接字串。 *Web.config 檔案*中的連接字串範例可能如下所示：
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> 在此範例中，連接字串會指向在伺服器上執行的 SQL Server 實例中的資料庫（相對於本機 *.sdf*檔案）。 您必須以適當的名稱取代 `myServer` 和 `myDatabase`，並指定 `username` 和 `password`的 SQL Server 登入值。 （使用者名稱和密碼值不一定與您的 Windows 認證相同，或者是您的主機服務提供者提供給您登入其伺服器的值。 請洽詢系統管理員以取得您所需的確切值）。
> 
> `Database.Open` 方法很有彈性，因為它可讓您傳遞資料庫 *.sdf*檔案的名稱或儲存在*web.config*檔案中的連接字串名稱。 下列範例顯示如何使用上述範例中所述的連接字串來連接到資料庫：
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> 如前所述，`Database.Open` 方法可讓您傳遞資料庫名稱或連接字串，並找出要使用的資料。 當您部署（發佈）您的網站時，這非常有用。 當您在開發和測試網站時，您可以在應用程式中使用 *.sdf*檔案 *\_Data*資料夾。 然後，當您將網站移至實際執行伺服器時，您可以*在 web.config 檔案*中使用與 *.sdf*檔案同名的連接字串，但這會指向主控提供者的資料庫&#8212; ，而不需要變更您的程式碼。
> 
> 最後，如果您想要直接使用連接字串，您可以呼叫 `Database.OpenConnectionString` 方法，並將實際*的*連接字串傳遞給它，而不只是 web.config 檔案中的名稱。 這在某些情況下很有用，因為您無法存取連接字串（或其中的值，例如 *.sdf*檔案名），直到頁面執行為止。 不過，在大部分的情況下，您可以使用本文中所述的 `Database.Open`。

## <a name="additional-resources"></a>其他資源

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [連接到 WebMatrix 中的 SQL Server 或 MySQL 資料庫](https://go.microsoft.com/fwlink/?LinkId=208661)
- [在 ASP.NET Web Pages 網站中驗證使用者輸入](https://go.microsoft.com/fwlink/?LinkId=253002)
