---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用 ViewData 並執行 ViewModel 類別 |Microsoft Docs
author: microsoft
description: 步驟6顯示如何支援更豐富的表單編輯案例，同時討論兩種可以用來將資料從控制器傳遞至 views 的方法： 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541605"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="90098-103">使用 ViewData 和實作 ViewModel 類別</span><span class="sxs-lookup"><span data-stu-id="90098-103">Use ViewData and Implement ViewModel Classes</span></span>

<span data-ttu-id="90098-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="90098-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="90098-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="90098-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="90098-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟6，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="90098-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="90098-107">步驟6顯示如何支援更豐富的表單編輯案例，同時討論兩種可以用來將資料從控制器傳遞至 views 的方法： ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="90098-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="90098-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="90098-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="90098-109">NerdDinner 步驟6： ViewData 和 ViewModel</span><span class="sxs-lookup"><span data-stu-id="90098-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="90098-110">我們已涵蓋數種表單張貼案例，並已討論如何執行建立、更新和刪除（CRUD）支援。</span><span class="sxs-lookup"><span data-stu-id="90098-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="90098-111">我們現在會進一步進行 DinnersController 的執行，並支援更豐富的表單編輯案例。</span><span class="sxs-lookup"><span data-stu-id="90098-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="90098-112">這麼做時，我們將討論兩種可用於將資料從控制器傳遞至 views 的方法： ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="90098-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="90098-113">將資料從控制器傳遞至流覽-範本</span><span class="sxs-lookup"><span data-stu-id="90098-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="90098-114">MVC 模式的其中一個定義特性是嚴格的「關注點分離」，有助於在應用程式的不同元件之間強制執行。</span><span class="sxs-lookup"><span data-stu-id="90098-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="90098-115">每個模型、控制器和視圖都具有妥善定義的角色和責任，而且它們會以定義完善的方式彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="90098-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="90098-116">這有助於提升可測試性和重複使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="90098-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="90098-117">當控制器類別決定將 HTML 回應轉譯回用戶端時，它會負責將轉譯回應所需的所有資料明確地傳遞給視圖範本。</span><span class="sxs-lookup"><span data-stu-id="90098-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="90098-118">視圖範本絕對不應執行任何資料抓取或應用程式邏輯，而是改為只將呈現程式碼導向至由控制器傳遞給它的模型/資料。</span><span class="sxs-lookup"><span data-stu-id="90098-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="90098-119">現在，我們的 DinnersController 類別傳遞給我們的視圖範本的模型資料，簡單明瞭明瞭–索引（）案例中的晚餐物件清單，以及在詳細資料（）、編輯（）、建立（）和刪除（）案例中的一個晚餐物件。</span><span class="sxs-lookup"><span data-stu-id="90098-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="90098-120">當我們在應用程式中新增更多 UI 功能時，我們通常只需要傳遞這種資料，就可以在我們的視圖範本內呈現 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="90098-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="90098-121">例如，我們可能會想要將 [編輯] 和 [建立視圖] 中的 [國家/地區] 欄位變更為 dropdownlist 的 HTML 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="90098-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="90098-122">我們可能會想要以動態方式填入的支援國家/地區清單來產生該清單，而不是以硬式編碼方式在 view 範本中顯示國家/地區名稱的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="90098-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="90098-123">我們需要一種方法，將晚餐物件*和*支援的國家/地區清單，從我們的控制器傳遞至我們的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="90098-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="90098-124">讓我們看一下兩種可以完成此動作的方法。</span><span class="sxs-lookup"><span data-stu-id="90098-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="90098-125">使用 ViewData 字典</span><span class="sxs-lookup"><span data-stu-id="90098-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="90098-126">控制器基類會公開 "ViewData" 字典屬性，可用來將控制器的其他資料項目傳遞給 Views。</span><span class="sxs-lookup"><span data-stu-id="90098-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="90098-127">例如，若要支援我們想要在編輯檢視中將 [國家/地區] 文字方塊從 HTML 文字方塊變更為 dropdownlist 的案例，我們可以更新編輯（）動作方法來傳遞（除了晚餐物件） SelectList 物件，以作為 m國家/地區 dropdownlist 的 mvc。</span><span class="sxs-lookup"><span data-stu-id="90098-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="90098-128">上述 SelectList 的函式會接受用來填入下拉式 downlist 的縣市清單，以及目前選取的值。</span><span class="sxs-lookup"><span data-stu-id="90098-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="90098-129">然後，我們可以更新編輯 .aspx view 範本，以使用 DropDownList （） helper 方法，而不是我們先前使用的 Html. TextBox （） helper 方法：</span><span class="sxs-lookup"><span data-stu-id="90098-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="90098-130">上述的 DropDownList （） helper 方法會採用兩個參數。</span><span class="sxs-lookup"><span data-stu-id="90098-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="90098-131">第一個是要輸出的 HTML 表單元素名稱。</span><span class="sxs-lookup"><span data-stu-id="90098-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="90098-132">第二個是我們透過 ViewData 字典傳遞的「SelectList」模型。</span><span class="sxs-lookup"><span data-stu-id="90098-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="90098-133">我們使用C# "as" 關鍵字將字典中的類型轉換成 SelectList。</span><span class="sxs-lookup"><span data-stu-id="90098-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="90098-134">現在當我們執行應用程式並在瀏覽器中存取 */Dinners/Edit/1* URL 時，會看到編輯 UI 已更新為顯示國家/地區 dropdownlist，而不是文字方塊：</span><span class="sxs-lookup"><span data-stu-id="90098-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="90098-135">因為我們也會從 HTTP POST 編輯方法轉譯編輯檢視範本（在發生錯誤的情況下），我們會想要確定我們也會在錯誤案例中轉譯視圖範本時，更新此方法，以將 SelectList 新增至 ViewData：</span><span class="sxs-lookup"><span data-stu-id="90098-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="90098-136">現在我們的 DinnersController edit 案例支援 DropDownList。</span><span class="sxs-lookup"><span data-stu-id="90098-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="90098-137">使用 ViewModel 模式</span><span class="sxs-lookup"><span data-stu-id="90098-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="90098-138">ViewData 字典方法具有相當快速且容易執行的優點。</span><span class="sxs-lookup"><span data-stu-id="90098-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="90098-139">不過，有些開發人員不喜歡使用以字串為基礎的字典，因為輸入錯誤可能會導致不會在編譯時期攔截到的錯誤。</span><span class="sxs-lookup"><span data-stu-id="90098-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="90098-140">不具類型的 ViewData 字典也需要使用 "as" 運算子，或在使用如C# view 範本的強型別語言時進行轉換。</span><span class="sxs-lookup"><span data-stu-id="90098-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="90098-141">另一種可以使用的方法，通常稱為「ViewModel」模式。</span><span class="sxs-lookup"><span data-stu-id="90098-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="90098-142">使用此模式時，我們會建立針對我們的特定視圖案例優化的強型別類別，並針對我們的視圖範本所需的動態值/內容公開屬性。</span><span class="sxs-lookup"><span data-stu-id="90098-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="90098-143">接著，我們的控制器類別可以填入這些視圖優化的類別，並將其傳遞給我們的 view 範本來使用。</span><span class="sxs-lookup"><span data-stu-id="90098-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="90098-144">這可讓您在 [視圖] 範本內進行型別安全、編譯時間檢查和編輯器 intellisense。</span><span class="sxs-lookup"><span data-stu-id="90098-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="90098-145">例如，若要啟用晚餐表單編輯案例，我們可以建立如下所示的 "DinnerFormViewModel" 類別，它會公開兩個強型別屬性：晚餐物件，以及填入國家（地區） dropdownlist 所需的 SelectList 模型：</span><span class="sxs-lookup"><span data-stu-id="90098-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="90098-146">然後，我們可以更新編輯（）動作方法，以使用我們從存放庫中抓取的晚餐物件來建立 DinnerFormViewModel，然後將它傳遞至我們的 view 範本：</span><span class="sxs-lookup"><span data-stu-id="90098-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="90098-147">接著，我們會更新我們的 view 範本，使其預期會有 "DinnerFormViewModel" 而不是 "晚餐" 物件，方法是變更編輯 .aspx 頁面頂端的 "inherits" 屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="90098-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="90098-148">這麼做之後，我們會更新 view 範本內 "Model" 屬性的 intellisense，以反映我們傳遞它的 DinnerFormViewModel 類型的物件模型：</span><span class="sxs-lookup"><span data-stu-id="90098-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="90098-149">然後，我們就可以更新我們的 view 程式碼，使其無法使用。</span><span class="sxs-lookup"><span data-stu-id="90098-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="90098-150">請注意，我們不會變更我們所建立之輸入元素的名稱（表單元素仍然會命名為「標題」、「國家/地區」），但我們正在更新 HTML Helper 方法，以使用 DinnerFormViewModel 類別來抓取值：</span><span class="sxs-lookup"><span data-stu-id="90098-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="90098-151">我們也會在轉譯錯誤時，更新我們的編輯 post 方法以使用 DinnerFormViewModel 類別：</span><span class="sxs-lookup"><span data-stu-id="90098-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="90098-152">我們也可以更新我們的 Create （）動作方法，以重複使用完全相同的*DinnerFormViewModel*類別，以啟用其中的國家/地區 DropDownList。</span><span class="sxs-lookup"><span data-stu-id="90098-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="90098-153">以下是 HTTP GET 執行：</span><span class="sxs-lookup"><span data-stu-id="90098-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="90098-154">以下是 HTTP POST 建立方法的執行：</span><span class="sxs-lookup"><span data-stu-id="90098-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="90098-155">現在，我們的編輯和建立畫面都支援下拉式 downlists 來挑選國家/地區。</span><span class="sxs-lookup"><span data-stu-id="90098-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="90098-156">自訂形狀的 ViewModel 類別</span><span class="sxs-lookup"><span data-stu-id="90098-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="90098-157">在上述案例中，我們的 DinnerFormViewModel 類別會直接將晚餐模型物件公開為屬性，以及支援的 SelectList 模型屬性。</span><span class="sxs-lookup"><span data-stu-id="90098-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="90098-158">當我們想要在我們的視圖範本內建立的 HTML UI 相對於我們的領域模型物件時，這種方法會正常運作。</span><span class="sxs-lookup"><span data-stu-id="90098-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="90098-159">針對不是這種情況的情況，您可以使用的一個選項是建立自訂形狀的 ViewModel 類別，其物件模型較適合供視圖取用，而且看起來可能與基礎領域模型物件完全不同。</span><span class="sxs-lookup"><span data-stu-id="90098-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="90098-160">例如，它可能會公開從多個模型物件收集而來的不同屬性名稱和/或匯總屬性。</span><span class="sxs-lookup"><span data-stu-id="90098-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="90098-161">自訂形狀的 ViewModel 類別可以用來將控制器的資料傳遞給 views 來呈現，以及協助處理回傳至控制器動作方法的表單資料。</span><span class="sxs-lookup"><span data-stu-id="90098-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="90098-162">在此稍後的案例中，您可能會有動作方法以表單張貼的資料更新 ViewModel 物件，然後使用 ViewModel 實例來對應或取出實際的領域模型物件。</span><span class="sxs-lookup"><span data-stu-id="90098-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="90098-163">自訂形狀的 ViewModel 類別可以提供很大的彈性，而且是在您發現視圖範本內的轉譯程式碼，或動作方法內的表單張貼程式碼開始變得太複雜時，要調查的一些專案。</span><span class="sxs-lookup"><span data-stu-id="90098-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="90098-164">這通常是您的網域模型不會完全對應至您所產生之 UI 的正負號，而中繼自訂形狀的 ViewModel 類別可以提供協助。</span><span class="sxs-lookup"><span data-stu-id="90098-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="90098-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90098-165">Next Step</span></span>

<span data-ttu-id="90098-166">現在讓我們看看如何使用部分和主版頁面，在整個應用程式中重複使用和共用 UI。</span><span class="sxs-lookup"><span data-stu-id="90098-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="90098-167">[上一頁](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一頁](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="90098-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
