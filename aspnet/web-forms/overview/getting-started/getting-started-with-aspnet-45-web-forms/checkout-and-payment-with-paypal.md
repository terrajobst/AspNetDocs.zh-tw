---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 簽出與使用 PayPal 付款 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78565405"
---
# <a name="checkout-and-payment-with-paypal"></a><span data-ttu-id="f5a39-103">簽出與使用 PayPal 付款</span><span class="sxs-lookup"><span data-stu-id="f5a39-103">Checkout and Payment with PayPal</span></span>

<span data-ttu-id="f5a39-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="f5a39-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="f5a39-105">[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="f5a39-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="f5a39-106">本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="f5a39-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="f5a39-107">本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="f5a39-108">本教學課程說明如何修改 Wingtip 玩具範例應用程式，以包含使用 PayPal 的使用者授權、註冊和付款。</span><span class="sxs-lookup"><span data-stu-id="f5a39-108">This tutorial describes how to modify the Wingtip Toys sample application to include user authorization, registration, and payment using PayPal.</span></span> <span data-ttu-id="f5a39-109">只有登入的使用者才會擁有購買產品的授權。</span><span class="sxs-lookup"><span data-stu-id="f5a39-109">Only users who are logged in will have authorization to purchase products.</span></span> <span data-ttu-id="f5a39-110">ASP.NET 4.5 Web form 專案範本的內建使用者註冊功能已包含您所需的大部分內容。</span><span class="sxs-lookup"><span data-stu-id="f5a39-110">The ASP.NET 4.5 Web Forms project template's built-in user registration functionality already includes much of what you need.</span></span> <span data-ttu-id="f5a39-111">您將新增 PayPal 快速簽出功能。</span><span class="sxs-lookup"><span data-stu-id="f5a39-111">You will add PayPal Express Checkout functionality.</span></span> <span data-ttu-id="f5a39-112">在本教學課程中，您將使用 PayPal 開發人員測試環境，因此不會傳輸實際的資金。</span><span class="sxs-lookup"><span data-stu-id="f5a39-112">In this tutorial you be using the PayPal developer testing environment, so no actual funds will be transferred.</span></span> <span data-ttu-id="f5a39-113">在本教學課程結束時，您將會藉由選取要加入購物車的產品、按一下 [結帳] 按鈕，然後將資料傳送到 PayPal 測試網站，來測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-113">At the end of the tutorial, you will test the application by selecting products to add to the shopping cart, clicking the checkout button, and transferring data to the PayPal testing web site.</span></span> <span data-ttu-id="f5a39-114">在 PayPal 測試網站上，您將會確認您的寄送和付款資訊，然後返回當地的 Wingtip 玩具範例應用程式，以確認並完成購買。</span><span class="sxs-lookup"><span data-stu-id="f5a39-114">On the PayPal testing web site, you will confirm your shipping and payment information and then return to the local Wingtip Toys sample application to confirm and complete the purchase.</span></span>

<span data-ttu-id="f5a39-115">有幾個經驗豐富的協力廠商付款處理器，專門用來解決擴充性和安全性的線上購物。</span><span class="sxs-lookup"><span data-stu-id="f5a39-115">There are several experienced third-party payment processors that specialize in online shopping that address scalability and security.</span></span> <span data-ttu-id="f5a39-116">ASP.NET 開發人員應該先考慮使用協力廠商付款解決方案的優點，再執行購物和購買解決方案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-116">ASP.NET developers should consider the advantages of utilizing a third party payment solution before implementing a shopping and purchasing solution.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5a39-117">Wingtip 玩具範例應用程式的設計，是為了示範 ASP.NET 網頁程式開發人員所能使用的特定 ASP.NET 概念和功能。</span><span class="sxs-lookup"><span data-stu-id="f5a39-117">The Wingtip Toys sample application was designed to shown specific ASP.NET concepts and features available to ASP.NET web developers.</span></span> <span data-ttu-id="f5a39-118">這個範例應用程式未針對擴充性和安全性方面的所有可能情況進行優化。</span><span class="sxs-lookup"><span data-stu-id="f5a39-118">This sample application was not optimized for all possible circumstances in regard to scalability and security.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f5a39-119">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="f5a39-119">What you'll learn:</span></span>

- <span data-ttu-id="f5a39-120">如何限制對資料夾中特定頁面的存取。</span><span class="sxs-lookup"><span data-stu-id="f5a39-120">How to restrict access to specific pages in a folder.</span></span>
- <span data-ttu-id="f5a39-121">如何從匿名購物車建立已知的購物車。</span><span class="sxs-lookup"><span data-stu-id="f5a39-121">How to create a known shopping cart from an anonymous shopping cart.</span></span>
- <span data-ttu-id="f5a39-122">如何為專案啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="f5a39-122">How to enable SSL for the project.</span></span>
- <span data-ttu-id="f5a39-123">如何將 OAuth 提供者新增至專案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-123">How to add an OAuth provider to the project.</span></span>
- <span data-ttu-id="f5a39-124">如何使用 paypal 來購買使用 PayPal 測試環境的產品。</span><span class="sxs-lookup"><span data-stu-id="f5a39-124">How to use PayPal to purchase products using the PayPal testing environment.</span></span>
- <span data-ttu-id="f5a39-125">如何在**DetailsView**控制項中顯示 PayPal 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-125">How to display details from PayPal in a **DetailsView** control.</span></span>
- <span data-ttu-id="f5a39-126">如何使用從 PayPal 取得的詳細資料來更新 Wingtip 玩具應用程式的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5a39-126">How to update the database of the Wingtip Toys application with details obtained from PayPal.</span></span>

## <a name="adding-order-tracking"></a><span data-ttu-id="f5a39-127">新增訂單追蹤</span><span class="sxs-lookup"><span data-stu-id="f5a39-127">Adding Order Tracking</span></span>

<span data-ttu-id="f5a39-128">在本教學課程中，您將建立兩個新的類別，以根據使用者建立的順序來追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-128">In this tutorial, you'll create two new classes to track data from the order a user has created.</span></span> <span data-ttu-id="f5a39-129">這些類別會追蹤有關運送資訊、購買總計和付款確認的資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-129">The classes will track data regarding shipping information, purchase total, and payment confirmation.</span></span>

### <a name="add-the-order-and-orderdetail-model-classes"></a><span data-ttu-id="f5a39-130">加入 Order 和 OrderDetail 模型類別</span><span class="sxs-lookup"><span data-stu-id="f5a39-130">Add the Order and OrderDetail Model Classes</span></span>

<span data-ttu-id="f5a39-131">稍早在本教學課程系列中，您可以藉由在 [*模型*] 資料夾中建立 `Category`、`Product`和 `CartItem` 類別，來定義類別目錄、產品和購物車專案的架構。</span><span class="sxs-lookup"><span data-stu-id="f5a39-131">Earlier in this tutorial series, you defined the schema for categories, products, and shopping cart items by creating the `Category`, `Product`, and `CartItem` classes in the *Models* folder.</span></span> <span data-ttu-id="f5a39-132">現在您將加入兩個新的類別，以定義產品訂單的架構和訂單的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-132">Now you will add two new classes to define the schema for the product order and the details of the order.</span></span>

1. <span data-ttu-id="f5a39-133">在 [**模型**] 資料夾中，加入名為*Order.cs*的新類別。</span><span class="sxs-lookup"><span data-stu-id="f5a39-133">In the **Models** folder, add a new class named *Order.cs*.</span></span>   
   <span data-ttu-id="f5a39-134">新的類別檔案會顯示在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="f5a39-134">The new class file is displayed in the editor.</span></span>
2. <span data-ttu-id="f5a39-135">使用下列項目取代預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="f5a39-135">Replace the default code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. <span data-ttu-id="f5a39-136">將*OrderDetail.cs*類別新增至 [*模型*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f5a39-136">Add an *OrderDetail.cs* class to the *Models* folder.</span></span>
4. <span data-ttu-id="f5a39-137">使用下列程式碼來取代預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="f5a39-137">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

<span data-ttu-id="f5a39-138">`Order` 和 `OrderDetail` 類別包含用來定義用於購買和出貨之訂單資訊的架構。</span><span class="sxs-lookup"><span data-stu-id="f5a39-138">The `Order` and `OrderDetail` classes contain the schema to define the order information used for purchasing and shipping.</span></span>

<span data-ttu-id="f5a39-139">此外，您還需要更新管理實體類別的資料庫內容類別，並提供資料庫的資料存取權。</span><span class="sxs-lookup"><span data-stu-id="f5a39-139">In addition, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="f5a39-140">若要這樣做，您要將新建立的順序和 `OrderDetail` 模型類別加入 `ProductContext` 類別。</span><span class="sxs-lookup"><span data-stu-id="f5a39-140">To do this, you will add the newly created Order and `OrderDetail` model classes to `ProductContext` class.</span></span>

1. <span data-ttu-id="f5a39-141">在**方案總管**中，尋找並開啟*ProductCoNtext.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-141">In **Solution Explorer**, find and open the *ProductContext.cs* file.</span></span>
2. <span data-ttu-id="f5a39-142">將反白顯示的程式碼新增至*ProductCoNtext.cs*檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5a39-142">Add the highlighted code to the *ProductContext.cs* file as shown below:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

<span data-ttu-id="f5a39-143">如先前在本教學課程系列中所述， *ProductCoNtext.cs*檔案中的程式碼會新增 `System.Data.Entity` 命名空間，讓您可以存取 Entity Framework 的所有核心功能。</span><span class="sxs-lookup"><span data-stu-id="f5a39-143">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="f5a39-144">這項功能包括使用強型別物件來查詢、插入、更新和刪除資料的功能。</span><span class="sxs-lookup"><span data-stu-id="f5a39-144">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="f5a39-145">在 `ProductContext` 類別中的上述程式碼會加入 Entity Framework 存取新增的 `Order` 和 `OrderDetail` 類別。</span><span class="sxs-lookup"><span data-stu-id="f5a39-145">The above code in the `ProductContext` class adds Entity Framework access to the newly added `Order` and `OrderDetail` classes.</span></span>

## <a name="adding-checkout-access"></a><span data-ttu-id="f5a39-146">新增簽出存取權</span><span class="sxs-lookup"><span data-stu-id="f5a39-146">Adding Checkout Access</span></span>

<span data-ttu-id="f5a39-147">Wingtip 玩具範例應用程式可讓匿名使用者進行審查，並將產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="f5a39-147">The Wingtip Toys sample application allows anonymous users to review and add products to a shopping cart.</span></span> <span data-ttu-id="f5a39-148">不過，當匿名使用者選擇購買他們新增至購物車的產品時，他們必須登入網站。</span><span class="sxs-lookup"><span data-stu-id="f5a39-148">However, when anonymous users choose to purchase the products they added to the shopping cart, they must log on to the site.</span></span> <span data-ttu-id="f5a39-149">登入之後，他們就可以存取處理結帳和購買程式的 Web 應用程式限制頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-149">Once they have logged on, they can access the restricted pages of the Web application that handle the checkout and purchase process.</span></span> <span data-ttu-id="f5a39-150">這些限制的頁面會包含在應用程式的 [*結帳*] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f5a39-150">These restricted pages are contained in the *Checkout* folder of the application.</span></span>

### <a name="add-a-checkout-folder-and-pages"></a><span data-ttu-id="f5a39-151">新增簽出資料夾和頁面</span><span class="sxs-lookup"><span data-stu-id="f5a39-151">Add a Checkout Folder and Pages</span></span>

<span data-ttu-id="f5a39-152">您現在將會建立 [*結帳*] 資料夾，以及客戶會在結帳程式中看到的頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-152">You will now create the *Checkout* folder and the pages in it that the customer will see during the checkout process.</span></span> <span data-ttu-id="f5a39-153">您稍後會在本教學課程中更新這些頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-153">You will update these pages later in this tutorial.</span></span>

1. <span data-ttu-id="f5a39-154">在**方案總管**中，以滑鼠右鍵按一下專案名稱（**Wingtip 玩具**），然後選取 [**新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-154">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add a New Folder**.</span></span> 

    ![使用 PayPal 簽出和付款-新的資料夾](checkout-and-payment-with-paypal/_static/image1.png)
2. <span data-ttu-id="f5a39-156">將新資料夾命名為*Checkout*。</span><span class="sxs-lookup"><span data-stu-id="f5a39-156">Name the new folder *Checkout*.</span></span>
3. <span data-ttu-id="f5a39-157">以滑鼠右鍵按一下 [*簽出*] 資料夾，**然後選取 [** 新增-&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-157">Right-click the *Checkout* folder and then select **Add**-&gt;**New Item**.</span></span> 

    ![使用 PayPal 簽出和付款-新專案](checkout-and-payment-with-paypal/_static/image2.png)
4. <span data-ttu-id="f5a39-159">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5a39-159">The **Add New Item** dialog box is displayed.</span></span>
5. <span data-ttu-id="f5a39-160">選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="f5a39-160">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="f5a39-161">然後，在中間窗格中，選取 [**使用主版頁面的 Web 表單**]，並將它命名為*CheckoutStart .aspx*。</span><span class="sxs-lookup"><span data-stu-id="f5a39-161">Then, from the middle pane, select **Web Form with Master Page**and name it *CheckoutStart.aspx*.</span></span> 

    ![使用 PayPal 簽出和付款-加入新專案對話方塊](checkout-and-payment-with-paypal/_static/image3.png)
6. <span data-ttu-id="f5a39-163">如先前所示，請選取 [*網站*] 檔案作為主版頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-163">As before, select the *Site.Master* file as the master page.</span></span>
7. <span data-ttu-id="f5a39-164">使用上述相同步驟，將下列其他頁面新增至 [*簽出*] 資料夾：</span><span class="sxs-lookup"><span data-stu-id="f5a39-164">Add the following additional pages to the *Checkout* folder using the same steps above:</span></span>   

    - <span data-ttu-id="f5a39-165">CheckoutReview .aspx</span><span class="sxs-lookup"><span data-stu-id="f5a39-165">CheckoutReview.aspx</span></span>
    - <span data-ttu-id="f5a39-166">CheckoutComplete .aspx</span><span class="sxs-lookup"><span data-stu-id="f5a39-166">CheckoutComplete.aspx</span></span>
    - <span data-ttu-id="f5a39-167">CheckoutCancel .aspx</span><span class="sxs-lookup"><span data-stu-id="f5a39-167">CheckoutCancel.aspx</span></span>
    - <span data-ttu-id="f5a39-168">CheckoutError .aspx</span><span class="sxs-lookup"><span data-stu-id="f5a39-168">CheckoutError.aspx</span></span>

### <a name="add-a-webconfig-file"></a><span data-ttu-id="f5a39-169">新增 Web.config 檔案</span><span class="sxs-lookup"><span data-stu-id="f5a39-169">Add a Web.config File</span></span>

<span data-ttu-id="f5a39-170">藉由*將新的 web.config 檔案*新增至 [*簽出*] 資料夾，您就能夠限制對該資料夾中包含的所有頁面進行存取。</span><span class="sxs-lookup"><span data-stu-id="f5a39-170">By adding a new *Web.config* file to the *Checkout* folder, you will be able to restrict access to all the pages contained in the folder.</span></span>

1. <span data-ttu-id="f5a39-171">以滑鼠右鍵按一下 [*簽出*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-171">Right-click the *Checkout* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="f5a39-172">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5a39-172">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="f5a39-173">選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="f5a39-173">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="f5a39-174">然後，在中間窗格中選取 [ **Web 設定檔**]，接受*web.config*的預設名稱，然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-174">Then, from the middle pane, select **Web Configuration File**, accept the default name of *Web.config*, and then select **Add**.</span></span>
3. <span data-ttu-id="f5a39-175">使用下列內容來取代 *Web.config* 檔案中的現有 XML 內容：</span><span class="sxs-lookup"><span data-stu-id="f5a39-175">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. <span data-ttu-id="f5a39-176">儲存 *Web.config* 檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-176">Save the *Web.config* file.</span></span>

<span data-ttu-id="f5a39-177">Web.config*檔案*會指定 web 應用程式的所有未知使用者都必須被拒絕存取*簽出*資料夾中包含的頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-177">The *Web.config* file specifies that all unknown users of the Web application must be denied access to the pages contained in the *Checkout* folder.</span></span> <span data-ttu-id="f5a39-178">不過，如果使用者已註冊帳戶並登入，他們會是已知的使用者，而且可以存取 [*簽出*] 資料夾中的頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-178">However, if the user has registered an account and is logged on, they will be a known user and will have access to the pages in the *Checkout* folder.</span></span>

<span data-ttu-id="f5a39-179">請務必注意，ASP.NET 設定會遵循階層，其中每個*web.config*檔案會將設定值套用至其所在的資料夾，以及其底下的所有子目錄。</span><span class="sxs-lookup"><span data-stu-id="f5a39-179">It's important to note that ASP.NET configuration follows a hierarchy, where each *Web.config* file applies configuration settings to the folder that it is in and to all of the child directories below it.</span></span>

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="f5a39-180">對專案啟用 SSL</span><span class="sxs-lookup"><span data-stu-id="f5a39-180">Enable SSL for the Project</span></span>

 <span data-ttu-id="f5a39-181">安全通訊端層 (SSL) 是一種定義的通訊協定，允許 Web 伺服器和 Web 用戶端透過加密，以更安全的方式進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f5a39-181">Secure Sockets Layer (SSL) is a protocol defined to allow Web servers and Web clients to communicate more securely through the use of encryption.</span></span> <span data-ttu-id="f5a39-182">未使用 SSL 時，在用戶端和伺服器之間傳送的資料會開放給任何可實體存取網路的人員進行封包探查。</span><span class="sxs-lookup"><span data-stu-id="f5a39-182">When SSL is not used, data sent between the client and server is open to packet sniffing by anyone with physical access to the network.</span></span> <span data-ttu-id="f5a39-183">此外，數種常見驗證結構描述在一般的 HTTP 上並不是很安全。</span><span class="sxs-lookup"><span data-stu-id="f5a39-183">Additionally, several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="f5a39-184">尤其是，基本驗證和表單驗證會傳送未加密的認證。</span><span class="sxs-lookup"><span data-stu-id="f5a39-184">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="f5a39-185">為了安全的理由，這些驗證結構描述必須使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="f5a39-185">To be secure, these authentication schemes must use SSL.</span></span> 

1. <span data-ttu-id="f5a39-186">在**方案總管**中，按一下 [ **WingtipToys** ] 專案，然後按**F4**顯示 [**屬性**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f5a39-186">In **Solution Explorer**, click the **WingtipToys** project, then press **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="f5a39-187">將 [ **SSL 已啟用**] 變更為 `true`。</span><span class="sxs-lookup"><span data-stu-id="f5a39-187">Change **SSL Enabled** to `true`.</span></span>
3. <span data-ttu-id="f5a39-188">複製 **SSL URL** ，以便稍後使用。</span><span class="sxs-lookup"><span data-stu-id="f5a39-188">Copy the **SSL URL** so you can use it later.</span></span>   
 <span data-ttu-id="f5a39-189">除非您先前已建立 SSL 網站（如下所示），否則 SSL URL 將會 `https://localhost:44300/`。</span><span class="sxs-lookup"><span data-stu-id="f5a39-189">The SSL URL will be `https://localhost:44300/` unless you've previously created SSL Web Sites (as shown below).</span></span>   
    <span data-ttu-id="f5a39-190">![專案屬性](checkout-and-payment-with-paypal/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-190">![Project Properties](checkout-and-payment-with-paypal/_static/image4.png)</span></span>
4. <span data-ttu-id="f5a39-191">在**方案總管**中，以滑鼠右鍵按一下**WingtipToys**專案，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-191">In **Solution Explorer**, right click the **WingtipToys** project and click **Properties**.</span></span>
5. <span data-ttu-id="f5a39-192">在左側索引標籤中按一下 [Web]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-192">In the left tab, click **Web**.</span></span>
6. <span data-ttu-id="f5a39-193">將 [**專案 Url** ] 變更為使用您稍早儲存的**SSL Url** 。</span><span class="sxs-lookup"><span data-stu-id="f5a39-193">Change the **Project Url** to use the **SSL URL** that you saved earlier.</span></span>   
    <span data-ttu-id="f5a39-194">![專案 Web 屬性](checkout-and-payment-with-paypal/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-194">![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)</span></span>
7. <span data-ttu-id="f5a39-195">按 **CTRL+S**儲存頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-195">Save the page by pressing **CTRL+S**.</span></span>
8. <span data-ttu-id="f5a39-196">按 **CTRL+F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-196">Press **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="f5a39-197">Visual Studio 將會顯示可避開 SSL 警告的選項。</span><span class="sxs-lookup"><span data-stu-id="f5a39-197">Visual Studio will display an option to allow you to avoid SSL warnings.</span></span>
9. <span data-ttu-id="f5a39-198">按一下 [ **是** ] 以信任 IIS Express SSL 憑證並繼續。</span><span class="sxs-lookup"><span data-stu-id="f5a39-198">Click **Yes** to trust the IIS Express SSL certificate and continue.</span></span>   
    <span data-ttu-id="f5a39-199">![IIS Express SSL 憑證資訊](checkout-and-payment-with-paypal/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-199">![IIS Express SSL certificate details](checkout-and-payment-with-paypal/_static/image6.png)</span></span>  
 <span data-ttu-id="f5a39-200">隨即顯示一則安全性警告。</span><span class="sxs-lookup"><span data-stu-id="f5a39-200">A Security Warning is displayed.</span></span>
10. <span data-ttu-id="f5a39-201">按一下 [ **是** ] 將憑證安裝到您的 localhost。</span><span class="sxs-lookup"><span data-stu-id="f5a39-201">Click **Yes** to install the certificate to your localhost.</span></span>   
    <span data-ttu-id="f5a39-202">![[安全性警告] 對話方塊](checkout-and-payment-with-paypal/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-202">![Security Warning dialog box](checkout-and-payment-with-paypal/_static/image7.png)</span></span>  
 <span data-ttu-id="f5a39-203">瀏覽器視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f5a39-203">The browser window will be displayed.</span></span>

<span data-ttu-id="f5a39-204">您現在可以使用 SSL，輕鬆地在本機測試 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-204">You can now easily test your Web application locally using SSL.</span></span>

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a><span data-ttu-id="f5a39-205">新增 OAuth 2.0 提供者</span><span class="sxs-lookup"><span data-stu-id="f5a39-205">Add an OAuth 2.0 Provider</span></span>

<span data-ttu-id="f5a39-206">ASP.NET Web Forms 提供成員資格和驗證的增強功能選項。</span><span class="sxs-lookup"><span data-stu-id="f5a39-206">ASP.NET Web Forms provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="f5a39-207">這些增強功能包括 OAuth。</span><span class="sxs-lookup"><span data-stu-id="f5a39-207">These enhancements include OAuth.</span></span> <span data-ttu-id="f5a39-208">OAuth 是一種開放式通訊協定，可讓 Web、行動和桌面應用程式以簡單、標準的方法執行安全授權。</span><span class="sxs-lookup"><span data-stu-id="f5a39-208">OAuth is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="f5a39-209">ASP.NET Web Forms 範本會使用 OAuth 將 Facebook、Twitter、Google 和 Microsoft 公開為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="f5a39-209">The ASP.NET Web Forms template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="f5a39-210">雖然本教學課程僅使用 Google 作為驗證提供者，但您可以輕易修改程式碼來使用任何提供者。</span><span class="sxs-lookup"><span data-stu-id="f5a39-210">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of the providers.</span></span> <span data-ttu-id="f5a39-211">實作其他提供者的步驟，與您將在本教學課程中看到的步驟極為類似。</span><span class="sxs-lookup"><span data-stu-id="f5a39-211">The steps to implement other providers are very similar to the steps you will see in this tutorial.</span></span>

<span data-ttu-id="f5a39-212">除了驗證，本教學課程也會使用角色來實作授權。</span><span class="sxs-lookup"><span data-stu-id="f5a39-212">In addition to authentication, the tutorial will also use roles to implement authorization.</span></span> <span data-ttu-id="f5a39-213">只有您新增至 `canEdit` 角色的使用者才能建立、編輯或刪除連絡人。</span><span class="sxs-lookup"><span data-stu-id="f5a39-213">Only those users you add to the `canEdit` role will be able to change data (create, edit, or delete contacts).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5a39-214">Windows Live 應用程式只接受工作網站的即時 URL，因此您無法使用本機網站 URL 來測試登入。</span><span class="sxs-lookup"><span data-stu-id="f5a39-214">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>

<span data-ttu-id="f5a39-215">下列步驟可新增 Google 驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="f5a39-215">The following steps will allow you to add a Google authentication provider.</span></span>

1. <span data-ttu-id="f5a39-216">開啟*應用程式\_Start\Startup.Auth.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-216">Open the *App\_Start\Startup.Auth.cs* file.</span></span>
2. <span data-ttu-id="f5a39-217">移除 `app.UseGoogleAuthentication()` 方法中的註解字元，然後此方法會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="f5a39-217">Remove the comment characters from the `app.UseGoogleAuthentication()` method so that the method appears as follows:</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. <span data-ttu-id="f5a39-218">瀏覽至 [Google Developers Console](https://console.developers.google.com/)。</span><span class="sxs-lookup"><span data-stu-id="f5a39-218">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span> <span data-ttu-id="f5a39-219">您還需要使用您的 Google 開發人員電子郵件帳戶 (gmail.com) 登入。</span><span class="sxs-lookup"><span data-stu-id="f5a39-219">You will also need to sign-in with your Google developer email account (gmail.com).</span></span> <span data-ttu-id="f5a39-220">如果您沒有 Google 帳戶，請選取 [ **建立帳戶** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="f5a39-220">If you do not have a Google account, select the **Create an account** link.</span></span>   
   <span data-ttu-id="f5a39-221">接下來，您會看到 [ **Google 開發人員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-221">Next, you'll see the **Google Developers Console**.</span></span>   
    <span data-ttu-id="f5a39-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span></span>
4. <span data-ttu-id="f5a39-223">按一下 [**建立專案**] 按鈕，然後輸入 [專案名稱] 和 [識別碼] （您可以使用預設值）。</span><span class="sxs-lookup"><span data-stu-id="f5a39-223">Click the **Create Project** button and enter a project name and ID (you can use the default values).</span></span> <span data-ttu-id="f5a39-224">然後按一下 [**合約] 核取方塊**和 [**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5a39-224">Then, click the **agreement checkbox** and the **Create** button.</span></span>  

    ![Google-新增專案](checkout-and-payment-with-paypal/_static/image9.png)

   <span data-ttu-id="f5a39-226">幾秒鐘內即可建立新的專案，您的瀏覽器便會顯示新的專案頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-226">In a few seconds the new project will be created and your browser will display the new projects page.</span></span>
5. <span data-ttu-id="f5a39-227">在左側索引標籤中，按一下 [ **api &amp; auth**]，然後按一下 [**認證**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-227">In the left tab, click **APIs &amp; auth**, and then click **Credentials**.</span></span>
6. <span data-ttu-id="f5a39-228">按一下 [ **OAuth**] 底下的 [**建立新的用戶端識別碼**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-228">Click the **Create New Client ID** under **OAuth**.</span></span>   
   <span data-ttu-id="f5a39-229">[ **建立用戶端識別碼** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f5a39-229">The **Create Client ID** dialog will be displayed.</span></span>   
    <span data-ttu-id="f5a39-230">![Google -  建立用戶端識別碼](checkout-and-payment-with-paypal/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-230">![Google - Create Client ID](checkout-and-payment-with-paypal/_static/image10.png)</span></span>
7. <span data-ttu-id="f5a39-231">在 [**建立用戶端識別碼**] 對話方塊中，保留應用程式類型的預設**Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f5a39-231">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
8. <span data-ttu-id="f5a39-232">將**授權的 JavaScript 來源**設定為您稍早在本教學課程中使用的 SSL URL （除非您已建立其他 SSL 專案，否則`https://localhost:44300/`）。</span><span class="sxs-lookup"><span data-stu-id="f5a39-232">Set the **Authorized JavaScript Origins** to the SSL URL you used earlier in this tutorial (`https://localhost:44300/` unless you've created other SSL projects).</span></span>   
   <span data-ttu-id="f5a39-233">此 URL 會是應用程式的原始來源。</span><span class="sxs-lookup"><span data-stu-id="f5a39-233">This URL is the origin for your application.</span></span> <span data-ttu-id="f5a39-234">在此範例中，您將僅輸入 localhost 測試 URL。</span><span class="sxs-lookup"><span data-stu-id="f5a39-234">For this sample, you will only enter the localhost test URL.</span></span> <span data-ttu-id="f5a39-235">不過，您可以輸入多個 Url 來考慮 localhost 和生產環境。</span><span class="sxs-lookup"><span data-stu-id="f5a39-235">However, you can enter multiple URLs to account for localhost and production.</span></span>
9. <span data-ttu-id="f5a39-236">將 [Authorized Redirect URI] 設定如下：</span><span class="sxs-lookup"><span data-stu-id="f5a39-236">Set the **Authorized Redirect URI** to the following:</span></span> 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   <span data-ttu-id="f5a39-237">此值是 ASP.NET OAuth 使用者與 Google OAuth 伺服器進行通訊的 URI。</span><span class="sxs-lookup"><span data-stu-id="f5a39-237">This value is the URI that ASP.NET OAuth users to communicate with the google OAuth server.</span></span> <span data-ttu-id="f5a39-238">請記住您先前使用的 SSL URL （除非您已建立其他 SSL 專案，否則 `https://localhost:44300/`）。</span><span class="sxs-lookup"><span data-stu-id="f5a39-238">Remember the SSL URL you used above (    `https://localhost:44300/` unless you've created other SSL projects).</span></span>
10. <span data-ttu-id="f5a39-239">按一下 [**建立用戶端識別碼**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5a39-239">Click the **Create Client ID** button.</span></span>
11. <span data-ttu-id="f5a39-240">在 Google 開發人員主控台的左側功能表上，按一下 [**同意畫面**] 功能表項目，然後設定您的電子郵件地址和產品名稱。</span><span class="sxs-lookup"><span data-stu-id="f5a39-240">On the left menu of the Google Developers Console, click the **Consent screen** menu item, then set your email address and product name.</span></span> <span data-ttu-id="f5a39-241">當您完成表單時，請按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-241">When you have completed the form, click **Save**.</span></span>
12. <span data-ttu-id="f5a39-242">按一下 [ **api** ] 功能表項目、向下流覽，然後按一下 [ **Google + API**] 旁的 [**關閉**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5a39-242">Click the **APIs** menu item, scroll down and click the **off** button next to **Google+ API**.</span></span>   
    <span data-ttu-id="f5a39-243">接受此選項將會啟用 Google + API。</span><span class="sxs-lookup"><span data-stu-id="f5a39-243">Accepting this option will enable the Google+ API.</span></span>
13. <span data-ttu-id="f5a39-244">您也必須將**Owin** NuGet 套件更新為版本3.0.0。</span><span class="sxs-lookup"><span data-stu-id="f5a39-244">You must also update the **Microsoft.Owin** NuGet package to version 3.0.0.</span></span>   
    <span data-ttu-id="f5a39-245">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**管理方案的 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-245">From the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages for Solution**.</span></span>  
    <span data-ttu-id="f5a39-246">從 [**管理 NuGet 封裝**] 視窗中，尋找**Owin**套件並將其更新為版本3.0.0。</span><span class="sxs-lookup"><span data-stu-id="f5a39-246">From the **Manage NuGet Packages** window, find and update the **Microsoft.Owin** package to version 3.0.0.</span></span>
14. <span data-ttu-id="f5a39-247">在 Visual Studio 中，將**用戶端識別碼**和**用戶端密碼**複製並貼到方法中，以更新*Startup.Auth.cs*頁面的 `UseGoogleAuthentication` 方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-247">In Visual Studio, update the `UseGoogleAuthentication` method of the *Startup.Auth.cs* page by copying and pasting the **Client ID** and **Client Secret** into the method.</span></span> <span data-ttu-id="f5a39-248">以下顯示的**用戶端識別碼**和**用戶端秘密**值為範例，因此無法使用。</span><span class="sxs-lookup"><span data-stu-id="f5a39-248">The **Client ID** and **Client Secret** values shown below are samples and will not work.</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. <span data-ttu-id="f5a39-249">按 **CTRL+F5** 以建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-249">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="f5a39-250">按一下 [登入] 連結。</span><span class="sxs-lookup"><span data-stu-id="f5a39-250">Click the **Log in** link.</span></span>
16. <span data-ttu-id="f5a39-251">在 [**使用其他服務登入**] 底下，按一下 [ **Google**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-251">Under **Use another service to log in**, click **Google**.</span></span>  
    <span data-ttu-id="f5a39-252">![登入](checkout-and-payment-with-paypal/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-252">![Log in](checkout-and-payment-with-paypal/_static/image11.png)</span></span>
17. <span data-ttu-id="f5a39-253">如果您需要輸入認證，您會被重新導向至 Google 網站，您可以在此輸入認證。</span><span class="sxs-lookup"><span data-stu-id="f5a39-253">If you need to enter your credentials, you will be redirected to the google site where you will enter your credentials.</span></span>  
    ![Google - 登入](checkout-and-payment-with-paypal/_static/image12.png)
18. <span data-ttu-id="f5a39-255">在您輸入認證之後，系統會提示您將許可權授與您剛建立的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-255">After you enter your credentials, you will be prompted to give permissions to the web application you just created.</span></span>  
    ![專案預設服務帳戶](checkout-and-payment-with-paypal/_static/image13.png)
19. <span data-ttu-id="f5a39-257">按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-257">Click **Accept**.</span></span> <span data-ttu-id="f5a39-258">您現在會重新導向回到**WingtipToys**應用程式的 [**註冊**] 頁面，您可以在其中註冊 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-258">You will now be redirected back to the **Register** page of the **WingtipToys** application where you can register your Google account.</span></span>  
    <span data-ttu-id="f5a39-259">![以您的 Google 帳戶註冊](checkout-and-payment-with-paypal/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="f5a39-259">![Register with your Google Account](checkout-and-payment-with-paypal/_static/image14.png)</span></span>
20. <span data-ttu-id="f5a39-260">您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。</span><span class="sxs-lookup"><span data-stu-id="f5a39-260">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="f5a39-261">按一下 [**登入**]，如上所示。</span><span class="sxs-lookup"><span data-stu-id="f5a39-261">Click **Log in** as shown above.</span></span>

### <a name="modifying-login-functionality"></a><span data-ttu-id="f5a39-262">修改登入功能</span><span class="sxs-lookup"><span data-stu-id="f5a39-262">Modifying Login Functionality</span></span>

<span data-ttu-id="f5a39-263">如先前在本教學課程系列中所述，大部分的使用者註冊功能已包含在 ASP.NET Web form 範本中，預設為。</span><span class="sxs-lookup"><span data-stu-id="f5a39-263">As previously mentioned in this tutorial series, much of the user registration functionality has been included in the ASP.NET Web Forms template by default.</span></span> <span data-ttu-id="f5a39-264">現在您將修改預設的*Login* ，並*註冊 .aspx*頁面來呼叫 `MigrateCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-264">Now you will modify the default *Login.aspx* and *Register.aspx* pages to call the `MigrateCart` method.</span></span> <span data-ttu-id="f5a39-265">`MigrateCart` 方法會將新登入的使用者與匿名購物車產生關聯。</span><span class="sxs-lookup"><span data-stu-id="f5a39-265">The `MigrateCart` method associates a newly logged in user with an anonymous shopping cart.</span></span> <span data-ttu-id="f5a39-266">藉由建立使用者和購物車的關聯，Wingtip 玩具範例應用程式將能夠在造訪間維護使用者的購物車。</span><span class="sxs-lookup"><span data-stu-id="f5a39-266">By associating the user and shopping cart, the Wingtip Toys sample application will be able to maintain the shopping cart of the user between visits.</span></span>

1. <span data-ttu-id="f5a39-267">在**方案總管**中，尋找並開啟 [*帳戶*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f5a39-267">In **Solution Explorer**, find and open the *Account* folder.</span></span>
2. <span data-ttu-id="f5a39-268">修改名為*Login.aspx.cs*的程式碼後置頁面，以包含以黃色反白顯示的程式碼，讓它看起來如下：</span><span class="sxs-lookup"><span data-stu-id="f5a39-268">Modify the code-behind page named *Login.aspx.cs* to include the code highlighted in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. <span data-ttu-id="f5a39-269">儲存*Login.aspx.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-269">Save the *Login.aspx.cs* file.</span></span>

<span data-ttu-id="f5a39-270">現在，您可以忽略 `MigrateCart` 方法沒有定義的警告。</span><span class="sxs-lookup"><span data-stu-id="f5a39-270">For now, you can ignore the warning that there is no definition for the `MigrateCart` method.</span></span> <span data-ttu-id="f5a39-271">稍後在本教學課程中，您將會新增它。</span><span class="sxs-lookup"><span data-stu-id="f5a39-271">You will be adding it a bit later in this tutorial.</span></span>

<span data-ttu-id="f5a39-272">*Login.aspx.cs*程式碼後置檔案支援登入方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-272">The *Login.aspx.cs* code-behind file supports a LogIn method.</span></span> <span data-ttu-id="f5a39-273">藉由檢查 Login .aspx 頁面，您會看到此頁面包含 [登入] 按鈕，當您按一下 [在程式碼後置時觸發 `LogIn` 處理常式]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-273">By inspecting the Login.aspx page, you'll see that this page includes a "Log in" button that when click triggers the `LogIn` handler on the code-behind.</span></span>

<span data-ttu-id="f5a39-274">呼叫*Login.aspx.cs*上的 `Login` 方法時，會建立名為 `usersShoppingCart` 的購物車的新實例。</span><span class="sxs-lookup"><span data-stu-id="f5a39-274">When the `Login` method on the *Login.aspx.cs* is called, a new instance of the shopping cart named `usersShoppingCart` is created.</span></span> <span data-ttu-id="f5a39-275">購物車的識別碼（GUID）會被取出並設定為 `cartId` 變數。</span><span class="sxs-lookup"><span data-stu-id="f5a39-275">The ID of the shopping cart (a GUID) is retrieved and set to the `cartId` variable.</span></span> <span data-ttu-id="f5a39-276">然後，會呼叫 `MigrateCart` 方法，同時將 `cartId` 和登入使用者的名稱傳遞給這個方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-276">Then, the `MigrateCart` method is called, passing both the `cartId` and the name of the logged-in user to this method.</span></span> <span data-ttu-id="f5a39-277">遷移購物車時，用來識別匿名購物車的 GUID 會以使用者名稱取代。</span><span class="sxs-lookup"><span data-stu-id="f5a39-277">When the shopping cart is migrated, the GUID used to identify the anonymous shopping cart is replaced with the user name.</span></span>

<span data-ttu-id="f5a39-278">除了修改*Login.aspx.cs*程式碼後置檔案，以在使用者登入時遷移購物車時，您也必須修改*Register.aspx.cs 程式碼後*置檔案，以在使用者建立新帳戶並登入時遷移購物車。</span><span class="sxs-lookup"><span data-stu-id="f5a39-278">In addition to modifying the *Login.aspx.cs* code-behind file to migrate the shopping cart when the user logs in, you must also modify the *Register.aspx.cs code-behind file* to migrate the shopping cart when the user creates a new account and logs in.</span></span>

1. <span data-ttu-id="f5a39-279">在 [*帳戶*] 資料夾中，開啟名為*Register.aspx.cs*的程式碼後置檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-279">In the *Account* folder, open the code-behind file named *Register.aspx.cs*.</span></span>
2. <span data-ttu-id="f5a39-280">以黃色包含程式碼來修改程式碼後置檔案，讓它看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5a39-280">Modify the code-behind file by including the code in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. <span data-ttu-id="f5a39-281">儲存*Register.aspx.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-281">Save the *Register.aspx.cs* file.</span></span> <span data-ttu-id="f5a39-282">同樣地，忽略有關 `MigrateCart` 方法的警告。</span><span class="sxs-lookup"><span data-stu-id="f5a39-282">Once again, ignore the warning about the `MigrateCart` method.</span></span>

<span data-ttu-id="f5a39-283">請注意，您在 `CreateUser_Click` 事件處理常式中使用的程式碼，與您在 `LogIn` 方法中使用的程式碼非常類似。</span><span class="sxs-lookup"><span data-stu-id="f5a39-283">Notice that the code you used in the `CreateUser_Click` event handler is very similar to the code you used in the `LogIn` method.</span></span> <span data-ttu-id="f5a39-284">當使用者註冊或登入網站時，將會進行 `MigrateCart` 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="f5a39-284">When the user registers or logs in to the site, a call to the `MigrateCart` method will be made.</span></span>

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="f5a39-285">遷移購物車</span><span class="sxs-lookup"><span data-stu-id="f5a39-285">Migrating the Shopping Cart</span></span>

<span data-ttu-id="f5a39-286">現在您已更新登入和註冊程式，您可以使用 `MigrateCart` 方法來新增程式碼，以遷移購物車。</span><span class="sxs-lookup"><span data-stu-id="f5a39-286">Now that you have the log-in and registration process updated, you can add the code to migrate the shopping cart using the `MigrateCart` method.</span></span>

1. <span data-ttu-id="f5a39-287">在**方案總管**中，尋找*邏輯*資料夾並開啟*ShoppingCartActions.cs*類別檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-287">In **Solution Explorer**, find the *Logic* folder and open the *ShoppingCartActions.cs* class file.</span></span>
2. <span data-ttu-id="f5a39-288">將黃色反白顯示的程式碼新增至*ShoppingCartActions.cs*檔案中的現有程式碼，讓*ShoppingCartActions.cs*檔案中的程式碼顯示如下：</span><span class="sxs-lookup"><span data-stu-id="f5a39-288">Add the code highlighted in yellow to the existing code in the *ShoppingCartActions.cs* file, so that the code in the *ShoppingCartActions.cs* file appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

<span data-ttu-id="f5a39-289">`MigrateCart` 方法會使用現有的 cartId 來尋找使用者的購物車。</span><span class="sxs-lookup"><span data-stu-id="f5a39-289">The `MigrateCart` method uses the existing cartId to find the shopping cart of the user.</span></span> <span data-ttu-id="f5a39-290">接下來，程式碼會迴圈處理所有的購物車專案，並以登入的使用者名稱取代 `CartId` 屬性（如 `CartItem` 架構所指定）。</span><span class="sxs-lookup"><span data-stu-id="f5a39-290">Next, the code loops through all the shopping cart items and replaces the `CartId` property (as specified by the `CartItem` schema) with the logged-in user name.</span></span>

### <a name="updating-the-database-connection"></a><span data-ttu-id="f5a39-291">正在更新資料庫連接</span><span class="sxs-lookup"><span data-stu-id="f5a39-291">Updating the Database Connection</span></span>

<span data-ttu-id="f5a39-292">如果您使用**預先**建立的 Wingtip 玩具範例應用程式來遵循本教學課程，就必須重新建立預設的成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5a39-292">If you are following this tutorial using the **prebuilt** Wingtip Toys sample application, you must recreate the default membership database.</span></span> <span data-ttu-id="f5a39-293">藉由修改預設連接字串，將會在下一次執行應用程式時建立成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5a39-293">By modifying the default connection string, the membership database will be created the next time the application runs.</span></span>

1. <span data-ttu-id="f5a39-294">開啟位於專案根目錄的*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-294">Open the *Web.config* file at the root of the project.</span></span>
2. <span data-ttu-id="f5a39-295">更新預設連接字串，讓它看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5a39-295">Update the default connection string so that it appears as follows:</span></span>   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a><span data-ttu-id="f5a39-296">整合 PayPal</span><span class="sxs-lookup"><span data-stu-id="f5a39-296">Integrating PayPal</span></span>

<span data-ttu-id="f5a39-297">PayPal 是以網路為基礎的計費平臺，可接受線上商家的付款。</span><span class="sxs-lookup"><span data-stu-id="f5a39-297">PayPal is a web-based billing platform that accepts payments by online merchants.</span></span> <span data-ttu-id="f5a39-298">本教學課程將說明如何將 PayPal 的「快速簽出」功能整合到您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f5a39-298">This tutorial next explains how to integrate PayPal's Express Checkout functionality into your application.</span></span> <span data-ttu-id="f5a39-299">「快速簽出」可讓您的客戶使用 PayPal 來支付他們已新增至購物車的專案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-299">Express Checkout allows your customers to use PayPal to pay for the items they have added to their shopping cart.</span></span>

### <a name="create-paypal-test-accounts"></a><span data-ttu-id="f5a39-300">建立 PayPal 測試帳戶</span><span class="sxs-lookup"><span data-stu-id="f5a39-300">Create PayPal Test Accounts</span></span>

<span data-ttu-id="f5a39-301">若要使用 PayPal 測試環境，您必須建立並驗證開發人員測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-301">To use the PayPal testing environment, you must create and verify a developer test account.</span></span> <span data-ttu-id="f5a39-302">您將使用開發人員測試帳戶來建立買方測試帳戶和賣方測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-302">You will use the developer test account to create a buyer test account and a seller test account.</span></span> <span data-ttu-id="f5a39-303">開發人員測試帳號憑證也會允許 Wingtip 玩具範例應用程式存取 PayPal 測試環境。</span><span class="sxs-lookup"><span data-stu-id="f5a39-303">The developer test account credentials also will allow the Wingtip Toys sample application to access the PayPal testing environment.</span></span>

1. <span data-ttu-id="f5a39-304">在瀏覽器中，流覽至 PayPal 開發人員測試網站：</span><span class="sxs-lookup"><span data-stu-id="f5a39-304">In a browser, navigate to the PayPal developer testing site:</span></span>   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. <span data-ttu-id="f5a39-305">如果您沒有 PayPal 開發人員帳戶，請按一下 [**註冊**] 並遵循註冊步驟來建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-305">If you don't have a PayPal developer account, create a new account by clicking **Sign Up**and following the sign up steps.</span></span> <span data-ttu-id="f5a39-306">如果您有現有的 PayPal 開發人員帳戶，請按一下 [**登入**] 來登入。</span><span class="sxs-lookup"><span data-stu-id="f5a39-306">If you have an existing PayPal developer account, sign in by clicking **Log In**.</span></span> <span data-ttu-id="f5a39-307">稍後在本教學課程中，您將需要 PayPal 開發人員帳戶來測試 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-307">You will need your PayPal developer account to test the Wingtip Toys sample application later in this tutorial.</span></span>
3. <span data-ttu-id="f5a39-308">如果您剛註冊 PayPal 開發人員帳戶，您可能需要使用 PayPal 來驗證您的 PayPal 開發人員帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-308">If you have just signed up for your PayPal developer account, you may need to verify your PayPal developer account with PayPal.</span></span> <span data-ttu-id="f5a39-309">您可以遵循 PayPal 傳送至您的電子郵件帳戶的步驟來驗證您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-309">You can verify your account by following the steps that PayPal sent to your email account.</span></span> <span data-ttu-id="f5a39-310">確認您的 PayPal 開發人員帳戶之後，請重新登入 PayPal 開發人員測試網站。</span><span class="sxs-lookup"><span data-stu-id="f5a39-310">Once you have verified your PayPal developer account, log back into the PayPal developer testing site.</span></span>
4. <span data-ttu-id="f5a39-311">使用您的 PayPal 開發人員帳戶登入 PayPal 開發人員網站之後，您必須建立 PayPal 買方測試帳戶（如果還沒有的話）。</span><span class="sxs-lookup"><span data-stu-id="f5a39-311">After you are logged in to the PayPal developer site with your PayPal developer account you need to create a PayPal buyer test account if you don't already have one.</span></span> <span data-ttu-id="f5a39-312">若要建立買方測試帳戶，請在 PayPal 網站上按一下 [**應用程式**] 索引標籤，然後按一下 [**沙箱帳戶**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-312">To create a buyer test account, on the PayPal site click the **Applications** tab and then click **Sandbox accounts**.</span></span>   
 <span data-ttu-id="f5a39-313">[**沙箱測試帳戶**] 頁面隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f5a39-313">The **Sandbox test accounts** page is shown.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="f5a39-314">PayPal 開發人員網站已經供應商家測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-314">The PayPal Developer site already provides a merchant test account.</span></span>

    ![使用 PayPal 簽出和付款-沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image15.png)
5. <span data-ttu-id="f5a39-316">在 [沙箱測試帳戶] 頁面上，按一下 [**建立帳戶**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-316">On the Sandbox test accounts page, click **Create Account**.</span></span>
6. <span data-ttu-id="f5a39-317">在 [**建立測試帳戶**] 頁面上，選擇您選擇的買方測試帳戶電子郵件和密碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-317">On the **Create test account** page choose a buyer test account email and password of your choice.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="f5a39-318">在本教學課程結尾處，您將需要購買者的電子郵件地址和密碼，才能測試 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-318">You will need the buyer email addresses and password to test the Wingtip Toys sample application at the end of this tutorial.</span></span>

    ![使用 PayPal 簽出和付款-沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image16.png)
7. <span data-ttu-id="f5a39-320">按一下 [**建立帳戶**] 按鈕，以建立買方測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-320">Create the buyer test account by clicking the **Create Account** button.</span></span>  
 <span data-ttu-id="f5a39-321">[**沙箱測試帳戶**] 頁面隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f5a39-321">The **Sandbox Test accounts** page is displayed.</span></span> 

    ![使用 PayPal 簽出和付款-PayPal 帳戶](checkout-and-payment-with-paypal/_static/image17.png)
8. <span data-ttu-id="f5a39-323">在 [**沙箱測試帳戶**] 頁面上，按一下 [**主持**者電子郵件帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-323">On the **Sandbox test accounts** page, click the **facilitator** email account.</span></span>  
    <span data-ttu-id="f5a39-324">[**設定檔**] 和 [**通知**] 選項隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f5a39-324">**Profile** and **Notification** options appear.</span></span>
9. <span data-ttu-id="f5a39-325">選取 [**設定檔**] 選項，然後按一下 [ **API 認證**] 以查看您的商家測試帳戶的 api 認證。</span><span class="sxs-lookup"><span data-stu-id="f5a39-325">Select the **Profile** option, then click **API credentials** to view your API credentials for the merchant test account.</span></span>
10. <span data-ttu-id="f5a39-326">將測試 API 認證複製到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-326">Copy the TEST API credentials to notepad.</span></span>

<span data-ttu-id="f5a39-327">您將需要顯示的傳統測試 API 認證（使用者名稱、密碼和簽章），以從 Wingtip 玩具範例應用程式對 PayPal 測試環境進行 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f5a39-327">You will need your displayed Classic TEST API credentials (Username, Password, and Signature) to make API calls from the Wingtip Toys sample application to the PayPal testing environment.</span></span> <span data-ttu-id="f5a39-328">您會在下一個步驟中新增認證。</span><span class="sxs-lookup"><span data-stu-id="f5a39-328">You will add the credentials in the next step.</span></span>

### <a name="add-paypal-class-and-api-credentials"></a><span data-ttu-id="f5a39-329">新增 PayPal 類別和 API 認證</span><span class="sxs-lookup"><span data-stu-id="f5a39-329">Add PayPal Class and API Credentials</span></span>

<span data-ttu-id="f5a39-330">您會將大部分的 PayPal 程式碼放入單一類別中。</span><span class="sxs-lookup"><span data-stu-id="f5a39-330">You will place the majority of the PayPal code into a single class.</span></span> <span data-ttu-id="f5a39-331">此類別包含用來與 PayPal 通訊的方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-331">This class contains the methods used to communicate with PayPal.</span></span> <span data-ttu-id="f5a39-332">此外，您也會將您的 PayPal 認證新增至此類別。</span><span class="sxs-lookup"><span data-stu-id="f5a39-332">Also, you will add your PayPal credentials to this class.</span></span>

1. <span data-ttu-id="f5a39-333">在 Visual Studio 內的 Wingtip 玩具範例應用程式中，以滑鼠右鍵按一下**邏輯**資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-333">In the Wingtip Toys sample application within Visual Studio, right-click the **Logic** folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="f5a39-334">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5a39-334">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="f5a39-335">在左側 [**已安裝**] 窗格中的 [**視覺效果C#**  ] 底下，選取 [程式**代碼**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-335">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span>
3. <span data-ttu-id="f5a39-336">從中間窗格中，選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-336">From the middle pane, select **Class**.</span></span> <span data-ttu-id="f5a39-337">將這個新類別命名為**PayPalFunctions.cs**。</span><span class="sxs-lookup"><span data-stu-id="f5a39-337">Name this new class **PayPalFunctions.cs**.</span></span>
4. <span data-ttu-id="f5a39-338">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-338">Click **Add**.</span></span>  
   <span data-ttu-id="f5a39-339">新的類別檔案會顯示在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="f5a39-339">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="f5a39-340">使用下列程式碼來取代預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="f5a39-340">Replace the default code with the following code:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. <span data-ttu-id="f5a39-341">新增您稍早在本教學課程中所顯示的商家 API 認證（使用者名稱、密碼和簽章），讓您可以對 PayPal 測試環境進行函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="f5a39-341">Add the Merchant API credentials (Username, Password, and Signature) that you displayed earlier in this tutorial so that you can make function calls to the PayPal testing environment.</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="f5a39-342">在此範例應用程式中，您只需將C#認證新增至檔案（.cs）。</span><span class="sxs-lookup"><span data-stu-id="f5a39-342">In this sample application you are simply adding credentials to a C# file (.cs).</span></span> <span data-ttu-id="f5a39-343">不過，在已實行的解決方案中，您應該考慮在設定檔中加密您的認證。</span><span class="sxs-lookup"><span data-stu-id="f5a39-343">However, in a implemented solution, you should consider encrypting your credentials in a configuration file.</span></span>

<span data-ttu-id="f5a39-344">NVPAPICaller 類別包含大部分的 PayPal 功能。</span><span class="sxs-lookup"><span data-stu-id="f5a39-344">The NVPAPICaller class contains the majority of the PayPal functionality.</span></span> <span data-ttu-id="f5a39-345">類別中的程式碼提供從 PayPal 測試環境進行測試購買所需的方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-345">The code in the class provides the methods needed to make a test purchase from the PayPal testing environment.</span></span> <span data-ttu-id="f5a39-346">下列三個 PayPal 函數可用來進行購買：</span><span class="sxs-lookup"><span data-stu-id="f5a39-346">The following three PayPal functions are used to make purchases:</span></span>

- <span data-ttu-id="f5a39-347">`SetExpressCheckout` 函式</span><span class="sxs-lookup"><span data-stu-id="f5a39-347">`SetExpressCheckout` function</span></span>
- <span data-ttu-id="f5a39-348">`GetExpressCheckoutDetails` 函式</span><span class="sxs-lookup"><span data-stu-id="f5a39-348">`GetExpressCheckoutDetails` function</span></span>
- <span data-ttu-id="f5a39-349">`DoExpressCheckoutPayment` 函式</span><span class="sxs-lookup"><span data-stu-id="f5a39-349">`DoExpressCheckoutPayment` function</span></span>

<span data-ttu-id="f5a39-350">`ShortcutExpressCheckout` 方法會從購物車收集測試購買資訊和產品詳細資料，並呼叫 `SetExpressCheckout` PayPal 函數。</span><span class="sxs-lookup"><span data-stu-id="f5a39-350">The `ShortcutExpressCheckout` method collects the test purchase information and product details from the shopping cart and calls the `SetExpressCheckout` PayPal function.</span></span> <span data-ttu-id="f5a39-351">`GetCheckoutDetails` 方法會確認購買詳細資料，並在進行測試之前，先呼叫 `GetExpressCheckoutDetails` PayPal 函數。</span><span class="sxs-lookup"><span data-stu-id="f5a39-351">The `GetCheckoutDetails` method confirms purchase details and calls the `GetExpressCheckoutDetails` PayPal function before making the test purchase.</span></span> <span data-ttu-id="f5a39-352">`DoCheckoutPayment` 方法會藉由呼叫 `DoExpressCheckoutPayment` PayPal 函式，從測試環境完成測試購買。</span><span class="sxs-lookup"><span data-stu-id="f5a39-352">The `DoCheckoutPayment` method completes the test purchase from the testing environment by calling the `DoExpressCheckoutPayment` PayPal function.</span></span> <span data-ttu-id="f5a39-353">其餘的程式碼支援 PayPal 方法和程式，例如編碼字串、解碼字串、處理陣列，以及判斷認證。</span><span class="sxs-lookup"><span data-stu-id="f5a39-353">The remaining code supports the PayPal methods and process, such as encoding strings, decoding strings, processing arrays, and determining credentials.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5a39-354">PayPal 可讓您根據[paypal 的 API 規格](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)，包含選擇性的購買詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-354">PayPal allows you to include optional purchase details based on [PayPal's API specification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout).</span></span> <span data-ttu-id="f5a39-355">藉由在 Wingtip 玩具範例應用程式中擴充程式碼，您可以包含當地語系化詳細資料、產品描述、稅金、客戶服務編號，以及其他許多選用欄位。</span><span class="sxs-lookup"><span data-stu-id="f5a39-355">By extending the code in the Wingtip Toys sample application, you can include localization details, product descriptions, tax, a customer service number, as well as many other optional fields.</span></span>

<span data-ttu-id="f5a39-356">請注意，在**ShortcutExpressCheckout**方法中指定的傳回和取消 url 會使用通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="f5a39-356">Notice that the return and cancel URLs that are specified in the **ShortcutExpressCheckout** method use a port number.</span></span>

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

<span data-ttu-id="f5a39-357">當 Visual Web Developer 使用 SSL 執行 Web 專案時，通常會將埠44300用於 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f5a39-357">When Visual Web Developer runs a web project using SSL, commonly the port 44300 is used for the web server.</span></span> <span data-ttu-id="f5a39-358">如上所示，埠號碼是44300。</span><span class="sxs-lookup"><span data-stu-id="f5a39-358">As shown above, the port number is 44300.</span></span> <span data-ttu-id="f5a39-359">當您執行應用程式時，可能會看到不同的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-359">When you run the application, you could see a different port number.</span></span> <span data-ttu-id="f5a39-360">您必須在程式碼中正確設定您的埠號碼，才能在本教學課程結尾處成功執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-360">Your port number needs to be correctly set in the code so that you can successful run the Wingtip Toys sample application at the end of this tutorial.</span></span> <span data-ttu-id="f5a39-361">本教學課程的下一節將說明如何取出本機主機埠號碼，並更新 PayPal 類別。</span><span class="sxs-lookup"><span data-stu-id="f5a39-361">The next section of this tutorial explains how to retrieve the local host port number and update the PayPal class.</span></span>

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a><span data-ttu-id="f5a39-362">更新 PayPal 類別中的 LocalHost 埠號碼</span><span class="sxs-lookup"><span data-stu-id="f5a39-362">Update the LocalHost Port Number in the PayPal Class</span></span>

<span data-ttu-id="f5a39-363">Wingtip 玩具範例應用程式會藉由流覽至 PayPal 測試網站，並返回您的 Wingtip 玩具範例應用程式的本機實例來購買產品。</span><span class="sxs-lookup"><span data-stu-id="f5a39-363">The Wingtip Toys sample application purchases products by navigating to the PayPal testing site and returning to your local instance of the Wingtip Toys sample application.</span></span> <span data-ttu-id="f5a39-364">為了讓 PayPal 回到正確的 URL，您必須在上述 PayPal 代碼中指定本機執行中範例應用程式的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-364">In order to have PayPal return to the correct URL, you need to specify the port number of the locally running sample application in the PayPal code mentioned above.</span></span>

1. <span data-ttu-id="f5a39-365">以滑鼠右鍵按一下**方案總管**中的專案名稱（**WingtipToys**），然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-365">Right-click the project name (**WingtipToys**) in **Solution Explorer** and select **Properties**.</span></span>
2. <span data-ttu-id="f5a39-366">在左欄中，選取 [ **Web** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f5a39-366">In the left column, select the **Web** tab.</span></span>
3. <span data-ttu-id="f5a39-367">從 [**專案 Url** ] 方塊中取出埠號碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-367">Retrieve the port number from the **Project Url** box.</span></span>
4. <span data-ttu-id="f5a39-368">如有需要，請更新*PayPalFunctions.cs*檔案中 PayPal 類別（`NVPAPICaller`）的 `returnURL` 和 `cancelURL`，以使用 web 應用程式的埠號碼：</span><span class="sxs-lookup"><span data-stu-id="f5a39-368">If needed, update the `returnURL` and `cancelURL` in the PayPal class (`NVPAPICaller`) in the *PayPalFunctions.cs* file to use the port number of your web application:</span></span>   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

<span data-ttu-id="f5a39-369">現在，您所新增的程式碼會符合本機 Web 應用程式的預期通訊埠。</span><span class="sxs-lookup"><span data-stu-id="f5a39-369">Now the code that you added will match the expected port for your local Web application.</span></span> <span data-ttu-id="f5a39-370">PayPal 將能夠回到您本機電腦上正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="f5a39-370">PayPal will be able to return to the correct URL on your local machine.</span></span>

### <a name="add-the-paypal-checkout-button"></a><span data-ttu-id="f5a39-371">新增 [PayPal 結帳] 按鈕</span><span class="sxs-lookup"><span data-stu-id="f5a39-371">Add the PayPal Checkout Button</span></span>

<span data-ttu-id="f5a39-372">現在，主要 PayPal 函式已新增至範例應用程式，您可以開始加入呼叫這些函式所需的標記和程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-372">Now that the primary PayPal functions have been added to the sample application, you can begin adding the markup and code needed to call these functions.</span></span> <span data-ttu-id="f5a39-373">首先，您必須新增使用者會在 [購物車] 頁面上看到的 [結帳] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5a39-373">First, you must add the checkout button that the user will see on the shopping cart page.</span></span>

1. <span data-ttu-id="f5a39-374">開啟*ShoppingCart .aspx*檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-374">Open the *ShoppingCart.aspx* file.</span></span>
2. <span data-ttu-id="f5a39-375">流覽至檔案底部，並尋找 `<!--Checkout Placeholder -->` 批註。</span><span class="sxs-lookup"><span data-stu-id="f5a39-375">Scroll to the bottom of the file and find the `<!--Checkout Placeholder -->` comment.</span></span>
3. <span data-ttu-id="f5a39-376">將批註取代為 `ImageButton` 控制項，讓 mark 的標記取代如下：</span><span class="sxs-lookup"><span data-stu-id="f5a39-376">Replace the comment with an `ImageButton` control so that the mark up is replaced as follows:</span></span>  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. <span data-ttu-id="f5a39-377">在*ShoppingCart.aspx.cs*檔案中，在接近檔案結尾的 `UpdateBtn_Click` 事件處理常式之後，新增 `CheckOutBtn_Click` 事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="f5a39-377">In the *ShoppingCart.aspx.cs* file, after the `UpdateBtn_Click` event handler near the end of the file, add the `CheckOutBtn_Click` event handler:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. <span data-ttu-id="f5a39-378">此外，在*ShoppingCart.aspx.cs*檔案中，新增 `CheckoutBtn`的參考，以便參考新的影像按鈕，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5a39-378">Also in the *ShoppingCart.aspx.cs* file, add a reference to the `CheckoutBtn`, so that the new image button is referenced as follows:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. <span data-ttu-id="f5a39-379">將您的變更儲存至*ShoppingCart .aspx*檔案和*ShoppingCart.aspx.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-379">Save your changes to both the *ShoppingCart.aspx* file and the *ShoppingCart.aspx.cs* file.</span></span>
7. <span data-ttu-id="f5a39-380">從功能表中，選取  **Debug**- &gt;**組建 WingtipToys**。</span><span class="sxs-lookup"><span data-stu-id="f5a39-380">From the menu, select **Debug**-&gt;**Build WingtipToys**.</span></span>  
   <span data-ttu-id="f5a39-381">專案會以新加入的**ImageButton**控制項重建。</span><span class="sxs-lookup"><span data-stu-id="f5a39-381">The project will be rebuilt with the newly added **ImageButton** control.</span></span>

### <a name="send-purchase-details-to-paypal"></a><span data-ttu-id="f5a39-382">將購買詳細資料傳送至 PayPal</span><span class="sxs-lookup"><span data-stu-id="f5a39-382">Send Purchase Details to PayPal</span></span>

<span data-ttu-id="f5a39-383">當使用者按一下 [購物車] 頁面（*ShoppingCart .aspx*）上的 [**結帳**] 按鈕時，他們會開始購買程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-383">When the user clicks the **Checkout** button on the shopping cart page (*ShoppingCart.aspx*), they'll begin the purchase process.</span></span> <span data-ttu-id="f5a39-384">下列程式碼會呼叫購買產品所需的第一個 PayPal 函數。</span><span class="sxs-lookup"><span data-stu-id="f5a39-384">The following code calls the first PayPal function needed to purchase products.</span></span>

1. <span data-ttu-id="f5a39-385">從 [*簽出*] 資料夾中，開啟名為*CheckoutStart.aspx.cs*的程式碼後置檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-385">From the *Checkout* folder, open the code-behind file named *CheckoutStart.aspx.cs*.</span></span>   
   <span data-ttu-id="f5a39-386">請務必開啟程式碼後置檔案。</span><span class="sxs-lookup"><span data-stu-id="f5a39-386">Be sure to open the code-behind file.</span></span>
2. <span data-ttu-id="f5a39-387">將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f5a39-387">Replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

<span data-ttu-id="f5a39-388">當應用程式的使用者按一下 [購物車] 頁面上的 [**結帳**] 按鈕時，瀏覽器將會流覽至 [ *CheckoutStart* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-388">When the user of the application clicks the **Checkout** button on the shopping cart page, the browser will navigate to the *CheckoutStart.aspx* page.</span></span> <span data-ttu-id="f5a39-389">當*CheckoutStart .aspx*頁面載入時，會呼叫 `ShortcutExpressCheckout` 方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-389">When the *CheckoutStart.aspx* page loads, the `ShortcutExpressCheckout` method is called.</span></span> <span data-ttu-id="f5a39-390">此時，使用者會轉移至 PayPal 測試網站。</span><span class="sxs-lookup"><span data-stu-id="f5a39-390">At this point, the user is transferred to the PayPal testing web site.</span></span> <span data-ttu-id="f5a39-391">在 PayPal 網站上，使用者輸入其 PayPal 認證、審查購買詳細資料、接受 PayPal 合約，然後回到 `ShortcutExpressCheckout` 方法完成的 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-391">On the PayPal site, the user enters their PayPal credentials, reviews the purchase details, accepts the PayPal agreement and returns to the Wingtip Toys sample application where the `ShortcutExpressCheckout` method completes.</span></span> <span data-ttu-id="f5a39-392">當 `ShortcutExpressCheckout` 方法完成時，它會將使用者重新導向至 `ShortcutExpressCheckout` 方法中指定的*CheckoutReview .aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-392">When the `ShortcutExpressCheckout` method is complete, it will redirect the user to the *CheckoutReview.aspx* page specified in the `ShortcutExpressCheckout` method.</span></span> <span data-ttu-id="f5a39-393">這可讓使用者從 Wingtip 玩具範例應用程式中，檢查訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-393">This allows the user to review the order details from within the Wingtip Toys sample application.</span></span>

### <a name="review-order-details"></a><span data-ttu-id="f5a39-394">審核順序詳細資料</span><span class="sxs-lookup"><span data-stu-id="f5a39-394">Review Order Details</span></span>

<span data-ttu-id="f5a39-395">從 PayPal 傳回之後，Wingtip 玩具範例應用程式的 [ *CheckoutReview* ] 頁面會顯示訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-395">After returning from PayPal, the *CheckoutReview.aspx* page of the Wingtip Toys sample application displays the order details.</span></span> <span data-ttu-id="f5a39-396">此頁面可讓使用者在購買產品前，先檢查訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-396">This page allows the user to review the order details before purchasing the products.</span></span> <span data-ttu-id="f5a39-397">*CheckoutReview*的建立方式必須如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5a39-397">The *CheckoutReview.aspx* page must be created as follows:</span></span>

1. <span data-ttu-id="f5a39-398">在 [*簽出*] 資料夾中，開啟名為*CheckoutReview*的頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-398">In the *Checkout* folder, open the page named *CheckoutReview.aspx*.</span></span>
2. <span data-ttu-id="f5a39-399">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="f5a39-399">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. <span data-ttu-id="f5a39-400">開啟名為*CheckoutReview.aspx.cs*的程式碼後置頁面，並將現有的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="f5a39-400">Open the code-behind page named *CheckoutReview.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

<span data-ttu-id="f5a39-401">**DetailsView**控制項是用來顯示已從 PayPal 傳回的訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-401">The **DetailsView** control is used to display the order details that have been returned from PayPal.</span></span> <span data-ttu-id="f5a39-402">此外，上述程式碼也會將訂單詳細資料儲存至 Wingtip 玩具資料庫，做為 `OrderDetail` 物件。</span><span class="sxs-lookup"><span data-stu-id="f5a39-402">Also, the above code saves the order details to the Wingtip Toys database as an `OrderDetail` object.</span></span> <span data-ttu-id="f5a39-403">當使用者按一下 [**完成訂單**] 按鈕時，系統會將他們重新導向至*CheckoutComplete .aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-403">When the user clicks on the **Complete Order** button, they are redirected to the *CheckoutComplete.aspx* page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5a39-404">**秘訣**</span><span class="sxs-lookup"><span data-stu-id="f5a39-404">**Tip**</span></span>
> 
> <span data-ttu-id="f5a39-405">請注意，在*CheckoutReview*的標記中，會使用 `<ItemStyle>` 標記來變更**DetailsView**控制項（接近頁面底部）中的專案樣式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-405">In the markup of the *CheckoutReview.aspx* page, notice that the `<ItemStyle>` tag is used to change the style of the items within the **DetailsView** control near the bottom of the page.</span></span> <span data-ttu-id="f5a39-406">藉由在 [**設計檢視**] 中查看頁面（在 Visual Studio 的左下角選取 [**設計**]），然後選取 [ **DetailsView** ] 控制項，然後選取 [**智慧標籤**] （控制項右上方的箭號圖示），您就能夠看到**DetailsView**工作。</span><span class="sxs-lookup"><span data-stu-id="f5a39-406">By viewing the page in **Design View** (by selecting **Design** at the lower left corner of Visual Studio), then selecting the **DetailsView** control, and selecting the **Smart Tag** (the arrow icon at the top right of the control), you will be able to see the **DetailsView Tasks**.</span></span>
> 
> ![使用 PayPal 簽出和付款-編輯欄位](checkout-and-payment-with-paypal/_static/image18.png)
> 
> <span data-ttu-id="f5a39-408">藉由選取 [**編輯欄位**]，將會顯示 [**欄位**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5a39-408">By selecting **Edit Fields**, the **Fields** dialog box will appear.</span></span> <span data-ttu-id="f5a39-409">在此對話方塊中，您可以輕鬆地控制**DetailsView**控制項的視覺屬性，例如**ItemStyle**。</span><span class="sxs-lookup"><span data-stu-id="f5a39-409">In this dialog box you can easily control the visual properties, such as **ItemStyle**, of the **DetailsView** control.</span></span>
> 
> ![使用 PayPal-[欄位] 對話方塊簽出和付款](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a><span data-ttu-id="f5a39-411">完成購買</span><span class="sxs-lookup"><span data-stu-id="f5a39-411">Complete Purchase</span></span>

<span data-ttu-id="f5a39-412">*CheckoutComplete .aspx*頁面會向 PayPal 購買。</span><span class="sxs-lookup"><span data-stu-id="f5a39-412">*CheckoutComplete.aspx* page makes the purchase from PayPal.</span></span> <span data-ttu-id="f5a39-413">如上所述，使用者必須按一下 [**完整訂單**] 按鈕，應用程式才會流覽至*CheckoutComplete .aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-413">As mentioned above, the user must click on the **Complete Order** button before the application will navigate to the *CheckoutComplete.aspx* page.</span></span>

1. <span data-ttu-id="f5a39-414">在 [*簽出*] 資料夾中，開啟名為*CheckoutComplete*的頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-414">In the *Checkout* folder, open the page named *CheckoutComplete.aspx*.</span></span>
2. <span data-ttu-id="f5a39-415">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="f5a39-415">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. <span data-ttu-id="f5a39-416">開啟名為*CheckoutComplete.aspx.cs*的程式碼後置頁面，並將現有的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="f5a39-416">Open the code-behind page named *CheckoutComplete.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

<span data-ttu-id="f5a39-417">載入*CheckoutComplete .aspx*頁面時，會呼叫 `DoCheckoutPayment` 方法。</span><span class="sxs-lookup"><span data-stu-id="f5a39-417">When the *CheckoutComplete.aspx* page is loaded, the `DoCheckoutPayment` method is called.</span></span> <span data-ttu-id="f5a39-418">如先前所述，`DoCheckoutPayment` 方法會從 PayPal 測試環境完成購買。</span><span class="sxs-lookup"><span data-stu-id="f5a39-418">As mentioned earlier, the `DoCheckoutPayment` method completes the purchase from the PayPal testing environment.</span></span> <span data-ttu-id="f5a39-419">一旦 PayPal 完成訂單的購買後，[ *CheckoutComplete* ] 頁面就會顯示購買者 `ID` 的付款交易。</span><span class="sxs-lookup"><span data-stu-id="f5a39-419">Once PayPal has completed the purchase of the order, the *CheckoutComplete.aspx* page displays a payment transaction `ID` to the purchaser.</span></span>

### <a name="handle-cancel-purchase"></a><span data-ttu-id="f5a39-420">處理取消購買</span><span class="sxs-lookup"><span data-stu-id="f5a39-420">Handle Cancel Purchase</span></span>

<span data-ttu-id="f5a39-421">如果使用者決定取消購買，他們會被導向至 [ *CheckoutCancel* ] 頁面，他們會看到他們的訂單已取消。</span><span class="sxs-lookup"><span data-stu-id="f5a39-421">If the user decides to cancel the purchase, they will be directed to the *CheckoutCancel.aspx* page where they will see that their order has been cancelled.</span></span>

1. <span data-ttu-id="f5a39-422">在 [*簽出*] 資料夾中，開啟名為*CheckoutCancel*的頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-422">Open the page named *CheckoutCancel.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="f5a39-423">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="f5a39-423">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a><span data-ttu-id="f5a39-424">處理購買錯誤</span><span class="sxs-lookup"><span data-stu-id="f5a39-424">Handle Purchase Errors</span></span>

<span data-ttu-id="f5a39-425">在購買程式期間的錯誤將由*CheckoutError*處理。</span><span class="sxs-lookup"><span data-stu-id="f5a39-425">Errors during the purchase process will be handled by the *CheckoutError.aspx* page.</span></span> <span data-ttu-id="f5a39-426">*CheckoutStart*的程式碼後置、 *CheckoutReview*頁面和*CheckoutComplete*頁面會在發生錯誤時，每個都會重新導向至*CheckoutError .aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-426">The code-behind of the *CheckoutStart.aspx* page, the *CheckoutReview.aspx* page, and the *CheckoutComplete.aspx* page will each redirect to the *CheckoutError.aspx* page if an error occurs.</span></span>

1. <span data-ttu-id="f5a39-427">在 [*簽出*] 資料夾中，開啟名為*CheckoutError*的頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-427">Open the page named *CheckoutError.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="f5a39-428">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="f5a39-428">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

<span data-ttu-id="f5a39-429">當簽出程式期間發生錯誤時，會顯示 [ *CheckoutError* ] 頁面，其中包含錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5a39-429">The *CheckoutError.aspx* page is displayed with the error details when an error occurs during the checkout process.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="f5a39-430">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f5a39-430">Running the Application</span></span>

<span data-ttu-id="f5a39-431">執行應用程式，以瞭解如何購買產品。</span><span class="sxs-lookup"><span data-stu-id="f5a39-431">Run the application to see how to purchase products.</span></span> <span data-ttu-id="f5a39-432">請注意，您將會在 PayPal 測試環境中執行。</span><span class="sxs-lookup"><span data-stu-id="f5a39-432">Note that you will be running in the PayPal testing environment.</span></span> <span data-ttu-id="f5a39-433">不會交換實際的金錢。</span><span class="sxs-lookup"><span data-stu-id="f5a39-433">No actual money is being exchanged.</span></span>

1. <span data-ttu-id="f5a39-434">請確定所有檔案都儲存在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="f5a39-434">Make sure all your files are saved in Visual Studio.</span></span>
2. <span data-ttu-id="f5a39-435">開啟網頁瀏覽器，並流覽至[https://developer.paypal.com](https://developer.paypal.com/)。</span><span class="sxs-lookup"><span data-stu-id="f5a39-435">Open a Web browser and navigate to [https://developer.paypal.com](https://developer.paypal.com/).</span></span>
3. <span data-ttu-id="f5a39-436">使用您稍早在本教學課程中建立的 PayPal 開發人員帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="f5a39-436">Login with your PayPal developer account that you created earlier in this tutorial.</span></span>  
   <span data-ttu-id="f5a39-437">對於 PayPal 的開發人員沙箱，您必須在[https://developer.paypal.com](https://developer.paypal.com/)登入，以測試快速簽出。</span><span class="sxs-lookup"><span data-stu-id="f5a39-437">For PayPal's developer sandbox, you need to be logged in at [https://developer.paypal.com](https://developer.paypal.com/) to test express checkout.</span></span> <span data-ttu-id="f5a39-438">這僅適用于 PayPal 的沙箱測試，而不適用於 PayPal 的即時環境。</span><span class="sxs-lookup"><span data-stu-id="f5a39-438">This only applies to PayPal's sandbox testing, not to PayPal's live environment.</span></span>
4. <span data-ttu-id="f5a39-439">在 Visual Studio 中，按**F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5a39-439">In Visual Studio, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="f5a39-440">重建資料庫之後，瀏覽器將會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-440">After the database rebuilds, the browser will open and show the *Default.aspx* page.</span></span>
5. <span data-ttu-id="f5a39-441">藉由選取產品類別（例如「汽車」），然後按一下每個產品旁的 [**新增至購物車**]，將三個不同的產品新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="f5a39-441">Add three different products to the shopping cart by selecting the product category, such as "Cars" and then clicking **Add to Cart** next to each product.</span></span>  
   <span data-ttu-id="f5a39-442">購物車會顯示您所選取的產品。</span><span class="sxs-lookup"><span data-stu-id="f5a39-442">The shopping cart will display the product you have selected.</span></span>
6. <span data-ttu-id="f5a39-443">按一下 [ **PayPal** ] 按鈕以簽出。</span><span class="sxs-lookup"><span data-stu-id="f5a39-443">Click the **PayPal** button to checkout.</span></span> 

    ![使用 PayPal 的結帳和付款-購物車](checkout-and-payment-with-paypal/_static/image20.png)

   <span data-ttu-id="f5a39-445">簽出將會要求您必須擁有 Wingtip 玩具範例應用程式的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-445">Checking out will require that you have a user account for the Wingtip Toys sample application.</span></span>
7. <span data-ttu-id="f5a39-446">按一下頁面右側的 [ **Google** ] 連結，以使用現有的 gmail.com 電子郵件帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="f5a39-446">Click the **Google** link on the right of the page to log in with an existing gmail.com email account.</span></span>  
   <span data-ttu-id="f5a39-447">如果您沒有 gmail.com 帳戶，可以在[www.gmail.com](https://www.gmail.com/)建立一個用於測試的用途。</span><span class="sxs-lookup"><span data-stu-id="f5a39-447">If you do not have a gmail.com account, you can create one for testing purposes at [www.gmail.com](https://www.gmail.com/).</span></span> <span data-ttu-id="f5a39-448">您也可以按一下 [註冊]，以使用標準的本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-448">You can also use a standard local account by clicking "Register".</span></span> 

    ![簽出與使用 PayPal 付款-登入](checkout-and-payment-with-paypal/_static/image21.png)
8. <span data-ttu-id="f5a39-450">使用您的 gmail 帳戶和密碼登入。</span><span class="sxs-lookup"><span data-stu-id="f5a39-450">Sign in with your gmail account and password.</span></span> 

    ![使用 PayPal 進行簽出和付款-Gmail 登入](checkout-and-payment-with-paypal/_static/image22.png)
9. <span data-ttu-id="f5a39-452">按一下 [**登入**] 按鈕，向您的 Wingtip 玩具範例應用程式使用者名稱註冊您的 gmail 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5a39-452">Click the **Log in** button to register your gmail account with your Wingtip Toys sample application user name.</span></span> 

    ![使用 PayPal 簽出和付款-註冊帳戶](checkout-and-payment-with-paypal/_static/image23.png)
10. <span data-ttu-id="f5a39-454">在 PayPal 測試網站上，新增您稍早在本教學課程中建立的**買方**電子郵件地址和密碼，然後按一下 [**登入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5a39-454">On the PayPal test site, add your **buyer** email address and password that you created earlier in this tutorial, then click the **Log In** button.</span></span> 

    ![使用 PayPal 簽出和付款-PayPal 登入](checkout-and-payment-with-paypal/_static/image24.png)
11. <span data-ttu-id="f5a39-456">同意 PayPal 原則，然後按一下 [**同意並繼續**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5a39-456">Agree to the PayPal policy and click the **Agree and Continue** button.</span></span>  
    <span data-ttu-id="f5a39-457">請注意，只有當您第一次使用此 PayPal 帳戶時，才會顯示此頁面。</span><span class="sxs-lookup"><span data-stu-id="f5a39-457">Note that this page is only displayed the first time you use this PayPal account.</span></span> <span data-ttu-id="f5a39-458">同樣地，請注意這是測試帳戶，並不會交換真正的金錢。</span><span class="sxs-lookup"><span data-stu-id="f5a39-458">Again note that this is a test account, no real money is exchanged.</span></span> 

    ![使用 PayPal 簽出和付款-PayPal 原則](checkout-and-payment-with-paypal/_static/image25.png)
12. <span data-ttu-id="f5a39-460">請參閱 PayPal 測試環境審查頁面上的訂單資訊，然後按一下 [**繼續**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-460">Review the order information on the PayPal testing environment review page and click **Continue**.</span></span> 

    ![簽出與使用 PayPal 的款項-審查資訊](checkout-and-payment-with-paypal/_static/image26.png)
13. <span data-ttu-id="f5a39-462">在 [ *CheckoutReview* ] 頁面上，確認訂單金額，並查看產生的寄送位址。</span><span class="sxs-lookup"><span data-stu-id="f5a39-462">On the *CheckoutReview.aspx* page, verify the order amount and view the generated shipping address.</span></span> <span data-ttu-id="f5a39-463">然後，按一下 [**完成訂單**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5a39-463">Then, click the **Complete Order** button.</span></span> 

    ![使用 PayPal-訂單審查簽出和付款](checkout-and-payment-with-paypal/_static/image27.png)
14. <span data-ttu-id="f5a39-465">隨即會顯示 [ **CheckoutComplete** ] 頁面，其中包含付款交易識別碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-465">The **CheckoutComplete.aspx** page is displayed with a payment transaction ID.</span></span> 

    ![使用 PayPal 簽出和付款-結帳完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a><span data-ttu-id="f5a39-467">檢查資料庫</span><span class="sxs-lookup"><span data-stu-id="f5a39-467">Reviewing the Database</span></span>

<span data-ttu-id="f5a39-468">在執行應用程式後，藉由在 Wingtip 玩具範例應用程式資料庫中查看更新的資料，您可以看到應用程式已成功記錄產品的購買。</span><span class="sxs-lookup"><span data-stu-id="f5a39-468">By reviewing the updated data in the Wingtip Toys sample application database after running the application, you can see that the application successfully recorded the purchase of the products.</span></span>

<span data-ttu-id="f5a39-469">您可以使用 [**資料庫總管**] 視窗（Visual Studio 中的 [**伺服器總管**] 視窗），檢查*Wingtiptoys*中包含的資料，就像您先前在本教學課程系列中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="f5a39-469">You can inspect the data contained in the *Wingtiptoys.mdf* database file by using the **Database Explorer** window (**Server Explorer** window in Visual Studio) as you did earlier in this tutorial series.</span></span>

1. <span data-ttu-id="f5a39-470">如果瀏覽器視窗仍為開啟狀態，請將它關閉。</span><span class="sxs-lookup"><span data-stu-id="f5a39-470">Close the browser window if it is still open.</span></span>
2. <span data-ttu-id="f5a39-471">在 Visual Studio 中，選取**方案總管**頂端的 [**顯示所有**檔案] 圖示，以讓您展開**應用程式\_** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f5a39-471">In Visual Studio, select the **Show All Files** icon at the top of **Solution Explorer** to allow you to expand the **App\_Data** folder.</span></span>
3. <span data-ttu-id="f5a39-472">展開**應用程式\_[Data** ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f5a39-472">Expand the **App\_Data** folder.</span></span>  
 <span data-ttu-id="f5a39-473">您可能需要選取資料夾的 [**顯示所有**檔案] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f5a39-473">You may need to select the **Show All Files** icon for the folder.</span></span>
4. <span data-ttu-id="f5a39-474">以滑鼠右鍵按一下*Wingtiptoys .mdf*資料庫檔案，然後選取 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-474">Right-click the *Wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="f5a39-475">隨即顯示 [**伺服器總管**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-475">**Server Explorer** is displayed.</span></span>
5. <span data-ttu-id="f5a39-476">展開 **[資料表]** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f5a39-476">Expand the **Tables** folder.</span></span>
6. <span data-ttu-id="f5a39-477">以滑鼠右鍵按一下**Orders**資料表，然後選取 [**顯示資料表資料**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-477">Right-click the **Orders**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="f5a39-478">[**訂單**] 資料表隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f5a39-478">The **Orders** table is displayed.</span></span>
7. <span data-ttu-id="f5a39-479">檢查**PaymentTransactionID**資料行以確認交易成功。</span><span class="sxs-lookup"><span data-stu-id="f5a39-479">Review the **PaymentTransactionID** column to confirm successful transactions.</span></span> 

    ![簽出和付款使用 PayPal-審核資料庫](checkout-and-payment-with-paypal/_static/image29.png)
8. <span data-ttu-id="f5a39-481">關閉 [ **Orders** ] 資料表視窗。</span><span class="sxs-lookup"><span data-stu-id="f5a39-481">Close the **Orders** table window.</span></span>
9. <span data-ttu-id="f5a39-482">在 伺服器總管中，以滑鼠右鍵按一下**OrderDetails**資料表，然後選取 **顯示資料表資料**。</span><span class="sxs-lookup"><span data-stu-id="f5a39-482">In the Server Explorer, right-click the **OrderDetails** table and select **Show Table Data**.</span></span>
10. <span data-ttu-id="f5a39-483">檢查**OrderDetails**資料表中的 `OrderId` 和 `Username` 值。</span><span class="sxs-lookup"><span data-stu-id="f5a39-483">Review the `OrderId` and `Username` values in the **OrderDetails** table.</span></span> <span data-ttu-id="f5a39-484">請注意，這些值符合**Orders**資料表中包含的 `OrderId` 和 `Username` 值。</span><span class="sxs-lookup"><span data-stu-id="f5a39-484">Note that these values match the `OrderId` and `Username` values included in the **Orders** table.</span></span>
11. <span data-ttu-id="f5a39-485">關閉 [ **OrderDetails**資料表] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f5a39-485">Close the **OrderDetails** table window.</span></span>
12. <span data-ttu-id="f5a39-486">以滑鼠右鍵按一下 Wingtip 玩具資料庫檔案（*Wingtiptoys .mdf*），然後選取 [**關閉連接**]。</span><span class="sxs-lookup"><span data-stu-id="f5a39-486">Right-click the Wingtip Toys database file (*Wingtiptoys.mdf*) and select **Close Connection**.</span></span>
13. <span data-ttu-id="f5a39-487">如果您看不到 **方案總管** 視窗，請按一下 **伺服器總管** 視窗底部的 **方案總管**，再次顯示**方案總管**。</span><span class="sxs-lookup"><span data-stu-id="f5a39-487">If you do not see the **Solution Explorer** window, click **Solution Explorer** at the bottom of the **Server Explorer** window to show the **Solution Explorer** again.</span></span>

## <a name="summary"></a><span data-ttu-id="f5a39-488">總結</span><span class="sxs-lookup"><span data-stu-id="f5a39-488">Summary</span></span>

<span data-ttu-id="f5a39-489">在本教學課程中，您已新增訂單和訂單詳細資料架構來追蹤產品的購買。</span><span class="sxs-lookup"><span data-stu-id="f5a39-489">In this tutorial you added order and order detail schemas to track the purchase of products.</span></span> <span data-ttu-id="f5a39-490">您也可以將 PayPal 功能整合到 Wingtip 玩具範例應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f5a39-490">You also integrated PayPal functionality into the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5a39-491">其他資源</span><span class="sxs-lookup"><span data-stu-id="f5a39-491">Additional Resources</span></span>

<span data-ttu-id="f5a39-492">[ASP.NET 設定總覽](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="f5a39-492">[ASP.NET Configuration Overview](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="f5a39-493">將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f5a39-493">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="f5a39-494">Microsoft Azure 免費試用</span><span class="sxs-lookup"><span data-stu-id="f5a39-494">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a><span data-ttu-id="f5a39-495">免責聲明</span><span class="sxs-lookup"><span data-stu-id="f5a39-495">Disclaimer</span></span>

<span data-ttu-id="f5a39-496">本教學課程包含範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-496">This tutorial contains sample code.</span></span> <span data-ttu-id="f5a39-497">這類範例程式碼是以「原樣」提供，不含任何種類的擔保。</span><span class="sxs-lookup"><span data-stu-id="f5a39-497">Such sample code is provided "as is" without warranty of any kind.</span></span> <span data-ttu-id="f5a39-498">因此，Microsoft 不保證範例程式碼的精確度、完整性或品質。</span><span class="sxs-lookup"><span data-stu-id="f5a39-498">Accordingly, Microsoft does not guarantee the accuracy, integrity, or quality of the sample code.</span></span> <span data-ttu-id="f5a39-499">您同意以自己的風險使用範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5a39-499">You agree to use the sample code at your own risk.</span></span> <span data-ttu-id="f5a39-500">在任何情況下，Microsoft 不會針對任何範例程式碼、內容（包括但不限於任何範例程式碼、內容，或任何因使用任何範例程式碼而產生的任何類型遺失或損毀），以任何方式對您造成任何問題。</span><span class="sxs-lookup"><span data-stu-id="f5a39-500">Under no circumstances will Microsoft be liable to you in any way for any sample code, content, including but not limited to, any errors or omissions in any sample code, content, or any loss or damage of any kind incurred as a result of the use of any sample code.</span></span> <span data-ttu-id="f5a39-501">您將會收到通知，並據此同意補償、儲存及保存 Microsoft 免于任何遺失的損害、遺失的索賠、傷害或任何種類的損害，包括或因您張貼的資料而產生的 occasioned、傳輸、使用或依賴包含（但不限於）其中所表示的觀點。</span><span class="sxs-lookup"><span data-stu-id="f5a39-501">You are hereby notified and do hereby agree to indemnify, save and hold Microsoft harmless from and against any and all loss, claims of loss, injury or damage of any kind including, without limitation, those occasioned by or arising from material that you post, transmit, use or rely on including, but not limited to, the views expressed therein.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f5a39-502">[上一頁](shopping-cart.md)
> [下一頁](membership-and-administration.md)</span><span class="sxs-lookup"><span data-stu-id="f5a39-502">[Previous](shopping-cart.md)
[Next](membership-and-administration.md)</span></span>
