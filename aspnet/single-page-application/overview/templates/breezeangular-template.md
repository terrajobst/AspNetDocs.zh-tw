---
uid: single-page-application/overview/templates/breezeangular-template
title: 輕鬆/角度範本 |Microsoft Docs
author: madskristensen
description: 輕鬆/角度單一頁面應用程式範本
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578537"
---
# <a name="breezeangular-template"></a><span data-ttu-id="1eba3-103">Breeze/Angular 範本</span><span class="sxs-lookup"><span data-stu-id="1eba3-103">Breeze/Angular template</span></span>

<span data-ttu-id="1eba3-104">依[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="1eba3-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="1eba3-105">以 Ward 鐘撰寫的輕鬆/角度 MVC 範本</span><span class="sxs-lookup"><span data-stu-id="1eba3-105">The Breeze/Angular MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="1eba3-106">下載簡單/角度 MVC 範本</span><span class="sxs-lookup"><span data-stu-id="1eba3-106">Download the Breeze/Angular MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=286437)

<span data-ttu-id="1eba3-107">[AngularJS](http://angularjs.org)是 Google 提供的開放原始碼程式庫，可用於建立單一頁面應用程式（spa）。</span><span class="sxs-lookup"><span data-stu-id="1eba3-107">[AngularJS](http://angularjs.org) is an open source library from Google for building Single Page Applications (SPAs).</span></span> <span data-ttu-id="1eba3-108">它提供資料系結、相依性插入，以及螢幕管理。</span><span class="sxs-lookup"><span data-stu-id="1eba3-108">It offers data binding, dependency injection, and screen management.</span></span> <span data-ttu-id="1eba3-109">將它與[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)、另一個用於資料模型化和資料管理的開放原始碼程式庫結合，而且您有絕佳的 HTML/JavaScript 用戶端應用程式的基本要素。</span><span class="sxs-lookup"><span data-stu-id="1eba3-109">Combine it with [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), another open source library for data modeling and data management, and you have the essential ingredients for a great HTML/JavaScript client app.</span></span>

<span data-ttu-id="1eba3-110">「輕鬆/角 SPA」範本是 ASP.NET 和 Web 工具2012.2 更新中所包含的[KNOCKOUTJS SPA 範本](../introduction/knockoutjs-template.md)的變化。</span><span class="sxs-lookup"><span data-stu-id="1eba3-110">The Breeze/Angular SPA template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="1eba3-111">如果您有 Visual Studio，就會有一個在60秒內啟動並執行的 SPA 範例。</span><span class="sxs-lookup"><span data-stu-id="1eba3-111">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

<span data-ttu-id="1eba3-112">外表，應用程式看起來與 KnockoutJS SPA 範本非常類似。</span><span class="sxs-lookup"><span data-stu-id="1eba3-112">Outwardly, the application looks the very similar to the KnockoutJS SPA template.</span></span> <span data-ttu-id="1eba3-113">但它的幕後也非常不同。</span><span class="sxs-lookup"><span data-stu-id="1eba3-113">But it's quite different under the hood.</span></span> <span data-ttu-id="1eba3-114">KnockoutJS 範本會使用挖的資料系結和原始 AJAX 來進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="1eba3-114">The KnockoutJS template uses Knockout for data binding and raw AJAX for data access.</span></span> <span data-ttu-id="1eba3-115">「簡單」/「角度」範本會使用角度來進行資料系結，並輕鬆地存取資料。</span><span class="sxs-lookup"><span data-stu-id="1eba3-115">The Breeze/Angular template uses Angular for data binding and Breeze for data access.</span></span> <span data-ttu-id="1eba3-116">這些程式庫可啟用額外的功能，包括頁面流覽和記錄。</span><span class="sxs-lookup"><span data-stu-id="1eba3-116">These libraries enable additional capabilities, including page navigation and history.</span></span>

<span data-ttu-id="1eba3-117">以下是應用程式的 [關於] 頁面：</span><span class="sxs-lookup"><span data-stu-id="1eba3-117">Here is the application's About page:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

<span data-ttu-id="1eba3-118">此頁面會在目前的使用者會話期間顯示執行中的事件記錄，包括：</span><span class="sxs-lookup"><span data-stu-id="1eba3-118">This page displays a running log of events during the current user session, including:</span></span>

- <span data-ttu-id="1eba3-119">速度.</span><span class="sxs-lookup"><span data-stu-id="1eba3-119">Paging.</span></span> <span data-ttu-id="1eba3-120">請注意，在 #2 和 #7 建立的 Todo 控制器。</span><span class="sxs-lookup"><span data-stu-id="1eba3-120">Note the Todo controller creation at #2 and #7.</span></span>
- <span data-ttu-id="1eba3-121">遠端查詢（#3）和本機快取查詢（#7）。</span><span class="sxs-lookup"><span data-stu-id="1eba3-121">Remote queries (#3) and local cache queries (#7).</span></span>
- <span data-ttu-id="1eba3-122">儲存新的（#5、#6）和修改的（#4）實體。</span><span class="sxs-lookup"><span data-stu-id="1eba3-122">Saving new (#5, #6) and modified (#4) entities.</span></span>
- <span data-ttu-id="1eba3-123">已在用戶端（#9）上驗證變更，讓使用者可以在將變更認可到資料庫之前更正錯誤。</span><span class="sxs-lookup"><span data-stu-id="1eba3-123">Changes validated on the client (#9), so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="1eba3-124">此範本中有更多的流覽功能，包括：</span><span class="sxs-lookup"><span data-stu-id="1eba3-124">There's more to explore in this template, including:</span></span>

- <span data-ttu-id="1eba3-125">動態載入 HTML 視圖範本。</span><span class="sxs-lookup"><span data-stu-id="1eba3-125">Dynamic loading of HTML view templates.</span></span>
- <span data-ttu-id="1eba3-126">透過角度「指示詞」的自訂資料系結。</span><span class="sxs-lookup"><span data-stu-id="1eba3-126">Custom data binding through Angular "directives."</span></span>
- <span data-ttu-id="1eba3-127">模組化和相依性插入。</span><span class="sxs-lookup"><span data-stu-id="1eba3-127">Modularity and dependency injection.</span></span>
- <span data-ttu-id="1eba3-128">查詢篩選、排序、分頁、投射和包含相關實體。</span><span class="sxs-lookup"><span data-stu-id="1eba3-128">Query filters, sorts, paging, projections, and inclusion of related entities.</span></span>
- <span data-ttu-id="1eba3-129">跨多個畫面共用資料。</span><span class="sxs-lookup"><span data-stu-id="1eba3-129">Sharing data across multiple screens.</span></span>
- <span data-ttu-id="1eba3-130">將多個變更儲存為單一交易。</span><span class="sxs-lookup"><span data-stu-id="1eba3-130">Saving multiple changes as a single transaction.</span></span>
- <span data-ttu-id="1eba3-131">驗證規則會自動從伺服器傳播至 JavaScript 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1eba3-131">Validation rules propagated automatically from the server to the JavaScript client.</span></span>

<span data-ttu-id="1eba3-132">我們現在就開始吧。</span><span class="sxs-lookup"><span data-stu-id="1eba3-132">Let's get started.</span></span>

## <a name="create-a-breezeangular-template-project"></a><span data-ttu-id="1eba3-133">建立輕而易舉/角度的範本專案</span><span class="sxs-lookup"><span data-stu-id="1eba3-133">Create a Breeze/Angular Template Project</span></span>

<span data-ttu-id="1eba3-134">按一下上方的 [下載] 按鈕，以下載並安裝範本。</span><span class="sxs-lookup"><span data-stu-id="1eba3-134">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="1eba3-135">此範本會封裝為 Visual Studio 擴充功能（VSIX）檔案。</span><span class="sxs-lookup"><span data-stu-id="1eba3-135">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="1eba3-136">您可能需要重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="1eba3-136">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="1eba3-137">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="1eba3-137">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="1eba3-138">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="1eba3-138">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="1eba3-139">在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="1eba3-139">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="1eba3-140">為專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1eba3-140">Name the project and click **OK**.</span></span>

<span data-ttu-id="1eba3-141">在 [**新增專案**] 中，選取 [**輕鬆角 SPA**]。</span><span class="sxs-lookup"><span data-stu-id="1eba3-141">In the **New Project** wizard, select **Breeze Angular SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

<span data-ttu-id="1eba3-142">按下 Ctrl-F5 以建立並執行應用程式，而不進行任何偵測，或按 F5 執行以進行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="1eba3-142">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

<span data-ttu-id="1eba3-143">當應用程式第一次執行時，它會顯示登入畫面。</span><span class="sxs-lookup"><span data-stu-id="1eba3-143">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="1eba3-144">按一下 [註冊] 連結和新的頁面 glides 至 [觀看]，您可以在其中輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="1eba3-144">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="1eba3-145">（登入和註冊頁面會使用 ASP.NET MVC 建立）。當您提交註冊表單時，伺服器會為您的帳戶產生包含兩個專案的 TodoList。</span><span class="sxs-lookup"><span data-stu-id="1eba3-145">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="1eba3-146">然後，它會以黃色附注呈現給您。</span><span class="sxs-lookup"><span data-stu-id="1eba3-146">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="1eba3-147">現在您已在 SPA 的土地。</span><span class="sxs-lookup"><span data-stu-id="1eba3-147">Now you are in the land of SPA.</span></span> <span data-ttu-id="1eba3-148">您在操作 Todo 時所看到及體驗的所有內容，都是在用戶端上轉譯和管理，並具有挖得的説明。</span><span class="sxs-lookup"><span data-stu-id="1eba3-148">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="1eba3-149">以使用者身分探索應用程式 。</span><span class="sxs-lookup"><span data-stu-id="1eba3-149">Explore the app as a user …</span></span> <span data-ttu-id="1eba3-150">但是有了開發人員的目光。</span><span class="sxs-lookup"><span data-stu-id="1eba3-150">but with a developer's eye.</span></span> <span data-ttu-id="1eba3-151">使用瀏覽器中的開發人員工具來捕捉網路流量。</span><span class="sxs-lookup"><span data-stu-id="1eba3-151">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="1eba3-152">（在 Internet Explorer 中：按 F12，選取 [**網路**] 索引標籤，然後按一下 [**開始捕獲**]）。現在請嘗試下列動作：</span><span class="sxs-lookup"><span data-stu-id="1eba3-152">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="1eba3-153">新增待辦事項專案。</span><span class="sxs-lookup"><span data-stu-id="1eba3-153">Add a new Todo item.</span></span>
- <span data-ttu-id="1eba3-154">按一下標籤，然後編輯待辦事項專案標題</span><span class="sxs-lookup"><span data-stu-id="1eba3-154">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="1eba3-155">核取核取方塊，將專案標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="1eba3-155">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="1eba3-156">請注意，textbox 已停用，因此標題已無法再編輯。</span><span class="sxs-lookup"><span data-stu-id="1eba3-156">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="1eba3-157">按一下標籤右邊的 [x]。</span><span class="sxs-lookup"><span data-stu-id="1eba3-157">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="1eba3-158">專案會消失，並從資料庫中刪除。</span><span class="sxs-lookup"><span data-stu-id="1eba3-158">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="1eba3-159">挑選另一個專案並清除其標題。</span><span class="sxs-lookup"><span data-stu-id="1eba3-159">Pick another item and clear its title.</span></span> <span data-ttu-id="1eba3-160">您會收到需要標題的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="1eba3-160">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="1eba3-161">短暫暫停之後，就會還原先前的標題。</span><span class="sxs-lookup"><span data-stu-id="1eba3-161">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="1eba3-162">輸入非常的長標題。</span><span class="sxs-lookup"><span data-stu-id="1eba3-162">Type in a ridiculously long title.</span></span> <span data-ttu-id="1eba3-163">您會收到不同的驗證錯誤，指出標題太長。</span><span class="sxs-lookup"><span data-stu-id="1eba3-163">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="1eba3-164">按一下 [新增待辦事項清單] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1eba3-164">Click the "Add Todo List" button.</span></span> <span data-ttu-id="1eba3-165">新的清單就會出現在先前清單的左邊。</span><span class="sxs-lookup"><span data-stu-id="1eba3-165">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="1eba3-166">播放 TodoList 標題，觸發其必要和長度驗證。</span><span class="sxs-lookup"><span data-stu-id="1eba3-166">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="1eba3-167">按一下 [標題] 文字方塊，以清除錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="1eba3-167">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="1eba3-168">按一下右上角圓形中的 "x"，以刪除 TodoList 及其 todo。</span><span class="sxs-lookup"><span data-stu-id="1eba3-168">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>
- <span data-ttu-id="1eba3-169">按一下右上方的 [關於] 連結，以查看這些活動的記錄。</span><span class="sxs-lookup"><span data-stu-id="1eba3-169">Click the "About" link in the upper right to see a log of these activities.</span></span>

<span data-ttu-id="1eba3-170">驗證邏輯會輕鬆地在用戶端執行。</span><span class="sxs-lookup"><span data-stu-id="1eba3-170">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="1eba3-171">伺服器模型類別上的驗證屬性會傳播至用戶端，並在用戶端聯繫伺服器之前自動執行。</span><span class="sxs-lookup"><span data-stu-id="1eba3-171">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="1eba3-172">檢查網路流量。</span><span class="sxs-lookup"><span data-stu-id="1eba3-172">Review the network traffic.</span></span> <span data-ttu-id="1eba3-173">請注意，在簡單偵測到錯誤時，並沒有對伺服器的呼叫。</span><span class="sxs-lookup"><span data-stu-id="1eba3-173">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="1eba3-174">每個有效的變更都會導致 POST 要求「/api/Todo/SaveChanges」。</span><span class="sxs-lookup"><span data-stu-id="1eba3-174">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="1eba3-175">輕鬆地將變更組合在一起，並以單一要求傳送至 Web API 控制器的 `SaveChanges` 方法。</span><span class="sxs-lookup"><span data-stu-id="1eba3-175">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="1eba3-176">這與 KnockoutJS SPA 範本不同，它會針對每個專案個別進行 PUT、POST 和 DELETE 要求。</span><span class="sxs-lookup"><span data-stu-id="1eba3-176">That's different from KnockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

<span data-ttu-id="1eba3-177">此外，請注意，當您在 TodoList 與 About 頁面之間切換時，不會有任何網路流量。</span><span class="sxs-lookup"><span data-stu-id="1eba3-177">Also, notice there is no network traffic when you switch between the TodoList and About pages.</span></span> <span data-ttu-id="1eba3-178">這是因為查詢已限制為本機簡單快取。</span><span class="sxs-lookup"><span data-stu-id="1eba3-178">That's because the query has been constrained to the local Breeze cache.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="1eba3-179">查看內部</span><span class="sxs-lookup"><span data-stu-id="1eba3-179">Peek inside</span></span>

<span data-ttu-id="1eba3-180">此應用程式具有用戶端和伺服器端。</span><span class="sxs-lookup"><span data-stu-id="1eba3-180">This application has a client side and a server side.</span></span> <span data-ttu-id="1eba3-181">用戶端堆疊包含一些 HTML 和應用程式 JavaScript 模組（在「應用程式」資料夾中）和協力廠商 JavaScript 程式庫（在 [腳本] 資料夾中）的組合。</span><span class="sxs-lookup"><span data-stu-id="1eba3-181">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

<span data-ttu-id="1eba3-182">UI 架構會將視圖的 HTML widget 與控制器中支援的呈現程式碼區隔開。</span><span class="sxs-lookup"><span data-stu-id="1eba3-182">The UI architecture separates the HTML widgets of the views from the supporting presentation code in the controllers.</span></span> <span data-ttu-id="1eba3-183">角度資料系結系統會協調視圖和控制器，讓每個都可以執行其作業，而不需要深入瞭解另一個。</span><span class="sxs-lookup"><span data-stu-id="1eba3-183">The Angular data-binding system coordinates views and controllers so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="1eba3-184">控制器會要求資料內容取得並儲存模型實體。</span><span class="sxs-lookup"><span data-stu-id="1eba3-184">The controller asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="1eba3-185">資料內容會將大部分的工作委派給輕鬆，這會從 JSON 查詢結果中，建立自我追蹤模型物件。</span><span class="sxs-lookup"><span data-stu-id="1eba3-185">The data context delegates most of the work to Breeze, which constructs self-tracking model objects from JSON query results.</span></span>

<span data-ttu-id="1eba3-186">伺服器端堆疊包含一些開發人員程式碼和三個準則 .NET 程式庫： Web API、Entity Framework 和 Breeze.NET：</span><span class="sxs-lookup"><span data-stu-id="1eba3-186">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="1eba3-187">基本架構與 KnockoutJS SPA 範本相同。</span><span class="sxs-lookup"><span data-stu-id="1eba3-187">The basic architecture is the same as the KnockoutJS SPA template.</span></span> <span data-ttu-id="1eba3-188">不過，這種做法很簡單：已刪除 Dto，而且大部分的 Entity Framework 詳細資料都已委派給 Breeze.NET。</span><span class="sxs-lookup"><span data-stu-id="1eba3-188">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1eba3-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1eba3-189">Next Steps</span></span>

<span data-ttu-id="1eba3-190">我們建議您流覽程式碼，並在「輕鬆的」網站上深入[討論](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)用戶端和伺服器堆疊。</span><span class="sxs-lookup"><span data-stu-id="1eba3-190">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="1eba3-191">您可以嘗試使用簡單的用戶端查詢來播放;新增一些篩選準則並進行排序。</span><span class="sxs-lookup"><span data-stu-id="1eba3-191">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="1eba3-192">您可以新增更多模型屬性和更多實體，以便更容易進行端對端 SPA 的開發。</span><span class="sxs-lookup"><span data-stu-id="1eba3-192">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="1eba3-193">當您確信此設計時，您可以卸載待辦事項功能，並以您自己的方式取代它們。</span><span class="sxs-lookup"><span data-stu-id="1eba3-193">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="1eba3-194">祝各位寫程式愉快！</span><span class="sxs-lookup"><span data-stu-id="1eba3-194">Happy coding!</span></span>
