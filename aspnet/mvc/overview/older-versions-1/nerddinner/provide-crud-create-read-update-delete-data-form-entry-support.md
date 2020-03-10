---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD （建立、讀取、更新、刪除）資料表單專案支援 |Microsoft Docs
author: microsoft
description: 步驟5顯示如何藉由啟用編輯、建立和刪除 Dinners 的支援，進一步 DinnersController 類別。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580553"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="8351b-103">提供 CRUD (建立、讀取、更新、刪除) 資料表單項目支援</span><span class="sxs-lookup"><span data-stu-id="8351b-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="8351b-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8351b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8351b-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="8351b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="8351b-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟5，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8351b-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="8351b-107">步驟5顯示如何藉由啟用編輯、建立和刪除 Dinners 的支援，進一步 DinnersController 類別。</span><span class="sxs-lookup"><span data-stu-id="8351b-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="8351b-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="8351b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="8351b-109">NerdDinner 步驟5：建立、更新、刪除表單案例</span><span class="sxs-lookup"><span data-stu-id="8351b-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="8351b-110">我們引進了控制器和觀點，並涵蓋如何使用它們來在網站上執行 Dinners 的清單/詳細資料體驗。</span><span class="sxs-lookup"><span data-stu-id="8351b-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="8351b-111">我們的下一步是進一步讓我們的 DinnersController 類別，並支援編輯、建立和刪除 Dinners。</span><span class="sxs-lookup"><span data-stu-id="8351b-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="8351b-112">DinnersController 處理的 Url</span><span class="sxs-lookup"><span data-stu-id="8351b-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="8351b-113">我們先前已將動作方法新增至 DinnersController，以支援兩個 Url： */Dinners*和 */Dinners/Details/[id]* 。</span><span class="sxs-lookup"><span data-stu-id="8351b-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="8351b-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="8351b-114">**URL**</span></span> | <span data-ttu-id="8351b-115">**動詞**</span><span class="sxs-lookup"><span data-stu-id="8351b-115">**VERB**</span></span> | <span data-ttu-id="8351b-116">**目的**</span><span class="sxs-lookup"><span data-stu-id="8351b-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8351b-117">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="8351b-117">*/Dinners/*</span></span> | <span data-ttu-id="8351b-118">GET</span><span class="sxs-lookup"><span data-stu-id="8351b-118">GET</span></span> | <span data-ttu-id="8351b-119">顯示即將推出之 dinners 的 HTML 清單。</span><span class="sxs-lookup"><span data-stu-id="8351b-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="8351b-120">*/Dinners/Details/[識別碼]*</span><span class="sxs-lookup"><span data-stu-id="8351b-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="8351b-121">GET</span><span class="sxs-lookup"><span data-stu-id="8351b-121">GET</span></span> | <span data-ttu-id="8351b-122">顯示特定晚餐的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8351b-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="8351b-123">我們現在會新增動作方法來執行三個額外的 Url： */Dinners/Edit/[id]* 、 */Dinners/Create*和 */Dinners/Delete/[id]* 。</span><span class="sxs-lookup"><span data-stu-id="8351b-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="8351b-124">這些 Url 可讓您編輯現有的 Dinners、建立新的 Dinners，以及刪除 Dinners。</span><span class="sxs-lookup"><span data-stu-id="8351b-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="8351b-125">我們將同時支援 HTTP GET 與 HTTP POST 動詞命令與這些新 Url 的互動。</span><span class="sxs-lookup"><span data-stu-id="8351b-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="8351b-126">這些 Url 的 HTTP GET 要求會顯示資料的初始 HTML 視圖（在 "edit" 案例中填入晚餐資料的表單、在 "create" 案例中為空白表單，以及在 "delete" 案例中為刪除確認畫面）。</span><span class="sxs-lookup"><span data-stu-id="8351b-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="8351b-127">對這些 Url 的 HTTP POST 要求將會儲存/更新/刪除 DinnerRepository 中的晚餐資料（從該處到資料庫）。</span><span class="sxs-lookup"><span data-stu-id="8351b-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="8351b-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="8351b-128">**URL**</span></span> | <span data-ttu-id="8351b-129">**動詞**</span><span class="sxs-lookup"><span data-stu-id="8351b-129">**VERB**</span></span> | <span data-ttu-id="8351b-130">**目的**</span><span class="sxs-lookup"><span data-stu-id="8351b-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8351b-131">*/Dinners/Edit/[識別碼]*</span><span class="sxs-lookup"><span data-stu-id="8351b-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="8351b-132">GET</span><span class="sxs-lookup"><span data-stu-id="8351b-132">GET</span></span> | <span data-ttu-id="8351b-133">顯示填入晚餐資料的可編輯 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="8351b-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="8351b-134">POST</span><span class="sxs-lookup"><span data-stu-id="8351b-134">POST</span></span> | <span data-ttu-id="8351b-135">將特定晚餐的表單變更儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="8351b-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="8351b-136">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="8351b-136">*/Dinners/Create*</span></span> | <span data-ttu-id="8351b-137">GET</span><span class="sxs-lookup"><span data-stu-id="8351b-137">GET</span></span> | <span data-ttu-id="8351b-138">顯示空的 HTML 表單，讓使用者定義新的 Dinners。</span><span class="sxs-lookup"><span data-stu-id="8351b-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="8351b-139">POST</span><span class="sxs-lookup"><span data-stu-id="8351b-139">POST</span></span> | <span data-ttu-id="8351b-140">建立新的晚餐，並將其儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="8351b-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="8351b-141">*/Dinners/Delete/[識別碼]*</span><span class="sxs-lookup"><span data-stu-id="8351b-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="8351b-142">GET</span><span class="sxs-lookup"><span data-stu-id="8351b-142">GET</span></span> | <span data-ttu-id="8351b-143">顯示刪除確認畫面。</span><span class="sxs-lookup"><span data-stu-id="8351b-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="8351b-144">POST</span><span class="sxs-lookup"><span data-stu-id="8351b-144">POST</span></span> | <span data-ttu-id="8351b-145">從資料庫刪除指定的晚餐。</span><span class="sxs-lookup"><span data-stu-id="8351b-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="8351b-146">編輯支援</span><span class="sxs-lookup"><span data-stu-id="8351b-146">Edit Support</span></span>

