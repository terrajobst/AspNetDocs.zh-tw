---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 在 ASP.NET Web API 中傳送 HTML 表單資料：表單 urlencoded 資料-ASP.NET 4。x
author: MikeWasson
description: 本文說明如何將表單 urlencoded 資料張貼至 ASP.NET 4.x 的 Web API 控制器
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557600"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="94e40-103">在 ASP.NET Web API 中傳送 HTML 表單資料：表單 urlencoded 資料</span><span class="sxs-lookup"><span data-stu-id="94e40-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="94e40-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="94e40-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="94e40-105">第1部分：表單 urlencoded 資料</span><span class="sxs-lookup"><span data-stu-id="94e40-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="94e40-106">本文說明如何將表單 urlencoded 資料張貼至 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="94e40-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="94e40-107">HTML 表單總覽</span><span class="sxs-lookup"><span data-stu-id="94e40-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="94e40-108">傳送複雜類型</span><span class="sxs-lookup"><span data-stu-id="94e40-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="94e40-109">透過 AJAX 傳送表單資料</span><span class="sxs-lookup"><span data-stu-id="94e40-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="94e40-110">傳送簡單類型</span><span class="sxs-lookup"><span data-stu-id="94e40-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="94e40-111">[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)。</span><span class="sxs-lookup"><span data-stu-id="94e40-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="94e40-112">HTML 表單總覽</span><span class="sxs-lookup"><span data-stu-id="94e40-112">Overview of HTML Forms</span></span>

<span data-ttu-id="94e40-113">HTML 表單使用 GET 或 POST 將資料傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="94e40-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="94e40-114">**Form**元素的**METHOD**屬性提供 HTTP 方法：</span><span class="sxs-lookup"><span data-stu-id="94e40-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="94e40-115">預設方法為 GET。</span><span class="sxs-lookup"><span data-stu-id="94e40-115">The default method is GET.</span></span> <span data-ttu-id="94e40-116">如果表單使用 GET，則表單資料會在 URI 中編碼為查詢字串。</span><span class="sxs-lookup"><span data-stu-id="94e40-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="94e40-117">如果表單使用 POST，則表單資料會放在要求主體中。</span><span class="sxs-lookup"><span data-stu-id="94e40-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="94e40-118">針對張貼的資料， **enctype**屬性會指定要求主體的格式：</span><span class="sxs-lookup"><span data-stu-id="94e40-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="94e40-119">enctype</span><span class="sxs-lookup"><span data-stu-id="94e40-119">enctype</span></span> | <span data-ttu-id="94e40-120">說明</span><span class="sxs-lookup"><span data-stu-id="94e40-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="94e40-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="94e40-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="94e40-122">表單資料會編碼成成對的名稱/值，類似于 URI 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="94e40-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="94e40-123">這是 POST 的預設格式。</span><span class="sxs-lookup"><span data-stu-id="94e40-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="94e40-124">多部分/表單資料</span><span class="sxs-lookup"><span data-stu-id="94e40-124">multipart/form-data</span></span> | <span data-ttu-id="94e40-125">表單資料會編碼為多部分 MIME 訊息。</span><span class="sxs-lookup"><span data-stu-id="94e40-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="94e40-126">如果您要將檔案上傳到伺服器，請使用此格式。</span><span class="sxs-lookup"><span data-stu-id="94e40-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="94e40-127">本文的第1部分探討 x-www-表單 urlencoded 格式。</span><span class="sxs-lookup"><span data-stu-id="94e40-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="94e40-128">[第2部分](sending-html-form-data-part-2.md)描述多部分 MIME。</span><span class="sxs-lookup"><span data-stu-id="94e40-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="94e40-129">傳送複雜類型</span><span class="sxs-lookup"><span data-stu-id="94e40-129">Sending Complex Types</span></span>

