---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 的安全性指導方針 2 OData-ASP.NET 4。x
author: MikeWasson
description: 說明在 ASP.NET 4.x 上透過 OData 針對 ASP.NET Web API 2 公開資料集時要考慮的安全性問題。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556494"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="a2e91-103">ASP.NET Web API 2 OData 的安全性指引</span><span class="sxs-lookup"><span data-stu-id="a2e91-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="a2e91-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a2e91-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a2e91-105">本主題說明在 ASP.NET 4.x 上透過 OData 針對 ASP.NET Web API 2 公開資料集時，您應該考慮的一些安全性問題。</span><span class="sxs-lookup"><span data-stu-id="a2e91-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="a2e91-106">EDM 安全性</span><span class="sxs-lookup"><span data-stu-id="a2e91-106">EDM Security</span></span>

<span data-ttu-id="a2e91-107">查詢的語義是以 entity data model （EDM）為基礎，而不是基礎模型類型。</span><span class="sxs-lookup"><span data-stu-id="a2e91-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="a2e91-108">您可以從 EDM 排除屬性，查詢看不到它。</span><span class="sxs-lookup"><span data-stu-id="a2e91-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="a2e91-109">例如，假設您的模型包含具有薪資屬性的員工類型。</span><span class="sxs-lookup"><span data-stu-id="a2e91-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="a2e91-110">您可能想要從 EDM 排除此屬性，以將它從用戶端隱藏。</span><span class="sxs-lookup"><span data-stu-id="a2e91-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="a2e91-111">有兩種方式可從 EDM 中排除屬性。</span><span class="sxs-lookup"><span data-stu-id="a2e91-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="a2e91-112">您可以在模型類別中的屬性上設定 **[IgnoreDataMember]** 屬性：</span><span class="sxs-lookup"><span data-stu-id="a2e91-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="a2e91-113">您也可以透過程式設計方式從 EDM 移除屬性：</span><span class="sxs-lookup"><span data-stu-id="a2e91-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="a2e91-114">查詢安全性</span><span class="sxs-lookup"><span data-stu-id="a2e91-114">Query Security</span></span>