<span data-ttu-id="8351b-147">讓我們從執行「編輯」案例開始。</span><span class="sxs-lookup"><span data-stu-id="8351b-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="8351b-148">HTTP-取得編輯動作方法</span><span class="sxs-lookup"><span data-stu-id="8351b-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="8351b-149">我們一開始會先執行編輯動作方法的 HTTP "GET" 行為。</span><span class="sxs-lookup"><span data-stu-id="8351b-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="8351b-150">當要求 */Dinners/Edit/[id]* URL 時，將會叫用這個方法。</span><span class="sxs-lookup"><span data-stu-id="8351b-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="8351b-151">我們的實現如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="8351b-152">上述程式碼會使用 DinnerRepository 來取出晚餐物件。</span><span class="sxs-lookup"><span data-stu-id="8351b-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="8351b-153">然後，它會使用晚餐物件呈現視圖範本。</span><span class="sxs-lookup"><span data-stu-id="8351b-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="8351b-154">因為我們尚未明確地將範本名稱傳遞給*view （）* helper 方法，所以它會使用以慣例為基礎的預設路徑來解析視圖範本：/Views/Dinners/Edit.aspx。</span><span class="sxs-lookup"><span data-stu-id="8351b-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="8351b-155">現在讓我們建立這個 view 範本。</span><span class="sxs-lookup"><span data-stu-id="8351b-155">Let's now create this view template.</span></span> <span data-ttu-id="8351b-156">若要這麼做，請以滑鼠右鍵按一下 [編輯] 方法，然後選取 [新增視圖] 內容功能表命令：</span><span class="sxs-lookup"><span data-stu-id="8351b-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="8351b-157">在 [新增視圖] 對話方塊中，我們會指示我們將晚餐物件傳遞至我們的 View 範本作為其模型，並選擇自動 scaffold 「編輯」範本：</span><span class="sxs-lookup"><span data-stu-id="8351b-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="8351b-158">當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們新增 "Edit .aspx" view 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="8351b-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="8351b-159">它也會在程式碼編輯器中開啟新的「編輯 .aspx」視圖範本，並以初始的「編輯」 scaffold 執行方式填入，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="8351b-160">讓我們對產生的預設 [編輯] scaffold 進行一些變更，並更新編輯檢視範本，使其具有下列內容（這會移除一些我們不想公開的屬性）：</span><span class="sxs-lookup"><span data-stu-id="8351b-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="8351b-161">當我們執行應用程式並要求 *"/Dinners/Edit/1"* URL 時，我們會看到下列頁面：</span><span class="sxs-lookup"><span data-stu-id="8351b-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="8351b-162">我們的視圖所產生的 HTML 標籤如下所示。</span><span class="sxs-lookup"><span data-stu-id="8351b-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="8351b-163">這是標準的 HTML –具有 &lt;表單&gt; 元素，可在推送 [儲存] &lt;輸入類型 = "submit"/&gt; 按鈕時，對 */Dinners/Edit/1* URL 執行 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="8351b-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="8351b-164">HTML &lt;輸入類型 = "text"/&gt; 元素已針對每個可編輯的屬性輸出：</span><span class="sxs-lookup"><span data-stu-id="8351b-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="8351b-165">Html. Html.beginform （）和 Html. TextBox （） Html Helper 方法</span><span class="sxs-lookup"><span data-stu-id="8351b-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="8351b-166">我們的 "Edit .aspx" 視圖範本使用數個 "Html Helper" 方法： Html. ValidationSummary （）、Html.beginform （）、Html. TextBox （）和 ValidationMessage （）。</span><span class="sxs-lookup"><span data-stu-id="8351b-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="8351b-167">除了為我們產生 HTML 標籤以外，這些 helper 方法還提供內建的錯誤處理和驗證支援。</span><span class="sxs-lookup"><span data-stu-id="8351b-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="8351b-168">Html.beginform （） helper 方法</span><span class="sxs-lookup"><span data-stu-id="8351b-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="8351b-169">Html.beginform （） helper 方法是在標記中將 HTML &lt;表單&gt; 元素的輸出。</span><span class="sxs-lookup"><span data-stu-id="8351b-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="8351b-170">在我們的編輯 .aspx 視圖範本中，您會發現，使用此C#方法時，我們會套用 "using" 語句。</span><span class="sxs-lookup"><span data-stu-id="8351b-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="8351b-171">左大括弧表示 &lt;表單的開頭&gt; 內容，而右大括弧則表示 &lt;/form&gt; 元素的結尾：</span><span class="sxs-lookup"><span data-stu-id="8351b-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="8351b-172">或者，如果您在這類案例中找到 "using" 語句方法非自然，您可以使用 Html.beginform （）和 EndForm （）組合（這會執行相同的動作）：</span><span class="sxs-lookup"><span data-stu-id="8351b-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="8351b-173">呼叫 Html.beginform （）而不使用任何參數，會使其輸出會對目前要求的 URL 執行 HTTP POST 的 form 元素。</span><span class="sxs-lookup"><span data-stu-id="8351b-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="8351b-174">這就是為什麼我們的編輯檢視會產生 *&lt;form action = "/Dinners/Edit/1" method = "post"&gt;* 元素。</span><span class="sxs-lookup"><span data-stu-id="8351b-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="8351b-175">如果我們想要張貼至不同的 URL，也可以選擇將明確的參數傳遞至 Html.beginform （）。</span><span class="sxs-lookup"><span data-stu-id="8351b-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="8351b-176">Html. TextBox （） helper 方法</span><span class="sxs-lookup"><span data-stu-id="8351b-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="8351b-177">我們的 Edit .aspx view 會使用 Html. TextBox （） helper 方法來輸出 &lt;輸入類型 = "text"/&gt; 元素：</span><span class="sxs-lookup"><span data-stu-id="8351b-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="8351b-178">上述的 .Html （）方法會採用單一參數，這是用來指定要輸出之 &lt;輸入類型 = "text"/&gt; 元素的 id/name 屬性，以及用來填入 TextBox 值的模型屬性。</span><span class="sxs-lookup"><span data-stu-id="8351b-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="8351b-179">例如，我們傳遞至編輯檢視的晚餐物件的「標題」屬性值為「.NET 先期，」，因此我們的 Html. TextBox （"Title"）方法會呼叫 output： *&lt;輸入 id = "title" name = "title" type = "text" value = ". NET 先期，"/&gt;* 。</span><span class="sxs-lookup"><span data-stu-id="8351b-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="8351b-180">或者，我們可以使用第一個 Html. TextBox （）參數來指定專案的識別碼/名稱，然後明確地傳入要當做第二個參數使用的值：</span><span class="sxs-lookup"><span data-stu-id="8351b-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="8351b-181">我們通常會想要對輸出的值執行自訂格式。</span><span class="sxs-lookup"><span data-stu-id="8351b-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="8351b-182">在這些情況下，內建 .NET 的 String. Format （）靜態方法很有用。</span><span class="sxs-lookup"><span data-stu-id="8351b-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="8351b-183">我們的 Edit .aspx view 範本會使用此格式來格式化 EventDate 值（這是 DateTime 類型），因此它不會顯示時間的秒數：</span><span class="sxs-lookup"><span data-stu-id="8351b-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="8351b-184">可以選擇性地使用 Html. TextBox （）的第三個參數來輸出其他 HTML 屬性。</span><span class="sxs-lookup"><span data-stu-id="8351b-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="8351b-185">下列程式碼片段示範如何在 &lt;輸入類型 = "text"/&gt; 元素上轉譯額外的 size = "30" 屬性和 class = "mycssclass" 屬性。</span><span class="sxs-lookup"><span data-stu-id="8351b-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="8351b-186">請注意，使用「@" character because "類別」來將類別屬性的名稱進行轉義，是中C#保留的關鍵字：</span><span class="sxs-lookup"><span data-stu-id="8351b-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="8351b-187">執行 HTTP POST 編輯動作方法</span><span class="sxs-lookup"><span data-stu-id="8351b-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="8351b-188">我們現在已執行編輯動作方法的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="8351b-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="8351b-189">當使用者要求 */Dinners/Edit/1* URL 時，他們會收到如下所示的 HTML 網頁：</span><span class="sxs-lookup"><span data-stu-id="8351b-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="8351b-190">按 [儲存] 按鈕會導致表單張貼至 */Dinners/Edit/1* URL，並使用 HTTP post 動詞命令提交 HTML &lt;輸入&gt; 的表單值。</span><span class="sxs-lookup"><span data-stu-id="8351b-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="8351b-191">現在讓我們來執行編輯動作方法的 HTTP POST 行為–這會處理晚餐的儲存。</span><span class="sxs-lookup"><span data-stu-id="8351b-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="8351b-192">首先，我們會將多載的「編輯」動作方法新增至我們的 DinnersController，其上具有 "AcceptVerbs" 屬性，表示它會處理 HTTP POST 案例：</span><span class="sxs-lookup"><span data-stu-id="8351b-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="8351b-193">當 [AcceptVerbs] 屬性套用至多載的動作方法時，ASP.NET MVC 會根據傳入的 HTTP 動詞命令，自動處理分派要求至適當的動作方法。</span><span class="sxs-lookup"><span data-stu-id="8351b-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="8351b-194">*/Dinners/Edit/[id]* URL 的 HTTP POST 要求將會移至上述的 Edit 方法，而 */Dinners/Edit/[id]* URL 的所有其他 HTTP 動詞要求都會移至我們所實的第一個編輯方法（沒有 `[AcceptVerbs]` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="8351b-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="8351b-195">**側邊主題：為什麼要透過 HTTP 動詞來區分？**</span><span class="sxs-lookup"><span data-stu-id="8351b-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="8351b-196">您可能會問–為什麼我們要使用單一 URL，並透過 HTTP 指令動詞來區分其行為？</span><span class="sxs-lookup"><span data-stu-id="8351b-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="8351b-197">為什麼不只有兩個不同的 Url 來處理載入和儲存編輯變更？</span><span class="sxs-lookup"><span data-stu-id="8351b-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="8351b-198">例如：/Dinners/Edit/[id] 顯示初始表單，而/Dinners/Save/[id] 則用來處理表單張貼以儲存它嗎？</span><span class="sxs-lookup"><span data-stu-id="8351b-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="8351b-199">發佈兩個不同的 Url 的缺點是，在我們張貼至/Dinners/Save/2，然後因為輸入錯誤而需要重新顯示 HTML 表單的情況下，使用者最後會在其瀏覽器的網址列中擁有/Dinners/Save/2 URL （因為這是表單張貼的 URL）。</span><span class="sxs-lookup"><span data-stu-id="8351b-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="8351b-200">如果使用者將此重新顯示頁面的書簽重新顯示到其瀏覽器的 [我的最愛] 清單，或複製/貼上 URL 並以電子郵件傳送給朋友，他們最後會儲存無法在未來使用的 URL （因為該 URL 取決於 post 值）。</span><span class="sxs-lookup"><span data-stu-id="8351b-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="8351b-201">藉由公開單一 URL （例如：/Dinners/Edit/[id]）並區分 HTTP 動詞命令的處理方式，使用者可以安全地將編輯頁面加入書簽，並（或）將 URL 傳送給其他人。</span><span class="sxs-lookup"><span data-stu-id="8351b-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="8351b-202">正在抓取表單張貼值</span><span class="sxs-lookup"><span data-stu-id="8351b-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="8351b-203">有多種方法可以存取我們的 HTTP POST "Edit" 方法內的張貼表單參數。</span><span class="sxs-lookup"><span data-stu-id="8351b-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="8351b-204">一個簡單的方法是只使用控制器基類上的 Request 屬性來存取表單集合，並直接抓取張貼的值：</span><span class="sxs-lookup"><span data-stu-id="8351b-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="8351b-205">上述方法稍加說明，尤其是在我們新增錯誤處理邏輯時。</span><span class="sxs-lookup"><span data-stu-id="8351b-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="8351b-206">此案例的更好方法是，在控制器基類上運用內建的*UpdateModel （）* helper 方法。</span><span class="sxs-lookup"><span data-stu-id="8351b-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="8351b-207">它支援更新物件的屬性，我們使用傳入的表單參數將其傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="8351b-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="8351b-208">它會使用反映來判斷物件上的屬性名稱，然後根據用戶端所提交的輸入值，自動轉換並指派值給它們。</span><span class="sxs-lookup"><span data-stu-id="8351b-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="8351b-209">我們可以使用 UpdateModel （）方法，透過下列程式碼來簡化我們的 HTTP POST 編輯動作：</span><span class="sxs-lookup"><span data-stu-id="8351b-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="8351b-210">我們現在可以造訪 */Dinners/Edit/1* URL，並變更晚餐的標題：</span><span class="sxs-lookup"><span data-stu-id="8351b-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="8351b-211">當我們按一下 [儲存] 按鈕時，我們會對編輯動作執行表單張貼，而更新的值將會保存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="8351b-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="8351b-212">接著，我們會將晚餐的詳細資料 URL 重新導向（這會顯示新儲存的值）：</span><span class="sxs-lookup"><span data-stu-id="8351b-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="8351b-213">處理編輯錯誤</span><span class="sxs-lookup"><span data-stu-id="8351b-213">Handling Edit Errors</span></span>

