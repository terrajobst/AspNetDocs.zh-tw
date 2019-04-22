---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: ASP.NET Web API 中傳送 HTML 表單資料：Form-urlencoded Data - ASP.NET 4.x
author: MikeWasson
description: 本文說明如何發佈至使用 ASP.NET 的 Web API 控制器的 form-urlencoded 資料 4.x
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: fb0309af11910125943737ebb721b356b7bd08bc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59418296"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="71572-103">ASP.NET Web API 中傳送 HTML 表單資料：Form-urlencoded 資料</span><span class="sxs-lookup"><span data-stu-id="71572-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="71572-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="71572-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="71572-105">第 1 部份：Form-urlencoded 資料</span><span class="sxs-lookup"><span data-stu-id="71572-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="71572-106">本文說明如何發佈到 Web API 控制器的 form-urlencoded 資料。</span><span class="sxs-lookup"><span data-stu-id="71572-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="71572-107">HTML 表單的概觀</span><span class="sxs-lookup"><span data-stu-id="71572-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="71572-108">傳送的複雜型別</span><span class="sxs-lookup"><span data-stu-id="71572-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="71572-109">透過 AJAX 的表單資料傳送</span><span class="sxs-lookup"><span data-stu-id="71572-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="71572-110">傳送的簡單類型</span><span class="sxs-lookup"><span data-stu-id="71572-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="71572-111">[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)。</span><span class="sxs-lookup"><span data-stu-id="71572-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="71572-112">HTML 表單的概觀</span><span class="sxs-lookup"><span data-stu-id="71572-112">Overview of HTML Forms</span></span>

<span data-ttu-id="71572-113">HTML 表單使用取得，或是張貼到將資料傳送到伺服器。</span><span class="sxs-lookup"><span data-stu-id="71572-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="71572-114">**方法**屬性**表單**項目提供的 HTTP 方法：</span><span class="sxs-lookup"><span data-stu-id="71572-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="71572-115">預設方法是 GET。</span><span class="sxs-lookup"><span data-stu-id="71572-115">The default method is GET.</span></span> <span data-ttu-id="71572-116">如果此表單會使用 GET，資料會被編碼為查詢字串之 URI 中的表單。</span><span class="sxs-lookup"><span data-stu-id="71572-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="71572-117">如果表單會使用 POST，表單資料被放在要求主體中。</span><span class="sxs-lookup"><span data-stu-id="71572-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="71572-118">已張貼的資料，如**enctype**屬性會指定要求主體格式：</span><span class="sxs-lookup"><span data-stu-id="71572-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="71572-119">enctype</span><span class="sxs-lookup"><span data-stu-id="71572-119">enctype</span></span> | <span data-ttu-id="71572-120">描述</span><span class="sxs-lookup"><span data-stu-id="71572-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71572-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="71572-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="71572-122">表單資料會編碼成名稱/值組，類似於 URI 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="71572-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="71572-123">這是 POST 的預設格式。</span><span class="sxs-lookup"><span data-stu-id="71572-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="71572-124">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="71572-124">multipart/form-data</span></span> | <span data-ttu-id="71572-125">表單資料會編碼為多部分 MIME 訊息。</span><span class="sxs-lookup"><span data-stu-id="71572-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="71572-126">如果您要將檔案上傳到伺服器，請使用此格式。</span><span class="sxs-lookup"><span data-stu-id="71572-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="71572-127">這篇文章的第 1 部分探討 x-www-表單-urlencoded 格式。</span><span class="sxs-lookup"><span data-stu-id="71572-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="71572-128">[第 2 部分](sending-html-form-data-part-2.md)描述多部分 MIME。</span><span class="sxs-lookup"><span data-stu-id="71572-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="71572-129">傳送的複雜型別</span><span class="sxs-lookup"><span data-stu-id="71572-129">Sending Complex Types</span></span>

<span data-ttu-id="71572-130">一般而言，您將會傳送複雜型別，從數個表單控制項的值所組成。</span><span class="sxs-lookup"><span data-stu-id="71572-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="71572-131">請考慮下列模型表示的狀態更新：</span><span class="sxs-lookup"><span data-stu-id="71572-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="71572-132">以下是可接受的 Web API 控制器`Update`透過 POST 的物件。</span><span class="sxs-lookup"><span data-stu-id="71572-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="71572-133">此控制器會使用[動作為基礎的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)，因此，路由範本&quot;api / {controller} / {action} / {id}&quot;。</span><span class="sxs-lookup"><span data-stu-id="71572-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="71572-134">用戶端會將資料公佈至&quot;/api/updates/complex&quot;。</span><span class="sxs-lookup"><span data-stu-id="71572-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>


