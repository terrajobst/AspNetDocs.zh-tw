---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 和 Visual Studio 2010 Web 開發總覽 |Microsoft Docs
author: rick-anderson
description: 本檔概述 the.NET Framework 4 和 Visual Studio 2010 中包含的許多 ASP.NET 新功能。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 8c93952adb33d1ce7008ebff9d032a71eb2a5f74
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995333"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="4605c-103">ASP.NET 4 與 Visual Studio 2010 網頁程式開發概觀</span><span class="sxs-lookup"><span data-stu-id="4605c-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>

> <span data-ttu-id="4605c-104">本檔概述 the.NET Framework 4 和 Visual Studio 2010 中包含的許多 ASP.NET 新功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="4605c-105">下載此白皮書</span><span class="sxs-lookup"><span data-stu-id="4605c-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

<span data-ttu-id="4605c-106">**內容**</span><span class="sxs-lookup"><span data-stu-id="4605c-106">**Contents**</span></span>

<span data-ttu-id="4605c-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="4605c-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
<span data-ttu-id="4605c-108">Web.config 檔案[重構](#0.2__Toc253429239 "_Toc253429239")</span><span class="sxs-lookup"><span data-stu-id="4605c-108">[Web.config File Refactoring](#0.2__Toc253429239 "_Toc253429239")</span></span>  
<span data-ttu-id="4605c-109">[可擴充的輸出]快取(#0.2__Toc253429240 "_Toc253429240")</span><span class="sxs-lookup"><span data-stu-id="4605c-109">[Extensible Output Caching](#0.2__Toc253429240 "_Toc253429240")</span></span>  
[<span data-ttu-id="4605c-110">自動啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4605c-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
<span data-ttu-id="4605c-111">[永久]重新導向頁面(#0.2__Toc253429242 "_Toc253429242")</span><span class="sxs-lookup"><span data-stu-id="4605c-111">[Permanently Redirecting a Page](#0.2__Toc253429242 "_Toc253429242")</span></span>  
[<span data-ttu-id="4605c-112">縮小會話狀態</span><span class="sxs-lookup"><span data-stu-id="4605c-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="4605c-113">擴充允許的 Url 範圍</span><span class="sxs-lookup"><span data-stu-id="4605c-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
<span data-ttu-id="4605c-114">可延伸的[要求驗證](#0.2__Toc253429245 "_Toc253429245")</span><span class="sxs-lookup"><span data-stu-id="4605c-114">[Extensible Request Validation](#0.2__Toc253429245 "_Toc253429245")</span></span>  
<span data-ttu-id="4605c-115">[物件快取和物件]快取擴充性(#0.2__Toc253429246 "_Toc253429246")</span><span class="sxs-lookup"><span data-stu-id="4605c-115">[Object Caching and Object Caching Extensibility](#0.2__Toc253429246 "_Toc253429246")</span></span>  
[<span data-ttu-id="4605c-116">可擴充的 HTML、URL 和 HTTP 標頭編碼</span><span class="sxs-lookup"><span data-stu-id="4605c-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="4605c-117">單一工作者進程中個別應用程式的效能監視</span><span class="sxs-lookup"><span data-stu-id="4605c-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="4605c-118">Multi-Targeting</span><span class="sxs-lookup"><span data-stu-id="4605c-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="4605c-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="4605c-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="4605c-120">Web Forms 和 MVC 中包含的 jQuery</span><span class="sxs-lookup"><span data-stu-id="4605c-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="4605c-121">內容傳遞網路支援</span><span class="sxs-lookup"><span data-stu-id="4605c-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="4605c-122">ScriptManager 明確腳本</span><span class="sxs-lookup"><span data-stu-id="4605c-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="4605c-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="4605c-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="4605c-124">使用 MetaKeywords 和 MetaDescription 屬性設定中繼標記</span><span class="sxs-lookup"><span data-stu-id="4605c-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="4605c-125">啟用個別控制項的檢視狀態</span><span class="sxs-lookup"><span data-stu-id="4605c-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="4605c-126">瀏覽器功能的變更</span><span class="sxs-lookup"><span data-stu-id="4605c-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="4605c-127">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="4605c-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="4605c-128">設定用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="4605c-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="4605c-129">保存資料控制項中的資料列選取範圍</span><span class="sxs-lookup"><span data-stu-id="4605c-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="4605c-130">ASP.NET Chart 控制項</span><span class="sxs-lookup"><span data-stu-id="4605c-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="4605c-131">使用 QueryExtender 控制項篩選資料</span><span class="sxs-lookup"><span data-stu-id="4605c-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
[<span data-ttu-id="4605c-132">Html 編碼的程式碼運算式</span><span class="sxs-lookup"><span data-stu-id="4605c-132">Html Encoded Code Expressions</span></span>](#0.2__Toc253429265 "_Toc253429265")  
[<span data-ttu-id="4605c-133">專案範本變更</span><span class="sxs-lookup"><span data-stu-id="4605c-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="4605c-134">CSS 改良功能</span><span class="sxs-lookup"><span data-stu-id="4605c-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
<span data-ttu-id="4605c-135">隱藏[欄位周圍的 Div 元素](#0.2__Toc253429268 "_Toc253429268")</span><span class="sxs-lookup"><span data-stu-id="4605c-135">[Hiding div Elements Around Hidden Fields](#0.2__Toc253429268 "_Toc253429268")</span></span>  
[<span data-ttu-id="4605c-136">呈現樣板化控制項的外部資料表</span><span class="sxs-lookup"><span data-stu-id="4605c-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="4605c-137">ListView 控制項增強功能</span><span class="sxs-lookup"><span data-stu-id="4605c-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="4605c-138">CheckBoxList 和 RadioButtonList 控制項的增強功能</span><span class="sxs-lookup"><span data-stu-id="4605c-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="4605c-139">Menu 控制項改良功能</span><span class="sxs-lookup"><span data-stu-id="4605c-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="4605c-140">Wizard 和 CreateUserWizard 控制項 56</span><span class="sxs-lookup"><span data-stu-id="4605c-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="4605c-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="4605c-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="4605c-142">區域支援</span><span class="sxs-lookup"><span data-stu-id="4605c-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="4605c-143">資料-批註屬性驗證支援</span><span class="sxs-lookup"><span data-stu-id="4605c-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
<span data-ttu-id="4605c-144">樣板[化]協助程式(#0.2__Toc253429277 "_Toc253429277")</span><span class="sxs-lookup"><span data-stu-id="4605c-144">[Templated Helpers](#0.2__Toc253429277 "_Toc253429277")</span></span>

<span data-ttu-id="4605c-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="4605c-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="4605c-146">啟用現有專案的動態資料</span><span class="sxs-lookup"><span data-stu-id="4605c-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="4605c-147">宣告式 DynamicDataManager 控制語法</span><span class="sxs-lookup"><span data-stu-id="4605c-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="4605c-148">實體範本</span><span class="sxs-lookup"><span data-stu-id="4605c-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="4605c-149">Url 和電子郵件地址的新欄位範本</span><span class="sxs-lookup"><span data-stu-id="4605c-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="4605c-150">使用 DynamicHyperLink 控制項建立連結</span><span class="sxs-lookup"><span data-stu-id="4605c-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="4605c-151">資料模型中的繼承支援</span><span class="sxs-lookup"><span data-stu-id="4605c-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="4605c-152">支援多對多關聯性 (僅限 Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="4605c-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="4605c-153">控制顯示和支援列舉的新屬性</span><span class="sxs-lookup"><span data-stu-id="4605c-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
[<span data-ttu-id="4605c-154">增強的篩選支援</span><span class="sxs-lookup"><span data-stu-id="4605c-154">Enhanced Support for Filters</span></span>](#0.2__Toc253429287 "_Toc253429287")

<span data-ttu-id="4605c-155">**[Visual Studio 2010 Web 開發改良功能](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="4605c-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="4605c-156">改良的 CSS 相容性</span><span class="sxs-lookup"><span data-stu-id="4605c-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="4605c-157">HTML 和 JavaScript 程式碼片段</span><span class="sxs-lookup"><span data-stu-id="4605c-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="4605c-158">JavaScript IntelliSense 增強功能</span><span class="sxs-lookup"><span data-stu-id="4605c-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="4605c-159">**[使用 Visual Studio 2010 的 Web 應用程式部署](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="4605c-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="4605c-160">網頁封裝</span><span class="sxs-lookup"><span data-stu-id="4605c-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
[<span data-ttu-id="4605c-161">Web.config Transformation</span><span class="sxs-lookup"><span data-stu-id="4605c-161">Web.config Transformation</span></span>](#0.2__Toc253429294 "_Toc253429294")  
[<span data-ttu-id="4605c-162">資料庫部署</span><span class="sxs-lookup"><span data-stu-id="4605c-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
<span data-ttu-id="4605c-163">[針對 Web 應用程式按一下 [發佈]](#0.2__Toc253429296 "_Toc253429296")</span><span class="sxs-lookup"><span data-stu-id="4605c-163">[One-Click Publish for Web Applications](#0.2__Toc253429296 "_Toc253429296")</span></span>  
[<span data-ttu-id="4605c-164">Resources</span><span class="sxs-lookup"><span data-stu-id="4605c-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="4605c-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="4605c-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="4605c-166">核心服務</span><span class="sxs-lookup"><span data-stu-id="4605c-166">Core Services</span></span>

<span data-ttu-id="4605c-167">ASP.NET 4 引進了一些可改善核心 ASP.NET 服務 (例如輸出快取和會話狀態儲存體) 的功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="4605c-168">Web.config 檔案重構</span><span class="sxs-lookup"><span data-stu-id="4605c-168">Web.config File Refactoring</span></span>

<span data-ttu-id="4605c-169">`Web.config`由於新增功能 (例如 Ajax、路由及與 IIS 7 的整合), 在過去幾個版本的 .NET Framework 中, 包含 Web 應用程式設定的檔案已經大幅增加。</span><span class="sxs-lookup"><span data-stu-id="4605c-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="4605c-170">這使得設定或啟動新的 Web 應用程式變得更難, 而不需要像 Visual Studio 的工具。</span><span class="sxs-lookup"><span data-stu-id="4605c-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="4605c-171">在中, [NET Framework 4] 是主要設定元素已移至`machine.config`檔案, 而應用程式現在會繼承這些設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="4605c-172">這可讓`Web.config` ASP.NET 4 應用程式中的檔案是空的, 或只包含下列幾行, 以指定 Visual Studio 應用程式的目標架構版本:</span><span class="sxs-lookup"><span data-stu-id="4605c-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="4605c-173">可擴充的輸出快取</span><span class="sxs-lookup"><span data-stu-id="4605c-173">Extensible Output Caching</span></span>

<span data-ttu-id="4605c-174">自從 ASP.NET 1.0 發行以來, 輸出快取已讓開發人員將頁面、控制項和 HTTP 回應的產生輸出儲存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="4605c-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="4605c-175">在後續的 Web 要求中, ASP.NET 可以藉由從記憶體抓取產生的輸出, 而不是從頭開始重新產生輸出, 以更快速的方式提供內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="4605c-176">不過, 這種方法有一項限制: 產生的內容一律必須儲存在記憶體中, 而在遇到大量流量的伺服器上, 輸出快取所耗用的記憶體可以與 Web 應用程式其他部分的記憶體需求競爭。</span><span class="sxs-lookup"><span data-stu-id="4605c-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="4605c-177">ASP.NET 4 會將擴充點新增至輸出快取, 讓您可以設定一或多個自訂輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="4605c-178">輸出快取提供者可以使用任何儲存機制來保存 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="4605c-179">這可讓您建立各種持續性機制的自訂輸出快取提供者, 其中包括本機或遠端磁片、雲端存放裝置, 以及分散式快取引擎。</span><span class="sxs-lookup"><span data-stu-id="4605c-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="4605c-180">您會建立自訂輸出快取提供者, 做為衍生自新*system.web.caching.outputcacheprovider*類型的類別。</span><span class="sxs-lookup"><span data-stu-id="4605c-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="4605c-181">接著, 您可以使用*outputCache*元素的`Web.config`新*提供者*子區段, 在檔案中設定提供者, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="4605c-182">根據預設, 在 ASP.NET 4 中, 所有 HTTP 回應、轉譯的頁面和控制項都會使用記憶體中的輸出快取, 如先前範例所示, 其中*defaultProvider*屬性設定為 AspNetInternalProvider。</span><span class="sxs-lookup"><span data-stu-id="4605c-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="4605c-183">您可以為*defaultProvider*指定不同的提供者名稱, 以變更用於 Web 應用程式的預設輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="4605c-184">此外, 您可以針對每個控制項和每個要求選取不同的輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="4605c-185">若要為不同的 Web 使用者控制項選擇不同的輸出快取提供者, 最簡單的方式就是使用控制項指示詞中的新*providerName*屬性, 以宣告方式執行此動作, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="4605c-186">為 HTTP 要求指定不同的輸出快取提供者需要更多工作。</span><span class="sxs-lookup"><span data-stu-id="4605c-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="4605c-187">您不是以宣告方式指定提供者, 而是在檔案中`Global.asax`覆寫新的 GetOuputCacheProviderName 方法, 以程式設計方式指定要用於特定要求的提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="4605c-188">下列範例顯示如何執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="4605c-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="4605c-189">透過將輸出快取提供者擴充性新增至 ASP.NET 4, 您現在可以為您的網站實現更積極且更聰明的輸出快取策略。</span><span class="sxs-lookup"><span data-stu-id="4605c-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="4605c-190">例如, 您現在可以在記憶體中快取網站的「前10個」頁面, 同時在磁片上快取取得較低流量的頁面。</span><span class="sxs-lookup"><span data-stu-id="4605c-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="4605c-191">或者, 您可以針對呈現的頁面快取每個不同的組合, 但使用分散式快取, 以便從前端 Web 服務器卸載記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="4605c-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="4605c-192">自動啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4605c-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="4605c-193">某些 Web 應用程式需要載入大量資料, 或在服務第一個要求之前執行昂貴的初始化處理。</span><span class="sxs-lookup"><span data-stu-id="4605c-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="4605c-194">在舊版的 ASP.NET 中, 在這些情況下, 您必須設計自訂方法來「喚醒」 ASP.NET 應用程式, 然後在檔案中`Global.asax`的*應用\_程式載入*方法期間執行初始化程式碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="4605c-195">在 Windows Server 2008 R2 上的 IIS 7.5 上執行 ASP.NET 4 時, 可直接解決此案例的新擴充功能稱為*自動啟動*。</span><span class="sxs-lookup"><span data-stu-id="4605c-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="4605c-196">自動啟動功能提供控制的方法來啟動應用程式集區、初始化 ASP.NET 應用程式, 然後接受 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="4605c-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4605c-197">IIS 7.5 的 IIS 應用程式準備模組</span><span class="sxs-lookup"><span data-stu-id="4605c-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="4605c-198">IIS 小組已發行 IIS 7.5 應用程式準備模組的第一個 Beta 測試版本。</span><span class="sxs-lookup"><span data-stu-id="4605c-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="4605c-199">這可讓您更輕鬆地啟動應用程式, 而不是先前所述。</span><span class="sxs-lookup"><span data-stu-id="4605c-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="4605c-200">您不需要撰寫自訂程式碼, 而是在 Web 應用程式接受來自網路的要求之前, 指定要執行的資源 Url。</span><span class="sxs-lookup"><span data-stu-id="4605c-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="4605c-201">這項準備工作會在 IIS 服務啟動時執行 (如果您將 IIS 應用程式集區設定為*AlwaysRunning*), 以及 iis 工作者進程回收的時間。</span><span class="sxs-lookup"><span data-stu-id="4605c-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="4605c-202">在回收期間, 舊的 IIS 背景工作進程會繼續執行要求, 直到新產生的背景工作進程完全準備就緒為止, 讓應用程式不會因為 unprimed 快取而遇到中斷或其他問題。</span><span class="sxs-lookup"><span data-stu-id="4605c-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="4605c-203">請注意, 此模組適用于任何版本的 ASP.NET, 從2.0 版開始。</span><span class="sxs-lookup"><span data-stu-id="4605c-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="4605c-204">如需詳細資訊, 請參閱 IIS.net 網站上的[應用程式暖開機](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)。</span><span class="sxs-lookup"><span data-stu-id="4605c-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="4605c-205">如需說明如何使用準備功能的逐步解說, 請參閱 IIS.net 網站上[的使用 IIS 7.5 應用程式準備模組的消費者入門](https://www.iis.net/learn/manage)。</span><span class="sxs-lookup"><span data-stu-id="4605c-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>

<span data-ttu-id="4605c-206">若要使用自動啟動功能, iis 系統管理員會將 iis 7.5 中的應用程式集區設定為使用檔案中`applicationHost.config`的下列設定自動啟動:</span><span class="sxs-lookup"><span data-stu-id="4605c-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="4605c-207">因為單一應用程式集區可以包含多個應用程式, 所以您可以使用檔案中`applicationHost.config`的下列設定, 指定要自動啟動的個別應用程式:</span><span class="sxs-lookup"><span data-stu-id="4605c-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="4605c-208">當 iis 7.5 伺服器是冷啟動或回收個別應用程式集區時, iis 7.5 會使用檔案中`applicationHost.config`的資訊來判斷需要自動啟動的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="4605c-209">針對每個標示為要自動啟動的應用程式, IIS 7.5 會將要求傳送至 ASP.NET 4, 以在應用程式暫時不接受 HTTP 要求的狀態下啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="4605c-210">當它處於此狀態時, ASP.NET 會具現化*serviceAutoStartProvider*屬性所定義的類型 (如前一個範例所示), 並呼叫其公用進入點。</span><span class="sxs-lookup"><span data-stu-id="4605c-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="4605c-211">您可以藉由執行*IProcessHostPreloadClient*介面, 建立具有必要進入點的受控自動啟動類型, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="4605c-212">當您的初始化程式碼在*預先載入*的方法中執行, 且方法傳回之後, ASP.NET 應用程式就可以開始處理要求。</span><span class="sxs-lookup"><span data-stu-id="4605c-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="4605c-213">透過將自動啟動新增至 IIS .5 和 ASP.NET 4, 您現在有一個定義完善的方法, 可在處理第一個 HTTP 要求之前執行昂貴的應用程式初始化。</span><span class="sxs-lookup"><span data-stu-id="4605c-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="4605c-214">例如, 您可以使用新的「自動啟動」功能來初始化應用程式, 然後發出應用程式已初始化且準備接受 HTTP 流量的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="4605c-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="4605c-215">永久重新導向頁面</span><span class="sxs-lookup"><span data-stu-id="4605c-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="4605c-216">Web 應用程式在一段時間前後移動頁面和其他內容是常見的作法, 這可能會導致搜尋引擎中的過時連結累積。</span><span class="sxs-lookup"><span data-stu-id="4605c-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="4605c-217">在 ASP.NET 中, 開發人員通常會使用回應來處理舊 Url 的要求 *。重新導向*方法會將要求轉送至新的 url。</span><span class="sxs-lookup"><span data-stu-id="4605c-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="4605c-218">不過, 重新*導向*方法會發出 HTTP 302 找到 (暫時重新導向) 回應, 而當使用者嘗試存取舊的 url 時, 就會產生額外的 HTTP 來回行程。</span><span class="sxs-lookup"><span data-stu-id="4605c-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="4605c-219">ASP.NET 4 新增了新的*RedirectPermanent* helper 方法, 可讓您輕鬆地發出 HTTP 301 已移動的永久回應, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="4605c-220">可辨識永久重新導向的搜尋引擎和其他使用者代理程式將會儲存與內容相關聯的新 URL, 以排除瀏覽器暫時重新導向所不必要的來回行程。</span><span class="sxs-lookup"><span data-stu-id="4605c-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="4605c-221">縮小會話狀態</span><span class="sxs-lookup"><span data-stu-id="4605c-221">Shrinking Session State</span></span>

<span data-ttu-id="4605c-222">ASP.NET 提供兩個預設選項, 可讓您在 Web 伺服陣列中儲存會話狀態: 叫用跨進程會話狀態伺服器的會話狀態提供者, 以及將資料儲存在 Microsoft SQL Server 資料庫中的會話狀態提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="4605c-223">因為這兩個選項都牽涉到在 Web 應用程式的背景工作進程外部儲存狀態資訊, 所以必須在將會話狀態傳送到遠端存放之前進行序列化。</span><span class="sxs-lookup"><span data-stu-id="4605c-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="4605c-224">視開發人員在會話狀態中儲存多少資訊而定, 序列化資料的大小可能會變得相當大。</span><span class="sxs-lookup"><span data-stu-id="4605c-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="4605c-225">ASP.NET 4 為這兩種跨進程會話狀態提供者引進了新的壓縮選項。</span><span class="sxs-lookup"><span data-stu-id="4605c-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="4605c-226">當下列範例中顯示的*compressionEnabled*設定選項設為*true*時, ASP.NET 會使用 .NET Framework 的 GZipStream 類別來壓縮 (和解壓縮) 序列化的會話狀態 *。* .</span><span class="sxs-lookup"><span data-stu-id="4605c-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="4605c-227">只要將新的屬性新增至`Web.config`檔案, 在 Web 服務器上具有備用 CPU 週期的應用程式就能大幅降低序列化會話狀態資料的大小。</span><span class="sxs-lookup"><span data-stu-id="4605c-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="4605c-228">擴充允許的 Url 範圍</span><span class="sxs-lookup"><span data-stu-id="4605c-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="4605c-229">ASP.NET 4 引進了擴充應用程式 Url 大小的新選項。</span><span class="sxs-lookup"><span data-stu-id="4605c-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="4605c-230">舊版的 ASP.NET 會根據 NTFS 檔案路徑限制, 限制 URL 路徑長度為260個字元。</span><span class="sxs-lookup"><span data-stu-id="4605c-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="4605c-231">在 ASP.NET 4 中, 您可以選擇使用兩個新的*HTTPRuntime*設定屬性來增加 (或減少) 應用程式適用的此限制。</span><span class="sxs-lookup"><span data-stu-id="4605c-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="4605c-232">下列範例會顯示這些新屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="4605c-233">若要允許長或短的路徑 （不包含通訊協定、 伺服器名稱，以及查詢字串之 url 的部分），修改 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="4605c-234">若要允許長或短的查詢字串，修改的值 *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="4605c-235">ASP.NET 4 也可讓您設定 URL 字元檢查所使用的字元。</span><span class="sxs-lookup"><span data-stu-id="4605c-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="4605c-236">當 ASP.NET 在 URL 的路徑部分中找到不正確字元時, 它會拒絕要求併發出 HTTP 400 錯誤。</span><span class="sxs-lookup"><span data-stu-id="4605c-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="4605c-237">在舊版的 ASP.NET 中, URL 字元檢查僅限於一組固定的字元。</span><span class="sxs-lookup"><span data-stu-id="4605c-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="4605c-238">在 ASP.NET 4 中, 您可以使用*HTTPRuntime* configuration 元素的新*requestPathInvalidCharacters*屬性來自訂一組有效的字元, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidCharacters* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="4605c-239">根據預設, *requestPathInvalidCharacters*屬性會將八個字元定義為無效。</span><span class="sxs-lookup"><span data-stu-id="4605c-239">By default, the *requestPathInvalidCharacters* attribute defines eight characters as invalid.</span></span> <span data-ttu-id="4605c-240">(在預設指派給*requestPathInvalidCharacters*的字串&lt;中, 小於 ()、大於 (&gt;) 和連字號 (&amp;) 字元會進行編碼, 因為`Web.config`檔案是 XML 檔案)。您可以視需要自訂一組不正確字元。</span><span class="sxs-lookup"><span data-stu-id="4605c-240">(In the string that is assigned to *requestPathInvalidCharacters* by default, the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="4605c-241">請注意, ASP.NET 4 一律會拒絕包含 ASCII 範圍0x00 至0x1F 字元的 URL 路徑, 因為這些是 IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)) 的 RFC 2396 中所定義的無效 url 字元。</span><span class="sxs-lookup"><span data-stu-id="4605c-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="4605c-242">在執行 IIS 6 或更新版本的 Windows Server 上, HTTP.sys 通訊協定設備磁碟機會自動拒絕含有這些字元的 Url。</span><span class="sxs-lookup"><span data-stu-id="4605c-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="4605c-243">可延伸的要求驗證</span><span class="sxs-lookup"><span data-stu-id="4605c-243">Extensible Request Validation</span></span>

<span data-ttu-id="4605c-244">ASP.NET 要求驗證會搜尋傳入 HTTP 要求資料, 尋找經常用於跨網站腳本 (XSS) 攻擊的字串。</span><span class="sxs-lookup"><span data-stu-id="4605c-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="4605c-245">如果找到潛在的 XSS 字串, 要求驗證會將可疑的字串加上旗標, 並傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="4605c-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="4605c-246">內建的要求驗證只有在發現 XSS 攻擊中最常見的字串時才會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="4605c-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="4605c-247">先前嘗試讓 XSS 驗證更加積極, 會導致太多誤報。</span><span class="sxs-lookup"><span data-stu-id="4605c-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="4605c-248">不過, 客戶可能會想要以更積極的要求進行驗證, 或相反地可能想要為特定頁面或特定類型的要求, 刻意放寬 XSS 檢查。</span><span class="sxs-lookup"><span data-stu-id="4605c-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="4605c-249">在 ASP.NET 4 中, 要求驗證功能已成為可延伸, 因此您可以使用自訂的要求驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="4605c-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="4605c-250">若要擴充要求驗證, 請建立衍生自*Util. RequestValidator*類型的類別, 並設定應用程式 (在檔案的*HTTPRuntime* `Web.config`區段中) 以使用自訂類型。</span><span class="sxs-lookup"><span data-stu-id="4605c-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="4605c-251">下列範例顯示如何設定自訂要求驗證類別:</span><span class="sxs-lookup"><span data-stu-id="4605c-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="4605c-252">新的*requestValidationType*屬性需要標準 .NET Framework 類型識別碼字串, 指定提供自訂要求驗證的類別。</span><span class="sxs-lookup"><span data-stu-id="4605c-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="4605c-253">針對每個要求, ASP.NET 會叫用自訂類型來處理傳入 HTTP 要求資料的每個部分。</span><span class="sxs-lookup"><span data-stu-id="4605c-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="4605c-254">傳入 URL、所有 HTTP 標頭 (cookie 和自訂標頭) 和實體主體全都可供自訂要求驗證類別檢查, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="4605c-255">如果您不想要檢查傳入 HTTP 資料的某個部分, 要求驗證類別可以切換回, 讓 ASP.NET 預設要求驗證執行, 方法是直接呼叫*base。IsValidRequestString。*</span><span class="sxs-lookup"><span data-stu-id="4605c-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="4605c-256">物件快取和物件快取擴充性</span><span class="sxs-lookup"><span data-stu-id="4605c-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="4605c-257">自其第一版起, ASP.NET 已包含強大的記憶體中物件快取 (*system.web. Caching*)。</span><span class="sxs-lookup"><span data-stu-id="4605c-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="4605c-258">快取的實行已經很熱門, 已在非 Web 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="4605c-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="4605c-259">不過, Windows Forms 或 WPF 應用程式`System.Web.dll`只需要包含的參考, 才能夠使用 ASP.NET 物件快取。</span><span class="sxs-lookup"><span data-stu-id="4605c-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="4605c-260">為了讓快取可供所有應用程式使用, .NET Framework 4 引進了新的元件、新的命名空間、一些基底類型, 以及具體的快取執行。</span><span class="sxs-lookup"><span data-stu-id="4605c-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="4605c-261">新`System.Runtime.Caching.dll`的元件會在 system.servicemodel 命名空間中包含新的快取 API。</span><span class="sxs-lookup"><span data-stu-id="4605c-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="4605c-262">命名空間包含兩個核心的類別集合:</span><span class="sxs-lookup"><span data-stu-id="4605c-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="4605c-263">抽象類別型, 提供建立任何自訂快取實作為類型的基礎。</span><span class="sxs-lookup"><span data-stu-id="4605c-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="4605c-264">具體的記憶體內建物件快取實作為 ( *MemoryCache*類別)。</span><span class="sxs-lookup"><span data-stu-id="4605c-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="4605c-265">新的*MemoryCache*類別會密切地在 ASP.NET 快取上進行模型化, 並與 ASP.NET 共用大部分的內部快取引擎邏輯。</span><span class="sxs-lookup"><span data-stu-id="4605c-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="4605c-266">雖然*系統*中的公用快取 api 已更新為支援自訂快取的開發, 但如果您已使用 ASP.NET 快取物件, 您會在新的 api 中找到熟悉的概念。</span><span class="sxs-lookup"><span data-stu-id="4605c-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="4605c-267">若要深入討論新的*MemoryCache*類別和支援的基底 api, 則需要整份檔。</span><span class="sxs-lookup"><span data-stu-id="4605c-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="4605c-268">不過, 下列範例可讓您瞭解新的快取 API 如何運作。</span><span class="sxs-lookup"><span data-stu-id="4605c-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="4605c-269">此範例是針對 Windows Forms 應用程式所撰寫, 而不會`System.Web.dll`有任何相依性。</span><span class="sxs-lookup"><span data-stu-id="4605c-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="4605c-270">可擴充的 HTML、URL 和 HTTP 標頭編碼</span><span class="sxs-lookup"><span data-stu-id="4605c-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="4605c-271">在 ASP.NET 4 中, 您可以建立下列一般文字編碼工作的自訂編碼常式:</span><span class="sxs-lookup"><span data-stu-id="4605c-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="4605c-272">HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-272">HTML encoding.</span></span>
- <span data-ttu-id="4605c-273">URL 編碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-273">URL encoding.</span></span>
- <span data-ttu-id="4605c-274">HTML 屬性編碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="4605c-275">編碼輸出 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="4605c-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="4605c-276">您可以從新的*Util HttpEncoder*類型衍生, 然後將 ASP.NET 設定為使用檔案的*HTTPRuntime* `Web.config`區段中的自訂類型, 以建立自訂編碼器, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="4605c-277">設定自訂編碼器之後, 每當呼叫*HTTPutility.htmlencode*或*HttpServerUtility*類別的公用編碼方法時, ASP.NET 就會自動呼叫自訂編碼的執行。</span><span class="sxs-lookup"><span data-stu-id="4605c-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="4605c-278">這可讓 Web 開發小組的一個部分建立自訂編碼器來執行嚴格的字元編碼, 而 Web 開發小組的其餘部分則會繼續使用公用 ASP.NET 編碼 Api。</span><span class="sxs-lookup"><span data-stu-id="4605c-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="4605c-279">藉由在*HTTPRuntime*元素中集中設定自訂編碼器, 您可以保證來自公用 ASP.NET 編碼 api 的所有文字編碼呼叫都會透過自訂編碼器來路由傳送。</span><span class="sxs-lookup"><span data-stu-id="4605c-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="4605c-280">單一工作者進程中個別應用程式的效能監視</span><span class="sxs-lookup"><span data-stu-id="4605c-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="4605c-281">為了增加可裝載于單一伺服器上的網站數目, 許多主控者會在單一背景工作進程中執行多個 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="4605c-282">不過, 如果有多個應用程式使用單一共用背景工作進程, 伺服器系統管理員就很難以識別遇到問題的個別應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="4605c-283">ASP.NET 4 利用 CLR 引進的新資源監視功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="4605c-284">若要啟用這項功能, 您可以將下列 XML 設定程式碼片段`aspnet.config`新增至設定檔。</span><span class="sxs-lookup"><span data-stu-id="4605c-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="4605c-285">`aspnet.config`請注意, 檔案位於 .NET Framework 安裝所在的目錄中。</span><span class="sxs-lookup"><span data-stu-id="4605c-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="4605c-286">這不`Web.config`是檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-286">It is not the `Web.config` file.</span></span>

<span data-ttu-id="4605c-287">當*appDomainResourceMonitoring*功能已啟用時, [ASP.NET 應用程式] 效能類別中會提供兩個新的效能計數器: [ *% 受控的處理器時間*] 和 [*使用的受控記憶體*]。</span><span class="sxs-lookup"><span data-stu-id="4605c-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="4605c-288">這兩個效能計數器都使用新的 CLR 應用程式網域資源管理功能來追蹤估計的 CPU 時間, 以及個別 ASP.NET 應用程式的受控記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="4605c-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="4605c-289">因此, 使用 ASP.NET 4, 系統管理員現在可以更精細地查看單一背景工作進程中執行之個別應用程式的資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="4605c-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="4605c-290">多目標</span><span class="sxs-lookup"><span data-stu-id="4605c-290">Multi-Targeting</span></span>

<span data-ttu-id="4605c-291">您可以建立以特定 .NET Framework 版本為目標的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="4605c-292">在 ASP.NET 4 中, 檔案之`Web.config` *編譯*元素中的新屬性可讓您以 .NET Framework 4 和更新版本為目標。</span><span class="sxs-lookup"><span data-stu-id="4605c-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="4605c-293">如果您明確地以 .NET Framework 4 為目標, 而且您在檔案中`Web.config`包含選擇性元素 (例如*system.object*的專案), 則 .NET Framework 4 的這些元素必須是正確的。</span><span class="sxs-lookup"><span data-stu-id="4605c-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="4605c-294">(如果您未明確以 .NET Framework 4 為目標, 則會從缺少檔案中`Web.config`的專案來推斷目標架構)。</span><span class="sxs-lookup"><span data-stu-id="4605c-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="4605c-295">下列範例示範如何在檔案的*編譯* `Web.config`元素中使用*targetFramework*屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="4605c-296">請注意下列有關以特定 .NET Framework 版本為目標的:</span><span class="sxs-lookup"><span data-stu-id="4605c-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="4605c-297">在 .NET Framework 4 應用程式集區中, 如果`Web.config`檔案未包含*targetFramework* `Web.config`屬性或檔案遺失, ASP.NET 組建系統會假設 .NET Framework 4 做為目標。</span><span class="sxs-lookup"><span data-stu-id="4605c-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="4605c-298">(您可能必須對應用程式進行編碼變更, 使其在 .NET Framework 4 之下執行)。</span><span class="sxs-lookup"><span data-stu-id="4605c-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="4605c-299">如果您包含*targetFramework*屬性, 而且如果在檔案中 `Web.config`定義了 system.web 元素, 則此檔案必須包含 .NET Framework 4 的正確專案。</span><span class="sxs-lookup"><span data-stu-id="4605c-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="4605c-300">如果您使用*aspnet\_編譯器*命令來先行編譯您的應用程式 (例如在組建環境中), 您必須使用目標 framework 的正確版本*aspnet\_編譯器*命令。</span><span class="sxs-lookup"><span data-stu-id="4605c-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="4605c-301">使用隨附于 .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) 的編譯器, 針對 .NET Framework 3.5 和更早版本進行編譯。</span><span class="sxs-lookup"><span data-stu-id="4605c-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="4605c-302">使用 .NET Framework 4 隨附的編譯器來編譯使用該架構建立的應用程式, 或使用較新的版本。</span><span class="sxs-lookup"><span data-stu-id="4605c-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="4605c-303">在執行時間, 編譯器會使用安裝在電腦上的最新架構元件 (因此在 GAC 中)。</span><span class="sxs-lookup"><span data-stu-id="4605c-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="4605c-304">如果稍後會對架構進行更新 (例如, 已安裝假設版本 4.1), 您可以使用較新版本 framework 中的功能, 即使*targetFramework*屬性是以較低的版本 (例如 4.0) 為目標也一樣。</span><span class="sxs-lookup"><span data-stu-id="4605c-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="4605c-305">(不過, 在 Visual Studio 2010 的設計階段, 或當您使用*aspnet\_編譯器*命令時, 使用較新的架構功能會導致編譯器錯誤)。</span><span class="sxs-lookup"><span data-stu-id="4605c-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="4605c-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="4605c-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="4605c-307">Web Forms 和 MVC 中包含的 jQuery</span><span class="sxs-lookup"><span data-stu-id="4605c-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="4605c-308">Web Forms 和 MVC 的 Visual Studio 範本都包含開放原始碼的 jQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="4605c-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="4605c-309">當您建立新的網站或專案時, 會建立包含下列3個檔案的 [腳本] 資料夾:</span><span class="sxs-lookup"><span data-stu-id="4605c-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="4605c-310">Jquery-1.7.2.min.js 1.4.1-jQuery 程式庫的人們可讀取、unminified 版本。</span><span class="sxs-lookup"><span data-stu-id="4605c-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="4605c-311">Jquery-1.7.2.min.js 14.1. min .js – jQuery 程式庫的縮減版本。</span><span class="sxs-lookup"><span data-stu-id="4605c-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="4605c-312">Jquery-1.7.2.min.js 1.4.1-vsdoc-jQuery 程式庫的 Intellisense 檔檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="4605c-313">在開發應用程式時包含 jQuery 的 unminified 版本。</span><span class="sxs-lookup"><span data-stu-id="4605c-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="4605c-314">包含適用于生產應用程式的 jQuery 縮減版本。</span><span class="sxs-lookup"><span data-stu-id="4605c-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="4605c-315">例如, 下列 Web form 頁面說明如何使用 jQuery, 將 ASP.NET TextBox 控制項的背景色彩變更為黃色 (如果有焦點)。</span><span class="sxs-lookup"><span data-stu-id="4605c-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="4605c-316">內容傳遞網路支援</span><span class="sxs-lookup"><span data-stu-id="4605c-316">Content Delivery Network Support</span></span>

<span data-ttu-id="4605c-317">Microsoft Ajax 內容傳遞網路 (CDN) 可讓您輕鬆地將 ASP.NET Ajax 和 jQuery 腳本新增至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="4605c-318">例如, 您可以開始使用 jQuery 程式庫, 只要將`<script>`標記新增至您的頁面, 以指向 Ajax.microsoft.com, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="4605c-319">藉由利用 Microsoft Ajax CDN, 您可以大幅提升 Ajax 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="4605c-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="4605c-320">Microsoft Ajax CDN 的內容會在位於世界各地的伺服器上進行快取。</span><span class="sxs-lookup"><span data-stu-id="4605c-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="4605c-321">此外, Microsoft Ajax CDN 可讓瀏覽器重複使用位於不同網域中之網站的快取 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="4605c-322">如果您需要使用安全通訊端層來服務網頁, Microsoft Ajax 內容傳遞網路支援 SSL (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="4605c-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="4605c-323">當 CDN 無法使用時, 請執行 fallback。</span><span class="sxs-lookup"><span data-stu-id="4605c-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="4605c-324">測試回退。</span><span class="sxs-lookup"><span data-stu-id="4605c-324">Test the fallback.</span></span>

<span data-ttu-id="4605c-325">若要深入瞭解 Microsoft Ajax CDN, 請造訪下列網站:</span><span class="sxs-lookup"><span data-stu-id="4605c-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="4605c-326">ASP.NET ScriptManager 支援 Microsoft Ajax CDN。</span><span class="sxs-lookup"><span data-stu-id="4605c-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="4605c-327">只要設定一個屬性 (EnableCdn 屬性), 您就可以從 CDN 抓取所有 ASP.NET framework JavaScript 檔案:</span><span class="sxs-lookup"><span data-stu-id="4605c-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="4605c-328">當您將 EnableCdn 屬性設定為 true 值之後, ASP.NET 架構將會從 CDN 抓取所有的 ASP.NET framework JavaScript 檔案, 包括用於驗證和 UpdatePanel 的所有 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="4605c-329">設定這個屬性可能會對 web 應用程式的效能產生顯著的影響。</span><span class="sxs-lookup"><span data-stu-id="4605c-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="4605c-330">您可以使用 WebResource 屬性來設定自己的 JavaScript 檔案的 CDN 路徑。</span><span class="sxs-lookup"><span data-stu-id="4605c-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="4605c-331">新的 CdnPath 屬性會指定當您將 EnableCdn 屬性設定為 true 值時, 所使用的 CDN 路徑:</span><span class="sxs-lookup"><span data-stu-id="4605c-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="4605c-332">ScriptManager 明確腳本</span><span class="sxs-lookup"><span data-stu-id="4605c-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="4605c-333">在過去, 如果您使用 ASP.NET ScriptManger, 則必須載入整個整合型 ASP.NET Ajax 程式庫。</span><span class="sxs-lookup"><span data-stu-id="4605c-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="4605c-334">藉由利用新的 AjaxFrameworkMode 屬性, 您可以精確地控制要載入的 ASP.NET Ajax 程式庫元件, 並只載入所需 ASP.NET Ajax 程式庫的元件。</span><span class="sxs-lookup"><span data-stu-id="4605c-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="4605c-335">AjaxFrameworkMode 屬性可以設定為下列值:</span><span class="sxs-lookup"><span data-stu-id="4605c-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="4605c-336">已啟用--指定 ScriptManager 控制項自動包含 Microsoftajax.debug.js 腳本檔案, 這是每個核心架構腳本的合併腳本檔案 (舊版行為)。</span><span class="sxs-lookup"><span data-stu-id="4605c-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="4605c-337">Disabled--指定停用所有的 Microsoft Ajax 腳本功能, 而且 ScriptManager 控制項不會自動參考任何腳本。</span><span class="sxs-lookup"><span data-stu-id="4605c-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="4605c-338">Explicit--指定您將明確包含網頁所需之個別 framework core 腳本檔案的腳本參考, 而且您將會包含每個腳本檔案所需之相依性的參考。</span><span class="sxs-lookup"><span data-stu-id="4605c-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="4605c-339">例如, 如果您將 AjaxFrameworkMode 屬性設定為 Explicit 值, 則可以指定所需的特定 ASP.NET Ajax 元件腳本:</span><span class="sxs-lookup"><span data-stu-id="4605c-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="4605c-340">Web Form</span><span class="sxs-lookup"><span data-stu-id="4605c-340">Web Forms</span></span>

<span data-ttu-id="4605c-341">Web form 在發行 ASP.NET 1.0 之後已經是 ASP.NET 的核心功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="4605c-342">ASP.NET 4 的這方面有許多增強功能, 包括下列各項:</span><span class="sxs-lookup"><span data-stu-id="4605c-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="4605c-343">設定*中繼*標記的能力。</span><span class="sxs-lookup"><span data-stu-id="4605c-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="4605c-344">更充分掌控檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-344">More control over view state.</span></span>
- <span data-ttu-id="4605c-345">更簡單的方式來使用瀏覽器功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="4605c-346">支援搭配 Web Forms 使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="4605c-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="4605c-347">對產生的識別碼有更大的控制權。</span><span class="sxs-lookup"><span data-stu-id="4605c-347">More control over generated IDs.</span></span>
- <span data-ttu-id="4605c-348">能夠在資料控制中保存選取的資料列。</span><span class="sxs-lookup"><span data-stu-id="4605c-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="4605c-349">進一步控制*FormView*和*ListView*控制項中呈現的 HTML。</span><span class="sxs-lookup"><span data-stu-id="4605c-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="4605c-350">篩選資料來源控制項的支援。</span><span class="sxs-lookup"><span data-stu-id="4605c-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="4605c-351">使用 MetaKeywords 和 MetaDescription 屬性設定中繼標記</span><span class="sxs-lookup"><span data-stu-id="4605c-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="4605c-352">ASP.NET 4 會將兩個屬性新增至*頁面*類別*MetaKeywords*和*MetaDescription*。</span><span class="sxs-lookup"><span data-stu-id="4605c-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="4605c-353">這兩個屬性代表頁面中對應的*中繼*標記, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="4605c-354">這兩個屬性的運作方式與頁面的 [*標題*] 屬性相同。</span><span class="sxs-lookup"><span data-stu-id="4605c-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="4605c-355">它們會遵循下列規則:</span><span class="sxs-lookup"><span data-stu-id="4605c-355">They follow these rules:</span></span>

1. <span data-ttu-id="4605c-356">如果*標頭*專案中沒有與屬性名稱相符的*中繼*標記 (也就是*MetaKeywords* , name = "關鍵字", 代表 MetaDescription, 表示尚未設定這些屬性 *。* ), 在轉譯時, 會將*中繼*標記加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="4605c-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="4605c-357">如果已經有使用這些名稱的*中繼*標記, 這些屬性會作為現有標記內容的 get 和 set 方法。</span><span class="sxs-lookup"><span data-stu-id="4605c-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="4605c-358">您可以在執行時間設定這些屬性, 這可讓您從資料庫或其他來源取得內容, 並可讓您以動態方式設定標記, 以描述特定頁面的用途。</span><span class="sxs-lookup"><span data-stu-id="4605c-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="4605c-359">您也可以在 Web form 頁面標記的頂端, 設定 *@ Page*指示詞中的*關鍵字*和*Description*屬性, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="4605c-360">這會覆寫已在頁面中宣告的*中繼*標記內容 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="4605c-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="4605c-361">Description *meta*標記的內容是用來改善 Google 中的搜尋清單預覽。</span><span class="sxs-lookup"><span data-stu-id="4605c-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="4605c-362">(如需詳細資訊, 請參閱在 Google 網站管理員中心的 blog 中,[使用中繼描述來改善程式碼片段改造](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html))。Google 和 Windows Live Search 不會針對任何專案使用關鍵字的內容, 但其他搜尋引擎可能會。</span><span class="sxs-lookup"><span data-stu-id="4605c-362">(For details, see [Improve snippets with a meta description makeover](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="4605c-363">如需詳細資訊, 請參閱搜尋引擎指南網站上的[中繼關鍵字建議](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)。</span><span class="sxs-lookup"><span data-stu-id="4605c-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="4605c-364">這些新屬性是簡單的功能, 但可讓您不需要手動新增這些內容, 或撰寫自己的程式碼來建立*中繼*標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="4605c-365">啟用個別控制項的檢視狀態</span><span class="sxs-lookup"><span data-stu-id="4605c-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="4605c-366">根據預設, 頁面會啟用 [檢視狀態], 結果是頁面上的每個控制項都可能儲存檢視狀態, 即使應用程式不需要它也一樣。</span><span class="sxs-lookup"><span data-stu-id="4605c-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="4605c-367">檢視狀態資料會包含在頁面產生的標記中, 並會增加將頁面傳送至用戶端並將其回傳所需的時間量。</span><span class="sxs-lookup"><span data-stu-id="4605c-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="4605c-368">儲存比所需更多的檢視狀態可能會造成明顯的效能降低。</span><span class="sxs-lookup"><span data-stu-id="4605c-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="4605c-369">在舊版的 ASP.NET 中, 開發人員可以停用個別控制項的檢視狀態, 以便減少頁面大小, 但必須針對個別控制項明確地執行此動作。</span><span class="sxs-lookup"><span data-stu-id="4605c-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="4605c-370">在 ASP.NET 4 中, Web 服務器控制項包含*ViewStateMode*屬性, 可讓您依預設停用 view 狀態, 然後只針對在頁面中需要它的控制項加以啟用。</span><span class="sxs-lookup"><span data-stu-id="4605c-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="4605c-371">*ViewStateMode*屬性會採用具有三個值的列舉:*Enabled*、 *Disabled*和*Inherit*。</span><span class="sxs-lookup"><span data-stu-id="4605c-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="4605c-372">[*已啟用*] 會啟用該控制項的檢視狀態, 以及任何設定為*繼承*或未設定任何子控制項的。</span><span class="sxs-lookup"><span data-stu-id="4605c-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="4605c-373">[*已停用*] 會停用檢視狀態, 而 [*繼承*] 則會指定控制項使用父控制項的*ViewStateMode*設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="4605c-374">下列範例顯示*ViewStateMode*屬性的運作方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="4605c-375">下列頁面中控制項的標記和程式碼包含*ViewStateMode*屬性的值:</span><span class="sxs-lookup"><span data-stu-id="4605c-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="4605c-376">如您所見, 程式碼會停用 PlaceHolder1 控制項的檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="4605c-377">子 label1 控制項會繼承這個屬性值 (*繼承*是控制項的*ViewStateMode*的預設值), 因此不會儲存任何檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="4605c-378">在 PlaceHolder2 控制項中, *ViewStateMode*會設為*Enabled*, 因此 label2 會繼承這個屬性並儲存檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="4605c-379">第一次載入頁面時, 這兩個*標籤*控制項的*Text*屬性會設定為字串 "[DynamicValue]"。</span><span class="sxs-lookup"><span data-stu-id="4605c-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="4605c-380">這些設定的作用是當頁面第一次載入時, 瀏覽器中會顯示下列輸出:</span><span class="sxs-lookup"><span data-stu-id="4605c-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="4605c-381">禁止`: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="4605c-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="4605c-382">後`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="4605c-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="4605c-383">但是在回傳之後, 會顯示下列輸出:</span><span class="sxs-lookup"><span data-stu-id="4605c-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="4605c-384">禁止`: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="4605c-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="4605c-385">後`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="4605c-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="4605c-386">Label1 控制項 (其*ViewStateMode*值設定為*停用*) 並未保留在程式碼中設定的值。</span><span class="sxs-lookup"><span data-stu-id="4605c-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="4605c-387">不過, label2 控制項 (其*ViewStateMode*值設為 [*已啟用*]) 已保留其狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="4605c-388">您也可以在 *@ Page*指示詞中設定*ViewStateMode* , 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="4605c-389">*Page*類別只是另一個控制項;它會作為頁面中所有其他控制項的父控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="4605c-390">*ViewStateMode*的預設值會針對*Page*的實例*啟用*。</span><span class="sxs-lookup"><span data-stu-id="4605c-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="4605c-391">因為控制項預設為*繼承*, 除非您在頁面或控制項層級設定*ViewStateMode* , 否則控制項將會繼承*已啟用*的屬性值。</span><span class="sxs-lookup"><span data-stu-id="4605c-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="4605c-392">*ViewStateMode*屬性的值會決定只有在*EnableViewState*屬性設定為*true*時, 才會維護檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="4605c-393">如果 [ *EnableViewState* ] 屬性設定為 [ *false*], 即使*ViewStateMode*設定為 [*已啟用*], 也不會保留 view 狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="4605c-394">這項功能適用于主版頁面中的*ContentPlaceHolder*控制項, 您可以在其中將主版頁面的*ViewStateMode*設定為*停用*, 然後個別針對*ContentPlaceHolder*控制項加以啟用, 然後再進行包含需要 view 狀態的控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="4605c-395">瀏覽器功能的變更</span><span class="sxs-lookup"><span data-stu-id="4605c-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="4605c-396">ASP.NET 會使用稱為「*瀏覽器」功能*的功能, 來決定使用者用來流覽網站的瀏覽器功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="4605c-397">瀏覽器功能是由*HttpBrowserCapabilities*物件表示 (由*要求*所公開)。</span><span class="sxs-lookup"><span data-stu-id="4605c-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="4605c-398">例如, 您可以使用*HttpBrowserCapabilities*物件來判斷目前瀏覽器的類型和版本是否支援特定版本的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="4605c-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="4605c-399">或者, 您可以使用*HttpBrowserCapabilities*物件來判斷要求是否源自行動裝置。</span><span class="sxs-lookup"><span data-stu-id="4605c-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="4605c-400">*HttpBrowserCapabilities*物件是由一組瀏覽器定義檔案所驅動。</span><span class="sxs-lookup"><span data-stu-id="4605c-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="4605c-401">這些檔案包含特定瀏覽器功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4605c-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="4605c-402">在 ASP.NET 4 中, 這些瀏覽器定義檔案已更新為包含最近推出的瀏覽器和裝置的相關資訊, 例如 Google Chrome、Research 在動作中的 BlackBerry smartphone 和 Apple iPhone。</span><span class="sxs-lookup"><span data-stu-id="4605c-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="4605c-403">下列清單顯示新的瀏覽器定義檔案:</span><span class="sxs-lookup"><span data-stu-id="4605c-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="4605c-404">*blackberry.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-404">*blackberry.browser*</span></span>
- <span data-ttu-id="4605c-405">*chrome.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-405">*chrome.browser*</span></span>
- <span data-ttu-id="4605c-406">*Default.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-406">*Default.browser*</span></span>
- <span data-ttu-id="4605c-407">*firefox.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-407">*firefox.browser*</span></span>
- <span data-ttu-id="4605c-408">*gateway.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-408">*gateway.browser*</span></span>
- <span data-ttu-id="4605c-409">*generic.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-409">*generic.browser*</span></span>
- <span data-ttu-id="4605c-410">*ie.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-410">*ie.browser*</span></span>
- <span data-ttu-id="4605c-411">*iemobile.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-411">*iemobile.browser*</span></span>
- <span data-ttu-id="4605c-412">*iphone.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-412">*iphone.browser*</span></span>
- <span data-ttu-id="4605c-413">*opera.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-413">*opera.browser*</span></span>
- <span data-ttu-id="4605c-414">*safari.browser*</span><span class="sxs-lookup"><span data-stu-id="4605c-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="4605c-415">使用瀏覽器功能提供者</span><span class="sxs-lookup"><span data-stu-id="4605c-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="4605c-416">在 ASP.NET 3.5 版 Service Pack 1 中, 您可以使用下列方式定義瀏覽器的功能:</span><span class="sxs-lookup"><span data-stu-id="4605c-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="4605c-417">在電腦層級, 您可以建立或更新`.browser`下列資料夾中的 XML 檔案:</span><span class="sxs-lookup"><span data-stu-id="4605c-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="4605c-418">定義瀏覽器功能之後, 您可以從 Visual Studio 命令提示字元執行下列命令, 以便重建瀏覽器功能元件, 並將它新增至 GAC:</span><span class="sxs-lookup"><span data-stu-id="4605c-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="4605c-419">針對個別應用程式, 您可以在`.browser`應用程式的`App_Browsers`資料夾中建立檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="4605c-420">這些方法需要您變更 XML 檔案, 而針對電腦層級的變更, 您必須在執行 aspnet\_regbrowsers 處理常式之後重新開機應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="4605c-421">ASP.NET 4 包含一個稱為*瀏覽器功能提供者*的功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="4605c-422">正如其名, 這可讓您建立一個提供者, 讓您能夠使用自己的程式碼來判斷瀏覽器的功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="4605c-423">在實務上, 開發人員通常不會定義自訂瀏覽器功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="4605c-424">瀏覽器檔案很難更新, 更新程式的程式相當複雜, 而且檔案的 XML 語法`.browser`可能很複雜, 無法使用和定義。</span><span class="sxs-lookup"><span data-stu-id="4605c-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="4605c-425">若有常見的瀏覽器定義語法, 或包含最新瀏覽器定義的資料庫, 或甚至是這類資料庫的 Web 服務, 則會讓此程式變得更容易。</span><span class="sxs-lookup"><span data-stu-id="4605c-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="4605c-426">新的瀏覽器功能提供者功能可讓協力廠商開發人員能夠和實際執行這些案例。</span><span class="sxs-lookup"><span data-stu-id="4605c-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="4605c-427">使用新的 ASP.NET 4 瀏覽器功能提供者功能的主要方法有兩種: 擴充 ASP.NET 瀏覽器功能定義功能, 或完全取代它。</span><span class="sxs-lookup"><span data-stu-id="4605c-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="4605c-428">下列各節將先說明如何取代功能, 以及如何加以擴充。</span><span class="sxs-lookup"><span data-stu-id="4605c-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="4605c-429">取代 ASP.NET 瀏覽器功能功能</span><span class="sxs-lookup"><span data-stu-id="4605c-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="4605c-430">若要完全取代 ASP.NET 的瀏覽器功能定義功能, 請遵循下列步驟:</span><span class="sxs-lookup"><span data-stu-id="4605c-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="4605c-431">建立衍生自*HttpCapabilitiesProvider*的提供者類別, 並覆寫*GetBrowserCapabilities*方法, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="4605c-432">此範例中的程式碼會建立新的*HttpBrowserCapabilities*物件, 只指定名為 browser 的功能, 並將該功能設定為 MyCustomBrowser。</span><span class="sxs-lookup"><span data-stu-id="4605c-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="4605c-433">向應用程式註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="4605c-434">若要將提供者與應用程式搭配使用, 您必須將*provider*屬性加入至 `Web.config`或`Machine.config`檔案中的 browserCaps 區段。</span><span class="sxs-lookup"><span data-stu-id="4605c-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="4605c-435">(您也可以針對應用程式中的特定目錄, 定義*location*元素中的提供者屬性, 例如在特定行動裝置的資料夾中)。下列範例顯示如何在設定檔中設定*provider*屬性:</span><span class="sxs-lookup"><span data-stu-id="4605c-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="4605c-436">註冊新瀏覽器功能定義的另一種方式是使用程式碼, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="4605c-437">此代碼必須在檔案的*應用\_程式啟動*事件`Global.asax`中執行。</span><span class="sxs-lookup"><span data-stu-id="4605c-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="4605c-438">對*BrowserCapabilitiesProvider*類別所做的任何變更, 都必須在應用程式中的任何程式碼執行之前進行, 以確保快取會針對已解析的*HttpCapabilitiesBase*物件維持有效的狀態。</span><span class="sxs-lookup"><span data-stu-id="4605c-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="4605c-439">快取 HttpBrowserCapabilities 物件</span><span class="sxs-lookup"><span data-stu-id="4605c-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="4605c-440">上述範例有一個問題, 這是每次叫用自訂提供者以取得*HttpBrowserCapabilities*物件時, 就會執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="4605c-441">這可能會在每次要求期間發生多次。</span><span class="sxs-lookup"><span data-stu-id="4605c-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="4605c-442">在此範例中, 提供者的程式碼不會執行太多動作。</span><span class="sxs-lookup"><span data-stu-id="4605c-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="4605c-443">不過, 如果自訂提供者中的程式碼執行大量工作以取得*HttpBrowserCapabilities*物件, 這可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="4605c-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="4605c-444">若要避免發生這種情況, 您可以快取*HttpBrowserCapabilities*物件。</span><span class="sxs-lookup"><span data-stu-id="4605c-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="4605c-445">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4605c-445">Follow these steps:</span></span>

1. <span data-ttu-id="4605c-446">建立衍生自*HttpCapabilitiesProvider*的類別, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="4605c-447">在此範例中, 程式碼會藉由呼叫自訂 BuildCacheKey 方法來產生快取索引鍵, 並藉由呼叫自訂的 GetCacheTime 方法取得快取的時間長度。</span><span class="sxs-lookup"><span data-stu-id="4605c-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="4605c-448">然後, 此程式碼會將已解析的*HttpBrowserCapabilities*物件新增至快取。</span><span class="sxs-lookup"><span data-stu-id="4605c-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="4605c-449">您可以從快取中抓取物件, 並重複使用自訂提供者的後續要求。</span><span class="sxs-lookup"><span data-stu-id="4605c-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="4605c-450">如先前的程式所述, 向應用程式註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="4605c-451">擴充 ASP.NET 瀏覽器功能功能</span><span class="sxs-lookup"><span data-stu-id="4605c-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="4605c-452">上一節說明如何在 ASP.NET 4 中建立新的*HttpBrowserCapabilities*物件。</span><span class="sxs-lookup"><span data-stu-id="4605c-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="4605c-453">您也可以將新的瀏覽器功能定義加入至已 ASP.NET 的使用者, 以擴充 ASP.NET 瀏覽器功能的功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="4605c-454">您不需要使用 XML 瀏覽器定義即可執行此動作。</span><span class="sxs-lookup"><span data-stu-id="4605c-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="4605c-455">下列程式顯示如何。</span><span class="sxs-lookup"><span data-stu-id="4605c-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="4605c-456">建立衍生自*HttpCapabilitiesEvaluator*的類別, 並覆寫*GetBrowserCapabilities*方法, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="4605c-457">此程式碼會先使用 ASP.NET 瀏覽器功能功能來嘗試識別瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4605c-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="4605c-458">不過, 如果找不到根據要求中定義的資訊來識別的瀏覽器 (亦即, 如果*HttpBrowserCapabilities*物件的*browser*屬性是字串 "Unknown"), 則程式碼會呼叫自訂提供者 (MyBrowserCapabilitiesEvaluator) 以識別瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4605c-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="4605c-459">如先前範例所述, 向應用程式註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="4605c-460">藉由將新功能新增至現有的功能定義來擴充瀏覽器功能功能</span><span class="sxs-lookup"><span data-stu-id="4605c-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="4605c-461">除了建立自訂瀏覽器定義提供者, 以及動態建立新的瀏覽器定義以外, 您還可以使用其他功能來擴充現有的瀏覽器定義。</span><span class="sxs-lookup"><span data-stu-id="4605c-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="4605c-462">這可讓您使用接近所需的定義, 但只缺少一些功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="4605c-463">若要這麼做，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4605c-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="4605c-464">建立衍生自*HttpCapabilitiesEvaluator*的類別, 並覆寫*GetBrowserCapabilities*方法, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="4605c-465">此範例程式碼會使用下列程式碼, 擴充現有的 ASP.NET *HttpCapabilitiesEvaluator*類別, 並取得符合目前要求定義的*HttpBrowserCapabilities*物件:</span><span class="sxs-lookup"><span data-stu-id="4605c-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="4605c-466">然後, 程式碼可以新增或修改此瀏覽器的功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="4605c-467">有兩種方式可以指定新的瀏覽器功能:</span><span class="sxs-lookup"><span data-stu-id="4605c-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="4605c-468">將索引鍵/值組新增至*IDictionary*物件, 而此物件是由*HttpCapabilitiesBase*物件的*功能*屬性所公開。</span><span class="sxs-lookup"><span data-stu-id="4605c-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="4605c-469">在上述範例中, 程式碼會新增名為多點觸控且值為*true*的功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="4605c-470">設定*HttpCapabilitiesBase*物件的現有屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="4605c-471">在上述範例中, 程式碼會將 [*框架*] 屬性設定為 [ *true*]。</span><span class="sxs-lookup"><span data-stu-id="4605c-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="4605c-472">此屬性只是由 [*功能*] 屬性公開之*IDictionary*物件的存取子。</span><span class="sxs-lookup"><span data-stu-id="4605c-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="4605c-473">請注意, 此模型適用于*HttpBrowserCapabilities*的任何屬性, 包括控制介面卡。</span><span class="sxs-lookup"><span data-stu-id="4605c-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="4605c-474">如先前的程式所述, 向應用程式註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="4605c-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="4605c-475">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="4605c-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="4605c-476">ASP.NET 4 加入了使用 Web form 路由的內建支援。</span><span class="sxs-lookup"><span data-stu-id="4605c-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="4605c-477">路由可讓您設定應用程式, 以接受未對應至實體檔案的要求 Url。</span><span class="sxs-lookup"><span data-stu-id="4605c-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="4605c-478">相反地, 您可以使用路由來定義對使用者有意義的 Url, 並協助您的應用程式使用搜尋引擎優化 (SEO)。</span><span class="sxs-lookup"><span data-stu-id="4605c-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="4605c-479">例如, 在現有的應用程式中顯示產品類別目錄之頁面的 URL 可能會如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="4605c-480">藉由使用路由, 您可以將應用程式設定為接受下列 URL 來呈現相同的資訊:</span><span class="sxs-lookup"><span data-stu-id="4605c-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="4605c-481">從 ASP.NET 3.5 SP1 開始已提供路由。</span><span class="sxs-lookup"><span data-stu-id="4605c-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="4605c-482">(如需如何在 ASP.NET 3.5 SP1 中使用路由的範例, 請參閱此專案[使用具有 WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "標題的")路由專案。</span><span class="sxs-lookup"><span data-stu-id="4605c-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.")</span></span> <span data-ttu-id="4605c-483">在 Phil Haack 的 blog 上)。不過, ASP.NET 4 包含一些功能, 可讓您更輕鬆地使用路由, 包括下列各項:</span><span class="sxs-lookup"><span data-stu-id="4605c-483">on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="4605c-484">*PageRouteHandler*類別, 這是您在定義路由時所使用的簡單 HTTP 處理常式。</span><span class="sxs-lookup"><span data-stu-id="4605c-484">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="4605c-485">類別會將資料傳遞至要求所路由傳送至的頁面。</span><span class="sxs-lookup"><span data-stu-id="4605c-485">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="4605c-486">新的屬性*HttpRequest. RequestCoNtext*和*RouteData* (這是*HttpRequest. RequestCoNtext.* RouteData 物件的 proxy)。</span><span class="sxs-lookup"><span data-stu-id="4605c-486">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="4605c-487">這些屬性可讓您更輕鬆地存取從路由傳遞的資訊。</span><span class="sxs-lookup"><span data-stu-id="4605c-487">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="4605c-488">下列新的運算式產生器 (定義于 RouteUrlExpressionBuilder 和*RouteValueExpressionBuilder*中): ( *system* 。</span><span class="sxs-lookup"><span data-stu-id="4605c-488">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="4605c-489">*RouteUrl*, 可提供簡單的方式來建立對應至 ASP.NET 伺服器控制項內之路由 URL 的 URL。</span><span class="sxs-lookup"><span data-stu-id="4605c-489">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="4605c-490">*RouteValue*, 提供從*routecoNtext.routedata*物件解壓縮資訊的簡單方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-490">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="4605c-491">*RouteParameter*類別, 可讓您更輕鬆地將*routecoNtext.routedata*物件中包含的資料傳遞至資料來源控制項的查詢 (類似于[*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx))。</span><span class="sxs-lookup"><span data-stu-id="4605c-491">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="4605c-492">Web Forms 網頁的路由</span><span class="sxs-lookup"><span data-stu-id="4605c-492">Routing for Web Forms Pages</span></span>

<span data-ttu-id="4605c-493">下列範例示範如何使用*route*類別的新*MapPageRoute*方法來定義 Web Forms 路由:</span><span class="sxs-lookup"><span data-stu-id="4605c-493">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="4605c-494">ASP.NET 4 引進了*MapPageRoute*方法。</span><span class="sxs-lookup"><span data-stu-id="4605c-494">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="4605c-495">下列範例相當於前一個範例所示的 SearchRoute 定義, 但使用*PageRouteHandler*類別。</span><span class="sxs-lookup"><span data-stu-id="4605c-495">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="4605c-496">範例中的程式碼會將路由對應至實體頁面 (在第一個路由中, `~/search.aspx`到)。</span><span class="sxs-lookup"><span data-stu-id="4605c-496">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="4605c-497">第一個路由定義也會指定名為 searchterm 的參數應該從 URL 中解壓縮並傳遞至頁面。</span><span class="sxs-lookup"><span data-stu-id="4605c-497">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="4605c-498">*MapPageRoute*方法支援下列方法多載:</span><span class="sxs-lookup"><span data-stu-id="4605c-498">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="4605c-499">*MapPageRoute (字串 routeName, 字串 routeUrl, 字串 physicalFile, bool checkPhysicalUrlAccess)*</span><span class="sxs-lookup"><span data-stu-id="4605c-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="4605c-500">*MapPageRoute (字串 routeName, 字串 routeUrl, 字串 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 預設值)*</span><span class="sxs-lookup"><span data-stu-id="4605c-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="4605c-501">*MapPageRoute (字串 routeName, 字串 routeUrl, 字串 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 預設值, RouteValueDictionary 條件約束)*</span><span class="sxs-lookup"><span data-stu-id="4605c-501">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="4605c-502">*CheckPhysicalUrlAccess*參數會指定路由是否應檢查要路由至之實體頁面 (在此案例中為 search .aspx) 的安全性許可權, 以及連入 URL (在此案例中為 search/{searchterm}) 的許可權。</span><span class="sxs-lookup"><span data-stu-id="4605c-502">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="4605c-503">如果*checkPhysicalUrlAccess*的值為*false*, 則只會檢查傳入 URL 的許可權。</span><span class="sxs-lookup"><span data-stu-id="4605c-503">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="4605c-504">這些許可權會使用如下的`Web.config`設定定義于檔案中:</span><span class="sxs-lookup"><span data-stu-id="4605c-504">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="4605c-505">在範例設定中, 所有使用者的實體頁面`search.aspx`存取權除外, 除非是系統管理員角色的人員。</span><span class="sxs-lookup"><span data-stu-id="4605c-505">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="4605c-506">當*checkPhysicalUrlAccess*參數設定為*true* (這是其預設值) 時, 只允許系統管理員使用者存取 URL/search/{searchterm}, 因為實體頁面搜尋 .aspx 僅限於該角色中的使用者。</span><span class="sxs-lookup"><span data-stu-id="4605c-506">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="4605c-507">如果*checkPhysicalUrlAccess*設定為*false* , 且網站已如前一個範例所示設定, 則允許所有已驗證的使用者存取 URL/search/{searchterm}。</span><span class="sxs-lookup"><span data-stu-id="4605c-507">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="4605c-508">讀取 Web Forms 頁面中的路由資訊</span><span class="sxs-lookup"><span data-stu-id="4605c-508">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="4605c-509">在 Web form 實體頁面的程式碼中, 您可以使用兩個新的屬性, 存取路由已從 URL (或另一個物件已新增至*RouteData*物件的其他資訊) 中解壓縮的資訊:*HttpRequest. RequestCoNtext*和*RouteData*。</span><span class="sxs-lookup"><span data-stu-id="4605c-509">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="4605c-510">(*Page. RouteData*會包裝*HttpRequest. RequestCoNtext. RouteData*)。下列範例顯示如何使用*RouteData*。</span><span class="sxs-lookup"><span data-stu-id="4605c-510">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="4605c-511">此程式碼會將傳遞給 searchterm 參數的值 (如稍早的範例路由中所定義) 解壓縮。</span><span class="sxs-lookup"><span data-stu-id="4605c-511">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="4605c-512">請考慮下列要求 URL:</span><span class="sxs-lookup"><span data-stu-id="4605c-512">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="4605c-513">提出此要求時, 會在`search.aspx`頁面中轉譯「scott」一詞。</span><span class="sxs-lookup"><span data-stu-id="4605c-513">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="4605c-514">存取標記中的路由資訊</span><span class="sxs-lookup"><span data-stu-id="4605c-514">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="4605c-515">上一節所述的方法示範如何在 Web form 頁面的程式碼中取得路由資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-515">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="4605c-516">您也可以在標記中使用運算式, 讓您存取相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="4605c-516">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="4605c-517">運算式產生器是使用宣告式程式碼的強大且簡潔的方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-517">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="4605c-518">(如需詳細資訊, 請參閱 Phil Haack 的 blog 的[自訂表格達式](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)產生器中的專案 Express)。</span><span class="sxs-lookup"><span data-stu-id="4605c-518">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="4605c-519">ASP.NET 4 包含兩個用於 Web 表單路由的新運算式產生器。</span><span class="sxs-lookup"><span data-stu-id="4605c-519">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="4605c-520">下列範例顯示如何使用它們。</span><span class="sxs-lookup"><span data-stu-id="4605c-520">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="4605c-521">在此範例中, *RouteUrl*運算式是用來定義以路由參數為基礎的 URL。</span><span class="sxs-lookup"><span data-stu-id="4605c-521">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="4605c-522">如此一來, 您就不必將完整的 URL 硬式編碼到標記中, 並讓您稍後變更 URL 結構, 而不需要變更此連結。</span><span class="sxs-lookup"><span data-stu-id="4605c-522">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="4605c-523">根據稍早定義的路由, 此標記會產生下列 URL:</span><span class="sxs-lookup"><span data-stu-id="4605c-523">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="4605c-524">ASP.NET 會根據輸入參數自動處理正確的路由 (也就是, 它會產生正確的 URL)。</span><span class="sxs-lookup"><span data-stu-id="4605c-524">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="4605c-525">您也可以在運算式中包含路由名稱, 讓您指定要使用的路由。</span><span class="sxs-lookup"><span data-stu-id="4605c-525">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="4605c-526">下列範例顯示如何使用*RouteValue*運算式。</span><span class="sxs-lookup"><span data-stu-id="4605c-526">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="4605c-527">當包含此控制項的頁面執行時, [scott] 值會顯示在標籤中。</span><span class="sxs-lookup"><span data-stu-id="4605c-527">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="4605c-528">*RouteValue*運算式可讓您輕鬆地在標記中使用路由資料, 並避免必須使用更複雜的頁面。 RouteData ["x"] 標記中的語法。</span><span class="sxs-lookup"><span data-stu-id="4605c-528">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="4605c-529">使用資料來源控制參數的路由資料</span><span class="sxs-lookup"><span data-stu-id="4605c-529">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="4605c-530">*RouteParameter*類別可讓您指定路由資料, 做為資料來源控制項中查詢的參數值。</span><span class="sxs-lookup"><span data-stu-id="4605c-530">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="4605c-531">其[運作方式非常類似](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)于類別, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-531">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="4605c-532">在此情況下，路由參數 searchterm 的值將用於@companyname中的參數 *選取* 陳述式。</span><span class="sxs-lookup"><span data-stu-id="4605c-532">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the *Select* statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="4605c-533">設定用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="4605c-533">Setting Client IDs</span></span>

<span data-ttu-id="4605c-534">新的*ClientIDMode*屬性可解決 ASP.NET 中長期的問題, 也就是控制項如何為其轉譯的元素建立*id*屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-534">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="4605c-535">如果您的應用程式包含參考這些專案的用戶端腳本, 知道轉譯元素的*id*屬性就很重要。</span><span class="sxs-lookup"><span data-stu-id="4605c-535">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="4605c-536">HTML 中針對 Web 服務器控制項轉譯的*id*屬性是根據控制項的*ClientID*屬性來產生。</span><span class="sxs-lookup"><span data-stu-id="4605c-536">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="4605c-537">在 ASP.NET 4 之前, 從*ClientID*屬性產生*id*屬性的演算法, 已連接到具有識別碼的命名容器 (如果有的話), 並在重複控制項 (如資料控制項) 的情況下, 加入前置詞和順序項數.</span><span class="sxs-lookup"><span data-stu-id="4605c-537">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="4605c-538">雖然這一定會保證頁面中控制項的識別碼是唯一的, 但演算法卻導致無法預測的控制項識別碼, 因此很難在用戶端腳本中參考。</span><span class="sxs-lookup"><span data-stu-id="4605c-538">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="4605c-539">新的*ClientIDMode*屬性可讓您更精確地指定如何為控制項產生用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-539">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="4605c-540">您可以設定任何控制項的*ClientIDMode*屬性, 包括網頁的。</span><span class="sxs-lookup"><span data-stu-id="4605c-540">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="4605c-541">可能的設定如下:</span><span class="sxs-lookup"><span data-stu-id="4605c-541">Possible settings are the following:</span></span>

- <span data-ttu-id="4605c-542">*Autoid predictable* –這相當於用於產生先前版本 ASP.NET 中所使用之*ClientID*屬性值的演算法。</span><span class="sxs-lookup"><span data-stu-id="4605c-542">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="4605c-543">*Static* –這會指定*ClientID*值會與識別碼相同, 而不會串連父命名容器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-543">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="4605c-544">這在 Web 使用者控制項中很有用。</span><span class="sxs-lookup"><span data-stu-id="4605c-544">This can be useful in Web user controls.</span></span> <span data-ttu-id="4605c-545">因為 Web 使用者控制項可以位在不同的頁面上, 而且位於不同的容器控制項中, 所以很難以針對使用*autoid predictable*演算法的控制項撰寫用戶端腳本, 因為您無法預測識別碼值會是什麼。</span><span class="sxs-lookup"><span data-stu-id="4605c-545">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="4605c-546">*可預測*–此選項主要是用於使用重複範本的資料控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-546">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="4605c-547">它會串連控制項的命名容器的 ID 屬性, 但產生的*ClientID*值不會包含 "ctlxxx" 之類的字串。</span><span class="sxs-lookup"><span data-stu-id="4605c-547">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="4605c-548">此設定會與控制項的*ClientIDRowSuffix*屬性搭配運作。</span><span class="sxs-lookup"><span data-stu-id="4605c-548">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="4605c-549">您可以將*ClientIDRowSuffix*屬性設定為資料欄位的名稱, 並使用該欄位的值做為所產生之*ClientID*值的尾碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-549">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="4605c-550">一般來說, 您會使用資料記錄的主鍵做為*ClientIDRowSuffix*值。</span><span class="sxs-lookup"><span data-stu-id="4605c-550">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="4605c-551">*Inherit* –此設定是控制項的預設行為;它會指定控制項的識別碼產生與其父系相同。</span><span class="sxs-lookup"><span data-stu-id="4605c-551">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="4605c-552">您可以在頁面層級設定*ClientIDMode*屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-552">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="4605c-553">這會定義目前頁面中所有控制項的預設*ClientIDMode*值。</span><span class="sxs-lookup"><span data-stu-id="4605c-553">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="4605c-554">頁面層級的預設*ClientIDMode*值為*autoid predictable*, 而控制項層級的預設*ClientIDMode*值為*Inherit*。</span><span class="sxs-lookup"><span data-stu-id="4605c-554">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="4605c-555">因此, 如果您未在程式碼中的任何位置設定此屬性, 則所有控制項都會預設為*autoid predictable*演算法。</span><span class="sxs-lookup"><span data-stu-id="4605c-555">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="4605c-556">您可以在 *@ page*指示詞中設定頁面層級的值, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-556">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="4605c-557">您也可以在設定檔中, 于電腦 (機器) 層級或應用層級設定*ClientIDMode*值。</span><span class="sxs-lookup"><span data-stu-id="4605c-557">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="4605c-558">這會為應用程式中所有頁面上的所有控制項定義預設的*ClientIDMode*設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-558">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="4605c-559">如果您在電腦層級設定值, 它會定義該電腦上所有網站的預設*ClientIDMode*設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-559">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="4605c-560">下列範例顯示設定檔中的*ClientIDMode*設定:</span><span class="sxs-lookup"><span data-stu-id="4605c-560">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="4605c-561">如先前所述, *ClientID*屬性的值衍生自控制項父系的命名容器。</span><span class="sxs-lookup"><span data-stu-id="4605c-561">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="4605c-562">在某些情況下, 例如當您使用主版頁面時, 控制項最後可能會有類似下列所呈現 HTML 中的識別碼:</span><span class="sxs-lookup"><span data-stu-id="4605c-562">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="4605c-563">雖然標記中所顯示的*輸入*專案 (來自*TextBox*控制項) 只是頁面中的兩個命名容器 (嵌套的*ContentPlaceholder*控制項), 但因為主版頁面的處理方式, 所以最終結果是控制項識別碼, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-563">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="4605c-564">此識別碼在頁面中保證是唯一的, 但在大部分的情況下, 它會不必要地長時間。</span><span class="sxs-lookup"><span data-stu-id="4605c-564">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="4605c-565">假設您想要縮短轉譯的識別碼長度, 並能夠更充分掌控識別碼的產生方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-565">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="4605c-566">(例如, 您想要排除 "ctlxxx" 前置詞)。達到此目的的最簡單方式是設定*ClientIDMode*屬性, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-566">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="4605c-567">在此範例中, 最外層的*NamingPanel*專案的*ClientIDMode*屬性設定為*Static* , 而內部*NamingControl*元素的則設為*可預測*。</span><span class="sxs-lookup"><span data-stu-id="4605c-567">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="4605c-568">這些設定會產生下列標記 (頁面的其餘部分和主版頁面會假設與先前範例中的相同):</span><span class="sxs-lookup"><span data-stu-id="4605c-568">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="4605c-569">*靜態*設定具有重設最外層*NamingPanel*元素內任何控制項之命名階層的效果, 以及用來排除產生的識別碼中的*ContentPlaceHolder*和*MasterPage*識別碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-569">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="4605c-570">(轉譯專案的*name*屬性不受影響, 因此會保留事件、檢視狀態等的一般 ASP.NET 功能)。重設命名階層的副作用是, 即使您將*NamingPanel*元素的標記移至不同的*ContentPlaceholder*控制項, 呈現的用戶端識別碼仍會保持不變。</span><span class="sxs-lookup"><span data-stu-id="4605c-570">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="4605c-571">請注意, 您必須確定呈現的控制項識別碼是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4605c-571">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="4605c-572">如果不是, 它可能會中斷需要個別 HTML 元素之唯一識別碼的任何功能, 例如用戶端*檔. getElementById*函式。</span><span class="sxs-lookup"><span data-stu-id="4605c-572">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="4605c-573">在資料繫結控制項中建立可預測的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="4605c-573">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="4605c-574">舊版演算法在資料系結清單控制項中為控制項產生的*ClientID*值可能很長, 而且不是真正可預測的。</span><span class="sxs-lookup"><span data-stu-id="4605c-574">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="4605c-575">*ClientIDMode*功能可協助您更充分掌控這些識別碼的產生方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-575">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="4605c-576">下列範例中的標記包含*ListView*控制項:</span><span class="sxs-lookup"><span data-stu-id="4605c-576">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="4605c-577">在上述範例中, *ClientIDMode*和*RowClientIDRowSuffix*屬性是在標記中設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-577">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="4605c-578">*ClientIDRowSuffix*屬性只能用在資料繫結控制項中, 而且其行為會根據您使用的控制項而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4605c-578">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="4605c-579">其差異如下:</span><span class="sxs-lookup"><span data-stu-id="4605c-579">The differences are these:</span></span>

- <span data-ttu-id="4605c-580">*GridView*控制項: 您可以在資料來源中指定一個或多個資料行的名稱, 這會在執行時間結合以建立用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-580">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="4605c-581">例如, 如果您將*RowClientIDRowSuffix*設定為 "ProductName, ProductId", 呈現專案的控制項識別碼將會具有如下格式:</span><span class="sxs-lookup"><span data-stu-id="4605c-581">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="4605c-582">*ListView*控制項: 您可以在資料來源中指定附加至用戶端識別碼的單一資料行。</span><span class="sxs-lookup"><span data-stu-id="4605c-582">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="4605c-583">例如, 如果您將*ClientIDRowSuffix*設定為 "ProductName", 呈現的控制項識別碼將會有如下的格式:</span><span class="sxs-lookup"><span data-stu-id="4605c-583">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="4605c-584">在此情況下, 尾端1是從目前資料項目的產品識別碼衍生而來。</span><span class="sxs-lookup"><span data-stu-id="4605c-584">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="4605c-585">*中繼器*控制項-此控制項不支援*ClientIDRowSuffix*屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-585">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="4605c-586">在*中繼器*控制項中, 會使用目前資料列的索引。</span><span class="sxs-lookup"><span data-stu-id="4605c-586">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="4605c-587">當您使用 ClientIDMode = "可預測的"搭配重複項控制項時, 會產生具有下列格式的用戶端識別碼:</span><span class="sxs-lookup"><span data-stu-id="4605c-587">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="4605c-588">尾端0是目前資料列的索引。</span><span class="sxs-lookup"><span data-stu-id="4605c-588">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="4605c-589">*FormView*和*DetailsView*控制項不會顯示多個資料列, 因此它們不支援*ClientIDRowSuffix*屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-589">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="4605c-590">保存資料控制項中的資料列選取範圍</span><span class="sxs-lookup"><span data-stu-id="4605c-590">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="4605c-591">*GridView*和*ListView*控制項可讓使用者選取資料列。</span><span class="sxs-lookup"><span data-stu-id="4605c-591">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="4605c-592">在舊版的 ASP.NET 中, 選取範圍是以頁面上的資料列索引為基礎。</span><span class="sxs-lookup"><span data-stu-id="4605c-592">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="4605c-593">例如, 如果您選取第1頁上的第三個專案, 然後移至第2頁, 則會選取該頁面上的第三個專案。</span><span class="sxs-lookup"><span data-stu-id="4605c-593">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="4605c-594">只有 .NET Framework 3.5 SP1 中的動態資料專案一開始才支援保存的選取。</span><span class="sxs-lookup"><span data-stu-id="4605c-594">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="4605c-595">啟用這項功能時, 目前選取的專案會以專案的資料索引鍵為基礎。</span><span class="sxs-lookup"><span data-stu-id="4605c-595">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="4605c-596">這表示如果您在第1頁上選取第三個數據列, 並移至 [第2頁], 第2頁上不會選取任何內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-596">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="4605c-597">當您移回第1頁時, 仍然會選取第三個數據列。</span><span class="sxs-lookup"><span data-stu-id="4605c-597">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="4605c-598">使用*EnablePersistedSelection*屬性, 在所有專案中, *GridView*和*ListView*控制項現在支援保存的選取, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-598">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="4605c-599">ASP.NET Chart 控制項</span><span class="sxs-lookup"><span data-stu-id="4605c-599">ASP.NET Chart Control</span></span>

<span data-ttu-id="4605c-600">ASP.NET *Chart*控制項會展開 .NET Framework 中的資料視覺效果供應專案。</span><span class="sxs-lookup"><span data-stu-id="4605c-600">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="4605c-601">使用*Chart*控制項, 您可以建立 ASP.NET 網頁, 其具有直覺且引人注目的圖表, 以進行複雜的統計或財務分析。</span><span class="sxs-lookup"><span data-stu-id="4605c-601">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="4605c-602">ASP.NET *Chart*控制項已引進為 .NET Framework 版本 3.5 SP1 版本的附加元件, 而且屬於 .NET Framework 4 版本。</span><span class="sxs-lookup"><span data-stu-id="4605c-602">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="4605c-603">控制項包括下列功能:</span><span class="sxs-lookup"><span data-stu-id="4605c-603">The control includes the following features:</span></span>

- <span data-ttu-id="4605c-604">35 種不同的圖表類型。</span><span class="sxs-lookup"><span data-stu-id="4605c-604">35 distinct chart types.</span></span>
- <span data-ttu-id="4605c-605">不限數目的圖表區域、標題、圖例和注釋。</span><span class="sxs-lookup"><span data-stu-id="4605c-605">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="4605c-606">適用于所有圖表元素的各種外觀設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-606">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="4605c-607">三維支援大部分的圖表類型。</span><span class="sxs-lookup"><span data-stu-id="4605c-607">3-D support for most chart types.</span></span>
- <span data-ttu-id="4605c-608">可自動納入資料點的智慧型資料標籤。</span><span class="sxs-lookup"><span data-stu-id="4605c-608">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="4605c-609">帶狀線、刻度中斷和對數縮放。</span><span class="sxs-lookup"><span data-stu-id="4605c-609">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="4605c-610">超過 50 種財務和統計公式可供資料分析與轉換。</span><span class="sxs-lookup"><span data-stu-id="4605c-610">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="4605c-611">圖表資料的簡單系結和操作。</span><span class="sxs-lookup"><span data-stu-id="4605c-611">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="4605c-612">支援常見的資料格式, 例如日期、時間和貨幣。</span><span class="sxs-lookup"><span data-stu-id="4605c-612">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="4605c-613">支援互動式和事件驅動自訂, 包括使用 Ajax 的用戶端 click 事件。</span><span class="sxs-lookup"><span data-stu-id="4605c-613">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="4605c-614">狀態管理。</span><span class="sxs-lookup"><span data-stu-id="4605c-614">State management.</span></span>
- <span data-ttu-id="4605c-615">二進位資料流。</span><span class="sxs-lookup"><span data-stu-id="4605c-615">Binary streaming.</span></span>

<span data-ttu-id="4605c-616">下圖顯示 ASP.NET Chart 控制項所產生之財務圖表的範例。</span><span class="sxs-lookup"><span data-stu-id="4605c-616">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="4605c-617">圖 2：ASP.NET Chart 控制項範例</span><span class="sxs-lookup"><span data-stu-id="4605c-617">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="4605c-618">如需如何使用 ASP.NET Chart 控制項的更多範例, 請在 MSDN 網站上的[Microsoft Chart 控制項的範例環境](https://go.microsoft.com/fwlink/?LinkId=128300)頁面上下載範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-618">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="4605c-619">您可以在[Chart 控制項論壇](https://go.microsoft.com/fwlink/?LinkId=128713)中找到更多的社區內容範例。</span><span class="sxs-lookup"><span data-stu-id="4605c-619">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="4605c-620">將 Chart 控制項加入至 ASP.NET 網頁</span><span class="sxs-lookup"><span data-stu-id="4605c-620">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="4605c-621">下列範例顯示如何使用標記, 將*Chart*控制項加入至 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="4605c-621">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="4605c-622">在此範例中, *Chart*控制項會產生靜態資料點的直條圖。</span><span class="sxs-lookup"><span data-stu-id="4605c-622">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="4605c-623">使用立體圖表</span><span class="sxs-lookup"><span data-stu-id="4605c-623">Using 3-D Charts</span></span>

<span data-ttu-id="4605c-624">*Chart*控制項包含*ChartAreas*集合, 其中可包含定義圖表區域特性的*ChartArea*物件。</span><span class="sxs-lookup"><span data-stu-id="4605c-624">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="4605c-625">例如, 若要針對圖表區域使用 3-d, 請使用*顯示 area3dstyle*屬性, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-625">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="4605c-626">下圖顯示包含四個*條形*圖類型系列的立體圖表。</span><span class="sxs-lookup"><span data-stu-id="4605c-626">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="4605c-627">圖 3：立體橫條圖</span><span class="sxs-lookup"><span data-stu-id="4605c-627">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="4605c-628">使用刻度中斷和對數刻度</span><span class="sxs-lookup"><span data-stu-id="4605c-628">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="4605c-629">刻度中斷和對數刻度是在圖表中加入複雜的兩種額外方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-629">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="4605c-630">這些功能專屬於圖表區域中的每個軸。</span><span class="sxs-lookup"><span data-stu-id="4605c-630">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="4605c-631">例如, 若要在圖表區域的主要 Y 軸上使用這些功能, 請使用*ChartArea*物件中的*AxisY IsLogarithmic*和*ScaleBreakStyle*屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-631">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="4605c-632">下列程式碼片段顯示如何在主要 Y 軸上使用刻度分欄。</span><span class="sxs-lookup"><span data-stu-id="4605c-632">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="4605c-633">下圖顯示已啟用尺規分隔的 Y 軸。</span><span class="sxs-lookup"><span data-stu-id="4605c-633">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="4605c-634">圖 4：刻度中斷</span><span class="sxs-lookup"><span data-stu-id="4605c-634">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="4605c-635">使用 QueryExtender 控制項篩選資料</span><span class="sxs-lookup"><span data-stu-id="4605c-635">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="4605c-636">建立資料導向網頁的開發人員非常常見的工作是篩選資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-636">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="4605c-637">這在傳統上是藉由在資料來源控制項中建立*Where*子句來執行。</span><span class="sxs-lookup"><span data-stu-id="4605c-637">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="4605c-638">這種方法可能很複雜, 而且在某些情況下, *Where*語法並不會讓您利用基礎資料庫的完整功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-638">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="4605c-639">為了讓篩選變得更容易, ASP.NET 4 中已加入新的*QueryExtender*控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-639">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="4605c-640">這個控制項可以加入至*EntityDataSource*或*LinqDataSource*控制項, 以便篩選這些控制項所傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-640">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="4605c-641">由於*QueryExtender*控制項會依賴 LINQ, 因此在將資料傳送至頁面之前, 會先在資料庫伺服器上套用篩選, 這樣會產生非常有效率的作業。</span><span class="sxs-lookup"><span data-stu-id="4605c-641">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="4605c-642">*QueryExtender*控制項支援各種不同的篩選選項。</span><span class="sxs-lookup"><span data-stu-id="4605c-642">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="4605c-643">下列各節將說明這些選項, 並提供如何使用它們的範例。</span><span class="sxs-lookup"><span data-stu-id="4605c-643">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="4605c-644">搜尋</span><span class="sxs-lookup"><span data-stu-id="4605c-644">Search</span></span>

<span data-ttu-id="4605c-645">針對搜尋選項, *QueryExtender*控制項會在指定的欄位中執行搜尋。</span><span class="sxs-lookup"><span data-stu-id="4605c-645">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="4605c-646">在下列範例中, 控制項使用在 TextBoxSearch 控制項中輸入的文字, 並在`ProductName`和`Supplier.CompanyName`資料行中搜尋從*LinqDataSource*控制項傳回的資料中的內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-646">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="4605c-647">Range</span><span class="sxs-lookup"><span data-stu-id="4605c-647">Range</span></span>

<span data-ttu-id="4605c-648">[範圍] 選項與 [搜尋] 選項相似, 但會指定一對值來定義範圍。</span><span class="sxs-lookup"><span data-stu-id="4605c-648">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="4605c-649">在下列範例中, *QueryExtender*控制項會搜尋*LinqDataSource*控制項`UnitPrice`所傳回之資料中的資料行。</span><span class="sxs-lookup"><span data-stu-id="4605c-649">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="4605c-650">範圍會從頁面上的 TextBoxFrom 和 TextBoxTo 控制項中讀取。</span><span class="sxs-lookup"><span data-stu-id="4605c-650">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="4605c-651">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="4605c-651">PropertyExpression</span></span>

<span data-ttu-id="4605c-652">[屬性運算式] 選項可讓您定義與屬性值的比較。</span><span class="sxs-lookup"><span data-stu-id="4605c-652">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="4605c-653">如果運算式評估為*true*, 則會傳回正在檢查的資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-653">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="4605c-654">在下列範例中, *QueryExtender*控制項會藉由比較資料`Discontinued`行中的資料與頁面上 CheckBoxDiscontinued 控制項的值, 來篩選資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-654">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="4605c-655">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="4605c-655">CustomExpression</span></span>

<span data-ttu-id="4605c-656">最後, 您可以指定要與*QueryExtender*控制項搭配使用的自訂表格達式。</span><span class="sxs-lookup"><span data-stu-id="4605c-656">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="4605c-657">此選項可讓您呼叫頁面中的函式, 該函式會定義自訂篩選邏輯。</span><span class="sxs-lookup"><span data-stu-id="4605c-657">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="4605c-658">下列範例顯示如何在*QueryExtender*控制項中以宣告方式指定自訂表格達式。</span><span class="sxs-lookup"><span data-stu-id="4605c-658">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="4605c-659">下列範例顯示*QueryExtender*控制項所叫用的自訂函式。</span><span class="sxs-lookup"><span data-stu-id="4605c-659">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="4605c-660">在此情況下, 程式碼會使用 LINQ 查詢來篩選資料, 而不是使用包含*Where*子句的資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="4605c-660">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="4605c-661">這些範例一次只會顯示一個在*QueryExtender*控制項中使用的運算式。</span><span class="sxs-lookup"><span data-stu-id="4605c-661">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="4605c-662">不過, 您可以在*QueryExtender*控制項內包含多個運算式。</span><span class="sxs-lookup"><span data-stu-id="4605c-662">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="4605c-663">Html 編碼的程式碼運算式</span><span class="sxs-lookup"><span data-stu-id="4605c-663">Html Encoded Code Expressions</span></span>

<span data-ttu-id="4605c-664">某些 ASP.NET 網站 (尤其是 ASP.NET MVC) 高度依賴 using `<%` =  `expression %>`語法 (通常稱為「程式碼區塊」) 來將一些文字寫入回應。</span><span class="sxs-lookup"><span data-stu-id="4605c-664">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="4605c-665">當您使用程式碼運算式時, 很容易忘記對文字進行 HTML 編碼, 如果文字來自使用者輸入, 它可能會讓頁面保持開啟狀態為 XSS (跨網站腳本) 攻擊。</span><span class="sxs-lookup"><span data-stu-id="4605c-665">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="4605c-666">ASP.NET 4 引進了下列適用于程式碼運算式的新語法:</span><span class="sxs-lookup"><span data-stu-id="4605c-666">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="4605c-667">根據預設, 此語法會在寫入回應時使用 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-667">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="4605c-668">這個新運算式會有效地轉譯成下列內容:</span><span class="sxs-lookup"><span data-stu-id="4605c-668">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="4605c-669">例如, &lt;%:Request ["userinput>"]%&gt;針對*Request ["userinput>"]* 的值執行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-669">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="4605c-670">這項功能的目標是讓您能夠使用新的語法來取代舊語法的所有實例, 如此一來, 您就不會被迫決定要使用的每個步驟。</span><span class="sxs-lookup"><span data-stu-id="4605c-670">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="4605c-671">不過, 在某些情況下, 輸出的文字應該是 HTML 或已經過編碼, 在這種情況下, 這可能會導致雙重編碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-671">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="4605c-672">在這些情況下, ASP.NET 4 引進了一個新介面*IHtmlString*, 以及一個具體的執行*HtmlString*。</span><span class="sxs-lookup"><span data-stu-id="4605c-672">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="4605c-673">這些類型的實例可讓您指出傳回值已經過正確編碼 (或已檢查) 以顯示為 HTML, 因此值不應該再次以 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="4605c-673">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="4605c-674">例如, 下列內容不應為 (而不是) HTML 編碼:</span><span class="sxs-lookup"><span data-stu-id="4605c-674">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="4605c-675">ASP.NET MVC 2 helper 方法已更新為使用這個新的語法, 因此不會進行雙重編碼, 只有在您執行 ASP.NET 4 時才會這麼做。</span><span class="sxs-lookup"><span data-stu-id="4605c-675">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="4605c-676">當您使用 ASP.NET 3.5 SP1 執行應用程式時, 這個新的語法無法運作。</span><span class="sxs-lookup"><span data-stu-id="4605c-676">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="4605c-677">請記住, 這樣做並不保證受到 XSS 攻擊的保護。</span><span class="sxs-lookup"><span data-stu-id="4605c-677">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="4605c-678">例如, 使用不在引號中的屬性值的 HTML, 可能會包含仍然易受影響的使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="4605c-678">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="4605c-679">請注意, ASP.NET 控制項和 ASP.NET MVC helper 的輸出一律會將屬性值包含在引號中, 這是建議的方法。</span><span class="sxs-lookup"><span data-stu-id="4605c-679">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="4605c-680">同樣地, 此語法不會執行 JavaScript 編碼, 例如當您根據使用者輸入建立 JavaScript 字串時。</span><span class="sxs-lookup"><span data-stu-id="4605c-680">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="4605c-681">專案範本變更</span><span class="sxs-lookup"><span data-stu-id="4605c-681">Project Template Changes</span></span>

<span data-ttu-id="4605c-682">在舊版的 ASP.NET 中, 當您使用 Visual Studio 建立新的網站專案或 web 應用程式專案時, 產生的專案只會包含 default.aspx 頁面、預設`Web.config`檔案`App_Data`和資料夾, 如下所示示意圖</span><span class="sxs-lookup"><span data-stu-id="4605c-682">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="4605c-683">Visual Studio 也支援空白的網站專案類型, 完全不包含任何檔案, 如下圖所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-683">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="4605c-684">結果是, 對於初學者來說, 如何建立生產 Web 應用程式的指引非常少。</span><span class="sxs-lookup"><span data-stu-id="4605c-684">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="4605c-685">因此, ASP.NET 4 引進三個新的範本, 一個用於空白的 Web 應用程式專案, 另一個用於 Web 應用程式和網站專案。</span><span class="sxs-lookup"><span data-stu-id="4605c-685">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="4605c-686">空白 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="4605c-686">Empty Web Application Template</span></span>

<span data-ttu-id="4605c-687">顧名思義, 空的 Web 應用程式範本是一個減少的 Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="4605c-687">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="4605c-688">您可以從 [Visual Studio 新增專案] 對話方塊中選取此專案範本, 如下圖所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-688">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="4605c-689">([按一下以查看完整大小的影像](overview/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="4605c-689">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="4605c-690">當您建立空的 ASP.NET Web 應用程式時, Visual Studio 會建立下列資料夾版面配置:</span><span class="sxs-lookup"><span data-stu-id="4605c-690">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="4605c-691">這類似于舊版 ASP.NET 中的空白網站版面配置, 但有一個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4605c-691">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="4605c-692">在 Visual Studio 2010 中, 空白 web 應用程式和空的網站專案包含下列`Web.config`最小檔案, 其中包含 Visual Studio 用來識別專案目標架構的資訊:</span><span class="sxs-lookup"><span data-stu-id="4605c-692">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="4605c-693">若沒有這個*targetFramework*屬性, Visual Studio 預設為以 .NET Framework 2.0 為目標, 以便在開啟繼承應用程式時保留相容性。</span><span class="sxs-lookup"><span data-stu-id="4605c-693">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="4605c-694">Web 應用程式和網站專案範本</span><span class="sxs-lookup"><span data-stu-id="4605c-694">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="4605c-695">隨附于 Visual Studio 2010 的其他兩個新專案範本包含重大變更。</span><span class="sxs-lookup"><span data-stu-id="4605c-695">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="4605c-696">下圖顯示當您建立新的 Web 應用程式專案時, 所建立的專案版面配置。</span><span class="sxs-lookup"><span data-stu-id="4605c-696">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="4605c-697">(網站專案的版面配置幾乎完全相同)。</span><span class="sxs-lookup"><span data-stu-id="4605c-697">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="4605c-698">專案包含一些未在舊版中建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-698">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="4605c-699">此外, 新的 Web 應用程式專案是以基本成員資格功能來設定, 可讓您快速開始保護新應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="4605c-699">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="4605c-700">由於此包含, 新專案`Web.config`的檔案會包含用來設定成員資格、角色和設定檔的專案。</span><span class="sxs-lookup"><span data-stu-id="4605c-700">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="4605c-701">下列範例會顯示新`Web.config` Web 應用程式專案的檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-701">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="4605c-702">(在此情況下, *roleManager*會停用)。</span><span class="sxs-lookup"><span data-stu-id="4605c-702">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="4605c-703">([按一下以查看完整大小的影像](overview/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="4605c-703">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="4605c-704">專案也包含`Account`目錄中的`Web.config`第二個檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-704">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="4605c-705">第二個設定檔提供一種方法來保護非登入使用者的 ChangePassword 頁面存取。</span><span class="sxs-lookup"><span data-stu-id="4605c-705">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="4605c-706">下列範例會顯示第二個`Web.config`檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-706">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="4605c-707">新專案範本中預設建立的頁面也包含比舊版更多的內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-707">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="4605c-708">專案包含預設的主版頁面和 CSS 檔案, 預設頁面 (default.aspx) 預設會設定為使用主版頁面。</span><span class="sxs-lookup"><span data-stu-id="4605c-708">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="4605c-709">結果是當您第一次執行 Web 應用程式或網站時, 預設 (首頁) 頁面已經可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="4605c-709">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="4605c-710">事實上, 它類似于您在啟動新的 MVC 應用程式時所看到的預設頁面。</span><span class="sxs-lookup"><span data-stu-id="4605c-710">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="4605c-711">([按一下以查看完整大小的影像](overview/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="4605c-711">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="4605c-712">這些專案範本的變更目的是提供如何開始建立新 Web 應用程式的指引。</span><span class="sxs-lookup"><span data-stu-id="4605c-712">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="4605c-713">在語義正確、嚴格的 XHTML 1.0 相容標記和使用 CSS 指定的版面配置中, 範本中的頁面代表建立 ASP.NET 4 Web 應用程式的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="4605c-713">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="4605c-714">預設頁面也有兩個數據行的版面配置, 您可以輕鬆地自訂。</span><span class="sxs-lookup"><span data-stu-id="4605c-714">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="4605c-715">例如, 假設您想要在新的 Web 應用程式中變更一些色彩, 並插入您的公司標誌來取代 [我的 ASP.NET] 應用程式標誌。</span><span class="sxs-lookup"><span data-stu-id="4605c-715">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="4605c-716">若要這麼做, 請在下`Content`建立新的目錄, 以儲存您的標誌影像:</span><span class="sxs-lookup"><span data-stu-id="4605c-716">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="4605c-717">若要將影像加入至頁面, 請開啟`Site.Master`檔案, 尋找定義 My ASP.NET 應用程式文字的位置, 並以其*src*屬性設定為新標誌影像的*image*元素取代它, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-717">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="4605c-718">([按一下以查看完整大小的影像](overview/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="4605c-718">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="4605c-719">接著, 您可以移至網站 .css 檔案, 並修改 CSS 類別定義來變更頁面的背景色彩, 以及標頭的色彩。</span><span class="sxs-lookup"><span data-stu-id="4605c-719">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="4605c-720">這些變更的結果是, 您可以輕鬆地顯示自訂的首頁:</span><span class="sxs-lookup"><span data-stu-id="4605c-720">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="4605c-721">([按一下以查看完整大小的影像](overview/_static/image25.png))</span><span class="sxs-lookup"><span data-stu-id="4605c-721">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="4605c-722">CSS 改良功能</span><span class="sxs-lookup"><span data-stu-id="4605c-722">CSS Improvements</span></span>

<span data-ttu-id="4605c-723">ASP.NET 4 中的其中一個主要工作領域, 是為了協助呈現符合最新 HTML 標準的 HTML。</span><span class="sxs-lookup"><span data-stu-id="4605c-723">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="4605c-724">這包括 ASP.NET Web 服務器控制項如何使用 CSS 樣式的變更。</span><span class="sxs-lookup"><span data-stu-id="4605c-724">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="4605c-725">呈現的相容性設定</span><span class="sxs-lookup"><span data-stu-id="4605c-725">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="4605c-726">根據預設, 當 Web 應用程式或網站的目標為 .NET Framework 4 時, *pages*元素的*controlRenderingCompatibilityVersion*屬性會設定為 "4.0"。</span><span class="sxs-lookup"><span data-stu-id="4605c-726">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="4605c-727">此元素定義于電腦層級`Web.config`檔案中, 而且預設會套用至所有 ASP.NET 4 應用程式:</span><span class="sxs-lookup"><span data-stu-id="4605c-727">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="4605c-728">*ControlRenderingCompatibility*的值是字串, 它允許未來版本中有可能的新版本定義。</span><span class="sxs-lookup"><span data-stu-id="4605c-728">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="4605c-729">在目前的版本中, 此屬性支援下列值:</span><span class="sxs-lookup"><span data-stu-id="4605c-729">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="4605c-730">"3.5".</span><span class="sxs-lookup"><span data-stu-id="4605c-730">"3.5".</span></span> <span data-ttu-id="4605c-731">此設定表示舊版的轉譯和標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-731">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="4605c-732">控制項所轉譯的標記是 100% 回溯相容, 而且會接受*xhtmlConformance*屬性的設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-732">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="4605c-733">"4.0".</span><span class="sxs-lookup"><span data-stu-id="4605c-733">"4.0".</span></span> <span data-ttu-id="4605c-734">如果屬性具有這項設定, ASP.NET Web 服務器控制項就會執行下列動作:</span><span class="sxs-lookup"><span data-stu-id="4605c-734">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="4605c-735">*XhtmlConformance*屬性一律會被視為「嚴格」。</span><span class="sxs-lookup"><span data-stu-id="4605c-735">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="4605c-736">因此, 控制項會呈現 XHTML 1.0 嚴格標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-736">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="4605c-737">停用非輸入控制項不再呈現不正確樣式。</span><span class="sxs-lookup"><span data-stu-id="4605c-737">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="4605c-738">隱藏欄位周圍的*div*元素現在已樣式化, 因此不會干擾使用者建立的 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="4605c-738">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="4605c-739">Menu 控制項會呈現在語義上正確且符合協助工具方針的標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-739">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="4605c-740">驗證控制項不會轉譯內嵌樣式。</span><span class="sxs-lookup"><span data-stu-id="4605c-740">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="4605c-741">先前呈現 border = "0" 的控制項 (衍生自 ASP.NET*資料表*控制項的控制項和 ASP.NET*影像*控制項) 不再轉譯此屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-741">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="4605c-742">停用控制項</span><span class="sxs-lookup"><span data-stu-id="4605c-742">Disabling Controls</span></span>

<span data-ttu-id="4605c-743">在 ASP.NET 3.5 SP1 和更早版本中, 架構會針對*已啟用*屬性設為*false*的任何控制項, 在 HTML 標籤中呈現*已停用*的屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-743">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="4605c-744">不過, 根據 HTML 4.01 規格, 只有*輸入*元素應該有這個屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-744">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="4605c-745">在 ASP.NET 4 中, 您可以將*controlRenderingCompatibilityVersion*屬性設定為 "3.5", 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-745">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="4605c-746">您可能會建立*標籤*控制項的標記, 如下所示, 這會停用控制項:</span><span class="sxs-lookup"><span data-stu-id="4605c-746">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="4605c-747">*標籤*控制項會轉譯下列 HTML:</span><span class="sxs-lookup"><span data-stu-id="4605c-747">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="4605c-748">在 ASP.NET 4 中, 您可以將*controlRenderingCompatibilityVersion*設定為 "4.0"。</span><span class="sxs-lookup"><span data-stu-id="4605c-748">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* to "4.0".</span></span> <span data-ttu-id="4605c-749">在這種情況下, 當控制項的*Enabled*屬性設定為*false*時, 只有轉譯*輸入*專案的控制項會轉譯*已停用*的屬性。</span><span class="sxs-lookup"><span data-stu-id="4605c-749">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="4605c-750">不會轉譯 HTML*輸入*專案的控制項會改為轉譯參考 CSS 類別的*類別*屬性, 您可以用來定義停用的控制面板。</span><span class="sxs-lookup"><span data-stu-id="4605c-750">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="4605c-751">例如, 先前範例中所示的*標籤*控制項會產生下列標記:</span><span class="sxs-lookup"><span data-stu-id="4605c-751">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="4605c-752">為此控制項指定之類別的預設值為 "aspNetDisabled"。</span><span class="sxs-lookup"><span data-stu-id="4605c-752">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="4605c-753">不過, 您可以藉由設定*WebControl*類別的靜態*DisabledCssClass*靜態屬性來變更這個預設值。</span><span class="sxs-lookup"><span data-stu-id="4605c-753">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="4605c-754">針對控制項開發人員, 用於特定控制項的行為也可以使用*SupportsDisabledAttribute*屬性來定義。</span><span class="sxs-lookup"><span data-stu-id="4605c-754">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="4605c-755">隱藏欄位周圍的 div 元素</span><span class="sxs-lookup"><span data-stu-id="4605c-755">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="4605c-756">ASP.NET 2.0 和更新版本會在*div*元素內轉譯系統特定的隱藏欄位 (例如用來儲存檢視狀態資訊的*hidden*元素), 以符合 XHTML 標準。</span><span class="sxs-lookup"><span data-stu-id="4605c-756">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="4605c-757">不過, 當 CSS 規則影響頁面上的*div*元素時, 這可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="4605c-757">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="4605c-758">例如, 它可能會導致頁面上出現一條圖元線, 這是隱藏的*div*元素周圍。</span><span class="sxs-lookup"><span data-stu-id="4605c-758">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="4605c-759">在 ASP.NET 4 中, 括住 ASP.NET 所產生之隱藏欄位的*div*元素會新增 CSS 類別參考, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-759">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="4605c-760">接著, 您可以定義僅適用于 ASP.NET 所產生*隱藏*元素的 CSS 類別, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-760">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="4605c-761">呈現樣板化控制項的外部資料表</span><span class="sxs-lookup"><span data-stu-id="4605c-761">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="4605c-762">根據預設, 支援範本的下列 ASP.NET Web 服務器控制項, 會自動包裝在用來套用內嵌樣式的外部資料表中:</span><span class="sxs-lookup"><span data-stu-id="4605c-762">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="4605c-763">*FormView*</span><span class="sxs-lookup"><span data-stu-id="4605c-763">*FormView*</span></span>
- <span data-ttu-id="4605c-764">*登入*</span><span class="sxs-lookup"><span data-stu-id="4605c-764">*Login*</span></span>
- <span data-ttu-id="4605c-765">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="4605c-765">*PasswordRecovery*</span></span>
- <span data-ttu-id="4605c-766">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="4605c-766">*ChangePassword*</span></span>
- <span data-ttu-id="4605c-767">*導向*</span><span class="sxs-lookup"><span data-stu-id="4605c-767">*Wizard*</span></span>
- <span data-ttu-id="4605c-768">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="4605c-768">*CreateUserWizard*</span></span>

<span data-ttu-id="4605c-769">已將名為*RenderOuterTable*的新屬性新增至這些控制項, 以允許從標記中移除外部資料表。</span><span class="sxs-lookup"><span data-stu-id="4605c-769">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="4605c-770">例如, 請考慮使用*FormView*控制項的下列範例:</span><span class="sxs-lookup"><span data-stu-id="4605c-770">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="4605c-771">此標記會將下列輸出轉譯至頁面, 其中包含 HTML 資料表:</span><span class="sxs-lookup"><span data-stu-id="4605c-771">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="4605c-772">若要防止呈現資料表, 您可以設定*FormView*控制項的*RenderOuterTable*屬性, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-772">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="4605c-773">上一個範例會轉譯下列輸出, 而不含*table*、 *tr*和*td*元素:</span><span class="sxs-lookup"><span data-stu-id="4605c-773">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="4605c-774">內容</span><span class="sxs-lookup"><span data-stu-id="4605c-774">Content</span></span>

<span data-ttu-id="4605c-775">這項增強功能可讓您更輕鬆地使用 CSS 將控制項的內容樣式, 因為控制項不會轉譯任何未預期的標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-775">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="4605c-776">請注意, 這項變更會停用 Visual Studio 2010 設計工具中自動格式化函式的支援, 因為已不再有可以主控自動格式選項所產生之樣式屬性的*table*元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-776">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="4605c-777">ListView 控制項增強功能</span><span class="sxs-lookup"><span data-stu-id="4605c-777">ListView Control Enhancements</span></span>

<span data-ttu-id="4605c-778">*ListView*控制項在 ASP.NET 4 中變得更容易使用。</span><span class="sxs-lookup"><span data-stu-id="4605c-778">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="4605c-779">舊版的控制項需要您指定一個版面配置範本, 其中包含具有已知識別碼的伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-779">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="4605c-780">下列標記顯示如何在 ASP.NET 3.5 中使用*ListView*控制項的典型範例。</span><span class="sxs-lookup"><span data-stu-id="4605c-780">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="4605c-781">在 ASP.NET 4 中, *ListView*控制項不需要版面配置範本。</span><span class="sxs-lookup"><span data-stu-id="4605c-781">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="4605c-782">先前範例中所顯示的標記可以取代為下列標記:</span><span class="sxs-lookup"><span data-stu-id="4605c-782">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="4605c-783">CheckBoxList 和 RadioButtonList 控制項的增強功能</span><span class="sxs-lookup"><span data-stu-id="4605c-783">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="4605c-784">在 ASP.NET 3.5 中, 您可以使用下列兩個設定來指定*CheckBoxList*和*RadioButtonList*的版面配置:</span><span class="sxs-lookup"><span data-stu-id="4605c-784">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="4605c-785">*Flow*。</span><span class="sxs-lookup"><span data-stu-id="4605c-785">*Flow*.</span></span> <span data-ttu-id="4605c-786">控制項會呈現*範圍*元素以包含其內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-786">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="4605c-787">*資料表*。</span><span class="sxs-lookup"><span data-stu-id="4605c-787">*Table*.</span></span> <span data-ttu-id="4605c-788">控制項會呈現包含其內容的*table*元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-788">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="4605c-789">下列範例會顯示每個控制項的標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-789">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="4605c-790">根據預設, 控制項會呈現類似下列的 HTML:</span><span class="sxs-lookup"><span data-stu-id="4605c-790">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="4605c-791">因為這些控制項包含專案的清單, 若要轉譯語義正確的 HTML, 則應該使用 HTML 清單 (*li*) 元素來轉譯其內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-791">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="4605c-792">這讓使用輔助技術閱讀網頁的使用者更容易, 並使用 CSS 讓控制項更容易進行樣式。</span><span class="sxs-lookup"><span data-stu-id="4605c-792">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="4605c-793">在 ASP.NET 4 中, *CheckBoxList*和*RadioButtonList*控制項支援*RepeatLayout*屬性的下列新值:</span><span class="sxs-lookup"><span data-stu-id="4605c-793">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="4605c-794">*OrderedList* –內容會轉譯為*ol*元素內的*li*元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-794">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="4605c-795">*UnorderedList* –內容會轉譯為*ul*元素內的*li*元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-795">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="4605c-796">下列範例顯示如何使用這些新的值。</span><span class="sxs-lookup"><span data-stu-id="4605c-796">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="4605c-797">上述標記會產生下列 HTML:</span><span class="sxs-lookup"><span data-stu-id="4605c-797">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="4605c-798">注意: 如果您將*RepeatLayout*設定為*OrderedList*或*UnorderedList*, 就無法再使用*RepeatDirection*屬性, 而且如果已在您的標記或程式碼中設定屬性, 就會在執行時間擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4605c-798">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="4605c-799">屬性不會有任何值, 因為這些控制項的視覺化版面配置是使用 CSS 來定義的。</span><span class="sxs-lookup"><span data-stu-id="4605c-799">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="4605c-800">Menu 控制項改良功能</span><span class="sxs-lookup"><span data-stu-id="4605c-800">Menu Control Improvements</span></span>

<span data-ttu-id="4605c-801">在 ASP.NET 4 之前, *Menu*控制項會呈現一系列的 HTML 資料表。</span><span class="sxs-lookup"><span data-stu-id="4605c-801">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="4605c-802">這使得在設定內嵌屬性以外套用 CSS 樣式, 也不符合協助工具標準。</span><span class="sxs-lookup"><span data-stu-id="4605c-802">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="4605c-803">在 ASP.NET 4 中, 控制項現在會使用包含未排序清單和清單元素的語義標記來呈現 HTML。</span><span class="sxs-lookup"><span data-stu-id="4605c-803">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="4605c-804">下列範例會在*Menu*控制項的 ASP.NET 網頁中顯示標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-804">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="4605c-805">當頁面呈現時, 控制項會產生下列 HTML (為了清楚起見, 已省略*onclick*程式碼):</span><span class="sxs-lookup"><span data-stu-id="4605c-805">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="4605c-806">除了轉譯改善之外, 也使用焦點管理來改善功能表的鍵盤導覽。</span><span class="sxs-lookup"><span data-stu-id="4605c-806">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="4605c-807">當*功能表*控制項取得焦點時, 您可以使用方向鍵來流覽元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-807">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="4605c-808">*Menu*控制項現在也會附加可存取的豐富網際網路應用程式 (ARIA) 角色和屬性下列次數 w[翼的](http://www.w3.org/TR/wai-aria-practices/#menu "功能表 ARIA 方針"), 以改善協助工具。</span><span class="sxs-lookup"><span data-stu-id="4605c-808">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="4605c-809">Menu 控制項的樣式是在頁面頂端的樣式區塊中轉譯, 而不是以轉譯的 HTML 專案作為程式列來呈現。</span><span class="sxs-lookup"><span data-stu-id="4605c-809">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="4605c-810">如果您想要完全掌控控制項的樣式, 您可以將新的*IncludeStyleBlock*屬性設定為*false*, 在此情況下不會發出樣式區塊。</span><span class="sxs-lookup"><span data-stu-id="4605c-810">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="4605c-811">使用此屬性的其中一種方式是使用 Visual Studio 設計工具中的自動格式化功能來設定功能表的外觀。</span><span class="sxs-lookup"><span data-stu-id="4605c-811">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="4605c-812">接著, 您可以執行頁面, 開啟頁面來源, 然後將轉譯的樣式區塊複製到外部 CSS 檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-812">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="4605c-813">在 Visual Studio 中, 復原樣式, 並將*IncludeStyleBlock*設定為*false*。</span><span class="sxs-lookup"><span data-stu-id="4605c-813">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="4605c-814">結果是會使用外部樣式表單中的樣式來定義功能表外觀。</span><span class="sxs-lookup"><span data-stu-id="4605c-814">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="4605c-815">Wizard 和 CreateUserWizard 控制項</span><span class="sxs-lookup"><span data-stu-id="4605c-815">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="4605c-816">ASP.NET *Wizard*和*CreateUserWizard*控制項支援範本, 可讓您定義所呈現的 HTML。</span><span class="sxs-lookup"><span data-stu-id="4605c-816">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="4605c-817">(*CreateUserWizard*衍生自*Wizard*)。下列範例顯示完整樣板化*CreateUserWizard*控制項的標記:</span><span class="sxs-lookup"><span data-stu-id="4605c-817">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="4605c-818">控制項會呈現如下的 HTML:</span><span class="sxs-lookup"><span data-stu-id="4605c-818">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="4605c-819">在 ASP.NET 3.5 SP1 中, 雖然您可以變更範本內容, 但您仍然無法控制*Wizard*控制項的輸出。</span><span class="sxs-lookup"><span data-stu-id="4605c-819">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="4605c-820">在 ASP.NET 4 中, 您可以建立*LayoutTemplate*範本並插入*預留位置*控制項 (使用保留名稱), 以指定您希望*Wizard 控制項*呈現的方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-820">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="4605c-821">下列範例顯示這種情況:</span><span class="sxs-lookup"><span data-stu-id="4605c-821">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="4605c-822">此範例會在*LayoutTemplate*元素中包含下列已命名的預留位置:</span><span class="sxs-lookup"><span data-stu-id="4605c-822">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="4605c-823">*headerPlaceholder* –在執行時間, 這會由*system.windows.controls.headereditemscontrol.headertemplate*元素的內容所取代。</span><span class="sxs-lookup"><span data-stu-id="4605c-823">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="4605c-824">*sideBarPlaceholder* –在執行時間, 這會由*SideBarTemplate*元素的內容所取代。</span><span class="sxs-lookup"><span data-stu-id="4605c-824">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="4605c-825">*wizardStepPlaceHolder* –在執行時間, 這會由*WizardStepTemplate*元素的內容所取代。</span><span class="sxs-lookup"><span data-stu-id="4605c-825">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="4605c-826">*navigationPlaceholder* –在執行時間, 這會由您已定義的任何導覽範本取代。</span><span class="sxs-lookup"><span data-stu-id="4605c-826">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="4605c-827">範例中使用預留位置的標記會轉譯下列 HTML (不含實際定義于範本中的內容):</span><span class="sxs-lookup"><span data-stu-id="4605c-827">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="4605c-828">現在唯一不是使用者定義的 HTML 是*span*元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-828">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="4605c-829">(我們預計在未來的版本中, 即使不會轉譯*span*元素)。這現在可讓您完全掌控*Wizard*控制項所產生的所有內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-829">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="4605c-830">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4605c-830">ASP.NET MVC</span></span>

<span data-ttu-id="4605c-831">ASP.NET MVC 在3月2009推出為 ASP.NET 3.5 SP1 的附加元件架構。</span><span class="sxs-lookup"><span data-stu-id="4605c-831">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="4605c-832">Visual Studio 2010 包含 ASP.NET MVC 2, 其中包含新的特性和功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-832">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="4605c-833">區域支援</span><span class="sxs-lookup"><span data-stu-id="4605c-833">Areas Support</span></span>

<span data-ttu-id="4605c-834">區域可讓您將控制器和 views 群組成與其他區段相對隔離的大型應用程式區段。</span><span class="sxs-lookup"><span data-stu-id="4605c-834">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="4605c-835">每個區域都可以實作為個別的 ASP.NET MVC 專案, 然後由主應用程式參考。</span><span class="sxs-lookup"><span data-stu-id="4605c-835">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="4605c-836">這可協助您在建立大型應用程式時管理複雜度, 並讓多個小組更輕鬆地在單一應用程式上共同作業。</span><span class="sxs-lookup"><span data-stu-id="4605c-836">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="4605c-837">資料-批註屬性驗證支援</span><span class="sxs-lookup"><span data-stu-id="4605c-837">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="4605c-838">*DataAnnotations*屬性可讓您使用中繼資料屬性, 將驗證邏輯附加至模型。</span><span class="sxs-lookup"><span data-stu-id="4605c-838">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="4605c-839">*DataAnnotations*屬性是在 ASP.NET 3.5 SP1 的 ASP.NET 動態資料中引進。</span><span class="sxs-lookup"><span data-stu-id="4605c-839">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="4605c-840">這些屬性已整合到預設的模型系結器中, 並提供中繼資料驅動的方法來驗證使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="4605c-840">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="4605c-841">樣板化協助程式</span><span class="sxs-lookup"><span data-stu-id="4605c-841">Templated Helpers</span></span>

<span data-ttu-id="4605c-842">樣板化協助程式可讓您自動將編輯和顯示範本與資料類型產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4605c-842">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="4605c-843">例如, 您可以使用範本協助程式, 指定自動呈現 system.string 值的日期選擇器 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-843">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="4605c-844">這類似于 ASP.NET 動態資料中的欄位範本。</span><span class="sxs-lookup"><span data-stu-id="4605c-844">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="4605c-845">*EditorFor*和*html. DisplayFor* helper 方法具有內建的支援, 可呈現標準資料類型, 以及具有多個屬性的複雜物件。</span><span class="sxs-lookup"><span data-stu-id="4605c-845">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="4605c-846">它們也會藉由讓您將資料批註屬性 (例如*DisplayName*和*ScaffoldColumn* ) 套用至*ViewModel*物件, 以自訂轉譯。</span><span class="sxs-lookup"><span data-stu-id="4605c-846">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="4605c-847">您通常會想要進一步自訂 UI 協助程式的輸出, 並對產生的內容有完整的控制權。</span><span class="sxs-lookup"><span data-stu-id="4605c-847">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="4605c-848">*EditorFor*和*html. DisplayFor* helper 方法會使用範本化機制來支援此功能, 讓您定義可覆寫並控制所轉譯輸出的外部樣板。</span><span class="sxs-lookup"><span data-stu-id="4605c-848">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="4605c-849">範本可以針對類別個別呈現。</span><span class="sxs-lookup"><span data-stu-id="4605c-849">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="4605c-850">Dynamic Data</span><span class="sxs-lookup"><span data-stu-id="4605c-850">Dynamic Data</span></span>

<span data-ttu-id="4605c-851">動態資料是在2008年 .NET Framework 3.5 SP1 版本中引進。</span><span class="sxs-lookup"><span data-stu-id="4605c-851">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="4605c-852">這項功能提供了許多用於建立資料驅動應用程式的增強功能, 包括下列:</span><span class="sxs-lookup"><span data-stu-id="4605c-852">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="4605c-853">用來快速建立資料驅動網站的 RAD 體驗。</span><span class="sxs-lookup"><span data-stu-id="4605c-853">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="4605c-854">自動驗證是以資料模型中定義的條件約束為基礎。</span><span class="sxs-lookup"><span data-stu-id="4605c-854">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="4605c-855">使用屬於動態資料專案之一部分的欄位範本, 輕鬆變更*GridView*和*DetailsView*控制項中的欄位所產生之標記的能力。</span><span class="sxs-lookup"><span data-stu-id="4605c-855">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="4605c-856">注意如需詳細資訊, 請參閱 MSDN Library 中的[動態資料檔](https://msdn.microsoft.com/library/cc488545.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4605c-856">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="4605c-857">對於 ASP.NET 4, 動態資料已經過增強, 可讓開發人員快速建立資料驅動網站的能力。</span><span class="sxs-lookup"><span data-stu-id="4605c-857">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="4605c-858">啟用現有專案的動態資料</span><span class="sxs-lookup"><span data-stu-id="4605c-858">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="4605c-859">.NET Framework 3.5 SP1 隨附的動態資料功能引進了下列新功能:</span><span class="sxs-lookup"><span data-stu-id="4605c-859">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="4605c-860">欄位範本: 這些會為資料繫結控制項提供以資料類型為基礎的範本。</span><span class="sxs-lookup"><span data-stu-id="4605c-860">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="4605c-861">欄位範本提供更簡單的方式來自訂資料控制項的外觀, 而不是使用每個欄位的範本欄位。</span><span class="sxs-lookup"><span data-stu-id="4605c-861">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="4605c-862">驗證–動態資料可讓您在資料類別上使用屬性來指定一般案例的驗證, 例如必要欄位、範圍檢查、類型檢查、使用正則運算式的模式比對, 以及自訂驗證。</span><span class="sxs-lookup"><span data-stu-id="4605c-862">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="4605c-863">驗證是由資料控制項強制執行。</span><span class="sxs-lookup"><span data-stu-id="4605c-863">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="4605c-864">不過, 這些功能具有下列需求:</span><span class="sxs-lookup"><span data-stu-id="4605c-864">However, these features had the following requirements:</span></span>

- <span data-ttu-id="4605c-865">資料存取層必須以 Entity Framework 或 LINQ to SQL 為基礎。</span><span class="sxs-lookup"><span data-stu-id="4605c-865">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="4605c-866">這些功能唯一支援的資料來源控制項為*EntityDataSource*或*LinqDataSource*控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-866">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="4605c-867">這些功能需要使用動態資料或動態資料實體範本建立的 Web 專案, 才能擁有支援此功能所需的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-867">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="4605c-868">在 ASP.NET 4 中動態資料支援的主要目標, 是要為任何 ASP.NET 應用程式啟用動態資料的新功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-868">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="4605c-869">下列範例會顯示可利用現有頁面中動態資料功能之控制項的標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-869">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="4605c-870">在頁面的程式碼中, 必須新增下列程式碼, 才能啟用這些控制項的動態資料支援:</span><span class="sxs-lookup"><span data-stu-id="4605c-870">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="4605c-871">當*GridView*控制項處於編輯模式時, 動態資料會自動驗證輸入的資料格式是否正確。</span><span class="sxs-lookup"><span data-stu-id="4605c-871">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="4605c-872">如果不是, 則會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4605c-872">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="4605c-873">這種功能也提供其他優點, 例如能夠指定插入模式的預設值。</span><span class="sxs-lookup"><span data-stu-id="4605c-873">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="4605c-874">如果沒有動態資料, 若要為欄位執行預設值, 您必須附加至事件、尋找控制項 (使用*FindControl*), 並設定其值。</span><span class="sxs-lookup"><span data-stu-id="4605c-874">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="4605c-875">在 ASP.NET 4 中, *EnableDynamicData*呼叫支援第二個參數, 可讓您傳遞物件上任何欄位的預設值, 如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-875">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="4605c-876">宣告式 DynamicDataManager 控制語法</span><span class="sxs-lookup"><span data-stu-id="4605c-876">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="4605c-877">*DynamicDataManager*控制項已增強, 可讓您以宣告方式設定它, 如同 ASP.NET 中的大部分控制項, 而不只是在程式碼中。</span><span class="sxs-lookup"><span data-stu-id="4605c-877">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="4605c-878">*DynamicDataManager*控制項的標記看起來如下列範例所示:</span><span class="sxs-lookup"><span data-stu-id="4605c-878">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="4605c-879">此標記會針對*DynamicDataManager*控制項的*工具列*區段中所參考的 GridView1 控制項, 啟用動態資料行為。</span><span class="sxs-lookup"><span data-stu-id="4605c-879">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="4605c-880">實體範本</span><span class="sxs-lookup"><span data-stu-id="4605c-880">Entity Templates</span></span>

<span data-ttu-id="4605c-881">實體範本提供新的方式來自訂資料的配置, 而不需要您建立自訂頁面。</span><span class="sxs-lookup"><span data-stu-id="4605c-881">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="4605c-882">頁面範本會使用*FormView*控制項 (而不是在舊版動態資料的頁面範本中使用的*DetailsView*控制項) 和*DynamicEntity*控制項來呈現實體範本。</span><span class="sxs-lookup"><span data-stu-id="4605c-882">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="4605c-883">這可讓您更充分掌控動態資料所呈現的標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-883">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="4605c-884">下列清單顯示包含實體範本的新專案目錄版面配置:</span><span class="sxs-lookup"><span data-stu-id="4605c-884">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="4605c-885">`EntityTemplate`目錄包含如何顯示資料模型物件的範本。</span><span class="sxs-lookup"><span data-stu-id="4605c-885">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="4605c-886">根據預設, 會使用`Default.ascx`範本來呈現物件, 其提供的標記就像是 ASP.NET 3.5 SP1 中動態資料所使用的*DetailsView*控制項所建立的標記。</span><span class="sxs-lookup"><span data-stu-id="4605c-886">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="4605c-887">下列範例會顯示`Default.ascx`控制項的標記:</span><span class="sxs-lookup"><span data-stu-id="4605c-887">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="4605c-888">您可以編輯預設範本, 以變更整個網站的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="4605c-888">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="4605c-889">有一些範本可用於顯示、編輯和插入作業。</span><span class="sxs-lookup"><span data-stu-id="4605c-889">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="4605c-890">新範本可以根據資料物件的名稱來新增, 以便只變更一種物件類型的外觀和操作。</span><span class="sxs-lookup"><span data-stu-id="4605c-890">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="4605c-891">例如, 您可以新增下列範本:</span><span class="sxs-lookup"><span data-stu-id="4605c-891">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="4605c-892">此範本可能包含下列標記:</span><span class="sxs-lookup"><span data-stu-id="4605c-892">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="4605c-893">新的實體範本會使用新的*DynamicEntity*控制項顯示在頁面上。</span><span class="sxs-lookup"><span data-stu-id="4605c-893">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="4605c-894">在執行時間, 會將此控制項取代為實體範本的內容。</span><span class="sxs-lookup"><span data-stu-id="4605c-894">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="4605c-895">下列標記會顯示`Detail.aspx`頁面範本中使用實體範本的*FormView*控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-895">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="4605c-896">請注意標記中的*DynamicEntity*元素。</span><span class="sxs-lookup"><span data-stu-id="4605c-896">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="4605c-897">Url 和電子郵件地址的新欄位範本</span><span class="sxs-lookup"><span data-stu-id="4605c-897">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="4605c-898">ASP.NET 4 引進了兩個新的內建欄位`EmailAddress.ascx`範本`Url.ascx`: 和。</span><span class="sxs-lookup"><span data-stu-id="4605c-898">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="4605c-899">這些範本會用於標示為*EmailAddress*的欄位, 或具有*DataType*屬性的*Url* 。</span><span class="sxs-lookup"><span data-stu-id="4605c-899">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="4605c-900">針對*EmailAddress*物件, 此欄位會顯示為使用*mailto:* 通訊協定所建立的超連結。</span><span class="sxs-lookup"><span data-stu-id="4605c-900">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="4605c-901">當使用者按一下連結時, 它會開啟使用者的電子郵件客戶程式, 並建立基本架構訊息。</span><span class="sxs-lookup"><span data-stu-id="4605c-901">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="4605c-902">輸入為*Url*的物件會顯示為一般超連結。</span><span class="sxs-lookup"><span data-stu-id="4605c-902">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="4605c-903">下列範例顯示如何標記欄位。</span><span class="sxs-lookup"><span data-stu-id="4605c-903">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="4605c-904">使用 DynamicHyperLink 控制項建立連結</span><span class="sxs-lookup"><span data-stu-id="4605c-904">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="4605c-905">動態資料使用 .NET Framework 3.5 SP1 中新增的路由功能來控制使用者存取網站時所看到的 Url。</span><span class="sxs-lookup"><span data-stu-id="4605c-905">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="4605c-906">新的*DynamicHyperLink*控制項可讓您輕鬆地在動態資料網站中建立頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="4605c-906">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="4605c-907">下列範例顯示如何使用*DynamicHyperLink*控制項:</span><span class="sxs-lookup"><span data-stu-id="4605c-907">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="4605c-908">此標記會根據檔案`Products` `Global.asax`中定義的路由, 建立指向資料表清單頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="4605c-908">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="4605c-909">控制項會自動使用動態資料頁面所依據的預設資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="4605c-909">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="4605c-910">資料模型中的繼承支援</span><span class="sxs-lookup"><span data-stu-id="4605c-910">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="4605c-911">Entity Framework 和 LINQ to SQL 都支援其資料模型中的繼承。</span><span class="sxs-lookup"><span data-stu-id="4605c-911">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="4605c-912">其中一個範例可能是具有`InsurancePolicy`資料表的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4605c-912">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="4605c-913">它也可能包含`CarPolicy`與`HousePolicy` `InsurancePolicy`具有相同欄位的和資料表, 然後再新增更多欄位。</span><span class="sxs-lookup"><span data-stu-id="4605c-913">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="4605c-914">動態資料已修改為了解資料模型中的繼承物件, 以及支援繼承資料表的樣板。</span><span class="sxs-lookup"><span data-stu-id="4605c-914">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="4605c-915">支援多對多關聯性 (僅限 Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="4605c-915">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="4605c-916">Entity Framework 對資料表之間的多對多關聯性有豐富的支援, 這是藉由將關聯性公開為*實體*物件上的集合來實現。</span><span class="sxs-lookup"><span data-stu-id="4605c-916">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="4605c-917">新增`ManyToMany.ascx`新`ManyToMany_Edit.ascx`的和欄位範本, 以支援顯示和編輯與多對多關聯性相關的資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-917">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="4605c-918">控制顯示和支援列舉的新屬性</span><span class="sxs-lookup"><span data-stu-id="4605c-918">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="4605c-919">已新增*DisplayAttribute* , 可讓您進一步控制欄位的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="4605c-919">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="4605c-920">舊版動態資料中的*DisplayName*屬性可讓您變更用來當做欄位標題的名稱。</span><span class="sxs-lookup"><span data-stu-id="4605c-920">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="4605c-921">新的*DisplayAttribute*類別可讓您指定更多選項來顯示欄位, 例如欄位的顯示順序, 以及是否將欄位當做篩選準則使用。</span><span class="sxs-lookup"><span data-stu-id="4605c-921">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="4605c-922">屬性也會針對*GridView*控制項中的標籤提供獨立的控制項、 *DetailsView*控制項中使用的名稱、欄位的解說文字, 以及用於欄位的浮水印 (如果欄位接受文字輸入)。</span><span class="sxs-lookup"><span data-stu-id="4605c-922">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="4605c-923">已加入*EnumDataTypeAttribute*類別, 可讓您將欄位對應至列舉。</span><span class="sxs-lookup"><span data-stu-id="4605c-923">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="4605c-924">當您將此屬性套用至欄位時, 您可以指定列舉類型。</span><span class="sxs-lookup"><span data-stu-id="4605c-924">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="4605c-925">動態資料使用新`Enumeration.ascx`的欄位範本來建立 UI, 以顯示和編輯列舉值。</span><span class="sxs-lookup"><span data-stu-id="4605c-925">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="4605c-926">此範本會將資料庫中的值對應至列舉中的名稱。</span><span class="sxs-lookup"><span data-stu-id="4605c-926">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="4605c-927">增強的篩選支援</span><span class="sxs-lookup"><span data-stu-id="4605c-927">Enhanced Support for Filters</span></span>

<span data-ttu-id="4605c-928">動態資料1.0 隨附于布林資料行和外鍵資料行的內建篩選。</span><span class="sxs-lookup"><span data-stu-id="4605c-928">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="4605c-929">篩選器不允許您指定是否要顯示它們, 或是以顯示的順序排列。</span><span class="sxs-lookup"><span data-stu-id="4605c-929">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="4605c-930">新的*DisplayAttribute*屬性可解決這兩個問題, 方法是讓您控制是否要將資料行顯示為篩選準則, 以及顯示的順序。</span><span class="sxs-lookup"><span data-stu-id="4605c-930">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="4605c-931">另一個增強功能是已重新撰寫篩選支援,[以使用 Web form 的新](#0.2__QueryExtender "_QueryExtender")功能。</span><span class="sxs-lookup"><span data-stu-id="4605c-931">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="4605c-932">這可讓您建立篩選器, 而不需要知道篩選將會搭配使用的資料來源控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-932">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="4605c-933">除了這些擴充功能之外, 篩選也已轉換成範本控制項, 讓您可以加入新的控制項。</span><span class="sxs-lookup"><span data-stu-id="4605c-933">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="4605c-934">最後, 先前所述的*DisplayAttribute*類別可讓您覆寫預設篩選, 其方式與*UIHint*允許覆寫資料行的預設欄位範本相同。</span><span class="sxs-lookup"><span data-stu-id="4605c-934">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="4605c-935">Visual Studio 2010 Web 開發改良功能</span><span class="sxs-lookup"><span data-stu-id="4605c-935">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="4605c-936">Visual Studio 2010 中的 Web 程式開發已經過增強, 可透過 HTML 和 ASP.NET 標記程式碼片段和新的動態 IntelliSense JavaScript, 加強 CSS 相容性、提高生產力。</span><span class="sxs-lookup"><span data-stu-id="4605c-936">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="4605c-937">改良的 CSS 相容性</span><span class="sxs-lookup"><span data-stu-id="4605c-937">Improved CSS Compatibility</span></span>

<span data-ttu-id="4605c-938">Visual Studio 2010 中的 Visual Web Developer 設計工具已更新, 以改善 CSS 2.1 標準合規性。</span><span class="sxs-lookup"><span data-stu-id="4605c-938">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="4605c-939">設計工具更能保留 HTML 來源的完整性, 而且比舊版的 Visual Studio 更健全。</span><span class="sxs-lookup"><span data-stu-id="4605c-939">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="4605c-940">實際上, 我們也改進了架構, 讓未來的轉譯、版面配置和維護性增強功能更加完備。</span><span class="sxs-lookup"><span data-stu-id="4605c-940">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="4605c-941">HTML 和 JavaScript 程式碼片段</span><span class="sxs-lookup"><span data-stu-id="4605c-941">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="4605c-942">在 HTML 編輯器中, IntelliSense 會自動完成標記名稱。</span><span class="sxs-lookup"><span data-stu-id="4605c-942">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="4605c-943">IntelliSense 程式碼片段功能會自動完成整個標記等等。</span><span class="sxs-lookup"><span data-stu-id="4605c-943">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="4605c-944">在 Visual Studio 2010 中, C#與舊版 Visual Studio 支援的 JavaScript 和 Visual Basic 支援 IntelliSense 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="4605c-944">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="4605c-945">Visual Studio 2010 包含超過200的程式碼片段, 可協助您自動完成常見的 ASP.NET 和 HTML 標籤, 包括必要的屬性 (例如 runat = "server"), 以及標記特有的一般屬性 (例如*ID*、 *DataSourceID*、 *ControlToValidate*和*Text*)。</span><span class="sxs-lookup"><span data-stu-id="4605c-945">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="4605c-946">您可以下載其他程式碼片段, 也可以撰寫自己的程式碼片段, 以封裝您或您的小組用於一般工作的標記區塊。</span><span class="sxs-lookup"><span data-stu-id="4605c-946">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="4605c-947">JavaScript IntelliSense 增強功能</span><span class="sxs-lookup"><span data-stu-id="4605c-947">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="4605c-948">在 Visual 2010 中, JavaScript IntelliSense 已經過重新設計, 可提供更豐富的編輯體驗。</span><span class="sxs-lookup"><span data-stu-id="4605c-948">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="4605c-949">IntelliSense 現在會辨識由方法 (例如*registerNamespace* ) 動態產生的物件, 以及其他 JavaScript 架構所使用的類似技術。</span><span class="sxs-lookup"><span data-stu-id="4605c-949">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="4605c-950">效能已經過改良, 可分析大型的腳本程式庫, 並在幾乎不需要處理延遲的情況之下顯示 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="4605c-950">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="4605c-951">相容性已大幅增加, 可支援幾乎所有協力廠商程式庫, 並支援各種編碼樣式。</span><span class="sxs-lookup"><span data-stu-id="4605c-951">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="4605c-952">檔批註現在會在您輸入時進行剖析, 而且 IntelliSense 會立即運用。</span><span class="sxs-lookup"><span data-stu-id="4605c-952">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="4605c-953">使用 Visual Studio 2010 的 Web 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="4605c-953">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="4605c-954">當 ASP.NET 開發人員部署 Web 應用程式時, 通常會發現它們遇到下列問題:</span><span class="sxs-lookup"><span data-stu-id="4605c-954">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="4605c-955">部署至共用的主控網站需要諸如 FTP 等技術, 這可能會很慢。</span><span class="sxs-lookup"><span data-stu-id="4605c-955">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="4605c-956">此外, 您還必須手動執行工作, 例如執行 SQL 腳本來設定資料庫, 而且您必須變更 IIS 設定, 例如將虛擬目錄資料夾設為應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-956">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="4605c-957">在企業環境中, 除了部署 Web 應用程式檔以外, 系統管理員經常必須修改 ASP.NET 設定檔和 IIS 設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-957">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="4605c-958">資料庫管理員必須執行一系列的 SQL 腳本, 才能讓應用程式資料庫運作。</span><span class="sxs-lookup"><span data-stu-id="4605c-958">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="4605c-959">這類安裝非常耗費人力, 通常需要數小時才能完成, 而且必須仔細記載。</span><span class="sxs-lookup"><span data-stu-id="4605c-959">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="4605c-960">Visual Studio 2010 包含解決這些問題的技術, 並可讓您順暢地部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4605c-960">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="4605c-961">其中一項技術是 IIS Web Deployment Tool (Msdeploy.exe)。</span><span class="sxs-lookup"><span data-stu-id="4605c-961">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="4605c-962">Visual Studio 2010 中的 Web 部署功能包含下列主要區域:</span><span class="sxs-lookup"><span data-stu-id="4605c-962">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="4605c-963">網頁封裝</span><span class="sxs-lookup"><span data-stu-id="4605c-963">Web packaging</span></span>
- <span data-ttu-id="4605c-964">Web.config 轉換</span><span class="sxs-lookup"><span data-stu-id="4605c-964">Web.config transformation</span></span>
- <span data-ttu-id="4605c-965">資料庫部署</span><span class="sxs-lookup"><span data-stu-id="4605c-965">Database deployment</span></span>
- <span data-ttu-id="4605c-966">針對 Web 應用程式按一下 [發佈]</span><span class="sxs-lookup"><span data-stu-id="4605c-966">One-click publish for Web applications</span></span>

<span data-ttu-id="4605c-967">下列各節提供有關這些功能的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-967">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="4605c-968">網頁封裝</span><span class="sxs-lookup"><span data-stu-id="4605c-968">Web Packaging</span></span>

<span data-ttu-id="4605c-969">Visual Studio 2010 使用 Msdeploy.exe 工具來為您的應用程式建立壓縮 (.zip) 檔案, 這稱為「 *Web 封裝*」。</span><span class="sxs-lookup"><span data-stu-id="4605c-969">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="4605c-970">封裝檔案包含您應用程式的相關中繼資料, 以及下列內容:</span><span class="sxs-lookup"><span data-stu-id="4605c-970">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="4605c-971">IIS 設定, 其中包括應用程式集區設定、錯誤頁面設定等等。</span><span class="sxs-lookup"><span data-stu-id="4605c-971">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="4605c-972">實際的 Web 內容, 包括網頁、使用者控制項、靜態內容 (影像和 HTML 檔案) 等等。</span><span class="sxs-lookup"><span data-stu-id="4605c-972">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="4605c-973">SQL Server 資料庫架構和資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-973">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="4605c-974">安全性憑證、要安裝在 GAC 中的元件、登錄設定等。</span><span class="sxs-lookup"><span data-stu-id="4605c-974">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="4605c-975">Web 封裝可以複製到任何伺服器, 然後使用 IIS 管理員以手動方式安裝。</span><span class="sxs-lookup"><span data-stu-id="4605c-975">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="4605c-976">或者, 若要進行自動化部署, 可以使用命令列命令或使用部署 Api 來安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="4605c-976">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="4605c-977">Visual Studio 2010 提供內建的 MSBuild 工作和目標, 以建立 Web 封裝。</span><span class="sxs-lookup"><span data-stu-id="4605c-977">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="4605c-978">如需詳細資訊, 請參閱 MSDN 網站上的[ASP.NET Web 應用程式專案部署總覽](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx), 以及[10 + 20 為什麼您應該](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)在 Vishal Joshi 的 Blog 上建立 web 套件的原因。</span><span class="sxs-lookup"><span data-stu-id="4605c-978">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="4605c-979">Web.config 轉換</span><span class="sxs-lookup"><span data-stu-id="4605c-979">Web.config Transformation</span></span>

<span data-ttu-id="4605c-980">針對 Web 應用程式部署, Visual Studio 2010 引進了[XML 檔轉換 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), 這是一項功能, 可`Web.config`讓您將檔案從開發設定轉換成生產環境設定。</span><span class="sxs-lookup"><span data-stu-id="4605c-980">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="4605c-981">轉換設定是在名為`web.debug.config`、 `web.release.config`等的轉換檔案中指定。</span><span class="sxs-lookup"><span data-stu-id="4605c-981">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="4605c-982">(這些檔案的名稱符合 MSBuild 設定)。轉換檔案只包含您需要對已部署`Web.config`的檔案進行的變更。</span><span class="sxs-lookup"><span data-stu-id="4605c-982">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="4605c-983">您可以使用簡單的語法來指定變更。</span><span class="sxs-lookup"><span data-stu-id="4605c-983">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="4605c-984">下列範例顯示可能針對部署發行設定`web.release.config`而產生的部分檔案。</span><span class="sxs-lookup"><span data-stu-id="4605c-984">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="4605c-985">範例中的 Replace 關鍵字會指定在部署期間,會將檔案中`Web.config`的 connectionString 節點取代為範例中所列的值。</span><span class="sxs-lookup"><span data-stu-id="4605c-985">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="4605c-986">如需詳細資訊, 請參閱 MSDN <a id="0.2_a"></a>網站上的 web[應用程式專案部署的 web.config 轉換語法](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)和[web 部署:Vishal Joshi 的 blog](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)上的 web.config 轉換。</span><span class="sxs-lookup"><span data-stu-id="4605c-986">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="4605c-987">資料庫部署</span><span class="sxs-lookup"><span data-stu-id="4605c-987">Database Deployment</span></span>

<span data-ttu-id="4605c-988">Visual Studio 2010 部署套件可以包含 SQL Server 資料庫的相依性。</span><span class="sxs-lookup"><span data-stu-id="4605c-988">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="4605c-989">在封裝定義中, 您會提供源資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4605c-989">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="4605c-990">當您建立 Web 封裝時, Visual Studio 2010 會為資料庫架構建立 SQL 腳本, 並選擇性地為該資料建立, 然後將它們加入至封裝。</span><span class="sxs-lookup"><span data-stu-id="4605c-990">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="4605c-991">您也可以提供自訂的 SQL 腳本, 並指定它們應該在伺服器上執行的順序。</span><span class="sxs-lookup"><span data-stu-id="4605c-991">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="4605c-992">在部署階段, 您會提供適用于目標伺服器的連接字串。接著, 部署程式會使用此連接字串來執行腳本, 以建立資料庫架構並加入資料。</span><span class="sxs-lookup"><span data-stu-id="4605c-992">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="4605c-993">此外, 只要使用單鍵發行, 您就可以設定部署, 在應用程式發行至遠端共用主控網站時直接發佈資料庫。</span><span class="sxs-lookup"><span data-stu-id="4605c-993">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="4605c-994">如需詳細資訊，請參閱[如何：在 MSDN 網站上使用 Web 應用程式](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)專案部署資料庫, 並在 Vishal Joshi 的 blog 上[使用 VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)來部署資料庫。</span><span class="sxs-lookup"><span data-stu-id="4605c-994">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="4605c-995">針對 Web 應用程式按一下 [發佈]</span><span class="sxs-lookup"><span data-stu-id="4605c-995">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="4605c-996">Visual Studio 2010 也可讓您使用 IIS 遠端系統管理服務, 將 Web 應用程式發行至遠端伺服器。</span><span class="sxs-lookup"><span data-stu-id="4605c-996">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="4605c-997">您可以為您的主控帳戶或測試伺服器或預備伺服器建立發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="4605c-997">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="4605c-998">每個設定檔都可以安全地儲存適當的認證。</span><span class="sxs-lookup"><span data-stu-id="4605c-998">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="4605c-999">您接著可以使用 Web 單鍵 [發行] 工具列, 只要按一下就能部署到任何目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="4605c-999">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="4605c-1000">使用 Visual Studio 2010, 您也可以使用 MSBuild 命令列來發行。</span><span class="sxs-lookup"><span data-stu-id="4605c-1000">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="4605c-1001">這可讓您將 team build 環境設定為包含連續整合模型中的發行。</span><span class="sxs-lookup"><span data-stu-id="4605c-1001">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="4605c-1002">如需詳細資訊，請參閱[如何：在 MSDN 網站上使用單鍵發佈和 Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)部署 web 應用程式專案, 並在 Vishal Joshi 的 blog 上, 按一下 [[使用 VS 2010 發佈](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)]。</span><span class="sxs-lookup"><span data-stu-id="4605c-1002">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="4605c-1003">若要在 Visual Studio 2010 中觀看有關 Web 應用程式部署的影片簡報, 請參閱 VS 2010, 以取得 Vishal Joshi 的網路上[的 Web 開發人員預覽版](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html)。</span><span class="sxs-lookup"><span data-stu-id="4605c-1003">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="4605c-1004">資源</span><span class="sxs-lookup"><span data-stu-id="4605c-1004">Resources</span></span>

<span data-ttu-id="4605c-1005">下列網站提供 ASP.NET 4 和 Visual Studio 2010 的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4605c-1005">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="4605c-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — MSDN 網站上的 ASP.NET 4 官方檔。</span><span class="sxs-lookup"><span data-stu-id="4605c-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="4605c-1007">[https://www.asp.net/](https://www.asp.net/)— ASP.NET 小組自己的網站。</span><span class="sxs-lookup"><span data-stu-id="4605c-1007">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="4605c-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx)和[ASP.NET 動態資料內容地圖](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)-ASP.NET 小組網站上的線上資源, 以及 ASP.NET 動態資料的官方檔。</span><span class="sxs-lookup"><span data-stu-id="4605c-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="4605c-1009">[https://www.asp.net/ajax/](../../ajax/index.md)-用來 ASP.NET Ajax 開發的主要 Web 資源。</span><span class="sxs-lookup"><span data-stu-id="4605c-1009">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="4605c-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/): Visual Web Developer 小組的 blog, 其中包含 Visual Studio 2010 中功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4605c-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="4605c-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — ASP.NET 的預覽版本主要 Web 資源。</span><span class="sxs-lookup"><span data-stu-id="4605c-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="4605c-1012">免責聲明</span><span class="sxs-lookup"><span data-stu-id="4605c-1012">Disclaimer</span></span>

<span data-ttu-id="4605c-1013">這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。</span><span class="sxs-lookup"><span data-stu-id="4605c-1013">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="4605c-1014">本文件中的資訊表示直到文件發行日前 Microsoft Corporation 針對問題的看法。</span><span class="sxs-lookup"><span data-stu-id="4605c-1014">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="4605c-1015">Microsoft 必須因應不斷變化的市場狀況，因此本文件不代表 Microsoft 的保證，且 Microsoft 不保證這些資訊在文件發行後的正確性。</span><span class="sxs-lookup"><span data-stu-id="4605c-1015">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="4605c-1016">本技術白皮書僅供參考。</span><span class="sxs-lookup"><span data-stu-id="4605c-1016">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="4605c-1017">MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。</span><span class="sxs-lookup"><span data-stu-id="4605c-1017">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="4605c-1018">承諾遵守所有適用的著作權法是使用者的責任。</span><span class="sxs-lookup"><span data-stu-id="4605c-1018">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="4605c-1019">著作權法沒有針對某種權利加以限制，但在未獲得 Microsoft Corporation 書面同意的情況下，本文件的任何部分不得複製、以檢索系統存放或擷取、以任何形式或方法傳送 (電子、機械、影像複製、錄音或其他任何方法)、或基於任何其他不良意圖。</span><span class="sxs-lookup"><span data-stu-id="4605c-1019">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="4605c-1020">本文件所提及的主要事務，Microsoft 得擁有專利、專利應用程式、商標、著作權或其他智慧財產權。</span><span class="sxs-lookup"><span data-stu-id="4605c-1020">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="4605c-1021">除了 Microsoft 於授權合約書中書面提供的之外，本文件所述內容並未賦予您這些專利、商標、著作權、或其他智慧財產的任何授權或使用權利。</span><span class="sxs-lookup"><span data-stu-id="4605c-1021">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="4605c-1022">除非另有說明, 否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、商標、人員、地點及事件均屬虛構, 而且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件相關。位址、標誌、人員、地點或事件的預定或應加以推斷。</span><span class="sxs-lookup"><span data-stu-id="4605c-1022">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="4605c-1023">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="4605c-1023">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="4605c-1024">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="4605c-1024">All rights reserved.</span></span>

<span data-ttu-id="4605c-1025">Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。</span><span class="sxs-lookup"><span data-stu-id="4605c-1025">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="4605c-1026">本文件中所提實際公司和產品，可能為各所有人所有之商標。</span><span class="sxs-lookup"><span data-stu-id="4605c-1026">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
