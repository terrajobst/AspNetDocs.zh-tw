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
# <a name="introducing-aspnet-web-pages---programming-basics"></a><span data-ttu-id="7f4d1-104">ASP.NET Web Pages 程式設計基本概念簡介</span><span class="sxs-lookup"><span data-stu-id="7f4d1-104">Introducing ASP.NET Web Pages - Programming Basics</span></span>

<span data-ttu-id="7f4d1-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7f4d1-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7f4d1-106">本教學課程可讓您瞭解如何使用 Razor 語法在 ASP.NET Web Pages 中進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-106">This tutorial gives you an overview of how to program in ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="7f4d1-107">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="7f4d1-108">您在 ASP.NET Web Pages 中用來進行程式設計的基本 "Razor" 語法。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-108">The basic "Razor" syntax that you use for programming in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="7f4d1-109">一些基本C#，這是您將使用的程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-109">Some basic C#, which is the programming language you'll use.</span></span>
> - <span data-ttu-id="7f4d1-110">Web Pages 的一些基本程式設計概念。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-110">Some fundamental programming concepts for Web Pages.</span></span>
> - <span data-ttu-id="7f4d1-111">如何安裝套件（包含預建程式碼的元件）以搭配您的網站使用。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-111">How to install packages (components that contain prebuilt code) to use with your site.</span></span>
> - <span data-ttu-id="7f4d1-112">如何使用 helper 來執行*一般的程式*設計工作。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-112">How to use *helpers* to perform common programming tasks.</span></span>
>   
> 
> <span data-ttu-id="7f4d1-113">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="7f4d1-114">NuGet 和套件管理員。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-114">NuGet and the package manager.</span></span>
> - <span data-ttu-id="7f4d1-115">`Gravatar` helper。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-115">The `Gravatar` helper.</span></span>

<span data-ttu-id="7f4d1-116">本教學課程主要是介紹您將用於 ASP.NET Web Pages 的程式設計語法。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-116">This tutorial is primarily an exercise in introducing you to the programming syntax that you'll use for ASP.NET Web Pages.</span></span> <span data-ttu-id="7f4d1-117">您將瞭解以程式C#設計語言撰寫的 Razor 語法和程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-117">You'll learn about *Razor syntax* and code that's written in the C# programming language.</span></span> <span data-ttu-id="7f4d1-118">在上一個教學課程中，您已經大致瞭解此語法;在本教學課程中，我們將詳細說明語法。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-118">You got a glimpse of this syntax in the previous tutorial; in this tutorial we'll explain the syntax more.</span></span>

<span data-ttu-id="7f4d1-119">我們保證本教學課程牽涉到您會在單一教學課程中看到的大部分程式設計，而這是唯一*僅*適用于程式設計的教學課程。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-119">We promise that this tutorial involves the most programming that you'll see in a single tutorial, and that it's the only tutorial that is *only* about programming.</span></span> <span data-ttu-id="7f4d1-120">在此集合的其餘教學課程中，您將會建立可執行有趣事項的頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-120">In the remaining tutorials in this set, you'll actually create pages that do interesting things.</span></span>

<span data-ttu-id="7f4d1-121">您也*會瞭解協助程式。*</span><span class="sxs-lookup"><span data-stu-id="7f4d1-121">You'll also learn about *helpers*.</span></span> <span data-ttu-id="7f4d1-122">協助程式是一種元件，也就是封裝的程式碼，您可以將它加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-122">A helper is a component — a packaged-up piece of code — that you can add to a page.</span></span> <span data-ttu-id="7f4d1-123">Helper 會為您執行工作，否則可能會單調乏味或複雜。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-123">The helper performs work for you that otherwise might be tedious or complex to do by hand.</span></span>

## <a name="creating-a-page-to-play-with-razor"></a><span data-ttu-id="7f4d1-124">建立要使用 Razor 播放的頁面</span><span class="sxs-lookup"><span data-stu-id="7f4d1-124">Creating a Page to Play with Razor</span></span>

<span data-ttu-id="7f4d1-125">在本節中，您將使用 Razor 來玩，讓您可以瞭解基本語法。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-125">In this section you'll play a bit with Razor so you can get a sense of the basic syntax.</span></span>

<span data-ttu-id="7f4d1-126">如果尚未執行，請啟動 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-126">Start WebMatrix if it's not already running.</span></span> <span data-ttu-id="7f4d1-127">您將會使用您在上一個教學課程中建立的網站（[消費者入門網頁](https://go.microsoft.com/fwlink/?LinkId=251578)）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-127">You'll use the website you created in the previous tutorial ([Getting Started With Web Pages](https://go.microsoft.com/fwlink/?LinkId=251578)).</span></span> <span data-ttu-id="7f4d1-128">若要重新開啟，請按一下 [**我的網站**]，然後選擇 [ **WebPageMovies**]：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-128">To reopen it, click **My Sites** and choose **WebPageMovies**:</span></span>

![WebMatrix 開始畫面，顯示 [開啟網站] 選項和 [我的網站] 反白顯示](intro-to-web-pages-programming/_static/image1.png)

<span data-ttu-id="7f4d1-130">選取 [**檔案**] 工作區。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-130">Select the **Files** workspace.</span></span>

<span data-ttu-id="7f4d1-131">在功能區中，按一下 [**新增**] 以建立頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-131">In the ribbon, click **New** to create a page.</span></span> <span data-ttu-id="7f4d1-132">選取 [ **CSHTML** ]，並將新頁面命名為*TestRazor*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-132">Select **CSHTML** and name the new page *TestRazor.cshtml*.</span></span>

<span data-ttu-id="7f4d1-133">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-133">Click **OK**.</span></span>

<span data-ttu-id="7f4d1-134">將下列內容複寫到檔案中，並完全取代已存在的檔案。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-134">Copy the following into the file, completely replacing what's there already.</span></span>

> [!NOTE]
> <span data-ttu-id="7f4d1-135">當您將範例中的程式碼或標記複製到頁面時，縮排和對齊可能不會與教學課程中的相同。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-135">When you copy code or markup from the examples into a page, the indentation and alignment might not be the same as in the tutorial.</span></span> <span data-ttu-id="7f4d1-136">不過，縮排和對齊不會影響程式碼的執行方式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-136">Indentation and alignment don't affect how the code runs, though.</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a><span data-ttu-id="7f4d1-137">檢查範例頁面</span><span class="sxs-lookup"><span data-stu-id="7f4d1-137">Examining the Example Page</span></span>

<span data-ttu-id="7f4d1-138">您所看到的大部分都是一般 HTML。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-138">Most of what you see is ordinary HTML.</span></span> <span data-ttu-id="7f4d1-139">不過，在頂端會有此程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-139">However, at the top there's this code block:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

<span data-ttu-id="7f4d1-140">請注意下列關於此程式碼區塊的事項：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-140">Notice the following things about this code block:</span></span>

