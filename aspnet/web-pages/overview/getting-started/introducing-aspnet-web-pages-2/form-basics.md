---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: ASP.NET Web Pages 簡介-HTML 表單基本概念 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程說明如何建立輸入表單，以及如何在使用 ASP.NET Web Pages （Razor）時處理使用者輸入的基本概念。 現在您已經 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574281"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>ASP.NET Web Pages 簡介-HTML 表單基本概念

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程說明如何建立輸入表單，以及如何在使用 ASP.NET Web Pages （Razor）時處理使用者輸入的基本概念。 現在您已經有資料庫，您將會使用表單技能，讓使用者能夠在資料庫中尋找特定電影。 它假設您已透過[使用 ASP.NET Web Pages 來顯示資料的簡介來](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)完成此系列。
> 
> 您將學到什麼：
> 
> - 如何使用標準 HTML 元素建立表單。
> - 如何讀取表單中的使用者輸入。
> - 如何使用使用者所提供的搜尋詞彙，建立選擇性地取得資料的 SQL 查詢。
> - 如何讓頁面中的欄位「記住」使用者輸入的內容。
>   
> 
> 討論的功能/技術：
> 
> - `Request` 物件。
> - SQL `Where` 子句。

## <a name="what-youll-build"></a>您要建置的內容

在上一個教學課程中，您已建立資料庫，並在其中加入資料，然後使用 `WebGrid` helper 來顯示資料。 在本教學課程中，您將新增搜尋方塊，讓您尋找特定類型的電影，或其標題包含您輸入的任何文字。 （例如，您可以找到內容類型為「動作」或其標題包含「Harry」或「艾德」）的所有電影。

當您完成本教學課程時，您將會有如下的頁面：

![具有內容類型和標題搜尋的電影頁面](form-basics/_static/image1.png)

頁面的清單部分與上一個教學課程 &mdash; 方格中的相同。 差別在於方格只會顯示您搜尋的電影。

## <a name="about-html-forms"></a>關於 HTML 表單

（如果您有建立 HTML 表單的經驗，以及 `GET` 和 `POST`之間的差異，您可以略過本節）。

表單具有使用者輸入元素 &mdash; 文字方塊、按鈕、選項按鈕、核取方塊、下拉式清單等。 使用者會填入這些控制項或進行選取，然後按一下按鈕來提交表單。

這個範例會說明表單的基本 HTML 語法：

[!code-html[Main](form-basics/samples/sample1.html)]

當此標記在頁面中執行時，它會建立一個簡單的表單，如下圖所示：

![在瀏覽器中呈現的基本 HTML 表單](form-basics/_static/image2.png)

