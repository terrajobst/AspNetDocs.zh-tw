---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 在 ASP.NET Web Pages （Razor）網站中建立和使用 Helper |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何在 ASP.NET Web Pages （Razor）網站中建立協助程式。 Helper 是可重複使用的元件，其中包含程式碼和標記到效能 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563508"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="4699b-104">在 ASP.NET Web Pages （Razor）網站中建立和使用 Helper</span><span class="sxs-lookup"><span data-stu-id="4699b-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="4699b-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4699b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4699b-106">本文說明如何在 ASP.NET Web Pages （Razor）網站中建立協助程式。</span><span class="sxs-lookup"><span data-stu-id="4699b-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="4699b-107">*Helper*是可重複使用的元件，其中包含程式碼和標記來執行可能單調乏味或複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="4699b-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="4699b-108">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="4699b-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="4699b-109">如何建立和使用簡單的 helper。</span><span class="sxs-lookup"><span data-stu-id="4699b-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="4699b-110">以下是文章中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="4699b-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="4699b-111">`@helper` 語法。</span><span class="sxs-lookup"><span data-stu-id="4699b-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4699b-112">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="4699b-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4699b-113">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="4699b-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="4699b-114">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="4699b-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="4699b-115">協助程式總覽</span><span class="sxs-lookup"><span data-stu-id="4699b-115">Overview of Helpers</span></span>

