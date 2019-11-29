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
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564879"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="6bbec-104">使用 Razor 語法 ASP.NET Web 程式設計的簡介（C#）</span><span class="sxs-lookup"><span data-stu-id="6bbec-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="6bbec-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6bbec-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6bbec-106">本文可讓您瞭解如何使用 Razor 語法 ASP.NET Web Pages 進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="6bbec-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="6bbec-107">ASP.NET 是 Microsoft 在網頁伺服器上執行動態網頁的技術。</span><span class="sxs-lookup"><span data-stu-id="6bbec-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="6bbec-108">這篇文章著重于使用C#程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="6bbec-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="6bbec-109">**您將瞭解的內容**：</span><span class="sxs-lookup"><span data-stu-id="6bbec-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="6bbec-110">使用 Razor 語法開始進行程式設計 ASP.NET Web Pages 的前8個程式設計秘訣。</span><span class="sxs-lookup"><span data-stu-id="6bbec-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="6bbec-111">您需要的基本程式設計概念。</span><span class="sxs-lookup"><span data-stu-id="6bbec-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="6bbec-112">什麼是 ASP.NET 伺服器程式碼和 Razor 語法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6bbec-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="6bbec-113">軟體版本</span><span class="sxs-lookup"><span data-stu-id="6bbec-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="6bbec-114">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="6bbec-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="6bbec-115">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="6bbec-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="6bbec-116">前8個程式設計提示</span><span class="sxs-lookup"><span data-stu-id="6bbec-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="6bbec-117">本節列出當您使用 Razor 語法開始撰寫 ASP.NET 伺服器程式碼時，您絕對需要知道的幾個秘訣。</span><span class="sxs-lookup"><span data-stu-id="6bbec-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbec-118">Razor 語法是以程式C#設計語言為基礎，這是最常用於 ASP.NET Web Pages 的語言。</span><span class="sxs-lookup"><span data-stu-id="6bbec-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="6bbec-119">不過，Razor 語法也支援 Visual Basic 語言，而且您看到的所有內容也可以在 Visual Basic 中執行。</span><span class="sxs-lookup"><span data-stu-id="6bbec-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="6bbec-120">如需詳細資訊，請參閱附錄[Visual Basic 語言和語法](https://go.microsoft.com/fwlink/?LinkId=202908)。</span><span class="sxs-lookup"><span data-stu-id="6bbec-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="6bbec-121">您稍後可以在本文中找到更多有關這些程式設計技巧的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6bbec-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="6bbec-122">1. 使用 @ 字元將程式碼加入至頁面</span><span class="sxs-lookup"><span data-stu-id="6bbec-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="6bbec-123">`@` 字元會啟動內嵌運算式、單一語句區塊和多重語句區塊：</span><span class="sxs-lookup"><span data-stu-id="6bbec-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="6bbec-124">當頁面在瀏覽器中執行時，這就是這些語句的樣子：</span><span class="sxs-lookup"><span data-stu-id="6bbec-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="6bbec-126">**HTML 編碼**</span><span class="sxs-lookup"><span data-stu-id="6bbec-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="6bbec-127">當您使用 `@` 字元在頁面中顯示內容時（如上述範例所示），ASP.NET 會以 HTML 編碼輸出。</span><span class="sxs-lookup"><span data-stu-id="6bbec-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="6bbec-128">這會將保留的 HTML 字元（例如 `<` 和 `>` 和 `&`）取代為程式碼，讓字元在網頁中顯示為字元，而不是被轉譯為 HTML 標籤或實體。</span><span class="sxs-lookup"><span data-stu-id="6bbec-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="6bbec-129">如果沒有 HTML 編碼，來自您的伺服器程式碼的輸出可能無法正確顯示，而且可能會讓頁面暴露于安全性風險下。</span><span class="sxs-lookup"><span data-stu-id="6bbec-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="6bbec-130">如果您的目標是要輸出將標記轉譯為標記的 HTML 標籤（例如 `<p></p>` 用於段落或 `<em></em>` 強調文字），請參閱本文稍後的在程式[代碼區塊中結合文字、標記和程式碼](#BM_CombiningTextMarkupAndCode)一節。</span><span class="sxs-lookup"><span data-stu-id="6bbec-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="6bbec-131">您可以閱讀更多有關[使用表單](https://go.microsoft.com/fwlink/?LinkId=202892)的 HTML 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="6bbec-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="6bbec-132">2. 以大括弧括住程式碼區塊</span><span class="sxs-lookup"><span data-stu-id="6bbec-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="6bbec-133">程式*代碼區塊*包含一或多個程式碼語句，並以大括弧括住。</span><span class="sxs-lookup"><span data-stu-id="6bbec-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="6bbec-134">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="6bbec-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="6bbec-136">3. 在區塊內，以分號結束每個程式碼語句</span><span class="sxs-lookup"><span data-stu-id="6bbec-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="6bbec-137">在程式碼區塊內，每個完整的程式碼語句都必須以分號結尾。</span><span class="sxs-lookup"><span data-stu-id="6bbec-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="6bbec-138">內嵌運算式的結尾不是分號。</span><span class="sxs-lookup"><span data-stu-id="6bbec-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="6bbec-139">4. 您可以使用變數來儲存值</span><span class="sxs-lookup"><span data-stu-id="6bbec-139">4. You use variables to store values</span></span>

<span data-ttu-id="6bbec-140">您可以將值儲存在*變數*中，包括字串、數位和日期等等。您可以使用 `var` 關鍵字來建立新的變數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="6bbec-141">您可以使用 `@`，直接在頁面中插入變數值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="6bbec-142">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="6bbec-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="6bbec-144">5. 用雙引號括住常值字串</span><span class="sxs-lookup"><span data-stu-id="6bbec-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="6bbec-145">*字串*是視為文字的字元序列。</span><span class="sxs-lookup"><span data-stu-id="6bbec-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="6bbec-146">若要指定字串，請將其括在雙引號內：</span><span class="sxs-lookup"><span data-stu-id="6bbec-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="6bbec-147">如果您想要顯示的字串包含反斜線字元（`\`）或雙引號（`"`），請使用前面加上 `@` 運算子的*逐字字串常*值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="6bbec-148">（在C#中，\ 字元具有特殊意義，除非您使用逐字字串常值）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="6bbec-149">若要內嵌雙引號，請使用逐字字串常值，並重複引號：</span><span class="sxs-lookup"><span data-stu-id="6bbec-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="6bbec-150">以下是在頁面中使用這兩個範例的結果：</span><span class="sxs-lookup"><span data-stu-id="6bbec-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="6bbec-152">請注意，`@` 字元會用來標記中C#的逐字字串常值，並在 ASP.NET 網頁中標記程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bbec-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="6bbec-153">6. 程式碼區分大小寫</span><span class="sxs-lookup"><span data-stu-id="6bbec-153">6. Code is case sensitive</span></span>

