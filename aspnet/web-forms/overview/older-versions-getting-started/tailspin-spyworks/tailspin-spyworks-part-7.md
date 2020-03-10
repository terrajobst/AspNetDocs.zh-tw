---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 第7部分：新增功能 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第7部分新增額外的功能，例如 account revie 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641992"
---
# <a name="part-7-adding-features"></a><span data-ttu-id="58864-104">第7部分：新增功能</span><span class="sxs-lookup"><span data-stu-id="58864-104">Part 7: Adding Features</span></span>

<span data-ttu-id="58864-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="58864-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="58864-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="58864-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="58864-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="58864-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="58864-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="58864-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="58864-109">第7部分新增額外的功能，例如帳戶審查、產品評論和「常用專案」，以及「也購買」的使用者控制項。</span><span class="sxs-lookup"><span data-stu-id="58864-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>

## <a id="_Toc260221673"></a><span data-ttu-id="58864-110">新增功能</span><span class="sxs-lookup"><span data-stu-id="58864-110">Adding Features</span></span>

<span data-ttu-id="58864-111">雖然使用者可以流覽我們的目錄、將專案放在其購物車中，以及完成結帳程式，但我們將會包含一些支援功能來改善我們的網站。</span><span class="sxs-lookup"><span data-stu-id="58864-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="58864-112">帳戶審查（列出訂單及查看詳細資料）。</span><span class="sxs-lookup"><span data-stu-id="58864-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="58864-113">將一些內容特定內容新增至 front 頁面。</span><span class="sxs-lookup"><span data-stu-id="58864-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="58864-114">新增功能，讓使用者能夠查看目錄中的產品。</span><span class="sxs-lookup"><span data-stu-id="58864-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="58864-115">建立使用者控制項來顯示熱門專案，並將該控制項放在 front 頁面上。</span><span class="sxs-lookup"><span data-stu-id="58864-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="58864-116">建立「也已購買」使用者控制項，並將它新增至產品詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="58864-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="58864-117">新增連絡人頁面。</span><span class="sxs-lookup"><span data-stu-id="58864-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="58864-118">新增 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="58864-118">Add an About Page.</span></span>
8. <span data-ttu-id="58864-119">全域錯誤</span><span class="sxs-lookup"><span data-stu-id="58864-119">Global Error</span></span>

## <a id="_Toc260221674"></a><span data-ttu-id="58864-120">帳戶審查</span><span class="sxs-lookup"><span data-stu-id="58864-120">Account Review</span></span>

<span data-ttu-id="58864-121">在 [帳戶] 資料夾中，建立名為 OrderList 的兩個 .aspx 頁面，另一個名為 OrderDetails .aspx</span><span class="sxs-lookup"><span data-stu-id="58864-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="58864-122">OrderList 會利用 GridView 和 EntityDataSource 控制項，就像我們之前的一樣。</span><span class="sxs-lookup"><span data-stu-id="58864-122">OrderList.aspx will leverage the GridView and EntityDataSource controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="58864-123">EntityDataSource 會根據使用者登入時，在會話變數中設定的 [Orders] 資料表中，選取已篩選的記錄（請參閱 WhereParameter）。</span><span class="sxs-lookup"><span data-stu-id="58864-123">The EntityDataSource selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="58864-124">另請注意 GridView HyperlinkField 中的這些參數：</span><span class="sxs-lookup"><span data-stu-id="58864-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="58864-125">這些會針對每個產品指定 [訂單詳細資料] 視圖的連結，並將 [訂單] 欄位指定為 OrderDetails 的 QueryString 參數。</span><span class="sxs-lookup"><span data-stu-id="58864-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a><span data-ttu-id="58864-126">OrderDetails .aspx</span><span class="sxs-lookup"><span data-stu-id="58864-126">OrderDetails.aspx</span></span>