<span data-ttu-id="71572-135">現在讓我們編寫 HTML 表單提交狀態更新的使用者。</span><span class="sxs-lookup"><span data-stu-id="71572-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="71572-136">請注意，**動作**表單上的屬性是我們的控制器動作的 URI。</span><span class="sxs-lookup"><span data-stu-id="71572-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="71572-137">以下是表單中輸入一些值：</span><span class="sxs-lookup"><span data-stu-id="71572-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="71572-138">當使用者按一下送出時，瀏覽器會傳送 HTTP 要求如下所示：</span><span class="sxs-lookup"><span data-stu-id="71572-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="71572-139">請注意要求主體包含表單資料，格式為名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="71572-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="71572-140">Web API 會自動轉換為名稱/值組的執行個體`Update`類別。</span><span class="sxs-lookup"><span data-stu-id="71572-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="71572-141">透過 AJAX 的表單資料傳送</span><span class="sxs-lookup"><span data-stu-id="71572-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="71572-142">當使用者提交表單時，瀏覽器瀏覽離開目前頁面，並呈現回應訊息的本文。</span><span class="sxs-lookup"><span data-stu-id="71572-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="71572-143">回應是 HTML 網頁時 [確定]。</span><span class="sxs-lookup"><span data-stu-id="71572-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="71572-144">使用 web API 中，不過，回應主體是通常是空的或包含結構化的資料，例如 JSON。</span><span class="sxs-lookup"><span data-stu-id="71572-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="71572-145">在此情況下，較為合理，將傳送使用 AJAX 的表單資料要求，讓網頁可以處理回應。</span><span class="sxs-lookup"><span data-stu-id="71572-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="71572-146">下列程式碼顯示如何發佈使用 jQuery 表單資料。</span><span class="sxs-lookup"><span data-stu-id="71572-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="71572-147">JQuery**提交**函式會以新的函式取代為表單動作。</span><span class="sxs-lookup"><span data-stu-id="71572-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="71572-148">這會覆寫 [提交] 按鈕的預設行為。</span><span class="sxs-lookup"><span data-stu-id="71572-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="71572-149">**序列化**函式會將表單資料序列化成名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="71572-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="71572-150">若要將表單資料傳送至伺服器中，呼叫`$.post()`。</span><span class="sxs-lookup"><span data-stu-id="71572-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="71572-151">要求完成時，`.success()`或`.error()`處理常式會向使用者顯示適當的訊息。</span><span class="sxs-lookup"><span data-stu-id="71572-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="71572-152">傳送的簡單類型</span><span class="sxs-lookup"><span data-stu-id="71572-152">Sending Simple Types</span></span>

<span data-ttu-id="71572-153">在先前章節中，我們會傳送複雜型別，Web API 的還原序列化的模型類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="71572-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="71572-154">您也可以傳送簡單的型別，例如字串。</span><span class="sxs-lookup"><span data-stu-id="71572-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="71572-155">在傳送之前的簡單類型，請考慮改為包裝複雜型別中的值。</span><span class="sxs-lookup"><span data-stu-id="71572-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="71572-156">這可讓您在伺服器端上的模型驗證的優點，並可讓您更輕鬆地擴充您的模型，如有需要。</span><span class="sxs-lookup"><span data-stu-id="71572-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>


<span data-ttu-id="71572-157">基本的步驟，以傳送簡單的型別相同，但有兩個微妙的差異。</span><span class="sxs-lookup"><span data-stu-id="71572-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="71572-158">首先，在控制器中，您必須裝飾的參數名稱前面加**FromBody**屬性。</span><span class="sxs-lookup"><span data-stu-id="71572-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="71572-159">根據預設，Web API 會嘗試取得要求 URI 中的簡單類型。</span><span class="sxs-lookup"><span data-stu-id="71572-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="71572-160">**FromBody**屬性會告知 Web API，可讀取的要求主體中的值。</span><span class="sxs-lookup"><span data-stu-id="71572-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="71572-161">Web API 回應主體讀取最多一次，因此只有一個動作的參數可能來自要求主體。</span><span class="sxs-lookup"><span data-stu-id="71572-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="71572-162">如果您需要從要求主體中取得多個值，定義複雜型別。</span><span class="sxs-lookup"><span data-stu-id="71572-162">If you need to get multiple values from the request body, define a complex type.</span></span>


<span data-ttu-id="71572-163">第二，用戶端必須傳送的值，其格式如下：</span><span class="sxs-lookup"><span data-stu-id="71572-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="71572-164">具體來說，名稱/值組的名稱部分必須是空的簡單型別。</span><span class="sxs-lookup"><span data-stu-id="71572-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="71572-165">並非所有瀏覽器都支援此 HTML 表單，但您建立此格式在指令碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="71572-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="71572-166">以下是範例表單：</span><span class="sxs-lookup"><span data-stu-id="71572-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="71572-167">而以下是要提交的表單值的指令碼。</span><span class="sxs-lookup"><span data-stu-id="71572-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="71572-168">先前的指令碼的唯一差別是傳入的引數**張貼**函式。</span><span class="sxs-lookup"><span data-stu-id="71572-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="71572-169">您可以使用相同的方法來傳送簡單類型的陣列：</span><span class="sxs-lookup"><span data-stu-id="71572-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="71572-170">其他資源</span><span class="sxs-lookup"><span data-stu-id="71572-170">Additional Resources</span></span>

[<span data-ttu-id="71572-171">第 2 部分：檔案上傳和多個 MIME</span><span class="sxs-lookup"><span data-stu-id="71572-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
