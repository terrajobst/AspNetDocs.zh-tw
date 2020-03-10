---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 和 Web 工具2012.2 版本資訊 |Microsoft Docs
author: rick-anderson
description: ASP.NET 和 Web 工具2012.2 的版本資訊。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579517"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a><span data-ttu-id="36130-103">ASP.NET 和 Web 工具 2012.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="36130-103">ASP.NET and Web Tools 2012.2 Release Notes</span></span>

> <span data-ttu-id="36130-104">本檔說明 ASP.NET 和 Web 工具2012.2 的版本。</span><span class="sxs-lookup"><span data-stu-id="36130-104">This document describes the release of ASP.NET and Web Tools 2012.2.</span></span> <span data-ttu-id="36130-105">這是 Visual Studio Web 工具和 ASP.NET 的更新。</span><span class="sxs-lookup"><span data-stu-id="36130-105">It is an update to Visual Studio Web Tooling and ASP.NET.</span></span>

- [<span data-ttu-id="36130-106">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="36130-106">Installation Notes</span></span>](#_Installation)
- [<span data-ttu-id="36130-107">文件</span><span class="sxs-lookup"><span data-stu-id="36130-107">Documentation</span></span>](#_Documentation)
- [<span data-ttu-id="36130-108">支援</span><span class="sxs-lookup"><span data-stu-id="36130-108">Support</span></span>](#_Support)
- [<span data-ttu-id="36130-109">軟體需求</span><span class="sxs-lookup"><span data-stu-id="36130-109">Software Requirements</span></span>](#_Software_Requirements)
- [<span data-ttu-id="36130-110">ASP.NET 和 Web 工具2012.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="36130-110">New Features in ASP.NET and Web Tools 2012.2</span></span>](#_New_Features_in)

    - [<span data-ttu-id="36130-111">工具</span><span class="sxs-lookup"><span data-stu-id="36130-111">Tooling</span></span>](#_Tooling)
    - [<span data-ttu-id="36130-112">網頁發佈</span><span class="sxs-lookup"><span data-stu-id="36130-112">Web Publishing</span></span>](#_Web_Publishing)
    - [<span data-ttu-id="36130-113">ASP.NET MVC 範本</span><span class="sxs-lookup"><span data-stu-id="36130-113">ASP.NET MVC Templates</span></span>](#_Templates)
    - [<span data-ttu-id="36130-114">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="36130-114">ASP.NET Web API</span></span>](#_ASP.NET_Web_API)

    - [<span data-ttu-id="36130-115">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="36130-115">ASP.NET SignalR</span></span>](#_ASP.NET_SignalR)
    - [<span data-ttu-id="36130-116">ASP.NET 易記 Url</span><span class="sxs-lookup"><span data-stu-id="36130-116">ASP.NET Friendly URLs</span></span>](#_ASP.NET_Friendly_URLs)
- [<span data-ttu-id="36130-117">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="36130-117">Known Issues and Breaking Changes</span></span>](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a><span data-ttu-id="36130-118">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="36130-118">Installation Notes</span></span>

<span data-ttu-id="36130-119">您可以使用[Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)來安裝 Visual Studio 2012 的 ASP.NET 和 Web 工具2012.2。</span><span class="sxs-lookup"><span data-stu-id="36130-119">ASP.NET and Web Tools 2012.2 for Visual Studio 2012 can be installed using [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).</span></span> <span data-ttu-id="36130-120">這是 Visual Studio 2012 或 Visual Studio Express 2012 for Web 的更新，這是必要的。</span><span class="sxs-lookup"><span data-stu-id="36130-120">This is an update to Visual Studio 2012 or Visual Studio Express 2012 for Web, which is required.</span></span> <span data-ttu-id="36130-121">如果您未安裝 Visual Studio，將會安裝適用于 Web 的 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="36130-121">If you do not have Visual Studio installed, Visual Studio Express 2012 for Web will be installed.</span></span>

<span data-ttu-id="36130-122">您也可以手動安裝 ASP.NET 和 Web 工具2012.2。</span><span class="sxs-lookup"><span data-stu-id="36130-122">You can also install ASP.NET and Web Tools 2012.2 manually.</span></span> <span data-ttu-id="36130-123">您必須已安裝適用于 Web 的 Visual Studio 2012 或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="36130-123">You must have Visual Studio 2012 or Visual Studio Express 2012 for Web installed.</span></span> <span data-ttu-id="36130-124">然後使用下列指示：</span><span class="sxs-lookup"><span data-stu-id="36130-124">Then use the following instructions:</span></span> 

1. <span data-ttu-id="36130-125">從下載中心下載[ASP.NET 和 Web framework 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)安裝程式。</span><span class="sxs-lookup"><span data-stu-id="36130-125">Download [ASP.NET and Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer from Download Center.</span></span>
2. <span data-ttu-id="36130-126">出現提示時，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="36130-126">When prompted click Run.</span></span> <span data-ttu-id="36130-127">您也可以儲存檔案，以便稍後執行。</span><span class="sxs-lookup"><span data-stu-id="36130-127">You can also save the file to run it later.</span></span>
3. <span data-ttu-id="36130-128">確認您要更新的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="36130-128">Verify the version of Visual Studio you will update.</span></span> <span data-ttu-id="36130-129">您可以藉由啟動您想要更新的 Visual Studio 來完成這項操作。</span><span class="sxs-lookup"><span data-stu-id="36130-129">You can do this by launching the Visual Studio you wish to update.</span></span> <span data-ttu-id="36130-130">然後按一下 [說明] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="36130-130">Then click the Help menu item.</span></span>   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. <span data-ttu-id="36130-131">如果您看到功能表項目 &quot;關於 Web&quot; 的 Microsoft Visual Studio 2012，請下載 web[開發人員工具 2012.2-Visual Studio Express 2012 For web](https://go.microsoft.com/fwlink/?LinkID=282228)。</span><span class="sxs-lookup"><span data-stu-id="36130-131">If you see the menu item &quot;About Microsoft Visual Studio 2012 for Web&quot; then download [Web Developer Tools 2012.2 - Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span> <span data-ttu-id="36130-132">否則，請下載[Web Developer Tools 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)。</span><span class="sxs-lookup"><span data-stu-id="36130-132">Otherwise download [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span>
5. <span data-ttu-id="36130-133">出現提示時，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="36130-133">When prompted click Run.</span></span> <span data-ttu-id="36130-134">您也可以儲存檔案，以便稍後執行。</span><span class="sxs-lookup"><span data-stu-id="36130-134">You can also save the file to run it later.</span></span>

> [!NOTE]
> <span data-ttu-id="36130-135">ASP.NET 和 Web 工具2012.2 版本不包含 SQL Server Data Tools。</span><span class="sxs-lookup"><span data-stu-id="36130-135">ASP.NET and Web Tools 2012.2 release does not include SQL Server Data Tools.</span></span> <span data-ttu-id="36130-136">SQL Server 和 Windows Azure SQL database 提供一組更豐富的資料庫工具，包括離線專案支援的開發、架構比較和增強的資料庫部署功能。</span><span class="sxs-lookup"><span data-stu-id="36130-136">SQL Server and Windows Azure SQL Databases provides a richer set of database tooling including offline project-backed development, schema comparison and enhanced database deployment capabilities.</span></span> <span data-ttu-id="36130-137">如需詳細資訊或安裝 SQL Server Data Tools 流覽[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)。</span><span class="sxs-lookup"><span data-stu-id="36130-137">For more information or to install SQL Server Data Tools visit [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).</span></span>

<a id="_Documentation"></a>
## <a name="documentation"></a><span data-ttu-id="36130-138">文件</span><span class="sxs-lookup"><span data-stu-id="36130-138">Documentation</span></span>

<span data-ttu-id="36130-139">您可以從 ASP.NET 網站（ https://www.asp.net)取得 ASP.NET 和 Web 工具2012.2 的教學課程和其他資訊。</span><span class="sxs-lookup"><span data-stu-id="36130-139">Tutorials and other information about ASP.NET and Web Tools 2012.2 are available from ASP.NET web site ( https://www.asp.net).</span></span>

<a id="_Support"></a>
## <a name="support"></a><span data-ttu-id="36130-140">支援</span><span class="sxs-lookup"><span data-stu-id="36130-140">Support</span></span>

<span data-ttu-id="36130-141">ASP.NET 和 Web 工具2012.2 已正式發行並受到支援。</span><span class="sxs-lookup"><span data-stu-id="36130-141">ASP.NET and Web Tools 2012.2 is officially released and supported.</span></span> <span data-ttu-id="36130-142">您可以使用您的一般支援通道。</span><span class="sxs-lookup"><span data-stu-id="36130-142">You can use your normal support channel.</span></span> <span data-ttu-id="36130-143">您也可以將問題張貼至 ASP.NET 論壇（[https://forums.asp.net/](https://forums.asp.net/)），其中 ASP.NET 社區的成員經常能夠提供非正式的支援。</span><span class="sxs-lookup"><span data-stu-id="36130-143">You can also post questions to the ASP.NET forums ([https://forums.asp.net/](https://forums.asp.net/)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="36130-144">軟體需求</span><span class="sxs-lookup"><span data-stu-id="36130-144">Software Requirements</span></span>

<span data-ttu-id="36130-145">ASP.NET 和 Web 工具2012.2 需要 Web 的 Visual Studio 2012 或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="36130-145">The ASP.NET and Web Tools 2012.2 requires Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a><span data-ttu-id="36130-146">ASP.NET 和 Web 工具2012.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="36130-146">New Features in ASP.NET and Web Tools 2012.2</span></span>

<span data-ttu-id="36130-147">本節說明 ASP.NET 和 Web 工具2012.2 版本中引進的功能。</span><span class="sxs-lookup"><span data-stu-id="36130-147">This section describes features that have been introduced in the ASP.NET and Web Tools 2012.2 release.</span></span>

<a id="_Tooling"></a>
### <a name="tooling"></a><span data-ttu-id="36130-148">Tooling</span><span class="sxs-lookup"><span data-stu-id="36130-148">Tooling</span></span>

- <span data-ttu-id="36130-149">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="36130-149">Page Inspector</span></span> 

    - <span data-ttu-id="36130-150">支援 JavaScript 選取對應可讓 Page Inspector 將以動態方式新增至頁面的專案對應回相對應的 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="36130-150">Support JavaScript selection mapping allowing Page Inspector to map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span>
    - <span data-ttu-id="36130-151">即時查看 CSS 更新的功能。</span><span class="sxs-lookup"><span data-stu-id="36130-151">The ability to see CSS updates in real-time.</span></span>
    - <span data-ttu-id="36130-152">如需詳細資訊，請參閱[Page Inspector 中的 CSS 自動同步處理和 JavaScript 選取對應](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。</span><span class="sxs-lookup"><span data-stu-id="36130-152">For more information, read [CSS Auto-Sync and JavaScript Selection Mapping in Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).</span></span>
- <span data-ttu-id="36130-153">編輯器</span><span class="sxs-lookup"><span data-stu-id="36130-153">Editor</span></span> 

    - <span data-ttu-id="36130-154">支援 CoffeeScript、Mustache、Handlebars 和 JsRender 的語法醒目提示。</span><span class="sxs-lookup"><span data-stu-id="36130-154">Support syntax highlighting for CoffeeScript, Mustache, Handlebars, and JsRender.</span></span>
    - <span data-ttu-id="36130-155">HTML 編輯器會提供 Intellisense 來進行挖結系結。</span><span class="sxs-lookup"><span data-stu-id="36130-155">The HTML editor provides Intellisense for Knockout bindings.</span></span>
    - <span data-ttu-id="36130-156">較少的編輯和編譯器支援，可讓您使用較少的建立動態 CSS。</span><span class="sxs-lookup"><span data-stu-id="36130-156">LESS editing and compiler support to enable building dynamic CSS using LESS.</span></span>
    - <span data-ttu-id="36130-157">將 JSON 貼入 .NET 類別。</span><span class="sxs-lookup"><span data-stu-id="36130-157">Paste JSON as a .NET class.</span></span> <span data-ttu-id="36130-158">使用這個特殊的 [貼上] 命令將C# JSON 貼入或 VB.NET 程式碼檔案中，Visual Studio 會自動產生從 JSON 推斷的 .net 類別。</span><span class="sxs-lookup"><span data-stu-id="36130-158">Using this Special Paste command to paste JSON into a C# or VB.NET code file, and Visual Studio will automatically generate .NET classes inferred from the JSON.</span></span>
- <span data-ttu-id="36130-159">行動模擬器支援新增擴充性攔截，讓協力廠商模擬器可以安裝為 VSIX。</span><span class="sxs-lookup"><span data-stu-id="36130-159">Mobile Emulator support adds extensibility hooks so that third-party emulators can be installed as a VSIX.</span></span> <span data-ttu-id="36130-160">已安裝的模擬器會顯示在 F5 下拉式清單中，讓開發人員可以在各種行動裝置上預覽其網站。</span><span class="sxs-lookup"><span data-stu-id="36130-160">The installed emulators will show up in the F5 dropdown, so that developers can preview their websites on a variety of mobile devices.</span></span> <span data-ttu-id="36130-161">如需這項功能的詳細資訊，請參閱 Scott Hanselman 在[與 Visual Studio 的新 BrowserStack 整合](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)的 blog 專案。</span><span class="sxs-lookup"><span data-stu-id="36130-161">Read more about this feature in Scott Hanselman's blog entry on [the new BrowserStack integration with Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).</span></span>

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a><span data-ttu-id="36130-162">Web Publishing</span><span class="sxs-lookup"><span data-stu-id="36130-162">Web Publishing</span></span>

- <span data-ttu-id="36130-163">網站專案現在具有與 Web 應用程式專案相同的發佈體驗，包括發行至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="36130-163">Web site projects now have the same publishing experience as Web Application projects including publishing to Windows Azure Web Sites.</span></span>
- <span data-ttu-id="36130-164">選擇性發佈&#8211;一或多個檔案您可以執行下列動作（發佈至 Web Deploy 端點之後）：</span><span class="sxs-lookup"><span data-stu-id="36130-164">Selective publish &#8211; for one or more files you can perform the following actions (after publishing to a Web Deploy endpoint):</span></span> 

    - <span data-ttu-id="36130-165">發行選取的檔案。</span><span class="sxs-lookup"><span data-stu-id="36130-165">Publish selected files.</span></span>
    - <span data-ttu-id="36130-166">查看本機檔案與遠端檔案之間的差異。</span><span class="sxs-lookup"><span data-stu-id="36130-166">See the difference between a local file and a remote file.</span></span>
    - <span data-ttu-id="36130-167">以遠端檔案更新本機檔案，或使用本機檔案更新遠端檔案。</span><span class="sxs-lookup"><span data-stu-id="36130-167">Update the local file with the remote file or update the remote file with the local file.</span></span>

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a><span data-ttu-id="36130-168">ASP.NET MVC 範本</span><span class="sxs-lookup"><span data-stu-id="36130-168">ASP.NET MVC Templates</span></span>

- <span data-ttu-id="36130-169">全新的 Facebook 應用程式範本可讓撰寫 Facebook Canvas 應用程式再容易不過了。</span><span class="sxs-lookup"><span data-stu-id="36130-169">The new Facebook Application template makes writing Facebook Canvas applications easy.</span></span> <span data-ttu-id="36130-170">只需幾個簡單的步驟，您便可建立 Facebook 應用程式，進而取得已登入使用者的資料並將資料與他的朋友進行整合。</span><span class="sxs-lookup"><span data-stu-id="36130-170">In a few simple steps, you can create a Facebook application that gets data from a logged in user and integrates with their friends.</span></span> <span data-ttu-id="36130-171">此範本包括一個新程式庫，處理建置 Facebook 應用程式時所涉及的所有連結，包括授權、權限、存取 Facebook 資料等等。</span><span class="sxs-lookup"><span data-stu-id="36130-171">The template includes a new library to take care of all the plumbing involved in building a Facebook app, including authentication, permissions, accessing Facebook data and more.</span></span> <span data-ttu-id="36130-172">如需使用 Facebook 應用程式範本的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)。</span><span class="sxs-lookup"><span data-stu-id="36130-172">For more information on using the Facebook Application template see [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).</span></span>
- <span data-ttu-id="36130-173">全新的單一網頁應用程式 MVC 範本可讓開發人員使用 HTML 5、CSS 3 和熱門的 Knockout 與 jQuery JavaScript 程式庫，在 ASP.NET Web API 的基礎上建置互動式用戶端 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="36130-173">A new Single Page Application MVC template allows developers to build interactive client-side web apps using HTML 5, CSS 3, and the popular Knockout and jQuery JavaScript libraries, on top of ASP.NET Web API.</span></span> <span data-ttu-id="36130-174">此範本包含「待辦事項」清單應用程式，其中示範建立使用 RESTful 伺服器 API 之 JavaScript HTML5 應用程式的常見作法。</span><span class="sxs-lookup"><span data-stu-id="36130-174">The template includes a "todo" list application that demonstrates common practices for building a JavaScript HTML5 application that uses a RESTful server API.</span></span> <span data-ttu-id="36130-175">您可以在[https://www.asp.net/single-page-application](../../../single-page-application/index.md)閱讀更多。</span><span class="sxs-lookup"><span data-stu-id="36130-175">You can read more at [https://www.asp.net/single-page-application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="36130-176">您現在可以建立 VSIX，將新的範本新增至 [ASP.NET MVC 新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="36130-176">You can now create a VSIX that adds new templates to the ASP.NET MVC New Project dialog.</span></span> <span data-ttu-id="36130-177">瞭解做法： [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span><span class="sxs-lookup"><span data-stu-id="36130-177">Learn how here: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span></span>
- <span data-ttu-id="36130-178">FixedDisplayModes 套件&#8211; MVC 專案範本已更新為包含新的 ' FixedDisplayModes ' NuGet 套件，其中包含 MVC 4 中 bug 的因應措施。</span><span class="sxs-lookup"><span data-stu-id="36130-178">FixedDisplayModes package &#8211; MVC project templates have been updated to include the new ‘FixedDisplayModes' NuGet package, which contains a workaround for a bug in MVC 4.</span></span> <span data-ttu-id="36130-179">如需封裝中包含之修正的詳細資訊，請參閱 MVC 小組的這篇 blog 文章（[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="36130-179">For more information on the fix contained in the package, refer to this blog post ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) from the MVC team.</span></span>

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="36130-180">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="36130-180">ASP.NET Web API</span></span>

<span data-ttu-id="36130-181">ASP.NET Web API 已透過數個新功能增強：</span><span class="sxs-lookup"><span data-stu-id="36130-181">ASP.NET Web API has been enhanced with several new features:</span></span>

- <span data-ttu-id="36130-182">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="36130-182">ASP.NET Web API OData</span></span>
- <span data-ttu-id="36130-183">ASP.NET Web API 追蹤</span><span class="sxs-lookup"><span data-stu-id="36130-183">ASP.NET Web API Tracing</span></span>
- <span data-ttu-id="36130-184">ASP.NET Web API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="36130-184">ASP.NET Web API Help Page</span></span>

#### <a name="aspnet-web-api-odata"></a><span data-ttu-id="36130-185">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="36130-185">ASP.NET Web API OData</span></span>

<span data-ttu-id="36130-186">ASP.NET Web API OData 提供您在任何資料來源上使用豐富商務邏輯建立 OData 端點所需的彈性。</span><span class="sxs-lookup"><span data-stu-id="36130-186">ASP.NET Web API OData gives you the flexibility you need to build OData endpoints with rich business logic over any data source.</span></span> <span data-ttu-id="36130-187">有了 ASP.NET Web API OData，您就可以控制要公開的 OData 語義數量。</span><span class="sxs-lookup"><span data-stu-id="36130-187">With ASP.NET Web API OData you control the amount of OData semantics that you want to expose.</span></span> <span data-ttu-id="36130-188">ASP.NET Web API OData 隨附于 ASP.NET MVC 4 專案範本，而且也可以從 NuGet （[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)）取得。</span><span class="sxs-lookup"><span data-stu-id="36130-188">ASP.NET Web API OData is included with the ASP.NET MVC 4 project templates and is also available from NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span></span>

<span data-ttu-id="36130-189">ASP.NET Web API OData 目前支援下列功能：</span><span class="sxs-lookup"><span data-stu-id="36130-189">ASP.NET Web API OData currently supports the following features:</span></span>

- <span data-ttu-id="36130-190">套用 [可查詢] 屬性來啟用 OData 查詢語義。</span><span class="sxs-lookup"><span data-stu-id="36130-190">Enable OData query semantics by applying the [Queryable] attribute.</span></span>
- <span data-ttu-id="36130-191">輕鬆驗證 OData 查詢，並限制支援的查詢選項、運算子和函式的集合。</span><span class="sxs-lookup"><span data-stu-id="36130-191">Easily validate OData queries and restrict the set of supported query options, operators and functions.</span></span>
- <span data-ttu-id="36130-192">參數系結至直接 ODataQueryOptions，以取得查詢的抽象語法樹狀結構標記法，然後可以驗證並套用至 IQueryable 或 IEnumerable。</span><span class="sxs-lookup"><span data-stu-id="36130-192">Parameter bind to ODataQueryOptions directly to get an abstract syntax tree representation of the query that can then be validated and applied to an IQueryable or IEnumerable.</span></span>
- <span data-ttu-id="36130-193">藉由指定 [可查詢] 屬性的結果限制，啟用服務導向分頁和下一頁連結產生。</span><span class="sxs-lookup"><span data-stu-id="36130-193">Enable service-driven paging and next page link generation by specifying result limits on [Queryable] attribute.</span></span>
- <span data-ttu-id="36130-194">使用 $inlinecount，要求相符資源總數的內嵌計數。</span><span class="sxs-lookup"><span data-stu-id="36130-194">Request an inlined count of the total number of matching resources using $inlinecount.</span></span>
- <span data-ttu-id="36130-195">控制 null 傳播。</span><span class="sxs-lookup"><span data-stu-id="36130-195">Control null propagation.</span></span>
- <span data-ttu-id="36130-196">$Filter 中的任何/所有運算子。</span><span class="sxs-lookup"><span data-stu-id="36130-196">Any/All operators in $filter.</span></span>
- <span data-ttu-id="36130-197">依照慣例推斷實體資料模型，或明確自訂模型，其方式類似于 Entity Framework 程式碼優先。</span><span class="sxs-lookup"><span data-stu-id="36130-197">Infer an entity data model by convention or explicitly customize a model in a manner similar to Entity Framework Code-First.</span></span>
- <span data-ttu-id="36130-198">藉由衍生自 EntitySetController 來公開實體集。</span><span class="sxs-lookup"><span data-stu-id="36130-198">Expose entity sets by deriving from EntitySetController.</span></span>
- <span data-ttu-id="36130-199">簡單、可自訂的慣例，用來公開導覽屬性、操作連結和執行 OData 動作。</span><span class="sxs-lookup"><span data-stu-id="36130-199">Simple, customizable conventions for exposing navigation properties, manipulating links and implementing OData actions.</span></span>
- <span data-ttu-id="36130-200">使用 MapODataRoute 擴充方法簡化路由。</span><span class="sxs-lookup"><span data-stu-id="36130-200">Simplified routing using the MapODataRoute extension method.</span></span>
- <span data-ttu-id="36130-201">藉由公開多個 EDM 模型來支援版本控制。</span><span class="sxs-lookup"><span data-stu-id="36130-201">Support for versioning by exposing multiple EDM models.</span></span>
- <span data-ttu-id="36130-202">公開服務檔和 $metadata，讓您可以為 Web API 產生用戶端（.NET、Windows Phone、Windows Store 等等）。</span><span class="sxs-lookup"><span data-stu-id="36130-202">Expose service document and $metadata so you can generate clients (.NET, Windows Phone, Windows Store, etc.) for your Web API.</span></span>
- <span data-ttu-id="36130-203">支援 OData Atom、JSON 和 JSON 詳細資訊格式。</span><span class="sxs-lookup"><span data-stu-id="36130-203">Support for the OData Atom, JSON, and JSON verbose formats.</span></span>
- <span data-ttu-id="36130-204">建立、更新、部分更新（PATCH）和刪除實體。</span><span class="sxs-lookup"><span data-stu-id="36130-204">Create, update, partially update (PATCH) and delete entities.</span></span>
- <span data-ttu-id="36130-205">查詢和操作實體之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="36130-205">Query and manipulate relationships between entities.</span></span>
- <span data-ttu-id="36130-206">建立連接到您的路由的關聯性連結。</span><span class="sxs-lookup"><span data-stu-id="36130-206">Create relationship links that wire up to your routes.</span></span>
- <span data-ttu-id="36130-207">複雜類型。</span><span class="sxs-lookup"><span data-stu-id="36130-207">Complex types.</span></span>
- <span data-ttu-id="36130-208">實體類型繼承。</span><span class="sxs-lookup"><span data-stu-id="36130-208">Entity Type Inheritance.</span></span>
- <span data-ttu-id="36130-209">集合屬性。</span><span class="sxs-lookup"><span data-stu-id="36130-209">Collection properties.</span></span>
- <span data-ttu-id="36130-210">列舉.</span><span class="sxs-lookup"><span data-stu-id="36130-210">Enums.</span></span>
- <span data-ttu-id="36130-211">OData 動作。</span><span class="sxs-lookup"><span data-stu-id="36130-211">OData actions.</span></span>
- <span data-ttu-id="36130-212">建基於與 WCF Data Services 相同的基礎，亦即 ODataLib （[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)）。</span><span class="sxs-lookup"><span data-stu-id="36130-212">Built upon the same foundation as WCF Data Services, namely ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span></span>

<span data-ttu-id="36130-213">如需 ASP.NET Web API OData 的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)。</span><span class="sxs-lookup"><span data-stu-id="36130-213">For more information on ASP.NET Web API OData see [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).</span></span>

#### <a name="aspnet-web-api-tracing"></a><span data-ttu-id="36130-214">ASP.NET Web API 追蹤</span><span class="sxs-lookup"><span data-stu-id="36130-214">ASP.NET Web API Tracing</span></span>

<span data-ttu-id="36130-215">ASP.NET Web API 追蹤會使用 .NET 追蹤來整合 Web Api 的追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="36130-215">ASP.NET Web API Tracing integrates tracing data from your web APIs with .NET Tracing.</span></span> <span data-ttu-id="36130-216">在 Web API 專案範本中，它現在會預設為啟用。</span><span class="sxs-lookup"><span data-stu-id="36130-216">It is now enabled by default in the Web API project template.</span></span> <span data-ttu-id="36130-217">Web Api 的追蹤資料會傳送至 [輸出] 視窗，並可透過 IntelliTrace 取得。</span><span class="sxs-lookup"><span data-stu-id="36130-217">Tracing data for your web APIs is sent to the Output window and is made available through IntelliTrace.</span></span> <span data-ttu-id="36130-218">ASP.NET Web API 追蹤可讓您在 Windows Azure 上透過與[windows Azure 診斷](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)的整合，追蹤 Web API 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="36130-218">ASP.NET Web API Tracing enables you to trace information about your Web API when hosted on Windows Azure through integration with [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx).</span></span> <span data-ttu-id="36130-219">您也可以使用 ASP.NET Web API 追蹤 NuGet 套件（[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)），在任何應用程式中安裝並啟用 ASP.NET Web API 追蹤。</span><span class="sxs-lookup"><span data-stu-id="36130-219">You can also install and enable ASP.NET Web API Tracing in any application using the ASP.NET Web API Tracing NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span></span>

<span data-ttu-id="36130-220">如需設定和使用 ASP.NET Web API 追蹤的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)。</span><span class="sxs-lookup"><span data-stu-id="36130-220">For more information on configuring and using ASP.NET Web API Tracing see [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).</span></span>

#### <a name="aspnet-web-api-help-page"></a><span data-ttu-id="36130-221">ASP.NET Web API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="36130-221">ASP.NET Web API Help Page</span></span>

<span data-ttu-id="36130-222">[ASP.NET Web API 說明] 頁面現在預設會包含在 [Web API] 專案範本中。</span><span class="sxs-lookup"><span data-stu-id="36130-222">The ASP.NET Web API Help Page is now included by default in the Web API project template.</span></span> <span data-ttu-id="36130-223">[ASP.NET Web API 說明] 頁面會自動產生 Web Api 的檔，包括 HTTP 端點、支援的 HTTP 方法、參數和範例要求和回應訊息裝載。</span><span class="sxs-lookup"><span data-stu-id="36130-223">The ASP.NET Web API Help Page automatically generates documentation for web APIs including the HTTP endpoints, the supported HTTP methods, parameters and example request and response message payloads.</span></span> <span data-ttu-id="36130-224">檔會自動從您程式碼中的批註提取。</span><span class="sxs-lookup"><span data-stu-id="36130-224">Documentation is automatically pulled from comments in your code.</span></span> <span data-ttu-id="36130-225">您也可以使用 ASP.NET Web API 說明頁面 NuGet 套件（[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)），將 ASP.NET Web API 說明頁新增至任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="36130-225">You can also add the ASP.NET Web API Help Page to any application using the ASP.NET Web API Help Page NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span></span>

<span data-ttu-id="36130-226">如需設定和自訂 ASP.NET Web API [說明] 頁面的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)。</span><span class="sxs-lookup"><span data-stu-id="36130-226">For more information on setting up and customizing the ASP.NET Web API Help Page see [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).</span></span>

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a><span data-ttu-id="36130-227">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="36130-227">ASP.NET SignalR</span></span>

<span data-ttu-id="36130-228">ASP.NET SignalR 可讓您輕鬆地將即時 web 功能新增至您的 ASP.NET 應用程式，使用 Websocket （如果有的話），並在沒有時自動回復至其他技術。</span><span class="sxs-lookup"><span data-stu-id="36130-228">ASP.NET SignalR makes it simple to add real-time web capabilities to your ASP.NET application, using WebSockets if available and automatically falling back to other techniques when it isn't.</span></span>

<span data-ttu-id="36130-229">如需使用 ASP.NET SignalR 的詳細資訊，請參閱[https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)。</span><span class="sxs-lookup"><span data-stu-id="36130-229">For more information on using ASP.NET SignalR see [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).</span></span>

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a><span data-ttu-id="36130-230">ASP.NET 易記 URL</span><span class="sxs-lookup"><span data-stu-id="36130-230">ASP.NET Friendly URLs</span></span>

<span data-ttu-id="36130-231">ASP.NET FriendlyURLs 讓 web form 開發人員能夠非常輕鬆地產生清楚的 Url （不含 .aspx 副檔名）。</span><span class="sxs-lookup"><span data-stu-id="36130-231">ASP.NET FriendlyURLs makes it very easy for web forms developers to generate cleaner looking URLs(without the .aspx extension).</span></span> <span data-ttu-id="36130-232">幾乎不需要進行任何設定，而且可以與現有的 ASP.NET v4.0 應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="36130-232">It requires little to no configuration and can be used with existing ASP.NET v4.0 applications.</span></span> <span data-ttu-id="36130-233">FriendlyURLs 功能也可讓開發人員藉由支援在桌面與行動裝置之間切換，更輕鬆地將行動支援新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="36130-233">The FriendlyURLs feature also makes it easier for developers to add mobile support to their applications, by supporting switching between desktop and mobile views.</span></span>

<span data-ttu-id="36130-234">如需安裝和使用 ASP.NET 易記 Url 的詳細資訊，請參閱[http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)。</span><span class="sxs-lookup"><span data-stu-id="36130-234">For more information on installing and using ASP.NET Friendly URLs see [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).</span></span>

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="36130-235">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="36130-235">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="36130-236">本節說明 ASP.NET 和 Web 工具2012.2 版本中的已知問題和重大變更。</span><span class="sxs-lookup"><span data-stu-id="36130-236">This section describes known issues and breaking changes that are in the ASP.NET and Web Tools 2012.2 release.</span></span>

### <a name="installation-issues"></a><span data-ttu-id="36130-237">安裝問題</span><span class="sxs-lookup"><span data-stu-id="36130-237">Installation Issues</span></span>

#### <a name="out-of-order-installs-of-visual-studio-2012"></a><span data-ttu-id="36130-238">依序安裝 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="36130-238">Out of order installs of Visual Studio 2012</span></span>

<span data-ttu-id="36130-239">安裝 ASP.NET 和 Web 工具2012.2 之後，安裝 Visual Studio 2012 的額外 SKU 將需要修復操作。</span><span class="sxs-lookup"><span data-stu-id="36130-239">Installing an additional SKU of Visual Studio 2012 after installing the ASP.NET and Web Tools 2012.2 will require a repair operation.</span></span> <span data-ttu-id="36130-240">考量以下發生順序：</span><span class="sxs-lookup"><span data-stu-id="36130-240">Consider the following sequence:</span></span>

1. <span data-ttu-id="36130-241">安裝 Visual Studio 2012 Express for Web</span><span class="sxs-lookup"><span data-stu-id="36130-241">Install Visual Studio 2012 Express for Web</span></span>
2. <span data-ttu-id="36130-242">安裝 ASP.NET 和 Web 工具2012。2</span><span class="sxs-lookup"><span data-stu-id="36130-242">Install ASP.NET and Web Tools 2012.2</span></span>
3. <span data-ttu-id="36130-243">安裝 Visual Studio 2012 Professional、Premium 或旗艦版</span><span class="sxs-lookup"><span data-stu-id="36130-243">Install Visual Studio 2012 Professional, Premium or Ultimate</span></span>

<span data-ttu-id="36130-244">步驟2只會導致安裝 Express for Web 的更新。</span><span class="sxs-lookup"><span data-stu-id="36130-244">Step 2 would only result in installing updates for Express for Web.</span></span> <span data-ttu-id="36130-245">為確保步驟3中安裝的其他 SKU 包含更新，您必須修復 ASP.NET 和 Web 工具2012.2，才能安裝最後安裝的 SKU 更新。</span><span class="sxs-lookup"><span data-stu-id="36130-245">To ensure that the additional SKU installed during step 3 contains the update you will need to repair the ASP.NET and Web Tools 2012.2 to install the updates for the last SKU installed.</span></span> <span data-ttu-id="36130-246">如果步驟1和3中的 Sku 是相反的，這也適用。</span><span class="sxs-lookup"><span data-stu-id="36130-246">This also applies if the SKUs in Step 1 and 3 are reversed.</span></span>

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a><span data-ttu-id="36130-247">Visual Studio 開啟時安裝 Microsoft ASP.NET 和 Web 工具2012。2</span><span class="sxs-lookup"><span data-stu-id="36130-247">Installing Microsoft ASP.NET and Web Tools 2012.2 when Visual Studio is open</span></span>

<span data-ttu-id="36130-248">如果在安裝 Microsoft ASP.NET 和 Web 工具2012.2 期間，VS 是開啟的，Visual Studio 可能會導致不正確的狀態。</span><span class="sxs-lookup"><span data-stu-id="36130-248">If VS is open during installation of Microsoft ASP.NET and Web Tools 2012.2, Visual Studio might end up in a bad state.</span></span> <span data-ttu-id="36130-249">建議使用者先關閉 Visual Studio 的所有實例，再繼續進行安裝。</span><span class="sxs-lookup"><span data-stu-id="36130-249">It is recommended that users close all instances of Visual Studio before proceeding with install.</span></span>

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a><span data-ttu-id="36130-250">在安裝過程中取消 ASP.NET 和 Web 工具2012.2 安裝程式</span><span class="sxs-lookup"><span data-stu-id="36130-250">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation</span></span>

<span data-ttu-id="36130-251">在安裝過程中取消 ASP.NET 和 Web 工具2012.2 安裝程式將會讓 Visual Studio 處於不正常的狀態。</span><span class="sxs-lookup"><span data-stu-id="36130-251">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation will leave Visual Studio in a bad state.</span></span> <span data-ttu-id="36130-252">若要解決此問題，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="36130-252">To address this problem follow these steps:</span></span> 

- <span data-ttu-id="36130-253">移至 [新增或移除程式]</span><span class="sxs-lookup"><span data-stu-id="36130-253">Go to Add Remove Programs</span></span>
- <span data-ttu-id="36130-254">卸載 Microsoft ASP.NET 和 Web 工具2012.2 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="36130-254">Uninstall Microsoft ASP.NET and Web Tools 2012.2, if present.</span></span>
- <span data-ttu-id="36130-255">重新安裝 Microsoft ASP.NET 和 Web 工具2012。2</span><span class="sxs-lookup"><span data-stu-id="36130-255">Reinstall Microsoft ASP.NET and Web Tools 2012.2</span></span>

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a><span data-ttu-id="36130-256">卸載 ASP.NET 和 Web 工具2012.2 之後，缺少 ASP.NET MVC 4 範本和 Razor v2 網站範本</span><span class="sxs-lookup"><span data-stu-id="36130-256">After uninstalling ASP.NET and Web Tools 2012.2 the ASP.NET MVC 4 templates and Razor v2 Web Site templates are missing</span></span>

<span data-ttu-id="36130-257">卸載 ASP.NET 和 Web 工具2012.2 也會從 Visual Studio 2012 卸載所有的 ASP.NET MVC 4 和 Razor v2 網站範本。</span><span class="sxs-lookup"><span data-stu-id="36130-257">Uninstalling ASP.NET and Web Tools 2012.2 will also uninstall all of ASP.NET MVC 4 and Razor v2 Web Site templates from Visual Studio 2012.</span></span>

<span data-ttu-id="36130-258">解決方法是修復您的 Visual Studio 2012 安裝，以重新安裝 ASP.NET MVC 4 和 Razor v2 網站範本。</span><span class="sxs-lookup"><span data-stu-id="36130-258">The workaround is to repair your Visual Studio 2012 installation to reinstall ASP.NET MVC 4 and Razor v2 Web Site templates.</span></span>

### <a name="tooling-issues"></a><span data-ttu-id="36130-259">工具問題</span><span class="sxs-lookup"><span data-stu-id="36130-259">Tooling Issues</span></span>

#### <a name="nuget-error-reported-during-project-creation"></a><span data-ttu-id="36130-260">建立專案期間回報的 NuGet 錯誤</span><span class="sxs-lookup"><span data-stu-id="36130-260">NuGet error reported during project creation</span></span>

<span data-ttu-id="36130-261">安裝 ASP.NET 和 Web 工具2012.2 之後，您可能會在建立 MVC 4 專案時看到下列錯誤</span><span class="sxs-lookup"><span data-stu-id="36130-261">After installing ASP.NET and Web Tools 2012.2 you may see the following error when creating an MVC 4 project</span></span>

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

<span data-ttu-id="36130-262">ASP.NET 和 Web 工具2012.2 隨附 NuGet 2.1，並會在 Visual Studio 2012 中升級延伸模組。</span><span class="sxs-lookup"><span data-stu-id="36130-262">The ASP.NET and Web Tools 2012.2 ships NuGet 2.1 and will upgrade the extension in Visual Studio 2012.</span></span> <span data-ttu-id="36130-263">在某些情況下，VSIX 安裝程式將無法正確更新 VSIX。</span><span class="sxs-lookup"><span data-stu-id="36130-263">In some cases, the VSIX installer will fail to correctly update the VSIX.</span></span> <span data-ttu-id="36130-264">下列步驟可讓您解決此問題：</span><span class="sxs-lookup"><span data-stu-id="36130-264">The following steps will allow you to address this problem:</span></span>

1. <span data-ttu-id="36130-265">以系統管理員身分啟動 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="36130-265">Start Visual Studio 2012 as an Administrator</span></span>
2. <span data-ttu-id="36130-266">移至 [工具]-&gt;[擴充功能和更新]，然後卸載 NuGet。</span><span class="sxs-lookup"><span data-stu-id="36130-266">Go to Tools-&gt;Extensions and Updates and uninstall NuGet.</span></span>
3. <span data-ttu-id="36130-267">關閉 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36130-267">Close Visual Studio</span></span>
4. <span data-ttu-id="36130-268">流覽至 ASP.NET 和 Web 工具2012.2 安裝資料夾：</span><span class="sxs-lookup"><span data-stu-id="36130-268">Navigate to the ASP.NET and Web Tools 2012.2 installation folder:</span></span>

    1. <span data-ttu-id="36130-269">針對 Visual Studio 2012： **Program FILES\MICROSOFT ASP. NET\ASP.NET Web Stack\Visual Studio 2012**</span><span class="sxs-lookup"><span data-stu-id="36130-269">For Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span></span>
    2. <span data-ttu-id="36130-270">針對 Visual Studio 2012 Express for Web： **Program FILES\MICROSOFT ASP. NET\ASP.NET web Stack\Visual Studio Express 2012 For web**</span><span class="sxs-lookup"><span data-stu-id="36130-270">For Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span></span>
5. <span data-ttu-id="36130-271">按兩下 [Nuget.exe] 以重新安裝 NuGet</span><span class="sxs-lookup"><span data-stu-id="36130-271">Double click on the NuGet.Tools.vsix to reinstall NuGet</span></span>

### <a name="web-api-issues"></a><span data-ttu-id="36130-272">Web API 問題</span><span class="sxs-lookup"><span data-stu-id="36130-272">Web API Issues</span></span>

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a><span data-ttu-id="36130-273">剖析 $filter 和日期時間常值中的問題</span><span class="sxs-lookup"><span data-stu-id="36130-273">Parsing issues in $filter and DateTime literals</span></span>

<span data-ttu-id="36130-274">OData URI 剖析器無法正確剖析部分日期時間常值。</span><span class="sxs-lookup"><span data-stu-id="36130-274">The OData URI parser fails to parse partial datetime literals properly.</span></span> <span data-ttu-id="36130-275">例如，$filter = start eq datetime ' 2012-12-31T12： 00 ' 無法正確剖析。</span><span class="sxs-lookup"><span data-stu-id="36130-275">For example, $filter=start eq datetime'2012-12-31T12:00' fails to parse properly.</span></span> <span data-ttu-id="36130-276">解決方法是使用完整的常值，$filter = start eq datetime ' 2012-12-31T12：00： 00 '。</span><span class="sxs-lookup"><span data-stu-id="36130-276">A workaround is to use the full literal, $filter=start eq datetime'2012-12-31T12:00:00'.</span></span>

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a><span data-ttu-id="36130-277">OData 不支援不區分大小寫的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="36130-277">OData doesn't support case-insensitive property names.</span></span>

<span data-ttu-id="36130-278">Odata 不支援 OData 查詢和 odata 路徑中不區分大小寫的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="36130-278">OData doesn't support case-insensitive property names in OData queries and odata path.</span></span> <span data-ttu-id="36130-279">請參閱工作專案：</span><span class="sxs-lookup"><span data-stu-id="36130-279">See workitems:</span></span>

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

<span data-ttu-id="36130-280">如果使用者在 javascript 用戶端和伺服器端上有不同的大小寫，他們可能會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="36130-280">If users have different casing on javascript client side and server side, they probably will encounter this issue.</span></span> <span data-ttu-id="36130-281">此問題是在 odata 通訊協定中設計的。</span><span class="sxs-lookup"><span data-stu-id="36130-281">This issue is by design in odata protocol.</span></span> <span data-ttu-id="36130-282">不過，許多使用者會報告此問題。</span><span class="sxs-lookup"><span data-stu-id="36130-282">However, many users reports this issue.</span></span> <span data-ttu-id="36130-283">若要解決此情況，使用者必須在 URL 中更正其案例。</span><span class="sxs-lookup"><span data-stu-id="36130-283">To work around it, users have to correct their cases in URL.</span></span>

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a><span data-ttu-id="36130-284">預設 OData 路由慣例不支援導覽屬性的 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="36130-284">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span>

<span data-ttu-id="36130-285">預設 OData 路由慣例不支援導覽屬性的 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="36130-285">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span> <span data-ttu-id="36130-286">請參閱工作專案[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)。</span><span class="sxs-lookup"><span data-stu-id="36130-286">See workitem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366).</span></span> <span data-ttu-id="36130-287">在預設慣例中，我們遺漏了這個常用慣例。</span><span class="sxs-lookup"><span data-stu-id="36130-287">We are missing this commonly used convention in default conventions.</span></span>

<span data-ttu-id="36130-288">若要解決此情況，使用者必須擴充新的路由慣例來支援它。</span><span class="sxs-lookup"><span data-stu-id="36130-288">To work around it, users need to extend new routing convention to support it.</span></span>

### <a name="facebook-template-issues"></a><span data-ttu-id="36130-289">Facebook 範本問題</span><span class="sxs-lookup"><span data-stu-id="36130-289">Facebook Template Issues</span></span>

#### <a name="facebook-application-template-only-works-using-net-45"></a><span data-ttu-id="36130-290">Facebook 應用程式範本僅適用于使用 .NET 4。5</span><span class="sxs-lookup"><span data-stu-id="36130-290">Facebook Application template only works using .NET 4.5</span></span>

<span data-ttu-id="36130-291">您必須在 [新增專案] 對話方塊的 [架構] 下拉式清單中選取 [.NET 4.5]，以查看 ASP.NET MVC 4 中的 Facebook 應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="36130-291">You must select .NET 4.5 in the framework dropdown list in the New Project dialog to see the Facebook Application template in ASP.NET MVC 4.</span></span>

#### <a name="real-time-update-controller"></a><span data-ttu-id="36130-292">即時更新控制器</span><span class="sxs-lookup"><span data-stu-id="36130-292">Real-time Update Controller</span></span>

<span data-ttu-id="36130-293">Facebook 應用程式範本可讓使用者輕鬆地建立 Web API 控制器，以處理來自 Facebook 的即時更新。</span><span class="sxs-lookup"><span data-stu-id="36130-293">The Facebook Application template allows user easily create a Web API Controller to handle real-time updates from Facebook.</span></span> <span data-ttu-id="36130-294">如果您的開發電腦位於 NAT 後方，則您的控制器可能無法在沒有進一步的網路設定的情況下工作。</span><span class="sxs-lookup"><span data-stu-id="36130-294">If your development machine is behind NAT, your Controller may not work without further network configuration.</span></span> <span data-ttu-id="36130-295">如需詳細資訊，請參閱這裡： [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span><span class="sxs-lookup"><span data-stu-id="36130-295">See here for details: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span></span>

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a><span data-ttu-id="36130-296">查詢字串值與 Facebook OAuth 參數衝突</span><span class="sxs-lookup"><span data-stu-id="36130-296">Query string values conflict with Facebook OAuth parameters</span></span>

<span data-ttu-id="36130-297">下欄欄位與 Facebook OAuth 對話的回呼 URL 衝突。</span><span class="sxs-lookup"><span data-stu-id="36130-297">The following fields conflict with Facebook OAuth dialog's call back URL.</span></span> <span data-ttu-id="36130-298">請勿新增您自己的查詢字串值，其名稱如下：程式碼、錯誤、錯誤\_描述、錯誤\_原因。</span><span class="sxs-lookup"><span data-stu-id="36130-298">Do not add your own query string values with the following names: code, error, error\_description, error\_reason.</span></span>

#### <a name="using-page-inspector-with-facebook-template"></a><span data-ttu-id="36130-299">搭配 Facebook 範本使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="36130-299">Using Page Inspector with Facebook Template</span></span>

<span data-ttu-id="36130-300">您無法使用 Visual Studio 2012 中的 Page Inspector 功能來偵測您的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="36130-300">You can't use the Page Inspector feature in Visual Studio 2012 while debugging your Facebook Application.</span></span> <span data-ttu-id="36130-301">Page Inspector 目前不支援 iframe。</span><span class="sxs-lookup"><span data-stu-id="36130-301">The Page Inspector does not currently support iframes.</span></span>

### <a name="single-page-application-template-issues"></a><span data-ttu-id="36130-302">單一頁面應用程式範本問題</span><span class="sxs-lookup"><span data-stu-id="36130-302">Single Page Application Template Issues</span></span>

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a><span data-ttu-id="36130-303">使用 JQuery 1.9/挖 2.2.1 update 時，執行預設 MVC SPA 專案時，不會正確處理新的 todo 專案編輯輸入焦點事件。</span><span class="sxs-lookup"><span data-stu-id="36130-303">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter focus event is not handled properly.</span></span>

<span data-ttu-id="36130-304">使用 JQuery 1.9/挖 2.2.1 update 時，執行預設 MVC SPA 專案時，新的 todo 專案編輯輸入在輸入待辦事項清單的新待辦事項之後，不會再將焦點放回新的 [待辦事項] 編輯方塊。</span><span class="sxs-lookup"><span data-stu-id="36130-304">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter no longer focus back to the new todo item edit box after entering the new todo item to the todo list.</span></span>

<span data-ttu-id="36130-305">若要解決此問題，請參考[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)，並對下列範例程式碼進行類似的修正：</span><span class="sxs-lookup"><span data-stu-id="36130-305">To workaround reference [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), and make similar fix to the following sample code:</span></span>

<span data-ttu-id="36130-306">檔案 todo. model .js</span><span class="sxs-lookup"><span data-stu-id="36130-306">File todo.model.js</span></span>  
 <span data-ttu-id="36130-307">函數 todolist （資料），加入下列內容：</span><span class="sxs-lookup"><span data-stu-id="36130-307">function todolist(data), add following:</span></span>  
 <span data-ttu-id="36130-308">**isSelected = ko。可觀察（false）;**</span><span class="sxs-lookup"><span data-stu-id="36130-308">**self.isSelected = ko.observable(false);**</span></span>

<span data-ttu-id="36130-309">addTodo 的 todoList，新增下列黑色文字：</span><span class="sxs-lookup"><span data-stu-id="36130-309">function todoList.prototype.addTodo, add the following blacked text:</span></span>  
 <span data-ttu-id="36130-310">**isSelected （true）;**</span><span class="sxs-lookup"><span data-stu-id="36130-310">**self.isSelected(true);**</span></span>  
 <span data-ttu-id="36130-311">newTodoTitle （&quot;&quot;）;</span><span class="sxs-lookup"><span data-stu-id="36130-311">self.newTodoTitle(&quot;&quot;);</span></span>

<span data-ttu-id="36130-312">檔案索引. cshtml，加入下列黑色文字：</span><span class="sxs-lookup"><span data-stu-id="36130-312">File index.cshtml, add the following blacked text:</span></span>  
 <span data-ttu-id="36130-313">&lt;表單資料系結 =&quot;提交： addTodo&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="36130-313">&lt;form data-bind=&quot;submit: addTodo&quot;&gt;</span></span>  
 <span data-ttu-id="36130-314">&lt;輸入類別 =&quot;addTodo&quot; 類型 =&quot;文字&quot; 資料系結 =&quot;值： newTodoTitle，預留位置： ' 在這裡加入 ' 類型 '，blurOnEnter： true， **hasfocus： isSelected**，事件： {模糊： addTodo}&quot; /&gt;</span><span class="sxs-lookup"><span data-stu-id="36130-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span></span>  
 <span data-ttu-id="36130-315">&lt;/form&gt;</span><span class="sxs-lookup"><span data-stu-id="36130-315">&lt;/form&gt;</span></span>
