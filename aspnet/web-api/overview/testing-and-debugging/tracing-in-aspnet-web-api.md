---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2 中的追蹤 |Microsoft Docs
author: MikeWasson
description: 顯示如何在 ASP.NET Web API 中啟用追蹤。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598550"
---
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="3dd67-103">ASP.NET Web API 2 中的追蹤</span><span class="sxs-lookup"><span data-stu-id="3dd67-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="3dd67-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3dd67-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="3dd67-105">當您嘗試進行 web 應用程式的調試時，不會有一組不錯的追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="3dd67-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="3dd67-106">本教學課程說明如何在 ASP.NET Web API 中啟用追蹤。</span><span class="sxs-lookup"><span data-stu-id="3dd67-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="3dd67-107">您可以使用這項功能，追蹤 Web API 架構在叫用您的控制器之前和之後所執行的工作。</span><span class="sxs-lookup"><span data-stu-id="3dd67-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="3dd67-108">您也可以使用它來追蹤您自己的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3dd67-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3dd67-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="3dd67-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="3dd67-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) （也適用于 Visual Studio 2015）</span><span class="sxs-lookup"><span data-stu-id="3dd67-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="3dd67-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="3dd67-111">Web API 2</span></span>
> - [<span data-ttu-id="3dd67-112">WebApi. 追蹤</span><span class="sxs-lookup"><span data-stu-id="3dd67-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="3dd67-113">在 Web API 中啟用系統診斷追蹤</span><span class="sxs-lookup"><span data-stu-id="3dd67-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="3dd67-114">首先，我們會建立新的 ASP.NET Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="3dd67-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="3dd67-115">在 Visual Studio 中，從 **[檔案**] 功能表選取 [**新增** > **專案**]。</span><span class="sxs-lookup"><span data-stu-id="3dd67-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="3dd67-116">在 [**範本**]**底下，選取**[ **ASP.NET web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="3dd67-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="3dd67-117">選擇 [Web API] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="3dd67-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="3dd67-118">從 [**工具**] 功能表中，依序選取 [ **NuGet 套件管理員**] 和 [**套件管理主控台**]。</span><span class="sxs-lookup"><span data-stu-id="3dd67-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="3dd67-119">在 [套件管理員主控台] 視窗中，輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="3dd67-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="3dd67-120">第一個命令會安裝最新的 Web API 追蹤封裝。</span><span class="sxs-lookup"><span data-stu-id="3dd67-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="3dd67-121">它也會更新核心 Web API 套件。</span><span class="sxs-lookup"><span data-stu-id="3dd67-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="3dd67-122">第二個命令會將 WebApi. WebHost 套件更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="3dd67-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="3dd67-123">如果您想要以特定版本的 Web API 為目標，請在安裝追蹤套件時使用-Version 旗標。</span><span class="sxs-lookup"><span data-stu-id="3dd67-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="3dd67-124">開啟應用程式\_[開始] 資料夾中的檔案 WebApiConfig.cs。</span><span class="sxs-lookup"><span data-stu-id="3dd67-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="3dd67-125">將下列程式碼新增至**Register**方法。</span><span class="sxs-lookup"><span data-stu-id="3dd67-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="3dd67-126">此程式碼會將[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)類別新增至 Web API 管線。</span><span class="sxs-lookup"><span data-stu-id="3dd67-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="3dd67-127">**SystemDiagnosticsTraceWriter**類別會將追蹤寫入至[system.object](https://msdn.microsoft.com/library/system.diagnostics.trace)。</span><span class="sxs-lookup"><span data-stu-id="3dd67-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="3dd67-128">若要查看追蹤，請在偵錯工具中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dd67-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="3dd67-129">在瀏覽器中，瀏覽至 `/api/values`。</span><span class="sxs-lookup"><span data-stu-id="3dd67-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="3dd67-130">追蹤語句會寫入 Visual Studio 的 [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="3dd67-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="3dd67-131">（從 [ **View** ] 功能表選取 [**輸出**]）。</span><span class="sxs-lookup"><span data-stu-id="3dd67-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="3dd67-132">因為**SystemDiagnosticsTraceWriter**會將追蹤寫入至**system.webserver**，所以您可以註冊其他追蹤接聽項;例如，將追蹤寫入記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3dd67-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="3dd67-133">如需追蹤寫入器的詳細資訊，請參閱 MSDN 上的[追蹤](https://msdn.microsoft.com/library/4y5y10s7.aspx)接聽項主題。</span><span class="sxs-lookup"><span data-stu-id="3dd67-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="3dd67-134">設定 SystemDiagnosticsTraceWriter</span><span class="sxs-lookup"><span data-stu-id="3dd67-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="3dd67-135">下列程式碼顯示如何設定追蹤寫入器。</span><span class="sxs-lookup"><span data-stu-id="3dd67-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="3dd67-136">有兩個設定可供您控制：</span><span class="sxs-lookup"><span data-stu-id="3dd67-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="3dd67-137">IsVerbose：如果為 false，則每個追蹤都包含最少的資訊。</span><span class="sxs-lookup"><span data-stu-id="3dd67-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="3dd67-138">若為 true，追蹤會包含詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3dd67-138">If true, traces include more information.</span></span>
- <span data-ttu-id="3dd67-139">MinimumLevel：設定最小追蹤層級。</span><span class="sxs-lookup"><span data-stu-id="3dd67-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="3dd67-140">追蹤層級（依序）為 Debug、Info、警告、Error 和嚴重。</span><span class="sxs-lookup"><span data-stu-id="3dd67-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="3dd67-141">將追蹤新增至您的 Web API 應用程式</span><span class="sxs-lookup"><span data-stu-id="3dd67-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="3dd67-142">新增追蹤寫入器可讓您立即存取 Web API 管線所建立的追蹤。</span><span class="sxs-lookup"><span data-stu-id="3dd67-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="3dd67-143">您也可以使用追蹤寫入器來追蹤您自己的程式碼：</span><span class="sxs-lookup"><span data-stu-id="3dd67-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="3dd67-144">若要取得追蹤寫入器，請呼叫**HttpConfiguration。 GetTraceWriter**。</span><span class="sxs-lookup"><span data-stu-id="3dd67-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="3dd67-145">在控制器上，此方法可透過**ApiController**屬性來存取。</span><span class="sxs-lookup"><span data-stu-id="3dd67-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="3dd67-146">若要撰寫追蹤，您可以直接呼叫**ITraceWriter**方法，但是[ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)類別會定義一些較容易瞭解的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="3dd67-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="3dd67-147">例如，上面顯示的**Info**方法會建立具有追蹤層級**資訊**的追蹤。</span><span class="sxs-lookup"><span data-stu-id="3dd67-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="3dd67-148">Web API 追蹤基礎結構</span><span class="sxs-lookup"><span data-stu-id="3dd67-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="3dd67-149">本節說明如何撰寫 Web API 的自訂追蹤寫入器。</span><span class="sxs-lookup"><span data-stu-id="3dd67-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="3dd67-150">WebApi. 追蹤套件是以 Web API 中更通用的追蹤基礎結構來建立。</span><span class="sxs-lookup"><span data-stu-id="3dd67-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="3dd67-151">除了使用 WebApi，您也可以插入一些其他的追蹤/記錄程式庫，例如[NLog](http://nlog-project.org/)或[log4net](http://logging.apache.org/log4net/)。</span><span class="sxs-lookup"><span data-stu-id="3dd67-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="3dd67-152">若要收集追蹤，請執行**ITraceWriter**介面。</span><span class="sxs-lookup"><span data-stu-id="3dd67-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="3dd67-153">以下是一個簡單的範例：</span><span class="sxs-lookup"><span data-stu-id="3dd67-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="3dd67-154">**ITraceWriter**方法會建立追蹤。</span><span class="sxs-lookup"><span data-stu-id="3dd67-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="3dd67-155">呼叫者會指定分類和追蹤層級。</span><span class="sxs-lookup"><span data-stu-id="3dd67-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="3dd67-156">類別可以是任何使用者定義的字串。</span><span class="sxs-lookup"><span data-stu-id="3dd67-156">The category can be any user-defined string.</span></span> <span data-ttu-id="3dd67-157">您的**追蹤**執行應該會進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="3dd67-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="3dd67-158">建立新的**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="3dd67-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="3dd67-159">使用要求、類別和追蹤層級將它初始化，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3dd67-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="3dd67-160">這些值是由呼叫端提供。</span><span class="sxs-lookup"><span data-stu-id="3dd67-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="3dd67-161">叫用*traceAction*委派。</span><span class="sxs-lookup"><span data-stu-id="3dd67-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="3dd67-162">在此委派中，呼叫端應該填入**TraceRecord**的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="3dd67-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="3dd67-163">使用您喜歡的任何記錄技術來撰寫**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="3dd67-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="3dd67-164">此處顯示的範例只會呼叫**system.object**。</span><span class="sxs-lookup"><span data-stu-id="3dd67-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="3dd67-165">設定追蹤寫入器</span><span class="sxs-lookup"><span data-stu-id="3dd67-165">Setting the Trace Writer</span></span>

<span data-ttu-id="3dd67-166">若要啟用追蹤，您必須設定 Web API 以使用您的**ITraceWriter**執行。</span><span class="sxs-lookup"><span data-stu-id="3dd67-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="3dd67-167">您可以透過**HttpConfiguration**物件來執行此動作，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="3dd67-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="3dd67-168">只有一個追蹤寫入器可以處於作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="3dd67-168">Only one trace writer can be active.</span></span> <span data-ttu-id="3dd67-169">根據預設，Web API 會設定不會執行任何作業的 &quot;無 op&quot; 追蹤。</span><span class="sxs-lookup"><span data-stu-id="3dd67-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="3dd67-170">（&quot;無作業&quot; 追蹤存在，因此追蹤程式碼不需要在寫入追蹤之前檢查追蹤寫入器是否為**null** ）。</span><span class="sxs-lookup"><span data-stu-id="3dd67-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="3dd67-171">Web API 追蹤的運作方式</span><span class="sxs-lookup"><span data-stu-id="3dd67-171">How Web API Tracing Works</span></span>

<span data-ttu-id="3dd67-172">Web API 中的追蹤會使用*外觀*模式：當啟用追蹤時，Web API 會使用執行追蹤呼叫的類別來包裝要求管線的各個部分。</span><span class="sxs-lookup"><span data-stu-id="3dd67-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="3dd67-173">例如，選取控制器時，管線會使用**IHttpControllerSelector**介面。</span><span class="sxs-lookup"><span data-stu-id="3dd67-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="3dd67-174">啟用追蹤之後，管線會插入一個可執行**IHttpControllerSelector**的類別，但會呼叫實際執行的：</span><span class="sxs-lookup"><span data-stu-id="3dd67-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API 追蹤會使用面板模式。](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="3dd67-176">這項設計的優點包括：</span><span class="sxs-lookup"><span data-stu-id="3dd67-176">The benefits of this design include:</span></span>

- <span data-ttu-id="3dd67-177">如果您沒有新增追蹤寫入器，追蹤元件就不會具現化，而且不會影響效能。</span><span class="sxs-lookup"><span data-stu-id="3dd67-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="3dd67-178">如果您使用自己的自訂執行來取代預設服務（例如**IHttpControllerSelector** ），則不會影響追蹤，因為追蹤是由包裝函式物件進行。</span><span class="sxs-lookup"><span data-stu-id="3dd67-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="3dd67-179">您也可以取代預設的**ITraceManager**服務，將整個 Web API 追蹤架構取代成您自己的自訂架構：</span><span class="sxs-lookup"><span data-stu-id="3dd67-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="3dd67-180">執行**ITraceManager** ，將您的追蹤系統初始化。</span><span class="sxs-lookup"><span data-stu-id="3dd67-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="3dd67-181">請注意，這會取代*整個*追蹤架構，包括 Web API 內建的所有追蹤程式碼。</span><span class="sxs-lookup"><span data-stu-id="3dd67-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
