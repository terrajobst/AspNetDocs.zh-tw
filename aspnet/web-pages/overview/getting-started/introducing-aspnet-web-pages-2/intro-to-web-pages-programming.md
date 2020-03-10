---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: ASP.NET Web Pages 程式設計基本概念簡介 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程可讓您瞭解如何使用 Razor 語法在 ASP.NET Web Pages 中進行程式設計。 您將瞭解的內容：您用於 pr 的基本 ' Razor ' 語法 。
ms.author: riande
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 474de7671ac2931e5ba9ff635d77385403644521
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628475"
---
# <a name="introducing-aspnet-web-pages---programming-basics"></a>ASP.NET Web Pages 程式設計基本概念簡介

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程可讓您瞭解如何使用 Razor 語法在 ASP.NET Web Pages 中進行程式設計。
> 
> 您將學到什麼：
> 
> - 您在 ASP.NET Web Pages 中用來進行程式設計的基本 "Razor" 語法。
> - 一些基本C#，這是您將使用的程式設計語言。
> - Web Pages 的一些基本程式設計概念。
> - 如何安裝套件（包含預建程式碼的元件）以搭配您的網站使用。
> - 如何使用 helper 來執行*一般的程式*設計工作。
>   
> 
> 討論的功能/技術：
> 
> - NuGet 和套件管理員。
> - `Gravatar` helper。

本教學課程主要是介紹您將用於 ASP.NET Web Pages 的程式設計語法。 您將瞭解以程式C#設計語言撰寫的 Razor 語法和程式碼。 在上一個教學課程中，您已經大致瞭解此語法;在本教學課程中，我們將詳細說明語法。

我們保證本教學課程牽涉到您會在單一教學課程中看到的大部分程式設計，而這是唯一*僅*適用于程式設計的教學課程。 在此集合的其餘教學課程中，您將會建立可執行有趣事項的頁面。

您也*會瞭解協助程式。* 協助程式是一種元件，也就是封裝的程式碼，您可以將它加入至頁面。 Helper 會為您執行工作，否則可能會單調乏味或複雜。

## <a name="creating-a-page-to-play-with-razor"></a>建立要使用 Razor 播放的頁面

在本節中，您將使用 Razor 來玩，讓您可以瞭解基本語法。

如果尚未執行，請啟動 WebMatrix。 您將會使用您在上一個教學課程中建立的網站（[消費者入門網頁](https://go.microsoft.com/fwlink/?LinkId=251578)）。 若要重新開啟，請按一下 [**我的網站**]，然後選擇 [ **WebPageMovies**]：

![WebMatrix 開始畫面，顯示 [開啟網站] 選項和 [我的網站] 反白顯示](intro-to-web-pages-programming/_static/image1.png)

選取 [**檔案**] 工作區。

在功能區中，按一下 [**新增**] 以建立頁面。 選取 [ **CSHTML** ]，並將新頁面命名為*TestRazor*。

按一下 [確定]。

將下列內容複寫到檔案中，並完全取代已存在的檔案。

> [!NOTE]
> 當您將範例中的程式碼或標記複製到頁面時，縮排和對齊可能不會與教學課程中的相同。 不過，縮排和對齊不會影響程式碼的執行方式。

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>檢查範例頁面

您所看到的大部分都是一般 HTML。 不過，在頂端會有此程式碼區塊：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

請注意下列關於此程式碼區塊的事項：

- @ 字元會告訴 ASP.NET，以下是 Razor 程式碼，而不是 HTML。 ASP.NET 會將 @ 字元之後的所有內容視為程式碼，直到它再次執行到某些 HTML。 （在此案例中，這是 &lt;！DOCTYPE&gt; 元素。
- 如果程式碼有多行，則大括弧（{和}）會括住 Razor 程式碼區塊。 大括弧會告訴 ASP.NET，該區塊的程式碼會在此處開始和結束。
- 字元會標示批註，也就是不會執行的程式碼的一部分。
- 每個語句的結尾都必須是分號（;)。 （不過，這不是批註）。
- 您可以將值儲存在*變數*中，您會使用關鍵字 var 來*建立（宣告*）。 當您建立變數時，您可以指定名稱，其中可以包含字母、數位和底線（\_）。 變數名稱不能以數位開頭，也不能使用程式設計關鍵字的名稱（例如 var）。
- 您可以用引號括住字元字串（例如 "ASP.NET" 和 "Web Pages"）。 （必須以雙引號括住）。數位不是括在引號中。
- 引號外的空白並不重要。 分行符號大多不重要;例外狀況是您無法跨行分割引號中的字串。 縮排和對齊並不重要。

