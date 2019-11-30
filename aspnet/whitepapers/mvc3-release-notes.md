---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 504202068f5db4f8614bba02e8066ffecfd15b48
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619244"
---
# <a name="aspnet-mvc-3"></a><span data-ttu-id="aba05-102">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="aba05-102">ASP.NET MVC 3</span></span>

- [<span data-ttu-id="aba05-103">概觀</span><span class="sxs-lookup"><span data-stu-id="aba05-103">Overview</span></span>](#overview)
- [<span data-ttu-id="aba05-104">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="aba05-104">Installation Notes</span></span>](#installation-notes)
- [<span data-ttu-id="aba05-105">軟體需求</span><span class="sxs-lookup"><span data-stu-id="aba05-105">Software Requirements</span></span>](#software-requirements)
- [<span data-ttu-id="aba05-106">文件 (英文)</span><span class="sxs-lookup"><span data-stu-id="aba05-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="aba05-107">支援</span><span class="sxs-lookup"><span data-stu-id="aba05-107">Support</span></span>](#support)
- [<span data-ttu-id="aba05-108">將 ASP.NET MVC 2 專案升級至 ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="aba05-108">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>](#upgrading)
- [<span data-ttu-id="aba05-109">ASP.NET MVC 3 工具更新（2011年4月12日）</span><span class="sxs-lookup"><span data-stu-id="aba05-109">ASP.NET MVC 3 Tools Update (April 12, 2011)</span></span>](#tu-changes)

    - <span data-ttu-id="aba05-110">[[新增控制器] 對話方塊現在可以使用 views 和資料存取程式碼 scaffold 控制器](#tu-AddControllerDialog)</span><span class="sxs-lookup"><span data-stu-id="aba05-110">["Add Controller" dialog box can now scaffold controllers with views and data access code](#tu-AddControllerDialog)</span></span>
    - <span data-ttu-id="aba05-111">[[ASP.NET MVC 3 新增專案] 對話方塊的改善](#tu-ImprovementsNewDialogBox)</span><span class="sxs-lookup"><span data-stu-id="aba05-111">[Improvements to the "ASP.NET MVC 3 New Project" Dialog Box](#tu-ImprovementsNewDialogBox)</span></span>
    - [<span data-ttu-id="aba05-112">專案範本現在包含 Modernizr 1。7</span><span class="sxs-lookup"><span data-stu-id="aba05-112">Project templates now include Modernizr 1.7</span></span>](#tu-Modernizr)
    - [<span data-ttu-id="aba05-113">專案範本包含 jQuery、jQuery UI 和 jQuery 驗證的更新版本</span><span class="sxs-lookup"><span data-stu-id="aba05-113">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>](#tu-UpdatedJQuery)
    - [<span data-ttu-id="aba05-114">專案範本現在包含 ADO.NET Entity Framework 4.1，做為預先安裝的 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="aba05-114">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>](#tu-EF)
    - [<span data-ttu-id="aba05-115">專案範本以預先安裝的 NuGet 套件形式包含 JavaScript 程式庫</span><span class="sxs-lookup"><span data-stu-id="aba05-115">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>](#tu-JavaScriptLibsNuget)
    - [<span data-ttu-id="aba05-116">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-116">Known Issues</span></span>](#tu-KI)
- [<span data-ttu-id="aba05-117">ASP.NET MVC 3 RTM （2011年1月13日）</span><span class="sxs-lookup"><span data-stu-id="aba05-117">ASP.NET MVC 3 RTM (January 13, 2011)</span></span>](#MVC3RTM)

    - [<span data-ttu-id="aba05-118">變更：將 jQuery UI 的版本更新為1.8。7</span><span class="sxs-lookup"><span data-stu-id="aba05-118">Change: Updated the version of jQuery UI to 1.8.7</span></span>](#RTM-1)
    - [<span data-ttu-id="aba05-119">變更：將預設 ModelMetadataProvider 變更回 DataAnnotationsModelMetadataProvider</span><span class="sxs-lookup"><span data-stu-id="aba05-119">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>](#RTM-2)
    - [<span data-ttu-id="aba05-120">已修正：貼上包含空白字元的 Razor 運算式部分，會導致它被反轉</span><span class="sxs-lookup"><span data-stu-id="aba05-120">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>](#RTM-3)
    - [<span data-ttu-id="aba05-121">已修正：重新命名在編輯器中開啟的 Razor 檔案時，會停用語法顏色標示和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="aba05-121">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>](#RTM-4)
    - [<span data-ttu-id="aba05-122">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-122">Known Issues</span></span>](#RTM-KI)
    - [<span data-ttu-id="aba05-123">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-123">Breaking Changes</span></span>](#RTM-BC)
- [<span data-ttu-id="aba05-124">ASP.NET MVC 3 候選版2（2010年12月10日）</span><span class="sxs-lookup"><span data-stu-id="aba05-124">ASP.NET MVC 3 Release Candidate 2 (December 10, 2010)</span></span>](#_Toc2)

    - [<span data-ttu-id="aba05-125">專案範本已變更為包含 jQuery 1.4.4、jQuery 驗證1.7 和 jQuery UI 1.8.6 y UI 1.8。6</span><span class="sxs-lookup"><span data-stu-id="aba05-125">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6y UI 1.8.6</span></span>](#_Toc2_1)
    - [<span data-ttu-id="aba05-126">已新增 "AdditionalMetadataAttribute" 類別</span><span class="sxs-lookup"><span data-stu-id="aba05-126">Added "AdditionalMetadataAttribute" Class</span></span>](#_Toc2_2)
    - [<span data-ttu-id="aba05-127">改良的視圖樣板</span><span class="sxs-lookup"><span data-stu-id="aba05-127">Improved View Scaffolding</span></span>](#_Toc2_3)
    - [<span data-ttu-id="aba05-128">已新增 Html。 Raw 方法</span><span class="sxs-lookup"><span data-stu-id="aba05-128">Added Html.Raw Method</span></span>](#_Toc2_3)
    - [<span data-ttu-id="aba05-129">將 "Controller. ViewModel" 屬性和 "View" 屬性重新命名為 "ViewBag"</span><span class="sxs-lookup"><span data-stu-id="aba05-129">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>](#_Toc2_4)
    - [<span data-ttu-id="aba05-130">將 "ControllerSessionStateAttribute" 類別重新命名為 "SessionStateAttribute"</span><span class="sxs-lookup"><span data-stu-id="aba05-130">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>](#_Toc2_5)
    - [<span data-ttu-id="aba05-131">將 RemoteAttribute "Fields" 屬性重新命名為 "AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="aba05-131">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>](#_Toc2_6)
    - [<span data-ttu-id="aba05-132">已將 "SkipRequestValidationAttribute" 重新命名為 "AllowHtmlAttribute"</span><span class="sxs-lookup"><span data-stu-id="aba05-132">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>](#_Toc2_7)
    - [<span data-ttu-id="aba05-133">已將 "ValidationMessage" 方法變更為顯示第一個有用的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="aba05-133">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>](#_Toc2_8)
    - [<span data-ttu-id="aba05-134">已修正 @model 宣告，不要在檔中加入空白字元</span><span class="sxs-lookup"><span data-stu-id="aba05-134">Fixed @model Declaration to not Add Whitespace to the Document</span></span>](#_Toc2_9)
    - [<span data-ttu-id="aba05-135">已新增 "Microsoft.extensions.configuration fileextensions" 屬性來查看引擎，以支援引擎特定的檔案名</span><span class="sxs-lookup"><span data-stu-id="aba05-135">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>](#_Toc2_10)
    - [<span data-ttu-id="aba05-136">已修正 "LabelFor" Helper 以發出 "For" 屬性的正確值</span><span class="sxs-lookup"><span data-stu-id="aba05-136">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>](#_Toc2_11)
    - [<span data-ttu-id="aba05-137">已修正 "RenderAction" 方法，以在模型系結期間提供明確值的優先順序</span><span class="sxs-lookup"><span data-stu-id="aba05-137">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>](#_Toc2_12)
    - [<span data-ttu-id="aba05-138">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-138">Breaking Changes</span></span>](#_Toc2_BC)
    - [<span data-ttu-id="aba05-139">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-139">Known Issues</span></span>](#_Toc2_KI)
- [<span data-ttu-id="aba05-140">ASP.NET MVC 3 發行候選版本（2010年11月9日）</span><span class="sxs-lookup"><span data-stu-id="aba05-140">ASP.NET MVC 3 Release Candidate (Nov 9, 2010)</span></span>](#TOC_ASP_NET_3_RC)

    - [<span data-ttu-id="aba05-141">ASP.NET MVC 3 RC 中的新功能</span><span class="sxs-lookup"><span data-stu-id="aba05-141">New Features in ASP.NET MVC 3 RC</span></span>](#_Toc276711785)
    - [<span data-ttu-id="aba05-142">NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="aba05-142">NuGet Package Manager</span></span>](#_Toc276711786)
    - <span data-ttu-id="aba05-143">[改良的 [新增專案] 對話方塊](#_Toc276711787)</span><span class="sxs-lookup"><span data-stu-id="aba05-143">[Improved "New Project" Dialog Box](#_Toc276711787)</span></span>
    - [<span data-ttu-id="aba05-144">無會話控制器</span><span class="sxs-lookup"><span data-stu-id="aba05-144">Sessionless Controllers</span></span>](#_Toc276711788)
    - [<span data-ttu-id="aba05-145">新的驗證屬性</span><span class="sxs-lookup"><span data-stu-id="aba05-145">New Validation Attributes</span></span>](#_Toc276711789)
    - [<span data-ttu-id="aba05-146">"LabelFor" 和 "LabelForModel" 方法的新多載</span><span class="sxs-lookup"><span data-stu-id="aba05-146">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>](#_Toc276711790)
    - [<span data-ttu-id="aba05-147">子動作輸出快取</span><span class="sxs-lookup"><span data-stu-id="aba05-147">Child Action Output Caching</span></span>](#_Toc276711791)
    - <span data-ttu-id="aba05-148">[[加入視圖] 對話方塊的改善](#_Toc276711792)</span><span class="sxs-lookup"><span data-stu-id="aba05-148">["Add View" Dialog Box Improvements](#_Toc276711792)</span></span>
    - [<span data-ttu-id="aba05-149">細微要求驗證</span><span class="sxs-lookup"><span data-stu-id="aba05-149">Granular Request Validation</span></span>](#_Toc276711793)
    - [<span data-ttu-id="aba05-150">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-150">Breaking Changes</span></span>](#_Toc276711794)
    - [<span data-ttu-id="aba05-151">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-151">Known Issues</span></span>](#_Toc276711795)
- [<span data-ttu-id="aba05-152">ASP.MVC 3 Beta 附注（2010年10月6日）</span><span class="sxs-lookup"><span data-stu-id="aba05-152">ASP.MVC 3 Beta Notes (Oct 6, 2010)</span></span>](#TOC_ASP_NET_3_Beta)

    - [<span data-ttu-id="aba05-153">ASP.NET MVC 3 Beta 的新功能</span><span class="sxs-lookup"><span data-stu-id="aba05-153">New Features in ASP.NET MVC 3 Beta</span></span>](#0.1__Toc274034215)
    - [<span data-ttu-id="aba05-154">NuPack 套件管理員</span><span class="sxs-lookup"><span data-stu-id="aba05-154">NuPack Package Manager</span></span>](#0.1__Toc274034216)
    - <span data-ttu-id="aba05-155">[改良的 [新增專案] 對話方塊](#0.1__Toc274034217)</span><span class="sxs-lookup"><span data-stu-id="aba05-155">[Improved New Project Dialog Box](#0.1__Toc274034217)</span></span>
    - [<span data-ttu-id="aba05-156">在 Razor Views 中指定強型別模型的簡化方式</span><span class="sxs-lookup"><span data-stu-id="aba05-156">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>](#0.1__Toc274034218)
    - [<span data-ttu-id="aba05-157">支援新的 ASP.NET Web Pages Helper 方法</span><span class="sxs-lookup"><span data-stu-id="aba05-157">Support for New ASP.NET Web Pages Helper Methods</span></span>](#0.1__Toc274034219)
    - [<span data-ttu-id="aba05-158">其他相依性插入支援</span><span class="sxs-lookup"><span data-stu-id="aba05-158">Additional Dependency Injection Support</span></span>](#0.1__Toc274034220)
    - [<span data-ttu-id="aba05-159">不顯眼的 jQuery 型 Ajax 的新支援</span><span class="sxs-lookup"><span data-stu-id="aba05-159">New Support for Unobtrusive jQuery-Based Ajax</span></span>](#0.1__Toc274034221)
    - [<span data-ttu-id="aba05-160">不顯眼 jQuery 驗證的新支援</span><span class="sxs-lookup"><span data-stu-id="aba05-160">New Support for Unobtrusive jQuery Validation</span></span>](#0.1__Toc274034222)
    - [<span data-ttu-id="aba05-161">適用于用戶端驗證和不顯眼 JavaScript 的新全應用程式旗標</span><span class="sxs-lookup"><span data-stu-id="aba05-161">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>](#0.1__Toc274034223)
    - [<span data-ttu-id="aba05-162">新支援在 Views 執行之前執行的程式碼</span><span class="sxs-lookup"><span data-stu-id="aba05-162">New Support for Code that Runs Before Views Run</span></span>](#0.1__Toc274034224)
    - [<span data-ttu-id="aba05-163">VBHTML Razor 語法的新支援</span><span class="sxs-lookup"><span data-stu-id="aba05-163">New Support for the VBHTML Razor Syntax</span></span>](#0.1__Toc274034225)
    - [<span data-ttu-id="aba05-164">更精細地控制 Validateinputattribute 套用</span><span class="sxs-lookup"><span data-stu-id="aba05-164">More Granular Control over ValidateInputAttribute</span></span>](#0.1__Toc274034226)
    - [<span data-ttu-id="aba05-165">協助程式將底線轉換為使用匿名物件指定之 HTML 屬性名稱的連字號</span><span class="sxs-lookup"><span data-stu-id="aba05-165">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>](#0.1__Toc274034227)
    - [<span data-ttu-id="aba05-166">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="aba05-166">Bug Fixes</span></span>](#0.1__Toc274034228)
    - [<span data-ttu-id="aba05-167">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-167">Breaking Changes</span></span>](#0.1__Toc274034229)
    - [<span data-ttu-id="aba05-168">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-168">Known Issues</span></span>](#0.1__Toc274034230)
- [<span data-ttu-id="aba05-169">免責聲明</span><span class="sxs-lookup"><span data-stu-id="aba05-169">Disclaimer</span></span>](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a><span data-ttu-id="aba05-170">概觀</span><span class="sxs-lookup"><span data-stu-id="aba05-170">Overview</span></span>

<span data-ttu-id="aba05-171">本檔說明適用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-171">This document describes the release of ASP.NET MVC 3 RTM for Visual Studio 2010.</span></span> <span data-ttu-id="aba05-172">ASP.NET MVC 是一種架構，可用於開發使用模型視圖控制器（MVC）模式的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aba05-172">ASP.NET MVC is a framework for developing Web applications that uses the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="aba05-173">ASP.NET MVC 3 安裝套裝程式含下列元件：</span><span class="sxs-lookup"><span data-stu-id="aba05-173">The ASP.NET MVC 3 installer includes the following components:</span></span>

- <span data-ttu-id="aba05-174">ASP.NET MVC 3 執行時間元件</span><span class="sxs-lookup"><span data-stu-id="aba05-174">ASP.NET MVC 3 runtime components</span></span>
- <span data-ttu-id="aba05-175">ASP.NET MVC 3 Visual Studio 2010 工具</span><span class="sxs-lookup"><span data-stu-id="aba05-175">ASP.NET MVC 3 Visual Studio 2010 tools</span></span>
- <span data-ttu-id="aba05-176">ASP.NET Web Pages 執行時間元件</span><span class="sxs-lookup"><span data-stu-id="aba05-176">ASP.NET Web Pages run-time components</span></span>
- <span data-ttu-id="aba05-177">ASP.NET Web Pages Visual Studio 2010 工具</span><span class="sxs-lookup"><span data-stu-id="aba05-177">ASP.NET Web Pages Visual Studio 2010 tools</span></span>
- <span data-ttu-id="aba05-178">適用于 .NET 的 Microsoft 套件管理員（NuGet）</span><span class="sxs-lookup"><span data-stu-id="aba05-178">Microsoft Package Manager for .NET (NuGet)</span></span>
- <span data-ttu-id="aba05-179">Visual Studio 2010 的更新，可支援 Razor 語法。</span><span class="sxs-lookup"><span data-stu-id="aba05-179">An update for Visual Studio 2010 that enables support for Razor syntax.</span></span> <span data-ttu-id="aba05-180">（如需詳細資訊，請參閱知識庫文章2483190。）</span><span class="sxs-lookup"><span data-stu-id="aba05-180">(For details, see KnowledgeBase article 2483190.)</span></span>

<span data-ttu-id="aba05-181">您可在 ASP.NET 網站上找到 ASP.NET MVC 3 每個預先發行版本之版本資訊的完整集合，其 URL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-181">The full set of release notes for each pre-release version of ASP.NET MVC 3 can be found on the ASP.NET website at the following URL:</span></span>

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a><span data-ttu-id="aba05-182">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="aba05-182">Installation Notes</span></span>

<span data-ttu-id="aba05-183">若要使用 Web Platform Installer （Web PI）安裝 ASP.NET MVC 3 RTM，請造訪下列頁面：</span><span class="sxs-lookup"><span data-stu-id="aba05-183">To install ASP.NET MVC 3 RTM using the Web Platform Installer (Web PI), visit the following page:</span></span>

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

<span data-ttu-id="aba05-184">或者，您可以從下列頁面下載適用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 安裝程式：</span><span class="sxs-lookup"><span data-stu-id="aba05-184">Alternatively, you can download the installer for ASP.NET MVC 3 RTM for Visual Studio 2010 from the following page:</span></span>

https://go.microsoft.com/fwlink/?LinkID=208140

<span data-ttu-id="aba05-185">ASP.NET MVC 3 可以安裝，而且可以與 ASP.NET MVC 2 並存執行。</span><span class="sxs-lookup"><span data-stu-id="aba05-185">ASP.NET MVC 3 can be installed and can run side-by-side with ASP.NET MVC 2.</span></span>

<a id="software-requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="aba05-186">軟體需求</span><span class="sxs-lookup"><span data-stu-id="aba05-186">Software Requirements</span></span>

<span data-ttu-id="aba05-187">ASP.NET MVC 3 執行時間元件需要下列軟體：</span><span class="sxs-lookup"><span data-stu-id="aba05-187">The ASP.NET MVC 3 run-time components require the following software:</span></span>

- <span data-ttu-id="aba05-188">.NET Framework 第4版。</span><span class="sxs-lookup"><span data-stu-id="aba05-188">.NET Framework version 4.</span></span> 

    <span data-ttu-id="aba05-189">ASP.NET MVC 3 Visual Studio 2010 工具需要下列軟體：</span><span class="sxs-lookup"><span data-stu-id="aba05-189">ASP.NET MVC 3 Visual Studio 2010 tools require the following software:</span></span>
- <span data-ttu-id="aba05-190">Visual Studio 2010 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="aba05-190">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="aba05-191">Documentation</span><span class="sxs-lookup"><span data-stu-id="aba05-191">Documentation</span></span>

<span data-ttu-id="aba05-192">您可以在 MSDN 網站上取得 ASP.NET MVC 的檔，網址如下：</span><span class="sxs-lookup"><span data-stu-id="aba05-192">Documentation for ASP.NET MVC is available on the MSDN Web site at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

<span data-ttu-id="aba05-193">如需有關 ASP.NET MVC 的教學課程和其他資訊，請在 ASP.NET 網站的 MVC 頁面上找到，網址如下：</span><span class="sxs-lookup"><span data-stu-id="aba05-193">Tutorials and other information about ASP.NET MVC are available on the MVC page of the ASP.NET Web site at the following URL:</span></span>

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a><span data-ttu-id="aba05-194">支援</span><span class="sxs-lookup"><span data-stu-id="aba05-194">Support</span></span>

<span data-ttu-id="aba05-195">這是有完整支援的版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-195">This is a fully supported release.</span></span> <span data-ttu-id="aba05-196">您可以在[Microsoft 支援服務網站](https://support.microsoft.com/)中找到取得技術支援的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aba05-196">Information about getting technical support can be found at the [Microsoft Support website](https://support.microsoft.com/).</span></span>

<span data-ttu-id="aba05-197">您也可隨時在 ASP.NET MVC 論壇張貼對此版本的問題，ASP.NET 社群成員可經常在此提供非正式的支援：</span><span class="sxs-lookup"><span data-stu-id="aba05-197">Also feel free to post questions about this release to the ASP.NET MVC forum, where members of the ASP.NET community are frequently able to provide informal support:</span></span>

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a><span data-ttu-id="aba05-198">將 ASP.NET MVC 2 專案升級至 ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="aba05-198">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="aba05-199">ASP.NET MVC 3 可以與 ASP.NET MVC 2 並存安裝在同一部電腦上，讓您有彈性選擇何時將 ASP.NET MVC 2 應用程式升級為 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="aba05-199">ASP.NET MVC 3 can be installed side by side with ASP.NET MVC 2 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 2 application to ASP.NET MVC 3.</span></span>

<span data-ttu-id="aba05-200">若要將現有的 ASP.NET MVC 2 應用程式手動升級至第3版，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="aba05-200">To manually upgrade an existing ASP.NET MVC 2 application to version 3, do the following:</span></span>

1. <span data-ttu-id="aba05-201">在您的電腦上建立新的空白 ASP.NET MVC 3 專案。</span><span class="sxs-lookup"><span data-stu-id="aba05-201">Create a new empty ASP.NET MVC 3 project on your computer.</span></span> <span data-ttu-id="aba05-202">這個專案將會包含升級所需的一些檔案。</span><span class="sxs-lookup"><span data-stu-id="aba05-202">This project will contain some files that are required for the upgrade.</span></span>
2. <span data-ttu-id="aba05-203">將下列檔案從 ASP.NET MVC 3 專案複製到 ASP.NET MVC 2 專案的對應位置。</span><span class="sxs-lookup"><span data-stu-id="aba05-203">Copy the following files from the ASP.NET MVC 3 project into the corresponding location of your ASP.NET MVC 2 project.</span></span> <span data-ttu-id="aba05-204">您必須更新所有 jQuery 程式庫的參考，以說明新檔案名稱 (jQuery-1.5.1.js)：</span><span class="sxs-lookup"><span data-stu-id="aba05-204">You'll need to update any references to the jQuery library to account for the new filename ( jQuery-1.5.1.js):</span></span> 

    - <span data-ttu-id="aba05-205">/Views/Web.config</span><span class="sxs-lookup"><span data-stu-id="aba05-205">/Views/Web.config</span></span>
    - <span data-ttu-id="aba05-206">/packages.config</span><span class="sxs-lookup"><span data-stu-id="aba05-206">/packages.config</span></span>
    - <span data-ttu-id="aba05-207">/scripts/\*.js</span><span class="sxs-lookup"><span data-stu-id="aba05-207">/scripts/\*.js</span></span>
    - <span data-ttu-id="aba05-208">/Content/themes/\*。\*</span><span class="sxs-lookup"><span data-stu-id="aba05-208">/Content/themes/\*.\*</span></span>
3. <span data-ttu-id="aba05-209">將空白 ASP.NET MVC 3 專案方案根目錄中的 [*套件*] 資料夾複製到方案的根目錄中，這位於方案的 .sln 檔案所在的目錄中。</span><span class="sxs-lookup"><span data-stu-id="aba05-209">Copy the *packages* folder in the root of the empty ASP.NET MVC 3 project solution into the root of your solution, which is in the directory where the solution's .sln file is located.</span></span>
4. <span data-ttu-id="aba05-210">如果您的 ASP.NET MVC 2 專案包含任何區域，請將/Views/Web.config 檔案複製到每個區域的*Views*資料夾。</span><span class="sxs-lookup"><span data-stu-id="aba05-210">If your ASP.NET MVC 2 project contains any areas, copy the /Views/Web.config file to the *Views* folder of each area.</span></span>
5. <span data-ttu-id="aba05-211">在 ASP.NET MVC 2 專案中的兩個 web.config 檔案中，全域搜尋並取代 ASP.NET MVC 版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-211">In both Web.config files in the ASP.NET MVC 2 project, globally search and replace the ASP.NET MVC version.</span></span> <span data-ttu-id="aba05-212">搜尋下列文字：</span><span class="sxs-lookup"><span data-stu-id="aba05-212">Find the following:</span></span> 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="aba05-213">然後取代成下列文字：</span><span class="sxs-lookup"><span data-stu-id="aba05-213">Replace it with the following:</span></span>

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. <span data-ttu-id="aba05-214">在方案總管中，刪除*system.web*的參考（指向第2版的 DLL），然後加入*system.web*的參考（v 3.0.0.0）。</span><span class="sxs-lookup"><span data-stu-id="aba05-214">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the DLL from version 2), then add a reference to *System.Web.Mvc* (v3.0.0.0).</span></span>
7. <span data-ttu-id="aba05-215">加入 System.web 的參考，然後再新增 system.web. system.web。</span><span class="sxs-lookup"><span data-stu-id="aba05-215">Add a reference to System.Web.WebPages.dll and System.Web.Helpers.dll.</span></span> <span data-ttu-id="aba05-216">這些組件位於下列資料夾：</span><span class="sxs-lookup"><span data-stu-id="aba05-216">These assemblies are located in the following folders:</span></span> 

    - <span data-ttu-id="aba05-217">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span><span class="sxs-lookup"><span data-stu-id="aba05-217">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span></span>
    - <span data-ttu-id="aba05-218">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies</span><span class="sxs-lookup"><span data-stu-id="aba05-218">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies</span></span>
8. <span data-ttu-id="aba05-219">在 [方案總管] 中，以滑鼠右鍵按一下專案名稱，並選取 [卸載專案]。</span><span class="sxs-lookup"><span data-stu-id="aba05-219">In Solution Explorer, right-click the project name and select Unload Project.</span></span> <span data-ttu-id="aba05-220">然後再次以滑鼠右鍵按一下專案名稱，並選取 [編輯*專案*名稱 .csproj]。</span><span class="sxs-lookup"><span data-stu-id="aba05-220">Then right-click the project name again and select Edit *ProjectName*.csproj.</span></span>
9. <span data-ttu-id="aba05-221">找出*ProjectTypeGuids*元素，並將 {F85E285D-A4E0-4152-9332-AB1D724D3325} 取代為 {E53F8FEA-EAE0-44A6-8774-FFD645390401}。</span><span class="sxs-lookup"><span data-stu-id="aba05-221">Locate the *ProjectTypeGuids* element and replace {F85E285D-A4E0-4152-9332-AB1D724D3325} with {E53F8FEA-EAE0-44A6-8774-FFD645390401}.</span></span>
10. <span data-ttu-id="aba05-222">儲存變更、以滑鼠右鍵按一下專案，然後選取 [重新載入專案]。</span><span class="sxs-lookup"><span data-stu-id="aba05-222">Save the changes, right-click the project, and then select Reload Project.</span></span>
11. <span data-ttu-id="aba05-223">在應用程式的根 web.config 檔案中，將下列設定新增至 [*元件*] 區段。</span><span class="sxs-lookup"><span data-stu-id="aba05-223">In the application's root Web.config file, add the following settings to the *assemblies* section.</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. <span data-ttu-id="aba05-224">如果專案參考使用 ASP.NET MVC 2 編譯的任何協力廠商程式庫，請將下列反白顯示的*bindingRedirect*元素新增至應用程式根目錄的 web.config 檔案中設定*區段底下*：</span><span class="sxs-lookup"><span data-stu-id="aba05-224">If the project references any third-party libraries that are compiled using ASP.NET MVC 2, add the following highlighted *bindingRedirect* element to the Web.config file in the application root under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a><span data-ttu-id="aba05-225">ASP.NET MVC 3 工具更新中的變更</span><span class="sxs-lookup"><span data-stu-id="aba05-225">Changes in ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="aba05-226">本節說明自 ASP.NET MVC 3 RTM 版本以來，在 ASP.NET MVC 3 工具更新版本中所做的變更。</span><span class="sxs-lookup"><span data-stu-id="aba05-226">This section describes changes made in the ASP.NET MVC 3 Tools Update release since the ASP.NET MVC 3 RTM release.</span></span>

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a><span data-ttu-id="aba05-227">[加入控制器] 對話方塊現在可以使用檢視和資料存取程式碼 Scaffold 控制器</span><span class="sxs-lookup"><span data-stu-id="aba05-227">"Add Controller" dialog box can now scaffold controllers with views and data access code</span></span>

<span data-ttu-id="aba05-228">Scaffolding 可用來快速產生您應用程式的控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="aba05-228">Scaffolding is a way of quickly generating a controller and views for your application.</span></span> <span data-ttu-id="aba05-229">程式碼產生之後，您可以進行編輯，以符合您的專案需求。</span><span class="sxs-lookup"><span data-stu-id="aba05-229">After the code has been generated, you can edit it to meet your project's requirements.</span></span>

<span data-ttu-id="aba05-230">若要啟動 ASP.NET MVC 3 中的 [*新增控制器*] 對話方塊，請以滑鼠右鍵按一下*方案總管*中的 [*控制器*] 資料夾，按一下 [*新增*]，然後按一下 [*控制器*]。</span><span class="sxs-lookup"><span data-stu-id="aba05-230">To launch the *Add Controller* dialog box in ASP.NET MVC 3, right-click the *Controllers* folder in *Solution Explorer*, click *Add*, and then click *Controller*.</span></span> <span data-ttu-id="aba05-231">此對話方塊功能已增強，可提供額外的 Scaffolding 選項。</span><span class="sxs-lookup"><span data-stu-id="aba05-231">The dialog box has been enhanced to offer additional scaffolding options.</span></span>

![](mvc3-release-notes/_static/image1.png)

<span data-ttu-id="aba05-232">根據預設，有三個 Scaffolding 範本可供使用。</span><span class="sxs-lookup"><span data-stu-id="aba05-232">There are three scaffolding templates available by default.</span></span>

#### <a name="empty-controller"></a><span data-ttu-id="aba05-233">空白控制器</span><span class="sxs-lookup"><span data-stu-id="aba05-233">Empty Controller</span></span>

<span data-ttu-id="aba05-234">此範本會產生空白的控制器檔案。</span><span class="sxs-lookup"><span data-stu-id="aba05-234">This template generates an empty controller file.</span></span> <span data-ttu-id="aba05-235">此範本等同于在舊版 ASP.NET MVC 中，不會*針對 [建立]、[編輯]、[詳細資料]、[刪除] 案例檢查新增動作*。</span><span class="sxs-lookup"><span data-stu-id="aba05-235">This template is equivalent to not checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="aba05-236">如果您選擇此範本，就不能另外提供選項。</span><span class="sxs-lookup"><span data-stu-id="aba05-236">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-empty-readwrite-actions"></a><span data-ttu-id="aba05-237">具有空白讀取/寫入動作的控制器</span><span class="sxs-lookup"><span data-stu-id="aba05-237">Controller with empty read/write actions</span></span>

<span data-ttu-id="aba05-238">此範本會產生包含所有必要動作方法的控制器檔案，但方法中沒有實作程式碼。</span><span class="sxs-lookup"><span data-stu-id="aba05-238">This template generates a controller file that has all the required action methods but no implementation code in the methods.</span></span> <span data-ttu-id="aba05-239">此範本相當於針對舊版 ASP.NET MVC 中*的 [建立]、[編輯]、[詳細資料]、[刪除] 案例檢查 [加入動作*]。</span><span class="sxs-lookup"><span data-stu-id="aba05-239">This template is equivalent to checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="aba05-240">如果您選擇此範本，就不能另外提供選項。</span><span class="sxs-lookup"><span data-stu-id="aba05-240">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a><span data-ttu-id="aba05-241">具有讀取/寫入動作和檢視、使用 Entity Framework 的控制器</span><span class="sxs-lookup"><span data-stu-id="aba05-241">Controller with read/write actions and views, using Entity Framework</span></span>

<span data-ttu-id="aba05-242">此範本可讓您迅速建立有效的資料輸入使用者介面。</span><span class="sxs-lookup"><span data-stu-id="aba05-242">This template enables you to quickly create a working data-entry user interface.</span></span> <span data-ttu-id="aba05-243">它會產生用於處理一組通用需求和案例的程式碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-243">It generates code that handles a range of common requirements and scenarios, such as the following:</span></span>

- <span data-ttu-id="aba05-244">*資料存取*。</span><span class="sxs-lookup"><span data-stu-id="aba05-244">*Data access*.</span></span> <span data-ttu-id="aba05-245">產生的程式碼會在資料庫中讀取和寫入實體。</span><span class="sxs-lookup"><span data-stu-id="aba05-245">The generated code reads and writes entities in a database.</span></span> <span data-ttu-id="aba05-246">如果您選擇現有的資料內容類別，或如果您讓範本產生新的*DbCoNtext*類別，它就會與 Entity Framework Code First 方法搭配使用。</span><span class="sxs-lookup"><span data-stu-id="aba05-246">It works with the Entity Framework Code First approach if you choose an existing data context class or if you let the template generate a new *DbContext* class.</span></span> <span data-ttu-id="aba05-247">如果您選擇現有的*ObjectCoNtext*類別，它也適用于 Entity Framework Database First 或 Model First 方法。</span><span class="sxs-lookup"><span data-stu-id="aba05-247">It also works with the Entity Framework Database First or Model First approach if you choose an existing *ObjectContext* class.</span></span>
- <span data-ttu-id="aba05-248">*驗證*。</span><span class="sxs-lookup"><span data-stu-id="aba05-248">*Validation*.</span></span> <span data-ttu-id="aba05-249">產生的程式碼會使用 ASP.NET MVC 模型繫結和中繼資料功能，如此系統會根據模型類別所宣告的規則來驗證表單提交作業。</span><span class="sxs-lookup"><span data-stu-id="aba05-249">The generated code uses ASP.NET MVC model binding and metadata features so that form submissions are validated according to rules declared on your model class.</span></span> <span data-ttu-id="aba05-250">這包括內建的驗證規則，例如*Required*和*StringLength*屬性，以及自訂驗證規則。</span><span class="sxs-lookup"><span data-stu-id="aba05-250">This includes built-in validation rules, such as the *Required* and *StringLength* attributes, and custom validation rules.</span></span>
- <span data-ttu-id="aba05-251">*一對多關聯性*。</span><span class="sxs-lookup"><span data-stu-id="aba05-251">*One-to-many relationships*.</span></span> <span data-ttu-id="aba05-252">如果您在模型類別之間定義一對多外部索引鍵關係，則產生的程式碼會產生下拉式清單供您選擇相關的實體。</span><span class="sxs-lookup"><span data-stu-id="aba05-252">If you define one-to-many foreign-key relationships between your model classes, the generated code will produce drop-down lists for selecting related entities.</span></span> <span data-ttu-id="aba05-253">例如，您可能依循「Entity Framework 程式碼優先」慣例定義下列模型類別：</span><span class="sxs-lookup"><span data-stu-id="aba05-253">For example, you might define the following model classes following Entity Framework Code First conventions:</span></span> 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    <span data-ttu-id="aba05-254">當您接著 scaffold *product*類別的控制器時，其 views 可讓使用者為每個*產品*實例選擇*Category*物件。</span><span class="sxs-lookup"><span data-stu-id="aba05-254">When you then scaffold a controller for the *Product* class, its views will allow users to choose a *Category* object for each *Product* instance.</span></span>

    <span data-ttu-id="aba05-255">此範本會啟用 [*新增控制器*] 對話方塊中的其他選項。</span><span class="sxs-lookup"><span data-stu-id="aba05-255">This template enables additional options in the *Add Controller* dialog box.</span></span> <span data-ttu-id="aba05-256">針對*模型類別*，您可以在方案中選擇任何模型類別，這會決定使用者可以建立或編輯的資料類型：</span><span class="sxs-lookup"><span data-stu-id="aba05-256">For *Model class*, you can choose any model class in your solution, which determines the type of data that users will be able to create or edit:</span></span>
- <span data-ttu-id="aba05-257">如果您要使用「Entity Framework 程式碼優先」，則可以選擇任何模型類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-257">If you want to use Entity Framework Code First, you can choose any model class.</span></span>
- <span data-ttu-id="aba05-258">如果您使用的是「Entity Framework 資料庫優先」或「Entity Framework 模型優先」，請務必選擇您概念模型中定義的實體類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-258">If you are using Entity Framework Database First or Entity Framework Model First, be sure to choose an entity class defined in your conceptual model.</span></span>

<span data-ttu-id="aba05-259">針對*資料內容類別*，您可以進行下列選擇：</span><span class="sxs-lookup"><span data-stu-id="aba05-259">For *Data Context class*, you can make these choices:</span></span>

- <span data-ttu-id="aba05-260">如果您想要使用 Code First，而且沒有現有的資料內容類別，請選擇 [新增資料內容]。</span><span class="sxs-lookup"><span data-stu-id="aba05-260">If you want to use Code First and have no existing data context class, choose \*\*New data context \*\*.</span></span> <span data-ttu-id="aba05-261">系統會為您產生資料內容類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-261">A data context class will then be generated for you.</span></span>
- <span data-ttu-id="aba05-262">如果您要使用「程式碼優先」且具有資料內容類別，則在此選擇此類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-262">If you want to use Code First and have an existing data context class, choose it here.</span></span> <span data-ttu-id="aba05-263">此類別會進行更新以保存您選取的模型類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-263">It will be updated to persist the model class you have selected.</span></span>
- <span data-ttu-id="aba05-264">如果您使用的是「資料庫優先」或「模型優先」，則在此選擇您的物件內容類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-264">If you are using Database First or Model First, choose your object context class here.</span></span>

<span data-ttu-id="aba05-265">針對 [檢視]，請選擇您要使用的檢視引擎，或選擇 [無]，如果您不要 Scaffold 任何檢視。</span><span class="sxs-lookup"><span data-stu-id="aba05-265">For Views, choose the view engine you want to use, or choose None if you don't want to scaffold any views.</span></span>

<span data-ttu-id="aba05-266">您可以選取 [Advanced Optionsto]，為產生的視圖指定進一步的選項。</span><span class="sxs-lookup"><span data-stu-id="aba05-266">You can select Advanced Optionsto specify further options for the generated views.</span></span> <span data-ttu-id="aba05-267">例如，您可以選擇要使用的版面配置頁或主版頁面。</span><span class="sxs-lookup"><span data-stu-id="aba05-267">For example, you can choose the layout or master page to use.</span></span>

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a><span data-ttu-id="aba05-268">[ASP.NET MVC 3 新增專案] 對話方塊中的改進功能</span><span class="sxs-lookup"><span data-stu-id="aba05-268">Improvements to the "ASP.NET MVC 3 New Project" Dialog Box</span></span>

<span data-ttu-id="aba05-269">您用來建立新 ASP.NET MVC 3 專案的對話方塊包含多項改良功能，如下所示。</span><span class="sxs-lookup"><span data-stu-id="aba05-269">The dialog box you use to create new ASP.NET MVC 3 projects includes multiple improvements, as listed below.</span></span>

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a><span data-ttu-id="aba05-270">新的「內部網路專案」範本</span><span class="sxs-lookup"><span data-stu-id="aba05-270">New "Intranet Project" Template</span></span>

<span data-ttu-id="aba05-271">[專案範本] 清單包含新的 [內部網路應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="aba05-271">The Project Template list includes a new Intranet Application template.</span></span> <span data-ttu-id="aba05-272">此範本包含的設定是用於以 Windows 驗證 (而不是表單驗證) 建置 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aba05-272">This template contains settings for building a web application using Windows authentication instead of forms authentication.</span></span> <span data-ttu-id="aba05-273">因為內部網路應用程式需要一些無法封裝在專案範本中的 IIS 設定，所以範本會包含讀我檔案，其中包含如何讓專案範本在 IIS 中工作的指示。</span><span class="sxs-lookup"><span data-stu-id="aba05-273">Because an intranet application requires some IIS settings that can't be encapsulated in a project template, the template includes a readme file with instructions for how to make the project template work in IIS.</span></span> <span data-ttu-id="aba05-274">您可以在 MSDN 網站上找到新的內部網路應用程式範本的檔，網址如下：</span><span class="sxs-lookup"><span data-stu-id="aba05-274">Documentation for the a new Intranet Application template is available on the MSDN website at the following URL:</span></span>

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a><span data-ttu-id="aba05-275">專案範本現在已啟用 HTML5</span><span class="sxs-lookup"><span data-stu-id="aba05-275">Project templates are now HTML5 enabled</span></span>

<span data-ttu-id="aba05-276">[新增專案] 對話方塊現在包含可將 HTML5 專屬功能加入至專案範本的選項。</span><span class="sxs-lookup"><span data-stu-id="aba05-276">The new-project dialog box now contains an option to add HTML5-specific features to the project templates.</span></span> <span data-ttu-id="aba05-277">選取此選項會產生包含新 HTML5 `<header>`、`<footer>`和 `<navigation>` 元素的 views。</span><span class="sxs-lookup"><span data-stu-id="aba05-277">Selecting the option causes views to be generated that contain the new HTML5 `<header>`, `<footer>`, and `<navigation>` elements.</span></span>

<span data-ttu-id="aba05-278">請注意舊版瀏覽器不支援 HTML5 專屬標記。</span><span class="sxs-lookup"><span data-stu-id="aba05-278">Note that earlier versions of browsers do not support HTML5-specific tags.</span></span> <span data-ttu-id="aba05-279">若要解決這項限制，HTML5 專案範本必須加入 Modernizr 程式庫的參考</span><span class="sxs-lookup"><span data-stu-id="aba05-279">To address this limitation, the HTML5 project templates include a reference to the Modernizr library.</span></span> <span data-ttu-id="aba05-280">(請參閱下節)。</span><span class="sxs-lookup"><span data-stu-id="aba05-280">(See the next section.)</span></span>

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a><span data-ttu-id="aba05-281">專案範本現在包含 Modernizr 1.7</span><span class="sxs-lookup"><span data-stu-id="aba05-281">Project templates now include Modernizr 1.7</span></span>

<span data-ttu-id="aba05-282">Modernizr 是一種 JavaScript 程式庫，可支援瀏覽器中尚未支援這些功能的 CSS 3 和 HTML5。</span><span class="sxs-lookup"><span data-stu-id="aba05-282">Modernizr is a JavaScript library that enables support for CSS 3 and HTML5 in browsers that do not yet support these features.</span></span> <span data-ttu-id="aba05-283">此程式庫是以預先安裝的 NuGet 套件形式包含在 ASP.NET MVC 3 專案的範本中。</span><span class="sxs-lookup"><span data-stu-id="aba05-283">This library is included as a pre-installed NuGet package in templates for ASP.NET MVC 3 projects.</span></span> <span data-ttu-id="aba05-284">如需 Modernizr 的詳細資訊，請參閱[http://www.modernizr.com/](http://www.modernizr.com/)。</span><span class="sxs-lookup"><span data-stu-id="aba05-284">For more information about Modernizr, see [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a><span data-ttu-id="aba05-285">專案範本包含 jQuery、jQuery UI 和 jQuery Validation 的更新版本</span><span class="sxs-lookup"><span data-stu-id="aba05-285">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>

<span data-ttu-id="aba05-286">專案範本現在包含下列 jQuery 指令碼版本：</span><span class="sxs-lookup"><span data-stu-id="aba05-286">The project templates now include the following versions of the jQuery scripts:</span></span>

- <span data-ttu-id="aba05-287">jQuery 1.5.1</span><span class="sxs-lookup"><span data-stu-id="aba05-287">jQuery 1.5.1</span></span>
- <span data-ttu-id="aba05-288">jQuery Validation 1.8</span><span class="sxs-lookup"><span data-stu-id="aba05-288">jQuery Validation 1.8</span></span>
- <span data-ttu-id="aba05-289">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="aba05-289">jQuery UI 1.8.11</span></span>

<span data-ttu-id="aba05-290">這些程式庫皆以預先安裝的 NuGet 套件形式內含在專案範本中。</span><span class="sxs-lookup"><span data-stu-id="aba05-290">These libraries are included as pre-installed NuGet packages.</span></span>

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a><span data-ttu-id="aba05-291">專案範本現在包含 ADO.NET Entity Framework 4.1，其以預先安裝的 NuGet 套件形式內含在範本中</span><span class="sxs-lookup"><span data-stu-id="aba05-291">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>

<span data-ttu-id="aba05-292">ADO.NET Entity Framework 4.1 包含 Code First 功能。</span><span class="sxs-lookup"><span data-stu-id="aba05-292">The ADO.NET Entity Framework 4.1 includes the Code First feature.</span></span> <span data-ttu-id="aba05-293">「程式碼優先」是 ADO.NET Entity Framework 的新開發模式，提供另一種方法來替代現有「資料庫優先」和「模型優先」模式。</span><span class="sxs-lookup"><span data-stu-id="aba05-293">Code First is a new development pattern for the ADO.NET Entity Framework that provides an alternative to the existing Database First and Model First patterns.</span></span>

<span data-ttu-id="aba05-294">「程式碼優先」的重點是使用以 Visual Basic 或 C# 撰寫的 POCO 類別 (「一般簡單的 CLR 物件」) 定義您的模型。</span><span class="sxs-lookup"><span data-stu-id="aba05-294">Code First is focused around defining your model using POCO classes ("plain old CLR objects") written in Visual Basic or C#.</span></span> <span data-ttu-id="aba05-295">這些類別接著可以對應至現有資料庫，或用來產生資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="aba05-295">These classes can then be mapped to an existing database or be used to generate a database schema.</span></span> <span data-ttu-id="aba05-296">您可以使用*DataAnnotations*屬性或使用流暢的 api 來提供額外的設定。</span><span class="sxs-lookup"><span data-stu-id="aba05-296">Additional configuration can be supplied using *DataAnnotations* attributes or using fluent APIs.</span></span>

<span data-ttu-id="aba05-297">如需使用程式碼 Firstwith ASP.NET MVC 的檔，請參閱 ASP.NET 網站上的下列 Url：</span><span class="sxs-lookup"><span data-stu-id="aba05-297">Documentation for using Code Firstwith ASP.NET MVC is available on the ASP.NET website at the following URLs:</span></span>

<span data-ttu-id="aba05-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="aba05-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span></span>

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a><span data-ttu-id="aba05-299">專案範本包含 JavaScript 程式庫，其以預先安裝的 NuGet 套件形式內含在範本中</span><span class="sxs-lookup"><span data-stu-id="aba05-299">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>

<span data-ttu-id="aba05-300">當您建立新的 ASP.NET MVC 3 專案時，專案會包含先前所述的 JavaScript 檔案（例如，Modernizr 程式庫），方法是使用 NuGet 安裝它們，而不是直接將腳本新增至專案範本中的 Scripts 資料夾。編制.</span><span class="sxs-lookup"><span data-stu-id="aba05-300">When you create a new ASP.NET MVC 3 project, the project includes the JavaScript files mentioned previously (for example, the Modernizr library) by installing them using NuGet instead of directly adding the scripts to the Scripts folder in the project template contents.</span></span> <span data-ttu-id="aba05-301">如此可讓您在指令碼新版本發行時，使用 NuGet 將指令碼更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-301">This enables you to use NuGet to update the scripts to the latest version when new versions of the scripts are released.</span></span>

<span data-ttu-id="aba05-302">例如，鑑於 jQuery 新版發行的頻率，專案範本內含的 jQuery 版本在某個時間點即會過時。</span><span class="sxs-lookup"><span data-stu-id="aba05-302">For example, given the frequency of new jQuery releases, the version of jQuery included in the project template will at some point be out of date.</span></span> <span data-ttu-id="aba05-303">不過，因為 jQuery 是以已安裝的 NuGet 套件內含在專案範本中，當 jQuery 新版發行時，將會透過 NuGet 對話方塊通知您。</span><span class="sxs-lookup"><span data-stu-id="aba05-303">However, because jQuery is included as an installed NuGet package, you will be notified in the NuGet dialog box when newer versions of jQuery are available.</span></span>

<span data-ttu-id="aba05-304">因為 jQuery 在檔案名中包含版本號碼，所以將 jQuery 更新為最新版本也需要更新參考 jQuery 檔案的 `<script>` 標記，以使用新的檔案名。</span><span class="sxs-lookup"><span data-stu-id="aba05-304">Because jQuery includes the version number in the file name, updating jQuery to the latest version also requires updating the `<script>` tag that references the jQuery file to use the new file name.</span></span> <span data-ttu-id="aba05-305">其他內含的指令碼程式庫並沒有在指令碼名稱中加入版本編號，所以較易於更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-305">Other included script libraries do not include the version number in the script name, so they can be more easily updated to their latest versions.</span></span>

<a id="tu-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="aba05-306">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-306">Known Issues</span></span>

- <span data-ttu-id="aba05-307">在某些情況下，安裝可能會失敗，並出現錯誤訊息「安裝失敗，錯誤碼為（0x80070643）」。</span><span class="sxs-lookup"><span data-stu-id="aba05-307">In some cases, installation may fail with the error message "Installation failed with error code (0x80070643)".</span></span> <span data-ttu-id="aba05-308">如需有關如何解決此問題的詳細資訊，請參閱[知識庫文章 2531566](https://support.microsoft.com/kb/2531566)。</span><span class="sxs-lookup"><span data-stu-id="aba05-308">For information about how to work around this issue, see [KnowledgeBase article 2531566](https://support.microsoft.com/kb/2531566).</span></span>
- <span data-ttu-id="aba05-309">用於加入控制器的 scaffolding 不會 Scaffold 利用 Entity Framework 實體繼承支援的實體。</span><span class="sxs-lookup"><span data-stu-id="aba05-309">The scaffolding for adding a controller does not scaffold entities that take advantage of entity inheritance support within Entity Framework.</span></span> <span data-ttu-id="aba05-310">例如，假設有一個由*student*類別繼承的基礎*Person*類別，則*student*類別會產生未編譯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="aba05-310">For example, given a base *Person* class that's inherited by a *Student* class, scaffolding the *Student* class will result in generated code that does not compile.</span></span>
- <span data-ttu-id="aba05-311">在方案資料夾中建立新的 ASP.NET MVC 3 專案會造成*NullReferenceException*錯誤。</span><span class="sxs-lookup"><span data-stu-id="aba05-311">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="aba05-312">因應措施是在方案的根目錄中建立 ASP.NET MVC 3 專案，然後將它移至方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="aba05-312">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="aba05-313">電腦若有安裝 ReSharper，Razor 語法的 IntelliSense 即無法運作。</span><span class="sxs-lookup"><span data-stu-id="aba05-313">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="aba05-314">如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 中的 Razor IntelliSense 支援，請參閱 Hadi Hariri 的 blog 中的專案[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中會討論今日使用它們的方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-314">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="aba05-315">在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。</span><span class="sxs-lookup"><span data-stu-id="aba05-315">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="aba05-316">當您編輯 Razor view （. cshtml 或）時。*vbhtml*檔案）、views。</span><span class="sxs-lookup"><span data-stu-id="aba05-316">When you are editing a Razor view (.cshtml or .*vbhtml* file), views.</span></span> <span data-ttu-id="aba05-317">ASP.NET MVC 3 不包含 Razor views 的任何程式碼片段。aspxselecting ASP.NET MVC 的程式碼片段會顯示的程式碼片段</span><span class="sxs-lookup"><span data-stu-id="aba05-317">ASP.NET MVC 3 does not include any snippets for Razor views..aspxselecting a code snippet for ASP.NET MVC will show snippets for</span></span>
- <span data-ttu-id="aba05-318">如果您在未安裝 Visual Studio 的電腦上安裝 ASP.NET MVC 3 for Visual Web Developer Express，然後在稍後安裝 Visual Studio，則必須重新安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="aba05-318">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="aba05-319">Visual Studio 和 Visual Web Developer Express 共用 ASP.NET MVC 3 安裝程式所升級的元件。</span><span class="sxs-lookup"><span data-stu-id="aba05-319">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="aba05-320">如果您在沒有 Visual Web Developer Express 的電腦上安裝 ASP.NET MVC Visual Studio 3，然後再安裝 Visual Web Developer Express，則適用相同的問題。</span><span class="sxs-lookup"><span data-stu-id="aba05-320">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a><span data-ttu-id="aba05-321">ASP.NET MVC 3 RTM 中的變更</span><span class="sxs-lookup"><span data-stu-id="aba05-321">Changes in ASP.NET MVC 3 RTM</span></span>

<span data-ttu-id="aba05-322">本節說明自 RC2 版本開始，在 ASP.NET MVC 3 RTM 版本中所做的變更和 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="aba05-322">This section describes changes and bug fixes made in the ASP.NET MVC 3 RTM release since the RC2 release.</span></span>

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a><span data-ttu-id="aba05-323">變更：將 jQuery UI 的版本更新為1.8。7</span><span class="sxs-lookup"><span data-stu-id="aba05-323">Change: Updated the version of jQuery UI to 1.8.7</span></span>

<span data-ttu-id="aba05-324">Visual Studio 的 ASP.NET MVC 專案範本已更新為包含最新版的 jQuery UI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="aba05-324">The ASP.NET MVC project templates for Visual Studio were updated to include the latest version of the jQuery UI library.</span></span> <span data-ttu-id="aba05-325">這些範本也包含 jQuery UI 所需的最小資源檔集，例如相關聯的 CSS 和影像檔案。</span><span class="sxs-lookup"><span data-stu-id="aba05-325">The templates also include the minimal set of resource files required by jQuery UI, such as the associated CSS and image files.</span></span>

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a><span data-ttu-id="aba05-326">變更：將預設 ModelMetadataProvider 變更回 DataAnnotationsModelMetadataProvider</span><span class="sxs-lookup"><span data-stu-id="aba05-326">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>

<span data-ttu-id="aba05-327">ASP.NET MVC 3 的 RC2 版本引進了*CachedDataAnnotationsMetadataProvider*類別，它會在現有*DataAnnotationsModelMetadataProvider*類別上提供快取，以改善效能。</span><span class="sxs-lookup"><span data-stu-id="aba05-327">The RC2 release of ASP.NET MVC 3 introduced a *CachedDataAnnotationsMetadataProvider* class that provided caching on top of the existing *DataAnnotationsModelMetadataProvider* class as a performance improvement.</span></span> <span data-ttu-id="aba05-328">不過，某些 bug 是使用此實作為回報，因此變更已還原並移至 MVC 先期專案中，可在[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)取得。</span><span class="sxs-lookup"><span data-stu-id="aba05-328">However, some bugs were reported with this implementation, so the change has been reverted and moved into the MVC Futures project, which is available at [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack).</span></span>

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a><span data-ttu-id="aba05-329">已修正：貼上包含空白字元的 Razor 運算式部分，會導致它被反轉</span><span class="sxs-lookup"><span data-stu-id="aba05-329">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>

<span data-ttu-id="aba05-330">在 ASP.NET MVC 3 的發行前版本中，當您將包含空白字元的 Razor 運算式部分貼入 Razor 檔案時，產生的運算式會反轉。</span><span class="sxs-lookup"><span data-stu-id="aba05-330">In pre-release versions of ASP.NET MVC 3, when you paste a part of a Razor expression that contains whitespace into a Razor file, the resulting expression is reversed.</span></span> <span data-ttu-id="aba05-331">例如，請考慮下列 Razor 程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="aba05-331">For example, consider the following Razor code block:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

<span data-ttu-id="aba05-332">如果您在第一個方法中選取「第一個參數」文字，並將它當做引數貼入第二個方法中，則結果會如下所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-332">If you select the text "first param" in the first method and paste it as an argument into the second method, the result is as follows:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="aba05-333">正確的行為是貼上作業應該會產生下列結果：</span><span class="sxs-lookup"><span data-stu-id="aba05-333">The correct behavior is that the paste operation should result in the following:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

<span data-ttu-id="aba05-334">此問題已在 RTM 版本中修正，以便在貼上作業期間正確地保留運算式。</span><span class="sxs-lookup"><span data-stu-id="aba05-334">This issue has been fixed in the RTM release so that the expression is correctly preserved during the paste operation.</span></span>

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a><span data-ttu-id="aba05-335">已修正：重新命名在編輯器中開啟的 Razor 檔案時，會停用語法顏色標示和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="aba05-335">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>

<span data-ttu-id="aba05-336">在編輯器視窗中開啟檔案時，使用方案總管重新命名 Razor 檔案，會導致語法醒目提示和 IntelliSense 停止處理該檔案。</span><span class="sxs-lookup"><span data-stu-id="aba05-336">Renaming a Razor file using Solution Explorer while the file is opened in the editor window causes syntax highlighting and IntelliSense to stop working for that file.</span></span> <span data-ttu-id="aba05-337">已修正此問題，以便在重新命名之後維護反白顯示和 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="aba05-337">This has been fixed so that highlighting and IntelliSense are maintained after a rename.</span></span>

<a id="RTM-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="aba05-338">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-338">Known Issues</span></span>

- <span data-ttu-id="aba05-339">如果您在 NuGet 套件管理員主控台開啟時關閉 Visual Studio 2010 SP1 Beta 版，Visual Studio 損毀並嘗試重新開機。</span><span class="sxs-lookup"><span data-stu-id="aba05-339">If you close Visual Studio 2010 SP1 Beta while the NuGet Package Manager Console is open, Visual Studio crashes and attempts to restart.</span></span> <span data-ttu-id="aba05-340">這會在 Visual Studio 2010 SP1 的 RTM 版本中修正。</span><span class="sxs-lookup"><span data-stu-id="aba05-340">This will be fixed in the RTM release of Visual Studio 2010 SP1.</span></span>
- <span data-ttu-id="aba05-341">ASP.NET MVC 3 安裝程式只可以安裝 NuGet 套件管理員的初始版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-341">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="aba05-342">安裝初始版本之後，您可以使用 Visual Studio 擴充管理員來安裝和更新 NuGet。</span><span class="sxs-lookup"><span data-stu-id="aba05-342">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="aba05-343">如果您已安裝 NuGet，請移至 Visual Studio 擴充功能庫，以更新為最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="aba05-343">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="aba05-344">在方案資料夾中建立新的 ASP.NET MVC 3 專案會造成*NullReferenceException*錯誤。</span><span class="sxs-lookup"><span data-stu-id="aba05-344">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="aba05-345">因應措施是在方案的根目錄中建立 ASP.NET MVC 3 專案，然後將它移至方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="aba05-345">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="aba05-346">安裝程式所需的時間可能比先前版本的 ASP.NET MVC 還長，因此無法完成。</span><span class="sxs-lookup"><span data-stu-id="aba05-346">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="aba05-347">這是因為它會更新 Visual Studio 2010 的元件。</span><span class="sxs-lookup"><span data-stu-id="aba05-347">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="aba05-348">電腦若有安裝 ReSharper，Razor 語法的 IntelliSense 即無法運作。</span><span class="sxs-lookup"><span data-stu-id="aba05-348">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="aba05-349">如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 中的 Razor IntelliSense 支援，請參閱 Hadi Hariri 的 blog 中的專案[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中會討論今日使用它們的方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-349">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="aba05-350">使用 ASP.NET MVC 3 Beta 版所建立的 CCSHTML 和 VBHTML 視圖並未正確設定其組建動作，結果是在發行專案時，會省略這些檢視類型。</span><span class="sxs-lookup"><span data-stu-id="aba05-350">CCSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="aba05-351">這些檔案的 [組建動作] 值應該設定為 [內容]。</span><span class="sxs-lookup"><span data-stu-id="aba05-351">The Build Action value for these files should be set to "Content".</span></span> <span data-ttu-id="aba05-352">ASP.NET MVC 3 RTM 會針對新檔案修正此問題，但不會針對使用發行前版本所建立之專案的現有檔案更正其設定。</span><span class="sxs-lookup"><span data-stu-id="aba05-352">ASP.NET MVC 3 RTM fixes this issue for new files, but doesn't correct the setting for existing files for a project created with prerelease versions.</span></span>
- ![](mvc3-release-notes/_static/image3.png)
- <span data-ttu-id="aba05-353">在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。</span><span class="sxs-lookup"><span data-stu-id="aba05-353">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="aba05-354">當您編輯 Razor view （cshtml 檔案）時，Visual Studio 中的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="aba05-354">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="aba05-355">如果您在未安裝 Visual Studio 的電腦上安裝 ASP.NET MVC 3 for Visual Web Developer Express，然後在稍後安裝 Visual Studio，則必須重新安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="aba05-355">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="aba05-356">Visual Studio 和 Visual Web Developer Express 共用 ASP.NET MVC 3 安裝程式所升級的元件。</span><span class="sxs-lookup"><span data-stu-id="aba05-356">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="aba05-357">如果您在沒有 Visual Web Developer Express 的電腦上安裝 ASP.NET MVC Visual Studio 3，然後再安裝 Visual Web Developer Express，則適用相同的問題。</span><span class="sxs-lookup"><span data-stu-id="aba05-357">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="aba05-358">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-358">Breaking Changes</span></span>

- <span data-ttu-id="aba05-359">在舊版的 ASP.NET MVC 中，動作篩選準則會針對每個要求建立，但在少數情況下除外。</span><span class="sxs-lookup"><span data-stu-id="aba05-359">In previous versions of ASP.NET MVC, action filters are create per request except in a few cases.</span></span> <span data-ttu-id="aba05-360">這種行為絕對不是保證的行為，而是只有執行詳細資料，而篩選準則的合約是將其視為無狀態。</span><span class="sxs-lookup"><span data-stu-id="aba05-360">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="aba05-361">在 ASP.NET MVC 3 中，篩選會更積極地快取。</span><span class="sxs-lookup"><span data-stu-id="aba05-361">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="aba05-362">因此，任何不正確儲存實例狀態的自訂動作篩選可能會中斷。</span><span class="sxs-lookup"><span data-stu-id="aba05-362">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="aba05-363">例外狀況篩選準則的執行順序已針對具有相同*順序*值的例外狀況篩選準則進行變更。</span><span class="sxs-lookup"><span data-stu-id="aba05-363">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="aba05-364">在 ASP.NET MVC 2 和更早版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其*順序*值會與動作方法上的相同。</span><span class="sxs-lookup"><span data-stu-id="aba05-364">In ASP.NET MVC 2 and earlier, exception filters on the controller that have the same *Order* value as those on an action method are executed before the exception filters on the action method.</span></span> <span data-ttu-id="aba05-365">這通常是沒有指定*順序*值的例外狀況篩選準則套用時的情況。</span><span class="sxs-lookup"><span data-stu-id="aba05-365">This would typically be the case when exception filters are applied without a specified *Order* value.</span></span> <span data-ttu-id="aba05-366">在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。</span><span class="sxs-lookup"><span data-stu-id="aba05-366">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="aba05-367">如同在舊版中，如果已明確指定*order*屬性，則會以指定的循序執行篩選。</span><span class="sxs-lookup"><span data-stu-id="aba05-367">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="aba05-368">已將名為*microsoft.extensions.configuration fileextensions*的新屬性新增至*VirtualPathProviderViewEngine*基類。</span><span class="sxs-lookup"><span data-stu-id="aba05-368">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="aba05-369">當 ASP.NET 依路徑（而不是名稱）查詢檢視時，只會考慮包含在此新屬性所指定清單中具有副檔名的 views。</span><span class="sxs-lookup"><span data-stu-id="aba05-369">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="aba05-370">這是應用程式的重大變更，其中已註冊自訂群組建提供者以啟用 Web 表單檢視的自訂副檔名，以及提供者使用完整路徑（而非名稱）來參考這些視圖。</span><span class="sxs-lookup"><span data-stu-id="aba05-370">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="aba05-371">解決方法是修改*microsoft.extensions.configuration fileextensions*屬性的值，以包含自訂副檔名。</span><span class="sxs-lookup"><span data-stu-id="aba05-371">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="aba05-372">直接執行*IControllerFactory*介面的自訂控制器 factory 預建必須提供新*GetControllerSessionBehavior*方法的實作為，這會在此版本中新增至介面。</span><span class="sxs-lookup"><span data-stu-id="aba05-372">Custom controller factory implementations that directly implement the *IControllerFactory* interface must provide an implementation of the new *GetControllerSessionBehavior* method that was added to the interface in this release.</span></span> <span data-ttu-id="aba05-373">一般來說，建議您不要直接執行此介面，而改為從*DefaultControllerFactory*衍生您的類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-373">In general, it is recommended that you do not implement this interface directly and instead derive your class from *DefaultControllerFactory*.</span></span>

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a><span data-ttu-id="aba05-374">ASP.NET MVC 3 RC2 中的變更</span><span class="sxs-lookup"><span data-stu-id="aba05-374">Changes in ASP.NET MVC 3 RC2</span></span>

<span data-ttu-id="aba05-375">本節說明自 RC 版本以來 ASP.NET MVC 3 RC2 版本中所做的變更（新功能和 bug 修正）。</span><span class="sxs-lookup"><span data-stu-id="aba05-375">This section describes changes (new features and bug fixes) made in the ASP.NET MVC 3 RC2 release since the RC release.</span></span>

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a><span data-ttu-id="aba05-376">專案範本已變更為包含 jQuery 1.4.4、jQuery 驗證1.7 和 jQuery UI 1.8。6</span><span class="sxs-lookup"><span data-stu-id="aba05-376">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6</span></span>

<span data-ttu-id="aba05-377">ASP.NET MVC 3 的專案範本現在包含 jQuery、jQuery 驗證和 jQuery UI 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-377">The project templates for ASP.NET MVC 3 now include the latest versions of jQuery, jQuery Validation, and jQuery UI.</span></span> <span data-ttu-id="aba05-378">jQuery UI 是專案範本的新功能，並提供實用的使用者介面小工具。</span><span class="sxs-lookup"><span data-stu-id="aba05-378">jQuery UI is a new addition to the project templates and provides useful user interface widgets.</span></span> <span data-ttu-id="aba05-379">如需 jQuery UI 的詳細資訊，請造訪其首頁： [http://jqueryui.com/](http://jqueryui.com/)。</span><span class="sxs-lookup"><span data-stu-id="aba05-379">For more information about jQuery UI, visit their homepage: [http://jqueryui.com/](http://jqueryui.com/).</span></span>

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a><span data-ttu-id="aba05-380">已新增 "AdditionalMetadataAttribute" 類別</span><span class="sxs-lookup"><span data-stu-id="aba05-380">Added "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="aba05-381">您可以使用*AdditionalMetadataAttribute*類別來填入模型屬性的*ModelMetadata. AdditionalValues*字典。</span><span class="sxs-lookup"><span data-stu-id="aba05-381">You can use the *AdditionalMetadataAttribute* class to populate the *ModelMetadata.AdditionalValues* dictionary for a model property.</span></span>

<span data-ttu-id="aba05-382">例如，假設視圖模型具有應該只顯示給系統管理員的屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-382">For example, suppose a view model has properties that should be displayed only to an administrator.</span></span> <span data-ttu-id="aba05-383">該模型可以使用 AdminOnly 做為索引鍵的新屬性加上批註，並以 true 作為值，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-383">That model can be annotated with the new attribute using AdminOnly as the key and true as the value, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

<span data-ttu-id="aba05-384">當呈現產品視圖模型時，任何顯示或編輯器範本都會提供此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="aba05-384">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="aba05-385">身為應用程式開發人員，您可以用它來解讀中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="aba05-385">It is up to you as application developer to interpret the metadata information.</span></span>

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a><span data-ttu-id="aba05-386">改良的視圖樣板</span><span class="sxs-lookup"><span data-stu-id="aba05-386">Improved View Scaffolding</span></span>

<span data-ttu-id="aba05-387">用於樣板視圖的 T4 範本現在會產生對範本協助程式方法的呼叫，例如*EditorFor* ，而不是像是*TextBoxFor*的協助程式。</span><span class="sxs-lookup"><span data-stu-id="aba05-387">The T4 templates used for scaffolding views now generate calls to template helper methods such as *EditorFor* instead of helpers such as *TextBoxFor*.</span></span> <span data-ttu-id="aba05-388">這項變更會在 [加入視圖] 對話方塊產生視圖時，以資料批註屬性的形式改善模型上的中繼資料支援。</span><span class="sxs-lookup"><span data-stu-id="aba05-388">This change improves support for metadata on the model in the form of data annotation attributes when the Add View dialog box generates a view.</span></span>

<span data-ttu-id="aba05-389">[加入視圖] 樣板也會根據慣例，在模型上包含改善的主要金鑰資訊偵測和使用方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-389">The Add View scaffolding also includes improved detection and usage of primary key information on the model, based on convention.</span></span> <span data-ttu-id="aba05-390">例如，[加入視圖] 對話方塊會使用這項資訊來確保主要索引鍵值不會 scaffold 為可編輯的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="aba05-390">For example, the Add View dialog box uses this information to ensure that the primary key value is not scaffolded as an editable form field.</span></span>

<span data-ttu-id="aba05-391">預設的 [編輯] 和 [建立] 範本包含用戶端驗證所需之 jQuery 腳本的參考。</span><span class="sxs-lookup"><span data-stu-id="aba05-391">The default Edit and Create templates include references to the jQuery scripts needed for client validation.</span></span>

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a><span data-ttu-id="aba05-392">已新增 Html。 Raw 方法</span><span class="sxs-lookup"><span data-stu-id="aba05-392">Added Html.Raw Method</span></span>

<span data-ttu-id="aba05-393">根據預設，Razor view 引擎會對所有值進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="aba05-393">By default, the Razor view engine HTML-encodes all values.</span></span> <span data-ttu-id="aba05-394">例如，下列程式碼片段會將問候語變數中的 HTML 編碼，使其在頁面中顯示為 `<strong>Hello World!</strong>`。</span><span class="sxs-lookup"><span data-stu-id="aba05-394">For example, the following code snippet encodes the HTML inside the greeting variable so that it is displayed in the page as `<strong>Hello World!</strong>`.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

<span data-ttu-id="aba05-395">新的 *.html*方法提供簡單的方式，在已知內容安全時顯示未編碼的 Html。</span><span class="sxs-lookup"><span data-stu-id="aba05-395">The new *Html.Raw* method provides a simple way of displaying unencoded HTML when the content is known to be safe.</span></span> <span data-ttu-id="aba05-396">下列範例會顯示相同的字串，但字串會轉譯為標記：</span><span class="sxs-lookup"><span data-stu-id="aba05-396">The following example displays the same string, but the string is rendered as markup:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a><span data-ttu-id="aba05-397">將 "Controller. ViewModel" 屬性和 "View" 屬性重新命名為 "ViewBag"</span><span class="sxs-lookup"><span data-stu-id="aba05-397">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>

<span data-ttu-id="aba05-398">在過去，*控制器*的*ViewModel*屬性會雖然該值至視圖的*view*屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-398">Previously, the *ViewModel* property of *Controller* corresponded to the *View* property of a view.</span></span> <span data-ttu-id="aba05-399">這兩個屬性都提供使用動態屬性存取子語法來存取*ViewDataDictionary*物件值的方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-399">Both of these properties provide a way to access values of the *ViewDataDictionary* object using dynamic property-accessor syntax.</span></span> <span data-ttu-id="aba05-400">這兩個屬性都已重新命名為相同，以避免混淆並使其更一致。</span><span class="sxs-lookup"><span data-stu-id="aba05-400">Both properties have been renamed to be the same in order to avoid confusion and to be more consistent.</span></span>

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a><span data-ttu-id="aba05-401">將 "ControllerSessionStateAttribute" 類別重新命名為 "SessionStateAttribute"</span><span class="sxs-lookup"><span data-stu-id="aba05-401">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>

<span data-ttu-id="aba05-402">*ControllerSessionStateAttribute*類別是在 ASP.NET MVC 3 的 RC 版本中引進。</span><span class="sxs-lookup"><span data-stu-id="aba05-402">The *ControllerSessionStateAttribute* class was introduced in the RC release of ASP.NET MVC 3.</span></span> <span data-ttu-id="aba05-403">屬性已重新命名為更簡潔。</span><span class="sxs-lookup"><span data-stu-id="aba05-403">The property was renamed to be more succinct.</span></span>

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a><span data-ttu-id="aba05-404">將 RemoteAttribute "Fields" 屬性重新命名為 "AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="aba05-404">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>

<span data-ttu-id="aba05-405">*RemoteAttribute*類別的*Fields*屬性會在使用者之間造成一些混淆。</span><span class="sxs-lookup"><span data-stu-id="aba05-405">The *RemoteAttribute* class's *Fields* property caused some confusion among users.</span></span> <span data-ttu-id="aba05-406">將此屬性重新命名為*AdditionalFields* ，表示其意圖。</span><span class="sxs-lookup"><span data-stu-id="aba05-406">Renaming this property to *AdditionalFields* clarifies its intent.</span></span>

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a><span data-ttu-id="aba05-407">已將 "SkipRequestValidationAttribute" 重新命名為 "AllowHtmlAttribute"</span><span class="sxs-lookup"><span data-stu-id="aba05-407">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>

<span data-ttu-id="aba05-408">*SkipRequestValidationAttribute*屬性已重新命名為*AllowHtmlAttribute* ，以更好的方式表示其預期的使用方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-408">The *SkipRequestValidationAttribute* attribute was renamed to *AllowHtmlAttribute* to better represent its intended usage.</span></span>

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a><span data-ttu-id="aba05-409">已將 "ValidationMessage" 方法變更為顯示第一個有用的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="aba05-409">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>

<span data-ttu-id="aba05-410">已修正*ValidationMessage*方法來顯示第一個有用的錯誤訊息，而不是只顯示第一個錯誤。</span><span class="sxs-lookup"><span data-stu-id="aba05-410">The *Html.ValidationMessage* method was fixed to show the first useful error message instead of simply displaying the first error.</span></span>

<span data-ttu-id="aba05-411">在模型系結期間，可以從多個來源填入*ModelState*字典，其中包含有關屬性的錯誤訊息，包括從模型本身（如果它會執行*IValidatableObject*）、從套用至屬性的驗證屬性，以及存取屬性時擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="aba05-411">During model binding, the *ModelState* dictionary can be populated from multiple sources with error messages about the property, including from the model itself (if it implements *IValidatableObject*), from validation attributes applied to the property, and from exceptions thrown while the property is being accessed.</span></span>

<span data-ttu-id="aba05-412">當*ValidationMessage*方法顯示驗證訊息時，它會略過包含例外狀況的模型狀態專案，因為這通常不是供使用者使用。</span><span class="sxs-lookup"><span data-stu-id="aba05-412">When the *Html.ValidationMessage* method displays a validation message, it skips model-state entries that include an exception, because these are generally not intended for the end user.</span></span> <span data-ttu-id="aba05-413">相反地，方法會尋找未與例外狀況相關聯的第一個驗證訊息，並顯示該訊息。</span><span class="sxs-lookup"><span data-stu-id="aba05-413">Instead, the method looks for the first validation message that is not associated with an exception and displays that message.</span></span> <span data-ttu-id="aba05-414">如果找不到這類訊息，則會預設為與第一個例外狀況相關聯的一般錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="aba05-414">If no such message is found, it defaults to a generic error message that is associated with the first exception.</span></span>

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a><span data-ttu-id="aba05-415">已修正 @model 宣告，不要在檔中加入空白字元</span><span class="sxs-lookup"><span data-stu-id="aba05-415">Fixed @model Declaration to not Add Whitespace to the Document</span></span>

<span data-ttu-id="aba05-416">在舊版中，在視圖頂端的 `@model` 宣告，已將空白行新增至轉譯的 HTML 輸出。</span><span class="sxs-lookup"><span data-stu-id="aba05-416">In earlier releases, the `@model` declaration at the top of a view added a blank line to the rendered HTML output.</span></span> <span data-ttu-id="aba05-417">已修正此問題，因此宣告不會引進空白字元。</span><span class="sxs-lookup"><span data-stu-id="aba05-417">This has been fixed so that the declaration does not introduce whitespace.</span></span>

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a><span data-ttu-id="aba05-418">已新增 "Microsoft.extensions.configuration fileextensions" 屬性來查看引擎，以支援引擎特定的檔案名</span><span class="sxs-lookup"><span data-stu-id="aba05-418">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>

<span data-ttu-id="aba05-419">視圖引擎可以使用明確的視圖路徑來傳回視圖，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-419">A view engine can return a view using an explicit view path as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

<span data-ttu-id="aba05-420">第一個 view 引擎一律會嘗試呈現視圖。</span><span class="sxs-lookup"><span data-stu-id="aba05-420">The first view engine always attempts to render the view.</span></span> <span data-ttu-id="aba05-421">根據預設，Web form view engine 是第一個 view 引擎;因為 Web 表單引擎無法轉譯 Razor 視圖，所以會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="aba05-421">By default, the Web Forms view engine is the first view engine; because the Web Forms engine cannot render a Razor view, an error occurs.</span></span> <span data-ttu-id="aba05-422">View engine 現在有一個*microsoft.extensions.configuration fileextensions*屬性，用來指定支援的副檔名。</span><span class="sxs-lookup"><span data-stu-id="aba05-422">View engines now have a *FileExtensions* property that is used to specify which file extensions they support.</span></span> <span data-ttu-id="aba05-423">當 ASP.NET 判斷視圖引擎是否可以轉譯檔案時，會檢查這個屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-423">This property is checked when ASP.NET determines whether a view engine can render a file.</span></span> <span data-ttu-id="aba05-424">這是一項重大變更，此檔的[重大變更](#_Toc2_BC)一節包含更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aba05-424">This is a breaking change and more details are included in the [Breaking Changes](#_Toc2_BC) section of this document.</span></span>

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a><span data-ttu-id="aba05-425">已修正 "LabelFor" Helper 以發出 "For" 屬性的正確值</span><span class="sxs-lookup"><span data-stu-id="aba05-425">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>

<span data-ttu-id="aba05-426">修正了 bug，其中*LabelFor*方法呈現了符合*輸入*專案之*name*屬性（而非其 ID）的*for*屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-426">A bug was fixed where the *LabelFor* method rendered a *for* attribute that matches the *input* element's *name* attribute instead of its ID.</span></span> <span data-ttu-id="aba05-427">根據 W3C， *for*屬性應符合*輸入*元素的識別碼。</span><span class="sxs-lookup"><span data-stu-id="aba05-427">According to the W3C, the *for* attribute should match the *input* element's ID.</span></span>

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a><span data-ttu-id="aba05-428">已修正 "RenderAction" 方法，以在模型系結期間提供明確值的優先順序</span><span class="sxs-lookup"><span data-stu-id="aba05-428">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>

<span data-ttu-id="aba05-429">在舊版中，傳遞至*RenderAction*方法的明確值，會在子動作內的模型系結期間忽略目前的表單值。</span><span class="sxs-lookup"><span data-stu-id="aba05-429">In earlier versions, explicit values that were passed to the *RenderAction* method were being ignored in favor of the current form values during model binding inside a child action.</span></span> <span data-ttu-id="aba05-430">修正可確保明確的值在模型系結期間會優先。</span><span class="sxs-lookup"><span data-stu-id="aba05-430">The fix ensures that explicit values take precedence during model binding.</span></span>

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="aba05-431">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-431">Breaking Changes</span></span>

- <span data-ttu-id="aba05-432">在舊版的 ASP.NET MVC 中，除了少數情況以外，每個要求都會建立動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="aba05-432">In previous versions of ASP.NET MVC, action filters were created per request except in a few cases.</span></span> <span data-ttu-id="aba05-433">這種行為絕對不是保證的行為，而是只有執行詳細資料，而篩選準則的合約是將其視為無狀態。</span><span class="sxs-lookup"><span data-stu-id="aba05-433">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="aba05-434">在 ASP.NET MVC 3 中，篩選會更積極地快取。</span><span class="sxs-lookup"><span data-stu-id="aba05-434">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="aba05-435">因此，任何不正確儲存實例狀態的自訂動作篩選可能會中斷。</span><span class="sxs-lookup"><span data-stu-id="aba05-435">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="aba05-436">例外狀況篩選準則的執行順序已針對具有相同*順序*值的例外狀況篩選準則進行變更。</span><span class="sxs-lookup"><span data-stu-id="aba05-436">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="aba05-437">在 ASP.NET MVC 2 和更早版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其*順序*值與動作方法上的相同。</span><span class="sxs-lookup"><span data-stu-id="aba05-437">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* value as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="aba05-438">這通常是未使用指定的*順序*值來套用例外狀況篩選時的情況。</span><span class="sxs-lookup"><span data-stu-id="aba05-438">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="aba05-439">在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。</span><span class="sxs-lookup"><span data-stu-id="aba05-439">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="aba05-440">如同在舊版中，如果已明確指定*order*屬性，則會以指定的循序執行篩選。</span><span class="sxs-lookup"><span data-stu-id="aba05-440">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="aba05-441">已將名為*microsoft.extensions.configuration fileextensions*的新屬性新增至*VirtualPathProviderViewEngine*基類。</span><span class="sxs-lookup"><span data-stu-id="aba05-441">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="aba05-442">當 ASP.NET 依路徑（而不是名稱）查詢檢視時，只會考慮包含在此新屬性所指定清單中具有副檔名的 views。</span><span class="sxs-lookup"><span data-stu-id="aba05-442">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="aba05-443">這是應用程式的重大變更，其中已註冊自訂群組建提供者以啟用 Web 表單檢視的自訂副檔名，以及提供者使用完整路徑（而非名稱）來參考這些視圖。</span><span class="sxs-lookup"><span data-stu-id="aba05-443">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="aba05-444">解決方法是修改*microsoft.extensions.configuration fileextensions*屬性的值，以包含自訂副檔名。</span><span class="sxs-lookup"><span data-stu-id="aba05-444">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="aba05-445">直接執行*IControllerFactory*介面的自訂控制器 factory 預建必須提供新*GetControllerSessionBehavior*方法的實作為，這會在此版本中新增至介面。</span><span class="sxs-lookup"><span data-stu-id="aba05-445">Custom controller factory implementations that directly implement the *IControllerFactory* interface must provide an implementation of the new *GetControllerSessionBehavior* method that was added to the interface in this release.</span></span> <span data-ttu-id="aba05-446">一般來說，建議您不要直接執行此介面，而改為從*DefaultControllerFactory*衍生您的類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-446">In general, it is recommended that you do not implement this interface directly and instead derive your class from *DefaultControllerFactory*.</span></span>

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a><span data-ttu-id="aba05-447">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-447">Known Issues</span></span>

- <span data-ttu-id="aba05-448">ASP.NET MVC 3 安裝程式只可以安裝 NuGet 套件管理員的初始版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-448">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="aba05-449">安裝初始版本之後，您可以使用 Visual Studio 擴充管理員來安裝和更新 NuGet。</span><span class="sxs-lookup"><span data-stu-id="aba05-449">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="aba05-450">如果您已安裝 NuGet，請移至 Visual Studio 擴充功能庫，以更新為最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="aba05-450">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="aba05-451">在方案資料夾中建立新的 ASP.NET MVC 3 專案會造成*NullReferenceException*錯誤。</span><span class="sxs-lookup"><span data-stu-id="aba05-451">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="aba05-452">因應措施是在方案的根目錄中建立 ASP.NET MVC 3 專案，然後將它移至方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="aba05-452">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="aba05-453">安裝程式所需的時間可能比先前版本的 ASP.NET MVC 還長，因此無法完成。</span><span class="sxs-lookup"><span data-stu-id="aba05-453">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="aba05-454">這是因為它會更新 Visual Studio 2010 的元件。</span><span class="sxs-lookup"><span data-stu-id="aba05-454">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="aba05-455">電腦若有安裝 ReSharper，Razor 語法的 IntelliSense 即無法運作。</span><span class="sxs-lookup"><span data-stu-id="aba05-455">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="aba05-456">如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 RC2 中的 Razor IntelliSense 支援，請參閱 Hadi Hariri 的 blog 中的專案[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中會討論今日使用它們的方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-456">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3 RC2, see the entry [Razor Intellisense and ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="aba05-457">以 ASP.NET MVC 3 的 Beta 版建立的 CSHTML 和 VBHTML views 並未正確設定其組建動作，結果是在發行專案時，會省略這些檢視類型。</span><span class="sxs-lookup"><span data-stu-id="aba05-457">CSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="aba05-458">這些檔案的 [*組建動作*] 值應該設定為 [內容]。</span><span class="sxs-lookup"><span data-stu-id="aba05-458">The *Build Action* value for these files should be set to Content".</span></span> <span data-ttu-id="aba05-459">ASP.NET MVC 3 RC2 會修正新檔案的這個問題，但不會更正以 Beta 版所建立之專案的現有檔案設定。![](mvc3-release-notes/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="aba05-459">ASP.NET MVC 3 RC2 fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta version.![](mvc3-release-notes/_static/image4.png)</span></span>
- <span data-ttu-id="aba05-460">在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。</span><span class="sxs-lookup"><span data-stu-id="aba05-460">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="aba05-461">當您編輯 Razor view （cshtml 檔案）時，Visual Studio 中的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="aba05-461">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="aba05-462">如果您在未安裝 Visual Studio 的電腦上安裝 ASP.NET MVC 3 for Visual Web Developer Express，然後在稍後安裝 Visual Studio，則必須重新安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="aba05-462">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="aba05-463">Visual Studio 和 Visual Web Developer Express 共用 ASP.NET MVC 3 安裝程式所升級的元件。</span><span class="sxs-lookup"><span data-stu-id="aba05-463">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="aba05-464">如果您在沒有 Visual Web Developer Express 的電腦上安裝 ASP.NET MVC Visual Studio 3，然後再安裝 Visual Web Developer Express，則適用相同的問題。</span><span class="sxs-lookup"><span data-stu-id="aba05-464">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>
- <span data-ttu-id="aba05-465">如果您已安裝 ASP.NET MVC 3 RC 2，則不會更新 NuGet。</span><span class="sxs-lookup"><span data-stu-id="aba05-465">Installing ASP.NET MVC 3 RC 2 does not update NuGet if you already have it installed.</span></span> <span data-ttu-id="aba05-466">若要升級 NuGet，請移至 Visual Studio 擴充管理員，它應該會顯示為可用的更新。</span><span class="sxs-lookup"><span data-stu-id="aba05-466">To upgrade NuGet, go to the Visual Studio Extension manager and it should show up as an available update.</span></span> <span data-ttu-id="aba05-467">您可以從該處將 NuGet 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-467">You can upgrade NuGet to the latest release from there.</span></span>

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a><span data-ttu-id="aba05-468">ASP.NET MVC 3 發行候選版本</span><span class="sxs-lookup"><span data-stu-id="aba05-468">ASP.NET MVC 3 Release Candidate</span></span>

<span data-ttu-id="aba05-469">ASP.NET MVC 發行候選版本已于2010年11月9日發行。</span><span class="sxs-lookup"><span data-stu-id="aba05-469">ASP.NET MVC Release Candidate was released on November 9, 2010.</span></span>

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a><span data-ttu-id="aba05-470">ASP.NET MVC 3 RC 中的新功能</span><span class="sxs-lookup"><span data-stu-id="aba05-470">New Features in ASP.NET MVC 3 RC</span></span>

<span data-ttu-id="aba05-471">本節說明自 Beta 版以來，已在 ASP.NET MVC 3 RC 版本中引進的功能。</span><span class="sxs-lookup"><span data-stu-id="aba05-471">This section describes features that have been introduced in the ASP.NET MVC 3 RC release since the Beta release.</span></span>

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a><span data-ttu-id="aba05-472">NuGet 封裝管理員</span><span class="sxs-lookup"><span data-stu-id="aba05-472">NuGet Package Manager</span></span>

<span data-ttu-id="aba05-473">ASP.NET MVC 3 包含 NuGet 套件管理員（之前稱為 NuPack），這是整合的封裝管理工具，可用來將程式庫和工具新增至 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="aba05-473">ASP.NET MVC 3 includes the NuGet Package Manager (formerly known as NuPack), which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="aba05-474">這種工具可讓開發人員立即採取的步驟，將程式庫帶入其來源樹狀結構中。</span><span class="sxs-lookup"><span data-stu-id="aba05-474">This tool automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="aba05-475">您可以使用 NuGet 做為命令列工具，作為 Visual Studio 2010 內的整合式主控台視窗，從 [Visual Studio] 內容功能表，以及一組 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="aba05-475">You can work with NuGet as a command-line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as a set of PowerShell cmdlets.</span></span>

<span data-ttu-id="aba05-476">如需 NuGet 的詳細資訊，請參閱[Nuget 檔](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="aba05-476">For more information about NuGet, read the [Nuget Documentation](https://docs.microsoft.com/nuget/).</span></span>

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a><span data-ttu-id="aba05-477">改良的 [新增專案] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="aba05-477">Improved "New Project" Dialog Box</span></span>

<span data-ttu-id="aba05-478">當您建立新的專案時，[新增專案] 對話方塊現在可讓您指定 view engine 以及 ASP.NET MVC 專案類型。</span><span class="sxs-lookup"><span data-stu-id="aba05-478">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image5.png)

<span data-ttu-id="aba05-479">此版本包含修改範本清單和對話方塊中所列之視圖引擎的支援。</span><span class="sxs-lookup"><span data-stu-id="aba05-479">Support for modifying the list of templates and view engines listed in the dialog box is included in this release.</span></span>

<span data-ttu-id="aba05-480">預設範本如下所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-480">The default templates are the following:</span></span>

<span data-ttu-id="aba05-481">空白。</span><span class="sxs-lookup"><span data-stu-id="aba05-481">Empty.</span></span> <span data-ttu-id="aba05-482">包含 ASP.NET MVC 專案的最小檔案集，包括 ASP.NET MVC 專案的預設目錄結構、包含預設 ASP.NET MVC 樣式的 .css 檔案，以及包含預設 JavaScript 檔案的腳本目錄。</span><span class="sxs-lookup"><span data-stu-id="aba05-482">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="aba05-483">網際網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="aba05-483">Internet Application.</span></span> <span data-ttu-id="aba05-484">包含範例功能，示範如何搭配使用成員資格提供者與 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="aba05-484">Contains sample functionality that demonstrates how to use the membership provider with ASP.NET MVC.</span></span>

<span data-ttu-id="aba05-485">對話方塊中顯示的專案範本清單會在 Windows 登錄中指定。</span><span class="sxs-lookup"><span data-stu-id="aba05-485">The list of project templates that is displayed in the dialog box is specified in the Windows registry.</span></span>

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a><span data-ttu-id="aba05-486">無會話控制器</span><span class="sxs-lookup"><span data-stu-id="aba05-486">Sessionless Controllers</span></span>

<span data-ttu-id="aba05-487">新的*ControllerSessionStateAttribute*會藉由指定[SessionState SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx)列舉值，讓您更充分掌控控制器的會話狀態行為。</span><span class="sxs-lookup"><span data-stu-id="aba05-487">The new *ControllerSessionStateAttribute* gives you more control over session-state behavior for controllers by specifying a [System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) enumeration value.</span></span>

<span data-ttu-id="aba05-488">下列範例顯示如何關閉對控制器之所有要求的會話狀態。</span><span class="sxs-lookup"><span data-stu-id="aba05-488">The following example shows how to turn off session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

<span data-ttu-id="aba05-489">下列範例顯示如何設定對控制器之所有要求的唯讀會話狀態。</span><span class="sxs-lookup"><span data-stu-id="aba05-489">The following example shows how to set read-only session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a><span data-ttu-id="aba05-490">新的驗證屬性</span><span class="sxs-lookup"><span data-stu-id="aba05-490">New Validation Attributes</span></span>

#### <a name="compareattribute"></a><span data-ttu-id="aba05-491">CompareAttribute</span><span class="sxs-lookup"><span data-stu-id="aba05-491">CompareAttribute</span></span>

<span data-ttu-id="aba05-492">新的*CompareAttribute*驗證屬性可讓您比較模型中兩個不同屬性的值。</span><span class="sxs-lookup"><span data-stu-id="aba05-492">The new *CompareAttribute* validation attribute lets you compare the values of two different properties of a model.</span></span> <span data-ttu-id="aba05-493">在下列範例中， *ComparePassword*屬性必須符合*密碼*欄位，才會生效。</span><span class="sxs-lookup"><span data-stu-id="aba05-493">In the following example, the *ComparePassword* property must match the *Password* field in order to be valid.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a><span data-ttu-id="aba05-494">RemoteAttribute</span><span class="sxs-lookup"><span data-stu-id="aba05-494">RemoteAttribute</span></span>

<span data-ttu-id="aba05-495">新的*RemoteAttribute*驗證屬性會利用 jQuery 驗證外掛程式的遠端驗證程式，這可讓用戶端驗證在執行實際驗證邏輯的伺服器上呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="aba05-495">The new *RemoteAttribute* validation attribute takes advantage of the jQuery Validation plug-in's remote validator, which enables client-side validation to call a method on the server that performs the actual validation logic.</span></span>

<span data-ttu-id="aba05-496">在下列範例中， *UserName*屬性已套用*RemoteAttribute* 。</span><span class="sxs-lookup"><span data-stu-id="aba05-496">In the following example, the *UserName* property has the *RemoteAttribute* applied.</span></span> <span data-ttu-id="aba05-497">在編輯檢視中編輯此屬性時，用戶端驗證會在*UsersController*類別上呼叫名為*UserNameAvailable*的動作，以便驗證此欄位。</span><span class="sxs-lookup"><span data-stu-id="aba05-497">When editing this property in an Edit view, client validation will call an action named *UserNameAvailable* on the *UsersController* class in order to validate this field.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

<span data-ttu-id="aba05-498">下列範例會顯示對應的控制器。</span><span class="sxs-lookup"><span data-stu-id="aba05-498">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

<span data-ttu-id="aba05-499">根據預設，套用屬性的屬性名稱會以查詢字串參數的形式傳送至動作方法。</span><span class="sxs-lookup"><span data-stu-id="aba05-499">By default, the property name that the attribute is applied to is sent to the action method as a query-string parameter.</span></span>

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a><span data-ttu-id="aba05-500">"LabelFor" 和 "LabelForModel" 方法的新多載</span><span class="sxs-lookup"><span data-stu-id="aba05-500">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>

<span data-ttu-id="aba05-501">已新增*LabelFor*和*LabelForModel*方法的新多載，可讓您指定標籤文字。</span><span class="sxs-lookup"><span data-stu-id="aba05-501">New overloads have been added for the *LabelFor* and *LabelForModel* methods that let you specify the label text.</span></span> <span data-ttu-id="aba05-502">下列範例顯示如何使用這些多載。</span><span class="sxs-lookup"><span data-stu-id="aba05-502">The following example shows how to use these overloads.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a><span data-ttu-id="aba05-503">子動作輸出快取</span><span class="sxs-lookup"><span data-stu-id="aba05-503">Child Action Output Caching</span></span>

<span data-ttu-id="aba05-504">*OutputCacheAttribute*支援使用*RenderAction*或*html. 動作*協助程式方法所呼叫之子動作的輸出快取。</span><span class="sxs-lookup"><span data-stu-id="aba05-504">The *OutputCacheAttribute* supports output caching of child actions that are called by using the *Html.RenderAction* or *Html.Action* helper methods.</span></span> <span data-ttu-id="aba05-505">下列範例顯示呼叫另一個動作的視圖。</span><span class="sxs-lookup"><span data-stu-id="aba05-505">The following example shows a view that calls another action.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

<span data-ttu-id="aba05-506">*GetDate*動作會以*OutputCacheAttribute*標注：</span><span class="sxs-lookup"><span data-stu-id="aba05-506">The *GetDate* action is annotated with the *OutputCacheAttribute*:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

<span data-ttu-id="aba05-507">當此程式碼執行時，會快取呼叫 Html. Action （"GetDate"）的結果100秒。</span><span class="sxs-lookup"><span data-stu-id="aba05-507">When this code runs, the result of the call to Html.Action("GetDate") is cached for 100 seconds.</span></span>

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a><span data-ttu-id="aba05-508">[加入視圖] 對話方塊的改善</span><span class="sxs-lookup"><span data-stu-id="aba05-508">"Add View" Dialog Box Improvements</span></span>

<span data-ttu-id="aba05-509">當您加入強型別視圖時，[加入視圖] 對話方塊現在會篩選出比舊版更不適用的類型，例如許多核心 .NET Framework 類型。</span><span class="sxs-lookup"><span data-stu-id="aba05-509">When you add a strongly typed view, the Add View dialog box now filters out more non-applicable types than in previous releases, such as many core .NET Framework types.</span></span> <span data-ttu-id="aba05-510">此外，此清單現在會依類別名稱排序，而不是完整的類型名稱，讓您更輕鬆地尋找類型。</span><span class="sxs-lookup"><span data-stu-id="aba05-510">Also, the list is now sorted by the class name and not by the fully qualified type name, which makes it easier to find types.</span></span> <span data-ttu-id="aba05-511">例如，現在會顯示類型名稱，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-511">For example, the type name is now displayed as in the following example:</span></span>

<span data-ttu-id="aba05-512">ClassName （命名空間）</span><span class="sxs-lookup"><span data-stu-id="aba05-512">ClassName (namespace)</span></span>

<span data-ttu-id="aba05-513">在先前的版本中，這會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="aba05-513">In earlier releases, this would have been displayed as the following:</span></span>

<span data-ttu-id="aba05-514">Namespace. ClassName</span><span class="sxs-lookup"><span data-stu-id="aba05-514">Namespace.ClassName</span></span>

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a><span data-ttu-id="aba05-515">細微要求驗證</span><span class="sxs-lookup"><span data-stu-id="aba05-515">Granular Request Validation</span></span>

<span data-ttu-id="aba05-516">*Validateinputattribute 套用*的*Exclude*屬性不再存在。</span><span class="sxs-lookup"><span data-stu-id="aba05-516">The *Exclude* property of *ValidateInputAttribute* no longer exists.</span></span> <span data-ttu-id="aba05-517">相反地，若要在模型系結期間略過模型特定屬性的要求驗證，請使用新的*SkipRequestValidationAttribute*。</span><span class="sxs-lookup"><span data-stu-id="aba05-517">Instead, to have request validation skipped for specific properties of a model during model binding, use the new *SkipRequestValidationAttribute*.</span></span>

<span data-ttu-id="aba05-518">例如，假設有一個動作方法用來編輯 blog 文章：</span><span class="sxs-lookup"><span data-stu-id="aba05-518">For example, suppose an action method is used to edit a blog post:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

<span data-ttu-id="aba05-519">下列範例顯示 blog 文章的視圖模型。</span><span class="sxs-lookup"><span data-stu-id="aba05-519">The following example shows the view model for a blog post.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

<span data-ttu-id="aba05-520">當使用者提交 Description 屬性的某些標記時，模型系結會因為要求驗證而失敗。</span><span class="sxs-lookup"><span data-stu-id="aba05-520">When a user submits some markup for the Description property, model binding will fail due to request validation.</span></span> <span data-ttu-id="aba05-521">若要在進行 blog 文章描述的模型系結期間停用要求驗證，請將*SkipRequpestValidationAttribute*套用至屬性，如下列範例所示：。</span><span class="sxs-lookup"><span data-stu-id="aba05-521">To disable request validation during model binding for the blog post Description, apply the *SkipRequpestValidationAttribute* to the property, as shown in this example:.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

<span data-ttu-id="aba05-522">或者，若要關閉模型的每個屬性的要求驗證，請將值為*false*的*validateinputattribute 套用*套用至動作方法：</span><span class="sxs-lookup"><span data-stu-id="aba05-522">Alternatively, to turn off request validation for every property of the model, apply *ValidateInputAttribute* with a value of *false* to the action method:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a><span data-ttu-id="aba05-523">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-523">Breaking Changes</span></span>

- <span data-ttu-id="aba05-524">例外狀況篩選準則的執行順序已針對具有相同*順序*值的例外狀況篩選準則進行變更。</span><span class="sxs-lookup"><span data-stu-id="aba05-524">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="aba05-525">在 ASP.NET MVC 2 和更早版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其*順序*與動作方法上的相同。</span><span class="sxs-lookup"><span data-stu-id="aba05-525">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="aba05-526">這通常是未使用指定的*順序*值來套用例外狀況篩選時的情況。</span><span class="sxs-lookup"><span data-stu-id="aba05-526">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="aba05-527">在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。</span><span class="sxs-lookup"><span data-stu-id="aba05-527">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="aba05-528">如同在舊版中，如果已明確指定*order*屬性，則會以指定的循序執行篩選。</span><span class="sxs-lookup"><span data-stu-id="aba05-528">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="aba05-529">將名為*microsoft.extensions.configuration fileextensions*的新屬性新增至*VirtualPathProviderViewEngine*基類。</span><span class="sxs-lookup"><span data-stu-id="aba05-529">Added a new property named *FileExtensions* to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="aba05-530">依路徑（而不是依名稱）查閱 view 時，只會考慮使用此新屬性所指定之清單中包含副檔名的 views。</span><span class="sxs-lookup"><span data-stu-id="aba05-530">When looking up a view by path (and not by name), only views with a file extension contained in the list specified by this new property is considered.</span></span> <span data-ttu-id="aba05-531">這是針對註冊自訂群組建提供者以啟用 web 表單檢視之自訂副檔名，並使用完整路徑（而非名稱）來參考這些視圖的使用者的重大變更。</span><span class="sxs-lookup"><span data-stu-id="aba05-531">This is a breaking change for those who register a custom build provider to enable a custom file extension for web form views and are referencing those views by using a full path rather than a name.</span></span> <span data-ttu-id="aba05-532">解決方法是修改*microsoft.extensions.configuration fileextensions*屬性的值，以包含自訂副檔名。</span><span class="sxs-lookup"><span data-stu-id="aba05-532">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>

<a id="_Toc276711795"></a>
## <a name="known-issues"></a><span data-ttu-id="aba05-533">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-533">Known Issues</span></span>

- <span data-ttu-id="aba05-534">安裝程式所需的時間可能比舊版的 ASP.NET MVC 更長，因為它會更新 Visual Studio 2010 的元件。</span><span class="sxs-lookup"><span data-stu-id="aba05-534">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="aba05-535">選取 astrongly 具類型的 view scaffold 僅限寫入屬性時的加入視圖。</span><span class="sxs-lookup"><span data-stu-id="aba05-535">The Add View scaffolding when selecting astrongly typed view scaffolds write-only properties.</span></span> <span data-ttu-id="aba05-536">這些樣板應一律予以忽略。</span><span class="sxs-lookup"><span data-stu-id="aba05-536">These should always be ignored by scaffolding.</span></span> <span data-ttu-id="aba05-537">當產生「編輯」或「建立」視圖時，[加入視圖] 對話方塊也會 scaffold 唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-537">The Add View dialog also scaffolds read-only properties when generating an "Edit" or "Create" view.</span></span> <span data-ttu-id="aba05-538">唯讀屬性只應針對顯示和列出視圖進行 scaffold。</span><span class="sxs-lookup"><span data-stu-id="aba05-538">Read-only properties should only be scaffolded for the Display and List views.</span></span>
- <span data-ttu-id="aba05-539">當 ASP.NET MVC 3 與非同步 CTP 一起安裝時，不能進行調試。</span><span class="sxs-lookup"><span data-stu-id="aba05-539">Debugging doesn't work when ASP.NET MVC 3 is installed alongside the Async CTP.</span></span> <span data-ttu-id="aba05-540">ASP.NET MVC 3 無法與非同步 CTP 並存安裝。</span><span class="sxs-lookup"><span data-stu-id="aba05-540">ASP.NET MVC 3 cannot be installed side-by-side with the Async CTP.</span></span> <span data-ttu-id="aba05-541">卸載非同步 CTP 以修復調試。</span><span class="sxs-lookup"><span data-stu-id="aba05-541">Uninstall the Async CTP to repair debugging.</span></span> <span data-ttu-id="aba05-542">如需詳細資訊，請閱讀[這篇](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html)關於卸載 ASP.NET MVC 3 RC 所有部分的文章。</span><span class="sxs-lookup"><span data-stu-id="aba05-542">For more details, read [this blog post](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) about uninstalling all the pieces of ASP.NET MVC 3 RC.</span></span>
- <span data-ttu-id="aba05-543">安裝 Resharper 時，Razor Intellisense 無法運作。</span><span class="sxs-lookup"><span data-stu-id="aba05-543">Razor Intellisense does not work when Resharper is installed.</span></span> <span data-ttu-id="aba05-544">如果您已安裝 ReSharper，而且想要利用 ASP.NET MVC 3 RC 中的 Razor intellisense 支援，請閱讀來自 JetBrains 的[這篇 blog 文章](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)，其中會討論今天使用這些專案的方法。</span><span class="sxs-lookup"><span data-stu-id="aba05-544">If you have ReSharper installed and want to take advantage of the Razor intellisense support in ASP.NET MVC 3 RC, please read [this blog post](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) from JetBrains which discusses ways to use them together today.</span></span>
- <span data-ttu-id="aba05-545">以 ASP.NET MVC 3 搶鮮版建立的 CSHTML 和 VBHTML views，其組建動作不會正確地使其無法發行。</span><span class="sxs-lookup"><span data-stu-id="aba05-545">CSHTML and VBHTML views created with Beta of ASP.NET MVC 3 do not have their build action correctly which omits them from publishing.</span></span> <span data-ttu-id="aba05-546">這些檔案的*組建動作*應設定為 [內容]。</span><span class="sxs-lookup"><span data-stu-id="aba05-546">The *Build Action* for these files should be set to "Content".</span></span> <span data-ttu-id="aba05-547">ASP.NET MVC 3 RC 會針對新檔案修正此問題，但不會更正以 Beta 版所建立之專案的現有檔案設定。</span><span class="sxs-lookup"><span data-stu-id="aba05-547">ASP.NET MVC 3 RC fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta.</span></span>
- <span data-ttu-id="aba05-548">安裝程式所需的時間可能比舊版的 ASP.NET MVC 更長，因為它會更新 Visual Studio 2010 的元件。</span><span class="sxs-lookup"><span data-stu-id="aba05-548">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="aba05-549">選取 [編輯] [強型別視圖] scaffold 唯讀屬性時的 [加入視圖] 樣板。</span><span class="sxs-lookup"><span data-stu-id="aba05-549">The Add View scaffolding when selecting an "Edit" strongly typed view scaffolds read only properties.</span></span> <span data-ttu-id="aba05-550">同樣地，[顯示] 視圖也會 scaffold 僅限寫入的屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-550">Likewise, write-only properties are scaffolded for "Display" views.</span></span>
- <span data-ttu-id="aba05-551">在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。</span><span class="sxs-lookup"><span data-stu-id="aba05-551">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="aba05-552">安裝 Visual Studio 非同步 CTP 會與 ASP.NET MVC 3 工具安裝中包含的 Razor 版本發生衝突。</span><span class="sxs-lookup"><span data-stu-id="aba05-552">Installing the Visual Studio Async CTP causes a conflict with the Razor release that is included as part of the ASP.NET MVC 3 tooling installation.</span></span> <span data-ttu-id="aba05-553">請確定您未嘗試在同一部電腦上安裝 Visual Studio 非同步 CTP 和 Razor 版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-553">Make sure that you do not try to install both the Visual Studio Async CTP and the Razor release on the same machine.</span></span>
- <span data-ttu-id="aba05-554">當您編輯 Razor view （cshtml 檔案）時，Visual Studio 中的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="aba05-554">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a><span data-ttu-id="aba05-555">ASP.NET MVC 3 Beta</span><span class="sxs-lookup"><span data-stu-id="aba05-555">ASP.NET MVC 3 Beta</span></span>

<span data-ttu-id="aba05-556">ASP.NET MVC 3 Beta 已于2010年10月6日發行。</span><span class="sxs-lookup"><span data-stu-id="aba05-556">ASP.NET MVC 3 Beta was released on October 6, 2010.</span></span> <span data-ttu-id="aba05-557">下列是 Beta 版特有的附注，受限於上述 ASP.NET MVC 3 發行候選章節中所參考的任何更新或變更。</span><span class="sxs-lookup"><span data-stu-id="aba05-557">The following notes are specific to the Beta release, and are subject to any updates or changes referenced in the ASP.NET MVC 3 Release Candidate section above.</span></span>

## <a id="0.1__Toc274034215"></a><span data-ttu-id="aba05-558">新的 Featuresin ASP.NET MVC 3 Beta</span><span class="sxs-lookup"><span data-stu-id="aba05-558">New Featuresin ASP.NET MVC 3 Beta</span></span>

<a id="0.1__Default_validation_system"></a><span data-ttu-id="aba05-559">本節說明 ASP.NET MVC 3 Beta 版本中引進的功能。</span><span class="sxs-lookup"><span data-stu-id="aba05-559">This section describes features that have been introduced in the ASP.NET MVC 3 Beta release.</span></span>

### <a id="0.1__Toc274034216"></a><span data-ttu-id="aba05-560">NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="aba05-560">NuGet Package Manager</span></span>

<span data-ttu-id="aba05-561">ASP.NET MVC 3 包含 NuGet 套件管理員，這是一個整合的封裝管理工具，可用來將程式庫和工具新增至 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="aba05-561">ASP.NET MVC 3 includes NuGet Package Manager, which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="aba05-562">在大部分的情況下，它會將開發人員立即採取的步驟自動化，以將程式庫帶入其來源樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="aba05-562">For the most part, it automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="aba05-563">您可以使用 NuGet 做為命令列工具，做為 Visual Studio 2010 內的整合式主控台視窗，從 [Visual Studio] 內容功能表，以及一組 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="aba05-563">You can work with NuGet as a command line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as set of PowerShell cmdlets.</span></span>

<span data-ttu-id="aba05-564">如需 NuGet 的詳細資訊，請參閱[Nuget 檔](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="aba05-564">For more information about NuGet, read the [NuGet Documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a id="0.1__Toc274034217"></a><span data-ttu-id="aba05-565">改良的 [新增專案] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="aba05-565">Improved New Project Dialog Box</span></span>

<span data-ttu-id="aba05-566">當您建立新的專案時，[新增專案] 對話方塊現在可讓您指定 view engine 以及 ASP.NET MVC 專案類型。</span><span class="sxs-lookup"><span data-stu-id="aba05-566">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image6.png)

<span data-ttu-id="aba05-567">此版本不包含修改對話方塊中所列的範本清單和視圖引擎的支援。</span><span class="sxs-lookup"><span data-stu-id="aba05-567">Support for modifying the list of templates and view engines listed in the dialog box is not included in this release.</span></span>

<span data-ttu-id="aba05-568">預設範本如下所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-568">The default templates are the following:</span></span>

<span data-ttu-id="aba05-569">空白。</span><span class="sxs-lookup"><span data-stu-id="aba05-569">Empty.</span></span> <span data-ttu-id="aba05-570">包含 ASP.NET MVC 專案的最小檔案集，包括 ASP.NET MVC 專案的預設目錄結構、包含預設 ASP.NET MVC 樣式的小型網站 .css 檔案，以及包含預設 JavaScript 檔案的腳本目錄。</span><span class="sxs-lookup"><span data-stu-id="aba05-570">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a small Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="aba05-571">網際網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="aba05-571">Internet Application.</span></span> <span data-ttu-id="aba05-572">包含範例功能，示範如何在 ASP.NET MVC 中使用成員資格提供者。</span><span class="sxs-lookup"><span data-stu-id="aba05-572">Contains sample functionality that demonstrates how to use the membership provider within ASP.NET MVC.</span></span>

### <a id="0.1__Toc274034218"></a><span data-ttu-id="aba05-573">在 Razor Views 中指定強型別模型的簡化方式</span><span class="sxs-lookup"><span data-stu-id="aba05-573">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>

<span data-ttu-id="aba05-574">為強型別 Razor views 指定模型類型的方法，已經使用適用于 CSHTML views 的新 @model 指示詞和 VBHTML 視圖的 @ModelType 指示詞來簡化。</span><span class="sxs-lookup"><span data-stu-id="aba05-574">The way to specify the model type for strongly typed Razor views has been simplified by using the new @model directive for CSHTML views and @ModelType directive for VBHTML views.</span></span> <span data-ttu-id="aba05-575">在舊版的 ASP.NET MVC 中，您會以這種方式指定 Razor views 的強型別模型：</span><span class="sxs-lookup"><span data-stu-id="aba05-575">In earlier versions of ASP.NET MVC, you would specify a strongly typed model for Razor views this way:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

<span data-ttu-id="aba05-576">在此版本中，您可以使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="aba05-576">In this release, you can use the following syntax:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a><span data-ttu-id="aba05-577">支援新的 ASP.NET Web Pages Helper 方法</span><span class="sxs-lookup"><span data-stu-id="aba05-577">Support for New ASP.NET Web Pages Helper Methods</span></span>

<span data-ttu-id="aba05-578">新的 ASP.NET Web Pages 技術包含一組協助程式方法，適用于將常用的功能新增至視圖和控制器。</span><span class="sxs-lookup"><span data-stu-id="aba05-578">The new ASP.NET Web Pages technology includes a set of helper methods that are useful for adding commonly used functionality to views and controllers.</span></span> <span data-ttu-id="aba05-579">ASP.NET MVC 3 支援在控制器和瀏覽器中使用這些協助程式方法（適當時）。</span><span class="sxs-lookup"><span data-stu-id="aba05-579">ASP.NET MVC 3 supports using these helper methods within controllers and views (where appropriate).</span></span> <span data-ttu-id="aba05-580">這些方法包含在 System.web. helper 元件中。</span><span class="sxs-lookup"><span data-stu-id="aba05-580">These methods are contained in the System.Web.Helpers assembly.</span></span> <span data-ttu-id="aba05-581">下表列出幾個 ASP.NET Web Pages helper 方法。</span><span class="sxs-lookup"><span data-stu-id="aba05-581">The following table lists a few of the ASP.NET Web Pages helper methods.</span></span>

| <span data-ttu-id="aba05-582">**輔助**</span><span class="sxs-lookup"><span data-stu-id="aba05-582">**Helper**</span></span> | <span data-ttu-id="aba05-583">**說明**</span><span class="sxs-lookup"><span data-stu-id="aba05-583">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="aba05-584">圖表</span><span class="sxs-lookup"><span data-stu-id="aba05-584">Chart</span></span> | <span data-ttu-id="aba05-585">呈現視圖中的圖表。</span><span class="sxs-lookup"><span data-stu-id="aba05-585">Renders a chart within a view.</span></span> <span data-ttu-id="aba05-586">包含 ToWebImage、Chart、Save 和 Chart 之類的方法。</span><span class="sxs-lookup"><span data-stu-id="aba05-586">Contains methods such as Chart.ToWebImage, Chart.Save, and Chart.Write.</span></span> |
| <span data-ttu-id="aba05-587">Ipp</span><span class="sxs-lookup"><span data-stu-id="aba05-587">Crypto</span></span> | <span data-ttu-id="aba05-588">會使用雜湊演算法來建立適當的 salted 和雜湊密碼。</span><span class="sxs-lookup"><span data-stu-id="aba05-588">Uses hashing algorithms to create properly salted and hashed passwords.</span></span> |
| <span data-ttu-id="aba05-589">WebGrid</span><span class="sxs-lookup"><span data-stu-id="aba05-589">WebGrid</span></span> | <span data-ttu-id="aba05-590">將物件的集合（通常是資料庫的資料）當做方格呈現。</span><span class="sxs-lookup"><span data-stu-id="aba05-590">Renders a collection of objects (typically, data from a database) as a grid.</span></span> <span data-ttu-id="aba05-591">支援分頁和排序。</span><span class="sxs-lookup"><span data-stu-id="aba05-591">Supports paging and sorting.</span></span> |
| <span data-ttu-id="aba05-592">WebImage</span><span class="sxs-lookup"><span data-stu-id="aba05-592">WebImage</span></span> | <span data-ttu-id="aba05-593">呈現影像。</span><span class="sxs-lookup"><span data-stu-id="aba05-593">Renders an image.</span></span> |
| <span data-ttu-id="aba05-594">WebMail</span><span class="sxs-lookup"><span data-stu-id="aba05-594">WebMail</span></span> | <span data-ttu-id="aba05-595">傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="aba05-595">Sends an email message.</span></span> |

<span data-ttu-id="aba05-596">列出協助程式和基本語法的快速參考主題可在 ASP.NET Razor 語法檔中取得，網址為下列 URL：</span><span class="sxs-lookup"><span data-stu-id="aba05-596">A quick reference topic that lists the helpers and basic syntax is available as part of the ASP.NET Razor syntax documentation at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a><span data-ttu-id="aba05-597">其他相依性插入支援</span><span class="sxs-lookup"><span data-stu-id="aba05-597">Additional Dependency Injection Support</span></span>

<span data-ttu-id="aba05-598">目前的版本是以 ASP.NET MVC 3 Preview 1 版本為基礎，其中包括新增了兩項新服務和四個現有服務的支援，並改善了對相依性解析和一般服務定位器的支援。</span><span class="sxs-lookup"><span data-stu-id="aba05-598">Building on the ASP.NET MVC 3 Preview 1 release, the current release includes added support for two new services and four existing services, and improved support for dependency resolution and the Common Service Locator.</span></span>

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a><span data-ttu-id="aba05-599">用於微調控制器具現化的新 IControllerActivator 介面</span><span class="sxs-lookup"><span data-stu-id="aba05-599">New IControllerActivator Interface for Fine-Grained Controller Instantiation</span></span>

<span data-ttu-id="aba05-600">新的 IControllerActivator 介面可讓您更精細地控制透過相依性插入來具現化控制器的方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-600">The new IControllerActivator interface provides more fine-grained control over how controllers are instantiated via dependency injection.</span></span> <span data-ttu-id="aba05-601">下列範例顯示介面：</span><span class="sxs-lookup"><span data-stu-id="aba05-601">The following example shows the interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

<span data-ttu-id="aba05-602">這與控制器 factory 的角色相反。</span><span class="sxs-lookup"><span data-stu-id="aba05-602">Contrast this to the role of the controller factory.</span></span> <span data-ttu-id="aba05-603">控制器 factory 是 IControllerFactory 介面的實作為，負責尋找控制器類型，以及具現化該控制器類型的實例。</span><span class="sxs-lookup"><span data-stu-id="aba05-603">A controller factory is an implementation of the IControllerFactory interface, which is responsible both for locating a controller type and for instantiating an instance of that controller type.</span></span>

<span data-ttu-id="aba05-604">控制器啟動程式只負責具現化控制器類型的實例。</span><span class="sxs-lookup"><span data-stu-id="aba05-604">Controller activators are responsible only for instantiating an instance of a controller type.</span></span> <span data-ttu-id="aba05-605">它們不會執行控制器類型查閱。</span><span class="sxs-lookup"><span data-stu-id="aba05-605">They do not perform the controller type lookup.</span></span> <span data-ttu-id="aba05-606">找出適當的控制器類型之後，控制器 factory 應委派給 IControllerActivator 的實例，以處理控制器的實際具現化。</span><span class="sxs-lookup"><span data-stu-id="aba05-606">After locating a proper controller type, controller factories should delegate to an instance of IControllerActivator to handle the actual instantiation of the controller.</span></span>

<span data-ttu-id="aba05-607">DefaultControllerFactory 類別具有接受 IControllerFactory 實例的新函式。</span><span class="sxs-lookup"><span data-stu-id="aba05-607">The DefaultControllerFactory class has a new constructor that accepts an IControllerFactory instance.</span></span> <span data-ttu-id="aba05-608">這可讓您套用相依性插入，以管理控制器建立的這個層面，而不需要覆寫預設的控制器類型查閱行為。</span><span class="sxs-lookup"><span data-stu-id="aba05-608">This lets you apply Dependency Injection to manage this aspect of controller creation without having to override the default controller-type lookup behavior.</span></span>

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a><span data-ttu-id="aba05-609">IServiceLocator 介面已取代為 IDependencyResolver</span><span class="sxs-lookup"><span data-stu-id="aba05-609">IServiceLocator Interface Replaced with IDependencyResolver</span></span>

<span data-ttu-id="aba05-610">根據社區的意見反應，ASP.NET MVC 3 Beta 版已將 IServiceLocator 介面的使用取代為 ASP.NET MVC 需求特有的簡式 IDependencyResolver 介面。</span><span class="sxs-lookup"><span data-stu-id="aba05-610">Based on community feedback, the ASP.NET MVC 3 Beta release has replaced the use of the IServiceLocator interface with a slimmed-down IDependencyResolver interface specific to the needs of ASP.NET MVC.</span></span> <span data-ttu-id="aba05-611">下列範例顯示新的介面：</span><span class="sxs-lookup"><span data-stu-id="aba05-611">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

<span data-ttu-id="aba05-612">做為這項變更的一部分，ServiceLocator 類別也會取代為 DependencyResolver 類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-612">As part of this change, the ServiceLocator class was also replaced with the DependencyResolver class.</span></span> <span data-ttu-id="aba05-613">相依性解析程式的註冊類似于舊版的 ASP.NET MVC：</span><span class="sxs-lookup"><span data-stu-id="aba05-613">Registration of a dependency resolver is similar to earlier versions of ASP.NET MVC:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

<span data-ttu-id="aba05-614">此介面的執行應直接委派至基礎相依性插入容器，以提供所要求類型的已註冊服務。</span><span class="sxs-lookup"><span data-stu-id="aba05-614">Implementations of this interface should simply delegate to the underlying dependency injection container to provide the registered service for the requested type.</span></span>

<span data-ttu-id="aba05-615">當沒有所要求類型的已註冊服務時，ASP.NET MVC 會預期此介面的執行會從 GetService 傳回 null，並從 GetServices 傳回空集合。</span><span class="sxs-lookup"><span data-stu-id="aba05-615">When there are no registered services of the requested type, ASP.NET MVC expects implementations of this interface to return null from GetService and to return an empty collection from GetServices.</span></span>

<span data-ttu-id="aba05-616">新的 DependencyResolver 類別可讓您註冊用來執行新 IDependencyResolver 介面或泛型服務定位器介面（IServiceLocator）的類別。</span><span class="sxs-lookup"><span data-stu-id="aba05-616">The new DependencyResolver class lets you register classes that implement either the new IDependencyResolver interface or the Common Service Locator interface (IServiceLocator).</span></span> <span data-ttu-id="aba05-617">如需有關一般服務定位器的詳細資訊，請參閱[GitHub 上的 CommonServiceLocator](https://github.com/unitycontainer/commonservicelocator)。</span><span class="sxs-lookup"><span data-stu-id="aba05-617">For more information about Common Service Locator, see [CommonServiceLocator on GitHub](https://github.com/unitycontainer/commonservicelocator).</span></span>

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a><span data-ttu-id="aba05-618">微調視圖頁面具現化的新 IViewActivator 介面</span><span class="sxs-lookup"><span data-stu-id="aba05-618">New IViewActivator Interface for Fine-Grained View Page Instantiation</span></span>

<span data-ttu-id="aba05-619">新的 IViewPageActivator 介面可讓您更精細地控制透過相依性插入來具現化視圖頁面的方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-619">The new IViewPageActivator interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="aba05-620">這同時適用于 WebFormView 實例和 RazorView 實例。</span><span class="sxs-lookup"><span data-stu-id="aba05-620">This applies to both WebFormView instances and RazorView instances.</span></span> <span data-ttu-id="aba05-621">下列範例顯示新的介面：</span><span class="sxs-lookup"><span data-stu-id="aba05-621">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

<span data-ttu-id="aba05-622">這些類別現在接受 IViewPageActivator 的函式引數，可讓您使用相依性插入來控制 ViewPage、ViewUserControl 和 WebViewPage 類型的具現化方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-622">These classes now accept an IViewPageActivator constructor argument, which lets you use dependency injection to control how the ViewPage, ViewUserControl, and WebViewPage types are instantiated.</span></span>

#### <a name="new-dependency-resolver-support-for-existing-services"></a><span data-ttu-id="aba05-623">現有服務的新相依性解析程式支援</span><span class="sxs-lookup"><span data-stu-id="aba05-623">New Dependency Resolver Support for Existing Services</span></span>

<span data-ttu-id="aba05-624">新版本包含下列服務的相依性解析支援：</span><span class="sxs-lookup"><span data-stu-id="aba05-624">The new release includes dependency resolution support for the following services:</span></span>

- <span data-ttu-id="aba05-625">模型驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="aba05-625">Model validation providers.</span></span> <span data-ttu-id="aba05-626">執行 ModelValidatorProvider 的類別可以在相依性解析程式中註冊，而且系統會使用它們來支援用戶端和伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="aba05-626">Classes that implement ModelValidatorProvider can be registered in the dependency resolver, and the system will use them to support client- and server-side validation.</span></span>
- <span data-ttu-id="aba05-627">模型中繼資料提供者。</span><span class="sxs-lookup"><span data-stu-id="aba05-627">Model metadata provider.</span></span> <span data-ttu-id="aba05-628">實 ModelMetadataProvider 的單一類別可以在相依性解析程式中註冊，而且系統會使用它來提供範本化和驗證系統的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="aba05-628">A single class that implements ModelMetadataProvider can be registered in the dependency resolver, and the system will use it to provide metadata for the templating and validation systems.</span></span>
- <span data-ttu-id="aba05-629">值提供者。</span><span class="sxs-lookup"><span data-stu-id="aba05-629">Value providers.</span></span> <span data-ttu-id="aba05-630">實 ValueProviderFactory 的類別可以在相依性解析程式中註冊，而且系統會使用它們來建立控制器和模型系結期間所使用的值提供者。</span><span class="sxs-lookup"><span data-stu-id="aba05-630">Classes that implement ValueProviderFactory can be registered in the dependency resolver, and the system will use them to create value providers that are consumed by the controller and during model binding.</span></span>
- <span data-ttu-id="aba05-631">模型系結器。</span><span class="sxs-lookup"><span data-stu-id="aba05-631">Model binders.</span></span> <span data-ttu-id="aba05-632">實 IModelBinderProvider 的類別可以在相依性解析程式中註冊，而且系統會使用它們來建立模型系結系統所使用的模型系結器。</span><span class="sxs-lookup"><span data-stu-id="aba05-632">Classes that implement IModelBinderProvider can be registered in the dependency resolver, and the system will use them to create model binders that are consumed by the model binding system.</span></span>

### <a id="0.1__Toc274034221"></a><span data-ttu-id="aba05-633">不顯眼的 jQuery 型 Ajax 的新支援</span><span class="sxs-lookup"><span data-stu-id="aba05-633">New Support for Unobtrusive jQuery-Based Ajax</span></span>

<span data-ttu-id="aba05-634">ASP.NET MVC 包含 Ajax helper 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-634">ASP.NET MVC includes Ajax helper methods such as the following:</span></span>

- <span data-ttu-id="aba05-635">Ajax Html.actionlink</span><span class="sxs-lookup"><span data-stu-id="aba05-635">Ajax.ActionLink</span></span>
- <span data-ttu-id="aba05-636">Ajax. RouteLink</span><span class="sxs-lookup"><span data-stu-id="aba05-636">Ajax.RouteLink</span></span>
- <span data-ttu-id="aba05-637">Ajax. Html.beginform</span><span class="sxs-lookup"><span data-stu-id="aba05-637">Ajax.BeginForm</span></span>
- <span data-ttu-id="aba05-638">Ajax. BeginRouteForm</span><span class="sxs-lookup"><span data-stu-id="aba05-638">Ajax.BeginRouteForm</span></span>

<span data-ttu-id="aba05-639">這些方法會使用 JavaScript 在伺服器上叫用動作方法，而不是使用完整回傳。</span><span class="sxs-lookup"><span data-stu-id="aba05-639">These methods use JavaScript to invoke an action method on the server rather than using a full postback.</span></span> <span data-ttu-id="aba05-640">這項功能已更新為以不顯眼的方式利用 jQuery。</span><span class="sxs-lookup"><span data-stu-id="aba05-640">This functionality has been updated to take advantage of jQuery in an unobtrusive manner.</span></span> <span data-ttu-id="aba05-641">這些 helper 方法會使用*data ajax*前置詞發出 HTML5 屬性，而不是發出內嵌用戶端腳本干擾。</span><span class="sxs-lookup"><span data-stu-id="aba05-641">Rather than intrusively emitting inline client scripts, these helper methods separate the behavior from the markup by emitting HTML5 attributes using the *data-ajax* prefix.</span></span> <span data-ttu-id="aba05-642">然後藉由參考適當的 JavaScript 檔案，將行為套用至標記。</span><span class="sxs-lookup"><span data-stu-id="aba05-642">Behavior is then applied to the markup by referencing the appropriate JavaScript files.</span></span> <span data-ttu-id="aba05-643">請確定已參考下列 JavaScript 檔案：</span><span class="sxs-lookup"><span data-stu-id="aba05-643">Make sure that the following JavaScript files are referenced:</span></span>

- <span data-ttu-id="aba05-644">jquery-1.7.2.min.js 1.4.1 .js</span><span class="sxs-lookup"><span data-stu-id="aba05-644">jquery-1.4.1.js</span></span>
- <span data-ttu-id="aba05-645">jquery. 不顯眼的 .js</span><span class="sxs-lookup"><span data-stu-id="aba05-645">jquery.unobtrusive.ajax.js</span></span>

<span data-ttu-id="aba05-646">在 ASP.NET MVC 3 新專案範本的 web.config 檔案中，預設會啟用這項功能，但現有專案預設會停用。</span><span class="sxs-lookup"><span data-stu-id="aba05-646">This feature is enabled by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="aba05-647">如需詳細資訊，請參閱本檔稍後的[針對用戶端驗證和不顯眼的 JavaScript 新增應用程式範圍的旗標](#0.1_AddedApplicationWideFlagsForClientValida)。</span><span class="sxs-lookup"><span data-stu-id="aba05-647">For more information, see [Added application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

### <a id="0.1__Toc274034222"></a><span data-ttu-id="aba05-648">不顯眼 jQuery 驗證的新支援</span><span class="sxs-lookup"><span data-stu-id="aba05-648">New Support for Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="aba05-649">根據預設，ASP.NET MVC 3 Beta 會以不顯眼的方式使用 jQuery 驗證，來執行用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="aba05-649">By default, ASP.NET MVC 3 Beta uses jQuery validation in an unobtrusive manner in order to perform client-side validation.</span></span> <span data-ttu-id="aba05-650">若要啟用不顯眼的用戶端驗證，請從視圖內部進行呼叫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-650">To enable unobtrusive client validation, make a call like the following from within a view:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

<span data-ttu-id="aba05-651">這會要求 ViewCoNtext. UnobtrusiveJavaScriptEnabled 屬性設定為 true，您可以藉由進行下列呼叫來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="aba05-651">This requires that ViewContext.UnobtrusiveJavaScriptEnabled property is set to true, which you can do by making the following call:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

<span data-ttu-id="aba05-652">此外，請確定已參考下列 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="aba05-652">Also make sure the following JavaScript files are referenced.</span></span>

- <span data-ttu-id="aba05-653">jquery-1.7.2.min.js 1.4.1 .js</span><span class="sxs-lookup"><span data-stu-id="aba05-653">jquery-1.4.1.js</span></span>
- <span data-ttu-id="aba05-654">jquery. validate .js</span><span class="sxs-lookup"><span data-stu-id="aba05-654">jquery.validate.js</span></span>
- <span data-ttu-id="aba05-655">jquery. validate. 不顯眼的 .js</span><span class="sxs-lookup"><span data-stu-id="aba05-655">jquery.validate.unobtrusive.js</span></span>

<span data-ttu-id="aba05-656">在 ASP.NET MVC 3 新專案範本的 web.config 檔案中，預設會啟用這項功能，但現有專案預設會停用。</span><span class="sxs-lookup"><span data-stu-id="aba05-656">This feature is enabled on by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="aba05-657">如需詳細資訊，請參閱本檔稍後的[適用于用戶端驗證的新應用程式範圍旗標和不顯眼的 JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) 。</span><span class="sxs-lookup"><span data-stu-id="aba05-657">For more information, see [New application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a><span data-ttu-id="aba05-658">適用于用戶端驗證和不顯眼 JavaScript 的新全應用程式旗標</span><span class="sxs-lookup"><span data-stu-id="aba05-658">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>

<span data-ttu-id="aba05-659">您可以使用 HtmlHelper 類別的靜態成員，全域啟用或停用用戶端驗證和不顯眼的 JavaScript，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-659">You can enable or disable client validation and unobtrusive JavaScript globally using static members of the HtmlHelper class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

<span data-ttu-id="aba05-660">預設的專案範本預設會啟用不顯眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="aba05-660">The default project templates enable unobtrusive JavaScript by default.</span></span> <span data-ttu-id="aba05-661">您也可以使用下列設定，在應用程式的根 Web.config 檔案中啟用或停用這些功能：</span><span class="sxs-lookup"><span data-stu-id="aba05-661">You can also enable or disable these features in the root Web.config file of your application using the following settings:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

<span data-ttu-id="aba05-662">因為根據預設，您可以啟用這些功能，所以新的多載會引進 HtmlHelper 類別，讓您覆寫預設設定，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-662">Because you can enable these features by default, new overloads were introduced to the HtmlHelper class that let you override the default settings, as shown in the following examples:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

<span data-ttu-id="aba05-663">為了回溯相容性，預設會停用這兩項功能。</span><span class="sxs-lookup"><span data-stu-id="aba05-663">For backward compatibility, both of these features are disabled by default.</span></span>

### <a id="0.1__Toc274034224"></a><span data-ttu-id="aba05-664">新支援在 Views 執行之前執行的程式碼</span><span class="sxs-lookup"><span data-stu-id="aba05-664">New Support for Code that Runs Before Views Run</span></span>

<span data-ttu-id="aba05-665">您現在可以將名為 \_viewstart 的檔案（或 \_viewstart）放在 Views 目錄中，並將程式碼新增至該目錄及其子目錄中的多個視圖之間共用。</span><span class="sxs-lookup"><span data-stu-id="aba05-665">You can now put a file named \_viewstart.cshtml (or \_viewstart.vbhtml) in the Views directory and add code to it that will be shared among multiple views in that directory and its subdirectories.</span></span> <span data-ttu-id="aba05-666">例如，您可能會將下列程式碼放入 ~/Views 資料夾中的 \_viewstart. cshtml 頁面：</span><span class="sxs-lookup"><span data-stu-id="aba05-666">For example, you might put the following code into the \_viewstart.cshtml page in the ~/Views folder:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

<span data-ttu-id="aba05-667">這會以遞迴方式設定 Views 資料夾及其所有子資料夾中每個視圖的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="aba05-667">This sets the layout page for every view within the Views folder and all its subfolders recursively.</span></span> <span data-ttu-id="aba05-668">當正在呈現視圖時，\_viewstart 中的程式碼會在視圖程式碼執行之前執行。</span><span class="sxs-lookup"><span data-stu-id="aba05-668">When a view is being rendered, the code in the \_viewstart.cshtml file runs before the view code runs.</span></span> <span data-ttu-id="aba05-669">\_viewstart 的程式碼會套用到該資料夾中的每個視圖。</span><span class="sxs-lookup"><span data-stu-id="aba05-669">The \_viewstart.cshtml code applies to every view in that folder.</span></span>

<span data-ttu-id="aba05-670">根據預設，\_viewstart 檔案中的程式碼也適用于任何子資料夾中的 views。</span><span class="sxs-lookup"><span data-stu-id="aba05-670">By default, the code in the \_viewstart.cshtml file also applies to views in any subfolder.</span></span> <span data-ttu-id="aba05-671">不過，個別的子資料夾可以有自己的 \_viewstart 檔版本;在此情況下，會優先使用本機版本。</span><span class="sxs-lookup"><span data-stu-id="aba05-671">However, individual subfolders can have their own version of the \_viewstart.cshtml file; in that case, the local version takes precedence.</span></span> <span data-ttu-id="aba05-672">例如，若要執行 HomeController 的所有視圖通用的程式碼，請在 ~/Views/Home 資料夾中放入 \_viewstart. cshtml 檔案。</span><span class="sxs-lookup"><span data-stu-id="aba05-672">For example, to run code that is common to all views for the HomeController, put a \_viewstart.cshtml file in the ~/Views/Home folder.</span></span>

### <a id="0.1__Toc274034225"></a><span data-ttu-id="aba05-673">VBHTML Razor 語法的新支援</span><span class="sxs-lookup"><span data-stu-id="aba05-673">New Support for the VBHTML Razor Syntax</span></span>

<span data-ttu-id="aba05-674">先前的 ASP.NET MVC preview 包含使用以 Razor 語法為基礎的視圖C#支援。</span><span class="sxs-lookup"><span data-stu-id="aba05-674">The previous ASP.NET MVC preview included support for views using Razor syntax based on C#.</span></span> <span data-ttu-id="aba05-675">這些視圖會使用. # 副檔名。</span><span class="sxs-lookup"><span data-stu-id="aba05-675">These views use the .cshtml file extension.</span></span> <span data-ttu-id="aba05-676">為支援 Razor 的持續性工作，ASP.NET MVC 3 Beta 引進了使用. vbhtml 副檔名之 Visual Basic 中 Razor 語法的支援。</span><span class="sxs-lookup"><span data-stu-id="aba05-676">As part of ongoing work to support Razor, the ASP.NET MVC 3 Beta introduces support for the Razor syntax in Visual Basic, which uses the .vbhtml file extension.</span></span>

<span data-ttu-id="aba05-677">如需在 VBHTML 頁面中使用 Visual Basic 語法的簡介，請參閱下列 URL 的教學課程：</span><span class="sxs-lookup"><span data-stu-id="aba05-677">For an introduction to using Visual Basic syntax in VBHTML pages, see the tutorial at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a><span data-ttu-id="aba05-678">更精細地控制 Validateinputattribute 套用</span><span class="sxs-lookup"><span data-stu-id="aba05-678">More Granular Control over ValidateInputAttribute</span></span>

<span data-ttu-id="aba05-679">ASP.NET MVC 一律包含 Validateinputattribute 套用類別，它會叫用核心 ASP.NET 要求驗證基礎結構，以確保連入要求不會包含可能的惡意輸入。</span><span class="sxs-lookup"><span data-stu-id="aba05-679">ASP.NET MVC has always included the ValidateInputAttribute class, which invokes the core ASP.NET request validation infrastructure to make sure that the incoming request does not contain potentially malicious input.</span></span> <span data-ttu-id="aba05-680">根據預設，會啟用輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="aba05-680">By default, input validation is enabled.</span></span> <span data-ttu-id="aba05-681">您可以使用 Validateinputattribute 套用屬性來停用要求驗證，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-681">It is possible to disable request validation by using the ValidateInputAttribute attribute, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

<span data-ttu-id="aba05-682">不過，許多 web 應用程式都有個別的表單欄位，需要允許 HTML，而其餘欄位則不應該。</span><span class="sxs-lookup"><span data-stu-id="aba05-682">However, many web applications have individual form fields that need to allow HTML, while the remaining fields should not.</span></span> <span data-ttu-id="aba05-683">Validateinputattribute 套用類別現在可讓您指定不應包含在要求驗證中的欄位清單。</span><span class="sxs-lookup"><span data-stu-id="aba05-683">The ValidateInputAttribute class now lets you specify a list of fields that should not be included in request validation.</span></span>

<span data-ttu-id="aba05-684">例如，如果您正在開發 blog engine，您可能會想要在 [內文] 和 [摘要] 欄位中允許標記。</span><span class="sxs-lookup"><span data-stu-id="aba05-684">For example, if you are developing a blog engine, you might want to allow markup in the Body and Summary fields.</span></span> <span data-ttu-id="aba05-685">這些欄位可能會以兩個 input 元素表示，每個專案都有一個對應至屬性名稱（「本文」和「摘要」）的名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-685">These fields might be represented by two input element, each with a name attribute corresponding to the property name ("Body" and "Summary").</span></span> <span data-ttu-id="aba05-686">若只要停用這些欄位的要求驗證，請在 ValidateInput 類別的 Exclude 屬性中指定名稱（以逗號分隔），如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-686">To disable request validation for these fields only, specify the names (comma-separated) in the Exclude property of the ValidateInput class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a><span data-ttu-id="aba05-687">協助程式將底線轉換為使用匿名物件指定之 HTML 屬性名稱的連字號</span><span class="sxs-lookup"><span data-stu-id="aba05-687">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>

<span data-ttu-id="aba05-688">Helper 方法可讓您使用匿名物件指定屬性名稱/值組，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aba05-688">Helper methods let you specify attribute name/value pairs using an anonymous object, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

<span data-ttu-id="aba05-689">這種方法不會讓您在屬性名稱中使用連字號，因為 ASP.NET 中的屬性名稱不能使用連字號。</span><span class="sxs-lookup"><span data-stu-id="aba05-689">This approach doesn't let you use hyphens in the attribute name, because a hyphen cannot be used for a property name in ASP.NET.</span></span> <span data-ttu-id="aba05-690">不過，連字號對自訂 HTML5 屬性而言很重要;例如，HTML5 會使用 "data-" 前置詞。</span><span class="sxs-lookup"><span data-stu-id="aba05-690">However, hyphens are important for custom HTML5 attributes; for example, HTML5 uses the "data-" prefix.</span></span>

<span data-ttu-id="aba05-691">同時，底線無法用於 HTML 中的屬性名稱，但是在屬性名稱中是有效的。</span><span class="sxs-lookup"><span data-stu-id="aba05-691">At the same time, underscores cannot be used for attribute names in HTML, but are valid within property names.</span></span> <span data-ttu-id="aba05-692">因此，如果您使用匿名物件指定屬性，而且如果屬性名稱包含底線，則 helper 方法會將底線轉換為連字號。</span><span class="sxs-lookup"><span data-stu-id="aba05-692">Therefore, if you specify attributes using an anonymous object, and if the attribute names include an underscore,, helper methods will convert the underscores to hyphens.</span></span> <span data-ttu-id="aba05-693">例如，下列 helper 語法會使用底線：</span><span class="sxs-lookup"><span data-stu-id="aba05-693">For example, the following helper syntax uses an underscore:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

<span data-ttu-id="aba05-694">上一個範例會在 helper 執行時呈現下列標記：</span><span class="sxs-lookup"><span data-stu-id="aba05-694">The previous example renders the following markup when the helper runs:</span></span>

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a><span data-ttu-id="aba05-695">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="aba05-695">Bug Fixes</span></span>

<span data-ttu-id="aba05-696">EditorFor 和 DisplayFor 範本協助程式的預設物件範本現在支援 DisplayAttribute. Order 屬性中所指定的順序。</span><span class="sxs-lookup"><span data-stu-id="aba05-696">The default object template for the EditorFor and DisplayFor template helpers now supports the ordering specified in the DisplayAttribute.Order property.</span></span> <span data-ttu-id="aba05-697">（在舊版中，不會使用訂單設定）。</span><span class="sxs-lookup"><span data-stu-id="aba05-697">(In previous versions, the Order setting was not used.)</span></span>

<span data-ttu-id="aba05-698">用戶端驗證現在支援驗證已套用驗證屬性的已覆寫屬性。</span><span class="sxs-lookup"><span data-stu-id="aba05-698">Client validation now supports validation of overridden properties that have validation attributes applied.</span></span>

<span data-ttu-id="aba05-699">JsonValueProviderFactory 現在預設為已註冊。</span><span class="sxs-lookup"><span data-stu-id="aba05-699">JsonValueProviderFactory is now registered by default.</span></span>

## <a id="0.1__Toc274034229"></a><span data-ttu-id="aba05-700">重大變更</span><span class="sxs-lookup"><span data-stu-id="aba05-700">Breaking Changes</span></span>

<span data-ttu-id="aba05-701">例外狀況篩選準則的執行順序已針對具有相同順序值的例外狀況篩選準則進行變更。</span><span class="sxs-lookup"><span data-stu-id="aba05-701">The order of execution for exception filters has changed for exception filters that have the same Order value.</span></span> <span data-ttu-id="aba05-702">在 ASP.NET MVC 2 （含）以前版本中，控制器上的例外狀況篩選準則會在例外狀況篩選動作方法之前執行，其順序與動作方法上的相同。</span><span class="sxs-lookup"><span data-stu-id="aba05-702">In ASP.NET MVC 2 and earlier, exception filters on the controller with the same Order as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="aba05-703">這通常是未使用指定的順序值來套用例外狀況篩選時的情況。</span><span class="sxs-lookup"><span data-stu-id="aba05-703">This would typically be the case when exception filters were applied without a specified Order value.</span></span> <span data-ttu-id="aba05-704">在 ASP.NET MVC 3 中，此順序已被反轉，因此最特定的例外狀況處理常式會先執行。</span><span class="sxs-lookup"><span data-stu-id="aba05-704">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="aba05-705">如同在舊版中，如果已明確指定 Order 屬性，則會以指定的循序執行篩選。</span><span class="sxs-lookup"><span data-stu-id="aba05-705">As in earlier versions, if the Order property is explicitly specified, the filters are run in the specified order.</span></span>

## <a id="0.1__Toc274034230"></a><span data-ttu-id="aba05-706">已知問題</span><span class="sxs-lookup"><span data-stu-id="aba05-706">Known Issues</span></span>

<span data-ttu-id="aba05-707">在安裝期間，EULA 接受對話方塊會在視窗中顯示授權條款，此視窗比預期的要小。</span><span class="sxs-lookup"><span data-stu-id="aba05-707">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>

<span data-ttu-id="aba05-708">Razor views 沒有 IntelliSense 支援或語法反白顯示。</span><span class="sxs-lookup"><span data-stu-id="aba05-708">Razor views do not have IntelliSense support nor syntax highlighting.</span></span> <span data-ttu-id="aba05-709">預期 Visual Studio 中的 Razor 語法支援將會納入為較新版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="aba05-709">It is anticipated that support for Razor syntax in Visual Studio will be included as part of a later release.</span></span>

<span data-ttu-id="aba05-710">當您編輯 Razor 視圖（CSHTML 檔案）時，Visual Studio 中<a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a>的 [移至控制器] 功能表項目將無法使用，而且不會有程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="aba05-710">When you are editing a Razor view (CSHTML file), the <a id="0.1__Toc224729061"></a><a id="0.1__Toc238051347"></a> Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<span data-ttu-id="aba05-711">使用 @model 語法來指定強型別 CSHTML 視圖時，無法辨識類型的語言特定快捷方式。</span><span class="sxs-lookup"><span data-stu-id="aba05-711">When using the @model syntax to specify a strongly typed CSHTML view, language-specific shortcuts for types are not recognized.</span></span> <span data-ttu-id="aba05-712">例如，@model int 將無法使用，但 @model Int32 會生效。</span><span class="sxs-lookup"><span data-stu-id="aba05-712">For example, @model int will not work, but @model Int32 will work.</span></span> <span data-ttu-id="aba05-713">這個 bug 的因應措施是在您指定模型類型時，使用實際的類型名稱。</span><span class="sxs-lookup"><span data-stu-id="aba05-713">The workaround for this bug is to use the actual type name when you specify the model type.</span></span>

<span data-ttu-id="aba05-714">使用 @model 語法來指定強型別 CSHTML 視圖（或 @ModelType 指定強型別 VBHTML 視圖）時，不支援可為 null 的類型和陣列宣告。</span><span class="sxs-lookup"><span data-stu-id="aba05-714">When using the @model syntax to specify a strongly typed CSHTML view (or @ModelType to specify a strongly typed VBHTML view), nullable types and array declarations are not supported.</span></span> <span data-ttu-id="aba05-715">例如，@model int？不受支援。</span><span class="sxs-lookup"><span data-stu-id="aba05-715">For example, @model int? is not supported.</span></span> <span data-ttu-id="aba05-716">請改用 `@model Nullable<Int32>`。</span><span class="sxs-lookup"><span data-stu-id="aba05-716">Instead, use `@model Nullable<Int32>`.</span></span> <span data-ttu-id="aba05-717">也不支援 @model string [] 語法;請改用 `@model IList<string>`。</span><span class="sxs-lookup"><span data-stu-id="aba05-717">The syntax @model string[] is also not supported; instead, use `@model IList<string>`.</span></span>

<span data-ttu-id="aba05-718">當您將 ASP.NET MVC 2 專案升級為 ASP.NET MVC 3 時，請務必將下列內容新增至 web.config 檔案的 appSettings 區段：</span><span class="sxs-lookup"><span data-stu-id="aba05-718">When you upgrade an ASP.NET MVC 2 project to ASP.NET MVC 3, make sure to add the following to the appSettings section of the Web.config file:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

<span data-ttu-id="aba05-719">有一個已知的問題會導致表單驗證一律將未驗證的使用者重新導向至 ~/Account/Login，而忽略 Web.config 中使用的表單驗證設定。解決方法是新增下列應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="aba05-719">There's a known issue that causes Forms Authentication to always redirect unauthenticated users to ~/Account/Login, ignoring the forms authentication setting used in Web.config. The workaround is to add the following app setting.</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a><span data-ttu-id="aba05-720">免責聲明</span><span class="sxs-lookup"><span data-stu-id="aba05-720">Disclaimer</span></span>

<span data-ttu-id="aba05-721">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="aba05-721">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="aba05-722">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="aba05-722">All rights reserved.</span></span> <span data-ttu-id="aba05-723">此文件內容未經修改。</span><span class="sxs-lookup"><span data-stu-id="aba05-723">This document is provided "as-is."</span></span> <span data-ttu-id="aba05-724">本文件提供的資訊和觀點 (包括 URL 和其他網站參考) 可能變更，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="aba05-724">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span> <span data-ttu-id="aba05-725">貴用戶必須自行承擔使用風險。</span><span class="sxs-lookup"><span data-stu-id="aba05-725">You bear the risk of using it.</span></span>

<span data-ttu-id="aba05-726">本文件並不提供您任何 Microsoft 產品之智慧財產權的法定權利。</span><span class="sxs-lookup"><span data-stu-id="aba05-726">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="aba05-727">貴用戶可以複製本文件供內部參考之用。</span><span class="sxs-lookup"><span data-stu-id="aba05-727">You may copy and use this document for your internal, reference purposes.</span></span>
