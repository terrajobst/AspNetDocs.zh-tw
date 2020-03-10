---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 使用輸出快取改善效能（VB） |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何利用輸出快取來大幅提升 ASP.NET MVC web 應用程式的效能。 您 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: b713b56e149f196794b3223ba88e3b41bf3e34c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601245"
---
# <a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="880b9-104">使用輸出快取改善效能 (VB)</span><span class="sxs-lookup"><span data-stu-id="880b9-104">Improving Performance with Output Caching (VB)</span></span>

<span data-ttu-id="880b9-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="880b9-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="880b9-106">在本教學課程中，您將瞭解如何利用輸出快取來大幅提升 ASP.NET MVC web 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="880b9-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="880b9-107">您將瞭解如何快取控制器動作傳回的結果，如此一來，每次新的使用者叫用動作時，都不需要建立相同的內容。</span><span class="sxs-lookup"><span data-stu-id="880b9-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>

<span data-ttu-id="880b9-108">本教學課程的目的是要說明如何利用輸出快取來大幅提升 ASP.NET MVC 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="880b9-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="880b9-109">輸出快取可讓您快取控制器動作所傳回的內容。</span><span class="sxs-lookup"><span data-stu-id="880b9-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="880b9-110">如此一來，每次叫用相同的控制器動作時，都不需要產生相同的內容。</span><span class="sxs-lookup"><span data-stu-id="880b9-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="880b9-111">例如，假設您的 ASP.NET MVC 應用程式會在名為 Index 的視圖中顯示資料庫記錄清單。</span><span class="sxs-lookup"><span data-stu-id="880b9-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="880b9-112">一般來說，每次使用者叫用傳回索引視圖的控制器動作時，都必須藉由執行資料庫查詢，從資料庫中抓取資料庫記錄集。</span><span class="sxs-lookup"><span data-stu-id="880b9-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="880b9-113">另一方面，如果您利用輸出快取，則每次使用者叫用相同的控制器動作時，都可以避免執行資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="880b9-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="880b9-114">您可以從快取中抓取此視圖，而不是從控制器動作重新產生。</span><span class="sxs-lookup"><span data-stu-id="880b9-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="880b9-115">快取可讓您避免在伺服器上執行多餘的工作。</span><span class="sxs-lookup"><span data-stu-id="880b9-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="880b9-116">啟用輸出快取</span><span class="sxs-lookup"><span data-stu-id="880b9-116">Enabling Output Caching</span></span>

<span data-ttu-id="880b9-117">若要啟用輸出快取，請將 &lt;OutputCache&gt; 屬性新增至個別的控制器動作或整個控制器類別。</span><span class="sxs-lookup"><span data-stu-id="880b9-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="880b9-118">例如，[清單 1] 中的控制器會公開名為 Index （）的動作。</span><span class="sxs-lookup"><span data-stu-id="880b9-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="880b9-119">索引（）動作的輸出會快取10秒。</span><span class="sxs-lookup"><span data-stu-id="880b9-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="880b9-120">**清單1– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="880b9-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

