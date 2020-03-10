---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用主版頁面和部分重新使用 UI |Microsoft Docs
author: microsoft
description: 步驟7探討我們可以在我們的視圖範本內套用「幹原則」的方式，使用部分視圖範本和主版頁面來消除程式碼重複。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580329"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="574e3-103">重複使用使用主版頁面和部分頁面的 UI</span><span class="sxs-lookup"><span data-stu-id="574e3-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="574e3-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="574e3-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="574e3-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="574e3-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="574e3-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟7，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="574e3-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="574e3-107">步驟7探討我們可以在我們的視圖範本內套用「幹原則」的方式，使用部分視圖範本和主版頁面來消除程式碼重複。</span><span class="sxs-lookup"><span data-stu-id="574e3-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="574e3-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="574e3-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="574e3-109">NerdDinner 步驟7：部分和主版頁面</span><span class="sxs-lookup"><span data-stu-id="574e3-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="574e3-110">MVC 所 ASP.NET 的其中一個設計觀念是「不要自行重複」原則（通常稱為「幹」）。</span><span class="sxs-lookup"><span data-stu-id="574e3-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="574e3-111">試設計有助於消除重複的程式碼和邏輯，這最終可讓應用程式更快速地建立及維護。</span><span class="sxs-lookup"><span data-stu-id="574e3-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="574e3-112">我們已經看過在數個 NerdDinner 案例中套用的試原則。</span><span class="sxs-lookup"><span data-stu-id="574e3-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="574e3-113">一些範例：我們的驗證邏輯會在我們的模型層內執行，讓它在控制器的編輯和建立案例中強制執行;我們會在 [編輯]、[詳細資料] 和 [刪除] 動作方法中重複使用 "NotFound" view 範本;我們在我們的視圖範本中使用慣例命名模式，這樣就不需要在我們呼叫 View （） helper 方法時明確指定名稱。而且我們會針對 [編輯] 和 [建立] 動作案例重複使用 DinnerFormViewModel 類別。</span><span class="sxs-lookup"><span data-stu-id="574e3-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="574e3-114">現在讓我們來看一下，我們可以在我們的視圖範本內套用「幹原則」，以避免程式碼重複。</span><span class="sxs-lookup"><span data-stu-id="574e3-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="574e3-115">重新造訪我們的編輯和建立視圖範本</span><span class="sxs-lookup"><span data-stu-id="574e3-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="574e3-116">目前我們使用兩個不同的視圖範本– "Edit .aspx" 和 "Create .aspx" –以顯示晚餐表單 UI。</span><span class="sxs-lookup"><span data-stu-id="574e3-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="574e3-117">它們的快速視覺化比較會反白顯示其相似之處。</span><span class="sxs-lookup"><span data-stu-id="574e3-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="574e3-118">以下是建立表單的樣子：</span><span class="sxs-lookup"><span data-stu-id="574e3-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="574e3-119">我們的「編輯」表單看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="574e3-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="574e3-120">沒有太多差異了嗎？</span><span class="sxs-lookup"><span data-stu-id="574e3-120">Not much of a difference is there?</span></span> <span data-ttu-id="574e3-121">除了標題和標題文字之外，表單版面配置和輸入控制項都相同。</span><span class="sxs-lookup"><span data-stu-id="574e3-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="574e3-122">如果我們開啟「編輯 .aspx」和「建立 .aspx」視圖範本，我們會發現它們包含相同的表單版面配置和輸入控制項程式碼。</span><span class="sxs-lookup"><span data-stu-id="574e3-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="574e3-123">這種重複方式表示，每當我們引進或變更新的晚餐屬性時，都必須進行變更兩次-這不是好的。</span><span class="sxs-lookup"><span data-stu-id="574e3-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="574e3-124">使用部分視圖範本</span><span class="sxs-lookup"><span data-stu-id="574e3-124">Using Partial View Templates</span></span>

