---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 建立資料傳輸物件（Dto） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445765"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="8e067-102">建立資料傳輸物件 (DTO)</span><span class="sxs-lookup"><span data-stu-id="8e067-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="8e067-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8e067-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="8e067-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="8e067-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="8e067-105">現在，我們的 Web API 會向用戶端公開資料庫實體。</span><span class="sxs-lookup"><span data-stu-id="8e067-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="8e067-106">用戶端會接收直接對應至資料庫資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="8e067-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="8e067-107">不過，這不一定是不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="8e067-107">However, that's not always a good idea.</span></span> <span data-ttu-id="8e067-108">有時候您會想要變更傳送給用戶端之資料的圖形。</span><span class="sxs-lookup"><span data-stu-id="8e067-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="8e067-109">例如，您可能要：</span><span class="sxs-lookup"><span data-stu-id="8e067-109">For example, you might want to:</span></span>

- <span data-ttu-id="8e067-110">移除迴圈參考（請參閱上一節）。</span><span class="sxs-lookup"><span data-stu-id="8e067-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="8e067-111">隱藏用戶端不應查看的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="8e067-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="8e067-112">省略某些屬性，以減少承載大小。</span><span class="sxs-lookup"><span data-stu-id="8e067-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="8e067-113">將包含嵌套物件的物件圖形壓平合併，使其更方便用戶端。</span><span class="sxs-lookup"><span data-stu-id="8e067-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="8e067-114">避免「過度張貼」的弱點。</span><span class="sxs-lookup"><span data-stu-id="8e067-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="8e067-115">（如需過度張貼的討論，請參閱[模型驗證](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。）</span><span class="sxs-lookup"><span data-stu-id="8e067-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="8e067-116">將您的服務層與您的資料庫層分離。</span><span class="sxs-lookup"><span data-stu-id="8e067-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="8e067-117">若要完成此動作，您可以定義*資料傳輸物件*（DTO）。</span><span class="sxs-lookup"><span data-stu-id="8e067-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="8e067-118">DTO 是一種物件，可定義如何透過網路來傳送資料。</span><span class="sxs-lookup"><span data-stu-id="8e067-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="8e067-119">我們來看一下該如何與 Book 實體搭配運作。</span><span class="sxs-lookup"><span data-stu-id="8e067-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="8e067-120">在 [模型] 資料夾中，新增兩個 DTO 類別：</span><span class="sxs-lookup"><span data-stu-id="8e067-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="8e067-121">`BookDetailDto` 類別包含書籍模型中的所有屬性，不同之處在于 `AuthorName` 是會保存作者名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="8e067-121">The `BookDetailDto` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="8e067-122">`BookDto` 類別包含來自 `BookDetailDto`的屬性子集。</span><span class="sxs-lookup"><span data-stu-id="8e067-122">The `BookDto` class contains a subset of properties from `BookDetailDto`.</span></span>

<span data-ttu-id="8e067-123">接下來，將 `BooksController` 類別中的兩個 GET 方法取代為傳回 Dto 的版本。</span><span class="sxs-lookup"><span data-stu-id="8e067-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="8e067-124">我們將使用 LINQ **Select**語句，從書籍實體轉換成 dto。</span><span class="sxs-lookup"><span data-stu-id="8e067-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="8e067-125">以下是新的 `GetBooks` 方法所產生的 SQL。</span><span class="sxs-lookup"><span data-stu-id="8e067-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="8e067-126">您可以看到 EF 將 LINQ **Select**轉換成 SQL select 語句。</span><span class="sxs-lookup"><span data-stu-id="8e067-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="8e067-127">最後，修改 `PostBook` 方法以傳回 DTO。</span><span class="sxs-lookup"><span data-stu-id="8e067-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="8e067-128">在本教學課程中，我們會在程式碼中以手動方式轉換為 Dto。</span><span class="sxs-lookup"><span data-stu-id="8e067-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="8e067-129">另一個選項是使用程式庫（例如[AutoMapper](http://automapper.org/) ）來自動處理轉換。</span><span class="sxs-lookup"><span data-stu-id="8e067-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="8e067-130">[上一頁](part-4.md)
> [下一頁](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="8e067-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
