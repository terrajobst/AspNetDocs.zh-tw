---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 和 Visual Studio 2012 的新功能 |Microsoft Docs
author: rick-anderson
description: 本檔說明 ASP.NET 4.5 中引進的新功能和增強功能。 它也會描述針對 web 程式開發所做的改進 。
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526674"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="ca38c-104">ASP.NET 4.5 與 Visual Studio 2012 的新功能</span><span class="sxs-lookup"><span data-stu-id="ca38c-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>

> <span data-ttu-id="ca38c-105">本檔說明 ASP.NET 4.5 中引進的新功能和增強功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="ca38c-106">它也描述在 Visual Studio 2012 中進行 網頁程式開發的改善。</span><span class="sxs-lookup"><span data-stu-id="ca38c-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="ca38c-107">這份檔最初是在2012年2月29日發行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-107">This document was originally published on February 29, 2012.</span></span>

- [<span data-ttu-id="ca38c-108">ASP.NET Core 執行時間和架構</span><span class="sxs-lookup"><span data-stu-id="ca38c-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="ca38c-109">非同步讀取和寫入 HTTP 要求和回應</span><span class="sxs-lookup"><span data-stu-id="ca38c-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="ca38c-110">HttpRequest 處理的改良功能</span><span class="sxs-lookup"><span data-stu-id="ca38c-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="ca38c-111">以非同步方式排清回應</span><span class="sxs-lookup"><span data-stu-id="ca38c-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="ca38c-112">支援*await* *和以工作為基礎*的非同步模組和處理常式</span><span class="sxs-lookup"><span data-stu-id="ca38c-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="ca38c-113">非同步 HTTP 模組</span><span class="sxs-lookup"><span data-stu-id="ca38c-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="ca38c-114">非同步 HTTP 處理常式</span><span class="sxs-lookup"><span data-stu-id="ca38c-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="ca38c-115">新的 ASP.NET 要求驗證功能</span><span class="sxs-lookup"><span data-stu-id="ca38c-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="ca38c-116">延遲（「延遲」）要求驗證</span><span class="sxs-lookup"><span data-stu-id="ca38c-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="ca38c-117">支援未驗證要求</span><span class="sxs-lookup"><span data-stu-id="ca38c-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="ca38c-118">AntiXSS 程式庫</span><span class="sxs-lookup"><span data-stu-id="ca38c-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="ca38c-119">Websocket 通訊協定的支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="ca38c-120">統合和縮製</span><span class="sxs-lookup"><span data-stu-id="ca38c-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="ca38c-121">Web 裝載的效能改進</span><span class="sxs-lookup"><span data-stu-id="ca38c-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="ca38c-122">關鍵效能因素</span><span class="sxs-lookup"><span data-stu-id="ca38c-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="ca38c-123">新效能功能的需求</span><span class="sxs-lookup"><span data-stu-id="ca38c-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="ca38c-124">共用萬用群組件</span><span class="sxs-lookup"><span data-stu-id="ca38c-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="ca38c-125">使用多核心 JIT 編譯加快啟動速度</span><span class="sxs-lookup"><span data-stu-id="ca38c-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="ca38c-126">微調垃圾收集以優化記憶體</span><span class="sxs-lookup"><span data-stu-id="ca38c-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="ca38c-127">預先提取 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca38c-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="ca38c-128">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="ca38c-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="ca38c-129">強型別資料控制項</span><span class="sxs-lookup"><span data-stu-id="ca38c-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="ca38c-130">模型繫結</span><span class="sxs-lookup"><span data-stu-id="ca38c-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="ca38c-131">選取資料</span><span class="sxs-lookup"><span data-stu-id="ca38c-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="ca38c-132">值提供者</span><span class="sxs-lookup"><span data-stu-id="ca38c-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="ca38c-133">依控制項中的值篩選</span><span class="sxs-lookup"><span data-stu-id="ca38c-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="ca38c-134">HTML 編碼的資料系結運算式</span><span class="sxs-lookup"><span data-stu-id="ca38c-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="ca38c-135">不顯眼的驗證</span><span class="sxs-lookup"><span data-stu-id="ca38c-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="ca38c-136">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="ca38c-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="ca38c-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="ca38c-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="ca38c-138">ASP.NET Web Pages 2</span><span class="sxs-lookup"><span data-stu-id="ca38c-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="ca38c-139">Visual Studio 2012 候選版</span><span class="sxs-lookup"><span data-stu-id="ca38c-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="ca38c-140">Visual Studio 2010 和 Visual Studio 2012 候選版之間的專案共用（專案相容性）</span><span class="sxs-lookup"><span data-stu-id="ca38c-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="ca38c-141">ASP.NET 4.5 網站範本中的設定變更</span><span class="sxs-lookup"><span data-stu-id="ca38c-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="ca38c-142">IIS 7 中用於 ASP.NET 路由的原生支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="ca38c-143">HTML 編輯器</span><span class="sxs-lookup"><span data-stu-id="ca38c-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="ca38c-144">智慧型工作</span><span class="sxs-lookup"><span data-stu-id="ca38c-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="ca38c-145">WAI-ARIA 支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="ca38c-146">新的 HTML5 程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ca38c-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="ca38c-147">解壓縮至使用者控制項</span><span class="sxs-lookup"><span data-stu-id="ca38c-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="ca38c-148">屬性中程式碼區塊的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="ca38c-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="ca38c-149">當您重新命名開頭或結束記號時，自動重新命名相符的標記</span><span class="sxs-lookup"><span data-stu-id="ca38c-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="ca38c-150">事件處理常式產生</span><span class="sxs-lookup"><span data-stu-id="ca38c-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="ca38c-151">智慧縮排</span><span class="sxs-lookup"><span data-stu-id="ca38c-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="ca38c-152">自動縮減語句完成</span><span class="sxs-lookup"><span data-stu-id="ca38c-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="ca38c-153">JavaScript 編輯器</span><span class="sxs-lookup"><span data-stu-id="ca38c-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="ca38c-154">程式碼大綱</span><span class="sxs-lookup"><span data-stu-id="ca38c-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="ca38c-155">括弧對稱</span><span class="sxs-lookup"><span data-stu-id="ca38c-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="ca38c-156">移至定義</span><span class="sxs-lookup"><span data-stu-id="ca38c-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="ca38c-157">ECMAScript5 支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="ca38c-158">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="ca38c-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="ca38c-159">VSDOC 簽章多載</span><span class="sxs-lookup"><span data-stu-id="ca38c-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="ca38c-160">隱含參考</span><span class="sxs-lookup"><span data-stu-id="ca38c-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="ca38c-161">CSS 編輯器</span><span class="sxs-lookup"><span data-stu-id="ca38c-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="ca38c-162">自動縮減語句完成</span><span class="sxs-lookup"><span data-stu-id="ca38c-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="ca38c-163">階層式縮排。</span><span class="sxs-lookup"><span data-stu-id="ca38c-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="ca38c-164">CSS 的駭客支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="ca38c-165">廠商特定架構（-moz-appearance-,-webkit）</span><span class="sxs-lookup"><span data-stu-id="ca38c-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="ca38c-166">批註和取消批註支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="ca38c-167">色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="ca38c-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="ca38c-168">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ca38c-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="ca38c-169">自訂區域</span><span class="sxs-lookup"><span data-stu-id="ca38c-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="ca38c-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="ca38c-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="ca38c-171">發佈</span><span class="sxs-lookup"><span data-stu-id="ca38c-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="ca38c-172">發佈設定檔</span><span class="sxs-lookup"><span data-stu-id="ca38c-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="ca38c-173">ASP.NET 先行編譯和合併</span><span class="sxs-lookup"><span data-stu-id="ca38c-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="ca38c-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="ca38c-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="ca38c-175">免責聲明</span><span class="sxs-lookup"><span data-stu-id="ca38c-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="ca38c-176">ASP.NET Core 執行時間和架構</span><span class="sxs-lookup"><span data-stu-id="ca38c-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="ca38c-177">非同步讀取和寫入 HTTP 要求和回應</span><span class="sxs-lookup"><span data-stu-id="ca38c-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="ca38c-178">ASP.NET 4 引進了使用*HttpRequest. GetBufferlessInputStream*方法，將 HTTP 要求實體讀取為數據流的功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="ca38c-179">這個方法提供要求實體的串流存取。</span><span class="sxs-lookup"><span data-stu-id="ca38c-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="ca38c-180">不過，它會以同步方式執行，這會在要求的持續時間內系結執行緒。</span><span class="sxs-lookup"><span data-stu-id="ca38c-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="ca38c-181">ASP.NET 4.5 支援以非同步方式讀取 HTTP 要求實體上的資料流程，以及非同步地進行清除的能力。</span><span class="sxs-lookup"><span data-stu-id="ca38c-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="ca38c-182">ASP.NET 4.5 也讓您能夠對 HTTP 要求實體進行雙重緩衝處理，這可讓您更輕鬆地與下游 HTTP 處理常式（例如 .aspx 頁面處理常式和 ASP.NET MVC 控制器）進行整合。</span><span class="sxs-lookup"><span data-stu-id="ca38c-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="ca38c-183">HttpRequest 處理的改良功能</span><span class="sxs-lookup"><span data-stu-id="ca38c-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="ca38c-184">ASP.NET 4.5 從*HttpRequest*傳回的資料流程參考同時支援同步和非同步讀取方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="ca38c-185">從*GetBufferlessInputStream*傳回的*資料流程*物件現在會同時執行 BeginRead 和 EndRead 方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="ca38c-186">非同步*資料流程*方法可讓您以區塊非同步方式讀取要求實體，而 ASP.NET 則會在非同步讀取迴圈的每個反復專案之間釋放目前的執行緒。</span><span class="sxs-lookup"><span data-stu-id="ca38c-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="ca38c-187">ASP.NET 4.5 也已加入隨附方法，以緩衝方式讀取要求實體： *HttpRequest. GetBufferedInputStream*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="ca38c-188">這個新的多載的運作方式類似*GetBufferlessInputStream*，同時支援同步和非同步讀取。</span><span class="sxs-lookup"><span data-stu-id="ca38c-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="ca38c-189">不過，在讀取時， *GetBufferedInputStream*也會將實體位元組複製到 ASP.NET 內部緩衝區，讓下游模組和處理常式仍然可以存取要求實體。</span><span class="sxs-lookup"><span data-stu-id="ca38c-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="ca38c-190">例如，如果管線中的某些上游程式碼已使用*GetBufferedInputStream*讀取要求實體，您仍然可以使用*HttpRequest*或*HttpRequest*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="ca38c-191">這可讓您對要求執行非同步處理（例如，串流處理大型檔案上傳至資料庫），但之後仍會執行 .aspx 頁面和 MVC ASP.NET 控制器。</span><span class="sxs-lookup"><span data-stu-id="ca38c-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="ca38c-192">以非同步方式排清回應</span><span class="sxs-lookup"><span data-stu-id="ca38c-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="ca38c-193">將回應傳送至 HTTP 用戶端可能需要相當長的時間，因為用戶端已離開或具有低頻寬連線。</span><span class="sxs-lookup"><span data-stu-id="ca38c-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="ca38c-194">通常 ASP.NET 會緩衝應用程式所建立的回應位元組。</span><span class="sxs-lookup"><span data-stu-id="ca38c-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="ca38c-195">然後，ASP.NET 會在要求處理結束時，執行累計緩衝區的單一傳送作業。</span><span class="sxs-lookup"><span data-stu-id="ca38c-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="ca38c-196">如果緩衝的回應很大（例如，將大型檔案串流處理至用戶端），您必須定期呼叫*HttpResponse* ，將緩衝的輸出傳送到用戶端，並將記憶體使用量保持在控制之下。</span><span class="sxs-lookup"><span data-stu-id="ca38c-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="ca38c-197">不過，因為*Flush*是同步呼叫，所以反復呼叫排*清仍然會*在可能長時間執行的要求期間耗用執行緒。</span><span class="sxs-lookup"><span data-stu-id="ca38c-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="ca38c-198">ASP.NET 4.5 加入了使用*HttpResponse*類別的*BeginFlush*和*EndFlush*方法，以非同步方式執行排清的支援。</span><span class="sxs-lookup"><span data-stu-id="ca38c-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="ca38c-199">使用這些方法，您可以建立異步模組和非同步處理常式，以累加方式將資料傳送至用戶端，而不需要佔用作業系統執行緒。</span><span class="sxs-lookup"><span data-stu-id="ca38c-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="ca38c-200">在*BeginFlush*與*EndFlush*呼叫之間，ASP.NET 會釋放目前的執行緒。</span><span class="sxs-lookup"><span data-stu-id="ca38c-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="ca38c-201">這會大幅減少所需的作用中線程總數，以便支援長時間執行的 HTTP 下載。</span><span class="sxs-lookup"><span data-stu-id="ca38c-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="ca38c-202">支援*await* *和以工作為基礎*的非同步模組和處理常式</span><span class="sxs-lookup"><span data-stu-id="ca38c-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="ca38c-203">.NET Framework 4 引進*了一個稱為工作的*非同步程式設計概念。</span><span class="sxs-lookup"><span data-stu-id="ca38c-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="ca38c-204">*工作是以工作類型和*[*系統執行緒*] 命名空間中的相關類型來表示。</span><span class="sxs-lookup"><span data-stu-id="ca38c-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="ca38c-205">.NET Framework 4.5 以此為基礎，使用編譯器增強功能，讓處理*工作物件變*得簡單。</span><span class="sxs-lookup"><span data-stu-id="ca38c-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="ca38c-206">在 .NET Framework 4.5 中，編譯器支援兩個新的關鍵字： *await*和*async*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="ca38c-207">*Await*關鍵字是語法速記，表示程式碼段應該以非同步方式等候某個程式碼的其他部分。</span><span class="sxs-lookup"><span data-stu-id="ca38c-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="ca38c-208">*Async*關鍵字代表一個提示，可讓您將方法標示為以工作為基礎的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="ca38c-209">*Await*、 *async*和*Task*物件的組合，可讓您更輕鬆地在 .net 4.5 中撰寫非同步程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca38c-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="ca38c-210">ASP.NET 4.5 透過新的 Api 支援這些簡化，可讓您使用新的編譯器增強功能撰寫非同步 HTTP 模組和非同步 HTTP 處理常式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="ca38c-211">非同步 HTTP 模組</span><span class="sxs-lookup"><span data-stu-id="ca38c-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="ca38c-212">假設您想要在傳回*Task*物件的方法內執行非同步工作。</span><span class="sxs-lookup"><span data-stu-id="ca38c-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="ca38c-213">下列程式碼範例定義非同步方法，以進行非同步呼叫以下載 Microsoft 首頁。</span><span class="sxs-lookup"><span data-stu-id="ca38c-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="ca38c-214">請注意，方法簽章中的*async*關鍵字和*DownloadStringTaskAsync*的*await*呼叫中的用法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="ca38c-215">這就是您必須撰寫的，.NET Framework 會在等候下載完成時，自動處理呼叫堆疊的回溯作業，以及在下載完成之後自動還原呼叫堆疊。</span><span class="sxs-lookup"><span data-stu-id="ca38c-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="ca38c-216">現在假設您想要在非同步 ASP.NET HTTP 模組中使用這個非同步方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="ca38c-217">ASP.NET 4.5 包含 helper 方法（*EventHandlerTaskAsyncHelper*）和新的委派類型（*TaskEventHandler*），可讓您用來整合以工作為基礎的非同步方法與 ASP.NET HTTP 管線所公開的舊版非同步程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="ca38c-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="ca38c-218">此範例顯示如何：</span><span class="sxs-lookup"><span data-stu-id="ca38c-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="ca38c-219">非同步 HTTP 處理常式</span><span class="sxs-lookup"><span data-stu-id="ca38c-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="ca38c-220">在 ASP.NET 中撰寫非同步處理常式的傳統方法是執行*IHttpAsyncHandler*介面。</span><span class="sxs-lookup"><span data-stu-id="ca38c-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="ca38c-221">ASP.NET 4.5 引進了您可以衍生自的*HttpTaskAsyncHandler*非同步基底類型，讓您更容易撰寫非同步處理常式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="ca38c-222">*HttpTaskAsyncHandler*類型是 abstract，而且需要您覆寫*ProcessRequestAsync*方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="ca38c-223">內部 ASP.NET 會負責將*ProcessRequestAsync*的傳回簽章（ *Task*物件）與 ASP.NET 管線所使用的舊版非同步程式設計模型整合。</span><span class="sxs-lookup"><span data-stu-id="ca38c-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="ca38c-224">下列範例顯示如何在非同步 HTTP 處理常式的執行過程中使用*Task*和*await* ：</span><span class="sxs-lookup"><span data-stu-id="ca38c-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="ca38c-225">新的 ASP.NET 要求驗證功能</span><span class="sxs-lookup"><span data-stu-id="ca38c-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="ca38c-226">根據預設，ASP.NET 會執行要求驗證，它會檢查要求以尋找欄位、標頭、cookie 等中的標記或腳本。</span><span class="sxs-lookup"><span data-stu-id="ca38c-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="ca38c-227">如果偵測到任何一種情況，ASP.NET 會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ca38c-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="ca38c-228">這可作為防禦潛在跨網站腳本攻擊的第一道防線。</span><span class="sxs-lookup"><span data-stu-id="ca38c-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="ca38c-229">ASP.NET 4.5 可讓您更輕鬆地讀取未驗證要求資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="ca38c-230">ASP.NET 4.5 也整合了熱門的 AntiXSS 程式庫，這是先前的外部程式庫。</span><span class="sxs-lookup"><span data-stu-id="ca38c-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="ca38c-231">開發人員經常會要求能夠選擇性地關閉其應用程式的要求驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="ca38c-232">例如，如果您的應用程式是論壇軟體，您可能會想要允許使用者提交 HTML 格式的論壇貼文和留言，但仍可確保要求驗證會檢查其他專案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="ca38c-233">ASP.NET 4.5 引進兩種功能，可讓您選擇性地使用未驗證輸入：延遲（「延遲」）要求驗證和存取未驗證要求資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="ca38c-234">延遲（「延遲」）要求驗證</span><span class="sxs-lookup"><span data-stu-id="ca38c-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="ca38c-235">在 ASP.NET 4.5 中，根據預設，所有要求資料都受限於要求驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="ca38c-236">不過，您可以將應用程式設定為延遲要求驗證，直到實際存取要求資料為止。</span><span class="sxs-lookup"><span data-stu-id="ca38c-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="ca38c-237">（這有時也稱為「延遲要求驗證」，這是根據某些資料案例的消極式載入等詞彙）。您可以在*HTTPRUntime*專案中將*requestValidationMode*屬性設為4.5，將應用程式設定為使用 web.config 檔案中的延遲驗證，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ca38c-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="ca38c-238">當要求驗證模式設定為4.5 時，只會針對特定要求值觸發要求驗證，而且只有在您的程式碼存取該值時才會觸發。</span><span class="sxs-lookup"><span data-stu-id="ca38c-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="ca38c-239">例如，如果您的程式碼取得 Request 的值。表單 ["論壇\_文章]，只會針對表單集合中的該元素叫用要求驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="ca38c-240">不會驗證*表單*集合中的其他任何專案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="ca38c-241">在舊版的 ASP.NET 中，當存取集合中的任何元素時，會針對整個要求集合觸發要求驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="ca38c-242">新的行為讓不同的應用程式元件能夠更輕鬆地查看要求資料的不同部分，而不會在其他片段上觸發要求驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="ca38c-243">支援未驗證要求</span><span class="sxs-lookup"><span data-stu-id="ca38c-243">Support for unvalidated requests</span></span>