<span data-ttu-id="6bbec-154">在C#中，關鍵字（例如 `var`、`true`和 `if`）和變數名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6bbec-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="6bbec-155">下列幾行程式碼會建立兩個不同的變數，`lastName` 和 `LastName.`</span><span class="sxs-lookup"><span data-stu-id="6bbec-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="6bbec-156">如果您將變數宣告為 `var lastName = "Smith";`，並嘗試在頁面中以 `@LastName`的形式參考該變數，您會得到 `"Jones"` 的值，而不是 `"Smith"`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbec-157">在 Visual Basic 中，關鍵字和變數*不*區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6bbec-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="6bbec-158">7. 您的程式碼大部分牽涉到物件</span><span class="sxs-lookup"><span data-stu-id="6bbec-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="6bbec-159">*物件*代表您可以使用&#8212;頁面、文字方塊、檔案、影像、web 要求、電子郵件訊息、客戶記錄（資料庫資料列）等進行程式設計的東西。物件具有描述其特性的屬性，而且您可以讀取或變更&#8212;文字方塊物件具有 `Text` 屬性（其中還有一個），要求物件具有 `Url` 屬性，電子郵件訊息具有 `From` 屬性，而 customer 物件則具有 `FirstName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="6bbec-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="6bbec-160">物件也有 &quot;動詞&quot; 可以執行的方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="6bbec-161">範例包括 file 物件的 `Save` 方法、影像物件的 `Rotate` 方法，以及電子郵件物件的 `Send` 方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="6bbec-162">您通常會使用 `Request` 物件，這會提供頁面上文字方塊（表單欄位）的值、提出要求的瀏覽器類型、頁面的 URL、使用者身分識別等資訊。下列範例示範如何存取 `Request` 物件的屬性，以及如何呼叫 `Request` 物件的 `MapPath` 方法，這會提供您伺服器上頁面的絕對路徑：</span><span class="sxs-lookup"><span data-stu-id="6bbec-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="6bbec-163">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="6bbec-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="6bbec-165">8. 您可以撰寫程式碼來做出決策</span><span class="sxs-lookup"><span data-stu-id="6bbec-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="6bbec-166">動態網頁的主要功能是，您可以根據條件來決定要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="6bbec-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="6bbec-167">最常見的做法是使用 `if` 語句（和選擇性的 `else` 語句）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="6bbec-168">語句 `if(IsPost)` 是撰寫 `if(IsPost == true)`的簡寫方式。</span><span class="sxs-lookup"><span data-stu-id="6bbec-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="6bbec-169">除了 `if` 語句之外，還有各種不同的方法可以測試條件、重複的程式碼區塊等等，本文稍後會加以說明。</span><span class="sxs-lookup"><span data-stu-id="6bbec-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="6bbec-170">在瀏覽器中顯示的結果（按一下 [**提交**] 之後）：</span><span class="sxs-lookup"><span data-stu-id="6bbec-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="6bbec-172">HTTP GET 和 POST 方法和 IsPost 屬性</span><span class="sxs-lookup"><span data-stu-id="6bbec-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="6bbec-173">網頁（HTTP）所使用的通訊協定支援非常有限的方法（動詞）數目，用來對伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="6bbec-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="6bbec-174">最常見的兩個是 GET，用來讀取頁面和 POST （用來提交頁面）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="6bbec-175">一般情況下，使用者第一次要求頁面時，會使用 GET 來要求頁面。</span><span class="sxs-lookup"><span data-stu-id="6bbec-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="6bbec-176">如果使用者填滿表單，然後按一下 [提交] 按鈕，則瀏覽器會對伺服器提出 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="6bbec-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="6bbec-177">在 web 程式設計中，知道頁面是否以 GET 或 POST 的方式要求，讓您知道如何處理頁面，通常會很有説明。</span><span class="sxs-lookup"><span data-stu-id="6bbec-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="6bbec-178">在 ASP.NET Web Pages 中，您可以使用 [`IsPost`] 屬性來查看要求是 GET 或 POST。</span><span class="sxs-lookup"><span data-stu-id="6bbec-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="6bbec-179">如果要求是 POST，`IsPost` 屬性會傳回 true，而您可以執行讀取表單上文字方塊值之類的動作。</span><span class="sxs-lookup"><span data-stu-id="6bbec-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="6bbec-180">您會看到的許多範例會告訴您如何根據 `IsPost`的值，以不同的方式處理頁面。</span><span class="sxs-lookup"><span data-stu-id="6bbec-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="6bbec-181">簡單的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6bbec-181">A Simple Code Example</span></span>

<span data-ttu-id="6bbec-182">此程式說明如何建立說明基本程式設計技術的頁面。</span><span class="sxs-lookup"><span data-stu-id="6bbec-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="6bbec-183">在此範例中，您會建立可讓使用者輸入兩個數字的頁面，然後將其加入並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="6bbec-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="6bbec-184">在您的編輯器中，建立新的檔案，並將它命名為*AddNumbers*。</span><span class="sxs-lookup"><span data-stu-id="6bbec-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="6bbec-185">將下列程式碼和標記複製到頁面中，並取代頁面中已存在的任何專案。</span><span class="sxs-lookup"><span data-stu-id="6bbec-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="6bbec-186">以下是您要注意的一些事項：</span><span class="sxs-lookup"><span data-stu-id="6bbec-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="6bbec-187">`@` 字元會啟動頁面中第一個程式碼區塊，並在靠近頁面底部的 `totalMessage` 變數之前。</span><span class="sxs-lookup"><span data-stu-id="6bbec-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="6bbec-188">頁面頂端的區塊會以大括弧括住。</span><span class="sxs-lookup"><span data-stu-id="6bbec-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="6bbec-189">在頂端的區塊中，所有行的結尾都是分號。</span><span class="sxs-lookup"><span data-stu-id="6bbec-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="6bbec-190">`total`、`num1`、`num2`和 `totalMessage` 的變數會儲存數個數字和一個字串。</span><span class="sxs-lookup"><span data-stu-id="6bbec-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="6bbec-191">指派給 `totalMessage` 變數的常值字串值是以雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="6bbec-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="6bbec-192">由於程式碼區分大小寫，因此當 `totalMessage` 變數使用接近頁面底部時，其名稱必須完全符合頂端的變數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="6bbec-193">運算式 `num1.AsInt() + num2.AsInt()` 顯示如何使用物件和方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="6bbec-194">每個變數上的 `AsInt` 方法會將使用者輸入的字串轉換成數位（整數），以便您在其上執行算數運算。</span><span class="sxs-lookup"><span data-stu-id="6bbec-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="6bbec-195">`<form>` 標記包含 `method="post"` 屬性。</span><span class="sxs-lookup"><span data-stu-id="6bbec-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="6bbec-196">這會指定當使用者按一下 [**新增**] 時，會使用 HTTP POST 方法將頁面傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="6bbec-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="6bbec-197">提交頁面時，`if(IsPost)` 測試會評估為 true，且會執行條件式程式碼，以顯示加入數位的結果。</span><span class="sxs-lookup"><span data-stu-id="6bbec-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="6bbec-198">儲存頁面，並在瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="6bbec-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="6bbec-199">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）輸入兩個整數，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6bbec-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="6bbec-201">基本程式設計概念</span><span class="sxs-lookup"><span data-stu-id="6bbec-201">Basic Programming Concepts</span></span>