<span data-ttu-id="4699b-116">如果您需要在網站中的不同頁面上執行相同的工作，您可以使用 helper。</span><span class="sxs-lookup"><span data-stu-id="4699b-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="4699b-117">ASP.NET Web Pages 包含一些協助程式，還有更多您可以下載和安裝的資訊。</span><span class="sxs-lookup"><span data-stu-id="4699b-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="4699b-118">（ASP.NET Web Pages 中的內建協助程式清單列在[ASP.NET API 快速參考](https://go.microsoft.com/fwlink/?LinkId=202907)中）。如果現有的協助程式都不符合您的需求，您可以建立自己的 helper。</span><span class="sxs-lookup"><span data-stu-id="4699b-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="4699b-119">協助程式可讓您在多個頁面上使用通用的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="4699b-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="4699b-120">假設在您的頁面中，您通常會想要建立與一般段落分開設定的便箋專案。</span><span class="sxs-lookup"><span data-stu-id="4699b-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="4699b-121">可能會將便箋建立為 `<div>` 元素，而此專案的樣式為具有框線的方塊。</span><span class="sxs-lookup"><span data-stu-id="4699b-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="4699b-122">您不需要在每次想要顯示附注時，將這個相同標記新增至頁面，而是可以將標記封裝為 helper。</span><span class="sxs-lookup"><span data-stu-id="4699b-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="4699b-123">然後您就可以在任何需要的地方插入含有一行程式碼的附注。</span><span class="sxs-lookup"><span data-stu-id="4699b-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="4699b-124">使用這樣的協助程式，可讓每個頁面中的程式碼更簡單且更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="4699b-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="4699b-125">它也可讓您更輕鬆地維護您的網站，因為如果您需要變更便箋的外觀，您可以在同一個位置變更標記。</span><span class="sxs-lookup"><span data-stu-id="4699b-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="4699b-126">建立 Helper</span><span class="sxs-lookup"><span data-stu-id="4699b-126">Creating a Helper</span></span>

<span data-ttu-id="4699b-127">此程式會示範如何建立協助程式，以依照剛才所述的方式建立附注。</span><span class="sxs-lookup"><span data-stu-id="4699b-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="4699b-128">這是一個簡單的範例，但是自訂 helper 可以包含您所需的任何標記和 ASP.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4699b-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="4699b-129">在網站的根資料夾中，建立名為 App 的資料夾 *\_程式碼*。</span><span class="sxs-lookup"><span data-stu-id="4699b-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="4699b-130">這是 ASP.NET 中的保留資料夾名稱，您可以在其中放置 helper 等元件的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4699b-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="4699b-131">在*應用程式\_Code*  資料夾中，建立新的*cshtml*檔案，並將它命名為*MyHelpers*。</span><span class="sxs-lookup"><span data-stu-id="4699b-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="4699b-132">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="4699b-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="4699b-133">程式碼會使用 `@helper` 語法來宣告名為 `MakeNote`的新 helper。</span><span class="sxs-lookup"><span data-stu-id="4699b-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="4699b-134">這個特定的協助程式可讓您傳遞名為 `content` 的參數，其中可包含文字和標記的組合。</span><span class="sxs-lookup"><span data-stu-id="4699b-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="4699b-135">Helper 會使用 `@content` 變數，將字串插入至便箋主體。</span><span class="sxs-lookup"><span data-stu-id="4699b-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="4699b-136">請注意，此檔案的名稱為*MyHelpers*，但協助程式名為 `MakeNote`。</span><span class="sxs-lookup"><span data-stu-id="4699b-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="4699b-137">您可以將多個自訂 helper 放入單一檔案。</span><span class="sxs-lookup"><span data-stu-id="4699b-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="4699b-138">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="4699b-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="4699b-139">在頁面中使用 Helper</span><span class="sxs-lookup"><span data-stu-id="4699b-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="4699b-140">在根資料夾中，建立名為*TestHelper*的新空白檔案。</span><span class="sxs-lookup"><span data-stu-id="4699b-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="4699b-141">將下列程式碼加入檔案：</span><span class="sxs-lookup"><span data-stu-id="4699b-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="4699b-142">若要呼叫您所建立的協助程式，請使用 `@`，後面接著 helper 所在的檔案名、句點，然後是 helper 名稱。</span><span class="sxs-lookup"><span data-stu-id="4699b-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="4699b-143">（如果您在*應用程式\_Code*資料夾中有多個資料夾，您可以使用語法 `@FolderName.FileName.HelperName`，在任何嵌套的資料夾層級中呼叫您的 helper）。</span><span class="sxs-lookup"><span data-stu-id="4699b-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="4699b-144">您在括弧內以引號括住的文字，就是協助專家會在網頁中顯示為便箋一部分的文字。</span><span class="sxs-lookup"><span data-stu-id="4699b-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="4699b-145">儲存頁面，並在瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="4699b-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="4699b-146">Helper 會產生您在兩個段落之間呼叫 helper 的「附注專案」。</span><span class="sxs-lookup"><span data-stu-id="4699b-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![螢幕擷取畫面：顯示瀏覽器中的頁面，以及協助程式產生的標記如何將方塊放在指定的文字周圍。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="4699b-148">其他資源</span><span class="sxs-lookup"><span data-stu-id="4699b-148">Additional Resources</span></span>

<span data-ttu-id="4699b-149">[以水準功能表作為 Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。</span><span class="sxs-lookup"><span data-stu-id="4699b-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="4699b-150">Mike Pope 的這個 blog 專案會示範如何使用標記、CSS 和程式碼，將水準功能表建立為協助程式。</span><span class="sxs-lookup"><span data-stu-id="4699b-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="4699b-151">[在 WebMatrix 和 ASP.NET MVC3 的 ASP.NET Web Pages 協助程式中運用 HTML5](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4699b-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="4699b-152">Sam Abraham 的這個 blog 專案會顯示轉譯 HTML5 `Canvas` 元素的 helper。</span><span class="sxs-lookup"><span data-stu-id="4699b-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="4699b-153">[WebMatrix 中 @Helpers 和 @Functions 之間的差異](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。</span><span class="sxs-lookup"><span data-stu-id="4699b-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="4699b-154">Mike Brind 的這個 blog 專案描述 `@helper` 語法和 `@function` 語法，以及每個語法的使用時機。</span><span class="sxs-lookup"><span data-stu-id="4699b-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
