---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 第5部分：商務邏輯 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第5部分會加入一些商務邏輯。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630302"
---
# <a name="part-5-business-logic"></a><span data-ttu-id="96b28-104">第5部分：商務邏輯</span><span class="sxs-lookup"><span data-stu-id="96b28-104">Part 5: Business Logic</span></span>

<span data-ttu-id="96b28-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="96b28-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="96b28-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="96b28-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="96b28-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="96b28-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="96b28-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="96b28-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="96b28-109">第5部分會加入一些商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="96b28-109">Part 5 adds some business logic.</span></span>

## <a id="_Toc260221671"></a><span data-ttu-id="96b28-110">新增一些商務邏輯</span><span class="sxs-lookup"><span data-stu-id="96b28-110">Adding Some Business Logic</span></span>

<span data-ttu-id="96b28-111">我們希望每次有人造訪我們的網站時，都能使用我們的購物體驗。</span><span class="sxs-lookup"><span data-stu-id="96b28-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="96b28-112">即使他們未註冊或登入，訪客也能夠流覽並將專案新增至購物車。</span><span class="sxs-lookup"><span data-stu-id="96b28-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="96b28-113">當他們準備好簽出時，系統會提供驗證選項，如果他們還不是成員，他們就能夠建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="96b28-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="96b28-114">這表示我們必須執行邏輯，將購物車從匿名狀態轉換為「已註冊的使用者」狀態。</span><span class="sxs-lookup"><span data-stu-id="96b28-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="96b28-115">讓我們建立一個名為「類別」的目錄，然後以滑鼠右鍵按一下該資料夾，並建立名為 MyShoppingCart.cs 的新「類別」檔案。</span><span class="sxs-lookup"><span data-stu-id="96b28-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="96b28-116">如先前所述，我們將擴充可執行 MyShoppingCart 的類別，我們將使用來進行此動作。NET 強大的「部分類別」結構。</span><span class="sxs-lookup"><span data-stu-id="96b28-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="96b28-117">針對我們的 MyShoppingCart.aspx.cf 檔案產生的呼叫看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="96b28-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="96b28-118">請注意 "partial" 關鍵字的用法。</span><span class="sxs-lookup"><span data-stu-id="96b28-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="96b28-119">我們剛才產生的類別檔案看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="96b28-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="96b28-120">我們也會將部分關鍵字新增至這個檔案，以合併我們的程式。</span><span class="sxs-lookup"><span data-stu-id="96b28-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="96b28-121">我們的新類別檔案現在看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="96b28-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="96b28-122">我們將在類別中新增的第一個方法是「AddItem」方法。</span><span class="sxs-lookup"><span data-stu-id="96b28-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="96b28-123">這是當使用者按一下 [產品清單] 和 [產品詳細資料] 頁面上的 [新增至美工] 連結時，最後會呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="96b28-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="96b28-124">將下列附加至頁面頂端的 using 語句。</span><span class="sxs-lookup"><span data-stu-id="96b28-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="96b28-125">並將此方法新增至 MyShoppingCart 類別。</span><span class="sxs-lookup"><span data-stu-id="96b28-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="96b28-126">我們會使用 LINQ to Entities 來查看該專案是否已存在於購物車中。</span><span class="sxs-lookup"><span data-stu-id="96b28-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="96b28-127">若是如此，我們會更新專案的訂單數量，否則我們會為選取的專案建立新的專案</span><span class="sxs-lookup"><span data-stu-id="96b28-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="96b28-128">為了呼叫這個方法，我們將會執行一個 AddToCart 的 .aspx 頁面，這個網頁不僅會將此方法類別，還會在新增專案之後顯示目前的購物 a = 購物車。</span><span class="sxs-lookup"><span data-stu-id="96b28-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="96b28-129">以滑鼠右鍵按一下 [方案瀏覽器] 中的方案名稱，然後新增名為 AddToCart 的新頁面，如同我們先前所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="96b28-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="96b28-130">雖然我們可以使用此頁面來顯示暫時結果（例如，低股票問題），但在我們的實中，頁面實際上不會轉譯，而是呼叫「新增」邏輯和重新導向。</span><span class="sxs-lookup"><span data-stu-id="96b28-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="96b28-131">為了達成此目的，我們會將下列程式碼新增至頁面\_載入事件。</span><span class="sxs-lookup"><span data-stu-id="96b28-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="96b28-132">請注意，我們正在從 QueryString 參數中抓取要加入購物車的產品，並呼叫我們類別的 AddItem 方法。</span><span class="sxs-lookup"><span data-stu-id="96b28-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="96b28-133">假設未發生任何錯誤，控制權會傳遞至 SHoppingCart，我們將會在下一步中完整地執行此頁面。</span><span class="sxs-lookup"><span data-stu-id="96b28-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="96b28-134">如果應該發生錯誤，我們會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="96b28-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="96b28-135">目前我們尚未執行全域錯誤處理常式，因此我們的應用程式無法處理此例外狀況，但我們很快就會解決此問題。</span><span class="sxs-lookup"><span data-stu-id="96b28-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="96b28-136">另請注意語句 Debug. Fail （）的用法（可透過 `using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="96b28-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="96b28-137">應用程式是否在偵錯工具內執行，這個方法會顯示詳細的對話方塊，其中包含應用程式狀態的相關資訊，以及我們指定的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="96b28-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="96b28-138">在生產環境中執行時，會忽略 Debug. Fail （）語句。</span><span class="sxs-lookup"><span data-stu-id="96b28-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="96b28-139">在上述程式碼中，您會注意到我們的購物車類別名稱 "GetShoppingCartId" 中的方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="96b28-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="96b28-140">新增程式碼來執行方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="96b28-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="96b28-141">請注意，我們也新增了 [更新] 和 [簽出] 按鈕，以及可顯示購物車「總計」的標籤。</span><span class="sxs-lookup"><span data-stu-id="96b28-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="96b28-142">我們現在可以將專案新增至購物車，但我們尚未實行在新增產品後顯示購物車的邏輯。</span><span class="sxs-lookup"><span data-stu-id="96b28-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="96b28-143">因此，在 MyShoppingCart .aspx 頁面中，我們將新增 EntityDataSource 控制項和 GridVire 控制項，如下所示。</span><span class="sxs-lookup"><span data-stu-id="96b28-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="96b28-144">在設計工具中呼叫表單，讓您可以按兩下 [更新購物車] 按鈕，並產生在標記的宣告中指定的 click 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="96b28-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="96b28-145">我們稍後會執行詳細資料，但這麼做可讓我們建立和執行我們的應用程式，而不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="96b28-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="96b28-146">當您執行應用程式並將專案新增至購物車時，您會看到這個。</span><span class="sxs-lookup"><span data-stu-id="96b28-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="96b28-147">請注意，我們已藉由執行三個自訂資料行，從 [預設] 方格顯示中偏離。</span><span class="sxs-lookup"><span data-stu-id="96b28-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="96b28-148">第一個是適用于數量的可編輯「系結」欄位：</span><span class="sxs-lookup"><span data-stu-id="96b28-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="96b28-149">下一個是 [計算] 資料行，可顯示明細專案總計（專案成本乘以要排序的數量）：</span><span class="sxs-lookup"><span data-stu-id="96b28-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="96b28-150">最後，我們有一個包含 CheckBox 控制項的自訂資料行，使用者會用它來指出應該從購物圖表中移除該專案。</span><span class="sxs-lookup"><span data-stu-id="96b28-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="96b28-151">如您所見，訂單合計列是空的，因此讓我們新增一些邏輯來計算訂單總計。</span><span class="sxs-lookup"><span data-stu-id="96b28-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="96b28-152">我們會先對我們的 MyShoppingCart 類別執行 "GetTotal" 方法。</span><span class="sxs-lookup"><span data-stu-id="96b28-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="96b28-153">在 MyShoppingCart.cs 檔案中，新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="96b28-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="96b28-154">然後在頁面\_載入事件處理常式 中，我們可以呼叫 GetTotal 方法。</span><span class="sxs-lookup"><span data-stu-id="96b28-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="96b28-155">同時我們也會新增測試，以查看購物車是否為空白，並據此調整顯示。</span><span class="sxs-lookup"><span data-stu-id="96b28-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="96b28-156">現在，如果購物車是空的，我們會取得：</span><span class="sxs-lookup"><span data-stu-id="96b28-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="96b28-157">如果不是，我們會看到總計。</span><span class="sxs-lookup"><span data-stu-id="96b28-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="96b28-158">不過，此頁面尚未完成。</span><span class="sxs-lookup"><span data-stu-id="96b28-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="96b28-159">我們需要額外的邏輯來重新計算購物車，方法是移除標示為移除的專案，以及判斷新的數量詞，因為使用者可能已在方格中變更某些數值。</span><span class="sxs-lookup"><span data-stu-id="96b28-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="96b28-160">讓我們將 "RemoveItem" 方法新增至 MyShoppingCart.cs 中的購物車類別，以處理使用者標示要移除之專案的情況。</span><span class="sxs-lookup"><span data-stu-id="96b28-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="96b28-161">現在讓我們在使用者直接變更要在 GridView 中排序的品質時，使用一種方法來處理這種情況。</span><span class="sxs-lookup"><span data-stu-id="96b28-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="96b28-162">有了基本的 [移除] 和 [更新] 功能之後，我們就可以在資料庫中執行實際更新購物車的邏輯。</span><span class="sxs-lookup"><span data-stu-id="96b28-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="96b28-163">（在 MyShoppingCart.cs 中）</span><span class="sxs-lookup"><span data-stu-id="96b28-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="96b28-164">您會注意到這個方法需要兩個參數。</span><span class="sxs-lookup"><span data-stu-id="96b28-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="96b28-165">其中一個是購物車識別碼，另一個則是使用者定義類型的物件陣列。</span><span class="sxs-lookup"><span data-stu-id="96b28-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="96b28-166">為了儘量減少我們的邏輯對使用者介面細節的相依性，我們定義了一個資料結構，我們可以用來將購物車專案傳遞給程式碼，而不需要直接存取 GridView 控制項的方法。</span><span class="sxs-lookup"><span data-stu-id="96b28-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="96b28-167">在我們的 MyShoppingCart.aspx.cs 檔案中，我們可以在 [更新] 按鈕的 Click 事件處理常式中使用此結構，如下所示。</span><span class="sxs-lookup"><span data-stu-id="96b28-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="96b28-168">請注意，除了更新購物車，我們也會更新購物車總計。</span><span class="sxs-lookup"><span data-stu-id="96b28-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="96b28-169">請注意，這行程式碼特別有趣：</span><span class="sxs-lookup"><span data-stu-id="96b28-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="96b28-170">GetValues （）是我們將在 MyShoppingCart.aspx.cs 中執行的特殊 helper 函式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="96b28-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="96b28-171">這可讓您以全新的方式存取 GridView 控制項中繫結項目的值。</span><span class="sxs-lookup"><span data-stu-id="96b28-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="96b28-172">因為我們的「移除專案」核取方塊控制項並未系結，所以我們會透過 FindControl （）方法來存取它。</span><span class="sxs-lookup"><span data-stu-id="96b28-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="96b28-173">在您專案開發的這個階段，我們準備好開始執行結帳程式。</span><span class="sxs-lookup"><span data-stu-id="96b28-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="96b28-174">在這麼做之前，讓我們使用 Visual Studio 來產生成員資格資料庫，並將使用者新增至成員資格存放庫。</span><span class="sxs-lookup"><span data-stu-id="96b28-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="96b28-175">[上一頁](tailspin-spyworks-part-4.md)
> [下一頁](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="96b28-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
