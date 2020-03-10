---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 第4部分：列出產品 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第4部分涵蓋以 GridView contr 列出產品 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566980"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="1f3cd-104">第4部分：列出產品</span><span class="sxs-lookup"><span data-stu-id="1f3cd-104">Part 4: Listing Products</span></span>

<span data-ttu-id="1f3cd-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="1f3cd-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="1f3cd-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="1f3cd-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="1f3cd-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="1f3cd-109">第4部分涵蓋了使用 GridView 控制項列出產品的內容。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a><span data-ttu-id="1f3cd-110">使用 GridView 控制項列出產品</span><span class="sxs-lookup"><span data-stu-id="1f3cd-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="1f3cd-111">讓我們先在解決方案上按一下滑鼠右鍵，然後選取 [新增] 和 [新專案]，開始執行 ProductsList .aspx 頁面。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="1f3cd-112">選擇 [使用主版頁面的 Web 表單]，然後輸入 ProductsList 的頁面名稱。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="1f3cd-113">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="1f3cd-114">接下來，選擇我們放置 [網站] 頁面的 [樣式] 資料夾，然後從 [資料夾內容] 視窗中選取它。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="1f3cd-115">按一下 [確定] 以建立頁面。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="1f3cd-116">我們的資料庫會填入產品資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="1f3cd-117">建立頁面之後，我們會再次使用實體資料來源來存取該產品資料，但在此情況下，我們需要選取產品實體，而且我們需要限制只傳回所選類別的專案。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="1f3cd-118">為了達到此目的，我們會告訴 EntityDataSource 自動產生 WHERE 子句，而我們將指定 WhereParameter。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="1f3cd-119">您會回想一下，當我們在 [產品類別目錄] 功能表中建立功能表項目時，我們會將類別目錄新增至每個連結的 QueryString，以動態建立連結。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="1f3cd-120">我們會告訴實體資料來源從該 QueryString 參數衍生 WHERE 參數。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="1f3cd-121">接下來，我們將設定 ListView 控制項以顯示產品清單。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="1f3cd-122">為了建立最佳的購物體驗，我們會將數個精簡的功能壓縮成 ListVew 中顯示的每個個別產品。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="1f3cd-123">產品名稱將是產品詳細資料檢視的連結。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="1f3cd-124">將會顯示產品的價格。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="1f3cd-125">將會顯示產品的影像，而我們會在應用程式中以動態方式從 [目錄映射] 目錄選取影像。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="1f3cd-126">我們會包含一個連結，以立即將特定產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="1f3cd-127">以下是 ListView 控制項實例的標記。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="1f3cd-128">我們會以動態方式為每個顯示的產品建立數個連結。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="1f3cd-129">此外，在測試自己的新頁面之前，我們必須先建立產品目錄映射的目錄結構，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="1f3cd-130">當我們的產品映射可供存取之後，我們就可以測試產品清單頁面。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="1f3cd-131">從網站的 [首頁] 中，按一下其中一個 [類別目錄清單] 連結。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="1f3cd-132">現在我們需要執行 ProductDetails .aspx 頁面和 AddToCart 功能。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="1f3cd-133">使用 [檔案-&gt;新增]，依照先前的方式使用網站主版頁面建立 ProductDetails 的頁面名稱。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="1f3cd-134">我們會再次使用 EntityDataSource 控制項來存取資料庫中的特定產品記錄，我們將使用 ASP.NET FormView 控制項來顯示產品資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="1f3cd-135">如果格式化看起來有點有趣，別擔心。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="1f3cd-136">上述標記會針對我們稍後將會執行的幾項功能，將空間留在顯示版面配置中。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="1f3cd-137">購物車會代表我們的應用程式中更複雜的邏輯。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="1f3cd-138">若要開始，請使用 [檔案-&gt;新增] 來建立名為 MyShoppingCart 的頁面。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="1f3cd-139">請注意，我們不會選擇名稱 ShoppingCart。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="1f3cd-140">我們的資料庫包含名為 "ShoppingCart" 的資料表。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="1f3cd-141">當我們產生實體資料模型類別是針對資料庫中的每個資料表所建立。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="1f3cd-142">因此，實體資料模型產生一個名為 "ShoppingCart" 的實體類別。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="1f3cd-143">我們可以編輯模型，讓我們可以將該名稱用於我們的購物車實施，或針對我們的需求進行擴充，但我們將改為選擇可避免衝突的名稱。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="1f3cd-144">另外值得一提的是，我們將建立簡單的購物車，並使用購物車顯示來內嵌購物車邏輯。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="1f3cd-145">我們也可以選擇在完全獨立的商務層中執行我們的購物車。</span><span class="sxs-lookup"><span data-stu-id="1f3cd-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1f3cd-146">[上一頁](tailspin-spyworks-part-3.md)
> [下一頁](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="1f3cd-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