這個範例不明顯的事情是，所有程式碼都區分大小寫。 這表示變數 TheSum 的變數，與可能名為 theSum 或 TheSum 的變數不同。 同樣地，var 是關鍵字，但 Var 則不是。

### <a name="objects-and-properties-and-methods"></a>物件和屬性和方法

接著是運算式日期時間。現在。 簡單來說，DateTime 是一個*物件*。 物件是您可以用來進行程式設計的專案，包括頁面、文字方塊、檔案、影像、web 要求、電子郵件訊息、客戶記錄等等。物件具有一或多個描述其特性的*屬性*。 一個文字方塊物件有一個 Text 屬性（還有一些），一個 request 物件有一個 Url 屬性（還有其他），一個電子郵件訊息具有 From 屬性和 To 屬性等等。 物件也有可執行檔「動詞」*方法*。 您將會很多使用物件。

如您在範例中所見，DateTime 是一個可讓您編寫日期和時間的物件。 它有一個名稱為 Now 的屬性，它會傳回目前的日期和時間。

### <a name="using-code-to-render-markup-in-the-page"></a>使用程式碼在頁面中呈現標記

在頁面主體中，請注意下列事項：

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

同樣地，@ 字元會告訴 ASP.NET，接下來是程式碼，而不是 HTML。 在標記中，您可以新增 @，後面接著程式碼運算式，而 ASP.NET 會在該時間點直接呈現該運算式的值。 在此範例中，@a 將會轉譯值為的變數，@product 呈現名為 product 的變數中的任何內容，依此類推。

不過，您並不限於變數。 在這裡的幾個實例中，@ 字元會在運算式之前：

- @ （a\*b）會呈現變數 a 和 b 中任何內容的乘積。 （\* 運算子表示乘法）。
- @ （技術 + "" + product）會在串連變數技術和產品後呈現這些值，並在其間加上空格。 串連字號串的運算子（+）與用於加入數位的運算子相同。 ASP.NET 通常會指出您是使用數位或字串，並使用 + 運算子進行正確的作業。
- @Request.Url 呈現 Request 物件的 Url 屬性。 Request 物件包含來自瀏覽器的目前要求的相關資訊，而 Url 屬性則包含該目前要求的 URL。

這個範例也是設計來說明您可以用不同的方式來執行工作。 您可以在頂端的程式碼區塊中執行計算，將結果放入變數中，然後在標記中轉譯變數。 或者，您也可以在標記的運算式中執行計算。 您所使用的方法取決於您所執行的動作，以及您自己的喜好設定。

### <a name="seeing-the-code-in-action"></a>查看動作中的程式碼

以滑鼠右鍵按一下檔案名，然後選擇 [**在瀏覽器中啟動**]。 您會在瀏覽器中看到頁面中已解決的所有值和運算式。

![在瀏覽器中執行的 ' TestRazor ' 頁面](intro-to-web-pages-programming/_static/image2.png)

查看瀏覽器中的來源。

![瀏覽器中的 [測試 Razor] 頁面來源](intro-to-web-pages-programming/_static/image3.png)

就像您在上一個教學課程中所預期的經驗，此頁面中沒有任何 Razor 程式碼。 您看到的只是實際的顯示值。 當您執行頁面時，實際上是對內建于 WebMatrix 的網頁伺服器提出要求。 收到要求時，ASP.NET 會解析所有值和運算式，並將其值轉譯成頁面。 然後，它會將頁面傳送至瀏覽器。

> [!TIP] 
> 
> **Razor 和C#**
> 
> 到目前為止，我們已說過您正在使用 Razor 語法。 沒錯，但這並不是完整的故事。 您所使用的實際程式設計語言稱為*C#* 。 C#這是 Microsoft 在十年前所建立的，而且已經成為建立 Windows 應用程式的主要程式設計語言之一。 您已瞭解如何為變數命名的所有規則，以及如何建立語句等等，實際上是C#語言的所有規則。
> 
> Razor 會特別針對您將此程式碼內嵌至頁面的一小部分慣例，更明確地參考。 例如，使用 @ 標記頁面中的程式碼，以及使用 @ {} 來內嵌程式碼區塊的慣例，是頁面的 Razor 層面。 協助程式也會被視為 Razor 的一部分。 Razor 語法在多個位置使用，而不只是 ASP.NET Web Pages。 （例如，它也用於 ASP.NET MVC views）。
> 
> 我們提過這是因為如果您尋找程式設計 ASP.NET Web Pages 的相關資訊，就會發現 Razor 的許多參考。 不過，其中有許多參考並不適用于您所做的事，因此可能會造成混淆。 事實上，許多程式設計問題都是關於使用C#或使用 ASP.NET。 因此，如果您特別瞭解 Razor 的相關資訊，可能就找不到所需的解答。