<span data-ttu-id="6bbec-202">本文提供 ASP.NET web 程式設計的總覽。</span><span class="sxs-lookup"><span data-stu-id="6bbec-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="6bbec-203">這不是詳盡的檢查，只要快速導覽一下您最常使用的程式設計概念即可。</span><span class="sxs-lookup"><span data-stu-id="6bbec-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="6bbec-204">就算如此，它還涵蓋了您開始使用 ASP.NET Web Pages 所需的幾乎所有專案。</span><span class="sxs-lookup"><span data-stu-id="6bbec-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="6bbec-205">但首先，有點的技術背景。</span><span class="sxs-lookup"><span data-stu-id="6bbec-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="6bbec-206">Razor 語法、伺服器程式碼和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6bbec-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="6bbec-207">Razor 語法是簡單的程式設計語法，用於在網頁中內嵌以伺服器為基礎的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bbec-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="6bbec-208">在使用 Razor 語法的網頁中，有兩種內容：用戶端內容和伺服器程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bbec-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="6bbec-209">用戶端內容是您在網頁中使用的專案： HTML 標籤（元素）、樣式資訊（例如 CSS）可能是某些用戶端腳本，例如 JavaScript 和純文字。</span><span class="sxs-lookup"><span data-stu-id="6bbec-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="6bbec-210">Razor 語法可讓您將伺服器程式碼新增到此用戶端內容。</span><span class="sxs-lookup"><span data-stu-id="6bbec-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="6bbec-211">如果頁面中有伺服器程式碼，伺服器會先執行該程式碼，然後再將頁面傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6bbec-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="6bbec-212">藉由在伺服器上執行，程式碼可以執行工作，使其更複雜，只使用用戶端內容，例如存取以伺服器為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6bbec-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="6bbec-213">最重要的是，伺服器程式碼可以動態&#8212;建立用戶端內容，它可以即時產生 HTML 標籤或其他內容，然後將它連同頁面可能包含的任何靜態 HTML 傳送到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6bbec-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="6bbec-214">從瀏覽器的觀點來看，您的伺服器程式碼所產生的用戶端內容與其他用戶端內容並無不同。</span><span class="sxs-lookup"><span data-stu-id="6bbec-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="6bbec-215">如您已見過，所需的伺服器程式碼相當簡單。</span><span class="sxs-lookup"><span data-stu-id="6bbec-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="6bbec-216">包含 Razor 語法的 ASP.NET 網頁具有特殊的副檔名（*cshtml*或*vbhtml*）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="6bbec-217">伺服器會辨識這些擴充功能、執行標記為 Razor 語法的程式碼，然後將頁面傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6bbec-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="6bbec-218">ASP.NET 適用於何處？</span><span class="sxs-lookup"><span data-stu-id="6bbec-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="6bbec-219">Razor 語法是以 Microsoft 的技術為基礎，稱為 ASP.NET，也就是以 Microsoft .NET Framework 為基礎。</span><span class="sxs-lookup"><span data-stu-id="6bbec-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="6bbec-220">The.NET Framework 是一個龐大的完整程式設計架構，可供 Microsoft 開發幾乎任何類型的電腦應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bbec-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="6bbec-221">ASP.NET 是專為建立 web 應用程式而設計的 .NET Framework 部分。</span><span class="sxs-lookup"><span data-stu-id="6bbec-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="6bbec-222">開發人員使用 ASP.NET，在世界各地建立許多最大且最高的流量網站。</span><span class="sxs-lookup"><span data-stu-id="6bbec-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="6bbec-223">（當您在網站中的 URL 中看到副檔名為 *.aspx*時，您會知道網站是以 ASP.NET 撰寫的）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="6bbec-224">Razor 語法為您提供 ASP.NET 的所有威力，但使用簡化的語法，如果您是新手，就能更輕鬆地學習，如果您是專家，也能讓您更具生產力。</span><span class="sxs-lookup"><span data-stu-id="6bbec-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="6bbec-225">雖然此語法很容易使用，它與 ASP.NET 的系列關係和 .NET Framework 表示當您的網站變得更精密時，您可以使用較大的架構。</span><span class="sxs-lookup"><span data-stu-id="6bbec-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="6bbec-227">**類別和實例**</span><span class="sxs-lookup"><span data-stu-id="6bbec-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="6bbec-228">ASP.NET 伺服器程式碼會使用物件，而這些物件則是以類別的概念為基礎。</span><span class="sxs-lookup"><span data-stu-id="6bbec-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="6bbec-229">類別是物件的定義或範本。</span><span class="sxs-lookup"><span data-stu-id="6bbec-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="6bbec-230">例如，應用程式可能會包含一個 `Customer` 類別，以定義任何客戶物件所需的屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="6bbec-231">當應用程式需要處理實際的客戶資訊時，它會建立一個（或具現*化*） customer 物件的實例。</span><span class="sxs-lookup"><span data-stu-id="6bbec-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="6bbec-232">每一位客戶都是 `Customer` 類別的個別實例。</span><span class="sxs-lookup"><span data-stu-id="6bbec-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="6bbec-233">每個實例都支援相同的屬性和方法，但每個實例的屬性值通常不同，因為每個客戶物件都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6bbec-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="6bbec-234">在一個客戶物件中，`LastName` 屬性可能是 "Smith";在另一個客戶物件中，`LastName` 屬性可能是「張」。</span><span class="sxs-lookup"><span data-stu-id="6bbec-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="6bbec-235">同樣地，您網站中的任何個別網頁都是 `Page` 物件，這是 `Page` 類別的實例。</span><span class="sxs-lookup"><span data-stu-id="6bbec-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="6bbec-236">頁面上的按鈕是 `Button` 物件，它是 `Button` 類別的實例，依此類推。</span><span class="sxs-lookup"><span data-stu-id="6bbec-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="6bbec-237">每個實例都有自己的特性，但它們都是以物件的類別定義中指定的內容為基礎。</span><span class="sxs-lookup"><span data-stu-id="6bbec-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="6bbec-238">基本語法</span><span class="sxs-lookup"><span data-stu-id="6bbec-238">Basic Syntax</span></span>

<span data-ttu-id="6bbec-239">稍早您會看到如何建立 ASP.NET Web Pages 頁面的基本範例，以及如何將伺服器程式碼加入至 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="6bbec-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="6bbec-240">在這裡，您將瞭解使用 Razor 語法&#8212; （也就是程式設計語言規則）撰寫 ASP.NET 伺服器程式碼的基本概念。</span><span class="sxs-lookup"><span data-stu-id="6bbec-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="6bbec-241">如果您對程式設計有經驗（特別是使用 C、 C++、 C#、Visual Basic 或 JavaScript），您在這裡閱讀的大部分內容都很熟悉。</span><span class="sxs-lookup"><span data-stu-id="6bbec-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="6bbec-242">您可能只需要熟悉如何將伺服器程式碼加入至*cshtml*檔案中的標記。</span><span class="sxs-lookup"><span data-stu-id="6bbec-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="6bbec-243">結合程式碼區塊中的文字、標記和程式碼</span><span class="sxs-lookup"><span data-stu-id="6bbec-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="6bbec-244">在 [伺服器程式碼區塊] 中，您通常會想要將文字或標記（或兩者）輸出至頁面。</span><span class="sxs-lookup"><span data-stu-id="6bbec-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="6bbec-245">如果伺服器程式碼區塊包含不是程式碼的文字，而應該改為轉譯，則 ASP.NET 必須能夠區別該文字與程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bbec-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="6bbec-246">有幾個方式可做到這點。</span><span class="sxs-lookup"><span data-stu-id="6bbec-246">There are several ways to do this.</span></span>

- <span data-ttu-id="6bbec-247">將文字括在 HTML 元素中，例如 `<p></p>` 或 `<em></em>`：</span><span class="sxs-lookup"><span data-stu-id="6bbec-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="6bbec-248">HTML 元素可以包含文字、其他 HTML 專案和伺服器程式碼運算式。</span><span class="sxs-lookup"><span data-stu-id="6bbec-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="6bbec-249">當 ASP.NET 看到開頭的 HTML 標籤（例如 `<p>`）時，它會將專案及其內容在內的一切轉譯為瀏覽器，並在伺服器程式碼運算式發生時加以解析。</span><span class="sxs-lookup"><span data-stu-id="6bbec-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="6bbec-250">請使用 `@:` 運算子或 `<text>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6bbec-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="6bbec-251">`@:` 輸出包含純文字或不相符 HTML 標籤的單一行內容;`<text>` 元素會將多行括住以輸出。</span><span class="sxs-lookup"><span data-stu-id="6bbec-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="6bbec-252">當您不想要將 HTML 元素轉譯為輸出的一部分時，這些選項會很有用。</span><span class="sxs-lookup"><span data-stu-id="6bbec-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="6bbec-253">如果您想要輸出多行文字或不相符的 HTML 標籤，您可以在每一行前面加上 `@:`，或者將該行括在 `<text>` 元素中。</span><span class="sxs-lookup"><span data-stu-id="6bbec-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="6bbec-254">就像 `@:` 運算子一樣，ASP.NET 會使用`<text>` 標記來識別文字內容，而且永遠不會呈現在頁面輸出中。</span><span class="sxs-lookup"><span data-stu-id="6bbec-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="6bbec-255">第一個範例會重複上一個範例，但會使用一對 `<text>` 標記來括住要轉譯的文字。</span><span class="sxs-lookup"><span data-stu-id="6bbec-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="6bbec-256">在第二個範例中，`<text>` 和 `</text>` 標記會括住三行，其中所有的程式碼都有一些非內含性文字和不相符的 HTML 標籤（`<br />`），以及伺服器程式碼和相符的 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="6bbec-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="6bbec-257">同樣地，您也可以分別在每一行的前面加上 `@:` 運算子;任一種方法都可行。</span><span class="sxs-lookup"><span data-stu-id="6bbec-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6bbec-258">當您&#8212;使用 HTML 專案（如本節所示）輸出文字時，`@:` 運算子或 `<text>` 元素&#8212; ASP.NET 不會對輸出進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="6bbec-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="6bbec-259">（如先前所述，ASP.NET 會對前面加上 `@`的伺服器程式碼運算式和伺服器程式碼區塊的輸出進行編碼，但本節中所述的特殊情況除外）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="6bbec-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="6bbec-260">Whitespace</span></span>

