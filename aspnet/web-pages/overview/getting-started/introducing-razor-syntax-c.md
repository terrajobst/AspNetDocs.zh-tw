---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: 使用 Razor 語法 ASP.NET Web 程式設計的簡介（C#） |Microsoft Docs
author: Rick-Anderson
description: 這一章可讓您大致瞭解如何使用 Razor 語法的 ASP.NET Web Pages 進行程式設計。 ASP.NET 是 Microsoft 用來執行動態 web pa 的技術 。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641572"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>使用 Razor 語法 ASP.NET Web 程式設計的簡介（C#）

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文可讓您瞭解如何使用 Razor 語法 ASP.NET Web Pages 進行程式設計。 ASP.NET 是 Microsoft 在網頁伺服器上執行動態網頁的技術。 這篇文章著重于使用C#程式設計語言。
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

## <a name="the-top-8-programming-tips"></a>前8個程式設計提示

本節列出當您使用 Razor 語法開始撰寫 ASP.NET 伺服器程式碼時，您絕對需要知道的幾個秘訣。

> [!NOTE]
> Razor 語法是以程式C#設計語言為基礎，這是最常用於 ASP.NET Web Pages 的語言。 不過，Razor 語法也支援 Visual Basic 語言，而且您看到的所有內容也可以在 Visual Basic 中執行。 如需詳細資訊，請參閱附錄[Visual Basic 語言和語法](https://go.microsoft.com/fwlink/?LinkId=202908)。

您稍後可以在本文中找到更多有關這些程式設計技巧的詳細資料。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. 使用 @ 字元將程式碼加入至頁面

`@` 字元會啟動內嵌運算式、單一語句區塊和多重語句區塊：

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

