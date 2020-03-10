---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API 中的模型驗證-ASP.NET 4。x
author: MikeWasson
description: ASP.NET 4.x 的 ASP.NET Web API 中的模型驗證總覽。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557236"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="25064-103">ASP.NET Web API 中的模型驗證</span><span class="sxs-lookup"><span data-stu-id="25064-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="25064-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="25064-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="25064-105">本文說明如何標注模型、使用批註進行資料驗證，以及處理 Web API 中的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="25064-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="25064-106">當用戶端將資料傳送至您的 Web API 時，您通常會想要先驗證資料，然後再進行任何處理。</span><span class="sxs-lookup"><span data-stu-id="25064-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="25064-107">資料註釋</span><span class="sxs-lookup"><span data-stu-id="25064-107">Data Annotations</span></span>

<span data-ttu-id="25064-108">在 ASP.NET Web API 中，您可以使用[system.workflow.componentmodel.activity. DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空間中的屬性，為模型上的屬性設定驗證規則。</span><span class="sxs-lookup"><span data-stu-id="25064-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="25064-109">請考慮下列模型：</span><span class="sxs-lookup"><span data-stu-id="25064-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="25064-110">如果您已在 ASP.NET MVC 中使用模型驗證，這看起來應該很熟悉。</span><span class="sxs-lookup"><span data-stu-id="25064-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="25064-111">**必要**的屬性指出 `Name` 屬性不得為 null。</span><span class="sxs-lookup"><span data-stu-id="25064-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="25064-112">**範圍**屬性指出 `Weight` 必須介於0到999之間。</span><span class="sxs-lookup"><span data-stu-id="25064-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="25064-113">假設用戶端傳送具有下列 JSON 標記法的 POST 要求：</span><span class="sxs-lookup"><span data-stu-id="25064-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="25064-114">您可以看到用戶端並未包含 [`Name`] 屬性，這會標示為 [必要]。</span><span class="sxs-lookup"><span data-stu-id="25064-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="25064-115">當 Web API 將 JSON 轉換成 `Product` 實例時，它會根據驗證屬性來驗證 `Product`。</span><span class="sxs-lookup"><span data-stu-id="25064-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="25064-116">在您的控制器動作中，您可以檢查模型是否有效：</span><span class="sxs-lookup"><span data-stu-id="25064-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="25064-117">模型驗證不保證用戶端資料是安全的。</span><span class="sxs-lookup"><span data-stu-id="25064-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="25064-118">應用程式的其他層可能需要額外的驗證。</span><span class="sxs-lookup"><span data-stu-id="25064-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="25064-119">（例如，資料層可能會強制執行 foreign key 條件約束）。[使用 WEB API 搭配 Entity Framework](../data/using-web-api-with-entity-framework/part-1.md)的教學課程會探討其中一些問題。</span><span class="sxs-lookup"><span data-stu-id="25064-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="25064-120">「**張貼**中」：當用戶端離開一些屬性時，就會進行張貼。</span><span class="sxs-lookup"><span data-stu-id="25064-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="25064-121">例如，假設用戶端傳送下列內容：</span><span class="sxs-lookup"><span data-stu-id="25064-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="25064-122">在這裡，用戶端未指定 `Price` 或 `Weight`的值。</span><span class="sxs-lookup"><span data-stu-id="25064-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="25064-123">JSON 格式器會將預設值零指派給遺漏的屬性。</span><span class="sxs-lookup"><span data-stu-id="25064-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="25064-124">模型狀態有效，因為零是這些屬性的有效值。</span><span class="sxs-lookup"><span data-stu-id="25064-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="25064-125">這是否為問題，取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="25064-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="25064-126">例如，在更新作業中，您可能會想要區分「零」和「未設定」。</span><span class="sxs-lookup"><span data-stu-id="25064-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="25064-127">若要強制用戶端設定值，請將屬性設為 nullable 並設定**必要**的屬性：</span><span class="sxs-lookup"><span data-stu-id="25064-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="25064-128">「**過度張貼**」：用戶端也可以傳送比您預期還要*多*的資料。</span><span class="sxs-lookup"><span data-stu-id="25064-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="25064-129">例如:</span><span class="sxs-lookup"><span data-stu-id="25064-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="25064-130">在這裡，JSON 包含不存在於 `Product` 模型中的屬性（「色彩」）。</span><span class="sxs-lookup"><span data-stu-id="25064-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="25064-131">在此情況下，JSON 格式器只會忽略此值。</span><span class="sxs-lookup"><span data-stu-id="25064-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="25064-132">（XML 格式器會執行相同的工作）。如果您的模型有您想要唯讀的屬性，則過度發佈會導致問題。</span><span class="sxs-lookup"><span data-stu-id="25064-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="25064-133">例如:</span><span class="sxs-lookup"><span data-stu-id="25064-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="25064-134">您不希望使用者更新 `IsAdmin` 屬性，並將自己提升為系統管理員！</span><span class="sxs-lookup"><span data-stu-id="25064-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="25064-135">最安全的策略是使用完全符合允許用戶端傳送的模型類別：</span><span class="sxs-lookup"><span data-stu-id="25064-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="25064-136">Brad Wilson 的 blog 文章「[輸入驗證與 ASP.NET MVC 中的模型驗證](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)」，在張貼和過度張貼方面都有很好的討論。</span><span class="sxs-lookup"><span data-stu-id="25064-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="25064-137">雖然這篇文章是關於 ASP.NET MVC 2，但這些問題仍然與 Web API 有關。</span><span class="sxs-lookup"><span data-stu-id="25064-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>

## <a name="handling-validation-errors"></a><span data-ttu-id="25064-138">處理驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="25064-138">Handling Validation Errors</span></span>

<span data-ttu-id="25064-139">驗證失敗時，Web API 不會自動將錯誤傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="25064-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="25064-140">由控制器動作負責檢查模型狀態並適當地回應。</span><span class="sxs-lookup"><span data-stu-id="25064-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="25064-141">您也可以在叫用控制器動作之前，建立動作篩選準則來檢查模型狀態。</span><span class="sxs-lookup"><span data-stu-id="25064-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="25064-142">下列程式碼顯示一個範例：</span><span class="sxs-lookup"><span data-stu-id="25064-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="25064-143">如果模型驗證失敗，此篩選會傳回包含驗證錯誤的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="25064-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="25064-144">在這種情況下，就不會叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="25064-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="25064-145">若要將此篩選套用至所有 Web API 控制器，請在設定期間，將篩選準則的實例新增至**HttpConfiguration**集合：</span><span class="sxs-lookup"><span data-stu-id="25064-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="25064-146">另一個選項是將篩選準則設定為個別控制器或控制器動作上的屬性：</span><span class="sxs-lookup"><span data-stu-id="25064-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
