---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: 從 ASP.NET Web Pages （Razor）網站傳送電子郵件 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何從網站傳送自動化的電子郵件訊息。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634712"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="8bc44-103">從 ASP.NET Web Pages （Razor）網站傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="8bc44-103">Sending Email from an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="8bc44-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8bc44-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8bc44-105">本文說明當您使用 ASP.NET Web Pages （Razor）時，如何從網站傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="8bc44-105">This article explains how to send an email message from a website when you use ASP.NET Web Pages (Razor).</span></span>
> 
> <span data-ttu-id="8bc44-106">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="8bc44-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="8bc44-107">如何從您的網站傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="8bc44-107">How to send an email message from your website.</span></span>
> - <span data-ttu-id="8bc44-108">如何將檔案附加至電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="8bc44-108">How to attach a file to an email message.</span></span>
> 
> <span data-ttu-id="8bc44-109">這是本文中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="8bc44-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="8bc44-110">`WebMail` helper。</span><span class="sxs-lookup"><span data-stu-id="8bc44-110">The `WebMail` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8bc44-111">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="8bc44-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="8bc44-112">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="8bc44-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="8bc44-113">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="8bc44-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a><span data-ttu-id="8bc44-114">從您的網站傳送電子郵件訊息</span><span class="sxs-lookup"><span data-stu-id="8bc44-114">Sending Email Messages from Your Website</span></span>

<span data-ttu-id="8bc44-115">您可能需要從您的網站傳送電子郵件的原因有很多種。</span><span class="sxs-lookup"><span data-stu-id="8bc44-115">There are all sorts of reasons why you might need to send email from your website.</span></span> <span data-ttu-id="8bc44-116">您可能會傳送確認訊息給使用者，或者您可能會將通知傳送給自己（例如，新使用者已註冊）。`WebMail` 協助程式可讓您輕鬆地傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="8bc44-116">You might send confirmation messages to users, or you might send notifications to yourself (for example, that a new user has registered.) The `WebMail` helper makes it easy for you to send email.</span></span>

<span data-ttu-id="8bc44-117">若要使用 `WebMail` helper，您必須具有 SMTP 伺服器的存取權。</span><span class="sxs-lookup"><span data-stu-id="8bc44-117">To use the `WebMail` helper, you have to have access to an SMTP server.</span></span> <span data-ttu-id="8bc44-118">（SMTP 代表*簡單郵件傳輸通訊協定*）。SMTP 伺服器是一種電子郵件伺服器，只會將郵件轉寄給收&#8212;件者的伺服器，它是電子郵件的輸出端。</span><span class="sxs-lookup"><span data-stu-id="8bc44-118">(SMTP stands for *Simple Mail Transfer Protocol*.) An SMTP server is an email server that only forwards messages to the recipient's server &#8212; it's the outbound side of email.</span></span> <span data-ttu-id="8bc44-119">如果您使用網站的主控提供者，他們可能會設定電子郵件給您，而他們可以告訴您 SMTP 伺服器名稱的內容。</span><span class="sxs-lookup"><span data-stu-id="8bc44-119">If you use a hosting provider for your website, they probably set you up with email and they can tell you what your SMTP server name is.</span></span> <span data-ttu-id="8bc44-120">如果您在公司網路內工作，系統管理員或您的 IT 部門通常可以提供您可使用之 SMTP 伺服器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8bc44-120">If you're working inside a corporate network, an administrator or your IT department can usually give you the information about an SMTP server that you can use.</span></span> <span data-ttu-id="8bc44-121">如果您在家工作，甚至可以使用您一般的電子郵件提供者來進行測試，以告訴您其 SMTP 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="8bc44-121">If you're working at home, you might even be able to test using your ordinary email provider, who can tell you the name of their SMTP server.</span></span> <span data-ttu-id="8bc44-122">您通常需要：</span><span class="sxs-lookup"><span data-stu-id="8bc44-122">You typically need:</span></span>

