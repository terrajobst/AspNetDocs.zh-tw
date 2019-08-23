---
uid: overview
title: ASP.NET 總覽 |Microsoft Docs
author: rick-anderson
description: ASP.NET 簡介, 這是用來建立網站、web 應用程式和 web Api 的免費架構。
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 9a6d08849f09c9d7a779df64f70e8770d2af3c87
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995291"
---
# <a name="aspnet-overview"></a><span data-ttu-id="43daa-103">ASP.NET 概觀</span><span class="sxs-lookup"><span data-stu-id="43daa-103">ASP.NET overview</span></span>

<span data-ttu-id="43daa-104">ASP.NET 是免費的 web 架構, 可用於使用 HTML、CSS 和 JavaScript 建立絕佳的網站和 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="43daa-104">ASP.NET is a free web framework for building great websites and web applications using HTML, CSS, and JavaScript.</span></span> <span data-ttu-id="43daa-105">您也可以建立 Web Api, 並使用 Web 通訊端等即時技術。</span><span class="sxs-lookup"><span data-stu-id="43daa-105">You can also create Web APIs and use real-time technologies like Web Sockets.</span></span>

<span data-ttu-id="43daa-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)是 ASP.NET 的替代方案。</span><span class="sxs-lookup"><span data-stu-id="43daa-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) is an alternative to ASP.NET.</span></span>  <span data-ttu-id="43daa-107">請參閱[如何在 ASP.NET 和 ASP.NET Core 之間選擇的指引](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)。</span><span class="sxs-lookup"><span data-stu-id="43daa-107">See the [guidance on how to choose between ASP.NET and ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).</span></span>

## <a name="get-started"></a><span data-ttu-id="43daa-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="43daa-108">Get started</span></span>

<span data-ttu-id="43daa-109">安裝[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)的社區版, 這是 Windows 上 ASP.NET 的免費 IDE。</span><span class="sxs-lookup"><span data-stu-id="43daa-109">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community edition, a free IDE for ASP.NET on Windows.</span></span>

## <a name="websites-and-web-applications"></a><span data-ttu-id="43daa-110">網站和 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="43daa-110">Websites and web applications</span></span>

 <span data-ttu-id="43daa-111">ASP.NET 提供三種建立 web 應用程式的架構:Web Forms、ASP.NET MVC 和 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="43daa-111">ASP.NET offers three frameworks for creating web applications: Web Forms, ASP.NET MVC, and ASP.NET Web Pages.</span></span> <span data-ttu-id="43daa-112">這三種架構都是穩定且成熟的, 而且您可以使用其中任何一個來建立絕佳的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="43daa-112">All three frameworks are stable and mature, and you can create great web applications with any of them.</span></span> <span data-ttu-id="43daa-113">無論您選擇何種架構, 都能取得所有 ASP.NET 的優點和功能。</span><span class="sxs-lookup"><span data-stu-id="43daa-113">No matter what framework you choose, you will get all the benefits and features of ASP.NET everywhere.</span></span>

<span data-ttu-id="43daa-114">每個架構的目標都是不同的開發樣式。</span><span class="sxs-lookup"><span data-stu-id="43daa-114">Each framework targets a different development style.</span></span> <span data-ttu-id="43daa-115">您所選擇的是取決於程式設計資產的組合 (知識、技能和開發經驗)、您所建立的應用程式類型, 以及您熟悉的開發方法。</span><span class="sxs-lookup"><span data-stu-id="43daa-115">The one you choose depends on a combination of your programming assets (knowledge, skills, and development experience), the type of application you're creating, and the development approach you're comfortable with.</span></span>

<span data-ttu-id="43daa-116">以下是每個架構的總覽, 以及如何在兩者之間進行選擇的一些概念。</span><span class="sxs-lookup"><span data-stu-id="43daa-116">Below is an overview of each of the frameworks and some ideas for how to choose between them.</span></span> <span data-ttu-id="43daa-117">如果您偏好影片簡介, 請參閱[建立具有 ASP.NET 的網站](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET)和[什麼是 Web 工具？](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)</span><span class="sxs-lookup"><span data-stu-id="43daa-117">If you prefer a video introduction, see [Making Websites with ASP.NET](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) and [What is Web Tools?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)</span></span>