<span data-ttu-id="8351b-214">我們目前的 HTTP-POST 執行正常運作，除非發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="8351b-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="8351b-215">當使用者編輯表單時發生錯誤時，我們必須確定表單會重新顯示，並出現一則資訊性錯誤訊息，引導他們修正此問題。</span><span class="sxs-lookup"><span data-stu-id="8351b-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="8351b-216">這包括使用者張貼不正確輸入的情況（例如：格式不正確的日期字串），以及輸入格式有效但有商務規則違規的情況。</span><span class="sxs-lookup"><span data-stu-id="8351b-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="8351b-217">發生錯誤時，表單應保留使用者原本輸入的輸入資料，讓他們不需要手動重新填滿變更。</span><span class="sxs-lookup"><span data-stu-id="8351b-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="8351b-218">此程式應該在表單成功完成之前，視需要重複多次。</span><span class="sxs-lookup"><span data-stu-id="8351b-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="8351b-219">ASP.NET MVC 包含一些好用的內建功能，可讓您輕鬆地進行錯誤處理和表單重新顯示。</span><span class="sxs-lookup"><span data-stu-id="8351b-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="8351b-220">若要查看這些功能的作用，讓我們使用下列程式碼來更新編輯動作方法：</span><span class="sxs-lookup"><span data-stu-id="8351b-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="8351b-221">上述程式碼與先前的執行方式類似，不同之處在于我們現在會將 try/catch 錯誤處理區塊包裝在我們的工作周圍。</span><span class="sxs-lookup"><span data-stu-id="8351b-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="8351b-222">如果在呼叫 UpdateModel （）時或在嘗試儲存 DinnerRepository 時發生例外狀況（如果我們嘗試儲存的晚餐物件因為在我們的模型中違反規則而無效，則會引發例外狀況），我們的 catch 錯誤處理區塊將會執行.</span><span class="sxs-lookup"><span data-stu-id="8351b-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="8351b-223">在此期間，我們會迴圈處理晚餐物件中存在的任何規則違規，並將其新增至 ModelState 物件（我們將在稍後討論）。</span><span class="sxs-lookup"><span data-stu-id="8351b-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="8351b-224">然後重新顯示此視圖。</span><span class="sxs-lookup"><span data-stu-id="8351b-224">We then redisplay the view.</span></span>