## <a name="adding-some-conditional-logic"></a>新增一些條件式邏輯

在頁面中使用程式碼的其中一個絕佳功能，就是您可以根據各種條件來變更會發生的情況。 在本教學課程的這個部分中，您將使用一些方式來變更頁面中顯示的內容。

這個範例很簡單，而且有點假設，讓我們可以專注于條件式邏輯。 您將建立的頁面將會執行下列動作：

- 根據網頁是否為第一次顯示頁面，或您是否已按下按鈕來提交頁面，在頁面上顯示不同的文字。 這會是第一個條件式測試。
- 只有在 URL 的查詢字串中傳遞特定值（HTTP：//...？ show = true）時，才顯示訊息。 這會是第二個條件式測試。

在 WebMatrix 中建立頁面，並將它命名為*TestRazorPart2*。 （在功能區中，按一下 [**新增**]，選擇 [ **CSHTML**]，為檔案命名，然後按一下 **[確定]** ）。

將該頁面的內容取代為下列內容：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

頂端的程式碼區塊會使用一些文字，將名為 message 的變數初始化。 在頁面主體中，訊息變數的內容會顯示在 &lt;p&gt; 元素內。 標記也會包含 &lt;輸入&gt; 元素，以建立**提交**按鈕。

執行頁面以查看其目前的運作方式。 現在，它基本上是靜態頁面，即使您按一下 [**提交**] 按鈕也一樣。

回到 WebMatrix。 在程式碼區塊中，將下列反白顯示的程式碼新增至初始化 message 的那一行*之後*：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>If {} 區塊

您剛剛新增的是 if 條件。 在程式碼中，if 條件的結構如下所示：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

要測試的條件是以括弧括住。 它必須是值或傳回 true 或 false 的運算式。 如果條件為 true，則 ASP.NET 會執行括弧內的語句或語句。 （這些是*if then*邏輯的*then*部分）。如果條件為 false，則會略過程式碼區塊。

以下是您可以在 if 語句中測試之條件的幾個範例：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

您可以使用*邏輯運算子*或*比較運算子*，根據值或運算式來測試變數：等於（= =）、大於（&gt;）、小於（&lt;）、大於或等於（&gt;=）和小於或等於（&lt;=）。 ！ = 運算子表示不等於，例如，如果（a！ = 0）表示不*等於 0*。

> [!NOTE]
> 請確定您注意到 equals 的比較運算子（= =）與 = 不相同。 = 運算子僅用於指派值（var a = 2）。 如果您混用這些運算子，您會收到錯誤訊息，否則會出現一些奇怪的結果。

若要測試某個專案是否為 true，完整的語法為 if （作業 = = true）。 但是，如果是（作業），您也可以使用快捷方式。 如果沒有比較運算子，ASP.NET 會假設您要測試是否為 true。

! operator 本身表示邏輯 NOT。 例如，條件 if （！IsPost）表示*IsPost 是否為 true*。

您可以使用邏輯 AND （&amp;&amp; 運算子）或邏輯 OR （| | operator）來合併條件。 例如，前述範例中的最後一個 if 條件，表示*FileProcessingIsDone 未設定為 TRUE，而 displayMessage 設定為 false*。

### <a name="the-else-block"></a>Else 區塊

If 區塊的最後一件事： if 區塊後面可以接著 else 區塊。 Else 區塊很有用，因為條件為 false 時，您必須執行不同的程式碼。 以下是簡單的範例：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

您會在本系列稍後的教學課程中看到一些範例，其中使用 else 區塊會很有用。

### <a name="testing-whether-the-request-is-a-submit-post"></a>測試要求是否為提交（post）

還有更多，但讓我們回到範例，其中有 if （IsPost） {...} 的條件。 IsPost 實際上是目前頁面的屬性。 第一次要求頁面時，IsPost 會傳回 false。 不過，如果您按一下按鈕或提交頁面（也就是您張貼），則 IsPost 會傳回 true。 因此，IsPost 可讓您判斷是否正在處理表單提交。 （就 HTTP 指令動詞而言，如果要求是 GET 作業，則 IsPost 會傳回 false。 如果要求是 POST 作業，IsPost 會傳回 true。）在稍後的教學課程中，您將使用輸入表單，這項測試會特別有用。

