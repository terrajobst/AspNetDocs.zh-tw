---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 在 ASP.NET Web API 中傳送 HTML 表單資料：檔案上傳和多部分 MIME ASP.NET 4。x
author: MikeWasson
description: 本教學課程說明如何將檔案上傳至 Web API。 它也會說明如何處理多部分 MIME 資料。
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557565"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="771b5-104">在 ASP.NET Web API 中傳送 HTML 表單資料：檔案上傳和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="771b5-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="771b5-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="771b5-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="771b5-106">第2部分：檔案上傳和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="771b5-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="771b5-107">本教學課程說明如何將檔案上傳至 Web API。</span><span class="sxs-lookup"><span data-stu-id="771b5-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="771b5-108">它也會說明如何處理多部分 MIME 資料。</span><span class="sxs-lookup"><span data-stu-id="771b5-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="771b5-109">[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)。</span><span class="sxs-lookup"><span data-stu-id="771b5-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>

<span data-ttu-id="771b5-110">以下是用來上傳檔案的 HTML 表單範例：</span><span class="sxs-lookup"><span data-stu-id="771b5-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="771b5-111">此表單包含文字輸入控制項和檔案輸入控制項。</span><span class="sxs-lookup"><span data-stu-id="771b5-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="771b5-112">當表單包含檔案輸入控制項時， **enctype**屬性應該一律為 &quot;多部分/表單資料&quot;，這會指定將表單當做多部分 MIME 訊息來傳送。</span><span class="sxs-lookup"><span data-stu-id="771b5-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="771b5-113">藉由查看範例要求，可以更輕鬆地瞭解多部分 MIME 訊息的格式：</span><span class="sxs-lookup"><span data-stu-id="771b5-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="771b5-114">此訊息分成兩個*部分*，每個表單控制項各一個。</span><span class="sxs-lookup"><span data-stu-id="771b5-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="771b5-115">部分界限是以連字號開頭的行來表示。</span><span class="sxs-lookup"><span data-stu-id="771b5-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="771b5-116">部分界限包含隨機元件（&quot;41184676334&quot;），以確保界限字串不會不慎出現在訊息部分內。</span><span class="sxs-lookup"><span data-stu-id="771b5-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>

<span data-ttu-id="771b5-117">每個訊息部分都包含一或多個標頭，後面接著元件內容。</span><span class="sxs-lookup"><span data-stu-id="771b5-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="771b5-118">內容配置標頭包含控制項的名稱。</span><span class="sxs-lookup"><span data-stu-id="771b5-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="771b5-119">針對檔案，它也包含檔案名。</span><span class="sxs-lookup"><span data-stu-id="771b5-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="771b5-120">Content-type 標頭會描述元件中的資料。</span><span class="sxs-lookup"><span data-stu-id="771b5-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="771b5-121">如果省略此標頭，則預設值為 text/純文字。</span><span class="sxs-lookup"><span data-stu-id="771b5-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="771b5-122">在上述範例中，使用者上傳了名為 GrandCanyon 的檔案，內容類型為 image/jpeg;而文字輸入的值是 &quot;夏日假期&quot;。</span><span class="sxs-lookup"><span data-stu-id="771b5-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="771b5-123">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="771b5-123">File Upload</span></span>