<span data-ttu-id="6bbec-261">語句（和字串常值外部）中的額外空格不會影響語句：</span><span class="sxs-lookup"><span data-stu-id="6bbec-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="6bbec-262">語句中的分行符號不會影響語句，而且您可以包裝語句以方便閱讀。</span><span class="sxs-lookup"><span data-stu-id="6bbec-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="6bbec-263">下列陳述式是相同的：</span><span class="sxs-lookup"><span data-stu-id="6bbec-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="6bbec-264">不過，您無法在字串常值的中間換行。</span><span class="sxs-lookup"><span data-stu-id="6bbec-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="6bbec-265">下列範例無法使用：</span><span class="sxs-lookup"><span data-stu-id="6bbec-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="6bbec-266">若要結合一個長字串，以包裝到多行（如上述程式碼），有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="6bbec-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="6bbec-267">您可以使用串連運算子（`+`），這會在本文稍後看到。</span><span class="sxs-lookup"><span data-stu-id="6bbec-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="6bbec-268">您也可以使用 `@` 字元來建立逐字字串常值，如您稍早在本文中所見。</span><span class="sxs-lookup"><span data-stu-id="6bbec-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="6bbec-269">您可以跨行中斷逐字字串常值：</span><span class="sxs-lookup"><span data-stu-id="6bbec-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="6bbec-270">程式碼（和標記）批註</span><span class="sxs-lookup"><span data-stu-id="6bbec-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="6bbec-271">批註可讓您為自己或其他人留下筆記。</span><span class="sxs-lookup"><span data-stu-id="6bbec-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="6bbec-272">它們也可讓您停用（*批註*）您不想執行的程式碼或標記區段，但想要保留在頁面中的時間。</span><span class="sxs-lookup"><span data-stu-id="6bbec-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="6bbec-273">Razor 程式碼和 HTML 標籤有不同的批註語法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="6bbec-274">就像所有的 Razor 程式碼一樣，在頁面傳送至瀏覽器之前，會先處理 Razor 批註，然後再將其移除。</span><span class="sxs-lookup"><span data-stu-id="6bbec-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="6bbec-275">因此，Razor 批註語法可讓您將批註放入程式碼中（甚至是標記），您可以在編輯檔案時看到，但即使在頁面原始檔中，也不會看到該使用者。</span><span class="sxs-lookup"><span data-stu-id="6bbec-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="6bbec-276">針對 ASP.NET Razor 批註，您可以使用 `@*` 開始批註，並以 `*@`結束。</span><span class="sxs-lookup"><span data-stu-id="6bbec-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="6bbec-277">批註可以位於一行或多行：</span><span class="sxs-lookup"><span data-stu-id="6bbec-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="6bbec-278">以下是程式碼區塊中的批註：</span><span class="sxs-lookup"><span data-stu-id="6bbec-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="6bbec-279">以下是相同的程式碼區塊，並將程式程式碼標記為批註，使其不會執行：</span><span class="sxs-lookup"><span data-stu-id="6bbec-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="6bbec-280">在程式碼區塊內，做為使用 Razor 批註語法的替代方法，您可以使用您所使用之程式設計語言的批註語法， C#例如：</span><span class="sxs-lookup"><span data-stu-id="6bbec-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="6bbec-281">在C#中，單行批註的前面會加上 `//` 個字元，而多行批註則以 `/*` 開頭，並以 `*/`結尾。</span><span class="sxs-lookup"><span data-stu-id="6bbec-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="6bbec-282">（如同 Razor 批註， C#批註不會轉譯至瀏覽器）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="6bbec-283">針對標記，您可能已經知道，您可以建立 HTML 批註：</span><span class="sxs-lookup"><span data-stu-id="6bbec-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="6bbec-284">HTML 批註的開頭為 `<!--` 個字元，並以 `-->`結尾。</span><span class="sxs-lookup"><span data-stu-id="6bbec-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="6bbec-285">您可以使用 HTML 批註來括住文字，但您可能會想要保留在頁面中，但不想呈現的任何 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="6bbec-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="6bbec-286">此 HTML 批註會隱藏標記的全部內容及其包含的文字：</span><span class="sxs-lookup"><span data-stu-id="6bbec-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="6bbec-287">不同于 Razor 批註，HTML 批註*會*轉譯成頁面，使用者可以藉由查看頁面來源來查看它們。</span><span class="sxs-lookup"><span data-stu-id="6bbec-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="6bbec-288">Razor 在的C#嵌套區塊上有限制。</span><span class="sxs-lookup"><span data-stu-id="6bbec-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="6bbec-289">如需詳細資訊[， C#請參閱命名變數和嵌套區塊產生中斷](http://aspnetwebstack.codeplex.com/workitem/1914)的程式碼</span><span class="sxs-lookup"><span data-stu-id="6bbec-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="6bbec-290">變數</span><span class="sxs-lookup"><span data-stu-id="6bbec-290">Variables</span></span>

<span data-ttu-id="6bbec-291">變數是您用來儲存資料的已命名物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="6bbec-292">您可以將變數命名為任何名稱，但名稱必須以字母字元開頭，而且不能包含空格或保留字元。</span><span class="sxs-lookup"><span data-stu-id="6bbec-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="6bbec-293">變數和資料類型</span><span class="sxs-lookup"><span data-stu-id="6bbec-293">Variables and Data Types</span></span>