<span data-ttu-id="94e40-130">一般來說，您會傳送複雜型別，其中包含從數個表單控制項取得的值。</span><span class="sxs-lookup"><span data-stu-id="94e40-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="94e40-131">請考慮下列代表狀態更新的模型：</span><span class="sxs-lookup"><span data-stu-id="94e40-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="94e40-132">以下是透過 POST 接受 `Update` 物件的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="94e40-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="94e40-133">此控制器使用以[動作為基礎的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)，因此路由範本為 &quot;api/{controller}/{action}/{id}&quot;。</span><span class="sxs-lookup"><span data-stu-id="94e40-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="94e40-134">用戶端會將資料張貼到 &quot;/api/updates/complex&quot;。</span><span class="sxs-lookup"><span data-stu-id="94e40-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="94e40-135">現在，我們將撰寫 HTML 表單，讓使用者提交狀態更新。</span><span class="sxs-lookup"><span data-stu-id="94e40-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="94e40-136">請注意，表單上的 [**動作**] 屬性是控制器動作的 URI。</span><span class="sxs-lookup"><span data-stu-id="94e40-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="94e40-137">以下是在中輸入一些值的表單：</span><span class="sxs-lookup"><span data-stu-id="94e40-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="94e40-138">當使用者按一下 [提交] 時，瀏覽器會傳送類似下列的 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="94e40-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="94e40-139">請注意，要求本文包含表單資料，格式為名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="94e40-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="94e40-140">Web API 會自動將名稱/值組轉換成 `Update` 類別的實例。</span><span class="sxs-lookup"><span data-stu-id="94e40-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="94e40-141">透過 AJAX 傳送表單資料</span><span class="sxs-lookup"><span data-stu-id="94e40-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="94e40-142">當使用者提交表單時，瀏覽器會離開目前頁面，並呈現回應訊息的本文。</span><span class="sxs-lookup"><span data-stu-id="94e40-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="94e40-143">當回應是 HTML 網頁時，這是正常的。</span><span class="sxs-lookup"><span data-stu-id="94e40-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="94e40-144">不過，使用 Web API，回應主體通常是空的或包含結構化的資料，例如 JSON。</span><span class="sxs-lookup"><span data-stu-id="94e40-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="94e40-145">在此情況下，使用 AJAX 要求來傳送表單資料會更有意義，讓頁面可以處理回應。</span><span class="sxs-lookup"><span data-stu-id="94e40-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="94e40-146">下列程式碼顯示如何使用 jQuery 張貼表單資料。</span><span class="sxs-lookup"><span data-stu-id="94e40-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="94e40-147">JQuery **submit**函式會將表單動作取代為新的函式。</span><span class="sxs-lookup"><span data-stu-id="94e40-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="94e40-148">這會覆寫 [提交] 按鈕的預設行為。</span><span class="sxs-lookup"><span data-stu-id="94e40-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="94e40-149">序列化函式會將表單資料**序列化**成成對的名稱/值。</span><span class="sxs-lookup"><span data-stu-id="94e40-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="94e40-150">若要將表單資料傳送到伺服器，請呼叫 `$.post()`。</span><span class="sxs-lookup"><span data-stu-id="94e40-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="94e40-151">當要求完成時，`.success()` 或 `.error()` 處理常式會向使用者顯示適當的訊息。</span><span class="sxs-lookup"><span data-stu-id="94e40-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="94e40-152">傳送簡單類型</span><span class="sxs-lookup"><span data-stu-id="94e40-152">Sending Simple Types</span></span>

<span data-ttu-id="94e40-153">在先前的章節中，我們傳送了複雜型別，也就是將哪個 Web API 還原序列化為模型類別的實例。</span><span class="sxs-lookup"><span data-stu-id="94e40-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="94e40-154">您也可以傳送簡單的類型，例如字串。</span><span class="sxs-lookup"><span data-stu-id="94e40-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="94e40-155">在傳送簡單型別之前，請考慮改為將值換成複雜型別。</span><span class="sxs-lookup"><span data-stu-id="94e40-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="94e40-156">這可讓您在伺服器端提供模型驗證的優點，並可讓您更輕鬆地視需要擴充模型。</span><span class="sxs-lookup"><span data-stu-id="94e40-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="94e40-157">傳送簡單類型的基本步驟相同，但有兩個細微的差異。</span><span class="sxs-lookup"><span data-stu-id="94e40-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="94e40-158">首先，在控制器中，您必須使用**FromBody**屬性裝飾參數名稱。</span><span class="sxs-lookup"><span data-stu-id="94e40-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="94e40-159">根據預設，Web API 會嘗試從要求 URI 取得簡單的類型。</span><span class="sxs-lookup"><span data-stu-id="94e40-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="94e40-160">**FromBody**屬性會告知 Web API 從要求主體讀取值。</span><span class="sxs-lookup"><span data-stu-id="94e40-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="94e40-161">Web API 會讀取最多一次的回應本文，因此只有一個動作參數可以來自要求主體。</span><span class="sxs-lookup"><span data-stu-id="94e40-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="94e40-162">如果您需要從要求主體取得多個值，請定義複雜型別。</span><span class="sxs-lookup"><span data-stu-id="94e40-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="94e40-163">第二，用戶端必須以下列格式傳送值：</span><span class="sxs-lookup"><span data-stu-id="94e40-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="94e40-164">具體而言，簡單類型的名稱/值組名稱部分必須是空的。</span><span class="sxs-lookup"><span data-stu-id="94e40-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="94e40-165">並非所有瀏覽器都支援 HTML 表單的此功能，但您會在腳本中建立此格式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="94e40-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="94e40-166">以下是範例表單：</span><span class="sxs-lookup"><span data-stu-id="94e40-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="94e40-167">以下是提交表單值的腳本。</span><span class="sxs-lookup"><span data-stu-id="94e40-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="94e40-168">與上一個腳本的唯一差異在於傳遞至**post**函式的引數。</span><span class="sxs-lookup"><span data-stu-id="94e40-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="94e40-169">您可以使用相同的方法來傳送簡單類型的陣列：</span><span class="sxs-lookup"><span data-stu-id="94e40-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="94e40-170">其他資源</span><span class="sxs-lookup"><span data-stu-id="94e40-170">Additional Resources</span></span>

[<span data-ttu-id="94e40-171">第2部分：檔案上傳和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="94e40-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
