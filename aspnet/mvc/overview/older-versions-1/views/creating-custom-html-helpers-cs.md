---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 建立自訂 HTML helperC#（） |Microsoft Docs
author: microsoft
description: 本教學課程的目的是要示範如何建立可在 MVC 視圖內使用的自訂 HTML 協助程式。 利用 HTML Helper 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594553"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="77b0e-104">建立自訂的 HTML 協助程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="77b0e-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="77b0e-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="77b0e-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="77b0e-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="77b0e-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="77b0e-107">本教學課程的目的是要示範如何建立可在 MVC 視圖內使用的自訂 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="77b0e-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="77b0e-108">藉由利用 HTML 協助程式，您可以減少在建立標準 HTML 網頁時，必須執行的 HTML 標籤的單調乏味輸入量。</span><span class="sxs-lookup"><span data-stu-id="77b0e-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="77b0e-109">本教學課程的目的是要示範如何建立可在 MVC 視圖內使用的自訂 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="77b0e-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="77b0e-110">藉由利用 HTML 協助程式，您可以減少在建立標準 HTML 網頁時，必須執行的 HTML 標籤的單調乏味輸入量。</span><span class="sxs-lookup"><span data-stu-id="77b0e-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="77b0e-111">在本教學課程的第一個部分中，我將說明 ASP.NET MVC 架構中包含的一些現有 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="77b0e-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="77b0e-112">接下來，我將說明建立自訂 HTML 協助程式的兩種方法：我將說明如何建立靜態方法，並藉由建立擴充方法，來建立自訂 HTML helper。</span><span class="sxs-lookup"><span data-stu-id="77b0e-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="77b0e-113">瞭解 HTML 協助程式</span><span class="sxs-lookup"><span data-stu-id="77b0e-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="77b0e-114">HTML Helper 只是傳回字串的方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="77b0e-115">字串可以代表您想要的任何類型內容。</span><span class="sxs-lookup"><span data-stu-id="77b0e-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="77b0e-116">例如，您可以使用 HTML helper 來呈現標準 HTML 標籤，例如 HTML `<input>` 和 `<img>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="77b0e-117">您也可以使用 HTML helper 來呈現更複雜的內容，例如索引標籤區域或資料庫資料的 HTML 表格。</span><span class="sxs-lookup"><span data-stu-id="77b0e-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="77b0e-118">ASP.NET MVC 架構包含下列一組標準 HTML 協助程式（這不是完整的清單）：</span><span class="sxs-lookup"><span data-stu-id="77b0e-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="77b0e-119">.Html （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-119">Html.ActionLink()</span></span>
- <span data-ttu-id="77b0e-120">Html.beginform （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-120">Html.BeginForm()</span></span>
- <span data-ttu-id="77b0e-121">Html. CheckBox （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-121">Html.CheckBox()</span></span>
- <span data-ttu-id="77b0e-122">DropDownList （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-122">Html.DropDownList()</span></span>
- <span data-ttu-id="77b0e-123">EndForm （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-123">Html.EndForm()</span></span>
- <span data-ttu-id="77b0e-124">Html. Hidden （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-124">Html.Hidden()</span></span>
- <span data-ttu-id="77b0e-125">Html. ListBox （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-125">Html.ListBox()</span></span>
- <span data-ttu-id="77b0e-126">Html. Password （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-126">Html.Password()</span></span>
- <span data-ttu-id="77b0e-127">Html （選項按鈕）（）</span><span class="sxs-lookup"><span data-stu-id="77b0e-127">Html.RadioButton()</span></span>
- <span data-ttu-id="77b0e-128">Html. TextArea （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-128">Html.TextArea()</span></span>
- <span data-ttu-id="77b0e-129">Html. TextBox （）</span><span class="sxs-lookup"><span data-stu-id="77b0e-129">Html.TextBox()</span></span>

<span data-ttu-id="77b0e-130">例如，請考慮 [清單 1] 中的表單。</span><span class="sxs-lookup"><span data-stu-id="77b0e-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="77b0e-131">這種表單是透過兩個標準 HTML helper 的協助來呈現的（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="77b0e-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="77b0e-132">這個表單會使用 `Html.BeginForm()` 和 `Html.TextBox()` Helper 方法來轉譯簡單的 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="77b0e-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="77b0e-133">[使用 HTML 協助程式轉譯的 ![頁面](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="77b0e-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="77b0e-134">**圖 01**：以 HTML 協助程式轉譯的頁面（[按一下以觀看完整大小的影像](creating-custom-html-helpers-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="77b0e-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="77b0e-135">**清單1– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="77b0e-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="77b0e-136">Html.beginform （） Helper 方法是用來建立開頭和結尾的 HTML `<form>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="77b0e-137">請注意，會在 using 語句中呼叫 `Html.BeginForm()` 方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="77b0e-138">Using 語句可確保在 using 區塊結尾處關閉 `<form>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="77b0e-139">如果您想要，而不是建立 using 區塊，您可以呼叫 EndForm （） Helper 方法來關閉 `<form>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="77b0e-140">您可以使用任何方法來建立開頭和結尾的 `<form>` 標記，這對您而言是最直覺的。</span><span class="sxs-lookup"><span data-stu-id="77b0e-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="77b0e-141">`Html.TextBox()` 的 Helper 方法會在清單1中用來呈現 HTML `<input>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="77b0e-142">如果您在瀏覽器中選取 [view source]，則會在 [清單 2] 中看到 HTML 原始檔。</span><span class="sxs-lookup"><span data-stu-id="77b0e-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="77b0e-143">請注意，來源包含標準 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="77b0e-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77b0e-144">請注意，`Html.TextBox()`HTML 協助程式是以 `<%= %>` 標記而非 `<% %>` 標記來呈現。</span><span class="sxs-lookup"><span data-stu-id="77b0e-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="77b0e-145">如果您未包含等號，則不會將任何內容轉譯至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="77b0e-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="77b0e-146">ASP.NET MVC 架構包含一小部分的協助程式。</span><span class="sxs-lookup"><span data-stu-id="77b0e-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="77b0e-147">最有可能的情況是，您必須使用自訂 HTML 協助程式來擴充 MVC 架構。</span><span class="sxs-lookup"><span data-stu-id="77b0e-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="77b0e-148">在本教學課程的其餘部分，您將瞭解建立自訂 HTML 協助程式的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="77b0e-149">**清單2– `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="77b0e-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="77b0e-150">使用靜態方法建立 HTML 協助程式</span><span class="sxs-lookup"><span data-stu-id="77b0e-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="77b0e-151">建立新 HTML Helper 的最簡單方式，就是建立可傳回字串的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="77b0e-152">例如，假設您決定要建立新的 HTML Helper，以轉譯 HTML `<label>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="77b0e-153">您可以使用 [清單 2] 中的類別來呈現 `<label>`。</span><span class="sxs-lookup"><span data-stu-id="77b0e-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="77b0e-154">**清單2– `Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="77b0e-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="77b0e-155">[清單 2] 中的類別沒有特別的內容。</span><span class="sxs-lookup"><span data-stu-id="77b0e-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="77b0e-156">`Label()` 方法只會傳回字串。</span><span class="sxs-lookup"><span data-stu-id="77b0e-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="77b0e-157">[清單 3] 中修改過的索引視圖會使用 `LabelHelper` 來呈現 HTML `<label>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="77b0e-158">請注意，此視圖包含匯入 `Application1.Helpers` 命名空間的 `<%@ imports %>` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="77b0e-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="77b0e-159">**清單2– `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="77b0e-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="77b0e-160">建立具有擴充方法的 HTML 協助程式</span><span class="sxs-lookup"><span data-stu-id="77b0e-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="77b0e-161">如果您想要建立 HTML 協助程式，其作用就像 ASP.NET MVC 架構中包含的標準 HTML helper，那麼您必須建立擴充方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="77b0e-162">擴充方法可讓您將新的方法加入至現有的類別。</span><span class="sxs-lookup"><span data-stu-id="77b0e-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="77b0e-163">建立 HTML Helper 方法時，您會將新的方法加入至由視圖的 Html 屬性所表示的 HtmlHelper 類別。</span><span class="sxs-lookup"><span data-stu-id="77b0e-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="77b0e-164">[清單 3] 中的類別會將擴充方法新增至名為 `Label()`的 `HtmlHelper` 類別。</span><span class="sxs-lookup"><span data-stu-id="77b0e-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="77b0e-165">關於此類別，您應該要注意幾件事。</span><span class="sxs-lookup"><span data-stu-id="77b0e-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="77b0e-166">首先，請注意類別是靜態類別。</span><span class="sxs-lookup"><span data-stu-id="77b0e-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="77b0e-167">您必須定義具有靜態類別的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="77b0e-168">第二，請注意，`Label()` 方法的第一個參數前面會加上關鍵字 `this`。</span><span class="sxs-lookup"><span data-stu-id="77b0e-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="77b0e-169">擴充方法的第一個參數表示擴充方法擴充的類別。</span><span class="sxs-lookup"><span data-stu-id="77b0e-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="77b0e-170">**清單3– `Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="77b0e-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="77b0e-171">在您建立擴充方法並成功建立應用程式之後，擴充方法會出現在 Visual Studio Intellisense 中，就像類別的所有其他方法一樣（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="77b0e-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="77b0e-172">唯一的差別在於擴充方法會在其旁邊顯示特殊符號（向下箭號的圖示）。</span><span class="sxs-lookup"><span data-stu-id="77b0e-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="77b0e-173">[使用 Html. Label （）擴充方法 ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="77b0e-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="77b0e-174">**圖 02**：使用 Html. Label （）擴充方法（[按一下以查看完整大小的影像](creating-custom-html-helpers-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="77b0e-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="77b0e-175">[清單 4] 中修改過的索引視圖會使用 Html. Label （）擴充方法來呈現其所有的 `<label>` 標記。</span><span class="sxs-lookup"><span data-stu-id="77b0e-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="77b0e-176">**清單4– `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="77b0e-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="77b0e-177">總結</span><span class="sxs-lookup"><span data-stu-id="77b0e-177">Summary</span></span>

<span data-ttu-id="77b0e-178">在本教學課程中，您已瞭解建立自訂 HTML 協助程式的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="77b0e-179">首先，您已瞭解如何建立一個會傳回字串的靜態方法，以建立自訂的 `Label()` HTML Helper。</span><span class="sxs-lookup"><span data-stu-id="77b0e-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="77b0e-180">接下來，您已瞭解如何在 `HtmlHelper` 類別上建立擴充方法，以建立自訂的 `Label()` HTML Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="77b0e-181">在本教學課程中，我將重點放在建立非常簡單的 HTML Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="77b0e-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="77b0e-182">請注意，HTML Helper 可以像您想要的一樣複雜。</span><span class="sxs-lookup"><span data-stu-id="77b0e-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="77b0e-183">您可以建立 HTML 協助程式來呈現豐富的內容，例如樹狀檢視、功能表或資料庫資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="77b0e-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77b0e-184">[上一頁](asp-net-mvc-views-overview-cs.md)
> [下一頁](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="77b0e-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
