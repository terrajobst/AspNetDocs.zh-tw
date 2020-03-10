---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: 使用 Windows 驗證驗證使用者（C#） |Microsoft Docs
author: microsoft
description: 瞭解如何在 MVC 應用程式的內容中使用 Windows 驗證。 您將瞭解如何在應用程式的 web co 中啟用 Windows 驗證 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bb3909bff2791c15a8737fc12cac69f79b55733f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624121"
---
# <a name="authenticating-users-with-windows-authentication-c"></a><span data-ttu-id="51764-104">使用 Windows 驗證驗證使用者 (C#)</span><span class="sxs-lookup"><span data-stu-id="51764-104">Authenticating Users with Windows Authentication (C#)</span></span>

<span data-ttu-id="51764-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="51764-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="51764-106">瞭解如何在 MVC 應用程式的內容中使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="51764-107">您將瞭解如何在應用程式的 web 設定檔中啟用 Windows 驗證，以及如何使用 IIS 設定驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="51764-108">最後，您將瞭解如何使用 [授權] 屬性來限制對特定 Windows 使用者或群組的控制器動作存取。</span><span class="sxs-lookup"><span data-stu-id="51764-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

<span data-ttu-id="51764-109">本教學課程的目的是要說明如何利用內建在 Internet Information Services 中的安全性功能，來保護 MVC 應用程式中的 views。</span><span class="sxs-lookup"><span data-stu-id="51764-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="51764-110">您將瞭解如何允許只有特定 Windows 使用者或特定 Windows 群組成員的使用者，才可以叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="51764-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="51764-111">當您要建立內部公司網站（內部網路網站），而且想要讓使用者能夠在存取網站時使用其標準 Windows 使用者名稱和密碼時，使用 Windows 驗證就很有意義。</span><span class="sxs-lookup"><span data-stu-id="51764-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="51764-112">如果您要建立向外面向網站（網際網路網站），請考慮改用表單驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="51764-113">啟用 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="51764-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="51764-114">當您建立新的 ASP.NET MVC 應用程式時，預設不會啟用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="51764-115">表單驗證是針對 MVC 應用程式啟用的預設驗證類型。</span><span class="sxs-lookup"><span data-stu-id="51764-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="51764-116">您必須藉由修改 MVC 應用程式的 web 設定（web.config）檔案來啟用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="51764-117">尋找 &lt;authentication&gt; 區段，並將它修改為使用 Windows，而不是像這樣的表單驗證：</span><span class="sxs-lookup"><span data-stu-id="51764-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

<span data-ttu-id="51764-118">當您啟用 Windows 驗證時，您的網頁伺服器會負責驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="51764-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="51764-119">一般來說，您在建立和部署 ASP.NET MVC 應用程式時，會使用兩種不同類型的 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="51764-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="51764-120">首先，在開發 MVC 應用程式時，您會使用 Visual Studio 隨附的 ASP.NET 開發 Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="51764-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="51764-121">根據預設，ASP.NET 開發 Web 服務器會執行目前 Windows 帳戶（您用來登入 Windows 的任何帳戶）內容中的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="51764-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="51764-122">ASP.NET 開發網頁伺服器也支援 NTLM 驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="51764-123">以滑鼠右鍵按一下 [方案總管] 視窗中的專案名稱，然後選取 [屬性]，即可啟用 NTLM 驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="51764-124">接下來，選取 [Web] 索引標籤並勾選 [NTLM] 核取方塊（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="51764-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="51764-125">**圖1–為 ASP.NET 開發 Web 服務器啟用 NTLM 驗證**</span><span class="sxs-lookup"><span data-stu-id="51764-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

<span data-ttu-id="51764-127">對於生產 web 應用程式，您可以使用 IIS 做為 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="51764-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="51764-128">IIS 支援數種類型的驗證，包括：</span><span class="sxs-lookup"><span data-stu-id="51764-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="51764-129">基本驗證–定義為 HTTP 1.0 通訊協定的一部分。</span><span class="sxs-lookup"><span data-stu-id="51764-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="51764-130">以純文字（Base64 編碼）傳送網際網路上的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="51764-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="51764-131">-摘要式驗證–透過網際網路傳送密碼雜湊，而不是密碼本身。</span><span class="sxs-lookup"><span data-stu-id="51764-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="51764-132">-整合式 Windows （NTLM）驗證–使用 Windows 在內部網路環境中使用的最佳驗證類型。</span><span class="sxs-lookup"><span data-stu-id="51764-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="51764-133">-憑證驗證–使用用戶端憑證來啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="51764-134">憑證會對應至 Windows 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="51764-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="51764-135">如需這些不同驗證類型的詳細總覽，請參閱[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。</span><span class="sxs-lookup"><span data-stu-id="51764-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>