<span data-ttu-id="8351b-225">若要查看此工作，讓我們重新執行應用程式、編輯晚餐，然後將它變更為空白標題、EventDate 為「假」，並使用國家/地區值為 USA 的英國電話號碼。</span><span class="sxs-lookup"><span data-stu-id="8351b-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="8351b-226">當我們按下 [儲存] 按鈕時，我們的 HTTP POST 編輯方法將無法儲存晚餐（因為有錯誤），並會重新顯示表單：</span><span class="sxs-lookup"><span data-stu-id="8351b-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="8351b-227">我們的應用程式具有適當的錯誤體驗。</span><span class="sxs-lookup"><span data-stu-id="8351b-227">Our application has a decent error experience.</span></span> <span data-ttu-id="8351b-228">具有無效輸入的文字元素會以紅色反白顯示，並向使用者顯示驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="8351b-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="8351b-229">表單也會保留使用者原先輸入的輸入資料，使其不需要重填任何專案。</span><span class="sxs-lookup"><span data-stu-id="8351b-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="8351b-230">您可能會問，這是發生的嗎？</span><span class="sxs-lookup"><span data-stu-id="8351b-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="8351b-231">[Title]、[EventDate] 和 [ContactPhone] 文字方塊會以紅色反白顯示其本身，並知道要輸出原先輸入的使用者值嗎？</span><span class="sxs-lookup"><span data-stu-id="8351b-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="8351b-232">錯誤訊息如何顯示在頂端的清單中？</span><span class="sxs-lookup"><span data-stu-id="8351b-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="8351b-233">好消息是，這並不是因為神奇而發生，因為我們使用一些內建的 ASP.NET MVC 功能，讓輸入驗證和錯誤處理案例變得很容易。</span><span class="sxs-lookup"><span data-stu-id="8351b-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="8351b-234">瞭解 ModelState 和驗證 HTML Helper 方法</span><span class="sxs-lookup"><span data-stu-id="8351b-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="8351b-235">控制器類別具有 "ModelState" 屬性集合，可提供一種方法來指出與傳遞給視圖的模型物件存在錯誤。</span><span class="sxs-lookup"><span data-stu-id="8351b-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="8351b-236">ModelState 集合內的錯誤專案會識別具有問題的模型屬性名稱（例如： "Title"、"EventDate" 或 "ContactPhone"），並允許指定人為易記的錯誤訊息（例如：「需要標題」）。</span><span class="sxs-lookup"><span data-stu-id="8351b-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="8351b-237">*UpdateModel （）* helper 方法會在嘗試將表單值指派給模型物件上的屬性時，自動填入 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="8351b-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="8351b-238">例如，我們晚餐物件的 EventDate 屬性是 DateTime 類型。</span><span class="sxs-lookup"><span data-stu-id="8351b-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="8351b-239">當 UpdateModel （）方法在上述案例中無法將字串值「假」指派給它時，UpdateModel （）方法會將專案新增至 ModelState 集合，指出該屬性發生指派錯誤。</span><span class="sxs-lookup"><span data-stu-id="8351b-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="8351b-240">開發人員也可以撰寫程式碼，以明確地將錯誤專案新增至 ModelState 集合，如同我們在「catch」錯誤處理區塊內執行的動作，它會根據中的作用中規則違規，將專案填入 ModelState 集合。晚餐物件：</span><span class="sxs-lookup"><span data-stu-id="8351b-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="8351b-241">Html Helper 與 ModelState 的整合</span><span class="sxs-lookup"><span data-stu-id="8351b-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="8351b-242">HTML helper 方法-like Html. TextBox （）-在轉譯輸出時檢查 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="8351b-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="8351b-243">如果專案的錯誤存在，則會轉譯使用者輸入的值和 CSS 錯誤類別。</span><span class="sxs-lookup"><span data-stu-id="8351b-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="8351b-244">例如，在我們的「編輯」視圖中，我們會使用 Html. TextBox （） helper 方法來呈現晚餐物件的 EventDate：</span><span class="sxs-lookup"><span data-stu-id="8351b-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="8351b-245">當此視圖在錯誤案例中呈現時，Html. TextBox （）方法會檢查 ModelState 集合，以查看是否有任何與晚餐物件的 "EventDate" 屬性相關聯的錯誤。</span><span class="sxs-lookup"><span data-stu-id="8351b-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="8351b-246">當它判定發生錯誤時，它會將提交的使用者輸入（「假」）轉譯為值，並將 css 錯誤類別新增至它所產生的 &lt;輸入類型 = "textbox"/&gt; 標記：</span><span class="sxs-lookup"><span data-stu-id="8351b-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="8351b-247">您可以自訂 css 錯誤類別的外觀，以尋找您想要的樣子。</span><span class="sxs-lookup"><span data-stu-id="8351b-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="8351b-248">預設的 CSS 錯誤類別-「輸入-驗證-錯誤」–定義于 *\content\site.css*樣式表單中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="8351b-249">此 CSS 規則會導致不正確輸入元素反白顯示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="8351b-250">ValidationMessage （） Helper 方法</span><span class="sxs-lookup"><span data-stu-id="8351b-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="8351b-251">ValidationMessage （） helper 方法可以用來輸出與特定模型屬性相關聯的 ModelState 錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="8351b-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="8351b-252">上述程式碼會輸出： *&lt;span class = "field-驗證-error"&gt; 值 ' 假 '&lt;/span 無效&gt;*</span><span class="sxs-lookup"><span data-stu-id="8351b-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="8351b-253">ValidationMessage （） helper 方法也支援第二個參數，可讓開發人員覆寫顯示的錯誤文字訊息：</span><span class="sxs-lookup"><span data-stu-id="8351b-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="8351b-254">上述程式碼會輸出： *&lt;span class = "欄位驗證-錯誤"&gt;\*&lt;/span&gt;* 而不是 EventDate 屬性出現錯誤時的預設錯誤文字。</span><span class="sxs-lookup"><span data-stu-id="8351b-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="8351b-255">ValidationSummary （） Helper 方法</span><span class="sxs-lookup"><span data-stu-id="8351b-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="8351b-256">ValidationSummary （） helper 方法可用來轉譯摘要錯誤訊息，伴隨 &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; ModelState 集合中所有詳細錯誤訊息的清單：</span><span class="sxs-lookup"><span data-stu-id="8351b-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="8351b-257">ValidationSummary （） helper 方法會接受選擇性的 string 參數，它會定義摘要錯誤訊息，以顯示在詳細錯誤清單上方：</span><span class="sxs-lookup"><span data-stu-id="8351b-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="8351b-258">您可以選擇性地使用 CSS 來覆寫 [錯誤清單] 的樣子。</span><span class="sxs-lookup"><span data-stu-id="8351b-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="8351b-259">使用 AddRuleViolations Helper 方法</span><span class="sxs-lookup"><span data-stu-id="8351b-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="8351b-260">初始的 HTTP POST 編輯執行會使用其 catch 區塊內的 foreach 語句來迴圈晚餐物件的規則違規，並將其新增至控制器的 ModelState 集合：</span><span class="sxs-lookup"><span data-stu-id="8351b-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="8351b-261">我們可以將 "ControllerHelpers" 類別新增至 NerdDinner 專案，並在其中執行「AddRuleViolations」擴充方法，將 helper 方法新增至 ASP.NET MVC ModelStateDictionary 類別，讓這段程式碼更簡潔。</span><span class="sxs-lookup"><span data-stu-id="8351b-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="8351b-262">這個擴充方法可以封裝在 ModelStateDictionary 中填入 RuleViolation 錯誤清單所需的邏輯：</span><span class="sxs-lookup"><span data-stu-id="8351b-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="8351b-263">然後，我們可以更新我們的 HTTP POST 編輯動作方法，以使用此延伸模組方法，在 ModelState 集合中填入晚餐規則違規。</span><span class="sxs-lookup"><span data-stu-id="8351b-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="8351b-264">完成編輯動作方法的執行</span><span class="sxs-lookup"><span data-stu-id="8351b-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="8351b-265">下列程式碼會執行編輯案例所需的所有控制器邏輯：</span><span class="sxs-lookup"><span data-stu-id="8351b-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="8351b-266">我們的編輯執行的好處在於，控制器類別和我們的 View 範本都不需要知道晚餐模型所強制執行的特定驗證或商務規則。</span><span class="sxs-lookup"><span data-stu-id="8351b-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="8351b-267">我們未來可以在模型中加入其他規則，而不需要對我們的控制器或視圖進行任何程式碼變更，就能加以支援。</span><span class="sxs-lookup"><span data-stu-id="8351b-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="8351b-268">如此一來，我們就能彈性地在未來輕鬆開發我們的應用程式需求，並變更最少的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8351b-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="8351b-269">建立支援</span><span class="sxs-lookup"><span data-stu-id="8351b-269">Create Support</span></span>

