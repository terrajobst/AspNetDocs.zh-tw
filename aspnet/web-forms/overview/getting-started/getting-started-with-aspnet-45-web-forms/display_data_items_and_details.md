---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 顯示資料項目和詳細資料 |Microsoft Docs
author: Erikre
description: 本教學課程系列將示範如何使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 建立 ASP.NET Web Forms 應用程式的基本概念
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641110"
---
# <a name="display-data-items-and-details"></a><span data-ttu-id="d0aac-103">顯示資料項目及詳細資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-103">Display data items and details</span></span>

<span data-ttu-id="d0aac-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="d0aac-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="d0aac-105">本教學課程系列會教您使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 建立 ASP.NET Web Forms 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="d0aac-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="d0aac-106">在本教學課程中，您將瞭解如何使用 ASP.NET Web Forms 和 Entity Framework Code First 來顯示資料項目和資料項目詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="d0aac-107">本教學課程是以先前的「UI 和流覽」教學課程為基礎，做為 Wingtip 玩具商店教學課程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="d0aac-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="d0aac-108">完成本教學課程之後，您會在 [ *ProductsList* ] 頁面上看到產品，以及*ProductDetails*的產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="d0aac-109">您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="d0aac-109">You'll learn how to:</span></span>

- <span data-ttu-id="d0aac-110">新增資料控制項以顯示資料庫中的產品</span><span class="sxs-lookup"><span data-stu-id="d0aac-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="d0aac-111">將資料控制項連接到選取的資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="d0aac-112">新增資料控制項，以顯示資料庫中的產品詳細資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="d0aac-113">從查詢字串抓取值，並使用該值來限制從資料庫抓取的資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="d0aac-114">本教學課程中引進的功能：</span><span class="sxs-lookup"><span data-stu-id="d0aac-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="d0aac-115">模型繫結</span><span class="sxs-lookup"><span data-stu-id="d0aac-115">Model binding</span></span>
- <span data-ttu-id="d0aac-116">值提供者</span><span class="sxs-lookup"><span data-stu-id="d0aac-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="d0aac-117">新增資料控制項</span><span class="sxs-lookup"><span data-stu-id="d0aac-117">Add a data control</span></span>

<span data-ttu-id="d0aac-118">您可以使用幾個不同的選項，將資料系結至伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="d0aac-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="d0aac-119">最常見的包括：</span><span class="sxs-lookup"><span data-stu-id="d0aac-119">The most common include:</span></span>

* <span data-ttu-id="d0aac-120">加入資料來源控制項</span><span class="sxs-lookup"><span data-stu-id="d0aac-120">Adding a data source control</span></span>
* <span data-ttu-id="d0aac-121">手動加入程式碼</span><span class="sxs-lookup"><span data-stu-id="d0aac-121">Adding code by hand</span></span>
* <span data-ttu-id="d0aac-122">使用模型系結</span><span class="sxs-lookup"><span data-stu-id="d0aac-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="d0aac-123">使用資料來源控制項來系結資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-123">Use a data source control to bind data</span></span>

<span data-ttu-id="d0aac-124">加入資料來源控制項可讓您將資料來源控制項連結至顯示資料的控制項。</span><span class="sxs-lookup"><span data-stu-id="d0aac-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="d0aac-125">透過這種方法，您可以用宣告方式（而不是以程式設計方式）將伺服器端控制項連接到資料來源。</span><span class="sxs-lookup"><span data-stu-id="d0aac-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="d0aac-126">手動撰寫程式碼以系結資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-126">Code by hand to bind data</span></span>

<span data-ttu-id="d0aac-127">手動撰寫程式碼包含：</span><span class="sxs-lookup"><span data-stu-id="d0aac-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="d0aac-128">讀取值</span><span class="sxs-lookup"><span data-stu-id="d0aac-128">Reading a value</span></span>
2. <span data-ttu-id="d0aac-129">檢查其是否為 null</span><span class="sxs-lookup"><span data-stu-id="d0aac-129">Checking if it's null</span></span>
3. <span data-ttu-id="d0aac-130">將它轉換成適當的類型</span><span class="sxs-lookup"><span data-stu-id="d0aac-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="d0aac-131">檢查轉換成功</span><span class="sxs-lookup"><span data-stu-id="d0aac-131">Checking conversion success</span></span>
5. <span data-ttu-id="d0aac-132">使用查詢中的值</span><span class="sxs-lookup"><span data-stu-id="d0aac-132">Using the value in the query</span></span> 

<span data-ttu-id="d0aac-133">這種方法可讓您完全掌控您的資料存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="d0aac-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="d0aac-134">使用模型系結來系結資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-134">Use model binding to bind data</span></span>

<span data-ttu-id="d0aac-135">模型系結可讓您以較少的程式碼來系結結果，並讓您能夠在整個應用程式中重複使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d0aac-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="d0aac-136">它可簡化使用以程式碼為主的資料存取邏輯，同時仍然提供豐富的資料系結架構。</span><span class="sxs-lookup"><span data-stu-id="d0aac-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="d0aac-137">顯示產品</span><span class="sxs-lookup"><span data-stu-id="d0aac-137">Display products</span></span>