<span data-ttu-id="6bbec-294">變數可以具有特定的資料類型，以指出變數中儲存的資料種類。</span><span class="sxs-lookup"><span data-stu-id="6bbec-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="6bbec-295">您可以擁有儲存字串值的字串變數（例如 &quot;Hello world&quot;）、儲存整數值（例如3或79）的整數變數，以及以各種格式（例如4/12/2012 或3月2009）儲存日期值的日期變數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="6bbec-296">而且還有許多其他資料類型可供您使用。</span><span class="sxs-lookup"><span data-stu-id="6bbec-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="6bbec-297">不過，您通常不需要指定變數的類型。</span><span class="sxs-lookup"><span data-stu-id="6bbec-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="6bbec-298">大部分的情況下，ASP.NET 都可以根據變數中的資料使用方式來找出型別。</span><span class="sxs-lookup"><span data-stu-id="6bbec-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="6bbec-299">（有時候您必須指定類型，您將會看到這是 true 的範例）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="6bbec-300">您可以使用 `var` 關鍵字（如果您不想指定類型）或使用類型的名稱來宣告變數：</span><span class="sxs-lookup"><span data-stu-id="6bbec-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="6bbec-301">下列範例顯示網頁中變數的一些一般用法：</span><span class="sxs-lookup"><span data-stu-id="6bbec-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="6bbec-302">如果您在頁面中結合前面的範例，您會看到這會顯示在瀏覽器中：</span><span class="sxs-lookup"><span data-stu-id="6bbec-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="6bbec-304">轉換和測試資料類型</span><span class="sxs-lookup"><span data-stu-id="6bbec-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="6bbec-305">雖然 ASP.NET 通常可以自動判斷資料類型，但有時卻不能。</span><span class="sxs-lookup"><span data-stu-id="6bbec-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="6bbec-306">因此，您可能需要執行明確轉換來協助 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="6bbec-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="6bbec-307">即使您不需要轉換類型，有時還是可以測試以查看您可能使用的資料類型。</span><span class="sxs-lookup"><span data-stu-id="6bbec-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="6bbec-308">最常見的情況是，您必須將字串轉換成另一種類型，例如整數或日期。</span><span class="sxs-lookup"><span data-stu-id="6bbec-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="6bbec-309">下列範例顯示您必須將字串轉換成數位的一般情況。</span><span class="sxs-lookup"><span data-stu-id="6bbec-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="6bbec-310">就規則而言，使用者輸入會以字串的形式提供給您。</span><span class="sxs-lookup"><span data-stu-id="6bbec-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="6bbec-311">即使您已提示使用者輸入數位，而且即使他們輸入了數位，當使用者輸入提交，而且您在程式碼中讀取時，資料仍會是字串格式。</span><span class="sxs-lookup"><span data-stu-id="6bbec-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="6bbec-312">因此，您必須將字串轉換成數位。</span><span class="sxs-lookup"><span data-stu-id="6bbec-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="6bbec-313">在此範例中，如果您嘗試對值執行算術而不加以轉換，則會產生下列錯誤，因為 ASP.NET 無法加入兩個字串：</span><span class="sxs-lookup"><span data-stu-id="6bbec-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="6bbec-314">*無法將類型 ' string ' 隱含轉換為 ' int '。*</span><span class="sxs-lookup"><span data-stu-id="6bbec-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="6bbec-315">若要將值轉換為整數，您可以呼叫 `AsInt` 方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="6bbec-316">如果轉換成功，您可以接著加入數位。</span><span class="sxs-lookup"><span data-stu-id="6bbec-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="6bbec-317">下表列出一些常見的變數轉換和測試方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="6bbec-318"><strong>方法</strong></span><span class="sxs-lookup"><span data-stu-id="6bbec-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-319"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="6bbec-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-320"><strong>範例</strong></span><span class="sxs-lookup"><span data-stu-id="6bbec-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-321">將代表整數（例如 "593"）的字串轉換為整數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
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
    <span data-ttu-id="6bbec-322">將 &quot;true&quot; 或 &quot;false&quot; 之類的字串轉換成布林值類型。</span><span class="sxs-lookup"><span data-stu-id="6bbec-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
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
    <span data-ttu-id="6bbec-323">將具有十進位值（例如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字串轉換為浮點數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
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
    <span data-ttu-id="6bbec-324">將具有十進位值（例如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字串轉換為十進位數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="6bbec-325">（在 ASP.NET 中，十進位數比浮點數更精確）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
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
    <span data-ttu-id="6bbec-326">將表示日期和時間值的字串轉換為 ASP.NET `DateTime` 類型。</span><span class="sxs-lookup"><span data-stu-id="6bbec-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
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
    <span data-ttu-id="6bbec-327">將任何其他資料類型轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="6bbec-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="6bbec-328">運算子</span><span class="sxs-lookup"><span data-stu-id="6bbec-328">Operators</span></span>

<span data-ttu-id="6bbec-329">「運算子」是一個關鍵字或字元，告訴 ASP.NET 要在運算式中執行哪一種命令。</span><span class="sxs-lookup"><span data-stu-id="6bbec-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="6bbec-330">C#語言（以及以它為基礎的 Razor 語法）支援許多運算子，但您只需要辨識幾個，即可開始使用。</span><span class="sxs-lookup"><span data-stu-id="6bbec-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="6bbec-331">下表摘要說明最常見的運算子。</span><span class="sxs-lookup"><span data-stu-id="6bbec-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="6bbec-332"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="6bbec-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-333"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="6bbec-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-334"><strong>範例</strong></span><span class="sxs-lookup"><span data-stu-id="6bbec-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="6bbec-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="6bbec-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-336">數值運算式中使用的數學運算子。</span><span class="sxs-lookup"><span data-stu-id="6bbec-336">Math operators used in numerical expressions.</span></span>
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
    <span data-ttu-id="6bbec-337">指派。</span><span class="sxs-lookup"><span data-stu-id="6bbec-337">Assignment.</span></span> <span data-ttu-id="6bbec-338">將語句右邊的值指派給左邊的物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
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
    <span data-ttu-id="6bbec-339">相等。</span><span class="sxs-lookup"><span data-stu-id="6bbec-339">Equality.</span></span> <span data-ttu-id="6bbec-340">如果值相等，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="6bbec-341">（請注意 `=` 運算子和 `==` 運算子之間的區別）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
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
    <span data-ttu-id="6bbec-342">不等。</span><span class="sxs-lookup"><span data-stu-id="6bbec-342">Inequality.</span></span> <span data-ttu-id="6bbec-343">如果值不相等，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-343">Returns `true` if the values are not equal.</span></span>
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
    <span data-ttu-id="6bbec-344">小於、大於、小於或等於，且大於或等於的情況下。</span><span class="sxs-lookup"><span data-stu-id="6bbec-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
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
    <span data-ttu-id="6bbec-345">串連，用來聯結字串。</span><span class="sxs-lookup"><span data-stu-id="6bbec-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="6bbec-346">ASP.NET 會根據運算式的資料類型，知道這個運算子和加號之間的差異。</span><span class="sxs-lookup"><span data-stu-id="6bbec-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="6bbec-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="6bbec-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-348">遞增和遞減運算子，會從變數相加和減去1（分別為）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
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
    <span data-ttu-id="6bbec-349">網點.</span><span class="sxs-lookup"><span data-stu-id="6bbec-349">Dot.</span></span> <span data-ttu-id="6bbec-350">用來區別物件及其屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-350">Used to distinguish objects and their properties and methods.</span></span>
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
    <span data-ttu-id="6bbec-351">後.</span><span class="sxs-lookup"><span data-stu-id="6bbec-351">Parentheses.</span></span> <span data-ttu-id="6bbec-352">用來將運算式分組，並將參數傳遞給方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-352">Used to group expressions and to pass parameters to methods.</span></span>
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
    <span data-ttu-id="6bbec-353">內.</span><span class="sxs-lookup"><span data-stu-id="6bbec-353">Brackets.</span></span> <span data-ttu-id="6bbec-354">用來存取陣列或集合中的值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-354">Used for accessing values in arrays or collections.</span></span>
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
    <span data-ttu-id="6bbec-355">並非.</span><span class="sxs-lookup"><span data-stu-id="6bbec-355">Not.</span></span> <span data-ttu-id="6bbec-356">將 `true` 值反轉為 `false`，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="6bbec-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="6bbec-357">通常用來做為測試 `false` 的簡短方式（也就是不 `true`）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="6bbec-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="6bbec-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="6bbec-359">邏輯 AND 和 OR，用來將條件連結在一起。</span><span class="sxs-lookup"><span data-stu-id="6bbec-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="6bbec-360">在程式碼中使用檔案和資料夾路徑</span><span class="sxs-lookup"><span data-stu-id="6bbec-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="6bbec-361">您通常會使用程式碼中的檔案和資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="6bbec-362">以下是網站的實體資料夾結構範例，因為它可能會出現在您的開發電腦上：</span><span class="sxs-lookup"><span data-stu-id="6bbec-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="6bbec-363">以下是一些有關 Url 和路徑的基本詳細資料：</span><span class="sxs-lookup"><span data-stu-id="6bbec-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="6bbec-364">URL 的開頭是功能變數名稱（`http://www.example.com`）或伺服器名稱（`http://localhost`，`http://mycomputer`）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="6bbec-365">URL 會對應至主機電腦上的實體路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="6bbec-366">例如，`http://myserver` 可能對應到伺服器上的*C:\websites\mywebsite*資料夾。</span><span class="sxs-lookup"><span data-stu-id="6bbec-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="6bbec-367">虛擬路徑是用來在程式碼中表示路徑的速記，而不需要指定完整路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="6bbec-368">它包含在網域或伺服器名稱後面的 URL 部分。</span><span class="sxs-lookup"><span data-stu-id="6bbec-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="6bbec-369">當您使用虛擬路徑時，您可以將程式碼移至不同的網域或伺服器，而不需要更新路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="6bbec-370">以下是可協助您瞭解差異的範例：</span><span class="sxs-lookup"><span data-stu-id="6bbec-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="6bbec-371">完成 URL</span><span class="sxs-lookup"><span data-stu-id="6bbec-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="6bbec-372">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="6bbec-372">Server name</span></span> | <span data-ttu-id="6bbec-373">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="6bbec-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="6bbec-374">虛擬路徑</span><span class="sxs-lookup"><span data-stu-id="6bbec-374">Virtual path</span></span> | <span data-ttu-id="6bbec-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="6bbec-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="6bbec-376">實體路徑</span><span class="sxs-lookup"><span data-stu-id="6bbec-376">Physical path</span></span> | <span data-ttu-id="6bbec-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="6bbec-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="6bbec-378">虛擬根目錄是/，就像 C：磁片磁碟機的根目錄一樣。</span><span class="sxs-lookup"><span data-stu-id="6bbec-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="6bbec-379">（虛擬資料夾路徑一律使用正斜線）。資料夾的虛擬路徑不一定要有與實體資料夾相同的名稱;它可以是別名。</span><span class="sxs-lookup"><span data-stu-id="6bbec-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="6bbec-380">（在實際執行伺服器上，虛擬路徑很少會符合確切的實體路徑）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="6bbec-381">當您在程式碼中使用檔案和資料夾時，有時候您必須參考實體路徑，有時也需要參照虛擬路徑，視您使用的物件而定。</span><span class="sxs-lookup"><span data-stu-id="6bbec-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="6bbec-382">ASP.NET 提供這些工具，讓您在程式碼中使用檔案和資料夾路徑： `Server.MapPath` 方法，以及 `~` 運算子和 `Href` 方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="6bbec-383">將虛擬轉換成實體路徑：伺服器. MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="6bbec-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="6bbec-384">`Server.MapPath` 方法會將虛擬路徑（例如 */default.cshtml*）轉換為絕對實體路徑（例如*C:\WebSites\MyWebSiteFolder\default.cshtml*）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="6bbec-385">每當您需要完整的實體路徑時，都可以使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="6bbec-386">典型的範例是當您在 web 伺服器上讀取或寫入文字檔或影像檔案時。</span><span class="sxs-lookup"><span data-stu-id="6bbec-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="6bbec-387">您通常不知道網站在主控網站伺服器上的絕對實體路徑，因此這個方法可以將您知道的路徑（虛擬路徑）轉換成伺服器上的對應路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="6bbec-388">您會將檔案或資料夾的虛擬路徑傳遞至方法，並傳回實體路徑：</span><span class="sxs-lookup"><span data-stu-id="6bbec-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="6bbec-389">參考虛擬根目錄： ~ 運算子和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="6bbec-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="6bbec-390">在*cshtml*或*vbhtml*檔案中，您可以使用 `~` 運算子來參考虛擬根路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="6bbec-391">這非常方便，因為您可以在網站中移動頁面，而其包含的任何連結也不會中斷。</span><span class="sxs-lookup"><span data-stu-id="6bbec-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="6bbec-392">如果您將網站移至不同的位置，這也很方便。</span><span class="sxs-lookup"><span data-stu-id="6bbec-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="6bbec-393">以下是一些範例：</span><span class="sxs-lookup"><span data-stu-id="6bbec-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="6bbec-394">如果網站 `http://myserver/myapp`，以下是當頁面執行時，ASP.NET 會如何處理這些路徑：</span><span class="sxs-lookup"><span data-stu-id="6bbec-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="6bbec-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="6bbec-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="6bbec-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="6bbec-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="6bbec-397">（您實際上不會看到這些路徑做為變數的值，但是 ASP.NET 會將這些路徑視為其本身）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="6bbec-398">您可以在伺服器程式碼（如上）和標記中使用 `~` 運算子，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6bbec-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="6bbec-399">在標記中，您可以使用 `~` 運算子來建立資源的路徑，例如影像檔、其他網頁和 CSS 檔案。</span><span class="sxs-lookup"><span data-stu-id="6bbec-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="6bbec-400">當頁面執行時，ASP.NET 會查看頁面（程式碼和標記），並將所有 `~` 參考解析為適當的路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="6bbec-401">條件式邏輯和迴圈</span><span class="sxs-lookup"><span data-stu-id="6bbec-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="6bbec-402">ASP.NET 伺服器程式碼可讓您根據條件執行工作，並撰寫會重複語句的程式碼特定次數（也就是執行迴圈的程式碼）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="6bbec-403">測試條件</span><span class="sxs-lookup"><span data-stu-id="6bbec-403">Testing Conditions</span></span>

