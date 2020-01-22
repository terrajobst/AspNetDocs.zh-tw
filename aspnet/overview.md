---
uid: overview
title: ASP.NET 總覽 |Microsoft Docs
author: rick-anderson
description: ASP.NET 簡介，這是用來建立網站、web 應用程式和 web Api 的免費架構。
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: aa4f627bca99f0a7ffbbb53ea45ebdcf0850fd89
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519358"
---
# <a name="aspnet-overview"></a>ASP.NET 概觀

ASP.NET 是免費的 web 架構，可用於使用 HTML、CSS 和 JavaScript 建立絕佳的網站和 web 應用程式。 您也可以建立 Web Api，並使用 Web 通訊端等即時技術。

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)是 ASP.NET 的替代方案。  請參閱[如何在 ASP.NET 和 ASP.NET Core 之間選擇的指引](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)。

## <a name="get-started"></a>開始使用

安裝[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019)的社區版，這是 Windows 上 ASP.NET 的免費 IDE。

## <a name="websites-and-web-applications"></a>網站和 web 應用程式

 ASP.NET 提供三種建立 web 應用程式的架構： Web Forms、ASP.NET MVC 和 ASP.NET Web Pages。 這三種架構都是穩定且成熟的，而且您可以使用其中任何一個來建立絕佳的 web 應用程式。 無論您選擇何種架構，都能取得所有 ASP.NET 的優點和功能。

每個架構的目標都是不同的開發樣式。 您所選擇的是取決於程式設計資產的組合（知識、技能和開發經驗）、您所建立的應用程式類型，以及您熟悉的開發方法。

以下是每個架構的總覽，以及如何在兩者之間進行選擇的一些概念。 如果您偏好影片簡介，請參閱[建立具有 ASP.NET 的網站](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET)和[什麼是 Web 工具？](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | 如果您的經驗 | 開發風格 | 專業知識 |
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web Form | Win Forms，WPF，.NET | 使用封裝 HTML 標籤的豐富控制項庫進行快速開發 | 中等層級、先進的 RAD |
| MVC       | Ruby on Rails，.NET  | 完全掌控 HTML 標籤、程式碼和標記分隔，以及輕鬆撰寫測試。 適用于行動和單頁應用程式（SPA）的最佳選擇。 | 中等層級，先進 |
| Web Pages  | 傳統 ASP，PHP     | 將 HTML 標籤和您的程式碼一起放在同一個檔案中 | 新的、中等層級 |

### <a name="web-forms"></a>Web Form

透過 ASP.NET Web form，您可以使用熟悉的拖放、事件驅動模型來建立動態網站。 單一設計介面和數百個控制項和元件可讓您快速建置功能強大、可存取資料的 UI 導向網站。

[深入瞭解 Web Forms](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC 可讓您透過功能強大、以模式為準的方式建置動態網站，而明確找出關注點，並讓您完全掌控標記，進而順暢、靈活地進行開發作業。 ASP.NET MVC 有多項功能可用於快速、適用於 TDD 的開發，以建立採用最新 Web 標準的精密應用程式。

[深入瞭解 MVC](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET 網頁

ASP.NET Web Pages 和 Razor 語法提供快速、平易近人且輕量的方式，將伺服器程式碼與 HTML 結合以建立動態 Web 內容。 連接到資料庫、新增影片、連結至社交網站，以及包含更多的功能，可協助您建立符合最新 web 標準的美觀網站。

[深入瞭解網頁](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Web Forms、MVC 和網頁的相關注意事項

這三種 ASP.NET 架構都是以 .NET 和 ASP.NET 的 .NET Framework 和共用核心功能為基礎。 例如，這三個架構都會根據成員資格提供登入安全性模型，而這三個架構會共用相同的功能來管理要求、處理會話等等，這些都是核心 ASP.NET 功能的一部分。

此外，這三個架構並不完全獨立，而選擇其中一個架構不會排除使用其他架構。 由於架構可以並存于相同的 web 應用程式中，因此查看使用不同架構所撰寫之應用程式的個別元件並不常見。 例如，應用程式的客戶面向部分可能會在 MVC 中開發以優化標記，而資料存取和系統管理部分則是在 Web form 中開發，以利用資料控制和簡單的資料存取。

## <a name="web-apis"></a>Web API

ASP.NET Web API 是一個架構，可輕易建置 HTTP 服務並擴及廣大的用戶端範圍，包括瀏覽器和行動裝置。 ASP.NET Web API 是一個想理平台，用以 .NET Framework 基礎建置 RESTful 應用程式。

[深入了解 Web API (英文)](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>即時技術

ASP.NET SignalR 是 ASP.NET 開發人員的新程式庫，可讓您更輕鬆地開發即時 web 功能。 SignalR 允許伺服器和用戶端之間的雙向通訊。 伺服器可以隨時將內容推送至已連線的用戶端。 SignalR 支援 Web 通訊端，並會回到舊版瀏覽器的其他相容技術。 SignalR 包含用於連線管理的 Api （例如，連線和中斷線上活動）、群組連接和授權。

[深入瞭解 SignalR](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>行動應用程式和網站

ASP.NET 可以使用 Web API 後端，以及使用回應式設計架構（例如 Twitter 啟動程式）的行動網站，來強大的原生行動應用程式。 如果您要建立原生行動應用程式，您可以輕鬆地建立 JSON 型 Web API 來處理應用程式的資料存取、驗證和推播通知。 如果您要建立回應式行動網站，您可以使用任何您偏好的 CSS 架構或開放式方格系統，或選取功能強大的行動系統，例如 jQuery Mobile 或 Sencha，以及使用 PhoneGap 的絕佳行動應用程式。

[深入瞭解行動應用程式和網站開發](mobile/overview.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>單頁應用程式

ASP.NET 單頁應用程式（SPA）可協助您使用 HTML 5、CSS 3 和 JavaScript，建立包含重大用戶端互動的應用程式。 Visual Studio 包含使用挖和 ASP.NET Web API 建立單一頁面應用程式的範本。 除了內建的 SPA 範本，也提供以社區建立的 SPA 範本，供您下載。

[深入瞭解單一頁面應用程式開發](single-page-application/index.md)

## <a name="webhooks"></a>WebHook

Webhook 是輕量的 HTTP 模式，提供簡單的 pub/sub 模型，可將 Web Api 和 SaaS 服務串聯在一起。 當服務中發生事件時，會以 HTTP POST 要求的形式將通知傳送給已註冊的訂閱者。 POST 要求包含事件的相關資訊，讓接收者可以據以採取動作。

Webhook 是由大量服務所公開，包括 Dropbox、GitHub、Instagram、MailChimp、PayPal、時差、Trello 等等。 例如，WebHook 可能表示檔案在 Dropbox 中已變更，或 GitHub 中的程式碼變更已認可，或已在 PayPal 中起始付款，或已在 Trello 中建立了卡片。

[深入瞭解 Webhook](webhooks/index.md)

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
