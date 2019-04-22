---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: 使用 ASP.NET Web API OData v4 中的複雜類型繼承 |Microsoft Docs
author: microsoft
description: 根據 OData v4 規格中，複雜型別可以繼承自另一個複雜類型。 （複雜型別是結構化的型別沒有索引鍵）。Web API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 76db6325b8528af5b82ca3ea4e34284ca470ff6e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59378590"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="fa888-104">使用 ASP.NET Web API OData v4 中的複雜類型繼承</span><span class="sxs-lookup"><span data-stu-id="fa888-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="fa888-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fa888-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fa888-106">根據 OData v4[規格](http://www.odata.org/documentation/odata-version-4-0/)，複雜型別可以繼承自另一個複雜類型。</span><span class="sxs-lookup"><span data-stu-id="fa888-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="fa888-107">(A*複雜*型別是結構化的型別沒有索引鍵。)Web API OData 5.3 支援複雜類型繼承。</span><span class="sxs-lookup"><span data-stu-id="fa888-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="fa888-108">本主題說明如何建置具有複雜繼承類型的實體資料模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="fa888-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="fa888-109">如需完整的原始程式碼，請參閱[OData 複雜類型繼承範例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="fa888-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fa888-110">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="fa888-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fa888-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="fa888-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="fa888-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="fa888-112">OData v4</span></span>


## <a name="model-hierarchy"></a><span data-ttu-id="fa888-113">模型階層</span><span class="sxs-lookup"><span data-stu-id="fa888-113">Model Hierarchy</span></span>

<span data-ttu-id="fa888-114">為了說明複雜類型繼承，我們將使用下列的類別階層架構。</span><span class="sxs-lookup"><span data-stu-id="fa888-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="fa888-115">`Shape` 是抽象的複雜類型。</span><span class="sxs-lookup"><span data-stu-id="fa888-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="fa888-116">`Rectangle``Triangle`，並`Circle`複雜型別衍生自`Shape`，以及`RoundRectangle`衍生自`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="fa888-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="fa888-117">`Window` 是實體類型，包含`Shape`執行個體。</span><span class="sxs-lookup"><span data-stu-id="fa888-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="fa888-118">以下是定義這些類型的 CLR 類別。</span><span class="sxs-lookup"><span data-stu-id="fa888-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="fa888-119">建置的 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="fa888-119">Build the EDM Model</span></span>

<span data-ttu-id="fa888-120">若要建立 EDM 中，您可以使用**ODataConventionModelBuilder**，這會推斷從 CLR 類型的繼承關聯性。</span><span class="sxs-lookup"><span data-stu-id="fa888-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="fa888-121">您也可以建置 EDM 明確地使用**ODataModelBuilder**。</span><span class="sxs-lookup"><span data-stu-id="fa888-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="fa888-122">這會讓更多的程式碼，但可讓您更充分掌控 EDM。</span><span class="sxs-lookup"><span data-stu-id="fa888-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="fa888-123">這兩個範例會建立相同的 EDM 結構描述。</span><span class="sxs-lookup"><span data-stu-id="fa888-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="fa888-124">中繼資料文件</span><span class="sxs-lookup"><span data-stu-id="fa888-124">Metadata Document</span></span>

<span data-ttu-id="fa888-125">以下是 OData 中繼資料顯示的文件，複雜類型繼承。</span><span class="sxs-lookup"><span data-stu-id="fa888-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="fa888-126">中繼資料文件中，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="fa888-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="fa888-127">`Shape`複雜型別為抽象。</span><span class="sxs-lookup"><span data-stu-id="fa888-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="fa888-128">`Rectangle`， `Triangle`，並`Circle`複雜類型具有基底型別`Shape`。</span><span class="sxs-lookup"><span data-stu-id="fa888-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="fa888-129">`RoundRectangle`類型具有基底類型`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="fa888-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="fa888-130">將複雜型別轉型</span><span class="sxs-lookup"><span data-stu-id="fa888-130">Casting Complex Types</span></span>

<span data-ttu-id="fa888-131">現在支援上的複雜型別進行轉換。</span><span class="sxs-lookup"><span data-stu-id="fa888-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="fa888-132">例如，下列查詢會轉換`Shape`至`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="fa888-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="fa888-133">以下是回應承載：</span><span class="sxs-lookup"><span data-stu-id="fa888-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
