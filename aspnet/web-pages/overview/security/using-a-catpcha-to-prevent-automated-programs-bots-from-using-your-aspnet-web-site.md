---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用 CAPTCHA 防止 Bot 使用您的 ASP.NET Web Razor）網站 |Microsoft Docs
author: microsoft
description: 本文說明如何使用 ReCaptcha （安全性措施）來防止自動化程式（bot）在 ASP.NET Web Pages （Razor）中執行工作 。
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547044"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="89cc2-103">使用 CAPTCHA 防止 Bot 使用您的 ASP.NET Web Razor）網站</span><span class="sxs-lookup"><span data-stu-id="89cc2-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="89cc2-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="89cc2-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="89cc2-105">本文說明如何使用 ReCaptcha （安全性措施）來防止自動化程式（bot）在 ASP.NET Web Pages （Razor）網站中執行工作。</span><span class="sxs-lookup"><span data-stu-id="89cc2-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="89cc2-106">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="89cc2-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="89cc2-107">如何將 CAPTCHA 測試新增至您的網站。</span><span class="sxs-lookup"><span data-stu-id="89cc2-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="89cc2-108">以下是文章中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="89cc2-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="89cc2-109">`ReCaptcha` helper。</span><span class="sxs-lookup"><span data-stu-id="89cc2-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="89cc2-110">本文中的資訊適用于 ASP.NET Web Pages 1.0 和 Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="89cc2-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="89cc2-111">關於 CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="89cc2-111">About CAPTCHAs</span></span>

<span data-ttu-id="89cc2-112">每當您讓使用者在您的網站中註冊，或只是輸入名稱和 URL （例如，針對 blog 留言），您可能會收到大量的假名稱。</span><span class="sxs-lookup"><span data-stu-id="89cc2-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="89cc2-113">這些通常是由自動化程式（bot）所留下，會嘗試在每個可以找到的網站中留下 Url。</span><span class="sxs-lookup"><span data-stu-id="89cc2-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="89cc2-114">（常見的動機是張貼產品的 Url 以供銷售。）</span><span class="sxs-lookup"><span data-stu-id="89cc2-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="89cc2-115">當使用者註冊或輸入其名稱和網站時，您可以使用*CAPTCHA*來驗證使用者，藉此確保使用者是真正的人員，而不是電腦程式。</span><span class="sxs-lookup"><span data-stu-id="89cc2-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="89cc2-116">CAPTCHA 代表完全自動化的公用 Turing 測試，以告訴電腦和人類的與眾不同之處。</span><span class="sxs-lookup"><span data-stu-id="89cc2-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="89cc2-117">CAPTCHA 是一種*挑戰-回應*測試，使用者會在這種情況中執行一些動作，讓人員可以輕鬆執行，而不需要執行自動化程式。</span><span class="sxs-lookup"><span data-stu-id="89cc2-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="89cc2-118">最常見的 CAPTCHA 類型是您會看到一些失真字母，並要求您輸入它們的位置。</span><span class="sxs-lookup"><span data-stu-id="89cc2-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="89cc2-119">（扭曲應該會讓 bot 難以破解字母）。</span><span class="sxs-lookup"><span data-stu-id="89cc2-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="89cc2-120">新增 ReCaptcha 測試</span><span class="sxs-lookup"><span data-stu-id="89cc2-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="89cc2-121">在 ASP.NET 網頁中，您可以使用 `ReCaptcha` helper 來呈現以 ReCaptcha 服務（[http://recaptcha.net](http://recaptcha.net)）為基礎的 CAPTCHA 測試。</span><span class="sxs-lookup"><span data-stu-id="89cc2-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="89cc2-122">`ReCaptcha` 協助程式會顯示兩個失真單字的影像，使用者必須在驗證頁面之前正確輸入。</span><span class="sxs-lookup"><span data-stu-id="89cc2-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="89cc2-123">使用者回應是由 ReCaptcha.Net 服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="89cc2-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="89cc2-124">在 ReCaptcha.Net （[http://recaptcha.net](http://recaptcha.net)）註冊您的網站。</span><span class="sxs-lookup"><span data-stu-id="89cc2-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="89cc2-125">當您完成註冊時，將會取得公開金鑰和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="89cc2-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="89cc2-126">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。</span><span class="sxs-lookup"><span data-stu-id="89cc2-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="89cc2-127">如果您還沒有 *\_AppStart. cshtml*檔案，請在網站的根資料夾中建立名為 *\_AppStart*的檔案。</span><span class="sxs-lookup"><span data-stu-id="89cc2-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="89cc2-128">在 *\_AppStart*中新增下列 `Recaptcha` 協助程式設定：</span><span class="sxs-lookup"><span data-stu-id="89cc2-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="89cc2-129">使用您自己的公開和私密金鑰來設定 `PublicKey` 和 `PrivateKey` 屬性。</span><span class="sxs-lookup"><span data-stu-id="89cc2-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="89cc2-130">儲存 *\_AppStart* ，並將它關閉。</span><span class="sxs-lookup"><span data-stu-id="89cc2-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="89cc2-131">在網站的根資料夾中，建立名為*Recaptcha*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="89cc2-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="89cc2-132">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="89cc2-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="89cc2-133">在瀏覽器中執行*Recaptcha。*</span><span class="sxs-lookup"><span data-stu-id="89cc2-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="89cc2-134">如果 `PrivateKey` 值有效，頁面就會顯示 [ReCaptcha] 控制項和一個按鈕。</span><span class="sxs-lookup"><span data-stu-id="89cc2-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="89cc2-135">如果您未在 *\_AppStart*中全域設定金鑰，此頁面會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="89cc2-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="89cc2-136">輸入測試的文字。</span><span class="sxs-lookup"><span data-stu-id="89cc2-136">Enter the words for the test.</span></span> <span data-ttu-id="89cc2-137">如果您通過 ReCaptcha 測試，就會看到該效果的訊息。</span><span class="sxs-lookup"><span data-stu-id="89cc2-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="89cc2-138">否則，您會看到錯誤訊息，而且 ReCaptcha 控制項會重新顯示。</span><span class="sxs-lookup"><span data-stu-id="89cc2-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="89cc2-139">如果您的電腦位於使用 proxy 伺服器的網域上，您可能需要設定*web.config*檔案的 `defaultproxy` 元素。</span><span class="sxs-lookup"><span data-stu-id="89cc2-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="89cc2-140">下列範例顯示已設定 `defaultproxy` 專案的*web.config*檔案，讓 ReCaptcha 服務能夠正常執行。</span><span class="sxs-lookup"><span data-stu-id="89cc2-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="89cc2-141">其他資源</span><span class="sxs-lookup"><span data-stu-id="89cc2-141">Additional Resources</span></span>

- [<span data-ttu-id="89cc2-142">針對 ASP.NET Web Pages 網站自訂全網站行為</span><span class="sxs-lookup"><span data-stu-id="89cc2-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="89cc2-143">ReCaptcha 網站</span><span class="sxs-lookup"><span data-stu-id="89cc2-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