<span data-ttu-id="6bbec-404">若要測試簡單的條件，請使用 `if` 語句，這會根據您指定的測試傳回 true 或 false：</span><span class="sxs-lookup"><span data-stu-id="6bbec-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="6bbec-405">`if` 關鍵字會啟動區塊。</span><span class="sxs-lookup"><span data-stu-id="6bbec-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="6bbec-406">實際測試（條件）在括弧中，並傳回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="6bbec-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="6bbec-407">如果測試為 true，則執行的語句會以大括弧括住。</span><span class="sxs-lookup"><span data-stu-id="6bbec-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="6bbec-408">`if` 語句可以包含 `else` 區塊，指定當條件為 false 時要執行的語句：</span><span class="sxs-lookup"><span data-stu-id="6bbec-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="6bbec-409">您可以使用 `else if` 區塊來新增多個條件：</span><span class="sxs-lookup"><span data-stu-id="6bbec-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="6bbec-410">在此範例中，如果 if 區塊中的第一個條件不是 true，則會核取 [`else if`] 條件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="6bbec-411">如果符合該條件，就會執行 `else if` 區塊中的語句。</span><span class="sxs-lookup"><span data-stu-id="6bbec-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="6bbec-412">如果沒有符合任何條件，則會執行 `else` 區塊中的語句。</span><span class="sxs-lookup"><span data-stu-id="6bbec-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="6bbec-413">您可以新增任意數目的 if 區塊，然後以 `else` 區塊關閉，因為 &quot;所有其他專案&quot; 條件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="6bbec-414">若要測試大量的條件，請使用 `switch` 組塊：</span><span class="sxs-lookup"><span data-stu-id="6bbec-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="6bbec-415">要測試的值是以括弧括住（在範例中為 `weekday` 變數）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="6bbec-416">每個個別測試都會使用以冒號（:) 結尾的 `case` 語句。</span><span class="sxs-lookup"><span data-stu-id="6bbec-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="6bbec-417">如果 `case` 語句的值符合測試值，則會執行該案例區塊中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bbec-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="6bbec-418">您可以使用 `break` 語句來關閉每個 case 語句。</span><span class="sxs-lookup"><span data-stu-id="6bbec-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="6bbec-419">（如果您忘了在每個 `case` 區塊中包含 break，則下一個 `case` 語句的程式碼也會執行）。`switch` 區塊通常會有 `default` 的語句做為 &quot;所有其他情況的&quot; 選項（如果沒有其他情況成立）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="6bbec-420">在瀏覽器中顯示的最後兩個條件式區塊的結果：</span><span class="sxs-lookup"><span data-stu-id="6bbec-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="6bbec-422">迴圈程式碼</span><span class="sxs-lookup"><span data-stu-id="6bbec-422">Looping Code</span></span>

