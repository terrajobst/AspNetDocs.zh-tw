---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[How Do I：]使用 ASP.NET 以非同步方式傳送電子郵件 |Microsoft Docs'
author: rick-anderson
description: 在這段影片中，Chris Pels 會示範如何使用 ASP.NET 中的系統 .Net. Mail 類別來傳送非同步電子郵件訊息。 首先，請參閱如何設定 web si 。
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: ea29823446cc1339003160bd3e945bde1af42473
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635699"
---
# <a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="db719-104">[How Do I：]使用 ASP.NET 以非同步方式傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="db719-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>

<span data-ttu-id="db719-105">依[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="db719-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="db719-106">在這段影片中，Chris Pels 會示範如何使用 ASP.NET 中的系統 .Net. Mail 類別來傳送非同步電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="db719-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="db719-107">首先，請參閱如何使用 web.config 檔案中的 &lt;mailSettings&gt; 元素，設定網站以傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="db719-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="db719-108">接下來，建立簡單的使用者介面來輸入電子郵件資訊。</span><span class="sxs-lookup"><span data-stu-id="db719-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="db719-109">然後學習如何建立使用 Send-mailmessage 類別，在頁面的程式碼後置中建立電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="db719-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="db719-110">在該程式中，會在傳送電子郵件之後，建立異步回呼的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="db719-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="db719-111">在事件處理常式中，請參閱如何使用 AsynchCompletedEventArgs 類別的實例，它會提供電子郵件傳送程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="db719-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="db719-112">最後，請以非同步方式傳送測試電子郵件，遵循 [偵錯工具] 模式中的步驟，並查看從程式收到的實際電子郵件。</span><span class="sxs-lookup"><span data-stu-id="db719-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="db719-113">&#9654;觀看影片（18分鐘）</span><span class="sxs-lookup"><span data-stu-id="db719-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
