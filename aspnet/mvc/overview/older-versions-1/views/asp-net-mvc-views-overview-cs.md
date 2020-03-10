---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
title: ASP.NET MVC Views 總覽（C#） |Microsoft Docs
author: StephenWalther
description: 什麼是 ASP.NET MVC 視圖，其與 HTML 網頁有何不同？ 在本教學課程中，Stephen Walther 會向您介紹 Views，並示範如何進行 。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 152ab1e5-aec2-4ea7-b8cc-27a24dd9acb8
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: b3f44aa9654a2a718381eaf9c856ca3e15ed1e27
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600314"
---
# <a name="aspnet-mvc-views-overview-c"></a><span data-ttu-id="6ef9b-104">ASP.NET MVC 檢視概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="6ef9b-104">ASP.NET MVC Views Overview (C#)</span></span>

<span data-ttu-id="6ef9b-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="6ef9b-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="6ef9b-106">什麼是 ASP.NET MVC 視圖，其與 HTML 網頁有何不同？</span><span class="sxs-lookup"><span data-stu-id="6ef9b-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="6ef9b-107">在本教學課程中，Stephen Walther 會向您介紹 Views，並示範如何在視圖中利用視圖資料和 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>

<span data-ttu-id="6ef9b-108">本教學課程的目的是為您提供 ASP.NET MVC views、view data 和 HTML helper 的簡介。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="6ef9b-109">本教學課程結束時，您應該瞭解如何建立新的視圖、將資料從控制器傳遞至視圖，以及使用 HTML 協助程式來產生視圖中的內容。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="6ef9b-110">了解檢視</span><span class="sxs-lookup"><span data-stu-id="6ef9b-110">Understanding Views</span></span>

<span data-ttu-id="6ef9b-111">若為 ASP.NET 或 Active Server Pages，ASP.NET MVC 不會包含直接對應至頁面的任何專案。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-111">For ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="6ef9b-112">在 ASP.NET MVC 應用程式中，磁片上沒有對應至您在瀏覽器網址列中輸入的路徑的頁面。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="6ef9b-113">ASP.NET MVC 應用程式中最接近的頁面，就是所謂的*觀點*。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="6ef9b-114">在 ASP.NET MVC 應用程式中，傳入瀏覽器要求會對應至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="6ef9b-115">控制器動作可能會傳回一個視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-115">A controller action might return a view.</span></span> <span data-ttu-id="6ef9b-116">不過，控制器動作可能會執行一些其他類型的動作，例如將您重新導向至另一個控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="6ef9b-117">[清單 1] 包含名為 HomeController 的簡單控制器。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="6ef9b-118">HomeController 會公開名為 Index （）和 Details （）的兩個控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="6ef9b-119">**清單 1-HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="6ef9b-119">**Listing 1 - HomeController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample1.cs)]

<span data-ttu-id="6ef9b-120">您可以在瀏覽器網址列中輸入下列 URL，以叫用第一個動作，也就是 Index （）動作：</span><span class="sxs-lookup"><span data-stu-id="6ef9b-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="6ef9b-121">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="6ef9b-121">/Home/Index</span></span>

<span data-ttu-id="6ef9b-122">您可以藉由在瀏覽器中輸入下列位址，叫用第二個動作，也就是詳細資料（）動作：</span><span class="sxs-lookup"><span data-stu-id="6ef9b-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="6ef9b-123">/Home/Details</span><span class="sxs-lookup"><span data-stu-id="6ef9b-123">/Home/Details</span></span>

<span data-ttu-id="6ef9b-124">Index （）動作會傳回 view。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-124">The Index() action returns a view.</span></span> <span data-ttu-id="6ef9b-125">您所建立的大部分動作都會傳回 views。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-125">Most actions that you create will return views.</span></span> <span data-ttu-id="6ef9b-126">不過，動作可能會傳回其他類型的動作結果。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="6ef9b-127">例如，Details （）動作會傳回將傳入要求重新導向至 Index （）動作的 RedirectToActionResult。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="6ef9b-128">Index （）動作包含下列一行程式碼：</span><span class="sxs-lookup"><span data-stu-id="6ef9b-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="6ef9b-129">View （）;</span><span class="sxs-lookup"><span data-stu-id="6ef9b-129">View();</span></span>