<span data-ttu-id="58864-127">我們將使用 EntityDataSource 控制項來存取訂單和 FormView，以顯示訂單資料和另一個具有 GridView 的 EntityDataSource，以顯示所有訂單的明細專案。</span><span class="sxs-lookup"><span data-stu-id="58864-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="58864-128">在程式碼後置檔案（OrderDetails.aspx.cs）中，我們有兩個小部分的維護。</span><span class="sxs-lookup"><span data-stu-id="58864-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="58864-129">首先，我們必須確定 OrderDetails 一律會取得「訂單」。</span><span class="sxs-lookup"><span data-stu-id="58864-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="58864-130">我們也需要計算並顯示明細專案的訂單總計。</span><span class="sxs-lookup"><span data-stu-id="58864-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a><span data-ttu-id="58864-131">首頁</span><span class="sxs-lookup"><span data-stu-id="58864-131">The Home Page</span></span>

<span data-ttu-id="58864-132">讓我們將一些靜態內容新增至 default.aspx 頁面。</span><span class="sxs-lookup"><span data-stu-id="58864-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="58864-133">首先我要建立一個 [Content （內容）] 資料夾，並在其中包含 [Images （首頁）] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="58864-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="58864-134">在 default.aspx 頁面的底部預留位置中，新增下列標記。</span><span class="sxs-lookup"><span data-stu-id="58864-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a><span data-ttu-id="58864-135">產品評論</span><span class="sxs-lookup"><span data-stu-id="58864-135">Product Reviews</span></span>