執行頁面。 因為這是您第一次要求頁面，所以您會看到「這是您第一次要求此頁面」。 該字串是您用來初始化訊息變數的值。 有一個 if （IsPost）測試，但它目前會傳回 false，因此在 if 區塊內的程式碼不會執行。

按一下 [**提交**] 按鈕。 再次要求頁面。 如前所述，message 變數會設定為「這是第一次 ...」。 但這次，測試 if （IsPost）會傳回 true，因此 if 區塊內的程式碼會執行。 程式碼會將 message 變數的值變更為不同的值，這就是在標記中呈現的內容。

現在，在標記中加入 if 條件。 在包含 [**提交**] 按鈕的 &lt;p&gt; 元素底下，新增下列標記：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

您要在標記內加入程式碼，因此您必須從 @開始。 然後會有一個 [if] 測試，與您稍早在程式碼區塊中新增的類似。 不過，在大括弧內，您會加入一般的 HTML，至少在 @DateTime.Now之前，通常都是正常的。 這是另一小段 Razor 程式碼，因此您必須在前面加上 @。

這裡的重點是，您可以在程式碼區塊的頂端和標記中加入 if 條件。 如果您在頁面主體中使用 if 條件，區塊內的程式列可以是標記或程式碼。 在這種情況下，當您混用標記和程式碼時，和都是如此，您必須使用 @ 讓它清楚 ASP.NET 程式碼所在的位置。

執行頁面，然後按一下 [**提交**]。 這次當您提交（「現在您已提交 ...」）時，您不只會看到不同的訊息，但是您會看到一則列出日期和時間的新訊息。

