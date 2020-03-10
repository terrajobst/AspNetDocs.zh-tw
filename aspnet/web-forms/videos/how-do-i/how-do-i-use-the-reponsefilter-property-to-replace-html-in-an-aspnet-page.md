---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[How Do I：]使用 [回應] 屬性來取代 ASP.NET 網頁中的 HTML |Microsoft Docs'
author: rick-anderson
description: 在這段影片中，Chris Pels 會示範如何使用回應. Filter 屬性來攔截並改變要傳送至頁面的 HTML。 首先，會建立範例頁面 。
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602813"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="737fb-104">[How Do I：]使用 [回應] 屬性來取代 ASP.NET 網頁中的 HTML</span><span class="sxs-lookup"><span data-stu-id="737fb-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>

<span data-ttu-id="737fb-105">依[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="737fb-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="737fb-106">在這段影片中，Chris Pels 會示範如何使用回應. Filter 屬性來攔截並改變要傳送至頁面的 HTML。</span><span class="sxs-lookup"><span data-stu-id="737fb-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="737fb-107">首先，會使用一些簡單的文字來建立範例頁面。</span><span class="sxs-lookup"><span data-stu-id="737fb-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="737fb-108">然後，會建立自訂資料流程類別，做為傳送至使用者瀏覽器之目前資料流程的取代資料流程。</span><span class="sxs-lookup"><span data-stu-id="737fb-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="737fb-109">在該自訂資料流程類別中，會從資料流程抓取頁面的內容、加以更改，然後寫出至回應資料流程。</span><span class="sxs-lookup"><span data-stu-id="737fb-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="737fb-110">在此自訂資料流程類別中，會自訂 Write 方法來取代基底回應資料流程中的 HTML，藉此改變傳送至使用者瀏覽器的內容。</span><span class="sxs-lookup"><span data-stu-id="737fb-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="737fb-111">最後，新的資料流程類別會指派給 回應 頁面中的 篩選 屬性，\_載入 事件，因此提供變更頁面內容的機制。</span><span class="sxs-lookup"><span data-stu-id="737fb-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="737fb-112">&#9654;觀看影片（13分鐘）</span><span class="sxs-lookup"><span data-stu-id="737fb-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
