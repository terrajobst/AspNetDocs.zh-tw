---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: 使用 Web API 2.2 在 OData v4 中建立單一實例 |Microsoft Docs
author: rick-anderson
description: 本主題說明如何在 Web API 2.2 的 OData 端點中定義 singleton。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622084"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="7e915-103">使用 Web API 2.2 在 OData v4 中建立單一</span><span class="sxs-lookup"><span data-stu-id="7e915-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="7e915-104">依 Zoe 羅文</span><span class="sxs-lookup"><span data-stu-id="7e915-104">by Zoe Luo</span></span>

> <span data-ttu-id="7e915-105">傳統上，只有當實體封裝于實體集內時，才可以存取它。</span><span class="sxs-lookup"><span data-stu-id="7e915-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="7e915-106">但是 OData v4 提供兩個額外的選項，即 Singleton 和內含專案，兩者都是 WebAPI 2.2 支援的。</span><span class="sxs-lookup"><span data-stu-id="7e915-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="7e915-107">本文說明如何在 Web API 2.2 的 OData 端點中定義單一專案。</span><span class="sxs-lookup"><span data-stu-id="7e915-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="7e915-108">如需單一專案是什麼，以及如何受益于它的詳細資訊，請參閱[使用單一專案來定義您的特殊實體](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7e915-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="7e915-109">若要在 Web API 中建立 OData V4 端點，請參閱[使用 ASP.NET Web API 2.2 建立 odata V4 端點](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="7e915-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="7e915-110">我們會使用下列資料模型，在您的 Web API 專案中建立 singleton：</span><span class="sxs-lookup"><span data-stu-id="7e915-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![資料模型](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="7e915-112">將根據型別 `Company`定義名為 `Umbrella` 的 singleton，並根據型別 `Employee`定義名為 `Employees` 的實體集。</span><span class="sxs-lookup"><span data-stu-id="7e915-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="7e915-113">本教學課程中使用的解決方案可以從[CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)下載。</span><span class="sxs-lookup"><span data-stu-id="7e915-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="7e915-114">定義資料模型</span><span class="sxs-lookup"><span data-stu-id="7e915-114">Define the data model</span></span>

1. <span data-ttu-id="7e915-115">定義 CLR 類型。</span><span class="sxs-lookup"><span data-stu-id="7e915-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="7e915-116">根據 CLR 類型產生 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="7e915-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="7e915-117">在這裡，`builder.Singleton<Company>("Umbrella")` 會告知模型產生器在 EDM 模型中建立名為 `Umbrella` 的 singleton。</span><span class="sxs-lookup"><span data-stu-id="7e915-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="7e915-118">產生的中繼資料看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="7e915-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="7e915-119">在中繼資料中，我們可以看到 `Employees` 實體集中 `Company` 的導覽屬性已系結至單一 `Umbrella`。</span><span class="sxs-lookup"><span data-stu-id="7e915-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="7e915-120">系結是由 `ODataConventionModelBuilder`自動完成，因為只有 `Umbrella` 具有 `Company` 類型。</span><span class="sxs-lookup"><span data-stu-id="7e915-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="7e915-121">如果模型中有任何不明確的情況，您可以使用 `HasSingletonBinding` 明確地將導覽屬性系結至 singleton;`HasSingletonBinding` 與在 CLR 型別定義中使用 `Singleton` 屬性具有相同的效果：</span><span class="sxs-lookup"><span data-stu-id="7e915-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="7e915-122">定義單一控制器</span><span class="sxs-lookup"><span data-stu-id="7e915-122">Define the singleton controller</span></span>

<span data-ttu-id="7e915-123">如同 EntitySet 控制器，單一控制器會繼承自 `ODataController`，而單一控制器名稱應該是 `[singletonName]Controller`。</span><span class="sxs-lookup"><span data-stu-id="7e915-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="7e915-124">為了處理不同類型的要求，必須在控制器中預先定義動作。</span><span class="sxs-lookup"><span data-stu-id="7e915-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="7e915-125">預設會在 WebApi 2.2 中啟用**屬性路由**。</span><span class="sxs-lookup"><span data-stu-id="7e915-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="7e915-126">例如，若要定義動作，以使用屬性路由從 `Company` 處理查詢 `Revenue`，請使用下列程式：</span><span class="sxs-lookup"><span data-stu-id="7e915-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="7e915-127">如果您不願意定義每個動作的屬性，只需定義遵循[OData 路由慣例](../odata-routing-conventions.md)的動作即可。</span><span class="sxs-lookup"><span data-stu-id="7e915-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="7e915-128">由於查詢 singleton 不需要索引鍵，因此在單一控制器中定義的動作與 entityset 控制器中定義的動作有些微不同。</span><span class="sxs-lookup"><span data-stu-id="7e915-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="7e915-129">如需參考，單一控制器中每個動作定義的方法簽章如下所示。</span><span class="sxs-lookup"><span data-stu-id="7e915-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="7e915-130">基本上，這就是您在服務端必須執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="7e915-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="7e915-131">[範例專案](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)包含方案的所有程式碼，以及顯示如何使用 Singleton 的 OData 用戶端。</span><span class="sxs-lookup"><span data-stu-id="7e915-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="7e915-132">用戶端會遵循[建立 OData V4 用戶端應用程式](create-an-odata-v4-client-app.md)中的步驟來建立。</span><span class="sxs-lookup"><span data-stu-id="7e915-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="7e915-133">。</span><span class="sxs-lookup"><span data-stu-id="7e915-133">.</span></span> 

<span data-ttu-id="7e915-134">*感謝 Leo Hu 這篇文章的原始內容。*</span><span class="sxs-lookup"><span data-stu-id="7e915-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
