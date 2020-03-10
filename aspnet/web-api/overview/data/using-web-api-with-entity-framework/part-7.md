---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 建立視圖（UI） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557299"
---
# <a name="create-the-view-ui"></a><span data-ttu-id="80b6d-102">建立檢視 (UI)</span><span class="sxs-lookup"><span data-stu-id="80b6d-102">Create the View (UI)</span></span>

<span data-ttu-id="80b6d-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="80b6d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="80b6d-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="80b6d-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="80b6d-105">在本節中，您將開始定義應用程式的 HTML，並在 HTML 和 view 模型之間加入資料系結。</span><span class="sxs-lookup"><span data-stu-id="80b6d-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="80b6d-106">開啟檔案 Views/Home/Index. cshtml。</span><span class="sxs-lookup"><span data-stu-id="80b6d-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="80b6d-107">將該檔案的整個內容取代為下列程式。</span><span class="sxs-lookup"><span data-stu-id="80b6d-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="80b6d-108">大部分的 `div` 元素都是針對[啟動](http://getbootstrap.com/)程式樣式。</span><span class="sxs-lookup"><span data-stu-id="80b6d-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="80b6d-109">重要的專案是具有 `data-bind` 屬性的元素。</span><span class="sxs-lookup"><span data-stu-id="80b6d-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="80b6d-110">這個屬性會將 HTML 連結至視圖模型。</span><span class="sxs-lookup"><span data-stu-id="80b6d-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="80b6d-111">例如:</span><span class="sxs-lookup"><span data-stu-id="80b6d-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="80b6d-112">在此範例中，&quot;`text`&quot; 系結會導致 `<p>` 專案顯示視圖模型中 `error` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="80b6d-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="80b6d-113">回想一下，`error` 宣告為 `ko.observable`：</span><span class="sxs-lookup"><span data-stu-id="80b6d-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="80b6d-114">每當有新的值指派給 `error`時，挖不會更新 `<p>` 元素中的文字。</span><span class="sxs-lookup"><span data-stu-id="80b6d-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="80b6d-115">`foreach` 系結會告訴挖的會在 `books` 陣列的內容中執行迴圈。</span><span class="sxs-lookup"><span data-stu-id="80b6d-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="80b6d-116">針對陣列中的每個專案，挖的會建立新的 &lt;li&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="80b6d-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="80b6d-117">`foreach` 內容中的系結會參考陣列專案上的屬性。</span><span class="sxs-lookup"><span data-stu-id="80b6d-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="80b6d-118">例如:</span><span class="sxs-lookup"><span data-stu-id="80b6d-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="80b6d-119">在這裡，`text` 系結會讀取每一本書的作者屬性。</span><span class="sxs-lookup"><span data-stu-id="80b6d-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="80b6d-120">如果您現在執行應用程式，它看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="80b6d-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="80b6d-121">在頁面載入之後，會以非同步方式載入書籍清單。</span><span class="sxs-lookup"><span data-stu-id="80b6d-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="80b6d-122">目前，&quot;詳細資料&quot; 連結無法運作。</span><span class="sxs-lookup"><span data-stu-id="80b6d-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="80b6d-123">我們將在下一節新增這項功能。</span><span class="sxs-lookup"><span data-stu-id="80b6d-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="80b6d-124">[上一頁](part-6.md)
> [下一頁](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="80b6d-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