<span data-ttu-id="880b9-121">在 ASP.NET MVC 的 Beta 版中，輸出快取不適用於[http://www.MySite.com/](http://www.mysite.com/)之類的 URL。</span><span class="sxs-lookup"><span data-stu-id="880b9-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="880b9-122">相反地，您必須輸入類似[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。</span><span class="sxs-lookup"><span data-stu-id="880b9-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>

<span data-ttu-id="880b9-123">在 [清單 1] 中，索引（）動作的輸出會快取10秒。</span><span class="sxs-lookup"><span data-stu-id="880b9-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="880b9-124">如果您想要的話，也可以指定較長的快取持續時間。</span><span class="sxs-lookup"><span data-stu-id="880b9-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="880b9-125">例如，如果您想要快取一天的控制器動作輸出，您可以指定86400秒的快取持續時間（60秒 \* 60 分鐘 \* 24 小時）。</span><span class="sxs-lookup"><span data-stu-id="880b9-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="880b9-126">並不保證會針對您指定的時間長度快取內容。</span><span class="sxs-lookup"><span data-stu-id="880b9-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="880b9-127">當記憶體資源變低時，快取會開始自動收回內容。</span><span class="sxs-lookup"><span data-stu-id="880b9-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="880b9-128">[清單 1] 中的 Home 控制器會傳回 [清單 2] 中的索引視圖。</span><span class="sxs-lookup"><span data-stu-id="880b9-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="880b9-129">這個觀點沒有什麼特殊之處。</span><span class="sxs-lookup"><span data-stu-id="880b9-129">There is nothing special about this view.</span></span> <span data-ttu-id="880b9-130">[索引] 視圖只會顯示目前的時間（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="880b9-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="880b9-131">**清單2– Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="880b9-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="880b9-132">**圖1–快取的索引視圖**</span><span class="sxs-lookup"><span data-stu-id="880b9-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="880b9-134">如果您藉由在瀏覽器的網址列中輸入 URL/Home/Index 來多次叫用 Index （）動作，並重複地在瀏覽器中按下 [重新整理]/[重載] 按鈕，則索引視圖所顯示的時間不會變更10秒。</span><span class="sxs-lookup"><span data-stu-id="880b9-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="880b9-135">會顯示相同的時間，因為已快取此視圖。</span><span class="sxs-lookup"><span data-stu-id="880b9-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="880b9-136">請務必瞭解，所有造訪您應用程式的人都會快取相同的觀點。</span><span class="sxs-lookup"><span data-stu-id="880b9-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="880b9-137">叫用 Index （）動作的任何人都會取得相同的快取版本的索引視圖。</span><span class="sxs-lookup"><span data-stu-id="880b9-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="880b9-138">這表示，web 伺服器必須執行以服務索引視圖的工作量會大幅降低。</span><span class="sxs-lookup"><span data-stu-id="880b9-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="880b9-139">[清單 2] 中的觀點剛好是這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="880b9-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="880b9-140">此視圖只會顯示目前的時間。</span><span class="sxs-lookup"><span data-stu-id="880b9-140">The view just displays the current time.</span></span> <span data-ttu-id="880b9-141">不過，您可以輕鬆快取顯示一組資料庫記錄的視圖。</span><span class="sxs-lookup"><span data-stu-id="880b9-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="880b9-142">在這種情況下，每次叫用傳回視圖的控制器動作時，都不需要從資料庫中抓取資料庫記錄集。</span><span class="sxs-lookup"><span data-stu-id="880b9-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="880b9-143">快取可以減少 web 伺服器和資料庫伺服器必須執行的工作量。</span><span class="sxs-lookup"><span data-stu-id="880b9-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="880b9-144">請勿在 MVC 視圖中使用頁面 &lt;% @ OutputCache%&gt; 指示詞。</span><span class="sxs-lookup"><span data-stu-id="880b9-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="880b9-145">這個指示詞會從 Web form 世界中不規則，不應用於 ASP.NET MVC 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="880b9-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="880b9-146">內容的快取位置</span><span class="sxs-lookup"><span data-stu-id="880b9-146">Where Content is Cached</span></span>

<span data-ttu-id="880b9-147">根據預設，當您使用 &lt;OutputCache&gt; 屬性時，會在三個位置快取內容：網頁伺服器、任何 proxy 伺服器，以及網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="880b9-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="880b9-148">您可以藉由修改 &lt;OutputCache&gt; 屬性的 Location 屬性，精確地控制快取內容的位置。</span><span class="sxs-lookup"><span data-stu-id="880b9-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="880b9-149">您可以將 Location 屬性設定為下列任何一個值：</span><span class="sxs-lookup"><span data-stu-id="880b9-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="880b9-150">·任何</span><span class="sxs-lookup"><span data-stu-id="880b9-150">· Any</span></span>
> 
> <span data-ttu-id="880b9-151">·台</span><span class="sxs-lookup"><span data-stu-id="880b9-151">· Client</span></span>
> 
> <span data-ttu-id="880b9-152">·數量</span><span class="sxs-lookup"><span data-stu-id="880b9-152">· Downstream</span></span>
> 
> <span data-ttu-id="880b9-153">·伺服器</span><span class="sxs-lookup"><span data-stu-id="880b9-153">· Server</span></span>
> 
> <span data-ttu-id="880b9-154">·無</span><span class="sxs-lookup"><span data-stu-id="880b9-154">· None</span></span>
> 
> <span data-ttu-id="880b9-155">·ServerAndClient</span><span class="sxs-lookup"><span data-stu-id="880b9-155">· ServerAndClient</span></span>

<span data-ttu-id="880b9-156">根據預設，Location 屬性的值為 Any。</span><span class="sxs-lookup"><span data-stu-id="880b9-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="880b9-157">不過，在某些情況下，您可能只想要在瀏覽器上或只在伺服器上快取。</span><span class="sxs-lookup"><span data-stu-id="880b9-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="880b9-158">例如，如果您要快取每個使用者個人化的資訊，則不應該快取伺服器上的資訊。</span><span class="sxs-lookup"><span data-stu-id="880b9-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="880b9-159">如果您要向不同的使用者顯示不同的資訊，您應該只在用戶端上快取資訊。</span><span class="sxs-lookup"><span data-stu-id="880b9-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="880b9-160">例如，[清單 3] 中的控制器會公開名為 GetName （）的動作，以傳回目前的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="880b9-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="880b9-161">如果「插孔」登入網站並叫用 GetName （）動作，則動作會傳回「Hi 的插座」字串。</span><span class="sxs-lookup"><span data-stu-id="880b9-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="880b9-162">之後，如果 Jill 登入網站並叫用 GetName （）動作，她也會取得字串 "Hi"。</span><span class="sxs-lookup"><span data-stu-id="880b9-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="880b9-163">在一開始叫用控制器動作之後，所有使用者都會在 web 伺服器上快取字串。</span><span class="sxs-lookup"><span data-stu-id="880b9-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="880b9-164">**清單3– Controllers\BadUserController.vb**</span><span class="sxs-lookup"><span data-stu-id="880b9-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="880b9-165">最有可能的情況是，[清單 3] 中的控制器不會以您想要的方式運作。</span><span class="sxs-lookup"><span data-stu-id="880b9-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="880b9-166">您不想要對 Jill 顯示「Hi 插座」訊息。</span><span class="sxs-lookup"><span data-stu-id="880b9-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="880b9-167">您絕對不應該快取伺服器快取中的個人化內容。</span><span class="sxs-lookup"><span data-stu-id="880b9-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="880b9-168">不過，您可能會想要在瀏覽器快取中快取個人化的內容，以改善效能。</span><span class="sxs-lookup"><span data-stu-id="880b9-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="880b9-169">如果您在瀏覽器中快取內容，且使用者多次叫用相同的控制器動作，則可以從瀏覽器快取中抓取內容，而不是從伺服器抓取。</span><span class="sxs-lookup"><span data-stu-id="880b9-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="880b9-170">清單4中修改過的控制器會快取 GetName （）動作的輸出。</span><span class="sxs-lookup"><span data-stu-id="880b9-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="880b9-171">不過，只會在瀏覽器上快取內容，而不是在伺服器上快取。</span><span class="sxs-lookup"><span data-stu-id="880b9-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="880b9-172">如此一來，當多位使用者叫用 GetName （）方法時，每個人都會取得自己的使用者名稱，而不是另一個人的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="880b9-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="880b9-173">**清單4– Controllers\UserController.vb**</span><span class="sxs-lookup"><span data-stu-id="880b9-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="880b9-174">請注意，[清單 4] 中的 [&lt;OutputCache&gt;] 屬性包含將 Location 屬性設定為值 OutputCacheLocation. Client。</span><span class="sxs-lookup"><span data-stu-id="880b9-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="880b9-175">&lt;OutputCache&gt; 屬性也包含 NoStore 屬性。</span><span class="sxs-lookup"><span data-stu-id="880b9-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="880b9-176">NoStore 屬性是用來通知 proxy 伺服器和瀏覽器，他們不應該儲存快取內容的永久複本。</span><span class="sxs-lookup"><span data-stu-id="880b9-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="880b9-177">改變輸出快取</span><span class="sxs-lookup"><span data-stu-id="880b9-177">Varying the Output Cache</span></span>

<span data-ttu-id="880b9-178">在某些情況下，您可能會想要有相同內容的不同快取版本。</span><span class="sxs-lookup"><span data-stu-id="880b9-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="880b9-179">例如，假設您要建立主要/詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="880b9-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="880b9-180">主版頁面會顯示電影標題清單。</span><span class="sxs-lookup"><span data-stu-id="880b9-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="880b9-181">當您按一下標題時，會取得所選電影的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="880b9-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="880b9-182">如果您快取 [詳細資料] 頁面，則無論您按一下哪一部電影，都會顯示相同電影的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="880b9-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="880b9-183">第一個使用者選取的第一個電影會顯示給所有未來的使用者。</span><span class="sxs-lookup"><span data-stu-id="880b9-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="880b9-184">您可以利用 &lt;OutputCache&gt; 屬性（attribute）的 VaryByParam 屬性（property），來修正這個問題。</span><span class="sxs-lookup"><span data-stu-id="880b9-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="880b9-185">當表單參數或查詢字串參數不同時，這個屬性可讓您建立相同內容的不同快取版本。</span><span class="sxs-lookup"><span data-stu-id="880b9-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="880b9-186">例如，[清單 5] 中的控制器會公開名為 Master （）和 Details （）的兩個動作。</span><span class="sxs-lookup"><span data-stu-id="880b9-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="880b9-187">主要（）動作會傳回電影標題清單，而 Details （）動作會傳回所選電影的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="880b9-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="880b9-188">**清單5– Controllers\MoviesController.vb**</span><span class="sxs-lookup"><span data-stu-id="880b9-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="880b9-189">Master （）動作包含 VaryByParam 屬性，其值為 "none"。</span><span class="sxs-lookup"><span data-stu-id="880b9-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="880b9-190">叫用 Master （）動作時，會傳回主視圖的相同快取版本。</span><span class="sxs-lookup"><span data-stu-id="880b9-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="880b9-191">系統會忽略任何表單參數或查詢字串參數（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="880b9-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="880b9-192">**圖2–/Movies/Master 視圖**</span><span class="sxs-lookup"><span data-stu-id="880b9-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="880b9-194">**圖3–/Movies/Details 視圖**</span><span class="sxs-lookup"><span data-stu-id="880b9-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="880b9-196">Details （）動作包含 VaryByParam 屬性，其值為 "Id"。</span><span class="sxs-lookup"><span data-stu-id="880b9-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="880b9-197">當 Id 參數的不同值傳遞至控制器動作時，會產生不同的快取版本的詳細資料檢視。</span><span class="sxs-lookup"><span data-stu-id="880b9-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="880b9-198">請務必瞭解，使用 VaryByParam 屬性會導致更快的快取，而不是較少。</span><span class="sxs-lookup"><span data-stu-id="880b9-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="880b9-199">會針對每個不同版本的 Id 參數建立詳細資料檢視的不同快取版本。</span><span class="sxs-lookup"><span data-stu-id="880b9-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="880b9-200">您可以將 VaryByParam 屬性設定為下列值：</span><span class="sxs-lookup"><span data-stu-id="880b9-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="880b9-201">\* = 每當表單或查詢字串參數不同時，建立不同的快取版本。</span><span class="sxs-lookup"><span data-stu-id="880b9-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="880b9-202">無 = 永不建立不同的快取版本</span><span class="sxs-lookup"><span data-stu-id="880b9-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="880b9-203">參數的分號清單 = 每當清單中的任何表單或查詢字串參數改變時，建立不同的快取版本</span><span class="sxs-lookup"><span data-stu-id="880b9-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>

#### <a name="creating-a-cache-profile"></a><span data-ttu-id="880b9-204">建立快取設定檔</span><span class="sxs-lookup"><span data-stu-id="880b9-204">Creating a Cache Profile</span></span>

<span data-ttu-id="880b9-205">除了藉由修改 &lt;OutputCache&gt; 屬性的屬性來設定輸出快取屬性以外，您也可以在 web 設定（web.config）檔案中建立快取設定檔。</span><span class="sxs-lookup"><span data-stu-id="880b9-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="880b9-206">在 web 設定檔中建立快取設定檔可提供幾個重要的優點。</span><span class="sxs-lookup"><span data-stu-id="880b9-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="880b9-207">首先，藉由在 web 設定檔中設定輸出快取，您可以控制控制器動作在單一中央位置快取內容的方式。</span><span class="sxs-lookup"><span data-stu-id="880b9-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="880b9-208">您可以建立一個快取設定檔，並將設定檔套用至數個控制器或控制器動作。</span><span class="sxs-lookup"><span data-stu-id="880b9-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="880b9-209">第二，您可以修改 web 設定檔案，而不需要重新編譯應用程式。</span><span class="sxs-lookup"><span data-stu-id="880b9-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="880b9-210">如果您需要停用已部署至生產環境之應用程式的快取，則可以直接修改 web 設定檔中定義的快取設定檔。</span><span class="sxs-lookup"><span data-stu-id="880b9-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="880b9-211">將會自動偵測並套用對 web 設定檔進行的任何變更。</span><span class="sxs-lookup"><span data-stu-id="880b9-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="880b9-212">例如，[清單 6] 中的 [&lt;快取&gt; web 設定] 區段會定義名為 Cache1Hour 的快取設定檔。</span><span class="sxs-lookup"><span data-stu-id="880b9-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="880b9-213">&lt;快取&gt; 區段必須出現在 web 設定檔的 &lt;system.web&gt; 區段中。</span><span class="sxs-lookup"><span data-stu-id="880b9-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="880b9-214">**[清單 6]-web.config 的快取區段**</span><span class="sxs-lookup"><span data-stu-id="880b9-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="880b9-215">[清單 7] 中的控制器會說明如何將 Cache1Hour 設定檔套用至具有 &lt;OutputCache&gt; 屬性的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="880b9-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="880b9-216">**清單7– Controllers\ProfileController.vb**</span><span class="sxs-lookup"><span data-stu-id="880b9-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="880b9-217">如果您叫用 [清單 7] 中的控制器所公開的 [索引] （）動作，則會傳回1小時的相同時間。</span><span class="sxs-lookup"><span data-stu-id="880b9-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="880b9-218">總結</span><span class="sxs-lookup"><span data-stu-id="880b9-218">Summary</span></span>

<span data-ttu-id="880b9-219">輸出快取提供非常簡單的方法，可大幅提升 ASP.NET MVC 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="880b9-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="880b9-220">在本教學課程中，您已瞭解如何使用 &lt;OutputCache&gt; 屬性來快取控制器動作的輸出。</span><span class="sxs-lookup"><span data-stu-id="880b9-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="880b9-221">您也已瞭解如何修改 &lt;OutputCache&gt; 屬性的屬性（例如 Duration 和 VaryByParam 屬性），以修改內容的快取方式。</span><span class="sxs-lookup"><span data-stu-id="880b9-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="880b9-222">最後，您已瞭解如何在 web 設定檔中定義快取設定檔。</span><span class="sxs-lookup"><span data-stu-id="880b9-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="880b9-223">[上一頁](understanding-action-filters-vb.md)
> [下一頁](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="880b9-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
