---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: ASP.NET Web Pages 簡介-顯示資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程說明如何在 WebMatrix 中建立資料庫，以及當您使用 ASP.NET Web Pages （Razor）時，如何在頁面中顯示資料庫資料。 它假設 y 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525218"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a>簡介 ASP.NET Web Pages-顯示資料

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程說明如何在 WebMatrix 中建立資料庫，以及當您使用 ASP.NET Web Pages （Razor）時，如何在頁面中顯示資料庫資料。 它假設您已完成[ASP.NET Web Pages 程式設計簡介](../introducing-razor-syntax-c.md)的系列。
> 
> 您將學到什麼：
> 
> - 如何使用 WebMatrix 工具來建立資料庫和資料庫資料表。
> - 如何使用 WebMatrix 工具將資料新增至資料庫。
> - 如何在頁面上顯示資料庫中的資料。
> - 如何在 ASP.NET Web Pages 中執行 SQL 命令。
> - 如何自訂 `WebGrid` helper 來變更資料顯示，以及新增分頁和排序。
>   
> 
> 討論的功能/技術：
> 
> - WebMatrix 資料庫工具。
> - `WebGrid` helper。

## <a name="what-youll-build"></a>您要建置的內容

在上一個教學課程中，您已介紹 ASP.NET Web Pages （*cshtml*檔案）、Razor 語法的基本概念，以及協助程式。 在本教學課程中，您將開始建立將用於該系列其餘部分的實際 web 應用程式。 應用程式是簡單的電影應用程式，可讓您查看、新增、變更及刪除電影的相關資訊。

當您完成本教學課程時，您將能夠看到看起來像此頁面的電影清單：

![WebGrid 顯示，其中包含設定為 CSS 類別名稱的參數](displaying-data/_static/image1.png)

但若要開始，您必須建立資料庫。

## <a name="a-very-brief-introduction-to-databases"></a>資料庫的簡要簡介

本教學課程只會提供資料庫的 briefest 簡介。 如果您有資料庫經驗，可以略過這個簡短的小節。

資料庫包含一個或多個資料表，其中包含 &mdash; 的資訊，例如客戶、訂單和廠商的資料表，或是學生、老師、班級和成績。 就結構而言，資料庫資料表就像是試算表。 想像一下一般通訊錄。 針對通訊錄中的每個專案（亦即，針對每個人），您會有數個資訊片段，例如名字、姓氏、位址、電子郵件地址和電話號碼。

![當做簡單方格的範例資料庫資料表](displaying-data/_static/image2.png)

（資料列有時稱為「*記錄*」，而資料行有時稱為「*欄位*」）。

對於大部分的資料庫資料表而言，資料表必須有一個包含唯一值的資料行，例如客戶編碼、帳戶號碼等等。 這個值稱為資料表的*主鍵*，您可以用它來識別資料表中的每個資料列。 在此範例中，ID 資料行是上一個範例中所顯示通訊錄的主要金鑰。

您在 web 應用程式中所做的大部分工作，都包含從資料庫讀取資訊，並將它顯示在頁面上。 您也經常會收集使用者的資訊，並將其新增至資料庫，或是修改已在資料庫中的記錄。 （我們將在本教學課程設定的過程中涵蓋所有這些作業）。

資料庫工作的大幅很複雜，而且可能需要專門知識。 不過，在本教學課程中，您必須只瞭解基本概念，這一切都將在您走時說明。

## <a name="creating-a-database"></a>建立資料庫

WebMatrix 所包含的工具可讓您輕鬆地建立資料庫，並在資料庫中建立資料表。 （資料庫的結構稱為資料庫的*架構*）。在此教學課程中，您將建立一個資料庫，其中只有一個資料表 &mdash; 電影。

開啟 WebMatrix （如果您尚未這麼做），並開啟您在上一個教學課程中建立的 WebPagesMovies 網站。

在左窗格中，按一下 [**資料庫**] 工作區。

