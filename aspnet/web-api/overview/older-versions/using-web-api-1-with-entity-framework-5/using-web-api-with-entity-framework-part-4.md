---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 第4部分：新增系統管理員視圖 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600006"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="b0e6f-102">第4部分：新增系統管理員視圖</span><span class="sxs-lookup"><span data-stu-id="b0e6f-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="b0e6f-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b0e6f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b0e6f-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="b0e6f-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="b0e6f-105">新增系統管理員視圖</span><span class="sxs-lookup"><span data-stu-id="b0e6f-105">Add an Admin View</span></span>

<span data-ttu-id="b0e6f-106">現在，我們會轉至用戶端，並新增可從管理控制器使用資料的頁面。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="b0e6f-107">此頁面可讓使用者將 AJAX 要求傳送至控制器，以建立、編輯或刪除產品。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="b0e6f-108">在方案總管中，展開 [控制器] 資料夾，然後開啟名為 HomeController.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="b0e6f-109">此檔案包含 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-109">This file contains an MVC controller.</span></span> <span data-ttu-id="b0e6f-110">新增名為 `Admin`的方法：</span><span class="sxs-lookup"><span data-stu-id="b0e6f-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="b0e6f-111">**HttpRouteUrl**方法會建立 WEB API 的 URI，並將其儲存在 view 包中，以便稍後進行。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="b0e6f-112">接下來，將文字游標放在 `Admin` 動作方法內，然後以滑鼠右鍵按一下並選取 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="b0e6f-113">這會顯示 [**加入視圖**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="b0e6f-114">在 [**加入視圖**] 對話方塊中，將 view 命名為 "Admin"。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="b0e6f-115">選取標示為 [**建立強型別視圖**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="b0e6f-116">在 [**模型類別**] 下，選取 [產品（ProductStore 模型）]。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="b0e6f-117">將所有其他選項保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="b0e6f-118">按一下 [**新增**]，會在 Views/Home 底下新增名為 Admin 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="b0e6f-119">開啟此檔案，並新增下列 HTML。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="b0e6f-120">此 HTML 會定義網頁的結構，但尚未啟動任何功能。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="b0e6f-121">建立 [系統管理員] 頁面的連結</span><span class="sxs-lookup"><span data-stu-id="b0e6f-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="b0e6f-122">在方案總管中，展開 [Views] 資料夾，然後展開 [共用] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="b0e6f-123">開啟名為 \_配置. cshtml 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="b0e6f-124">找出 id = "menu" 的**ul**元素，以及 Admin 視圖的動作連結：</span><span class="sxs-lookup"><span data-stu-id="b0e6f-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="b0e6f-125">在範例專案中，我做了一些其他的表面變更，例如取代「此處的標誌」字串。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="b0e6f-126">這些不會影響應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="b0e6f-127">您可以下載專案並比較檔案。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-127">You can download the project and compare the files.</span></span>

<span data-ttu-id="b0e6f-128">執行應用程式，然後按一下出現在首頁頂端的 [Admin] 連結。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="b0e6f-129">[管理] 頁面看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="b0e6f-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="b0e6f-130">目前，此頁面不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="b0e6f-131">在下一節中，我們將使用挖的 .js 來建立動態 UI。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="b0e6f-132">新增授權</span><span class="sxs-lookup"><span data-stu-id="b0e6f-132">Add Authorization</span></span>

<span data-ttu-id="b0e6f-133">流覽網站的任何人目前都可以存取 [管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="b0e6f-134">讓我們將此變更為限制系統管理員的許可權。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="b0e6f-135">首先新增「系統管理員」角色和系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="b0e6f-136">在方案總管中，展開 [篩選] 資料夾，然後開啟名為 InitializeSimpleMembershipAttribute.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="b0e6f-137">找出 `SimpleMembershipInitializer` 的函式。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="b0e6f-138">呼叫**WebSecurity. InitializeDatabaseConnection**之後，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b0e6f-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="b0e6f-139">這是新增「系統管理員」角色並為角色建立使用者的快速且正常的方式。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="b0e6f-140">在方案總管中，展開 [控制器] 資料夾，然後開啟 HomeController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="b0e6f-141">將**授權**屬性新增至 `Admin` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="b0e6f-142">開啟 AdminController.cs 檔案，並將**授權**屬性新增至整個 `AdminController` 類別。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="b0e6f-143">MVC 和 Web API 都會在不同的命名空間中定義**授權**屬性。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="b0e6f-144">MVC 會使用**AuthorizeAttribute**，而 Web API 則會使用**AuthorizeAttribute**。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>

<span data-ttu-id="b0e6f-145">現在只有系統管理員可以看到 [管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="b0e6f-146">此外，如果您將 HTTP 要求傳送至管理控制器，要求必須包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="b0e6f-147">如果不是，伺服器會傳送 HTTP 401 （未經授權）的回應。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="b0e6f-148">您可以藉由將 GET 要求傳送至 `http://localhost:*port*/api/admin`，在 Fiddler 中看到此情況。</span><span class="sxs-lookup"><span data-stu-id="b0e6f-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b0e6f-149">[上一頁](using-web-api-with-entity-framework-part-3.md)
> [下一頁](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="b0e6f-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