- <span data-ttu-id="8bc44-123">SMTP 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="8bc44-123">The name of the SMTP server.</span></span>
- <span data-ttu-id="8bc44-124">埠號碼。</span><span class="sxs-lookup"><span data-stu-id="8bc44-124">The port number.</span></span> <span data-ttu-id="8bc44-125">這幾乎都是25。</span><span class="sxs-lookup"><span data-stu-id="8bc44-125">This is almost always 25.</span></span> <span data-ttu-id="8bc44-126">不過，您的 ISP 可能會要求您使用埠587。</span><span class="sxs-lookup"><span data-stu-id="8bc44-126">However, your ISP may require you to use port 587.</span></span> <span data-ttu-id="8bc44-127">如果您使用安全通訊端層（SSL）來傳送電子郵件，您可能需要不同的埠。</span><span class="sxs-lookup"><span data-stu-id="8bc44-127">If you are using secure sockets layer (SSL) for email, you might need a different port.</span></span> <span data-ttu-id="8bc44-128">請洽詢您的電子郵件提供者。</span><span class="sxs-lookup"><span data-stu-id="8bc44-128">Check with your email provider.</span></span>
- <span data-ttu-id="8bc44-129">認證（使用者名稱、密碼）。</span><span class="sxs-lookup"><span data-stu-id="8bc44-129">Credentials (user name, password).</span></span>

<span data-ttu-id="8bc44-130">在此程式中，您會建立兩個頁面。</span><span class="sxs-lookup"><span data-stu-id="8bc44-130">In this procedure, you create two pages.</span></span> <span data-ttu-id="8bc44-131">第一頁的表單可讓使用者輸入描述，就像是填入技術支援表單一樣。</span><span class="sxs-lookup"><span data-stu-id="8bc44-131">The first page has a form that lets users enter a description, as if they were filling in a technical-support form.</span></span> <span data-ttu-id="8bc44-132">第一頁會將其資訊提交至第二頁。</span><span class="sxs-lookup"><span data-stu-id="8bc44-132">The first page submits its information to a second page.</span></span> <span data-ttu-id="8bc44-133">在第二頁中，程式碼會解壓縮使用者的資訊，並傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="8bc44-133">In the second page, code extracts the user's information and sends an email message.</span></span> <span data-ttu-id="8bc44-134">它也會顯示一則訊息，確認已收到問題報告。</span><span class="sxs-lookup"><span data-stu-id="8bc44-134">It also displays a message confirming that the problem report has been received.</span></span>