![WebMatrix 資料庫工作區索引標籤](displaying-data/_static/image3.png)

功能區會變更以顯示資料庫相關工作。 在功能區中，按一下 [**新增資料庫**]。

![WebMatrix 功能區中的 [新增資料庫] 按鈕](displaying-data/_static/image4.png)

WebMatrix 會建立與您的網站 &mdash; *WebPagesMovies*同名的 SQL Server CE 資料庫（ *.sdf*檔案）。 （您不會在這裡執行此動作，但您可以將檔案重新命名為任何您喜歡的專案，只要它的副檔名為 *.sdf*即可）。

## <a name="creating-a-table"></a>建立資料表

在功能區中，按一下 [**新增資料表**]。 WebMatrix 會在新的索引標籤中開啟 [資料表設計工具] （如果無法使用 [新增資料表] 選項，請確定已在左側樹狀檢視中選取新的資料庫）。

![WebMatrix 功能區中的 [新增資料表] 按鈕](displaying-data/_static/image5.png)

在頂端的文字方塊中（浮水印會顯示為「輸入資料表名稱」），輸入「電影」。

![在 WebMatrix 資料庫設計工具中輸入資料表名稱](displaying-data/_static/image6.png)

資料表名稱底下的窗格是您定義個別資料行的位置。 針對本教學課程中的*電影*資料表，您只會建立幾個資料行： *ID*、 *Title* *、內容*類型和*年份*。

在 [**名稱**] 方塊中，輸入 "ID"。 在此輸入值會啟用新資料行的所有控制項。

索引標籤至 [**資料類型**] 清單，然後選擇 [ **int**]。這個值會指定 ID 資料行將包含整數（數位）資料。

> [!NOTE]
> 我們不會在此呼叫它（很多），但您可以使用標準 Windows 鍵盤手勢在此方格中進行流覽。 例如，您可以在欄位之間定位，只要開始輸入，就可以選取清單中的專案，依此類推。

索引標籤超過**預設值**方塊（也就是將它保留空白）。 選擇 [**是主要金鑰**] 核取方塊，然後選取它。 此選項會告訴資料庫，[*識別碼*] 資料行會包含可識別個別資料列的資料。 （也就是說，每個資料列在 [識別碼] 資料行中都有唯一的值，您可以用來尋找該資料列）。

選擇 [**是身分識別**] 選項。 此選項會告訴資料庫，它應該會自動為每個新的資料列產生下一個連續數位。 （[**是身分識別**] 選項只有在您也選取了 [**是主要索引鍵**] 選項時才適用）。

按一下下一個格線列，或按兩次 Tab 鍵，完成目前的資料列。 任一手勢會儲存目前的資料列，並啟動下一個資料列。 請注意，[**預設值**] 資料行現在會顯示**Null**。 （Null 是預設值的預設值，因此要說出）。

當您完成定義新的**ID**資料行時，設計工具看起來會像這樣：

![定義電影資料表的 ID 資料行之後的 WebMatrix 資料庫設計工具](displaying-data/_static/image7.png)

若要建立下一個資料行，請按一下 [**名稱**] 資料行中的方塊。 輸入資料行的「標題」，然後選取 [ **Nvarchar** ] 做為**資料類型**值。 **NVarchar**的 "var" 部分會告訴資料庫，此資料行的資料將是字串，其大小可能會因記錄而異。 （"N" 前置詞代表「國家」，表示欄位可以保存任何字母或書寫系統的字元資料，也就是欄位保留 Unicode 資料）。

當您選擇 [ **Nvarchar**] 時，會出現另一個方塊，您可以在其中輸入欄位的最大長度。 輸入50，假設您在本教學課程中使用的電影標題不會超過50個字元。

略過**預設值**，並清除 [**允許 null]** 選項。 您不希望資料庫允許將任何電影輸入至沒有標題的資料庫中。

當您完成並移至下一個資料列時，設計工具會如下圖所示：

![定義電影資料表的標題資料行之後的 WebMatrix 資料庫設計工具](displaying-data/_static/image8.png)

