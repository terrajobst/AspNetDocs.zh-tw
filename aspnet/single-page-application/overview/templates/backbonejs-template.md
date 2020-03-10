---
uid: single-page-application/overview/templates/backbonejs-template
title: 骨幹範本 |Microsoft Docs
author: madskristensen
description: 骨幹 SPA 範本
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558223"
---
# <a name="backbone-template"></a><span data-ttu-id="9c54b-103">Backbone 範本</span><span class="sxs-lookup"><span data-stu-id="9c54b-103">Backbone Template</span></span>

<span data-ttu-id="9c54b-104">依[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="9c54b-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="9c54b-105">骨幹 SPA 範本是由 Kazi Manzur Rashid 所撰寫</span><span class="sxs-lookup"><span data-stu-id="9c54b-105">The Backbone SPA Template was written by Kazi Manzur Rashid</span></span>
> 
> [<span data-ttu-id="9c54b-106">下載骨幹 SPA 範本</span><span class="sxs-lookup"><span data-stu-id="9c54b-106">Download the Backbone.js SPA Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=293631)

<span data-ttu-id="9c54b-107">骨幹 SPA 範本的設計目的是讓您快速開始使用骨幹來建立互動式用戶端 web 應用程式[。](http://backbonejs.org/)</span><span class="sxs-lookup"><span data-stu-id="9c54b-107">The Backbone.js SPA template is designed to get you started quickly building interactive client-side web apps using [Backbone.js.](http://backbonejs.org/)</span></span>

<span data-ttu-id="9c54b-108">範本提供在 ASP.NET MVC 中開發骨幹應用程式的初始基本架構。</span><span class="sxs-lookup"><span data-stu-id="9c54b-108">The template provides an initial skeleton for developing a Backbone.js application in ASP.NET MVC.</span></span> <span data-ttu-id="9c54b-109">它提供基本的使用者登入功能，包括使用者註冊、登入、密碼重設，以及使用基本電子郵件範本的使用者確認。</span><span class="sxs-lookup"><span data-stu-id="9c54b-109">Out of the box it provides basic user login functionality, including user sign-up, sign-in, password reset, and user confirmation with basic email templates.</span></span>

<span data-ttu-id="9c54b-110">需求：</span><span class="sxs-lookup"><span data-stu-id="9c54b-110">Requirements:</span></span>

- [<span data-ttu-id="9c54b-111">ASP.NET 和 Web 工具2012.2 更新</span><span class="sxs-lookup"><span data-stu-id="9c54b-111">ASP.NET and Web Tools 2012.2 update</span></span>](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a><span data-ttu-id="9c54b-112">建立骨幹範本專案</span><span class="sxs-lookup"><span data-stu-id="9c54b-112">Create a Backbone Template Project</span></span>

<span data-ttu-id="9c54b-113">按一下上方的 [下載] 按鈕，以下載並安裝範本。</span><span class="sxs-lookup"><span data-stu-id="9c54b-113">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="9c54b-114">此範本會封裝為 Visual Studio 擴充功能（VSIX）檔案。</span><span class="sxs-lookup"><span data-stu-id="9c54b-114">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="9c54b-115">您可能需要重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9c54b-115">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="9c54b-116">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="9c54b-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="9c54b-117">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="9c54b-117">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="9c54b-118">在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="9c54b-118">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="9c54b-119">為專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9c54b-119">Name the project and click **OK**.</span></span>

![](backbonejs-template/_static/image1.png)

<span data-ttu-id="9c54b-120">在 [**新增專案**] 中，選取 [骨幹 SPA 專案]。</span><span class="sxs-lookup"><span data-stu-id="9c54b-120">In the **New Project** wizard, select Backbone.js SPA Project.</span></span>

![](backbonejs-template/_static/image2.png)

<span data-ttu-id="9c54b-121">按下 Ctrl-F5 以建立並執行應用程式，而不進行任何偵測，或按 F5 執行以進行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="9c54b-121">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](backbonejs-template/_static/image3.png)

<span data-ttu-id="9c54b-122">按一下 [我的帳戶] 就會顯示登入頁面：</span><span class="sxs-lookup"><span data-stu-id="9c54b-122">Clicking "My Account" brings up the login page:</span></span>

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a><span data-ttu-id="9c54b-123">逐步解說：用戶端程式代碼</span><span class="sxs-lookup"><span data-stu-id="9c54b-123">Walkthrough: Client Code</span></span>

<span data-ttu-id="9c54b-124">讓我們從用戶端開始。</span><span class="sxs-lookup"><span data-stu-id="9c54b-124">Let's starts with the client side.</span></span> <span data-ttu-id="9c54b-125">用戶端應用程式腳本位於 ~/Scripts/application 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9c54b-125">The client application scripts are located in the ~/Scripts/application folder.</span></span> <span data-ttu-id="9c54b-126">應用程式是以[TypeScript](http://www.typescriptlang.org/) （. ts 檔案）撰寫，並編譯成 JavaScript （.js 檔案）。</span><span class="sxs-lookup"><span data-stu-id="9c54b-126">The application is written in [TypeScript](http://www.typescriptlang.org/) (.ts files) which are compiled into JavaScript (.js files).</span></span>

<span data-ttu-id="9c54b-127">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="9c54b-127">**Application**</span></span>

<span data-ttu-id="9c54b-128">`Application` 是在 application. ts 中定義。</span><span class="sxs-lookup"><span data-stu-id="9c54b-128">`Application` is defined in application.ts.</span></span> <span data-ttu-id="9c54b-129">此物件會初始化應用程式，並作為根命名空間。</span><span class="sxs-lookup"><span data-stu-id="9c54b-129">This object initializes the application and acts as the root namespace.</span></span> <span data-ttu-id="9c54b-130">它會維護應用程式間共用的設定和狀態資訊，例如使用者是否已登入。</span><span class="sxs-lookup"><span data-stu-id="9c54b-130">It maintains configuration and state information that is shared across the application, such as whether the user is signed in.</span></span>

<span data-ttu-id="9c54b-131">`application.start` 方法會建立強制回應視圖，並附加應用層級事件的事件處理常式，例如使用者登入。</span><span class="sxs-lookup"><span data-stu-id="9c54b-131">The `application.start` method creates the modal views and attaches event handlers for application-level events, such as user sign-in.</span></span> <span data-ttu-id="9c54b-132">接下來，它會建立預設路由器，並檢查是否已指定任何用戶端 URL。</span><span class="sxs-lookup"><span data-stu-id="9c54b-132">Next, it creates the default router and checks whether any client-side URL is specified.</span></span> <span data-ttu-id="9c54b-133">如果不是，它會重新導向至預設 url （#！/）。</span><span class="sxs-lookup"><span data-stu-id="9c54b-133">If not, it redirects to the default url (#!/).</span></span>

<span data-ttu-id="9c54b-134">**事件**</span><span class="sxs-lookup"><span data-stu-id="9c54b-134">**Events**</span></span>

<span data-ttu-id="9c54b-135">開發鬆散結合的元件時，事件一律很重要。</span><span class="sxs-lookup"><span data-stu-id="9c54b-135">Events are always important when developing loosely coupled components.</span></span> <span data-ttu-id="9c54b-136">應用程式通常會執行多個作業，以回應使用者動作。</span><span class="sxs-lookup"><span data-stu-id="9c54b-136">Applications often perform multiple operations in response to a user action.</span></span> <span data-ttu-id="9c54b-137">骨幹提供內建的事件，包括模型、集合和 View 等元件。</span><span class="sxs-lookup"><span data-stu-id="9c54b-137">Backbone provides built-in events with components such as Model, Collection, and View.</span></span> <span data-ttu-id="9c54b-138">範本會使用「pub/sub」模型，而不是建立這些元件之間的相依性，而是在事件中定義的 `events` 物件，做為用於發佈和訂閱應用程式事件的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9c54b-138">Instead of creating inter-dependencies among these components, the template uses a "pub/sub" model: The `events` object, defined in events.ts, acts as an event hub for publishing and subscribing to application events.</span></span> <span data-ttu-id="9c54b-139">`events` 物件是單一的。</span><span class="sxs-lookup"><span data-stu-id="9c54b-139">The `events` object is a singleton.</span></span> <span data-ttu-id="9c54b-140">下列程式碼顯示如何訂閱事件，然後觸發事件：</span><span class="sxs-lookup"><span data-stu-id="9c54b-140">The following code shows how to subscribe to an event and then trigger the event:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

<span data-ttu-id="9c54b-141">**傳送**</span><span class="sxs-lookup"><span data-stu-id="9c54b-141">**Router**</span></span>

<span data-ttu-id="9c54b-142">在骨幹中，路由器會提供方法來路由傳送用戶端頁面，並將它們連接到動作和事件。</span><span class="sxs-lookup"><span data-stu-id="9c54b-142">In Backbone.js, a router provides methods for routing client-side pages and connecting them to actions and events.</span></span> <span data-ttu-id="9c54b-143">此範本會在 [ts] 中定義單一路由器。</span><span class="sxs-lookup"><span data-stu-id="9c54b-143">The template defines a single router, in router.ts.</span></span> <span data-ttu-id="9c54b-144">路由器會建立 activable views，並在切換 views 時維持狀態。</span><span class="sxs-lookup"><span data-stu-id="9c54b-144">The router creates the activable views and maintains the state when switching views.</span></span> <span data-ttu-id="9c54b-145">（Activable views 會在下一節中說明）。一開始，專案有兩個虛擬視圖： Home 和 About。</span><span class="sxs-lookup"><span data-stu-id="9c54b-145">(Activable views are described in the next section.) Initially, the project has two dummy views, Home and About.</span></span> <span data-ttu-id="9c54b-146">它也有一個 [NotFound] 視圖，如果路由不是已知的，就會顯示此畫面。</span><span class="sxs-lookup"><span data-stu-id="9c54b-146">It also has a NotFound view, which is displayed if the route is not known.</span></span>

<span data-ttu-id="9c54b-147">**檢視**</span><span class="sxs-lookup"><span data-stu-id="9c54b-147">**Views**</span></span>

<span data-ttu-id="9c54b-148">這些觀點定義于 ~/Scripts/application/views。</span><span class="sxs-lookup"><span data-stu-id="9c54b-148">The views are defined in ~/Scripts/application/views.</span></span> <span data-ttu-id="9c54b-149">有兩種類型的視圖： activable views 和強制回應對話方塊視圖。</span><span class="sxs-lookup"><span data-stu-id="9c54b-149">There are two kinds of views, activable views and modal dialog views.</span></span> <span data-ttu-id="9c54b-150">Activable views 是由路由器叫用。</span><span class="sxs-lookup"><span data-stu-id="9c54b-150">Activable views are invoked by the router.</span></span> <span data-ttu-id="9c54b-151">顯示 activable 視圖時，所有其他 activable 視圖都會變成非作用中。</span><span class="sxs-lookup"><span data-stu-id="9c54b-151">When an activable view is shown, all other activable views become inactive.</span></span> <span data-ttu-id="9c54b-152">若要建立 activable 視圖，請使用 `Activable` 物件來擴充此視圖：</span><span class="sxs-lookup"><span data-stu-id="9c54b-152">To create an activable view, extend the view with the `Activable` object:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

<span data-ttu-id="9c54b-153">以 `Activable` 擴充會在視圖中加入兩個新的方法，`activate` 和 `deactivate`。</span><span class="sxs-lookup"><span data-stu-id="9c54b-153">Extending with `Activable` adds two new methods to the view, `activate` and `deactivate`.</span></span> <span data-ttu-id="9c54b-154">路由器會呼叫這些方法來啟動和停用此視圖。</span><span class="sxs-lookup"><span data-stu-id="9c54b-154">The router calls these methods to activate and deactive the view.</span></span>

<span data-ttu-id="9c54b-155">強制回應視圖會實作為[Twitter 啟動](https://twitter.github.com/bootstrap/)程式強制回應對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9c54b-155">Modal views are implemented as [Twitter Bootstrap](https://twitter.github.com/bootstrap/) modal dialogs.</span></span> <span data-ttu-id="9c54b-156">[`Membership`] 和 [`Profile`] 視圖是強制回應的視圖。</span><span class="sxs-lookup"><span data-stu-id="9c54b-156">The `Membership` and `Profile` views are modal views.</span></span> <span data-ttu-id="9c54b-157">模型視圖可以由任何應用程式事件叫用。</span><span class="sxs-lookup"><span data-stu-id="9c54b-157">Model views can be invoked by any application events.</span></span> <span data-ttu-id="9c54b-158">例如，在 [`Navigation`] 視圖中，按一下 [我的帳戶] 連結會顯示 [`Membership` 視圖] 或 [`Profile`] 視圖，視使用者是否登入而定。</span><span class="sxs-lookup"><span data-stu-id="9c54b-158">For example, in the `Navigation` view, clicking the "My Account" link shows either the `Membership` view or the `Profile` view, depending on whether the user is logged in.</span></span> <span data-ttu-id="9c54b-159">`Navigation` 會將 click 事件處理常式附加至任何具有 `data-command` 屬性的子專案。</span><span class="sxs-lookup"><span data-stu-id="9c54b-159">The `Navigation` attaches click event handlers to any child elements that have the `data-command` attribute.</span></span> <span data-ttu-id="9c54b-160">以下是 HTML 標籤：</span><span class="sxs-lookup"><span data-stu-id="9c54b-160">Here is the HTML markup:</span></span>

[!code-html[Main](backbonejs-template/samples/sample3.html)]

<span data-ttu-id="9c54b-161">以下是導覽. ts 中的程式碼，用來連結事件：</span><span class="sxs-lookup"><span data-stu-id="9c54b-161">Here is the code in navigation.ts to hook up the events:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

<span data-ttu-id="9c54b-162">**模型**</span><span class="sxs-lookup"><span data-stu-id="9c54b-162">**Models**</span></span>

<span data-ttu-id="9c54b-163">模型定義于 ~/Scripts/application/models。</span><span class="sxs-lookup"><span data-stu-id="9c54b-163">The models are defined in ~/Scripts/application/models.</span></span> <span data-ttu-id="9c54b-164">這些模型都有三個基本事項：預設屬性、驗證規則和伺服器端端點。</span><span class="sxs-lookup"><span data-stu-id="9c54b-164">The models all have three basic things: default attributes, validation rules, and a server-side end point.</span></span> <span data-ttu-id="9c54b-165">以下是典型的範例：</span><span class="sxs-lookup"><span data-stu-id="9c54b-165">Here is a typical example:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

<span data-ttu-id="9c54b-166">**外掛程式**</span><span class="sxs-lookup"><span data-stu-id="9c54b-166">**Plug-ins**</span></span>

<span data-ttu-id="9c54b-167">~/Scripts/application/lib 資料夾包含幾個方便使用的 jQuery 外掛程式. Ts 檔案會定義用來處理表單資料的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="9c54b-167">The ~/Scripts/application/lib folder contains a few handy jQuery plug-ins. The form.ts file defines a plug-in for working with form data.</span></span> <span data-ttu-id="9c54b-168">您通常需要序列化或還原序列化表單資料，並顯示任何模型驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c54b-168">Often you need to serialize or deserialize form data and show any model validation errors.</span></span> <span data-ttu-id="9c54b-169">Ts 外掛程式的形式包括 `serializeFields`、`deserializeFields`和 `showFieldErrors`等方法。</span><span class="sxs-lookup"><span data-stu-id="9c54b-169">The form.ts plug-in has methods such as `serializeFields`, `deserializeFields`, and `showFieldErrors`.</span></span> <span data-ttu-id="9c54b-170">下列範例示範如何將表單序列化為模型。</span><span class="sxs-lookup"><span data-stu-id="9c54b-170">The following example shows how to serialize a form to a model.</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

<span data-ttu-id="9c54b-171">Flashbar 可為使用者提供各種類型的意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="9c54b-171">The flashbar.ts plug-in gives various kinds of feedback messages to the user.</span></span> <span data-ttu-id="9c54b-172">這些方法是 `$.showSuccessbar`、`$.showErrorbar` 和 `$.showInfobar`。</span><span class="sxs-lookup"><span data-stu-id="9c54b-172">The methods are `$.showSuccessbar`, `$.showErrorbar` and `$.showInfobar`.</span></span> <span data-ttu-id="9c54b-173">在幕後，它會使用 Twitter 啟動程式警示來顯示美觀的動畫訊息。</span><span class="sxs-lookup"><span data-stu-id="9c54b-173">Behind the scenes, it uses Twitter Bootstrap alerts to show nicely animated messages.</span></span>

<span data-ttu-id="9c54b-174">不過，如果 API 有點不同，則 confirm 外掛程式會取代瀏覽器的 [確認] 對話方塊：</span><span class="sxs-lookup"><span data-stu-id="9c54b-174">The confirm.ts plug-in replaces the browser's confirm dialog, although the API is somewhat different:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a><span data-ttu-id="9c54b-175">逐步解說：伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="9c54b-175">Walkthrough: Server Code</span></span>

<span data-ttu-id="9c54b-176">現在讓我們來看一下伺服器端。</span><span class="sxs-lookup"><span data-stu-id="9c54b-176">Now let's look at the server side.</span></span>

<span data-ttu-id="9c54b-177">**控制器**</span><span class="sxs-lookup"><span data-stu-id="9c54b-177">**Controllers**</span></span>

<span data-ttu-id="9c54b-178">在單一頁面應用程式中，伺服器只會在使用者介面中播放小型角色。</span><span class="sxs-lookup"><span data-stu-id="9c54b-178">In a single page application, the server plays only a small role in the user interface.</span></span> <span data-ttu-id="9c54b-179">一般來說，伺服器會轉譯初始頁面，然後傳送和接收 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="9c54b-179">Typically, the server renders the initial page and then sends and receives JSON data.</span></span>

<span data-ttu-id="9c54b-180">範本有兩個 MVC 控制器： `HomeController` 會轉譯初始頁面，而 `SupportsController` 則用來確認新的使用者帳戶及重設密碼。</span><span class="sxs-lookup"><span data-stu-id="9c54b-180">The template has two MVC controllers: `HomeController` renders the initial page, and `SupportsController` is used to confirm new user accounts and reset passwords.</span></span> <span data-ttu-id="9c54b-181">範本中的其他所有控制器都是 ASP.NET Web API 控制器，其會傳送和接收 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="9c54b-181">All other controllers in the template are ASP.NET Web API controllers, which send and receive JSON data.</span></span> <span data-ttu-id="9c54b-182">根據預設，控制器會使用新的 `WebSecurity` 類別來執行使用者相關的工作。</span><span class="sxs-lookup"><span data-stu-id="9c54b-182">By default, the controllers use the new `WebSecurity` class to perform user-related tasks.</span></span> <span data-ttu-id="9c54b-183">不過，它們也有選擇性的函式，可讓您傳入委派以進行這些工作。</span><span class="sxs-lookup"><span data-stu-id="9c54b-183">However, they also have optional constructors that let you pass in delegates for these tasks.</span></span> <span data-ttu-id="9c54b-184">這可讓測試更容易，並可讓您使用 IoC 容器來取代 `WebSecurity` 的其他專案。</span><span class="sxs-lookup"><span data-stu-id="9c54b-184">This makes testing easier, and lets you replace `WebSecurity` with something else, by using an IoC Container.</span></span> <span data-ttu-id="9c54b-185">請看以下範例：</span><span class="sxs-lookup"><span data-stu-id="9c54b-185">Here is an example:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a><span data-ttu-id="9c54b-186">檢視</span><span class="sxs-lookup"><span data-stu-id="9c54b-186">Views</span></span>

<span data-ttu-id="9c54b-187">這些觀點設計為模組化：網頁的每個區段都有自己專屬的視圖。</span><span class="sxs-lookup"><span data-stu-id="9c54b-187">The views are designed to be modular: Each section of a page has its own dedicated view.</span></span> <span data-ttu-id="9c54b-188">在單一頁面應用程式中，通常會包含沒有任何對應控制器的視圖。</span><span class="sxs-lookup"><span data-stu-id="9c54b-188">In a single page application, it is common to include views that do not have any corresponding controller.</span></span> <span data-ttu-id="9c54b-189">您可以藉由呼叫 `@Html.Partial('myView')`來包含視圖，但這會變得繁瑣。</span><span class="sxs-lookup"><span data-stu-id="9c54b-189">You can include a view by calling `@Html.Partial('myView')`, but this gets tedious.</span></span> <span data-ttu-id="9c54b-190">為了簡化這項作業，範本會定義 helper 方法（`IncludeClientViews`），以呈現指定資料夾中的所有視圖：</span><span class="sxs-lookup"><span data-stu-id="9c54b-190">To make this easier, the template defines a helper method, `IncludeClientViews`, that renders all of the views in a specified folder:</span></span>

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

<span data-ttu-id="9c54b-191">如果未指定資料夾名稱，預設的資料夾名稱會是 "ClientViews"。</span><span class="sxs-lookup"><span data-stu-id="9c54b-191">If the folder name is not specified, the default folder name is "ClientViews".</span></span> <span data-ttu-id="9c54b-192">如果您的用戶端視圖也使用部分視圖，請使用底線字元（例如 `_SignUp`）來命名部分視圖。</span><span class="sxs-lookup"><span data-stu-id="9c54b-192">If your client view also uses partial views, name the partial view with an underscore character (for example, `_SignUp`).</span></span> <span data-ttu-id="9c54b-193">`IncludeClientViews` 方法會排除名稱以底線開頭的任何 views。</span><span class="sxs-lookup"><span data-stu-id="9c54b-193">The `IncludeClientViews` method excludes any views whose name starts with an underscore.</span></span> <span data-ttu-id="9c54b-194">若要在用戶端視圖中包含部分視圖，請呼叫 `Html.ClientView('SignUp')`，而不是 `Html.Partial('_SignUp')`。</span><span class="sxs-lookup"><span data-stu-id="9c54b-194">To include a partial view in the client view, call `Html.ClientView('SignUp')` instead of `Html.Partial('_SignUp')`.</span></span>

<span data-ttu-id="9c54b-195">**傳送電子郵件**</span><span class="sxs-lookup"><span data-stu-id="9c54b-195">**Sending Email**</span></span>

<span data-ttu-id="9c54b-196">若要傳送電子郵件，範本會使用 [[郵遞區號](http://aboutcode.net/postal)]。</span><span class="sxs-lookup"><span data-stu-id="9c54b-196">To send email, the template uses [Postal](http://aboutcode.net/postal).</span></span> <span data-ttu-id="9c54b-197">不過，郵遞區號會從程式碼的其餘部分抽象化 `IMailer` 介面，因此您可以輕鬆地將它取代為另一個實作為。</span><span class="sxs-lookup"><span data-stu-id="9c54b-197">However, Postal is abstracted from the rest of the code with the `IMailer` interface, so you can easily replace it with another implementation.</span></span> <span data-ttu-id="9c54b-198">電子郵件範本位於 Views/Email 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9c54b-198">The email templates are located in the Views/Emails folder.</span></span> <span data-ttu-id="9c54b-199">寄件者的電子郵件地址是在 web.config 檔案的**appSettings**區段的 `sender.email` 機碼中指定。</span><span class="sxs-lookup"><span data-stu-id="9c54b-199">The sender's email address is specified in the web.config file, in the `sender.email` key of the **appSettings** section.</span></span> <span data-ttu-id="9c54b-200">此外，當 web.config 中的 `debug="true"` 時，應用程式不需要確認使用者電子郵件，就能加速開發工作。</span><span class="sxs-lookup"><span data-stu-id="9c54b-200">Also, when `debug="true"` in web.config, the application does not require user email confirmation, to speed up development.</span></span>

## <a name="github"></a><span data-ttu-id="9c54b-201">GitHub</span><span class="sxs-lookup"><span data-stu-id="9c54b-201">GitHub</span></span>

<span data-ttu-id="9c54b-202">您也可以在[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)上找到骨幹 SPA 範本。</span><span class="sxs-lookup"><span data-stu-id="9c54b-202">You can also find the Backbone.js SPA template on [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span></span>
