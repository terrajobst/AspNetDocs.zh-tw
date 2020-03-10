---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: 檢查 Details 和 Delete 方法 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 37787a26f37473b9d36792a9f7715982cb274074
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599684"
---
# <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="66bf3-104">檢查 Details 和 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="66bf3-104">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="66bf3-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="66bf3-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="66bf3-106">本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="66bf3-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="66bf3-107">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="66bf3-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="66bf3-108">在本教學課程的這個部分中，您將會檢查自動產生的 `Details` 和 `Delete` 方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-108">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="66bf3-109">檢查 Details 和 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="66bf3-109">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="66bf3-110">開啟 `Movie` 控制器，並檢查 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-110">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="66bf3-111">建立此動作方法的 MVC 樣板引擎會加入批註，其中會顯示叫用方法的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="66bf3-111">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="66bf3-112">在此情況下，它是具有三個 URL 區段、`Movies` 控制器、`Details` 方法和 `ID` 值的 `GET` 要求。</span><span class="sxs-lookup"><span data-stu-id="66bf3-112">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="66bf3-113">Code First 可讓您輕鬆地使用 `Find` 方法來搜尋資料。</span><span class="sxs-lookup"><span data-stu-id="66bf3-113">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="66bf3-114">方法內建一項重要的安全性功能，就是程式碼確認 `Find` 方法在程式碼嘗試執行任何動作之前，已找到電影。</span><span class="sxs-lookup"><span data-stu-id="66bf3-114">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="66bf3-115">例如，駭客可能會將連結所建立的 URL 從 `http://localhost:xxxx/Movies/Details/1` 變更為類似 `http://localhost:xxxx/Movies/Details/12345` （或其他不代表實際電影的其他值），藉此將錯誤導入網站中。</span><span class="sxs-lookup"><span data-stu-id="66bf3-115">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="66bf3-116">如果您未檢查是否有 null 電影，null 電影會導致資料庫錯誤。</span><span class="sxs-lookup"><span data-stu-id="66bf3-116">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="66bf3-117">檢查 `Delete` 和 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-117">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="66bf3-118">請注意，`HTTP Get``Delete` 方法不會刪除指定的電影，它會傳回電影的觀看畫面，您可以在其中提交（`HttpPost`）刪除。</span><span class="sxs-lookup"><span data-stu-id="66bf3-118">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="66bf3-119">如果您執行刪除作業以回應 GET 要求 (或是執行相關編輯作業、建立作業或任何會變更資料的其他作業)，則會造成安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="66bf3-119">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="66bf3-120">如需有關此情況的詳細資訊，請參閱 Stephen Walther 的 blog 專案[ASP.NET MVC Tip #46-請勿使用刪除連結，因為它們會建立安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。</span><span class="sxs-lookup"><span data-stu-id="66bf3-120">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="66bf3-121">我們將可刪除資料的 `HttpPost` 方法命名為 `DeleteConfirmed`，以提供 HTTP POST 方法的唯一簽章或名稱。</span><span class="sxs-lookup"><span data-stu-id="66bf3-121">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="66bf3-122">這兩個方法簽章如下所示：</span><span class="sxs-lookup"><span data-stu-id="66bf3-122">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="66bf3-123">通用語言執行平台 (CLR) 需要多載方法，以提供唯一的參數簽章 (方法名稱相同但參數清單不同)。</span><span class="sxs-lookup"><span data-stu-id="66bf3-123">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="66bf3-124">不過，在這裡您需要兩個 Delete 方法，一個用於 GET，另一個用於 POST--兩者都有相同的參數簽章。</span><span class="sxs-lookup"><span data-stu-id="66bf3-124">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="66bf3-125">(它們都需要接受單一整數作為參數)。</span><span class="sxs-lookup"><span data-stu-id="66bf3-125">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="66bf3-126">若要將其排序，您可以執行幾項工作。</span><span class="sxs-lookup"><span data-stu-id="66bf3-126">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="66bf3-127">其中一個是提供不同名稱的方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-127">One is to give the methods different names.</span></span> <span data-ttu-id="66bf3-128">這是 scaffolding 機制在上述範例採取的方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-128">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="66bf3-129">不過，這麼做會導致一個小問題：ASP.NET 會依名稱將 URL 區段與動作方法對應，一旦您重新命名方法，路由通常就會找不到這個方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-129">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="66bf3-130">解決辦法正如您看到的這個範例：將 `ActionName("Delete")` 屬性新增至 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-130">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="66bf3-131">這會有效地執行路由系統的對應，使包含 POST 要求<em>/Delete/</em>的 URL 會找到 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="66bf3-131">This effectively performs mapping for the routing system so that a URL that includes <em>/Delete/</em>for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="66bf3-132">另一個避免具有相同名稱和簽章之方法發生問題的常見方法，就是將 POST 方法的簽章變更為包含未使用的參數。</span><span class="sxs-lookup"><span data-stu-id="66bf3-132">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="66bf3-133">例如，有些開發人員會加入一個參數型別，`FormCollection` 傳遞至 POST 方法，然後直接不使用參數：</span><span class="sxs-lookup"><span data-stu-id="66bf3-133">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="66bf3-134">總結</span><span class="sxs-lookup"><span data-stu-id="66bf3-134">Summary</span></span>

<span data-ttu-id="66bf3-135">您現在有一個完整的 ASP.NET MVC 應用程式，可將資料儲存在本機 DB 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="66bf3-135">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="66bf3-136">您可以建立、讀取、更新、刪除及搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="66bf3-136">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="66bf3-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66bf3-137">Next Steps</span></span>

<span data-ttu-id="66bf3-138">在您建立並測試 web 應用程式之後，下一個步驟是讓其他人可以透過網際網路使用它。</span><span class="sxs-lookup"><span data-stu-id="66bf3-138">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="66bf3-139">若要這麼做，您必須將它部署到 web 主控提供者。</span><span class="sxs-lookup"><span data-stu-id="66bf3-139">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="66bf3-140">Microsoft 在[免費的 Windows Azure 試用帳戶](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中，最多可為10個網站提供免費的 web 主機。</span><span class="sxs-lookup"><span data-stu-id="66bf3-140">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="66bf3-141">我建議您接著遵循我的教學課程，將[具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="66bf3-141">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="66bf3-142">一個絕佳的教學課程是 Tom 作者: dykstra 的中繼層級，[為 ASP.NET MVC 應用程式建立 Entity Framework 資料模型](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="66bf3-142">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="66bf3-143">[Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 論壇](https://forums.asp.net/1146.aspx)是提出問題的絕佳地方。</span><span class="sxs-lookup"><span data-stu-id="66bf3-143">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="66bf3-144">請在 twitter 上追蹤[我](https://twitter.com/RickAndMSFT)的最新教學課程，以取得更新。</span><span class="sxs-lookup"><span data-stu-id="66bf3-144">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="66bf3-145">歡迎您提供意見反應。</span><span class="sxs-lookup"><span data-stu-id="66bf3-145">Feedback is welcome.</span></span>

<span data-ttu-id="66bf3-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="66bf3-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="66bf3-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter： [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="66bf3-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="66bf3-148">上一篇</span><span class="sxs-lookup"><span data-stu-id="66bf3-148">Previous</span></span>](adding-validation-to-the-model.md)
