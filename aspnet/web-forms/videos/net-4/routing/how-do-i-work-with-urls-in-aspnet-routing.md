---
uid: web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
title: 如何：使用 ASP.NET 路由中的 Url？ | Microsoft Docs
author: rick-anderson
description: 在這段影片中，Chris Pels 示範如何在使用 ASP.NET 路由的網站中指定 Url。 首先，會建立網站，並在總帳中定義路由 。
ms.author: riande
ms.date: 10/15/2010
ms.assetid: 08f9d0a7-cfa0-4914-a672-8a64295d7ba8
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
msc.type: video
ms.openlocfilehash: eb1060fd9cc9469dc2b1d2e918823316c36840cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78565125"
---
# <a name="how-do-i-work-with-urls-in-aspnet-routing"></a><span data-ttu-id="ae4b0-105">如何：使用 ASP.NET 路由中的 Url？</span><span class="sxs-lookup"><span data-stu-id="ae4b0-105">How Do I: Work with URLs in ASP.NET Routing?</span></span>

<span data-ttu-id="ae4b0-106">依[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="ae4b0-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="ae4b0-107">在這段影片中，Chris Pels 示範如何在使用 ASP.NET 路由的網站中指定 Url。</span><span class="sxs-lookup"><span data-stu-id="ae4b0-107">In this video Chris Pels shows how to specify URLs in a web site that utilizes ASP.NET routing.</span></span> <span data-ttu-id="ae4b0-108">首先，會建立網站，並在全域應用程式類別（global.asax）中定義路由。</span><span class="sxs-lookup"><span data-stu-id="ae4b0-108">First, a web site is created and routing is defined in the Global Application Class (.asax).</span></span> <span data-ttu-id="ae4b0-109">接下來，會建立範例網頁，並使用標準的「硬式編碼」方法（例如 "~/Stats/Visitors"）將以定義的路由為基礎的 URL 加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="ae4b0-109">Next, a sample web page is created and a URL based upon a defined route is added to the page using the standard "hard coded" approach, e.g., "~/Stats/Visitors".</span></span> <span data-ttu-id="ae4b0-110">接著，會將另一個連結新增至頁面，使用接受路由名稱和參數的 RouteValue 方法，以動態方式在標記中產生相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="ae4b0-110">Another link is then added to the page which dynamically generates the same URL in markup using the RouteValue method which accepts the route name and parameters.</span></span> <span data-ttu-id="ae4b0-111">然後使用程式碼（而不是直接在頁面中的標記）來執行相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="ae4b0-111">The same URL is then implemented using code rather than markup directly in the page.</span></span> <span data-ttu-id="ae4b0-112">然後，原始路由和實體頁面位置會變更，導致硬式編碼連結無法再運作，而動態產生的連結也會正常運作。</span><span class="sxs-lookup"><span data-stu-id="ae4b0-112">The original route and physical page location are then changed, resulting in the hard coded link no longer working whereas both dynamically generated links function properly.</span></span> <span data-ttu-id="ae4b0-113">最後，會討論動態產生之連結的值。</span><span class="sxs-lookup"><span data-stu-id="ae4b0-113">Finally, the value of dynamically generated links is then discussed.</span></span>

[<span data-ttu-id="ae4b0-114">&#9654;觀看影片（20分鐘）</span><span class="sxs-lookup"><span data-stu-id="ae4b0-114">&#9654; Watch video (20 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> [<span data-ttu-id="ae4b0-115">上一篇</span><span class="sxs-lookup"><span data-stu-id="ae4b0-115">Previous</span></span>](how-do-i-use-routing-with-aspnet-web-forms.md)