![[影像]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> <span data-ttu-id="8bc44-136">為了讓此範例保持簡單，程式碼會在您使用它的頁面中，初始化 `WebMail` helper。</span><span class="sxs-lookup"><span data-stu-id="8bc44-136">To keep this example simple, the code initializes the `WebMail` helper right in the page where you use it.</span></span> <span data-ttu-id="8bc44-137">不過，對於真實的網站而言，將初始化程式碼放在全域檔案中是較好的主意，以便為網站中的所有檔案初始化 `WebMail` helper。</span><span class="sxs-lookup"><span data-stu-id="8bc44-137">However, for real websites, it's a better idea to put initialization code like this in a global file, so that you initialize the `WebMail` helper for all files in your website.</span></span> <span data-ttu-id="8bc44-138">如需詳細資訊，請參閱針對[ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)。</span><span class="sxs-lookup"><span data-stu-id="8bc44-138">For more information, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).</span></span>

1. <span data-ttu-id="8bc44-139">建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="8bc44-139">Create a new website.</span></span>
2. <span data-ttu-id="8bc44-140">新增名為*EmailRequest*的新頁面，並新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="8bc44-140">Add a new page named *EmailRequest.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    <span data-ttu-id="8bc44-141">請注意，form 元素的 `action` 屬性已設定為*ProcessRequest*。</span><span class="sxs-lookup"><span data-stu-id="8bc44-141">Notice that the `action` attribute of the form element has been set to *ProcessRequest.cshtml*.</span></span> <span data-ttu-id="8bc44-142">這表示表單會提交至該頁面，而不是回到目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="8bc44-142">This means that the form will be submitted to that page instead of back to the current page.</span></span>
3. <span data-ttu-id="8bc44-143">將名為*ProcessRequest*的新頁面新增至網站，並新增下列程式碼和標記：</span><span class="sxs-lookup"><span data-stu-id="8bc44-143">Add a new page named *ProcessRequest.cshtml* to the website and add the following code and markup:</span></span>   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    <span data-ttu-id="8bc44-144">在程式碼中，您會取得已提交至頁面之表單欄位的值。</span><span class="sxs-lookup"><span data-stu-id="8bc44-144">In the code, you get the values of the form fields that were submitted to the page.</span></span> <span data-ttu-id="8bc44-145">接著，您可以呼叫 `WebMail` helper 的 `Send` 方法來建立和傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="8bc44-145">You then call the `WebMail` helper's `Send` method to create and send the email message.</span></span> <span data-ttu-id="8bc44-146">在此情況下，要使用的值是由文字所組成，您可以使用從表單提交的值進行串連。</span><span class="sxs-lookup"><span data-stu-id="8bc44-146">In this case, the values to use are made up of text that you concatenate with the values that were submitted from the form.</span></span>

    <span data-ttu-id="8bc44-147">此頁面的程式碼位於 `try/catch` 區塊內。</span><span class="sxs-lookup"><span data-stu-id="8bc44-147">The code for this page is inside a `try/catch` block.</span></span> <span data-ttu-id="8bc44-148">如果因任何原因而無法傳送電子郵件（例如設定不正確），則 `catch` 區塊中的程式碼會執行，並將 `errorMessage` 變數設定為已發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="8bc44-148">If for any reason the attempt to send an email doesn't work (for example, the settings aren't right), the code in the `catch` block runs and sets the `errorMessage` variable to the error that has occurred.</span></span> <span data-ttu-id="8bc44-149">（如需 `try/catch` 區塊或 `<text>` 標記的詳細資訊，請參閱[使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)）。</span><span class="sxs-lookup"><span data-stu-id="8bc44-149">(For more information about `try/catch` blocks or the `<text>` tag, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span></span>

    <span data-ttu-id="8bc44-150">在頁面主體中，如果 `errorMessage` 變數是空的（預設值），則使用者會看到電子郵件訊息已傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="8bc44-150">In the body of the page, if the `errorMessage` variable is empty (the default), the user sees a message that the email message has been sent.</span></span> <span data-ttu-id="8bc44-151">如果 `errorMessage` 變數設定為 true，則使用者會看到訊息，指出傳送訊息時發生問題。</span><span class="sxs-lookup"><span data-stu-id="8bc44-151">If the `errorMessage` variable is set to true, the user sees a message that there's been a problem sending the message.</span></span>

    <span data-ttu-id="8bc44-152">請注意，在顯示錯誤訊息的頁面部分中，有一個額外的測試： `if(debuggingFlag)`。</span><span class="sxs-lookup"><span data-stu-id="8bc44-152">Notice that in the portion of the page that displays an error message, there's an additional test: `if(debuggingFlag)`.</span></span> <span data-ttu-id="8bc44-153">如果您在傳送電子郵件時遇到問題，您可以將此變數設定為 true。</span><span class="sxs-lookup"><span data-stu-id="8bc44-153">This is a variable that you can set to true if you're having trouble sending email.</span></span> <span data-ttu-id="8bc44-154">當 `debuggingFlag` 為 true，且傳送電子郵件時發生問題時，會顯示額外的錯誤訊息，顯示當 ASP.NET 嘗試傳送電子郵件訊息時回報的內容。</span><span class="sxs-lookup"><span data-stu-id="8bc44-154">When `debuggingFlag` is true, and if there's a problem sending email, an additional error message is displayed that shows whatever ASP.NET has reported when it tried to send the email message.</span></span> <span data-ttu-id="8bc44-155">公平警告：不過，ASP.NET 在無法傳送電子郵件訊息時回報的錯誤訊息可以是一般的。</span><span class="sxs-lookup"><span data-stu-id="8bc44-155">Fair warning, though: the error messages that ASP.NET reports when it can't send an email message can be generic.</span></span> <span data-ttu-id="8bc44-156">例如，如果 ASP.NET 無法連線到 SMTP 伺服器（例如，因為您在伺服器名稱中發生錯誤），則會 `Failure sending mail`錯誤。</span><span class="sxs-lookup"><span data-stu-id="8bc44-156">For example, if ASP.NET can't contact the SMTP server (for example, because you made an error in the server name), the error is `Failure sending mail`.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="8bc44-157">**重要事項**當您從例外狀況物件（在程式碼中`ex`）收到錯誤訊息時，*請不要定期將*該訊息傳遞給使用者。</span><span class="sxs-lookup"><span data-stu-id="8bc44-157">**Important** When you get an error message from an exception object (`ex` in the code), do *not* routinely pass that message through to users.</span></span> <span data-ttu-id="8bc44-158">例外狀況物件通常會包含使用者不應該看到的資訊，甚至可能是安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="8bc44-158">Exception objects often include information that users should not see and that can even be a security vulnerability.</span></span> <span data-ttu-id="8bc44-159">這就是為什麼這段程式碼包含變數 `debuggingFlag`，做為用來顯示錯誤訊息的參數，以及為什麼變數預設會設定為 false。</span><span class="sxs-lookup"><span data-stu-id="8bc44-159">That's why this code includes the variable `debuggingFlag` that's used as a switch to display the error message, and why the variable by default is set to false.</span></span> <span data-ttu-id="8bc44-160">只有當您在傳送電子郵件時遇到問題，而且需要進行偵錯工具時，*才*應該將該變數設定為 true （因此會顯示錯誤訊息）。</span><span class="sxs-lookup"><span data-stu-id="8bc44-160">You should set that variable to true (and therefore display the error message) *only* if you're having a problem with sending email and you need to debug.</span></span> <span data-ttu-id="8bc44-161">一旦您已修正任何問題，請將 `debuggingFlag` 設回 false。</span><span class="sxs-lookup"><span data-stu-id="8bc44-161">Once you have fixed any problems, set `debuggingFlag` back to false.</span></span>

    <span data-ttu-id="8bc44-162">修改程式碼中的下列電子郵件相關設定：</span><span class="sxs-lookup"><span data-stu-id="8bc44-162">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="8bc44-163">將 `your-SMTP-host` 設定為您可以存取的 SMTP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="8bc44-163">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="8bc44-164">將 `your-user-name-here` 設定為 SMTP 伺服器帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8bc44-164">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="8bc44-165">將 `your-account-password` 設定為 SMTP 伺服器帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="8bc44-165">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="8bc44-166">將 `your-email-address-here` 設定為您自己的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8bc44-166">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="8bc44-167">這是傳送訊息的來源電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8bc44-167">This is the email address that the message is sent from.</span></span> <span data-ttu-id="8bc44-168">（有些電子郵件提供者不會讓您指定不同的 `From` 位址，而且會使用您的使用者名稱作為 `From` 位址）。</span><span class="sxs-lookup"><span data-stu-id="8bc44-168">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a><span data-ttu-id="8bc44-169">正在設定電子郵件設定</span><span class="sxs-lookup"><span data-stu-id="8bc44-169">Configuring Email Settings</span></span>
     > 
     > <span data-ttu-id="8bc44-170">有時可能會有一項挑戰，就是確定您有適當的 SMTP 伺服器、埠號碼等等設定。</span><span class="sxs-lookup"><span data-stu-id="8bc44-170">It can be a challenge sometimes to make sure you have the right settings for the SMTP server, port number, and so on.</span></span> <span data-ttu-id="8bc44-171">下列提供幾個秘訣：</span><span class="sxs-lookup"><span data-stu-id="8bc44-171">Here are a few tips:</span></span>
     > 
     > - <span data-ttu-id="8bc44-172">SMTP 伺服器名稱通常類似 `smtp.provider.com` 或 `smtp.provider.net`。</span><span class="sxs-lookup"><span data-stu-id="8bc44-172">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="8bc44-173">不過，如果您將網站發佈至主機服務提供者，該點的 SMTP 伺服器名稱可能會 `localhost`。</span><span class="sxs-lookup"><span data-stu-id="8bc44-173">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="8bc44-174">這是因為在您已發佈，且您的網站在提供者的伺服器上執行之後，電子郵件伺服器可能會從您的應用程式觀點來看。</span><span class="sxs-lookup"><span data-stu-id="8bc44-174">This is because after you've published and your site is running on the provider's server, the email server might be local from the perspective of your application.</span></span> <span data-ttu-id="8bc44-175">伺服器名稱的這項變更可能表示您必須在發佈程式中變更 SMTP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="8bc44-175">This change in server names might mean you have to change the SMTP server name as part of your publishing process.</span></span>
     > - <span data-ttu-id="8bc44-176">埠號碼通常是25。</span><span class="sxs-lookup"><span data-stu-id="8bc44-176">The port number is usually 25.</span></span> <span data-ttu-id="8bc44-177">不過，某些提供者會要求您使用埠587或其他通訊埠。</span><span class="sxs-lookup"><span data-stu-id="8bc44-177">However, some providers require you to use port 587 or some other port.</span></span>
     > - <span data-ttu-id="8bc44-178">請確定您使用正確的認證。</span><span class="sxs-lookup"><span data-stu-id="8bc44-178">Make sure that you use the right credentials.</span></span> <span data-ttu-id="8bc44-179">如果您已將您的網站發佈至主控提供者，請使用提供者特別指出的認證做為電子郵件。</span><span class="sxs-lookup"><span data-stu-id="8bc44-179">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="8bc44-180">這些可能與您用來發佈的認證不同。</span><span class="sxs-lookup"><span data-stu-id="8bc44-180">These might be different from the credentials you use to publish.</span></span>
     > - <span data-ttu-id="8bc44-181">有時候您不需要認證。</span><span class="sxs-lookup"><span data-stu-id="8bc44-181">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="8bc44-182">如果您是使用個人 ISP 傳送電子郵件，您的電子郵件提供者可能已經知道您的認證。</span><span class="sxs-lookup"><span data-stu-id="8bc44-182">If you're sending email using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="8bc44-183">發行之後，您可能需要使用與在本機電腦上測試時不同的認證。</span><span class="sxs-lookup"><span data-stu-id="8bc44-183">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
     > - <span data-ttu-id="8bc44-184">如果您的電子郵件提供者使用加密，您必須將 `WebMail.EnableSsl` 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="8bc44-184">If your email provider uses encryption, you have to set `WebMail.EnableSsl` to `true`.</span></span>
4. <span data-ttu-id="8bc44-185">在瀏覽器中執行*EmailRequest。*</span><span class="sxs-lookup"><span data-stu-id="8bc44-185">Run the *EmailRequest.cshtml* page in a browser.</span></span> <span data-ttu-id="8bc44-186">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）</span><span class="sxs-lookup"><span data-stu-id="8bc44-186">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
5. <span data-ttu-id="8bc44-187">輸入您的名稱和問題描述，然後按一下 [**提交**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bc44-187">Enter your name and a problem description, and then click the **Submit** button.</span></span> <span data-ttu-id="8bc44-188">系統會將您重新導向至*ProcessRequest* ，以確認您的訊息，並傳送電子郵件訊息給您。</span><span class="sxs-lookup"><span data-stu-id="8bc44-188">You're redirected to the *ProcessRequest.cshtml* page, which confirms your message and which sends you an email message.</span></span> 

    ![[影像]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a><span data-ttu-id="8bc44-190">使用電子郵件傳送檔案</span><span class="sxs-lookup"><span data-stu-id="8bc44-190">Sending a File Using Email</span></span>

<span data-ttu-id="8bc44-191">您也可以傳送附加至電子郵件訊息的檔案。</span><span class="sxs-lookup"><span data-stu-id="8bc44-191">You can also send files that are attached to email messages.</span></span> <span data-ttu-id="8bc44-192">在這個程式中，您會建立一個文字檔和兩個 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="8bc44-192">In this procedure, you create a text file and two HTML pages.</span></span> <span data-ttu-id="8bc44-193">您將使用文字檔做為電子郵件附件。</span><span class="sxs-lookup"><span data-stu-id="8bc44-193">You'll use the text file as an email attachment.</span></span>

1. <span data-ttu-id="8bc44-194">在網站中，加入新的文字檔，並將它命名為*myfile.txt .txt*。</span><span class="sxs-lookup"><span data-stu-id="8bc44-194">In the website, add a new text file and name it *MyFile.txt*.</span></span>
2. <span data-ttu-id="8bc44-195">複製下列文字並貼到檔案中：</span><span class="sxs-lookup"><span data-stu-id="8bc44-195">Copy the following text and paste it in the file:</span></span> 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. <span data-ttu-id="8bc44-196">建立名為*SendFile*的頁面，並新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="8bc44-196">Create a page named *SendFile.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. <span data-ttu-id="8bc44-197">建立名為*ProcessFile*的頁面，並新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="8bc44-197">Create a page named *ProcessFile.cshtml* and add the following markup:</span></span> 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. <span data-ttu-id="8bc44-198">在範例的程式碼中修改下列電子郵件相關設定：</span><span class="sxs-lookup"><span data-stu-id="8bc44-198">Modify the following email related settings in the code from the example:</span></span>

    - <span data-ttu-id="8bc44-199">將 `your-SMTP-host` 設定為您可以存取的 SMTP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="8bc44-199">Set `your-SMTP-host` to the name of an SMTP server that you have access to.</span></span>
    - <span data-ttu-id="8bc44-200">將 `your-user-name-here` 設定為 SMTP 伺服器帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8bc44-200">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="8bc44-201">將 `your-email-address-here` 設定為您自己的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8bc44-201">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="8bc44-202">這是傳送訊息的來源電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8bc44-202">This is the email address that the message is sent from.</span></span>
    - <span data-ttu-id="8bc44-203">將 `your-account-password` 設定為 SMTP 伺服器帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="8bc44-203">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="8bc44-204">將 `target-email-address-here` 設定為您自己的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8bc44-204">Set `target-email-address-here` to your own email address.</span></span> <span data-ttu-id="8bc44-205">（如前所述，您通常會將電子郵件傳送給其他人，但若要進行測試，您可以將它傳送給自己。）</span><span class="sxs-lookup"><span data-stu-id="8bc44-205">(As before, you'd normally send an email to someone else, but for testing, you can send it to yourself.)</span></span>
6. <span data-ttu-id="8bc44-206">在瀏覽器中執行*SendFile。*</span><span class="sxs-lookup"><span data-stu-id="8bc44-206">Run the *SendFile.cshtml* page in a browser.</span></span>
7. <span data-ttu-id="8bc44-207">輸入您的名稱、主旨行，以及要附加的文字檔名稱（*myfile.txt .txt*）。</span><span class="sxs-lookup"><span data-stu-id="8bc44-207">Enter your name, a subject line, and the name of the text file to attach (*MyFile.txt*).</span></span>
8. <span data-ttu-id="8bc44-208">按一下 `Submit` 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bc44-208">Click the `Submit` button.</span></span> <span data-ttu-id="8bc44-209">就像之前一樣，您會被重新導向至*ProcessFile* ，以確認您的訊息，並將附加的檔案傳送給您電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="8bc44-209">As before, you're redirected to the *ProcessFile.cshtml* page, which confirms your message and which sends you an email message with the attached file.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="8bc44-210">其他資源</span><span class="sxs-lookup"><span data-stu-id="8bc44-210">Additional Resources</span></span>

- [<span data-ttu-id="8bc44-211">ASP.NET Web Pages (Razor) 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="8bc44-211">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)
- [<span data-ttu-id="8bc44-212">簡易郵件傳送通訊協定</span><span class="sxs-lookup"><span data-stu-id="8bc44-212">Simple Mail Transfer Protocol</span></span>](https://msdn.microsoft.com/library/aa480435.aspx)
- [<span data-ttu-id="8bc44-213">針對 ASP.NET Web Pages 自訂全網站行為</span><span class="sxs-lookup"><span data-stu-id="8bc44-213">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