重複這些步驟來建立名為「內容類型」的資料行，但長度除外，請將它設定為只30。

建立另一個名為 "Year" 的資料行。 針對 [資料類型]，選擇 [ **Nchar** （非**Nvarchar**）]，並將長度設定為4。 在年份中，您會使用4位數的數位，例如 "1995" 或 "2010"，因此您不需要可變大小的資料行。

完成的設計如下所示：

![針對電影資料表定義所有欄位後的 WebMatrix 資料庫設計工具](displaying-data/_static/image9.png)

按 Ctrl + S，或按一下快速存取工具列中的 [**儲存**] 按鈕。 關閉 [資料庫設計工具]，方法是關閉索引標籤。

## <a name="adding-some-example-data"></a>新增一些範例資料

稍後在本教學課程系列中，您將建立一個頁面，您可以在表單中輸入新電影。 不過，現在您可以新增一些範例資料，讓您可以在頁面上顯示。

在 WebMatrix 的 [**資料庫**] 工作區中，您會看到一個樹狀結構，其中會顯示您稍早建立的 *.sdf*檔案。 開啟新的 *.sdf*檔案的節點，然後開啟 [**資料表]** 節點。

![將樹狀結構開啟至電影資料表的 WebMatrix 資料庫工作區](displaying-data/_static/image10.png)

以滑鼠右鍵按一下 [**電影**] 節點，然後選擇 [**資料**]。 WebMatrix 會開啟一個格線，您可以在其中輸入*電影*資料表的資料：

![WebMatrix 中的資料庫專案方格（空白）](displaying-data/_static/image11.png)

按一下 [**標題**] 資料行，並輸入 "When Harry 符合 Sally"。 移至 [類型]**資料行（** 您可以使用 Tab 鍵），然後輸入 "Romantic 喜劇"。 移至 [**年**] 資料行，然後輸入 "1989"：

![具有一筆記錄的 WebMatrix 中的資料庫輸入方格](displaying-data/_static/image12.png)

按 Enter 鍵，WebMatrix 會儲存新電影。 請注意，[**識別碼**] 資料行已填入。

![WebMatrix 中的資料庫輸入方格，其中包含一筆記錄和自動產生的識別碼](displaying-data/_static/image13.png)

輸入另一部電影（例如，"戲劇"、"1939"）。 [識別碼] 資料行會再次填入：

![WebMatrix 中的資料庫專案方格，其中包含兩個記錄和自動產生的識別碼](displaying-data/_static/image14.png)

輸入第三個電影（例如，"Ghostbusters"、"喜劇"）。 以實驗的方式，將 [**年份**] 資料行保留空白，然後按 enter。 因為您已取消選取 [**允許 Null]** 選項，所以資料庫會顯示錯誤：

![如果必要的資料行值保留空白，則會顯示「不正確資料」錯誤](displaying-data/_static/image15.png)

按一下 **[確定]** 返回並修正專案（"Ghostbusters" 的年份是1984），然後按 enter。

填入數個電影，直到您有8個以上的影片為止。 （輸入8可讓您更輕鬆地在稍後使用分頁。 但如果太多，現在只需輸入幾個。）實際的資料並不重要。

![具有任一筆記錄的 WebMatrix 中的資料庫輸入方格](displaying-data/_static/image16.png)

如果您輸入所有電影而沒有任何錯誤，則識別碼值為連續。 如果您嘗試儲存未完成的電影記錄，識別碼編號可能不是連續的。 如果是這樣，沒關係。 這些數位沒有任何固有的意義，而且唯一重要的是，它們在*電影*資料表中是唯一的。

關閉包含 [資料庫設計工具] 的索引標籤。

現在您可以將此資料顯示在網頁上。

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a>使用 WebGrid Helper 在頁面中顯示資料

若要在頁面中顯示資料，您將使用 `WebGrid` helper。 此 helper 會在方格或資料表（資料列和資料行）中產生顯示。 如您所見，您可以使用格式設定和其他功能來縮小方格的範圍。