<span data-ttu-id="58864-136">首先，我們會新增一個按鈕，其中包含可供我們用來輸入產品評論的表單連結。</span><span class="sxs-lookup"><span data-stu-id="58864-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="58864-137">請注意，我們會在查詢字串中傳遞 ProductID</span><span class="sxs-lookup"><span data-stu-id="58864-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="58864-138">接下來，我們將新增名為 ReviewAdd 的頁面</span><span class="sxs-lookup"><span data-stu-id="58864-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="58864-139">此頁面會使用 ASP.NET AJAX 控制項工具組。</span><span class="sxs-lookup"><span data-stu-id="58864-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="58864-140">如果您還沒有這麼做，可以從[DevExpress](http://devexpress.com/act)下載，而且有關于設定工具組以用於此處[https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)之 Visual Studio 的指導方針。</span><span class="sxs-lookup"><span data-stu-id="58864-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="58864-141">在設計模式中，從 [工具箱] 拖曳控制項和驗證器，並建立如下所示的表單。</span><span class="sxs-lookup"><span data-stu-id="58864-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="58864-142">標記看起來會像這樣。</span><span class="sxs-lookup"><span data-stu-id="58864-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="58864-143">現在我們可以輸入評論，讓我們在 [產品] 頁面上顯示這些評論。</span><span class="sxs-lookup"><span data-stu-id="58864-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="58864-144">將此標記新增至 [ProductDetails] 頁面。</span><span class="sxs-lookup"><span data-stu-id="58864-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="58864-145">立即執行我們的應用程式，並流覽至產品，其中會顯示產品資訊，包括客戶評論。</span><span class="sxs-lookup"><span data-stu-id="58864-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a><span data-ttu-id="58864-146">熱門專案控制項（建立使用者控制項）</span><span class="sxs-lookup"><span data-stu-id="58864-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="58864-147">為了增加網站的銷售額，我們會將幾項功能新增至「暗示銷售」熱門或相關的產品。</span><span class="sxs-lookup"><span data-stu-id="58864-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="58864-148">這些功能的第一項是產品目錄中更熱門的產品清單。</span><span class="sxs-lookup"><span data-stu-id="58864-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="58864-149">我們會建立「使用者控制項」，以在應用程式的首頁上顯示最前面的銷售專案。</span><span class="sxs-lookup"><span data-stu-id="58864-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="58864-150">因為這會是控制項，所以我們可以在任何頁面上使用它，只要在 Visual Studio 的設計工具中，將控制項拖放到想要的任何頁面上即可。</span><span class="sxs-lookup"><span data-stu-id="58864-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="58864-151">在 Visual Studio 的方案 explorer 中，以滑鼠右鍵按一下方案名稱，然後建立名為 "Controls" 的新目錄。</span><span class="sxs-lookup"><span data-stu-id="58864-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="58864-152">雖然不需要這麼做，但我們會在「控制項」目錄中建立所有的使用者控制項，以協助保護專案的組織。</span><span class="sxs-lookup"><span data-stu-id="58864-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="58864-153">以滑鼠右鍵按一下 [控制項] 資料夾，然後選擇 [新增專案]：</span><span class="sxs-lookup"><span data-stu-id="58864-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="58864-154">為我們的 "PopularItems" 控制項指定名稱。</span><span class="sxs-lookup"><span data-stu-id="58864-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="58864-155">請注意，使用者控制項的副檔名為 .ascx，而不是 .aspx。</span><span class="sxs-lookup"><span data-stu-id="58864-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="58864-156">我們的熱門專案使用者控制項將定義如下。</span><span class="sxs-lookup"><span data-stu-id="58864-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="58864-157">在這裡，我們將使用我們尚未在此應用程式中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="58864-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="58864-158">我們使用的是中繼器控制項，而不是使用資料來源控制項，我們會將 Repeater 控制項系結至 LINQ to Entities 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="58864-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="58864-159">在控制項背後的程式碼中，我們會執行此動作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="58864-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="58864-160">請注意，我們在控制項標記的頂端也會看到這一行重要的程式碼。</span><span class="sxs-lookup"><span data-stu-id="58864-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="58864-161">由於最受歡迎的專案不會每分鐘變更一次，因此我們可以新增 aching 指示詞來改善應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="58864-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="58864-162">這個指示詞只會在控制項的快取輸出過期時，才執行控制項程式碼。</span><span class="sxs-lookup"><span data-stu-id="58864-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="58864-163">否則，將會使用控制項輸出的快取版本。</span><span class="sxs-lookup"><span data-stu-id="58864-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="58864-164">我們只需要在 default.aspx 頁面中加入新的控制項即可。</span><span class="sxs-lookup"><span data-stu-id="58864-164">Now all we have to do is include our new control in our Default.aspx page.</span></span>

<span data-ttu-id="58864-165">使用拖放功能，將控制項的實例放在預設表單的 [開啟] 資料行中。</span><span class="sxs-lookup"><span data-stu-id="58864-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="58864-166">現在當我們執行應用程式時，首頁會顯示最受歡迎的專案。</span><span class="sxs-lookup"><span data-stu-id="58864-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a><span data-ttu-id="58864-167">「也購買」控制項（具有參數的使用者控制項）</span><span class="sxs-lookup"><span data-stu-id="58864-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="58864-168">我們所建立的第二個使用者控制項，會藉由新增內容的明確性，讓您有更好的銷售。</span><span class="sxs-lookup"><span data-stu-id="58864-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="58864-169">計算前「也已購買」專案的邏輯並不簡單。</span><span class="sxs-lookup"><span data-stu-id="58864-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="58864-170">我們的「也已購買」控制項將會針對目前選取的 ProductID 選取 OrderDetails 記錄（先前購買的），並針對每個找到的唯一訂單取得 Orderid。</span><span class="sxs-lookup"><span data-stu-id="58864-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="58864-171">然後，我們會選取所有訂單中的產品，並加總購買的數量。</span><span class="sxs-lookup"><span data-stu-id="58864-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="58864-172">我們會依該數量總和排序產品，並顯示前五個專案。</span><span class="sxs-lookup"><span data-stu-id="58864-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="58864-173">基於此邏輯的複雜度，我們會將此演算法實作為預存程式。</span><span class="sxs-lookup"><span data-stu-id="58864-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="58864-174">預存程式的 T-sql 如下所示。</span><span class="sxs-lookup"><span data-stu-id="58864-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="58864-175">請注意，當我們在應用程式中包含此預存程式（SelectPurchasedWithProducts）時，資料庫中會有此預存程式，而當我們所指定的實體資料模型，除了我們所需的資料表和 Views 以外，實體資料模型應該包含此預存程式。</span><span class="sxs-lookup"><span data-stu-id="58864-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="58864-176">若要從實體資料模型存取預存程式，我們必須匯入函數。</span><span class="sxs-lookup"><span data-stu-id="58864-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="58864-177">按兩下 [方案瀏覽器] 中的 [實體資料模型]，在設計工具中開啟它並開啟 [模型瀏覽器]，然後在設計工具中按一下滑鼠右鍵，然後選取 [加入函式匯入]。</span><span class="sxs-lookup"><span data-stu-id="58864-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="58864-178">這麼做會開啟此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="58864-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="58864-179">如下所示填寫欄位，並選取 "SelectPurchasedWithProducts"，並使用程式名稱作為匯入函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="58864-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="58864-180">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="58864-180">Click "Ok".</span></span>

<span data-ttu-id="58864-181">完成這項作業之後，就可以像在模型中的其他專案一樣，對預存程式進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="58864-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="58864-182">因此，在我們的 "Controls" 資料夾中，建立名為 AlsoPurchased 的新使用者控制項。</span><span class="sxs-lookup"><span data-stu-id="58864-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="58864-183">這個控制項的標記看起來很熟悉 PopularItems 控制項。</span><span class="sxs-lookup"><span data-stu-id="58864-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="58864-184">值得注意的差異在於，因為要轉譯的專案會依產品而有所不同，所以不會快取輸出。</span><span class="sxs-lookup"><span data-stu-id="58864-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="58864-185">ProductId 會是控制項的「屬性」。</span><span class="sxs-lookup"><span data-stu-id="58864-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="58864-186">在控制項的可呈現事件處理常式中，我們 eed 執行三項工作。</span><span class="sxs-lookup"><span data-stu-id="58864-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="58864-187">請確定已設定 ProductID。</span><span class="sxs-lookup"><span data-stu-id="58864-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="58864-188">查看是否有任何已使用目前產品購買的產品。</span><span class="sxs-lookup"><span data-stu-id="58864-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="58864-189">輸出 #2 中判斷的某些專案。</span><span class="sxs-lookup"><span data-stu-id="58864-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="58864-190">請注意，透過模型呼叫預存程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="58864-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="58864-191">判斷「也已購買」之後，我們可以直接將中繼器系結至查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="58864-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="58864-192">如果沒有任何「也購買」的專案，我們只會顯示類別目錄中的其他熱門專案。</span><span class="sxs-lookup"><span data-stu-id="58864-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="58864-193">若要查看「也購買」的專案，請開啟 [ProductDetails] 頁面，並從 [方案瀏覽器] 拖曳 AlsoPurchased 控制項，使其出現在標記中的這個位置。</span><span class="sxs-lookup"><span data-stu-id="58864-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="58864-194">這麼做會在 [ProductDetails] 頁面頂端建立控制項的參考。</span><span class="sxs-lookup"><span data-stu-id="58864-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="58864-195">因為 AlsoPurchased 使用者控制項需要 ProductId 編號，所以我們會針對頁面的目前資料模型專案使用 Eval 語句，以設定控制項的 ProductID 屬性。</span><span class="sxs-lookup"><span data-stu-id="58864-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="58864-196">當我們建立並立即執行並流覽至產品時，我們會看到「也購買」的專案。</span><span class="sxs-lookup"><span data-stu-id="58864-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="58864-197">[上一頁](tailspin-spyworks-part-6.md)
> [下一頁](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="58864-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