當頁面在瀏覽器中執行時，這就是這些語句的樣子：

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 編碼**
> 
> 當您使用 `@` 字元在頁面中顯示內容時（如上述範例所示），ASP.NET 會以 HTML 編碼輸出。 這會將保留的 HTML 字元（例如 `<` 和 `>` 和 `&`）取代為程式碼，讓字元在網頁中顯示為字元，而不是被轉譯為 HTML 標籤或實體。 如果沒有 HTML 編碼，來自您的伺服器程式碼的輸出可能無法正確顯示，而且可能會讓頁面暴露于安全性風險下。
> 
> 如果您的目標是要輸出將標記轉譯為標記的 HTML 標籤（例如 `<p></p>` 用於段落或 `<em></em>` 強調文字），請參閱本文稍後的在程式[代碼區塊中結合文字、標記和程式碼](#BM_CombiningTextMarkupAndCode)一節。
> 
> 您可以閱讀更多有關[使用表單](https://go.microsoft.com/fwlink/?LinkId=202892)的 HTML 編碼方式。

### <a name="2-you-enclose-code-blocks-in-braces"></a>2. 以大括弧括住程式碼區塊

程式*代碼區塊*包含一或多個程式碼語句，並以大括弧括住。

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

在瀏覽器中顯示的結果：

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3. 在區塊內，以分號結束每個程式碼語句

在程式碼區塊內，每個完整的程式碼語句都必須以分號結尾。 內嵌運算式的結尾不是分號。

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4. 您可以使用變數來儲存值

您可以將值儲存在*變數*中，包括字串、數位和日期等等。您可以使用 `var` 關鍵字來建立新的變數。 您可以使用 `@`，直接在頁面中插入變數值。

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

在瀏覽器中顯示的結果：

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 用雙引號括住常值字串

*字串*是視為文字的字元序列。 若要指定字串，請將其括在雙引號內：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

如果您想要顯示的字串包含反斜線字元（`\`）或雙引號（`"`），請使用前面加上 `@` 運算子的*逐字字串常*值。 （在C#中，\ 字元具有特殊意義，除非您使用逐字字串常值）。

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

若要內嵌雙引號，請使用逐字字串常值，並重複引號：

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

以下是在頁面中使用這兩個範例的結果：

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> 請注意，`@` 字元會用來標記中C#的逐字字串常值，並在 ASP.NET 網頁中標記程式碼。

### <a name="6-code-is-case-sensitive"></a>6. 程式碼區分大小寫

在C#中，關鍵字（例如 `var`、`true`和 `if`）和變數名稱會區分大小寫。 下列幾行程式碼會建立兩個不同的變數，`lastName` 和 `LastName.`

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

如果您將變數宣告為 `var lastName = "Smith";`，並嘗試在頁面中以 `@LastName`的形式參考該變數，您會得到 `"Jones"` 的值，而不是 `"Smith"`。

> [!NOTE]
> 在 Visual Basic 中，關鍵字和變數*不*區分大小寫。

### <a name="7-much-of-your-coding-involves-objects"></a>7. 您的程式碼大部分牽涉到物件

*物件*代表您可以使用&#8212;頁面、文字方塊、檔案、影像、web 要求、電子郵件訊息、客戶記錄（資料庫資料列）等進行程式設計的東西。物件具有描述其特性的屬性，而且您可以讀取或變更&#8212;文字方塊物件具有 `Text` 屬性（其中還有一個），要求物件具有 `Url` 屬性，電子郵件訊息具有 `From` 屬性，而 customer 物件則具有 `FirstName` 屬性。 物件也有 &quot;動詞&quot; 可以執行的方法。 範例包括 file 物件的 `Save` 方法、影像物件的 `Rotate` 方法，以及電子郵件物件的 `Send` 方法。

您通常會使用 `Request` 物件，這會提供頁面上文字方塊（表單欄位）的值、提出要求的瀏覽器類型、頁面的 URL、使用者身分識別等資訊。下列範例示範如何存取 `Request` 物件的屬性，以及如何呼叫 `Request` 物件的 `MapPath` 方法，這會提供您伺服器上頁面的絕對路徑：

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

在瀏覽器中顯示的結果：

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 您可以撰寫程式碼來做出決策

動態網頁的主要功能是，您可以根據條件來決定要執行的動作。 最常見的做法是使用 `if` 語句（和選擇性的 `else` 語句）。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

語句 `if(IsPost)` 是撰寫 `if(IsPost == true)`的簡寫方式。 除了 `if` 語句之外，還有各種不同的方法可以測試條件、重複的程式碼區塊等等，本文稍後會加以說明。

在瀏覽器中顯示的結果（按一下 [**提交**] 之後）：

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>HTTP GET 和 POST 方法和 IsPost 屬性
> 
> 網頁（HTTP）所使用的通訊協定支援非常有限的方法（動詞）數目，用來對伺服器提出要求。 最常見的兩個是 GET，用來讀取頁面和 POST （用來提交頁面）。 一般情況下，使用者第一次要求頁面時，會使用 GET 來要求頁面。 如果使用者填滿表單，然後按一下 [提交] 按鈕，則瀏覽器會對伺服器提出 POST 要求。
> 
> 在 web 程式設計中，知道頁面是否以 GET 或 POST 的方式要求，讓您知道如何處理頁面，通常會很有説明。 在 ASP.NET Web Pages 中，您可以使用 [`IsPost`] 屬性來查看要求是 GET 或 POST。 如果要求是 POST，`IsPost` 屬性會傳回 true，而您可以執行讀取表單上文字方塊值之類的動作。 您會看到的許多範例會告訴您如何根據 `IsPost`的值，以不同的方式處理頁面。

## <a name="a-simple-code-example"></a>簡單的程式碼範例

此程式說明如何建立說明基本程式設計技術的頁面。 在此範例中，您會建立可讓使用者輸入兩個數字的頁面，然後將其加入並顯示結果。

1. 在您的編輯器中，建立新的檔案，並將它命名為*AddNumbers*。
2. 將下列程式碼和標記複製到頁面中，並取代頁面中已存在的任何專案。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    以下是您要注意的一些事項：

    - `@` 字元會啟動頁面中第一個程式碼區塊，並在靠近頁面底部的 `totalMessage` 變數之前。
    - 頁面頂端的區塊會以大括弧括住。
    - 在頂端的區塊中，所有行的結尾都是分號。
    - `total`、`num1`、`num2`和 `totalMessage` 的變數會儲存數個數字和一個字串。
    - 指派給 `totalMessage` 變數的常值字串值是以雙引號括住。
    - 由於程式碼區分大小寫，因此當 `totalMessage` 變數使用接近頁面底部時，其名稱必須完全符合頂端的變數。
    - 運算式 `num1.AsInt() + num2.AsInt()` 顯示如何使用物件和方法。 每個變數上的 `AsInt` 方法會將使用者輸入的字串轉換成數位（整數），以便您在其上執行算數運算。
    - `<form>` 標記包含 `method="post"` 屬性。 這會指定當使用者按一下 [**新增**] 時，會使用 HTTP POST 方法將頁面傳送至伺服器。 提交頁面時，`if(IsPost)` 測試會評估為 true，且會執行條件式程式碼，以顯示加入數位的結果。
3. 儲存頁面，並在瀏覽器中執行。 （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）輸入兩個整數，然後按一下 [**新增**] 按鈕。 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>基本程式設計概念

本文提供 ASP.NET web 程式設計的總覽。 這不是詳盡的檢查，只要快速導覽一下您最常使用的程式設計概念即可。 就算如此，它還涵蓋了您開始使用 ASP.NET Web Pages 所需的幾乎所有專案。

但首先，有點的技術背景。

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Razor 語法、伺服器程式碼和 ASP.NET

Razor 語法是簡單的程式設計語法，用於在網頁中內嵌以伺服器為基礎的程式碼。 在使用 Razor 語法的網頁中，有兩種內容：用戶端內容和伺服器程式碼。 用戶端內容是您在網頁中使用的專案： HTML 標籤（元素）、樣式資訊（例如 CSS）可能是某些用戶端腳本，例如 JavaScript 和純文字。

Razor 語法可讓您將伺服器程式碼新增到此用戶端內容。 如果頁面中有伺服器程式碼，伺服器會先執行該程式碼，然後再將頁面傳送至瀏覽器。 藉由在伺服器上執行，程式碼可以執行工作，使其更複雜，只使用用戶端內容，例如存取以伺服器為基礎的資料庫。 最重要的是，伺服器程式碼可以動態&#8212;建立用戶端內容，它可以即時產生 HTML 標籤或其他內容，然後將它連同頁面可能包含的任何靜態 HTML 傳送到瀏覽器。 從瀏覽器的觀點來看，您的伺服器程式碼所產生的用戶端內容與其他用戶端內容並無不同。 如您已見過，所需的伺服器程式碼相當簡單。

包含 Razor 語法的 ASP.NET 網頁具有特殊的副檔名（*cshtml*或*vbhtml*）。 伺服器會辨識這些擴充功能、執行標記為 Razor 語法的程式碼，然後將頁面傳送至瀏覽器。

### <a name="where-does-aspnet-fit-in"></a>ASP.NET 適用於何處？

Razor 語法是以 Microsoft 的技術為基礎，稱為 ASP.NET，也就是以 Microsoft .NET Framework 為基礎。 The.NET Framework 是一個龐大的完整程式設計架構，可供 Microsoft 開發幾乎任何類型的電腦應用程式。 ASP.NET 是專為建立 web 應用程式而設計的 .NET Framework 部分。 開發人員使用 ASP.NET，在世界各地建立許多最大且最高的流量網站。 （當您在網站中的 URL 中看到副檔名為 *.aspx*時，您會知道網站是以 ASP.NET 撰寫的）。

Razor 語法為您提供 ASP.NET 的所有威力，但使用簡化的語法，如果您是新手，就能更輕鬆地學習，如果您是專家，也能讓您更具生產力。 雖然此語法很容易使用，它與 ASP.NET 的系列關係和 .NET Framework 表示當您的網站變得更精密時，您可以使用較大的架構。

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **類別和實例**
> 
> ASP.NET 伺服器程式碼會使用物件，而這些物件則是以類別的概念為基礎。 類別是物件的定義或範本。 例如，應用程式可能會包含一個 `Customer` 類別，以定義任何客戶物件所需的屬性和方法。
> 
> 當應用程式需要處理實際的客戶資訊時，它會建立一個（或具現*化*） customer 物件的實例。 每一位客戶都是 `Customer` 類別的個別實例。 每個實例都支援相同的屬性和方法，但每個實例的屬性值通常不同，因為每個客戶物件都是唯一的。 在一個客戶物件中，`LastName` 屬性可能是 "Smith";在另一個客戶物件中，`LastName` 屬性可能是「張」。
> 
> 同樣地，您網站中的任何個別網頁都是 `Page` 物件，這是 `Page` 類別的實例。 頁面上的按鈕是 `Button` 物件，它是 `Button` 類別的實例，依此類推。 每個實例都有自己的特性，但它們都是以物件的類別定義中指定的內容為基礎。

## <a name="basic-syntax"></a>基本語法

稍早您會看到如何建立 ASP.NET Web Pages 頁面的基本範例，以及如何將伺服器程式碼加入至 HTML 標籤。 在這裡，您將瞭解使用 Razor 語法&#8212; （也就是程式設計語言規則）撰寫 ASP.NET 伺服器程式碼的基本概念。

如果您對程式設計有經驗（特別是使用 C、 C++、 C#、Visual Basic 或 JavaScript），您在這裡閱讀的大部分內容都很熟悉。 您可能只需要熟悉如何將伺服器程式碼加入至*cshtml*檔案中的標記。

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>結合程式碼區塊中的文字、標記和程式碼

在 [伺服器程式碼區塊] 中，您通常會想要將文字或標記（或兩者）輸出至頁面。 如果伺服器程式碼區塊包含不是程式碼的文字，而應該改為轉譯，則 ASP.NET 必須能夠區別該文字與程式碼。 有數個方式可以執行此動作。

- 將文字括在 HTML 元素中，例如 `<p></p>` 或 `<em></em>`：   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    HTML 元素可以包含文字、其他 HTML 專案和伺服器程式碼運算式。 當 ASP.NET 看到開頭的 HTML 標籤（例如 `<p>`）時，它會將專案及其內容在內的一切轉譯為瀏覽器，並在伺服器程式碼運算式發生時加以解析。
- 請使用 `@:` 運算子或 `<text>` 元素。 `@:` 輸出包含純文字或不相符 HTML 標籤的單一行內容;`<text>` 元素會將多行括住以輸出。 當您不想要將 HTML 元素轉譯為輸出的一部分時，這些選項會很有用。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    如果您想要輸出多行文字或不相符的 HTML 標籤，您可以在每一行前面加上 `@:`，或者將該行括在 `<text>` 元素中。 就像 `@:` 運算子一樣，ASP.NET 會使用`<text>` 標記來識別文字內容，而且永遠不會呈現在頁面輸出中。

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    第一個範例會重複上一個範例，但會使用一對 `<text>` 標記來括住要轉譯的文字。 在第二個範例中，`<text>` 和 `</text>` 標記會括住三行，其中所有的程式碼都有一些非內含性文字和不相符的 HTML 標籤（`<br />`），以及伺服器程式碼和相符的 HTML 標籤。 同樣地，您也可以分別在每一行的前面加上 `@:` 運算子;任一種方法都可行。

    > [!NOTE]
    > 當您&#8212;使用 HTML 專案（如本節所示）輸出文字時，`@:` 運算子或 `<text>` 元素&#8212; ASP.NET 不會對輸出進行 HTML 編碼。 （如先前所述，ASP.NET 會對前面加上 `@`的伺服器程式碼運算式和伺服器程式碼區塊的輸出進行編碼，但本節中所述的特殊情況除外）。

### <a name="whitespace"></a>Whitespace

語句（和字串常值外部）中的額外空格不會影響語句：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

語句中的分行符號不會影響語句，而且您可以包裝語句以方便閱讀。 下列陳述式是相同的：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

不過，您無法在字串常值的中間換行。 下列範例無法使用：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

若要結合一個長字串，以包裝到多行（如上述程式碼），有兩個選項。 您可以使用串連運算子（`+`），這會在本文稍後看到。 您也可以使用 `@` 字元來建立逐字字串常值，如您稍早在本文中所見。 您可以跨行中斷逐字字串常值：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>程式碼（和標記）批註

批註可讓您為自己或其他人留下筆記。 它們也可讓您停用（*批註*）您不想執行的程式碼或標記區段，但想要保留在頁面中的時間。

Razor 程式碼和 HTML 標籤有不同的批註語法。 就像所有的 Razor 程式碼一樣，在頁面傳送至瀏覽器之前，會先處理 Razor 批註，然後再將其移除。 因此，Razor 批註語法可讓您將批註放入程式碼中（甚至是標記），您可以在編輯檔案時看到，但即使在頁面原始檔中，也不會看到該使用者。

針對 ASP.NET Razor 批註，您可以使用 `@*` 開始批註，並以 `*@`結束。 批註可以位於一行或多行：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

以下是程式碼區塊中的批註：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

以下是相同的程式碼區塊，並將程式程式碼標記為批註，使其不會執行：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

在程式碼區塊內，做為使用 Razor 批註語法的替代方法，您可以使用您所使用之程式設計語言的批註語法， C#例如：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

在C#中，單行批註的前面會加上 `//` 個字元，而多行批註則以 `/*` 開頭，並以 `*/`結尾。 （如同 Razor 批註， C#批註不會轉譯至瀏覽器）。

針對標記，您可能已經知道，您可以建立 HTML 批註：

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

HTML 批註的開頭為 `<!--` 個字元，並以 `-->`結尾。 您可以使用 HTML 批註來括住文字，但您可能會想要保留在頁面中，但不想呈現的任何 HTML 標籤。 此 HTML 批註會隱藏標記的全部內容及其包含的文字：

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

不同于 Razor 批註，HTML 批註*會*轉譯成頁面，使用者可以藉由查看頁面來源來查看它們。

Razor 在的C#嵌套區塊上有限制。 如需詳細資訊[， C#請參閱命名變數和嵌套區塊產生中斷](http://aspnetwebstack.codeplex.com/workitem/1914)的程式碼

## <a name="variables"></a>變數

變數是您用來儲存資料的已命名物件。 您可以將變數命名為任何名稱，但名稱必須以字母字元開頭，而且不能包含空格或保留字元。

### <a name="variables-and-data-types"></a>變數和資料類型

變數可以具有特定的資料類型，以指出變數中儲存的資料種類。 您可以擁有儲存字串值的字串變數（例如 &quot;Hello world&quot;）、儲存整數值（例如3或79）的整數變數，以及以各種格式（例如4/12/2012 或3月2009）儲存日期值的日期變數。 而且還有許多其他資料類型可供您使用。

不過，您通常不需要指定變數的類型。 大部分的情況下，ASP.NET 都可以根據變數中的資料使用方式來找出型別。 （有時候您必須指定類型，您將會看到這是 true 的範例）。

您可以使用 `var` 關鍵字（如果您不想指定類型）或使用類型的名稱來宣告變數：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

下列範例顯示網頁中變數的一些一般用法：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

如果您在頁面中結合前面的範例，您會看到這會顯示在瀏覽器中：

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>轉換和測試資料類型

雖然 ASP.NET 通常可以自動判斷資料類型，但有時卻不能。 因此，您可能需要執行明確轉換來協助 ASP.NET。 即使您不需要轉換類型，有時還是可以測試以查看您可能使用的資料類型。

最常見的情況是，您必須將字串轉換成另一種類型，例如整數或日期。 下列範例顯示您必須將字串轉換成數位的一般情況。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

就規則而言，使用者輸入會以字串的形式提供給您。 即使您已提示使用者輸入數位，而且即使他們輸入了數位，當使用者輸入提交，而且您在程式碼中讀取時，資料仍會是字串格式。 因此，您必須將字串轉換成數位。 在此範例中，如果您嘗試對值執行算術而不加以轉換，則會產生下列錯誤，因為 ASP.NET 無法加入兩個字串：

*無法將類型 ' string ' 隱含轉換為 ' int '。*

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
    將代表整數（例如 "593"）的字串轉換為整數。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
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
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>運算子

「運算子」是一個關鍵字或字元，告訴 ASP.NET 要在運算式中執行哪一種命令。 C#語言（以及以它為基礎的 Razor 語法）支援許多運算子，但您只需要辨識幾個，即可開始使用。 下表摘要說明最常見的運算子。

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
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    數值運算式中使用的數學運算子。
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    指派。 將語句右邊的值指派給左邊的物件。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    相等。 如果值相等，則傳回 `true`。 （請注意 `=` 運算子和 `==` 運算子之間的區別）。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    不等。 如果值不相等，則傳回 `true`。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    小於、大於、小於或等於，且大於或等於的情況下。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    串連，用來聯結字串。 ASP.NET 會根據運算式的資料類型，知道這個運算子和加號之間的差異。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    遞增和遞減運算子，會從變數相加和減去1（分別為）。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    後. 用來將運算式分組，並將參數傳遞給方法。
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    內. 用來存取陣列或集合中的值。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    並非. 將 `true` 值反轉為 `false`，反之亦然。 通常用來做為測試 `false` 的簡短方式（也就是不 `true`）。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    邏輯 AND 和 OR，用來將條件連結在一起。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
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

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>參考虛擬根目錄： ~ 運算子和 Href 方法

在*cshtml*或*vbhtml*檔案中，您可以使用 `~` 運算子來參考虛擬根路徑。 這非常方便，因為您可以在網站中移動頁面，而其包含的任何連結也不會中斷。 如果您將網站移至不同的位置，這也很方便。 以下是一些範例：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

如果網站 `http://myserver/myapp`，以下是當頁面執行時，ASP.NET 會如何處理這些路徑：

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

（您實際上不會看到這些路徑做為變數的值，但是 ASP.NET 會將這些路徑視為其本身）。

您可以在伺服器程式碼（如上）和標記中使用 `~` 運算子，如下所示：

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

在標記中，您可以使用 `~` 運算子來建立資源的路徑，例如影像檔、其他網頁和 CSS 檔案。 當頁面執行時，ASP.NET 會查看頁面（程式碼和標記），並將所有 `~` 參考解析為適當的路徑。

## <a name="conditional-logic-and-loops"></a>條件式邏輯和迴圈

ASP.NET 伺服器程式碼可讓您根據條件執行工作，並撰寫會重複語句的程式碼特定次數（也就是執行迴圈的程式碼）。

### <a name="testing-conditions"></a>測試條件

若要測試簡單的條件，請使用 `if` 語句，這會根據您指定的測試傳回 true 或 false：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

`if` 關鍵字會啟動區塊。 實際測試（條件）在括弧中，並傳回 true 或 false。 如果測試為 true，則執行的語句會以大括弧括住。 `if` 語句可以包含 `else` 區塊，指定當條件為 false 時要執行的語句：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

您可以使用 `else if` 區塊來新增多個條件：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

在此範例中，如果 if 區塊中的第一個條件不是 true，則會核取 [`else if`] 條件。 如果符合該條件，就會執行 `else if` 區塊中的語句。 如果沒有符合任何條件，則會執行 `else` 區塊中的語句。 您可以新增任意數目的 if 區塊，然後以 `else` 區塊關閉，因為 &quot;所有其他專案&quot; 條件。

若要測試大量的條件，請使用 `switch` 組塊：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

要測試的值是以括弧括住（在範例中為 `weekday` 變數）。 每個個別測試都會使用以冒號（:) 結尾的 `case` 語句。 如果 `case` 語句的值符合測試值，則會執行該案例區塊中的程式碼。 您可以使用 `break` 語句來關閉每個 case 語句。 （如果您忘了在每個 `case` 區塊中包含 break，則下一個 `case` 語句的程式碼也會執行）。`switch` 區塊通常會有 `default` 的語句做為 &quot;所有其他情況的&quot; 選項（如果沒有其他情況成立）。

在瀏覽器中顯示的最後兩個條件式區塊的結果：

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>迴圈程式碼

您通常需要重複執行相同的語句。 您可以藉由迴圈來完成這項操作。 例如，您通常會針對資料集合中的每個專案執行相同的語句。 如果您確切知道您想要迴圈的次數，可以使用 `for` 迴圈。 這種迴圈特別適合用來計算或計數：

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

迴圈會以 `for` 關鍵字開頭，後面接著以括弧括住的三個語句，每個都以分號結束。

- 在括弧內，第一個語句（`var i=10;`）會建立一個計數器，並將它初始化為10個。 您不需要將計數器命名 `i` &#8212;您可以使用任何變數。 當 `for` 迴圈執行時，計數器會自動遞增。
- 第二個語句（`i < 21;`）會設定您想要計算的距離條件。 在此情況下，您想要將它移到最多20個（也就是，在計數器小於21時繼續進行）。
- 第三個語句（`i++`）使用遞增運算子，這只會指定在每次執行迴圈時，計數器應該加入1。

括弧內的程式碼會針對迴圈的每個反復專案執行。 標記會每次建立新的段落（`<p>` 元素），並在輸出中加入一行，顯示 `i` （計數器）的值。 當您執行此頁面時，此範例會建立顯示輸出的11行，而每一行中的文字會指出專案編號。

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

如果您使用的是集合或陣列，通常會使用 `foreach` 迴圈。 集合是一組類似的物件，而 `foreach` 迴圈可讓您在集合中的每個專案上執行工作。 這種類型的迴圈對集合很方便，因為與 `for` 迴圈不同的是，您不需要遞增計數器或設定限制。 相反地，`foreach` 迴圈程式碼只會繼續完成集合，直到完成為止。

例如，下列程式碼會傳回 `Request.ServerVariables` 集合中的專案，這是包含您的 web 伺服器相關資訊的物件。 它會使用 `foreac` h 迴圈來顯示每個專案的名稱，方法是在 HTML 項目符號清單中建立新的 `<li>` 元素。

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

`foreach` 關鍵字後面加上括弧，您可以在其中宣告代表集合中單一專案的變數（在範例中，`var item`），後面接著 `in` 關鍵字，後面接著您要迴圈執行的集合。 在 `foreach` 迴圈的主體中，您可以使用先前宣告的變數來存取目前的專案。

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

若要建立更一般用途的迴圈，請使用 `while` 語句：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

`while` 迴圈是以 `while` 關鍵字開頭，後面接著括弧，您可以在其中指定迴圈繼續的時間（在這裡，只要 `countNum` 小於50），就會重複區塊。 迴圈通常會遞增（加入）或遞減（減去）用來計算的變數或物件。 在此範例中，`+=` 運算子會在每次執行迴圈時，將1新增至 `countNum`。 （若要遞減迴圈中計數的變數，您可以使用遞減運算子 `-=`）。

## <a name="objects-and-collections"></a>物件和集合

ASP.NET 網站中幾乎所有內容都是物件，包括網頁本身。 本節討論您在程式碼中經常使用的一些重要物件。

### <a name="page-objects"></a>頁面物件

ASP.NET 中最基本的物件是頁面。 您可以直接存取頁面物件的屬性，而不需要任何限定的物件。 下列程式碼會使用頁面的 `Request` 物件，取得頁面的檔案路徑：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

若要清楚指出您是在目前頁面物件上參考屬性和方法，您可以選擇性地使用關鍵字 `this` 來代表程式碼中的頁面物件。 以下是先前的程式碼範例，加上 `this` 以代表該頁面：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

您可以使用 `Page` 物件的屬性來取得大量資訊，例如：

- `Request` 如您所見，這是目前要求的相關資訊集合，包括提出要求的瀏覽器類型、頁面的 URL、使用者身分識別等。
- `Response` 這是在伺服器程式碼完成執行時，將會傳送至瀏覽器的回應（頁面）相關資訊集合。 例如，您可以使用這個屬性將資訊寫入至回應。 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>集合物件（陣列和字典）

*集合*是一組相同類型的物件，例如從資料庫 `Customer` 物件的集合。 ASP.NET 包含許多內建集合，例如 `Request.Files` 集合。

您通常會使用集合中的資料。 有兩個常見的集合類型是*陣列*和*字典*。 當您想要儲存類似專案的集合，但不想要建立個別的變數來保存每個專案時，陣列會很有用：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

使用陣列，您可以宣告特定的資料類型，例如 `string`、`int`或 `DateTime`。 若要指出變數可以包含陣列，您可以在宣告中加上括弧（例如 `string[]` 或 `int[]`）。 您可以使用物件的位置（索引），或使用 `foreach` 語句來存取陣列中的專案。 陣列索引以零&#8212;為起始，亦即，第一個專案位於位置0，第二個專案位於位置1，依此類推。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

您可以藉由取得 `Length` 屬性來判斷陣列中的專案數。 若要取得陣列中特定專案的位置（以搜尋陣列），請使用 `Array.IndexOf` 方法。 您也可以執行一些動作，像是反轉陣列的內容（`Array.Reverse` 方法）或排序內容（`Array.Sort` 方法）。

在瀏覽器中顯示的字串陣列程式碼輸出：

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

字典是索引鍵/值組的集合，您可以在其中提供用來設定或抓取對應值的索引鍵（或名稱）：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

若要建立字典，您可以使用 `new` 關鍵字來表示您要建立新的字典物件。 您可以使用 `var` 關鍵字，將字典指派給變數。 您可以使用角括弧（`< >`）來指示字典中專案的資料類型。 在宣告的結尾，您必須加入一對括弧，因為這實際上是建立新字典的方法。

若要將專案加入至字典，您可以呼叫 dictionary 變數的 `Add` 方法（在此案例中為`myScores`），然後指定索引鍵和值。 或者，您可以使用方括弧來表示金鑰，並執行簡單的指派，如下列範例所示：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

若要從字典取得值，請在括弧中指定索引鍵：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>使用參數呼叫方法

如您稍早在本文中所閱讀，使用進行程式設計的物件可以有方法。 例如，`Database` 物件可能會有 `Database.Connect` 的方法。 許多方法也有一或多個參數。 *參數*是您傳遞給方法的值，可讓方法完成其工作。 例如，查看 `Request.MapPath` 方法的宣告，其採用三個參數：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

（這一行已包裝，使其更容易閱讀。 請記住，除了括在引號中的字串之外，您幾乎可以在任何地方放置分行符號）。

這個方法會傳回伺服器上對應至指定虛擬路徑的實體路徑。 方法的三個參數是 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。 （請注意，在宣告中，參數會列出其接受的資料類型）。當您呼叫這個方法時，您必須提供所有三個參數的值。

Razor 語法提供兩個選項，讓您將參數傳遞給方法：*位置參數*和*具名引數*。 若要使用位置參數呼叫方法，請以方法宣告中指定的嚴格順序來傳遞參數。 （您通常會藉由閱讀方法的檔來得知此順序）。您必須遵循順序，而且如果有必要，就無法略過&#8212;任何參數，您可以為沒有值的位置參數傳遞空字串（`""`）或 `null`。

下列範例假設您的網站上有一個名為 [*腳本*] 的資料夾。 程式碼會呼叫 `Request.MapPath` 方法，並以正確的順序傳遞三個參數的值。 然後，它會顯示所產生的對應路徑。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

當方法有許多參數時，您可以使用具名引數，讓您的程式碼更容易閱讀。 若要使用具名引數來呼叫方法，請指定參數名稱，後面接著冒號（:)，然後是值。 具名引數的優點是您可以依照您想要的任何順序傳遞它們。 （缺點是方法呼叫不是精簡的）。

