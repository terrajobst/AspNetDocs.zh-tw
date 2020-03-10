---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET Web Pages （Razor）疑難排解指南 |Microsoft Docs
author: Rick-Anderson
description: 本文描述使用 ASP.NET Web Pages （Razor）時可能發生的問題，以及一些建議的解決方案。 軟體版本 ASP.NET Web Pag 。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585761"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="8cef5-104">ASP.NET Web Pages (Razor) 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="8cef5-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>

<span data-ttu-id="8cef5-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8cef5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8cef5-106">本文描述使用 ASP.NET Web Pages （Razor）時可能發生的問題，以及一些建議的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8cef5-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="8cef5-107">軟體版本</span><span class="sxs-lookup"><span data-stu-id="8cef5-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="8cef5-108">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="8cef5-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="8cef5-109">本教學課程也適用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0。</span><span class="sxs-lookup"><span data-stu-id="8cef5-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>

<span data-ttu-id="8cef5-110">本主題包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="8cef5-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="8cef5-111">執行頁面的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="8cef5-112">Razor 程式碼的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="8cef5-113">安全性和成員資格的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="8cef5-114">傳送電子郵件的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="8cef5-115">其他資源</span><span class="sxs-lookup"><span data-stu-id="8cef5-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="8cef5-116">如需一般問題，請參閱[ASP.NET Web Pages （Razor）常見問題](https://go.microsoft.com/fwlink/?LinkId=253000)。</span><span class="sxs-lookup"><span data-stu-id="8cef5-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="8cef5-117">執行頁面的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-117">Issues with Running Pages</span></span>

<span data-ttu-id="8cef5-118">各種不同的問題可能會導致*cshtml*和*vbhtml*頁面無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="8cef5-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="8cef5-119">本節列出常見的錯誤訊息和可能的原因。</span><span class="sxs-lookup"><span data-stu-id="8cef5-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="8cef5-120">HTTP 錯誤 403-禁止：拒絕存取</span><span class="sxs-lookup"><span data-stu-id="8cef5-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="8cef5-121">*您無權使用您提供的認證來查看此目錄或網頁。*</span><span class="sxs-lookup"><span data-stu-id="8cef5-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="8cef5-122">如果伺服器未執行正確的 .NET Framework 版本，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cef5-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="8cef5-123">請確定執行伺服器（本機或遠端）的電腦至少已安裝 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="8cef5-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="8cef5-124">也請確定應用程式本身已設定為執行正確的版本。</span><span class="sxs-lookup"><span data-stu-id="8cef5-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="8cef5-125">如果您在 WebMatrix 中工作時在本機看到此問題，請按一下 [**網站**] 工作區，然後在 treeview 中按一下 [**設定**]。</span><span class="sxs-lookup"><span data-stu-id="8cef5-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="8cef5-126">在 [**選取 .NET Framework 版本**] 清單中，選取 [ **.Net 4 （整合式）** ]。</span><span class="sxs-lookup"><span data-stu-id="8cef5-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="8cef5-127">如果已設定此版本，請嘗試以系統管理員身分執行 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="8cef5-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="8cef5-128">請確定您網站的根目錄中至少有一個*cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="8cef5-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="8cef5-129">如果網頁伺服器位於遠端伺服器上時看到此錯誤，請洽詢伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="8cef5-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="8cef5-130">請確定伺服器已安裝 .NET Framework 4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8cef5-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="8cef5-131">也請確定應用程式是在設定為使用該版本 the.NET Framework 的應用程式集區中執行。</span><span class="sxs-lookup"><span data-stu-id="8cef5-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="8cef5-132">如果您可以控制伺服器，請確定它正在執行正確的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="8cef5-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="8cef5-133">您也可以執行 `aspnet_regiis -iru` 命令來嘗試修復安裝。</span><span class="sxs-lookup"><span data-stu-id="8cef5-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="8cef5-134">（例如，如果您在安裝 .NET Framework 之後安裝 IIS，則 IIS 將不會正確設定為執行 ASP.NET 網頁。）如需詳細資訊，請參閱[ASP.NET IIS 註冊工具（Aspnet\_regiis）](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="8cef5-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="8cef5-135">HTTP 錯誤 403.14-禁止</span><span class="sxs-lookup"><span data-stu-id="8cef5-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="8cef5-136">*網頁伺服器已設定為不列出此目錄的內容。*</span><span class="sxs-lookup"><span data-stu-id="8cef5-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="8cef5-137">如果您要求受保護的資源（例如*web.config*檔案），或在受保護的資料夾（例如*應用程式\_資料*或*應用程式\_碼*）中，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cef5-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="8cef5-138">HTTP 錯誤 404.17-找不到</span><span class="sxs-lookup"><span data-stu-id="8cef5-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="8cef5-139">*要求的內容似乎是腳本，因此靜態檔案處理常式不會提供服務。*</span><span class="sxs-lookup"><span data-stu-id="8cef5-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="8cef5-140">如果伺服器未正確設定為使用 .NET Framework 4 或更新版本，因而無法辨識 `@{ }` 區塊中的程式碼，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cef5-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="8cef5-141">請參閱稍早的 < *HTTP 錯誤 403-禁止的描述：拒絕存取*。</span><span class="sxs-lookup"><span data-stu-id="8cef5-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="8cef5-142">HTTP 錯誤 404.7-找不到</span><span class="sxs-lookup"><span data-stu-id="8cef5-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="8cef5-143">*要求篩選模組設定為拒絕副檔名*</span><span class="sxs-lookup"><span data-stu-id="8cef5-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="8cef5-144">如果伺服器上已明確封鎖 *. cshtml*或*vbhtml*延伸模組，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cef5-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="8cef5-145">這個問題的徵兆是，當 Url 不包含副檔名，但包含 *. cshtml*或*vbhtml*的 url 無法使用時，就會執行。</span><span class="sxs-lookup"><span data-stu-id="8cef5-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="8cef5-146">可能的解決方法是在*網站的 web.config*檔案中重新啟用延伸模組。</span><span class="sxs-lookup"><span data-stu-id="8cef5-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="8cef5-147">下列範例顯示如何啟用 *.* # 副檔名。</span><span class="sxs-lookup"><span data-stu-id="8cef5-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="8cef5-148">HTTP 錯誤 404.8-找不到</span><span class="sxs-lookup"><span data-stu-id="8cef5-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="8cef5-149">*要求篩選模組設定為拒絕包含 hiddenSegment 區段之 URL 中的路徑。*</span><span class="sxs-lookup"><span data-stu-id="8cef5-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="8cef5-150">如果您要求受保護的資源（例如*web.config*檔案），或在受保護的資料夾（例如*應用程式\_資料*或*應用程式\_碼*）中，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cef5-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="8cef5-151">未提供此類型的頁面（'/' 應用程式中的伺服器錯誤）</span><span class="sxs-lookup"><span data-stu-id="8cef5-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="8cef5-152">請參閱稍早的 HTTP 錯誤404.17 說明。</span><span class="sxs-lookup"><span data-stu-id="8cef5-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="8cef5-153">Razor 程式碼的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="8cef5-154">名稱 '*class*' 不存在於目前的內容中</span><span class="sxs-lookup"><span data-stu-id="8cef5-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="8cef5-155">通常，您會看到此錯誤的原因是 `class` 參考協助程式，但未安裝 helper。</span><span class="sxs-lookup"><span data-stu-id="8cef5-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="8cef5-156">例如，如果您嘗試使用協助程式，但未從 NuGet 安裝套件，您將會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cef5-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="8cef5-157">使用 WebMatrix 中的圖庫來尋找並安裝協助程式。</span><span class="sxs-lookup"><span data-stu-id="8cef5-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="8cef5-158">如果已安裝協助程式，但頁面仍無法辨識，請嘗試新增 [將 `using` 語句加入至程式碼]。</span><span class="sxs-lookup"><span data-stu-id="8cef5-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="8cef5-159">在 `using` 語句中，參考包含 helper 的命名空間。</span><span class="sxs-lookup"><span data-stu-id="8cef5-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="8cef5-160">例如，ASP.NET Web helper 套件中的基本協助程式位於 `System.Web.Helpers` 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="8cef5-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="8cef5-161">在您要使用 helper 的頁面頂端，新增下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="8cef5-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="8cef5-162">安全性和成員資格的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-162">Issues with Security and Membership</span></span>

<span data-ttu-id="8cef5-163">如果您使用 ASP.NET Web Pages （Razor）中的內建安全性（成員資格）系統，您可能會遇到下列問題。</span><span class="sxs-lookup"><span data-stu-id="8cef5-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="8cef5-164">若要呼叫此方法，"成員資格. Provider" 屬性必須是 "ExtendedMembershipProvider" 的實例。</span><span class="sxs-lookup"><span data-stu-id="8cef5-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="8cef5-165">此錯誤可能表示未設定任何 `AspNetSqlMembershipProvider` 類別。</span><span class="sxs-lookup"><span data-stu-id="8cef5-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="8cef5-166">（徵兆是網站在本機運作正常，但當您將此錯誤發行至主機服務提供者的伺服器時，會擲回此錯誤）。此問題的一個修正是將下列內容新增至網站的*web.config*檔案，明確啟用簡單的成員資格：</span><span class="sxs-lookup"><span data-stu-id="8cef5-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="8cef5-167">傳送電子郵件的問題</span><span class="sxs-lookup"><span data-stu-id="8cef5-167">Issues with Sending Email</span></span>

<span data-ttu-id="8cef5-168">傳送電子郵件的問題可能會很難進行 debug。</span><span class="sxs-lookup"><span data-stu-id="8cef5-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="8cef5-169">最初的問題可能是您無法連接到 SMTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8cef5-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="8cef5-170">如果連接成功，請 ASP.NET 將訊息交給 SMTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8cef5-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="8cef5-171">不過，可能會有訊息本身的問題，而導致 SMTP 伺服器無法傳送它。</span><span class="sxs-lookup"><span data-stu-id="8cef5-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="8cef5-172">如果您的應用程式未成功傳送電子郵件，請嘗試下列動作：</span><span class="sxs-lookup"><span data-stu-id="8cef5-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="8cef5-173">SMTP 伺服器名稱通常類似 `smtp.provider.com` 或 `smtp.provider.net`。</span><span class="sxs-lookup"><span data-stu-id="8cef5-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="8cef5-174">不過，如果您將網站發佈至主機服務提供者，該點的 SMTP 伺服器名稱可能會 `localhost`。</span><span class="sxs-lookup"><span data-stu-id="8cef5-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="8cef5-175">發生這種情況的原因是，當您發佈，而且您的網站在提供者的伺服器上執行之後，SMTP 伺服器可能會從您的應用程式觀點來看。</span><span class="sxs-lookup"><span data-stu-id="8cef5-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="8cef5-176">伺服器名稱的這項變更可能表示您必須在發佈程式中變更 SMTP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="8cef5-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="8cef5-177">埠號碼通常是25。</span><span class="sxs-lookup"><span data-stu-id="8cef5-177">The port number is usually 25.</span></span> <span data-ttu-id="8cef5-178">不過，某些提供者會要求您使用埠587或其他通訊埠。</span><span class="sxs-lookup"><span data-stu-id="8cef5-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="8cef5-179">向 SMTP 伺服器的擁有者確認他們預期使用的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="8cef5-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="8cef5-180">請確定您使用正確的認證。</span><span class="sxs-lookup"><span data-stu-id="8cef5-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="8cef5-181">如果您已將您的網站發佈至主控提供者，請使用提供者特別指出的認證做為電子郵件。</span><span class="sxs-lookup"><span data-stu-id="8cef5-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="8cef5-182">這些認證可能與您用來發佈的認證不同。</span><span class="sxs-lookup"><span data-stu-id="8cef5-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="8cef5-183">有時候您不需要認證。</span><span class="sxs-lookup"><span data-stu-id="8cef5-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="8cef5-184">如果您是使用個人 ISP 來傳送電子郵件，您的電子郵件提供者可能已經知道您的認證。</span><span class="sxs-lookup"><span data-stu-id="8cef5-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="8cef5-185">發行之後，您可能需要使用與在本機電腦上測試時不同的認證。</span><span class="sxs-lookup"><span data-stu-id="8cef5-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="8cef5-186">如果您的電子郵件提供者使用加密，請將 `WebMail.EnableSsl` 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="8cef5-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="8cef5-187">如果傳送電子郵件時發生錯誤，您可能會看到標準的 ASP.NET 錯誤訊息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8cef5-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![當電子郵件發生問題時 ASP.NET 錯誤訊息](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="8cef5-189">您也可以使用 `try-catch` 區塊來偵測傳送電子郵件的問題，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="8cef5-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="8cef5-190">當您使用 `try-catch` 區塊時，ASP.NET 不會顯示其標準錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="8cef5-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="8cef5-191">相反地，您可以在區塊的 `catch` 部分中捕捉錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cef5-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="8cef5-192">請以適當的值取代 `your-SMTP-server-name`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="8cef5-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="8cef5-193">某些您可能會看到的錯誤訊息包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="8cef5-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="8cef5-194">*無法傳送郵件。*</span><span class="sxs-lookup"><span data-stu-id="8cef5-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="8cef5-195">-或-</span><span class="sxs-lookup"><span data-stu-id="8cef5-195">-or-</span></span>

    <span data-ttu-id="8cef5-196">*連線嘗試失敗，因為連接的合作物件在一段時間內未正確回應，或建立的連線失敗，因為連接的主機無法回應*</span><span class="sxs-lookup"><span data-stu-id="8cef5-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="8cef5-197">此錯誤通常表示應用程式無法連接到 SMTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8cef5-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="8cef5-198">檢查伺服器名稱和埠號碼。</span><span class="sxs-lookup"><span data-stu-id="8cef5-198">Check the server name and port number.</span></span>
- <span data-ttu-id="8cef5-199">*信箱無法使用。伺服器回應為： 5.1.0 &lt;someuser@invaliddomain&gt; 寄件者拒絕：不正確寄件者網域*</span><span class="sxs-lookup"><span data-stu-id="8cef5-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="8cef5-200">此訊息可能表示 `From` 位址不正確或遺失。</span><span class="sxs-lookup"><span data-stu-id="8cef5-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="8cef5-201">*指定的字串不是電子郵件地址所需的格式。*</span><span class="sxs-lookup"><span data-stu-id="8cef5-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="8cef5-202">此錯誤可能表示 `To` 或 `From` 屬性的值無法辨識為電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8cef5-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="8cef5-203">（ASP.NET 無法檢查電子郵件地址是否有效，只有其格式正確，如 *name@domain.com* 。）</span><span class="sxs-lookup"><span data-stu-id="8cef5-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="8cef5-204">將頁面發行至即時網站之前，請先移除顯示錯誤的標記（`@errorMessage`）。</span><span class="sxs-lookup"><span data-stu-id="8cef5-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="8cef5-205">讓使用者看得到從伺服器取得的錯誤訊息並不是個好主意。</span><span class="sxs-lookup"><span data-stu-id="8cef5-205">It's not a good idea to let users see error messages that you get from a server.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="8cef5-206">其他資源</span><span class="sxs-lookup"><span data-stu-id="8cef5-206">Additional Resources</span></span>

[<span data-ttu-id="8cef5-207">ASP.NET Web Pages (Razor) 常見問題集</span><span class="sxs-lookup"><span data-stu-id="8cef5-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="8cef5-208">ASP.NET 網站上的[WebMatrix 和 ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix)論壇</span><span class="sxs-lookup"><span data-stu-id="8cef5-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