![在瀏覽器中執行的 [測試 Razor 2] 頁面，包含提交後顯示的時間戳記](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>測試查詢字串的值

另一個測試。 這次，您會新增一個 if 區塊來測試名為 show 且可能會在查詢字串中傳遞的值。 （如下所示： `http://localhost:43097/TestRazorPart2.cshtml?show=true`）您將變更頁面，使您已顯示的訊息（「這是第一次 ...」等等）只有在 show 的值為 true 時才會顯示。

在頁面頂端的程式碼區塊底部（但內部），新增下列內容：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

完整的程式碼區塊現在看起來如下列範例所示。 （請記住，當您將程式碼複製到頁面時，縮排可能看起來會不同。 但這並不會影響程式碼執行的方式）。

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

區塊中的新程式碼會將名為 showMessage 的變數初始化為 false。 然後，它會執行 if 測試，以在查詢字串中尋找值。 當您第一次要求頁面時，它會有如下的 URL：

`http://localhost:43097/TestRazorPart2.cshtml`

此程式碼會判斷 URL 是否包含查詢字串中名為 show 的變數，如下列 URL 版本所示：

`http://localhost:43097/TestRazorPart2.cshtml`？ show = true

測試本身會查看 Request 物件的 QueryString 屬性。 如果查詢字串包含名為 show 的專案，而且該專案設定為 true，則 if 區塊會執行，並將 showMessage 變數設定為 true。

這裡有個秘訣，如您所見。 如同名稱所示，查詢字串是一個字串。 不過，如果您要測試的值是布林值（true/false），則只能測試 true 和 false。 您必須先將查詢字串中的 show 變數值轉換成布林值，才可以在此測試字串中測試它。 這就是 AsBool 方法的作用-它會採用字串做為輸入，並將它轉換成布林值。 很明顯地，如果字串為 "true"，則 AsBool 方法會將該值轉換為 true。 如果字串的值為任何其他專案，則 AsBool 會傳回 false。

> [!TIP] 
> 
> **資料類型和 As （）方法**
> 
> 我們目前只有在建立變數時才會用到關鍵字 var。 不過，這不是整個故事。 若要操作值，以加入數位或串連字號串，或比較日期或測試是否為 true/false， C#必須使用適當的值內部標記法。 C#*通常*可以根據您所執行的值，找出該標記法（也就是資料的*類型*）。 不過，現在它不能這麼做。 如果沒有，您就必須明確指出應該如何C#呈現資料，以協助您。 AsBool 方法會這麼做，它會C#告知字串值 "true" 或 "false" 應視為布林值。 也有類似的方法，將字串表示為其他類型，例如 AsInt （視為整數）、AsDateTime （視為日期/時間）、AsFloat （視為浮點數）等等。 當您使用這些 As （）方法時， C#如果無法代表要求的字串值，您會看到錯誤。

在頁面的標記中，移除或批註化此元素（這裡會顯示為批註）：

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

在您移除或取消批註該文字的右方，新增下列內容：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

If 測試指出如果 showMessage 變數為 true，則會以 message 變數的值呈現 &lt;p&gt; 元素。

### <a name="summary-of-your-conditional-logic"></a>條件式邏輯的摘要

如果您不確定剛完成的作業，這裡有一個摘要。

- Message 變數會初始化為預設字串（「這是第一次 ...」）。
- 如果頁面要求是提交（post）的結果，則訊息的值會變更為「現在您已提交 ...」
- ShowMessage 變數已初始化為 false。
- 如果查詢字串包含？ show = true，則 showMessage 變數會設定為 true。
- 在標記中，如果 showMessage 為 true，則會轉譯 &lt;p&gt; 元素，以顯示 message 的值。 （如果 showMessage 為 false，則在標記中的該時間點不會轉譯任何內容）。
- 在標記中，如果要求是 post，則會轉譯 &lt;p&gt; 元素，以顯示日期和時間。

執行頁面。 沒有訊息，因為 showMessage 是 false，所以在標記中，if （showMessage）測試會傳回 false。

按一下 [提交]。 您會看到日期和時間，但仍然沒有訊息。

在瀏覽器中，移至 [URL] 方塊，並將下列內容新增至 URL 結尾：？ show = true，然後按 Enter。

![顯示查詢字串的瀏覽器中的 [測試 Razor 2] 頁面](intro-to-web-pages-programming/_static/image5.png)

該頁面會再次顯示。 （因為您變更了 URL，所以這是新的要求，而不是提交）。再次按一下 [**提交**]。 訊息會再次顯示，如同日期和時間。

![當有查詢字串時，提交後的 [測試 Razor 2] 頁面](intro-to-web-pages-programming/_static/image6.png)

在 [URL] 中，將？ show = true 變更為？ show = false，然後按 Enter 鍵。 再次提交頁面。 頁面會回到您的啟動方式—沒有訊息。

如先前所述，此範例的邏輯有點假設。 不過，如果要在許多頁面中出現，則會採用您在這裡看到的一或多個表單。

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>安裝 Helper （顯示 Gravatar 的影像）

人們通常會想要在網頁上執行的某些工作需要大量的程式碼，或需要額外的知識。 範例：顯示資料的圖表;將 Facebook 「贊」按鈕放在頁面上;正在從您的網站傳送電子郵件;裁剪或調整影像大小;針對您的網站使用 PayPal。 為了讓您輕鬆執行這類工作，ASP.NET Web Pages 可讓*您使用協助*程式。 Helper 是您為網站安裝的元件，可讓您只使用幾行 Razor 程式碼來執行一般工作。

ASP.NET Web Pages 內建了一些協助程式。 不過，許多協助程式都可以在使用 NuGet 套件管理員所提供的封裝（增益集）中取得。 NuGet 可讓您選取要安裝的套件，然後負責安裝的所有詳細資料。

在本教學課程的這個部分中，您將會安裝協助程式，讓您顯示 Gravatar （「全球辨識的頭像」）影像。 您將會學到兩件事。 其中一個是如何尋找及安裝 helper。 您也將瞭解協助專家如何使用許多您必須自行撰寫的程式碼，輕鬆地執行某些動作。

您可以在位於[http://www.gravatar.com/](http://www.gravatar.com/)的 Gravatar 網站註冊自己的 Gravatar，但建立 Gravatar 帳戶來執行本教學課程部分並不重要。

在 WebMatrix 中，按一下 [ **NuGet** ] 按鈕。

![WebMatrix 中的 [NuGet 資源庫] 對話方塊](intro-to-web-pages-programming/_static/image7.png)

這會啟動 NuGet 套件管理員，並顯示可用的套件。 （並非所有的封裝都是協助程式; 有些會將功能加入至 WebMatrix 本身，有些則是額外的範本）。您可能會收到與版本不相容相關的錯誤訊息。 您可以按一下 **[確定]** 並繼續進行本教學課程，以忽略此錯誤訊息。

![WebMatrix 中的 [NuGet 資源庫] 對話方塊](intro-to-web-pages-programming/_static/image8.png)

在搜尋方塊中，輸入 "asp.net helper"。 NuGet 會顯示符合搜尋詞彙的套件。

![WebMatrix 中的 NuGet 資源庫顯示套件](intro-to-web-pages-programming/_static/image9.png)

ASP.NET Web helper 程式庫包含可簡化許多一般工作的程式碼，包括使用 Gravatar 影像。 選取**ASP.NET Web** Helper 程式庫套件，然後按一下 [**安裝**] 以啟動安裝程式。 當系統詢問您是否要安裝套件，並接受條款以完成安裝時，請選取 **[是]** 。

就這麼容易！ NuGet 會下載並安裝所有專案，包括任何可能需要的其他元件 *（相依*性）。

如果您因為某些原因而必須卸載協助程式，則進程非常類似。 按一下 [ **NuGet** ] 按鈕，按一下 [**已安裝**] 索引標籤，然後挑選您要卸載的套件。

## <a name="using-a-helper-in-a-page"></a>在頁面中使用 Helper

現在您將使用剛安裝的 helper。 將協助程式新增至頁面的程式，與大部分的協助程式類似。

在 WebMatrix 中建立頁面，並將它命名為*GravatarTest. cshml*。 （您要建立一個特殊的頁面來測試協助程式，但是您可以在網站的任何頁面中使用 helper）。

在 &lt;主體&gt; 元素內，新增 &lt;div&gt; 專案。 在 &lt;div&gt; 元素內，輸入下列內容：

@Gravatar

@ 字元與您用來標示 Razor 程式碼的字元相同。 **Gravatar**是您要使用的 helper 物件。

一旦您輸入句號（.），WebMatrix 會顯示 Gravatar helper 提供的*方法*（函式）清單：

![Gravatar helper IntelliSense 下拉式清單](intro-to-web-pages-programming/_static/image10.png)

這項功能稱為*IntelliSense*。 它會提供內容適當的選擇，協助您撰寫程式碼。 IntelliSense 適用于在 WebMatrix 中支援的 HTML、CSS、ASP.NET 程式碼、JavaScript 和其他語言。 這是另一項功能，可讓您更輕鬆地在 WebMatrix 中開發網頁。

在鍵盤上按 G，您會看到 IntelliSense 找到 Recaptcha.gethtml 方法。 按下 Tab 鍵。 IntelliSense 會為您插入選取的方法（Recaptcha.gethtml）。 輸入左括弧，並注意右括弧會自動新增。 在兩個括弧之間的引號中輸入您的電子郵件地址。 如果您有 Gravatar 帳戶，則會傳回您的個人資料圖片。 如果您沒有 Gravatar 帳戶，則會傳回預設映射。 當您完成時，該行看起來會像這樣：

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

現在請在瀏覽器中查看頁面。 視您是否有 Gravatar 帳戶而定，會顯示您的圖片或預設影像。

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![預設影像](intro-to-web-pages-programming/_static/image12.png)

若要瞭解協助專家為您做什麼，請在瀏覽器中查看頁面的來源。 除了您在頁面中所擁有的 HTML 之外，您還會看到包含識別碼的 image 元素。 這是協助程式在您已 @Gravatar.GetHtml的位置呈現在頁面中的程式碼。 Helper 會採用您提供的資訊，並產生直接與 Gravatar 交談的程式碼，以取得所提供帳戶的正確影像。

Recaptcha.gethtml 方法也可讓您藉由提供其他參數來自訂映射。 下列程式碼示範如何要求影像的寬度和高度為40圖元，如果指定的帳號不存在，則會使用名為**wavatar**的指定預設映射。

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

此程式碼會產生類似下列結果的內容（預設映射會隨機改變）。

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>下一步

為了讓本教學課程簡短，我們必須只著重于幾個基本概念。 而且 Razor 和C#還有*許多*其他方面。 當您完成這些教學課程時，您將會進一步瞭解。 如果您想要深入瞭解 Razor 和C#目前的程式設計方面，您可以在這裡閱讀更詳盡的簡介：[使用 Razor 語法進行 Web 程式設計的簡介 ASP.NET](https://go.microsoft.com/fwlink/?LinkID=202890)。

下一個教學課程將為您介紹如何使用資料庫。 在該教學課程中，您將開始建立範例應用程式，讓您列出最愛的電影。

## <a name="complete-listing-for-testrazor-page"></a>TestRazor 頁面的完整清單

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>TestRazorPart2 頁面的完整清單

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>GravatarTest 頁面的完整清單

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Twitter helper](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [上一頁](getting-started.md)
> [下一頁](displaying-data.md)