<span data-ttu-id="6ef9b-130">這行程式碼會傳回必須位於 web 伺服器上下列路徑的視圖：</span><span class="sxs-lookup"><span data-stu-id="6ef9b-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="6ef9b-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="6ef9b-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="6ef9b-132">視圖的路徑是從控制器的名稱和控制器動作的名稱推斷而來。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="6ef9b-133">如果您想要的話，可以明確瞭解此視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="6ef9b-134">下面這行程式碼會傳回名為 Fred 的視圖：</span><span class="sxs-lookup"><span data-stu-id="6ef9b-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="6ef9b-135">View （Fred）;</span><span class="sxs-lookup"><span data-stu-id="6ef9b-135">View( Fred );</span></span>

<span data-ttu-id="6ef9b-136">執行這行程式碼時，會從下列路徑傳回 view：</span><span class="sxs-lookup"><span data-stu-id="6ef9b-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="6ef9b-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="6ef9b-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6ef9b-138">如果您打算為 ASP.NET MVC 應用程式建立單元測試，則最好明確瞭解視圖名稱。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="6ef9b-139">如此一來，您就可以建立單元測試，以確認控制器動作是否傳回預期的視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>

## <a name="adding-content-to-a-view"></a><span data-ttu-id="6ef9b-140">將內容加入至視圖</span><span class="sxs-lookup"><span data-stu-id="6ef9b-140">Adding Content to a View</span></span>

<span data-ttu-id="6ef9b-141">「視圖」是一種可包含腳本的標準（X） HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="6ef9b-142">您可以使用腳本將動態內容新增至視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="6ef9b-143">例如，[清單 2] 中的視圖會顯示目前的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="6ef9b-144">**清單 2-\Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="6ef9b-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample2.aspx)]

<span data-ttu-id="6ef9b-145">請注意，[清單 2] 中的 HTML 頁面主體包含下列腳本：</span><span class="sxs-lookup"><span data-stu-id="6ef9b-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="6ef9b-146">&lt;% Response。 Write （DateTime. Now）;%&gt;</span><span class="sxs-lookup"><span data-stu-id="6ef9b-146">&lt;% Response.Write(DateTime.Now);%&gt;</span></span>

<span data-ttu-id="6ef9b-147">您可以使用腳本分隔符號 &lt;% 和%&gt; 來標記腳本的開頭和結尾。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="6ef9b-148">此腳本是以C#撰寫。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-148">This script is written in C#.</span></span> <span data-ttu-id="6ef9b-149">它會藉由呼叫回應. Write （）方法來顯示目前的日期和時間，以將內容轉譯至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="6ef9b-150">&lt;% 和%&gt; 的腳本分隔符號可以用來執行一個或多個語句。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="6ef9b-151">因為您呼叫回應，所以請經常寫入（），Microsoft 會提供一個快捷方式來呼叫回應. Write （）方法。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="6ef9b-152">[清單 3] 中的視圖使用分隔符號 &lt;% = 和%&gt; 做為呼叫 Response 的快捷方式。 Write （）。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="6ef9b-153">**清單 3-Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="6ef9b-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample3.aspx)]

<span data-ttu-id="6ef9b-154">您可以使用任何 .NET 語言，在視圖中產生動態內容。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="6ef9b-155">一般來說，您會使用 Visual Basic .NET 或C#來撰寫您的控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-155">Normally, you'll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="6ef9b-156">使用 HTML helper 產生視圖內容</span><span class="sxs-lookup"><span data-stu-id="6ef9b-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="6ef9b-157">為了讓您更輕鬆地將內容新增至視圖，您可以利用名為*HTML Helper*的東西。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="6ef9b-158">HTML Helper 通常是產生字串的方法。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="6ef9b-159">您可以使用 HTML helper 來產生標準 HTML 元素，例如文字方塊、連結、下拉式清單和清單方塊。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="6ef9b-160">例如，[清單 4] 中的視圖會利用三個 HTML 協助程式，也就是 Html.beginform （）、TextBox （）和 Password （） helper--以產生登入表單（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="6ef9b-161">**清單 4--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="6ef9b-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample4.aspx)]