|   | <span data-ttu-id="43daa-118">如果您的經驗</span><span class="sxs-lookup"><span data-stu-id="43daa-118">If you have experience in</span></span> | <span data-ttu-id="43daa-119">開發風格</span><span class="sxs-lookup"><span data-stu-id="43daa-119">Development style</span></span> | <span data-ttu-id="43daa-120">經驗</span><span class="sxs-lookup"><span data-stu-id="43daa-120">Expertise</span></span> |
|-----------|----------------------|-----------------------------------------------------|----------------|
| <span data-ttu-id="43daa-121">Web Form</span><span class="sxs-lookup"><span data-stu-id="43daa-121">Web Forms</span></span> | <span data-ttu-id="43daa-122">Win Forms, WPF, .NET</span><span class="sxs-lookup"><span data-stu-id="43daa-122">Win Forms, WPF, .NET</span></span> | <span data-ttu-id="43daa-123">使用封裝 HTML 標籤的豐富控制項庫進行快速開發</span><span class="sxs-lookup"><span data-stu-id="43daa-123">Rapid development using a rich library of controls that encapsulate HTML markup</span></span> | <span data-ttu-id="43daa-124">中等層級、先進的 RAD</span><span class="sxs-lookup"><span data-stu-id="43daa-124">Mid-Level, Advanced RAD</span></span> |
| <span data-ttu-id="43daa-125">MVC</span><span class="sxs-lookup"><span data-stu-id="43daa-125">MVC</span></span>       | <span data-ttu-id="43daa-126">Ruby on Rails, .NET</span><span class="sxs-lookup"><span data-stu-id="43daa-126">Ruby on Rails, .NET</span></span>  | <span data-ttu-id="43daa-127">完全掌控 HTML 標籤、程式碼和標記分隔, 以及輕鬆撰寫測試。</span><span class="sxs-lookup"><span data-stu-id="43daa-127">Full control over HTML markup, code and markup separated, and easy to write tests.</span></span> <span data-ttu-id="43daa-128">適用于行動和單頁應用程式 (SPA) 的最佳選擇。</span><span class="sxs-lookup"><span data-stu-id="43daa-128">The best choice for mobile and single-page applications (SPA).</span></span> | <span data-ttu-id="43daa-129">中等層級, 先進</span><span class="sxs-lookup"><span data-stu-id="43daa-129">Mid-Level, Advanced</span></span> |
| <span data-ttu-id="43daa-130">Web Pages</span><span class="sxs-lookup"><span data-stu-id="43daa-130">Web Pages</span></span>  | <span data-ttu-id="43daa-131">傳統 ASP, PHP</span><span class="sxs-lookup"><span data-stu-id="43daa-131">Classic ASP, PHP</span></span>     | <span data-ttu-id="43daa-132">將 HTML 標籤和您的程式碼一起放在同一個檔案中</span><span class="sxs-lookup"><span data-stu-id="43daa-132">HTML markup and your code together in the same file</span></span> | <span data-ttu-id="43daa-133">新的、中等層級</span><span class="sxs-lookup"><span data-stu-id="43daa-133">New, Mid-Level</span></span> |

### <a name="web-forms"></a><span data-ttu-id="43daa-134">Web Form</span><span class="sxs-lookup"><span data-stu-id="43daa-134">Web Forms</span></span>

<span data-ttu-id="43daa-135">透過 ASP.NET Web form, 您可以使用熟悉的拖放、事件驅動模型來建立動態網站。</span><span class="sxs-lookup"><span data-stu-id="43daa-135">With ASP.NET Web Forms, you can build dynamic websites using a familiar drag-and-drop, event-driven model.</span></span> <span data-ttu-id="43daa-136">設計介面和數百個控制項和元件可讓您快速建立複雜且功能強大的 UI 驅動網站, 並進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="43daa-136">A design surface and hundreds of controls and components let you rapidly build sophisticated, powerful UI-driven sites with data access.</span></span>