<span data-ttu-id="6bbec-423">您通常需要重複執行相同的語句。</span><span class="sxs-lookup"><span data-stu-id="6bbec-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="6bbec-424">您可以藉由迴圈來完成這項操作。</span><span class="sxs-lookup"><span data-stu-id="6bbec-424">You do this by looping.</span></span> <span data-ttu-id="6bbec-425">例如，您通常會針對資料集合中的每個專案執行相同的語句。</span><span class="sxs-lookup"><span data-stu-id="6bbec-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="6bbec-426">如果您確切知道您想要迴圈的次數，可以使用 `for` 迴圈。</span><span class="sxs-lookup"><span data-stu-id="6bbec-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="6bbec-427">這種迴圈特別適合用來計算或計數：</span><span class="sxs-lookup"><span data-stu-id="6bbec-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="6bbec-428">迴圈會以 `for` 關鍵字開頭，後面接著以括弧括住的三個語句，每個都以分號結束。</span><span class="sxs-lookup"><span data-stu-id="6bbec-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="6bbec-429">在括弧內，第一個語句（`var i=10;`）會建立一個計數器，並將它初始化為10個。</span><span class="sxs-lookup"><span data-stu-id="6bbec-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="6bbec-430">您不需要將計數器命名 `i` &#8212;您可以使用任何變數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="6bbec-431">當 `for` 迴圈執行時，計數器會自動遞增。</span><span class="sxs-lookup"><span data-stu-id="6bbec-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="6bbec-432">第二個語句（`i < 21;`）會設定您想要計算的距離條件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="6bbec-433">在此情況下，您想要將它移到最多20個（也就是，在計數器小於21時繼續進行）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="6bbec-434">第三個語句（`i++`）使用遞增運算子，這只會指定在每次執行迴圈時，計數器應該加入1。</span><span class="sxs-lookup"><span data-stu-id="6bbec-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="6bbec-435">括弧內的程式碼會針對迴圈的每個反復專案執行。</span><span class="sxs-lookup"><span data-stu-id="6bbec-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="6bbec-436">標記會每次建立新的段落（`<p>` 元素），並在輸出中加入一行，顯示 `i` （計數器）的值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="6bbec-437">當您執行此頁面時，此範例會建立顯示輸出的11行，而每一行中的文字會指出專案編號。</span><span class="sxs-lookup"><span data-stu-id="6bbec-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="6bbec-439">如果您使用的是集合或陣列，通常會使用 `foreach` 迴圈。</span><span class="sxs-lookup"><span data-stu-id="6bbec-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="6bbec-440">集合是一組類似的物件，而 `foreach` 迴圈可讓您在集合中的每個專案上執行工作。</span><span class="sxs-lookup"><span data-stu-id="6bbec-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="6bbec-441">這種類型的迴圈對集合很方便，因為與 `for` 迴圈不同的是，您不需要遞增計數器或設定限制。</span><span class="sxs-lookup"><span data-stu-id="6bbec-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="6bbec-442">相反地，`foreach` 迴圈程式碼只會繼續完成集合，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="6bbec-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="6bbec-443">例如，下列程式碼會傳回 `Request.ServerVariables` 集合中的專案，這是包含您的 web 伺服器相關資訊的物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="6bbec-444">它會使用 `foreac` h 迴圈來顯示每個專案的名稱，方法是在 HTML 項目符號清單中建立新的 `<li>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6bbec-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="6bbec-445">`foreach` 關鍵字後面加上括弧，您可以在其中宣告代表集合中單一專案的變數（在範例中，`var item`），後面接著 `in` 關鍵字，後面接著您要迴圈執行的集合。</span><span class="sxs-lookup"><span data-stu-id="6bbec-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="6bbec-446">在 `foreach` 迴圈的主體中，您可以使用先前宣告的變數來存取目前的專案。</span><span class="sxs-lookup"><span data-stu-id="6bbec-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="6bbec-448">若要建立更一般用途的迴圈，請使用 `while` 語句：</span><span class="sxs-lookup"><span data-stu-id="6bbec-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="6bbec-449">`while` 迴圈是以 `while` 關鍵字開頭，後面接著括弧，您可以在其中指定迴圈繼續的時間（在這裡，只要 `countNum` 小於50），就會重複區塊。</span><span class="sxs-lookup"><span data-stu-id="6bbec-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="6bbec-450">迴圈通常會遞增（加入）或遞減（減去）用來計算的變數或物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="6bbec-451">在此範例中，`+=` 運算子會在每次執行迴圈時，將1新增至 `countNum`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="6bbec-452">（若要遞減迴圈中計數的變數，您可以使用遞減運算子 `-=`）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="6bbec-453">物件和集合</span><span class="sxs-lookup"><span data-stu-id="6bbec-453">Objects and Collections</span></span>

<span data-ttu-id="6bbec-454">ASP.NET 網站中幾乎所有內容都是物件，包括網頁本身。</span><span class="sxs-lookup"><span data-stu-id="6bbec-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="6bbec-455">本節討論您在程式碼中經常使用的一些重要物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="6bbec-456">頁面物件</span><span class="sxs-lookup"><span data-stu-id="6bbec-456">Page Objects</span></span>

