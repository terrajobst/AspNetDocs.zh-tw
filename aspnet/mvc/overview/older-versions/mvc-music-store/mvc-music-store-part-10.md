---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 第10部分：流覽和網站設計的最後更新，結論 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第10部分涵蓋了最後的流覽和更新 。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539365"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="777db-104">第10部分：流覽和網站設計的最後更新，結論</span><span class="sxs-lookup"><span data-stu-id="777db-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>

<span data-ttu-id="777db-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="777db-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="777db-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="777db-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="777db-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="777db-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="777db-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="777db-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="777db-109">第10部分涵蓋流覽和網站設計的最後更新，結論。</span><span class="sxs-lookup"><span data-stu-id="777db-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>

<span data-ttu-id="777db-110">我們已完成網站的所有主要功能，但仍有一些功能可新增至網站導覽、首頁和存放區流覽頁面。</span><span class="sxs-lookup"><span data-stu-id="777db-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="777db-111">建立購物車摘要部分視圖</span><span class="sxs-lookup"><span data-stu-id="777db-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="777db-112">我們想要在整個網站上公開使用者購物車中的專案數。</span><span class="sxs-lookup"><span data-stu-id="777db-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="777db-113">我們可以藉由建立已新增至我們網站的部分視圖，輕鬆地執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="777db-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="777db-114">如先前所示，ShoppingCart 控制器包含會傳回部分視圖的 CartSummary 動作方法：</span><span class="sxs-lookup"><span data-stu-id="777db-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="777db-115">若要建立 CartSummary 部分視圖，請在 Views/ShoppingCart 資料夾上按一下滑鼠右鍵，然後選取 [加入視圖]。</span><span class="sxs-lookup"><span data-stu-id="777db-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="777db-116">為 view CartSummary 命名，並核取 [建立部分視圖] 核取方塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="777db-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="777db-117">CartSummary 部分視圖其實很簡單，只是 ShoppingCart 索引視圖的連結，它會顯示購物車中的專案數。</span><span class="sxs-lookup"><span data-stu-id="777db-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="777db-118">CartSummary 的完整程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="777db-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="777db-119">我們可以使用 RenderAction 方法，在網站的任何頁面中包含部分視圖，包括網站主機。</span><span class="sxs-lookup"><span data-stu-id="777db-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="777db-120">RenderAction 需要我們指定動作名稱（"CartSummary"）和控制器名稱（"ShoppingCart"），如下所示。</span><span class="sxs-lookup"><span data-stu-id="777db-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="777db-121">在將此內容新增至網站配置之前，我們也會建立 [內容類型] 功能表，讓我們可以將所有網站更新一次。</span><span class="sxs-lookup"><span data-stu-id="777db-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="777db-122">建立 [內容類型] 功能表部分視圖</span><span class="sxs-lookup"><span data-stu-id="777db-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="777db-123">我們可以藉由新增 [內容類型] 功能表（其中列出我們的存放區中所有可用的內容類型），讓使用者更輕鬆地流覽 store。</span><span class="sxs-lookup"><span data-stu-id="777db-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="777db-124">我們會遵循相同的步驟，也會建立 GenreMenu 部分視圖，然後我們可以將它們同時新增至網站主機。</span><span class="sxs-lookup"><span data-stu-id="777db-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="777db-125">首先，將下列 GenreMenu 控制器動作新增至 StoreController：</span><span class="sxs-lookup"><span data-stu-id="777db-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="777db-126">此動作會傳回內容清單，這些內容會由部分視圖顯示，我們將在下一步建立。</span><span class="sxs-lookup"><span data-stu-id="777db-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="777db-127">*注意：我們已將 [ChildActionOnly] 屬性新增至此控制器動作，這表示我們只想要從部分視圖使用此動作。這個屬性會藉由流覽至/Store/GenreMenu. 來防止執行控制器動作部分視圖並不需要這樣做，但這是很好的作法，因為我們想要確定我們的控制器動作會如我們預期的方式使用。我們也會傳回 PartialView 而不是 View，這讓視圖引擎知道它不應該使用此視圖的版面配置，因為它包含在其他視圖中。*</span><span class="sxs-lookup"><span data-stu-id="777db-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="777db-128">以滑鼠右鍵按一下 [GenreMenu 控制器] 動作，並建立名為 GenreMenu 的部分視圖，這是使用內容類型 view 資料類別的強型別，如下所示。</span><span class="sxs-lookup"><span data-stu-id="777db-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="777db-129">更新 GenreMenu 部分視圖的視圖程式碼，以使用未排序的清單來顯示專案，如下所示。</span><span class="sxs-lookup"><span data-stu-id="777db-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="777db-130">正在更新網站版面配置以顯示我們的部分視圖</span><span class="sxs-lookup"><span data-stu-id="777db-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="777db-131">我們可以藉由呼叫 RenderAction （），將我們的部分觀點新增至網站配置（/Views/Shared/\_Layout）。</span><span class="sxs-lookup"><span data-stu-id="777db-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="777db-132">我們會在中新增這兩個專案，以及用來顯示它們的一些額外標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="777db-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="777db-133">現在當我們執行應用程式時，我們會在左側導覽區域中看到內容類型，並在頂端看到購物車摘要。</span><span class="sxs-lookup"><span data-stu-id="777db-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="777db-134">更新存放區流覽頁面</span><span class="sxs-lookup"><span data-stu-id="777db-134">Update to the Store Browse page</span></span>

