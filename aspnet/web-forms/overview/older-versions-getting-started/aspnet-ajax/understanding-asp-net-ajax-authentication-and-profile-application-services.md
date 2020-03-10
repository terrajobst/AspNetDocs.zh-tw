---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: 瞭解 ASP.NET AJAX 驗證和設定檔應用程式服務 |Microsoft Docs
author: scottcate
description: 驗證服務可讓使用者提供認證，以接收驗證 cookie，而閘道服務則允許自訂使用者 。
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640529"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a><span data-ttu-id="c67f4-103">了解 ASP.NET AJAX 驗證與設定檔應用程式服務</span><span class="sxs-lookup"><span data-stu-id="c67f4-103">Understanding ASP.NET AJAX Authentication and Profile Application Services</span></span>

<span data-ttu-id="c67f4-104">由[Scott Cate](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="c67f4-104">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="c67f4-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="c67f4-105">Download PDF</span></span>](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> <span data-ttu-id="c67f4-106">驗證服務可讓使用者提供認證，以接收驗證 cookie，而是閘道服務，允許 ASP.NET 所提供的自訂使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="c67f4-106">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="c67f4-107">使用 ASP.NET AJAX authentication 服務與標準 ASP.NET 表單驗證相容，因此目前使用表單驗證的應用程式（例如使用登入控制項）不會因為升級至 AJAX 驗證服務而中斷。</span><span class="sxs-lookup"><span data-stu-id="c67f4-107">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

## <a name="introduction"></a><span data-ttu-id="c67f4-108">簡介</span><span class="sxs-lookup"><span data-stu-id="c67f4-108">Introduction</span></span>

<span data-ttu-id="c67f4-109">作為 .NET Framework 3.5 的一部分，Microsoft 提供了可調整規模的環境升級;不僅提供新的開發環境，還推出了新的語言整合式查詢（LINQ）功能和其他語言增強功能。</span><span class="sxs-lookup"><span data-stu-id="c67f4-109">As part of the .NET Framework 3.5, Microsoft is delivering a sizable environment upgrade; not only is a new development environment available, but the new Language-Integrated Query (LINQ) features and other language enhancements are forthcoming.</span></span> <span data-ttu-id="c67f4-110">此外，其他工具組的一些熟悉功能（尤其是 ASP.NET AJAX 延伸模組）會包含為 .NET Framework 基類庫的第一類成員。</span><span class="sxs-lookup"><span data-stu-id="c67f4-110">In addition, some familiar features of other toolsets, notably the ASP.NET AJAX Extensions, are being included as first-class members of the .NET Framework Base Class Library.</span></span> <span data-ttu-id="c67f4-111">這些延伸模組可啟用許多新的豐富用戶端功能，包括部分呈現頁面，而不需要完整的頁面重新整理、透過用戶端腳本存取 Web 服務的能力（包括 ASP.NET 分析 API），以及廣泛的用戶端 API設計來鏡像 ASP.NET 伺服器端控制項集中所見的許多控制項配置。</span><span class="sxs-lookup"><span data-stu-id="c67f4-111">These extensions enable many new rich client features, including partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="c67f4-112">本白皮書探討 ASP.NET 分析和表單驗證服務的執行方式，因為它們是由 Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions 所公開，讓表單驗證非常容易支援，也就是分析服務）是透過 Web 服務 proxy 腳本公開。</span><span class="sxs-lookup"><span data-stu-id="c67f4-112">This whitepaper looks at the implementation and use of the ASP.NET Profiling and Forms Authentication services as they are exposed by the Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions make Forms authentication incredibly easy to support, as it (as well as the Profiling Service) is exposed through a Web Service proxy script.</span></span> <span data-ttu-id="c67f4-113">AJAX 延伸模組也支援透過 AuthenticationServiceManager 類別的自訂驗證。</span><span class="sxs-lookup"><span data-stu-id="c67f4-113">The AJAX Extensions also support custom authentication through the AuthenticationServiceManager class.</span></span>

<span data-ttu-id="c67f4-114">本白皮書是以 Visual Studio 2008 和 .NET Framework 3.5 的 Beta 2 版為基礎。</span><span class="sxs-lookup"><span data-stu-id="c67f4-114">This whitepaper is based on the Beta 2 release of the Visual Studio 2008 and the .NET Framework 3.5.</span></span> <span data-ttu-id="c67f4-115">本白皮書也假設您將使用 Visual Studio 2008 Beta 2，而不是 Visual Web Developer Express，並將根據 Visual Studio 的使用者介面提供逐步解說。</span><span class="sxs-lookup"><span data-stu-id="c67f4-115">This whitepaper also assumes that you will be working with Visual Studio 2008 Beta 2, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="c67f4-116">有些程式碼範例可能會利用 Visual Web Developer Express 中無法使用的專案範本。</span><span class="sxs-lookup"><span data-stu-id="c67f4-116">Some code samples may utilize project templates unavailable in Visual Web Developer Express.</span></span>

## <a name="profiles-and-authentication"></a><span data-ttu-id="c67f4-117">*設定檔和驗證*</span><span class="sxs-lookup"><span data-stu-id="c67f4-117">*Profiles and Authentication*</span></span>

<span data-ttu-id="c67f4-118">Microsoft ASP.NET 設定檔和驗證服務是由 ASP.NET 表單驗證系統提供，而且是 ASP.NET 的標準元件。</span><span class="sxs-lookup"><span data-stu-id="c67f4-118">The Microsoft ASP.NET Profiles and Authentication services are provided by the ASP.NET Forms Authentication system, and are standard components of ASP.NET.</span></span> <span data-ttu-id="c67f4-119">ASP.NET AJAX 延伸模組透過腳本 proxy 提供這些服務的腳本存取，其方式是在用戶端 AJAX 程式庫的 Sys.databases 命名空間下相當簡單的模型。</span><span class="sxs-lookup"><span data-stu-id="c67f4-119">The ASP.NET AJAX Extensions provide script access to these services via script proxies, through a fairly straightforward model under the Sys.Services namespace of the client AJAX library.</span></span>

<span data-ttu-id="c67f4-120">驗證服務可讓使用者提供認證，以接收驗證 cookie，而是閘道服務，允許 ASP.NET 所提供的自訂使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="c67f4-120">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="c67f4-121">使用 ASP.NET AJAX authentication 服務與標準 ASP.NET 表單驗證相容，因此目前使用表單驗證的應用程式（例如使用登入控制項）不會因為升級至 AJAX 驗證服務而中斷。</span><span class="sxs-lookup"><span data-stu-id="c67f4-121">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

<span data-ttu-id="c67f4-122">設定檔服務可讓您根據驗證服務所提供的成員資格，自動整合和儲存使用者資料。</span><span class="sxs-lookup"><span data-stu-id="c67f4-122">The Profile service allows the automatic integration and storage of user data based on membership as provided by the Authentication service.</span></span> <span data-ttu-id="c67f4-123">儲存的資料是由 web.config 檔案所指定，而各種分析服務提供者會處理資料管理。</span><span class="sxs-lookup"><span data-stu-id="c67f4-123">The stored data is specified by the web.config file, and the various profiling service providers handle the data management.</span></span> <span data-ttu-id="c67f4-124">就像驗證服務一樣，AJAX 設定檔服務與標準的 ASP.NET 設定檔服務相容，因此包含 AJAX 支援的情況不應中斷目前納入 ASP.NET 設定檔服務功能的頁面。</span><span class="sxs-lookup"><span data-stu-id="c67f4-124">As with the Authentication service, the AJAX Profile service is compatible with the standard ASP.NET profile service, so that pages currently incorporating features of the ASP.NET Profile service should not be broken by including AJAX support.</span></span>

<span data-ttu-id="c67f4-125">將 ASP.NET Authentication 和分析服務本身合併到應用程式中，不在此白皮書的範圍內。</span><span class="sxs-lookup"><span data-stu-id="c67f4-125">Incorporating the ASP.NET Authentication and Profiling services themselves into an application is outside of the scope of this whitepaper.</span></span> <span data-ttu-id="c67f4-126">如需主題的詳細資訊，請參閱 MSDN Library 參考文章使用[https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)的成員資格來管理使用者。</span><span class="sxs-lookup"><span data-stu-id="c67f4-126">For more information on the topic, see the MSDN Library reference article Managing Users by Using Membership at [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx).</span></span> <span data-ttu-id="c67f4-127">ASP.NET 也包含一個公用程式，可自動設定 SQL Server 的成員資格，這是 ASP.NET 成員資格的預設驗證服務提供者。</span><span class="sxs-lookup"><span data-stu-id="c67f4-127">ASP.NET also includes a utility to automatically set up Membership with a SQL Server, which is the default authentication service provider for ASP.NET Membership.</span></span> <span data-ttu-id="c67f4-128">如需詳細資訊，請參閱[https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)的 ASP.NET SQL Server 註冊工具（Aspnet\_regsql 一文）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-128">For more information, see the article ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe) at [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).</span></span>

## <a name="using-the-aspnet-ajax-authentication-service"></a><span data-ttu-id="c67f4-129">*使用 ASP.NET AJAX Authentication 服務*</span><span class="sxs-lookup"><span data-stu-id="c67f4-129">*Using the ASP.NET AJAX Authentication Service*</span></span>

<span data-ttu-id="c67f4-130">ASP.NET AJAX Authentication 服務必須在 web.config 檔案中啟用：</span><span class="sxs-lookup"><span data-stu-id="c67f4-130">The ASP.NET AJAX Authentication service must be enabled in the web.config file:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

<span data-ttu-id="c67f4-131">驗證服務需要啟用 ASP.NET 表單驗證，而且必須在用戶端瀏覽器上啟用 cookie （因為無 cookie 的會話需要 URL 參數，所以腳本無法啟用無 cookie 的會話）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-131">The Authentication service requires ASP.NET Forms authentication to be enabled and requires cookies to be enabled on the client browser (a script cannot enable a cookieless session since cookieless sessions require URL parameters).</span></span>

<span data-ttu-id="c67f4-132">一旦啟用並設定 AJAX 驗證服務之後，用戶端腳本就可以立即利用 AuthenticationService 物件。</span><span class="sxs-lookup"><span data-stu-id="c67f4-132">Once the AJAX authentication service is enabled and configured, client script can immediately take advantage of the Sys.Services.AuthenticationService object.</span></span> <span data-ttu-id="c67f4-133">用戶端腳本主要會想要利用 `login` 方法和 `isLoggedIn` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-133">Primarily, client script will want to take advantage of the `login` method and `isLoggedIn` property.</span></span> <span data-ttu-id="c67f4-134">有數個屬性可提供登入方法的預設值，這可以接受大量的參數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-134">Several properties exist to provide defaults for the login method, which can accept a large number of parameters.</span></span>

<span data-ttu-id="c67f4-135">*AuthenticationService 成員*</span><span class="sxs-lookup"><span data-stu-id="c67f4-135">*Sys.Services.AuthenticationService members*</span></span>

<span data-ttu-id="c67f4-136">*登入方法：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-136">*login method:*</span></span>

<span data-ttu-id="c67f4-137">Login （）方法會開始驗證使用者認證的要求。</span><span class="sxs-lookup"><span data-stu-id="c67f4-137">The login() method begins a request to authenticate the user's credentials.</span></span> <span data-ttu-id="c67f4-138">這個方法是非同步，不會封鎖執行。</span><span class="sxs-lookup"><span data-stu-id="c67f4-138">This method is asynchronous and does not block execution.</span></span>

<span data-ttu-id="c67f4-139">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-139">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-140">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-140">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-141">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-141">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-142">userName</span><span class="sxs-lookup"><span data-stu-id="c67f4-142">userName</span></span> | <span data-ttu-id="c67f4-143">必要。</span><span class="sxs-lookup"><span data-stu-id="c67f4-143">Required.</span></span> <span data-ttu-id="c67f4-144">要驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c67f4-144">The username to authenticate.</span></span> |
| <span data-ttu-id="c67f4-145">密碼</span><span class="sxs-lookup"><span data-stu-id="c67f4-145">password</span></span> | <span data-ttu-id="c67f4-146">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-146">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-147">使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="c67f4-147">The user's password.</span></span> |
| <span data-ttu-id="c67f4-148">isPersistent</span><span class="sxs-lookup"><span data-stu-id="c67f4-148">isPersistent</span></span> | <span data-ttu-id="c67f4-149">選擇性（預設為 false）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-149">Optional (defaults to false).</span></span> <span data-ttu-id="c67f4-150">使用者的驗證 cookie 是否應跨會話保存。</span><span class="sxs-lookup"><span data-stu-id="c67f4-150">Whether the user's authentication cookie should persist across sessions.</span></span> <span data-ttu-id="c67f4-151">若為 false，則使用者會在瀏覽器關閉或會話到期時登出。</span><span class="sxs-lookup"><span data-stu-id="c67f4-151">If false, the user will log out when the browser is closed or the session expires.</span></span> |
| <span data-ttu-id="c67f4-152">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="c67f4-152">redirectUrl</span></span> | <span data-ttu-id="c67f4-153">選擇性（預設為 null）。驗證成功時，要將瀏覽器重新導向至的 URL。</span><span class="sxs-lookup"><span data-stu-id="c67f4-153">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="c67f4-154">如果此參數為 null 或空字串，則不會進行重新導向。</span><span class="sxs-lookup"><span data-stu-id="c67f4-154">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="c67f4-155">customInfo</span><span class="sxs-lookup"><span data-stu-id="c67f4-155">customInfo</span></span> | <span data-ttu-id="c67f4-156">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-156">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-157">此參數目前未使用，保留供未來使用。</span><span class="sxs-lookup"><span data-stu-id="c67f4-157">This parameter is currently unused and is reserved for future use.</span></span> |
| <span data-ttu-id="c67f4-158">loginCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-158">loginCompletedCallback</span></span> | <span data-ttu-id="c67f4-159">選擇性（預設為 null）。登入成功完成時所要呼叫的函數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-159">Optional (defaults to null).The function to call when the login has successfully completed.</span></span> <span data-ttu-id="c67f4-160">如果指定，這個參數會覆寫 defaultLoginCompleted 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-160">If specified, this parameter overrides the defaultLoginCompleted property.</span></span> |
| <span data-ttu-id="c67f4-161">failedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-161">failedCallback</span></span> | <span data-ttu-id="c67f4-162">選擇性（預設為 null）。登入失敗時所要呼叫的函數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-162">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="c67f4-163">如果指定，這個參數會覆寫 defaultFailedCallback 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-163">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="c67f4-164">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-164">userContext</span></span> | <span data-ttu-id="c67f4-165">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-165">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-166">應該傳遞至回呼函式的自訂使用者內容資料。</span><span class="sxs-lookup"><span data-stu-id="c67f4-166">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="c67f4-167">*傳回值：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-167">*Return Value:*</span></span>

<span data-ttu-id="c67f4-168">此函數不包含傳回值。</span><span class="sxs-lookup"><span data-stu-id="c67f4-168">This function does not include a return value.</span></span> <span data-ttu-id="c67f4-169">不過，完成呼叫此函式時，會包含一些行為：</span><span class="sxs-lookup"><span data-stu-id="c67f4-169">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="c67f4-170">如果 `redirectUrl` 參數既不是 null 也不是空字串，則會重新整理或變更目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="c67f4-170">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="c67f4-171">不過，如果參數為 null 或空字串，則會呼叫 `loginCompletedCallback` 參數或 `defaultLoginCompletedCallback` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-171">However, if the parameter was null or an empty string, the `loginCompletedCallback` parameter, or `defaultLoginCompletedCallback` property is called.</span></span>
- <span data-ttu-id="c67f4-172">如果 web 服務的呼叫失敗，則會呼叫 `defaultFailedCallback` 屬性的 `failedCallback` 參數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-172">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="c67f4-173">*登出方法：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-173">*logout method:*</span></span>

<span data-ttu-id="c67f4-174">登出（）方法會移除認證 cookie，並從 web 應用程式登出目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="c67f4-174">The logout() method removes the credentials cookie and logs out the current user from the web application.</span></span>

<span data-ttu-id="c67f4-175">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-175">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-176">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-176">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-177">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-177">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-178">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="c67f4-178">redirectUrl</span></span> | <span data-ttu-id="c67f4-179">選擇性（預設為 null）。驗證成功時，要將瀏覽器重新導向至的 URL。</span><span class="sxs-lookup"><span data-stu-id="c67f4-179">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="c67f4-180">如果此參數為 null 或空字串，則不會進行重新導向。</span><span class="sxs-lookup"><span data-stu-id="c67f4-180">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="c67f4-181">logoutCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-181">logoutCompletedCallback</span></span> | <span data-ttu-id="c67f4-182">選擇性（預設為 null）。成功完成登出時要呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-182">Optional (defaults to null).The function to call when the logout has successfully completed.</span></span> <span data-ttu-id="c67f4-183">如果指定，這個參數會覆寫 defaultLogoutCompleted 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-183">If specified, this parameter overrides the defaultLogoutCompleted property.</span></span> |
| <span data-ttu-id="c67f4-184">failedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-184">failedCallback</span></span> | <span data-ttu-id="c67f4-185">選擇性（預設為 null）。登入失敗時所要呼叫的函數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-185">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="c67f4-186">如果指定，這個參數會覆寫 defaultFailedCallback 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-186">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="c67f4-187">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-187">userContext</span></span> | <span data-ttu-id="c67f4-188">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-188">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-189">應該傳遞至回呼函式的自訂使用者內容資料。</span><span class="sxs-lookup"><span data-stu-id="c67f4-189">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="c67f4-190">*傳回值：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-190">*Return Value:*</span></span>

<span data-ttu-id="c67f4-191">此函數不包含傳回值。</span><span class="sxs-lookup"><span data-stu-id="c67f4-191">This function does not include a return value.</span></span> <span data-ttu-id="c67f4-192">不過，完成呼叫此函式時，會包含一些行為：</span><span class="sxs-lookup"><span data-stu-id="c67f4-192">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="c67f4-193">如果 `redirectUrl` 參數既不是 null 也不是空字串，則會重新整理或變更目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="c67f4-193">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="c67f4-194">不過，如果參數為 null 或空字串，則會呼叫 `logoutCompletedCallback` 參數或 `defaultLogoutCompletedCallback` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-194">However, if the parameter was null or an empty string, the `logoutCompletedCallback` parameter, or `defaultLogoutCompletedCallback` property is called.</span></span>
- <span data-ttu-id="c67f4-195">如果 web 服務的呼叫失敗，則會呼叫 `defaultFailedCallback` 屬性的 `failedCallback` 參數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-195">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="c67f4-196">*defaultFailedCallback 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-196">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="c67f4-197">如果無法與 web 服務通訊，則此屬性會指定應呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-197">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="c67f4-198">它應該會接收委派（或函數參考）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-198">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="c67f4-199">這個屬性所指定的函式參考應該具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="c67f4-199">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

<span data-ttu-id="c67f4-200">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-200">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-201">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-201">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-202">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-202">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-203">error</span><span class="sxs-lookup"><span data-stu-id="c67f4-203">error</span></span> | <span data-ttu-id="c67f4-204">指定錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-204">Specifies the error information.</span></span> |
| <span data-ttu-id="c67f4-205">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-205">userContext</span></span> | <span data-ttu-id="c67f4-206">指定呼叫 login 或登出函數時所提供的使用者內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-206">Specifies the user context information provided when the login or logout function was called.</span></span> |
| <span data-ttu-id="c67f4-207">methodName</span><span class="sxs-lookup"><span data-stu-id="c67f4-207">methodName</span></span> | <span data-ttu-id="c67f4-208">呼叫方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="c67f4-208">The name of the calling method.</span></span> |

<span data-ttu-id="c67f4-209">*defaultLoginCompletedCallback 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-209">*defaultLoginCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="c67f4-210">這個屬性會指定當登入 web 服務呼叫完成時，應該呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-210">This property specifies a function that should be called when the login web service call has completed.</span></span> <span data-ttu-id="c67f4-211">它應該會接收委派（或函數參考）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-211">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="c67f4-212">這個屬性所指定的函式參考應該具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="c67f4-212">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

<span data-ttu-id="c67f4-213">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-213">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-214">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-214">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-215">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-215">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-216">validCredentials</span><span class="sxs-lookup"><span data-stu-id="c67f4-216">validCredentials</span></span> | <span data-ttu-id="c67f4-217">指定使用者是否提供有效的認證。</span><span class="sxs-lookup"><span data-stu-id="c67f4-217">Specifies whether the user provided valid credentials.</span></span> <span data-ttu-id="c67f4-218">`true` 如果使用者成功登入，則為，否則 `false`。</span><span class="sxs-lookup"><span data-stu-id="c67f4-218">`true` if the user successfully logged in; otherwise `false`.</span></span> |
| <span data-ttu-id="c67f4-219">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-219">userContext</span></span> | <span data-ttu-id="c67f4-220">指定呼叫登入函數時所提供的使用者內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-220">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="c67f4-221">methodName</span><span class="sxs-lookup"><span data-stu-id="c67f4-221">methodName</span></span> | <span data-ttu-id="c67f4-222">呼叫方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="c67f4-222">The name of the calling method.</span></span> |

<span data-ttu-id="c67f4-223">*defaultLogoutCompletedCallback 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-223">*defaultLogoutCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="c67f4-224">這個屬性會指定當登出 web 服務呼叫完成時應該呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-224">This property specifies a function that should be called when the logout web service call has completed.</span></span> <span data-ttu-id="c67f4-225">它應該會接收委派（或函數參考）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-225">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="c67f4-226">這個屬性所指定的函式參考應該具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="c67f4-226">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

<span data-ttu-id="c67f4-227">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-227">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-228">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-228">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-229">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-229">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-230">result</span><span class="sxs-lookup"><span data-stu-id="c67f4-230">result</span></span> | <span data-ttu-id="c67f4-231">這個參數一律會 `null`。它會保留供日後使用。</span><span class="sxs-lookup"><span data-stu-id="c67f4-231">This parameter will always be `null`; it is reserved for future use.</span></span> |
| <span data-ttu-id="c67f4-232">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-232">userContext</span></span> | <span data-ttu-id="c67f4-233">指定呼叫登入函數時所提供的使用者內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-233">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="c67f4-234">methodName</span><span class="sxs-lookup"><span data-stu-id="c67f4-234">methodName</span></span> | <span data-ttu-id="c67f4-235">呼叫方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="c67f4-235">The name of the calling method.</span></span> |

<span data-ttu-id="c67f4-236">*isLoggedIn 屬性（get）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-236">*isLoggedIn property (get):*</span></span>

<span data-ttu-id="c67f4-237">這個屬性會取得使用者的目前驗證狀態。它是在頁面要求期間由 ScriptManager 物件所設定。</span><span class="sxs-lookup"><span data-stu-id="c67f4-237">This property gets the current authentication state of the user; it is set by the ScriptManager object during a page request.</span></span>

<span data-ttu-id="c67f4-238">如果使用者目前已登入，此屬性會傳回 `true`;否則，它會傳回 `false`。</span><span class="sxs-lookup"><span data-stu-id="c67f4-238">This property returns `true` if the user is currently logged in; otherwise, it returns `false`.</span></span>

<span data-ttu-id="c67f4-239">*path 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-239">*path property (get, set):*</span></span>

<span data-ttu-id="c67f4-240">這個屬性會以程式設計方式決定驗證 web 服務的位置。</span><span class="sxs-lookup"><span data-stu-id="c67f4-240">This property programmatically determines the location of the authentication web service.</span></span> <span data-ttu-id="c67f4-241">它可以用來覆寫預設驗證提供者，以及在 ScriptManager 控制項的 AuthenticationService 子節點的 Path 屬性中以宣告方式設定一個集合（如需詳細資訊，請參閱使用自訂驗證服務提供者主題）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-241">It can be used to override the default authentication provider, as well as one set declaratively in the Path property of the ScriptManager control's AuthenticationService child node (for more information, see the Using a Custom Authentication Service Provider topic below).</span></span>

<span data-ttu-id="c67f4-242">請注意，預設驗證服務的位置不會變更。</span><span class="sxs-lookup"><span data-stu-id="c67f4-242">Note that the location of the default authentication service does not change.</span></span> <span data-ttu-id="c67f4-243">不過，ASP.NET AJAX 可讓您指定 web 服務的位置，以提供與 ASP.NET AJAX authentication 服務 proxy 相同的類別介面。</span><span class="sxs-lookup"><span data-stu-id="c67f4-243">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="c67f4-244">另請注意，此屬性不應設定為將腳本要求從目前網站導向的值。</span><span class="sxs-lookup"><span data-stu-id="c67f4-244">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="c67f4-245">因為目前的應用程式不會收到驗證認證，所以不會有任何用處;此外，基礎 AJAX 的技術不應張貼跨網站要求，而且可能會在用戶端瀏覽器中產生安全性例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c67f4-245">Because the current application would not receive the authentication credentials, it would be useless; also, the technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="c67f4-246">這個屬性是一個 `String` 物件，代表驗證 web 服務的路徑。</span><span class="sxs-lookup"><span data-stu-id="c67f4-246">This property is a `String` object representing the path to the authentication web service.</span></span>

<span data-ttu-id="c67f4-247">*timeout 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-247">*timeout property (get, set):*</span></span>

<span data-ttu-id="c67f4-248">這個屬性會決定在假設登入要求失敗之前，等候驗證服務的時間長度。</span><span class="sxs-lookup"><span data-stu-id="c67f4-248">This property determines the length of time to wait for the authentication service before assuming the login request has failed.</span></span> <span data-ttu-id="c67f4-249">如果等候完成呼叫時，超時時間過期，將會呼叫要求失敗的回呼，而且呼叫將不會完成。</span><span class="sxs-lookup"><span data-stu-id="c67f4-249">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="c67f4-250">這個屬性是一個 `Number` 物件，代表等候驗證服務結果的毫秒數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-250">This property is a `Number` object representing the number of milliseconds to wait for results from the authentication service.</span></span>

<span data-ttu-id="c67f4-251">*程式碼範例：登入驗證服務*</span><span class="sxs-lookup"><span data-stu-id="c67f4-251">*Code Sample: Logging into the Authentication Service*</span></span>

<span data-ttu-id="c67f4-252">下列標記是一個範例 ASP.NET 網頁，其中包含對 AuthenticationService 類別的 login 和登出方法進行簡單的腳本呼叫。</span><span class="sxs-lookup"><span data-stu-id="c67f4-252">The following markup is an example ASP.NET page with a simple script call to the login and logout methods of the AuthenticationService class.</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a><span data-ttu-id="c67f4-253">透過 AJAX 存取 ASP.NET 分析資料</span><span class="sxs-lookup"><span data-stu-id="c67f4-253">Accessing ASP.NET Profiling Data via AJAX</span></span>

<span data-ttu-id="c67f4-254">ASP.NET 分析服務也會透過 ASP.NET AJAX 延伸模組公開。</span><span class="sxs-lookup"><span data-stu-id="c67f4-254">The ASP.NET profiling service is also exposed through the ASP.NET AJAX Extensions.</span></span> <span data-ttu-id="c67f4-255">由於 ASP.NET 分析服務提供豐富、細微的 API 來儲存和抓取使用者資料，因此這可能是絕佳的生產力工具。</span><span class="sxs-lookup"><span data-stu-id="c67f4-255">Since the ASP.NET profiling service provides a rich, granular API by which to store and retrieve user data, this can be an excellent productivity tool.</span></span>

<span data-ttu-id="c67f4-256">必須在 web.config 中啟用設定檔服務;預設值不是。</span><span class="sxs-lookup"><span data-stu-id="c67f4-256">The profile service must be enabled in web.config; it is not by default.</span></span> <span data-ttu-id="c67f4-257">若要這麼做，請確定 web.config 中的 `profileService` 子專案已啟用 = true，而且您已指定可以讀取或寫入哪些屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c67f4-257">To do so, ensure that the `profileService` child element has enabled= true specified in web.config, and that you have specified which properties can be read or written as follows:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

<span data-ttu-id="c67f4-258">您也必須設定設定檔服務。</span><span class="sxs-lookup"><span data-stu-id="c67f4-258">The profile service must also be configured.</span></span> <span data-ttu-id="c67f4-259">雖然分析服務的設定不在此白皮書的範圍內，但值得注意的是，設定檔設定中所定義的群組，將可作為組名的子屬性來存取。</span><span class="sxs-lookup"><span data-stu-id="c67f4-259">Although configuration of the profiling service is outside of the scope of this whitepaper, it is worthwhile to note that groups as defined in profile configuration settings will be accessible as sub-properties of the group name.</span></span> <span data-ttu-id="c67f4-260">例如，在指定了下列設定檔區段的情況下：</span><span class="sxs-lookup"><span data-stu-id="c67f4-260">For example, with the following profile section specified:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

<span data-ttu-id="c67f4-261">用戶端腳本可以存取 Name、Address、Line2、Address、City、Address、Address、.Zip 和 BackgroundColor 當做 ProfileService 類別的 properties 欄位屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-261">Client script would be able to access Name, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, and BackgroundColor as properties of the properties field of the ProfileService class.</span></span>

<span data-ttu-id="c67f4-262">一旦設定 AJAX 分析服務，它就會立即在頁面中提供;不過，在使用之前，必須載入一次。</span><span class="sxs-lookup"><span data-stu-id="c67f4-262">Once the AJAX Profiling Service is configured, it will be immediately available in pages; however, it will have to be loaded once before use.</span></span>

<span data-ttu-id="c67f4-263">*ProfileService 成員*</span><span class="sxs-lookup"><span data-stu-id="c67f4-263">*Sys.Services.ProfileService members*</span></span>

<span data-ttu-id="c67f4-264">*屬性欄位：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-264">*properties field:*</span></span>

<span data-ttu-id="c67f4-265">[屬性] 欄位會將所有已設定的設定檔資料公開為可由點運算子名稱慣例參考的子屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-265">The properties field exposes all configured profile data as child properties that can be referenced by the dot-operator-name convention.</span></span> <span data-ttu-id="c67f4-266">屬於屬性群組子系的屬性稱為 [PropertyName]。</span><span class="sxs-lookup"><span data-stu-id="c67f4-266">Properties that are children of property groups are referred to as GroupName.PropertyName.</span></span> <span data-ttu-id="c67f4-267">在上面顯示的範例設定檔設定中，若要取得使用者的狀態，您可以使用下列識別碼：</span><span class="sxs-lookup"><span data-stu-id="c67f4-267">In the example profile configuration presented above, to get the state of the user, you could use the following identifier:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

<span data-ttu-id="c67f4-268">*載入方法：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-268">*load method:*</span></span>

<span data-ttu-id="c67f4-269">從伺服器載入選取的清單或所有屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-269">Loads a selected list or all properties from the server.</span></span>

<span data-ttu-id="c67f4-270">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-270">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-271">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-271">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-272">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-273">之 propertynames</span><span class="sxs-lookup"><span data-stu-id="c67f4-273">propertyNames</span></span> | <span data-ttu-id="c67f4-274">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-274">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-275">要從伺服器載入的屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-275">The properties to be loaded from the server.</span></span> |
| <span data-ttu-id="c67f4-276">loadCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-276">loadCompletedCallback</span></span> | <span data-ttu-id="c67f4-277">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-277">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-278">載入完成時要呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-278">The function to call when loading has completed.</span></span> |
| <span data-ttu-id="c67f4-279">failedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-279">failedCallback</span></span> | <span data-ttu-id="c67f4-280">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-280">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-281">發生錯誤時所要呼叫的函數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-281">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="c67f4-282">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-282">userContext</span></span> | <span data-ttu-id="c67f4-283">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-283">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-284">要傳遞至回呼函式的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-284">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="c67f4-285">Load 函數沒有傳回值。</span><span class="sxs-lookup"><span data-stu-id="c67f4-285">The load function does not have a return value.</span></span> <span data-ttu-id="c67f4-286">如果呼叫成功完成，它會呼叫 `loadCompletedCallback` 參數或 `defaultLoadCompletedCallback` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-286">If the call completed successfully, it will call either the `loadCompletedCallback` parameter or `defaultLoadCompletedCallback` property.</span></span> <span data-ttu-id="c67f4-287">如果呼叫失敗，或超時時間已過期，則會呼叫 `failedCallback` 參數或 `defaultFailedCallback` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-287">If the call failed, or the timeout expired, either the `failedCallback` parameter or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="c67f4-288">如果未提供 `propertyNames` 參數，則會從伺服器中取出所有讀取設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-288">If the `propertyNames` parameter is not supplied, all read-configured properties are retrieved from the server.</span></span>

<span data-ttu-id="c67f4-289">*儲存方法：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-289">*save method:*</span></span>

<span data-ttu-id="c67f4-290">Save （）方法會將指定的屬性清單（或所有屬性）儲存至使用者的 ASP.NET 設定檔。</span><span class="sxs-lookup"><span data-stu-id="c67f4-290">The save() method saves the specified property list (or all properties) to the user's ASP.NET profile.</span></span>

<span data-ttu-id="c67f4-291">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-291">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-292">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-292">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-293">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-293">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-294">之 propertynames</span><span class="sxs-lookup"><span data-stu-id="c67f4-294">propertyNames</span></span> | <span data-ttu-id="c67f4-295">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-295">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-296">要儲存至伺服器的屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-296">The properties to be saved to the server.</span></span> |
| <span data-ttu-id="c67f4-297">saveCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-297">saveCompletedCallback</span></span> | <span data-ttu-id="c67f4-298">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-298">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-299">完成儲存時要呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-299">The function to call when saving has completed.</span></span> |
| <span data-ttu-id="c67f4-300">failedCallback</span><span class="sxs-lookup"><span data-stu-id="c67f4-300">failedCallback</span></span> | <span data-ttu-id="c67f4-301">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-301">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-302">發生錯誤時所要呼叫的函數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-302">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="c67f4-303">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-303">userContext</span></span> | <span data-ttu-id="c67f4-304">選擇性（預設為 null）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-304">Optional (defaults to null).</span></span> <span data-ttu-id="c67f4-305">要傳遞至回呼函式的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-305">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="c67f4-306">Save 函數沒有傳回值。</span><span class="sxs-lookup"><span data-stu-id="c67f4-306">The save function does not have a return value.</span></span> <span data-ttu-id="c67f4-307">如果呼叫成功完成，它會呼叫 `saveCompletedCallback` 參數或 `defaultSaveCompletedCallback` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-307">If the call completes successfully, it will call either the `saveCompletedCallback` parameter or `defaultSaveCompletedCallback` property.</span></span> <span data-ttu-id="c67f4-308">如果呼叫失敗，或超時時間已過期，則會呼叫 `failedCallback` 或 `defaultFailedCallback` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-308">If the call failed, or the timeout expired, either the `failedCallback` or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="c67f4-309">如果 `propertyNames` 參數是 null，則會將所有配置檔案屬性傳送至伺服器，而伺服器會決定可以儲存哪些屬性，哪些則不能。</span><span class="sxs-lookup"><span data-stu-id="c67f4-309">If the `propertyNames` parameter is null, all profile properties will be sent to the server, and the server will decide which properties can be saved and which cannot.</span></span>

<span data-ttu-id="c67f4-310">*defaultFailedCallback 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-310">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="c67f4-311">如果無法與 web 服務通訊，則此屬性會指定應呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-311">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="c67f4-312">它應該會接收委派（或函數參考）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-312">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="c67f4-313">這個屬性所指定的函式參考應該具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="c67f4-313">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

<span data-ttu-id="c67f4-314">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-314">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-315">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-315">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-316">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-316">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-317">錯誤</span><span class="sxs-lookup"><span data-stu-id="c67f4-317">Error</span></span> | <span data-ttu-id="c67f4-318">指定錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-318">Specifies the error information.</span></span> |
| <span data-ttu-id="c67f4-319">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-319">userContext</span></span> | <span data-ttu-id="c67f4-320">指定呼叫 load 或 save 函數時所提供的使用者內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-320">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="c67f4-321">methodName</span><span class="sxs-lookup"><span data-stu-id="c67f4-321">methodName</span></span> | <span data-ttu-id="c67f4-322">呼叫方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="c67f4-322">The name of the calling method.</span></span> |

<span data-ttu-id="c67f4-323">*defaultSaveCompleted 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-323">*defaultSaveCompleted property (get, set):*</span></span>

<span data-ttu-id="c67f4-324">這個屬性會指定在儲存使用者的設定檔資料時，應該呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-324">This property specifies a function that should be called upon the completion of saving the user's profile data.</span></span> <span data-ttu-id="c67f4-325">它應該會接收委派（或函數參考）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-325">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="c67f4-326">這個屬性所指定的函式參考應該具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="c67f4-326">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

<span data-ttu-id="c67f4-327">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-327">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-328">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-328">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-329">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-329">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-330">numPropsSaved</span><span class="sxs-lookup"><span data-stu-id="c67f4-330">numPropsSaved</span></span> | <span data-ttu-id="c67f4-331">指定已儲存的屬性數目。</span><span class="sxs-lookup"><span data-stu-id="c67f4-331">Specifies the number of properties that were saved.</span></span> |
| <span data-ttu-id="c67f4-332">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-332">userContext</span></span> | <span data-ttu-id="c67f4-333">指定呼叫 load 或 save 函數時所提供的使用者內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-333">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="c67f4-334">methodName</span><span class="sxs-lookup"><span data-stu-id="c67f4-334">methodName</span></span> | <span data-ttu-id="c67f4-335">呼叫方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="c67f4-335">The name of the calling method.</span></span> |

<span data-ttu-id="c67f4-336">*defaultLoadCompleted 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-336">*defaultLoadCompleted property (get, set):*</span></span>

<span data-ttu-id="c67f4-337">這個屬性會指定在使用者的設定檔資料載入完成時呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="c67f4-337">This property specifies a function that should be called upon the completion of loading of the user's profile data.</span></span> <span data-ttu-id="c67f4-338">它應該會接收委派（或函數參考）。</span><span class="sxs-lookup"><span data-stu-id="c67f4-338">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="c67f4-339">這個屬性所指定的函式參考應該具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="c67f4-339">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

<span data-ttu-id="c67f4-340">*參數：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-340">*Parameters:*</span></span>

| <span data-ttu-id="c67f4-341">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="c67f4-341">**Parameter Name**</span></span> | <span data-ttu-id="c67f4-342">**意義**</span><span class="sxs-lookup"><span data-stu-id="c67f4-342">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="c67f4-343">numPropsLoaded</span><span class="sxs-lookup"><span data-stu-id="c67f4-343">numPropsLoaded</span></span> | <span data-ttu-id="c67f4-344">指定已載入的屬性數目。</span><span class="sxs-lookup"><span data-stu-id="c67f4-344">Specifies the number of properties loaded.</span></span> |
| <span data-ttu-id="c67f4-345">userCoNtext</span><span class="sxs-lookup"><span data-stu-id="c67f4-345">userContext</span></span> | <span data-ttu-id="c67f4-346">指定呼叫 load 或 save 函數時所提供的使用者內容資訊。</span><span class="sxs-lookup"><span data-stu-id="c67f4-346">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="c67f4-347">methodName</span><span class="sxs-lookup"><span data-stu-id="c67f4-347">methodName</span></span> | <span data-ttu-id="c67f4-348">呼叫方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="c67f4-348">The name of the calling method.</span></span> |

<span data-ttu-id="c67f4-349">*path 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-349">*path property (get, set):*</span></span>

<span data-ttu-id="c67f4-350">這個屬性會以程式設計方式決定設定檔 web 服務的位置。</span><span class="sxs-lookup"><span data-stu-id="c67f4-350">This property programmatically determines the location of the profile web service.</span></span> <span data-ttu-id="c67f4-351">它可以用來覆寫預設的設定檔服務提供者，以及在 ScriptManager 控制項的 ProfileService 子節點的 Path 屬性中以宣告方式設定一個集合。</span><span class="sxs-lookup"><span data-stu-id="c67f4-351">It can be used to override the default profile service provider, as well as one set declaratively in the Path property of the ScriptManager control's ProfileService child node.</span></span>

<span data-ttu-id="c67f4-352">請注意，預設設定檔服務的位置不會變更。</span><span class="sxs-lookup"><span data-stu-id="c67f4-352">Note that the location of the default profile service does not change.</span></span> <span data-ttu-id="c67f4-353">不過，ASP.NET AJAX 可讓您指定 web 服務的位置，以提供與 ASP.NET AJAX authentication 服務 proxy 相同的類別介面。</span><span class="sxs-lookup"><span data-stu-id="c67f4-353">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="c67f4-354">另請注意，此屬性不應設定為將腳本要求從目前網站導向的值。</span><span class="sxs-lookup"><span data-stu-id="c67f4-354">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="c67f4-355">基礎 AJAX 的技術不應張貼跨網站要求，而且可能會在用戶端瀏覽器中產生安全性例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c67f4-355">The technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="c67f4-356">這個屬性是一個 `String` 物件，代表設定檔 web 服務的路徑。</span><span class="sxs-lookup"><span data-stu-id="c67f4-356">This property is a `String` object representing the path to the profile web service.</span></span>

<span data-ttu-id="c67f4-357">*timeout 屬性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-357">*timeout property (get, set):*</span></span>

<span data-ttu-id="c67f4-358">這個屬性會決定在假設載入或儲存要求失敗之前，等候設定檔服務的時間長度。</span><span class="sxs-lookup"><span data-stu-id="c67f4-358">This property determines the length of time to wait for the profile service before assuming the load or save request has failed.</span></span> <span data-ttu-id="c67f4-359">如果等候完成呼叫時，超時時間過期，將會呼叫要求失敗的回呼，而且呼叫將不會完成。</span><span class="sxs-lookup"><span data-stu-id="c67f4-359">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="c67f4-360">此屬性是一個 `Number` 物件，代表等候來自設定檔服務之結果的毫秒數。</span><span class="sxs-lookup"><span data-stu-id="c67f4-360">This property is a `Number` object representing the number of milliseconds to wait for results from the profile service.</span></span>

<span data-ttu-id="c67f4-361">*程式碼範例：在頁面載入時載入設定檔資料*</span><span class="sxs-lookup"><span data-stu-id="c67f4-361">*Code sample: Loading profile data at page load*</span></span>

<span data-ttu-id="c67f4-362">下列程式碼會檢查使用者是否已驗證，如果是，將會載入使用者慣用的背景色彩做為網頁的。</span><span class="sxs-lookup"><span data-stu-id="c67f4-362">The following code will check to see whether a user is authenticated, and if so, will load the user's preferred background color as the page's.</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a><span data-ttu-id="c67f4-363">*使用自訂驗證服務提供者*</span><span class="sxs-lookup"><span data-stu-id="c67f4-363">*Using a Custom Authentication Service Provider*</span></span>

<span data-ttu-id="c67f4-364">ASP.NET AJAX Extensions 可讓您透過自訂的 web 服務公開您的功能，以建立自訂腳本驗證服務提供者。</span><span class="sxs-lookup"><span data-stu-id="c67f4-364">The ASP.NET AJAX Extensions allow you to create a custom script authentication service provider by exposing your functionality through a custom web service.</span></span> <span data-ttu-id="c67f4-365">為了要使用，您的 web 服務必須公開兩個方法，`Login` 和 `Logout`;而且，您必須使用與預設 ASP.NET AJAX Authentication web 服務相同的方法簽章來指定這些方法。</span><span class="sxs-lookup"><span data-stu-id="c67f4-365">In order to be used, your web service must expose two methods, `Login` and `Logout`; and these methods must be specified with the same method signatures as the default ASP.NET AJAX Authentication web service.</span></span>

<span data-ttu-id="c67f4-366">建立自訂 web 服務之後，您必須以宣告方式在頁面上、程式碼中或透過用戶端腳本來指定它的路徑。</span><span class="sxs-lookup"><span data-stu-id="c67f4-366">Once you have created the custom web service, you will need to specify the path to it, either declaratively on your page, programmatically in code, or via the client script.</span></span>

<span data-ttu-id="c67f4-367">*若要以宣告方式設定路徑：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-367">*To set the path declaratively:*</span></span>

<span data-ttu-id="c67f4-368">若要以宣告方式設定路徑，請在 ASP.NET 網頁上包含 ScriptManager 物件的 AuthenticationService 子系：</span><span class="sxs-lookup"><span data-stu-id="c67f4-368">To set the path declaratively, include the AuthenticationService child of the ScriptManager object on your ASP.NET page:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

<span data-ttu-id="c67f4-369">*若要在程式碼中設定路徑：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-369">*To set the path in code:*</span></span>

<span data-ttu-id="c67f4-370">若要以程式設計方式設定路徑，請透過腳本管理員的實例指定路徑：</span><span class="sxs-lookup"><span data-stu-id="c67f4-370">To set the path programmatically, specify the path via the instance of your script manager:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

<span data-ttu-id="c67f4-371">*若要在腳本中設定路徑：*</span><span class="sxs-lookup"><span data-stu-id="c67f4-371">*To set the path in script:*</span></span>

<span data-ttu-id="c67f4-372">若要在腳本中以程式設計方式設定路徑，請利用 AuthenticationService 類別的 `path` 屬性：</span><span class="sxs-lookup"><span data-stu-id="c67f4-372">To set the path programmatically in script, utilize the `path` property of the AuthenticationService class:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

<span data-ttu-id="c67f4-373">*自訂驗證的範例 Web 服務*</span><span class="sxs-lookup"><span data-stu-id="c67f4-373">*Sample Web Service for Custom Authentication*</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a><span data-ttu-id="c67f4-374">總結</span><span class="sxs-lookup"><span data-stu-id="c67f4-374">Summary</span></span>

<span data-ttu-id="c67f4-375">ASP.NET 服務-特別是程式碼剖析、成員資格和驗證服務-可輕鬆地公開給用戶端瀏覽器上的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="c67f4-375">ASP.NET services - specifically the profiling, membership, and authentication services - are easily exposed to JavaScript on the client browser.</span></span> <span data-ttu-id="c67f4-376">這可讓開發人員順暢地將其用戶端程式代碼與驗證機制整合，而不需視 Updatepanel 之類的控制項來執行繁重的工作。</span><span class="sxs-lookup"><span data-stu-id="c67f4-376">This allows developers to integrate their client-side code with the authentication mechanism seamlessly, without depending on controls such as UpdatePanels to do the heavy lifting.</span></span> <span data-ttu-id="c67f4-377">您也可以利用 web 設定值，從用戶端保護分析資料。預設不提供任何資料，而開發人員必須加入宣告配置檔案屬性。</span><span class="sxs-lookup"><span data-stu-id="c67f4-377">Profile data can be protected from the client as well, by utilizing web configuration settings; no data is available by default, and developers must opt-in to profile properties.</span></span>

<span data-ttu-id="c67f4-378">此外，藉由建立具有對等方法簽章的簡化 web 服務，開發人員可以為這些內部 ASP.NET 服務建立自訂腳本提供者。</span><span class="sxs-lookup"><span data-stu-id="c67f4-378">Furthermore, by creating simplified web service implementations with equivalent method signatures, developers can create custom script providers for these intrinsic ASP.NET services.</span></span> <span data-ttu-id="c67f4-379">這些技術的支援簡化了豐富型用戶端應用程式的開發，同時為開發人員提供各種彈性來符合特定需求。</span><span class="sxs-lookup"><span data-stu-id="c67f4-379">Support for these techniques simplifies the development of rich client applications, while providing developers with a wide range of flexibility to meet specific needs.</span></span>

## <a name="bio"></a><span data-ttu-id="c67f4-380">*生物*</span><span class="sxs-lookup"><span data-stu-id="c67f4-380">*Bio*</span></span>

<span data-ttu-id="c67f4-381">Scott Cate 自1997起開始使用 Microsoft Web 技術，而這是 myKB.com （[www.myKB.com](http://www.myKB.com)）的總裁，他專門撰寫以 ASP.NET 為基礎的應用程式，著重于知識庫軟體解決方案。</span><span class="sxs-lookup"><span data-stu-id="c67f4-381">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="c67f4-382">Scott 可以透過電子郵件聯絡，位於[scott.cate@myKB.com](mailto:scott.cate@myKB.com)或他的[ScottCate.com](http://ScottCate.com)的 blog</span><span class="sxs-lookup"><span data-stu-id="c67f4-382">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c67f4-383">[上一頁](understanding-asp-net-ajax-updatepanel-triggers.md)
> [下一頁](understanding-asp-net-ajax-localization.md)</span><span class="sxs-lookup"><span data-stu-id="c67f4-383">[Previous](understanding-asp-net-ajax-updatepanel-triggers.md)
[Next](understanding-asp-net-ajax-localization.md)</span></span>
