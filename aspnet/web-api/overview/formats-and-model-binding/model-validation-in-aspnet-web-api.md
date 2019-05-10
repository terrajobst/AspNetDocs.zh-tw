---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: 模型驗證，在 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: 概觀的 ASP.NET Web API 中的模型驗證，asp.net 4.x。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112834"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="b36d9-103">ASP.NET Web API 中的模型驗證</span><span class="sxs-lookup"><span data-stu-id="b36d9-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="b36d9-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b36d9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b36d9-105">本文說明如何將模型加上註解、 使用註解進行資料驗證和處理您的 web API 中的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="b36d9-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="b36d9-106">當用戶端會將資料傳送至您的 web API 時，通常您想要驗證資料再進行任何處理。</span><span class="sxs-lookup"><span data-stu-id="b36d9-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="b36d9-107">資料註釋</span><span class="sxs-lookup"><span data-stu-id="b36d9-107">Data Annotations</span></span>

<span data-ttu-id="b36d9-108">在 ASP.NET Web API 中，您可以使用中的屬性[System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)在模型上設定屬性的驗證規則的命名空間。</span><span class="sxs-lookup"><span data-stu-id="b36d9-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="b36d9-109">請考慮下列模型：</span><span class="sxs-lookup"><span data-stu-id="b36d9-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="b36d9-110">如果您已在 ASP.NET MVC 中使用模型驗證，這應該看起來很熟悉。</span><span class="sxs-lookup"><span data-stu-id="b36d9-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="b36d9-111">**所需**屬性指出`Name`屬性不得為 null。</span><span class="sxs-lookup"><span data-stu-id="b36d9-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="b36d9-112">**範圍**屬性指出`Weight`必須是介於 0 到 999 之間。</span><span class="sxs-lookup"><span data-stu-id="b36d9-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="b36d9-113">假設用戶端傳送 POST 要求，使用下列的 JSON 表示法：</span><span class="sxs-lookup"><span data-stu-id="b36d9-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="b36d9-114">您可以看到用戶端未包含`Name`屬性，它會標示為必要。</span><span class="sxs-lookup"><span data-stu-id="b36d9-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="b36d9-115">當 Web API 會將轉換成 JSON`Product`執行個體，它會驗證`Product`針對驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="b36d9-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="b36d9-116">在控制器動作中，您可以檢查模型是否有效：</span><span class="sxs-lookup"><span data-stu-id="b36d9-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="b36d9-117">模型驗證並不保證用戶端的資料安全無虞。</span><span class="sxs-lookup"><span data-stu-id="b36d9-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="b36d9-118">在應用程式的其他層級，可能會需要額外的驗證。</span><span class="sxs-lookup"><span data-stu-id="b36d9-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="b36d9-119">（例如，資料層可能會強制執行 foreign key 條件約束。）本教學課程[使用 Web API 和 Entity Framework](../data/using-web-api-with-entity-framework/part-1.md)探討其中一些問題。</span><span class="sxs-lookup"><span data-stu-id="b36d9-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="b36d9-120">**「 不足公佈 」**:當用戶端將被排除某些屬性，則會發生不足張貼。</span><span class="sxs-lookup"><span data-stu-id="b36d9-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="b36d9-121">例如，假設用戶端會傳送下列：</span><span class="sxs-lookup"><span data-stu-id="b36d9-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="b36d9-122">在這裡，用戶端未指定值`Price`或`Weight`。</span><span class="sxs-lookup"><span data-stu-id="b36d9-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="b36d9-123">JSON 格式器指派的預設值為 0 時可遺漏的屬性。</span><span class="sxs-lookup"><span data-stu-id="b36d9-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="b36d9-124">模型狀態無效，因為 0 是有效的值，這些屬性。</span><span class="sxs-lookup"><span data-stu-id="b36d9-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="b36d9-125">是否為問題取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="b36d9-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="b36d9-126">比方說，在更新作業中，您可能想要區別 「 零 」 和 「 未設定 」。</span><span class="sxs-lookup"><span data-stu-id="b36d9-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="b36d9-127">若要強制用戶端設定值，將屬性設為可為 null 和 set**需要**屬性：</span><span class="sxs-lookup"><span data-stu-id="b36d9-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="b36d9-128">**「 過度發佈"**:用戶端也可以傳送*更多*比您預期的資料。</span><span class="sxs-lookup"><span data-stu-id="b36d9-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="b36d9-129">例如: </span><span class="sxs-lookup"><span data-stu-id="b36d9-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="b36d9-130">JSON，包含屬性 （[色彩]），不存在於`Product`模型。</span><span class="sxs-lookup"><span data-stu-id="b36d9-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="b36d9-131">在此情況下，JSON 格式器只會忽略此值。</span><span class="sxs-lookup"><span data-stu-id="b36d9-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="b36d9-132">（XML 格式器執行相同作業。）如果您的模型有您想要處於唯讀模式的屬性，過度發佈就會造成問題。</span><span class="sxs-lookup"><span data-stu-id="b36d9-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="b36d9-133">例如：</span><span class="sxs-lookup"><span data-stu-id="b36d9-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="b36d9-134">您不希望使用者更新`IsAdmin`屬性並將自己提升至系統管理員 ！</span><span class="sxs-lookup"><span data-stu-id="b36d9-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="b36d9-135">最安全的策略是使用完全符合 用戶端允許傳送的模型類別：</span><span class="sxs-lookup"><span data-stu-id="b36d9-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="b36d9-136">Brad Wilson 的部落格文章"[驗證輸入 vs。ASP.NET MVC 中的模型驗證](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)「 有不足張貼和 over-posting 棒的探討。</span><span class="sxs-lookup"><span data-stu-id="b36d9-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="b36d9-137">雖然文章是關於 ASP.NET MVC 2，問題是與 Web API 仍然相關。</span><span class="sxs-lookup"><span data-stu-id="b36d9-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>

## <a name="handling-validation-errors"></a><span data-ttu-id="b36d9-138">處理驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="b36d9-138">Handling Validation Errors</span></span>

<span data-ttu-id="b36d9-139">Web API 不會自動傳回錯誤給用戶端驗證失敗時。</span><span class="sxs-lookup"><span data-stu-id="b36d9-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="b36d9-140">負責檢查模型狀態，並適當地回應的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="b36d9-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="b36d9-141">您也可以建立動作篩選條件在叫用控制器動作之前，檢查模型狀態。</span><span class="sxs-lookup"><span data-stu-id="b36d9-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="b36d9-142">下列程式碼顯示範例：</span><span class="sxs-lookup"><span data-stu-id="b36d9-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="b36d9-143">如果模型驗證失敗，此篩選器就會傳回 HTTP 回應，其中包含驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="b36d9-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="b36d9-144">在此情況下，不會叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="b36d9-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="b36d9-145">若要將此篩選套用至所有的 Web API 控制器，將新增的篩選，以執行個體**HttpConfiguration.Filters**設定期間的集合：</span><span class="sxs-lookup"><span data-stu-id="b36d9-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="b36d9-146">另一個選項是設定為屬性的篩選器，在個別的控制器或控制器動作：</span><span class="sxs-lookup"><span data-stu-id="b36d9-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
