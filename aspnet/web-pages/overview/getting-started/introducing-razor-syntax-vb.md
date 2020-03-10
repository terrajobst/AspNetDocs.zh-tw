---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: 使用 Razor 語法 ASP.NET Web 程式設計的簡介（Visual Basic） |Microsoft Docs
author: Rick-Anderson
description: 本附錄提供使用 Razor 語法在 Visual Basic 中使用 ASP.NET 網頁進行程式設計的總覽。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526590"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>使用 Razor 語法 ASP.NET Web 程式設計的簡介（Visual Basic）

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文提供使用 Razor 語法和 Visual Basic 進行 ASP.NET Web Pages 程式設計的總覽。 ASP.NET 是 Microsoft 在網頁伺服器上執行動態網頁的技術。
> 
> **您將瞭解的內容**：
> 
> - 使用 Razor 語法開始進行程式設計 ASP.NET Web Pages 的前8個程式設計秘訣。
> - 您需要的基本程式設計概念。
> - 什麼是 ASP.NET 伺服器程式碼和 Razor 語法的相關資訊。
>   
> 
> ## <a name="software-versions"></a>軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

使用 ASP.NET Web Pages 搭配 Razor 語法的大部分範例C#。 但是 Razor 語法也支援 Visual Basic。 若要在 Visual Basic 中程式設計 ASP.NET 網頁，請建立副檔名為*vbhtml*的網頁，然後加入 Visual Basic 碼。 本文可讓您瞭解如何使用 Visual Basic 語言和語法來建立 ASP.NET 網頁。

> [!NOTE]
> C#和 Visual Basic 版本中提供 Microsoft WebMatrix 的預設網站範本（**麵包店**、**相片圖庫**和**入門網站**等等）。 您可以將 Visual Basic 範本安裝為 NuGet 套件。 網站範本會安裝在您網站的根資料夾中，名為*Microsoft templates*的資料夾中。

## <a name="the-top-8-programming-tips"></a>前8個程式設計提示

本節列出當您使用 Razor 語法開始撰寫 ASP.NET 伺服器程式碼時，您絕對需要知道的幾個秘訣。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. 使用 @ 字元將程式碼加入至頁面

`@` 字元會啟動內嵌運算式、單一語句區塊和多重語句區塊：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