<span data-ttu-id="771b5-124">現在讓我們看看從多部分 MIME 訊息讀取檔案的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="771b5-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="771b5-125">控制器會以非同步方式讀取檔案。</span><span class="sxs-lookup"><span data-stu-id="771b5-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="771b5-126">Web API 支援使用以工作為[基礎的程式設計模型](https://msdn.microsoft.com/library/dd460693.aspx)的非同步動作。</span><span class="sxs-lookup"><span data-stu-id="771b5-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="771b5-127">首先，如果您的目標為支援**async**和**await**關鍵字的 .NET Framework 4.5，這裡就是程式碼。</span><span class="sxs-lookup"><span data-stu-id="771b5-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="771b5-128">請注意，控制器動作不會接受任何參數。</span><span class="sxs-lookup"><span data-stu-id="771b5-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="771b5-129">這是因為我們會處理動作內的要求本文，而不會叫用媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="771b5-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="771b5-130">**IsMultipartContent**方法會檢查要求是否包含多部分 MIME 訊息。</span><span class="sxs-lookup"><span data-stu-id="771b5-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="771b5-131">如果沒有，控制器會傳回 HTTP 狀態碼415（不支援的媒體類型）。</span><span class="sxs-lookup"><span data-stu-id="771b5-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="771b5-132">**MultipartFormDataStreamProvider**類別是一個協助程式物件，它會為上傳的檔案設定檔案串流。</span><span class="sxs-lookup"><span data-stu-id="771b5-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="771b5-133">若要讀取多部分 MIME 訊息，請呼叫**ReadAsMultipartAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="771b5-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="771b5-134">這個方法會解壓縮所有訊息部分，並將它們寫入**MultipartFormDataStreamProvider**所提供的資料流程。</span><span class="sxs-lookup"><span data-stu-id="771b5-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="771b5-135">當方法完成時，您可以從**FileData**屬性取得檔案的相關資訊，這是**MultipartFileData**物件的集合。</span><span class="sxs-lookup"><span data-stu-id="771b5-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="771b5-136">**MultipartFileData**是伺服器上儲存檔案的本機檔案名。</span><span class="sxs-lookup"><span data-stu-id="771b5-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="771b5-137">**MultipartFileData：標頭**包含元件標頭（*而不*是要求標頭）。</span><span class="sxs-lookup"><span data-stu-id="771b5-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="771b5-138">您可以使用這個來存取\_配置和內容類型標頭的內容。</span><span class="sxs-lookup"><span data-stu-id="771b5-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="771b5-139">顧名思義， **ReadAsMultipartAsync**是非同步方法。</span><span class="sxs-lookup"><span data-stu-id="771b5-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="771b5-140">若要在方法完成後執行工作，請使用[接續](https://msdn.microsoft.com/library/ee372288.aspx)工作（.net 4.0）或**await**關鍵字（.net 4.5）。</span><span class="sxs-lookup"><span data-stu-id="771b5-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="771b5-141">以下是先前程式碼的 .NET Framework 4.0 版本：</span><span class="sxs-lookup"><span data-stu-id="771b5-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="771b5-142">讀取表單控制項資料</span><span class="sxs-lookup"><span data-stu-id="771b5-142">Reading Form Control Data</span></span>

<span data-ttu-id="771b5-143">我稍早所示的 HTML 表單具有文字輸入控制項。</span><span class="sxs-lookup"><span data-stu-id="771b5-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="771b5-144">您可以從**MultipartFormDataStreamProvider**的**FormData**屬性取得控制項的值。</span><span class="sxs-lookup"><span data-stu-id="771b5-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="771b5-145">**FormData**是一個**NameValueCollection** ，其中包含表單控制項的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="771b5-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="771b5-146">集合可以包含重複的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="771b5-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="771b5-147">請考慮下列形式：</span><span class="sxs-lookup"><span data-stu-id="771b5-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="771b5-148">要求主體可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="771b5-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="771b5-149">在此情況下， **FormData**集合會包含下列索引鍵/值組：</span><span class="sxs-lookup"><span data-stu-id="771b5-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="771b5-150">旅程：來回</span><span class="sxs-lookup"><span data-stu-id="771b5-150">trip: round-trip</span></span>
- <span data-ttu-id="771b5-151">選項：持續</span><span class="sxs-lookup"><span data-stu-id="771b5-151">options: nonstop</span></span>
- <span data-ttu-id="771b5-152">選項：日期</span><span class="sxs-lookup"><span data-stu-id="771b5-152">options: dates</span></span>
- <span data-ttu-id="771b5-153">基座：視窗</span><span class="sxs-lookup"><span data-stu-id="771b5-153">seat: window</span></span>