<span data-ttu-id="574e3-125">ASP.NET MVC 支援定義「部分視圖」範本的功能，可用來封裝頁面子部分的視圖呈現邏輯。</span><span class="sxs-lookup"><span data-stu-id="574e3-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="574e3-126">「部分」提供一個實用的方式來定義 view 轉譯邏輯一次，然後在應用程式的多個位置重複使用它。</span><span class="sxs-lookup"><span data-stu-id="574e3-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="574e3-127">為了協助「清理」我們的編輯 .aspx，並建立 .aspx view 範本重複，我們可以建立名為 "DinnerForm" 的部分視圖範本，以封裝兩者通用的表單配置和輸入元素。</span><span class="sxs-lookup"><span data-stu-id="574e3-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="574e3-128">若要這麼做，請以滑鼠右鍵按一下/Views/Dinners 目錄，然後選擇 [新增&gt;View] 功能表命令：</span><span class="sxs-lookup"><span data-stu-id="574e3-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="574e3-129">這會顯示 [新增視圖] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="574e3-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="574e3-130">我們會將新的視圖命名為 [DinnerForm]，選取對話方塊中的 [建立部分視圖] 核取方塊，並指出我們會將 DinnerFormViewModel 類別傳遞給它：</span><span class="sxs-lookup"><span data-stu-id="574e3-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="574e3-131">當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "DinnerForm" 視圖範本。</span><span class="sxs-lookup"><span data-stu-id="574e3-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="574e3-132">然後，我們可以將重複的表單版面配置/輸入控制項程式碼從編輯 .aspx/Create .aspx view 範本複製/貼上到新的 "DinnerForm" 部分視圖範本：</span><span class="sxs-lookup"><span data-stu-id="574e3-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="574e3-133">然後，我們可以更新編輯和建立視圖範本來呼叫 DinnerForm 部分範本，並消除表單重複。</span><span class="sxs-lookup"><span data-stu-id="574e3-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="574e3-134">我們可以在我們的 view 範本內呼叫 RenderPartial （"DinnerForm"）來完成這項操作：</span><span class="sxs-lookup"><span data-stu-id="574e3-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="574e3-135">建立 .aspx</span><span class="sxs-lookup"><span data-stu-id="574e3-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="574e3-136">編輯 .aspx</span><span class="sxs-lookup"><span data-stu-id="574e3-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="574e3-137">呼叫 RenderPartial （例如： ~ Views/Dinners/DinnerForm）時，您可以明確限定所需部分範本的路徑。</span><span class="sxs-lookup"><span data-stu-id="574e3-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="574e3-138">不過，在上述程式碼中，我們會利用 ASP.NET MVC 中以慣例為基礎的命名模式，並只將 "DinnerForm" 指定為要轉譯之部分的名稱。</span><span class="sxs-lookup"><span data-stu-id="574e3-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="574e3-139">當我們執行此 ASP.NET 時，MVC 會先在以慣例為基礎的 views 目錄中尋找（針對 DinnersController，這會是/Views/Dinners）。</span><span class="sxs-lookup"><span data-stu-id="574e3-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="574e3-140">如果找不到部分範本，則會在/Views/Shared 目錄中尋找它。</span><span class="sxs-lookup"><span data-stu-id="574e3-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="574e3-141">以部分視圖的名稱呼叫 RenderPartial （）時，ASP.NET MVC 會傳遞給部分視圖，這是呼叫視圖範本所使用的相同模型和 ViewData 字典物件。</span><span class="sxs-lookup"><span data-stu-id="574e3-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="574e3-142">或者，還有 RenderPartial （）的多載版本，可讓您傳遞替代模型物件和/或 ViewData 字典，供部分視圖使用。</span><span class="sxs-lookup"><span data-stu-id="574e3-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="574e3-143">這適用于您只想要傳遞完整模型/ViewModel 子集的案例。</span><span class="sxs-lookup"><span data-stu-id="574e3-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="574e3-144">**側邊主題：為什麼 &lt;%%&gt;，而不是 &lt;% =%&gt;？**</span><span class="sxs-lookup"><span data-stu-id="574e3-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="574e3-145">在上述程式碼中，您可能已注意到的其中一項很微妙，就是在呼叫 RenderPartial （）時，使用 &lt;%%&gt; 區塊，而不是 &lt;% =%&gt; 區塊。</span><span class="sxs-lookup"><span data-stu-id="574e3-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="574e3-146">&lt;% =%&gt; ASP.NET 中的區塊表示開發人員想要轉譯指定的值（例如： &lt;% = "Hello"%&gt; 會轉譯 "Hello"）。</span><span class="sxs-lookup"><span data-stu-id="574e3-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="574e3-147">&lt;%%&gt; 區塊，而不是表示開發人員想要執行程式碼，而且它們內的任何轉譯輸出都必須明確完成（例如： &lt;% Response。 Write （"Hello"）%&gt;。</span><span class="sxs-lookup"><span data-stu-id="574e3-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="574e3-148">我們使用 &lt;%%&gt; 區塊的原因是上述的 RenderPartial 程式碼，因為 RenderPartial （）方法不會傳回字串，而是會直接將內容輸出至呼叫視圖範本的輸出資料流程。</span><span class="sxs-lookup"><span data-stu-id="574e3-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="574e3-149">這是基於效能效率的理由，這樣做可避免建立（可能非常大）暫存字串物件的需求。</span><span class="sxs-lookup"><span data-stu-id="574e3-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="574e3-150">這會減少記憶體使用量，並改善整體應用程式輸送量。</span><span class="sxs-lookup"><span data-stu-id="574e3-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="574e3-151">使用 RenderPartial （）時，有一項常見的錯誤是忘了在呼叫結尾處加上分號（當它在 &lt;%%&gt; 區塊內）。</span><span class="sxs-lookup"><span data-stu-id="574e3-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="574e3-152">例如，此程式碼會造成編譯器錯誤： &lt;% RenderPartial （"DinnerForm"）%&gt; 您必須寫入： &lt;% Html. RenderPartial （"DinnerForm"）;%&gt; 這是因為 &lt;%%&gt; 區塊是獨立的程式碼語句，而且使用C#程式碼語句時必須以分號結束。</span><span class="sxs-lookup"><span data-stu-id="574e3-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="574e3-153">使用部分視圖範本來澄清程式碼</span><span class="sxs-lookup"><span data-stu-id="574e3-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="574e3-154">我們建立了 "DinnerForm" 部分視圖範本，以避免在多個位置複製 view 轉譯邏輯。</span><span class="sxs-lookup"><span data-stu-id="574e3-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="574e3-155">這是建立部分視圖範本最常見的原因。</span><span class="sxs-lookup"><span data-stu-id="574e3-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="574e3-156">有時候，建立部分視圖還是很合理，即使只是在單一位置呼叫也一樣。</span><span class="sxs-lookup"><span data-stu-id="574e3-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="574e3-157">當其 view 轉譯邏輯已解壓縮並分割成一個或多個名稱完整的部分範本時，非常複雜的視圖範本通常會變得更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="574e3-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="574e3-158">例如，請考慮下列網站中的程式碼片段：我們的專案中的主版檔案（我們很快就會看到）。</span><span class="sxs-lookup"><span data-stu-id="574e3-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="574e3-159">程式碼相當簡單明瞭，部分是因為在畫面右上方顯示登入/登出連結的邏輯會封裝在 "Logonusercontrol.ascx" 部分中：</span><span class="sxs-lookup"><span data-stu-id="574e3-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="574e3-160">當您發現自己不想要瞭解在視圖範本內的 html/程式碼標記時，請考慮是否要將其中一些元件解壓縮和重構為名稱完整的部分視圖，這樣會變得更清楚。</span><span class="sxs-lookup"><span data-stu-id="574e3-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="574e3-161">主版頁面</span><span class="sxs-lookup"><span data-stu-id="574e3-161">Master Pages</span></span>