<span data-ttu-id="d0aac-138">在本教學課程中，您將使用模型系結來系結資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="d0aac-139">若要將資料控制項設定為使用模型系結來選取資料，請將控制項的 `SelectMethod` 屬性設為頁面程式碼中的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="d0aac-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="d0aac-140">資料控制項會在頁面生命週期的適當時間呼叫方法，並自動系結傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="d0aac-141">不需要明確地呼叫 `DataBind` 方法。</span><span class="sxs-lookup"><span data-stu-id="d0aac-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="d0aac-142">在**方案總管**中，開啟*ProductList。*</span><span class="sxs-lookup"><span data-stu-id="d0aac-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="d0aac-143">以下列標記取代現有標記：</span><span class="sxs-lookup"><span data-stu-id="d0aac-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="d0aac-144">此程式碼會使用名為 `productList` 的**ListView**控制項來顯示產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="d0aac-145">使用範本和樣式，您可以定義**ListView**控制項顯示資料的方式。</span><span class="sxs-lookup"><span data-stu-id="d0aac-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="d0aac-146">這適用于任何重複結構中的資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="d0aac-147">雖然此**ListView**範例只會顯示資料庫資料，但您也可以不使用程式碼，讓使用者編輯、插入和刪除資料，以及排序和分頁資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="d0aac-148">藉由設定**ListView**控制項中的 [`ItemType`] 屬性，就可以使用資料系結運算式 `Item`，而且控制項會成為強型別。</span><span class="sxs-lookup"><span data-stu-id="d0aac-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="d0aac-149">如先前的教學課程中所述，您可以使用 IntelliSense 選取專案物件詳細資料，例如指定 `ProductName`：</span><span class="sxs-lookup"><span data-stu-id="d0aac-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![顯示資料項目和詳細資料-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="d0aac-151">您也會使用模型系結來指定 `SelectMethod` 值。</span><span class="sxs-lookup"><span data-stu-id="d0aac-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="d0aac-152">這個值（`GetProducts`）會對應至您要新增至程式碼後置的方法，以在下一個步驟中顯示產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="d0aac-153">新增程式碼以顯示產品</span><span class="sxs-lookup"><span data-stu-id="d0aac-153">Add code to display products</span></span>

<span data-ttu-id="d0aac-154">在此步驟中，您將新增程式碼，以在**ListView**控制項中填入資料庫的產品資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="d0aac-155">此程式碼支援顯示所有產品和個別類別產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="d0aac-156">在**方案總管**中，以滑鼠右鍵按一下 [ *ProductList* ]，然後選取 [ **View Code**]。</span><span class="sxs-lookup"><span data-stu-id="d0aac-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="d0aac-157">將*ProductList.aspx.cs*檔案中的現有程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="d0aac-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="d0aac-158">這段程式碼顯示**ListView**控制項的 `ItemType` 屬性在*ProductList*中參考的 `GetProducts` 方法。</span><span class="sxs-lookup"><span data-stu-id="d0aac-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="d0aac-159">若要將結果限制為特定的資料庫類別，程式碼會在流覽*ProductList .aspx*頁面時，從傳遞至*ProductList*的查詢字串值設定 `categoryId` 值。</span><span class="sxs-lookup"><span data-stu-id="d0aac-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="d0aac-160">`System.Web.ModelBinding` 命名空間中的 `QueryStringAttribute` 類別是用來抓取查詢字串變數 `id`的值。</span><span class="sxs-lookup"><span data-stu-id="d0aac-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="d0aac-161">這會指示模型系結嘗試在執行時間將值從查詢字串系結至 `categoryId` 參數。</span><span class="sxs-lookup"><span data-stu-id="d0aac-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="d0aac-162">當有效的類別目錄當做查詢字串傳遞至頁面時，查詢的結果會限制為資料庫中符合 `categoryId` 值的產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="d0aac-163">例如，如果*ProductsList .aspx*頁面 URL 為：</span><span class="sxs-lookup"><span data-stu-id="d0aac-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="d0aac-164">此頁面只會顯示 `categoryId` 等於 `1`的產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="d0aac-165">如果呼叫*ProductList .aspx*頁面時未包含任何查詢字串，則會顯示所有產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="d0aac-166">這些方法的值來源稱為*值提供*者（例如*QueryString*），而參數屬性會指出要使用的值提供者稱為*值提供者屬性*（例如 `id`）。</span><span class="sxs-lookup"><span data-stu-id="d0aac-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="d0aac-167">ASP.NET 包含 Web Forms 應用程式中所有一般使用者輸入來源的值提供者和對應屬性，例如查詢字串、cookie、表單值、控制項、檢視狀態、會話狀態和配置檔案屬性。</span><span class="sxs-lookup"><span data-stu-id="d0aac-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="d0aac-168">您也可以撰寫自訂值提供者。</span><span class="sxs-lookup"><span data-stu-id="d0aac-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="d0aac-169">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d0aac-169">Run the application</span></span>