<span data-ttu-id="777db-135">[存放區流覽] 頁面可正常運作，但外觀不佳。</span><span class="sxs-lookup"><span data-stu-id="777db-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="777db-136">我們可以藉由更新視圖程式碼（在/Views/Store/Browse.cshtml 中找到）來更新頁面，以更佳的版面配置顯示專輯，如下所示：</span><span class="sxs-lookup"><span data-stu-id="777db-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="777db-137">我們使用的是 Url，而不是 Html.actionlink，讓我們可以將特殊的格式套用至連結以包含專輯作品。</span><span class="sxs-lookup"><span data-stu-id="777db-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="777db-138">*注意：我們會顯示這些專輯的一般專輯封面。這項資訊會儲存在資料庫中，而且可透過存放區管理員來編輯。歡迎您加入自己的作品。*</span><span class="sxs-lookup"><span data-stu-id="777db-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="777db-139">現在當我們流覽至內容類型時，我們會在方格中看到以專輯圖案顯示的專輯。</span><span class="sxs-lookup"><span data-stu-id="777db-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="777db-140">更新首頁以顯示熱門銷售專輯</span><span class="sxs-lookup"><span data-stu-id="777db-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="777db-141">我們想要在首頁上為我們的頂尖銷售專輯提供功能，以增加銷售。</span><span class="sxs-lookup"><span data-stu-id="777db-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="777db-142">我們會對我們的 HomeController 進行一些更新，以處理這種情況，並同時新增一些其他圖形。</span><span class="sxs-lookup"><span data-stu-id="777db-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="777db-143">首先，我們會將導覽屬性新增至我們的專輯類別，讓 EntityFramework 知道它們是相關聯的。</span><span class="sxs-lookup"><span data-stu-id="777db-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="777db-144">**專輯**類別的最後幾行現在看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="777db-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="777db-145">*注意：這將需要加入 using 語句來帶入 System.web 命名空間。*</span><span class="sxs-lookup"><span data-stu-id="777db-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="777db-146">首先，我們會使用語句來新增 storeDB 欄位和 MvcMusicStore，如同在我們的其他控制器中一樣。</span><span class="sxs-lookup"><span data-stu-id="777db-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="777db-147">接下來，我們會將下列方法新增至 HomeController，以查詢我們的資料庫，根據 OrderDetails 尋找最熱門的銷售專輯。</span><span class="sxs-lookup"><span data-stu-id="777db-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="777db-148">這是私用方法，因為我們不想讓它當做控制器動作來使用。</span><span class="sxs-lookup"><span data-stu-id="777db-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="777db-149">為了簡單起見，我們在 HomeController 中包含它，但建議您視需要將商務邏輯移至不同的服務類別。</span><span class="sxs-lookup"><span data-stu-id="777db-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="777db-150">備妥之後，我們可以更新 [索引控制器] 動作來查詢前5名銷售專輯，並將其傳回給視圖。</span><span class="sxs-lookup"><span data-stu-id="777db-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="777db-151">已更新之 HomeController 的完整程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="777db-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="777db-152">最後，我們需要更新 [主目錄] 視圖，使其可以藉由更新模型類型並將 [專輯清單] 新增至底部來顯示專輯清單。</span><span class="sxs-lookup"><span data-stu-id="777db-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="777db-153">我們也會利用這個機會，將標題和升級區段新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="777db-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="777db-154">現在當我們執行應用程式時，我們會看到我們已更新的首頁，其中包含最高的銷售專輯和我們的促銷訊息。</span><span class="sxs-lookup"><span data-stu-id="777db-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="777db-155">結論</span><span class="sxs-lookup"><span data-stu-id="777db-155">Conclusion</span></span>

<span data-ttu-id="777db-156">我們已瞭解 ASP.NET MVC 可讓您輕鬆地建立具有資料庫存取權、成員資格、AJAX 等的精密網站。</span><span class="sxs-lookup"><span data-stu-id="777db-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="777db-157">非常快速。</span><span class="sxs-lookup"><span data-stu-id="777db-157">pretty quickly.</span></span> <span data-ttu-id="777db-158">希望本教學課程提供您開始建立自己的 ASP.NET MVC 應用程式所需的工具！</span><span class="sxs-lookup"><span data-stu-id="777db-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="777db-159">上一篇</span><span class="sxs-lookup"><span data-stu-id="777db-159">Previous</span></span>](mvc-music-store-part-9.md)