<span data-ttu-id="ca38c-244">延遲的要求驗證單獨無法解決選擇性略過要求驗證的問題。</span><span class="sxs-lookup"><span data-stu-id="ca38c-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="ca38c-245">對 Request 的呼叫。表單 ["論壇\_文章"] 仍會觸發該特定要求值的要求驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="ca38c-246">不過，您可能會想要在不觸發驗證的情況下存取此欄位，因為您想要允許該欄位中的標記。</span><span class="sxs-lookup"><span data-stu-id="ca38c-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="ca38c-247">為了允許這種情況，ASP.NET 4.5 現在支援對要求資料的未驗證存取。</span><span class="sxs-lookup"><span data-stu-id="ca38c-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="ca38c-248">ASP.NET 4.5 在*HttpRequest*類別中包含新的*未驗證*集合屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="ca38c-249">這個集合可讓您存取要求資料的所有通用值，例如*表單*、 *QueryString*、 *cookie*和*Url*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="ca38c-250">使用論壇範例，若要能夠讀取未驗證要求資料，您必須先將應用程式設定為使用新的要求驗證模式：</span><span class="sxs-lookup"><span data-stu-id="ca38c-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="ca38c-251">接著，您可以使用*HttpRequest. 未驗證*屬性來讀取未驗證表單值：</span><span class="sxs-lookup"><span data-stu-id="ca38c-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> <span data-ttu-id="ca38c-252">安全性-*請小心使用未驗證要求資料！*</span><span class="sxs-lookup"><span data-stu-id="ca38c-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="ca38c-253">ASP.NET 4.5 新增了未驗證要求屬性和集合，讓您更輕鬆地存取非常特定的未驗證要求資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="ca38c-254">不過，您仍然必須對未經處理的要求資料執行自訂驗證，以確保不會對使用者呈現危險的文字。</span><span class="sxs-lookup"><span data-stu-id="ca38c-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="ca38c-255">AntiXSS 程式庫</span><span class="sxs-lookup"><span data-stu-id="ca38c-255">AntiXSS Library</span></span>

