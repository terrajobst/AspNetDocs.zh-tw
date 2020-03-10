---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 第9部分：註冊和簽出 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第9部分涵蓋註冊和簽出。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559532"
---
# <a name="part-9-registration-and-checkout"></a><span data-ttu-id="b2d57-104">第9部分：註冊和簽出</span><span class="sxs-lookup"><span data-stu-id="b2d57-104">Part 9: Registration and Checkout</span></span>

<span data-ttu-id="b2d57-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="b2d57-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="b2d57-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="b2d57-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="b2d57-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="b2d57-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="b2d57-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="b2d57-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="b2d57-109">第9部分涵蓋註冊和簽出。</span><span class="sxs-lookup"><span data-stu-id="b2d57-109">Part 9 covers Registration and Checkout.</span></span>

<span data-ttu-id="b2d57-110">在本節中，我們將建立 CheckoutController，其會收集購物者的位址和付款資訊。</span><span class="sxs-lookup"><span data-stu-id="b2d57-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="b2d57-111">我們會要求使用者在簽出之前向我們的網站註冊，因此此控制站將需要授權。</span><span class="sxs-lookup"><span data-stu-id="b2d57-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="b2d57-112">使用者可以按一下 [結帳] 按鈕，從購物車流覽至結帳程式。</span><span class="sxs-lookup"><span data-stu-id="b2d57-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="b2d57-113">如果使用者未登入，系統會提示他們輸入。</span><span class="sxs-lookup"><span data-stu-id="b2d57-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="b2d57-114">成功登入後，使用者就會顯示在 [位址] 和 [付款] 視圖中。</span><span class="sxs-lookup"><span data-stu-id="b2d57-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="b2d57-115">填寫表單並提交訂單後，就會顯示在 [訂單確認] 畫面上。</span><span class="sxs-lookup"><span data-stu-id="b2d57-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="b2d57-116">嘗試查看不存在的順序或不屬於您的順序時，將會顯示錯誤視圖。</span><span class="sxs-lookup"><span data-stu-id="b2d57-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="b2d57-117">遷移購物車</span><span class="sxs-lookup"><span data-stu-id="b2d57-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="b2d57-118">當購物程式是匿名的時，當使用者按一下 [結帳] 按鈕時，就必須註冊並登入。</span><span class="sxs-lookup"><span data-stu-id="b2d57-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="b2d57-119">使用者會預期我們會在造訪之間維護其購物車資訊，因此，當他們完成註冊或登入時，我們需要將購物車資訊與使用者建立關聯。</span><span class="sxs-lookup"><span data-stu-id="b2d57-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="b2d57-120">這其實非常簡單，因為我們的 ShoppingCart 類別已經有一個方法，可將目前購物車中的所有專案與使用者名稱產生關聯。</span><span class="sxs-lookup"><span data-stu-id="b2d57-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="b2d57-121">只有在使用者完成註冊或登入時，才需要呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="b2d57-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="b2d57-122">開啟我們在設定成員資格和授權時所新增的**AccountController**類別。</span><span class="sxs-lookup"><span data-stu-id="b2d57-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="b2d57-123">加入參考 MvcMusicStore 的 using 語句，然後新增下列 MigrateShoppingCart 方法：</span><span class="sxs-lookup"><span data-stu-id="b2d57-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="b2d57-124">接下來，修改登入 post 動作，以在使用者經過驗證後呼叫 MigrateShoppingCart，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2d57-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="b2d57-125">在成功建立使用者帳戶之後，立即對 [註冊 post] 動作進行相同的變更：</span><span class="sxs-lookup"><span data-stu-id="b2d57-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="b2d57-126">這就是-現在匿名購物車會在成功註冊或登入時自動轉移到使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b2d57-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="b2d57-127">建立 CheckoutController</span><span class="sxs-lookup"><span data-stu-id="b2d57-127">Creating the CheckoutController</span></span>

