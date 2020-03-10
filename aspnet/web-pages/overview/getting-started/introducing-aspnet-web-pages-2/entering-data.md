---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: 簡介 ASP.NET Web Pages 使用表單輸入資料庫資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程會示範如何建立輸入表單，然後在使用 ASP.NET Web Pages （...）時，將您從表單取得的資料輸入至資料庫資料表。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624534"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>簡介 ASP.NET Web Pages 使用表單輸入資料庫資料

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程會示範如何建立輸入表單，然後在使用 ASP.NET Web Pages （Razor）時，將您從表單中取得的資料輸入至資料庫資料表。 它假設您已[在 ASP.NET Web Pages 中，透過 HTML 表單的基本概念](https://go.microsoft.com/fwlink/?LinkId=251581)來完成數列。
> 
> 您將學到什麼：
> 
> - 深入瞭解如何處理輸入表單。
> - 如何在資料庫中加入（插入）資料。
> - 如何確保使用者在表單中輸入了必要的值（如何驗證使用者輸入）。
> - 如何顯示驗證錯誤。
> - 如何從目前的頁面跳到另一個頁面。
>   
> 
> 討論的功能/技術：
> 
> - `Database.Execute` 方法
> - SQL `Insert Into` 語句
> - `Validation` helper。
> - `Response.Redirect` 方法

## <a name="what-youll-build"></a>您要建置的內容

在先前示範如何建立資料庫的教學課程中，您可以直接在 WebMatrix 中編輯資料庫來輸入資料庫資料，請在 [**資料庫**] 工作區中工作。 不過在大部分的應用程式中，這不是將資料放入資料庫的實用方式。 因此，在本教學課程中，您將建立 web 型介面，讓您或任何人輸入資料並將其儲存至資料庫。

您將建立可在其中輸入新電影的頁面。 此頁面會包含一個輸入表單，其中具有欄位（文字方塊），您可以在其中輸入電影標題、內容類型和年份。 頁面看起來會像這個頁面：

![瀏覽器中的 [新增電影] 頁面](entering-data/_static/image1.png)

文字方塊會是 HTML `<input>` 專案，看起來就像此標記：

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>建立基本輸入表單

建立名為*AddMovie*的頁面。

以下列標記取代檔案中的內容。 全部覆寫;您很快就會在頂端新增程式碼區塊。

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

這個範例會顯示建立表單的一般 HTML。 它會針對文字方塊和 [提交] 按鈕使用 `<input>` 元素。 文字方塊的標題是使用標準 `<label>` 元素所建立。 `<fieldset>` 和 `<legend>` 元素會在表單周圍放置一個不錯的方塊。

請注意，在此頁面中，`<form>` 元素會使用 `post` 做為 `method` 屬性的值。 在上一個教學課程中，您已建立一個使用 `get` 方法的表單。 這是正確的，因為雖然表單已提交值給伺服器，但要求並未進行任何變更。 這一切都是以不同的方式提取資料。 不過，在此頁面中，您*將會*進行變更，也就是加入新的資料庫記錄。 因此，此表單應該使用 `post` 方法。 （如需 `GET` 和 `POST` 作業之間差異的詳細資訊，請參閱上一個教學課程中的[GET、POST 和 HTTP Verb 安全](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety)提要欄位）。

請注意，每個文字方塊都有一個 `name` 元素（`title`、`genre``year`）。 如您在上一個教學課程中所見，這些名稱很重要，因為您必須擁有這些名稱，才能在稍後取得使用者的輸入。 您可以使用任何名稱。 使用有意義的名稱有助於記住您所使用的資料，是很有説明的。

每個 `<input>` 元素的 `value` 屬性包含一些 Razor 程式碼（例如，`Request.Form["title"]`）。 您已在上一個教學課程中瞭解此技巧的某個版本，以在提交表單後保留在文字方塊中輸入的值（如果有的話）。

## <a name="getting-the-form-values"></a>取得表單值

接下來，您可以加入處理表單的程式碼。 在大綱中，您會執行下列動作：

1. 檢查頁面是否正在張貼（已提交）。 您只想要讓程式碼在使用者按下按鈕時執行，而不是在頁面第一次執行時執行。
2. 取得使用者在文字方塊中輸入的值。 在此情況下，因為表單使用 `POST` 動詞，所以您會從 `Request.Form` 集合取得表單值。
3. 將這些值插入*電影*資料庫資料表中的新記錄。

在檔案的頂端，新增下列程式碼：

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

前幾行會建立變數（`title`、`genre`和 `year`），以保存文字方塊中的值。 這一行 `if(IsPost)` 確保只有在使用者按一下 [**新增電影**] 按鈕時，也就是在張貼表單時，*才*會設定變數。

如您在先前的教學課程中所見，您可以使用運算式（例如 `Request.Form["name"]`）來取得文字方塊的值，其中*name*是 `<input>` 元素的名稱。

變數的名稱（`title`、`genre`和 `year`）是任意的。 就像您指派給 `<input>` 元素的名稱一樣，您可以隨意呼叫它們。 （變數的名稱不一定要與表單上 `<input>` 元素的名稱屬性相符）。但是如同 `<input>` 的元素，使用變數名稱來反映它們所包含的資料，是個不錯的主意。 當您撰寫程式碼時，一致的名稱可讓您更輕鬆地記住您所使用的資料。

## <a name="adding-data-to-the-database"></a>將資料新增至資料庫

在您剛才加入的程式碼區塊中，只在 `if` 區塊的右大括弧（`}`）*內*（而不是在程式碼區塊內），新增下列程式碼：

[!code-csharp[Main](entering-data/samples/sample3.cs)]

這個範例類似于您在上一個教學課程中用來提取和顯示資料的程式碼。 以 `db =` 開頭的那一行會開啟資料庫（如先前的程式碼），而下一行會定義 SQL 語句，如同您之前所看到的一樣。 不過，這次它會定義 SQL `Insert Into` 語句。 下列範例顯示 `Insert Into` 語句的一般語法：

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

換句話說，您可以指定要插入的資料表，然後列出要插入的資料行，再列出要插入的值。 （如前所述，SQL 並不區分大小寫，但有些人會將關鍵字變成大寫，讓您更輕鬆地讀取命令）。

您要插入的資料行已列在命令中，`(Title, Genre, Year)`。 有趣的部分是如何從文字方塊中取得值到命令的 `VALUES` 部分。 您看不到實際的值，而是看到 `@0`、`@1`和 `@2`，這是課程預留位置。 當您執行命令時（在 `db.Execute` 行），會傳遞您從文字方塊中所獲得的值。

**重要！** 請記住，您應該在 SQL 語句中包含使用者在線上輸入的資料的唯一方式，就是使用預留位置，如這裡所見（`VALUES(@0, @1, @2)`）。 如果您將使用者輸入串連到 SQL 語句中，您會將自己開啟至 SQL 插入式攻擊，如[ASP.NET Web Pages 的表單基本概念](https://go.microsoft.com/fwlink/?LinkId=251581)（上一個教學課程）中所述。

仍然在 `if` 區塊內，在 `db.Execute` 行後面新增下列程式程式碼：

[!code-css[Main](entering-data/samples/sample4.css)]

將新電影插入資料庫之後，這行程式碼會將您（重新導向）至*電影*頁面，讓您可以看到剛才輸入的電影。 `~` 運算子表示「網站的根目錄」。 （`~` 運算子僅適用于 ASP.NET 網頁，而非 HTML 一般）。

完整的程式碼區塊如下列範例所示：

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>測試插入命令（到目前為止）

您還沒這麼做，但現在是測試的好時機。

在 WebMatrix 中檔案的樹狀檢視中，以滑鼠右鍵按一下 [ *AddMovie* ] 頁面，然後按一下 [**在瀏覽器中啟動**]。

![瀏覽器中的 [新增電影] 頁面](entering-data/_static/image2.png)

（如果您最終會在瀏覽器中使用不同的頁面，請確定 URL 是 `http://localhost:nnnnn/AddMovie`），其中*nnnnn*是您所使用的埠號碼）。

您是否收到錯誤頁面？ 若是如此，請仔細閱讀，並確定程式碼看起來完全符合先前所列的內容。

以 &mdash; 的形式輸入電影，例如，使用 "公民 Kane"、"戲劇" 和 "1941"。 （或任何）。然後按一下 [**新增電影**]。

如果一切順利，您會被重新導向至 [*電影*] 頁面。 請確定您的新電影已列出。

![顯示新增電影的電影頁面](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>驗證使用者輸入

返回 [ *AddMovie* ] 頁面，或重新執行。 輸入另一個電影，但這次請輸入 &mdash; 的標題，例如，輸入 "Singin' in the Rain"。 然後按一下 [**新增電影**]。

您會重新導向至 [*電影*] 頁面。 您可以找到新電影，但它不完整。

![顯示遺漏一些值的新電影的電影頁面](entering-data/_static/image4.png)

當您建立*電影*資料表時，您會明確指出沒有任何欄位可以是 null。 在這裡，您會有新電影的輸入表單，而您要將欄位保留空白。 這就是錯誤。

在此情況下，資料庫實際上不會引發（或*擲*回）錯誤。 您未提供內容類型或年份，因此*AddMovie*頁面中的程式碼會將這些值視為所謂的*空字串*。 當 SQL `Insert Into` 命令執行時，[內容類型] 和 [年份] 欄位在其中沒有有用的資料，但它們不是 null。

很明顯地，您不想讓使用者在資料庫中輸入半空白的電影資訊。 解決方案是驗證使用者的輸入。 一開始，驗證只會確保使用者已輸入所有欄位的值（亦即，它們都不會包含空字串）。

> [!TIP]
> 
> **Null 和空字串**
> 
> 在程式設計中，「沒有值」的不同概念會有所區別。 一般來說，如果從未以任何方式設定或初始化值，就會是*null* 。 相反地，預期字元資料（字串）的變數可以設定為*空字串*。 在此情況下，此值不是 null;它只會明確設定為長度為零的字元字串。 這兩個語句會顯示差異：
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> 這有點複雜，但重點在於，`null` 代表一種不確定的狀態。
> 
> 接下來，請務必瞭解值為 null 的確切時間，以及它是否只是空字串。 在 [ *AddMovie* ] 頁面的程式碼中，您可以使用 `Request.Form["title"]` 等來取得文字方塊的值。 當頁面第一次執行時（在您按一下按鈕之前），`Request.Form["title"]` 的值為 null。 但是當您提交表單時，`Request.Form["title"]` 會取得 `title` 文字方塊的值。 這並不明顯，但空白的文字方塊不是 null;其中只有一個空字串。 因此，當程式碼執行以回應按下按鈕時，`Request.Form["title"]` 中會有一個空字串。
> 
> 這項區別為何重要？ 當您建立*電影*資料表時，您會明確指出沒有任何欄位可以是 null。 但在這裡，您會有新電影的輸入表單，而您會將欄位保留空白。 當您嘗試儲存沒有內容類型或年份值的新電影時，您會合理地預期資料庫抱怨。 這就是 &mdash; 的重點，即使您將這些文字方塊保留空白，值也不會是 null;它們是空字串。 因此，您可以將新電影儲存到資料庫中，這些資料行都是空的 &mdash; 而不是 null！ &mdash; 值。 因此，您必須確定使用者不會提交空字串，您可以藉由驗證使用者的輸入來進行。

### <a name="the-validation-helper"></a>驗證協助程式

ASP.NET Web Pages 包括協助程式 &mdash; `Validation` helper &mdash;，您可以用來確保使用者輸入符合您需求的資料。 `Validation` helper 是內建 ASP.NET Web Pages 的協助程式之一，因此您不需要使用 NuGet 將它安裝為套件，這是您在先前的教學課程中安裝 Gravatar helper 的方式。

若要驗證使用者的輸入，您將執行下列動作：

- 使用 [程式碼]，指定您想要在頁面上的文字方塊中要求值。
- 將測試放入程式碼中，只有當所有專案都正確驗證時，才會將電影資訊新增至資料庫。
- 將程式碼新增至標記，以顯示錯誤訊息。

在 [ *AddMovie* ] 頁面的程式碼區塊中，于變數宣告前面的頂端，新增下列程式碼：

[!code-csharp[Main](entering-data/samples/sample7.cs)]

您會針對您想要要求輸入的每個欄位（`<input>` 元素）呼叫 `Validation.RequireField` 一次。 您也可以為每個呼叫新增自訂的錯誤訊息，就像您在這裡看到的一樣。 （我們只會改變訊息，告訴您可以把任何東西放在那裡）。

如果發生問題，您會想要防止新電影資訊插入資料庫中。 在 `if(IsPost)` 區塊中，使用 `&&` （邏輯 AND）來新增另一個測試 `Validation.IsValid()`的條件。 當您完成時，整個 `if(IsPost)` 區塊看起來就像下面這段程式碼：

[!code-csharp[Main](entering-data/samples/sample8.cs)]

如果您使用 `Validation` helper 註冊的任何欄位發生驗證錯誤，則 `Validation.IsValid` 方法會傳回 false。 在此情況下，將不會執行該區塊中的任何程式碼，因此不會將不正確電影專案插入資料庫中。 當然，您也不會被重新導向到*電影*頁面。

完整的程式碼區塊，包括驗證程式代碼，現在看起來像這個範例：

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>顯示驗證錯誤

最後一個步驟是顯示任何錯誤訊息。 您可以針對每個驗證錯誤顯示個別的訊息，也可以顯示摘要或兩者。 在本教學課程中，您將會執行這兩項作業，讓您可以查看其運作方式。

在您要驗證的每個 `<input>` 元素旁，呼叫 `Html.ValidationMessage` 方法，並將您要驗證的 `<input>` 元素名稱傳遞給它。 您可以將 `Html.ValidationMessage` 方法放在您想要出現錯誤訊息的位置。 當頁面執行時，`Html.ValidationMessage` 方法會呈現驗證錯誤所在的 `<span>` 元素。 （如果沒有錯誤，則會轉譯 `<span>` 專案，但其中沒有任何文字）。

變更頁面中的標記，使其在頁面上包含三個 `<input>` 元素的 `Html.ValidationMessage` 方法，如下列範例所示：

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

若要查看摘要的運作方式，也請在頁面上的 `<h1>Add a Movie</h1>` 元素後面，加入下列標記和程式碼：

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

根據預設，`Html.ValidationSummary` 方法會顯示清單中的所有驗證訊息（位於 `<div>` 元素內的 `<ul>` 元素）。 如同 `Html.ValidationMessage` 方法，一律會轉譯驗證摘要的標記;如果沒有任何錯誤，則不會轉譯任何清單專案。

摘要可以是顯示驗證訊息的替代方式，而不是使用 `Html.ValidationMessage` 方法來顯示每個欄位特定的錯誤。 或者，您可以同時使用摘要和詳細資料。 或者，您可以使用 `Html.ValidationSummary` 方法來顯示一般錯誤，然後使用個別的 `Html.ValidationMessage` 呼叫來顯示詳細資料。

[完成] 頁面現在會如下列範例所示：

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

就這麼容易！ 您現在可以藉由新增電影來測試頁面，但保留一或多個欄位。 當您這樣做時，您會看到下列錯誤顯示：

![新增顯示驗證錯誤訊息的電影頁面](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>設定驗證錯誤訊息的樣式

您可以看到有錯誤訊息，但它們並沒有太大的差異。 不過，有一種簡單的方式可將錯誤訊息樣式。

若要將 `Html.ValidationMessage`顯示的個別錯誤訊息樣式，請建立名為 `field-validation-error`的 CSS 樣式類別。 若要定義驗證摘要的尋找，請建立名為 `validation-summary-errors`的 CSS 樣式類別。

若要查看這項技術的運作方式，請在頁面的 [`<head>`] 區段內加入 `<style>` 元素。 然後定義名為 `field-validation-error` 的樣式類別，以及包含下列規則的 `validation-summary-errors`：

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

一般來說，您可能會將樣式資訊放在個別的 *.css*檔案中，但為了簡單起見，您可以將它們放在頁面中，以供您立即使用。 （稍後在本教學課程中，您會將 CSS 規則移至不同的 *.css*檔案）。

如果發生驗證錯誤，`Html.ValidationMessage` 方法會呈現包含 `class="field-validation-error"`的 `<span>` 元素。 藉由加入該類別的樣式定義，您可以設定訊息的外觀。 如果發生錯誤，`ValidationSummary` 方法同樣會以動態方式呈現屬性 `class="validation-summary-errors"`。

再次執行頁面，並故意省略幾個欄位。 這些錯誤現在更明顯。 （事實上，它們是過渡濫用的，但這只是為了說明您可以執行的動作）。

![[新增電影] 頁面，其中顯示已樣式的驗證錯誤](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>新增電影頁面的連結

最後一個步驟是讓從原始電影清單中取得*AddMovie*頁面變得更方便。

再次開啟 [*電影*] 頁面。 在 `WebGrid` helper 後面的關閉 `</div>` 標記之後，新增下列標記：

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

如先前所見，ASP.NET 會將 `~` 運算子解讀為網站的根目錄。 您不需要使用 `~` 運算子;您可以使用標記 `<a href="./AddMovie">Add a movie</a>` 或其他方式來定義 HTML 瞭解的路徑。 但是，當您建立 Razor 頁面的連結時，`~` 運算子是不錯的一般方法，因為它可讓網站更具彈性，如果您將目前頁面移至子資料夾，此連結仍然會前往 [ *AddMovie* ] 頁面。 （請記住，`~` 運算子僅適用于*cshtml*頁面。 ASP.NET 瞭解它，但它並不是標準的 HTML）。

當您完成時，請執行 [*電影*] 頁面。 看起來會像這個頁面：

![包含連結至 [新增電影] 頁面的電影頁面](entering-data/_static/image7.png)

按一下 [**新增電影**] 連結，以確定它會移至 [ *AddMovie* ] 頁面。

## <a name="coming-up-next"></a>下一步

在下一個教學課程中，您將學習如何讓使用者編輯已在資料庫中的資料。

## <a name="complete-listing-for-addmovie-page"></a>AddMovie 頁面的完整清單

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools 網站上的[SQL INSERT INTO 語句](http://www.w3schools.com/sql/sql_insert.asp)
- [驗證 ASP.NET Web Pages 網站中的使用者輸入](https://go.microsoft.com/fwlink/?LinkId=253002)。 有關使用 `Validation` helper 的詳細資訊。

> [!div class="step-by-step"]
> [上一頁](form-basics.md)
> [下一頁](updating-data.md)