若要執行方格，您必須撰寫幾行程式碼。 這幾行會做為您在本教學課程中所做的幾乎所有資料存取的一種模式。

> [!NOTE]
> 您實際上有許多選項可以在頁面上顯示資料;`WebGrid` helper 只是一個。 我們在本教學課程中選擇它，是因為它是顯示資料的最簡單方式，而且是合理的彈性。 在下一個教學課程中，您將瞭解如何使用更「手動」方式來處理頁面中的資料，讓您更直接控制如何顯示資料。

在 WebMatrix 的左窗格中，按一下 [檔案]**工作區。**

您所建立的新資料庫會在*應用程式\_Data*資料夾中。 如果資料夾尚未存在，則 WebMatrix 會為您的新資料庫建立該資料夾。 （如果您先前已安裝 helper，此資料夾可能已經存在）。

在樹狀檢視中，選取網站的根目錄。 您必須選取網站的根目錄;否則，新的檔案可能會新增至應用程式\_Data 資料夾中。

在功能區中，按一下 [**新增**]。 在 [**選擇檔案類型**] 方塊中，選擇 [ **CSHTML**]。

在 [**名稱**] 方塊中，將新頁面命名為「電影. cshtml」：

![顯示 [電影] 頁面的 [選擇檔案類型] 對話方塊](displaying-data/_static/image17.png)

按一下 [確定] 按鈕。 WebMatrix 會開啟新檔案，其中包含一些基本架構元素。 首先，您要撰寫一些程式碼，從資料庫取得資料。 接著，您會將標記新增至頁面，以實際顯示資料。

### <a name="writing-the-data-query-code"></a>撰寫資料查詢程式碼

在頁面頂端的 [`@{`] 和 [`}`] 字元之間，輸入下列程式碼。 （請確定您在開頭和右大括弧之間輸入此程式碼）。

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

第一行會開啟您稍早建立的資料庫，這一律是在資料庫中執行某些動作之前的第一個步驟。 您會告訴資料庫的 `Database.Open` 方法名稱已開啟。 請注意，您不會在名稱中包含 *.sdf。* `Open` 方法假設它正在尋找 *.sdf*檔案（也就是*WebPagesMovies .sdf*），而且 *.sdf*檔案位於*應用程式\_Data*資料夾中。 （稍早我們說過，*應用程式\_Data*資料夾是保留的，此案例是 ASP.NET 對該名稱進行假設的其中一個地方）。

當資料庫開啟時，它的參考會放入名為 `db`的變數中。 （可以命名為任何專案）。`db` 變數是您最後與資料庫互動的方式。

第二行會使用 `Query` 方法，實際提取資料庫資料。 請注意此程式碼的運作方式： `db` 變數具有已開啟資料庫的參考，而且您會使用 `db` 變數（`db.Query`）來叫用 `Query` 方法。

查詢本身是 SQL `Select` 語句。 （如需有關 SQL 的背景資訊，請參閱稍後的說明）。在語句中，`Movies` 會識別要查詢的資料表。 `*` 字元指定查詢應傳回資料表中的所有資料行。 （您也可以個別列出資料行，並以逗號分隔）。

傳回查詢的結果（如果有的話），並可在 `selectedData` 變數中取得。 同樣地，變數可以命名為任何專案。

最後，第三行會告訴 ASP.NET 您想要使用 `WebGrid` helper 的實例。 您可以使用 `new` 關鍵字來建立（具現*化*） helper 物件，並透過 `selectedData` 變數將查詢結果傳遞給它。 新的 `WebGrid` 物件以及資料庫查詢的結果，可在 `grid` 變數中取得。 您需要這樣的結果，才能實際顯示頁面中的資料。

在這個階段，資料庫已開啟，您已取得您想要的資料，而且您已準備好該資料的 `WebGrid` helper。 接下來是在頁面中建立標記。