<span data-ttu-id="51764-136">您可以使用 Internet Information Services 管理員來啟用特定類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="51764-137">請注意，所有類型的驗證在每個作業系統的情況下都不適用。</span><span class="sxs-lookup"><span data-stu-id="51764-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="51764-138">此外，如果您將 IIS 7.0 與 Windows Vista 搭配使用，您必須先啟用不同類型的 Windows 驗證，才會出現在 Internet Information Services 管理員中。</span><span class="sxs-lookup"><span data-stu-id="51764-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="51764-139">開啟 [**控制台]、[程式]、[程式和功能]、[開啟或關閉 Windows 功能**]，然後展開 [Internet Information Services] 節點（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="51764-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="51764-140">**[圖 2]-啟用 Windows IIS 功能**</span><span class="sxs-lookup"><span data-stu-id="51764-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

<span data-ttu-id="51764-142">使用 Internet Information Services，您可以啟用或停用不同類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="51764-143">例如，[圖 3] 說明如何停用匿名驗證，並在使用 IIS 7.0 時啟用整合式 Windows （NTLM）驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="51764-144">**[圖 3]-啟用整合式 Windows 驗證**</span><span class="sxs-lookup"><span data-stu-id="51764-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="51764-146">授權 Windows 使用者和群組</span><span class="sxs-lookup"><span data-stu-id="51764-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="51764-147">啟用 Windows 驗證之後，您可以使用 [授權] 屬性來控制控制器或控制器動作的存取權。</span><span class="sxs-lookup"><span data-stu-id="51764-147">After you enable Windows authentication, you can use the [Authorize] attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="51764-148">這個屬性可以套用至整個 MVC 控制器或特定的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="51764-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="51764-149">例如，[清單 1] 中的 Home 控制器會公開名為 Index （）、CompanySecrets （）和 StephenSecrets （）的三個動作。</span><span class="sxs-lookup"><span data-stu-id="51764-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="51764-150">任何人都可以叫用 Index （）動作。</span><span class="sxs-lookup"><span data-stu-id="51764-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="51764-151">不過，只有 Windows 本機管理員群組的成員可以叫用 CompanySecrets （）動作。</span><span class="sxs-lookup"><span data-stu-id="51764-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="51764-152">最後，只有名為 Stephen （位於 Redmond 網域）的 Windows 網域使用者，才能夠叫用 StephenSecrets （）動作。</span><span class="sxs-lookup"><span data-stu-id="51764-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="51764-153">**清單1– Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="51764-153">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="51764-154">由於 Windows 使用者帳戶控制（UAC），在使用 Windows Vista 或 Windows Server 2008 時，本機系統管理員群組的行為會與其他群組不同。</span><span class="sxs-lookup"><span data-stu-id="51764-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="51764-155">除非您修改電腦的 UAC 設定，否則 [授權] 屬性將不會正確辨識本機 Administrators 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="51764-155">The [Authorize] attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>

<span data-ttu-id="51764-156">當您嘗試叫用控制器動作而不是正確的許可權時，會發生什麼事，視啟用的驗證類型而定。</span><span class="sxs-lookup"><span data-stu-id="51764-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="51764-157">根據預設，使用 ASP.NET 程式開發伺服器時，您只會看到空白頁面。</span><span class="sxs-lookup"><span data-stu-id="51764-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="51764-158">此頁面提供**401 未授權**的 HTTP 回應狀態。</span><span class="sxs-lookup"><span data-stu-id="51764-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="51764-159">另一方面，如果您使用的 IIS 已停用匿名驗證，且已啟用基本驗證，則每次要求受保護的頁面時，都會持續取得登入對話方塊提示（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="51764-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="51764-160">**[圖 4]-基本驗證登入對話方塊**</span><span class="sxs-lookup"><span data-stu-id="51764-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="51764-162">總結</span><span class="sxs-lookup"><span data-stu-id="51764-162">Summary</span></span>

<span data-ttu-id="51764-163">本教學課程會說明如何在 ASP.NET MVC 應用程式的內容中使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="51764-164">您已瞭解如何在應用程式的 web 設定檔中啟用 Windows 驗證，以及如何使用 IIS 設定驗證。</span><span class="sxs-lookup"><span data-stu-id="51764-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="51764-165">最後，您已瞭解如何使用 [授權] 屬性來限制對特定 Windows 使用者或群組的控制器動作存取。</span><span class="sxs-lookup"><span data-stu-id="51764-165">Finally, you learned how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="51764-166">[上一頁](authenticating-users-with-forms-authentication-cs.md)
> [下一頁](preventing-javascript-injection-attacks-cs.md)</span><span class="sxs-lookup"><span data-stu-id="51764-166">[Previous](authenticating-users-with-forms-authentication-cs.md)
[Next](preventing-javascript-injection-attacks-cs.md)</span></span>