- <span data-ttu-id="7f4d1-141">@ 字元會告訴 ASP.NET，以下是 Razor 程式碼，而不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-141">The @ character tells ASP.NET that what follows is Razor code, not HTML.</span></span> <span data-ttu-id="7f4d1-142">ASP.NET 會將 @ 字元之後的所有內容視為程式碼，直到它再次執行到某些 HTML。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-142">ASP.NET will treat everything after the @ character as code until it runs into some HTML again.</span></span> <span data-ttu-id="7f4d1-143">（在此案例中，這是 &lt;！DOCTYPE&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-143">(In this case, that's the &lt;!DOCTYPE&gt; element.</span></span>
- <span data-ttu-id="7f4d1-144">如果程式碼有多行，則大括弧（{和}）會括住 Razor 程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-144">The braces ( { and } ) enclose a block of Razor code if the code has more than one line.</span></span> <span data-ttu-id="7f4d1-145">大括弧會告訴 ASP.NET，該區塊的程式碼會在此處開始和結束。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-145">The braces tell ASP.NET where the code for that block starts and ends.</span></span>
- <span data-ttu-id="7f4d1-146">字元會標示批註，也就是不會執行的程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-146">The // characters mark a comment — that is, a part of the code that won't execute.</span></span>
- <span data-ttu-id="7f4d1-147">每個語句的結尾都必須是分號（;)。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-147">Each statement has to end with a semicolon (;).</span></span> <span data-ttu-id="7f4d1-148">（不過，這不是批註）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-148">(Not comments, though.)</span></span>
- <span data-ttu-id="7f4d1-149">您可以將值儲存在*變數*中，您會使用關鍵字 var 來*建立（宣告*）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-149">You can store values in *variables*, which you create (*declare*) with the keyword var.</span></span> <span data-ttu-id="7f4d1-150">當您建立變數時，您可以指定名稱，其中可以包含字母、數位和底線（\_）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-150">When you create a variable, you give it a name, which can include letters, numbers, and underscore (\_).</span></span> <span data-ttu-id="7f4d1-151">變數名稱不能以數位開頭，也不能使用程式設計關鍵字的名稱（例如 var）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-151">Variable names can't start with a number and can't use the name of a programming keyword (like var).</span></span>
- <span data-ttu-id="7f4d1-152">您可以用引號括住字元字串（例如 "ASP.NET" 和 "Web Pages"）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-152">You enclose character strings (like "ASP.NET" and "Web Pages") in quotation marks.</span></span> <span data-ttu-id="7f4d1-153">（必須以雙引號括住）。數位不是括在引號中。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-153">(They must be double quotation marks.) Numbers are not in quotation marks.</span></span>
- <span data-ttu-id="7f4d1-154">引號外的空白並不重要。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-154">Whitespace outside of quotation marks doesn't matter.</span></span> <span data-ttu-id="7f4d1-155">分行符號大多不重要;例外狀況是您無法跨行分割引號中的字串。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-155">Line breaks mostly don't matter; the exception is that you can't split a string in quotation marks across lines.</span></span> <span data-ttu-id="7f4d1-156">縮排和對齊並不重要。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-156">Indentation and alignment don't matter.</span></span>

<span data-ttu-id="7f4d1-157">這個範例不明顯的事情是，所有程式碼都區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-157">Something that's not obvious from this example is that all code is case sensitive.</span></span> <span data-ttu-id="7f4d1-158">這表示變數 TheSum 的變數，與可能名為 theSum 或 TheSum 的變數不同。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-158">This means that the variable TheSum is a different variable than variables that might be named theSum or thesum.</span></span> <span data-ttu-id="7f4d1-159">同樣地，var 是關鍵字，但 Var 則不是。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-159">Similarly, var is a keyword, but Var is not.</span></span>

### <a name="objects-and-properties-and-methods"></a><span data-ttu-id="7f4d1-160">物件和屬性和方法</span><span class="sxs-lookup"><span data-stu-id="7f4d1-160">Objects and properties and methods</span></span>

<span data-ttu-id="7f4d1-161">接著是運算式日期時間。現在。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-161">Then there's the expression DateTime.Now.</span></span> <span data-ttu-id="7f4d1-162">簡單來說，DateTime 是一個*物件*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-162">In simple terms, DateTime is an *object*.</span></span> <span data-ttu-id="7f4d1-163">物件是您可以用來進行程式設計的專案，包括頁面、文字方塊、檔案、影像、web 要求、電子郵件訊息、客戶記錄等等。物件具有一或多個描述其特性的*屬性*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-163">An object is a thing that you can program with—a page, a text box, a file, an image, a web request, an email message, a customer record, etc. Objects have one or more *properties* that describe their characteristics.</span></span> <span data-ttu-id="7f4d1-164">一個文字方塊物件有一個 Text 屬性（還有一些），一個 request 物件有一個 Url 屬性（還有其他），一個電子郵件訊息具有 From 屬性和 To 屬性等等。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-164">A text box object has a Text property (among others), a request object has a Url property (and others), an email message has a From property and a To property, and so on.</span></span> <span data-ttu-id="7f4d1-165">物件也有可執行檔「動詞」*方法*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-165">Objects also have *methods* that are the "verbs" they can perform.</span></span> <span data-ttu-id="7f4d1-166">您將會很多使用物件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-166">You'll be working with objects a lot.</span></span>

<span data-ttu-id="7f4d1-167">如您在範例中所見，DateTime 是一個可讓您編寫日期和時間的物件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-167">As you can see from the example, DateTime is an object that lets you program dates and times.</span></span> <span data-ttu-id="7f4d1-168">它有一個名稱為 Now 的屬性，它會傳回目前的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-168">It has a property named Now that returns the current date and time.</span></span>

### <a name="using-code-to-render-markup-in-the-page"></a><span data-ttu-id="7f4d1-169">使用程式碼在頁面中呈現標記</span><span class="sxs-lookup"><span data-stu-id="7f4d1-169">Using code to render markup in the page</span></span>

<span data-ttu-id="7f4d1-170">在頁面主體中，請注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-170">In the body of the page, notice the following:</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

<span data-ttu-id="7f4d1-171">同樣地，@ 字元會告訴 ASP.NET，接下來是程式碼，而不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-171">Again, the @ character tells ASP.NET that what follows is code, not HTML.</span></span> <span data-ttu-id="7f4d1-172">在標記中，您可以新增 @，後面接著程式碼運算式，而 ASP.NET 會在該時間點直接呈現該運算式的值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-172">In the markup you can add @ followed by a code expression, and ASP.NET will render the value of that expression right at that point.</span></span> <span data-ttu-id="7f4d1-173">在此範例中，@a 將會轉譯值為的變數，@product 呈現名為 product 的變數中的任何內容，依此類推。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-173">In the example, @a will render whatever the value is of the variable named a, @product renders whatever is in the variable named product, and so on.</span></span>

<span data-ttu-id="7f4d1-174">不過，您並不限於變數。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-174">You're not limited to variables, though.</span></span> <span data-ttu-id="7f4d1-175">在這裡的幾個實例中，@ 字元會在運算式之前：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-175">In a few instances here, the @ character precedes an expression:</span></span>

- <span data-ttu-id="7f4d1-176">@ （a\*b）會呈現變數 a 和 b 中任何內容的乘積。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-176">@(a\*b) renders the product of whatever is in the variables a and b.</span></span> <span data-ttu-id="7f4d1-177">（\* 運算子表示乘法）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-177">(The \* operator means multiplication.)</span></span>
- <span data-ttu-id="7f4d1-178">@ （技術 + "" + product）會在串連變數技術和產品後呈現這些值，並在其間加上空格。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-178">@(technology + " " + product) renders the values in the variables technology and product after concatenating them and adding a space in between.</span></span> <span data-ttu-id="7f4d1-179">串連字號串的運算子（+）與用於加入數位的運算子相同。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-179">The operator (+) for concatenating strings is the same as the operator for adding numbers.</span></span> <span data-ttu-id="7f4d1-180">ASP.NET 通常會指出您是使用數位或字串，並使用 + 運算子進行正確的作業。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-180">ASP.NET can usually tell whether you're working with numbers or with strings and does the right thing with the + operator.</span></span>
- <span data-ttu-id="7f4d1-181">@Request.Url 呈現 Request 物件的 Url 屬性。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-181">@Request.Url renders the Url property of the Request object.</span></span> <span data-ttu-id="7f4d1-182">Request 物件包含來自瀏覽器的目前要求的相關資訊，而 Url 屬性則包含該目前要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-182">The Request object contains information about the current request from the browser, and of course the Url property contains the URL of that current request.</span></span>

