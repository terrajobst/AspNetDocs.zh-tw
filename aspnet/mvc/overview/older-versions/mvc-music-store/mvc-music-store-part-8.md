---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 第8部分：使用 Ajax 更新的購物車 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第8部分涵蓋使用 Ajax 更新的購物車。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539253"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="c8061-104">第8部分：使用 Ajax 更新的購物車</span><span class="sxs-lookup"><span data-stu-id="c8061-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="c8061-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="c8061-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="c8061-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="c8061-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="c8061-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="c8061-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="c8061-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="c8061-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="c8061-109">第8部分涵蓋使用 Ajax 更新的購物車。</span><span class="sxs-lookup"><span data-stu-id="c8061-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>

<span data-ttu-id="c8061-110">我們可讓使用者將專輯放在自己的購物車中，而不需註冊，但他們必須註冊為來賓才能完成結帳。</span><span class="sxs-lookup"><span data-stu-id="c8061-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="c8061-111">購物和結帳程式會分成兩個控制器：一個 ShoppingCart 控制器，可讓您以匿名方式將專案新增至購物車，並使用簽出控制器來處理結帳程式。</span><span class="sxs-lookup"><span data-stu-id="c8061-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="c8061-112">我們會從本節的「購物車」開始，然後在下一節中建立結帳程式。</span><span class="sxs-lookup"><span data-stu-id="c8061-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="c8061-113">加入購物車、順序和 OrderDetail 模型類別</span><span class="sxs-lookup"><span data-stu-id="c8061-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="c8061-114">我們的購物車和結帳程式會使用一些新的類別。</span><span class="sxs-lookup"><span data-stu-id="c8061-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="c8061-115">以滑鼠右鍵按一下 [模型] 資料夾，然後使用下列程式碼加入購物車類別（Cart.cs）。</span><span class="sxs-lookup"><span data-stu-id="c8061-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="c8061-116">這個類別非常類似于目前為止使用的其他專案，但 RecordId 屬性的 [Key] 屬性除外。</span><span class="sxs-lookup"><span data-stu-id="c8061-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="c8061-117">我們的購物車專案會有一個名為 CartID 的字串識別碼，以允許匿名購物，但資料表包含名為 RecordId 的整數主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8061-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="c8061-118">依照慣例，Entity Framework 程式碼優先預期名為購物車之資料表的主鍵會是 CartId 或 ID，但我們可以視需要透過注釋或程式碼輕鬆地覆寫該金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8061-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="c8061-119">這是一個範例，示範如何在 Entity Framework 程式碼中使用簡單的慣例（如果它們符合我們的條件），但不會在它們不受到限制。</span><span class="sxs-lookup"><span data-stu-id="c8061-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="c8061-120">接下來，使用下列程式碼新增 Order 類別（Order.cs）。</span><span class="sxs-lookup"><span data-stu-id="c8061-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="c8061-121">這個類別會追蹤訂單的摘要和傳遞資訊。</span><span class="sxs-lookup"><span data-stu-id="c8061-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="c8061-122">**它還不會編譯**，因為它有一個 OrderDetails 的導覽屬性，其相依于尚未建立的類別。</span><span class="sxs-lookup"><span data-stu-id="c8061-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="c8061-123">讓我們透過新增名為 OrderDetail.cs 的類別，新增下列程式碼來修正此問題。</span><span class="sxs-lookup"><span data-stu-id="c8061-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="c8061-124">我們會對我們的 MusicStoreEntities 類別進行最後一次更新，以包含會公開這些新模型類別的 DbSets，其中也包括 DbSet&lt;的演出者&gt;。</span><span class="sxs-lookup"><span data-stu-id="c8061-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="c8061-125">更新後的 MusicStoreEntities 類別會如下所示。</span><span class="sxs-lookup"><span data-stu-id="c8061-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="c8061-126">管理購物車商務邏輯</span><span class="sxs-lookup"><span data-stu-id="c8061-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="c8061-127">接下來，我們會在 [模型] 資料夾中建立 ShoppingCart 類別。</span><span class="sxs-lookup"><span data-stu-id="c8061-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="c8061-128">ShoppingCart 模型會處理對購物車資料表的資料存取。</span><span class="sxs-lookup"><span data-stu-id="c8061-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="c8061-129">此外，它也會處理從購物車新增和移除專案的商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="c8061-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="c8061-130">因為我們不想要求使用者註冊帳戶，只是要將專案新增至購物車，所以我們會在存取購物車時，為使用者指派一個暫時的唯一識別碼（使用 GUID 或全域唯一識別碼）。</span><span class="sxs-lookup"><span data-stu-id="c8061-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="c8061-131">我們會使用 ASP.NET 會話類別來儲存此識別碼。</span><span class="sxs-lookup"><span data-stu-id="c8061-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="c8061-132">*注意： ASP.NET 會話是一個方便的位置，用來儲存使用者特定資訊，這會在離開網站後過期。雖然誤用會話狀態可能會對較大的網站造成效能的影響，但我們的輕量使用也適用于示範用途。*</span><span class="sxs-lookup"><span data-stu-id="c8061-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="c8061-133">ShoppingCart 類別會公開下列方法：</span><span class="sxs-lookup"><span data-stu-id="c8061-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="c8061-134">**AddToCart**會採用專輯做為參數，並將它新增至使用者的購物車。</span><span class="sxs-lookup"><span data-stu-id="c8061-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="c8061-135">由於 [購物車] 資料表會追蹤每個專輯的數量，因此它會包含邏輯以視需要建立新的資料列，或只在使用者已訂購一份專輯副本時，才增加數量。</span><span class="sxs-lookup"><span data-stu-id="c8061-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="c8061-136">**RemoveFromCart**會採用專輯識別碼，並將它從使用者的購物車中移除。</span><span class="sxs-lookup"><span data-stu-id="c8061-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="c8061-137">如果使用者的購物車中只有一個專輯複本，則會移除該資料列。</span><span class="sxs-lookup"><span data-stu-id="c8061-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="c8061-138">**EmptyCart**會從使用者的購物車移除所有專案。</span><span class="sxs-lookup"><span data-stu-id="c8061-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="c8061-139">**GetCartItems**會抓取用於顯示或處理的 CartItems 清單。</span><span class="sxs-lookup"><span data-stu-id="c8061-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="c8061-140">**GetCount**會抓取使用者在其購物車中的專輯總數。</span><span class="sxs-lookup"><span data-stu-id="c8061-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="c8061-141">**GetTotal**會計算購物車中所有專案的總成本。</span><span class="sxs-lookup"><span data-stu-id="c8061-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="c8061-142">**CreateOrder**會在結帳階段期間將購物車轉換成訂單。</span><span class="sxs-lookup"><span data-stu-id="c8061-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="c8061-143">**GetCart**是一種靜態方法，可讓我們的控制器取得購物車物件。</span><span class="sxs-lookup"><span data-stu-id="c8061-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="c8061-144">它會使用**GetCartId**方法來處理從使用者的會話讀取 CartId。</span><span class="sxs-lookup"><span data-stu-id="c8061-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="c8061-145">GetCartId 方法需要 HttpCoNtextBase，讓它可以從使用者的會話讀取使用者的 CartId。</span><span class="sxs-lookup"><span data-stu-id="c8061-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="c8061-146">以下是完整的**ShoppingCart 類別**：</span><span class="sxs-lookup"><span data-stu-id="c8061-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="c8061-147">ViewModels</span><span class="sxs-lookup"><span data-stu-id="c8061-147">ViewModels</span></span>