<span data-ttu-id="d0aac-170">立即執行應用程式，以查看所有產品或類別的產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="d0aac-171">在 Visual Studio 中按**F5**鍵，以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0aac-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="d0aac-172">瀏覽器會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="d0aac-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="d0aac-173">從 [產品類別] 流覽功能表中選取 [ **Cars** ]。</span><span class="sxs-lookup"><span data-stu-id="d0aac-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="d0aac-174">[ *ProductList* ] 頁面會顯示 [僅顯示**車輛**類別目錄] 產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="d0aac-175">稍後在本教學課程中，您將會顯示產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-175">Later in this tutorial, you'll display product details.</span></span>  

    ![顯示資料項目和詳細資料-Cars](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="d0aac-177">從頂端的導覽功能表中，選取 [**產品**]。</span><span class="sxs-lookup"><span data-stu-id="d0aac-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="d0aac-178">同樣地， *ProductList*會顯示 [default.aspx] 頁面，不過這次它會顯示完整的產品清單。</span><span class="sxs-lookup"><span data-stu-id="d0aac-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![顯示資料項目和詳細資料-產品](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="d0aac-180">關閉瀏覽器並返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d0aac-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="d0aac-181">新增資料控制項以顯示產品詳細資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-181">Add a data control to display product details</span></span>

<span data-ttu-id="d0aac-182">接下來，您將修改您在上一個教學課程中新增的*ProductDetails*頁面中的標記，以顯示特定的產品資訊。</span><span class="sxs-lookup"><span data-stu-id="d0aac-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="d0aac-183">在**方案總管**中，開啟*ProductDetails。*</span><span class="sxs-lookup"><span data-stu-id="d0aac-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="d0aac-184">以下列標記取代現有標記：</span><span class="sxs-lookup"><span data-stu-id="d0aac-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="d0aac-185">這段程式碼會使用**FormView**控制項來顯示特定的產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="d0aac-186">此標記會使用方法，就像在*ProductList .aspx*頁面中用來顯示資料的方法一樣。</span><span class="sxs-lookup"><span data-stu-id="d0aac-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="d0aac-187">**FormView**控制項是用來一次從資料來源顯示單一記錄。</span><span class="sxs-lookup"><span data-stu-id="d0aac-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="d0aac-188">當您使用**FormView**控制項時，您會建立範本來顯示和編輯資料系結值。</span><span class="sxs-lookup"><span data-stu-id="d0aac-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="d0aac-189">這些範本包含控制項、系結運算式，以及定義表單外觀和功能的格式。</span><span class="sxs-lookup"><span data-stu-id="d0aac-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="d0aac-190">將先前的標記連接到資料庫需要額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d0aac-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="d0aac-191">在**方案總管**中，以滑鼠右鍵按一下 [ *ProductDetails* ]，然後按一下 [ **View Code**]。</span><span class="sxs-lookup"><span data-stu-id="d0aac-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="d0aac-192">隨即會顯示*ProductDetails.aspx.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="d0aac-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="d0aac-193">使用下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="d0aac-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="d0aac-194">此程式碼會檢查 "`productID`" 查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="d0aac-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="d0aac-195">如果找到有效的查詢字串值，則會顯示相符的產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="d0aac-196">如果找不到查詢字串，或其值無效，則不會顯示任何產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="d0aac-197">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d0aac-197">Run the application</span></span>

<span data-ttu-id="d0aac-198">現在您可以執行應用程式，以查看根據產品識別碼顯示的個別產品。</span><span class="sxs-lookup"><span data-stu-id="d0aac-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="d0aac-199">在 Visual Studio 中按**F5**鍵，以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0aac-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="d0aac-200">瀏覽器會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="d0aac-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="d0aac-201">從 [類別] 導覽功能表中，選取 [ **Boats** ]。</span><span class="sxs-lookup"><span data-stu-id="d0aac-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="d0aac-202">隨即顯示 [ *ProductList* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d0aac-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="d0aac-203">從 [產品] 清單中選取 [**紙張船**]。</span><span class="sxs-lookup"><span data-stu-id="d0aac-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="d0aac-204">隨即顯示 [ *ProductDetails* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d0aac-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![顯示資料項目和詳細資料-產品](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="d0aac-206">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d0aac-206">Close the browser.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0aac-207">其他資源</span><span class="sxs-lookup"><span data-stu-id="d0aac-207">Additional resources</span></span>

[<span data-ttu-id="d0aac-208">使用模型系結和 web forms 來抓取和顯示資料</span><span class="sxs-lookup"><span data-stu-id="d0aac-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="d0aac-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0aac-209">Next steps</span></span>

<span data-ttu-id="d0aac-210">在本教學課程中，您已新增標記和程式碼，以顯示產品和產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0aac-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="d0aac-211">您已瞭解強型別資料控制、模型系結和值提供者。</span><span class="sxs-lookup"><span data-stu-id="d0aac-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="d0aac-212">在下一個教學課程中，您會將購物車新增至 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0aac-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="d0aac-213">[上一頁](ui_and_navigation.md)
> [下一頁](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="d0aac-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