<span data-ttu-id="7f4d1-183">這個範例也是設計來說明您可以用不同的方式來執行工作。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-183">The example is also designed to show you that you can do work in different ways.</span></span> <span data-ttu-id="7f4d1-184">您可以在頂端的程式碼區塊中執行計算，將結果放入變數中，然後在標記中轉譯變數。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-184">You can do calculations in the code block at the top, put the results into a variable, and then render the variable in markup.</span></span> <span data-ttu-id="7f4d1-185">或者，您也可以在標記的運算式中執行計算。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-185">Or you can do calculations in an expression right in the markup.</span></span> <span data-ttu-id="7f4d1-186">您所使用的方法取決於您所執行的動作，以及您自己的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-186">The approach you use depends on what you're doing and, to some extent, on your own preference.</span></span>

### <a name="seeing-the-code-in-action"></a><span data-ttu-id="7f4d1-187">查看動作中的程式碼</span><span class="sxs-lookup"><span data-stu-id="7f4d1-187">Seeing the code in action</span></span>

<span data-ttu-id="7f4d1-188">以滑鼠右鍵按一下檔案名，然後選擇 [**在瀏覽器中啟動**]。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-188">Right-click the name of the file and then choose **Launch in browser**.</span></span> <span data-ttu-id="7f4d1-189">您會在瀏覽器中看到頁面中已解決的所有值和運算式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-189">You see the page in the browser with all the values and expressions resolved in the page.</span></span>

![在瀏覽器中執行的 ' TestRazor ' 頁面](intro-to-web-pages-programming/_static/image2.png)

<span data-ttu-id="7f4d1-191">查看瀏覽器中的來源。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-191">Look at the source in the browser.</span></span>

![瀏覽器中的 [測試 Razor] 頁面來源](intro-to-web-pages-programming/_static/image3.png)

<span data-ttu-id="7f4d1-193">就像您在上一個教學課程中所預期的經驗，此頁面中沒有任何 Razor 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-193">As you expect from your experience in the previous tutorial, none of the Razor code is in the page.</span></span> <span data-ttu-id="7f4d1-194">您看到的只是實際的顯示值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-194">All you see are the actual display values.</span></span> <span data-ttu-id="7f4d1-195">當您執行頁面時，實際上是對內建于 WebMatrix 的網頁伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-195">When you run a page, you're actually making a request to the web server that's built into WebMatrix.</span></span> <span data-ttu-id="7f4d1-196">收到要求時，ASP.NET 會解析所有值和運算式，並將其值轉譯成頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-196">When the request is received, ASP.NET resolves all the values and expressions and renders their values into the page.</span></span> <span data-ttu-id="7f4d1-197">然後，它會將頁面傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-197">It then sends the page to the browser.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="7f4d1-198">**Razor 和C#**</span><span class="sxs-lookup"><span data-stu-id="7f4d1-198">**Razor and C#**</span></span>
> 
> <span data-ttu-id="7f4d1-199">到目前為止，我們已說過您正在使用 Razor 語法。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-199">Up to now we've said that you're working with Razor syntax.</span></span> <span data-ttu-id="7f4d1-200">沒錯，但這並不是完整的故事。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-200">That's true, but it's not the complete story.</span></span> <span data-ttu-id="7f4d1-201">您所使用的實際程式設計語言稱為*C#* 。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-201">The actual programming language you're using is called *C#*.</span></span> <span data-ttu-id="7f4d1-202">C#這是 Microsoft 在十年前所建立的，而且已經成為建立 Windows 應用程式的主要程式設計語言之一。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-202">C# was created by Microsoft over a decade ago and has become one of the primary programming languages for creating Windows apps.</span></span> <span data-ttu-id="7f4d1-203">您已瞭解如何為變數命名的所有規則，以及如何建立語句等等，實際上是C#語言的所有規則。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-203">All the rules you've seen about how to name a variable and how to create statements and so on are actually all rules of the C# language.</span></span>
> 
> <span data-ttu-id="7f4d1-204">Razor 會特別針對您將此程式碼內嵌至頁面的一小部分慣例，更明確地參考。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-204">Razor refers more specifically to the small set of conventions for how you embed this code into a page.</span></span> <span data-ttu-id="7f4d1-205">例如，使用 @ 標記頁面中的程式碼，以及使用 @ {} 來內嵌程式碼區塊的慣例，是頁面的 Razor 層面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-205">For example, the convention of using @ to mark code in the page and using @{ } to embed a code block is the Razor aspect of a page.</span></span> <span data-ttu-id="7f4d1-206">協助程式也會被視為 Razor 的一部分。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-206">Helpers are also considered to be part of Razor.</span></span> <span data-ttu-id="7f4d1-207">Razor 語法在多個位置使用，而不只是 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-207">Razor syntax is used in more places than just in ASP.NET Web Pages.</span></span> <span data-ttu-id="7f4d1-208">（例如，它也用於 ASP.NET MVC views）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-208">(For example, it's used in ASP.NET MVC views as well.)</span></span>
> 
> <span data-ttu-id="7f4d1-209">我們提過這是因為如果您尋找程式設計 ASP.NET Web Pages 的相關資訊，就會發現 Razor 的許多參考。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-209">We mention this because if you look for information about programming ASP.NET Web Pages, you'll find lots of references to Razor.</span></span> <span data-ttu-id="7f4d1-210">不過，其中有許多參考並不適用于您所做的事，因此可能會造成混淆。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-210">However, a lot of those references don't apply to what you're doing and might therefore be confusing.</span></span> <span data-ttu-id="7f4d1-211">事實上，許多程式設計問題都是關於使用C#或使用 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-211">And in fact, many of your programming questions are really going to be about either working with C# or working with ASP.NET.</span></span> <span data-ttu-id="7f4d1-212">因此，如果您特別瞭解 Razor 的相關資訊，可能就找不到所需的解答。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-212">So if you look specifically for information about Razor, you might not find the answers you need.</span></span>

## <a name="adding-some-conditional-logic"></a><span data-ttu-id="7f4d1-213">新增一些條件式邏輯</span><span class="sxs-lookup"><span data-stu-id="7f4d1-213">Adding Some Conditional Logic</span></span>

<span data-ttu-id="7f4d1-214">在頁面中使用程式碼的其中一個絕佳功能，就是您可以根據各種條件來變更會發生的情況。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-214">One of the great features about using code in a page is that you can change what happens based on various conditions.</span></span> <span data-ttu-id="7f4d1-215">在本教學課程的這個部分中，您將使用一些方式來變更頁面中顯示的內容。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-215">In this part of the tutorial, you'll play around with some ways to change what's displayed in the page.</span></span>

<span data-ttu-id="7f4d1-216">這個範例很簡單，而且有點假設，讓我們可以專注于條件式邏輯。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-216">The example will be simple and somewhat contrived so that we can concentrate on the conditional logic.</span></span> <span data-ttu-id="7f4d1-217">您將建立的頁面將會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-217">The page you'll create will do this:</span></span>

- <span data-ttu-id="7f4d1-218">根據網頁是否為第一次顯示頁面，或您是否已按下按鈕來提交頁面，在頁面上顯示不同的文字。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-218">Show different text on the page depending on whether it's the first time the page is displayed or whether you've clicked a button to submit the page.</span></span> <span data-ttu-id="7f4d1-219">這會是第一個條件式測試。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-219">That will be the first conditional test.</span></span>
- <span data-ttu-id="7f4d1-220">只有在 URL 的查詢字串中傳遞特定值（HTTP：//...？ show = true）時，才顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-220">Display the message only if a certain value is passed in the query string of the URL (http://...?show=true).</span></span> <span data-ttu-id="7f4d1-221">這會是第二個條件式測試。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-221">That will be the second conditional test.</span></span>

<span data-ttu-id="7f4d1-222">在 WebMatrix 中建立頁面，並將它命名為*TestRazorPart2*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-222">In WebMatrix, create a page and name it *TestRazorPart2.cshtml*.</span></span> <span data-ttu-id="7f4d1-223">（在功能區中，按一下 [**新增**]，選擇 [ **CSHTML**]，為檔案命名，然後按一下 **[確定]** ）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-223">(In the ribbon, click **New**, choose **CSHTML**, name the file, and then click **OK**.)</span></span>

<span data-ttu-id="7f4d1-224">將該頁面的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-224">Replace the contents of that page with the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

