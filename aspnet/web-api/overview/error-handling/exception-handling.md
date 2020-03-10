---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API 中的例外狀況處理-ASP.NET 4。x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622315"
---
# <a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="a018a-102">ASP.NET Web API 中的例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="a018a-102">Exception Handling in ASP.NET Web API</span></span>

<span data-ttu-id="a018a-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a018a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a018a-104">本文描述 ASP.NET Web API 中的錯誤和例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="a018a-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="a018a-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="a018a-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="a018a-106">例外狀況篩選條件</span><span class="sxs-lookup"><span data-stu-id="a018a-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="a018a-107">註冊例外狀況篩選準則</span><span class="sxs-lookup"><span data-stu-id="a018a-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="a018a-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="a018a-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="a018a-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="a018a-109">HttpResponseException</span></span>

<span data-ttu-id="a018a-110">如果 Web API 控制器擲回未攔截的例外狀況，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="a018a-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="a018a-111">根據預設，大部分的例外狀況會轉譯為 HTTP 回應，狀態碼為500、內部伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="a018a-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="a018a-112">**HttpResponseException**類型是特殊案例。</span><span class="sxs-lookup"><span data-stu-id="a018a-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="a018a-113">這個例外狀況會傳回您在例外狀況函數中指定的任何 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="a018a-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="a018a-114">例如，如果*id*參數無效，下列方法會傳回404，但找不到。</span><span class="sxs-lookup"><span data-stu-id="a018a-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="a018a-115">若要更充分掌控回應，您也可以建立整個回應訊息，並將它包含在**HttpResponseException 中：**</span><span class="sxs-lookup"><span data-stu-id="a018a-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="a018a-116">例外狀況篩選條件</span><span class="sxs-lookup"><span data-stu-id="a018a-116">Exception Filters</span></span>

<span data-ttu-id="a018a-117">您可以藉由撰寫*例外狀況篩選準則*來自訂 Web API 處理例外狀況的方式。</span><span class="sxs-lookup"><span data-stu-id="a018a-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="a018a-118">當控制器方法擲回*不*是**HttpResponseException**例外狀況的任何未處理例外狀況時，就會執行例外狀況篩選。</span><span class="sxs-lookup"><span data-stu-id="a018a-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="a018a-119">**HttpResponseException**類型是特殊案例，因為它是特別針對傳回 HTTP 回應而設計的。</span><span class="sxs-lookup"><span data-stu-id="a018a-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="a018a-120">例外狀況篩選準則會執行**IExceptionFilter**介面。</span><span class="sxs-lookup"><span data-stu-id="a018a-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="a018a-121">撰寫例外狀況篩選器的最簡單方式是衍生自**ExceptionFilterAttribute**類別，並覆寫**OnException**方法。</span><span class="sxs-lookup"><span data-stu-id="a018a-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="a018a-122">ASP.NET Web API 中的例外狀況篩選準則類似于 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="a018a-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="a018a-123">不過，它們會分別在不同的命名空間和函式中宣告。</span><span class="sxs-lookup"><span data-stu-id="a018a-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="a018a-124">特別是，在 MVC 中使用的**system.web.mvc.handleerrorattribute class**類別不會處理 Web API 控制器所擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a018a-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>

<span data-ttu-id="a018a-125">以下是將**NotImplementedException**例外狀況轉換成 HTTP 狀態碼501的篩選準則，而不是實作為：</span><span class="sxs-lookup"><span data-stu-id="a018a-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="a018a-126">**HttpActionExecutedCoNtext**物件的**Response**屬性包含將傳送至用戶端的 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="a018a-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="a018a-127">註冊例外狀況篩選準則</span><span class="sxs-lookup"><span data-stu-id="a018a-127">Registering Exception Filters</span></span>

