---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 範本 |Microsoft Docs
author: xqiu
description: EmberJS 範本
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578502"
---
# <a name="emberjs-template"></a><span data-ttu-id="37d69-103">EmberJS 範本</span><span class="sxs-lookup"><span data-stu-id="37d69-103">EmberJS template</span></span>

<span data-ttu-id="37d69-104">依[Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="37d69-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="37d69-105">EmberJS MVC 範本是由 Nathan Totten、Thiago Santos 和 Xinyang Qiu 所撰寫。</span><span class="sxs-lookup"><span data-stu-id="37d69-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="37d69-106">下載 EmberJS MVC 範本</span><span class="sxs-lookup"><span data-stu-id="37d69-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)

<span data-ttu-id="37d69-107">EmberJS SPA 範本的設計可讓您開始使用 EmberJS 快速建立互動式用戶端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37d69-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="37d69-108">「單頁應用程式」（SPA）是 web 應用程式的一般詞彙，它會載入單一 HTML 頁面，然後動態更新頁面，而不是載入新的頁面。</span><span class="sxs-lookup"><span data-stu-id="37d69-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="37d69-109">載入初始頁面之後，SPA 會透過 AJAX 要求與伺服器交談。</span><span class="sxs-lookup"><span data-stu-id="37d69-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="37d69-110">AJAX 是新的，但目前有 JavaScript 架構，可讓您更輕鬆地建立和維護大型的 SPA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37d69-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="37d69-111">此外，HTML 5 和 CSS3 可讓您更輕鬆地建立豐富的 Ui。</span><span class="sxs-lookup"><span data-stu-id="37d69-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="37d69-112">EmberJS SPA 範本會使用[Ember.js](http://emberjs.com/) JavaScript 程式庫來處理來自 AJAX 要求的頁面更新。</span><span class="sxs-lookup"><span data-stu-id="37d69-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="37d69-113">Ember.js 會使用資料系結來同步處理頁面與最新的資料。</span><span class="sxs-lookup"><span data-stu-id="37d69-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="37d69-114">如此一來，您就不需要撰寫任何逐步解說 JSON 資料並更新 DOM 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="37d69-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="37d69-115">相反地，您會將宣告式屬性放在 HTML 中，告訴 Ember.js 如何呈現資料。</span><span class="sxs-lookup"><span data-stu-id="37d69-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="37d69-116">在伺服器端，EmberJS 範本與[KNOCKOUTJS SPA 範本](../introduction/knockoutjs-template.md)幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="37d69-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="37d69-117">它會使用 ASP.NET MVC 來提供 HTML 檔案，並 ASP.NET Web API 來處理來自用戶端的 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="37d69-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="37d69-118">如需範本相關層面的詳細資訊，請參閱[KnockoutJS 範本](../introduction/knockoutjs-template.md)檔。</span><span class="sxs-lookup"><span data-stu-id="37d69-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="37d69-119">本主題著重于挖的範本與 EmberJS 範本之間的差異。</span><span class="sxs-lookup"><span data-stu-id="37d69-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="37d69-120">建立 EmberJS SPA 範本專案</span><span class="sxs-lookup"><span data-stu-id="37d69-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="37d69-121">按一下上方的 [下載] 按鈕，以下載並安裝範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="37d69-122">您可能需要重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="37d69-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="37d69-123">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="37d69-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="37d69-124">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="37d69-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="37d69-125">在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="37d69-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="37d69-126">為專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="37d69-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="37d69-127">在 [**新增專案**] 中，選取 [ember.js] [SPA] [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="37d69-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="37d69-128">EmberJS SPA 範本總覽</span><span class="sxs-lookup"><span data-stu-id="37d69-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="37d69-129">EmberJS 範本使用 jQuery、Ember.js、Handlebars 的組合來建立流暢的互動式 UI。</span><span class="sxs-lookup"><span data-stu-id="37d69-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="37d69-130">Ember.js 是使用用戶端 MVC 模式的 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="37d69-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="37d69-131">以 Handlebars 範本化語言撰寫的*範本*會描述應用程式使用者介面。</span><span class="sxs-lookup"><span data-stu-id="37d69-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="37d69-132">在發行模式中， [Handlebars 編譯器](https://github.com/Myslik/csharp-ember-handlebars)是用來組合和編譯 Handlebars 範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="37d69-133">*模型*會儲存從伺服器取得的應用程式資料（todo 清單和 todo 專案）。</span><span class="sxs-lookup"><span data-stu-id="37d69-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="37d69-134">*控制器*會儲存應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="37d69-134">A *controller* stores application state.</span></span> <span data-ttu-id="37d69-135">控制器通常會向對應的範本呈現模型資料。</span><span class="sxs-lookup"><span data-stu-id="37d69-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="37d69-136">「*視圖*」會從應用程式轉譯基本事件，並將它們傳遞至控制器。</span><span class="sxs-lookup"><span data-stu-id="37d69-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="37d69-137">*路由器*會管理應用程式狀態，讓 url 和範本保持同步。</span><span class="sxs-lookup"><span data-stu-id="37d69-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="37d69-138">此外，Ember.js 資料連結庫可以用來同步處理 JSON 物件（透過 RESTful API 從伺服器取得）和用戶端模型。</span><span class="sxs-lookup"><span data-stu-id="37d69-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="37d69-139">EmberJS SPA 範本會將腳本組織成八個層級：</span><span class="sxs-lookup"><span data-stu-id="37d69-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="37d69-140">webapi\_adapter、webapi\_序列化程式：擴充 Ember.js 資料連結庫以與 ASP.NET Web API 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="37d69-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="37d69-141">Scripts/helper .js：定義新的 Ember.js Handlebars helper。</span><span class="sxs-lookup"><span data-stu-id="37d69-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="37d69-142">Scripts/node.js：建立應用程式並設定介面卡和序列化程式。</span><span class="sxs-lookup"><span data-stu-id="37d69-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="37d69-143">Scripts/app/模型/\*.js：定義模型。</span><span class="sxs-lookup"><span data-stu-id="37d69-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="37d69-144">Scripts/app/views/\*.js：定義 views。</span><span class="sxs-lookup"><span data-stu-id="37d69-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="37d69-145">腳本/應用程式/控制器/\*.js：定義控制器。</span><span class="sxs-lookup"><span data-stu-id="37d69-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="37d69-146">Scripts/app/route、Scripts/app/node.js：定義路由。</span><span class="sxs-lookup"><span data-stu-id="37d69-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="37d69-147">Templates/\*. hbs：定義 handlebars 範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="37d69-148">讓我們更詳細地查看其中一些腳本。</span><span class="sxs-lookup"><span data-stu-id="37d69-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="37d69-149">模型</span><span class="sxs-lookup"><span data-stu-id="37d69-149">Models</span></span>

<span data-ttu-id="37d69-150">這些模型定義于 [腳本/應用程式/模型] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="37d69-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="37d69-151">有兩個模型檔案： todoItem 和 todoList。</span><span class="sxs-lookup"><span data-stu-id="37d69-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="37d69-152">**todo。 model .js**會定義待辦事項清單的用戶端（瀏覽器）模型。</span><span class="sxs-lookup"><span data-stu-id="37d69-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="37d69-153">有兩個模型類別： todoItem 和 todoList。</span><span class="sxs-lookup"><span data-stu-id="37d69-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="37d69-154">在 Ember.js 中，模型是 DS 的子類別。模組.</span><span class="sxs-lookup"><span data-stu-id="37d69-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="37d69-155">模型可以具有屬性（attribute）：</span><span class="sxs-lookup"><span data-stu-id="37d69-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="37d69-156">模型可以定義與其他模型的關聯性：</span><span class="sxs-lookup"><span data-stu-id="37d69-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="37d69-157">模型可以有系結至其他屬性的計算屬性：</span><span class="sxs-lookup"><span data-stu-id="37d69-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="37d69-158">模型可以具有觀察者函式，當觀察到的屬性變更時，就會叫用這些函數：</span><span class="sxs-lookup"><span data-stu-id="37d69-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="37d69-159">檢視</span><span class="sxs-lookup"><span data-stu-id="37d69-159">Views</span></span>

<span data-ttu-id="37d69-160">這些 views 會定義在 Scripts/app/views 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="37d69-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="37d69-161">「視圖」會從應用程式 UI 轉譯事件。</span><span class="sxs-lookup"><span data-stu-id="37d69-161">A view translates events from the application UI.</span></span> <span data-ttu-id="37d69-162">事件處理常式可以回呼控制器函式，或直接呼叫資料內容。</span><span class="sxs-lookup"><span data-stu-id="37d69-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="37d69-163">例如，下列程式碼來自 views/TodoItemEditView。</span><span class="sxs-lookup"><span data-stu-id="37d69-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="37d69-164">它會定義輸入文字欄位的事件處理。</span><span class="sxs-lookup"><span data-stu-id="37d69-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="37d69-165">控制器</span><span class="sxs-lookup"><span data-stu-id="37d69-165">Controller</span></span>

<span data-ttu-id="37d69-166">這些控制器定義于 [腳本/應用程式/控制器] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="37d69-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="37d69-167">若要表示單一模型，請擴充 `Ember.ObjectController`：</span><span class="sxs-lookup"><span data-stu-id="37d69-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="37d69-168">控制器也可以藉由擴充 `Ember.ArrayController`來代表模型的集合。</span><span class="sxs-lookup"><span data-stu-id="37d69-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="37d69-169">例如，Todolistcontroller.cs」代表 `todoList` 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="37d69-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="37d69-170">控制器會依 todoList 識別碼排序（以遞減順序）：</span><span class="sxs-lookup"><span data-stu-id="37d69-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="37d69-171">控制器會定義名為 `addTodoList`的函式，此函式會建立新的 todoList，並將它新增至陣列。</span><span class="sxs-lookup"><span data-stu-id="37d69-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="37d69-172">若要查看如何呼叫此函式，請在 [範本] 資料夾中開啟名為 todoListTemplate 的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="37d69-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="37d69-173">下列範本程式碼會將按鈕系結至 `addTodoList` 函式：</span><span class="sxs-lookup"><span data-stu-id="37d69-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="37d69-174">控制器也包含一個 `error` 屬性，它會保存一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="37d69-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="37d69-175">以下是用來顯示錯誤訊息的範本程式碼（也是在 todoListTemplate 中）：</span><span class="sxs-lookup"><span data-stu-id="37d69-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="37d69-176">路由</span><span class="sxs-lookup"><span data-stu-id="37d69-176">Routes</span></span>

<span data-ttu-id="37d69-177">Node.js 會定義要顯示的路由和預設範本、設定應用程式狀態，以及與路由的 Url 相符：</span><span class="sxs-lookup"><span data-stu-id="37d69-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="37d69-178">TodoListRoute 會藉由覆寫 setupController 函式來載入 TodoListRoute 的資料：</span><span class="sxs-lookup"><span data-stu-id="37d69-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="37d69-179">Ember.js 會使用命名慣例來比對 Url、路由名稱、控制器和範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="37d69-180">如需詳細資訊，請參閱 EmberJS 檔中的[http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) 。</span><span class="sxs-lookup"><span data-stu-id="37d69-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="37d69-181">範本</span><span class="sxs-lookup"><span data-stu-id="37d69-181">Templates</span></span>

<span data-ttu-id="37d69-182">Templates 資料夾包含四個範本：</span><span class="sxs-lookup"><span data-stu-id="37d69-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="37d69-183">hbs：啟動應用程式時所呈現的預設範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="37d69-184">關於 hbs： "/about" 路由的範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="37d69-185">hbs：根 "/" 路由的範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="37d69-186">todoList. hbs： "/todo" 路由的範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="37d69-187">\_hbs：範本會定義導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="37d69-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="37d69-188">應用程式範本的作用就像主版頁面。</span><span class="sxs-lookup"><span data-stu-id="37d69-188">The application template acts like a master page.</span></span> <span data-ttu-id="37d69-189">其中包含標頭、頁尾和 "{{輸出口}}"，以根據路由在中插入其他範本。</span><span class="sxs-lookup"><span data-stu-id="37d69-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="37d69-190">如需 Ember.js 中應用程式範本的詳細資訊，請參閱[http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)。</span><span class="sxs-lookup"><span data-stu-id="37d69-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="37d69-191">"/TodoList" 範本包含兩個迴圈運算式。</span><span class="sxs-lookup"><span data-stu-id="37d69-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="37d69-192">外部迴圈會 `{{#each controller}}`，且 `{{#each todos}}`內的迴圈。</span><span class="sxs-lookup"><span data-stu-id="37d69-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="37d69-193">下列程式碼顯示內建的 `Ember.Checkbox` view、自訂的 `App.TodoItemEditView`，以及具有 `deleteTodo` 動作的連結。</span><span class="sxs-lookup"><span data-stu-id="37d69-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="37d69-194">在 web.config 檔案中，當**debug**設定為**true**時，在 controller/HtmlHelperExtensions 中定義的 `HtmlHelperExtensions` 類別會定義 helper 函式來快取和插入範本檔案。</span><span class="sxs-lookup"><span data-stu-id="37d69-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="37d69-195">此函式是從 Views/Home/App.config 中定義的 ASP.NET MVC view 檔案呼叫：</span><span class="sxs-lookup"><span data-stu-id="37d69-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="37d69-196">呼叫不含引數的函式時，函式會轉譯 Templates 資料夾中的所有範本檔案。</span><span class="sxs-lookup"><span data-stu-id="37d69-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="37d69-197">您也可以指定子資料夾或特定的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="37d69-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="37d69-198">當 web.config 中的**debug**為**false**時，應用程式會包含配套專案 "~/bundles/templates"。</span><span class="sxs-lookup"><span data-stu-id="37d69-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="37d69-199">使用 Handlebars 編譯器程式庫，在 BundleConfig.cs 中新增此配套專案：</span><span class="sxs-lookup"><span data-stu-id="37d69-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