<span data-ttu-id="6bbec-457">ASP.NET 中最基本的物件是頁面。</span><span class="sxs-lookup"><span data-stu-id="6bbec-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="6bbec-458">您可以直接存取頁面物件的屬性，而不需要任何限定的物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="6bbec-459">下列程式碼會使用頁面的 `Request` 物件，取得頁面的檔案路徑：</span><span class="sxs-lookup"><span data-stu-id="6bbec-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="6bbec-460">若要清楚指出您是在目前頁面物件上參考屬性和方法，您可以選擇性地使用關鍵字 `this` 來代表程式碼中的頁面物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="6bbec-461">以下是先前的程式碼範例，加上 `this` 以代表該頁面：</span><span class="sxs-lookup"><span data-stu-id="6bbec-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="6bbec-462">您可以使用 `Page` 物件的屬性來取得大量資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="6bbec-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="6bbec-463">`Request`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-463">`Request`.</span></span> <span data-ttu-id="6bbec-464">如您所見，這是目前要求的相關資訊集合，包括提出要求的瀏覽器類型、頁面的 URL、使用者身分識別等。</span><span class="sxs-lookup"><span data-stu-id="6bbec-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="6bbec-465">`Response`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-465">`Response`.</span></span> <span data-ttu-id="6bbec-466">這是在伺服器程式碼完成執行時，將會傳送至瀏覽器的回應（頁面）相關資訊集合。</span><span class="sxs-lookup"><span data-stu-id="6bbec-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="6bbec-467">例如，您可以使用這個屬性將資訊寫入至回應。</span><span class="sxs-lookup"><span data-stu-id="6bbec-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="6bbec-468">集合物件（陣列和字典）</span><span class="sxs-lookup"><span data-stu-id="6bbec-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="6bbec-469">*集合*是一組相同類型的物件，例如從資料庫 `Customer` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="6bbec-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="6bbec-470">ASP.NET 包含許多內建集合，例如 `Request.Files` 集合。</span><span class="sxs-lookup"><span data-stu-id="6bbec-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="6bbec-471">您通常會使用集合中的資料。</span><span class="sxs-lookup"><span data-stu-id="6bbec-471">You'll often work with data in collections.</span></span> <span data-ttu-id="6bbec-472">有兩個常見的集合類型是*陣列*和*字典*。</span><span class="sxs-lookup"><span data-stu-id="6bbec-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="6bbec-473">當您想要儲存類似專案的集合，但不想要建立個別的變數來保存每個專案時，陣列會很有用：</span><span class="sxs-lookup"><span data-stu-id="6bbec-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="6bbec-474">使用陣列，您可以宣告特定的資料類型，例如 `string`、`int`或 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="6bbec-475">若要指出變數可以包含陣列，您可以在宣告中加上括弧（例如 `string[]` 或 `int[]`）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="6bbec-476">您可以使用物件的位置（索引），或使用 `foreach` 語句來存取陣列中的專案。</span><span class="sxs-lookup"><span data-stu-id="6bbec-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="6bbec-477">陣列索引以零&#8212;為起始，亦即，第一個專案位於位置0，第二個專案位於位置1，依此類推。</span><span class="sxs-lookup"><span data-stu-id="6bbec-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="6bbec-478">您可以藉由取得 `Length` 屬性來判斷陣列中的專案數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="6bbec-479">若要取得陣列中特定專案的位置（以搜尋陣列），請使用 `Array.IndexOf` 方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="6bbec-480">您也可以執行一些動作，像是反轉陣列的內容（`Array.Reverse` 方法）或排序內容（`Array.Sort` 方法）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="6bbec-481">在瀏覽器中顯示的字串陣列程式碼輸出：</span><span class="sxs-lookup"><span data-stu-id="6bbec-481">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="6bbec-483">字典是索引鍵/值組的集合，您可以在其中提供用來設定或抓取對應值的索引鍵（或名稱）：</span><span class="sxs-lookup"><span data-stu-id="6bbec-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="6bbec-484">若要建立字典，您可以使用 `new` 關鍵字來表示您要建立新的字典物件。</span><span class="sxs-lookup"><span data-stu-id="6bbec-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="6bbec-485">您可以使用 `var` 關鍵字，將字典指派給變數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="6bbec-486">您可以使用角括弧（`< >`）來指示字典中專案的資料類型。</span><span class="sxs-lookup"><span data-stu-id="6bbec-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="6bbec-487">在宣告的結尾，您必須加入一對括弧，因為這實際上是建立新字典的方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="6bbec-488">若要將專案加入至字典，您可以呼叫 dictionary 變數的 `Add` 方法（在此案例中為`myScores`），然後指定索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="6bbec-489">或者，您可以使用方括弧來表示金鑰，並執行簡單的指派，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6bbec-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="6bbec-490">若要從字典取得值，請在括弧中指定索引鍵：</span><span class="sxs-lookup"><span data-stu-id="6bbec-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="6bbec-491">使用參數呼叫方法</span><span class="sxs-lookup"><span data-stu-id="6bbec-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="6bbec-492">如您稍早在本文中所閱讀，使用進行程式設計的物件可以有方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="6bbec-493">例如，`Database` 物件可能會有 `Database.Connect` 的方法。</span><span class="sxs-lookup"><span data-stu-id="6bbec-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="6bbec-494">許多方法也有一或多個參數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="6bbec-495">*參數*是您傳遞給方法的值，可讓方法完成其工作。</span><span class="sxs-lookup"><span data-stu-id="6bbec-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="6bbec-496">例如，查看 `Request.MapPath` 方法的宣告，其採用三個參數：</span><span class="sxs-lookup"><span data-stu-id="6bbec-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="6bbec-497">（這一行已包裝，使其更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="6bbec-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="6bbec-498">請記住，除了括在引號中的字串之外，您幾乎可以在任何地方放置分行符號）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="6bbec-499">這個方法會傳回伺服器上對應至指定虛擬路徑的實體路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="6bbec-500">方法的三個參數是 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="6bbec-501">（請注意，在宣告中，參數會列出其接受的資料類型）。當您呼叫這個方法時，您必須提供所有三個參數的值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="6bbec-502">Razor 語法提供兩個選項，讓您將參數傳遞給方法：*位置參數*和*具名引數*。</span><span class="sxs-lookup"><span data-stu-id="6bbec-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="6bbec-503">若要使用位置參數呼叫方法，請以方法宣告中指定的嚴格順序來傳遞參數。</span><span class="sxs-lookup"><span data-stu-id="6bbec-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="6bbec-504">（您通常會藉由閱讀方法的檔來得知此順序）。您必須遵循順序，而且如果有必要，就無法略過&#8212;任何參數，您可以為沒有值的位置參數傳遞空字串（`""`）或 `null`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="6bbec-505">下列範例假設您的網站上有一個名為 [*腳本*] 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6bbec-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="6bbec-506">程式碼會呼叫 `Request.MapPath` 方法，並以正確的順序傳遞三個參數的值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="6bbec-507">然後，它會顯示所產生的對應路徑。</span><span class="sxs-lookup"><span data-stu-id="6bbec-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="6bbec-508">當方法有許多參數時，您可以使用具名引數，讓您的程式碼更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="6bbec-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="6bbec-509">若要使用具名引數來呼叫方法，請指定參數名稱，後面接著冒號（:)，然後是值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="6bbec-510">具名引數的優點是您可以依照您想要的任何順序傳遞它們。</span><span class="sxs-lookup"><span data-stu-id="6bbec-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="6bbec-511">（缺點是方法呼叫不是精簡的）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="6bbec-512">下列範例會呼叫與上述相同的方法，但會使用具名引數來提供值：</span><span class="sxs-lookup"><span data-stu-id="6bbec-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="6bbec-513">如您所見，參數會以不同的順序傳遞。</span><span class="sxs-lookup"><span data-stu-id="6bbec-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="6bbec-514">不過，如果您執行上述範例和此範例，則會傳回相同的值。</span><span class="sxs-lookup"><span data-stu-id="6bbec-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="6bbec-515">處理錯誤</span><span class="sxs-lookup"><span data-stu-id="6bbec-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="6bbec-516">Try-catch 語句</span><span class="sxs-lookup"><span data-stu-id="6bbec-516">Try-Catch Statements</span></span>

<span data-ttu-id="6bbec-517">您的程式碼中通常會有語句，可能會因為控制項以外的原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="6bbec-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="6bbec-518">例如：</span><span class="sxs-lookup"><span data-stu-id="6bbec-518">For example:</span></span>

- <span data-ttu-id="6bbec-519">如果您的程式碼嘗試建立或存取檔案，可能會發生各種錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bbec-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="6bbec-520">您想要的檔案可能不存在、可能被鎖定、程式碼可能沒有許可權等等。</span><span class="sxs-lookup"><span data-stu-id="6bbec-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="6bbec-521">同樣地，如果您的程式碼嘗試更新資料庫中的記錄，可能會有許可權問題，可能會卸載與資料庫的連接、要儲存的資料可能無效等等。</span><span class="sxs-lookup"><span data-stu-id="6bbec-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="6bbec-522">在程式設計的詞彙中，這些情況稱為*例外*狀況。</span><span class="sxs-lookup"><span data-stu-id="6bbec-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="6bbec-523">如果您的程式碼遇到例外狀況，它會產生（擲回）一則錯誤訊息，其中最棒的是使用者很討厭：</span><span class="sxs-lookup"><span data-stu-id="6bbec-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="6bbec-525">在您的程式碼可能會遇到例外狀況的情況下，為了避免這種類型的錯誤訊息，您可以使用 `try/catch` 語句。</span><span class="sxs-lookup"><span data-stu-id="6bbec-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="6bbec-526">在 `try` 語句中，您會執行您要檢查的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bbec-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="6bbec-527">在一或多個 `catch` 語句中，您可以尋找可能發生的特定錯誤（特定類型的例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="6bbec-528">您可以視需要包含多個 `catch` 語句，以尋找您預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bbec-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbec-529">我們建議您避免在 `try/catch` 語句中使用 `Response.Redirect` 方法，因為它可能會在您的頁面中造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6bbec-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="6bbec-530">下列範例顯示的頁面會在第一個要求上建立文字檔，然後顯示一個按鈕，讓使用者開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="6bbec-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="6bbec-531">此範例刻意使用錯誤的檔案名，因此會造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6bbec-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="6bbec-532">此程式碼包含兩個可能例外狀況的 `catch` 語句： `FileNotFoundException`，如果檔案名不正確，就會發生這種情況，如果 ASP.NET 找不到資料夾，就會發生 `DirectoryNotFoundException`。</span><span class="sxs-lookup"><span data-stu-id="6bbec-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="6bbec-533">（您可以將範例中的語句取消批註，以便在所有專案正常運作時查看其執行方式）。</span><span class="sxs-lookup"><span data-stu-id="6bbec-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="6bbec-534">如果您的程式碼未處理例外狀況，您會看到如先前螢幕擷取畫面所示的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="6bbec-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="6bbec-535">不過，`try/catch` 區段有助於防止使用者看到這些類型的錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bbec-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="6bbec-536">其他資源</span><span class="sxs-lookup"><span data-stu-id="6bbec-536">Additional Resources</span></span>

<span data-ttu-id="6bbec-537">**使用 Visual Basic 進行程式設計**</span><span class="sxs-lookup"><span data-stu-id="6bbec-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="6bbec-538">附錄： Visual Basic 語言和語法</span><span class="sxs-lookup"><span data-stu-id="6bbec-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="6bbec-539">**參考檔**</span><span class="sxs-lookup"><span data-stu-id="6bbec-539">**Reference Documentation**</span></span>

[<span data-ttu-id="6bbec-540">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6bbec-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="6bbec-541">C#語言</span><span class="sxs-lookup"><span data-stu-id="6bbec-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
