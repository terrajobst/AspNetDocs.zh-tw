---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: '[說明] 頁面建立 ASP.NET Web API-ASP.NET 4.x'
author: MikeWasson
description: 本教學課程中的使用程式碼示範如何建立的 ASP.NET 中的 ASP.NET Web API 說明頁面 4.x。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: e3f6a9b8a6835b034a075d580cd9a33136969990
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59395009"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="17404-103">建立的 ASP.NET Web API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="17404-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="17404-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="17404-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="17404-105">本教學課程中的使用程式碼示範如何建立的 ASP.NET 中的 ASP.NET Web API 說明頁面 4.x。</span><span class="sxs-lookup"><span data-stu-id="17404-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="17404-106">當您建立的 web API 時，它通常很有用來建立說明網頁，以便在其他開發人員知道如何呼叫您的 API。</span><span class="sxs-lookup"><span data-stu-id="17404-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="17404-107">您可以手動建立所有文件，但最好是盡量的自動產生。</span><span class="sxs-lookup"><span data-stu-id="17404-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="17404-108">若要簡化這項工作中，ASP.NET Web API 會在執行階段，程式庫提供自動產生說明頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="17404-109">建立 API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="17404-109">Creating API Help Pages</span></span>

<span data-ttu-id="17404-110">安裝[ASP.NET 和 Web 工具 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="17404-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="17404-111">此更新會整合到 Web API 專案範本的 [說明] 頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="17404-112">接下來，建立新的 ASP.NET MVC 4 專案，然後選取 Web API 專案範本。</span><span class="sxs-lookup"><span data-stu-id="17404-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="17404-113">專案範本會建立名為範例 API 控制器`ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="17404-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="17404-114">此範本也會建立 API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-114">The template also creates the API help pages.</span></span> <span data-ttu-id="17404-115">所有 [說明] 頁面的程式碼檔案位於專案的 [區域] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="17404-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="17404-116">當您執行應用程式時，[首頁] 頁面會包含 API 說明頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="17404-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="17404-117">從 [首頁] 頁面中，相對路徑會是 /Help。</span><span class="sxs-lookup"><span data-stu-id="17404-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="17404-118">此連結將帶您前往 API 摘要頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="17404-119">此頁面的 [MVC] 檢視會定義在 Areas/HelpPage/Views/Help/Index.cshtml。</span><span class="sxs-lookup"><span data-stu-id="17404-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="17404-120">您可以編輯此頁面修改版面配置、 簡介、 標題、 樣式和其他等等。</span><span class="sxs-lookup"><span data-stu-id="17404-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="17404-121">頁面的主要部分是依控制站的 api 的資料表。</span><span class="sxs-lookup"><span data-stu-id="17404-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="17404-122">資料表項目使用，以動態方式產生**IApiExplorer**介面。</span><span class="sxs-lookup"><span data-stu-id="17404-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="17404-123">（我會詳細討論有關此介面更新版本。）如果您新增新的 API 控制器，請在執行階段時，會自動更新的資料表。</span><span class="sxs-lookup"><span data-stu-id="17404-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="17404-124">「 API 」 資料行列出的 HTTP 方法和相對 URI。</span><span class="sxs-lookup"><span data-stu-id="17404-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="17404-125">「 說明 」 資料行包含每個 API 的文件。</span><span class="sxs-lookup"><span data-stu-id="17404-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="17404-126">一開始，文件就是只是預留位置文字。</span><span class="sxs-lookup"><span data-stu-id="17404-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="17404-127">下一節，我將示範如何從 XML 註解加入文件。</span><span class="sxs-lookup"><span data-stu-id="17404-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="17404-128">每個 API 有更詳細的資訊，包括範例要求和回應內文的頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="17404-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="17404-129">加入現有的專案中的 [說明] 頁面</span><span class="sxs-lookup"><span data-stu-id="17404-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="17404-130">您可以透過 NuGet 套件管理員，將 [說明] 頁面新增至現有的 Web API 專案中。</span><span class="sxs-lookup"><span data-stu-id="17404-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="17404-131">這個選項適合您開始從不同的專案範本，於 [Web API] 範本。</span><span class="sxs-lookup"><span data-stu-id="17404-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="17404-132">從**工具**功能表上，選取**NuGet 套件管理員**，然後選取**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="17404-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="17404-133">在  [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)視窗中，輸入下列命令之一：</span><span class="sxs-lookup"><span data-stu-id="17404-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="17404-134">針對**C#** 應用程式：</span><span class="sxs-lookup"><span data-stu-id="17404-134">For a **C#** application:</span></span> `Install-Package Microsoft.AspNet.WebApi.HelpPage`

<span data-ttu-id="17404-135">針對**Visual Basic**應用程式：</span><span class="sxs-lookup"><span data-stu-id="17404-135">For a **Visual Basic** application:</span></span> `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

<span data-ttu-id="17404-136">有兩個套件，一個適用於 C#，一個適用於 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="17404-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="17404-137">請務必使用符合您的專案。</span><span class="sxs-lookup"><span data-stu-id="17404-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="17404-138">此命令會安裝必要的組件，並新增 （位於 [區域/HelpPage] 資料夾） 的 [說明] 頁的 MVC 檢視。</span><span class="sxs-lookup"><span data-stu-id="17404-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="17404-139">您必須手動將連結新增至 [說明] 頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="17404-140">URI 是 /Help。</span><span class="sxs-lookup"><span data-stu-id="17404-140">The URI is /Help.</span></span> <span data-ttu-id="17404-141">若要建立連結，在 razor 檢視中，新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="17404-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="17404-142">此外，請確定註冊區域。</span><span class="sxs-lookup"><span data-stu-id="17404-142">Also, make sure to register areas.</span></span> <span data-ttu-id="17404-143">在 Global.asax 檔案中，新增下列程式碼**應用程式\_啟動**方法，如果找不到已：</span><span class="sxs-lookup"><span data-stu-id="17404-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="17404-144">新增 API 文件</span><span class="sxs-lookup"><span data-stu-id="17404-144">Adding API Documentation</span></span>

<span data-ttu-id="17404-145">根據預設，說明 頁面都有文件的預留位置字串。</span><span class="sxs-lookup"><span data-stu-id="17404-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="17404-146">您可以使用[XML 文件註解](https://msdn.microsoft.com/library/b2s063f7.aspx)建立文件。</span><span class="sxs-lookup"><span data-stu-id="17404-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="17404-147">若要啟用此功能，開啟 區域/HelpPage/應用程式的檔案\_Start/HelpPageConfig.cs 並取消註解下面這一行：</span><span class="sxs-lookup"><span data-stu-id="17404-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="17404-148">現在可讓 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="17404-148">Now enable XML documentation.</span></span> <span data-ttu-id="17404-149">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="17404-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="17404-150">選取 **建置**頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="17404-151">底下**輸出**，檢查**XML 文件檔案**。</span><span class="sxs-lookup"><span data-stu-id="17404-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="17404-152">在 [編輯] 方塊中，輸入 「 應用程式\_Data/XmlDocument.xml"。</span><span class="sxs-lookup"><span data-stu-id="17404-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="17404-153">接下來，開啟的程式碼`ValuesController`API 控制器，其定義於 /Controllers/ValuesController.cs。</span><span class="sxs-lookup"><span data-stu-id="17404-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="17404-154">控制器方法中加入一些文件註解。</span><span class="sxs-lookup"><span data-stu-id="17404-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="17404-155">例如：</span><span class="sxs-lookup"><span data-stu-id="17404-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="17404-156">提示：如果您的方法上方列上放置插入號，並輸入三個正斜線，Visual Studio 會自動插入的 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="17404-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="17404-157">然後您可以填上空白。</span><span class="sxs-lookup"><span data-stu-id="17404-157">Then you can fill in the blanks.</span></span>


<span data-ttu-id="17404-158">現在建置並再次執行應用程式，並瀏覽至 [說明] 頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="17404-159">文件字串，應該會出現在 API 資料表。</span><span class="sxs-lookup"><span data-stu-id="17404-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="17404-160">[說明] 頁面會在執行階段，從 XML 檔案讀取的字串。</span><span class="sxs-lookup"><span data-stu-id="17404-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="17404-161">（當您部署應用程式時，請確定部署的 XML 檔案。）</span><span class="sxs-lookup"><span data-stu-id="17404-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="17404-162">背後原理</span><span class="sxs-lookup"><span data-stu-id="17404-162">Under the Hood</span></span>

<span data-ttu-id="17404-163">說明網頁為基礎建置的**ApiExplorer**類別，這是 Web API 架構的一部分。</span><span class="sxs-lookup"><span data-stu-id="17404-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="17404-164">**ApiExplorer**類別提供原始資料來建立說明頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="17404-165">每個 API，如**ApiExplorer**包含**ApiDescription**描述 API。</span><span class="sxs-lookup"><span data-stu-id="17404-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="17404-166">基於此目的，「 API 」 定義為 HTTP 方法和相對 URI 的組合。</span><span class="sxs-lookup"><span data-stu-id="17404-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="17404-167">例如，以下是一些不同的 Api:</span><span class="sxs-lookup"><span data-stu-id="17404-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="17404-168">GET /api/Products</span><span class="sxs-lookup"><span data-stu-id="17404-168">GET /api/Products</span></span>
- <span data-ttu-id="17404-169">GET /api/Products/{id}</span><span class="sxs-lookup"><span data-stu-id="17404-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="17404-170">POST /api/Products</span><span class="sxs-lookup"><span data-stu-id="17404-170">POST /api/Products</span></span>

<span data-ttu-id="17404-171">如果控制器動作支援多個 HTTP 方法， **ApiExplorer**視為不同的 API 中的每個方法。</span><span class="sxs-lookup"><span data-stu-id="17404-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="17404-172">若要隱藏的 API **ApiExplorer**，新增**ApiExplorerSettings**屬性設為動作和 set *IgnoreApi*設為 true。</span><span class="sxs-lookup"><span data-stu-id="17404-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="17404-173">您也可以將這個屬性加入到控制站，以排除整個控制器中。</span><span class="sxs-lookup"><span data-stu-id="17404-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="17404-174">ApiExplorer 類別取得文件字串，從**IDocumentationProvider**介面。</span><span class="sxs-lookup"><span data-stu-id="17404-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="17404-175">如您稍早所見，說明頁面的程式庫會提供**IDocumentationProvider** ，取得文件從 XML 文件字串。</span><span class="sxs-lookup"><span data-stu-id="17404-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="17404-176">程式碼位於 /Areas/HelpPage/XmlDocumentationProvider.cs。</span><span class="sxs-lookup"><span data-stu-id="17404-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="17404-177">您可以取得文件從其他來源藉由撰寫您自己**IDocumentationProvider**。</span><span class="sxs-lookup"><span data-stu-id="17404-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="17404-178">若要將其註冊，呼叫**SetDocumentationProvider**擴充方法，定義於**HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="17404-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="17404-179">**ApiExplorer**會自動呼叫**IDocumentationProvider**介面，以取得每個 API 的文件字串。</span><span class="sxs-lookup"><span data-stu-id="17404-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="17404-180">它會儲存在**文件**屬性**ApiDescription**並**ApiParameterDescription**物件。</span><span class="sxs-lookup"><span data-stu-id="17404-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17404-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17404-181">Next Steps</span></span>

<span data-ttu-id="17404-182">您不限於如下所示的 [說明] 頁。</span><span class="sxs-lookup"><span data-stu-id="17404-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="17404-183">事實上， **ApiExplorer**不限於建立 [說明] 頁面。</span><span class="sxs-lookup"><span data-stu-id="17404-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="17404-184">Yao Huang 連結已寫入一些很棒的部落格文章以取得您想要立即可用的：</span><span class="sxs-lookup"><span data-stu-id="17404-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="17404-185">將簡單的測試用戶端新增至 ASP.NET Web API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="17404-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="17404-186">進行 ASP.NET Web API 說明頁面在自我裝載的服務上運作</span><span class="sxs-lookup"><span data-stu-id="17404-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="17404-187">設計階段產生說明頁面 （或用戶端） 的 ASP.NET Web api</span><span class="sxs-lookup"><span data-stu-id="17404-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="17404-188">進階的說明頁面自訂</span><span class="sxs-lookup"><span data-stu-id="17404-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