<span data-ttu-id="a2e91-115">惡意或簡單的用戶端可能會建立花費很長時間執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="a2e91-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="a2e91-116">在最糟的情況下，這可能會干擾您的服務存取。</span><span class="sxs-lookup"><span data-stu-id="a2e91-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="a2e91-117">**[可查詢]** 屬性是用來剖析、驗證及套用查詢的動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="a2e91-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="a2e91-118">篩選準則會將查詢選項轉換成 LINQ 運算式。</span><span class="sxs-lookup"><span data-stu-id="a2e91-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="a2e91-119">當 OData 控制器傳回**iqueryable**類型時， **iqueryable** linq 提供者會將 linq 運算式轉換成查詢。</span><span class="sxs-lookup"><span data-stu-id="a2e91-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="a2e91-120">因此，效能取決於所使用的 LINQ 提供者，以及您的資料集或資料庫架構的特定特性。</span><span class="sxs-lookup"><span data-stu-id="a2e91-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="a2e91-121">如需在 ASP.NET Web API 中使用 OData 查詢選項的詳細資訊，請參閱[支援 OData 查詢選項](supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="a2e91-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="a2e91-122">如果您知道所有用戶端都是受信任的（例如，在企業環境中），或如果您的資料集很小，則查詢效能可能不會有問題。</span><span class="sxs-lookup"><span data-stu-id="a2e91-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="a2e91-123">否則，您應該考慮下列建議。</span><span class="sxs-lookup"><span data-stu-id="a2e91-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="a2e91-124">使用各種查詢來測試您的服務，並分析資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2e91-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="a2e91-125">啟用伺服器導向的分頁，以避免在單一查詢中傳回大型資料集。</span><span class="sxs-lookup"><span data-stu-id="a2e91-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="a2e91-126">如需詳細資訊，請參閱[伺服器導向的分頁](supporting-odata-query-options.md#server-paging)。</span><span class="sxs-lookup"><span data-stu-id="a2e91-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="a2e91-127">您需要 $filter 和 $orderby 嗎？</span><span class="sxs-lookup"><span data-stu-id="a2e91-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="a2e91-128">某些應用程式可能會允許用戶端分頁，使用 $top 和 $skip，但停用其他查詢選項。</span><span class="sxs-lookup"><span data-stu-id="a2e91-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="a2e91-129">請考慮將 $orderby 限制為叢集索引中的屬性。</span><span class="sxs-lookup"><span data-stu-id="a2e91-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="a2e91-130">在沒有叢集索引的情況下排序大型資料會變慢。</span><span class="sxs-lookup"><span data-stu-id="a2e91-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="a2e91-131">節點計數上限： **[可查詢]** 上的**MaxNodeCount**屬性會設定 $filter 語法樹狀結構中所允許的最大節點數目。</span><span class="sxs-lookup"><span data-stu-id="a2e91-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="a2e91-132">預設值為100，但您可能會想要設定較低的值，因為編譯的節點可能會變得很慢。</span><span class="sxs-lookup"><span data-stu-id="a2e91-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="a2e91-133">如果您使用 LINQ to Objects （也就是在記憶體中的集合上執行 LINQ 查詢，而不使用中繼的 LINQ 提供者），這特別適用。</span><span class="sxs-lookup"><span data-stu-id="a2e91-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="a2e91-134">請考慮停用 any （）和 all （）函式，因為這些函式可能會變慢。</span><span class="sxs-lookup"><span data-stu-id="a2e91-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="a2e91-135">如有任何字串屬性包含大型&#8212;字串（例如，產品描述或 blog 專案&#8212;），請考慮停用字串函數。</span><span class="sxs-lookup"><span data-stu-id="a2e91-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="a2e91-136">考慮禁止篩選導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="a2e91-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="a2e91-137">根據您的資料庫架構而定，篩選導覽屬性可能會導致聯結，這可能會很慢。</span><span class="sxs-lookup"><span data-stu-id="a2e91-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="a2e91-138">下列程式碼顯示可防止篩選導覽屬性的查詢驗證程式。</span><span class="sxs-lookup"><span data-stu-id="a2e91-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="a2e91-139">如需查詢驗證程式的詳細資訊，請參閱[查詢驗證](supporting-odata-query-options.md#query-validation)。</span><span class="sxs-lookup"><span data-stu-id="a2e91-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="a2e91-140">請考慮撰寫針對您的資料庫自訂的驗證程式，以限制 $filter 查詢。</span><span class="sxs-lookup"><span data-stu-id="a2e91-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="a2e91-141">例如，請考慮下列兩個查詢：</span><span class="sxs-lookup"><span data-stu-id="a2e91-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="a2e91-142">具有姓氏開頭為 ' A ' 之動作專案的所有電影。</span><span class="sxs-lookup"><span data-stu-id="a2e91-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="a2e91-143">1994中發行的所有電影。</span><span class="sxs-lookup"><span data-stu-id="a2e91-143">All movies released in 1994.</span></span>

    <span data-ttu-id="a2e91-144">除非電影是由動作專案編制索引，否則第一個查詢可能需要資料庫引擎掃描整個電影清單。</span><span class="sxs-lookup"><span data-stu-id="a2e91-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="a2e91-145">雖然第二個查詢可能是可接受的，但假設電影是以發行年份進行編制索引。</span><span class="sxs-lookup"><span data-stu-id="a2e91-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="a2e91-146">下列程式碼顯示允許篩選 "ReleaseYear" 和 "Title" 屬性，但沒有其他屬性的驗證器。</span><span class="sxs-lookup"><span data-stu-id="a2e91-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="a2e91-147">一般來說，請考慮您需要的 $filter 功能。</span><span class="sxs-lookup"><span data-stu-id="a2e91-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="a2e91-148">如果您的用戶端不需要 $filter 的完整表達，您可以限制允許的功能。</span><span class="sxs-lookup"><span data-stu-id="a2e91-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