[<span data-ttu-id="43daa-137">深入瞭解 Web Forms</span><span class="sxs-lookup"><span data-stu-id="43daa-137">Learn more about Web Forms</span></span>](web-forms/index.md)

### <a name="mvc"></a><span data-ttu-id="43daa-138">MVC</span><span class="sxs-lookup"><span data-stu-id="43daa-138">MVC</span></span>

<span data-ttu-id="43daa-139">ASP.NET MVC 提供功能強大、以模式為基礎的方式來建立動態網站, 讓您能夠清楚區分問題, 並讓您完全掌控標記, 以進行更好的敏捷式開發。</span><span class="sxs-lookup"><span data-stu-id="43daa-139">ASP.NET MVC gives you a powerful, patterns-based way to build dynamic websites that enables a clean separation of concerns and that gives you full control over markup for enjoyable, agile development.</span></span> <span data-ttu-id="43daa-140">ASP.NET MVC 包含許多功能, 可讓您快速、以 TDD 易懂的開發, 建立採用最新 web 標準的精密應用程式。</span><span class="sxs-lookup"><span data-stu-id="43daa-140">ASP.NET MVC includes many features that enable fast, TDD-friendly development for creating sophisticated applications that use the latest web standards.</span></span>

[<span data-ttu-id="43daa-141">深入瞭解 MVC</span><span class="sxs-lookup"><span data-stu-id="43daa-141">Learn more about MVC</span></span>](mvc/index.md)

### <a name="aspnet-web-pages"></a><span data-ttu-id="43daa-142">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="43daa-142">ASP.NET Web Pages</span></span>

<span data-ttu-id="43daa-143">ASP.NET Web Pages 和 Razor 語法提供快速、平易近人且輕量的方式, 將伺服器程式碼與 HTML 結合以建立動態 Web 內容。</span><span class="sxs-lookup"><span data-stu-id="43daa-143">ASP.NET Web Pages and the Razor syntax provide a fast, approachable, and lightweight way to combine server code with HTML to create dynamic web content.</span></span> <span data-ttu-id="43daa-144">連接到資料庫、新增影片、連結至社交網站, 以及包含更多的功能, 可協助您建立符合最新 web 標準的美觀網站。</span><span class="sxs-lookup"><span data-stu-id="43daa-144">Connect to databases, add video, link to social networking sites, and include many more features that help you create beautiful sites that conform to the latest web standards.</span></span>

