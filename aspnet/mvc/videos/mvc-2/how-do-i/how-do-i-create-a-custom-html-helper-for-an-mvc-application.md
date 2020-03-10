---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: 如何：為 MVC 應用程式建立自訂 HTML Helper？ | Microsoft Docs
author: rick-anderson
description: 在這段影片中，Chris Pels 示範如何建立在 MVC 應用程式中，標準集內無法使用的自訂 HtmlHelper。 首先，範例 MVC 應用程式 。
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559042"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="c7893-105">如何：為 MVC 應用程式建立自訂 HTML Helper？</span><span class="sxs-lookup"><span data-stu-id="c7893-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="c7893-106">依[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="c7893-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="c7893-107">在這段影片中，Chris Pels 示範如何建立在 MVC 應用程式中，標準集內無法使用的自訂 HtmlHelper。</span><span class="sxs-lookup"><span data-stu-id="c7893-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="c7893-108">首先，會使用示範控制器和 view 來建立範例 MVC 應用程式，以測試自訂 HtmlHelper。</span><span class="sxs-lookup"><span data-stu-id="c7893-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="c7893-109">接下來，系統會使用公開函式建立模組，此方法是代表自訂 HtmlHelper 之執行的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="c7893-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="c7893-110">自訂 helper 是用來在頁面中建立 `<img>` 標記，並接收數個輸入參數，包括影像標記的識別碼、url 和替代文字。</span><span class="sxs-lookup"><span data-stu-id="c7893-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="c7893-111">然後，會將邏輯新增至函式，以使用指定的資訊傳回已完成的 `<img>` 標記。</span><span class="sxs-lookup"><span data-stu-id="c7893-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="c7893-112">然後，在 [示範] 頁面上使用自訂 HtmlHelper 來顯示影像。</span><span class="sxs-lookup"><span data-stu-id="c7893-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="c7893-113">最後，自訂 HtmlHelper 會展開以包含多個「函數覆寫」，以提供更輕鬆地建立不同 `<img>` 標記的彈性。</span><span class="sxs-lookup"><span data-stu-id="c7893-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="c7893-114">&#9654;觀看影片（18分鐘）</span><span class="sxs-lookup"><span data-stu-id="c7893-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="c7893-115">[上一頁](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [下一頁](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="c7893-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