<span data-ttu-id="8351b-270">我們已完成執行 DinnersController 類別的「編輯」行為。</span><span class="sxs-lookup"><span data-stu-id="8351b-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="8351b-271">現在讓我們繼續執行它的「建立」支援–這可讓使用者加入新的 Dinners。</span><span class="sxs-lookup"><span data-stu-id="8351b-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="8351b-272">HTTP-GET Create 動作方法</span><span class="sxs-lookup"><span data-stu-id="8351b-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="8351b-273">我們一開始會先執行建立動作方法的 HTTP 「GET」行為。</span><span class="sxs-lookup"><span data-stu-id="8351b-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="8351b-274">當有人造訪 */Dinners/Create* URL 時，將會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="8351b-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="8351b-275">我們的執行如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="8351b-276">上述程式碼會建立新的晚餐物件，並將其 EventDate 屬性指派為未來的一周。</span><span class="sxs-lookup"><span data-stu-id="8351b-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="8351b-277">然後，它會呈現以新晚餐物件為基礎的視圖。</span><span class="sxs-lookup"><span data-stu-id="8351b-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="8351b-278">因為我們尚未明確地將名稱傳遞給*view （）* helper 方法，所以它會使用以慣例為基礎的預設路徑來解析視圖範本：/Views/Dinners/Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="8351b-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="8351b-279">現在讓我們建立這個 view 範本。</span><span class="sxs-lookup"><span data-stu-id="8351b-279">Let's now create this view template.</span></span> <span data-ttu-id="8351b-280">若要這麼做，請在 [建立動作] 方法中按一下滑鼠右鍵，然後選取 [新增視圖] 內容功能表命令。</span><span class="sxs-lookup"><span data-stu-id="8351b-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="8351b-281">在 [新增視圖] 對話方塊中，我們會指出我們要將晚餐物件傳遞至 View 範本，並選擇自動 scaffold 「建立」範本：</span><span class="sxs-lookup"><span data-stu-id="8351b-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="8351b-282">當我們按一下 [新增] 按鈕時，Visual Studio 會將以 scaffold 為基礎的新 "Create .aspx" 視圖儲存至 "\Views\Dinners" 目錄，並在 IDE 中開啟它：</span><span class="sxs-lookup"><span data-stu-id="8351b-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="8351b-283">讓我們對為我們產生的預設「建立」 scaffold 檔案進行一些變更，並加以修改，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="8351b-284">現在當我們執行應用程式並在瀏覽器中存取 *"/Dinners/Create"* URL 時，它會從我們的建立動作執行轉譯如下所示的 UI：</span><span class="sxs-lookup"><span data-stu-id="8351b-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="8351b-285">執行 HTTP POST 建立動作方法</span><span class="sxs-lookup"><span data-stu-id="8351b-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="8351b-286">我們已實現建立動作方法的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="8351b-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="8351b-287">當使用者按一下 [儲存] 按鈕時，它會執行表單張貼至 */Dinners/Create* URL，並使用 HTTP post 動詞命令提交 HTML &lt;輸入&gt; 的表單值。</span><span class="sxs-lookup"><span data-stu-id="8351b-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="8351b-288">現在讓我們來執行 create action 方法的 HTTP POST 行為。</span><span class="sxs-lookup"><span data-stu-id="8351b-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="8351b-289">我們一開始會先將多載的「建立」動作方法新增至我們的 DinnersController，其上具有 "AcceptVerbs" 屬性，表示它會處理 HTTP POST 案例：</span><span class="sxs-lookup"><span data-stu-id="8351b-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="8351b-290">有多種方式可以在啟用 HTTP POST 的「建立」方法中存取張貼的表單參數。</span><span class="sxs-lookup"><span data-stu-id="8351b-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="8351b-291">其中一種方法是建立新的晚餐物件，然後使用*UpdateModel （）* helper 方法（如同我們對 [編輯] 動作所做的），將已張貼的表單值填入其中。</span><span class="sxs-lookup"><span data-stu-id="8351b-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="8351b-292">然後，我們可以將它新增至 DinnerRepository、將它保存在資料庫中，然後將使用者重新導向至 [詳細資料] 動作，以使用下列程式碼來顯示新建立的晚餐：</span><span class="sxs-lookup"><span data-stu-id="8351b-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="8351b-293">或者，我們可以使用一種方法，讓我們的 Create （）動作方法接受晚餐物件作為方法參數。</span><span class="sxs-lookup"><span data-stu-id="8351b-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="8351b-294">ASP.NET MVC 接著會自動為我們產生新的晚餐物件，並使用表單輸入填入其屬性，然後將它傳遞給我們的動作方法：</span><span class="sxs-lookup"><span data-stu-id="8351b-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="8351b-295">上述動作方法會藉由檢查 ModelState 屬性，確認晚餐物件是否已成功填入表單張貼值。</span><span class="sxs-lookup"><span data-stu-id="8351b-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="8351b-296">如果有輸入轉換問題（例如，EventDate 屬性的字串為 "假"），這會傳回 false，而如果有任何問題，則動作方法會重新出現表單。</span><span class="sxs-lookup"><span data-stu-id="8351b-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="8351b-297">如果輸入值有效，則動作方法會嘗試新增新晚餐並將其儲存至 DinnerRepository。</span><span class="sxs-lookup"><span data-stu-id="8351b-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="8351b-298">它會在 try/catch 區塊中包裝這項工作，並在有任何商務規則違規時重新出現表單（這會造成 dinnerRepository （）方法引發例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="8351b-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="8351b-299">若要查看作用中的這個錯誤處理行為，我們可以要求 */Dinners/Create* URL，並填寫新晚餐的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8351b-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="8351b-300">不正確的輸入或值會導致建立表單重新顯示，並醒目提示如下所示的錯誤：</span><span class="sxs-lookup"><span data-stu-id="8351b-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="8351b-301">請注意，我們的建立表單如何接受與編輯表單完全相同的驗證和商務規則。</span><span class="sxs-lookup"><span data-stu-id="8351b-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="8351b-302">這是因為我們在模型中定義了驗證和商務規則，而不是內嵌在應用程式的 UI 或控制器中。</span><span class="sxs-lookup"><span data-stu-id="8351b-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="8351b-303">這表示我們稍後可以在單一位置變更/發展我們的驗證或商務規則，並將其套用至整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="8351b-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="8351b-304">我們不需要變更我們的編輯或建立動作方法內的任何程式碼，就能自動接受任何新規則或對現有的修改。</span><span class="sxs-lookup"><span data-stu-id="8351b-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="8351b-305">當我們修正輸入值，然後再按一下 [儲存] 按鈕時，我們對 DinnerRepository 的新增將會成功，而且新的晚餐會新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="8351b-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="8351b-306">接著，我們會將您重新導向至 */Dinners/Details/[id]* URL-，我們會在其中看到新建立的晚餐的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="8351b-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="8351b-307">刪除支援</span><span class="sxs-lookup"><span data-stu-id="8351b-307">Delete Support</span></span>