> [!TIP] 
> 
> **結構化查詢語言 (SQL)**
> 
> SQL 是一種語言，用於大部分關係資料庫中，用來管理資料庫中的資料。 其中包含的命令可讓您抓取資料並加以更新，並可讓您建立、修改和管理資料庫資料表中的資料。 SQL 不同于程式設計語言（例如C#）。 在 SQL 中，您會告訴資料庫您所需的內容，而這就是資料庫的工作，以找出如何取得資料或執行工作。 以下是一些 SQL 命令的範例，以及它們的作用：
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 第一個 `Select` 語句會從*電影*資料表取得所有資料行（由 `*`指定）。
> 
> 第二個 `Select` 語句會從*Product*資料表中的記錄，提取 price 資料行值大於10的識別碼、名稱和價格資料行。 此命令會根據名稱資料行的值，以字母順序傳回結果。 如果沒有任何記錄符合價格條件，此命令會傳回空的集合。
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> 此命令會將新記錄插入*Product*資料表，並將 Name 資料行設定為 "可頌麵包"、Description 資料行設為 "a 不穩定取悅"，並將價格設為1.99。
> 
> 請注意，當您指定非數值時，此值會以單引號括住（不是雙引號，如所示C#）。 您可以在文字或日期值前後加上引號，但不能用在數位的周圍。
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> 此命令會刪除*產品*資料表中，其到期日資料行早于2008年1月1日的記錄。 （此命令假設*產品*資料表具有這類資料行）。以 MM/DD/YYYY 格式輸入日期，但應以用於地區設定的格式輸入。
> 
> `Insert` 和 `Delete` 命令不會傳回結果集。 相反地，它們會傳回一個數位，告訴您命令有多少記錄受到影響。
> 
> 對於其中某些作業（例如插入和刪除記錄），要求操作的進程必須在資料庫中擁有適當的許可權。 這就是為什麼生產資料庫在您連接到資料庫時，通常必須提供使用者名稱和密碼的原因。
> 
> 有數十個 SQL 命令，但它們都遵循如下所示的模式。 您可以使用 SQL 命令來建立資料庫資料表、計算資料表中的記錄數目、計算價格，以及執行許多其他作業。

### <a name="adding-markup-to-display-the-data"></a>加入標記以顯示資料

在 `<head>` 元素內，將 `<title>` 元素的內容設定為「電影」：

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

在頁面的 `<body>` 元素內，新增下列專案：

[!code-html[Main](displaying-data/samples/sample3.html)]

就這麼容易！ `grid` 變數是您稍早在程式碼中建立 `WebGrid` 物件時所建立的值。

在 WebMatrix 樹狀檢視中，以滑鼠右鍵按一下頁面，然後選取 [**在瀏覽器中啟動**]。 您會看到類似此頁面的內容：

![電影資料表的預設 WebGrid helper 輸出](displaying-data/_static/image18.png)

按一下資料行標題連結，依該資料行排序。 按一下標題就能夠排序，這是內建在**WebGrid** helper 中的功能。

`GetHtml` 方法，如其名所示，會產生可顯示資料的標記。 根據預設，`GetHtml` 方法會產生 HTML `<table>` 元素。 （如果您想要的話，可以在瀏覽器中查看頁面的來源來驗證轉譯）。

## <a name="modifying-the-look-of-the-grid"></a>修改方格的外觀

像您一樣使用 `WebGrid` 協助程式很簡單，但所產生的顯示是純文字。 [`WebGrid` helper] 具有各種選項，可讓您控制資料的顯示方式。 本教學課程中有太多要探索的內容，但本節將為您介紹其中一些選項。 本系列稍後的教學課程將涵蓋一些其他選項。

### <a name="specifying-individual-columns-to-display"></a>指定要顯示的個別資料行

若要開始，您可以指定只顯示特定資料行。 根據預設，如您所見，方格會顯示 [*電影*] 資料表中的四個數據行。