在瀏覽器中顯示的結果：

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 編碼**
> 
> 當您使用 `@` 字元在頁面中顯示內容時（如上述範例所示），ASP.NET 會以 HTML 編碼輸出。 這會將保留的 HTML 字元（例如 `<` 和 `>` 和 `&`）取代為程式碼，讓字元在網頁中顯示為字元，而不是被轉譯為 HTML 標籤或實體。 如果沒有 HTML 編碼，來自您的伺服器程式碼的輸出可能無法正確顯示，而且可能會讓頁面暴露于安全性風險下。
> 
> 如果您的目標是要輸出將標記轉譯為標記的 HTML 標籤（例如 `<p></p>` 用於段落或 `<em></em>` 強調文字），請參閱本文稍後的在程式[代碼區塊中結合文字、標記和程式碼](#BM_CombiningTextMarkupAndCode)一節。
> 
> 若要深入瞭解 HTML 編碼，請參閱[使用 ASP.NET Web Pages 網站中的 Html 表單](https://go.microsoft.com/fwlink/?LinkId=202892)。

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. 以程式碼括住程式碼區塊 .。。結束代碼

程式碼區塊包含一或多個程式碼語句，並以 `Code` 和 `End Code`的關鍵字括住。 將開頭的 `Code` 關鍵字緊接在 `@` 字元&#8212;之後，其之間不能有空格。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

在瀏覽器中顯示的結果：

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. 在區塊內，您會結束每個程式碼語句並加上分行符號

在 Visual Basic 的程式碼區塊中，每個語句的結尾都是分行符號。 （稍後在本文中，您會看到一個將長程式碼語句包裝成多行（如有需要）的方法）。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. 您可以使用變數來儲存值

您可以將值儲存在*變數*中，包括字串、數位和日期等等。您可以使用 `Dim` 關鍵字來建立新的變數。 您可以使用 `@`，直接在頁面中插入變數值。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

在瀏覽器中顯示的結果：

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 用雙引號括住常值字串

*字串*是視為文字的字元序列。 若要指定字串，請將其括在雙引號內：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

若要在字串值內內嵌雙引號，請插入兩個雙引號字元。 如果您想要在頁面輸出中出現雙引號一次，請在加上引號的字串中輸入 `""`，如果您希望它出現兩次，請在加上引號的字串中輸入 `""""`。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

在瀏覽器中顯示的結果：

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic 程式碼不區分大小寫

Visual Basic 語言不區分大小寫。 程式設計關鍵字（例如 `Dim`、`If`和 `True`）和變數名稱（例如 `myString`或 `subTotal`）可在任何情況下寫入。

下列幾行程式碼會使用小寫名稱將值指派給變數 `lastname`，然後使用大寫名稱將變數值輸出至頁面。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

在瀏覽器中顯示的結果：

![vb-語法-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. 您的程式碼大部分都牽涉到使用物件

物件代表您可以使用&#8212;頁面、文字方塊、檔案、影像、web 要求、電子郵件訊息、客戶記錄（資料庫資料列）等進行程式設計的東西。物件具有描述其特性&#8212;的屬性：文字方塊物件具有 `Text` 屬性、要求物件具有 `Url` 屬性、電子郵件訊息具有 `From` 屬性，以及客戶物件具有 `FirstName` 屬性。 物件也有 &quot;動詞&quot; 可以執行的方法。 範例包括 file 物件的 `Save` 方法、影像物件的 `Rotate` 方法，以及電子郵件物件的 `Send` 方法。

您通常會使用 `Request` 物件，這會提供如頁面上表單欄位的值（文字方塊等）、建立要求的瀏覽器類型、頁面的 URL、使用者身分識別等資訊。這個範例會示範如何存取 `Request` 物件的屬性，以及如何呼叫 `Request` 物件的 `MapPath` 方法，這會提供您伺服器上頁面的絕對路徑：

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

在瀏覽器中顯示的結果：

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 您可以撰寫程式碼來做出決策

動態網頁的主要功能是，您可以根據條件來決定要執行的動作。 最常見的做法是使用 `If` 語句（和選擇性的 `Else` 語句）。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

語句 `If IsPost` 是撰寫 `If IsPost = True`的簡寫方式。 除了 `If` 語句之外，還有各種不同的方法可以測試條件、重複的程式碼區塊等等，本文稍後會加以說明。

在瀏覽器中顯示的結果（按一下 [**提交**] 之後）：

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET 和 POST 方法和 IsPost 屬性**
> 
> 網頁（HTTP）所使用的通訊協定支援非常有限的方法數（&quot;動詞&quot;），可用來對伺服器提出要求。 最常見的兩個是 GET，用來讀取頁面和 POST （用來提交頁面）。 一般情況下，使用者第一次要求頁面時，會使用 GET 來要求頁面。 如果使用者填滿表單，然後按一下 [**提交**]，則瀏覽器會對伺服器提出 POST 要求。
> 
> 在 web 程式設計中，知道頁面是否以 GET 或 POST 的方式要求，讓您知道如何處理頁面，通常會很有説明。 在 ASP.NET Web Pages 中，您可以使用 [`IsPost`] 屬性來查看要求是 GET 或 POST。 如果要求是 POST，`IsPost` 屬性會傳回 true，而您可以執行讀取表單上文字方塊值之類的動作。 您會看到的許多範例會告訴您如何根據 `IsPost`的值，以不同的方式處理頁面。

## <a name="a-simple-code-example"></a>簡單的程式碼範例

此程式說明如何建立說明基本程式設計技術的頁面。 在此範例中，您會建立可讓使用者輸入兩個數字的頁面，然後將其加入並顯示結果。

1. 在您的編輯器中，建立新的檔案，並將它命名為*AddNumbers*。
2. 將下列程式碼和標記複製到頁面中，並取代頁面中已存在的任何專案。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    以下是您要注意的一些事項：

    - `@` 字元會啟動頁面中第一個程式碼區塊，並在靠近底部的 `totalMessage` 變數之前。
    - 頁面頂端的區塊會以 `Code...End Code`括住。
    - `total`、`num1`、`num2`和 `totalMessage` 的變數會儲存數個數字和一個字串。
    - 指派給 `totalMessage` 變數的常值字串值是以雙引號括住。
    - 因為 Visual Basic 程式碼不區分大小寫，所以當使用 `totalMessage` 變數接近頁面底部時，其名稱只需要符合頁面頂端的變數宣告拼寫。 大小寫並不重要。
    - 運算式 `num1.AsInt()` + `num2.AsInt()` 會顯示如何使用物件和方法。 每個變數上的 `AsInt` 方法會將使用者輸入的字串，轉換成可新增的整數（整數）。
    - `<form>` 標記包含 `method="post"` 屬性。 這會指定當使用者按一下 [**新增**] 時，會使用 HTTP POST 方法將頁面傳送至伺服器。 提交頁面時，程式碼 `If IsPost` 會評估為 true，並執行條件式程式碼，以顯示加入數位的結果。
3. 儲存頁面，並在瀏覽器中執行。 （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）輸入兩個整數，然後按一下 [**新增**] 按鈕。

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic 語言和語法

稍早您會看到如何建立 ASP.NET 網頁的基本範例，以及如何將伺服器程式碼加入至 HTML 標籤。 在這裡，您將瞭解使用 Visual Basic 來撰寫 ASP.NET 伺服器程式碼的基本概念&#8212; ，Razor 語法亦即程式設計語言規則。

如果您對程式設計有經驗（特別是使用 C、 C++、 C#、Visual Basic 或 JavaScript），您在這裡閱讀的大部分內容都很熟悉。 您可能只需要熟悉 WebMatrix 程式碼如何加入至*vbhtml*檔案中的標記。

### <a id="BM_CombiningTextMarkupAndCode"></a>結合程式碼區塊中的文字、標記和程式碼

在 [伺服器程式碼區塊] 中，您通常會想要將文字和標記輸出至頁面。 如果伺服器程式碼區塊包含不是程式碼的文字，而應該改為轉譯，則 ASP.NET 必須能夠區別該文字與程式碼。 有數個方式可以執行此動作。

- 將文字括在 HTML 區塊元素中，例如 `<p></p>` 或 `<em></em>`：

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML 元素可以包含文字、其他 HTML 專案和伺服器程式碼運算式。 當 ASP.NET 看到開頭的 HTML 標籤（例如 `<p>`）時，它會將元素及其內容的所有專案轉譯為瀏覽器（並解析伺服器程式碼運算式）。

- 請使用 `@:` 運算子或 `<text>` 元素。 `@:` 輸出包含純文字或不相符 HTML 標籤的單一行內容;`<text>` 元素會將多行括住以輸出。 當您不想要將 HTML 元素轉譯為輸出的一部分時，這些選項會很有用。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    下列範例會重複上一個範例，但會使用一對 `<text>` 標記來括住要轉譯的文字。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    在下列範例中，`<text>` 和 `</text>` 標記會括住三行，其中全部都有一些非內含性文字和不相符的 HTML 標籤（`<br />`），以及伺服器程式碼和相符的 HTML 標籤。 同樣地，您也可以分別在每一行的前面加上 `@:` 運算子;任一種方法都可行。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > 當您&#8212;使用 HTML 專案（如本節所示）輸出文字時，`@:` 運算子或 `<text>` 元素&#8212; ASP.NET 不會對輸出進行 HTML 編碼。 （如先前所述，ASP.NET 會對前面加上 `@`的伺服器程式碼運算式和伺服器程式碼區塊的輸出進行編碼，但本節中所述的特殊情況除外）。

### <a name="whitespace"></a>Whitespace

語句（和字串常值外部）中的額外空格不會影響語句：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>將長語句細分成多行

在每一行程式碼之後，您可以使用底線字元 `_` （在 Visual Basic 中稱為*接續字元*），將長程式碼語句分解成多行。 若要將語句分成下一行，請在行尾加入一個空格，然後再加上接續字元。 繼續下一行中的語句。 您可以視需要將語句包裝到多行，以提高可讀性。 下列陳述式是相同的：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

不過，您無法在字串常值的中間換行。 下列範例無法使用：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

若要結合一個長字串，以包裝到多行（如上述程式碼），您必須使用*串連運算子*（`&`），這將在本文稍後看到。

### <a name="code-comments"></a>程式碼批註

批註可讓您為自己或其他人留下筆記。 Razor 語法批註的前面會加上 `@*`，並以 `*@`結尾。

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

在程式碼區塊中，您可以使用 Razor 語法批註，也可以使用一般的 Visual Basic 批註字元，這是每一行前面加上一個單引號（`'`）。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>變數

變數是您用來儲存資料的已命名物件。 您可以將變數命名為任何名稱，但名稱必須以字母字元開頭，而且不能包含空格或保留字元。 如先前所見，在 Visual Basic 中，變數名稱中的字母大小寫並不重要。

### <a name="variables-and-data-types"></a>變數和資料類型

變數可以具有特定的資料類型，以指出變數中儲存的資料種類。 您可以擁有儲存字串值的字串變數（例如 &quot;Hello world&quot;）、儲存整數值（例如3或79）的整數變數，以及以各種格式（例如4/12/2012 或3月2009）儲存日期值的日期變數。 而且還有許多其他資料類型可供您使用。

不過，您不需要指定變數的類型。 在大多數情況下，ASP.NET 可以根據變數中的資料使用方式來找出型別。 （有時候您必須指定類型，您將會看到這是 true 的範例）。

若要宣告變數而不指定類型，請使用 `Dim` 加上變數名稱（例如，`Dim myVar`）。 若要宣告型別為的變數，請使用 `Dim` 加上變數名稱，後面接著 `As` 然後是型別名稱（例如，`Dim myVar As String`）。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

下列範例顯示使用網頁中之變數的一些內嵌運算式。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

在瀏覽器中顯示的結果：

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>轉換和測試資料類型

雖然 ASP.NET 通常可以自動判斷資料類型，但有時卻不能。 因此，您可能需要執行明確轉換來協助 ASP.NET。 即使您不需要轉換類型，有時還是可以測試以查看您可能使用的資料類型。

最常見的情況是，您必須將字串轉換成另一種類型，例如整數或日期。 下列範例顯示您必須將字串轉換成數位的一般情況。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

就規則而言，使用者輸入會以字串的形式提供給您。 即使您已提示使用者輸入數位，而且即使他們輸入了數位，當使用者輸入提交，而且您在程式碼中讀取時，資料仍會是字串格式。 因此，您必須將字串轉換成數位。 在此範例中，如果您嘗試對值執行算術而不加以轉換，則會產生下列錯誤，因為 ASP.NET 無法加入兩個字串：

`Cannot implicitly convert type 'string' to 'int'.`

若要將值轉換為整數，您可以呼叫 `AsInt` 方法。 如果轉換成功，您可以接著加入數位。

下表列出一些常見的變數轉換和測試方法。

:::row:::
    :::column:::
        <strong>方法</strong>
    :::column-end:::
    :::column:::
        <strong>說明</strong>
    :::column-end:::
    :::column:::
        <strong>範例</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        將代表整數（例如 &quot;593&quot;）的字串轉換為整數。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        將 &quot;true&quot; 或 &quot;false&quot; 之類的字串轉換成布林值類型。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        將具有十進位值（例如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字串轉換為浮點數。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        將具有十進位值（例如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字串轉換為十進位數。 （在 ASP.NET 中，十進位數比浮點數更精確）。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        將表示日期和時間值的字串轉換為 ASP.NET `DateTime` 類型。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        將任何其他資料類型轉換為字串。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>運算子

「運算子」是一個關鍵字或字元，告訴 ASP.NET 要在運算式中執行哪一種命令。 Visual Basic 支援許多運算子，但您只需要辨識幾個，就能開始開發 ASP.NET 網頁。 下表摘要說明最常見的運算子。

:::row:::
    :::column:::
        <strong>Operator</strong>
    :::column-end:::
    :::column:::
        <strong>說明</strong>
    :::column-end:::
    :::column:::
        <strong>範例</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        數值運算式中使用的數學運算子。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        指派和相等。 視內容而定，請將語句右邊的值指派給左邊的物件，或檢查值是否相等。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        不等。 如果值不相等，則傳回 `True`。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        小於、大於、小於或等於，且大於或等於。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        串連，用來聯結字串。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        遞增和遞減運算子，會從變數相加和減去1（分別為）。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        網點. 用來區別物件及其屬性和方法。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        後. 用來將運算式分組、將參數傳遞給方法，以及存取陣列和集合的成員。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        並非. 將 true 值反轉為 false，反之亦然。 通常用來做為測試 `False` 的簡短方式（也就是不 `True`）。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        邏輯 AND 和 OR，用來將條件連結在一起。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a>在程式碼中使用檔案和資料夾路徑

您通常會使用程式碼中的檔案和資料夾路徑。 以下是網站的實體資料夾結構範例，因為它可能會出現在您的開發電腦上：

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

以下是一些有關 Url 和路徑的基本詳細資料：

- URL 的開頭是功能變數名稱（`http://www.example.com`）或伺服器名稱（`http://localhost`，`http://mycomputer`）。
- URL 會對應至主機電腦上的實體路徑。 例如，`http://myserver` 可能對應到伺服器上的*C:\websites\mywebsite*資料夾。
- 虛擬路徑是用來在程式碼中表示路徑的速記，而不需要指定完整路徑。 它包含在網域或伺服器名稱後面的 URL 部分。 當您使用虛擬路徑時，您可以將程式碼移至不同的網域或伺服器，而不需要更新路徑。

以下是可協助您瞭解差異的範例：

| 完成 URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| 伺服器名稱 | *mycompanyserver* |
| 虛擬路徑 | */humanresources/CompanyPolicy.htm* |
| 實體路徑 | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

虛擬根目錄是/，就像 C：磁片磁碟機的根目錄一樣。 （虛擬資料夾路徑一律使用正斜線）。資料夾的虛擬路徑不一定要有與實體資料夾相同的名稱;它可以是別名。 （在實際執行伺服器上，虛擬路徑很少會符合確切的實體路徑）。

當您在程式碼中使用檔案和資料夾時，有時候您必須參考實體路徑，有時也需要參照虛擬路徑，視您使用的物件而定。 ASP.NET 提供這些工具，讓您在程式碼中使用檔案和資料夾路徑： `Server.MapPath` 方法，以及 `~` 運算子和 `Href` 方法。

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>將虛擬轉換成實體路徑：伺服器. MapPath 方法

`Server.MapPath` 方法會將虛擬路徑（例如 */default.cshtml*）轉換為絕對實體路徑（例如*C:\WebSites\MyWebSiteFolder\default.cshtml*）。 每當您需要完整的實體路徑時，都可以使用這個方法。 典型的範例是當您在 web 伺服器上讀取或寫入文字檔或影像檔案時。

您通常不知道網站在主控網站伺服器上的絕對實體路徑，因此這個方法可以將您知道的路徑（虛擬路徑）轉換成伺服器上的對應路徑。 您會將檔案或資料夾的虛擬路徑傳遞至方法，並傳回實體路徑：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>參考虛擬根目錄： ~ 運算子和 Href 方法

在*cshtml*或*vbhtml*檔案中，您可以使用 `~` 運算子來參考虛擬根路徑。 這非常方便，因為您可以在網站中移動頁面，而其包含的任何連結也不會中斷。 如果您將網站移至不同的位置，這也很方便。 以下是一些範例：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

如果網站 `http://myserver/myapp`，以下是當頁面執行時，ASP.NET 會如何處理這些路徑：

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

（您實際上不會看到這些路徑做為變數的值，但是 ASP.NET 會將這些路徑視為其本身）。

您可以在伺服器程式碼（如上）和標記中使用 `~` 運算子，如下所示：

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

在標記中，您可以使用 `~` 運算子來建立資源的路徑，例如影像檔、其他網頁和 CSS 檔案。 當頁面執行時，ASP.NET 會查看頁面（程式碼和標記），並將所有 `~` 參考解析為適當的路徑。

## <a name="conditional-logic-and-loops"></a>條件式邏輯和迴圈

ASP.NET 伺服器程式碼可讓您根據條件執行工作，並撰寫程式碼，以重複語句的特定次數，也就是執行迴圈的程式碼）。

### <a name="testing-conditions"></a>測試條件

若要測試簡單的條件，請使用 `If...Then` 語句，這會根據您指定的測試傳回 `True` 或 `False`：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If` 關鍵字會啟動區塊。 實際的測試（條件）會遵循 `If` 關鍵字，並傳回 true 或 false。 `If` 語句的結尾為 `Then`。 如果測試為 true，將會執行的語句會以 `If` 和 `End If`括住。 `If` 語句可以包含 `Else` 區塊，指定當條件為 false 時要執行的語句：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

如果 `If` 語句啟動程式碼區塊，您就不需要使用一般的 `Code...End Code` 語句來包含區塊。 您可以只將 `@` 新增至區塊，它就能正常執行。 這個方法適用于 `If`，以及後面接著程式碼區塊的其他 Visual Basic 程式設計關鍵字，包括 `For`、`For Each`、`Do While`等等。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

您可以使用一或多個 `ElseIf` 區塊來新增多個條件：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

在此範例中，如果 `If` 區塊中的第一個條件不是 true，則會檢查 `ElseIf` 條件。 如果符合該條件，就會執行 `ElseIf` 區塊中的語句。 如果沒有符合任何條件，則會執行 `Else` 區塊中的語句。 您可以新增任意數目的 `ElseIf` 區塊，然後關閉 `Else` 區塊，做為 &quot;所有其他專案&quot; 條件。

若要測試大量的條件，請使用 `Select Case` 組塊：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

要測試的值是以括弧括住（在範例中為 weekday 變數）。 每個個別測試都會使用列出值的 `Case` 語句。 如果 `Case` 語句的值符合測試值，則會執行該 `Case` 區塊中的程式碼。

在瀏覽器中顯示的最後兩個條件式區塊的結果：

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>迴圈程式碼

您通常需要重複執行相同的語句。 您可以藉由迴圈來完成這項操作。 例如，您通常會針對資料集合中的每個專案執行相同的語句。 如果您確切知道您想要迴圈的次數，可以使用 `For` 迴圈。 這種迴圈特別適合用來計算或計數：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

迴圈會以 `For` 關鍵字開頭，後面接著三個元素：

- 緊接在 `For` 語句之後，您可以宣告計數器變數（您不需要使用 `Dim`），然後指定範圍，如 `i = 10 to 20`中所示。 這表示變數 `i` 會開始計數為10，並繼續直到達到20（含）為止。
- 在 `For` 和 `Next` 語句之間是區塊的內容。 這可以包含一或多個以每個迴圈執行的程式碼語句。
- `Next i` 語句會結束迴圈。 它會遞增計數器並啟動迴圈的下一個反復專案。

`For` 和 `Next` 行之間的程式程式碼包含針對迴圈的每個反復專案執行的程式碼。 標記會每次建立新的段落（`<p>` 元素），並在輸出中加入一行，顯示 i （計數器）的值。 當您執行此頁面時，此範例會建立顯示輸出的11行，而每一行中的文字會指出專案編號。

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

如果您使用的是集合或陣列，通常會使用 `For Each` 迴圈。 集合是一組類似的物件，而 `For Each` 迴圈可讓您在集合中的每個專案上執行工作。 這種類型的迴圈對集合很方便，因為與 `For` 迴圈不同的是，您不需要遞增計數器或設定限制。 相反地，`For Each` 迴圈程式碼只會繼續完成集合，直到完成為止。

這個範例會傳回 `Request.ServerVariables` 集合中的專案（其中包含您的 web 伺服器的相關資訊）。 它會使用 `For Each` 迴圈來顯示每個專案的名稱，方法是在 HTML 項目符號清單中建立新的 `<li>` 元素。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each` 關鍵字後面接著一個變數，代表集合中的單一專案（在範例中，`myItem`），後面接著 `In` 關鍵字，後面接著您要迴圈執行的集合。 在 `For Each` 迴圈的主體中，您可以使用先前宣告的變數來存取目前的專案。

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

若要建立更一般用途的迴圈，請使用 `Do While` 語句：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

這個迴圈會以 `Do While` 關鍵字開頭，後面接著條件，然後是要重複的區塊。 迴圈通常會遞增（加入）或遞減（減去）用來計算的變數或物件。 在此範例中，每次執行迴圈時，`+=` 運算子都會在變數的值加1。 （若要遞減迴圈中計數的變數，您可以使用遞減運算子 `-=`）。

## <a name="objects-and-collections"></a>物件和集合

ASP.NET 網站中幾乎所有內容都是物件，包括網頁本身。 本節討論您在程式碼中經常使用的一些重要物件。

### <a name="page-objects"></a>頁面物件

ASP.NET 中最基本的物件是頁面。 您可以直接存取頁面物件的屬性，而不需要任何限定的物件。 下列程式碼會使用頁面的 `Request` 物件，取得頁面的檔案路徑：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

您可以使用 `Page` 物件的屬性來取得大量資訊，例如：

- `Request` 如您所見，這是目前要求的相關資訊集合，包括提出要求的瀏覽器類型、頁面的 URL、使用者身分識別等。
- `Response` 這是在伺服器程式碼完成執行時，將會傳送至瀏覽器的回應（頁面）相關資訊集合。 例如，您可以使用這個屬性將資訊寫入至回應。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>集合物件（陣列和字典）

集合是一組相同類型的物件，例如從資料庫 `Customer` 物件的集合。 ASP.NET 包含許多內建集合，例如 `Request.Files` 集合。

您通常會使用集合中的資料。 有兩個常見的集合類型是*陣列*和*字典*。 當您想要儲存類似專案的集合，但不想要建立個別的變數來保存每個專案時，陣列會很有用：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

使用陣列，您可以宣告特定的資料類型，例如 `String`、`Integer`或 `DateTime`。 若要指出變數可以包含陣列，您可以在宣告的變數名稱中加上括弧（例如 `Dim myVar() As String`）。 您可以使用物件的位置（索引），或使用 `For Each` 語句來存取陣列中的專案。 陣列索引以零&#8212;為起始，亦即，第一個專案位於位置0，第二個專案位於位置1，依此類推。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

您可以藉由取得 `Length` 屬性來判斷陣列中的專案數。 若要取得陣列中特定專案的位置（也就是搜尋陣列），請使用 `Array.IndexOf` 方法。 您也可以執行一些動作，像是反轉陣列的內容（`Array.Reverse` 方法）或排序內容（`Array.Sort` 方法）。

在瀏覽器中顯示的字串陣列程式碼輸出：

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

字典是索引鍵/值組的集合，您可以在其中提供用來設定或抓取對應值的索引鍵（或名稱）：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

若要建立字典，您可以使用 `New` 關鍵字來表示您要建立新的 `Dictionary` 物件。 您可以使用 `Dim` 關鍵字，將字典指派給變數。 您可以使用括弧（`( )`）來指示字典中專案的資料類型。 在宣告的結尾，您必須加入另一對括弧，因為這實際上是建立新字典的方法。

若要將專案加入至字典，您可以呼叫 dictionary 變數的 `Add` 方法（在此案例中為`myScores`），然後指定索引鍵和值。 或者，您可以使用括弧來表示金鑰，並執行簡單的指派，如下列範例所示：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

若要從字典取得值，請在括弧中指定索引鍵：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>使用參數呼叫方法

如您稍早在本文中所見，使用進行程式設計的物件有方法。 例如，`Database` 物件可能會有 `Database.Connect` 的方法。 許多方法也有一或多個參數。 *參數*是您傳遞給方法的值，可讓方法完成其工作。 例如，查看 `Request.MapPath` 方法的宣告，其採用三個參數：

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

這個方法會傳回伺服器上對應至指定虛擬路徑的實體路徑。 方法的三個參數是 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。 （請注意，在宣告中，參數會列出其接受的資料類型）。當您呼叫這個方法時，您必須提供所有三個參數的值。

當您使用 Razor 語法的 Visual Basic 時，您有兩個選項可將參數傳遞給方法：*位置參數*或*具名引數*。 若要使用位置參數呼叫方法，請以方法宣告中指定的嚴格順序來傳遞參數。 （您通常會藉由閱讀方法的檔來得知此順序）。您必須遵循順序，而且不能在必要時略過任何&#8212;參數，您可以傳遞空字串（`""`），或為沒有值的位置參數傳遞 null。

下列範例假設您的網站上有一個名為 [*腳本*] 的資料夾。 程式碼會呼叫 `Request.MapPath` 方法，並以正確的順序傳遞三個參數的值。 然後，它會顯示所產生的對應路徑。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

當方法有許多參數時，您可以使用具名引數，讓您的程式碼更簡潔且更容易閱讀。 若要使用具名引數來呼叫方法，請指定參數名稱，後面接著 `:=`，然後提供值。 具名引數的優點是您可以依照任何想要的順序來新增它們。 （缺點是方法呼叫不是精簡的）。

下列範例會呼叫與上述相同的方法，但會使用具名引數來提供值：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

如您所見，參數會以不同的順序傳遞。 不過，如果您執行上述範例和此範例，則會傳回相同的值。

## <a name="handling-errors"></a>處理錯誤

### <a name="try-catch-statements"></a>Try-catch 語句

您的程式碼中通常會有語句，可能會因為控制項以外的原因而失敗。 例如:

- 如果您的程式碼嘗試開啟、建立、讀取或寫入檔案，可能會發生各種錯誤。 您想要的檔案可能不存在、可能被鎖定、程式碼可能沒有許可權等等。
- 同樣地，如果您的程式碼嘗試更新資料庫中的記錄，可能會有許可權問題，可能會卸載與資料庫的連接、要儲存的資料可能無效等等。

在程式設計的詞彙中，這些情況稱為*例外*狀況。 如果您的程式碼遇到例外狀況，它會產生（擲回）一則錯誤訊息，也就是使用者的討厭程度最高。

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

在您的程式碼可能會遇到例外狀況的情況下，為了避免這種類型的錯誤訊息，您可以使用 `Try/Catch` 語句。 在 `Try` 語句中，您會執行您要檢查的程式碼。 在一或多個 `Catch` 語句中，您可以尋找可能發生的特定錯誤（特定類型的例外狀況）。 您可以視需要包含多個 `Catch` 語句，以尋找您預期的錯誤。

> [!NOTE]
> 我們建議您避免在 `Try/Catch` 語句中使用 `Response.Redirect` 方法，因為它可能會在您的頁面中造成例外狀況。

下列範例顯示的頁面會在第一個要求上建立文字檔，然後顯示一個按鈕，讓使用者開啟檔案。 此範例刻意使用錯誤的檔案名，因此會造成例外狀況。 此程式碼包含兩個可能例外狀況的 `Catch` 語句： `FileNotFoundException`，如果檔案名不正確，就會發生這種情況，如果 ASP.NET 找不到資料夾，就會發生 `DirectoryNotFoundException`。 （您可以將範例中的語句取消批註，以便在所有專案正常運作時查看其執行方式）。

如果您的程式碼未處理例外狀況，您會看到如先前螢幕擷取畫面所示的錯誤頁面。 不過，`Try/Catch` 區段有助於防止使用者看到這些類型的錯誤。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>其他資源

### <a name="reference-documentation"></a>參考文件

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic 語言](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
