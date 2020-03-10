---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: 使用服務層進行驗證（C#） |Microsoft Docs
author: StephenWalther
description: 瞭解如何將您的驗證邏輯移出控制器動作並放入個別的服務層。 在本教學課程中，Stephen Walther 將說明您如何 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: da1a1c9cc79a452eb0d7597810e86f7bcf6cd179
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542858"
---
# <a name="validating-with-a-service-layer-c"></a><span data-ttu-id="50f64-104">驗證與服務層 (C#)</span><span class="sxs-lookup"><span data-stu-id="50f64-104">Validating with a Service Layer (C#)</span></span>

<span data-ttu-id="50f64-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="50f64-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="50f64-106">瞭解如何將您的驗證邏輯移出控制器動作並放入個別的服務層。</span><span class="sxs-lookup"><span data-stu-id="50f64-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="50f64-107">在本教學課程中，Stephen Walther 將說明如何藉由將您的服務層與控制器層隔離，來維持明顯的顧慮分離。</span><span class="sxs-lookup"><span data-stu-id="50f64-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>

<span data-ttu-id="50f64-108">本教學課程的目的是要說明在 ASP.NET MVC 應用程式中執行驗證的一種方法。</span><span class="sxs-lookup"><span data-stu-id="50f64-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="50f64-109">在本教學課程中，您將瞭解如何將您的驗證邏輯移出您的控制器，並將其移至不同的服務層。</span><span class="sxs-lookup"><span data-stu-id="50f64-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="50f64-110">區分考慮</span><span class="sxs-lookup"><span data-stu-id="50f64-110">Separating Concerns</span></span>

<span data-ttu-id="50f64-111">當您建立 ASP.NET MVC 應用程式時，您不應該將資料庫邏輯放在控制器動作內。</span><span class="sxs-lookup"><span data-stu-id="50f64-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="50f64-112">混用您的資料庫和控制器邏輯，會讓您的應用程式在一段時間內更難以維護。</span><span class="sxs-lookup"><span data-stu-id="50f64-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="50f64-113">建議您將所有的資料庫邏輯放在個別的存放庫層中。</span><span class="sxs-lookup"><span data-stu-id="50f64-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="50f64-114">例如，清單1包含名為 ProductRepository 的簡單存放庫。</span><span class="sxs-lookup"><span data-stu-id="50f64-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="50f64-115">產品存放庫包含應用程式的所有資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="50f64-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="50f64-116">此清單也包含產品存放庫所實行的 IProductRepository 介面。</span><span class="sxs-lookup"><span data-stu-id="50f64-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="50f64-117">**清單 1--Models\ProductRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="50f64-117">**Listing 1 -- Models\ProductRepository.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

<span data-ttu-id="50f64-118">[清單 2] 中的控制器會在其索引（）和 Create （）動作中使用儲存機制層。</span><span class="sxs-lookup"><span data-stu-id="50f64-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="50f64-119">請注意，此控制器不包含任何資料庫邏輯。</span><span class="sxs-lookup"><span data-stu-id="50f64-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="50f64-120">建立存放庫層可讓您維持清楚的關注點分離。</span><span class="sxs-lookup"><span data-stu-id="50f64-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="50f64-121">控制器負責應用程式流程式控制制邏輯，而存放庫負責資料存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="50f64-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="50f64-122">**清單 2-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="50f64-122">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="50f64-123">建立服務層級</span><span class="sxs-lookup"><span data-stu-id="50f64-123">Creating a Service Layer</span></span>

<span data-ttu-id="50f64-124">因此，應用程式流程式控制制邏輯屬於控制器，而資料存取邏輯則屬於存放庫。</span><span class="sxs-lookup"><span data-stu-id="50f64-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="50f64-125">在這種情況下，您要將驗證邏輯放在哪裡？</span><span class="sxs-lookup"><span data-stu-id="50f64-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="50f64-126">其中一個選項是將您的驗證邏輯放在*服務層*中。</span><span class="sxs-lookup"><span data-stu-id="50f64-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="50f64-127">服務層是 ASP.NET MVC 應用程式中的另一層，可協調控制器和存放庫層之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="50f64-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="50f64-128">服務層包含商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="50f64-128">The service layer contains business logic.</span></span> <span data-ttu-id="50f64-129">特別是，它包含驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="50f64-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="50f64-130">例如，[清單 3] 中的產品服務層有一個 CreateProduct （）方法。</span><span class="sxs-lookup"><span data-stu-id="50f64-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="50f64-131">CreateProduct （）方法會呼叫 ValidateProduct （）方法來驗證新的產品，然後才將產品傳遞至產品存放庫。</span><span class="sxs-lookup"><span data-stu-id="50f64-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="50f64-132">**清單 3-Models\ProductService.cs**</span><span class="sxs-lookup"><span data-stu-id="50f64-132">**Listing 3 - Models\ProductService.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

<span data-ttu-id="50f64-133">[清單 4] 中的產品控制器已更新為使用服務層，而不是儲存機制層。</span><span class="sxs-lookup"><span data-stu-id="50f64-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="50f64-134">控制器層會與服務層交談。</span><span class="sxs-lookup"><span data-stu-id="50f64-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="50f64-135">服務層會與存放庫層交談。</span><span class="sxs-lookup"><span data-stu-id="50f64-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="50f64-136">每一層都有個別的責任。</span><span class="sxs-lookup"><span data-stu-id="50f64-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="50f64-137">**清單 4-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="50f64-137">**Listing 4 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

