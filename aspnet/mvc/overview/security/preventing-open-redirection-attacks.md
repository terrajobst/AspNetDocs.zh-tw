---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 防止開啟重新導向攻擊C#（） |Microsoft Docs
author: jongalloway
description: 本教學課程說明如何在 ASP.NET MVC 應用程式中防止開啟重新導向攻擊。 本教學課程將討論已進行的變更 。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538168"
---
# <a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="fdf6f-104">預防開啟重新導向攻擊 (C#)</span><span class="sxs-lookup"><span data-stu-id="fdf6f-104">Preventing Open Redirection Attacks (C#)</span></span>

<span data-ttu-id="fdf6f-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="fdf6f-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="fdf6f-106">本教學課程說明如何在 ASP.NET MVC 應用程式中防止開啟重新導向攻擊。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="fdf6f-107">本教學課程會討論在 ASP.NET MVC 3 的 AccountController 中所做的變更，並示範如何將這些變更套用至現有的 ASP.NET MVC 1.0 和2應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>

## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="fdf6f-108">什麼是開放式重新導向攻擊？</span><span class="sxs-lookup"><span data-stu-id="fdf6f-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="fdf6f-109">重新導向至透過要求（例如 querystring 或表單資料）指定之 URL 的任何 web 應用程式，可能會遭到篡改，以將使用者重新導向至外部的惡意 URL。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="fdf6f-110">這種篡改稱為開放式重新導向攻擊。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="fdf6f-111">每當您的應用程式邏輯重新導向至指定的 URL 時，您都必須確認重新導向 URL 未遭到篡改。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="fdf6f-112">ASP.NET MVC 1.0 和 ASP.NET MVC 2 的預設 AccountController 中使用的登入，容易受到開放式重新導向攻擊。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="fdf6f-113">幸好，您可以輕鬆地更新現有的應用程式，以使用 ASP.NET MVC 3 Preview 的更正。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="fdf6f-114">若要瞭解此弱點，讓我們看看登入重新導向在預設的 ASP.NET MVC 2 Web 應用程式專案中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="fdf6f-115">在此應用程式中，嘗試流覽具有 [授權] 屬性的控制器動作，會將未經授權的使用者重新導向至/Account/LogOn view。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="fdf6f-116">此重新導向至/Account/LogOn 會包含 returnUrl querystring 參數，讓使用者可以在成功登入之後，傳回給原始要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="fdf6f-117">在下面的螢幕擷取畫面中，我們可以看到嘗試在未登入的情況下存取/Account/ChangePassword 視圖，會導致重新導向至/Account/LogOn？ReturnUrl =% 2fAccount% 2fChangePassword% 2f。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="fdf6f-118">**圖 01**：具有開啟重新導向的登入頁面</span><span class="sxs-lookup"><span data-stu-id="fdf6f-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="fdf6f-119">由於不會驗證 ReturnUrl querystring 參數，因此攻擊者可以修改它，以將任何 URL 位址插入參數中，以進行開啟的重新導向攻擊。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="fdf6f-120">為了示範這一點，我們可以將 ReturnUrl 參數修改為[http://bing.com](http://bing.com)，因此產生的登入 URL 將會是/Account/LogOn？ReturnUrl =<http://www.bing.com/>。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="fdf6f-121">成功登入網站後，我們會被重新導向至[http://bing.com](http://bing.com)。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com).</span></span> <span data-ttu-id="fdf6f-122">由於此重新導向並未經過驗證，因此可以改為指向嘗試誘騙使用者的惡意網站。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-122">Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="fdf6f-123">更複雜的開放式重新導向攻擊</span><span class="sxs-lookup"><span data-stu-id="fdf6f-123">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="fdf6f-124">開啟重新導向攻擊特別危險，因為攻擊者知道我們正嘗試登入特定網站，這讓我們容易遭受[網路釣魚攻擊](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-124">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="fdf6f-125">例如，攻擊者可能會將惡意電子郵件傳送給網站使用者，以嘗試捕獲他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-125">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="fdf6f-126">讓我們看看如何在 NerdDinner 網站上執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-126">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="fdf6f-127">（請注意，live NerdDinner 網站已更新為防止開啟重新導向攻擊）。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-127">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="fdf6f-128">首先，攻擊者會將 NerdDinner 上登入頁面的連結傳送給我們，其中包含重新導向至其偽造的網頁：</span><span class="sxs-lookup"><span data-stu-id="fdf6f-128">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="fdf6f-129">請注意，傳回的 URL 會指向 nerddiner.com，這在「晚餐」中遺漏了「n」。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-129">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="fdf6f-130">在此範例中，這是攻擊者所控制的網域。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-130">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="fdf6f-131">當我們存取上述連結時，就會進入合法的 NerdDinner.com 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-131">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="fdf6f-132">**圖 02**：具有開啟重新導向的 NerdDinner 登入頁面</span><span class="sxs-lookup"><span data-stu-id="fdf6f-132">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="fdf6f-133">當我們正確登入時，ASP.NET MVC AccountController 的登入動作會將我們重新導向至 returnUrl querystring 參數中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-133">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="fdf6f-134">在此情況下，這是攻擊者所輸入的 URL，也就是[http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-134">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="fdf6f-135">除非我們非常關注，否則我們很可能不會注意到這一點，特別是因為攻擊者已小心確定其偽造的頁面看起來與合法的登入頁面完全一樣。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-135">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="fdf6f-136">此登入頁面包含一則錯誤訊息，要求我們再次登入。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-136">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="fdf6f-137">笨拙我們，我們必須輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-137">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="fdf6f-138">**圖 03**：偽造的 NerdDinner 登入畫面</span><span class="sxs-lookup"><span data-stu-id="fdf6f-138">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="fdf6f-139">當我們重新輸入使用者名稱和密碼時，偽造的登入頁面會儲存資訊，並將我們傳回到合法的 NerdDinner.com 網站。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-139">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="fdf6f-140">此時，NerdDinner.com 網站已驗證我們，因此偽造的登入頁面可以直接重新導向至該頁面。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-140">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="fdf6f-141">最終結果是攻擊者有使用者名稱和密碼，但我們不知道我們已提供給他們。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-141">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="fdf6f-142">查看 AccountController 登入動作中的弱點程式碼</span><span class="sxs-lookup"><span data-stu-id="fdf6f-142">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="fdf6f-143">ASP.NET MVC 2 應用程式中登入動作的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-143">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="fdf6f-144">請注意，成功登入時，控制器會傳回 returnUrl 的重新導向。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-144">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="fdf6f-145">您可以看到不會針對 returnUrl 參數執行任何驗證。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-145">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="fdf6f-146">**清單1– `AccountController.cs` 中的 ASP.NET MVC 2 登入動作**</span><span class="sxs-lookup"><span data-stu-id="fdf6f-146">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="fdf6f-147">現在讓我們來看一下 ASP.NET MVC 3 登入動作的變更。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-147">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="fdf6f-148">這個程式碼已變更為驗證 returnUrl 參數，方法是在名為 `IsLocalUrl()`的 System.web helper 類別中呼叫新的方法。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-148">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="fdf6f-149">**清單2– `AccountController.cs` 中的 ASP.NET MVC 3 登入動作**</span><span class="sxs-lookup"><span data-stu-id="fdf6f-149">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="fdf6f-150">這已變更為藉由呼叫 System.web helper 類別中的新方法來驗證傳回 URL 參數，`IsLocalUrl()`。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-150">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="fdf6f-151">保護您的 ASP.NET MVC 1.0 和 MVC 2 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdf6f-151">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="fdf6f-152">我們可以藉由新增 IsLocalUrl （） helper 方法並更新登入動作來驗證 returnUrl 參數，以利用現有 ASP.NET MVC 1.0 和2個應用程式中的 ASP.NET MVC 3 變更。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-152">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="fdf6f-153">UrlHelper IsLocalUrl （）方法實際上只會呼叫 System.web 中的方法，因為 ASP.NET Web Pages 應用程式也會使用此驗證。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-153">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="fdf6f-154">**[清單 3] –來自 ASP.NET MVC 3 UrlHelper `class` 的 IsLocalUrl （）方法**</span><span class="sxs-lookup"><span data-stu-id="fdf6f-154">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="fdf6f-155">IsUrlLocalToHost 方法包含實際的驗證邏輯，如 [清單 4] 所示。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-155">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="fdf6f-156">**從 System.web RequestExtensions 類別列出4– IsUrlLocalToHost （）方法**</span><span class="sxs-lookup"><span data-stu-id="fdf6f-156">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="fdf6f-157">在我們的 ASP.NET MVC 1.0 或2應用程式中，我們會在 AccountController 中新增 IsLocalUrl （）方法，但建議您盡可能將它新增至個別的 helper 類別。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-157">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="fdf6f-158">我們會對 ASP.NET MVC 3 版本的 IsLocalUrl （）進行兩個小變更，使其可在 AccountController 內正常執行。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-158">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="fdf6f-159">首先，我們會將它從公用方法變更為私用方法，因為控制器中的公用方法可以當作控制器動作來存取。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-159">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="fdf6f-160">第二，我們將修改對應用程式主機檢查 URL 主機的呼叫。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-160">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="fdf6f-161">該呼叫會使用 UrlHelper 類別中的本機 RequestCoNtext 欄位。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-161">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="fdf6f-162">而不是使用此。RequestCoNtext，我們將使用此 Url。Request. Url. 主機。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="fdf6f-163">下列程式碼顯示已修改的 IsLocalUrl （）方法，以便與 ASP.NET MVC 1.0 和2應用程式中的控制器類別搭配使用。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-163">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="fdf6f-164">**[清單5– IsLocalUrl （）] 方法，其已修改以與 MVC 控制器類別搭配使用**</span><span class="sxs-lookup"><span data-stu-id="fdf6f-164">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="fdf6f-165">現在已備妥 IsLocalUrl （）方法，我們可以從登入動作呼叫它，以驗證 returnUrl 參數，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-165">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="fdf6f-166">**[清單 6]-驗證 returnUrl 參數的已更新登入方法**</span><span class="sxs-lookup"><span data-stu-id="fdf6f-166">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="fdf6f-167">現在，我們可以嘗試使用外部傳回 URL 來登入，藉以測試開啟的重新導向攻擊。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-167">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="fdf6f-168">讓我們使用/Account/LogOn 嗎？ReturnUrl = 再次<http://www.bing.com/>。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-168">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="fdf6f-169">**圖 04**：測試已更新的登入動作</span><span class="sxs-lookup"><span data-stu-id="fdf6f-169">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="fdf6f-170">成功登入之後，我們會被重新導向至主/索引控制器動作，而不是外部 URL。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-170">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="fdf6f-171">**圖 05**：開啟重新導向攻擊失效</span><span class="sxs-lookup"><span data-stu-id="fdf6f-171">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="fdf6f-172">總結</span><span class="sxs-lookup"><span data-stu-id="fdf6f-172">Summary</span></span>

<span data-ttu-id="fdf6f-173">當重新導向 Url 當做應用程式 URL 中的參數傳遞時，可能會發生開啟重新導向攻擊。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-173">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="fdf6f-174">ASP.NET MVC 3 範本包含可防止開啟重新導向攻擊的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-174">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="fdf6f-175">您可以在 ASP.NET MVC 1.0 和2個應用程式的修改中新增此程式碼。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-175">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="fdf6f-176">若要在登入 ASP.NET 1.0 和2個應用程式時防止開啟重新導向攻擊，請新增 IsLocalUrl （）方法，並驗證登入動作中的 returnUrl 參數。</span><span class="sxs-lookup"><span data-stu-id="fdf6f-176">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>