<span data-ttu-id="7f4d1-225">頂端的程式碼區塊會使用一些文字，將名為 message 的變數初始化。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-225">The code block at the top initializes a variable named message with some text.</span></span> <span data-ttu-id="7f4d1-226">在頁面主體中，訊息變數的內容會顯示在 &lt;p&gt; 元素內。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-226">In the body of the page, the contents of the message variable are displayed inside a &lt;p&gt; element.</span></span> <span data-ttu-id="7f4d1-227">標記也會包含 &lt;輸入&gt; 元素，以建立**提交**按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-227">The markup also contains an &lt;input&gt; element to create a **Submit** button.</span></span>

<span data-ttu-id="7f4d1-228">執行頁面以查看其目前的運作方式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-228">Run the page to see how it works now.</span></span> <span data-ttu-id="7f4d1-229">現在，它基本上是靜態頁面，即使您按一下 [**提交**] 按鈕也一樣。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-229">For now, it's basically a static page, even if you click the **Submit** button.</span></span>

<span data-ttu-id="7f4d1-230">回到 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-230">Go back to WebMatrix.</span></span> <span data-ttu-id="7f4d1-231">在程式碼區塊中，將下列反白顯示的程式碼新增至初始化 message 的那一行*之後*：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-231">Inside the code block, add the following highlighted code *after* the line that initializes message:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a><span data-ttu-id="7f4d1-232">If {} 區塊</span><span class="sxs-lookup"><span data-stu-id="7f4d1-232">The if { } block</span></span>

<span data-ttu-id="7f4d1-233">您剛剛新增的是 if 條件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-233">What you just added was an if condition.</span></span> <span data-ttu-id="7f4d1-234">在程式碼中，if 條件的結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-234">In code, the if condition has a structure like this:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

<span data-ttu-id="7f4d1-235">要測試的條件是以括弧括住。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-235">The condition to test is in parentheses.</span></span> <span data-ttu-id="7f4d1-236">它必須是值或傳回 true 或 false 的運算式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-236">It has to be a value or an expression that returns true or false.</span></span> <span data-ttu-id="7f4d1-237">如果條件為 true，則 ASP.NET 會執行括弧內的語句或語句。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-237">If the condition is true, ASP.NET runs the statement or statements that are inside the braces.</span></span> <span data-ttu-id="7f4d1-238">（這些是*if then*邏輯的*then*部分）。如果條件為 false，則會略過程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-238">(Those are the *then* part of the *if-then* logic.) If the condition is false, the block of code is skipped.</span></span>

<span data-ttu-id="7f4d1-239">以下是您可以在 if 語句中測試之條件的幾個範例：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-239">Here are a few examples of conditions you can test in an if statement:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

<span data-ttu-id="7f4d1-240">您可以使用*邏輯運算子*或*比較運算子*，根據值或運算式來測試變數：等於（= =）、大於（&gt;）、小於（&lt;）、大於或等於（&gt;=）和小於或等於（&lt;=）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-240">You can test variables against values or against expressions by using a *logical operator* or *comparison operator*: equal to (==), greater than (&gt;), less than (&lt;), greater than or equal to (&gt;=), and less than or equal to (&lt;=).</span></span> <span data-ttu-id="7f4d1-241">！ = 運算子表示不等於，例如，如果（a！ = 0）表示不*等於 0*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-241">The != operator means not equal to — for example, if(a != 0) means *if a is not equal to 0*.</span></span>

> [!NOTE]
> <span data-ttu-id="7f4d1-242">請確定您注意到 equals 的比較運算子（= =）與 = 不相同。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-242">Make sure you notice that the comparison operator for equals to (==) is not the same as =.</span></span> <span data-ttu-id="7f4d1-243">= 運算子僅用於指派值（var a = 2）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-243">The = operator is used only to assign values (var a=2).</span></span> <span data-ttu-id="7f4d1-244">如果您混用這些運算子，您會收到錯誤訊息，否則會出現一些奇怪的結果。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-244">If you mix these operators up, you'll either get an error or you'll get some strange results.</span></span>

<span data-ttu-id="7f4d1-245">若要測試某個專案是否為 true，完整的語法為 if （作業 = = true）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-245">To test whether something is true, the complete syntax is if(IsDone == true).</span></span> <span data-ttu-id="7f4d1-246">但是，如果是（作業），您也可以使用快捷方式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-246">But you can also use the shortcut if(IsDone).</span></span> <span data-ttu-id="7f4d1-247">如果沒有比較運算子，ASP.NET 會假設您要測試是否為 true。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-247">If there's no comparison operator, ASP.NET assumes that you're testing for true.</span></span>

<span data-ttu-id="7f4d1-248">!</span><span class="sxs-lookup"><span data-stu-id="7f4d1-248">The !</span></span> <span data-ttu-id="7f4d1-249">operator 本身表示邏輯 NOT。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-249">operator by itself means a logical NOT.</span></span> <span data-ttu-id="7f4d1-250">例如，條件 if （！IsPost）表示*IsPost 是否為 true*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-250">For example, the condition if(!IsPost) means *if IsPost is not true*.</span></span>

<span data-ttu-id="7f4d1-251">您可以使用邏輯 AND （&amp;&amp; 運算子）或邏輯 OR （| | operator）來合併條件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-251">You can combine conditions by using a logical AND (&amp;&amp; operator) or logical OR (|| operator).</span></span> <span data-ttu-id="7f4d1-252">例如，前述範例中的最後一個 if 條件，表示*FileProcessingIsDone 未設定為 TRUE，而 displayMessage 設定為 false*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-252">For example, the last of the if conditions in the preceding examples means *if FileProcessingIsDone is not set to true AND displayMessage is set to false*.</span></span>

### <a name="the-else-block"></a><span data-ttu-id="7f4d1-253">Else 區塊</span><span class="sxs-lookup"><span data-stu-id="7f4d1-253">The else block</span></span>

<span data-ttu-id="7f4d1-254">If 區塊的最後一件事： if 區塊後面可以接著 else 區塊。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-254">One final thing about if blocks: an if block can be followed by an else block.</span></span> <span data-ttu-id="7f4d1-255">Else 區塊很有用，因為條件為 false 時，您必須執行不同的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-255">An else block is useful is you have to execute different code when the condition is false.</span></span> <span data-ttu-id="7f4d1-256">以下是簡單的範例：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-256">Here's a simple example:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

<span data-ttu-id="7f4d1-257">您會在本系列稍後的教學課程中看到一些範例，其中使用 else 區塊會很有用。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-257">You'll see some examples in later tutorials in this series where using an else block is useful.</span></span>

### <a name="testing-whether-the-request-is-a-submit-post"></a><span data-ttu-id="7f4d1-258">測試要求是否為提交（post）</span><span class="sxs-lookup"><span data-stu-id="7f4d1-258">Testing whether the request is a submit (post)</span></span>