<span data-ttu-id="c8061-148">我們的購物車控制器必須將一些複雜的資訊傳達給其觀點，而無法完全對應到我們的模型物件。</span><span class="sxs-lookup"><span data-stu-id="c8061-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="c8061-149">我們不想要修改我們的模型，以符合我們的觀點;模型類別應該代表我們的網域，而不是使用者介面。</span><span class="sxs-lookup"><span data-stu-id="c8061-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="c8061-150">其中一個解決方法是使用 ViewBag 類別將資訊傳遞給我們的視圖，如同我們對存放區管理員的下拉式清單資訊所做的，但透過 ViewBag 傳遞大量資訊很難管理。</span><span class="sxs-lookup"><span data-stu-id="c8061-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="c8061-151">解決方法是使用*ViewModel*模式。</span><span class="sxs-lookup"><span data-stu-id="c8061-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="c8061-152">使用此模式時，我們會建立針對我們的特定視圖案例優化的強型別類別，並針對我們的視圖範本所需的動態值/內容公開屬性。</span><span class="sxs-lookup"><span data-stu-id="c8061-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="c8061-153">接著，我們的控制器類別可以填入這些視圖優化的類別，並將其傳遞給我們的 view 範本來使用。</span><span class="sxs-lookup"><span data-stu-id="c8061-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="c8061-154">這可讓您在 [視圖] 範本內進行型別安全、編譯時間檢查和編輯器 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="c8061-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="c8061-155">我們會建立兩個用於購物車控制器的視圖模型： ShoppingCartViewModel 會保存使用者購物車的內容，而 ShoppingCartRemoveViewModel 則會在使用者移除某個專案時用來顯示確認資訊從他們的購物車。</span><span class="sxs-lookup"><span data-stu-id="c8061-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="c8061-156">讓我們在專案的根目錄中建立新的 Viewmodel 資料夾，以保持組織的內容。</span><span class="sxs-lookup"><span data-stu-id="c8061-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="c8061-157">以滑鼠右鍵按一下專案，然後選取 [加入]/[新增資料夾]。</span><span class="sxs-lookup"><span data-stu-id="c8061-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="c8061-158">將資料夾命名為 Viewmodel。</span><span class="sxs-lookup"><span data-stu-id="c8061-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="c8061-159">接下來，在 Viewmodel 資料夾中新增 ShoppingCartViewModel 類別。</span><span class="sxs-lookup"><span data-stu-id="c8061-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="c8061-160">它有兩個屬性：購物車專案清單，以及用來保存購物車中所有專案之總價的十進位值。</span><span class="sxs-lookup"><span data-stu-id="c8061-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="c8061-161">現在，將 ShoppingCartRemoveViewModel 新增至 Viewmodel 資料夾，並具有下列四個屬性。</span><span class="sxs-lookup"><span data-stu-id="c8061-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="c8061-162">購物車控制器</span><span class="sxs-lookup"><span data-stu-id="c8061-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="c8061-163">購物車控制器有三個主要用途：將專案新增至購物車、移除購物車中的專案，以及查看購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="c8061-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="c8061-164">它會使用我們剛才建立的三個類別： ShoppingCartViewModel、ShoppingCartRemoveViewModel 和 ShoppingCart。</span><span class="sxs-lookup"><span data-stu-id="c8061-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="c8061-165">如同在 StoreController 和 StoreManagerController 中，我們會新增欄位來保存 MusicStoreEntities 的實例。</span><span class="sxs-lookup"><span data-stu-id="c8061-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="c8061-166">使用空白控制器範本，將新的購物車控制器新增至專案。</span><span class="sxs-lookup"><span data-stu-id="c8061-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="c8061-167">以下是完整的 ShoppingCart 控制器。</span><span class="sxs-lookup"><span data-stu-id="c8061-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="c8061-168">「索引」和「新增控制器」動作看起來應該很熟悉。</span><span class="sxs-lookup"><span data-stu-id="c8061-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="c8061-169">[移除] 和 [CartSummary 控制器] 動作會處理兩個特殊案例，我們將在下一節中討論。</span><span class="sxs-lookup"><span data-stu-id="c8061-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="c8061-170">使用 jQuery 的 Ajax 更新</span><span class="sxs-lookup"><span data-stu-id="c8061-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="c8061-171">接下來，我們將建立一個強型別為 ShoppingCartViewModel 的購物車索引頁面，並使用與先前相同的方法來使用清單視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c8061-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="c8061-172">不過，我們不會使用 Html.actionlink 來移除購物車中的專案，而是使用 jQuery 以「連接」此視圖中所有連結的 click 事件，其中具有 HTML 類別 RemoveLink。</span><span class="sxs-lookup"><span data-stu-id="c8061-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="c8061-173">此 click 事件處理常式不會張貼表單，而只會對我們的 RemoveFromCart 控制器動作進行 AJAX 回呼。</span><span class="sxs-lookup"><span data-stu-id="c8061-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="c8061-174">RemoveFromCart 會傳回 JSON 序列化結果，而我們的 jQuery 回呼接著會使用 jQuery 剖析並執行四個快速更新頁面：</span><span class="sxs-lookup"><span data-stu-id="c8061-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="c8061-175">從清單中移除已刪除的專輯</span><span class="sxs-lookup"><span data-stu-id="c8061-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="c8061-176">更新標頭中的購物車計數</span><span class="sxs-lookup"><span data-stu-id="c8061-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="c8061-177">向使用者顯示更新訊息</span><span class="sxs-lookup"><span data-stu-id="c8061-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="c8061-178">更新購物車的總價</span><span class="sxs-lookup"><span data-stu-id="c8061-178">Updates the cart total price</span></span>

