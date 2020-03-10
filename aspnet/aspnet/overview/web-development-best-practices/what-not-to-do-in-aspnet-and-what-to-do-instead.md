---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: 不要在 ASP.NET 中做什麼，以及該怎麼做？Microsoft Docs
author: Rick-Anderson
description: 本主題說明在 ASP.NET Web 專案中的幾個常見錯誤。 它會提供您應採取哪些措施來避免這些通用的建議 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616988"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="ad551-104">在 ASP.NET 中不該做什麼以及該做什麼</span><span class="sxs-lookup"><span data-stu-id="ad551-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="ad551-105">本主題說明在 ASP.NET Web 專案中的幾個常見錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad551-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="ad551-106">它會提供您應採取哪些動作來避免這些常見錯誤的建議。</span><span class="sxs-lookup"><span data-stu-id="ad551-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="ad551-107">其以[簡報](http://vimeo.com/68390507)為基礎， **Damian Edwards**在挪威開發人員會議。</span><span class="sxs-lookup"><span data-stu-id="ad551-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="ad551-108">免責聲明</span><span class="sxs-lookup"><span data-stu-id="ad551-108">Disclaimer</span></span>

<span data-ttu-id="ad551-109">本主題不是為了確保您的應用程式安全且有效率的完整指南。</span><span class="sxs-lookup"><span data-stu-id="ad551-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="ad551-110">您仍然需要遵循本主題未概述之安全性和效能的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="ad551-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="ad551-111">它只會建議如何避免與 .NET 類別和進程相關的常見錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad551-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="ad551-112">概觀</span><span class="sxs-lookup"><span data-stu-id="ad551-112">Overview</span></span>