<span data-ttu-id="50f64-138">請注意，產品服務是在產品控制器的程式中建立的。</span><span class="sxs-lookup"><span data-stu-id="50f64-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="50f64-139">建立產品服務時，會將模型狀態字典傳遞至服務。</span><span class="sxs-lookup"><span data-stu-id="50f64-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="50f64-140">產品服務會使用模型狀態，將驗證錯誤訊息傳回到控制器。</span><span class="sxs-lookup"><span data-stu-id="50f64-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="50f64-141">將服務層分離</span><span class="sxs-lookup"><span data-stu-id="50f64-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="50f64-142">我們無法將控制器和服務層隔離在一個方面。</span><span class="sxs-lookup"><span data-stu-id="50f64-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="50f64-143">控制器和服務層會透過模型狀態進行通訊。</span><span class="sxs-lookup"><span data-stu-id="50f64-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="50f64-144">換句話說，服務層級相依于 ASP.NET MVC 架構的特定功能。</span><span class="sxs-lookup"><span data-stu-id="50f64-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="50f64-145">我們想要盡可能將服務層與控制器層隔離。</span><span class="sxs-lookup"><span data-stu-id="50f64-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="50f64-146">理論上，我們應該能夠將服務層與任何類型的應用程式搭配使用，而不只是 ASP.NET 的 MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="50f64-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="50f64-147">例如，在未來，我們可能會想要為應用程式建立 WPF 前端。</span><span class="sxs-lookup"><span data-stu-id="50f64-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="50f64-148">我們應該會找到一種方法，從我們的服務層中移除對 ASP.NET MVC 模型狀態的相依性。</span><span class="sxs-lookup"><span data-stu-id="50f64-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="50f64-149">在 [清單 5] 中，服務層已更新，因此不會再使用模型狀態。</span><span class="sxs-lookup"><span data-stu-id="50f64-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="50f64-150">相反地，它會使用任何可執行 IValidationDictionary 介面的類別。</span><span class="sxs-lookup"><span data-stu-id="50f64-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="50f64-151">**清單 5-Models\ProductService.cs （分離）**</span><span class="sxs-lookup"><span data-stu-id="50f64-151">**Listing 5 - Models\ProductService.cs (decoupled)**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

<span data-ttu-id="50f64-152">IValidationDictionary 介面定義于 [清單 6] 中。</span><span class="sxs-lookup"><span data-stu-id="50f64-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="50f64-153">這個簡單介面具有單一方法和單一屬性。</span><span class="sxs-lookup"><span data-stu-id="50f64-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="50f64-154">**清單 6-Models\IValidationDictionary.cs**</span><span class="sxs-lookup"><span data-stu-id="50f64-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

<span data-ttu-id="50f64-155">清單7中名為 ModelStateWrapper 類別的類別會執行 IValidationDictionary 介面。</span><span class="sxs-lookup"><span data-stu-id="50f64-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="50f64-156">您可以藉由將模型狀態字典傳遞給此函式，來具現化 ModelStateWrapper 類別。</span><span class="sxs-lookup"><span data-stu-id="50f64-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="50f64-157">**清單 7-Models\ModelStateWrapper.cs**</span><span class="sxs-lookup"><span data-stu-id="50f64-157">**Listing 7 - Models\ModelStateWrapper.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

<span data-ttu-id="50f64-158">最後，在 [清單 8] 中更新的控制器在其「函式」中建立服務層時，會使用 ModelStateWrapper。</span><span class="sxs-lookup"><span data-stu-id="50f64-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="50f64-159">**清單 8-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="50f64-159">**Listing 8 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

<span data-ttu-id="50f64-160">使用 IValidationDictionary 介面和 ModelStateWrapper 類別可讓我們將我們的服務層與控制器層完全隔離。</span><span class="sxs-lookup"><span data-stu-id="50f64-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="50f64-161">服務層不再相依于模型狀態。</span><span class="sxs-lookup"><span data-stu-id="50f64-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="50f64-162">您可以將任何可執行 IValidationDictionary 介面的類別傳遞至服務層。</span><span class="sxs-lookup"><span data-stu-id="50f64-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="50f64-163">例如，WPF 應用程式可能會使用簡單的集合類別來執行 IValidationDictionary 介面。</span><span class="sxs-lookup"><span data-stu-id="50f64-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="50f64-164">總結</span><span class="sxs-lookup"><span data-stu-id="50f64-164">Summary</span></span>

<span data-ttu-id="50f64-165">本教學課程的目的是要討論在 ASP.NET MVC 應用程式中執行驗證的一種方法。</span><span class="sxs-lookup"><span data-stu-id="50f64-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="50f64-166">在本教學課程中，您已瞭解如何將您的所有驗證邏輯移出控制器，並將其移至不同的服務層。</span><span class="sxs-lookup"><span data-stu-id="50f64-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="50f64-167">您也已瞭解如何藉由建立 ModelStateWrapper 類別，將您的服務層與控制器層隔離。</span><span class="sxs-lookup"><span data-stu-id="50f64-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="50f64-168">[上一頁](validating-with-the-idataerrorinfo-interface-cs.md)
> [下一頁](validation-with-the-data-annotation-validators-cs.md)</span><span class="sxs-lookup"><span data-stu-id="50f64-168">[Previous](validating-with-the-idataerrorinfo-interface-cs.md)
[Next](validation-with-the-data-annotation-validators-cs.md)</span></span>
