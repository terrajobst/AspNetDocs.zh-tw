---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 應用程式的生命週期 |Microsoft Docs
author: cephalin
description: 下載 PDF 檔，以圖表 ASP.NET MVC 5 應用程式的生命週期。 本生命週期檔提供 MVC 生命週期的高階觀點 。
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582198"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a><span data-ttu-id="70a0b-104">ASP.NET MVC 5 應用程式生命週期</span><span class="sxs-lookup"><span data-stu-id="70a0b-104">Lifecycle of an ASP.NET MVC 5 Application</span></span>

<span data-ttu-id="70a0b-105">依[Cephas Lin](https://github.com/cephalin)</span><span class="sxs-lookup"><span data-stu-id="70a0b-105">by [Cephas Lin](https://github.com/cephalin)</span></span>

[<span data-ttu-id="70a0b-106">下載 PDF 檔</span><span class="sxs-lookup"><span data-stu-id="70a0b-106">Download PDF Document</span></span>](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

<span data-ttu-id="70a0b-107">在這裡，您可以下載一份 PDF 檔，它會將每個 ASP.NET MVC 5 應用程式的生命週期，從接收 HTTP 要求，到將 HTTP 回應傳送回用戶端。</span><span class="sxs-lookup"><span data-stu-id="70a0b-107">Here you can download a PDF document that charts the lifecycle of every ASP.NET MVC 5 application, from receiving the HTTP request to sending the HTTP response back to the client.</span></span> <span data-ttu-id="70a0b-108">它是設計來做為 ASP.NET MVC 新手的教育工具，也是針對需要深入瞭解應用程式特定層面的人員所做的參考。</span><span class="sxs-lookup"><span data-stu-id="70a0b-108">It is designed both as an educational tool for those who are new to ASP.NET MVC and also as a reference for those who need to drill into specific aspects of the application.</span></span> <span data-ttu-id="70a0b-109">PDF 檔具有下列功能：</span><span class="sxs-lookup"><span data-stu-id="70a0b-109">The PDF document has the following features:</span></span>

- <span data-ttu-id="70a0b-110">相關的[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)階段，可協助您瞭解 MVC 與[ASP.NET 應用程式生命週期](https://msdn.microsoft.com/library/bb470252.aspx)的整合位置。</span><span class="sxs-lookup"><span data-stu-id="70a0b-110">Relevant [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) stages to help you understand where MVC integrates into the [ASP.NET application lifecycle](https://msdn.microsoft.com/library/bb470252.aspx).</span></span>
- <span data-ttu-id="70a0b-111">MVC 應用程式生命週期的高階觀點，您可以在其中瞭解每個 MVC 應用程式在要求處理管線中傳遞的主要階段。</span><span class="sxs-lookup"><span data-stu-id="70a0b-111">A high-level view of the MVC application lifecycle, where you can understand the major stages that every MVC application passes through in the request processing pipeline.</span></span>  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- <span data-ttu-id="70a0b-112">詳細資料檢視，顯示向下切入要求處理管線的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="70a0b-112">A detail view that shows drills down into the details of the request processing pipeline.</span></span> <span data-ttu-id="70a0b-113">您可以比較高階視圖和詳細資料檢視，查看如何將生命週期詳細資料收集到各種階段。</span><span class="sxs-lookup"><span data-stu-id="70a0b-113">You can compare the high-level view and the detail view to see how the lifecycles details are collected into the various stages.</span></span> <span data-ttu-id="70a0b-114">[下載 PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)以查看較大的視圖。</span><span class="sxs-lookup"><span data-stu-id="70a0b-114">[Download PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) to see a larger view.</span></span>
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- <span data-ttu-id="70a0b-115">在要求處理管線中，[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)物件上所有可覆寫方法的位置和用途。</span><span class="sxs-lookup"><span data-stu-id="70a0b-115">Placement and purpose of all overridable methods on the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) object in the request processing pipeline.</span></span> <span data-ttu-id="70a0b-116">您不一定需要覆寫任何一種方法，但請務必瞭解其在應用程式生命週期中的角色，讓您可以在適當的生命週期階段針對您想要的效果撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="70a0b-116">You may or may not have the need to override any one method, but it is important for you to understand their role in the application lifecycle so that you can write code at the appropriate life cycle stage for the effect you intend.</span></span>
- <span data-ttu-id="70a0b-117">放大的圖表會顯示每個篩選類型（驗證、授權、動作和結果）的叫用方式。</span><span class="sxs-lookup"><span data-stu-id="70a0b-117">Blown-up diagrams showing how each of the filter types (authentication, authorization, action, and result) is invoked.</span></span>
- <span data-ttu-id="70a0b-118">從詳細資料檢視中每個感興趣的點連結到有用的文章或 blog。</span><span class="sxs-lookup"><span data-stu-id="70a0b-118">Link to a useful article or blog from each point of interest in the detail view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70a0b-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70a0b-119">Next Steps</span></span>

<span data-ttu-id="70a0b-120">這份檔是否符合您的需求？</span><span class="sxs-lookup"><span data-stu-id="70a0b-120">Does this document meet your need?</span></span> <span data-ttu-id="70a0b-121">歡迎您提供寶貴的意見。</span><span class="sxs-lookup"><span data-stu-id="70a0b-121">We'd appreciate your feedback.</span></span> <span data-ttu-id="70a0b-122">如果您對應用程式中的 ASP.NET MVC 生命週期有任何疑問， [Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 論壇](https://forums.asp.net/1146.aspx)是很棒的地方。</span><span class="sxs-lookup"><span data-stu-id="70a0b-122">If you have any question on the ASP.NET MVC lifecycle in your application, [Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are great places to ask.</span></span> <span data-ttu-id="70a0b-123">請在 twitter 上追蹤[我](https://twitter.com/Cephas_MSFT)的最新教學課程，以取得更新。</span><span class="sxs-lookup"><span data-stu-id="70a0b-123">Follow [me](https://twitter.com/Cephas_MSFT) on twitter so you can get updates on my latest tutorials.</span></span>