<span data-ttu-id="ad551-113">本主題包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="ad551-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="ad551-114">標準合規性</span><span class="sxs-lookup"><span data-stu-id="ad551-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="ad551-115">控制介面卡</span><span class="sxs-lookup"><span data-stu-id="ad551-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="ad551-116">控制項的樣式屬性</span><span class="sxs-lookup"><span data-stu-id="ad551-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="ad551-117">頁面和控制項回呼</span><span class="sxs-lookup"><span data-stu-id="ad551-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="ad551-118">瀏覽器功能偵測</span><span class="sxs-lookup"><span data-stu-id="ad551-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="ad551-119">Security</span><span class="sxs-lookup"><span data-stu-id="ad551-119">Security</span></span>](#security)

    - [<span data-ttu-id="ad551-120">要求驗證</span><span class="sxs-lookup"><span data-stu-id="ad551-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="ad551-121">無 cookie 的表單驗證和會話</span><span class="sxs-lookup"><span data-stu-id="ad551-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="ad551-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="ad551-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="ad551-123">中度信任</span><span class="sxs-lookup"><span data-stu-id="ad551-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="ad551-124">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="ad551-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="ad551-125">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="ad551-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="ad551-126">可靠性和效能</span><span class="sxs-lookup"><span data-stu-id="ad551-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="ad551-127">PreSendRequestHeaders 和 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="ad551-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="ad551-128">使用 Web Forms 的非同步頁面事件</span><span class="sxs-lookup"><span data-stu-id="ad551-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="ad551-129">火災和忘記的工作</span><span class="sxs-lookup"><span data-stu-id="ad551-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="ad551-130">要求實體主體</span><span class="sxs-lookup"><span data-stu-id="ad551-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="ad551-131">回應。重新導向和回應。結束</span><span class="sxs-lookup"><span data-stu-id="ad551-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="ad551-132">EnableViewState 和 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="ad551-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="ad551-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="ad551-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="ad551-134">長時間執行的要求（> 110 秒）</span><span class="sxs-lookup"><span data-stu-id="ad551-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="ad551-135">標準合規性</span><span class="sxs-lookup"><span data-stu-id="ad551-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="ad551-136">控制介面卡</span><span class="sxs-lookup"><span data-stu-id="ad551-136">Control adapters</span></span>

<span data-ttu-id="ad551-137">建議：停止使用控制項介面卡進行調適型轉譯，而改用 CSS 媒體查詢和符合標準的 HTML。</span><span class="sxs-lookup"><span data-stu-id="ad551-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="ad551-138">控制項介面卡是在 .NET 2.0 中引進，以轉譯針對不同裝置和環境自訂的呈現程式碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="ad551-139">現在，您可以使用 CSS 和 HTML 來完成此彈性轉譯。</span><span class="sxs-lookup"><span data-stu-id="ad551-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="ad551-140">您應該停止使用控制項介面卡，並將任何現有的介面卡轉換成 CSS 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="ad551-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="ad551-141">如需詳細資訊，請參閱[媒體查詢](http://www.w3.org/TR/css3-mediaqueries/)和[如何：將行動頁面加入至您的 ASP.NET WEB Forms/MVC 應用程式](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="ad551-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="ad551-142">控制項的樣式屬性</span><span class="sxs-lookup"><span data-stu-id="ad551-142">Style properties on controls</span></span>

<span data-ttu-id="ad551-143">建議：停止在控制項標記中設定樣式值，並改為在 CSS 樣式表單中設定格式化值。</span><span class="sxs-lookup"><span data-stu-id="ad551-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="ad551-144">Web 服務器控制項包含數十個屬性，可用於設定內嵌樣式屬性。</span><span class="sxs-lookup"><span data-stu-id="ad551-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="ad551-145">例如，前景屬性會設定控制項的文字色彩。</span><span class="sxs-lookup"><span data-stu-id="ad551-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="ad551-146">您可以透過 CSS 樣式表單，更有效率地達成相同的效果。</span><span class="sxs-lookup"><span data-stu-id="ad551-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="ad551-147">樣式表單可讓您集中樣式值，並避免在整個應用程式中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="ad551-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="ad551-148">下列範例顯示將文字設為紅色的 CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="ad551-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="ad551-149">下一個範例顯示如何動態套用 CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="ad551-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="ad551-150">頁面和控制項回呼</span><span class="sxs-lookup"><span data-stu-id="ad551-150">Page and control callbacks</span></span>

<span data-ttu-id="ad551-151">建議：停止使用頁面和控制項回呼，並改為使用下列任何一項： AJAX、UpdatePanel、MVC 動作方法、Web API 或 SignalR。</span><span class="sxs-lookup"><span data-stu-id="ad551-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="ad551-152">在舊版的 ASP.NET 中，頁面和控制項回呼方法可讓您更新部分網頁，而不需要重新整理整個頁面。</span><span class="sxs-lookup"><span data-stu-id="ad551-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="ad551-153">您現在可以透過[AJAX](../../../ajax/index.md)、 [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)、 [MVC](../../../mvc/index.md)、 [Web API](../../../web-api/index.md)或[SignalR](../../../signalr/index.md)完成部分頁面更新。</span><span class="sxs-lookup"><span data-stu-id="ad551-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="ad551-154">您應該停止使用回呼方法，因為它們可能會造成易記 Url 和路由的問題。</span><span class="sxs-lookup"><span data-stu-id="ad551-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="ad551-155">根據預設，控制項不會啟用回呼方法，但如果您已在控制項中啟用這項功能，您應該將它停用。</span><span class="sxs-lookup"><span data-stu-id="ad551-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="ad551-156">瀏覽器功能偵測</span><span class="sxs-lookup"><span data-stu-id="ad551-156">Browser capability detection</span></span>

<span data-ttu-id="ad551-157">建議：停止使用靜態瀏覽器功能偵測，並改為使用動態功能偵測。</span><span class="sxs-lookup"><span data-stu-id="ad551-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="ad551-158">在舊版的 ASP.NET 中，每個瀏覽器所支援的功能都是儲存在 XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ad551-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="ad551-159">透過靜態查閱偵測功能支援並不是最佳的方法。</span><span class="sxs-lookup"><span data-stu-id="ad551-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="ad551-160">現在，您可以使用功能偵測架構（例如[Modernizr](http://modernizr.com/)），動態偵測瀏覽器支援的功能。</span><span class="sxs-lookup"><span data-stu-id="ad551-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="ad551-161">功能偵測藉由嘗試使用方法或屬性，然後檢查瀏覽器是否產生想要的結果，來判斷支援。</span><span class="sxs-lookup"><span data-stu-id="ad551-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="ad551-162">根據預設，Modernizr 會包含在 Web 應用程式範本中。</span><span class="sxs-lookup"><span data-stu-id="ad551-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="ad551-163">安全性</span><span class="sxs-lookup"><span data-stu-id="ad551-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="ad551-164">要求驗證</span><span class="sxs-lookup"><span data-stu-id="ad551-164">Request validation</span></span>

<span data-ttu-id="ad551-165">建議：驗證使用者輸入，並將使用者的輸出編碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="ad551-166">要求驗證是 ASP.NET 的一項功能，它會檢查每個要求，並在發現認知的威脅時停止要求。</span><span class="sxs-lookup"><span data-stu-id="ad551-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="ad551-167">請勿依賴要求驗證來保護您的應用程式，以防止跨網站腳本攻擊。</span><span class="sxs-lookup"><span data-stu-id="ad551-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="ad551-168">相反地，請驗證使用者的所有輸入，並將輸出編碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="ad551-169">在某些有限的情況下，您可以使用正則運算式來驗證輸入，但在較複雜的情況下，您應該使用 .NET 類別來驗證使用者輸入，以判斷值是否符合允許的值。</span><span class="sxs-lookup"><span data-stu-id="ad551-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="ad551-170">下列範例示範如何在 Uri 類別中使用靜態方法，以判斷使用者所提供的 Uri 是否有效。</span><span class="sxs-lookup"><span data-stu-id="ad551-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="ad551-171">不過，若要充分驗證 Uri，您也應該檢查以確定它指定 `http` 或 `https`。</span><span class="sxs-lookup"><span data-stu-id="ad551-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="ad551-172">下列範例會使用實例方法來確認 Uri 是否有效。</span><span class="sxs-lookup"><span data-stu-id="ad551-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="ad551-173">將使用者輸入轉譯為 HTML 或在 SQL 查詢中包含使用者輸入之前，請將值編碼，以確保不會包含惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="ad551-174">您可以使用 &lt;%：%&gt; 語法，以 HTML 編碼標記中的值，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ad551-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="ad551-175">或者，在 Razor 語法中，您可以使用 @ 進行 HTML 編碼，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ad551-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="ad551-176">下一個範例顯示如何在程式碼後置中以 HTML 編碼值。</span><span class="sxs-lookup"><span data-stu-id="ad551-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="ad551-177">若要安全地編碼 SQL 命令的值，請使用命令參數，例如[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="ad551-178">無 cookie 的表單驗證和會話</span><span class="sxs-lookup"><span data-stu-id="ad551-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="ad551-179">建議：需要 cookie。</span><span class="sxs-lookup"><span data-stu-id="ad551-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="ad551-180">在查詢字串中傳遞驗證資訊並不安全。</span><span class="sxs-lookup"><span data-stu-id="ad551-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="ad551-181">因此，當您的應用程式包含驗證時，需要 cookie。</span><span class="sxs-lookup"><span data-stu-id="ad551-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="ad551-182">如果您的 cookie 會儲存敏感資訊，請考慮為 cookie 要求 SSL。</span><span class="sxs-lookup"><span data-stu-id="ad551-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="ad551-183">下列範例顯示如何在 web.config 檔案中指定表單驗證需要透過 SSL 傳輸的 cookie。</span><span class="sxs-lookup"><span data-stu-id="ad551-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="ad551-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="ad551-184">EnableViewStateMac</span></span>

<span data-ttu-id="ad551-185">建議：永不設定為 false。</span><span class="sxs-lookup"><span data-stu-id="ad551-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="ad551-186">根據預設，EnableViewStateMac 會設定為 true。</span><span class="sxs-lookup"><span data-stu-id="ad551-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="ad551-187">即使您的應用程式未使用 view 狀態，也不會將 EnableViewStateMac 設定為 false。</span><span class="sxs-lookup"><span data-stu-id="ad551-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="ad551-188">將此值設定為 false 會讓您的應用程式容易遭受跨網站腳本處理。</span><span class="sxs-lookup"><span data-stu-id="ad551-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="ad551-189">從 ASP.NET 4.5.2 開始，執行時間會強制執行**EnableViewStateMac = true**。</span><span class="sxs-lookup"><span data-stu-id="ad551-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="ad551-190">即使您將它設定為 false，執行時間也會忽略此值，並繼續將值設定為 true。</span><span class="sxs-lookup"><span data-stu-id="ad551-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="ad551-191">如需詳細資訊，請參閱[ASP.NET 4.5.2 And EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="ad551-192">下列範例顯示如何將 EnableViewStateMac 設定為 true。</span><span class="sxs-lookup"><span data-stu-id="ad551-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="ad551-193">您不需要實際將此值設定為 true，因為它預設為 true。</span><span class="sxs-lookup"><span data-stu-id="ad551-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="ad551-194">不過，如果您已在應用程式的任何頁面上將它設為 false，則必須立即更正此值。</span><span class="sxs-lookup"><span data-stu-id="ad551-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="ad551-195">中度信任</span><span class="sxs-lookup"><span data-stu-id="ad551-195">Medium trust</span></span>

<span data-ttu-id="ad551-196">建議：不要依賴中等信任（或任何其他信任層級）做為安全性界限。</span><span class="sxs-lookup"><span data-stu-id="ad551-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="ad551-197">部分信任不會適當地保護您的應用程式，因此不應使用。</span><span class="sxs-lookup"><span data-stu-id="ad551-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="ad551-198">相反地，請使用完全信任，並隔離不同應用程式集區中不受信任的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad551-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="ad551-199">此外，請在唯一的身分識別下執行每個應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="ad551-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="ad551-200">如需詳細資訊，請參閱[ASP.NET 部分信任不保證應用程式隔離](https://support.microsoft.com/kb/2698981)。</span><span class="sxs-lookup"><span data-stu-id="ad551-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="ad551-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="ad551-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="ad551-202">建議：請勿停用 &lt;appSettings&gt; 元素中的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="ad551-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="ad551-203">AppSettings 元素包含許多安全性更新所需的值。</span><span class="sxs-lookup"><span data-stu-id="ad551-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="ad551-204">您不應該變更或停用這些值。</span><span class="sxs-lookup"><span data-stu-id="ad551-204">You should not change or disable these values.</span></span> <span data-ttu-id="ad551-205">如果您在部署更新時必須停用這些值，請在完成部署之後立即重新啟用。</span><span class="sxs-lookup"><span data-stu-id="ad551-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="ad551-206">如需詳細資訊，請參閱[ASP.NET AppSettings 元素](https://msdn.microsoft.com/library/hh975440.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="ad551-207">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="ad551-207">UrlPathEncode</span></span>

<span data-ttu-id="ad551-208">建議：請改用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ad551-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="ad551-209">UrlPathEncode 方法已新增至 .NET Framework，以解決非常特定的瀏覽器相容性問題。</span><span class="sxs-lookup"><span data-stu-id="ad551-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="ad551-210">它不會對 URL 進行適當的編碼，而且不會保護您的應用程式不會受到跨網站腳本的攻擊。</span><span class="sxs-lookup"><span data-stu-id="ad551-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="ad551-211">您不應該在應用程式中使用它。</span><span class="sxs-lookup"><span data-stu-id="ad551-211">You should never use it in your application.</span></span> <span data-ttu-id="ad551-212">請改用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="ad551-213">下列範例示範如何傳遞編碼的 URL 做為超連結控制項的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="ad551-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="ad551-214">可靠性和效能</span><span class="sxs-lookup"><span data-stu-id="ad551-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="ad551-215">PreSendRequestHeaders 和 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="ad551-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="ad551-216">建議：請勿將這些事件與受控模組搭配使用。</span><span class="sxs-lookup"><span data-stu-id="ad551-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="ad551-217">請改為撰寫原生 IIS 模組來執行必要的工作。</span><span class="sxs-lookup"><span data-stu-id="ad551-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="ad551-218">請參閱[建立原生程式碼 HTTP 模組](https://msdn.microsoft.com/library/ms693629.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="ad551-219">您可以使用[PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx)和[PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx)事件搭配原生 IIS 模組。</span><span class="sxs-lookup"><span data-stu-id="ad551-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="ad551-220">請不要搭配執行 `IHttpModule`的受控模組使用 `PreSendRequestHeaders` 和 `PreSendRequestContent`。</span><span class="sxs-lookup"><span data-stu-id="ad551-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="ad551-221">設定這些屬性可能會造成非同步要求的問題。</span><span class="sxs-lookup"><span data-stu-id="ad551-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="ad551-222">應用程式要求路由（ARR）和 websocket 的組合，可能會導致 w3wp.exe 損毀的存取違規例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ad551-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="ad551-223">例如，iiscore！Iiscore 中的 W3_CONTEXT_BASE：： GetIsLastNotification + 68 造成存取違規例外狀況（0xC0000005）。</span><span class="sxs-lookup"><span data-stu-id="ad551-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="ad551-224">使用 web forms 的非同步頁面事件</span><span class="sxs-lookup"><span data-stu-id="ad551-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="ad551-225">建議：在 Web form 中，避免針對頁面生命週期事件撰寫非同步 void 方法，而改為使用[RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx)來執行非同步程式碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="ad551-226">當您以**async**和**void**標記頁面事件時，您無法判斷非同步程式碼何時完成。</span><span class="sxs-lookup"><span data-stu-id="ad551-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="ad551-227">相反地，請使用 RegisterAsyncTask 來執行非同步程式碼，讓您能夠追蹤其完成的方式。</span><span class="sxs-lookup"><span data-stu-id="ad551-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="ad551-228">下列範例顯示包含非同步程式碼的按鈕點擊處理常式。</span><span class="sxs-lookup"><span data-stu-id="ad551-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="ad551-229">這個範例包括以非同步方式讀取字串值，這僅提供做為非同步工作的簡化範例，而不是建議的作法。</span><span class="sxs-lookup"><span data-stu-id="ad551-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="ad551-230">如果您使用非同步工作，請在 Web.config 檔案中將 Http 執行時間目標架構設定為4.5 （或更新版本）。</span><span class="sxs-lookup"><span data-stu-id="ad551-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="ad551-231">將 [目標 framework] 設定為4.5 會開啟 .NET 4.5 中新增的同步處理內容。</span><span class="sxs-lookup"><span data-stu-id="ad551-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="ad551-232">預設會在 Visual Studio 的新專案中設定這個值，但如果您使用現有的專案，則不會設定這個值。</span><span class="sxs-lookup"><span data-stu-id="ad551-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="ad551-233">火災和忘記的工作</span><span class="sxs-lookup"><span data-stu-id="ad551-233">Fire-and-forget work</span></span>

<span data-ttu-id="ad551-234">建議：在 ASP.NET 內處理要求時，請避免啟動不正常的工作（例如呼叫 ThreadPool. QueueUserWorkItem 方法，或建立重複呼叫委派的計時器）。</span><span class="sxs-lookup"><span data-stu-id="ad551-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="ad551-235">如果您的應用程式有在 ASP.NET 內執行的火災和忘工作，您的應用程式可能會無法同步。應用程式域可以在任何時間終結，這表示您進行中的程式可能不再符合應用程式的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="ad551-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="ad551-236">您應該將這種類型的工作移到 ASP.NET 之外。</span><span class="sxs-lookup"><span data-stu-id="ad551-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="ad551-237">您可以在 Azure 中使用 Web 作業、Windows 服務或背景工作角色來執行進行中的工作，並從另一個進程執行該程式碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="ad551-238">如果您必須在 ASP.NET 中執行此工作，您可以新增名為[WebBackgrounder](http://www.nuget.org/packages/webbackgrounder)的 Nuget 套件來執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="ad551-239">要求實體主體</span><span class="sxs-lookup"><span data-stu-id="ad551-239">Request entity body</span></span>

<span data-ttu-id="ad551-240">建議：請避免在處理常式的 execute 事件之前，InputStream 讀取要求. Form 或 Request。</span><span class="sxs-lookup"><span data-stu-id="ad551-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="ad551-241">您最早應從 Request 讀取。表單或要求。 InputStream 是在處理常式的 execute 事件期間。</span><span class="sxs-lookup"><span data-stu-id="ad551-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="ad551-242">在 MVC 中，控制器是處理常式，而執行事件是在動作方法執行時。</span><span class="sxs-lookup"><span data-stu-id="ad551-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="ad551-243">在 Web form 中，頁面是處理常式，而執行事件是在 Page. Init 事件引發時。</span><span class="sxs-lookup"><span data-stu-id="ad551-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="ad551-244">如果您讀取的要求實體內容早于執行事件，您會干擾要求的處理。</span><span class="sxs-lookup"><span data-stu-id="ad551-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="ad551-245">如果您需要在執行事件之前讀取要求實體主體，請使用[GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx)或[request. GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="ad551-246">當您使用 GetBufferlessInputStream 時，您會從要求取得未經處理的資料流程，並假設您負責處理整個要求。</span><span class="sxs-lookup"><span data-stu-id="ad551-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="ad551-247">在呼叫 GetBufferlessInputStream 之後，要求. Form 和 Request. InputStream 無法使用，因為 ASP.NET 並未填入這些要求。</span><span class="sxs-lookup"><span data-stu-id="ad551-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="ad551-248">當您使用 GetBufferedInputStream 時，您會從要求取得資料流程的複本。</span><span class="sxs-lookup"><span data-stu-id="ad551-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="ad551-249">InputStream 仍可在要求中使用，因為 ASP.NET 會填入另一個複本。</span><span class="sxs-lookup"><span data-stu-id="ad551-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="ad551-250">回應。重新導向和回應。結束</span><span class="sxs-lookup"><span data-stu-id="ad551-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="ad551-251">建議：請留意執行緒在呼叫回應後的處理方式差異[。重新導向（字串）](https://msdn.microsoft.com/library/t9dwyts4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="ad551-252">[Response （String）](https://msdn.microsoft.com/library/t9dwyts4.aspx)方法會呼叫 Response. End 方法。</span><span class="sxs-lookup"><span data-stu-id="ad551-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="ad551-253">在同步處理過程中，呼叫要求。重新導向會導致目前的執行緒立即中止。</span><span class="sxs-lookup"><span data-stu-id="ad551-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="ad551-254">不過，在非同步程式中，呼叫回應。重新導向並不會中止目前的執行緒，因此程式碼會繼續執行要求。</span><span class="sxs-lookup"><span data-stu-id="ad551-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="ad551-255">在非同步處理過程中，您必須從方法傳回工作，以停止執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="ad551-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="ad551-256">在 MVC 專案中，您不應該呼叫 Response。重新導向。</span><span class="sxs-lookup"><span data-stu-id="ad551-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="ad551-257">相反地，會傳回 RedirectResult。</span><span class="sxs-lookup"><span data-stu-id="ad551-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="ad551-258">EnableViewState 和 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="ad551-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="ad551-259">建議：使用 ViewStateMode，而不是 EnableViewState，以提供更細微的控制哪些控制項使用檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="ad551-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="ad551-260">當您在頁面指示詞中將 EnableViewState 設定為 false 時，頁面中的所有控制項都會停用檢視狀態，而且無法啟用。</span><span class="sxs-lookup"><span data-stu-id="ad551-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="ad551-261">如果您只想要針對頁面中的特定控制項啟用 [檢視狀態]，請將頁面的 [ViewStateMode] 設定為 [停用]。</span><span class="sxs-lookup"><span data-stu-id="ad551-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="ad551-262">然後，只在實際需要檢視狀態的控制項上，將 [ViewStateMode] 設定為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="ad551-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="ad551-263">藉由僅針對需要的控制項啟用 [檢視狀態]，您可以壓縮網頁的檢視狀態大小。</span><span class="sxs-lookup"><span data-stu-id="ad551-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="ad551-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="ad551-264">SqlMembershipProvider</span></span>

<span data-ttu-id="ad551-265">建議：使用 Universal Providers。</span><span class="sxs-lookup"><span data-stu-id="ad551-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="ad551-266">在目前的專案範本中，SqlMembershipProvider 已由[ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)取代，這是以 NuGet 套件的形式提供。</span><span class="sxs-lookup"><span data-stu-id="ad551-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="ad551-267">如果您在以舊版範本建立的專案中使用 SqlMembershipProvider，您應該切換到 Universal Providers。</span><span class="sxs-lookup"><span data-stu-id="ad551-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="ad551-268">Universal Providers 會使用 Entity Framework 所支援的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="ad551-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="ad551-269">如需詳細資訊，請參閱[ASP.NET Universal Providers 簡介](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad551-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="ad551-270">長時間執行的要求（> 110 秒）</span><span class="sxs-lookup"><span data-stu-id="ad551-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="ad551-271">建議：針對已連線的用戶端使用[websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx)或[SignalR](../../../signalr/index.md) ，並使用非同步 i/o 作業。</span><span class="sxs-lookup"><span data-stu-id="ad551-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="ad551-272">長時間執行的要求可能會導致您的 web 應用程式發生無法預期的結果和效能不佳。</span><span class="sxs-lookup"><span data-stu-id="ad551-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="ad551-273">要求的預設超時設定為110秒。</span><span class="sxs-lookup"><span data-stu-id="ad551-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="ad551-274">如果您使用會話狀態搭配長時間執行的要求，ASP.NET 會在110秒後釋放會話物件的鎖定。</span><span class="sxs-lookup"><span data-stu-id="ad551-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="ad551-275">不過，當釋放鎖定時，您的應用程式可能正在會話物件上進行作業，而此操作可能無法順利完成。</span><span class="sxs-lookup"><span data-stu-id="ad551-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="ad551-276">當第一個要求執行時，如果使用者的第二個要求遭到封鎖，第二個要求可能會存取處於不一致狀態的會話物件。</span><span class="sxs-lookup"><span data-stu-id="ad551-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="ad551-277">如果您的應用程式包含封鎖（或同步） i/o 作業，應用程式將會沒有回應。</span><span class="sxs-lookup"><span data-stu-id="ad551-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="ad551-278">若要改善效能，請使用 .NET Framework 中的非同步 i/o 作業。</span><span class="sxs-lookup"><span data-stu-id="ad551-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="ad551-279">此外，請使用 Websocket 或 SignalR 將用戶端連接到伺服器。</span><span class="sxs-lookup"><span data-stu-id="ad551-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="ad551-280">這些功能的設計目的是要有效率地處理長時間執行的要求。</span><span class="sxs-lookup"><span data-stu-id="ad551-280">These features are designed to efficiently handle long-running requests.</span></span>