<span data-ttu-id="ca38c-256">由於 Microsoft AntiXSS 程式庫的熱門程度，ASP.NET 4.5 現在包含該程式庫4.0 版的核心編碼常式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="ca38c-257">編碼常式是由新的*AntiXss*命名空間中的*AntiXssEncoder*類型所執行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="ca38c-258">您可以藉由呼叫在型別中實作為的任何靜態編碼方法，直接使用*AntiXssEncoder*類型。</span><span class="sxs-lookup"><span data-stu-id="ca38c-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="ca38c-259">不過，使用新的反 XSS 常式的最簡單方法，就是將 ASP.NET 應用程式設定為預設使用*AntiXssEncoder*類別。</span><span class="sxs-lookup"><span data-stu-id="ca38c-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="ca38c-260">若要這麼做，請將下列屬性新增至 web.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="ca38c-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="ca38c-261">當*encoderType*屬性設定為使用*AntiXssEncoder*類型時，ASP.NET 中的所有輸出編碼都會自動使用新的編碼常式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="ca38c-262">以下是外部 AntiXSS 程式庫中已併入 ASP.NET 4.5 的部分：</span><span class="sxs-lookup"><span data-stu-id="ca38c-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="ca38c-263">*HtmlEncode*、 *HtmlFormUrlEncode*和*HtmlAttributeEncode*</span><span class="sxs-lookup"><span data-stu-id="ca38c-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="ca38c-264">*XmlAttributeEncode*和*XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="ca38c-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="ca38c-265">*UrlEncode*和*UrlPathEncode* （新）</span><span class="sxs-lookup"><span data-stu-id="ca38c-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="ca38c-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="ca38c-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="ca38c-267">Websocket 通訊協定的支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="ca38c-268">Websocket 通訊協定是以標準為基礎的網路通訊協定，可定義如何透過 HTTP 在用戶端與伺服器之間建立安全的即時雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="ca38c-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="ca38c-269">Microsoft 已同時使用 IETF 和 W3C 標準內文來協助定義通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ca38c-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="ca38c-270">所有用戶端（而不只是瀏覽器）都支援 Websocket 通訊協定，而 Microsoft 會在用戶端和行動作業系統上投資支援 Websocket 通訊協定的大量資源。</span><span class="sxs-lookup"><span data-stu-id="ca38c-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="ca38c-271">Websocket 通訊協定可讓您更輕鬆地在用戶端和伺服器之間建立長時間執行的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="ca38c-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="ca38c-272">例如，撰寫聊天應用程式很容易，因為您可以在用戶端與伺服器之間建立真正的長時間執行連接。</span><span class="sxs-lookup"><span data-stu-id="ca38c-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="ca38c-273">您不需要使用定期輪詢或 HTTP 長時間輪詢等因應措施來模擬通訊端的行為。</span><span class="sxs-lookup"><span data-stu-id="ca38c-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="ca38c-274">ASP.NET 4.5 和 IIS 8 包含低層級的 Websocket 支援，讓 ASP.NET 開發人員可以使用受控 Api 以非同步方式讀取和寫入 Websocket 物件上的字串和二進位資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="ca38c-275">針對 ASP.NET 4.5，有一個新的*system.web*命名空間，其中包含用於使用 websocket 通訊協定的類型。</span><span class="sxs-lookup"><span data-stu-id="ca38c-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="ca38c-276">瀏覽器用戶端會建立 Websocket 連接，其方式是在 ASP.NET 應用程式中建立指向 URL 的 DOM *WebSocket*物件，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ca38c-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="ca38c-277">您可以使用任何類型的模組或處理常式，在 ASP.NET 中建立 Websocket 端點。</span><span class="sxs-lookup"><span data-stu-id="ca38c-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="ca38c-278">在上述範例中，使用了 ashx 檔案，因為 ashx 檔案是快速建立處理常式的方式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="ca38c-279">根據 Websocket 通訊協定，ASP.NET 應用程式會藉由指出要求應從 HTTP GET 要求升級至 Websocket 要求，來接受用戶端的 Websocket 要求。</span><span class="sxs-lookup"><span data-stu-id="ca38c-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="ca38c-280">以下為範例：</span><span class="sxs-lookup"><span data-stu-id="ca38c-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="ca38c-281">*AcceptWebSocketRequest*方法會接受函數委派，因為 ASP.NET 會回溯目前的 HTTP 要求，然後將控制權轉移至函式委派。</span><span class="sxs-lookup"><span data-stu-id="ca38c-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="ca38c-282">在概念上，此方法類似于您使用*system.object*的方式，您可以在其中定義執行背景工作的執行緒啟動委派。</span><span class="sxs-lookup"><span data-stu-id="ca38c-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="ca38c-283">在 ASP.NET 且用戶端成功完成 Websocket 交握之後，ASP.NET 會呼叫您的委派，而 Websocket 應用程式會開始執行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="ca38c-284">下列程式碼範例顯示在 ASP.NET 中使用內建 Websocket 支援的簡單回應應用程式：</span><span class="sxs-lookup"><span data-stu-id="ca38c-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="ca38c-285">適用于*await*關鍵字和非同步工作型作業的 .net 4.5 支援，是撰寫 websocket 應用程式的自然配合。</span><span class="sxs-lookup"><span data-stu-id="ca38c-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="ca38c-286">此程式碼範例顯示 Websocket 要求在 ASP.NET 內完全以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="ca38c-287">應用程式會藉由呼叫 await socket，以非同步方式等待訊息傳送給用戶端 *。ReceiveAsync*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="ca38c-288">同樣地，您可以藉由呼叫 await socket，將非同步訊息傳送至用戶端 *。SendAsync*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="ca38c-289">在瀏覽器中，應用程式會透過*onmessage*函數來接收 websocket 訊息。</span><span class="sxs-lookup"><span data-stu-id="ca38c-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="ca38c-290">若要從瀏覽器傳送訊息，您可以呼叫*WebSocket* DOM 類型的*send*方法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ca38c-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="ca38c-291">在未來，我們可能會發行這項功能的更新，以抽象化此版本針對 Websocket 應用程式所需的一些低層級編碼。</span><span class="sxs-lookup"><span data-stu-id="ca38c-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="ca38c-292">統合和縮製</span><span class="sxs-lookup"><span data-stu-id="ca38c-292">Bundling and Minification</span></span>

<span data-ttu-id="ca38c-293">「配套」可讓您將個別的 JavaScript 和 CSS 檔案結合成可視為單一檔案的組合。</span><span class="sxs-lookup"><span data-stu-id="ca38c-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="ca38c-294">縮制總是 JavaScript 和 CSS 檔案，方法是移除不必要的空白字元和其他字元。</span><span class="sxs-lookup"><span data-stu-id="ca38c-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="ca38c-295">這些功能適用 Web form、ASP.NET MVC 和網頁。</span><span class="sxs-lookup"><span data-stu-id="ca38c-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="ca38c-296">套件組合是使用配套類別或其中一個子類別（ScriptBundle 和 StyleBundle）所建立。</span><span class="sxs-lookup"><span data-stu-id="ca38c-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="ca38c-297">設定配套的實例之後，只要將套組新增至全域 BundleCollection 實例，就可以將該組合提供給傳入的要求。</span><span class="sxs-lookup"><span data-stu-id="ca38c-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="ca38c-298">在預設範本中，配套設定會在 Bundleconfig.json 檔案中執行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="ca38c-299">此預設設定會為範本所使用的所有核心腳本和 css 檔案建立配套。</span><span class="sxs-lookup"><span data-stu-id="ca38c-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="ca38c-300">使用其中一種可能的 helper 方法，從 views 內參考配套。</span><span class="sxs-lookup"><span data-stu-id="ca38c-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="ca38c-301">為了支援在 debug 與 release 模式下轉譯組合的不同標記，ScriptBundle 和 StyleBundle 類別具有 helper 方法，呈現。</span><span class="sxs-lookup"><span data-stu-id="ca38c-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="ca38c-302">在 [偵錯工具] 模式中，Render 會針對組合中的每個資源產生標記。</span><span class="sxs-lookup"><span data-stu-id="ca38c-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="ca38c-303">在發行模式中，Render 會為整個組合產生單一標記元素。</span><span class="sxs-lookup"><span data-stu-id="ca38c-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="ca38c-304">在 web.config 中修改編譯專案的 debug 屬性，即可在 debug 和 release 模式之間切換，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ca38c-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="ca38c-305">此外，您可以直接透過當. EnableOptimizations 屬性來設定啟用或停用優化。</span><span class="sxs-lookup"><span data-stu-id="ca38c-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="ca38c-306">當檔案已配套時，首先會依字母順序排序（顯示在**方案總管**中的方式）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="ca38c-307">然後會進行組織，以便先載入已知的程式庫及其自訂擴充功能（例如 jQuery、MooTools 和 Dojo）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="ca38c-308">例如，如上所示，腳本資料夾的組合最終順序將會是：</span><span class="sxs-lookup"><span data-stu-id="ca38c-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="ca38c-309">jquery-1.7.2.min.js 1.6.2 .js</span><span class="sxs-lookup"><span data-stu-id="ca38c-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="ca38c-310">jquery-ui .js</span><span class="sxs-lookup"><span data-stu-id="ca38c-310">jquery-ui.js</span></span>
3. <span data-ttu-id="ca38c-311">jquery. tools .js</span><span class="sxs-lookup"><span data-stu-id="ca38c-311">jquery.tools.js</span></span>
4. <span data-ttu-id="ca38c-312">.js</span><span class="sxs-lookup"><span data-stu-id="ca38c-312">a.js</span></span>

<span data-ttu-id="ca38c-313">CSS 檔案也會依字母順序排序，然後再重新組織，以便重設 .css 和正規化。 css 會在任何其他檔案之前。</span><span class="sxs-lookup"><span data-stu-id="ca38c-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="ca38c-314">如上所示的 [樣式] 資料夾組合的最終排序將會是：</span><span class="sxs-lookup"><span data-stu-id="ca38c-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="ca38c-315">重設 .css</span><span class="sxs-lookup"><span data-stu-id="ca38c-315">reset.css</span></span>
2. <span data-ttu-id="ca38c-316">content .css</span><span class="sxs-lookup"><span data-stu-id="ca38c-316">content.css</span></span>
3. <span data-ttu-id="ca38c-317">forms .css</span><span class="sxs-lookup"><span data-stu-id="ca38c-317">forms.css</span></span>
4. <span data-ttu-id="ca38c-318">globals</span><span class="sxs-lookup"><span data-stu-id="ca38c-318">globals.css</span></span>
5. <span data-ttu-id="ca38c-319">menu .css</span><span class="sxs-lookup"><span data-stu-id="ca38c-319">menu.css</span></span>
6. <span data-ttu-id="ca38c-320">樣式 .css</span><span class="sxs-lookup"><span data-stu-id="ca38c-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="ca38c-321">Web 裝載的效能改進</span><span class="sxs-lookup"><span data-stu-id="ca38c-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="ca38c-322">.NET Framework 4.5 和 Windows 8 引進的功能，可協助您大幅提升 web 伺服器工作負載的效能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="ca38c-323">這包括減少（最多35%）在啟動期間，以及使用 ASP.NET 之 web 主控網站的記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="ca38c-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="ca38c-324">關鍵效能因素</span><span class="sxs-lookup"><span data-stu-id="ca38c-324">Key performance factors</span></span>

