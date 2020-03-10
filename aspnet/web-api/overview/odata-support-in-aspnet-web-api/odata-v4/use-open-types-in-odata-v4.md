---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: 在具有 ASP.NET Web API 的 OData v4 中開啟類型 |Microsoft Docs
author: microsoft
description: 在 OData v4 中，開放式型別是包含動態屬性的結構化型別，以及在型別定義中宣告的任何屬性。 開啟...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622175"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="04e35-104">使用 ASP.NET Web API 在 OData v4 中開啟類型</span><span class="sxs-lookup"><span data-stu-id="04e35-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="04e35-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="04e35-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="04e35-106">在 OData v4 中，*開放式型*別是包含動態屬性的結構化型別，以及在型別定義中宣告的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="04e35-107">開放式類型可讓您為資料模型增加彈性。</span><span class="sxs-lookup"><span data-stu-id="04e35-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="04e35-108">本教學課程說明如何在 ASP.NET Web API OData 中使用開放式型別。</span><span class="sxs-lookup"><span data-stu-id="04e35-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="04e35-109">本教學課程假設您已經知道如何在 ASP.NET Web API 中建立 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="04e35-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="04e35-110">如果不是，請先閱讀[建立 OData V4 端點](create-an-odata-v4-endpoint.md)一開始。</span><span class="sxs-lookup"><span data-stu-id="04e35-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="04e35-111">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="04e35-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="04e35-112">Web API OData 5。3</span><span class="sxs-lookup"><span data-stu-id="04e35-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="04e35-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="04e35-113">OData v4</span></span>

<span data-ttu-id="04e35-114">首先，有些 OData 術語：</span><span class="sxs-lookup"><span data-stu-id="04e35-114">First, some OData terminology:</span></span>

- <span data-ttu-id="04e35-115">實體類型：具有索引鍵的結構化類型。</span><span class="sxs-lookup"><span data-stu-id="04e35-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="04e35-116">複雜型別：不含索引鍵的結構化型別。</span><span class="sxs-lookup"><span data-stu-id="04e35-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="04e35-117">開啟類型：具有動態屬性的類型。</span><span class="sxs-lookup"><span data-stu-id="04e35-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="04e35-118">實體類型和複雜類型都可以開啟。</span><span class="sxs-lookup"><span data-stu-id="04e35-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="04e35-119">動態屬性的值可以是基本類型、複雜類型或列舉類型;或其中任何一種類型的集合。</span><span class="sxs-lookup"><span data-stu-id="04e35-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="04e35-120">如需有關開放式類型的詳細資訊，請參閱[OData v4 規格](http://www.odata.org/documentation/odata-version-4-0/)。</span><span class="sxs-lookup"><span data-stu-id="04e35-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="04e35-121">安裝 Web OData 程式庫</span><span class="sxs-lookup"><span data-stu-id="04e35-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="04e35-122">使用 NuGet 套件管理員來安裝最新的 Web API OData 程式庫。</span><span class="sxs-lookup"><span data-stu-id="04e35-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="04e35-123">從 [套件管理員主控台] 視窗：</span><span class="sxs-lookup"><span data-stu-id="04e35-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="04e35-124">定義 CLR 類型</span><span class="sxs-lookup"><span data-stu-id="04e35-124">Define the CLR Types</span></span>

<span data-ttu-id="04e35-125">首先，將 EDM 模型定義為 CLR 類型。</span><span class="sxs-lookup"><span data-stu-id="04e35-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="04e35-126">建立實體資料模型（EDM）時，</span><span class="sxs-lookup"><span data-stu-id="04e35-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="04e35-127">`Category` 是列舉型別。</span><span class="sxs-lookup"><span data-stu-id="04e35-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="04e35-128">`Address` 是複雜型別。</span><span class="sxs-lookup"><span data-stu-id="04e35-128">`Address` is a complex type.</span></span> <span data-ttu-id="04e35-129">（它沒有索引鍵，因此它不是實體類型）。</span><span class="sxs-lookup"><span data-stu-id="04e35-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="04e35-130">`Customer` 是實體類型。</span><span class="sxs-lookup"><span data-stu-id="04e35-130">`Customer` is an entity type.</span></span> <span data-ttu-id="04e35-131">（它有一個金鑰）。</span><span class="sxs-lookup"><span data-stu-id="04e35-131">(It has a key.)</span></span>
- <span data-ttu-id="04e35-132">`Press` 是開放式複雜型別。</span><span class="sxs-lookup"><span data-stu-id="04e35-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="04e35-133">`Book` 是開放式實體類型。</span><span class="sxs-lookup"><span data-stu-id="04e35-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="04e35-134">若要建立開放式型別，CLR 型別必須有一個型別為 `IDictionary<string, object>`的屬性，它會保存動態屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="04e35-135">建立 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="04e35-135">Build the EDM Model</span></span>