<span data-ttu-id="574e3-162">除了支援部分視圖以外，ASP.NET MVC 也支援建立「主版頁面」範本的功能，可用來定義網站的一般版面配置和最上層 html。</span><span class="sxs-lookup"><span data-stu-id="574e3-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="574e3-163">接著可以將內容預留位置控制項新增至主版頁面，以識別可由 views 覆寫或「填入」的可取代區域。</span><span class="sxs-lookup"><span data-stu-id="574e3-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="574e3-164">這提供了一種非常有效率的方法，讓您在應用程式中套用通用版面配置。</span><span class="sxs-lookup"><span data-stu-id="574e3-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="574e3-165">根據預設，新的 ASP.NET MVC 專案會自動加入主版頁面範本。</span><span class="sxs-lookup"><span data-stu-id="574e3-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="574e3-166">此主版頁面會命名為 "\Views\Shared\"，並存在於下列資料夾中：</span><span class="sxs-lookup"><span data-stu-id="574e3-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="574e3-167">預設的網站. master 檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="574e3-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="574e3-168">它會定義網站的外部 html，以及頂端導覽的功能表。</span><span class="sxs-lookup"><span data-stu-id="574e3-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="574e3-169">其中包含兩個可取代的內容預留位置控制項–一個用於標題，另一個則用於頁面的主要內容取代：</span><span class="sxs-lookup"><span data-stu-id="574e3-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="574e3-170">我們為 NerdDinner 應用程式建立的所有視圖範本（[清單]、[詳細資料]、[編輯]、[建立]、[NotFound] 等等）都是以這個網站為主範本為基礎。</span><span class="sxs-lookup"><span data-stu-id="574e3-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="574e3-171">當我們使用 [加入視圖] 對話方塊建立我們的視圖時，會透過預設新增至前 &lt;% @ Page%&gt; 指示詞的 "MasterPageFile" 屬性來表示這種情況：</span><span class="sxs-lookup"><span data-stu-id="574e3-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="574e3-172">這表示我們可以變更網站的內容，並在轉譯任何視圖範本時，自動套用並使用變更。</span><span class="sxs-lookup"><span data-stu-id="574e3-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="574e3-173">讓我們更新我們的網站。主要的標頭區段，讓應用程式的標頭是 "NerdDinner"，而不是「我的 MVC 應用程式」。</span><span class="sxs-lookup"><span data-stu-id="574e3-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="574e3-174">讓我們也更新導覽功能表，讓第一個索引標籤為「尋找晚餐」（由 HomeController 的 Index （）動作方法處理），並新增名為「主控晚餐」的新索引標籤（由 DinnersController 的 Create （）動作方法處理）：</span><span class="sxs-lookup"><span data-stu-id="574e3-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="574e3-175">當我們儲存網站檔案並重新整理瀏覽器時，我們會看到我們的應用程式內所有視圖的標頭變更會顯示在其中。</span><span class="sxs-lookup"><span data-stu-id="574e3-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="574e3-176">例如:</span><span class="sxs-lookup"><span data-stu-id="574e3-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="574e3-177">並使用 */Dinners/Edit/[id]* URL：</span><span class="sxs-lookup"><span data-stu-id="574e3-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="574e3-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="574e3-178">Next Step</span></span>

<span data-ttu-id="574e3-179">部分和主版頁面提供極具彈性的選項，可讓您完全整理視圖。</span><span class="sxs-lookup"><span data-stu-id="574e3-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="574e3-180">您會發現它們可協助您避免重複的 view 內容/程式碼，並讓您的視圖範本更容易閱讀和維護。</span><span class="sxs-lookup"><span data-stu-id="574e3-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="574e3-181">現在讓我們來回顧我們稍早建立的清單案例，並啟用可調整的分頁支援。</span><span class="sxs-lookup"><span data-stu-id="574e3-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="574e3-182">[上一頁](use-viewdata-and-implement-viewmodel-classes.md)
> [下一頁](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="574e3-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