<span data-ttu-id="8351b-308">現在讓我們將「刪除」支援新增至我們的 DinnersController。</span><span class="sxs-lookup"><span data-stu-id="8351b-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="8351b-309">HTTP-GET Delete 動作方法</span><span class="sxs-lookup"><span data-stu-id="8351b-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="8351b-310">我們一開始會先執行刪除動作方法的 HTTP GET 行為。</span><span class="sxs-lookup"><span data-stu-id="8351b-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="8351b-311">當有人造訪 */Dinners/Delete/[id]* URL 時，就會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="8351b-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="8351b-312">以下是實作為：</span><span class="sxs-lookup"><span data-stu-id="8351b-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="8351b-313">動作方法會嘗試取出要刪除的晚餐。</span><span class="sxs-lookup"><span data-stu-id="8351b-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="8351b-314">如果晚餐存在，則會根據晚餐物件呈現視圖。</span><span class="sxs-lookup"><span data-stu-id="8351b-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="8351b-315">如果物件不存在（或已被刪除），它會傳回一個呈現我們稍早為「詳細資料」動作方法所建立之「NotFound」視圖範本的視圖。</span><span class="sxs-lookup"><span data-stu-id="8351b-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="8351b-316">我們可以在 [刪除動作] 方法中按一下滑鼠右鍵，然後選取 [新增視圖] 內容功能表命令，以建立 [刪除] 視圖範本。</span><span class="sxs-lookup"><span data-stu-id="8351b-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="8351b-317">在 [新增視圖] 對話方塊中，我們會指出我們會將晚餐物件傳遞至我們的 View 範本作為其模型，並選擇建立空的範本：</span><span class="sxs-lookup"><span data-stu-id="8351b-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="8351b-318">當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們新增 "Delete .aspx" 視圖範本檔案。</span><span class="sxs-lookup"><span data-stu-id="8351b-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="8351b-319">我們會將一些 HTML 和程式碼新增至範本，以執行如下所示的刪除確認畫面：</span><span class="sxs-lookup"><span data-stu-id="8351b-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="8351b-320">上述程式碼會顯示要刪除的晚餐標題，並輸出 &lt;表單&gt; 元素，該專案會在使用者按一下其中的 [刪除] 按鈕時，對/Dinners/Delete/[id] URL 執行 POST。</span><span class="sxs-lookup"><span data-stu-id="8351b-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="8351b-321">當我們執行應用程式並存取有效晚餐物件的 *"/Dinners/Delete/[id]"* URL 時，它會呈現如下所示的 UI：</span><span class="sxs-lookup"><span data-stu-id="8351b-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="8351b-322">**側邊主題：為什麼要進行貼文？**</span><span class="sxs-lookup"><span data-stu-id="8351b-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="8351b-323">您可能會問–為什麼我們要在刪除確認畫面中&gt; 建立 &lt;表單的工作？</span><span class="sxs-lookup"><span data-stu-id="8351b-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="8351b-324">為什麼不直接使用標準超連結來連結至執行實際刪除作業的動作方法？</span><span class="sxs-lookup"><span data-stu-id="8351b-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="8351b-325">這是因為我們想要小心預防 web 編目和搜尋引擎探索我們的 Url，並在追蹤這些連結時不小心造成資料被刪除。</span><span class="sxs-lookup"><span data-stu-id="8351b-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="8351b-326">以 HTTP 為基礎的 Url 會被視為「安全」，讓它們存取/編目，而且它們應該不會遵循 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="8351b-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="8351b-327">理想的規則是確保您一律將破壞性或資料修改作業放在 HTTP POST 要求後面。</span><span class="sxs-lookup"><span data-stu-id="8351b-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="8351b-328">執行 HTTP POST 刪除動作方法</span><span class="sxs-lookup"><span data-stu-id="8351b-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="8351b-329">我們現在已執行刪除動作方法的 HTTP GET 版本，它會顯示刪除確認畫面。</span><span class="sxs-lookup"><span data-stu-id="8351b-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="8351b-330">當使用者按一下 [刪除] 按鈕時，它會對 */Dinners/Dinner/[id]* URL 執行表單張貼。</span><span class="sxs-lookup"><span data-stu-id="8351b-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="8351b-331">現在，讓我們使用下列程式碼，來執行 delete 動作方法的 HTTP "POST" 行為：</span><span class="sxs-lookup"><span data-stu-id="8351b-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="8351b-332">刪除動作方法的 HTTP POST 版本會嘗試抓取晚餐物件以進行刪除。</span><span class="sxs-lookup"><span data-stu-id="8351b-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="8351b-333">如果找不到它（因為它已經被刪除），它會呈現我們的 "NotFound" 範本。</span><span class="sxs-lookup"><span data-stu-id="8351b-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="8351b-334">如果找到晚餐，則會將其從 DinnerRepository 中刪除。</span><span class="sxs-lookup"><span data-stu-id="8351b-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="8351b-335">然後，它會轉譯「已刪除」範本。</span><span class="sxs-lookup"><span data-stu-id="8351b-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="8351b-336">若要執行「已刪除」範本，我們會在動作方法中按一下滑鼠右鍵，然後選擇 [加入視圖] 內容功能表。</span><span class="sxs-lookup"><span data-stu-id="8351b-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="8351b-337">我們會將我們的觀點命名為「已刪除」，並讓它成為空的範本（而不是採用強型別模型物件）。</span><span class="sxs-lookup"><span data-stu-id="8351b-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="8351b-338">接著，我們會在其中新增一些 HTML 內容：</span><span class="sxs-lookup"><span data-stu-id="8351b-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="8351b-339">現在當我們執行應用程式並存取有效晚餐物件的 *"/Dinners/Delete/[id]"* URL 時，它會轉譯晚餐的刪除確認畫面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="8351b-340">當我們按一下 [刪除] 按鈕時，它會對 */Dinners/Delete/[id]* URL 執行 HTTP POST，這會從我們的資料庫刪除晚餐，並顯示我們的「已刪除」視圖範本：</span><span class="sxs-lookup"><span data-stu-id="8351b-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="8351b-341">模型系結安全性</span><span class="sxs-lookup"><span data-stu-id="8351b-341">Model Binding Security</span></span>

