---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[How Do I：]選擇 AJAX 頁面更新的方法嗎？ | Microsoft Docs'
author: JoeStagner
description: 在這段影片中，Joe Stagner 會比較在 ASP.NET 應用程式中執行 AJAX 樣式頁面更新的兩個主要方法。 第一種方法是使用 Upd 。
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 56e3ebfbe0b5af4234791136725de79e38171cc1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523664"
---
# <a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="0a99f-105">[How Do I：]選擇 AJAX 頁面更新的方法嗎？</span><span class="sxs-lookup"><span data-stu-id="0a99f-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>

<span data-ttu-id="0a99f-106">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="0a99f-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="0a99f-107">在這段影片中，Joe Stagner 會比較在 ASP.NET 應用程式中執行 AJAX 樣式頁面更新的兩個主要方法。</span><span class="sxs-lookup"><span data-stu-id="0a99f-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="0a99f-108">第一種方法是使用 UpdatePanel，其中不需要在用戶端或伺服器端撰寫任何額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0a99f-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="0a99f-109">使用 UpdatePanel 的優點是所有專案都會自動運作。</span><span class="sxs-lookup"><span data-stu-id="0a99f-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="0a99f-110">其負面影響是，在用戶端需要將大量資料包含在 AJAX 要求和回應中，而且在伺服器上，它需要執行完整的頁面生命週期。</span><span class="sxs-lookup"><span data-stu-id="0a99f-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="0a99f-111">第二種方法是使用網路回呼，也就是必須在用戶端和伺服器端撰寫額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0a99f-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="0a99f-112">使用網路回呼的優點是，在用戶端上，它只需要在 AJAX 要求和回應中包含非常少的資料，而在伺服器上只需要執行所呼叫的服務方法。</span><span class="sxs-lookup"><span data-stu-id="0a99f-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="0a99f-113">Penality 是撰寫必要程式碼所需的時間和工作。</span><span class="sxs-lookup"><span data-stu-id="0a99f-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="0a99f-114">Joe 藉由討論在 AJAX 樣式頁面更新的兩個主要方法之間進行選擇時，您應該考慮的事項。</span><span class="sxs-lookup"><span data-stu-id="0a99f-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="0a99f-115">（這段影片會使用[如何開始使用 ASP.NET ajax](how-do-i-get-started-with-aspnet-ajax.md)影片中的程式碼，以及[如何使用 ASP.NET Ajax 來進行用戶端網路回呼](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md)）。</span><span class="sxs-lookup"><span data-stu-id="0a99f-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="0a99f-116">&#9654;觀看影片（11分鐘）</span><span class="sxs-lookup"><span data-stu-id="0a99f-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="0a99f-117">[上一頁](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [下一頁](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="0a99f-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>
