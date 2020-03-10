---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 處理實體關聯 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557460"
---
# <a name="handling-entity-relations"></a><span data-ttu-id="e766b-102">處理實體關聯性</span><span class="sxs-lookup"><span data-stu-id="e766b-102">Handling Entity Relations</span></span>

<span data-ttu-id="e766b-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e766b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="e766b-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="e766b-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="e766b-105">本節說明 EF 如何載入相關實體，以及如何在模型類別中處理迴圈導覽屬性的一些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e766b-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="e766b-106">（本節提供背景知識，而且不需要用來完成教學課程。</span><span class="sxs-lookup"><span data-stu-id="e766b-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="e766b-107">如果您想要的話，請跳到[第5部分：](part-5.md)）</span><span class="sxs-lookup"><span data-stu-id="e766b-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="e766b-108">積極式載入與延遲載入</span><span class="sxs-lookup"><span data-stu-id="e766b-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="e766b-109">搭配關係資料庫使用 EF 時，請務必瞭解 EF 如何載入相關資料。</span><span class="sxs-lookup"><span data-stu-id="e766b-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="e766b-110">查看 EF 產生的 SQL 查詢也很有用。</span><span class="sxs-lookup"><span data-stu-id="e766b-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="e766b-111">若要追蹤 SQL，請將下列程式程式碼新增至 `BookServiceContext` 的函式：</span><span class="sxs-lookup"><span data-stu-id="e766b-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="e766b-112">如果您將 GET 要求傳送至/api/books，它會傳回 JSON，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e766b-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="e766b-113">您可以看到 Author 屬性為 null，即使本書包含有效的作者。</span><span class="sxs-lookup"><span data-stu-id="e766b-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="e766b-114">這是因為 EF 不會載入相關的作者實體。</span><span class="sxs-lookup"><span data-stu-id="e766b-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="e766b-115">SQL 查詢的追蹤記錄會確認下列事項：</span><span class="sxs-lookup"><span data-stu-id="e766b-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="e766b-116">SELECT 語句取自 [書籍] 資料表，而且不會參考 [作者] 資料表。</span><span class="sxs-lookup"><span data-stu-id="e766b-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="e766b-117">以下是傳回書籍清單的 `BooksController` 類別中的方法，供您參考。</span><span class="sxs-lookup"><span data-stu-id="e766b-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="e766b-118">我們來看一下如何傳回作者做為 JSON 資料的一部分。</span><span class="sxs-lookup"><span data-stu-id="e766b-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="e766b-119">有三種方式可以在 Entity Framework 中載入相關資料：積極式載入、消極式載入和明確載入。</span><span class="sxs-lookup"><span data-stu-id="e766b-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="e766b-120">每項技術都有取捨，因此請務必瞭解它們的運作方式。</span><span class="sxs-lookup"><span data-stu-id="e766b-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="e766b-121">積極式載入</span><span class="sxs-lookup"><span data-stu-id="e766b-121">Eager Loading</span></span>

<span data-ttu-id="e766b-122">使用*積極式載入*時，EF 會載入相關實體做為初始資料庫查詢的一部分。</span><span class="sxs-lookup"><span data-stu-id="e766b-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="e766b-123">若要執行積極式載入，請使用**system.object. Include**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="e766b-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="e766b-124">這會告訴 EF 將作者資料包含在查詢中。</span><span class="sxs-lookup"><span data-stu-id="e766b-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="e766b-125">如果您進行這類變更並執行應用程式，現在 JSON 資料看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="e766b-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="e766b-126">追蹤記錄檔會顯示 EF 在 Book 和 Author 資料表上執行了聯結。</span><span class="sxs-lookup"><span data-stu-id="e766b-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="e766b-127">消極式載入</span><span class="sxs-lookup"><span data-stu-id="e766b-127">Lazy Loading</span></span>

