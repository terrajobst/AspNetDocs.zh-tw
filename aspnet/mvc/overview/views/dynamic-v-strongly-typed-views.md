---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 動態與 強型別視圖 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455641"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="ecedd-103">動態與</span><span class="sxs-lookup"><span data-stu-id="ecedd-103">Dynamic v.</span></span> <span data-ttu-id="ecedd-104">強型別檢視</span><span class="sxs-lookup"><span data-stu-id="ecedd-104">Strongly Typed Views</span></span>

<span data-ttu-id="ecedd-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ecedd-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ecedd-106">有三種方式可將控制器的資訊傳遞至 ASP.NET MVC 3 中的 view：</span><span class="sxs-lookup"><span data-stu-id="ecedd-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="ecedd-107">做為強型別模型物件。</span><span class="sxs-lookup"><span data-stu-id="ecedd-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="ecedd-108">當做動態類型（使用 @model 動態）</span><span class="sxs-lookup"><span data-stu-id="ecedd-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="ecedd-109">使用 ViewBag</span><span class="sxs-lookup"><span data-stu-id="ecedd-109">Using the ViewBag</span></span>

<span data-ttu-id="ecedd-110">我撰寫了一個簡單的 MVC 3 熱門 Blog 應用程式來比較和對比動態和強型別的觀點。</span><span class="sxs-lookup"><span data-stu-id="ecedd-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="ecedd-111">控制器一開始會有一份簡單的 blog 清單：</span><span class="sxs-lookup"><span data-stu-id="ecedd-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="ecedd-112">在 IndexNotStonglyTyped （）方法中按一下滑鼠右鍵，並新增 Razor view。</span><span class="sxs-lookup"><span data-stu-id="ecedd-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="ecedd-113">[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ecedd-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="ecedd-114">請確定未核取 [**建立強型別的視圖**] 方塊。</span><span class="sxs-lookup"><span data-stu-id="ecedd-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="ecedd-115">產生的視圖不會包含太多：</span><span class="sxs-lookup"><span data-stu-id="ecedd-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="ecedd-116">由於我們使用的是動態的，而不是強型別視圖，因此 intellisense 並不會協助我們。</span><span class="sxs-lookup"><span data-stu-id="ecedd-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="ecedd-117">完成的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="ecedd-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="ecedd-118">[![6646。 NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ecedd-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="ecedd-119">現在我們要加入強型別視圖。</span><span class="sxs-lookup"><span data-stu-id="ecedd-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="ecedd-120">將下列程式碼新增至控制器：</span><span class="sxs-lookup"><span data-stu-id="ecedd-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="ecedd-121">請注意，它完全是相同的傳回視圖（topBlogs）;以非強型別視圖的形式呼叫。</span><span class="sxs-lookup"><span data-stu-id="ecedd-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="ecedd-122">以滑鼠右鍵按一下*StonglyTypedIndex （）* 內部，然後選取 [**新增視圖**]。</span><span class="sxs-lookup"><span data-stu-id="ecedd-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="ecedd-123">這次請選取 [ **Blog**模型] 類別，然後選取 [**清單**] 做為 Scaffold 範本。</span><span class="sxs-lookup"><span data-stu-id="ecedd-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="ecedd-124">[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ecedd-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="ecedd-125">在新的 view 範本內，我們取得 intellisense 支援。</span><span class="sxs-lookup"><span data-stu-id="ecedd-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="ecedd-126">[![7002。 IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ecedd-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="ecedd-127">您可以在[這裡](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)下載 c # 專案。</span><span class="sxs-lookup"><span data-stu-id="ecedd-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