`<form>` 元素會括住要提交的 HTML 元素。 （容易犯的錯誤是將專案新增至頁面，但忘了將它們放在 `<form>` 元素中。 在此情況下，並不會提交任何內容）。`method` 屬性會告訴瀏覽器如何提交使用者輸入。 如果您要在伺服器上執行更新，請將此設定為 `post`，如果您只是從伺服器提取資料，則會 `get`。

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET、POST 和 HTTP 動詞安全**
> 
> HTTP 是瀏覽器和伺服器用來交換資訊的通訊協定，在其基本作業中很簡單。 瀏覽器只會使用幾個動詞來對伺服器提出要求。 當您撰寫 web 的程式碼時，瞭解這些動詞以及瀏覽器和伺服器如何使用它們會很有説明。 遠低於最常使用的動詞：
> 
> - `GET` 瀏覽器會使用這個動詞命令從伺服器提取內容。 例如，當您在瀏覽器中輸入 URL 時，瀏覽器會執行 `GET` 作業來要求您想要的頁面。 如果頁面包含圖形，瀏覽器會執行其他 `GET` 作業來取得影像。 如果 `GET` 作業必須將資訊傳遞給伺服器，則會在查詢字串中將資訊當做 URL 的一部分傳遞。
> - `POST` 瀏覽器會傳送 `POST` 要求，以便提交要在伺服器上新增或變更的資料。 例如，`POST` 指令動詞是用來在資料庫中建立記錄，或變更現有的記錄。 在大部分的情況下，當您填寫表單並按一下 [提交] 按鈕時，瀏覽器會執行 `POST` 作業。 在 `POST` 作業中，傳遞至伺服器的資料會在頁面的主體中。
> 
> 這些動詞的重要差異在於，`GET` 作業不應該變更伺服器上的任何專案，或是以稍微更抽象的方式來放置，`GET` 作業不會導致伺服器上的狀態變更。 您可以視需要在相同的資源上執行 `GET` 作業，而這些資源不會變更。 （`GET` 作業通常稱為「安全」，或使用技術術語，其為*等冪*）。相反地，在每次執行作業時，`POST` 要求都會變更伺服器上的某些專案。
> 
> 有兩個範例將有助於說明這種區別。 當您使用 Bing 或 Google 之類的引擎執行搜尋時，您會填入包含一個文字方塊的表單，然後按一下 [搜尋] 按鈕。 瀏覽器會執行 `GET` 作業，並將您輸入的值當做 URL 的一部分來傳遞。 針對這種類型的表單使用 `GET` 作業是正常的，因為搜尋作業不會變更伺服器上的任何資源，而只會提取資訊。
> 
> 現在請考慮在線上排序某個專案的程式。 填寫訂單詳細資料，然後按一下 [提交] 按鈕。 這項作業將會是 `POST` 的要求，因為此作業會導致伺服器上的變更，例如新的訂單記錄、帳戶資訊的變更，以及可能有其他許多變更。 不同于 `GET` 作業，您無法重複您的 `POST` 要求，如果您這麼做，則每次重新提交要求時，就會在伺服器上產生新的訂單。 （在這種情況下，網站通常會警告您不要再按一次 [提交] 按鈕，或會停用 [提交] 按鈕，讓您不會不小心重新提交表單。）
> 
> 在本教學課程的過程中，您將使用 `GET` 作業和 `POST` 操作，以使用 HTML 表單。 我們將在每個案例中說明您使用的動詞為何是適當的。
> 
> （若要深入瞭解 HTTP 指令動詞，請參閱 W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)一文）。

大部分的使用者輸入元素都是 HTML `<input>` 元素。 它們看起來像 `<input type="type" name="name">,`，其中*type*表示您想要的使用者輸入控制項類型。 這些元素是常見的專案：

- 文字方塊： `<input type="text">`
- 核取方塊： `<input type="check">`
- 選項按鈕： `<input type="radio">`
- 按鈕： `<input type="button">`
- 提交按鈕： `<input type="submit">`

