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
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="8d22b-103">使用 Razor 語法 ASP.NET Web 程式設計的簡介（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="8d22b-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="8d22b-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8d22b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8d22b-105">本文提供使用 Razor 語法和 Visual Basic 進行 ASP.NET Web Pages 程式設計的總覽。</span><span class="sxs-lookup"><span data-stu-id="8d22b-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="8d22b-106">ASP.NET 是 Microsoft 在網頁伺服器上執行動態網頁的技術。</span><span class="sxs-lookup"><span data-stu-id="8d22b-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="8d22b-107">**您將瞭解的內容**：</span><span class="sxs-lookup"><span data-stu-id="8d22b-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="8d22b-108">使用 Razor 語法開始進行程式設計 ASP.NET Web Pages 的前8個程式設計秘訣。</span><span class="sxs-lookup"><span data-stu-id="8d22b-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="8d22b-109">您需要的基本程式設計概念。</span><span class="sxs-lookup"><span data-stu-id="8d22b-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="8d22b-110">什麼是 ASP.NET 伺服器程式碼和 Razor 語法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8d22b-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="8d22b-111">軟體版本</span><span class="sxs-lookup"><span data-stu-id="8d22b-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="8d22b-112">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="8d22b-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="8d22b-113">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="8d22b-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="8d22b-114">使用 ASP.NET Web Pages 搭配 Razor 語法的大部分範例C#。</span><span class="sxs-lookup"><span data-stu-id="8d22b-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="8d22b-115">但是 Razor 語法也支援 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="8d22b-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="8d22b-116">若要在 Visual Basic 中程式設計 ASP.NET 網頁，請建立副檔名為*vbhtml*的網頁，然後加入 Visual Basic 碼。</span><span class="sxs-lookup"><span data-stu-id="8d22b-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="8d22b-117">本文可讓您瞭解如何使用 Visual Basic 語言和語法來建立 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="8d22b-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="8d22b-118">C#和 Visual Basic 版本中提供 Microsoft WebMatrix 的預設網站範本（**麵包店**、**相片圖庫**和**入門網站**等等）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="8d22b-119">您可以將 Visual Basic 範本安裝為 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="8d22b-120">網站範本會安裝在您網站的根資料夾中，名為*Microsoft templates*的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="8d22b-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="8d22b-121">前8個程式設計提示</span><span class="sxs-lookup"><span data-stu-id="8d22b-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="8d22b-122">本節列出當您使用 Razor 語法開始撰寫 ASP.NET 伺服器程式碼時，您絕對需要知道的幾個秘訣。</span><span class="sxs-lookup"><span data-stu-id="8d22b-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="8d22b-123">1. 使用 @ 字元將程式碼加入至頁面</span><span class="sxs-lookup"><span data-stu-id="8d22b-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="8d22b-124">`@` 字元會啟動內嵌運算式、單一語句區塊和多重語句區塊：</span><span class="sxs-lookup"><span data-stu-id="8d22b-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="8d22b-125">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="8d22b-127">**HTML 編碼**</span><span class="sxs-lookup"><span data-stu-id="8d22b-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="8d22b-128">當您使用 `@` 字元在頁面中顯示內容時（如上述範例所示），ASP.NET 會以 HTML 編碼輸出。</span><span class="sxs-lookup"><span data-stu-id="8d22b-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="8d22b-129">這會將保留的 HTML 字元（例如 `<` 和 `>` 和 `&`）取代為程式碼，讓字元在網頁中顯示為字元，而不是被轉譯為 HTML 標籤或實體。</span><span class="sxs-lookup"><span data-stu-id="8d22b-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="8d22b-130">如果沒有 HTML 編碼，來自您的伺服器程式碼的輸出可能無法正確顯示，而且可能會讓頁面暴露于安全性風險下。</span><span class="sxs-lookup"><span data-stu-id="8d22b-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="8d22b-131">如果您的目標是要輸出將標記轉譯為標記的 HTML 標籤（例如 `<p></p>` 用於段落或 `<em></em>` 強調文字），請參閱本文稍後的在程式[代碼區塊中結合文字、標記和程式碼](#BM_CombiningTextMarkupAndCode)一節。</span><span class="sxs-lookup"><span data-stu-id="8d22b-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="8d22b-132">若要深入瞭解 HTML 編碼，請參閱[使用 ASP.NET Web Pages 網站中的 Html 表單](https://go.microsoft.com/fwlink/?LinkId=202892)。</span><span class="sxs-lookup"><span data-stu-id="8d22b-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="8d22b-133">2. 以程式碼括住程式碼區塊 .。。結束代碼</span><span class="sxs-lookup"><span data-stu-id="8d22b-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="8d22b-134">程式碼區塊包含一或多個程式碼語句，並以 `Code` 和 `End Code`的關鍵字括住。</span><span class="sxs-lookup"><span data-stu-id="8d22b-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="8d22b-135">將開頭的 `Code` 關鍵字緊接在 `@` 字元&#8212;之後，其之間不能有空格。</span><span class="sxs-lookup"><span data-stu-id="8d22b-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="8d22b-136">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="8d22b-138">3. 在區塊內，您會結束每個程式碼語句並加上分行符號</span><span class="sxs-lookup"><span data-stu-id="8d22b-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="8d22b-139">在 Visual Basic 的程式碼區塊中，每個語句的結尾都是分行符號。</span><span class="sxs-lookup"><span data-stu-id="8d22b-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="8d22b-140">（稍後在本文中，您會看到一個將長程式碼語句包裝成多行（如有需要）的方法）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="8d22b-141">4. 您可以使用變數來儲存值</span><span class="sxs-lookup"><span data-stu-id="8d22b-141">4. You use variables to store values</span></span>

<span data-ttu-id="8d22b-142">您可以將值儲存在*變數*中，包括字串、數位和日期等等。您可以使用 `Dim` 關鍵字來建立新的變數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="8d22b-143">您可以使用 `@`，直接在頁面中插入變數值。</span><span class="sxs-lookup"><span data-stu-id="8d22b-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="8d22b-144">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="8d22b-146">5. 用雙引號括住常值字串</span><span class="sxs-lookup"><span data-stu-id="8d22b-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="8d22b-147">*字串*是視為文字的字元序列。</span><span class="sxs-lookup"><span data-stu-id="8d22b-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="8d22b-148">若要指定字串，請將其括在雙引號內：</span><span class="sxs-lookup"><span data-stu-id="8d22b-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="8d22b-149">若要在字串值內內嵌雙引號，請插入兩個雙引號字元。</span><span class="sxs-lookup"><span data-stu-id="8d22b-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="8d22b-150">如果您想要在頁面輸出中出現雙引號一次，請在加上引號的字串中輸入 `""`，如果您希望它出現兩次，請在加上引號的字串中輸入 `""""`。</span><span class="sxs-lookup"><span data-stu-id="8d22b-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="8d22b-151">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="8d22b-153">6. Visual Basic 程式碼不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8d22b-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="8d22b-154">Visual Basic 語言不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8d22b-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="8d22b-155">程式設計關鍵字（例如 `Dim`、`If`和 `True`）和變數名稱（例如 `myString`或 `subTotal`）可在任何情況下寫入。</span><span class="sxs-lookup"><span data-stu-id="8d22b-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="8d22b-156">下列幾行程式碼會使用小寫名稱將值指派給變數 `lastname`，然後使用大寫名稱將變數值輸出至頁面。</span><span class="sxs-lookup"><span data-stu-id="8d22b-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="8d22b-157">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-157">The result displayed in a browser:</span></span>

![vb-語法-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="8d22b-159">7. 您的程式碼大部分都牽涉到使用物件</span><span class="sxs-lookup"><span data-stu-id="8d22b-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="8d22b-160">物件代表您可以使用&#8212;頁面、文字方塊、檔案、影像、web 要求、電子郵件訊息、客戶記錄（資料庫資料列）等進行程式設計的東西。物件具有描述其特性&#8212;的屬性：文字方塊物件具有 `Text` 屬性、要求物件具有 `Url` 屬性、電子郵件訊息具有 `From` 屬性，以及客戶物件具有 `FirstName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="8d22b-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="8d22b-161">物件也有 &quot;動詞&quot; 可以執行的方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="8d22b-162">範例包括 file 物件的 `Save` 方法、影像物件的 `Rotate` 方法，以及電子郵件物件的 `Send` 方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="8d22b-163">您通常會使用 `Request` 物件，這會提供如頁面上表單欄位的值（文字方塊等）、建立要求的瀏覽器類型、頁面的 URL、使用者身分識別等資訊。這個範例會示範如何存取 `Request` 物件的屬性，以及如何呼叫 `Request` 物件的 `MapPath` 方法，這會提供您伺服器上頁面的絕對路徑：</span><span class="sxs-lookup"><span data-stu-id="8d22b-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="8d22b-164">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="8d22b-166">8. 您可以撰寫程式碼來做出決策</span><span class="sxs-lookup"><span data-stu-id="8d22b-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="8d22b-167">動態網頁的主要功能是，您可以根據條件來決定要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="8d22b-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="8d22b-168">最常見的做法是使用 `If` 語句（和選擇性的 `Else` 語句）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="8d22b-169">語句 `If IsPost` 是撰寫 `If IsPost = True`的簡寫方式。</span><span class="sxs-lookup"><span data-stu-id="8d22b-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="8d22b-170">除了 `If` 語句之外，還有各種不同的方法可以測試條件、重複的程式碼區塊等等，本文稍後會加以說明。</span><span class="sxs-lookup"><span data-stu-id="8d22b-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="8d22b-171">在瀏覽器中顯示的結果（按一下 [**提交**] 之後）：</span><span class="sxs-lookup"><span data-stu-id="8d22b-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="8d22b-173">**HTTP GET 和 POST 方法和 IsPost 屬性**</span><span class="sxs-lookup"><span data-stu-id="8d22b-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="8d22b-174">網頁（HTTP）所使用的通訊協定支援非常有限的方法數（&quot;動詞&quot;），可用來對伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="8d22b-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="8d22b-175">最常見的兩個是 GET，用來讀取頁面和 POST （用來提交頁面）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="8d22b-176">一般情況下，使用者第一次要求頁面時，會使用 GET 來要求頁面。</span><span class="sxs-lookup"><span data-stu-id="8d22b-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="8d22b-177">如果使用者填滿表單，然後按一下 [**提交**]，則瀏覽器會對伺服器提出 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="8d22b-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="8d22b-178">在 web 程式設計中，知道頁面是否以 GET 或 POST 的方式要求，讓您知道如何處理頁面，通常會很有説明。</span><span class="sxs-lookup"><span data-stu-id="8d22b-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="8d22b-179">在 ASP.NET Web Pages 中，您可以使用 [`IsPost`] 屬性來查看要求是 GET 或 POST。</span><span class="sxs-lookup"><span data-stu-id="8d22b-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="8d22b-180">如果要求是 POST，`IsPost` 屬性會傳回 true，而您可以執行讀取表單上文字方塊值之類的動作。</span><span class="sxs-lookup"><span data-stu-id="8d22b-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="8d22b-181">您會看到的許多範例會告訴您如何根據 `IsPost`的值，以不同的方式處理頁面。</span><span class="sxs-lookup"><span data-stu-id="8d22b-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="8d22b-182">簡單的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="8d22b-182">A Simple Code Example</span></span>

<span data-ttu-id="8d22b-183">此程式說明如何建立說明基本程式設計技術的頁面。</span><span class="sxs-lookup"><span data-stu-id="8d22b-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="8d22b-184">在此範例中，您會建立可讓使用者輸入兩個數字的頁面，然後將其加入並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="8d22b-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="8d22b-185">在您的編輯器中，建立新的檔案，並將它命名為*AddNumbers*。</span><span class="sxs-lookup"><span data-stu-id="8d22b-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="8d22b-186">將下列程式碼和標記複製到頁面中，並取代頁面中已存在的任何專案。</span><span class="sxs-lookup"><span data-stu-id="8d22b-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="8d22b-187">以下是您要注意的一些事項：</span><span class="sxs-lookup"><span data-stu-id="8d22b-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="8d22b-188">`@` 字元會啟動頁面中第一個程式碼區塊，並在靠近底部的 `totalMessage` 變數之前。</span><span class="sxs-lookup"><span data-stu-id="8d22b-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="8d22b-189">頁面頂端的區塊會以 `Code...End Code`括住。</span><span class="sxs-lookup"><span data-stu-id="8d22b-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="8d22b-190">`total`、`num1`、`num2`和 `totalMessage` 的變數會儲存數個數字和一個字串。</span><span class="sxs-lookup"><span data-stu-id="8d22b-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="8d22b-191">指派給 `totalMessage` 變數的常值字串值是以雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="8d22b-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="8d22b-192">因為 Visual Basic 程式碼不區分大小寫，所以當使用 `totalMessage` 變數接近頁面底部時，其名稱只需要符合頁面頂端的變數宣告拼寫。</span><span class="sxs-lookup"><span data-stu-id="8d22b-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="8d22b-193">大小寫並不重要。</span><span class="sxs-lookup"><span data-stu-id="8d22b-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="8d22b-194">運算式 `num1.AsInt()` + `num2.AsInt()` 會顯示如何使用物件和方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="8d22b-195">每個變數上的 `AsInt` 方法會將使用者輸入的字串，轉換成可新增的整數（整數）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="8d22b-196">`<form>` 標記包含 `method="post"` 屬性。</span><span class="sxs-lookup"><span data-stu-id="8d22b-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="8d22b-197">這會指定當使用者按一下 [**新增**] 時，會使用 HTTP POST 方法將頁面傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="8d22b-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="8d22b-198">提交頁面時，程式碼 `If IsPost` 會評估為 true，並執行條件式程式碼，以顯示加入數位的結果。</span><span class="sxs-lookup"><span data-stu-id="8d22b-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="8d22b-199">儲存頁面，並在瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="8d22b-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="8d22b-200">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）輸入兩個整數，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d22b-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="8d22b-202">Visual Basic 語言和語法</span><span class="sxs-lookup"><span data-stu-id="8d22b-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="8d22b-203">稍早您會看到如何建立 ASP.NET 網頁的基本範例，以及如何將伺服器程式碼加入至 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="8d22b-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="8d22b-204">在這裡，您將瞭解使用 Visual Basic 來撰寫 ASP.NET 伺服器程式碼的基本概念&#8212; ，Razor 語法亦即程式設計語言規則。</span><span class="sxs-lookup"><span data-stu-id="8d22b-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="8d22b-205">如果您對程式設計有經驗（特別是使用 C、 C++、 C#、Visual Basic 或 JavaScript），您在這裡閱讀的大部分內容都很熟悉。</span><span class="sxs-lookup"><span data-stu-id="8d22b-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="8d22b-206">您可能只需要熟悉 WebMatrix 程式碼如何加入至*vbhtml*檔案中的標記。</span><span class="sxs-lookup"><span data-stu-id="8d22b-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a><span data-ttu-id="8d22b-207">結合程式碼區塊中的文字、標記和程式碼</span><span class="sxs-lookup"><span data-stu-id="8d22b-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="8d22b-208">在 [伺服器程式碼區塊] 中，您通常會想要將文字和標記輸出至頁面。</span><span class="sxs-lookup"><span data-stu-id="8d22b-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="8d22b-209">如果伺服器程式碼區塊包含不是程式碼的文字，而應該改為轉譯，則 ASP.NET 必須能夠區別該文字與程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d22b-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="8d22b-210">有數個方式可以執行此動作。</span><span class="sxs-lookup"><span data-stu-id="8d22b-210">There are several ways to do this.</span></span>

- <span data-ttu-id="8d22b-211">將文字括在 HTML 區塊元素中，例如 `<p></p>` 或 `<em></em>`：</span><span class="sxs-lookup"><span data-stu-id="8d22b-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="8d22b-212">HTML 元素可以包含文字、其他 HTML 專案和伺服器程式碼運算式。</span><span class="sxs-lookup"><span data-stu-id="8d22b-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="8d22b-213">當 ASP.NET 看到開頭的 HTML 標籤（例如 `<p>`）時，它會將元素及其內容的所有專案轉譯為瀏覽器（並解析伺服器程式碼運算式）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="8d22b-214">請使用 `@:` 運算子或 `<text>` 元素。</span><span class="sxs-lookup"><span data-stu-id="8d22b-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="8d22b-215">`@:` 輸出包含純文字或不相符 HTML 標籤的單一行內容;`<text>` 元素會將多行括住以輸出。</span><span class="sxs-lookup"><span data-stu-id="8d22b-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="8d22b-216">當您不想要將 HTML 元素轉譯為輸出的一部分時，這些選項會很有用。</span><span class="sxs-lookup"><span data-stu-id="8d22b-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="8d22b-217">下列範例會重複上一個範例，但會使用一對 `<text>` 標記來括住要轉譯的文字。</span><span class="sxs-lookup"><span data-stu-id="8d22b-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="8d22b-218">在下列範例中，`<text>` 和 `</text>` 標記會括住三行，其中全部都有一些非內含性文字和不相符的 HTML 標籤（`<br />`），以及伺服器程式碼和相符的 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="8d22b-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="8d22b-219">同樣地，您也可以分別在每一行的前面加上 `@:` 運算子;任一種方法都可行。</span><span class="sxs-lookup"><span data-stu-id="8d22b-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="8d22b-220">當您&#8212;使用 HTML 專案（如本節所示）輸出文字時，`@:` 運算子或 `<text>` 元素&#8212; ASP.NET 不會對輸出進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="8d22b-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="8d22b-221">（如先前所述，ASP.NET 會對前面加上 `@`的伺服器程式碼運算式和伺服器程式碼區塊的輸出進行編碼，但本節中所述的特殊情況除外）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="8d22b-222">Whitespace</span><span class="sxs-lookup"><span data-stu-id="8d22b-222">Whitespace</span></span>

<span data-ttu-id="8d22b-223">語句（和字串常值外部）中的額外空格不會影響語句：</span><span class="sxs-lookup"><span data-stu-id="8d22b-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="8d22b-224">將長語句細分成多行</span><span class="sxs-lookup"><span data-stu-id="8d22b-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="8d22b-225">在每一行程式碼之後，您可以使用底線字元 `_` （在 Visual Basic 中稱為*接續字元*），將長程式碼語句分解成多行。</span><span class="sxs-lookup"><span data-stu-id="8d22b-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="8d22b-226">若要將語句分成下一行，請在行尾加入一個空格，然後再加上接續字元。</span><span class="sxs-lookup"><span data-stu-id="8d22b-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="8d22b-227">繼續下一行中的語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-227">Continue the statement on the next line.</span></span> <span data-ttu-id="8d22b-228">您可以視需要將語句包裝到多行，以提高可讀性。</span><span class="sxs-lookup"><span data-stu-id="8d22b-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="8d22b-229">下列陳述式是相同的：</span><span class="sxs-lookup"><span data-stu-id="8d22b-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="8d22b-230">不過，您無法在字串常值的中間換行。</span><span class="sxs-lookup"><span data-stu-id="8d22b-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="8d22b-231">下列範例無法使用：</span><span class="sxs-lookup"><span data-stu-id="8d22b-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="8d22b-232">若要結合一個長字串，以包裝到多行（如上述程式碼），您必須使用*串連運算子*（`&`），這將在本文稍後看到。</span><span class="sxs-lookup"><span data-stu-id="8d22b-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="8d22b-233">程式碼批註</span><span class="sxs-lookup"><span data-stu-id="8d22b-233">Code comments</span></span>

<span data-ttu-id="8d22b-234">批註可讓您為自己或其他人留下筆記。</span><span class="sxs-lookup"><span data-stu-id="8d22b-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="8d22b-235">Razor 語法批註的前面會加上 `@*`，並以 `*@`結尾。</span><span class="sxs-lookup"><span data-stu-id="8d22b-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="8d22b-236">在程式碼區塊中，您可以使用 Razor 語法批註，也可以使用一般的 Visual Basic 批註字元，這是每一行前面加上一個單引號（`'`）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="8d22b-237">變數</span><span class="sxs-lookup"><span data-stu-id="8d22b-237">Variables</span></span>

<span data-ttu-id="8d22b-238">變數是您用來儲存資料的已命名物件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="8d22b-239">您可以將變數命名為任何名稱，但名稱必須以字母字元開頭，而且不能包含空格或保留字元。</span><span class="sxs-lookup"><span data-stu-id="8d22b-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="8d22b-240">如先前所見，在 Visual Basic 中，變數名稱中的字母大小寫並不重要。</span><span class="sxs-lookup"><span data-stu-id="8d22b-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="8d22b-241">變數和資料類型</span><span class="sxs-lookup"><span data-stu-id="8d22b-241">Variables and data types</span></span>

<span data-ttu-id="8d22b-242">變數可以具有特定的資料類型，以指出變數中儲存的資料種類。</span><span class="sxs-lookup"><span data-stu-id="8d22b-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="8d22b-243">您可以擁有儲存字串值的字串變數（例如 &quot;Hello world&quot;）、儲存整數值（例如3或79）的整數變數，以及以各種格式（例如4/12/2012 或3月2009）儲存日期值的日期變數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="8d22b-244">而且還有許多其他資料類型可供您使用。</span><span class="sxs-lookup"><span data-stu-id="8d22b-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="8d22b-245">不過，您不需要指定變數的類型。</span><span class="sxs-lookup"><span data-stu-id="8d22b-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="8d22b-246">在大多數情況下，ASP.NET 可以根據變數中的資料使用方式來找出型別。</span><span class="sxs-lookup"><span data-stu-id="8d22b-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="8d22b-247">（有時候您必須指定類型，您將會看到這是 true 的範例）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="8d22b-248">若要宣告變數而不指定類型，請使用 `Dim` 加上變數名稱（例如，`Dim myVar`）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="8d22b-249">若要宣告型別為的變數，請使用 `Dim` 加上變數名稱，後面接著 `As` 然後是型別名稱（例如，`Dim myVar As String`）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="8d22b-250">下列範例顯示使用網頁中之變數的一些內嵌運算式。</span><span class="sxs-lookup"><span data-stu-id="8d22b-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="8d22b-251">在瀏覽器中顯示的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="8d22b-253">轉換和測試資料類型</span><span class="sxs-lookup"><span data-stu-id="8d22b-253">Converting and testing data types</span></span>

<span data-ttu-id="8d22b-254">雖然 ASP.NET 通常可以自動判斷資料類型，但有時卻不能。</span><span class="sxs-lookup"><span data-stu-id="8d22b-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="8d22b-255">因此，您可能需要執行明確轉換來協助 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="8d22b-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="8d22b-256">即使您不需要轉換類型，有時還是可以測試以查看您可能使用的資料類型。</span><span class="sxs-lookup"><span data-stu-id="8d22b-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="8d22b-257">最常見的情況是，您必須將字串轉換成另一種類型，例如整數或日期。</span><span class="sxs-lookup"><span data-stu-id="8d22b-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="8d22b-258">下列範例顯示您必須將字串轉換成數位的一般情況。</span><span class="sxs-lookup"><span data-stu-id="8d22b-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="8d22b-259">就規則而言，使用者輸入會以字串的形式提供給您。</span><span class="sxs-lookup"><span data-stu-id="8d22b-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="8d22b-260">即使您已提示使用者輸入數位，而且即使他們輸入了數位，當使用者輸入提交，而且您在程式碼中讀取時，資料仍會是字串格式。</span><span class="sxs-lookup"><span data-stu-id="8d22b-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="8d22b-261">因此，您必須將字串轉換成數位。</span><span class="sxs-lookup"><span data-stu-id="8d22b-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="8d22b-262">在此範例中，如果您嘗試對值執行算術而不加以轉換，則會產生下列錯誤，因為 ASP.NET 無法加入兩個字串：</span><span class="sxs-lookup"><span data-stu-id="8d22b-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="8d22b-263">若要將值轉換為整數，您可以呼叫 `AsInt` 方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="8d22b-264">如果轉換成功，您可以接著加入數位。</span><span class="sxs-lookup"><span data-stu-id="8d22b-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="8d22b-265">下表列出一些常見的變數轉換和測試方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-265">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="8d22b-266"><strong>方法</strong></span><span class="sxs-lookup"><span data-stu-id="8d22b-266"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="8d22b-267"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="8d22b-267"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="8d22b-268"><strong>範例</strong></span><span class="sxs-lookup"><span data-stu-id="8d22b-268"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="8d22b-269">將代表整數（例如 &quot;593&quot;）的字串轉換為整數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-269">Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
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
        <span data-ttu-id="8d22b-270">將 &quot;true&quot; 或 &quot;false&quot; 之類的字串轉換成布林值類型。</span><span class="sxs-lookup"><span data-stu-id="8d22b-270">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
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
        <span data-ttu-id="8d22b-271">將具有十進位值（例如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字串轉換為浮點數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-271">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
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
        <span data-ttu-id="8d22b-272">將具有十進位值（例如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字串轉換為十進位數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-272">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="8d22b-273">（在 ASP.NET 中，十進位數比浮點數更精確）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-273">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
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
        <span data-ttu-id="8d22b-274">將表示日期和時間值的字串轉換為 ASP.NET `DateTime` 類型。</span><span class="sxs-lookup"><span data-stu-id="8d22b-274">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
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
        <span data-ttu-id="8d22b-275">將任何其他資料類型轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="8d22b-275">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="8d22b-276">運算子</span><span class="sxs-lookup"><span data-stu-id="8d22b-276">Operators</span></span>

<span data-ttu-id="8d22b-277">「運算子」是一個關鍵字或字元，告訴 ASP.NET 要在運算式中執行哪一種命令。</span><span class="sxs-lookup"><span data-stu-id="8d22b-277">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="8d22b-278">Visual Basic 支援許多運算子，但您只需要辨識幾個，就能開始開發 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="8d22b-278">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="8d22b-279">下表摘要說明最常見的運算子。</span><span class="sxs-lookup"><span data-stu-id="8d22b-279">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="8d22b-280"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="8d22b-280"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="8d22b-281"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="8d22b-281"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="8d22b-282"><strong>範例</strong></span><span class="sxs-lookup"><span data-stu-id="8d22b-282"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        <span data-ttu-id="8d22b-283">數值運算式中使用的數學運算子。</span><span class="sxs-lookup"><span data-stu-id="8d22b-283">Math operators used in numerical expressions.</span></span>
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
        <span data-ttu-id="8d22b-284">指派和相等。</span><span class="sxs-lookup"><span data-stu-id="8d22b-284">Assignment and equality.</span></span> <span data-ttu-id="8d22b-285">視內容而定，請將語句右邊的值指派給左邊的物件，或檢查值是否相等。</span><span class="sxs-lookup"><span data-stu-id="8d22b-285">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
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
        <span data-ttu-id="8d22b-286">不等。</span><span class="sxs-lookup"><span data-stu-id="8d22b-286">Inequality.</span></span> <span data-ttu-id="8d22b-287">如果值不相等，則傳回 `True`。</span><span class="sxs-lookup"><span data-stu-id="8d22b-287">Returns `True` if the values are not equal.</span></span>
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
        <span data-ttu-id="8d22b-288">小於、大於、小於或等於，且大於或等於。</span><span class="sxs-lookup"><span data-stu-id="8d22b-288">Less than, greater than, less than or equal, and greater than or equal.</span></span>
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
        <span data-ttu-id="8d22b-289">串連，用來聯結字串。</span><span class="sxs-lookup"><span data-stu-id="8d22b-289">Concatenation, which is used to join strings.</span></span>
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
        <span data-ttu-id="8d22b-290">遞增和遞減運算子，會從變數相加和減去1（分別為）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-290">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
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
        <span data-ttu-id="8d22b-291">網點.</span><span class="sxs-lookup"><span data-stu-id="8d22b-291">Dot.</span></span> <span data-ttu-id="8d22b-292">用來區別物件及其屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-292">Used to distinguish objects and their properties and methods.</span></span>
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
        <span data-ttu-id="8d22b-293">後.</span><span class="sxs-lookup"><span data-stu-id="8d22b-293">Parentheses.</span></span> <span data-ttu-id="8d22b-294">用來將運算式分組、將參數傳遞給方法，以及存取陣列和集合的成員。</span><span class="sxs-lookup"><span data-stu-id="8d22b-294">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
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
        <span data-ttu-id="8d22b-295">並非.</span><span class="sxs-lookup"><span data-stu-id="8d22b-295">Not.</span></span> <span data-ttu-id="8d22b-296">將 true 值反轉為 false，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="8d22b-296">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="8d22b-297">通常用來做為測試 `False` 的簡短方式（也就是不 `True`）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-297">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
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
        <span data-ttu-id="8d22b-298">邏輯 AND 和 OR，用來將條件連結在一起。</span><span class="sxs-lookup"><span data-stu-id="8d22b-298">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="8d22b-299">在程式碼中使用檔案和資料夾路徑</span><span class="sxs-lookup"><span data-stu-id="8d22b-299">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="8d22b-300">您通常會使用程式碼中的檔案和資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-300">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="8d22b-301">以下是網站的實體資料夾結構範例，因為它可能會出現在您的開發電腦上：</span><span class="sxs-lookup"><span data-stu-id="8d22b-301">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="8d22b-302">以下是一些有關 Url 和路徑的基本詳細資料：</span><span class="sxs-lookup"><span data-stu-id="8d22b-302">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="8d22b-303">URL 的開頭是功能變數名稱（`http://www.example.com`）或伺服器名稱（`http://localhost`，`http://mycomputer`）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-303">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="8d22b-304">URL 會對應至主機電腦上的實體路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-304">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="8d22b-305">例如，`http://myserver` 可能對應到伺服器上的*C:\websites\mywebsite*資料夾。</span><span class="sxs-lookup"><span data-stu-id="8d22b-305">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="8d22b-306">虛擬路徑是用來在程式碼中表示路徑的速記，而不需要指定完整路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-306">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="8d22b-307">它包含在網域或伺服器名稱後面的 URL 部分。</span><span class="sxs-lookup"><span data-stu-id="8d22b-307">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="8d22b-308">當您使用虛擬路徑時，您可以將程式碼移至不同的網域或伺服器，而不需要更新路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-308">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="8d22b-309">以下是可協助您瞭解差異的範例：</span><span class="sxs-lookup"><span data-stu-id="8d22b-309">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="8d22b-310">完成 URL</span><span class="sxs-lookup"><span data-stu-id="8d22b-310">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="8d22b-311">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="8d22b-311">Server name</span></span> | <span data-ttu-id="8d22b-312">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="8d22b-312">*mycompanyserver*</span></span> |
| <span data-ttu-id="8d22b-313">虛擬路徑</span><span class="sxs-lookup"><span data-stu-id="8d22b-313">Virtual path</span></span> | <span data-ttu-id="8d22b-314">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="8d22b-314">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="8d22b-315">實體路徑</span><span class="sxs-lookup"><span data-stu-id="8d22b-315">Physical path</span></span> | <span data-ttu-id="8d22b-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="8d22b-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="8d22b-317">虛擬根目錄是/，就像 C：磁片磁碟機的根目錄一樣。</span><span class="sxs-lookup"><span data-stu-id="8d22b-317">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="8d22b-318">（虛擬資料夾路徑一律使用正斜線）。資料夾的虛擬路徑不一定要有與實體資料夾相同的名稱;它可以是別名。</span><span class="sxs-lookup"><span data-stu-id="8d22b-318">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="8d22b-319">（在實際執行伺服器上，虛擬路徑很少會符合確切的實體路徑）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-319">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="8d22b-320">當您在程式碼中使用檔案和資料夾時，有時候您必須參考實體路徑，有時也需要參照虛擬路徑，視您使用的物件而定。</span><span class="sxs-lookup"><span data-stu-id="8d22b-320">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="8d22b-321">ASP.NET 提供這些工具，讓您在程式碼中使用檔案和資料夾路徑： `Server.MapPath` 方法，以及 `~` 運算子和 `Href` 方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-321">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="8d22b-322">將虛擬轉換成實體路徑：伺服器. MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="8d22b-322">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="8d22b-323">`Server.MapPath` 方法會將虛擬路徑（例如 */default.cshtml*）轉換為絕對實體路徑（例如*C:\WebSites\MyWebSiteFolder\default.cshtml*）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-323">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="8d22b-324">每當您需要完整的實體路徑時，都可以使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-324">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="8d22b-325">典型的範例是當您在 web 伺服器上讀取或寫入文字檔或影像檔案時。</span><span class="sxs-lookup"><span data-stu-id="8d22b-325">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="8d22b-326">您通常不知道網站在主控網站伺服器上的絕對實體路徑，因此這個方法可以將您知道的路徑（虛擬路徑）轉換成伺服器上的對應路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-326">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="8d22b-327">您會將檔案或資料夾的虛擬路徑傳遞至方法，並傳回實體路徑：</span><span class="sxs-lookup"><span data-stu-id="8d22b-327">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="8d22b-328">參考虛擬根目錄： ~ 運算子和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="8d22b-328">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="8d22b-329">在*cshtml*或*vbhtml*檔案中，您可以使用 `~` 運算子來參考虛擬根路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-329">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="8d22b-330">這非常方便，因為您可以在網站中移動頁面，而其包含的任何連結也不會中斷。</span><span class="sxs-lookup"><span data-stu-id="8d22b-330">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="8d22b-331">如果您將網站移至不同的位置，這也很方便。</span><span class="sxs-lookup"><span data-stu-id="8d22b-331">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="8d22b-332">以下是一些範例：</span><span class="sxs-lookup"><span data-stu-id="8d22b-332">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="8d22b-333">如果網站 `http://myserver/myapp`，以下是當頁面執行時，ASP.NET 會如何處理這些路徑：</span><span class="sxs-lookup"><span data-stu-id="8d22b-333">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="8d22b-334">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="8d22b-334">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="8d22b-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="8d22b-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="8d22b-336">（您實際上不會看到這些路徑做為變數的值，但是 ASP.NET 會將這些路徑視為其本身）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-336">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="8d22b-337">您可以在伺服器程式碼（如上）和標記中使用 `~` 運算子，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8d22b-337">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="8d22b-338">在標記中，您可以使用 `~` 運算子來建立資源的路徑，例如影像檔、其他網頁和 CSS 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d22b-338">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="8d22b-339">當頁面執行時，ASP.NET 會查看頁面（程式碼和標記），並將所有 `~` 參考解析為適當的路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-339">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="8d22b-340">條件式邏輯和迴圈</span><span class="sxs-lookup"><span data-stu-id="8d22b-340">Conditional Logic and Loops</span></span>

<span data-ttu-id="8d22b-341">ASP.NET 伺服器程式碼可讓您根據條件執行工作，並撰寫程式碼，以重複語句的特定次數，也就是執行迴圈的程式碼）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-341">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="8d22b-342">測試條件</span><span class="sxs-lookup"><span data-stu-id="8d22b-342">Testing conditions</span></span>

<span data-ttu-id="8d22b-343">若要測試簡單的條件，請使用 `If...Then` 語句，這會根據您指定的測試傳回 `True` 或 `False`：</span><span class="sxs-lookup"><span data-stu-id="8d22b-343">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="8d22b-344">`If` 關鍵字會啟動區塊。</span><span class="sxs-lookup"><span data-stu-id="8d22b-344">The `If` keyword starts a block.</span></span> <span data-ttu-id="8d22b-345">實際的測試（條件）會遵循 `If` 關鍵字，並傳回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="8d22b-345">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="8d22b-346">`If` 語句的結尾為 `Then`。</span><span class="sxs-lookup"><span data-stu-id="8d22b-346">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="8d22b-347">如果測試為 true，將會執行的語句會以 `If` 和 `End If`括住。</span><span class="sxs-lookup"><span data-stu-id="8d22b-347">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="8d22b-348">`If` 語句可以包含 `Else` 區塊，指定當條件為 false 時要執行的語句：</span><span class="sxs-lookup"><span data-stu-id="8d22b-348">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="8d22b-349">如果 `If` 語句啟動程式碼區塊，您就不需要使用一般的 `Code...End Code` 語句來包含區塊。</span><span class="sxs-lookup"><span data-stu-id="8d22b-349">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="8d22b-350">您可以只將 `@` 新增至區塊，它就能正常執行。</span><span class="sxs-lookup"><span data-stu-id="8d22b-350">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="8d22b-351">這個方法適用于 `If`，以及後面接著程式碼區塊的其他 Visual Basic 程式設計關鍵字，包括 `For`、`For Each`、`Do While`等等。</span><span class="sxs-lookup"><span data-stu-id="8d22b-351">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="8d22b-352">您可以使用一或多個 `ElseIf` 區塊來新增多個條件：</span><span class="sxs-lookup"><span data-stu-id="8d22b-352">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="8d22b-353">在此範例中，如果 `If` 區塊中的第一個條件不是 true，則會檢查 `ElseIf` 條件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-353">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="8d22b-354">如果符合該條件，就會執行 `ElseIf` 區塊中的語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-354">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="8d22b-355">如果沒有符合任何條件，則會執行 `Else` 區塊中的語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-355">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="8d22b-356">您可以新增任意數目的 `ElseIf` 區塊，然後關閉 `Else` 區塊，做為 &quot;所有其他專案&quot; 條件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-356">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="8d22b-357">若要測試大量的條件，請使用 `Select Case` 組塊：</span><span class="sxs-lookup"><span data-stu-id="8d22b-357">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="8d22b-358">要測試的值是以括弧括住（在範例中為 weekday 變數）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-358">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="8d22b-359">每個個別測試都會使用列出值的 `Case` 語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-359">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="8d22b-360">如果 `Case` 語句的值符合測試值，則會執行該 `Case` 區塊中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d22b-360">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="8d22b-361">在瀏覽器中顯示的最後兩個條件式區塊的結果：</span><span class="sxs-lookup"><span data-stu-id="8d22b-361">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="8d22b-363">迴圈程式碼</span><span class="sxs-lookup"><span data-stu-id="8d22b-363">Looping code</span></span>

<span data-ttu-id="8d22b-364">您通常需要重複執行相同的語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-364">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="8d22b-365">您可以藉由迴圈來完成這項操作。</span><span class="sxs-lookup"><span data-stu-id="8d22b-365">You do this by looping.</span></span> <span data-ttu-id="8d22b-366">例如，您通常會針對資料集合中的每個專案執行相同的語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-366">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="8d22b-367">如果您確切知道您想要迴圈的次數，可以使用 `For` 迴圈。</span><span class="sxs-lookup"><span data-stu-id="8d22b-367">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="8d22b-368">這種迴圈特別適合用來計算或計數：</span><span class="sxs-lookup"><span data-stu-id="8d22b-368">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="8d22b-369">迴圈會以 `For` 關鍵字開頭，後面接著三個元素：</span><span class="sxs-lookup"><span data-stu-id="8d22b-369">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="8d22b-370">緊接在 `For` 語句之後，您可以宣告計數器變數（您不需要使用 `Dim`），然後指定範圍，如 `i = 10 to 20`中所示。</span><span class="sxs-lookup"><span data-stu-id="8d22b-370">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="8d22b-371">這表示變數 `i` 會開始計數為10，並繼續直到達到20（含）為止。</span><span class="sxs-lookup"><span data-stu-id="8d22b-371">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="8d22b-372">在 `For` 和 `Next` 語句之間是區塊的內容。</span><span class="sxs-lookup"><span data-stu-id="8d22b-372">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="8d22b-373">這可以包含一或多個以每個迴圈執行的程式碼語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-373">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="8d22b-374">`Next i` 語句會結束迴圈。</span><span class="sxs-lookup"><span data-stu-id="8d22b-374">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="8d22b-375">它會遞增計數器並啟動迴圈的下一個反復專案。</span><span class="sxs-lookup"><span data-stu-id="8d22b-375">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="8d22b-376">`For` 和 `Next` 行之間的程式程式碼包含針對迴圈的每個反復專案執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d22b-376">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="8d22b-377">標記會每次建立新的段落（`<p>` 元素），並在輸出中加入一行，顯示 i （計數器）的值。</span><span class="sxs-lookup"><span data-stu-id="8d22b-377">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="8d22b-378">當您執行此頁面時，此範例會建立顯示輸出的11行，而每一行中的文字會指出專案編號。</span><span class="sxs-lookup"><span data-stu-id="8d22b-378">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="8d22b-380">如果您使用的是集合或陣列，通常會使用 `For Each` 迴圈。</span><span class="sxs-lookup"><span data-stu-id="8d22b-380">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="8d22b-381">集合是一組類似的物件，而 `For Each` 迴圈可讓您在集合中的每個專案上執行工作。</span><span class="sxs-lookup"><span data-stu-id="8d22b-381">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="8d22b-382">這種類型的迴圈對集合很方便，因為與 `For` 迴圈不同的是，您不需要遞增計數器或設定限制。</span><span class="sxs-lookup"><span data-stu-id="8d22b-382">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="8d22b-383">相反地，`For Each` 迴圈程式碼只會繼續完成集合，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="8d22b-383">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="8d22b-384">這個範例會傳回 `Request.ServerVariables` 集合中的專案（其中包含您的 web 伺服器的相關資訊）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-384">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="8d22b-385">它會使用 `For Each` 迴圈來顯示每個專案的名稱，方法是在 HTML 項目符號清單中建立新的 `<li>` 元素。</span><span class="sxs-lookup"><span data-stu-id="8d22b-385">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="8d22b-386">`For Each` 關鍵字後面接著一個變數，代表集合中的單一專案（在範例中，`myItem`），後面接著 `In` 關鍵字，後面接著您要迴圈執行的集合。</span><span class="sxs-lookup"><span data-stu-id="8d22b-386">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="8d22b-387">在 `For Each` 迴圈的主體中，您可以使用先前宣告的變數來存取目前的專案。</span><span class="sxs-lookup"><span data-stu-id="8d22b-387">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="8d22b-389">若要建立更一般用途的迴圈，請使用 `Do While` 語句：</span><span class="sxs-lookup"><span data-stu-id="8d22b-389">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="8d22b-390">這個迴圈會以 `Do While` 關鍵字開頭，後面接著條件，然後是要重複的區塊。</span><span class="sxs-lookup"><span data-stu-id="8d22b-390">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="8d22b-391">迴圈通常會遞增（加入）或遞減（減去）用來計算的變數或物件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-391">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="8d22b-392">在此範例中，每次執行迴圈時，`+=` 運算子都會在變數的值加1。</span><span class="sxs-lookup"><span data-stu-id="8d22b-392">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="8d22b-393">（若要遞減迴圈中計數的變數，您可以使用遞減運算子 `-=`）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-393">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="8d22b-394">物件和集合</span><span class="sxs-lookup"><span data-stu-id="8d22b-394">Objects and Collections</span></span>

<span data-ttu-id="8d22b-395">ASP.NET 網站中幾乎所有內容都是物件，包括網頁本身。</span><span class="sxs-lookup"><span data-stu-id="8d22b-395">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="8d22b-396">本節討論您在程式碼中經常使用的一些重要物件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-396">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="8d22b-397">頁面物件</span><span class="sxs-lookup"><span data-stu-id="8d22b-397">Page objects</span></span>

<span data-ttu-id="8d22b-398">ASP.NET 中最基本的物件是頁面。</span><span class="sxs-lookup"><span data-stu-id="8d22b-398">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="8d22b-399">您可以直接存取頁面物件的屬性，而不需要任何限定的物件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-399">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="8d22b-400">下列程式碼會使用頁面的 `Request` 物件，取得頁面的檔案路徑：</span><span class="sxs-lookup"><span data-stu-id="8d22b-400">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="8d22b-401">您可以使用 `Page` 物件的屬性來取得大量資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="8d22b-401">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="8d22b-402">`Request`</span><span class="sxs-lookup"><span data-stu-id="8d22b-402">`Request`.</span></span> <span data-ttu-id="8d22b-403">如您所見，這是目前要求的相關資訊集合，包括提出要求的瀏覽器類型、頁面的 URL、使用者身分識別等。</span><span class="sxs-lookup"><span data-stu-id="8d22b-403">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="8d22b-404">`Response`</span><span class="sxs-lookup"><span data-stu-id="8d22b-404">`Response`.</span></span> <span data-ttu-id="8d22b-405">這是在伺服器程式碼完成執行時，將會傳送至瀏覽器的回應（頁面）相關資訊集合。</span><span class="sxs-lookup"><span data-stu-id="8d22b-405">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="8d22b-406">例如，您可以使用這個屬性將資訊寫入至回應。</span><span class="sxs-lookup"><span data-stu-id="8d22b-406">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="8d22b-407">集合物件（陣列和字典）</span><span class="sxs-lookup"><span data-stu-id="8d22b-407">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="8d22b-408">集合是一組相同類型的物件，例如從資料庫 `Customer` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="8d22b-408">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="8d22b-409">ASP.NET 包含許多內建集合，例如 `Request.Files` 集合。</span><span class="sxs-lookup"><span data-stu-id="8d22b-409">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="8d22b-410">您通常會使用集合中的資料。</span><span class="sxs-lookup"><span data-stu-id="8d22b-410">You'll often work with data in collections.</span></span> <span data-ttu-id="8d22b-411">有兩個常見的集合類型是*陣列*和*字典*。</span><span class="sxs-lookup"><span data-stu-id="8d22b-411">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="8d22b-412">當您想要儲存類似專案的集合，但不想要建立個別的變數來保存每個專案時，陣列會很有用：</span><span class="sxs-lookup"><span data-stu-id="8d22b-412">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="8d22b-413">使用陣列，您可以宣告特定的資料類型，例如 `String`、`Integer`或 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="8d22b-413">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="8d22b-414">若要指出變數可以包含陣列，您可以在宣告的變數名稱中加上括弧（例如 `Dim myVar() As String`）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-414">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="8d22b-415">您可以使用物件的位置（索引），或使用 `For Each` 語句來存取陣列中的專案。</span><span class="sxs-lookup"><span data-stu-id="8d22b-415">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="8d22b-416">陣列索引以零&#8212;為起始，亦即，第一個專案位於位置0，第二個專案位於位置1，依此類推。</span><span class="sxs-lookup"><span data-stu-id="8d22b-416">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="8d22b-417">您可以藉由取得 `Length` 屬性來判斷陣列中的專案數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-417">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="8d22b-418">若要取得陣列中特定專案的位置（也就是搜尋陣列），請使用 `Array.IndexOf` 方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-418">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="8d22b-419">您也可以執行一些動作，像是反轉陣列的內容（`Array.Reverse` 方法）或排序內容（`Array.Sort` 方法）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-419">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="8d22b-420">在瀏覽器中顯示的字串陣列程式碼輸出：</span><span class="sxs-lookup"><span data-stu-id="8d22b-420">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="8d22b-422">字典是索引鍵/值組的集合，您可以在其中提供用來設定或抓取對應值的索引鍵（或名稱）：</span><span class="sxs-lookup"><span data-stu-id="8d22b-422">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="8d22b-423">若要建立字典，您可以使用 `New` 關鍵字來表示您要建立新的 `Dictionary` 物件。</span><span class="sxs-lookup"><span data-stu-id="8d22b-423">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="8d22b-424">您可以使用 `Dim` 關鍵字，將字典指派給變數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-424">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="8d22b-425">您可以使用括弧（`( )`）來指示字典中專案的資料類型。</span><span class="sxs-lookup"><span data-stu-id="8d22b-425">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="8d22b-426">在宣告的結尾，您必須加入另一對括弧，因為這實際上是建立新字典的方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-426">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="8d22b-427">若要將專案加入至字典，您可以呼叫 dictionary 變數的 `Add` 方法（在此案例中為`myScores`），然後指定索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="8d22b-427">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="8d22b-428">或者，您可以使用括弧來表示金鑰，並執行簡單的指派，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8d22b-428">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="8d22b-429">若要從字典取得值，請在括弧中指定索引鍵：</span><span class="sxs-lookup"><span data-stu-id="8d22b-429">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="8d22b-430">使用參數呼叫方法</span><span class="sxs-lookup"><span data-stu-id="8d22b-430">Calling Methods with Parameters</span></span>

<span data-ttu-id="8d22b-431">如您稍早在本文中所見，使用進行程式設計的物件有方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-431">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="8d22b-432">例如，`Database` 物件可能會有 `Database.Connect` 的方法。</span><span class="sxs-lookup"><span data-stu-id="8d22b-432">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="8d22b-433">許多方法也有一或多個參數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-433">Many methods also have one or more parameters.</span></span> <span data-ttu-id="8d22b-434">*參數*是您傳遞給方法的值，可讓方法完成其工作。</span><span class="sxs-lookup"><span data-stu-id="8d22b-434">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="8d22b-435">例如，查看 `Request.MapPath` 方法的宣告，其採用三個參數：</span><span class="sxs-lookup"><span data-stu-id="8d22b-435">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="8d22b-436">這個方法會傳回伺服器上對應至指定虛擬路徑的實體路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-436">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="8d22b-437">方法的三個參數是 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="8d22b-437">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="8d22b-438">（請注意，在宣告中，參數會列出其接受的資料類型）。當您呼叫這個方法時，您必須提供所有三個參數的值。</span><span class="sxs-lookup"><span data-stu-id="8d22b-438">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="8d22b-439">當您使用 Razor 語法的 Visual Basic 時，您有兩個選項可將參數傳遞給方法：*位置參數*或*具名引數*。</span><span class="sxs-lookup"><span data-stu-id="8d22b-439">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="8d22b-440">若要使用位置參數呼叫方法，請以方法宣告中指定的嚴格順序來傳遞參數。</span><span class="sxs-lookup"><span data-stu-id="8d22b-440">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="8d22b-441">（您通常會藉由閱讀方法的檔來得知此順序）。您必須遵循順序，而且不能在必要時略過任何&#8212;參數，您可以傳遞空字串（`""`），或為沒有值的位置參數傳遞 null。</span><span class="sxs-lookup"><span data-stu-id="8d22b-441">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="8d22b-442">下列範例假設您的網站上有一個名為 [*腳本*] 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8d22b-442">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="8d22b-443">程式碼會呼叫 `Request.MapPath` 方法，並以正確的順序傳遞三個參數的值。</span><span class="sxs-lookup"><span data-stu-id="8d22b-443">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="8d22b-444">然後，它會顯示所產生的對應路徑。</span><span class="sxs-lookup"><span data-stu-id="8d22b-444">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="8d22b-445">當方法有許多參數時，您可以使用具名引數，讓您的程式碼更簡潔且更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="8d22b-445">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="8d22b-446">若要使用具名引數來呼叫方法，請指定參數名稱，後面接著 `:=`，然後提供值。</span><span class="sxs-lookup"><span data-stu-id="8d22b-446">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="8d22b-447">具名引數的優點是您可以依照任何想要的順序來新增它們。</span><span class="sxs-lookup"><span data-stu-id="8d22b-447">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="8d22b-448">（缺點是方法呼叫不是精簡的）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-448">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="8d22b-449">下列範例會呼叫與上述相同的方法，但會使用具名引數來提供值：</span><span class="sxs-lookup"><span data-stu-id="8d22b-449">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="8d22b-450">如您所見，參數會以不同的順序傳遞。</span><span class="sxs-lookup"><span data-stu-id="8d22b-450">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="8d22b-451">不過，如果您執行上述範例和此範例，則會傳回相同的值。</span><span class="sxs-lookup"><span data-stu-id="8d22b-451">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="8d22b-452">處理錯誤</span><span class="sxs-lookup"><span data-stu-id="8d22b-452">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="8d22b-453">Try-catch 語句</span><span class="sxs-lookup"><span data-stu-id="8d22b-453">Try-Catch statements</span></span>

<span data-ttu-id="8d22b-454">您的程式碼中通常會有語句，可能會因為控制項以外的原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="8d22b-454">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="8d22b-455">例如:</span><span class="sxs-lookup"><span data-stu-id="8d22b-455">For example:</span></span>

- <span data-ttu-id="8d22b-456">如果您的程式碼嘗試開啟、建立、讀取或寫入檔案，可能會發生各種錯誤。</span><span class="sxs-lookup"><span data-stu-id="8d22b-456">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="8d22b-457">您想要的檔案可能不存在、可能被鎖定、程式碼可能沒有許可權等等。</span><span class="sxs-lookup"><span data-stu-id="8d22b-457">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="8d22b-458">同樣地，如果您的程式碼嘗試更新資料庫中的記錄，可能會有許可權問題，可能會卸載與資料庫的連接、要儲存的資料可能無效等等。</span><span class="sxs-lookup"><span data-stu-id="8d22b-458">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="8d22b-459">在程式設計的詞彙中，這些情況稱為*例外*狀況。</span><span class="sxs-lookup"><span data-stu-id="8d22b-459">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="8d22b-460">如果您的程式碼遇到例外狀況，它會產生（擲回）一則錯誤訊息，也就是使用者的討厭程度最高。</span><span class="sxs-lookup"><span data-stu-id="8d22b-460">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="8d22b-462">在您的程式碼可能會遇到例外狀況的情況下，為了避免這種類型的錯誤訊息，您可以使用 `Try/Catch` 語句。</span><span class="sxs-lookup"><span data-stu-id="8d22b-462">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="8d22b-463">在 `Try` 語句中，您會執行您要檢查的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d22b-463">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="8d22b-464">在一或多個 `Catch` 語句中，您可以尋找可能發生的特定錯誤（特定類型的例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-464">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="8d22b-465">您可以視需要包含多個 `Catch` 語句，以尋找您預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="8d22b-465">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="8d22b-466">我們建議您避免在 `Try/Catch` 語句中使用 `Response.Redirect` 方法，因為它可能會在您的頁面中造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8d22b-466">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="8d22b-467">下列範例顯示的頁面會在第一個要求上建立文字檔，然後顯示一個按鈕，讓使用者開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="8d22b-467">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="8d22b-468">此範例刻意使用錯誤的檔案名，因此會造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8d22b-468">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="8d22b-469">此程式碼包含兩個可能例外狀況的 `Catch` 語句： `FileNotFoundException`，如果檔案名不正確，就會發生這種情況，如果 ASP.NET 找不到資料夾，就會發生 `DirectoryNotFoundException`。</span><span class="sxs-lookup"><span data-stu-id="8d22b-469">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="8d22b-470">（您可以將範例中的語句取消批註，以便在所有專案正常運作時查看其執行方式）。</span><span class="sxs-lookup"><span data-stu-id="8d22b-470">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="8d22b-471">如果您的程式碼未處理例外狀況，您會看到如先前螢幕擷取畫面所示的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="8d22b-471">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="8d22b-472">不過，`Try/Catch` 區段有助於防止使用者看到這些類型的錯誤。</span><span class="sxs-lookup"><span data-stu-id="8d22b-472">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="8d22b-473">其他資源</span><span class="sxs-lookup"><span data-stu-id="8d22b-473">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="8d22b-474">參考文件</span><span class="sxs-lookup"><span data-stu-id="8d22b-474">Reference Documentation</span></span>

- [<span data-ttu-id="8d22b-475">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8d22b-475">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="8d22b-476">Visual Basic 語言</span><span class="sxs-lookup"><span data-stu-id="8d22b-476">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