<span data-ttu-id="8351b-342">我們討論了兩種不同的方式，可使用 ASP.NET MVC 的內建模型系結功能。</span><span class="sxs-lookup"><span data-stu-id="8351b-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="8351b-343">第一個使用 UpdateModel （）方法來更新現有模型物件上的屬性，而第二個使用 ASP.NET MVC 支援在 as 動作方法參數中傳遞模型物件。</span><span class="sxs-lookup"><span data-stu-id="8351b-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="8351b-344">這兩種技術都非常強大，而且非常有用。</span><span class="sxs-lookup"><span data-stu-id="8351b-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="8351b-345">這種威力也具有 it 責任。</span><span class="sxs-lookup"><span data-stu-id="8351b-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="8351b-346">在接受任何使用者輸入時，一定要擇善固執安全性，而且當您將物件系結至表單輸入時，也會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="8351b-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="8351b-347">請務必小心，一律以 HTML 編碼任何使用者輸入的值，以避免 HTML 和 JavaScript 插入式攻擊，並留意 SQL 插入式攻擊（注意：我們會使用應用程式的 LINQ to SQL，這會自動將參數編碼以避免這些攻擊的類型）。</span><span class="sxs-lookup"><span data-stu-id="8351b-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="8351b-348">您絕對不應該依賴用戶端驗證，而且一律會採用伺服器端驗證，以防止駭客嘗試傳送假的值給您。</span><span class="sxs-lookup"><span data-stu-id="8351b-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="8351b-349">另一個安全性專案，請確定您在使用 ASP.NET MVC 的系結功能時，是您要系結之物件的範圍。</span><span class="sxs-lookup"><span data-stu-id="8351b-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="8351b-350">具體而言，您會想要確定您瞭解允許系結之屬性的安全性含意，並確定您只允許使用者可更新的那些屬性確實是可更新的。</span><span class="sxs-lookup"><span data-stu-id="8351b-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="8351b-351">根據預設，UpdateModel （）方法會嘗試更新模型物件上符合傳入表單參數值的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="8351b-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="8351b-352">同樣地，當做動作方法參數傳遞的物件，也可以透過表單參數來設定其所有屬性。</span><span class="sxs-lookup"><span data-stu-id="8351b-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="8351b-353">依據每次使用方式鎖定系結</span><span class="sxs-lookup"><span data-stu-id="8351b-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="8351b-354">您可以藉由提供可更新的屬性明確「包含清單」，以根據每次使用來鎖定系結原則。</span><span class="sxs-lookup"><span data-stu-id="8351b-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="8351b-355">這可以藉由將額外的字串陣列參數傳遞至 UpdateModel （）方法來完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="8351b-356">當做動作方法參數傳遞的物件也支援 [Bind] 屬性，可讓您指定允許屬性的「包含清單」，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8351b-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="8351b-357">依據類型鎖定系結</span><span class="sxs-lookup"><span data-stu-id="8351b-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="8351b-358">您也可以根據每個類型來鎖定系結規則。</span><span class="sxs-lookup"><span data-stu-id="8351b-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="8351b-359">這可讓您指定系結規則一次，然後將它們套用到所有控制器和動作方法的所有案例中（包括 UpdateModel 和動作方法參數案例）。</span><span class="sxs-lookup"><span data-stu-id="8351b-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="8351b-360">您可以自訂每個類型的系結規則，方法是將 [Bind] 屬性加入至類型，或在應用程式的 global.asax 檔案中註冊（適用于您不擁有該類型的案例）。</span><span class="sxs-lookup"><span data-stu-id="8351b-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="8351b-361">接著，您可以使用 Bind 屬性的 Include 和 Exclude 屬性來控制哪些屬性可系結至特定類別或介面。</span><span class="sxs-lookup"><span data-stu-id="8351b-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="8351b-362">我們會針對 NerdDinner 應用程式中的晚餐類別使用這項技術，並在其中新增 [Bind] 屬性，將可系結屬性的清單限制如下：</span><span class="sxs-lookup"><span data-stu-id="8351b-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="8351b-363">請注意，我們不允許透過系結來操作 RSVPs 集合，也不允許透過系結設定 DinnerID 或 HostedBy 屬性。</span><span class="sxs-lookup"><span data-stu-id="8351b-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="8351b-364">基於安全性理由，我們只會在動作方法內使用明確的程式碼來操作這些特定屬性。</span><span class="sxs-lookup"><span data-stu-id="8351b-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="8351b-365">CRUD 總結</span><span class="sxs-lookup"><span data-stu-id="8351b-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="8351b-366">ASP.NET MVC 包含一些內建功能，可協助您執行表單張貼案例。</span><span class="sxs-lookup"><span data-stu-id="8351b-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="8351b-367">我們使用了各種功能，在我們的 DinnerRepository 之上提供 CRUD UI 支援。</span><span class="sxs-lookup"><span data-stu-id="8351b-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="8351b-368">我們使用以模型為主的方法來執行我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8351b-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="8351b-369">這表示我們的所有驗證和商務規則邏輯都是在模型層內定義，而不是在我們的控制器或 views 內。</span><span class="sxs-lookup"><span data-stu-id="8351b-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="8351b-370">我們的控制器類別和我們的視圖範本都不知道晚餐模型類別所強制執行的特定商務規則。</span><span class="sxs-lookup"><span data-stu-id="8351b-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="8351b-371">這會讓我們的應用程式架構保持整潔，讓測試更容易。</span><span class="sxs-lookup"><span data-stu-id="8351b-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="8351b-372">我們可以在未來的模型層中加入額外的商務規則，而不需要對控制器或視圖*進行任何程式碼變更*，就能加以支援。</span><span class="sxs-lookup"><span data-stu-id="8351b-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="8351b-373">如此一來，我們就能在未來發展和變更應用程式，提供極大的靈活性。</span><span class="sxs-lookup"><span data-stu-id="8351b-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="8351b-374">我們的 DinnersController 現在會啟用晚餐清單/詳細資料，以及建立、編輯和刪除支援。</span><span class="sxs-lookup"><span data-stu-id="8351b-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="8351b-375">類別的完整程式碼可以在下面找到：</span><span class="sxs-lookup"><span data-stu-id="8351b-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="8351b-376">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8351b-376">Next Step</span></span>

<span data-ttu-id="8351b-377">我們現在有基本 CRUD （建立、讀取、更新和刪除）支援在我們的 DinnersController 類別中執行。</span><span class="sxs-lookup"><span data-stu-id="8351b-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="8351b-378">現在讓我們來看看如何使用 ViewData 和 ViewModel 類別，在我們的表單上啟用更豐富的 UI。</span><span class="sxs-lookup"><span data-stu-id="8351b-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8351b-379">[上一頁](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一頁](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="8351b-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