您也可以使用 `<textarea>` 元素來建立多行文字方塊和 `<select>` 元素，以建立下拉式清單或可滾動清單。 （如需 HTML 表單元素的詳細資訊，請參閱 W3Schools 網站上的[Html 表單和輸入](http://www.w3schools.com/html/html_forms.asp)。）

`name` 屬性非常重要，因為名稱是您稍後將會取得元素值的方式，如下所示。

有趣的是，網頁開發人員對使用者的輸入做了什麼。 沒有與這些元素相關聯的內建行為。 相反地，您必須取得使用者已輸入或選取的值，並對它們執行一些動作。 這就是您將在本教學課程中學習到的內容。

> [!TIP] 
> 
> **HTML5 和輸入表單**
> 
> 如您所知，HTML 正在轉換中，而最新版本（HTML5）包含支援更直覺化的方式，讓使用者輸入資訊。 例如，在 HTML5 中，您（網頁開發人員）可以告訴您要使用者輸入日期的頁面。 然後，瀏覽器可以自動顯示行事曆，而不是要求使用者手動輸入日期。 不過，HTML5 是新的，而且所有的瀏覽器目前都不支援。
> 
> ASP.NET Web Pages 支援 HTML5 輸入至使用者瀏覽器的範圍。 如需 HTML5 中 `<input>` 元素的新屬性概念，請參閱 W3Schools 網站上的[HTML &lt;輸入&gt; 類型屬性](http://www.w3schools.com/html/html_form_input_types.asp)。

## <a name="creating-the-form"></a>建立表單

在 WebMatrix 的 [檔案 **] 工作區**中，開啟 [*電影. cshtml* ] 頁面。

在結尾 `</h1>` 標記之後，以及 `grid.GetHtml` 呼叫的開啟 `<div>` 標記之前，新增下列標記：

[!code-html[Main](form-basics/samples/sample2.html)]

此標記會建立一個表單，其中包含名為 `searchGenre` 的文字方塊和 [提交] 按鈕。 [文字方塊] 和 [提交] 按鈕會括在 `<form>` 元素中，其 `method` 屬性設為 `get`。 （請記住，如果您未將 [文字方塊] 和 [提交] 按鈕放在 `<form>` 專案內，當您按一下按鈕時，將不會提交任何內容）。您會在這裡使用 `GET` 動詞，因為您所建立的表單不會在伺服器上進行任何變更，而只會產生搜尋。 （在上一個教學課程中，您使用了 `post` 方法，這就是您將變更提交至伺服器的方式。 您會在下一個教學課程中再次看到）。

執行頁面。 雖然您尚未定義表單的任何行為，但是您可以查看它看起來的樣子：

![具有內容類型搜尋方塊的電影頁面](form-basics/_static/image3.png)

在文字方塊中輸入值，例如 "喜劇"。 然後按一下 [**搜尋**內容類型]。

記下頁面的 URL。 因為您將 `<form>` 專案的 `method` 屬性設定為 [`get`]，所以您輸入的值現在會是 URL 中查詢字串的一部分，如下所示：

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>讀取表單值

此頁面已經包含一些程式碼，可取得資料庫資料並將結果顯示在方格中。 現在您必須新增一些程式碼來讀取文字方塊的值，以便執行包含搜尋詞彙的 SQL 查詢。

因為您將表單的方法設定為 `get`，所以您可以使用如下所示的程式碼，來讀取在文字方塊中輸入的值：

`var searchTerm = Request.QueryString["searchGenre"];`

`Request.QueryString` 物件（`Request` 物件的 `QueryString` 屬性）包含已提交做為 `GET` 作業一部分的元素值。 `Request.QueryString` 屬性包含在表單中提交之值的*集合*（清單）。 若要取得任何個別值，請指定您想要的元素名稱。 這就是為什麼在建立文字方塊的 `<input>` 元素（`searchTerm`）上必須有 `name` 屬性的原因。 （如需 `Request` 物件的詳細資訊，請參閱稍後的[邊欄](#BKMK_TheRequestObject)）。

這很簡單，足以讀取文字方塊的值。 但是，如果使用者沒有在文字方塊中輸入任何內容，但按下 [**搜尋**]，則您可以忽略該點擊，因為沒有任何可搜尋的專案。

下列程式碼範例顯示如何執行這些條件。 （您還不需要新增此程式碼; 您稍後會這麼做）。

[!code-csharp[Main](form-basics/samples/sample3.cs)]

此測試會以這種方式細分：

- 取得 `Request.QueryString["searchGenre"]`的值，也就是輸入至名為 `searchGenre`之 `<input>` 元素的值。
- 使用 `IsEmpty` 方法，找出是否為空的。 這個方法是判斷某個專案（例如，表單元素）是否包含值的標準方式。 但事實上，您只在意它*不*是空的，因此 。
- 將 `!` 運算子加入 `IsEmpty` 測試前面。 （`!` 運算子表示邏輯 NOT）。

在純英文中，整個 `if` 條件會轉譯成下列專案：*如果表單的 searchGenre 元素不是空的，則 ...*

此區塊會設定用來建立使用搜尋詞彙之查詢的階段。 您將在下一節中執行該動作。

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Request 物件**
> 
> `Request` 物件包含當要求或提交頁面時，瀏覽器傳送到您應用程式的所有資訊。 此物件包含使用者提供的任何資訊，例如文字方塊值或要上傳的檔案。 它也包括各種額外的資訊，例如 cookie、URL 查詢字串中的值（如果有的話）、正在執行之網頁的檔案路徑、使用者所使用的瀏覽器類型，以及在瀏覽器中設定的語言清單還有更多。
> 
> `Request` 物件是值的*集合*（清單）。 您可以藉由指定名稱，從集合中取得個別的值：
> 
> `var someValue = Request["name"];`
> 
> `Request` 物件實際上會公開數個子集。 例如:
> 
> - 如果要求是 `POST` 要求，`Request.Form` 會從已提交的 `<form>` 元素內的元素提供值。
> - `Request.QueryString` 只會為您提供 URL 的查詢字串中的值。 （在類似 `http://mysite/myapp/page?searchGenre=action&page=2`的 URL 中，URL 的 `?searchGenre=action&page=2` 區段是查詢字串）。
> - `Request.Cookies` 集合可讓您存取瀏覽器已傳送的 cookie。
> 
> 若要取得您知道在已提交表單中的值，您可以使用 `Request["name"]`。 或者，您可以使用更具體的版本 `Request.Form["name"]` （適用于 `POST` 要求）或 `Request.QueryString["name"]` （適用于 `GET` 要求）。 當然， *name*是要取得的專案名稱。
> 
> 您想要取得的專案名稱在您所使用的集合中必須是唯一的。 這就是為什麼 `Request` 物件提供 `Request.Form` 和 `Request.QueryString`這類子集的原因。 假設您的頁面包含名為 `userName` 的 form 元素，而且*也*包含名為 `userName`的 cookie。 如果您取得 `Request["userName"]`，不論您想要表單值或 cookie，都是不明確的。 不過，如果您取得 `Request.Form["userName"]` 或 `Request.Cookie["userName"]`，您就會明確瞭解要取得哪個值。
> 
> 最好的作法是使用您感興趣的 `Request` 子集，例如 `Request.Form` 或 `Request.QueryString`。 針對您在本教學課程中建立的簡單頁面，它可能不會真正有任何差異。 不過，當您建立更複雜的頁面時，使用明確的版本 `Request.Form` 或 `Request.QueryString` 可以協助您避免頁面包含表單（或多個表單）、cookie、查詢字串值等等時可能發生的問題。

## <a name="creating-a-query-by-using-a-search-term"></a>使用搜尋詞彙建立查詢

既然您已經知道如何取得使用者輸入的搜尋字詞，就可以建立使用它的查詢。 請記住，若要取得資料庫中的所有電影專案，您會使用類似此語句的 SQL 查詢：

`SELECT * FROM Movies`

若只要取得特定電影，您就必須使用包含 `Where` 子句的查詢。 此子句可讓您設定查詢所傳回之資料列的條件。 以下為範例：

`SELECT * FROM Movies WHERE Genre = 'Action'`

基本格式為 `WHERE column = value`。 除了 `=`以外，您還可以使用不同的運算子，例如 `>` （大於）、`<` （小於）、`<>` （不等於）、`<=` （小於或等於）等，視您要尋找的內容而定。

如果您想知道，SQL 語句並不區分大小寫 &mdash; `SELECT` 與 `Select` （或甚至 `select`）相同。 不過，使用者通常會將 SQL 語句中的關鍵字（例如 `SELECT` 和 `WHERE`）大寫，以便更容易閱讀。

### <a name="passing-the-search-term-as-a-parameter"></a>傳遞搜尋詞彙做為參數

搜尋特定的內容類型很容易（`WHERE Genre = 'Action'`），但您想要能夠搜尋使用者輸入的任何類型。 若要這麼做，您可以建立 SQL 查詢，其中包含要搜尋之值的預留位置。 此命令看起來會像下面這樣：

`SELECT * FROM Movies WHERE Genre = @0`

預留位置是後面接著零的 `@` 字元。 您可能會猜到，查詢可以包含多個預留位置，而且它們會命名 `@0`、`@1`、`@2`等等。

若要設定查詢，並實際將值傳遞給它，您可以使用如下所示的程式碼：

[!code-sql[Main](form-basics/samples/sample4.sql)]

這段程式碼與您在方格中顯示資料所做的類似。 唯一的差異如下：

- 查詢包含預留位置（`WHERE Genre = @0"`）。
- 查詢會放入變數（`selectCommand`）;在之前，您會直接將查詢傳遞給 `db.Query` 方法。
- 當您呼叫 `db.Query` 方法時，您會同時傳遞查詢和用於預留位置的值。 （如果查詢有多個預留位置，您會將它們全部當做個別值傳遞給方法）。

如果您將所有這些元素放在一起，您會取得下列程式碼：

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **重要！** 使用預留位置（例如 `@0`）將值傳遞至 SQL 命令對於安全性而言*非常重要*。 您在這裡看到的方式，加上變數資料的預留位置，是您應該用來建立 SQL 命令的唯一方式。
> 
> 絕對不要建立 SQL 語句，方法是將常值文字和您從使用者取得的值放在一起（串連）。 將使用者輸入串連到 SQL 語句，會開啟您的網站進入*sql 插入式攻擊*，其中惡意使用者會將值提交至您的頁面，以攻擊您的資料庫。 （您可以在[SQL 插入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 網站一文中深入瞭解）。

## <a name="updating-the-movies-page-with-search-code"></a>使用搜尋程式碼更新電影頁面

現在您可以更新 [*電影*] 檔案中的程式碼。 若要開始，請使用下列程式碼取代頁面頂端程式碼區塊中的程式碼：

[!code-csharp[Main](form-basics/samples/sample6.cs)]

此處的差異在於，您已將查詢放入 `selectCommand` 變數中，而您將在稍後傳遞給 `db.Query`。 將 SQL 語句放入變數中，可讓您變更語句，這就是執行搜尋時所要執行的動作。

您也已移除這兩行，您將在稍後將它們放回：

[!code-csharp[Main](form-basics/samples/sample7.cs)]

您還不想要執行查詢（也就是呼叫 `db.Query`），而且您也不想要初始化 `WebGrid` helper。 在您瞭解必須執行的 SQL 語句之後，就會執行這些動作。

在此重寫區塊之後，您可以新增用來處理搜尋的邏輯。 完成後的程式碼看起來會像下面這樣。 更新頁面中的程式碼，使其符合此範例：

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

此頁面現在的運作方式如下所示。 每次執行頁面時，程式碼都會開啟資料庫，而 `selectCommand` 變數會設定為從 `Movies` 資料表取得所有記錄的 SQL 語句。 程式碼也會初始化 `searchTerm` 變數。

不過，如果目前的要求包含 `searchGenre` 元素的值，則程式碼會將 `selectCommand` 設定為不同的查詢，也就是包含 `Where` 子句來搜尋內容類型的查詢。 它也會將 `searchTerm` 設定為搜尋方塊所傳遞的內容（這可能不是任何內容）。

不論 `selectCommand`的 SQL 語句為何，程式碼會接著呼叫 `db.Query` 來執行查詢，並將它傳遞至 `searchTerm`中的任何內容。 如果 `searchTerm`中沒有任何東西，這並不重要，因為在這種情況下，沒有任何參數可以將值傳遞給 `selectCommand`。

最後，程式碼會使用查詢結果來初始化 `WebGrid` helper，就像之前一樣。

您可以藉由將 SQL 語句和搜尋詞彙放入變數中來看出，您已在程式碼中增加彈性。 如您稍後在本教學課程中所見，您可以使用此基本架構，並持續為不同的搜尋類型新增邏輯。

## <a name="testing-the-search-by-genre-feature"></a>測試依風格搜尋的功能

在 WebMatrix 中，執行 [*電影. cshtml* ] 頁面。 您會看到具有文字類型文字方塊的頁面。

輸入您為其中一個測試記錄輸入的內容類型，然後按一下 [**搜尋**]。 此時，您只會看到符合該內容類型的電影清單：

![搜尋內容類型 ' Comedies ' 之後的電影頁面清單](form-basics/_static/image4.png)

輸入不同的內容類型，然後再搜尋一次。 嘗試使用全部小寫或全部大寫來輸入內容類型，讓您可以看到搜尋不區分大小寫。

## <a name="remembering-what-the-user-entered"></a>「記住」使用者輸入的內容

您可能已經注意到在輸入內容類型，然後按一下 [**搜尋**內容類型] 之後，就會看到該內容類型的清單。 不過，[搜尋] 文字方塊是空的 &mdash; 換句話說，這並不記得您輸入的內容。

請務必瞭解為何會發生這種行為。 當您提交頁面時，瀏覽器會將要求傳送至 web 伺服器。 當 ASP.NET 取得要求時，它會建立頁面的全新實例、執行其中的程式碼，然後再次將頁面轉譯至瀏覽器。 但實際上，此頁面並不知道您使用的是舊版本身。 它知道它會得到一個要求，裡面有一些表單資料。

每次要求頁面時 &mdash; 是第一次還是提交，&mdash; 您正在取得新的頁面。 網頁伺服器沒有您上一個要求的記憶體。 兩者都不會 ASP.NET，而且瀏覽器都不會執行。 這些個別實例之間的唯一連接是您在它們之間傳輸的任何資料。 例如，如果您提交頁面，新的頁面實例可以取得先前實例所傳送的表單資料。 （在頁面之間傳遞資料的另一種方式是使用 cookie）。

描述這種情況的一種正式方式是說，網頁是*無狀態*的。 網頁伺服器和頁面本身，以及頁面中的元素不會維護任何有關頁面先前狀態的資訊。 Web 是以這種方式設計的，因為維護個別要求的狀態會快速耗盡 web 伺服器的資源，這通常會處理數千個（甚至是每秒數百個要求）。

這就是為什麼文字方塊是空的。 提交頁面之後，ASP.NET 會建立頁面的新實例，並透過程式碼和標記執行。 該程式碼中沒有任何告訴 ASP.NET 將值放入文字方塊中的東西。 因此 ASP.NET 不會執行任何動作，而且文字方塊的呈現不含值。

實際上，有一個簡單的方法可以解決此問題。 您在文字方塊中輸入的內容類型可供您在*程式*代碼中使用，&mdash; 它在 `Request.QueryString["searchGenre"]`中。

更新文字方塊的標記，讓 `value` 屬性從 `searchTerm`取得其值，如下列範例所示：

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

在此頁面中，您也可以將 `value` 屬性設定為 `searchTerm` 變數，因為該變數也包含您所輸入的內容類型。 但是，使用 `Request` 物件來設定 `value` 屬性，如下所示，這是完成這項工作的標準方式。 （假設您甚至想要在某些情況下執行這項 &mdash;，您可能會想要在欄位中呈現*不含*值的頁面。 這一切都取決於應用程式的狀況。）

> [!NOTE]
> 您不能「記住」用於密碼的文字方塊值。 這會是一個安全性漏洞，讓使用者可以使用程式碼填寫密碼欄位。

再次執行頁面，輸入內容類型，然後按一下 [**搜尋**內容類型]。 這次不只會看到搜尋結果，而文字方塊會記住您上一次輸入的內容：

![頁面，顯示文字方塊已「記住」先前的專案](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>搜尋標題中的任何單字

您現在可以搜尋任何類型內容，但您可能也會想要搜尋標題。 當您搜尋時，很難正確地取得標題，因此您可以搜尋出現在標題中任何位置的單字。 若要在 SQL 中執行此動作，請使用 `LIKE` 運算子和語法，如下所示：

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

此命令會取得標題包含「艾德」的所有電影。 當您使用 `LIKE` 運算子時，您會在搜尋字詞中包含萬用字元 `%`。 搜尋 `LIKE 'adventure%'` 表示「從 ' 冒險 ' 開始」。 （技術上來說，這表示「字串 ' 艾德」後面接著任何東西。」）同樣地，搜尋詞彙 `LIKE '%adventure'` 表示「任何後面接著字串 ' 艾德 '」的「專案」，也就是「以 ' 艾德 ' 做為結尾」的另一種方式。

因此，搜尋詞彙 `LIKE '%adventure%'` 因此會在標題中的任何位置表示「具有 ' 艾德」。」 （技術上來說，「標題中的任何東西」，後面接著「艾德」，再加上任何東西）。

在 `<form>` 專案中，于內容類型搜尋的結尾 `</div>` 標記（緊接在結尾 `</form>` 元素之前）新增下列標記：

[!code-html[Main](form-basics/samples/sample10.html)]

處理此搜尋的程式碼類似于內容類型搜尋的程式碼，不同之處在于您必須組合 `LIKE` 搜尋。 在頁面頂端的程式碼區塊中，在內容類型搜尋的 `if` 區塊之後，新增此 `if` 組塊：

[!code-csharp[Main](form-basics/samples/sample11.cs)]

此程式碼會使用您稍早看到的相同邏輯，不同之處在于搜尋會使用 `LIKE` 運算子，而程式碼會將 "`%`" 放在搜尋詞彙的前後。

請注意，如何輕鬆地將另一個搜尋新增至頁面。 您只需要：

- 建立測試的 `if` 區塊，以查看相關的搜尋方塊是否具有值。
- 將 `selectCommand` 變數設定為新的 SQL 語句。
- 將 `searchTerm` 變數設定為要傳遞給查詢的值。

以下是完整的程式碼區塊，其中包含標題搜尋的新邏輯：

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

以下摘要說明此程式碼的作用：

- `searchTerm` 和 `selectCommand` 的變數會在頂端初始化。 您將根據使用者在頁面中執行的工作，將這些變數設定為適當的搜尋字詞（如果有的話）和適當的 SQL 命令。 預設搜尋是從資料庫取得所有電影的簡單案例。
- 在 `searchGenre` 和 `searchTitle`的測試中，程式碼會將 `searchTerm` 設定為您要搜尋的值。 這些程式碼區塊也會將 `selectCommand` 設定為該搜尋的適當 SQL 命令。
- `db.Query` 方法只會叫用一次，使用 `selectedCommand` 的 SQL 命令，以及 `searchTerm`中的任何值。 如果沒有搜尋字詞（沒有內容類型，也沒有標題字），`searchTerm` 的值就是空字串。 不過，這並不重要，因為在這種情況下，查詢不需要參數。

## <a name="testing-the-title-search-feature"></a>測試標題搜尋功能

現在您可以測試已完成的搜尋頁面。 執行*電影。 cshtml*。

輸入內容類型，然後按一下 [**搜尋**內容類型]。 格線會顯示該內容類型的電影，就像之前一樣。

輸入標題文字，然後按一下 [**搜尋標題**]。 此方格會顯示標題中有該單字的電影。

![在標題中搜尋 ' the ' 之後的電影頁面清單](form-basics/_static/image6.png)

將兩個文字方塊保持空白，然後按一下其中一個按鈕。 方格會顯示所有電影。

## <a name="combining-the-queries"></a>結合查詢

您可能會注意到，您可以執行的搜尋是獨佔的。 您不能同時搜尋標題和內容類型，即使這兩個搜尋方塊中有值也一樣。 例如，您無法搜尋標題包含 "艾德" 的所有動作電影。 （當頁面已編碼時，如果您同時輸入內容類型和標題的值，則標題搜尋會優先）。若要建立合併條件的搜尋，您必須建立具有如下語法的 SQL 查詢：

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

而且，您必須使用如下所示的語句來執行查詢（大致說）：

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

建立邏輯來允許許多搜尋條件的排列，可能會有一些相關的情況，如您所見。 因此，我們將在此停止。

## <a name="coming-up-next"></a>下一步

在下一個教學課程中，您將建立使用表單的頁面，讓使用者將電影新增至資料庫。

## <a name="complete-listing-for-movie-page-updated-with-search"></a>電影頁面的完整清單（使用搜尋更新）

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools 網站上的[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)
- W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章

> [!div class="step-by-step"]
> [上一頁](displaying-data.md)
> [下一頁](entering-data.md)
