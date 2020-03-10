---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 將新專案新增至資料庫 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557285"
---
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="ad173-102">將新項目新增至資料庫</span><span class="sxs-lookup"><span data-stu-id="ad173-102">Add a New Item to the Database</span></span>

<span data-ttu-id="ad173-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ad173-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ad173-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="ad173-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="ad173-105">在本節中，您將新增可讓使用者建立新書籍的功能。</span><span class="sxs-lookup"><span data-stu-id="ad173-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="ad173-106">在 node.js 中，將下列程式碼新增至視圖模型：</span><span class="sxs-lookup"><span data-stu-id="ad173-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="ad173-107">在 [Index. cshtml] 中，取代下列標記：</span><span class="sxs-lookup"><span data-stu-id="ad173-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="ad173-108">成為：</span><span class="sxs-lookup"><span data-stu-id="ad173-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="ad173-109">此標記會建立表單，以提交新的作者。</span><span class="sxs-lookup"><span data-stu-id="ad173-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="ad173-110">[作者] 下拉式清單的值會系結至 view 模型中 `authors` 可觀察的資料。</span><span class="sxs-lookup"><span data-stu-id="ad173-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="ad173-111">針對其他表單輸入，值會系結至視圖模型的 `newBook` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ad173-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="ad173-112">表單上的提交處理常式會系結至 `addBook` 函數：</span><span class="sxs-lookup"><span data-stu-id="ad173-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="ad173-113">`addBook` 函式會讀取資料系結表單輸入的目前值，以建立 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="ad173-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="ad173-114">然後，它會將 JSON 物件張貼到 `/api/books`。</span><span class="sxs-lookup"><span data-stu-id="ad173-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ad173-115">[上一頁](part-8.md)
> [下一頁](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="ad173-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
