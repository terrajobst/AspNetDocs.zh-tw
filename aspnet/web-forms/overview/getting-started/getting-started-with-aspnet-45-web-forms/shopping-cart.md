---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 購物車 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 46264a0ab2244cff24761ce94b41722e61e3f426
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614918"
---
# <a name="shopping-cart"></a><span data-ttu-id="b3da9-103">購物車</span><span class="sxs-lookup"><span data-stu-id="b3da9-103">Shopping Cart</span></span>

<span data-ttu-id="b3da9-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="b3da9-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="b3da9-105">[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="b3da9-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="b3da9-106">本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="b3da9-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="b3da9-107">本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="b3da9-108">本教學課程說明將購物車新增至 Wingtip 玩具範例 ASP.NET Web Forms 應用程式所需的商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="b3da9-108">This tutorial describes the business logic required to add a shopping cart to the Wingtip Toys sample ASP.NET Web Forms application.</span></span> <span data-ttu-id="b3da9-109">本教學課程是根據上一個教學課程「顯示資料項目和詳細資料」來建立，屬於 Wingtip 玩具商店教學課程系列。</span><span class="sxs-lookup"><span data-stu-id="b3da9-109">This tutorial builds on the previous tutorial "Display Data Items and Details" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="b3da9-110">當您完成本教學課程時，您的範例應用程式使用者將能夠在其購物車中新增、移除及修改產品。</span><span class="sxs-lookup"><span data-stu-id="b3da9-110">When you've completed this tutorial, the users of your sample app will be able to add, remove, and modify the products in their shopping cart.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="b3da9-111">您將瞭解的內容：</span><span class="sxs-lookup"><span data-stu-id="b3da9-111">What you'll learn:</span></span>

1. <span data-ttu-id="b3da9-112">如何建立 web 應用程式的購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-112">How to create a shopping cart for the web application.</span></span>
2. <span data-ttu-id="b3da9-113">如何讓使用者將專案新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-113">How to enable users to add items to the shopping cart.</span></span>
3. <span data-ttu-id="b3da9-114">如何新增[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction)控制項以顯示購物車詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3da9-114">How to add a [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) control to display shopping cart details.</span></span>
4. <span data-ttu-id="b3da9-115">如何計算和顯示訂單總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-115">How to calculate and display the order total.</span></span>
5. <span data-ttu-id="b3da9-116">如何移除和更新購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-116">How to remove and update items in the shopping cart.</span></span>
6. <span data-ttu-id="b3da9-117">如何包含購物車計數器。</span><span class="sxs-lookup"><span data-stu-id="b3da9-117">How to include a shopping cart counter.</span></span>

## <a name="code-features-in-this-tutorial"></a><span data-ttu-id="b3da9-118">本教學課程中的程式碼功能：</span><span class="sxs-lookup"><span data-stu-id="b3da9-118">Code features in this tutorial:</span></span>

1. <span data-ttu-id="b3da9-119">Entity Framework Code First</span><span class="sxs-lookup"><span data-stu-id="b3da9-119">Entity Framework Code First</span></span>
2. <span data-ttu-id="b3da9-120">資料註釋</span><span class="sxs-lookup"><span data-stu-id="b3da9-120">Data Annotations</span></span>
3. <span data-ttu-id="b3da9-121">強型別資料控制</span><span class="sxs-lookup"><span data-stu-id="b3da9-121">Strongly typed data controls</span></span>
4. <span data-ttu-id="b3da9-122">模型繫結</span><span class="sxs-lookup"><span data-stu-id="b3da9-122">Model binding</span></span>

## <a name="creating-a-shopping-cart"></a><span data-ttu-id="b3da9-123">建立購物車</span><span class="sxs-lookup"><span data-stu-id="b3da9-123">Creating a Shopping Cart</span></span>

<span data-ttu-id="b3da9-124">稍早在本教學課程系列中，您已新增頁面和程式碼，以從資料庫中查看產品資料。</span><span class="sxs-lookup"><span data-stu-id="b3da9-124">Earlier in this tutorial series, you added pages and code to view product data from a database.</span></span> <span data-ttu-id="b3da9-125">在本教學課程中，您將建立購物車來管理使用者有興趣購買的產品。</span><span class="sxs-lookup"><span data-stu-id="b3da9-125">In this tutorial, you'll create a shopping cart to manage the products that users are interested in buying.</span></span> <span data-ttu-id="b3da9-126">使用者即使未註冊或登入，也可以流覽並將專案新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-126">Users will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="b3da9-127">若要管理購物車存取權，當使用者第一次存取購物車時，您會使用全域唯一識別碼（GUID）將唯一的 `ID` 指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="b3da9-127">To manage shopping cart access, you will assign users a unique `ID` using a globally unique identifier (GUID) when the user accesses the shopping cart for the first time.</span></span> <span data-ttu-id="b3da9-128">您會使用 ASP.NET 會話狀態來儲存此 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-128">You'll store this `ID` using the ASP.NET Session state.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b3da9-129">ASP.NET 會話狀態是儲存使用者特定資訊的方便位置，這會在使用者離開網站後過期。</span><span class="sxs-lookup"><span data-stu-id="b3da9-129">The ASP.NET Session state is a convenient place to store user-specific information which will expire after the user leaves the site.</span></span> <span data-ttu-id="b3da9-130">雖然誤用會話狀態可能會對較大的網站造成效能的影響，但會話狀態的輕量使用很適合用於示範。</span><span class="sxs-lookup"><span data-stu-id="b3da9-130">While misuse of session state can have performance implications on larger sites, light use of session state works well for demonstration purposes.</span></span> <span data-ttu-id="b3da9-131">Wingtip 玩具範例專案顯示如何使用沒有外部提供者的會話狀態，其中會話狀態會在裝載網站的 web 伺服器上以同進程方式儲存。</span><span class="sxs-lookup"><span data-stu-id="b3da9-131">The Wingtip Toys sample project shows how to use session state without an external provider, where session state is stored in-process on the web server hosting the site.</span></span> <span data-ttu-id="b3da9-132">對於提供多個應用程式實例的大型網站，或針對在不同伺服器上執行多個應用程式實例的網站，請考慮使用**Windows Azure**快取服務。</span><span class="sxs-lookup"><span data-stu-id="b3da9-132">For larger sites that provide multiple instances of an application or for sites that run multiple instances of an application on different servers, consider using **Windows Azure Cache Service**.</span></span> <span data-ttu-id="b3da9-133">此快取服務會提供網站外部的分散式快取服務，並解決使用同進程會話狀態的問題。</span><span class="sxs-lookup"><span data-stu-id="b3da9-133">This Cache Service provides a distributed caching service that is external to the web site and solves the problem of using in-process session state.</span></span> <span data-ttu-id="b3da9-134">如需詳細資訊，請參閱[如何搭配 Windows Azure 網站使用 ASP.NET 會話狀態](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)。</span><span class="sxs-lookup"><span data-stu-id="b3da9-134">For more information see, [How to Use ASP.NET Session State with Windows Azure Web Sites](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider).</span></span>

### <a name="add-cartitem-as-a-model-class"></a><span data-ttu-id="b3da9-135">將 CartItem 新增為模型類別</span><span class="sxs-lookup"><span data-stu-id="b3da9-135">Add CartItem as a Model Class</span></span>

<span data-ttu-id="b3da9-136">稍早在本教學課程系列中，您可以藉由在 [*模型*] 資料夾中建立 `Category` 和 `Product` 類別，來定義分類和產品資料的架構。</span><span class="sxs-lookup"><span data-stu-id="b3da9-136">Earlier in this tutorial series, you defined the schema for the category and product data by creating the `Category` and `Product` classes in the *Models* folder.</span></span> <span data-ttu-id="b3da9-137">現在，新增類別以定義購物車的架構。</span><span class="sxs-lookup"><span data-stu-id="b3da9-137">Now, add a new class to define the schema for the shopping cart.</span></span> <span data-ttu-id="b3da9-138">稍後在本教學課程中，您將加入一個類別來處理 `CartItem` 資料表的資料存取。</span><span class="sxs-lookup"><span data-stu-id="b3da9-138">Later in this tutorial, you will add a class to handle data access to the `CartItem` table.</span></span> <span data-ttu-id="b3da9-139">這個類別會供應商業規則來新增、移除及更新購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-139">This class will provide the business logic to add, remove, and update items in the shopping cart.</span></span>

1. <span data-ttu-id="b3da9-140">以滑鼠右鍵按一下 [*模型*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-140">Right-click the *Models* folder and select **Add** -&gt; **New Item**.</span></span> 

    ![購物車-新專案](shopping-cart/_static/image1.png)
2. <span data-ttu-id="b3da9-142">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b3da9-142">The **Add New Item** dialog box is displayed.</span></span> <span data-ttu-id="b3da9-143">選取 [程式**代碼**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-143">Select **Code**, and then select **Class**.</span></span> 

    ![購物車-[加入新專案] 對話方塊](shopping-cart/_static/image2.png)
3. <span data-ttu-id="b3da9-145">將這個新類別命名為*CartItem.cs*。</span><span class="sxs-lookup"><span data-stu-id="b3da9-145">Name this new class *CartItem.cs*.</span></span>
4. <span data-ttu-id="b3da9-146">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-146">Click **Add**.</span></span>  
   <span data-ttu-id="b3da9-147">新的類別檔案會顯示在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="b3da9-147">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="b3da9-148">將預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b3da9-148">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

<span data-ttu-id="b3da9-149">`CartItem` 類別包含會定義使用者新增至購物車之每個產品的架構。</span><span class="sxs-lookup"><span data-stu-id="b3da9-149">The `CartItem` class contains the schema that will define each product a user adds to the shopping cart.</span></span> <span data-ttu-id="b3da9-150">這個類別與您稍早在本教學課程系列中建立的其他架構類別類似。</span><span class="sxs-lookup"><span data-stu-id="b3da9-150">This class is similar to the other schema classes you created earlier in this tutorial series.</span></span> <span data-ttu-id="b3da9-151">依照慣例，Entity Framework Code First 預期 `CartItem` 資料表的主鍵會是 `CartItemId` 或 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-151">By convention, Entity Framework Code First expects that the primary key for the `CartItem` table will be either `CartItemId` or `ID`.</span></span> <span data-ttu-id="b3da9-152">不過，程式碼會使用資料批註 `[Key]` 屬性來覆寫預設行為。</span><span class="sxs-lookup"><span data-stu-id="b3da9-152">However, the code overrides the default behavior by using the data annotation `[Key]` attribute.</span></span> <span data-ttu-id="b3da9-153">ItemId 屬性的 `Key` 屬性會指定 `ItemID` 屬性是主要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b3da9-153">The `Key` attribute of the ItemId property specifies that the `ItemID` property is the primary key.</span></span>

<span data-ttu-id="b3da9-154">`CartId` 屬性會指定與要購買的專案相關聯之使用者的 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-154">The `CartId` property specifies the `ID` of the user that is associated with the item to purchase.</span></span> <span data-ttu-id="b3da9-155">當使用者存取購物車時，您會新增程式碼來建立此使用者 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-155">You'll add code to create this user `ID` when the user accesses the shopping cart.</span></span> <span data-ttu-id="b3da9-156">此 `ID` 也會儲存為 ASP.NET 會話變數。</span><span class="sxs-lookup"><span data-stu-id="b3da9-156">This `ID` will also be stored as an ASP.NET Session variable.</span></span>

### <a name="update-the-product-context"></a><span data-ttu-id="b3da9-157">更新產品內容</span><span class="sxs-lookup"><span data-stu-id="b3da9-157">Update the Product Context</span></span>

<span data-ttu-id="b3da9-158">除了加入 `CartItem` 類別以外，您還需要更新管理實體類別的資料庫內容類別，並提供資料庫的資料存取權。</span><span class="sxs-lookup"><span data-stu-id="b3da9-158">In addition to adding the `CartItem` class, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="b3da9-159">若要這麼做，您要將新建立的 `CartItem` 模型類別加入至 `ProductContext` 類別。</span><span class="sxs-lookup"><span data-stu-id="b3da9-159">To do this, you will add the newly created `CartItem` model class to the `ProductContext` class.</span></span>

1. <span data-ttu-id="b3da9-160">在**方案總管**中，尋找並開啟 [*模型*] 資料夾中的*ProductCoNtext.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-160">In **Solution Explorer**, find and open the *ProductContext.cs* file in the *Models* folder.</span></span>
2. <span data-ttu-id="b3da9-161">將反白顯示的程式碼新增至*ProductCoNtext.cs*檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3da9-161">Add the highlighted code to the *ProductContext.cs* file as follows:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

<span data-ttu-id="b3da9-162">如先前在本教學課程系列中所述， *ProductCoNtext.cs*檔案中的程式碼會新增 `System.Data.Entity` 命名空間，讓您可以存取 Entity Framework 的所有核心功能。</span><span class="sxs-lookup"><span data-stu-id="b3da9-162">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="b3da9-163">這項功能包括使用強型別物件來查詢、插入、更新和刪除資料的功能。</span><span class="sxs-lookup"><span data-stu-id="b3da9-163">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="b3da9-164">`ProductContext` 類別會加入新加入 `CartItem` 模型類別的存取權。</span><span class="sxs-lookup"><span data-stu-id="b3da9-164">The `ProductContext` class adds access to the newly added `CartItem` model class.</span></span>

### <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="b3da9-165">管理購物車商務邏輯</span><span class="sxs-lookup"><span data-stu-id="b3da9-165">Managing the Shopping Cart Business Logic</span></span>

<span data-ttu-id="b3da9-166">接下來，您將在新的*邏輯*資料夾中建立 `ShoppingCart` 類別。</span><span class="sxs-lookup"><span data-stu-id="b3da9-166">Next, you'll create the `ShoppingCart` class in a new *Logic* folder.</span></span> <span data-ttu-id="b3da9-167">`ShoppingCart` 類別會處理 `CartItem` 資料表的資料存取。</span><span class="sxs-lookup"><span data-stu-id="b3da9-167">The `ShoppingCart` class handles data access to the `CartItem` table.</span></span> <span data-ttu-id="b3da9-168">類別也會包含商務邏輯，以新增、移除和更新購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-168">The class will also include the business logic to add, remove, and update items in the shopping cart.</span></span>

<span data-ttu-id="b3da9-169">您將新增的購物車邏輯將包含管理下列動作的功能：</span><span class="sxs-lookup"><span data-stu-id="b3da9-169">The shopping cart logic that you will add will contain the functionality to manage the following actions:</span></span>

1. <span data-ttu-id="b3da9-170">將專案新增至購物車</span><span class="sxs-lookup"><span data-stu-id="b3da9-170">Adding items to the shopping cart</span></span>
2. <span data-ttu-id="b3da9-171">從購物車移除專案</span><span class="sxs-lookup"><span data-stu-id="b3da9-171">Removing items from the shopping cart</span></span>
3. <span data-ttu-id="b3da9-172">取得購物車識別碼</span><span class="sxs-lookup"><span data-stu-id="b3da9-172">Getting the shopping cart ID</span></span>
4. <span data-ttu-id="b3da9-173">從購物車中取出專案</span><span class="sxs-lookup"><span data-stu-id="b3da9-173">Retrieving items from the shopping cart</span></span>
5. <span data-ttu-id="b3da9-174">匯總所有購物車專案的數量</span><span class="sxs-lookup"><span data-stu-id="b3da9-174">Totaling the amount of all the shopping cart items</span></span>
6. <span data-ttu-id="b3da9-175">更新購物車資料</span><span class="sxs-lookup"><span data-stu-id="b3da9-175">Updating the shopping cart data</span></span>

<span data-ttu-id="b3da9-176">[購物車] 頁面（*ShoppingCart .aspx*）和 [購物車] 類別會一起用來存取購物車資料。</span><span class="sxs-lookup"><span data-stu-id="b3da9-176">A shopping cart page (*ShoppingCart.aspx*) and the shopping cart class will be used together to access shopping cart data.</span></span> <span data-ttu-id="b3da9-177">[購物車] 頁面將會顯示使用者新增至購物車的所有專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-177">The shopping cart page will display all the items the user adds to the shopping cart.</span></span> <span data-ttu-id="b3da9-178">除了 [購物車] 頁面和類別以外，您還會建立一個頁面（*AddToCart .aspx*），將產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-178">Besides the shopping cart page and class, you'll create a page (*AddToCart.aspx*) to add products to the shopping cart.</span></span> <span data-ttu-id="b3da9-179">您也會將程式碼加入至*ProductList*頁面，以及將提供*AddToCart*頁面連結的*ProductDetails*頁面，讓使用者可以將產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-179">You will also add code to the *ProductList.aspx* page and the *ProductDetails.aspx* page that will provide a link to the *AddToCart.aspx* page, so that the user can add products to the shopping cart.</span></span>

<span data-ttu-id="b3da9-180">下圖顯示當使用者將產品新增至購物車時所發生的基本程式。</span><span class="sxs-lookup"><span data-stu-id="b3da9-180">The following diagram shows the basic process that occurs when the user adds a product to the shopping cart.</span></span>

![購物車-新增至購物車](shopping-cart/_static/image3.png)

<span data-ttu-id="b3da9-182">當使用者按一下 [ *ProductList* ] 頁面或 [ *ProductDetails* ] 頁面上的 [**新增至購物車**] 連結時，應用程式將會流覽至 [ *AddToCart* ] 頁面，然後自動移至 [ *ShoppingCart* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-182">When the user clicks the **Add To Cart** link on either the *ProductList.aspx* page or the *ProductDetails.aspx* page, the application will navigate to the *AddToCart.aspx* page and then automatically to the *ShoppingCart.aspx* page.</span></span> <span data-ttu-id="b3da9-183">*AddToCart*會藉由呼叫 ShoppingCart 類別中的方法，將選取產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-183">The *AddToCart.aspx* page will add the select product to the shopping cart by calling a method in the ShoppingCart class.</span></span> <span data-ttu-id="b3da9-184">[ *ShoppingCart* ] 頁面會顯示已新增至「購物車」的產品。</span><span class="sxs-lookup"><span data-stu-id="b3da9-184">The *ShoppingCart.aspx* page will display the products that have been added to the shopping cart.</span></span>

#### <a name="creating-the-shopping-cart-class"></a><span data-ttu-id="b3da9-185">建立購物車類別</span><span class="sxs-lookup"><span data-stu-id="b3da9-185">Creating the Shopping Cart Class</span></span>

<span data-ttu-id="b3da9-186">`ShoppingCart` 類別會加入至應用程式中的個別資料夾，讓模型（模型資料夾）、頁面（根資料夾）和邏輯（邏輯資料夾）之間有清楚的區別。</span><span class="sxs-lookup"><span data-stu-id="b3da9-186">The `ShoppingCart` class will be added to a separate folder in the application so that there will be a clear distinction between the model (Models folder), the pages (root folder) and the logic (Logic folder).</span></span>

1. <span data-ttu-id="b3da9-187">在**方案總管**中，以滑鼠右鍵按一下**WingtipToys**專案，然後選取 [**加入**-] &gt;[**新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-187">In **Solution Explorer**, right-click the **WingtipToys**project and select **Add**-&gt;**New Folder**.</span></span> <span data-ttu-id="b3da9-188">將新資料夾命名為*邏輯*。</span><span class="sxs-lookup"><span data-stu-id="b3da9-188">Name the new folder *Logic*.</span></span>
2. <span data-ttu-id="b3da9-189">以滑鼠右鍵按一下*邏輯*資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-189">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>
3. <span data-ttu-id="b3da9-190">新增名為*ShoppingCartActions.cs*的新類別檔案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-190">Add a new class file named *ShoppingCartActions.cs*.</span></span>
4. <span data-ttu-id="b3da9-191">將預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b3da9-191">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

<span data-ttu-id="b3da9-192">`AddToCart` 方法可根據產品 `ID`，將個別產品納入購物車中。</span><span class="sxs-lookup"><span data-stu-id="b3da9-192">The `AddToCart` method enables individual products to be included in the shopping cart based on the product `ID`.</span></span> <span data-ttu-id="b3da9-193">產品會新增至購物車，或如果購物車已經包含該產品的專案，則數量會遞增。</span><span class="sxs-lookup"><span data-stu-id="b3da9-193">The product is added to the cart, or if the cart already contains an item for that product, the quantity is incremented.</span></span>

<span data-ttu-id="b3da9-194">`GetCartId` 方法會傳回使用者 `ID` 的購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-194">The `GetCartId` method returns the cart `ID` for the user.</span></span> <span data-ttu-id="b3da9-195">購物車 `ID` 用來追蹤使用者在其購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-195">The cart `ID` is used to track the items that a user has in their shopping cart.</span></span> <span data-ttu-id="b3da9-196">如果使用者沒有現有的購物車 `ID`，系統就會為他們建立新的購物車 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-196">If the user does not have an existing cart `ID`, a new cart `ID` is created for them.</span></span> <span data-ttu-id="b3da9-197">如果使用者是以已註冊的使用者身分登入，購物車 `ID` 會設定為其使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b3da9-197">If the user is signed in as a registered user, the cart `ID` is set to their user name.</span></span> <span data-ttu-id="b3da9-198">不過，如果使用者未登入，購物車 `ID` 會設定為唯一值（GUID）。</span><span class="sxs-lookup"><span data-stu-id="b3da9-198">However, if the user is not signed in, the cart `ID` is set to a unique value (a GUID).</span></span> <span data-ttu-id="b3da9-199">GUID 可確保根據會話，只為每個使用者建立一個購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-199">A GUID ensures that only one cart is created for each user, based on session.</span></span>

<span data-ttu-id="b3da9-200">`GetCartItems` 方法會傳回使用者的購物車專案清單。</span><span class="sxs-lookup"><span data-stu-id="b3da9-200">The `GetCartItems` method returns a list of shopping cart items for the user.</span></span> <span data-ttu-id="b3da9-201">稍後在本教學課程中，您會看到使用 `GetCartItems` 方法，將模型系結用於顯示購物車中的購物車專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-201">Later in this tutorial, you will see that model binding is used to display the cart items in the shopping cart using the `GetCartItems` method.</span></span>

### <a name="creating-the-add-to-cart-functionality"></a><span data-ttu-id="b3da9-202">建立「新增至購物車」功能</span><span class="sxs-lookup"><span data-stu-id="b3da9-202">Creating the Add-To-Cart Functionality</span></span>

<span data-ttu-id="b3da9-203">如先前所述，您將建立名為*AddToCart*的處理頁面，用來將新產品新增至使用者的購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-203">As mentioned earlier, you will create a processing page named *AddToCart.aspx* that will be used to add new products to the shopping cart of the user.</span></span> <span data-ttu-id="b3da9-204">此頁面將會在您剛才建立的 `ShoppingCart` 類別中呼叫 `AddToCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3da9-204">This page will call the `AddToCart` method in the `ShoppingCart` class that you just created.</span></span> <span data-ttu-id="b3da9-205">*AddToCart*會預期會將產品 `ID` 傳遞至該頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-205">The *AddToCart.aspx* page will expect that a product `ID` is passed to it.</span></span> <span data-ttu-id="b3da9-206">在 `ShoppingCart` 類別中呼叫 `AddToCart` 方法時，將會使用此產品 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-206">This product `ID` will be used when calling the `AddToCart` method in the `ShoppingCart` class.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b3da9-207">您將修改此頁面的程式碼後置（*AddToCart.aspx.cs*），而不是頁面 UI （*AddToCart .aspx*）。</span><span class="sxs-lookup"><span data-stu-id="b3da9-207">You will be modifying the code-behind (*AddToCart.aspx.cs*) for this page, not the page UI (*AddToCart.aspx*).</span></span>

#### <a name="to-create-the-add-to-cart-functionality"></a><span data-ttu-id="b3da9-208">若要建立「新增至購物車」功能：</span><span class="sxs-lookup"><span data-stu-id="b3da9-208">To create the Add-To-Cart functionality:</span></span>

1. <span data-ttu-id="b3da9-209">在**方案總管**中，以滑鼠右鍵按一下**WingtipToys**專案，**然後按一下 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-209">In **Solution Explorer**, right-click the **WingtipToys**project, click **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="b3da9-210">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b3da9-210">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="b3da9-211">將標準的新頁面（Web Form）新增至名為*AddToCart*的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3da9-211">Add a standard new page (Web Form) to the application named *AddToCart.aspx*.</span></span> 

    ![購物車-新增 Web 表單](shopping-cart/_static/image4.png)
3. <span data-ttu-id="b3da9-213">在**方案總管**中，以滑鼠右鍵按一下 [ *AddToCart* ] 頁面，然後按一下 [**查看程式碼**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-213">In **Solution Explorer**, right-click the *AddToCart.aspx* page and then click **View Code**.</span></span> <span data-ttu-id="b3da9-214">*AddToCart.aspx.cs*程式碼後置檔案會在編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="b3da9-214">The *AddToCart.aspx.cs* code-behind file is opened in the editor.</span></span>
4. <span data-ttu-id="b3da9-215">將*AddToCart.aspx.cs*程式碼後置中的現有程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="b3da9-215">Replace the existing code in the *AddToCart.aspx.cs* code-behind with the following:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

<span data-ttu-id="b3da9-216">載入*AddToCart .aspx*頁面時，會從查詢字串中抓取產品 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-216">When the *AddToCart.aspx* page is loaded, the product `ID` is retrieved from the query string.</span></span> <span data-ttu-id="b3da9-217">接下來，會建立購物車類別的實例，並使用它來呼叫您稍早在本教學課程中新增的 `AddToCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3da9-217">Next, an instance of the shopping cart class is created and used to call the `AddToCart` method that you added earlier in this tutorial.</span></span> <span data-ttu-id="b3da9-218">包含在*ShoppingCartActions.cs*檔案中的 `AddToCart` 方法包括將選取的產品新增至購物車的邏輯，或增加所選產品的產品數量。</span><span class="sxs-lookup"><span data-stu-id="b3da9-218">The `AddToCart` method, contained in the *ShoppingCartActions.cs* file, includes the logic to add the selected product to the shopping cart or increment the product quantity of the selected product.</span></span> <span data-ttu-id="b3da9-219">如果產品尚未新增至「購物車」，則會將產品新增至資料庫的 `CartItem` 資料表。</span><span class="sxs-lookup"><span data-stu-id="b3da9-219">If the product hasn't been added to the shopping cart, the product is added to the `CartItem` table of the database.</span></span> <span data-ttu-id="b3da9-220">如果產品已新增至購物車，而使用者新增了相同產品的其他專案，則 [`CartItem`] 資料表中的產品數量會遞增。</span><span class="sxs-lookup"><span data-stu-id="b3da9-220">If the product has already been added to the shopping cart and the user adds an additional item of the same product, the product quantity is incremented in the `CartItem` table.</span></span> <span data-ttu-id="b3da9-221">最後，頁面會重新導向回到您將在下一個步驟中新增的*ShoppingCart*頁面，使用者會在其中看到購物車中已更新的專案清單。</span><span class="sxs-lookup"><span data-stu-id="b3da9-221">Finally, the page redirects back to the *ShoppingCart.aspx* page that you'll add in the next step, where the user sees an updated list of items in the cart.</span></span>

<span data-ttu-id="b3da9-222">如先前所述，使用者 `ID` 是用來識別與特定使用者相關聯的產品。</span><span class="sxs-lookup"><span data-stu-id="b3da9-222">As previously mentioned, a user `ID` is used to identify the products that are associated with a specific user.</span></span> <span data-ttu-id="b3da9-223">每次使用者將產品新增至購物車時，都會將此 `ID` 新增至 `CartItem` 資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="b3da9-223">This `ID` is added to a row in the `CartItem` table each time the user adds a product to the shopping cart.</span></span>

### <a name="creating-the-shopping-cart-ui"></a><span data-ttu-id="b3da9-224">建立購物車 UI</span><span class="sxs-lookup"><span data-stu-id="b3da9-224">Creating the Shopping Cart UI</span></span>

<span data-ttu-id="b3da9-225">[ *ShoppingCart* ] 頁面會顯示使用者已新增到其購物車的產品。</span><span class="sxs-lookup"><span data-stu-id="b3da9-225">The *ShoppingCart.aspx* page will display the products that the user has added to their shopping cart.</span></span> <span data-ttu-id="b3da9-226">它也能讓您新增、移除和更新購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-226">It will also provide the ability to add, remove and update items in the shopping cart.</span></span>

1. <span data-ttu-id="b3da9-227">在**方案總管**中，以滑鼠**按右鍵 [** **WingtipToys**]，然後按一下 [新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-227">In **Solution Explorer**, right-click **WingtipToys**, click **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="b3da9-228">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b3da9-228">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="b3da9-229">**使用主版頁面選取 Web 表單**，以新增包含主版頁面的新頁面（Web form）。</span><span class="sxs-lookup"><span data-stu-id="b3da9-229">Add a new page (Web Form) that includes a master page by selecting **Web Form using Master Page**.</span></span> <span data-ttu-id="b3da9-230">將新頁面命名為*ShoppingCart .aspx*。</span><span class="sxs-lookup"><span data-stu-id="b3da9-230">Name the new page *ShoppingCart.aspx*.</span></span>
3. <span data-ttu-id="b3da9-231">選取 [**網站**]，將主版頁面附加至新建立的 *.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-231">Select **Site.Master** to attach the master page to the newly created *.aspx* page.</span></span>
4. <span data-ttu-id="b3da9-232">在 [ *ShoppingCart* ] 頁面中，將現有標記取代為下列標記：</span><span class="sxs-lookup"><span data-stu-id="b3da9-232">In the *ShoppingCart.aspx* page, replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

<span data-ttu-id="b3da9-233">*ShoppingCart .aspx*頁面包含名為 `CartList`的**GridView**控制項。</span><span class="sxs-lookup"><span data-stu-id="b3da9-233">The *ShoppingCart.aspx* page includes a **GridView** control named `CartList`.</span></span> <span data-ttu-id="b3da9-234">此控制項使用模型系結，將購物車資料從資料庫系結至**GridView**控制項。</span><span class="sxs-lookup"><span data-stu-id="b3da9-234">This control uses model binding to bind the shopping cart data from the database to the **GridView** control.</span></span> <span data-ttu-id="b3da9-235">當您設定**GridView**控制項的 [`ItemType`] 屬性時，資料系結運算式 `Item` 會出現在控制項的標記中，而控制項則會變成強型別。</span><span class="sxs-lookup"><span data-stu-id="b3da9-235">When you set the `ItemType` property of the **GridView** control, the data-binding expression `Item` is available in the markup of the control and the control becomes strongly typed.</span></span> <span data-ttu-id="b3da9-236">如稍早在本教學課程系列中所述，您可以使用 IntelliSense 來選取 `Item` 物件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3da9-236">As mentioned earlier in this tutorial series, you can select details of the `Item` object using IntelliSense.</span></span> <span data-ttu-id="b3da9-237">若要將資料控制項設定為使用模型系結來選取資料，您必須設定控制項的 `SelectMethod` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b3da9-237">To configure a data control to use model binding to select data, you set the `SelectMethod` property of the control.</span></span> <span data-ttu-id="b3da9-238">在上述標記中，您會將 `SelectMethod` 設定為使用 GetShoppingCartItems 方法，以傳回 `CartItem` 物件的清單。</span><span class="sxs-lookup"><span data-stu-id="b3da9-238">In the markup above, you set the `SelectMethod` to use the GetShoppingCartItems method which returns a list of `CartItem` objects.</span></span> <span data-ttu-id="b3da9-239">**GridView**資料控制項會在頁面生命週期的適當時間呼叫方法，並自動系結傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="b3da9-239">The **GridView** data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="b3da9-240">您仍然必須加入 `GetShoppingCartItems` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3da9-240">The `GetShoppingCartItems` method must still be added.</span></span>

#### <a name="retrieving-the-shopping-cart-items"></a><span data-ttu-id="b3da9-241">正在抓取購物車專案</span><span class="sxs-lookup"><span data-stu-id="b3da9-241">Retrieving the Shopping Cart Items</span></span>

<span data-ttu-id="b3da9-242">接下來，您要將程式碼新增至*ShoppingCart.aspx.cs*程式碼後置，以取出並填入購物車 UI。</span><span class="sxs-lookup"><span data-stu-id="b3da9-242">Next, you add code to the *ShoppingCart.aspx.cs* code-behind to retrieve and populate the Shopping Cart UI.</span></span>

1. <span data-ttu-id="b3da9-243">在**方案總管**中，以滑鼠右鍵按一下 [ *ShoppingCart* ] 頁面，然後按一下 [**查看程式碼**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-243">In **Solution Explorer**, right-click the *ShoppingCart.aspx* page and then click **View Code**.</span></span> <span data-ttu-id="b3da9-244">*ShoppingCart.aspx.cs*程式碼後置檔案會在編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="b3da9-244">The *ShoppingCart.aspx.cs* code-behind file is opened in the editor.</span></span>
2. <span data-ttu-id="b3da9-245">將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b3da9-245">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

<span data-ttu-id="b3da9-246">如前所述，`GridView` 資料控制項會在頁面生命週期的適當時間呼叫 `GetShoppingCartItems` 方法，並自動系結傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="b3da9-246">As mentioned above, the `GridView` data control calls the `GetShoppingCartItems` method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="b3da9-247">`GetShoppingCartItems` 方法會建立 `ShoppingCartActions` 物件的實例。</span><span class="sxs-lookup"><span data-stu-id="b3da9-247">The `GetShoppingCartItems` method creates an instance of the `ShoppingCartActions` object.</span></span> <span data-ttu-id="b3da9-248">然後，程式碼會使用該實例，藉由呼叫 `GetCartItems` 方法來傳回購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-248">Then, the code uses that instance to return the items in the cart by calling the `GetCartItems` method.</span></span>

### <a name="adding-products-to-the-shopping-cart"></a><span data-ttu-id="b3da9-249">將產品新增至購物車</span><span class="sxs-lookup"><span data-stu-id="b3da9-249">Adding Products to the Shopping Cart</span></span>

<span data-ttu-id="b3da9-250">當顯示 [ *ProductList* ] 或 [ *ProductDetails* ] 頁面時，使用者將能夠使用連結將產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-250">When either the *ProductList.aspx* or the *ProductDetails.aspx* page is displayed, the user will be able to add the product to the shopping cart using a link.</span></span> <span data-ttu-id="b3da9-251">當他們按一下連結時，應用程式會流覽至名為*AddToCart*的處理頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-251">When they click the link, the application navigates to the processing page named *AddToCart.aspx*.</span></span> <span data-ttu-id="b3da9-252">*AddToCart*會呼叫您稍早在本教學課程中新增的 `ShoppingCart` 類別中的 `AddToCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3da9-252">The *AddToCart.aspx* page will call the `AddToCart` method in the `ShoppingCart` class that you added earlier in this tutorial.</span></span>

<span data-ttu-id="b3da9-253">現在，您會將 [**新增至購物車**] 連結新增至 [ *ProductList* ] 頁面和 [ *ProductDetails* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-253">Now, you'll add an **Add to Cart** link to both the *ProductList.aspx* page and the *ProductDetails.aspx* page.</span></span> <span data-ttu-id="b3da9-254">此連結會包含從資料庫中抓取的產品 `ID`。</span><span class="sxs-lookup"><span data-stu-id="b3da9-254">This link will include the product `ID` that is retrieved from the database.</span></span>

1. <span data-ttu-id="b3da9-255">在**方案總管**中，尋找並開啟名為*ProductList*的頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-255">In **Solution Explorer**, find and open the page named *ProductList.aspx*.</span></span>
2. <span data-ttu-id="b3da9-256">將以黃色反白顯示的標記新增至 [ *ProductList* ] 頁面，讓整個頁面顯示如下：</span><span class="sxs-lookup"><span data-stu-id="b3da9-256">Add the markup highlighted in yellow to the *ProductList.aspx* page so that the entire page appears as follows:</span></span>  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a><span data-ttu-id="b3da9-257">測試購物車</span><span class="sxs-lookup"><span data-stu-id="b3da9-257">Testing the Shopping Cart</span></span>

<span data-ttu-id="b3da9-258">執行應用程式，以瞭解如何將產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-258">Run the application to see how you add products to the shopping cart.</span></span>

1. <span data-ttu-id="b3da9-259">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3da9-259">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="b3da9-260">在專案重新建立資料庫之後，瀏覽器將會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-260">After the project recreates the database, the browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="b3da9-261">從 [類別] 流覽功能表中選取 [ **Cars** ]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-261">Select **Cars** from the category navigation menu.</span></span>  
 <span data-ttu-id="b3da9-262">隨即顯示 [ *ProductList* ] 頁面，只顯示 "Cars" 類別中包含的產品。</span><span class="sxs-lookup"><span data-stu-id="b3da9-262">The *ProductList.aspx* page is displayed showing only products included in the "Cars" category.</span></span> 

    ![購物車-汽車](shopping-cart/_static/image5.png)
3. <span data-ttu-id="b3da9-264">按一下所列第一個產品旁的 [**新增至購物車**] 連結（可轉換的車）。</span><span class="sxs-lookup"><span data-stu-id="b3da9-264">Click the **Add to Cart** link next to the first product listed (the convertible car).</span></span>   
 <span data-ttu-id="b3da9-265">隨即顯示 [ *ShoppingCart* ] 頁面，顯示您的購物車中的選取專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-265">The *ShoppingCart.aspx* page is displayed, showing the selection in your shopping cart.</span></span> 

    ![購物車-購物車](shopping-cart/_static/image6.png)
4. <span data-ttu-id="b3da9-267">從 [類別] 導覽功能表選取 [**平面**]，以查看其他產品。</span><span class="sxs-lookup"><span data-stu-id="b3da9-267">View additional products by selecting **Planes** from the category navigation menu.</span></span>
5. <span data-ttu-id="b3da9-268">按一下所列第一個產品旁的 [**新增至購物車**] 連結。</span><span class="sxs-lookup"><span data-stu-id="b3da9-268">Click the **Add to Cart** link next to the first product listed.</span></span>  
 <span data-ttu-id="b3da9-269">隨即會顯示 [ *ShoppingCart* ] 頁面，其中包含其他專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-269">The *ShoppingCart.aspx* page is displayed with the additional item.</span></span>
6. <span data-ttu-id="b3da9-270">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="b3da9-270">Close the browser.</span></span>

### <a name="calculating-and-displaying-the-order-total"></a><span data-ttu-id="b3da9-271">計算和顯示訂單總計</span><span class="sxs-lookup"><span data-stu-id="b3da9-271">Calculating and Displaying the Order Total</span></span>

<span data-ttu-id="b3da9-272">除了將產品新增至購物車以外，您還會將 `GetTotal` 方法新增至 [`ShoppingCart`] 類別，並在 [購物車] 頁面中顯示總訂單金額。</span><span class="sxs-lookup"><span data-stu-id="b3da9-272">In addition to adding products to the shopping cart, you will add a `GetTotal` method to the `ShoppingCart` class and display the total order amount in the shopping cart page.</span></span>

1. <span data-ttu-id="b3da9-273">在**方案總管**中，開啟*邏輯*資料夾中的*ShoppingCartActions.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-273">In **Solution Explorer**, open the *ShoppingCartActions.cs* file in the *Logic* folder.</span></span>
2. <span data-ttu-id="b3da9-274">將下列 `GetTotal` 方法以黃色反白顯示 `ShoppingCart` 類別，讓類別顯示如下：</span><span class="sxs-lookup"><span data-stu-id="b3da9-274">Add the following `GetTotal` method highlighted in yellow to the `ShoppingCart` class, so that the class appears as follows:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

<span data-ttu-id="b3da9-275">首先，`GetTotal` 方法會取得使用者的購物車識別碼。</span><span class="sxs-lookup"><span data-stu-id="b3da9-275">First, the `GetTotal` method gets the ID of the shopping cart for the user.</span></span> <span data-ttu-id="b3da9-276">然後，方法會將產品價格乘以購物車中列出之每個產品的產品數量，藉以取得購物車總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-276">Then the method gets the cart total by multiplying the product price by the product quantity for each product listed in the cart.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b3da9-277">上述程式碼會使用可為 null 的型別 "`int?`"。</span><span class="sxs-lookup"><span data-stu-id="b3da9-277">The above code uses the nullable type "`int?`".</span></span> <span data-ttu-id="b3da9-278">可為 null 的類型可以表示基礎類型的所有值，以及 null 值。</span><span class="sxs-lookup"><span data-stu-id="b3da9-278">Nullable types can represent all the values of an underlying type, and also as a null value.</span></span> <span data-ttu-id="b3da9-279">如需詳細資訊，請參閱[使用可為 null 的類型](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b3da9-279">For more information see, [Using Nullable Types](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx).</span></span>

### <a name="modify-the-shopping-cart-display"></a><span data-ttu-id="b3da9-280">修改購物車顯示</span><span class="sxs-lookup"><span data-stu-id="b3da9-280">Modify the Shopping Cart Display</span></span>

<span data-ttu-id="b3da9-281">接下來，您將修改*ShoppingCart*的程式碼，以呼叫 `GetTotal` 方法，並在頁面載入時，在*ShoppingCart*頁面上顯示該總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-281">Next you'll modify the code for the *ShoppingCart.aspx* page to call the `GetTotal` method and display that total on the *ShoppingCart.aspx* page when the page loads.</span></span>

1. <span data-ttu-id="b3da9-282">在**方案總管**中，以滑鼠右鍵按一下 [ *ShoppingCart* ] 頁面，然後選取 [ **View Code**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-282">In **Solution Explorer**, right-click the *ShoppingCart.aspx* page and select **View Code**.</span></span>
2. <span data-ttu-id="b3da9-283">在*ShoppingCart.aspx.cs*檔案中，新增下列以黃色反白顯示的程式碼，以更新 `Page_Load` 處理常式：</span><span class="sxs-lookup"><span data-stu-id="b3da9-283">In the *ShoppingCart.aspx.cs* file, update the `Page_Load` handler by adding the following code highlighted in yellow:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

<span data-ttu-id="b3da9-284">當*ShoppingCart .aspx*頁面載入時，它會載入購物車物件，然後藉由呼叫 `ShoppingCart` 類別的 `GetTotal` 方法來抓取購物車總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-284">When the *ShoppingCart.aspx* page loads, it loads the shopping cart object and then retrieves the shopping cart total by calling the `GetTotal` method of the `ShoppingCart` class.</span></span> <span data-ttu-id="b3da9-285">如果購物車是空的，就會顯示該效果的訊息。</span><span class="sxs-lookup"><span data-stu-id="b3da9-285">If the shopping cart is empty, a message to that effect is displayed.</span></span>

### <a name="testing-the-shopping-cart-total"></a><span data-ttu-id="b3da9-286">測試購物車總計</span><span class="sxs-lookup"><span data-stu-id="b3da9-286">Testing the Shopping Cart Total</span></span>

<span data-ttu-id="b3da9-287">立即執行應用程式，以瞭解您不能只將產品新增至購物車，但可以查看購物車總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-287">Run the application now to see how you can not only add a product to the shopping cart, but you can see the shopping cart total.</span></span>

1. <span data-ttu-id="b3da9-288">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3da9-288">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="b3da9-289">瀏覽器將會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-289">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="b3da9-290">從 [類別] 流覽功能表中選取 [ **Cars** ]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-290">Select **Cars** from the category navigation menu.</span></span>
3. <span data-ttu-id="b3da9-291">按一下第一個產品旁的 [**新增至購物車**] 連結。</span><span class="sxs-lookup"><span data-stu-id="b3da9-291">Click the **Add To Cart** link next to the first product.</span></span>   
 <span data-ttu-id="b3da9-292">隨即顯示 [ *ShoppingCart* ] 頁面與 [訂單總計]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-292">The *ShoppingCart.aspx* page is displayed with the order total.</span></span> 

    ![購物車-購物車總計](shopping-cart/_static/image7.png)
4. <span data-ttu-id="b3da9-294">將一些其他產品（例如平面）新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-294">Add some other products (for example, a plane) to the cart.</span></span>
5. <span data-ttu-id="b3da9-295">隨即會顯示 [ *ShoppingCart* ] 頁面，其中包含您已新增的所有產品的更新總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-295">The *ShoppingCart.aspx* page is displayed with an updated total for all the products you've added.</span></span> 

    ![購物車-多項產品](shopping-cart/_static/image8.png)
6. <span data-ttu-id="b3da9-297">關閉瀏覽器視窗以停止執行中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3da9-297">Stop the running app by closing the browser window.</span></span>

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a><span data-ttu-id="b3da9-298">將 [更新] 和 [簽出] 按鈕新增至購物車</span><span class="sxs-lookup"><span data-stu-id="b3da9-298">Adding Update and Checkout Buttons to the Shopping Cart</span></span>

<span data-ttu-id="b3da9-299">若要允許使用者修改購物車，您要將 [**更新**] 按鈕和 [**結帳**] 按鈕新增至 [購物車] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-299">To allow the users to modify the shopping cart, you'll add an **Update** button and a **Checkout** button to the shopping cart page.</span></span> <span data-ttu-id="b3da9-300">在本教學課程系列稍後的版本中，不會使用 [**簽出**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3da9-300">The **Checkout** button is not used until later in this tutorial series.</span></span>

1. <span data-ttu-id="b3da9-301">在**方案總管**中，開啟 web 應用程式專案根目錄中的 [ *ShoppingCart* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-301">In **Solution Explorer**, open the *ShoppingCart.aspx* page in the root of the web application project.</span></span>
2. <span data-ttu-id="b3da9-302">若要將 [**更新**] 按鈕和 [**簽出**] 按鈕新增至*ShoppingCart*頁面，請將以黃色反白顯示的標記新增至現有的標記，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="b3da9-302">To add the **Update** button and the **Checkout** button to the *ShoppingCart.aspx* page, add the markup highlighted in yellow to the existing markup, as shown in the following code:</span></span>   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

<span data-ttu-id="b3da9-303">當使用者按一下 [**更新**] 按鈕時，就會呼叫 `UpdateBtn_Click` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b3da9-303">When the user clicks the **Update** button, the `UpdateBtn_Click` event handler will be called.</span></span> <span data-ttu-id="b3da9-304">這個事件處理常式會呼叫您將在下一個步驟中新增的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b3da9-304">This event handler will call the code that you'll add in the next step.</span></span>

<span data-ttu-id="b3da9-305">接下來，您可以更新*ShoppingCart.aspx.cs*檔案中包含的程式碼，以迴圈處理購物車專案，並呼叫 `RemoveItem` 和 `UpdateItem` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3da9-305">Next, you can update the code contained in the *ShoppingCart.aspx.cs* file to loop through the cart items and call the `RemoveItem` and `UpdateItem` methods.</span></span>

1. <span data-ttu-id="b3da9-306">在**方案總管**中，開啟 web 應用程式專案根目錄中的*ShoppingCart.aspx.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-306">In **Solution Explorer**, open the *ShoppingCart.aspx.cs* file in the root of the web application project.</span></span>
2. <span data-ttu-id="b3da9-307">將下列以黃色反白顯示的程式碼區段新增至*ShoppingCart.aspx.cs*檔案：</span><span class="sxs-lookup"><span data-stu-id="b3da9-307">Add the following code sections highlighted in yellow to the *ShoppingCart.aspx.cs* file:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

<span data-ttu-id="b3da9-308">當使用者按一下 [ *ShoppingCart* ] 頁面上的 [**更新**] 按鈕時，就會呼叫 UpdateCartItems 方法。</span><span class="sxs-lookup"><span data-stu-id="b3da9-308">When the user clicks the **Update** button on the *ShoppingCart.aspx* page, the UpdateCartItems method is called.</span></span> <span data-ttu-id="b3da9-309">UpdateCartItems 方法會針對購物車中的每個專案取得更新的值。</span><span class="sxs-lookup"><span data-stu-id="b3da9-309">The UpdateCartItems method gets the updated values for each item in the shopping cart.</span></span> <span data-ttu-id="b3da9-310">然後，UpdateCartItems 方法會呼叫 `UpdateShoppingCartDatabase` 方法（在下一個步驟中新增並說明），以從購物車新增或移除專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-310">Then, the UpdateCartItems method calls the `UpdateShoppingCartDatabase` method (added and explained in the next step) to either add or remove items from the shopping cart.</span></span> <span data-ttu-id="b3da9-311">一旦更新資料庫以反映購物車的更新之後， **gridview**控制項就會藉由呼叫**gridview**的 `DataBind` 方法，在 [購物車] 頁面上更新。</span><span class="sxs-lookup"><span data-stu-id="b3da9-311">Once the database has been updated to reflect the updates to the shopping cart, the **GridView** control is updated on the shopping cart page by calling the `DataBind` method for the **GridView**.</span></span> <span data-ttu-id="b3da9-312">此外，[購物車] 頁面上的 [總訂單數量] 也會更新，以反映專案的更新清單。</span><span class="sxs-lookup"><span data-stu-id="b3da9-312">Also, the total order amount on the shopping cart page is updated to reflect the updated list of items.</span></span>

### <a name="updating-and-removing-shopping-cart-items"></a><span data-ttu-id="b3da9-313">更新和移除購物車專案</span><span class="sxs-lookup"><span data-stu-id="b3da9-313">Updating and Removing Shopping Cart Items</span></span>

<span data-ttu-id="b3da9-314">在 [ *ShoppingCart* ] 頁面上，您可以看到已加入的控制項，用於更新專案的數量和移除專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-314">On the *ShoppingCart.aspx* page, you can see controls have been added for updating the quantity of an item and removing an item.</span></span> <span data-ttu-id="b3da9-315">現在，請新增程式碼，讓這些控制項能夠正常執行。</span><span class="sxs-lookup"><span data-stu-id="b3da9-315">Now, add the code that will make these controls work.</span></span>

1. <span data-ttu-id="b3da9-316">在**方案總管**中，開啟*邏輯*資料夾中的*ShoppingCartActions.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-316">In **Solution Explorer**, open the *ShoppingCartActions.cs* file in the *Logic* folder.</span></span>
2. <span data-ttu-id="b3da9-317">將下列以黃色反白顯示的程式碼新增至*ShoppingCartActions.cs*類別檔案：</span><span class="sxs-lookup"><span data-stu-id="b3da9-317">Add the following code highlighted in yellow to the *ShoppingCartActions.cs* class file:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

<span data-ttu-id="b3da9-318">`UpdateShoppingCartDatabase` 方法（從 [ *ShoppingCart.aspx.cs* ] 頁面上的 [`UpdateCartItems`] 方法呼叫）包含從 [購物車] 更新或移除專案的邏輯。</span><span class="sxs-lookup"><span data-stu-id="b3da9-318">The `UpdateShoppingCartDatabase` method, called from the `UpdateCartItems` method on the *ShoppingCart.aspx.cs* page, contains the logic to either update or remove items from the shopping cart.</span></span> <span data-ttu-id="b3da9-319">`UpdateShoppingCartDatabase` 方法會逐一查看購物車清單中的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="b3da9-319">The `UpdateShoppingCartDatabase` method iterates through all the rows within the shopping cart list.</span></span> <span data-ttu-id="b3da9-320">如果已標示要移除的購物車專案，或數量小於一，則會呼叫 `RemoveItem` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3da9-320">If a shopping cart item has been marked to be removed, or the quantity is less than one, the `RemoveItem` method is called.</span></span> <span data-ttu-id="b3da9-321">否則，在呼叫 `UpdateItem` 方法時，會檢查購物車專案是否有更新。</span><span class="sxs-lookup"><span data-stu-id="b3da9-321">Otherwise, the shopping cart item is checked for updates when the `UpdateItem` method is called.</span></span> <span data-ttu-id="b3da9-322">移除或更新購物車專案之後，就會儲存資料庫變更。</span><span class="sxs-lookup"><span data-stu-id="b3da9-322">After the shopping cart item has been removed or updated, the database changes are saved.</span></span>

<span data-ttu-id="b3da9-323">`ShoppingCartUpdates` 結構用來保存所有購物車專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-323">The `ShoppingCartUpdates` structure is used to hold all the shopping cart items.</span></span> <span data-ttu-id="b3da9-324">`UpdateShoppingCartDatabase` 方法會使用 `ShoppingCartUpdates` 結構來判斷是否需要更新或移除任何專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-324">The `UpdateShoppingCartDatabase` method uses the `ShoppingCartUpdates` structure to determine if any of the items need to be updated or removed.</span></span>

<span data-ttu-id="b3da9-325">在下一個教學課程中，您將使用 `EmptyCart` 方法來清除購買產品後的購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-325">In the next tutorial, you will use the `EmptyCart` method to clear the shopping cart after purchasing products.</span></span> <span data-ttu-id="b3da9-326">但現在，您將使用剛新增至*ShoppingCartActions.cs*檔案的 `GetCount` 方法，來判斷購物車中有多少專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-326">But for now, you will use the `GetCount` method that you just added to the *ShoppingCartActions.cs* file to determine how many items are in the shopping cart.</span></span>

### <a name="adding-a-shopping-cart-counter"></a><span data-ttu-id="b3da9-327">加入購物車計數器</span><span class="sxs-lookup"><span data-stu-id="b3da9-327">Adding a Shopping Cart Counter</span></span>

<span data-ttu-id="b3da9-328">若要允許使用者查看購物車中的總專案數，您要將計數器新增至 [*網站*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-328">To allow the user to view the total number of items in the shopping cart, you will add a counter to the *Site.Master* page.</span></span> <span data-ttu-id="b3da9-329">此計數器也會做為購物車的連結。</span><span class="sxs-lookup"><span data-stu-id="b3da9-329">This counter will also act as a link to the shopping cart.</span></span>

1. <span data-ttu-id="b3da9-330">在**方案總管**中，開啟 [*網站*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-330">In **Solution Explorer**, open the *Site.Master* page.</span></span>
2. <span data-ttu-id="b3da9-331">將 [購物車] 計數器連結新增至導覽區段，以修改標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3da9-331">Modify the markup by adding the shopping cart counter link as shown in yellow to the navigation section so it appears as follows:</span></span>  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. <span data-ttu-id="b3da9-332">接下來，新增以黃色反白顯示的程式碼，以更新*Site.Master.cs*檔案的程式碼後置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3da9-332">Next, update the code-behind of the *Site.Master.cs* file by adding the code highlighted in yellow as follows:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

<span data-ttu-id="b3da9-333">將頁面轉譯為 HTML 之前，會引發 `Page_PreRender` 事件。</span><span class="sxs-lookup"><span data-stu-id="b3da9-333">Before the page is rendered as HTML, the `Page_PreRender` event is raised.</span></span> <span data-ttu-id="b3da9-334">在 `Page_PreRender` 處理常式中，購物車的總計數是藉由呼叫 `GetCount` 方法來決定。</span><span class="sxs-lookup"><span data-stu-id="b3da9-334">In the `Page_PreRender` handler, the total count of the shopping cart is determined by calling the `GetCount` method.</span></span> <span data-ttu-id="b3da9-335">傳回的值會加入至*網站主版*頁面的標記所包含的 `cartCount` 範圍內。</span><span class="sxs-lookup"><span data-stu-id="b3da9-335">The returned value is added to the `cartCount` span included in the markup of the *Site.Master* page.</span></span> <span data-ttu-id="b3da9-336">`<span>` 標記可正確呈現內部元素。</span><span class="sxs-lookup"><span data-stu-id="b3da9-336">The `<span>` tags enables the inner elements to be properly rendered.</span></span> <span data-ttu-id="b3da9-337">當網站的任何頁面顯示時，將會顯示購物車總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-337">When any page of the site is displayed, the shopping cart total will be displayed.</span></span> <span data-ttu-id="b3da9-338">使用者也可以按一下 [購物車總計]，以顯示 [購物車]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-338">The user can also click the shopping cart total to display the shopping cart.</span></span>

## <a name="testing-the-completed-shopping-cart"></a><span data-ttu-id="b3da9-339">測試已完成的購物車</span><span class="sxs-lookup"><span data-stu-id="b3da9-339">Testing the Completed Shopping Cart</span></span>

<span data-ttu-id="b3da9-340">您可以立即執行應用程式，以瞭解如何在「購物車」中新增、刪除及更新專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-340">You can run the application now to see how you can add, delete, and update items in the shopping cart.</span></span> <span data-ttu-id="b3da9-341">購物車總計會反映購物車中所有專案的總成本。</span><span class="sxs-lookup"><span data-stu-id="b3da9-341">The shopping cart total will reflect the total cost of all items in the shopping cart.</span></span>

1. <span data-ttu-id="b3da9-342">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3da9-342">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="b3da9-343">瀏覽器會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="b3da9-343">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="b3da9-344">從 [類別] 流覽功能表中選取 [ **Cars** ]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-344">Select **Cars** from the category navigation menu.</span></span>
3. <span data-ttu-id="b3da9-345">按一下第一個產品旁的 [**新增至購物車**] 連結。</span><span class="sxs-lookup"><span data-stu-id="b3da9-345">Click the **Add To Cart** link next to the first product.</span></span>   
 <span data-ttu-id="b3da9-346">隨即顯示 [ *ShoppingCart* ] 頁面與 [訂單總計]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-346">The *ShoppingCart.aspx* page is displayed with the order total.</span></span>
4. <span data-ttu-id="b3da9-347">從 [類別] 導覽功能表選取 [**平面**]。</span><span class="sxs-lookup"><span data-stu-id="b3da9-347">Select **Planes** from the category navigation menu.</span></span>
5. <span data-ttu-id="b3da9-348">按一下第一個產品旁的 [**新增至購物車**] 連結。</span><span class="sxs-lookup"><span data-stu-id="b3da9-348">Click the **Add To Cart** link next to the first product.</span></span>
6. <span data-ttu-id="b3da9-349">將購物車中第一個專案的數量設定為3，然後選取第二個專案的 [**移除專案**] 核取方塊。<a id="a"></a></span><span class="sxs-lookup"><span data-stu-id="b3da9-349">Set the quantity of the first item in the shopping cart to 3 and select the **Remove Item** check box of the second item.<a id="a"></a></span></span>
7. <span data-ttu-id="b3da9-350">按一下 [**更新**] 按鈕以更新 [購物車] 頁面，並顯示新的訂單總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-350">Click the **Update** button to update the shopping cart page and display the new order total.</span></span> 

    ![購物車-購物車更新](shopping-cart/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="b3da9-352">總結</span><span class="sxs-lookup"><span data-stu-id="b3da9-352">Summary</span></span>

<span data-ttu-id="b3da9-353">在本教學課程中，您已建立 Wingtip 玩具 Web Forms 範例應用程式的購物車。</span><span class="sxs-lookup"><span data-stu-id="b3da9-353">In this tutorial, you have created a shopping cart for the Wingtip Toys Web Forms sample application.</span></span> <span data-ttu-id="b3da9-354">在本教學課程中，您已使用 Entity Framework Code First、資料批註、強型別資料控制和模型系結。</span><span class="sxs-lookup"><span data-stu-id="b3da9-354">During this tutorial you have used Entity Framework Code First, data annotations, strongly typed data controls, and model binding.</span></span>

<span data-ttu-id="b3da9-355">購物車支援新增、刪除和更新使用者已選取要購買的專案。</span><span class="sxs-lookup"><span data-stu-id="b3da9-355">The shopping cart supports adding, deleting, and updating items that the user has selected for purchase.</span></span> <span data-ttu-id="b3da9-356">除了執行購物車功能以外，您也已瞭解如何在**GridView**控制項中顯示購物車專案，並計算訂單總計。</span><span class="sxs-lookup"><span data-stu-id="b3da9-356">In addition to implementing the shopping cart functionality, you have learned how to display shopping cart items in a **GridView** control and calculate the order total.</span></span>

## <a name="addition-information"></a><span data-ttu-id="b3da9-357">額外資訊</span><span class="sxs-lookup"><span data-stu-id="b3da9-357">Addition Information</span></span>

[<span data-ttu-id="b3da9-358">ASP.NET 會話狀態總覽</span><span class="sxs-lookup"><span data-stu-id="b3da9-358">ASP.NET Session State Overview</span></span>](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> <span data-ttu-id="b3da9-359">[上一頁](display_data_items_and_details.md)
> [下一頁](checkout-and-payment-with-paypal.md)</span><span class="sxs-lookup"><span data-stu-id="b3da9-359">[Previous](display_data_items_and_details.md)
[Next](checkout-and-payment-with-paypal.md)</span></span>