<span data-ttu-id="ca38c-325">在理想的情況下，所有網站都應該在使用中，且在記憶體中，以確保在每次收到要求時都能快速回應。</span><span class="sxs-lookup"><span data-stu-id="ca38c-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="ca38c-326">可能會影響網站回應性的因素包括：</span><span class="sxs-lookup"><span data-stu-id="ca38c-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="ca38c-327">在應用程式集區回收之後，網站重新開機所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="ca38c-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="ca38c-328">這是當網站元件不再位於記憶體中時，啟動網站的 web 伺服器進程所需的時間。</span><span class="sxs-lookup"><span data-stu-id="ca38c-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="ca38c-329">（平臺元件仍然在記憶體中，因為其他網站會使用它們）。這種情況稱為「冷網站、暖架構啟動」，或只是「冷網站啟動」。</span><span class="sxs-lookup"><span data-stu-id="ca38c-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="ca38c-330">網站佔用的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="ca38c-330">How much memory the site occupies.</span></span> <span data-ttu-id="ca38c-331">這是「每個網站的記憶體耗用量」或「取消共用的工作集」。</span><span class="sxs-lookup"><span data-stu-id="ca38c-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="ca38c-332">新的效能改進著重于這兩個因素。</span><span class="sxs-lookup"><span data-stu-id="ca38c-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="ca38c-333">新效能功能的需求</span><span class="sxs-lookup"><span data-stu-id="ca38c-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="ca38c-334">新功能的需求可以細分成下列類別：</span><span class="sxs-lookup"><span data-stu-id="ca38c-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="ca38c-335">在 .NET Framework 4 上執行的改善。</span><span class="sxs-lookup"><span data-stu-id="ca38c-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="ca38c-336">需要 .NET Framework 4.5 的改良功能，但可以在任何版本的 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="ca38c-337">僅適用于在 Windows 8 上執行 .NET Framework 4.5 的改進功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="ca38c-338">效能會隨著您能夠啟用的每個改善層級而增加。</span><span class="sxs-lookup"><span data-stu-id="ca38c-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="ca38c-339">其中一些 .NET Framework 的4.5 改良功能可充分利用適用于其他案例的更廣泛效能功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="ca38c-340">共用萬用群組件</span><span class="sxs-lookup"><span data-stu-id="ca38c-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="ca38c-341">**需求**： .NET Framework 4 和 Visual Studio 11 開發人員預覽 SDK</span><span class="sxs-lookup"><span data-stu-id="ca38c-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="ca38c-342">伺服器上的不同網站通常會使用相同的 helper 元件（例如，來自入門套件或範例應用程式的元件）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="ca38c-343">每個網站在其 Bin 目錄中都有自己的這些元件複本。</span><span class="sxs-lookup"><span data-stu-id="ca38c-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="ca38c-344">雖然元件的物件程式碼完全相同，但它們實際上是不同的元件，因此在冷網站啟動時，每個元件都必須分別讀取，並在記憶體中分開保存。</span><span class="sxs-lookup"><span data-stu-id="ca38c-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="ca38c-345">新的暫存功能可解決這種效率，並減少 RAM 需求和載入時間。</span><span class="sxs-lookup"><span data-stu-id="ca38c-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="ca38c-346">「暫留」可讓 Windows 在檔案系統中保留每個元件的單一複本，而網站 Bin 資料夾中的個別元件則會以單一複本的符號連結來取代。</span><span class="sxs-lookup"><span data-stu-id="ca38c-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="ca38c-347">如果個別網站需要元件的不同版本，則符號連結會取代為元件的新版本，而且只有該網站會受到影響。</span><span class="sxs-lookup"><span data-stu-id="ca38c-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="ca38c-348">使用符號連結共用元件需要一個名為 aspnet 的新工具\_appcmd.exe，這可讓您建立和管理已留用元件的存放區。</span><span class="sxs-lookup"><span data-stu-id="ca38c-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="ca38c-349">它是以 Visual Studio 11 開發人員預覽 SDK 的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="ca38c-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="ca38c-350">（不過，如果您已安裝最新的[更新](https://support.microsoft.com/kb/2468871)，它將會在只安裝 .NET Framework 4 的系統上工作。）</span><span class="sxs-lookup"><span data-stu-id="ca38c-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="ca38c-351">為了確保所有合格的元件都已暫留，您會定期執行 aspnet\_實習（例如，一週一次，做為排定的工作）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="ca38c-352">一般的用法如下所示：</span><span class="sxs-lookup"><span data-stu-id="ca38c-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="ca38c-353">若要查看所有選項，請執行不含引數的工具。</span><span class="sxs-lookup"><span data-stu-id="ca38c-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="ca38c-354">使用多核心 JIT 編譯加快啟動速度</span><span class="sxs-lookup"><span data-stu-id="ca38c-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="ca38c-355">**需求**： .NET Framework 4。5</span><span class="sxs-lookup"><span data-stu-id="ca38c-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="ca38c-356">在冷網站啟動時，不僅需要從磁片讀取元件，還必須以 JIT 編譯網站。</span><span class="sxs-lookup"><span data-stu-id="ca38c-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="ca38c-357">針對複雜的網站，這可能會增加顯著的延遲。</span><span class="sxs-lookup"><span data-stu-id="ca38c-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="ca38c-358">.NET Framework 4.5 中的新一般用途技術，會將 JIT 編譯分散到可用的處理器核心，以減少這些延遲。</span><span class="sxs-lookup"><span data-stu-id="ca38c-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="ca38c-359">它會使用上一次啟動網站時所收集的資訊，盡可能地儘早執行此工作。</span><span class="sxs-lookup"><span data-stu-id="ca38c-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="ca38c-360">這項功能是由[ProfileOptimization. StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法所執行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="ca38c-361">預設會在 ASP.NET 中啟用使用多個核心的 JIT 編譯，因此您不需要執行任何動作，即可充分利用這項功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="ca38c-362">如果您想要停用此功能，請在 web.config 檔案中進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="ca38c-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="ca38c-363">微調垃圾收集以優化記憶體</span><span class="sxs-lookup"><span data-stu-id="ca38c-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="ca38c-364">**需求**： .NET Framework 4。5</span><span class="sxs-lookup"><span data-stu-id="ca38c-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="ca38c-365">一旦網站執行之後，使用垃圾收集行程（GC）堆積可能是其記憶體耗用量的重要因素。</span><span class="sxs-lookup"><span data-stu-id="ca38c-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="ca38c-366">就像任何垃圾收集行程一樣，.NET Framework GC 會在 CPU 時間（集合的頻率和重要性）和記憶體耗用量（用於新的、已釋放或可釋放的物件的額外空間）之間做出取捨。</span><span class="sxs-lookup"><span data-stu-id="ca38c-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="ca38c-367">在先前的版本中，我們已提供如何設定 GC 以達到適當平衡的指引（例如，請參閱[ASP.NET 2.0/3.5 共用裝載](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)設定）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="ca38c-368">針對 .NET Framework 4.5，而不是多個獨立設定，可以使用工作負載定義的設定，以啟用所有先前建議的 GC 設定，以及新的微調，為每個網站提供額外的效能工作集。</span><span class="sxs-lookup"><span data-stu-id="ca38c-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="ca38c-369">若要啟用 GC 記憶體微調，請將下列設定新增至 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="ca38c-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="ca38c-370">（如果您熟悉先前的 aspnet 變更指引，請注意，此設定會取代舊的設定，例如，不需要設定 gcServer、gcConcurrent 等。您不需要移除舊的設定）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="ca38c-371">預先提取 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca38c-371">Prefetching for web applications</span></span>

<span data-ttu-id="ca38c-372">**需求**：在 Windows 8 上執行 .NET Framework 4。5</span><span class="sxs-lookup"><span data-stu-id="ca38c-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="ca38c-373">針對數個版本，Windows 已包含稱為[prefetcher](http://en.wikipedia.org/wiki/Prefetcher)的技術，可減少應用程式啟動的磁片讀取成本。</span><span class="sxs-lookup"><span data-stu-id="ca38c-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="ca38c-374">由於冷啟動是主要針對用戶端應用程式的問題，因此這項技術並未包含在 Windows Server 中，只包含對伺服器而言是必要的元件。</span><span class="sxs-lookup"><span data-stu-id="ca38c-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="ca38c-375">預先提取已在最新版的 Windows Server 中提供，可讓您將個別網站的啟動優化。</span><span class="sxs-lookup"><span data-stu-id="ca38c-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="ca38c-376">對於 Windows Server，預設不會啟用 prefetcher。</span><span class="sxs-lookup"><span data-stu-id="ca38c-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="ca38c-377">若要啟用和設定高密度 web 裝載的 prefetcher，請在命令列執行下列命令集：</span><span class="sxs-lookup"><span data-stu-id="ca38c-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="ca38c-378">然後，若要將 prefetcher 與 ASP.NET 應用程式整合，請將下列內容新增至 web.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="ca38c-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="ca38c-379">ASP.NET Web Form</span><span class="sxs-lookup"><span data-stu-id="ca38c-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="ca38c-380">強型別資料控制項</span><span class="sxs-lookup"><span data-stu-id="ca38c-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="ca38c-381">在 ASP.NET 4.5 中，Web Forms 包含一些使用資料的改良功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="ca38c-382">第一種改進是強型別資料控制措施。</span><span class="sxs-lookup"><span data-stu-id="ca38c-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="ca38c-383">若是舊版 ASP.NET 中的 Web form 控制項，您可以使用*Eval*和資料系結運算式來顯示資料系結值：</span><span class="sxs-lookup"><span data-stu-id="ca38c-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="ca38c-384">針對雙向資料系結，您可以使用*Bind*：</span><span class="sxs-lookup"><span data-stu-id="ca38c-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="ca38c-385">在執行時間，這些呼叫會使用反映來讀取指定成員的值，然後在標記中顯示結果。</span><span class="sxs-lookup"><span data-stu-id="ca38c-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="ca38c-386">這種方法可讓您輕鬆地將資料系結到任意的 unshaped 資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="ca38c-387">不過，像這樣的資料系結運算式不支援成員名稱的 IntelliSense、導覽（例如 [移至定義]），或這些名稱的編譯時間檢查等功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="ca38c-388">為了解決這個問題，ASP.NET 4.5 加入了宣告控制項所系結資料之資料類型的功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="ca38c-389">您可以使用新的*ItemType*屬性來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="ca38c-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="ca38c-390">當您設定這個屬性時，資料系結運算式的範圍中會提供兩個新的具類型變數： *Item*和*BindItem*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="ca38c-391">因為變數是強型別，所以您可以獲得 Visual Studio 開發經驗的完整優勢。</span><span class="sxs-lookup"><span data-stu-id="ca38c-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>

<span data-ttu-id="ca38c-392">若為雙向資料系結運算式，請使用*BindItem*變數：</span><span class="sxs-lookup"><span data-stu-id="ca38c-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

<span data-ttu-id="ca38c-393">ASP.NET Web form 架構中支援資料系結的大部分控制項都已更新，以支援*ItemType*屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="ca38c-394">模型繫結</span><span class="sxs-lookup"><span data-stu-id="ca38c-394">Model Binding</span></span>

<span data-ttu-id="ca38c-395">模型系結會擴充 ASP.NET Web form 控制項中的資料系結，以使用以程式碼為主的資料存取。</span><span class="sxs-lookup"><span data-stu-id="ca38c-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="ca38c-396">它結合了*ObjectDataSource*控制項的概念，以及從 ASP.NET MVC 中的模型系結。</span><span class="sxs-lookup"><span data-stu-id="ca38c-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="ca38c-397">選取資料</span><span class="sxs-lookup"><span data-stu-id="ca38c-397">Selecting data</span></span>

<span data-ttu-id="ca38c-398">若要將資料控制項設定為使用模型系結來選取資料，請將控制項的 [ *SelectMethod* ] 屬性設為頁面程式碼中的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="ca38c-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="ca38c-399">資料控制項會在頁面生命週期的適當時間呼叫方法，並自動系結傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="ca38c-400">不需要明確地呼叫*DataBind*方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="ca38c-401">在下列範例中， *GridView*控制項已設定為使用名為*GetCategories*的方法：</span><span class="sxs-lookup"><span data-stu-id="ca38c-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="ca38c-402">您會在頁面的程式碼中建立*GetCategories*方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="ca38c-403">針對簡單的 select 作業，方法不需要任何參數，而且應該傳回*IEnumerable*或*IQueryable*物件。</span><span class="sxs-lookup"><span data-stu-id="ca38c-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="ca38c-404">如果設定了新的*ItemType*屬性（如稍早的強型別[資料控制](#_Toc318097386)項所述，它會啟用強型別資料系結運算式），則應該傳回這些介面的泛型版本— *IEnumerable&lt;T&gt;* 或*IQueryable&lt;t&gt;* ，其中*t*參數符合*ItemType*屬性的類型（例如， *IQueryable&lt;Category&gt;* ）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="ca38c-405">下列範例顯示*GetCategories*方法的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca38c-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="ca38c-406">這個範例會使用 Entity Framework 的 Code First 模型搭配 Northwind 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca38c-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="ca38c-407">此程式碼可確保查詢會透過*Include*方法，傳回每個類別之相關產品的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="ca38c-408">（這可確保標記中的*TemplateField*元素會顯示每個類別中的產品計數，而不需要[n + 1 選取](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="ca38c-409">當頁面執行時， *GridView*控制項會自動呼叫*GetCategories*方法，並使用已設定的欄位呈現傳回的資料：</span><span class="sxs-lookup"><span data-stu-id="ca38c-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="ca38c-410">因為 select 方法會傳回*IQueryable*物件，所以*GridView*控制項可以在執行查詢之前進一步操作。</span><span class="sxs-lookup"><span data-stu-id="ca38c-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="ca38c-411">例如， *GridView*控制項可以加入查詢運算式，以便在執行之前對傳回的*IQueryable*物件進行排序和分頁，以便由基礎 LINQ 提供者執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="ca38c-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="ca38c-412">在此情況下，Entity Framework 將確保這些作業會在資料庫中執行。</span><span class="sxs-lookup"><span data-stu-id="ca38c-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="ca38c-413">下列範例顯示已修改成允許排序和分頁的*GridView*控制項：</span><span class="sxs-lookup"><span data-stu-id="ca38c-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="ca38c-414">現在當頁面執行時，控制項可以確保只會顯示目前的資料頁面，並依選取的欄排序：</span><span class="sxs-lookup"><span data-stu-id="ca38c-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="ca38c-415">若要篩選傳回的資料，必須將參數加入至 select 方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="ca38c-416">在執行時間，模型系結會填入這些參數，您可以使用它們來改變查詢，然後再傳回資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="ca38c-417">例如，假設您想要讓使用者在查詢字串中輸入關鍵字來篩選產品。</span><span class="sxs-lookup"><span data-stu-id="ca38c-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="ca38c-418">您可以將參數新增至方法，並更新程式碼以使用參數值：</span><span class="sxs-lookup"><span data-stu-id="ca38c-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="ca38c-419">如果為*關鍵字*提供了值，則此程式碼會包含*Where*運算式，然後傳回查詢結果。</span><span class="sxs-lookup"><span data-stu-id="ca38c-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="ca38c-420">值提供者</span><span class="sxs-lookup"><span data-stu-id="ca38c-420">Value providers</span></span>

<span data-ttu-id="ca38c-421">先前的範例並未特別說明*關鍵字*參數的值是來自何處。</span><span class="sxs-lookup"><span data-stu-id="ca38c-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="ca38c-422">若要指出此資訊，您可以使用參數屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="ca38c-423">在此範例中，您可以使用*ModelBinding*命名空間中的*QueryStringAttribute*類別：</span><span class="sxs-lookup"><span data-stu-id="ca38c-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="ca38c-424">這會指示模型系結嘗試在執行時間將值從查詢字串系結至*關鍵字*參數。</span><span class="sxs-lookup"><span data-stu-id="ca38c-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="ca38c-425">（這可能牽涉到執行類型轉換，但在此情況下不會這麼做）。如果無法提供值，而且類型不可為 null，就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ca38c-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="ca38c-426">這些方法的值來源稱為「值提供者」，而參數屬性則表示要使用哪一個值提供者稱為「值提供者」屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="ca38c-427">Web form 會針對 Web Forms 應用程式中使用者輸入的所有一般來源（例如查詢字串、cookie、表單值、控制項、檢視狀態、會話狀態和配置檔案屬性），包含值提供者和對應的屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="ca38c-428">您也可以撰寫自訂值提供者。</span><span class="sxs-lookup"><span data-stu-id="ca38c-428">You can also write custom value providers.</span></span>

<span data-ttu-id="ca38c-429">根據預設，參數名稱會用來做為在值提供者集合中尋找值的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ca38c-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="ca38c-430">在此範例中，程式碼會尋找名為關鍵字的查詢字串值（例如 ~/default.aspx？關鍵字 = chef）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="ca38c-431">您可以指定自訂索引鍵，其方式是將它當做引數傳遞給參數屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="ca38c-432">例如，若要使用名為 q 的查詢字串變數值，您可以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="ca38c-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="ca38c-433">如果這個方法是在頁面的程式碼中，使用者可以使用查詢字串傳遞關鍵字來篩選結果：</span><span class="sxs-lookup"><span data-stu-id="ca38c-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="ca38c-434">模型系結會完成許多您原本就必須手動編寫程式碼的工作：讀取值、檢查是否有 null 值、嘗試將它轉換成適當的類型、檢查轉換是否成功，最後使用中的值。查詢.</span><span class="sxs-lookup"><span data-stu-id="ca38c-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="ca38c-435">模型系結會產生較少的程式碼，而且能夠在整個應用程式中重複使用功能。</span><span class="sxs-lookup"><span data-stu-id="ca38c-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="ca38c-436">依控制項中的值篩選</span><span class="sxs-lookup"><span data-stu-id="ca38c-436">Filtering by values from a control</span></span>

<span data-ttu-id="ca38c-437">假設您想要擴充範例，讓使用者從下拉式清單中選擇篩選值。</span><span class="sxs-lookup"><span data-stu-id="ca38c-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="ca38c-438">將下列下拉式清單新增至標記，並將它設定為使用*SelectMethod*屬性從另一個方法取得其資料：</span><span class="sxs-lookup"><span data-stu-id="ca38c-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="ca38c-439">通常您也會將*EmptyDataTemplate*專案新增至*GridView*控制項，如此一來，當找不到相符的產品時，控制項就會顯示訊息：</span><span class="sxs-lookup"><span data-stu-id="ca38c-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="ca38c-440">在頁面程式碼中，為下拉式清單加入新的 select 方法：</span><span class="sxs-lookup"><span data-stu-id="ca38c-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="ca38c-441">最後，更新*GetProducts* select 方法以接受新的參數，其中包含下拉式清單中所選取類別的識別碼：</span><span class="sxs-lookup"><span data-stu-id="ca38c-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="ca38c-442">現在當頁面執行時，使用者可以從下拉式清單中選取類別，而*GridView*控制項會自動重新系結以顯示篩選過的資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="ca38c-443">這是可行的，因為模型系結會追蹤 select 方法的參數值，並偵測回傳後是否有任何參數值變更。</span><span class="sxs-lookup"><span data-stu-id="ca38c-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="ca38c-444">若是如此，模型系結會強制相關聯的資料控制項重新系結至資料。</span><span class="sxs-lookup"><span data-stu-id="ca38c-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="ca38c-445">HTML 編碼的資料系結運算式</span><span class="sxs-lookup"><span data-stu-id="ca38c-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="ca38c-446">您現在可以對資料系結運算式的結果進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="ca38c-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="ca38c-447">新增冒號（:)至標示資料系結運算式之 &lt;% # 前置詞的結尾：</span><span class="sxs-lookup"><span data-stu-id="ca38c-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="ca38c-448">不顯眼的驗證</span><span class="sxs-lookup"><span data-stu-id="ca38c-448">Unobtrusive Validation</span></span>

<span data-ttu-id="ca38c-449">您現在可以設定內建的驗證器控制項，針對用戶端驗證邏輯使用不顯眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="ca38c-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="ca38c-450">這會大幅減少在頁面標記中內嵌呈現的 JavaScript 數量，並減少整體頁面大小。</span><span class="sxs-lookup"><span data-stu-id="ca38c-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="ca38c-451">您可以透過下列任一種方式，為驗證程式控制項設定不顯眼的 JavaScript：</span><span class="sxs-lookup"><span data-stu-id="ca38c-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="ca38c-452">將下列設定加入 Web.config 檔案中的 *&lt;appSettings&gt;* 元素，以全域方式執行：</span><span class="sxs-lookup"><span data-stu-id="ca38c-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="ca38c-453">全域方式，將*UnobtrusiveValidationMode*屬性設定為*UnobtrusiveValidationMode. WebForms* （通常是在*Application\_* global.asax 檔案中的 Start 方法）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="ca38c-454">藉由將*頁面*類別的新*UnobtrusiveValidationMode*屬性設定為*UnobtrusiveValidationMode*，來個別取得頁面。</span><span class="sxs-lookup"><span data-stu-id="ca38c-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="ca38c-455">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="ca38c-455">HTML5 Updates</span></span>

<span data-ttu-id="ca38c-456">Web form 伺服器控制項已有一些改進，可利用 HTML5 的新功能：</span><span class="sxs-lookup"><span data-stu-id="ca38c-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="ca38c-457">*TextBox*控制項的*TextMode*屬性已更新為支援新的 HTML5 輸入類型，例如*電子郵件*、*日期時間*等等。</span><span class="sxs-lookup"><span data-stu-id="ca38c-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="ca38c-458">*FileUpload*控制項現在支援從支援此 HTML5 功能的瀏覽器進行多個檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="ca38c-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="ca38c-459">驗證程式控制項現在支援驗證 HTML5 輸入元素。</span><span class="sxs-lookup"><span data-stu-id="ca38c-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="ca38c-460">具有代表 URL 之屬性的新 HTML5 元素現在支援 runat = "server"。</span><span class="sxs-lookup"><span data-stu-id="ca38c-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="ca38c-461">因此，您可以使用 URL 路徑中的 ASP.NET 慣例，例如 ~ 運算子來代表應用程式根目錄（例如，&lt;video runat = "server" src = "~/myVideo.wmv"/&gt;）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="ca38c-462">已修正*UpdatePanel*控制項，以支援張貼 HTML5 輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="ca38c-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="ca38c-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="ca38c-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="ca38c-464">ASP.NET MVC 4 Beta 現已包含在 Visual Studio 11 Beta 中。</span><span class="sxs-lookup"><span data-stu-id="ca38c-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="ca38c-465">ASP.NET MVC 是一種架構，可讓您利用模型視圖控制器（MVC）模式來開發高度可測試且可維護的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="ca38c-466">ASP.NET MVC 4 可讓您輕鬆地建立行動 Web 應用程式，並包含 ASP.NET Web API，這可協助您建立可連線到任何裝置的 HTTP 服務。</span><span class="sxs-lookup"><span data-stu-id="ca38c-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="ca38c-467">如需詳細資訊，請參閱[ASP.NET MVC 4 版本](mvc4-release-notes.md)資訊。</span><span class="sxs-lookup"><span data-stu-id="ca38c-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="ca38c-468">ASP.NET Web Pages 2</span><span class="sxs-lookup"><span data-stu-id="ca38c-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="ca38c-469">新功能包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="ca38c-469">New features include the following:</span></span>

- <span data-ttu-id="ca38c-470">新增及更新的網站範本。</span><span class="sxs-lookup"><span data-stu-id="ca38c-470">New and updated site templates.</span></span>
- <span data-ttu-id="ca38c-471">使用*驗證*協助程式新增伺服器端和用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="ca38c-472">使用資產管理員註冊腳本的能力。</span><span class="sxs-lookup"><span data-stu-id="ca38c-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="ca38c-473">使用 OAuth 和 OpenID 啟用 Facebook 和其他網站的登入。</span><span class="sxs-lookup"><span data-stu-id="ca38c-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="ca38c-474">使用*地圖*服務協助程式新增對應。</span><span class="sxs-lookup"><span data-stu-id="ca38c-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="ca38c-475">並存執行 Web Pages 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="ca38c-476">行動裝置的轉譯頁面。</span><span class="sxs-lookup"><span data-stu-id="ca38c-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="ca38c-477">如需這些功能和完整頁面程式碼範例的詳細資訊，請參閱[Web Pages 2 Beta 中的最上層功能](https://go.microsoft.com/fwlink/?LinkID=227824)。</span><span class="sxs-lookup"><span data-stu-id="ca38c-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="ca38c-478">Visual Web Developer 11 搶鮮版（Beta）</span><span class="sxs-lookup"><span data-stu-id="ca38c-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="ca38c-479">本節提供 Visual Web Developer 11 Beta 和 Visual Studio 2012 候選版中的網頁程式開發改良功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ca38c-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="ca38c-480">Visual Studio 2010 和 Visual Studio 2012 候選版之間的專案共用（專案相容性）</span><span class="sxs-lookup"><span data-stu-id="ca38c-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="ca38c-481">在 Visual Studio 2012 候選版之前，在較新版本的中開啟現有專案 Visual Studio 啟動轉換向導。</span><span class="sxs-lookup"><span data-stu-id="ca38c-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="ca38c-482">這會強制將專案和方案的內容（資產）升級為新格式，而這些格式無法回溯相容。</span><span class="sxs-lookup"><span data-stu-id="ca38c-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="ca38c-483">因此，在轉換之後，您無法在舊版的 Visual Studio 中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="ca38c-484">許多客戶告訴我們，這不是正確的方法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="ca38c-485">在 Visual Studio 11 搶鮮版（Beta）中，我們現在支援使用 Visual Studio 2010 SP1 來共用專案和解決方案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="ca38c-486">這表示如果您在 Visual Studio 2012 候選版中開啟2010專案，仍然可以在 Visual Studio 2010 SP1 中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="ca38c-487">有幾種類型的專案無法在 Visual Studio 2010 SP1 和 Visual Studio 2012 候選版之間共用。</span><span class="sxs-lookup"><span data-stu-id="ca38c-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="ca38c-488">其中包括一些較舊的專案（例如 ASP.NET MVC 2 專案），或用於特殊用途的專案（例如安裝專案）。</span><span class="sxs-lookup"><span data-stu-id="ca38c-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="ca38c-489">當您第一次在 Visual Studio 11 Beta 中開啟 Visual Studio 2010 SP1 Web 專案時，會將下列屬性新增至專案檔：</span><span class="sxs-lookup"><span data-stu-id="ca38c-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="ca38c-490">FileUpgradeFlags</span><span class="sxs-lookup"><span data-stu-id="ca38c-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="ca38c-491">UpgradeBackupLocation</span><span class="sxs-lookup"><span data-stu-id="ca38c-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="ca38c-492">OldToolsVersion</span><span class="sxs-lookup"><span data-stu-id="ca38c-492">OldToolsVersion</span></span>
- <span data-ttu-id="ca38c-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="ca38c-493">VisualStudioVersion</span></span>
- <span data-ttu-id="ca38c-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="ca38c-494">VSToolsPath</span></span>

<span data-ttu-id="ca38c-495">升級專案檔的進程會使用 FileUpgradeFlags、UpgradeBackupLocation 和 OldToolsVersion。</span><span class="sxs-lookup"><span data-stu-id="ca38c-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="ca38c-496">它們不會影響在 Visual Studio 2010 中使用專案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="ca38c-497">VisualStudioVersion 是 MSBuild 4.5 用來指出目前專案之 Visual Studio 版本的新屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="ca38c-498">因為此屬性不存在於 MSBuild 4.0 中（Visual Studio 2010 SP1 所使用的 MSBuild 版本），所以我們會將預設值插入專案檔中。</span><span class="sxs-lookup"><span data-stu-id="ca38c-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="ca38c-499">VSToolsPath 屬性是用來判斷要從 MSBuildExtensionsPath32 設定所代表的路徑匯入的正確 .targets 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="ca38c-500">此外，還有一些與 Import 元素相關的變更。</span><span class="sxs-lookup"><span data-stu-id="ca38c-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="ca38c-501">必須進行這些變更，才能支援兩個版本 Visual Studio 之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="ca38c-502">如果專案是在兩部不同電腦的 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 之間共用，而且如果專案在應用程式\_資料夾中包含本機資料庫，您就必須確定資料庫所使用的 SQL Server 版本已安裝在兩部電腦上。</span><span class="sxs-lookup"><span data-stu-id="ca38c-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="ca38c-503">ASP.NET 4.5 網站範本中的設定變更</span><span class="sxs-lookup"><span data-stu-id="ca38c-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="ca38c-504">在 Visual Studio 2012 候選版中使用網站範本所建立*之網站的預設 web.config*檔案已進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="ca38c-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="ca38c-505">在 `<httpRuntime>` 元素中，現在預設會設定 `encoderType` 屬性，以使用已加入至 ASP.NET 的 AntiXSS 類型。</span><span class="sxs-lookup"><span data-stu-id="ca38c-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="ca38c-506">如需詳細資訊，請參閱[AntiXSS 程式庫](#_Toc318097382)。</span><span class="sxs-lookup"><span data-stu-id="ca38c-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="ca38c-507">此外，在 `<httpRuntime>` 元素中，`requestValidationMode` 屬性會設定為 "4.5"。</span><span class="sxs-lookup"><span data-stu-id="ca38c-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="ca38c-508">這表示根據預設，要求驗證會設定為使用延後（「延遲」）驗證。</span><span class="sxs-lookup"><span data-stu-id="ca38c-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="ca38c-509">如需詳細資訊，請參閱[新的 ASP.NET 要求驗證功能](#_Toc318097379)。</span><span class="sxs-lookup"><span data-stu-id="ca38c-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="ca38c-510">`<system.webServer>` 區段的 `<modules>` 元素不包含 `runAllManagedModulesForAllRequests` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="ca38c-511">（其預設值為 false）。這表示如果您使用的 IIS 7 版本尚未更新為 SP1，您可能會遇到新網站中的路由問題。</span><span class="sxs-lookup"><span data-stu-id="ca38c-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="ca38c-512">如需詳細資訊，請參閱[IIS 7 中針對 ASP.NET 路由的原生支援](#Native_Support_In_IIS7_For_ASPNET_Routine)。</span><span class="sxs-lookup"><span data-stu-id="ca38c-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="ca38c-513">這些變更不會影響現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="ca38c-514">不過，它們可能代表現有網站與您使用新範本為 ASP.NET 4.5 建立的新網站之間的行為差異。</span><span class="sxs-lookup"><span data-stu-id="ca38c-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="ca38c-515">IIS 7 中用於 ASP.NET 路由的原生支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="ca38c-516">這不是 ASP.NET 的變更，但如果您使用的是未套用 SP1 更新的 IIS 7 版本，新網站專案的範本變更可能會影響您。</span><span class="sxs-lookup"><span data-stu-id="ca38c-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="ca38c-517">在 ASP.NET 中，您可以在應用程式中新增下列設定，以便支援路由：</span><span class="sxs-lookup"><span data-stu-id="ca38c-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="ca38c-518">當**runAllManagedModulesForAllRequests**為 true 時，像 `http://mysite/myapp/home` 之類的 url 就會移至 ASP.NET，即使 url 上沒有 *.aspx*、 *mvc*或類似的延伸模組也是一樣。</span><span class="sxs-lookup"><span data-stu-id="ca38c-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="ca38c-519">對 IIS 7 進行的更新會使**runAllManagedModulesForAllRequests**設定不必要，並以原生方式支援 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="ca38c-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="ca38c-520">（如需更新的詳細資訊，請參閱 Microsoft 支援服務[一文，其中提供可讓特定 IIS 7.0 或 IIS 7.5 處理常式處理其 url 結尾不是句號的要求](https://support.microsoft.com/kb/980368)）的更新。</span><span class="sxs-lookup"><span data-stu-id="ca38c-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="ca38c-521">如果您的網站是在 IIS 7 上執行，而且 IIS 已更新，您就不需要將**runAllManagedModulesForAllRequests**設定為 true。</span><span class="sxs-lookup"><span data-stu-id="ca38c-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="ca38c-522">事實上，不建議將它設定為 true，因為它會對要求增加不必要的處理負荷。</span><span class="sxs-lookup"><span data-stu-id="ca38c-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="ca38c-523">當此設定為 true 時，所有要求（包括適用于 *.htm*、 *.jpg*和其他靜態檔案）也會經過 ASP.NET 要求管線。</span><span class="sxs-lookup"><span data-stu-id="ca38c-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="ca38c-524">如果您使用 Visual Studio 2012 RC 中提供的範本來建立新的 ASP.NET 4.5 網站，則網站的設定不會包含**runAllManagedModulesForAllRequests**設定。</span><span class="sxs-lookup"><span data-stu-id="ca38c-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="ca38c-525">這表示根據預設，此設定為 false。</span><span class="sxs-lookup"><span data-stu-id="ca38c-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="ca38c-526">如果您在未安裝 SP1 的 Windows 7 上執行網站，則 IIS 7 不會包含必要的更新。</span><span class="sxs-lookup"><span data-stu-id="ca38c-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="ca38c-527">因此，路由將無法使用，而且您會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca38c-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="ca38c-528">如果您有路由無法運作的問題，您可以執行下列其中一項動作：</span><span class="sxs-lookup"><span data-stu-id="ca38c-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="ca38c-529">將 Windows 7 更新為 SP1，這會將更新新增至 IIS 7。</span><span class="sxs-lookup"><span data-stu-id="ca38c-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="ca38c-530">安裝先前所列 Microsoft 支援服務文章中所述的更新。</span><span class="sxs-lookup"><span data-stu-id="ca38c-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="ca38c-531">在該網站的 web.config 檔案中，將**runAllManagedModulesForAllRequests**設定為 true。</span><span class="sxs-lookup"><span data-stu-id="ca38c-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="ca38c-532">請注意，這會對要求增加一些額外負荷。</span><span class="sxs-lookup"><span data-stu-id="ca38c-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="ca38c-533">HTML 編輯器</span><span class="sxs-lookup"><span data-stu-id="ca38c-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="ca38c-534">智慧型工作</span><span class="sxs-lookup"><span data-stu-id="ca38c-534">Smart Tasks</span></span>

<span data-ttu-id="ca38c-535">在設計檢視中，伺服器控制項的複雜屬性通常會有相關聯的對話方塊和嚮導，讓您可以輕鬆地設定它們。</span><span class="sxs-lookup"><span data-stu-id="ca38c-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="ca38c-536">例如，您可以使用特殊的對話方塊，將資料來源加入至重複*項控制項，* 或將資料行加入至*GridView*控制項。</span><span class="sxs-lookup"><span data-stu-id="ca38c-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="ca38c-537">不過，來源視圖中尚未提供複雜屬性的這類 UI 說明。</span><span class="sxs-lookup"><span data-stu-id="ca38c-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="ca38c-538">因此，Visual Studio 11 引進了來源視圖的智慧型工作。</span><span class="sxs-lookup"><span data-stu-id="ca38c-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="ca38c-539">智慧型工作C#是和 Visual Basic 編輯器中常用功能的內容感知快捷方式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="ca38c-540">對於 ASP.NET Web form 控制項，當插入點位於元素內部時，智慧型工作會以小型圖像的形式出現在伺服器標記上：</span><span class="sxs-lookup"><span data-stu-id="ca38c-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="ca38c-541">當您按一下圖像或按 CTRL + 時，智慧工作提示會展開。</span><span class="sxs-lookup"><span data-stu-id="ca38c-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="ca38c-542">（點），就如同在程式碼編輯器中一樣。</span><span class="sxs-lookup"><span data-stu-id="ca38c-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="ca38c-543">然後，它會顯示與設計檢視中的智慧工作類似的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="ca38c-544">例如，上圖中的智慧工作提示顯示 [GridView 工作] 選項。</span><span class="sxs-lookup"><span data-stu-id="ca38c-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="ca38c-545">如果您選擇 [編輯資料行]，則會顯示下列對話方塊：</span><span class="sxs-lookup"><span data-stu-id="ca38c-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="ca38c-546">填入對話方塊會設定您可以在設計檢視中設定的相同屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="ca38c-547">當您按一下 [確定] 時，會以新的設定更新控制項的標記：</span><span class="sxs-lookup"><span data-stu-id="ca38c-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="ca38c-548">WAI-ARIA 支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-548">WAI-ARIA support</span></span>

<span data-ttu-id="ca38c-549">撰寫可存取的網站變得越來越重要。</span><span class="sxs-lookup"><span data-stu-id="ca38c-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="ca38c-550">[WAI-ARIA 協助工具標準](http://www.w3.org/WAI/intro/aria)定義開發人員應該如何撰寫可存取的網站。</span><span class="sxs-lookup"><span data-stu-id="ca38c-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="ca38c-551">Visual Studio 現在已完全支援此標準。</span><span class="sxs-lookup"><span data-stu-id="ca38c-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="ca38c-552">例如， *role*屬性現在具有完整的 IntelliSense：</span><span class="sxs-lookup"><span data-stu-id="ca38c-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="ca38c-553">WAI-ARIA 標準也引進了前面加上*ARIA*的屬性，可讓您將語義新增至 HTML5 檔。</span><span class="sxs-lookup"><span data-stu-id="ca38c-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="ca38c-554">Visual Studio 也完全支援這些*aria*屬性：</span><span class="sxs-lookup"><span data-stu-id="ca38c-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="ca38c-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="ca38c-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="ca38c-556">新的 HTML5 程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ca38c-556">New HTML5 snippets</span></span>

<span data-ttu-id="ca38c-557">為了讓您更快速且更輕鬆地撰寫常用的 HTML5 標記，Visual Studio 包含一些程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca38c-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="ca38c-558">影片程式碼片段範例如下：</span><span class="sxs-lookup"><span data-stu-id="ca38c-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="ca38c-559">若要叫用程式碼片段，請在 IntelliSense 中選取元素時按兩次 Tab 鍵：</span><span class="sxs-lookup"><span data-stu-id="ca38c-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="ca38c-560">這會產生可供您自訂的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca38c-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="ca38c-561">解壓縮至使用者控制項</span><span class="sxs-lookup"><span data-stu-id="ca38c-561">Extract to user control</span></span>

<span data-ttu-id="ca38c-562">在大型的網頁中，將個別片段移入使用者控制項是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="ca38c-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="ca38c-563">這種重整形式有助於增加頁面的可讀性，並可簡化頁面結構。</span><span class="sxs-lookup"><span data-stu-id="ca38c-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="ca38c-564">若要簡化此作業，當您在原始檔視圖中編輯 Web form 頁面時，您現在可以選取頁面中的文字，以滑鼠右鍵按一下它，然後選擇 [解壓縮至使用者控制項]：</span><span class="sxs-lookup"><span data-stu-id="ca38c-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="ca38c-565">屬性中程式碼區塊的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="ca38c-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="ca38c-566">Visual Studio 一律會在任何頁面或控制項中提供伺服器端程式碼區塊的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ca38c-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="ca38c-567">現在 Visual Studio 也在 HTML 屬性中包含程式碼區塊的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ca38c-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="ca38c-568">這可讓您更輕鬆地建立資料系結運算式：</span><span class="sxs-lookup"><span data-stu-id="ca38c-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="ca38c-569">當您重新命名開頭或結束記號時，自動重新命名相符的標記</span><span class="sxs-lookup"><span data-stu-id="ca38c-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="ca38c-570">如果您重新命名 HTML 專案（例如，將*div*標記變更為*標頭*標記），則對應的開頭或結束記號也會即時變更。</span><span class="sxs-lookup"><span data-stu-id="ca38c-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="ca38c-571">這有助於避免您忘了變更結束標記或變更錯誤的標籤的錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca38c-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="ca38c-572">事件處理常式產生</span><span class="sxs-lookup"><span data-stu-id="ca38c-572">Event handler generation</span></span>

<span data-ttu-id="ca38c-573">Visual Studio 現在包含來源視圖中的功能，可協助您撰寫事件處理常式，並以手動方式加以系結。</span><span class="sxs-lookup"><span data-stu-id="ca38c-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="ca38c-574">如果您正在編輯來源視圖中的事件名稱，IntelliSense 會顯示 &lt;建立新事件&gt;，這會在頁面的程式碼中建立具有正確簽章的事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="ca38c-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="ca38c-575">根據預設，事件處理常式將會使用控制項的 ID 做為事件處理方法的名稱：</span><span class="sxs-lookup"><span data-stu-id="ca38c-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="ca38c-576">產生的事件處理常式看起來會像這樣（在此案例C#中為）：</span><span class="sxs-lookup"><span data-stu-id="ca38c-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="ca38c-577">智慧縮排</span><span class="sxs-lookup"><span data-stu-id="ca38c-577">Smart indent</span></span>

<span data-ttu-id="ca38c-578">當您在空白 HTML 專案內按 Enter 鍵時，編輯器會將插入點放在正確的位置：</span><span class="sxs-lookup"><span data-stu-id="ca38c-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="ca38c-579">如果您在這個位置按下 Enter 鍵，則結束記號會向下移動並縮排，以符合開頭的標記。</span><span class="sxs-lookup"><span data-stu-id="ca38c-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="ca38c-580">插入點也會縮排：</span><span class="sxs-lookup"><span data-stu-id="ca38c-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="ca38c-581">自動縮減語句完成</span><span class="sxs-lookup"><span data-stu-id="ca38c-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="ca38c-582">Visual Studio 中的 IntelliSense 清單現在會根據您所輸入的內容進行篩選，使其只顯示相關的選項：</span><span class="sxs-lookup"><span data-stu-id="ca38c-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="ca38c-583">IntelliSense 也會根據 IntelliSense 清單中個別單字的標題大小寫來進行篩選。</span><span class="sxs-lookup"><span data-stu-id="ca38c-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="ca38c-584">例如，如果您輸入 "dl"，則會顯示 [dl] 和 [asp： DataList]：</span><span class="sxs-lookup"><span data-stu-id="ca38c-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="ca38c-585">這項功能可讓您更快速地取得已知元素的語句完成。</span><span class="sxs-lookup"><span data-stu-id="ca38c-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="ca38c-586">JavaScript 編輯器</span><span class="sxs-lookup"><span data-stu-id="ca38c-586">JavaScript Editor</span></span>

<span data-ttu-id="ca38c-587">Visual Studio 2012 候選版中的 JavaScript 編輯器是全新的，它大幅改善了在 Visual Studio 中使用 JavaScript 的經驗。</span><span class="sxs-lookup"><span data-stu-id="ca38c-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="ca38c-588">程式碼大綱</span><span class="sxs-lookup"><span data-stu-id="ca38c-588">Code outlining</span></span>

<span data-ttu-id="ca38c-589">現在會自動為所有函式建立大綱區域，讓您可以折迭檔案的某些部分，而不是與您目前的焦點有關。</span><span class="sxs-lookup"><span data-stu-id="ca38c-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="ca38c-590">括號對稱</span><span class="sxs-lookup"><span data-stu-id="ca38c-590">Brace matching</span></span>

<span data-ttu-id="ca38c-591">當您將插入點放在左或右大括弧時，編輯器會反白顯示相符的位置。</span><span class="sxs-lookup"><span data-stu-id="ca38c-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="ca38c-592">移至定義</span><span class="sxs-lookup"><span data-stu-id="ca38c-592">Go to Definition</span></span>

<span data-ttu-id="ca38c-593">[移至定義] 命令可讓您跳到函式或變數的來源。</span><span class="sxs-lookup"><span data-stu-id="ca38c-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="ca38c-594">ECMAScript5 支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-594">ECMAScript5 support</span></span>

<span data-ttu-id="ca38c-595">編輯器支援 ECMAScript5 中的新語法和 Api，這是描述 JavaScript 語言的最新標準版本。</span><span class="sxs-lookup"><span data-stu-id="ca38c-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="ca38c-596">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="ca38c-596">DOM IntelliSense</span></span>

<span data-ttu-id="ca38c-597">DOM Api 的 IntelliSense 已改良，並支援許多新的 HTML5 Api，包括*querySelector*、DOM 儲存、跨檔訊息和*畫布*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="ca38c-598">DOM IntelliSense 現在是由單一簡單的 JavaScript 檔案驅動，而不是原生類型程式庫定義。</span><span class="sxs-lookup"><span data-stu-id="ca38c-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="ca38c-599">這可讓您輕鬆地延伸或取代。</span><span class="sxs-lookup"><span data-stu-id="ca38c-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="ca38c-600">VSDOC 簽章多載</span><span class="sxs-lookup"><span data-stu-id="ca38c-600">VSDOC signature overloads</span></span>

<span data-ttu-id="ca38c-601">您現在可以使用新的&lt;簽章 *&gt;* 元素，為 JavaScript 函式的個別多載宣告詳細的 IntelliSense 批註，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ca38c-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="ca38c-602">隱含參考</span><span class="sxs-lookup"><span data-stu-id="ca38c-602">Implicit references</span></span>

<span data-ttu-id="ca38c-603">您現在可以將 JavaScript 檔案新增至中央清單，而這些檔案會以隱含方式包含在任何指定的 JavaScript 檔案或區塊參考的檔案清單中，這表示您將會取得其內容的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ca38c-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="ca38c-604">例如，您可以將 jQuery 檔案加入檔案的中央清單中，而不論您是否明確參考它（使用///&lt;參考/&gt;），都能在檔案的任何 JavaScript 區塊中取得 jQuery 函式的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ca38c-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="ca38c-605">CSS 編輯器</span><span class="sxs-lookup"><span data-stu-id="ca38c-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="ca38c-606">自動縮減語句完成</span><span class="sxs-lookup"><span data-stu-id="ca38c-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="ca38c-607">CSS 的 IntelliSense 清單現在會根據所選架構所支援的 CSS 屬性和值進行篩選。</span><span class="sxs-lookup"><span data-stu-id="ca38c-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="ca38c-608">IntelliSense 也支援標題案例搜尋：</span><span class="sxs-lookup"><span data-stu-id="ca38c-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="ca38c-609">階層式縮排</span><span class="sxs-lookup"><span data-stu-id="ca38c-609">Hierarchical indentation</span></span>

<span data-ttu-id="ca38c-610">CSS 編輯器會使用縮排來顯示階層式規則，讓您大致瞭解串聯式規則如何以邏輯方式組織。</span><span class="sxs-lookup"><span data-stu-id="ca38c-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="ca38c-611">在下列範例中，#list 選取器是清單的串聯子系，因此會縮排。</span><span class="sxs-lookup"><span data-stu-id="ca38c-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="ca38c-612">下列範例會顯示更複雜的繼承：</span><span class="sxs-lookup"><span data-stu-id="ca38c-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="ca38c-613">規則的縮排是由其父規則所決定。</span><span class="sxs-lookup"><span data-stu-id="ca38c-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="ca38c-614">預設會啟用階層式縮排，但您可以將它停用 [選項] 對話方塊（[工具]、功能表列中的選項）：</span><span class="sxs-lookup"><span data-stu-id="ca38c-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="ca38c-615">CSS 的駭客支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-615">CSS hacks support</span></span>

<span data-ttu-id="ca38c-616">分析數百個真實世界的 CSS 檔案，會顯示 CSS 的駭客攻擊非常常見，現在 Visual Studio 支援最廣泛使用的程式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="ca38c-617">這項支援包括 IntelliSense 和驗證星形（\*）和底線（\_）屬性的駭客：</span><span class="sxs-lookup"><span data-stu-id="ca38c-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="ca38c-618">此外，也支援一般的選取器的攻擊，因此即使套用了階層式縮排也可以保留。</span><span class="sxs-lookup"><span data-stu-id="ca38c-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="ca38c-619">用來以 Internet Explorer 7 為目標的一般選擇器，是在選取器前面加上 *\*： first-child + html*。</span><span class="sxs-lookup"><span data-stu-id="ca38c-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="ca38c-620">使用該規則將會維護階層式縮排：</span><span class="sxs-lookup"><span data-stu-id="ca38c-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="ca38c-621">廠商特定架構（-moz-appearance-,-webkit）</span><span class="sxs-lookup"><span data-stu-id="ca38c-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="ca38c-622">CSS3 引進了許多由不同瀏覽器在不同時間執行的屬性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="ca38c-623">這個方法先前會強制開發人員使用廠商專屬的語法來撰寫特定瀏覽器的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca38c-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="ca38c-624">這些瀏覽器特有的屬性現在包含在 IntelliSense 中。</span><span class="sxs-lookup"><span data-stu-id="ca38c-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="ca38c-625">批註和取消批註支援</span><span class="sxs-lookup"><span data-stu-id="ca38c-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="ca38c-626">您現在可以使用您在程式碼編輯器中使用的相同快速鍵（Ctrl + K、C 來批註和 Ctrl + K）來批註和取消批註 CSS 規則，以取消批註。</span><span class="sxs-lookup"><span data-stu-id="ca38c-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="ca38c-627">色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="ca38c-627">Color picker</span></span>

<span data-ttu-id="ca38c-628">在舊版的 Visual Studio 中，色彩相關屬性的 IntelliSense 是由已命名色彩值的下拉式清單所組成。</span><span class="sxs-lookup"><span data-stu-id="ca38c-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="ca38c-629">該清單已由全功能的色彩選擇器所取代。</span><span class="sxs-lookup"><span data-stu-id="ca38c-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="ca38c-630">當您輸入色彩值時，色彩選擇器會自動顯示，並且顯示先前使用的色彩清單，後面接著預設的調色板。</span><span class="sxs-lookup"><span data-stu-id="ca38c-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="ca38c-631">您可以使用滑鼠或鍵盤來選取色彩。</span><span class="sxs-lookup"><span data-stu-id="ca38c-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="ca38c-632">清單可以擴充為完整的色彩選擇器。</span><span class="sxs-lookup"><span data-stu-id="ca38c-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="ca38c-633">選擇器可讓您在移動不透明度滑杆時，自動將任何色彩轉換成 RGBA，藉此控制 Alpha 色板：</span><span class="sxs-lookup"><span data-stu-id="ca38c-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="ca38c-634">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ca38c-634">Snippets</span></span>

<span data-ttu-id="ca38c-635">CSS 編輯器中的程式碼片段可讓您更輕鬆快速地建立跨瀏覽器樣式。</span><span class="sxs-lookup"><span data-stu-id="ca38c-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="ca38c-636">許多需要瀏覽器專屬設定的 CSS3 屬性現在已匯總成程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca38c-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="ca38c-637">CSS 程式碼片段藉由輸入符號（@）來支援先進的案例（例如 CSS3 媒體查詢），這會顯示 IntelliSense 清單。</span><span class="sxs-lookup"><span data-stu-id="ca38c-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="ca38c-638">當您選取 @media 值並按 Tab 鍵時，CSS 編輯器會插入下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="ca38c-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="ca38c-639">如同程式碼片段，您可以建立自己的 CSS 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca38c-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="ca38c-640">自訂區域</span><span class="sxs-lookup"><span data-stu-id="ca38c-640">Custom regions</span></span>

<span data-ttu-id="ca38c-641">已在 [程式碼編輯器] 中使用的已命名程式碼區域，現在可供 CSS 編輯之用。</span><span class="sxs-lookup"><span data-stu-id="ca38c-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="ca38c-642">這可讓您輕鬆地將相關的樣式區塊分組。</span><span class="sxs-lookup"><span data-stu-id="ca38c-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="ca38c-643">當區域折迭時，它會顯示區域的名稱：</span><span class="sxs-lookup"><span data-stu-id="ca38c-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="ca38c-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="ca38c-644">Page Inspector</span></span>

<span data-ttu-id="ca38c-645">Page Inspector 是在 Visual Studio IDE 中呈現網頁（HTML、Web form、ASP.NET MVC 或網頁）的工具，可讓您檢查原始程式碼和所產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="ca38c-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="ca38c-646">在 ASP.NET 網頁中，Page Inspector 可讓您判斷哪些伺服器端程式碼產生了呈現給瀏覽器的 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="ca38c-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="ca38c-647">如需 Page Inspector 的詳細資訊，請參閱下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="ca38c-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="ca38c-648">在[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="ca38c-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="ca38c-649">在[ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="ca38c-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="ca38c-650">發佈</span><span class="sxs-lookup"><span data-stu-id="ca38c-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="ca38c-651">發行設定檔</span><span class="sxs-lookup"><span data-stu-id="ca38c-651">Publish profiles</span></span>

<span data-ttu-id="ca38c-652">在 Visual Studio 2010 中，Web 應用程式專案的發行資訊不會儲存在版本控制中，而且不是設計來與其他人共用。</span><span class="sxs-lookup"><span data-stu-id="ca38c-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="ca38c-653">在 Visual Studio 2012 候選版中，發行設定檔的格式已經變更。</span><span class="sxs-lookup"><span data-stu-id="ca38c-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="ca38c-654">它已成為 team 成品，現在可以輕鬆地從以 MSBuild 為基礎的組建中運用。</span><span class="sxs-lookup"><span data-stu-id="ca38c-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="ca38c-655">組建設定資訊位於 [發佈] 對話方塊中，因此您可以在發行之前輕鬆地切換組建設定。</span><span class="sxs-lookup"><span data-stu-id="ca38c-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="ca38c-656">發行設定檔會儲存在 PublishProfiles 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ca38c-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="ca38c-657">資料夾的位置取決於您所使用的程式設計語言：</span><span class="sxs-lookup"><span data-stu-id="ca38c-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="ca38c-658">C#: Properties\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="ca38c-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="ca38c-659">Visual Basic：我的 Project\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="ca38c-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="ca38c-660">每個設定檔都是 MSBuild 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="ca38c-661">在發佈期間，會將此檔案匯入至專案的 MSBuild 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca38c-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="ca38c-662">在 Visual Studio 2010 中，如果您想要對發佈或封裝程式進行變更，您必須將自訂專案放在名為檔案**名稱**. wpp. .targets 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="ca38c-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="ca38c-663">這仍然受支援，但您現在可以將自訂專案放在發行設定檔本身。</span><span class="sxs-lookup"><span data-stu-id="ca38c-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="ca38c-664">如此一來，自訂只會用於該設定檔。</span><span class="sxs-lookup"><span data-stu-id="ca38c-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="ca38c-665">您現在也可以利用 MSBuild 的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="ca38c-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="ca38c-666">若要這樣做，當您建立專案時，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ca38c-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="ca38c-667">專案 .csproj 值是專案的路徑，而 ProfileName 是要發行之設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="ca38c-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="ca38c-668">或者，您可以傳遞發行設定檔的完整路徑，而不是傳遞*PublishProfile*屬性的設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="ca38c-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="ca38c-669">ASP.NET 先行編譯和合併</span><span class="sxs-lookup"><span data-stu-id="ca38c-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="ca38c-670">對於 Web 應用程式專案，Visual Studio 2012 發行候選版會在 [封裝/發行 Web 屬性] 頁面上新增一個選項，讓您在發行或封裝專案時，先行編譯和合併網站的內容。</span><span class="sxs-lookup"><span data-stu-id="ca38c-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="ca38c-671">若要查看這些選項，請以滑鼠右鍵按一下方案總管中的專案，選擇 [屬性]，然後選擇 [封裝/發行 Web] 屬性頁。</span><span class="sxs-lookup"><span data-stu-id="ca38c-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="ca38c-672">下圖顯示 [發行之前先行編譯此應用程式] 選項。</span><span class="sxs-lookup"><span data-stu-id="ca38c-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="ca38c-673">選取此選項時，Visual Studio 會在您發行或封裝 web 應用程式時，將應用程式進行預先編譯。</span><span class="sxs-lookup"><span data-stu-id="ca38c-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="ca38c-674">如果您想要控制編譯網站的方式或合併元件的方式，請按一下 [Advanced] 按鈕來設定這些選項。</span><span class="sxs-lookup"><span data-stu-id="ca38c-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="ca38c-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="ca38c-675">IIS Express</span></span>

<span data-ttu-id="ca38c-676">Visual Studio 中用來測試 Web 專案的預設 web 伺服器現在 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="ca38c-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="ca38c-677">Visual Studio 程式開發伺服器在開發期間仍然是本機 web 伺服器的選項，但 IIS Express 現在是建議的伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca38c-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="ca38c-678">在 Visual Studio 11 Beta 版中使用 IIS Express，與在 Visual Studio 2010 SP1 中使用的經驗非常類似。</span><span class="sxs-lookup"><span data-stu-id="ca38c-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="ca38c-679">免責聲明</span><span class="sxs-lookup"><span data-stu-id="ca38c-679">Disclaimer</span></span>

<span data-ttu-id="ca38c-680">這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。</span><span class="sxs-lookup"><span data-stu-id="ca38c-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="ca38c-681">本文件中的資訊表示直到文件發行日前 Microsoft Corporation 針對問題的看法。</span><span class="sxs-lookup"><span data-stu-id="ca38c-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="ca38c-682">Microsoft 必須因應不斷變化的市場狀況，因此本文件不代表 Microsoft 的保證，且 Microsoft 不保證這些資訊在文件發行後的正確性。</span><span class="sxs-lookup"><span data-stu-id="ca38c-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="ca38c-683">本技術白皮書僅供參考。</span><span class="sxs-lookup"><span data-stu-id="ca38c-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="ca38c-684">MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。</span><span class="sxs-lookup"><span data-stu-id="ca38c-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="ca38c-685">承諾遵守所有適用的著作權法是使用者的責任。</span><span class="sxs-lookup"><span data-stu-id="ca38c-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="ca38c-686">著作權法沒有針對某種權利加以限制，但在未獲得 Microsoft Corporation 書面同意的情況下，本文件的任何部分不得複製、以檢索系統存放或擷取、以任何形式或方法傳送 (電子、機械、影像複製、錄音或其他任何方法)、或基於任何其他不良意圖。</span><span class="sxs-lookup"><span data-stu-id="ca38c-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="ca38c-687">本文件所提及的主要事務，Microsoft 得擁有專利、專利應用程式、商標、著作權或其他智慧財產權。</span><span class="sxs-lookup"><span data-stu-id="ca38c-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="ca38c-688">除了 Microsoft 於授權合約書中書面提供的之外，本文件所述內容並未賦予您這些專利、商標、著作權、或其他智慧財產的任何授權或使用權利。</span><span class="sxs-lookup"><span data-stu-id="ca38c-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="ca38c-689">除非另有說明，否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、商標、人員、地點及事件均屬虛構，而且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件相關。位址、標誌、人員、地點或事件的預定或應加以推斷。</span><span class="sxs-lookup"><span data-stu-id="ca38c-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="ca38c-690">(C) 2012 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="ca38c-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="ca38c-691">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="ca38c-691">All rights reserved.</span></span>

<span data-ttu-id="ca38c-692">Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。</span><span class="sxs-lookup"><span data-stu-id="ca38c-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="ca38c-693">本文件中所提實際公司和產品，可能為各所有人所有之商標。</span><span class="sxs-lookup"><span data-stu-id="ca38c-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
