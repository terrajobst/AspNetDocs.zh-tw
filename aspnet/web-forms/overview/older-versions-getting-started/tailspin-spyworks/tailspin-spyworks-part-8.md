---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第8部分：最後的頁面、例外狀況處理和結論 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第8部分新增連絡人頁面、關於頁面和例外狀況 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586881"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="60b1b-104">第8部分：最後的頁面、例外狀況處理和結論</span><span class="sxs-lookup"><span data-stu-id="60b1b-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="60b1b-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="60b1b-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="60b1b-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="60b1b-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="60b1b-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="60b1b-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="60b1b-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="60b1b-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="60b1b-109">第8部分新增 [連絡人] 頁面、[關於] 頁面和例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="60b1b-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="60b1b-110">這就是數列的結論。</span><span class="sxs-lookup"><span data-stu-id="60b1b-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a><span data-ttu-id="60b1b-111">連絡人頁面（從 ASP.NET 傳送電子郵件）</span><span class="sxs-lookup"><span data-stu-id="60b1b-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="60b1b-112">建立名為 ContactUs 的新頁面</span><span class="sxs-lookup"><span data-stu-id="60b1b-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="60b1b-113">使用設計工具建立下列表單，採取特殊的備註，將 ToolkitScriptManager 和編輯器控制項包含在 AjaxControlToolkit 中。</span><span class="sxs-lookup"><span data-stu-id="60b1b-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="60b1b-114">。</span><span class="sxs-lookup"><span data-stu-id="60b1b-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="60b1b-115">按兩下 [提交] 按鈕，以在程式碼後置檔案中產生 click 事件處理常式，並執行方法以電子郵件傳送連絡人資訊。</span><span class="sxs-lookup"><span data-stu-id="60b1b-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="60b1b-116">這段程式碼需要您的 web.config 檔案在 configuration 區段中包含一個專案，以指定要用於傳送郵件的 SMTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="60b1b-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="60b1b-117">關於頁面</span><span class="sxs-lookup"><span data-stu-id="60b1b-117">About Page</span></span>

<span data-ttu-id="60b1b-118">建立名為 AboutUs 的頁面，並加入您喜歡的任何內容。</span><span class="sxs-lookup"><span data-stu-id="60b1b-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="60b1b-119">全域例外狀況處理常式</span><span class="sxs-lookup"><span data-stu-id="60b1b-119">Global Exception Handler</span></span>

<span data-ttu-id="60b1b-120">最後，在整個應用程式中，我們擲回了例外狀況，而在非預期的情況下，冷也會造成 web 應用程式中的未處理例外</span><span class="sxs-lookup"><span data-stu-id="60b1b-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="60b1b-121">我們永遠不希望對網站訪客顯示未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="60b1b-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="60b1b-122">除了是嚴重的使用者體驗未處理的例外狀況之外，也可能會造成安全性問題。</span><span class="sxs-lookup"><span data-stu-id="60b1b-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="60b1b-123">為了解決這個問題，我們將會執行全域例外狀況處理常式。</span><span class="sxs-lookup"><span data-stu-id="60b1b-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="60b1b-124">若要這麼做，請開啟 global.asax 檔案，並記下下列預先產生的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="60b1b-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="60b1b-125">加入程式碼以依照下列方式來執行應用程式\_錯誤處理常式。</span><span class="sxs-lookup"><span data-stu-id="60b1b-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="60b1b-126">然後，將名為 Error 的頁面加入至方案，並加入此標記程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="60b1b-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="60b1b-127">現在在頁面\_載入事件處理常式會從要求物件中解壓縮錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="60b1b-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="60b1b-128">結果</span><span class="sxs-lookup"><span data-stu-id="60b1b-128">Conclusion</span></span>

<span data-ttu-id="60b1b-129">我們已瞭解 ASP.NET WebForms 可讓您輕鬆地建立具有資料庫存取權、成員資格、AJAX 等的精密網站。</span><span class="sxs-lookup"><span data-stu-id="60b1b-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="60b1b-130">非常快速。</span><span class="sxs-lookup"><span data-stu-id="60b1b-130">pretty quickly.</span></span>

<span data-ttu-id="60b1b-131">希望本教學課程提供您開始建立自己的 ASP.NET WebForms 應用程式所需的工具！</span><span class="sxs-lookup"><span data-stu-id="60b1b-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="60b1b-132">上一篇</span><span class="sxs-lookup"><span data-stu-id="60b1b-132">Previous</span></span>](tailspin-spyworks-part-7.md)