<span data-ttu-id="b2d57-128">以滑鼠右鍵按一下 [控制器] 資料夾，然後使用空白控制器範本，將新的控制器新增至名為 CheckoutController 的專案。</span><span class="sxs-lookup"><span data-stu-id="b2d57-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="b2d57-129">首先，將 [授權] 屬性新增至控制器類別宣告上方，以要求使用者在簽出前先進行註冊：</span><span class="sxs-lookup"><span data-stu-id="b2d57-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="b2d57-130">*注意：這與先前對 StoreManagerController 所做的變更類似，但在此情況下，授權屬性需要使用者必須是系統管理員角色。在結帳控制器中，我們要求使用者登入，但不要求他們是系統管理員。*</span><span class="sxs-lookup"><span data-stu-id="b2d57-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="b2d57-131">為了簡單起見，我們不會在本教學課程中處理付款資訊。</span><span class="sxs-lookup"><span data-stu-id="b2d57-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="b2d57-132">相反地，我們允許使用者使用促銷代碼來簽出。</span><span class="sxs-lookup"><span data-stu-id="b2d57-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="b2d57-133">我們會使用名為促銷代碼的常數來儲存此促銷代碼。</span><span class="sxs-lookup"><span data-stu-id="b2d57-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="b2d57-134">如同在 StoreController 中，我們會宣告一個欄位來保存 MusicStoreEntities 類別的實例，名為 storeDB。</span><span class="sxs-lookup"><span data-stu-id="b2d57-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="b2d57-135">若要使用 MusicStoreEntities 類別，我們必須為 MvcMusicStore 命名空間加入 using 語句。</span><span class="sxs-lookup"><span data-stu-id="b2d57-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="b2d57-136">我們的結帳控制器頂端會顯示如下。</span><span class="sxs-lookup"><span data-stu-id="b2d57-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="b2d57-137">CheckoutController 將會有下列控制器動作：</span><span class="sxs-lookup"><span data-stu-id="b2d57-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="b2d57-138">**AddressAndPayment （GET 方法）** 會顯示一個表單，讓使用者輸入其資訊。</span><span class="sxs-lookup"><span data-stu-id="b2d57-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="b2d57-139">**AddressAndPayment （POST 方法）** 會驗證輸入並處理訂單。</span><span class="sxs-lookup"><span data-stu-id="b2d57-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="b2d57-140">**完成**將會在使用者成功完成簽出程式之後顯示。</span><span class="sxs-lookup"><span data-stu-id="b2d57-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="b2d57-141">此視圖會包含使用者的訂單號碼，做為確認。</span><span class="sxs-lookup"><span data-stu-id="b2d57-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="b2d57-142">首先，讓我們將索引控制器動作（在我們建立控制器時產生）重新命名為 AddressAndPayment。</span><span class="sxs-lookup"><span data-stu-id="b2d57-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="b2d57-143">此控制器動作只會顯示簽出表單，因此不需要任何模型資訊。</span><span class="sxs-lookup"><span data-stu-id="b2d57-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="b2d57-144">我們的 AddressAndPayment 文章方法將遵循我們在 StoreManagerController 中使用的相同模式：它會嘗試接受表單提交並完成訂單，如果失敗，將會重新顯示表單。</span><span class="sxs-lookup"><span data-stu-id="b2d57-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="b2d57-145">驗證表單輸入符合訂單的驗證需求之後，我們會直接檢查促銷代碼表單值。</span><span class="sxs-lookup"><span data-stu-id="b2d57-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="b2d57-146">假設一切都正確，我們將以訂單儲存更新後的資訊，告訴 ShoppingCart 物件完成訂單程式，然後重新導向至完整的動作。</span><span class="sxs-lookup"><span data-stu-id="b2d57-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="b2d57-147">成功完成結帳程式後，系統會將使用者重新導向至完整的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="b2d57-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="b2d57-148">此動作會執行簡單的檢查，以驗證訂單確實屬於已登入的使用者，然後才將訂單號碼顯示為確認。</span><span class="sxs-lookup"><span data-stu-id="b2d57-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="b2d57-149">*注意：當我們開始專案時，會在/Views/Shared 資料夾中自動為我們建立錯誤視圖。*</span><span class="sxs-lookup"><span data-stu-id="b2d57-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="b2d57-150">完整的 CheckoutController 程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2d57-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="b2d57-151">新增 AddressAndPayment 視圖</span><span class="sxs-lookup"><span data-stu-id="b2d57-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="b2d57-152">現在，讓我們建立 AddressAndPayment view。</span><span class="sxs-lookup"><span data-stu-id="b2d57-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="b2d57-153">以滑鼠右鍵按一下其中一個 [AddressAndPayment 控制器] 動作，並新增名為 AddressAndPayment 的視圖，其強型別為訂單並使用編輯範本，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b2d57-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="b2d57-154">此視圖會使用我們在建立 StoreManagerEdit view 時所查看的兩種技術：</span><span class="sxs-lookup"><span data-stu-id="b2d57-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="b2d57-155">我們將使用 EditorForModel （）來顯示訂單模型的表單欄位</span><span class="sxs-lookup"><span data-stu-id="b2d57-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="b2d57-156">我們將使用順序類別搭配驗證屬性來運用驗證規則</span><span class="sxs-lookup"><span data-stu-id="b2d57-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="b2d57-157">首先，我們將更新表單程式碼來使用 EditorForModel （），然後再加上促銷代碼的額外文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b2d57-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="b2d57-158">AddressAndPayment view 的完整程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="b2d57-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="b2d57-159">定義訂單的驗證規則</span><span class="sxs-lookup"><span data-stu-id="b2d57-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="b2d57-160">我們已設定好我們的視圖，接下來我們會設定訂單模型的驗證規則，就像先前針對專輯模型所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="b2d57-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="b2d57-161">以滑鼠右鍵按一下 [模型] 資料夾，然後新增名為 Order 的類別。</span><span class="sxs-lookup"><span data-stu-id="b2d57-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="b2d57-162">除了我們先前針對專輯使用的驗證屬性以外，我們也會使用正則運算式來驗證使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b2d57-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="b2d57-163">嘗試提交具有遺失或無效資訊的表單，現在會使用用戶端驗證來顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b2d57-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="b2d57-164">好的，我們已完成簽出程式的大部分困難的工作;我們只會有一些機率，並結束完成。</span><span class="sxs-lookup"><span data-stu-id="b2d57-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="b2d57-165">我們需要新增兩個簡單的視圖，而且我們需要在登入程式期間，負責交付購物車資訊。</span><span class="sxs-lookup"><span data-stu-id="b2d57-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="b2d57-166">加入結帳完整視圖</span><span class="sxs-lookup"><span data-stu-id="b2d57-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="b2d57-167">[結帳完成] 視圖非常簡單，因為它只需要顯示訂單識別碼。</span><span class="sxs-lookup"><span data-stu-id="b2d57-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="b2d57-168">以滑鼠右鍵按一下 [完成控制器] 動作，並新增名為 [完成] 的視圖，其強型別為 int。</span><span class="sxs-lookup"><span data-stu-id="b2d57-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="b2d57-169">現在，我們將更新 view 程式碼以顯示訂單識別碼，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b2d57-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="b2d57-170">正在更新錯誤視圖</span><span class="sxs-lookup"><span data-stu-id="b2d57-170">Updating The Error view</span></span>

<span data-ttu-id="b2d57-171">預設範本會在 [共用的 views] 資料夾中包含錯誤視圖，以便在網站中的其他地方重複使用。</span><span class="sxs-lookup"><span data-stu-id="b2d57-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="b2d57-172">這個錯誤視圖包含非常簡單的錯誤，而且不會使用我們的網站版面配置，所以我們會進行更新。</span><span class="sxs-lookup"><span data-stu-id="b2d57-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="b2d57-173">由於這是一般錯誤網頁，內容非常簡單。</span><span class="sxs-lookup"><span data-stu-id="b2d57-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="b2d57-174">如果使用者想要重新嘗試其動作，我們會包含訊息和連結，以流覽至歷程記錄中的上一頁。</span><span class="sxs-lookup"><span data-stu-id="b2d57-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> <span data-ttu-id="b2d57-175">[上一頁](mvc-music-store-part-8.md)
> [下一頁](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="b2d57-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