[<span data-ttu-id="43daa-145">深入瞭解網頁</span><span class="sxs-lookup"><span data-stu-id="43daa-145">Learn more about Web Pages</span></span>](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a><span data-ttu-id="43daa-146">Web Forms、MVC 和網頁的相關注意事項</span><span class="sxs-lookup"><span data-stu-id="43daa-146">Notes about Web Forms, MVC, and Web Pages</span></span>

<span data-ttu-id="43daa-147">這三種 ASP.NET 架構都是以 .NET 和 ASP.NET 的 .NET Framework 和共用核心功能為基礎。</span><span class="sxs-lookup"><span data-stu-id="43daa-147">All three ASP.NET frameworks are based on the .NET Framework and share core functionality of .NET and of ASP.NET.</span></span> <span data-ttu-id="43daa-148">比方說，所有的三個架構提供成員資格以基礎的登入安全性模型，並全部三種共用屬於 ASP.NET Core功能相同的設施管理要求、 處理工作階段，等等。</span><span class="sxs-lookup"><span data-stu-id="43daa-148">For example, all three frameworks offer a login security model based around membership, and all three share the same facilities for managing requests, handling sessions, and so on that are part of the core ASP.NET functionality.</span></span>

<span data-ttu-id="43daa-149">此外, 這三個架構並不完全獨立, 而選擇其中一個架構不會排除使用其他架構。</span><span class="sxs-lookup"><span data-stu-id="43daa-149">In addition, the three frameworks are not entirely independent, and choosing one does not preclude using another.</span></span> <span data-ttu-id="43daa-150">由於架構可以並存于相同的 web 應用程式中, 因此查看使用不同架構所撰寫之應用程式的個別元件並不常見。</span><span class="sxs-lookup"><span data-stu-id="43daa-150">Since the frameworks can coexist in the same web application, it's not uncommon to see individual components of applications written using different frameworks.</span></span> <span data-ttu-id="43daa-151">例如, 應用程式的客戶面向部分可能會在 MVC 中開發以優化標記, 而資料存取和系統管理部分則是在 Web form 中開發, 以利用資料控制和簡單的資料存取。</span><span class="sxs-lookup"><span data-stu-id="43daa-151">For example, customer-facing portions of an app might be developed in MVC to optimize the markup, while the data access and administrative portions are developed in Web Forms to take advantage of data controls and simple data access.</span></span>

## <a name="web-apis"></a><span data-ttu-id="43daa-152">Web API</span><span class="sxs-lookup"><span data-stu-id="43daa-152">Web APIs</span></span>

<span data-ttu-id="43daa-153">ASP.NET Web API 是一種架構, 可讓您輕鬆地建立可觸及各種用戶端 (包括瀏覽器和行動裝置) 的 HTTP 服務。</span><span class="sxs-lookup"><span data-stu-id="43daa-153">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="43daa-154">ASP.NET Web 應用程式開發介面是在 .NET Framework 上建置 RESTful 應用程式的理想平台。</span><span class="sxs-lookup"><span data-stu-id="43daa-154">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

[<span data-ttu-id="43daa-155">深入瞭解 Web API</span><span class="sxs-lookup"><span data-stu-id="43daa-155">Learn more about Web API</span></span>](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a><span data-ttu-id="43daa-156">即時技術</span><span class="sxs-lookup"><span data-stu-id="43daa-156">Real-time technologies</span></span>

<span data-ttu-id="43daa-157">ASP.NET SignalR 是 ASP.NET 開發人員的新程式庫, 可讓您更輕鬆地開發即時 web 功能。</span><span class="sxs-lookup"><span data-stu-id="43daa-157">ASP.NET SignalR is a new library for ASP.NET developers that makes developing real-time web functionality easier.</span></span> <span data-ttu-id="43daa-158">SignalR 允許伺服器和用戶端之間的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="43daa-158">SignalR allows bi-directional communication between server and client.</span></span> <span data-ttu-id="43daa-159">伺服器可以隨時將內容推送至已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="43daa-159">Servers can push content to connected clients instantly as it becomes available.</span></span> <span data-ttu-id="43daa-160">SignalR 支援 Web 通訊端, 並會回到舊版瀏覽器的其他相容技術。</span><span class="sxs-lookup"><span data-stu-id="43daa-160">SignalR supports Web Sockets, and falls back to other compatible techniques for older browsers.</span></span> <span data-ttu-id="43daa-161">SignalR 包含用於連線管理的 Api (例如, 連線和中斷線上活動)、群組連接和授權。</span><span class="sxs-lookup"><span data-stu-id="43daa-161">SignalR includes APIs for connection management (for instance, connect and disconnect events), grouping connections, and authorization.</span></span>

[<span data-ttu-id="43daa-162">深入瞭解 SignalR</span><span class="sxs-lookup"><span data-stu-id="43daa-162">Learn more about SignalR</span></span>](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a><span data-ttu-id="43daa-163">行動應用程式和網站</span><span class="sxs-lookup"><span data-stu-id="43daa-163">Mobile apps and sites</span></span>

<span data-ttu-id="43daa-164">ASP.NET 可以使用 Web API 後端, 以及使用回應式設計架構 (例如 Twitter 啟動程式) 的行動網站, 來強大的原生行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="43daa-164">ASP.NET can power native mobile apps with a Web API back end, as well as mobile web sites using responsive design frameworks like Twitter Bootstrap.</span></span> <span data-ttu-id="43daa-165">如果您要建立原生行動應用程式, 您可以輕鬆地建立 JSON 型 Web API 來處理應用程式的資料存取、驗證和推播通知。</span><span class="sxs-lookup"><span data-stu-id="43daa-165">If you are building a native mobile app, it's easy to create a JSON-based Web API to handle data access, authentication, and push notifications for your app.</span></span> <span data-ttu-id="43daa-166">如果您要建立回應式行動網站, 您可以使用任何您偏好的 CSS 架構或開放式方格系統, 或選取功能強大的行動系統, 例如 jQuery Mobile 或 Sencha, 以及使用 PhoneGap 的絕佳行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="43daa-166">If you are building a responsive mobile site, you can use any CSS framework or open grid system you prefer, or select a powerful mobile system like jQuery Mobile or Sencha and great mobile applications with PhoneGap.</span></span>

[<span data-ttu-id="43daa-167">深入瞭解行動應用程式和網站開發</span><span class="sxs-lookup"><span data-stu-id="43daa-167">Learn more about mobile app and site development</span></span>](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a><span data-ttu-id="43daa-168">單一頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="43daa-168">Single-page applications</span></span>

<span data-ttu-id="43daa-169">ASP.NET 單頁應用程式 (SPA) 可協助您使用 HTML 5、CSS 3 和 JavaScript, 建立包含重大用戶端互動的應用程式。</span><span class="sxs-lookup"><span data-stu-id="43daa-169">ASP.NET Single Page Application (SPA) helps you build applications that include significant client-side interactions using HTML 5, CSS 3 and JavaScript.</span></span> <span data-ttu-id="43daa-170">Visual Studio 包含使用挖和 ASP.NET Web API 建立單一頁面應用程式的範本。</span><span class="sxs-lookup"><span data-stu-id="43daa-170">Visual Studio includes a template for building single page applications using knockout.js and ASP.NET Web API.</span></span> <span data-ttu-id="43daa-171">除了內建的 SPA 範本, 也提供以社區建立的 SPA 範本, 供您下載。</span><span class="sxs-lookup"><span data-stu-id="43daa-171">In addition to the built-in SPA template, community-created SPA templates are also available for download.</span></span>

[<span data-ttu-id="43daa-172">深入瞭解單一頁面應用程式開發</span><span class="sxs-lookup"><span data-stu-id="43daa-172">Learn more about single-page app development</span></span>](single-page-application/index.md)

## <a name="webhooks"></a><span data-ttu-id="43daa-173">WebHook</span><span class="sxs-lookup"><span data-stu-id="43daa-173">WebHooks</span></span>

<span data-ttu-id="43daa-174">Webhook 是輕量的 HTTP 模式, 提供簡單的 pub/sub 模型, 可將 Web Api 和 SaaS 服務串聯在一起。</span><span class="sxs-lookup"><span data-stu-id="43daa-174">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="43daa-175">當服務中發生事件時, 會以 HTTP POST 要求的形式將通知傳送給已註冊的訂閱者。</span><span class="sxs-lookup"><span data-stu-id="43daa-175">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="43daa-176">POST 要求包含事件的相關資訊, 讓接收者可以據以採取動作。</span><span class="sxs-lookup"><span data-stu-id="43daa-176">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="43daa-177">Webhook 是由大量服務所公開, 包括 Dropbox、GitHub、Instagram、MailChimp、PayPal、時差、Trello 等等。</span><span class="sxs-lookup"><span data-stu-id="43daa-177">WebHooks are exposed by a large number of services including Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello, and many more.</span></span> <span data-ttu-id="43daa-178">例如, WebHook 可能表示檔案在 Dropbox 中已變更, 或 GitHub 中的程式碼變更已認可, 或已在 PayPal 中起始付款, 或已在 Trello 中建立了卡片。</span><span class="sxs-lookup"><span data-stu-id="43daa-178">For example, a WebHook can indicate that a file has changed in Dropbox, or a code change has been committed in GitHub, or a payment has been initiated in PayPal, or a card has been created in Trello.</span></span>

[<span data-ttu-id="43daa-179">深入瞭解 Webhook</span><span class="sxs-lookup"><span data-stu-id="43daa-179">Learn more about WebHooks</span></span>](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