在 [*電影*] 檔案中，將您剛才新增的 `@grid.GetHtml()` 標記取代為下列內容：

[!code-css[Main](displaying-data/samples/sample4.css)]

若要告知 helper 要顯示哪些資料行，您可以加入 `GetHtml` 方法的 `columns` 參數，並傳入資料行集合。 在集合中，您可以指定要包含的每個資料行。 您可以藉由包含 `grid.Column` 物件來指定要顯示的個別資料行，並傳入您想要的資料行名稱。 （這些資料行必須包含在 SQL 查詢結果中，`WebGrid` helper 無法顯示查詢未傳回的資料行）。

再次啟動瀏覽器中的 [ *cshtml* ] 頁面，這次您會看到如下所示的畫面（請注意，不會顯示任何 ID 資料行）：

![WebGrid 顯示只顯示選取的資料行](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a>變更方格的外觀

另外還有幾個選項可用來顯示資料行，其中有一些會在本集合稍後的教學課程中探索。 目前，本節將為您介紹可將方格的樣式設為整體的方式。

在頁面的 `<head>` 區段中，在結尾 `</head>` 標記之前，新增下列 `<style>` 元素：

[!code-css[Main](displaying-data/samples/sample5.css)]

這個 CSS 標記會定義名為 `grid`、`head`等等的類別。 您也可以將這些樣式定義放在個別的 *.css*檔案中，並將其連結至頁面。 （事實上，您稍後會在本教學課程中設定）。但為了方便您進行本教學課程，這些專案會在顯示資料的相同頁面中。

現在您可以取得 `WebGrid` helper 以使用這些樣式類別。 Helper 只有這種用途的屬性（例如 `tableStyle`），您可以將 CSS 樣式類別名稱指派給它們，而該類別名稱會轉譯成由協助程式轉譯的標記之一部分。

變更 `grid.GetHtml` 標記，使其看起來像下面這段程式碼：

[!code-css[Main](displaying-data/samples/sample6.css)]

這裡的新功能是您已將 `tableStyle`、`headerStyle`和 `alternatingRowStyle` 參數新增至 `GetHtml` 方法。 這些參數已設定為您稍早新增的 CSS 樣式名稱。

執行頁面，這次您會看到看起來比以前更簡單的方格：

![WebGrid 顯示，其中包含設定為 CSS 類別名稱的參數](displaying-data/_static/image20.png)

若要查看 `GetHtml` 方法產生的內容，您可以在瀏覽器中查看頁面的來源。 這裡不會詳細說明，但重點是，藉由指定 `tableStyle`之類的參數，您就會使方格產生如下所示的 HTML 標籤：

`<table class="grid">`

`<table>` 標記已加入 `class` 屬性，它會參考您稍早新增的其中一個 CSS 規則。 這段程式碼會顯示基本模式 &mdash; `GetHtml` 方法的不同參數，讓您參考該方法接著會連同標記一起產生的 CSS 類別。 您對 CSS 類別的作用是由您決定。

## <a name="adding-paging"></a>加入分頁

做為本教學課程的最後一項工作，您會將分頁加入至方格。 現在就不會發生任何問題，同時顯示所有電影。 但是，如果您新增了數百個電影，頁面顯示會變長。

在頁面程式碼中，將建立 `WebGrid` 物件的那一行變更為下列程式碼：

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

與之前的唯一差異在於，您已加入設定為3的 `rowsPerPage` 參數。

執行頁面。 方格一次會顯示3個數據列，再加上導覽連結，讓您逐頁流覽資料庫中的電影：

![WebGrid 顯示與分頁](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a>下一步

在下一個教學課程中，您將瞭解如何使用 Razor C#和程式碼來取得表單中的使用者輸入。 您會在 [電影] 頁面中新增搜尋方塊，讓您可以依標題或內容類型來尋找電影。

## <a name="complete-listing-for-movies-page"></a>電影的完整清單頁面

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> [上一頁](intro-to-web-pages-programming.md)
> [下一頁](form-basics.md)