下列範例會呼叫與上述相同的方法，但會使用具名引數來提供值：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

如您所見，參數會以不同的順序傳遞。 不過，如果您執行上述範例和此範例，則會傳回相同的值。

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>處理錯誤

### <a name="try-catch-statements"></a>Try-catch 語句

您的程式碼中通常會有語句，可能會因為控制項以外的原因而失敗。 例如:

- 如果您的程式碼嘗試建立或存取檔案，可能會發生各種錯誤。 您想要的檔案可能不存在、可能被鎖定、程式碼可能沒有許可權等等。
- 同樣地，如果您的程式碼嘗試更新資料庫中的記錄，可能會有許可權問題，可能會卸載與資料庫的連接、要儲存的資料可能無效等等。

在程式設計的詞彙中，這些情況稱為*例外*狀況。 如果您的程式碼遇到例外狀況，它會產生（擲回）一則錯誤訊息，其中最棒的是使用者很討厭：

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

在您的程式碼可能會遇到例外狀況的情況下，為了避免這種類型的錯誤訊息，您可以使用 `try/catch` 語句。 在 `try` 語句中，您會執行您要檢查的程式碼。 在一或多個 `catch` 語句中，您可以尋找可能發生的特定錯誤（特定類型的例外狀況）。 您可以視需要包含多個 `catch` 語句，以尋找您預期的錯誤。

> [!NOTE]
> 我們建議您避免在 `try/catch` 語句中使用 `Response.Redirect` 方法，因為它可能會在您的頁面中造成例外狀況。

下列範例顯示的頁面會在第一個要求上建立文字檔，然後顯示一個按鈕，讓使用者開啟檔案。 此範例刻意使用錯誤的檔案名，因此會造成例外狀況。 此程式碼包含兩個可能例外狀況的 `catch` 語句： `FileNotFoundException`，如果檔案名不正確，就會發生這種情況，如果 ASP.NET 找不到資料夾，就會發生 `DirectoryNotFoundException`。 （您可以將範例中的語句取消批註，以便在所有專案正常運作時查看其執行方式）。

如果您的程式碼未處理例外狀況，您會看到如先前螢幕擷取畫面所示的錯誤頁面。 不過，`try/catch` 區段有助於防止使用者看到這些類型的錯誤。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>其他資源

**使用 Visual Basic 進行程式設計**

[附錄： Visual Basic 語言和語法](https://go.microsoft.com/fwlink/?LinkId=202908)

**參考文件**

[ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)

[C#語言](https://msdn.microsoft.com/library/kx37x362.aspx)
