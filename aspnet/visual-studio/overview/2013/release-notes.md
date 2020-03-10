---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 版本資訊的 ASP.NET 和 Web 工具 |Microsoft Docs
author: microsoft
description: 本檔說明 Visual Studio 2013 的 ASP.NET 和 Web 工具版本。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557929"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="6d14f-103">適用於 Visual Studio 2013 的 ASP.NET 和 Web 工具版本資訊</span><span class="sxs-lookup"><span data-stu-id="6d14f-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="6d14f-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6d14f-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6d14f-105">本檔說明 Visual Studio 2013 的 ASP.NET 和 Web 工具版本。</span><span class="sxs-lookup"><span data-stu-id="6d14f-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="6d14f-106">內容</span><span class="sxs-lookup"><span data-stu-id="6d14f-106">Contents</span></span>

- [<span data-ttu-id="6d14f-107">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="6d14f-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="6d14f-108">文件</span><span class="sxs-lookup"><span data-stu-id="6d14f-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="6d14f-109">軟體需求</span><span class="sxs-lookup"><span data-stu-id="6d14f-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="6d14f-110">Visual Studio 2013 ASP.NET 和 Web 工具的新功能</span><span class="sxs-lookup"><span data-stu-id="6d14f-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="6d14f-111">一個 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d14f-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="6d14f-112">新的 Web 專案體驗</span><span class="sxs-lookup"><span data-stu-id="6d14f-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="6d14f-113">ASP.NET 的樣板</span><span class="sxs-lookup"><span data-stu-id="6d14f-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="6d14f-114">瀏覽器連結</span><span class="sxs-lookup"><span data-stu-id="6d14f-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="6d14f-115">Visual Studio Web 編輯器增強功能</span><span class="sxs-lookup"><span data-stu-id="6d14f-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="6d14f-116">Visual Studio 中的 Azure App Service Web Apps 支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="6d14f-117">Web 發行增強功能</span><span class="sxs-lookup"><span data-stu-id="6d14f-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="6d14f-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="6d14f-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="6d14f-119">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="6d14f-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="6d14f-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="6d14f-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="6d14f-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="6d14f-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="6d14f-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="6d14f-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="6d14f-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="6d14f-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="6d14f-124">Microsoft OWIN 元件</span><span class="sxs-lookup"><span data-stu-id="6d14f-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="6d14f-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="6d14f-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="6d14f-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="6d14f-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="6d14f-127">ASP.NET 應用程式暫停</span><span class="sxs-lookup"><span data-stu-id="6d14f-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="6d14f-128">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="6d14f-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="6d14f-129">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="6d14f-129">Installation Notes</span></span>

<span data-ttu-id="6d14f-130">Visual Studio 2013 的 ASP.NET 和 Web 工具會配套在主要安裝程式中，而且可以在[這裡](https://www.asp.net/downloads)下載。</span><span class="sxs-lookup"><span data-stu-id="6d14f-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="6d14f-131">文件</span><span class="sxs-lookup"><span data-stu-id="6d14f-131">Documentation</span></span>

<span data-ttu-id="6d14f-132">有關 Visual Studio 2013 ASP.NET 和 Web 工具的教學課程和其他資訊可從[ASP.NET 網站](https://www.asp.net/)取得。</span><span class="sxs-lookup"><span data-stu-id="6d14f-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="6d14f-133">軟體需求</span><span class="sxs-lookup"><span data-stu-id="6d14f-133">Software Requirements</span></span>

<span data-ttu-id="6d14f-134">ASP.NET 和 Web 工具需要 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="6d14f-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="6d14f-135">Visual Studio 2013 ASP.NET 和 Web 工具的新功能</span><span class="sxs-lookup"><span data-stu-id="6d14f-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="6d14f-136">下列各節說明版本中引進的功能。</span><span class="sxs-lookup"><span data-stu-id="6d14f-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="6d14f-137">一個 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d14f-137">One ASP.NET</span></span>

<span data-ttu-id="6d14f-138">隨著 Visual Studio 2013 的發行，我們採取了整合使用 ASP.NET 技術的經驗，讓您可以輕鬆地混搭並比對您想要的。</span><span class="sxs-lookup"><span data-stu-id="6d14f-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="6d14f-139">例如，您可以使用 MVC 啟動專案，並在稍後輕鬆地將 Web form 頁面加入至專案，或在 Web Forms 專案中 scaffold Web Api。</span><span class="sxs-lookup"><span data-stu-id="6d14f-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="6d14f-140">其中一個 ASP.NET 是讓您以開發人員更輕鬆的方式來執行您在 ASP.NET 中所喜愛的專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="6d14f-141">無論您選擇哪一種技術，都可以放心地在一個 ASP.NET 的受信任基礎架構上打造。</span><span class="sxs-lookup"><span data-stu-id="6d14f-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="6d14f-142">新的 Web 專案體驗</span><span class="sxs-lookup"><span data-stu-id="6d14f-142">New Web Project Experience</span></span>

<span data-ttu-id="6d14f-143">我們已增強在 Visual Studio 2013 中建立新 Web 專案的體驗。</span><span class="sxs-lookup"><span data-stu-id="6d14f-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="6d14f-144">在 [**新增 ASP.NET Web 專案**] 對話方塊中，您可以選取所需的專案類型、設定任何技術組合（web FORM、MVC、Web API）、設定驗證選項，以及加入單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新增 ASP.NET 專案](release-notes/_static/image1.png)

<span data-ttu-id="6d14f-146">新的對話方塊可讓您變更許多範本的預設驗證選項。</span><span class="sxs-lookup"><span data-stu-id="6d14f-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="6d14f-147">例如，當您建立 ASP.NET Web Forms 專案時，您可以選取下列任何選項：</span><span class="sxs-lookup"><span data-stu-id="6d14f-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="6d14f-148">不需要驗證</span><span class="sxs-lookup"><span data-stu-id="6d14f-148">No Authentication</span></span>
- <span data-ttu-id="6d14f-149">個別使用者帳戶（ASP.NET 成員資格或社交提供者登入）</span><span class="sxs-lookup"><span data-stu-id="6d14f-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="6d14f-150">組織帳戶（在網際網路應用程式中 Active Directory）</span><span class="sxs-lookup"><span data-stu-id="6d14f-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="6d14f-151">Windows 驗證（在內部網路應用程式中 Active Directory）</span><span class="sxs-lookup"><span data-stu-id="6d14f-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![驗證選項](release-notes/_static/image2.png)

<span data-ttu-id="6d14f-153">如需建立 Web 專案之新進程的詳細資訊，請參閱[在 Visual Studio 2013 中建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="6d14f-154">如需新驗證選項的詳細資訊，請參閱本檔稍後的[ASP.NET Identity](#TOC8) 。</span><span class="sxs-lookup"><span data-stu-id="6d14f-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="6d14f-155">ASP.NET 的樣板</span><span class="sxs-lookup"><span data-stu-id="6d14f-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="6d14f-156">ASP.NET 樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。</span><span class="sxs-lookup"><span data-stu-id="6d14f-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="6d14f-157">它可讓您輕鬆地將未定案程式碼加入至您的專案，以與資料模型互動。</span><span class="sxs-lookup"><span data-stu-id="6d14f-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="6d14f-158">在舊版的 Visual Studio 中，架構僅限於 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="6d14f-159">使用 Visual Studio 2013，您現在可以使用任何 ASP.NET 專案的樣板，包括 Web Forms。</span><span class="sxs-lookup"><span data-stu-id="6d14f-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="6d14f-160">Visual Studio 2013 目前不支援產生 Web form 專案的頁面，但您仍然可以將 MVC 相依性新增至專案，以使用具有 Web form 的樣板。</span><span class="sxs-lookup"><span data-stu-id="6d14f-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="6d14f-161">在未來的更新中，將會新增針對 Web form 產生網頁的支援。</span><span class="sxs-lookup"><span data-stu-id="6d14f-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="6d14f-162">使用 [樣板] 時，我們會確保專案中已安裝所有必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="6d14f-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="6d14f-163">例如，如果您從 ASP.NET Web form 專案開始，然後使用樣板來新增 Web API 控制器，則會自動將所需的 NuGet 套件和參考新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="6d14f-164">若要將 MVC 樣板加入至 Web form 專案，請加入**新的 Scaffold 專案**，然後在交談視窗中選取 [ **MVC 5**相依性]。</span><span class="sxs-lookup"><span data-stu-id="6d14f-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="6d14f-165">有兩個適用于樣板 MVC 的選項;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="6d14f-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="6d14f-166">如果您選取 [最低]，則只會將 ASP.NET MVC 的 NuGet 套件和參考新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="6d14f-167">如果您選取 [完整] 選項，則會加入最少的相依性，以及 MVC 專案所需的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="6d14f-168">支援架構的非同步控制器會使用 Entity Framework 6 的新異步功能。</span><span class="sxs-lookup"><span data-stu-id="6d14f-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="6d14f-169">如需詳細資訊和教學課程，請參閱 ASP.NET 架構的[總覽](aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="6d14f-170">瀏覽器連結-瀏覽器和 Visual Studio 之間的 SignalR 通道</span><span class="sxs-lookup"><span data-stu-id="6d14f-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="6d14f-171">新的[瀏覽器連結](using-browser-link.md)功能可讓您將多個瀏覽器連接到 Visual Studio，然後按一下工具列中的按鈕，將它們全部重新整理。</span><span class="sxs-lookup"><span data-stu-id="6d14f-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="6d14f-172">您可以將多個瀏覽器連接到您的開發網站，包括行動模擬器，然後按一下 [重新整理]，同時重新整理所有的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="6d14f-173">瀏覽器連結也會公開 API，讓開發人員能夠撰寫瀏覽器連結延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6d14f-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="6d14f-174">藉由讓開發人員充分利用瀏覽器連結 API，您就可以建立非常先進的案例，以跨越 Visual Studio 和任何連線的瀏覽器之間的界限。</span><span class="sxs-lookup"><span data-stu-id="6d14f-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="6d14f-175">Web Essentials 利用 API 來建立 Visual Studio 與瀏覽器開發人員工具之間的整合式體驗，以及遠端控制行動模擬器和其他許多功能。</span><span class="sxs-lookup"><span data-stu-id="6d14f-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="6d14f-176">Visual Studio Web 編輯器增強功能</span><span class="sxs-lookup"><span data-stu-id="6d14f-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="6d14f-177">Visual Studio 2013 在 web 應用程式中包含 Razor 檔案和 HTML 檔案的新 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="6d14f-178">新的 HTML 編輯器提供以 HTML5 為基礎的單一整合架構。</span><span class="sxs-lookup"><span data-stu-id="6d14f-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="6d14f-179">它具有自動大括弧完成、jQuery UI 和 AngularJS 屬性 IntelliSense、屬性 IntelliSense 群組、識別碼和類別名稱 Intellisense，以及其他改良功能，包括更好的效能、格式設定和智慧標籤。</span><span class="sxs-lookup"><span data-stu-id="6d14f-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="6d14f-180">下列螢幕擷取畫面示範如何在 HTML 編輯器中使用啟動程式屬性 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="6d14f-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 編輯器中的 Intellisense](release-notes/_static/image4.png)

<span data-ttu-id="6d14f-182">Visual Studio 2013 也隨附內建的 CoffeeScript 和 LESS 編輯器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="6d14f-183">較少的編輯器隨附 CSS 編輯器中的所有酷炫功能，而且具有特定的 Intellisense 可用於變數，並在 @import 鏈中的所有較少檔之間 mixin。</span><span class="sxs-lookup"><span data-stu-id="6d14f-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="6d14f-184">Visual Studio 中的 Azure App Service Web Apps 支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="6d14f-185">在使用 Azure SDK for .NET 2.2 Visual Studio 2013 中，您可以使用**伺服器總管**直接與您的遠端 web 應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="6d14f-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="6d14f-186">您可以登入您的 Azure 帳戶、建立新的 web 應用程式、設定應用程式、查看即時記錄等等。</span><span class="sxs-lookup"><span data-stu-id="6d14f-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="6d14f-187">在 SDK 2.2 發行後即將推出，您將能夠在 Azure 中從遠端執行于 [調試] 模式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="6d14f-188">當您安裝目前版本的 Azure SDK for .NET 時，Azure App Service Web Apps 的大部分新功能也可在 Visual Studio 2012 中使用。</span><span class="sxs-lookup"><span data-stu-id="6d14f-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="6d14f-189">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="6d14f-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="6d14f-190">在 Azure App Service 中建立 ASP.NET web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6d14f-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="6d14f-191">使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6d14f-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="6d14f-192">Web 發行增強功能</span><span class="sxs-lookup"><span data-stu-id="6d14f-192">Web Publish Enhancements</span></span>

<span data-ttu-id="6d14f-193">Visual Studio 2013 包含新的和增強的 Web 發佈功能。</span><span class="sxs-lookup"><span data-stu-id="6d14f-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="6d14f-194">以下提供其中一些範例：</span><span class="sxs-lookup"><span data-stu-id="6d14f-194">Here are a few of them:</span></span>

- <span data-ttu-id="6d14f-195">輕鬆地[自動化 web.config 檔案加密](https://go.microsoft.com/fwlink/?LinkId=325529)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="6d14f-196">（這個連結和下列兩個重點，是 MSDN 上的檔，在10/17 年的第一天之後可能無法使用）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="6d14f-197">輕鬆地[在部署期間自動讓應用程式離線](https://go.microsoft.com/fwlink/?LinkId=325530)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="6d14f-198">將 Web Deploy 設定為使用檔案總和檢查碼，[而不是上次變更日期](https://go.microsoft.com/fwlink/?LinkId=325531)，以判斷哪些檔案應該複製到伺服器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="6d14f-199">當您使用 FTP 或檔案系統發行方法以及 Web Deploy 時，可以快速發行個別選取的檔案（包括 web.config）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="6d14f-200">如需 ASP.NET web 部署的詳細資訊，請參閱[ASP.NET 網站](https://go.microsoft.com/fwlink/?LinkId=322027)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="6d14f-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="6d14f-201">NuGet 2.7</span></span>

<span data-ttu-id="6d14f-202">NuGet 2.7 包含一組豐富的新功能，在[NuGet 2.7 版本](http://docs.nuget.org/docs/release-notes/nuget-2.7)資訊中有詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="6d14f-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="6d14f-203">此版本的 NuGet 也不需要為 NuGet 的套件還原功能提供明確同意，即可下載套件。</span><span class="sxs-lookup"><span data-stu-id="6d14f-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="6d14f-204">您現在可以透過安裝 NuGet 來授與同意（以及 NuGet 的 [喜好設定] 對話方塊中關聯的核取方塊）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="6d14f-205">套件還原現在只會在預設情況下運作。</span><span class="sxs-lookup"><span data-stu-id="6d14f-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="6d14f-206">ASP.NET Web Form</span><span class="sxs-lookup"><span data-stu-id="6d14f-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="6d14f-207">一個 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d14f-207">One ASP.NET</span></span>

<span data-ttu-id="6d14f-208">Web Forms 專案範本會與新的 ASP.NET 體驗緊密整合。</span><span class="sxs-lookup"><span data-stu-id="6d14f-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="6d14f-209">您可以將 MVC 和 Web API 支援新增至您的 Web form 專案，而且可以使用一個 ASP.NET 專案建立嚮導來設定驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="6d14f-210">如需詳細資訊，請參閱[在 Visual Studio 2013 中建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="6d14f-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="6d14f-211">ASP.NET Identity</span></span>

<span data-ttu-id="6d14f-212">Web Forms 專案範本支援新的 ASP.NET Identity 架構。</span><span class="sxs-lookup"><span data-stu-id="6d14f-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="6d14f-213">此外，範本現在支援建立 Web Forms 內部網路專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="6d14f-214">如需詳細資訊，請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案**中的[驗證方法](creating-web-projects-in-visual-studio.md#auth)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="6d14f-215">從中</span><span class="sxs-lookup"><span data-stu-id="6d14f-215">Bootstrap</span></span>

<span data-ttu-id="6d14f-216">Web form 範本會使用[啟動](http://twitter.github.io/bootstrap/)程式，提供您可以輕鬆自訂的精緻且快速的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="6d14f-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="6d14f-217">如需詳細資訊，請參閱[Visual Studio 2013 Web 專案範本中的啟動](creating-web-projects-in-visual-studio.md#bootstrap)程式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="6d14f-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="6d14f-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="6d14f-219">一個 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d14f-219">One ASP.NET</span></span>

<span data-ttu-id="6d14f-220">Web MVC 專案範本會與新的 ASP.NET 體驗緊密整合。</span><span class="sxs-lookup"><span data-stu-id="6d14f-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="6d14f-221">您可以自訂 MVC 專案，並使用一個 ASP.NET 專案建立嚮導來設定驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="6d14f-222">如需 ASP.NET MVC 5 的簡介教學課程，請參閱[使用 ASP.NET MVC 5 的消費者入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="6d14f-223">如需將 MVC 4 專案升級為 MVC 5 的資訊，請參閱[如何將 ASP.NET mvc 4 和 WEB Api 專案升級至 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="6d14f-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="6d14f-224">ASP.NET Identity</span></span>

<span data-ttu-id="6d14f-225">MVC 專案範本已更新為使用 ASP.NET Identity 進行驗證和身分識別管理。</span><span class="sxs-lookup"><span data-stu-id="6d14f-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="6d14f-226">如需 Facebook 和 Google 驗證的教學課程和新的成員資格 API，請參閱[使用 facebook 和 Google OAuth2 和 OpenID 登入建立 ASP.NET mvc 5 應用](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)程式和[使用驗證和 SQL DB 建立 ASP.NET mvc 應用程式並部署至 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="6d14f-227">從中</span><span class="sxs-lookup"><span data-stu-id="6d14f-227">Bootstrap</span></span>

<span data-ttu-id="6d14f-228">MVC 專案範本已更新為使用[啟動](http://getbootstrap.com/)程式來提供精緻且快速的外觀與風格，讓您可以輕鬆地進行自訂。</span><span class="sxs-lookup"><span data-stu-id="6d14f-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="6d14f-229">如需詳細資訊，請參閱[Visual Studio 2013 Web 專案範本中的啟動](creating-web-projects-in-visual-studio.md#bootstrap)程式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="6d14f-230">驗證篩選</span><span class="sxs-lookup"><span data-stu-id="6d14f-230">Authentication filters</span></span>

<span data-ttu-id="6d14f-231">驗證篩選是 ASP.NET MVC 中的一種新篩選準則，會在 ASP.NET MVC 管線的授權篩選準則之前執行，並可讓您針對所有控制器指定每個動作的驗證邏輯、每個控制器或全域。</span><span class="sxs-lookup"><span data-stu-id="6d14f-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="6d14f-232">驗證篩選準則會處理要求中的認證，並提供對應的主體。</span><span class="sxs-lookup"><span data-stu-id="6d14f-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="6d14f-233">驗證篩選也可以新增驗證挑戰，以回應未經授權的要求。</span><span class="sxs-lookup"><span data-stu-id="6d14f-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="6d14f-234">篩選覆寫</span><span class="sxs-lookup"><span data-stu-id="6d14f-234">Filter overrides</span></span>

<span data-ttu-id="6d14f-235">您現在可以藉由指定覆寫篩選準則，覆寫哪些篩選準則會套用至指定的動作方法或控制器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="6d14f-236">覆寫篩選指定一組不應針對指定範圍（動作或控制器）執行的篩選類型。</span><span class="sxs-lookup"><span data-stu-id="6d14f-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="6d14f-237">這可讓您設定全域套用的篩選準則，但會排除特定的全域篩選，使其不會套用至特定動作或控制器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="6d14f-238">屬性路由</span><span class="sxs-lookup"><span data-stu-id="6d14f-238">Attribute routing</span></span>

<span data-ttu-id="6d14f-239">ASP.NET MVC 現在支援屬性路由，感謝 Tim McCall 的貢獻（ [http://attributerouting.net](http://attributerouting.net)的作者）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="6d14f-240">您可以使用屬性路由來指定您的路由，方法是標注動作和控制器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="6d14f-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="6d14f-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="6d14f-242">屬性路由</span><span class="sxs-lookup"><span data-stu-id="6d14f-242">Attribute routing</span></span>

<span data-ttu-id="6d14f-243">ASP.NET Web API 現在支援屬性路由，感謝 Tim McCall 的貢獻， [http://attributerouting.net](http://attributerouting.net)的作者。</span><span class="sxs-lookup"><span data-stu-id="6d14f-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="6d14f-244">透過屬性路由，您可以藉由對動作和控制器加上批註來指定 Web API 路由，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d14f-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="6d14f-245">屬性路由可讓您更充分掌控 Web API 中的 Uri。</span><span class="sxs-lookup"><span data-stu-id="6d14f-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="6d14f-246">例如，您可以使用單一 API 控制器輕鬆地定義資源階層：</span><span class="sxs-lookup"><span data-stu-id="6d14f-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="6d14f-247">屬性路由也提供便利的語法來指定選擇性參數、預設值和路由條件約束：</span><span class="sxs-lookup"><span data-stu-id="6d14f-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="6d14f-248">如需屬性路由的詳細資訊，請參閱[WEB API 2 中的屬性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="6d14f-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="6d14f-249">OAuth 2.0</span></span>

<span data-ttu-id="6d14f-250">Web API 和單一頁面應用程式專案範本現在支援使用 OAuth 2.0 的授權。</span><span class="sxs-lookup"><span data-stu-id="6d14f-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="6d14f-251">OAuth 2.0 是一種架構，可授權用戶端存取受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="6d14f-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="6d14f-252">它適用于各種用戶端，包括瀏覽器和行動裝置。</span><span class="sxs-lookup"><span data-stu-id="6d14f-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="6d14f-253">OAuth 2.0 的支援是以 Microsoft OWIN 元件提供的新安全性中介軟體為基礎，用於持有人驗證和執行授權伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="6d14f-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="6d14f-254">或者，您也可以使用組織授權伺服器（例如 Windows Server 2012 R2 中的 Azure Active Directory 或 ADFS）來授權用戶端。</span><span class="sxs-lookup"><span data-stu-id="6d14f-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="6d14f-255">OData 改善</span><span class="sxs-lookup"><span data-stu-id="6d14f-255">OData Improvements</span></span>

<span data-ttu-id="6d14f-256">**支援 $select、$expand、$batch 和 $value**</span><span class="sxs-lookup"><span data-stu-id="6d14f-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="6d14f-257">ASP.NET Web API OData 現在具有 $select、$expand 和 $value 的完整支援。</span><span class="sxs-lookup"><span data-stu-id="6d14f-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="6d14f-258">您也可以使用 $batch 進行變更集的要求批次處理和處理。</span><span class="sxs-lookup"><span data-stu-id="6d14f-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="6d14f-259">[$Select] 和 [$expand] 選項可讓您變更從 OData 端點傳回的資料圖形。</span><span class="sxs-lookup"><span data-stu-id="6d14f-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="6d14f-260">如需詳細資訊，請參閱[WEB API OData 中的 $select 和 $expand 支援簡介](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="6d14f-261">**改良的擴充性**</span><span class="sxs-lookup"><span data-stu-id="6d14f-261">**Improved extensibility**</span></span>

<span data-ttu-id="6d14f-262">OData 格式器現在可以擴充。</span><span class="sxs-lookup"><span data-stu-id="6d14f-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="6d14f-263">您可以新增 Atom 專案中繼資料、支援命名的資料流程和媒體連結專案、加入實例注釋，以及自訂產生連結的方式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="6d14f-264">**不支援類型**</span><span class="sxs-lookup"><span data-stu-id="6d14f-264">**Type-less support**</span></span>

<span data-ttu-id="6d14f-265">您現在可以建立 OData 服務，而不需要為您的實體類型定義 CLR 類型。</span><span class="sxs-lookup"><span data-stu-id="6d14f-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="6d14f-266">相反地，您的 OData 控制器可以接受或傳回**IEdmObject**的實例，這是 odata 格式器序列化/還原序列化。</span><span class="sxs-lookup"><span data-stu-id="6d14f-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="6d14f-267">**重複使用現有的模型**</span><span class="sxs-lookup"><span data-stu-id="6d14f-267">**Reuse an existing model**</span></span>

<span data-ttu-id="6d14f-268">如果您已經有現有的 entity data model （EDM），您現在可以直接重複使用它，而不需要建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="6d14f-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="6d14f-269">例如，如果您使用 Entity Framework，您可以使用 EF 為您建立的 EDM。</span><span class="sxs-lookup"><span data-stu-id="6d14f-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="6d14f-270">要求批次處理</span><span class="sxs-lookup"><span data-stu-id="6d14f-270">Request Batching</span></span>

<span data-ttu-id="6d14f-271">要求批次處理會將多個作業結合成單一 HTTP POST 要求，以減少網路流量，並提供更流暢、較不多對話的使用者介面。</span><span class="sxs-lookup"><span data-stu-id="6d14f-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="6d14f-272">ASP.NET Web API 現在支援數個要求批次處理策略：</span><span class="sxs-lookup"><span data-stu-id="6d14f-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="6d14f-273">使用 OData 服務的 $batch 端點。</span><span class="sxs-lookup"><span data-stu-id="6d14f-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="6d14f-274">將多個要求封裝成單一 MIME 多部分要求。</span><span class="sxs-lookup"><span data-stu-id="6d14f-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="6d14f-275">使用自訂的批次處理格式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-275">Use a custom batching format.</span></span>

<span data-ttu-id="6d14f-276">若要啟用要求批次處理，只需將具有批次處理處理常式的路由新增至您的 Web API 設定：</span><span class="sxs-lookup"><span data-stu-id="6d14f-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="6d14f-277">您也可以控制要求或依序或循序執行。</span><span class="sxs-lookup"><span data-stu-id="6d14f-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="6d14f-278">可攜 ASP.NET Web API 用戶端</span><span class="sxs-lookup"><span data-stu-id="6d14f-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="6d14f-279">您現在可以使用 ASP.NET Web API 用戶端來建立可在您的 Windows Store 和 Windows Phone 8 應用程式之間工作的便攜類別庫。</span><span class="sxs-lookup"><span data-stu-id="6d14f-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="6d14f-280">您也可以建立可在用戶端和伺服器之間共用的便攜格式器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="6d14f-281">改良的可測試性</span><span class="sxs-lookup"><span data-stu-id="6d14f-281">Improved Testability</span></span>

<span data-ttu-id="6d14f-282">Web API 2 可讓您更輕鬆地對 API 控制器進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="6d14f-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="6d14f-283">只要使用您的要求訊息和設定來具現化您的 API 控制器，然後呼叫您想要測試的動作方法。</span><span class="sxs-lookup"><span data-stu-id="6d14f-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="6d14f-284">針對執行連結產生的動作方法，也很容易模擬**UrlHelper**類別。</span><span class="sxs-lookup"><span data-stu-id="6d14f-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="6d14f-285">應傳回 iHTTPactionresult</span><span class="sxs-lookup"><span data-stu-id="6d14f-285">IHttpActionResult</span></span>

<span data-ttu-id="6d14f-286">您現在可以執行應傳回 iHTTPactionresult 來封裝 Web API 動作方法的結果。</span><span class="sxs-lookup"><span data-stu-id="6d14f-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="6d14f-287">ASP.NET Web API 執行時間會執行從 Web API 動作方法傳回的應傳回 iHTTPactionresult，以產生結果回應訊息。</span><span class="sxs-lookup"><span data-stu-id="6d14f-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="6d14f-288">您可以從任何 Web API 動作傳回應傳回 iHTTPactionresult，以簡化 Web API 執行的單元測試。</span><span class="sxs-lookup"><span data-stu-id="6d14f-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="6d14f-289">為了方便起見，會提供一些現成的應傳回 iHTTPactionresult 實作為，包括傳回特定狀態碼、格式化內容或內容協商回應的結果。</span><span class="sxs-lookup"><span data-stu-id="6d14f-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="6d14f-290">HttpRequestCoNtext</span><span class="sxs-lookup"><span data-stu-id="6d14f-290">HttpRequestContext</span></span>

<span data-ttu-id="6d14f-291">新的**HttpRequestCoNtext**會追蹤系結至要求但不會立即從要求取得的任何狀態。</span><span class="sxs-lookup"><span data-stu-id="6d14f-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="6d14f-292">例如，您可以使用**HttpRequestCoNtext**來取得路由資料、與要求相關聯的主體、用戶端憑證、 **UrlHelper**和虛擬路徑根。</span><span class="sxs-lookup"><span data-stu-id="6d14f-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="6d14f-293">您可以輕鬆地為單元測試目的建立**HttpRequestCoNtext** 。</span><span class="sxs-lookup"><span data-stu-id="6d14f-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="6d14f-294">由於要求的主體會與要求進行流動，而不是依賴**thread.currentprincipal**，因此主體現在會在要求的存留期內提供，同時位於 Web API 管線中。</span><span class="sxs-lookup"><span data-stu-id="6d14f-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="6d14f-295">CORS</span><span class="sxs-lookup"><span data-stu-id="6d14f-295">CORS</span></span>

<span data-ttu-id="6d14f-296">感謝 Brock Allen 的另一個絕佳貢獻，ASP.NET 現在完全支援跨原始來源要求共用（CORS）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="6d14f-297">瀏覽器安全性可防止網頁對另一個網域提出 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="6d14f-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="6d14f-298">[CORS](http://www.w3.org/TR/cors/)是一種 W3C 標準，可讓伺服器放寬相同的原始原則。</span><span class="sxs-lookup"><span data-stu-id="6d14f-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="6d14f-299">使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。</span><span class="sxs-lookup"><span data-stu-id="6d14f-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="6d14f-300">Web API 2 現在支援 CORS，包括自動處理預檢要求。</span><span class="sxs-lookup"><span data-stu-id="6d14f-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="6d14f-301">如需詳細資訊，請參閱 [在 ASP.NET Web API 中啟用跨原始來源要求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="6d14f-302">驗證篩選</span><span class="sxs-lookup"><span data-stu-id="6d14f-302">Authentication Filters</span></span>

<span data-ttu-id="6d14f-303">驗證篩選是 ASP.NET Web API 中的一種新篩選準則，會在 ASP.NET Web API 管線中的授權篩選準則之前執行，並可讓您針對所有控制器指定驗證邏輯的每一動作、每個控制器或全域。</span><span class="sxs-lookup"><span data-stu-id="6d14f-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="6d14f-304">驗證篩選準則會處理要求中的認證，並提供對應的主體。</span><span class="sxs-lookup"><span data-stu-id="6d14f-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="6d14f-305">驗證篩選也可以新增驗證挑戰，以回應未經授權的要求。</span><span class="sxs-lookup"><span data-stu-id="6d14f-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="6d14f-306">篩選覆寫</span><span class="sxs-lookup"><span data-stu-id="6d14f-306">Filter Overrides</span></span>

<span data-ttu-id="6d14f-307">您現在可以藉由指定覆寫篩選準則，覆寫哪些篩選準則會套用至指定的動作方法或控制器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="6d14f-308">覆寫篩選指定一組不應針對指定範圍（動作或控制器）執行的篩選類型。</span><span class="sxs-lookup"><span data-stu-id="6d14f-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="6d14f-309">這可讓您新增全域篩選器，但從特定動作或控制器中排除部分。</span><span class="sxs-lookup"><span data-stu-id="6d14f-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="6d14f-310">OWIN 整合</span><span class="sxs-lookup"><span data-stu-id="6d14f-310">OWIN Integration</span></span>

<span data-ttu-id="6d14f-311">ASP.NET Web API 現在完全支援 OWIN，而且可以在任何具有 OWIN 功能的主機上執行。</span><span class="sxs-lookup"><span data-stu-id="6d14f-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="6d14f-312">此外，也包含可與 OWIN authentication 系統整合的**HostAuthenticationFilter** 。</span><span class="sxs-lookup"><span data-stu-id="6d14f-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="6d14f-313">透過 OWIN 整合，您可以在自己的進程中自我裝載 Web API，以及其他 OWIN 中介軟體，例如 SignalR。</span><span class="sxs-lookup"><span data-stu-id="6d14f-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="6d14f-314">如需詳細資訊，請參閱[使用 OWIN 至自我裝載 ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="6d14f-315">ASP.NET SignalR 2。0</span><span class="sxs-lookup"><span data-stu-id="6d14f-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="6d14f-316">下列各節說明 SignalR 2.0 的功能。</span><span class="sxs-lookup"><span data-stu-id="6d14f-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="6d14f-317">以 OWIN 為基礎</span><span class="sxs-lookup"><span data-stu-id="6d14f-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="6d14f-318">MapHubs 和 MapConnection 現在已 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="6d14f-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="6d14f-319">跨網域支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="6d14f-320">透過 MonoTouch 和 MonoDroid 的 iOS 和 Android 支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="6d14f-321">可移植的 .NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="6d14f-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="6d14f-322">新的自我裝載套件</span><span class="sxs-lookup"><span data-stu-id="6d14f-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="6d14f-323">與舊版相容的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="6d14f-324">已移除 .NET 4.0 的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="6d14f-325">將訊息傳送至用戶端和群組的清單</span><span class="sxs-lookup"><span data-stu-id="6d14f-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="6d14f-326">將訊息傳送給特定使用者</span><span class="sxs-lookup"><span data-stu-id="6d14f-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="6d14f-327">更好的錯誤處理支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="6d14f-328">簡化中樞的單元測試</span><span class="sxs-lookup"><span data-stu-id="6d14f-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="6d14f-329">JavaScript 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="6d14f-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="6d14f-330">如需如何將現有1.x 專案升級至 SignalR 2.0 的範例，請參閱[升級 SignalR 1.X 專案](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="6d14f-331">以 OWIN 為基礎</span><span class="sxs-lookup"><span data-stu-id="6d14f-331">Built on OWIN</span></span>

<span data-ttu-id="6d14f-332">SignalR 2.0 完全建置於[OWIN （適用于 .net 的開放式 Web 介面）](http://owin.org/)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="6d14f-333">這項變更讓 SignalR 的設定程式在 web 裝載和自我裝載的 SignalR 應用程式之間更加一致，但也需要一些 API 變更。</span><span class="sxs-lookup"><span data-stu-id="6d14f-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="6d14f-334">MapHubs 和 MapConnection 現在已 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="6d14f-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="6d14f-335">為了與 OWIN 標準相容，這些方法已重新命名為 `MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="6d14f-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="6d14f-336">不含參數的 `MapSignalR` 呼叫將會對應所有中樞（如1.x 版中的 `MapHubs`）;若要對應個別的**PersistentConnection**物件，請將連線類型指定為類型參數，並將連接的 URL 延伸模組指定為第一個引數。</span><span class="sxs-lookup"><span data-stu-id="6d14f-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="6d14f-337">在 Owin 啟動類別中呼叫 `MapSignalR` 方法。</span><span class="sxs-lookup"><span data-stu-id="6d14f-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="6d14f-338">Visual Studio 2013 包含 Owin 啟動類別的新範本;若要使用此範本，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6d14f-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="6d14f-339">以滑鼠右鍵按一下專案</span><span class="sxs-lookup"><span data-stu-id="6d14f-339">Right-click on the project</span></span>
2. <span data-ttu-id="6d14f-340">選取 [**加入**]、[**新增專案**]</span><span class="sxs-lookup"><span data-stu-id="6d14f-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="6d14f-341">選取 [ **Owin 啟動類別**]。</span><span class="sxs-lookup"><span data-stu-id="6d14f-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="6d14f-342">將新類別命名為**Startup.cs**。</span><span class="sxs-lookup"><span data-stu-id="6d14f-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="6d14f-343">在**web 應用程式中，** 包含 `MapSignalR` 方法的 Owin 啟動類別，接著會使用 web.config 檔案的 [應用程式設定] 節點中的專案新增至 Owin 的啟動程式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6d14f-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="6d14f-344">在自我裝載的**應用程式**中，啟動類別會當做 `WebApp.Start` 方法的型別參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="6d14f-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="6d14f-345">**在 SignalR 1.x （從 web 應用程式中的全域應用程式檔）對應中樞和連接：**</span><span class="sxs-lookup"><span data-stu-id="6d14f-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="6d14f-346">**在 SignalR 2.0 （來自 Owin 啟動類別檔案）中對應中樞和連線：**</span><span class="sxs-lookup"><span data-stu-id="6d14f-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="6d14f-347">在自我裝載的**應用程式**中，啟動類別會當做 `WebApp.Start` 方法的型別參數傳遞，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6d14f-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="6d14f-348">跨網域支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-348">Cross-Domain Support</span></span>

<span data-ttu-id="6d14f-349">在 SignalR 1.x 中，跨網域要求是由單一 EnableCrossDomain 旗標所控制。</span><span class="sxs-lookup"><span data-stu-id="6d14f-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="6d14f-350">此旗標會同時控制 JSONP 和 CORS 要求。</span><span class="sxs-lookup"><span data-stu-id="6d14f-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="6d14f-351">為了提供更大的彈性，所有 CORS 支援都已從 SignalR 的伺服器元件中移除（如果偵測到瀏覽器支援，JavaScript 用戶端仍會正常使用 CORS），而且已提供新的 OWIN 中介軟體來支援這些案例。</span><span class="sxs-lookup"><span data-stu-id="6d14f-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="6d14f-352">在 SignalR 2.0 中，如果用戶端需要 JSONP （以支援舊版瀏覽器中的跨網域要求），則必須將 `HubConfiguration` 物件上的 `EnableJSONP` 設定為 `true`，以明確地啟用它，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6d14f-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="6d14f-353">預設會停用 JSONP，因為它的安全性不如 CORS。</span><span class="sxs-lookup"><span data-stu-id="6d14f-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="6d14f-354">若要在 SignalR 2.0 中新增新的 CORS 中介軟體，請將 `Microsoft.Owin.Cors` 程式庫新增至您的專案，並在 SignalR 中介軟體之前呼叫 `UseCors`，如下一節所示。</span><span class="sxs-lookup"><span data-stu-id="6d14f-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="6d14f-355">**將 Owin 新增至您的專案**：若要安裝此程式庫，請在 [套件管理員主控台] 中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6d14f-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="6d14f-356">此命令會將套件的2.0.0 版本新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="6d14f-357">**呼叫 UseCors**</span><span class="sxs-lookup"><span data-stu-id="6d14f-357">**Calling UseCors**</span></span>

<span data-ttu-id="6d14f-358">下列程式碼片段示範如何在 SignalR 1.x 和2.0 中執行跨網域連接。</span><span class="sxs-lookup"><span data-stu-id="6d14f-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="6d14f-359">**在 SignalR 1.x 中執行跨網域要求（從全域應用程式檔）**</span><span class="sxs-lookup"><span data-stu-id="6d14f-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="6d14f-360">**在 SignalR 2.0 （從程式C#代碼檔案）中執行跨網域要求**</span><span class="sxs-lookup"><span data-stu-id="6d14f-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="6d14f-361">下列程式碼示範如何在 SignalR 2.0 專案中啟用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="6d14f-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="6d14f-362">這個程式碼範例會使用 `Map` 和 `RunSignalR`，而不是 `MapSignalR`，因此 CORS 中介軟體只會針對需要 CORS 支援的 SignalR 要求（而不是針對 `MapSignalR`中指定之路徑上的所有流量）執行。 `Map` 也可以用於需要針對特定 URL 首碼執行的任何其他中介軟體，而不是針對整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="6d14f-363">透過 MonoTouch 和 MonoDroid 的 iOS 和 Android 支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="6d14f-364">已使用[Xamarin 程式庫](https://xamarin.com/)中的 MonoTouch 和 MonoDroid 元件，為 IOS 和 Android 用戶端新增了支援。</span><span class="sxs-lookup"><span data-stu-id="6d14f-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="6d14f-365">如需如何使用它們的詳細資訊，請參閱[使用 Xamarin 元件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="6d14f-366">當 SignalR RTW 版本可供使用時， [Xamarin 存放區](https://store.xamarin.com/)中將會提供這些元件。</span><span class="sxs-lookup"><span data-stu-id="6d14f-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="6d14f-367"># # # 可移植 .NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="6d14f-367">### Portable .NET client</span></span>

<span data-ttu-id="6d14f-368">為了更方便跨平臺開發，Silverlight、WinRT 和 Windows Phone 用戶端已由支援下列平臺的單一可移植 .NET 用戶端所取代：</span><span class="sxs-lookup"><span data-stu-id="6d14f-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="6d14f-369">NET 4。5</span><span class="sxs-lookup"><span data-stu-id="6d14f-369">NET 4.5</span></span>
- <span data-ttu-id="6d14f-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="6d14f-370">Silverlight 5</span></span>
- <span data-ttu-id="6d14f-371">WinRT （適用于 Windows Store 應用程式的 .NET）</span><span class="sxs-lookup"><span data-stu-id="6d14f-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="6d14f-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="6d14f-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="6d14f-373">新的自我裝載套件</span><span class="sxs-lookup"><span data-stu-id="6d14f-373">New Self-Host Package</span></span>

<span data-ttu-id="6d14f-374">現在有 NuGet 套件可讓您更輕鬆地開始使用 SignalR 自我裝載（SignalR 應用程式（裝載于進程或其他應用程式中），而不是裝載在 web 伺服器中。</span><span class="sxs-lookup"><span data-stu-id="6d14f-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="6d14f-375">若要升級以 SignalR 1.x 建立的自我裝載專案，請移除 SignalR. Owin 套件，然後新增 SignalR. SelfHost 套件。</span><span class="sxs-lookup"><span data-stu-id="6d14f-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="6d14f-376">如需有關如何開始使用自我裝載套件的詳細資訊，請參閱[教學課程： SignalR 自我裝載](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="6d14f-377">與舊版相容的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-377">Backward-compatible server support</span></span>

<span data-ttu-id="6d14f-378">在舊版的 SignalR 中，用戶端和伺服器中所使用的 SignalR 套件版本必須相同。</span><span class="sxs-lookup"><span data-stu-id="6d14f-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="6d14f-379">為了支援不容易更新的胖用戶端應用程式，SignalR 2.0 現在支援使用較舊的伺服器版本搭配舊版用戶端。</span><span class="sxs-lookup"><span data-stu-id="6d14f-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="6d14f-380">**注意： SignalR 2.0 不支援以較新版本的舊版用戶端建立的伺服器。**</span><span class="sxs-lookup"><span data-stu-id="6d14f-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="6d14f-381">已移除 .NET 4.0 的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="6d14f-382">SignalR 2.0 已中斷與 .NET 4.0 的伺服器互通性支援。</span><span class="sxs-lookup"><span data-stu-id="6d14f-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="6d14f-383">.NET 4.5 必須與 SignalR 2.0 伺服器搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6d14f-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="6d14f-384">SignalR 2.0 仍然有 .NET 4.0 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6d14f-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="6d14f-385">將訊息傳送至用戶端和群組的清單</span><span class="sxs-lookup"><span data-stu-id="6d14f-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="6d14f-386">在 SignalR 2.0 中，您可以使用用戶端和群組識別碼的清單來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="6d14f-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="6d14f-387">下列程式碼片段示範如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="6d14f-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="6d14f-388">**使用 PersistentConnection 將訊息傳送至用戶端和群組的清單**</span><span class="sxs-lookup"><span data-stu-id="6d14f-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="6d14f-389">**使用中樞將訊息傳送至用戶端和群組清單**</span><span class="sxs-lookup"><span data-stu-id="6d14f-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="6d14f-390">將訊息傳送給特定使用者</span><span class="sxs-lookup"><span data-stu-id="6d14f-390">Sending a message to a specific user</span></span>

<span data-ttu-id="6d14f-391">這項功能可讓使用者透過新的介面 IUserIdProvider，指定 userId 是以 IRequest 為基礎：</span><span class="sxs-lookup"><span data-stu-id="6d14f-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="6d14f-392">**IUserIdProvider 介面**</span><span class="sxs-lookup"><span data-stu-id="6d14f-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="6d14f-393">根據預設，會有一個使用使用者的 IPrincipal.Identity.Name 做為使用者名稱的執行。</span><span class="sxs-lookup"><span data-stu-id="6d14f-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="6d14f-394">在中樞中，您將能夠透過新的 API 將訊息傳送給這些使用者：</span><span class="sxs-lookup"><span data-stu-id="6d14f-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="6d14f-395">**使用用戶端 API**</span><span class="sxs-lookup"><span data-stu-id="6d14f-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="6d14f-396">更好的錯誤處理支援</span><span class="sxs-lookup"><span data-stu-id="6d14f-396">Better Error Handling Support</span></span>

<span data-ttu-id="6d14f-397">使用者現在可以從任何中樞調用中擲回**HubException** 。</span><span class="sxs-lookup"><span data-stu-id="6d14f-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="6d14f-398">**HubException**的函式可以接受字串訊息和物件額外的錯誤資料。</span><span class="sxs-lookup"><span data-stu-id="6d14f-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="6d14f-399">SignalR 會自動將例外狀況序列化，並將它傳送至用戶端，以便用來拒絕/失敗中樞方法叫用。</span><span class="sxs-lookup"><span data-stu-id="6d14f-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="6d14f-400">[**顯示詳細的中樞例外**狀況] 設定與傳送回用戶端的**HubException**無關。一律會傳送。</span><span class="sxs-lookup"><span data-stu-id="6d14f-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="6d14f-401">**示範如何將 HubException 傳送至用戶端的伺服器端程式碼**</span><span class="sxs-lookup"><span data-stu-id="6d14f-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="6d14f-402">**示範回應從伺服器傳送之 HubException 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6d14f-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="6d14f-403">**示範回應從伺服器傳送之 HubException 的 .NET 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6d14f-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="6d14f-404">簡化中樞的單元測試</span><span class="sxs-lookup"><span data-stu-id="6d14f-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="6d14f-405">SignalR 2.0 包含一個在中樞上稱為 `IHubCallerConnectionContext` 的介面，可讓您更輕鬆地建立模擬用戶端調用。</span><span class="sxs-lookup"><span data-stu-id="6d14f-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="6d14f-406">下列程式碼片段示範如何將此介面與熱門的測試能力[xUnit.net](https://github.com/xunit/xunit)和[moq](https://code.google.com/p/moq/)搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6d14f-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="6d14f-407">**使用 xUnit.net 的單元測試 SignalR**</span><span class="sxs-lookup"><span data-stu-id="6d14f-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="6d14f-408">**使用 moq 的單元測試 SignalR**</span><span class="sxs-lookup"><span data-stu-id="6d14f-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="6d14f-409">JavaScript 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="6d14f-409">JavaScript error handling</span></span>

<span data-ttu-id="6d14f-410">在 SignalR 2.0 中，所有 JavaScript 錯誤處理回呼都會傳回 JavaScript 錯誤物件，而不是原始字串。</span><span class="sxs-lookup"><span data-stu-id="6d14f-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="6d14f-411">這可讓 SignalR 將更豐富的資訊傳遞給您的錯誤處理常式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="6d14f-412">您可以從錯誤的 `source` 屬性取得內部例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6d14f-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="6d14f-413">**處理 Start 的 JavaScript 用戶端程式代碼。 Fail 例外狀況**</span><span class="sxs-lookup"><span data-stu-id="6d14f-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="6d14f-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="6d14f-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="6d14f-415">新的 ASP.NET 成員資格系統</span><span class="sxs-lookup"><span data-stu-id="6d14f-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="6d14f-416">ASP.NET Identity 是 ASP.NET 應用程式的新成員資格系統。</span><span class="sxs-lookup"><span data-stu-id="6d14f-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="6d14f-417">ASP.NET Identity 可讓您輕鬆地整合使用者特定的設定檔資料與應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="6d14f-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="6d14f-418">ASP.NET Identity 也可讓您選擇應用程式中使用者設定檔的持續性模型。</span><span class="sxs-lookup"><span data-stu-id="6d14f-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="6d14f-419">您可以將資料儲存在 SQL Server 資料庫或另一個資料存放區中，包括 NoSQL 資料存放區（例如 Azure 儲存體資料表）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="6d14f-420">如需詳細資訊，請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案**中的[個別使用者帳戶](creating-web-projects-in-visual-studio.md#indauth)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="6d14f-421">宣告架構驗證</span><span class="sxs-lookup"><span data-stu-id="6d14f-421">Claims-based authentication</span></span>

<span data-ttu-id="6d14f-422">ASP.NET 現在支援以宣告為基礎的驗證，其中使用者的身分識別會表示為來自受信任簽發者的一組宣告。</span><span class="sxs-lookup"><span data-stu-id="6d14f-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="6d14f-423">使用者可以使用在應用程式資料庫中維護的使用者名稱和密碼，或使用社交識別提供者（例如 Microsoft 帳戶、Facebook、Google、Twitter），或透過 Azure Active Directory 或使用組織帳戶來進行驗證。Active Directory 同盟服務（ADFS）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="6d14f-424">與 Azure Active Directory 和 Windows Server Active Directory 整合</span><span class="sxs-lookup"><span data-stu-id="6d14f-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="6d14f-425">您現在可以建立使用 Azure Active Directory 或 Windows Server Active Directory （AD）進行驗證的 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="6d14f-426">如需詳細資訊，請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案**中的[組織帳戶](creating-web-projects-in-visual-studio.md#orgauth)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="6d14f-427">OWIN 整合</span><span class="sxs-lookup"><span data-stu-id="6d14f-427">OWIN Integration</span></span>

<span data-ttu-id="6d14f-428">ASP.NET authentication 現在是以 OWIN 中介軟體為基礎，可用於任何以 OWIN 為基礎的主機。</span><span class="sxs-lookup"><span data-stu-id="6d14f-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="6d14f-429">如需 OWIN 的詳細資訊，請參閱下列[MICROSOFT OWIN Components](#TOC7)一節。</span><span class="sxs-lookup"><span data-stu-id="6d14f-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="6d14f-430">Microsoft OWIN 元件</span><span class="sxs-lookup"><span data-stu-id="6d14f-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="6d14f-431">[Open Web Interface for .net](http://owin.org/) （OWIN）會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="6d14f-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="6d14f-432">OWIN 會將 web 應用程式與伺服器分離，使 web 應用程式不受主機限制。</span><span class="sxs-lookup"><span data-stu-id="6d14f-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="6d14f-433">例如，您可以在 IIS 中裝載以 OWIN 為基礎的 web 應用程式，或在自訂進程中自我裝載它。</span><span class="sxs-lookup"><span data-stu-id="6d14f-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="6d14f-434">Microsoft OWIN 元件（也稱為 Katana 專案）中引進的變更包含新的伺服器和主機元件、新的協助程式程式庫和中介軟體，以及新的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="6d14f-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="6d14f-435">如需 OWIN 和 Katana 的詳細資訊，請參閱[OWIN 和 Katana 的新功能](../../../aspnet/overview/owin-and-katana/index.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="6d14f-436">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式無法在 IIS 傳統模式中執行;它們必須以整合模式執行。**</span><span class="sxs-lookup"><span data-stu-id="6d14f-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="6d14f-437">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式必須以完全信任的方式執行。**</span><span class="sxs-lookup"><span data-stu-id="6d14f-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="6d14f-438">新的伺服器和主機</span><span class="sxs-lookup"><span data-stu-id="6d14f-438">New Servers and Hosts</span></span>

<span data-ttu-id="6d14f-439">在此版本中，新增了新的元件以啟用自我裝載案例。</span><span class="sxs-lookup"><span data-stu-id="6d14f-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="6d14f-440">這些元件包括下列 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="6d14f-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="6d14f-441">**Owin. HttpListener**。</span><span class="sxs-lookup"><span data-stu-id="6d14f-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="6d14f-442">提供使用**HttpListener**接聽 HTTP 要求並將其導向 OWIN 管線的 OWIN 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="6d14f-443">**Owin**為想要在自訂進程（例如主控台應用程式或 Windows 服務）中自我裝載 Owin 管線的開發人員提供程式庫。</span><span class="sxs-lookup"><span data-stu-id="6d14f-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="6d14f-444">**OwinHost**。</span><span class="sxs-lookup"><span data-stu-id="6d14f-444">**OwinHost**.</span></span> <span data-ttu-id="6d14f-445">提供獨立的可執行檔，可包裝 `Microsoft.Owin.Hosting`，並可讓您自行裝載 OWIN 管線，而不需要撰寫自訂主應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="6d14f-446">此外，`Microsoft.Owin.Host.SystemWeb` 封裝現在可讓中介軟體將提示提供給**SystemWeb**伺服器，表示應該在特定 ASP.NET 管線階段呼叫中介軟體。</span><span class="sxs-lookup"><span data-stu-id="6d14f-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="6d14f-447">這項功能特別適用于驗證中介軟體，這應該在 ASP.NET 管線早期執行。</span><span class="sxs-lookup"><span data-stu-id="6d14f-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="6d14f-448">Helper 程式庫和中介軟體</span><span class="sxs-lookup"><span data-stu-id="6d14f-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="6d14f-449">雖然您只能使用 OWIN 規格中的函式和類型定義來撰寫 OWIN 元件，但新的 `Microsoft.Owin` 封裝會提供一組更好的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="6d14f-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="6d14f-450">此套件將數個先前的套件（例如 `Owin.Extensions`、`Owin.Types`）結合成單一且結構良好的物件模型，讓其他 OWIN 元件可以輕鬆地使用它。</span><span class="sxs-lookup"><span data-stu-id="6d14f-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="6d14f-451">事實上，大部分的 Microsoft OWIN 元件現在都使用這個套件。</span><span class="sxs-lookup"><span data-stu-id="6d14f-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="6d14f-452">[OWIN](http://www.owin.org)應用程式無法在 IIS 傳統模式中執行;它們必須以整合模式執行。</span><span class="sxs-lookup"><span data-stu-id="6d14f-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="6d14f-453">[OWIN](http://www.owin.org)應用程式必須以完全信任的方式執行。</span><span class="sxs-lookup"><span data-stu-id="6d14f-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="6d14f-454">此版本也包含 Owin 診斷套件，其中包含用來驗證執行中 OWIN 應用程式的中介軟體，加上錯誤頁面中介軟體可協助調查失敗。</span><span class="sxs-lookup"><span data-stu-id="6d14f-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="6d14f-455">驗證元件</span><span class="sxs-lookup"><span data-stu-id="6d14f-455">Authentication Components</span></span>

<span data-ttu-id="6d14f-456">下列是可用的驗證元件。</span><span class="sxs-lookup"><span data-stu-id="6d14f-456">The following authentication components are available.</span></span>

- <span data-ttu-id="6d14f-457">**Owin. 安全的 ActiveDirectory**。</span><span class="sxs-lookup"><span data-stu-id="6d14f-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="6d14f-458">使用內部部署或雲端式目錄服務來啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="6d14f-459">**Owin**使用 cookie 啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="6d14f-460">此封裝先前已命名為 `Microsoft.Owin.Security.Forms`。</span><span class="sxs-lookup"><span data-stu-id="6d14f-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="6d14f-461">**Owin**會使用 Facebook 的 OAuth 型服務來啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="6d14f-462">**Owin**使用 Google 的 OpenID 型服務來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="6d14f-463">**Owin**會使用 jwt 權杖來啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="6d14f-464">**Owin. MicrosoftAccount**使用 microsoft 帳戶啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="6d14f-465">**Owin. Security. OAuth**。</span><span class="sxs-lookup"><span data-stu-id="6d14f-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="6d14f-466">提供 OAuth 授權伺服器，以及用來驗證持有人權杖的中介軟體。</span><span class="sxs-lookup"><span data-stu-id="6d14f-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="6d14f-467">**Owin**會使用 Twitter 的 OAuth 型服務來啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="6d14f-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="6d14f-468">此版本也包含 `Microsoft.Owin.Cors` 封裝，其中包含用來處理跨原始來源 HTTP 要求的中介軟體。</span><span class="sxs-lookup"><span data-stu-id="6d14f-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="6d14f-469">Visual Studio 2013 的最終版本中已移除 JWT 簽署的支援。</span><span class="sxs-lookup"><span data-stu-id="6d14f-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="6d14f-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="6d14f-470">Entity Framework 6</span></span>

<span data-ttu-id="6d14f-471">如需 Entity Framework 6 中的新功能和其他變更清單，請參閱[Entity Framework 版本歷程記錄](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="6d14f-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="6d14f-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="6d14f-473">ASP.NET Razor 3 包含下列新功能：</span><span class="sxs-lookup"><span data-stu-id="6d14f-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="6d14f-474">支援索引標籤編輯。</span><span class="sxs-lookup"><span data-stu-id="6d14f-474">Support for Tab editing.</span></span> <span data-ttu-id="6d14f-475">先前，使用 [保留索引標籤 **]** 選項時，Visual Studio 中的**格式檔**命令、自動縮排和自動格式化無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="6d14f-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="6d14f-476">這種變更會更正 Razor 程式碼的 Visual Studio 格式，以進行索引標籤格式。</span><span class="sxs-lookup"><span data-stu-id="6d14f-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="6d14f-477">在產生連結時支援 URL 重寫規則。</span><span class="sxs-lookup"><span data-stu-id="6d14f-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="6d14f-478">移除安全性透明屬性。</span><span class="sxs-lookup"><span data-stu-id="6d14f-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="6d14f-479">這是一種重大變更，使 Razor 3 與 MVC4 和更早版本不相容，而 Razor 2 則與 MVC5 或針對 MVC5 編譯的元件不相容。</span><span class="sxs-lookup"><span data-stu-id="6d14f-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="6d14f-480">從發行前版本的 Visual Studio 2013 中修正的 Razor 3 問題，可在[這裡](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到。</span><span class="sxs-lookup"><span data-stu-id="6d14f-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="6d14f-481">ASP.NET 應用程式暫停</span><span class="sxs-lookup"><span data-stu-id="6d14f-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="6d14f-482">ASP.NET 應用程式暫停是 .NET Framework 4.5.1 中的遊戲變更功能，它徹底改變了在單一電腦上裝載大量 ASP.NET 網站的使用者體驗和經濟模型。</span><span class="sxs-lookup"><span data-stu-id="6d14f-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="6d14f-483">如需詳細資訊，請參閱[ASP.NET 應用程式暫止–回應式共用 .net web 裝載](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="6d14f-484">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="6d14f-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="6d14f-485">本節說明 Visual Studio 2013 的 ASP.NET 和 Web 工具中的已知問題和重大變更。</span><span class="sxs-lookup"><span data-stu-id="6d14f-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="6d14f-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="6d14f-486">NuGet</span></span>

- <span data-ttu-id="6d14f-487">[使用 .sln 檔案時，新的套件還原無法在 Mono 上使用](https://nuget.codeplex.com/workitem/3596)–將在即將推出的 nuget.exe 下載和[Nuget. 命令列套件](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修正。</span><span class="sxs-lookup"><span data-stu-id="6d14f-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="6d14f-488">[新的封裝還原不適用於 Wix 專案](https://nuget.codeplex.com/workitem/3598)–將在即將推出的 nuget.exe 下載和[Nuget. 命令列套件](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修正。</span><span class="sxs-lookup"><span data-stu-id="6d14f-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="6d14f-489">[自動套件還原不適用於解決方案資料夾下的專案](https://nuget.codeplex.com/workitem/3625)–將在 NuGet 2.8 中修正。</span><span class="sxs-lookup"><span data-stu-id="6d14f-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="6d14f-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6d14f-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="6d14f-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` 不會 `IQueryable<T>` 一律傳回，因為我們新增了 `$select` 和 `$expand`的支援。</span><span class="sxs-lookup"><span data-stu-id="6d14f-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="6d14f-492">先前 `ODataQueryOptions<T>` 的範例一律會將 `ApplyTo` 的傳回值轉換至 `IQueryable<T>`。</span><span class="sxs-lookup"><span data-stu-id="6d14f-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="6d14f-493">這是稍早的作法，因為我們先前支援的查詢選項（`$filter`、`$orderby`、`$skip`、`$top`）並不會變更查詢的形狀。</span><span class="sxs-lookup"><span data-stu-id="6d14f-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="6d14f-494">現在，我們支援 `$select` 並 `$expand` 來自 `ApplyTo` 的傳回值一律不會 `IQueryable<T>`。</span><span class="sxs-lookup"><span data-stu-id="6d14f-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="6d14f-495">如果您使用稍早所述的範例程式碼，當用戶端未傳送 `$select` 和 `$expand`時，它會繼續運作。</span><span class="sxs-lookup"><span data-stu-id="6d14f-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="6d14f-496">不過，如果您想要支援 `$select` 和 `$expand` 則必須將該程式碼變更為此。</span><span class="sxs-lookup"><span data-stu-id="6d14f-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="6d14f-497">**在批次要求期間，request. Url 或 RequestCoNtext 為 null**</span><span class="sxs-lookup"><span data-stu-id="6d14f-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="6d14f-498">在批次處理案例中，從**Request**或**RequestCoNtext**存取時， **UrlHelper**是 null。</span><span class="sxs-lookup"><span data-stu-id="6d14f-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="6d14f-499">這裡目前已追蹤此問題：[批次要求的 BatchRequestCoNtext 是 null](http://aspnetwebstack.codeplex.com/workitem/1301)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="6d14f-500">此問題的因應措施是建立**UrlHelper**的新實例，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6d14f-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="6d14f-501">**建立 UrlHelper 的新實例**</span><span class="sxs-lookup"><span data-stu-id="6d14f-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="6d14f-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="6d14f-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="6d14f-503">使用 MVC5 和 OrgAuth 時，如果您有可執行 AntiForgerToken 驗證的視圖，當您將資料張貼到視圖時，可能會遇到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="6d14f-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="6d14f-504">**錯誤**：</span><span class="sxs-lookup"><span data-stu-id="6d14f-504">**Error**:</span></span>

    <span data-ttu-id="6d14f-505">*'/' 應用程式中發生伺服器錯誤。*</span><span class="sxs-lookup"><span data-stu-id="6d14f-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="6d14f-506"><em>提供的 ClaimsIdentity 上沒有類型為 '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' 或 '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' 的宣告。若要啟用以宣告為基礎之驗證的防偽權杖支援，請確認已設定的宣告提供者在它所產生的 ClaimsIdentity 實例上提供這兩個宣告。如果設定的宣告提供者改為使用不同的宣告類型做為唯一識別碼，則可以藉由設定靜態屬性 AntiForgeryConfig 來進行設定。 UniqueClaimTypeIdentifier。</em></span><span class="sxs-lookup"><span data-stu-id="6d14f-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="6d14f-507">**因應措施**：</span><span class="sxs-lookup"><span data-stu-id="6d14f-507">**Workaround**:</span></span>

    <span data-ttu-id="6d14f-508">在 global.asax 中加入下面這一行來修正它：</span><span class="sxs-lookup"><span data-stu-id="6d14f-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="6d14f-509">這會在下一版中修正。</span><span class="sxs-lookup"><span data-stu-id="6d14f-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="6d14f-510">將 MVC4 應用程式升級至 MVC5 之後，請建立解決方案並加以啟動。</span><span class="sxs-lookup"><span data-stu-id="6d14f-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="6d14f-511">您應該會看到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="6d14f-511">You should see the following error:</span></span>

    <span data-ttu-id="6d14f-512">為HostSection 無法轉換為 [B] System.web. HostSection....... i m。</span><span class="sxs-lookup"><span data-stu-id="6d14f-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="6d14f-513">類型 A 源自 ' System.webserver，Version = 2.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 '，其位置為 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ System.web. .dll ' 的內容 ' Default '。</span><span class="sxs-lookup"><span data-stu-id="6d14f-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="6d14f-514">類型 B 源自 ' System.webserver，Version = 3.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 '，位於位置 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01 \ System.web. ' 的內容 ' Default ' 中。</span><span class="sxs-lookup"><span data-stu-id="6d14f-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="6d14f-515">若要修正上述錯誤，請在專案中開啟*所有*的 web.config 檔案（包括 Views 資料夾中的檔案），然後執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6d14f-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="6d14f-516">將 "4.0.0.0" 版本 "" 的所有出現專案更新為 "5.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="6d14f-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="6d14f-517">更新 "3.0.0.0" 版本中所有出現 "2.0.0.0" 的專案，&quot;System.web&quot; 和 &quot;System.webserver&quot; 至 ""。</span><span class="sxs-lookup"><span data-stu-id="6d14f-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="6d14f-518">例如，在您進行上述變更之後，元件系結看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="6d14f-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="6d14f-519">如需將 MVC 4 專案升級為 MVC 5 的資訊，請參閱[如何將 ASP.NET mvc 4 和 WEB Api 專案升級至 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="6d14f-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="6d14f-520">當您使用用戶端驗證搭配 jQuery 不顯眼驗證時，驗證訊息有時不會對類型 = ' number ' 的 HTML 輸入元素進行錯誤。</span><span class="sxs-lookup"><span data-stu-id="6d14f-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="6d14f-521">輸入不正確數位（而不是正確的訊息必須有有效的數位）時，會顯示必要值的驗證錯誤（「需要年齡欄位」）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="6d14f-522">在建立和編輯檢視上具有整數屬性的模型的 scaffold 程式碼，通常會發現此問題。</span><span class="sxs-lookup"><span data-stu-id="6d14f-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="6d14f-523">若要解決此問題，請將編輯器 helper 變更為：</span><span class="sxs-lookup"><span data-stu-id="6d14f-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="6d14f-524">收件者:</span><span class="sxs-lookup"><span data-stu-id="6d14f-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="6d14f-525">ASP.NET MVC 5 不再支援部分信任。</span><span class="sxs-lookup"><span data-stu-id="6d14f-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="6d14f-526">連結至 MVC 或 WebAPI 二進位檔的專案應該會移除[SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)屬性和[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="6d14f-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="6d14f-527">移除這些屬性將會排除編譯器錯誤，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6d14f-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="6d14f-528">請注意，這種情況的副作用是，您無法在同一個應用程式中使用4.0 和5.0 元件。</span><span class="sxs-lookup"><span data-stu-id="6d14f-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="6d14f-529">您必須將它們全部更新為5.0。</span><span class="sxs-lookup"><span data-stu-id="6d14f-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="6d14f-530">具有 Facebook 授權的 SPA 範本在網站裝載于內部網路區域時，可能會導致 IE 不穩定</span><span class="sxs-lookup"><span data-stu-id="6d14f-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="6d14f-531">SPA 範本提供使用 Facebook 的外部登入。</span><span class="sxs-lookup"><span data-stu-id="6d14f-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="6d14f-532">當使用範本建立的專案在本機執行時，登入可能會導致 IE 當機。</span><span class="sxs-lookup"><span data-stu-id="6d14f-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="6d14f-533">解決方案:</span><span class="sxs-lookup"><span data-stu-id="6d14f-533">Solution:</span></span>

1. <span data-ttu-id="6d14f-534">在網際網路區域中主控網站;或</span><span class="sxs-lookup"><span data-stu-id="6d14f-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="6d14f-535">在 IE 以外的瀏覽器中測試案例。</span><span class="sxs-lookup"><span data-stu-id="6d14f-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="6d14f-536">Web Forms Scaffolding</span><span class="sxs-lookup"><span data-stu-id="6d14f-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="6d14f-537">Web form 樣板已從 VS2013 中移除，並將在未來的更新中提供 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6d14f-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="6d14f-538">不過，您仍然可以在 Web form 專案中使用樣板，方法是新增 MVC 相依性並產生 MVC 的樣板。</span><span class="sxs-lookup"><span data-stu-id="6d14f-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="6d14f-539">您的專案將包含 Web Forms 和 MVC 的組合。</span><span class="sxs-lookup"><span data-stu-id="6d14f-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="6d14f-540">若要將 MVC 加入至您的 Web form 專案，請加入新的 scaffold 專案，然後選取 [ **MVC 5**相依性]。</span><span class="sxs-lookup"><span data-stu-id="6d14f-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="6d14f-541">根據您是否需要所有內容檔案（例如腳本），選取 [最小] 或 [完整]。</span><span class="sxs-lookup"><span data-stu-id="6d14f-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="6d14f-542">然後，為 MVC 新增 scaffold 專案，這會在專案中建立視圖和控制器。</span><span class="sxs-lookup"><span data-stu-id="6d14f-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="6d14f-543">MVC 和 Web API 架構-HTTP 404，找不到錯誤</span><span class="sxs-lookup"><span data-stu-id="6d14f-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="6d14f-544">如果將 scaffold 專案新增至專案時遇到錯誤，您的專案可能會處於不一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="6d14f-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="6d14f-545">所做的部分變更會復原，但其他變更（例如已安裝的 NuGet 套件）將不會復原。</span><span class="sxs-lookup"><span data-stu-id="6d14f-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="6d14f-546">如果復原路由設定變更，使用者在流覽至 scaffold 專案時，會收到 HTTP 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="6d14f-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="6d14f-547">因應措施：</span><span class="sxs-lookup"><span data-stu-id="6d14f-547">Workaround:</span></span>

- <span data-ttu-id="6d14f-548">若要修正 MVC 的這個錯誤，請加入新的 scaffold 專案，然後選取 [MVC 5 相依性] （最小或完整）。</span><span class="sxs-lookup"><span data-stu-id="6d14f-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="6d14f-549">此程式會將所有必要的變更新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="6d14f-550">若要修正 Web API 的這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="6d14f-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="6d14f-551">將 WebApiConfig 類別新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6d14f-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="6d14f-552">依照下列方式，在 WebApiConfig 中註冊應用程式\_Start 方法：</span><span class="sxs-lookup"><span data-stu-id="6d14f-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