<span data-ttu-id="e766b-128">使用消極式載入時，EF 會在參考該實體的導覽屬性時，自動載入相關實體。</span><span class="sxs-lookup"><span data-stu-id="e766b-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="e766b-129">若要啟用消極式載入，請將導覽屬性設為 [虛擬]。</span><span class="sxs-lookup"><span data-stu-id="e766b-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="e766b-130">例如，在 Book 類別中：</span><span class="sxs-lookup"><span data-stu-id="e766b-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="e766b-131">現在請考慮下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="e766b-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="e766b-132">啟用消極式載入時，存取 `books[0]` 上的 `Author` 屬性會導致 EF 為作者查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="e766b-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="e766b-133">消極式載入需要多個資料庫往返，因為 EF 會在每次抓取相關實體時傳送查詢。</span><span class="sxs-lookup"><span data-stu-id="e766b-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="e766b-134">一般來說，您會想要針對序列化的物件停用消極式載入。</span><span class="sxs-lookup"><span data-stu-id="e766b-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="e766b-135">序列化程式必須讀取模型上的所有屬性，以觸發載入相關實體。</span><span class="sxs-lookup"><span data-stu-id="e766b-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="e766b-136">例如，當 EF 將已啟用消極式載入的書籍清單序列化時，以下是 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="e766b-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="e766b-137">您可以看到 EF 針對三個作者進行三個不同的查詢。</span><span class="sxs-lookup"><span data-stu-id="e766b-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="e766b-138">有時候，您可能會想要使用消極式載入。</span><span class="sxs-lookup"><span data-stu-id="e766b-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="e766b-139">積極式載入可能會導致 EF 產生非常複雜的聯結。</span><span class="sxs-lookup"><span data-stu-id="e766b-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="e766b-140">或者，您可能需要一小部分資料的相關實體，而消極式載入會更有效率。</span><span class="sxs-lookup"><span data-stu-id="e766b-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="e766b-141">避免序列化問題的其中一種方法是序列化資料傳輸物件（Dto），而不是實體物件。</span><span class="sxs-lookup"><span data-stu-id="e766b-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="e766b-142">我稍後會在本文中說明這個方法。</span><span class="sxs-lookup"><span data-stu-id="e766b-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="e766b-143">明確式載入</span><span class="sxs-lookup"><span data-stu-id="e766b-143">Explicit Loading</span></span>

<span data-ttu-id="e766b-144">明確載入類似于消極式載入，不同之處在于您明確地取得程式碼中的相關資料。當您存取導覽屬性時，不會自動進行此動作。</span><span class="sxs-lookup"><span data-stu-id="e766b-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="e766b-145">明確的載入可讓您更充分掌控載入相關資料的時間，但需要額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e766b-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="e766b-146">如需明確載入的詳細資訊，請參閱[載入相關實體](https://msdn.microsoft.com/data/jj574232#explicit)。</span><span class="sxs-lookup"><span data-stu-id="e766b-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="e766b-147">導覽屬性和迴圈參考</span><span class="sxs-lookup"><span data-stu-id="e766b-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="e766b-148">當我定義書籍和作者模型時，我在 [書籍-作者] 關聯性的 [`Book`] 類別上定義了一個導覽屬性，但是我並未定義另一個方向的導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="e766b-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="e766b-149">如果您將對應的導覽屬性加入 `Author` 類別中，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="e766b-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="e766b-150">可惜的是，當您將模型序列化時，這會造成問題。</span><span class="sxs-lookup"><span data-stu-id="e766b-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="e766b-151">如果您載入相關的資料，它會建立迴圈物件圖形。</span><span class="sxs-lookup"><span data-stu-id="e766b-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="e766b-152">當 JSON 或 XML 格式器嘗試將圖形序列化時，它會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e766b-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="e766b-153">這兩個格式子會擲回不同的例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="e766b-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="e766b-154">以下是 JSON 格式器的範例：</span><span class="sxs-lookup"><span data-stu-id="e766b-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="e766b-155">以下是 XML 格式器：</span><span class="sxs-lookup"><span data-stu-id="e766b-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="e766b-156">其中一個解決方法是使用 Dto，我在下一節中說明。</span><span class="sxs-lookup"><span data-stu-id="e766b-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="e766b-157">或者，您可以設定 JSON 和 XML 格式器來處理圖形週期。</span><span class="sxs-lookup"><span data-stu-id="e766b-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="e766b-158">如需詳細資訊，請參閱[處理迴圈物件參考](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。</span><span class="sxs-lookup"><span data-stu-id="e766b-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="e766b-159">在本教學課程中，您不需要 `Author.Book` 導覽屬性，因此您可以將其省略。</span><span class="sxs-lookup"><span data-stu-id="e766b-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e766b-160">[上一頁](part-3.md)
> [下一頁](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="e766b-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