<span data-ttu-id="7f4d1-259">還有更多，但讓我們回到範例，其中有 if （IsPost） {...} 的條件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-259">There's more, but let's get back to the example, which has the condition if(IsPost){ ... }.</span></span> <span data-ttu-id="7f4d1-260">IsPost 實際上是目前頁面的屬性。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-260">IsPost is actually a property of the current page.</span></span> <span data-ttu-id="7f4d1-261">第一次要求頁面時，IsPost 會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-261">The first time the page is requested, IsPost returns false.</span></span> <span data-ttu-id="7f4d1-262">不過，如果您按一下按鈕或提交頁面（也就是您張貼），則 IsPost 會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-262">However, if you click a button or otherwise submit the page — that is, you post it — IsPost returns true.</span></span> <span data-ttu-id="7f4d1-263">因此，IsPost 可讓您判斷是否正在處理表單提交。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-263">So IsPost lets you determine whether you're dealing with a form submission.</span></span> <span data-ttu-id="7f4d1-264">（就 HTTP 指令動詞而言，如果要求是 GET 作業，則 IsPost 會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-264">(In terms of HTTP verbs, if the request is a GET operation, IsPost returns false.</span></span> <span data-ttu-id="7f4d1-265">如果要求是 POST 作業，IsPost 會傳回 true。）在稍後的教學課程中，您將使用輸入表單，這項測試會特別有用。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-265">If the request is a POST operation, IsPost returns true.) In a later tutorial you'll work with input forms, where this test becomes particularly useful.</span></span>

<span data-ttu-id="7f4d1-266">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-266">Run the page.</span></span> <span data-ttu-id="7f4d1-267">因為這是您第一次要求頁面，所以您會看到「這是您第一次要求此頁面」。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-267">Because this is the first time you're requested the page, you see "This is the first time you've requested the page".</span></span> <span data-ttu-id="7f4d1-268">該字串是您用來初始化訊息變數的值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-268">That string is the value that you initialized the message variable to.</span></span> <span data-ttu-id="7f4d1-269">有一個 if （IsPost）測試，但它目前會傳回 false，因此在 if 區塊內的程式碼不會執行。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-269">There's an if(IsPost) test, but that returns false at the moment, so the code inside the if block doesn't run.</span></span>

<span data-ttu-id="7f4d1-270">按一下 [**提交**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-270">Click the **Submit** button.</span></span> <span data-ttu-id="7f4d1-271">再次要求頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-271">The page is requested again.</span></span> <span data-ttu-id="7f4d1-272">如前所述，message 變數會設定為「這是第一次 ...」。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-272">As before, the message variable is set to "This is the first time ...".</span></span> <span data-ttu-id="7f4d1-273">但這次，測試 if （IsPost）會傳回 true，因此 if 區塊內的程式碼會執行。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-273">But this time, the test if(IsPost) returns true, so the code inside the if block runs.</span></span> <span data-ttu-id="7f4d1-274">程式碼會將 message 變數的值變更為不同的值，這就是在標記中呈現的內容。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-274">The code changes the value of the message variable to a different value, which is what's rendered in the markup.</span></span>

<span data-ttu-id="7f4d1-275">現在，在標記中加入 if 條件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-275">Now add an if condition in the markup.</span></span> <span data-ttu-id="7f4d1-276">在包含 [**提交**] 按鈕的 &lt;p&gt; 元素底下，新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-276">Below the &lt;p&gt; element that contains the **Submit** button, add the following markup:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

<span data-ttu-id="7f4d1-277">您要在標記內加入程式碼，因此您必須從 @開始。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-277">You're adding code inside the markup, so you have to start with @.</span></span> <span data-ttu-id="7f4d1-278">然後會有一個 [if] 測試，與您稍早在程式碼區塊中新增的類似。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-278">Then there's an if test similar to the one you added earlier up in the code block.</span></span> <span data-ttu-id="7f4d1-279">不過，在大括弧內，您會加入一般的 HTML，至少在 @DateTime.Now之前，通常都是正常的。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-279">Inside the braces, though, you're adding ordinary HTML — at least, it's ordinary until it gets to @DateTime.Now.</span></span> <span data-ttu-id="7f4d1-280">這是另一小段 Razor 程式碼，因此您必須在前面加上 @。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-280">This is another little bit of Razor code, so again you have to add @ in front of it.</span></span>

<span data-ttu-id="7f4d1-281">這裡的重點是，您可以在程式碼區塊的頂端和標記中加入 if 條件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-281">The point here is that you can add if conditions in both the code block at the top and in the markup.</span></span> <span data-ttu-id="7f4d1-282">如果您在頁面主體中使用 if 條件，區塊內的程式列可以是標記或程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-282">If you use an if condition in the body of the page, the lines inside the block can be markup or code.</span></span> <span data-ttu-id="7f4d1-283">在這種情況下，當您混用標記和程式碼時，和都是如此，您必須使用 @ 讓它清楚 ASP.NET 程式碼所在的位置。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-283">In that case, and as is true anytime you mix markup and code, you have to use @ to make it clear to ASP.NET where the code is.</span></span>

<span data-ttu-id="7f4d1-284">執行頁面，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-284">Run the page and click **Submit**.</span></span> <span data-ttu-id="7f4d1-285">這次當您提交（「現在您已提交 ...」）時，您不只會看到不同的訊息，但是您會看到一則列出日期和時間的新訊息。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-285">This time you not only see a different message when you submit ("Now you've submitted ..."), but you see a new message that lists the date and time.</span></span>

![在瀏覽器中執行的 [測試 Razor 2] 頁面，包含提交後顯示的時間戳記](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a><span data-ttu-id="7f4d1-287">測試查詢字串的值</span><span class="sxs-lookup"><span data-stu-id="7f4d1-287">Testing the value of a query string</span></span>

<span data-ttu-id="7f4d1-288">另一個測試。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-288">One more test.</span></span> <span data-ttu-id="7f4d1-289">這次，您會新增一個 if 區塊來測試名為 show 且可能會在查詢字串中傳遞的值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-289">This time, you'll add an if block that tests a value named show that might be passed in the query string.</span></span> <span data-ttu-id="7f4d1-290">（如下所示： `http://localhost:43097/TestRazorPart2.cshtml?show=true`）您將變更頁面，使您已顯示的訊息（「這是第一次 ...」等等）只有在 show 的值為 true 時才會顯示。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-290">(Like this: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) You'll change the page so that the message you've been displaying ("This is the first time ...", etc.) is only displayed if the value of show is true.</span></span>

<span data-ttu-id="7f4d1-291">在頁面頂端的程式碼區塊底部（但內部），新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-291">At the bottom (but inside) the code block at the top of the page, add the following:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

<span data-ttu-id="7f4d1-292">完整的程式碼區塊現在看起來如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-292">The complete code block now look like the following example.</span></span> <span data-ttu-id="7f4d1-293">（請記住，當您將程式碼複製到頁面時，縮排可能看起來會不同。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-293">(Remember that when you copy the code into your page, the indentation might look different.</span></span> <span data-ttu-id="7f4d1-294">但這並不會影響程式碼執行的方式）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-294">But that doesn't affect how the code runs.)</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

<span data-ttu-id="7f4d1-295">區塊中的新程式碼會將名為 showMessage 的變數初始化為 false。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-295">The new code in the block initializes a variable named showMessage to false.</span></span> <span data-ttu-id="7f4d1-296">然後，它會執行 if 測試，以在查詢字串中尋找值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-296">It then does an if test to look for a value in the query string.</span></span> <span data-ttu-id="7f4d1-297">當您第一次要求頁面時，它會有如下的 URL：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-297">When you first request the page, it has a URL like this one:</span></span>

`http://localhost:43097/TestRazorPart2.cshtml`

<span data-ttu-id="7f4d1-298">此程式碼會判斷 URL 是否包含查詢字串中名為 show 的變數，如下列 URL 版本所示：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-298">The code determines whether the URL contains a variable named show in the query string, like this version of the URL:</span></span>

<span data-ttu-id="7f4d1-299">`http://localhost:43097/TestRazorPart2.cshtml`？ show = true</span><span class="sxs-lookup"><span data-stu-id="7f4d1-299">`http://localhost:43097/TestRazorPart2.cshtml`?show=true</span></span>

<span data-ttu-id="7f4d1-300">測試本身會查看 Request 物件的 QueryString 屬性。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-300">The test itself looks at the QueryString property of the Request object.</span></span> <span data-ttu-id="7f4d1-301">如果查詢字串包含名為 show 的專案，而且該專案設定為 true，則 if 區塊會執行，並將 showMessage 變數設定為 true。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-301">If the query string contains an item named show, and if that item is set to true, the if block runs and sets the showMessage variable to true.</span></span>

<span data-ttu-id="7f4d1-302">這裡有個秘訣，如您所見。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-302">There's a trick here, as you can see.</span></span> <span data-ttu-id="7f4d1-303">如同名稱所示，查詢字串是一個字串。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-303">Like the name says, the query string is a string.</span></span> <span data-ttu-id="7f4d1-304">不過，如果您要測試的值是布林值（true/false），則只能測試 true 和 false。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-304">However, you can only test for true and false if the value you're testing is a Boolean (true/false) value.</span></span> <span data-ttu-id="7f4d1-305">您必須先將查詢字串中的 show 變數值轉換成布林值，才可以在此測試字串中測試它。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-305">Before you can test the value of the show variable in the query string, you have to convert it to a Boolean value.</span></span> <span data-ttu-id="7f4d1-306">這就是 AsBool 方法的作用-它會採用字串做為輸入，並將它轉換成布林值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-306">That's what the AsBool method does — it takes a string as input and converts it to a Boolean value.</span></span> <span data-ttu-id="7f4d1-307">很明顯地，如果字串為 "true"，則 AsBool 方法會將該值轉換為 true。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-307">Clearly, if the string is "true", the AsBool method converts that value to true.</span></span> <span data-ttu-id="7f4d1-308">如果字串的值為任何其他專案，則 AsBool 會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-308">If the value of the string is anything else, AsBool returns false.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="7f4d1-309">**資料類型和 As （）方法**</span><span class="sxs-lookup"><span data-stu-id="7f4d1-309">**Data Types and As() Methods**</span></span>
> 
> <span data-ttu-id="7f4d1-310">我們目前只有在建立變數時才會用到關鍵字 var。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-310">We've only said so far that when you create a variable, you use the keyword var.</span></span> <span data-ttu-id="7f4d1-311">不過，這不是整個故事。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-311">That's not the entire story, though.</span></span> <span data-ttu-id="7f4d1-312">若要操作值，以加入數位或串連字號串，或比較日期或測試是否為 true/false， C#必須使用適當的值內部標記法。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-312">In order to manipulate values — to add numbers, or concatenate strings, or compare dates, or test for true/false — C# has to work with an appropriate internal representation of the value.</span></span> <span data-ttu-id="7f4d1-313">C#*通常*可以根據您所執行的值，找出該標記法（也就是資料的*類型*）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-313">C# can *usually* figure out what that representation should be (that is, what *type* the data is) based on what you're doing with the values.</span></span> <span data-ttu-id="7f4d1-314">不過，現在它不能這麼做。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-314">Now and then, though, it can't do that.</span></span> <span data-ttu-id="7f4d1-315">如果沒有，您就必須明確指出應該如何C#呈現資料，以協助您。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-315">If not, you have to help out by explicitly indicating how C# should represent the data.</span></span> <span data-ttu-id="7f4d1-316">AsBool 方法會這麼做，它會C#告知字串值 "true" 或 "false" 應視為布林值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-316">The AsBool method does that — it tells C# that a string value of "true" or "false" should be treated as a Boolean value.</span></span> <span data-ttu-id="7f4d1-317">也有類似的方法，將字串表示為其他類型，例如 AsInt （視為整數）、AsDateTime （視為日期/時間）、AsFloat （視為浮點數）等等。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-317">Similar methods exist to represent strings as other types as well, like AsInt (treat as an integer), AsDateTime (treat as a date/time), AsFloat (treat as a floating-point number), and so on.</span></span> <span data-ttu-id="7f4d1-318">當您使用這些 As （）方法時， C#如果無法代表要求的字串值，您會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-318">When you use these As( ) methods, if C# can't represent the string value as requested, you'll see an error.</span></span>

<span data-ttu-id="7f4d1-319">在頁面的標記中，移除或批註化此元素（這裡會顯示為批註）：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-319">In the markup of the page, remove or comment out this element (here it's shown commented out):</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

<span data-ttu-id="7f4d1-320">在您移除或取消批註該文字的右方，新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-320">Right where you removed or commented out that text, add the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

<span data-ttu-id="7f4d1-321">If 測試指出如果 showMessage 變數為 true，則會以 message 變數的值呈現 &lt;p&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-321">The if test says that if the showMessage variable is true, render a &lt;p&gt; element with the value of the message variable.</span></span>

### <a name="summary-of-your-conditional-logic"></a><span data-ttu-id="7f4d1-322">條件式邏輯的摘要</span><span class="sxs-lookup"><span data-stu-id="7f4d1-322">Summary of your conditional logic</span></span>

<span data-ttu-id="7f4d1-323">如果您不確定剛完成的作業，這裡有一個摘要。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-323">In case you're not entirely sure of what you've just done, here's a summary.</span></span>

- <span data-ttu-id="7f4d1-324">Message 變數會初始化為預設字串（「這是第一次 ...」）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-324">The message variable is initialized to a default string ("This is the first time ...").</span></span>
- <span data-ttu-id="7f4d1-325">如果頁面要求是提交（post）的結果，則訊息的值會變更為「現在您已提交 ...」</span><span class="sxs-lookup"><span data-stu-id="7f4d1-325">If the page request is the result of a submit (post), the value of message is changed to "Now you've submitted ..."</span></span>
- <span data-ttu-id="7f4d1-326">ShowMessage 變數已初始化為 false。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-326">The showMessage variable is initialized to false.</span></span>
- <span data-ttu-id="7f4d1-327">如果查詢字串包含？ show = true，則 showMessage 變數會設定為 true。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-327">If the query string contains ?show=true, the showMessage variable is set to true.</span></span>
- <span data-ttu-id="7f4d1-328">在標記中，如果 showMessage 為 true，則會轉譯 &lt;p&gt; 元素，以顯示 message 的值。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-328">In the markup, if showMessage is true, a &lt;p&gt; element is rendered that shows the value of message.</span></span> <span data-ttu-id="7f4d1-329">（如果 showMessage 為 false，則在標記中的該時間點不會轉譯任何內容）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-329">(If showMessage is false, nothing is rendered at that point in the markup.)</span></span>
- <span data-ttu-id="7f4d1-330">在標記中，如果要求是 post，則會轉譯 &lt;p&gt; 元素，以顯示日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-330">In the markup, if the request is a post, a &lt;p&gt; element is rendered that displays the date and time.</span></span>

<span data-ttu-id="7f4d1-331">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-331">Run the page.</span></span> <span data-ttu-id="7f4d1-332">沒有訊息，因為 showMessage 是 false，所以在標記中，if （showMessage）測試會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-332">There's no message, because showMessage is false, so in the markup the if(showMessage) test returns false.</span></span>

<span data-ttu-id="7f4d1-333">按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-333">Click **Submit**.</span></span> <span data-ttu-id="7f4d1-334">您會看到日期和時間，但仍然沒有訊息。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-334">You see the date and time, but still no message.</span></span>

<span data-ttu-id="7f4d1-335">在瀏覽器中，移至 [URL] 方塊，並將下列內容新增至 URL 結尾：？ show = true，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-335">In your browser, go to the URL box and add the following to the end of the URL: ?show=true and then press Enter.</span></span>

![顯示查詢字串的瀏覽器中的 [測試 Razor 2] 頁面](intro-to-web-pages-programming/_static/image5.png)

<span data-ttu-id="7f4d1-337">該頁面會再次顯示。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-337">The page is displayed again.</span></span> <span data-ttu-id="7f4d1-338">（因為您變更了 URL，所以這是新的要求，而不是提交）。再次按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-338">(Because you changed the URL, this is a new request, not a submit.) Click **Submit** again.</span></span> <span data-ttu-id="7f4d1-339">訊息會再次顯示，如同日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-339">The message is displayed again, as is the date and time.</span></span>

![當有查詢字串時，提交後的 [測試 Razor 2] 頁面](intro-to-web-pages-programming/_static/image6.png)

<span data-ttu-id="7f4d1-341">在 [URL] 中，將？ show = true 變更為？ show = false，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-341">In the URL, change ?show=true to ?show=false and press Enter.</span></span> <span data-ttu-id="7f4d1-342">再次提交頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-342">Submit the page again.</span></span> <span data-ttu-id="7f4d1-343">頁面會回到您的啟動方式—沒有訊息。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-343">The page is back to how you started — no message.</span></span>

<span data-ttu-id="7f4d1-344">如先前所述，此範例的邏輯有點假設。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-344">As noted earlier, the logic of this example is a little contrived.</span></span> <span data-ttu-id="7f4d1-345">不過，如果要在許多頁面中出現，則會採用您在這裡看到的一或多個表單。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-345">However, if is going to come up in many of your pages, and it will take one or more of the forms you've seen here.</span></span>

## <a name="installing-a-helper-displaying-a-gravatar-image"></a><span data-ttu-id="7f4d1-346">安裝 Helper （顯示 Gravatar 的影像）</span><span class="sxs-lookup"><span data-stu-id="7f4d1-346">Installing a Helper (Displaying a Gravatar Image)</span></span>

<span data-ttu-id="7f4d1-347">人們通常會想要在網頁上執行的某些工作需要大量的程式碼，或需要額外的知識。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-347">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="7f4d1-348">範例：顯示資料的圖表;將 Facebook 「贊」按鈕放在頁面上;正在從您的網站傳送電子郵件;裁剪或調整影像大小;針對您的網站使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-348">Examples: displaying a chart for data; putting a Facebook "Like" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="7f4d1-349">為了讓您輕鬆執行這類工作，ASP.NET Web Pages 可讓*您使用協助*程式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-349">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="7f4d1-350">Helper 是您為網站安裝的元件，可讓您只使用幾行 Razor 程式碼來執行一般工作。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-350">Helpers are components that you install for a site and that let you perform typical tasks by using just a few lines of Razor code.</span></span>

<span data-ttu-id="7f4d1-351">ASP.NET Web Pages 內建了一些協助程式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-351">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="7f4d1-352">不過，許多協助程式都可以在使用 NuGet 套件管理員所提供的封裝（增益集）中取得。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-352">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="7f4d1-353">NuGet 可讓您選取要安裝的套件，然後負責安裝的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-353">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

<span data-ttu-id="7f4d1-354">在本教學課程的這個部分中，您將會安裝協助程式，讓您顯示 Gravatar （「全球辨識的頭像」）影像。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-354">In this part of the tutorial, you'll install a helper that lets you display a Gravatar ("globally recognized avatar") image.</span></span> <span data-ttu-id="7f4d1-355">您將會學到兩件事。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-355">You'll learn two things.</span></span> <span data-ttu-id="7f4d1-356">其中一個是如何尋找及安裝 helper。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-356">One is how to find and install a helper.</span></span> <span data-ttu-id="7f4d1-357">您也將瞭解協助專家如何使用許多您必須自行撰寫的程式碼，輕鬆地執行某些動作。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-357">You'll also learn how a helper makes it easy to do something you'd otherwise need to do by using a lot of code you'd have to write yourself.</span></span>

<span data-ttu-id="7f4d1-358">您可以在位於[http://www.gravatar.com/](http://www.gravatar.com/)的 Gravatar 網站註冊自己的 Gravatar，但建立 Gravatar 帳戶來執行本教學課程部分並不重要。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-358">You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/), but it is not essential to create a Gravatar account to perform this part of the tutorial.</span></span>

<span data-ttu-id="7f4d1-359">在 WebMatrix 中，按一下 [ **NuGet** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-359">In WebMatrix, click the **NuGet** button.</span></span>

![WebMatrix 中的 [NuGet 資源庫] 對話方塊](intro-to-web-pages-programming/_static/image7.png)

<span data-ttu-id="7f4d1-361">這會啟動 NuGet 套件管理員，並顯示可用的套件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-361">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="7f4d1-362">（並非所有的封裝都是協助程式; 有些會將功能加入至 WebMatrix 本身，有些則是額外的範本）。您可能會收到與版本不相容相關的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-362">(Not all of the packages are helpers; some add functionality to WebMatrix itself, some are additional templates, and so on.) You may get an error message about version incompatibility.</span></span> <span data-ttu-id="7f4d1-363">您可以按一下 **[確定]** 並繼續進行本教學課程，以忽略此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-363">You can ignore this error message by clicking **OK** and proceeding with this tutorial.</span></span>

![WebMatrix 中的 [NuGet 資源庫] 對話方塊](intro-to-web-pages-programming/_static/image8.png)

<span data-ttu-id="7f4d1-365">在搜尋方塊中，輸入 "asp.net helper"。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-365">In the search box, enter "asp.net helpers".</span></span> <span data-ttu-id="7f4d1-366">NuGet 會顯示符合搜尋詞彙的套件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-366">NuGet shows the packages that match the search terms.</span></span>

![WebMatrix 中的 NuGet 資源庫顯示套件](intro-to-web-pages-programming/_static/image9.png)

<span data-ttu-id="7f4d1-368">ASP.NET Web helper 程式庫包含可簡化許多一般工作的程式碼，包括使用 Gravatar 影像。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-368">The ASP.NET Web Helpers Library contains code to simplify many common tasks, including the use of Gravatar images.</span></span> <span data-ttu-id="7f4d1-369">選取**ASP.NET Web** Helper 程式庫套件，然後按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-369">Select the **ASP.NET Web Helpers Library** package and then click **Install** to launch the installer.</span></span> <span data-ttu-id="7f4d1-370">當系統詢問您是否要安裝套件，並接受條款以完成安裝時，請選取 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-370">Select **Yes** when asked if you want to install the package, and accept the terms to complete the installation.</span></span>

<span data-ttu-id="7f4d1-371">就這麼容易！</span><span class="sxs-lookup"><span data-stu-id="7f4d1-371">That's it.</span></span> <span data-ttu-id="7f4d1-372">NuGet 會下載並安裝所有專案，包括任何可能需要的其他元件 *（相依*性）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-372">NuGet downloads and installs everything, including any additional components that might be required (*dependencies*).</span></span>

<span data-ttu-id="7f4d1-373">如果您因為某些原因而必須卸載協助程式，則進程非常類似。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-373">If for some reason you have to uninstall a helper, the process is very similar.</span></span> <span data-ttu-id="7f4d1-374">按一下 [ **NuGet** ] 按鈕，按一下 [**已安裝**] 索引標籤，然後挑選您要卸載的套件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-374">Click the **NuGet** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="using-a-helper-in-a-page"></a><span data-ttu-id="7f4d1-375">在頁面中使用 Helper</span><span class="sxs-lookup"><span data-stu-id="7f4d1-375">Using a Helper in a Page</span></span>

<span data-ttu-id="7f4d1-376">現在您將使用剛安裝的 helper。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-376">Now you'll use the helper that you just installed.</span></span> <span data-ttu-id="7f4d1-377">將協助程式新增至頁面的程式，與大部分的協助程式類似。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-377">The process for adding a helper to a page is similar for most helpers.</span></span>

<span data-ttu-id="7f4d1-378">在 WebMatrix 中建立頁面，並將它命名為*GravatarTest. cshml*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-378">In WebMatrix, create a page and name it *GravatarTest.cshml*.</span></span> <span data-ttu-id="7f4d1-379">（您要建立一個特殊的頁面來測試協助程式，但是您可以在網站的任何頁面中使用 helper）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-379">(You're creating a special page to test the helper, but you can use helpers in any page in your site.)</span></span>

<span data-ttu-id="7f4d1-380">在 &lt;主體&gt; 元素內，新增 &lt;div&gt; 專案。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-380">Inside the &lt;body&gt; element, add a &lt;div&gt; element.</span></span> <span data-ttu-id="7f4d1-381">在 &lt;div&gt; 元素內，輸入下列內容：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-381">Inside the &lt;div&gt; element, type this:</span></span>

<span data-ttu-id="7f4d1-382">@Gravatar</span><span class="sxs-lookup"><span data-stu-id="7f4d1-382">@Gravatar.</span></span>

<span data-ttu-id="7f4d1-383">@ 字元與您用來標示 Razor 程式碼的字元相同。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-383">The @ character is the same character you've been using to mark Razor code.</span></span> <span data-ttu-id="7f4d1-384">**Gravatar**是您要使用的 helper 物件。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-384">**Gravatar** is the helper object that you're working with.</span></span>

<span data-ttu-id="7f4d1-385">一旦您輸入句號（.），WebMatrix 會顯示 Gravatar helper 提供的*方法*（函式）清單：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-385">As soon as you type the period (.), WebMatrix displays a list of *methods* (functions) that the Gravatar helper makes available:</span></span>

![Gravatar helper IntelliSense 下拉式清單](intro-to-web-pages-programming/_static/image10.png)

<span data-ttu-id="7f4d1-387">這項功能稱為*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-387">This feature is known as *IntelliSense*.</span></span> <span data-ttu-id="7f4d1-388">它會提供內容適當的選擇，協助您撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-388">It helps you code by providing context-appropriate choices.</span></span> <span data-ttu-id="7f4d1-389">IntelliSense 適用于在 WebMatrix 中支援的 HTML、CSS、ASP.NET 程式碼、JavaScript 和其他語言。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-389">IntelliSense works with HTML, CSS, ASP.NET code, JavaScript, and other languages that are supported in WebMatrix.</span></span> <span data-ttu-id="7f4d1-390">這是另一項功能，可讓您更輕鬆地在 WebMatrix 中開發網頁。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-390">It's another feature that makes it easier to develop web pages in WebMatrix.</span></span>

<span data-ttu-id="7f4d1-391">在鍵盤上按 G，您會看到 IntelliSense 找到 Recaptcha.gethtml 方法。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-391">Press G on the keyboard, and you see that IntelliSense finds the GetHtml method.</span></span> <span data-ttu-id="7f4d1-392">按下 Tab 鍵。 IntelliSense 會為您插入選取的方法（Recaptcha.gethtml）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-392">Press Tab. IntelliSense inserts the selected method (GetHtml) for you.</span></span> <span data-ttu-id="7f4d1-393">輸入左括弧，並注意右括弧會自動新增。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-393">Type an open parenthesis, and notice that the closing parenthesis is automatically added.</span></span> <span data-ttu-id="7f4d1-394">在兩個括弧之間的引號中輸入您的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-394">Type your email address in quotation marks between the two parenthesis.</span></span> <span data-ttu-id="7f4d1-395">如果您有 Gravatar 帳戶，則會傳回您的個人資料圖片。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-395">If you have a Gravatar account, your profile picture will be returned.</span></span> <span data-ttu-id="7f4d1-396">如果您沒有 Gravatar 帳戶，則會傳回預設映射。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-396">If you do not have a Gravatar account, a default image is returned.</span></span> <span data-ttu-id="7f4d1-397">當您完成時，該行看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="7f4d1-397">When you're done, the line looks like this:</span></span>

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

<span data-ttu-id="7f4d1-398">現在請在瀏覽器中查看頁面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-398">Now view the page in a browser.</span></span> <span data-ttu-id="7f4d1-399">視您是否有 Gravatar 帳戶而定，會顯示您的圖片或預設影像。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-399">Either your picture or the default image is displayed, depending on whether you have a Gravatar account.</span></span>

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![預設影像](intro-to-web-pages-programming/_static/image12.png)

<span data-ttu-id="7f4d1-402">若要瞭解協助專家為您做什麼，請在瀏覽器中查看頁面的來源。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-402">To get an idea of what the helper is doing for you, view the source of the page in the browser.</span></span> <span data-ttu-id="7f4d1-403">除了您在頁面中所擁有的 HTML 之外，您還會看到包含識別碼的 image 元素。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-403">Along with the HTML that you had in your page, you see an image element that includes an identifier.</span></span> <span data-ttu-id="7f4d1-404">這是協助程式在您已 @Gravatar.GetHtml的位置呈現在頁面中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-404">This is code that the helper rendered into the page at the place where you had @Gravatar.GetHtml.</span></span> <span data-ttu-id="7f4d1-405">Helper 會採用您提供的資訊，並產生直接與 Gravatar 交談的程式碼，以取得所提供帳戶的正確影像。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-405">The helper took the information you provided and generated the code that talks directly to Gravatar in order to get back the correct image for supplied account.</span></span>

<span data-ttu-id="7f4d1-406">Recaptcha.gethtml 方法也可讓您藉由提供其他參數來自訂映射。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-406">The GetHtml method also enables you to customize the image by providing other parameters.</span></span> <span data-ttu-id="7f4d1-407">下列程式碼示範如何要求影像的寬度和高度為40圖元，如果指定的帳號不存在，則會使用名為**wavatar**的指定預設映射。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-407">The following code shows how to request an image has a width and height of 40 pixels, and uses a specified default image named **wavatar** if the specified account does not exist.</span></span>

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

<span data-ttu-id="7f4d1-408">此程式碼會產生類似下列結果的內容（預設映射會隨機改變）。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-408">This code produces something like the following result (the default image will randomly vary).</span></span>

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a><span data-ttu-id="7f4d1-409">下一步</span><span class="sxs-lookup"><span data-stu-id="7f4d1-409">Coming Up Next</span></span>

<span data-ttu-id="7f4d1-410">為了讓本教學課程簡短，我們必須只著重于幾個基本概念。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-410">To keep this tutorial short, we had to focus on only a few basics.</span></span> <span data-ttu-id="7f4d1-411">而且 Razor 和C#還有*許多*其他方面。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-411">Naturally, there's a *lot* more to Razor and C#.</span></span> <span data-ttu-id="7f4d1-412">當您完成這些教學課程時，您將會進一步瞭解。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-412">You'll learn more as you go through these tutorials.</span></span> <span data-ttu-id="7f4d1-413">如果您想要深入瞭解 Razor 和C#目前的程式設計方面，您可以在這裡閱讀更詳盡的簡介：[使用 Razor 語法進行 Web 程式設計的簡介 ASP.NET](https://go.microsoft.com/fwlink/?LinkID=202890)。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-413">If you're interested in learning more about the programming aspects of Razor and C# right now, you can read a more thorough introduction here: [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=202890).</span></span>

<span data-ttu-id="7f4d1-414">下一個教學課程將為您介紹如何使用資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-414">The next tutorial introduces you to working with a database.</span></span> <span data-ttu-id="7f4d1-415">在該教學課程中，您將開始建立範例應用程式，讓您列出最愛的電影。</span><span class="sxs-lookup"><span data-stu-id="7f4d1-415">In that tutorial, you'll begin creating the sample application that lets you list your favorite movies.</span></span>

## <a name="complete-listing-for-testrazor-page"></a><span data-ttu-id="7f4d1-416">TestRazor 頁面的完整清單</span><span class="sxs-lookup"><span data-stu-id="7f4d1-416">Complete Listing for TestRazor Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a><span data-ttu-id="7f4d1-417">TestRazorPart2 頁面的完整清單</span><span class="sxs-lookup"><span data-stu-id="7f4d1-417">Complete Listing for TestRazorPart2 Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a><span data-ttu-id="7f4d1-418">GravatarTest 頁面的完整清單</span><span class="sxs-lookup"><span data-stu-id="7f4d1-418">Complete Listing for GravatarTest Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="7f4d1-419">其他資源</span><span class="sxs-lookup"><span data-stu-id="7f4d1-419">Additional Resources</span></span>

- [<span data-ttu-id="7f4d1-420">使用 Razor 語法 ASP.NET Web 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="7f4d1-420">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- [<span data-ttu-id="7f4d1-421">Twitter helper</span><span class="sxs-lookup"><span data-stu-id="7f4d1-421">Twitter helper</span></span>](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> <span data-ttu-id="7f4d1-422">[上一頁](getting-started.md)
> [下一頁](displaying-data.md)</span><span class="sxs-lookup"><span data-stu-id="7f4d1-422">[Previous](getting-started.md)
[Next](displaying-data.md)</span></span>
