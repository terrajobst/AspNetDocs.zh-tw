---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 建立自訂的 HTML 協助程式 (C#) |Microsoft Docs
author: microsoft
description: 本教學課程的目標在於示範如何建立自訂的 HTML 協助程式，您可以使用 MVC 檢視中。 利用 HTML 協助程式...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 23741d7974713102e6ccb46ced5d62ec202505e8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400850"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="77927-104">建立自訂的 HTML 協助程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="77927-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="77927-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="77927-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="77927-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="77927-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="77927-107">本教學課程的目標在於示範如何建立自訂的 HTML 協助程式，您可以使用 MVC 檢視中。</span><span class="sxs-lookup"><span data-stu-id="77927-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="77927-108">利用 HTML 協助程式，您可以減少您必須執行才能建立標準的 HTML 網頁的 HTML 標記的 tedious 打字的量。</span><span class="sxs-lookup"><span data-stu-id="77927-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="77927-109">本教學課程的目標在於示範如何建立自訂的 HTML 協助程式，您可以使用 MVC 檢視中。</span><span class="sxs-lookup"><span data-stu-id="77927-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="77927-110">利用 HTML 協助程式，您可以減少您必須執行才能建立標準的 HTML 網頁的 HTML 標記的 tedious 打字的量。</span><span class="sxs-lookup"><span data-stu-id="77927-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="77927-111">在本教學課程的第一個部分中，我會說明一些現有 ASP.NET MVC framework 隨附的 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="77927-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="77927-112">接下來，我先說明兩種建立自訂的 HTML 協助程式方法：我會說明如何建立自訂的 HTML 協助程式，藉由建立靜態方法，並藉由建立擴充方法。</span><span class="sxs-lookup"><span data-stu-id="77927-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="77927-113">了解 HTML 協助程式</span><span class="sxs-lookup"><span data-stu-id="77927-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="77927-114">HTML 協助程式是只會傳回字串的方法。</span><span class="sxs-lookup"><span data-stu-id="77927-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="77927-115">字串可以代表任一種您想要的內容。</span><span class="sxs-lookup"><span data-stu-id="77927-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="77927-116">比方說，您可以使用 HTML Helper 來呈現標準的 HTML 標記，例如 HTML`<input>`和`<img>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="77927-117">您也可以使用 HTML Helper 來呈現更複雜的內容，例如索引標籤帶或資料庫資料的 HTML 資料表。</span><span class="sxs-lookup"><span data-stu-id="77927-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="77927-118">ASP.NET MVC 架構包括下列設定中 （這不是完整的清單） 的標準 HTML 協助程式：</span><span class="sxs-lookup"><span data-stu-id="77927-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="77927-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="77927-119">Html.ActionLink()</span></span>
- <span data-ttu-id="77927-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="77927-120">Html.BeginForm()</span></span>
- <span data-ttu-id="77927-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="77927-121">Html.CheckBox()</span></span>
- <span data-ttu-id="77927-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="77927-122">Html.DropDownList()</span></span>
- <span data-ttu-id="77927-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="77927-123">Html.EndForm()</span></span>
- <span data-ttu-id="77927-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="77927-124">Html.Hidden()</span></span>
- <span data-ttu-id="77927-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="77927-125">Html.ListBox()</span></span>
- <span data-ttu-id="77927-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="77927-126">Html.Password()</span></span>
- <span data-ttu-id="77927-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="77927-127">Html.RadioButton()</span></span>
- <span data-ttu-id="77927-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="77927-128">Html.TextArea()</span></span>
- <span data-ttu-id="77927-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="77927-129">Html.TextBox()</span></span>

<span data-ttu-id="77927-130">例如，請考慮在列表 1 中的表單。</span><span class="sxs-lookup"><span data-stu-id="77927-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="77927-131">此表單會轉譯兩個標準的 HTML 協助程式 （請參閱 圖 1） 的協助。</span><span class="sxs-lookup"><span data-stu-id="77927-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="77927-132">這個表單用`Html.BeginForm()`和`Html.TextBox()`轉譯簡單的 HTML 表單的 Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="77927-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>


[![P<span data-ttu-id="77927-133">age 呈現與 HTML 協助程式]</span><span class="sxs-lookup"><span data-stu-id="77927-133">age rendered with HTML Helpers]</span></span>(creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

<span data-ttu-id="77927-134">**圖 01**:使用 HTML Helper 呈現網頁 ([按一下以檢視完整大小的影像](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="77927-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>


**<span data-ttu-id="77927-135">列表 1 –</span><span class="sxs-lookup"><span data-stu-id="77927-135">Listing 1 –</span></span> `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="77927-136">Html.BeginForm() 協助程式方法用來建立的開頭和結尾的 HTML`<form>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="77927-137">請注意，`Html.BeginForm()`方法稱為在 using 陳述式。</span><span class="sxs-lookup"><span data-stu-id="77927-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="77927-138">使用陳述式可以確保`<form>`標記取得關閉使用結尾區塊。</span><span class="sxs-lookup"><span data-stu-id="77927-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="77927-139">如果您偏好，而不是建立 using 區塊中，您可以呼叫 Html.EndForm() 協助程式方法，以關閉`<form>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="77927-140">使用任何方法，來建立開啟和關閉`<form>`似乎最直覺的標記。</span><span class="sxs-lookup"><span data-stu-id="77927-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="77927-141">`Html.TextBox()` Helper 方法會在 列表 1 中用來呈現 HTML`<input>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="77927-142">如果您選取檢視原始檔瀏覽器中您會看到列表 2 中的 HTML 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="77927-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="77927-143">請注意來源包含標準的 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="77927-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77927-144">請注意， `Html.TextBox()`HTML 協助程式以呈現`<%= %>`而不是標記`<% %>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="77927-145">如果您未包含等號，然後執行任何動作取得呈現在瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="77927-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="77927-146">ASP.NET MVC 架構會包含較少的協助程式。</span><span class="sxs-lookup"><span data-stu-id="77927-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="77927-147">最有可能，您必須擴充 MVC 架構使用自訂 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="77927-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="77927-148">在本教學課程的其餘部分，您將了解建立自訂的 HTML 協助程式的兩個方法。</span><span class="sxs-lookup"><span data-stu-id="77927-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

**<span data-ttu-id="77927-149">列表 2 –</span><span class="sxs-lookup"><span data-stu-id="77927-149">Listing 2 –</span></span> `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="77927-150">建立 HTML 協助程式搭配靜態方法</span><span class="sxs-lookup"><span data-stu-id="77927-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="77927-151">若要建立新的 HTML 協助程式的最簡單方式是建立靜態方法會傳回字串。</span><span class="sxs-lookup"><span data-stu-id="77927-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="77927-152">想像一下，比方說，您決定建立新的 HTML Helper 呈現 HTML`<label>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="77927-153">您也可以在 列表 2 中使用類別來呈現`<label>`。</span><span class="sxs-lookup"><span data-stu-id="77927-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

**<span data-ttu-id="77927-154">列表 2 –</span><span class="sxs-lookup"><span data-stu-id="77927-154">Listing 2 –</span></span> `Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="77927-155">沒有特別關於列表 2 中的類別。</span><span class="sxs-lookup"><span data-stu-id="77927-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="77927-156">`Label()`方法只會傳回字串。</span><span class="sxs-lookup"><span data-stu-id="77927-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="77927-157">在 列表 3 中修改過的 索引 檢視會使用`LabelHelper`呈現 HTML`<label>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="77927-158">請注意，此檢視包含`<%@ imports %>`匯入的指示詞`Application1.Helpers`命名空間。</span><span class="sxs-lookup"><span data-stu-id="77927-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

**<span data-ttu-id="77927-159">列表 2 –</span><span class="sxs-lookup"><span data-stu-id="77927-159">Listing 2 –</span></span> `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="77927-160">使用擴充方法建立 HTML 協助程式</span><span class="sxs-lookup"><span data-stu-id="77927-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="77927-161">如果您想要建立只是工作的 HTML 協助程式，例如標準包含 ASP.NET MVC 架構中，則您需要建立擴充方法的 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="77927-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="77927-162">擴充方法可讓您將新方法新增至現有的類別。</span><span class="sxs-lookup"><span data-stu-id="77927-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="77927-163">在建立時的 HTML Helper 方法，您會將新方法加入至檢視的 Html 屬性所表示的 HtmlHelper 類別中。</span><span class="sxs-lookup"><span data-stu-id="77927-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="77927-164">列表 3 中的類別加入至擴充方法`HtmlHelper`名為類別`Label()`。</span><span class="sxs-lookup"><span data-stu-id="77927-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="77927-165">有幾個您應該注意到關於此類別的項目。</span><span class="sxs-lookup"><span data-stu-id="77927-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="77927-166">首先，請注意，類別的靜態類別。</span><span class="sxs-lookup"><span data-stu-id="77927-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="77927-167">您必須定義靜態類別的延伸方法。</span><span class="sxs-lookup"><span data-stu-id="77927-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="77927-168">其次，請注意，第一個參數`Label()`方法的前面是關鍵字`this`。</span><span class="sxs-lookup"><span data-stu-id="77927-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="77927-169">擴充方法的第一個參數指出的擴充方法要擴充的類別。</span><span class="sxs-lookup"><span data-stu-id="77927-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

**<span data-ttu-id="77927-170">列表 3 –</span><span class="sxs-lookup"><span data-stu-id="77927-170">Listing 3 –</span></span> `Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="77927-171">擴充方法建立擴充方法，並成功建置您的應用程式之後，會出現在 Visual Studio Intellisense，如同所有其他方法的類別 （請參閱 圖 2）。</span><span class="sxs-lookup"><span data-stu-id="77927-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="77927-172">唯一的差別是該方法會出現特殊符號旁邊 （向下箭號圖示） 的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="77927-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


[![U<span data-ttu-id="77927-173">發揚光大 Html.Label() 擴充方法]</span><span class="sxs-lookup"><span data-stu-id="77927-173">sing the Html.Label() extension method]</span></span>(creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

<span data-ttu-id="77927-174">**圖 02**:使用 Html.Label() 擴充方法 ([按一下以檢視完整大小的影像](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="77927-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>


<span data-ttu-id="77927-175">在 列表 4 中已修改的 索引 檢視使用 Html.Label(); 擴充方法來呈現所有其`<label>`標記。</span><span class="sxs-lookup"><span data-stu-id="77927-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

**<span data-ttu-id="77927-176">列表 4 –</span><span class="sxs-lookup"><span data-stu-id="77927-176">Listing 4 –</span></span> `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="77927-177">總結</span><span class="sxs-lookup"><span data-stu-id="77927-177">Summary</span></span>

<span data-ttu-id="77927-178">在本教學課程中，您已了解建立自訂的 HTML 協助程式的兩個方法。</span><span class="sxs-lookup"><span data-stu-id="77927-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="77927-179">首先，您已了解如何建立自訂`Label()`藉由建立靜態方法的 HTML 協助程式傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="77927-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="77927-180">接下來，您已了解如何建立自訂`Label()`上建立擴充方法的 HTML Helper 方法`HtmlHelper`類別。</span><span class="sxs-lookup"><span data-stu-id="77927-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="77927-181">在本教學課程中，我會著重於建置非常簡單的 HTML Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="77927-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="77927-182">請注意，HTML 協助程式可以是任意的複雜。</span><span class="sxs-lookup"><span data-stu-id="77927-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="77927-183">您可以建置 HTML 協助程式呈現豐富的內容，例如樹狀檢視、 功能表或資料庫資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="77927-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77927-184">[上一頁](asp-net-mvc-views-overview-cs.md)
> [下一頁](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="77927-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
