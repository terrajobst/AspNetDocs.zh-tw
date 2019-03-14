---
uid: web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
title: '[How Do i:]使用 ASP.NET 的電子郵件中內嵌影像 |Microsoft Docs'
author: rick-anderson
description: Chris Pels 將示範如何使用 ASP.NET 將影像內嵌在電子郵件。 他會建立 web form （使用的欄位，從主旨以及本文），會使用 AlternateView...
ms.author: riande
ms.date: 11/06/2008
ms.assetid: 424788ac-0a43-4063-99e7-db5aa4c66a9d
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
msc.type: video
ms.openlocfilehash: d046c988c060580b856fb65c90521c3a2815e760
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059685"
---
<a name="how-do-i-embed-an-image-in-an-email-with-aspnet"></a><span data-ttu-id="9b736-104">[How Do i:]使用 ASP.NET 的電子郵件中內嵌影像</span><span class="sxs-lookup"><span data-stu-id="9b736-104">[How Do I:] Embed an Image in an Email with ASP.NET</span></span>
====================
<span data-ttu-id="9b736-105">藉由[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="9b736-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="9b736-106">Chris Pels 將示範如何使用 ASP.NET 將影像內嵌在電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9b736-106">Chris Pels shows how to embed an image in an email with ASP.NET.</span></span> <span data-ttu-id="9b736-107">他會建立 web form （使用的欄位，從主旨以及本文），使用 AlternateView 類別來建立文件和電子郵件的 HTML 版本、 LinkedResource 類別執行個體中儲存映像，將其內嵌於 HTML AlternateView。</span><span class="sxs-lookup"><span data-stu-id="9b736-107">He creates a web form (with fields for To, From, Subject, and Body), uses the AlternateView class to create text and HTML versions of an email, stores an image in a LinkedResource class instance, embeds it in the HTML AlternateView.</span></span> <span data-ttu-id="9b736-108">他然後出來的 MailMessage 物件中加入這兩個版本，並將兩次，傳送電子郵件，第一次使用啟用的 HTML 接收功能，然後為純文字。</span><span class="sxs-lookup"><span data-stu-id="9b736-108">He then adds both versions to the MailMessage object and sends the email twice, first with HTML-receiving capabilities enabled and then as text-only.</span></span> <span data-ttu-id="9b736-109">這兩個電子郵件訊息會出現在 Outlook 中。</span><span class="sxs-lookup"><span data-stu-id="9b736-109">Both email messages appear in Outlook.</span></span> <span data-ttu-id="9b736-110">HTML 版本顯示內嵌的影像沒有文字版本。</span><span class="sxs-lookup"><span data-stu-id="9b736-110">The HTML version shows the embedded image; the text version does not.</span></span>

[<span data-ttu-id="9b736-111">&#9654;觀看影片 （19 分鐘）</span><span class="sxs-lookup"><span data-stu-id="9b736-111">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-embed-an-image-in-an-email-with-aspnet)