<span data-ttu-id="a018a-128">有數種方式可以註冊 Web API 例外狀況篩選︰</span><span class="sxs-lookup"><span data-stu-id="a018a-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="a018a-129">透過動作</span><span class="sxs-lookup"><span data-stu-id="a018a-129">By action</span></span>
- <span data-ttu-id="a018a-130">透過控制器</span><span class="sxs-lookup"><span data-stu-id="a018a-130">By controller</span></span>
- <span data-ttu-id="a018a-131">全域</span><span class="sxs-lookup"><span data-stu-id="a018a-131">Globally</span></span>

<span data-ttu-id="a018a-132">若要將篩選套用至特定動作，請在動作中新增篩選來做為屬性︰</span><span class="sxs-lookup"><span data-stu-id="a018a-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="a018a-133">若要將篩選套用至控制器上的所有動作，請將篩選準則新增為控制器類別的屬性：</span><span class="sxs-lookup"><span data-stu-id="a018a-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="a018a-134">若要將篩選準則全域套用至所有 Web API 控制器，請將篩選準則的實例新增至**GlobalConfiguration**集合。</span><span class="sxs-lookup"><span data-stu-id="a018a-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="a018a-135">此集合中的例外狀況篩選會套用至任何 Web API 控制器動作。</span><span class="sxs-lookup"><span data-stu-id="a018a-135">Exception filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="a018a-136">如果您使用 ASP.NET MVC 4 Web 應用程式 專案範本來建立專案，請將您的 Web API 設定程式碼放在 `WebApiConfig` 類別中，此類別位於應用程式\_啟動 資料夾中：</span><span class="sxs-lookup"><span data-stu-id="a018a-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="a018a-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="a018a-137">HttpError</span></span>

<span data-ttu-id="a018a-138">**HttpError**物件會提供一致的方式，在回應主體中傳回錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="a018a-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="a018a-139">下列範例示範如何在回應主體中傳回 HTTP 狀態碼404（找不到）和**HttpError** 。</span><span class="sxs-lookup"><span data-stu-id="a018a-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="a018a-140">**CreateErrorResponse**是在**HttpRequestMessageExtensions**類別中定義的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="a018a-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="a018a-141">就內部而言， **CreateErrorResponse**會建立**HttpError**實例，然後建立包含**HttpError**的**HttpResponseMessage** 。</span><span class="sxs-lookup"><span data-stu-id="a018a-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="a018a-142">在此範例中，如果方法成功，它會傳回 HTTP 回應中的產品。</span><span class="sxs-lookup"><span data-stu-id="a018a-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="a018a-143">但是，如果找不到要求的產品，則 HTTP 回應會在要求主體中包含**HttpError** 。</span><span class="sxs-lookup"><span data-stu-id="a018a-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="a018a-144">回應可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="a018a-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="a018a-145">請注意，在此範例中， **HttpError**已序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="a018a-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="a018a-146">使用**HttpError**的其中一個優點是，它會經歷與任何其他強型別模型相同的[內容協調](../formats-and-model-binding/content-negotiation.md)和序列化程式。</span><span class="sxs-lookup"><span data-stu-id="a018a-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="a018a-147">HttpError 和模型驗證</span><span class="sxs-lookup"><span data-stu-id="a018a-147">HttpError and Model Validation</span></span>

<span data-ttu-id="a018a-148">若要進行模型驗證，您可以將模型狀態傳遞至**CreateErrorResponse**，以在回應中包含驗證錯誤：</span><span class="sxs-lookup"><span data-stu-id="a018a-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="a018a-149">這個範例可能會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="a018a-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="a018a-150">如需模型驗證的詳細資訊，請參閱[ASP.NET Web API 中的模型驗證](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a018a-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="a018a-151">搭配使用 HttpError 與 HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="a018a-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="a018a-152">先前的範例會從控制器動作傳回**HttpResponseMessage**訊息，但是您也可以使用**HttpResponseException**來傳回**HttpError**。</span><span class="sxs-lookup"><span data-stu-id="a018a-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="a018a-153">這可讓您在正常的成功情況下傳回強型別模型，而如果發生錯誤，仍然會傳回**HttpError** ：</span><span class="sxs-lookup"><span data-stu-id="a018a-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