<span data-ttu-id="c8061-179">由於「移除」案例正由「索引」視圖內的 Ajax 回呼處理，因此我們不需要額外的 RemoveFromCart 動作視圖。</span><span class="sxs-lookup"><span data-stu-id="c8061-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="c8061-180">以下是/ShoppingCart/Index view 的完整程式碼：</span><span class="sxs-lookup"><span data-stu-id="c8061-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="c8061-181">為了測試這一點，我們必須能夠將專案新增至我們的購物車。</span><span class="sxs-lookup"><span data-stu-id="c8061-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="c8061-182">我們會更新**存放區詳細資料**視圖，以包含 [新增至購物車] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c8061-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="c8061-183">當我們在此時，我們可以包含我們在上次更新此視圖之後新增的一些專輯其他資訊：內容類型、演出者、價格和專輯封面。</span><span class="sxs-lookup"><span data-stu-id="c8061-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="c8061-184">更新的商店詳細資料檢視程式碼隨即出現，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c8061-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="c8061-185">現在，我們可以按一下 [存放區]，並在我們的購物車中進行新增和移除專輯的測試。</span><span class="sxs-lookup"><span data-stu-id="c8061-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="c8061-186">執行應用程式，並流覽至存放區索引。</span><span class="sxs-lookup"><span data-stu-id="c8061-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="c8061-187">接下來，按一下內容類型來查看專輯清單。</span><span class="sxs-lookup"><span data-stu-id="c8061-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="c8061-188">按一下專輯標題現在會顯示更新的專輯詳細資料檢視，包括 [新增至購物車] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c8061-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="c8061-189">按一下 [新增至購物車] 按鈕，即可使用 [購物車摘要] 清單顯示我們的購物車索引視圖。</span><span class="sxs-lookup"><span data-stu-id="c8061-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="c8061-190">載入購物車之後，您可以按一下 [從購物車移除] 連結，以查看您的購物車的 Ajax 更新。</span><span class="sxs-lookup"><span data-stu-id="c8061-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="c8061-191">我們建立了一個可運作的購物車，讓未註冊的使用者可以將專案新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="c8061-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="c8061-192">在下一節中，我們將允許他們註冊並完成結帳程式。</span><span class="sxs-lookup"><span data-stu-id="c8061-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c8061-193">[上一頁](mvc-music-store-part-7.md)
> [下一頁](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="c8061-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
