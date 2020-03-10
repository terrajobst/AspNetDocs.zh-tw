---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: 建立 JavaScript 用戶端 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622343"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="7c017-102">建立 JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="7c017-102">Create the JavaScript Client</span></span>

<span data-ttu-id="7c017-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7c017-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7c017-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="7c017-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="7c017-105">在本節中，您將建立應用程式的用戶端，使用 HTML、JavaScript 和挖的[.js](http://knockoutjs.com/)程式庫。</span><span class="sxs-lookup"><span data-stu-id="7c017-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="7c017-106">我們會分階段建立用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="7c017-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="7c017-107">顯示書籍清單。</span><span class="sxs-lookup"><span data-stu-id="7c017-107">Showing a list of books.</span></span>
- <span data-ttu-id="7c017-108">顯示書籍詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7c017-108">Showing a book detail.</span></span>
- <span data-ttu-id="7c017-109">加入新書籍。</span><span class="sxs-lookup"><span data-stu-id="7c017-109">Adding a new book.</span></span>

<span data-ttu-id="7c017-110">挖的程式庫會使用 ViewModel （MVVM）模式：</span><span class="sxs-lookup"><span data-stu-id="7c017-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="7c017-111">**模型**是商業領域中的資料伺服器端標記法（在我們的案例中，也就是書籍和作者）。</span><span class="sxs-lookup"><span data-stu-id="7c017-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="7c017-112">此**視圖**為展示層（HTML）。</span><span class="sxs-lookup"><span data-stu-id="7c017-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="7c017-113">**視圖模型**是包含模型的 JavaScript 物件。</span><span class="sxs-lookup"><span data-stu-id="7c017-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="7c017-114">視圖模型是 UI 的程式碼抽象概念。</span><span class="sxs-lookup"><span data-stu-id="7c017-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="7c017-115">它不知道 HTML 標記法。</span><span class="sxs-lookup"><span data-stu-id="7c017-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="7c017-116">相反地，它代表視圖的抽象功能，例如 &quot;書籍清單&quot;。</span><span class="sxs-lookup"><span data-stu-id="7c017-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="7c017-117">此視圖會資料系結至視圖模型。</span><span class="sxs-lookup"><span data-stu-id="7c017-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="7c017-118">視圖模型的更新會自動反映在視圖中。</span><span class="sxs-lookup"><span data-stu-id="7c017-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="7c017-119">視圖模型也會從視圖取得事件，例如按一下按鈕。</span><span class="sxs-lookup"><span data-stu-id="7c017-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="7c017-120">這種方法可讓您輕鬆地變更應用程式的版面配置和 UI，因為您可以變更系結，而不需要重寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="7c017-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="7c017-121">例如，您可能會將專案清單顯示為 `<ul>`，然後在稍後將其變更為資料表。</span><span class="sxs-lookup"><span data-stu-id="7c017-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="7c017-122">新增挖的程式庫</span><span class="sxs-lookup"><span data-stu-id="7c017-122">Add the Knockout Library</span></span>

<span data-ttu-id="7c017-123">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]。</span><span class="sxs-lookup"><span data-stu-id="7c017-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="7c017-124">接著，選取 [Package Manager 主控台]。</span><span class="sxs-lookup"><span data-stu-id="7c017-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="7c017-125">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="7c017-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="7c017-126">此命令會將挖的檔案新增至 [腳本] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7c017-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="7c017-127">建立視圖模型</span><span class="sxs-lookup"><span data-stu-id="7c017-127">Create the View Model</span></span>

<span data-ttu-id="7c017-128">將名為 app.config 的 JavaScript 檔案新增至 [腳本] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7c017-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="7c017-129">（在方案總管中，以滑鼠右鍵按一下 [腳本] 資料夾，選取 [**新增**]，然後選取 [ **JavaScript**檔案]）。貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7c017-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="7c017-130">在挖式中，`observable` 類別會啟用資料系結。</span><span class="sxs-lookup"><span data-stu-id="7c017-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="7c017-131">當可觀察的內容變更時，可觀察的會通知所有的資料繫結控制項，以便自行更新。</span><span class="sxs-lookup"><span data-stu-id="7c017-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="7c017-132">（`observableArray` 類別是可*觀察*的陣列版本）。首先，我們的視圖模型有兩個可預見值：</span><span class="sxs-lookup"><span data-stu-id="7c017-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="7c017-133">`books` 包含書籍清單。</span><span class="sxs-lookup"><span data-stu-id="7c017-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="7c017-134">如果 AJAX 呼叫失敗，`error` 會包含錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7c017-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="7c017-135">`getAllBooks` 方法會進行 AJAX 呼叫，以取得書籍的清單。</span><span class="sxs-lookup"><span data-stu-id="7c017-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="7c017-136">然後它會將結果推送至 `books` 陣列。</span><span class="sxs-lookup"><span data-stu-id="7c017-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="7c017-137">`ko.applyBindings` 方法是「挖程式庫」的一部分。</span><span class="sxs-lookup"><span data-stu-id="7c017-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="7c017-138">它會採用 view 模型做為參數，並設定資料系結。</span><span class="sxs-lookup"><span data-stu-id="7c017-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="7c017-139">新增腳本配套</span><span class="sxs-lookup"><span data-stu-id="7c017-139">Add a Script Bundle</span></span>

<span data-ttu-id="7c017-140">配套是 ASP.NET 4.5 中的一項功能，可讓您輕鬆地將多個檔案結合或組合成單一檔案。</span><span class="sxs-lookup"><span data-stu-id="7c017-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="7c017-141">「配套」可減少對伺服器的要求數，進而改善頁面載入時間。</span><span class="sxs-lookup"><span data-stu-id="7c017-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="7c017-142">開啟檔案應用程式\_Start/Bundleconfig.json. cs。</span><span class="sxs-lookup"><span data-stu-id="7c017-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="7c017-143">將下列程式碼新增至 RegisterBundles 方法。</span><span class="sxs-lookup"><span data-stu-id="7c017-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="7c017-144">[上一頁](part-5.md)
> [下一頁](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="7c017-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