<span data-ttu-id="04e35-136">如果您使用**ODataConventionModelBuilder**來建立 EDM，`Press` 和 `Book` 會根據 `IDictionary<string, object>` 屬性是否存在，自動加入為開啟的類型。</span><span class="sxs-lookup"><span data-stu-id="04e35-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="04e35-137">您也可以使用**用**，明確地建立 EDM。</span><span class="sxs-lookup"><span data-stu-id="04e35-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="04e35-138">新增 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="04e35-138">Add an OData Controller</span></span>

<span data-ttu-id="04e35-139">接下來，新增 OData 控制器。</span><span class="sxs-lookup"><span data-stu-id="04e35-139">Next, add an OData controller.</span></span> <span data-ttu-id="04e35-140">在本教學課程中，我們將使用簡單的控制器，只支援 GET 和 POST 要求，並使用記憶體中的清單來儲存實體。</span><span class="sxs-lookup"><span data-stu-id="04e35-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="04e35-141">請注意，第一個 `Book` 實例沒有動態屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="04e35-142">第二個 `Book` 實例具有下列動態屬性：</span><span class="sxs-lookup"><span data-stu-id="04e35-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="04e35-143">「已發行」：基本類型</span><span class="sxs-lookup"><span data-stu-id="04e35-143">"Published": Primitive type</span></span>
- <span data-ttu-id="04e35-144">「作者」：基本類型的集合</span><span class="sxs-lookup"><span data-stu-id="04e35-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="04e35-145">"OtherCategories"：列舉類型的集合。</span><span class="sxs-lookup"><span data-stu-id="04e35-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="04e35-146">此外，該 `Book` 實例的 `Press` 屬性具有下列動態屬性：</span><span class="sxs-lookup"><span data-stu-id="04e35-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="04e35-147">「Blog」：基本類型</span><span class="sxs-lookup"><span data-stu-id="04e35-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="04e35-148">"Address"：複雜類型</span><span class="sxs-lookup"><span data-stu-id="04e35-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="04e35-149">查詢中繼資料</span><span class="sxs-lookup"><span data-stu-id="04e35-149">Query the Metadata</span></span>

<span data-ttu-id="04e35-150">若要取得 OData 元資料檔案，請將 GET 要求傳送至 `~/$metadata`。</span><span class="sxs-lookup"><span data-stu-id="04e35-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="04e35-151">回應主體看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="04e35-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="04e35-152">在元資料檔案中，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="04e35-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="04e35-153">針對 `Book` 和 `Press` 類型，`OpenType` 屬性的值為 true。</span><span class="sxs-lookup"><span data-stu-id="04e35-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="04e35-154">`Customer` 和 `Address` 類型沒有此屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="04e35-155">`Book` 實體類型有三個宣告的屬性： ISBN、Title 和按下。</span><span class="sxs-lookup"><span data-stu-id="04e35-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="04e35-156">OData 中繼資料不包含來自 CLR 類別的 `Book.Properties` 屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="04e35-157">同樣地，`Press` 複雜型別只有兩個宣告的屬性： Name 和 Category。</span><span class="sxs-lookup"><span data-stu-id="04e35-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="04e35-158">中繼資料不包含來自 CLR 類別的 `Press.DynamicProperties` 屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="04e35-159">查詢實體</span><span class="sxs-lookup"><span data-stu-id="04e35-159">Query an Entity</span></span>

<span data-ttu-id="04e35-160">若要取得具有等於 "978-0-7356-7942-9" 之 ISBN 的書籍，請將 GET 要求傳送至 `~/Books('978-0-7356-7942-9')`。</span><span class="sxs-lookup"><span data-stu-id="04e35-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="04e35-161">回應主體看起來應該如下所示。</span><span class="sxs-lookup"><span data-stu-id="04e35-161">The response body should look similar to the following.</span></span> <span data-ttu-id="04e35-162">（縮排，使其更容易閱讀）。</span><span class="sxs-lookup"><span data-stu-id="04e35-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="04e35-163">請注意，動態屬性會包含在已宣告屬性的內嵌中。</span><span class="sxs-lookup"><span data-stu-id="04e35-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="04e35-164">張貼實體</span><span class="sxs-lookup"><span data-stu-id="04e35-164">POST an Entity</span></span>

<span data-ttu-id="04e35-165">若要新增書籍實體，請將 POST 要求傳送至 `~/Books`。</span><span class="sxs-lookup"><span data-stu-id="04e35-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="04e35-166">用戶端可以在要求承載中設定動態屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="04e35-167">以下是範例要求。</span><span class="sxs-lookup"><span data-stu-id="04e35-167">Here is an example request.</span></span> <span data-ttu-id="04e35-168">請注意「價格」和「已發佈」屬性。</span><span class="sxs-lookup"><span data-stu-id="04e35-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="04e35-169">如果您在控制器方法中設定中斷點，您可以看到 Web API 已將這些屬性新增至 `Properties` 字典。</span><span class="sxs-lookup"><span data-stu-id="04e35-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="04e35-170">其他資源</span><span class="sxs-lookup"><span data-stu-id="04e35-170">Additional Resources</span></span>

[<span data-ttu-id="04e35-171">OData 開啟類型範例</span><span class="sxs-lookup"><span data-stu-id="04e35-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
