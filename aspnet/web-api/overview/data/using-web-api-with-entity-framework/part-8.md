---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 顯示專案詳細資料 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557320"
---
# <a name="display-item-details"></a><span data-ttu-id="e5b4d-102">顯示項目詳細資料</span><span class="sxs-lookup"><span data-stu-id="e5b4d-102">Display Item Details</span></span>

<span data-ttu-id="e5b4d-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e5b4d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="e5b4d-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="e5b4d-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="e5b4d-105">在本節中，您將新增可查看每一本書詳細資料的功能。</span><span class="sxs-lookup"><span data-stu-id="e5b4d-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="e5b4d-106">在 node.js 中，將下列程式碼新增至視圖模型：</span><span class="sxs-lookup"><span data-stu-id="e5b4d-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="e5b4d-107">在 Views/Home/Index. cshtml 中，將資料繫結項新增至 Details 連結：</span><span class="sxs-lookup"><span data-stu-id="e5b4d-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="e5b4d-108">這會將 &lt;&gt; 元素的 click 處理常式系結至視圖模型上的 `getBookDetail` 函數。</span><span class="sxs-lookup"><span data-stu-id="e5b4d-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="e5b4d-109">在相同的檔案中，取代下列標記：</span><span class="sxs-lookup"><span data-stu-id="e5b4d-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="e5b4d-110">取代為這個：</span><span class="sxs-lookup"><span data-stu-id="e5b4d-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="e5b4d-111">此標記會建立資料系結至視圖模型中可觀察之 `detail` 屬性的資料表。</span><span class="sxs-lookup"><span data-stu-id="e5b4d-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="e5b4d-112">"&lt;!--ko--&gt;&quot; 語法可讓您在 DOM 元素之外包含挖式系結。</span><span class="sxs-lookup"><span data-stu-id="e5b4d-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="e5b4d-113">在此情況下，`if` 系結只會在 `details` 為非 null 時，才會顯示標記的區段。</span><span class="sxs-lookup"><span data-stu-id="e5b4d-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="e5b4d-114">現在，如果您執行應用程式，然後按一下其中一個 &quot;詳細資料&quot; 連結，應用程式將會顯示書籍詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e5b4d-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="e5b4d-115">[上一頁](part-7.md)
> [下一頁](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="e5b4d-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