<span data-ttu-id="6ef9b-162">[![[新增專案] 對話方塊](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6ef9b-162">[![The New Project dialog box](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)</span></span>

<span data-ttu-id="6ef9b-163">**圖 01**：標準登入表單（[按一下以查看完整大小的影像](asp-net-mvc-views-overview-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="6ef9b-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-cs/_static/image2.png))</span></span>

<span data-ttu-id="6ef9b-164">所有 HTML helper 方法都是在 view 的 Html 屬性上呼叫。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="6ef9b-165">例如，您可以藉由呼叫 Html. TextBox （）方法來呈現 TextBox。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="6ef9b-166">請注意，當您同時呼叫 Html. TextBox （）和 .Html （） helper 時，會使用腳本分隔符號 &lt;% = 和%&gt;。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="6ef9b-167">這些協助程式只會傳回字串。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-167">These helpers simply return a string.</span></span> <span data-ttu-id="6ef9b-168">您必須呼叫 Response. Write （），才能將字串轉譯為瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="6ef9b-169">使用 HTML Helper 方法是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="6ef9b-170">藉由減少您需要撰寫的 HTML 和腳本量，讓您的生活更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="6ef9b-171">[清單 5] 中的視圖會在不使用 HTML 協助程式的情況下，呈現與清單4中的視圖完全相同的表單。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="6ef9b-172">**清單 5--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="6ef9b-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample5.aspx)]

<span data-ttu-id="6ef9b-173">您也可以選擇建立自己的 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="6ef9b-174">例如，您可以建立 GridView （） helper 方法，自動在 HTML 資料表中顯示一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="6ef9b-175">我們會在**建立自訂 HTML**協助程式教學課程中探索此主題。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="6ef9b-176">使用視圖資料將資料傳遞至視圖</span><span class="sxs-lookup"><span data-stu-id="6ef9b-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="6ef9b-177">您可以使用 [視圖資料]，將控制器的資料傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="6ef9b-178">請將 view 資料視為您透過郵件傳送的套件。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="6ef9b-179">從控制器傳遞到視圖的所有資料都必須使用此封裝來傳送。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="6ef9b-180">例如，[清單 6] 中的控制器會新增訊息來查看資料。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="6ef9b-181">**清單 6-ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="6ef9b-181">**Listing 6 - ProductController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample6.cs)]

<span data-ttu-id="6ef9b-182">控制器 ViewData 屬性代表名稱和值配對的集合。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="6ef9b-183">在 [清單 6] 中，Index （）方法會將專案新增至名為 message 的 view 資料集合，其值 Hello World！。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="6ef9b-184">當 Index （）方法傳回 view 時，會自動將視圖資料傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="6ef9b-185">[清單 7] 中的視圖會從 view 資料中抓取訊息，並將訊息轉譯至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="6ef9b-186">**清單 7--\Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="6ef9b-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample7.aspx)]

<span data-ttu-id="6ef9b-187">請注意，在轉譯訊息時，此視圖會利用 Html 的編碼方式（） HTML Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="6ef9b-188">Html. 編碼（） HTML Helper 會將特殊字元（例如 &lt; 和 &gt;）編碼成可在網頁中顯示的安全字元。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="6ef9b-189">每當您呈現使用者提交至網站的內容時，您應該將內容編碼以防止 JavaScript 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="6ef9b-190">（因為我們會在 ProductController 中自行建立訊息，所以我們不需要對訊息進行編碼。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-190">(Because we created the message ourselves in the ProductController, we don't really need to encode the message.</span></span> <span data-ttu-id="6ef9b-191">不過，在視圖中顯示從 view 資料抓取的內容時，一律會呼叫 Html. 編碼（）方法是很好的習慣。）</span><span class="sxs-lookup"><span data-stu-id="6ef9b-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="6ef9b-192">在 [清單 7] 中，我們利用了視圖資料，將簡單的字串訊息從控制器傳遞至視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="6ef9b-193">您也可以使用 [視圖資料]，將其他類型的資料（例如資料庫記錄的集合）從控制器傳遞至視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="6ef9b-194">例如，如果您想要在視圖中顯示 Products 資料庫資料表的內容，則您會將資料庫記錄的集合傳遞至 view data。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="6ef9b-195">您也可以選擇將強型別視圖資料從控制器傳遞到 view。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="6ef9b-196">我們會在瞭解強型別**視圖資料和 Views**教學課程中探索此主題。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="6ef9b-197">總結</span><span class="sxs-lookup"><span data-stu-id="6ef9b-197">Summary</span></span>

<span data-ttu-id="6ef9b-198">本教學課程提供 ASP.NET MVC 視圖、視圖資料和 HTML 協助程式的簡介。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="6ef9b-199">在第一節中，您已瞭解如何將新的視圖加入至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="6ef9b-200">您已瞭解，您必須將 view 新增至正確的資料夾，才能從特定的控制器呼叫它。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="6ef9b-201">接下來，我們討論過 HTML 協助程式的主題。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="6ef9b-202">您已瞭解 HTML 協助程式如何讓您輕鬆地產生標準 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="6ef9b-203">最後，您已瞭解如何利用視圖資料，將控制器中的資料傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="6ef9b-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6ef9b-204">下一個</span><span class="sxs-lookup"><span data-stu-id="6ef9b-204">Next</span></span>](creating-custom-html-helpers-cs.md)
