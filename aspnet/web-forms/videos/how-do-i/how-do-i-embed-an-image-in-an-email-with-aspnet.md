---
uid: web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
title: '[How Do I：]使用 ASP.NET 在電子郵件中內嵌影像 |Microsoft Docs'
author: rick-anderson
description: Chris Pels 說明如何使用 ASP.NET 在電子郵件中內嵌影像。 他會建立一個 web 表單（具有 To、From、Subject 和 Body 的欄位），並使用 AlternateView 。
ms.author: riande
ms.date: 11/06/2008
ms.assetid: 424788ac-0a43-4063-99e7-db5aa4c66a9d
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
msc.type: video
ms.openlocfilehash: fce565c7746acaa10ef1cf68e3ed98e052cca43e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567939"
---
# <a name="how-do-i-embed-an-image-in-an-email-with-aspnet"></a><span data-ttu-id="df601-104">[How Do I：]使用 ASP.NET 在電子郵件中內嵌影像</span><span class="sxs-lookup"><span data-stu-id="df601-104">[How Do I:] Embed an Image in an Email with ASP.NET</span></span>

<span data-ttu-id="df601-105">依[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="df601-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="df601-106">Chris Pels 說明如何使用 ASP.NET 在電子郵件中內嵌影像。</span><span class="sxs-lookup"><span data-stu-id="df601-106">Chris Pels shows how to embed an image in an email with ASP.NET.</span></span> <span data-ttu-id="df601-107">他會建立一個 web 表單（具有 To、From、Subject 和 Body 的欄位），使用 AlternateView 類別來建立電子郵件的文字和 HTML 版本，將影像儲存在 LinkedResource 類別實例中，並內嵌在 HTML AlternateView 中。</span><span class="sxs-lookup"><span data-stu-id="df601-107">He creates a web form (with fields for To, From, Subject, and Body), uses the AlternateView class to create text and HTML versions of an email, stores an image in a LinkedResource class instance, embeds it in the HTML AlternateView.</span></span> <span data-ttu-id="df601-108">然後他將這兩個版本新增至 Send-mailmessage 物件，並傳送電子郵件兩次，先啟用 HTML 接收功能，然後再以純文字形式傳送。</span><span class="sxs-lookup"><span data-stu-id="df601-108">He then adds both versions to the MailMessage object and sends the email twice, first with HTML-receiving capabilities enabled and then as text-only.</span></span> <span data-ttu-id="df601-109">這兩個電子郵件訊息都會出現在 Outlook 中。</span><span class="sxs-lookup"><span data-stu-id="df601-109">Both email messages appear in Outlook.</span></span> <span data-ttu-id="df601-110">HTML 版本會顯示內嵌影像;文字版本不是。</span><span class="sxs-lookup"><span data-stu-id="df601-110">The HTML version shows the embedded image; the text version does not.</span></span>

[<span data-ttu-id="df601-111">&#9654;觀看影片（19分鐘）</span><span class="sxs-lookup"><span data-stu-id="df601-111">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-embed-an-image-in-an-email-with-aspnet)
